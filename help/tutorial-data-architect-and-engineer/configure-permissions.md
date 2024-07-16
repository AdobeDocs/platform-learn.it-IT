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
source-wordcount: '1196'
ht-degree: 1%

---

# Configurare le autorizzazioni

<!--30min-->

In questa lezione verranno configurate le autorizzazioni utente di Adobe Experience Platform utilizzando [!DNL Adobe's Admin Console] e la schermata [!UICONTROL Autorizzazioni] nell&#39;interfaccia di Platform.

Il controllo degli accessi è una funzionalità chiave per la privacy di Experience Platform e consigliamo di limitare le autorizzazioni al minimo necessario per consentire alle persone di eseguire le proprie funzioni lavorative. Per ulteriori informazioni, vedere la [documentazione sul controllo degli accessi](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=it).

Gli architetti di dati e i data engineer sono utenti avanzati di Adobe Experience Platform e avrai bisogno di molte autorizzazioni per completare questa esercitazione e successivamente nel tuo lavoro quotidiano. Gli architetti di dati saranno probabilmente coinvolti nell&#39;amministrazione di *altri utenti di Platform* presso la propria azienda, ad esempio addetti al marketing, analisti e data scientist. Mentre completi questa lezione, pensa a come potresti utilizzare queste funzioni per gestire altri utenti della tua azienda.

**Gli architetti di dati** spesso configurano le autorizzazioni per altri utenti al di fuori di questa esercitazione.

>[!IMPORTANT]
>
>Un amministratore di sistema dei prodotti Adobe Experience Cloud deve completare alcuni dei passaggi descritti in questa lezione, descritti nei titoli delle sezioni. Se non sei l&#39;amministratore di sistema, rivolgiti a un amministratore della tua azienda e chiedi di completare queste attività. È inoltre necessario completare un&#39;attività durante la lezione [Configurazione di Developer Console e Postman](set-up-developer-console-and-postman.md).

## Informazioni sull’Admin Console

[!DNL Admin Console] è l&#39;interfaccia utilizzata per amministrare l&#39;accesso degli utenti a tutti i prodotti Adobe Experience Cloud. Per accedere a Platform, è necessario aggiungere un utente o nell’Admin Console, quindi tutti i relativi elementi di autorizzazione granulari vengono gestiti nella schermata Autorizzazioni di Adobe Experience Platform.


Di seguito è riportato un rapido riepilogo dei ruoli esistenti per Platform:

* **Gli utenti** di un profilo di prodotto possono completare attività nell&#39;interfaccia utente di Platform in base alle autorizzazioni assegnate nel profilo di prodotto.
* **Gli sviluppatori** possono creare credenziali API e progetti in Adobe Developer Console per iniziare a utilizzare Experience Platform API
* **Gli amministratori di prodotto** possono aggiungere utenti e sviluppatori al prodotto Adobe Experience Platform in Adobe Admin Console, nonché gestire l&#39;accesso utente granulare nella schermata Autorizzazioni dell&#39;interfaccia di Platform.
* **Gli amministratori di sistema** possono aggiungere gli amministratori di prodotto e amministrare essenzialmente qualsiasi autorizzazione per tutti i prodotti Adobe Experience Cloud.

## Aggiungere un utente e uno sviluppatore al profilo di prodotto `AEP-Default-All-Users` (richiede un amministratore di sistema o un amministratore di prodotto)

In questo esercizio, l’utente o l’amministratore di sistema o l’amministratore di prodotto aggiungerà l’utente come utente e sviluppatore al prodotto Adobe Experience Platform di Adobe Admin Console.

>[!NOTE]
>
>Se sei un amministratore di sistema che assiste un collega che segue questa esercitazione, puoi aggiungere il tuo collega come *amministratore di prodotto* per Adobe Experience Platform. In qualità di amministratore di prodotto, in futuro potrebbe completare questi passaggi da solo e amministrare altri utenti Experienci Platform.

Per aggiungere il partecipante all&#39;esercitazione come [!UICONTROL Utente] e [!UICONTROL Sviluppatore]:

1. Accedi a [Adobe Admin Console](https://adminconsole.adobe.com)
1. Seleziona **[!UICONTROL Prodotti]** nella navigazione superiore
1. Seleziona **Adobe Experience Platform**
   ![Seleziona Adobe Experience Platform](assets/adminconsole-experiencePlatform.png)
1. Potresti avere già diversi profili nell’istanza Experience Platform. Seleziona il profilo `AEP-Default-All-Users`
   ![Seleziona Aggiungi nuovo profilo](assets/adminconsole-newProfile.png)

1. Vai alla scheda **[!UICONTROL Utenti]**
1. Seleziona il pulsante **[!UICONTROL Aggiungi utente]**
   ![Seleziona Aggiungi utente](assets/adminconsole-addUser.png)
1. Completa il flusso di lavoro per aggiungere il partecipante all’esercitazione come utente al profilo di prodotto

1. Vai alla scheda **[!UICONTROL Sviluppatori]**
1. Seleziona il pulsante **[!UICONTROL Aggiungi sviluppatore]**
   ![Seleziona Aggiungi utente](assets/adminconsole-addDeveloper.png)
1. Completa il flusso di lavoro per aggiungere il partecipante all’esercitazione come sviluppatore al profilo di prodotto


## Aggiungere un ruolo in Adobe Experience Platform (richiede un amministratore di sistema o un amministratore di prodotto)

Le autorizzazioni granulari di Experience Platform vengono gestite nella schermata Autorizzazioni dell’interfaccia di Platform. Solo gli amministratori di sistema e di prodotto hanno accesso a questa schermata, quindi se non disponi dei privilegi di amministratore, avrai bisogno dell’assistenza di qualcuno che lo fa.

Le autorizzazioni vengono gestite in Ruoli. Crea un Ruolo per l&#39;esercitazione:

1. Accedi a [Adobe Experience Platform](https://platform.adobe.com)
1. Seleziona **[!UICONTROL Autorizzazioni]** nella barra di navigazione a sinistra per passare alla schermata [!UICONTROL Ruoli]
1. Seleziona **[!UICONTROL Crea ruolo]**

   ![Crea una mansione in Experience Platform](assets/permissions-addRole.png)
1. Assegna un nome al ruolo `Luma Tutorial Platform` (aggiungi alla fine il nome del partecipante all&#39;esercitazione, se più persone della tua azienda stanno seguendo questa esercitazione) e seleziona **[!UICONTROL Conferma]**

   ![Crea una mansione in Experience Platform](assets/permissions-nameRole.png)


1. Aggiungi tutti gli elementi di autorizzazione per le risorse seguenti utilizzando **[!UICONTROL +]** e **[!UICONTROL Aggiungi tutti]**:

   1. Modellazione dati
   1. Gestione dati
   1. Gestione profilo
   1. Identity Management
   1. Amministrazione sandbox
   1. Servizio query
   1. Raccolta dati
   1. Governance dei dati
   1. Dashboard
   1. Avvisi

      ![Aggiungi elementi autorizzazione](assets/permissions-addPermissionItems.png)

1. In Acquisizione dati, aggiungi gli elementi di autorizzazione Gestisci origini e Visualizza origini.

1. Dopo aver aggiunto tutti gli elementi di autorizzazione, assicurati di selezionare il pulsante Salva
   ![Salva elementi di autorizzazione](assets/permissions-savePermissions.png)

Effettuerai alcuni piccoli aggiornamenti a questo ruolo dopo le lezioni [Creare una sandbox](create-a-sandbox.md) e [Configurare Developer Console e Postman](set-up-developer-console-and-postman.md).

## Creare un profilo di prodotto per la raccolta dati (richiede un amministratore di sistema o un amministratore di prodotto)

In questo esercizio, tu o un amministratore di sistema della tua azienda creerete un profilo di prodotto per Data Collection (precedentemente noto come Adobe Experience Platform Launch) e vi aggiungerete come amministratore del profilo di prodotto.

>[!NOTE]
>
>Se sei un amministratore di sistema che assiste un collega in questa esercitazione, puoi aggiungerlo come *amministratore di prodotto* per la raccolta dati. In qualità di amministratore di prodotto, in futuro potrà completare questi passaggi da solo e amministrare altri utenti di Data Collection.

Per creare il profilo di prodotto:

1. In [!DNL Adobe Admin Console] vai al prodotto Raccolta dati di Adobe Experience Platform
1. Aggiungi un nuovo profilo denominato `Luma Tutorial Data Collection` (aggiungi alla fine il nome del partecipante all&#39;esercitazione, se più persone della tua azienda seguono questa esercitazione)
1. Disattiva l&#39;impostazione **[!UICONTROL Proprietà]** > **[!UICONTROL Inclusione automatica]**
1. Al momento non assegnare proprietà o autorizzazioni
1. Aggiungi il partecipante all’esercitazione come amministratore di questo profilo

Dopo aver completato questi passaggi, dovresti vedere che il profilo `Luma Tutorial Data Collection` è configurato con un amministratore.
![Profilo raccolta dati creato](assets/adminconsole-dc-profileCreated.png)

## Configurare il profilo di prodotto Raccolta dati

Ora che sei un amministratore del profilo di prodotto `Luma Tutorial Data Collection` puoi configurare le autorizzazioni e i ruoli necessari per completare l&#39;esercitazione.

### Aggiungere autorizzazioni

Ora aggiungerai i singoli elementi di autorizzazione al profilo:

1. In [Adobe Admin Console](https://adminconsole.adobe.com), vai a **[!UICONTROL Prodotti]** > **[!UICONTROL Raccolta dati]**
1. Apri il profilo `Luma Tutorial Data Collection`
1. Vai alla scheda **[!UICONTROL Autorizzazioni]**
1. Apri **[!UICONTROL piattaforme]**
1. Assicurati che tutte le piattaforme disponibili siano selezionate (è possibile visualizzare opzioni diverse in base alla licenza)
1. **[!UICONTROL Salva]** eventuali modifiche
   ![Aggiungi piattaforme](assets/adminconsole-launch-addPlatforms.png)
1. Apri **[!UICONTROL Proprietà]**
1. Assicurati che l&#39;opzione **[!UICONTROL Inclusione automatica]** sia disattivata in modo da non poter accedere ad alcuna proprietà (ne verrà aggiunta una in seguito)
1. **[!UICONTROL Salva]** eventuali modifiche
   ![Rimuovi proprietà](assets/adminconsole-launch-removeProperties.png)
1. Apri **[!UICONTROL Diritti proprietà]**
1. Seleziona **[!UICONTROL Aggiungi tutto]** per aggiungere tutte le autorizzazioni di proprietà
1. **[!UICONTROL Salva]**
   ![Rimuovi proprietà](assets/adminconsole-launch-addPropertyRights.png)
1. Apri **[!UICONTROL Diritti società]**
1. Aggiungi **[!UICONTROL Gestisci proprietà]**
1. Seleziona **[!UICONTROL Salva]**
   ![Rimuovi proprietà](assets/adminconsole-launch-companyRights.png)


### Aggiungi te stesso come utente

Ora aggiungi te stesso/a come utente al profilo di raccolta dati:

1. Vai alla scheda **[!UICONTROL Utenti]**
1. Seleziona il pulsante **[!UICONTROL Aggiungi utente]**
   ![Seleziona Aggiungi utente](assets/adminconsole-launch-addUser.png)
1. Completa il flusso di lavoro per aggiungerti come utente al profilo di prodotto

Non è necessario aggiungersi come sviluppatore per la raccolta dati.

Ora disponi di quasi tutte le autorizzazioni necessarie per completare l’esercitazione. Saranno disponibili altre due modifiche all&#39;interno di [!DNL Adobe Admin Console], inclusa una dopo la [creazione di una sandbox](create-a-sandbox.md).
