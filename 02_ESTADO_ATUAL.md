# 02. Estado atual e diferença para a regra vigente

**Entrega de código em 23/10/2026 — notificações:** avisos internos com contador/leitura, cadastro de dispositivos, fila push Expo com recibos e integração com saída/conferência/decisão de pagamento implementados. Frontend configurado para Firebase e SDK 57. 487 testes backend aprovados; build/lint, tipos, scripts frontend e exportação web aprovados. MySQL real validou fixtures e cascata na purga com rollback. Push no aparelho ainda não homologado; worker depende de PUSH_NOTIFICATIONS_ENABLED=true. Aprovação inicial continua pendente. Esta atualização supera a descrição de dependências ausentes no parágrafo de preparação abaixo. Ver [07_NOTIFICACOES_CONFIGURACAO.md](07_NOTIFICACOES_CONFIGURACAO.md).

**23/10/2026 — notificações:** projeto Expo vinculado ao frontend, pacote Android e eas.json configurados; FCM V1 cadastrado pelo responsável na EAS. google-services.json presente, mas ainda sem googleServicesFile no app.json; expo-notifications ausente do package.json. Usuário informou reversão da implementação anterior. Infraestrutura parcial não comprova dupla aprovação ou push funcionando. Ver [registro de configuração](07_NOTIFICACOES_CONFIGURACAO.md). Banco não foi inspecionado nesta etapa; reversão do código não comprova reversão de migrações.

Última inspeção de código: 22/10/2026. Backend: d8da016. Frontend: 531e654.

**Atualização posterior em 22/10/2026:** os commits acima identificam a avaliação inicial. A exclusão lógica pelo criador foi implementada em alterações locais posteriores, conforme a [DEC-002](decisoes/DEC-002-EXCLUSAO-PELO-CRIADOR.md). A autoria é validada no servidor; a ação exige ausência de qualquer marcação. RH mantém seu cancelamento administrativo. Verificações desta entrega: 402 testes do backend, build e lint aprovados; tipos, lint e dois scripts do frontend aprovados. Não houve migração nem escrita em dados reais; tela não foi validada manualmente com login nesta entrega.

## Requisito vigente versus implementação

**Atualização de exclusão:** [DEC-003](decisoes/DEC-003-LIXEIRA-E-EXCLUSAO-DEFINITIVA.md) implementada após a DEC-002: cancelamento e envio à lixeira são ações distintas; canceladas selecionadas saem da consulta normal, podem ser consultadas/restauradas na lixeira e podem ser apagadas definitivamente junto do histórico. Campos de lixeira e FK/índice foram adicionados por migração no banco local sem apagar dados existentes. Integração MySQL com fixtures confirmou purga física e rollback; nenhuma fixture permaneceu. Detalhes e relatórios normais excluem a lixeira. Dupla aprovação continua pendente.

**A dupla aprovação foi aceita como regra de produto, mas ainda não foi implementada.** O código inspecionado cria jornadas em EM_ANDAMENTO e permite eventos antes de qualquer decisão do ADM. A autorização atualmente existente ocorre apenas depois da saída e da conferência do RH, para liberar o registro do pagamento.

Portanto, o sistema atual não atende à aprovação prévia exigida pela [DEC-001](decisoes/DEC-001-DUPLA-APROVACAO.md). Não afirmar que há duas aprovações só porque a documentação já foi atualizada.

## Já implementado no código examinado

- Autenticação de usuários ativos; senhas com scrypt; tokens com expiração; logout com revogação e permissões no servidor.
- Início e ações por perfil; criação, filtros e detalhes de jornadas.
- Entrada, início/fim de intervalo e saída com horário do servidor; cálculo líquido e monetário.
- Conferência pelo RH, decisão posterior do ADM, correção com recálculo e registro de pagamento pelo RH.
- Histórico com autor, instante e snapshots; transações e locks nas operações de jornadas.
- APIs de manutenção de prestadores, funções e setores, com alterações reservadas ao RH.
- APIs de relatório por período e totais por status; painéis usam parte dos totais.
- Exclusão lógica pelo criador antes de marcações e cancelamento administrativo pelo RH; auditoria preservada e estado CANCELADO.

## Lacunas conhecidas

- Aprovação da realização antes da entrada e separação persistida das duas decisões do ADM.
- Telas de manutenção de prestadores, funções e setores.
- Tela de relatório por período e visão consolidada dos totais.
- Homologação em Android, validação integrada do ciclo completo e concorrência real entre conexões.
- Evidências de HTTPS implantado, desempenho e backup diário com sete cópias e restauração.
- Reconciliação do artigo, requisitos, diagrama e dicionário com as decisões posteriores.

## Verificações realizadas na avaliação de 22/10/2026

Backend: 390 testes aprovados, build e lint aprovados. Um teste E2E aprovado, limitado à rota GET /; não cobre o ciclo completo do negócio. Frontend: checagem de tipos, lint e scripts test-api.cjs e test-jornadas.cjs aprovados.

MySQL: conexão confirmada, seis tabelas e ENUM com sete estados, incluindo CANCELADO. Consultas reais de relatórios executaram sem erro; não houve reconciliação dos valores com fixtures esperadas. Acesso de avaliação foi somente leitura.

Esses resultados antecedem a implementação da dupla aprovação; não são evidência de teste do novo fluxo.

## Decisões e ambiguidades a preservar

- Documento do prestador: implementação exige unicidade global; RN04 do artigo fala em ativos, enquanto seu dicionário declara UNIQUE. Regra final precisa ser harmonizada.
- Valor/hora: criação copia o preço da função; não recebe preço livre. RH pode corrigir o histórico nos status permitidos.
- Fuso: interface usa Brasília UTC-03; backend depende do ambiente/conexão. Não foi localizada configuração organizacional de fuso.
- Sessões em memória: reinício do backend invalida tokens; recarga do frontend exige novo login.
- Banco físico enxuto: seis tabelas, diferente do diagrama ampliado. Precisa de justificativa formal.

## Regra de atualização desta sala

Só mudar a dupla aprovação para implementada após registrar arquivos alterados, migração, verificações e limites remanescentes. Manter o relatório anterior como avaliação histórica e explicitar sua ressalva posterior.
