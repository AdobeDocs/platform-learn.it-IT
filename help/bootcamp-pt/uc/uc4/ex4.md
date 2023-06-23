---
title: Bootcamp - Customer Journey Analytics - Preparazione dei dati in Analysis Workspace - Brasile
description: Bootcamp - Customer Journey Analytics - Preparazione dei dati in Analysis Workspace - Brasile
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: d56128af-dd1e-47ea-922f-85418e9da687
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# 4.4 Preparação de dados em Customer Journey Analytics

## Objetivos

- Entenda a UO do Analysis Workspace no CJA
- Entenda os concepitos de preparação de dados no Analysis Workspace
- Aprenda a fazer cálculos de dados

## 4.4.1 Interfaccia utente di Analysis Workspace su CJA

O Analysis Workspace rimuovere todas come limitações típicas de um único relatório do Analytics. Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes (dimensões, métricas, segmentos e granularidades de tempo) para um projeto. Criação instantânea de avarias e segmentos, criação de cortes para análise, criação de alertas, comparação de segmentos, análise de fluxo e de falhas e relatórios de curadoria e agendamento para compartilhar com qualquer pessoa em seu negócio.

O Customer Journey Analytics traz essa solução além dos dados da plataforma. É comendável assistir a este vídeo de visão geral de quatro minutos:

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

Se você nunca usou o Analysis Workspace antes, consiglio:

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### Crie Seu Projeto

Agora é hora de criar seu primeiro projeto do CJA. Vá para a aba de projetos dentro do CJA. Clique em **Crea nuovo**.

![demo](./images/prmenu.png)

Em seguida, você verá a tela abaixo. Selecione **Progetto vuoto** então clique em **Crea**.

![demo](./images/prmenu1.png)

Você verá um projeto vazio.

![demo](./images/premptyprojects.png)

Primeiro, certifique-se de selecionar a Visualização de dados correta no canto superior direito da tela. Neste exemplo, una Visualização de dados a ser selecionada é `vangeluwe - Omnichannel Data View`.

![demo](./images/prdv.png)

Voce irá salvar seu projeto e dar um nome a ele. Você pode usar o seguinte comando para salvar:

| Sistema operativo | Scelta rapida |
| ----------------- |-------------| 
| Windows | Ctrl+S |
| Mac | Comando+S |

Você verá este pop-up:

![demo](./images/prsave.png)

Usare este modelo de nomenclatura:

| Nome | Descrizione |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em seguida, cricca em **Salva**.

![demo](./images/prsave2.png)

## 4.4.2 Calcoli metrici

Embora tenhamos organizado todos os componentes na Visualização de dados, você ainda deve adaptar alguns deles para que os usuários de negócios estejam prontos para iniciar suas análises. Além disso, durante qualquer processo de analytics, você pode criar métricas calculadas para aprofoundation a descoberta de insights.

Como exemplo, criaremos uma Taxa de conversão calcolada a métrica/evento Compras que definimos na Visualização de dados.

## Taxa de conversão

Vamos começar a abrir o construtor de métricas calculadas. Clique em **+** para criar sua primeira Métrica calculada no Analysis Workspace.

![demo](./images/pradd.png)

O **Generatore di metriche calcolate** aparecer irá:

![demo](./images/prbuilder.png)

Incontra **Acquisti** una lista de métricas no menu do lado esquerdo Em **Metriche** cricca em **Mostra tutto**

![demo](./images/calcbuildercr1.png)

Agora arraste e solte a métrica **Acquisti** una definição da métrica calculada

![demo](./images/calcbuildercr2.png)

Normalmente, taxa di conversione **Conversioni/Sessioni**. Então, vamos fazer o mesmo cálculo na tela de definição de métrica calculada. Encontre a métrica **Sessioni** e arraste e solte-a no criador de definição, no evento **Acquisti**.

![demo](./images/calcbuildercr3.png)

Observe que o operador de divisão é selecionado.

![demo](./images/calcbuildercr4.png)

Un taxa de conversão é comumente rappresentada em porcentagem. Então, vamos mudar o formato para porcentagem e selecionar 2 casas decimais.

![demo](./images/calcbuildercr5.png)

Infine, modifica il nome e la descrizione della metrica calcolata:

| Titolo | Descrizione |
| ----------------- |-------------| 
| Tasso di conversione | Tasso di conversione |

Por fim, altere o nome e a descrição da métrica calculada:

![demo](./images/calcbuildercr6.png)

Não se esqueça de **Salvar** una Métrica calculada.

![demo](./images/pr9.png)

## 4.4.3 Dimensões calculadas: Filtros (segmentação) e interval de datas

### Filtros: Calcoli di Dimensões

Cálculos não devem ser apenas para métricas. Antes de iniciar qualquer análise, também é interessante criar algumas **Dimension calcolati**. Isso, essencialmente, **segmenti** nessun Adobe Analytics. Nessun Customer Journey Analytics, ses segmentos são chamados de **Filtri**.

![demo](./images/prfilters.png)

Un criação de filtros ajudará os usuários de negócios un iniciar o analytics com algumas dimensões calculadas valiosas. Isso irá automatizar algumas tarefas, além de ajudar na parte de adoção. Abaixo estão alguns exemplos:

1. Mídia Própria, Mídia Paga
2. Visitas novas x recorrentes
3. Clientes com carrinho abbandonado

Esses filtros podem ser criados antes ou durante a parte de análise (o que você fará no próximo exercício).

### Intervalos de datas: Dimensões de tempo calculadas

Come dimensões de tempo são outro tipo de dimensioni calculadas. Alguns já foram criados, mas você também pode criar suas próprias Dimensões de tempo personalizadas na fase de preparação de dados.

Essas Dimensões de tempo calculado ajudarão analistas e usuários de negócios a lembrar datas importantes e usá-las para filtrar e alterar o tempo de relatório. Perguntas e dúvidas típicas quando fazemos análises:

- Quando è un Black Friday do ano passado? Immetti os dias 21 e 29?
- Quando veicoli ulamos aquela campanha de TV em dezembro?
- De quando a quando fizemos è vendas de verão de 2018? Quero comparar com 2019. Un propósito, você sabe os dias exatos em 2019?

![demo](./images/timedimensions.png)

Agora você conclusiu o exercício de preparação de dados o Analysis Workspace do CJA.

Próxima etapa [4.5 Customer Journey Analytics Visualização](./ex5.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
