---
title: Creare la campagna orchestrata
description: Creare la campagna orchestrata
kt: 5342
doc-type: tutorial
exl-id: f3ca3230-db30-4e41-91f1-9324b12211a6
source-git-commit: 0328260e8699107bc82103af98caae684319a60d
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 2%

---

# 3.8.2 Creare una campagna orchestrata

## 3.8.2.1 Crea la tua campagna orchestrata

Vai a **Campagne**. Fai clic su **Crea campagna**.

![AJO OC](./images/ajooc1.png)

Seleziona **Orchestrazione - Marketing** e fai clic su **Conferma**.

![AJO OC](./images/ajooc2.png)

Immetti il nome della campagna: `--aepUserLdap-- - CitiSignal Family Account Optimization Campaign` e fai clic su **Salva**.

![AJO OC](./images/ajooc3.png)

Dovresti vedere questo. Fai clic sull&#39;icona **+**.

![AJO OC](./images/ajooc4.png)

Seleziona **Fork**.

![AJO OC](./images/ajooc5.png)

### Crea pubblico 1

Fai clic sull&#39;icona **+**, quindi seleziona **Genera pubblico**.

![AJO OC](./images/ajooc6.png)

Fare clic per aprire la cartella per la **dimensione di targeting**.

![AJO OC](./images/ajooc7.png)

Seleziona **`--aepUserLdap--_citisignal_recipients`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc8.png)

Fai clic su **Crea pubblico**.

![AJO OC](./images/ajooc9.png)

Fai clic su **Aggiungi condizione**.

![AJO OC](./images/ajooc10.png)

Seleziona **recipient_type** e fai clic su **Confirm**.

![AJO OC](./images/ajooc11.png)

Immetti **`account_holder`** nel campo **Valore** e fai clic su **Calcola**.

![AJO OC](./images/ajooc12.png)

Dovresti quindi visualizzare un numero per **profili target**. Fare clic in un punto qualsiasi dell&#39;area grigia, come indicato.

![AJO OC](./images/ajooc13.png)

Fai clic su **Aggiungi condizione**.

![AJO OC](./images/ajooc14.png)

Espandere fino a **`citisignal_accounts`**.

![AJO OC](./images/ajooc15.png)

Seleziona **`account_status`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc16.png)

Immetti **`active`** nel campo **Valore**. Fare quindi clic in un punto qualsiasi dell&#39;area grigia, come indicato.

![AJO OC](./images/ajooc17.png)

Fai clic su **Aggiungi condizione**.

![AJO OC](./images/ajooc18.png)

Espandere fino a **`citisignal_mobile_subscriptions`**.

![AJO OC](./images/ajooc19.png)

Seleziona **`subscription_id`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc20.png)

Abilita il commutatore per **Aggregate data**. Quindi seleziona quanto segue:

- **Funzione aggregata**: **Conteggio**
- **Operatore**: **maggiore o uguale a**
- **Valore**: **1**

Fai clic su **Conferma**.

![AJO OC](./images/ajooc21.png)

Dovresti vedere questo. Fai clic su **Conferma**.

![AJO OC](./images/ajooc22.png)

### Creare un pubblico 2

Fare clic sull&#39;icona **+** nel nodo successivo nell&#39;altro percorso.

![AJO OC](./images/ajooc23.png)

Seleziona **Genera pubblico**.

![AJO OC](./images/ajooc24.png)

Fare clic per aprire la cartella per la **dimensione di targeting**.

![AJO OC](./images/ajooc25.png)

Seleziona **`--aepUserLdap--_mobile_subscriptions`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc26.png)

Fai clic su **Crea pubblico**.

![AJO OC](./images/ajooc27.png)

Fai clic su **Aggiungi condizione**.

![AJO OC](./images/ajooc28.png)

Seleziona **subscription_status** e fai clic su **Conferma**.

![AJO OC](./images/ajooc29.png)

Immetti **`active`** nel campo **Valore**. Quindi fare clic su **Aggiungi condizione**.

![AJO OC](./images/ajooc30.png)

Seleziona **`is_upgrade_eligible`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc31.png)

Imposta **Valore** su **vero**

![AJO OC](./images/ajooc32.png)

