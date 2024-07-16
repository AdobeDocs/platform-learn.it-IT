---
title: Bootcamp - Real-time CDP - Creare un pubblico e intervenire - Inviare il pubblico ad Adobe Target
description: Bootcamp - Real-time CDP - Creare un pubblico e intervenire - Inviare il pubblico ad Adobe Target
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
solution: Experience Platform, Target
feature: Audiences, Integrations
exl-id: 6a76c2ab-96b7-4626-a6d3-afd555220b1e
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# 1.4 Intervenire: inviare il pubblico ad Adobe Target

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``Bootcamp``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella riga blu nella parte superiore dello schermo. Dopo aver selezionato la [!UICONTROL sandbox] appropriata, la schermata verrà modificata e ora sei nella [!UICONTROL sandbox] dedicata.

![Acquisizione dei dati](./images/sb1.png)

## 1.4.1 Attiva il pubblico nella destinazione Adobe Target

Adobe Target è disponibile come destinazione da Real-Time CDP. Per configurare la tua integrazione con Adobe Target, vai a **Destinazioni**, **Catalogo**.

Fai clic su **Personalization** nel menu **Categorie**. Verrà visualizzata la scheda di destinazione **Adobe Target**. Fai clic su **Attiva pubblico**.

![ALLE](./images/atdest1.png)

Selezionare la destinazione ``Bootcamp Target`` e fare clic su **Avanti**.

![ALLE](./images/atdest3.png)

Nell&#39;elenco dei tipi di pubblico disponibili selezionare il pubblico creato in [1.3 Creare un pubblico](./ex3.md), denominato `yourLastName - Interest in Real-Time CDP`. Quindi fare clic su **Avanti**.

![ALLE](./images/atdest8.png)

Nella pagina successiva, fai clic su **Avanti**.

![ALLE](./images/atdest9.png)

Fai clic su **Fine**.

![ALLE](./images/atdest10.png)

Il pubblico è ora attivato nei confronti di Adobe Target.

![ALLE](./images/atdest11.png)

>[!IMPORTANT]
>
>Quando hai appena creato la destinazione Adobe Target in Real-Time CDP, la pubblicazione della destinazione potrebbe richiedere fino a un’ora. Si tratta di un tempo di attesa una tantum, dovuto alla configurazione del back-end. Al termine della configurazione del tempo di attesa iniziale di 1 ora e del back-end, i nuovi tipi di pubblico edge aggiunti, inviati alla destinazione Adobe Target, saranno disponibili per il targeting in tempo reale.

## 1.4.2 Configurare l’attività basata su moduli di Adobe Target

Ora che il pubblico di Real-Time CDP è configurato per essere inviato ad Adobe Target, puoi configurare la tua attività Targeting esperienza in Adobe Target. In questo esercizio configurerai un’attività basata sul Compositore esperienza visivo.

