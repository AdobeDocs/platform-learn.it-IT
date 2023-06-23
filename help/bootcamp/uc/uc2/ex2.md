---
title: Bootcamp - Journey Optimizer Crea il tuo evento
description: Bootcamp - Journey Optimizer Crea il tuo evento
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 89db40ab-d4c5-4310-aca6-cb64828e7bc9
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 2.2 Creare l’evento

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Clic **Journey Optimizer**.

![ACOP](./images/acophome.png)

Verrai reindirizzato al **Home**  in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `Bootcamp`. Per passare da una sandbox all’altra, fai clic su **Prod** e seleziona la sandbox dall’elenco. In questo esempio, la sandbox è denominata **Bootcamp**. Sarai quindi nel **Home** visualizzazione della sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Nel menu a sinistra, scorri verso il basso e fai clic su **Configurazioni**. Quindi, fai clic su **Gestisci** pulsante sotto **Eventi**.

![ACOP](./images/acopmenu.png)

Viene quindi visualizzata una panoramica di tutti gli eventi disponibili. Clic **Crea evento** per iniziare a creare un evento personalizzato.

![ACOP](./images/emptyevent.png)

Viene visualizzata una nuova finestra di evento vuota.

![ACOP](./images/emptyevent1.png)

Prima di tutto, assegna all’evento un nome simile al seguente: `yourLastNameAccountCreationEvent` e aggiungi una descrizione come questa `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Quindi, assicurati che le **Tipo** è impostato su **Unitario**, e per **Tipo ID evento** selezione, seleziona **Generato dal sistema**.

![ACOP](./images/eventidtype.png)

Di seguito è riportata la selezione dello schema. Per questo esercizio è stato preparato uno schema. Utilizza lo schema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Dopo aver selezionato lo schema, vedrai una serie di campi selezionati nel **Campi** sezione. Ora dovresti passare il cursore sopra **Campi** e vedrai 3 icone a comparsa. Fai clic sul pulsante **Modifica** icona.

![ACOP](./images/eventpayload.png)

Vedrai un **Campi** finestra a comparsa, in cui è necessario selezionare alcuni dei campi necessari per personalizzare l’e-mail.  In seguito sceglieremo altri attributi di profilo, utilizzando i dati già presenti in Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Nell&#39;oggetto `_experienceplatform.demoEnvironment`, assicurati di selezionare i campi **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

Nell&#39;oggetto `_experienceplatform.identification.core`, assicurati di selezionare il campo **email**.

![ACOP](./images/eventpayloadbrid.png)

Clic **Ok** per salvare le modifiche.

![ACOP](./images/saveok.png)

Dovresti vedere questo. Clic **Salva** ancora una volta per salvare le modifiche.

![ACOP](./images/eventsave.png)

L’evento è ora configurato e salvato.

![ACOP](./images/eventdone.png)

Fai di nuovo clic sull’evento per aprire **Modifica evento** schermo di nuovo. Passa il cursore sopra **Campi** per visualizzare di nuovo le 3 icone. Fai clic sul pulsante **Visualizza payload** icona.

![ACOP](./images/viewevent.png)

Ora vedrai un esempio del payload previsto.
L’evento ha un ID evento di orchestrazione univoco, che puoi trovare scorrendo verso il basso in tale payload fino a visualizzare `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

L’ID evento è ciò che deve essere inviato a Adobe Experience Platform per attivare il percorso che creerai in uno degli esercizi successivi. Ricorda questo eventID, in quanto potrebbe essere necessario in un secondo momento.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

Clic **Ok**, seguito da clic **Annulla**.

Hai terminato questo esercizio.

Passaggio successivo: [2.3 Creare il messaggio e-mail](./ex3.md)

[Torna a Flusso utente 2](./uc2.md)

[Torna a tutti i moduli](../../overview.md)
