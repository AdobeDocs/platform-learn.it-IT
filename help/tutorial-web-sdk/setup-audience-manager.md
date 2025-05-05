---
title: Configurare un Audience Manager con Platform Web SDK
description: Scopri come configurare Adobe Audience Manager utilizzando Platform Web SDK e convalidare l’implementazione utilizzando una destinazione cookie. Questa lezione fa parte del tutorial Implementare Adobe Experience Cloud con Web SDK.
solution: Data Collection, Audience Manager
jira: KT-15409
exl-id: 45db48e9-73cf-4a9c-88f4-b5872a8224d3
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 4%

---

# Configurare un Audience Manager con Platform Web SDK

Scopri come configurare Adobe Audience Manager utilizzando Adobe Experience Platform Web SDK e convalidare l’implementazione utilizzando una destinazione cookie.

[Adobe Audience Manager](https://experienceleague.adobe.com/it/docs/audience-manager) è la soluzione Adobe Experience Cloud che fornisce tutto il necessario per raccogliere informazioni rilevanti dal punto di vista commerciale sui visitatori del sito, creare segmenti commerciabili e distribuire pubblicità e contenuti mirati al pubblico giusto.

![Diagramma Web SDK e Adobe Audience Manager](assets/dc-websdk-aam.png)

## Obiettivi di apprendimento

Alla fine di questa lezione, potrai:

* Configurare uno stream di dati per abilitare Audience Manager
* Abilitare una destinazione cookie in Audience Manager
* Convalida l’implementazione di Audience Manager confermando la qualifica del pubblico con Adobe Experience Platform Debugger

## Prerequisiti

Per completare questa lezione, devi prima:

* Completa le lezioni precedenti nelle sezioni Configurazione iniziale e Configurazione tag di questa esercitazione.
* Accedi a Adobe Audience Manager e disponi delle autorizzazioni appropriate per creare, leggere e scrivere caratteristiche, segmenti e destinazioni. Per ulteriori informazioni, rivedere il controllo degli accessi basato sul ruolo di [Audience Manager](https://experienceleague.adobe.com/it/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control).

## Configurare lo stream di dati

L&#39;implementazione di Audience Manager con Platform Web SDK è diversa dall&#39;implementazione con [Server-Side Forwarding (SSF)](https://experienceleague.adobe.com/it/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/server-side-forwarding/ssf). L’inoltro lato server trasmette ad Audience Manager i dati della richiesta di Adobe Analytics. Un’implementazione di Platform Web SDK trasmette i dati XDM inviati all’Edge Network di Platform all’Audience Manager. Audience Manager abilitato nello stream di dati:

1. Vai all&#39;interfaccia [Raccolta dati](https://experience.adobe.com/#/data-collection){target="blank"}
1. Nel menu di navigazione a sinistra, seleziona **[!UICONTROL Flussi di dati]**
1. Seleziona lo stream di dati `Luma Web SDK: Development Environment` creato in precedenza

   ![Seleziona lo stream di dati di Luma Web SDK](assets/datastream-luma-web-sdk-development.png)

1. Seleziona **[!UICONTROL Aggiungi servizio]**
   ![Aggiungi un servizio allo stream di dati](assets/aam-datastream-addService.png)
1. Seleziona **[!UICONTROL Adobe Audience Manager]** come **[!UICONTROL Servizio]**
1. Conferma che **[!UICONTROL Destinazioni cookie abilitate]** e **[!UICONTROL Destinazioni URL abilitate]** siano selezionate
1. Seleziona **[!UICONTROL Salva]**
   ![Conferma le impostazioni dello stream di dati di Audience Manager e salva](assets/aam-datastream-save.png)

## Creare un’origine dati

Quindi, crea un [Data Source](https://experienceleague.adobe.com/it/docs/audience-manager/user-guide/features/data-sources/datasources-list-and-settings), uno strumento fondamentale per organizzare i dati in Audience Manager:

1. Passa all&#39;interfaccia [Audience Manager](https://experience.adobe.com/#/audience-manager/)
1. Seleziona **[!UICONTROL Dati pubblico]** dalla navigazione superiore
1. Seleziona **[!UICONTROL Origini dati]** dal menu a discesa
1. Seleziona il pulsante **[!UICONTROL Aggiungi nuovo]** nella parte superiore della pagina Origini dati

   ![Origini dati Audienci Manager Adobe Experience Platform](assets/data-sources-list.jpg)

1. Assegna al Data Source un nome descrittivo e una descrizione. Per la configurazione iniziale, è possibile denominare `Platform Web SDK tutorial`.
1. Imposta **[!UICONTROL Tipo ID]** su **[!UICONTROL Cookie]**
1. Nella sezione **[!UICONTROL Controlli sull&#39;esportazione dei dati]**, seleziona **[!UICONTROL Nessuna restrizione]**

   ![Installazione di Adobe Experience Platform Audience Manager Data Source](assets/data-source-details.png)

1. **[!UICONTROL Salva]** il Data Source


## Creare una caratteristica

Dopo il salvataggio del Data Source, imposta una [caratteristica](https://experienceleague.adobe.com/it/docs/audience-manager/user-guide/features/traits/traits-overview). Le caratteristiche sono una combinazione di uno o più segnali in Audience Manager. Creare una caratteristica per i visitatori della homepage.

>[!NOTE]
>
>Tutti i dati XDM vengono inviati ad Audience Manager se sono abilitati nello stream di dati, tuttavia i dati potrebbero richiedere 24 ore finché non sono disponibili nel rapporto Segnali non utilizzati. Crea caratteristiche esplicite per i dati XDM da utilizzare immediatamente in Audience Manager, come descritto in questo esercizio.

1. Seleziona **[!UICONTROL Dati pubblico]** > **[!UICONTROL Caratteristiche]**
1. Seleziona **[!UICONTROL Aggiungi nuova]** > **[!UICONTROL Caratteristica basata su regole]**

   ![Caratteristiche basate su regole di Audience Manager di Adobe Experience Platform](assets/rule-based-trait.jpg)

1. Assegna alla caratteristica un nome descrittivo e una descrizione, `Luma homepage view`
1. Seleziona **[!UICONTROL Data Source]** creato nella sezione precedente.
1. **[!UICONTROL Selezionare una cartella]** in cui salvare le caratteristiche nel riquadro a destra. È possibile creare una cartella selezionando **l&#39;icona +** accanto a una cartella padre esistente. È possibile denominare la nuova cartella `Platform Web SDK tutorial`.
1. Espandi il cursore **[!UICONTROL Espressione caratteristica]** e seleziona **[!UICONTROL Generatore espressioni]**. Devi fornire una coppia chiave-valore che indica una visita alla homepage.
1. Apri la [home page Luma](https://luma.enablementadobe.com/content/luma/us/en.html) (mappata alla tua proprietà tag) e il **Adobe Experience Platform Debugger** e aggiorna la pagina.
1. Osserva le Richieste di rete e i dettagli dell’evento per Platform Web SDK per trovare la chiave e il valore del nome per la home page.
   ![Dati XDM di Audience Manager Adobe Experience Platform](assets/xdm-keyvalue.jpg)
1. Tornare al Generatore di espressioni nell&#39;interfaccia utente Audience Manager e immettere la chiave come **`web.webPageDetails.name`** e il valore di **`content:luma:us:en`**. Questo passaggio ti assicura di attivare una caratteristica ogni volta che carichi la pagina home.
1. **[!UICONTROL Salva]** la caratteristica.


## Crea un segmento

I passaggi successivi consistono nel creare un **segmento** e assegnare la caratteristica appena definita a questo segmento.

1. Seleziona **[!UICONTROL Dati pubblico]** nella navigazione superiore e seleziona **[!UICONTROL Segmenti]**
1. Seleziona **[!UICONTROL Aggiungi nuovo]** in alto a sinistra per aprire il Generatore di segmenti
1. Assegna al segmento un nome descrittivo e una descrizione, ad esempio `Platform Web SDK - Homepage visitors`
1. **[!UICONTROL Selezionare una cartella]** in cui salvare il segmento nel riquadro a destra. È possibile creare una cartella selezionando **l&#39;icona +** accanto a una cartella padre esistente. È possibile denominare la nuova cartella `Platform Web SDK tutorial`.
1. Aggiungi un codice di integrazione, che in questo caso è un set casuale di numeri.
1. Nella sezione **[!UICONTROL Data Source]**, seleziona **[!UICONTROL Audience Manager]** e l&#39;origine dati creata in precedenza
1. Espandi la sezione **[!UICONTROL Caratteristiche]** e cerca la caratteristica creata
1. Seleziona **[!UICONTROL Aggiungi caratteristica]**.
1. Seleziona **[!UICONTROL Salva]** nella parte inferiore della pagina

   ![Aggiungi caratteristica Audience Manager Adobe Experience Platform](assets/add-trait-segment.jpg)

   ![Aggiungi caratteristica Audience Manager Adobe Experience Platform](assets/saved-segment.jpg)

## Creare una destinazione

Quindi, crea una **destinazione basata su cookie** utilizzando **Generatore di destinazione**. Il Generatore di destinazioni consente di creare e gestire cookie, URL e destinazioni da server a server.

1. Apri il Generatore di destinazioni selezionando **[!UICONTROL Destinazioni]** nel menu **Dati pubblico** nella navigazione superiore
1. Seleziona **[!UICONTROL Crea destinazione]**
1. Immettere un nome e una descrizione, `Platform Web SDK tutorial`
1. Come **[!UICONTROL Categoria]**, seleziona **[!UICONTROL Personalizzato]**
1. Come **[!UICONTROL Tipo]**, seleziona **[!UICONTROL Cookie]**

   ![Aggiungi caratteristica Audience Manager Adobe Experience Platform](assets/destination-settings.jpg)

1. Apri la sezione **[!UICONTROL Configurazione]** per immettere i dettagli sulla destinazione del cookie
1. Assegna al cookie un nome descrittivo, `platform_web_sdk_tutorial`
1. Come **[!UICONTROL dominio cookie]**, aggiungi il dominio del sito in cui stai pianificando l&#39;integrazione, per l&#39;esercitazione inserisci il dominio Luma, `luma.enablementadobe.com`
1. Come opzione **[!UICONTROL Dati Publish in]**, selezionare **[!UICONTROL Solo i domini selezionati]**
1. Seleziona il dominio se non è già stato aggiunto
1. Come **[!UICONTROL Formato dati]**, seleziona **[!UICONTROL Chiave singola]** e assegna al cookie una chiave. Per questa esercitazione utilizzare `segment` come valore chiave.
1. Infine, selezionare **[!UICONTROL Salva]** per salvare i dettagli della configurazione di destinazione.

   ![Sezione Configurazione di destinazione Audience Manager](assets/aam-destination-config-dw.png)

<!--
   ![Adobe Experience Platform Audience Manager Add Trait](assets/aam-destination-config.jpg)


   ![Adobe Experience Platform Audience Manager Add Trait](assets/cookie-destination-config.jpg)
-->

1. Nella sezione **[!UICONTROL Mappature segmento]**, utilizza la funzione **[!UICONTROL Cerca e aggiungi segmenti]** per cercare `Platform Web SDK - Homepage visitors` creato in precedenza e selezionare **[!UICONTROL Aggiungi]**.


1. Dopo aver aggiunto il segmento, viene visualizzato un pop-up in cui devi fornire un valore previsto per il cookie. Per questo esercizio, immetti il valore &quot;hpvisitor&quot;.

1. Seleziona **[!UICONTROL Salva]**

1. Seleziona **[!UICONTROL Fine]**
   ![Aggiungi caratteristica Audience Manager Adobe Experience Platform](assets/luma-cookie-segment-dw.png)

Il periodo di mappatura dei segmenti richiede alcune ore per essere attivato. Al termine, potrai aggiornare l&#39;interfaccia Audience Manager e vedere che l&#39;elenco **Segmenti mappati** è stato aggiornato.

## Convalidare il segmento

Poche ore dopo la creazione iniziale del segmento, puoi verificare che funzioni correttamente.

Innanzitutto, conferma di essere idoneo per il segmento

1. Apri la [home page del sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html) con mappatura sulla proprietà tag per qualificarti per il segmento appena creato.
1. Apri la scheda **Strumenti per sviluppatori** > **Rete** del browser
1. Filtra la richiesta Platform Web SDK utilizzando `interact` come filtro di testo
1. Seleziona una chiamata e apri la scheda **Anteprima** per visualizzare i dettagli della risposta
1. Espandi il **payload** per visualizzare i dettagli previsti dei cookie, come configurato in precedenza in Audience Manager. In questo esempio verrà visualizzato il nome di cookie previsto `platform_web_sdk_tutorial`.

   ![Aggiungi caratteristica Audience Manager Adobe Experience Platform](assets/segment-validate-response.jpg)

1. Apri la scheda **Applicazione** e apri **Cookie** dal menu **Archiviazione**.
1. Seleziona il dominio **`https://luma.enablementadobe.com`** e verifica che il cookie sia scritto correttamente nell&#39;elenco

   ![Aggiungi caratteristica Audience Manager Adobe Experience Platform](assets/validate-cookie.jpg)


Infine, apri il segmento nell&#39;interfaccia Audience Manager e assicurati che le **Popolazioni di segmenti** siano state incrementate:

![Aggiungi caratteristica Audience Manager Adobe Experience Platform](assets/segment-population.jpg)


Dopo aver completato questa lezione, dovresti essere in grado di vedere in che modo l’SDK web di Platform trasmette i dati a Audience Manager e puoi impostare un cookie di prime parti specifico per il segmento con una destinazione cookie.

[Successivo: ](setup-target.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [Experience League post di discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
