# Quadro de tarefas do PontoXtra

**Situação deste documento: proposta de organização, aguardando avaliação do responsável.**

Atualização: 22/10/2026. Base inicial: avaliação local e memória do projeto da mesma data. Atualizações posteriores: T-04.05 registra cancelamento pelo criador; T-04.06 registra seleção, lixeira e exclusão física de jornada/histórico, implementados após a primeira proposta do quadro. O formato do quadro continua em avaliação.

## 1. Como funciona

Exatamente três níveis de trabalho:

1. **Grande tarefa (GT):** uma entrega ampla do projeto, por exemplo, implantar as duas aprovações.
2. **Tarefa (T):** uma parte dessa entrega, por exemplo, adaptar o backend.
3. **Subtarefa (ST):** uma ação verificável, por exemplo, bloquear entrada sem autorização prévia.

Os IDs permanecem estáveis ao reorganizar a ordem. Exemplo: GT-03 → T-03.02 → ST-03.02.01.

### Estados

| Estado | Significado |
| --- | --- |
| Feito | Existe entrega ou evidência identificada, dentro do escopo descrito |
| Em andamento | Existe trabalho realmente iniciado e ainda não finalizado |
| A fazer | Trabalho ainda pendente, mesmo que seja prioritário ou tenha partes prontas |

"Parcial", "aguardando decisão" e "bloqueado" são observações, não novos estados. Cada bloqueio registra motivo e condição de liberação. Um item prioritário não vira automaticamente "em andamento".

Uma grande tarefa ou tarefa só fica **Feito** quando todos os itens necessários estiverem concluídos e seu critério de aceite tiver evidência. Se há partes prontas e pendências sem trabalho ativo, o estado da entrega é **A fazer**, com observação de entrega parcial. Isso evita confundir software parcialmente entregue com trabalho atualmente em execução.

Datas de conclusão, responsáveis por execução e prazos não conhecidos ficam como "não definido"; não inventar cronograma. A data deste quadro não significa que todas as implementações foram feitas nessa data.

## 2. Visão geral das grandes tarefas

| ID | Grande tarefa | Estado | Prioridade | Situação real |
| --- | --- | --- | --- | --- |
| GT-01 | Base técnica e acesso | Feito | Base existente | Implementação observada; homologação fica em GT-07 |
| GT-02 | Memória e organização do projeto | Em andamento | Atual | Memória criada; formato do quadro em avaliação |
| GT-03 | Duas aprovações do ADM | A fazer | P1 | Regra documentada; implementação não iniciada nesta entrega |
| GT-04 | Adequar o núcleo de jornadas | A fazer | P1, junto de GT-03 | Fluxo anterior existe; integração ao novo ciclo pendente |
| GT-05 | Completar cadastros do RH | A fazer | P2 | APIs existentes; telas pendentes |
| GT-06 | Completar relatórios e indicadores | A fazer | P2 | APIs e parte dos painéis existentes; entrega incompleta |
| GT-07 | Homologar qualidade e aplicativo Android | A fazer | P3 | Verificações existentes são parciais; novo fluxo não testado |
| GT-08 | Preparar implantação e operação | A fazer | P3 | HTTPS, backups, fuso e desempenho precisam de evidências |
| GT-09 | Atualizar entrega acadêmica e técnica | A fazer | P4 | Documentos de referência existem; revisão final pendente |

### O que está sendo acompanhado agora

- T-02.03: apresentar e revisar esta proposta de quadro com o responsável.
- Nenhuma implementação da dupla aprovação está em andamento nesta etapa documental.
- Entrega posterior concluída: T-04.05, exclusão lógica pelo criador antes de marcações. A implementação das duas aprovações continua pendente.

### Próxima entrega sugerida

Após avaliar a organização da memória, a próxima frente técnica é GT-03, começando pelas decisões de domínio em T-03.01. Os pontos ainda indefinidos não precisam impedir tarefas independentes de análise e preparação.

## 3. Detalhamento das grandes tarefas

## GT-01. Base técnica e acesso

**Estado:** Feito, no escopo da implementação já observada. **Evidências:** [estado atual](02_ESTADO_ATUAL.md) e [mapa de fontes](04_MAPA_DE_FONTES.md). Não representa homologação em produção ou Android.

