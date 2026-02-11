---
title: Usa il cursore per sviluppare il progetto
description: Usa il cursore per sviluppare il progetto
kt: 5342
doc-type: tutorial
exl-id: c73498b6-5e08-41b5-81a9-c0a76a6e2792
source-git-commit: 25901342e8d9c46b0edce3b2092b9f1d66ba5849
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 0%

---

# 1.7.2 Usare il cursore per sviluppare il progetto

## 1.7.2.1 Configura directory e strumenti

Sul desktop, creare una nuova directory denominata `--aepUserLdap---commerce`

![Commerce e agente](./images/cursorai1.png)

Fai clic con il pulsante destro del mouse sulla cartella e seleziona **Nuovo terminale nella cartella**.

![Commerce e agente](./images/cursorai2.png)

Dovresti vedere questo.

![Commerce e agente](./images/cursorai3.png)

Ora devi clonare un archivio Github esistente, che puoi visualizzare [https://github.com/adobe/commerce-integration-starter-kit](https://github.com/adobe/commerce-integration-starter-kit).

Questo archivio è il kit di avvio per l’integrazione di Adobe che utilizza Adobe Developer App Builder per migliorare l’affidabilità delle connessioni in tempo reale e ridurre il time-to-market per le integrazioni tra Adobe Commerce e altri sistemi di back-office, come ERP, CRM e PIM.

![Commerce e agente](./images/cursorai4.png)

Esistono diversi modi per clonare questo archivio; in questo esempio viene utilizzato Terminal.

Immetti il seguente comando nella finestra del terminale ed eseguilo.

`git clone https://github.com/adobe/commerce-integration-starter-kit`

![Commerce e agente](./images/cursorai5.png)

Dopo un paio di secondi, dovresti vedere questo risultato.

![Commerce e agente](./images/cursorai6.png)

Quindi, passa alla cartella appena creata. Immetti il seguente comando, quindi eseguilo.

`cd commerce-integration-starter-kit`

![Commerce e agente](./images/cursorai7.png)

Dovresti vedere questo.

![Commerce e agente](./images/cursorai8.png)

Successivamente, è necessario impostare gli strumenti di estensibilità Commerce per Cursore. Immetti il seguente comando, quindi eseguilo.

`aio commerce extensibility tools-setup`

![Commerce e agente](./images/cursorai9.png)

Selezionare **Directory corrente**.

![Commerce e agente](./images/cursorai10.png)

Seleziona **Cursore**.

![Commerce e agente](./images/cursorai11.png)

Seleziona **npm**.

![Commerce e agente](./images/cursorai12.png)

Dopo un paio di minuti, dovresti vederlo.

![Commerce e agente](./images/cursorai13.png)

Installando gli strumenti di estensibilità di Commerce per Cursor, ora è disponibile un server MCP come parte dell’ambiente Cursor. Negli esercizi successivi, utilizzerai il server MCP per sviluppare e distribuire il progetto App Builder.

## 1.7.2.2 Configura il tuo webhook

Per questo esercizio, avrai bisogno di un webhook che deve essere configurato in modo che, quando viene creato un ordine, l’evento dell’ordine possa essere inviato in streaming a tale webhook. In questo esercizio utilizzerai un endpoint di esempio utilizzando [https://pipedream.com/requestbin](https://pipedream.com/requestbin).

Vai a [https://pipedream.com/requestbin](https://pipedream.com/requestbin), crea un account e quindi crea un&#39;area di lavoro. Una volta creata l’area di lavoro, verrà visualizzato qualcosa di simile a questo.

Fai clic su **copia** per copiare l&#39;URL. Nel prossimo esercizio dovrai specificare questo URL. L&#39;URL in questo esempio è `https://eodts05snjmjz67.m.pipedream.net`.

![Cursore + Commerce](./images/webhook1.png)

## 1.7.2.3 Crea app con cursore

Apri cursore. Fai clic su **Apri progetto**.

![Cursore + Commerce](./images/cursorai14.png)

Passare alla cartella creata, che deve essere denominata `--aepUserLdap---commerce`. In tale cartella selezionare la cartella denominata `commerce-integration-starter-kit`. Fai clic su **Apri**.

![Cursore + Commerce](./images/cursorai15.png)

Dovresti vedere questo. Prima di continuare, verificare che la cartella di primo livello aperta in Cursor sia `commerce-integration-starter-kit`.

![Cursore + Commerce](./images/cursorai16.png)

Utilizzare la scelta rapida da tastiera `Cmd + Shift + J` per aprire le impostazioni del cursore. Dovresti vedere questo. Vai a **Strumenti e MCP**.

![Cursore + Commerce](./images/cursorai17.png)

Abilita il server MCP **commerce-extensibility**. Al termine, fare clic su **X** per chiudere la finestra.

![Cursore + Commerce](./images/cursorai18.png)

Copiate il seguente prompt e incollatelo in Cursore. Quindi fare clic sul pulsante **invia**.

`I would like to build an app that subscribes to order created events and sends them to a configurable URL with basic authentication`

![Cursore + Commerce](./images/cursorai19.png)

Il cursore inizierà a ragionare ed eseguire. Il cursore ti chiederà di confermare un paio di volte. In questo caso, fare clic su **Esegui**. Questo può accadere 5-10 volte, a seconda del ragionamento e delle impostazioni.

![Cursore + Commerce](./images/cursorai20.png)

Dopo un paio di minuti, dovresti vedere qualcosa del genere.

![Cursore + Commerce](./images/cursorai21.png)

Come indicato da Cursore, il passaggio successivo consiste nel creare un file con il nome `.env` e fornire le variabili richieste.

## 1.7.2.4 Crea il file.env

Selezionare il file **env.dist**. Immettere il comando `Cmd + C`, quindi immettere il comando `Cmd + V`.

![Cursore + Commerce](./images/cursorai22.png)

Rinomina il file appena creato in `.env`.

![Cursore + Commerce](./images/cursorai23.png)

È quindi necessario fornire i valori per tutte le variabili nel file **.env**.

![Cursore + Commerce](./images/cursorai24.png)

Qui puoi trovare tutte le informazioni richieste.

### Endpoint Commerce

Puoi trovare queste variabili da [https://experience.adobe.com](https://experience.adobe.com). Fare clic su **Commerce**.

![Cursore + Commerce](./images/cursorai25.png)

Dovresti vedere questo. Fai clic sull&#39;icona **informazioni** accanto all&#39;ambiente ACS, che deve essere denominato `--aepUserLdap-- - ACCS`. Copia i valori dell’endpoint REST e dell’endpoint GraphQL.

In questo esempio, questi sono i valori da copiare. Incollali accanto alle variabili seguenti nel file **.env** alle righe 6 e 7.


- **COMMERCE_BASE_URL** = https://na1-sandbox.api.commerce.adobe.com/Lkp3U7tvTBNAmpFvwnZJ4B/
- **COMMERCE_GRAPHQL_ENDPOINT** = https://na1-sandbox.api.commerce.adobe.com/Lkp3U7tvTBNAmpFvwnZJ4B/graphql

![Cursore + Commerce](./images/cursorai26.png)

Dovresti quindi averlo nel file **.env**.

![Cursore + Commerce](./images/cursorai26a.png)

### Variabili del progetto Adobe I/O

Puoi trovare queste variabili da [https://developer.adobe.com/console](https://developer.adobe.com/console). Vai a **Progetti** e fai clic per aprire il progetto Adobe I/O creato nell&#39;esercizio precedente, che deve essere denominato `--aepUserLdap-- Commerce Events`.

![Cursore + Commerce](./images/cursorai27.png)

Vai a **Produzione**.

![Cursore + Commerce](./images/cursorai28.png)

Vai a **Server-to-Server OAuth**. Dovresti vedere questo.

![Cursore + Commerce](./images/cursorai29.png)

Copia i valori dei campi **ID client**, **Segreto client**, **ID account tecnico**, **E-mail account tecnico** e **ID organizzazione** e incollali accanto alle variabili seguenti nel file **.env** alle righe 13-17.

- **OAUTH_CLIENT_ID**= **ID client**
- **OAUTH_CLIENT_SECRET**= **Segreto client**
- **OAUTH_TECHNICAL_ACCOUNT_ID**= **ID account tecnico**
- **OAUTH_TECHNICAL_ACCOUNT_EMAIL**= **E-mail account tecnico**
- **OAUTH_ORG_ID**= **ID organizzazione**

Dovresti quindi averlo nel file **.env**.

![Cursore + Commerce](./images/cursorai29a.png)

### COMMERCE_ADOBE_IO_EVENTS_MERCHANT_ID

Per il campo **COMMERCE_ADOBE_IO_EVENTS_MERCHANT_ID=**, immettere il valore `--aepUserLdap--_commerce_events` alla riga 34 nel file **.env**.

Dovresti quindi averlo nel file **.env**.

![Cursore + Commerce](./images/cursorai30.png)

### Configurazioni Workspace

Per recuperare queste variabili, torna al tuo progetto Adobe I/O e fai clic su **Panoramica di Workspace**.

Dopo aver visitato la **panoramica di Workspace**, controlla l&#39;URL con questo aspetto: **https://developer.adobe.com/console/projects/133309/4566206088345586770/workspaces/4566206088345619105/details**.

Il primo numero di questo esempio, 133309, è il valore da utilizzare per il campo **IO_CONSUMER_ID**.
Il secondo numero di questo esempio, 4566206088345586770, è il valore da utilizzare per il campo **IO_PROJECT_ID**.
Il terzo numero in questo esempio, 4566206088345619105, è il valore da utilizzare per il campo **IO_WORKSPACE_ID**.

![Cursore + Commerce](./images/cursorai31.png)

- **IO_CONSUMER_ID**= 133309
- **IO_PROJECT_ID**= 4566206088345586770
- **IO_WORKSPACE_ID**= 4566206088345619105

Copiare questi valori e incollarli accanto alle variabili seguenti nel file **.env** alle righe 42-44.

![Cursore + Commerce](./images/cursorai32.png)

### EVENT_PREFIX

Per il campo **EVENT_PREFIX =**, immettere il valore `--aepUserLdap--_` alla riga 47 nel file **.env**.

Dovresti quindi averlo nel file **.env**.

![Cursore + Commerce](./images/cursorai33.png)

### Webhook

Per il campo **ORDER_WEBHOOK_URL**, è necessario incollare l&#39;URL del webhook creato in precedenza in questo esercizio, che dovrebbe essere simile al seguente: `https://eodts05snjmjz67.m.pipedream.net`.

Dovresti quindi averlo nel file **.env**.

![Cursore + Commerce](./images/cursorai34.png)

### Credenziali di App Builder

È necessario aggiornare le seguenti variabili nel file **.env** alle righe 54-55:

- **AIO_RUNTIME_NAMESPACE**=
- **AIO_RUNTIME_AUTH**=

Puoi recuperare i valori per queste variabili tornando al tuo progetto Adobe I/O. Vai a **Panoramica di Workspace** e fai clic su **Scarica tutto**.

![Cursore + Commerce](./images/cursorai35.png)

Un file come questo verrà quindi scaricato. Apri il file utilizzando un editor di testo.

![Cursore + Commerce](./images/cursorai36.png)

Scorri verso destra fino a visualizzare **runtime**. Dovresti quindi visualizzare il campo **name**, che contiene il valore per **AIO_RUNTIME_NAMESPACE**.

![Cursore + Commerce](./images/cursorai37.png)

Scorri verso destra fino a visualizzare **auth**, che contiene il valore per **AIO_RUNTIME_AUTH**.

![Cursore + Commerce](./images/cursorai38.png)

Incollare entrambi i valori nel file **.env** alle righe 54-55.

![Cursore + Commerce](./images/cursorai39.png)

Il file **.env** è ora completamente configurato.

## 1.7.2.5 workspace.json

Nel passaggio precedente hai scaricato un file come questo dal progetto Adobe I/O.

![Cursore + Commerce](./images/cursorai36.png)

Rinominare il file e utilizzare il nome `workspace.json`.

![Cursore + Commerce](./images/cursorai40.png)

Copia il file nella directory **scripts**>**onboarding**>**config**.

![Cursore + Commerce](./images/cursorai41.png)

## Accesso a 1.7.2.6 Adobe I/O

Tornare alla finestra del terminale utilizzata in precedenza. Immettere il comando `aio login`.

![Cursore + Commerce](./images/cursorai44.png)

Dovresti visualizzarlo dopo aver effettuato l’accesso tramite il browser.

![Cursore + Commerce](./images/cursorai45.png)

## 1.7.2.7 Pronto per la distribuzione

Copiate il seguente prompt e incollatelo in Cursore. Quindi fare clic sul pulsante **invia**.

`Please deploy this code to Adobe I/O`

![Cursore + Commerce](./images/cursorai42.png)

Fai clic su **Esegui** per consentire l&#39;azione. Il cursore potrebbe richiedere più volte di confermare un&#39;azione.

![Cursore + Commerce](./images/cursorai43.png)

L’implementazione terminerà dopo un paio di minuti.

![Cursore + Commerce](./images/cursorai46.png)

Copiate il seguente prompt e incollatelo in Cursore. Quindi fare clic sul pulsante **invia**.

`run the onboarding to commerce`

![Cursore + Commerce](./images/cursorai50.png)

Dopo un paio di minuti, dovresti vederlo.

![Cursore + Commerce](./images/cursorai51.png)

Copiate il seguente prompt e incollatelo in Cursore. Quindi fare clic sul pulsante **invia**.

`subscribe to commerce events`

![Cursore + Commerce](./images/cursorai47.png)

Dopo un paio di minuti, dovresti vederlo.

![Cursore + Commerce](./images/cursorai49.png)

## 1.7.2.8 Verifica la configurazione in Adobe Commerce as a Cloud Service

Vai a [https://experience.adobe.com](https://experience.adobe.com). Fare clic su **Commerce**.

![Cursore + Commerce](./images/cursorai60.png)

Fai clic sul tuo ambiente Adobe Commerce as a Cloud Service per aprirlo e quindi accedere.

![Cursore + Commerce](./images/cursorai61.png)

Vai a **Sistema** e quindi a **Sottoscrizioni eventi**.

![Cursore + Commerce](./images/cursorai62.png)

Dovresti quindi visualizzare questo elenco di abbonamenti agli eventi.

![Cursore + Commerce](./images/cursorai63.png)

Vai a **Archivi** e quindi a **Configurazione**.

![Cursore + Commerce](./images/cursorai64.png)

Vai a **Adobe Services** e seleziona **Adobe I/O Events**. Dovresti quindi notare che il campo **Configurazione Workspace di Adobe I/O** ha un valore di un paio di asterischi e il campo **ID esercente** deve avere anche un valore come `--aepUserLdap--_commerce_events`.

![Cursore + Commerce](./images/cursorai65.png)

Dopo aver impostato questa configurazione, puoi testarla.

## 1.7.2.9 Verifica lo scenario

Apri il tuo sito web.

![Cursore + Commerce](./images/cursorai101.png)

Vai a **Orologi** e fai clic su qualsiasi prodotto.

![Cursore + Commerce](./images/cursorai102.png)

Configura il prodotto e fai clic su **Aggiungi al carrello**.

![Cursore + Commerce](./images/cursorai103.png)

Fai clic sull&#39;icona **Carrello** e seleziona **Estrai**.

![Cursore + Commerce](./images/cursorai104.png)

Compila i tuoi dettagli e fai clic su **Ordina**.

![Cursore + Commerce](./images/cursorai105.png)

Dovresti quindi vedere una conferma dell’ordine.

![Cursore + Commerce](./images/cursorai106.png)

Passa all’applicazione webhook. Ora dovresti vedere un evento in arrivo per l’ordine appena confermato.

![Cursore + Commerce](./images/cursorai107.png)

## Debug di Adobe I/O 1.7.2.10

Torna al progetto Adobe I/O. Vai a **Panoramica di Workspace**. Dovresti vedere qualcosa di simile a questo. Scorri verso il basso un po&#39;.

![Cursore + Commerce](./images/cursorai108.png)

Fare clic per aprire **Commerce Order Sync**.

![Cursore + Commerce](./images/cursorai109.png)

Vai a **Analisi debug**. Qui puoi trovare gli ultimi eventi in arrivo e il relativo payload. È utile per capire quali eventi sono stati elaborati e se sono stati elaborati correttamente.

![Cursore + Commerce](./images/cursorai110.png)

## Passaggi successivi

Torna a [Strumenti per sviluppatori intelligenti per Adobe Commerce](./aiassisteddev.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}
