---
title: Iscriviti agli eventi di acquisizione dati
seo-title: Subscribe to data ingestion events | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Iscriviti agli eventi di acquisizione dati
description: In questa lezione, ti abbonerai a eventi di acquisizione dati configurando un webhook con la console Adobe Developer e uno strumento di sviluppo di webhook online. Seguirai questi eventi per monitorare lo stato dei processi di acquisizione dei dati nelle lezioni successive.
role: Data Engineer
feature: Data Management
jira: KT-4348
thumbnail: 4348-subscribe-to-data-ingestion-events.jpg
exl-id: f4b90832-4415-476f-b496-2f079b4fcbbc
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 1%

---

# Iscriviti agli eventi di acquisizione dati

<!--25min-->

In questa lezione, ti abbonerai a eventi di acquisizione dati configurando un webhook con la console Adobe Developer e uno strumento di sviluppo di webhook online. Seguirai questi eventi per monitorare lo stato dei processi di acquisizione dei dati nelle lezioni successive.

**Ingegneri dati** desideri abbonarti a eventi di acquisizione dati al di fuori di questa esercitazione.
**Architetti di dati** _può saltare questa lezione_ e vai al [lezione di acquisizione batch](ingest-batch-data.md).

## Autorizzazioni richieste

In [Configurare le autorizzazioni](configure-permissions.md) Per completare questa lezione, è necessario impostare tutti i controlli di accesso necessari, in particolare:

<!--* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

>[!IMPORTANT]
>
> Queste notifiche attivate dagli eventi di acquisizione dati verranno applicate a _tutte le sandbox_, non solo il tuo `Luma Tutorial`. Potresti visualizzare anche le notifiche provenienti da altri eventi di acquisizione dati nel tuo account.


## Configurare un webhook

In questo esercizio creeremo un webhook utilizzando uno strumento online denominato webhook.site (puoi sostituire qualsiasi altro strumento di sviluppo del webhook che preferisci utilizzare):

1. In un’altra scheda del browser, apri il sito web [https://webhook.site/](https://webhook.site/)
1. Ti viene assegnato un URL univoco, che dovresti aggiungere ai segnalibri, così come ti tornerà in seguito nelle lezioni di acquisizione dei dati:

   ![Webhook.site](assets/ioevents-webhook-home.png)
1. Seleziona la **Modifica** pulsante nella navigazione superiore
1. Come corpo della Risposta, immetti `$request.query.challenge$`. Le notifiche degli eventi Adobi I/O configurate più avanti in questa lezione inviano una sfida al webhook e richiedono che venga incluso nel corpo della risposta.
1. Seleziona il pulsante **Salva**

   ![Modifica la risposta](assets/ioevents-webhook-editResponse.png)

## Configurazione

1. In un&#39;altra scheda del browser, apri [Console Adobe Developer](https://console.adobe.io/)
1. Apri il `Luma Tutorial API Project`
1. Seleziona la **[!UICONTROL Aggiungi al progetto]** e quindi selezionare **[!UICONTROL Evento]**

   ![Aggiungi evento](assets/ioevents-addEvents.png)
1. Filtra l’elenco selezionando **[!UICONTROL Experience Platform]**
1. Seleziona **[!UICONTROL Notifiche della piattaforma]**
1. Seleziona la **[!UICONTROL Successivo]** pulsante
   ![Aggiungere le notifiche](assets/ioevents-addNotifications.png)
1. Seleziona tutti gli eventi
1. Seleziona la **[!UICONTROL Successivo]** pulsante
   ![Seleziona le sottoscrizioni](assets/ioevents-addSubscriptions.png)
1. Nella schermata successiva per la configurazione delle credenziali, seleziona **[!UICONTROL Successivo]** nuovamente pulsante
   ![Ignora la schermata delle credenziali](assets/ioevents-clickNext.png)
1. Come **[!UICONTROL Nome registrazione evento]**, immetti `Platform notifications`
1. Scorri verso il basso e seleziona per aprire **[!UICONTROL Webhook]** sezione
1. Come **[!UICONTROL URL webhook]**, incolla il valore dalla **L’URL univoco** campo da webhook.site
1. Seleziona la **[!UICONTROL Salva eventi configurati]** pulsante
   ![Salvare gli eventi](assets/ioevents-addWebhook.png)
1. Attendi il salvataggio della configurazione e dovresti notare che il `Platform notifications` l&#39;evento è attivo con i dettagli del webhook e nessun messaggio di errore
   ![Configurazione salvata](assets/ioevents-webhookConfigured.png)
1. Torna alla scheda webhook.site e dovresti visualizzare la prima richiesta al webhook, derivante dalla convalida della configurazione di Developer Console:
   ![Prima richiesta in webhook.site](assets/ioevents-webhook-firstRequest.png)

Per il momento, acquisirai ulteriori informazioni su queste notifiche nelle prossime lezioni.

## Risorse aggiuntive

* [Webhook.site](https://webhook.site/)
* [Documentazione delle notifiche di acquisizione dei dati](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html)
* [Guida introduttiva agli eventi Adobe I/O](https://www.adobe.io/apis/experienceplatform/events/docs.html)

Ok, iniziamo finalmente [acquisizione dei dati](ingest-batch-data.md)!
