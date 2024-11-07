---
title: Real-time CDP - Creare un segmento e intervenire - Inviare il segmento ad Adobe Target
description: Real-time CDP - Creare un segmento e intervenire - Inviare il segmento ad Adobe Target
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 2%

---

# 2.3.5 Intervenire: inviare il segmento ad Adobe Target

Vai a [Adobe Experience Platform](https://experience.adobe.com/platform). Dopo aver effettuato l’accesso, accedi alla home page di Adobe Experience Platform.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/home.png)

Prima di continuare, devi selezionare una **sandbox**. La sandbox da selezionare è denominata ``--aepSandboxName--``. A tale scopo, fai clic sul testo **[!UICONTROL Prod produzione]** nella riga blu nella parte superiore dello schermo. Dopo aver selezionato la [!UICONTROL sandbox] appropriata, la schermata verrà modificata e ora sei nella [!UICONTROL sandbox] dedicata.

![Acquisizione dei dati](./../../../modules/datacollection/module1.2/images/sb1.png)

## 2.3.5.1 Verificare lo stream di dati

La destinazione Adobe Target in Real-Time CDP è connessa allo stream di dati utilizzato per acquisire i dati nella rete Edge di Adobe. Se desideri impostare la destinazione di Adobe Target, devi innanzitutto verificare se lo stream di dati è già abilitato per Adobe Target. Il flusso di dati è stato configurato in [Esercizio 0.2 Creare il flusso di dati](./../../../modules/gettingstarted/gettingstarted/ex2.md) ed è stato denominato `--aepUserLdap-- - Demo System Datastream`.

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/), quindi fai clic su **Datastreams** o **Datastreams (Beta)**.

![Acquisizione dei dati](./images/atdestds1.png)

Nell&#39;angolo in alto a destra dello schermo, seleziona il nome della sandbox, che dovrebbe essere `--aepSandboxName--`.

