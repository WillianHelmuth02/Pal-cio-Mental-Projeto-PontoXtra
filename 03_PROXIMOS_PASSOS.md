# 03. Próximos passos

Última atualização: 22/10/2026.

## Prioridade 1: alinhar o ciclo às duas aprovações

- Documentação da regra e da memória: concluída nesta tarefa.
- Implementação da nova regra: pendente; conferir a [DEC-001](decisoes/DEC-001-DUPLA-APROVACAO.md).
- Resolver políticas de reenvio, alteração após aprovação, legado, cancelamento e conflito de jornadas.
- Definir contrato de estados, endpoints e dados separados de cada decisão.
- Preparar migração preservando registros e auditoria; validar em base de teste antes de aplicar em base existente.
- Implementar criação pendente, decisão inicial do ADM e bloqueio de eventos no servidor.
- Separar a decisão de pagamento, preservando conferência, correção e quitação.
- Atualizar telas, mensagens, ações por perfil, filtros, painéis, totais e relatórios.
- Validar critérios de aceite da decisão, incluindo permissões, rejeição/correção, concorrência e auditoria.

Não marcar essa prioridade como concluída pela mera existência da especificação. Registrar evidências de execução quando houver implementação.

## Prioridade 2: concluir a interface do MVP

- RF03: manutenção de prestadores pelo RH.
- RF04: manutenção de funções, setores e valores/hora.
- RF15/RF16: relatório por período e totais consolidados, incluindo as duas etapas de autorização.

## Prioridade 3: validação e operação

- Roteiro integrado com Operacional, RH e ADM e dados de teste conhecidos.
- Testes em Android 9 e versão recente; rede real de aparelho.
- Concorrência entre conexões e resposta perdida após commit.
- HTTPS e política de fuso consistente.
- Backup diário, retenção mínima de sete cópias e restauração demonstrada.
- Medição do requisito de 95% das respostas em até dez segundos.

## Prioridade 4: entrega acadêmica

- Atualizar artigo/requisitos, dicionário, diagrama, protótipos e roteiro de demonstração.
- Reconciliar unicidade do documento, valor/hora derivado da função e cancelamento.
- Substituir READMEs genéricos por instruções de instalação e execução do PontoXtra.
- Distinguir resultados demonstrados de etapas futuras; não extrapolar o alcance dos testes existentes.

Não há cronograma de disciplina validado nesta memória. Não assumir datas ou percentuais de conclusão sem fonte.
