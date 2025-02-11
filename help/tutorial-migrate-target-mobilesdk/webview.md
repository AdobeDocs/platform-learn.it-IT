---
title: 'Abilitare il supporto tra più domini: migrazione da Adobe Target a Adobe Journey Optimizer, estensione Decisioning per dispositivi mobili'
description: Scopri come configurare Adobe Target per app mobili e tra domini diversi in scenari di browser web utilizzando Experience Platform Web SDK.
exl-id: 1dc78771-b85c-4127-8d1b-6558509f9db8
source-git-commit: 18f0190881d2a997491d4d6ce367add74cc30288
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---

# Abilitare i profili dei visitatori tra domini

Platform Web SDK supporta le funzionalità di condivisione degli ID visitatore, che consentono ai clienti di fornire esperienze personalizzate in modo più accurato nei vari domini. Questa funzionalità ti consente di fornire una personalizzazione coerente tra i domini e di migliorare la precisione dei rapporti sull’attività dei visitatori, senza ricorrere a cookie di terze parti.

## Prerequisiti

Per utilizzare la condivisione ID tra domini diversi, è necessario utilizzare Platform Web SDK versione 2.11.0 o successiva. Questa funzionalità è compatibile anche con VisitorAPI.js versione 1.7.0 o successiva.

La condivisione degli ID tra domini diversi funziona aggiungendo un parametro speciale della stringa di query `adobe_mc` all&#39;URL del dominio di destinazione. Questo parametro viene utilizzato per specificare l’ID visitatore invece di generare un nuovo ID o di utilizzare un ID esistente.

Il dominio di destinazione deve utilizzare una di queste librerie per la condivisione degli ID tra domini diversi per elaborare il parametro `adobe_mc` e condividere correttamente l&#39;ID visitatore.

## Confronto degli approcci

Prima di implementare, verifica se l&#39;implementazione esistente utilizza la funzione `visitor.appendVisitorIDsTo()`. Qualsiasi codice personalizzato che utilizza questa funzione deve essere aggiornato per utilizzare il nuovo comando `appendIdentityToUrl` Web SDK.

| VisitorAPI.js | SDK Web per Platform |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## Utilizzo del comando `appendIdentityToURL`

Per la condivisione ID tra domini diversi, Web SDK versione 2.11.0 aggiunge il supporto per il comando `appendIdentityToUrl`. Se utilizzato, questo comando genera il parametro stringa query `adobe_mc`.

Il comando accetta un oggetto con una proprietà, `url`, e restituisce un oggetto con l&#39;URL della proprietà.

Questo comando non attende alcun aggiornamento del consenso. Se non è stato fornito il consenso, l’URL viene restituito invariato.

Se non viene fornito un ECID, l&#39;endpoint `/acquire` viene chiamato per generare un ECID.

Di seguito è riportato un esempio di come implementare la condivisione ID tra più domini.

Questo codice aggiunge un listener di eventi per tutti i clic sulla pagina. Se il clic si trovava su un collegamento a un dominio corrispondente, in questo caso adobe.com o behance.com, aggiunge l’identità all’URL e reindirizza l’utente lì.

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
>Quando si utilizza la funzione dei tag (precedentemente Launch) per implementare Web SDK, la condivisione degli ID tra domini diversi può essere eseguita senza codice personalizzato. Per ulteriori informazioni, consulta la [documentazione dedicata](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension).

>[!NOTE]
>
>Platform Web SDK supporta anche la condivisione di ID da dispositivo mobile a web per i casi d’uso nativi delle app mobili. Per ulteriori informazioni, consulta la documentazione dedicata su [condivisione ID da dispositivo mobile a Web e tra domini](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html).

Successivamente, scopri come [aggiornare tipi di pubblico e script di profilo](update-audiences.md) per garantire la compatibilità con Platform Web SDK.

>[!NOTE]
>
>Ci impegniamo ad aiutarti ad effettuare con successo la migrazione di Target mobile dall’estensione Target all’estensione Decisioning. Se incontri ostacoli con la migrazione o pensi che in questa guida manchino informazioni critiche, inviaci [questa discussione della community](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
