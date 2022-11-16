---
title: Creare regole per il tracciamento della visualizzazione della pagina e degli eventi di e-commerce
description: Creare regole per il tracciamento della visualizzazione della pagina e degli eventi di e-commerce
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 2dd02462-ddb5-4f67-8b0f-4a5bf5f7d655
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---

# Creare regole per il tracciamento della visualizzazione della pagina e degli eventi di e-commerce

Per verificare che l’utente abbia visualizzato la pagina del prodotto, crea una regola all’interno dei tag Adobe Experience Platform. Fai clic su [!UICONTROL Regole] nel menu a sinistra, quindi fai clic su [!UICONTROL Aggiungi regola].

Per il nome della regola, immetti _Pagina visualizzata_.

## Aggiungere un evento

Fai clic sul pulsante [!UICONTROL Aggiungi] pulsante sotto [!UICONTROL Eventi]. Ora puoi visualizzare la visualizzazione dell’evento. Per [!UICONTROL Estensione] campo , seleziona [!UICONTROL Livello dati client di Adobe]. Per [!UICONTROL Tipo evento] campo , seleziona [!UICONTROL Dati scaricati].

Perché desideri che questa regola venga attivata solo quando `pageViewed` l&#39;evento viene inviato al livello dati, seleziona [!UICONTROL Evento specifico] sotto [!UICONTROL Ascolta] e tipo _pageViewed_ nel [!UICONTROL Evento / Chiave per la registrazione] campo di testo.

![Evento visualizzato nella pagina](../../../assets/implementation-strategy/page-viewed-event.png)

Fai clic su [!UICONTROL Mantieni modifiche].

## Aggiungi un&#39;azione

Ora che ti trovi nuovamente nella visualizzazione delle regole, fai clic sul pulsante [!UICONTROL Aggiungi] pulsante sotto [!UICONTROL Azioni]. Ora dovresti essere nella visualizzazione delle azioni. Per [!UICONTROL Estensione] campo , seleziona [!UICONTROL Adobe Experience Platform Web SDK]. Per [!UICONTROL Tipo di azione] campo , seleziona [!UICONTROL Invia evento]. Questa azione ti consente di inviare un evento di esperienza a Adobe Experience Platform Edge Network.

Sul lato destro dello schermo, trova la [!UICONTROL Tipo] campo e seleziona `web.webpagedetails.pageViews`. Questo è uno dei tipi di evento esperienza canonico forniti da Adobe Experience Platform. Rappresenta una visualizzazione di pagina.

Per [!UICONTROL Dati XDM] campo, immettere `%event.fullState%`. Questo indica che lo stato calcolato (noto anche come stato completo) del livello dati, che viene acquisito al momento dell&#39;attivazione della regola, deve essere inviato come parte dell&#39;evento di esperienza.

![Azione visualizzata nella pagina](../../../assets/implementation-strategy/page-viewed-action.png)

Se i dati inviati dal sito web al livello dati non sono conformi allo schema XDM o se desideri inviare solo una parte dello stato calcolato del livello dati, utilizza il [!UICONTROL Oggetto XDM] tipo di elemento dati (fornito dall&#39;estensione Adobe Experience Platform Web SDK) per creare un oggetto appropriato che corrisponda allo schema.

Fai clic sul pulsante [!UICONTROL Mantieni modifiche.]

## Salva la regola

La regola dovrebbe ora essere completa.

![Regola visualizzata nella pagina](../../../assets/implementation-strategy/page-viewed-rule.png)

Salva la regola facendo clic su [!UICONTROL Salva].

## Ripeti il processo

Ripeti il processo descritto sopra per creare regole per quando un prodotto viene visualizzato, viene aperto un carrello e viene aggiunto un prodotto al carrello. Le uniche differenze tra le regole saranno il nome della regola e il valore inserito nella [!UICONTROL Evento / Chiave per la registrazione] nel campo [!UICONTROL Dati scaricati] e [!UICONTROL Tipo] nel campo [!UICONTROL Invia evento] azione. Di seguito sono riportati i valori per ogni regola:

Regola visualizzata dal prodotto:

* **Nome della regola**: _Prodotto visualizzato_
* **Evento / Chiave per la registrazione** entro [!UICONTROL Dati scaricati] evento: `productViewed`
* **Tipo** entro [!UICONTROL Invia evento] azione: `commerce.productViews`

Regola aperta del carrello:

* **Nome della regola**: _Carrello aperto_
* **Evento / Chiave per la registrazione** entro [!UICONTROL Dati scaricati] evento: `cartOpened`
* **Tipo** entro [!UICONTROL Invia evento] azione: `commerce.productListOpens`

Prodotto aggiunto alla regola del carrello:

* **Nome della regola**: _Prodotto Aggiunto Al Carrello_
* **Evento / Chiave per la registrazione** entro [!UICONTROL Dati scaricati] evento: `productAddedToCart`
* **Tipo** entro [!UICONTROL Invia evento] azione: `commerce.productListAdds`

Ora, gestiremo i clic di tracciamento sul [!UICONTROL Scaricare l’app] link.
