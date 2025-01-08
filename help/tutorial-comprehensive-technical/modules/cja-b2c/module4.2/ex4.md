---
title: 'Acquisire e analizzare i dati Google Analytics in Adobe Experience Platform con il connettore Source BigQuery: caricare i dati da BigQuery in Adobe Experience Platform'
description: 'Acquisire e analizzare i dati Google Analytics in Adobe Experience Platform con il connettore Source BigQuery: caricare i dati da BigQuery in Adobe Experience Platform'
kt: 5342
doc-type: tutorial
exl-id: 793b35c6-761f-4b0a-b0bc-3eab93c82162
source-git-commit: 608fc570f9aa172db3578664e793f35fb3f1bf50
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 1%

---

# 4.2.4 Caricare dati da BigQuery in Adobe Experience Platform

## Obiettivi

- Mappare i dati BigQuery su uno schema XDM
- Caricare dati BigQuery in Adobe Experience Platform
- Acquisisci familiarità con l’interfaccia utente del connettore Source BigQuery

## Prima di iniziare

Dopo l’esercizio precedente, dovresti aprire questa pagina in Adobe Experience Platform:

![demo](./images/datasets.png)

**Se è aperto, continuare con l&#39;esercizio successivo.**

**Se non è aperto, passare a [Adobe Experience Platform](https://experience.adobe.com/platform/home).**

Nel menu a sinistra, vai a Sorgenti. Verrà quindi visualizzata la home page **Sources**. Nel menu **Origini**, vai al connettore di origine **Google BigQuery** e fai clic su **Configura**.

![demo](./images/sourceshome.png)

Viene visualizzata la schermata di selezione dell’account BigQuery Google. Seleziona il tuo account e fai clic su **Avanti**.

![demo](./images/0c.png)

Viene visualizzata la schermata **Seleziona dati**.

![demo](./images/datasets.png)

## 4.2.4.1 Selezione della tabella BigQuery

Nella schermata **Seleziona dati**, seleziona il set di dati BigQuery. Ora puoi visualizzare un’anteprima dei dati di Google Analytics di esempio in BigQuery.

Fai clic su **Avanti**.

![demo](./images/datasets1.png)

## 4.2.4.2 Mappatura XDM

Ora visualizzerai questo:

![demo](./images/xdm4a.png)

Ora devi creare un nuovo set di dati o selezionare un set di dati esistente in cui caricare i dati delle Google Analytics. Per questo esercizio, sono già stati creati un set di dati e uno schema. Non è necessario creare un nuovo schema o set di dati.

Seleziona **Set di dati esistente**. Apri il menu a discesa per selezionare un set di dati. Cercare il set di dati denominato `Demo System - Event Dataset for BigQuery (Global v1.1)` e selezionarlo. Fai clic su **Avanti**.

![demo](./images/xdm6.png)

Scorri verso il basso. Ora devi mappare ogni **Campo Source** da Google Analytics/BigQuery a un **Campo di destinazione** XDM, campo per campo. Potresti visualizzare una serie di errori che verranno corretti dal seguente esercizio di mappatura.

![demo](./images/xdm8.png)

Utilizzare la tabella di mapping riportata di seguito per questo esercizio.

| Campo origine | Campo di destinazione |
| ----------------- |-------------| 
| `_id` | `_id` |
| `_id` | canale._id |
| `timeStamp` | timestamp |
| `GA_ID` | ``--aepTenantId--``.identifier.core.gaid |
| `customerID` | ``--aepTenantId--``. identification.core.crmId |
| `Page` | web.webPageDetails.name |
| `Device` | device.type |
| `Browser` | environment.browserDetails.vendor |
| `MarketingChannel` | marketing.trackingCode |
| `TrafficSource` | channel.typeAtSource |
| `TrafficMedium` | channel.mediaType |
| `TransactionID` | commerce.order.payments.transactionID |
| `Ecommerce_Action_Type` | eventType |
| `Pageviews` | web.webPageDetails.pageViews.value |


Per alcuni campi, è necessario rimuovere la mappatura originale e crearne una nuova, per un **Campo calcolato**.

| Campo calcolato | Campo di destinazione |
| ----------------- |-------------| 
| `iif(Unique_Purchases == null, 0, Unique_Purchases)` | commerce.purchases.value |
| `iif(Product_Detail_Views == null, 0, Product_Detail_Views)` | commerce.productViews.value |
| `iif(Adds_To_Cart == null, 0, Adds_To_Cart)` | commerce.productListAdds.value |
| `iif(Product_Removes_From_Cart == null, 0, Product_Removes_From_Cart), 1, 0)` | commerce.productListRemovals.value |
| `iif(Product_Checkouts == null, 0, Product_Checkouts)` | commerce.checkouts.value |

Per creare un **Campo calcolato**, fare clic su **+ Nuovo tipo di campo** e quindi su **Campo calcolato**.

![demo](./images/xdm8a.png)

Incolla la regola precedente e fai clic su **Salva** per ciascuno dei campi della tabella precedente.

![demo](./images/xdm8b.png)

Ora hai una **Mappatura** come questa.

I campi di origine **GA_ID** e **customerID** sono mappati a un identificatore in questo schema XDM. Questo ti consentirà di arricchire i dati Google Analytics (dati sul comportamento web/app) con altri set di dati come Dati fedeltà o Dati del call center.

Fai clic su **Avanti**.

![demo](./images/xdm34.png)

## 4.2.4.3 Connessione e programmazione dell’acquisizione dei dati

Verrà visualizzata la scheda **Pianificazione**:

Nella scheda **Pianificazione**, è possibile definire una frequenza per il processo di acquisizione dei dati per **Mappatura** e dati.

Poiché in Google BigQuery utilizzi dati demo che non verranno aggiornati, non è realmente necessario impostare una pianificazione in questo esercizio. Devi selezionare qualcosa e, per evitare troppi processi inutili di acquisizione dei dati, devi impostare la frequenza in questo modo:

- Frequenza: **Settimana**
- Intervallo: **200**
- Ora di inizio: **qualsiasi ora nell&#39;ora successiva**

**Importante**: assicurarsi di attivare l&#39;opzione **Backfill**.

Ultimo ma non meno importante, è necessario definire un campo **delta**.

Il campo **delta** viene utilizzato per pianificare la connessione e caricare solo le nuove righe incluse nel set di dati BigQuery. Un campo delta è in genere sempre una colonna timestamp. Pertanto, per le future acquisizioni pianificate di dati, verranno acquisite solo le righe con una nuova marca temporale più recente.

Selezionare **timestamp** come campo delta.
Fai clic su **Avanti**.

![demo](./images/ex437.png)

## 4.2.4.4 Revisione e avvio della connessione

Ora viene visualizzata una panoramica dettagliata della connessione. Assicurati che tutto sia corretto prima di continuare, poiché alcune impostazioni non possono più essere modificate in seguito, come ad esempio la mappatura XDM.

Fai clic su **Fine**.

![demo](./images/xdm46.png)

Una volta creata la connessione, visualizzerai quanto segue:

![demo](./images/xdm48.png)

Ora puoi continuare con il prossimo esercizio, in cui utilizzerai il Customer Journey Analytics per creare visualizzazioni efficaci oltre ai dati Google Analytics.

Passaggio successivo: [4.2.5 Analizzare i dati di Google Analytics utilizzando il Customer Journey Analytics](./ex5.md)

[Torna al modulo 4.2](./customer-journey-analytics-bigquery-gcp.md)

[Torna a tutti i moduli](./../../../overview.md)
