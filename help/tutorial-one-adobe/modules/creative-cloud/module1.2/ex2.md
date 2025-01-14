---
title: Guida introduttiva ai servizi di Firefly
description: Guida introduttiva ai servizi di Firefly
kt: 5342
doc-type: tutorial
exl-id: 23ebf8b4-3f16-474c-afe1-520d88331417
source-git-commit: a0c16a47372d322a7931578adca30a246b537183
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 2%

---

# 1.2.2 Utilizzare le API di Adobe in Workfront Fusion

## 1.2.2.1 Utilizzare l’API Testo Firefly per immagine con Workfront Fusion

Passa il puntatore del mouse sul secondo nodo **Imposta più variabili** e fai clic su **+** per aggiungere un altro modulo.

![WF Fusion](./images/wffusion48.png)

Cerca **http**, quindi seleziona **HTTP**.

![WF Fusion](./images/wffusion49.png)

Seleziona **Crea una richiesta**.

![WF Fusion](./images/wffusion50.png)

Seleziona queste variabili:

- **URL**: `https://firefly-api.adobe.io/v3/images/generate`
- **Metodo**: `POST`

Fai clic su **Aggiungi un&#39;intestazione**.

![WF Fusion](./images/wffusion51.png)

Inserisci le seguenti intestazioni:

| Chiave | Valore |
|:-------------:| :---------------:| 
| `x-api-key` | la variabile archiviata per `CONST_client_id` |
| `Authorization` | `Bearer ` + la variabile archiviata per `bearer_token` |
| `Content-Type` | `application/json` |
| `Accept` | `*/*` |

Immettere i dettagli per `x-api-key`. Fai clic su **Aggiungi**.

![WF Fusion](./images/wffusion52.png)

Fai clic su **Aggiungi un&#39;intestazione**.

![WF Fusion](./images/wffusion53.png)

Immettere i dettagli per `Authorization`. Fai clic su **Aggiungi**.

![WF Fusion](./images/wffusion54.png)

Fai clic su **Aggiungi un&#39;intestazione**. Immettere i dettagli per `Content-Type`. Fai clic su **Aggiungi**.

![WF Fusion](./images/wffusion541.png)

Fai clic su **Aggiungi un&#39;intestazione**. Immettere i dettagli per `Accept`. Fai clic su **Aggiungi**.

![WF Fusion](./images/wffusion542.png)

Imposta **Body type** su **Raw**. Per **Tipo di contenuto**, selezionare **JSON (application/json)**.

![WF Fusion](./images/wffusion55.png)

Incolla questo payload nel campo **Contenuto richiesta**.

```json
{
  "numVariations": 1,
  "size": {
    "width": 2048,
    "height": 2048
  },
  "prompt": "Horses in a field",
  "promptBiasingLocaleCode": "en-US"
}
```

Seleziona la casella di controllo per **Analisi risposta**. Fai clic su **OK**.

![WF Fusion](./images/wffusion56.png)

Fare clic su **Esegui una volta**.

![WF Fusion](./images/wffusion57.png)

Una volta eseguito lo scenario, dovresti visualizzarlo.

![WF Fusion](./images/wffusion58.png)

Fare clic su **?Icona** sul quarto nodo HTTP per visualizzare la risposta. Dovresti trovare un file di immagine nella risposta.

![WF Fusion](./images/wffusion59.png)

Copia l’URL dell’immagine e aprilo in una finestra del browser. Dovresti vedere qualcosa di simile a questo:

![WF Fusion](./images/wffusion60.png)

Fare clic con il pulsante destro del mouse sull&#39;oggetto **HTTP** e rinominarlo in **Firefly T2I**.

![WF Fusion](./images/wffusion62.png)

Fai clic su **Salva** per salvare le modifiche.

![WF Fusion](./images/wffusion61.png)

## 1.2.2.2 Utilizzare l’API Photoshop con Workfront Fusion

Fai clic sull&#39;icona **chiave inglese** tra i nodi **Imposta token Bearer** e **Firefly T2I**. Selezionare **Aggiungi un router**.

