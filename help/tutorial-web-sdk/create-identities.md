---
title: Acquisire identità per Platform Web SDK
description: Scopri come acquisire le identità in XDM e utilizzare l’elemento dati Identity Map per acquisire gli ID utente. Questa lezione fa parte del tutorial Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK, Tags, Identities
jira: KT-15402
exl-id: 7ca32dc8-dd86-48e0-8931-692bcbb2f446
source-git-commit: 070fc02801d3403bf65ca732323338481e25b581
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 3%

---

# Acquisire le identità

Scopri come acquisire le identità con Adobe Experience Platform Web SDK. Acquisisci dati di identità autenticati e non autenticati sul [sito Web di dimostrazione Luma](https://luma.enablementadobe.com). Scopri come utilizzare gli elementi dati creati in precedenza per raccogliere dati autenticati con un tipo di elemento dati Platform Web SDK denominato Identity map.

Questa lezione si concentra sull’elemento dati Identity map disponibile con l’estensione tag Adobe Experience Platform Web SDK. Mappa su XDM gli elementi dati contenenti un ID utente autenticato e lo stato di autenticazione.



## Obiettivi di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Comprendere la relazione tra Experience Cloud ID (ECID) e First Party Device ID (FPID)
* Differenza tra ID non autenticati e ID autenticati
* Creare un elemento dati della mappa di identità

## Prerequisiti

Hai una conoscenza di cos’è un livello dati, del sito web di dimostrazione [Luma](https://luma.enablementadobe.com){target="_blank"} e di come fare riferimento agli elementi dati nei tag. Devi aver completato le lezioni precedenti nell’esercitazione:

* [Configurare uno schema XDM](configure-schemas.md)
* [Configurare uno spazio dei nomi delle identità](configure-identities.md)
* [Configurare uno stream di dati](configure-datastream.md)
* [Estensione Web SDK installata nella proprietà tag](install-web-sdk.md)
* [Creare elementi dati](create-data-elements.md)


## Experience Cloud ID

[Experience Cloud ID (ECID)](https://experienceleague.adobe.com/it/docs/experience-platform/identity/features/ecid) è uno spazio dei nomi di identità condiviso e utilizzato nelle applicazioni Adobe Experience Platform e Adobe Experience Cloud. ECID fornisce la base per l’identità del cliente ed è l’identità predefinita per le proprietà digitali. ECID è l’identificatore ideale per il tracciamento del comportamento degli utenti non autenticati, in quanto è sempre presente.

<!-- FYI I commented this out because it was breaking the build - Jack
>[!TIP]
>
> When you use the Experience Platform Web SDK to set up Adobe applications on your digital properties, the ECID is generated at the Adobe Edge server level. As such, ECID is not viewable on the client-side network request payload. You can view the ECID by seeing the Preview tab of the network request, or by using the [Adobe Experience Platform Debugger Edge Trace](set-up-analytics.md#experience-cloud-id-validation).
>![View ECID](assets/validate-dev-console-ecid.png)
-->

Ulteriori informazioni sul tracciamento di [ECID tramite Platform Web SDK](https://experienceleague.adobe.com/it/docs/experience-platform/edge/identity/overview).

Gli ECID vengono impostati utilizzando una combinazione di cookie di prime parti e Platform Edge Network. Per impostazione predefinita, i cookie di identità di prime parti sono impostati sul lato client dal Web SDK. Per tenere conto delle restrizioni del browser sulla durata dei cookie, puoi scegliere di impostare cookie di identità di prima parte lato server. Questi cookie di identità sono denominati ID dispositivo di prime parti (FPID).

>[!IMPORTANT]
>
>L&#39;estensione del servizio [Experience Cloud ID](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension) non è necessaria per l&#39;implementazione di Adobe Experience Platform Web SDK, in quanto la funzionalità del servizio ID è incorporata in Platform Web SDK.

## ID dispositivo di prime parti (FPID)

Gli FPID sono cookie di prime parti _impostati con i propri server Web_ che Adobe utilizza per creare l&#39;ECID, invece di utilizzare il cookie di prime parti impostato dal Web SDK. Anche se il supporto del browser può variare, i cookie di prime parti tendono a essere più duraturi se impostati da un server che sfrutta un record DNS A (per IPv4) o AAAA (per IPv6), rispetto a quando impostati da un codice DNS CNAME o JavaScript.

Una volta impostato un cookie FPID, il relativo valore può essere recuperato e inviato ad Adobe durante la raccolta dei dati dell’evento. Gli FPID raccolti vengono utilizzati come seed per generare ECID su Platform Edge Network, che continuano ad essere gli identificatori predefiniti nelle applicazioni Adobe Experience Cloud.

Anche se gli FPID non vengono utilizzati in questa esercitazione, si consiglia di utilizzarli nella propria implementazione di Web SDK. Ulteriori informazioni su [ID dispositivo di prime parti in Platform Web SDK](https://experienceleague.adobe.com/it/docs/experience-platform/edge/identity/first-party-device-ids)

>[!CAUTION]
>
> L’FPID è un modo alternativo di generare l’ECID utilizzando un cookie impostato dai server web. Non viene utilizzato per identificare gli utenti autenticati.

## ID autenticato

Come indicato in precedenza, a tutti i visitatori delle proprietà digitali viene assegnato un ECID da Adobe quando si utilizza Platform Web SDK. ECID è l’identità predefinita per il tracciamento del comportamento digitale non autenticato.

Puoi anche inviare un ID utente autenticato in modo che Platform possa creare [grafi di identità](https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/identities/understanding-identity-and-identity-graphs) e Target possa impostare il proprio [ID terze parti](https://experienceleague.adobe.com/it/docs/target/using/audiences/visitor-profiles/3rd-party-id). L&#39;impostazione dell&#39;ID autenticato viene eseguita utilizzando il tipo di elemento dati [!UICONTROL Identity Map].

Per creare l&#39;elemento dati [!UICONTROL Identity Map]:

1. Vai a **[!UICONTROL Elementi dati]** e seleziona **[!UICONTROL Aggiungi elemento dati]**

1. **[!UICONTROL Denomina]** l&#39;elemento dati `Identity Map`

1. Come **[!UICONTROL Estensione]**, seleziona `Adobe Experience Platform Web SDK`

1. Come **[!UICONTROL Tipo di elemento dati]**, selezionare `Identity map`

1. Come **[!UICONTROL Spazio dei nomi]**, seleziona lo spazio dei nomi `lumaCrmId` creato nella lezione [Configurare le identità](configure-identities.md). Se non viene visualizzato nel menu a discesa, digitalo in.

1. Come **[!UICONTROL ID]**, seleziona l&#39;elemento dati `User Id` creato nella lezione [Creare elementi dati](create-data-elements.md#create-data-elements-to-capture-the-data-layer).

1. Come **[!UICONTROL Stato autenticato]**, selezionare **[!UICONTROL Stato autenticato]**
1. Seleziona **[!UICONTROL primario]**

1. Seleziona **[!UICONTROL Salva]**

   ![Interfaccia raccolta dati](assets/identity-id-namespace.png)

>[!IMPORTANT]
>
> Adobe consiglia di inviare identità che rappresentano una persona, ad esempio `Luma CRM Id`, come identità [!UICONTROL primaria].
>
> Se la mappa delle identità contiene l&#39;identificatore della persona, ad esempio `Luma CRM Id`, l&#39;identificatore della persona diventa l&#39;identità [!UICONTROL primaria]. In caso contrario, `ECID` diventa l&#39;identità [!UICONTROL primary].
>
> Inoltre, per i clienti delle applicazioni Platform, Adobe consiglia di implementare [regole di collegamento del grafico delle identità](https://experienceleague.adobe.com/it/docs/platform-learn/tutorials/identities/graph-linking-rules/overview) per evitare la compressione del grafico.

>[!NOTE]
>
> Non è necessario eseguire alcuna azione per acquisire l’ECID in un’implementazione di Web SDK. Viene acquisita automaticamente.


Al termine di questi passaggi, dovresti aver creato i seguenti elementi di dati:

| Elementi dati dell&#39;estensione core | Elementi dati dell’estensione Platform Web SDK |
|-----------------------------|-------------------------------|
| `Ecommerce Cart Products` | `Data Variable` |
| `Ecommerce Product Category` | `Identity Map` |
| `Ecommerce Product Id` | `XDM Variable` |
| `Ecommerce Product Name` | |
| `Ecommerce Purchase Id` | |
| `Ecommerce Purchase Products` |  |
| `Page Name` | |
| `User Id` | |
| `User Logged In` | |

Una volta impostati questi elementi dati, puoi iniziare a inviare dati a Platform Edge Network creando una regola nei tag.

>[!NOTE]
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com/adobe-experience-platform-18/tutorial-discussion-implement-adobe-experience-cloud-with-web-sdk-tutorial-248848?profile.language=it)
