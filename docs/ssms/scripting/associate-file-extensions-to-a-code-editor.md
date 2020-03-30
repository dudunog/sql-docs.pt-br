---
title: Associar extensões de arquivo a um Editor de Códigos
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- file extensions [SQL Server]
- associating file extensions [SQL Server]
- Query Editor [SQL Server Management Studio], associating file extensions
ms.assetid: 193630f4-93de-4950-8f36-68702531f925
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1e8b9084ff83c16c57241f737ccc40665ee2414b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75246456"
---
# <a name="associate-file-extensions-to-a-code-editor"></a>Associar extensões de arquivo a um Editor de Códigos

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Associar extensões de arquivo a um editor de código específico permite a você abrir um arquivo com o editor de código [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] apropriado quando você clicar duas vezes num arquivo em Windows Explorer. As extensões normalmente usadas pelo [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], como .sql e .mdx, são associadas durante a instalação. As novas extensões de arquivos também devem estar associadas a [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] no sistema de arquivos. Você pode usar este recurso para abrir arquivos criados com outros editores ou abrir arquivos que você renomeou, como backups de arquivos .sql que foram renomeados como .bak.  
  
 Há duas etapas no processo. Primeiro associe a extensão a [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]e então associe a extensão a um editor de código específico.  
  
### <a name="to-associate-a-new-file-extension-with-sql-server-management-studio"></a>Para associar uma nova extensão de arquivo ao SQL Server Management Studio  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, **Acessórios**e então clique em **Windows Explorer**.  
  
2.  No Windows Explorer, no menu **Ferramentas** , clique em **Opções de Pasta**.  
  
3.  Na caixa de diálogo **Opções de Pasta** , na guia **Tipos de Arquivo** , clique em **Novo**.  
  
4.  Na caixa de diálogo **Criar Nova Extensão** , na caixa **Extensão de Arquivo** , digite a nova extensão de arquivo que você deseja associar e então clique em **OK**. Não inicie a extensão com um ponto.  
  
5.  Na caixa **Tipos de arquivo registrados** , clique na sua extensão e clique em **Alterar**.  
  
6.  Na caixa de diálogo **Abrir Com**, clique em **SSMS – SQL Server Management Studio** e clique em **OK**.  
  
7.  Clique em **Fechar** para fechar a caixa de diálogo **Opções de Pasta** e feche o Windows Explorer.  
  
### <a name="to-associate-a-new-file-extension-with-a-code-editor-in-sql-server-management-studio"></a>Para associar uma nova extensão de arquivo a um editor de código em SQL Server Management Studio  
  
1.  Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no menu **Ferramentas** , clique em **Opções**.  
  
2.  Na caixa de diálogo **Opções** , clique em **Editor de Texto**e clique em **Extensão de Arquivo**.  
  
3.  Na caixa **Extensão** , digite sua nova extensão de arquivo.  
  
4.  Na caixa **Editor** , clique no editor de código que você deseja usar para abrir este tipo de arquivo, clique em **Adicionar**e então clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário de Ssms](../../tools/sql-server-management-studio/ssms-utility.md)  
  
  
