---
title: Abilitare il supporto tra più domini | Migrare Target da at.js 2.x all’SDK per web
description: Scopri come configurare Adobe Target per scenari di app mobili e tra domini diversi in browser web utilizzando Experience Platform Web SDK.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# Abilitare i profili visitatore tra più domini

L’SDK per web di Platform supporta le funzionalità di condivisione degli ID visitatore che consentono ai clienti di fornire esperienze personalizzate più accuratamente nei tuoi domini. Questa funzionalità ti consente di fornire una personalizzazione coerente tra i domini e di migliorare la precisione del reporting dell’attività del visitatore, senza ricorrere ai cookie di terze parti.

## Prerequisiti

Per utilizzare la condivisione di ID tra più domini, devi utilizzare la versione 2.11.0 o successiva dell’SDK per web di Platform. Questa funzionalità è compatibile anche con VisitorAPI.js versione 1.7.0 o successiva.

La condivisione degli ID tra domini diversi funziona aggiungendo uno speciale `adobe_mc` parametro della stringa di interrogazione per l&#39;URL del dominio di destinazione. Questo parametro viene utilizzato per specificare l&#39;ID visitatore anziché generare un nuovo ID o utilizzare un ID esistente.

Per elaborare il dominio di destinazione, il dominio di destinazione deve utilizzare una di queste librerie per la condivisione degli ID tra domini diversi `adobe_mc` e condividi correttamente l&#39;ID visitatore.

## Confronto dell&#39;approccio

Prima di implementare, verifica innanzitutto se l’implementazione esistente utilizza la funzione `visitor.appendVisitorIDsTo()` funzione . Eventuali codici personalizzati che utilizzano questa funzione devono essere aggiornati per utilizzare il nuovo `appendIdentityToUrl` Comando SDK per web.

| VisitorAPI.js | SDK Web per Platform |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## Utilizzo della `appendIdentityToURL` command

Per la condivisione di ID tra domini diversi, la versione 2.11.0 dell’SDK per web aggiunge il supporto per la `appendIdentityToUrl` comando. Se utilizzato, questo comando genera il `adobe_mc` parametro della stringa query.

Il comando accetta un oggetto con una proprietà, `url`e restituisce un oggetto con l&#39;url della proprietà.

Questo comando non attende alcun aggiornamento del consenso. Se non è stato fornito il consenso, l’URL viene restituito invariato.

Se non viene fornito un ECID, la variabile `/acquire` per generare un ECID viene chiamato l’endpoint .

Di seguito è riportato un esempio di come implementare la condivisione ID tra più domini.

Questo codice aggiunge un listener di eventi per tutti i clic sulla pagina. Se il clic si trovava su un collegamento a un dominio corrispondente, in questo caso adobe.com o Behance.com, aggiunge l&#39;identità all&#39;URL e reindirizzerà l&#39;utente a tale sito.

```Javascript
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

>[!TIP]
>
>Quando si utilizza la funzione tag (precedentemente Launch) per implementare l’SDK per web, la condivisione degli ID tra domini diversi può essere eseguita senza codice personalizzato. Fai riferimento a [documentazione dedicata](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension) per ulteriori dettagli.

>[!NOTE]
>
>L’SDK per web di Platform supporta anche la condivisione di ID da mobile a web per casi d’uso nativi di app per dispositivi mobili. Per ulteriori informazioni, consulta la documentazione dedicata sulle [condivisione di ID da mobile a web e tra più domini](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html).

Quindi, scopri come [aggiornare tipi di pubblico e script di profilo](update-audiences.md) per garantire la compatibilità con Platform Web SDK.

>[!NOTE]
>
>Ci impegniamo ad aiutarti a eseguire con successo la migrazione di Target da at.js all’SDK per web. Se incontri ostacoli con la tua migrazione o se ti senti che mancano informazioni critiche in questa guida, compila l&#39;invio del tuo messaggio [discussione comunitaria](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).