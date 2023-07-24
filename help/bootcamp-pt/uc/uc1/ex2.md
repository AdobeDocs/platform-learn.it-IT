---
title: Bootcamp - Real-time Customer Profile - Visualizza il tuo Real-time Customer Profile - Interfaccia utente - Brasile
description: Bootcamp - Real-time Customer Profile - Visualizza il tuo Real-time Customer Profile - Interfaccia utente - Brasile
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4eebb080-77fd-4162-aa64-d599f1274c93
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 2%

---

# 1.2 Visualizzare seu próprio perfil de cliente em tempo real - UI

Neste exercício, você irá fazer login na Adobe Experience Platform e visualizar seu próprio Perfil de cliente em tempo real na UI.

## História

Nessun Perfil do cliente em tempo real, todos os dados do perfil são exibidos juntamente com os dados do evento, além das associações de segmentos exists entes. Os dados mostrados podem vir de qualquer lugar, de aplicativos da Adobe e soluções externas. Essa é a exibição mais poderosa da Adobe Experience Platform, o verdadeiro local do sistema de experiência.

## 1.2.1 Utilizzare una visualização do perfil do cliente na Adobe Experience Platform

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). Accesso Depois de fazer, você irá acessar a página inicial da Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Antes de continuar, você selecionar um **sandbox**. O nome do sandbox a ser selecionado é Bootcamp. É possível fazer isso clicando no texto **[!UICONTROL Prod produzione]** è una linha azul na parte superior da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedicado.

![Acquisizione dei dati](./images/sb1.png)

Nessun menu à esquerda, acesse **Profili** e **Sfoglia**.

![Profilo cliente](./images/homemenu.png)

Nessun painel Visualizador de perfil nessun sito seu, você pode encontrar a visão geral da identidade. Cada identidade está vinculada a um namespace.

![Profilo cliente](./images/identities.png)

Nessun dolcetto Visualizador de perfil, agora você pode ver uma identidade semelhante a seguinte:

| Namespace | Identità |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 19428085896177382402834560825640259081 |

Com a Adobe Experience Platform, todos os IDs são igualmente importanti. Anteriormente, o ECID era o ID mais importante no contexto da Adobe e todos os outros IDs estavam vinculados ao ECID em uma relação hierárquica. Com a Adobe Experience Platform, isso mudou e cada ID pode ser considerado um identador primário.

Normalmente, o identificador primário dipendente do contexto. Se você perguntar ao seu Call Centre : **Qual è o ID mais importante?** Eles provavelmente responderão scrive: **o número de telefone!** Mas se você perguntar à sua equipe de CRM, eles responderão: **o endereço de e-mail** Una Adobe Experience Platform entende essa complessidade e gerencia isso para você. Cada aplicativo, seja um aplicativo da Adobe ou não, se comunicará com a Adobe Experience Platform referindo-se ao ID que consideram principal. E semplicemente funzionale.

Para o campo **Spazio dei nomi dell’identità**, selecione **ECID** e para o campo **Valore identità** insira o ECID que você pode encontrar no painel Visualizador de perfil do site do Bootcamp. Clique em **Visualizza**. Você verá seu perfil na lista. Clique no **ID profilo** para abrir seu perfil.

![Profilo cliente](./images/popupecid.png)

Agora você tem uma visão geral de alguns **Atributos de perfil** importantes do seu perfil de cliente.

![Profilo cliente](./images/profile.png)

Acesse **Eventi**, onde você pode ver come entradas de cada evento de experiência vinculado ao seu Perfil.

![Profilo cliente](./images/profileee.png)

Por fim, acesse a opção de menu **Iscrizione al segmento**. Agora você verá todos os segmentos que se qualificam para este perfil.

![Profilo cliente](./images/profileseg.png)

Agora vamos criar um novo permitirá que você personalizza un experiência do cliente para um cliente anônimo ou conhecido.

Próxima etapa [1.3 Crie um - Interfaccia utente](./ex3.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
