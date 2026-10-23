# 07. Preparação das notificações Android

Registro: 23/10/2026. Situação: infraestrutura parcialmente configurada; notificações ainda não homologadas no aplicativo.

## Objetivo e situação

O responsável solicitou avisos de pendência e de decisão nas duas aprovações do ADM, tanto dentro do aplicativo como com ele fechado. Informou ter revertido as alterações anteriores de implementação. Não considerar aquela tentativa uma entrega vigente nem reaplicar migrações sem inspecionar código e banco separadamente.

## Concluído

- Conta e projeto PontoXtra existentes na Expo.
- Projeto Firebase criado pelo responsável, com ID pontoxtra; aplicativo Android cadastrado como com.pontoxtra.mobile.
- Login no EAS CLI autorizado pelo navegador; terminal confirmou Logged in.
- Pasta front vinculada ao projeto Expo 30458422-6b9a-441b-b5a9-4fdce1887405 por eas init; slug ajustado para pontoxtra.
- eas build:configure --platform android gerou front/eas.json com perfis development, preview e production. Nenhum build foi iniciado por esse comando.
- front/app.json contém android.package com.pontoxtra.mobile e extra.eas.projectId correspondente. Arquivos conferidos nesta data.
- Responsável enviou o JSON privado da conta de serviço pelo EAS CLI. Saída compartilhada confirmou Uploaded Google Service Account Key e assigned to com.pontoxtra.mobile for FCM V1. Confirmação baseada no terminal do usuário, sem nova consulta remota.
- FCM Legacy e credencial de submissão à Play Store ficaram sem configuração; não são necessários para essa etapa de push FCM V1.
- Usuário saiu do assistente; isso não desfaz a credencial salva.

## Ainda falta

1. Configurar android.googleServicesFile para o google-services.json já presente no frontend (existência conferida, conteúdo não lido nesta etapa). Validar correspondência de projeto/pacote. Não confundir esse arquivo com o JSON privado da conta de serviço.
2. Instalar/configurar expo-notifications e implementar permissões, canal Android, registro do token, vínculo ao usuário, leitura e abertura do aviso.
3. Implementar/revalidar o fluxo das duas aprovações e os avisos correspondentes no backend e frontend; persistência e permissões precisam ser verificadas no estado atual.
4. Configurar assinatura Android (keystore); EAS pode gerá-la. Não há confirmação de geração nesta sessão.
5. Garantir API acessível pelo celular, preparar build Android de teste e instalar o APK. Expo Go Android não atende ao teste de push remoto no SDK 57.
6. Homologar com perfis reais: pendência, aprovação/rejeição em cada etapa, app aberto, em segundo plano e fechado, toque no aviso e troca de usuário. Encerramento forçado pelo sistema/usuário pode afetar entrega; não prometer entrega garantida.

## Por que há várias configurações

Backend decide quem deve receber; Expo encaminha a mensagem; Firebase Cloud Messaging entrega no Android; sistema operacional controla permissão e apresentação. Assinatura identifica o aplicativo, credencial FCM autoriza o envio e token identifica a instalação. Essa infraestrutura também existe em apps Kotlin, Java, Flutter ou outras tecnologias.

## Segurança e limites

Não guardar JSON privado, senhas, tokens ou conteúdo de credenciais na memória ou no Git. Identificadores públicos do projeto não são a chave privada. Não foram enviados pushes nem comprovado recebimento em aparelho nesta etapa. Não executar testes de código para validar uma alteração somente documental.

## Referências

- https://docs.expo.dev/push-notifications/fcm-credentials/
- https://docs.expo.dev/push-notifications/push-notifications-setup/
- https://docs.expo.dev/versions/v57.0.0/sdk/notifications/
- https://docs.expo.dev/app-signing/managed-credentials/

Evidências: conversa e saída do EAS CLI fornecida pelo responsável; leitura de front/app.json, front/eas.json e front/package.json em 23/10/2026.
