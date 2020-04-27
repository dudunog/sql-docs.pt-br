---
title: Bibliotecas de .NET Framework com suporte | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], .NET Framework libraries
- .NET Framework [CLR Integration]
ms.assetid: 417544ff-c25c-496e-add4-2f278f8a4911
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c2518404830577839bce3e84c4eac9b76c850cd3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62873766"
---
# <a name="supported-net-framework-libraries"></a>Bibliotecas do .NET Framework compatíveis
  Com o CLR (common language runtime) hospedado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você pode criar procedimentos armazenados, gatilhos, funções definidas pelo usuário, tipos definidos pelo usuário e agregações definidas pelo usuário em código gerenciado. Com a funcionalidade contida nas bibliotecas de classe do .NET Framework, você tem acesso a classes pré-criadas que fornecem recursos de manipulação de cadeia de caracteres, operações matemáticas avançadas, acesso a arquivos, criptografia, e mais. Essas classes podem ser acessadas de qualquer procedimento armazenado gerenciado, tipo definido pelo usuário, gatilho, função definida pelo usuário ou agregação definida pelo usuário.  
  
> [!NOTE]  
>  Se você atender ou atualizar assemblies sem suporte no GAC (cache de assembly global), seu [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se um assembly existir em uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] integração CLR. Se você reparar ou atualizar qualquer assembly no GAC que também está registrado no banco de dados, incluindo os assemblies do .NET Framework sem suporte, verifique se também reparou ou atualizou a cópia do assembly nos bancos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com a instrução `ALTER ASSEMBLY`. Para obter mais informações, consulte o [artigo 949080 da base de dados de conhecimento](https://support.microsoft.com/kb/949080).  
  
## <a name="supported-libraries"></a>Bibliotecas com suporte  
 A partir [!INCLUDE[ssVersion2005](../../../includes/ssnoversion-md.md)] do tem uma lista de bibliotecas de .NET Framework com suporte, que foram testadas para garantir que elas atendam aos padrões de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] confiabilidade e segurança para interação com as cargas diretamente do GAC (cache de assembly global).  
  
 As bibliotecas/namespaces suportados pela integração CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são:  
  
-   CustomMarshalers  
  
-   Microsoft.VisualBasic  
  
-   Microsoft.VisualC  
  
-   mscorlib  
  
-   Sistema  
  
-   System.Configuration  
  
-   System.Data  
  
-   System.Data.OracleClient  
  
-   System.Data.SqlXml  
  
-   System.Deployment  
  
-   System.Security  
  
-   System.Transactions  
  
-   System.Web.Services  
  
-   System.Xml  
  
-   System.Core.dll  
  
-   System.Xml.Linq.dll  
  
## <a name="unsupported-libraries"></a>Bibliotecas sem-suporte  
 As bibliotecas sem-suporte ainda podem ser chamadas de seus procedimentos armazenados gerenciados, gatilhos, funções definidas pelo usuário, tipos definidos pelo usuário e agregações definidos pelo usuário. A biblioteca sem-suporte deve ser registrada primeiro no banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], usando a instrução `CREATE ASSEMBLY`, antes de poder ser usada no seu código. Qualquer biblioteca sem-suporte que é registrada e executada no servidor deveria ser examinada e testada para fins de segurança e confiabilidade.  
  
 Por exemplo, o namespace `System.DirectoryServices` não é suportado. Você deve registrar o assembly System.DirectoryServices.dll com permissões `UNSAFE` antes de poder chamá-lo do seu código. A permissão `UNSAFE` é necessária porque classes no namespace `System.DirectoryServices` não satisfazem aos requisitos para `SAFE` ou `EXTERNAL_ACCESS`. Para obter mais informações, consulte [restrições de modelo de programação de integração CLR](clr-integration-programming-model-restrictions.md) e segurança de acesso a código de [integração CLR](../security/clr-integration-code-access-security.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um assembly](../assemblies/creating-an-assembly.md)   
 [Segurança de acesso ao código de integração CLR](../security/clr-integration-code-access-security.md)   
 [Restrições do modelo de programação da Integração CLR](clr-integration-programming-model-restrictions.md)  
  
  
