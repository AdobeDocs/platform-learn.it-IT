---
title: Bootcamp - Real-time CDP - Crea un segmento e interviene - Invia il segmento ad Adobe Target
description: Bootcamp - Real-time CDP - Crea un segmento e interviene - Invia il segmento ad Adobe Target
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 6a76c2ab-96b7-4626-a6d3-afd555220b1e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 1%

---

# 1.4 Intervenire: inviare il segmento ad Adobe Target

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l&#39;accesso, si aprirà la homepage di Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Prima di continuare, devi selezionare un **sandbox**. La sandbox da selezionare è denominata ``Bootcamp``. Per eseguire questa operazione, fai clic sul testo **[!UICONTROL Produzione Prod]** nella linea blu sopra lo schermo. Dopo aver selezionato il [!UICONTROL sandbox], vedrai la modifica dello schermo e ora sei nel tuo dedicato [!UICONTROL sandbox].

![Acquisizione dei dati](./images/sb1.png)

## 1.4.1 Attiva il segmento nella destinazione Adobe Target

Adobe Target è disponibile come destinazione da Real-Time CDP. Per configurare l’integrazione di Adobe Target, passa a **Destinazioni**, a **Catalogo**.

Fai clic su **Personalizzazione** in **Categorie** menu. Vedrai il **Adobe Target** scheda di destinazione. Fai clic su **Attiva segmenti**.

![AT](./images/atdest1.png)

Selezionare la destinazione ``Bootcamp Target`` e fai clic su **Successivo**.

![AT](./images/atdest3.png)

Nell’elenco dei segmenti disponibili, seleziona il segmento creato in [1.3 Creare un segmento](./ex3.md), denominato `yourLastName - Interest in Real-Time CDP`. Quindi, fai clic su **Successivo**.

![AT](./images/atdest8.png)

Nella pagina successiva, fai clic su **Successivo**.

![AT](./images/atdest9.png)

Fai clic su **Fine**.

![AT](./images/atdest10.png)

Il segmento viene ora attivato in Adobe Target.

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>Una volta creata la destinazione Adobe Target in Real-Time CDP, potrebbe essere necessaria fino a un&#39;ora per rendere live la destinazione. Questo è un tempo di attesa una tantum, a causa della configurazione della configurazione del backend. Una volta completata la configurazione iniziale di attesa e back-end di 1 ora, i nuovi segmenti edge aggiunti alla destinazione Adobe Target saranno disponibili per il targeting in tempo reale.

## 1.4.2 Configurare l’attività basata su moduli di Adobe Target

Ora che il segmento Real-Time CDP è configurato per l’invio ad Adobe Target, puoi configurare l’attività Targeting esperienza in Adobe Target. In questo esercizio configurerai un’attività basata su Compositore esperienza visivo.

