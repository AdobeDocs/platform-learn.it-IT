---
title: Eseguire test A/B con Target
description: Scopri come utilizzare un test A/B di Target nell’app mobile con Platform Mobile SDK e Adobe Target.
solution: Data Collection,Target
feature-set: Target
feature: A/B Tests
hide: true
source-git-commit: 35b38e7491a3751d21afe4a7b998e5dc2292ba27
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 2%

---


# Eseguire test A/B con Target

Scopri come eseguire test A/B nelle app mobili con Platform Mobile SDK e Adobe Target.

Target offre tutto ciò che è necessario adattare e personalizzare le esperienze dei clienti. Target consente di massimizzare i ricavi sui siti web e mobili, applicazioni, social media e altri canali digitali. Questa esercitazione si concentra sulla funzionalità di test A/B di Target. Consulta la [Panoramica sui test A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=en) per ulteriori informazioni.

Prima di poter eseguire test A/B con Target Premium, è necessario assicurarsi che siano presenti le configurazioni e le integrazioni corrette.

>[!NOTE]
>
>Questa lezione è facoltativa e si applica solo agli utenti Adobe Target Premium che desiderano eseguire test A/B.


## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente.
* Accedi ad Adobe Target Premium con le autorizzazioni, i ruoli configurati correttamente, le aree di lavoro e le proprietà come descritto [qui](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=it).
Dovresti essere in grado di utilizzare anche Target Standard, ma il tutorial utilizza alcuni concetti avanzati (ad esempio le proprietà di Target) che sono univoci per Target Premium.


## Finalità di apprendimento

In questa lezione, potrai

* Aggiorna la configurazione Edge per l’integrazione di Target.
* Aggiorna la proprietà tag con l’estensione Journey Optimizer - Decisioning.
* Aggiorna lo schema per acquisire gli eventi della proposta.
* Convalidare l&#39;impostazione in Assurance.
* Crea un semplice test A/B in Target.
* Aggiorna l&#39;app per includere l&#39;estensione Optimize.
* Implementa il test A/B nell’app.
* Convalidare l’implementazione in Assurance.


## Aggiorna configurazione Edge

Per fare in modo che i dati inviati dalla tua app mobile a Edge Network vengano inoltrati ad Adobe Target, devi aggiornare la configurazione di Experience Edge.

1. Nell’interfaccia utente di Data Collection, seleziona **[!UICONTROL Flussi di dati]** e seleziona il flusso di dati, ad esempio **[!UICONTROL App mobile Luma]**.
1. Seleziona **[!UICONTROL Aggiungi servizio]** e seleziona **[!UICONTROL Adobe Target]** dal **[!UICONTROL Servizio]** elenco.
1. Inserisci il target **[!UICONTROL Token proprietà]** valore che desideri utilizzare per questa integrazione.

   Puoi trovare le tue proprietà nell’interfaccia utente di Target, in **[!UICONTROL Amministrazione]** > **[!UICONTROL Proprietà]**. Seleziona ![Codice](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) per visualizzare il token di proprietà per la proprietà che desideri utilizzare. Il token di proprietà ha un formato simile a `"at_property": "xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"`; è sufficiente immettere il valore `xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx`.

1. Seleziona **[!UICONTROL Salva]**.

   ![Aggiungere Target allo stream di dati](assets/edge-datastream-target.png)


## Installare Adobe Journey Optimizer - Estensione tag Decisioning

1. Accedi a **[!UICONTROL Tag]** e trova la tua proprietà tag mobile e apri la proprietà.
1. Seleziona **[!UICONTROL Estensioni]**.
1. Seleziona **[!UICONTROL Catalogo]**.
1. Cerca **[!UICONTROL Adobe Journey Optimizer - Decisioning]** estensione.
1. Installa l’estensione. L&#39;estensione non richiede una configurazione aggiuntiva.

   ![Aggiungere l’estensione Decisioning](assets/tag-add-decisioning-extension.png)


## Aggiornare lo schema

1. Passa all’interfaccia utente di Data Collection e seleziona Schemi dalla barra a sinistra.
1. Seleziona **[!UICONTROL Sfoglia]** dalla barra superiore.
1. Seleziona lo schema per aprirlo.
1. Nell’editor schema, seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Aggiungi]** accanto a **[!UICONTROL Gruppi di campi]**.
1. Nella finestra di dialogo Aggiungi gruppi di campi, cerca `proposition`, seleziona **[!UICONTROL Evento esperienza - Interazioni proposte]** e seleziona **[!UICONTROL Aggiungi gruppi di campi]**.
   ![Proposta](assets/schema-fieldgroup-proposition.png)