### T-01.01. Estruturar os módulos da aplicação — Feito

- [x] ST-01.01.01 — Manter frontend Expo/React Native com TypeScript e rotas.
- [x] ST-01.01.02 — Manter backend NestJS/TypeScript com serviços e persistência separados.
- [x] ST-01.01.03 — Integrar API ao MySQL com TypeORM.

### T-01.02. Implementar autenticação e separação de perfis — Feito

- [x] ST-01.02.01 — Permitir login de usuários ativos e logout com revogação.
- [x] ST-01.02.02 — Armazenar senhas com hash e usar tokens com expiração.
- [x] ST-01.02.03 — Validar permissões de Operacional, RH e ADM no servidor.
- [x] ST-01.02.04 — Exibir início e ações compatíveis com o perfil no frontend.

### T-01.03. Preservar estruturas centrais e acesso à API — Feito

- [x] ST-01.03.01 — Implementar as seis entidades centrais do modelo enxuto.
- [x] ST-01.03.02 — Disponibilizar cliente HTTP autenticado com tratamento de erros.
- [x] ST-01.03.03 — Confirmar conexão MySQL em leitura na avaliação de 22/10/2026.

**Critério de conclusão:** estrutura existente inspecionada e verificações básicas registradas. O modelo precisará evoluir em GT-03; a existência desta base não conclui essa evolução.

## GT-02. Memória e organização do projeto

**Estado:** Em andamento. **Prioridade:** Atual. **Responsável pela avaliação do formato:** responsável pelo projeto. **Prazo:** não definido.

### T-02.01. Criar a memória compartilhada — Feito

- [x] ST-02.01.01 — Criar pasta com índice e protocolo de consulta.
- [x] ST-02.01.02 — Registrar contexto, arquitetura e limites do MVP.
- [x] ST-02.01.03 — Registrar estado atual, evidências, lacunas e próximos passos.
- [x] ST-02.01.04 — Criar mapa de fontes e histórico de alterações.

### T-02.02. Registrar a decisão das duas aprovações — Feito

- [x] ST-02.02.01 — Documentar a regra aceita na DEC-001.
- [x] ST-02.02.02 — Diferenciar aprovação de realização e aprovação de pagamento.
- [x] ST-02.02.03 — Documentar impactos, critérios de aceite e questões em aberto.
- [x] ST-02.02.04 — Sinalizar o fluxo antigo nos guias e no relatório anterior.
- [x] ST-02.02.05 — Adicionar apontadores da memória aos AGENTS.md dos módulos e da raiz.

### T-02.03. Definir o quadro hierárquico de acompanhamento — Em andamento

- [x] ST-02.03.01 — Preparar proposta com grandes tarefas, tarefas e subtarefas.
- [x] ST-02.03.02 — Preencher feitos e pendências com base na memória disponível.
- [ ] ST-02.03.03 — **Em andamento:** submeter o formato à avaliação do responsável.
- [ ] ST-02.03.04 — **A fazer:** incorporar os ajustes solicitados.
- [ ] ST-02.03.05 — **A fazer:** consolidar a versão aceita como quadro oficial e apontar a consulta nos AGENTS.md.

### T-02.04. Estabelecer manutenção entre sessões — A fazer

- [ ] ST-02.04.01 — **A fazer:** confirmar o formato de registro de responsável, datas, bloqueios e evidências.
- [ ] ST-02.04.02 — **A fazer:** definir a relação entre quadro, próximos passos e histórico, evitando listas concorrentes.
- [ ] ST-02.04.03 — **A fazer:** consolidar a orientação para toda IA atualizar estado, evidência e próxima ação ao encerrar trabalho.

**Critério de conclusão:** responsável aceita o formato; quadro oficial está acessível, coerente com a memória e acompanhado por instruções de manutenção.

## GT-03. Duas aprovações do ADM

**Estado:** A fazer. **Prioridade:** P1. **Referência:** [DEC-001](decisoes/DEC-001-DUPLA-APROVACAO.md). **Responsável pela implementação:** não definido.

### T-03.01. Fechar as regras de domínio ainda abertas — A fazer

