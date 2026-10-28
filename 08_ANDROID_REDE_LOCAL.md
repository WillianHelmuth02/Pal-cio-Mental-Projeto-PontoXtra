# 08. Android e API na rede local — 28/10/2026

## Origem e situação

Usuário confirmou APK anterior gerado e instalado, com falha de acesso à API. Solicitou executar a preparação omitida nas etapas 1–4 e ajustar o código/configuração necessários.

## Diagnóstico confirmado

- Frontend SDK 58 (`package.json`), não SDK 57 citado no resumo histórico.
- Não havia `.env.local` frontend. `api.ts` usava fallback `http://localhost:3000`; `eas.json` não declarava URL. Isso permite gerar APK apontando para o próprio aparelho. O APK anterior não foi descompilado para confirmar seu valor exato.
- IP Wi-Fi do PC: `192.168.0.119` (gateway 192.168.0.1).
- MySQL escutando em 3306; `node dist/check-database.js` executou SELECT 1 com sucesso, sem escrita.
- API não estava escutando em 3000. Foi compilada e iniciada em segundo plano (`dist/main.js`, PID 143004), com `HOST=0.0.0.0`, `PORT=3000` e `PUSH_NOTIFICATIONS_ENABLED=false` apenas nesse processo. Não houve alteração do `.env` backend.
- GET `/` retornou HTTP 200 e `Hello World!` tanto em loopback quanto no IP Wi-Fi, a partir do PC.
- **Usuário confirmou `Hello World!` no navegador do tablet E do smartphone, ambos no mesmo Wi-Fi.** Etapa 3 tem evidência por relato explícito do usuário.
- Wi-Fi classificado como Public no Windows, com regras Node existentes. Não foi alterada classificação da rede nem qualquer regra de firewall; teste nos dispositivos funcionou.

## Alterações aplicadas

- `front/eas.json`: env explícito nos perfis development/preview com `EXPO_PUBLIC_API_URL=http://192.168.0.119:3000` e `PONTOXTRA_ALLOW_HTTP=true`.
- `front/.env.local` (ignorado pelo Git): mesmos valores públicos para desenvolvimento.
- `front/app.config.js`: valida URL e bloqueia build EAS sem URL, com loopback ou HTTP não habilitado; production exige HTTPS.
- `front/plugins/with-api-network.js`: plugin de manifesto define `android:usesCleartextTraffic` conforme configuração. Sem editar pastas Android geradas; sem nova dependência. Permissão HTTP abrange o app no preview de homologação, somente quando habilitada.
- `front/src/services/api.ts`: erro de rede mostra endereço tentado; Bearer/401/timeout preservados.
- `front/scripts/test-build-config.cjs`: regressão de URL ausente/loopback/inválida, HTTP explícito e produção HTTPS.
- `back/src/main.ts`: interface HOST explícita, padrão 0.0.0.0; PORT padrão 3000.
- Exemplos de ambiente, README frontend e `front/ANDROID_REDE_LOCAL.md` atualizados.

## Verificações executadas

- Teste de configuração de build e test-api aprovados.
- Build e lint backend aprovados.
- Exportação Android com 1731 módulos aprovada em `.expo/network-check` (saída local ignorada pelo Git).
- Introspecção real Expo: manifesto preview com `usesCleartextTraffic=true`; production HTTPS com `false`.
- Bundle Android Hermes contém `http://192.168.0.119:3000`.
- Tipos frontend executados: continuam falhando nos mesmos arquivos preexistentes `app-tabs.tsx`, `app-tabs.web.tsx`, `jornadas-screen.tsx`, `use-theme.ts`.
- Lint frontend executado: continua bloqueado pela incompatibilidade ESLint 10/plugin React (`contextOrFilename.getFilename`). Não atribuir aprovação global.
- Não foram executadas migrações nem escritas em dados de negócio. SELECT 1 é diagnóstico, não homologação de CRUD/jornada.

## Etapas 1–4 após esta intervenção

1. IP identificado: concluída nesta rede.
2. Banco e API ativos e conexão confirmada: concluída durante esta execução; o PC e os processos precisam continuar ligados.
3. Acesso Android: confirmado pelo usuário nos dois dispositivos.
4. URL/configuração corrigida e bundle validado: concluída em código; **falta gerar/instalar o novo APK e validar login/dados dentro dele**.

