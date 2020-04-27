---
title: Depurando procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- debugging stored procedures [Analysis Services]
- stored procedures [Analysis Services], debugging
ms.assetid: 34f51b85-02b3-40dd-bf93-375a9e522385
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 90b72b0e60550b0b6bdf89e0ba39e6089c5d8de2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62727742"
---
# <a name="debugging-stored-procedures"></a>Depurando procedimentos armazenados
  Os procedimentos armazenados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são, na verdade, bibliotecas CLR ou COM (normalmente DLLs) escritas em C# (ou em outra linguagem CLR ou COM). Portanto, depurar um procedimento armazenado é bem parecido com depurar outro aplicativo no ambiente de depuração do Visual Studio. Você depura procedimentos armazenados no ambiente de desenvolvimento do Visual Studio usando funções de depuração integradas. Elas permitem que você pare nas localizações do procedimento, verifique a memória e os valores do Registro, altere variáveis, observe o tráfego de mensagens e analise como o código funciona.  
  
### <a name="to-debug-a-stored-procedure"></a>Depurar um procedimento armazenado  
  
1.  Abra o projeto usado para criar a DLL no Visual Studio.  
  
2.  Crie pontos de interrupção no método ou na função correspondente ao procedimento que você deseja depurar.  
  
3.  Use o Visual Studio para criar uma compilação para depuração de uma DLL de procedimentos armazenados.  
  
4.  Implante a DLL no servidor. Para obter mais informações sobre como implantar a DLL no servidor, consulte [criando procedimentos armazenados](creating-stored-procedures.md).  
  
5.  Você precisa de um aplicativo que chame o procedimento armazenado que deseja testar. Se ainda não houver um aplicativo pronto, use o Editor de Consultas MDX do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar uma consulta MDX para chamar o procedimento armazenado que será testado.  
  
6.  No Visual Studio, anexe ao processo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (Msmdsrv.exe).  
  
    1.  No menu **depurar** , escolha **attatch toprocess**.  
  
    2.  Na caixa de diálogo **attatch toprocess** , selecione **Mostrar processos de todos os usuários**.  
  
    3.  Na lista **processos disponíveis** , na coluna **processo** , clique em **msmdsrv. exe**. Se houver mais que uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em execução no servidor, será necessário identificar o processo pelo ID da instância que você deseja usar.  
  
    4.  Na caixa de texto **anexar a** , verifique se o tipo de programa apropriado está selecionado. Para uma DLL CLR, clique em **selecionar**, clique em **depurar esses tipos de código**, clique em **gerenciado**e em **OK**. Para uma DLL COM, clique em **selecionar**, clique em **depurar esses tipos de código**, clique em **nativo**e, em seguida, clique em **OK**.  
  
    5.  Clique em **Anexar**.  
  
7.  No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], acione o programa ou script MDX que chama o procedimento armazenado. O depurador será interrompido quando chegar a uma linha que contém um ponto de interrupção. Você pode avaliar variáveis na janela de informação, exibir os locais e navegar pelo código.  
  
 Se houver problemas ao depurar uma biblioteca, certifique-se de que o arquivo do banco de dados do programa correspondente (arquivo PDB) foi copiado para o local de implantação no servidor. Se esse arquivo não foi copiado durante o registro ou a implantação, copie-o manualmente no mesmo local onde está a DLL. No caso de código nativo (DLL COM), o arquivo PDB reside no subdiretório \debug. Para código gerenciado (DLL CLR), reside no subdiretório \WINDEBUG.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento de assemblies de modelo multidimensional](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definindo procedimentos armazenados](defining-stored-procedures.md)  
  
  
