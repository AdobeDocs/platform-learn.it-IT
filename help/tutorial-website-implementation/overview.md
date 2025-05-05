---
title: Implementare l’Experience Cloud nei siti web con i tag
description: L’implementazione dell’Experience Cloud nei siti web con i tag è il punto di partenza ideale per gli sviluppatori front-end o per gli esperti di marketing tecnico che desiderano imparare a implementare le soluzioni Adobe Experience Cloud sul loro sito web.
recommendations: catalog, noDisplay
exl-id: 1b95f0b2-3062-49d1-9b0b-e6824a54008f
source-git-commit: 2483409b52562e13a4f557fe5bdec75b5afb4716
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 37%

---

# Panoramica

_L&#39;implementazione dell&#39;Experience Cloud in Siti Web con Tag_ è il punto di partenza ideale per gli sviluppatori front-end o per gli esperti di marketing tecnico che desiderano imparare a implementare le soluzioni Adobe Experience Cloud sul proprio sito Web.

Ogni lezione contiene esercitazioni e informazioni fondamentali utili per implementare Experience Cloud e comprenderne il valore. Sono disponibili siti di dimostrazione per completare l’esercitazione e apprendere le tecniche di base in un ambiente sicuro. Dopo aver completato questa esercitazione, dovresti essere in grado di iniziare a implementare tutte le soluzioni di marketing tramite i tag sul tuo sito web.

>[!INFO]
>
>Questa esercitazione utilizza estensioni e librerie specifiche per l’applicazione (AppMeasurement.js per Adobe Analytics, at.js per Adobe Target). Se desideri implementare Adobe Experience Platform Web SDK, consulta l&#39;esercitazione [Implementare Adobe Experience Cloud con Web SDK](/help/tutorial-web-sdk/overview.md).


Dopo aver completato questa esercitazione, sarai in grado di:

* Creare una proprietà tag

* Installare una proprietà tag in un sito Web

* Aggiungere le seguenti soluzioni Adobe Experience Cloud:
   * **[Servizio Adobe Experience Platform Identity](id-service.md)**
   * **[Adobe Target](target.md)**
   * **[Adobe Analytics](analytics.md)**
   * **[Adobe Audience Manager](audience-manager.md)**

* Creare regole ed elementi dati per inviare dati alle soluzioni Adobe

* Convalidare le implementazione tramite Adobe Experience Cloud Debugger

* Modifiche a Publish tramite ambienti di sviluppo, staging e produzione

>[!NOTE]
>
>Adobe Experience Platform Launch viene integrato in Adobe Experience Platform come suite di tecnologie per la raccolta dati. Nell’interfaccia sono state introdotte diverse modifiche terminologiche di cui tenere conto quando si utilizza questo contenuto:
>
> * Il platform launch (lato client) è ora **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it)**
> * Platform Launch Server Side è ora **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=it)**
> * Le configurazioni di Edge sono ora **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=it)**

