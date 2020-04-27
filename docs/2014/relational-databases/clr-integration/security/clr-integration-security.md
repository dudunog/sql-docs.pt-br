---
title: Segurança de integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- security [CLR integration]
- authorization [CLR integration]
- common language runtime [SQL Server], security
- database objects [CLR integration], security
ms.assetid: 05d7a471-c5d5-4730-b903-e4edc8157bb4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 12ca3fcb00122313c1d1e4aae8b64733be9140c9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62918998"
---
# <a name="clr-integration-security"></a>Segurança da integração CLR
  O modelo de segurança do [!INCLUDE[ssNoVersion](../../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR) gerencia e protege o acesso entre diferentes tipos de objetos CLR e não CLR em execução na [!INCLUDE[ssNoVersion](../../../includes/tsql-md.md)] instrução ou outro objeto CLR em execução no servidor. As chamadas entre objetos conhecidas como links. Os tipos de verificações de segurança realizados nesses objetos dependem dos tipos de links envolvidos.  
  
 O modelo de segurança de integração do CLR tem as seguintes metas:  
  
-   Por padrão, a execução de código de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]usuário gerenciado no. Realizar operações que podem comprometem a eficiência do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ser protegido por meio de permissões de alto nível apropriadas.  
  
-   O código de usuário gerenciado não deve ter acesso não autorizado a dados de usuário ou outro código de usuário no banco de dados. O código definido pelo usuário deve ser executado no contexto de segurança da sessão do usuário que o invocou e com os privilégios corretos para o contexto de segurança.  
  
-   Deve haver controles para impedir que o código do usuário acesse qualquer recurso fora do servidor, usando-o estritamente para acesso a dados locais e computação.  
  
-   O código definido pelo usuário não deve obter acesso não autorizado a recursos do sistema em virtude da execução no processo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]com o modelo de segurança baseado em acesso ao código do CLR. Algumas das vantagens dessa abordagem combinada em relação à segurança são abordadas nesta seção.  
  
 A tabela a seguir lista os tópicos desta seção.  
  
 [Segurança de acesso a código da integração CLR](clr-integration-code-access-security.md)  
 Discute o modelo CAS (segurança de acesso do código) para código gerenciado.  
  
 [Atributos de proteção de host e programação da Integração CLR](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)  
 Fornece informações sobre valores HPA (atributo de proteção do host) que são desaprovados nos assemblies SAFE e EXTERNAL_ACCESS.  
  
 [Links em segurança da integração CLR](../../../database-engine/dev-guide/links-in-clr-integration-security.md)  
 Descreve como partes do código do usuário podem se chamar uma à outra no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Representação e segurança de integração CLR](../../../database-engine/dev-guide/impersonation-and-clr-integration-security.md)  
 Aborda como o código gerenciado acessa recursos externos que usam representação.  
  
 [Permitindo chamadores parcialmente confiáveis](../../../database-engine/dev-guide/allowing-partially-trusted-callers.md)  
 Aborda problemas que surgem quando um método gerenciado invoca um método em uma classe contida em outro assembly.  
  
 [Domínios do aplicativo e segurança da integração CLR](../../../database-engine/dev-guide/application-domains-and-clr-integration-security.md)  
 Descreve como os assemblies são carregados em domínios de aplicativo.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciando assemblies de integração CLR](../assemblies/managing-clr-integration-assemblies.md)  
  
  
