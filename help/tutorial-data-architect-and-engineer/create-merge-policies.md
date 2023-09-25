---
title: Creare criteri di unione
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Creare criteri di unione
description: In questa lezione verranno creati criteri di unione per determinare il modo in cui i dati vengono uniti nei profili.
role: Data Architect, Data Engineer
feature: Profiles
jira: KT-4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 1%

---

# Creare criteri di unione

<!--20 min-->

In questa lezione verranno creati criteri di unione per assegnare la priorità all’unione di più origini dati nei profili.

Adobe Experience Platform consente di unire dati provenienti da più origini e combinarli per ottenere una visualizzazione completa di ogni singolo cliente. Quando si riuniscono questi dati, i criteri di unione determinano il modo in cui viene assegnata la priorità ai dati e quali dati vengono combinati per creare tale vista unificata.

Per questa lezione verrà utilizzata l’interfaccia utente, ma sono disponibili opzioni API anche per la creazione di criteri di unione.

**Architetti di dati** dovrà creare criteri di unione al di fuori di questa esercitazione.

Prima di iniziare gli esercizi, guarda questo breve video per ulteriori informazioni sui criteri di unione:
>[!VIDEO](https://video.tv.adobe.com/v/330433?learn=on)

## Autorizzazioni richieste

In [Configurare le autorizzazioni](configure-permissions.md) Per completare questa lezione, è necessario impostare tutti i controlli di accesso necessari.

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## Informazioni sui criteri di unione e sullo schema di unione

Forse ricordi che nella lezione sull’acquisizione in batch abbiamo caricato due record con informazioni leggermente diverse per lo stesso cliente. In [!DNL Loyalty] dati, il nome del cliente era `Daniel` e viveva in `New York City`, ma nei dati CRM il nome del cliente era `Danny` e viveva in `Portland`. I dati dei clienti cambiano nel tempo. Forse si è trasferito da `Portland` a `New York City`. Cambiano anche altre cose, come numeri di telefono e indirizzi e-mail. I criteri di unione consentono di decidere come gestire questi tipi di conflitti quando due origini dati forniscono informazioni diverse per lo stesso utente.

Allora, perché l&#39;ha fatto? `Danny` vinci come nome? Diamo un&#39;occhiata:

1. Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Profili]** nel menu di navigazione a sinistra
1. Vai a **[!UICONTROL Criteri di unione]** scheda
1. Il criterio di unione predefinito è la marca temporale ordinata. Poiché hai caricato i dati CRM dopo i dati sulla fedeltà, `Danny` ha vinto come nome nel profilo:

![schermata Criterio di unione](assets/mergepolicies-default.png)

Quando più schemi sono abilitati per il profilo, viene [!UICONTROL Schema di unione] viene creato automaticamente per tutti gli schemi di record abilitati per i profili che condividono una classe base. È possibile visualizzare [!UICONTROL Schemi di unione] passando al **[!UICONTROL Schema di unione]** scheda.

![schermata Criterio di unione](assets/mergepolicies-unionSchema.png)

Non esiste uno schema di unione per la classe ExperienceEvent. Anche se i dati ExperienceEvent arrivano ancora nel profilo, poiché si basano su serie temporali, ogni evento include una marca temporale e un ID; le collisioni non rappresentano un problema.

E se non ti piace questo criterio di unione predefinito? E se Luma decidesse che il proprio sistema CRM dovrebbe essere la fonte di verità quando c’è un conflitto? A tale scopo, verrà creato un criterio di unione.

## Creare un criterio di unione nell’interfaccia utente

1. Nella schermata Criteri di unione, seleziona la **[!UICONTROL Crea criterio di unione]** in alto a destra
1. Come **[!UICONTROL Nome]**, immetti `Loyalty Prioritized`
1. Come **[!UICONTROL Schema]**, seleziona **[!UICONTROL Profilo XDM]** la classe personalizzata, poiché si tratta di dati record, è disponibile anche per i criteri di unione.
1. Per **[!UICONTROL Unione ID]**, seleziona **[!UICONTROL Private Graph]**
1. Per **[!UICONTROL Unione attributi]**, seleziona **[!UICONTROL Precedenza set di dati]**
1. Trascinamento della selezione `Luma Loyalty Dataset` e `Luma CRM Dataset` al **[!UICONTROL Set di dati]** pannello.
1. Assicurati che `Luma Loyalty Dataset` è in alto trascinandolo e rilasciandolo sopra il `Luma CRM Dataset`
1. Seleziona il pulsante **[!UICONTROL Salva]**
   <!--do i need to explain Private Graph? Is that GA?-->
   ![Criterio di unione](assets/mergepolicies-newPolicy.png)

## Convalidare il criterio di unione

Vediamo se il criterio di unione sta facendo quello che ci aspetteremmo:

1. Vai a **[!UICONTROL Sfoglia]** scheda
1. Modificare il **[!UICONTROL Criterio di unione]** al tuo nuovo `Loyalty Prioritized` policy
1. Come **[!UICONTROL Spazio dei nomi dell’identità]**, utilizza `Luma CRM Id`
1. Come **[!UICONTROL Valore identità]** utilizzare `112ca06ed53d3db37e4cea49cc45b71e`
1. Seleziona la **[!UICONTROL Mostra profilo]** pulsante
1. `Daniel` è tornato!

![Visualizzazione di un profilo con un criterio di unione diverso](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## Creare un criterio di unione con set di dati limitati

Quando si creano criteri di unione utilizzando la precedenza dei set di dati, nel profilo vengono inclusi solo i set di dati della stessa classe base inclusi a destra. Imposta un altro criterio di unione

1. Nella schermata Criteri di unione, seleziona la **[!UICONTROL Crea criterio di unione]** in alto a destra
1. Come **[!UICONTROL Nome]**, immetti  `Loyalty Only`
1. Come **[!UICONTROL Schema]**, seleziona **[!UICONTROL Profilo XDM]**
1. Per **[!UICONTROL Unione ID]**, seleziona **[!UICONTROL Nessuno]**
1. Per **[!UICONTROL Unione attributi]**, seleziona **[!UICONTROL Precedenza set di dati]**
1. Trascina solo il `Luma Loyalty Dataset` a **[!UICONTROL Set di dati selezionato]** pannello.
1. Seleziona il pulsante **[!UICONTROL Salva]**

![Criterio di unione solo fedeltà](assets/mergepolicies-loyaltyOnly.png)

## Convalidare il criterio di unione

Vediamo ora quali sono le funzioni di questo criterio di unione:

1. Vai a **[!UICONTROL Sfoglia]** scheda
1. Modificare il **[!UICONTROL Criterio di unione]** al tuo nuovo `Loyalty Only` policy
1. Come **[!UICONTROL Spazio dei nomi dell’identità]**, utilizza `Luma CRM Id`
1. Come **[!UICONTROL Valore identità]** utilizzare `112ca06ed53d3db37e4cea49cc45b71e`
1. Seleziona la **[!UICONTROL Mostra profilo]** pulsante
1. Conferma che non è stato trovato alcun profilo:
   ![Fedeltà Solo nessuna ricerca di ID CRM.](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

ID CRM è un campo di identità in `Luma Loyalty Dataset`, ma solo le identità primarie possono essere utilizzate per cercare i profili. Quindi, cerchiamo il profilo usando l&#39;identità primaria, `Luma Loyalty Id`&quot;

1. Modificare il **[!UICONTROL Spazio dei nomi identità]** a `Luma Loyalty Id`
1. Come **[!UICONTROL Valore identità]** utilizzare `5625458`
1. Seleziona la **[!UICONTROL Mostra profilo]** pulsante
1. Seleziona l’ID profilo per aprire il profilo
1. Vai a **[!UICONTROL Attributi]** scheda
1. Altri dettagli del profilo dal set di dati CRM, come il numero di telefono cellulare e l’indirizzo e-mail, non sono disponibili perché solo
   ![I dati CRM non sono visualizzabili nel criterio Solo fedeltà](assets/mergepolicies-loyaltyOnly-attributes.png)
1. Vai a **[!UICONTROL Eventi]** scheda
1. I dati ExperienceEvent sono disponibili nonostante non siano stati inclusi esplicitamente nei set di dati dei criteri di unione:
   ![Gli eventi sono visualizzabili nel criterio Solo fedeltà](assets/mergepolicies-loyaltyOnly-events.png)

## Ulteriori informazioni sui criteri di unione

Nella ricerca del profilo, modifica il criterio di unione utilizzato in `Default Timebased` e seleziona la **[!UICONTROL Mostra profilo]** pulsante. Danny è tornato!

![Visualizzazione di un profilo con un criterio di unione diverso](assets/mergepolicies-backToDanny.png)

Cosa sta succedendo qui? Beh, l&#39;unione dei profili non è una cosa unica. I profili cliente in tempo reale vengono assemblati al volo, in base a vari fattori, tra cui il criterio di unione utilizzato. È possibile creare più criteri di unione da utilizzare in contesti diversi, a seconda della visualizzazione del cliente desiderata.

Un caso d’uso chiave per i criteri di unione è la governance dei dati. Ad esempio, supponi di acquisire in Platform dati di terze parti che non possono essere utilizzati per casi di utilizzo di personalizzazione, ma _può_ essere utilizzati per casi di utilizzo pubblicitari. Puoi creare un criterio di unione che escluda questo set di dati di terze parti e utilizzarlo per creare segmenti per i casi di utilizzo pubblicitari.

## Risorse aggiuntive

* [Documentazione sui criteri di unione](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html)
* [Riferimento API per i criteri di unione (parte di Real-time Customer Profile API)](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

Passiamo ora al [framework di governance dei dati](apply-data-governance-framework.md).
