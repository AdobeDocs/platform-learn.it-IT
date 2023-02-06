---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brasile
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brasile
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---

# 4.1 Customer Journey Analytics 101

## Obiettivi

- Entenda o que é o CJA
- Entenda qual è o papel do CJA
- Entenda o workflow do CJA: da conexão de dados approfondimenti aos

## 4.1.1 O que é o Customer Journey Analytics?

O Customer Journey Analytics (CJA) fornece uma interface em que os times de Analytics, Negócios e Tecnologia | em unir toos dados da companhia e analisar a jornada cross channel (online e offline) do cliente de ponta a ponta. O CJA é capaz de fornecer contexto e clareza para essa jornada, trazendo uma visão acionável em cima das dificuldades no sette de conversão e possibilitando o planejamento de experiências rilevanti e personalizadas nos pontos mais rilevanti.

O CJA traz o Analysis Workspace conectado à Adobe Experience Platform. A Adobe Experience Platform é o cérebro da comunicação e da orquestração e, com o CJA, come marcas agora podem contextualizar e visualizar todos esses dados, para que as equipes de negócios e insights possam aprender com eles, analisando toda a jornada on-line para off-line do cliente.

Come equipaggiamenti de negócios e insights podem conversar com o CJA, fazer perguntas e obter respoas em tempo real com un&#39;interfaccia do usuário de arrastar e soltar, apontar e clicar e fácil de usar do Analysis Workspace.

![demo](./images/cja-adv-analysis1.png)

## 4.1.2 Principais vantagens

Os três principis benefit ícios para os clientsão:

- Un condensidade de disponibilizar insights para todos (ou seja, democratizar o acesso aos dados).
- Contestuale (ou seja, os dados podem ser visualizados sequencialmente, abranmúltiplos canais on-line e off-line).
- Condensidade de aproveitar o poder dos dados sem que haja a need (ou seja, permite que indivíduos usem dados para desbloquear insights e análises profundas para ativação de marketing).

## 4.1.3 ## 4.1.3 Por que scolher o Customer Journey Analytics?

O CJA não se destina a subituir um aplicativo de BI atual, como Power BI, Microstrategia, Locker ou Tableau. O objetivo desses aplicativos de BI é visualizar dados para criar doloréis corporativos para que todos em uma organização possam ver métricas importantes eg. O objetivo do CJA é trazer poder de análise para as equipes de Marketing e Negócios, tornando-o uma ferramenta de análise obrigatória para essas pessoas



Tradicionalmente, os aplicativos de BI têm sido incapazes de permitir a verdadeira inteligência do cliente:

- Eles não podem fazer atribuição e não fazem análises de jornada do cliente.
- Os aplicativos de BI Precam saber a pergunta com antecedência
- Consulas interativas são limitadas pela estrutura do Banco de dados
- Habilidades de SQL são necessárias.
- Os aplicativos de BI não permitem que você pergunte o vuoto de acontecimento
- Os aplicativos de BI não têm conexão direta com os pontos de contato do cliente.

Portanto, usuários de negócios e analistas chegam a becos sem saída quase imedinata, tornando a análise cara, lenta, inflexível e desconectada dos sistemas de ação.

Com o CJA vocpode ter uma visão da jornada do cliente, com as ferramentas certas para reduzir o tempo de insight, tornando os usuários de negócios Independent para entender por que algo aconteceu e como responder a isso.

![demo](./images/cja-use-case.png)

## 4.1.4 Compreenda o fluxo de trabalho do Customer Journey Analytics

Antes de iniciar os próximos exercícios, é essencial compender quais etapas são necessárias para trazer dados da Adobe Experience Platform para o CJA para visualizá-los e obter alguns insights profundos. É o que chamamos de fluxo de trabalho do CJA. Vamos verificato:

![demo](./images/cja-work-flow.jpg)

Antes de iniciar as etapas acima, não se esqueça da etapa 0, que é compressender os dados que estão disponíveis na Adobe Experience Platform.

**Spazzatura dentro, spazzatura fuori.** Você deve ter uma ideia clara de quais dados estão disponíveis e como os esquemas na Adobe Experience Platform são configurados. Compreender os dados que estão na Adobe Experience Platform facilitará as coisas, não só na parte de conexão de dados, mas também na hora de costrutuir visualizações e fazer análises.

## 4.1.5 Etapa 0: Query e set di dati compositi da Adobe Experience Platform

Faça login na Adobe Experience Platform acessando un URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer login, você irá acessar a página inicial da Adobe Experience Platform.

![Acquisizione dei dati](../uc1/images/home.png)

Antes de continuar, você precisa selionar um **sandbox**. O nome do sandbox un utente selionado é ``Bootcamp``. Você pode fazer isso clicando no ícone **[!UICONTROL Prod]** nessun canto superiore direito da tela. Depois de selionar o sandbox apropriado, você verá a tela mudando e agora você está em seu sandbox deduado.

![Acquisizione dei dati](../uc1/images/sb1.png)

Verifica gli schemi e i set di dati in Adobe Experience Platform.

| Set di dati | Schema |
| ----------------- |-------------| 
| Sistema di demo - Set di dati evento per il sito web (Global v1.1) | Sistema demo - Schema evento per sito web (Global v1.1) |
| Sistema demo - Set di dati evento per Call Center (Global v1.1) | Sistema demo - Schema evento per Call Center (Global v1.1) |
| Sistema demo - Set di dati evento per assistenti vocali (Global v1.1) | Sistema demo - Schema eventi per assistenti vocali (versione globale 1.1) |

Certifique-se de ter verify ao menos:

- Identità: CRMID, phoneNumber, ECID, email. Quali sono gli identificatori principali, quali sono gli identificatori secondari?
È possibile trovare gli identificatori aprendo uno schema e guardando l&#39;oggetto `_experienceplatform.identification.core`. Osserva lo schema [Sistema demo - Schema evento per sito web (Global v1.1)](https://experience.adobe.com/platform/schema).

- Identificazioni: CRMID, phoneNumber, ECID, email. Quais identidades são os identificadores primários, quais são os identificadores secundários?
Você pode encontrar os identificadores abrindo um schema e osservando o objeto `_experienceplatform.identification.core`. Verificatore dello schema [Sistema demo - Schema evento per sito web (Global v1.1)](https://experience.adobe.com/platform/schema).

![demo](./images/identity.png)

- Esplora lo schema di objeto de comércio dentro do [Sistema demo - Schema evento per sito web (Global v1.1)](https://experience.adobe.com/platform/schema).

![demo](./images/commerce.png)

- Visualizzare gli strumenti os [set di dati](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) e verifique os dados

Agora você está rapidamente para começar a usar a interface do usuário do Customer Journey Analytics.

Próxima etapa: [Connetti set di dati da Adobe Experience Platform nessun Customer Journey Analytics](./ex2.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](../../overview.md)
