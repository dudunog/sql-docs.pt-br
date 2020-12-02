---
description: Gerenciador de conexões do cache
title: Gerenciador de Conexões do Cache | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.cacheconnection.f1
helpviewer_keywords:
- Cache connection manager
ms.assetid: bdc92038-3720-4795-8a5c-79b963f2c952
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 074aa791a20eed06241aef1087f5ac355f8ea493
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123709"
---
# <a name="cache-connection-manager"></a>Gerenciador de conexões do cache

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  O gerenciador de conexões do Cache lê dados da transformação Cache ou de um arquivo de cache (.caw) e salva os dados em um arquivo de cache. Se você configurar o gerenciador de conexões do Cache para usar um arquivo de cache, os dados sempre serão armazenados na memória.  
  
 A transformação Cache grava dados de uma fonte de dados conectada no fluxo de dados para um gerenciador de conexões do Cache. A transformação Pesquisa em um pacote realiza pesquisas nos dados.  
  
> [!NOTE]  
>  O gerenciador de conexões do Cache não oferece suporte aos tipos de dados BLOB (objetos binários grandes) DT_TEXT, DT_NTEXT e DT_IMAGE. Se o conjunto de dados de referência contiver um tipo de dados BLOB, o componente irá falhar quando o pacote for executado. Você pode usar o **Editor do Gerenciador de Conexões de Cache** para modificar os tipos de dados da coluna. Para obter mais informações, consulte [Cache Connection Manager Editor]().  
  
> [!NOTE]  
>  O nível de proteção do pacote não se aplica ao arquivo de cache. Se o arquivo de cache tiver informações confidenciais, use uma lista de controle de acesso (ACL) para restringir o acesso ao local ou à pasta na qual você deseja armazenar o arquivo. Você deve habilitar o acesso apenas para determinadas contas. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../../integration-services/security/security-overview-integration-services.md#files).  
  
## <a name="configuration-of-the-cache-connection-manager"></a>Configuração do gerenciador de conexões do Cache  
 Você pode configurar o gerenciador de conexões do Cache das seguintes maneiras:  
  
-   Indique se precisa usar um arquivo de cache.  
  
     Se você configurar o gerenciador de conexões de cache para usar um arquivo de cache, o gerenciador irá realizar uma das seguintes ações:  
  
    -   Salvar os dados no arquivo quando a transformação Cache estiver configurada para gravar dados de uma fonte de dados no fluxo de dados para o gerenciador de conexões de cache.  
  
    -   Ler os dados do arquivo de cache.  
  
     Para obter mais informações, consulte [Cache Transform](../../integration-services/data-flow/transformations/cache-transform.md).  
  
-   Altere os metadados para as colunas armazenadas no cache.  
  
-   Atualize o nome do arquivo de cache no runtime usando uma expressão para definir a propriedade ConnectionString. Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou programaticamente.  
  
 Para obter informações sobre como configurar um gerenciador de conexões de forma programática, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionar conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="cache-connection-manager-editor"></a>Editor do Gerenciador de Conexões de Cache
  O gerenciador de conexões de Cache lê um conjunto de dados de referência da transformação Cache ou de um arquivo cache (.caw) e salva os dados em um arquivo cache. Os dados sempre são armazenados na memória.  
  
> [!NOTE]  
>  O gerenciador de conexões do Cache não oferece suporte aos tipos de dados BLOB (objetos binários grandes) DT_TEXT, DT_NTEXT e DT_IMAGE. Se o conjunto de dados de referência contiver um tipo de dados BLOB, o componente irá falhar quando o pacote for executado. Você pode usar o **Editor do Gerenciador de Conexões de Cache** para modificar os tipos de dados da coluna.  
  
 A transformação Pesquisa realiza as pesquisas no conjunto de dados de referência.  
  
 A caixa de diálogo **Editor do Gerenciador de Conexões de Cache** inclui as seguintes guias:  
  
