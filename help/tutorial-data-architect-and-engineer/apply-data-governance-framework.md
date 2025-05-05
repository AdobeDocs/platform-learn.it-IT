---
title: Applicare il framework di governance dei dati
seo-title: Apply the data governance framework | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Applicare il framework di governance dei dati
description: In questa lezione, applicherai il framework di governance dei dati ai dati acquisiti nella sandbox.
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-apply-data-governance-framework.jpg
exl-id: 3cc3c794-5ffd-41bf-95d8-be5bca2e3a0f
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 1%

---

# Applicare il framework di governance dei dati

<!--15min-->

In questa lezione, applicherai il framework di governance dei dati ai dati acquisiti nella sandbox.

La governance dei dati di Adobe Experience Platform consente di gestire i dati dei clienti e di garantire la conformità alle normative, alle restrizioni e alle politiche applicabili all’utilizzo dei dati. Svolge un ruolo chiave all’interno di Experience Platform a vari livelli, incluso il controllo dell’utilizzo dei dati.

Prima di iniziare gli esercizi, guarda questi brevi video sulla governance dei dati:
>[!VIDEO](https://video.tv.adobe.com/v/41161?learn=on&enablevpops&captions=ita)

>[!VIDEO](https://video.tv.adobe.com/v/35476?learn=on&enablevpops&captions=ita)

<!--
## Permissions required

In the [Configure Permissions](configure-permissions.md) lesson, you set up all the access controls required to complete this lesson, specifically:

* Permission items **[!UICONTROL Data Governance]** > **[!UICONTROL Manage Usage Labels]**, **[!UICONTROL Manage Data Usage Policies]** and **[!UICONTROL View Data Usage Policies]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` Product Profile
-->

## Scenario di business

Luma fa una promessa ai membri del loro programma di fedeltà, ossia che i dati di fedeltà non verranno condivisi con terze parti. Implementeremo questo scenario nel resto della lezione.

## Applicare le etichette di governance dei dati

Il primo passaggio nel processo di governance dei dati consiste nell’applicare etichette di governance ai dati. Prima di procedere, diamo un’occhiata alle etichette disponibili:

1. Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Criteri]** nell&#39;area di navigazione a sinistra
1. Passa alla scheda **[!UICONTROL Etichette]** per visualizzare tutte le etichette nell&#39;account.

Ci sono molte etichette pronte all&#39;uso, inoltre puoi crearne di personalizzate tramite il pulsante [!UICONTROL Crea etichetta]. Esistono tre tipi principali: [!UICONTROL Etichette contratto], [!UICONTROL Etichette identità] e [!UICONTROL Etichette riservate] che corrispondono a motivi comuni per cui i dati potrebbero essere soggetti a restrizioni. Ciascuna delle etichette ha un [!UICONTROL Nome descrittivo] e un breve [!UICONTROL Nome] che è solo un&#39;abbreviazione del tipo e un numero. Ad esempio, l&#39;etichetta [!DNL C1] è per &quot;Nessuna esportazione di terze parti&quot;, che è ciò di cui abbiamo bisogno per la nostra politica di fedeltà.

![Etichetta governance dati](assets/governance-policies.png)

Ora è il momento di etichettare i dati di cui vogliamo limitare l’utilizzo:

1. Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Set di dati]** nell&#39;area di navigazione a sinistra
1. Apri `Luma Loyalty Dataset`
1. Passa alla scheda **[!UICONTROL Governance dei dati]**
1. Puoi applicare le etichette ai singoli campi o all’intero set di dati. L’etichetta verrà applicata all’intero set di dati. Fai clic sull’icona della matita. Se l’icona non è visibile, prova ad allargare il browser o a scorrere verso destra il pannello centrale.
   ![Governance dei dati](assets/governance-dataset.png)
1. Nel modale, espandi la sezione **[!UICONTROL Etichette contratto]** e controlla l&#39;etichetta **[!UICONTROL C2]**
1. Seleziona il pulsante **[!UICONTROL Salva modifiche]**
   ![Governance dei dati](assets/governance-applyLabel.png)
1. Tornando alla schermata principale [!UICONTROL Governance dei dati], con l&#39;opzione **[!UICONTROL Mostra etichette ereditate]** attivata, puoi vedere come l&#39;etichetta è stata applicata a tutti i campi del set di dati.
   ![Governance dei dati](assets/governance-labelsAdded.png)


<!--adding extra, unnecessary fields from field groups makes it harder to see which fields really need labels-->
<!--Are there any best practices for applying governance labels-->

## Creare criteri di governance dei dati

Ora che i nostri dati sono etichettati, possiamo creare una policy.

1. Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Criteri]** nell&#39;area di navigazione a sinistra
1. Nella scheda Sfoglia è già presente un criterio predefinito denominato &quot;Restrizione all&#39;esportazione di terze parti&quot; che associa l&#39;etichetta C2 all&#39;azione di marketing [!UICONTROL Esporta a terze parti], esattamente ciò che ci serve.
1. Selezionare il criterio e abilitarlo tramite l&#39;interruttore **[!UICONTROL Stato criterio]**
   ![Governance dei dati](assets/governance-enablePolicy.png)

Puoi creare criteri personalizzati selezionando il pulsante **[!UICONTROL Crea criterio]**. Viene visualizzata una procedura guidata che consente di combinare più etichette e restrizioni alle azioni di marketing.

## Applicazione dei criteri di governance

L&#39;applicazione delle politiche di governance è ovviamente una componente chiave del quadro. L’applicazione avviene a valle quando i dati vengono attivati e inviati fuori da Platform, in particolare con Real-Time Customer Data Platform, che è possibile concedere in licenza o meno. In entrambi i casi, non rientra nell’ambito di questa esercitazione. In questo video, che ho messo in coda per vedere la parte rilevante del video, puoi imparare di più su come vengono applicate le policy. Ti mostrerà anche cosa accade quando una policy viene violata.

>[!VIDEO](https://video.tv.adobe.com/v/33631/?t=151&quality=12&learn=on&enablevpops)


## Risorse aggiuntive

* [Documentazione sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it)
* [Riferimento API servizio set di dati](https://www.adobe.io/experience-platform-apis/references/dataset-service/)
* [Riferimento API servizio criteri di governance](https://www.adobe.io/experience-platform-apis/references/policy-service/)

Passiamo ora al [servizio query](run-queries.md).
