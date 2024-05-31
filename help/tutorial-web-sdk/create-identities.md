---
title: Creare identità per Platform Web SDK
description: Scopri come creare identità in XDM e utilizzare l’elemento dati Identity Map per acquisire gli ID utente. Questa lezione fa parte del tutorial Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK, Tags, Identities
jira: KT-15402
exl-id: 7ca32dc8-dd86-48e0-8931-692bcbb2f446
source-git-commit: c5318809bfd475463bac3c05d4f35138fb2d7f28
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 3%

---

# Creare identità

Scopri come acquisire le identità con Adobe Experience Platform Web SDK. Acquisire dati di identità autenticati e non autenticati sul [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Scopri come utilizzare gli elementi dati creati in precedenza per la raccolta di dati autenticati con un tipo di elemento dati Platform Web SDK denominato Mappa identità.

Questa lezione si concentra sull’elemento dati Identity map disponibile con l’estensione tag Adobe Experience Platform Web SDK. Mappa su XDM gli elementi dati contenenti un ID utente autenticato e lo stato di autenticazione.

## Obiettivi di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Comprendere la relazione tra l’ID Experience Cloud (ECID) e l’ID dispositivo di prime parti (FPID)
* Differenza tra ID non autenticati e ID autenticati
* Creare un elemento dati della mappa di identità

## Prerequisiti

Conoscere cos’è un livello dati, acquisire familiarità con [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} e sapere come fare riferimento agli elementi dati nei tag. Devi aver completato le lezioni precedenti nell’esercitazione:

* [Configurare uno schema XDM](configure-schemas.md)
* [Configurare uno spazio dei nomi delle identità](configure-identities.md)
* [Configurare uno stream di dati](configure-datastream.md)
* [Estensione Web SDK installata nella proprietà tag](install-web-sdk.md)
* [Creare elementi dati](create-data-elements.md)


## Experience Cloud ID

Il [ID Experience Cloud (ECID)](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/ecid) è uno spazio dei nomi di identità condiviso utilizzato nelle applicazioni Adobe Experience Platform e Adobe Experience Cloud. ECID fornisce la base per l’identità del cliente ed è l’identità predefinita per le proprietà digitali. ECID è l’identificatore ideale per il tracciamento del comportamento degli utenti non autenticati, in quanto è sempre presente.

<!-- FYI I commented this out because it was breaking the build - Jack
>[!TIP]
>
> When you use the Experience Platform Web SDK to set up Adobe applications on your digital properties, the ECID is generated at the Adobe Edge server level. As such, ECID is not viewable on the client-side network request payload. You can view the ECID by seeing the Preview tab of the network request, or by using the [Adobe Experience Platform Debugger Edge Trace](set-up-analytics.md#experience-cloud-id-validation).
>![View ECID](assets/validate-dev-console-ecid.png)
-->

Ulteriori informazioni su come [Gli ECID vengono tracciati utilizzando Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/overview).

Gli ECID vengono impostati utilizzando una combinazione di cookie di prime parti e Edge Network di Platform. Per impostazione predefinita, i cookie di identità di prime parti sono impostati lato client dall’SDK web. Per tenere conto delle restrizioni del browser sulla durata dei cookie, puoi scegliere di impostare cookie di identità di prima parte lato server. Questi cookie di identità sono denominati ID dispositivo di prime parti (FPID).

>[!IMPORTANT]
>
>Il [Estensione del servizio ID Experience Cloud](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension) non è necessario quando si implementa Adobe Experience Platform Web SDK, in quanto la funzionalità del servizio ID è integrata in Platform Web SDK.

## ID dispositivo di prime parti (FPID)

Gli FPID sono cookie di prime parti _si imposta utilizzando i propri server web_ L’Adobe utilizza quindi per creare l’ECID, invece di utilizzare il cookie di prime parti impostato dall’SDK web. Anche se il supporto del browser può variare, i cookie di prime parti tendono a essere più duraturi se impostati da un server che sfrutta un record A DNS (per IPv4) o AAAA (per IPv6), rispetto a quando impostati da un CNAME DNS o da un codice JavaScript.

Una volta impostato un cookie FPID, il relativo valore può essere recuperato e inviato all’Adobe durante la raccolta dei dati dell’evento. Gli FPID raccolti vengono utilizzati come seed per generare ECID sull’Edge Network di Platform, che continuano a essere gli identificatori predefiniti nelle applicazioni Adobe Experience Cloud.

Anche se gli FPID non vengono utilizzati in questa esercitazione, si consiglia di utilizzarli nella propria implementazione dell’SDK per web. Ulteriori informazioni su [ID dispositivo di prime parti nell’SDK per web di Platform](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/first-party-device-ids)

>[!CAUTION]
>
> L’FPID è un modo alternativo di generare l’ECID utilizzando un cookie impostato dai server web. Non viene utilizzato per identificare gli utenti autenticati.

## ID autenticato

Come indicato in precedenza, a tutti i visitatori delle proprietà digitali viene assegnato un ECID a titolo di Adobe quando si utilizza Platform Web SDK. ECID è l’identità predefinita per il tracciamento del comportamento digitale non autenticato.

Puoi anche inviare un ID utente autenticato in modo che Platform possa creare [Grafici delle identità](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/identities/understanding-identity-and-identity-graphs) e Target può impostare i propri [Id Terze Parti](https://experienceleague.adobe.com/en/docs/target/using/audiences/visitor-profiles/3rd-party-id). L’impostazione dell’ID autenticato viene eseguita utilizzando [!UICONTROL Mappa identità] tipo di elemento dati.

Per creare [!UICONTROL Mappa identità] data element:

1. Vai a **[!UICONTROL Elementi dati]** e seleziona **[!UICONTROL Aggiungi elemento dati]**

1. **[!UICONTROL Nome]** l’elemento dati `identityMap.loginID`

1. Come **[!UICONTROL Estensione]**, seleziona `Adobe Experience Platform Web SDK`

1. Come **[!UICONTROL Tipo di elemento dati]**, seleziona `Identity map`

1. In questo modo viene visualizzata un&#39;area dello schermo a destra all&#39;interno del **[!UICONTROL Interfaccia di Data Collection]** per configurare l’identità:

   ![Interfaccia di Data Collection](assets/identity-identityMap-setup.png)

1. Come  **[!UICONTROL Namespace]**, seleziona la `lumaCrmId` spazio dei nomi creato in precedenza nel [Configurare le identità](configure-identities.md) lezione. Se non viene visualizzato nel menu a discesa, digitalo in.

1. Dopo il **[!UICONTROL Namespace]** deve essere impostato un ID. Seleziona la `user.profile.attributes.username` elemento dati creato in precedenza in [Creare elementi dati](create-data-elements.md#create-data-elements-to-capture-the-data-layer) lezione, che acquisisce un ID quando gli utenti vengono connessi al sito Luma.

   <!--  >[!TIP]
    >
    >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
    >
    >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
    -->

1. Come **[!UICONTROL Stato autenticato]**, seleziona **[!UICONTROL Autenticato]**
1. Seleziona **[!UICONTROL Principale]**

1. Seleziona **[!UICONTROL Salva]**

   ![Interfaccia di Data Collection](assets/identity-id-namespace.png)

>[!TIP]
>
> L’Adobe consiglia di inviare identità che rappresentano una persona, come `Luma CRM Id`, come [!UICONTROL primario] identità.
>
> Se la mappa delle identità contiene l’identificatore della persona (ad esempio, `Luma CRM Id`), l’identificatore della persona diventa [!UICONTROL primario] identità. Altrimenti, `ECID` diventa [!UICONTROL primario] identità.




<!--
1. Once the data element is configured in **[!UICONTROL Data Collection interface]**, it can be tested on the Luma web property like any other Data Element. Enter the following script in the browser developer console
   
   
   ```
   _satellite.getVar('identityMap.loginID')
   ```  

   ![Data Collection interface](assets/identity-consoleIdentityDataElement.png)
   
   >[!NOTE]
   >
   >ECID identifier will NOT populate in the Data Element, as this is configured already with Platform Web SDK.   
-->

Al termine di questi passaggi, dovresti aver creato i seguenti elementi di dati:

| Elementi dati dell&#39;estensione core | Elementi dati dell’estensione Platform Web SDK |
-----------------------------|-------------------------------
| `cart.orderId` | `data.variable` |
| `cart.productInfo` | `identityMap.loginID` |
| `cart.productInfo.purchase` | `xdm.variable.content` |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `product.category` | |
| `product.productInfo.sku` | |
| `product.productInfo.title` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

Una volta impostati questi elementi dati, puoi iniziare a inviare dati all’Edge Network di Platform creando una regola nei tag.

[Successivo: ](create-tag-rule.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
