---
title: Real-time CDP - Creare un segmento e intervenire - Creare un segmento
description: Real-time CDP - Creare un segmento e intervenire - Creare un segmento
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 2%

---

# 2.3.1 Creare un segmento

In questo esercizio creerai un segmento utilizzando il Generatore di segmenti di Adobe Experience Platform.

## 2.3.1.1 Contesto

Nel mondo di oggi, la risposta al comportamento di un cliente deve essere in tempo reale. Uno dei modi per rispondere al comportamento del cliente in tempo reale è quello di utilizzare un segmento, a condizione che il segmento si qualifichi in tempo reale. In questo esercizio, devi creare un segmento, tenendo conto delle attività reali sul sito web che abbiamo utilizzato.

## 2.3.1.2 Identificare il comportamento a cui si desidera reagire

Vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

Ora puoi seguire il flusso seguente per accedere al sito web. Fai clic su **Integrazioni**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web1.png)

Nella pagina **Integrazioni** è necessario selezionare la proprietà Raccolta dati creata nell&#39;esercizio 0.1.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web2.png)

Poi vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

Incolla l’URL del sito web demo, che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l’accesso con il tuo Adobe ID.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

Seleziona il tipo di account e completa la procedura di accesso.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

Vedrai quindi il tuo sito web caricato in una finestra del browser in incognito. Per ogni dimostrazione, dovrai utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

In questo esempio, desideri rispondere a un cliente specifico che visualizza un prodotto specifico.
Dalla home page di **Luma**, vai a **Men** e fai clic sul prodotto **CAMICIA FITNESS PROTEUS**.

![Acquisizione dei dati](./images/homenadia.png)

Quindi, quando qualcuno visita la pagina del prodotto **PROTEUS FITNESS JACKSHIRT**, vuoi essere in grado di intervenire. La prima cosa da fare per intervenire è definire un segmento.

![Acquisizione dei dati](./images/homenadiapp.png)

## 2.3.1.3 Creare il segmento

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella riga blu nella parte superiore dello schermo. Dopo aver selezionato la [!UICONTROL sandbox] appropriata, la schermata verrà modificata e ora sei nella [!UICONTROL sandbox] dedicata.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/sb1.png)

Nel menu a sinistra, vai a **Segmenti** e poi a **Sfoglia** dove puoi vedere una panoramica di tutti i segmenti esistenti. Fai clic sul pulsante **Crea segmento** per iniziare a creare un nuovo segmento.

![Segmentazione](./images/menuseg.png)

Come accennato in precedenza, devi creare un segmento tra tutti i clienti che hanno visualizzato il prodotto **PROTEUS FITNESS JACKSHIRT**.

Per creare questo segmento, devi aggiungere un evento. Per trovare tutti gli eventi, fai clic sull&#39;icona **Eventi** nella barra dei menu **Segmenti**.

Successivamente verrà visualizzato il nodo principale **XDM ExperienceEvent**.

Per trovare i clienti che hanno visitato il prodotto **PROTEUS FITNESS JACKSHIRT**, fai clic su **XDM ExperienceEvent**.

![Segmentazione](./images/findee.png)

Scorri verso il basso fino a **Elementi elenco prodotti** e fai clic su di esso.

![Segmentazione](./images/see.png)

Seleziona **Nome** e trascina l&#39;oggetto **Nome** dal menu di sinistra **Elementi elenco prodotti** nell&#39;area di lavoro del Generatore di segmenti nella sezione **Eventi**.

![Segmentazione](./images/eewebpdtlname1.png)

Il parametro di confronto deve essere **uguale a** e nel campo di input immettere `PROTEUS FITNESS JACKSHIRT`.

![Segmentazione](./images/pv.png)

Le **Regole evento** dovrebbero ora avere questo aspetto. Ogni volta che aggiungi un elemento al generatore di segmenti, puoi fare clic sul pulsante **Aggiorna stima** per ottenere una nuova stima della popolazione nel segmento.

![Segmentazione](./images/ldap4.png)

Infine, diamo un nome al segmento e salvalo.

Come convenzione di denominazione, utilizza:

- `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`

Il nome del segmento deve essere simile al seguente:
`vangeluw - Interest in PROTEUS FITNESS JACKSHIRT`

Fai clic sul pulsante **Salva e chiudi** per salvare il segmento.

![Segmentazione](./images/segmentname.png)

Ora tornerai alla pagina di panoramica dei segmenti.

![Segmentazione](./images/savedsegment.png)

Passaggio successivo: [2.3.2 Verificare come configurare la destinazione DV360 utilizzando le destinazioni](./ex2.md)

[Torna al modulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Torna a tutti i moduli](../../../overview.md)
