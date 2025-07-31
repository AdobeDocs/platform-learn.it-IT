---
title: Configurare il consenso con Platform Web SDK
description: Scopri come configurare le impostazioni di privacy dell’estensione tag Experience Platform Web SDK. Questa lezione fa parte del tutorial Implementare Adobe Experience Cloud con Web SDK.
feature: Web SDK,Tags,Consent
jira: KT-15413
exl-id: 502a7467-3699-4b2b-93bf-6b6069ea2090
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 1%

---

# Configurare il consenso con Platform Web SDK

Scopri come configurare le impostazioni di privacy dell’estensione tag Adobe Experience Platform Web SDK. Imposta il consenso in base all’interazione del visitatore con un banner di una piattaforma di gestione del consenso (CMP).

>[!NOTE]
> 
>Per scopi dimostrativi, questo tutorial utilizza [Klaro](https://klaro.org/) come CMP. Siete invitati a seguire l&#39;utilizzo di Klaro o la CMP che usate con il vostro sito web.


## Obiettivi di apprendimento

Alla fine di questa lezione, sarai in grado di:

* Caricare una CMP utilizzando i tag
* Configurare le impostazioni della privacy nell’estensione tag Experience Platform Web SDK
* Imposta il consenso per Experience Platform Web SDK in base all’azione del visitatore

## Prerequisiti

Devi acquisire familiarità con i tag e i passaggi per creare regole, elementi di dati, creare librerie in ambienti e cambiare le librerie di tag utilizzando Experience Platform Debugger.

Prima di iniziare a configurare le impostazioni della privacy e a creare le regole per l’impostazione del consenso, assicurati di aver inserito lo script della piattaforma di gestione del consenso sul sito web e di funzionare correttamente. Una CMP può essere caricata direttamente nel codice sorgente con l’aiuto degli sviluppatori del sito o attraverso i tag stessi. Questa lezione illustra quest&#39;ultimo approccio.

>[!NOTE]
> 
>1. Una piattaforma di gestione del consenso (o CMP) viene utilizzata dalle organizzazioni per documentare e gestire legalmente le scelte di consenso di un visitatore prima di raccogliere, condividere o vendere i dati del visitatore da fonti online come siti web e app.
>
>2. L’approccio consigliato per l’inserimento di una CMP è quello di passare direttamente attraverso il codice sorgente prima dello script di gestione dei tag.

### Configurare Klaro

Prima di passare alle configurazioni di tag, scopri di più sulla piattaforma di gestione del consenso utilizzata in questo tutorial Klaro.

1. Visita [Klaro](https://klaro.org/) e configura un account.
1. Vai a **Privacy Manager** e crea un&#39;istanza seguendo le istruzioni.
1. Utilizza il **Codice integrazione** per inserire Klaro nella tua proprietà tag (le istruzioni sono nel prossimo esercizio).
1. Ignora la sezione **Scansione**, in quanto rileva la proprietà tag codificata nel sito Web di dimostrazione Luma e non quella creata per questa esercitazione.
1. Aggiungi un servizio denominato `aep web sdk` e attiva **Stato predefinito servizio**. Quando è attivata, il valore di consenso predefinito è `true`, altrimenti è `false`. Questa configurazione è utile quando desideri decidere quale sarà lo stato di consenso predefinito (prima del consenso del visitatore) per l’applicazione web. Ad esempio:
   * Per il CCPA, il consenso predefinito è in genere impostato su `true`. Stai per fare riferimento a questo scenario come **consenso implicito** in questa esercitazione
   * Per il RGPD, il consenso predefinito è comunemente impostato su `false`. Stai per fare riferimento a questo scenario come **Rinuncia implicita** in questa esercitazione.

<!--
    This consent value can be verified by returning the JavaScript object ```klaro.getManager().consents``` in the browser's developer console.
-->
    >[!NOTE]
    >
    >In genere, i passaggi sopra indicati vengono eseguiti e gestiti dal team o dalla persona responsabile della gestione della CMP, ad esempio OneTrust o TrustArc.

## Iniettare una CMP

>[!WARNING]
>
>La best practice per implementare una piattaforma di gestione dei consensi consiste nel caricare la CMP _prima_ del caricamento del gestore di tag. Per facilitare questa esercitazione, caricherai CMP _con_ il gestore di tag. Questa lezione è progettata per mostrarti come utilizzare le funzioni di consenso in Platform Web SDK e non deve essere utilizzata come guida per configurare correttamente Klaro o qualsiasi altra CMP.


Ora, una volta completate le configurazioni di Klaro, crea regole tag con le seguenti configurazioni:

* [!UICONTROL Nome]: `all pages - library load - Klaro`
* [!UICONTROL Evento]: [!UICONTROL Libreria caricata (parte superiore della pagina)] con [!UICONTROL Opzioni avanzate] > [!UICONTROL Ordine] impostato su 1
* [!UICONTROL Azione]: [!UICONTROL Codice personalizzato], [!UICONTROL Lingua]: HTML per caricare lo script CMP.

![Inserisci regola CMP](assets/consent-cmp-inject-rule-1.png)

Il blocco di codice personalizzato deve essere simile al seguente:

![Inserisci regola CMP](assets/consent-cmp-inject-rule-2.png)

Ora salva e genera questa regola nella libreria di sviluppo, verifica che il banner di consenso venga visualizzato cambiando la libreria di tag dal sito Luma al tuo. Dovresti visualizzare un banner CMP sul sito web, come indicato di seguito. Inoltre, per verificare l’autorizzazione del consenso del visitatore corrente, puoi utilizzare il seguente frammento di codice nella console del browser.

```javascript
    klaro.getManager().consents 
```

![Banner di consenso](assets/consent-cmp-banner.png)

Per accedere alla modalità di debug, utilizza la seguente casella di controllo nel debugger di Adobe Experience Platform.

![Modalità debug tag](assets/consent-rule-debugging.png)

Inoltre, potrebbe essere necessario cancellare i cookie e l’archiviazione locale più volte durante l’esercitazione, poiché il valore di consenso del visitatore viene memorizzato lì. Puoi semplicemente farlo come segue:

![Cancellazione dell&#39;archiviazione](assets/consent-clearning-cookies.png)

## Scenari di consenso

Gli atti in materia di privacy come RGPD, CCPA e altri svolgono un ruolo fondamentale nel modo in cui vengono implementati i consensi. In questa lezione, esplori come un visitatore potrebbe interagire con il banner del consenso in base ai due atti sulla privacy più importanti.
![Scenari di consenso](assets/consent-scenarios.jpeg)


### Scenario 1: consenso implicito

Il consenso implicito significa che l’azienda non deve ottenere il consenso del visitatore (o il &quot;consenso&quot;) prima di raccogliere i propri dati, e quindi tutti i visitatori del sito web vengono trattati come consenso predefinito. Tuttavia, il visitatore può rinunciare rifiutando i cookie tramite il banner di consenso. Questo caso d’uso è simile al CCPA.

Ora configurerai e implementerai il consenso per questo scenario:

1. Nella sezione **[!UICONTROL Privacy]** dell&#39;estensione tag Experience Platform Web SDK, assicurati che il **[!UICONTROL consenso predefinito]** sia impostato su **[!UICONTROL In]**:


   ![Configurazione privacy estensione AEP](assets/consent-web-sdk-privacy-in.png)

   >[!NOTE]
   > 
   >Per una soluzione dinamica, selezionare l&#39;opzione &quot;Provide a data element&quot; (Fornisci un elemento dati) e passare un elemento dati che restituisca il valore di ```klaro.getManager().consents```
   >
   >Questa opzione viene utilizzata se la CMP viene inserita nel codice sorgente *prima* del codice di incorporamento del tag, in modo che il consenso predefinito sia disponibile prima che l&#39;estensione Experience Platform Web SDK inizi a essere caricata. Nel nostro esempio, non è possibile utilizzare questa opzione perché la CMP è caricata con i tag e non prima dei tag.



2. Salva e genera questa modifica nella libreria tag
3. Caricare la libreria di tag nel sito di dimostrazione Luma
4. Abilita il debug dei tag durante la visita al sito Luma e ricarica la pagina. Nella console per sviluppatori del browser, dovresti notare che defaultConsent è uguale a **[!UICONTROL In]**
5. Con questa configurazione, l’estensione Experience Platform Web SDK continua a effettuare richieste di rete, a meno che un visitatore non decida di rifiutare i cookie e la rinuncia:

   ![Consenso implicito Consenso negato](assets/consent-Implied-optin-default.png)



Se un visitatore decide di rinunciare (rifiutare i cookie di tracciamento), devi cambiare il consenso in **[!UICONTROL Out]**. Modifica l’impostazione del consenso seguendo questi passaggi:

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

1. Crea una regola che viene attivata quando il visitatore fa clic su **Rifiuto**.  Denomina questa regola come: `all pages - click consent banner - set consent "out"`

1. Come **[!UICONTROL Evento]**, utilizza **[!UICONTROL Clic]** su **[!UICONTROL Elementi che corrispondono al selettore CSS]** `#klaro .cn-decline`

   ![L&#39;utente della condizione della regola fa clic su &quot;Rifiuto&quot;](assets/consent-optOut-clickEvent.png)

1. Ora, utilizza Experience Platform Web SDK, [!UICONTROL Imposta consenso] [!UICONTROL tipo azione] per impostare il consenso come &quot;out&quot;:

   ![Azione di rinuncia regola di consenso](assets/consent-rule-optout-action.png)

1. Seleziona **[!UICONTROL Salva nella libreria e genera]**:

   ![Salva e genera la libreria](assets/consent-rule-optout-saveAndBuild.png)

Ora, quando un visitatore rinuncia, la regola configurata nel modo precedente si attiva e imposta il consenso di Web SDK come **[!UICONTROL Out]**.

Per eseguire la convalida, accedi al sito di dimostrazione Luma, rifiuta i cookie e verifica che non venga attivata alcuna richiesta di Web SDK dopo la rinuncia.

### Scenario 2: rinuncia implicita


La rinuncia implicita significa che i visitatori devono essere trattati come rinuncia per impostazione predefinita e i cookie non devono essere impostati. Le richieste di Web SDK non devono essere attivate a meno che i visitatori non decidano di acconsentire manualmente accettando i cookie tramite il banner di consenso. Potresti dover gestire un caso d’uso di questo tipo nell’area dell’Unione Europea in cui si applica il RGPD.

Ecco come impostare la configurazione per uno scenario di rinuncia implicita:

1. In Klaro, disattiva **Stato predefinito servizio** nel servizio `aep web sdk` e salva la configurazione aggiornata.

1. Nella sezione **[!UICONTROL Privacy]** dell&#39;estensione Experience Platform Web SDK, imposta il consenso predefinito su **[!UICONTROL Out]** o **[!UICONTROL Pending]** come richiesto.

   ![Configurazione privacy estensione AEP](assets/consent-implied-opt-out.png)

1. **Salva** la configurazione aggiornata nella libreria di tag e ricreala.

   Con questa configurazione, Experience Platform Web SDK garantisce che nessuna richiesta venga attivata a meno che l&#39;autorizzazione di consenso non cambi in **[!UICONTROL In]**. Ciò potrebbe verificarsi in seguito all’accettazione manuale dei cookie da parte di un visitatore che acconsente.

1. In Debugger, assicurati che il sito Luma sia mappato sulla proprietà tag e che la registrazione della console tag sia attiva.
1. Utilizza la console per sviluppatori del browser per **cancellare i dati del sito** in **Applicazione** > **Archiviazione**

1. Ricarica il sito Luma. `defaultConsent` è impostato su **[!UICONTROL Out]** e non sono state effettuate richieste Web SDK

   ![Consenso implicito Rinuncia](assets/consent-implied-out-cmp.png)

Se un visitatore decide di dare il consenso (accettare i cookie di tracciamento), devi modificare il consenso e impostarlo su **[!UICONTROL In]**. Ecco come eseguire questa operazione con una regola:

1. Crea una regola che viene attivata quando il visitatore fa clic su **Non importa**.  Denomina questa regola come: `all pages - click consent banner - set consent "in"`

1. Come **[!UICONTROL Evento]**, utilizza **[!UICONTROL Clic]** su **[!UICONTROL Elementi che corrispondono al selettore CSS]** `#klaro .cm-btn-success`

   ![L&#39;utente della condizione della regola fa clic su &quot;Tutto a posto&quot;](assets/consent-optIn-clickEvent.png)

1. Aggiungi un&#39;azione tramite l&#39;estensione [!UICONTROL &#x200B; di Experience Platform Web SDK, &#x200B;]Tipo azione **[!UICONTROL di]** Imposta consenso **[!UICONTROL ,]** Consenso generale **[!UICONTROL come]** In **[!UICONTROL .]**

   ![Azione Di Consenso Alla Regola Di Consenso](assets/consent-rule-optin-action.png)

   Tieni presente che questa azione [!UICONTROL Imposta consenso] sarà la prima richiesta inviata e stabilirà l&#39;identità. Per questo motivo, potrebbe essere importante sincronizzare le identità alla prima richiesta. È possibile aggiungere la mappa di identità all&#39;azione [!UICONTROL Imposta consenso] passando un elemento dati di tipo identità.

1. Seleziona **[!UICONTROL Salva nella libreria e genera]**:

   ![Rinuncia a una regola di consenso](assets/consent-rule-optin-saveAndBuild.png)

1. **[!UICONTROL Salva]** la regola nella libreria e ricreala.

Dopo aver impostato questa regola, la raccolta di eventi deve iniziare quando un visitatore acconsente.

![Consenso post visitatore Optin](assets/consent-post-user-optin.png)


Per ulteriori informazioni sul consenso in Web SDK, consulta [Preferenze di supporto del consenso dei clienti](https://experienceleague.adobe.com/en/docs/experience-platform/edge/consent/supporting-consent).


Per ulteriori informazioni sull&#39;azione [!UICONTROL Imposta consenso], vedere [Imposta consenso](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/action-types#set-consent).

>[!NOTE]
>
>Grazie per aver dedicato tempo all&#39;apprendimento di Adobe Experience Platform Web SDK. Se hai domande, vuoi condividere commenti generali o suggerimenti su contenuti futuri, condividili in questo [post di discussione della community Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
