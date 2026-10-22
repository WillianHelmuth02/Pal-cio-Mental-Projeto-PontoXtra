# 02. Estado atual e diferença para a regra vigente

Última inspeção de código: 22/10/2026. Backend: d8da016. Frontend: 531e654.

## Requisito vigente versus implementação

**A dupla aprovação foi aceita como regra de produto, mas ainda não foi implementada.** O código inspecionado cria jornadas em EM_ANDAMENTO e permite eventos antes de qualquer decisão do ADM. A autorização atualmente existente ocorre apenas depois da saída e da conferência do RH, para liberar o registro do pagamento.

Portanto, o sistema atual não atende à aprovação prévia exigida pela [DEC-001](decisoes/DEC-001-DUPLA-APROVACAO.md). Não afirmar que há duas aprovações só porque a documentação já foi atualizada.

## Já implementado no código examinado

- Autenticação de usuários ativos; senhas com scrypt; tokens com expiração; logout com revogação e permissões no servidor.
- Início e ações por perfil; criação, filtros e detalhes de jornadas.
- Entrada, início/fim de intervalo e saída com horário do servidor; cálculo líquido e monetário.
- Conferência pelo RH, decisão posterior do ADM, correção com recálculo e registro de pagamento pelo RH.
- Histórico com autor, instante e snapshots; transações e locks nas operações de jornadas.
- APIs de manutenção de prestadores, funções e setores, com alterações reservadas ao RH.
- APIs de relatório por período e totais por status; painéis usam parte dos totais.
- Cancelamento auditável de jornada sem marcações; estado CANCELADO.

## Lacunas conhecidas

- Aprovação da realização antes da entrada e separação persistida das duas decisões do ADM.
- Telas de manutenção de prestadores, funções e setores.
- Tela de relatório por período e visão consolidada dos totais.
- Homologação em Android, validação integrada do ciclo completo e concorrência real entre conexões.
- Evidências de HTTPS implantado, desempenho e backup diário com sete cópias e restauração.
- Reconciliação do artigo, requisitos, diagrama e dicionário com as decisões posteriores.

## Verificações realizadas na avaliação de 22/10/2026

Backend: 390 testes aprovados, build e lint aprovados. Um teste E2E aprovado, limitado à rota GET /; não cobre o ciclo completo do negócio. Frontend: checagem de tipos, lint e scripts test-api.cjs e test-jornadas.cjs aprovados.

MySQL: conexão confirmada, seis tabelas e ENUM com sete estados, incluindo CANCELADO. Consultas reais de relatórios executaram sem erro; não houve reconciliação dos valores com fixtures esperadas. Acesso de avaliação foi somente leitura.

Esses resultados antecedem a implementação da dupla aprovação; não são evidência de teste do novo fluxo.

## Decisões e ambiguidades a preservar

- Documento do prestador: implementação exige unicidade global; RN04 do artigo fala em ativos, enquanto seu dicionário declara UNIQUE. Regra final precisa ser harmonizada.
- Valor/hora: criação copia o preço da função; não recebe preço livre. RH pode corrigir o histórico nos status permitidos.
- Fuso: interface usa Brasília UTC-03; backend depende do ambiente/conexão. Não foi localizada configuração organizacional de fuso.
- Sessões em memória: reinício do backend invalida tokens; recarga do frontend exige novo login.
- Banco físico enxuto: seis tabelas, diferente do diagrama ampliado. Precisa de justificativa formal.

## Regra de atualização desta sala

Só mudar a dupla aprovação para implementada após registrar arquivos alterados, migração, verificações e limites remanescentes. Manter o relatório anterior como avaliação histórica e explicitar sua ressalva posterior.
