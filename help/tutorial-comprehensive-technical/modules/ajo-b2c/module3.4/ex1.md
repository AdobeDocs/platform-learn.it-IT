---
title: Adobe Journey Optimizer - Configurare un percorso basato su trigger - Conferma dell’ordine
description: In questa sezione viene configurato un percorso basato su trigger - Conferma ordine
kt: 5342
doc-type: tutorial
exl-id: b9d9b357-08d1-4f65-9e0b-46224d035602
source-git-commit: c531412a2c0a5c216f49560e01fb26b9b7e71869
workflow-type: tm+mt
source-wordcount: '1921'
ht-degree: 0%

---

# 3.4.1 Configurare un percorso basato su trigger - Conferma dell’ordine

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`. Ti troverai quindi nella **Home** della tua sandbox `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

## 3.4.1.1 Creare l’evento

Nel menu, vai a **Configurazioni** e fai clic su **Gestisci** in **Eventi**.

![Journey Optimizer](./images/oc30.png)

Nella schermata **Eventi** verrà visualizzata una visualizzazione simile a questa. Fare clic su **Crea evento**.

![Journey Optimizer](./images/oc31.png)

Viene quindi visualizzata una configurazione dell’evento vuota.

Prima di tutto, assegna all&#39;evento un nome come `--aepUserLdap--PurchaseEvent` e aggiungi una descrizione come questa: `Purchase Event`.

Per **Tipo**, selezionare **Unitario**.
Per **Tipo ID evento**, selezionare **Generato dal sistema**.

![Journey Optimizer](./images/eventidtype.png)

Di seguito è riportata la selezione dello schema. Per questo esercizio è stato preparato uno schema. Utilizzare lo schema `Demo System - Event Schema for Website (Global v1.1) v.1`.

Dopo aver selezionato lo schema, nella sezione **Payload** verranno selezionati diversi campi. Fai clic sull&#39;icona **Modifica/Matita** per aggiungere altri campi a questo evento.

![Journey Optimizer](./images/oc36.png)

Poi vedrai questo popup. È ora necessario selezionare caselle di controllo aggiuntive per accedere a dati aggiuntivi quando l’evento viene attivato.

![Journey Optimizer](./images/oc37.png)

Selezionare innanzitutto la casella di controllo alla riga `--aepTenantId--`.

![Journey Optimizer](./images/oc38.png)

Quindi scorrere verso il basso e selezionare la casella di controllo sulla riga `commerce`.

![Journey Optimizer](./images/oc391.png)

Quindi scorrere verso il basso e selezionare la casella di controllo sulla riga `productListItems`. Fare clic su **Ok**.

![Journey Optimizer](./images/oc39.png)

Vedrai quindi che sono stati aggiunti campi aggiuntivi all’evento. Fai clic su **Salva**.

![Journey Optimizer](./images/oc40.png)

Il nuovo evento viene quindi salvato e ora vedrai l’evento nell’elenco degli eventi disponibili.

Fai di nuovo clic sull&#39;evento per aprire di nuovo la schermata **Modifica evento**.
Passa di nuovo il puntatore del mouse sul campo **Payload** per visualizzare nuovamente le 3 icone. Fai clic sull&#39;icona **Visualizza payload**.

![Journey Optimizer](./images/oc41.png)

Ora vedrai un esempio del payload previsto. L&#39;evento ha un ID evento di orchestrazione univoco, che puoi trovare scorrendo verso il basso in tale payload fino a visualizzare `_experience.campaign.orchestration.eventID`.

![Journey Optimizer](./images/oc42.png)

L’ID evento è ciò che deve essere inviato a Adobe Journey Optimizer per attivare il percorso che verrà generato nel passaggio successivo. Scrivere questo eventID, in quanto sarà necessario in uno dei passaggi successivi.
`"eventID": "1c8148a8ab1993537d0ba4e6ac293dd4f2a88d80b2ca7be6293c3b28d4ff5ae6"`

Fai clic su **Ok**, seguito da **Annulla**.

