---
title: Bootcamp - Customer Journey Analytics - Collegare i set di dati Adobe Experience Platform in Customer Journey Analytics - Brasile
description: Bootcamp - Customer Journey Analytics - Collegare i set di dati Adobe Experience Platform in Customer Journey Analytics - Brasile
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Connections
exl-id: 51078fca-f234-4e50-96ba-ee7f5e286869
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 0%

---

# 4.2 Set di dati concreti da Adobe Experience Platform nessun Customer Journey Analytics

## Objetivos

- Compreenda un UI da conexão de dados
- Traga os dados da Adobe Experience Platform para o CJA
- Entenda a ID da pessoa e a compilação de dados
- Aprenda o concepito de streaming de dados no Percorso di clienti

## 4.2.1 Conexão

Acesse [analytics.adobe.com](https://analytics.adobe.com) para acessar o Customer Journey Analytics.

Na página inicial do Customer Journey Analytics, acesse **Connessioni**.

![demo](./images/cja2.png)

Aqui você pode ver todas è un distinto conexões feitas entre o CJA e a Plataforma. Essas conexões têm o mesmo objetivo dos conjuntos de relatórios no Adobe Analytics. Niente entanto, un coleta dos dados é completamente diferente. Todos os dados vêm de datasets da Adobe Experience Platform.

Voce principale: Vamos criar sua primeira conexão. **Crea nuova connessione**.

![demo](./images/cja4.png)

Você verá a UI **Crea connessione** UI.

![demo](./images/cja5.png)

Agora você pode dar um nome à sua conexão.

Utilizzare este modello o nomenclatura: `yourLastName – Omnichannel Data Connection`.

Esemplare: `vangeluw - Omnichannel Data Connection`

Você também deve selecionar o sandbox correto para usar. Nessun menu sandbox, sandbox seu selecione, que deve ser `Bootcamp`. Neste exemplo, o sandbox a ser usado é o **Bootcamp**. E você também deve definir o **Numero medio di eventi giornalieri** in **meno di 1 milione**.

![demo](./images/cjasb.png)

Após selecionar seu sandbox, você pode começar a dataset adicionar a esta conexão. **Aggiungi set di dati**.

![demo](./images/cjasb1.png)

## 4.2.2 Set di dati selecione da Adobe Experience Platform

Prequise del set di dati `Demo System - Event Dataset for Website (Global v1.1)`. Clique em **+** para adicionar o dataset a esta conexão.

![demo](./images/cja7.png)

Agora pesquise e marque come caixas de seleção `Demo System - Event Dataset for Voice Assistants (Global v1.1)` e `Demo System - Event Dataset for Call Center (Global v1.1)`.

Em seguida, você verá a tela abaixo. **Avanti**.

![demo](./images/cja9.png)

## 4.2.3 ID da pessoa e compilação de dados

### ID da pessoa

O objetivo agora é juntar esses set di dati. Para cada dataset selecionado, você verá um campo chamado **ID persona**. Cada dataset tem seu próprio campo de ID de pessoa.

![demo](./images/cja11.png)

Como você pode ver, a maioria deles tem o ID da pessoa selecionado. Isso ocorre porque um identador principal é selecionado em cada esquema na Adobe Experience Platform. Como exemplo, aqui está o esquema para `Demo System - Event Schema for Call Center (Global v1.1)`, onde você pode ver que o Identificador Primário está definido como `phoneNumber`.

![demo](./images/cja13.png)

No entanto, você ainda pode influenciar qual identador será usado para compilar datasets para sua conexão. Você pode usar qualquer identador configurado no esquema vinculado ao seu set di dati. Clique no menu suspenso para explorar os IDs disponíveis em cada set di dati.

![demo](./images/cja14.png)

Conforme mencionado, você pode definir diferentes IDs de pessoa para cada set di dati. Isso permite reunir diferentes datasets de múltiplas origens no CJA. Immaginate Trazer NPS ou dados de pesquisa que seriam muito interessantes e úteis para compender o contexto e o motivo de um acontecimento.

O nome do campo ID da pessoa não é importante, desde que o valor nos campos ID da pessoa corresponda. Digamos que temos `email` em um dataset e `emailAddress` em outro dataset definido como ID da pessoa. Vedere `delaigle@adobe.com` tiver o mesmo valor para o campo ID da pessoa em ambos os set di dati, o CJA poderá compilar os dados.

Atualmente, exists algumas outras limitações, como compilar o anônimo para conhecido. Consulta come perguntas freques aqui: [FAQ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html).


### Compilando os dados o ID da pessoa

Agora que você comprende o concepito de compilar datasets o ID da pessoa, vamos escolher `email` como ID da pessoa para cada dataset.

![demo](./images/cja15.png)

Set di dati di Acesse cada para atualizar o ID da pessoa.

![demo](./images/cja12a.png)

Agora preencha o campo ID da pessoa escolhendo o `email` na lista suspensa.

![demo](./images/cja17.png)

Set di dati Depois de compilar os três, estamos prontos para continuar.

| set di dati | ID persona |
| ----------------- |-------------| 
| Sistema di dimostrazione - Set di dati di eventi per il sito web (Global v1.1) | e-mail |
| Sistema demo - Set di dati evento per assistenti vocali (Global v1.1) | e-mail |
| Sistema demo - Set di dati evento per Call Center (Global v1.1) | e-mail |

Você também garantir que, para cada dataset, essas opções estejam habilitadas:

- Importar todos os novos dados
- Preencher todos os dados exists
- Preencher tipo de fonte de dados COM &quot;Altro&quot;
- Preencher a descrição com o mesmo nome do Dataset

**Aggiungi set di dati**.

![demo](./images/cja16.png)

Clique em **Salva** e vá para o próximo exercício. Depois de criar sua **Connessione**, pode levar algumas horas até que seus dados estejam disponíveis no CJA.

![demo](./images/cja20.png)

Eta Próxima: [4.3 Crie uma Visualização de Dados](./ex3.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
