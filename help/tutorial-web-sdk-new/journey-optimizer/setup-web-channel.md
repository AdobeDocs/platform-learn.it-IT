---
title: Configurare un canale web con Platform Web SDK
description: Scopri come implementare il canale web utilizzando Platform Web SDK. Questa lezione fa parte dell’esercitazione Implementare Adobe Experience Cloud con Web SDK.
solution: Data Collection,Experience Platform,Journey Optimizer
feature-set: Journey Optimizer
feature: Web Channel,Web SDK
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '2463'
ht-degree: 0%

---


# Configurare un canale web con Platform Web SDK

Scopri come implementare il canale web utilizzando Platform Web SDK. Questa guida descrive i prerequisiti fondamentali per il canale web, i passaggi dettagliati per la configurazione e un approfondimento del caso d’uso incentrato sullo stato di fedeltà.

Seguendo questa guida, gli utenti di Journey Optimizer sono in grado di applicare in modo efficace il canale web per la personalizzazione online avanzata utilizzando Journey Optimizer Web Designer.

## Finalità di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Comprendi la funzione e il significato di Web SDK nella distribuzione dell’esperienza del canale web.
* Comprendi il processo di creazione di una campagna per canale web dall’inizio alla fine utilizzando il caso d’uso dei premi fedeltà Luma di esempio.
* Configura le proprietà, le azioni e le pianificazioni della campagna all’interno dell’interfaccia.
* Scopri le funzionalità e i vantaggi dell’estensione Adobe Experience Cloud Visual Editing Helper.
* Scopri come modificare il contenuto delle pagine web, incluse immagini, intestazioni e altri elementi, utilizzando Progettazione web.
* Scopri come inserire le offerte in una pagina web utilizzando il componente Decisione offerta.
* Acquisisci familiarità con le best practice per garantire la qualità e il successo di una campagna canale web.

## Prerequisiti

Per completare le lezioni in questa sezione, devi prima:

* Assicurati che la versione dell’SDK per web di AEP sia 2.16 o successiva.
* Se utilizzi Journey Optimizer Web Designer per creare la tua esperienza di canale web, assicurati di utilizzare i browser Google Chrome o Microsoft® Edge.
* Verifica inoltre di aver scaricato l’estensione del browser Adobe Experience Cloud Visual Editing Helper. Abilita l’estensione del browser Helper per editing video nella barra degli strumenti del browser prima di creare l’esperienza del canale web.
   * In Journey Optimizer Web Designer, alcuni siti Web potrebbero non essere aperti in modo affidabile per uno dei motivi seguenti:
      1. Il sito web dispone di criteri di sicurezza rigorosi.
      1. Il sito web è incorporato in un iframe.
      1. Il sito per il controllo qualità o il sito di staging del cliente non è accessibile esternamente (è un sito interno).
* Assicurati che i cookie di terze parti siano consentiti nel browser. Potrebbe essere necessario disattivare anche i blocchi degli annunci nel browser.
* Durante la creazione di esperienze web e l’inclusione di contenuto dalla libreria Adobe Experience Manager Assets Essentials, è necessario configurare il sottodominio per la pubblicazione di questo contenuto. [Ulteriori informazioni](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/web-delegated-subdomains.html?lang=en).
* Se utilizzi la funzione di sperimentazione dei contenuti, assicurati che il set di dati web sia incluso anche nella configurazione di reporting.
* Attualmente, sono supportati due tipi di implementazioni per abilitare l’authoring e la distribuzione di campagne canale web sulle proprietà web:
   * Solo lato client: per modificare il sito web, è necessario implementare Adobe Experience Platform Web SDK.
   * Modalità ibrida: puoi utilizzare l’API server di AEP Edge Network per richiedere la personalizzazione lato server. La risposta dell’API viene quindi fornita a Adobe Experience Platform Web SDK per il rendering delle modifiche sul lato client. Per ulteriori informazioni, consultare la documentazione relativa all&#39;API del server di rete Edge di Adobe Experience Platform. Ulteriori dettagli ed esempi di implementazione per la modalità ibrida sono disponibili in questo post di blog.

>[!NOTE]
>
>L’implementazione solo lato server non è attualmente supportata.

## Terminologia

