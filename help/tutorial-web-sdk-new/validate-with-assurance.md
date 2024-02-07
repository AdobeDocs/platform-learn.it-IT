---
title: Convalidare le implementazioni dell’SDK web con Experienci Platform Assurance
description: Scopri come convalidare l’implementazione di Platform Web SDK con Adobe Experience Platform Assurance. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK,Tags,Assurance
source-git-commit: 4361d8e688ff2c2f3b5472f2cfff246efa627c7f
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# Convalidare le implementazioni dell’SDK web con Experienci Platform Assurance


## Avviare una sessione Assurance

Adobe Experience Platform Assurance è un prodotto di Adobe Experience Cloud che consente di verificare, verificare, simulare e convalidare le modalità di raccolta dei dati o di gestione delle esperienze.

Ulteriori informazioni su [Adobe Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=en).

Ogni volta che abiliti Edge Trace, viene avviata in background una sessione Assurance.

Per visualizzare la sessione Assurance:

1. Con Edge Trace abilitato, puoi visualizzare un’icona di collegamento in uscita in alto. Seleziona l’icona per aprire Assurance. Viene visualizzata una nuova scheda nel browser.

   ![Avvia sessione Assurance](assets/validate-debugger-start-assurnance.png)

1. Seleziona la riga con l’evento denominato Adobe Response Handle.
1. A destra viene visualizzato un menu. Seleziona la `+` accedi a `[!UICONTROL ACPExtensionEvent]`
1. Espandere selezionando `[!UICONTROL payload > 0 > payload > 0 > namespace]`. L’ID mostrato sotto l’ultimo `0` corrisponde al `ECID`. Lo sai dal valore che viene visualizzato in `namespace` corrispondenza `ECID`

   ![Convalida garanzia ECID](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >Il valore ECID potrebbe essere troncato a causa della larghezza della finestra. Seleziona la barra della maniglia nell’interfaccia e trascina a sinistra per visualizzare l’intero ECID.

Nelle lezioni future, utilizzi Assurance per convalidare i payload completamente elaborati raggiungendo un’applicazione di Adobe abilitata nel flusso di dati.

Ora che un oggetto XDM viene attivato su una pagina e sai come convalidare la raccolta dati, puoi configurare le singole applicazioni Adobe utilizzando Platform Web SDK.