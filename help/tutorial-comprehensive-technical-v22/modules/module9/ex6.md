---
title: 'offer decisioning: verifica la tua decisione utilizzando l’API'
description: Testa la tua decisione utilizzando l’API
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 0091c31f-0b54-4d40-a82b-3bf688db8a1f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# 9.6 Verifica la tua decisione utilizzando l&#39;API

## 9.6.1 Utilizzare l&#39;API Offer Decisioning con Postman

Scarica [questa raccolta Postman per Offer decisioning](./../../assets/postman/postman_offer-decisioning.zip) sul desktop e decomprimerlo. A quel punto avrai questo:

![API OD](./images/unzip.png)

Ora disponi di questo file sul desktop:

- [!UICONTROL _Modulo 14- Decisioning Service.postman_collection.json]

In [Esercizio 3.3.3 - Autenticazione Postman ad Adobe I/O](./../../modules/module3/ex3.md) hai installato Postman. Sarà necessario utilizzare nuovamente Postman per questo esercizio.

Apri Postman. Fai clic su **[!UICONTROL Importa]**.

![Adobe I/O di nuova integrazione](./images/postmanui.png)

Fai clic su **[!UICONTROL Caricare file]**.

![Adobe I/O di nuova integrazione](./images/pm1.png)

Selezionare il file **[!UICONTROL _Modulo 14- Decisioning Service.postman_collection.json]** e fai clic su **[!UICONTROL Apri]**.

![Adobe I/O di nuova integrazione](./images/pm2.png)

Questa raccolta sarà quindi disponibile in Postman.

![Adobe I/O di nuova integrazione](./images/pm3.png)

Ora disponi di tutto il necessario in Postman per iniziare a interagire con Adobe Experience Platform tramite le API.

### 9.6.1.1 Contenitori di elenchi

Fai clic per aprire la richiesta **[!UICONTROL GET - Elenca contenitori]**.

Sotto **[!UICONTROL Parametri]**, vedrai quanto segue:

- proprietà: `_instance.parentName==aepenablementfy22`

In tale parametro, **[!UICONTROL aepenablementfy22]** è il nome della sandbox utilizzata in Adobe Experience Platform. La sandbox da utilizzare è `--aepSandboxId--`. Sostituire il testo **[!UICONTROL aepenablementfy22]** da `--aepSandboxId--`.

Dopo aver sostituito il nome della sandbox, fai clic su **[!UICONTROL Invia]**.

![API OD](./images/api2.png)

Questa è la risposta, che mostra il contenitore dell’offerta per la sandbox specificata. Copia il **[!UICONTROL container instanceId]** come indicato di seguito e annotarlo in un file di testo sul computer. Dovrà utilizzare questo **[!UICONTROL container instanceId]** per il prossimo esercizio!

![API OD](./images/api3.png)

### 9.6.1.2 Posizionamenti elenco

Fai clic per aprire la richiesta **[!UICONTROL GET - Posizionamenti elenco]**. Fai clic su **[!UICONTROL Invia]**.

![API OD](./images/api4.png)

Ora visualizzi tutti i posizionamenti disponibili nel contenitore delle offerte. I posizionamenti visualizzati sono stati definiti nell’interfaccia utente di Adobe Experience Platform, come puoi vedere in [Esercizio 9.1.3](./ex1.md).

![API OD](./images/api5.png)

### 9.6.1.3 Elencare le regole decisionali

Fai clic per aprire la richiesta **[!UICONTROL GET - Elencare regole decisionali]**. Fai clic su **[!UICONTROL Invia]**.

![API OD](./images/api6.png)

Nella risposta, vedrai le regole decisionali definite nell&#39;interfaccia utente di Adobe Experience Platform, come puoi vedere in [Esercizio 9.1.4](./ex1.md).

![API OD](./images/api7.png)

### 9.6.1.4 Elencare offerte personalizzate

Fai clic per aprire la richiesta **[!UICONTROL GET - Elencare offerte personalizzate]**. Fai clic su **[!UICONTROL Invia]**.

![API OD](./images/api8.png)

Nella risposta, vedrai le offerte personalizzate definite nell’interfaccia utente di Adobe Experience Platform in [Esercizio 9.2.1](./ex2.md).

![API OD](./images/api9.png)

### 9.6.1.5 Elenco offerte di fallback

Fai clic per aprire la richiesta **[!UICONTROL GET - Elencare offerte di fallback]**. Fai clic su **[!UICONTROL Invia]**.

![API OD](./images/api10.png)

Nella risposta, vedrai l’offerta di fallback definita nell’interfaccia utente di Adobe Experience Platform in [Esercizio 9.2.2](./ex2.md).

![API OD](./images/api11.png)

### 9.6.1.6 Raccolte elenco

Fai clic per aprire la richiesta **[!UICONTROL GET - Raccolte elenco]**.

![API OD](./images/api12.png)

Nella risposta, vedrai la raccolta definita nell’interfaccia utente di Adobe Experience Platform in [Esercizio 9.2.3](./ex2.md).

![API OD](./images/api13.png)

### 9.6.1.7 Ottieni offerte dettagliate per il profilo cliente

Fai clic per aprire la richiesta **[!UICONTROL POST - Ottenere offerte dettagliate per il profilo cliente]**. Questa richiesta è simile a quella precedente, ma in realtà restituisce dettagli come URL di immagini, testo, ecc.

![API OD](./images/api23.png)

Per questa richiesta, simile all&#39;esercizio precedente che ha requisiti simili, è necessario fornire i valori per **[!UICONTROL xdm:placementId]** e **[!UICONTROL xdm:activityId]** per recuperare i dettagli specifici dell’offerta per un cliente.

Il campo **[!UICONTROL xdm:activityId]** deve essere compilato. Puoi recuperarlo nell’interfaccia utente di Adobe Experience Platform, come indicato di seguito.

![API OD](./images/activityid.png)

Il campo **[!UICONTROL xdm:placementId]** deve essere compilato. Puoi recuperarlo nell’interfaccia utente di Adobe Experience Platform, come indicato di seguito. Nell’esempio seguente, puoi visualizzare il placementId per il posizionamento **[!UICONTROL Web - Immagine]**.

![API OD](./images/placementid.png)

Vai a **[!UICONTROL Corpo]** e inserisci l’indirizzo e-mail del cliente per il quale desideri richiedere un’offerta. Fai clic su **[!UICONTROL Invia]**.

![API OD](./images/api24.png)

Infine, vedrai il risultato di quale tipo di offerta personalizzata e quali risorse devono essere visualizzate a questo cliente.

![API OD](./images/api25.png)

Ora hai completato questo esercizio.

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 9](./offer-decisioning.md)

[Torna a tutti i moduli](./../../overview.md)
