---
title: Creare le modifiche di implementazione per la libreria di sviluppo
description: Scopri come creare le modifiche apportate alla libreria di sviluppo nella proprietà dei tag, in modo da poter testare i risultati sul sito web di sviluppo.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16762
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Creare le modifiche di implementazione per la libreria di sviluppo

Scopri come creare le modifiche apportate alla libreria di sviluppo nella proprietà dei tag, in modo da poter testare i risultati sul sito web di sviluppo.

Man mano che procedi con questa esercitazione, o in qualsiasi momento in cui apporti modifiche all&#39;implementazione, dovrai generare/pubblicare tali modifiche per visualizzarle nei siti di sviluppo, staging o produzione. Sono sicuro che lo hai già fatto in passato, poiché si tratta di un documento di migrazione e non di un documento di implementazione da pubblicare per la prima volta. In realtà, vorrai farlo abbastanza spesso, quando esegui ogni funzione e vuoi testarla e accertarti che funzioni correttamente, inviando i dati giusti ad Analytics.

Pertanto, in questa esercitazione saranno presenti alcuni promemoria per generare o pubblicare le modifiche. Se necessario, inserisci un segnalibro in questa pagina e non esitare a creare nella libreria di sviluppo. Puoi farlo in qualsiasi momento.

Costruiamo quello che abbiamo fatto finora. A proposito, talvolta in questa esercitazione potremmo scambiare &quot;build&quot; e &quot;publish&quot;. Ciò che è più importante è sapere se si sta &quot;creando&quot; in una libreria di sviluppo o di staging, o se si sta &quot;pubblicando&quot; nella libreria di produzione e nell&#39;ambiente, indipendentemente dalla parola utilizzata.

## Creare modifiche di migrazione allo sviluppo nei tag Experience Platform

1. Nella proprietà in Experience Platform tags, seleziona **Flusso di pubblicazione** dal menu di navigazione a sinistra, quindi aggiungi una nuova libreria.

   ![Flusso di pubblicazione](assets/publishing-flow-new-library.jpg)

1. Assegna alla libreria un nome qualsiasi, ad esempio **Initial Web SDK Migration**.
1. Selezionare l&#39;ambiente **Sviluppo**.
1. Selezionare **Aggiungi tutte le risorse modificate** per aggiungere tutti gli elementi su cui si sta lavorando.

   ![Nuova libreria](assets/new-library-websdk-migration.jpg)

1. Salva e genera in sviluppo

   ![Salva e genera in dev](assets/save-and-build-to-dev.jpg)

1. Al termine della build, potrai verificare se è stata eseguita correttamente. Passa il puntatore del mouse sul punto verde a sinistra della nuova libreria nel flusso di pubblicazione e, in effetti, se è verde, sarà stato completato correttamente.

   ![Pubblicazione completata](assets/successful-publish.jpg)

### Seleziona una libreria di lavoro

Di seguito è riportata una scorciatoia utile quando si apportano modifiche ai tag. Invece di esaminare l’intero flusso di pubblicazione ogni volta che apporti una modifica, puoi scegliere una libreria di lavoro e salvare e generare con un clic. Fallo. Mi ringrazierete più tardi.

1. Da qualsiasi punto dell’interfaccia utente dei tag, fai clic su Seleziona una libreria di lavoro in alto a destra nell’interfaccia utente e scegli quella desiderata. Per questo tutorial, scegli Initial Web SDK Migration.

   ![Seleziona la libreria di lavoro](assets/select-working-library.jpg)

