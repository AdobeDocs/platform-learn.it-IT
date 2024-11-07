---
title: 'Raccolta dati di Adobe Experience Platform e inoltro lato server in tempo reale: creazione e configurazione di un webhook personalizzato'
description: Creare e configurare un webhook personalizzato
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 1%

---

# 2.5.3 Creare e configurare un webhook personalizzato

## 2.5.3.1 Creare un webhook personalizzato

Vai a [https://webhook.site/](https://webhook.site/). Vedrai qualcosa del genere:

![demo](./images/webhook1.png)

Verrà visualizzato l&#39;URL univoco, che si presenta così: `https://webhook.site/585126a1-41fc-4721-864b-d4aa8c268a1d`.

Questo webhook è stato creato dal sito Web e sarà possibile configurarlo nel **[!DNL Event Forwarding property]** per iniziare a testare l&#39;inoltro degli eventi.

## 2.5.3.2 Aggiornare la proprietà di Inoltro eventi: creare un elemento dati

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/) e vai a **Inoltro eventi**. Cerca nella proprietà Inoltro eventi e fai clic su di essa per aprirla.

![SSF raccolta dati Adobe Experience Platform](./images/prop1.png)

Nel menu a sinistra, vai a **Elementi dati**. Fai clic su **Crea nuovo elemento dati**.

![SSF raccolta dati Adobe Experience Platform](./images/de1.png)

Viene quindi visualizzato un nuovo elemento dati da configurare.

![SSF raccolta dati Adobe Experience Platform](./images/de2.png)

Effettua la seguente selezione:

- Come **Nome**, immetti **Evento XDM**.
- Come **Estensione**, seleziona **Core**.
- Come **Tipo elemento dati**, selezionare **Percorso**.
- Come **Percorso**, immetti **arc.event.xdm**. Immettendo questo percorso, escluderai la sezione **XDM** dal payload dell&#39;evento inviato dal sito Web o dall&#39;app mobile all&#39;interno di Adobe Edge.

Ora avrai questo. Fai clic su **Salva**.

![SSF raccolta dati Adobe Experience Platform](./images/de3.png)

>[!NOTE]
>
>Nel percorso precedente viene fatto riferimento a **arc**. **arc** sta per Contesto risorsa Adobe e **arc** sta sempre per l&#39;oggetto disponibile più alto disponibile nel contesto lato server. È possibile aggiungere arricchimenti e trasformazioni all&#39;oggetto **arc** utilizzando le funzioni del server di raccolta dati di Adobe Experience Platform.
>
>Nel percorso precedente viene fatto riferimento a **event**. **event** rappresenta un evento univoco e Adobe Experience Platform Data Collection Server valuterà sempre ogni evento singolarmente. A volte è possibile che venga visualizzato un riferimento a **eventi** nel payload inviato dal lato client di Web SDK, ma nel server di raccolta dati di Adobe Experience Platform ogni evento viene valutato singolarmente.

## 2.5.3.3 Aggiornare la proprietà del server di raccolta dati di Adobe Experience Platform: creare una regola

Nel menu a sinistra, vai a **Regole**. Fai clic su **Crea nuova regola**.

![SSF raccolta dati Adobe Experience Platform](./images/rl1.png)

Viene quindi visualizzata una nuova regola da configurare. Immetti **Nome**: **Tutte le pagine**. Per questo esercizio non sarà necessario configurare una condizione. Viene invece impostata un&#39;azione. Fai clic sul pulsante **+ Aggiungi** in **Azioni**.

![SSF raccolta dati Adobe Experience Platform](./images/rl2.png)

Poi vedrai questo. Effettua la seguente selezione:

- Seleziona l&#39;**estensione**: **Connettore cloud Adobe**.
- Seleziona il **Tipo azione**: **Effettua chiamata di recupero**.

Questo dovrebbe darti **Nome**: **Connettore Adobe Cloud - Effettua una chiamata di recupero**. Ora dovresti vedere:

![SSF raccolta dati Adobe Experience Platform](./images/rl4.png)

Quindi, configura quanto segue:

- Cambia il metodo di richiesta da GET a **POST**
- Immetti l&#39;URL del webhook personalizzato creato in uno dei passaggi precedenti del sito Web [https://webhook.site/](https://webhook.site/), che si presenta così: `https://webhook.site/585126a1-41fc-4721-864b-d4aa8c268a1d`

Ora dovresti avere questo. Quindi, vai a **Corpo**.

![SSF raccolta dati Adobe Experience Platform](./images/rl6.png)

