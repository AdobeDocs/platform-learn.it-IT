---
title: Guida introduttiva ai servizi di Firefly
description: Guida introduttiva ai servizi di Firefly
kt: 5342
doc-type: tutorial
exl-id: 60eecc24-1713-4fec-9ffa-a3186db1a8ca
source-git-commit: 0fe4bbf6bcc80d4fa88bc30718a1de6621f93f17
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 1%

---

# 1.1.3 Adobe Firefly e Adobe Photoshop

## 1.1.3.1 Aggiornare l’integrazione dell’Adobe I/O

Vai a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/projects).

![Adobe I/O di nuova integrazione](./images/iohome.png)

Vai a **Progetti** e fai clic per aprire il progetto creato nell&#39;esercizio precedente, che si chiama `--aepUserLdap-- Firefly`.

![Archiviazione Azure](./images/ps1.png)

Fare clic su **+ Aggiungi al progetto** e quindi su **API**.

![Archiviazione Azure](./images/ps2.png)

Selezionare **Creative Cloud** e fare clic su **Photoshop - Servizi di Firefly**. Fai clic su **Avanti**.

![Archiviazione Azure](./images/ps3.png)

Fai clic su **Avanti**.

![Archiviazione Azure](./images/ps4.png)

Successivamente, devi selezionare un profilo di prodotto che definirà quali autorizzazioni sono disponibili per questa integrazione.

Selezionare il profilo **Configurazione predefinita servizi di Firefly** e **Configurazione predefinita servizi di automazione Creative Cloud**.

Fare clic su **Salva API configurata**.

![Archiviazione Azure](./images/ps5.png)

Il progetto di Adobe I/O è stato aggiornato per funzionare con le API di Photoshop e Firefly Services.

![Archiviazione Azure](./images/ps6.png)

## 1.1.3.2 Interagire a livello di programmazione con un file PSD

Scarica il file Vai a [citisignal-fibre.psd](./../../../assets/ff/citisignal-fiber.psd) sul desktop.

Apri il file **citisignal-fiber.psd** in Photoshop. Dovresti avere questo.

![Archiviazione Azure](./images/ps7.png)

Nel riquadro **Livelli** verrà visualizzato che l&#39;autore del file ha assegnato un nome univoco a ogni livello. Potete visualizzare le informazioni sui livelli aprendo il file PSD in Photoshop, ma potete anche farlo a livello di programmazione.

Inviiamo la tua prima richiesta API alle API di Photoshop.

Passa a Postman. Prima di inviare le richieste API a Photoshop, devi eseguire l’autenticazione in Adobe I/O. Esegui la richiesta utilizzata in precedenza con il nome **POST - Ottieni token di accesso**.

Vai a **Parametri** e verifica che il parametro **Ambito** sia impostato correttamente. Il valore **Value** per l&#39;ambito **Scope** deve essere simile al seguente:

`openid,session,AdobeID,read_organizations,additional_info.projectedProductContext, ff_apis, firefly_api`

Quindi fare clic su **Invia**.

![Archiviazione Azure](./images/ps8.png)

Quindi disponi di un token di accesso valido per interagire con le API di Photoshop.

![Archiviazione Azure](./images/ps9.png)

Ora, supponiamo di salutare le API di Photoshop per verificare se tutte le autorizzazioni e l’accesso sono impostati correttamente. Nella raccolta **Photoshop**, apri la richiesta con il nome **Photoshop Hello (Test Auth).**. Fai clic su **Invia**.

![Archiviazione Azure](./images/ps10.png)

Dovresti quindi ricevere questa risposta: **Benvenuto nell&#39;API Photoshop!**.

![Archiviazione Azure](./images/ps11.png)

Quindi, per interagire a livello di programmazione con il file PSD **citisignal-fiber.psd**, devi caricarlo nel tuo account di archiviazione. Puoi farlo manualmente trascinandolo nel contenitore utilizzando Azure Storage Explorer, ma questa volta devi farlo tramite l’API.

In Postman, apri la richiesta **Carica PSD nell&#39;account di archiviazione Azure**. Nell’esercizio precedente, hai configurato queste variabili di ambiente in Postman, che ora utilizzerai:

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Come è possibile vedere nella richiesta **Carica PSD nell&#39;account di archiviazione Azure**, l&#39;URL è configurato per utilizzare queste variabili.

![Archiviazione Azure](./images/ps12.png)

In **Body**, aggiungere il file **citisignal-fiber.psd**.

