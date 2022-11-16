---
title: Applicare il quadro di governance dei dati
seo-title: Apply the data governance framework | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Applicare il quadro di governance dei dati
description: In questa lezione, applicherai il framework di governance dei dati ai dati che hai acquisito nella sandbox.
role: Data Architect
feature: Data Governance
kt: 4348
thumbnail: 4348-apply-data-governance-framework.jpg
exl-id: 3cc3c794-5ffd-41bf-95d8-be5bca2e3a0f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 2%

---

# Applicare il quadro di governance dei dati

<!--15min-->

In questa lezione, applicherai il framework di governance dei dati ai dati che hai acquisito nella sandbox.

La governance dei dati di Adobe Experience Platform ti consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all’utilizzo dei dati. Svolge un ruolo chiave all’interno dell’Experience Platform a vari livelli, compreso il controllo dell’utilizzo dei dati.

Prima di iniziare gli esercizi, guarda questi brevi video sulla governance dei dati:
>[!VIDEO](https://video.tv.adobe.com/v/36653?quality=12&learn=on)

>[!VIDEO](https://video.tv.adobe.com/v/29708?quality=12&learn=on)

<!--
## Permissions required

In the [Configure Permissions](configure-permissions.md) lesson, you set up all the access controls required to complete this lesson, specifically:

* Permission items **[!UICONTROL Data Governance]** > **[!UICONTROL Manage Usage Labels]**, **[!UICONTROL Manage Data Usage Policies]** and **[!UICONTROL View Data Usage Policies]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` Product Profile
-->

## Scenario aziendale

Luma fa una promessa ai membri del loro programma Fedeltà, che i dati Fedeltà non saranno condivisi con terze parti. Implementeremo questo scenario nel resto della lezione.

## Applicare etichette di governance dei dati

Il primo passaggio nel processo di governance dei dati consiste nell’applicare etichette di governance ai dati. Prima di farlo, diamo un&#39;occhiata veloce alle etichette disponibili:

1. Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Criteri]** nella navigazione a sinistra
1. Vai a **[!UICONTROL Etichette]** per visualizzare tutte le etichette nell’account.

Ci sono molte etichette pronte all&#39;uso, oltre a poter creare il proprio tramite il [!UICONTROL Crea etichetta] pulsante . Esistono tre tipi principali: [!UICONTROL Etichette per i contratti], [!UICONTROL Etichette di identità]e [!UICONTROL Etichette sensibili] che corrispondono a motivi comuni i dati potrebbero essere limitati. Ciascuna etichetta ha un [!UICONTROL Nome descrittivo] e breve [!UICONTROL Nome] che è solo un&#39;abbreviazione del tipo e un numero. Ad esempio, il [!DNL C1] l&#39;etichetta è per &quot;nessuna esportazione di terzi&quot;, che è ciò di cui abbiamo bisogno per la nostra politica di fedeltà.

![Etichetta della governance dei dati](assets/governance-policies.png)

Ora è il momento di etichettare i dati di cui vogliamo limitare l’utilizzo:

1. Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Set di dati]** nella navigazione a sinistra
1. Apri `Luma Loyalty Dataset`
1. Vai a **[!UICONTROL Governance dei dati]** scheda
1. Puoi applicare etichette ai singoli campi o all’intero set di dati. Applicheremo l’etichetta all’intero set di dati. Fai clic sull’icona della matita. Se l&#39;icona non viene visualizzata, prova a ingrandire il browser o a scorrere il pannello centrale verso destra.
   ![Governance dei dati](assets/governance-dataset.png)
1. Nel modale , espandi la **[!UICONTROL Etichette contratto]** e controlla la sezione **[!UICONTROL C2]** etichetta
1. Seleziona la **[!UICONTROL Salva modifiche]** pulsante
   ![Governance dei dati](assets/governance-applyLabel.png)
1. Torna alla pagina principale [!UICONTROL Governance dei dati] con **[!UICONTROL Mostra etichette ereditate]** attivato, puoi vedere come l’etichetta è stata applicata a tutti i campi del set di dati.
   ![Governance dei dati](assets/governance-labelsAdded.png)


<!--adding extra, unnecessary fields from field groups makes it harder to see which fields really need labels-->
<!--Are there any best practices for applying governance labels-->

## Creare criteri di governance dei dati

Ora che i nostri dati sono etichettati, possiamo creare una politica.

1. Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Criteri]** nella navigazione a sinistra
1. Nella scheda Sfoglia è già presente un criterio predefinito denominato &quot;restrizione all’esportazione di terze parti&quot; che associa l’etichetta C2 all’azione di marketing [!UICONTROL Esportazione verso terzi]- esattamente ciò di cui abbiamo bisogno!
1. Seleziona il criterio e attivalo tramite la **[!UICONTROL Stato dei criteri]** interruttore
   ![Governance dei dati](assets/governance-enablePolicy.png)

Puoi creare i tuoi criteri selezionando la **[!UICONTROL Crea criterio]** pulsante . Viene visualizzata una procedura guidata che consente di combinare più etichette e restrizioni delle azioni di marketing.

## Applicazione delle politiche di governance

L&#39;applicazione delle politiche di governance è ovviamente un elemento chiave del quadro. L’applicazione avviene a valle quando i dati vengono attivati e inviati fuori da Platform, in particolare con Real-time Customer Data Platform, che può essere concesso o meno in licenza. In entrambi i casi, non rientra nell&#39;ambito di questa esercitazione. Ma così non ti lasci appendere, puoi imparare di più su come vengono applicate le politiche in questo video, che ho messo in coda fino alla parte rilevante. Vi mostrerà anche cosa succede quando una politica viene violata.

>[!VIDEO](https://video.tv.adobe.com/v/33631/?t=151&quality=12&learn=on)


## Risorse aggiuntive

* [Documentazione sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it)
* [Riferimento API del servizio set di dati](https://www.adobe.io/experience-platform-apis/references/dataset-service/)
* [Riferimento API del servizio criteri di governance](https://www.adobe.io/experience-platform-apis/references/policy-service/)

Ora passiamo a [servizio query](run-queries.md).
