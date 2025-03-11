---
title: Tracciare gli eventi di conversione - Migrare l’implementazione di Adobe Target nell’app mobile a Adobe Journey Optimizer - Estensione Decisioning
description: Scopri come tenere traccia degli eventi di conversione di Adobe Target utilizzando l’estensione Adobe Journey Optimizer - Decisioning Mobile
exl-id: 7b53aab1-0922-4d9f-8bf0-f5cf98ac04c4
source-git-commit: 4bc5323e1f406b1fc9524838978ba8673e33b44e
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---

# Tracciare gli eventi di conversione di Target utilizzando l’estensione per dispositivi mobili Decisioning

L’obiettivo della maggior parte delle attività di Target è quello di stimolare azioni utili degli utenti nell’applicazione, come acquisti, registrazione, clic e altro ancora. Le implementazioni di Target solitamente utilizzano eventi di conversione personalizzati per monitorare queste azioni, spesso contenenti dettagli aggiuntivi sulla conversione. Gli eventi di conversione per Target possono essere tracciati con Ottimizza SDK simile a Target SDK. È necessario invocare API specifiche per tenere traccia degli eventi di conversione, come illustrato nella tabella seguente:

| Obiettivo attività | Estensione Target | Estensione Decisioning |
|---|---|---|

| Tracciare un evento di conversione della visualizzazione per una posizione mbox (ambito) | Chiama l&#39;API [displayLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} quando viene visualizzato il percorso mbox | Chiama l&#39;API [viewed](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} quando viene visualizzata l&#39;offerta per il percorso mbox. In questo modo viene inviato un evento con tipo di evento decisioning.propositionDisplay alla rete Experience Edge. |

| Tracciare un evento di conversione dei clic per una posizione mbox (ambito) | Chiama l&#39;API [clickedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} in quando si fa clic sul percorso mbox | Chiama l&#39;API [tapped](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} quando fai clic sull&#39;offerta per il percorso mbox. In questo modo viene inviato un evento con tipo di evento decisioning.propositionInteract alla rete Experience Edge. |

| Tracciare un evento di conversione personalizzato che può includere anche dati aggiuntivi, come parametri del profilo di Target e dettagli dell’ordine |Passa i dati aggiuntivi nel campo TargetParameters fornito dalle API [viewedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} e [clickedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} | Utilizza i metodi pubblici [generateDisplayInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank} e [generateTapInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank} API disponibili in Offer per il percorso mbox per generare i dati formattati XDM per la visualizzazione e fare clic rispettivamente. Quindi chiama l&#39;API [sendEvent](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#sendevent){target=_blank} di Edge SDK per inviare questi dati XDM di tracciamento insieme a eventuali dati XDM e a forma libera aggiuntivi alla rete Experience Edge. |


Successivamente, scopri come [aggiornare tipi di pubblico e script di profilo](update-audiences.md) per garantire la compatibilità con l&#39;estensione Decisioning.

>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
