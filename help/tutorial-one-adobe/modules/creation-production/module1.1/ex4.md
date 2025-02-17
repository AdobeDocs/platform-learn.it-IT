---
title: API per modelli personalizzati Firefly
description: Utilizzo dell’API per modelli personalizzati di Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 330f4492-d0df-4298-9edc-4174b0065c9a
source-git-commit: b083a817700320e8e45645702c2868423c1fae99
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# API per modelli personalizzati Firefly 1.1.4

## 1.1.4.1 Configurare il modello personalizzato

Vai a [https://firefly.adobe.com/](https://firefly.adobe.com/). Fare clic su **Modelli personalizzati**.

![Modelli personalizzati Firefly](./images/ffcm1.png){zoomable="yes"}

È possibile che questo messaggio venga visualizzato. In caso contrario, fare clic su **Accetto** per continuare.

![Modelli personalizzati Firefly](./images/ffcm2.png){zoomable="yes"}

Dovresti vedere questo. Fai clic su **Addestra un modello**.

![Modelli personalizzati Firefly](./images/ffcm3.png){zoomable="yes"}

Configura i campi seguenti:

- **Nome**: utilizzare `--aepUserLdap-- - Citi Signal Router Model`
- **Modalità di formazione**: seleziona **Oggetto (anteprima tecnica)**
- **Concetto**: immettere `router`
- **Salva in**: apri l&#39;elenco a discesa e fai clic su **+ Crea nuovo progetto**

![Modelli personalizzati Firefly](./images/ffcm4.png){zoomable="yes"}

Assegnare un nome al nuovo progetto: `--aepUserLdap-- - Custom Models`. Fai clic su **Crea**.

![Modelli personalizzati Firefly](./images/ffcm5.png){zoomable="yes"}

Dovresti vedere questo. Fai clic su **Crea**.

![Modelli personalizzati Firefly](./images/ffcm6.png){zoomable="yes"}

Ora devi fornire le immagini di riferimento per il modello personalizzato da addestrare. Fai clic su **Seleziona immagini dal computer**.

![Modelli personalizzati Firefly](./images/ffcm7.png){zoomable="yes"}

Scarica le immagini di riferimento [qui](https://tech-insiders.s3.us-west-2.amazonaws.com/CitiSignal_router.zip). Decomprimi il file di download, che ti fornirà questo.

![Modelli personalizzati Firefly](./images/ffcm8.png){zoomable="yes"}

Passare alla cartella contenente i file dell&#39;immagine di download. Selezionali tutti e fai clic su **Apri**.

![Modelli personalizzati Firefly](./images/ffcm9.png){zoomable="yes"}

Si vedrà che le immagini vengono caricate.

![Modelli personalizzati Firefly](./images/ffcm10.png){zoomable="yes"}

Dopo alcuni minuti, le immagini vengono caricate correttamente. È possibile che alcune immagini presentino un errore, dovuto al fatto che la didascalia dell’immagine non è stata generata o non è sufficientemente lunga. Esaminate ogni immagine con un errore e immettete una didascalia che soddisfi i requisiti e descriva l&#39;immagine.

![Modelli personalizzati Firefly](./images/ffcm11.png){zoomable="yes"}

Una volta che tutte le immagini hanno sottotitoli che soddisfano i requisiti, è comunque necessario fornire un prompt di esempio. Immettere un prompt che utilizzi la parola &quot;router&quot;. Dopo aver fatto questo, puoi iniziare ad addestrare il tuo modello. Fai clic su **Addestra**.

![Modelli personalizzati Firefly](./images/ffcm12.png){zoomable="yes"}

Poi vedrai questo. La formazione del modello può richiedere dai 20 ai 30 minuti o più.

![Modelli personalizzati Firefly](./images/ffcm13.png){zoomable="yes"}

Dopo 20-30 minuti, il modello è ora addestrato e può essere pubblicato. Fai clic su **Pubblica**.

![Modelli personalizzati Firefly](./images/ffcm14.png){zoomable="yes"}

Fai di nuovo clic su **Pubblica**.

![Modelli personalizzati Firefly](./images/ffcm15.png){zoomable="yes"}

Chiudere la finestra a comparsa **Condividi modello personalizzato**.

![Modelli personalizzati Firefly](./images/ffcm16.png){zoomable="yes"}

## 1.1.4.2 Utilizzare il modello personalizzato nell’interfaccia utente

Vai a [https://firefly.adobe.com/cme/train](https://firefly.adobe.com/cme/train). Fai clic sul modello personalizzato per aprirlo.

![Modelli personalizzati Firefly](./images/ffcm19.png){zoomable="yes"}

Fare clic su **Anteprima e prova**.

![Modelli personalizzati Firefly](./images/ffcm17.png){zoomable="yes"}

Viene quindi visualizzato il prompt di esempio immesso prima dell&#39;esecuzione.

![Modelli personalizzati Firefly](./images/ffcm18.png){zoomable="yes"}

## 1.1.4.3 Abilitare il modello personalizzato per l’API dei modelli personalizzati dei servizi Firefly

Una volta che il modello personalizzato è stato addestrato, può essere utilizzato anche tramite l’API. Nell’esercizio 1.1.1 hai già configurato il progetto Adobe I/O per l’interazione con i servizi Firefly tramite l’API.

Vai a [https://firefly.adobe.com/cme/train](https://firefly.adobe.com/cme/train). Fai clic sul modello personalizzato per aprirlo.

![Modelli personalizzati Firefly](./images/ffcm19.png){zoomable="yes"}

Fare clic sui tre punti **...** e quindi su **Condividi**.

![Modelli personalizzati Firefly](./images/ffcm20.png){zoomable="yes"}

Per accedere a un modello personalizzato di Firefly, il modello personalizzato deve essere condiviso con l&#39;**ID account tecnico** del nostro progetto Adobe I/O.

Per recuperare il tuo **ID account tecnico**, passa a [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects). Fare clic per aprire il progetto, denominato `--aepUserLdap-- Firefly`.

![Modelli personalizzati Firefly](./images/ffcm24.png){zoomable="yes"}

Fare clic su **Server-to-Server OAuth**.

![Modelli personalizzati Firefly](./images/ffcm25.png){zoomable="yes"}

Fai clic per copiare il tuo **ID account tecnico**.

![Modelli personalizzati Firefly](./images/ffcm23.png){zoomable="yes"}

Incolla il tuo **ID account tecnico** e fai clic su **Invita a modificare**.

![Modelli personalizzati Firefly](./images/ffcm21.png){zoomable="yes"}

L&#39;**ID account tecnico** deve ora essere in grado di accedere al modello personalizzato.

![Modelli personalizzati Firefly](./images/ffcm22.png){zoomable="yes"}

## 1.1.4.4 Interagire con l’API di modelli personalizzati dei servizi Firefly

Nell&#39;esercizio 1.1.1 Guida introduttiva a Firefly Services, hai scaricato il file [postman-ff.zip](./../../../assets/postman/postman-ff.zip) sul desktop locale e hai quindi importato la raccolta in Postman.

Apri Postman e vai alla cartella **FF - Modelli personalizzati API**.

![Modelli personalizzati Firefly](./images/ffcm30.png){zoomable="yes"}

Apri la richiesta **1. FF - getCustomModels** e fare clic su **Invia**.

![Modelli personalizzati Firefly](./images/ffcm31.png){zoomable="yes"}

Nella risposta dovrebbe essere visualizzato il modello personalizzato creato in precedenza, denominato `--aepUserLdap-- - Citi Signal Router Model`. Il campo **assetId** è l&#39;identificatore univoco del modello personalizzato a cui verrà fatto riferimento nella richiesta successiva.

![Modelli personalizzati Firefly](./images/ffcm32.png){zoomable="yes"}

Apri la richiesta **2. Genera immagini asincrone**. In questo esempio, richiederai la generazione di 2 varianti in base al modello personalizzato. Puoi aggiornare il prompt che in questo caso è `a white router on a volcano in Africa`.

Fai clic su **Invia**.

![Modelli personalizzati Firefly](./images/ffcm33.png){zoomable="yes"}

La risposta contiene un campo **jobId**. Il processo per generare queste 2 immagini è ora in esecuzione e puoi controllarne lo stato utilizzando la richiesta successiva.

![Modelli personalizzati Firefly](./images/ffcm34.png){zoomable="yes"}

Apri la richiesta **3. Ottieni lo stato CM** e fai clic su **Invia**. A questo punto lo stato è impostato su In esecuzione.

![Modelli personalizzati Firefly](./images/ffcm35.png){zoomable="yes"}

Dopo alcuni minuti, fare di nuovo clic su **Invia** per la richiesta **3. Ottieni stato CM**. Dovresti vedere che lo stato è cambiato in **completato** e che nell&#39;output dovrebbero essere presenti due URL di immagine. Fare clic per aprire entrambi i file.

![Modelli personalizzati Firefly](./images/ffcm36.png){zoomable="yes"}

Questa è la prima immagine generata in questo esempio.

![Modelli personalizzati Firefly](./images/ffcm37.png){zoomable="yes"}

Questa è la seconda immagine generata in questo esempio.

![Modelli personalizzati Firefly](./images/ffcm38.png){zoomable="yes"}

Hai completato l&#39;esercizio.

## Passaggi successivi

Vai a [Riepilogo e vantaggi](./summary.md){target="_blank"}

Torna a [Utilizzo delle API di Photoshop](./ex3.md){target="_blank"}

Torna a [Panoramica dei servizi Adobe Firefly](./firefly-services.md){target="_blank"}
