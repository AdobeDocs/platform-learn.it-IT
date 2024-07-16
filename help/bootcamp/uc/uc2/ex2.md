---
title: Bootcamp - Journey Optimizer Crea il tuo evento
description: Bootcamp - Journey Optimizer Crea il tuo evento
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 89db40ab-d4c5-4310-aca6-cb64828e7bc9
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# 2.2 Creare l’evento

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `Bootcamp`. Per passare da una sandbox all&#39;altra, fare clic su **Prod** e selezionare la sandbox dall&#39;elenco. In questo esempio, la sandbox è denominata **Bootcamp**. Ti troverai quindi nella **Home** della tua sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Nel menu a sinistra, scorri verso il basso e fai clic su **Configurazioni**. Fare clic sul pulsante **Gestisci** in **Eventi**.

![ACOP](./images/acopmenu.png)

Viene quindi visualizzata una panoramica di tutti gli eventi disponibili. Fai clic su **Crea evento** per iniziare a creare il tuo evento.

![ACOP](./images/emptyevent.png)

Viene visualizzata una nuova finestra di evento vuota.

![ACOP](./images/emptyevent1.png)

Prima di tutto, assegna all&#39;evento un nome come `yourLastNameAccountCreationEvent` e aggiungi una descrizione come `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Assicurarsi quindi che il tipo **Type** sia impostato su **Unitario** e per la selezione del tipo **ID evento** selezionare **Generato dal sistema**.

![ACOP](./images/eventidtype.png)

Di seguito è riportata la selezione dello schema. Per questo esercizio è stato preparato uno schema. Utilizzare lo schema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Dopo aver selezionato lo schema, nella sezione **Fields** verranno selezionati diversi campi. Passa il cursore del mouse sulla sezione **Campi** per visualizzare la finestra a comparsa delle 3 icone. Fai clic sull&#39;icona **Modifica**.

![ACOP](./images/eventpayload.png)

Verrà visualizzata una finestra popup **Campi** in cui è necessario selezionare alcuni dei campi necessari per personalizzare l&#39;e-mail.  In seguito sceglieremo altri attributi di profilo, utilizzando i dati già presenti in Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Nell&#39;oggetto `_experienceplatform.demoEnvironment`, assicurarsi di selezionare i campi **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

Nell&#39;oggetto `_experienceplatform.identification.core`, assicurarsi di selezionare il campo **email**.

![ACOP](./images/eventpayloadbrid.png)

Fai clic su **Ok** per salvare le modifiche.

![ACOP](./images/saveok.png)

Dovresti vedere questo. Fai clic ancora una volta su **Salva** per salvare le modifiche.

![ACOP](./images/eventsave.png)

L’evento è ora configurato e salvato.

![ACOP](./images/eventdone.png)

Fai di nuovo clic sull&#39;evento per aprire di nuovo la schermata **Modifica evento**. Passa nuovamente il puntatore del mouse su **Campi** per visualizzare nuovamente le 3 icone. Fai clic sull&#39;icona **Visualizza payload**.

![ACOP](./images/viewevent.png)

Ora vedrai un esempio del payload previsto.
L&#39;evento ha un ID evento di orchestrazione univoco, che puoi trovare scorrendo verso il basso in tale payload fino a visualizzare `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

L’ID evento è ciò che deve essere inviato a Adobe Experience Platform per attivare il percorso che creerai in uno degli esercizi successivi. Ricorda questo eventID, in quanto potrebbe essere necessario in un secondo momento.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

Fare clic su **Ok**, quindi su **Annulla**.

Hai terminato questo esercizio.

Passaggio successivo: [2.3 Crea il tuo messaggio e-mail](./ex3.md)

[Torna a Flusso utente 2](./uc2.md)

[Torna a tutti i moduli](../../overview.md)
