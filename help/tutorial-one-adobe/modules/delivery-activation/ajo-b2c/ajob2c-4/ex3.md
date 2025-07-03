---
title: 'Adobe Journey Optimizer: applicare la personalizzazione a un messaggio e-mail'
description: Questo esercizio spiega come utilizzare la personalizzazione dei segmenti all’interno di un contenuto e-mail
kt: 5342
doc-type: tutorial
exl-id: a1ad649e-d0c4-4e87-b784-1e2d99f34a2e
source-git-commit: 203590e3289d2e5342085bf8b6b4e3cd11859539
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---

# 3.4.3 Applicare la personalizzazione basata sui segmenti in un messaggio e-mail

Accedi a Adobe Experience Cloud da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Adobe Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepTenantId--``.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## Personalizzazione basata su 3.4.3.1 segmenti

In questo esercizio migliorerai il messaggio e-mail per la newsletter creato nell’esercizio precedente con un testo personalizzato in base all’iscrizione al segmento.

Vai a **Campagne**. Trova il percorso di newsletter creato nell’esercizio precedente. Cerca `--aepUserLdap-- - CitiSignal Newsletter`. Fare clic con il pulsante destro del mouse sui tre punti **...** e scegliere **Duplica**.

![Journey Optimizer](./images/sbp1.png)

Poi vedrai questo. Utilizza questo per il **titolo**: `--aepUserLdap-- - CitiSignal Newsletter (SBP)`. Fai clic su **Duplica**.

![Journey Optimizer](./images/sbp2.png)

Fai clic sulla campagna duplicata per aprirla.

![Journey Optimizer](./images/sbp3.png)

Fai clic su **Modifica** per modificare il contenuto.

![Journey Optimizer](./images/sbp3a.png)

Fai clic su **Modifica corpo dell&#39;e-mail**.

![Journey Optimizer](./images/sbp4.png)

Poi vedrai questo.

![Journey Optimizer](./images/sbp5.png)

Apri **Componenti contenuto** e trascina una **colonna 1:1** sopra l&#39;offerta AirPods.

![Journey Optimizer](./images/sbp6.png)

Trascina e rilascia un componente **Testo** nella colonna 1:1.

![Journey Optimizer](./images/sbp6a.png)

Selezionare l&#39;intero testo predefinito ed eliminarlo. Quindi fare clic sul pulsante **Aggiungi personalizzazione** nella barra degli strumenti.

![Journey Optimizer](./images/sbp7.png)

Poi vedrai questo. Nel menu a sinistra, fai clic su **Tipi di pubblico**.

![Journey Optimizer](./images/seg1.png)

Selezionare il segmento `--aepUserLdap-- - Interest in Plans` e fare clic sull&#39;icona **+** per aggiungerlo all&#39;area di lavoro.

![Journey Optimizer](./images/seg3.png)

Lasciare quindi invariata la prima riga e sostituire le righe 2 e 3 con questo codice:

&grave;&grave;
    PS: It may be a good idea to check if your plan still meets your needs! Click here to be contacted by one of our experts!
{%else%}
    PS: Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: NEWSLETTER10
{%/if%}
&grave;&grave;

Allora avrai questo. Fai clic su **Salva**.

![Journey Optimizer](./images/seg4.png)

Cambia l&#39;allineamento del testo in **Allineamento al centro**.

![Journey Optimizer](./images/sbp9.png)

Per salvare il messaggio, fai clic sul pulsante **Salva** nell&#39;angolo in alto a destra. Quindi, fai clic sulla **freccia** accanto al testo della riga dell&#39;oggetto nell&#39;angolo in alto a sinistra.

![Journey Optimizer](./images/sbp9a.png)

Fai clic su **Rivedi per attivare**.

![Journey Optimizer](./images/oc79afff.png)

Fare clic su **Attiva**.

![Journey Optimizer](./images/oc79bfff.png)

È ora pubblicata la newsletter con personalizzazione basata sui segmenti. Il messaggio e-mail della newsletter verrà inviato in base alla pianificazione e il percorso verrà interrotto non appena l’ultima e-mail sarà stata inviata.

Se ti qualifichi per il segmento utilizzato, lo vedrai nell’e-mail che riceverai:

![Journey Optimizer](./images/sbp20fff.png)

Hai finito questo esercizio.

## Passaggi successivi

Vai a [Riepilogo e vantaggi](./summary.md){target="_blank"}

Torna a [Adobe Journey Optimizer](journeyoptimizer.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
