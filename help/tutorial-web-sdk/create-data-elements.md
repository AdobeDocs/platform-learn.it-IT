---
title: Creare elementi dati
description: Scopri come creare un oggetto XDM e mappare ad esso gli elementi dati nei tag. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
feature: Tags
exl-id: d662ec46-de9b-44ba-974a-f81dfc842e68
source-git-commit: 15bc08bdbdcb19f5b086267a6d94615cbfe1bac7
workflow-type: tm+mt
source-wordcount: '1212'
ht-degree: 0%

---

# Creare elementi dati


>[!CAUTION]
>
>Prevediamo di pubblicare modifiche principali a questo tutorial martedì 23 aprile 2024. Dopo questo punto molti esercizi cambieranno e potrebbe essere necessario riavviare l&#39;esercitazione dall&#39;inizio per completare tutte le lezioni.

Scopri come creare gli elementi dati essenziali necessari per acquisire i dati con Experienci Platform Web SDK. Acquisire sia contenuti che dati di identità sul [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Scopri come utilizzare lo schema XDM creato in precedenza per la raccolta di dati tramite Platform Web SDK tramite un nuovo tipo di elemento dati denominato Oggetto XDM.

>[!NOTE]
>
> A scopo dimostrativo, gli esercizi di questa lezione si basano sull’esempio utilizzato durante [Configurare uno schema](configure-schemas.md) passaggio; creazione di oggetti XDM di esempio che acquisiscono il contenuto visualizzato e le identità degli utenti sul [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!IMPORTANT]
>
>I dati per questa lezione provengono da `[!UICONTROL digitalData]` sul sito Luma. Per visualizzare il livello dati, apri la console per sviluppatori e digita `[!UICONTROL digitalData]` per visualizzare l’intero livello dati disponibile.![livello dati digitalData](assets/data-element-data-layer.png)


Indipendentemente da Platform Web SDK, è necessario continuare a creare all’interno della proprietà tag elementi di dati che vengono mappati dalle variabili di raccolta dati del sito web, ad esempio un livello di dati, un attributo HTML o altri. Una volta creati, tali elementi dati devono essere mappati sullo schema XDM creato durante il [configurare gli schemi](configure-schemas.md) lezione. A tal fine, l’estensione Platform Web SDK rende disponibile un nuovo tipo di elemento dati denominato oggetto XDM. Pertanto, la creazione di elementi dati consiste in due azioni:

1. Mappatura delle variabili del sito web con elementi di dati e
1. Mappatura di tali elementi dati a un oggetto XDM

Per il passaggio 1, continui a mappare il livello dati agli elementi dati nello stesso modo in cui lo mappi attualmente, utilizzando uno qualsiasi dei tipi di elementi dati dell’estensione tag Core. Per il passaggio 2, l’estensione Platform Web SDK crea un set di nuovi tipi di elementi dati non disponibili in precedenza:

* ID unione evento
* Mappa identità
* Oggetto XDM

Questa lezione si concentra sui tipi di elementi dati di tipo Oggetto XDM e Mappa delle identità. Verranno creati oggetti XDM per acquisire l’attività e lo stato di autenticazione dei visitatori Luma.

## Obiettivi di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Creare elementi di dati per acquisire contenuti e dati ID di accesso utente
* Creare un elemento dati della mappa di identità
* Mappare elementi dati a un elemento dati di oggetti XDM


## Prerequisiti

Conoscere cos’è un livello dati, acquisire familiarità con [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} e sapere come fare riferimento agli elementi dati nei tag. Devi aver completato i seguenti passaggi precedenti nell’esercitazione

* [Configurare le autorizzazioni](configure-permissions.md)
* [Configurare uno schema XDM](configure-schemas.md)
* [Configurare uno spazio dei nomi delle identità](configure-identities.md)
* [Configurare uno stream di dati](configure-datastream.md)
* [Estensione Web SDK installata nella proprietà tag](install-web-sdk.md)

>[!IMPORTANT]
>
>Il [Estensione del servizio ID Experience Cloud](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) non è necessario quando si implementa Adobe Experience Platform Web SDK, in quanto la funzionalità del servizio ID è integrata in Platform Web SDK.

## Creare elementi dati per acquisire il livello dati

Prima di iniziare la creazione dell’oggetto XDM, crea il seguente set di elementi dati mappati su [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} livello dati:

1. Vai a **[!UICONTROL Elementi dati]** e seleziona **[!UICONTROL Aggiungi elemento dati]** (o **[!UICONTROL Creare un nuovo elemento dati]** se nella proprietà tag non sono presenti elementi dati)

   ![Crea elemento dati](assets/data-element-create.jpg)

1. Denomina l’elemento dati `page.pageInfo.pageName`
1. Utilizza il **[!UICONTROL Variabile JavaScript]** **[!UICONTROL Tipo di elemento dati]** per puntare a un valore nel livello dati di Luma: `digitalData.page.pageInfo.pageName`

1. Seleziona le caselle per **[!UICONTROL Forza valore minuscolo]** e **[!UICONTROL Pulisci testo]** per standardizzare l&#39;uso di maiuscole/minuscole e rimuovere spazi estranei

1. Esci `None` come **[!UICONTROL Durata archiviazione]** poiché questo valore è diverso su ogni pagina

1. Seleziona **[!UICONTROL Salva]**

   ![Elemento dati Nome pagina](assets/data-element-pageName.jpg)

Segui gli stessi passaggi per creare questi quattro elementi dati aggiuntivi:

* **`page.pageInfo.server`**  mappato a
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  mappato a
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  mappato a
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** mappato a
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`cart.orderId`** mappato a `digitalData.cart.orderId` (utilizzerai durante il [Configurazione analisi](setup-analytics.md) lezione)


>[!CAUTION]
>
>Il [!UICONTROL Variabile JavaScript] il tipo di elemento dati tratta i riferimenti di array come punti invece che come parentesi, facendo riferimento all’elemento dati username come `digitalData.user[0].profile[0].attributes.username` **non funzionerà**.

## Creare un elemento dati di Identity Map

Successivamente puoi creare l’elemento dati Identity Map:

1. Vai a **[!UICONTROL Elementi dati]** e seleziona **[!UICONTROL Aggiungi elemento dati]**

1. **[!UICONTROL Nome]** l’elemento dati `identityMap.loginID`

1. Come **[!UICONTROL Estensione]**, seleziona `Adobe Experience Platform Web SDK`

1. Come **[!UICONTROL Tipo di elemento dati]**, seleziona `Identity map`

1. In questo modo viene visualizzata un&#39;area dello schermo a destra all&#39;interno del **[!UICONTROL Interfaccia di Data Collection]** per configurare l’identità:

   ![Interfaccia di Data Collection](assets/identity-identityMap-setup.png)

1. Come  **[!UICONTROL Namespace]**, seleziona la `Luma CRM Id` spazio dei nomi creato in precedenza nel [Configurare le identità](configure-identities.md) lezione.

   >[!NOTE]
   >
   >    Se non vedi il tuo `Luma CRM Id` spazio dei nomi, verifica di averlo creato anche nella sandbox di produzione predefinita. Solo gli spazi dei nomi creati nella sandbox di produzione predefinita vengono attualmente visualizzati nel menu a discesa dello spazio dei nomi.

1. Dopo il **[!UICONTROL Namespace]** deve essere impostato un ID. Seleziona la `user.profile.attributes.username` elemento dati creato in precedenza in questa lezione, che acquisisce un ID quando gli utenti vengono registrati nel sito Luma.

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
> Se la mappa di identità contiene l’identificatore della persona (ad es. `Luma CRM Id`), l&#39;identificatore della persona diventa [!UICONTROL primario] identità. Altrimenti, `ECID` diventa [!UICONTROL primario] identità.





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

## Mappatura di elementi dati su oggetti XDM

Tutti gli elementi dati creati devono essere mappati su un oggetto XDM. Questo oggetto deve essere conforme allo schema XDM creato durante la [Configurare uno schema](configure-schemas.md) lezione.

Esistono diversi modi per mappare gli elementi dati ai campi oggetto XDM. È possibile mappare singoli elementi dati a singoli campi XDM o mappare elementi dati a interi oggetti XDM, purché l’elemento dati corrisponda esattamente allo schema della coppia chiave-valore presente nell’oggetto XDM. In questa lezione verranno acquisiti i dati del contenuto mediante il mapping a singoli campi. Imparerai a [mappare un elemento dati a un intero oggetto XDM](setup-analytics.md#Map-an-entire-array-to-an-XDM-Object) nel [Configurazione analisi](setup-analytics.md) lezione.

Crea un oggetto XDM per acquisire i dati del contenuto:

1. Nel menu di navigazione a sinistra, seleziona **[!UICONTROL Elementi dati]**
1. Seleziona **[!UICONTROL Aggiungi elemento dati]**
1. **[!UICONTROL Nome]** l’elemento dati **`xdm.content`**
1. Come **[!UICONTROL Estensione]** seleziona `Adobe Experience Platform Web SDK`
1. Come **[!UICONTROL Tipo di elemento dati]** seleziona `XDM object`
1. Seleziona la piattaforma **[!UICONTROL Sandbox]** in cui hai creato lo schema XDM in durante la [Configurare uno schema XDM](configure-schemas.md) lezione, in questo esempio `DEVELOPMENT Mobile and Web SDK Courses`
1. Come **[!UICONTROL Schema]**, seleziona il tuo `Luma Web Event Data` schema:

   ![Oggetto XDM](assets/data-element-xdm.content-fields.png)

   >[!NOTE]
   >
   >La sandbox corrisponde all’Experience Platform di sandbox in cui è stato creato lo schema. Nell’istanza di Experience Platform possono essere disponibili più sandbox, quindi assicurati di selezionare quella giusta. Lavora sempre prima nello sviluppo, poi nella produzione.

1. Scorri verso il basso fino a raggiungere il **`web`** oggetto
1. Seleziona per aprirlo

   ![Oggetto Web](assets/data-element-pageviews-xdm-object.png)


1. Mappa le seguenti variabili XDM web su elementi di dati

   * **`web.webPageDetials.name`** a `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** a `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** a `%page.pageInfo.hierarchie1%`

   ![Oggetto XDM](assets/data-element-xdm.content.png)

1. Quindi, trova il `identityMap` nello schema e selezionarlo

1. Mappa su `identityMap.loginID` elemento dati

1. Seleziona **[!UICONTROL Salva]**

   ![Interfaccia di Data Collection](assets/identity-dataElements-xdmContent-LumaSchema-identityMapSelect3.png)




Al termine di questi passaggi, dovresti aver creato i seguenti elementi di dati:

| Elementi dati dell&#39;estensione CORE | Elementi dati di Platform Web SDK |
-----------------------------|-------------------------------
| `cart.orderId` | `identityMap.loginID` |
| `page.pageInfo.hierarchie1` | `xdm.content` |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

Una volta impostati questi elementi dati, puoi iniziare a inviare dati all’Edge Network di Platform tramite l’oggetto XDM creando una regola nei tag.

[Successivo: ](create-tag-rule.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
