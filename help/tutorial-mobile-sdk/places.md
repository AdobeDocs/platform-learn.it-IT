---
title: Utilizzare Places con Platform Mobile SDK
description: Scopri come utilizzare il servizio di geolocalizzazione Places nella tua app mobile.
jira: KT-14635
exl-id: adc2952f-cb01-4e06-9629-49fb95f22ca5
source-git-commit: 3186788dfb834f980f743cef82942b3cf468a857
workflow-type: tm+mt
source-wordcount: '1588'
ht-degree: 2%

---

# Usa luoghi

Scopri come utilizzare il servizio di geolocalizzazione Places nella tua app.

Il servizio Adobe Experience Platform Data Collection Places è un servizio di geolocalizzazione che consente alle app mobili dotate di awareness della posizione di contestualizzare quest’ultima. Il servizio utilizza interfacce SDK avanzate e facili da usare, associate a un database flessibile di punti di interesse (POI).

## Prerequisiti

* Tutte le dipendenze del pacchetto sono presenti nel progetto Xcode.
* Estensioni registrate in AppDelegate.
* MobileCore configurato per utilizzare l&#39;appId di sviluppo.
* SDK importati.
* L&#39;app è stata creata ed eseguita correttamente con le modifiche precedenti.

## Obiettivi di apprendimento

In questa lezione, potrai

* Scopri come definire i punti di interesse nel servizio Places.
* Aggiorna la proprietà tag con l’estensione Places.
* Aggiorna lo schema per acquisire eventi di geolocalizzazione.
* Convalidare l&#39;impostazione in Assurance.
* Aggiorna l’app per registrare l’estensione Luoghi.
* Implementa il tracciamento della geolocalizzazione dal servizio Places nell’app.


## Configurazione

Affinché il servizio Places funzioni all’interno dell’app e nell’SDK di Mobile, devi effettuare alcune impostazioni.

### Definisci luoghi

È possibile definire alcuni punti di interesse nel servizio Places.

1. Nell&#39;interfaccia utente di Data Collection, selezionare **[!UICONTROL Places]**.
1. Seleziona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg).
1. Dal menu di scelta rapida, selezionare **[!UICONTROL Gestisci librerie]**.
   ![Gestisci librerie](assets/places-manage-libraries.png)
1. Nella finestra di dialogo **[!UICONTROL Gestisci librerie]**, seleziona **[!UICONTROL Nuovo]**.
1. Nella finestra di dialogo **[!UICONTROL Crea libreria]** immetti un **[!UICONTROL Nome]**, ad esempio `Luma`.
1. Seleziona **[!UICONTROL Conferma]**.
   ![Crea libreria](assets/places-create-library.png)
1. Per chiudere la finestra di dialogo **[!UICONTROL Gestisci librerie]**, selezionare **[!UICONTROL Chiudi]**.
1. Di nuovo in **[!UICONTROL Gestione POI]**, seleziona **[!UICONTROL Importa POI]**.
1. Seleziona **[!UICONTROL Inizio]** nella finestra di dialogo **[!UICONTROL Importa luoghi]**.
1. Seleziona **[!DNL Luma]** dall&#39;elenco delle librerie,
1. Seleziona **[!UICONTROL Avanti]**.
   ![Seleziona libreria](assets/places-import-select-library.png)
1. Scarica il file ZIP [Luma POIs](assets/luma_pois.csv.zip) ed estrailo in una posizione sul computer.
1. Nella finestra di dialogo **[!UICONTROL Importa luoghi]**, trascina il file `luma_pois.csv` estratto su **[!UICONTROL Scegli il file CSV - Trascina e rilascia il file]**. Dovresti trovare **[!UICONTROL Convalida completata]** - **[!UICONTROL Il file CSV è stato convalidato correttamente]**.
1. Selezionare **[!UICONTROL Inizia importazione]**. Dovresti vedere **[!UICONTROL Operazione completata]** - **[!UICONTROL Sono stati aggiunti 6 nuovi POI]**.
1. Seleziona **[!UICONTROL Fine]**.
1. In **[!UICONTROL Gestione POI]**, dovresti notare che sei nuovi store Luma sono stati aggiunti all&#39;elenco. Puoi passare dalla visualizzazione ![Elenco](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) alla visualizzazione ![Mappa](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MapView_18_N.svg).
   ![Elenco luoghi](assets/places-list.png).


### Estensione Install Places

1. Passa a **[!UICONTROL Tag]**, individua la proprietà del tag mobile e apri la proprietà.
1. Seleziona **[!UICONTROL Estensioni]**.
1. Seleziona **[!UICONTROL Catalogo]**.
1. Cerca l&#39;estensione **[!UICONTROL Places]**.
1. Installa l’estensione.

   ![Aggiungi estensione Decisioning](assets/tag-places-extension.png)

