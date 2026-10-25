# Memória do PontoXtra: o palácio mental do projeto

Esta pasta reúne o contexto duradouro do projeto para o desenvolvedor e para assistentes de IA. Foi criada em 22/10/2026, a pedido do responsável pelo projeto. É uma memória explícita em arquivos: precisa ser lida e mantida; não depende de uma IA lembrar conversas anteriores.

## Entrada e salas

Dupla aprovação implementada em 24/10/2026: consultar [DEC-004](decisoes/DEC-004-IMPLEMENTACAO-DUPLA-APROVACAO.md) para políticas, migração, evidências e limites; complementa a DEC-001.

Configuração Android e pendências de push: [07_NOTIFICACOES_CONFIGURACAO.md](07_NOTIFICACOES_CONFIGURACAO.md), atualizado em 23/10/2026.

| Sala | Conteúdo | Quando consultar |
| --- | --- | --- |
| [01_CONTEXTO.md](01_CONTEXTO.md) | Problema, objetivo, perfis, arquitetura e limites | No início de qualquer trabalho |
| [02_ESTADO_ATUAL.md](02_ESTADO_ATUAL.md) | O que existe, evidências e diferença entre código e requisito | Antes de avaliar progresso ou implementar |
| [decisoes/DEC-001-DUPLA-APROVACAO.md](decisoes/DEC-001-DUPLA-APROVACAO.md) | Duas aprovações obrigatórias do ADM | Qualquer trabalho com jornadas, permissões, pagamento ou status |
| [decisoes/DEC-002-EXCLUSAO-PELO-CRIADOR.md](decisoes/DEC-002-EXCLUSAO-PELO-CRIADOR.md) | Origem do cancelamento pelo criador antes de marcações; revisada pela DEC-003 | Autoria e histórico da evolução do cancelamento |
| [decisoes/DEC-003-LIXEIRA-E-EXCLUSAO-DEFINITIVA.md](decisoes/DEC-003-LIXEIRA-E-EXCLUSAO-DEFINITIVA.md) | Seleção, lixeira, restauração CANCELADO e remoção física de jornada/histórico | Regra atual de exclusão; sucede a Proposta 003 e revisa a DEC-002 |
| [03_PROXIMOS_PASSOS.md](03_PROXIMOS_PASSOS.md) | Pendências priorizadas e critérios de aceite | Ao planejar a próxima entrega |
| [04_MAPA_DE_FONTES.md](04_MAPA_DE_FONTES.md) | Localização de documentos e código | Para confirmar uma informação |
| [05_HISTORICO.md](05_HISTORICO.md) | Registro de alterações relevantes | Para entender a evolução |
| [06_QUADRO_DE_TAREFAS_PROPOSTA.md](06_QUADRO_DE_TAREFAS_PROPOSTA.md) | Proposta de grandes tarefas, tarefas e subtarefas com estados | Para avaliar o formato de acompanhamento; ainda não consolidado como quadro oficial |

## Como interpretar a memória

1. A instrução atual do usuário é a referência para o trabalho solicitado.
2. Decisões de produto aceitas registram o comportamento desejado, mesmo quando o código ainda não o implementa.
3. Código e verificações executadas mostram o comportamento efetivamente entregue.
4. O artigo da pré-banca é uma referência histórica de especificação; decisões posteriores podem revisá-lo.
5. Propostas técnicas e questões em aberto não se tornam decisões do usuário só por estarem escritas aqui.

Ao encontrar conflito, registre a diferença e trabalhe com essas categorias. Não apresente uma regra documentada como funcionalidade pronta.

## Protocolo de atualização

- Nova decisão: criar `decisoes/DEC-NNN-TITULO.md`, usando o modelo abaixo, e adicionar ao índice.
- Implementação: atualizar o estado atual somente depois de conferir código e resultados de verificação.
- Descoberta: registrar fonte, data e limites da evidência. Evitar listas de conclusões sem referência.
- Mudança de regra: manter o histórico; indicar qual decisão foi substituída e por qual.
- Conclusão de tarefa: registrar o resultado em `05_HISTORICO.md` e revisar os próximos passos.
- Nunca copiar credenciais, tokens ou dados pessoais para estes arquivos.

## Modelo de decisão

```markdown
# DEC-NNN: título
Data:
Situação: proposta / aceita / substituída
Origem: instrução do usuário ou fonte identificada
Implementação: pendente / parcial / concluída, com evidências

## Contexto e problema
## Decisão de produto
## Consequências e invariantes
## Proposta técnica, se houver
## Questões em aberto
## Critérios de aceite
## Fontes e arquivos afetados
```

## Portabilidade

`PontoXtra/AGENTS.md`, `front/AGENTS.md` e `back/AGENTS.md` apontam para esta memória. Agentes que reconhecem `AGENTS.md` recebem esse caminho no escopo correspondente. Para ferramentas que não leem esse arquivo automaticamente, peça explicitamente a leitura de `Memoria_Projeto/README.md` ao abrir o projeto.

A pasta fica ao lado dos dois repositórios, e não dentro deles. Ao clonar apenas `front` ou `back`, será necessário compartilhar também esta memória. Nenhum repositório novo foi inicializado para alterar a organização existente.
