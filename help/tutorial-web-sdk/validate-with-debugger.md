---
title: Convalidare le implementazioni Web SDK con Experienci Platform Debugger
description: Scopri come convalidare l’implementazione di Platform Web SDK con l’Adobe Experience Platform Debugger. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK,Tags,Debugger
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: aeff30f808fd65370b58eba69d24e658474a92d7
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 1%

---

# Convalidare le implementazioni Web SDK con Experienci Platform Debugger

Scopri come convalidare l’implementazione di Platform Web SDK con l’Adobe Experience Platform Debugger.

Experienci Platform Debugger è un’estensione disponibile per i browser Chrome e Firefox che consente di visualizzare la tecnologia Adobe implementata nelle pagine web. Scarica la versione per il browser preferito:

* [Estensione Firefox](https://addons.mozilla.org/it/firefox/addon/adobe-experience-platform-dbg/)
* [Estensione Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Se non hai mai utilizzato il debugger prima, e questo è diverso dal precedente Adobe Experience Cloud Debugger, guarda questo video introduttivo di cinque minuti:

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on)

In questa lezione, utilizzerai [Estensione Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) per sostituire la proprietà di tag in codifica fissa [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html) con la tua proprietà.

Questa tecnica è denominata cambio di ambiente e sarà utile in un secondo momento, quando lavorerai con i tag sul tuo sito web. Puoi caricare il tuo sito web di produzione nel browser, ma con *sviluppo* nell’ambiente dei tag. Questa funzionalità ti consente di creare e convalidare le modifiche ai tag in modo indipendente dalle regolari versioni del codice. Dopo tutto, questa separazione tra versioni di tag di marketing e versioni di codice è uno dei motivi principali per cui i clienti utilizzano i tag.

## Obiettivi di apprendimento

Alla fine di questa lezione, potrai utilizzare il debugger per:

* Caricare una libreria di tag alternativa
* Verifica che l’evento XDM lato client acquisisca e invii i dati come previsto all’Edge Network di Platform
* Abilita Edge Trace per visualizzare le richieste lato server inviate dall’Edge Network di Platform

## Prerequisiti

Conosci i tag di raccolta dati e la [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} e hanno completato le lezioni precedenti nell’esercitazione:

* [Configurare uno schema XDM](configure-schemas.md)
* [Configurare uno spazio dei nomi delle identità](configure-identities.md)
* [Configurare uno stream di dati](configure-datastream.md)
* [Estensione Web SDK installata nella proprietà tag](install-web-sdk.md)
* [Creare elementi dati](create-data-elements.md)
* [Creare identità](create-identities.md)
* [Creare regole di tag](create-tag-rule.md)

## Caricare librerie di tag alternative con Debugger

Experienci Platform Debugger dispone di una funzione interessante che consente di sostituire una libreria di tag esistente con una diversa. Questa tecnica è utile per la convalida e ci consente di saltare molti passaggi di implementazione in questa esercitazione.

1. Assicurati di avere [Sito web di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} apri e seleziona l’icona dell’estensione Experienci Platform Debugger
1. Verrà aperto Debugger e verranno visualizzati alcuni dettagli dell’implementazione hardcoded (potrebbe essere necessario ricaricare il sito Luma dopo aver aperto Debugger)
1. Conferma che il debugger è &quot;**[!UICONTROL Connesso a Luma]**&quot; come illustrato di seguito, quindi selezionare la&quot;**[!UICONTROL blocca]**&quot; per bloccare Debugger sul sito Luma.
1. Seleziona la **[!UICONTROL Accedi]** e accedi a Adobe Experience Cloud utilizzando il tuo ID Adobe.
1. Ora vai a **[!UICONTROL Tag Experience Platform]** nel menu di navigazione a sinistra

   ![Schermata tag del debugger](assets/validate-launch-screen.png)

1. Seleziona la **[!UICONTROL Configurazione]** scheda
1. A destra della posizione in cui è visualizzato **[!UICONTROL Codici di incorporamento pagina]**, apri **[!UICONTROL Azioni]** e seleziona **[!UICONTROL Sostituisci]**

   ![Seleziona Azioni > Sostituisci](assets/validate-switch-environment.png)

1. Poiché sei autenticato, il Debugger estrae le proprietà e gli ambienti dei tag disponibili. Seleziona la proprietà; in questo caso `Web SDK Course 3`
1. Seleziona il `Development` ambiente
1. Seleziona la **[!UICONTROL Applica]** pulsante

   ![Seleziona la proprietà tag alternativa](assets/validate-switch-selection.png)

1. Il sito web Luma verrà ricaricato _con la tua proprietà tag_.

   ![proprietà tag sostituita](assets/validate-switch-success.png)

Continuando l’esercitazione, utilizzi questa tecnica per mappare il sito Luma sulla tua proprietà tag per convalidare l’implementazione dell’SDK web per Platform. Quando inizi a utilizzare i tag sul sito web di produzione, puoi usare questa stessa tecnica per convalidare le modifiche apportate nell’ambiente di sviluppo dei tag.

## Convalidare richieste di rete lato client con Experienci Platform Debugger

Puoi utilizzare il debugger per convalidare i beacon lato client attivati dall’implementazione di Platform Web SDK per visualizzare i dati inviati a Platform, ad Edge Network:

1. Vai a **[!UICONTROL Riepilogo]** nel menu di navigazione a sinistra, per visualizzare i dettagli della proprietà tag

   ![Scheda Riepilogo](assets/validate-summary.png)

1. Ora vai a **[!UICONTROL Experienci Platform Web SDK]** nel menu di navigazione a sinistra per visualizzare **[!UICONTROL Richieste di rete]**
1. Apri **[!UICONTROL Eventi]** riga

   ![richiesta Adobe Experience Platform Web SDK](assets/validate-aep-screen.png)

1. Nota come è possibile visualizzare `web.webpagedetails.pageView` tipo di evento specificato nel [!UICONTROL Aggiorna variabile] e altre variabili pronte all’uso conformi alla `AEP Web SDK ExperienceEvent` gruppo di campi

   ![Dettagli evento](assets/validate-event-pageViews.png)

1. Scorri verso il basso fino a `web` dell&#39;oggetto, selezionare per aprirlo ed esaminare `webPageDetails.name`, `webPageDetails.server`, e `webPageDetails.siteSection`. Devono corrispondere al corrispondente `digitalData` variabili del livello dati nella home page

>[!TIP]
>
> Per visualizzare e confrontare `digitalData` livello dati nella home page:
>
> 1. Nella home page di Luma, apri gli strumenti di sviluppo del browser. Nel caso di Chrome, seleziona il pulsante `F12` sulla tastiera
> 1. Seleziona la **[!UICONTROL Console]** scheda
> 1. Invio `digitalData` e seleziona `Enter` sulla tastiera per visualizzare i valori del livello dati

![Scheda Rete](assets/validate-xdm-content.png)

Puoi anche convalidare i dettagli di Identity Map:

1. Accedi al sito Luma utilizzando le credenziali `test@adobe.com`/`test`

1. Torna alla [home page di Luma](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Apri **[!UICONTROL Experienci Platform Web SDK]** sezione nel menu di navigazione a sinistra

   ![SDK per web nel debugger](assets/identity-debugger-websdk-dark.png)

1. Seleziona la **[!UICONTROL Eventi]** riga per aprire i dettagli in un pop-up

   ![SDK per web nel debugger](assets/identity-deugger-websdk-event-dark.png)

1. Cerca **identityMap** all&#39;interno del pop-up. Qui dovresti vedere `lumaCrmId` con tre chiavi di authenticatedState, id e primary:
   ![SDK per web nel debugger](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)

### Convalidare le richieste lato client con gli strumenti di sviluppo del browser

Questi tipi di dettagli della richiesta sono visibili anche negli strumenti di sviluppo web del browser **Rete** (supponendo che il sito web stia caricando la libreria di tag).

1. Apri gli strumenti di sviluppo web del browser **Rete** e ricarica la pagina. Filtra per chiamate con `/ee` per individuare la chiamata, selezionarla e quindi cercare nella **Intestazioni** e **Payload** scheda

   ![Scheda Rete](assets/validate-dev-console.png)

1. Vai a **Risposta** e osserva come il valore ECID viene incluso nella risposta. Copia questo valore così come lo utilizzerai per convalidare le informazioni sul profilo nel prossimo esercizio

   ![Scheda Rete](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   > Il valore ECID è visibile nella risposta di rete. Non è incluso nel `identityMap` parte della richiesta di rete, né viene memorizzata in questo formato in un cookie.

## Convalidare le richieste di rete lato server con Experienci Platform Debugger

Come hai imparato nella [Configurare uno stream di dati](configure-datastream.md) lezione, Platform Web SDK invia prima i dati dalla proprietà digitale all’Edge Network di Platform. Quindi, l’Edge Network di Platform effettua richieste aggiuntive lato server ai servizi corrispondenti abilitati nello stream di dati. Puoi convalidare le richieste lato server effettuate dall’Edge Network di Platform utilizzando Edge Trace nel Debugger.

<!--Furthermore, you can also validate the fully processed payload after it reaches an Adobe application by using [Adobe Experience Platform Assurance](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home). -->


### Abilita traccia perimetrale

Per abilitare Edge Trace:

1. Nella barra di navigazione a sinistra di **[!UICONTROL Debugger Experienci Platform]** seleziona **[!UICONTROL Registri]**
1. Seleziona la **[!UICONTROL Bordo]** e seleziona **[!UICONTROL Connetti]**

   ![Connetti traccia spigolo](assets/analytics-debugger-edgeTrace.png)

1. Per il momento è vuoto

   ![Traccia bordi connessi](assets/analytics-debugger-edge-connected.png)

1. Aggiorna il [Home page Luma](https://luma.enablementadobe.com/) e verifica **[!UICONTROL Debugger Experienci Platform]** di nuovo, per vedere i dati arrivare attraverso.

   ![Traccia Edge beacon di Analytics](assets/validate-edge-trace.png)

A questo punto, non è possibile visualizzare le richieste di Edge Network di Platform indirizzate ad applicazioni di Adobe, perché non ne hai abilitate nessuna nello stream di dati. Nelle lezioni future, utilizzi Edge Trace per visualizzare le richieste lato server in uscita alle applicazioni Adobe e all’inoltro di eventi. Ma prima di tutto, scopri un altro strumento per convalidare le richieste lato server effettuate da Edge Network di Platform: Adobe Experience Platform Assurance.

[Successivo: ](validate-with-assurance.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
