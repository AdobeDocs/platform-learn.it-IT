---
title: Servizi intelligenti - Customer AI Creare una nuova istanza (configurare)
description: Customer AI - Creare una nuova istanza (Configura)
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: d9377c97-efed-427a-a063-aa9c6bd1a78a
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 3%

---

# 5.2 Customer AI - Creare una nuova istanza (Configura)

Customer AI funziona analizzando i dati esistenti dell’evento esperienza del consumatore per prevedere i punteggi di propensione di abbandono o conversione. La creazione di una nuova istanza di Customer AI consente agli addetti al marketing di definire obiettivi e misure.

## 5.2.1 Configurare una nuova istanza di Customer AI

In Adobe Experience Platform, fai clic su **Servizi** nel menu a sinistra. La **Servizi** viene visualizzato il browser e visualizza tutti i servizi disponibili a tua disposizione. Nella scheda di Customer AI, fai clic su **Apri**.

![Navigazione nel servizio](./images/navigatetoservice.png)

Fai clic su **Crea istanza**.

![Crea nuova istanza](./images/createnewinstance.png)

Vedrete questo.

![Crea nuova istanza](./images/custai1.png)

Immetti i dettagli richiesti per l’istanza Customer AI:

- Nome: use `--demoProfileLdap-- Product Purchase Propensity`
- Descrizione: utilizzare: **Prevedere la probabilità che i clienti acquistino un prodotto**
- Tipo di tendenza: select **Conversione**

![Pagina di configurazione 1](./images/setuppage1.png)

Fai clic su **Avanti**.

![Pagina di configurazione 1](./images/next.png)

Vedrete questo. Seleziona il set di dati creato nell’esercizio precedente, denominato `--demoProfileLdap - Demo System - Customer Experience Event Dataset`. Fai clic su **Avanti**.

![Pagina di configurazione 1](./images/custai2.png)

Seleziona **Si verificherà** e definire il campo **commerce.purchased.value** come variabile target.

![Definizione dell’obiettivo ICC](./images/caidefinegoal.png)

Fai clic su **Avanti**.

![Pagina di configurazione 1](./images/next.png)

Imposta la pianificazione da eseguire **Settimanale** e impostare l&#39;ora il più vicino possibile all&#39;ora corrente. Assicurati che l&#39;interruttore **Abilitare i punteggi per profilo** è abilitato.

![Definire l’avanzamento CAI](./images/caiadvancepage.png)

Fai clic su **Fine**.

![Pagina di configurazione 1](./images/finish.png)

Vedrete questa finestra a comparsa. Fai clic su **OK**.

![Pagina di configurazione 1](./images/finish1.png)

Dopo aver configurato l’istanza, puoi visualizzarla nell’elenco delle istanze di Customer AI e visualizzare in anteprima il riepilogo dei dettagli di configurazione ed esecuzione facendo clic sulla riga dell’istanza di Customer AI. Il pannello di riepilogo visualizza anche i dettagli dell’errore in caso di errori riscontrati.

![Riepilogo configurazione istanza](./images/caiinstancesummary.png)

>[!NOTE]
>
>Puoi modificare qualsiasi definizione o attributo purché lo stato dell’istanza di Customer AI sia **In attesa di formazione** o **Errore**

Passaggio successivo: [5.3 Customer AI - Dashboard di valutazione e segmentazione (Predict &amp; Take Action)](./ex3.md)

[Torna al modulo 5](./intelligent-services.md)

[Torna a tutti i moduli](./../../overview.md)
