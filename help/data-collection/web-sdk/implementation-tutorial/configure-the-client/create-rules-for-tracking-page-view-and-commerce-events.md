---
title: Creare regole per il tracciamento della visualizzazione di pagina e degli eventi di e-commerce
description: Creare regole per il tracciamento della visualizzazione di pagina e degli eventi di e-commerce
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 2dd02462-ddb5-4f67-8b0f-4a5bf5f7d655
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---

# Creare regole per il tracciamento della visualizzazione di pagina e degli eventi di e-commerce

Per tenere traccia del fatto che l’utente ha visualizzato la pagina del prodotto, crea una regola all’interno dei tag di Adobe Experience Platform. Per farlo, fai clic su [!UICONTROL Regole] nel menu a sinistra, quindi fai clic su [!UICONTROL Aggiungi regola].

Per il nome della regola, immetti _Pagina visualizzata_.

## Aggiungere un evento

Fai clic su [!UICONTROL Aggiungi] pulsante sotto [!UICONTROL Eventi]. Ora mostri di essere nella visualizzazione evento. Per [!UICONTROL Estensione] campo, seleziona [!UICONTROL Adobe Client Data Layer]. Per [!UICONTROL Tipo di evento] campo, seleziona [!UICONTROL Dati inviati].

Perché desideri che questa regola venga attivata solo quando `pageViewed` viene inviato al livello dati, seleziona [!UICONTROL Evento specifico] in [!UICONTROL Ascolta] e tipo _pageViewed_ in [!UICONTROL Evento/Chiave per cui registrarsi] campo di testo.

![Evento di visualizzazione pagina](../../../assets/implementation-strategy/page-viewed-event.png)

Clic [!UICONTROL Mantieni modifiche].

## Aggiungi un&#39;azione

Ora che sei tornato alla visualizzazione della regola, fai clic sul pulsante [!UICONTROL Aggiungi] pulsante sotto [!UICONTROL Azioni]. Ora dovresti essere nella visualizzazione azione. Per [!UICONTROL Estensione] campo, seleziona [!UICONTROL Adobe Experience Platform Web SDK]. Per [!UICONTROL Tipo di azione] campo, seleziona [!UICONTROL Invia evento]. Questa azione ti consente di inviare un evento esperienza a Adobe Experience Platform Edge Network.

Sul lato destro dello schermo, individua [!UICONTROL Tipo] e seleziona `web.webpagedetails.pageViews`. Questo è uno dei tipi canonici di Evento esperienza che Adobe Experience Platform fornisce come impostazione predefinita. Rappresenta una visualizzazione pagina.

Per [!UICONTROL Dati XDM] campo, immetti `%event.fullState%`. Questo indica che lo stato calcolato (noto anche come stato completo) del livello dati, che viene acquisito al momento in cui la regola è stata attivata, deve essere inviato come parte dell’evento esperienza.

![Azione pagina visualizzata](../../../assets/implementation-strategy/page-viewed-action.png)

Se i dati inviati al livello dati dal sito web non sono conformi allo schema XDM, o se desideri inviare solo una parte dello stato calcolato del livello dati, utilizza [!UICONTROL Oggetto XDM] tipo di elemento dati (fornito dall’estensione Adobe Experience Platform Web SDK) per generare un oggetto appropriato che corrisponda allo schema.

Fai clic sul pulsante [!UICONTROL Mantieni modifiche.]

## Salva la regola

La regola ora dovrebbe essere completa.

![Regola di visualizzazione pagina](../../../assets/implementation-strategy/page-viewed-rule.png)

Salva la regola facendo clic su [!UICONTROL Salva].

## Ripeti il processo

Ripeti il processo descritto in precedenza per creare regole per quando un prodotto viene visualizzato, viene aperto un carrello e un prodotto viene aggiunto al carrello. Le uniche differenze tra le regole saranno il nome della regola, il valore immesso nel [!UICONTROL Evento/Chiave per cui registrarsi] campo in [!UICONTROL Dati inviati] e [!UICONTROL Tipo] campo in [!UICONTROL Invia evento] azione. Di seguito sono riportati i valori per ogni regola:

Regola visualizzata sul prodotto:

* **Nome regola**: _Prodotto visualizzato_
* **Evento/Chiave per cui registrarsi** entro [!UICONTROL Dati inviati] evento: `productViewed`
* **Tipo** entro [!UICONTROL Invia evento] azione: `commerce.productViews`

Regola carrello aperto:

* **Nome regola**: _Carrello aperto_
* **Evento/Chiave per cui registrarsi** entro [!UICONTROL Dati inviati] evento: `cartOpened`
* **Tipo** entro [!UICONTROL Invia evento] azione: `commerce.productListOpens`

Prodotto aggiunto alla regola del carrello:

* **Nome regola**: _Prodotto aggiunto al carrello_
* **Evento/Chiave per cui registrarsi** entro [!UICONTROL Dati inviati] evento: `productAddedToCart`
* **Tipo** entro [!UICONTROL Invia evento] azione: `commerce.productListAdds`

Ora gestiremo il tracciamento dei clic sul [!UICONTROL Scaricare l’app] collegamento.