## Bloqueio de build e pendências

Foi solicitada execução de `npx.cmd eas-cli@latest build --platform android --profile preview --non-interactive`. **A revisão automática rejeitou a ação antes da execução**, por envolver envio do código/configuração ao serviço Expo/EAS sem autorização explícita para esse envio. Não houve novo build remoto nesta intervenção. Não contornar o bloqueio; solicitar autorização específica para destino/payload antes de tentar novamente.

Após autorização, gerar APK com a assinatura existente e entregar link; instalar e testar login/listagens no tablet ADM e smartphone RH. O APK instalado anteriormente não muda ao editar arquivos no PC.

Jornada vigente: criação → ADM autoriza realização → execução/encerramento → RH confere → ADM autoriza pagamento → RH registra quitação. Esse ordenamento corrige a sequência provisória do resumo produzido sem acesso ao projeto.

Push permanece não homologado; worker foi mantido desabilitado. Tipos/lint frontend têm pendências preexistentes, fora desta correção de conectividade. Produção/uso fora do Wi-Fi exige API HTTPS acessível, com ambiente próprio. Se IP mudar, atualizar `.env.local` e env do eas.json antes de gerar outro APK.

Logs locais desta execução: `output/android-network/api.stdout.log` e `api.stderr.log`. Para parar, confirmar o PID/porta antes de encerrar o processo correspondente. Não prometer permanência da API após reinício do computador.

## Atualização — envio autorizado e build iniciada

Em 28/10/2026, o usuário autorizou explicitamente enviar o código à Expo/EAS. O envio concluiu com sucesso; EAS carregou EXPO_PUBLIC_API_URL e PONTOXTRA_ALLOW_HTTP do perfil preview e reutilizou a Keystore remota existente. Build Android preview solicitada: 962ee26b-789e-40d7-9c0b-2d92cad39d87. Link: https://expo.dev/accounts/willianhelmuhts-team/projects/pontoxtra/builds/962ee26b-789e-40d7-9c0b-2d92cad39d87 . Estado na última saída: aguardando conclusão. Isso supera a pendência de autorização do envio; conclusão/instalação e testes do novo APK ainda não confirmados.

## 28/10/2026 — Push nativo ativado e recebimento confirmado

Usuário relatou avisos internos funcionando, sem notificação Android. Diagnóstico somente leitura: PUSH_NOTIFICATIONS_ENABLED estava false no .env e o processo anterior também havia sido iniciado com false para teste de conectividade; um dispositivo ativo e uma entrega PENDENTE. O código existente já configurava canal aprovacoes com importância HIGH, som default, apresentação foreground e payload de push com som default.

A pedido do usuário, habilitado PUSH_NOTIFICATIONS_ENABLED=true no .env backend, preservando demais configurações, e reiniciada somente a API previamente iniciada nesta tarefa. Novo PID: 146132. Sessões em memória são perdidas no reinício. GET / pelo IP Wi-Fi retornou HTTP 200. Entrega passou de PENDENTE para AGUARDANDO_RECIBO, sem erro registrado, indicando aceitação pela Expo (não leitura garantida). Teste existente front/scripts/test-push.cjs aprovado com SDK simulado.

**Usuário confirmou: a notificação apareceu no Android com som ou vibração.** Isso comprova recebimento nativo nesse aparelho/evento. Não houve alteração do código nem novo APK para esta correção; a configuração faltante estava no backend. A condição de som/vibração continua sujeita à permissão/canal e às preferências Android. Não foram alterados tokens, credenciais Firebase ou preferências do aparelho.

Continuam pendentes os cenários completos de push: demais aparelhos/perfis, foreground/background/encerrado, toque, logout e troca de conta. Em outros aparelhos, abrir Notificações > Ativar avisos neste celular e permitir notificações. Autor da ação não recebe seu próprio aviso, conforme regra existente. O backend deve permanecer ativo e com acesso à internet. A presente atualização supera os registros anteriores de worker desabilitado; não implica homologação global de todas as jornadas/notificações.
