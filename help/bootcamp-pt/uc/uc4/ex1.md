---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brasile
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brasile
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 63933d9e-b774-483f-b547-188c77440595
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# 4.1 Customer Journey Analytics 101

## Objetivos

- Entenda o que é o CJA
- Entenda qual é o papel do CJA
- Entenda o workflow do CJA: da conexão de dados aos insights

## 4.1.1 O que é o Customer Journey Analytics?

O Customer Journey Analytics (CJA) fornece uma interface em que os os times de Analytics, Negócios e Tecnologia conseguem unir todos os dados da companhia e analisar a jornada cross-channel (online e offline) do cliente de ponta a ponta. O CJA é capaz de fornecer contexto e clareza para essa jornada, trazendo uma visão acionável em cima das dificuldades no processo de conversão e possibilitando o planejamento de experiências rilevanti e personalizadas nos pontos mais rilevanti.

O CJA traz o Analysis Workspace conectado à Adobe Experience Platform. A Adobe Experience Platform é o cérebro da comunicação e da orquestração e, com o CJA, as marcas agora podem contextualizar e visualizar todos esses dados, para que as equipes de negócios e insights possam aprender com eles, analisando toda a jornada on-line para off-line do cliente.

Come equipes de negócios e insights podem conversar com o CJA, fazer perguntas e obter respostas em tempo real com a interface do usuário de arrastar e soltar, apontar e clicar e fácil de usar do Analysis Workspace.

![demo](./images/cja-adv-analysis1.png)

## 4.1.2 Principi di base

Os três princippais benefits para os clientes são:

- Una capacidade de disponibilizar insights para todos (ou seja, democratizar o acesso aos dados).
- Una capacidade de ver o cliente em uma jornada contestuale (ou seja, os dados podem ser visualizados sequencialmente, abrangendo múltiplos canais on-line e off-line).
- Una capacidade de aproveitar o poder dos dados sem que haja a necessidade (ou seja, permite que indivíduos usem dados para desbloquear insights e análises profoundation para ativação de marketing).

## 4.1.3 ## 4.1.3 Por que escolher o Customer Journey Analytics?

CJA não se destina a substituir um aplicativo de BI atual, como Power BI, Microstrategy, Locker ou Tableau. O objetivo desses aplicativos de BI é visualizar dados para criar painéis corporativos para que todos em uma organização possam ver métricas importantes. O objetivo do CJA é trazer poder de análise para as equipes de Marketing e Negócios, tornando-o uma ferramenta de análise obrigatória para essas pessoas



Tradicionalmente, os aplicativos de BI têm sido incapazes de permitir a verdadeira inteligência do cliente:

- Eles não podem fazer atribuição e não fazem análises de jornada do cliente.
- Os aplicativos de BI precisam saber a pergunta com antecedência
- Consulas interativas são limitadas pela estrutura do banco de dados
- Habilidades de SQL são necessárias.
- Os aplicativos de BI não permitem que você pergunte o motivo de um acontecimento.
- Os aplicativos de BI não têm conexão direta com os pontos de contato do cliente.

Portanto, usuários de negócios e analistas chegam a becos sem saída quase imediatamente, tornando a análise cara, lenta, inflexível e desconectada dos sistemas de ação.

Com o CJA você pode ter uma visão completa da jornada do cliente, dados offline e online, com as ferramentas certas para reduzir o tempo de insight, tornando os usuários de negócios indipendentes para entender por que algo aconteceu e como responder a isso.

![demo](./images/cja-use-case.png)

## 4.1.4 Compreenda o fluxo de trabalho do Customer Journey Analytics

Antes de iniciar os próximos exercícios, é essencial compender quais etapas são necessárias para trazer dados da Adobe Experience Platform para o CJA para visualizá-los e obter alguns insights profundos. É o que chamamos de fluxo de trabalho do CJA Vamos verificar:

![demo](./images/cja-work-flow.jpg)

Antes de iniciar è etapas acima, não se esqueça da etapa 0, que é compender os dados que estão disponíveis na Adobe Experience Platform.

**Spazzatura dentro, spazzatura fuori.** Você deve ter uma ideia clara de quais dados estão disponíveis e como os esquemas na Adobe Experience Platform são configurados Compreender os dados que estão na Adobe Experience Platform facilitará come coisas, não só na parte de conexão de dados, mas também na hora de coisações e fazer análises.

## 4.1.5 Etapa 0: esquema e set di dati del Compreender da Adobe Experience Platform

Faça login na Adobe Experience Platform acessando un URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Accesso Depois de fazer, você irá acessar a página inicial da Adobe Experience Platform.

![Acquisizione dei dati](../uc1/images/home.png)

Antes de continuar, você selecionar um **sandbox**. O nome do sandbox a ser selecionado é ``Bootcamp``. Você pode fazer isso clicando no ícone **[!UICONTROL Prod]** nessun canto superiore direito da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu sandbox dedicado.

![Acquisizione dei dati](../uc1/images/sb1.png)

Verifica degli schemi e dei set di dati in Adobe Experience Platform.

| Set di dati | Schema |
| ----------------- |-------------| 
| Sistema di dimostrazione - Set di dati di eventi per il sito web (Global v1.1) | Sistema di dimostrazione - Schema eventi per il sito web (Global v1.1) |
| Sistema demo - Set di dati evento per Call Center (Global v1.1) | Sistema demo - Schema eventi per Call Center (Global v1.1) |
| Sistema demo - Set di dati evento per assistenti vocali (Global v1.1) | Sistema demo - Schema eventi per assistenti vocali (Global v1.1) |

Certifique-se de ter verificado ao menos:

- Identificazioni: CRMID, phoneNumber, ECID, e-mail. Quais identidades são os identadores primários, quais são os identadores secundários?

Você pode encontrar os identadores abrindo um schema e observando o objeto `_experienceplatform.identification.core`. Verifica dello schema [Sistema di dimostrazione - Schema eventi per il sito web (Global v1.1)](https://experience.adobe.com/platform/schema).

![demo](./images/identity.png)

- Esplora lo schema objeto de comércio dentro do [Sistema di dimostrazione - Schema eventi per il sito web (Global v1.1)](https://experience.adobe.com/platform/schema).

![demo](./images/commerce.png)

- Visualizza il sistema operativo delle attività [set di dati](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) e verifica dei dado del sistema operativo

Agora você está pronta para começar a usar a interface do usuário do Customer Journey Analytics.

Próxima etapa [4.2 Set di dati concreti da Adobe Experience Platform nessun Customer Journey Analytics](./ex2.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](../../overview.md)
