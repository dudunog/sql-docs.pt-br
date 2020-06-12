---
title: Configuração de erro (caixa de diálogo estrutura de mineração) (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.miningstructuredialog.general.f1
ms.assetid: d9aa028b-bad9-49c7-a81c-c2150e4dd481
author: minewiskan
ms.author: owend
ms.openlocfilehash: ef6ba1926d23990399be8571ed117b87dd2edb8b
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528379"
---
# <a name="error-configuration-mining-structure-dialog-box-analysis-services---multidimensional-data"></a>Configuração de Erros (Caixa de diálogo Estrutura de Mineração) (Analysis Services – Dados Multidimensionais)
  Utilize a página **Configuração de Erros** da caixa de diálogo **Propriedades da Estrutura de Mineração** no **SQL Server Management Studio** para definir as propriedades de configuração de erros de uma estrutura de mineração em um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
## <a name="options"></a>Opções  
 **Usar configuração de erro padrão**  
 Selecione para usar a configuração de erro padrão para objetos na operação de processamento.  
  
 **Ação de erro de chave**  
 Escolha uma das seguintes ações que ocorrem quando uma nova chave é encontrada durante processamento que não pode ser pesquisado:  
  
-   **Converter em desconhecido** agrega as informações do registro ao membro desconhecido.  
  
-   **Descartar registro** exclui a informações do registro para que não sejam processadas com o objeto.  
  
 **Ignorar contagem de erros**  
 Clique para ignorar quaisquer erros ocorridos durante o processamento.  
  
 **Parar se houver erro**  
 Clique para interromper o processamento quando ocorrerem erros. Essa opção habilita as opções **Número de erros** e **Ação se houver erro** .  
  
 **Número de erros**  
 Digite o número de erros que são ignorados antes do processamento ser encerrado.  
  
 **Ação se houver erro**  
 Escolha uma das seguintes ações a serem executadas quando o número de erros exceder o valor em **Número de erros**:  
  
-   **Parar processamento** encerra a operação de processamento.  
  
-   **Parar log** para o log de erros, mas continua a operação de processamento.  
  
 **Chave não encontrada**  
 Especifique uma das seguintes ações a ser executada quando uma chave não for localizada quando um objeto for processado:  
  
-   **Ignorar erro** ignora o erro  
  
-   **Relatar e continuar** relata o erro e continua a operação de processamento.  
  
-   **Relatar e parar** relata o erro e para a operação de processamento.  
  
 **Chave duplicada**  
 Especifique uma das seguintes ações a ser executada se uma chave duplicada for localizada quando um objeto for processado:  
  
-   **Ignorar erro** ignora o erro  
  
-   **Relatar e continuar** relata o erro e continua a operação de processamento.  
  
-   **Relatar e parar** relata o erro e para a operação de processamento.  
  
 **Chave nula convertida em desconhecida**  
 Especifique uma das seguintes ações a ser executada quando uma chave de membro nula for adicionada ao membro desconhecido durante o processamento de um objeto.  
  
-   **Ignorar erro** ignora o erro  
  
-   **Relatar e continuar** relata o erro e continua a operação de processamento.  
  
-   **Relatar e parar** relata o erro e para a operação de processamento.  
  
 **Chave nula não permitida**  
 Especifique uma das seguintes ações a ser executada quando uma chave nula for localizada, mas não for permitida, quando um objeto for processado.  
  
-   **Ignorar erro** ignora o erro  
  
-   **Relatar e continuar** relata o erro e continua a operação de processamento.  
  
-   **Relatar e parar** relata o erro e para a operação de processamento.  
  
 **Caminho do log de erros**  
 Digite o caminho completo e nome do arquivo de log de erros.  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo Propriedades da estrutura de mineração &#40;Analysis Services-Mineração de dados&#41;](mining-structure-properties-dialog-analysis-services-data-mining.md)   
 [Caixa de diálogo &#40;geral de estrutura de mineração&#41; &#40;Analysis Services-Mineração de dados&#41;](general-mining-structure-dialog-box-analysis-services-data-mining.md)  
  
  
