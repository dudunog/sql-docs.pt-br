---
title: Solução de problemas do IntelliSense
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- unavailable options [IntelliSense]
- IntelliSense [SQL Server], troubleshooting
- IntelliSense [SQL Server], unavailable options
- troubleshooting [IntelliSense]
ms.assetid: 4b72ffc6-aea2-4e11-ab36-fa2de4d7bcc5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: eb7fa5b5b4f12e37ba698c7f912abc2146366ac4
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718195"
---
# <a name="troubleshooting-intellisense-sql-server-management-studio"></a>Solucionando problemas do IntelliSense (SQL Server Management Studio)
  Em certos casos, o funcionamento das opções do IntelliSense podem não ser o esperado:  
  
## <a name="conditions-that-affect-intellisense"></a>Condições que afetam o IntelliSense  
 As seguintes condições podem afetar o comportamento do IntelliSense:  
  
-   Há um erro de código acima do cursor.  
  
     Se houver uma instrução incompleta ou outro erro de código acima do local do ponto de inserção, o IntelliSense talvez não consiga analisar os elementos do código e por isso não funcionará. Você pode comentar o código aplicável para habilitar o IntelliSense novamente.  
  
-   O ponto de inserção está dentro de um comentário de código.  
  
     As opções do IntelliSense não são disponibilizadas quando o ponto de inserção está dentro de um comentário no arquivo de origem.  
  
-   O ponto de inserção está dentro de uma literal da cadeia de caracteres.  
  
     As opções do IntelliSense não serão disponibilizadas quando o ponto de inserção estiver entre as aspas que envolvem uma literal de cadeia de caracteres, por exemplo:  
  
     `WHERE FirstName LIKE 'Patri%|'`  
  
-   As opções automáticas estão desativadas.  
  
     Muitos recursos do IntelliSense funcionam automaticamente por padrão, mas qualquer recurso pode ser desabilitado.  
  
     Mesmo quando a conclusão automática da instrução está desabilitada, é possível usar um recurso do IntelliSense. Para obter mais informações, consulte [Configurar IntelliSense &#40;SQL Server Management Studio&#41;](configure-intellisense-sql-server-management-studio.md).  
  
## <a name="database-engine-query-intellisense"></a>Consulta do Mecanismo de Banco de Dados do IntelliSense  
 As questões a seguir se aplicam ao Editor de Consultas [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] :  
  
-   A funcionalidade IntelliSense do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não dá suporte para todos os elementos de sintaxe do [!INCLUDE[tsql](../../includes/tsql-md.md)] . A ajuda do parâmetro não dá suporte para os parâmetros em alguns objetos, como procedimentos armazenados estendidos. Para obter mais informações, consulte [Sintaxe Transact-SQL com suporte do IntelliSense](transact-sql-syntax-supported-by-intellisense.md).  
  
-   O IntelliSense está disponível apenas quando o Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] está conectado a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou posterior. O IntelliSense não está disponível quando o Editor de Consultas está conectado a versões anteriores do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   O IntelliSense é desativado no Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] quando o modo SQLCMD está ativado.  
  
-   A funcionalidade do IntelliSense não abrange objetos de banco de dados criados por outra conexão depois que a janela do editor está conectada ao banco de dados. Se os objetos estiverem ausentes nos recursos do IntelliSense, como as listas de conclusão, você poderá escolher um destes três mecanismos para atualizar o cache de objetos da janela do editor:  
  
    -   Selecione o menu **Editar** , selecione **IntelliSense**e selecione **Atualizar Cache Local**.  
  
    -   Use as teclas de atalho CTRL+Shift+R.  
  
    -   Desconecte a janela do editor da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e reconecte.  
  
-   As listas de conclusão não contêm os objetos de banco de dados para os quais você não tem permissões. O IntelliSense sinaliza as referências aos objetos para os quais você tem permissões. Por exemplo, se você abrir um script gravado por outra pessoa, as referências aos objetos para os quais essa pessoa tem permissões e você não tem serão sinalizadas como incorretas.  
  
-   As listas de conclusão podem deixar de funcionar se a conexão com a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]for desfeita. Reconecte à instância.  
  
  
