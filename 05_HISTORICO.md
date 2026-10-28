# 05. Histórico de decisões e entregas

## 28/10/2026 — Correção de conectividade do APK na rede local

- IP identificado, MySQL confirmado por SELECT 1 e API iniciada em 0.0.0.0:3000 com push desabilitado; usuário confirmou Hello World! no navegador do tablet e smartphone.
- URL pública explícita nos perfis EAS development/preview e .env.local; plugin HTTP de homologação, validação de URL/build e mensagem de rede com endereço. HOST explícito no backend; guias/exemplos atualizados.
- Testes de configuração/API, build/lint backend, exportação Android, manifesto preview/production e URL no bundle aprovados. Tipos/lint frontend mantêm erros preexistentes. Sem alteração de dados ou migração.
- Build remoto não executado: revisão automática rejeitou envio do código/configuração à Expo/EAS sem autorização explícita. Novo APK, login mobile, jornada e push pendentes. Ver 08_ANDROID_REDE_LOCAL.md.


## 28/10/2026 — Relatórios e consolidação integral da documentação atual

- Criados front/src/app/relatorios.tsx, components/relatorios-screen.tsx, services/relatorios.ts, utils/relatorios.ts e scripts/test-relatorios.cjs. Período inclusivo, prestador/status, paginação de 50 itens, totais globais/por dez estados e acesso ao detalhe. Totais usam filtros idênticos sem paginação; valores/contagens preservados como strings.
- Adicionados acessos no journey-home, journey-ui e jornadas-screen, incluindo Operacional. use-api-resource reinicia loading/fresh/error quando muda o loader; chave da consulta impede mostrar dados de outro filtro/página.
- Reutilizadas APIs existentes; sem migração ou escrita em registros reais. Criado back/scripts/inspect-schema.cjs; inspeção somente leitura confirmou onze tabelas, campos, estados e FKs, documentados em BD/DICIONARIO_ATUAL.md.
- 533 testes backend, build/lint backend e um E2E básico aprovados; seis scripts frontend aprovados; exportação web aprovada. Tipos frontend falham nos quatro arquivos antigos registrados no estado; lint frontend bloqueado pela incompatibilidade ESLint/plugin React. Homologação manual/Android, push e concorrência real não executados.
- Revisados READMEs, guias dos módulos e desenvolvimento, memória/índice/mapa/quadro/notificações. Criadas visão detalhada, especificação atual, roteiro integrado, inventário de API, guia de banco e relatório. Estado/próximos passos consolidados, com versões anteriores preservadas. Decisões originais/PDFs históricos preservados; revisão vigente em Markdown, sem nova edição diagramada dos PDFs.
- Contagem documentada: cinco módulos CRUD com D lógico nos quatro cadastros; jornadas têm correção/purga restritas. Nenhum módulo principal de negócio da API aguarda tela principal após esta entrega; endpoints auxiliares e infraestrutura interna são diferenciados de recursos ausentes.

## 28/10/2026 — Gestão de usuários pelo ADM

- Criadas front/src/app/usuarios.tsx, components/usuarios-screen.tsx, utils/usuarios.ts, scripts/test-usuarios.cjs e docs/usuarios-adm.md. Adicionado acesso no journey-home.tsx e suporte opcional a senha mascarada no Field de journey-ui.tsx.
- Consulta/busca/filtros, criação, edição somente de campos alterados, senha confirmada, desativação/reativação com confirmação e proteção da própria conta. Reutilizadas regras da API de revogação; edição própria encaminha a novo login. Sem migração ou escrita em contas reais.
- 44 testes backend de autenticação/contas, scripts test-usuarios/test-cadastros/test-api e compilação web aprovados. Tipos/lint globais com problemas anteriores; homologação manual/Android pendente. Memória atualizada; próximo bloco são relatórios.

## 28/10/2026 — Tela de prestadores RH

- Adicionada front/src/app/prestadores.tsx e acesso no journey-home.tsx; estendidos cadastros-screen.tsx e utils/cadastros.ts para dados e validações do prestador. Ampliado scripts/test-cadastros.cjs e roteiro docs/cadastros-rh.md.
- Nome/documento obrigatórios e contatos opcionais; limpeza com null, preservação de zeros/pontuação, busca, filtros e confirmação de desativação/reativação. APIs existentes; sem migração ou escrita no banco real.
- 121 testes HTTP dos três cadastros, scripts test-cadastros/test-api e compilação web aprovados. Tipos/lint globais continuam com problemas existentes. Homologação manual e Android não executada.

## 28/10/2026 — Telas de funções e setores do RH

