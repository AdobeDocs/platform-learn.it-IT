---
title: 'Intelligent Services - IA per l’analisi dei clienti: crea una nuova istanza (Configura)'
description: 'IA per l’analisi dei clienti: creare una nuova istanza (Configura)'
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---

# 2.2.2 Customer AI - Creare una nuova istanza (Configura)

Customer AI funziona analizzando i dati esistenti di Consumer Experience Event per prevedere i punteggi di propensione di abbandono o conversione. La creazione di una nuova istanza di Customer AI consente agli esperti di marketing di definire obiettivi e misure.

## 2.2.2.1 Configurare una nuova istanza di Customer AI

In Adobe Experience Platform, fai clic su **Servizi** nel menu a sinistra. Verrà visualizzato il browser **Servizi** in cui sono visualizzati tutti i servizi disponibili. Nella scheda di IA per l&#39;analisi dei clienti, fai clic su **Apri**.

![Navigazione dei servizi](./images/navigatetoservice.png)

Fai clic su **Crea istanza**.

![Crea nuova istanza](./images/createnewinstance.png)

Poi vedrai questo.

![Crea nuova istanza](./images/custai1.png)

Immetti i dettagli richiesti per l’istanza di IA per l’analisi dei clienti:

- Nome: utilizzare `--aepUserLdap-- Product Purchase Propensity`
- Descrizione: use: **Prevedere la probabilità che i clienti acquistino un prodotto**
- Tipo di propensione: seleziona **Conversione**

![Imposta pagina 1](./images/setuppage1.png)

Fai clic su **Avanti**.

![Imposta pagina 1](./images/next.png)

Poi vedrai questo. Selezionare il set di dati creato nell&#39;esercizio precedente denominato `--demoProfileLdap - Demo System - Customer Experience Event Dataset`. Fai clic su **Avanti**.

![Imposta pagina 1](./images/custai2.png)

Seleziona **Si verificherà** e definisci il campo **commerce.purchases.value** come variabile di destinazione.

![Definizione obiettivo IA per l&#39;analisi dei clienti](./images/caidefinegoal.png)

Fai clic su **Avanti**.

![Imposta pagina 1](./images/next.png)

Quindi, imposta la pianificazione in modo che venga eseguita **Ogni settimana** e imposta l&#39;ora il più vicino possibile all&#39;ora corrente. Verificare che l&#39;opzione attiva/disattiva **Abilita punteggi per il profilo** sia abilitata.

![Definisci anticipo IA per l&#39;analisi dei clienti](./images/caiadvancepage.png)

Fai clic su **Fine**.

![Imposta pagina 1](./images/finish.png)

Poi vedrai questo popup. Fai clic su **OK**.

![Imposta pagina 1](./images/finish1.png)

Dopo aver configurato l’istanza, puoi visualizzarla nell’elenco delle istanze di Customer AI e anche visualizzare in anteprima il riepilogo dei dettagli di configurazione ed esecuzione facendo clic sulla riga dell’istanza di Customer AI. Nel pannello di riepilogo vengono inoltre visualizzati i dettagli dell’errore nel caso in cui siano stati rilevati errori.

![Riepilogo installazione istanza](./images/caiinstancesummary.png)

>[!NOTE]
>
>Puoi modificare qualsiasi definizione o attributo purché lo stato dell&#39;istanza di Customer AI sia **In attesa di formazione** o **Errore**

Passaggio successivo: [2.2.3 IA per l&#39;analisi dei clienti - Dashboard di punteggio e segmentazione (previsione e azione)](./ex3.md)

[Torna al modulo 2.2](./intelligent-services.md)

[Torna a tutti i moduli](./../../../overview.md)
