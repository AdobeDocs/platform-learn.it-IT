---
title: Creare uno schema XDM per i dati web
description: Scopri come creare uno schema XDM per i dati web nell’interfaccia di Data Collection. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK,Tags,Schemas
exl-id: 2858ce03-4f95-43ac-966c-1b647b33ef16
source-git-commit: 15bc08bdbdcb19f5b086267a6d94615cbfe1bac7
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 2%

---

# Creare uno schema XDM per i dati web


>[!CAUTION]
>
>Prevediamo di pubblicare modifiche principali a questo tutorial martedì 23 aprile 2024. Dopo questo punto molti esercizi cambieranno e potrebbe essere necessario riavviare l&#39;esercitazione dall&#39;inizio per completare tutte le lezioni.

Scopri come creare uno schema XDM per i dati web nell’interfaccia di Data Collection.

Gli schemi Experience Data Model (XDM) sono gli elementi costitutivi, i principi e le best practice per la composizione di schemi in Adobe Experience Platform.

Platform Web SDK utilizza lo schema per standardizzare i dati dell’evento web, inviarli all’Edge Network di Platform e infine inoltrarli a qualsiasi applicazione Experience Cloud configurata nello stream di dati. Questo passaggio è fondamentale in quanto definisce un modello dati standard necessario per acquisire i dati sulla customer experience in Experienci Platform e abilita servizi e applicazioni a valle basati su questi standard.

