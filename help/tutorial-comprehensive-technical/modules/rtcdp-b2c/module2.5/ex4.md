---
title: 'Raccolta dati e inoltro lato server in tempo reale: creazione e configurazione di una funzione cloud di Google'
description: Creare e configurare una funzione cloud di Google
kt: 5342
doc-type: tutorial
exl-id: ee73ce3a-baaa-432a-9626-249be9aaeff2
source-git-commit: 7779e249b4ca03c243cf522811cd81370002d51a
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 1%

---

# 2.5.4 Inoltra gli eventi a GCP Pub/Sub

>[!NOTE]
>
>Per questo esercizio, devi accedere a un ambiente della piattaforma Google Cloud. Se non hai ancora accesso a GCP, crea un nuovo account utilizzando il tuo indirizzo e-mail personale.

## Crea il tuo argomento Google Cloud Pub/Sub

Vai a [https://console.cloud.google.com/](https://console.cloud.google.com/). Nella barra di ricerca immettere `pub/sub`. Fai clic sul risultato della ricerca **Pub/Sub - Messaggistica globale in tempo reale**.

![GCP](./images/gcp1.png)

Poi vedrai questo. Fare clic su **CREA ARGOMENTO**.

![GCP](./images/gcp2.png)

Poi vedrai questo. Per il tuo ID argomento, usa `--aepUserLdap---event-forwarding`. Fai clic su **Crea**.

![GCP](./images/gcp6.png)

L&#39;argomento è stato creato. Fare clic sul **ID sottoscrizione** dell&#39;argomento.

![GCP](./images/gcp7.png)

Poi vedrai questo. Copia il **Nome argomento** negli Appunti e archivialo, come ti servirà nei prossimi esercizi.

![GCP](./images/gcp8.png)

Passiamo ora all’inoltro degli eventi di raccolta dati di Adobe Experience Platform, per aggiornare la proprietà di inoltro degli eventi in modo da avviare l’inoltro degli eventi a Pub/Sub.


## Aggiorna la proprietà di Inoltro eventi: Secrets

**I segreti** nelle proprietà di Inoltro eventi vengono utilizzati per memorizzare le credenziali che verranno utilizzate per l&#39;autenticazione in base alle API esterne. In questo esempio, devi configurare un segreto per memorizzare il token OAuth di Google Cloud Platform, che verrà utilizzato per l’autenticazione quando si utilizza Pub/Sub per lo streaming dei dati verso GCP.

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/) e vai a **Segreti**. Fai clic su **Crea nuovo segreto**.

![SSF raccolta dati Adobe Experience Platform](./images/secret1.png)

Poi vedrai questo. Seguire queste istruzioni:

- Nome: utilizzare `--aepUserLdap---gcp-secret`
- Ambiente di destinazione: seleziona **Sviluppo**
- Tipo: **Google OAuth 2**
- Seleziona la casella di controllo per **Pub/Sub**

Fai clic su **Crea segreto**.

![SSF raccolta dati Adobe Experience Platform](./images/secret2.png)

Dopo aver fatto clic su **Crea segreto**, verrà visualizzata una finestra a comparsa per impostare l&#39;autenticazione tra il segreto della proprietà di Inoltro eventi e Google. Fai clic su **Crea e autorizza segreto `--aepUserLdap---gcp-secret` con Google**.

![SSF raccolta dati Adobe Experience Platform](./images/secret3.png)

Fai clic su per selezionare il tuo account Google.

![SSF raccolta dati Adobe Experience Platform](./images/secret4.png)

Fai clic su **Continua**.

>[!NOTE]
>
>Il messaggio popup può variare. Autorizzare/consentire l’accesso richiesto per continuare con l’esercizio.

![SSF raccolta dati Adobe Experience Platform](./images/secret5.png)

Dopo l’autenticazione, visualizzerai questo messaggio.

![SSF raccolta dati Adobe Experience Platform](./images/secret6.png)

Il segreto è ora configurato correttamente e può essere utilizzato in un elemento dati.

## Aggiorna la proprietà di Inoltro eventi: Elemento dati

Per utilizzare il segreto nella proprietà Inoltro eventi, è necessario creare un elemento dati in cui venga memorizzato il valore del segreto.

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/) e vai a **Inoltro eventi**. Cerca nella proprietà Inoltro eventi e fai clic su di essa per aprirla.

![SSF raccolta dati Adobe Experience Platform](./images/prop1.png)

Nel menu a sinistra, vai a **Elementi dati**. Fare clic su **Aggiungi elemento dati**.

![SSF raccolta dati Adobe Experience Platform](./images/de1gcp.png)

Configura l’elemento dati in questo modo:

- Nome: **Segreto GCP**
- Estensione: **Core**
- Tipo di elemento dati: **Segreto**
- Segreto di sviluppo: selezionare il segreto creato, denominato `--aepUserLdap---gcp-secret`

Fai clic su **Salva**

![SSF raccolta dati Adobe Experience Platform](./images/secret7.png)

## Aggiorna la proprietà di Inoltro eventi: Extension

Con il segreto e l’elemento dati configurati, ora puoi impostare l’estensione per Google Cloud Platform nella proprietà Inoltro eventi.

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/), vai a **Inoltro eventi** e apri la tua proprietà Inoltro eventi.

![SSF raccolta dati Adobe Experience Platform](./images/prop1.png)

Quindi, vai a **Estensioni**, a **Catalogo**. Fai clic sull&#39;estensione **Google Cloud Platform** e fai clic su **Installa**.

