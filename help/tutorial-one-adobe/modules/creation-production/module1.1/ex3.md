---
title: Utilizzo delle API di Photoshop
description: Scopri come utilizzare le API di Photoshop e Firefly Services
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 60eecc24-1713-4fec-9ffa-a3186db1a8ca
source-git-commit: 2dd9c43bbf348805fe6c271d92b3db51fd25ca6f
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 0%

---

# 1.1.3 Utilizzo delle API di Photoshop

Scopri come utilizzare le API di Photoshop e Firefly Services.

## 1.1.3.1 Prerequisiti

Prima di continuare con questo esercizio, devi aver completato la configurazione di [il tuo progetto Adobe I/O](./../../../modules/getting-started/gettingstarted/ex6.md) e devi anche aver configurato un&#39;applicazione per interagire con le API, ad esempio [Postman](./../../../modules/getting-started/gettingstarted/ex7.md) o [PostBuster](./../../../modules/getting-started/gettingstarted/ex8.md).

## 1.1.3.2 Adobe I/O - access_token

Nella raccolta **Adobe IO - OAuth**, selezionare la richiesta denominata **POST - Ottieni token di accesso** e selezionare **Invia**. La risposta deve contenere un nuovo **accestoken**.

![Postman](./images/ioauthresp.png)

## 1.1.3.3 interagisce a livello di programmazione con un file PSD

Scarica [citisignal-fiber.psd](./../../../assets/ff/citisignal-fiber.psd){target="_blank"} sul desktop.

Apri **citisignal-fiber.psd** in Photoshop.

![Archiviazione Azure](./images/ps7.png)

Nel riquadro **Livelli**, l&#39;autore del file ha assegnato un nome univoco a ogni livello. Potete visualizzare le informazioni sui livelli aprendo il file PSD in Photoshop, ma potete anche farlo a livello di programmazione.

Inviiamo la tua prima richiesta API alle API di Photoshop.

### API Photoshop - Hello World

Ora, supponiamo di salutare le API di Photoshop per verificare se tutte le autorizzazioni e l’accesso sono impostati correttamente.

Nella raccolta **Photoshop**, apri la richiesta **Photoshop Hello (autenticazione test).**. Seleziona **Invia**.

![Archiviazione Azure](./images/ps10.png)

Dovresti ricevere la risposta **Benvenuto nell&#39;API Photoshop!**.

![Archiviazione Azure](./images/ps11.png)

Quindi, per interagire a livello di programmazione con il file PSD **citisignal-fiber.psd**, devi caricarlo nel tuo account di archiviazione. Puoi farlo manualmente trascinandolo nel contenitore utilizzando Azure Storage Explorer, ma questa volta dovresti farlo tramite l’API.

### Carica PSD in Azure

In Postman, apri la richiesta **Carica PSD nell&#39;account di archiviazione Azure**. Nell’esercizio precedente, hai configurato queste variabili di ambiente in Postman, che utilizzerai ora:

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Come è possibile vedere nella richiesta **Carica PSD nell&#39;account di archiviazione Azure**, l&#39;URL è configurato per utilizzare queste variabili.

![Archiviazione Azure](./images/ps12.png)

In **Body**, selezionare il file **citisignal-fiber.psd**.

![Archiviazione Azure](./images/ps13.png)

Lo schermo dovrebbe essere simile al seguente. Seleziona **Invia**.

![Archiviazione Azure](./images/ps14.png)

È necessario ottenere questa risposta vuota da Azure, il che significa che il file è archiviato nel contenitore nell’account di archiviazione di Azure.

![Archiviazione Azure](./images/ps15.png)

Se utilizzi Azure Storage Explorer per esaminare il file, assicurati di aggiornare la cartella.

![Archiviazione Azure](./images/ps16.png)

### API Photoshop - Ottieni manifesto

Successivamente, devi ottenere il file manifesto del tuo file PSD.

In Postman aprire la richiesta **Photoshop - Ottieni manifesto PSD**. Vai a **Corpo**.

Il corpo deve essere simile al seguente:

```json
  {
    "inputs": [
      {
        "storage": "external",
        "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
      }
    ],
    "options": {
      "thumbnails": {
        "type": "image/jpeg"
      }
    }
  }
```

Seleziona **Invia**.

Nella risposta viene visualizzato un collegamento. Poiché il completamento delle operazioni in Photoshop a volte può richiedere un po’ di tempo, Photoshop fornisce un file di stato come risposta alla maggior parte delle richieste in arrivo. Per capire cosa sta succedendo con la tua richiesta, devi leggere il file di stato.

![Archiviazione Azure](./images/ps17.png)

Per leggere il file di stato, aprire la richiesta **Photoshop - Ottieni stato PS**. È possibile vedere che questa richiesta utilizza una variabile come URL, che è una variabile impostata dalla richiesta precedente inviata, **Photoshop - Ottieni manifesto PSD**. Le variabili sono impostate negli **Script** di ogni richiesta. Seleziona **Invia**.

![Archiviazione Azure](./images/ps18.png)

Lo schermo dovrebbe essere simile al seguente. Attualmente, lo stato è impostato su **in sospeso**, il che significa che il processo non è ancora completato.

