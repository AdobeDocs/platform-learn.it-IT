---
title: Implementare l’Experience Cloud nei siti web con tag
description: L’implementazione dell’Experience Cloud in Siti web con tag è il punto di partenza ideale per gli sviluppatori front-end o per gli esperti di marketing tecnico che desiderano imparare a implementare le soluzioni Adobe Experience Cloud sul loro sito web.
recommendations: catalog, noDisplay
exl-id: 1b95f0b2-3062-49d1-9b0b-e6824a54008f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 44%

---

# Panoramica

_Implementare l’Experience Cloud nei siti web con tag_ è il punto di partenza ideale per gli sviluppatori front-end o per gli esperti di marketing tecnico che desiderano imparare a implementare le soluzioni Adobe Experience Cloud sul loro sito web.

Ogni lezione contiene esercitazioni e informazioni fondamentali utili per implementare Experience Cloud e comprenderne il valore. Sono disponibili siti di dimostrazione per completare l’esercitazione e apprendere le tecniche di base in un ambiente sicuro. Dopo aver completato questa esercitazione, dovresti essere in grado di iniziare a implementare tutte le soluzioni di marketing tramite i tag sul tuo sito web.

>[!INFO]
>
>Questa esercitazione utilizza estensioni e librerie specifiche per le applicazioni (AppMeasurement.js per Adobe Analytics, at.js per Adobe Target). Se desideri implementare Adobe Experience Platform Web SDK, consulta la sezione [Implementare Adobe Experience Cloud con l’SDK per web](/help/tutorial-web-sdk/overview.md) esercitazione.


Dopo aver completato questa esercitazione, sarai in grado di:

* Creare una proprietà tag

* Installare una proprietà tag in un sito web

* Aggiungere le seguenti soluzioni Adobe Experience Cloud:
   * **[Servizio Adobe Experience Platform Identity](id-service.md)**
   * **[Adobe Target](target.md)**
   * **[Adobe Analytics](analytics.md)**
   * **[Adobe Audience Manager](audience-manager.md)**

* Creare regole ed elementi dati per inviare dati alle soluzioni Adobe

* Convalidare le implementazione tramite Adobe Experience Cloud Debugger

* Pubblicare modifiche tramite ambienti di sviluppo, staging e produzione.

>[!NOTE]
>
>Adobe Experience Platform Launch viene integrato in Adobe Experience Platform come suite di tecnologie per la raccolta dati. Nell’interfaccia sono state introdotte diverse modifiche terminologiche di cui tenere conto durante l’utilizzo di questo contenuto:
>
> * Il platform launch (lato client) è ora **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it)**
> * Lato server di platform launch è ora **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Le configurazioni Edge sono ora **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=it)**


>[!NOTE]
>
>Sono disponibili esercitazioni simili per più soluzioni anche per [SDK per web](../tutorial-web-sdk/overview.md) e [SDK per dispositivi mobili](../tutorial-mobile-sdk/overview.md).

## Prerequisiti

In queste lezioni, si presume che tu sia in possesso di un Adobe ID e delle autorizzazioni necessarie per completare gli esercizi. In caso contrario, potresti dover contattare l’amministratore di Experience Cloud per richiedere l’accesso.

* Per i tag, devi disporre delle autorizzazioni per sviluppare, approvare, pubblicare, gestire le estensioni e gestire gli ambienti. Per ulteriori informazioni sulle autorizzazioni per gli utenti dei tag, consulta [la documentazione](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).
* Con Adobe Analytics, devi conoscere il tuo server di tracciamento e quali suite per report utilizzerai per completare questa esercitazione.
* Ad Audience Manager, devi conoscere il tuo sottodominio Audience Manager (noto anche come &quot;Nome partner&quot; &quot;ID partner&quot; o &quot;Sottodominio partner&quot;)

Inoltre, si presume che tu abbia familiarità con linguaggi di sviluppo front-end come HTML e JavaScript. Non devi essere un esperto in queste lingue per completare le lezioni, ma ti saranno più utili se sei in grado di leggere e comprendere il codice senza difficoltà.

## Informazioni sui tag

La funzione tag di Adobe Experience Platform è la nuova generazione di funzionalità di gestione tag per siti web e SDK per dispositivi mobili di Adobe. I tag forniscono ai clienti un modo semplice di implementare e gestire tutte le soluzioni di analisi, marketing e pubblicità necessarie per fornire ai clienti esperienze personalizzate. Non esiste alcun costo aggiuntivo per i tag. È disponibile per qualsiasi cliente Adobe Experience Cloud.

I tag per i siti web ti consentono di gestire centralmente tutti i JavaScript relativi alle soluzioni di analisi, marketing e pubblicità utilizzate sui siti desktop e mobili. Ad esempio, se distribuisci Adobe Analytics, i tag gestiranno la libreria JavaScript AppMeasurement, compileranno le variabili e attiveranno le richieste.

Il contenuto del contenitore è ridotto al minimo, compreso il tuo codice personalizzato. Ogni caratteristica è modulare. Se non hai bisogno di un elemento, non verrà incluso nella libreria. Il risultato è un&#39;implementazione veloce e compatta.

I tag sono anche una piattaforma che consente ai fornitori di terze parti di creare estensioni per semplificare la distribuzione delle loro soluzioni tramite i tag. Un&#39;estensione è un pacchetto di codice (JavaScript, HTML e CSS) che estende l&#39;interfaccia tag e le funzionalità client. È possibile considerare i tag come un sistema operativo, e le estensioni sono le app che si utilizzano per eseguire le attività.

## Informazioni sulle lezioni

In queste lezioni, implementerai Adobe Experience Cloud in un finto sito web per la vendita al dettaglio denominato Luma. Il [sito Luma](https://luma.enablementadobe.com/content/luma/us/en.html) dispone di un livello dati e funzionalità avanzati che consentono di realizzare un’implementazione realistica. Potrai creare la tua proprietà tag, nella tua organizzazione Experience Cloud, e mapparla sul nostro sito Luma ospitato utilizzando il Experience Cloud Debugger .

[![Sito web Luma](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

## Procurati gli strumenti

1. Poiché utilizzerai alcune estensioni specifiche per il browser, è consigliabile completare l’esercitazione tramite il [browser web Chrome](https://www.google.com/chrome/)
1. Aggiungi l’estensione [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) al browser Chrome
1. Scarica la [pagina HTML di esempio](https://www.enablementadobe.com/multi/web/basic-sample.html) (fai clic con il pulsante destro del mouse sul collegamento e fai clic su “Salva link con nome”)
1. Procurati un editor di testo in cui puoi apportare modifiche alla pagina HTML di esempio. (Se non ne hai uno, consigliamo di provare [Brackets](https://brackets.io/))
1. Segnalibro del sito [Luma](https://luma.enablementadobe.com/content/luma/us/en.html)

>[!NOTE]
>
>Potrebbe essere più facile completare questa esercitazione con il sito Luma aperto in Chrome, mentre leggi questa esercitazione e completi i passaggi dell’interfaccia di raccolta dati in un altro browser.

Cominciamo.

[Avanti &quot;Creare una proprietà tag&quot; >](create-a-property.md)
