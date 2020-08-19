---
description: Criar casos de teste (OracleToSQL)
title: Criando casos de teste (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Test Case Wizard
ms.assetid: 22f38901-ec35-4707-a911-784e6ad8dafb
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 4f7183089fd67f413515034a557e4b73388f950f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418382"
---
# <a name="creating-test-cases-oracletosql"></a>Criar casos de teste (OracleToSQL)
Use o assistente de caso de teste para criar um teste. Este assistente permite que você crie casos de teste escolhendo objetos testados e verificados e especificando os parâmetros de teste.  
  
## <a name="starting-the-test-case-wizard"></a>Iniciando o assistente de caso de teste  
Para iniciar o assistente de caso de teste, clique em **novo caso de teste...** no menu **testador** .  
  
Quando iniciado, o assistente procura SSMATESTER_ORACLE de esquema no servidor Oracle de origem. É o esquema de extensão do testador usado para armazenar objetos auxiliares. Se o assistente de caso de teste não conseguir localizar SSMATESTER_ORACLE, ele exibirá uma janela de diálogo que propõe criar o esquema. (Essa situação geralmente ocorre durante a primeira execução do SSMA Tester.)  
  
Se você receber a janela de diálogo, clique em **Sim** para criar SSMATESTER_ORACLE esquema no servidor de origem. Observe que você deve ter privilégios Oracle para criar um novo usuário e criar objetos no esquema deste usuário.  
  
## <a name="overview-of-creating-test-cases-using-the-wizard"></a>Visão geral da criação de casos de teste usando o assistente  
O processo de criação de um caso de teste consiste em cinco etapas:  
  
1.  [Inicializando casos de teste &#40;OracleToSQL&#41;](../../ssma/oracle/initializing-test-cases-oracletosql.md)  
  
2.  [Selecionando e configurando objetos para testar &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-objects-to-test-oracletosql.md)  
  
3.  [Selecionando e configurando objetos afetados &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
4.  [Personalizando a ordem das chamadas &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
5.  [Concluindo a preparação do caso de teste &#40;OracleToSQL&#41;](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Testando objetos de banco de dados migrados &#40;OracleToSQL&#41;](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
