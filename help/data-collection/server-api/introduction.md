---
title: Introduzione di base alle API
description: Introduzione alle interfacce di programmazione delle applicazioni
activity: understand
doc-type: article
feature-set: Experience Platform
feature: Server API,API,Data Collection,Integrations
level: Beginner
role: User,Developer
solution: Data Collection
topic: Integrations
exl-id: 9607e641-b0d5-49c1-b319-32ed0720e715
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 0%

---

# API 101 - Introduzione di base alle API

API sta per Interfaccia di programmazione applicazioni. Significa solo ciò che dice: ci sono interfacce tra i programmi e queste interfacce permettono a questi programmi di comunicare. Quando i programmatori sviluppano applicazioni software, spesso hanno bisogno del loro software per comunicare con altri software o hardware. L’API definisce cosa, come, quando, dove e perché per tali comunicazioni e interazioni.

Le API sono un modo per risolvere i problemi aziendali con il software. Nella maggior parte delle aziende, questo è uno sforzo collaborativo. La collaborazione è sempre più semplice grazie a una comprensione condivisa di termini, concetti e passaggi chiave.

Se pensi di fare clic su un collegamento in una pagina web, il browser utilizza alcune API quando fai clic sul collegamento. Il browser riconosce il clic, effettua la richiesta per la pagina da visitare, recupera la pagina su Internet e la visualizza sullo schermo. Ci sono molti passaggi intermedi più piccoli, ma il tuo browser è un software che comunica e interagisce con una varietà di API solo per mostrarti una pagina web. In questo articolo presenteremo termini, concetti e passaggi importanti per l’utilizzo o la discussione delle API.

Entro la fine di questo articolo si dovrebbe avere una chiara comprensione di questi termini fondamentali, concetti e passaggi. La documentazione sulle API può essere estesa e le discussioni sull’utilizzo delle API per affrontare casi d’uso specifici possono essere molto dettagliate. La navigazione nella documentazione e la discussione delle API è più semplice e produttiva grazie a elementi di base chiari e a una comprensione condivisa.

>[!NOTE]
>
> Sebbene siano disponibili molte API, qui l’attenzione si concentrerà sulle API web e browser: fondamentalmente, quando un&#39;applicazione software interagisce con un&#39;altra tramite Internet.

## Termini e concetti dell’API

Cosa significa una parola o una frase, e come posso pensarla in modo semplice e semplice? In un’API, la parte &quot;applicazione&quot; significa un’applicazione software o un programma. La parte &quot;interfaccia di programmazione&quot; si riferisce a come e dove un&#39;applicazione interagisce con un&#39;altra applicazione per determinati scopi. Nel nostro esempio di pagina web, quando fai clic su un collegamento, il browser invia una richiesta a un server per la pagina web.

![Immagine del collegamento ipertestuale con l’URL di destinazione](../assets/api101-link-destination.png)

In questa schermata il cursore del mouse passa sopra il collegamento Adobe Experience Platform. In basso c&#39;è la barra di stato del browser web che mostra l&#39;&quot;indirizzo&quot; della pagina che il browser otterrà. In altre parole, cliccando il link Adobe Experience Platform dice al browser di &quot;ottenere quella pagina per me in modo che io possa vedere qui sul mio schermo&quot;.

Quando fai clic su un collegamento, il browser invia una richiesta a un server per ottenere una pagina. Questa è una `GET` , uno dei metodi di richiesta comunemente utilizzati con API web. Una cosa che il browser deve soddisfare la richiesta è la pagina &quot;indirizzo&quot; - dov&#39;è sul web?

### Parti di un URL

![Barra degli indirizzi del browser con URL](../assets/api101-address-bar.png)

La maggior parte dei browser dispone di una &quot;barra degli indirizzi&quot; che mostra alcuni o tutti gli &quot;indirizzi&quot; di una pagina web. Quando il browser &quot;ottiene&quot; la pagina per il collegamento che abbiamo fatto clic, visualizza l&#39;&quot;indirizzo&quot; della pagina in questa barra degli indirizzi. Quindi qual è l&#39;&quot;indirizzo&quot; di una pagina web?

