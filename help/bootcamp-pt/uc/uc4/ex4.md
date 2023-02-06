---
title: Bootcamp - Customer Journey Analytics - Preparazione dei dati in Analysis Workspace - Brasile
description: Bootcamp - Customer Journey Analytics - Preparazione dei dati in Analysis Workspace - Brasile
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# 4.4 Customer Journey Analytics di Preparação de dados em

## Obiettivi

- Entenda a UO fare Analysis Workspace su CJA
- Entenda os ocitos de preparação de dados no Analysis Workspace
- Aprenda a fazer cálculos de dados

## L’interfaccia utente 4.4.1 utilizza Analysis Workspace su CJA

O Analysis Workspace rimuovere todas as limitações típicas de um único relatório do Analytics. Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arraste e solte qualquer número de tabelas de dados, visualizações e componentes (dimensioni, métricas, segmentos e granularidades de tempo) para um projeto. Criação instantânea de avarias e segmentos, criação de cortes para análise, criação de alertas, comparação de segmentos, análise de fluxo e de falhas e relatórios de curadoria e agendamento para compartilhar com qualquer pessem seu negócio oa.

O Customer Journey Analytics traz essa solução além dos dados da plataforma. É altamente recomendável assistir a este vídeo de visão geral de quatro minutos:

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

Vedere você nunca usou o antes Analysis Workspace, recomendamos este vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### Crie Seu Projeto

Agora é hora de criar seu primeiro projeto do CJA. Vá para a aba de projetos dentro do CJA. Clipart **Crea nuovo**.

![demo](./images/prmenu.png)

Em seguida, você verá a tela abaixo. Selecione **Progetto vuoto** então cliem **Crea**.

![demo](./images/prmenu1.png)

Você verá um projeto vazio.

![demo](./images/premptyprojects.png)

Primeiro, certificfique-se de selecionar a Visualização de dados correta no canto superior direito da tela. Neste exemplo, a Visualização de dados a ser selecionada é `vangeluwe - Omnichannel Data View`.

![demo](./images/prdv.png)

Em seguida, você irá salvar seu projeto e dar um nome a ele. Você pode usar o seguinte comando para salvar:

| Sistema operativo | Taglio corto |
| ----------------- |-------------| 
| Windows | Ctrl+S |
| Mac | Comando+S |

Você verá este pop-up:

![demo](./images/prsave.png)

Utilizzare il modello este di classificazione:

| Nome | Descrizione |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em seguida, clique em **Salva**.

![demo](./images/prsave2.png)

## 4.4.2 Métricas calcolo

Embora tenhamos organizado todos os componentes na Visualização de dados, você ainda deve adaptar alguns deles para que os usuários de negócios estejam prontos para iniciar suas análises. Além disso, durante qualquer sette de analytics, você pode criar métricas calcoladas para aprofundar a descoberta de insights.

Como exemplo, criaremos uma Taxa de conversão calculada a métrica/Compras que definimos na Visualização de dados.

## Taxa de conversão

Vamos começar un abrir o Construtor de métricas calcoladas. Clipart **+** para criar sua primeira Métrica calcolada su Analysis Workspace.

![demo](./images/pradd.png)

O **Generatore di metriche calcolate** aparecer dell&#39;irá:

![demo](./images/prbuilder.png)

Encontra **Acquisti** na lista de métricas no menù do lado esquerdo. Em **Metriche** cricca **Mostra tutto**

![demo](./images/calcbuildercr1.png)

Agora arraste e solte a métrica **Acquisti** na definição da métrica calculada.

![demo](./images/calcbuildercr2.png)

Normalmente, taxa de conversão significa **Conversioni/sessioni**. Então, vamos fazer o mesmo cálculo na tela de definição de métrica calculada. Encontra a métrica **Sessioni** e arraste e solte-a no criador de definição, no evento **Acquisti**.

![demo](./images/calcbuildercr3.png)

Observe que o operador de divisão é selionado automaticamente.

![demo](./images/calcbuildercr4.png)

Un taxa de conversão é comumente rappresentada em porcentagem. Então, vamos mudar o formato para porcentagem e selionar 2 casas decimali.

![demo](./images/calcbuildercr5.png)

Infine, Modifica il nome e la descrizione della metrica calcolata:

| Title | Descrizione |
| ----------------- |-------------| 
| Tasso di conversione | Tasso di conversione |

Por fim, altere o nome e a descrição da métrica calcolada:

![demo](./images/calcbuildercr6.png)

Não se esqueça de **Salvatore** una Métrica calcolada.

![demo](./images/pr9.png)

## 4.4.3 Dimensões calcoladas: Filtros (segmentação) e Interval de datas

### Filtri: Calcoli Dimensões

Os cálculos não devem ser apenas para métricas. Antes de iniciar qualquer análise, também é interessante criar algumas **Dimension calcolati**. Isso significa, essencialmente **segmenti** niente Adobe Analytics. No Customer Journey Analytics, esses segmentos são chamados de **Filtri**.

![demo](./images/prfilters.png)

A criação de filtros ajudará os usuários de negócios a iniciar of analytics com algumas dimensões calculadas valiosas. Isso irá automatizar algumas tarefas, além de ajudar na parte de adoção. Le alghe Abaixo estão sfruttano:

1. Mídia Própria, Mídia Paga,
2. Registri di Visitas novas x
3. Clientes com carrinho abbandonato

Esses filtros podem criados antes ou durante a parte de análise (o que você fará no próximo exercício).

### Intervalos de datas: Dimensões de timografie

Come dimensões de tempo são outro tipo de dimensões calcoladas. Alguns já foram criados, mas você também pode criar suas próprias Dimensões de tempo personalizadas na false de preparação de dados.

Essas Dimensões de tempo calculado ajudarão analistas e usuários de negócios a lembar datas importantes e usá-las para filtrar e alterar o tempo de relatório. Perguntas e dúvidas típicas quando fazemos análises:

- Quando per un Black Friday do ano passado? Entre os dias 21 e 29?
- Quando veic ulamos aquela campanha de TV em dezembro?
- De quando a quando fizemos come vendas de verão de 2018? Quero comparar com 2019. Un propósito, você sabe os dias exatos em 2019?

![demo](./images/timedimensions.png)

Agora você conclusiu o exercício de preparação de dados o Analysis Workspace do CJA.

Próxima etapa: [4.5 Customer Journey Analytics Visualização](./ex5.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
