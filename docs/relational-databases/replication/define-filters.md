---
title: Definir filtros | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.replconflictviewer.definefilters.f1
helpviewer_keywords:
- Define Filters dialog box
ms.assetid: 1fa71d22-ce5a-4aae-ba05-4d755842aeac
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1837e3b57548ec0d4324a408f8f43201ccc3ca6b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68768167"
---
# <a name="define-filters"></a>Definir Filtros
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  A caixa de diálogo **Definir Filtros** permite que você defina filtros que são aplicados em conflitos de dados para consultar um subconjunto dos conflitos na grade. Para definir um filtro, escolha um operador na caixa de listagem suspensa **Operador** e então insira em um valor. Por exemplo, para mostrar somente conflitos onde o perdedor do conflito é o servidor **ReplTest1**, selecione **Igual a** na caixa de lista suspensa **Operador** e insira **ReplTest1** na primeira coluna **Valor** .  
  
## <a name="options"></a>Opções  
 **Operador**  
 Selecione um operador para o filtro, como **Menor que ou Igual a**.
  
 **Valor**  
 Insira um valor para o filtro. A maioria dos operadores só exige um valor na primeira coluna **Valor** , mas os operadores **Entre** e **Não Entre** requerem um valor em ambas as coluna **Valor** .  
  
 **Limpar**  
 Clique nesse botão para limpar todos os filtros anteriormente definidos.  
  
## <a name="see-also"></a>Consulte Também  
 [Visualizador de Conflitos de Replicação da Microsoft &#40;replicação de mesclagem&#41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-merge-replication.md)   
 [Visualizador de Conflitos de Replicação da Microsoft &#40;replicação transacional&#41;](../../relational-databases/replication/microsoft-replication-conflict-viewer-transactional-replication.md)  
  
  
