---
title: Bootcamp - Blending physical and digital - Journey Optimizer Crea il tuo percorso e notifica push
description: Bootcamp - Blending physical and digital - Journey Optimizer Crea il tuo percorso e notifica push
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: be8c23ec-c5f8-4abc-849f-994446072a84
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# 3.3 Creare il percorso e la notifica push

In questo esercizio configurerai il percorso e il messaggio da attivare quando qualcuno entra in un beacon utilizzando l&#39;app mobile.

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `Bootcamp`. Per passare da una sandbox all&#39;altra, fare clic su **Prod** e selezionare la sandbox dall&#39;elenco. In questo esempio, la sandbox è denominata **Bootcamp**. Ti troverai quindi nella **Home** della tua sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Creare il percorso

Nel menu a sinistra, fai clic su **Percorsi**. Fare clic su **Crea Percorso** per creare un nuovo percorso.

![ACOP](./images/createjourney.png)

Viene quindi visualizzata una schermata di percorso vuota.

![ACOP](./images/journeyempty.png)

Nell&#39;esercizio precedente è stato creato un nuovo **evento**. L&#39;utente ha assegnato un nome simile a `yourLastNameBeaconEntryEvent` e ha sostituito `yourLastName` con il cognome. Questo è stato il risultato della creazione dell’evento:

![ACOP](./images/eventdone.png)

Ora devi prendere questo evento come inizio di questo Percorso. Per farlo, vai sul lato sinistro della schermata e cerca l’evento nell’elenco degli eventi.

![ACOP](./images/eventlist.png)

Seleziona l’evento, trascinalo sull’area di lavoro del percorso. Il tuo percorso ora si presenta così. Fai clic su **Ok** per salvare le modifiche.

![ACOP](./images/journeyevent.png)

Come secondo passaggio del percorso, devi aggiungere un&#39;azione **Push**. Vai sul lato sinistro della schermata a **Azioni**, seleziona l&#39;azione **Invia**, quindi trascinala sul secondo nodo del percorso.

![ACOP](./images/journeyactions.png)

Sul lato destro dello schermo, ora è necessario creare la notifica push.

Imposta **Categoria** su **Marketing** e seleziona una superficie push che ti consenta di inviare notifiche push. In questo caso, la superficie push da selezionare è **mmeeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Creare il messaggio

Fare clic su **Modifica contenuto**.

![ACOP](./images/emptymsg.png)

A questo punto viene visualizzato quanto segue:

![ACOP](./images/emailmsglist.png)

Definiamo il contenuto della notifica push.

Fai clic sul campo di testo **Titolo**.

![Journey Optimizer](./images/msg5.png)

Nell&#39;area di testo inizia a scrivere **Ciao**. Fai clic sull’icona di personalizzazione.

![Journey Optimizer](./images/msg6.png)

È ora necessario inserire il token di personalizzazione per il campo **First name** memorizzato in `profile.person.name.firstName`. Nel menu a sinistra, seleziona **Attributi profilo**, scorri verso il basso/sfoglia per trovare l&#39;elemento **Persona** e fai clic sulla freccia per andare più a fondo fino a raggiungere il campo `profile.person.name.firstName`. Fai clic sull&#39;icona **+** per aggiungere il campo all&#39;area di lavoro. Fai clic su **Salva**.

![Journey Optimizer](./images/msg7.png)

Allora tornerai qui. Fai clic sull&#39;icona di personalizzazione accanto al campo **Corpo**.

![Journey Optimizer](./images/msg11.png)

Nell&#39;area di testo, scrivere `Welcome at the `.

![Journey Optimizer](./images/msg12.png)

Fare clic su **Attributi contestuali** e quindi su **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Fai clic su **Eventi**.

![ACOP](./images/jomsg4.png)

Fai clic sul nome dell&#39;evento, che avrà un aspetto simile al seguente: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Fare clic su **Inserisci contesto**.

![ACOP](./images/jomsg6.png)

Fai clic su **Interazione POI**.

![ACOP](./images/jomsg7.png)

Fai clic su **Dettagli POI**.

![ACOP](./images/jomsg8.png)

Fai clic sull&#39;icona **+** in **Nome POI**.
Poi vedrai questo. Fai clic su **Salva**.

![ACOP](./images/jomsg9.png)

Il messaggio è ora pronto. Fai clic sulla freccia nell’angolo in alto a sinistra per tornare al percorso.

![ACOP](./images/jomsg11.png)

Fare clic su **Ok**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Inviare un messaggio a uno schermo

Come terzo passaggio del percorso, devi aggiungere un&#39;azione **sendMessageToScreen**. Vai sul lato sinistro della schermata a **Azioni**, seleziona l&#39;azione **inviaMessaggioAlloSchermo**, quindi trascinala e rilasciala sul terzo nodo del percorso. Poi vedrai questo.

![ACOP](./images/jomsg15.png)

L&#39;azione **sendMessageToScreen** è un&#39;azione personalizzata che pubblicherà un messaggio sull&#39;endpoint utilizzato dalla visualizzazione in-store. L&#39;azione **sendMessageToScreen** prevede la definizione di una serie di variabili. Puoi visualizzare queste variabili scorrendo verso il basso fino a visualizzare **Parametri azione**.

![ACOP](./images/jomsg16.png)

Ora devi impostare i valori per ogni parametro di azione. Segui questa tabella per capire quali valori sono richiesti e dove.

| Parametro | valore |
|:-------------:| :---------------:|
| CONSEGNA | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| NOME | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| SANDBOX | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style="table-layout:auto"}

Per impostare tali valori, fare clic sull&#39;icona **Modifica**.

![ACOP](./images/jomsg17.png)

Selezionare **Modalità avanzata**.

![ACOP](./images/jomsg18.png)

Quindi, incolla il valore in base alla tabella precedente. Fare clic su **Ok**.

![ACOP](./images/jomsg19.png)

Ripetere questo processo per aggiungere valori per ogni campo.

>[!IMPORTANT]
>
>Per il campo ECID, esiste un riferimento all&#39;evento `yourLastNameBeaconEntryEvent`. Sostituire `yourLastName` con il cognome.

Il risultato finale dovrebbe essere simile al seguente:

![ACOP](./images/jomsg20.png)

Scorri verso l&#39;alto e fai clic su **Ok**.

![ACOP](./images/jomsg21.png)

È comunque necessario assegnare un nome al percorso. Per farlo, fai clic sull&#39;icona **Matita** in alto a sinistra nella schermata.

![ACOP](./images/journeyname.png)

È quindi possibile immettere qui il nome del percorso. Utilizzare `yourLastName - Beacon Entry Journey`. Fai clic su **OK** per salvare le modifiche.

![ACOP](./images/journeyname1.png)

È ora possibile pubblicare il percorso facendo clic su **Publish**.

![ACOP](./images/publishjourney.png)

Fai di nuovo clic su **Publish**.

![ACOP](./images/publish1.png)

Viene visualizzata una barra di conferma verde che indica che il percorso è ora pubblicato.

![ACOP](./images/published.png)

Il percorso è ora attivo e può essere attivato.

Hai terminato questo esercizio.

Passaggio successivo: [3.4 Verifica il percorso](./ex4.md)

[Torna a Flusso utente 3](./uc3.md)

[Torna a tutti i moduli](../../overview.md)