L’evento è ora configurato e pronto per essere utilizzato.

## 3.4.1.2 Creare il percorso

Nel menu, vai a **Percorsi** e fai clic su **Crea Percorso**.

![Journey Optimizer](./images/oc43.png)

Poi vedrai questo. Assegna un nome al percorso. Usa `--aepUserLdap-- - Order Confirmation journey`. Fai clic su **Salva**.

![Journey Optimizer](./images/oc45.png)

Innanzitutto, devi aggiungere l’evento come punto di partenza del percorso. Cercare l&#39;evento `--aepUserLdap--PurchaseEvent` e trascinarlo sull&#39;area di lavoro. Fai clic su **Salva**.

![Journey Optimizer](./images/oc46.png)

Quindi, in **Azioni**, cerca l&#39;azione **E-mail** e aggiungilo all&#39;area di lavoro.

![Journey Optimizer](./images/oc47.png)

Imposta **Categoria** su **Marketing** e seleziona una superficie e-mail che ti consenta di inviare messaggi e-mail. In questo caso, la superficie e-mail da selezionare è **E-mail**. Assicurati che le caselle di controllo per **Clic su e-mail** e **aperture e-mail** siano entrambe abilitate.

![ACOP](./images/journeyactions1.png)

Il passaggio successivo consiste nel creare il messaggio. A tale scopo, fare clic su **Modifica contenuto**.

![ACOP](./images/journeyactions2.png)

Ora vedete questo. Fare clic sul campo di testo **Oggetto**.

![ACOP](./images/journeyactions3.png)

Nell&#39;area di testo inizia a scrivere **Grazie per l&#39;ordine,** e fai clic sull&#39;icona **Personalization**.

![Journey Optimizer](./images/oc5.png)

L’oggetto non è ancora stato completato. Successivamente devi inserire il token di personalizzazione per il campo **First name**, memorizzato in `profile.person.name.firstName`. Nel menu a sinistra, scorri verso il basso per trovare il campo **Persona** > **Nome completo** > **Nome** e fai clic sull&#39;icona **+** per aggiungere il token di personalizzazione nella riga dell&#39;oggetto. Fai clic su **Salva**.

![Journey Optimizer](./images/oc6.png)

Allora tornerai qui. Fai clic su **Modifica corpo dell&#39;e-mail** per creare il contenuto dell&#39;e-mail.

![Journey Optimizer](./images/oc7.png)

Nella schermata successiva, fai clic su **Progetta da zero**.

![Journey Optimizer](./images/oc8.png)

Nel menu a sinistra trovi i componenti struttura che puoi utilizzare per definire la struttura dell’e-mail (righe e colonne).

Trascina e rilascia 8 volte una **colonna 1:1** nell&#39;area di lavoro, per ottenere quanto segue:

![Journey Optimizer](./images/oc9.png)

Nel menu a sinistra, vai a **Frammenti**. Trascina l’intestazione creata in precedenza nell’esercizio 3.2.2 sul primo componente nell’area di lavoro. Trascinare il piè di pagina creato in precedenza nell&#39;esercizio 3.2.2 sull&#39;ultimo componente dell&#39;area di lavoro.

![Journey Optimizer](./images/fragm1.png)

Fai clic sull&#39;icona **+** nel menu a sinistra. Vai a **Sommario** per iniziare ad aggiungere contenuti all&#39;area di lavoro.

![Journey Optimizer](./images/oc10.png)

Vai a **Sommario** e trascina un componente **Immagine** sulla seconda riga. Fare clic su **Sfoglia**.

![Journey Optimizer](./images/oc15.png)

Apri la cartella **citi-signal-images**, fai clic per selezionare l&#39;immagine **citisignal-preparation.png**, quindi fai clic su **Select**.

![Journey Optimizer](./images/oc14.png)

In **Stili**, modifica la larghezza in **40%**.

![Journey Optimizer](./images/oc14a.png)

Quindi, vai a **Sommario** e trascina un componente **Testo** sulla terza riga.

