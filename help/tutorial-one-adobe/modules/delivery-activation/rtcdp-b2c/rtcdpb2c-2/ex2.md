---
title: 'Intelligent Services - IA per l’analisi dei clienti: crea una nuova istanza (Configura)'
description: 'IA per l’analisi dei clienti: creare una nuova istanza (Configura)'
kt: 5342
doc-type: tutorial
exl-id: faf84607-39fc-4e02-b38b-8fb0c64699e7
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 1%

---

# 2.2.2 Customer AI - Creare una nuova istanza (Configura)

Customer AI funziona analizzando i dati esistenti di Consumer Experience Event per prevedere i punteggi di propensione di abbandono o conversione. La creazione di una nuova istanza di Customer AI consente agli esperti di marketing di definire obiettivi e misure.

## Configurare una nuova istanza di Customer AI

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

Fai clic su **Salva e continua**.

![Imposta pagina 1](./images/setuppage1.png)

Poi vedrai questo. Selezionare il set di dati creato nell&#39;esercizio precedente denominato `--aepUserLdap-- - Demo System - Customer Experience Event Dataset`. Fai clic su **Aggiungi**.

![Imposta pagina 1](./images/custai2.png)

Poi vedrai questo. devi definire il campo **Identità**. Fare clic su **Nessuno**.

![Imposta pagina 1](./images/custai2a.png)

Nel popup, selezionare **Identity Map (identityMap)**, quindi selezionare lo spazio dei nomi **Demo System - CRMID (crmId)**. Fare clic su **Salva**.

![Imposta pagina 1](./images/custai2b.png)

Fai clic su **Salva e continua**.

![Imposta pagina 1](./images/custai2c.png)

Seleziona **Si verificherà** nel set di dati specifico e definisci il campo **commerce.purchases.value** come variabile di destinazione.

![Definizione obiettivo IA per l&#39;analisi dei clienti](./images/caidefinegoal.png)

Quindi, imposta la pianificazione in modo che venga eseguita **Ogni settimana** e imposta l&#39;ora il più vicino possibile all&#39;ora corrente. Verificare che l&#39;opzione attiva/disattiva **Abilita punteggi per il profilo** sia abilitata. Fai clic su **Salva e continua**.

![Definisci anticipo IA per l&#39;analisi dei clienti](./images/caiadvancepage.png)

Dopo aver configurato l’istanza, è possibile visualizzarla nell’elenco del servizio Customer AI e inoltre visualizzare in anteprima il riepilogo dei dettagli di configurazione ed esecuzione facendo clic sulla riga dell’istanza Customer AI. Nel pannello di riepilogo vengono inoltre visualizzati i dettagli dell’errore nel caso in cui siano stati rilevati errori.

![Riepilogo installazione istanza](./images/caiinstancesummary.png)

>[!NOTE]
>
>Puoi modificare qualsiasi definizione o attributo purché lo stato dell&#39;istanza di Customer AI sia **In attesa di formazione** o **Errore**

Una volta eseguito il modello, questo verrà visualizzato.

![Riepilogo installazione istanza](./images/caiinstancesummary1.png)

## Passaggi successivi

Vai a [2.2.3 Customer AI - Dashboard punteggio e segmentazione (Previsione e azione)](./ex3.md){target="_blank"}

Torna a [Intelligent Services](./intelligent-services.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
