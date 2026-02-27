---
title: Creare regole di tag per Platform Web SDK
description: Scopri come inviare un evento a Platform Edge Network con l’oggetto XDM utilizzando una regola di tag. Questa lezione fa parte del tutorial Implementare Adobe Experience Cloud con Web SDK.
feature: Tags
jira: KT-15403
exl-id: e06bad06-3ee3-475f-9b10-f0825a48a312
source-git-commit: 9b5e7192094e2d3b8eb41cbb4a0f28411e990e8f
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 2%

---

# Creare regole di tag

Scopri come inviare eventi all’Edge Network di Adobe Experience Platform con l’oggetto XDM utilizzando le regole di tag. Una regola di tag è una combinazione di eventi, condizioni e azioni che indica alla proprietà tag di eseguire un&#39;operazione. Con Platform Web SDK, le regole vengono utilizzate per inviare eventi a Platform Edge Network con i dati corretti.



## Obiettivi di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Utilizza una convenzione di denominazione per gestire le regole all’interno dei tag
* Inviare un evento con campi XDM utilizzando le azioni Aggiorna variabile e Invia evento
* Sovrapponi più set di campi XDM in più regole
* Mappare singoli o interi elementi di dati array all’oggetto XDM
* Pubblicare una regola di tag in una libreria di sviluppo


## Prerequisiti

