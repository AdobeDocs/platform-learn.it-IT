---
title: Configurazione della base dati relazionali
description: Configurazione della base dati relazionali
kt: 5342
doc-type: tutorial
exl-id: 532e5f2c-971f-488f-bef4-3a8141408cc8
source-git-commit: 7a595d9b1fb3dc6a3b5b413e65dbaaaf5ac143c4
workflow-type: tm+mt
source-wordcount: '1805'
ht-degree: 2%

---

# 3.8.1 Configurazione della base dati relazionali

Accedi a Adobe Journey Optimizer da [https://experience.adobe.com](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![AJO OC](./images/aechome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`.

![AJO OC](./images/ajohome.png)

## 3.8.1.1 configurazione schema basato su relazioni

Uno schema relazionale è la definizione formale del modello di dati basato su modello.

Specifica:

- Il set di tabelle
- Colonne in ogni tabella
- I vincoli
- Le relazioni tra le tabelle

L’organizzazione di schemi o tabelle in un modello di dati basato su modelli riguarda la strutturazione dei dati in più tabelle. Assicurati che ogni tabella memorizzi un tipo di entità/schemi.

Quando si acquisiscono i dati in per l’utilizzo con le campagne orchestrate di Adobe Journey Optimizer, sono disponibili le seguenti origini:

- Amazon S3
- Google Cloud Storage
- SFTP
- Snowflake
- Google BigQuery
- Data Landing Zone
- Azure Databricks
- Caricamento file locale

Il primo passaggio di questo esercizio è la configurazione degli schemi XDM relazionali. Nel menu a sinistra, scorri verso il basso fino a **Gestione dati** e seleziona **Schemi**. Fare clic su **+ Crea schema**.

![AJO OC](./images/ajoocdata1.png)

Selezionare **Relazionale**.

![AJO OC](./images/ajoocdata2.png)

Selezionare **Carica file DDL**, quindi fare clic su **Scegli file**.

![AJO OC](./images/ajoocdata3.png)

Scarica il file [citisignal_ddl_tables_only.sql](./assets/citisignal_ddl_tables_only.sql) sul desktop.

![AJO OC](./images/ajoocdata4.png)

Selezionare il file **`citisignal_ddl_tables_only.sql`** e fare clic su **apri**.

![AJO OC](./images/ajoocdata5.png)

Dovresti vedere questo. Fai clic su **Avanti**.

![AJO OC](./images/ajoocdata6.png)

### Identità

Alcuni degli schemi contengono identificatori personali e tali campi devono essere contrassegnati come **Identità** ed è necessario selezionare lo **Spazio dei nomi** applicabile a quel tipo specifico di identità.

**`citisignal_accounts`**

Per questo schema, vai al campo **account_id** e imposta il tipo **Identity** su **Demo System - CRMID**.

![AJO OC](./images/ajoocdata7.png)

**`citisignal_recipients`**

Per questo schema, vai al campo **account_id** e imposta il tipo **Identity** su **Demo System - CRMID**, quindi vai al campo **email** e imposta il tipo **Identity** su **Email**.

![AJO OC](./images/ajoocdata8.png)

### Controllo delle versioni

Per tenere traccia degli aggiornamenti ai dati che verranno acquisiti in base a questi schemi, è necessario impostare un campo che verrà utilizzato per tenere traccia della versione dei dati caricati. Il campo utilizzato per questo in tutti questi schemi è il campo **lastmodified**, che contiene una marca temporale dei dati caricati.

È ora necessario selezionare la casella di controllo per **Controllo versioni** per il campo **lastmodified** in ciascuno di questi schemi.

**`citisignal_products`**

Seleziona la casella di controllo per **Controllo delle versioni** per il campo **lastmodified**.

![AJO OC](./images/ajoocdata9.png)

**`citisignal_product_bundles`**

Seleziona la casella di controllo per **Controllo delle versioni** per il campo **lastmodified**.

![AJO OC](./images/ajoocdata10.png)

**`citisignal_product_relationships`**

Seleziona la casella di controllo per **Controllo delle versioni** per il campo **lastmodified**.

![AJO OC](./images/ajoocdata11.png)

**`citisignal_accounts`**

Seleziona la casella di controllo per **Controllo delle versioni** per il campo **lastmodified**.

![AJO OC](./images/ajoocdata12.png)

**`citisignal_recipients`**

Seleziona la casella di controllo per **Controllo delle versioni** per il campo **lastmodified**.

![AJO OC](./images/ajoocdata13.png)

**`citisignal_mobile_subscriptions`**

Seleziona la casella di controllo per **Controllo delle versioni** per il campo **lastmodified**.

![AJO OC](./images/ajoocdata14.png)

**`citisignal_internet_subscriptions`**

Seleziona la casella di controllo per **Controllo delle versioni** per il campo **lastmodified**.

![AJO OC](./images/ajoocdata15.png)

**`citisignal_tv_subscriptions`**

Seleziona la casella di controllo per **Controllo delle versioni** per il campo **lastmodified**.

![AJO OC](./images/ajoocdata16.png)

**`citisignal_equipment_subscriptions`**

Seleziona la casella di controllo per **Controllo delle versioni** per il campo **lastmodified**.

![AJO OC](./images/ajoocdata17.png)

**`citisignal_mobile_usage_summary`**

Seleziona la casella di controllo per **Controllo delle versioni** per il campo **lastmodified**.

![AJO OC](./images/ajoocdata18.png)

**`citisignal_internet_usage_summary`**

Seleziona la casella di controllo per **Controllo delle versioni** per il campo **lastmodified**.

![AJO OC](./images/ajoocdata19.png)

**`citisignal_offers`**

Seleziona la casella di controllo per **Controllo delle versioni** per il campo **lastmodified**.

![AJO OC](./images/ajoocdata20.png)

**`citisignal_offer_eligibility`**

Seleziona la casella di controllo per **Controllo delle versioni** per il campo **lastmodified**.

![AJO OC](./images/ajoocdata21.png)

### Nome dello schema

Quando si acquisiscono questi schemi a scopo di abilitazione in una sandbox condivisa, è necessario modificare il nome di ogni schema in modo che sia univoco nella sandbox specifica. Questa modifica è stata apportata per evitare conflitti di denominazione degli schemi.

Per questa esercitazione, aggiungere il proprio LDAP prima di ogni nome di schema, il che significa che ogni nome di schema deve avere questo prefisso: `--aepUserLdap--_`

**`citisignal_products`**

Cambia il nome dello schema in `--aepUserLdap--_ citisignal_products`.

![AJO OC](./images/ajoocdatan9.png)

**`citisignal_product_bundles`**

Cambia il nome dello schema in `--aepUserLdap--_ citisignal_product_bundles`.

![AJO OC](./images/ajoocdatan10.png)

**`citisignal_product_relationships`**

Cambia il nome dello schema in `--aepUserLdap--_ citisignal_product_relationships`.

![AJO OC](./images/ajoocdatan11.png)

**`citisignal_accounts`**

Cambia il nome dello schema in `--aepUserLdap--_ citisignal_accounts`.

![AJO OC](./images/ajoocdatan12.png)

**`citisignal_recipients`**

Cambia il nome dello schema in `--aepUserLdap--_ citisignal_recipients`.

![AJO OC](./images/ajoocdatan13.png)

**`citisignal_mobile_subscriptions`**

Cambia il nome dello schema in `--aepUserLdap--_ citisignal_mobile_subscriptions`.

![AJO OC](./images/ajoocdatan14.png)

**`citisignal_internet_subscriptions`**

Cambia il nome dello schema in `--aepUserLdap--_ citisignal_internet_subscriptions`.

![AJO OC](./images/ajoocdatan15.png)

**`citisignal_tv_subscriptions`**

Cambia il nome dello schema in `--aepUserLdap--_ citisignal_internet_subscriptions`.

![AJO OC](./images/ajoocdatan16.png)

**`citisignal_equipment_subscriptions`**

Cambia il nome dello schema in `--aepUserLdap--_ citisignal_equipment_subscriptions`.

![AJO OC](./images/ajoocdatan17.png)

**`citisignal_mobile_usage_summary`**

Cambia il nome dello schema in `--aepUserLdap--_ citisignal_mobile_usage_summary`.

![AJO OC](./images/ajoocdatan18.png)

**`citisignal_internet_usage_summary`**

Cambia il nome dello schema in `--aepUserLdap--_ citisignal_internet_usage_summary`.

![AJO OC](./images/ajoocdatan19.png)

**`citisignal_offers`**

Cambia il nome dello schema in `--aepUserLdap--_ citisignal_offers`.

![AJO OC](./images/ajoocdatan20.png)

**`citisignal_offer_eligibility`**

Cambia il nome dello schema in `--aepUserLdap--_ citisignal_offer_eligibility`.

![AJO OC](./images/ajoocdatan21.png)

Gli schemi sono pronti per essere salvati. Fai clic su **Fine**.

![AJO OC](./images/ajoocdata22.png)

Dovresti vedere questo. Fai clic su **Salva**.

![AJO OC](./images/ajoocdata23.png)

Fai clic su **Apri processi**.

![AJO OC](./images/ajoocdata24.png)

Dovresti vedere questo. Prima di procedere al passaggio successivo, è necessario attendere il completamento del processo.

![AJO OC](./images/ajoocdata25.png)

Una volta completato correttamente il processo, puoi continuare con il passaggio successivo. Questa operazione può richiedere 5-10 minuti.

![AJO OC](./images/ajoocdata26.png)

Ora che gli schemi XDM relazionali sono configurati e i dati vengono acquisiti, puoi iniziare a utilizzarli per creare la campagna orchestrata nell’esercizio successivo.

## Acquisizione dati 3.8.1.2

Vai a **Set di dati**. Dovresti quindi visualizzare un set di dati creato per ogni schema creato.

![AJO OC](./images/ajoocdata27.png)

Scarica il file [data.zip](./assets/data.zip) sul desktop e decomprimi.

![AJO OC](./images/ajoocdata28.png)

Apri la cartella **data**. Dovresti visualizzare un file CSV per ciascuno degli schemi creati. Ora devi caricare tali dati in ogni set di dati corrispondente. Per questa esercitazione, effettuerai il caricamento di un file locale in ciascun set di dati.

![AJO OC](./images/ajoocdata29.png)

**`vangeluw_citisignal_products`**

Vai a **Origini**, cerca `local`, quindi fai clic su **Aggiungi dati** in **Caricamento file locale**.

![AJO OC](./images/ajoocdatas10.png)

Attiva/disattiva per **Abilita acquisizione dati modifiche**.

Selezionare il set di dati `vangeluw_citisignal_products`.

Fai clic su **Avanti**.

![AJO OC](./images/ajoocdatas9a.png)

Fare clic su **Scegli file**. Selezionare il file **`citisignal_products.csv`** e fare clic su **apri**.

![AJO OC](./images/ajoocdatas9b.png)

Fai clic su **Avanti**

![AJO OC](./images/ajoocdatas9c.png)

Fai clic su **Fine**.

![AJO OC](./images/ajoocdatas9d.png)

Dopo un paio di minuti, puoi vedere i dati acquisiti nel set di dati.

![AJO OC](./images/ajoocdatas9e.png)

**`vangeluw_citisignal_product_bundles`**

Vai a **Origini**, cerca `local`, quindi fai clic su **Aggiungi dati** in **Caricamento file locale**.

![AJO OC](./images/ajoocdatas10.png)

Attiva/disattiva per **Abilita acquisizione dati modifiche**.

Selezionare il set di dati `vangeluw_citisignal_product_bundles`.

Fai clic su **Avanti**.

![AJO OC](./images/ajoocdatas10a.png)

Fare clic su **Scegli file**. Selezionare il file **`citisignal_product_bundles.csv`** e fare clic su **apri**.

![AJO OC](./images/ajoocdatas10b.png)

Fai clic su **Avanti**

![AJO OC](./images/ajoocdatas10c.png)

Fai clic su **Fine**.

![AJO OC](./images/ajoocdatas10d.png)

Dopo un paio di minuti, puoi vedere i dati acquisiti nel set di dati.

![AJO OC](./images/ajoocdatas10e.png)

**`vangeluw_citisignal_product_relationships`**

Vai a **Origini**, cerca `local`, quindi fai clic su **Aggiungi dati** in **Caricamento file locale**.

![AJO OC](./images/ajoocdatas10.png)

Attiva/disattiva per **Abilita acquisizione dati modifiche**.

Selezionare il set di dati `vangeluw_citisignal_product_relationships`.

Fai clic su **Avanti**.

![AJO OC](./images/ajoocdatas11a.png)

Fare clic su **Scegli file**. Selezionare il file **`citisignal_product_relationships.csv`** e fare clic su **apri**.

![AJO OC](./images/ajoocdatas11b.png)

Fai clic su **Avanti**

![AJO OC](./images/ajoocdatas11c.png)

Fai clic su **Fine**.

![AJO OC](./images/ajoocdatas11d.png)

Dopo un paio di minuti, puoi vedere i dati acquisiti nel set di dati.

![AJO OC](./images/ajoocdatas11e.png)

**`vangeluw_citisignal_accounts`**

Vai a **Origini**, cerca `local`, quindi fai clic su **Aggiungi dati** in **Caricamento file locale**.

![AJO OC](./images/ajoocdatas10.png)

Attiva/disattiva per **Abilita acquisizione dati modifiche**.

Selezionare il set di dati `vangeluw_citisignal_accounts`.

Fai clic su **Avanti**.

![AJO OC](./images/ajoocdatas12a.png)

Fare clic su **Scegli file**. Selezionare il file **`citisignal_accounts.csv`** e fare clic su **apri**.

![AJO OC](./images/ajoocdatas12b.png)

Fai clic su **Avanti**

![AJO OC](./images/ajoocdatas12c.png)

Fai clic su **Fine**.

![AJO OC](./images/ajoocdatas12d.png)

Dopo un paio di minuti, puoi vedere i dati acquisiti nel set di dati.

![AJO OC](./images/ajoocdatas12e.png)

**`vangeluw_citisignal_recipients`**

Vai a **Origini**, cerca `local`, quindi fai clic su **Aggiungi dati** in **Caricamento file locale**.

![AJO OC](./images/ajoocdatas10.png)

Attiva/disattiva per **Abilita acquisizione dati modifiche**.

Selezionare il set di dati `vangeluw_citisignal_recipients`.

Fai clic su **Avanti**.

![AJO OC](./images/ajoocdatas13a.png)

Fare clic su **Scegli file**. Selezionare il file **`citisignal_recipients.csv`** e fare clic su **apri**.

![AJO OC](./images/ajoocdatas13b.png)

Fai clic su **Avanti**

![AJO OC](./images/ajoocdatas13c.png)

Fai clic su **Fine**.

![AJO OC](./images/ajoocdatas13d.png)

Dopo un paio di minuti, puoi vedere i dati acquisiti nel set di dati.

![AJO OC](./images/ajoocdatas13e.png)

**`vangeluw_citisignal_mobile_subscriptions`**

Vai a **Origini**, cerca `local`, quindi fai clic su **Aggiungi dati** in **Caricamento file locale**.

![AJO OC](./images/ajoocdatas10.png)

Attiva/disattiva per **Abilita acquisizione dati modifiche**.

Selezionare il set di dati `vangeluw_citisignal_mobile_subscriptions`.

Fai clic su **Avanti**.

![AJO OC](./images/ajoocdatas14a.png)

Fare clic su **Scegli file**. Selezionare il file **`citisignal_mobile_subscriptions.csv`** e fare clic su **apri**.

![AJO OC](./images/ajoocdatas14b.png)

Fai clic su **Avanti**

![AJO OC](./images/ajoocdatas14c.png)

Fai clic su **Fine**.

![AJO OC](./images/ajoocdatas14d.png)

Dopo un paio di minuti, puoi vedere i dati acquisiti nel set di dati.

![AJO OC](./images/ajoocdatas14e.png)

**`vangeluw_citisignal_internet_subscriptions`**

Vai a **Origini**, cerca `local`, quindi fai clic su **Aggiungi dati** in **Caricamento file locale**.

![AJO OC](./images/ajoocdatas10.png)

Attiva/disattiva per **Abilita acquisizione dati modifiche**.

Selezionare il set di dati `vangeluw_citisignal_internet_subscriptions`.

Fai clic su **Avanti**.

![AJO OC](./images/ajoocdatas15a.png)

Fare clic su **Scegli file**. Selezionare il file **`citisignal_internet_subscriptions.csv`** e fare clic su **apri**.

![AJO OC](./images/ajoocdatas15b.png)

Fai clic su **Avanti**

![AJO OC](./images/ajoocdatas15c.png)

Fai clic su **Fine**.

![AJO OC](./images/ajoocdatas15d.png)

Dopo un paio di minuti, puoi vedere i dati acquisiti nel set di dati.

![AJO OC](./images/ajoocdatas15e.png)

**`vangeluw_citisignal_tv_subscriptions`**

Vai a **Origini**, cerca `local`, quindi fai clic su **Aggiungi dati** in **Caricamento file locale**.

![AJO OC](./images/ajoocdatas10.png)

Attiva/disattiva per **Abilita acquisizione dati modifiche**.

Selezionare il set di dati `vangeluw_citisignal_tv_subscriptions`.

Fai clic su **Avanti**.

![AJO OC](./images/ajoocdatas16a.png)

Fare clic su **Scegli file**. Selezionare il file **`citisignal_tv_subscriptions.csv`** e fare clic su **apri**.

![AJO OC](./images/ajoocdatas16b.png)

Fai clic su **Avanti**

![AJO OC](./images/ajoocdatas16c.png)

Fai clic su **Fine**.

![AJO OC](./images/ajoocdatas16d.png)

Dopo un paio di minuti, puoi vedere i dati acquisiti nel set di dati.

![AJO OC](./images/ajoocdatas16e.png)

**`vangeluw_citisignal_equipment_subscriptions`**

Vai a **Origini**, cerca `local`, quindi fai clic su **Aggiungi dati** in **Caricamento file locale**.

![AJO OC](./images/ajoocdatas10.png)

Attiva/disattiva per **Abilita acquisizione dati modifiche**.

Selezionare il set di dati `vangeluw_citisignal_equipment_subscriptions`.

Fai clic su **Avanti**.

![AJO OC](./images/ajoocdatas17a.png)

Fare clic su **Scegli file**. Selezionare il file **`citisignal_equipment_subscriptions.csv`** e fare clic su **apri**.

![AJO OC](./images/ajoocdatas17b.png)

Fai clic su **Avanti**

![AJO OC](./images/ajoocdatas17c.png)

Fai clic su **Fine**.

![AJO OC](./images/ajoocdatas17d.png)

Dopo un paio di minuti, puoi vedere i dati acquisiti nel set di dati.

![AJO OC](./images/ajoocdatas17e.png)

**`vangeluw_citisignal_mobile_usage_summary`**

Vai a **Origini**, cerca `local`, quindi fai clic su **Aggiungi dati** in **Caricamento file locale**.

![AJO OC](./images/ajoocdatas10.png)

Attiva/disattiva per **Abilita acquisizione dati modifiche**.

Selezionare il set di dati `vangeluw_citisignal_mobile_usage_summary`.

Fai clic su **Avanti**.

![AJO OC](./images/ajoocdatas18a.png)

Fare clic su **Scegli file**. Selezionare il file **`citisignal_mobile_usage_summary.csv`** e fare clic su **apri**.

![AJO OC](./images/ajoocdatas18b.png)

Fai clic su **Avanti**

![AJO OC](./images/ajoocdatas18c.png)

Fai clic su **Fine**.

![AJO OC](./images/ajoocdatas18d.png)

Dopo un paio di minuti, puoi vedere i dati acquisiti nel set di dati.

![AJO OC](./images/ajoocdatas18e.png)

**`vangeluw_citisignal_internet_usage_summary`**

Vai a **Origini**, cerca `local`, quindi fai clic su **Aggiungi dati** in **Caricamento file locale**.

![AJO OC](./images/ajoocdatas10.png)

Attiva/disattiva per **Abilita acquisizione dati modifiche**.

Selezionare il set di dati `vangeluw_citisignal_internet_usage_summary`.

Fai clic su **Avanti**.

![AJO OC](./images/ajoocdatas19a.png)

Fare clic su **Scegli file**. Selezionare il file **`citisignal_internet_usage_summary.csv`** e fare clic su **apri**.

![AJO OC](./images/ajoocdatas19b.png)

Fai clic su **Avanti**

![AJO OC](./images/ajoocdatas19c.png)

Fai clic su **Fine**.

![AJO OC](./images/ajoocdatas19d.png)

Dopo un paio di minuti, puoi vedere i dati acquisiti nel set di dati.

![AJO OC](./images/ajoocdatas19e.png)

**`vangeluw_citisignal_offers`**

Vai a **Origini**, cerca `local`, quindi fai clic su **Aggiungi dati** in **Caricamento file locale**.

![AJO OC](./images/ajoocdatas10.png)

Attiva/disattiva per **Abilita acquisizione dati modifiche**.

Selezionare il set di dati `vangeluw_citisignal_offers`.

Fai clic su **Avanti**.

![AJO OC](./images/ajoocdatas20a.png)

Fare clic su **Scegli file**. Selezionare il file **`citisignal_offers.csv`** e fare clic su **apri**.

![AJO OC](./images/ajoocdatas20b.png)

Fai clic su **Avanti**

![AJO OC](./images/ajoocdatas20c.png)

Fai clic su **Fine**.

![AJO OC](./images/ajoocdatas20d.png)

Dopo un paio di minuti, puoi vedere i dati acquisiti nel set di dati.

![AJO OC](./images/ajoocdatas20e.png)

**`vangeluw_citisignal_offer_eligibility`**

Vai a **Origini**, cerca `local`, quindi fai clic su **Aggiungi dati** in **Caricamento file locale**.

![AJO OC](./images/ajoocdatas10.png)

Attiva/disattiva per **Abilita acquisizione dati modifiche**.

Selezionare il set di dati `vangeluw_citisignal_offer_eligibility`.

Fai clic su **Avanti**.

![AJO OC](./images/ajoocdatas21a.png)

Fare clic su **Scegli file**. Selezionare il file **`citisignal_offer_eligibility.csv`** e fare clic su **apri**.

![AJO OC](./images/ajoocdatas21b.png)

Fai clic su **Avanti**

![AJO OC](./images/ajoocdatas21c.png)

Fai clic su **Fine**.

![AJO OC](./images/ajoocdatas21d.png)

Dopo un paio di minuti, puoi vedere i dati acquisiti nel set di dati.

![AJO OC](./images/ajoocdatas21e.png)

Tutti i dati vengono ora acquisiti. Nel prossimo esercizio inizierai a utilizzare tali dati come parte di una campagna orchestrata.

## Passaggi successivi

Vai a [Crea la tua campagna orchestrata](./ex2.md){target="_blank"}

Torna a [Adobe Journey Optimizer: Campagne](./ajocampaigns.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
