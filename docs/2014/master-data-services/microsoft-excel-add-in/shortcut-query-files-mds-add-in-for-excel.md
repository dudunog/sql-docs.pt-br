---
title: Arquivos de consulta de atalho (Suplemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 1ba0219a-6c40-41fa-aff9-8c8f41ef3220
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 11e875d5b171194c3ac8ba4ad33fad51cacacffe
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65482667"
---
# <a name="shortcut-query-files-mds-add-in-for-excel"></a>Arquivos de consulta de atalho (suplemento MDS para Excel)
  No [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], use arquivos de consulta de atalho para conectar e carregar dados usados frequentemente de forma rápida. Você também pode usá-los quando desejar compartilhar dados do MDS com outros usuários. Em vez de salvar a planilha e enviá-la por email, você deve salvar um arquivo de consulta de atalho e enviá-lo por email. Isso garante que vocês se conectem ao repositório do MDS para obter os dados mais recentes.  
  
 Arquivos de consulta de atalho são arquivos XML que contêm informações sobre:  
  
-   A conexão ao repositório do MDS.  
  
-   O modelo, a versão e a entidade.  
  
-   Qualquer filtro aplicado quando o atalho foi criado.  
  
-   A ordem da esquerda para a direita das colunas quando o atalho foi criado.  
  
 Você pode salvar esses arquivos em uma lista e escolher entre eles quando abrir o suplemento. Você pode exportá-los para o seu computador ou para um local compartilhado, ou pode enviá-los a outros usuários por email.  
  
## <a name="queryopener-application"></a>Aplicativo QueryOpener  
 Todos os usuários que instalam o [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] têm um aplicativo chamado QueryOpener instalado. Esse aplicativo é usado para abrir arquivos de consulta de atalho no [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]. Se você clicar duas vezes em um arquivo de consulta de atalho, esse aplicativo será usado para abrir o arquivo automaticamente no suplemento.  
  
 Ao abrir um arquivo de consulta de atalho com esse aplicativo, você será solicitado tornar a conexão "segura", que o significa que você confia no conteúdo dessa localização. Sempre que você marca uma conexão como segura, ela é adicionada a uma lista. Se desejar apagar essa lista, abra a caixa de diálogo **Configurações** e, na seção **Servidores Adicionados à Lista Segura** , clique em **Desmarcar Tudo**.  
  
 O local padrão para o aplicativo é *drive*: \Program Files\Microsoft SQL Server\120\Master data Services\Excel Add-In\Microsoft.MasterDataServices.QueryOpener.exe.  
  
 Há duas maneiras de abrir arquivos de consulta de atalho: você pode importá-los ou clicar duas vezes neles para abri-los automaticamente.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Salve o conteúdo da planilha ativa como um arquivo de consulta de atalho.|[Salvar um arquivo de consulta de atalho &#40;Suplemento MDS para Excel&#41;](save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Salve o arquivo de consulta de atalho que representa o conteúdo da planilha ativa.|[Enviar um arquivo de consulta de atalho por email &#40;Suplemento MDS para Excel&#41;](email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Conexões &#40;Suplemento MDS para Excel&#41;](connections-mds-add-in-for-excel.md)  
  
-   [Suplemento do Master Data Services para Microsoft Excel](master-data-services-add-in-for-microsoft-excel.md)  
  
-   [Segurança &#40;Master Data Services&#41;](../security-master-data-services.md)  
  
  
