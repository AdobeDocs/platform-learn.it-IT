---
title: Bootcamp - Blending physical and digital - Journey Optimizer Crea il tuo evento - Brasile
description: Bootcamp - Blending physical and digital - Journey Optimizer Crea il tuo evento - Brasile
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 2133b560-09d8-419d-bb99-05d0f3df52cc
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# 3.2 Crie seu evento

Accesso Faça a Adobe Journey Optimizer acessando a [Adobe Experience Cloud]. Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a **Home** no Journey Optimizer. Primeiro, verifique se você está o sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, cricca em **Prod** e selecione o sandbox na lista. Neste exemplo, o nome do sandbox é **Bootcamp**. Você estará na visualização da **Home** do seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Nessun menu à esquerda, ruolo para baixo e clique em **Configurazioni**. Em seguida, cricca no botão **Gestisci** em Eventi.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos disponíveis. Clique em **Crea evento** para começar a criar seu próprio evento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia irá aparecer.

Em primeiro lugar, dê um nome ao seu evento como, por exemplo: `yourLastNameBeaconEntryEvent` e adicione uma descripção como, por exemplo: `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

Em seguida, certifique-se de que **Tipo** está definido como **Unitario** e, para a seleção de **Tipo ID evento**, selecione **Generato dal sistema**.

![ACOP](./images/eventidtype.png)

Un etapa seguinte é a seleção do schema. Um schema per preparado para este exercício. Usa lo schema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selecionar o Schema, você verá vários campos sendo selecionados na seção **Campi**. Agora você deve passar o mouse sobre a seção **Fields** e três ícones pop-up serão exibidos. Clique no ícone de **Modifica**.

![ACOP](./images/eventpayload.png)

Você verá uma janela pop-up de **Fields**, onde você deve selecionar alguns dos campos que precisamos para personalizar a jornada. Escolheremos outros atributos de perfil posteriormente, utilizando os dados já exists na Adobe Experience Platform

![ACOP](./images/eventfields.png)

Para baixo até ver o objeto `Place context` e marque a caixa de seleção. Com isso, todo o contexto da localização do cliente será disponibilizado para a jornada. Cricca em **Ok** para salvar suas alterações.

![ACOP](./images/eventpayloadbr.png)

Em seguida, você deverá ver a tela abaixo. Clique em **Salva** mais uma vez para salvar suas alterações.

![ACOP](./images/eventsave.png)

Seu evento agora está configurado e salva.

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir a tela **Modifica evento** mais uma vez. Passe o mouse sobre **Fields** para ver os 3 ícones. Clique no ícone **Visualizza**.

![ACOP](./images/viewevent.png)

Agora você verá um exemplo do payload esperado
Seu evento tem um eventID de orquestração único, que você pode encontrar rolando para baixo nessa carga útil até visualiza `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jornada que você costrutto em um dos próximos exercícios. Lembre-se deste eventID, você pode precisar dele posteriormente in posizione normale.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

Cricca em **Ok** e, em seguida, Cricca em **Cancellare**.

Você terminou este exercício

Tapa Próxima: [3.3 Crie sua jornada e notificação push](./ex3.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
