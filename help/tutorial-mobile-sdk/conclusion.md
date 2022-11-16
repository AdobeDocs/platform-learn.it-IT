---
title: Conclusione e fasi successive
description: Come procedere dopo il completamento dell’esercitazione
recommendations: display,noCatalog
exl-id: 69db6cf3-0d5d-4864-aac2-e5e1aea4c02e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 4%

---

# Conclusione e fasi successive

Congratulazioni! Hai completato l’esercitazione &quot;Implementa Adobe Experience Cloud nelle app mobili&quot;!

Rivediamo rapidamente tutto quello che hai realizzato. Hai:

* Creazione di uno schema tramite gruppi di campi standard e personalizzati.
* Imposta un datastream.
* Configurata una proprietà tag mobile.
* Installate e implementate le estensioni dei tag in un’app.
* Implementazione delle seguenti funzionalità in un’app:
   * Consenso
   * Dati del ciclo di vita
   * Tracciamento degli eventi
   * Identità
   * Profilo
* Sono stati passati correttamente parametri di Experience Cloud a una visualizzazione Web.
* Convalida dell&#39;implementazione tramite Adobe Experience Platform Assurance.
* È stata connessa l’implementazione alle seguenti applicazioni di Experience Cloud:
   * Adobe Analytics
   * Experience Platform
   * Journey Optimizer

Sei pronto per iniziare la fase successiva del percorso: implementazione di Adobe Experience Cloud nella tua app mobile!

E c&#39;è sempre più da imparare! Di seguito sono riportati alcuni suggerimenti su altri contenuti da basare sulla tua implementazione:

* **Abilitare l’inoltro degli eventi**. L&#39;inoltro degli eventi può essere facilmente abilitato nel datastream. Qui [una lezione pratica per configurare l’inoltro degli eventi](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html) dall’esercitazione SDK per web. Utilizza solo le risorse create per la tua implementazione mobile e scegli i campi XDM implementati nell’app.
* **Attivare un percorso in Journey Optimizer**. Gli eventi implementati nell’app Luma possono essere utilizzati per attivare i percorsi. Ulteriori informazioni [tutorial video](https://experienceleague.adobe.com/docs/journey-optimizer-learn/tutorials/create-journeys/use-case-transactional-journey.html).
* **Customer Journey Analytics di connessione**. Se hai creato il [Set di dati della piattaforma](platform.md), puoi collegare il set di dati a Customer Journey Analytics. Ulteriori informazioni [tutorial video](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/connecting-customer-journey-analytics-to-data-sources-in-platform.html)
* **Abilita Audience Manager** Abilita l’Audience Manager nel tuo datastream per inviare i tuoi eventi esperienza XDM e iniziare a creare segmenti in base al coinvolgimento dell’app mobile.
* **Implementare Adobe Target**. Target non è ancora supportato con la configurazione del datastream collegata a una proprietà mobile, ma può essere implementato utilizzando [Estensione Adobe Target](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target).
* **Creare un segmento in Platform**. Se hai attivato la [schema e set di dati per Profilo cliente in tempo reale](platform.md), puoi creare segmenti in base agli eventi della tua app mobile, combinarli con dati provenienti da altre sorgenti e quindi inviare tali segmenti alle destinazioni in Real-time Customer Data Platform. Ulteriori informazioni sul generatore di segmenti in questo [tutorial video](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html).
* **Implementare l’SDK per web di Platform**. Dopo aver acquisito dimestichezza con un SDK, imparane un altro! Adobe Experience Platform Web SDK è l’SDK JavaScript utilizzato per alimentare i servizi di Experience Cloud e di terze parti sui siti web. C&#39;è un simile [esercitazione pratica per SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=it). Completa entrambi e visualizza l’unione dei profili tra dispositivi.
* **Ulteriori informazioni su Experience Platform**. Scopri di più su come acquisire dati da altre sorgenti e combinarli con i dati SDK di Mobile in [Guida introduttiva di Adobe Experience Platform per architetti di dati e data engineer](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html)


>[!NOTE]
>
>Grazie per aver investito il tuo tempo nell&#39;apprendimento dell&#39;SDK di Adobe Experience Platform Mobile. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)