Vai alla home page di Adobe Experience Cloud andando a [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Fai clic su **Target** per aprirlo.

![RTCDP](./images/excl.png)

Sulla **Adobe Target** nella home page verranno visualizzate tutte le attività esistenti.
Fai clic su **+ Crea attività** per creare una nuova attività.

![RTCDP](./images/exclatov.png)

Seleziona **Targeting esperienza**.

![RTCDP](./images/exclatcrxt.png)

Seleziona **Visivo** e imposta **URL attività** a `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, ma prima di farlo, sostituisci XX con un numero compreso tra 01 e 30.

>[!IMPORTANT]
>
>Ogni partecipante all’abilitazione deve utilizzare una pagina web separata per evitare il conflitto tra diverse esperienze Adobe Target. Puoi scegliere una pagina web e trovare l’URL facendo clic qui: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Tutte le pagine condividono lo stesso URL di base e terminano con il numero del partecipante.
>
>Ad esempio, il partecipante 1 deve utilizzare l’URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, il partecipante 30 deve utilizzare l’URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

Selezionare l’area di lavoro **AT Bootcamp**.

Fai clic su **Avanti**.

![RTCDP](./images/exclatcrxtdtlform.png)

Ora ti trovi nel Compositore esperienza visivo. Potrebbero essere necessari 20-30 secondi fino a quando il sito web non è completamente caricato.

![RTCDP](./images/atform1.png)

Il pubblico predefinito è attualmente **Tutti i visitatori**. Fai clic sul pulsante **3 punti** accanto a **Tutti i visitatori** e fai clic su **Cambia pubblico**.

![RTCDP](./images/atform3.png)

Ora visualizzi l’elenco dei tipi di pubblico disponibili e il segmento Adobe Experience Platform creato in precedenza e inviato ad Adobe Target fa parte di questo elenco. Seleziona il segmento creato in precedenza in Adobe Experience Platform. Fai clic su **Assegna pubblico**.

![RTCDP](./images/exclatvecchaud.png)

Il segmento Adobe Experience Platform fa ora parte di questa attività di targeting delle esperienze.

![RTCDP](./images/atform4.png)

Prima di poter modificare l&#39;immagine protagonista, dovrai fare clic su **Consenti tutto** sul banner cookie.

Per farlo, vai a **Sfoglia**

![RTCDP](./images/cook1.png)

Quindi, fai clic su **Consenti tutto**.

![RTCDP](./images/cook2.png)

Quindi, torna a **Componi**.

![RTCDP](./images/cook3.png)

Ora cambiamo l&#39;immagine protagonista sulla homepage del sito web. Fai clic sull’immagine protagonista predefinita sul sito web, quindi fai clic su **Sostituisci contenuto** quindi seleziona **Immagine**.

![RTCDP](./images/atform5.png)

Ricerca del file di immagine **rtcdp.png**. Selezionalo e fai clic su **Salva**.

![RTCDP](./images/atform6.png)

Verrà quindi visualizzata la nuova esperienza con la nuova immagine, per il pubblico selezionato.

![RTCDP](./images/atform7.png)

Fai clic sul titolo dell’attività nell’angolo in alto a sinistra per rinominarla.

![RTCDP](./images/exclatvecname.png)

Per il nome, utilizzare:

- `yourLastName - RTCDP - XT (VEC)`

Fai clic su **Avanti**.

![RTCDP](./images/atform8.png)

Fai clic su **Avanti**.

![RTCDP](./images/atform8a.png)

Sulla **Obiettivi e impostazioni** - pagina, vai a **Metriche dell&#39;obiettivo**.

![RTCDP](./images/atform9.png)

Imposta l&#39;obiettivo principale su **Coinvolgimento** - **Time On Site**. Fai clic su **Salva e chiudi**.

![RTCDP](./images/vec3.png)

Ora sei sul **Panoramica dell’attività** pagina. È comunque necessario attivare l&#39;attività.

![RTCDP](./images/atform10.png)

Fai clic sul campo **Inattivo** e seleziona **Attiva**.

![RTCDP](./images/atform11.png)

Otterrai quindi una conferma visiva del fatto che l’attività è ora in diretta.

![RTCDP](./images/atform12.png)

La tua attività è ora live e può essere testata sul sito web del bootcamp.

Se ora ritorni al tuo sito web dimostrativo e visita la pagina del prodotto per **Real-Time CDP**, ti qualificherai immediatamente per il segmento creato e vedrai l’attività Adobe Target essere visualizzata sulla home page in tempo reale.

>[!IMPORTANT]
>
>Ogni partecipante all’abilitazione deve utilizzare una pagina web separata per evitare il conflitto tra diverse esperienze Adobe Target. Puoi scegliere una pagina web e trovare l’URL facendo clic qui: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Tutte le pagine condividono lo stesso URL di base e terminano con il numero del partecipante.
>
>Ad esempio, il partecipante 1 deve utilizzare l’URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, il partecipante 30 deve utilizzare l’URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Passaggio successivo: [1.5 Intervenire: inviare il segmento a Facebook](./ex5.md)

[Torna al flusso utente 1](./uc1.md)

[Torna a tutti i moduli](../../overview.md)
