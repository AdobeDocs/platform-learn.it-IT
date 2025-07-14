---
title: Journey Optimizer Crea il tuo percorso e messaggio e-mail
description: Journey Optimizer Crea il tuo messaggio e-mail
kt: 5342
doc-type: tutorial
exl-id: e264ab9e-e7f1-4a0b-b3b7-17003c40f17a
source-git-commit: ea8255de9869061cd21d2b5e7c8690f84be0a25b
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 0%

---

# 3.1.3 Creare il percorso e il messaggio e-mail

In questo esercizio configurerai il percorso e il messaggio da attivare quando qualcuno crea un account sul sito web demo.

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`.

![ACOP](./images/acoptriglp.png)

## 3.1.3.1 Crea il tuo Percorso

Nel menu a sinistra, fai clic su **Percorsi**. Fare clic su **Crea Percorso** per creare un nuovo percorso.

![ACOP](./images/createjourney.png)

Viene quindi visualizzata una schermata di percorso vuota.

![ACOP](./images/journeyempty.png)

Nell&#39;esercizio precedente è stato creato un nuovo **evento**. L&#39;hai denominato così `--aepUserLdap--AccountCreationEvent`. Questo è stato il risultato della creazione dell’evento:

![ACOP](./images/eventdone.png)

Ora devi prendere questo evento come inizio di questo Percorso. Per farlo, vai sul lato sinistro della schermata e cerca l’evento nell’elenco degli eventi.

![ACOP](./images/eventlist.png)

Seleziona l’evento, trascinalo sull’area di lavoro del percorso. Il percorso si presenta ora come segue:

![ACOP](./images/journeyevent.png)

Come secondo passaggio del percorso, devi aggiungere un breve passaggio **Attendi**. Vai sul lato sinistro della schermata alla sezione **Orchestration** per trovarlo. Utilizzerai gli attributi del profilo e dovrai accertarti che siano popolati in Real-time Customer Profile.

![ACOP](./images/journeywait.png)

Il tuo percorso ora si presenta così. Sul lato destro dello schermo è necessario configurare il tempo di attesa. Imposta su 1 minuto. In questo modo gli attributi del profilo saranno disponibili dopo l’attivazione dell’evento. Fai clic su **Salva** per salvare le modifiche.

![ACOP](./images/journeywait1.png)

Come terzo passaggio del percorso, devi aggiungere un&#39;azione **E-mail**. Vai sul lato sinistro della schermata a **Azioni**, seleziona l&#39;azione **E-mail**, quindi trascinala sul secondo nodo del percorso. Ora vedete questo.

![ACOP](./images/journeyactions.png)

Imposta **Categoria** su **Marketing** e seleziona una configurazione e-mail che ti consenta di inviare messaggi e-mail. In questo caso, la configurazione e-mail da selezionare è **Email-TI**.

![ACOP](./images/journeyactions1.png)

## 3.1.3.2 Crea il tuo messaggio

Per creare il messaggio, fai clic su **Modifica contenuto**.

![ACOP](./images/journeyactions2.png)

Ora vedete questo.

![ACOP](./images/journeyactions3.png)

Fai clic sull&#39;icona **Apri finestra di personalizzazione**.

![Journey Optimizer](./images/msg5.png)

Scrivere il testo `Hi `. Successivamente devi inserire il token di personalizzazione per il campo **First name**, memorizzato in `profile.person.name.firstName`. Nel menu a sinistra, individua il campo **Persona > Nome completo > Nome** e fai clic sull&#39;icona **+**. Il token di personalizzazione verrà quindi visualizzato nel campo di testo.

![Journey Optimizer](./images/msg9.png)

Quindi, aggiungere il testo **. Grazie per la registrazione.**. Fai clic su **Salva**.

![Journey Optimizer](./images/msg10.png)

Ora puoi iniziare a configurare il corpo dell’e-mail. Fai clic su **Modifica corpo dell&#39;e-mail**.

![Journey Optimizer](./images/msg11.png)

Prima di iniziare a creare il contenuto del messaggio effettivo, è consigliabile considerare il contenuto del messaggio. Alcuni contenuti del messaggio sono specifici per il messaggio stesso, ma altre parti sono componenti standard che probabilmente saranno gli stessi per ogni e-mail che invierai ai clienti.

Nell’esercizio precedente, hai già creato questi componenti standard come Frammenti in Journey Optimizer, a cui ora puoi fare riferimento in questo messaggio e in tutti gli altri messaggi futuri che creerai.

Nella schermata successiva ti verranno richiesti 3 metodi diversi per fornire il contenuto dell’e-mail:

- **Progettazione da zero**: inizia con un&#39;area di lavoro vuota e utilizza l&#39;editor di WYSIWYG per trascinare i componenti struttura e contenuto per creare visivamente il contenuto dell&#39;e-mail.
- **Crea un codice personale**: crea un modello di e-mail personalizzato codificandolo con HTML
- **Importa HTML**: importa un modello HTML esistente che potrai modificare.

Fare clic su **Progetta da zero**.

![Journey Optimizer](./images/msg12.png)

Nel menu a sinistra trovi i componenti struttura che puoi utilizzare per definire la struttura dell’e-mail (righe e colonne).

![Journey Optimizer](./images/msg13.png)

Troverai anche **Frammenti** nel menu a sinistra, dove vedrai i frammenti creati in precedenza.

![Journey Optimizer](./images/msg14.png)

Prima di poter aggiungere l’intestazione e il piè di pagina all’area di lavoro, è necessario aggiungere 2 strutture all’e-mail. Fai clic sull&#39;icona **+** nel menu a sinistra e trascina 2 componenti **1:1 column** nell&#39;area di lavoro.

![Journey Optimizer](./images/msg14a.png)

Nel menu a sinistra, torna a **Frammenti**. Trascina il frammento di intestazione nel primo componente e il frammento di piè di pagina nel secondo componente. Poi vedrai questo.

![Journey Optimizer](./images/msg15.png)

Fai clic sull&#39;icona **+** nel menu a sinistra e trascina altri 2 componenti **1:1 column** nell&#39;area di lavoro, tra l&#39;intestazione e il piè di pagina.

![Journey Optimizer](./images/msg16.png)

Trascina e rilascia un componente **Immagine** nel primo componente **1:1 colonna**. Fare clic su **Sfoglia**.

![Journey Optimizer](./images/msg17.png)

Nella cartella **citi-signal-images**. Selezionare l&#39;immagine **`welcome_email_image.png`** e fare clic su **Seleziona**.

![Journey Optimizer](./images/msg28.png)

A questo punto si otterrà:

![Journey Optimizer](./images/msg30.png)

Quindi, vai a **Sommario** e trascina un componente **Testo** nel componente struttura nella quarta riga.

![Journey Optimizer](./images/msg33.png)

Selezionare il testo predefinito **Digitare qui il testo.** come si farebbe con qualsiasi editor di testo. Scrivi invece **Benvenuto nella famiglia**. Nella barra degli strumenti, fai clic sull&#39;icona **Aggiungi personalizzazione**.

![Journey Optimizer](./images/msg34.png)

Successivamente, devi portare il token di personalizzazione **First name** memorizzato in `profile.person.name.firstName`. Nel menu, trovare l&#39;elemento **Person**, espandere l&#39;elemento **Full Name** e quindi fare clic sull&#39;icona **+** per aggiungere il campo First Name all&#39;editor di espressioni.

Fai clic su **Salva**.

![Journey Optimizer](./images/msg36.png)

Ora noterai come il campo di personalizzazione è stato aggiunto al testo.

![Journey Optimizer](./images/msg37.png)

Nello stesso campo di testo, premere **Invio** due volte per aggiungere due righe e copiare e incollare il testo seguente:

```
Welcome aboard! We're thrilled to have you join the CitiSignal family. 
As a valued member of our community, you're now poised to experience top-notch telecommunications services that cater to your every need.