che `https://business.adobe.com/products/experience-platform/adobe-experience-platform.html` qui sopra è l&#39;indirizzo di una pagina sul web, e si chiama URL o Uniform Resource Locator. Gli URL possono fare riferimento a una pagina come questa o un file di immagine, un video o altri tipi di file.

![Parti di un URL](../assets/api101-url-parts.jpg)

Questo indirizzo, l’URL, ha parti specifiche che sono molto rilevanti per le API web e browser.

**Schema**

La `scheme` sopra è anche chiamato `protocol` con API web e in genere `http` o `https`. HTTP o HyperText Transfer Protocol è il modo in cui risorse come le pagine web vengono trasferite da un server web a un browser web. HTTPS è la versione sicura, in cui il trasferimento avviene su Internet utilizzando una sicurezza destinata a evitare interferenze con la risorsa che si sta trasferendo. È comune visualizzare una piccola icona di blocco nella barra degli indirizzi del browser quando si visualizza una pagina su HTTPS.

Per le API web, i trasferimenti di queste risorse avvengono tramite richieste HTTP, ovvero tramite richieste HTTP.

**Host e domini**

La `business.adobe.com` è l&#39;host della risorsa richiesta. Quando fai clic sul nostro collegamento di esempio, il browser utilizza questa parte dell’URL per trovare il server in cui è ospitata la pagina. Non è sempre esattamente lo stesso del server web, ma a un livello base possiamo pensare che sia il server in cui il browser otterrà la pagina che abbiamo richiesto.

I nomi di dominio fanno parte del sistema dei nomi di dominio, meglio noto come DNS. La maggior parte delle persone pensa `adobe.com` o `example.com` come &quot;nome di dominio&quot;, ma sono presenti parti rilevanti per le API. `www.adobe.com` e `business.adobe.com` possono essere chiamati nomi di dominio, ma `www.` e `business.` le parti sono denominate sottodomini. Le API interagiscono spesso con un URL che include un sottodominio come `api.example.com` o `sub.www.example.com`.

È molto comune vedere il termine _host_ fai riferimento a un nome di dominio completo, compresi eventuali sottodomini come `business.adobe.com`. È anche comune vedere i termini _dominio_ o _nome di dominio_ quando si fa riferimento a un host senza il sottodominio come `adobe.com`. Memorizzare i termini specifici per ogni parte e variazione di un host non è importante in questo caso. Tuttavia, è importante essere consapevoli del fatto che questi termini sono comunemente utilizzati, in modo da poter chiarire tutte le specifiche rilevanti per la tua attività e le tue discussioni.

**Origin**

L’origine è un altro termine da considerare, strettamente correlato alle parti di un URL. A livello di base, un&#39;origine è approssimativamente il `scheme` più `host` più `domain` like `https://business.adobe.com`. Valori diversi spesso rappresentano origini diverse come `https://business.adobe.com` e `http://business.adobe.com` non hanno la stessa origine perché hanno regimi diversi. `https://www.adobe.com` e `https://business.adobe.com` Inoltre, non sono della stessa origine in molti usi a causa dei diversi sottodomini.

**Path**

L’ultimo bit nell’esempio URL precedente è il `path` alla risorsa: la pagina nel nostro esempio. La `/products/experience-platform/` in genere rappresenta cartelle o directory sul server web. Proprio come abbiamo cartelle o directory sui nostri computer per documenti e foto, abbiamo anche cartelle sui server web per organizzare i contenuti. Infine, la `/adobe-experience-platform.html` parte è il nome del file, la pagina web.

Ci sono altre parti più dettagliate di un URL che saranno evidenziate nella parte successiva di questa serie.

### API di terze parti

Le API web sono talvolta denominate API di terze parti. Pensateci come le parti coinvolte in una transazione. Nel nostro esempio di collegamento, tu, o più nello specifico il tuo browser, sei la prima parte nella richiesta per la pagina. Il server web è di seconda parte. Dov&#39;è il terzo?

