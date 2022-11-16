---
title: Iscriviti agli eventi di inserimento dati
seo-title: Subscribe to data ingestion events | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Iscriviti agli eventi di inserimento dati
description: In questa lezione, ti abbonerai agli eventi di acquisizione dei dati configurando un webhook con Adobe Developer Console e uno strumento di sviluppo webhook online. Puoi utilizzare questi eventi per monitorare lo stato dei processi di inserimento dei dati nelle lezioni successive.
role: Data Engineer
feature: Data Management
kt: 4348
thumbnail: 4348-subscribe-to-data-ingestion-events.jpg
exl-id: f4b90832-4415-476f-b496-2f079b4fcbbc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 1%

---

# Iscriviti agli eventi di inserimento dati

<!--25min-->

In questa lezione, ti abbonerai agli eventi di acquisizione dei dati configurando un webhook con Adobe Developer Console e uno strumento di sviluppo webhook online. Puoi utilizzare questi eventi per monitorare lo stato dei processi di inserimento dei dati nelle lezioni successive.

**Ingegneri dati** desidera abbonarsi a eventi di acquisizione dati al di fuori di questa esercitazione.
**Architetti dei dati** _saltare questa lezione_ e vai al [lezione di acquisizione batch](ingest-batch-data.md).

## Autorizzazioni necessarie

In [Configurare le autorizzazioni](configure-permissions.md) lezione, è possibile impostare tutti i controlli di accesso necessari per completare la lezione, in particolare:

<!--* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

>[!IMPORTANT]
>
> Queste notifiche attivate dagli eventi di acquisizione dati verranno applicate a _tutte le tue sandbox_, non solo il tuo `Luma Tutorial`. Nel tuo account potrebbero essere presenti anche notifiche provenienti da altri eventi di inserimento dati.


## Configurare un webhook

In questo esercizio, creeremo un webhook utilizzando uno strumento online chiamato webhook.site (sentiti libero di sostituire qualsiasi altro strumento di sviluppo webhook che preferisci utilizzare):

1. In un’altra scheda del browser, apri il sito web [https://webhook.site/](https://webhook.site/)
1. Ti viene assegnato un URL univoco, a cui devi aggiungere un segnalibro, come ti ritrovi successivamente nelle lezioni di inserimento dei dati:

   ![Webhook.site](assets/ioevents-webhook-home.png)
1. Seleziona la **Modifica** pulsante nella navigazione superiore
1. Come corpo della risposta, immetti `$request.query.challenge$`. Le notifiche degli eventi di Adobe I/O impostate più avanti in questa lezione inviano una sfida al webhook e ne richiedono l’inclusione nel corpo della risposta.
1. Seleziona il pulsante **Salva**

   ![Modificare la risposta](assets/ioevents-webhook-editResponse.png)

## Configurazione

1. In un’altra scheda del browser, apri le [Console Adobe Developer](https://console.adobe.io/)
1. Apri il tuo `Luma Tutorial API Project`
1. Seleziona la **[!UICONTROL Aggiungi a progetto]** quindi seleziona **[!UICONTROL Evento]**

   ![Aggiungi evento](assets/ioevents-addEvents.png)
1. Filtrare l’elenco selezionando **[!UICONTROL Experience Platform]**
1. Seleziona **[!UICONTROL Notifiche di Platform]**
1. Seleziona la **[!UICONTROL Successivo]** pulsante
   ![Aggiungere le notifiche](assets/ioevents-addNotifications.png)
1. Seleziona tutti gli eventi
1. Seleziona la **[!UICONTROL Successivo]** pulsante
   ![Selezionare gli abbonamenti](assets/ioevents-addSubscriptions.png)
1. Nella schermata successiva per la configurazione delle credenziali, seleziona la **[!UICONTROL Successivo]** pulsante di nuovo
   ![Ignora la schermata delle credenziali](assets/ioevents-clickNext.png)
1. Come **[!UICONTROL Nome registrazione evento]**, inserisci `Platform notifications`
1. Scorri verso il basso e seleziona per aprire **[!UICONTROL Webhook]** sezione
1. Come **[!UICONTROL URL webhook]**, incolla il valore dal **URL univoco** campo da webhook.site
1. Seleziona la **[!UICONTROL Salva eventi configurati]** pulsante
   ![Salvare gli eventi](assets/ioevents-addWebhook.png)
1. Attendi il salvataggio della configurazione e dovresti vedere che il tuo `Platform notifications` l&#39;evento è attivo con i dettagli del webhook e nessun messaggio di errore
   ![Configurazione salvata](assets/ioevents-webhookConfigured.png)
1. Torna alla scheda webhook.site e dovresti visualizzare la prima richiesta al webhook, risultante dalla convalida della configurazione di Developer Console:
   ![Prima richiesta in webhook.site](assets/ioevents-webhook-firstRequest.png)

Per il momento, imparerai di più su queste notifiche nelle prossime lezioni quando acquisisci i dati.

## Risorse aggiuntive

* [Webhook.site](https://webhook.site/)
* [Documentazione sulle notifiche di inserimento dati](https://experienceleague.adobe.com/docs/experience-platform/ingestion/quality/subscribe-events.html)
* [Guida introduttiva ad Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events/docs.html)

Ok, iniziamo finalmente [acquisizione di dati](ingest-batch-data.md)!
