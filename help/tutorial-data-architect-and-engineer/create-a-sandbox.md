---
title: Creare una sandbox
seo-title: Create a sandbox | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Creare una sandbox
description: In questa lezione verrà creato un ambiente di sviluppo sandbox da utilizzare per il resto dell’esercitazione.
role: Data Architect, Data Engineer
feature: Sandboxes
jira: KT-4348
thumbnail: 4348-create-a-sandbox.jpg
exl-id: a04afada-52a1-4812-8fa2-14be72e68614
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 2%

---

# Creare una sandbox

<!--25min-->

In questa lezione verrà creato un ambiente di sviluppo sandbox da utilizzare per il resto dell’esercitazione.

Le sandbox forniscono ambienti isolati in cui è possibile provare le funzionalità senza mescolare risorse e dati con l’ambiente di produzione. Per ulteriori dettagli, consulta la [documentazione sulle sandbox](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=it).

**Gli architetti di dati** e **i data engineer** dovranno creare delle sandbox al di fuori di questa esercitazione.

Prima di iniziare gli esercizi, guarda questo breve video per ulteriori informazioni sulle sandbox:
>[!VIDEO](https://video.tv.adobe.com/v/3430300/?learn=on&enablevpops&captions=ita)

## Autorizzazioni richieste

Nella lezione [Configurare le autorizzazioni](configure-permissions.md) è possibile impostare tutti i controlli di accesso necessari per completare la lezione.

<!--
* Permission items **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]** and **[!UICONTROL Manage Sandboxes]**
* Permission item **[!UICONTROL Sandboxes]** > **[!UICONTROL Prod]**
* User-role access to the `Luma Tutorial Platform` product profile
* Admin-level access to the `Luma Tutorial Platform` product profile
-->

## Creare una sandbox

Creiamo una sandbox:

1. Accedi all&#39;interfaccia [Adobe Experience Platform](https://experience.adobe.com/platform)
1. Vai a **[!UICONTROL Sandbox]** nel menu di navigazione a sinistra
1. Seleziona **[!UICONTROL Crea sandbox]** in alto a destra
   ![Seleziona Crea sandbox](assets/sandbox-createSandbox.png)

1. Seleziona **[!UICONTROL Sviluppo]** come **[!UICONTROL Tipo]**
1. Assegna un nome alla sandbox `luma-tutorial` (puoi aggiungere il tuo nome alla fine)
1. Assegna un titolo all&#39;esercitazione `Luma Tutorial` (provare ad aggiungere il nome alla fine)
1. Seleziona il pulsante **[!UICONTROL Crea]**
   ![Crea la sandbox](assets/sandbox-nameSandbox.png)
   >[!NOTE]
   >
   >Anche se puoi utilizzare valori arbitrari per il nome e il titolo della sandbox, si consiglia di attenersi ai valori suggeriti, poiché faremo riferimento a queste etichette durante l’esercitazione. Se nell’organizzazione sono presenti più persone che completano questa esercitazione, puoi aggiungere il tuo nome alla fine del titolo e del nome della sandbox, ad esempio luma-tutorial-ignatiusjreilly.

La creazione delle sandbox richiede circa 30 secondi, durante i quali viene visualizzato lo stato &quot;[!UICONTROL Creazione]&quot;. Una volta creata, la sandbox viene visualizzata come &quot;[!UICONTROL Attiva]&quot;:
![Stato attivo](assets/sandbox-active.png)

Attendi che la sandbox sia &quot;[!UICONTROL Attiva]&quot; prima di continuare con l&#39;esercizio successivo.

## Aggiungi la nuova sandbox al ruolo

Una volta che la sandbox è attiva, devi includerla nel tuo ruolo per poterla utilizzare. Per aggiungerlo al tuo ruolo (richiede i privilegi di amministratore di sistema o di amministratore di prodotto):

1. Vai alla schermata [!UICONTROL Autorizzazioni]
1. Apri la mansione `Luma Tutorial Platform`
1. Facoltativamente _rimuovere_ la sandbox `Prod` dal ruolo
1. Aggiungi la sandbox `Luma Tutorial`
1. Seleziona **[!UICONTROL Salva]**
1. Nella riga [!UICONTROL Sandbox], seleziona **[!UICONTROL Modifica]**

   ![Aggiungi esercitazione Luma](assets/sandbox-addLumaTutorial.png)

1. Ricarica (o ricarica con MAIUSC) la pagina. Ora dovresti trovarti nella sandbox `Luma Tutorial` o dovrebbe essere visualizzata nel menu a discesa della sandbox
1. Passa alla sandbox `Luma Tutorial` se non la stai già utilizzando

   ![Conferma Sandbox](assets/sandbox-confirmDropdown.png)

Benissimo, hai creato la sandbox e sei pronto a [configurare Developer Console e Postman](set-up-developer-console-and-postman.md)!
