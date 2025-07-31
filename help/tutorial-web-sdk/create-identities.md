---
title: Creare identità per Platform Web SDK
description: Scopri come creare identità in XDM e utilizzare l’elemento dati Identity Map per acquisire gli ID utente. Questa lezione fa parte del tutorial Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK, Tags, Identities
jira: KT-15402
exl-id: 7ca32dc8-dd86-48e0-8931-692bcbb2f446
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 3%

---

# Creare identità

Scopri come acquisire le identità con Adobe Experience Platform Web SDK. Acquisisci dati di identità autenticati e non autenticati sul [sito demo Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Scopri come utilizzare gli elementi dati creati in precedenza per raccogliere dati autenticati con un tipo di elemento dati Platform Web SDK denominato Identity map.

Questa lezione si concentra sull’elemento dati Identity map disponibile con l’estensione tag Adobe Experience Platform Web SDK. Mappa su XDM gli elementi dati contenenti un ID utente autenticato e lo stato di autenticazione.

## Obiettivi di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Comprendere la relazione tra Experience Cloud ID (ECID) e First Party Device ID (FPID)
* Differenza tra ID non autenticati e ID autenticati
* Creare un elemento dati della mappa di identità

## Prerequisiti

Hai una conoscenza di cos’è un livello dati, del sito di dimostrazione [Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} e di come fare riferimento agli elementi dati nei tag. Devi aver completato le lezioni precedenti nell’esercitazione:

* [Configurare uno schema XDM](configure-schemas.md)
* [Configurare uno spazio dei nomi delle identità](configure-identities.md)
* [Configurare uno stream di dati](configure-datastream.md)
* [Estensione Web SDK installata nella proprietà tag](install-web-sdk.md)
* [Creare elementi dati](create-data-elements.md)


## Experience Cloud ID

[Experience Cloud ID (ECID)](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/ecid) è uno spazio dei nomi di identità condiviso e utilizzato nelle applicazioni Adobe Experience Platform e Adobe Experience Cloud. ECID fornisce la base per l’identità del cliente ed è l’identità predefinita per le proprietà digitali. ECID è l’identificatore ideale per il tracciamento del comportamento degli utenti non autenticati, in quanto è sempre presente.

<!-- FYI I commented this out because it was breaking the build - Jack
>[!TIP]
>
> When you use the Experience Platform Web SDK to set up Adobe applications on your digital properties, the ECID is generated at the Adobe Edge server level. As such, ECID is not viewable on the client-side network request payload. You can view the ECID by seeing the Preview tab of the network request, or by using the [Adobe Experience Platform Debugger Edge Trace](set-up-analytics.md#experience-cloud-id-validation).
>![View ECID](assets/validate-dev-console-ecid.png)
-->

Ulteriori informazioni sul tracciamento di [ECID tramite Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/overview).

Gli ECID vengono impostati utilizzando una combinazione di cookie di prime parti e Platform Edge Network. Per impostazione predefinita, i cookie di identità di prime parti sono impostati sul lato client dal Web SDK. Per tenere conto delle restrizioni del browser sulla durata dei cookie, puoi scegliere di impostare cookie di identità di prima parte lato server. Questi cookie di identità sono denominati ID dispositivo di prime parti (FPID).

>[!IMPORTANT]
>
>L&#39;estensione del servizio [Experience Cloud ID](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension) non è necessaria per l&#39;implementazione di Adobe Experience Platform Web SDK, in quanto la funzionalità del servizio ID è incorporata in Platform Web SDK.

## ID dispositivo di prime parti (FPID)

Gli FPID sono cookie di prime parti _impostati con i propri server Web_ che Adobe utilizza per creare l&#39;ECID, invece di utilizzare il cookie di prime parti impostato dal Web SDK. Anche se il supporto del browser può variare, i cookie di prime parti tendono a essere più duraturi se impostati da un server che sfrutta un record DNS A (per IPv4) o AAAA (per IPv6), rispetto a quando impostati da un codice DNS CNAME o JavaScript.

Una volta impostato un cookie FPID, il relativo valore può essere recuperato e inviato ad Adobe durante la raccolta dei dati dell’evento. Gli FPID raccolti vengono utilizzati come seed per generare ECID su Platform Edge Network, che continuano ad essere gli identificatori predefiniti nelle applicazioni Adobe Experience Cloud.

Anche se gli FPID non vengono utilizzati in questa esercitazione, si consiglia di utilizzarli nella propria implementazione di Web SDK. Ulteriori informazioni su [ID dispositivo di prime parti in Platform Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/first-party-device-ids)

>[!CAUTION]
>
> L’FPID è un modo alternativo di generare l’ECID utilizzando un cookie impostato dai server web. Non viene utilizzato per identificare gli utenti autenticati.

## ID autenticato

Come indicato in precedenza, a tutti i visitatori delle proprietà digitali viene assegnato un ECID da Adobe quando si utilizza Platform Web SDK. ECID è l’identità predefinita per il tracciamento del comportamento digitale non autenticato.

Puoi anche inviare un ID utente autenticato in modo che Platform possa creare [grafi di identità](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/identities/understanding-identity-and-identity-graphs) e Target possa impostare il proprio [ID terze parti](https://experienceleague.adobe.com/en/docs/target/using/audiences/visitor-profiles/3rd-party-id). L&#39;impostazione dell&#39;ID autenticato viene eseguita utilizzando il tipo di elemento dati [!UICONTROL Identity Map].

Per creare l&#39;elemento dati [!UICONTROL Identity Map]:

1. Vai a **[!UICONTROL Elementi dati]** e seleziona **[!UICONTROL Aggiungi elemento dati]**

1. **[!UICONTROL Nome]** dell&#39;elemento dati `identityMap.loginID`

1. Come **[!UICONTROL Estensione]**, seleziona `Adobe Experience Platform Web SDK`

1. Come **[!UICONTROL Tipo di elemento dati]**, selezionare `Identity map`

1. Verrà visualizzata un&#39;area dello schermo a destra nell&#39;interfaccia **[!UICONTROL Data Collection]** per configurare l&#39;identità:

   ![Interfaccia raccolta dati](assets/identity-identityMap-setup.png)

1. Come **[!UICONTROL Spazio dei nomi]**, seleziona lo spazio dei nomi `lumaCrmId` creato in precedenza nella lezione [Configurare le identità](configure-identities.md). Se non viene visualizzato nel menu a discesa, digitalo in.

1. Dopo aver selezionato **[!UICONTROL Spazio dei nomi]**, è necessario impostare un ID. Seleziona l’elemento dati `user.profile.attributes.username` creato in precedenza nella lezione [Creare elementi dati](create-data-elements.md#create-data-elements-to-capture-the-data-layer), che acquisisce un ID quando gli utenti vengono registrati nel sito Luma.

   <!--  >[!TIP]
    >
    >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
    >
    >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
    -->

1. Come **[!UICONTROL Stato autenticato]**, selezionare **[!UICONTROL Stato autenticato]**
1. Seleziona **[!UICONTROL primario]**

1. Seleziona **[!UICONTROL Salva]**

   ![Interfaccia raccolta dati](assets/identity-id-namespace.png)

>[!TIP]
>
> Adobe consiglia di inviare identità che rappresentano una persona, ad esempio `Luma CRM Id`, come identità [!UICONTROL primaria].
>
> Se la mappa delle identità contiene l&#39;identificatore della persona, ad esempio `Luma CRM Id`, l&#39;identificatore della persona diventa l&#39;identità [!UICONTROL primaria]. In caso contrario, `ECID` diventa l&#39;identità [!UICONTROL primary].




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

Una volta impostati questi elementi dati, puoi iniziare a inviare dati a Platform Edge Network creando una regola nei tag.

>[!NOTE]
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
