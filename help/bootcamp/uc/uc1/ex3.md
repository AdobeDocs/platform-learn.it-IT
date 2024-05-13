---
title: Bootcamp - Profilo cliente in tempo reale - Creare un pubblico - Interfaccia utente
description: Bootcamp - Profilo cliente in tempo reale - Creare un pubblico - Interfaccia utente
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Audiences
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# 1.3 Creare un pubblico - Interfaccia utente

In questo esercizio creerai un pubblico utilizzando Audience Builder di Adobe Experience Platform.

## Storia

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Prima di continuare, è necessario selezionare una **sandbox**. La sandbox da selezionare è denominata ``Bootcamp``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella linea blu sopra lo schermo. Dopo aver selezionato la [!UICONTROL sandbox], verrà visualizzata la modifica dello schermo e ora si è nel [!UICONTROL sandbox].

![Acquisizione dei dati](./images/sb1.png)

Nel menu a sinistra, vai a **Tipi di pubblico**. In questa pagina vengono visualizzate dashboard con informazioni essenziali su **Pubblico** prestazioni.

![Segmentazione](./images/menuseg.png)

Fai clic su **Sfoglia** per visualizzare una panoramica di tutti i tipi di pubblico esistenti. Fai clic sul pulsante **+ Crea pubblico** per iniziare a creare un nuovo pubblico.


![Segmentazione](./images/segmentationui.png)

Verrà visualizzato un messaggio pop-ip in cui viene chiesto se si desidera **&#39;Componi pubblico&#39;** o **&#39;Genera regola&#39;**. Scegli **&#39;Genera regola&#39;** per continuare e fare clic su **creare**.

![Segmentazione][def]

Una volta entrati nel generatore di pubblico, noterai immediatamente **Attributi** e la **Profilo individuale XDM** riferimento.


Poiché XDM è il linguaggio che alimenta il business dell’esperienza, XDM è anche la base per il generatore di pubblico. Tutti i dati acquisiti in Platform devono essere mappati su XDM e, come tale, tutti i dati diventano parte dello stesso modello di dati, indipendentemente da dove provengono. Questo ti offre un grande vantaggio durante la creazione di tipi di pubblico; infatti, da questa interfaccia utente di audience builder puoi combinare dati di qualsiasi origine nello stesso flusso di lavoro. I tipi di pubblico generati in Audience Builder possono essere inviati a soluzioni come Adobe Target, Adobe Campaign o qualsiasi altro canale di attivazione.

Ora devi creare un pubblico di tutti i clienti che hanno visualizzato il prodotto **Real-Time CDP**.

Per creare questo pubblico, devi aggiungere un evento esperienza. Puoi trovare tutti gli eventi esperienza facendo clic sul pulsante **Eventi** icona in **Campi** barra dei menu.

![Segmentazione](./images/findee.png)

Poi, vedrai il livello superiore, **XDM ExperienceEvents** nodo. Fai clic su **XDM ExperienceEvent**.

![Segmentazione](./images/see.png)

Vai a **Elementi elenco prodotti**.

![Segmentazione](./images/plitems.png)

Seleziona **Nome** e trascina **Nome** dal menu a sinistra all&#39;area di lavoro di audience builder nel **Eventi** sezione. A questo punto viene visualizzato quanto segue:

![Segmentazione](./images/eewebpdtlname.png)

Il parametro di confronto deve essere **è uguale a** e nel campo di immissione, immetti **Real-time CDP**.

![Segmentazione](./images/pv.png)

Ogni volta che aggiungi un elemento al generatore di pubblico, puoi fare clic sul pulsante **Aggiorna stima** per ottenere una nuova stima della popolazione nel pubblico.

![Segmentazione](./images/refreshest.png)

As **Metodo di valutazione**, seleziona **Bordo**.

![Segmentazione](./images/evedge.png)

Infine, diamo un nome al pubblico e salvalo.

Come convenzione di denominazione, utilizza:

- `yourLastName - Interest in Real-Time CDP`

Quindi, fai clic su **Salva e chiudi** per salvare il pubblico.

![Segmentazione](./images/segmentname.png)

Ora viene visualizzata la pagina di panoramica del pubblico, in cui è disponibile un’anteprima di esempio dei profili cliente idonei per il pubblico.

![Segmentazione](./images/savedsegment.png)

Ora puoi continuare con l’esercizio successivo e utilizzare il pubblico con Adobe Target.

Passaggio successivo: [1.4 Intervenire: inviare il pubblico ad Adobe Target](./ex4.md)

[Torna a Flusso utente 1](./uc1.md)

[Torna a tutti i moduli](../../overview.md)


[def]: ./images/segmentationpopup.png
