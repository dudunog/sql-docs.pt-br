---
title: Definir um tamanho do arquivo máximo para um arquivo de rastreamento
titleSuffix: SQL Server Profiler
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: e86dc4ce-5aa3-4c0d-acb5-c9e8871ed963
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 74d0d90ed27da0cd66ccf4a14232731a9eeb8f7b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307909"
---
# <a name="set-a-maximum-file-size-for-a-trace-file-sql-server-profiler"></a>Definir um tamanho máximo para um arquivo de rastreamento (SQL Server Profiler)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use o procedimento a seguir para definir um tamanho máximo para um arquivo de rastreamento.  
  
### <a name="to-set-a-maximum-file-size-for-a-trace-file"></a>Para definir um tamanho máximo para um arquivo de rastreamento  
  
1.  No menu **Arquivo** , clique em **Novo Rastreamento**e conecte-se a uma instância do Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     A caixa de diálogo **Propriedades do Rastreamento**é exibida.  
  
    > [!NOTE]  
    >  Se **Iniciar rastreamento imediatamente após estabelecer a conexão**estiver selecionado, a caixa de diálogo **Propriedades do Rastreamento**não será exibida e o rastreamento será iniciado. Para desabilitar essa configuração, no menu **Ferramentas**, clique em **Opções**e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão** .  
  
2.  Na caixa **Nome do rastreamento** , digite um nome para o rastreamento.  
  
3.  Na lista **Nome do modelo**, selecione um modelo de rastreamento.  
  
4.  Selecione **Salvar em arquivo**e especifique um arquivo em que serão armazenadas as informações do rastreamento.  
  
5.  Na caixa de seleção **Definir tamanho máximo do arquivo** , especifique um tamanho do arquivo máximo para o rastreamento. Quando o tamanho de arquivo alcançar esse máximo, os eventos do rastreamento deixarão de ser registrados no arquivo. Se você selecionar **Habilitar substituição de arquivo** (que está selecionado por padrão), ocorrerá o seguinte:  
  
     A opção de substituição de arquivo faz com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] feche o arquivo atual e crie um novo arquivo quando o tamanho máximo é atingido. O novo arquivo recebe o mesmo nome do arquivo anterior, acrescido de um número inteiro indicando a sua sequência; por exemplo, se o arquivo de rastreamento original for denominado nomedoarquivo_1.trc, o arquivo seguinte será nomeado nomedoarquivo_2.trc, e assim por diante. Se o nome atribuído a um novo arquivo de substituição já estiver sendo usado por um arquivo existente, este último será substituído, exceto se for somente leitura. A opção de substituição de arquivo é habilitada por padrão quando você salva dados de rastreamento em um arquivo.  
  
     Com a opção de substituição de arquivo ativada, o rastreamento continua até que seja interrompido de alguma outra maneira. Para interromper o rastreamento quando o limite de tamanho de arquivo for atingido, desabilite a opção de substituição de arquivo.  
  
    > [!NOTE]  
    >  O sistema de arquivos FAT32 limita arquivos a um pouco menos de 4 gigabytes (GB). Quando o arquivo de rastreamento atinge esse tamanho, o rastreamento falha com o erro "Espaço em disco insuficiente". Para criar arquivos maiores, use o sistema de arquivos NTFS.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
