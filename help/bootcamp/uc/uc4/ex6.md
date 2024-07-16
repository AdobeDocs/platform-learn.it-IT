---
title: Bootcamp - Customer Journey Analytics - Dagli approfondimenti all'azione
description: Bootcamp - Customer Journey Analytics - Dagli approfondimenti all'azione
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Audiences
exl-id: 7a38a0a4-46e4-41f2-9a75-316dfde7128f
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 4.6 Da informazioni approfondite ad azioni

## Obiettivi

- Come creare un pubblico in base a una visualizzazione raccolta nel Customer Journey Analytics
- Utilizza questo pubblico in Real-Time CDP e Adobe Journey Optimizer

## 4.6.1 Creare un pubblico e pubblicarlo

Nel progetto hai creato un filtro denominato **Sentimenti di chiamata** e hai potuto visualizzare il numero di utenti per i quali le chiamate al call center sono state classificate come **positive**. Ora potrai creare un segmento con questi utenti e attivarli in percorsi o canali di comunicazione.

Il primo passaggio è: nel pannello creato nell&#39;ultimo esercizio, selezionare la riga **1. Sentimento di chiamata - Positivo**, fai clic con il pulsante destro del mouse e seleziona l&#39;opzione **Crea pubblico dalla selezione**:

![demo](./images/aud1.png)

Quindi, dai un nome al pubblico seguendo il modello **yourLastName - Chiamata del pubblico CJA con esito positivo**:

![demo](./images/aud2.png)

Tieni presente che è possibile avere un’anteprima del pubblico che viene creato:

![demo](./images/aud3.png)

Fare clic su **Publish**.

![demo](./images/aud4.png)

## 4.6.2 Utilizzare il pubblico come parte di un segmento

Torna a Adobe Experience Platform, vai a **Segmenti > Sfoglia** e potrai vedere il tuo segmento creato in CJA pronto e disponibile per essere utilizzato nelle tue attivazioni e nei tuoi percorsi.

![demo](./images/aud5.png)

Ora utilizziamo questo segmento in un’attivazione Facebook e in un percorso di clienti.

## 4.6.3 Utilizzare il segmento in Real-Time CDP in tempo reale

In Adobe Experience Platform, vai a **Segmenti > Sfoglia** e trova il pubblico che hai creato in CJA:

![demo](./images/aud6.png)

Fai clic sul segmento, quindi fai clic su **Attiva nella destinazione**:

![demo](./images/aud7.png)

Selezionare la destinazione denominata **bootcamp-facebook**, quindi fare clic su **Next**.

![demo](./images/aud8.png)

Fai di nuovo clic su **Avanti**.

![demo](./images/aud9.png)

Seleziona l&#39;opzione **Origine del pubblico** e impostala su **Direttamente dai clienti**, quindi fai clic su **Avanti**.

![demo](./images/aud10.png)

Fai clic su **Fine**.

![demo](./images/aud11.png)

Il segmento è ora connesso ai tipi di pubblico personalizzati di Facebook. Ora utilizziamo lo stesso segmento in Adobe Journey Optimizer.

## 4.6.4 Utilizzare il segmento in Adobe Journey Optimizer

In Adobe Experience Platform, fare clic su **Journey Optimizer**, quindi nel menu a sinistra fare clic su **Percorsi** e iniziare a creare un percorso facendo clic su **Crea Percorso**.

![demo](./images/aud20.png)

![demo](./images/aud21.png)

![demo](./images/aud22.png)

Quindi, nel menu a sinistra, in **Eventi**, seleziona **Qualifica segmento** e trascinalo nel percorso:

![demo](./images/aud23.png)

In Segmento fare clic su **Modifica** per selezionare un segmento:

![demo](./images/aud24.png)

Seleziona il pubblico creato in precedenza in CJA e fai clic su **Salva**.

![demo](./images/aud25.png)

Pronti! Da qui puoi creare un percorso per i clienti idonei per questo segmento.

[Torna a Flusso utente 4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)
