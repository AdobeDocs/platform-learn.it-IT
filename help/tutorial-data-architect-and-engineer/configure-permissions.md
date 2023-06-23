---
title: Configurare le autorizzazioni
seo-title: Configure permissions | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Configurare le autorizzazioni
description: In questa lezione, configurerai le autorizzazioni utente di Adobe Experience Platform utilizzando l’Admin Console di Adobe.
role: Data Architect, Data Engineer
feature: Access Control
jira: KT-4348
thumbnail: 4348-configure-permissions.jpg
exl-id: ca01f99e-f10c-4bf0-bef2-b011ac29a565
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 2%

---

# Configurare le autorizzazioni

<!--30min-->

In questa lezione, configurerai le autorizzazioni utente di Adobe Experience Platform utilizzando [!DNL Adobe's Admin Console] e [!UICONTROL Autorizzazioni] nell’interfaccia di Platform.

Il controllo degli accessi è una funzionalità chiave per la privacy di Experience Platform e consigliamo di limitare le autorizzazioni al minimo necessario per consentire alle persone di eseguire le proprie funzioni lavorative. Consulta la [Documentazione sul controllo degli accessi](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=it) per ulteriori informazioni.

Gli architetti di dati e i data engineer sono utenti avanzati di Adobe Experience Platform e avrai bisogno di molte autorizzazioni per completare questa esercitazione e successivamente nel tuo lavoro quotidiano. Gli architetti di dati sono probabilmente coinvolti nella somministrazione di *altri utenti di Platform* nella loro azienda, ad esempio addetti al marketing, analisti e data scientist. Mentre completi questa lezione, pensa a come potresti utilizzare queste funzioni per gestire altri utenti della tua azienda.

**Architetti di dati** spesso configura le autorizzazioni per altri utenti al di fuori di questa esercitazione.

>[!IMPORTANT]
>
>Un amministratore di sistema dei prodotti Adobe Experience Cloud deve completare alcuni dei passaggi descritti in questa lezione, descritti nei titoli delle sezioni. Se non sei l&#39;amministratore di sistema, rivolgiti a un amministratore della tua azienda e chiedi di completare queste attività. È inoltre necessario completare un&#39;attività durante la [Configurare Console sviluppatori e Postman](set-up-developer-console-and-postman.md) lezione.

## Informazioni sull’Admin Console

Il [!DNL Admin Console] è l’interfaccia utilizzata per amministrare l’accesso degli utenti a tutti i prodotti Adobe Experience Cloud. Per accedere a Platform, è necessario aggiungere un utente o nell’Admin Console, quindi tutti i relativi elementi di autorizzazione granulari vengono gestiti nella schermata Autorizzazioni di Adobe Experience Platform.


Di seguito è riportato un rapido riepilogo dei ruoli esistenti per Platform:

* **Utenti** di un profilo di prodotto può completare attività nell’interfaccia utente di Platform in base alle autorizzazioni assegnate nel profilo di prodotto.
* **Sviluppatori** può creare credenziali API e progetti nella console Adobe Developer, per iniziare a utilizzare l’API Experience Platform
* **Amministratori di prodotto** può aggiungere utenti e sviluppatori al prodotto Adobe Experience Platform in Adobe Admin Console, nonché gestire l’accesso granulare degli utenti nella schermata Autorizzazioni dell’interfaccia di Platform.
* **Amministratori di sistema** può aggiungere amministratori di prodotto e amministrare essenzialmente qualsiasi autorizzazione per tutti i prodotti Adobe Experience Cloud.

## Aggiungere un utente e uno sviluppatore al `AEP-Default-All-Users` profilo di prodotto (richiede un amministratore di sistema o un amministratore di prodotto)

In questo esercizio, l’utente o l’amministratore di sistema o l’amministratore di prodotto aggiungerà l’utente come utente e sviluppatore al prodotto Adobe Experience Platform di Adobe Admin Console.

>[!NOTE]
>
>Se sei un amministratore di sistema che assiste un collega che segue questa esercitazione, puoi aggiungere un collega come *Amministratore del prodotto* per Adobe Experience Platform. In qualità di amministratore di prodotto, in futuro potrebbe completare questi passaggi da solo e amministrare altri utenti Experienci Platform.

Per aggiungere il partecipante all&#39;esercitazione come [!UICONTROL Utente] e [!UICONTROL Sviluppatore]:

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com)
1. Seleziona **[!UICONTROL Prodotti]** nella navigazione superiore
1. Seleziona **Adobe Experience Platform**
   ![Seleziona Adobe Experience Platform](assets/adminconsole-experiencePlatform.png)
