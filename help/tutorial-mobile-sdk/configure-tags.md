---
title: Configurare una proprietà tag per le implementazioni dell’SDK di Platform Mobile
description: Scopri come configurare una proprietà tag nell’interfaccia [!UICONTROL Raccolta dati].
feature: Mobile SDK,Tags
jira: KT-14626
exl-id: 0c4b00cc-34e3-4d08-945e-3fd2bc1b6ccf
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 4%

---

# Configurare una proprietà tag

Scopri come configurare una proprietà tag nell’interfaccia [!UICONTROL Raccolta dati].

I tag in Adobe Experience Platform costituiscono la soluzione Adobe di nuova generazione per la gestione dei tag. I tag offrono ai clienti un modo semplice di implementare e gestire i tag di analisi, marketing e annunci pubblicitari necessari per fornire ai clienti esperienze personalizzate. Ulteriori informazioni su [Tag](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it) sono disponibili nella documentazione del prodotto.

## Prerequisiti

Per completare la lezione, devi disporre dell’autorizzazione per creare una proprietà tag. È inoltre utile avere una conoscenza di base dei tag.

>[!NOTE]
>
> Il platform launch (lato client) è ora [Tag](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it)

## Obiettivi di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

* Installa e configura le estensioni di tag per dispositivi mobili.
* Genera le istruzioni di installazione dell’SDK.

## Configurazione iniziale

1. Crea una nuova proprietà di tag mobile nell’interfaccia di raccolta dati:
   1. Seleziona **[!UICONTROL Tag]** nel menu di navigazione a sinistra.
   1. Seleziona **[!UICONTROL Nuova proprietà]**

      ![crea una proprietà tag](assets/tags-new-property.png).
   1. Per **[!UICONTROL Name]**, immetti `Luma Mobile App Tutorial`.
   1. Per **[!UICONTROL Platform]**, seleziona **[!UICONTROL Mobile]**.
   1. Seleziona **[!UICONTROL Salva]**.

      ![configurare la proprietà tag](assets/tags-property-config.png)

      >[!NOTE]
      >
      > Le impostazioni di consenso predefinite per le implementazioni dell&#39;sdk per dispositivi mobili basate su Edge, come quella che stai eseguendo in questa lezione, provengono dall&#39;estensione [!UICONTROL Consent] e non dall&#39;impostazione [!UICONTROL Privacy] nella configurazione della proprietà tag. Puoi aggiungere e configurare l’estensione Consent più avanti in questa lezione. Per ulteriori informazioni, consulta [la documentazione](https://developer.adobe.com/client-sdks/edge/consent-for-edge-network/).


1. Apri la nuova proprietà.
1. Creare una libreria:

   1. Vai a **[!UICONTROL Flusso di pubblicazione]** nella navigazione a sinistra.
   1. Seleziona **[!UICONTROL Aggiungi libreria]**.

      ![Seleziona Aggiungi libreria](assets/tags-create-library.png)

   1. Per **[!UICONTROL Name]**, immetti `Initial Build`.
   1. Per **[!UICONTROL Ambiente]**, selezionare **[!UICONTROL Sviluppo (sviluppo)]**.
   1. Seleziona ![Aggiungi pulsante](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Aggiungi tutte le risorse modificate]**.
   1. Seleziona **[!UICONTROL Salva e genera in sviluppo]**.

      ![Genera la libreria](assets/tags-save-library.png)

   1. Selezionare **[!UICONTROL Build iniziale]** come libreria di lavoro dal menu **[!UICONTROL Seleziona una libreria di lavoro]**.

      ![Seleziona come libreria di lavoro](assets/tags-working-library.png)
1. Verifica estensioni:

   1. Verificare che **[!UICONTROL Build iniziale]** sia selezionata come libreria predefinita.

   1. Seleziona **[!UICONTROL Estensioni]** nella barra a sinistra.

   1. Selezionare la scheda **[!UICONTROL Installato]**.

      Le estensioni [!UICONTROL Mobile Core] e [!UICONTROL Profile] devono essere preinstallate.

      ![Tag installati](assets/tags-installed.png)

## Configurazione dell&#39;estensione

1. Assicurati di trovarti in **[!UICONTROL Estensioni]** all&#39;interno della proprietà della tua app mobile.

1. Seleziona **[!UICONTROL Catalogo]**.

   ![installazione iniziale](assets/tags-starting.png)

1. Utilizza il campo ![Ricerca](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Ricerca]** per trovare l&#39;estensione **Identità**.

   1. Cerca `Identity`.

   2. Seleziona l&#39;estensione **[!UICONTROL Identity]**.

   3. Selezionare **[!UICONTROL Installa]**.

      ![Installazione identità](assets/tags-identity-install.png)

   Questa estensione non richiede alcuna ulteriore configurazione.

1. Utilizza il campo ![Ricerca](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Ricerca]** per trovare e installare l&#39;estensione **AEP Assurance**.

   Questa estensione non richiede alcuna ulteriore configurazione.

