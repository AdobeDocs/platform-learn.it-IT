---
title: Guida introduttiva ai servizi Firefly
description: Scopri come utilizzare Postman e Adobe I/O per eseguire query sulle API dei servizi Adobe Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: 219945c74c620b9a4b93cb2b7462137118d42d33
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# 1.1.1 Guida introduttiva ai servizi Firefly

Scopri come utilizzare Postman e Adobe I/O per eseguire query sulle API dei servizi Adobe Firefly.

## 1.1.1.1 Configurare il progetto Adobe I/O

In questo esercizio, Adobe I/O viene utilizzato per eseguire query sulle API dei servizi Firefly. Segui questi passaggi per configurare Adobe I/O.

1. Vai a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/projects){target="_blank"}.

![Nuova integrazione Adobe I/O](./images/iohome.png){zoomable="yes"}

1. Assicurati di selezionare l’istanza corretta nell’angolo in alto a destra dello schermo. L&#39;istanza è `--aepImsOrgName--`. Selezionare **Crea nuovo progetto**.

![Nuova integrazione Adobe I/O](./images/iocomp.png){zoomable="yes"}

1. Selezionare **+ Aggiungi al progetto** e scegliere **API**.

![Nuova integrazione Adobe I/O](./images/adobe_io_access_api.png){zoomable="yes"}

Lo schermo dovrebbe essere simile al seguente.

![Nuova integrazione Adobe I/O](./images/api1.png){zoomable="yes"}

1. Seleziona **Creative Cloud** e scegli **Firefly - Firefly Services**, quindi seleziona **Next**.

![Nuova integrazione Adobe I/O](./images/api3.png){zoomable="yes"}

1. Immetti un nome per le credenziali: `--aepUserLdap-- - Firefly Services OAuth credential`e seleziona **Avanti**.

![Nuova integrazione Adobe I/O](./images/api4.png){zoomable="yes"}

1. Selezionare il profilo predefinito **Configurazione predefinita servizi Firefly** e selezionare **Salva API configurata**.

![Nuova integrazione Adobe I/O](./images/api9.png){zoomable="yes"}

L’integrazione con Adobe I/O è ora pronta.

![Nuova integrazione Adobe I/O](./images/api11.png){zoomable="yes"}

## 1.1.1.2 Scaricare l’ambiente Postman

1. Seleziona **Scarica per Postman**, quindi scegli **OAuth Server-to-Server** per scaricare un ambiente Postman.

![Nuova integrazione Adobe I/O](./images/iopm.png){zoomable="yes"}

1. Seleziona il nome del progetto.

![Nuova integrazione Adobe I/O](./images/api13.png){zoomable="yes"}

1. Seleziona **Modifica progetto**.

![Nuova integrazione Adobe I/O](./images/api14.png){zoomable="yes"}

1. Immetti un nome descrittivo per l&#39;integrazione: `--aepUserLdap-- Firefly`e seleziona **Salva**.

![Nuova integrazione Adobe I/O](./images/api15.png){zoomable="yes"}

La configurazione dell’integrazione Adobe I/O è ora completata.

![Nuova integrazione Adobe I/O](./images/api16.png){zoomable="yes"}

## 1.1.1.3 Autenticazione di Postman in Adobe I/O

