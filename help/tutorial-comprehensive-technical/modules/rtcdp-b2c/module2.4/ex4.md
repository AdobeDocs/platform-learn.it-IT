---
title: 'Audience Activation dell’hub eventi di Microsoft Azure: creazione di un pubblico'
description: 'Audience Activation dell’hub eventi di Microsoft Azure: creazione di un pubblico'
kt: 5342
doc-type: tutorial
exl-id: 56f6a6dc-82aa-4b64-a3f6-b6f59c484ccb
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

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

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. Dopo aver selezionato la sandbox appropriata, la schermata cambia e ora sei nella sandbox dedicata.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/sb1.png)

Vai a **Tipi di pubblico**. Fare clic sul pulsante **+ Crea pubblico**.

![Acquisizione dei dati](./images/seg.png)

Seleziona **Genera regola** e fai clic su **Crea**.

![Acquisizione dei dati](./images/seg1.png)

Assegna un nome al pubblico `--aepUserLdap-- - Interest in Plans`, imposta il metodo di valutazione su **Edge** e aggiungi il nome della pagina dall&#39;evento esperienza.

Fai clic su **Eventi** e trascina **XDM ExperienceEvent > Web > Dettagli pagina Web > Nome**. Immetti **piani** come valore:

![4-05-create-ee-2.png](./images/405createee2.png)

Trascina e rilascia **XDM ExperienceEvent > `--aepTenantId--` > demoEnvironment > brandName**. Immetti `--aepUserLdap--` come valore, imposta il parametro di confronto su **contains** e fai clic su **Publish**:

![4-05-create-ee-2-brand.png](./images/405createee2brand.png)

Il pubblico è ora pubblicato.

![4-05-create-ee-2-brand.png](./images/405createee2brand1.png)

Passaggio successivo: [2.4.5 Attiva il pubblico](./ex5.md)

[Torna al modulo 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Torna a tutti i moduli](./../../../overview.md)
