---
title: Bootcamp - Fusione fisica e digitale - Journey Optimizer Crea il tuo evento - Brasile
description: Bootcamp - Fusione fisica e digitale - Journey Optimizer Crea il tuo evento - Brasile
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# 3.2 Creare un evento

Accedi a Adobe Journey Optimizer accedendo a [Adobe Experience Cloud](https://experience.adobe.com). Fai clic su **Journey Optimizer**.

![ACOP](./images/acophome.png)

Verrai reindirizzato al **Pagina principale**  in Journey Optimizer. In primo luogo, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare è denominata `Bootcamp`. Per passare da una sandbox all’altra, fai clic su **Prod** e selezionate la sandbox dall’elenco. In questo esempio, la sandbox è denominata **Bootcamp2**. Allora sarai nel **Pagina principale** visualizzazione della sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Nel menu a sinistra, scorri verso il basso e fai clic su **Configurazioni**. Fai clic su **Gestisci** pulsante sotto **Eventi**.

![ACOP](./images/acopmenu.png)

Verrà visualizzata una panoramica di tutti gli eventi disponibili. Fai clic su **Crea evento** per iniziare a creare un proprio evento.

![ACOP](./images/emptyevent.png)

Viene quindi visualizzata una nuova finestra di evento vuota.

Prima di tutto, dai al tuo Evento un Nome come questo: `yourLastNameBeaconEntryEvent` e aggiungi una descrizione come questa `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

Quindi, assicurati che **Tipo** è impostato su **Unitario** e per **Tipo ID evento** selezione, seleziona **Sistema generato**.

![ACOP](./images/eventidtype.png)

Segue la selezione dello schema. È stato preparato uno schema per questo esercizio. Utilizzare lo schema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Dopo aver selezionato lo schema, nella sezione **Campi** sezione . Ora dovresti passare il cursore sul pulsante **Campi** e vedrai 3 icone a comparsa. Fai clic sul pulsante **Modifica** icona.

![ACOP](./images/eventpayload.png)

Vedrete un **Campi** finestra a comparsa, in cui è necessario selezionare alcuni dei campi necessari per personalizzare il percorso.  Sceglieremo altri attributi di profilo in un secondo momento, utilizzando i dati già presenti in Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Scorri verso il basso fino a visualizzare l’oggetto `Place context` e seleziona la casella di controllo . In questo modo, tutto il contesto della posizione del cliente sarà reso disponibile al percorso. Fai clic su **Ok** per salvare le modifiche.

![ACOP](./images/eventpayloadbr.png)

Dovresti vedere questo. Fai clic su **Salva** ancora una volta per salvare le modifiche.

![ACOP](./images/eventsave.png)

L’evento è ora configurato e salvato.

![ACOP](./images/eventdone.png)

Fai nuovamente clic sull&#39;evento per aprire **Modifica evento** schermo di nuovo. Passa il cursore **Campi** di nuovo per vedere le 3 icone. Fai clic sul pulsante **Visualizza** icona.

![ACOP](./images/viewevent.png)

Viene ora visualizzato un esempio del payload previsto.
L&#39;evento dispone di un ID evento di orchestrazione univoco, che è possibile trovare scorrendo in quel payload fino a quando non viene visualizzato `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

L’ID evento è ciò che deve essere inviato a Adobe Experience Platform per attivare il percorso che verrà generato in uno dei prossimi esercizi. Ricorda questo eventID, in quanto potrebbe essere necessario in seguito.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

Fai clic su **Ok**, seguito da clic su **Annulla**.

Ora avete finito questo esercizio.

Passaggio successivo: [3.3 Creare il percorso e la notifica push](./ex3.md)

[Torna al flusso utente 3](./uc3.md)

[Torna a tutti i moduli](../../overview.md)
