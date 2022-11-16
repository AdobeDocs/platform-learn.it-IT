---
title: Aggiungi il codice di incorporamento
description: Scopri come ottenere i codici di incorporamento della proprietà tag e implementarli nel sito web. Questa lezione fa parte dell’esercitazione Implementa l’Experience Cloud in siti web .
exl-id: a2959553-2d6a-4c94-a7df-f62b720fd230
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 48%

---

# Aggiungi il codice di incorporamento

In questa lezione implementerai il codice di incorporamento asincrono dell’ambiente di sviluppo della proprietà tag. Lungo il percorso verranno illustrati due concetti principali dei tag: Ambienti e Codici di incorporamento.

>[!NOTE]
>
>Adobe Experience Platform Launch viene integrato in Adobe Experience Platform come suite di tecnologie per la raccolta dati. Nell’interfaccia sono state introdotte diverse modifiche terminologiche di cui tenere conto durante l’utilizzo di questo contenuto:
>
> * Il platform launch (lato client) è ora **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it)**
> * Lato server di platform launch è ora **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Le configurazioni Edge sono ora **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=it)**


## Finalità di apprendimento

Alla fine di questa lezione, potrai:

* Ottieni il codice di incorporamento per la proprietà tag
* Comprendere la differenza tra ambiente di sviluppo, ambiente di staging e ambiente di produzione.
* Aggiungere un codice di incorporamento tag a un documento HTML
* Spiega la posizione ottimale del codice di incorporamento del tag in relazione ad altro codice nel `<head>` di un documento HTML

## Copiare il codice di incorporamento

Il codice di incorporamento è un `<script>` alle pagine Web per caricare ed eseguire la logica generata nei tag. Se carichi la libreria in modo asincrono, il browser continua a caricare la pagina, recupera la libreria di tag ed esegue le operazioni in parallelo. In questo caso, esiste un solo codice da incorporare, che collochi in `<head>`. (Quando i tag vengono distribuiti in modo sincrono, esistono due codici di incorporamento, uno inserito nella `<head>` e un altro che hai messo davanti alla `</body>`).

Dalla schermata Panoramica della proprietà, fai clic su **[!UICONTROL Ambienti]** nella navigazione a sinistra per passare alla pagina degli ambienti. Vi sono già stati creati gli ambienti di sviluppo, staging e produzione.

![Selezione di Ambienti nella navigazione superiore](images/launch-environments.png)

Gli ambienti di sviluppo, staging e produzione corrispondono agli ambienti tipici nel processo di sviluppo e rilascio del codice. Il codice viene scritto per la prima volta dallo sviluppatore in un ambiente di sviluppo. Una volta completato il lavoro, l’utente lo invierà a un ambiente di staging per il QA e ad altri team per la revisione. Una volta effettuato correttamente il QA e quando i team si ritengono soddisfatti, il codice viene quindi pubblicato nell’ambiente di produzione, che è l’ambiente rivolto al pubblico sperimentato dai visitatori quando accedono al sito web.

I tag consentono ulteriori ambienti di sviluppo ed è utile nelle grandi organizzazioni in cui più sviluppatori lavorano contemporaneamente a progetti diversi.

Questi sono gli unici ambienti necessari per completare l’esercitazione. Gli ambienti consentono di disporre di diverse versioni di lavoro delle librerie di tag ospitate su URL diversi, per aggiungere nuove funzioni e renderle disponibili per gli utenti interessati (ad esempio sviluppatori, ingegneri QA, pubblico e così via) al momento giusto.

Ora copiamo il codice da incorporare:

1. Nella riga **[!UICONTROL Sviluppo]**, fai clic sull’icona Installa ![icona Installa](images/launch-installIcon.png) per aprire il modale.

1. I tag verranno impostati per impostazione predefinita sui codici di incorporamento asincroni.

1. Fai clic sull’icona Copia ![icona Copia](images/launch-copyIcon.png) per copiare il codice da incorporare negli Appunti.

1. Fai clic su **[!UICONTROL Chiudi]** per chiudere il modale.

   ![Icona di installazione](images/launch-copyInstallCode.png)

## Implementare il codice di incorporamento nell’`<head>` della pagina HTML di esempio

Il codice di incorporamento deve essere implementato nell’elemento `<head>` di tutte le pagine HTML che condivideranno la proprietà. Potresti avere uno o più file di modello che controllano `<head>` a livello globale nel sito, rendendo più semplice l’aggiunta di tag.

