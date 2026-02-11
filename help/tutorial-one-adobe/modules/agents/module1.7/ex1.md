---
title: Configurazione dell’ambiente di sviluppo
description: Configurazione dell’ambiente di sviluppo
kt: 5342
doc-type: tutorial
exl-id: c9bfb327-362f-4475-89da-8e9788940d56
source-git-commit: 25901342e8d9c46b0edce3b2092b9f1d66ba5849
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# 1.7.1 Configurazione dell’ambiente di sviluppo

## 1.7.1.1 Crea il tuo progetto Adobe I/O

Vai a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/projects){target="_blank"}.

Assicurati di selezionare l’istanza corretta nell’angolo in alto a destra dello schermo. L&#39;istanza è `--aepImsOrgName--`.

>[!NOTE]
>
> La schermata seguente mostra un’organizzazione specifica selezionata. Durante l’esercitazione, è molto probabile che il nome dell’organizzazione sia diverso. Quando ti sei iscritto a questo tutorial, ti sono stati forniti i dettagli dell’ambiente da utilizzare, segui queste istruzioni.

Quindi, seleziona **Crea progetto da modello**.

![Estendibilità GSPeM](./images/commerceagent1.png)

Seleziona **App Builder**.

![Estendibilità GSPeM](./images/commerceagent2.png)

Immettere il nome `--aepUserLdap-- Commerce Events`. Fai clic su **Salva**.

![Estendibilità GSPeM](./images/commerceagent4.png)

Dovresti vedere qualcosa del genere.

![Estendibilità GSPeM](./images/commerceagent5.png)

Fare clic su **+ Aggiungi servizio** e quindi selezionare **API**.

![Estendibilità GSPeM](./images/commerceagent6.png)

Cerca e seleziona l&#39;API **Eventi di I/O**. Fai clic su **Avanti**.

![Estendibilità GSPeM](./images/commerceagent7.png)

Modificare il nome delle credenziali in `vangeluw Commerce Events - Production`. Fai clic su **Salva API configurata**.

![Estendibilità GSPeM](./images/commerceagent8.png)

Dovresti vedere questo. Fare clic su **+ Aggiungi servizio** e quindi selezionare **API**.

![Estendibilità GSPeM](./images/commerceagent9.png)

Cerca e seleziona l&#39;API **API di gestione I/O**. Fai clic su **Avanti**.

![Estendibilità GSPeM](./images/commerceagent10.png)

Fai clic su **Salva API configurata**.

![Estendibilità GSPeM](./images/commerceagent11.png)

Dovresti vedere questo. Fare clic su **+ Aggiungi servizio** e quindi selezionare **API**.

![Estendibilità GSPeM](./images/commerceagent12.png)

Cerca e seleziona l&#39;API **Adobe Commerce as a Cloud Service**. Fai clic su **Avanti**.

![Estendibilità GSPeM](./images/commerceagent13.png)

Selezionare **Autenticazione da server a server**. Fai clic su **Avanti**.

![Estendibilità GSPeM](./images/commerceagent14.png)

Fai clic su **Avanti**.

![Estendibilità GSPeM](./images/commerceagent15.png)

Selezionare **Predefinito - Cloud Manager**. Fai clic su **Salva API configurata**.

![Estendibilità GSPeM](./images/commerceagent16.png)

Dovresti vedere questo. Fare clic su **+ Aggiungi servizio** e quindi selezionare **API**.

![Estendibilità GSPeM](./images/commerceagent17.png)

Cerca e seleziona l&#39;API **Adobe I/O Events per Adobe Commerce**. Fai clic su **Avanti**.

![Estendibilità GSPeM](./images/commerceagent18.png)

Fai clic su **Salva API configurata**.

![Estendibilità GSPeM](./images/commerceagent19.png)

Il progetto è ora configurato e può essere utilizzato.

![Estendibilità GSPeM](./images/commerceagent20.png)

## 1.7.1.2 Configurare l&#39;ambiente di sviluppo

Per creare, inviare e distribuire l’app estensibile, nell’ambiente di sviluppo locale del computer devono essere installati le applicazioni e i pacchetti seguenti:

- Node.js (versione 20.x o successiva)
- npm (in pacchetto con Node.js)
- Interfaccia della riga di comando (CLI) di Adobe Developer

Se queste applicazioni o pacchetti non sono ancora installati nel computer, eseguire la procedura seguente.

### Node.js e npm

Vai a [https://nodejs.org/en/download](https://nodejs.org/en/download). Dovresti visualizzare questo messaggio, con una serie di comandi terminali che devono essere eseguiti per poter installare Node.js e npm. I comandi mostrati di seguito sono applicabili a MacBook.

![Estendibilità GSPeM](./images/commerceagent21.png)

Aprire innanzitutto una nuova finestra del terminale. Incolla ed esegui il comando indicato nella riga 2 della schermata:

`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash`

Quindi, esegui il comando sulla riga 5 nella schermata:

`\. "$HOME/.nvm/nvm.sh"`

Dopo aver eseguito entrambi i comandi correttamente, eseguire il comando seguente:

`node -v`

Dovresti trovare un numero di versione da restituire.

![Estendibilità GSPeM](./images/commerceagent22.png)

Eseguire quindi il comando seguente:

`npm -v`

Se NPM non è ancora installato, è possibile installarlo utilizzando il comando seguente: `npm install -g npm@11.9.0`.

Dovresti trovare un numero di versione da restituire.

![Estendibilità GSPeM](./images/commerceagent23.png)

Se gli ultimi 2 comandi hanno restituito un numero di versione, la configurazione di queste 2 funzionalità ha esito positivo.

### Interfaccia della riga di comando (CLI) di Adobe Developer

Per installare l’interfaccia della riga di comando (CLI) di Adobe Developer, esegui il seguente comando in una finestra del terminale:

`npm install -g @adobe/aio-cli`

L&#39;esecuzione di questo comando potrebbe richiedere alcuni minuti. Il risultato finale dovrebbe essere simile al seguente:

![Estendibilità GSPeM](./images/commerceagent24.png)

Anche l&#39;interfaccia della riga di comando (CLI) di Adobe Developer è stata installata correttamente.

### Estensione Adobe Developer CLI (Command-Line Interface) SDK per Commerce

Per installare l’estensione Adobe I/O SDK per Commerce, esegui il seguente comando in una finestra del terminale:

`npm install @adobe/aio-commerce-sdk`

![Estendibilità GSPeM](./images/commerceagent25.png)

### Plug-in di Adobe Commerce per Adobe I/O CLI

Per installare i plug-in di Adobe Commerce per Adobe I/O CLI, esegui il seguente comando in una finestra del terminale:

`aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime`

![Estendibilità GSPeM](./images/commerceagent26.png)

Ora hai impostato gli elementi di base per poter eseguire un progetto App Builder, in combinazione con Adobe Commerce, Adobe I/O Events e Adobe I/O Runtime.

## Passaggi successivi

Vai a [Usa il cursore per sviluppare il progetto](./ex2.md){target="_blank"}

Torna a [Strumenti per sviluppatori intelligenti per Adobe Commerce](./aiassisteddev.md){target="_blank"}

[Torna a tutti i moduli](./../../../overview.md){target="_blank"}