![Archiviazione Azure](./images/ps19.png)

Selezionare invia altre volte in **Photoshop - Ottieni stato PS**, fino a quando lo stato non cambia in **completato**. L&#39;operazione potrebbe richiedere alcuni minuti.

Quando la risposta è disponibile, puoi vedere che il file json contiene informazioni su tutti i livelli del file PSD. Si tratta di informazioni utili, in quanto è possibile identificare elementi come il nome o l’ID del livello.

![Archiviazione Azure](./images/ps20.png)

Ad esempio, cercare il testo `2048x2048-cta`. Lo schermo dovrebbe essere simile al seguente:

![Archiviazione Azure](./images/ps21.png)


### API Photoshop - Sostituzione SmartObject

Successivamente, devi modificare lo sfondo del file citisignal-fibre.psd utilizzando l’immagine generata con Firefly in uno degli esercizi precedenti.

In Postman, apri la richiesta **Photoshop - SmartObject Replace** e passa a **Body**.

Lo schermo dovrebbe essere simile al seguente:

- viene innanzitutto specificato un file di input: `citisignal-fiber.psd`
- in secondo luogo, viene specificato il livello da modificare, con il nuovo file di sfondo da utilizzare
- terzo, è specificato un file di output: `citisignal-fiber-replacedbg.psd`

```json
  {
    "inputs": [
        {
            "storage": "azure",
            "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
        }
    ],
    "options": {
        "layers": [
            {
                "name": "2048x2048-image",
                "input": {
                    "href": "{{FIREFLY_COMPLETED_ASSET_URL}}",
                    "storage": "external"
                }
            }
        ]
    },
    "outputs": [
        {
            "storage": "azure",
            "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber-replacedbg.psd{{AZURE_STORAGE_SAS_WRITE}}",
            "type": "vnd.adobe.photoshop",
            "overwrite": true
        }
    ]
}
```

Il nome del file di output è diverso, in quanto non si desidera ignorare il file di input originale.

Seleziona **Invia**.

![Archiviazione Azure](./images/psbg23.png)

Proprio come prima, la risposta contiene un collegamento che punta al file di stato che tiene traccia dell’avanzamento.

![Archiviazione Azure](./images/psbg22.png)

Per leggere il file di stato, apri la richiesta **Photoshop - Ottieni stato PS** e seleziona **Invia**. Se lo stato non è impostato su **completato** immediatamente, attendere alcuni secondi e selezionare di nuovo **Invia**.

Seleziona l’URL per scaricare il file di output.

![Archiviazione Azure](./images/psbg24.png)

Apri **citisignal-fiber-replacedbg.psd** dopo aver scaricato il file sul computer. Dovresti notare che l&#39;immagine di sfondo è stata modificata in un&#39;immagine simile a quella riportata di seguito:

![Archiviazione Azure](./images/psbg25.png)

Puoi anche visualizzare questo file nel contenitore utilizzando Azure Storage Explorer.

![Archiviazione Azure](./images/psbg26.png)

### API Photoshop - Modifica testo

Successivamente, devi modificare il testo per call to action utilizzando le API.

In Postman, apri la richiesta **Photoshop - Cambia testo** e passa a **Corpo**.

Lo schermo dovrebbe essere simile al seguente:

- viene innanzitutto specificato un file di input: `citisignal-fiber-replacedbg.psd`, ovvero il file generato nel passaggio precedente quando è stata modificata l&#39;immagine di sfondo
- in secondo luogo, viene specificato il livello da modificare, con il testo da modificare in
- terzo, è specificato un file di output: `citisignal-fiber-changed-text.psd`

```json
  {
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber-replacedbg.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "layers": [
      {
        "name": "2048x2048-cta",
        "text": {
          "content": "Get Fiber now!"
        }
      }
    ]
  },
  "outputs": [
    {
      "storage": "azure",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
      "type": "vnd.adobe.photoshop",
      "overwrite": true
    }
  ]
}
```

Il nome del file di output è diverso, in quanto non si desidera ignorare il file di input originale.

Seleziona **Invia**.

![Archiviazione Azure](./images/ps23.png)

Proprio come prima, la risposta contiene un collegamento che punta al file di stato che tiene traccia dell’avanzamento.

![Archiviazione Azure](./images/ps22.png)

Per leggere il file di stato, apri la richiesta **Photoshop - Ottieni stato PS** e seleziona **Invia**. Se lo stato non è impostato su **completato** immediatamente, attendere alcuni secondi e selezionare di nuovo **Invia**.

Seleziona l’URL per scaricare il file di output.

![Archiviazione Azure](./images/ps24.png)

Apri **citisignal-fiber-changed-text.psd** dopo aver scaricato il file sul computer. Dovresti vedere che il segnaposto per call to action è stato sostituito dal testo **Get Fiber now!**.

![Archiviazione Azure](./images/ps25.png)

Puoi anche visualizzare questo file nel contenitore utilizzando Azure Storage Explorer.

![Archiviazione Azure](./images/ps26.png)

## Passaggi successivi

Vai a [API modelli personalizzati Firefly](./ex4.md){target="_blank"}

Torna a [Panoramica di Adobe Firefly Services](./firefly-services.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}