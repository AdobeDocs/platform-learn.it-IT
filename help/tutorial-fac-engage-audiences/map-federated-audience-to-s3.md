---
title: Mappare un pubblico federato a una destinazione S3
seo-title: Map a Federated Audience to an S3 Destination | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: Mappare un pubblico federato a S3
description: In questo esercizio, mapperemo un pubblico federato a una destinazione Real-Time CDP a valle per supportare un’esperienza offline personalizzata.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
exl-id: a47b8f7b-7bd0-43a0-bc58-8b57d331b444
source-git-commit: 7e2f7bbb392eba51c0d6b9ccc8224c2081a01c7c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Mappare un pubblico federato a una destinazione S3 per sfruttare gli attributi di pubblico per l’arricchimento

Puoi sfruttare gli attributi del pubblico nel data warehouse per arricchire l’esperienza del pubblico nei flussi di lavoro di attivazione a valle che utilizzano le destinazioni RTCDP. Per SecurFinancial, questi attributi federati possono essere utilizzati per migliorare l’esperienza di personalizzazione offline del pubblico cliente. Di seguito, il pubblico federato è mappato su una destinazione Amazon S3 preconfigurata.

## Passaggi

1. Passa al portale **Destinazioni**.

2. Fai clic sul pulsante **3 dot menu** accanto alla destinazione Amazon S3 preconfigurata, quindi fai clic su **Attiva pubblico**.

   ![activate-audiences](assets/activate-audiences.png)

3. Seleziona la **destinazione S3**, quindi fai clic su **Successivo**.

   ![select-s3-destination](assets/select-s3-destination.png)

4. Seleziona il pubblico appropriato. Nel nostro esempio: **Clienti SecureFinancial - Nessun prestito, Buon credito** pubblico.

   ![select-s3-audience](assets/select-s3-audience.png)

5. Nella sezione **Pianificazione**, utilizza le impostazioni predefinite e fai clic su **Avanti**.

6. Nel passaggio **Mappatura**, scegli la chiave di deduplicazione. Nel nostro esempio, `xdm: personalEmail.address` è incluso e selezionato come **Chiave di deduplicazione**. Quindi fai clic su **Avanti**:

   ![chiave di deduplicazione](assets/deduplication-key.png)

7. Nel passaggio di mappatura, seleziona gli attributi di arricchimento in base alle mappature dei campi del pubblico nella composizione del pubblico federato. Fai clic sull&#39;icona **matita (modifica)** per visualizzare gli attributi preselezionati.

   ![modifica-attributi](assets/edit-attributes.png)

   ![final-attributes](assets/final-attribution.png)

8. Rivedi la mappatura del pubblico e premi **Fine**.

>[**!SUMMARY**]
>
> Un pubblico è stato creato correttamente e attivato facilmente su una destinazione S3. Qualsiasi altra soluzione può raccogliere questo pubblico e utilizzarlo immediatamente. L’interfaccia intuitiva consente ai team di marketing di creare e attivare rapidamente i tipi di pubblico senza spostare i dati sottostanti. I clienti che adottano questo approccio sono andati LIVE con il loro primo caso d’uso in circa un mese.


Ora [creeremo un percorso](build-journey-federated-audience.md).
