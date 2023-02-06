---
title: Bootcamp - Customer Journey Analytics - Crea una visualizzazione dati - Brasile
description: Customer Journey Analytics - Creare una visualizzazione dati - Brasile
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 072179998d19c32589280defdb257a86d8728fea
workflow-type: tm+mt
source-wordcount: '1655'
ht-degree: 2%

---

# 4.3 Criterio uma Visualização de Dados

## Obiettivi

- Entenda a UI de Visualização de Dados
- Compreenda come configurações básicas de definição de visita
- Compreenda a atribuição e a Persistência em uma Visualização de de Persistência

## 4.3.1 Visualização de Dados

Agora, com sua conexão concluída, é possível progressive para influenciar a visualização. Uma diferença entre of Adobe Analytics e o CJA é que o CJA precisa de uma visualização de dados para limpar e preparar os dados antes da visualização.

Uma Visualização de Dados é semelhante ao concito de Virtual Report Suite no Adobe Analytics, onde você estabelece as definições de visita com reconhecimento de contexto, filtragem e também como os componentes são chamados.

Será necessário, no mínimo, uma Visualização de Dados por conexão. No entanto, para alguns casos de uso, é ótimo ter múltiplas Visualizações de Dados para a mesma conexão, com o objetivo de fornecer insights diferentes para attrezzes distintas. Se você deseja que sua empresa seja orientada por dados, deve adaptar a como os dados são vistos em cada attrezze. Gli algoritmi sfruttano:

- Métricas de UX apenas para a Equipment de UX Design
- Usa os mesmos nomes para KPI e métricas para o Google Analytics e para o Customer Journey Analytics, para que a equipe de análise digital fale apenas 1 idioma.
- Visualização de Dados filtrada para mostrar, por exemplo, dados para apenas um mercado, ou uma marca, ou apenas para Dispositivos móveis.

Na tela **Connessioni** marque a caixa de seleção da conexão que você acabou de criar. Clipart  **Crea visualizzazione dati**.

![demo](./images/exta.png)

Você será redirecionado para o fluxo de trabalho **Crea visualizzazione dati** workflow.

![demo](./images/0-v2.png)

## 4.3.2 Definição de Visualização de Dados

Agora você pode configurar as definições básicas para la sua Visualização de dados.

![demo](./images/0-v2.png)

A **Connessione** que você criou no exercício anteriore já está selionada. Sama conexão se chama `yourLastName – Omnichannel Data Connection`.

![demo](./images/ext5.png)

Em seguida, dê um nome à sua Visualização de Dados seguindo este modelo de nomenclatura: `yourLastName – Omnichannel Data View`.

Insira o mesmo valor para a description: `yourLastName – Omnichannel Data View`.

| Nome | Descrizione |
| ----------------- |-------------| 
| `yourLastName – Omnichannel Data View` | `yourLastName – Omnichannel Data View` |

![demo](./images/1-v2.png)

Para **Fuso orario**, selione o fuso a horário **Berlim, Estocolmo, Roma, Berna, Bruxelas, Viena, Amsterdã GMT+01:00**. Este é um cenário interessante, pois algumas empresas operam em diferentes países e geografias. Alocar o horário certo para cada país evará erros típicos de dados, como, por exemplo, acreditar que a maioria das pessoas compreso camisetas às 4h no Perù.

![demo](./images/ext7.png)

Você também pode modificar a nomenclatura das métricas princippais (Pessoa, Sessão e Evento). Isso não é obrigatório, mas alguns clientes gostam de usar Pessoas, Visitas e Acessos em vez de Pessoa, Sessão e Eventos (convocção de nomenclatura padrão do Customer Journey Analytics).

Agora você dev as seguintes configurações definidas:

![demo](./images/1-v2.png)

Clipart **Salva e continua**.

![demo](./images/12-v2.png)

## 4.3.3 Componenti da Visualização de Dados

Neste exercício, você irá configurar os componentes necessários para analisar os dados e visalizá-los o Analysis Workspace. Nesta IU, há três áreas princippais:

- Lado esquerdo: Componenti disponíveis dos datasets selionados
- Meio: Componenti adicionados à Visualização de Dados
- Lado direito: Configurações do

![demo](./images/2-v2.png)

>[!IMPORTANT]
>
>Se você não encontrar uma métrica ou dimensão specífica, verifique se o campo `Contains data` foi removido de sua visualização de dados. Caso contrário, esclua esse campo.
>
>![demo](./images/2-v2a.png)

Agora você precisa arrastar e soltar os componentes necessários para a análise nos **Componenti aggiunti**. Para isso, você deve selionar os componentes no menu à esquerda e arrastá-los e soltá-los na tela no meio.

