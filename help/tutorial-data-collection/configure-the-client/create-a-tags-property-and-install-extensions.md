---
title: Creare una proprietà tag Adobe Experience Platform e installare le estensioni
description: Creare una proprietà tag Adobe Experience Platform e installare le estensioni
exl-id: d0fe82b5-a036-4e13-bae1-d1fee78d0084
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 1%

---

# Creare un Adobe Experience Platform [!DNL Tags] estensioni di proprietà e installazione

Ora che il codice su pagina sta inviando dati ed eventi al livello dati, è ora che l&#39;addetto al marketing legga i dati dal livello dati e li invii a Adobe Experience Platform. Questo richiederebbe in genere due librerie JavaScript:

* Livello dati client di Adobe: Nei passaggi precedenti, era stato creato un array di livello dati e inserito degli oggetti. Per accedere a questi dati, devi caricare la libreria JavaScript Adobe Client Data Layer. Questa libreria fornisce notifiche per eventi e modifiche al livello dati e un accesso semplice ai dati.
* Adobe Experience Platform Web SDK: Questa libreria JavaScript comunica con [Adobe Experience Platform Edge Network](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). L’SDK gestisce identità, consenso, raccolta dati, personalizzazione, pubblico e altro ancora.

Anche se puoi caricare queste librerie individuali sul tuo sito web e utilizzarle direttamente, ti consigliamo di utilizzare [Tag Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it). Con i tag, è possibile incorporare un singolo script in HTML e utilizzare l’interfaccia utente Tag per distribuire sia Adobe Client Data Layer che Adobe Experience Platform Web SDK. I tag consentono inoltre di creare regole per l’invio di dati, tra le altre cose. Questa esercitazione utilizza i tag a questo scopo e presuppone che tu abbia una comprensione di base del funzionamento dei tag.

## Creare una proprietà all’interno di Tag

1. [Creare una proprietà in Tag](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html#create-or-configure-a-property).

## Installare l’estensione Adobe Client Data Layer

Installa l&#39;estensione Adobe Client Data Layer:

1. Seleziona **[!UICONTROL Estensioni]** nella barra di navigazione a sinistra nella proprietà Tag utilizzata per questa esercitazione.
1. Seleziona la **[!UICONTROL Catalogo]** link in alto, quindi cercare &#39;livello dati&#39;.
1. Una volta che Adobe Client Data Layer viene visualizzato nei risultati, fai clic sul **[!UICONTROL Installa]** pulsante . Dovresti visualizzare una schermata di configurazione. Per questa esercitazione, non è necessario modificare i valori predefiniti.
1. Fai clic su **[!UICONTROL Salva]**.
   ![Installazione dell’estensione Adobe Client Data Layer](../assets/acdl-extension-installation.png)


## Installare l’estensione Adobe Experience Platform Web SDK

Quindi, installa l&#39;estensione Adobe Experience Platform Web SDK:

1. Cerca l&#39;estensione nel catalogo delle estensioni e fai clic sul rispettivo **[!UICONTROL Installa]** pulsante . Dovresti visualizzare la schermata di configurazione:
   ![Installazione dell&#39;estensione Adobe Experience Platform Web SDK](../assets/web-sdk-extension-installation.png)
1. In [!UICONTROL Datastream] selezionare il datastream creato in precedenza. Ti vengono presentati gli stessi ambienti del datastream che hai visto in [Creare un datastream](../configure-the-server/create-a-datastream.md).
   ![Selezione di Datastream](../assets/web-sdk-datastream-selection.png)
1. Ulteriori informazioni nella schermata di configurazione, trova e deseleziona **[!UICONTROL Abilita raccolta dati clic]**. Per impostazione predefinita, l’SDK tiene traccia automaticamente dei collegamenti. Questa esercitazione, tuttavia, illustra come tenere traccia dei clic sui collegamenti personalizzati utilizzando le informazioni sui collegamenti personalizzati.
1. Fai clic sul pulsante **[!UICONTROL Salva]** per completare l&#39;installazione dell&#39;estensione Adobe Experience Platform Web SDK.

>[!TIP]
>
>Gli ambienti di set di dati hanno una relazione con gli ambienti di tag. Supponi di completare l’installazione dell’estensione Adobe Experience Platform Web SDK, di creare una libreria di tag che include l’estensione, quindi di pubblicare la libreria in un ambiente di sviluppo Tag . Quando la libreria di tag viene caricata sulla pagina web e l&#39;estensione Adobe Experience Platform Web SDK invia una richiesta a Edge Network, l&#39;estensione include [!UICONTROL Ambiente di sviluppo] ID ambiente datastream. La rete Edge, a sua volta, utilizza tale ID per leggere la configurazione della [!UICONTROL Ambiente di sviluppo] ambiente datastream e inoltrare i dati ai prodotti di Adobe appropriati.
>
>Al momento, disponi di un solo ambiente datastream di sviluppo, un ambiente datastream di staging e un ambiente datastream di produzione. È possibile creare più ambienti di sviluppo del datastream (uno per te e uno per il tuo collega, forse) utilizzando l&#39;interfaccia utente del datastream. Se si dispone di più ambienti di datastream di sviluppo, è possibile selezionare quello che si desidera utilizzare per questa proprietà tag.


Sono state installate le estensioni appropriate. È ora di creare regole ed elementi di dati.

[Avanti: ](create-rules-for-tracking-page-view-and-commerce-events.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento della Raccolta dati. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
