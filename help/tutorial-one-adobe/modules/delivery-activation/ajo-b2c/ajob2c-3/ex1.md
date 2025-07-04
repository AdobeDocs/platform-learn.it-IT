---
title: Guida introduttiva alle notifiche push
description: Guida introduttiva alle notifiche push
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
exl-id: b46e0205-b0a1-4a14-95f6-9afe21cd2b5e
source-git-commit: fb14ba45333bdd5834ff0c6c2dc48dda35cfe85f
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 1%

---

# 3.3.1 Guida introduttiva alle notifiche push

Per utilizzare le notifiche push con Adobe Journey Optimizer, è necessario controllare e conoscere diverse impostazioni.

Di seguito sono elencate tutte le impostazioni da verificare:

- Set di dati e schemi in Adobe Experience Platform
- Stream di dati per dispositivi mobili
- Proprietà raccolta dati per dispositivi mobili
- Superficie app per certificati push
- Testare la configurazione push con AEP Assurance

Esaminiamo questi uno per uno.

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxName--`. Ti troverai quindi nella **Home** della tua sandbox `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.3.1.1 set di dati push

Adobe Journey Optimizer utilizza i set di dati per memorizzare elementi come i token push da dispositivi mobili o interazioni con messaggi push (come: messaggio inviato, messaggio aperto, ecc.) in un set di dati in Adobe Journey Optimizer.

Puoi trovare questi set di dati da **Set di dati** nel menu sul lato sinistro della schermata. Per visualizzare i set di dati di sistema, fai clic sull&#39;icona **Abilita filtri**.

Abilita l&#39;opzione per **System** e cerca **AJO**. Vedrai quindi i set di dati utilizzati per le notifiche push.

![Acquisizione dei dati](./images/menudsjo1.png)

## 3.3.1.2 Datastream per dispositivi mobili

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/).

Nel menu a sinistra, vai a **Datastreams** e cerca lo stream di dati creato in [Guida introduttiva](./../../../../modules/getting-started/gettingstarted/ex2.md), denominato `--aepUserLdap-- - One Adobe Datastream (Mobile)`. Fai clic su per aprirlo.

![Stream di dati](./images/edgeconfig1a.png)

Fai clic su **Modifica** nel servizio **Adobe Experience Platform**.

![Stream di dati](./images/edgeconfig1.png)

Vengono quindi visualizzate le impostazioni dello stream di dati definite e in quali set di dati verranno memorizzati gli eventi e gli attributi del profilo.

Se non sono ancora abilitate, abilita anche le seguenti opzioni:

- **Offer Decisioning**
- **Destinazioni di personalizzazione**
- **Adobe Journey Optimizer**

Fai clic su **Salva**.

![Denomina lo stream di dati e salva](./images/edgeconfig2.png)

## 3.3.1.3 Rivedi la proprietà Data Collection per Mobile

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/), a **Tag**. Come parte del modulo [Guida introduttiva](./../../../../modules/getting-started/gettingstarted/ex1.md), sono state create le proprietà dei tag di raccolta dati.

Queste proprietà dei tag di raccolta dati sono già state utilizzate nei moduli precedenti.

Fai clic su per aprire la proprietà Raccolta dati per dispositivi mobili.

![DSN](./images/launchprop.png)

Nella proprietà Raccolta dati, vai a **Estensioni**. Vedrai quindi le varie estensioni necessarie per l’app mobile. Fare clic per selezionare l&#39;estensione **Adobe Experience Platform Edge Network**, quindi selezionare **Configura**.

![Raccolta dati di Adobe Experience Platform](./images/launchprop1.png)

Vedrai quindi che il flusso di dati per dispositivi mobili è collegato qui. Fare clic su **Annulla** per tornare alla panoramica delle estensioni.

![Raccolta dati di Adobe Experience Platform](./images/launchprop2.png)

Allora tornerai qui. Verrà visualizzata l&#39;estensione per **AEP Assurance**. AEP Assurance consente di verificare, verificare, simulare e convalidare la modalità di raccolta dei dati o di gestione delle esperienze nell’app mobile. Ulteriori informazioni su AEP Assurance sono disponibili qui: [https://experienceleague.adobe.com/it/docs/experience-platform/assurance/home](https://experienceleague.adobe.com/it/docs/experience-platform/assurance/home).

![Raccolta dati di Adobe Experience Platform](./images/launchprop8.png)

Fare clic su **Configura** per aprire l&#39;estensione **Adobe Journey Optimizer**. Questa estensione abilita le notifiche push e la misurazione per Adobe Journey Optimizer.

![Raccolta dati di Adobe Experience Platform](./images/launchprop9.png)

Qui è collegato il set di dati per il tracciamento degli eventi push. Non è necessario apportare modifiche alla proprietà Data Collection. Fai clic su **Annulla** per tornare alla schermata precedente.

![Raccolta dati di Adobe Experience Platform](./images/launchprop10.png)

## 3.3.1.4 Verifica la configurazione della superficie dell&#39;app

Vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/). Nel menu a sinistra, vai a **Superfici app** e apri la Superficie app per **APNS app demo**.

![Raccolta dati di Adobe Experience Platform](./images/appsf.png)

Viene quindi visualizzata la superficie configurata dell’app per iOS e Android.

![Raccolta dati di Adobe Experience Platform](./images/appsf1.png)

## 3.3.1.5 Verifica la configurazione della notifica push tramite AEP Assurance.

Hai già installato l&#39;app mobile **DX Demo** come parte del modulo **Guida introduttiva**. Una volta installata l’app, questa si trova nella schermata iniziale del dispositivo. Fai clic sull&#39;icona per aprire l&#39;app.

