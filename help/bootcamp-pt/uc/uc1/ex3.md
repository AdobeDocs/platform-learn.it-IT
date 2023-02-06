---
title: Bootcamp - Profilo cliente in tempo reale - Creare un segmento - Interfaccia utente - Brasile
description: Bootcamp - Profilo cliente in tempo reale - Creare un segmento - Interfaccia utente - Brasile
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 9cc01c7d3018319137f915e103bce9dc39b0d472
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# 1.3 Crite um segmento - Interfaccia utente

Neste exercício, você irá criar um segmento o Construtor de Segmentos da Adobe Experience Platform.

## História

Acesse [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer login, você irá acessar a página inicial da Adobe Experience Platform.

![Acquisizione dei dati](./images/home.png)

Antes de continuar, você precisa selionar um **sandbox**. O nome do sandbox un utente selionado é ``Bootcamp``. É possível fazer isso clicando nessun texto **[!UICONTROL Produzione Prod]** na linha azul na parte superior da tela. depois de selionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedica.

![Acquisizione dei dati](./images/sb1.png)

Nessun menu à esquerda, acesse **Segmenti**. Nesta página, você tem uma visão geral de todos os segmentos esiste. Clique no botão + Criar segmento para começar a criar um novo segmento.

![Segmentazione](./images/menuseg.png)

Quando estremo no novo Construtor de segmentos, você irá perceber imediall opção de menu **Attributi** e un referência do **Profilo individuale XDM**.

![Segmentazione](./images/segmentationui.png)

Como o XDM é a linguagem que alimenta o setor de experiência, o XDM também é a base para o Construtor de segmentos. Todos os dados ingeridos na plataforma devem ser mapeados em relação ao XDM e, portanto, todos os dados se tornam parte do mesmo modelo de dados, indipendente da origem desses dados. Isso oferece uma grande vantagem ao criar segmentos, pois a partir dessa interface do usuário do Construtor de segmento, é possível combinar dados de qualquer origem no mesmo fluxo de trabalho. Os segmentos criados no Construtor de segmentos podem enviados para soluções como Adobe Target, Adobe Campaign e Adobe Audience Manager para ativação.

Agora você precisa criar um segmento de todos os clientque visualizaram o produto **Real-Time CDP**.

Para vinuir este segmento, você precisa adicionar um esperienza ência. Você pode encontrar todos os Eventos de experiência clicando no ícone **Eventi** menu a barra **Campi**.

![Segmentazione](./images/findee.png)

Em seguida, você verá o nó **Eventi esperienza XDM** di Nível superiore. Clipart **ExperienceEvent XDM**.

![Segmentazione](./images/see.png)

Acesse **Elementi elenco prodotti**.

![Segmentazione](./images/plitems.png)

Selecione **Nome** e arraste e solte o objeto **Nome** do menu à esquerda na tela do costrutor de segmentos na seção **Eventi**. Em seguida, o seguinte será exibido:

![Segmentazione](./images/eewebpdtlname.png)

O parâmetro de comparação DEVE **è** e, non campo de entrada, insira **Real-time CDP**.

![Segmentazione](./images/pv.png)

Sempre que adicionar ao costrutor de segmentos, você pode clicar no botão **Aggiorna stima** para obter uma nova estimativa da população em seu segmento.

![Segmentazione](./images/refreshest.png)

Para **Metodo di valutazione**, selione **Bordo**.

![Segmentazione](./images/evedge.png)

Por fim, vamos dar um nome ao seu segmento e salvá-lo.

Modello comune di nomenclatura, utilizzare:

- `yourLastName - Interest in Real-Time CDP`

Em seguida, clique no botão **Salva e chiudi** para salvar seu segmento.

![Segmentazione](./images/segmentname.png)

Agora você irá retornar à página de visão geral do segmento, onde verá uma visualização de amostra dos perfis de clientes que se Qualam para o seu segmento.

![Segmentazione](./images/savedsegment.png)

Agora você pode continuar no próximo exercício e usar seu segmento com su Adobe Target.

Próxima etapa: [1.4 Ação: Inviate seu segmento para o Adobe Target](./ex4.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
