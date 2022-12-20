---
title: Creare criteri di unione
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Creare criteri di unione
description: In questa lezione verranno creati criteri di unione per determinare il modo in cui i dati vengono uniti nei profili.
role: Data Architect, Data Engineer
feature: Profiles
kt: 4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 1%

---

# Creare criteri di unione

<!--20 min-->

In questa lezione verranno creati criteri di unione per assegnare priorità alla modalità di unione di più origini dati in profili.

Adobe Experience Platform consente di unire dati provenienti da più sorgenti e combinarli per visualizzare una visione completa di ogni singolo cliente. Quando si riuniscono questi dati, i criteri di unione determinano in che modo i dati vengono definiti come priorità e quali dati vengono combinati per creare la visualizzazione unificata.

Seguiremo l’interfaccia utente di questa lezione, ma esistono anche opzioni API per la creazione di criteri di unione.

**Architetti dei dati** dovrà creare criteri di unione al di fuori di questa esercitazione.

Prima di iniziare gli esercizi, guarda questo breve video per ulteriori informazioni sui criteri di unione:
>[!VIDEO](https://video.tv.adobe.com/v/330433?quality=12&learn=on)

## Autorizzazioni necessarie

In [Configurare le autorizzazioni](configure-permissions.md) per completare la lezione, è necessario impostare tutti i controlli di accesso necessari.

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## Informazioni sui criteri di unione e lo schema di unione

Nella lezione sull’acquisizione batch, potresti ricordare che abbiamo caricato due record con informazioni leggermente diverse per lo stesso cliente. In [!DNL Loyalty] il nome del cliente era `Daniel` e viveva `New York City`, ma nei dati CRM il nome del cliente era `Danny` e viveva `Portland`. I dati del cliente cambiano nel tempo. Forse si è trasferito da `Portland` a `New York City`. Anche altre cose cambiano, come i numeri di telefono e gli indirizzi e-mail. I criteri di unione consentono di decidere come gestire questi tipi di conflitti quando due origini dati forniscono informazioni diverse per lo stesso utente.

Allora, perché? `Danny` come nome? Diamo un&#39;occhiata:

1. Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Profili]** nella navigazione a sinistra
1. Vai a **[!UICONTROL Unisci criteri]** scheda
1. Le marche temporali predefinite sono ordinate. Perché hai caricato i dati CRM dopo i dati fedeltà, `Danny` ha aggiunto come nome nel profilo:

![Schermata dei criteri di unione](assets/mergepolicies-default.png)

