---
title: Bootcamp - Customer Journey Analytics - Da informazioni all'azione - Brasile
description: Bootcamp - Customer Journey Analytics - Da informazioni all'azione - Brasile
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: febeba3596d3f98b2352c5ef8688ee011d25c9fe
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 4.6 Dos insights à ação

## Obiettivi

- Entenda como criar um público com base em uma visão coletada no Customer Journey Analytics
- Usa esse público no CDP em tempo reale e no Adobe Journey Optimizer

## 4.6.1 Crie uma audiência e publique-a

Em seu projeto, você criou um filtro chamado **Sentimenti di chiamata** e realizzati visualizzazione a quantidade de usuários que tiveram suas ligações ao call center classificadas como **positivas**. Agora, você poderá criar um segmento com esses usuários e ativação-los em jornadas ou em canais de comunicação.

O primeiro passo é: No penel criado no último exercício, selione a linha **1. Sensazione di chiamata - Positivo**, clique com o botão direito de seu mouse e selecione a opção **Creare un pubblico dalla selezione**:

![demo](./images/aud1.png)

Em seguida, dê um nome para a sua audiência seguindo o modelo **yourLastName - cia audience call che si sente positiva**:

![demo](./images/aud2.png)

Nota que é possível ter um preview da audiência que está sendo criada:

![demo](./images/aud3.png)

Para finalizar, clique em **Pubblicitario**:

![demo](./images/aud4.png)

## 4.6.2 Utilizzare sua audiência como parte de um segmento

Voltando para a Adobe Experience Platform, vá em **Segmenti > Sfoglia** e você irá visualizzazione o seu segmento criado no CJA rapidamente e disponível para ser usado nas suas ativaçes e jornadas!

![demo](./images/aud5.png)

Vamos agora usar esse segmento em uma ativação no Facebook e em uma jornada do cliente!

## 4.6.3 Utilizzare seu segmento un Real-Time CDP em tempo reale

Na Adobe Experience Platform, vá em **Segmenti > Sfoglia** Incontra un audiência que você criou no CJA:

![demo](./images/aud6.png)

Clique no seu segmento e, em seguida, clique em **Attiva a destinazione**:

![demo](./images/aud7.png)

Selecione una destinazione chamada bootcamp-facebook e, em seguida, clique em Next:

![demo](./images/aud8.png)

Em seguida, clique em Next novamente:

![demo](./images/aud9.png)

Selecione a opção **Origine del pubblico** e defina como **Direttamente dai clienti** e clique em Next:

![demo](./images/aud10.png)

Por fim, na página **Revisione** clicca su Fine!

![demo](./images/aud11.png)

Pronto! Agora o seu segmento está vinculado aos públicos personalizados do Facebook.
Agora, vamos utilizar esse segmento no AJO!

## 4.6.4 Utilizzare il segmento seu su Adobe Journey Optimizer

Interfaccia da Adobe Experience Platform clique em Journey Optimizer e, em seguida, nessun menu esquerdo laterale, clique em **Percorsi** e compone un parroco uma jornada clicando em **Crea Percorso**:

![demo](./images/aud20.png)

![demo](./images/aud21.png)

![demo](./images/aud22.png)

Em seguida, senza menu esquerdo laterale, em Eventos, selione **Qualificazione del segmento** e arraste-o até a jornada:

![demo](./images/aud23.png)

Em seguida, em **Segmento** cricca **Modifica** para selionar um segmento:

![demo](./images/aud24.png)

Selecione a audiência que você criou no CJA e clique em **Salva**:

![demo](./images/aud25.png)

Pronto! A partir daí você pode criar uma jornada para clientque se Qualam para esse segmento!

[Torna al flusso utente 4](./uc4.md)

[Voltar para todos os módulos](./../../overview.md)
