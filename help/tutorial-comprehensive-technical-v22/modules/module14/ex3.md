---
title: Raccolta dati di Adobe Experience Platform e inoltro lato server in tempo reale - Creare e configurare un webhook personalizzato
description: Creare e configurare un webhook personalizzato
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: db15c445-b45a-44cb-bc24-598676f02a5d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1101'
ht-degree: 1%

---

# 14.3 Creare e configurare un webhook personalizzato

## 14.3.1 Crea il tuo webhook personalizzato

Vai a [https://webhook.site/](https://webhook.site/). Vedrete qualcosa del genere:

![demo](./images/webhook1.png)

Vedrai il tuo URL univoco, simile al seguente: `https://webhook.site/585126a1-41fc-4721-864b-d4aa8c268a1d`.

Questo sito web ora ha creato questo webhook per te e sarai in grado di configurare questo webhook nel tuo **[!DNL Event Forwarding property]** per iniziare a testare l’inoltro degli eventi.

## 14.3.2 Aggiorna la proprietà Event Forwarding : Creare un elemento dati

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) e vai a **Inoltro eventi**. Cerca la proprietà Event Forwarding e fai clic su di essa per aprirla.

![SSF raccolta dati Adobe Experience Platform](./images/prop1.png)

Nel menu a sinistra, vai a **Elementi dati**. Fai clic su **Crea nuovo elemento dati**.

![SSF raccolta dati Adobe Experience Platform](./images/de1.png)

Verrà quindi visualizzato un nuovo elemento dati da configurare.

![SSF raccolta dati Adobe Experience Platform](./images/de2.png)

Effettua la selezione seguente:

- Come **Nome**, inserisci **Evento XDM**.
- Come **Estensione**, seleziona **Core**.
- Come **Tipo di elemento dati**, seleziona **Percorso**.
- Come **Percorso**, inserisci **arc.event.xdm**. Inserendo questo percorso, filtrerai il **XDM** dal payload dell’evento inviato dal sito web o dall’app mobile in Adobe Edge.

Ora avrà questo. Fai clic su **Salva**.

![SSF raccolta dati Adobe Experience Platform](./images/de3.png)

>[!NOTE]
>
>Nel percorso precedente viene fatto riferimento a **arc**. **arc** sta per contesto risorsa Adobe e **arc** sta sempre per l&#39;oggetto disponibile più alto disponibile nel contesto lato server. Arricchimenti e trasformazioni possono essere aggiunti a quello **arc** mediante le funzioni di Adobe Experience Platform Data Collection Server.
>
>Nel percorso precedente viene fatto riferimento a **event**. **event** sta per un evento univoco e Adobe Experience Platform Data Collection Server valuterà sempre ogni singolo evento. A volte è possibile visualizzare un riferimento a **events** nel payload inviato dal lato client dell’SDK per web, ma in Adobe Experience Platform Data Collection Server, ogni evento viene valutato singolarmente.

## 14.3.3 Aggiorna la proprietà Adobe Experience Platform Data Collection Server : Creare una regola

Nel menu a sinistra, vai a **Regole**. Fai clic su **Crea nuova regola**.

![SSF raccolta dati Adobe Experience Platform](./images/rl1.png)

Verrà quindi visualizzata una nuova regola da configurare. Inserisci il **Nome**: **Tutte le pagine**. Per questo esercizio, non sarà necessario configurare una condizione. Imposta invece un&#39;azione. Fai clic sul pulsante **+ Aggiungi** pulsante sotto **Azioni**.

![SSF raccolta dati Adobe Experience Platform](./images/rl2.png)

Vedrete questo. Effettua la selezione seguente:

- Seleziona la **Estensione**: **Connettore cloud di Adobe**.
- Seleziona la **Tipo di azione**: **Fai una chiamata di recupero**.

Questo dovrebbe darvi questo **Nome**: **Connettore cloud di Adobe - Effettua una chiamata di recupero**. Ora dovresti vedere quanto segue:

![SSF raccolta dati Adobe Experience Platform](./images/rl4.png)

Quindi, configura quanto segue:

- Modifica il metodo di richiesta da GET a **POST**
- Inserisci l’URL del webhook personalizzato creato in uno dei passaggi precedenti nel [https://webhook.site/](https://webhook.site/) sito web, simile a questo: `https://webhook.site/585126a1-41fc-4721-864b-d4aa8c268a1d`

Dovrebbe avere questo ora. Quindi, vai a **Corpo**.

![SSF raccolta dati Adobe Experience Platform](./images/rl6.png)

Vedrete questo. Fai clic sull’icona dell’elemento dati come indicato di seguito.

![SSF raccolta dati Adobe Experience Platform](./images/rl7.png)

Nella finestra a comparsa, seleziona l’elemento dati **Evento XDM** creato nel passaggio precedente. Fai clic su **Seleziona**.

![SSF raccolta dati Adobe Experience Platform](./images/rl8.png)

Vedrete questo. Fai clic su **Mantieni modifiche**.

![SSF raccolta dati Adobe Experience Platform](./images/rl9.png)

Vedrete questo. Fai clic su **Salva**.

![SSF raccolta dati Adobe Experience Platform](./images/rl10.png)

Ora hai configurato la tua prima regola in una proprietà Inoltro eventi. Vai a **Flusso di pubblicazione** per pubblicare le modifiche.
Apri la libreria di sviluppo . **Principale** facendo clic su **Modifica** come indicato.

![SSF raccolta dati Adobe Experience Platform](./images/rl11.png)

Fai clic sul pulsante **Aggiungi tutte le risorse modificate** , dopodiché vedrai la regola e l&#39;elemento dati visualizzati in questa libreria. Quindi, fai clic su **Salva e genera per sviluppo**. Le modifiche vengono ora distribuite.

![SSF raccolta dati Adobe Experience Platform](./images/rl13.png)

Dopo un paio di minuti, vedrai che la distribuzione è completata e pronta per essere testata.

![SSF raccolta dati Adobe Experience Platform](./images/rl14.png)

## 14.3.4 Verifica la configurazione

Vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, vedrai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![DSN](../module0/images/web8.png)

Ora puoi seguire il flusso seguente per accedere al sito web. Fai clic su **Integrazioni**.

![DSN](../module0/images/web1.png)

Sulla **Integrazioni** pagina , devi selezionare la proprietà Raccolta dati creata nell&#39;esercizio 0.1.

![DSN](../module0/images/web2.png)

Vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](../module0/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](../module0/images/web4.png)

Incolla l’URL del sito web dimostrativo che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l&#39;accesso utilizzando il tuo Adobe ID.

![DSN](../module0/images/web5.png)

Seleziona il tipo di account e completa il processo di accesso.

![DSN](../module0/images/web6.png)

Il sito web verrà quindi caricato in una finestra del browser in incognito. Per ogni dimostrazione, è necessario utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](../module0/images/web7.png)

Quando apri il browser Developer View, puoi controllare le richieste di rete come indicato di seguito. Quando utilizzi il filtro **interagire**, vedrai le richieste di rete inviate dal client di raccolta dati di Adobe Experience Platform ad Adobe Edge.

![Configurazione della raccolta dati di Adobe Experience Platform](./images/hook1.png)

Se selezioni il payload non elaborato, vai a [https://jsonformatter.org/json-pretty-print](https://jsonformatter.org/json-pretty-print) e incolla il payload. Fai clic su **Rendi carino**. Vedrai quindi il payload JSON, il **events** e **xdm** oggetto. In uno dei passaggi precedenti, quando hai definito l’elemento dati, hai utilizzato il riferimento **arc.event.xdm**, che consente di analizzare il **xdm** oggetto del payload.

![Configurazione della raccolta dati di Adobe Experience Platform](./images/hook2.png)

Passa alla visualizzazione del sito web [https://webhook.site/](https://webhook.site/) utilizzato in uno dei passaggi precedenti. Ora dovresti avere una visualizzazione simile a questa, con le richieste di rete visualizzate nel menu a sinistra. Stai vedendo il **xdm** payload filtrato dalla richiesta di rete mostrata sopra.

![Configurazione della raccolta dati di Adobe Experience Platform](./images/hook3.png)

Scorri verso il basso nel payload per trovare il nome della pagina, che in questo caso è **vangeluw-OCUC** (nome del progetto del sito web demo).

![Configurazione della raccolta dati di Adobe Experience Platform](./images/hook4.png)

Se ora navigi attraverso il sito web, vedrai ulteriori richieste di rete che diventano disponibili su questo webhook personalizzato in tempo reale.

![Configurazione della raccolta dati di Adobe Experience Platform](./images/hook5.png)

Ora hai configurato l’inoltro lato server dei payload SDK/XDM per web su un webhook personalizzato esterno. Negli esercizi successivi, configurerai un approccio simile e invierai gli stessi dati agli ambienti Google e AWS.

Passaggio successivo: [14.4 Creare e configurare una funzione Google Cloud](./ex4.md)

[Torna al modulo 14](./aep-data-collection-ssf.md)

[Torna a tutti i moduli](./../../overview.md)