- Criadas rotas front/src/app/funcoes.tsx e setores.tsx, componente compartilhado cadastros-screen.tsx, validação utils/cadastros.ts e script test-cadastros.cjs. Adicionados acessos RH no journey-home.tsx.
- Consulta, busca, filtros, criação, edição, desativação e reativação com confirmação e proteção contra envio repetido. APIs existentes mantidas; sem migração ou gravação em dados reais. Alteração preexistente em eas.json preservada.
- 63 testes backend dos cadastros aprovados; scripts frontend test-cadastros/test-api e exportação web aprovados. Typecheck falha em arquivos existentes (app-tabs, jornadas-screen, use-theme); lint bloqueado por incompatibilidade ESLint/plugin React. Sem erros de tipos nas novas telas após regenerar rotas.
- Atualizados estado/próximos passos e criado front/docs/cadastros-rh.md com roteiro. Homologação manual RH e Android não executada.

## 24/10/2026 - Duas aprovações implementadas

- Responsável autorizou executar a DEC-001. Criação agora pendente de realização; novas rotas ADM autorizam/rejeitam antes da entrada; decisões de pagamento continuam após saída e conferência RH. Metadados iniciais separados e preservados em correções.
- Atualizados ações, mensagens, painéis, filtros e detalhe com blocos de realização/pagamento, motivos e identificação de legado. Cancelamento/recriação adotado para rejeição ou mudança de planejamento; uma reserva pendente/liberada/em execução por prestador.
- Conectados avisos internos/fila push da criação pendente e decisão inicial. Configurações Expo/Firebase e alterações anteriores do frontend preservadas.
- Migração local encontrou ENUM/colunas novos da tentativa anterior; preparou mapeamento idempotente e controle sem decisão retroativa. Contagem preservada em 3/3; nenhuma jornada ou histórico removidos. Fixtures de testes MySQL revertidas.
- 533 testes backend aprovados; build/lint sem avisos de código e E2E básico aprovados. Tipos/lint frontend, scripts API/jornadas/push aprovados. MySQL real validou duas aprovações, bloqueios, rejeições, correção preservando a primeira decisão, avisos, quitação, lixeira e notificações.
- Criados guia jornadas-aprovacoes.md, migração, testes e DEC-004; atualizados memória e guias relacionados. Homologação visual/mobile e concorrência real permanecem pendentes; não iniciado build EAS nem envio push externo.
- Bundles Android, iOS e web exportados com sucesso; são artefatos de compilação JavaScript, não APK/IPA nem comprovação de recebimento push. Inspeção final confirmou compatibilidade do schema local e reexecução do mapeamento já havia preservado 3/3 jornadas.


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

## Atualização — envio autorizado e build iniciada

Em 28/10/2026, o usuário autorizou explicitamente enviar o código à Expo/EAS. O envio concluiu com sucesso; EAS carregou EXPO_PUBLIC_API_URL e PONTOXTRA_ALLOW_HTTP do perfil preview e reutilizou a Keystore remota existente. Build Android preview solicitada: 962ee26b-789e-40d7-9c0b-2d92cad39d87. Link: https://expo.dev/accounts/willianhelmuhts-team/projects/pontoxtra/builds/962ee26b-789e-40d7-9c0b-2d92cad39d87 . Estado na última saída: aguardando conclusão. Isso supera a pendência de autorização do envio; conclusão/instalação e testes do novo APK ainda não confirmados.

## 28/10/2026 — Push nativo ativado e recebimento confirmado

Usuário relatou avisos internos funcionando, sem notificação Android. Diagnóstico somente leitura: PUSH_NOTIFICATIONS_ENABLED estava false no .env e o processo anterior também havia sido iniciado com false para teste de conectividade; um dispositivo ativo e uma entrega PENDENTE. O código existente já configurava canal aprovacoes com importância HIGH, som default, apresentação foreground e payload de push com som default.

A pedido do usuário, habilitado PUSH_NOTIFICATIONS_ENABLED=true no .env backend, preservando demais configurações, e reiniciada somente a API previamente iniciada nesta tarefa. Novo PID: 146132. Sessões em memória são perdidas no reinício. GET / pelo IP Wi-Fi retornou HTTP 200. Entrega passou de PENDENTE para AGUARDANDO_RECIBO, sem erro registrado, indicando aceitação pela Expo (não leitura garantida). Teste existente front/scripts/test-push.cjs aprovado com SDK simulado.

**Usuário confirmou: a notificação apareceu no Android com som ou vibração.** Isso comprova recebimento nativo nesse aparelho/evento. Não houve alteração do código nem novo APK para esta correção; a configuração faltante estava no backend. A condição de som/vibração continua sujeita à permissão/canal e às preferências Android. Não foram alterados tokens, credenciais Firebase ou preferências do aparelho.

Continuam pendentes os cenários completos de push: demais aparelhos/perfis, foreground/background/encerrado, toque, logout e troca de conta. Em outros aparelhos, abrir Notificações > Ativar avisos neste celular e permitir notificações. Autor da ação não recebe seu próprio aviso, conforme regra existente. O backend deve permanecer ativo e com acesso à internet. A presente atualização supera os registros anteriores de worker desabilitado; não implica homologação global de todas as jornadas/notificações.
