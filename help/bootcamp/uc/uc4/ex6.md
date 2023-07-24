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
source-wordcount: '409'
ht-degree: 0%

---

# 4.6 Da informazioni approfondite ad azioni

## Obiettivi

- Come creare un pubblico in base a una visualizzazione raccolta nel Customer Journey Analytics
- Utilizza questo pubblico in Real-Time CDP e Adobe Journey Optimizer

## 4.6.1 Creare un pubblico e pubblicarlo

Nel tuo progetto, hai creato un filtro denominato **Sentimenti di chiamata** ed è stato in grado di visualizzare il numero di utenti per i quali le chiamate al call center erano classificate come **positivo**. Ora potrai creare un segmento con questi utenti e attivarli in percorsi o canali di comunicazione.

Il primo passaggio consiste nel selezionare una linea nel pannello creato nell&#39;ultimo esercizio **1. Sentimento di chiamata - Positivo**, fare clic con il pulsante destro del mouse e selezionare **Creare un pubblico dalla selezione** opzione:

![demo](./images/aud1.png)

Quindi, assegna un nome al pubblico seguendo il modello **yourLastName - La chiamata del pubblico di CJA si sente positiva**:

![demo](./images/aud2.png)

Tieni presente che è possibile avere un’anteprima del pubblico che viene creato:

![demo](./images/aud3.png)

Infine, fai clic su **Pubblica**.

![demo](./images/aud4.png)

## 4.6.2 Utilizzare il pubblico come parte di un segmento

Torna al Adobe Experience Platform, vai a **Segmenti > Sfoglia** e potrai vedere il segmento creato in CJA pronto e disponibile per essere utilizzato nelle attivazioni e nei percorsi.

![demo](./images/aud5.png)

Ora utilizziamo questo segmento in un’attivazione Facebook e in un percorso di clienti.

## 4.6.3 Utilizzare il segmento in Real-Time CDP in tempo reale

In Adobe Experience Platform, vai a **Segmenti > Sfoglia** e trova il pubblico che hai creato in CJA:

![demo](./images/aud6.png)

Fai clic sul segmento, quindi fai clic su **Attiva nella destinazione**:

![demo](./images/aud7.png)

Seleziona la destinazione denominata **bootcamp-facebook** e quindi fare clic su **Successivo**.

![demo](./images/aud8.png)

Clic **Successivo** di nuovo.

![demo](./images/aud9.png)

Seleziona la **Origine del pubblico** e impostarla su **Direttamente dai clienti**, fai clic su **Successivo**.

![demo](./images/aud10.png)

Fai clic su **Fine**.

![demo](./images/aud11.png)

Il segmento è ora connesso ai tipi di pubblico personalizzati di Facebook. Ora utilizziamo lo stesso segmento in Adobe Journey Optimizer.

## 4.6.4 Utilizzare il segmento in Adobe Journey Optimizer

In Adobe Experience Platform, fai clic su **Journey Optimizer**, quindi nel menu a sinistra fare clic su **Percorsi** e iniziare a creare un percorso facendo clic su **Crea Percorso**.

![demo](./images/aud20.png)

![demo](./images/aud21.png)

![demo](./images/aud22.png)

Quindi, nel menu a sinistra, sotto **Eventi**, seleziona **Qualificazione del segmento** e trascinarlo nel percorso:

![demo](./images/aud23.png)

In Segmento, fai clic su **Modifica** per selezionare un segmento:

![demo](./images/aud24.png)

Seleziona il pubblico creato in precedenza in CJA e fai clic su  **Salva**.

![demo](./images/aud25.png)

Pronti! Da qui puoi creare un percorso per i clienti idonei per questo segmento.

[Torna a Flusso utente 4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)
