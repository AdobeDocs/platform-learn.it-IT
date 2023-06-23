---
title: Bootcamp - Journey Optimizer Crea il tuo percorso e messaggio e-mail
description: Bootcamp - Journey Optimizer Crea il tuo percorso e messaggio e-mail
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 138a70fa-fe50-4585-b47f-150db4770c3d
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 4%

---

# 2.3 Creare il percorso e il messaggio e-mail

In questo esercizio configurerai il percorso che deve essere attivato quando qualcuno crea un account sul sito web demo.

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Clic **Journey Optimizer**.

![ACOP](./images/acophome.png)

Verrai reindirizzato al **Home**  in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `Bootcamp`. Per passare da una sandbox all’altra, fai clic su **Prod** e seleziona la sandbox dall’elenco. In questo esempio, la sandbox è denominata **Bootcamp**. Sarai quindi nel **Home** visualizzazione della sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Creare il percorso

Nel menu a sinistra, fai clic su **Percorsi**. Quindi, fai clic su **Crea Percorso** per creare un nuovo percorso.

![ACOP](./images/createjourney.png)

Viene quindi visualizzata una schermata di percorso vuota.

![ACOP](./images/journeyempty.png)

Nell’esercizio precedente, hai creato una nuova **Evento**. L&#39;hai chiamato così `yourLastNameAccountCreationEvent` e sostituito `yourLastName` con il tuo cognome. Questo è stato il risultato della creazione dell’evento:

![ACOP](./images/eventdone.png)

Ora devi prendere questo evento come inizio di questo Percorso. Per farlo, vai sul lato sinistro della schermata e cerca l’evento nell’elenco degli eventi.

![ACOP](./images/eventlist.png)

Seleziona l’evento, trascinalo sull’area di lavoro del Percorso. Il Percorso si presenta ora come segue:

![ACOP](./images/journeyevent.png)

Come secondo passaggio del percorso, è necessario aggiungere un breve **Wait** passaggio. Passa alla parte sinistra dello schermo per **Orchestrazione** per trovare questo. Utilizzerai gli attributi del profilo e dovrai accertarti che siano popolati in Real-time Customer Profile.

![ACOP](./images/journeywait.png)

Il tuo percorso ora si presenta così. Sul lato destro dello schermo è necessario configurare il tempo di attesa. Imposta su 1 minuto. In questo modo gli attributi del profilo saranno disponibili dopo l’attivazione dell’evento.

![ACOP](./images/journeywait1.png)

Clic **Ok** per salvare le modifiche.

Come terzo passaggio del percorso, devi aggiungere un’ **E-mail** azione. Vai sul lato sinistro dello schermo per **Azioni**, seleziona la **E-mail** , quindi trascinarlo e rilasciarlo sul secondo nodo del percorso. Ora vedete questo.

![ACOP](./images/journeyactions.png)

Imposta il **Categoria** a **Marketing** e seleziona una superficie e-mail che ti consenta di inviare e-mail. In questo caso, la superficie e-mail da selezionare è **E-mail**. Assicurati che le caselle di controllo per **Clic sull’e-mail** e **aperture e-mail** sono entrambi abilitati.

![ACOP](./images/journeyactions1.png)

Il passaggio successivo consiste nel creare il messaggio. A tale scopo, fai clic su **Modifica contenuto**.

![ACOP](./images/journeyactions2.png)

## 2.3.2 Creare il messaggio

Per creare il messaggio, fai clic su **Modifica contenuto**.

![ACOP](./images/journeyactions2.png)

Ora vedete questo.

![ACOP](./images/journeyactions3.png)

Fai clic su **Oggetto** campo di testo.

![Journey Optimizer](./images/msg5.png)

Nell&#39;area di testo iniziare a scrivere **Ciao**

![Journey Optimizer](./images/msg6.png)

L’oggetto non è ancora stato completato. Ora devi inserire il token di personalizzazione per il campo **Nome** che è memorizzato in `profile.person.name.firstName`. Nel menu a sinistra, scorri verso il basso per trovare il **Persona** e fai clic sulla freccia per andare a un livello più profondo.