1. Potresti avere già diversi profili nell’istanza Experience Platform. Seleziona la `AEP-Default-All-Users` profilo
   ![Seleziona Aggiungi nuovo profilo](assets/adminconsole-newProfile.png)

1. Vai a **[!UICONTROL Utenti]** scheda
1. Seleziona la **[!UICONTROL Aggiungi utente]** pulsante
   ![Seleziona Aggiungi utente](assets/adminconsole-addUser.png)
1. Completa il flusso di lavoro per aggiungere il partecipante all’esercitazione come utente al profilo di prodotto

1. Vai a **[!UICONTROL Sviluppatori]** scheda
1. Seleziona la **[!UICONTROL Aggiungi sviluppatore]** pulsante
   ![Seleziona Aggiungi utente](assets/adminconsole-addDeveloper.png)
1. Completa il flusso di lavoro per aggiungere il partecipante all’esercitazione come sviluppatore al profilo di prodotto


## Aggiungere un ruolo in Adobe Experience Platform (richiede un amministratore di sistema o un amministratore di prodotto)

Le autorizzazioni granulari di Experience Platform vengono gestite nella schermata Autorizzazioni dell’interfaccia di Platform. Solo gli amministratori di sistema e di prodotto hanno accesso a questa schermata, quindi se non disponi dei privilegi di amministratore, avrai bisogno dell’assistenza di qualcuno che lo fa.

Le autorizzazioni vengono gestite in Ruoli. Crea un Ruolo per l&#39;esercitazione:

