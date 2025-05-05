---
title: Prendi in considerazione lo spostamento di tag fornitore all’inoltro eventi
description: Scopri come valutare un tag fornitore lato client per la distribuzione dei dati lato server.
feature: Event Forwarding, Tags, Integrations
role: Admin, Developer, Architect, Data Engineer
level: Intermediate, Experienced
jira: KT-9921
exl-id: f8fd351a-435c-4cc1-b987-ed2ead20d4d6
source-git-commit: 7edf8fc46943ae2f1e6e2e20f4d589d7959310c8
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 2%

---

# Prendi in considerazione lo spostamento di tag fornitore lato client all’inoltro eventi

Ci sono diversi motivi validi per prendere in considerazione lo spostamento di tag fornitore lato client da browser e dispositivi e su un server. In questo articolo viene descritto come valutare un tag fornitore lato client per spostarlo potenzialmente in una proprietà di inoltro eventi.

Questa valutazione è necessaria solo se stai valutando di rimuovere un tag fornitore lato client e sostituirlo con la distribuzione dei dati lato server in una proprietà di inoltro degli eventi. In questo articolo si presuppone che tu abbia familiarità con le nozioni di base di [raccolta dati](https://experienceleague.adobe.com/docs/data-collection.html?lang=it) e [inoltro eventi](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=it).

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=it) come riferimento consolidato delle modifiche terminologiche.

I fornitori di browser stanno cambiando il modo in cui trattano i cookie di terze parti. I fornitori e le tecnologie Advertising e marketing richiedono spesso l’utilizzo di molti tag lato client. Queste sfide sono solo due ragioni convincenti per cui i nostri clienti stanno aggiungendo la distribuzione dei dati lato server.

>[!NOTE]
>
>`Tag` in questo articolo significa codice lato client, in genere JavaScript di un fornitore utilizzato per la raccolta dati nel browser o nel dispositivo mentre un visitatore interagisce con il sito o l&#39;app. `Website` o `site` fa riferimento a un sito Web, un&#39;applicazione Web o un&#39;applicazione per un dispositivo mobile. Un &quot;tag&quot; per questi scopi è spesso chiamato anche pixel.

## Casi d’uso e dati {#use-cases-data}

Il primo passaggio consiste nel definire i casi d’uso implementati con il tag fornitore lato client. Ad esempio, considera il pixel Facebook (Meta). Spostarlo dal sito all&#39;API [Meta Conversions](https://exchange.adobe.com/apps/ec/109168/meta-conversions-api) con l&#39;estensione di inoltro degli eventi significa documentare prima i casi d&#39;uso specifici.

Per il codice fornitore lato client corrente:

- Quali eventi specifici e altri punti dati vengono esposti e passati al tag lato client?
- Quando e dove avviene il trasferimento dei dati?

È utile creare un elenco, un foglio di calcolo, un diagramma o un altro record dei dati e della sequenza di eventi per documentare questa valutazione, anche se è solo per uso personale. Assicurarsi di includere etichette per le origini dati, da dove provengono? Destinazioni: dove va a finire? E le trasformazioni: cosa succede tra origine e destinazione?

Nel nostro esempio, monitoriamo le conversioni con il pixel di Facebook quando i visitatori interagiscono con il nostro sito dopo aver visualizzato un annuncio Facebook. Potrebbero anche interagire con il nostro sito dopo aver visualizzato annunci correlati su un’altra piattaforma social. Per visualizzare queste conversioni negli strumenti pubblicitari e nei rapporti di Facebook, i dati richiesti devono arrivare a Facebook. Questi dati possono includere eventi di conversione come download, registrazioni, Mi piace o acquisti.

### Dati {#data}

Con il tag lato client esistente, quando viene eseguito o eseguito sul sito, cosa succede con i dati del caso d’uso? Possiamo acquisire i dati di cui abbiamo bisogno nel client, senza il tag del fornitore, in modo da poterli inviare all’inoltro degli eventi? Quando si utilizzano [tag](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it) o altri sistemi di gestione dei tag, la maggior parte dei dati di interazione del visitatore è disponibile per la raccolta e la distribuzione. Ma i dati di cui abbiamo bisogno per il nostro caso d’uso sono disponibili quando ne abbiamo bisogno, dove ne abbiamo bisogno e nel formato che ci serve, senza il tag fornitore lato client? Ecco alcune ulteriori domande sui dati da considerare:

- È necessario un ID utente fornitore per ogni evento?
- In caso affermativo, come può essere raccolta o generata senza il tag lato client?
- Il fornitore richiede specificamente il proprio codice lato client in fase di runtime?
- Quali altri dati sono richiesti? Da dove verranno quei dati?

La maggior parte dei tag fornitore lato client non richiede molti punti dati per qualsiasi caso d’uso particolare, ma è utile notare i casi d’uso e i dati richiesti durante queste valutazioni.

## API fornitore {#vendor-apis}