>[!NOTE]
>
> A scopo dimostrativo, gli esercizi di questa lezione creano uno schema di esempio per acquisire i contenuti visualizzati e i prodotti acquistati dai clienti in [Sito dimostrativo Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Anche se puoi utilizzare questi passaggi per creare uno schema diverso per le tue finalità, ti consigliamo di seguire prima la creazione dello schema di esempio per scoprire le funzionalità dell’editor schema.

Per ulteriori informazioni sugli schemi XDM, segui il corso &quot;[Modellare i dati sull’esperienza del cliente con XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm&amp;lang=it)&quot; o visualizzare [Panoramica del sistema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it).

## Obiettivi di apprendimento

Alla fine di questa lezione, potrai:

* Creare uno schema XDM dall’interfaccia di Data Collection
* Aggiungere gruppi di campi allo schema XDM
* Creare schemi XDM per i dati degli eventi web utilizzando le best practice

## Prerequisiti

Tutte le autorizzazioni utente e di provisioning necessarie per Data Collection e Adobe Experience Platform descritte in [Configurare le autorizzazioni](configure-permissions.md) lezione.

## Creare uno schema XDM

Gli schemi XDM sono il modo standard per descrivere i dati in Experienci Platform, consentendo a tutti i dati conformi agli schemi di essere riutilizzati in un’organizzazione senza conflitti, o anche condivisi tra più organizzazioni. Per ulteriori informazioni, consulta [Nozioni di base sulla composizione dello schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it).

In questo esercizio creerai uno schema XDM utilizzando i gruppi di campi della linea di base consigliati per l’acquisizione dei dati dell’evento web sulla [Sito dimostrativo Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}:

1. Apri [Interfaccia di Data Collection](https://launch.adobe.com/){target="_blank"}
1. Assicurati di trovarti nella sandbox corretta

   >[!NOTE]
   >
   >Se sei il cliente di un’applicazione basata su Platform come Real-Time CDP, per questa esercitazione ti consigliamo di utilizzare una sandbox di sviluppo. In caso contrario, utilizza **[!UICONTROL Prod]** sandbox.

1. Vai a **[!UICONTROL Schemi]** nel menu di navigazione a sinistra
1. Seleziona la **[!UICONTROL Crea schema]** pulsante in alto a destra
1. Dal menu a discesa, seleziona **[!UICONTROL XDM ExperienceEvent]**

![Evento esperienza schema](assets/schema-XDM-experience-event.jpg)

## Aggiungi gruppi di campi

Come indicato in precedenza, XDM è il framework principale che standardizza i dati sull’esperienza del cliente fornendo strutture e definizioni comuni da utilizzare nei servizi Adobe Experience Platform a valle. Aderendo agli standard XDM, _tutti i dati sulla customer experience_ può essere incorporata in una rappresentazione comune. Questo approccio consente di ottenere informazioni preziose dalle azioni dei clienti, definire i tipi di pubblico dei clienti attraverso i segmenti ed esprimere gli attributi dei clienti a scopo di personalizzazione utilizzando dati provenienti da più origini. Consulta [Best practice per la modellazione dei dati](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/best-practices.html?lang=en) per ulteriori informazioni.

Quando possibile, si consiglia di utilizzare i gruppi di campi esistenti e di aderire a un modello indipendente dal prodotto e alle convenzioni di denominazione. Per i dati specifici dell’organizzazione che non rientrano nei gruppi di campi predefiniti qui sopra, puoi creare un gruppo di campi personalizzato. Consulta [Creazione di uno schema tramite l’Editor di schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#create) per i passaggi più dettagliati sugli schemi personalizzati.

>[!TIP]
> 
>In questo esercizio aggiungerai i gruppi di campi predefiniti consigliati per la raccolta di dati web: _**[!UICONTROL ExperienceEvent di AEP Web SDK]**_, e _**[!UICONTROL Evento esperienza del consumatore]**_.

1. In **[!UICONTROL Gruppi di campi]** sezione, seleziona **[!UICONTROL Aggiungi]**
1. Cerca [!UICONTROL `AEP Web SDK ExperienceEvent`]
1. Seleziona la casella
1. Cerca [!UICONTROL `Consumer Experience Event`]
1. Seleziona la casella
1. Seleziona **[!UICONTROL Aggiungi gruppi di campi]**

   ![Aggiungi gruppo di campi](assets/schema-add-field-group.jpg)

Con i gruppi di campi selezionati, puoi assegnare un nome allo schema. Una convenzione di denominazione comune per gli schemi XDM consiste nel denominare lo schema dopo l’origine dei dati:

1. Nel **[!UICONTROL Composizione**] , seleziona la `Untitled schema name`
1. In **[!UICONTROL Proprietà dello schema]** , immetti il **[!UICONTROL Nome visualizzato]** `Luma Web Event Data`
1. Seleziona un elemento al di fuori del **[!UICONTROL Nome visualizzato]** campo per attivare **[!UICONTROL Salva]** opzione
1. Seleziona **[!UICONTROL Salva]**

![Dati evento web Luma](assets/schema-luma-web-event-data.png)

Con entrambi i gruppi di campi, puoi accedere alle coppie chiave-valore più comunemente utilizzate, necessarie per la raccolta di dati sul web. Il [!UICONTROL nome visualizzato] di ciascun campo viene visualizzato dagli addetti al marketing nell’interfaccia di segment builder delle applicazioni basate su Platform e puoi modificare il nome visualizzato dei campi standard in base alle tue esigenze. È inoltre possibile rimuovere i campi non desiderati. Quando fai clic sul nome di uno dei gruppi di campi, l’interfaccia evidenzia quali gruppi di coppie chiave-valore appartengono ad esso. Nell’esempio seguente, puoi vedere a quali gruppi appartengono **[!UICONTROL Evento esperienza del consumatore]**.

![Gruppi di campi schema](assets/schema-consumer-experience-event.jpg)

Questa lezione è solo un punto di partenza. Quando crei uno schema di eventi web personalizzato, devi esplorare e documentare i requisiti aziendali. Questo processo è simile alla creazione di un’ [Documento sui requisiti aziendali](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document.html?lang=it) e [Guida di riferimento per la progettazione della soluzione](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html) per un’implementazione di Adobe Analytics, ma devono includere i requisiti per _tutti i destinatari di dati a valle_ ad esempio Platform, Target e le destinazioni di inoltro degli eventi.


### Oggetto identityMap

Per identificare gli utenti web è necessario uno speciale set di dati denominato `[!UICONTROL identityMap]`.

![Dati evento web Luma](assets/schema-identityMap.png)

Si tratta di un oggetto obbligatorio per qualsiasi raccolta di dati relativi al web, in quanto ospita l’ID Experience Cloud richiesto per identificare gli utenti sul web. È anche la chiave per impostare gli ID cliente interni per gli utenti autenticati. `[!UICONTROL identityMap]` viene discusso ulteriormente in [Configurare le identità](configure-identities.md) lezione. Viene incluso automaticamente in tutti gli schemi utilizzando **[!UICONTROL XDM ExperienceEvent]** classe.


>[!IMPORTANT]
>
> È possibile abilitare **[!UICONTROL Profilo]** per uno schema prima di salvarlo. **Do not** attivala a questo punto. Una volta che uno schema è abilitato per il profilo, non può essere disabilitato o eliminato. Inoltre, i campi non possono essere rimossi dallo schema dopo questo punto. Queste implicazioni sono importanti da tenere presenti in un secondo momento quando si lavora con i propri dati nell’ambiente di produzione.
>
>Questa impostazione viene discussa ulteriormente durante il [Experience Platform di configurazione](setup-experience-platform.md) lezione.
>![Schema profilo](assets/schema-profile.png)

Ora puoi fare riferimento a questo schema quando aggiungi l’estensione Web SDK alla proprietà tag.


[Successivo: ](configure-identities.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
