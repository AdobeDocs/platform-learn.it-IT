---
title: Raccogliere dati del ciclo di vita
description: Scopri come raccogliere i dati del ciclo di vita in un’app mobile.
hide: true
exl-id: a3b26e45-2a17-4b44-aec0-fdf83526a273
source-git-commit: d7410a19e142d233a6c6597de92f112b961f5ad6
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 2%

---

# Raccogliere dati del ciclo di vita

Scopri come raccogliere i dati del ciclo di vita in un’app mobile.

L&#39;estensione del ciclo di vita Adobe Experience Platform Mobile SDK abilita la raccolta dei dati del ciclo di vita dalla tua app mobile. L’estensione Adobe Experience Platform Edge Network invia i dati del ciclo di vita alla rete Edge di Platform, dove vengono quindi inoltrati ad altre applicazioni e servizi in base alla configurazione dello stream di dati. Ulteriori informazioni su [Estensione del ciclo di vita](https://developer.adobe.com/client-sdks/documentation/lifecycle-for-edge-network/) nella documentazione del prodotto.


## Prerequisiti

* L&#39;app con gli SDK installati e configurati è stata creata ed eseguita correttamente. Come parte di questa lezione, hai già iniziato il monitoraggio del ciclo di vita. Consulta [Installare gli SDK - Aggiornare AppDelegate](install-sdks.md#update-appdelegate) da rivedere.
* L&#39;estensione Assurance è stata registrata come descritto in [lezione precedente](install-sdks.md).

## Finalità di apprendimento

In questa lezione verranno fornite le seguenti informazioni:

<!--
* Add lifecycle field group to the schema.
* -->
* Abilita metriche del ciclo di vita precise avviando/mettendo in pausa correttamente l’app mentre si sposta tra il primo piano e lo sfondo.
* Invia dati dall’app a Platform Edge Network.
* Convalida in Assurance.

<!--
## Add lifecycle field group to schema

The Consumer Experience Event field group you added in the [previous lesson](create-schema.md) already contains the lifecycle fields, so you can skip this step. If you don't use Consumer Experience Event field group in your own app, you can add the lifecycle fields by doing the following:

1. Navigate to the schema interface as described in the [previous lesson](create-schema.md).
1. Open the **Luma Mobile App Event Schema** schema and select **[!UICONTROL Add]** next to Field groups.
    ![select add](assets/lifecycle-add.png)
1. In the search bar, enter "lifecycle".
1. Select the checkbox next to **[!UICONTROL AEP Mobile Lifecycle Details]**.
1. Select **[!UICONTROL Add field groups]**.
    ![add field group](assets/lifecycle-lifecycle-field-group.png)
1. Select **[!UICONTROL Save]**.
    ![save](assets/lifecycle-lifecycle-save.png)
-->

## Modifiche all’implementazione

Ora puoi aggiornare il progetto per registrare gli eventi del ciclo di vita.

1. Accedi a **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]** nel Navigatore progetti Xcode.

