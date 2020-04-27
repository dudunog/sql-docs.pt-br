---
title: Examinar e gerar scripts de log suplementares | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- scripts
ms.assetid: 5c858ae2-37d6-42e8-a252-7f6ed4e628a7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 68aa51facd21ec09be78e6ad0996131a9ee3cc5b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62835333"
---
# <a name="review-and-generate-supplemental-logging-scripts"></a>Revisar e gerar scripts de log suplementares
  Use a guia **Scripts** para executar ou executar novamente um script no banco de dados de origem Oracle que configura o registro em log suplementar.  
  
 Antes de executar os scripts, siga um destes procedimentos:  
  
 **Inclua alterações nesta sessão**  
 Selecione isto para executar o script em qualquer nova tabela que foi adicionada à instância CDC ou em tabelas que foram alteradas de alguma maneira usando o editor de Propriedades.  
  
> [!NOTE]  
>  Se nenhuma alteração foi feita às tabelas na instância CDC, a área de script suplementar de registro em log do Oracle estará vazia.  
  
 **Inclua todas as instâncias de tabelas/captura**  
 Selecione isto para executar o script em todas as tabelas e instâncias de captura na instância CDC.  
  
 Depois de selecionar uma destas opções, execute o script suplementar de registro em log.  
  
### <a name="to-run-the-supplemental-logging-scripts"></a>Para executar os scripts suplementares de registro em log  
  
1.  Clique em **Executar Script** para executar o script suplementar de registro em log nas tabelas definidas para a instância CDC. Este script instrui o banco de dados Oracle para gravar todas as colunas de interesse em seus logs de transação ao registrar em log operações UPDATE para tabelas capturadas. Este script é examinado e executado normalmente por um administrador do sistema Oracle.  
  
2.  Quando você executa os scripts de log suplementares, a caixa de diálogo Oracle Credentials for Running Script abre e você fornece um nome de usuário e senha do Oracle válidos. Para obter informações sobre como fornecer as credenciais corretas do Oracle, consulte [Oracle Credentials for Running Script](oracle-credentials-for-running-script.md).  
  
 Você também pode executar os scripts manualmente usando o SQL * Plus, se necessário.  
  
### <a name="to-run-the-scripts-manually"></a>Para executar os scripts manualmente  
  
1.  Clique em **Copiar** para colar o script na área de transferência. Abra o SQL * Plus e vá para o diretório com seu banco de dados de origem Oracle. Cole o script no SQL\*Plus para executar isto.  
  
### <a name="to-save-the-supplemental-logging-script-in-a-text-file"></a>Para salvar o script suplementar de registro em log em um arquivo de texto  
  
1.  Clique em **Salvar como** e navegue até o local em que você deseja salvar o arquivo.  
  
2.  Dê ao arquivo um nome e clique em **Salvar** para salvar o arquivo.  
  
## <a name="see-also"></a>Consulte Também  
 [Como editar as propriedades de instância CDC](how-to-edit-the-cdc-instance-properties.md)   
 [Credenciais Oracle para executar scripts](oracle-credentials-for-running-script.md)  
  
  
