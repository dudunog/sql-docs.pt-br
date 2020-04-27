---
title: Objetos de automação no Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], OLE Automation
- batches [SQL Server], OLE Automation
- OLE Automation [SQL Server]
- OLE Automation [SQL Server], about OLE Automation
ms.assetid: a887d956-4cd0-400a-aa96-00d7abd7c44b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 06913c27af89657aef5a0a5397cd77a1ee025299
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211852"
---
# <a name="ole-automation-objects-in-transact-sql"></a>Objetos de automação OLE em Transact-SQL
  [!INCLUDE[tsql](../../includes/tsql-md.md)] inclui diversos procedimentos armazenados do sistema que permitem que os objetos da Automação OLE sejam mencionados nos lotes, procedimentos armazenados e gatilhos do [!INCLUDE[tsql](../../includes/tsql-md.md)] . Esses procedimentos armazenados do sistema são executados como procedimentos armazenados estendidos, e os objetos de automação OLE executados por meio dos procedimentos armazenados são executados no espaço de endereço de uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] da mesma forma que um procedimento armazenado entendido.  
  
 Os procedimentos armazenados da Automação OLE permitem que os lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] façam referência aos objetos SQL-DMO e aos objetos da Automação OLE personalizados, como objetos que expõe a interface **IDispatch** . Um servidor OLE personalizado em processo criado com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] precisa ter um manipulador de erros (especificado com a instrução **On Error GoTo**) para as sub-rotinas **Class_Initialize** e **Class_Terminate**. Erros sem tratamento nas sub-rotinas **Class_Initialize** e **Class_Terminate** podem causar erros imprevisíveis, como uma violação de acesso em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Recomendam-se também manipuladores de erro para outras sub-rotinas.  
  
 A primeira etapa ao usar um objeto de Automação OLE no [!INCLUDE[tsql](../../includes/tsql-md.md)] é chamar o procedimento armazenado do sistema **sp_OACreate** para criar uma instância de objeto no espaço de endereço da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Após uma instância do objeto ter sido criada, chame os seguintes procedimento armazenados para trabalhar com propriedades, métodos e informações de erro referentes ao objeto:  
  
-   **sp_OAGetProperty** obtém o valor de uma propriedade.  
  
-   **sp_OASetProperty** define o valor de uma propriedade.  
  
-   **sp_OAMethod** chama um método.  
  
-   **sp_OAGetErrorInfo** obtém as informações de erro mais recentes.  
  
 Quando não houver mais necessidade do objeto, chame o **sp_OADestroy** para desalocar a instância do objeto criado usando o **sp_OACreate**.  
  
 Objetos de automação OLE retornam dados através de valores de propriedade e métodos. **sp_OAGetProperty** e **sp_OAMethod** retornam esses valores de dados no formato de um conjunto de resultados.  
  
 O escopo de um objeto de automação OLE é um lote. Todas as referências a um objeto devem estar contidas em um único lote, procedimento armazenado ou gatilho.  
  
 Quando se referem aos objetos, os objetos de automação OLE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dão suporte ao desvio do referido objeto a outros objetos existentes nele. Por exemplo, ao usar o objeto SQL-DMO **SQLServer** , é possível fazer referência a bancos de dados e tabelas contidos nesse servidor.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Sintaxe da hierarquia de objetos &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/object-hierarchy-syntax-transact-sql)  
  
 [Configuração da Área de Superfície](../security/surface-area-configuration.md)  
  
 [Opção de configuração de servidor Ole Automation Procedures](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md)  
  
 [sp_OACreate &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oacreate-transact-sql)  
  
 [sp_OAGetProperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oagetproperty-transact-sql)  
  
 [sp_OASetProperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oasetproperty-transact-sql)  
  
 [sp_OAMethod &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oamethod-transact-sql)  
  
 [sp_OAGetErrorInfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oageterrorinfo-transact-sql)  
  
 [sp_OADestroy &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-oadestroy-transact-sql)  
  
  
