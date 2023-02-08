---
title: Bootcamp - Journey Optimizer Crea il tuo evento - Brasile
description: Bootcamp - Journey Optimizer Crea il tuo evento - Brasile
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# 2.2 Crie seu evento

Accesso Faça su Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). Clipart **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a visualização da a **Pagina principale** niente Journey Optimizer. Primeiro se você está germente sandbox corrispondente. O nome do sandbox que dev ser usado é `Bootcamp`. Para alternar de um sandbox para outro, clique em Prod e selecione o sandbox na lista. Neste esempio, o nome do sandbox é **Bootcamp**. Você estará na visualização da **Pagina principale** sandbox da fare `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Nessun menu à esquerda, ruolo para baixo e clique em **Configurazioni**. Em seguida, clique no botão **Gestisci** abaixo de **Eventi**.

![ACOP](./images/acopmenu.png)

Você verá uma visão geral de todos os eventos disponíveis. Clipart **Crea evento** para começar a parroco seu próposevento.

![ACOP](./images/emptyevent.png)

Uma nova janela de evento vazia irá aparecer.

![ACOP](./images/emptyevent1.png)

Em primeiro chargar, dê um nome ao seu evento como, por exemplo: `seuSobrenomeAccountCreationEvent` e adicione uma descrição como, por exesemplo: `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Em seguida, certificfique se de que **Tipo** está definido como **Unitario** e, para a seleção de **Tipo ID evento**, selione **Sistema generato**.

![ACOP](./images/eventidtype.png)

Un etapa seguinte a seleção do schema. Um schema foi preparado para este exercício. Utilizzo di uno schema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Depois de selionar o Schema, você verá vários campos sendo selecionados na seção **Campi**. Agora você deve passar del topo sobre a seção **Campi** e três ícones pop-up serão exibidos. Clique no ícone **Modifica**.

![ACOP](./images/eventpayload.png)

Você verá uma janela pop-up de **Campi**, onde você devono selionar alguns dos campos que precisamos para personalizar o e-mail. Escolheremos outros ributos de perfil posteriori, utilizando os dados já esiste na Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Nessun oggetto `_experienceplatform.demoEnvironment`, pcertificfique-se de selionar os campos **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

Nessun oggetto `_experienceplatform.identification.core`, certificate-se de selionar o campo **email**.

![ACOP](./images/eventpayloadbrid.png)

Clipart **Ok** a para salvar suas alterações.

![ACOP](./images/saveok.png)

Em seguida, a tela abaixo deve ser exibida. Clipart **Salva**  mais uma vez para salvar suas alterações.

![ACOP](./images/eventsave.png)

Seu evento agora está configurado e salvo.

![ACOP](./images/eventdone.png)

Clique no seu evento novamente para abrir mais uma vez a tela **Modifica evento**. Passe o sobria **Campi** para ver os 3 ícones outra vez. Clique no ícone **Visualizza payload**.

![ACOP](./images/viewevent.png)

Agora você verá um exemplo da carga útil esperada.
Seu evento tem um eventID de orquestração único, que você pode encontrar rolando para baixo nessa carga útil (payload) até visualizar `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

O eventID é o que deve ser enviado à Adobe Experience Platform para acionar a jornada que você vinuirá em um dos próximos exercícios. Lembre-se deste eventID, você pode preciso del posteriore.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

Clipart **Ok** e, em seguida, clique em **Annulla**.

Agora você terminou este exercício.

Próxima etapa: [ 2.3 Crie sua mensagem de e-mail](./ex3.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
