---
title: Creare un pubblico federato
seo-title: Create a federated audience | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: Creare un pubblico federato
description: In questo esercizio, creiamo un pubblico dal data warehouse di Snowflake utilizzando Federated Audience Composition.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
exl-id: a507cab5-dba9-4bf7-a043-d7c967e9e07d
source-git-commit: 7e2f7bbb392eba51c0d6b9ccc8224c2081a01c7c
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# Creare un pubblico federato

Successivamente, ti guideremo attraverso la creazione di un pubblico dal data warehouse di Snowflake utilizzando Federated Audience Composition. Il pubblico è composto da clienti SecurFinancial con un punteggio di credito pari o superiore a 650 e che attualmente non hanno un prestito nel loro portafoglio SecurFinancial.

## Passaggi

1. Nel portale **Cliente > Tipi di pubblico**, fai clic sulla scheda **Composizioni federate**.
2. Fare clic su **Crea composizione**.

   ![create-composition](assets/create-composition.png)

3. Etichettate la composizione. Nel nostro esempio: `SecurFinancial Customers - No Loans, Good Credit`. Fai clic su **Crea**.

4. Fai clic sul pulsante **+** nell&#39;area di lavoro e seleziona **Genera pubblico**. Viene visualizzata la barra di destra.

5. Fai clic su **Seleziona uno schema**, seleziona lo schema appropriato, quindi fai clic su **Conferma**.

6. Fai clic su **Continua**. Nella finestra del generatore di query fare clic sul pulsante **+** e quindi **Condizione personalizzata**. Scrivi le condizioni. Il nostro esempio utilizza:

   `CURRENTPRODUCTS does not contain loan`
   `AND`
   `CREDITSCORE greater than or equal to 650`
   `AND`
   `CONSENTSMARKETINGPREFERRED equal to email`

   *L&#39;ultima condizione garantisce che i dati delle preferenze di marketing vengano utilizzati per segmentare i clienti che hanno scelto la posta elettronica come canale di comunicazione preferito*.

   **Nota:** nel campo del valore viene fatta distinzione tra maiuscole e minuscole.

   ![generatore di query](assets/query-builder.png)

7. Fai clic sul pulsante **+** successivo, quindi fai clic su **Salva pubblico**. Etichetta questo passaggio. Nel nostro esempio, lo etichetteremo come `SecurFinancial Customers - No Loans, Good Credit`.

8. Aggiungi le mappature del pubblico pertinenti. In questo esempio:

   - **Campo pubblico Source:** E-MAIL
   - **Campo pubblico Source:** CURRENTPRODUCTS
   - **Campo pubblico Source:** FIRST NAME

9. Seleziona l’identità principale e lo spazio dei nomi da utilizzare per i profili. Queste sono le identità e i campi utilizzati per i nostri dati:

   - **Campo identità primaria:** e-mail
   - **Spazio dei nomi identità:** E-mail

10. Fai clic su **Salva**, quindi su **Inizia** per eseguire la query della composizione.

>[**RIEPILOGO**]
>
> In questo esempio, le informazioni su prodotti e crediti sono state utilizzate per creare il nostro pubblico attraverso l’accesso diretto ai dati aziendali da Snowflake, senza crearne una copia in Adobe Experience Platform. Una volta che il sistema esterno elabora la query, solo l’e-mail pertinente, i prodotti correnti e i valori di nome vengono riportati nella definizione del pubblico per l’attivazione a valle. Questo vale per tutte le destinazioni supportate da RTCDP.

Per ulteriori informazioni sulla composizione del pubblico, visita [Experience League](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/compositions/create-composition/create-composition){target="_blank"}.

Una volta creato il pubblico federato, [lo mapperemo su una destinazione S3 in Experience Platform](map-federated-audience-to-s3.md).