Fai clic su **Calcola** per visualizzare una stima dei profili idonei per questo pubblico. Quindi fare clic su **Conferma**

![AJO OC](./images/ajooc33.png)

### Dividi

Fai clic sull&#39;icona **+**, quindi seleziona **Dividi**.

![AJO OC](./images/ajooc34.png)

Cambia il campo **Etichetta** in **90/10 Trattamento vs Controllo**. Fare clic per aprire l&#39;oggetto **Subset**.

![AJO OC](./images/ajooc35.png)

Abilita il commutatore per **Abilita limite** e imposta la **dimensione limite** su **10 percento**.

![AJO OC](./images/ajooc36.png)

Fai clic su **Aggiungi segmento** per visualizzare l&#39;oggetto **Risultato** aggiunto.

Fai clic su **Salva**.

![AJO OC](./images/ajooc37.png)

### Salva pubblico

Fai clic sull&#39;icona **+**, quindi seleziona **Salva pubblico**.

![AJO OC](./images/ajooc38.png)

Imposta il campo **Etichetta pubblico** su **`--aepUserLdap-- - Control Group`**. Fare clic su **Aggiungi mapping pubblico**.

![AJO OC](./images/ajooc39.png)

Espandere la **dimensione di targeting**.

![AJO OC](./images/ajooc40.png)

Seleziona **`account_id`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc41.png)

Imposta il campo **Mapping profilo** su **`--aepUserLdap--_citisignal_recipients - account_id`**.

![AJO OC](./images/ajooc41a.png)

### Arricchimento: abbonamento a Internet

Fai clic sull&#39;icona **+**.

![AJO OC](./images/ajooc42.png)

Seleziona **Arricchimento**.

![AJO OC](./images/ajooc43.png)

Dovresti vedere questo. Fai clic su **Aggiungi dati di arricchimento**.

![AJO OC](./images/ajooc44.png)

Espandere fino a **`Targeting dimension`**.

![AJO OC](./images/ajooc44a.png)

Espandere fino a **`citisignal_accounts`**.

![AJO OC](./images/ajooc45.png)

Espandere fino a **`citisignal_internet_subscriptions`**.

![AJO OC](./images/ajooc45a.png)

Seleziona **`account_id`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc46.png)

Dovresti vedere questo. Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc47.png)

Seleziona **`subscription_status`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc48.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc49.png)

Seleziona **`connection_type`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc50.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc51.png)

Seleziona **`service_city`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc52.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc53.png)

Seleziona **`avg_bandwidth_usage_gb`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc54.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc55.png)

Seleziona **`data_cap_gb`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc56.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc57.png)

Seleziona **`advertised_speed_mbps`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc58.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc59.png)

Seleziona **`monthly_recurring_charge`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc60.png)

Fai clic su **Salva**.

![AJO OC](./images/ajooc61.png)

Scorri verso l&#39;alto e modifica il campo **Etichetta** in `Enrichment: Internet Subscription`.

![AJO OC](./images/ajooc61a.png)

### Arricchimento: abbonamento dispositivi mobili

Fai clic sull&#39;icona **+** nel nodo successivo e seleziona **Arricchimento**.

![AJO OC](./images/ajooc62.png)

Modificare il campo **Label** in `Enrichment: Mobile Devices Subscription` e quindi fare clic su **Aggiungi dati di arricchimento**.

![AJO OC](./images/ajooc63.png)

Espandere la **dimensione di targeting**.

![AJO OC](./images/ajooc64.png)

Espandere fino a **`citisignal_accounts`**.

![AJO OC](./images/ajooc65.png)

Espandere fino a **`citisignal_mobile_subscriptions`**.

![AJO OC](./images/ajooc65a.png)

Seleziona **`phone_number`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc66.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc67.png)

Espandere fino a **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc68.png)

Seleziona **`model`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc68a.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc69.png)

Espandere fino a **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc69a.png)

Seleziona **`recommended_device_model`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc70.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc71.png)

Espandere fino a **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc71a.png)

Seleziona **`is_upgrade_eligible`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc72.png)

Ora puoi verificare l’avanzamento eseguendo un’esecuzione di test e vedere quali dati sono disponibili nella campagna.

Salva le modifiche e fai clic su **Avvia**.

![AJO OC](./images/ajooctest1.png)

