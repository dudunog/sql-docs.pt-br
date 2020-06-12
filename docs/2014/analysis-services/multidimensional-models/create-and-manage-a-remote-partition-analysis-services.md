---
title: Criar e gerenciar uma partição remota (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- partitions [Analysis Services], remote
- remote partitions [Analysis Services]
ms.assetid: 4322b5cb-af07-4e79-8ecb-59e1121a9eb8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6c87de5fb72036848088afd2fbfd651be5d7b850
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84536108"
---
# <a name="create-and-manage-a-remote-partition-analysis-services"></a>Criar e gerenciar uma partição remota (Analysis Services)
  Ao particionar um grupo de medidas, você pode configurar um banco de dados secundário em uma instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como um armazenamento da partição.  
  
 Partições remotas para um cubo (chamado de banco de dados mestre), são armazenadas em um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dedicado na instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (chamado de banco de dados secundário).  
  
 Um banco de dados secundário dedicado pode armazenar partições remotas para um único banco de dados mestre, mas o banco de dados mestre pode usar vários bancos de dados secundários, desde que todos os bancos de dados secundários estejam na mesma instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Dimensões em um banco de dados dedicado a partições remotas são criadas como dimensões vinculadas.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Antes de criar uma partição remota, as seguintes condições devem ser cumpridas:  
  
-   Você deve ter uma segunda instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e um banco de dados dedicado para armazenar as partições. O banco de dados secundário tem uma única finalidade; ele fornece o armazenamento de partições remotas para um banco de dados mestre.  
  
-   Ambas as instâncias de servidor devem ter a mesma versão. Ambos os bancos de dados devem ter o mesmo nível funcional.  
  
-   Ambas as instâncias devem ser configuradas para conexões TCP. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não dá suporte à criação de partições remotas usando o protocolo HTTP.  
  
-   As configurações de firewall em ambos os computadores devem ser definidas para aceitar conexões externas. Para obter mais informações sobre como configurar o firewall, consulte [Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
-   A conta de serviço para a instância que executa o banco de dados mestre deve ter acesso administrativo à instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Se a conta de serviço for alterada, você deverá atualizar permissões no servidor e no banco de dados.  
  
-   Você precisa ser administrador do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nos dois computadores.  
  
-   Certifique-se de que seu plano de recuperação de desastres acomode o backup e a restauração das partições remotas. Usar partições remotas pode complicar operações de backup e restauração. Teste minuciosamente seu plano para ter certeza de que você pode restaurar os dados necessários.  
  
## <a name="configure-remote-partitions"></a>Configurar partições remotas  
 Dois computadores separados que executam uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são necessários para criar uma organização de partição remota que designa um computador como o servidor mestre e o outro computador como o servidor subordinado.  
  
 O procedimento a seguir supõe que você tenha duas instâncias de servidor, com um banco de dados de cubo implantado no servidor mestre. Para fins deste procedimento, o banco de dados de cubo é referenciado como db-master. O banco de dados de armazenamento que contém partições remotas é referenciado como db-storage.  
  
 Você usará o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para concluir este procedimento.  
  
> [!NOTE]  
>  As partições remotas podem ser mescladas somente com outras partições remotas. Se você estiver usando uma combinação de partições locais e remotas, uma abordagem alternativa é criar novas partições que incluam os dados combinados, excluindo as partições que não são mais usadas.  
  
#### <a name="specify-valid-server-names-for-cube-deployment-in-ssdt"></a>Especificar nomes de servidor válidos para a implantação de cubo (no SSDT)  
  
1.  No servidor mestre: no Gerenciador de Soluções, clique com o botão direito do mouse no nome da solução e selecione **Propriedades**. Na caixa de diálogo **Propriedades** , clique em **Propriedades de Configuração**, em **Implantação**e em **Servidor** . Defina o nome do servidor mestre.  
  
2.  No servidor subordinado: no Gerenciador de Soluções, clique com o botão direito do mouse no nome da solução e selecione **Propriedades**. Na caixa de diálogo **Propriedades** , clique em **Propriedades de Configuração**, em **Implantação**e em **Servidor** . Defina o nome do servidor subordinado.  
  
#### <a name="create-and-deploy-a-secondary-database-in-ssdt"></a>Criar e implantar um banco de dados secundário (no SSDT)  
  
1.  No servidor subordinado: Crie um novo projeto do Analysis Services para o banco de dados de armazenamento.  
  
2.  No servidor subordinado: No Gerenciador de Soluções, crie uma nova fonte de dados que aponte para o banco de dados do cubo, db-master. Use o provedor **OLE DB Nativo\Provedor Microsoft OLE DB para Analysis Services 11.0**.  
  
3.  No servidor subordinado: Implante a solução.  
  
#### <a name="enable-features-in-ssms"></a>Habilitar recursos (no SSMS)  
  
1.  No servidor subordinado: no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse na instância conectada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no Pesquisador de Objetos e selecione **Propriedades**. Defina **Feature\LinkToOtherInstanceEnabled** e **Feature\LinkFromOtherInstanceEnabled** como **True**.  
  
2.  No servidor subordinado: reinicie o servidor clicando com o botão direito do mouse no nome do servidor no Pesquisador de Objetos e selecionando **Reiniciar**.  
  
3.  No servidor mestre: no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse na instância conectada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no Pesquisador de Objetos e selecione **Propriedades**. Defina **Feature\LinkToOtherInstanceEnabled** e **Feature\LinkFromOtherInstanceEnabled** como **True**.  
  
4.  No servidor mestre: para reiniciar o servidor, clique com o botão direito do mouse no nome do servidor no Pesquisador de Objetos e selecione **Reiniciar**.  
  
#### <a name="set-the-masterdatasourceid-database-property-on-the-remote-server-in-ssms"></a>Definir a propriedade do banco de dados MasterDataSourceID no servidor remoto (no SSMS)  
  
1.  No servidor subordinado: clique com o botão direito do mouse na janela Banco de dados de armazenamento, armazenamento de banco de dados, ponto de **script como**  |  **alterar para**  |  **nova editor de consultas**.  
  
2.  Adicione **MasterDataSourceID** ao XMLA e especifique a ID do banco de dados do cubo, db-master, como o valor. O XMLA deve ter a aparência a seguir.  
  
    ```  
    <Alter ObjectExpansion="ExpandFull" xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">  
    <Object>  
       <DatabaseID>DB-Storage</DatabaseID>  
    </Object>  
    <ObjectDefinition>  
       <Database xmlns:xsd="http://www.w3.org/2001/XMLSchema" 400"   
          <ID>DB-Storage</ID>  
          <Name>DB-StorageB</Name>  
          <ddl200:CompatibilityLevel>1100</ddl200:CompatibilityLevel>  
          <Language>1033</Language>  
          <Collation>Latin1_General_CI_AS</Collation>  
          <DataSourceImpersonationInfo>  
    <ImpersonationMode>ImpersonateAccount</ImpersonationMode>  
             <Account>*********</Account>  
          </DataSourceImpersonationInfo>  
          <MasterDataSourceID>DB-Master</MasterDataSourceID>  
       </Database>  
    </ObjectDefinition>  
    </Alter>  
    ```  
  
3.  Pressione F5 para executar o script.  
  
#### <a name="set-up-the-remote-partition-in-ssdt"></a>Configurar a partição remota (no SSDT)  
  
1.  No servidor mestre: Abra o cubo no designer de cubo e clique na guia **partições** . expanda o grupo de medidas. Clique em **Nova Partição** se o grupo de medidas já estiver configurado para várias partições ou clique no botão Procurar. . ) na coluna de origem para editar a partição existente.  
  
2.  No Assistente para Partições, em **Especificar Informações sobre a Origem**, selecione a Exibição da Fonte de Dados original e a tabela de fatos.  
  
3.  Se estiver usando uma associação de consulta, forneça uma cláusula WHERE que segmente os dados para a nova partição que você estiver criando.  
  
4.  Em **Locais de Processamento e Armazenamento**, em **Local de Processamento**, escolha **Fonte de dados remota do Analysis Services** e clique em **Nova** para criar uma nova fonte de dados que aponta para o banco de dados subordinado, db-storage.  
  
    > [!NOTE]  
    >  Se você receber um erro indicando que a fonte de dados não existe na coleção, abra o projeto de banco de dados de armazenamento, db-storage, e crie uma fonte de dados que aponte para o banco de dados mestre, db-master.  
  
5.  No servidor mestre: clique com o botão direito do mouse no nome do cubo no Gerenciador de Soluções, selecione **Processar** e processe totalmente o cubo.  
  
## <a name="administering-remote-partitions"></a>Administrando partições remotas  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dá suporte ao processamento paralelo e sequencial de partições remotas. O banco de dados mestre, onde as partições foram definidas, coordena as transações entre todas as instâncias que participam no processamento das partições de um cubo. Os relatórios de processamento são então enviados a todas as instâncias que processaram uma partição.  
  
 Um cubo que contém partições remotas pode ser administrado junto com suas partições em uma única instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Porém, os metadados para a partição remota podem ser exibidos e atualizados somente na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] onde foram definidos a partição e seu cubo pai. A partição remota não pode ser exibida ou atualizada na instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Embora bancos de dados dedicados a armazenamento de partições remotas não seja exposto a conjuntos de linhas de esquema, os aplicativos que usam AMO (Objetos de Gerenciamento de Análise) ainda podem descobrir um banco de dados dedicado usando o comando Discover do XML for Analysis. Qualquer comando CREATE ou DELETE que é enviado diretamente a um banco de dados dedicado usando um TCP ou cliente de HTTP terá sucesso, mas o servidor retornará um aviso indicando que a ação pode danificar o banco de dados gerenciado de perto.  
  
## <a name="see-also"></a>Consulte Também  
 [Partições &#40;Analysis Services – Dados Multidimensionais&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
