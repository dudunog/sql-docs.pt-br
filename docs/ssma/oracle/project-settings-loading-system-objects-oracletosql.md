---
title: Configurações do projeto (carregando objetos do sistema) (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9418cb34-d869-4d24-95b3-6cb9db949bb0
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: a5e8feb6c083c787d877cbc5491c533b8a35d740
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68266607"
---
# <a name="project-settingsloading-system-objects-oracletosql"></a>Configurações do projeto (carregar objetos de sistema) (OracleToSQL)
A página carregando objetos do sistema da caixa de diálogo **configurações do projeto** permite especificar quais objetos do sistema Oracle o SSMA converte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e carrega.  
  
O painel carregando objetos do sistema está disponível nas caixas de diálogo **configurações do projeto** e **configurações padrão do projeto** :  
  
-   Para especificar as configurações para todos os projetos do SSMA, no menu **ferramentas** , selecione **configurações de projeto padrão**, selecione tipo de projeto de migração para o qual as configurações devem ser exibidas ou alteradas na lista suspensa **versão de destino de migração** clique em **geral** na parte inferior do painel esquerdo e clique em **carregar objetos do sistema**.  
  
-   Para especificar as configurações do projeto atual, no menu **ferramentas** , selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique em **carregar objetos do sistema**.  
  
## <a name="default-settings"></a>Configurações padrão  
A conversão de objetos do sistema consome recursos do sistema e leva tempo. Para melhorar o desempenho, o SSMA seleciona apenas os objetos do sistema usados com mais frequência, conforme mostrado na lista a seguir:  
  
-   Sistema. DBMS_OUTPUT  
  
-   Sistema. DBMS_PIPE  
  
-   Sistema. DBMS_UTILITY  
  
-   Sistema. STANDARDIZATION  
  
-   Sistema. UTL_FILE  
  
-   Sistema. DBMS_LOB  
  
-   Sistema. DBMS_SQL  
  
-   Sistema. DBMS_SESSION  
  
Se os objetos do Oracle fizerem referência a outros objetos do sistema, você deverá selecionar esses objetos. Se você não selecionar os objetos do sistema que são referenciados por seus objetos de banco de dados Oracle, o SSMA relatará erros de conversão. Se você receber erros de conversão causados por objetos do sistema ausentes, selecione os objetos ausentes nessa caixa de diálogo. Em seguida, você pode repetir a conversão conforme necessário.  
  
