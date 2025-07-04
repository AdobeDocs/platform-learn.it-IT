---
title: Configurare un percorso con messaggi push
description: Configurare un percorso con messaggi push
kt: 5342
doc-type: tutorial
exl-id: 63d7ee24-b6b5-4503-b104-a345c2b26960
source-git-commit: fb14ba45333bdd5834ff0c6c2dc48dda35cfe85f
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# 3.3.2 Configurare un percorso con messaggi push

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`. Ti troverai quindi nella **Home** della tua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.3.2.1 Crea un nuovo evento

Nel menu a sinistra, vai a **Configurazioni** e fai clic su **Gestisci** in **Eventi**.

![ACOP](./images/acopmenu.png)

Nella schermata **Eventi** verrà visualizzata una visualizzazione simile a questa. Fare clic su **Crea evento**.

![ACOP](./images/add.png)

Viene quindi visualizzata una configurazione dell’evento vuota.
Prima di tutto, assegna all&#39;evento un nome come `--aepUserLdap--StoreEntryEvent` e imposta la descrizione su `Store Entry Event`.
La selezione **Tipo evento** è successiva. Seleziona **Unitario**.
La selezione del **Tipo ID evento** è successiva. Selezionare **Generato dal sistema**.

![ACOP](./images/eventname.png)

Di seguito è riportata la selezione dello schema. Per questo esercizio è stato preparato uno schema. Utilizzare lo schema `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

Dopo aver selezionato lo schema, nella sezione **Payload** verranno selezionati diversi campi. Verificare che il campo **Spazio dei nomi** sia impostato su **ECID**. Il tuo evento è ora completamente configurato.

Fai clic su **Salva**.

![ACOP](./images/eventschema.png)

L’evento è ora configurato e salvato. Fai di nuovo clic sull&#39;evento per aprire di nuovo la schermata **Modifica evento**.

![ACOP](./images/eventdone.png)

Passa il puntatore del mouse sul campo **Payload** e fai clic sull&#39;icona **Visualizza payload**.

![ACOP](./images/hover.png)

Ora vedrai un esempio del payload previsto.

Il tuo evento ha un ID evento di orchestrazione univoco, che puoi trovare scorrendo verso il basso in tale payload fino a visualizzare `_experience.campaign.orchestration.eventID`.

L’ID evento è ciò che deve essere inviato a Adobe Experience Platform per attivare il Percorso che verrà generato nel passaggio successivo. Annota questo eventID, come sarà necessario nel passaggio successivo.
`"eventID": "aa895251f76831e6440f169f1bb9d2a4388f0696d8e2782cfab192a275817dfa"`

Fare clic su **Ok**.

![ACOP](./images/payloadeventID.png)

Fare clic su **Annulla**.

![ACOP](./images/payloadeventIDa.png)

## 3.3.2.2 Creazione di un percorso

Nel menu a sinistra, vai a **Percorsi** e fai clic su **Crea Percorso**.

![DSN](./images/sjourney1.png)

Poi vedrai questo. Assegnare un nome al percorso: `--aepUserLdap-- - Store Entry journey`. Fai clic su **Salva**.

![DSN](./images/sjourney3.png)

Innanzitutto, devi aggiungere l’evento come punto di partenza del percorso. Cercare l&#39;evento `--aepUserLdap--StoreEntryEvent` e trascinarlo sull&#39;area di lavoro. Fai clic su **Salva**.

![DSN](./images/sjourney4.png)

Quindi, in **Azioni**, cerca l&#39;azione **Invia**. Trascina e rilascia l&#39;azione **Push** nell&#39;area di lavoro.

Imposta **Categoria** su **Marketing** e seleziona una superficie push che ti consenta di inviare notifiche push. In questo caso, la superficie e-mail da selezionare è **Push-iOS-Android**.

>[!NOTE]
>
>Deve esistere un canale in Journey Optimizer che utilizza la **superficie app** come rivisto in precedenza.