###  <a name="general-tab"></a><a name="generaltab"></a> Guia Geral  
 Use a guia **Geral** da caixa de diálogo **Editor do Gerenciador de Conexões de Cache** para indicar se é necessário ler o cache de um arquivo ou salvar o cache em um arquivo.  
  
#### <a name="options"></a>Opções  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de cache no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva a conexão. Como prática recomendável, descreva a conexão de acordo com a sua finalidade para tornar os pacotes autodocumentados e facilitar a sua manutenção.  
  
 **Usar cache de arquivo.**  
 Indique se precisa usar um arquivo de cache.  
  
> [!NOTE]  
>  O nível de proteção do pacote não se aplica ao arquivo de cache. Se o arquivo de cache tiver informações confidenciais, use uma lista de controle de acesso (ACL) para restringir o acesso ao local ou à pasta na qual você deseja armazenar o arquivo. Você deve habilitar o acesso apenas para determinadas contas. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../../integration-services/security/security-overview-integration-services.md#files).  
  
 Se você configurar o gerenciador de conexões de cache para usar um arquivo de cache, o gerenciador irá realizar uma das seguintes ações:  
  
-   Salvar os dados no arquivo quando a transformação Cache estiver configurada para gravar dados de uma fonte de dados no fluxo de dados para o gerenciador de conexões de cache. Para obter mais informações, consulte [Cache Transform](../../integration-services/data-flow/transformations/cache-transform.md).  
  
-   Ler os dados do arquivo de cache.  
  
 **Nome do arquivo**  
 Digite o caminho e o nome do arquivo do arquivo de cache.  
  
 **Procurar**  
 Localize o arquivo de cache.  
  
 **Atualizar metadados**  
 Exclua os metadados de colunas no gerenciador de conexões de Cache e popule novamente o gerenciador de conexões do Cache com matadados de colunas de um arquivo de cache selecionado.  
  
###  <a name="columns-tab"></a><a name="columnstab"></a> Guia Colunas  
 Use a guia **Colunas** da caixa de diálogo **Editor do Gerenciador de Conexões de Cache** para configurar as propriedades de cada coluna no cache.  
  
#### <a name="options"></a>Opções  
 **Coluna**  
 Especifique o nome da coluna.  
  
 **Posição de Índice**  
 Especifique quais colunas são colunas de índice indicando a posição de índice de cada coluna. O índice é uma coleção de uma ou mais colunas.  
  
 Para colunas sem-índice, a posição de índice é 0.  
  
 Para colunas de índice, a posição de índice é um número sequencial positivo. Este número indica a ordem na qual a transformação Pesquisa compara as linhas no conjunto de dados de referência às linhas na fonte de dados de entrada. A coluna com os valores mais exclusivos deve ter a posição de índice mais baixa.  
  
> [!NOTE]  
>  Quando a transformação Pesquisa é configurada para usar um gerenciador de conexões de Cache, somente as colunas de índice no conjunto de dados de referência podem ser mapeadas para as colunas de entrada. Além disso, todas as colunas de índice devem ser mapeadas.  
  
 **Tipo**  
 Especifique o tipo de dados da coluna  
  
 **Comprimento**  
 Especifica o tipo de dados da coluna. Se aplicável ao tipo de dados, você pode atualizar o **Comprimento**.  
  
 **Precisão**  
 Especifica a precisão de alguns tipos de dados de coluna. A precisão é o número de dígitos em um número. Se aplicável ao tipo de dados, você pode atualizar a **Precisão**.  
  
 **Escala**  
 Especifica a escala de alguns tipos de dados de coluna. A escala é o número de dígitos à direita da casa decimal em um número. Se aplicável ao tipo de dados, você pode atualizar a **Escala**.  
  
 **Página de Código**  
 Especifica a página de código para o tipo de coluna. Se aplicável ao tipo de dados, você pode atualizar a **Página de Código**.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Implementar uma Transformação de Pesquisa em modo de Cache Cheio usando o Gerenciador de Conexões de Cache](lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
