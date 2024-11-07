---
title: Customer AI - Dashboard e segmentazione del punteggio (Predict & Take Action)
description: Customer AI - Dashboard e segmentazione del punteggio (Predict & Take Action)
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---

# 2.2.3 IA per l’analisi dei clienti - Dashboard di punteggio e segmentazione (Predict &amp; Take Action)

Una volta completata l’esecuzione di un modello, l’istanza di IA per l’analisi dei clienti ti consente di visualizzare il punteggio di propensione valutato per prevedere un cliente che effettua un acquisto nei successivi 30 giorni.

![IA](./images/caimodels.png)

>[!NOTE]
>
>Solo un&#39;istanza di IA per l&#39;analisi dei clienti con stato **Operazione riuscita** ti consentirà di visualizzare in anteprima le informazioni del servizio.

## 2.2.3.1 Previsione della tendenza

Esaminiamo ora la tendenza prevista generata dal modello di istanza di IA per l’analisi dei clienti. Fai clic sul nome dell’istanza per visualizzare il dashboard.

![IA](./images/caimodels1.png)

La dashboard di IA per l’analisi dei clienti mostra il riepilogo relativo a punteggio, distribuzione della popolazione e fattori influenti per il modello da valutare.

![Descrizione IA](./images/caidescription.png)

![Riepilogo dashboard](./images/caidashboard.png)

Passa il mouse sui fattori influenti per visualizzare l’ulteriore suddivisione della distribuzione dei dati.

![Fattori di influenza](./images/caiinfluencefactors.png)

## 2.2.3.2 Azioni intraprese dalle imprese

### 2.2.3.2.1 Segmentazione dei clienti

La dashboard di Customer AI consente di definire i segmenti con un solo clic. Fai clic sul pulsante **Crea segmento** nelle schede delle tendenze.

![Crea un segmento](./images/caiinfluencefactors1.png)

Vedrai che viene creata automaticamente una definizione di segmento.

![Regola segmento](./images/caicreatesegment.png)

Assegna un nome al segmento seguendo questa convenzione di denominazione: `--demoProfileLdap-- - Customer AI High Propensity`. Fai clic su **Salva**.

![Regola segmento](./images/caicreatesegment1.png)

Ora puoi utilizzare questo segmento per il targeting utilizzando ad esempio Real-time CDP, Journey Orchestration e Adobe Target.

### 2.2.3.2.2 Panoramica del profilo

Poiché il punteggio tendenza di Customer AI diventa parte del profilo cliente in tempo reale, puoi visualizzare il punteggio del singolo cliente.

In Adobe Experience Platform, vai a **Profili** nel menu a sinistra e seleziona **Sfoglia**.

Cerca un profilo utilizzando uno degli identificatori, ad esempio **EMAIL hbirkenshawa@businessweek.com**, disponibili nel file JSON che hai acquisito. Fare clic su **ID profilo** per aprire il profilo.

![Profilo](./images/profile1.png)

A questo punto viene visualizzato quanto segue:

![Profilo](./images/profile2.png)

Vai a **Attributi**, che contiene l&#39;output del modello di IA per l&#39;analisi dei clienti.

![Profilo](./images/profile3.png)

Scorri verso il basso per visualizzare il Punteggio tendenza calcolato dal modello di IA per l’analisi dei clienti.

![Profilo](./images/profile4.png)

Passaggio successivo: [Riepilogo e vantaggi](./summary.md)

[Torna al modulo 2.2](./intelligent-services.md)

[Torna a tutti i moduli](./../../../overview.md)