1. per salvare le modifiche apportate allo schema, seleziona **[!UICONTROL Salva]** .


## Convalida impostazione in Assurance

Per convalidare la configurazione in Assurance:

1. Passa all’interfaccia utente Assurance.
1. Seleziona **[!UICONTROL Configura]** nella barra a sinistra e seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) accanto a **[!UICONTROL Convalida configurazione]** sotto **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]**.
1. Seleziona **[!UICONTROL Salva]**.
1. Seleziona **[!UICONTROL Convalida configurazione]** nella barra a sinistra. La configurazione di entrambi gli stream di dati viene convalidata e la configurazione dell’SDK nell’applicazione.
   ![Convalida delle decisioni AJO](assets/ajo-decisioning-validation.png)

## Creare un test A/B

1. Nell’interfaccia utente di Target, seleziona **[!UICONTROL Attività]** dalla barra superiore.
1. Seleziona **[!UICONTROL Crea attività]** e **[!UICONTROL Test A/B]** dal menu di scelta rapida.
1. In **[!UICONTROL Crea attività test A/B]** modale, seleziona **[!UICONTROL Dispositivi mobili]** come **[!UICONTROL Tipo]**, seleziona un’area di lavoro dalla sezione **[!UICONTROL Scegli area di lavoro]** e seleziona la tua proprietà dalla sezione **[!UICONTROL Scegli proprietà]** elenco.
1. Seleziona **[!UICONTROL Crea]**.
   ![Creare un’attività Target](assets/target-create-activity1.png)

1. In **[!UICONTROL Attività senza titolo]** schermata, alla **[!UICONTROL Esperienze]** passaggio:

   1. Invio `luma-mobileapp-abtest` in **[!UICONTROL Seleziona posizione]** sotto L**[!UICONTROL POSIZIONE 1]**.
   1. Seleziona ![Chrevron verso il basso](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) accanto a **[!UICONTROL Contenuto predefinito]** e seleziona **[!UICONTROL Crea offerta JSON]** dal menu di scelta rapida.
   1. Copia il seguente JSON in **[!UICONTROL Immetti un oggetto JSON valido]**.

      ```json
      { 
          "title": "Luma Anaolog Watch",
          "text": "Designed to stand up to your active lifestyle, this women's Luma Analog Watch features a tasteful brushed chrome finish and a stainless steel, water-resistant construction for lasting durability.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Luma_Analog_Watch.jpg" 
      }
      ```

   1. Seleziona **[!UICONTROL + Aggiungi esperienza]**.

      ![Esperienza A](assets/target-create-activity-experienceA.png)

   1. Ripeti i passaggi b e c per l’esperienza B, ma utilizza il seguente JSON:

      ```json
      { 
          "title": "Aim Analog Watch",
          "text": "The flexible, rubberized strap is contoured to conform to the shape of your wrist for a comfortable all-day fit. The face features three illuminated hands, a digital read-out of the current time, and stopwatch functions.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Aim_Watch.jpg" 
      }
      ```

   1. Seleziona **[!UICONTROL Avanti]**.

      ![Esperienza B](assets/target-create-activity-experienceB.png)

1. In **[!UICONTROL Targeting]** fase, controlla la configurazione del test A/B. Per impostazione predefinita, entrambe le offerte vengono allocate in modo uniforme a tutti i visitatori. Seleziona **[!UICONTROL Next]** (Avanti) per continuare.

   ![Targeting](assets/taget-targeting.png)

1. In **[!UICONTROL Obiettivi e impostazioni]** passaggio:

   1. Rinomina l’attività senza titolo, ad esempio in `Luma Mobile SDK Tutorial - A/B Test Example`.
   1. Immetti un **[!UICONTROL Obiettivo]** per il test A/B, ad esempio `A/B Test for Luma mobile app tutorial`.
   1. Seleziona **[!UICONTROL Conversione]**, **[!UICONTROL Clic su una mbox]** nel **[!UICONTROL Metrica per obiettivo]** > **[!UICONTROL IL MIO OBIETTIVO PRINCIPALE]** affiancare e immettere il nome della posizione (mbox), ad esempio `luma-mobileapp-abtest`.
   1. Seleziona **[!UICONTROL Salva e chiudi]**.

      ![Impostazioni obiettivi](assets/target-goals.png)

1. Torna in **[!UICONTROL Tutte le attività]** schermata:

   1. Seleziona ![Altro](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) all’attività.
   1. Seleziona ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg) **[!UICONTROL Attiva]** per attivare il test A/B.

   ![Attiva](assets/target-activate.png)


## Implementare Target nell’app

