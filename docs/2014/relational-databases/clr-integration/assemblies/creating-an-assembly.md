---
title: Criando um assembly | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 995c3a621e6de5d1b878f28c7c0fffaae3311bd2
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84953851"
---
# <a name="creating-an-assembly"></a>Criando um assembly
  Os objetos de banco de dados gerenciado, como os procedimentos armazenados ou gatilhos, são compilados e implantados em unidades chamadas de assembly. Os assemblies DLL gerenciados devem ser registrados no [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)] antes da funcionalidade que o assembly fornece pode ser usado. Para registrar um assembly em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], use a instrução CREATE ASSEMBLY. Este tópico trata sobre como registrar um assembly em um banco de dados usando a instrução CREATE ASSEMBLY e como especificar as configurações de segurança do assembly.  
  
## <a name="the-create-assembly-statement"></a>A instrução CREATE ASSEMBLY  
 A instrução CREATE ASSEMBLY é usada para criar um assembly em um banco de dados. Veja um exemplo:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 A cláusula FROM especifica o nome do caminho do assembly a ser criado. Esse caminho pode ser um caminho UNC (convenção de nomenclatura universal) ou um caminho físico do arquivo que é local no computador.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não permite o registro de versões diferentes de um assembly com nome, cultura e chave pública iguais.  
  
 É possível criar assemblies que referenciem outros. Quando um assembly é criado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , o também cria os assemblies referenciados pelo assembly de nível raiz, se os assemblies referenciados ainda não estiverem criados no banco de dados.  
  
 Os usuários de banco de dados ou as funções de usuário obtêm permissões para criar, e assim ter propriedade sobre, os assemblies em um banco de dados. Para criar assemblies, a função ou o usuário de banco de dados deve ter a permissão CREATE ASSEMBLY.  
  
 Um assembly só poderá ter êxito ao referenciar outros assemblies se:  
  
-   O assembly chamado ou referenciado tem como proprietário o mesmo usuário ou função.  
  
-   O assembly chamado ou referenciado foi criado no mesmo banco de dados.  
  
## <a name="specifying-security-when-creating-assemblies"></a>Especificando a segurança ao criar assemblies  
 Ao criar um assembly em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você pode especificar um dos três diferentes níveis de segurança em que o código pode ser executado: `SAFE`, `EXTERNAL_ACCESS` ou `UNSAFE`. Quando a instrução `CREATE ASSEMBLY` é executada, determinadas verificações são realizadas no assembly do código que podem causar falha no assembly ao se registrar no servidor. Para obter mais informações, consulte o exemplo de representação no [codeplex](https://msftengprodsamples.codeplex.com/).  
  
 `SAFE` é o conjunto de permissões padrão e funciona para a maioria dos cenários. Para especificar um determinado nível de segurança, modifique a sintaxe da instrução CREATE ASSEMBLY da seguinte maneira:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 Também é possível criar um assembly com o conjunto de permissões `SAFE` simplesmente omitindo a terceira linha de código acima:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 Quando o código de um assembly é executado no conjunto de permissões `SAFE`, ele só pode fazer cálculos e acessar dados no servidor através do provedor gerenciado em processo.  
  
### <a name="creating-external_access-and-unsafe-assemblies"></a>Criando assemblies EXTERNAL_ACCESS e UNSAFE  
 O `EXTERNAL_ACCESS` aborda cenários nos quais o código precisa acessar recursos fora do servidor, como arquivos, rede, o Registro e variáveis de ambiente. Sempre que o servidor acessa um recurso externo, ele representa o contexto de segurança do usuário que chama o código gerenciado.  
  
 A permissão de código `UNSAFE` é usada nas situações em que um assembly não é seguro de modo verificável ou exige acesso adicional a recursos restritos, como a API do Win32 da [!INCLUDE[msCoName](../../../includes/msconame-md.md)].  
  
 Para criar um assembly `EXTERNAL_ACCESS` ou `UNSAFE` no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], é necessário atender a uma das duas condições a seguir:  
  
1.  O assembly é assinado com nome forte ou com Authenticode usando um certificado. Esse nome forte (ou certificado) é criado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como uma chave assimétrica (ou certificado) e tem um logon correspondente com a permissão `EXTERNAL ACCESS ASSEMBLY` (para assemblies de acesso externo) ou a permissão `UNSAFE ASSEMBLY` (para assemblies não seguros).  
  
2.  O proprietário do banco de dados (DBO) tem `EXTERNAL ACCESS ASSEMBLY` `EXTERNAL ACCESS` a permissão (para assemblies) ou `UNSAFE ASSEMBLY` (para `UNSAFE` assemblies) e o banco de dados tem a [propriedade de banco de dados TRUSTWORTHY](../../security/trustworthy-database-property.md) definida como `ON` .  
  
 As duas condições listadas acima também são verificadas na hora do carregamento do assembly (que inclui a execução). Pelo menos um das condições precisa ser cumprida para carregar o assembly.  
  
 É recomendável que a [propriedade de banco](../../security/trustworthy-database-property.md) de dados TRUSTWORTHY em um banco de dados não seja definida somente para `ON` executar Common Language Runtime (CLR) no processo do servidor. Em vez disso, recomendamos que seja criada uma chave assimétrica do arquivo de assembly no banco de dados mestre. É necessário criar um logon mapeado para essa chave assimétrica o qual precisa receber a concessão de uma permissão `EXTERNAL ACCESS ASSEMBLY` ou `UNSAFE ASSEMBLY`.  
  
 As instruções a seguir [!INCLUDE[tsql](../../../includes/tsql-md.md)] antes de executar a instrução CREATE assembly.  
  
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
  
 Para criar um assembly `EXTERNAL ACCESS`, o criador precisa ter a permissão `EXTERNAL ACCESS`. Isso é especificado ao criar o assembly:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 As instruções a seguir [!INCLUDE[tsql](../../../includes/tsql-md.md)] antes de executar a instrução CREATE assembly.  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 Para especificar que um assembly é carregado com a permissão `UNSAFE`, especifique o conjunto de permissões `UNSAFE` ao carregar o assembly no servidor:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 Para obter mais detalhes sobre as permissões para cada uma das configurações, consulte [segurança da integração CLR](../security/clr-integration-security.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciando assemblies de integração CLR](managing-clr-integration-assemblies.md)   
 [Alterando um assembly](altering-an-assembly.md)   
 [Descartando um assembly](dropping-an-assembly.md)   
 [Segurança de acesso ao código de integração CLR](../security/clr-integration-code-access-security.md)   
 [propriedade TRUSTWORTHY do banco de dados](../../security/trustworthy-database-property.md)   
 [Permitindo chamadores parcialmente confiáveis](../../../database-engine/dev-guide/allowing-partially-trusted-callers.md)  
  
