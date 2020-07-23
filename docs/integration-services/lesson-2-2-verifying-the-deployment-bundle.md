---
title: 'Etapa 2: verificar o pacote de implantação | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 6c13f5c9-c75e-4e52-94dc-2d2db2c578fe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fec0b4e8180141fdea37e2ac484f5a2b0195b44a
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917228"
---
# <a name="lesson-2-2---verifying-the-deployment-bundle"></a>Lição 2-2 – verificar o pacote de implantação

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


Na lição 1, você criou o projeto do Tutorial de Implantação e adicionou pacotes e arquivos auxiliares ao projeto; na tarefa anterior você compilou um utilitário de implantação para o projeto.  
  
Nesta tarefa, você verificará o conteúdo do pacote de implantação. O pacote de implantação é a pasta que você copiará para o computador de destino e usará para instalar os pacotes. Se você tiver usado o valor padrão – bin\Deployment – como a localização do utilitário de implantação, o pacote de implantação será a pasta Bin\Deployment dentro da pasta Tutorial de Implantação no projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
### <a name="to-verify-the-content-of-deployment-bundle"></a>Para verificar o conteúdo do pacote de implantação  
  
1.  Localize a pasta bin\Deployment em seu computador.  
  
2.  Verifique se os seguintes arquivos estão presentes:  
  
    -   DataTransfer.dtsx  
  
    -   datatransferconfig.dtsconfig  
  
    -   Deployment Tutorial.SSISDeploymentManifest  
  
    -   LoadXMLData.dtsx  
  
    -   loadxmldataconfig.dtsconfig  
  
    -   NewCustomers.txt  
  
    -   orders.xml  
  
    -   orders.xsd  
  
    -   Readme.txt  
  
3.  Clique com o botão direito do mouse em Deployment Tutorial.SSISDeploymentManifest, aponte para **Abrir Com**e clique em **Internet Explorer**. Você também pode abrir o arquivo em um editor de textos como o Bloco de Notas. O código XML do arquivo deve ser o seguinte:  
  
    `<?xml version="1.0"?><DTSDeploymentManifest GeneratedBy="Domain\UserName" GeneratedFromProjectName="Deployment Tutorial" GeneratedDate="2006-02-24T13:29:02.6537669-08:00" AllowConfigurationChanges="true"><Package>DataTransfer.dtsx</Package><Package>LoadXMLData.dtsx</Package><ConfigurationFile>datatransferconfig.dtsconfig</ConfigurationFile><ConfigurationFile>loadxmldataconfig.dtsconfig</ConfigurationFile><MiscellaneousFile>Readme.txt</MiscellaneousFile><MiscellaneousFile>orders.xml</MiscellaneousFile><MiscellaneousFile>NewCustomers.txt</MiscellaneousFile><MiscellaneousFile>orders.xsd</MiscellaneousFile></DTSDeploymentManifest>`  
  
4.  Verifique se o valor do atributo **AllowConfigurationChanges** é **true** e se o XML inclui um elemento **Package** para cada um dos dois pacotes, um elemento **MiscellaneousFile** para cada um dos quatro arquivos que não são de pacote e um elemento **ConfigurationFile** para cada um dos dois arquivos de configuração XML.  
  
5.  Saia do Internet Explorer ou do editor de textos.  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 3: Instalar os pacotes SSIS](../integration-services/lesson-3-install-ssis-packages.md)  
  
  
  
