---
title: 'Etapa 4: Testar o pacote da Lição 5 | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cc02e55b0079ec10e8335168ce754c77dfdc3ad0
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918099"
---
# <a name="lesson-5-4-test-the-lesson-5-package"></a>Lição 5-4: Testar o pacote da Lição 5

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Em tempo de execução, seu pacote obtém o valor para a propriedade **Directory** de uma variável de configuração, em vez do nome do diretório especificado quando você criou o pacote. O valor da variável é proveniente do arquivo XML **SSISTutorial.dtsConfig**.  
  
Para verificar se o pacote atualiza a propriedade **Directory** com o novo valor durante o tempo de execução, execute o pacote. Como apenas três arquivos de dados de exemplo estão no novo diretório, o fluxo de dados é executado em apenas três vezes.  
  
## <a name="checking-the-package-layout"></a>Verificando o layout do pacote  
Antes de testar o pacote, verifique se os fluxos de controle e de dados do pacote da Lição 5 são similares aos objetos mostrados nos diagramas a seguir:  
  
**Fluxo de Controle**  
  
![Fluxo de controle no pacote](../integration-services/media/task4lesson2control.gif "Fluxo de controle no pacote")  
  
**Fluxo de Dados**  
  
![Fluxo de dados no pacote](../integration-services/media/task9lesson1data.gif "Fluxo de dados no pacote")  
  
## <a name="test-the-lesson-5-package"></a>Testar o pacote da Lição 5  
  
1.  No menu **Depurar**, selecione **Iniciar Depuração**.  
  
2.  Terminada a execução do pacote, no menu **Depurar**, selecione **Parar Depuração**.  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 6: Usar parâmetros com o modelo de implantação de projetos no SSIS](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
  
