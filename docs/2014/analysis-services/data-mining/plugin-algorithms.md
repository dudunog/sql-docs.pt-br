---
title: Algoritmos de plug-in | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- third-party algorithms [Analysis Services]
- algorithms [data mining], creating
- plugin algorithms [Analysis Services]
ms.assetid: fe364ddc-576e-42fc-9ced-baa399992f92
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac6494a438f8ecd9c1fb48cc7c2a588cfab9bd9a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66083167"
---
# <a name="plugin-algorithms"></a>Algoritmos de plug-in
  Além dos algoritmos que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o fornece, há muitos outros algoritmos que você pode usar para Data Mining. Conforme o caso, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece um mecanismo de "plugin" para algoritmos que são criados por terceiros. Contanto que os algoritmos sigam determinados padrões, é possível usá-los com o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da mesma forma que os algoritmos da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Os algoritmos de plug-in têm todos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] os recursos dos algoritmos fornecidos pelo.  
  
 Para obter uma descrição completa das interfaces que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa para comunicar-se com algoritmos de plugin, consulte os exemplos para criar um algoritmo personalizado e um visualizador de modelo personalizado que estão publicados no site do [CodePlex](https://go.microsoft.com/fwlink/?LinkID=87843) .  
  
## <a name="algorithm-requirements"></a>Requisitos de algoritmo  
 Para conectar um algoritmo no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], é necessário implementar as seguintes interfaces COM:  
  
 `IDMAlgorithm`  
 Implementa um algoritmo que produz modelos e implementa as operações de previsão dos modelos resultantes.  
  
 `IDMAlgorithmNavigation`  
 Permite que navegadores acessem o conteúdo dos modelos.  
  
 `IDMPersist`  
 Habilita os modelos que o algoritmo treina para serem salvos e carregados pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 `IDMAlgorithmMetadata`  
 Descreve os recursos e parâmetros de entrada do algoritmo.  
  
 `IDMAlgorithmFactory`  
 Cria instâncias dos objetos que implementam a interface de algoritmo e fornece ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] acesso para a interface de metadados de algoritmo.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa essas interfaces COM para se comunicar com algoritmos de plugin. Embora os algoritmos de plugin que você usa devam oferecer suporte à especificação [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB for Data Mining, eles não oferecem suporte a todas as opções de mineração de dados na especificação. Você pode usar o conjunto de linhas do esquema [MINING_SERVICES](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset) para determinar os recursos de um algoritmo. Esse conjunto de linhas de esquema lista as opções de suporte à mineração de dados para cada provedor de algoritmo de plugin.  
  
 É necessário registrar os novos algoritmos antes de usá-los com o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para registrar um algoritmo, inclua as seguintes informações no arquivo .ini file da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual você deseja incluir os algoritmos:  
  
-   O nome do algoritmo  
  
-   PROGID (ele é opcional e será incluído apenas para algoritmos de plugin)  
  
-   Um sinalizador que indique se o algoritmo está habilitado ou não  
  
 O exemplo de código a seguir ilustra como registrar um novo algoritmo:  
  
 `<ConfigurationSettings>`  
  
 `...`  
  
 `<DataMining>`  
  
 `...`  
  
 `<Algorithms>`  
  
 `...`  
  
 `<Sample_Plugin_Algorithm>`  
  
 `<Enabled>1</Enabled>`  
  
 `<ProgID>Microsoft.DataMining.SamplePlugInAlgorithm.Factory</ProgID>`  
  
 `</Sample_PlugIn_Algorithm>`  
  
 `...`  
  
 `</Algorithms>`  
  
 `...`  
  
 `</DataMining>`  
  
 `...`  
  
 `</ConfigurationSettings>`  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Conjunto de linhas DMSCHEMA_MINING_SERVICES](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-services-rowset)  
  
  
