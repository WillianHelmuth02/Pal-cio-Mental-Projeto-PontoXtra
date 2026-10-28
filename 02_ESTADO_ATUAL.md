# 02. Estado atual — 28/10/2026

Esta é a visão vigente. As avaliações e complementos anteriores foram preservados em [arquivo histórico](02_ESTADO_ATUAL_HISTORICO_ATE_28_10_2026.md); não interpretar lacunas históricas como situação atual.

## Implementado no código

- Login/logout, usuários ativos, sessão com expiração/revogação, senha scrypt e autorização no servidor.
- Quatro cadastros com API e frontend: usuários ADM; prestadores, funções/valor-hora e setores RH. Consulta, busca, filtros, criação, edição, desativação e reativação.
- Jornadas com criação pendente, duas aprovações independentes, entrada/intervalo/saída, cálculo, conferência, correção, registro de quitação e histórico.
- Cancelamento antes de qualquer marcação, seleção de canceladas/lixeira, restauração como CANCELADO e purga condicionada, conforme DEC-003/004.
- Avisos internos, contador/leitura e suporte push/fila; recebimento no aparelho ainda não homologado.
- /relatorios para os três perfis: período inclusivo, prestador/status, paginação de 50 itens, totais de todo o conjunto e por dez estados. Nulos e valores grandes preservados, sem soma local dos cartões.
- Acessos no painel e na lista de jornadas; relatório mostra filtros efetivamente aplicados.

São **cinco módulos CRUD** contando desativação como remoção lógica. Jornadas têm atualização/exclusão limitada por estado; só canceladas sem marcações podem ser purgadas. Login, histórico, relatórios e notificações não são CRUDs extras.

## Back/API e banco sem frontend

Nenhum módulo principal do MVP da API continua sem tela principal após esta entrega. GET individuais de cadastros e /auth/me são auxiliares sem página dedicada; telas cadastrais editam a partir da lista. Não há console administrativo de entregas/dispositivos/migrações, nem API de administração completa dessas tabelas esperando apenas tela.

Inspeção somente leitura atual do information_schema confirmou **11 tabelas**, dez estados de jornada, campos das duas decisões, lixeira, legado e FKs. Seis tabelas centrais, três de notificações e duas de controle. O SQL inicial tem dez tabelas; controle_migracoes_aprovacao é criado pelo script de aprovação. [Dicionário](../BD/DICIONARIO_ATUAL.md).

## Evidência executada nesta revisão

- 533 testes backend aprovados; build e lint backend aprovados.
- Um E2E básico aprovado, limitado a GET /.
- Seis scripts frontend aprovados: test-api, test-jornadas, test-push, test-cadastros, test-usuarios e test-relatorios.
- Exportação web aprovada, incluindo /relatorios e os quatro cadastros.
- tsc executado após geração de rotas: falha nos arquivos existentes app-tabs.tsx, app-tabs.web.tsx, jornadas-screen.tsx e use-theme.ts. Nenhum erro nos novos arquivos de relatório.
- Lint frontend executado: bloqueado pela incompatibilidade ESLint 10/plugin React (contextOrFilename.getFilename).
- MySQL atual: somente metadados, sem gravação de negócio/migração/purga. Inspeção não reconcilia totais nem testa concorrência.

Testes MySQL de 22–24/10 permanecem como evidência histórica nas decisões; não foram reexecutados nesta revisão. Build não comprova homologação visual ou recebimento push. Nenhum build remoto/publicação/env real foi alterado.

## Pendências reais

Homologação manual com os três perfis; cadastros e relatório reconciliados com massa conhecida; Android; push real; concorrência entre conexões/perda de resposta após commit; política de fuso consistente; HTTPS; backup diário/sete cópias e restauração; desempenho; recuperação de migração em cópia.

Limitações/evoluções: sessões em memória, lista principal de jornadas sem paginação, ausência de recuperação autônoma de senha/exportação CSV-PDF/filtro por data de pagamento/editor de planejamento/console push. Não são novos requisitos aceitos automaticamente.

## Documentação atual

[Visão detalhada](../Documentos/VISAO_GERAL_ATUAL.md), [especificação revisada](../Documentos/ESPECIFICACAO_ATUAL.md), [API e cobertura](../back/docs/api-cobertura.md), [roteiro](../Documentos/ROTEIRO_HOMOLOGACAO.md) e READMEs atualizados. PDFs de pré-banca e decisões originais preservados; revisão funcional/técnica atual em Markdown, sem nova edição diagramada dos PDFs.

## Complemento — conectividade Android (28/10/2026)

[Registro detalhado](08_ANDROID_REDE_LOCAL.md). Usuário confirmou APK anterior gerado/instalado, mas sem API. MySQL SELECT 1 e GET / via IP Wi-Fi aprovados; usuário confirmou acesso no navegador dos dois Androids. Configurados preview/development para 192.168.0.119:3000, HTTP explícito de homologação e bloqueios de configuração inválida. Bundle Android e manifesto validados; build/lint backend e testes de configuração/API aprovados. Tipos/lint frontend continuam com os bloqueios já registrados. API iniciada com push desabilitado; sem migração/dados de negócio. Novo build remoto rejeitado pela revisão automática por exigir autorização explícita do envio de código/configuração à Expo/EAS; novo APK, login mobile e jornada ainda pendentes.

## Complemento — push real (28/10/2026)

Worker habilitado no ambiente local e API reiniciada; envio aceito pela Expo, e usuário confirmou notificação nativa Android com som ou vibração em um aparelho/evento. Demais cenários permanecem pendentes. Ver 08_ANDROID_REDE_LOCAL.md. Sem mudança de código ou novo APK.