Innanzitutto, devi comprendere la terminologia utilizzata nelle campagne del canale web.

* **Canale web**: mezzo di comunicazione o per la distribuzione di contenuti tramite web. Nel contesto di questa guida, si riferisce al meccanismo attraverso il quale i contenuti personalizzati vengono consegnati ai visitatori del sito web utilizzando Platform Web SDK, all’interno di Adobe Journey Optimizer.
* **Superficie web**: si riferisce a una proprietà web identificata da un URL in cui viene distribuito il contenuto. Può includere una o più pagine web.
* **Journey Optimizer Web Designer**: strumento o interfaccia specifica all’interno di Journey Optimizer che consente agli utenti di progettare le esperienze dei canali web.
* **Helper per editing video Adobe Experience Cloud**: estensione del browser per la modifica visiva e la progettazione delle esperienze del canale web.
* **Datastream**: configurazione all’interno del servizio Adobe Experience Platform che consente di fornire esperienze del canale web.
* **Criterio di unione**: configurazione che assicura l’attivazione e la pubblicazione accurate delle campagne in entrata.
* **Pubblico**: segmento specifico di utenti o visitatori del sito che soddisfano determinati criteri.
* **Designer web**: interfaccia o strumento per la modifica visiva e la progettazione di esperienze web senza immergersi nel codice.
* **Editor espressioni**: strumento all’interno di Web Designer che consente agli utenti di aggiungere personalizzazioni al contenuto web, potenzialmente in base ad attributi di dati o altri criteri.
* **Componente decisione offerta**: componente di Web Designer che consente di decidere quale offerta è più adatta per essere visualizzata da un visitatore specifico in base alla gestione delle decisioni.
* **Esperimento contenuti**: metodo per testare diverse varianti di contenuto e individuare quella che offre le migliori prestazioni in termini di metrica desiderata, ad esempio i clic in entrata.
* **Trattamento**: nel contesto degli esperimenti sui contenuti, un trattamento si riferisce a una specifica variante di contenuto in fase di test rispetto a un’altra.
* **Simulazione**: meccanismo di anteprima per visualizzare l’esperienza del canale web prima di attivarla per i tipi di pubblico live.

## Configurare lo stream di dati

Assicurati che all’interno del servizio Adobe Experience Platform sia definito uno stream di dati e che l’opzione Adobe Journey Optimizer sia abilitata. Questa deve essere configurata prima che l’SDK web di Platform possa distribuire qualsiasi esperienza di canale web.

Per configurare Adobe Journey Optimizer nello stream di dati:

1. Passa all’interfaccia di Data Collection.
1. Nel menu di navigazione a sinistra, seleziona **Flussi di dati**.
1. Seleziona lo stream di dati Luma Web SDK creato in precedenza.

   ![Seleziona flusso di dati](../assets/web-channel-select-datastream.png)

1. Seleziona **Modifica** all&#39;interno del servizio Adobe Experience Platform.

   ![Modifica flusso di dati](../assets/web-channel-edit-datastream.png)

1. Controlla la **Adobe Journey Optimizer** casella.

   ![Casella Seleziona AJO](../assets/web-channel-check-ajo-box.png)

1. Seleziona **Salva**.

In questo modo gli eventi in entrata per Journey Optimizer vengono gestiti correttamente da Adobe Experience Platform Edge.

## Configurare il criterio di unione

Assicurati che un criterio di unione sia definito con **Criterio di unione Attivo su Edge** opzione abilitata. Questa opzione dei criteri di unione viene utilizzata dai canali in entrata di Journey Optimizer per garantire l’attivazione e la pubblicazione accurate delle campagne in entrata sul server Edge di.

Per configurare l’opzione nel criterio di unione:

1. Vai a **Cliente > Profili** di rete.
1. Nell’area di navigazione, seleziona **Criteri di unione**.
1. Seleziona il criterio e attiva/disattiva **Criterio di unione Attivo su Edge** all&#39;interno del **Configura** passaggio.

   ![Attiva/disattiva criterio di unione](..//assets/web-channel-active-on-edge-merge-policy.png)

## Configurare il set di dati web per la sperimentazione dei contenuti

Per utilizzare esperimenti sui contenuti nelle campagne per canali web, devi assicurarti che il set di dati web utilizzato sia incluso anche nella configurazione di reporting. Il sistema di reporting di Journey Optimizer utilizza il set di dati in modalità di sola lettura per popolare i rapporti di sperimentazione sui contenuti OOTB.

[L’aggiunta di set di dati per il reporting degli esperimenti sui contenuti è descritta in questa sezione](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/content-experiment/reporting-configuration.html?lang=en#add-datasets).

## Panoramica del caso d’uso: premi fedeltà

In questa lezione, un esempio di caso di utilizzo dei premi fedeltà viene utilizzato per descrivere nel dettaglio l’implementazione di un’esperienza di canale web utilizzando l’SDK per web.

Questo caso d’uso consente di comprendere meglio in che modo Journey Optimizer può contribuire a fornire ai clienti le migliori esperienze in entrata, utilizzando le campagne Journey Optimizer e Web Designer.

>[!NOTE]
>
>Poiché questo tutorial è destinato agli implementatori, vale la pena notare che questa lezione richiede un notevole lavoro sull’interfaccia utente in AJO. Anche se tali attività di interfaccia utente sono in genere gestite dagli esperti di marketing, può essere utile che i responsabili dell’implementazione possano ottenere informazioni approfondite sul processo, anche se alla fine non sono responsabili della creazione delle campagne per i canali web.

### Crea campagna di premi fedeltà

Iniziamo con la creazione della campagna per il canale web dei Premi fedeltà in Adobe Journey Optimizer.

Per creare la campagna di esempio:

1. Passa a Gestione Percorsi > Campagne nel menu di navigazione a sinistra
1. Clic **Crea campagna** in alto a destra.
1. In **Proprietà** , specifica come eseguire la campagna. Per il caso d’uso Premi fedeltà, scegli **Pianificato**.

   ![Campagna pianificata](../assets/web-channel-campaign-properties-scheduled.png)

1. In **Azioni** , scegli il **Canale web**. In questa fase, scegliere anche la superficie Web.

>[!NOTE]
>
>Una superficie web si riferisce a una proprietà web identificata da un URL in cui viene distribuito il contenuto. Può corrispondere a un URL di pagina singola o comprendere più pagine, consentendo di applicare modifiche su una o più pagine web.

Scegli la **URL della pagina** opzione superficie web per distribuire l’esperienza su una pagina per questa campagna. Immetti l’URL per la pagina Luma.

1. Una volta definita la superficie web, seleziona **Crea**.

   ![Seleziona la superficie web](../assets/web-channel-web-surface.png)

1. Ora aggiungi alcuni dettagli aggiuntivi alla nuova campagna per canali web. Innanzitutto, assegna un nome alla campagna. Chiamatela &#39;*Premi fedeltà Luma - Stato oro - Ottobre 2023*&quot;. Facoltativamente, puoi aggiungere una descrizione alla campagna. Aggiungi anche **Tag** migliorare la tassonomia complessiva della campagna.

   ![Assegna un nome alla campagna](../assets/web-channel-campaign-name.png)

1. Per impostazione predefinita, la campagna è attiva per tutti i visitatori del sito. Ai fini di questo caso d’uso, solo i membri che ricevono un premio in oro devono visualizzare l’esperienza. Per abilitare questa funzione, fai clic su **Seleziona pubblico** e scegli il &quot;*Premi fedeltà Luma - Gold Status*&#39; pubblico.

1. In **Spazio dei nomi dell’identità** , seleziona lo spazio dei nomi per identificare i singoli utenti all’interno del segmento scelto. Poiché stai distribuendo la campagna sul sito Luma, puoi scegliere lo spazio dei nomi ECID. Profili in &quot;*Premi fedeltà Luma - Gold Status* Il pubblico privo dello spazio dei nomi ECID tra le varie identità non è preso di mira dalla campagna del canale web.

   ![Scegli il tipo di identità](../assets/web-channel-indentity-type.png)

1. Pianifica la campagna a partire dal 1° dicembre utilizzando **Inizio campagna** e termina il 31 dicembre utilizzando il **Fine campagna** opzione.

   ![Pianificazione della campagna](../assets/web-channel-campaign-schedule.png)

>[!NOTE]
>
>Tieni presente che, per le campagne per canali web, l’esperienza web viene visualizzata quando il visitatore apre la pagina. Pertanto, a differenza di altri tipi di campagne in Adobe Journey Optimizer, il **Trigger azione** non è configurabile.

### Sperimentazione con contenuti di premi fedeltà

In **Azione** , puoi facoltativamente creare un esperimento per verificare quale contenuto funziona meglio per la &quot;*Premi fedeltà Luma - Gold Status*&#39; pubblico. Creiamo e testiamo due trattamenti come componente della configurazione della campagna.

Per creare l’esperimento sui contenuti:

1. Clic **Crea esperimento**.

   ![Crea esperimento](../assets/web-channel-create-content-experiment.png)

1. Scegli un **Metrica di successo**. Questa è la metrica per determinare l’efficacia dei contenuti. Scegli **Clic univoci in entrata**, per vedere quale trattamento dei contenuti genera più clic sul CTA dell’esperienza web.

   ![Scegli metrica di successo](../assets/web-channel-content-experiment-metric.png)

1. Quando si imposta un esperimento utilizzando il canale web e si sceglie **Clic in entrata**, **Clic univoci in entrata**, **Visualizzazioni pagina**, o **Visualizzazioni pagina univoche** metriche, le **Azione clic** a discesa consente di monitorare e tenere traccia con precisione dei clic e delle visualizzazioni su pagine specifiche.

1. Facoltativamente, puoi designare un **Blocco** che non riceve nessuno dei due trattamenti. Lascia questa opzione deselezionata per il momento.

1. Inoltre, se lo desideri, scegli di **Distribuisci uniformemente**. Selezionare questa opzione per assicurarsi che le divisioni del trattamento siano sempre divise in modo uniforme.

[Ulteriori informazioni sugli esperimenti di contenuto in Adobe Journey Optimizer Web Channel](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/content-experiment/get-started-experiment.html?lang=en).

### Modificare il contenuto con Visual Helper

Ora creiamo l’esperienza del canale web. A tale scopo, utilizza Adobe Experience Cloud **Helper visivo**. Questo strumento è un’estensione del browser compatibile con Google Chrome e Microsoft® Edge. Assicurati di aver scaricato l’estensione prima di tentare di generare le esperienze. Assicurati inoltre che la pagina web includa l’SDK per web.

1. All&#39;interno del **Azione** scheda della campagna, fai clic su **Modifica contenuto**. Poiché hai inserito come superficie un URL a pagina singola, dovresti essere pronto per iniziare a lavorare nel compositore.

   ![Modificare i contenuti](../assets/web-channel-edit-content.png)

1. Ora fai clic su **Modifica pagina web** per iniziare l’authoring.

   ![Modifica pagina web](../assets/web-channel-edit-web-page.png)

1. Inizia modificando alcuni elementi utilizzando il compositore web. Utilizza il menu contestuale per modificare l’intestazione dell’immagine protagonista Luma. Regola lo stile del riquadro contestuale a destra.

   ![Aggiungere modifiche contestuali](../assets/web-channel-some-contextual-edit.png)

1. Aggiungi anche la personalizzazione al contenitore utilizzando **Editor espressioni**.

   ![Aggiungere la personalizzazione](../assets/web-channel-add-basic-personalization.png)

1. Assicurati che l’esperienza sia correttamente tracciata per i clic. Scegli **Fai clic sull’elemento di tracciamento** dal menu contestuale.

   ![Traccia clic](../assets/web-channel-click-tracking.png)

1. Utilizza il **Componente decisione offerta** per inserire offerte nella pagina web. Questo componente utilizza **Gestione delle decisioni** per scegliere l’offerta migliore da consegnare ai visitatori Luma.


### Modifiche alla progettazione di HTML

Sono disponibili alcuni metodi per apportare modifiche più avanzate o personalizzate al sito come componente della campagna Premi fedeltà.

Utilizza il **Componenti** per aggiungere HTML o altri contenuti direttamente al sito Luma.

![Esplora il riquadro dei componenti](../assets/web-channel-components-pane.png)

Aggiungi un nuovo componente HTML nella parte superiore della pagina. Modifica il HTML all’interno del componente dall’interfaccia di progettazione oppure **Contestuale** riquadro.

![Aggiungi HTML personalizzato](../assets/web-channel-add-html-component.png)

In alternativa, aggiungi modifiche HTML da **Modifiche** riquadro. Questo riquadro consente di selezionare un componente nella pagina e modificarlo dall’interfaccia di progettazione.

Nell’editor, aggiungi il HTML per &quot;*Premi fedeltà Luma - Gold Status*&#39; pubblico. Clic **Convalida**.

![Convalida HTML](../assets/web-channel-add-custom-html-validate.png)

Ora controlla il nuovo componente HTML personalizzato per adattarlo alle esigenze.

![Rivedi HTML personalizzato](../assets/web-channel-review-custom-html.png)

Modificare un componente specifico utilizzando **Tipo di selettore CSS** modifica.

![Modifica CSS](../assets/web-channel-css-selector.png)

Aggiungere codice personalizzato utilizzando **Pagina `<head>` tipo** modifica.

![Modifica intestazione](../assets/web-channel-page-head-modification.png)

Le possibilità di utilizzo della **Helper visivo**.

### Simula contenuto premi fedeltà

Osserva un’anteprima della pagina web modificata prima di attivare la campagna. Tieni presente che devi avere profili di test configurati per simulare esperienze di canali web.

Per simulare l&#39;esperienza:

1. Seleziona **Simula contenuto** all’interno della campagna.

   ![Simula contenuto](../assets/web-channel-simulate-content.png)

1. Scegli un profilo di test per ricevere la simulazione. Tieni presente che il profilo di test deve essere nel &quot;*Premi fedeltà Luma - Gold Status*&#39; per ricevere il trattamento appropriato.

1. Viene visualizzata l’anteprima per il profilo di test.

### Attivazione della campagna Premi fedeltà

Infine, attiva la campagna del canale web.

1. Seleziona **Controlla per attivare**.

1. Ti viene chiesto di confermare un’ultima volta i dettagli della campagna. Seleziona **Attiva**. Potrebbero essere necessari fino a 15 minuti perché la campagna diventi live sul sito.

### Premi fedeltà QA

Come best practice, monitora **Web** scheda dei rapporti live e globali della campagna per i KPI specifici della campagna. Per questa campagna, monitora le impression dell’esperienza e la percentuale di clic.

![Visualizza rapporto web](../assets/web-channel-web-report.png)

### Convalida del canale web con Adobi Experience Platform Debugger

L’estensione Adobi Experience Platform Debugger, disponibile sia per Chrome che per Firefox, analizza le pagine web per identificare i problemi nell’implementazione delle soluzioni Adobe Experience Cloud.

Puoi utilizzare il debugger sul sito Luma per convalidare l’esperienza del canale web in produzione. Questa è una best practice una volta che il caso di utilizzo dei premi fedeltà è attivo e in esecuzione, per garantire che tutto sia configurato correttamente.

[Scopri come configurare il debugger nel browser utilizzando la guida qui](https://experienceleague.adobe.com/docs/platform-learn/data-collection/debugger/overview.html?lang=en).

Per iniziare la convalida tramite il debugger:

1. Passa alla pagina web Luma con l’esperienza del canale web.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Nella pagina web, apri **Adobe Experience Platform Debugger**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Accedi a **Riepilogo**. Verificare che **ID flusso di dati** corrisponde al **flusso di dati** in **Raccolta dati di Adobe** per cui hai abilitato Adobe Journey Optimizer.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Puoi quindi accedere al sito con vari account fedeltà Luma e utilizzare il debugger per convalidare le richieste inviate alla rete Edge di Adobe Experience Platform.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Sotto **Soluzioni** passa a **Experienci Platform Web SDK**.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. All&#39;interno del **Configurazione** , Attiva **Abilita debug**. Questo abilita la registrazione per la sessione all’interno di un **Adobe Experience Platform Assurance** sessione.
   <!--
    ![ADD SCREENSHOT](#)
    -->
1. Accedi al sito con vari account fedeltà Luma e utilizza il debugger per convalidare le richieste inviate al **Adobe Experience Platform Edge Network**. Tutte queste richieste devono essere acquisite in **Assurance** per il tracciamento dei registri.
<!--
   ![ADD SCREENSHOT](#)
-->