In una pagina web è comune includere contenuti o risorse provenienti da altri host o origini. In questi casi, quando il browser inizia a visualizzare la pagina, effettua un altro set di richieste a quegli altri host, o &quot;terze parti&quot;, che ospitano tali risorse. Ciò è molto comune, soprattutto per contenuti multimediali come video o immagini, ma anche per dati che devono essere aggiornati al momento della visualizzazione o dell’utilizzo. Ottenere l’ora attuale, il tempo corrente o un messaggio di benvenuto personalizzato per una persona specifica è un esempio in cui un’API di terze parti può fornire la risorsa giusta al momento giusto. È comune che tali richieste provengano da queste API di terze parti.

## Utilizzi comuni per le API web

A parte l’ora del giorno, il tempo o i contenuti personalizzati, sono disponibili molti utilizzi per le API web. Le piattaforme di social media come Twitter, TikTok, Facebook, LinkedIn, Snapchat, Pinterest e altri hanno una varietà di API che i programmatori possono utilizzare con le loro applicazioni. E naturalmente, anche l&#39;Adobe ha [un&#39;ampia varietà di API](https://developer.adobe.com/apis) che i programmatori utilizzano in modo che il loro software possa interagire con i prodotti e i servizi di Adobe. I prodotti e i servizi software accedono ad altri prodotti e servizi software attraverso queste API.

## API di esempio

Le API del browser consentono ai programmatori di interagire direttamente con le funzioni del browser. L&#39;API della batteria consente al software di controllare lo stato della batteria di un dispositivo in modo che possa avvertire se necessario. L’API Appunti consente al software di copiare o incollare gli appunti del dispositivo. L’API a schermo intero consente al software di presentare l’opzione per espandere la visualizzazione a schermo intero del dispositivo, come YouTube.

Adobe Experience Platform Data Access API è un’API web che consente ai programmatori di accedere e scaricare file di set di dati da Adobe Experience Platform in modo che possano utilizzare i dati del profilo del cliente nei propri programmi. È molto comune che API come questa facciano parte di un processo di automazione del software in cui il software è programmato per eseguire una sequenza di passaggi utilizzando diverse API in combinazione. Spesso si tratta di un notevole risparmio sui costi rispetto all&#39;esecuzione manuale degli stessi passaggi.

## Endpoint API

Quando i programmatori &quot;utilizzano&quot; un browser o un&#39;API web nei loro programmi, in genere fanno richieste di invio o ricezione di risorse, come il nostro esempio browser che richiede una pagina web. La documentazione API elenca spesso gli &quot;endpoint&quot; per tali richieste, ad esempio: `https://platform.adobe.io/data/foundation/export/files/{dataSetFileId}`. Questo è il pattern specifico o &quot;endpoint&quot; dell’API di accesso ai dati di Platform che un programmatore utilizzerà per ottenere un file di set di dati.

La `{dataSetFileId}` circondato da queste parentesi graffe rappresenta un valore che il programmatore deve inviare nella richiesta. Quindi l’URL nella richiesta API effettiva assomiglierebbe a qualcosa `https://platform.adobe.io/data/foundation/export/files/xyz123brb` se `xyz123brb` deve essere un ID valido del file di set di dati che il programmatore desidera ricevere.

In altre parole, proprio come il browser ottiene una pagina a un URL specifico, le richieste API ottengono risorse da un endpoint specifico come questo esempio di set di dati o inviano risorse a esso.

## Metodi di richiesta HTTP

A questo punto, dovrebbe essere chiaro che le API web effettuano richieste per risorse come pagine web o set di dati. Come la maggior parte dei concetti software, queste richieste HTTP seguono pattern ripetibili. Una richiesta viene inviata da un&#39;applicazione software a un&#39;altra applicazione software che valuta la richiesta e quindi risponde: il browser richiede una pagina da un server web e risponde con il contenuto della pagina.