At CitiSignal, we understand that staying connected is more than just a convenience - it's a necessity. Whether you're browsing the web, streaming your favourite content, or keeping in touch with loved ones, we're here to ensure you have the best tools and resources at your fingertips.
```

![Journey Optimizer](./images/msg38.png)

Imposta l&#39;allineamento del testo **Allineamento testo** da centrare e puoi modificare l&#39;aspetto del messaggio in base alle tue esigenze. Al termine, fai clic su **Salva**.

![Journey Optimizer](./images/msg39.png)

Il controllo finale da eseguire per verificare che l&#39;e-mail sia pronta è l&#39;anteprima, fare clic sul pulsante **Simula contenuto**.

![Journey Optimizer](./images/msg50.png)

Prima di poter simulare il messaggio e-mail, devi aggiungere un profilo di test. Fare clic su **Gestisci profili di test**.

![Journey Optimizer](./images/test1.png)

Seleziona lo spazio dei nomi **email** facendo clic sull&#39;icona accanto al campo **Enter identity namespace** (Inserisci spazio dei nomi delle identità).

Nell&#39;elenco degli spazi dei nomi di identità, seleziona lo spazio dei nomi **E-mail**. Nel campo **Valore identità** immettere l&#39;indirizzo di posta elettronica di un profilo precedente utilizzato in un esercizio precedente e già archiviato in Adobe Experience Platform. Fare clic su **Aggiungi profilo**. Torna alla schermata precedente.

![Journey Optimizer](./images/msg53.png)

Visualizzerai quindi il tuo messaggio e-mail, ora simulato per questo profilo cliente. Ora puoi convalidare la personalizzazione nell’oggetto e nel corpo e inviare un’e-mail di bozza, se necessario.

Fai clic su **Chiudi** per chiudere l&#39;anteprima.

![Journey Optimizer](./images/msg54.png)

Fai clic su **Salva** per salvare il messaggio e tornare alla dashboard dei messaggi facendo clic sulla **freccia** accanto al testo dell&#39;oggetto nell&#39;angolo in alto a sinistra.

![Journey Optimizer](./images/msg55.png)

Fai clic sulla **freccia** per tornare al percorso.

![Journey Optimizer](./images/msg57a.png)

## 3.1.3.3 Pubblica il tuo percorso

Fai clic su **Salva**.

![Journey Optimizer](./images/msg58.png)

È comunque necessario assegnare un nome al percorso. Per farlo, fai clic sull&#39;icona **Proprietà** in alto a destra nella schermata.

![ACOP](./images/journeyname.png)

È quindi possibile immettere qui il nome del percorso. Utilizzare `--aepUserLdap-- - Registration Journey`. Fai clic su **Salva**.

![ACOP](./images/journeyname1.png)

Per pubblicare il percorso, fai clic su **Pubblica**.

![ACOP](./images/publishjourney.png)

Fai di nuovo clic su **Pubblica**.

![ACOP](./images/publish1.png)

Dopo alcuni minuti, lo stato del percorso passerà a **Live** e vedrai una dashboard in tempo reale delle prestazioni del percorso.

![ACOP](./images/published.png)

Hai terminato questo esercizio.

## Passaggi successivi

Vai a [3.1.4 Aggiorna la proprietà di raccolta dati e verifica il percorso](./ex4.md){target="_blank"}

Torna a [Adobe Journey Optimizer: orchestrazione](./journey-orchestration-create-account.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
