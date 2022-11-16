---
title: Prendi in considerazione lo spostamento dei tag fornitore all'inoltro eventi
description: Scopri come valutare un tag fornitore lato client per la distribuzione dei dati lato server.
feature: Event Forwarding, Tags, Integrations
solution: Data Collection
kt: 9921
level: Intermediate, Experienced
role: Admin, Developer, Architect
exl-id: f8fd351a-435c-4cc1-b987-ed2ead20d4d6
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 3%

---

# Prendi in considerazione lo spostamento di tag fornitore lato client all’inoltro eventi

Ci sono diversi motivi convincenti per considerare lo spostamento di tag fornitore lato client da browser e dispositivi e su un server. In questo articolo viene illustrato come valutare un tag fornitore lato client per spostarlo potenzialmente in una proprietà di inoltro eventi.

Questa valutazione è necessaria solo se stai considerando di rimuovere un tag fornitore lato client e sostituirlo con la distribuzione dei dati lato server in una proprietà di inoltro eventi. Questo articolo presuppone che tu abbia familiarità con le nozioni di base di [raccolta dati](https://experienceleague.adobe.com/docs/data-collection.html)e [inoltro eventi](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html).

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) come riferimento consolidato delle modifiche terminologiche.

I fornitori di browser stanno modificando il modo in cui trattano i cookie di terze parti. I fornitori e le tecnologie di pubblicità e marketing spesso richiedono l’uso di molti tag lato client. Queste sfide sono solo due ragioni convincenti per cui i nostri clienti stanno aggiungendo la distribuzione dei dati lato server.

>[!NOTE]
>
>`Tag` in questo articolo significa codice lato client, in genere JavaScript di un fornitore utilizzato per la raccolta di dati nel browser o nel dispositivo mentre un visitatore interagisce con il sito o l&#39;app. `Website` o `site` qui si riferisce a un sito web, un’applicazione web o un’applicazione per un dispositivo mobile. Un &quot;tag&quot; per questi scopi viene spesso chiamato anche pixel.

## Casi di utilizzo e dati {#use-cases-data}

