---
title: Gerenciando partes de relatório | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 41947b4c-8ecf-4e4f-b30e-66e1d6692b74
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2de2ed783db4f717b86e94424b994f78d4eb75d6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105585"
---
# <a name="managing-report-parts"></a>Gerenciando partes de relatório
  [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]A partir do, as partes de relatório podem ser publicadas em servidores de relatório e reutilizadas em outros relatórios e por outros usuários se tiverem as permissões apropriadas.  
  
 Partes de relatório podem ser reutilizadas por vários usuários e em vários relatórios. Os usuários podem pesquisar partes de relatório no servidor e adicioná-las a um relatório.  Também podem ser informados de atualizações para a parte de relatório no servidor e republicar novas versões de uma parte de relatório. Essas ações de criação de relatório podem ser afetadas e controladas pelas permissões de segurança dos serviços de relatório.  Este tópico revisa as propriedades de parte de relatório e o comportamento depois que elas estão no servidor.  
  
## <a name="managing-report-parts"></a>Gerenciando partes de relatório  
 Para gerenciar partes de relatório, você pode usar Report Manager para um servidor de relatório no modo nativo ou páginas de aplicativo para um servidor de relatório no modo integrado do SharePoint.  
  
### <a name="server-side-interaction-and-search"></a>Interação e pesquisa do servidor  
 Partes de relatório podem ser publicadas em um servidor de relatório em modo nativo ou em modo integrado do SharePoint. Os usuários podem usar o recurso Galeria de partes de relatório em um aplicativo de criação [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de relatório, como Construtor de relatórios para localizar e adicionar partes de relatório a seus relatórios. Quando um usuário pesquisa uma parte de relatório, a pesquisa olha para o catálogo de servidor de relatório independentemente do modo no qual o servidor foi instalado.  
  
 Quando as partes de relatório são publicadas de um aplicativo de criação de relatório, como o Construtor de Relatórios em um servidor de relatório em modo integrado do SharePoint, o catálogo de servidor de relatório também é atualizado e as pesquisas da galeria refletem com precisão a parte de relatório nova ou atualizada.  
  
#### <a name="directly-uploading-report-parts-to-a-sharepoint-folder"></a>Carregando partes de relatório diretamente para uma pasta do SharePoint  
 Se uma parte de relatório for carregada diretamente em uma pasta de documentos do SharePoint, em vez de publicada de um aplicativo de criação de relatório, o catálogo do servidor de relatório também não será atualizado. As pesquisas da galeria de partes de relatório não localizarão a parte de relatório carregada. Para ajudar a manter suas pastas do SharePoint e o catálogo do servidor de relatório sincronizados, você pode ativar o recurso de sincronização de arquivos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no servidor do SharePoint. Para obter mais informações, consulte [ativar o recurso de sincronização de arquivos do servidor de relatório na administração central do SharePoint](../activate-report-server-file-sync-feature-sharepoint-central-administration.md).  
  
 Os arquivos também podem ser sincronizados usando a chamada de algumas das APIs de gerenciamento de serviços de relatório, como GetProperties e SetProperties.  
  
### <a name="organizing-and-moving-report-parts"></a>Organizando e movendo partes de relatório  
 Planeje com antecedência a maneira como sua equipe usará e organizará partes de relatório, conjuntos de dados compartilhados e fontes de dados compartilhadas. Embora eles possam ser movidos no futuro, poderá haver problemas.  
  
#### <a name="native-mode-report-server"></a>Servidor de relatório em modo nativo  
 Se você mover uma parte de relatório em um servidor de relatório em modo nativo para qualquer outra pasta no mesmo servidor, a capacidade de aplicativos de criação para pesquisar ou baixar atualizações da parte de relatório não será afetada. Isto acontece porque o servidor depende do ComponentID exclusivo. No entanto, se a parte de relatório for movida para uma pasta para a qual um usuário não tenha permissões, suas pesquisas não localizarão a parte de relatório e seus relatórios não serão notificados quando houver atualizações na parte de relatório.  
  
#### <a name="report-server-in-sharepoint-integrated-mode"></a>Servidor de relatório em modo integrado do SharePoint  
 A movimentação de partes de relatório para uma biblioteca ou pasta de documentos diferente tem o mesmo efeito que carregá-las diretamente em um servidor do SharePoint: o catálogo do servidor de relatório não será sincronizado. Para evitar isso, ative o recurso Sincronização de arquivos do Servidor de Relatório no servidor do SharePoint.  
  
 Subpastas são uma exceção. A pesquisa sempre pesquisará subpastas, portanto, se você mover manualmente uma parte de relatório para uma subpasta, ela ainda será localizada em uma pesquisa na galeria de relatórios. ela ainda será localizada em uma pesquisa na galeria de partes de relatório.  
  
### <a name="report-server-catalog-properties"></a>Propriedades do catálogo do servidor de relatório  
 A tabela a seguir descreve como os campos do catálogo do servidor de relatório existentes se relacionam com uma parte de relatório, e com novos campos adicionados ao catálogo de partes de relatório. Esses são expostos no gerenciador de relatórios, em bibliotecas do SharePoint e em aplicativos de criação de relatório, como o Construtor de Relatórios.  
  
 (*) indica que isso é novo para esta versão.  
  
|Propriedade|Descrição|Parte de relatório<br /><br /> Critérios de pesquisa de galeria|  
|--------------|-----------------|---------------------------------------------|  
|Nome|Esse é um dos critérios pelos quais um usuário pode pesquisar na Galeria de Partes de Relatório.|Sim|  
|Descrição|Você deve organizar os nomes de partes de relatório de uma maneira que facilite para os usuários a localização na galeria. Por exemplo, você pode pesquisar pela descrição iniciando com "Vendas>>" para procurar as partes de relatório que envolvem dados e apresentações relacionadas a vendas.|Sim|  
|CreatedBy|A ID do usuário que adicionou originalmente a parte de relatório ao banco de dados do servidor de relatório. O formato exato depende do método de autenticação. Por exemplo, alguns métodos de autenticação mostrarão o domínio\nome de usuário completo nos campos CreatedBy e ModifiedBy.|Sim|  
|CreationDate|As data em que a parte de relatório foi criada originalmente.<br /><br /> Esse é um dos critérios pelos quais um usuário pode pesquisar na Galeria de Partes de Relatório.|Sim|  
|ModifiedBy|ModifiedBy é a ID do usuário que modificou por último a parte do relatório.|Sim|  
|ModifiedDate|A data em que a parte de relatório foi modificada pela última vez no servidor.<br /><br /> Esse campo é usado como parte da lógica para determinar quando há atualizações do servidor em uma parte de relatório. Para obter mais informações, consulte a descrição de ComponentID mais à frente nessa tabela.|Sim|  
|SubType (*)|Subtipo é uma cadeia de caracteres que indica o tipo de parte de relatório para pesquisar, como "Tablix" ou "Gráfico."|Sim|  
|ComponentID (*)|ComponentID é um identificador exclusivo da parte de relatório. Esse é um novo campo adicionado ao catálogo e é visível no servidor e nos aplicativos de criação de relatório, como o Construtor de Relatórios.<br /><br /> Esse campo é usado por aplicativos cliente ao verificar atualizações de uma parte de relatório no servidor. O aplicativo cliente pesquisa o servidor em busca de ComponentIDs que estão no relatório atual do lado do cliente. Quando houver uma correspondência de ComponentID, o ModifiedDate será comparado ao SyncDate do item de relatório do lado do cliente.|N0|  
  
## <a name="controlling-access-to-report-parts"></a>Controlando o acesso a partes de relatório  
 As tabelas a seguir descrevem as atribuições de função padrão e como elas permitem executar várias operações. Os nomes de atribuição de função são diferentes dependendo do tipo de servidor de relatório que está sendo usado.  
  
### <a name="server-in-native-mode"></a>Servidor em modo nativo  
  
|Ações|Funções|  
|-------------|-----------|  
|Adicionar, excluir, editar propriedades de item, gerenciar a segurança e baixar partes de relatório|Gerenciador de Conteúdo<br /><br /> Meus Relatórios|  
|Adicionar, excluir e baixar partes de relatório|Editor|  
|Pesquisar e reutilizar|Navegador<br /><br /> Construtor de Relatórios|  
  
### <a name="server-in-sharepoint-integrated-mode"></a>Servidor em modo integrado do SharePoint  
  
|Ações|Função|  
|-------------|----------|  
|Adicionar, excluir, editar propriedades de item, gerenciar a segurança e baixar partes de relatório|Controle total|  
|Adicionar, excluir, editar propriedades de item e baixar partes de relatório|Design<br /><br /> Contribuir|  
|Pesquisar e reutilizar|Ler<br /><br /> Exibir Apenas|  
  
### <a name="security-considerations"></a>Considerações de segurança  
  
-   Quando as definições de partes de relatório são reutilizadas em um relatório, elas são copiadas na definição do relatório em sua totalidade, junto com o ComponentID que as identifica. Se uma parte de relatório for atualizada no servidor, os usuários poderão escolher baixar as partes de relatório atualizadas aos seus relatórios. As atualizações também são cópias completas da parte de relatório, substituindo a versão existente da parte de relatório que estava no relatório.  
  
    > [!IMPORTANT]  
    >  Em cada uma dessas etapas, verifique se as partes de relatórios estão sendo reutilizadas em relatórios de locais e usuários confiáveis.  
  
-   As partes de relatório usam as mesmas políticas de permissão que as existentes no tipo de item "Resource". Dentro de uma pasta, não há nenhuma diferenciação entre itens de recurso tradicionais e partes de relatório a partir de uma perspectiva de herança de segurança. A parte de relatório herdará a mesma política de permissão que as imagens na mesma pasta. Quando esta distinção é necessária, a segurança de nível de item pode ser configurada para as partes de relatório desejadas. Ou você pode colocar partes de relatório que deveriam estar em pastas separadas e que têm as permissões corretas configuradas.  
  
## <a name="see-also"></a>Consulte Também  
 [Partes de relatório e conjuntos de valores no Construtor de Relatórios](../report-data/report-parts-and-datasets-in-report-builder.md)   
 [Página Propriedades gerais, partes de relatório &#40;Report Manager&#41;](../general-properties-page-report-parts-report-manager.md)   
 [&#40;página mover itens Report Manager&#41;](../move-items-page-report-manager.md)   
 [Gerenciamento do conteúdo do Servidor de Relatório &#40;Modo Nativo do SSRS&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [Solucionar problemas de partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-parts-report-builder-and-ssrs.md)   
 [Partes de relatório no Designer de Relatórios &#40;SSRS&#41;](report-parts-in-report-designer-ssrs.md)  
  
  
