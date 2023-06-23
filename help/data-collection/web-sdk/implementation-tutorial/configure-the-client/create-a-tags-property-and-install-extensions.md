---
title: Creare una proprietà tag Adobe Experience Platform e installare le estensioni
description: Creare una proprietà tag Adobe Experience Platform e installare le estensioni
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 7403059f-b34c-48e0-9efe-b2db7a9afb27
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# Creare una proprietà tag Adobe Experience Platform e installare le estensioni

Ora che il codice nella pagina sta inviando dati ed eventi al livello dati, è ora che l’addetto al marketing legga i dati dal livello dati e li invii a Adobe Experience Platform. In genere, questo richiederebbe due librerie JavaScript:

* Adobe di Client Data Layer: nei passaggi precedenti, hai creato un array di livello dati e vi hai inserito oggetti. Per accedere ai dati, devi caricare la libreria JavaScript Adobe Client Data Layer, che offre diversi modi per ricevere notifiche su eventi e modifiche al livello dati, oltre a metodi semplici per accedere ai dati.
* Adobe Experience Platform Web SDK: questa libreria JavaScript comunica con Adobe Experience Platform Edge Network. L’SDK gestisce l’identità, il consenso, la raccolta dati, la personalizzazione, i tipi di pubblico e altro ancora.

Sebbene sia possibile caricare queste singole librerie sul sito web e utilizzarle direttamente, si consiglia di utilizzare [Tag Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it). Con Tag, puoi incorporare un singolo script nel HTML e utilizzare l’interfaccia utente Tag per distribuire sia Adobe Client Data Layer che Adobe Experience Platform Web SDK. I tag consentono inoltre di creare regole per l’invio di dati, tra le altre cose. Questo tutorial utilizza i tag per questo scopo e presuppone che tu abbia una conoscenza di base del funzionamento dei tag.

## Creare una proprietà all’interno di Tag

Se non lo hai già fatto, [creare una proprietà all’interno di Tag](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html#create-or-configure-a-property).

## Installare l’estensione Adobe Client Data Layer

Installa l’estensione Adobe Client Data Layer passando al catalogo delle estensioni, individuando l’estensione e facendo clic sulle rispettive [!UICONTROL Installa] pulsante. Dovresti visualizzare una schermata di configurazione.

![Installazione dell’estensione Adobe Client Data Layer](../../../assets/implementation-strategy/acdl-extension-installation.png)

Per questa esercitazione, non è necessario modificare i valori predefiniti. Fai clic su [!UICONTROL Salva].

## Installare l’estensione Adobe Experience Platform Web SDK

Quindi, installa l&#39;estensione Adobe Experience Platform Web SDK trovando l&#39;estensione nel catalogo delle estensioni e facendo clic sul rispettivo [!UICONTROL Installa] pulsante. Dovresti visualizzare una schermata di configurazione.

![Installazione dell’estensione Adobe Experience Platform Web SDK](../../../assets/implementation-strategy/web-sdk-extension-installation.png)

In entrata [Creare un flusso di dati](../configure-the-server/create-a-datastream.md), hai creato un flusso di dati a cui Adobe Experience Platform Edge Network fa riferimento per determinare dove inviare i dati in entrata. Quando esegui richieste da Adobe Experience Platform Web SDK a Edge Network, devi indicare a quale flusso di dati deve fare riferimento Edge Network.

A tale scopo, trovare il [!UICONTROL Datastream] e selezionare lo stream di dati creato in precedenza. Vengono presentati gli stessi ambienti dello stream di dati visualizzati in [Creare un flusso di dati](../configure-the-server/create-a-datastream.md).

![Selezione dello stream di dati](../../../assets/implementation-strategy/web-sdk-datastream-selection.png)

Come discusso in [Creare un flusso di dati](../configure-the-server/create-a-dataset.md), questi ambienti di set di dati hanno una relazione con gli ambienti di tag. Supponiamo di completare l’installazione dell’estensione Adobe Experience Platform Web SDK, creare una libreria di tag che includa l’estensione, quindi pubblicare la libreria in un ambiente di sviluppo Tag. Quando la libreria di tag viene caricata sulla pagina web e l’estensione Adobe Experience Platform Web SDK effettua una richiesta a Edge Network, l’estensione include [!UICONTROL Ambiente di sviluppo] ID ambiente dello stream di dati. Edge Network, a sua volta, utilizza tale ID per leggere la configurazione di [!UICONTROL Ambiente di sviluppo] ambiente dello stream di dati e inoltro dei dati ai prodotti Adobe appropriati.

Al momento, disponi di un solo ambiente per lo stream di dati di sviluppo, un ambiente per lo stream di dati di staging e un ambiente per lo stream di dati di produzione. Per questo motivo, nell’interfaccia utente per la configurazione dell’estensione vengono visualizzati tutti come preselezionati e non modificabili. È tuttavia possibile creare più ambienti di sviluppo dello stream di dati (uno per te e uno per il tuo collega, ad esempio) utilizzando l’interfaccia utente dello stream di dati. Se disponi di più ambienti di flusso di dati di sviluppo, puoi selezionare quello che desideri utilizzare per questa proprietà tag.

Infine, scorri verso il basso e deseleziona [!UICONTROL Abilita raccolta dati di clic]. Per impostazione predefinita, l&#39;SDK tiene traccia automaticamente dei collegamenti. Tuttavia, in questo tutorial verrà illustrato come tenere traccia dei clic sui collegamenti personalizzati utilizzando le informazioni sui collegamenti personalizzati.

Fai clic sul pulsante [!UICONTROL Salva] per completare l&#39;installazione dell&#39;estensione Adobe Experience Platform Web SDK.

Sono state installate le estensioni appropriate. È ora di creare regole ed elementi di dati.