- [ ] ST-03.01.01 — **A fazer:** definir edição e reenvio após rejeição da realização.
- [ ] ST-03.01.02 — **A fazer:** definir quais alterações antes da entrada invalidam a aprovação inicial.
- [ ] ST-03.01.03 — **A fazer:** definir tratamento das jornadas legadas sem aprovação prévia.
- [ ] ST-03.01.04 — **A fazer:** definir cancelamento nos novos estados sem marcações.
- [ ] ST-03.01.05 — **A fazer:** definir conflito entre jornadas planejadas, autorizadas e em execução.

**Dependência:** decisões do responsável para as políticas indefinidas. **Resultado esperado:** complementar a DEC-001 sem apresentar propostas técnicas como regras já aceitas.

### T-03.02. Projetar estados, contratos e persistência — A fazer

- [ ] ST-03.02.01 — **A fazer:** definir nomes inequívocos para as duas etapas de aprovação/rejeição.
- [ ] ST-03.02.02 — **A fazer:** definir ações de API, respostas e permissões por etapa.
- [ ] ST-03.02.03 — **A fazer:** separar autor, instante, resultado e justificativa das duas decisões.
- [ ] ST-03.02.04 — **A fazer:** planejar histórico e referências à versão aprovada da jornada.

### T-03.03. Preparar e validar migração do banco — A fazer

- [ ] ST-03.03.01 — **A fazer:** escrever migração explícita preservando registros e auditoria.
- [ ] ST-03.03.02 — **A fazer:** mapear estados antigos sem criar aprovações prévias fictícias.
- [ ] ST-03.03.03 — **A fazer:** validar a migração e a recuperação em base de teste.
- [ ] ST-03.03.04 — **A fazer:** documentar procedimento e condições para aplicação na base existente.

**Dependências:** T-03.01 e T-03.02. Não executar BD/pontoxtra.sql como migração.

### T-03.04. Implementar as duas decisões no backend — A fazer

- [ ] ST-03.04.01 — **A fazer:** criar jornada pendente de autorização da realização.
- [ ] ST-03.04.02 — **A fazer:** permitir decisão inicial somente ao ADM ativo.
- [ ] ST-03.04.03 — **A fazer:** impedir eventos sem aprovação prévia válida, inclusive via API direta.
- [ ] ST-03.04.04 — **A fazer:** manter segunda decisão do ADM após encerramento e conferência do RH.
- [ ] ST-03.04.05 — **A fazer:** preservar primeira decisão quando houver rejeição/correção do pagamento.
- [ ] ST-03.04.06 — **A fazer:** registrar ambas as decisões com transação, locks e auditoria.

### T-03.05. Implementar as duas etapas no aplicativo — A fazer

- [ ] ST-03.05.01 — **A fazer:** informar, após a criação, que a jornada aguarda autorização para ocorrer.
- [ ] ST-03.05.02 — **A fazer:** exibir ao ADM pendências e ações distintas de realização e pagamento.
- [ ] ST-03.05.03 — **A fazer:** bloquear ações operacionais enquanto a realização não estiver autorizada.
- [ ] ST-03.05.04 — **A fazer:** apresentar separadamente as decisões e justificativas no detalhe/histórico.
- [ ] ST-03.05.05 — **A fazer:** atualizar contratos, rótulos, filtros e mensagens do novo ciclo.

**Critério de conclusão:** critérios da DEC-001 demonstrados em banco, API e interface, com evidências dos testes. Documentação sozinha não conclui esta grande tarefa.

## GT-04. Adequar o núcleo de jornadas

**Estado:** A fazer, com implementação anterior existente. **Prioridade:** P1, junto de GT-03. **Observação:** adaptar e validar o que já existe, evitando reescrever sem necessidade.

### T-04.01. Adequar criação e início efetivo — A fazer

- [x] ST-04.01.01 — Criar jornada para prestador, função e setor ativos, com preço histórico da função, no fluxo anterior.
- [x] ST-04.01.02 — Impedir duas jornadas efetivamente em andamento para o mesmo prestador no fluxo anterior.
- [ ] ST-04.01.03 — **A fazer:** aplicar os critérios de conflito definidos em T-03.01 aos novos estados.
- [ ] ST-04.01.04 — **A fazer:** distinguir criação, autorização para realização e início efetivo pela entrada.

