---
title: Bootcamp - Fusione fisica e digitale - Journey Optimizer Crea il tuo percorso e notifica push
description: Bootcamp - Fusione fisica e digitale - Journey Optimizer Crea il tuo percorso e notifica push
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: be8c23ec-c5f8-4abc-849f-994446072a84
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 2%

---

# 3.3 Creare il percorso e la notifica push

In questo esercizio configurerai il percorso e il messaggio da attivare quando un utente accede a un beacon utilizzando l’app mobile.

Accedi a Adobe Journey Optimizer accedendo a [Adobe Experience Cloud](https://experience.adobe.com). Fai clic su **Journey Optimizer**.

![ACOP](./images/acophome.png)

Verrai reindirizzato al **Pagina principale**  in Journey Optimizer. In primo luogo, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare è denominata `Bootcamp`. Per passare da una sandbox all’altra, fai clic su **Prod** e selezionate la sandbox dall’elenco. In questo esempio, la sandbox è denominata **Bootcamp**. Allora sarai nel **Pagina principale** visualizzazione della sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Crea il tuo percorso

Nel menu a sinistra, fai clic su **Percorsi**. Quindi, fai clic su **Crea Percorso** per creare un nuovo percorso.

![ACOP](./images/createjourney.png)

Verrà visualizzata una schermata di percorso vuota.

![ACOP](./images/journeyempty.png)

Nell’esercizio precedente, hai creato una nuova **Evento**. L&#39;hai chiamato così `yourLastNameBeaconEntryEvent` e sostituito `yourLastName` con il tuo cognome. Questo è stato il risultato della creazione dell’evento:

![ACOP](./images/eventdone.png)

Ora devi prendere questo evento come inizio di questo Percorso. Per farlo, vai sul lato sinistro dello schermo e cerca l’evento nell’elenco degli eventi.

![ACOP](./images/eventlist.png)

Seleziona l’evento, trascinalo sull’area di lavoro del percorso e rilascialo. Il tuo percorso ora assomiglia a questo. Fai clic su **Ok** per salvare le modifiche.

![ACOP](./images/journeyevent.png)

Come secondo passaggio del percorso, devi aggiungere un **Push** azione. Vai al lato sinistro dello schermo fino a **Azioni**, seleziona **Push** , quindi trascinalo sul secondo nodo del percorso.

![ACOP](./images/journeyactions.png)

Sul lato destro dello schermo è ora necessario creare la notifica push.

Imposta la **Categoria** a **Marketing** e seleziona una superficie push che ti consenta di inviare notifiche push. In questo caso, la superficie di spinta da selezionare è **mmeeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Creare il messaggio

Fai clic su **Modifica contenuto**.

![ACOP](./images/emptymsg.png)

Vedrai questo:

![ACOP](./images/emailmsglist.png)

Definiamo il contenuto della notifica push.

Fai clic sul pulsante **Titolo** campo di testo.

![Journey Optimizer](./images/msg5.png)

Nell’area di testo inizia la scrittura **Ciao**. Fai clic sull’icona della personalizzazione.

![Journey Optimizer](./images/msg6.png)

Ora devi inserire il token di personalizzazione per il campo **Nome** che è immagazzinato in `profile.person.name.firstName`. Nel menu a sinistra, seleziona **Attributi del profilo**, scorri verso il basso/naviga per trovare il **Persona** e fai clic sulla freccia per andare un livello più profondo fino a raggiungere il campo `profile.person.name.firstName`. Fai clic sul pulsante **+** per aggiungere il campo all’area di lavoro. Fai clic su **Salva**.

![Journey Optimizer](./images/msg7.png)

Allora tornerai qui. Fai clic sull’icona di personalizzazione accanto al campo **Corpo**.

![Journey Optimizer](./images/msg11.png)

Nell’area di testo, scrivere `Welcome at the `.

![Journey Optimizer](./images/msg12.png)

Quindi, fai clic su **Attributi contestuali** e poi **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Fai clic su **Eventi**.

![ACOP](./images/jomsg4.png)

Fai clic sul nome dell’evento, che avrà un aspetto simile al seguente: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Fai clic su **Posizionare il contesto**.

![ACOP](./images/jomsg6.png)

Fai clic su **Interazione POI**.

![ACOP](./images/jomsg7.png)

Fai clic su **Dettagli POI**.

![ACOP](./images/jomsg8.png)

Fai clic sul pulsante **+** icona su **Nome POI**.
Vedrete questo. Fai clic su **Salva**.

![ACOP](./images/jomsg9.png)

Il tuo messaggio è ora pronto. Fai clic sulla freccia nell&#39;angolo in alto a sinistra per tornare al percorso.

![ACOP](./images/jomsg11.png)

Fai clic su **Ok**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Inviare un messaggio a una schermata

Come terzo passaggio del percorso, devi aggiungere un **sendMessageToScreen** azione. Vai al lato sinistro dello schermo fino a **Azioni**, seleziona **sendMessageToScreen** , quindi trascinalo sul terzo nodo del percorso. Vedrete questo.

![ACOP](./images/jomsg15.png)

La **sendMessageToScreen** action è un’azione personalizzata che pubblicherà un messaggio sull’endpoint utilizzato dalla visualizzazione in-store. La **sendMessageToScreen** per action è necessario definire una serie di variabili. Puoi vedere queste variabili scorrendo verso il basso fino a quando non vedi **Parametri azione**.

![ACOP](./images/jomsg16.png)

Ora devi impostare i valori per ogni parametro di azione. Seguire questa tabella per comprendere i valori richiesti.

| Parametro | Valore  |
|:-------------:| :---------------:|
| CONSEGNA | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| NOME | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| SANDBOX | `'bootcamp'` |
| CONTAINERIA | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style=&quot;table-layout:auto&quot;}

Per impostare tali valori, fai clic sul pulsante **Modifica** icona.

![ACOP](./images/jomsg17.png)

Quindi, seleziona **Modalità avanzata**.

![ACOP](./images/jomsg18.png)

Quindi, incolla il valore in base alla tabella precedente. Fai clic su **Ok**.

![ACOP](./images/jomsg19.png)

Ripetere questo processo per aggiungere valori per ciascun campo.

>[!IMPORTANT]
>
>Per il campo ECID, c&#39;è un riferimento all&#39;evento `yourLastNameBeaconEntryEvent`. Assicurati di sostituire `yourLastName` con il tuo cognome.

Il risultato finale dovrebbe essere simile al seguente:

![ACOP](./images/jomsg20.png)

Scorri verso l’alto e fai clic su **Ok**.

![ACOP](./images/jomsg21.png)

Devi ancora dare un Nome al tuo percorso. Per farlo, fai clic sul pulsante **Proprietà** in alto a destra sullo schermo.

![ACOP](./images/journeyname.png)

Potete quindi inserire il nome del percorso qui. Utilizzare `yourLastName - Beacon Entry Journey`. Fai clic su **OK** per salvare le modifiche.

![ACOP](./images/journeyname1.png)

Ora puoi pubblicare il percorso facendo clic su **Pubblica**.

![ACOP](./images/publishjourney.png)

Fai clic su **Pubblica** di nuovo.

![ACOP](./images/publish1.png)

Verrà visualizzata una barra di conferma verde che indica che il percorso è ora Pubblicato.

![ACOP](./images/published.png)

Il percorso è ora attivo e può essere attivato.

Ora avete finito questo esercizio.

Passaggio successivo: [3.4 Testare il percorso](./ex4.md)

[Torna al flusso utente 3](./uc3.md)

[Torna a tutti i moduli](../../overview.md)