![Journey Optimizer](./images/oc17.png)

Selezionare il testo predefinito nel componente **Digitare qui il testo.** e sostituirlo con il testo seguente:

```javascript
You’re one step closer!

Hi 

We've received your order details!

We will also send you a separate email containing your VAT Invoice.

We'll be back in touch with you as soon as we've finished packing your package. Please read carefully the Order Information detailed below.
```

![Journey Optimizer](./images/oc18.png)

Posizionare il cursore accanto al testo **Ciao** e fare clic su **Aggiungi Personalization**.

![Journey Optimizer](./images/oc19.png)

Passa al campo **Persona** > **Nome completo** > **Nome** e fai clic sull&#39;icona **+** per aggiungere il token di personalizzazione nella riga dell&#39;oggetto. Fai clic su **Salva**.

![Journey Optimizer](./images/oc20.png)

A questo punto viene visualizzato quanto segue:

![Journey Optimizer](./images/oc21.png)

Quindi, vai a **Sommario** e trascina un componente **Testo** sulla quarta riga.

![Journey Optimizer](./images/oc22.png)

Selezionare il testo predefinito nel componente **Digitare qui il testo.** e sostituirlo con il testo seguente:

`Order Information`

Cambia la dimensione del carattere in **26px** e centrare il testo in questa cella. A questo punto si otterrà:

![Journey Optimizer](./images/oc23.png)

Quindi, vai a **Sommario** e trascina un componente **HTML** sulla quinta riga. Fare clic sul componente HTML e quindi su **Mostra il codice sorgente**.

![Journey Optimizer](./images/oc24.png)

Nel popup **Modifica HTML**, incolla questo HTML:

```<table><tbody><tr><td><b>Items purchased</b></td><td></td><td><b>Quantity</b></td><td><b>Subtotal</b></td></tr><tr><td colspan="4" width="500"><hr></td></tr></tbody></table>```

Fai clic su **Salva**.

![Journey Optimizer](./images/oc25.png)

Allora avrai questo. Fai clic su **Salva** per salvare l&#39;avanzamento.

![Journey Optimizer](./images/oc26.png)

Vai a **Sommario** e trascina un componente **HTML** sulla sesta riga. Fare clic sul componente HTML e quindi su **Mostra il codice sorgente**.

![Journey Optimizer](./images/oc57.png)

Nel popup **Modifica HTML**, incolla questo HTML:

```{{#each xxx as |item|}}<table width="500"><tbody><tr><td><img src="{{item.--aepTenantId--.core.imageURL}}" width="100"></td><td><table><tbody><tr><td><b>{{item.name}}</b><br>{{item.--aepTenantId--.core.subCategory}}<br><b>{{item.priceTotal}}</b><br>&nbsp;<br>Article no: {{item.SKU}}</td></tr></tbody></table></td><td>{{item.quantity}}</td><td><b>{{item.priceTotal}}</b></td></tr></tbody></table>{{/each}}```

A questo punto si otterrà:

![Journey Optimizer](./images/oc58.png)

È ora necessario sostituire **xxx** con un riferimento all&#39;oggetto productListItems che fa parte dell&#39;evento che attiva il percorso.

![Journey Optimizer](./images/oc59.png)

Elimina prima **xxx** nel codice HTML.

![Journey Optimizer](./images/oc60.png)

Nel menu a sinistra, fai clic su **Attributi contestuali**. Questo contesto viene passato al messaggio dal percorso.

Poi vedrai questo. Fai clic sulla freccia accanto a **Journey Orchestration** per approfondire.

![Journey Optimizer](./images/oc601.png)

Fai clic sulla freccia accanto a **Eventi** per approfondire.

![Journey Optimizer](./images/oc62.png)

Fare clic sulla freccia accanto a `--aepUserLdap--PurchaseEvent` per approfondire.

![Journey Optimizer](./images/oc63.png)

Fai clic sulla freccia accanto a **productListItems** per approfondire.

![Journey Optimizer](./images/oc64.png)

