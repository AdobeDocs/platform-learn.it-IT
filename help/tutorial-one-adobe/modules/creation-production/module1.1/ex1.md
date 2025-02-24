---
title: Guida introduttiva ai servizi Firefly
description: Scopri come utilizzare Postman e Adobe I/O per eseguire query sulle API dei servizi Adobe Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: c5a80b87ac8e997922cb8c69b4180c4220dd9862
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---

# 1.1.1 Guida introduttiva ai servizi Firefly

Scopri come utilizzare Postman e Adobe I/O per eseguire query sulle API dei servizi Adobe Firefly.

## 1.1.1.1 Prerequisiti

Prima di continuare con questo esercizio, devi aver completato la configurazione di [il tuo progetto Adobe I/O](./../../../modules/getting-started/gettingstarted/ex6.md) e devi anche aver configurato un&#39;applicazione per interagire con le API, ad esempio [Postman](./../../../modules/getting-started/gettingstarted/ex7.md) o [PostBuster](./../../../modules/getting-started/gettingstarted/ex8.md).

## 1.1.1.2 firefly.adobe.com

Vai a [https://firefly.adobe.com](https://firefly.adobe.com). Fai clic sull&#39;icona **profile** e accertati di aver effettuato l&#39;accesso all&#39;account **Account** corretto, che dovrebbe essere `--aepImsOrgName--`. Se necessario, fare clic su **Cambia profilo** per passare a tale account.

![Postman](./images/ffui1.png){zoomable="yes"}

Immettere il prompt `Horses in a field` e fare clic su **Genera**.

![Postman](./images/ffui2.png){zoomable="yes"}

Dovresti vedere qualcosa di simile a questo.

![Postman](./images/ffui3.png){zoomable="yes"}

Apri i **Strumenti per sviluppatori** nel browser.

![Postman](./images/ffui4.png){zoomable="yes"}

Dovresti vedere questo. Passare alla scheda **Rete**.

![Postman](./images/ffui5.png){zoomable="yes"}

Immetti il termine di ricerca **generate**, quindi fai di nuovo clic su **Generate**. Dovresti quindi visualizzare una richiesta denominata **generate-async**. Selezionala e passa a **Payload** dove visualizzerai i dettagli della richiesta.

![Postman](./images/ffui6.png){zoomable="yes"}

La richiesta che visualizzi qui è la richiesta inviata al backend lato server di Firefly Services. Contiene diversi parametri importanti:

- **prompt**: questo è il prompt, che richiede che tipo di immagine deve essere generata da Firefly

- **seed**: in questa richiesta, i seed sono stati generati in modo casuale. Ogni volta che Firefly genera un&#39;immagine, per impostazione predefinita inizia il processo scegliendo un numero casuale denominato valore di inizializzazione. Questo numero casuale contribuisce a rendere univoca ogni immagine, il che è ottimo quando si desidera generare un’ampia varietà di immagini. Tuttavia, in alcuni casi potrebbe essere necessario generare immagini simili tra loro in più richieste. Ad esempio, quando Firefly genera un’immagine che desideri modificare utilizzando le altre opzioni di Firefly (come predefiniti di stile, immagini di riferimento, ecc.), utilizza il valore di inizializzazione di tale immagine nelle richieste HTTP future per limitare la casualità delle immagini future e specifica quello desiderato.

![Postman](./images/ffui7.png){zoomable="yes"}

Dai un’occhiata di nuovo all’interfaccia utente. Modificare le **proporzioni** in **Orizzontale (4:3)**.

![Postman](./images/ffui8.png){zoomable="yes"}

Scorri verso il basso fino a **Effetti**, passa a **Temi** e seleziona un effetto come **Fumetto**.

![Postman](./images/ffui9.png){zoomable="yes"}

Apri di nuovo **Strumenti per sviluppatori** nel browser. Quindi, fare clic su **Genera** ed esaminare la richiesta di rete inviata.

![Postman](./images/ffui10.png){zoomable="yes"}

Quando analizzi i dettagli della richiesta di rete, visualizzerai quanto segue:

- **prompt** non è stato modificato rispetto alla richiesta precedente
- **seed** non sono cambiati rispetto alla richiesta precedente
- **dimensioni** è stato modificato in base alla modifica in **Proporzioni**.
- Sono stati aggiunti **stili** con un riferimento all&#39;effetto **fumetto** selezionato

![Postman](./images/ffui11.png){zoomable="yes"}

Per il prossimo esercizio, dovrai utilizzare uno dei numeri **seed**. Annotare un numero di seed desiderato.

Nell&#39;esercizio successivo, eseguirai operazioni simili con i servizi Firefly, ma in seguito utilizzerai l&#39;API invece dell&#39;interfaccia utente. In questo esempio, il numero di seed è **45781**.

## 1.1.1.3 Adobe I/O - access_token

Nella raccolta **Adobe IO - OAuth**, selezionare la richiesta denominata **POST - Ottieni token di accesso** e selezionare **Invia**. La risposta deve contenere un nuovo **accestoken**.

![Postman](./images/ioauthresp.png){zoomable="yes"}

## API dei servizi Firefly di 1.1.1.4, immagine testo 2

Ora che disponi di un access_token valido e aggiornato, puoi inviare la prima richiesta alle API dei servizi Firefly.

Selezionare la richiesta denominata **POST - Firefly - T2I V3** dalla raccolta **FF - Firefly Services Tech Insiders**.

![Firefly](./images/ff1.png){zoomable="yes"}

Copia l’URL dell’immagine dalla risposta e aprilo nel browser web per visualizzarla.

![Firefly](./images/ff2.png){zoomable="yes"}

Dovresti vedere una bella immagine che rappresenta `horses in a field`.

![Firefly](./images/ff3.png){zoomable="yes"}

Nel **Corpo** della richiesta **POST - Firefly - T2I V3**, aggiungere quanto segue nel campo `"promptBiasingLocaleCode": "en-US"` e sostituire la variabile `XXX` con uno dei numeri di seed utilizzati in modo casuale dall&#39;interfaccia utente di Firefly Services. In questo esempio, il numero **seed** è `45781`.

```json
,
  "seeds": [
    XXX
  ]
```

Fai clic su **Invia**. Verrà quindi inviata una risposta con una nuova immagine generata da Firefly Services. Apri l’immagine per visualizzarla.

![Firefly](./images/ff4.png){zoomable="yes"}

Dovresti quindi visualizzare una nuova immagine con lievi differenze, in base al **seed** utilizzato.

![Firefly](./images/ff5.png){zoomable="yes"}

Quindi, in **Body** della richiesta **POST - Firefly - T2I V3**, incolla l&#39;oggetto **styles** sotto l&#39;oggetto **seed**. Lo stile dell&#39;immagine generata verrà modificato in **fumetto**.

```json
,
  "contentClass": "art",
  "styles": {
    "presets": [
      "comic_book"
    ],
    "strength": 50
  }
```

Dovresti avere questo. Fai clic su **Invia**.

![Firefly](./images/ff6.png){zoomable="yes"}

Fai clic sull’URL dell’immagine per aprirlo.

![Firefly](./images/ff7.png){zoomable="yes"}

L&#39;immagine è cambiata un po&#39;. Quando applicate i predefiniti di stile, l&#39;immagine di partenza non viene più applicata come prima.

![Firefly](./images/ff8.png){zoomable="yes"}

Rimuovi il codice per l&#39;oggetto **seed** dal **Body** della richiesta. Fai clic su **Invia**, quindi fai clic sull&#39;URL dell&#39;immagine che ottieni dalla risposta.

```json
,
  "seeds": [
    XXX
  ]
```

![Firefly](./images/ff9.png){zoomable="yes"}

L&#39;immagine è cambiata di nuovo un po&#39;.

![Firefly](./images/ff10.png){zoomable="yes"}


## API di Firefly Services 1.1.1.5, Gen Expand

Seleziona la richiesta denominata **POST - Firefly - Gen Expand** dalla raccolta **FF - Firefly Services Tech Insiders** e passa al **Body** della richiesta.

- **size**: immettere la risoluzione desiderata. Il valore inserito in questo campo deve essere maggiore delle dimensioni originali dell&#39;immagine e non può essere maggiore di 4096.
- **image.source.url**: questo campo richiede un collegamento all&#39;immagine che deve essere espanso. In questo esempio, viene utilizzata una variabile per fare riferimento all&#39;immagine generata nell&#39;esercizio precedente.

- **allineamento orizzontale**: valori accettati: `"center"`,`"left`, `"right"`.
- **allineamento verticale**: valori accettati: `"center"`,`"top`, `"bottom"`.

![Firefly](./images/ff11.png){zoomable="yes"}

Fai clic sull’URL dell’immagine che fa parte della risposta.

![Firefly](./images/ff12.png){zoomable="yes"}

Ora l&#39;immagine generata nell&#39;esercizio precedente è stata espansa alla risoluzione di 3999x3999.

![Firefly](./images/ff13.png){zoomable="yes"}

Quando modificate l&#39;allineamento del posizionamento, anche l&#39;output sarà leggermente diverso. In questo esempio, il posizionamento viene modificato in **left, bottom**. Fai clic su **Invia** e quindi su per aprire l&#39;URL dell&#39;immagine generata.

![Firefly](./images/ff14.png){zoomable="yes"}

Dovreste quindi vedere che l&#39;immagine originale viene utilizzata in un posizionamento diverso, che influenza l&#39;intera immagine.

![Firefly](./images/ff15.png){zoomable="yes"}

## Passaggi successivi

Vai a [Ottimizza il processo Firefly utilizzando Microsoft Azure e gli URL prefirmati](./ex2.md){target="_blank"}

Torna a [Panoramica dei servizi Adobe Firefly](./firefly-services.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}