### T-04.02. Integrar eventos e cálculo ao novo ciclo — A fazer

- [x] ST-04.02.01 — Registrar entrada, início/fim do intervalo e saída com horário do servidor.
- [x] ST-04.02.02 — Validar ordem temporal, intervalo opcional e cálculo líquido/monetário.
- [ ] ST-04.02.03 — **A fazer:** integrar as regras existentes ao novo estado autorizado para realização, em conjunto com T-03.04.
- [ ] ST-04.02.04 — **A fazer:** validar encerramento e encaminhamento ao RH sem pular a segunda aprovação.

### T-04.03. Preservar conferência, correção e pagamento — A fazer

- [x] ST-04.03.01 — Conferir, rejeitar, corrigir, recalcular, autorizar e registrar pagamento no ciclo anterior.
- [ ] ST-04.03.02 — **A fazer:** preservar a autorização de realização nas correções posteriores.
- [ ] ST-04.03.03 — **A fazer:** exigir nova autorização de pagamento quando a versão conferida for corrigida.
- [ ] ST-04.03.04 — **A fazer:** demonstrar que pagamento exige segunda aprovação, sem herdar a primeira.

### T-04.04. Adequar cancelamento e consultas — A fazer

- [x] ST-04.04.01 — Cancelar jornada sem marcações com motivo e histórico no ciclo anterior.
- [x] ST-04.04.02 — Consultar lista, detalhes e histórico com filtros no ciclo anterior.
- [ ] ST-04.04.03 — **A fazer:** aplicar a política de cancelamento aos novos estados.
- [ ] ST-04.04.04 — **A fazer:** revisar ações disponíveis e histórico de todas as transições.

### T-04.05. Permitir exclusão lógica pelo criador antes da entrada — Feito

- [x] ST-04.05.01 — Registrar a escolha do responsável e as regras na DEC-002.
- [x] ST-04.05.02 — Validar no backend autoria, usuário ativo e ausência de marcações; preservar permissão administrativa do RH.
- [x] ST-04.05.03 — Oferecer Excluir jornada nos detalhes, com justificativa, confirmação e verificação do usuário.
- [x] ST-04.05.04 — Testar autoria, bloqueios de horários/estado, repetição e preservação de auditoria.
- [x] ST-04.05.05 — Atualizar documentação e memória com evidências e limites.

Evidência: [DEC-002](decisoes/DEC-002-EXCLUSAO-PELO-CRIADOR.md); 402 testes backend, build/lint e verificações frontend aprovados. A homologação visual/manual e a adaptação aos futuros estados seguem em GT-07 e GT-03/04.

**Critério de conclusão de GT-04:** comportamentos anteriores continuam corretos nas etapas correspondentes e nenhum caminho contorna as duas aprovações.

### T-04.06. Excluir canceladas selecionadas, consultar lixeira e purgar banco — Feito

- [x] ST-04.06.01 — Registrar a escolha de apagar jornada e histórico na exclusão definitiva, na DEC-003.
- [x] ST-04.06.02 — Criar marcadores de lixeira e migração preservando a base existente; aplicar no banco local.
- [x] ST-04.06.03 — Implementar envio/restauração/purga em lote com autoria, status, limite e transação.
- [x] ST-04.06.04 — Retirar lixeira da consulta normal, detalhes e relatórios/totais.
- [x] ST-04.06.05 — Criar seleção múltipla separada de Entrada, ação Excluir selecionadas e tela /lixeira.
- [x] ST-04.06.06 — Validar purga física e rollback no MySQL com fixtures temporárias, removidas ao final.
- [x] ST-04.06.07 — Atualizar guias e memória; registrar que homologação manual/Android ainda pertence a GT-07.

Evidência: [DEC-003](decisoes/DEC-003-LIXEIRA-E-EXCLUSAO-DEFINITIVA.md) e [guia de lixeira](../back/docs/jornadas-lixeira.md). GT-04 continua pendente das duas aprovações; esta entrega não encerra a grande tarefa.

## GT-05. Completar cadastros do RH

