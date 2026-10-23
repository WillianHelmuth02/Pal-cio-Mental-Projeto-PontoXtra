# DEC-002: exclusão lógica da jornada pelo criador

Data: 22/10/2026. Situação: **aceita**. Implementação: **concluída no código, com verificações automatizadas**; teste visual/manual com login real ainda não executado nesta entrega.

## Origem e decisão

O responsável solicitou que quem criou uma jornada possa excluí-la para completar o CRUD. Em resposta à pergunta sobre o limite da exclusão, escolheu explicitamente: **somente antes da entrada, preservando o histórico**.

Implementar como exclusão lógica reutilizando o cancelamento existente. Não apagar fisicamente a jornada nem sua auditoria.

## Regras implementadas

- Qualquer usuário autenticado e ativo nos perfis existentes pode excluir uma jornada de sua autoria, desde que não tenha qualquer marcação.
- O RH mantém a permissão administrativa existente de cancelar jornadas de outros criadores nas mesmas condições de estado e horários.
- No ciclo atualmente implementado, a ação exige EM_ANDAMENTO sem entrada, início/fim de intervalo ou saída. A validação adicional dos demais horários impede excluir registros inconsistentes que tenham outras marcações sem entrada.
- Jornadas iniciadas, encerradas, em conferência/autorização, autorizadas para pagamento, rejeitadas, pagas ou canceladas não podem ser excluídas por esta operação.
- A exclusão exige justificativa e confirmação. Grava CANCELADO, autor, instante, motivo e estados anterior/novo em histórico transacional.
- Repetir a exclusão é recusado. Não há restauração. O prestador é liberado para uma nova jornada.
- A interface apresenta **Excluir jornada** nos detalhes. O status continua **Cancelado**; a jornada permanece consultável e pode aparecer nas consultas e relatórios históricos.
- Autoria é comparada por ID string exato, obtido da sessão. O cliente não pode informar ou substituir o autor da exclusão.
- Mesmo que o criador tenha mudado de perfil para ADM, sua autoria continua permitindo excluir a própria jornada sem marcações. Isso não concede ao ADM criação de novas jornadas ou exclusão de registros alheios.

## API e dados

Reutiliza `PATCH /jornadas/:id/cancelar` com `{ "justificativa": "..." }`. Não é necessário um DELETE físico ou um novo endpoint para oferecer exclusão lógica no CRUD.

Não há migração nova: `criada_por`, CANCELADO e histórico já existiam. O banco deve possuir o ENUM de cancelamento previamente documentado. Não houve aplicação de DDL nem alteração de dados de negócio nesta entrega.

## Relação com a dupla aprovação

A DEC-001 continua vigente e pendente de implementação. Ao implementar os estados de planejamento e aprovação inicial, a exclusão deve continuar bloqueada após qualquer marcação. Definir sua disponibilidade exata nos novos estados antes de migrá-los; esta entrega não introduz os estados novos nem aprovações fictícias.

## Critérios de aceite e verificação

- Criador ativo exclui jornada própria sem marcações; outro usuário sem a permissão de RH recebe 403.
- RH continua cancelando jornada sem marcações de outro criador.
- Entrada ou qualquer outra marcação bloqueia a ação; estados incompatíveis recebem 409.
- API revalida usuário, autoria e estado sob locks, antes da escrita; guarda auditoria na mesma transação.
- Interface calcula ações usando o ID real do usuário e relê a jornada antes de enviar. O servidor continua sendo a autoridade final.
- Repetição não grava novo histórico; tentativa de forjar autoria no corpo é recusada.

Resultado de 22/10/2026: 402 testes do backend aprovados (incluindo 103 na suíte de fluxo), build e lint aprovados. Frontend: tipos, lint, test-api.cjs e test-jornadas.cjs aprovados. Persistência/relógio são simulados nos testes HTTP; concorrência real entre conexões, rollback MySQL e execução manual da tela não foram demonstrados por esses testes.

## Fontes de implementação

- `back/src/jornadas/jornadas.controller.ts`: rota aceita os três perfis.
- `back/src/jornadas/jornadas.service.ts`: verifica usuário ativo e autoria dentro da transação, preservando a exceção administrativa do RH.
- `back/src/jornadas/jornadas.fluxo.ts`: mantém validação de status e ausência de marcações.
- `back/src/jornadas/jornadas.fluxo.spec.ts`: testes HTTP, autoria e auditoria.
- `front/src/utils/jornadas.ts`: contrato com criada_por e matriz de ações por usuário.
- `front/src/components/journey-details.tsx`: botão, confirmação e releitura.
- `front/scripts/test-jornadas.cjs`: matriz de autoria, IDs grandes, horários e estados.
