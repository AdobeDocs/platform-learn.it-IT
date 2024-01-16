---
title: Creare una regola di tag
description: Scopri come inviare un evento a Platform Edge Network con il tuo oggetto XDM utilizzando una regola di tag. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
feature: Tags
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 1%

---

# Creare una regola di tag

Scopri come inviare un evento a Platform Edge Network con il tuo oggetto XDM utilizzando una regola di tag. Una regola di tag è una combinazione di eventi, condizioni e azioni che indica alla proprietà tag di eseguire un&#39;operazione.

>[!NOTE]
>
> A scopo dimostrativo, gli esercizi di questa lezione si basano sull’esempio utilizzato durante la [Creare identità](create-identities.md) passaggio; invio di un’azione evento XDM per acquisire contenuto e identità dagli utenti sul [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html).


## Obiettivi di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Utilizza una convenzione di denominazione per gestire le regole all’interno dei tag
* Inviare un evento XDM utilizzando i tipi di azione Aggiorna variabile e Invia evento in una regola di tag
* Pubblicare una regola di tag in una libreria di sviluppo


## Prerequisiti

Conosci i tag di raccolta dati e la [Sito di dimostrazione Luma](https://luma.enablementadobe.com/content/luma/us/en.html), e aver completato le seguenti lezioni precedenti nell’esercitazione:

* [Configurare uno schema XDM](configure-schemas.md)
* [Configurare uno spazio dei nomi delle identità](configure-identities.md)
* [Configurare uno stream di dati](configure-datastream.md)
* [Estensione Web SDK installata nella proprietà tag](install-web-sdk.md)
* [Creare elementi dati](create-data-elements.md)
* [Creare identità](create-identities.md)

## Convenzioni di denominazione

Per gestire meglio le regole nei tag, si consiglia di seguire una convenzione di denominazione standard. Questa esercitazione utilizza una convenzione di denominazione in tre parti:

* [**posizione**] - [**evento**] - [**strumento**] (**sequenza**)

dove;

1. **posizione** è la pagina o le pagine del sito in cui viene attivata la regola
1. **evento** è il trigger della regola
1. **strumento** è l’applicazione o le applicazioni specifiche utilizzate nel passaggio di azione per tale regola
1. **sequenza** è l&#39;ordine in cui la regola deve essere attivata in relazione ad altre regole
<!-- minor update -->

## Crea regola di tag

Nei tag, le regole vengono utilizzate per eseguire azioni (chiamate di attivazione) in varie condizioni. L’estensione dei tag di Platform Web SDK include due azioni che verranno utilizzate in questa lezione:

* **[!UICONTROL Aggiorna variabile]** mappa gli elementi dati sui campi XDM
* **[!UICONTROL Invia evento]** invia l&#39;oggetto XDM ad Experienci Platform Edge Network

### Aggiorna variabile

Crea questa prima regola come &quot;configurazione globale&quot; per impostare tutte le variabili di contenuto essenziali nell’oggetto XDM utilizzando l’SDK web di Platform **[!UICONTROL Aggiorna variabile]** azione. Quindi crea una seconda regola, in sequenza per attivare dopo la prima, per inviare l’oggetto XDM a Platform Edge Network utilizzando **[!UICONTROL Invia evento]** azione. Più avanti in questo tutorial, invii diversi campi XDM in base al tipo di pagina su cui si trova il visitatore (ad esempio, SKU di prodotto sulle pagine dei prodotti). A tal fine, sequenziate le regole contenenti **[!UICONTROL Aggiorna variabile]** azioni prima della regola che utilizza **[!UICONTROL Invia evento]** azione.

Per creare una regola di tag:

1. Apri la proprietà tag utilizzata per questa esercitazione

1. Vai a **[!UICONTROL Regole]** nel menu di navigazione a sinistra

1. Seleziona la **[!UICONTROL Crea nuova regola]** pulsante

   ![Creare una regola](assets/rules-create.png)

1. Denomina la regola `all pages global content variables - page bottom - AA (order 1)`

1. In **[!UICONTROL Eventi]** sezione, seleziona **[!UICONTROL Aggiungi]**

   ![Denomina la regola e aggiungi un evento](assets/rule-name-new.png)

1. Utilizza il **[!UICONTROL Estensione core]** e seleziona `Page Bottom` come **[!UICONTROL Tipo di evento]**

1. Sotto **[!UICONTROL Nome]** campo, assegna un nome `Core - Page Bottom - order 1`. In questo modo è possibile descrivere il trigger con un nome significativo.

1. Seleziona **[!UICONTROL Avanzate]** a discesa e immettere `1` in **[!UICONTROL Ordine]**

   >[!NOTE]
   >
   > Maggiore è il numero immesso, più tardi nell&#39;ordine complessivo delle operazioni attivate.

1. Seleziona **[!UICONTROL Mantieni modifiche]** per tornare alla schermata principale delle regole
   ![Seleziona trigger di pagina inferiore](assets/create-tag-rule-trigger-bottom.png)

1. In **[!UICONTROL Azioni]** sezione, seleziona **[!UICONTROL Aggiungi]**

1. Come **[!UICONTROL Estensione]**, seleziona **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Come **[!UICONTROL Tipo di azione]**, seleziona **[!UICONTROL Aggiorna variabile]**

1. Come **[!UICONTROL Elemento dati]**, seleziona la `xdm.variable.content` creato in [Creare elementi dati](create-data-elements.md) lezione

   ![Aggiorna schema variabile](assets/create-rule-update-variable.png)

Ora mappa il tuo [!UICONTROL elementi dati] al [!UICONTROL schema] utilizzato dall’oggetto XDM.

>[!NOTE]
> 
> È possibile eseguire il mapping a singole proprietà o a interi oggetti. In questo esempio, esegui il mapping a singole proprietà.


1. Scorri verso il basso fino a raggiungere il **`web`** oggetto

1. Seleziona per aprirlo

1. Mappa i seguenti elementi dati al corrispondente `web` Variabili XDM

   * **`web.webPageDetials.name`** a `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** a `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** a `%page.pageInfo.hierarchie1%`

   ![Aggiorna contenuto variabile](assets/create-rule-xdm-variable-content.png)

1. Quindi, trova il `identityMap` nello schema e selezionarlo

1. Mappa su `identityMap.loginID` elemento dati

   ![Aggiorna mappa identità variabile](assets/create-rule-variable-identityMap.png)

1. Individuare quindi il campo eventType e selezionarlo

1. Inserisci il valore `web.webpagedetails.pageViews`

   >[!WARNING]
   >
   > Questo menu a discesa popola **`xdm.eventType`** variabile nell’oggetto XDM. Anche se è possibile digitare etichette in formato libero in questo campo, si consiglia di **non** in quanto ha effetti avversi con Platform.

   >[!TIP]
   >
   > Per capire quali valori compilare nel `eventType` , è necessario passare alla pagina schema e selezionare `eventType` per visualizzare i valori suggeriti nella barra a destra.

   ![Aggiorna mappa identità variabile](assets/create-tag-rule-eventType.png)


1. Seleziona **[!UICONTROL Mantieni modifiche]** e poi **[!UICONTROL Salva]** la regola nella schermata successiva per completare la creazione della regola

### Invia evento

Dopo aver impostato le variabili, puoi creare la seconda regola per inviare l’oggetto XDM a Platform Edge Network con **[!UICONTROL Invia evento]** tipo di azione.

1. A destra, seleziona per **[!UICONTROL Aggiungi regola]** per creare un&#39;altra regola

1. Denomina la regola `all pages send event - page bottom - AA (order 50)`

1. In **[!UICONTROL Eventi]** sezione, seleziona **[!UICONTROL Aggiungi]**

1. Utilizza il **[!UICONTROL Estensione core]** e seleziona `Page Bottom` come **[!UICONTROL Tipo di evento]**

1. Sotto **[!UICONTROL Nome]** campo, assegna un nome `Core - Page Bottom - order 50`. In questo modo è possibile descrivere il trigger con un nome significativo.

1. Seleziona **[!UICONTROL Avanzate]** a discesa e immettere `50` in **[!UICONTROL Ordine]**. In questo modo la seconda regola verrà attivata dopo la prima regola impostata per l’attivazione come `1`.

1. Seleziona **[!UICONTROL Mantieni modifiche]** per tornare alla schermata principale delle regole
   ![Seleziona trigger di pagina inferiore](assets/create-tag-rule-trigger-bottom-send.png)

1. In **[!UICONTROL Azioni]** sezione, seleziona **[!UICONTROL Aggiungi]**

1. Come **[!UICONTROL Estensione]**, seleziona  **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Come  **[!UICONTROL Tipo di azione]**, seleziona  **[!UICONTROL Invia evento]**

1. Come **[!UICONTROL XDM]**, seleziona la `xdm.variable.content` elemento dati creato nella lezione precedente

1. Seleziona **[!UICONTROL Mantieni modifiche]** per tornare alla schermata principale delle regole

   ![Aggiungere l’azione Invia evento](assets/create-rule-send-event-action.png)
1. Seleziona **[!UICONTROL Salva]** per salvare la regola

   ![Salva la regola](assets/create-rule-save-rule.png)

## Pubblicare la regola in una libreria

Successivamente, pubblica la regola nell&#39;ambiente di sviluppo in modo da poterne verificare il funzionamento.

Per creare una libreria:

1. Vai a **[!UICONTROL Flusso di pubblicazione]** nel menu di navigazione a sinistra

1. Seleziona **[!UICONTROL Aggiungi libreria]**

   ![Seleziona Aggiungi libreria](assets/rule-publish-library.png)
1. Per **[!UICONTROL Nome]**, immetti `Luma Web SDK Tutorial`
1. Per **[!UICONTROL Ambiente]**, seleziona `Development`
1. Seleziona  **[!UICONTROL Aggiungi tutte le risorse modificate]**

   >[!NOTE]
   >
   >    Oltre all’estensione Adobe Experience Platform Web SDK e al `all pages global content variables - page bottom - AA (order 50)` regola, puoi visualizzare i componenti tag creati nelle lezioni precedenti. L’estensione Core contiene il JavaScript di base richiesto da tutte le proprietà dei tag web.

1. Seleziona **[!UICONTROL Salva e genera per sviluppo]**

   ![Creare e generare la libreria](assets/create-tag-rule-library-changes.png)

La creazione della libreria potrebbe richiedere alcuni minuti e al termine viene visualizzato un punto verde a sinistra del nome della libreria:

![Compilazione completata](assets/create-rule-development-success.png)

Come è possibile vedere sul [!UICONTROL Flusso di pubblicazione] , il processo di pubblicazione richiede molto di più, il che va oltre l’ambito di questa esercitazione. Questo tutorial utilizza una sola libreria nell’ambiente di sviluppo.

Ora puoi convalidare i dati nella richiesta utilizzando l’Adobe Experience Platform Debugger.

[Successivo ](validate-with-debugger.md)

>[!NOTE]
>
>Grazie per aver dedicato il tuo tempo all’apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
