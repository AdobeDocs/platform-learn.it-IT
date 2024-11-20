---
title: Real-time CDP - Creare un pubblico e intervenire - Creare un pubblico
description: Real-time CDP - Creare un pubblico e intervenire - Creare un pubblico
kt: 5342
doc-type: tutorial
exl-id: a46b1640-769d-4fb3-97e6-beaf9706efbf
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 2%

---

# 2.3.1 Creare un pubblico

In questo esercizio creerai un pubblico utilizzando il generatore di pubblico di Adobe Experience Platform.

## Contesto

Rispondere agli interessi di un cliente deve essere in tempo reale. Uno dei modi per rispondere al comportamento dei clienti in tempo reale è utilizzare un pubblico, a condizione che il pubblico si qualifichi in tempo reale. In questo esercizio, devi creare un pubblico, tenendo conto dell’attività reale sul sito web che abbiamo utilizzato.

## Identificare il comportamento a cui si desidera reagire

Vai a [https://dsn.adobe.com](https://dsn.adobe.com). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sui tre punti **...** del progetto del sito Web, quindi fai clic su **Esegui** per aprirlo.

![DSN](./../../datacollection/module1.1/images/web8.png)

Poi vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Incolla l’URL del sito web demo, che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l’accesso con il tuo Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Seleziona il tipo di account e completa la procedura di accesso.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Vedrai quindi il tuo sito web caricato in una finestra del browser in incognito. Per ogni esercizio, dovrai utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

In questo esempio, desideri rispondere a un cliente specifico che visualizza un prodotto specifico.
Dalla home page di **Citi Signal**, vai a **Telefoni e dispositivi** e fai clic sul prodotto **Galaxy S24**.

![Acquisizione dei dati](./images/homegalaxy.png)

Quindi, quando qualcuno visita la pagina del prodotto per **Galaxy S24**, vuoi poter intervenire. La prima cosa da fare per agire è definire un pubblico.

![Acquisizione dei dati](./images/homegalaxy1.png)

## Creare il pubblico

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. Dopo aver selezionato la [!UICONTROL sandbox] appropriata, la schermata verrà modificata e ora sei nella [!UICONTROL sandbox] dedicata.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/sb1.png)

Nel menu a sinistra, vai a **Tipi di pubblico** e quindi vai a **Sfoglia** dove puoi vedere una panoramica di tutti i tipi di pubblico esistenti. Fai clic sul pulsante **Crea pubblico** per iniziare a creare un nuovo pubblico.

![Segmentazione](./images/menuseg.png)

Seleziona **Genera regola** e fai clic su **Crea**.

![Segmentazione](./images/menuseg1.png)

Come accennato in precedenza, è necessario creare un pubblico tra tutti i clienti che hanno visualizzato il prodotto **Galaxy S24**.

Per creare questo pubblico, devi aggiungere un evento. Per trovare tutti gli eventi, fai clic sull&#39;icona **Eventi** nella barra dei menu **Tipi di pubblico**.

Successivamente verrà visualizzato il nodo principale **XDM ExperienceEvent**.

Per trovare i clienti che hanno visitato il prodotto **Galaxy S24**, fai clic su **XDM ExperienceEvent**.

![Segmentazione](./images/findee.png)

Scorri verso il basso fino a **Elementi elenco prodotti** e fai clic su di esso.

![Segmentazione](./images/see.png)

Seleziona **Nome** e trascina l&#39;oggetto **Nome** dal menu di sinistra **Elementi elenco prodotti** nell&#39;area di lavoro di audience builder nella sezione **Eventi**.

![Segmentazione](./images/eewebpdtlname1.png)

Il parametro di confronto deve essere **uguale a** e nel campo di input immettere `Galaxy S24`.

![Segmentazione](./images/pv.png)

Le **Regole evento** dovrebbero ora avere questo aspetto. Ogni volta che aggiungi un elemento al generatore di pubblico, puoi fare clic sul pulsante **Aggiorna stima** per ottenere una nuova stima della popolazione nel pubblico.

![Segmentazione](./images/ldap4.png)

Assegna un nome al pubblico e imposta il **metodo di valutazione** su **Edge**.

Come convenzione di denominazione, utilizza:

- `--aepUserLdap-- - Interest in Galaxy S24`

Fai clic sul pulsante **Publish** per salvare il pubblico.

![Segmentazione](./images/segmentname.png)

Ora verrai riportato alla pagina di panoramica del pubblico.

![Segmentazione](./images/savedsegment.png)

Passaggio successivo: [2.3.2 Verificare come configurare la destinazione DV360 utilizzando le destinazioni](./ex2.md)

[Torna al modulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Torna a tutti i moduli](../../../overview.md)
