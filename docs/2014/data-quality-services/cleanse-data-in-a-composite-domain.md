---
title: Limpar dados em um domínio de composição | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7d1076e0-7710-469a-9107-e293e4bd80ac
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: df41f9ae623053a61691076f9c96247f7a41564f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938007"
---
# <a name="cleanse-data-in-a-composite-domain"></a>Limpar dados em um domínio composto
  Este tópico fornece informações sobre como limpar domínios compostos no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Um domínio composto consiste em dois ou mais domínios únicos, e é mapeado para um campo de dados que consiste em vários termos relacionados. Os domínios individuais em um domínio composto devem ter uma área comum de conhecimento. Para obter informações detalhadas sobre domínios compostos, consulte [Managing a Composite Domain](../../2014/data-quality-services/managing-a-composite-domain.md).  
  
##  <a name="mapping-a-composite-domain-to-the-source-data"></a><a name="Mapping"></a> Mapeando um domínio composto para os dados de origem  
 Há dois modos para mapear seus dados de origem para um domínio composto:  
  
-   Os dados de origem são um único campo (digamos Nome Completo), que é mapeado para um domínio composto.  
  
    -   Se o domínio composto for mapeado para um serviço de dados de referência, os dados de origem serão enviados como tal para o serviço de dados de referência para correção e análise.  
  
    -   Se o domínio composto não for mapeado para um serviço de dados de referência, a análise se baseará no método de análise definido no domínio composto. Para obter mais informações sobre como especificar um método de análise para domínios compostos, consulte [Create a Composite Domain](../../2014/data-quality-services/create-a-composite-domain.md)  
  
-   Os dados de origem consistem em vários campos (digamos Nome, Nome do Meio e Sobrenome) que são mapeados para domínios individuais em um domínio composto.  
  
 Para obter um exemplo de como mapear domínios compostos para dados de origem, consulte [anexar um domínio ou um domínio de composição aos dados de referência](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md).  
  
##  <a name="data-correction-using-definitive-cross-domain-rules"></a><a name="CDCorrection"></a> Correção de dados usando regras de domínio cruzado definitivas  
 As regras do domínio cruzado no domínio composto permitem que você crie regras que indicam a relação entre domínios individuais em um domínio composto. As regras do domínio cruzado são levadas em conta quando você executa a atividade de limpeza em seus dados de origem envolvendo domínios compostos. Além de informá-lo sobre a validade de uma regra de domínio cruzado, a regra de domínio cruzado *Then* , **Valor é igual a**, também corrige os dados durante a atividade de limpeza de dados.  
  
 Considere o seguinte exemplo: há um domínio composto, Product, com três domínios individuais: ProductName, CompanyName e ProductVersion. Crie a seguinte regra de domínio cruzado definitiva:  
  
 O valor de domínio IF 'CompanyName' contém *Microsoft* e o valor de domínio 'ProductName' equivale a *Office*, o valor 'ProductVersion' equivale a *2010*. O valor de domínio THEN 'ProductName' Valor equivale a *Microsoft Office 2010*.  
  
 Quando esta regra de domínio cruzado é executada, os dados de origem (ProductName) são corrigidos da seguinte forma após a atividade de limpeza:  
  
 **Dados de origem**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Office|Microsoft Inc.|2010|  
  
 **Dados de saída**  
  
|ProductName|CompanyName|ProductVersion|  
|-----------------|-----------------|--------------------|  
|Microsoft Office 2010|Microsoft Inc.|2010|  
  
 Quando você testa a regra de domínio cruzado *Then* definitiva, **Valor é igual a**, a caixa de diálogo **Testar Regra de Domínio Composto** contém uma nova coluna, **Corrigir para**, que exibe os dados corretos. Em um projeto de qualidade de dados de limpeza, essa regra de domínio cruzado definitiva altera os dados com 100% de confiança e a coluna **motivo** exibe a seguinte mensagem: corrigida pela regra ' *\<Cross-Domain Rule Name>* '. Para obter mais informações sobre regras de domínio cruzado, consulte [Create a Cross-Domain Rule](../../2014/data-quality-services/create-a-cross-domain-rule.md).  
  
> [!NOTE]  
>  A regra do domínio cruzado definitiva não funcionará para domínios compostos que estão anexados ao serviço de dados de referência.  
  
##  <a name="data-profiling-for-composite-domains"></a><a name="DataProfiling"></a> Criação de perfis de dados para domínios compostos  
 A criação de perfil do DQS fornece duas dimensões de qualidade de dados: *integridade* (até que ponto os dados estão presentes) e *exatidão* (até que ponto os dados podem ser empregados para o uso pretendido) durante a atividade de limpeza. A criação de perfil talvez não forneça estatísticas confiáveis de integridade para domínios compostos. Se você precisar de estatísticas de integridade, use domínios únicos, em vez de domínios compostos. Para utilizar domínios compostos, talvez você queira criar uma base de dados de conhecimento com domínios únicos para a criação de perfil, a fim de determinar a integridade e criar outro domínio com um domínio composto para a atividade de limpeza. Por exemplo, a criação de perfil pode mostrar 95% de integridade para registros de endereço usando um domínio composto, mas pode haver um nível muito mais alto de não integridade para uma das colunas, por exemplo, uma coluna de CEP. Neste exemplo, talvez você queira medir a integridade da coluna de CEP com um domínio único.  
  
 A criação de perfil provavelmente fornecerá estatísticas de exatidão confiáveis para domínios compostos, pois é possível medir a exatidão para várias colunas juntas. O valor desses dados está na agregação composta, de modo que talvez você queira medir a exatidão com um domínio composto.  
  
 Para obter informações detalhadas sobre a criação de perfil de dados durante a atividade de limpeza, consulte [Estatísticas do criador de perfil](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Profiler) em [Limpar dados usando o conhecimento &#40;interno&#41; do DQS](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
  