![WF Fusion](./images/wffusion63.png)

Fare clic con il pulsante destro del mouse sull&#39;oggetto **Firefly T2I** e selezionare **Clone**.

![WF Fusion](./images/wffusion64.png)

Trascina e rilascia l&#39;oggetto clonato in prossimità dell&#39;oggetto **Router**, che si connetterà automaticamente al **Router**. Dovresti avere questo.

![WF Fusion](./images/wffusion65.png)

È ora disponibile una copia identica basata sulla richiesta HTTP di **Firefly T2I**. Alcune impostazioni della richiesta HTTP **Firefly T2I** sono simili a quelle necessarie per interagire con l&#39;**API Photoshop**, che consente di risparmiare tempo. Ora devi solo modificare le variabili che non sono uguali, come l’URL della richiesta e il payload.

Cambia **URL** in `https://image.adobe.io/pie/psdService/text`.

![WF Fusion](./images/wffusion66.png)

Sostituisci il **contenuto richiesta** con il seguente payload:

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/sevoi-psd.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "layers": [
      {
        "name": "2048x2048-button",
        "text": {
          "content": "Click here"
        }
      },
      {
        "name": "2048x2048-cta",
        "text": {
          "content": "Buy this stuff"
        }
      }
    ]
  },
  "outputs": [
    {
      "storage": "azure",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/sevoi-psd-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
      "type": "vnd.adobe.photoshop",
      "overwrite": true
    }
  ]
}
```

![WF Fusion](./images/wffusion67.png)

Per il corretto funzionamento di **Richiedi contenuto**, mancano alcune variabili:

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Torna al primo nodo, fai clic su **Inizializza costanti**, quindi seleziona **Aggiungi elemento** per ciascuna di queste variabili.

![WF Fusion](./images/wffusion69.png)

| Chiave | Esempio di valore |
|:-------------:| :---------------:| 
| `AZURE_STORAGE_URL` | `https://vangeluw.blob.core.windows.net` |
| `AZURE_STORAGE_CONTAINER` | `vangeluw` |
| `AZURE_STORAGE_SAS_READ` | `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D` |
| `AZURE_STORAGE_SAS_WRITE` | `?sv=2023-01-03&st=2025-01-13T17%3A21%3A09Z&se=2025-01-14T17%3A21%3A09Z&sr=c&sp=racwl&sig=FD4m0YyyqUj%2B5T8YyTFJDi55RiTDC9xKtLTgW0CShps%3D` |

Puoi trovare le variabili tornando a Postman e aprendo **Variabili di ambiente**.

![Archiviazione Azure](./../module1.1/images/az105.png)

Copiate questi valori in Workfront Fusion e aggiungete un nuovo elemento per ciascuna di queste 4 variabili.

Dovresti avere questo. Fai clic su **OK**.

![WF Fusion](./images/wffusion68.png)

Quindi, torna alla richiesta HTTP clonata per aggiornare il **contenuto della richiesta**. Noterai queste variabili nere nel **Contenuto richiesta**, che sono le variabili copiate da Postman. È ora necessario modificare queste variabili nelle appena definite in Workfront Fusion. Sostituire ciascuna variabile con una eliminando il testo nero e sostituendolo con la variabile corretta.

![WF Fusion](./images/wffusion70.png)

Nella sezione **input** è necessario apportare 3 modifiche.

![WF Fusion](./images/wffusion71.png)

Nella sezione **output** sono inoltre disponibili 3 modifiche da apportare. Fai clic su **OK**.

![WF Fusion](./images/wffusion72.png)

Fare clic con il pulsante destro del mouse sul nodo clonato e selezionare **Rinomina**. Cambia il nome in **Testo modifica Photoshop**.

![WF Fusion](./images/wffusion73.png)

Dovresti avere questo.

![WF Fusion](./images/wffusion74.png)

Passaggio successivo: [1.2.3 ...](./ex3.md)

[Torna al modulo 1.2](./automation.md)

[Torna a tutti i moduli](./../../../overview.md)
