---
title: Bootcamp - Profilo cliente in tempo reale - Creare un segmento - Interfaccia utente
description: Bootcamp - Profilo cliente in tempo reale - Creare un segmento - Interfaccia utente
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 3%

---

# 1.3 Creare un segmento - Interfaccia utente

In questo esercizio creerai un segmento utilizzando il Generatore di segmenti di Adobe Experience Platform.

## Storia

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l&#39;accesso, si aprirà la homepage di Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``Bootcamp``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo. Dopo aver selezionato il [!UICONTROL sandbox], vedrai la modifica dello schermo e ora sei nel tuo dedicato [!UICONTROL sandbox].

![Acquisizione dei dati](./images/sb1.png)

Nel menu a sinistra, vai a **Segmenti**. In questa pagina puoi vedere una panoramica di tutti i segmenti esistenti. Fai clic sul pulsante **+ Crea segmento** per iniziare a creare un nuovo segmento.

![Segmentazione](./images/menuseg.png)

Una volta entrato nel nuovo generatore di segmenti, noterai immediatamente il **Attributi** l&#39;opzione di menu e **Profilo individuale XDM** riferimento.

![Segmentazione](./images/segmentationui.png)

Poiché XDM è il linguaggio che attiva l’attività di esperienza, XDM è anche la base per il generatore di segmenti. Tutti i dati acquisiti in Platform devono essere mappati su XDM e, di conseguenza, tutti i dati diventano parte dello stesso modello di dati, indipendentemente da dove provengono. Questo ti offre un grande vantaggio nella creazione di segmenti, poiché da questa interfaccia utente del generatore di segmenti puoi combinare dati di qualsiasi origine nello stesso flusso di lavoro. I segmenti generati nel Generatore di segmenti possono essere inviati a soluzioni come Adobe Target, Adobe Campaign e Adobe Audience Manager per l’attivazione.

Ora devi creare un segmento di tutti i clienti che hanno visualizzato il prodotto **Real-Time CDP**.

Per creare questo segmento, devi aggiungere un evento esperienza. Per trovare tutti gli eventi di esperienza, fai clic sul pulsante **Eventi** nella **Campi** barra dei menu.

![Segmentazione](./images/findee.png)

Ora, vedrai il livello superiore, **Eventi esperienza XDM** nodo. Fai clic su **ExperienceEvent XDM**.

![Segmentazione](./images/see.png)

Vai a **Elementi elenco prodotti**.

![Segmentazione](./images/plitems.png)

Seleziona **Nome** e trascina e rilascia la **Nome** dal menu di sinistra nell’area di lavoro del generatore di segmenti nel **Eventi** sezione . Vedrai questo:

![Segmentazione](./images/eewebpdtlname.png)

Il parametro di confronto deve essere **è** e nel campo di immissione immettere **Real-time CDP**.

![Segmentazione](./images/pv.png)

Ogni volta che aggiungi un elemento al generatore di segmenti, puoi fare clic sul pulsante **Aggiorna stima** per ottenere una nuova stima della popolazione nel segmento.

![Segmentazione](./images/refreshest.png)

Come **Metodo di valutazione**, seleziona **Bordo**.

![Segmentazione](./images/evedge.png)

Infine, diamo un nome al segmento e salvalo.

Come convenzione di denominazione, utilizza:

- `yourLastName - Interest in Real-Time CDP`

Quindi, fai clic sul pulsante **Salva e chiudi** per salvare il segmento.

![Segmentazione](./images/segmentname.png)

Verrai reindirizzato alla pagina di panoramica dei segmenti, dove vedrai un esempio di anteprima dei profili dei clienti idonei per il tuo segmento.

![Segmentazione](./images/savedsegment.png)

Ora puoi continuare l’esercizio successivo e utilizzare il segmento con Adobe Target.

Passaggio successivo: [1.4 Intervenire: inviare il segmento ad Adobe Target](./ex4.md)

[Torna al flusso utente 1](./uc1.md)

[Torna a tutti i moduli](../../overview.md)