![DSN](./../../../../modules/getting-started/gettingstarted/images/mobileappn1.png)

Dopo aver effettuato l’accesso, verrà visualizzata una notifica con la richiesta dell’autorizzazione per l’invio di notifiche. Invieremo notifiche come parte dell&#39;esercitazione, quindi fai clic su **Consenti**.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn2.png)

Viene quindi visualizzata la home page dell’app. Vai a **Impostazioni**.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn3.png)

Nelle impostazioni, vedrai che attualmente un **progetto pubblico** è caricato nell&#39;app. Fai clic su **Progetto personalizzato**.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn4.png)

Ora puoi caricare un progetto personalizzato. Fai clic sul codice QR per caricare facilmente il progetto.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn5.png)

Dopo aver esaminato la sezione **Guida introduttiva**, si è verificato questo risultato. Fai clic per aprire il **progetto Mobile Retail** creato per te.

![DSN](./../../../modules/../getting-started/gettingstarted/images/dsn5b.png)

Nel caso in cui tu abbia chiuso accidentalmente la finestra del browser o per sessioni di attivazione o demo future, puoi anche accedere al progetto del tuo sito web da [https://dsn.adobe.com/projects](https://dsn.adobe.com/projects). Dopo aver effettuato l’accesso con il tuo Adobe ID, visualizzerai questo. Fai clic sul progetto dell’app mobile per aprirlo.

![DSN](./../../../modules/../getting-started/gettingstarted/images/web8a.png)

Fare clic su **Esegui**.

![DSN](./images/web8b.png)

Viene quindi visualizzata questa finestra a comparsa contenente un codice QR. Esegui la scansione di questo codice QR dall’app mobile.

![DSN](./../../../modules/../getting-started/gettingstarted/images/web8c.png)

Nell&#39;app verrà quindi visualizzato l&#39;ID progetto, dopodiché potrai fare clic su **Switch**.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn7.png)

L&#39;app è ora pronta per essere utilizzata.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn8.png)

Ora devi scansionare un codice QR per collegare il dispositivo mobile alla sessione Assurance.

Per avviare una sessione di AEP Assurance, vai a [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/it#/data-collection/). Fai clic su **Assurance** nel menu a sinistra. Quindi fare clic su **Crea sessione**.

![Raccolta dati di Adobe Experience Platform](./images/griffon3.png)

Seleziona **Connessione collegamento profondo**, quindi fai clic su **Avvia**.

![Raccolta dati di Adobe Experience Platform](./images/griffon5.png)

Compila i valori:

- Nome sessione: `--aepUserLdap-- - Push Debugging`
- URL di base: `dxdemo://default`

Fai clic su **Avanti**.

![Raccolta dati di Adobe Experience Platform](./images/griffon4.png)

Visualizzerai quindi un codice QR sullo schermo, che dovresti scansionare con il dispositivo iOS.

![Raccolta dati di Adobe Experience Platform](./images/griffon6.png)

Sul dispositivo mobile, apri l’app della fotocamera e scansiona il codice QR visualizzato da Assurance.

![Raccolta dati di Adobe Experience Platform](./images/ipadPushTest8a.png)

Viene quindi visualizzata una finestra a comparsa in cui viene richiesto di immettere il codice PIN. Copia il codice PIN dalla schermata Assurance di AEP e fai clic su **Connetti**.

![Raccolta dati di Adobe Experience Platform](./images/ipadPushTest9.png)

Poi vedrai questo.

![Raccolta dati di Adobe Experience Platform](./images/ipadPushTest11.png)

In Assurance, ora vedrai che un dispositivo client è connesso alla sessione di Assurance. Fare clic su **Configura**.

![Raccolta dati di Adobe Experience Platform](./images/griffon7.png)

Scorri verso il basso fino a **Debug push**. Fai clic sull&#39;icona **+** e quindi su **Salva**.

![Raccolta dati di Adobe Experience Platform](./images/griffon7a.png)

Vai a **Debug push**. Dovresti vedere questo.

![Raccolta dati di Adobe Experience Platform](./images/griffon10.png)

Alcune spiegazioni:

- La prima colonna, **Client**, mostra gli identificatori disponibili sul dispositivo iOS. Vedrai un ECID e un Token push.
- La seconda colonna mostra le **credenziali e configurazione di App Store**
- La seconda colonna mostra le informazioni del **profilo**, con informazioni aggiuntive sulla piattaforma in cui si trova il token push (APNS o APNSSandbox). Se fai clic sul pulsante **Ispeziona profilo**, verrai indirizzato a Adobe Experience Platform e visualizzerai l&#39;intero profilo cliente in tempo reale.

Per verificare la configurazione push, vai al pulsante **Invia configurazione push di prova**. Fai clic su **Invia notifica push di prova**

![Raccolta dati di Adobe Experience Platform](./images/griffon11.png)

Assicurati che l&#39;app **DX Demo** non sia aperta al momento di fare clic sul pulsante **Invia notifica push**. Se l’app è aperta, la notifica push potrebbe essere ricevuta in background e non sarebbe visibile.

Vedrai quindi una notifica push come questa visualizzata sul tuo dispositivo mobile.

![Raccolta dati di Adobe Experience Platform](./images/ipadPush2.png)

Se hai ricevuto la notifica push, significa che la configurazione è corretta e funziona correttamente e ora puoi creare un percorso reale che si tradurrà nell’invio di un messaggio push da Journey Optimizer.

## Passaggi successivi

Vai a [3.3.2 Configurare un percorso con messaggi push](./ex2.md){target="_blank"}

Torna a [Adobe Journey Optimizer: messaggi push e in-app](ajopushinapp.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
