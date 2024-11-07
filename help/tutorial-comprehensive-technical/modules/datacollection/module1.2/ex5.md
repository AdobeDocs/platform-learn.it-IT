---
title: Foundation - Acquisizione dei dati - Acquisizione dei dati da origini offline
description: Foundation - Acquisizione dei dati - Acquisizione dei dati da origini offline
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 1%

---

# 1.2.5 Data Landing Zone

In questo esercizio, l’obiettivo è quello di configurare il connettore Source Data Landing Zone con l’archiviazione BLOB di Azure.

Data Landing Zone è un’interfaccia di archiviazione Azure Blob fornita da Adobe Experience Platform che consente di accedere a una struttura di archiviazione dei file sicura e basata su cloud per portare i file in Platform. Data Landing Zone supporta l’autenticazione basata su SAS e i suoi dati sono protetti con i meccanismi di sicurezza standard dell’archiviazione BLOB di Azure a riposo e in transito. L’autenticazione basata su SAS consente di accedere in modo sicuro al contenitore della Data Landing Zone tramite una connessione Internet pubblica.

>[!NOTE]
>
> Adobe Experience Platform **applica un TTL (time-to-live) di sette giorni rigoroso** su tutti i file caricati in un contenitore di aree di destinazione dati. Tutti i file vengono eliminati dopo sette giorni.


## 1.2.5.1 Prerequisiti

