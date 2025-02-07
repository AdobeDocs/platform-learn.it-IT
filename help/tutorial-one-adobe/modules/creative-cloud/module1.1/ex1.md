---
title: Guida introduttiva ai servizi di Firefly
description: Scopri come utilizzare Postman e Adobe I/O per eseguire query sulle API dei servizi Adobe Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: e6a549441d425801f2a554da9af803dca646009e
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# 1.1.1 Introduzione ai servizi di Firefly

Scopri come utilizzare Postman e Adobe I/O per eseguire query sulle API dei servizi Adobe Firefly.

## 1.1.1.2 Configurare il progetto Adobe I/O

In questo esercizio, Adobe I/O viene utilizzato per eseguire query sulle API di Servizi di Firefly. Per impostare l’Adobe I/O, segui la procedura riportata di seguito.

1. Vai a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/projects){target="_blank"}.

![Adobe I/O di nuova integrazione](./images/iohome.png)

1. Assicurati di selezionare l’istanza corretta nell’angolo in alto a destra dello schermo. L&#39;istanza è `--aepImsOrgName--`. Selezionare **Crea nuovo progetto**.

![Adobe I/O di nuova integrazione](./images/iocomp.png)

1. Selezionare **+ Aggiungi al progetto** e scegliere **API**.

![Adobe I/O di nuova integrazione](./images/adobe_io_access_api.png)

Lo schermo dovrebbe essere simile al seguente.

![Adobe I/O di nuova integrazione](./images/api1.png)

1. Seleziona **Creative Cloud** e scegli **Firefly - Servizi di Firefly**, quindi seleziona **Successivo**.

![Adobe I/O di nuova integrazione](./images/api3.png)

1. Immetti un nome per le credenziali: `--aepUserLdap-- - Firefly Services OAuth credential`e seleziona **Avanti**.

![Adobe I/O di nuova integrazione](./images/api4.png)

1. Selezionare il profilo predefinito **Configurazione predefinita servizi di Firefly** e selezionare **Salva API configurata**.

![Adobe I/O di nuova integrazione](./images/api9.png)

L’integrazione di Adobe I/O è ora pronta.

![Adobe I/O di nuova integrazione](./images/api11.png)

## 1.1.1.3 Scaricare l’ambiente Postman

1. Seleziona **Scarica per Postman**, quindi scegli **OAuth Server-to-Server** per scaricare un ambiente Postman.

![Adobe I/O di nuova integrazione](./images/iopm.png)

1. Seleziona il nome del progetto.

![Adobe I/O di nuova integrazione](./images/api13.png)

1. Seleziona **Modifica progetto**.

![Adobe I/O di nuova integrazione](./images/api14.png)

1. Immetti un nome descrittivo per l&#39;integrazione: `--aepUserLdap-- Firefly`e seleziona **Salva**.

![Adobe I/O di nuova integrazione](./images/api15.png)

La configurazione dell’integrazione Adobe I/O è terminata.

![Adobe I/O di nuova integrazione](./images/api16.png)

## 1.1.1.4 Autenticazione Postman per Adobe I/O

>[!IMPORTANT]
>
>Se sei un dipendente Adobe, segui le istruzioni qui riportate per utilizzare [PostBuster](./../../../postbuster.md).

