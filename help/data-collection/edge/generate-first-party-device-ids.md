---
title: Generare ID dispositivo di prime parti
description: Scopri come generare ID dispositivo di prime parti
feature: Web SDK
level: Experienced
jira: KT-9728
thumbnail: KT-9728.jpeg
exl-id: 2e3c1f71-e224-4631-b680-a05ecd4c01e7
source-git-commit: fd60f7ad338c81f5b32e7951d5a00b49c5aa1756
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---

# Generare ID dispositivo di prime parti

Tradizionalmente, le applicazioni Adobe Experience Cloud generano cookie per memorizzare gli ID dispositivo utilizzando diverse tecnologie, tra cui:

1. Cookie di terze parti
1. Cookie di prime parti impostati da un server Adobe utilizzando la configurazione CNAME di un nome di dominio
1. Cookie di prime parti impostati da JavaScript

Le modifiche recenti apportate al browser limitano la durata di questi tipi di cookie. I cookie di prime parti sono più efficaci quando vengono impostati utilizzando un server di proprietà del cliente che utilizza un record A/AAAA DNS anziché un CNAME DNS. La funzionalità [ID dispositivo di prime parti (FPID)](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/identity/first-party-device-ids) consente ai clienti che implementano Adobe Experience Platform Web SDK di utilizzare gli ID dispositivo nei cookie dei server che utilizzano i record A/AAAA DNS. Questi ID possono quindi essere inviati ad Adobe e utilizzati come seed per generare Experience Cloud ID (ECID), che rimane l’identificatore primario nelle applicazioni Adobe Experience Cloud.

Di seguito è riportato un rapido esempio di come funziona la funzionalità:

![ID dispositivo di prime parti (FPID) e ID Experience Cloud (ECID)](../assets/kt-9728.png)

1. Il browser di un utente finale richiede una pagina web dal server web o dalla rete CDN di un cliente.
1. Il cliente genera un ID dispositivo (FPID) sul proprio server web o CDN (il server web deve essere associato al record A/AAAA DNS del nome di dominio).
1. Il cliente imposta un cookie di prima parte per memorizzare l’FPID nel browser dell’utente finale.
1. L’implementazione di Adobe Experience Platform Web SDK del cliente invia una richiesta all’Edge Network della piattaforma e:
   1. Include l&#39;FPID nella mappa di identità.
   1. Configura un CNAME per le richieste Web SDK e configura il relativo stream di dati con il nome del cookie FPID.
1. Experience Platform Edge Network riceve l’FPID e lo utilizza per generare un Experience Cloud ID (ECID).
1. La risposta di Platform Web SDK invia nuovamente l’ECID al browser dell’utente finale.
1. Se `idMigrationEnabled=true`, Platform Web SDK utilizza JavaScript per memorizzare l&#39;ECID come cookie `AMCV_` nel browser dell&#39;utente finale.
1. Nel caso in cui il cookie `AMCV_` scada, il processo si ripete. Se è disponibile lo stesso ID dispositivo di prima parte, viene creato un nuovo cookie `AMCV_` con lo stesso valore ECID di prima.

>[!NOTE]
>
>Non è necessario impostare `idMigrationEnabled` su `true` per utilizzare l&#39;FPID. Con `idMigrationEnabled=false` è possibile che non venga visualizzato un cookie `AMCV_` e che sia necessario cercare il valore ECID nella risposta di rete.


Per questo tutorial, viene utilizzato un esempio specifico che utilizza il linguaggio di script PHP per mostrare come:

* Generare un UUIDv4
* Scrivi il valore UUIDv4 in un cookie
* Includi il valore del cookie nella mappa di identità
* Convalidare la generazione di ECID

Ulteriori informazioni relative agli ID dispositivo di prime parti sono disponibili nella documentazione del prodotto.

## Generare un UUIDv4

PHP non dispone di una libreria nativa per la generazione di UUID, quindi questi esempi di codice sono più estesi di quanto sarebbe probabilmente necessario se fosse stato utilizzato un altro linguaggio di programmazione. Il PHP è stato scelto per questo esempio perché è un linguaggio lato server ampiamente supportato.


Quando viene chiamata la seguente funzione, genera un UUID versione-4 casuale:

```
<?php
    
    function guidv4($data)
    {
        $data = $data ?? random_bytes(16);

        $data[6] = chr(ord($data[6]) & 0x0f | 0x40); // set version to 0100
        $data[8] = chr(ord($data[8]) & 0x3f | 0x80); // set bits 6-7 to 10

        return vsprintf('%s%s-%s-%s-%s-%s%s%s', str_split(bin2hex($data), 4));
    }

?>
```

## Scrivi il valore UUIDv4 in un cookie

Il codice seguente invia una richiesta alla funzione precedente per generare un UUID. Quindi imposta i flag di cookie decisi dalla tua organizzazione. Se è già stato generato un cookie, la scadenza viene estesa.

```
<?php

    if(!isset($_COOKIE['FPID'])) {
        $cookie_value = guidv4(openssl_random_pseudo_bytes(16));        
        $arr_cookie_options = array (
        'expires' => time() + 60*60*24*30*13,
        'path' => '/',
        'domain' => 'mysiteurl.com',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'lax'
        );
        setcookie($cookie_name, $cookie_value, $arr_cookie_options);
        $_COOKIE[$cookie_name] = $cookie_value;
    }
    else {
        $cookie_value = $_COOKIE[$cookie_name];
        $arr_cookie_options = array (
        'expires' => time() + 60*60*24*30*13,
        'path' => '/',
        'domain' => 'mysiteurl.com',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'lax'
        );
        setcookie($cookie_name, $cookie_value, $arr_cookie_options);
    }

?>
```

>[!NOTE]
>
>Il cookie che contiene l’ID dispositivo di prime parti può avere qualsiasi nome.

## Includere il valore del cookie in Identity Map

Il passaggio finale consiste nell’utilizzare PHP per copiare il valore del cookie in Identity Map.


```
{
    "identityMap": {
        "FPID": [
                    {
                        "id": "<? echo $_COOKIE[$cookie_name] ?>",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
        }
}
```

>[!IMPORTANT]
>
>Il simbolo dello spazio dei nomi dell&#39;identità utilizzato nella mappa identità deve essere denominato `FPID`.
>
> `FPID` è uno spazio dei nomi di identità riservato non visibile negli elenchi di interfaccia degli spazi dei nomi di identità.


## Convalidare la generazione di ECID

Convalida l’implementazione confermando che lo stesso ECID viene generato dal tuo ID dispositivo di prime parti:

1. Genera un cookie FPID.
1. Invia una richiesta a Platform Edge Network utilizzando Platform Web SDK.
1. È stato generato un cookie con il formato `AMCV_<IMSORGID@AdobeOrg>`. Questo cookie contiene l’ECID.
1. Prendere nota del valore del cookie generato, quindi eliminare tutti i cookie del sito ad eccezione del cookie `FPID`.
1. Invia un’altra richiesta a Platform Edge Network.
1. Confermare che il valore nel cookie `AMCV_<IMSORGID@AdobeOrg>` è uguale al valore `ECID` del cookie `AMCV_` eliminato. Se il valore del cookie è lo stesso per un determinato FPID, il processo di seeding per l’ECID è riuscito.

Per ulteriori informazioni su questa funzione, consulta [la documentazione](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html).
