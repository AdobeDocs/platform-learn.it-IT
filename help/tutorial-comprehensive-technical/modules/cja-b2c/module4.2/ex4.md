---
title: 'Acquisire e analizzare i dati Google Analytics in Adobe Experience Platform con il connettore Source BigQuery: caricare i dati da BigQuery in Adobe Experience Platform'
description: 'Acquisire e analizzare i dati Google Analytics in Adobe Experience Platform con il connettore Source BigQuery: caricare i dati da BigQuery in Adobe Experience Platform'
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 1%

---

# 4.2.4 Caricare dati da BigQuery in Adobe Experience Platform

## Obiettivi

- Mappare i dati BigQuery su uno schema XDM
- Caricare dati BigQuery in Adobe Experience Platform
- Acquisisci familiarità con l’interfaccia utente del connettore Source BigQuery

## Prima di iniziare

Dopo l’esercizio 12.3, dovresti aprire questa pagina in Adobe Experience Platform:

![demo](./images/datasets.png)

**Se è aperto, continuare con l&#39;esercizio 12.4.1.**

**Se non è aperto, passare a [Adobe Experience Platform](https://experience.adobe.com/platform/home).**

Nel menu a sinistra, vai a Sorgenti. Verrà quindi visualizzata la home page **Sources**. Nel menu **Origini**, fare clic su **Database**.

![demo](./images/sourceshome.png)

Seleziona il connettore Source **Google BigQuery** e fai clic su **+ Configura**.

![demo](./images/bq.png)

Viene visualizzata la schermata di selezione dell’account BigQuery Google.

![demo](./images/0-c.png)

Seleziona il tuo account e fai clic su **Avanti**.

![demo](./images/ex4/0-d.png)

Verrà quindi visualizzata la visualizzazione **Aggiungi dati**.

![demo](./images/datasets.png)

## 4.2.4.1 Selezione della tabella BigQuery

Nella visualizzazione **Aggiungi dati**, seleziona il set di dati BigQuery.

![demo](./images/datasets.png)

Ora puoi visualizzare un’anteprima dei dati di Google Analytics di esempio in BigQuery.

Fai clic su **Avanti**.

![demo](./images/ex4/3.png)

## 4.2.4.2 Mappatura XDM

Ora visualizzerai questo:

![demo](./images/xdm4a.png)

Ora devi creare un nuovo set di dati o selezionare un set di dati esistente in cui caricare i dati delle Google Analytics. Per questo esercizio, sono già stati creati un set di dati e uno schema. Non è necessario creare un nuovo schema o set di dati.

Seleziona **Set di dati esistente**. Apri il menu a discesa per selezionare un set di dati. Cercare il set di dati denominato `Demo System - Event Dataset for BigQuery (Global v1.1)` e selezionarlo. Fai clic su **Avanti**.

![demo](./images/xdm6.png)

Scorri verso il basso. Ora devi mappare ogni **Campo Source** da Google Analytics/BigQuery a un **Campo di destinazione** XDM, campo per campo.

![demo](./images/xdm8.png)

Utilizzare la tabella di mapping riportata di seguito per questo esercizio.

| Campo origine | Campo di destinazione |
| ----------------- |-------------| 
| **_id** | _id |
| **_id** | canale._id |
| timestamp | timestamp |
| GA_ID | ``--aepTenantId--``.identifier.core.gaid |
| customerID | ``--aepTenantId--``.identifier.core.loyaltyId |
| Pagina | web.webPageDetails.name |
| Dispositivo | device.type |
| Browser | environment.browserDetails.vendor |
| MarketingChannel | marketing.trackingCode |
| TrafficSource | channel.typeAtSource |
| TrafficMedium | channel.mediaType |
| TransactionID | commerce.order.payments.transactionID |
| Tipo_Azione_Ecommerce | eventType |
| Visualizzazioni pagina | web.webPageDetails.pageViews.value |
| Acquisti_univoci | commerce.purchases.value |
| Visualizzazioni dettagli prodotto | commerce.productViews.value |
| Adds_To_Cart | commerce.productListAdds.value |
| Product_Removes_From_Cart | commerce.productListRemovals.value |
| Product_Checkouts | commerce.checkouts.value |

Dopo aver copiato e incollato la mappatura di cui sopra nell’interfaccia utente di Adobe Experience Platform, verifica di non visualizzare errori dovuti a errori di battitura o a spazi iniziali/finali.

Hai ora una **Mappatura** come questa:

![demo](./images/xdm34.png)

I campi di origine **GA_ID** e **customerID** sono mappati a un identificatore in questo schema XDM. Questo ti consentirà di arricchire i dati Google Analytics (dati sul comportamento web/app) con altri set di dati come Dati fedeltà o Dati del call center.

Fai clic su **Avanti**.

![demo](./images/ex4/38.png)

## 4.2.4.3 Connessione e programmazione dell’acquisizione dei dati

Verrà visualizzata la scheda **Pianificazione**:

![demo](./images/xdm38a.png)

Nella scheda **Pianificazione**, è possibile definire una frequenza per il processo di acquisizione dei dati per **Mappatura** e dati.

Poiché in Google BigQuery utilizzi dati demo che non verranno aggiornati, non è realmente necessario impostare una pianificazione in questo esercizio. Devi selezionare qualcosa e, per evitare troppi processi inutili di acquisizione dei dati, devi impostare la frequenza in questo modo:

- Frequenza: **Settimana**
- Intervallo: **200**

![demo](./images/ex4/39.png)

**Importante**: assicurarsi di attivare l&#39;opzione **Backfill**.

![demo](./images/ex4/39a.png)

Ultimo ma non meno importante, è necessario definire un campo **delta**.

![demo](./images/ex4/36.png)

Il campo **delta** viene utilizzato per pianificare la connessione e caricare solo le nuove righe incluse nel set di dati BigQuery. Un campo delta è in genere sempre una colonna timestamp. Pertanto, per le future acquisizioni pianificate di dati, verranno acquisite solo le righe con una nuova marca temporale più recente.

Selezionare **timestamp** come campo delta.

![demo](./images/ex4/37.png)

Ora hai questo.

![demo](./images/xdm37a.png)

Fai clic su **Avanti**.

![demo](./images/ex4/42.png)

## 4.2.4.4 Revisione e avvio della connessione

Nella visualizzazione **Dettagli flusso set di dati**. devi assegnare un nome alla connessione, per facilitarne la ricerca in seguito.

Utilizza questa convenzione per i nomi:

| Campo | Denominazione | Esempio |
| ----------------- |-------------| -------------|
| Nome flusso set di dati | Flusso di dati - ldap - Interazione con il sito Web BigQuery | DataFlow - vangeluw - Interazione con il sito Web BigQuery |
| Descrizione | Flusso di dati - ldap - Interazione con il sito Web BigQuery | DataFlow - vangeluw - Interazione con il sito Web BigQuery |

![demo](./images/xdm44.png)

Fai clic su **Avanti**.

![demo](./images/ex4/45.png)

Ora viene visualizzata una panoramica dettagliata della connessione. Assicurati che tutto sia corretto prima di continuare, poiché alcune impostazioni non possono più essere modificate in seguito, come ad esempio la mappatura XDM.

![demo](./images/xdm46.png)

Fai clic su **Fine**.

![demo](./images/ex4/finish.png)

L&#39;impostazione della connessione potrebbe richiedere del tempo, quindi non preoccuparti se noti che:

![demo](./images/ex4/47.png)

Una volta creata la connessione, visualizzerai quanto segue:

![demo](./images/xdm48.png)

Ora puoi continuare con il prossimo esercizio, in cui utilizzerai il Customer Journey Analytics per creare visualizzazioni efficaci oltre ai dati Google Analytics.

Passaggio successivo: [4.2.5 Analizzare i dati di Google Analytics utilizzando il Customer Journey Analytics](./ex5.md)

[Torna al modulo 4.2](./customer-journey-analytics-bigquery-gcp.md)

[Torna a tutti i moduli](./../../../overview.md)