![ACOP](./images/journeyactions1push.png)

Il passaggio successivo consiste nel creare il messaggio. A tale scopo, fare clic su **Modifica contenuto**.

![ACOP](./images/journeyactions2push.png)

Poi vedrai questo. Fai clic sull&#39;icona **personalization** per il campo **Title**.

![Invia](./images/bp5.png)

Poi vedrai questo. Ora puoi selezionare qualsiasi attributo di profilo direttamente da Real-time Customer Profile.

Cerca il campo **Nome**, quindi fai clic sull&#39;icona **+** accanto al campo **Nome**. Verrà quindi visualizzato il token di personalizzazione per First Name aggiunto: **{{profile.person.name.firstName}}**.

![Invia](./images/bp9.png)

Quindi, aggiungi il testo **, benvenuto nel nostro store!** dietro **{{profile.person.name.firstName}}**.

Fai clic su **Salva**.

![Invia](./images/bp10.png)

Ora hai questo. Fai clic sull&#39;icona **personalization** per il campo **Body**.

![Invia](./images/bp11.png)

Immetti questo testo **Fai clic qui per ottenere uno sconto del 10% al momento dell&#39;acquisto.** e fare clic su **Salva**.

![Invia](./images/bp12.png)

Allora avrai questo. Fai clic sulla freccia nell’angolo in alto a sinistra per tornare al percorso.

![Journey Optimizer](./images/bp12a.png)

Fai clic su **Salva** per chiudere l&#39;azione push.

![DSN](./images/sjourney8.png)

Fai clic su **Pubblica**.

![DSN](./images/sjourney10.png)

Fai di nuovo clic su **Pubblica**.

![DSN](./images/sjourney10a.png)

Il percorso è stato pubblicato.

![DSN](./images/sjourney11.png)

## 3.3.2.3 Aggiorna la proprietà di raccolta dati per dispositivi mobili

In **Guida introduttiva**, il sistema di dimostrazione ha creato le proprietà dei tag per te: uno per il sito Web e uno per l&#39;app mobile. Trovarli cercando `--aepUserLdap--` nella casella **Cerca**. Fare clic per aprire la proprietà **Mobile**.

![DSN](./images/pushpoi1.png)

Dovresti vedere questo.

![DSN](./images/pushpoi2.png)

Nel menu a sinistra, vai a **Regole** e fai clic per aprire la regola **Voce posizione**.

![DSN](./images/pushpoi3.png)

Dovresti vedere questo. Fai clic sull&#39;azione **Mobile Core - Allega dati**.

![DSN](./images/pushpoi4.png)

Dovresti vedere questo.

![DSN](./images/pushpoi5.png)

Incolla l&#39;eventID dell&#39;evento `--aepUserLdap--StoreEntryEvent` nella finestra **Payload JSON**. Fai clic su **Mantieni modifiche**.

![DSN](./images/pushpoi6.png)

Fai clic su **Salva** o **Salva nella libreria**.

![DSN](./images/pushpoi7.png)

Vai a **Flusso di pubblicazione** e fai clic per aprire la libreria **Principale**.

![DSN](./images/pushpoi8.png)

Fai clic su **Aggiungi tutte le risorse modificate**, quindi fai clic su **Salva e genera in sviluppo**.

![DSN](./images/pushpoi9.png)

## 3.3.2.4 Test del percorso e messaggio push

Aprire l&#39;applicazione **DSN Mobile**.

![DSN](./images/dxdemo1.png)

Vai alla pagina **Store Locator**.

![DSN](./images/dxdemo2.png)

Fai clic su **Simula voce POI**.

![DSN](./images/dxdemo3.png)

Dopo un paio di secondi, verrà visualizzata la notifica push.

![DSN](./images/dxdemo4.png)

## Passaggi successivi

Vai a [3.3.3 Configurare una campagna con messaggi in-app](./ex3.md){target="_blank"}

Torna a [Adobe Journey Optimizer: messaggi push e in-app](ajopushinapp.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}