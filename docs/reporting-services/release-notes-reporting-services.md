---
title: Notas de versão do (SSRS) 2017 e posteriores | Microsoft Docs
ms.date: 09/01/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.reviewer: maghan
author: casualoak
ms.author: RhysSchmidtke
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: c85d3811fc467d94dc1841b871964e3bb594e2df
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58283286"
---
# <a name="release-notes-for-sql-server-reporting-services-ssrs-2017-and-later"></a>Notas sobre a versão do SSRS (SQL Server Reporting Services) 2017 e posteriores

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017-and-later](../includes/ssrs-appliesto-2017-and-later.md)]

Este artigo descreve as alterações no [!INCLUDE[ssnoversion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS) para versões 2017 e posteriores.

Para obter as notas de versão para controles do Visualizador de relatórios, consulte [notas de versão para o Visualizador de relatórios controles de formulários da Web e WinForms do SSRS](application-integration/release-notes-ssrs-application-integration.md).

<!--
We are "standardizing" all our 'Release Notes' style articles:

  - File names:   'release-notes-[TechArea-Name].md'


  - Content format:   2-column tables.  No longer using bullet lists.

    - Ideally, the 'Details' column should contain a link to another SSRS documentation article wherein the particular issue fix is discussed in any way.  Or if there is more to say beyond one sentence, the other sentences of elaboration would go into the 'Details' column.


  - H2 header names are kept short, for better display.


  - Try to keep all Release Notes in one .md file.  Avoid having multiple R.N. files whose names differ only by version or date.

    - Seriously consider erasing info about ancient releases that are so old that nobody cares about them anymore.  If you really want to retain ancient info, consider doing so in an HTML comment at the end of the .md file, just in case a Microsoft employee needs to re-examine ancient info.  In any case, this file cannot get ever longer, and some deletion or hiding of oldest info must eventually occur.


  - Do use '::: moniker range=' zones when version 2017 is no longer the only version represented inside this .md file.

    - Use the '=' operator on the moniker, not the '>=' operator.
    - In contrast, in our 'Whats New' articles we do use the '>=', rather than '='.

GeneMi, DevOps = 1467988 (MsEng > TechnicalContent) , 2019/03/19
-->

## <a name="1406001109-20190212"></a>14.0.600.1109, 12/02/2019

| Correção do problema | Detalhes |
| :---------- | :------ |
| O instantâneo de cache programa alterações para a "agenda específica do relatório" depois de modificar a assinatura. | &nbsp; |
| rc:Toolbar=false não está funcionando na Express Edition. | &nbsp; |
| Determinados caracteres tailandeses são renderizados incorretamente quando relatórios paginados são exportados para PDF. | &nbsp; |
| Deadlock durante a notificação de conclusão de assinaturas controladas por dados. | &nbsp; |
| Imagens incorporadas não são exibidas em determinadas circunstâncias quando se usa o parâmetro rc:ToolBar=False. | &nbsp; |
| Não é possível criar assinaturas controladas por dados para relatórios que usam parâmetros em cascata. | &nbsp; |
| Não é possível editar assinaturas configuradas com um intervalo inválido. | &nbsp; |
| Atualizações de segurança. | &nbsp; |
| A interface do usuário vinculada a relatórios não está sendo mostrada. | &nbsp; |
| Determinados relatórios paginados com controles de tablix aninhados está com fontes incorretas. | &nbsp; |
| Espaço em branco é adicionado incorretamente para determinados relatórios paginados que contêm regiões de dados tablix. | &nbsp; |
| As linhas de cabeçalhos desaparecem quando as grades de dados simples de um relatório móvel são expandidas. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600906-20180912"></a>14.0.600.906, 12/09/2018

Os seguintes problemas foram corrigidos:

| Correção do problema | Detalhes |
| :---------- | :------ |
| A autenticação personalizada não está retornando informações de cookie corretas. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600892-20180831"></a>14.0.600.892, 31/08/2018

| Correção do problema | Detalhes |
| :---------- | :------ |
| A caixa de texto dentro do retângulo faz com que o retângulo não cresça na vertical quando rc:Toolbar=False e ele tem o texto longo. | &nbsp; |
| O tamanho do texto não está se ajustando caso pageHeight seja inferior a 0,5 polegada. | &nbsp; |
| Deadlock ocorre no banco de dados do catálogo SSRS quando ele é usado com o CRM. | &nbsp; |
| Os cabeçalhos de coluna alinhados verticalmente são exibidos incorretamente ao se rolar para baixo no relatório. | &nbsp; |
| Usuários adicionados à Função de Relatórios do SCOM têm o acesso bloqueado no portal da Web do SSRS. | &nbsp; |
| Caracteres tailandês não são exportados corretamente em PDF. | &nbsp; |
| Alteração de comportamento da função de navegador. | &nbsp; |
| rc:Toolbar=false não funciona na Express Edition. | &nbsp; |
| Falta a barra de rolagem vertical na área de prompt de parâmetro. | &nbsp; |
| Tempo de execução do relatório de dispositivo móvel atualizado. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600744-20180425"></a>14.0.600.744, 25/04/2018

| Correção do problema | Detalhes |
| :---------- | :------ |
| A página de assinaturas controladas por dados não mostra a opção de entrega quando ela é criada. | &nbsp; |
| A atualização do SSRS 2012 para o SSRS 2017 no RSManagement resulta na geração de uma exceção em intervalos de poucos segundos. | &nbsp; |
| Não é possível alterar os valores padrão de parâmetros de vários valores no IE11. | &nbsp; |
| As agendas ficam vazias sempre que a agenda compartilhada é executada. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600689-20180228"></a>14.0.600.689, 28/02/2018

| Correção do problema | Detalhes |
| :---------- | :------ |
| A visibilidade do Parâmetro de Relatório em um relatório vinculado é revertida após a edição das respectivas propriedades. | &nbsp; |
| O parâmetro de URL rc:Toolbar=false não funciona na Express Edition. | &nbsp; |
| Propriedade com expressões em uma caixa de texto com o CanGrow definida como false resulta em valores não exibindo. | &nbsp; |
| Link _Saiba mais_ adicionado à chave do produto (Product Key) na instalação. | &nbsp; |
| O portal da Web com autenticação de formulários personalizados ignora os cookies sliding expiration. | &nbsp; |
| Exportar para o Word cria linhas com alturas diferentes, quando o conteúdo de uma linha está vazio. | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="140600594-20180109"></a>14.0.600.594, 09/01/2018

Algumas atualizações de segurança foram implementadas.

### <a name="140600490-20171101"></a>14.0.600.490, 01/11/2017

Problemas resolvidos com a atualização do SKU.

## <a name="140600451-20170930"></a>14.0.600.451, 30/09/2017

Versão inicial.

## <a name="next-steps"></a>Próximas etapas

[Novidades do Reporting Services (SSRS)?](what-s-new-in-sql-server-reporting-services-ssrs.md)

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).