Il primo passaggio consiste nel definire i casi di utilizzo implementati con il tag fornitore lato client. Ad esempio, considera il pixel Facebook (Meta). Spostamento dal sito a [API di conversione facebook](https://exchange.adobe.com/apps/ec/105509/facebook-conversions-api-extension) con l&#39;estensione di inoltro eventi significa prima documentare i casi d&#39;uso specifici.

Per il codice fornitore lato client corrente:

- Quale evento specifico e altri punti dati vengono esposti e passati al tag lato client?
- Quando e dove avviene il trasferimento dei dati?

È utile creare un elenco, un foglio di calcolo, un diagramma o un altro record dei dati e della sequenza di eventi per documentare questa valutazione, anche se è solo per il tuo utilizzo. Accertati di includere etichette per le origini dati, da dove vengono? Destinazioni: dove va? E le trasformazioni - cosa le succede tra sorgente e destinazione?

Nel nostro esempio, monitoriamo le conversioni con il pixel di Facebook quando i visitatori interagiscono con il nostro sito dopo aver visualizzato un annuncio Facebook. Potrebbero anche interagire con il nostro sito dopo aver visualizzato annunci correlati su un&#39;altra piattaforma social. Per visualizzare queste conversioni negli strumenti e nei rapporti pubblicitari di Facebook, i dati richiesti devono arrivare a Facebook. Questi dati possono includere eventi di conversione come download, registrazioni, Mi piace o acquisti.

### Dati {#data}

Con il tag lato client esistente, quando viene eseguito o eseguito sul nostro sito, cosa succede con i dati del nostro caso d’uso? È possibile acquisire i dati di cui abbiamo bisogno nel client, senza il tag fornitore, in modo da poterli inviare all’inoltro degli eventi? Quando utilizzi [tag](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) Per altri sistemi di gestione dei tag, la maggior parte dei dati di interazione dei visitatori è disponibile per la raccolta e la distribuzione. Ma i dati di cui abbiamo bisogno per il nostro caso d&#39;uso sono disponibili quando ne abbiamo bisogno, dove ne abbiamo bisogno e nel formato di cui abbiamo bisogno, senza il tag del fornitore lato client? Seguono alcune ulteriori domande da prendere in considerazione:

- È richiesto un ID utente fornitore per ogni evento?
- In caso affermativo, come può essere raccolto o generato senza il tag lato client?
- Il fornitore richiede in modo specifico il proprio codice lato client in fase di esecuzione?
- Quali altri dati sono richiesti? Da dove verranno quei dati?

La maggior parte dei tag fornitore lato client non richiede molti punti dati per un caso d’uso particolare, ma è utile notare i casi d’uso e i dati richiesti durante queste valutazioni.

## API fornitore {#vendor-apis}

Ora conosciamo i casi d’uso specifici da implementare, i dati richiesti e la sequenza di eventi dall’origine alla destinazione. Per determinare se il caso d’uso è adatto per l’inoltro di eventi, ora possiamo esaminare i dettagli dell’API del fornitore.

>[!IMPORTANT]
>
>Anche se molti fornitori abilitano le API per il trasferimento server-to-server, ce ne sono anche molti che al momento non dispongono di API adatte a questi scopi.

### Indagine sulle API {#investigate-apis}

Di seguito sono riportati alcuni passi che possiamo intraprendere per indagare sugli endpoint API dei fornitori.

Il fornitore dispone di API progettate per il trasferimento server-to-server dei dati evento? Per prima cosa, trova i requisiti per gli endpoint API specifici:

- Gli endpoint API esistono per inviare i dati richiesti? Per trovare gli endpoint che supportano i casi d’uso, consulta la documentazione per sviluppatori o API del fornitore.
- Consentono lo streaming dei dati evento o solo dei dati batch?
- Quali metodi di autenticazione supportano? Token, HTTP, versione delle credenziali client OAuth o altro? Vedi [qui](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) per i metodi supportati dall&#39;inoltro eventi.
- Qual è l’offset di aggiornamento della relativa API? Questa limitazione è compatibile con i requisiti minimi di inoltro degli eventi? Dettagli [qui](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html#:~:text=you%20can%20configure%20the%20Refresh%20Offset%20value%20for%20the%20secret).
- Di quali dati hanno bisogno per gli endpoint pertinenti?
- Richiedono un identificatore utente specifico del fornitore con ogni chiamata all’endpoint?
- Se richiedono tale identificatore, dove e come può essere generato o acquisito senza codice lato client?

In altre parole:

- Il fornitore fornisce gli endpoint API richiesti per i nostri casi d’uso?
- Dispongono di un metodo di autenticazione compatibile per l&#39;inoltro di eventi?
- Posso accedere a tutti i dati necessari per un&#39;implementazione di inoltro eventi (dal lato client o da altre chiamate API)?

Il tag è probabilmente un buon candidato per passare dal client ai nostri server in una proprietà di inoltro di eventi se possiamo rispondere sì a tali domande.

Se il fornitore non dispone degli endpoint API per supportare i nostri casi di utilizzo, allora ovviamente il tag fornitore non è un buon candidato per l’utilizzo dell’inoltro eventi al posto del tag fornitore lato client.

Cosa succede se dispongono di API, ma richiedono anche un ID visitatore o utente univoco con ogni chiamata API? Come posso accedere a tale ID se sul sito non è in esecuzione il codice lato client (tag) del fornitore?

Alcuni fornitori stanno cambiando i loro sistemi per il nuovo mondo senza cookie di terze parti. Queste modifiche includono l’uso di identificatori univoci alternativi, come un [UUID](https://developer.mozilla.org/en-US/docs/Glossary/UUID) o altro [ID generato dal cliente](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html). Se il fornitore consente un ID generato dal cliente, possiamo inviarlo dal client a Platform Edge Network con Web o Mobile SDK oppure recuperarlo da una chiamata API in caso di inoltro. Quando inviamo dati a quel fornitore in una regola di inoltro eventi, includiamo semplicemente l&#39;identificatore in base alle esigenze.

Se il fornitore richiede dati (ad esempio un ID univoco specifico per il fornitore) che possono essere generati o accessibili solo dal proprio tag lato client, è probabile che il tag fornitore non sia un buon candidato per lo spostamento. _Il tentativo di decodificare un tag lato client con l’idea di spostare la raccolta dati all’inoltro degli eventi senza le API appropriate è scoraggiato._

La [Connettore Adobe Experience Platform Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/cloud-connector/overview.html) L&#39;estensione può effettuare richieste HTTP in base alle esigenze con i fornitori che dispongono delle API appropriate per il trasferimento dei dati evento da server a server. Anche se è bene avere estensioni specifiche per il fornitore e al momento sono in fase di sviluppo attivo più estensioni, è possibile implementare regole di inoltro eventi oggi tramite l’estensione Cloud Connector, senza attendere ulteriori estensioni del fornitore.

## Strumenti {#tools}

Indagare e testare gli endpoint API dei fornitori è più semplice con strumenti come [Postman](https://www.postman.com/)o estensioni di editor di testo come Visual Studio Code [Client Thunder](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)oppure [Client HTTP](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-http-client).

## Passaggi successivi {#next-steps}

Questo articolo fornisce una sequenza di passaggi per valutare un tag lato client del fornitore e potenzialmente spostarlo lato server in una proprietà di inoltro eventi. Per ulteriori informazioni sugli argomenti correlati, consulta questi collegamenti:

- [Gestione dei tag](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) in Adobe Experience Platform
- [Inoltro eventi](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) per elaborazione lato server
- [Aggiornamenti terminologici](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) nella raccolta dati
