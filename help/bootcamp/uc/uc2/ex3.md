---
title: Bootcamp - Journey Optimizer Crea il tuo percorso e messaggio e-mail
description: Bootcamp - Journey Optimizer Crea il tuo percorso e messaggio e-mail
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 138a70fa-fe50-4585-b47f-150db4770c3d
source-git-commit: f018e3aae714879de0cccb3a47b1f2242b57abc1
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 4%

---

# 2.3 Creare il percorso e il messaggio e-mail

In questo esercizio, configurerai il percorso da attivare quando qualcuno crea un account sul sito web demo.

Accedi a Adobe Journey Optimizer accedendo a [Adobe Experience Cloud](https://experience.adobe.com). Fai clic su **Journey Optimizer**.

![ACOP](./images/acophome.png)

Verrai reindirizzato al **Pagina principale**  in Journey Optimizer. In primo luogo, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare è denominata `Bootcamp`. Per passare da una sandbox all’altra, fai clic su **Prod** e selezionate la sandbox dall’elenco. In questo esempio, la sandbox è denominata **Bootcamp**. Allora sarai nel **Pagina principale** visualizzazione della sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 2.3.1 Crea il tuo percorso

Nel menu a sinistra, fai clic su **Percorsi**. Quindi, fai clic su **Crea Percorso** per creare un nuovo percorso.

![ACOP](./images/createjourney.png)

Verrà visualizzata una schermata di percorso vuota.

![ACOP](./images/journeyempty.png)

Nell’esercizio precedente, hai creato una nuova **Evento**. L&#39;hai chiamato così `yourLastNameAccountCreationEvent` e sostituito `yourLastName` con il tuo cognome. Questo è stato il risultato della creazione dell’evento:

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

## 2.3.2 Creare il messaggio

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

Fai clic su **Importa HTML**. In alternativa, puoi fare clic su **Modelli salvati** e seleziona il modello **Bootcamp - Modello e-mail**.

![Journey Optimizer](./images/msg12.png)

Se hai selezionato **Importa HTML**, ora puoi trascinare e rilasciare il file **mailtemplatebootcamp.html**, scaricabile [qui](../../assets/html/mailtemplatebootcamp.html.zip). Fai clic su Importa.

![Journey Optimizer](./images/msg13.png)

Verrà quindi visualizzato questo modello e-mail predefinito:

![Journey Optimizer](./images/msg14.png)

Personalizziamo l’e-mail. Fai clic accanto al testo **Ciao** quindi fai clic sul pulsante **Aggiungi personalizzazione** icona.

![Journey Optimizer](./images/msg35.png)

Successivamente, devi portare il **Nome** token di personalizzazione memorizzato in `profile.person.name.firstName`. Nel menu , trova la **Persona** elemento, scegli **Nome completo** , quindi fai clic sul **+** per aggiungere il campo Nome all’editor di espressioni.

Fai clic su **Salva**.

![Journey Optimizer](./images/msg36.png)

Ora noterai come il campo di personalizzazione è stato aggiunto al testo.

![Journey Optimizer](./images/msg37.png)

Fai clic su **Salva** per salvare il messaggio.

![Journey Optimizer](./images/msg55.png)

Torna al dashboard dei messaggi facendo clic sul pulsante **freccia** accanto all’oggetto nell’angolo in alto a sinistra.

![Journey Optimizer](./images/msg56.png)

Hai completato la creazione del messaggio e-mail di registrazione. Fai clic sulla freccia nell&#39;angolo in alto a sinistra per tornare al percorso.

![Journey Optimizer](./images/msg57.png)

Fai clic su **Ok**.

![Journey Optimizer](./images/msg57a.png)

## 2.3.3 Pubblicare il percorso

Devi ancora dare un Nome al tuo percorso. Per farlo, fai clic sul pulsante **Proprietà** in alto a destra sullo schermo.

![ACOP](./images/journeyname.png)

Potete quindi inserire il nome del percorso qui. Utilizzare `yourLastName - Account Creation Journey`. Fai clic su **OK** per salvare le modifiche.

![ACOP](./images/journeyname1.png)

Ora puoi pubblicare il percorso facendo clic su **Pubblica**.

![ACOP](./images/publishjourney.png)

Fai clic su **Pubblica** di nuovo.

![ACOP](./images/publish1.png)

Verrà visualizzata una barra di conferma verde che indica che il percorso è ora Pubblicato.

![ACOP](./images/published.png)

Ora avete finito questo esercizio.

Passaggio successivo: [2.4 Test del percorso](./ex4.md)

[Torna al flusso utente 2](./uc2.md)

[Torna a tutti i moduli](../../overview.md)