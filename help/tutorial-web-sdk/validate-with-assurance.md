---
title: Convalidare le implementazioni di Web SDK con Experience Platform Assurance
description: Scopri come convalidare l’implementazione di Platform Web SDK con Adobe Experience Platform Assurance. Questa lezione fa parte del tutorial Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK,Tags,Assurance
jira: KT-15406
exl-id: 31e381ea-fbaf-495f-a6e9-2ff6c0d36939
source-git-commit: 1fc027db2232c8c56de99d12b719ec10275b590a
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 7%

---

# Convalidare le implementazioni di Web SDK con Experience Platform Assurance

Adobe Experience Platform Assurance è una funzione che consente di ispezionare, verificare, simulare e convalidare le modalità di raccolta dei dati o di gestione delle esperienze. Ulteriori informazioni su [Adobe Assurance](https://experienceleague.adobe.com/it/docs/experience-platform/assurance/home).


>[!WARNING]
>
> Il sito web Luma utilizzato in questa esercitazione dovrebbe essere sostituito durante la settimana del 16 febbraio 2026. Il lavoro svolto come parte di questo tutorial potrebbe non essere applicabile al nuovo sito web.

## Obiettivi di apprendimento

Alla fine di questa lezione, potrai:

* Avviare una sessione di Assurance
* Visualizzare le richieste inviate a e da Platform Edge Network

## Prerequisiti

Conosci i tag di raccolta dati e il [sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} e hai completato le lezioni precedenti nell’esercitazione:

* [Configurare uno schema XDM](configure-schemas.md)
* [Configurare uno spazio dei nomi delle identità](configure-identities.md)
* [Configurare uno stream di dati](configure-datastream.md)
* [Estensione Web SDK installata nella proprietà tag](install-web-sdk.md)
* [Creare elementi dati](create-data-elements.md)
* [Creare identità](create-identities.md)
* [Creare una regola di tag](create-tag-rule.md)
* [Convalida con Debugger](validate-with-debugger.md)


## Avviare e visualizzare una sessione di Assurance

Esistono diversi modi per avviare una sessione Assurance.

### Avviare una sessione di Assurance nel debugger

Ogni volta che abiliti Edge Trace in Adobe Experience Platform Debugger, viene avviata in background una sessione di Assurance.

Rivedi come abbiamo fatto questo nella lezione di Debugger:

1. Vai al [sito demo Luma](https://luma.enablementadobe.com/content/luma/us/en.html) e utilizza il debugger per [passare la proprietà tag sul sito alla tua proprietà di sviluppo](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Nel menu di navigazione a sinistra di **[!UICONTROL Experience Platform Debugger]** seleziona **[!UICONTROL Registri]**
1. Seleziona la scheda **[!UICONTROL Edge]** e seleziona **[!UICONTROL Connetti]**

   ![Connetti traccia Edge](assets/analytics-debugger-edgeTrace.png)
1. Con Edge Trace abilitato, puoi visualizzare un’icona di collegamento in uscita in alto. Seleziona l’icona per aprire Assurance.

   ![Avvia sessione Assurance](assets/validate-debugger-start-assurnance.png)

1. Viene visualizzata una nuova scheda del browser con l’interfaccia Assurance.

### Avviare una sessione di Assurance dall’interfaccia di Assurance

1. Apri l&#39;interfaccia di [Data Collection](https://experience.adobe.com/#/data-collection/home){target="_blank"}
1. Seleziona Assurance nel menu di navigazione a sinistra
1. Seleziona Crea sessione
   ![Crea una sessione Assurance](assets/assurance-create-session.png)
1. Seleziona Inizio
1. Assegna un nome alla sessione, ad esempio `Luma Web SDK validation`
1. Come **[!UICONTROL URL di base]** immettere `https://luma.enablementadobe.com/`
   ![Assegna un nome alla sessione di Assurance](assets/assurance-name-session.png)
1. Nella schermata successiva, seleziona **[!UICONTROL Copia collegamento]**
1. Seleziona l’icona per copiare il collegamento negli Appunti
1. Incolla l’URL nel browser, che aprirà il sito web Luma con uno speciale parametro URL `adb_validation_sessionid` e avvierà la sessione
1. Nell’interfaccia di Assurance, dovrebbe essere visualizzato un messaggio per indicare che la connessione alla sessione è avvenuta correttamente e dovrebbero essere visualizzati gli eventi acquisiti nell’interfaccia di Assurance.
   ![La sessione Assurance è stata connessa](assets/assurance-success.png)

## Convalidare lo stato corrente dell’implementazione di Web SDK

Le informazioni da visualizzare in questa fase dell’implementazione sono limitate. Un valore visibile è l’ID Experience Cloud (ECID) generato su Platform Edge Network:

1. Selezionare la riga con l&#39;evento denominato `Alloy Response Handle`.
1. A destra viene visualizzato un menu. Seleziona il segno `+` accanto a `[!UICONTROL ACPExtensionEventData]`
1. Espandere selezionando `[!UICONTROL payload > 0 > payload > 0 > namespace]`. L&#39;ID visualizzato sotto l&#39;ultimo `0` corrisponde a `ECID`. Si sa che dal valore visualizzato in `namespace` corrisponde a `ECID`

   ![Assurance convalida ECID](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >Il valore ECID potrebbe essere troncato a causa della larghezza della finestra. Seleziona la barra della maniglia nell’interfaccia e trascina a sinistra per visualizzare l’intero ECID.

Nelle lezioni future, utilizzerai Assurance per convalidare i payload completamente elaborati che raggiungono un’applicazione Adobe abilitata nello stream di dati.

Ora che un oggetto XDM viene attivato su una pagina e sai come convalidare la raccolta dati, puoi configurare Experience Platform e le singole applicazioni Adobe utilizzando Platform Web SDK.

>[!NOTE]
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=it)
