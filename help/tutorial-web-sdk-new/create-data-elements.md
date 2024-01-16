---
title: Creare elementi dati
description: Scopri come creare un oggetto XDM e mappare ad esso gli elementi dati nei tag. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
feature: Tags
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 1%

---

# Creare elementi dati

Scopri come creare gli elementi dati essenziali necessari per acquisire i dati con Experienci Platform Web SDK. Acquisire sia contenuti che dati di identità sul [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Scopri come utilizzare lo schema XDM creato in precedenza per la raccolta di dati utilizzando il tipo di elemento dati Platform Web SDK denominato Variabile.

>[!NOTE]
>
> A scopo dimostrativo, gli esercizi di questa lezione si basano sull’esempio utilizzato durante [Configurare uno schema](configure-schemas.md) passaggio; creazione di oggetti XDM di esempio che acquisiscono il contenuto visualizzato e le identità degli utenti sul [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!IMPORTANT]
>
>I dati per questa lezione provengono da `[!UICONTROL digitalData]` sul sito Luma. Per visualizzare il livello dati, apri la console per sviluppatori e digita `[!UICONTROL digitalData]` per visualizzare l’intero livello dati disponibile.![livello dati digitalData](assets/data-element-data-layer.png)


Indipendentemente da Platform Web SDK, è necessario continuare a creare all’interno della proprietà tags elementi di dati che vengono mappati dalle variabili di raccolta dati del sito web, ad esempio un livello di dati, un attributo HTML o altri. Una volta creati, tali elementi dati devono essere mappati sullo schema XDM creato durante il [configurare gli schemi](configure-schemas.md) lezione. Pertanto, la creazione di elementi dati consiste in due azioni:

1. Mappatura delle variabili del sito web con elementi di dati e
1. Mappatura di tali elementi dati a un oggetto XDM

Per il passaggio 1, continui a mappare il livello dati agli elementi dati nello stesso modo in cui lo mappi attualmente, utilizzando uno qualsiasi dei tipi di elementi dati dell’estensione tag Core. Per il passaggio 2, l’estensione Platform Web SDK dispone dei seguenti tipi di elementi dati:

* ID unione evento
* Mappa identità
* Variable
* Oggetto XDM

Questa lezione si concentra sul tipo di elemento dati Variable. Crea un elemento dati per acquisire l’attività dei visitatori Luma in base al livello dati disponibile sul sito Luma. Nella prossima lezione verranno fornite informazioni su Identity Map.

>[!NOTE]
>
> I tipi di elementi dati di tipo ID unione eventi e oggetto XDM vengono raramente utilizzati per i casi limite.

## Obiettivi di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Comprendere diversi approcci per la mappatura di un livello dati su XDM
* Creare elementi dati per acquisire dati di contenuto
* Mappare elementi dati a un elemento dati di oggetti XDM


## Prerequisiti

Conoscere cos’è un livello dati, acquisire familiarità con [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} e sapere come fare riferimento agli elementi dati nei tag. Devi aver completato i seguenti passaggi precedenti nell&#39;esercitazione.

* [Configurare uno schema XDM](configure-schemas.md)
* [Configurare uno spazio dei nomi delle identità](configure-identities.md)
* [Configurare uno stream di dati](configure-datastream.md)
* [Estensione Web SDK installata nella proprietà tag](install-web-sdk.md)

>[!IMPORTANT]
>
>Il [Estensione del servizio ID Experience Cloud](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) non è necessario quando si implementa Adobe Experience Platform Web SDK, in quanto la funzionalità del servizio ID è integrata in Platform Web SDK.

## Approcci Data Layer

Esistono diversi modi per mappare i dati dal livello dati a XDM utilizzando la funzionalità tag di Adobe Experience Platform. Di seguito sono riportati alcuni pro e contro di tre diversi approcci:

* [Implementare XDM nel livello dati](create-data-elements.md#implement-xdm-in-the-data-layer)
* [Mappa su XDM nello stream di dati](create-data-elements.md#map-to-xdm-in-the-datastream)
* [Mappare su XDM nei tag](create-data-elements.md#map-data-layer-in-tags)

>[!NOTE]
>
>Gli esempi in questa esercitazione seguono l’approccio Map to XDM in tags.


### Implementare XDM nel livello dati

Questo approccio comporta l’utilizzo dell’oggetto XDM completamente definito come struttura per il livello dati. Quindi mappi l’intero livello dati a un elemento dati di oggetti XDM in Adobe Tags. Se l’implementazione non utilizza un gestore di tag, questo approccio può essere ideale perché puoi inviare dati a XDM direttamente dall’applicazione utilizzando [XDM sendEvent, comando](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#sending-xdm-data). Se utilizzi i tag Adobe, puoi creare un elemento dati con codice personalizzato che acquisisce l’intero livello dati come oggetto JSON pass-through per XDM. Quindi, mappi il JSON pass-through al campo dell’oggetto XDM nell’azione Invia evento.

Di seguito è riportato un esempio dell’aspetto del livello dati utilizzando il formato Livello dati client di Adobe:

Esempio di +++XDM in Data Layer

```JSON
window.adobeDataLayer.push({
"eventType": "web.webPageDetails.pageViews",
"web":{
         "webInteraction":{
            "linkClicks":{
               "id":"",
               "value":""
            },
            "URL":"",
            "name":"",
            "region":"",
            "type":""
         },
         "webPageDetails":{
            "pageViews":{
               "id":"",
               "value":"1"
            },
            "URL":"https://luma.enablementadobe.com/",
            "isErrorPage":"",
            "isHomePage":"",
            "name":"luma:home",
            "server":"enablementadobe.com",
            "siteSection":"home",
            "viewName":""
         },
         "webReferrer":{
            "URL":"",
            "type":""
         }
      }
});
```

+++

Pro

* Ignora i passaggi per mappare singole variabili del livello dati su XDM
* Può essere più rapido da implementare se il team di sviluppo è responsabile del comportamento digitale dei tag

Contro

* Completa dipendenza dal team di sviluppo e dal ciclo di sviluppo per aggiornare i dati da inviare a XDM
* Flessibilità limitata, poiché XDM riceve il payload esatto dal livello dati
* Non è possibile utilizzare le funzioni incorporate nei tag, ad esempio scraping, persistenza e funzioni per distribuzioni rapide
* Impossibile utilizzare il livello dati per pixel di terze parti
* Impossibilità di trasformare i dati tra il livello dati e XDM

### Mappa su XDM nello stream di dati

Questo approccio utilizza funzionalità integrate nella configurazione dello stream di dati denominate [Preparazione per la raccolta dati](https://experienceleague.adobe.com/docs/experience-platform/datastreams/data-prep.html) e ignora la mappatura delle variabili del livello dati su XDM nei tag.

Pro

* Flessibile in quanto è possibile mappare singole variabili su XDM
* Possibilità di [calcola nuovi valori](https://experienceleague.adobe.com/docs/experience-platform/data-prep/functions.html?lang=it) o [trasformare tipi di dati](https://experienceleague.adobe.com/docs/experience-platform/data-prep/data-handling.html) da un livello dati prima di passare a XDM
* Utilizzo di un [Interfaccia utente di mappatura](https://experienceleague.adobe.com/docs/experience-platform/datastreams/data-prep.html#create-mapping) per mappare i campi dei dati di origine su XDM con un’interfaccia utente semplice e intuitiva

Contro

* Non è possibile utilizzare le variabili del livello dati come elementi dati per pixel di terze parti lato client, ma può utilizzarle con tag di Adobe per l’inoltro degli eventi
* Impossibile utilizzare la funzionalità di raschiamento della funzionalità tag di Adobe Experience Platform
* La complessità di manutenzione aumenta se si esegue la mappatura del livello dati sia nei tag che nello stream di dati

### Mappare il livello dati nei tag

Questo approccio comporta la mappatura di singole variabili del livello dati O di oggetti del livello dati su elementi dati nei tag e infine su XDM. Si tratta dell’approccio tradizionale all’implementazione tramite un sistema di gestione dei tag.

Pro

* L’approccio più flessibile, in quanto è possibile controllare singole variabili e trasformare i dati prima che arrivino a XDM
* Può utilizzare i trigger di tag Adobe e la funzionalità di scraping per trasmettere dati a XDM
* È in grado di mappare gli elementi dati su pixel di terze parti lato client

Contro

* L&#39;implementazione potrebbe richiedere più tempo

>[!TIP]
>
> Google Data Layer
> 
> Se la tua organizzazione utilizza già Google Analytics e dispone del tradizionale oggetto Google dataLayer sul sito web, puoi utilizzare [Estensione Google Data Layer](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/google-data-layer/overview.html?lang=en) in Tag di Adobe. Questo consente di implementare la tecnologia Adobe più rapidamente senza dover richiedere supporto al team IT. La mappatura del livello dati di Google su XDM segue gli stessi passaggi indicati sopra.

>[!IMPORTANT]
>
>Come indicato in precedenza, gli esempi in questa esercitazione seguono l’approccio Map to XDM in tags.

## Creare elementi dati per acquisire il livello dati

Prima di creare l’oggetto XDM, crea il seguente set di elementi dati per [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} livello dati:

1. Vai a **[!UICONTROL Elementi dati]** e seleziona **[!UICONTROL Aggiungi elemento dati]** (o **[!UICONTROL Creare un nuovo elemento dati]** se nella proprietà tag non sono presenti elementi dati)

   ![Crea elemento dati](assets/data-element-create.jpg)

1. Denomina l’elemento dati `page.pageInfo.pageName`
1. Utilizza il **[!UICONTROL Variabile JavaScript]** **[!UICONTROL Tipo di elemento dati]** per puntare a un valore nel livello dati di Luma: `digitalData.page.pageInfo.pageName`

1. Seleziona le caselle per **[!UICONTROL Forza valore minuscolo]** e **[!UICONTROL Pulisci testo]** per standardizzare l&#39;uso di maiuscole/minuscole e rimuovere spazi estranei

1. Esci `None` come **[!UICONTROL Durata archiviazione]** poiché questo valore è diverso su ogni pagina

1. Seleziona **[!UICONTROL Salva]**

   ![Elemento dati Nome pagina](assets/data-element-pageName.jpg)

Crea questi quattro elementi dati aggiuntivi seguendo gli stessi passaggi:

* **`page.pageInfo.server`**  mappato a
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  mappato a
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  mappato a
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** mappato a
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`cart.orderId`** mappato a `digitalData.cart.orderId` (viene utilizzato durante il [Configurazione analisi](setup-analytics.md) lezione)


>[!CAUTION]
>
>Il [!UICONTROL Variabile JavaScript] il tipo di elemento dati tratta i riferimenti di array come punti invece che come parentesi, facendo riferimento all’elemento dati username come `digitalData.user[0].profile[0].attributes.username` **non funzionerà**.

## Creare un elemento dati variabile

Dopo aver creato gli elementi dati, mapparli su XDM utilizzando **[!UICONTROL Variabile]** elemento dati che definisce lo schema utilizzato per l’oggetto XDM. Questo oggetto deve essere conforme allo schema XDM creato durante la [Configurare uno schema](configure-schemas.md) lezione.

Per creare l&#39;elemento dati Variable:

1. Seleziona **[!UICONTROL Aggiungi elemento dati]**
1. Denomina l’elemento dati `xdm.variable.content`. È consigliabile usare il prefisso &quot;xdm&quot; per gli elementi dati specifici di XDM per organizzare meglio la proprietà tag
1. Seleziona la **[!UICONTROL Adobe Experience Platform Web SDK]** come **[!UICONTROL Estensione]**
1. Seleziona la **[!UICONTROL Variabile]** come **[!UICONTROL Tipo di elemento dati]**
1. Seleziona l’Experience Platform appropriato **[!UICONTROL Sandbox]**
1. Seleziona la scheda appropriata **[!UICONTROL Schema]**, in questo caso `Luma Web Event Data`
1. Seleziona **[!UICONTROL Salva]**

   ![Elemento dati variabile](assets/analytics-tags-data-element-xdm-variable.png)

<!-- There are different ways to map data elements to XDM object fields. You can map individual data elements to individual XDM fields or map data elements to entire XDM objects as long as your data element matches the exact key-value pair schema present in the XDM object. In this lesson, you will capture content data by mapping to individual fields. You will learn how to [map a data element to an entire XDM object](setup-analytics.md#Map-an-entire-array-to-an-XDM-Object) in the [Setup Analytics](setup-analytics.md) lesson. 

Create an XDM object to capture content data:

1. In the left navigation, select **[!UICONTROL Data Elements]**
1. Select **[!UICONTROL Add Data Element]**
1. **[!UICONTROL Name]** the data element **`xdm.content`**
1. As the **[!UICONTROL Extension]** select `Adobe Experience Platform Web SDK`
1. As the **[!UICONTROL Data Element Type]** select `XDM object`
1. Select the Platform **[!UICONTROL Sandbox]** in which you created the XDM schema in during the [Configure an XDM Schema](configure-schemas.md) lesson, in this example `DEVELOPMENT Mobile and Web SDK Courses`
1. As the **[!UICONTROL Schema]**, select your `Luma Web Event Data` schema:

    ![XDM object](assets/data-element-xdm.content-fields.png)

    >[!NOTE]
    >
    >The sandbox corresponds to the Experience Platform sandbox in which you created the schema. There can be multiple sandboxes available in your Experience Platform instance, so make sure to select the right one. Always work in development first, then production.

1. Scroll down until you reach the **`web`** object
1. Select to open it

    ![Web Object](assets/data-element-pageviews-xdm-object.png)


1. Map the following web XDM variables to data elements

    * **`web.webPageDetials.name`** to `%page.pageInfo.pageName%`
    * **`web.webPageDetials.server`** to `%page.pageInfo.server%`
    * **`web.webPageDetials.siteSection`** to `%page.pageInfo.hierarchie1%`

    ![XDM object](assets/data-element-xdm.content.png)

1. Next, find the `identityMap` object in the schema and select it
 
1. Map to the `identityMap.loginID` data element

1. Select **[!UICONTROL Save]**

   ![Data Collection interface](assets/identity-dataElements-xdmContent-LumaSchema-identityMapSelect3.png)

-->

Al termine di questi passaggi, dovresti aver creato i seguenti elementi di dati:

| Elementi dati dell&#39;estensione CORE | Elementi dati di Platform Web SDK |
-----------------------------|-------------------------------
| `cart.orderId` | `xdm.variable.content` |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |


>[!TIP]
>
>In un futuro [Creare una regola di tag](create-tag-rule.md) lezione, si impara come **[!UICONTROL Variabile]** elemento dati consente di sovrapporre più regole nei tag utilizzando **[!UICONTROL Aggiorna tipo di azione variabile]**. Quindi, puoi inviare in modo indipendente l’oggetto XDM a Adobe Experience Platform Edge Network utilizzando un **[!UICONTROL Invia tipo di azione evento]**.

Una volta impostati questi elementi dati, puoi iniziare a inviare dati a Platform Edge Network con una regola di tag. Ma prima, scopri come raccogliere le identità con Web SDK.

[Successivo: ](create-identities.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
