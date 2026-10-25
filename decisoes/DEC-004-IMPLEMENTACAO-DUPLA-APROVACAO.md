# DEC-004: implementação da dupla aprovação e políticas complementares

Data: 24/10/2026. Origem: autorização explícita do responsável para executar a DEC-001 após preparar notificações. Situação: DEC-001 implementada no código; escolhas complementares de implementação documentadas abaixo, sem nova regra aprovada em pergunta separada. Responsável pode solicitar revisão dessas escolhas.

## Comportamento entregue

- Criação por RH/Operacional fica AGUARDANDO_AUTORIZACAO_REALIZACAO. ADM ativo aprova ou rejeita com motivo; ações auditadas, com lock e transação.
- Aprovação inicial muda para AUTORIZADA_PARA_REALIZACAO; entrada pelo Operacional muda para EM_ANDAMENTO. Entrada sem decisão válida é recusada inclusive por API direta.
- Saída calcula e encaminha ao RH; conferência encaminha ao ADM para pagamento. AUTORIZADO/REJEITADO continuam exclusivamente estados da decisão de pagamento. RH registra quitação apenas após essa segunda aprovação.
- Campos realizacao_decidida_por/em e justificativa_rejeicao_realizacao separam a primeira decisão dos campos decidida_por/em e justificativa_rejeicao, preservados para pagamento. Correção não apaga a primeira aprovação; invalida conferência e decisão de pagamento da versão anterior. Entrada corrigida não antecede a primeira aprovação, salvo legado identificado.
- Avisos internos e fila push conectados a pendência e decisão das duas aprovações. Criador/RH recebem decisões, ADM recebe pendências, excluindo o autor da ação. Push em aparelho ainda não homologado.

## Escolhas complementares

1. Não foi criado editor/reenvio de planejamento. Realização rejeitada: criador/RH pode cancelar e criar outra jornada. Mudar planejamento aprovado também exige cancelamento/recriação antes das marcações, preservando a regra de nova aprovação.
2. Uma jornada pendente, liberada ou em execução reserva o prestador. Mantida a restrição do MVP, sem agendamento múltiplo. Rejeição de realização/cancelamento libera a reserva.
3. Cancelamento continua por criador/RH antes de qualquer marcação, agora incluindo os três estados de realização. Lixeira e purga continuam exclusivas de CANCELADO sem marcações, conforme DEC-003.
4. Legado iniciado pode continuar com flag explícito legado_sem_aprovacao_previa; não recebe decisão fictícia. Flag não autoriza nova entrada. Dados antigos inconsistentes continuam sujeitos a validação de horários/totais.

## Banco e implantação

Schema local já tinha ENUM e quatro colunas da tentativa anterior. Migração db:aprovacoes inspecionou, preparou mapeamento/controle com marcador 20261024_dupla_aprovacao e preservou a contagem (3 jornadas antes/depois). Sem recriação de banco ou remoção de linhas. Reexecução idempotente. EM_ANDAMENTO sem marcações vira pendente; iniciadas/encerradas sem primeira aprovação preservam estado e recebem flag de legado. Nenhuma primeira decisão foi preenchida retroativamente.

Executar em outros ambientes com API parada. DDL tem commit implícito; não prometer recuperação automática de schema. Não usar BD/pontoxtra.sql como migração. Migrações e preparação do banco são independentes de reverter arquivos no Git.

## Evidências e limites

533 testes backend aprovados após adaptações e novos casos de decisões, perfis, rejeição, repetição, legado e migração. MySQL real validou ciclo de duas aprovações, impedimento de entrada/pagamento, preservação da primeira decisão na correção e avisos; fixtures revertidas. Fluxos de lixeira e notificações também passaram com rollback. Testes de concorrência real entre conexões e homologação visual/mobile ainda pertencem a GT-07.

Fontes: back/src/jornadas/jornadas.aprovacao.ts, aprovacoes.migration.ts, aprovacoes.spec.ts, jornadas.fluxo.ts, jornadas.eventos.ts e jornadas.service.ts; frontend src/utils/jornadas.ts e componentes de criação, detalhe, lista e painel. Guia: [jornadas-aprovacoes.md](../../back/docs/jornadas-aprovacoes.md).
