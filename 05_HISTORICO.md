# 05. Histórico de decisões e entregas

## 23/10/2026 - Implementação de notificações internas e suporte push

- Implementados módulo autenticado de notificações, persistência/fila transacional, worker Expo com recibos, leitura por destinatário e gestão de dispositivos. Avisos atuais: saída, conferência e autorização/rejeição de pagamento. Contratos para aprovação inicial preparados; fluxo inicial não foi implementado nesta entrega.
- Tela /notificacoes e contador, ativação por permissão explícita, registro automático quando já autorizado, desassociação no logout e abertura da jornada ao tocar no push. Configurados expo-notifications e googleServicesFile; .gitignore protege JSONs privados usuais.
- Schema existente inspecionado/preparado; MySQL real com fixtures verificou leitura/propriedade/lixeira/cascata de purga e rollback. Dados temporários não permaneceram; nenhum push externo foi enviado.
- 487 testes backend aprovados, build/lint e tipos/lint frontend aprovados, scripts API/jornadas/push e exportação web aprovados. Push nativo validado com SDK simulado, sem homologação física. .env real preservado; habilitação do worker, assinatura e APK permanecem pendentes.
- Criado back/docs/notificacoes.md e atualizadas memória, estado e próximos passos. Não iniciado build remoto nem publicação.


## 23/10/2026 - Preparação Expo/EAS e Firebase para notificações

- Responsável informou reversão da implementação anterior e realizou configuração assistida: login EAS, vínculo ao projeto Expo existente, slug pontoxtra, geração de eas.json e pacote com.pontoxtra.mobile.
- Criou projeto Firebase e aplicativo Android; enviou conta de serviço pelo EAS CLI, que confirmou atribuição FCM V1 ao pacote correto. Não foi configurado FCM Legacy nem submissão à loja.
- Arquivos app.json/eas.json conferidos; google-services.json presente, mas ligação googleServicesFile e dependência expo-notifications ainda ausentes. Sem leitura de credenciais privadas, teste de envio, build ou alteração de código nesta entrega documental.
- Criado 07_NOTIFICACOES_CONFIGURACAO.md com resumo, tarefas e limites; índice, estado atual e próximos passos atualizados. Situação: infraestrutura parcial, recurso ainda não homologado.


## 22/10/2026 - DEC-003: lixeira e remoção completa no banco

- Responsável escolheu explicitamente apagar jornada e histórico vinculado na exclusão definitiva; consulta na lixeira somente até essa ação.
- Implementados seleção de canceladas em lote, envio à lixeira, consulta de detalhes/histórico, restauração como Cancelado e DELETE definitivo. Cancelar e Excluir passaram a ser ações distintas.
- Aplicada migração local de campos opcionais, FK e índice, sem apagar jornadas existentes; inspeção posterior confirmou idempotência.
- Criador ou RH pode gerenciar os registros; outras jornadas/estados/marcações são recusados e lote inválido não é executado parcialmente.
- Consulta normal, detalhes e relatórios/totais não incluem registros na lixeira.
- Verificações: 445 testes do backend aprovados, mais um E2E básico; build/lint aprovados. Frontend: tipos, lint, test-api e test-jornadas aprovados; exportação web com a rota /lixeira concluída.
- Integração MySQL real verificou envio, retirada da lista e dos relatórios, consulta, autoria, restauração, purga física de filhos/pai e rollback após falha na exclusão do pai. Fixtures próprias foram revertidas e sua ausência foi confirmada por ID; registros preexistentes não foram excluídos.
- Tela não foi validada manualmente com login real em Android; concorrência entre conexões continua pendente. A dupla aprovação não foi implementada por esta entrega.

## 22/10/2026 - Proposta de lixeira e exclusão definitiva

- Responsável solicitou exclusão da visualização de jornadas canceladas selecionadas, consulta posterior em lixeira e remoção completa no banco, aceitando sugestões.
- Conferidos seleção única atual, consultas, histórico e chave estrangeira para jornadas.
- Preparada proposta em duas etapas: Excluir envia à lixeira; Excluir definitivamente remove fisicamente depois.
- Apresentada decisão de retenção ao responsável: apagar ou preservar histórico na purga. Proposta permanece em avaliação até a resposta.
- Código, schema e dados de negócio não foram alterados por essa análise.

## 22/10/2026 - DEC-002 e exclusão lógica pelo criador

- Responsável confirmou exclusão somente antes da entrada, preservando o histórico.
- Implementado acesso do criador à operação existente de cancelamento, mantendo a permissão administrativa do RH.
- Backend revalida autoria e usuário ativo sob transação; mantém bloqueio de qualquer marcação e dos estados incompatíveis.
- Interface mostra Excluir jornada nos detalhes, com motivo e confirmação; contrato agora inclui criada_por e a matriz de ações recebe o ID do usuário.
- Atualizados testes, documentação, estado atual e quadro proposto. Dupla aprovação permanece pendente.
- Verificação: 402 testes do backend, build e lint aprovados; tipos, lint e dois scripts do frontend aprovados. Não houve migração ou escrita de negócio no banco real, nem teste manual da tela. Testes de persistência são simulados.

## 22/10/2026 - Proposta de quadro hierárquico

- O responsável pediu uma lista completa do que foi feito, está em andamento e falta fazer, com três níveis: grandes tarefas, tarefas e subtarefas.
- Criada a proposta `06_QUADRO_DE_TAREFAS_PROPOSTA.md`, preenchida com o estado já documentado e as pendências conhecidas.
- Quadro inclui IDs, prioridades, dependências, pontos em aberto, critérios de conclusão e modelo de ficha de acompanhamento.
- Formato apresentado para avaliação antes de consolidá-lo como quadro oficial; listas existentes foram preservadas.
- Trabalho atual é documental. Nenhuma tarefa de implementação listada foi iniciada por esta entrega.

## 22/10/2026 - Avaliação do estado do projeto

- Comparação da implementação com o artigo de pré-banca, antes da nova decisão de negócio.
- Produzidos relatório Markdown e PDF com 16 requisitos funcionais, 12 não funcionais, regras, evidências e próximos passos.
- Backend: 390 testes, um E2E básico, build e lint aprovados. Frontend: tipos, lint e dois scripts aprovados.
- Banco consultado em leitura; conexão, tabelas, estado CANCELADO e consultas de relatório confirmados.

## 22/10/2026 - DEC-001 e criação da memória do projeto

- O responsável determinou duas decisões do ADM: autorização da realização após criação e autorização do pagamento após execução.
- O responsável confirmou que esta etapa deve apenas documentar e organizar a memória; a implementação fica para outra entrega.
- Registrada decisão aceita, invariantes, proposta de estados, critérios de aceite, impacto e questões em aberto.
- Criada a pasta Memoria_Projeto, com contexto geral, estado atual, fontes e próximos passos.
- Adicionados pontos de entrada em AGENTS.md na raiz e nos módulos para orientar futuras sessões e outras IAs.
- Documentação técnica e relatório anterior receberam avisos sobre a mudança de regra.
- Código executável, schema e dados de negócio não foram alterados por esta entrega documental. A dupla aprovação continua pendente de implementação.
- Validação documental: 22 arquivos Markdown inspecionados, nenhum link local ausente entre os links encontrados; diffs sem erros de espaços. Relatório atualizado continua com sete páginas e sua ressalva foi verificada no texto e visualmente. Testes anteriores não validam a nova regra.
