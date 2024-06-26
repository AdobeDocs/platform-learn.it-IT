---
title: Configurare uno spazio dei nomi delle identità
description: Scopri come configurare gli spazi dei nomi delle identità da utilizzare con Adobe Experience Platform Web SDK. Questa lezione fa parte del tutorial Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK,Identities
jira: KT-15400
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: 1a4f2e3813a6db4bef77753525c8a7d40692a4b2
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 12%

---

# Configurare uno spazio dei nomi delle identità

Scopri come configurare gli spazi dei nomi di identità da utilizzare con Adobe Experience Platform Web SDK.

Il [Servizio Adobe Experience Cloud Identity](https://experienceleague.adobe.com/en/docs/id-service/using/home) imposta un ID visitatore comune (ECID) tra le applicazioni Adobe basate su SDK per abilitare le funzionalità di Experience Cloud, ad esempio la condivisione del pubblico tra le applicazioni. Puoi anche inviare i tuoi ID cliente personalizzati al Servizio per abilitare il targeting su più dispositivi e le integrazioni con altri sistemi, come il sistema di gestione delle relazioni con i clienti (CRM).

Il [Servizio Adobe Experience Platform Identity](https://experienceleague.adobe.com/en/docs/experience-platform/identity/home) (sì, sono due!) utilizza gli ECID e gli ID cliente per generare grafici di identità, che consentono di unire attributi e comportamenti in profili cliente in tempo reale.

>[!NOTE]
>
>Uno spazio dei nomi di identità personalizzato è _non obbligatorio_ per implementare Adobe Analytics, Adobe Target o Adobe Audience Manager con Web SDK (le identità autenticate possono essere trasmesse `data` oggetto invece del `xdm` come vedrai in seguito). Gli spazi dei nomi di identità sono necessari per le applicazioni native per la piattaforma come Journey Optimizer, Real-time Customer Data Platform, Customer Journey Analytics. Anche se puoi decidere di non utilizzare uno spazio dei nomi delle identità nella tua implementazione, è previsto che tu lo faccia come parte di questa esercitazione.

>[!NOTE]
>
> A scopo dimostrativo, gli esercizi di questa lezione consentono di acquisire i dettagli di identità di un cliente fittizio connesso a [Sito dimostrativo Luma](https://luma.enablementadobe.com/content/luma/us/en.html) utilizzando le credenziali, **utente: `test@adobe.com` / password: test**.

## Obiettivi di apprendimento

Alla fine di questa lezione, potrai:

* Comprendere gli spazi dei nomi delle identità
* Creare uno spazio dei nomi di identità personalizzato per acquisire un ID CRM interno


## Prerequisiti

Devi avere già completato le lezioni precedenti:

* [Configurare gli schemi](configure-schemas.md)

>[!IMPORTANT]
>
>Il [Estensione ID Experience Cloud](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension) non è necessario quando si implementa Adobe Experience Platform Web SDK, in quanto la libreria JavaScript dell’SDK Web contiene la funzionalità del servizio ID visitatore.
>
> Se il sito web utilizza già il servizio ID Experience Cloud sul sito web, tramite API Visitor o l’estensione tag del servizio ID Experience Cloud, e desideri continuare a utilizzarlo durante la migrazione a Adobe Experience Platform Web SDK, devi utilizzare la versione più recente dell’API Visitor o l’estensione tag del servizio ID Experience Cloud. Consulta [Migrazione degli ID](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/overview) per ulteriori informazioni.

## Creare uno spazio dei nomi delle identità

In questo esercizio creerai uno spazio dei nomi delle identità per il campo di identità personalizzato di Luma, `lumaCrmId`. Gli spazi dei nomi delle identità svolgono un ruolo fondamentale nella creazione di profili cliente in tempo reale, in quanto due valori corrispondenti nello stesso spazio dei nomi consentono a due origini di dati di formare un grafo identità.

Prima di iniziare gli esercizi, guarda questo breve video per ulteriori informazioni sull’identità in Adobe Experience Platform:

>[!VIDEO](https://video.tv.adobe.com/v/27841?learn=on)

Ora crea uno spazio dei nomi per l’ID CRM Luma:

1. Apri [Interfaccia di Data Collection](https://launch.adobe.com/){target="_blank"}
1. Seleziona la sandbox in uso per l’esercitazione

   >[!NOTE]
   >
   >Se sei il cliente di un’applicazione basata su Platform come Real-Time CDP o Journey Optimizer, per questa esercitazione ti consigliamo di utilizzare una sandbox di sviluppo. In caso contrario, utilizza **[!UICONTROL Prod]** sandbox.

1. Seleziona **[!UICONTROL Identità]** nel menu di navigazione a sinistra
1. Seleziona **[!UICONTROL Sfoglia]**

   Nell’interfaccia principale della pagina viene visualizzato un elenco di spazi dei nomi di identità, con i nomi, i simboli di identità, la data dell’ultimo aggiornamento e se si tratta di spazi dei nomi standard o personalizzati. La barra a destra contiene informazioni su [!UICONTROL Forza del grafo delle identità].

1. Seleziona **[!UICONTROL Creare lo spazio dei nomi delle identità]**

   ![Visualizza identità](assets/configure-identities-screen.png)

1. Fornisci i dettagli come segue e seleziona **[!UICONTROL Crea]**.

   | Campo | Valore |
   |---------------|-----------|
   | Nome visualizzato | ID CRM Luma |
   | Simbolo di identità | lumaCrmId |
   | Tipo | ID individuale per più dispositivi |


   ![Creare spazi dei nomi](assets/identities-create-namespace.png)


   Lo spazio dei nomi Identity viene popolato in **[!UICONTROL Identità]** schermo.

   ![Creare spazi dei nomi](assets/configure-identities-namespace-lumaCrmId.png)


>[!NOTE]
>
> In [Creare le identità](create-identities.md) lezione, scoprirai come utilizzare questo spazio dei nomi quando invii identità all’Edge Network di Platform.

Ora che le identità sono presenti, è possibile configurare lo stream di dati.

[Successivo: ](configure-datastream.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
