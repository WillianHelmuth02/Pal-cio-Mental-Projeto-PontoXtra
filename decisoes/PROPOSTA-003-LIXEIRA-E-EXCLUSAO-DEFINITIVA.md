# Proposta 003: lixeira e exclusão definitiva de jornadas canceladas

Data: 22/10/2026. Situação: **substituída pela [DEC-003](DEC-003-LIXEIRA-E-EXCLUSAO-DEFINITIVA.md)**. O responsável escolheu apagar jornada e histórico na exclusão definitiva, e a implementação posterior está registrada naquela decisão. O restante deste arquivo preserva o desenho proposto originalmente, não o estado atual.

## Solicitação do responsável

Adicionar ação para jornadas selecionadas nas telas de consulta, permitindo excluir da visualização somente jornadas canceladas. Criar lixeira para consulta posterior. O responsável também solicitou remoção completa das informações da jornada no banco e aceitou sugestões, motivado pela necessidade de demonstrar o CRUD à banca.

## Distinção necessária

Uma lixeira consultável exige que seus dados continuem armazenados enquanto o registro estiver nela. A remoção completa do banco deve acontecer em etapa posterior. O histórico atual é uma tabela do mesmo banco (`historico_jornada`) e contém snapshots da jornada. Mantê-lo integralmente após a exclusão não equivale a apagar todas as informações da jornada.

Pendência apresentada ao responsável: na exclusão definitiva, remover também o histórico vinculado ou preservá-lo? A implementação de destruição/retencão depende dessa definição; não considerar esta proposta aceita por silêncio.

## Fluxo recomendado

| Ação visível | Condição | Efeito no banco e na interface |
| --- | --- | --- |
| Cancelar jornada | Criador ou RH, antes de qualquer marcação, conforme DEC-002 | Mantém a jornada e histórico; altera status para CANCELADO |
| Excluir selecionadas | Somente CANCELADO sem marcações, com permissão por registro | Move para lixeira; deixa de aparecer na consulta normal |
| Consultar lixeira | Registros na lixeira dentro das permissões do usuário | Permite visualizar antes da remoção definitiva |
| Restaurar da lixeira | Registro ainda existente na lixeira | Retorna à consulta como CANCELADO; nunca reabre a execução |
| Excluir definitivamente | Somente registro cancelado, sem marcações e já na lixeira | Recomendação: apaga histórico vinculado e jornada na mesma transação, sem restauração |

Recomendação de permissão: manter autoria ou privilégio administrativo do RH para todas as operações; ADM não recebe exclusão de jornadas alheias automaticamente. Acesso à lixeira não amplia permissão de escrita.

O botão de cancelamento atual é chamado Excluir jornada. Ao implantar este fluxo, renomeá-lo para Cancelar jornada e reservar Excluir para envio à lixeira, evitando duas ações diferentes com o mesmo nome. Registrar a evolução da DEC-002 após a decisão.

## Proposta de interface

Consulta: seleção múltipla com quantidade selecionada, ação Excluir selecionadas e acesso à Lixeira. Entrada operacional deve continuar inequívoca e utilizar uma única jornada; seleção múltipla não pode disparar eventos em lote.

Excluir selecionadas só fica habilitado quando todos os registros selecionados forem cancelados e o usuário tiver permissão. A API revalida cada ID, status, ausência de marcações e autoria dentro da transação. Em seleção incompatível, não apagar parcialmente o lote sem informar: preferir rejeitar o lote inteiro e explicar o impedimento.

Lixeira: lista própria com detalhes, restauração como CANCELADO e exclusão definitiva de registros selecionados. Mostrar claramente a diferença entre remover da lista e apagar definitivamente. Evitar remoção automática por prazo nesta primeira entrega, para manter a demonstração previsível.

## Impactos técnicos identificados

- Backend: endpoints de envio/restauração/purga e consulta de lixeira; validação de lote com limite; autorização por registro; locks e transações.
- Persistência: marcador de lixeira e metadados de envio, por exemplo excluida_em/excluida_por; definir contrato e migração preservando dados existentes.
- Consultas e relatórios: definir explicitamente exclusão da consulta normal e dos totais operacionais; consulta de lixeira separada. Canceladas fora da lixeira seguem a política atual até revisão.
- Exclusão física: o SQL atual tem chave estrangeira de historico_jornada para jornadas. Se aprovada a remoção total, excluir filhos e jornada na mesma transação, sem alterar prestadores, usuários, funções ou setores compartilhados.
- Caso seja escolhido preservar histórico: redesenhar o vínculo da auditoria, pois não basta apagar jornadas com a FK atual; documentar quais informações continuarão retidas.
- Frontend: substituir seleção única onde apropriado, preservar entrada operacional, incluir barra de ações e nova tela de lixeira.
- Documentos: revisar DEC-002, estado atual, guias, quadro e requisitos de auditoria. Exclusão definitiva fica restrita a canceladas sem eventos; jornadas executadas/pagas não entram nesse fluxo.

## Critérios de aceite propostos

1. Jornada ativa/iniciada/concluída/paga não pode ser enviada à lixeira nem purgada por esta funcionalidade.
2. Jornada cancelada autorizada pode ser selecionada e removida da consulta normal; aparece na lixeira após recarregar.
3. Restaurar devolve registro CANCELADO e preserva a consulta de seu histórico enquanto não houver purga.
4. Outro Operacional não altera jornada alheia; RH mantém o privilégio administrativo existente.
5. Se aprovada a remoção total, após a purga não existem a jornada nem linhas de historico_jornada para seu ID no banco operacional.
6. Falha de permissão, vínculo ou concorrência não deixa lote parcialmente apagado; testes devem verificar transação e consistência.
7. Registros compartilhados dos cadastros não são removidos.
8. A demonstração de criação, consulta, atualização e exclusão utiliza dados de teste e evidencia o efeito real no banco.

## Fontes conferidas

`front/src/components/jornadas-screen.tsx`: seleção única atual e registro de entrada.

`back/src/jornadas/jornadas.service.ts`: consulta normal atualmente inclui todos os estados, sem marcador de lixeira.

`BD/pontoxtra.sql` e `back/src/jornadas/historico-jornada.entity.ts`: histórico referenciado à jornada e snapshots no banco.

`Memoria_Projeto/decisoes/DEC-002-EXCLUSAO-PELO-CRIADOR.md`: cancelamento lógico atual preserva histórico e ainda não possui lixeira/purga.

## Limite desta entrega

A análise preparou o desenho para avaliação. Nenhum endpoint, schema ou dado de negócio foi alterado nesta proposta. Não foi executada exclusão no banco.