Fai clic sull&#39;icona **+** accanto a **Name** per aggiungerla all&#39;area di lavoro. Allora avrai questo. Selezionare **.name** come indicato nella schermata seguente, quindi rimuovere **.name**.

![Journey Optimizer](./images/oc65.png)

Allora avrai questo. Fai clic su **Salva**.

![Journey Optimizer](./images/oc66.png)

Ora tornerai al Designer delle e-mail. Fai clic su **Salva** per salvare l&#39;avanzamento.

![Journey Optimizer](./images/oc67.png)

Quindi, vai a **Sommario** e trascina un componente **HTML** sulla settima riga. Fare clic sul componente HTML e quindi su **Mostra il codice sorgente**.

![Journey Optimizer](./images/oc68.png)

Nel popup **Modifica HTML**, incolla questo HTML:

```<table><tbody><tr><td><b>Subtotal</b><br>Delivery charge (included)</td><td align="right"><b>xxx</b><br><b>5</b></td></tr><tr><td colspan="2" width="500"><hr></td></tr><tr><td><b>Total including VAT</b></td><td align="right"><b>xxx</b></td></tr></tbody></table>```

In questo codice HTML sono presenti 2 riferimenti di **xxx**. È ora necessario sostituire ogni **xxx** con un riferimento all&#39;oggetto productListItems che fa parte dell&#39;evento che attiva il percorso.

![Journey Optimizer](./images/oc69.png)

Elimina innanzitutto il primo **xxx** nel codice HTML.

![Journey Optimizer](./images/oc71.png)

Nel menu a sinistra, fai clic su **Attributi contestuali**.
Fai clic sulla freccia accanto a **Journey Orchestration** per approfondire.

![Journey Optimizer](./images/oc72.png)

Fai clic sulla freccia accanto a **Eventi** per approfondire.

![Journey Optimizer](./images/oc722.png)

Fare clic sulla freccia accanto a `--aepUserLdap--PurchaseEvent` per approfondire.

![Journey Optimizer](./images/oc73.png)

Fai clic sulla freccia accanto a **Commerce** per approfondire.

![Journey Optimizer](./images/oc733.png)

Fai clic sulla freccia accanto a **Ordine** per approfondire.

![Journey Optimizer](./images/oc74.png)

Fai clic sull&#39;icona **+** accanto a **Prezzo totale** per aggiungerla all&#39;area di lavoro.

![Journey Optimizer](./images/oc75.png)

Allora avrai questo. Ora elimina il secondo **xxx** nel codice HTML.

![Journey Optimizer](./images/oc76.png)

Fai di nuovo clic sull&#39;icona **+** accanto a **Prezzo totale** per aggiungerla all&#39;area di lavoro.
È inoltre possibile aggiungere il campo **Valuta** dall&#39;interno dell&#39;oggetto **Ordine** all&#39;area di lavoro, come illustrato in questa sezione.
Al termine, fai clic su **Salva** per salvare le modifiche.

![Journey Optimizer](./images/oc77.png)

Tornerai a utilizzare E-mail Designer. Fai di nuovo clic su **Salva**.

![Journey Optimizer](./images/oc78.png)

Torna alla dashboard dei messaggi facendo clic sulla **freccia** accanto al testo dell&#39;oggetto nell&#39;angolo in alto a sinistra.

![Journey Optimizer](./images/oc79.png)

Fai clic sulla freccia nell’angolo in alto a sinistra per tornare al percorso.

![Journey Optimizer](./images/oc79a.png)

Fai clic su **Salva** per chiudere l&#39;azione e-mail.

![Journey Optimizer](./images/oc79b.png)

Fai clic su **Publish** per pubblicare il percorso.

![Journey Optimizer](./images/oc511.png)

Fai di nuovo clic su **Publish**.

![Journey Optimizer](./images/oc512.png)

Il percorso è stato pubblicato.

![Journey Optimizer](./images/oc513.png)

## 3.4.1.5 Aggiornare la proprietà Client di raccolta dati di Adobe Experience Platform

