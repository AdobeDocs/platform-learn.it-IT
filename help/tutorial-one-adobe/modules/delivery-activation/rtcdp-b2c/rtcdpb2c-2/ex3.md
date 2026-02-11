---
title: Customer AI - Dashboard e segmentazione del punteggio (Predict & Take Action)
description: Customer AI - Dashboard e segmentazione del punteggio (Predict & Take Action)
kt: 5342
doc-type: tutorial
exl-id: a6df3ff1-f907-4185-8189-f0b39c67c943
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 1%

---

# 2.2.3 IA per l’analisi dei clienti - Dashboard di punteggio e segmentazione (Predict &amp; Take Action)

Una volta completata l’esecuzione di un modello, l’istanza di IA per l’analisi dei clienti ti consente di visualizzare il punteggio di propensione valutato per prevedere un cliente che effettua un acquisto nei successivi 30 giorni.

![IA](./images/caiinstancesummary1.png)

>[!NOTE]
>
>Solo un&#39;istanza di IA per l&#39;analisi dei clienti con stato **Operazione riuscita** ti consentirà di visualizzare in anteprima le informazioni del servizio.

## Previsione tendenza

Esaminiamo ora la tendenza prevista generata dal modello di istanza di IA per l’analisi dei clienti. Fai clic sul nome dell’istanza per visualizzare il dashboard.

![IA](./images/caimodels1.png)

La dashboard di IA per l’analisi dei clienti mostra il riepilogo relativo a punteggio, distribuzione della popolazione e fattori influenti per il modello da valutare.

![Descrizione IA](./images/caidescription.png)

Passa il mouse sui fattori influenti per visualizzare l’ulteriore suddivisione della distribuzione dei dati.

![Fattori di influenza](./images/caiinfluencefactors.png)

## Azioni aziendali

### Segmentazione dei clienti

La dashboard di Customer AI consente di definire i segmenti con un solo clic. Fai clic sul pulsante **Crea segmento** nelle schede delle tendenze.

![Crea un segmento](./images/caiinfluencefactors1.png)

Vedrai che viene creata automaticamente una definizione di segmento.

![Regola segmento](./images/caicreatesegment.png)

Assegna un nome al segmento seguendo questa convenzione di denominazione: `--aepUserLdap-- - Customer AI High Propensity`. Fai clic su **Pubblica**.

![Regola segmento](./images/caicreatesegment1.png)

Ora puoi utilizzare questo segmento per il targeting utilizzando ad esempio Real-time CDP, Journey Optimizer e Adobe Target.

## Pulizia

Per assicurarsi che nell&#39;ambiente non vengano conservati dati demo non necessari, assicurarsi di eliminare il set di dati `--aepUserLdap-- - Demo System - Customer Experience Event Dataset` dopo aver completato correttamente questo esercizio. Se non elimini i dati demo, si avrà un impatto sui costi per l’istanza AEP.

![Profilo](./images/cleanup.png)

## Passaggi successivi

Torna a [Intelligent Services](./intelligent-services.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