Se non lo hai già fatto, scarica [la pagina HTML di esempio](https://www.enablementadobe.com/multi/web/basic-sample.html) (fai clic con il pulsante destro del mouse su questo collegamento e fai clic su &quot;Salva collegamento con nome&quot;) e aprilo in un editor di codice. [Brackets](https://brackets.io/) è un editor gratuito open source, se necessario.

Sostituisci il codice di incorporamento esistente alla riga 34 o vicino con quello presente negli Appunti e salva la pagina. Ora apri la pagina in un browser web. Se carichi la pagina utilizzando il protocollo `file://`, dovrai aggiungere &quot;https:&quot; all’inizio dell’URL del codice di incorporamento nell’editor di codice). Le linee 33-36 della pagina di esempio possono essere così:

```html
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="https://assets.adobedtm.com/launch-ENa21cfed3f06f4ddf9690de8077b39e81-development.min.js" async></script>
    <!--/Tags Header Embed Code-->
```

Apri gli strumenti di sviluppo del browser web e passa alla scheda Rete. A questo punto, dovresti visualizzare un errore 404 per l’URL dell’ambiente tag:
![Errore 404](images/samplepage-404.png)

L&#39;errore 404 è previsto perché non hai ancora generato una libreria in questo ambiente Tag. Scoprirai come farlo nella lezione successiva. Se compare un messaggio &quot;failed&quot; invece di un errore 404, probabilmente hai dimenticato di aggiungere il protocollo `https://` nel codice di incorporamento. Di nuovo, devi solo specificare il protocollo `https://` solo se si sta cari cando la pagina di esempio utilizzando il protocollo `file://`. Effettua la modifica e ricarica la pagina finché non viene visualizzato l&#39;errore 404.

## Tecniche consigliate per l’implementazione dei tag

Dedichiamo un momento alla revisione di alcune delle best practice di implementazione dei tag, illustrate nella pagina di esempio:

* **Livello dati**:

   * Noi *fortemente* consigliamo di creare un livello di dati sul sito contenente tutti gli attributi necessari per compilare variabili in Analytics, Target e altre soluzioni di marketing. Questa pagina di esempio contiene solo un livello di dati molto semplice, ma un livello dati reale potrebbe contenere ulteriori dettagli sulla pagina, il visitatore, i dettagli del carrello, ecc. Per ulteriori informazioni sui livelli dati, consulta [Customer Experience Digital Data Layer 1.0](https://www.w3.org/2013/12/ceddl-201312.pdf)

   * Definisci il livello dati prima del codice di incorporamento del tag, in modo da massimizzare le operazioni che puoi eseguire con le soluzioni di Experience Cloud.

* **Librerie di supporto JavaScript**: Se disponi già di una libreria come JQuery implementata in `<head>` delle pagine, caricalo prima dei tag per sfruttare la sintassi nei tag e in Target

* **Doctype HTML5**: per Target è necessario il doctype HTML5

* **preconnect e dns-prefetch**: utilizza preconnect e il dns-prefetch per migliorare il tempo di caricamento della pagina. Vedi anche: [https://w3c.github.io/resource-hints/](https://w3c.github.io/resource-hints/)

* **frammento pre-hiding per le implementazioni asincrone di Target**: Per ulteriori informazioni, consulta la lezione di Target , ma quando Target viene distribuito tramite codici di incorporamento tag asincroni, è necessario codificare un frammento pre-hiding sulle pagine prima dei codici di incorporamento tag per gestire lo sfarfallio del contenuto

Di seguito viene riportato un riepilogo delle best practice nell’ordine suggerito. Tieni presente che esistono alcuni segnaposto per i dettagli specifici dell’account:

```html
<!doctype html>
<html lang="en">
<head>
    <title>Basic Demo</title>
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
    <!--prehiding snippet for Adobe Target with asynchronous tags deployment-->
    <script>
        (function(g,b,d,f){(function(a,c,d){if(a){var e=b.createElement("style");e.id=c;e.innerHTML=d;a.appendChild(e)}})(b.getElementsByTagName("head")[0],"at-body-style",d);setTimeout(function(){var a=b.getElementsByTagName("head")[0];if(a){var c=b.getElementById("at-body-style");c&&a.removeChild(c)}},f)})(window,document,"body {opacity: 0 !important}",3E3);
    </script>
    <!--/prehiding snippet for Adobe Target with asynchronous tags deployment-->
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE INSTALL CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Tags Header Embed Code-->
</head>
<body>
    <h1>Tags Basic Demo</h1>
    <p>This is a very simple page to demonstrate basic concepts of tags</p>
</body>
</html>
```

Ora sai come aggiungere il codice di incorporamento tag al tuo sito!

[Avanti &quot;Aggiungere un elemento dati, una regola e una libreria&quot; >](add-data-elements-rules.md)
