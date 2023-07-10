---
title: Configurare uno spazio dei nomi delle identità
description: Scopri come configurare gli spazi dei nomi delle identità da utilizzare con Adobe Experience Platform Web SDK. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK,Tags,Identities
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 11%

---

# Configurare uno spazio dei nomi delle identità

Scopri come configurare gli spazi dei nomi delle identità da utilizzare con Adobe Experience Platform Web SDK.

Il [Servizio Adobe Experience Platform Identity](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=it) imposta un ID visitatore comune in tutte le soluzioni di Adobe per abilitare funzionalità di Experience Cloud come la condivisione dei tipi di pubblico tra le soluzioni. Puoi anche inviare i tuoi ID cliente personalizzati al Servizio per abilitare il targeting su più dispositivi e le integrazioni con altri sistemi, come il sistema di gestione delle relazioni con i clienti (CRM).

Se il tuo sito web utilizza già il servizio ID Experience Cloud sul tuo sito web, tramite API Visitor o l’estensione tag del servizio ID Experience Cloud, e desideri continuare a utilizzarlo durante la migrazione a Adobe Experience Platform Web SDK, devi utilizzare la versione più recente dell’API Visitor o l’estensione tag del servizio ID Experience Cloud. Consulta [Migrazione degli ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en) per ulteriori informazioni.

>[!NOTE]
>
> A scopo dimostrativo, gli esercizi di questa lezione consentono di acquisire i dettagli di identità di un cliente fittizio connesso a [Sito dimostrativo Luma](https://luma.enablementadobe.com/content/luma/us/en.html) utilizzando le credenziali, **utente: test@adobe.com / password: test**. Anche se puoi utilizzare questi passaggi per creare un’identità diversa per le tue finalità, per scoprire le funzionalità di Identity Map nell’interfaccia di Data Collection è consigliabile procedere prima di tutto per acquisire l’identità di esempio.

## Finalità di apprendimento

Alla fine di questa lezione, potrai:

* Comprendere gli spazi dei nomi delle identità
* Creare uno spazio dei nomi di identità personalizzato per acquisire un ID CRM interno


## Prerequisiti

Devi avere già completato le lezioni precedenti:

* [Configurare le autorizzazioni](configure-permissions.md)
* [Configurare gli schemi](configure-schemas.md)

>[!IMPORTANT]
>
>Il [Estensione ID Experience Cloud](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) non è necessario quando si implementa Adobe Experience Platform Web SDK, in quanto la libreria JavaScript dell’SDK Web contiene la funzionalità del servizio ID visitatore.

## Creare uno spazio dei nomi delle identità

In questo esercizio creerai uno spazio dei nomi delle identità per il campo di identità personalizzato di Luma, `lumaCrmId`. Gli spazi dei nomi delle identità svolgono un ruolo fondamentale nella creazione di profili cliente in tempo reale, in quanto due valori corrispondenti nello stesso spazio dei nomi consentono a due origini di dati di formare un grafo identità.

Prima di iniziare gli esercizi, guarda questo breve video per ulteriori informazioni sull’identità in Adobe Experience Platform:
>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

Ora crea uno spazio dei nomi per l’ID CRM Luma:

1. Apri [Interfaccia di Data Collection](https://launch.adobe.com/){target="_blank"}
1. Seleziona la sandbox in uso per l’esercitazione

   >[!NOTE]
   >
   >Se sei il cliente di un’applicazione basata su Platform come Real-Time CDP, per questa esercitazione ti consigliamo di utilizzare una sandbox di sviluppo. In caso contrario, utilizza **[!UICONTROL Prod]** sandbox.

1. Seleziona **[!UICONTROL Identità]** nel menu di navigazione a sinistra
1. Seleziona **[!UICONTROL Sfoglia]**

   Nell’interfaccia principale della pagina viene visualizzato un elenco di spazi dei nomi di identità, con i nomi, i simboli di identità, la data dell’ultimo aggiornamento e se si tratta di spazi dei nomi standard o personalizzati. La barra a destra contiene informazioni sulla forza del grafico Identità.

1. Seleziona **[!UICONTROL Crea uno spazio dei nomi delle identità]**

   ![Visualizza identità](assets/configure-identities-screen.png)

1. Fornisci i dettagli come segue e seleziona **[!UICONTROL Crea]**.

   | Campo | Valore |
   |---------------|-----------|
   | Nome visualizzato | ID CRM Luma |
   | Simbolo di identità | lumaCrmId |
   | Tipo | ID multi-dispositivo |


   ![Creare spazi dei nomi](assets/identities-create-namespace.png)


   Lo spazio dei nomi Identity viene popolato in **[!UICONTROL Identità]** schermo.

   ![Creare spazi dei nomi](assets/configure-identities-namespace-lumaCrmId.png)


>[!INFO]
>
> In [Creare elementi dati](create-data-elements.md) lezione, scoprirai come utilizzare questo spazio dei nomi quando invii identità a Platform Edge Network.

## Creare lo spazio dei nomi delle identità nella sandbox di produzione

A causa di una limitazione corrente nell’estensione Web SDK, è necessario creare spazi dei nomi di identità anche nella sandbox di produzione per utilizzare lo spazio dei nomi per inviare dati a una sandbox di sviluppo. Quindi, se per questa esercitazione hai utilizzato una sandbox di sviluppo, crea anche la `Luma CRM ID` dello spazio dei nomi nella sandbox di produzione.

## Risorse aggiuntive

* [Documentazione del servizio Identity](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=it)
* [API del servizio Identity](https://www.adobe.io/experience-platform-apis/references/identity-service/)

Ora che le identità sono presenti, è possibile configurare lo stream di dati.

[Successivo: ](configure-datastream.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
