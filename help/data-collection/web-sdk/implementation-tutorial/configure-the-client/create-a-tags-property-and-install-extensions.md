---
title: Creare una proprietà tag Adobe Experience Platform e installare le estensioni
description: Creare una proprietà tag Adobe Experience Platform e installare le estensioni
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 7403059f-b34c-48e0-9efe-b2db7a9afb27
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 1%

---

# Creare una proprietà tag Adobe Experience Platform e installare le estensioni

Ora che il codice su pagina sta inviando dati ed eventi al livello dati, è ora che l&#39;addetto al marketing legga i dati dal livello dati e li invii a Adobe Experience Platform. Questo richiederebbe in genere due librerie JavaScript:

* Livello dati client di Adobe: Nei passaggi precedenti, era stato creato un array di livello dati e inserito degli oggetti. Per accedere ai dati, è necessario caricare la libreria JavaScript Adobe Client Data Layer, che fornisce modi per ricevere notifiche sulle modifiche e sugli eventi dei livelli dati e fornisce anche modi semplici per accedere ai dati.
* Adobe Experience Platform Web SDK: Questa libreria JavaScript comunica con Adobe Experience Platform Edge Network. L’SDK gestisce identità, consenso, raccolta dati, personalizzazione, pubblico e altro ancora.

Anche se puoi caricare queste librerie individuali sul tuo sito web e utilizzarle direttamente, ti consigliamo di utilizzare [Tag Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it). Con i tag, è possibile incorporare un singolo script in HTML e utilizzare l’interfaccia utente Tag per distribuire sia Adobe Client Data Layer che Adobe Experience Platform Web SDK. I tag consentono inoltre di creare regole per l’invio di dati, tra le altre cose. Questa esercitazione utilizza i tag a questo scopo e presuppone che tu abbia una comprensione di base del funzionamento dei tag.

## Creare una proprietà all’interno di Tag

Se non lo hai già fatto, [creare una proprietà all’interno di Tag](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html#create-or-configure-a-property).

## Installare l’estensione Adobe Client Data Layer

Installa l&#39;estensione Adobe Client Data Layer andando al catalogo delle estensioni, trovando l&#39;estensione e facendo clic sul rispettivo [!UICONTROL Installa] pulsante . Dovresti visualizzare una schermata di configurazione.

![Installazione dell’estensione Adobe Client Data Layer](../../../assets/implementation-strategy/acdl-extension-installation.png)

Per questa esercitazione, non è necessario modificare i valori predefiniti. Fai clic su [!UICONTROL Salva].

## Installare l’estensione Adobe Experience Platform Web SDK

Quindi, installa l&#39;estensione Adobe Experience Platform Web SDK trovando l&#39;estensione nel catalogo delle estensioni e facendo clic sul rispettivo [!UICONTROL Installa] pulsante . Dovresti visualizzare una schermata di configurazione.

![Installazione dell&#39;estensione Adobe Experience Platform Web SDK](../../../assets/implementation-strategy/web-sdk-extension-installation.png)

In [Creare un datastream](../configure-the-server/create-a-datastream.md), hai creato un datastream a cui Adobe Experience Platform Edge Network fa riferimento per determinare dove inviare i dati in entrata. Quando esegui richieste da Adobe Experience Platform Web SDK a Edge Network, devi indicare a quale rete Edge di datastream deve fare riferimento.

Per eseguire questa operazione, individua la variabile [!UICONTROL Datastream] e selezionare il datastream creato in precedenza. Ti vengono presentati gli stessi ambienti del datastream che hai visto in [Creare un datastream](../configure-the-server/create-a-datastream.md).

![Selezione di Datastream](../../../assets/implementation-strategy/web-sdk-datastream-selection.png)

Come discusso in [Creare un datastream](../configure-the-server/create-a-dataset.md), questi ambienti di set di dati hanno una relazione con gli ambienti di tag. Supponi di completare l’installazione dell’estensione Adobe Experience Platform Web SDK, di creare una libreria di tag che include l’estensione, quindi di pubblicare la libreria in un ambiente di sviluppo Tag . Quando la libreria di tag viene caricata sulla pagina web e l&#39;estensione Adobe Experience Platform Web SDK invia una richiesta a Edge Network, l&#39;estensione include [!UICONTROL Ambiente di sviluppo] ID ambiente datastream. La rete Edge, a sua volta, utilizza tale ID per leggere la configurazione della [!UICONTROL Ambiente di sviluppo] ambiente datastream e inoltrare i dati ai prodotti di Adobe appropriati.

Al momento, disponi di un solo ambiente datastream di sviluppo, un ambiente datastream di staging e un ambiente datastream di produzione. Per questo motivo l’interfaccia utente per la configurazione dell’estensione li mostra tutti preselezionati e immodificabili. È tuttavia possibile creare più ambienti di sviluppo del datastream (uno per te e uno per il tuo collega, forse) utilizzando l’interfaccia utente del datastream. Se si dispone di più ambienti di datastream di sviluppo, è possibile selezionare quello che si desidera utilizzare per questa proprietà tag.

Infine, scorri verso il basso e deseleziona [!UICONTROL Abilita raccolta dati clic]. Per impostazione predefinita, l’SDK tiene traccia automaticamente dei collegamenti. In questa esercitazione, tuttavia, dimostreremo come tenere traccia dei clic sui collegamenti personalizzati utilizzando le informazioni sui collegamenti personalizzati.

Fai clic sul pulsante [!UICONTROL Salva] per completare l&#39;installazione dell&#39;estensione Adobe Experience Platform Web SDK.

Sono state installate le estensioni appropriate. È ora di creare regole ed elementi di dati.
