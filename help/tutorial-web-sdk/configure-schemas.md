---
title: Creare uno schema XDM per i dati web
description: Scopri come creare uno schema XDM per i dati web nell’interfaccia di raccolta dati. Questa lezione fa parte dell’esercitazione Implementa Adobe Experience Cloud con SDK per web.
feature: Schemas
exl-id: 2858ce03-4f95-43ac-966c-1b647b33ef16
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 5%

---

# Creare uno schema XDM per i dati web

Scopri come creare uno schema XDM per i dati web nell’interfaccia di raccolta dati.

Gli schemi Experience Data Model (XDM) sono gli elementi di base, i principi e le best practice per la composizione di schemi in Adobe Experience Platform.

L’SDK per web di Platform utilizza lo schema per standardizzare i dati dell’evento web, inviarli alla rete Edge di Platform e, in ultima analisi, inoltrarli a qualsiasi applicazione Experience Cloud configurata nel datastream. Questo passaggio è fondamentale in quanto definisce un modello dati standard necessario per l’acquisizione dei dati sulla customer experience in Experience Platform e consente ai servizi e alle applicazioni a valle basati su questi standard.

>[!NOTE]
>
> A scopo dimostrativo, gli esercizi di questa lezione generano uno schema di esempio per acquisire il contenuto visualizzato e i prodotti acquistati dai clienti nel [Sito Demo Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Mentre è possibile utilizzare questi passaggi per creare uno schema diverso per scopi propri, è consigliabile seguire la creazione dello schema di esempio per apprendere le funzionalità dell’editor dello schema.

Per saperne di più sugli schemi XDM, segui il corso &quot;[Modellare i dati sulla customer experience con XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)&quot; o vedi [Panoramica del sistema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it).

## Finalità di apprendimento

Alla fine di questa lezione, potrai:

* Creare uno schema XDM dall’interfaccia di raccolta dati
* Aggiungi gruppi di campi allo schema XDM
* Creare schemi XDM per i dati degli eventi web utilizzando le best practice

## Prerequisiti

Tutti i ruoli e le autorizzazioni utente necessari per la raccolta dati e Adobe Experience Platform descritti in [Configurare le autorizzazioni](configure-permissions.md) lezione.

## Creare uno schema XDM

Gli schemi XDM sono il metodo standard per descrivere i dati in Experience Platform, consentendo il riutilizzo di tutti i dati conformi agli schemi in un’organizzazione senza conflitti o anche condivisi tra più organizzazioni. Per ulteriori informazioni, consulta la sezione [nozioni di base sulla composizione dello schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=it).

In questo esercizio, creerai uno schema XDM utilizzando i gruppi di campi della linea di base consigliati per l’acquisizione dei dati degli eventi web sul [Sito Demo Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target=&quot;_blank&quot;}:

1. Apri [Interfaccia di raccolta dati](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. Assicurati di essere nella sandbox corretta

   >[!NOTE]
   >
   >Se sei cliente di un’applicazione basata su Platform come Real-Time CDP, ti consigliamo di utilizzare una sandbox di sviluppo per questa esercitazione. In caso contrario, utilizza il **[!UICONTROL Prod]** sandbox.

1. Vai a **[!UICONTROL Schemi]** nella navigazione a sinistra
1. Seleziona la **[!UICONTROL Crea schema]** in alto a destra
1. Dal menu a discesa, seleziona **[!UICONTROL ExperienceEvent XDM]**

![Evento esperienza schema](assets/schema-XDM-experience-event.jpg)

## Aggiungi gruppi di campi

Come osservato in precedenza, XDM è il framework principale che standardizza i dati sulla customer experience fornendo strutture e definizioni comuni da utilizzare nei servizi Adobe Experience Platform a valle. Aderendo agli standard XDM, _tutti i dati sulla customer experience_ possono essere incorporati in una rappresentazione comune. Questo approccio ti consente di ottenere informazioni utili dalle azioni dei clienti, definire il pubblico dei clienti attraverso i segmenti ed esprimere gli attributi dei clienti a scopo di personalizzazione utilizzando dati provenienti da più sorgenti. Vedi [Best practice per la modellazione dei dati](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/best-practices.html?lang=en) per ulteriori informazioni.

Quando possibile, si consiglia di utilizzare i gruppi di campi esistenti e aderire a un modello agnostico del prodotto e alle convenzioni di denominazione. Per qualsiasi dato specifico della tua organizzazione che non rientri nei gruppi di campi predefiniti di cui sopra, puoi creare un gruppo di campi personalizzati. Vedi [Creazione di uno schema tramite l’Editor di schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#create) per passaggi più dettagliati sugli schemi personalizzati.

>[!TIP]
> 
>In questo esercizio, aggiungi i gruppi di campi predefiniti consigliati per la raccolta di dati web: _**[!UICONTROL ExperienceEvent AEP Web SDK]**_ e _**[!UICONTROL Evento esperienza consumatore]**_.

1. In **[!UICONTROL Gruppi di campi]** sezione , seleziona **[!UICONTROL Aggiungi]**
1. Cerca [!UICONTROL `AEP Web SDK ExperienceEvent`]
1. Seleziona la casella
1. Cerca [!UICONTROL `Consumer Experience Event`]
1. Seleziona la casella
1. Seleziona **[!UICONTROL Aggiungi gruppi di campi]**

   ![Aggiungi gruppo di campi](assets/schema-add-field-group.jpg)

Con i gruppi di campi selezionati, è possibile assegnare un nome allo schema. Una convenzione di denominazione comune per gli schemi XDM consiste nel denominare lo schema dopo l’origine dei dati:

1. Nel **[!UICONTROL Composizione**] , seleziona `Untitled schema name`
1. In **[!UICONTROL Proprietà dello schema]** , immetti **[!UICONTROL Nome visualizzato]** `Luma Web Event Data`
1. Seleziona qualsiasi elemento al di fuori del **[!UICONTROL Nome visualizzato]** campo per attivare **[!UICONTROL Salva]** opzione
1. Seleziona **[!UICONTROL Salva]**

![Dati evento web Luma](assets/schema-luma-web-event-data.png)

Con entrambi i gruppi di campi, noterai di avere accesso alle coppie chiave-valore più comunemente utilizzate richieste per la raccolta di dati sul web. La [!UICONTROL nome visualizzato] di ciascun campo viene visualizzato agli addetti al marketing nell’interfaccia di Generatore di segmenti delle applicazioni basate su Platform e puoi modificare il nome visualizzato dei campi standard in base alle tue esigenze. È inoltre possibile rimuovere i campi non desiderati. Quando fai clic sul nome di uno dei gruppi di campi, l’interfaccia evidenzia a cosa appartengono i raggruppamenti di coppie chiave-valore. Nell’esempio seguente, puoi vedere a quali gruppi appartengono **[!UICONTROL Evento esperienza consumatore]**.

![Gruppi di campi dello schema](assets/schema-consumer-experience-event.jpg)

Questa lezione è solo un punto di partenza. Quando crei uno schema di eventi web personalizzato, devi esplorare e documentare i requisiti aziendali. Questo processo è simile alla creazione di un [Documento sui requisiti aziendali](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document.html?lang=it) e [Riferimento per la progettazione della soluzione](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html) per un’implementazione Adobe Analytics, ma deve includere i requisiti per _tutti i destinatari di dati a valle_ come le destinazioni di inoltro di eventi, ad esempio Piattaforma, Target.


### Oggetto identityMap

Esiste un set speciale di dati necessari per identificare gli utenti web denominati `[!UICONTROL identityMap]`.

![Dati evento web Luma](assets/schema-identityMap.png)

Si tratta di un oggetto must-have per qualsiasi raccolta dati correlata al web, in quanto contiene l’ID Experience Cloud necessario per identificare gli utenti sul web. È anche la chiave per impostare gli ID cliente interni per gli utenti autenticati. `[!UICONTROL identityMap]` viene discusso di più in [Configurare le identità](configure-identities.md) lezione. Viene automaticamente incluso in tutti gli schemi che utilizzano **[!UICONTROL ExperienceEvent XDM]** classe.


>[!IMPORTANT]
>
> È possibile abilitare **[!UICONTROL Profilo]** per uno schema prima di salvare lo schema. **Non** attivala a questo punto. Una volta abilitato lo schema per il profilo, non può essere disabilitato o eliminato. Inoltre, i campi non possono essere rimossi dallo schema dopo questo punto. Queste implicazioni sono importanti da tenere a mente in un secondo momento quando lavori con i tuoi dati nel tuo ambiente di produzione.
>
>Questa impostazione è discussa di più durante la [Experience Platform di configurazione](setup-experience-platform.md) lezione.
>![Schema del profilo](assets/schema-profile.png)

Ora puoi fare riferimento a questo schema quando aggiungi l&#39;estensione SDK per web alla proprietà tag .


[Avanti: ](configure-identities.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nel conoscere Adobe Experience Platform Web SDK. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