1. Quando viene avviata, se l&#39;app sta riprendendo da uno stato in background, iOS potrebbe chiamare il tuo `sceneWillEnterForeground:` metodo delegate ed è qui che si desidera attivare un evento di avvio del ciclo di vita. Aggiungi questo codice a `func sceneWillEnterForeground(_ scene: UIScene)`:

   ```swift
   // When in foreground start lifecycle data collection
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

1. Quando l&#39;app entra in background, desideri sospendere la raccolta di dati del ciclo di vita dall&#39;app `sceneDidEnterBackground:` metodo delegate. Aggiungi questo codice a  `func sceneDidEnterBackground(_ scene: UIScene)`:

   ```swift
   // When in background pause lifecycle data collection
   MobileCore.lifecyclePause()
   ```

## Convalida con garanzia

1. Rivedi [istruzioni di configurazione](assurance.md#connecting-to-a-session) per collegare il simulatore o il dispositivo ad Assurance.
1. Invia l&#39;app in background. Controlla **[!UICONTROL LifecyclePause]** nell&#39;interfaccia utente Assurance.
1. Porta l’app in primo piano. Controlla **[!UICONTROL LifecycleResume]** nell&#39;interfaccia utente Assurance.
   ![convalida ciclo di vita](assets/lifecycle-lifecycle-assurance.png)


## Inoltrare dati a Platform Edge Network

L’esercizio precedente invia gli eventi in primo piano e in background all’SDK di Adobe Experience Platform Mobile. Per inoltrare questi eventi a Platform Edge Network:

1. Seleziona **[!UICONTROL Regole]** nella proprietà Tags.
   ![Crea regola](assets/rule-create.png)
1. Seleziona **[!UICONTROL Build iniziale]** come libreria da utilizzare.
1. Seleziona **[!UICONTROL Crea nuova regola]**.
   ![Crea nuova regola](assets/rules-create-new.png)
1. In **[!UICONTROL Crea regola]** schermata, invio `Application Status` per **[!UICONTROL Nome]**.
1. Seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Aggiungi]** sotto **[!UICONTROL EVENTI]**.
   ![Finestra di dialogo Crea regola](assets/rule-create-name.png)
1. In **[!UICONTROL Configurazione evento]** passaggio:
   1. Seleziona **[!UICONTROL Core mobile]** come **[!UICONTROL Estensione]**.
   1. Seleziona **[!UICONTROL Primo piano]** come **[!UICONTROL Tipo di evento]**.
   1. Seleziona **[!UICONTROL Mantieni modifiche]**.
      ![Configurazione evento regola](assets/rule-event-configuration.png)
1. Torna in **[!UICONTROL Crea regola]** schermata, seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Aggiungi]** accanto a **[!UICONTROL Mobile Core - Primo piano]**.
   ![Configurazione evento successivo](assets/rule-event-configuration-next.png)
1. In **[!UICONTROL Configurazione evento]** passaggio:
   1. Seleziona **[!UICONTROL Core mobile]** come **[!UICONTROL Estensione]**.
   1. Seleziona **[!UICONTROL Sfondo]** come **[!UICONTROL Tipo di evento]**.
   1. Seleziona **[!UICONTROL Mantieni modifiche]**.
      ![Configurazione evento regola](assets/rule-event-configuration-background.png)
1. Torna in **[!UICONTROL Crea regola]** schermata, seleziona ![Aggiungi](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Aggiungi]** sotto **[!UICONTROL AZIONI]**.
   ![Azione aggiunta regola](assets/rule-action-button.png)
1. In **[!UICONTROL Configurazione azione]** passaggio:
   1. Seleziona **[!UICONTROL Adobe Experience Edge Network]** come **[!UICONTROL Estensione]**.
   1. Seleziona **[!UICONTROL Inoltra evento a Edge Network]** come **[!UICONTROL Tipo di azione]**.
   1. Seleziona **[!UICONTROL Mantieni modifiche]**.
      ![Configurazione azione regola](assets/rule-action-configuration.png)
1. Seleziona **[!UICONTROL Salva nella libreria]**.
   ![Regola: salva nella libreria](assets/rule-save-to-library.png)
1. Seleziona **[!UICONTROL Genera]** per ricreare la libreria.
   ![Regola - Genera](assets/rule-build.png)

Dopo aver generato correttamente la proprietà, gli eventi vengono inviati a Platform Edge Network e vengono inoltrati ad altre applicazioni e servizi in base alla configurazione dello stream di dati.

Dovresti vedere **[!UICONTROL Chiusura applicazione (sfondo)]** e **[!UICONTROL Avvio applicazione (primo piano)]** eventi contenenti dati XDM in Assurance.

![convalida del ciclo di vita inviato a Platform Edge](assets/lifecycle-edge-assurance.png)

>[!SUCCESS]
>
>Ora hai impostato l’app per inviare eventi relativi allo stato dell’applicazione (in primo piano, in background) alla rete Edge di Adobe Experience Platform e a tutti i servizi definiti nello stream di dati.<br>Grazie per aver dedicato il tuo tempo all’apprendimento dell’SDK di Adobe Experience Platform Mobile. Se hai domande, vuoi condividere feedback generali o suggerimenti su contenuti futuri, condividili su questo [Experience League post di discussione community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Successivo: **[Tracciare i dati dell’evento](events.md)**