![SSF raccolta dati Adobe Experience Platform](./images/gext2.png)

Poi vedrai questo. Fai clic sull’icona Elemento dati.

![SSF raccolta dati Adobe Experience Platform](./images/gext3.png)

Selezionare l&#39;elemento dati creato nell&#39;esercizio precedente, denominato **Segreto GCP**. Fai clic su **Seleziona**.

![SSF raccolta dati Adobe Experience Platform](./images/gext4.png)

Poi vedrai questo. Fai clic su **Salva**.

![SSF raccolta dati Adobe Experience Platform](./images/gext5.png)

## Aggiornare la proprietà di inoltro degli eventi: Aggiornare una regola

Ora che l’estensione Google Cloud Platform è configurata, puoi definire una regola per iniziare a inoltrare i dati dell’evento all’argomento Pub/Sub. A tale scopo, è necessario aggiornare la regola **Tutte le pagine** creata in uno degli esercizi precedenti.

Nel menu a sinistra, vai a **Regole**. Nell&#39;esercizio precedente hai creato la regola **Tutte le pagine**. Fai clic su quella regola per aprirla.

![SSF raccolta dati Adobe Experience Platform](./images/rl1gcp.png)

Allora questo lo farai. Fai clic sull&#39;icona **+** in **Azioni** per aggiungere una nuova azione.

![SSF raccolta dati Adobe Experience Platform](./images/rl2gcp.png)

Poi vedrai questo. Effettua la seguente selezione:

- Seleziona l&#39;**estensione**: **Google Cloud Platform**.
- Seleziona **Tipo azione**: **Invia dati a Cloud Pub/Sub**.

Questo dovrebbe darti **Nome**: **Piattaforma Google Cloud - Invia dati a Cloud Pub/Sub**. Ora dovresti vedere:

![SSF raccolta dati Adobe Experience Platform](./images/rl5gcp.png)

Ora è necessario configurare l’argomento Pub/Sub creato in precedenza.

Puoi trovare il **Nome argomento** qui, copialo.

![GCP](./images/gcp8.png)

Incolla **Nome argomento** nella configurazione regola. Fare clic sull&#39;icona Elemento dati accanto al campo **Dati (obbligatorio)**.

![SSF raccolta dati Adobe Experience Platform](./images/rl6gcp.png)

Seleziona **Evento XDM** e fai clic su **Seleziona**.

![SSF raccolta dati Adobe Experience Platform](./images/rl7gcp.png)

Poi vedrai questo. Fai clic su **Mantieni modifiche**.

![SSF raccolta dati Adobe Experience Platform](./images/rl8gcp.png)

Fai clic su **Salva**.

![SSF raccolta dati Adobe Experience Platform](./images/rl9gcp.png)

Poi vedrai questo.

![SSF raccolta dati Adobe Experience Platform](./images/rl10gcp.png)

## Pubblicare le modifiche

La configurazione è terminata. Vai a **Flusso di pubblicazione** per pubblicare le modifiche. Apri la libreria di sviluppo **Principale** facendo clic su **Modifica** come indicato.

![SSF raccolta dati Adobe Experience Platform](./images/rl12gcp.png)

Fai clic sul pulsante **Aggiungi tutte le risorse modificate**, dopo di che la regola e l&#39;elemento dati verranno visualizzati in questa libreria. Fare clic su **Salva e genera per sviluppo**. Le modifiche sono ora in fase di implementazione.

![SSF raccolta dati Adobe Experience Platform](./images/rl13gcp.png)

Dopo un paio di minuti, vedrai che l’implementazione è completata e pronta per essere testata.

![SSF raccolta dati Adobe Experience Platform](./images/rl14.png)

## Verifica la configurazione

Vai a [https://dsn.adobe.com](https://dsn.adobe.com). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sui tre punti **...** del progetto del sito Web, quindi fai clic su **Esegui** per aprirlo.

![DSN](./../../datacollection/module1.1/images/web8.png)

Poi vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Incolla l’URL del sito web demo, che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l’accesso con il tuo Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Seleziona il tipo di account e completa la procedura di accesso.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Vedrai quindi il tuo sito web caricato in una finestra del browser in incognito. Per ogni esercizio, dovrai utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Passa al tuo Google Cloud Pub/Sub e passa a **MESSAGES**. Fai clic su **PULL** e dopo un paio di secondi verranno visualizzati alcuni messaggi nell&#39;elenco. Fai clic su un messaggio per visualizzarne il contenuto.

![Configurazione raccolta dati di Adobe Experience Platform](./images/hook3gcp.png)

Ora puoi visualizzare il payload XDM dell’evento in Google Pub/Sub. Hai inviato correttamente i dati raccolti dalla raccolta dati di Adobe Experience Platform, in tempo reale, a un endpoint Google Cloud Pub/Sub. Da lì, tali dati possono essere utilizzati da qualsiasi applicazione Google Cloud Platform, ad esempio BigQuery per l’archiviazione e il reporting o per casi di utilizzo di apprendimento automatico.

![Configurazione raccolta dati di Adobe Experience Platform](./images/hook4gcp.png)

Passaggio successivo: [2.5.5 Inoltra gli eventi ad AWS Kinesis e AWS S3](./ex5.md)

[Torna al modulo 2.5](./aep-data-collection-ssf.md)

[Torna a tutti i moduli](./../../../overview.md)
