---
title: Gerenciador de Conexões do Armazenamento do Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpstorageconn.f1
- sql11.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ea689f96911af35176d6467e73d496b59f35e3c9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62833554"
---
# <a name="azure-storage-connection-manager"></a>Gerenciador de conexões do Armazenamento do Azure
  O gerenciador de conexões do Armazenamento do Azure permite que um pacote SSIS se conecte a uma conta do Armazenamento do Azure usando os valores especificados para as propriedades: Nome da Conta de Armazenamento e Chave de Conta.  
  
1.  Na caixa de diálogo **Adicionar gerenciador de conexões do SSIS** , selecione **AzureStorage**e clique em **Adicionar**.  
  
2.  Na caixa de diálogo Editor do Gerenciador de Conexão do Armazenamento do Azure, escolha **Usar conta do Azure** para se conectar a um Serviço de Armazenamento do Azure por meio da Internet ou escolha **Usar conta de desenvolvedor local** para se conectar ao serviço local hospedado pelo Emulador de Armazenamento do Azure.  
  
3.  Se você tiver escolhido a opção **Usar conta do Azure** , faça o seguinte:  
  
    1.  Especifique valores para os campos **Nome da conta de armazenamento** e **Chave de conta** . Esses valores serão armazenados como dados confidenciais no pacote SSIS.  
  
    2.  Escolha **Usar HTTPS** se quiser usar HTTPS em vez de HTTP para se conectar ao Serviço de Armazenamento do Azure.  
  
4.  Clique em **OK** para fechar a caixa de diálogo.  
  
5.  Você pode ver as propriedades do gerenciador de conexões criado na janela **Propriedades** .  
  
  
