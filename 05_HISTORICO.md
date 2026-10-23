# 05. Histórico de decisões e entregas

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
