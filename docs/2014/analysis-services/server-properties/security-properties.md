---
title: Propriedades de segurança | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- security [Analysis Services], properties
- SecurityPackageList property
- BuiltinAdminsAreServerAdmins property
- DisableClientImpersonation property
- ErrorMessageMode property
- RequiredProtectionLevel property
- ServiceAccountIsServerAdmin property
- RequireClientAuthentication property
ms.assetid: 2fc7fe10-0cbb-49ac-aa8c-8ec3f7a7705f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9316827245adfbcf64bd798869f570dc5f0af14c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66068904"
---
# <a name="security-properties"></a>Propriedades de segurança
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades do servidor de segurança listadas na tabela a seguir. Para obter mais informações sobre as propriedades de servidor adicionais e como defini-las, consulte [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md).  
  
 **Aplica-se a:** modo de servidor multidimensional e tabular  
  
## <a name="properties"></a>Propriedades  
 `RequireClientAuthentication`  
 Uma propriedade booliana que indica se autenticação de cliente é necessária.  
  
 O valor padrão para essa propriedade é True, o que indica que autenticação de cliente é necessária.  
  
 `SecurityPackageList`  
 Uma propriedade de cadeia de caracteres que contém uma lista separada por vírgulas de pacotes SSPI usada pelo servidor para autenticação de cliente.  
  
 `DisableClientImpersonation`  
 Uma propriedade booliana que indica se a representação do cliente (por exemplo, de procedimentos armazenados) está desabilitada.  
  
 O valor padrão dessa propriedade é False, o que indica que representação do cliente está habilitada.  
  
 `BuiltinAdminsAreServerAdmins`  
 Uma propriedade booliana que indica se membros do grupo de administradores de máquina local são administradores do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 `ServiceAccountIsServerAdmin`  
 Uma propriedade booliana que indica se a conta de serviço é um administrador do servidor.  
  
 O valor padrão dessa propriedade é True, o que indica que a conta de serviço é um administrador do servidor.  
  
 `ErrorMessageMode`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 `DataProtection\ RequiredProtectionLevel`  
 Uma propriedade de inteiro de 32 bits assinada que define o nível de proteção exigido para todas as requisições do cliente. Essa propriedade tem um dos valores listados na tabela a seguir:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|*0*|Nenhum, texto não criptografado permitido.|  
|*1*|(Padrão) Criptografia necessária, sem log de texto não criptografado.|  
|*2*|Solicitações de textos não criptografados são permitidas, mas apenas com assinaturas (proteção mais baixa do que criptografia).|  
  
 `AdministrativeDataProtection\ RequiredProtectionLevel`  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar propriedades do servidor no Analysis Services](server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
