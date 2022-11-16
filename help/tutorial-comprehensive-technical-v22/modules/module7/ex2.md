---
title: Journey Optimizer Crea il tuo percorso e messaggio e-mail
description: Journey Optimizer Crea il tuo messaggio e-mail
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 2b7333c3-5b6a-41c5-a7a7-b048d1579ddd
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 5%

---

# 7.2 Creare il percorso e il messaggio e-mail

In questo esercizio, configurerai il percorso e il messaggio da attivare quando qualcuno crea un account sul sito web demo.

Accedi a Adobe Journey Optimizer accedendo a [Adobe Experience Cloud](https://experience.adobe.com). Fai clic su **Journey Optimizer**.

![ACOP](./images/acophome.png)

Verrai reindirizzato al **Pagina principale**  in Journey Optimizer. In primo luogo, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare è denominata `--aepSandboxId--`. Per passare da una sandbox all’altra, fai clic su **PROD DI PRODUZIONE (VA7)** e selezionate la sandbox dall’elenco. In questo esempio, la sandbox è denominata **Abilitazione AEP FY22**. Allora sarai nel **Pagina principale** visualizzazione della sandbox `--aepSandboxId--`.

![ACOP](./images/acoptriglp.png)

## 7.2.1 Crea il tuo percorso

Nel menu a sinistra, fai clic su **Percorsi**. Quindi, fai clic su **Crea Percorso** per creare un nuovo percorso.

![ACOP](./images/createjourney.png)

Verrà visualizzata una schermata di percorso vuota.

![ACOP](./images/journeyempty.png)

Nell’esercizio precedente, hai creato una nuova **Evento**. L&#39;hai chiamato così `ldapAccountCreationEvent` e sostituito `ldap` con il tuo ldap. Questo è stato il risultato della creazione dell’evento:

![ACOP](./images/eventdone.png)

Ora devi prendere questo evento come inizio di questo Percorso. Per farlo, vai sul lato sinistro dello schermo e cerca l’evento nell’elenco degli eventi.

![ACOP](./images/eventlist.png)

Seleziona l’evento, trascinalo sull’area di lavoro del Percorso e rilascialo. Il tuo Percorso ora si presenta così:

![ACOP](./images/journeyevent.png)

Come secondo passaggio del percorso, devi aggiungere una breve **Wait** passo. Passa al lato sinistro dello schermo e **Orchestrazione** per trovare questo. Utilizzerai gli attributi del profilo e dovrai accertarti che siano popolati nel Profilo del cliente in tempo reale.

![ACOP](./images/journeywait.png)

Il tuo percorso ora assomiglia a questo. Sul lato destro dello schermo è necessario configurare il tempo di attesa. Impostalo a 1 minuto. In questo modo gli attributi del profilo saranno disponibili per un periodo di tempo sufficiente dopo l’attivazione dell’evento.

![ACOP](./images/journeywait1.png)

Fai clic su **Ok** per salvare le modifiche.

Come terzo passaggio del percorso, devi aggiungere un **E-mail** azione. Vai al lato sinistro dello schermo fino a **Azioni**, seleziona **E-mail** , quindi trascinalo sul secondo nodo del percorso. Ora vedete questo.

![ACOP](./images/journeyactions.png)

Imposta la **Categoria** a **Marketing** e seleziona una superficie e-mail che ti consente di inviare e-mail. In questo caso, la superficie dell’e-mail da selezionare è **E-mail**. Assicurati che le caselle di controllo per **Clic su e-mail** e **aperture e-mail** sono entrambi abilitati.

![ACOP](./images/journeyactions1.png)

Il passaggio successivo consiste nel creare il messaggio. A tale scopo, fai clic su **Modifica contenuto**.

![ACOP](./images/journeyactions2.png)

## 7.2.2 Creare il messaggio

Per creare il messaggio, fai clic su **Modifica contenuto**.

![ACOP](./images/journeyactions2.png)

Ora vedete questo.

![ACOP](./images/journeyactions3.png)

Fai clic sul pulsante **Linea oggetto** campo di testo.

![Journey Optimizer](./images/msg5.png)

Nell’area di testo inizia la scrittura **Ciao**

![Journey Optimizer](./images/msg6.png)

L&#39;oggetto non è ancora stato completato. Ora devi inserire il token di personalizzazione per il campo **Nome** che è immagazzinato in `profile.person.name.firstName`. Nel menu a sinistra, scorri verso il basso per trovare il **Persona** e fai clic sulla freccia per andare un livello più profondo.

![Journey Optimizer](./images/msg7.png)

Ora trova la **Nome completo** e fai clic sulla freccia per andare un livello più profondo.

![Journey Optimizer](./images/msg8.png)

Infine, trova il **Nome** e fai clic sul **+** firmi accanto a esso. Il token di personalizzazione verrà visualizzato nel campo di testo.

![Journey Optimizer](./images/msg9.png)

Quindi, aggiungi il testo **Grazie per esserti registrato!**. Fai clic su **Salva**.

![Journey Optimizer](./images/msg10.png)

Allora tornerai qui. Fai clic su **E-mail Designer** per creare il contenuto dell’e-mail.

![Journey Optimizer](./images/msg11.png)

Nella schermata successiva verranno visualizzati 3 metodi diversi per fornire il contenuto dell’e-mail:

- **Progettazione da zero**: Inizia con un’area di lavoro vuota e utilizza l’editor WYSIWYG per trascinare e rilasciare componenti di struttura e contenuto per creare visivamente il contenuto dell’e-mail.
- **Codice personalizzato**: Crea il tuo modello e-mail codificandolo utilizzando HTML
- **Importa HTML**: Importa un modello HTML esistente, che potrai modificare.

Fai clic su **Progettazione da zero**.

![Journey Optimizer](./images/msg12.png)

Nel menu a sinistra trovi i componenti struttura che puoi utilizzare per definire la struttura dell’e-mail (righe e colonne).

![Journey Optimizer](./images/msg13.png)

Trascina e rilascia una **Colonna 1:2 a sinistra** dal menu nell’area di lavoro. Segnaposto per l’immagine del logo.

![Journey Optimizer](./images/msg14.png)

Trascina e rilascia una **Colonna 1:1** sotto il componente precedente. Questo sarà il blocco banner.

![Journey Optimizer](./images/msg15.png)

Trascina e rilascia una **Colonna 1:2 a sinistra** sotto il componente precedente. Sarà il contenuto effettivo con un’immagine sul lato sinistro e del testo sul lato destro.

![Journey Optimizer](./images/msg16.png)

Quindi, trascina e rilascia una **Colonna 1:1** sotto il componente precedente. Questo sarà il piè di pagina dell’e-mail. A questo punto la tela deve avere questo aspetto:

![Journey Optimizer](./images/msg17.png)

Quindi, utilizziamo Componenti contenuto per aggiungere contenuto all’interno di questi blocchi. Fai clic sul pulsante **Componenti contenuto** voce di menu

![Journey Optimizer](./images/msg18.png)

Trascina e rilascia una **Immagine** nella prima cella della prima riga. Fai clic su **Sfoglia**.

![Journey Optimizer](./images/msg19.png)

Vedrete questo. Passa alla cartella **enablement-assets** e selezionare il file **luma-logo.png**. Fai clic su **Seleziona**.

![Journey Optimizer](./images/msg21.png)

Ora sei di nuovo qui:

![Journey Optimizer](./images/msg25.png)

Vai a **Componenti contenuto** e trascinare un **Immagine** nella prima cella della prima riga. Fai clic su **Sfoglia**.

![Journey Optimizer](./images/msg26.png)

In **Risorse** pop-up, vai al **enablement-assets** cartella. In questa cartella trovi tutte le risorse precedentemente preparate e caricate dal team creativo. Seleziona **module23-grazie-new.png** e fai clic su **Seleziona**.

![Journey Optimizer](./images/msg28.png)

A quel punto avrai questo:

![Journey Optimizer](./images/msg30.png)

Seleziona l’immagine e scorri verso il basso nel menu di destra fino a visualizzare la **Dimensione** componente cursore larghezza. Usa il cursore per cambiare la larghezza in f.i. **60%**.

![Journey Optimizer](./images/msg31.png)

Quindi, vai a **Componenti contenuto** e trascina e rilascia una **Testo** nel componente struttura nella quarta riga.

![Journey Optimizer](./images/msg33.png)

Selezionare il testo predefinito **Digitare il testo qui.** come per qualsiasi editor di testo. Scrivi **Gentile** invece. La barra degli strumenti Testo viene visualizzata in modalità testo.

![Journey Optimizer](./images/msg34.png)

Nella barra degli strumenti, fai clic su **Aggiungi personalizzazione** icona.

![Journey Optimizer](./images/msg35.png)

Successivamente, devi portare il **Nome** token di personalizzazione memorizzato in `profile.person.name.firstName`. Nel menu , trova la **Persona** elemento, scegli **Nome completo** , quindi fai clic sul **+** per aggiungere il campo Nome all’editor di espressioni.

Fai clic su **Salva**.

![Journey Optimizer](./images/msg36.png)

Ora noterai come il campo di personalizzazione è stato aggiunto al testo.

![Journey Optimizer](./images/msg37.png)

Nello stesso campo di testo, premi **Invio** due volte per aggiungere due righe e scrivere **Grazie per aver creato il tuo account con Luma!**.

![Journey Optimizer](./images/msg38.png)

Il controllo finale da eseguire per verificare che l’e-mail sia pronta per essere visualizzata in anteprima, fai clic sul pulsante **Simula contenuto** pulsante .

![Journey Optimizer](./images/msg50.png)

Per iniziare, identifica il profilo da utilizzare per l’anteprima. Seleziona la **email** namespace facendo clic sull’icona accanto a **Immettere lo spazio dei nomi identità** campo .

Nell’elenco dei namespace delle identità, seleziona la **E-mail** spazio dei nomi.

In **Valore identità** immetti l’indirizzo e-mail di un profilo demo precedente già memorizzato nel Profilo cliente in tempo reale. Esempio **woutervangeluwe+06022022-01@gmail.com** e fai clic su **Trova profilo di test** pulsante

![Journey Optimizer](./images/msg53.png)

Una volta che il tuo profilo si presenta nella tabella, fai clic sul **Anteprima** per accedere alla schermata di anteprima.

Quando l’anteprima è pronta, verifica che la personalizzazione sia corretta nella riga dell’oggetto, che il testo del corpo e il collegamento di annullamento all’abbonamento siano evidenziati come collegamento ipertestuale.

Fai clic su **Chiudi** per chiudere l&#39;anteprima.

![Journey Optimizer](./images/msg54.png)

Fai clic su **Salva** per salvare il messaggio.

![Journey Optimizer](./images/msg55.png)

Torna al dashboard dei messaggi facendo clic sul pulsante **freccia** accanto all’oggetto nell’angolo in alto a sinistra.

![Journey Optimizer](./images/msg56.png)

Hai completato la creazione del messaggio e-mail di registrazione. Fai clic sulla freccia nell&#39;angolo in alto a sinistra per tornare al percorso.

![Journey Optimizer](./images/msg57.png)

Fai clic su **Ok**.

![Journey Optimizer](./images/msg57a.png)

## 7.2.3 Pubblicare il percorso

Devi ancora dare un Nome al tuo percorso. Per farlo, fai clic sul pulsante **Proprietà** in alto a destra sullo schermo.

![ACOP](./images/journeyname.png)

Potete quindi inserire il nome del percorso qui. Utilizzare `--demoProfileLdap-- - Account Creation Journey`. Fai clic su **OK** per salvare le modifiche.

![ACOP](./images/journeyname1.png)

Ora puoi pubblicare il percorso facendo clic su **Pubblica**.

![ACOP](./images/publishjourney.png)

Fai clic su **Pubblica** di nuovo.

![ACOP](./images/publish1.png)

Verrà visualizzata una barra di conferma verde che indica che il percorso è ora Pubblicato.

![ACOP](./images/published.png)

Ora avete finito questo esercizio.

Passaggio successivo: [7.3 Aggiorna la proprietà Data Collection e verifica il percorso](./ex3.md)

[Torna al modulo 7](./journey-orchestration-create-account.md)

[Torna a tutti i moduli](../../overview.md)
