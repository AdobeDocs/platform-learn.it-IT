---
title: Configurare il consenso con Platform Web SDK
description: Scopri come configurare le impostazioni di privacy dell’estensione tag Experience Platform Web SDK. Questa lezione fa parte dell’esercitazione Implementa Adobe Experience Cloud con SDK per web.
exl-id: 502a7467-3699-4b2b-93bf-6b6069ea2090
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1624'
ht-degree: 0%

---

# Configurare il consenso con Platform Web SDK

Scopri come configurare le impostazioni di privacy dell’estensione tag Experience Platform Web SDK. Imposta il consenso in base all’interazione del visitatore con un banner da una piattaforma di gestione del consenso (CMP, Consent Management Platform).

>[!NOTE]
> 
>A scopo dimostrativo, questa esercitazione utilizza [Klaro](https://heyklaro.com/) come CMP. Sei libero di seguire l&#39;uso di Klaro o CMP che utilizzi con il tuo sito web.


## Finalità di apprendimento

Alla fine di questa lezione, puoi:

* Caricare una CMP utilizzando i tag
* Configurare le impostazioni di privacy nell’estensione tag Experience Platform Web SDK
* Imposta il consenso per Experience Platform Web SDK in base all&#39;azione del visitatore

## Prerequisiti

Acquisisci familiarità con i tag e i passaggi necessari per creare regole, elementi dati, creare librerie in ambienti e passare a librerie di tag tramite Experience Platform Debugger.

Prima di iniziare a configurare le impostazioni di privacy e a creare le regole per impostare il consenso, assicurati di aver inserito lo script della piattaforma di gestione del consenso sul sito web e di funzionare correttamente. Una piattaforma CMP può essere caricata direttamente nel codice sorgente con l’aiuto degli sviluppatori del sito o tramite i tag stessi. Questa lezione dimostra l&#39;ultimo approccio.
>[!NOTE]
> 
>1. Una piattaforma di gestione del consenso (o CMP) viene utilizzata dalle organizzazioni per documentare e gestire legalmente le scelte di consenso di un visitatore prima di raccogliere, condividere o vendere i dati dei visitatori da fonti online, come siti web e app.
>
>2. L’approccio consigliato per l’inserimento di una CMP avviene direttamente attraverso il codice sorgente prima dello script di gestione dei tag.


### Configura Klaro

Prima di passare alle configurazioni dei tag, scopri di più sulla piattaforma di gestione del consenso utilizzata in questa esercitazione Klaro.

1. Visita [Klaro](https://heyklaro.com/) e configura un account.
1. Vai a **Privacy Manager** e crea un&#39;istanza in base alle istruzioni.
1. Utilizza la **Codice di integrazione** per inserire Klaro nella proprietà tag (le istruzioni sono nell&#39;esercizio successivo).
1. Salta la **Scansione** , in quanto rileva la proprietà tag , che è codificata nel sito web dimostrativo Luma e non quella creata per questa esercitazione.
1. Aggiungi un servizio denominato `aep web sdk` e attivare **Stato predefinito del servizio**. Quando è attivato, il valore predefinito del consenso è `true`, altrimenti `false`. Questa configurazione è utile quando desideri decidere quale sarà lo stato predefinito del consenso (prima del consenso del visitatore) per l’applicazione web. Ad esempio:
   * Per CCPA, il consenso predefinito è comunemente impostato su `true`. Fai riferimento a questo scenario come **Consenso implicito** durante questa esercitazione
   * Per il RGPD, il consenso predefinito è comunemente impostato su `false`. Fai riferimento a questo scenario come **Rinuncia implicita** in questa esercitazione.

<!--
    This consent value can be verified by returning the JavaScript object ```klaro.getManager().consents``` in the browser's developer console.
-->
    >[!NOTE]
    >
    >Generalmente, i passaggi sopra menzionati sono fatti e presi cura dal team o dalla persona responsabile della gestione della CMP come OneTrust o TrustArc.

## Inserire una CMP

>[!WARNING]
>
>La best practice per implementare una piattaforma di gestione dei consensi è in genere quella di caricare la CMP _prima_ caricamento del gestore di tag. Per facilitare questa esercitazione, caricate la CMP _con_ il gestore di tag. Questa lezione è progettata per mostrare come utilizzare le funzioni di consenso in Platform Web SDK e non deve essere utilizzata come guida per configurare correttamente Klaro o qualsiasi altra CMP.


Ora, una volta completate le configurazioni di Klaro, crea una regola di tag con le seguenti configurazioni:

* [!UICONTROL Nome]: `all pages - library load - Klaro`
* [!UICONTROL Evento]: [!UICONTROL Libreria caricata (Pagina in alto)] con [!UICONTROL Opzioni avanzate] > [!UICONTROL Ordine] impostato su 1
* [!UICONTROL Azione]: [!UICONTROL Codice personalizzato], [!UICONTROL Lingua]: HTML per caricare lo script CMP.

![Inserisci regola CMP](assets/consent-cmp-inject-rule-1.png)

Il blocco di codice personalizzato deve essere simile al seguente:

![Inserisci regola CMP](assets/consent-cmp-inject-rule-2.png)

Ora salva e genera questa regola nella libreria di sviluppo, verifica che il banner di consenso venga visualizzato cambiando la libreria di tag dal sito Luma al tuo. Dovresti vedere un banner CMP sul sito web come segue. E per controllare l&#39;autorizzazione del visitatore corrente puoi usare il seguente frammento sulla console del browser.

```javascript
    klaro.getManager().consents 
```

![Banner di consenso](assets/consent-cmp-banner.png)

Per accedere alla modalità di debug, utilizza la casella di controllo seguente nel debugger Adobe Experience Platform.

![Modalità debug tag](assets/consent-rule-debugging.png)

Inoltre, potrebbe essere necessario cancellare i cookie e l’archiviazione locale più volte durante l’esercitazione, dal momento che il valore del consenso del visitatore viene memorizzato in tale area. È sufficiente eseguire questa operazione come segue:

![Cancellazione dello storage](assets/consent-clearning-cookies.png)

## Scenari di consenso

Gli atti relativi alla privacy come RGPD, CCPA e altri svolgono un ruolo fondamentale nel modo in cui architetti l’implementazione del consenso. In questa lezione, esplorerai in che modo un visitatore potrebbe interagire con il banner di consenso in due atti di privacy più importanti.
![Scenari di consenso](assets/consent-scenarios.jpeg)


### Scenario 1: Opt-in implicito

L&#39;opt-in implicito significa che l&#39;azienda non deve ottenere il consenso del visitatore (o il &quot;opt-in&quot;) prima di raccogliere i propri dati, e quindi tutti i visitatori del sito web vengono trattati come opted-in per impostazione predefinita. Tuttavia, il visitatore può rinunciare rifiutando i cookie tramite il banner di consenso. Questo caso d’uso è simile al CCPA.

Ora configurerai e implementerai il consenso per questo scenario:

1. In **[!UICONTROL Privacy]** dell&#39;estensione tag Experience Platform Web SDK, assicurati che  **[!UICONTROL Consenso predefinito]** è impostato su **[!UICONTROL In]** :


   ![Configurazione della privacy dell&#39;estensione AEP del consenso](assets/consent-web-sdk-privacy-in.png)

   >[!NOTE]
   > 
   >Per una soluzione dinamica, seleziona l’opzione &quot;Fornisci un elemento dati&quot; e passa un elemento dati che restituisce il valore di ```klaro.getManager().consents```
   >
   >Questa opzione viene utilizzata se la CMP viene inserita nel codice sorgente *prima* codice di incorporamento del tag in modo che il consenso predefinito sia disponibile prima che l’estensione Experience Platform Web SDK inizi a essere caricata. Nel nostro esempio, non possiamo utilizzare questa opzione perché la CMP viene caricata con tag e non prima dei tag.



2. Salva e genera questa modifica nella libreria di tag
3. Carica la libreria di tag sul sito Demo Luma
4. Abilita il debug dei tag durante il sito Luma e ricarica la pagina. Nella console per sviluppatori del browser, dovresti vedere che defaultConsent è uguale a **[!UICONTROL In]**
5. Con questa configurazione, l’estensione Experience Platform Web SDK continua a effettuare richieste di rete, a meno che un visitatore non decida di rifiutare i cookie e la rinuncia:

   ![Consenso implicito Opt In](assets/consent-Implied-optin-default.png)



Se un visitatore decide di rinunciare (rifiutare i cookie di tracciamento), devi modificare il consenso in **[!UICONTROL Uscita]**. Modifica l’impostazione del consenso seguendo questi passaggi:

<!--
1. Create a data element to store the consent value of the visitor. Let's call it `klaro consent value`. Use the code snippet to create a custom code type data element:
    
    ```javascript
    return klaro.getManager().consents["aep web sdk"]
    ```

    ![Data Element consent value](assets/consent-data-element-value.png)


1. Create another custom code data element, `consent confirmed`, with the following snippet which returns ```true``` only after a visitor confirms consent:

    
    ```javascript
    return klaro.getManager().confirmed
    ```

    ![Data Element consent confirmed](assets/consent-data-element-confirmed.png)
-->

1. Crea una regola che si attiva quando il visitatore fa clic su **Rifiuto**.  Denomina questa regola come: `all pages - click consent banner - set consent "out"`

1. Come **[!UICONTROL Evento]**, utilizza **[!UICONTROL Fai clic su]** su **[!UICONTROL Elementi che corrispondono al selettore CSS]** `#klaro .cn-decline`

   ![L&#39;utente della condizione della regola fa clic su &quot;Rifiuto&quot;](assets/consent-optOut-clickEvent.png)

1. Ora utilizza l’SDK per web di Experience Platform, [!UICONTROL Imposta consenso] [!UICONTROL tipo di azione] per impostare il consenso come &quot;esaurito&quot;:

   ![Azione di rinuncia alla regola del consenso](assets/consent-rule-optout-action.png)

1. Seleziona **[!UICONTROL Salva nella libreria e genera]**:

   ![Salva e genera la libreria](assets/consent-rule-optout-saveAndBuild.png)

Ora, quando un visitatore rinuncia, la regola configurata in questo modo si attiverebbe e imposta il consenso dell’SDK web come **[!UICONTROL Uscita]**.

Convalida andando al sito Demo Luma, rifiutando i cookie e confermando che nessuna richiesta SDK web viene attivata dopo l’rinuncia.

### Scenario 2: Rinuncia implicita


La rinuncia implicita significa che i visitatori devono essere trattati come oggetto di rinuncia per impostazione predefinita e che i cookie non devono essere impostati. Le richieste SDK per web non devono attivarsi a meno che i visitatori non decidano di accettare manualmente i cookie tramite il banner di consenso. Potrebbe essere necessario trattare un caso d’uso di questo tipo nell’area dell’Unione europea in cui si applica il RGPD.

Ecco come impostare la configurazione per uno scenario di rinuncia implicita:

1. In Klaro, disattivare **Stato predefinito del servizio** nel tuo `aep web sdk` e salva la configurazione aggiornata.

1. In **[!UICONTROL Privacy]** sezione dell&#39;estensione Experience Platform Web SDK, imposta il consenso predefinito su **[!UICONTROL Uscita]** o **[!UICONTROL In sospeso]** se necessario.

   ![Configurazione della privacy dell&#39;estensione AEP del consenso](assets/consent-implied-opt-out.png)

1. **Salva** la configurazione aggiornata alla libreria di tag e ricrearla.

   Con questa configurazione, Experience Platform Web SDK assicura che nessuna richiesta venga attivata a meno che l&#39;autorizzazione di consenso non venga modificata in **[!UICONTROL In]**. Questo potrebbe accadere in seguito all’accettazione manuale dei cookie da parte di un visitatore tramite consenso.

1. Nel debugger, assicurati che il sito Luma sia mappato alla proprietà tag e che la console-logging dei tag sia attiva.
1. Utilizza la console di sviluppo del browser in **Cancella dati del sito** in **Applicazione** > **Storage**

1. Ricarica il sito Luma e dovresti vedere che `defaultConsent` è impostato su **[!UICONTROL Uscita]** e non sono state effettuate richieste SDK per web

   ![Consenso implicito Opt Out](assets/consent-implied-out-cmp.png)

Nel caso in cui un visitatore decida di accettare i cookie di tracciamento, devi modificare il consenso e impostarlo su **[!UICONTROL In]**. Ecco come eseguire questa operazione con una regola:

1. Crea una regola che si attiva quando il visitatore fa clic su **Va bene**.  Denomina questa regola come: `all pages - click consent banner - set consent "in"`

1. Come **[!UICONTROL Evento]**, utilizza **[!UICONTROL Fai clic su]** su **[!UICONTROL Elementi che corrispondono al selettore CSS]** `#klaro .cm-btn-success`

   ![L&#39;utente della condizione della regola fa clic su &quot;Va bene&quot;](assets/consent-optIn-clickEvent.png)

1. Aggiungere un’azione utilizzando l’SDK per web di Experience Platform [!UICONTROL Estensione], **[!UICONTROL Tipo di azione]** di **[!UICONTROL Imposta consenso]**, **[!UICONTROL Consenso generale]** come **[!UICONTROL In]**.

   ![Azione di consenso della regola](assets/consent-rule-optin-action.png)

   Una cosa da notare è che [!UICONTROL Imposta consenso] l&#39;azione sarà la prima richiesta che esce e stabilisce l&#39;identità. Per questo motivo, potrebbe essere importante sincronizzare le identità sulla prima richiesta stessa. È possibile aggiungere la mappa di identità a [!UICONTROL Imposta consenso] passa un elemento dati di tipo identity.

1. Seleziona **[!UICONTROL Salva nella libreria e genera]**:

   ![Rinuncia alla regola del consenso](assets/consent-rule-optin-saveAndBuild.png)

1. **[!UICONTROL Salva]** la regola nella libreria e ricrearla.

Una volta implementata questa regola, la raccolta degli eventi dovrebbe iniziare quando un visitatore effettua il consenso.

![Consenso Opt. visitatore del post](assets/consent-post-user-optin.png)


Per ulteriori informazioni sul consenso in SDK per web, vedi [Supporto delle preferenze di consenso dei clienti](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?lang=en).


Per ulteriori informazioni sulla [!UICONTROL Imposta consenso] azione, vedi [Imposta consenso](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/action-types.html?lang=en#set-consent).

[Avanti: ](setup-event-forwarding.md)

>[!NOTE]
>
>Grazie per aver investito il tuo tempo nel conoscere Adobe Experience Platform Web SDK. In caso di domande, se desideri condividere feedback generali o se hai suggerimenti su contenuti futuri, condividi questi su questo [Experience League Articolo di discussione della Comunità](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
