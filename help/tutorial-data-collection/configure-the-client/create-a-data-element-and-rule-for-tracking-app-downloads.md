---
title: Creare un elemento dati e una regola per monitorare i download delle app
description: Creare un elemento dati e una regola per monitorare i download delle app
feature: Web SDK
exl-id: 8012ba48-38ac-4fb5-9876-8f57d1c5da5d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 2%

---

# Creare un elemento dati e una regola per monitorare i download delle app

Come promemoria, quando un utente fa clic su [!UICONTROL Scaricare l’app] , hai inviato al livello dati come segue:

```js
window.adobeDataLayer.push({
  "event": "downloadAppClicked",
  "eventInfo": {
    "web": {
      "webInteraction": {
        "URL": "https://example.com/download",
        "name": "App Download",
        "type": "download"
      }
    }
  }
});
```

Hai utilizzato il `eventInfo` , che comunica al livello dati di comunicare questi dati insieme all’evento, ma a _not_ conserva i dati all’interno del livello dati. Per un clic su un collegamento, non è utile aggiungere al livello dati le informazioni sul collegamento selezionato, perché non è applicabile ad altri eventi che possono verificarsi successivamente sulla pagina.

Per questa implementazione, invii un evento di esperienza a Adobe Experience Platform contenente il risultato unito di (1) lo stato calcolato del livello di dati e (2) il contenuto di `eventInfo`.

A questo scopo, devi creare un elemento dati che unisca questi due blocchi di informazioni.

## Creare un elemento dati

Per creare l’elemento dati appropriato:

1. Fai clic su [!UICONTROL Elementi dati] nel menu a sinistra.
1. Fai clic su [!UICONTROL Crea nuovo elemento dati] link.
1. Immetti il nome dell&#39;elemento dati, `computedStateAndEventInfo`.
1. Per [!UICONTROL Estensione] campo , seleziona [!UICONTROL Core] se non è già selezionato.
1. Per [!UICONTROL Tipo di elemento dati] campo , seleziona **[!UICONTROL Oggetti uniti]**. Questo elemento dati consente di unire più oggetti. Il risultato unito viene restituito dall’elemento dati.
1. Aggiungere il primo oggetto da includere nell&#39;unione. Invio `%event.fullState%` in [!UICONTROL Oggetto(obbligatorio)] campo . Quando viene utilizzato all&#39;interno di una regola attivata da un [!UICONTROL Dati scaricati] evento di regola, fa riferimento allo stato calcolato di Adobe Client Data Layer al momento dell&#39;attivazione della regola.
1. Fai clic sul pulsante  **[!UICONTROL Aggiungi un altro]** comando.
1. Aggiungere il secondo oggetto. Invio `%event.eventInfo%` in [!UICONTROL Oggetto(obbligatorio)] campo . Quando viene utilizzato all&#39;interno di una regola attivata da un [!UICONTROL Dati scaricati] evento di regola, fa riferimento al `eventInfo` porzione inviata ad Adobe Client Data Layer.
1. Salva l’elemento dati facendo clic sul pulsante [!UICONTROL Salva] pulsante .
   ![elemento dati computedStateAndEventInfo](../assets/computed-state-and-event-info-data-element.png)

L&#39;elemento dati è completo.

## Creare una regola

Per creare la regola per tracciare i clic sul pulsante [!UICONTROL Scaricare l’app] link:

1. Fai clic su **[!UICONTROL Regole]** nel menu a sinistra.
1. Fai clic su **[!UICONTROL Aggiungi regola]**.
1. Invio **_Fai clic sul collegamento Scarica app_** in [!UICONTROL Nome] campo .

## Aggiungere un evento

1. Fai clic sul pulsante **[!UICONTROL Aggiungi]** pulsante sotto [!UICONTROL Eventi]. Ora puoi visualizzare la visualizzazione dell’evento.
1. Per [!UICONTROL Estensione] campo , seleziona **[!UICONTROL Livello dati client di Adobe]**.
1. Per [!UICONTROL Tipo evento] campo , seleziona **[!UICONTROL Dati scaricati]**.
1. Fai clic su **[!UICONTROL Mantieni modifiche]**.
   ![Scaricare l’evento su cui l’app ha fatto clic](../assets/download-app-clicked-event.png)
Perché desideri che questa regola venga attivata solo quando `downloadAppClicked` l&#39;evento viene inviato al livello dati, seleziona **[!UICONTROL Evento specifico]** radio sotto [!UICONTROL Ascolta] e tipo **_downloadAppClic_** nel [!UICONTROL Evento / Chiave per la registrazione]  campo di testo visualizzato.

## Aggiungi un&#39;azione

Ora che sei tornato alla vista delle regole:

1. Fai clic sul pulsante **[!UICONTROL Aggiungi]** pulsante sotto [!UICONTROL Azioni].
1. Ora dovresti essere nella visualizzazione delle azioni. Per [!UICONTROL Estensione] campo , seleziona **[!UICONTROL Adobe Experience Platform Web SDK]**. Per [!UICONTROL Tipo di azione] campo , seleziona **[!UICONTROL Invia evento]**.
1. In [!UICONTROL Tipo] a destra, seleziona `web.webinteraction.linkClicks`.
1. Per [!UICONTROL Dati XDM] , fai clic sul pulsante di selezione dell’elemento dati a destra e seleziona **[!UICONTROL computedStateAndEventInfo]**. Questo è l&#39;elemento dati creato di recente.
1. Per questa regola (a differenza delle altre regole create), controlla la **[!UICONTROL Il documento verrà scaricato]** casella di controllo.
   ![Casella di controllo Scaricare il documento](../assets/document-will-unload.png)
1. Salva l’azione facendo clic sul pulsante **[!UICONTROL Mantieni modifiche]** pulsante .

>[!TIP]
>
>La [!UICONTROL Funzione di scaricamento del documento] comunica all’SDK che l’utente si allontana dalla pagina quando fa clic sul collegamento. Questo è importante, perché consente all’SDK di effettuare la richiesta anche se l’utente si sposta dalla pagina, in quanto la richiesta continua a essere in esecuzione in background e a raggiungere il server. Se questa casella di controllo è deselezionata, la richiesta non verrà effettuata in questo modo e quindi probabilmente verrà annullata quando il documento corrente viene scaricato.
>
>Potreste chiedervi, &quot;Sembra carino. Perché questa opzione non è sempre abilitata allora?&quot;
>
>Beh, è un po&#39; complicato, ma quando utilizzi questa funzione, l&#39;SDK utilizza un metodo del browser chiamato [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) per inviare la richiesta. Quando si invia una richiesta utilizzando `sendBeacon`, il browser non consente all&#39;SDK (o a qualsiasi altra cosa) di accedere ai dati restituiti dal server. Se l’SDK dovesse utilizzare questa funzione per ogni richiesta, non sarebbe mai in grado di ricevere dati dal server. Per questo motivo, è importante controllare il [!UICONTROL Il documento verrà scaricato] selezionare solo quando il documento corrente verrà scaricato, nel qual caso i dati di risposta possono essere comunque scartati.

## Salva la regola

La regola dovrebbe ora essere completa.

1. Fai clic su **[!UICONTROL Salva]** nell&#39;angolo in alto a destra.
   ![Scarica la regola su cui è stato fatto clic il collegamento all’app](../assets/download-app-link-clicked-rule.png)

[Avanti: ](publish-the-library.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento della Raccolta dati. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)