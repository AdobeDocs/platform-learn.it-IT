---
title: Migrare regole di pagina aggiuntive
description: Scopri come migrare ulteriori regole basate su pagina all’estensione Web SDK.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16764
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---


# Migrare regole di pagina aggiuntive

In questo esercizio imparerai a migrare ulteriori regole basate su pagine all’estensione Web SDK. Si tratta di un esercizio simile a quello già eseguito durante la migrazione della regola di caricamento pagina predefinita a Web SDK. I metodi sono ancora validi. La differenza maggiore è che con queste regole, non aggiungerai un’azione Invia evento, perché nella maggior parte dei casi, la regola non contiene l’azione Invia beacon di un’estensione Analytics.

## Panoramica

Effettuiamo un piccolo backup e parliamo delle implementazioni di Analytics così come sono con l’estensione tag di Adobe Analytics (nota anche come implementazione &quot;AppMeasurement&quot;, in quanto è il nome del file JavaScript).

Non suppongo di sapere esattamente come viene implementato, ma in molte implementazioni che utilizzano tag Experience Platform (precedentemente noti come &quot;Launch&quot;), esistono diverse regole che si attivano solo in modo condizionale, in base a qualcosa sulla pagina o nell’URL. Alcuni esempi:

* Regola dei risultati di ricerca, che viene attivata solo quando viene eseguita una ricerca interna e viene visualizzata la pagina dei risultati di ricerca
* Regola della pagina di destinazione della campagna, che viene attivata solo quando nell’URL è presente un codice di tracciamento
* Regola del tipo di pagina, che viene attivata solo per una pagina che è un determinato tipo di pagina, ad esempio pagina dei dettagli del prodotto, pagina del carrello acquisti, ecc.
* Qualsiasi altra pagina che viene attivata in modo condizionale

Il punto chiave è che tutti questi casi d&#39;uso attivano solo **a volte** su una pagina e **anche** si aspetta che la regola di pagina predefinita venga attivata. Pertanto, non è necessario includere un beacon di invio (estensione AA) o un evento di invio (estensione Web SDK) con una di queste regole, altrimenti verranno inseriti due hit per lo stesso caricamento di pagina.

Pertanto, queste regole creano l’oggetto, ma non inviano i dati in. Ci assicuriamo che queste regole attivino **prima** della regola di caricamento pagina predefinita, in modo che dopo la creazione dell&#39;oggetto, l&#39;azione Invia beacon/invia evento sulla regola di caricamento pagina predefinita invii tutto in. Ora, è probabile che tu sappia tutto questo, e che questo sia il modo in cui il tuo sito è configurato. Tuttavia, se sei un nuovo utente dell’implementazione o se devi &quot;correggere&quot; l’implementazione in modo che assomigli a questo metodo, questo esercizio è particolarmente utile.

## Esempio di migrazione di una regola condizionale

Di seguito è riportato un esempio di migrazione di una regola che viene attivata in modo condizionale. Utilizzerò l’esempio precedente di una pagina di destinazione della campagna. Come ho detto sopra, questo segue lo stesso pattern con cui abbiamo già lavorato nella nostra regola di pagina predefinita, tranne per il fatto che è ancora più facile perché impostiamo solo le variabili e non attiviamo hit.

1. Individua la regola condizionale. In questo esempio, troviamo la regola del codice di tracciamento della campagna e la selezioniamo.

   ![Selezione regola codice di tracciamento campagna](assets/campaign-tracking-code-rule-select.jpg)

1. All’apertura della regola, è possibile vedere che esiste una condizione per l’attivazione di questa regola in base a un parametro della stringa di query. Non è necessario modificare nulla sulla condizione, perché vogliamo solo aggiornare/migrare l’azione, non l’evento o la condizione.
1. Fai clic sull&#39;azione **Adobe Analytics - Imposta variabile**
1. Prendi nota di qualsiasi elemento impostato nell’azione. In questo esempio viene impostato **event101** e la variabile **Campaign**.

   ![evento101](assets/event101.jpg)
   ![var campagna](assets/campaign-variable.jpg)

1. Abbiamo fatto clic qui solo per fare la nota e non è necessario apportare alcuna modifica, quindi ora è sufficiente fare clic su **annulla**.
1. Crea una nuova azione facendo clic sull&#39;icona **più** nella sezione delle azioni

   ![nuova azione](assets/new-action-conditional-rule.jpg)

1. Configurare la nuova regola
   1. Selezionare **Adobe Experience Platform Web SDK** dal menu a discesa Estensione.
   1. Selezionare **Aggiorna variabile** dal menu a discesa Tipo azione.
   1. Nel pannello di destra, seleziona l&#39;oggetto **Analytics** all&#39;interno dell&#39;oggetto dati

      ![Aggiorna azione variabile](assets/configure-conditional-rule-action.jpg)

1. Ora imposta event101 e la variabile della campagna sugli stessi valori impostati nell’azione esistente.

   ![Imposta evento101](assets/web-sdk-event101.jpg)
   ![Imposta campagna](assets/web-sdk-campaign-var.jpg)

1. Ora è possibile **Mantieni le modifiche** e **Salva nella libreria** e la regola è stata migrata a Web SDK.

>[!IMPORTANT]
>
>Come la regola di caricamento pagina predefinita, abbiamo lasciato l&#39;azione **Imposta variabile** dell&#39;estensione Analytics nella regola in modo da poter confrontare i dati durante la convalida della migrazione. Non dimenticare di tornare in seguito e rimuovere l’azione dell’estensione Analytics durante la pulizia finale.