L&#39;intero processo dalla richiesta alla risposta comporta molti passaggi più piccoli e molto dettagliati, ma i metodi di richiesta sono semplici. I metodi di richiesta definiscono l’operazione richiesta.

**`GET`**

La `GET` il metodo di richiesta viene utilizzato quando si richiede una risposta che fornisce una risorsa, come la nostra pagina web e gli esempi di set di dati. Quando si fa clic su un collegamento in un browser o si tocca un collegamento su un dispositivo mobile, viene creato un `GET` richiesta dietro le quinte.

**`POST`**

La `POST` invia i dati con la richiesta. Può sembrare strano che una &quot;richiesta&quot; invii dati, ma l&#39;idea è che fare la richiesta API sta chiedendo all&#39;endpoint, il software ricevente, di accettare la richiesta, e nel caso di un `POST`, per accettare anche i dati inviati. I dati inviati vengono generalmente scritti in un archivio dati come un database o un file, in modo che possano essere salvati.

**`PUT`**

La `PUT` il metodo di richiesta è simile a `POST` poiché invia dati, ma se i dati inviati esistono già nell’endpoint, un `PUT` aggiorna i dati esistenti sostituendoli. A `POST` non aggiorna, invia semplicemente, quindi più `POST` le richieste possono creare più record dei dati inviati, anziché aggiornare qualsiasi record esistente.

**`PATCH`**

La `PATCH` metodo di richiesta viene utilizzato per inviare dati che aggiornano parte di un record esistente, come quando modifichiamo il nostro indirizzo aggiornando il nostro profilo account. Con un `POST` può essere creato un profilo aggiuntivo e con un `PUT`, è possibile sostituire il profilo esistente, ma utilizzando `PATCH` metodo semplicemente aggiorniamo la parte pertinente del record esistente, come il nostro indirizzo.

**`DELETE`**

La `DELETE` il metodo request rimuove una risorsa specificata nella richiesta, ad esempio se si fa clic su un collegamento per eliminare completamente il profilo del nostro account.

Ce ne sono diversi altri, ma si tratta di un elenco dei metodi più comuni quando si lavora con le API.

### Esempio di richiesta

Ora che conosci i termini, i concetti e i passaggi di base relativi alle API, nella pratica puoi esaminare una richiesta API di esempio.

La pagina del nostro esempio del browser ha un URL di `https://business.adobe.com/products/experience-platform/adobe-experience-platform.html`. Quando fai clic sul collegamento Adobe Experience Platform, il browser crea un `GET` richiesta per questa pagina. Dal momento che abbiamo il browser per fare il lavoro per noi, tutto quello che dobbiamo fare è fare clic, ma se un programmatore vuole che la richiesta avvenga in un&#39;applicazione software, deve fornire tutti i dettagli necessari per il corretto soddisfacimento della richiesta API.

Ecco come potrebbe apparire nel codice:

```js
fetch(
  "https://business.adobe.com/products/experience-platform/adobe-experience-platform.html",
  {
    headers: {
      accept:
        "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
      "accept-language": "en-US,en;q=0.9",
      "sec-ch-ua":
        '" Not A;Brand";v="99", "Chromium";v="101", "Microsoft Edge";v="101"',
      "sec-fetch-dest": "document",
      "sec-fetch-mode": "navigate",
      "sec-fetch-site": "none",
      "sec-fetch-user": "?1",
      "upgrade-insecure-requests": "1",
    },
    referrerPolicy: "strict-origin-when-cross-origin",
    body: null,
    method: "GET",
    mode: "cors",
    credentials: "include",
  }
);
```

Nel codice riportato sopra, puoi vedere la `URL` il browser richiede e verso il basso è `method: "GET"` metodo di richiesta. Anche le altre linee di codice sono parte della richiesta, ma sono al di fuori dell&#39;ambito di applicazione di questo articolo.


*[API]: Interfaccia di programmazione delle applicazioni *[URL]: Uniform Resource Locator *[HTTP]: Protocollo di trasferimento HyperText *[DNS]: Sistema dei nomi di dominio