**Estado:** A fazer, com APIs existentes. **Prioridade:** P2. **Requisitos:** RF03 e RF04.

### T-05.01. Entregar manutenção de prestadores — A fazer

- [x] ST-05.01.01 — Disponibilizar API de consulta, criação, edição, inativação e reativação.
- [ ] ST-05.01.02 — **A fazer:** criar listagem com busca e filtro de ativos/inativos.
- [ ] ST-05.01.03 — **A fazer:** criar formulário de cadastro e edição com validações.
- [ ] ST-05.01.04 — **A fazer:** criar detalhes e ações de inativar/reativar pelo RH.
- [ ] ST-05.01.05 — **A fazer:** validar permissões e preservação do histórico pelo aplicativo.

### T-05.02. Entregar manutenção de funções e valores/hora — A fazer

- [x] ST-05.02.01 — Disponibilizar API de manutenção de funções e preço padrão.
- [ ] ST-05.02.02 — **A fazer:** criar telas de listagem, cadastro e edição.
- [ ] ST-05.02.03 — **A fazer:** oferecer alteração de situação ativa/inativa.
- [ ] ST-05.02.04 — **A fazer:** demonstrar que alterar preço padrão não altera jornadas históricas.

### T-05.03. Entregar manutenção de setores — A fazer

- [x] ST-05.03.01 — Disponibilizar API de manutenção de setores.
- [ ] ST-05.03.02 — **A fazer:** criar listagem e formulário de cadastro/edição.
- [ ] ST-05.03.03 — **A fazer:** oferecer inativação/reativação pelo RH e validar vínculos históricos.

**Critério de conclusão:** RH mantém os três cadastros pelo aplicativo, respeitando permissões e histórico, sem depender de chamadas manuais à API.

## GT-06. Completar relatórios e indicadores

**Estado:** A fazer, com entrega parcial existente. **Prioridade:** P2. **Dependência para estados finais:** contratos de GT-03.

### T-06.01. Entregar relatório resumido por período — A fazer

- [x] ST-06.01.01 — Disponibilizar API de relatório com filtros e paginação no modelo anterior.
- [ ] ST-06.01.02 — **A fazer:** criar tela com período, prestador e status.
- [ ] ST-06.01.03 — **A fazer:** apresentar trabalhador, data, horas, valor e situação.
- [ ] ST-06.01.04 — **A fazer:** permitir percorrer os resultados paginados e tratar vazio/erro.

### T-06.02. Consolidar totais e pendências — A fazer

- [x] ST-06.02.01 — Disponibilizar API de totais e painéis parciais por perfil no modelo anterior.
- [ ] ST-06.02.02 — **A fazer:** diferenciar pendências de realização e de pagamento.
- [ ] ST-06.02.03 — **A fazer:** apresentar visão consolidada, incluindo pagos e demais estados.
- [ ] ST-06.02.04 — **A fazer:** conferir valores exibidos com uma base de teste de resultados conhecidos.

**Critério de conclusão:** RF15/RF16 utilizáveis no aplicativo e coerentes com o novo ciclo e com os filtros. Exportação PDF/CSV não é exigência atual do MVP.

## GT-07. Homologar qualidade e aplicativo Android

**Estado:** A fazer, com verificações anteriores registradas. **Prioridade:** P3; testes do novo fluxo acompanham sua implementação, sem esperar todas as telas ficarem prontas.

### T-07.01. Registrar e manter verificações automatizadas — A fazer

- [x] ST-07.01.01 — Registrar aprovação dos 390 testes do backend e build/lint na avaliação anterior.
- [x] ST-07.01.02 — Registrar aprovação de tipos, lint e dois scripts do frontend na avaliação anterior.
- [x] ST-07.01.03 — Identificar que o E2E atual cobre apenas GET /.
- [ ] ST-07.01.04 — **A fazer:** adaptar testes relevantes às duas decisões e às novas transições.
- [ ] ST-07.01.05 — **A fazer:** comprovar bloqueio de eventos e pagamento por chamadas diretas indevidas.

### T-07.02. Validar o ciclo integrado com os três perfis — A fazer