Vai alla home page di Adobe Experience Cloud da [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Fai clic su **Target** per aprirlo.

![RTCDP](./images/excl.png)

Nella home page di **Adobe Target** verranno visualizzate tutte le attività esistenti.
Fai clic su **+ Crea attività** per creare una nuova attività.

![RTCDP](./images/exclatov.png)

Seleziona **Targeting esperienza**.

![RTCDP](./images/exclatcrxt.png)

Selezionare **Visual** e impostare **URL attività** su `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`. Prima di eseguire questa operazione, sostituire XX con un numero compreso tra 01 e 30.

>[!IMPORTANT]
>
>Ogni partecipante all’abilitazione deve utilizzare una pagina web separata per evitare conflitti tra diverse esperienze Adobe Target. È possibile scegliere una pagina Web e trovare l&#39;URL scegliendo il percorso seguente: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Tutte le pagine condividono lo stesso URL di base e terminano con il numero del partecipante.
>
>Ad esempio, il partecipante 1 deve utilizzare l&#39;URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, il partecipante 30 l&#39;URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

Selezionare l&#39;area di lavoro **AT Bootcamp**.

Fai clic su **Avanti**.

![RTCDP](./images/exclatcrxtdtlform.png)

Ora sei nel Compositore esperienza visivo. Potrebbero essere necessari 20-30 secondi prima che il sito web sia completamente caricato.

![RTCDP](./images/atform1.png)

Il pubblico predefinito è attualmente **Tutti i visitatori**. Fai clic su **3 punti** accanto a **Tutti i visitatori** e fai clic su **Cambia pubblico**.

![RTCDP](./images/atform3.png)

Ora visualizzi l’elenco dei tipi di pubblico disponibili e il pubblico Adobe Experience Platform creato in precedenza e inviato ad Adobe Target ora fa parte di questo elenco. Seleziona il pubblico creato in precedenza in Adobe Experience Platform. Fai clic su **Assegna pubblico**.

![RTCDP](./images/exclatvecchaud.png)

Il pubblico di Adobe Experience Platform ora fa parte di questa attività Targeting esperienza.

![RTCDP](./images/atform4.png)

Prima di poter modificare l&#39;immagine protagonista, è necessario fare clic su **Consenti tutto** sul banner del cookie.

Per eseguire questa operazione, vai a **Sfoglia**

![RTCDP](./images/cook1.png)

Fare clic su **Consenti tutto**.

![RTCDP](./images/cook2.png)

Quindi, torna a **Componi**.

![RTCDP](./images/cook3.png)

Ora cambiamo l&#39;immagine protagonista sulla homepage del sito web. Fare clic sull&#39;immagine protagonista predefinita nel sito Web, fare clic su **Sostituisci contenuto** e quindi selezionare **Immagine**.

![RTCDP](./images/atform5.png)

Cerca il file di immagine **rtcdp.png**. Selezionarlo e fare clic su **Salva**.

![RTCDP](./images/atform6.png)

Potrai quindi visualizzare la nuova esperienza con la nuova immagine, per il pubblico selezionato.

![RTCDP](./images/atform7.png)

Fai clic sul titolo dell’attività nell’angolo in alto a sinistra per rinominarla.

![RTCDP](./images/exclatvecname.png)

Per il nome, utilizzare:

- `yourLastName - RTCDP - XT (VEC)`

Fai clic su **Avanti**.

![RTCDP](./images/atform8.png)

Fai clic su **Avanti**.

![RTCDP](./images/atform8a.png)

Nella pagina **Obiettivi e impostazioni** - vai a **Metriche obiettivo**.

![RTCDP](./images/atform9.png)

Imposta l&#39;obiettivo principale su **Coinvolgimento** - **Tempo sul sito**. Fai clic su **Salva e chiudi**.

![RTCDP](./images/vec3.png)

Sei ora nella pagina **Panoramica attività**. Devi comunque attivare l&#39;attività.

![RTCDP](./images/atform10.png)

Fai clic sul campo **Inattivo** e seleziona **Attiva**.

![RTCDP](./images/atform11.png)

Otterrai quindi una conferma visiva che l’attività è ora live.

![RTCDP](./images/atform12.png)

La tua attività è ora live e può essere testata sul sito web di bootcamp.

Se ora torni al sito Web di dimostrazione e visiti la pagina del prodotto di **Real-Time CDP**, potrai immediatamente qualificarti per il pubblico creato e l&#39;attività Adobe Target verrà visualizzata nella pagina principale in tempo reale.

>[!IMPORTANT]
>
>Ogni partecipante all’abilitazione deve utilizzare una pagina web separata per evitare conflitti tra diverse esperienze Adobe Target. È possibile scegliere una pagina Web e trovare l&#39;URL scegliendo il percorso seguente: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Tutte le pagine condividono lo stesso URL di base e terminano con il numero del partecipante.
>
>Ad esempio, il partecipante 1 deve utilizzare l&#39;URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, il partecipante 30 l&#39;URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Passaggio successivo: [1.5 Azione: inviare il pubblico a Facebook](./ex5.md)

[Torna a Flusso utente 1](./uc1.md)

[Torna a tutti i moduli](../../overview.md)
