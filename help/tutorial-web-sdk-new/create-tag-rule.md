---
title: Creare regole di tag
description: Scopri come inviare un evento all’Edge Network di Platform con l’oggetto XDM utilizzando una regola di tag. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
feature: Tags
exl-id: c77ab8a1-922b-481e-b3cb-d2c5ca7bb8cb
source-git-commit: fe8b92c560c9676a44935005cc558388244d6aea
workflow-type: tm+mt
source-wordcount: '2025'
ht-degree: 1%

---

# Creare regole di tag

Scopri come inviare eventi all’Edge Network Platform con l’oggetto XDM utilizzando le regole di tag. Una regola di tag è una combinazione di eventi, condizioni e azioni che indica alla proprietà tag di eseguire un&#39;operazione. Con Platform Web SDK, le regole vengono utilizzate per inviare eventi all’Edge Network di Platform con i campi XDM corretti.

>[!NOTE]
>
> A scopo dimostrativo, gli esercizi di questa lezione si basano sulle lezioni precedenti per inviare eventi dagli utenti su [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}.


## Obiettivi di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Utilizza una convenzione di denominazione per gestire le regole all’interno dei tag
* Inviare un evento con campi XDM utilizzando le azioni Aggiorna variabile e Invia evento
* Sovrapponi più set di campi XDM in più regole
* Mappare singoli o interi elementi di dati array all’oggetto XDM
* Pubblicare una regola di tag in una libreria di sviluppo


## Prerequisiti

Conosci i tag di raccolta dati e la [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html) e hanno completato le lezioni precedenti nell’esercitazione:

* [Configurare uno schema XDM](configure-schemas.md)
* [Configurare uno spazio dei nomi delle identità](configure-identities.md)
* [Configurare uno stream di dati](configure-datastream.md)
* [Installare l’estensione Web SDK](install-web-sdk.md)
* [Creare elementi dati](create-data-elements.md)
* [Creare identità](create-identities.md)

## Convenzioni di denominazione

Per gestire meglio le regole nei tag, si consiglia di seguire una convenzione di denominazione standard. Questa esercitazione utilizza una convenzione di denominazione in cinque parti:

* [**posizione**] - [**evento**] - [**scopo**] - [**strumento**] - [**ordine**]

dove;

1. **posizione** è la pagina o le pagine del sito in cui viene attivata la regola
1. **evento** è il trigger della regola
1. **scopo** è l’azione principale eseguita dalla regola
1. **strumento** è l’applicazione o le applicazioni specifiche utilizzate nel passaggio di azione per tale regola, che dovrebbe essere rara con Web SDK
1. **sequenza** è l&#39;ordine in cui la regola deve essere attivata in relazione ad altre regole
<!-- minor update -->

## Creare regole di tag

Nei tag, le regole vengono utilizzate per eseguire azioni (chiamate di attivazione) in varie condizioni. L’estensione dei tag di Platform Web SDK include due azioni che verranno utilizzate in questa lezione:

* **[!UICONTROL Aggiorna variabile]** mappa gli elementi dati sui campi XDM
* **[!UICONTROL Invia evento]** invia l&#39;oggetto XDM ad Experienci Platform Edge Network

Nel resto di questa lezione:

