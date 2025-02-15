---
title: Guida introduttiva ad Adobe I/O
description: Guida introduttiva ad Adobe I/O
kt: 5342
doc-type: tutorial
source-git-commit: 431f7696df12c8c133aced57c0f639c682304dee
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Configurare il progetto Adobe I/O

## Creare un progetto Adobe I/O

In questo esercizio, Adobe I/O viene utilizzato per eseguire query su vari endpoint di Adobe. Segui questi passaggi per configurare Adobe I/O.

Vai a [https://developer.adobe.com/console/home](https://developer.adobe.com/console/projects){target="_blank"}.

![Nuova integrazione Adobe I/O](./images/iohome.png){zoomable="yes"}

Assicurati di selezionare l’istanza corretta nell’angolo in alto a destra dello schermo. L&#39;istanza è `--aepImsOrgName--`.
Selezionare **Crea nuovo progetto**.

![Nuova integrazione Adobe I/O](./images/iocomp.png){zoomable="yes"}

### API dei servizi Firefly

Dovresti vedere questo. Selezionare **+ Aggiungi al progetto** e scegliere **API**.

![Nuova integrazione Adobe I/O](./images/adobe_io_access_api.png){zoomable="yes"}

Lo schermo dovrebbe essere simile al seguente.

![Nuova integrazione Adobe I/O](./images/api1.png){zoomable="yes"}

Seleziona **Creative Cloud** e scegli **Firefly - Firefly Services**, quindi seleziona **Next**.

![Nuova integrazione Adobe I/O](./images/api3.png){zoomable="yes"}

Immetti un nome per le credenziali: `--aepUserLdap-- - One Adobe OAuth credential`e seleziona **Avanti**.

![Nuova integrazione Adobe I/O](./images/api4.png){zoomable="yes"}

Selezionare il profilo predefinito **Configurazione predefinita servizi Firefly** e selezionare **Salva API configurata**.

![Nuova integrazione Adobe I/O](./images/api9.png){zoomable="yes"}

Dovresti vedere questo.

![Nuova integrazione Adobe I/O](./images/api10.png){zoomable="yes"}

### API PHOTOSHOP SERVICES

Selezionare **+ Aggiungi al progetto**, quindi selezionare **API**.

![Archiviazione Azure](./images/ps2.png){zoomable="yes"}

Selezionare **Creative Cloud** e scegliere **Photoshop - Servizi Firefly**. Seleziona **Avanti**.

![Archiviazione Azure](./images/ps3.png){zoomable="yes"}

Seleziona **Avanti**.

![Archiviazione Azure](./images/ps4.png){zoomable="yes"}

Successivamente, devi selezionare un profilo di prodotto che definisca quali autorizzazioni sono disponibili per questa integrazione.

Selezionare **Configurazione predefinita servizi Firefly** e **Configurazione predefinita servizi di automazione Creative Cloud**.

Seleziona **Salva API configurata**.

![Archiviazione Azure](./images/ps5.png){zoomable="yes"}

Dovresti vedere questo.

![Nuova integrazione Adobe I/O](./images/ps7.png){zoomable="yes"}

### API ADOBE EXPERIENCE PLATFORM

Selezionare **+ Aggiungi al progetto**, quindi selezionare **API**.

![Archiviazione Azure](./images/aep1.png){zoomable="yes"}

Seleziona **Adobe Experience Platform** e scegli **Experience Platform API**. Seleziona **Avanti**.

![Archiviazione Azure](./images/aep2.png){zoomable="yes"}

Seleziona **Avanti**.

![Archiviazione Azure](./images/aep3.png){zoomable="yes"}

Successivamente, devi selezionare un profilo di prodotto che definisca quali autorizzazioni sono disponibili per questa integrazione.

Selezionare **Adobe Experience Platform - Tutti gli utenti - PROD**.

Seleziona **Salva API configurata**.

![Archiviazione Azure](./images/aep4.png){zoomable="yes"}

Dovresti vedere questo.

![Nuova integrazione Adobe I/O](./images/aep5.png){zoomable="yes"}

### Nome progetto

Fai clic sul nome del progetto.

![Nuova integrazione Adobe I/O](./images/api13.png){zoomable="yes"}

Seleziona **Modifica progetto**.

![Nuova integrazione Adobe I/O](./images/api14.png){zoomable="yes"}

Immetti un nome descrittivo per l&#39;integrazione: `--aepUserLdap-- One Adobe tutorial`e seleziona **Salva**.

![Nuova integrazione Adobe I/O](./images/api15.png){zoomable="yes"}

La configurazione del progetto Adobe I/O è terminata.

![Nuova integrazione Adobe I/O](./images/api16.png){zoomable="yes"}

## Passaggi successivi

Vai a [Opzione 1: installazione di Postman](./ex7.md){target="_blank"}

Vai a [Opzione 2: installazione di PostBuster](./ex8.md){target="_blank"}

Torna a [Guida introduttiva](./getting-started.md){target="_blank"}

Torna a [Tutti i moduli](./../../../overview.md){target="_blank"}