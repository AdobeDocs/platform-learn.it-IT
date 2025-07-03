---
title: 'Adobe Journey Optimizer: API meteo esterna, SMS e altro ancora - Definizione di un evento'
description: Adobe Journey Optimizer - API meteo esterna, SMS e altro
kt: 5342
doc-type: tutorial
exl-id: bde4290a-59d1-4471-83a7-1cad69f94ff1
source-git-commit: d19bd2e39c7ff5eb5c99fc7c747671fb80e125ee
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 2%

---

# 3.2.1 Definire un evento

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`. Ti troverai quindi nella **Home** della tua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

Nel menu a sinistra, scorri verso il basso e fai clic su **Configurazioni**. Fare clic sul pulsante **Gestisci** in **Eventi**.

![ACOP](./images/acopmenu.png)

Viene quindi visualizzata una panoramica di tutti gli eventi disponibili. Fai clic su **Crea evento** per iniziare a creare il tuo evento.

![ACOP](./images/emptyevent.png)

Viene visualizzata una nuova finestra di evento vuota.
Come nome dell&#39;evento, utilizzare `--aepUserLdap--GeofenceEntry`.

Imposta descrizione su: `Geofence Entry Event`.

Assicurati che il **Tipo** sia impostato su **Unitario** e per la selezione del **Tipo ID evento**, seleziona **Generato dal sistema**

![Demo](./images/evname.png)

Quindi, seleziona uno schema.

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

Tuttavia, un addetto al marketing deve avere un accesso flessibile a tutti i punti dati che forniscono contesto a un percorso. Accertiamoci quindi di selezionare almeno i campi seguenti (che si trovano all’interno del nodo di contesto Luogo ):

- Città

Al termine, fare clic su **OK**.

![Demo](./images/popupok.png)

Adobe Journey Optimizer necessita anche di un identificatore per identificare il cliente. Poiché Adobe Journey Optimizer è collegato a Adobe Experience Platform, l’identificatore primario di uno schema viene automaticamente assunto come identificatore del Percorso.
L’identificatore primario terrà automaticamente conto del grafo delle identità completo di Adobe Experience Platform e collegherà tutti i comportamenti di tutte le identità, i dispositivi e i canali disponibili allo stesso profilo, in modo che Adobe Journey Optimizer sia contestuale, pertinente e coerente. Fai clic su **Salva**.

![Demo](./images/eventidentifier.png)

L’evento farà quindi parte dell’elenco degli eventi disponibili.

![Demo](./images/eventlist.png)

Infine, è necessario ripristinare `Orchestration eventID` per l&#39;evento personalizzato.

Apri nuovamente l’evento facendo clic su di esso nell’elenco degli eventi.
Nel tuo evento, fai clic sull&#39;icona **Visualizza payload** accanto a **Campi**.

![Demo](./images/fieldseyepayload.png)

Facendo clic sull&#39;icona **Visualizza payload** viene aperto un payload XDM di esempio per questo evento. Scorri verso il basso nel **Payload** fino a visualizzare la riga `eventID`.

![Demo](./images/fieldseyepayloadev.png)

Annota `eventID` in quanto ti servirà nell&#39;ultimo per testare la configurazione.

In questo esempio, `eventID` è `209a2eecb641e20a517909e186a559ced155384a26429a557eb259e5a470bca7`.

Ora hai definito l&#39;evento che attiverà il percorso che stiamo costruendo. Una volta attivato il percorso, i campi del recinto geografico come Città e tutti gli altri che potresti aver scelto (come Paese, Latitudine e Longitudine) saranno resi disponibili al percorso.

Come descritto nella descrizione del caso d’uso, dobbiamo quindi fornire promozioni contestuali che dipendono dal tempo. Per ottenere informazioni meteo, dovremo definire una fonte di dati esterna che ci fornirà le informazioni meteo per quella località. Per fornirci tali informazioni, userai il servizio **API OpenWeather**.

## Passaggi successivi

Vai a [3.2.2 Definisci un&#39;origine dati esterna](./ex2.md){target="_blank"}

Torna a [Adobe Journey Optimizer: origini dati esterne e azioni personalizzate](journey-orchestration-external-weather-api-sms.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}