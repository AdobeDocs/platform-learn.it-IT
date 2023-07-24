---
title: Bootcamp - Journey Optimizer Crea il tuo evento - Brasile
description: Bootcamp - Journey Optimizer Crea il tuo evento - Brasile
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 1b9d7a35-cddf-4f4a-ad0a-95723b00c278
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 2.2 Crie seu evento

Accesso a Faça da Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a visualização da **Home** nessuna Journey Optimizer. Primeiro, verifique se você está o sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em Prod e selecione o sandbox na lista. Neste exemplo, o nome do sandbox é **Bootcamp**. Você estará na visualização da **Home** do seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Nessun menu à esquerda, ruolo para baixo e clique em **Configurazioni**. Em seguida, cricca no botão **Gestisci** abaixo de **Eventi**.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos disponíveis. Clique em **Crea evento** para começar a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia irá aparecer.

![ACOP](./images/emptyevent1.png)

Em primeiro lugar, dê um nome ao seu evento como, por exemplo: `seuSobrenomeAccountCreationEvent` e adicione uma descrição como, por exemplo: `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Em seguida, certifique-se de que **Tipo** está definido como **Unitario** e, para a seleção de **Tipo ID evento**, selecione **Generato dal sistema**.

![ACOP](./images/eventidtype.png)

Un etapa seguinte é a seleção do schema. Um schema per preparado para este exercício. Utilizzo dello schema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema, você verá vários campos sendo selecionados na seção **Campi**. Agora você deve passar o mouse sobre a seção **Campi** e três ícones pop-up serão exibidos. Clique no ícone **Modifica**.

![ACOP](./images/eventpayload.png)

Você verá uma janela pop-up de **Campi**, onde você deve selecionar alguns dos campos que precisamos para personalizar o e-mail. Escolheremos outros atributos de perfil posteriormente, utilizando os dados já exists na Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Nessun oggetto `_experienceplatform.demoEnvironment`, pcertifique-se de selecionar os campos **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

Nessun oggetto `_experienceplatform.identification.core`, certifique-se de selecionar o campo **email**.

![ACOP](./images/eventpayloadbrid.png)

Clique em **Ok** al para salvar suas alterações.

![ACOP](./images/saveok.png)

Em seguida, una tela abaixo deve ser exibida. Clique em **Salva**  mais uma vez para salvar suas alterações.

![ACOP](./images/eventsave.png)

Seu evento agora está configurado e salva.

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir mais uma vez a tela **Modifica evento**. Passe o mouse sobre **Campi** para ver os 3 ícones outra vez. Clique no ícone **Visualizza payload**.

![ACOP](./images/viewevent.png)

Agora você verá um exemplo da carga útil esperada.
Seu evento tem um eventID de orquestração único, que você pode encontrar rolando para baixo nessa carga útil (payload) até visualizar `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jornada que você costrutto em um dos próximos exercícios. Lembre-se deste eventID, você pode precisar dele posteriormente in posizione normale.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

Clique em **Ok** e, em seguida, cricca em **Annulla**.

Agora você terminou este exercício

Próxima etapa [ 2.3 Crie sua mensagem de e-mail](./ex3.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
