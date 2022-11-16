---
title: Implementare il consenso con una piattaforma di gestione del consenso (CMP, Consent Management Platform)
description: Scopri come implementare e attivare i dati di consenso ottenuti da una piattaforma di gestione dei consensi (CMP) utilizzando l’estensione Adobe Experience Platform Web SDK nella raccolta dati.
feature: Web SDK, Tags
role: Developer, Data Engineer
doc-type: tutorial
exl-id: bee792c3-17b7-41fb-a422-289ca018097d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '3347'
ht-degree: 2%

---

# Implementa il consenso con una piattaforma di gestione dei consensi (CMP) utilizzando l’estensione Platform Web SDK

Molte normative legali sulla privacy hanno introdotto requisiti per il consenso attivo e specifico in relazione alla raccolta dei dati, alla personalizzazione e ad altri casi d’uso del marketing. Per soddisfare questi requisiti, Adobe Experience Platform ti consente di acquisire le informazioni sul consenso nei profili dei singoli clienti e di utilizzarle come fattore determinante per l’utilizzo dei dati di ciascun cliente nei flussi di lavoro della piattaforma a valle.

>[!NOTE]
>
>Adobe Experience Platform Launch viene integrato in Adobe Experience Platform come suite di tecnologie per la raccolta dati. Nell’interfaccia sono state introdotte diverse modifiche terminologiche di cui tenere conto durante l’utilizzo di questo contenuto:
>
> * Il platform launch (lato client) è ora **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it)**
> * Lato server di platform launch è ora **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Le configurazioni Edge sono ora **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=it)**


Questa esercitazione illustra come implementare e attivare i dati di consenso ottenuti da una piattaforma di gestione dei consensi (CMP) utilizzando l’estensione Platform Web SDK nella raccolta dati. Lo faremo utilizzando sia gli standard di Adobe che lo standard di consenso IAB TCF 2.0, con OneTrust o Sourcepoint come CMP di esempio.

Questa esercitazione utilizza l’estensione Platform Web SDK per inviare i dati di consenso a Platform. Per una panoramica dell&#39;SDK web, vedi [questa pagina](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=it).

## Prerequisiti