Come descritto nelle lezioni precedenti, l’installazione di un’estensione tag per dispositivi mobili fornisce solo la configurazione. Ora devi installare e registrare l’SDK di ottimizzazione. Se questi passaggi non sono chiari, rivedi [Installare gli SDK](install-sdks.md) sezione.

>[!NOTE]
>
>Se hai completato il [Installare gli SDK](install-sdks.md) , l&#39;SDK è già installato e puoi passare al passaggio #7.
>

1. In Xcode, assicurati che [Ottimizzazione AEP](https://github.com/adobe/aepsdk-messaging-ios.git) viene aggiunto all’elenco dei pacchetti in Dipendenze dai pacchetti. Consulta [Gestione pacchetti Swift](install-sdks.md#swift-package-manager).
1. Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]**.
1. Assicurare `AEPMessaging` fa parte dell’elenco delle importazioni.

   `import AEPOptimize`

1. Assicurare `Optimize.self` fa parte dell’array di estensioni che si stanno registrando.

   ```swift
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   ```

1. Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utilità]** > **[!UICONTROL MobileSDK]** nel Navigatore progetti Xcode. Trova il ` func updatePropositionAT(ecid: String, location: String) async` funzione. Inspect il codice che configura
   * un dizionario XDM `xdmData`, contenente l’ECID per identificare il profilo per il quale si deve presentare il test A/B, e
   * il `decisionScope`, un array di posizioni in cui presentare il test A/B.

   Quindi la funzione chiama due API: [`Optimizer.clearCachePropositions`](https://support.apple.com/en-ie/guide/mac-help/mchlp1015/mac)  e [`Optimizer.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions). Queste funzioni cancellano tutte le proposte memorizzate nella cache e aggiornano le proposte per questo profilo.

1. Accedi a **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Visualizzazioni]** > **[!UICONTROL Personalizzazione]** > **[!UICONTROL TargetOffersView]** nel Navigatore progetti Xcode. Trova il `func getPropositionAT(location: String) async` e controllare il codice di questa funzione. La parte più importante di questa funzione è la  [`Optimizer.getPropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#getpropositions) Chiamata API, che
   * recupera le proposte per il profilo corrente in base all’ambito della decisione (che è la posizione definita nel test A/B) e
   * consente di annullare il wrapping del risultato in un contenuto che può essere visualizzato correttamente nell’app.

1. Ancora in **[!UICONTROL TargetOffersView]**, trova la f`unc updatePropositions(location: String) async` e aggiungi il seguente codice:

   ```swift
       Task {
           await self.updatePropositionAT(
               ecid: currentEcid,
               location: location
           )
       }
       try? await Task.sleep(seconds: 2.0)
       Task {
           await self.getPropositionAT(
               location: location
           )
       }
   ```

   Questo codice ti assicura di aggiornare le proposte e quindi recuperare i risultati utilizzando le funzioni descritte nei passaggi 5 e 6.


## Convalida tramite l’app

1. Apri l’app su un dispositivo o nel simulatore.

1. Vai a **[!UICONTROL Personalizzazione]** scheda.

1. Seleziona **[!UICONTROL Personalizzazione Edge]**.

1. Scorri verso il basso e visualizzi una delle due offerte definite nel test A/B visualizzato in **[!UICONTROL TARGET]** affiancare.

   <img src="assets/target-app-offer.png" width="300">


## Convalida implementazione in Assurance

Per convalidare il test A/B in Assurance:

1. Passa all’interfaccia utente Assurance.
1. Seleziona **[!UICONTROL Configura]** nella barra a sinistra e seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) accanto a **[!UICONTROL Revisione e simulazione]** sotto **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]**.
1. Seleziona **[!UICONTROL Salva]**.
1. Seleziona **[!UICONTROL Revisione e simulazione]** nella barra a sinistra. La configurazione di entrambi gli stream di dati viene convalidata e la configurazione dell’SDK nell’applicazione.
1. Seleziona **[!UICONTROL Richieste]** nella barra superiore. Visualizzi le richieste Target.
   ![Convalida delle decisioni AJO](assets/assurance-decisioning-requests.png)

1. Puoi esplorare le schede Simula ed Elenco eventi per ulteriori funzionalità, verificando la configurazione per le offerte Target.

## Implementare nell’app

Ora dovresti disporre di tutti gli strumenti necessari per iniziare ad aggiungere all’app Luma più test A/B o altre attività di Target, ove pertinente e applicabile.

>[!SUCCESS]
>
>Ora hai abilitato l’app per test A/B e visualizzato i risultati di un test A/B utilizzando Adobe Target e l’estensione Adobe Journey Optimizer - Decisioning per l’SDK di Adobe Experience Platform Mobile.<br/>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Successivo: **[Conclusione e prossime tappe](conclusion.md)**
