# 04. Mapa de fontes

Última revisão: 22/10/2026. Caminhos relativos à raiz PontoXtra.

| Informação | Fonte |
| --- | --- |
| Regra atual de duas aprovações | Instrução do usuário em 22/10/2026, registrada em `decisoes/DEC-001-DUPLA-APROVACAO.md` nesta pasta |
| Especificação histórica da pré-banca | `Documentos/Artigo_PontoXtra_Pre_Banca_Final.pdf`, especialmente páginas 6 a 12 |
| Documentos complementares | `Documentos/Requisitos e Regras Pronto.pdf`, `Dicionario_de_Dados_PontoXtra.pdf`, `Termo de Abertura Pronto.pdf` e `_3-Prototipação.pdf` |
| Avaliação técnica antes da nova decisão | `Documentos/Relatorio_Estado_Atual_PontoXtra_2026-10-22.md` e versão em `output/pdf/`, com ressalva posterior |
| Estado e persistência de jornadas | `back/src/jornadas/jornada.entity.ts`, `jornadas.service.ts` e `BD/pontoxtra.sql` |
| Rotas e perfis | `back/src/jornadas/jornadas.controller.ts`, `back/src/auth/acesso.guard.ts` |
| Eventos e cálculo | `back/src/jornadas/jornadas.eventos.ts`, `jornadas.calculo.ts` |
| Conferência, decisão e pagamento existentes | `back/src/jornadas/jornadas.fluxo.ts`, `jornadas.fluxo.validation.ts`, `back/docs/jornadas-fluxo.md` |
| Cancelamento existente | `back/docs/jornadas-cancelamento.md`, `back/src/migrate-cancelamento.ts` |
| Telas de jornadas | `front/src/components/journey-home.tsx`, `jornadas-screen.tsx`, `journey-create.tsx`, `journey-details.tsx`, `journey-correction.tsx` |
| Contratos e ações da interface | `front/src/utils/jornadas.ts`, `front/src/services/jornadas.ts` |
| Relatórios | `back/src/relatorios/`, `back/docs/relatorios.md` |
| Configuração e autenticação | `back/src/app.module.ts`, `back/src/auth/`, `front/src/services/api.ts`, `front/src/contexts/auth.tsx` |
| Desenvolvimento e roteiro manual | `front/DESENVOLVIMENTO.md`, `back/docs/` |
| Testes | `back/src/**/*.spec.ts`, `back/test/app.e2e-spec.ts`, `front/scripts/test-api.cjs`, `front/scripts/test-jornadas.cjs` |

Os PDFs originais não foram reescritos nesta tarefa. Sua permanência não indica que a decisão anterior de uma única aprovação continua vigente.

Notificações (23/10/2026): `back/src/notificacoes/`, `back/src/migrate-notificacoes.ts`, `back/src/check-notificacoes.ts`, `back/docs/notificacoes.md`; frontend em `src/contexts/notificacoes.tsx`, `src/components/notificacoes-screen.tsx`, `src/services/push.native.ts` e `scripts/test-push.cjs`. Configuração e limites em [07_NOTIFICACOES_CONFIGURACAO.md](07_NOTIFICACOES_CONFIGURACAO.md).