1. Accedi a [Adobe Experience Platform](https://platform.adobe.com)
1. Seleziona **[!UICONTROL Autorizzazioni]** nella barra di navigazione a sinistra, che consente di accedere al [!UICONTROL Ruoli] screen
1. Seleziona **[!UICONTROL Crea ruolo]**

   ![Crea un ruolo in Experience Platform](assets/permissions-addRole.png)
1. Assegna un nome al ruolo `Luma Tutorial Platform` (aggiungi alla fine il nome del partecipante all’esercitazione, se più persone della tua azienda stanno seguendo questa esercitazione) e seleziona **[!UICONTROL Conferma]**

   ![Crea un ruolo in Experience Platform](assets/permissions-nameRole.png)


1. Aggiungi tutti gli elementi di autorizzazione per le risorse seguenti utilizzando  **[!UICONTROL +]** e **[!UICONTROL Aggiungi tutto]**:

   1. Modellazione dati
   1. Gestione dati
   1. Gestione profilo
   1. Gestione identità
   1. Amministrazione sandbox
   1. Servizio query
   1. Raccolta dati
   1. Governance dei dati
   1. Dashboard
   1. Avvisi

      ![Aggiungi elementi di autorizzazione](assets/permissions-addPermissionItems.png)

1. In Acquisizione dati, aggiungi gli elementi di autorizzazione Gestisci origini e Visualizza origini.

1. Dopo aver aggiunto tutti gli elementi di autorizzazione, assicurati di selezionare il pulsante Salva
   ![Salva elementi di autorizzazione](assets/permissions-savePermissions.png)

Effettuerai alcuni piccoli aggiornamenti a questo ruolo dopo il [Creare una sandbox](create-a-sandbox.md) e [Configurare Console sviluppatori e Postman](set-up-developer-console-and-postman.md) lezioni.

## Creare un profilo di prodotto per la raccolta dati (richiede un amministratore di sistema o un amministratore di prodotto)

In questo esercizio, tu o un amministratore di sistema della tua azienda creerete un profilo di prodotto per Data Collection (precedentemente noto come Adobe Experience Platform Launch) e vi aggiungerete come amministratore del profilo di prodotto.

>[!NOTE]
>
>Se sei un amministratore di sistema che assiste un collega con questa esercitazione, puoi aggiungerli come *Amministratore del prodotto* per la raccolta dati. In qualità di amministratore di prodotto, in futuro potrà completare questi passaggi da solo e amministrare altri utenti di Data Collection.

Per creare il profilo di prodotto:

1. In [!DNL Adobe Admin Console] vai al prodotto Raccolta dati di Adobe Experience Platform
1. Aggiungi un nuovo profilo denominato `Luma Tutorial Data Collection` (aggiungi alla fine il nome del partecipante all&#39;esercitazione, se più persone della tua azienda stanno seguendo questa esercitazione)
1. Disattiva il **[!UICONTROL Proprietà]** > **[!UICONTROL Inclusione automatica]** impostazione
1. Al momento non assegnare proprietà o autorizzazioni
1. Aggiungi il partecipante all’esercitazione come amministratore di questo profilo

Dopo aver completato questi passaggi, dovresti notare che il `Luma Tutorial Data Collection` il profilo è configurato con un amministratore.
![Profilo di raccolta dati creato](assets/adminconsole-dc-profileCreated.png)

## Configurare il profilo di prodotto Raccolta dati

Ora che sei un amministratore di `Luma Tutorial Data Collection` profilo prodotto puoi configurare le autorizzazioni e i ruoli necessari per completare l’esercitazione.

### Aggiungere autorizzazioni

Ora aggiungerai i singoli elementi di autorizzazione al profilo:

1. In [Adobe Admin Console](https://adminconsole.adobe.com), vai a **[!UICONTROL Prodotti]** > **[!UICONTROL Raccolta dati]**
1. Apri `Luma Tutorial Data Collection` profilo
1. Vai a **[!UICONTROL Autorizzazioni]** scheda
1. Apri **[!UICONTROL Piattaforme]**
1. Assicurati che tutte le piattaforme disponibili siano selezionate (è possibile visualizzare opzioni diverse in base alla licenza)
1. **[!UICONTROL Salva]** eventuali modifiche
   ![Aggiungere piattaforme](assets/adminconsole-launch-addPlatforms.png)
1. Apri **[!UICONTROL Proprietà]**
1. Assicurati che le **[!UICONTROL Inclusione automatica]** l’opzione è disattivata in modo da non poter accedere ad alcuna proprietà (ne aggiungeremo una in seguito)
1. **[!UICONTROL Salva]** eventuali modifiche
   ![Rimuovi proprietà](assets/adminconsole-launch-removeProperties.png)
1. Apri **[!UICONTROL Diritti di proprietà]**
1. Seleziona **[!UICONTROL Aggiungi tutto]** per aggiungere tutte le autorizzazioni di proprietà
1. **[!UICONTROL Salva]**
   ![Rimuovi proprietà](assets/adminconsole-launch-addPropertyRights.png)
1. Apri **[!UICONTROL Diritti aziendali]**
1. Aggiungi **[!UICONTROL Gestisci proprietà]**
1. Seleziona **[!UICONTROL Salva]**
   ![Rimuovi proprietà](assets/adminconsole-launch-companyRights.png)


### Aggiungi te stesso come utente

Ora aggiungi te stesso/a come utente al profilo di raccolta dati:

1. Vai a **[!UICONTROL Utenti]** scheda
1. Seleziona la **[!UICONTROL Aggiungi utente]** pulsante
   ![Seleziona Aggiungi utente](assets/adminconsole-launch-addUser.png)
1. Completa il flusso di lavoro per aggiungerti come utente al profilo di prodotto

Non è necessario aggiungersi come sviluppatore per la raccolta dati.

Ora disponi di quasi tutte le autorizzazioni necessarie per completare l’esercitazione. Ci saranno solo due ulteriori modifiche che potrai apportare all&#39;interno del [!DNL Adobe Admin Console], incluso uno dopo di te [creare una sandbox](create-a-sandbox.md)!
