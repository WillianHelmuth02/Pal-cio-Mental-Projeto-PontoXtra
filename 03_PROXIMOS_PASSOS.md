# 03. Próximos passos — 28/10/2026

Cadastros RH, contas ADM e relatórios estão entregues no código. Planejamentos anteriores preservados em [arquivo histórico](03_PROXIMOS_PASSOS_HISTORICO_ATE_28_10_2026.md). Não reiniciar a implementação já concluída.

1. Regularizar tipos frontend em app-tabs, jornadas-screen e use-theme e compatibilidade ESLint 10/plugin React. Hoje os scripts e o bundle passam, mas os dois checks globais não.
2. Homologar os cinco módulos e o ciclo completo com Operacional/RH/ADM, seguindo [roteiro integrado](../Documentos/ROTEIRO_HOMOLOGACAO.md). Conferir permissões, contatos vazios, valores históricos, sessões revogadas, duas decisões, correção, lixeira e relatórios com mais de 50 itens.
3. Preparar API acessível por aparelho/HTTPS e APK de teste; habilitar worker no ambiente autorizado e validar push aberto/fechado, toque, logout e troca de conta. Código/mock não comprova entrega.
4. Validar concorrência entre conexões, resposta perdida após commit, fuso/relógio, recuperação de migração e desempenho.
5. Demonstrar backup diário, retenção de sete cópias e restauração.
6. Usar a revisão atual de [documentação](../Documentos/LEIA_PRIMEIRO.md) na apresentação; se for exigida nova diagramação acadêmica em PDF, produzir novas edições a partir da especificação atual, preservando originais e sem inventar assinaturas/prazos.
7. Avaliar depois, conforme necessidade: sessões persistentes, paginação da lista principal, recuperação autônoma de senha, exportação de relatórios e outros recursos fora do fluxo atual. Não marcar propostas como aprovadas.

Não há prazo ou percentual de conclusão validado. GT-05/06 possuem código entregue; homologação continua pendente e o quadro permanece proposta de acompanhamento.

## Atualização — rede local (28/10/2026)

Etapas 1–3 da preparação de rede concluídas nesta execução; usuário confirmou acesso nos dois aparelhos. URL e HTTP de preview corrigidos/validados no código e bundle. Próximo passo: autorizar explicitamente envio do frontend/configuração à Expo/EAS, gerar novo APK e testar login/dados instalados. API ativa depende do PC ligado; IP atual 192.168.0.119. Push continua desabilitado/não homologado. Detalhes em [08_ANDROID_REDE_LOCAL.md](08_ANDROID_REDE_LOCAL.md).

## Atualização — push real (28/10/2026)

Primeiro recebimento nativo com som ou vibração confirmado pelo usuário após habilitar worker. Prosseguir com demais aparelhos/perfis, app em segundo plano/encerrado, toque no aviso e troca de conta; não repetir habilitação como pendência local. Ver 08_ANDROID_REDE_LOCAL.md.

