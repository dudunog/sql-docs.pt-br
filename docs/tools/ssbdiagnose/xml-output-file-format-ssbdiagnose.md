---
title: Formato de arquivo de saída XML
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose]
- ssbdiagnose
ms.assetid: 3ceb991b-6f15-4504-8828-de5adf448bc5
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 50d1c8467c3ec7d51325b1a2beaad8f9216f0dbc
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75254179"
---
# <a name="xml-output-file-format-ssbdiagnose"></a>Formato de arquivo de saída XML (ssbdiagnose)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O utilitário **ssbdiagnose** entrega sua saída como um arquivo XML quando você o executa com a opção **-XML** . O arquivo de saída XML lista informações de cabeçalho e erros encontrados na configuração ou conversa do [!INCLUDE[ssSB](../../includes/sssb-md.md)] analisadas. Você pode escrever um aplicativo para analisar ou reportar os erros listados no arquivo. Ou pode exibir o arquivo de XML em um editor de XML geral, como o Bloco de Notas XML.  
  
 Um arquivo de saída do **ssbdiangose** contém um elemento raiz DiagnosticInformation com dois tipos de filho:  
  
-   Um elemento Banner com informações de cabeçalho.  
  
-   Um elemento Issue para cada problema reportado por **ssbdiagnose**.  
  
## <a name="diagnosticinformation-root-element"></a>Elemento raiz DiagnosticInformation  
  
-   [Elemento DiagnosticInformation &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)  
  
## <a name="banner-element"></a>Elemento Banner  
  
-   [Elemento Banner &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)  
  
## <a name="issue-element"></a>Elemento Issue  
  
-   [Elemento Issue &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário ssbdiagnose &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
