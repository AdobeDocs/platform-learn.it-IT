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

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``Bootcamp``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella riga blu nella parte superiore dello schermo. Dopo aver selezionato la [!UICONTROL sandbox] appropriata, la schermata verrà modificata e ora sei nella [!UICONTROL sandbox] dedicata.

![Acquisizione dei dati](./images/sb1.png)

Nel menu a sinistra, vai a **Tipi di pubblico**. In questa pagina verranno visualizzate dashboard con informazioni essenziali sulle prestazioni di **Audience**.

![Segmentazione](./images/menuseg.png)

Fai clic su **Sfoglia** per visualizzare una panoramica di tutti i tipi di pubblico esistenti. Fai clic sul pulsante **+ Crea pubblico** per iniziare a creare un nuovo pubblico.


![Segmentazione](./images/segmentationui.png)

Verrà visualizzato un pop-ip che ti chiederà se desideri **&#39;Componi pubblico&#39;** o **&#39;Genera regola&#39;**. Scegliere **&#39;Genera regola&#39;** per continuare e fare clic su **crea**.

![Segmentazione][def]

Quando ti trovi nel generatore di tipi di pubblico, noterai immediatamente l&#39;opzione di menu **Attributi** e il riferimento a **Profilo individuale XDM**.


Poiché XDM è il linguaggio che alimenta il business dell’esperienza, XDM è anche la base per il generatore di pubblico. Tutti i dati acquisiti in Platform devono essere mappati su XDM e, come tale, tutti i dati diventano parte dello stesso modello di dati, indipendentemente da dove provengono. Questo ti offre un grande vantaggio durante la creazione di tipi di pubblico; infatti, da questa interfaccia utente di audience builder puoi combinare dati di qualsiasi origine nello stesso flusso di lavoro. I tipi di pubblico generati in Audience Builder possono essere inviati a soluzioni come Adobe Target, Adobe Campaign o qualsiasi altro canale di attivazione.

È ora necessario creare un pubblico di tutti i clienti che hanno visualizzato il prodotto **Real-Time CDP**.

Per creare questo pubblico, devi aggiungere un evento esperienza. Per trovare tutti gli eventi esperienza, fai clic sull&#39;icona **Eventi** nella barra dei menu **Campi**.

![Segmentazione](./images/findee.png)

Verrà visualizzato il nodo principale **XDM ExperienceEvents**. Fai clic su **XDM ExperienceEvent**.

![Segmentazione](./images/see.png)

Vai a **Elementi elenco prodotti**.

![Segmentazione](./images/plitems.png)

Seleziona **Name** e trascina l&#39;oggetto **Name** dal menu a sinistra nell&#39;area di lavoro di audience builder nella sezione **Events**. A questo punto viene visualizzato quanto segue:

![Segmentazione](./images/eewebpdtlname.png)

Il parametro di confronto deve essere **uguale a** e nel campo di input immettere **Real-time CDP**.

![Segmentazione](./images/pv.png)

Ogni volta che aggiungi un elemento al generatore di pubblico, puoi fare clic sul pulsante **Aggiorna stima** per ottenere una nuova stima della popolazione nel pubblico.

![Segmentazione](./images/refreshest.png)

Come **Metodo di valutazione**, selezionare **Edge**.

![Segmentazione](./images/evedge.png)

Infine, diamo un nome al pubblico e salvalo.

Come convenzione di denominazione, utilizza:

- `yourLastName - Interest in Real-Time CDP`

Quindi, fai clic sul pulsante **Salva e chiudi** per salvare il pubblico.

![Segmentazione](./images/segmentname.png)

Ora viene visualizzata la pagina di panoramica del pubblico, in cui è disponibile un’anteprima di esempio dei profili cliente idonei per il pubblico.

![Segmentazione](./images/savedsegment.png)

Ora puoi continuare con l’esercizio successivo e utilizzare il pubblico con Adobe Target.

Passaggio successivo: [1.4 Azione: inviare il pubblico ad Adobe Target](./ex4.md)

[Torna a Flusso utente 1](./uc1.md)

[Torna a tutti i moduli](../../overview.md)


[def]: ./images/segmentationpopup.png