1. Scarica e installa la versione rilevante di Postman per il tuo sistema operativo in [Download di Postman](https://www.postman.com/downloads/){target="_blank"}.

![Nuova integrazione Adobe I/O](./images/getstarted.png){zoomable="yes"}

1. Avvia l’applicazione.

In Postman sono disponibili 2 concetti: ambienti e raccolte.

- Il file di ambiente contiene tutte le variabili di ambiente che sono più o meno coerenti. Nell’ambiente troverai elementi come l’IMSOrg dell’ambiente Adobe, insieme alle credenziali di sicurezza come l’ID client e altri. Il file di ambiente è stato scaricato durante la configurazione di Adobe I/O in precedenza ed è denominato **`oauth_server_to_server.postman_environment.json`**.

- La raccolta contiene diverse richieste API che puoi utilizzare. Utilizzeremo 2 raccolte
   - 1 raccolta per l’autenticazione in Adobe I/O
   - 1 Raccolta per gli esercizi in questo modulo

1. Scarica [postman-ff.zip](./../../../assets/postman/postman-ff.zip) sul desktop locale.

![Nuova integrazione Adobe I/O](./images/pmfolder.png){zoomable="yes"}

Nel file **postman.zip** sono presenti i seguenti file:

    - `Adobe IO - OAuth.postman_collection.json`
    - `FF - Firefly Services Tech Insiders.postman_collection.json`

1. Decomprimi **postman-ff.zip** e archivia i seguenti 2 file in una cartella sul desktop:
- Adobe IO - OAuth.postman_collection.json
- FF - Firefly Services Tech Insiders.postman_collection.json
- oauth_server_to_server.postman_environment.json

![Nuova integrazione Adobe I/O](./images/pmfolder1.png){zoomable="yes"}

1. In Postman, selezionare **Importa**.

![Nuova integrazione Adobe I/O](./images/postmanui.png){zoomable="yes"}

1. Selezionare **File**.

![Nuova integrazione Adobe I/O](./images/choosefiles.png){zoomable="yes"}

1. Scegli i tre file dalla cartella, quindi seleziona **Apri** e **Importa**.

![Nuova integrazione Adobe I/O](./images/selectfiles.png){zoomable="yes"}

![Nuova integrazione Adobe I/O](./images/impconfirm.png){zoomable="yes"}

No, in Postman hai tutto il necessario per iniziare a interagire con i servizi Firefly tramite le API.

## 1.1.1.4 Richiesta di un token di accesso

Successivamente, per assicurarti di essere autenticato correttamente, devi richiedere un token di accesso.

1. Accertati di aver selezionato l’ambiente corretto prima di eseguire qualsiasi richiesta, verificando l’elenco a discesa Ambiente nell’angolo in alto a destra. L&#39;ambiente selezionato deve avere un nome simile a questo, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea1.png){zoomable="yes"}

L&#39;ambiente selezionato deve avere un nome simile a questo, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea.png){zoomable="yes"}

Ora che l’ambiente e le raccolte Postman sono configurati e funzionanti, puoi eseguire l’autenticazione da Postman ad Adobe I/O.

1. Nella raccolta **Adobe IO - OAuth**, selezionare la richiesta denominata **POST - Ottieni token di accesso** e selezionare **Invia**.

In **Parametri query** sono presenti due variabili di riferimento, `API_KEY` e `CLIENT_SECRET`. Queste variabili vengono prese dall&#39;ambiente selezionato, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/ioauth.png){zoomable="yes"}

In caso di esito positivo, nella sezione **Body** di Postman verrà visualizzata una risposta contenente un token Bearer, un token di accesso e una finestra di scadenza.

![Postman](./images/ioauthresp.png){zoomable="yes"}


Dovresti vedere una risposta simile contenente le seguenti informazioni:

| Chiave | Valore |
|:-------------:| :---------------:| 
| token_type | **portatore** |
| access_token | **eyJhbGciOiJSU...** |
| expires_in | **86399** |

Il **bearer-token** di Adobe I/O ha un valore specifico (access_token molto lungo) e una finestra di scadenza ed è ora valido per 24 ore. Ciò significa che dopo 24 ore, se desideri utilizzare Postman per l’autenticazione in Adobe I/O, dovrai generare un nuovo token eseguendo nuovamente questa richiesta.

## 1.1.1.5 API dei servizi Firefly, immagine testo 2

Ora puoi inviare la tua prima richiesta alle API di Firefly Services.

1. Selezionare la richiesta denominata **POST - Firefly - T2I V3** dalla raccolta **FF - Firefly Services Tech Insiders**.

![Firefly](./images/ff1.png){zoomable="yes"}

1. Copia l’URL dell’immagine dalla risposta e aprilo nel browser web per visualizzarla.

![Firefly](./images/ff2.png){zoomable="yes"}

Dovresti vedere una bella immagine che rappresenta `horses in a field`.

![Firefly](./images/ff3.png){zoomable="yes"}

Puoi rispondere alla richiesta API prima di continuare con l’esercizio successivo.

## Passaggi successivi

Vai a [Ottimizza il processo Firefly utilizzando Microsoft Azure e gli URL prefirmati](./ex2.md){target="_blank"}

Torna a [Panoramica dei servizi Adobe Firefly](./firefly-services.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}
