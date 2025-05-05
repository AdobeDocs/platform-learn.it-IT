---
title: Iscriviti agli eventi di acquisizione dati
seo-title: Subscribe to data ingestion events | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Iscriviti agli eventi di acquisizione dati
description: In questa lezione, ti abbonerai a eventi di acquisizione dati configurando un webhook con Adobe Developer Console e uno strumento di sviluppo di webhook online. Seguirai questi eventi per monitorare lo stato dei processi di acquisizione dei dati nelle lezioni successive.
role: Data Engineer
feature: Data Management
jira: KT-4348
thumbnail: 4348-subscribe-to-data-ingestion-events.jpg
exl-id: f4b90832-4415-476f-b496-2f079b4fcbbc
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Iscriviti agli eventi di acquisizione dati

<!--25min-->

In questa lezione, ti abbonerai a eventi di acquisizione dati configurando un webhook con Adobe Developer Console e uno strumento di sviluppo di webhook online. Seguirai questi eventi per monitorare lo stato dei processi di acquisizione dei dati nelle lezioni successive.

**I Data Engineer** vorranno abbonarsi a eventi di acquisizione dati al di fuori di questa esercitazione.
**Gli architetti di dati** _possono saltare questa lezione_ e passare alla [lezione di acquisizione batch](ingest-batch-data.md).

## Autorizzazioni richieste

Nella lezione [Configurare le autorizzazioni](configure-permissions.md) è possibile impostare tutti i controlli di accesso necessari per completare la lezione, in particolare:

<!--* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

>[!IMPORTANT]
>
> Queste notifiche attivate dagli eventi di acquisizione dati verranno applicate a _tutte le sandbox_, non solo a `Luma Tutorial`. Potresti visualizzare anche le notifiche provenienti da altri eventi di acquisizione dati nel tuo account.


## Configurare un webhook

In questo esercizio creeremo un webhook utilizzando uno strumento online denominato webhook.site (puoi sostituire qualsiasi altro strumento di sviluppo del webhook che preferisci utilizzare):

1. In un&#39;altra scheda del browser, aprire il sito Web [https://webhook.site/](https://webhook.site/)
1. Ti viene assegnato un URL univoco, che dovresti aggiungere ai segnalibri, così come ti tornerà in seguito nelle lezioni di acquisizione dei dati:

   ![Sito Web](assets/ioevents-webhook-home.png)
1. Seleziona il pulsante **Modifica** nella navigazione superiore
1. Come corpo della risposta, immettere `$request.query.challenge$`. Le notifiche degli eventi Adobi I/O configurate più avanti in questa lezione inviano una sfida al webhook e richiedono che venga incluso nel corpo della risposta.
1. Seleziona il pulsante **Salva**

   ![Modifica la risposta](assets/ioevents-webhook-editResponse.png)

## Configura

1. In un&#39;altra scheda del browser, apri [Adobe Developer Console](https://console.adobe.io/)
1. Apri `Luma Tutorial API Project`
1. Seleziona il pulsante **[!UICONTROL Aggiungi al progetto]**, quindi seleziona **[!UICONTROL Evento]**

   ![Aggiungi evento](assets/ioevents-addEvents.png)
1. Filtra l&#39;elenco selezionando **[!UICONTROL Experience Platform]**
1. Seleziona **[!UICONTROL notifiche piattaforma]**
1. Seleziona il pulsante **[!UICONTROL Avanti]**
   ![Aggiungi le notifiche](assets/ioevents-addNotifications.png)
1. Seleziona tutti gli eventi
1. Seleziona il pulsante **[!UICONTROL Avanti]**
   ![Selezionare le sottoscrizioni](assets/ioevents-addSubscriptions.png)
1. Nella schermata successiva per la configurazione delle credenziali, seleziona nuovamente il pulsante **[!UICONTROL Avanti]**
   ![Ignora la schermata delle credenziali](assets/ioevents-clickNext.png)
1. Come **[!UICONTROL Nome registrazione evento]**, immettere `Platform notifications`
1. Scorri verso il basso e seleziona per aprire la sezione **[!UICONTROL Webhook]**
1. Come **[!UICONTROL URL webhook]**, incolla il valore dal campo **URL univoco** da webhook.site
1. Seleziona il pulsante **[!UICONTROL Salva eventi configurati]**
   ![Salva gli eventi](assets/ioevents-addWebhook.png)
1. Attendi che la configurazione venga salvata. Dovresti vedere che l&#39;evento `Platform notifications` è attivo con i dettagli del tuo webhook e senza messaggi di errore
   ![Configurazione salvata](assets/ioevents-webhookConfigured.png)
1. Torna alla scheda webhook.site e dovresti visualizzare la prima richiesta al webhook, derivante dalla convalida della configurazione di Developer Console:
   ![Prima richiesta in webhook.site](assets/ioevents-webhook-firstRequest.png)

Per il momento, acquisirai ulteriori informazioni su queste notifiche nelle prossime lezioni.

## Risorse aggiuntive

* [Sito Web](https://webhook.site/)
* [Documentazione delle notifiche di acquisizione dati](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html?lang=it)
* [Guida introduttiva agli eventi Adobe I/O](https://www.adobe.io/apis/experienceplatform/events/docs.html)

Ok, iniziamo finalmente [l&#39;acquisizione dei dati](ingest-batch-data.md)!