![Archiviazione Azure](./images/ps13.png)

Dovresti avere questo. Fai clic su **Invia**.

![Archiviazione Azure](./images/ps14.png)

Dovresti quindi ottenere questa risposta vuota da Azure, il che significa che il file è archiviato nel contenitore nell’account di archiviazione Azure.

![Archiviazione Azure](./images/ps15.png)

Se si utilizza Esplora archivi di Azure per avere un&#39;occhiata, il file verrà visualizzato dopo l&#39;aggiornamento della cartella.

![Archiviazione Azure](./images/ps16.png)

Successivamente, devi ottenere il file manifesto del file PSD. In Postman, apri la richiesta **Photoshop - Get PSD Manifest**. Vai a **Corpo**.

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

Fai clic su **Invia**.

Nella risposta viene visualizzato un collegamento. Poiché il completamento delle operazioni in Photoshop a volte può richiedere un po’ di tempo, Photoshop fornirà un file di stato come risposta alla maggior parte delle richieste in arrivo. Per capire cosa sta succedendo con la tua richiesta, devi leggere il file di stato.

![Archiviazione Azure](./images/ps17.png)

Per leggere il file di stato, aprire la richiesta **Photoshop - Ottieni stato PS**. Viene quindi visualizzato che questa richiesta utilizza una variabile come URL, che è una variabile impostata dalla richiesta precedente inviata, **Photoshop - Ottieni manifesto PSD**. Le variabili sono impostate negli **Script** di ogni richiesta.

Fai clic su **Invia**.

![Archiviazione Azure](./images/ps18.png)

Dovresti vedere questo. Attualmente, lo stato è impostato su **in sospeso**, il che significa che il processo non è ancora completato.

![Archiviazione Azure](./images/ps19.png)

Puoi fare clic su Invia altre volte nella richiesta **Photoshop - Ottieni stato PS**, fino a quando lo stato non cambia in **completato**. L&#39;operazione potrebbe richiedere alcuni minuti.

Quando la risposta è disponibile, viene visualizzato un file json contenente informazioni su tutti i livelli del file PSD. Si tratta di informazioni utili, in quanto qui è possibile visualizzare elementi come il nome o l’ID del livello.

![Archiviazione Azure](./images/ps20.png)

Ad esempio, cercare il testo `2048x2048-cta`. Dovresti vedere questo.

![Archiviazione Azure](./images/ps21.png)

Ora devi modificare il testo per l’invito all’azione utilizzando le API. In Postman, apri la richiesta **Photoshop - Cambia testo** e passa a **Corpo**.

Dovresti vedere questo. È possibile vedere che:

- viene innanzitutto specificato un file di input: `citisignal-fiber.psd`
- in secondo luogo, viene specificato il livello da modificare, con il testo da modificare in
- terzo, è specificato un file di output: `citisignal-fiber-changed-text.psd`

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
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

Il file di output ha un nome diverso, in quanto non si desidera sovrascrivere il file di input originale.

Fai clic su **Invia**.

![Archiviazione Azure](./images/ps23.png)

Proprio come prima, la risposta contiene un collegamento che punta al file di stato che tiene traccia dell’avanzamento.

![Archiviazione Azure](./images/ps22.png)

Per leggere il file di stato, apri di nuovo la richiesta **Photoshop - Ottieni stato PS** e fai clic su **Invia**. Se lo stato non è impostato su **completato** immediatamente, attendere qualche secondo e quindi fare di nuovo clic su **Invia**.

Una volta impostato lo stato su **riuscito**, dovresti vedere questo. Nel percorso `outputs[0]._links.renditions[0].href` dovrebbe essere visualizzato l&#39;URL del file di output creato da Photoshop e contenente il testo modificato.

Fai clic sull’URL per scaricare il file di output.

![Archiviazione Azure](./images/ps24.png)

Il file **citisignal-fiber-changed-text.psd** verrà quindi scaricato nel computer, dopodiché potrai aprirlo. Dovresti quindi vedere che il segnaposto per l&#39;invito all&#39;azione è stato sostituito dal testo **Get Fiber now!**.

![Archiviazione Azure](./images/ps25.png)

Infine, il file viene visualizzato anche nel contenitore utilizzando Azure Storage Explorer.

![Archiviazione Azure](./images/ps26.png)

Hai completato l&#39;esercizio.

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 1.1](./firefly-services.md)

[Torna a tutti i moduli](./../../../overview.md)
