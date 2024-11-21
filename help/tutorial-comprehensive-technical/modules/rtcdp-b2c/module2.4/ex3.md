---
title: 'Audience Activation dell’hub eventi di Microsoft Azure: configurare la destinazione RTCDP dell’hub eventi in Adobe Experience Platform'
description: 'Audience Activation dell’hub eventi di Microsoft Azure: configurare la destinazione RTCDP dell’hub eventi in Adobe Experience Platform'
kt: 5342
doc-type: tutorial
exl-id: 86bc3afa-16a9-4834-9119-ce02445cd524
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# 2.4.3 Configurare la destinazione dell’hub eventi di Azure in Adobe Experience Platform

## Identificare i parametri di connessione di Azure richiesti

Per configurare una destinazione Hub eventi in Adobe Experience Platform è necessario:

- Spazio dei nomi degli hub eventi
- Hub eventi
- Nome chiave SAS di Azure
- Chiave SAS di Azure

Nell&#39;esercizio precedente sono stati definiti l&#39;hub eventi e lo spazio dei nomi EventHub: [Imposta hub eventi in Azure](./ex2.md)

### Spazio dei nomi degli hub eventi

Per cercare le informazioni di cui sopra nel portale di Azure, passare a [https://portal.azure.com/#home](https://portal.azure.com/#home). Assicurati di utilizzare l’account Azure corretto.

Fai clic su **Tutte le risorse** nel portale di Azure:

![2-01-azure-all-resources.png](./images/201azureallresources.png)

Trova il tuo **Spazio dei nomi degli hub eventi** nell&#39;elenco e fai clic su di esso.

![2-01-azure-all-resources.png](./images/201azureallresources1.png)

Il nome dello spazio dei nomi **Event Hubs** è ora chiaramente visibile. Deve essere simile a `--aepUserLdap---aep-enablement`.

![2-01-azure-all-resources.png](./images/201azureallresources2.png)

### Hub eventi

Nella pagina **Spazio dei nomi degli hub eventi**, fai clic su **Entità > Hub eventi** per ottenere un elenco di hub eventi definiti nello spazio dei nomi degli hub eventi. Se hai seguito le convenzioni di denominazione utilizzate nell&#39;esercizio precedente, troverai un hub eventi denominato `--aepUserLdap---aep-enablement-event-hub`. Prendetene nota, ne avrete bisogno nel prossimo esercizio.

![2-04-event-hub-selected.png](./images/204eventhubselected.png)

### Nome chiave SAS

Nella pagina **Spazio dei nomi degli hub eventi**, fai clic su **Impostazioni > Criteri di accesso condiviso**. Verrà visualizzato un elenco dei criteri di accesso condiviso. La chiave SAS che si sta cercando è **RootManageSharedAccessKey**, che è il nome della chiave **SAS. Annotatelo.

![2-05-select-sas.png](./images/205selectsas.png)

### Valore chiave SAS

Fare clic su **RootManageSharedAccessKey** per ottenere il valore della chiave SAS. E premi l&#39;icona **Copia negli Appunti** per copiare la **chiave primaria**, in questo caso `pqb1jEC0KLazwZzIf2gTHGr75Z+PdkYgv+AEhObbQEY=`.

![2-07-sas-key-value.png](./images/207saskeyvalue.png)

### Riepilogo valori di destinazione

A questo punto, dovresti aver identificato tutti i valori necessari per definire la destinazione dell’hub eventi di Azure in Adobe Experience Platform Real-time CDP.

| Nome attributo di destinazione | Valore attributo di destinazione | Esempio di valore |
|---|---|---|
| sasKeyName | Nome chiave SAS | RootManageSharedAccessKey |
| sasKey | Valore chiave SAS | pqb1jEC0KLazwZzIf2gTHGr75Z+PdkYgv+AEhObbQEY= |
| namespace | Spazio dei nomi degli hub eventi | `--aepUserLdap---aep-enablement` |
| eventHubName | Hub eventi | `--aepUserLdap---aep-enablement-event-hub` |

## Creare la destinazione dell’hub eventi di Azure in Adobe Experience Platform

Accedi a Adobe Experience Platform da questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. Dopo aver selezionato la sandbox appropriata, la schermata cambia e ora sei nella sandbox dedicata.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/sb1.png)

Vai a **Destinazioni**, quindi vai a **Catalogo**. Seleziona **Archiviazione cloud**, passa a **Azure Event Hubs** e fai clic su **Configura**.

![2-08-list-destinations.png](./images/208listdestinations.png)

Seleziona **Autenticazione standard**. Compila i dettagli di connessione raccolti nell’esercizio precedente. Fare clic su **Connetti alla destinazione**.

![2-09-destination-values.png](./images/209destinationvalues.png)

Se le credenziali sono corrette, verrà visualizzata una conferma: **Connesso**.

![2-09-destination-values.png](./images/209destinationvaluesa.png)

Immettere il nome e la descrizione nel formato `--aepUserLdap---aep-enablement`. Immetti **eventHubName** (vedi l&#39;esercizio precedente, è simile al seguente: `--aepUserLdap---aep-enablement-event-hub`) e fai clic su **Next**.

![2-10-create-destination.png](./images/210createdestination.png)

È possibile selezionare un criterio di governance dei dati. Fai clic su **Salva ed esci**.

![2-11-save-exit-activation.png](./images/211saveexitactivation.png)

La destinazione è ora creata e disponibile in Adobe Experience Platform.

![2-12-destination-created.png](./images/212destinationcreated.png)

Passaggio successivo: [2.4.4 Crea un pubblico](./ex4.md)

[Torna al modulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Torna a tutti i moduli](./../../../overview.md)
