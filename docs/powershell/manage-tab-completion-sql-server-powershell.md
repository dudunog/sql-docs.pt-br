---
title: Gerenciar o preenchimento de guias (SQL Server PowerShell) | Microsoft Docs
description: Saiba como controlar o preenchimento com Tab do Windows PowerShell fazendo uso adequado de três variáveis nos módulos do SQL Server PowerShell.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 6296848a-890f-4ad3-8d9f-92ed6a79aa00
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 96e6bf9e0f564e68449a8dfaf99d921c69aadd47
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919092"
---
# <a name="manage-tab-completion-sql-server-powershell"></a>Gerenciar conclusão de guia (SQL Server PowerShell)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

 Os snap-ins do PowerShell no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] apresentam três variáveis (**$SqlServerMaximumTabCompletion**, **$SqlServerMaximumChildItems** e **$SqlServerIncludeSystemObjects**) para controlar o preenchimento com Tab do Windows PowerShell. A conclusão da guia reduz a quantidade de digitação necessária, retornando tabelas de itens cujos nomes iniciam com a cadeia de caracteres que você está digitando.  

> [!NOTE]
> Há dois módulos do SQL Server PowerShell; **SqlServer** e **SQLPS**. O módulo **SQLPS** está incluído na instalação do SQL Server (para compatibilidade com versões anteriores), mas não está sendo atualizado. O módulo do PowerShell mais atualizado é o módulo do **SqlServer**. O módulo do **SqlServer** contém versões atualizadas dos cmdlets no **SQLPS** e também inclui novos cmdlets para dar suporte aos recursos mais recentes do SQL.  
> As versões anteriores do módulo do **SqlServer** *foram* incluídas no SQL Server Management Studio (SSMS), mas apenas nas versões 16.x do SSMS. Para usar o PowerShell com o SSMS 17.0 e versões posteriores, o módulo do **SqlServer** deve ser instalado da Galeria do PowerShell.
> Para instalar o módulo do **SqlServer**, consulte [Instalar o SQL Server PowerShell](download-sql-server-ps-module.md).
  
Com a tab-completion do Windows PowerShell, quando você digita parte do nome de um caminho ou cmdlet, pode pressionar a tecla Tab para obter uma lista de itens cujos nomes correspondem aos já digitados. Em seguida, é possível selecionar o item desejado da lista sem precisar digitar o restante do nome.  
  
Se você estiver trabalhando em um banco de dados com muitos objetos, as listas tab-completion poderão se tornar grandes. Alguns tipos de objetos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , como exibições, também têm vários objetos de sistema.  
  
Os snap-ins do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] apresentam três variáveis de sistema que podem ser usadas para controlar a quantidade de informações apresentadas por tab-completion e **Get-ChildItem**.  
  
 **$SqlServerMaximumTabCompletion =** *n*  
 Especifica o número máximo de objetos que devem ser incluídos em uma lista tab-completion. Se você selecionar Tab em um nó de caminho com mais de *n* objetos, a lista tab-completion será truncada em *n*. *n* é um inteiro. 0 é a configuração padrão e significa que não há limite para o número de objetos na lista.  
  
 **$SqlServerMaximumChildItems =** *n*  
 Especifica o número máximo de objetos exibidos por **Get-ChildItem**. Se **Get-ChildItem** for executado em um nó de caminho com mais de *n* objetos, a lista será truncada em *n*. *n* é um inteiro. 0 é a configuração padrão e significa que não há limite para o número de objetos na lista.  
  
 **$SqlServerIncludeSystemObjects =** { **$True** |  **$False** }  
 Se for **$True**, os objetos do sistema serão exibidos por tab-completion e **Get-ChildItem**. Se for **$False**, nenhum objeto de sistema será exibido. A configuração padrão é **$False**.  
  
## <a name="set-the-sql-server-tab-completion-variables"></a>Definir as variáveis de conclusão de guia do SQL Server  
 Para qualquer variável a ser alterada do valor padrão, defina a variável como o novo valor.  
  
### <a name="example-powershell"></a>Exemplo (PowerShell)  
 O exemplo a seguir define todas as três variáveis e lista suas configurações:  
  
```  
$SqlServerMaximumTabCompletion = 20  
$SqlServerMaximumChildItems = 10  
$SqlServerIncludeSystemObjects = $False  
dir variable:sqlserver*  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
