---
title: Mappare un pubblico federato a S3
seo-title: Map a federated audience to S3 | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Mappare un pubblico federato a S3
description: In questa lezione, mapperemo un pubblico federato a una destinazione Real-Time CDP a valle per supportare un’esperienza offline personalizzata.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Mappare Federated Audience su S3 per sfruttare gli attributi di pubblico per l’arricchimento

In questo esercizio imparerai a sfruttare gli attributi del pubblico nel data warehouse per arricchire l&#39;esperienza del pubblico nei flussi di lavoro di attivazione a valle che utilizzano le destinazioni RTCDP. Per SecurFinancial, questi attributi federati possono essere utilizzati per migliorare l’esperienza di personalizzazione offline del pubblico cliente. In questo esempio, il pubblico federato verrà mappato su una destinazione Amazon S3 preconfigurata.

## Passaggi

1. Passa al portale **Destinazioni**.

2. Fai clic sul pulsante **3 dot menu** accanto alla destinazione Amazon S3 preconfigurata, quindi fai clic su **Attiva pubblico**.

   ![activate-audiences](assets/activate-audiences.png)

3. Seleziona la **destinazione S3**, quindi fai clic su **Successivo**.

   ![select-s3-destination](assets/select-s3-destination.png)

4. Selezionare il pubblico **SecureFinancial Customers - No Loans, Good Credit**.

   ![select-s3-audience](assets/select-s3-audience.png)

5. Nella sezione **Pianificazione**, lascia tutte le impostazioni predefinite e fai clic su **Avanti**.

6. Nel passaggio **Mappatura**, accertati che quanto segue sia incluso e selezionato come **Chiave di deduplicazione**. Quindi fai clic su **Avanti**:
   - `xdm: personalEmail.address`

   ![chiave di deduplicazione](assets/deduplication-key.png)

7. Nel passaggio di mappatura seguente, puoi selezionare gli attributi di arricchimento in base alle mappature dei campi del pubblico nella composizione del pubblico federato. Fai clic sull&#39;icona **matita (modifica)** per visualizzare gli attributi preselezionati.

   ![modifica-attributi](assets/edit-attributes.png)

   ![final-attributes](assets/final-attribution.png)

8. Rivedi la mappatura del pubblico e premi **Fine**.

Siamo pronti a passare alla [creazione di un percorso](build-journey-federated-audience.md).
