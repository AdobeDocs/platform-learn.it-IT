---
title: 'Hub eventi da Audience Activation a Microsoft Azure: creazione di un pubblico'
description: 'Hub eventi da Audience Activation a Microsoft Azure: creazione di un pubblico'
kt: 5342
doc-type: tutorial
exl-id: d9450e18-7c9b-4a6c-8317-19baf99d43a3
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 3%

---

# 2.4.4 Creare un pubblico

## Introduzione

Puoi creare un pubblico semplice:

- **Interesse nei piani** per i quali i clienti si qualificheranno quando visitano la pagina **Piani** del sito Web di dimostrazione di CitiSignal.

### Buono a sapersi

Real-Time CDP attiva un&#39;attivazione su una destinazione quando ti qualifichi per un pubblico che fa parte dell&#39;elenco di attivazione di tale destinazione. In questo caso, il payload di qualificazione del pubblico che verrà inviato a tale destinazione conterrà **tutti i tipi di pubblico per i quali è qualificato il profilo cliente**.

L’obiettivo di questo modulo è mostrare che la qualificazione del pubblico del tuo profilo cliente viene inviata alla destinazione dell’hub eventi in tempo reale.

### Stato del pubblico

Una qualifica di pubblico in Adobe Experience Platform ha sempre una proprietà **status** e può essere una delle seguenti:

- **realized**: indica una nuova qualifica per il pubblico
- **uscita**: indica che il profilo non è più idoneo per il pubblico

## Creare il pubblico

Accedi a Adobe Experience Platform da questo URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. Dopo aver selezionato la sandbox appropriata, la schermata cambia e ora sei nella sandbox dedicata.

![Acquisizione dei dati](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Vai a **Tipi di pubblico**. Fare clic sul pulsante **+ Crea pubblico**.

![Acquisizione dei dati](./images/seg.png)

Seleziona **Genera regola** e fai clic su **Crea**.

![Acquisizione dei dati](./images/seg1.png)

Assegna un nome al pubblico `--aepUserLdap-- - Interest in Plans`, imposta il metodo di valutazione su **Edge** e aggiungi il nome della pagina dall&#39;evento esperienza.

Fai clic su **Eventi** e trascina **XDM ExperienceEvent > Web > Dettagli pagina Web > Nome**. Immetti **piani** come valore:

![4-05-create-ee-2.png](./images/405createee2.png)

Trascina e rilascia **XDM ExperienceEvent > `--aepTenantId--` > demoEnvironment > brandName**. Immetti `--aepUserLdap--` come valore, imposta il parametro di confronto su **contains** e fai clic su **Pubblica**:

![4-05-create-ee-2-brand.png](./images/405createee2brand.png)

Il pubblico è ora pubblicato.

![4-05-create-ee-2-brand.png](./images/405createee2brand1.png)

## Passaggi successivi

Vai a [2.4.5 Attiva il pubblico](./ex5.md){target="_blank"}

Torna a [Real-Time CDP: da Audience Activation a Microsoft Azure Event Hub](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