- [ ] ST-07.02.01 — **A fazer:** preparar dados de teste e resultados esperados.
- [ ] ST-07.02.02 — **A fazer:** percorrer criação, aprovação inicial, execução e conferência.
- [ ] ST-07.02.03 — **A fazer:** percorrer rejeição, correção, nova conferência, segunda aprovação e pagamento.
- [ ] ST-07.02.04 — **A fazer:** validar intervalo opcional, passagem da meia-noite e histórico.
- [ ] ST-07.02.05 — **A fazer:** validar bloqueios por perfil e comportamento dos registros legados.

### T-07.03. Testar concorrência e falhas de comunicação — A fazer

- [ ] ST-07.03.01 — **A fazer:** testar criações conflitantes por conexões simultâneas.
- [ ] ST-07.03.02 — **A fazer:** testar eventos e decisões repetidos/concorrentes.
- [ ] ST-07.03.03 — **A fazer:** simular resposta perdida após commit e verificar recuperação por consulta.
- [ ] ST-07.03.04 — **A fazer:** demonstrar atomicidade entre alteração da jornada e auditoria.

### T-07.04. Homologar Android e usabilidade — A fazer

- [ ] ST-07.04.01 — **A fazer:** gerar e instalar aplicativo em Android 9 e versão recente.
- [ ] ST-07.04.02 — **A fazer:** validar rede e URL da API no aparelho físico.
- [ ] ST-07.04.03 — **A fazer:** verificar teclado, rolagem, legibilidade e mensagens de validação.
- [ ] ST-07.04.04 — **A fazer:** executar o ciclo completo em dispositivo e registrar evidências.

**Critério de conclusão:** resultados reproduzíveis demonstram os critérios funcionais do novo ciclo e o uso mobile; limitações remanescentes ficam explícitas.

## GT-08. Preparar implantação e operação

**Estado:** A fazer. **Prioridade:** P3. **Observação:** ausência de evidência nesta memória não prova ausência de configuração externa.

### T-08.01. Preparar ambiente com HTTPS — A fazer

- [ ] ST-08.01.01 — **A fazer:** identificar/definir ambiente de implantação e URL da API.
- [ ] ST-08.01.02 — **A fazer:** configurar HTTPS e origens CORS do cliente.
- [ ] ST-08.01.03 — **A fazer:** demonstrar comunicação do app com a API implantada.

### T-08.02. Consolidar política de fuso — A fazer

- [ ] ST-08.02.01 — **A fazer:** definir política organizacional de armazenamento e apresentação.
- [ ] ST-08.02.02 — **A fazer:** alinhar servidor, conexão MySQL e frontend.
- [ ] ST-08.02.03 — **A fazer:** validar datas/horários em eventos, correção, auditoria e relatórios.

### T-08.03. Automatizar backup e comprovar restauração — A fazer

- [ ] ST-08.03.01 — **A fazer:** configurar rotina diária de backup.
- [ ] ST-08.03.02 — **A fazer:** manter pelo menos sete cópias recentes.
- [ ] ST-08.03.03 — **A fazer:** restaurar cópia em banco separado e verificar integridade.
- [ ] ST-08.03.04 — **A fazer:** documentar execução, retenção e recuperação sem expor credenciais.

### T-08.04. Medir desempenho — A fazer

- [ ] ST-08.04.01 — **A fazer:** definir rede e carga representativas do MVP.
- [ ] ST-08.04.02 — **A fazer:** medir consultas e registros e calcular percentual até dez segundos.
- [ ] ST-08.04.03 — **A fazer:** verificar a meta de 95% e corrigir causas identificadas se necessário.

**Critério de conclusão:** evidências dos RNF02, RNF07, RNF09 e RNF11, conforme o escopo e as condições de teste registradas.

## GT-09. Atualizar entrega acadêmica e técnica

**Estado:** A fazer, com referências existentes. **Prioridade:** P4; decisões documentais podem acompanhar GT-03.

### T-09.01. Reconciliar documentos de produto — A fazer

- [x] ST-09.01.01 — Identificar requisitos, regras, modelo de dados e protótipos no artigo original.
- [ ] ST-09.01.02 — **A fazer:** incorporar a dupla aprovação aos requisitos e regras.
- [ ] ST-09.01.03 — **A fazer:** atualizar máquina de estados, dicionário e diagrama conforme a implementação escolhida.
- [ ] ST-09.01.04 — **A fazer:** harmonizar documento único, preço por função e cancelamento.
- [ ] ST-09.01.05 — **A fazer:** revisar protótipos e capturas das telas efetivamente entregues.