>[!NOTE]
>
>Esercitazioni simili per più soluzioni sono disponibili anche per [Web SDK](../tutorial-web-sdk/overview.md) e [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## Prerequisiti

In queste lezioni, si presume che tu sia in possesso di un Adobe ID e delle autorizzazioni necessarie per completare gli esercizi. In caso contrario, potresti dover contattare l’amministratore di Experience Cloud per richiedere l’accesso.

* Per i tag, devi disporre delle autorizzazioni per sviluppare, approvare, Publish, gestire le estensioni e gestire gli ambienti. Per ulteriori informazioni sulle autorizzazioni per gli utenti tag, consulta [la documentazione](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=it).
* Con Adobe Analytics, devi conoscere il tuo server di tracciamento e quali suite per report utilizzerai per completare questa esercitazione.
* Ad Audience Manager, devi conoscere il tuo sottodominio Audience Manager (noto anche come &quot;Nome partner&quot; &quot;ID partner&quot; o &quot;Sottodominio partner&quot;)

Inoltre, si presume che tu abbia familiarità con linguaggi di sviluppo front-end come HTML e JavaScript. Non devi essere un esperto in questi linguaggi per completare le lezioni, ma ti saranno più utili se sei in grado di leggere e comprendere il codice senza difficoltà.

## Informazioni sui tag

La funzione tag di Adobe Experience Platform è la nuova generazione di funzionalità di gestione di tag per siti web e SDK per dispositivi mobili di Adobe. I tag offrono ai clienti un modo semplice di implementare e gestire tutte le soluzioni di analisi, marketing e annunci pubblicitari necessarie per fornire ai clienti esperienze personalizzate. Non esiste alcun costo aggiuntivo per i tag. È disponibile per qualsiasi cliente Adobe Experience Cloud.

I tag per i siti web consentono di gestire centralmente tutti i JavaScript relativi alle soluzioni di analisi, marketing e annunci pubblicitari utilizzate sui siti desktop e mobili. Ad esempio, se distribuisci Adobe Analytics, i tag gestiranno la libreria JavaScript di AppMeasurement, compileranno le variabili e attiveranno le richieste.

Il contenuto del contenitore è ridotto al minimo, compreso il tuo codice personalizzato. Ogni caratteristica è modulare. Se non hai bisogno di un elemento, non verrà incluso nella libreria. Il risultato è un&#39;implementazione veloce e compatta.

I tag sono anche una piattaforma che consente ai fornitori di terze parti di creare estensioni per semplificare la distribuzione delle soluzioni tramite i tag. Un’estensione è un pacchetto di codice (JavaScript, HTML e CSS) che estende l’interfaccia e le funzionalità client dei tag. Considera i tag come un sistema operativo; le estensioni sono paragonabili alle applicazioni che consentono di eseguire determinate attività.

## Informazioni sulle lezioni

In queste lezioni, implementerai Adobe Experience Cloud in un finto sito web per la vendita al dettaglio denominato Luma. Il [sito Luma](https://luma.enablementadobe.com/content/luma/us/en.html) dispone di un livello dati e funzionalità avanzati che consentono di realizzare un’implementazione realistica. Genererai la tua proprietà tag, nella tua organizzazione di Experienci Cloud, e la mapperai al nostro sito Luma ospitato utilizzando il Experience Cloud Debugger.

[![Sito Web Luma](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

## Procurati gli strumenti

1. Poiché utilizzerai alcune estensioni specifiche per il browser, è consigliabile completare l’esercitazione tramite il [browser web Chrome](https://www.google.com/chrome/)
1. Aggiungi l&#39;estensione [Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) al browser Chrome
1. Copia il codice pagina HTML di esempio

   +++Codice pagina HTML di esempio

   ```html
   <!doctype html>
   <html lang="en">
   <head>
       <title>Tags: Sample HTML Page</title>
       <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
       <link rel="preconnect" href="//dpm.demdex.net">
       <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
       <link rel="preconnect" href="//techmarketingdemos.demdex.net">
       <link rel="preconnect" href="//cm.everesttech.net">
       <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
       <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
       <link rel="dns-prefetch" href="//dpm.demdex.net">
       <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
       <link rel="dns-prefetch" href="//cm.everesttech.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
       <!--/Preconnect and DNS-Prefetch-->
       <!--Data Layer to enable rich data collection and targeting-->
       <script>
       var digitalData = {
           "page": {
               "pageInfo" : {
                   "pageName": "Home"
                   }
               }
       };
       </script>
       <!--/Data Layer-->
       <!--jQuery or other helper libraries-->
       <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
       <!--/jQuery-->
       <!--Tags Header Embed Code: REPLACE THE NEXT LINE WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
       <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
       <!--/Tags Header Embed Code-->
   </head>
   <body>
       <h1>Tags: Sample HTML Page</h1>
       <p>This is a very simple page to demonstrate basic implementation concepts of Tags</p>
       <p>See <a href="https://docs.adobe.com/content/help/it-IT/experience-cloud/implementing-in-websites-with-launch/index.html">Implementing the Experience Cloud in Websites with Tags</a> for the complete tutorial</p>
   </body>
   </html>
   ```

   +++

1. Procurati un editor di testo in cui puoi apportare modifiche alla pagina HTML di esempio. (Se non ne hai uno, consigliamo di provare [Brackets](https://brackets.io/))
1. Segnalibro del sito [Luma](https://luma.enablementadobe.com/content/luma/us/en.html)

>[!NOTE]
>
>Potrebbe essere più facile completare questa esercitazione con il sito Luma aperto in Chrome, mentre leggi questa esercitazione e completi i passaggi dell’interfaccia di Data Collection in un altro browser.

Cominciamo.

[Avanti &quot;Creare una proprietà tag&quot; >](create-a-property.md)
