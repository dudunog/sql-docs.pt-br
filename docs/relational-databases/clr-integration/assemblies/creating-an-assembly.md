---
title: Criando um assembly | Microsoft Docs
description: Use CREATE ASSEMBLY para registrar um assembly em SQL Server e especifique suas configurações de segurança. Registre um assembly para usar sua funcionalidade.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- creating assemblies
- UNSAFE assemblies
- CREATE ASSEMBLY statement
- SAFE assemblies
- EXTERNAL_ACCESS assemblies
- assemblies [CLR integration], creating
ms.assetid: a2bc503d-b6b2-4963-8beb-c11c323f18e0
author: rothja
ms.author: jroth
ms.openlocfilehash: 6ca6787abae22722a7bbb99d335e63d47051bb46
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81486825"
---
# <a name="creating-an-assembly"></a>Criando um assembly
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os objetos de banco de dados gerenciado, como os procedimentos armazenados ou gatilhos, são compilados e implantados em unidades chamadas de assembly. Os assemblies DLL gerenciados devem ser [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] registrados no antes da funcionalidade que o assembly fornece pode ser usado. Para registrar um assembly em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], use a instrução CREATE ASSEMBLY. Este tópico trata sobre como registrar um assembly em um banco de dados usando a instrução CREATE ASSEMBLY e como especificar as configurações de segurança do assembly.  
  
## <a name="the-create-assembly-statement"></a>A instrução CREATE ASSEMBLY  
 A instrução CREATE ASSEMBLY é usada para criar um assembly em um banco de dados. Veja um exemplo:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 A cláusula FROM especifica o nome do caminho do assembly a ser criado. Esse caminho pode ser um caminho UNC (convenção de nomenclatura universal) ou um caminho físico do arquivo que é local no computador.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não permite o registro de versões diferentes de um assembly com nome, cultura e chave pública iguais.  
  
 É possível criar assemblies que referenciem outros. Quando um assembly é criado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] também cria os assemblies referenciados pelo assembly do nível raiz, se eles ainda não foram criados no banco de dados.  
  
 Os usuários de banco de dados ou as funções de usuário obtêm permissões para criar, e assim ter propriedade sobre, os assemblies em um banco de dados. Para criar assemblies, a função ou o usuário de banco de dados deve ter a permissão CREATE ASSEMBLY.  
  
 Um assembly só poderá ter êxito ao referenciar outros assemblies se:  
  
-   O assembly chamado ou referenciado tem como proprietário o mesmo usuário ou função.  
  
-   O assembly chamado ou referenciado foi criado no mesmo banco de dados.  
  
## <a name="specifying-security-when-creating-assemblies"></a>Especificando a segurança ao criar assemblies  
 Ao criar um assembly em um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados, você pode especificar um dos três níveis diferentes de segurança em que seu código pode ser executado: **seguro**, **EXTERNAL_ACCESS**ou **não seguro**. Quando a instrução **Create assembly** é executada, determinadas verificações são executadas no assembly de código, o que pode fazer com que o assembly falhe ao se registrar no servidor. Para obter mais informações, consulte o exemplo de representação no [codeplex](https://msftengprodsamples.codeplex.com/).  
  
 **Safe** é o conjunto de permissões padrão e funciona para a maioria dos cenários. Para especificar um determinado nível de segurança, modifique a sintaxe da instrução CREATE ASSEMBLY da seguinte maneira:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 Também é possível criar um assembly com o conjunto de permissões **seguro** , simplesmente omitindo a terceira linha de código acima:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 Quando o código em um assembly é executado sob o conjunto de permissões **seguro** , ele só pode fazer computação e acesso a dados no servidor por meio do provedor gerenciado em processo.  
  
### <a name="creating-external_access-and-unsafe-assemblies"></a>Criando assemblies EXTERNAL_ACCESS e UNSAFE  
 **EXTERNAL_ACCESS** trata dos cenários nos quais o código precisa acessar recursos fora do servidor, como arquivos, rede, registro e variáveis de ambiente. Sempre que o servidor acessa um recurso externo, ele representa o contexto de segurança do usuário que chama o código gerenciado.  
  
 A permissão de código **inseguro** é para essas situações em que um assembly não é verificamente seguro ou requer acesso adicional a recursos restritos, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] como a API do Win32.  
  
 Para criar um assembly **EXTERNAL_ACCESS** ou **não seguro** no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], uma das duas condições a seguir deve ser atendida:  
  
1.  O assembly é assinado com nome forte ou com Authenticode usando um certificado. Esse nome forte (ou certificado) é criado dentro [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como uma chave assimétrica (ou certificado) e tem um logon correspondente com permissão de **assembly de acesso externo** (para assemblies de acesso externo) ou permissão de **assembly não segura** (para assemblies não seguros).  
  
2.  O proprietário do banco de dados (DBO) tem o **assembly de acesso externo** (para ASSEMBLIES de **acesso externo** ) ou a permissão de **assembly não seguro** (para assemblies **não seguros** ) e o banco de dados tem a [propriedade de banco de dados TRUSTWORTHY](../../../relational-databases/security/trustworthy-database-property.md) definida como **on**.  

 As duas condições listadas acima também são verificadas na hora do carregamento do assembly (que inclui a execução). Pelo menos um das condições precisa ser cumprida para carregar o assembly.  
  
 Recomendamos que a [propriedade de banco](../../../relational-databases/security/trustworthy-database-property.md) de dados TRUSTWORTHY em um banco de dados não seja definida como **on** somente para executar o código Common Language Runtime (CLR) no processo do servidor. Em vez disso, recomendamos que seja criada uma chave assimétrica do arquivo de assembly no banco de dados mestre. Um logon mapeado para essa chave assimétrica deve ser criado, e o logon deve receber o **assembly de acesso externo** ou a permissão de **assembly não segura** .  
  
 As instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir executam as etapas necessárias para criar uma chave assimétrica, mapear um logon para essa chave e conceder **EXTERNAL_ACCESS** permissão para o logon. Você deve executar as instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir antes de executar a instrução CREATE ASSEMBLY.  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll'     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey     
GRANT EXTERNAL ACCESS ASSEMBLY TO SQLCLRTestLogin;   
GO   
```  
  
> [!NOTE]  
>  Você deve criar um logon novo para associar com a chave assimétrica. Esse logon é usado somente para conceder permissões; não precisa estar associado a um usuário ou usado dentro do aplicativo.  
  
 Para criar um assembly de **acesso externo** , o criador precisa ter permissão de **acesso externo** . Isso é especificado ao criar o assembly:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 As instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir executam as etapas necessárias para criar uma chave assimétrica, mapear um logon para essa chave e conceder permissão **insegura** ao logon. Você deve executar as instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir antes de executar a instrução CREATE ASSEMBLY.  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 Para especificar que um assembly é carregado com permissão **não segura** , você especifica o conjunto de permissões **não seguro** ao carregar o assembly no servidor:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 Para obter mais detalhes sobre as permissões para cada uma das configurações, consulte [segurança da integração CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciando assemblies de integração CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md)   
 [Alterando um assembly](../../../relational-databases/clr-integration/assemblies/altering-an-assembly.md)   
 [Descartando um assembly](../../../relational-databases/clr-integration/assemblies/dropping-an-assembly.md)   
 [Segurança de acesso ao código de integração CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [propriedade TRUSTWORTHY do banco de dados](../../../relational-databases/security/trustworthy-database-property.md)   
 [Permitindo chamadores parcialmente confiáveis](https://msdn.microsoft.com/library/20b0248f-36da-4fc3-97d2-3789fcf6e084)  
  
  