Ora conosciamo i casi d’uso specifici da implementare, i dati richiesti e la sequenza di eventi dal sorgente alla destinazione. Per determinare se il caso d’uso è adatto per l’inoltro di eventi, ora possiamo esaminare i dettagli API del fornitore.

>[!IMPORTANT]
>
>Anche se molti fornitori stanno abilitando le API per il trasferimento da server a server, ce ne sono molti che attualmente non dispongono di API adatte a questi scopi.

### Analisi delle API {#investigate-apis}

Di seguito sono riportati alcuni passaggi che è possibile eseguire per analizzare gli endpoint API del fornitore.

Il fornitore dispone di API progettate per il trasferimento server-to-server dei dati evento? In primo luogo, individua i requisiti per questi endpoint API specifici:

- Esistono gli endpoint API per inviare i dati richiesti? Per trovare gli endpoint che supportano i casi di utilizzo, consulta la documentazione per sviluppatori o API del fornitore.
- Consentono dati di eventi in streaming o solo dati batch?
- Quali metodi di autenticazione sono supportati? Token, HTTP, versione delle credenziali client OAuth o altro? Consulta [qui](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=it) per i metodi supportati dall&#39;inoltro di eventi.
- Qual è lo scostamento di aggiornamento delle loro API? Questa limitazione è compatibile con i minimi di inoltro degli eventi? Dettagli [qui](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=it#:~:text=you%20can%20configure%20the%20Refresh%20Offset%20value%20for%20the%20secret).
- Quali dati richiedono per gli endpoint rilevanti?
- Richiedono un identificatore utente specifico del fornitore per ogni chiamata all’endpoint?
- Se richiedono tale identificatore, dove e come può essere generato o acquisito, senza codice lato client?

In altre parole:

- Il fornitore fornisce gli endpoint API necessari per i nostri casi d’uso?
- Dispongono di un metodo di autenticazione compatibile per l’inoltro degli eventi?
- Possiamo accedere a tutti i dati necessari per l’implementazione di inoltro degli eventi (dal lato client o da altre chiamate API)?

Il tag è probabilmente un buon candidato per passare dal client ai nostri server in una proprietà di inoltro degli eventi se possiamo rispondere affermativamente a tali domande.

Se il fornitore non dispone degli endpoint API per supportare i nostri casi d’uso, allora ovviamente quel tag fornitore non è adatto per l’utilizzo dell’inoltro eventi al posto del tag fornitore lato client.

Cosa succede se dispongono di API, ma richiedono anche un ID visitatore o utente univoco per ogni chiamata API? Come possiamo accedere a tale ID se il codice lato client (tag) del fornitore non è in esecuzione sul sito?

Alcuni fornitori stanno cambiando i loro sistemi per il nuovo mondo senza cookie di terze parti. Queste modifiche includono l&#39;uso di identificatori univoci alternativi, come un [UUID](https://developer.mozilla.org/en-US/docs/Glossary/UUID) o un altro [ID generato dal cliente](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html?lang=it). Se il fornitore consente un ID generato dal cliente, possiamo inviarlo dal client all’Edge Network di Platform con Web SDK o Mobile SDK, oppure possiamo riceverlo da una chiamata API nell’inoltro degli eventi. Quando inviamo i dati a quel fornitore in una regola di inoltro degli eventi, includiamo semplicemente l’identificatore in base alle esigenze.

Se il fornitore richiede dati (ad esempio, un ID univoco specifico del fornitore) che possono essere generati o accessibili solo dal proprio tag lato client, è probabile che il tag del fornitore non sia adatto allo spostamento. _Si sconsiglia di decodificare un tag lato client con l&#39;idea di spostare la raccolta dati nell&#39;inoltro eventi senza le API appropriate._

L&#39;estensione [Adobe Experience Platform Cloud Connector](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/cloud-connector/overview.html?lang=it) può effettuare richieste HTTP in base alle esigenze con i fornitori che dispongono delle API appropriate per il trasferimento dei dati evento server-to-server. Anche se è preferibile avere estensioni specifiche per fornitore e al momento altre estensioni sono in fase di sviluppo attivo, è possibile implementare oggi le regole di inoltro degli eventi utilizzando l’estensione Cloud Connector, senza attendere estensioni aggiuntive per il fornitore.

## Strumenti {#tools}

L&#39;analisi e la verifica degli endpoint API del fornitore sono più semplici con strumenti come [Postman](https://www.postman.com/) o estensioni dell&#39;editor di testo come Visual Studio Code [Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client) o [HTTP Client](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-http-client).

## Passaggi successivi {#next-steps}

Questo articolo fornisce una sequenza di passaggi per valutare un tag lato client del fornitore e potenzialmente spostarlo lato server in una proprietà di inoltro degli eventi. Per ulteriori informazioni sugli argomenti correlati, vedere i collegamenti seguenti:

- [Gestione tag](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=it) in Adobe Experience Platform
- [Inoltro eventi](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=it) per elaborazione lato server
- [Aggiornamenti terminologici](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=it) nella raccolta dati
