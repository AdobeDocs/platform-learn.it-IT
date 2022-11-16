---
title: Journey Optimizer Crea un evento
description: Journey Optimizer Crea un evento
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: e35d2357-21f9-4566-b2a1-cc0cf0c64956
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 7.1 Creare un evento

Accedi a Adobe Journey Optimizer accedendo a [Adobe Experience Cloud](https://experience.adobe.com). Fai clic su **Journey Optimizer**.

![ACOP](./images/acophome.png)

Verrai reindirizzato al **Pagina principale**  in Journey Optimizer. In primo luogo, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare è denominata `--aepSandboxId--`. Per passare da una sandbox all’altra, fai clic su **PROD DI PRODUZIONE (VA7)** e selezionate la sandbox dall’elenco. In questo esempio, la sandbox è denominata **Abilitazione AEP FY22**. Allora sarai nel **Pagina principale** visualizzazione della sandbox `--aepSandboxId--`.

![ACOP](./images/acoptriglp.png)

Nel menu a sinistra, scorri verso il basso e fai clic su **Configurazioni**. Fai clic su **Gestisci** pulsante sotto **Eventi**.

![ACOP](./images/acopmenu.png)

Verrà visualizzata una panoramica di tutti gli eventi disponibili. Fai clic su **Crea evento** per iniziare a creare un proprio evento.

![ACOP](./images/emptyevent.png)

Viene quindi visualizzata una nuova finestra di evento vuota.

![ACOP](./images/emptyevent1.png)

Prima di tutto, dai al tuo Evento un Nome come questo: `--demoProfileLdap--AccountCreationEvent`.

![ACOP](./images/eventname.png)

Quindi, aggiungi una descrizione come questa `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Quindi, assicurati che **Tipo** è impostato su **Unitario** e per **Tipo ID evento** selezione, seleziona **Sistema generato**.

![ACOP](./images/eventidtype.png)

Segue la selezione dello schema. È stato preparato uno schema per questo esercizio. Utilizzare lo schema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Dopo aver selezionato lo schema, nella sezione **Payload** sezione . Ora dovresti passare il cursore sul pulsante **Payload** e vedrai 3 icone a comparsa. Fai clic sul pulsante **Modifica** icona.

![ACOP](./images/eventpayload.png)

Vedrete un **Campi** finestra a comparsa, in cui è necessario selezionare alcuni dei campi necessari per personalizzare l’e-mail.  Sceglieremo altri attributi di profilo in un secondo momento, utilizzando i dati già presenti in Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Nell’oggetto `--aepTenantId--.demoEnvironment`, assicurati di selezionare i campi **brandLogo** e **brandName**.

![ACOP](./images/eventpayloadbr.png)

Nell’oggetto `--aepTenantId--.identification.core`, assicurati di selezionare il campo **email**.

![ACOP](./images/eventpayloadbrid.png)

Fai clic su **Ok** per salvare le modifiche.

![ACOP](./images/saveok.png)

Dovresti quindi vedere questo:

![ACOP](./images/eventsave.png)

Fai clic su **Salva** ancora una volta per salvare le modifiche.

![ACOP](./images/save1.png)

L’evento è ora configurato e salvato.

![ACOP](./images/eventdone.png)

Fai nuovamente clic sull&#39;evento per aprire **Modifica evento** schermo di nuovo. Passa il puntatore del mouse **Payload** per visualizzare di nuovo le 3 icone. Fai clic sul pulsante **Visualizza payload** icona.

![ACOP](./images/viewevent.png)

Viene ora visualizzato un esempio del payload previsto.

![ACOP](./images/fullpayload.png)

L’evento dispone di un ID evento di orchestrazione univoco, che puoi trovare scorrendo in quel payload fino a quando non vedi `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

L’ID evento è ciò che deve essere inviato a Adobe Experience Platform per attivare il Percorso generato nell’esercizio 7.2. Ricorda questo ID evento, in quanto ne avrai bisogno nell’esercizio 7.3.
`"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`

Fai clic su **Ok**, seguito da clic su **Annulla**.

Ora avete finito questo esercizio.

Passaggio successivo: [7.2 Journey Optimizer: Creare il percorso e il messaggio e-mail](./ex2.md)

[Torna al modulo 7](./journey-orchestration-create-account.md)

[Torna a tutti i moduli](../../overview.md)
