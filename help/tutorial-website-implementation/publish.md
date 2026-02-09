---
title: Pubblicare la proprietà tag
description: Scopri come pubblicare la proprietà tag dall’ambiente di sviluppo agli ambienti di staging e produzione. Questa lezione fa parte dell’esercitazione Implementare Experience Cloud nei siti web.
exl-id: dec70472-cecc-4630-b68e-723798f17a56
source-git-commit: 1fc027db2232c8c56de99d12b719ec10275b590a
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 55%

---

# Pubblicare la proprietà tag

Ora che hai implementato alcune soluzioni chiave di Adobe Experience Cloud nell’ambiente di sviluppo, è ora di imparare il flusso di lavoro di pubblicazione.


>[!WARNING]
>
> Il sito web Luma utilizzato in questa esercitazione dovrebbe essere sostituito durante la settimana del 16 febbraio 2026. Il lavoro svolto come parte di questo tutorial potrebbe non essere applicabile al nuovo sito web.

>[!NOTE]
>
>Adobe Experience Platform Launch viene integrato in Adobe Experience Platform come suite di tecnologie per la raccolta dati. Nell’interfaccia sono state introdotte diverse modifiche terminologiche di cui tenere conto quando si utilizza questo contenuto:
>
> * Platform Launch (lato client) è ora **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it)**
> * Platform Launch Server Side è ora **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Le configurazioni di Edge sono ora **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=it)**

## Finalità di apprendimento

Alla fine di questa lezione, potrai:

1. Pubblicare una libreria di sviluppo nell’ambiente di staging
1. Mappare una libreria di staging al sito web di produzione utilizzando il debugger
1. Pubblicare una libreria di sviluppo nell&#39;ambiente di produzione

## Pubblicare nell&#39;ambiente di staging

Ora che hai creato e convalidato la libreria nell’ambiente di sviluppo, è necessario pubblicarla nell’ambiente di staging.

1. Vai alla pagina **[!UICONTROL Flusso di pubblicazione]**

1. Apri il menu a discesa accanto alla libreria e seleziona **[!UICONTROL Invia per approvazione]**

   ![Invia per approvazione](images/publishing-submitForApproval.png)

1. Fai clic sul pulsante **[!UICONTROL Invia]** nella finestra di dialogo:

   ![Clic su Invia nella finestra modale](images/publishing-submit.png)

1. La libreria verrà ora visualizzata nella colonna [!UICONTROL Inviato] in uno stato non generato:

1. Apri il menu a discesa e seleziona **[!UICONTROL Build per staging]**:

   ![Generazione per staging](images/publishing-buildForStaging.png)

1. Quando l&#39;icona del puntino diventa verde, la libreria può essere visualizzata in anteprima nell&#39;ambiente di staging.

In uno scenario reale, il passaggio successivo nel processo in genere consisterebbe nel far sì che il team di QA convalidi le modifiche nella libreria di staging. Questo è possibile utilizzando il debugger.

**Convalidare le modifiche nella libreria di staging**

1. Nella proprietà tag, apri la pagina [!UICONTROL Ambienti]

1. Nella riga [!UICONTROL Staging], fai clic sull’icona ![icona Installa](images/launch-installIcon.png) per aprire il modale

   ![Vai alla pagina Ambienti e fai clic per aprire il modale](images/publishing-getStagingCode.png).

1. Fai clic sull’icona Copia ![icona Copia](images/launch-copyIcon.png) per copiare il codice da incorporare negli Appunti

1. Fai clic su **[!UICONTROL Chiudi]** per chiudere il modale

   ![Icona di installazione](images/publishing-copyStagingCode.png)

1. Apri il [sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html) nel browser Chrome

1. Apri l&#39;estensione [Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) facendo clic sull&#39;icona ![icona Debugger](images/icon-debugger.png)

   ![Fai clic sull’icona Debugger](images/switchEnvironments-openDebugger.png)

1. Passa alla scheda Strumenti

1. Nella sezione **[!UICONTROL Adobe Launch > Replace Launch Embed Code]** incolla il codice di incorporamento di staging presente negli Appunti
1. Attiva l&#39;opzione **[!UICONTROL Applica in luma.enablementadobe.com]**

1. Fai clic sull’icona del disco per salvare

   ![ambiente tag visualizzato in Debugger](images/switchEnvironments-debugger-save.png)

1. Ricarica e controlla la scheda Riepilogo del debugger. Nella sezione Launch, dovresti vedere che la proprietà di staging è implementata, con il nome della tua proprietà visualizzato (ad esempio, &quot;esercitazione sui tag&quot; o qualsiasi altro nome assegnato alla proprietà).

   ![ambiente tag visualizzato in Debugger](images/publishing-debugger-staging.png)

In uno scenario, dopo che il team di QA ha dato l’approvazione esaminando le modifiche nell’ambiente di staging, è ora di pubblicare in produzione.

## Pubblicare in produzione

1. Passa alla pagina [!UICONTROL Pubblicazione]

1. Dal menu a discesa, fai clic su **[!UICONTROL Approva per la pubblicazione]**:

   ![Approva per la Pubblicazione](images/publishing-approveForPublishing.png)

1. Fai clic sul pulsante **[!UICONTROL Approva]** nella finestra di dialogo:

   ![Clic su Approva](images/publishing-approve.png)

1. La libreria verrà ora visualizzata nella colonna [!UICONTROL Approvato] in uno stato non generato (punto giallo):

1. Apri il menu a discesa e seleziona **[!UICONTROL Genera e pubblica in produzione]**:

   ![Clic su Genera e pubblica in Produzione](images/publishing-buildAndPublishToProduction.png)

1. Fai clic su **[!UICONTROL Pubblica]** nella finestra di dialogo:

   ![Clic su Pubblica](images/publishing-publish.png)

1. La libreria verrà ora visualizzata nella colonna [!UICONTROL Pubblicato]:

   ![Pubblicato](images/publishing-published.png)

Tutto qui. Hai completato l’esercitazione e hai pubblicato la tua prima proprietà nei tag.
