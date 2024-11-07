---
title: Adobe Journey Optimizer - API meteo esterna, SMS e altro ancora - Definire un’origine dati esterna
description: Adobe Journey Optimizer - API meteo esterna, SMS e altro ancora - Definire un’origine dati esterna
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 3%

---

# 3.2.2 Definire una sorgente di dati esterna

In questo esercizio creerai un’origine dati esterna personalizzata utilizzando Adobe Journey Optimizer.

Accedi a Adobe Journey Optimizer da [Adobe Experience Cloud](https://experience.adobe.com). Fare clic su **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Verrai reindirizzato alla visualizzazione **Home** in Journey Optimizer. Innanzitutto, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare si chiama `--aepSandboxId--`. Per passare da una sandbox all&#39;altra, fare clic su **Production Prod (VA7)** e selezionare la sandbox dall&#39;elenco. In questo esempio, la sandbox è denominata **AEP Enablement FY22**. Ti troverai quindi nella **Home** della tua sandbox `--aepSandboxId--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

Nel menu a sinistra, scorri verso il basso e fai clic su **Configurazioni**. Fare clic sul pulsante **Gestisci** in **Origini dati**.

![Demo](./images/menudatasources.png)

Verrà quindi visualizzato l&#39;elenco **Origini dati**.
Fai clic su **Crea Source dati** per iniziare ad aggiungere la tua origine dati.

![Demo](./images/dshome.png)

Verrà visualizzata una finestra a comparsa dell&#39;origine dati vuota.

![Demo](./images/emptyds.png)

Prima di iniziare la configurazione, è necessario un account con il servizio **Apri mappa meteo**. Per creare l’account e ottenere la chiave API, segui la procedura riportata di seguito.

Vai a [https://openweathermap.org/](https://openweathermap.org/). Nella home page fare clic su **Accedi**.

![MappaMeteo](./images/owm.png)

Fai clic su **Crea un account**.

![MappaMeteo](./images/owm1.png)

Compila i dettagli.

![MappaMeteo](./images/owm2.png)

Fare clic su **Crea account**.

![MappaMeteo](./images/owm3.png)

Verrai quindi reindirizzato alla pagina del tuo account.

![MappaMeteo](./images/owm4.png)

Nel menu, fai clic su **Chiavi API** per recuperare la tua chiave API, che dovrai impostare l&#39;origine dati esterna personalizzata.

![MappaMeteo](./images/owm5.png)

Una chiave **API** si presenta così: `b2c4c36b6bb59c3458d6686b05311dc3`.

Puoi trovare la **documentazione API** per il **meteo attuale** [qui](https://openweathermap.org/current).

Nel nostro caso d’uso, implementeremo il collegamento con Open Weather Map in base alla città in cui si trova il cliente.

![MappaMeteo](./images/owm6.png)

Torna a **Adobe Journey Optimizer**, al popup **External Data Source** vuoto.

![Demo](./images/emptyds.png)

Come nome per l&#39;origine dati, utilizzare `--demoProfileLdap--WeatherApi`. In questo esempio, il nome dell&#39;origine dati è `vangeluwWeatherApi `.

Imposta descrizione su: `Access to the Open Weather Map`.

L&#39;URL per l&#39;API Open Weather Map è: **http://api.openweathermap.org/data/2.5/weather?units=metric**

![Demo](./images/dsname.png)

Quindi, seleziona l’Autenticazione da utilizzare.

Utilizza queste variabili:

| Campo | Valore |
|:-----------------------:| :-----------------------|
| Tipo | **Chiave API** |
| Nome | **APPID** |
| Valore | **la tua chiave API** |
| Posizione | **Parametro query** |

![Demo](./images/dsauth.png)

Infine, devi definire un **GruppoCampi**, che è sostanzialmente la richiesta che invierai all&#39;API Meteo. Nel nostro caso, vogliamo usare il nome della Città per richiedere il Tempo Attuale per quella Città.

![Demo](./images/fg.png)

In base alla documentazione dell&#39;API meteo, è necessario inviare un parametro `q=City`.

![Demo](./images/owmapi.png)

Per corrispondere alla richiesta API prevista, configura il FieldGroup come segue:

>[!IMPORTANT]
>
>Il nome del gruppo di campi deve essere univoco. Utilizzare questa convenzione di denominazione: `--demoProfileLdap--WeatherByCity`. In questo caso, il nome deve essere `vangeluwWeatherByCity`

![Demo](./images/fg1.png)

Per il payload di risposta, è necessario incollare un esempio della risposta che verrà inviata dall’API meteo.

La risposta JSON API prevista è disponibile nella pagina della documentazione API [qui](https://openweathermap.org/current).

![Demo](./images/owmapi1.png)

Oppure puoi copiare la risposta JSON da qui:

```json
{"coord": { "lon": 139,"lat": 35},
  "weather": [
    {
      "id": 800,
      "main": "Clear",
      "description": "clear sky",
      "icon": "01n"
    }
  ],
  "base": "stations",
  "main": {
    "temp": 281.52,
    "feels_like": 278.99,
    "temp_min": 280.15,
    "temp_max": 283.71,
    "pressure": 1016,
    "humidity": 93
  },
  "wind": {
    "speed": 0.47,
    "deg": 107.538
  },
  "clouds": {
    "all": 2
  },
  "dt": 1560350192,
  "sys": {
    "type": 3,
    "id": 2019346,
    "message": 0.0065,
    "country": "JP",
    "sunrise": 1560281377,
    "sunset": 1560333478
  },
  "timezone": 32400,
  "id": 1851632,
  "name": "Shuzenji",
  "cod": 200
}
```

Copia la risposta JSON di cui sopra negli Appunti, quindi vai alla schermata di configurazione dell’origine dati personalizzata.

Fai clic sull&#39;icona **Modifica payload**.

![Demo](./images/owmapi2.png)

Viene visualizzata una finestra a comparsa in cui è necessario incollare la risposta JSON precedente.

![Demo](./images/owmapi3.png)

Incolla la risposta JSON, dopo di che visualizzerai questo. Fai clic su **Salva**.

![Demo](./images/owmapi4.png)

La configurazione dell’origine dati personalizzata è stata completata. Scorri verso l&#39;alto e fai clic su **Salva**.

![Demo](./images/dssave.png)

L&#39;origine dati è stata creata correttamente e fa parte dell&#39;elenco **Origini dati**.

![Demo](./images/dslist.png)

Passaggio successivo: [3.2.3 Definisci un&#39;azione personalizzata](./ex3.md)

[Torna al modulo 3.2](journey-orchestration-external-weather-api-sms.md)

[Torna a tutti i moduli](../../../overview.md)