Vamos começar com o primeiro: **Nome (web.webPageDetails.name)**. Pesquise esse destina e arraste-o solte-o na tela.

![demo](./images/3-v2.png)

Sono componenti o nome da página, como vocare poderivati da leitura do campo do schema `(web.webPageDetails.name)`.

No entanto, usar **Nome** como o nome não é a melhor convocção de classificazione para um usuário corporativo compressender essa dimensão.

Vamos mudar o nome para **Nome pagina**. Clique no deste o renomeie na área **Impostazioni dei componenti**.

![demo](./images/3-0-v2.png)

Come Configurações de persistência são **Impostazioni di persistenza**. Os concitos de eVars e prop não exists no CJA, mas as configurações de Persistência possibilitam um comportamento semelhante.

![demo](./images/3-0-v21.png)

Se você não alterar essas configurações o CJA irá interpretar a dimensão como um **Prop** (nível de ocorrência). Além disso, podemoar alterar a Persistência para tornar a dimensão uma **eVar** (persistir o valor ao longo da jornada).

Se você não estiver familiarizado com eVars e Props, [leia mais sobre isso documentação](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html).

Vamos deixar o Nome da Página como Prop. Dessa forma, você não precisa alterar nenhuma **Impostazioni di persistenza**.

| Nome componente da cercare | Nuovo nome | Impostazioni di persistenza |
| ----------------- |-------------| --------------------| 
| Nome (web.webPageDetails.name) | Nome pagina |  |

Em seguida, escolha a dimensão **phoneNumber** e solte-a na tela. O nuovo nome DEVE **Numero di telefono**.

![demo](./images/3-1-v2.png)

Por fim, vamos alterar as Configurações de persistência, pois o Número do Celular deve persistir no nível do usuário.

Para alterar a Persistência, ruolo para baixo no menu à direita e abra a aba **Persistenza**:

![demo](./images/5-v2.png)

Marque a caixa de seleção para modificar as configurações de persistência. Selecione **Più recente** e o escopo **Persona (intervallo di reporting)**, pois nos preocupamos apenas com o último número de celular da pessoa. Se o cliente não preencher o celular em visitas futuras, você ainda verá esse valor preenchido.

![demo](./images/6-v2.png)

| Nome componente da cercare | Nuovo nome | Impostazioni di persistenza |
| ----------------- |-------------| --------------------| 
| phoneNumber | Numero di telefono | Più recente, Persona (intervallo di reporting) |

O próximo in `web.webPageDetails.pageViews.value`.

Nessun menu à esquerda, peschezza `web.webPageDetails.pageViews.value`. Arraste e solte essa métrica na tela.

Altere o nome para **Visualizzazioni pagina** in **Impostazioni dei componenti**.

| Nome componente da cercare | Nuovo nome | Impostazioni di attribuzione |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | Page Views |  |

![demo](./images/7-v2.png)

Para as configurações de atribuição, deixaremos em branco.

Osservatorio: Come configurações de persistência nas métricas também podem ser alteradas no Analysis Workspace. Em alguns casos, você pode optar por configurá-las aqui para evitar que os usuários de negócios tenham decar qual é o melhor modelo de persistência.

Em seguida, você terá que configurar várias Dimensões e Métricas, conforme indicado na tabela abaixo.

### DIMENSIONS ES

| Nome componente da cercare | Nuovo nome | Impostazioni di persistenza |
| ----------------- |-------------| --------------------| 
| brandName | Nome del marchio | Sessione più recente |
| sentimento | Sensazione di chiamata |  |
| ID chiamata | Tipo di interazione chiamata |  |
| callTopic | Argomento della chiamata | Sessione più recente |
| ecid | ECID | Più recente, Persona (intervallo di reporting) |
| e-mail | ID e-mail | Più recente, Persona (intervallo di reporting) |
| Tipo di pagamento | Tipo di pagamento |  |
| Metodo di aggiunta dei prodotti | Metodo di aggiunta dei prodotti | Sessione più recente |
| Tipo evento | Tipo evento |  |
| Nome (productListItems.name) | Nome del prodotto |  |
| SKU | SKU (sessione) | Sessione più recente |
| ID transazione | ID transazione |  |
| URL (web.webPageDetails.URL) | URL |  |
| Agente utente | Agente utente | Sessione più recente |

### MÉTRICA

| Nome componente da cercare | Nuovo nome | Impostazioni di attribuzione |
| ----------------- |-------------| --------------------| 
| Quantità | Quantità |  |
| commerce.order.priceTotal | Ricavi |  |

Sua configuração deve ser semelhante ao seguinte:

![demo](./images/11-v2.png)

Não se esqueça de Salvar sua Visualização de Dados. Clic Então em **Salva**.

![demo](./images/12-v2s.png)

## 4.3.4 Métricas calcoladas

