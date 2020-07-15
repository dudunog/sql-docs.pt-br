---
title: MSSQLSERVER_916 | Microsoft Docs
description: O logon não tem permissões suficientes para conectar-se ao banco de dados nomeado do SQL Server. Veja uma explicação do erro e as possíveis resoluções.
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 916 (Database Engine error)
ms.assetid: 73eb6581-99fe-49a5-9b42-e239d7ffe27f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 510708fd1cd119ee3a665cecb903ff63edbb525e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85636811"
---
# <a name="mssqlserver_916"></a>MSSQLSERVER_916
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|916|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|NOTUSER|  
|Texto da mensagem|A entidade de segurança do servidor "%.*ls" não é capaz de acessar o banco de dados "%.\*ls" no contexto de segurança atual.|  
  
## <a name="explanation"></a>Explicação  
O logon não tem permissões suficientes para conectar-se ao banco de dados nomeado. Os logons que podem conectar-se a essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas que não têm permissões específicas em um banco de dados, recebem as permissões do usuário convidado. Esta é uma medida de segurança para evitar que usuários em um banco de dados se conectem a outros bancos de dados em que não têm privilégios. Esta mensagem de erro pode ocorrer quando o usuário convidado não tem permissão CONNECT para o banco de dados nomeado e a propriedade confiável não está definida. Essa mensagem de erro poderá ser exibida quando o usuário convidado não tiver a permissão CONNECT para o banco de dados nomeado.  
  
Quando a permissão CONNECT para o banco de dados msdb for negada ou revogada, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] poderá receber esse erro quando o Pesquisador de Objetos tentar mostrar o status do gerenciamento baseado em políticas de cada banco de dados. O Pesquisador de Objetos usa as permissões do logon atual para consultar o banco de dados msdb quanto a essas informações, o que causa o erro. A seguinte mensagem de erro também ocorre:  
  
Falha ao recuperar dados para esta solicitação. (Microsoft.SqlServer.Management.Sdk.Sfc)  
  
## <a name="user-action"></a>Ação do usuário  
  
> [!WARNING]  
> Para evitar esta medida de segurança, verifique se há uma compreensão clara sobre a autenticação de usuários em diversos bancos de dados. Os métodos a seguir talvez permitam que usuários tenham permissões em um banco de dados para se conectarem a outros bancos de dados que podem expor os dados a um usuário mal-intencionado. Quando os bancos de dados independentes são habilitados, as etapas a seguir podem permitir proprietários de banco de dados em um banco de dados para conceder acesso a outro banco de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Você pode se conectar ao banco de dados de uma das seguintes maneiras:  
  
-   Concedendo ao logon específico acesso ao banco de dados nomeado. O exemplo a seguir concede ao logon `Adventure-Works\Larry` acesso ao banco de dados `msdb`.  

    ```sql
    USE msdb ;
    
    GO
    
    GRANT CONNECT TO [Adventure-Works\Larry] ;
    ```
  
-   Concedendo a permissão CONNECT ao banco de dados nomeado na mensagem de erro para o usuário convidado. O exemplo a seguir concede a permissão `CONNECT` ao banco de dados `msdb` para o usuário `guest`.  

    ```sql
    USE msdb ;
    
    GO
    
    GRANT CONNECT TO guest ;
    ```
  
-   Habilite a propriedade TRUSTWORTHY no banco de dados que tem o usuário autenticado.  

    ```sql
    ALTER DATABASE AdventureWorks SET TRUSTWORTHY ON;
    ```
