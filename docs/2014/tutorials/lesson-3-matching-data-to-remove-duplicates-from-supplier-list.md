---
title: 'Lição 3: dados correspondentes para remover duplicatas da lista de fornecedores | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 059170b6-d62e-4b28-9451-99a0cc7e1f5f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: c59a2fce106b08f53722ce44ae69225b680d7925
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65484648"
---
# <a name="lesson-3-matching-data-to-remove-duplicates-from-supplier-list"></a>Lição 3: Correspondendo dados para remover duplicatas da lista de fornecedores
  Você prepara a base de dados de conhecimento para executar uma atividade de correspondência criando uma política de correspondência na base de dados de conhecimento. Pode haver apenas uma política de correspondência em uma base de dados de conhecimento. Uma política de correspondência consiste em uma ou mais regras de correspondência. Uma regra identifica os domínios envolvidos no processo de correspondência e especifica o peso que cada valor de domínio tem na avaliação de correspondência. Você especifica na regra se os valores do domínio precisam ser uma correspondência exata ou se podem ser semelhantes, e com que grau de semelhança. Você também especifica se a correspondência de domínio é um pré-requisito para o processo de correspondência. Você pode testar cada regra separadamente e testar toda a política em relação aos dados de exemplo. O processo de teste exibe registros cujas pontuações de correspondência são maiores que o limite **mínimo de Pontuação de registro** especificado na configuração do DQS em um cluster (grupo). Você poderá continuar ajustando as regras na política até ficar satisfeito.  
  
 Depois de definir a política, crie um Projeto de Qualidade de Dados para executar a atividade de correspondência. O projeto de correspondência aplica as regras de correspondência da política de correspondência à fonte de dados a ser avaliada. Esse processo avalia a probabilidade de quaisquer duas linhas serem correspondências. Quando o DQS executa a análise de correspondência, cria clusters de registros considerados como correspondências pelo DQS. O DQS identifica aleatoriamente um dos registros como um registro dinâmico. Você pode verificar e rejeitar qualquer registro que não seja uma correspondência apropriada para o cluster. Consulte [o tópico criar uma política de correspondência](https://msdn.microsoft.com/library/hh270290.aspx) para obter mais detalhes.  
  
 Nesta lição, você realizará uma atividade de correspondência para remover duplicatas na lista de fornecedores. Primeiro, crie uma política de correspondência com uma regra para identificar duplicatas na lista de fornecedores e publicar a política para a base de dados de conhecimento. Em seguida, crie e execute um projeto de qualidade de dados para correspondência. Finalmente, exporte os resultados da atividade de correspondência para um arquivo do Excel que você usará posteriormente no carregamento de dados para o MDS (Master Data Services).  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 1: Definindo uma política de correspondência](../../2014/tutorials/task-1-defining-a-matching-policy.md)  
  
  