Poi vedrai questo. Fai clic sull’icona dell’elemento dati come indicato di seguito.

![SSF raccolta dati Adobe Experience Platform](./images/rl7.png)

Nel popup, seleziona l&#39;elemento dati **XDM Event** creato nel passaggio precedente. Fai clic su **Seleziona**.

![SSF raccolta dati Adobe Experience Platform](./images/rl8.png)

Poi vedrai questo. Fai clic su **Mantieni modifiche**.

![SSF raccolta dati Adobe Experience Platform](./images/rl9.png)

Poi vedrai questo. Fai clic su **Salva**.

![SSF raccolta dati Adobe Experience Platform](./images/rl10.png)

Hai configurato la prima regola in una proprietà di Inoltro eventi. Vai a **Flusso di pubblicazione** per pubblicare le modifiche.
Apri la libreria di sviluppo **Principale** facendo clic su **Modifica** come indicato.

![SSF raccolta dati Adobe Experience Platform](./images/rl11.png)

Fai clic sul pulsante **Aggiungi tutte le risorse modificate**, dopo di che la regola e l&#39;elemento dati verranno visualizzati in questa libreria. Fare clic su **Salva e genera per sviluppo**. Le modifiche sono ora in fase di implementazione.

![SSF raccolta dati Adobe Experience Platform](./images/rl13.png)

Dopo un paio di minuti, vedrai che l’implementazione è completata e pronta per essere testata.

![SSF raccolta dati Adobe Experience Platform](./images/rl14.png)

## 2.5.3.4 Testare la configurazione

Vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![DSN](../../gettingstarted/gettingstarted/images/web8.png)

Ora puoi seguire il flusso seguente per accedere al sito web. Fai clic su **Integrazioni**.

![DSN](../../gettingstarted/gettingstarted/images/web1.png)

Nella pagina **Integrazioni** è necessario selezionare la proprietà Raccolta dati creata nell&#39;esercizio 0.1.

![DSN](../../gettingstarted/gettingstarted/images/web2.png)

Poi vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Incolla l’URL del sito web demo, che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l’accesso con il tuo Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Seleziona il tipo di account e completa la procedura di accesso.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Vedrai quindi il tuo sito web caricato in una finestra del browser in incognito. Per ogni dimostrazione, dovrai utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Quando apri la visualizzazione per sviluppatori del browser, puoi esaminare le richieste di rete come indicato di seguito. Quando utilizzi il filtro **interact**, vengono visualizzate le richieste di rete inviate dal client di raccolta dati di Adobe Experience Platform ad Adobe Edge.

![Configurazione raccolta dati di Adobe Experience Platform](./images/hook1.png)

Se selezioni il payload non elaborato, passa a [https://jsonformatter.org/json-pretty-print](https://jsonformatter.org/json-pretty-print) e incolla il payload. Fare clic su **Rendi carino**. Vedrai quindi il payload JSON, l&#39;oggetto **events** e l&#39;oggetto **xdm**. In uno dei passaggi precedenti, quando hai definito l&#39;elemento dati, hai utilizzato il riferimento **arc.event.xdm**, che ti porterà ad analizzare l&#39;oggetto **xdm** di questo payload.

![Configurazione raccolta dati di Adobe Experience Platform](./images/hook2.png)

Passa al sito Web [https://webhook.site/](https://webhook.site/) utilizzato in uno dei passaggi precedenti. Ora dovresti avere una visualizzazione simile a questa, con le richieste di rete visualizzate nel menu a sinistra. Stai visualizzando il payload **xdm** filtrato dalla richiesta di rete mostrata sopra.

![Configurazione raccolta dati di Adobe Experience Platform](./images/hook3.png)

Scorrere verso il basso un po&#39; del payload per trovare il nome della pagina, che in questo caso è **vangeluw-OCUC** (che è il nome del progetto del sito Web demo).

![Configurazione raccolta dati di Adobe Experience Platform](./images/hook4.png)

Se ora esplori il sito web, vedrai ulteriori richieste di rete disponibili in tempo reale su questo webhook personalizzato.

![Configurazione raccolta dati di Adobe Experience Platform](./images/hook5.png)

Ora hai configurato l’inoltro lato server dei payload Web SDK/XDM su un webhook personalizzato esterno. Negli esercizi successivi, configurerai un approccio simile e invierai gli stessi dati agli ambienti Google e AWS.

Passaggio successivo: [2.5.4 Creare e configurare una funzione cloud di Google](./ex4.md)

[Torna al modulo 2.5](./aep-data-collection-ssf.md)

[Torna a tutti i moduli](./../../../overview.md)