1. Utilizza il campo ![Ricerca](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Ricerca]** per trovare e installare l&#39;estensione **Consenso**. Nella schermata di configurazione:

   1. Seleziona **[!UICONTROL In sospeso]**. In questa esercitazione, gestisci ulteriormente il consenso nell’applicazione. Ulteriori informazioni sull&#39;estensione Consent sono disponibili nella [documentazione](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/).
   1. Seleziona **[!UICONTROL Salva nella libreria]**.

      ![impostazioni consenso](assets/tags-extension-consent.png)

1. Utilizza il campo ![Cerca](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Cerca]** per trovare e installare l&#39;estensione **Adobe Experience Platform Edge Network**.

   1. In **[!UICONTROL Datastream]** seleziona lo **[!UICONTROL Datastream]** creato nel [passaggio precedente](create-datastream.md) per ciascuno degli ambienti, ad esempio **[!DNL Luma Mobile App]**.

   1. Se non è già stato popolato, specificare il **[!UICONTROL dominio Edge Network]** all&#39;interno di **[!UICONTROL Configurazione dominio]**. Il dominio di Edge Network è il nome dell&#39;organizzazione, seguito da `data.adobedc.net`, ad esempio `techmarketingdemos.data.adobedc.net`.

   1. Dal menu **[!UICONTROL Salva nella libreria]**, selezionare **[!UICONTROL Salva nella libreria e genera]**.

      ![impostazioni di rete edge](assets/tags-extension-edge.png)

La libreria viene creata per le nuove estensioni e configurazioni. Una compilazione completata è indicata da un <span style="color:green">●</span> nel pulsante **[!UICONTROL Build iniziale]**.


## Generare istruzioni di installazione SDK

1. Seleziona **[!UICONTROL Ambienti]** dalla barra a sinistra.

1. Selezionare l&#39;icona di installazione **[!UICONTROL Sviluppo]** ![Box](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg).

   ![ambienti nella schermata iniziale](assets/tags-environments.png)

1. Nella finestra di dialogo **[!UICONTROL Istruzioni di installazione mobile]**, seleziona la scheda **[!UICONTROL iOS]**.

1. È possibile copiare ![Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) le istruzioni per configurare il progetto utilizzando CocoaPods. I CocoaPod vengono utilizzati per gestire le versioni e i download dell’SDK. Per ulteriori informazioni, consulta la [documentazione di CocoaPods](https://cocoapods.org/). Se utilizzi Android™ come piattaforma di sviluppo, Gradle è lo strumento per gestire la versione SDK, i download e le dipendenze. Per ulteriori informazioni, consulta la [documentazione Gradle](https://gradle.org/)

   Le istruzioni di installazione forniscono un buon punto di partenza per l’implementazione. Puoi trovare ulteriori informazioni [qui](https://developer.adobe.com/client-sdks/documentation/getting-started/get-the-sdk/).

   >[!INFO]
   >
   >Per il resto di questo tutorial, **non** utilizzerai le istruzioni CocoaPods ma una configurazione nativa basata su Swift Package Manager (SPM).
   >

1. Selezionare la scheda **[!UICONTROL Swift]** sotto **[!UICONTROL Aggiungi codice di inizializzazione]**. Questo blocco di codice mostra come importare gli SDK richiesti e registrare le estensioni all’avvio. Questo argomento è trattato più dettagliatamente in [Installare gli SDK](install-sdks.md).

1. Copiare ![Copia](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) l&#39;ID **[!UICONTROL File di ambiente]** e archiviarlo in un luogo che sarà necessario in un secondo momento. Questo ID univoco punta all’ambiente di sviluppo. Ogni ambiente (Produzione, Staging, Sviluppo) ha un proprio valore ID univoco.

   ![istruzioni di installazione](assets/tags-install-instructions.png)

>[!NOTE]
>
>Le istruzioni di installazione devono essere considerate un punto di partenza e non una documentazione definitiva. Le versioni più recenti dell&#39;SDK e gli esempi di codice sono disponibili nella [documentazione ufficiale](https://developer.adobe.com/client-sdks/home/).

## Architettura dei tag per dispositivi mobili

Se conosci la versione web di Tag, precedentemente Launch, è importante comprendere le differenze su dispositivi mobili.

* Sul web, viene eseguito il rendering di una proprietà tag in JavaScript che è poi (in genere) ospitato nel cloud. Viene fatto riferimento al file JavaScript direttamente nel sito Web.

* In una proprietà di tag mobile, le regole e le configurazioni vengono sottoposte a rendering in file JSON ospitati nel cloud. I file JSON vengono scaricati e letti dall’estensione core per dispositivi mobili nell’app mobile. Le estensioni sono SDK separati che funzionano insieme. Se aggiungi un’estensione alla proprietà tag, devi aggiornare anche l’app. Se modifichi l’impostazione di un’estensione o crei una regola, tali modifiche vengono applicate nell’app dopo che la libreria di tag aggiornata è stata pubblicata. Questa flessibilità ti consente di modificare le impostazioni (come l’ID suite di rapporti di Adobe Analytics) o anche cambiare il comportamento dell’app (utilizzando elementi dati e regole, come vedrai nelle lezioni successive) senza dover modificare il codice nell’app e inviare nuovamente l’app store.

>[!SUCCESS]
>
>Nel resto dell&#39;esercitazione è disponibile una proprietà di tag per dispositivi mobili.
>
>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [Experience League post di discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Successivo: **[Installare gli SDK](install-sdks.md)**
