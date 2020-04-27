---
title: Identificadores do SQL Server no PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Cmdlets [SQL Server], Encode-Sqlname
- PowerShell [SQL Server], identifiers
- Encode-Sqlname cmdlet
- PowerShell [SQL Server], Encode-Sqlname
- Decode-Sqlname cmdlet
- PowerShell [SQL Server], Decode-Sqlname
- identifiers [SQL Server], PowerShell
- Cmdlets [SQL Server], Decode-Sqlname
ms.assetid: 651099b0-33b4-453a-a864-b067f21eb8b9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3823b6d55439aad860d9176933c348e44acc1ba5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62922840"
---
# <a name="sql-server-identifiers-in-powershell"></a>Identificadores do SQL Server no PowerShell
  O provedor [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para Windows PowerShell usa identificadores [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em caminhos do Windows PowerShell. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Identificadores podem conter caracteres sem suporte pelo Windows PowerShell em caminhos. É necessário substituir esses caracteres ou usar codificação especial quando usar os identificadores em caminhos do Windows PowerShell.  
  
## <a name="sql-server-identifiers-in-windows-powershell-paths"></a>Identificadores do SQL Server em caminhos do Windows PowerShell  
 Os provedores Windows PowerShell expõem as hierarquias de dados usando uma estrutura de caminho semelhante àquela usada no sistema de arquivos do Windows. O provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Windows PowerShell implementa caminhos para objetos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . No [!INCLUDE[ssDE](../includes/ssde-md.md)], a unidade é definida como SQLSERVER:, a primeira pasta é definida como \SQL e os objetos de banco de dados são considerados como contêineres e itens. Este é o caminho para a tabela Vendor no esquema Purchasing do banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] na instância padrão do [!INCLUDE[ssDE](../includes/ssde-md.md)]:  
  
```  
SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Purchasing.Vendor  
```  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Os identificadores são os nomes de objetos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , como nomes de tabela ou coluna. Existem dois tipos de identificadores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] :  
  
-   Os identificadores regulares estão limitados a um conjunto de caracteres que também são suportados em caminhos do Windows PowerShell. Esses nomes podem ser usados em caminhos do Windows PowerShell sem a necessidade de alterá-los.  
  
-   Os identificadores delimitados podem usar caracteres que não são suportados em nomes de caminho do Windows PowerShell. Identificadores delimitados são chamados de identificadores entre colchetes quando estão entre colchetes, como ([IdentifierName]), e identificadores entre aspas quando estão entre aspas, como ("IdentifierName"). Se um identificador delimitado usa caracteres que não são suportados em caminhos do Windows PowerShell, os caracteres devem ser codificados ou substituídos antes de usar o identificador como um contêiner ou nome de item. A codificação aceita todos os caracteres. Alguns caracteres, como o caractere de dois-pontos (:), não pode ser substituído.  
  
## <a name="sql-server-identifiers-in-cmdlets"></a>Identificadores do SQL Server em cmdlets  
 Alguns cmdlets do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contêm um parâmetro que usa um identificador como entrada. Normalmente, os valores de parâmetro são fornecidos como constantes de cadeia de caracteres entre aspas ou em variáveis da cadeia de caracteres. Quando os identificadores são fornecidos como constantes de cadeia de caracteres ou em variáveis, não há conflitos com o conjunto de caracteres suportado pelo Windows PowerShell.  
  
## <a name="sql-server-identifier-tasks"></a>Tarefas do identificador do SQL Server  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como especificar um nome de instância, inclusive o nome do computador no qual a instância está sendo executada.|[Especificar instâncias no provedor do SQL Server PowerShell](sql-server-powershell-provider.md)|  
|Descreve como especificar a codificação hexadecimal para caracteres em identificadores delimitados sem suporte em caminhos do Windows PowerShell. Também descreve como decodificar os caracteres hexadecimais.|[Codificar e decodificar identificadores do SQL Server](encode-and-decode-sql-server-identifiers.md)|  
|Descreve como usar o caractere de escape do Windows PowerShell para caracteres sem suporte em caminhos do PowerShell.|[Retirar identificadores do SQL Server](escape-sql-server-identifiers.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Provedor de SQL Server PowerShell](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)   
 [Identificadores de banco de dados](../relational-databases/databases/database-identifiers.md)  
  
  