![Journey Optimizer](./images/msg7.png)

Ora trova il **Nome e cognome** e fai clic sulla freccia per andare a un livello più profondo.

![Journey Optimizer](./images/msg8.png)

Infine, trova il **Nome** e fai clic sul pulsante **+** accedi accanto. Il token di personalizzazione verrà quindi visualizzato nel campo di testo.

![Journey Optimizer](./images/msg9.png)

Aggiungere quindi il testo **, grazie per esserti registrato!**. Fai clic su **Salva**.

![Journey Optimizer](./images/msg10.png)

Allora tornerai qui. Clic **E-mail Designer** per creare il contenuto dell’e-mail.

![Journey Optimizer](./images/msg11.png)

Nella schermata successiva ti verranno richiesti 3 metodi diversi per fornire il contenuto dell’e-mail:

- **Progettare da zero**: inizia con un’area di lavoro vuota e utilizza l’editor WYSIWYG per trascinare e rilasciare i componenti struttura e contenuto per creare visivamente il contenuto dell’e-mail.
- **Crea il codice**: crea un modello e-mail personalizzato codificandolo con HTML
- **Importa HTML**: importa un modello di HTML esistente che potrai modificare.

Clic **Importa HTML**. In alternativa, è possibile fare clic su **Modelli salvati** e seleziona il modello **Bootcamp - Modello e-mail**.

![Journey Optimizer](./images/msg12.png)

Se hai selezionato **Importa HTML**, è ora possibile trascinare e rilasciare il file **mailtemplatebootcamp.html**, che puoi scaricare [qui](../../assets/html/mailtemplatebootcamp.html.zip). Fai clic su Importa.

![Journey Optimizer](./images/msg13.png)

Visualizzerai quindi questo modello e-mail predefinito:

![Journey Optimizer](./images/msg14.png)

Personalizziamo l’e-mail. Fai clic su accanto al testo **Ciao** e quindi fare clic su **Aggiungi personalizzazione** icona.

![Journey Optimizer](./images/msg35.png)

Quindi, devi portare il **Nome** token di personalizzazione memorizzato in `profile.person.name.firstName`. Nel menu, individua **Persona** , espandere fino a **Nome e cognome** e quindi fare clic sul pulsante **+** per aggiungere il campo First Name all’editor di espressioni.

Fai clic su **Salva**.

![Journey Optimizer](./images/msg36.png)

Ora noterai come il campo di personalizzazione è stato aggiunto al testo.

![Journey Optimizer](./images/msg37.png)

Clic **Salva** per salvare il messaggio.

![Journey Optimizer](./images/msg55.png)

Torna alla dashboard dei messaggi facendo clic sul pulsante **freccia** accanto al testo della riga oggetto nell&#39;angolo superiore sinistro.

![Journey Optimizer](./images/msg56.png)

Hai completato la creazione dell’e-mail di registrazione. Fai clic sulla freccia nell’angolo in alto a sinistra per tornare al percorso.

![Journey Optimizer](./images/msg57.png)

Clic **Ok**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Pubblicare il percorso

È comunque necessario assegnare un nome al percorso. Per farlo, fai clic sul pulsante **Proprietà** in alto a destra.

![ACOP](./images/journeyname.png)

È quindi possibile immettere qui il nome del percorso. Utilizza `yourLastName - Account Creation Journey`. Clic **OK** per salvare le modifiche.

![ACOP](./images/journeyname1.png)

Ora puoi pubblicare il percorso facendo clic su **Pubblica**.

![ACOP](./images/publishjourney.png)

Clic **Pubblica** di nuovo.

![ACOP](./images/publish1.png)

Viene visualizzata una barra di conferma verde che indica che il percorso è ora pubblicato.

![ACOP](./images/published.png)

Hai terminato questo esercizio.

Passaggio successivo: [2.4 Test del percorso](./ex4.md)

[Torna a Flusso utente 2](./uc2.md)

[Torna a tutti i moduli](../../overview.md)