Vai a [Raccolta dati Adobe Experience Platform](https://experience.adobe.com/launch/) e seleziona **Tag**.

Questa è la pagina Proprietà raccolta dati di Adobe Experience Platform che hai visto prima.

![Pagina delle proprietà](./../../../modules/datacollection/module1.1/images/launch1.png)

In **Guida introduttiva**, Demo System ha creato due proprietà client: una per il sito Web e una per l&#39;app mobile. Trovarli cercando `--aepUserLdap--` nella casella **[!UICONTROL Cerca]**. Fare clic per aprire la proprietà **Web**.

![Casella di ricerca](./../../../modules/datacollection/module1.1/images/property6.png)

Vai a **Elementi dati**. Cerca e apri l&#39;elemento dati **XDM - Purchase**.

![Journey Optimizer](./images/oc91.png)

Poi vedrai questo. Passa al campo **_experience.campaign.orchestration.eventID** e compila qui il tuo eventID. L&#39;eventID da compilare qui è l&#39;eventID che hai creato come parte dell&#39;esercizio 3.4.1.1 Fai clic su **Salva** o **Salva nella libreria**.

![Journey Optimizer](./images/oc92.png)

Salva le modifiche nella proprietà, quindi pubblica le modifiche aggiornando la libreria di sviluppo.

![Journey Optimizer](./images/oc93.png)

Le modifiche sono ora implementate e possono essere testate.

## 3.4.1.6 Verifica l’e-mail di conferma dell’ordine utilizzando il sito web demo

Testiamo il percorso aggiornato acquistando un prodotto sul sito web demo.

Vai a [https://dsn.adobe.com](https://dsn.adobe.com). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sui tre punti **...** del progetto del sito Web, quindi fai clic su **Esegui** per aprirlo.

![DSN](./../../datacollection/module1.1/images/web8.png)

Poi vedrai il tuo sito web demo aperto. Seleziona l’URL e copialo negli Appunti.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Apri una nuova finestra del browser in incognito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Incolla l’URL del sito web demo, che hai copiato nel passaggio precedente. Ti verrà quindi chiesto di effettuare l’accesso con il tuo Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Seleziona il tipo di account e completa la procedura di accesso.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Vedrai quindi il tuo sito web caricato in una finestra del browser in incognito. Per ogni esercizio, dovrai utilizzare una nuova finestra del browser in incognito per caricare l’URL del sito web demo.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Dai un&#39;occhiata al pannello Visualizzatore profili e al Profilo cliente in tempo reale con **ID Experience Cloud** come identificatore primario per questo cliente attualmente sconosciuto.

![Demo](./../../../modules/datacollection/module1.2/images/pv2.png)

Vai alla pagina di registrazione/accesso. Fare clic su **CREA UN ACCOUNT**.

![Demo](./../../../modules/datacollection/module1.2/images/pv9.png)

Compila i tuoi dettagli e fai clic su **Registra** dopo di che sarai reindirizzato alla pagina precedente.

![Demo](./../../../modules/datacollection/module1.2/images/pv10.png)

Aggiungi qualsiasi prodotto al carrello

![Journey Optimizer](./images/cart1a.png)

Vai alla pagina **Carrello**. Fai clic su **Estrai**.

![Journey Optimizer](./images/cart1.png)

Quindi, verifica i campi e completa se necessario. Fai clic su **Procedi**.

![Journey Optimizer](./images/cart2.png)

Fai clic su **Conferma ordine**.

![Journey Optimizer](./images/cart2a.png)

Il tuo ordine è ora confermato.

![Journey Optimizer](./images/cart2b.png)

Riceverai quindi l’e-mail di conferma dell’ordine entro pochi secondi.

![Journey Optimizer](./images/oc98.png)

Hai finito questo esercizio.

Passaggio successivo: [3.4.2 Configurare un percorso di newsletter basato su batch](./ex2.md)

[Torna al modulo 3.4](./journeyoptimizer.md)

[Torna a tutti i moduli](../../../overview.md)
