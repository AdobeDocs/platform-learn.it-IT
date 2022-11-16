---
title: Foundation - Acquisizione dei dati - Acquisizione dei dati da origini offline
description: Foundation - Acquisizione dei dati - Acquisizione dei dati da origini offline
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 93d9f4ef-9cbd-4310-879e-d69106b70404
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 2%

---

# 2.5 Data Landing Zone

In questo esercizio, l’obiettivo è quello di impostare il connettore Origine area di destinazione dati con l’archiviazione BLOB di Azure.

Data Landing Zone è un’interfaccia di archiviazione BLOB di Azure fornita da Adobe Experience Platform che ti consente di accedere a una struttura di archiviazione file sicura basata su cloud per l’importazione di file in Platform. La zona di destinazione dei dati supporta l’autenticazione basata su SAS e i relativi dati sono protetti con i meccanismi standard di sicurezza dell’archiviazione BLOB di Azure a riposo e in transito. L’autenticazione basata su SAS consente di accedere in modo sicuro al contenitore Area di destinazione dei dati tramite una connessione Internet pubblica.

>[!NOTE]
>
> Adobe Experience Platform **applica un TTL (time-to-live) di sette giorni** su tutti i file caricati in un contenitore Zona di destinazione dati. Tutti i file vengono eliminati dopo sette giorni.


## Prerequisiti per la versione 2.5.1

Per copiare BLOB o file nella Adobe Experience Platform Data Landing Zone, utilizza AzCopy, un&#39;utilità a riga di comando. È possibile scaricare una versione per il sistema operativo in uso tramite [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

![dlz-install-az-copy.png](./images/dlz-install-az-copy.png)

- Decomprimi il file scaricato

![dlz-install-az-copy.png](./images/dlz1.png)

- Scarica il file di dati di esempio [global-context-websiteinteractions.csv](../../assets/csv/data-ingestion/global-context-websiteinteractions.csv), che contiene le interazioni di esempio del sito web e le salva nella cartella in cui hai decompresso **azcopy**.

![dlz-install-az-copy.png](./images/dlz2.png)

- Apri una finestra terminale e passa alla cartella sul desktop. Dovresti visualizzare il seguente contenuto (azcopy e global-context-websiteinteractions.csv), ad esempio su OSX:

![dlz-unzip-azcopy.png](./images/dlz-unzip-azcopy.png)

## 2.5.2 Collegare la zona di destinazione dei dati a Adobe Experience Platform

Accedi a Adobe Experience Platform andando a questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l&#39;accesso, si aprirà la homepage di Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``--module2sandbox--``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo. Dopo aver selezionato la sandbox appropriata, visualizzerai la modifica dello schermo e ora ti trovi nella sandbox dedicata.

![Acquisizione dei dati](./images/sb1.png)

Nel menu a sinistra, vai a **Origini**. Nel catalogo Origini, cerca **data landing**. Sulla **Zona di destinazione dei dati** scheda, fai clic su **...** e seleziona **Visualizza credenziali**.

![dlz-view-credentials.png](./images/dlz-view-credentials.png)

Fai clic sulla copia in alto **SASUri**.

![dlz-copy-sas-uri.png](./images/dlz-copy-sas-uri.png)

## 2.5.3 Copia il file csv nella tua zona di destinazione dati AEP

Ora i dati vengono inseriti in Adobe Experience Platform utilizzando gli strumenti della riga di comando di Azure tramite AZCopy.

Apri un terminale nella posizione di installazione di azcopy ed esegui il seguente comando per copiare un file nella zona di destinazione dei dati di AEP:

``./azcopy copy <your-local-file> <your SASUri>``

Assicurati di circondare il SASUri con virgolette doppie. Sostituisci `<your-local-file>` dal percorso della copia locale del file **global-context-websiteinteractions.csv** nella directory azcopy e sostituire `<your SASUri>` dal **SASUri** Valore copiato dall’interfaccia utente di Adobe Experience Platform. Il comando deve essere simile al seguente:

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