Conosci i tag di raccolta dati e il [sito di dimostrazione Luma](https://newluma.enablementadobe.com) e hai completato le lezioni precedenti nell’esercitazione:

* [Configurare uno schema XDM](configure-schemas.md)
* [Configurare uno spazio dei nomi delle identità](configure-identities.md)
* [Configurare uno stream di dati](configure-datastream.md)
* [Installare l’estensione Web SDK](install-web-sdk.md)
* [Creare elementi dati](create-data-elements.md)
* [Creare identità](create-identities.md)

## Convenzioni di denominazione

Per gestire le regole nei tag, si consiglia di seguire una convenzione di denominazione standard. Questa esercitazione utilizza una convenzione di denominazione in cinque parti:

* [**posizione**] - [**evento**] - [**scopo**] - [**ordine**]

dove;

1. **posizione** è la pagina o le pagine del sito in cui viene attivata la regola
1. **event** è il trigger per la regola
1. **scopo** è l&#39;azione principale eseguita dalla regola
1. **order** è l&#39;ordine in cui attivare la regola in relazione ad altre regole
<!-- minor update -->

## Aggiungere l’estensione Adobe Client Data Layer

Il sito web Luma utilizza un livello dati basato su eventi denominato Adobe Client Data Layer (ACDL). Ogni volta che si verifica un evento, questo viene inviato all&#39;array `adobeDataLayer`. Utilizzeremo questi eventi per costruire le nostre regole, anche se molte opzioni predefinite.

1. Vai a **[!UICONTROL Estensioni]**
1. Filtra per **[!UICONTROL Adobe Client Data Layer]**
1. Seleziona **[!UICONTROL Installa]**

   ![Aggiungi estensione Adobe Client Data Layer](assets/rules-acdl-extension.png)

1. Lascia le impostazioni predefinite
1. Seleziona **[!UICONTROL Salva]**

## Creare regole di tag

Nei tag, le regole vengono utilizzate per eseguire azioni (chiamate di attivazione) in varie condizioni. L’estensione dei tag di Platform Web SDK include due azioni utilizzate nelle regole:

* **[!UICONTROL Aggiorna variabile]** associa gli elementi dati alle variabili di dati o XDM
* **[!UICONTROL Invia evento]** invia i dati ad Experience Platform Edge Network

Nel resto di questa lezione:

1. Utilizza l&#39;azione **[!UICONTROL Aggiorna variabile]** per definire una &quot;configurazione globale&quot; dei campi XDM.

1. Utilizza l&#39;azione **[!UICONTROL Aggiorna variabile]** che sostituisce la &quot;configurazione globale&quot; e contribuisce con campi XDM aggiuntivi in determinate condizioni (ad esempio, l&#39;aggiunta di dettagli prodotto nelle pagine dei prodotti).

1. Utilizza l&#39;azione **[!UICONTROL Invia evento]** per inviare tutti i dati desiderati a Adobe Experience Platform Edge Network.

Tutte queste regole verranno sequenziate correttamente utilizzando l&#39;opzione &quot;[!UICONTROL order]&quot;.

Questo video offre una panoramica del processo:

>[!VIDEO](https://video.tv.adobe.com/v/3454035/?captions=ita&learn=on&enablevpops)

### Campi di configurazione globali

Per creare una regola di tag per i campi XDM globali:

1. Apri la proprietà tag utilizzata per questa esercitazione

1. Vai a **[!UICONTROL Regole]** nel menu di navigazione a sinistra

1. Seleziona il pulsante **[!UICONTROL Crea nuova regola]**

   ![Crea una regola](assets/rules-create.png)

1. Denomina la regola `all pages - adobeDataLayer push - set global variables - 1`

1. Nella sezione **[!UICONTROL Eventi]**, seleziona **[!UICONTROL Aggiungi]**

   ![Denomina la regola e aggiungi un evento](assets/rule-name-new.png)

1. Utilizza l&#39;estensione **[!UICONTROL Adobe Client Data Layer]** e seleziona **[!UICONTROL Dati inviati]** come **[!UICONTROL Tipo evento]**

1. Seleziona il menu a discesa **[!UICONTROL Avanzate]** e immetti `1` come **[!UICONTROL Ordine]**

   >[!NOTE]
   >
   > Minore è il numero d&#39;ordine, prima viene eseguito. Pertanto, alla nostra &quot;configurazione globale&quot; viene assegnato un numero d&#39;ordine basso.

1. Ascolta **[!UICONTROL Tutti gli eventi]**
1. Seleziona **[!UICONTROL Mantieni modifiche]** per tornare alla schermata della regola principale
   ![Seleziona trigger caricato dalla libreria](assets/create-tag-rule-trigger-loaded.png)

1. Nella sezione **[!UICONTROL Azioni]**, seleziona **[!UICONTROL Aggiungi]**

1. Come **[!UICONTROL Estensione]**, seleziona **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Come **[!UICONTROL Tipo azione]**, seleziona **[!UICONTROL Aggiorna variabile]**

1. Come **[!UICONTROL elemento dati]**, seleziona `xdm.variable.content` creato nella lezione [Creare elementi dati](create-data-elements.md)

   ![Aggiorna schema variabile](assets/create-rule-update-variable.png)

1. Ora, specifica i campi XDM mappandoli ai valori appropriati:

   | Campo XDM | Mappa a |
   |---|---|
   | `eventType` | `Web Webpagedetails Page Views` (iniziare a digitare per visualizzare i valori suggeriti) |
   | `identityMap` | `Identity Map` elemento dati |
   | `web.webPageDetails.name` | `Page Name` elemento dati |
   | `web.webPageDetails.pageViews.value` | `1` |


   >[!TIP]
   >
   > I campi XDM non verranno inclusi nella richiesta di rete se l’elemento dati è nullo. Pertanto, quando l&#39;utente non è autenticato e l&#39;elemento dati `Identity Map` è null, l&#39;oggetto `identityMap` non verrà inviato. Per questo possiamo definirla nella nostra &quot;configurazione globale&quot;.

   >[!TIP]
   >
   > Sebbene non sia necessario `eventType` impostato su `web.webpagedetails.pageViews` né `web.webPageDetails.pageViews.value` per consentire ad Adobe Analytics di elaborare un beacon come visualizzazione di pagina, è utile disporre di un modo standard per indicare una visualizzazione di pagina per altre applicazioni a valle.

1. Al termine, `XDM Variable` avrà un aspetto simile a questo. I campi compilati e parzialmente compilati sono indicati con i cerchi blu:
   ![Variabile XDM](assets/rule-xdm-variable.png)
1. Seleziona **[!UICONTROL Mantieni modifiche]**, quindi **[!UICONTROL Salva]** la regola nella schermata successiva per completare la regola



### Campi pagina prodotto

Ora, inizia a utilizzare **[!UICONTROL Aggiorna variabile]** in regole aggiuntive in sequenza per arricchire l&#39;oggetto XDM prima di inviarlo a [!UICONTROL Platform Edge Network].

>[!TIP]
>
>L&#39;ordine delle regole determina quale regola viene eseguita per prima quando viene attivato un evento. Se due regole hanno lo stesso tipo di evento, viene eseguito per primo quello con il numero più basso.
> 

Per iniziare, monitora le visualizzazioni del prodotto nella pagina dei dettagli del prodotto di Luma:

1. Seleziona **[!UICONTROL Aggiungi regola]**
1. Denomina [!UICONTROL `product detail pages - adobeDataLayer push - set product details variables - 20`]
1. Seleziona il simbolo ![+](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) in Evento per aggiungere un nuovo trigger
1. In **[!UICONTROL Estensione]**, seleziona **[!UICONTROL Adobe Client Data Layer]**
1. In **[!UICONTROL Tipo evento]**, seleziona **[!UICONTROL Dati inviati]**
1. Seleziona per aprire **[!UICONTROL Opzioni avanzate]**, digita in `20`. Questo valore dell&#39;ordine assicura che la regola venga eseguita _dopo_ la regola delle variabili globali.
1. Ascolta un **[!UICONTROL evento specifico]**
1. Immetti `productView` come **[!UICONTROL Evento / Chiave da registrare per]**
1. Seleziona **[!UICONTROL Mantieni modifiche]**

   ![Regole XDM per Analytics](assets/rule-pdp-event.png)


1. In **[!UICONTROL Azioni]** selezionare **[!UICONTROL Aggiungi]**
1. Seleziona estensione **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Seleziona **[!UICONTROL Tipo azione]** come **[!UICONTROL Aggiorna variabile]**
1. Seleziona `XDM Variable` come **[!UICONTROL elemento dati]**
1. Mappa questi campi XDM sui valori appropriati:

   | Campo XDM | Mappa a |
   |---|---|
   | `eventType` | `Commerce Product Views` (iniziare a digitare per visualizzare i valori suggeriti) |
   | `commerce.productViews.value` | `1` |
   | `productListItems.name` | `Ecommerce Product Name` (Seleziona **[!UICONTROL Fornisci singoli elementi]** e **[!UICONTROL Aggiungi elemento]** prima ) |
   | `productListItems.sku` | `Ecommerce Product Id` |

1. Seleziona **[!UICONTROL Mantieni modifiche]**

1. Seleziona **[!UICONTROL Salva]** per salvare la regola

   >[!NOTE]
   >
   >Poiché questa regola ha un ordine più alto, sovrascriverà `eventType` impostato nella regola di &quot;configurazione globale&quot;. `eventType` può contenere un solo valore e si consiglia di impostarlo con l&#39;evento di maggior valore.

   >[!TIP]
   >
   >L&#39;impostazione di commerce.productViews.value=1 in XDM viene mappata automaticamente all&#39;evento `prodView` in Analytics


### Campi carrello

Puoi mappare l’intero array a un oggetto XDM, purché l’array corrisponda al formato dello schema XDM. L’elemento dati del codice personalizzato `Ecommerce Cart Products` creato in precedenza esegue un ciclo nell’oggetto livello dati `adobeDataLayer.ecommerce.cart.items` sul sito web Luma e lo traduce nel formato richiesto dell’oggetto `productListItems` dello schema XDM.

Per illustrare, consulta il confronto seguente del livello dati del sito Luma (a sinistra) con l’elemento dati tradotto (a destra):

![Formato array di oggetti XDM](assets/data-element-xdm-array.png)

Confrontare l&#39;elemento dati con la struttura `productListItems` (suggerimento, dovrebbe corrispondere).

>[!IMPORTANT]
>
>Si noti come le variabili numeriche vengono convertite, con valori stringa nel livello dati come `price` e `qty` riformattati in numeri nell&#39;elemento dati. Questi requisiti di formato sono importanti per l&#39;integrità dei dati in Platform e vengono determinati durante il passaggio [configura schemi](configure-schemas.md). Nell&#39;esempio, **[!UICONTROL quantity]** utilizza il tipo di dati **[!UICONTROL Integer]**.
> ![Tipo di dati dello schema XDM](assets/set-up-analytics-quantity-integer.png)

Ora associamo il nostro array all’oggetto XDM:


1. Crea una nuova regola denominata `cart page - adobeDataLayer push - set cart variables - 20`
1. Seleziona il simbolo ![+](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) in Evento per aggiungere un nuovo trigger
1. In **[!UICONTROL Estensione]**, seleziona **[!UICONTROL Adobe Client Data Layer]**
1. In **[!UICONTROL Tipo evento]**, seleziona **[!UICONTROL Dati inviati]**
1. Seleziona per aprire **[!UICONTROL Opzioni avanzate]**, digita in `20`. Questo valore dell&#39;ordine assicura che la regola venga eseguita _dopo_ la regola delle variabili globali.
1. Ascolta un **[!UICONTROL evento specifico]**
1. Immetti `cartView` come **[!UICONTROL Evento / Chiave da registrare per]**
1. Seleziona **[!UICONTROL Mantieni modifiche]**


   ![Evento per regola carrello](assets/rule-cart-event.png)

1. In **[!UICONTROL Azioni]** selezionare **[!UICONTROL Aggiungi]**
1. Seleziona estensione **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Seleziona **[!UICONTROL Tipo azione]** come **[!UICONTROL Aggiorna variabile]**
1. Seleziona `XDM Variable` come **[!UICONTROL elemento dati]**
1. Mappa questi campi XDM sui valori appropriati:

   | Campo XDM | Mappa a |
   |---|---|
   | `eventType` | `Commerce Product List (Cart) Views` (iniziare a digitare per visualizzare i valori suggeriti) |
   | `commerce.productListViews.value` | `1` |
   | `productListItems.name` | `Ecommerce Product Name` (Seleziona **[!UICONTROL Fornisci singoli elementi]** e **[!UICONTROL Aggiungi elemento]** prima ) |
   | `productListItems.sku` | `Ecommerce Product Id` |



   >[!TIP]
   >
   >L&#39;impostazione di commerce.productListViews.value=1 in XDM viene mappata automaticamente all&#39;evento `scView` in Analytics

1. Seleziona `eventType` e imposta su `commerce.productListViews`

1. Scorri verso il basso fino a e seleziona l&#39;array **[!UICONTROL productListItems]**

1. Seleziona **[!UICONTROL Fornisci intero array]**

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
   >Equivale a impostare l&#39;evento `scCheckout` in Analytics


**Nome regola**: `ecommerce - library loaded - set purchase variables -  20`

1. **[!UICONTROL Condizione]**: /content/luma/us/en/user/checkout/order/thank-you.html
1. Imposta `eventType` su `commerce.purchases`.
1. Imposta `commerce.purchases.value` su `1`.

   >[!TIP]
   >
   >Equivale a impostare l&#39;evento `purchase` in Analytics

1. Imposta `commerce.order.purchaseID` sull&#39;elemento dati `cart.orderId`
1. Imposta `commerce.order.currencyCode` sul valore hardcoded `USD`

   ![Impostazione purchaseID per Analytics](assets/set-up-analytics-purchase.png)

   >[!TIP]
   >
   >Equivale a impostare le variabili `s.purchaseID` e `s.currencyCode` in Analytics

1. Scorri verso il basso fino a e seleziona l&#39;array **[!UICONTROL productListItems]**
1. Seleziona **[!UICONTROL Fornisci intero array]**
1. Mappa a **`cart.productInfo.purchase`** elemento dati
1. Seleziona **[!UICONTROL Mantieni modifiche]**
1. Seleziona **[!UICONTROL Salva]**

Al termine dell’operazione, dovresti vedere che sono state create le seguenti regole.

![Regole XDM per Analytics](assets/set-up-analytics-rules.png)


### Invia regola evento

Dopo aver impostato le variabili, puoi creare la regola per inviare l&#39;oggetto XDM completo a Platform Edge Network con l&#39;azione **[!UICONTROL Invia evento]**.

1. A destra, seleziona **[!UICONTROL Aggiungi regola]** per creare un&#39;altra regola

1. Denomina la regola `all pages - library loaded - send event - 50`

1. Nella sezione **[!UICONTROL Eventi]**, seleziona **[!UICONTROL Aggiungi]**

1. Utilizza l&#39;estensione **[!UICONTROL Core]** e seleziona `Library Loaded (Page Top)` come **[!UICONTROL Tipo evento]**

1. Seleziona il menu a discesa **[!UICONTROL Avanzate]** e immetti `50` in **[!UICONTROL Ordine]**. Questa regola verrà attivata dopo tutte le altre regole configurate (che avevano `1` o `20` come [!UICONTROL Ordine]).

1. Seleziona **[!UICONTROL Mantieni modifiche]** per tornare alla schermata della regola principale
   ![Seleziona trigger caricato dalla libreria](assets/create-tag-rule-trigger-loaded-send.png)

1. Nella sezione **[!UICONTROL Azioni]**, seleziona **[!UICONTROL Aggiungi]**

1. Come **[!UICONTROL Estensione]**, seleziona **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Come **[!UICONTROL Tipo azione]**, seleziona **[!UICONTROL Invia evento]**

1. Come **[!UICONTROL XDM]**, seleziona l&#39;elemento dati `xdm.variable.content` creato nella lezione precedente

1. Seleziona **[!UICONTROL Mantieni modifiche]** per tornare alla schermata della regola principale

   ![Aggiungi azione Invia evento](assets/create-rule-send-event-action.png)
1. Seleziona **[!UICONTROL Salva]** per salvare la regola

   ![Salva la regola](assets/create-rule-save-rule.png)

## Pubblicare le regole in una libreria

Successivamente, pubblica la regola nell&#39;ambiente di sviluppo in modo da poterne verificare il funzionamento.

Per creare una libreria:

1. Vai a **[!UICONTROL Flusso di pubblicazione]** nel menu di navigazione a sinistra

1. Seleziona **[!UICONTROL Aggiungi libreria]**

   ![Seleziona Aggiungi libreria](assets/rule-publish-library.png)
1. Per **[!UICONTROL Name]**, immetti `Luma Web SDK Tutorial`
1. Per l&#39;**[!UICONTROL ambiente]**, selezionare `Development`
1. Seleziona **[!UICONTROL Aggiungi tutte le risorse modificate]**

   >[!NOTE]
   >
   >    Dovresti visualizzare tutti i componenti tag creati nelle lezioni precedenti. L’estensione Core contiene il JavaScript di base richiesto da tutte le proprietà dei tag web.

1. Seleziona **[!UICONTROL Salva e genera per sviluppo]**

   ![Crea e genera la libreria](assets/create-tag-rule-library-changes.png)

La creazione della libreria potrebbe richiedere alcuni minuti e al termine viene visualizzato un punto verde a sinistra del nome della libreria:

![Build completata](assets/create-rule-development-success.png)

Come puoi vedere nella schermata [!UICONTROL Flusso di pubblicazione], il processo di pubblicazione richiede molto di più, il che va oltre l&#39;ambito di questa esercitazione. Questo tutorial utilizza una sola libreria nell’ambiente di sviluppo.

Ora puoi convalidare i dati nella richiesta utilizzando Adobe Experience Platform Debugger.

>[!NOTE]
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=it)