1. Crea una regola per definire una &quot;configurazione globale&quot; di campi XDM (utilizzando [!UICONTROL Aggiorna variabile] che vogliamo inviare su ogni pagina del sito web (ad esempio, il nome della pagina) utilizzando **[!UICONTROL Aggiorna variabile]** azione.

1. Crea regole aggiuntive che sovrascrivono la &quot;configurazione globale&quot; di o contribuiscono ad altri campi XDM (utilizzando [!UICONTROL Aggiorna variabile] ) che sono pertinenti solo in determinate condizioni (ad esempio, l’aggiunta di dettagli di prodotto nelle pagine dei prodotti).

1. Crea un&#39;altra regola con **[!UICONTROL Invia evento]** azione che invia l’oggetto XDM completo all’Edge Network di Adobe Experience Platform.

Tutte queste regole saranno sequenziate correttamente utilizzando il comando &quot;[!UICONTROL ordine]&quot;.

Questo video offre una panoramica del processo:

>[!VIDEO](https://video.tv.adobe.com/v/3427710/?learn=on)

### Aggiorna regole variabili

#### Configurazione globale

Per creare regole di tag per i campi XDM globali:

1. Apri la proprietà tag utilizzata per questa esercitazione

1. Vai a **[!UICONTROL Regole]** nel menu di navigazione a sinistra

1. Seleziona la **[!UICONTROL Crea nuova regola]** pulsante

   ![Creare una regola](assets/rules-create.png)

1. Denomina la regola `all pages - library loaded - set global variables - 1`

1. In **[!UICONTROL Eventi]** sezione, seleziona **[!UICONTROL Aggiungi]**

   ![Denomina la regola e aggiungi un evento](assets/rule-name-new.png)

1. Utilizza il **[!UICONTROL Estensione core]** e seleziona **[!UICONTROL Library Loaded (Page Top)]** come **[!UICONTROL Tipo di evento]**

1. Seleziona **[!UICONTROL Avanzate]** a discesa e immettere `1` come **[!UICONTROL Ordine]**

   >[!NOTE]
   >
   > Minore è il numero d&#39;ordine, prima viene eseguito. Pertanto, alla nostra &quot;configurazione globale&quot; viene assegnato un numero d&#39;ordine basso.

1. Seleziona **[!UICONTROL Mantieni modifiche]** per tornare alla schermata principale delle regole
   ![Seleziona attivatore caricato dalla libreria](assets/create-tag-rule-trigger-loaded.png)

1. In **[!UICONTROL Azioni]** sezione, seleziona **[!UICONTROL Aggiungi]**

1. Come **[!UICONTROL Estensione]**, seleziona **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Come **[!UICONTROL Tipo di azione]**, seleziona **[!UICONTROL Aggiorna variabile]**

1. Come **[!UICONTROL Elemento dati]**, seleziona la `xdm.variable.content` creato in [Creare elementi dati](create-data-elements.md) lezione

   ![Aggiorna schema variabile](assets/create-rule-update-variable.png)

Ora mappa il tuo [!UICONTROL elementi dati] al [!UICONTROL schema] utilizzato dall’oggetto XDM.

>[!NOTE]
> 
> È possibile eseguire il mapping a singole proprietà o a interi oggetti. In questo esempio, esegui il mapping a singole proprietà.

1. Individuare il campo eventType e selezionarlo

1. Inserisci il valore `web.webpagedetails.pageViews`

   >[!TIP]
   >
   > Per capire quali valori compilare nel `eventType` , è necessario passare alla pagina schema e selezionare `eventType` per visualizzare i valori suggeriti nella barra a destra. Se necessario, puoi anche immettere un nuovo valore.
   > ![valori suggeriti da eventType nella pagina schemi](assets/create-tag-rule-eventType.png)

1. Quindi, trova il `identityMap` nello schema e selezionarlo

1. Mappa su `identityMap.loginID` elemento dati

   ![Aggiorna mappa identità variabile](assets/create-rule-variable-identityMap.png)


   >[!TIP]
   >
   > I campi XDM non verranno inclusi nella richiesta di rete se l’elemento dati è nullo. Pertanto, quando l’utente non è autenticato e il `identityMap.loginID` l&#39;elemento dati è nullo, l&#39; `identityMap` l&#39;oggetto non verrà inviato. Per questo possiamo definirla nella nostra &quot;configurazione globale&quot;.

1. Scorri verso il basso fino a raggiungere il **`web`** oggetto

1. Seleziona per aprirlo

1. Mappa i seguenti elementi dati al corrispondente `web` Variabili XDM

   * **`web.webPageDetials.name`** a `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** a `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** a `%page.pageInfo.hierarchie1%`

1. Imposta `web.webPageDetials.pageViews.value` su `1`.

   ![Aggiorna contenuto variabile](assets/create-rule-xdm-variable-content.png)

   >[!TIP]
   >
   > Mentre nessuno dei due `eventType` imposta su `web.webpagedetails.pageViews` né `web.webPageDetials.pageViews.value` sono necessari affinché Adobe Analytics possa elaborare un beacon come visualizzazione di pagina; è utile disporre di una modalità standard per indicare una visualizzazione di pagina per altre applicazioni a valle.


1. Seleziona **[!UICONTROL Mantieni modifiche]** e poi **[!UICONTROL Salva]** la regola nella schermata successiva per completare la creazione della regola


#### Campi pagina prodotto

Ora, inizia a utilizzare **[!UICONTROL Aggiorna variabile]** in regole aggiuntive in sequenza per arricchire l’oggetto XDM prima di inviarlo a [!UICONTROL Edge Network piattaforma].

>[!TIP]
>
>L&#39;ordine delle regole determina quale regola viene eseguita per prima quando viene attivato un evento. Se due regole hanno lo stesso tipo di evento, viene eseguito per primo quello con il numero più basso.
> 
>![ordine delle regole](assets/set-up-analytics-sequencing.png)

Per iniziare, monitora le visualizzazioni del prodotto nella pagina dei dettagli del prodotto di Luma:

1. Seleziona **[!UICONTROL Aggiungi regola]**
1. Assegna un nome  [!UICONTROL `ecommerce - library loaded - set product details variables - 20`]
1. Seleziona la ![simbolo +](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) in Evento per aggiungere un nuovo trigger
1. Sotto **[!UICONTROL Estensione]**, seleziona **[!UICONTROL Core]**
1. Sotto **[!UICONTROL Tipo di evento]**, seleziona **[!UICONTROL Library Loaded (Page Top)]**
1. Seleziona per aprire **[!UICONTROL Opzioni avanzate]**, digitare `20`. In questo modo la regola viene eseguita dopo il `all pages - library loaded - set global variables - 1` che imposta la configurazione globale.

   ![Regole XDM per Analytics](assets/set-up-analytics-pdp.png)

1. Sotto **[!UICONTROL Condizioni]**, seleziona per **[!UICONTROL Aggiungi]**
1. Esci **[!UICONTROL Tipo di logica]** as **[!UICONTROL Normale]**
1. Esci **[!UICONTROL Estensione]** as **[!UICONTROL Core]**
1. Seleziona **[!UICONTROL Tipo di condizione]** as **[!UICONTROL Percorso senza stringa di query]**
1. A destra, abilita **[!UICONTROL Regex]** attivare/disattivare
1. Sotto **[!UICONTROL path è uguale a]** set `/products/`. Per il sito di dimostrazione Luma, assicura che la regola venga attivata solo sulle pagine dei prodotti
1. Seleziona **[!UICONTROL Mantieni modifiche]**

   ![Regole XDM per Analytics](assets/set-up-analytics-product-condition.png)

1. Sotto **[!UICONTROL Azioni]** seleziona **[!UICONTROL Aggiungi]**
1. Seleziona **[!UICONTROL Adobe Experience Platform Web SDK]** estensione
1. Seleziona **[!UICONTROL Tipo di azione]** as **[!UICONTROL Aggiorna variabile]**
1. Scorri verso il basso fino a `commerce` oggetto
1. Apri **[!UICONTROL productViews]** oggetto e set **[!UICONTROL valore]** a `1`

   ![configurare la visualizzazione prodotto](assets/set-up-analytics-prodView.png)

   >[!TIP]
   >
   >L’impostazione di commerce.productViews.value=1 in XDM viene mappata automaticamente sul `prodView` evento in Analytics

1. Scorri verso il basso fino a `eventType` e impostarlo su `commerce.productViews`

   >[!NOTE]
   >
   >Poiché questa regola ha un ordine più alto, sovrascriverà il `eventType` impostato nella regola &quot;configurazione globale&quot;. `eventType` può contenere un solo valore e si consiglia di impostarlo con l’evento di valore più alto.

1. Scorri verso il basso fino a e seleziona `productListItems` array
1. Seleziona **[!UICONTROL Fornisci singoli elementi]**
1. Seleziona **[!UICONTROL Aggiungi elemento]**

   ![Impostazione dell’evento di visualizzazione prodotto](assets/set-up-analytics-xdm-individual.png)

   >[!CAUTION]
   >
   >Il **`productListItems`** è un `array` tipo di dati in modo che preveda che i dati vengano inseriti come una raccolta di elementi. A causa della struttura del livello dati del sito di dimostrazione Luma e poiché è possibile visualizzare un solo prodotto alla volta sul sito Luma, puoi aggiungere elementi singolarmente. Quando implementi sul tuo sito web, a seconda della struttura del livello dati, potresti essere in grado di fornire un intero array.

1. Seleziona per aprire **[!UICONTROL Elemento 1]**
1. Mappa **`productListItems.item1.SKU`** a `%product.productInfo.sku%`

   ![Variabile oggetto XDM SKU del prodotto](assets/set-up-analytics-sku.png)

1. Seleziona **[!UICONTROL Mantieni modifiche]**

1. Seleziona **[!UICONTROL Salva]** per salvare la regola


#### Campi carrello

Puoi mappare l’intero array a un oggetto XDM, purché l’array corrisponda al formato dello schema XDM. Elemento dati del codice personalizzato `cart.productInfo` sono stati creati cicli precedenti in `digitalData.cart.cartEntries` oggetto livello dati su Luma e lo traduce nel formato richiesto del `productListItems` oggetto dello schema XDM.

Per illustrare, consulta il confronto seguente del livello dati del sito Luma (a sinistra) con l’elemento dati tradotto (a destra):

![Formato array di oggetti XDM](assets/data-element-xdm-array.png)

Confronta l’elemento dati con `productListItems` struttura (suggerimento, deve corrispondere).

>[!IMPORTANT]
>
>Nota come le variabili numeriche vengono tradotte, con valori stringa nel livello dati come `price` e `qty` viene riformattato in numeri nell’elemento dati. Questi requisiti di formato sono importanti per l’integrità dei dati in Platform e vengono determinati durante [configurare gli schemi](configure-schemas.md) passaggio. Nell’esempio, **[!UICONTROL quantità]** utilizza **[!UICONTROL Intero]** tipo di dati.
> ![Tipo di dati dello schema XDM](assets/set-up-analytics-quantity-integer.png)

Ora associamo il nostro array all’oggetto XDM:


1. Crea una nuova regola denominata `ecommerce - library loaded - set shopping cart variables - 20`
1. Seleziona la ![simbolo +](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) in Evento per aggiungere un nuovo trigger
1. Sotto **[!UICONTROL Estensione]**, seleziona **[!UICONTROL Core]**
1. Sotto **[!UICONTROL Tipo di evento]**, seleziona **[!UICONTROL Library Loaded (Page Top)]**
1. Seleziona per aprire **[!UICONTROL Opzioni avanzate]**, digitare `20`
1. Seleziona **[!UICONTROL Mantieni modifiche]**

   ![Regole XDM per Analytics](assets/set-up-analytics-cart-sequence.png)

1. Sotto **[!UICONTROL Condizioni]**, seleziona per **[!UICONTROL Aggiungi]**
1. Esci **[!UICONTROL Tipo di logica]** as **[!UICONTROL Normale]**
1. Esci **[!UICONTROL Estensioni]** as **[!UICONTROL Core]**
1. Seleziona **[!UICONTROL Tipo di condizione]** as **[!UICONTROL Percorso senza stringa di query]**
1. Sulla destra, **non** abilita **[!UICONTROL Regex]** attivare/disattivare
1. Sotto **[!UICONTROL path è uguale a]** set `/content/luma/us/en/user/cart.html`. Per il sito di dimostrazione Luma, assicura che la regola venga attivata solo sulla pagina del carrello
1. Seleziona **[!UICONTROL Mantieni modifiche]**

   ![Regole XDM per Analytics](assets/set-up-analytics-cart-condition.png)

1. Sotto **[!UICONTROL Azioni]** seleziona **[!UICONTROL Aggiungi]**
1. Seleziona **[!UICONTROL Adobe Experience Platform Web SDK]** estensione
1. Seleziona **[!UICONTROL Tipo di azione]** as **[!UICONTROL Aggiorna variabile]**
1. Scorri verso il basso fino a `commerce` e selezionare per aprirlo.
1. Apri **[!UICONTROL productListViews]** oggetto e set **[!UICONTROL valore]** a `1`

   ![configurare la visualizzazione prodotto](assets/set-up-analytics-cart-view.png)

   >[!TIP]
   >
   >L’impostazione di commerce.productListViews.value=1 in XDM viene mappata automaticamente sul `scView` evento in Analytics

1. Seleziona `eventType` e impostato su `commerce.productListViews`

1. Scorri verso il basso fino a e seleziona **[!UICONTROL productListItems]** array

1. Seleziona **[!UICONTROL Fornire l&#39;intero array]**

1. Mappa a **`cart.productInfo`** elemento dati

1. Seleziona **[!UICONTROL Mantieni modifiche]**

1. Seleziona **[!UICONTROL Salva]** per salvare la regola

Crea altre due regole per il pagamento e l’acquisto seguendo lo stesso pattern con le seguenti differenze:

**Nome regola**: `ecommerce  - library loaded - set checkout variables - 20`

1. **[!UICONTROL Condizione]**: /content/luma/us/en/user/checkout.html
1. Imposta `eventType` su `commerce.checkouts`.
1. Imposta `commerce.checkout.value` su `1`.

   >[!TIP]
   >
   >Equivale all&#39;impostazione `scCheckout` evento in Analytics


**Nome regola**: `ecommerce - library loaded - set purchase variables -  20`

1. **[!UICONTROL Condizione]**: /content/luma/us/en/user/checkout/order/thank-you.html
1. Imposta `eventType` su `commerce.purchases`.
1. Imposta `commerce.purchases.value` su `1`.

   >[!TIP]
   >
   >Equivale all&#39;impostazione `purchase` evento in Analytics

1. Imposta `commerce.order.purchaseID` al `cart.orderId` elemento dati
1. Imposta `commerce.order.currencyCode` al valore hardcoded `USD`

   ![Impostazione purchaseID per Analytics](assets/set-up-analytics-purchase.png)

   >[!TIP]
   >
   >Equivale all&#39;impostazione `s.purchaseID` e `s.currencyCode` variabili in Analytics

1. Scorri verso il basso fino a e seleziona **[!UICONTROL productListItems]** array
1. Seleziona **[!UICONTROL Fornire l&#39;intero array]**
1. Mappa a **`cart.productInfo.purchase`** elemento dati
1. Seleziona **[!UICONTROL Salva]**

Al termine dell’operazione, dovresti vedere che sono state create le seguenti regole.

![Regole XDM per Analytics](assets/set-up-analytics-rules.png)


### Invia regola evento

Dopo aver impostato le variabili, puoi creare la regola per inviare l’oggetto XDM completo all’Edge Network di Platform con **[!UICONTROL Invia evento]** azione.

1. A destra, seleziona **[!UICONTROL Aggiungi regola]** per creare un&#39;altra regola

1. Denomina la regola `all pages - library loaded - set send event - 50`

1. In **[!UICONTROL Eventi]** sezione, seleziona **[!UICONTROL Aggiungi]**

1. Utilizza il **[!UICONTROL Estensione core]** e seleziona `Library Loaded (Page Top)` come **[!UICONTROL Tipo di evento]**

1. Seleziona **[!UICONTROL Avanzate]** a discesa e immettere `50` in **[!UICONTROL Ordine]**. In questo modo la seconda regola verrà attivata dopo la prima regola impostata per l’attivazione come `1`.

1. Seleziona **[!UICONTROL Mantieni modifiche]** per tornare alla schermata principale delle regole
   ![Seleziona attivatore caricato dalla libreria](assets/create-tag-rule-trigger-loaded-send.png)

1. In **[!UICONTROL Azioni]** sezione, seleziona **[!UICONTROL Aggiungi]**

1. Come **[!UICONTROL Estensione]**, seleziona  **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Come  **[!UICONTROL Tipo di azione]**, seleziona  **[!UICONTROL Invia evento]**

1. Come **[!UICONTROL XDM]**, seleziona la `xdm.variable.content` elemento dati creato nella lezione precedente

1. Seleziona **[!UICONTROL Mantieni modifiche]** per tornare alla schermata principale delle regole

   ![Aggiungere l’azione Invia evento](assets/create-rule-send-event-action.png)
1. Seleziona **[!UICONTROL Salva]** per salvare la regola

   ![Salva la regola](assets/create-rule-save-rule.png)

## Pubblicare la regola in una libreria

Successivamente, pubblica la regola nell&#39;ambiente di sviluppo in modo da poterne verificare il funzionamento.

Per creare una libreria:

1. Vai a **[!UICONTROL Flusso di pubblicazione]** nel menu di navigazione a sinistra

1. Seleziona **[!UICONTROL Aggiungi libreria]**

   ![Seleziona Aggiungi libreria](assets/rule-publish-library.png)
1. Per **[!UICONTROL Nome]**, immetti `Luma Web SDK Tutorial`
1. Per **[!UICONTROL Ambiente]**, seleziona `Development`
1. Seleziona  **[!UICONTROL Aggiungi tutte le risorse modificate]**

   >[!NOTE]
   >
   >    Dovresti visualizzare tutti i componenti tag creati nelle lezioni precedenti. L’estensione Core contiene il JavaScript di base richiesto da tutte le proprietà dei tag web.

1. Seleziona **[!UICONTROL Salva e genera per sviluppo]**

   ![Creare e generare la libreria](assets/create-tag-rule-library-changes.png)

La creazione della libreria potrebbe richiedere alcuni minuti e al termine viene visualizzato un punto verde a sinistra del nome della libreria:

![Compilazione completata](assets/create-rule-development-success.png)

Come è possibile vedere sul [!UICONTROL Flusso di pubblicazione] , il processo di pubblicazione richiede molto di più, il che va oltre l’ambito di questa esercitazione. Questo tutorial utilizza una sola libreria nell’ambiente di sviluppo.

Ora puoi convalidare i dati nella richiesta utilizzando l’Adobe Experience Platform Debugger.

[Successivo ](validate-with-debugger.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
