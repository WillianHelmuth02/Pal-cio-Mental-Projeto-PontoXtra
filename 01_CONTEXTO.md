# 01. Contexto e identidade do projeto

Última atualização: 28/10/2026. Dupla aprovação, cadastros RH, usuários ADM e relatórios implementados; homologação manual/mobile ainda pendente. Visão detalhada em ../Documentos/VISAO_GERAL_ATUAL.md.

## Problema e objetivo

PontoXtra é um aplicativo para controlar jornadas e registrar repasses a prestadores de serviços sob demanda, com foco em hospitalidade e gastronomia. Centraliza registros, cálculos e decisões para substituir controles dispersos e preservar rastreabilidade.

## Responsabilidades

| Perfil | Responsabilidades de domínio |
| --- | --- |
| Operacional | Criar jornadas e registrar entrada, intervalo e saída nas condições autorizadas |
| RH | Manter prestadores, funções e setores; criar, consultar, conferir e corrigir jornadas; registrar pagamentos autorizados |
| Administrador / ADM | Autorizar ou rejeitar a realização da jornada antes da entrada; depois, decidir separadamente sobre o pagamento após o encerramento e a conferência |

O ADM possui gestão de contas na API e na tela /usuarios. Ele não herda automaticamente as ações de RH ou Operacional. Os três perfis consultam /relatorios; RH mantém /prestadores, /funcoes e /setores.

## Fluxo vigente de produto

Criação → aprovação do ADM para realização → execução da jornada → encerramento e cálculo → conferência do RH → aprovação do ADM para pagamento → registro do pagamento pelo RH.

A [DEC-001](decisoes/DEC-001-DUPLA-APROVACAO.md) é a fonte detalhada dessa regra. O fluxo anterior tinha somente a decisão posterior ao encerramento; ele já não descreve integralmente o produto desejado.

## Limites do MVP

Gestão de canceladas: criador ou RH pode cancelar antes de marcações, enviar canceladas selecionadas à lixeira e restaurá-las como CANCELADO. A exclusão definitiva, confirmada à parte, remove jornada e histórico vinculado do banco operacional, conforme [DEC-003](decisoes/DEC-003-LIXEIRA-E-EXCLUSAO-DEFINITIVA.md). Não aplicar essa purga a jornadas executadas ou pagas.

Pagamento significa registro administrativo de quitação. Não inclui transferência bancária. Não estão previstos folha celetista completa, encargos/eSocial, integrações contábeis legadas, biometria avançada, geolocalização obrigatória ou equipamentos físicos de ponto.

Não acrescentar esses recursos como exigência implícita da dupla aprovação.

## Organização técnica observada

- `front/`: repositório Git independente, Expo/React Native, TypeScript e Expo Router; alvo mobile com execução web de desenvolvimento.
- `back/`: repositório Git independente, NestJS/TypeScript, TypeORM, API REST/JSON.
- `BD/`: SQL MySQL; seis tabelas centrais de negócio (usuarios, prestadores, funcoes, setores, jornadas e historico_jornada), mais notificacoes, dispositivos_notificacao, entregas_push e duas tabelas de controle de migrações: onze tabelas confirmadas por inspeção de metadados em 28/10. Migração explícita, sem sincronização automática. Dicionário atual em BD/DICIONARIO_ATUAL.md.
- `Documentos/`: artigo, requisitos, termo, dicionário e protótipos; também contém o relatório de avaliação.
- `output/pdf/`: relatório de avaliação em PDF.
- `Memoria_Projeto/`: contexto, decisões e acompanhamento entre tarefas.

## Cuidados do ambiente

`BD/pontoxtra.sql` recria o banco, incluindo DROP DATABASE. Não usá-lo como migração de uma base existente. Configuração automática do TypeORM tem synchronize, migrationsRun e dropSchema desativados. Alterações de schema devem ter migração explícita que preserve os dados e plano de validação.
