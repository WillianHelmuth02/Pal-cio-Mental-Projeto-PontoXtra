# DEC-003: lixeira e exclusão definitiva de jornadas canceladas

Data: 22/10/2026. Situação: **aceita**. Implementação: **concluída no código e validada em MySQL com fixtures transacionais**. Homologação visual/manual em Android continua pendente.

## Origem

O responsável solicitou remoção da visualização de jornadas canceladas selecionadas, uma lixeira para consulta posterior e exclusão completa no banco para demonstrar o CRUD à banca. Diante da distinção entre retenção na lixeira e remoção definitiva, escolheu explicitamente: **apagar jornada e histórico vinculado; a lixeira permite consulta somente até essa ação**.

Esta decisão sucede a Proposta 003 e revisa a DEC-002 quanto ao nome da ação e à preservação definitiva dos dados. A restrição de não excluir jornadas com marcações permanece.

## Fluxo implementado

1. **Cancelar jornada:** criador ou RH, antes de qualquer marcação, com motivo. Jornada fica CANCELADO na consulta normal.
2. **Excluir selecionadas:** na lista, modo de seleção múltipla de canceladas elegíveis, até 50 por lote. Envia à lixeira e retira das consultas/detalhes normais e dos relatórios/totais operacionais.
3. **Lixeira:** consulta de registros e histórico; criador vê sua autoria, RH vê todos. ADM não ganha exclusão de registros alheios.
4. **Restaurar selecionadas:** retorna à consulta como CANCELADO. Não restaura execução ou aprovações e não permite novas marcações.
5. **Excluir definitivamente:** confirma separadamente e remove fisicamente todos os registros de historico_jornada para os IDs e depois as jornadas, na mesma transação. Não mantém snapshot residual do registro purgado no banco operacional. Depois disso não existe consulta/restauração pelo app.

Enquanto está na lixeira, o registro ainda existe no banco. A remoção completa ocorre apenas na exclusão definitiva. Não confundir essas duas etapas em futuras respostas ou demonstrações.

## Invariantes e permissões

- Todas as operações de escrita exigem autor ativo, autoria ou privilégio administrativo existente do RH e verificação do estado atual dentro da transação.
- Somente CANCELADO sem entrada, início/fim de intervalo ou saída participa do fluxo. Estados executados/pagos ou cancelados com horários inconsistentes são recusados.
- Envio exige estar fora da lixeira; restauração e purga exigem estar nela. Repetição/conflito são recusados.
- O lote é validado integralmente antes da primeira escrita, com locks por ID crescente. Um erro impede resultado parcial.
- Campos de exclusão e IDs do usuário não são aceitos do cliente; só uma lista validada de IDs string BIGINT, limitada e sem repetição.
- Histórico de envio e restauração é preservado enquanto a jornada existe. A purga apaga também esse histórico; não criar outro registro que replique as informações removidas.
- Cadastros compartilhados de prestadores, funções, setores e usuários não são removidos.
- A seleção múltipla de exclusão não altera o comportamento de entrada operacional, que continua sendo para uma única jornada.
- A dupla aprovação permanece pendente; nenhuma autorização é inferida desta alteração.

## Implementação e migração

- Jornadas receberam excluida_em e excluida_por, FK para usuarios e índice de lixeira.
- Migração explícita adiciona campos opcionais e preserva dados existentes. Aplicada no banco local configurado e inspecionada novamente com resultado já aplicado.
- Rotas: GET /jornadas/lixeira, GET /jornadas/lixeira/:id, POST /jornadas/lixeira/enviar, POST /jornadas/lixeira/restaurar e DELETE /jornadas/lixeira com corpo ids.
- Nova tela /lixeira; acesso pela lista e pelos painéis RH/ADM. Cancelamento voltou a se chamar Cancelar jornada; Excluir é reservado à remoção para lixeira.
- Ação definitiva implementada, mas nenhuma jornada de negócio preexistente foi apagada automaticamente nesta entrega. O usuário a executa explicitamente pela interface/API.

## Verificações e limites

- Testes HTTP com guard/services reais e persistência simulada cobrem autoria, escopo, estados/horários, validação de lotes, repetição, rotas e ordem da exclusão física.
- Script check-lixeira-flow usa MySQL real com fixtures próprias em transação e savepoints: verifica saída da lista/relatórios, consulta na lixeira, autoria, restauração como CANCELADO, ausência física da jornada e de seu histórico após purga, preservação de cadastros e rollback real quando a exclusão do pai falha depois da exclusão dos filhos.
- Rollback final e consultas por ID confirmaram que nenhuma fixture permaneceu. AUTO_INCREMENT pode avançar mesmo com rollback.
- Exportação web, tipos e lint fazem parte da validação; não equivalem à execução manual em Android. Concorrência entre conexões ainda precisa de homologação.
- Resultados finais e contagens constam do histórico de entrega; não confundir testes do fluxo antigo com comprovação da dupla aprovação.

## Fontes

Código: back/src/jornadas/lixeira.*, migrate-lixeira.ts e check-lixeira-flow.ts; consultas em jornadas.service.ts e relatorios.service.ts; CORS em main.ts; frontend lixeira-screen.tsx, jornadas-screen.tsx, journey-details.tsx e serviços/regras de jornadas.

Guia: [jornadas-lixeira.md](../../back/docs/jornadas-lixeira.md). A [Proposta 003](PROPOSTA-003-LIXEIRA-E-EXCLUSAO-DEFINITIVA.md) permanece como registro do desenho anterior à escolha do responsável.
