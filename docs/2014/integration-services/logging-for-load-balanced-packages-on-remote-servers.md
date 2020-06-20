---
title: Registro em log para pacotes com balanceamento de carga em servidores remotos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], remote packages
ms.assetid: fd571567-b625-4f9a-8b7e-42c5c588b11b
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 5f0adbcc17ad629f585cd04f43f757612a120ba4
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84951236"
---
# <a name="logging-for-load-balanced-packages-on-remote-servers"></a>Log para carga de pacotes balanceados em servidores remotos
  É mais fácil para um administrador gerenciar os logs de todos os pacotes filho que estão sendo executados em vários servidores quando todos os pacotes filho usam o mesmo provedor de log e todos gravam no mesmo destino. Um modo para criar um arquivo de log comum para todos os pacotes filho é configurar os pacotes filho para registrar os seus eventos em um provedor de log SQL Server. Você pode configurar todos os pacotes para usarem o mesmo banco de dados, o mesmo servidor e a mesma instância do servidor.  
  
 Para exibir os arquivos de log, o administrador precisa apenas fazer logon em um único servidor para exibir os arquivos de log de todos os pacotes filho.  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como habilitar o log em um pacote, consulte [Habilitar log de pacote no SQL Server Data Tools](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Registro em Log do SSIS &#40;Integration Services&#41;](performance/integration-services-ssis-logging.md)  
  
  
