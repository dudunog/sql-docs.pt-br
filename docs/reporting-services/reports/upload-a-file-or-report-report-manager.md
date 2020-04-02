---
title: Carregar um arquivo ou relatório no Servidor de Relatório | Microsoft Docs
description: Saiba como adicionar relatórios e outros arquivos a um servidor de relatório sem precisar publicar esses itens de um aplicativo cliente.
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- publishing reports [Reporting Services], uploading files
- reports [Reporting Services], publishing
- uploading reports [Reporting Services]
- uploading files [Reporting Services]
- files [Reporting Services], uploading
ms.assetid: 79027e11-f4ba-4bfd-bd8c-d334e3da02a1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6d5d70a2147ea5cb9846ed37ea8963cc8c3f98e3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79510047"
---
# <a name="upload-a-file-or-report-in-the-report-server"></a>Carregar um arquivo ou relatório no servidor de relatório
O portal da Web do servidor de relatório fornece um recurso de upload que permite adicionar relatórios e outros arquivos a um servidor de relatório sem ter que publicar esses itens de um aplicativo cliente. Os arquivos carregados a partir do sistema de arquivos são armazenados como itens no servidor de relatório. O tipo de arquivo carregado determina o modo de armazenamento:  
  
-   Os arquivos .rdl são armazenados como relatórios paginados.  
  
-   Todos os outros arquivos, incluindo os arquivos de fonte de dados compartilhada (.rds), são carregados como recursos. Os recursos não serão processados por um servidor de relatório, mas poderão ser exibidos no portal da Web se o servidor de relatório for compatível com o tipo MIME de arquivo.  
  
### <a name="to-upload-a-file-or-report"></a>Para carregar um arquivo ou relatório  
  
1.  No portal da web, clique em **Carregar**.  
  
4.  Navegue até o arquivo que você deseja carregar. Você pode carregar um arquivo de definição de relatório, uma imagem, um documento ou qualquer arquivo que deseje disponibilizar no servidor de relatório.  
  
5.  Digite um nome para o novo item. Um nome de item pode incluir espaços, mas não pode incluir os caracteres reservados: \; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|.  
  
6.  Se desejar substituir um item existente pelo novo item, selecione **Substituir item, se existir**.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também   
[Criar, modificar e excluir fontes de dados compartilhadas](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)
[Carregar arquivos para uma pasta](../../reporting-services/report-server/upload-files-to-a-folder.md)  
  
  