Dopo un po&#39; di tempo, dovresti vedere questo. Fare clic su **Anteprima risultati**.

![AJO OC](./images/ajooctest2.png)

Dovresti vedere qualcosa di simile a questo. Fai clic su **Chiudi**.

![AJO OC](./images/ajooctest3.png)

Torna al nodo **Arricchimento: abbonamento dispositivi mobili**.

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc73.png)

Seleziona **`account_id`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc74.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc75.png)

Seleziona **`subscription_id`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc76.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc77.png)

Seleziona **`renewal_eligibility_date`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc78.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc79.png)

Seleziona **`line_user_recipient_id`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc80.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc81.png)

Seleziona **`current_device_id`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc82.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc86.png)

Seleziona **`contract_start_date`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc87.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc89.png)

Espandere fino a **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc90.png)

Seleziona **`manufacturer`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc91.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc92.png)

Espandere fino a **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc93.png)

Seleziona **`device_age_months`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc94.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc95.png)

Espandere fino a **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc96.png)

Seleziona **`trade_in_value`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc97.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc98.png)

Espandere fino a **`citisignal_equipment_subscriptions`**.

![AJO OC](./images/ajooc99.png)

Seleziona **`monthly_payment`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc100.png)

### Arricchimento: abbonamento dispositivi mobili

Dovresti avere questo. Fai clic su **Salva**. Quindi fare clic sull&#39;icona **+** per aggiungere un nuovo nodo e selezionare **Arricchimento**.

![AJO OC](./images/ajooc101.png)

Dovresti vedere questo. Fai clic su **Aggiungi dati di arricchimento**.

![AJO OC](./images/ajooc102.png)

Espandere la **dimensione di targeting**.

![AJO OC](./images/ajooc103.png)

Espandere fino a **`citisignal_offer_eligibility`**.

![AJO OC](./images/ajooc104.png)

Espandere fino a **`citisignal_offers`**.

![AJO OC](./images/ajooc105.png)

Seleziona **`offer_name`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc106.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc107.png)

Espandere fino a **`citisignal_offers`**.

![AJO OC](./images/ajooc108.png)

Seleziona **`offer_code`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc109.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc110.png)

Espandere fino a **`citisignal_offers`**.

![AJO OC](./images/ajooc111.png)

Seleziona **`offer_description`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc112.png)

Fare clic su **Aggiungi attributo**.

![AJO OC](./images/ajooc110.png)

Espandere fino a **`citisignal_offers`**.

![AJO OC](./images/ajooc113.png)

Seleziona **`offer_description`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc114.png)

Attiva **Abilita ordinamento**.

![AJO OC](./images/ajooc115.png)

Espandere fino a **`citisignal_offers`**.

![AJO OC](./images/ajooc116.png)

Seleziona **`offer_priority`** e fai clic su **Conferma**.

![AJO OC](./images/ajooc117.png)

Ora puoi testare la tua campagna. Fai clic su **Inizio**.

![AJO OC](./images/ajooc118.png)

Dopo un po&#39; di tempo dovresti vedere questo. Fare clic su **Risultato** e selezionare **Anteprima risultati**.

![AJO OC](./images/ajooc120.png)

Dovresti vedere qualcosa di simile a questo.

![AJO OC](./images/ajooc121.png)

### Attività e-mail

Fai clic sull&#39;icona **+**, quindi seleziona **E-mail**.

![AJO OC](./images/ajooc122.png)

Fai clic su **Modifica e-mail**.

![AJO OC](./images/ajooc123.png)

Vai a **Azioni**.

![AJO OC](./images/ajooc124.png)

Seleziona la **configurazione del canale e-mail** creata in precedenza e fai clic su **Modifica contenuto**.

![AJO OC](./images/ajooc125.png)

Per **Oggetto**, incolla questo:

`{{target.--aepUserLdap--_citisignal_recipients.first_name}}, Your CitiSignal Family Account Summary`

Fai clic su **Modifica corpo dell&#39;e-mail**.

![AJO OC](./images/ajooc126.png)

## Passaggi successivi

Torna a [Adobe Journey Optimizer: campagne orchestrate](./ajocampaigns.md){target="_blank"}

Torna a [Tutti i moduli](./../../../../overview.md){target="_blank"}
