---
title: 'Adobe Journey Optimizer: API meteo esterna, SMS e altro ancora - Definizione di un evento'
description: Adobe Journey Optimizer - API meteo esterna, SMS e altro
kt: 5342
doc-type: tutorial
source-git-commit: c6ba1f751f18afe39fb6b746a62bc848fa8ec9bf
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 2%

---

# 3.2.1 Definire un evento

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxId--`. Per passare da una sandbox all&#39;altra, fare clic su **Production Prod (VA7)** e selezionare la sandbox dall&#39;elenco. In questo esempio, la sandbox è denominata **AEP Enablement FY22**. Ti troverai quindi nella **Home** della tua sandbox `--aepSandboxId--`.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

Nel menu a sinistra, scorri verso il basso e fai clic su **Configurazioni**. Fare clic sul pulsante **Gestisci** in **Eventi**.

![ACOP](./images/acopmenu.png)

Viene quindi visualizzata una panoramica di tutti gli eventi disponibili. Fai clic su **Crea evento** per iniziare a creare il tuo evento.

![ACOP](./images/emptyevent.png)

Viene visualizzata una nuova finestra di evento vuota.

![ACOP](./images/emptyevent1.png)

Come nome per l&#39;evento, utilizzare `--demoProfileLdap--GeofenceEntry`. In questo esempio, il nome evento è `vangeluwGeofenceEntry`.

Imposta descrizione su: `Geofence Entry Event`.

![Demo](./images/evname.png)

Assicurarsi quindi che il tipo **Type** sia impostato su **Unitario** e per la selezione del tipo **ID evento** selezionare **Generato dal sistema**

![ACOP](./images/eventidtype.png)

Quindi, seleziona uno schema. Tutti gli schemi mostrati di seguito sono schemi Adobe Experience Platform.

![Demo](./images/evschema.png)

Noterai che non tutti gli schemi vengono visualizzati. In Adobe Experience Platform sono disponibili molti altri schemi.
Per essere visualizzato in questo elenco, uno schema deve avere un gruppo di campi molto specifico collegato ad esso. Il gruppo di campi necessario per la visualizzazione è denominato `Orchestration eventID`.

Diamo un’occhiata rapida a come questi schemi vengono definiti in Adobe Experience Platform.

Nel menu a sinistra, vai a **Schemi** e apri in una nuova scheda del browser. In **Schemi**, passa a **Sfoglia** per visualizzare l&#39;elenco degli schemi disponibili.
Aprire lo schema `Demo System - Event Schema for Website (Global v1.1)`.

![Acquisizione dei dati](./images/schemas.png)

Dopo aver aperto lo schema, il gruppo di campi `Orchestration eventID` farà parte dello schema.
Questo gruppo di campi contiene solo due campi, `_experience.campaign.orchestration.eventID` e `originJourneyID`.

![Acquisizione dei dati](./images/schemageo.png)

Una volta che questo gruppo di campi e questo campo eventID specifico fanno parte di uno schema, quest’ultimo sarà disponibile per l’utilizzo in Adobe Journey Optimizer.

Torna alla configurazione dell’evento in Adobe Journey Optimizer.

![Demo](./images/evschema.png)

In questo caso d&#39;uso, desideri ascoltare un evento Recinto geografico per capire se un cliente si trova in una posizione specifica, quindi ora seleziona lo schema `Demo System - Event Schema for Website (Global v1.1)` come schema per l&#39;evento.

![Demo](./images/evschema1.png)

Adobe Journey Optimizer selezionerà quindi automaticamente alcuni campi obbligatori, ma puoi modificare i campi resi disponibili a Adobe Journey Optimizer.

Fai clic sull&#39;icona **matita** per modificare i campi.

![Demo](./images/editfields.png)

Viene quindi visualizzata una finestra a comparsa con una gerarchia di schemi che consente di selezionare i campi.

![Demo](./images/popup.png)

I campi come ECID e Orchestration eventID sono obbligatori e come tali sono preselezionati.

Tuttavia, un addetto al marketing deve avere un accesso flessibile a tutti i punti dati che forniscono contesto a un Percorso. Accertiamoci quindi di selezionare almeno i campi seguenti (che si trovano all’interno del nodo di contesto Luogo ):

- Città

Al termine, fare clic su **OK**.

![Demo](./images/popupok.png)

Adobe Journey Optimizer necessita anche di un identificatore per identificare il cliente. Poiché Adobe Journey Optimizer è collegato a Adobe Experience Platform, l’identificatore primario di uno schema viene automaticamente assunto come identificatore del Percorso.
L’identificatore primario terrà automaticamente conto del grafo delle identità completo di Adobe Experience Platform e collegherà tutti i comportamenti di tutte le identità, i dispositivi e i canali disponibili allo stesso profilo, in modo che Adobe Journey Optimizer sia contestuale, pertinente e coerente.

![Demo](./images/eventidentifier.png)

Fai clic su **Salva** per salvare l&#39;evento personalizzato.

![Demo](./images/save.png)

L’evento farà quindi parte dell’elenco degli eventi disponibili.

![Demo](./images/eventlist.png)

Infine, è necessario ripristinare `Orchestration eventID` per l&#39;evento personalizzato.

Apri nuovamente l’evento facendo clic su di esso nell’elenco degli eventi.
Nel tuo evento, fai clic sull&#39;icona **Visualizza payload** accanto a **Campi**.

![Demo](./images/eventlist1.png)

Facendo clic sull&#39;icona **Visualizza payload** viene aperto un payload XDM di esempio per questo evento.

![Demo](./images/fieldseyepayload.png)

Scorri verso il basso nel **Payload** fino a visualizzare la riga `eventID`.

![Demo](./images/fieldseyepayloadev.png)

Annota `eventID` in quanto ti servirà nell&#39;ultimo per testare la configurazione.

In questo esempio, `eventID` è `fa42ab7982ba55f039eacec24c1e32e5c51b310c67f0fa559ab49b89b63f4934`.

Ora hai definito l&#39;evento che attiverà il percorso che stiamo costruendo. Una volta attivato il percorso, i campi del recinto geografico come Città e tutti gli altri che potresti aver scelto (come Paese, Latitudine e Longitudine) saranno resi disponibili al percorso.

Come descritto nella descrizione del caso d’uso, dobbiamo quindi fornire promozioni contestuali che dipendono dal tempo. Per ottenere informazioni meteo, dovremo definire una fonte di dati esterna che ci fornirà le informazioni meteo per quella località. Il servizio **OpenWeather** fornirà tutte le informazioni, come parte di 2.

Passaggio successivo: [3.2.2 Definire un&#39;origine dati esterna](./ex2.md)

[Torna al modulo 3.2](journey-orchestration-external-weather-api-sms.md)

[Torna a tutti i moduli](../../../overview.md)