1. Scarica e installa la versione rilevante di Postman per il tuo sistema operativo in [Download di Postman](https://www.postman.com/downloads/){target="_blank"}.

![Adobe I/O di nuova integrazione](./images/getstarted.png)

1. Avvia l’applicazione.

In Postman sono disponibili 2 concetti: ambienti e raccolte.

- Il file di ambiente contiene tutte le variabili di ambiente che sono più o meno coerenti. Nell’ambiente troverai elementi come l’IMSOrg dell’ambiente Adobe, insieme alle credenziali di sicurezza come l’ID client e altri. Il file di ambiente è stato scaricato durante la configurazione dell&#39;Adobe I/O precedente ed è denominato **`oauth_server_to_server.postman_environment.json`**.

- La raccolta contiene diverse richieste API che puoi utilizzare. Utilizzeremo 2 raccolte
   - 1 raccolta per l&#39;autenticazione all&#39;Adobe I/O
   - 1 Raccolta per gli esercizi in questo modulo

1. Scarica [postman.zip](./../../../assets/postman/postman-ff.zip) sul desktop locale.

![Adobe I/O di nuova integrazione](./images/pmfolder.png)

Nel file **postman.zip** sono presenti i seguenti file:

    - `Adobe IO - OAuth.postman_collection.json`
    - `FF - Firefly Services Tech Insiders.postman_collection.json`

1. Decomprimi **postman-ff.zip** e archivia i seguenti 2 file in una cartella sul desktop:
- Adobe - OAuth.postman_collection.json
- FF - Firefly Services Tech Insiders.postman_collection.json
- oauth_server_to_server.postman_environment.json

![Adobe I/O di nuova integrazione](./images/pmfolder1.png)

1. In Postman, selezionare **Importa**.

![Adobe I/O di nuova integrazione](./images/postmanui.png)

1. Selezionare **File**.

![Adobe I/O di nuova integrazione](./images/choosefiles.png)

1. Scegli i tre file dalla cartella, quindi seleziona **Apri** e **Importa**.

![Adobe I/O di nuova integrazione](./images/selectfiles.png)

![Adobe I/O di nuova integrazione](./images/impconfirm.png)

No, in Postman hai tutto il necessario per iniziare a interagire con i servizi di Firefly tramite le API.

## 1.1.1.5 Richiesta di un token di accesso

Successivamente, per assicurarti di essere autenticato correttamente, devi richiedere un token di accesso.

1. Accertati di aver selezionato l’ambiente corretto prima di eseguire qualsiasi richiesta, verificando l’elenco a discesa Ambiente nell’angolo in alto a destra. L&#39;ambiente selezionato deve avere un nome simile a questo, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea1.png)

L&#39;ambiente selezionato deve avere un nome simile a questo, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea.png)

Ora che l’ambiente e le raccolte Postman sono configurati e funzionanti, puoi eseguire l’autenticazione da Postman a Adobe I/O.

1. Nella raccolta **Adobe IO - OAuth**, selezionare la richiesta denominata **POST - Ottieni token di accesso** e selezionare **Invia**.

In **Parametri query** sono presenti due variabili di riferimento, `API_KEY` e `CLIENT_SECRET`. Queste variabili vengono prese dall&#39;ambiente selezionato, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/ioauth.png)

In caso di esito positivo, nella sezione **Body** di Postman verrà visualizzata una risposta contenente un token Bearer, un token di accesso e una finestra di scadenza.

![Postman](./images/ioauthresp.png)


Dovresti vedere una risposta simile contenente le seguenti informazioni:

| Chiave | Valore |
|:-------------:| :---------------:| 
| token_type | **portatore** |
| access_token | **eyJhbGciOiJSU...** |
| expires_in | **86399** |

L&#39;Adobe I/O **bearer-token** ha un valore specifico (access_token molto lungo) e una finestra di scadenza ed è ora valido per 24 ore. Ciò significa che dopo 24 ore, se desideri utilizzare Postman per l’autenticazione in Adobe I/O, dovrai generare un nuovo token eseguendo nuovamente questa richiesta.

## 1.1.1.6 API dei servizi di Firefly, immagine testo 2

Ora puoi inviare la tua prima richiesta alle API di Servizi di Firefly.

1. Selezionare la richiesta denominata **POST - Firefly - T2I V3** dalla raccolta **FF - Firefly Services Tech Insiders**.

![Firefly](./images/ff1.png)

1. Copia l’URL dell’immagine dalla risposta e aprilo nel browser web per visualizzarla.

![Firefly](./images/ff2.png)

Dovresti vedere una bella immagine che rappresenta `horses in a field`.

![Firefly](./images/ff3.png)

Puoi rispondere alla richiesta API prima di continuare con l’esercizio successivo.

## Passaggi successivi

Vai a [Ottimizza il processo di Firefly utilizzando Microsoft Azure e gli URL prefirmati](./ex2.md){target="_blank"}

Torna a [Panoramica dei servizi Adobe Firefly](./firefly-services.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}