Quando più schemi sono abilitati per il profilo, un [!UICONTROL Schema dell&#39;unione] viene creato automaticamente per tutte le classi di base abilitate per il profilo e che condividono lo schema di record. È possibile visualizzare [!UICONTROL Regimi dell&#39;Unione] andando al **[!UICONTROL Schema dell&#39;unione]** scheda .

![Schermata dei criteri di unione](assets/mergepolicies-unionSchema.png)

Non esiste uno schema di unione per la classe ExperienceEvent. Anche se i dati ExperienceEvent arrivano ancora nel profilo perché sono basati su serie temporali, ogni evento include una marca temporale e un ID e le collisioni non sono un problema.

E se non ti piace quel criterio di unione predefinito? E se Luma decidesse che il loro sistema di gestione delle relazioni con i clienti dovrebbe essere la fonte della verità quando c&#39;è un conflitto? A questo scopo, creeremo un criterio di unione.

## Creare un criterio di unione nell’interfaccia utente

1. Nella schermata Unisci criteri , seleziona la **[!UICONTROL Crea criterio di unione]** pulsante in alto a destra
1. Come **[!UICONTROL Nome]**, inserisci `Loyalty Prioritized`
1. Come **[!UICONTROL Schema]**, seleziona **[!UICONTROL Profilo XDM]** (notare che la classe personalizzata, poiché si tratta di dati di record, è disponibile anche per i criteri di unione).
1. Per **[!UICONTROL Stitching Id]**, seleziona **[!UICONTROL Grafico privato]**
1. Per **[!UICONTROL Unione attributi]**, seleziona **[!UICONTROL Precedenza del set di dati]**
1. Trascinamento della selezione `Luma Loyalty Dataset` e `Luma CRM Dataset` al **[!UICONTROL Set di dati]** pannello.
1. Assicurati `Luma Loyalty Dataset` è in alto trascinandolo sopra il `Luma CRM Dataset`
1. Seleziona il pulsante **[!UICONTROL Salva]**
<!--do i need to explain Private Graph? Is that GA?-->
![Criteri di unione](assets/mergepolicies-newPolicy.png)

## Convalida dei criteri di unione

Vediamo se la politica di unione fa quello che ci aspetteremmo:

1. Vai a **[!UICONTROL Sfoglia]** scheda
1. Modificare la **[!UICONTROL Criteri di unione]** al nuovo `Loyalty Prioritized` policy
1. Come **[!UICONTROL Spazio dei nomi identità]**, utilizza `Luma CRM Id`
1. Come **[!UICONTROL Valore identità]** use `112ca06ed53d3db37e4cea49cc45b71e`
1. Seleziona la **[!UICONTROL Mostra profilo]** pulsante
1. `Daniel` è tornato!

![Visualizzazione di un profilo con un criterio di unione diverso](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## Creare un criterio di unione con set di dati limitati

Quando crei criteri di unione utilizzando la precedenza dei set di dati, nel profilo vengono inclusi solo i set di dati della stessa classe di base che includi a destra. Imposta un altro criterio di unione

1. Nella schermata Unisci criteri , seleziona la **[!UICONTROL Crea criterio di unione]** pulsante in alto a destra
1. Come **[!UICONTROL Nome]**, inserisci  `Loyalty Only`
1. Come **[!UICONTROL Schema]**, seleziona **[!UICONTROL Profilo XDM]**
1. Per **[!UICONTROL Stitching Id]**, seleziona **[!UICONTROL Nessuno]**
1. Per **[!UICONTROL Unione attributi]**, seleziona **[!UICONTROL Precedenza del set di dati]**
1. Solo trascinamento della selezione `Luma Loyalty Dataset` a **[!UICONTROL Set di dati selezionato]** pannello.
1. Seleziona il pulsante **[!UICONTROL Salva]**

![Criteri di unione solo fedeltà](assets/mergepolicies-loyaltyOnly.png)

## Convalida dei criteri di unione

Ora esaminiamo il funzionamento di questo criterio di unione:

1. Vai a **[!UICONTROL Sfoglia]** scheda
1. Modificare la **[!UICONTROL Criteri di unione]** al nuovo `Loyalty Only` policy
1. Come **[!UICONTROL Spazio dei nomi identità]**, utilizza `Luma CRM Id`
1. Come **[!UICONTROL Valore identità]** use `112ca06ed53d3db37e4cea49cc45b71e`
1. Seleziona la **[!UICONTROL Mostra profilo]** pulsante
1. Conferma che non è stato trovato alcun profilo:
   ![Solo fedeltà senza ricerca ID CRM.](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

L&#39;ID del sistema di gestione delle relazioni con i clienti è un campo di identità nel `Luma Loyalty Dataset`, ma solo le identità principali possono essere utilizzate per cercare i profili. Allora, cerchiamo il profilo usando l&#39;identità primaria, `Luma Loyalty Id`&quot;

1. Modificare la **[!UICONTROL Namespace Identity]** a `Luma Loyalty Id`
1. Come **[!UICONTROL Valore identità]** use `5625458`
1. Seleziona la **[!UICONTROL Mostra profilo]** pulsante
1. Seleziona l’ID profilo per aprire il profilo
1. Vai a **[!UICONTROL Attributi]** scheda
1. Tieni presente che altri dettagli del profilo dal set di dati CRM, come il numero di telefono cellulare e l’indirizzo e-mail, non sono disponibili perché solo
   ![I dati CRM non sono visualizzabili nel criterio Solo fedeltà](assets/mergepolicies-loyaltyOnly-attributes.png)
1. Vai a **[!UICONTROL Eventi]** scheda
1. I dati ExperienceEvent sono disponibili nonostante non siano stati esplicitamente inclusi nei set di dati dei criteri di unione:
   ![Gli eventi sono visualizzabili nel criterio Solo fedeltà](assets/mergepolicies-loyaltyOnly-events.png)

## Ulteriori informazioni sui criteri di unione

Nella ricerca del profilo, modifica il criterio di unione utilizzato di nuovo in `Default Timebased` e seleziona la **[!UICONTROL Mostra profilo]** pulsante . Danny è tornato!

![Visualizzazione di un profilo con un criterio di unione diverso](assets/mergepolicies-backToDanny.png)

Cosa sta succedendo qui? Beh, la fusione dei profili non è una cosa unica. I profili cliente in tempo reale vengono assemblati al volo in base a vari fattori, tra cui i criteri di unione utilizzati. È possibile creare più criteri di unione da utilizzare in contesti diversi, a seconda della visualizzazione del cliente desiderata.

Un caso d’uso chiave per i criteri di unione è la governance dei dati. Ad esempio, puoi inserire dati di terze parti in Platform che non possono essere utilizzati per casi di utilizzo di personalizzazione, ma _può_ da utilizzare per i casi di utilizzo pubblicitario. Puoi creare un criterio di unione che escluda questo set di dati di terze parti e utilizzare questo criterio di unione per creare segmenti per i casi di utilizzo pubblicitario.

## Risorse aggiuntive

* [Documentazione sui criteri di unione](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html)
* [Riferimento API dei criteri di unione (parte del Profilo API del cliente in tempo reale)](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

Ora passiamo alla [quadro di riferimento per la governance dei dati](apply-data-governance-framework.md).
