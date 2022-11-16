---
title: Configurare Audience Manager con SDK per web di Platform
description: Scopri come configurare Adobe Audience Manager utilizzando Platform Web SDK e convalidare l’implementazione utilizzando una destinazione cookie. Questa lezione fa parte dell’esercitazione Implementa Adobe Experience Cloud con SDK per web.
solution: Data Collection, Audience Manager
exl-id: 45db48e9-73cf-4a9c-88f4-b5872a8224d3
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 3%

---

# Configurare Audience Manager con SDK per web di Platform

Scopri come configurare Adobe Audience Manager utilizzando Platform Web SDK e convalidare l’implementazione utilizzando una destinazione cookie.

[Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager.html) è la soluzione Adobe Experience Cloud che offre tutto il necessario per raccogliere informazioni rilevanti dal punto di vista commerciale sui visitatori del sito, creare segmenti commerciabili e distribuire pubblicità e contenuti mirati al pubblico giusto.


## Finalità di apprendimento

Alla fine di questa lezione, potrai:

* Configura un datastream per abilitare l’Audience Manager
* Abilitare una destinazione cookie in Audience Manager
* Convalidare l’implementazione di Audience Manager confermando la qualifica del pubblico con Adobe Experience Platform Debugger

## Prerequisiti

Per completare questa lezione, devi prima:

* Completa le lezioni precedenti nelle sezioni Configurazione iniziale e Configurazione tag di questa esercitazione.
* Accedi a Adobe Audience Manager e dispone delle autorizzazioni appropriate per creare, leggere e scrivere caratteristiche, segmenti e destinazioni. Per ulteriori informazioni, consulta [Controllo degli accessi basato sul ruolo di Audience Manager](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control.html?lang=en).

## Configurare il datastream

L’implementazione di Audience Manager tramite Platform Web SDK è diversa dall’implementazione tramite [inoltro lato server (SSF)](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html?lang=it). L&#39;inoltro lato server trasmette ad Audience Manager i dati della richiesta di Adobe Analytics. Un’implementazione Platform Web SDK trasmette ad Audience Manager i dati XDM inviati a Platform Edge Network. L’Audience Manager è abilitato nel datastream:

1. Vai a [Raccolta dati](https://experience.adobe.com/#/data-collection)Interfaccia {target=&quot;blank&quot;}
1. Nella navigazione a sinistra, seleziona **[!UICONTROL Datastreams]**
1. Seleziona il creato in precedenza `Luma Web SDK` datastream

   ![Seleziona il datastream Luma Web SDK](assets/datastream-luma-web-sdk.png)

1. Seleziona **[!UICONTROL Aggiungi servizio]**

   ![Aggiungi un servizio al datastream](assets/aam-datastream-addService.png)
1. Seleziona **[!UICONTROL Adobe Audience Manager]** come **[!UICONTROL Servizio]**
1. Conferma che **[!UICONTROL Destinazioni cookie abilitate]** e **[!UICONTROL Destinazioni URL abilitate]** sono selezionati
1. Seleziona **[!UICONTROL Salva]**

   ![Conferma le impostazioni del datastream di Audience Manager e salva](assets/aam-datastream-save.png)

## Creazione di un’origine dati

Quindi, crea un [Origine dati](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-sources/datasources-list-and-settings.html?lang=en), uno strumento fondamentale per organizzare i dati all’interno dell’Audience Manager:

1. Vai a [Audience Manager](https://experience.adobe.com/#/audience-manager/) interfaccia
1. Seleziona **[!UICONTROL Dati sul pubblico]** dalla navigazione superiore
1. Seleziona la **[!UICONTROL Origini dati]** dal menu a discesa
1. Seleziona la **[!UICONTROL Aggiungi nuovo]** pulsante nella parte superiore della pagina Origini dati

   ![Origini dati di Adobe Experience Platform Audience Manager](assets/data-sources-list.jpg)

1. Assegna all’origine dati un nome e una descrizione descrittivi. Per la configurazione iniziale, è possibile assegnare un nome`Platform Web SDK tutorial`.
1. Imposta **[!UICONTROL Tipo di ID]** a **[!UICONTROL Cookie]**
1. In **[!UICONTROL Controlli sull&#39;esportazione dei dati]** sezione , seleziona **[!UICONTROL Nessuna restrizione]**

   ![Configurazione dell’origine dati di Adobe Experience Platform Audience Manager](assets/data-source-details.png)

1. **[!UICONTROL Salva]** Origine dati


## Creare una caratteristica

Una volta salvata l&#39;Origine dati, imposta un [caratteristica](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/traits-overview.html?lang=en). Le caratteristiche sono una combinazione di uno o più segnali in Audience Manager. Crea una caratteristica per i visitatori della homepage.

>[!NOTE]
>
>Tutti i dati XDM vengono inviati ad Audience Manager se sono attivati nel datastream, tuttavia i dati potrebbero richiedere 24 ore fino a quando non saranno disponibili nel rapporto Segnali non utilizzati . Crea caratteristiche esplicite per i dati XDM che desideri utilizzare immediatamente in Audience Manager, come descritto in questo esercizio.

1. Seleziona **[!UICONTROL Dati sul pubblico]** >  **[!UICONTROL Caratteristiche]**
1. Seleziona **[!UICONTROL Aggiungi nuovo]** >  **[!UICONTROL Basato su regole]** caratteristica

   ![Caratteristica basata su regole di Adobe Experience Platform Audience Manager](assets/rule-based-trait.jpg)

1. Assegna alla tua caratteristica un nome e una descrizione descrittivi, `Luma homepage view`
1. Seleziona la **[!UICONTROL Origine dati]** creato nella sezione precedente.
1. **[!UICONTROL Selezionare una cartella]** in cui salvare le caratteristiche nel riquadro a destra. È possibile creare una cartella per **selezione dell’icona +** accanto a una cartella principale esistente. È possibile denominare questa nuova cartella `Platform Web SDK tutorial`.
1. Espandi la **[!UICONTROL Espressione caratteristica]** caret e seleziona **[!UICONTROL Generatore di espressioni]** Devi fornire una coppia di valori chiave che indica una visita alla home page.
1. Apri [Homepage Luma](https://luma.enablementadobe.com/content/luma/us/en.html) (mappata alla proprietà tag) e **Debugger SDK per web Platform** e aggiorna la pagina.
1. Per trovare la chiave e il valore del nome per la home page, controlla le richieste di rete e i dettagli dell’evento per Platform Web SDK.
   ![Dati XDM di Adobe Experience Platform Audience Manager](assets/xdm-keyvalue.jpg)
1. Torna a Generatore di espressioni nell’interfaccia utente di Audience Manager e immetti la chiave come **`web.webPageDetails.name`** e il valore **`content:luma:us:en`**. Questo passaggio ti assicura di attivare una caratteristica ogni volta che carichi la home page.
1. **[!UICONTROL Salva]** la caratteristica.


## Crea un segmento

Il passaggio successivo consiste nel creare un **segmento** e assegna le caratteristiche appena definite a questo segmento.

1. Seleziona **[!UICONTROL Dati sul pubblico]** nella navigazione superiore e seleziona **[!UICONTROL Segmenti]**
1. Seleziona **[!UICONTROL Aggiungi nuovo]** in alto a sinistra della pagina per aprire il generatore di segmenti
1. Assegna al segmento un nome e una descrizione descrittivi, ad esempio `Platform Web SDK - Homepage visitors`
1. **[!UICONTROL Selezionare una cartella]** dove il segmento verrà salvato nel riquadro a destra. È possibile creare una cartella per **selezione dell’icona +** accanto a una cartella principale esistente. È possibile denominare questa nuova cartella `Platform Web SDK tutorial`.
1. Aggiungi un codice di integrazione, che in questo caso è un set casuale di numeri. 1. **[!UICONTROL Origine dati]** sezione , seleziona **[!UICONTROL Audience Manager]** e l&#39;origine dati creata in precedenza
1. Espandi la **[!UICONTROL Caratteristiche]** e cerca la caratteristica creata
1. Seleziona **[!UICONTROL Aggiungi caratteristica]**.
1. Seleziona **[!UICONTROL Salva]** nella parte inferiore della pagina

   ![Aggiungi caratteristica Adobe Experience Platform Audience Manager](assets/add-trait-segment.jpg)

   ![Aggiungi caratteristica Adobe Experience Platform Audience Manager](assets/saved-segment.jpg)

## Creare una destinazione

Quindi, crea un **Destinazione basata su cookie** utilizzando **Generatore di destinazioni**. Il Generatore di destinazione consente di creare e gestire destinazioni da server a server, cookie, URL e .

1. Apri il Generatore di destinazioni selezionando **[!UICONTROL Destinazioni]** all&#39;interno del **Dati sul pubblico** menu nella navigazione superiore
1. Seleziona **[!UICONTROL Crea destinazione]**
1. Immettere un nome e una descrizione, `Platform Web SDK tutorial`
1. Come **[!UICONTROL Categoria]**, seleziona **[!UICONTROL Personalizzato]**
1. Come **[!UICONTROL Tipo]**, seleziona **[!UICONTROL Cookie]**

   ![Aggiungi caratteristica Adobe Experience Platform Audience Manager](assets/destination-settings.jpg)

1. Apri **[!UICONTROL Configurazione]** per inserire i dettagli sulla destinazione del cookie
1. Assegna al tuo biscotto un nome descrittivo, `platform_web_sdk_tutorial`
1. Come **[!UICONTROL Dominio cookie]**, aggiungi il dominio del sito in cui stai pianificando l’integrazione, per l’esercitazione inserisci il dominio Luma, `luma.enablementadobe.com`
1. Come **[!UICONTROL Pubblica dati in]** seleziona **[!UICONTROL Solo i domini selezionati]**
1. Seleziona il dominio se non è già stato aggiunto
1. Come **[!UICONTROL Formato dati]**, seleziona **[!UICONTROL Chiave singola]** e dai una chiave al tuo cookie. Per questo utilizzo dell&#39;esercitazione `segment` come valore chiave.
1. Infine, seleziona **[!UICONTROL Salva]** per salvare i dettagli di configurazione della destinazione.

   ![Sezione Configurazione della destinazione di Audience Manager](assets/aam-destination-config-dw.png)

<!--
   ![Adobe Experience Platform Audience Manager Add Trait](assets/aam-destination-config.jpg)


   ![Adobe Experience Platform Audience Manager Add Trait](assets/cookie-destination-config.jpg)
-->

1. In **[!UICONTROL Mappature dei segmenti]** utilizza **[!UICONTROL Ricerca e aggiunta di segmenti]** funzione per cercare la creazione precedente `Platform Web SDK - Homepage visitors` e seleziona **[!UICONTROL Aggiungi]**.


1. Una volta aggiunto il segmento, viene visualizzata una finestra a comparsa in cui è necessario fornire un valore previsto per il cookie. Per questo esercizio, inserisci il valore &quot;visitatore&quot;.

1. Seleziona **[!UICONTROL Salva]**

1. Seleziona **[!UICONTROL Fine]**

   ![Aggiungi caratteristica Adobe Experience Platform Audience Manager](assets/luma-cookie-segment-dw.png)

Il periodo di mappatura dei segmenti richiede alcune ore per essere attivato. Una volta completato, puoi aggiornare l’interfaccia di Audience Manager e visualizzare che la **Segmenti mappati** elenco aggiornato.

## Convalida il segmento

Poche ore dopo la creazione iniziale del segmento, puoi verificare che funzioni correttamente.

Innanzitutto, conferma che è possibile qualificarsi per il segmento

1. Apri [Homepage del sito dimostrativo Luma](https://luma.enablementadobe.com/content/luma/us/en.html) con mappatura sulla proprietà tag per qualificarsi per il segmento appena creato.
1. Apri il browser **strumenti per sviluppatori**  > **Rete** scheda
1. Filtrare la richiesta Platform Web SDK utilizzando `interact` come filtro di testo
1. Seleziona una chiamata e apri la **Anteprima** scheda per visualizzare i dettagli della risposta
1. Espandi la **carico utile** per visualizzare i dettagli dei cookie previsti, come precedentemente configurato in Audience Manager. In questo esempio, verrà visualizzato il nome del cookie previsto `platform_web_sdk_tutorial`.

   ![Aggiungi caratteristica Adobe Experience Platform Audience Manager](assets/segment-validate-response.jpg)

1. Apri **Applicazione** e apri **Cookie** dal **Storage** menu.
1. Seleziona la **`https://luma.enablementadobe.com`** e conferma che il cookie sia scritto in modo appropriato nell’elenco

   ![Aggiungi caratteristica Adobe Experience Platform Audience Manager](assets/validate-cookie.jpg)


Infine, apri il segmento nell’interfaccia di Audience Manager e assicurati che la **Popolazioni di segmenti** ha incrementato:

![Aggiungi caratteristica Adobe Experience Platform Audience Manager](assets/segment-population.jpg)


Dopo aver completato questa lezione, dovresti essere in grado di vedere in che modo l’SDK per web di Platform trasmette i dati all’Audience Manager e può impostare un cookie di prime parti specifico per il segmento con una destinazione cookie.

[Avanti: ](setup-target.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nel conoscere Adobe Experience Platform Web SDK. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
