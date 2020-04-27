---
title: Selecionar opções de Gerenciamento de Pacotes (Assistente de atualização de pacotes SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectpackagemgtoptions.f1
ms.assetid: 810fc020-51cd-43ed-9f35-af99b4f35947
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c71f254b0d0fb79e3ee8135c10d2d9ed715d3437
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66056024"
---
# <a name="select-package-management-options-ssis-package-upgrade-wizard"></a>Selecionar Opções de Gerenciamento de Pacotes (Assistente de Atualização de Pacotes SSIS)
  Use a página **Selecionar Opções de Gerenciamento de Pacote** para especificar opções para atualizar pacotes.  
  
 **Para executar o Assistente de Atualização de Pacotes SSIS**  
  
-   [Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="options"></a>Opções  
 **Atualizar cadeias de conexão para usar novos nomes de provedor**  
 Atualize as cadeias de conexão para usar os nomes dos seguintes provedores da versão atual do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   Provedor OLE DB para [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 O Assistente de Atualização de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] só atualiza cadeias de conexão armazenadas em gerenciadores de conexões. O assistente não atualiza cadeias de conexão construídas dinamicamente com a linguagem de expressão do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ou o código de uma tarefa Script.  
  
 **Validar pacotes de atualização**  
 Valide os pacotes de atualização e salve só os pacotes aprovados na validação.  
  
 Se você não selecionar essa opção, o assistente não validará pacotes de atualização. Portanto, o assistente salvará todos os pacotes de atualização, independentemente de sua validez. O assistente salva os pacotes de atualização no destino especificado na página **Selecionar Local de Destino** do assistente.  
  
 A validação prolonga o processo de atualização. Recomendamos que você não selecione essa opção para pacotes grandes que provavelmente serão atualizados com êxito.  
  
 **Criar novas IDs de pacote**  
 Crie novas IDs para os pacotes de atualização.  
  
 **Continuar o processo de upgrade quando um upgrade de pacote falhar**  
 Especifique que o Assistente de Atualização de Pacotes [!INCLUDE[ssIS](../includes/ssis-md.md)] deve continuar atualizando os pacotes restantes quando não for possível atualizar um pacote.  
  
 **Conflitos de nome de pacote**  
 Especifique como o assistente deve manipular pacotes que têm o mesmo nome. Os valores dessa opção estão relacionados na tabela a seguir.  
  
 **Substituir arquivos de pacote existentes**  
 Substitui o pacote existente pelo pacote de atualização do mesmo nome.  
  
 **Adicionar sufixos numéricos para fazer upgrade de nomes de pacote**  
 Adiciona um sufixo numérico ao nome do pacote de atualização.  
  
 **Não fazer upgrade de pacotes**  
 Interrompe a atualização dos pacotes e exibe um erro quando o assistente é concluído.  
  
 Essas opções não estão disponíveis quando a opção **Salvar no local de origem** é selecionada na página **Selecionar Local de Destino** do assistente.  
  
 **Ignorar configurações**  
 Não carrega configurações de pacotes durante a atualização de pacotes. A seleção dessa opção reduz o tempo necessário para atualizar o pacote.  
  
 **Fazer backup dos pacotes originais**  
 Configure o assistente para fazer backup dos pacotes originais em uma pasta **SSISBackupFolder** . O assistente cria a pasta **SSISBackupFolder** como uma subpasta da pasta que contém os pacotes originais e os pacotes atualizados.  
  
> [!NOTE]  
>  Essa opção só está disponível quando você especifica que os pacotes originais e os pacotes atualizados estão armazenados no sistema de arquivos e na mesma pasta.  
  
 Para obter mais informações, consulte [Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Atualizar pacotes do Integration Services](install-windows/upgrade-integration-services-packages.md)  
  
  