1. Nella finestra di dialogo **[!UICONTROL Installa estensione]**:
   1. Selezionare **[!DNL Luma]** dall&#39;elenco **[!UICONTROL Seleziona una libreria]**.
   1. Verifica di aver scelto la tua libreria di lavoro, ad esempio **[!UICONTROL Build iniziale]**.
   1. Seleziona **[!UICONTROL Salva nella libreria e genera]** da **[!UICONTROL Salva nella libreria]**.

      ![Installa estensione Luoghi](assets/places-install-extension.png).

1. La libreria viene ricreata.


### Verifica lo schema

Verifica se lo schema, come definito in [Crea schema](create-schema.md), incorpora i gruppi di campi e le classi necessari per raccogliere i dati dei punti di interesse e di geolocalizzazione.

1. Passa all&#39;interfaccia di Data Collection e seleziona **[!UICONTROL Schemi]** dalla barra a sinistra.
1. Seleziona **[!UICONTROL Sfoglia]** dalla barra superiore.
1. Seleziona lo schema per aprirlo.
1. Nell&#39;editor schema, selezionare **[!UICONTROL Evento esperienza del consumatore]**.
1. È presente un oggetto **[!UICONTROL placeContext]** con oggetto e campi per acquisire i dati di interazione e geolocalizzazione dei punti di interesse.
   ![Posizioni schema](assets/schema-places-context.png).


### Aggiornare la proprietà tag

L’estensione Luoghi per i tag fornisce funzionalità per monitorare gli eventi di geolocalizzazione e consente di attivare azioni basate su tali eventi. Puoi utilizzare questa funzionalità per ridurre al minimo la codifica API da implementare nell’app.

**Elementi dati**

Innanzitutto, puoi creare diversi elementi dati.

1. Passa alla proprietà tag nell’interfaccia utente di Data Collection.
1. Seleziona **[!UICONTROL Elementi dati]** dalla barra a sinistra.
1. Selezionare **[!UICONTROL Aggiungi elemento dati]**.
1. Nella schermata **[!UICONTROL Crea elemento dati]**, immettere un nome, ad esempio `Name - Entered`.
1. Seleziona **[!UICONTROL Luoghi]** dall&#39;elenco **[!UICONTROL Estensione]**.
1. Selezionare **[!UICONTROL Nome]** dall&#39;elenco **[!UICONTROL Tipo elemento dati]**.
1. Seleziona **[!UICONTROL Current POI]** sotto **[!UICONTROL TARGET]**.
1. Seleziona **[!UICONTROL Salva nella libreria]**.
   ![Elemento dati](assets/tags-create-data-element.png)

1. Ripeti i passaggi da 4 a 8 utilizzando le informazioni della tabella seguente, per creare elementi di dati aggiuntivi.

   | Nome | Estensione | Tipo di elemento dati | TARGET |
   |---|---|---|---|
   | `Name - Exited` | Places | Nome | Ultimo punto di interesse di uscita |
   | `Category - Current` | Places | Categoria | POI corrente |
   | `Category - Exited` | Places | Categoria | Ultimo punto di interesse di uscita |
   | `City - Current` | Places | Città | POI corrente |
   | `City - Exited` | Places | Città | Ultimo punto di interesse di uscita |

   Dovresti disporre del seguente elenco di elementi dati.

   ![Elenco di elementi dati](assets/tags-data-elements-list.png)

**Regole**

Ora devi definire le regole da utilizzare con questi elementi dati.

1. Nella proprietà tag, seleziona **[!UICONTROL Regole]** dalla barra a sinistra.
1. Seleziona **[!UICONTROL Aggiungi regola]**.
1. Nella schermata **[!UICONTROL Crea regola]**, immetti un nome per la regola, ad esempio `POI - Entry`.
1. Seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) sotto **[!UICONTROL EVENTI]**.
   1. Seleziona **[!UICONTROL Luoghi]** dall&#39;elenco **[!UICONTROL Estensione]** e seleziona **[!UICONTROL Inserisci POI]** dall&#39;elenco **[!UICONTROL Tipo evento]**.
   1. Seleziona **[!UICONTROL Mantieni modifiche]**.

      ![Tag evento](assets/tags-event-mobile-core.png).
1. Seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) sotto **[!UICONTROL AZIONI]**.
   1. Seleziona **[!UICONTROL Mobile Core]** dall&#39;elenco **[!UICONTROL Extension]**, seleziona **[!UICONTROL Allega dati]** da **[!UICONTROL Action Type]**. Questa azione allega i dati del payload.
   1. Nel payload **[!UICONTROL JSON]**, incolla il seguente payload:

      ```json
      {
          "xdm": {
              "eventType": "location.entry",
              "placeContext": {
                  "geo": {
                      "city": "{%%City - Current%%}"
                  },
                  "POIinteraction": {
                      "poiDetail": {
                          "name": "{%%Name - Current%%}",
                          "category": "{%%Category - Current%%}"
                      },
                      "poiEntries": {
                          "value": 1
                      }
                  }
              }
          }
      }
      ```

      Puoi anche inserire `{%% ... %%}` valori segnaposto di elementi dati nel JSON selezionando ![Dati](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg). Una finestra di dialogo a comparsa consente di scegliere qualsiasi elemento dati creato.

   1. Seleziona **[!UICONTROL Mantieni modifiche]**.

      ![Azione tag](assets/tags-action-mobile-core.png)

1. Seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) accanto all&#39;azione **[!UICONTROL Core mobile - Allega dati]**.
   1. Seleziona **[!UICONTROL Edge Network Adobe Experience Platform]** dall&#39;elenco **[!UICONTROL Estensione]** e seleziona **[!UICONTROL Inoltra evento all&#39;Edge Network]**. Questa azione assicura che l’evento e i dati di payload aggiuntivi vengano inoltrati all’Edge Network di Platform.
   1. Seleziona **[!UICONTROL Mantieni modifiche]**.

1. Per salvare la regola, selezionare **[!UICONTROL Salva nella libreria]**.

   ![Regola](assets/tags-rule-poi-entry.png)

Creiamo un’altra regola

1. Nella schermata **[!UICONTROL Crea regola]**, immetti un nome per la regola, ad esempio `POI - Exit`.
1. Seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) sotto **[!UICONTROL EVENTI]**.
   1. Seleziona **[!UICONTROL Luoghi]** dall&#39;elenco **[!UICONTROL Estensione]** e seleziona **[!UICONTROL Esci da POI]** dall&#39;elenco **[!UICONTROL Tipo evento]**.
   1. Seleziona **[!UICONTROL Mantieni modifiche]**.
1. Seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) sotto **[!UICONTROL AZIONI]**.
   1. Selezionare **[!UICONTROL Mobile Core]** dall&#39;elenco **[!UICONTROL Extension]**, selezionare **[!UICONTROL Allega dati]** dall&#39;elenco **[!UICONTROL Action Type]**.
   1. Nel payload **[!UICONTROL JSON]**, incolla il seguente payload:

      ```json
      {
          "xdm": {
              "eventType": "location.exit",
              "placeContext": {
                  "geo": {
                      "city": "{%%City - Exited%%}"
                  },
                  "POIinteraction": {
                      "poiExits": {
                          "value": 1
                      },
                      "poiDetail": {
                          "name": "{%%Name - Exited%%}",
                          "category": "{%%Category - Exited%%}"
                      }
                  }
              }
          }
      }
      ```

   1. Seleziona **[!UICONTROL Mantieni modifiche]**.

1. Seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) accanto all&#39;azione **[!UICONTROL Core mobile - Allega dati]**.
   1. Seleziona **[!UICONTROL Edge Network Adobe Experience Platform]** dall&#39;elenco **[!UICONTROL Estensione]** e seleziona **[!UICONTROL Inoltra evento all&#39;Edge Network]**.
   1. Seleziona **[!UICONTROL Mantieni modifiche]**.

1. Per salvare la regola, selezionare **[!UICONTROL Salva nella libreria]**.

   ![Regola](assets/tags-rule-poi-exit.png)


Per pubblicare tutte le modifiche apportate al tag

1. Selezionare **[!UICONTROL Build iniziale]** come libreria da compilare.
1. Seleziona **[!UICONTROL Build]**.
   ![Genera libreria](assets/tags-build-library.png)




## Convalida impostazione in Assurance

Per convalidare la configurazione in Assurance:

1. Passa all’interfaccia utente Assurance.
1. Se non è già disponibile nella barra a sinistra, seleziona **[!UICONTROL Configura]** nella barra a sinistra e seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) accanto a **[!UICONTROL Eventi]** e **[!UICONTROL Mappa e simula]** sotto **[!UICONTROL PLACES SERVICE]**.
1. Seleziona **[!UICONTROL Salva]**.
1. Seleziona **[!UICONTROL Mappa e simula]** nella barra a sinistra.
1. Sposta la mappa nella posizione di uno dei punti di interesse.
1. Seleziona ![Ingranaggio](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Gears_18_N.svg) Simula punti di interesse di caricamento. Il punto di interesse viene identificato mediante un cerchio e un pin.
1. Seleziona il punto di interesse.
1. Dal popup, selezionare ![Gear](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Gears_18_N.svg) **[!UICONTROL Simulate Entry Event]**.
   ![Simula evento di ingresso](assets/places-simulate.png)
1. Seleziona **[!UICONTROL Eventi]** dalla barra a sinistra per visualizzare gli eventi simulati.
   ![Convalida di AJO Decisioning](assets/places-events.png)


## Implementare Places nell’app