### T-09.02. Documentar instalação e manutenção — A fazer

- [x] ST-09.02.01 — Manter guias técnicos existentes no backend e DESENVOLVIMENTO.md no frontend.
- [ ] ST-09.02.02 — **A fazer:** substituir os READMEs genéricos por instruções do PontoXtra.
- [ ] ST-09.02.03 — **A fazer:** documentar configuração, contas de teste, migração e execução reproduzível.
- [ ] ST-09.02.04 — **A fazer:** alinhar os guias ao fluxo implementado após GT-03.

### T-09.03. Preparar relatório final e demonstração — A fazer

- [x] ST-09.03.01 — Produzir avaliação histórica do estado atual e ressalva sobre a nova regra.
- [ ] ST-09.03.02 — **A fazer:** atualizar matriz de requisitos com evidências da implementação final.
- [ ] ST-09.03.03 — **A fazer:** reunir resultados de testes, desempenho, Android e backup.
- [ ] ST-09.03.04 — **A fazer:** preparar roteiro de demonstração com os três perfis e as duas decisões.
- [ ] ST-09.03.05 — **A fazer:** conferir coerência entre artigo final, aplicativo, API e banco.

**Critério de conclusão:** entrega acadêmica descreve o sistema realmente entregue, comprova os resultados e explicita o que permaneceu fora da implementação.

## 4. Ficha de acompanhamento de uma tarefa

Modelo proposto para tarefas ativas ou com bloqueios; evita repetir uma ficha extensa em cada subtarefa simples.

| Campo | Exemplo real deste quadro |
| --- | --- |
| ID e título | T-03.04 — Implementar as duas decisões no backend |
| Grande tarefa | GT-03 — Duas aprovações do ADM |
| Estado | A fazer |
| Prioridade | P1 |
| Responsável | Não definido |
| Prazo | Não definido |
| Última atualização | 22/10/2026 |
| Objetivo | Impedir realização sem aprovação prévia e pagamento sem segunda aprovação |
| Dependências | Regras e contratos definidos; migração compatível preparada |
| Pontos em aberto | Políticas de legado, reenvio, mudanças de planejamento e cancelamento |
| Próxima ação | Após definição dos contratos, adaptar criação e validação de transições |
| Critério de aceite | API bloqueia atalhos e preserva separadamente as duas decisões e sua auditoria |
| Evidência de conclusão | Ainda não há; registrar arquivos, migração e resultados de testes ao concluir |

## 5. Regras propostas para manter o quadro útil

- Ao começar uma tarefa, indicar o trabalho ativo e a próxima ação concreta.
- Ao concluir subtarefa, registrar evidência no nível da tarefa: arquivos, teste, documento ou validação do usuário.
- Não concluir tarefa de implementação com base em decisão documentada ou código de um fluxo superado.
- Ao parar trabalho incompleto, registrar onde parou, o que falta e eventual bloqueio, sem afirmar que continua sendo executado em segundo plano.
- Atualizar estado dos pais após mudar os filhos. Manter IDs para que decisões e histórico continuem rastreáveis.
- Não repetir a mesma implementação em duas tarefas: GT-03 entrega as novas aprovações; GT-04 adapta e verifica o comportamento existente em torno delas.
- Após aceitar este formato, usar o quadro oficial como lista de trabalho; `03_PROXIMOS_PASSOS.md` deve apenas apontar para ele e resumir a ordem, evitando duas listas independentes.
- Usar `02_ESTADO_ATUAL.md` como visão técnica comprovada e `05_HISTORICO.md` como registro das mudanças. O quadro acompanha execução; as decisões explicam as regras.

## 6. Revisão pelo responsável

Esta proposta pode ser ajustada em estrutura, quantidade de detalhes, nomes dos estados e divisão das entregas. A estrutura ainda não foi consolidada como quadro oficial. A avaliação solicitada é sobre a organização; não autoriza automaticamente implementar as tarefas listadas.
