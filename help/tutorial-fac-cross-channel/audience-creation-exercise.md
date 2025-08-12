---
title: Creazione di un pubblico
seo-title: Create an audience | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Creazione di un pubblico
description: In questa lezione, configuriamo una connessione tra Adobe Experience Platform e il tuo Data Warehouse aziendale per abilitare Federated Audience Composition.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 3%

---


# Esercizio di creazione del pubblico

Questo esercizio ti guida attraverso la creazione di un pubblico dal tuo Data Warehouse utilizzando Federated Audience Composition. Creiamo un pubblico per qualificare i clienti SecurFinancial che hanno un punteggio di credito pari o superiore a 650 e non hanno attualmente un prestito nel loro portafoglio SecurFinancial.

## Passaggi

1. Nel portale **Cliente > Tipi di pubblico**, fai clic sulla scheda **Composizioni federate**.
2. Fare clic su **Crea composizione**.

   ![create-composition](assets/create-composition.png)

3. Etichetta la composizione come `SecurFinancial Customers - No Loans, Good Credit + [your lab user ID]`. Fai clic su **Crea**.

4. Fai clic sul pulsante **+** nell&#39;area di lavoro e seleziona **Genera pubblico**. Dovrebbe essere visualizzata la barra di destra.

5. Fai clic su **Seleziona uno schema** e seleziona lo schema **FSI_CRM**, quindi fai clic su **Conferma**.

6. Fai clic su **Continua**. Nella finestra del generatore di query fare clic sul pulsante **+** e quindi **Condizione personalizzata**. Crea le seguenti condizioni:
   - `CURRENTPRODUCTS does not contain loan`
   - `AND`
   - `CREDITSCORE greater than or equal to 650`
   - Utilizziamo i dati delle preferenze di marketing per segmentare i clienti che hanno scelto l’e-mail come canale di comunicazione preferito:
   - `AND`
   - `CONSENTSMARKETINGPREFERRED equal to email`

   **Nota:** nel campo del valore viene fatta distinzione tra maiuscole e minuscole.

   A questo punto la query dovrebbe essere simile alla seguente:

   ![generatore di query](assets/query-builder.png)

7. Fai clic sul pulsante **+** successivo, quindi fai clic su **Salva pubblico**.

   Etichettare questo passaggio come `SecurFinancial Customers - No Loans, Good Credit + [your lab user ID]`. Utilizza lo stesso valore dell’etichetta del pubblico.

8. Aggiungi le seguenti mappature di pubblico:
   - **Campo pubblico Source:** E-MAIL
   - **Campo pubblico Source:** CURRENTPRODUCTS
   - **Campo pubblico Source:** FIRST NAME

9. Seleziona l’identità principale e lo spazio dei nomi da utilizzare per i profili:
   - **Campo identità primaria:** e-mail
   - **Spazio dei nomi identità:** E-mail

10. Fai clic su **Salva**, quindi su **Inizia** per eseguire la query della composizione appena creata.

**Nota:** abbiamo utilizzato informazioni su prodotti e crediti per creare il nostro pubblico che non ha spostato dati sensibili, come il punteggio di credito, sulle piattaforme a valle per l&#39;attivazione.

Per ulteriori informazioni sulla composizione del pubblico, visita [Experience League](https://experienceleague.adobe.com/it/docs/federated-audience-composition/using/compositions/create-composition/create-composition){target="_blank"}.

Ora che il nostro pubblico federato è stato creato, [procederemo con la mappatura su un account S3](map-federated-audience-to-s3.md).
