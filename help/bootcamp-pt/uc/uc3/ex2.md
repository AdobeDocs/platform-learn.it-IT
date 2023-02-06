---
title: Bootcamp - Fusione fisica e digitale - Journey Optimizer Crea il tuo evento - Brasile
description: Bootcamp - Fusione fisica e digitale - Journey Optimizer Crea il tuo evento - Brasile
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 3.2 Crie seu evento

Accesso Faça su Adobe Journey Optimizer acessando a [Adobe Experience Cloud]. Clipart **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a **Pagina principale** niente Journey Optimizer. Primeiro se você está germente sandbox corrispondente. O nome do sandbox que dev ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em **Prod** e selione o sandbox na lista. Neste esempio, o nome do sandbox é **Bootcamp2**. Você estará na visualização da **Pagina principale** sandbox da fare `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Nessun menu à esquerda, ruolo para baixo e clique em **Configurazioni**. Em seguida, clique no botão **Gestisci** em Eventos.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos disponíveis. Clipart **Crea evento** para começar a parroco seu próposevento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia irá aparecer.

Em primeiro chargar, dê um nome ao seu evento como, por exemplo: `yourLastNameBeaconEntryEvent` e adicione uma descrição como, por exesemplo: `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

Em seguida, certificfique se de que **Tipo** está definido como **Unitario** e, para a seleção de **Tipo ID evento**, selione **Sistema generato**.

![ACOP](./images/eventidtype.png)

Un etapa seguinte a seleção do schema. Um schema foi preparado para este exercício. Utilizzo di uno schema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selionar o Schema, você verá vários campos sendo selecionados na seção **Campi**. Agora você deve passar del topo sobre a seção **Campi** e três ícones pop-up serão exibidos. Clique no ícone de **Modifica**.

![ACOP](./images/eventpayload.png)

Você verá uma janela pop-up de **Campi**, onde você deviva algune selionari dos campos que precisamos para personalizar a jornada. Escolheremos outros ributos de perfil posteriori, utilizando os dados já esiste na Adobe Experience Platform

![ACOP](./images/eventfields.png)

Ruolo para baixo até ver o objeto `Place context` e marque a caixa de seleção. Com isso, todo o contexto da localização do cliente disponibilizado para a jornada. Clipart **Ok** para salvar suas alterações.

![ACOP](./images/eventpayloadbr.png)

Em seguida, você deverá ver a tela abaixo. Clipart **Salva** mais uma vez para salvar suas alterações.

![ACOP](./images/eventsave.png)

Seu evento agora está configurado e salvo.

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir a tela **Modifica evento** mais uma vez. Passe o sobria **Campi** para ver os 3 ícones. Clique no ícone **Visualizza**.

![ACOP](./images/viewevent.png)

Agora você verá um exemplo da carga útil esperada.
Seu evento tem um eventID de orquestração único, que você pode encontrando rolando para baixo nessa carga útil até visualiza `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jornada que você vinuirá em um dos próximos exercícios. Lembre-se deste eventID, você pode preciso del posteriore.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

Clipart **Ok** e, em seguida, clique em **Cancellare**.

Você terminou este exercício.

Próxima etapa: [3.3 Crie sua jornada e notificação push](./ex3.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