Come descritto nelle lezioni precedenti, l’installazione di un’estensione tag per dispositivi mobili fornisce solo la configurazione. Ora devi installare e registrare l’SDK Places. Se questi passaggi non sono chiari, controlla la sezione [Installare gli SDK](install-sdks.md).

>[!NOTE]
>
>Se hai completato la sezione [Installare gli SDK](install-sdks.md), l&#39;SDK Luoghi è già installato e puoi saltare questo passaggio.
>

1. In Xcode, accertati che [AEP Places](https://github.com/adobe/aepsdk-places-ios) sia aggiunto all&#39;elenco dei pacchetti nelle dipendenze dei pacchetti. Consulta [Gestione pacchetti Swift](install-sdks.md#swift-package-manager).
1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL AppDelegate]** nel Navigator dei progetti Xcode.
1. Assicurarsi che `AEPPlaces` faccia parte dell&#39;elenco delle importazioni.

   ```swift
   import AEPPlaces
   ```

1. Assicurarsi che `Places.self` faccia parte dell&#39;array di estensioni che si sta registrando.

   ```swift
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   ```

1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** nel navigatore progetti Xcode e trova la funzione `func processRegionEvent(regionEvent: PlacesRegionEvent, forRegion region: CLRegion) async`. Aggiungi il seguente codice:

   ```swift
   // Process geolocation event
   Places.processRegionEvent(regionEvent, forRegion: region)
   ```

   Questa API [`Places.processRegionEvent`](https://developer.adobe.com/client-sdks/documentation/places/api-reference/#processregionevent) comunica le informazioni di geolocalizzazione al servizio Places.

1. Passa a **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Location]** > **[!DNL GeofenceSheet]** nel Navigatore progetti di Xcode.

   1. Per il pulsante Immissione, immettere il codice seguente

   ```swift
   // Simulate geofence entry event
   Task {
       await MobileSDK.shared.processRegionEvent(regionEvent: .entry, forRegion: region)
   }
   ```

   1. Per il pulsante Esci, immetti il codice seguente

   ```swift
   // Simulate geofence exit event
   Task {
       await MobileSDK.shared.processRegionEvent(regionEvent: .exit, forRegion: region)
   }
   ```

## Convalida tramite l’app

1. Apri l’app su un dispositivo o nel simulatore.

1. Passa alla scheda **[!UICONTROL Posizione]**.

1. Sposta (trascina) la mappa per assicurarti che il cerchio blu centrale sia sopra uno dei punti di interesse, ad esempio Londra.

1. Tocca <img src="assets/geobutton.png" width="20" /> finché la categoria e il nome non vengono visualizzati nell&#39;etichetta nella posizione rossa con il pin.

1. Tocca l&#39;etichetta del punto di interesse, che apre il foglio **[!UICONTROL POI nelle vicinanze]**.

   <img src="assets/appgeolocation.png" width="300" />

1. Premi i pulsanti **[!UICONTROL Entrata]** o **[!UICONTROL Uscita]** per simulare eventi di entrata recinto geografico e uscita recinto geografico dall&#39;app.

   <img src="assets/appentryexit.png" width="300" />

1. Dovresti visualizzare gli eventi nell’interfaccia utente Assurance.



## Passaggi successivi

Ora dovresti disporre di tutti gli strumenti necessari per iniziare ad aggiungere ulteriori funzionalità alla funzionalità di geolocalizzazione nell’app. Dopo aver inoltrato gli eventi all&#39;Edge Network, dopo aver configurato l&#39;app per l&#39;[Experience Platform](platform.md), dovresti vedere gli eventi esperienza visualizzati per il profilo utilizzato nell&#39;app.

Nella sezione Journey Optimizer di questo tutorial, vedrai che gli eventi di esperienza possono essere utilizzati per attivare i percorsi (vedi [notifica push](journey-optimizer-inapp.md) e [messaggistica in-app](journey-optimizer-push.md) con Journey Optimizer). Ad esempio, il solito esempio di invio all’utente dell’app di una notifica push con una promozione di prodotto quando l’utente entra nel recinto geografico di un negozio fisico.

Hai visto un’implementazione delle funzionalità dell’app, principalmente guidata dal servizio Places e dagli elementi dati e regole definiti nella proprietà tag. Di conseguenza, la riduzione a icona del codice nell’app. In alternativa, puoi implementare la stessa funzionalità direttamente nell&#39;app utilizzando l&#39;API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) (vedi [Eventi](events.md) per ulteriori informazioni) con un payload XDM contenente un oggetto `placeContext` popolato.

>[!SUCCESS]
>
>Ora hai abilitato l’app per i servizi di geolocalizzazione utilizzando l’estensione Places nell’SDK di Experience Platform Mobile.
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [Experience League post di discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[Mappa i dati su Adobe Analytics](analytics.md)**
