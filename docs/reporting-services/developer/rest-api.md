---
title: Desenvolver usando APIs REST
description: A API REST fornece acesso programático aos objetos em um catálogo do servidor de relatório do SQL Server 2017 Reporting Services.
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: developer
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/12/2018
ms.openlocfilehash: 90ccb4084f9dc2a2a2cd1da4f51281df147524c6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78937675"
---
# <a name="develop-with-the-rest-apis-for-reporting-services"></a>Desenvolver com as APIs REST para o Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

O Microsoft SQL Server 2017 Reporting Services dá suporte a APIs REST (Transferência de Estado Representacional). As APIs REST são pontos de extremidade de serviço que dão suporte a um conjunto de operações HTTP (métodos), que fornecem acesso de criação, recuperação, atualização ou exclusão para recursos em um servidor de relatório.

A API REST fornece acesso programático aos objetos em um catálogo do servidor de relatório do SQL Server 2017 Reporting Services. Exemplos de objetos são pastas, relatórios, KPIs, fontes de dados, conjuntos de dados, planos de atualização, assinaturas e muito mais. Usando a API REST, você pode, por exemplo, navegar pela hierarquia de pastas, descobrir o conteúdo de uma pasta ou baixar uma definição de relatório. Você também pode criar, atualizar e excluir objetos. Exemplos de como trabalhar com objetos são carregar um relatório, executar um plano de atualização, excluir uma pasta e assim por diante.

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-hybrid-note.md)]

## <a name="components-of-a-rest-api-requestresponse"></a>Componentes de uma solicitação/resposta da API REST

Um par de solicitação/resposta da API REST pode ser separado em cinco componentes:

* O **URI de solicitação**, que consiste em `{URI-scheme} :// {URI-host} / {resource-path} ? {query-string}`. Embora o URI de solicitação seja incluído no cabeçalho da mensagem de solicitação, chamamos o URI separadamente aqui porque a maioria das linguagens ou estruturas exige que ele seja passado separadamente da mensagem de solicitação.

    * Esquema de URI: indica o protocolo usado para transmitir a solicitação. Por exemplo, `http` ou `https`.
    * Host de URI: especifica o nome de domínio ou o endereço IP do servidor no qual o ponto de extremidade de serviço REST está hospedado, como `myserver.contoso.com`.
    * Caminho do recurso: especifica o recurso ou a coleção de recursos, que pode incluir vários segmentos usados pelo serviço para determinar a seleção desses recursos. Por exemplo: `CatalogItems(01234567-89ab-cdef-0123-456789abcdef)/Properties` pode ser usado para obter as propriedades especificadas para o CatalogItem.
    * Cadeia de consulta (opcional): fornece parâmetros adicionais simples, como a versão de API ou os critérios de seleção de recursos.

* Campos de cabeçalho da mensagem de solicitação HTTP:

    * Um [método HTTP](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) obrigatório (também conhecido como uma operação ou um verbo), que indica ao serviço que tipo de operação está sendo solicitada. As APIs REST do Reporting Services dão suporte a métodos DELETE, GET, HEAD, PUT, POST e PATCH.
    * Campos de cabeçalho adicionais opcionais, conforme exigido pelo URI e método HTTP especificados.

* Campos opcionais de **corpo da mensagem de solicitação** HTTP, para dar suporte à operação de URI e HTTP. Por exemplo, as operações POST contêm objetos codificado em MIME que são passados como parâmetros complexos. Para operações POST ou PUT, o tipo de codificação MIME do corpo deve ser especificado também no cabeçalho de solicitação `Content-type`. Alguns serviços exigem o uso de um tipo MIME específico, como `application/json`.

* Campos de **cabeçalho da mensagem de resposta** HTTP:

    * Um [código de status HTTP](http://www.w3.org/Protocols/HTTP/HTRESP.html), que varia de códigos de sucesso 2xx a códigos de erro 4xx ou 5xx. Como alternativa, um código de status definido pelo serviço pode ser retornado, conforme indicado na documentação da API.
    * Campos de cabeçalho adicionais opcionais, conforme necessário, para dar suporte à resposta da solicitação, como um cabeçalho de resposta `Content-type`.

* Campos opcionais de **corpo da mensagem de resposta** HTTP:

    * Os objetos de resposta codificados em MIME são retornados no corpo da resposta HTTP, como uma resposta de um método GET que está retornando dados. Normalmente, esses objetos são retornados em um formato estruturado como JSON ou XML, conforme indicado pelo cabeçalho de resposta `Content-type`.

## <a name="api-documentation"></a>Documentação da API

Uma API REST moderna necessita de uma documentação de API moderna. A API REST baseia-se na especificação OpenAPI (também chamada a especificação do swagger) e a documentação está disponível no [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0). Além da documentação da API, o SwaggerHub ajuda a gerar uma biblioteca de cliente na linguagem de sua preferência – JavaScript, TypeScript, C#, Java, Python, Ruby e muito mais.

## <a name="testing-api-calls"></a>Testando chamadas à API

Uma ferramenta para testar as mensagens de solicitação/resposta HTTP é o [Fiddler](https://www.telerik.com/fiddler). O Fiddler é um proxy Web de depuração gratuito que pode interceptar as solicitações REST, facilitando o diagnóstico de mensagens de solicitação/resposta HTTP.

## <a name="next-steps"></a>Próximas etapas

Examine as APIs disponíveis no [SwaggerHub](https://app.swaggerhub.com/api/microsoft-rs/SSRS/2.0).

As amostras estão disponíveis no [GitHub](https://github.com/Microsoft/Reporting-Services). A amostra inclui um aplicativo HTML5 baseado em TypeScript, React e Webpack, juntamente com um exemplo do PowerShell.

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