Sono elencati i prerequisiti per l’utilizzo dell’SDK per web [qui](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/prerequisite.html?lang=en#fundamentals).

In quella pagina, c&#39;è un requisito per un &quot;Set di dati evento&quot; e, proprio come sembra, questo è un set di dati per contenere i dati dell&#39;evento esperienza. Per inviare informazioni sul consenso con gli eventi, la [Gruppo di campi Dettagli privacy](https://github.com/adobe/xdm/blob/master/docs/reference/field groups/experience-event/experienceevent-privacy.schema.md) deve essere aggiunto allo schema Experience Event (Evento esperienza):

![](./images/event-schema.png)

Per lo standard di consenso Platform v2.0, è inoltre necessario accedere al profilo Adobe Experience per creare uno schema di profilo individuale XDM e un set di dati. Per un&#39;esercitazione sulla creazione dello schema, vedi [Creare uno schema utilizzando l’Editor di schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#tutorials) e per il gruppo di campi profilo Dettagli preferenza richiesto vedi [Documentazione di XDM](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/overview.html?lang=en).

Questa esercitazione presuppone che tu abbia accesso alla raccolta dati e che tu abbia creato una proprietà tag lato client con l&#39;estensione SDK per web installata e una libreria di lavoro creata e creata per lo sviluppo. Questi argomenti sono descritti in dettaglio e illustrati in questi documenti:

* [Creare o configurare una proprietà](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=en#create-or-configure-a-property)
* [Panoramica delle librerie](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html)
* [Panoramica sulla pubblicazione](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html)

Useremo anche il [Debugger di Platform](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) Estensione Chrome per controllare e convalidare la nostra implementazione.

Per implementare l’esempio IAB TCF con una CMP sul tuo sito, avrai bisogno di accedere a una CMP come OneTrust o Sourcepoint per generare i dati che forniscono, oppure puoi semplicemente seguire questo esempio e vedere i risultati qui sotto.

## Utilizzo dell’SDK per web con Adobe Consent Standard (v1.0 o v2.0)

>[!NOTE]
>
>Lo standard 1.0 viene gradualmente eliminato a favore della versione v2.0. Lo standard 2.0 ti consente di aggiungere dati di consenso aggiuntivi che possono essere utilizzati per applicare manualmente le preferenze di consenso. Le schermate seguenti dell’estensione Platform Web SDK provengono dalla versione [2.4.0](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html?lang=en#version-2.4.0) dell’estensione compatibile con le versioni v1.0 o v2.0 di Adobe Consent Standard.

Per ulteriori informazioni su questi standard, vedi [Supporto delle preferenze di consenso dei clienti](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html).

### Passaggio 1: Configurare il consenso nell’estensione SDK per web

Dopo aver installato l’estensione Platform Web SDK in una proprietà tag, possiamo configurare le opzioni per la gestione dei dati di consenso nella schermata di configurazione dell’estensione:

![](./images/pending.png)

La sezione &quot;Privacy&quot; imposta il livello di consenso per l&#39;SDK se l&#39;utente non ha precedentemente fornito le preferenze di consenso. Questo imposta lo stato predefinito per la raccolta dei dati del consenso e dell’evento nell’SDK. L’impostazione scelta risponde alla domanda &quot;cosa deve fare l’SDK se l’utente non ha ancora fornito preferenze di consenso esplicite?&quot;

* In : raccogli eventi che si verificano prima che l&#39;utente fornisca le preferenze di consenso.
* Out: eventi di rilascio che si verificano prima che l’utente fornisca le preferenze di consenso.
* In sospeso: eventi in coda che si verificano prima che l’utente fornisca le preferenze di consenso.
* Fornito dall’elemento dati

Se l’impostazione di consenso predefinito è &quot;In&quot;, questo indica all’SDK di non attendere il consenso esplicito e di raccogliere gli eventi che si verificano prima che l’utente fornisca le preferenze di consenso. Queste preferenze vengono in genere gestite e memorizzate in una piattaforma CMP.

Se l&#39;impostazione di consenso predefinita è &quot;Out&quot;, questo indica all&#39;SDK che non deve raccogliere eventi che si verificano prima che le preferenze di consenso dell&#39;utente siano impostate. L’attività del visitatore che si verifica prima dell’impostazione della preferenza di consenso non verrà inclusa nei dati inviati dall’SDK dopo aver impostato il consenso. Ad esempio, se scorri e visualizzi una pagina web prima di selezionare il banner di consenso e utilizzi questa impostazione &quot;Out&quot;, l’attività di scorrimento e il tempo di visualizzazione non verranno inviati se l’utente successivamente fornisce il consenso esplicito per la raccolta dei dati.

Se l&#39;impostazione di consenso predefinita è &quot;In sospeso&quot;, l&#39;SDK mette in coda tutti gli eventi che si verificano prima che l&#39;utente fornisca le preferenze di consenso, in modo che gli eventi possano essere inviati dopo che le preferenze di consenso sono state impostate e dopo che l&#39;SDK è stato inizialmente configurato durante una visita.

Con questa impostazione &quot;In sospeso&quot;, il tentativo di eseguire i comandi che richiedono le preferenze di consenso dell&#39;utente (ad esempio, il comando dell&#39;evento) determina la messa in coda del comando all&#39;interno dell&#39;SDK. Questi comandi non vengono elaborati finché non avrai comunicato le preferenze di consenso dell&#39;utente all&#39;SDK.

Una volta che una CMP raccoglie le preferenze dell&#39;utente, possiamo comunicare tali preferenze all&#39;SDK. In una sezione successiva, vedremo come ottenere i dati di consenso e utilizzarli con l’estensione SDK per web.

&quot;Fornito dall’elemento dati&quot; consente di accedere a un elemento dati contenente eventuali dati di preferenza del consenso acquisiti dal codice personalizzato o da una CMP sul sito o nel livello dati. Un elemento dati utilizzato a questo scopo deve essere risolto in &quot;in&quot;, &quot;out&quot; o &quot;in sospeso&quot;.

Nota: questa impostazione di configurazione per l’SDK non viene mantenuta sui profili degli utenti, ma è specifica per impostare il comportamento dell’SDK prima che il visitatore fornisca le preferenze di consenso esplicito.

Per ulteriori informazioni sulla configurazione dell&#39;estensione SDK per web, consulta la sezione [Panoramica dell’estensione SDK per web Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-extension-configuration.html?lang=en#configure-the-extension) e [Supporto delle preferenze di consenso dei clienti](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html).

Per questo esempio, scegliamo l&#39;opzione per &quot;In sospeso&quot; e selezioniamo **Salva** per salvare le impostazioni di configurazione.

### Passaggio 2: Comunicazione delle preferenze di consenso

Ora che abbiamo impostato il comportamento predefinito dell’SDK, possiamo utilizzare i tag per inviare le preferenze di consenso esplicito di un visitatore a Platform. L’invio dei dati di consenso tramite lo standard Adobe 1.0 o 2.0 è facilmente implementabile utilizzando l’azione setConsent dell’SDK web nelle regole dei tag.

#### Impostazione del consenso con Platform Consent Standard 1.0

Creiamo una regola per dimostrarlo. Nella proprietà Tag piattaforma , seleziona Regole , quindi fai clic sul pulsante blu Aggiungi regole . Denomina la regola &quot;setAdobeConsent&quot; e seleziona per aggiungere un evento. Per Tipo evento, scegli &quot;Window Loaded&quot; che attiverà questa regola ogni volta che una pagina viene caricata sul nostro sito web. Quindi, in &quot;Azioni&quot; seleziona &quot;Aggiungi&quot; per aprire la schermata di configurazione dell&#39;azione. Qui verranno impostati i dati di consenso. Seleziona il menu a discesa &quot;Estensione&quot; e seleziona &quot;Platform Web SDK&quot;, quindi seleziona il &quot;Tipo di azione&quot; e seleziona &quot;Imposta consenso&quot;.

In &quot;Informazioni sul consenso&quot;, scegliere &quot;Compila un modulo&quot;. In questa azione della regola, utilizzeremo l’SDK per web per impostare il consenso per lo standard di consenso Adobe 1.0 compilando il modulo visualizzato:

![](./images/1-0-form.png)

Con questa azione Imposta consenso possiamo scegliere di passare &quot;In&quot;, &quot;Out&quot; o &quot;Fornito dall’elemento dati&quot;. Un elemento dati in questo caso deve essere &quot;in&quot; o &quot;out&quot;.

In questo esempio, selezioneremo &quot;In&quot; per indicare che il visitatore ha acconsentito a consentire all’SDK per web di inviare dati a Platform. Seleziona il pulsante blu &quot;Mantieni modifiche&quot; per salvare questa azione, quindi &quot;Salva&quot; per salvare questa regola.

Nota: Una volta che un visitatore del sito web ha rinunciato, l&#39;SDK non ti consente di impostare il consenso degli utenti ad in.

Le regole dei tag possono essere attivate da una varietà di [events](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/core/overview.html?lang=en) che può essere utilizzato per trasmettere i dati di consenso al momento appropriato durante una sessione del visitatore. Nell’esempio precedente, abbiamo utilizzato l’evento window loaded per attivare la regola. In una sezione successiva, utilizzeremo un evento di preferenza del consenso da una CMP per attivare un’azione Imposta consenso. Puoi utilizzare un&#39;azione Imposta consenso in una regola attivata da qualsiasi evento che preferisci che indichi un&#39;impostazione di preferenza di consenso.

#### Impostazione del consenso con Platform Consent Standard 2.0

La versione 2.0 dello standard di consenso di Platform funziona con [XDM](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/schemas-and-experience-data-model.html?lang=it) dati. Inoltre, è necessario aggiungere un gruppo di campi Privacy Details allo schema del profilo in Platform. Vedi [Elaborazione del consenso in Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/overview.html) per ulteriori informazioni su Adobe standard versione 2.0 e questo gruppo di campi.

Creeremo un elemento dati di codice personalizzato per trasmettere i dati alle proprietà di raccolta e metadati dell&#39;oggetto consenso mostrato nello schema seguente:

![](./images/collect-metadata.png)

Questo gruppo di campi Dettagli preferenza contiene campi per [Consensi e preferenze Tipo di dati XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/data-types/consents.html?lang=en#prerequisites) che conterrà i dati delle preferenze di consenso inviati a Platform con l’estensione Platform Web SDK nella nostra azione regola. Attualmente, le uniche proprietà richieste per implementare Platform Consent Standard 2.0 sono il valore di raccolta (val) e il valore di tempo dei metadati, evidenziati in precedenza in rosso.

Creiamo un elemento dati per questi dati. Seleziona Elementi dati e il pulsante blu Aggiungi elemento dati . Chiamiamolo &quot;xdm-permission 2.0&quot; e utilizzando l’estensione Core, selezioneremo un tipo di codice personalizzato. Puoi immettere o copiare e incollare i seguenti dati nella finestra dell’editor di codice personalizzato:

```js
var dateString = new Date().toISOString();

return {
  collect: {
    val: "y"
  },
  metadata: {
    time: dateString
  }
}
```

Il campo temporale deve specificare l’ultima volta che l’utente ha aggiornato le proprie preferenze di consenso. Stiamo creando una marca temporale qui come esempio utilizzando un metodo standard sull&#39;oggetto Data JavaScript. Seleziona salva per salvare il codice personalizzato e seleziona nuovamente salva per salvare l’elemento dati.

Quindi, selezioniamo Regole, quindi il pulsante blu Aggiungi regola e immetti il nome &quot;setConsent onLoad - Consent 2.0&quot;. Scegliamo l&#39;evento Window Loaded come attivatore della regola, quindi seleziona Aggiungi in Azioni. Scegli l’estensione Platform Web SDK e, per Tipo azione, scegli Imposta consenso. Lo standard deve essere Adobe e la versione deve essere 2.0. Per Valore, utilizzeremo l’elemento dati appena creato che contiene i valori di raccolta e ora che dobbiamo inviare a Platform:

![](./images/2-0-form.png)

Per rivedere questa azione di esempio, chiamiamo l’estensione Set Consent dall’SDK per web di Platform e passiamo lo Standard e la Versione dal modulo, mentre trasmettiamo i valori per la raccolta e l’ora dall’elemento dati creato in precedenza.

Seleziona il pulsante blu Salva e di nuovo per salvare la regola.

Ora disponiamo di due regole, una per ciascuno degli standard di Platform Consent. In pratica, probabilmente sceglierai uno standard tra i tuoi siti. Ora creeremo un esempio utilizzando lo standard di consenso IAB TCF 2.0.

## Utilizzo dell’SDK per web con lo standard di consenso IAB TCF 2.0

Per ulteriori informazioni sulla versione 2.0 del framework per la trasparenza e il consenso IAB, consulta [Sito web IAB Europe](https://iabeurope.eu/transparency-consent-framework/).

Per impostare i dati delle preferenze di consenso utilizzando questo standard, è necessario aggiungere il gruppo di campi Privacy Details allo schema Experience Event (Evento esperienza) in Platform:

![](./images/consentStrings.png)

Questo gruppo di campi contiene i campi delle preferenze di consenso richiesti dallo standard IAB TCF 2.0. Per ulteriori informazioni sugli schemi e sui gruppi di campi, consulta la sezione [Panoramica del sistema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it).

### Passaggio 1: Creare un elemento dati di consenso

Per inviare i dati evento di consenso dai tag utilizzando lo standard di consenso IAB TCF 2.0, per prima cosa abbiamo impostato un elemento dati xdm con i campi di consenso richiesti:

![](./images/data-element.png)

Nella proprietà lato client dei tag, seleziona Elementi dati e il pulsante blu &quot;Aggiungi elemento dati&quot;. Questo elemento dati verrà denominato &quot;xdm-permissionStrings&quot; per questo esempio. Questi campi xdm contengono i dati di consenso utente richiesti per lo standard IAB TCF 2.0.

Nel menu a discesa Estensione , scegli &quot;Platform Web SDK&quot; e, per Tipo di elemento dati, scegli &quot;Oggetto XDM&quot;. Viene visualizzata la mappatura xdm, che consente di selezionare ed espandere l’elemento &quot;permissionStrings&quot; come mostrato nella schermata precedente.

Imposta ciascuna delle proprietà consentString come segue:

* **`consentStandard`**:  `IAB TCF`
* **`consentStandardVersion`**:  `2.0`
* **`consentStringValue`**:  `%IAB TCF Consent String%`
* **`containsPersonalData`**:  `False` (scelta dal pulsante Seleziona valore )
* **`gdprApplies`**:  `%IAB TCF Consent GDPR%`

Insieme a permissionStandard e consentStandardVersion sono presenti solo stringhe di testo per lo standard in uso, ovvero IAB TCF versione 2.0. Il permissionStringValue fa riferimento a un elemento di dati denominato &quot;IAB TCF Consent String&quot;. I segni di percentuale che circondano il testo indicano il nome di un elemento dati, e lo guarderemo tra un attimo. La proprietà containsPersonalData indica se la stringa di consenso IAB TCF 2.0 contiene dati personali con &quot;True&quot; o &quot;False&quot;. Il campo rgpdApplies indica se si applica &quot;true&quot; per il RGPD, &quot;false&quot; per il RGPD non si applica o &quot;undefined&quot; per unknown se si applica il RGPD. Al momento, l’SDK per web tratterà &quot;non definito&quot; come &quot;true&quot;, pertanto i dati di consenso inviati con &quot;gdprApplies&quot;: indefinito&quot; sarà trattato come se il visitatore si trovi in un’area in cui si applica il RGPD.

Consulta la sezione [documentazione di consenso](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/iab-tcf/with-launch.html?lang=en#getting-started) per ulteriori informazioni su queste proprietà e su IAB TCF 2.0 nei tag .

### Passaggio 2: Crea una regola per impostare il consenso con lo standard IAB TCF 2.0

Successivamente, creiamo una regola per impostare il consenso con l’SDK per web quando i dati di consenso per questo standard vengono impostati o modificati da un visitatore del sito web. In questa regola, vedremo anche come acquisire i segnali di modifica del consenso da una CMP come [OneTrust](https://www.onetrust.com/products/cookie-consent/) o [Sourcepoint](https://www.sourcepoint.com/cmp/).

#### Aggiungere un evento regola

Seleziona la sezione Regole nella proprietà Tag Platform , quindi fai clic sul pulsante blu Aggiungi regola . Denomina la regola setConsent - IAB e seleziona Aggiungi in Eventi. Denomina questo evento tcfapi addEventListener e seleziona Open Editor per aprire l&#39;editor di codice personalizzato.

Copia e incolla il seguente codice nella finestra dell&#39;editor:

```js
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString properties in data elements
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Questo codice crea ed esegue semplicemente una funzione chiamata addEventListener. La funzione controlla se la finestra.__tcfapi esiste e, in caso affermativo, aggiunge un listener di eventi in base alle specifiche dell&#39;API. Per ulteriori informazioni su tali specifiche, consulta la sezione [Repo IAB](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework) su GitHub. Se questo listener di eventi viene aggiunto correttamente e il visitatore del sito web ha completato le scelte di consenso e preferenze, il codice imposta le variabili personalizzate dei tag per tcData tcString e l&#39;indicatore per le aree RGPD. Anche in questo caso, per ulteriori informazioni su IAB TCF, consulta l’IAB [sito web](https://iabeurope.eu/transparency-consent-framework/) e [Archivio GitHub](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework) per informazioni tecniche. Dopo aver impostato questi valori, il codice esegue la funzione di attivazione che attiva l&#39;esecuzione di questa regola.

Se la finestra.__tcfapi l&#39;oggetto non esisteva al primo avvio dell&#39;esecuzione di questa funzione, la funzione lo controlla nuovamente ogni 100 millisecondi, in modo che il listener di eventi possa essere aggiunto. L&#39;ultima riga di codice esegue semplicemente la funzione addEventListener definita nelle righe di codice sopra di essa.

Per riepilogare, abbiamo creato una funzione per verificare lo stato del consenso impostato da un visitatore del sito web utilizzando un banner di consenso CMP (o personalizzato). Quando questa preferenza di consenso è impostata, questo codice crea due variabili personalizzate (elementi dati codice personalizzato) che possiamo utilizzare nell&#39;azione della regola. Dopo aver incollato il codice riportato sopra nella finestra dell&#39;editor di codice personalizzato del nostro evento, seleziona il pulsante blu Salva per salvare l&#39;evento della regola.

Imposta l’azione Imposta regola consenso per utilizzare questi valori e inviarli a Platform.

#### Aggiungi un&#39;azione regola

Selezionare Aggiungi nella sezione Azioni. In Estensione , scegli SDK web per piattaforma dal menu a discesa. In Tipo azione, scegli Imposta consenso. Denomina questa azione setConsent.

Nella configurazione dell’azione in Informazioni consenso, scegli Compila un modulo. Per Standard, scegli IAB TCF e per Versione inserisci 2.0. Per Valore, utilizzeremo la variabile personalizzata dal nostro evento e immetteremo %IAB TCF Consent String% che proviene dal [tcData](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20CMP%20API%20v2.md#tcdata) abbiamo acquisito la funzione personalizzata dell&#39;evento regola di cui sopra.

In Applicazione RGPD utilizzeremo l’altra variabile personalizzata dal nostro evento e immetteremo %IAB TCF Consent RGPD% che proviene anche da tcData che abbiamo acquisito nella funzione personalizzata dell’evento regola di cui sopra. Se sai che il RGPD verrà o meno applicato ai visitatori di questo sito web, puoi selezionare Sì o No, a seconda dei casi, invece di utilizzare la scelta della variabile personalizzata (elemento dati). Puoi anche utilizzare la logica condizionale in un elemento dati per verificare se il RGPD è applicabile e restituire il valore appropriato.

In RGPD Contiene dati personali, seleziona l’opzione per indicare se i dati di questo utente contengono o meno dati personali. Un elemento dati in questo caso deve essere true o false.

![](./images/data-element-2-0.png)

Seleziona il pulsante blu Salva per salvare l’azione e il pulsante blu Salva (o Salva nella libreria) per salvare la regola. A questo punto, hai implementato correttamente l’elemento dati e la regola nei tag per impostare il consenso tramite l’estensione SDK per web con lo standard di consenso IAB TCF 2.0.

### Passaggio 3: Salva nella libreria e genera

Se utilizzi il [biblioteca di lavoro](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/add-data-elements-rules.html?lang=en#use-the-working-library-feature) prerequisito: hai già salvato queste modifiche e generato la libreria di sviluppo:

![](./images/save-library.png)

### Passaggio 4: Inspect e convalida della raccolta dati

Sul nostro sito, aggiorniamo la pagina e confermiamo la build della libreria nel [Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) Estensione Chrome, nella sezione del menu tag:

![](./images/build-date.png)

È inoltre possibile controllare la chiamata setConsent per gli standard Adobe 1.0 o 2.0 nella sezione debugger Platform Web SDK , selezionando sulla riga POST Body nella richiesta di rete in cui viene visualizzato `{"consent":[{"value":{"general":"in"},"version…`:

![](./images/inspect-consent-call.png)

Per convalidare la chiamata setConsent e la nostra regola per lo standard IAB TCF 2.0, utilizzeremo il banner di consenso OneTrust sul nostro sito di test per impostare le preferenze di consenso e creare i tcData descritti in precedenza:

![](./images/banner.png)

Dopo aver selezionato &quot;Accetto&quot;, possiamo controllare la chiamata setConsent per lo standard IAB TCF 2.0 nella sezione debugger Platform Web SDK, selezionando sulla riga corpo di POST nella richiesta di rete in cui viene visualizzato `{"consent":[{"value":"someAlphaNumericCharacters…`.

![](./images/inspect-2-0.png)

Qui vediamo i dati impostati in precedenza nei nostri elementi dati e nelle nostre regole di tag. La proprietà value contiene i dati tcString codificati visualizzati in precedenza.

OneTrust, Sourcepoint e altri CMP che implementano lo standard IAB TCF 2.0 produrranno tutti dati simili nelle nostre pagine. Possiamo acquisire tali dati e utilizzarli con l’estensione SDK per web nei tag utilizzando l’evento codice personalizzato nella regola creata in precedenza. Il codice personalizzato sarà lo stesso indipendentemente dalla CMP utilizzata per generare i dati IAB TCF 2.0. Il codice personalizzato può essere utilizzato anche con uno degli standard di consenso della piattaforma (1.0 o 2.0).

## Invio di dati di consenso con eventi Experience

Potresti aver notato che non abbiamo fatto riferimento all’elemento dati &quot;xdm-permissionStrings&quot; creato in precedenza in un campo elemento dati in una delle nostre regole. Questo elemento dati è da utilizzare quando devi inviare i dati di consenso con un evento di esperienza.

![](./images/consentStrings-data-element.png)

Poiché questo elemento dati contiene tutti i campi richiesti per lo standard IAB TCF 2.0, è sufficiente fare riferimento all’elemento dati quando si inviano questi dati xdm con i tuoi eventi Experience:

![](./images/consentStrings-reference.png)

## Conclusione

Dopo aver esaminato e convalidato i dati, dovresti vedere come implementare e attivare i dati di consenso ottenuti da una CMP utilizzando l’estensione Platform Web SDK per Platform.