Per copiare BLOB o file nell’area di destinazione dati di Adobe Experience Platform, utilizzerai AzCopy, un’utility per riga di comando. Puoi scaricare una versione per il tuo sistema operativo tramite [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

![dlz-install-az-copy.png](./images/dlz-install-az-copy.png)

- Decomprimi il file scaricato

![dlz-install-az-copy.png](./images/dlz1.png)

- Scarica il file di dati di esempio global-context-websiteinteractions.csv, che contiene interazioni di esempio con siti Web, e salvalo nella cartella in cui hai decompresso **azcopy**.

![dlz-install-az-copy.png](./images/dlz2.png)

- Apri una finestra del terminale e passa alla cartella sul desktop. Dovresti visualizzare i seguenti contenuti (azcopy e global-context-websiteinteractions.csv), ad esempio su OSX:

![dlz-unzip-azcopy.png](./images/dlz-unzip-azcopy.png)

## 1.2.5.2 Collegare Data Landing Zone a Adobe Experience Platform

Accedi a Adobe Experience Platform da questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--module2sandbox--``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella riga blu nella parte superiore dello schermo. Dopo aver selezionato la sandbox appropriata, la schermata cambia e ora sei nella sandbox dedicata.

![Acquisizione dei dati](./images/sb1.png)

Nel menu a sinistra, vai a **Origini**. Nel catalogo Origini, cerca **destinazione dati**. Nella scheda **Data Landing Zone**, fai clic su **...** e seleziona **Visualizza credenziali**.

![dlz-view-credentials.png](./images/dlz-view-credentials.png)

Fare clic su tp copy **SASUri**.

![dlz-copy-sas-uri.png](./images/dlz-copy-sas-uri.png)

## 1.2.5.3 Copia il file csv nella zona di destinazione dati AEP

Ora è possibile acquisire i dati in Adobe Experience Platform utilizzando gli strumenti della riga di comando di Azure utilizzando AZCopy.

Apri un terminale nel percorso di installazione di azcopy ed esegui il seguente comando per copiare un file nella zona di destinazione dati di AEP:

``./azcopy copy <your-local-file> <your SASUri>``

Assicurarsi di racchiudere SASUri tra virgolette doppie. Sostituisci `<your-local-file>` con il percorso della copia locale del file **global-context-websiteinteractions.csv** nella directory di azcopy e sostituisci `<your SASUri>` con il valore **SASUri** copiato dall&#39;interfaccia utente di Adobe Experience Platform. Il comando deve essere simile al seguente:

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

Dopo aver eseguito il comando di cui sopra nel terminale, visualizzerai quanto segue:

![dlz-exec-copy-command.png](./images/dlz-exec-copy-command.png)

## 1.2.5.4 Ricercare il file nella Data Landing Zone

Vai alla Data Landing Zone in Adobe Experience Platform.

Seleziona **Origini**, cerca **destinazione dati** e fai clic sul pulsante **Configurazione**.

![dlz-inspect-datalanding-zone.png](./images/dlz-inspect-datalanding-zone.png)

Verrà aperta la Data Landing Zone. Vedrai il file appena caricato nel pannello **Seleziona dati** dell&#39;area di destinazione dati.

![dlz-datalanding-zone-open.png](./images/dlz-datalanding-zone-open.png)

## 1.2.5.5 Elaborazione del file

Seleziona il file e seleziona **Delimitato** come formato dati. Viene quindi visualizzata un&#39;anteprima dei dati. Fai clic su **Avanti**.

![dlz-datalanding-select-file.png](./images/dlz-datalanding-select-file.png)

Ora puoi iniziare a mappare i dati caricati in modo che corrispondano allo schema XDM del set di dati.

Seleziona **Set di dati esistente** e seleziona il set di dati **Sistema demo - Set di dati evento per il sito Web (Global v1.1)**. Fai clic su **Avanti**.

![dlz-target-dataset.png](./images/dlz-target-dataset.png)

Ora è possibile mappare i dati di origine in arrivo dal file csv ai campi di destinazione dallo schema XDM del set di dati.

![dlz-start-mapping.png](./images/dlz-start-mapping.png)

>[!NOTE]
>
> Non preoccuparti dei potenziali errori di mappatura. La mappatura verrà corretta nel passaggio successivo.

## 1.2.5.6 Campi mappa

Innanzitutto, fai clic sul pulsante **Cancella tutte le mappature**. Puoi quindi iniziare con una mappatura pulita.

![dlz-clear-mappings.png](./images/mappings1.png)

Fare clic su **Nuovo tipo di campo**, quindi selezionare **Aggiungi nuovo campo**.

![dlz-clear-mappings.png](./images/dlz-clear-mappings.png)

Per mappare il campo di origine **ecid**, selezionare il campo **identities.ecid** e fare clic su **Select**.

![dlz-map-identity.png](./images/dlz-map-identity.png)

Fare clic su **Mappa campo di destinazione**.

![dlz-map-select-target-field.png](./images/dlz-map-select-target-field.png)

Selezionare il campo ``--aepTenantId--``.identifier.core.ecid nella struttura dello schema.

![dlz-map-target-field.png](./images/dlz-map-target-field.png)

Devi mappare un paio di altri campi, fai clic su **+ Nuovo tipo di campo** seguito da **Aggiungi nuovo campo** e aggiungi i campi per questa mappatura

| sorgente | destinazione |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| timestamp | timestamp |
| timestamp | _id |

![dlz-add-other-mapping.png](./images/dlz-add-other-mapping.png)

Al termine, la schermata dovrebbe essere simile a quella riportata di seguito. Fai clic su **Avanti**.

![dlz-mapping-result.png](./images/dlz-mapping-result.png)

Fai clic su **Avanti**.

![dlz-default-scheduling.png](./images/dlz-default-scheduling.png)

Fai clic su **Fine**.

![dlz-import-finish.png](./images/dlz-import-finish.png)

## 1.2.5.7 Monitorare il flusso di dati

Per monitorare il flusso di dati, vai a **Origini**, **Flussi di dati** e fai clic sul flusso di dati:

![dlz-monitor-dataflow.png](./images/dlz-monitor-dataflow.png)

Il caricamento dei dati può richiedere alcuni minuti. Al termine, lo stato visualizzato sarà **Operazione riuscita**:

![dlz-monitor-dataflow-result.png](./images/dlz-monitor-dataflow-result.png)

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 1.2](./data-ingestion.md)

[Torna a tutti i moduli](../../../overview.md)