Embora tenhamos organizado todos os componentes na Visualização de dados, você ainda deve adaptar alguns deles para que os usuários de negócios estejam prontos para iniciar suas análises.

Se você se lembra, não trouxemos specificamente Métricas como Adicionar ao Carrinho, Visualização do produto ou Compras para a Visualização de dados. No entanto, temos uma dimensão chamada: **Tipo evento**. Então, vamos derivati esses tipos de interação criando 3 métricas calculadas.

Vamos começar com a primeira Métrica: **Visualizzazioni prodotto**.

Nessun lado esquerdo, peschezza **Tipo evento** e selezionate un dimensão. Em seguida, arraste-o e solte-o na tela **Componenti inclusi**.

![demo](./images/calcmetr1.png)

Clique para selionar a nova métrica **Tipo evento**.

![demo](./images/calcmetr2.png)

Agora altere nome e a descrição do ceros seguintes valores:

| Nome componente | Descrizione del componente |
| ----------------- |-------------| 
| Visualizzazioni prodotto | Visualizzazioni prodotto |

![demo](./images/calcmetr3.png)

Agora vamos contar apenas eventos de **Visualizzazioni prodotto**. Para fazer isso, ruolo para baixo em **Impostazioni dei componenti** até ver Valores de Valores **Includi valori di esclusione**. Certifique-se de habilitar a opção **Imposta valori di inclusione/esclusione**.

![demo](./images/calcmetr4.png)

Como queremos apene contadine **Visualizzazioni prodotto**, specifiche **commerce.productViews** nos critérios.

![demo](./images/calcmetr5.png)

Agora a sua sua sua Calada está pronta!

Em seguida, repita o mesmo sette para os eventos **Aggiungi al carrello** e **Acquisto**.

### Aggiungi al carrello

Primeiro, arraste e solte a mesma dimensão **Tipo evento**.

![demo](./images/calcmetr1.png)

Você verá um alerta pop-up de um Campo Duplicado, pois estamos a mesma variável. Clipart **Aggiungi comunque**:

![demo](./images/calcmetr6.png)

Agora, siga o mesmo sette fizemos para a métrica Visualizações de produto:
- Altopiano di Primeiro o nome e una descrizione.
- Por fim, adicione **commerce.productListAdd** como critério para contar apenas Aggiungi al carrello

| Nome | Discrepione | Criteri |
| ----------------- |-------------| -------------|
| Aggiungi al carrello | Aggiungi al carrello | commerce.productListAdds |

![demo](./images/calcmetr6a.png)

### Acquisti

Primeiro, arraste e solte a mesma dimensão **Tipo evento** como fizemos para as duas métricas anteriori.

![demo](./images/calcmetr1.png)

Você verá um alerta pop-up de um Campo Duplicado, pois estamos a mesma variável. Clipart **Aggiungi comunque**:

![demo](./images/calcmetr7.png)

Agora, siga o mesmo sette fizemos para as métricas Visualizzazioni prodotto e Aggiungi al carrello:
- Altopiano di Primeiro o nome e una descrizione.
- Por fim, adicione **commerce.purchase** como critérios para contabil izar apenas come Compras

| Nome | Discrepione | Criteri |
| ----------------- |-------------| -------------|
| Acquisti | Acquisti | commerce.purchases |

![demo](./images/calcmetr7a.png)

Sana configuração finale deve ser semelhante ao seguinte. Clipart **Salva e continua**.

![demo](./images/calcmetr8.png)

## 4.3.5 Componenti da Configuração de Dados

Você deve ser redirecionado para esta tela:

![demo](./images/8-v2.png)

Nesta aba, você pode modificar algumas configurações importantes para alterar a forma como os dados são processados. Vamos começar definindo o **Timeout sessione** como 30 min. Graças ao registro de data e hora de cada evento de experiência, você pode estender o concito de uma sessão em todos os canais. Por exemplo que acontece se um cliente ligar para o call center depois de visitar o site? Usando Tempos Limite de Sessão personalizados, você tem muita flexibilidade para decidir o que é uma sessão e como essa sessão irá mesclar os dados.

![demo](./images/ext8.png)

Nesta ê pode modificar outras coisas coisas filtrar os dados segmento/filtro. Você não precisará fazer isso neste exercício.

![demo](./images/10-v2.png)

Quando terminar, clique em **Salva e completa**.

![demo](./images/13-v2.png)

>[!NOTE]
>
>Você pode di voltar a esta Visualização de dados posteriori e alterar as configurações e os components a qualquer momento. Come alterações afetarão a forma como os dados históricos são mostrados.

Agora você pode continuar com a parte de visualização e análise!

Próxima etapa: [4.4 Customer Journey Analytics di Preparação de dados em](./ex4.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
