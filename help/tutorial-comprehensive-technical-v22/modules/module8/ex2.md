---
title: Adobe Journey Optimizer - External Weather API, SMS Action e altro ancora - Definire un’origine dati esterna
description: Adobe Journey Optimizer - External Weather API, SMS Action e altro ancora - Definire un’origine dati esterna
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: e3e04415-4258-4ad7-a227-0e68dfcba235
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 4%

---

# 8.2 Definire un’origine dati esterna

In questo esercizio creerai un’origine dati esterna personalizzata utilizzando Adobe Journey Optimizer.

Accedi a Adobe Journey Optimizer accedendo a [Adobe Experience Cloud](https://experience.adobe.com). Fai clic su **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Verrai reindirizzato al **Pagina principale**  in Journey Optimizer. In primo luogo, assicurati di utilizzare la sandbox corretta. La sandbox da utilizzare è denominata `--aepSandboxId--`. Per passare da una sandbox all’altra, fai clic su **PROD DI PRODUZIONE (VA7)** e selezionate la sandbox dall’elenco. In questo esempio, la sandbox è denominata **Abilitazione AEP FY22**. Allora sarai nel **Pagina principale** visualizzazione della sandbox `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

Nel menu a sinistra, scorri verso il basso e fai clic su **Configurazioni**. Fai clic su **Gestisci** pulsante sotto **Origini dati**.

![Demo](./images/menudatasources.png)

Vedrai il **Origini dati** elenco.
Fai clic su **Crea origine dati** per iniziare ad aggiungere l’origine dati.

![Demo](./images/dshome.png)

Verrà visualizzato un popup per l&#39;origine dati vuota.

![Demo](./images/emptyds.png)

Prima di iniziare la configurazione, è necessario un account con **Mappa meteo aperta** servizio. Segui questi passaggi per creare il tuo account e ottenere la tua chiave API.

Vai a [https://openweathermap.org/](https://openweathermap.org/). Nella home page, fai clic su **Accesso**.

![Mappa meteo](./images/owm.png)

Fai clic su **Creare un account**.

![Mappa meteo](./images/owm1.png)

Compila i dettagli.

![Mappa meteo](./images/owm2.png)

Fai clic su **Crea account**.

![Mappa meteo](./images/owm3.png)

Verrai quindi reindirizzato alla pagina dell’account.

![Mappa meteo](./images/owm4.png)

Nel menu , fai clic su **Chiavi API** per recuperare la chiave API, che dovrai impostare l’origine dati esterna personalizzata.

![Mappa meteo](./images/owm5.png)

Un **Chiave API** si presenta così: `b2c4c36b6bb59c3458d6686b05311dc3`.

È possibile trovare le **Documentazione API** per **Tempo attuale** [qui](https://openweathermap.org/current).

Nel nostro caso d’uso, implementeremo la connessione con Open Weather Map basata sulla città in cui si trova il cliente.

![Mappa meteo](./images/owm6.png)

Torna a **Adobe Journey Optimizer**, al tuo vuoto **Origine dati esterna** popup.

![Demo](./images/emptyds.png)

Come nome per l’origine dati, utilizza `--demoProfileLdap--WeatherApi`. In questo esempio, il Nome origine dati è `vangeluwWeatherApi `.

Imposta descrizione su: `Access to the Open Weather Map`.

L’URL dell’API Open Weather Map è: **http://api.openweathermap.org/data/2.5/weather?units=metric**

![Demo](./images/dsname.png)

Quindi, devi selezionare l&#39;autenticazione da utilizzare.

Utilizza queste variabili:

| Campo | Valore |
|:-----------------------:| :-----------------------|
| Tipo | **API key** |
| Nome | **APPID** |
| Valore | **la chiave API** |
| Posizione | **Parametro query** |

![Demo](./images/dsauth.png)

Infine, devi definire un **FieldGroup**, che è fondamentalmente la richiesta che invierai all’API Meteo. Nel nostro caso, vogliamo usare il nome della Città per richiedere il Tempo Corrente per quella Città.

![Demo](./images/fg.png)

In base alla documentazione sulle API meteo, dobbiamo inviare un parametro `q=City`.

![Demo](./images/owmapi.png)

Per soddisfare la richiesta API prevista, configura il tuo FieldGroup come segue:

>[!IMPORTANT]
>
>Il nome del gruppo di campi deve essere univoco. Utilizza questa convenzione di denominazione: `--demoProfileLdap--WeatherByCity` in questo caso, il nome deve essere `vangeluwWeatherByCity`

![Demo](./images/fg1.png)

Per il payload di risposta, devi incollare un esempio della risposta che verrà inviata dall’API Meteo.

Puoi trovare la risposta API JSON prevista nella pagina Documentazione API . [qui](https://openweathermap.org/current).

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

Fai clic sul pulsante **Modifica payload** icona.

![Demo](./images/owmapi2.png)

Viene visualizzata una finestra a comparsa in cui è ora necessario incollare la risposta JSON di cui sopra.

![Demo](./images/owmapi3.png)

Incolla la tua risposta JSON, dopodiché visualizzerai questa. Fai clic su **Salva**.

![Demo](./images/owmapi4.png)

La configurazione dell’origine dati personalizzata è ora completa. Scorri verso l’alto e fai clic su **Salva**.

![Demo](./images/dssave.png)

L&#39;origine dati è stata creata correttamente e fa parte del **Origini dati** elenco.

![Demo](./images/dslist.png)

Passaggio successivo: [8.3 Definire un’azione personalizzata](./ex3.md)

[Torna al modulo 8](journey-orchestration-external-weather-api-sms.md)

[Torna a tutti i moduli](../../overview.md)
