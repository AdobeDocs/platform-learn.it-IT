---
title: Convalidare le implementazioni dell’SDK web con Experienci Platform Assurance
description: Scopri come convalidare l’implementazione di Platform Web SDK con Adobe Experience Platform Assurance. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK,Tags,Assurance
exl-id: 31e381ea-fbaf-495f-a6e9-2ff6c0d36939
source-git-commit: aeff30f808fd65370b58eba69d24e658474a92d7
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 2%

---

# Convalidare le implementazioni dell’SDK web con Experienci Platform Assurance

Adobe Experience Platform Assurance è un prodotto di Adobe Experience Cloud che consente di verificare, verificare, simulare e convalidare le modalità di raccolta dei dati o di gestione delle esperienze. Ulteriori informazioni su [Adobe Assurance](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home).


## Obiettivi di apprendimento

Alla fine di questa lezione, potrai:

* Avviare una sessione Assurance
* Edge Network di visualizzazione delle richieste inviate a e da Platform

## Prerequisiti

Conosci i tag di raccolta dati e la [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} e hanno completato le lezioni precedenti nell’esercitazione:

* [Configurare uno schema XDM](configure-schemas.md)
* [Configurare uno spazio dei nomi delle identità](configure-identities.md)
* [Configurare uno stream di dati](configure-datastream.md)
* [Estensione Web SDK installata nella proprietà tag](install-web-sdk.md)
* [Creare elementi dati](create-data-elements.md)
* [Creare identità](create-identities.md)
* [Creare una regola di tag](create-tag-rule.md)
* [Convalida con Debugger](validate-with-debugger.md)


## Avviare e visualizzare una sessione Assurance

Esistono diversi modi per avviare una sessione Assurance.

### Avviare una sessione Assurance nel debugger

Ogni volta che abiliti Edge Trace in Adobi Experience Platform Debugger, viene avviata in background una sessione Assurance.

Rivedi come abbiamo fatto questo nella lezione di Debugger:

1. Vai a [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html) e utilizza il debugger per [modifica la proprietà tag sul sito con la tua proprietà di sviluppo](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Nella barra di navigazione a sinistra di **[!UICONTROL Debugger Experienci Platform]** seleziona **[!UICONTROL Registri]**
1. Seleziona la **[!UICONTROL Bordo]** e seleziona **[!UICONTROL Connetti]**

   ![Connetti traccia spigolo](assets/analytics-debugger-edgeTrace.png)
1. Con Edge Trace abilitato, puoi visualizzare un’icona di collegamento in uscita in alto. Seleziona l’icona per aprire Assurance. Viene visualizzata una nuova scheda nel browser.

   ![Avvia sessione Assurance](assets/validate-debugger-start-assurnance.png)


### Avviare una sessione Assurance dall&#39;interfaccia Assurance

1. Apri [Interfaccia di Data Collection](https://experience.adobe.com/#/data-collection/home){target="_blank"}
1. Seleziona Assurance nel menu di navigazione a sinistra
1. Seleziona Crea sessione
   ![Creare una sessione Assurance](assets/assurance-create-session.png)
1. Seleziona Inizio
1. Assegna un nome alla sessione, ad esempio: `Luma Web SDK validation`
1. Come **[!UICONTROL URL di base]** Invio `https://luma.enablementadobe.com/`
   ![Assegnare un nome alla sessione Assurance](assets/assurance-name-session.png)
1. Nella schermata successiva, seleziona **[!UICONTROL Copia collegamento]**
1. Seleziona l’icona per copiare il collegamento negli Appunti
1. Incolla l’URL nel browser, che aprirà il sito web Luma con uno speciale parametro URL `adb_validation_sessionid` e avvia la sessione
1. Nell’interfaccia Assurance viene visualizzato un messaggio che indica che la connessione alla sessione è avvenuta correttamente e nell’interfaccia Assurance vengono visualizzati gli eventi.
   ![La sessione di verifica è connessa](assets/assurance-success.png)

## Convalidare lo stato corrente dell’implementazione dell’SDK web

Le informazioni da visualizzare in questa fase dell’implementazione sono limitate. Un valore visibile è l’ID Experience Cloud (ECID) generato su Platform Edge Network:

1. Seleziona la riga con l’evento denominato Adobe Response Handle.
1. A destra viene visualizzato un menu. Seleziona la `+` accedi a `[!UICONTROL ACPExtensionEvent]`
1. Espandere selezionando `[!UICONTROL payload > 0 > payload > 0 > namespace]`. L’ID mostrato sotto l’ultimo `0` corrisponde al `ECID`. Lo sai dal valore che viene visualizzato in `namespace` corrispondenza `ECID`

   ![Convalida garanzia ECID](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >Il valore ECID potrebbe essere troncato a causa della larghezza della finestra. Seleziona la barra della maniglia nell’interfaccia e trascina a sinistra per visualizzare l’intero ECID.

Nelle lezioni future, utilizzi Assurance per convalidare i payload completamente elaborati raggiungendo un’applicazione di Adobe abilitata nel flusso di dati.

Ora che un oggetto XDM viene attivato su una pagina e sai come convalidare la raccolta dati, puoi configurare le singole applicazioni Adobe utilizzando Platform Web SDK.

[Successivo: ](setup-experience-platform.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
