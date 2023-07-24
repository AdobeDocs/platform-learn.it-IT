---
title: Bootcamp - Blending physical and digital - Journey Optimizer Crea il tuo percorso e push - Brazilnotification
description: Bootcamp - Blending physical and digital - Journey Optimizer Crea il tuo percorso e push - Brazilnotification
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: a4ef6eaf-6b39-4450-82bf-7db99595a323
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 1%

---

# 3.3 Crie sua jornada e notificação push

Neste exercício, você irá configurar a jornada e a mensagem que ser acionada quando alguém inserir uma sinalização (beacon) o aplicativo móvel.

Accesso a Faça da Adobe Journey Optimizer acessando a [Adobe Experience Cloud](https://experience.adobe.com). Clique em **Journey Optimizer**.

![ACOP](./images/acophome.png)

Você será redirecionado para a visualização da **Home** nessuna Journey Optimizer. Primeiro, verifique se você está o sandbox correto. O nome do sandbox que deve ser usado é `Bootcamp`. Para alternar de um sandbox para outro, cricca em **Prod** e selecione o sandbox na lista Neste exemplo, o nome do sandbox é **Bootcamp**. Você estará na visualização da **Home**  do seu sandbox `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Crie a sua jornada

Nessun menu à esquerda, cricca em **Percorsi**. Em seguida, cricca em **Crea Percorso** para criar uma nova jornada.

![ACOP](./images/createjourney.png)

Você verá uma tela de jornada vazia

![ACOP](./images/journeyempty.png)

Nessun exercício anteriore, você criou um novo **Evento**. Você nomeou o evento `yourLastNameBeaconEntryEvent` e substituiu `yourLastName` pelo seu sobrenome. Este foi o resultado da criação do Evento:

![ACOP](./images/eventdone.png)

Agora você deve considerar este evento como o início desta Jornada. Você pode fazer isso indo para o lado esquerdo da tela e procurando pelo seu evento na lista de eventos.

![ACOP](./images/eventlist.png)

Selecione seu evento, arraste e solte o evento na tela de jornada. Sua jornada agora deve ser semelhante ao seguinte. Clique em **Ok** para salvar suas alterações.

![ACOP](./images/journeyevent.png)

Como segunda etapa da jornada, você deve adicionar uma ação **Push**. Vá para o lado esquerdo da tela para **Azioni**, selecione a ação **Push** e arraste e solte a ação no segundo nó da sua jornada.

![ACOP](./images/journeyactions.png)

Non c&#39;è nessun lado direito da tela, agora você deve criar sua notificação push.

Definisci un **Categoria** como **Marketing** e selecione um push surface que permite enviar notificações push. Nesse caso, un superfície spinge una ser selecionada é **meeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Crie a sua mensagem

Clique em **Modifica contenuto**.

![ACOP](./images/emptymsg.png)

Em seguida, a tela abaixo será exibida:

![ACOP](./images/emailmsglist.png)

Vamos definir o conteúdo da notificação push.

Clique no campo de texto **Titolo**.

![Journey Optimizer](./images/msg5.png)

Na área de texto, comece **Olá**. Cricca di personalização.

![Journey Optimizer](./images/msg6.png)

Agora você trazer o token de personalização para o campo **Nome** que está armazenado em `profile.person.name.firstName`. Nessun menu à esquerda, selecione **Attributi del profilo**, role para baixo/navegue para encontrar o elemento **Persona** e clique na seta para avançar um nível até chegar ao campo `profile.person.name.firstName`. Clique no ícone **+** para adicionar o campo à tela Clique em **Salva**.

![Journey Optimizer](./images/msg7.png)

Voce irá retornar para esta tela. Clique no ícone de personalização ao lado do campo **Corpo**.

![Journey Optimizer](./images/msg11.png)

Na área de texto, escreva `Bem-vindo(a)`.

![Journey Optimizer](./images/msg12.png)

Em seguida, cricca em  **Attributi contestuali** e **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Clique em **Eventi**.

![ACOP](./images/jomsg4.png)

Clique no nome do seu evento, que deve ser semelhante ao seguinte: **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Clique em **Contesto del luogo**.

![ACOP](./images/jomsg6.png)

Clique em **Interazione POI**.

![ACOP](./images/jomsg7.png)

Clique em **Dettagli POI**.

![ACOP](./images/jomsg8.png)

Clique no **+** icona no **Nome punto di interesse**.
Em seguida, o seguinte será exibido. Clique em **Salva**.

![ACOP](./images/jomsg9.png)

Sua mensagem agora está pronta. Cricca na seta no canto superiore esquerdo para retornar à sua jornada.

![ACOP](./images/jomsg11.png)

Clique em **Ok**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envie uma mensagem para uma tela

Como terceira etapa da jornada, você deve adicionar uma ação  **sendMessageToScreen**. Vá para o lado esquerdo da tela para **Azioni**, selecione a ação **sendMessageToScreen** e arraste e solte a ação no terceiro nó da sua jornada. Em seguida, você verá a tela abaixo.

![ACOP](./images/jomsg15.png)

**sendMessageToScreen** é uma ação personalizada que irá publicar uma mensagem no **Endpoint** è il primo film della storia, usado pela exibição na loja. A ação **sendMessageToScreen** espera que múltiplas variáveis sejam definidas. Você pode visualizar essas variáveis rolando para baixo até ver **Parametri azione**.

![ACOP](./images/jomsg16.png)

Agora você definir os valores para cada parâmetro de ação. Siga esta tabela para entender quais valores são necessários e onde.

| Parametro | Valore  |
|:-------------:| :---------------:|
| CONSEGNA | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| NOME | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| SANDBOX | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style="table-layout:auto"}

Para definir esses valores, cricca no ícone **Modifica**.

![ACOP](./images/jomsg17.png)

Em seguida, selecione **Modalità avanzata**.

![ACOP](./images/jomsg18.png)

Em seguida, cole o valor com base na tabela acima. Clique em **Ok**.

![ACOP](./images/jomsg19.png)

Repita esse processo para adicionar valores para cada campo.

>[!IMPORTANT]
>
>Para o campo ECID, há uma referência ao evento`yourLastNameBeaconEntryEvent`. Lembre-se de subituir  `yourLastName` pelo seu sobrenome.

O risultato finale deve ser semelhante ao seguinte:

![ACOP](./images/jomsg20.png)

Ruolo para cima e clique em **Ok**.

![ACOP](./images/jomsg21.png)

È comunque necessario assegnare un nome al percorso. Per farlo, fai clic sul pulsante **Proprietà** in alto a destra.

![ACOP](./images/journeyname.png)

Você pode inserir o nome da jornada aqui Seleziona `yourLastName - Beacon Entry Journey`. Clique em **OK** para salvar suas alterações.

![ACOP](./images/journeyname1.png)

Agora você pode publicar sua jornada clicando em **Pubblica**.

![ACOP](./images/publishjourney.png)

Clique em **Pubblica** novamente.

![ACOP](./images/publish1.png)

Você verá uma barra de confirm mação verde informando que sua jornada agora está Publicada.

![ACOP](./images/published.png)

Sua jornada agora está ativa e pode ser acionada.

Você terminou este exercício

Próxima etapa [3.4 Teste sua jornada](./ex4.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
