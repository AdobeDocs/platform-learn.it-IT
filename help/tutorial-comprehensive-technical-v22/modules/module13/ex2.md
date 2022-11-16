---
title: Attivazione segmento a Microsoft Azure Event Hub - Configurazione della destinazione RTCDP di Event Hub in Adobe Experience Platform
description: Attivazione segmento a Microsoft Azure Event Hub - Configurazione della destinazione RTCDP di Event Hub in Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: b42b4ccb-1952-480b-b538-c1bd661e29eb
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# 13.2 Configurare la destinazione dell&#39;hub eventi di Azure in Adobe Experience Platform

## 13.2.1 Identificare i parametri di connessione di Azure richiesti

Per definire una destinazione Hub eventi in Adobe Experience Platform, devi disporre dei seguenti elementi:

- Spazio dei nomi Hubs evento
- Hub eventi
- Nome chiave SAS di Azure
- Chiave SAS di Azure

Lo spazio dei nomi Event Hub e EventHub è stato definito nell’esercizio precedente: [Esercizio 1 - Configurazione dell’hub eventi in Azure](./ex1.md)

### Namespace Event Hubs

Per cercare le informazioni di cui sopra nel portale di Azure, passa a [https://portal.azure.com/#home](https://portal.azure.com/#home). Assicurati di utilizzare l’account Azure corretto.

Seleziona **Tutte le risorse** nel portale di Azure:

![2-01-azure-all-resources.png](./images/2-01-azure-all-resources.png)

### Hub eventi

Cercare una risorsa con il tipo di risorsa **Namespace Event Hubs**, se hai seguito le convenzioni di denominazione utilizzate nell’esercizio precedente, Event Hubs Namespace sarà `--demoProfileLdap---aep-enablement`. Prendetene nota, ne avrete bisogno nel prossimo esercizio.

![2-02-select-event-hubs-namespace.png](./images/2-02-select-event-hubs-namespace.png)

Fai clic sul nome dello spazio dei nomi Hubs evento per ottenere i dettagli:

![2-03-select-event-hub.png](./images/2-03-select-event-hub.png)

Seleziona **Hubs evento** per ottenere un elenco degli hub evento definiti nello spazio dei nomi degli hub eventi, se si seguono le convenzioni di denominazione utilizzate nell’esercizio precedente, verrà trovato un hub eventi denominato `--demoProfileLdap---aep-enablement-event-hub`. Prendetene nota, ne avrete bisogno nel prossimo esercizio.

![2-04-event-hub-selected.png](./images/2-04-event-hub-selected.png)

### Nome chiave SAS

Seleziona **Criteri di accesso condivisi** per **Namespace Event Hubs**

![2-05-select-sas.png](./images/2-05-select-sas.png)

Verrà visualizzato un elenco dei criteri di accesso condiviso. La chiave SAS che stiamo cercando è **RootManageSharedAccessKey**. Nome della chiave SAS. Annotatela.

![2-06-sas-overview.png](./images/2-06-sas-overview.png)

### Valore chiave SAS

Fai clic sul pulsante **RootManageSharedAccessKey** per ottenere il valore della chiave SAS. E premi il pulsante **Copia negli Appunti** per copiare **Chiave principale**:

![2-07-sas-key-value.png](./images/2-07-sas-key-value.png)

### Riepilogo dei valori di destinazione

A questo punto, dovresti aver identificato tutti i valori necessari per definire la destinazione di Azure Event Hub in Adobe Experience Platform Real-time CDP.

| Nome attributo di destinazione | Valore attributo di destinazione | Valore di esempio |
|---|---|---|
| sasKeyName | Nome chiave SAS | RootManageSharedAccessKey |
| sasKey | Valore chiave SAS | srREx9ShJG1Rv7f/.. |
| namespace | Namespace Event Hubs | `--demoProfileLdap---aep-enablement` |
| eventHubName | Hub eventi | `--demoProfileLdap---aep-enablement-event-hub` |

## 13.2.2 Creare la destinazione dell&#39;hub eventi di Azure in Adobe Experience Platform

Accedi a Adobe Experience Platform andando a questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l&#39;accesso, si aprirà la homepage di Adobe Experience Platform.

![Acquisizione dei dati](../module2/images/home.png)

Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxId--``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo. Dopo aver selezionato la sandbox appropriata, visualizzerai la modifica dello schermo e ora ti trovi nella sandbox dedicata.

![Acquisizione dei dati](../module2/images/sb1.png)

Vai a **Destinazioni**, quindi vai a **Catalogo**.

![Acquisizione dei dati](./images/sb2a.png)

Seleziona **Archiviazione cloud** e vai a **Hub eventi di Azure** e fai clic su **Configurazione** o **Configura**:

![2-08-list-destinations.png](./images/2-08-list-destinations.png)

Inserisci i valori di destinazione raccolti nell&#39;esercizio precedente. Quindi, fai clic su **Connetti a destinazione**.

![2-09-destination-values.png](./images/2-09-destination-values.png)

Se le tue credenziali sono corrette, verrà visualizzata una conferma: **Connesso**.

![2-09-destination-values.png](./images/2-09-destination-valuesa.png)

È ora necessario immettere il nome e la descrizione nel formato `--demoProfileLdap---aep-enablement`. Inserisci il **eventHubName** (vedere l’esercizio precedente, si presenta così: `--demoProfileLdap---aep-enablement-event-hub`) e fai clic su **Successivo**.

![2-10-create-destination.png](./images/2-10-create-destination.png)

Fai clic su **Salva e esci**.

![2-11-save-exit-activation.png](./images/2-11-save-exit-activation.png)

La destinazione viene ora creata e disponibile in Adobe Experience Platform.

![2-12-destination-created.png](./images/2-12-destination-created.png)

Passaggio successivo: [13.3 Creare un segmento](./ex3.md)

[Torna al modulo 13](./segment-activation-microsoft-azure-eventhub.md)

[Torna a tutti i moduli](./../../overview.md)