Dopo aver eseguito il comando di cui sopra nel terminale, vedrete questo:

![dlz-exec-copy-command.png](./images/dlz-exec-copy-command.png)

## 2.5.4 Ricercare il file nella Data Landing Zone

Vai alla tua zona di destinazione dati in Adobe Experience Platform.

Seleziona **Origini**, cerca **data landing** e fai clic su **Configurazione** pulsante .

![dlz-ispt-datalanding-zone.png](./images/dlz-inspect-datalanding-zone.png)

Verrà aperta la Data Landing Zone. Vedrai il file appena caricato nella sezione della zona di destinazione dei dati **seleziona dati** pannello.

![dlz-datalanding-zone-open.png](./images/dlz-datalanding-zone-open.png)

## 2.5.5 Elaborazione del file

Seleziona il file e seleziona **Delimitato** come formato dati. Verrà visualizzata un’anteprima dei dati. Fai clic su **Avanti**.

![dlz-datalanding-select-file.png](./images/dlz-datalanding-select-file.png)

Ora puoi iniziare a mappare i dati caricati in modo che corrispondano allo schema XDM del set di dati.

Seleziona **Set di dati esistente** e seleziona il set di dati **Sistema di demo - Set di dati evento per il sito web (Global v1.1)**. Fai clic su **Avanti**.

![dlz-target-dataset.png](./images/dlz-target-dataset.png)

Ora puoi mappare i dati di origine in entrata dal file csv ai campi di destinazione dallo schema XDM del set di dati.

![dlz-start-mapping.png](./images/dlz-start-mapping.png)

>[!NOTE]
>
> Non preoccuparti dei potenziali errori con la mappatura. La mappatura verrà corretta nel passaggio successivo.

## 2.5.6 Mappatura dei campi

Prima di tutto, fai clic sul pulsante **Cancella tutte le mappature** pulsante . Puoi quindi iniziare con una mappatura pulita.

![dlz-clear-mappings.png](./images/mappings1.png)

Quindi, fai clic su **Nuovo tipo di campo** quindi seleziona **Aggiungi nuovo campo**.

![dlz-clear-mappings.png](./images/dlz-clear-mappings.png)

Per mappare il **ecid** campo di origine, selezionare il campo **identity.ecid** e fai clic su **Seleziona**.

![dlz-map-identity.png](./images/dlz-map-identity.png)

Quindi, fai clic su **Campo di destinazione mappa**.

![dlz-map-select-target-field.png](./images/dlz-map-select-target-field.png)

Selezionare il campo ``--aepTenantId--``.identity.core.ecid nella struttura dello schema.

![dlz-map-target-field.png](./images/dlz-map-target-field.png)

Devi mappare un paio di altri campi, fai clic su **+ Nuovo tipo di campo** seguito da **Aggiungi nuovo campo** e aggiungi campi per questa mappatura

| source | target |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| timestamp | timestamp |
| timestamp | _id |

![dlz-add-other-mapping.png](./images/dlz-add-other-mapping.png)

Al termine, la schermata dovrebbe essere simile a quella riportata di seguito. Fai clic su **Avanti**.

![dlz-mapping-result.png](./images/dlz-mapping-result.png)

Fai clic su **Avanti**.

![dlz-default-programmazione.png](./images/dlz-default-scheduling.png)

Fai clic su **Fine**.

![dlz-import-finish.png](./images/dlz-import-finish.png)

## Flusso di dati del monitor 2.5.7

Per monitorare il flusso di dati, vai a **Origini**, **Flussi di dati** e fai clic sul flusso di dati:

![dlz-monitor-dataflow.png](./images/dlz-monitor-dataflow.png)

Il caricamento dei dati può richiedere un paio di minuti, una volta completato, visualizzerai uno stato di **Completato**:

![dlz-monitor-dataflow-result.png](./images/dlz-monitor-dataflow-result.png)

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 2](./data-ingestion.md)

[Torna a tutti i moduli](../../overview.md)
