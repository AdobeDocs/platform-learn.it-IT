---
title: Adobe Journey Optimizer - Configurare un percorso basato su trigger - Conferma ordine
description: In questa sezione configurerai un percorso basato su trigger - Conferma ordine
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 69bb9eca-3942-4c31-a3d2-0b218143e1eb
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1988'
ht-degree: 9%

---

# 10.1 Configurare un percorso basato su trigger - Conferma ordine

Accedi a Adobe Journey Optimizer accedendo a [Adobe Experience Cloud](https://experience.adobe.com). Fai clic su **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Verrai reindirizzato al **Pagina principale**  in Journey Optimizer. In primo luogo, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare è denominata `--aepSandboxId--`. Per passare da una sandbox all’altra, fai clic su **PROD DI PRODUZIONE (VA7)** e selezionate la sandbox dall’elenco. In questo esempio, la sandbox è denominata **Abilitazione AEP FY22**. Allora sarai nel **Pagina principale** visualizzazione della sandbox `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

## 10.1.1 Creare l’evento

Nel menu , vai a **Configurazioni** e fai clic su **Gestisci** sotto **Eventi**.

![Journey Optimizer](./images/oc30.png)

Sulla **Eventi** viene visualizzata una visualizzazione simile a questa. Fai clic su **Crea evento**.

![Journey Optimizer](./images/oc31.png)

Verrà quindi visualizzata una configurazione di evento vuota.

![Journey Optimizer](./images/oc32.png)

Prima di tutto, dai al tuo Evento un Nome come questo: `--demoProfileLdap--PurchaseEvent`e aggiungi una descrizione come questa: `Purchase Event`.

![Journey Optimizer](./images/oc34.png)

Successivo è il **Tipo evento** selezione. Seleziona **Unitario**.

![Journey Optimizer](./images/eventidtype1.png)

Successivo è il **Tipo ID evento** selezione. Seleziona **Sistema generato**

![Journey Optimizer](./images/eventidtype.png)

Segue la selezione dello schema. È stato preparato uno schema per questo esercizio. Utilizzare lo schema `Demo System - Event Schema for Website (Global v1.1) v.1`.

![Journey Optimizer](./images/oc35.png)

Dopo aver selezionato lo schema, nella sezione **Payload** sezione . Fai clic sul pulsante **Modifica/Matita** per aggiungere altri campi a questo evento.

![Journey Optimizer](./images/oc36.png)

Vedrete questa finestra a comparsa. È ora necessario selezionare caselle di controllo aggiuntive per accedere ai dati aggiuntivi quando questo evento viene attivato.

![Journey Optimizer](./images/oc37.png)

Prima di tutto, seleziona la casella di controllo sulla riga `--aepTenantId--`.

![Journey Optimizer](./images/oc38.png)

Quindi, scorri verso il basso e spunta la casella di controllo sulla riga `productListItems`.

![Journey Optimizer](./images/oc39.png)

Quindi, scorri verso il basso e spunta la casella di controllo sulla riga `commerce`.

![Journey Optimizer](./images/oc391.png)

Quindi, fai clic su **Ok**.

Vedrai che all’evento sono stati aggiunti altri campi. Fai clic su **Salva**.

![Journey Optimizer](./images/oc40.png)

Il nuovo evento viene quindi condiviso e l’evento verrà visualizzato nell’elenco degli eventi disponibili.

Fai di nuovo clic sull&#39;evento per aprire **Modifica evento** schermo di nuovo.
Passa il puntatore del mouse **Payload** per visualizzare di nuovo le 3 icone. Fai clic sul pulsante **Visualizza payload** icona.

![Journey Optimizer](./images/oc41.png)

Viene ora visualizzato un esempio del payload previsto. L&#39;evento dispone di un ID evento di orchestrazione univoco, che è possibile trovare scorrendo in quel payload fino a quando non viene visualizzato `_experience.campaign.orchestration.eventID`.

![Journey Optimizer](./images/oc42.png)

L’ID evento è ciò che deve essere inviato a Adobe Journey Optimizer per attivare il percorso da generare nel passaggio successivo. Annota questo eventID, in quanto ne avrai bisogno in uno dei passaggi successivi.
`"eventID": "ef6dd943c94fe1b4763c098ccd1772344662f2a9f614513106cb5ada8be36857"`

Fai clic su **Ok**, seguita da **Annulla**.

L’evento è ora configurato e pronto per essere utilizzato.

## 10.1.2 Crea il tuo percorso

Nel menu , vai a **Percorsi** e fai clic su **Crea Percorso**.

![Journey Optimizer](./images/oc43.png)

Vedrete questo. Dai un nome al tuo percorso. Seleziona `--demoProfileLdap-- - Order Confirmation journey`. Fai clic su **OK**.

![Journey Optimizer](./images/oc45.png)

Innanzitutto, devi aggiungere l’evento come punto di partenza del percorso. Cerca l&#39;evento `--demoProfileLdap--PurchaseEvent` e trascinarlo nell&#39;area di lavoro. Fai clic su **OK**.

![Journey Optimizer](./images/oc46.png)

Successivamente, sotto **Azioni**, cerca il **E-mail** e aggiungerlo all’area di lavoro.

![Journey Optimizer](./images/oc47.png)

Imposta la **Categoria** a **Marketing** e seleziona una superficie e-mail che ti consente di inviare e-mail. In questo caso, la superficie dell’e-mail da selezionare è **E-mail**. Assicurati che le caselle di controllo per **Clic su e-mail** e **aperture e-mail** sono entrambi abilitati.

![ACOP](./images/journeyactions1.png)

Il passaggio successivo consiste nel creare il messaggio. A tale scopo, fai clic su **Modifica contenuto**.

![ACOP](./images/journeyactions2.png)

Ora vedete questo. Fai clic sul pulsante **Linea oggetto** campo di testo.

![ACOP](./images/journeyactions3.png)

Nell’area di testo inizia la scrittura **Grazie per il tuo ordine,**

![Journey Optimizer](./images/oc5.png)

L&#39;oggetto non è ancora stato completato. Ora devi inserire il token di personalizzazione per il campo **Nome** che è immagazzinato in `profile.person.name.firstName`. Nel menu a sinistra, scorri verso il basso per trovare il **Persona** > **Nome completo** >  **Nome** e fai clic sul **+** per aggiungere il token di personalizzazione alla riga dell’oggetto. Fai clic su **Salva**.

![Journey Optimizer](./images/oc6.png)

Allora tornerai qui. Fai clic su **E-mail Designer** per creare il contenuto dell’e-mail.

![Journey Optimizer](./images/oc7.png)

Nella schermata successiva, fai clic su **Progettazione da zero**.

![Journey Optimizer](./images/oc8.png)

Nel menu a sinistra trovi i componenti struttura che puoi utilizzare per definire la struttura dell’e-mail (righe e colonne).

Trascinare 8 volte a **Colonna 1:1** sulla tela, che dovrebbe darvi questo:

![Journey Optimizer](./images/oc9.png)

Vai a **Componenti contenuto**.

![Journey Optimizer](./images/oc10.png)

Trascina e rilascia una **Immagine** nella prima riga. Fai clic su **Sfoglia**.

![Journey Optimizer](./images/oc11.png)

Vai alla cartella **enablement-assets**, seleziona il file **luma-logo.png** e fai clic su **Seleziona**.

![Journey Optimizer](./images/oc12.png)

È tornato qui adesso. Fai clic sull’immagine per selezionarla e quindi utilizza la **Dimensione** per ridurre leggermente l’immagine del logo.

![Journey Optimizer](./images/oc13.png)

Vai a **Componenti contenuto** e trascinare un **Immagine** nella seconda riga. Seleziona la **Componente immagine** MA NON fare clic su Sfoglia.

![Journey Optimizer](./images/oc15.png)

Incolla l&#39;immagine nel campo **Origine**: `https://parsefiles.back4app.com/hgJBdVOS2eff03JCn6qXXOxT5jJFzialLAHJixD9/29043bedcde632a9cbe8a02a164189c9_preparing.png`. Questa immagine è ospitata all&#39;esterno di Adobe.

![Journey Optimizer](./images/oc14.png)

Quando cambi l’ambito in un altro campo, l’immagine viene riprodotta e vedrai quanto segue:

![Journey Optimizer](./images/oc16.png)

Quindi, vai a **Componenti contenuto** e trascina e rilascia una **Testo** nella terza riga.

![Journey Optimizer](./images/oc17.png)

Selezionare il testo predefinito nel componente **Digitare il testo qui.** e sostituirlo con il testo seguente:

```javascript
You’re one step closer!

Hi 

We've received your order details!

We will also send you a separate email containing your VAT Invoice.

We'll be back in touch with you as soon as we've finished packing your package. Please read carefully the Order Information detailed below.
```

![Journey Optimizer](./images/oc18.png)

Posizionare il cursore accanto al testo **Ciao** e fai clic su **Aggiungi personalizzazione**.

![Journey Optimizer](./images/oc19.png)

Passa a **Persona** > **Nome completo** > **Nome** e fai clic sul **+** per aggiungere il token di personalizzazione alla riga dell’oggetto. Fai clic su **Salva**.

![Journey Optimizer](./images/oc20.png)

Vedrai questo:

![Journey Optimizer](./images/oc21.png)

Quindi, vai a **Componenti contenuto** e trascina e rilascia una **Testo** nella quarta riga.

![Journey Optimizer](./images/oc22.png)

Selezionare il testo predefinito nel componente **Digitare il testo qui.** e sostituirlo con il testo seguente:

`Order Information`

Modifica la dimensione del font in **26 px** e centra il testo in questa cella. A quel punto avrai questo:

![Journey Optimizer](./images/oc23.png)

Quindi, vai a **Componenti contenuto** e trascinare un **HTML** nella quinta riga. Fai clic sul componente HTML , quindi fai clic su **Mostra il codice sorgente**.

![Journey Optimizer](./images/oc24.png)

In **Modifica HTML** popup, incolla questo HTML:

```<table><tbody><tr><td><b>Items purchased</b></td><td></td><td><b>Quantity</b></td><td><b>Subtotal</b></td></tr><tr><td colspan="4" width="500"><hr></td></tr></tbody></table>```

Fai clic su **Salva**.

![Journey Optimizer](./images/oc25.png)

Poi avrai questo. Fai clic su **Salva** per salvare i progressi.

![Journey Optimizer](./images/oc26.png)

Vai a **Componenti contenuto** e trascinare un **HTML** componente sulla sesta riga. Fai clic sul componente HTML , quindi fai clic su **Mostra il codice sorgente**.

![Journey Optimizer](./images/oc57.png)

In **Modifica HTML** popup, incolla questo HTML:

```{{#each xxx as |item|}}<table width="500"><tbody><tr><td><img src="{{item.--aepTenantId--.core.imageURL}}" width="100"></td><td><table><tbody><tr><td><b>{{item.name}}</b><br>{{item.--aepTenantId--.core.subCategory}}<br><b>{{item.priceTotal}}</b><br>&nbsp;<br>Article no: {{item.SKU}}</td></tr></tbody></table></td><td>{{item.quantity}}</td><td><b>{{item.priceTotal}}</b></td></tr></tbody></table>{{/each}}```

A quel punto avrai questo:

![Journey Optimizer](./images/oc58.png)

È ora necessario sostituire **xxx** mediante un riferimento all&#39;oggetto productListItems che fa parte dell&#39;evento che attiva il percorso.

![Journey Optimizer](./images/oc59.png)

Per prima cosa, elimina **xxx** prima nel codice HTML.

![Journey Optimizer](./images/oc60.png)

Nel menu a sinistra, fai clic su **Attributi contestuali**. Questo contesto viene trasmesso al messaggio dal percorso.

![Journey Optimizer](./images/oc601.png)

Vedrete questo. Fai clic sulla freccia accanto a **Journey Orchestration** per approfondire.

![Journey Optimizer](./images/oc61.png)

Fai clic sulla freccia accanto a **Eventi** per approfondire.

![Journey Optimizer](./images/oc62.png)

Fai clic sulla freccia accanto a `--demoProfileLdap--PurchaseEvent` per approfondire.

![Journey Optimizer](./images/oc63.png)

Fai clic sulla freccia accanto a **productListItems** per approfondire.

![Journey Optimizer](./images/oc64.png)

Fai clic sul pulsante **+** accanto a **Nome** per aggiungerlo all’area di lavoro. Poi avrai questo. Ora devi selezionare  **.name** come indicato nella schermata seguente, e quindi devi rimuovere **.name**.

![Journey Optimizer](./images/oc65.png)

Poi avrai questo. Fai clic su **Salva**.

![Journey Optimizer](./images/oc66.png)

Ora tornerai a utilizzare E-mail Designer. Fai clic su **Salva** per salvare i progressi.

![Journey Optimizer](./images/oc67.png)

Quindi, vai a **Componenti contenuto** e trascinare un **HTML** componente sulla settima riga. Fai clic sul componente HTML , quindi fai clic su **Mostra il codice sorgente**.

![Journey Optimizer](./images/oc68.png)

In **Modifica HTML** popup, incolla questo HTML:

```<table><tbody><tr><td><b>Subtotal</b><br>Delivery charge (included)</td><td align="right"><b>xxx</b><br><b>5</b></td></tr><tr><td colspan="2" width="500"><hr></td></tr><tr><td><b>Total including VAT</b></td><td align="right"><b>xxx</b></td></tr></tbody></table>```

Ci sono 2 riferimenti di **xxx** in questo codice HTML. È ora necessario sostituire ciascuna **xxx** mediante un riferimento all&#39;oggetto productListItems che fa parte dell&#39;evento che attiva il percorso.

![Journey Optimizer](./images/oc69.png)

Innanzitutto, elimina il primo **xxx** nel codice HTML.

![Journey Optimizer](./images/oc71.png)

Nel menu a sinistra, fai clic su **Attributi contestuali**.

![Journey Optimizer](./images/oc711.png)

Fai clic sulla freccia accanto a **Journey Orchestration** per approfondire.

![Journey Optimizer](./images/oc72.png)

Fai clic sulla freccia accanto a **Eventi** per approfondire.

![Journey Optimizer](./images/oc722.png)

Fai clic sulla freccia accanto a `--demoProfileLdap--PurchaseEvent` per approfondire.

![Journey Optimizer](./images/oc73.png)

Fai clic sulla freccia accanto a **Commerce** per approfondire.

![Journey Optimizer](./images/oc733.png)

Fai clic sulla freccia accanto a **Ordine** per approfondire.

![Journey Optimizer](./images/oc74.png)

Fai clic sul pulsante **+** accanto a **Totale prezzo** per aggiungerlo all’area di lavoro.

![Journey Optimizer](./images/oc75.png)

Poi avrai questo. Elimina il secondo **xxx** nel codice HTML.

![Journey Optimizer](./images/oc76.png)

Fai clic sul pulsante **+** accanto a **Totale prezzo** per aggiungerlo nuovamente all&#39;area di lavoro.

![Journey Optimizer](./images/oc77.png)

Puoi anche aggiungere il campo **Valuta** dall&#39;interno del **Ordine** sull&#39;area di lavoro, come potete vedere qui.
Al termine, fai clic su **Salva** per salvare le modifiche.

![Journey Optimizer](./images/oc771.png)

A questo punto potrai tornare a E-mail Designer. Fai clic su **Salva** di nuovo.

![Journey Optimizer](./images/oc78.png)

Torna al dashboard dei messaggi facendo clic sul pulsante **freccia** accanto all’oggetto nell’angolo in alto a sinistra.

![Journey Optimizer](./images/oc79.png)

Fai clic sulla freccia nell&#39;angolo in alto a sinistra per tornare al percorso.

![Journey Optimizer](./images/oc79a.png)

Fai clic su **Ok** per chiudere l’azione e-mail.

![Journey Optimizer](./images/oc79b.png)

Fai clic su **Pubblica** per pubblicare il percorso.

![Journey Optimizer](./images/oc511.png)

Fai clic su **Pubblica** di nuovo.

![Journey Optimizer](./images/oc512.png)

Il percorso è ora pubblicato.

![Journey Optimizer](./images/oc513.png)

## 10.1.5 Aggiornare la proprietà client di raccolta dati di Adobe Experience Platform

Vai a [Raccolta dati Adobe Experience Platform](https://experience.adobe.com/launch/) e seleziona **Tag**.

Questa è la pagina Proprietà raccolta dati di Adobe Experience Platform che hai visto prima.

![Pagina Proprietà](../module1/images/launch1.png)

Nel modulo 0, Demo System ha creato due proprietà Client: uno per il sito web e uno per l’app mobile. Trovarli cercando `--demoProfileLdap--` in **[!UICONTROL Ricerca]** scatola. Fai clic per aprire **Web** proprietà.

![Casella di ricerca](../module1/images/property6.png)

Vai a **Elementi dati**. Cerca e apri l’elemento dati **XDM - Acquisto**.

![Journey Optimizer](./images/oc91.png)

Vedrete questo. Passa al campo . **_experience.campaign.orchestration.eventID** e compila il tuo eventID qui. L&#39;ID evento da compilare qui è l&#39;ID evento creato come parte dell&#39;esercizio 10.1.2. Fai clic su **Salva** o **Salva nella libreria**.

![Journey Optimizer](./images/oc92.png)

Salva le modifiche nella proprietà Client e pubblica le modifiche aggiornando la libreria di sviluppo.

![Journey Optimizer](./images/oc93.png)

Le modifiche sono ora implementate e possono essere testate.

## 10.1.6 Verifica l&#39;e-mail di conferma dell&#39;ordine utilizzando il sito web demo

Mettiamo alla prova il percorso aggiornato acquistando un prodotto sul sito web demo.

Vai a [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, vedrai questo. Fai clic sul progetto del tuo sito web per aprirlo.

![DSN](../module0/images/web8.png)

Sulla **Schermi** pagina, fai clic su **Esegui**.

![DSN](../module1/images/web2.png)

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

Fai clic sull’icona del logo Adobe nell’angolo in alto a sinistra dello schermo per aprire il Visualizzatore profili.

![Demo](../module2/images/pv1.png)

Guarda il pannello Visualizzatore profili e il Profilo cliente in tempo reale con **ID Experience Cloud** come identificatore principale per questo cliente attualmente sconosciuto.

![Demo](../module2/images/pv2.png)

Vai alla pagina Registrazione/Accesso . Fai clic su **CREARE UN ACCOUNT**.

![Demo](../module2/images/pv9.png)

Inserisci i tuoi dati e fai clic su **Registro** dopo di che verrai reindirizzato alla pagina precedente.

![Demo](../module2/images/pv10.png)

Aggiungi qualsiasi prodotto al tuo carrello e vai al **Carrello** pagina. Fai clic su **Procedi al pagamento**.

![Journey Optimizer](./images/cart1.png)

Quindi, verifica i campi nella pagina di pagamento e fai clic su **Pagamento**.

![Journey Optimizer](./images/cart2.png)

Riceverai quindi l&#39;e-mail di conferma dell&#39;ordine entro pochi secondi.

![Journey Optimizer](./images/oc98.png)

Ha finito questo esercizio.

Passaggio successivo: [10.2 Configurare un percorso di newsletter basato su batch](./ex2.md)

[Torna al modulo 10](./journeyoptimizer.md)

[Torna a tutti i moduli](../../overview.md)