![Fai clic sull&#39;icona Configurazione di Edge nell&#39;area di navigazione a sinistra](./images/edgeconfig1b.png)

In Datastreams, cercare lo stream di dati denominato `--aepUserLdap-- - Demo System Datastream`. Fai clic sullo stream di dati per aprirlo.

![Acquisizione dei dati](./images/atdestds3.png)

Visualizzerai quindi questo elemento, fai clic su **...** accanto a **Adobe Experience Platform** e quindi su **Modifica**.

![Acquisizione dei dati](./images/atdestds4.png)

Seleziona le caselle di controllo per **Segmentazione Edge** e **Destinazioni Personalization**. Fai clic su **Salva**.

![Acquisizione dei dati](./images/atdestds4a.png)

Fare clic su **+ Aggiungi servizio**.

![Acquisizione dei dati](./images/atdestds4b.png)

Selezionare il servizio **Adobe Target**. Fai clic su **Salva**.

![Acquisizione dei dati](./images/atdestds5.png)

Lo stream di dati è ora configurato per Adobe Target.

![Acquisizione dei dati](./images/atdestds5a.png)

## 2.3.5.2 Configurare la destinazione Adobe Target

Adobe Target è disponibile come destinazione da Real-Time CDP. Per configurare la tua integrazione con Adobe Target, vai a **Destinazioni**, **Catalogo**.

![ALLE](./images/atdest1.png)

Fai clic su **Personalization** nel menu **Categorie**. Verrà visualizzata la scheda di destinazione **Adobe Target**. Fai clic su **Attiva segmenti** (o **Configura** a seconda dell&#39;ambiente).

![ALLE](./images/atdest2.png)

A seconda dell&#39;ambiente, potrebbe essere necessario fare clic su **+ Configurare una nuova destinazione** per iniziare a creare la destinazione.

![ALLE](./images/atdest3.png)

Poi vedrai questo.

![ALLE](./images/atdest4.png)

Nella schermata **Configura nuova destinazione**, è necessario configurare due elementi:

- Nome: utilizzare il nome `--aepUserLdap-- - Adobe Target (Web)`, che deve essere simile al seguente: **vangeluw - Adobe Target (Web)**.
- ID dello stream di dati: è necessario selezionare lo stream di dati configurato in [Esercizio 0.2 Creare lo stream di dati](./../../../modules/gettingstarted/gettingstarted/ex2.md). Il nome dello stream di dati deve essere: `--aepUserLdap-- - Demo System Datastream`.

Fai clic su **Avanti**.

![ALLE](./images/atdest5.png)

Nella schermata successiva è possibile selezionare facoltativamente un criterio di governance. Non è necessario selezionarne uno, in questo caso non è necessario selezionarne uno, quindi fai clic su **Crea**.

![ALLE](./images/atdest6.png)

La destinazione viene ora creata e verrà visualizzata nell’elenco. Seleziona la destinazione e fai clic su **Avanti** per iniziare a inviare segmenti alla destinazione.

![ALLE](./images/atdest7.png)

Nell&#39;elenco dei segmenti disponibili selezionare il segmento creato in [Esercizio 6.1 Creare un segmento](./ex1.md), denominato `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. Quindi fare clic su **Avanti**.

![ALLE](./images/atdest8.png)

Nella pagina successiva, fai clic su **Avanti**.

![ALLE](./images/atdest9.png)

Fai clic su **Fine**.

![ALLE](./images/atdest10.png)

Il segmento è ora attivato verso Adobe Target.

![ALLE](./images/atdest11.png)

>[!IMPORTANT]
>
>Quando hai appena creato la destinazione Adobe Target in Real-Time CDP, la pubblicazione della destinazione potrebbe richiedere fino a un’ora. Si tratta di un tempo di attesa una tantum, dovuto alla configurazione del back-end. Al termine della configurazione del tempo di attesa iniziale di 1 ora e del back-end, i nuovi segmenti edge aggiunti inviati alla destinazione Adobe Target saranno disponibili per il targeting in tempo reale.

## 2.3.5.3 Configurare l’attività basata su moduli di Adobe Target

Ora che il segmento di Real-Time CDP è configurato per essere inviato ad Adobe Target, puoi configurare l’attività Targeting esperienze in Adobe Target. In questo esercizio configurerai un’attività basata su moduli.

Vai alla home page di Adobe Experience Cloud da [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Fai clic su **Target** per aprirlo.

![RTCDP](./images/excl.png)

Nella home page di **Adobe Target** verranno visualizzate tutte le attività esistenti.

![RTCDP](./images/exclatov.png)

Fai clic su **+ Crea attività** per creare una nuova attività.

![RTCDP](./images/exclatcr.png)

Seleziona **Targeting esperienza**.

![RTCDP](./images/exclatcrxt.png)

Selezionare **Modulo** e **Nessuna restrizione proprietà**. Fai clic su **Avanti**.

![RTCDP](./images/exclatcrxtdtlform.png)

Ora sei nel compositore attività basato su moduli.

![RTCDP](./images/atform1.png)

Per il campo **POSIZIONE 1**, selezionare **target-global-mbox**.

![RTCDP](./images/atform2.png)

Il pubblico predefinito è attualmente **Tutti i visitatori**. Fai clic su **3 punti** accanto a **Tutti i visitatori** e fai clic su **Cambia pubblico**.

![RTCDP](./images/atform3.png)

Ora visualizzi l’elenco dei tipi di pubblico disponibili e il segmento Adobe Experience Platform creato in precedenza e inviato ad Adobe Target ora fa parte di questo elenco. Seleziona il segmento creato in precedenza in Adobe Experience Platform. Fai clic su **Assegna pubblico**.

![RTCDP](./images/exclatvecchaud.png)

Il segmento Adobe Experience Platform ora fa parte di questa attività Targeting esperienza.

![RTCDP](./images/atform4.png)

Ora cambiamo l&#39;immagine protagonista sulla homepage del sito web. Fai clic su per aprire l&#39;elenco a discesa accanto a **Contenuto predefinito** e fai clic su **Crea offerta HTML**.

![RTCDP](./images/atform5.png)

Incolla il seguente codice. Quindi fare clic su **Avanti**.

```javascript
<script>document.querySelector("#home > div > div > div > div > div.banner_img.d-none.d-lg-block > img").src="https://parsefiles.back4app.com/hgJBdVOS2eff03JCn6qXXOxT5jJFzialLAHJixD9/ff92fdc3885972c0090ad5419e0ef4d4_Luma - Product - Proteus - Hero Banner.png"; document.querySelector(".banner_text > *").remove()</script>
```

![RTCDP](./images/atform6.png)

Potrai quindi visualizzare la nuova esperienza con la nuova immagine, per il pubblico selezionato.

![RTCDP](./images/atform7.png)

Fai clic sul titolo dell&#39;attività nell&#39;angolo superiore sinistro per rinominarla.

![RTCDP](./images/exclatvecname.png)

Per il nome, utilizzare:

- `--aepUserLdap-- - RTCDP - XT (Form)`

![RTCDP](./images/atform8.png)

Fai clic su **Avanti**.

![RTCDP](./images/exclatvecnamenext.png)

Nella pagina **Obiettivi e impostazioni** - vai a **Metriche obiettivo**.

![RTCDP](./images/atform9.png)

Imposta l&#39;obiettivo principale su **Coinvolgimento** - **Tempo sul sito**.

![RTCDP](./images/vec3.png)

Fai clic su **Salva e chiudi**.

![RTCDP](./images/vecsave.png)

Sei ora nella pagina **Panoramica attività**. Devi comunque attivare l&#39;attività.

![RTCDP](./images/atform10.png)

Fai clic sul campo **Inattivo** e seleziona **Attiva**.

![RTCDP](./images/atform11.png)

Otterrai quindi una conferma visiva che l’attività è ora live.

![RTCDP](./images/atform12.png)

L&#39;attività è ora live e può essere testata sul sito web demo.

>[!IMPORTANT]
>
>Quando hai appena creato la destinazione Adobe Target in Real-Time CDP, la pubblicazione della destinazione potrebbe richiedere fino a un’ora. Si tratta di un tempo di attesa una tantum, dovuto alla configurazione del back-end. Al termine della configurazione del tempo di attesa iniziale di 1 ora e del back-end, i nuovi segmenti edge aggiunti inviati alla destinazione Adobe Target saranno disponibili per il targeting in tempo reale.

Se ora torni al tuo sito web demo e visiti la pagina del prodotto di PROTEUS FITNESS JACKSHIRT, ti qualificherai immediatamente per il segmento creato, e vedrai l’attività Adobe Target visualizzata nella pagina principale in tempo reale.

![RTCDP](./images/atform13.png)

Passaggio Successivo: [2.3.6 Tipi Di Pubblico Esterni](./ex6.md)

[Torna al modulo 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Torna a tutti i moduli](../../../overview.md)
