---
title: Publicar e republicar partes do relatório (Construtor de Relatórios) | Microsoft Docs
description: Saiba como publicar uma parte de relatório com metadados editados com configurações padrão em uma localização padrão no Construtor de Relatórios.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 92dce484-f39b-403c-9caf-d8772bc3aca3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f8848fb3d8d474083e0ce1a10b7d355a2e4b886e
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87928627"
---
# <a name="publish-and-republish-report-parts-report-builder-and-ssrs"></a>Publicar e republicar partes de relatório (Construtor de Relatórios e SSRS)
  Partes de relatório são itens de relatório paginados que foram publicados separadamente em um servidor de relatório e que podem ser reutilizados em outros relatórios paginados. Você pode publicar uma parte de relatório com configurações padrão em um local padrão ou pode editar os metadados de parte do relatório, como nome e descrição e salvá-lo em outro lugar no servidor de relatório. Também será possível salvá-lo em um site do SharePoint integrado com um servidor de relatório se você tiver as permissões corretas.  
  
 Você pode publicar apenas a parte de relatório, com o conjunto de dados do qual ela depende ou está inserida, ou pode publicar o conjunto de dados separadamente. Se você publicar o conjunto de dados separadamente, ele se tornará um conjunto de dados compartilhado e a parte de relatório será vinculada a ele. Para obter mais informações, consulte [Partes de relatório e conjuntos de dados no Construtor de Relatórios](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md).  
  
 Você pode publicar novamente uma parte de relatório existente. Se tiver permissões, você poderá salvar sobre a instância original da parte de relatório no servidor, mesmo que não a tenha criado. Também é possível publicá-la como uma nova parte de relatório e salvá-la no mesmo ou em outro local.  
  
## <a name="to-publish-a-report-part"></a>Para publicar uma parte de relatório  
  
1.  No menu Construtor de Relatórios, clique em **Publicar Partes de Relatório**.  
  
     Se você não estiver conectado a um servidor de relatório, receberá uma solicitação para se conectar. Se você não puder se conectar a um servidor de relatório, não poderá publicar partes de relatório.  
  
2.  Para salvar suas partes de relatório com configurações padrão para o local padrão, clique em **Publicar todas as partes de relatório com configurações padrão**.  
  
     Caso contrário, clique em **Examine e modifique as partes de relatório antes da publicação**.  
  
3.  Edite o nome e a descrição da parte do relatório: clique duas vezes no nome para editá-lo e clique no campo **Descrição** para adicionar uma descrição.  
  
    > [!NOTE]  
    >  É conveniente dar à parte de relatório nome e descrição claros, para facilitar a identificação durante a pesquisa. O comprimento máximo para o nome de uma parte de relatório é 260 caracteres para o caminho inteiro, inclusive os nomes das pastas no servidor, seguido pelo nome real da parte de relatório.  
  
4.  Para salvar sua parte de relatório em outra pasta que não a padrão, clique no botão **Procurar** .  
  
5.  Depois de definir as opções para todas as partes de relatório no relatório, clique em **Publicar**.  
  
     Depois que você publicar as partes de relatório, a caixa de diálogo mostrará as que foram publicadas com êxito e as que não foram. Você pode exibir detalhes na caixa de diálogo **Publicar Partes de Relatório** para as partes de relatório que não foram publicadas.  
  
6.  Clique em **fechar**  
  
## <a name="to-republish-a-report-part"></a>Para publicar uma parte de relatório novamente  
  
1.  Siga o procedimento anterior para publicar uma parte de relatório.  
  
2.  Na caixa de diálogo **Publicar Partes de Relatório** , se você clicar em **Publicar como uma Nova Cópia da Parte de Relatório**, o Construtor de Relatórios não salvará sobre a parte de relatório existente no servidor, mas criará outra parte de relatório.  
  
> [!NOTE]  
>  Se você publicá-la como uma nova parte de relatório, ela terá uma nova ID exclusiva. Ela não receberá mais atualizações se a parte de relatório original for alterada.  
  
## <a name="see-also"></a>Consulte Também  
 [Partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md)   
 [Partes de relatório e conjuntos de dados no Construtor de Relatórios](../../reporting-services/report-data/report-parts-and-datasets-in-report-builder.md)   
 [Procurar partes de relatório e definir uma pasta padrão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/browse-for-report-parts-and-set-a-default-folder-report-builder-and-ssrs.md)  
  
  
