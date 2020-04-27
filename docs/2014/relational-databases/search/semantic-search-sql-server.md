---
title: Pesquisa semântica (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server]
- semantic search [SQL Server], overview
- statistical semantic search [SQL Server]
- statistical semantic search [SQL Server], overview
ms.assetid: cd8faa9d-07db-420d-93f4-a2ea7c974b97
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 651705426b52b822c3eb8c7cf9d341968bbc088f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66010988"
---
# <a name="semantic-search-sql-server"></a>Pesquisa semântica (SQL Server)
  A Pesquisa Semântica Estatística fornece uma profunda compreensão de documentos não estruturados armazenados em bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] extraindo e indexando *frases-chave*estatisticamente relevantes. Portanto, essas frases-chave também são usadas para identificar e indexar *documentos semelhantes ou relacionados*.  
  
 Você consulta esses índices semânticos usando três funções de conjunto de linhas do Transact-SQL para recuperar os resultados como dados estruturados.  
  
##  <a name="what-can-i-do-with-semantic-search"></a><a name="whatcanido"></a>O que posso fazer com a pesquisa semântica?  
 A pesquisa semântica tem como base o recurso de pesquisa de texto completo existente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas habilita novos cenários que ampliam as pesquisas de palavra-chave. Enquanto a pesquisa de texto completo permite que você consulte as *palavras* em um documento, a pesquisa semântica permite a consulta do *significado* do documento. Agora, as soluções possíveis incluem a extração automática de marcas, a descoberta de conteúdo relacionado e a navegação hierárquica por conteúdo semelhante. Por exemplo, você pode consultar o índice de frases-chave para criar a taxonomia para uma organização ou para um corpo de documentos. Ou, você pode consultar o índice de similaridade do documento para identificar os currículos que correspondem a uma descrição do trabalho.  
  
 Os exemplos a seguir demonstram os recursos da Pesquisa Semântica.  
  
###  <a name="find-the-key-phrases-in-a-document"></a><a name="find1"></a>Localizar as frases-chave em um documento  
 A consulta a seguir obtém as frases-chave que foram identificadas no documento de exemplo. Apresenta os resultados em ordem decrescente pela contagem que classifica a significância estatística de cada frase-chave. Essa consulta chama a função [semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql).  
  
```sql  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS Title, keyphrase, score  
    FROM SEMANTICKEYPHRASETABLE(Documents, *, @DocID)  
    ORDER BY score DESC  
  
```  
  
  
  
###  <a name="find-similar-or-related-documents"></a><a name="find2"></a>Localizar documentos semelhantes ou relacionados  
 A consulta a seguir obtém os documentos que foram identificados como semelhantes ou relacionados ao documento de exemplo. Apresenta os resultados em ordem decrescente pela contagem que classifica a semelhança dos 2 documentos. Essa consulta chama a função [semanticsimilaritytable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritytable-transact-sql).  
  
```vb  
SET @Title = 'Sample Document.docx'  
  
SELECT @DocID = DocumentID  
    FROM Documents  
    WHERE DocumentTitle = @Title  
  
SELECT @Title AS SourceTitle, DocumentTitle AS MatchedTitle,  
        DocumentID, score  
    FROM SEMANTICSIMILARITYTABLE(Documents, *, @DocID)  
    INNER JOIN Documents ON DocumentID = matched_document_key  
    ORDER BY score DESC  
  
```  
  
  
  
###  <a name="find-the-key-phrases-that-make-documents-similar-or-related"></a><a name="find3"></a>Localizar as frases-chave que tornam os documentos semelhantes ou relacionados  
 A consulta a seguir obtém as frases-chave que tornam os 2 documentos de exemplo semelhantes ou relacionados a outro documento. Apresenta os resultados em ordem decrescente pela contagem que classifica o peso de cada frase-chave. Essa consulta chama a função [semanticsimilaritydetailstable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semanticsimilaritydetailstable-transact-sql).  
  
```sql  
SET @SourceTitle = 'first.docx'  
SET @MatchedTitle = 'second.docx'  
  
SELECT @SourceDocID = DocumentID FROM Documents WHERE DocumentTitle = @SourceTitle  
SELECT @MatchedDocID = DocumentID FROM Documents WHERE DocumentTitle = @MatchedTitle  
  
SELECT @SourceTitle AS SourceTitle, @MatchedTitle AS MatchedTitle, keyphrase, score  
    FROM semanticsimilaritydetailstable(Documents, DocumentContent,  
        @SourceDocID, DocumentContent, @MatchedDocID)  
    ORDER BY score DESC  
  
```  
  
  
  
##  <a name="storing-documents-in-sql-server"></a><a name="store"></a>Armazenando documentos no SQL Server  
 Antes de você poder indexar documentos com Pesquisa Semântica, é preciso armazenar os documentos em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 O recurso FileTable no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] torna arquivos e documentos não estruturados objetos de primeira classe do banco de dados relacional. Como resultado, os desenvolvedores de banco de dados podem manipular documentos junto com dados estruturados em operações baseadas em conjuntos Transact-SQL.  
  
 Para obter mais informações sobre o recurso FileTable, veja [FileTables &#40;SQL Server&#41;](../blob/filetables-sql-server.md). Para obter informações sobre o recurso FILESTREAM, que é outra opção para armazenar documentos no banco de dados, veja [FILESTREAM &#40;SQL Server&#41;](../blob/filestream-sql-server.md).  
  
  
  
##  <a name="related-tasks"></a><a name="reltasks"></a> Tarefas relacionadas  
 [Instalar e configurar a pesquisa semântica](install-and-configure-semantic-search.md)  
 Descreve os pré-requisitos para a pesquisa semântica estatística e como instalá-los ou verificá-los.  
  
 [Habilitar a pesquisa semântica em tabelas e colunas](enable-semantic-search-on-tables-and-columns.md)  
 Descreve como habilitar ou desabilitar a indexação semântica estatística em colunas selecionadas que contêm documentos ou texto.  
  
 [Localizar frases chave em documentos com a pesquisa semântica](find-key-phrases-in-documents-with-semantic-search.md)  
 Descreve como localizar as frases chave em documentos ou colunas de texto configuradas para indexação semântica estatística.  
  
 [Localizar documentos semelhantes e relacionados com a pesquisa semântica](find-similar-and-related-documents-with-semantic-search.md)  
 Descreve como localizar documentos ou valores de texto semelhantes ou relacionados, e informações sobre como eles são semelhantes ou relacionados, em colunas configuradas para indexação semântica estatística.  
  
 [Gerenciar e monitorar a pesquisa semântica](manage-and-monitor-semantic-search.md)  
 Descreve o processo de indexação semântica e as tarefas relacionadas a monitoramento e gerenciamento dos índices.  
  
##  <a name="related-content"></a><a name="relcontent"></a> Conteúdo relacionado  
 [DDL, funções, procedimentos armazenados e exibições de pesquisa semântica](../views/views.md)  
 Lista as instruções Transact-SQL e os objetos de banco de dados do SQL Server adicionados ou alterados para oferecer suporte à pesquisa semântica estatística.  
  
  
