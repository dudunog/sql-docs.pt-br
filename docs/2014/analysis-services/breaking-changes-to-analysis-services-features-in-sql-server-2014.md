---
title: Alterações recentes em recursos de Analysis Services no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- breaking changes [Analysis Services]
- upgrading Analysis Services
ms.assetid: aeb02542-5a6c-458c-a110-13413dd3e9d9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 65b70cf2bb85bca60a372f09a5d3fc9ffedb90cc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66064414"
---
# <a name="breaking-changes-to-analysis-services-features-in-sql-server-2014"></a>Alterações recentes em recursos do Analysis Services no SQL Server 2014
  Este tópico descreve as alterações recentes no [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]. Essas alterações podem interromper aplicativos, scripts ou funcionalidades baseados em versões anteriores do SQL Server.  
  
 Neste tópico:  
  
-   [Alterações recentes no SQL Server 2014](#bkmk_sql2014)  
  
-   [Alterações recentes no SQL Server 2012 SP1](#bkmk_2012Sp1)  
  
-   [Alterações recentes no SQL Server 2012](#bkmk_sql11)  
  
-   [Alterações recentes no SQL Server 2008/SQL Server 2008 R2](#bkmk_sql10)  
  
##  <a name="breaking-changes-in-sssql14"></a><a name="bkmk_sql2014"></a> Últimas alterações do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Nenhuma alteração significativa anunciada para mineração de dados tabular, multidimensional ou recursos [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] nesta versão.  No entanto, como  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] é tão semelhante às versões [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] , as alterações significativas de ambas as versões anteriores são fornecidas aqui como uma conveniência, se você estiver atualizando do [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
##  <a name="breaking-changes-in-sql-server-2012-sp1"></a><a name="bkmk_2012Sp1"></a>Alterações recentes no SQL Server 2012 SP1  
 Alterações de código relacionadas à globalização comprovadamente interrompem alguns aplicativos. Os problemas conhecidos incluem:  
  
 **Diferenciação de maiúsculas e minúsculas de identificadores de objeto**  
 Uma alteração de código destinada a fazer com que todos os identificadores de objeto não diferenciem maiúsculas e minúsculas está causando o efeito oposto em alguns idiomas. A intenção é que todos os identificadores de objeto não diferenciem maiúsculas de minúsculas, independentemente da ordenação. Essa alteração alinha o Analysis Services com outros aplicativos geralmente usados na mesma pilha de solução.  
  
 Para idiomas com base em 26 caracteres do alfabeto latino básico, identificadores de objeto agora não diferenciam maiúsculas de minúsculas, que é o comportamento desejado.  
  
 Para cirílico e outros scripts de idioma bicamerais que usam maiúsculas/minúsculas (em grego, armênio, e copta), identificadores de objetos agora diferenciam maiúsculas de minúsculas. As alterações mais recentes têm mais probabilidade de ocorrer quando há diferenciação de maiúsculas/minúsculas entre um identificador de objeto e como ele é referenciado (por exemplo, um script de processamento que se refere ao identificador de objeto com todas as letras minúsculas). Esse comportamento provavelmente será alterado no futuro, mas como uma solução temporária é recomendável modificar os scripts para usar a mesma caixa que o identificador de objeto.  
  
##  <a name="breaking-changes-in-sssql11"></a><a name="bkmk_sql11"></a> Últimas alterações do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 Esta seção documenta as últimas alterações relatadas referentes a recursos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
|Problema|Descrição|  
|-----------|-----------------|  
|Comandos de instalação removidos para uma instalação do [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] .|A instalação é realizada, mas não configura mais um [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]. Os comandos de instalação que coletavam valores usados em ações de configuração agora são removidos. Eles incluem /FARMACCOUNT, /FARMPASSWORD, /PASSPHRASE e /FARMADMINPORT.<br /><br /> Se você criou scripts de instalação para instalação autônoma, precisará modificar esses scripts para uma instalação do [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] . A alternativa é usar cmdlets do PowerShell para configurar o servidor em modo autônomo. Para obter mais informações, consulte [instalar o PowerPivot no prompt de comando e na](../../2014/sql-server/install/install-powerpivot-from-the-command-prompt.md) configuração do [PowerPivot usando o Windows PowerShell](power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md).|  
  
##  <a name="breaking-changes-in-sskatmaisskilimanjaro"></a><a name="bkmk_sql10"></a>Alterações recentes em[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]/[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
 Esta seção contém as alterações de quebra de versões anteriores. Se você estiver atualizando do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], deverá revisar as alterações de quebra introduzidas no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)].  
  
|Problema|Descrição|  
|-----------|-----------------|  
|A função shallow exists agora funciona de maneira diferente com conjuntos nomeados que contêm membros enumerados ou junções cruzadas de enumsets.|No [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], a função shallow exists não funcionava com conjuntos nomeados que continham membros enumerados ou interjunções de conjuntos de enumsets. Para fins de compatibilidade com a versão de lançamento original e o SP1 do [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], defina a propriedade de configuração "ConfigurationSettings\OLAP\Query\NamedSetShallowExistsMode" como 1, ou para compatibilidade com o [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] SP2, defina-a como 2.|  
|As funções do VBA lidam com valores nulos e vazios diferentemente de como faziam no [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]|No [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], as funções do VBA retornavam 0 ou uma cadeia vazia quando valores nulos ou vazios eram usados como argumentos. No [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], elas retornarão nulo.|  
|O Assistente de Migração falhará porque o DSO não é instalado por padrão.|Por padrão, o SQL Server 2008 não instala o componente de compatibilidade com versões anteriores DSO (Decision Support Objects). O pacote de compatibilidade com versões anteriores é instalado por padrão, mas o componente DSO do pacote ficará desabilitado. Uma vez que o Assistente de Migração do SQL Server Analysis Services depende desse componente, ele falhará, a menos que o componente seja instalado. Para instalar o componente DSO, execute o seguinte procedimento:<br /><br /> 1) Abra o painel de controle.<br />2) no Windows XP ou no Windows Server 2003, selecione **Adicionar ou remover programas**. No Windows Vista e Windows Server 2008, selecione **Programas e Recursos**.<br />3) clique com o botão direito do mouse em **2005 Microsoft SQL Server compatibilidade com versões anteriores**e selecione **alterar**.<br />4) no assistente de configuração de compatibilidade com versões anteriores, clique em **Avançar**.<br />5) na página manutenção do programa, selecione **Modificar**e clique em **Avançar**.<br />6) na página seleção de recursos, se o DSO (Decision Support Objects) não estiver disponível, clique na seta para baixo e selecione **este recurso será instalado na unidade de disco rígido local**. Clique em **Avançar**.<br />7) na página pronto para modificar o programa, clique em **instalar**.<br />8) quando a instalação for concluída, clique em **concluir**.<br /><br /> <br /><br /> Você pode remover o DSO após a conclusão da migração seguindo as etapas anteriores, alterando a opção de DSO para "**este recurso não estará disponível**".<br /><br /> Se o pacote de compatibilidade com versões anteriores não estiver instalado, você poderá instalá-lo usando a mídia de distribuição do SQL Server 2008. Observe que existem versões específicas de cada arquitetura de destino (x86, x64, ia64). Essas versões podem ser encontradas nos seguintes locais:<br /><br /> x86\Setup\x86\SQLServer2005_BC.msi<br /><br /> x64\Setup\x64\SQLServer2005_BC.msi<br /><br /> ia64\Setup\ia64\SQLServer2005_BC.msi|  
|Não é recomendável colocar o local da partição na pasta Dados.|O servidor gerencia a pasta Dados e cria ou elimina pastas à medida que objetos são criados, excluídos e alterados. Por isso, é totalmente desaconselhável especificar um local de armazenamento da partição na pasta Dados, principalmente nas subpastas de bancos de dados, cubos e dimensões. Embora o servidor permita fazer isso com Create ou Alter, ele exibirá um aviso. Quando você atualizar bancos de dados do SQL Server 2005 Analysis Services para o [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services que têm locais de armazenamento de partição na pasta Dados, isso funcionará. Restore ou Sync exigirão que você remova os locais de armazenamento da partição da pasta Dados.|  
|Você pode obter resultados inesperados de consultas que usam a palavra-chave MDX "EXISTING" no Servidor Analítico da ProClarity e no Microsoft Office PerformancePoint Server 2007.|O Servidor Analítico da ProClarity e o Microsoft Office PerformancePoint Server 2007 usam a palavra-chave EXISTING da linguagem MDX incorretamente em certos cenários. Devido a alterações feitas no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services, essas consultas podem retornar resultados inesperados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Analysis Services Backward Compatibility](analysis-services-backward-compatibility.md)  
  
  
