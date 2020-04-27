---
title: Referências de globais internas e referências de usuários (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5f5e1149-c967-454d-9a63-18ec4a33d985
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ef0438dfa0750c2a516a801a2d81b5d1c0b49721
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106435"
---
# <a name="built-in-globals-and-users-references-report-builder-and-ssrs"></a>Referências globais internas e referências de usuários (Construtor de Relatórios e SSRS)
  A coleção de campos internos que inclui as coleções de `Globals` e de `User` representa valores globais fornecidos pelo Reporting Services quando um relatório é processado. A coleção de `Globals` fornece valores, como o nome do relatório, a hora em que o seu processamento foi iniciado e os números das páginas atuais para o cabeçalho ou o rodapé do relatório. A coleção de `User` fornece o identificador de usuário e configurações de idioma. Esses valores podem ser usados em expressões para filtrar resultados em um relatório.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-globals-collection"></a>Usando a coleção de globais  
 A coleção de `Globals` contém as variáveis globais para o relatório. Na superfície de design, essas variáveis são exibidas prefixadas por um & (E comercial), por exemplo, `[&ReportName]`. A tabela a seguir descreve os membros da coleção de `Globals`.  
  
|**Membro**|**Tipo**|**Descrição**|  
|----------------|--------------|---------------------|  
|ExecutionTime|`DateTime`|A data e a hora em que o relatório começou a ser executado.|  
|PageNumber|`Integer`|O número da página atual em relação às quebras de página que redefinem o número da página. No início do processamento do relatório, o valor inicial é definido como 1. O número da página é incrementado para cada página renderizada.<br /><br /> Para numerar páginas dentro de quebras de página para um retângulo, uma região de dados, um grupo de região de dados ou um mapa, na Propriedade PageBreak, `True`defina a propriedade ResetPageNumber como. Sem suporte em grupos de hierarquias de colunas tablix.<br /><br /> PageNumber somente pode ser usada em uma expressão em um cabeçalho ou rodapé de página.|  
|ReportFolder|`String`|O caminho completo para a pasta que contém o relatório. Isso não inclui a URL do servidor de relatório.|  
|ReportName|`String`|O nome do relatório conforme armazenado no banco de dados do servidor de relatório.|  
|ReportServerUrl|`String`|A URL do servidor de relatório na qual o relatório está sendo executado.|  
|TotalPages|`Integer`|O número total de páginas em relação às quebras de página que redefinem PageNumber. Se nenhuma quebra de página for definida, esse valor será o mesmo de OverallTotalPages.<br /><br /> TotalPages somente pode ser usada em uma expressão em um cabeçalho ou rodapé de página.|  
|PageName|`String`|O nome da página. No início do processamento do relatório, o valor inicial é definido por meio de InitialPageName, uma propriedade de relatório. À medida que cada item do relatório é processado, esse valor é substituído pelo valor correspondente de PageName de um retângulo, uma região de dados, um grupo de regiões de dados ou um mapa. Sem suporte em grupos de hierarquias de colunas tablix.<br /><br /> PageName somente pode ser usada em uma expressão em um cabeçalho ou rodapé de página.|  
|OverallPageNumber|`Integer`|O número da página atual para todo o relatório. Esse valor não é afetado por ResetPageNumber.<br /><br /> OverallPageNumber somente pode ser usada em uma expressão em um cabeçalho ou rodapé de página.|  
|OverallTotalPages|`Integer`|O número total de páginas para todo o relatório. Esse valor não é afetado por ResetPageNumber.<br /><br /> OverallTotalPages somente pode ser usada em uma expressão em um cabeçalho ou rodapé de página.|  
|RenderFormat|`RenderFormat`|Informações sobre a solicitação de renderização atual.<br /><br /> Para obter mais informações, consulte "RenderFormat" na próxima seção.|  
  
 Membros da coleção de `Globals` retornam uma variante. Se você desejar usar um membro dessa coleção em uma expressão que exige um tipo de dados específico, deverá primeiro converter a variável. Por exemplo, para converter a variante de tempo de execução em um formato de Data, use `=CDate(Globals!ExecutionTime)`. Para obter mais informações, consulte [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md).  
  
### <a name="renderformat"></a>RenderFormat  
 A tabela a seguir descreve os membros de `RenderFormat`.  
  
|Membro|Tipo|Descrição|  
|------------|----------|-----------------|  
|Nome|`String`|O nome do renderizador conforme registrado no arquivo de configuração RSReportServer.<br /><br /> Disponível durante partes específicas do ciclo de processamento/renderização do relatório.|  
|IsInteractive|`Boolean`|Se a solicitação de renderização atual usa um formato de renderização interativo.|  
|DeviceInfo|Coleção de nomes/valores somente leitura|Pares de chave/valor para parâmetros deviceinfo da solicitação de renderização atual.<br /><br /> É possível especificar valores de cadeia de caracteres usando a chave ou um índice na coleção.|  
  
### <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como usar uma referência à coleção de `Globals` em uma expressão:  
  
-   Esta expressão, colocada em uma caixa de texto no rodapé de um relatório, fornece o número da página e o total de páginas no relatório:  
  
     `=Globals.PageNumber & " of " & Globals.TotalPages`  
  
-   Esta expressão fornece o nome do relatório e a hora em que foi executado. A hora é formatada com a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] cadeia de caracteres de formatação para data abreviada:  
  
     `=Globals.ReportName & ", dated " & Format(Globals.ExecutionTime, "d")`  
  
-   Esta expressão, colocada na caixa de diálogo **Visibilidade da Coluna** para uma coluna selecionada, exibe a coluna somente quando o relatório é exportado para o Excel. Caso contrário, a coluna fica oculta.  
  
     `EXCELOPENXML` se refere ao formato do Excel que é incluído no Office 2007. `EXCEL` se refere ao formato do Excel que é incluído no Office 2003.  
  
     `=IIF(Globals!RenderFormat.Name = "EXCELOPENXML" OR Globals!RenderFormat.Name = "EXCEL", false, true)`  
  
## <a name="using-the-user-collection"></a>Usando a coleção de usuário  
 A coleção de `User` contém dados sobre o usuário que está executando o relatório. É possível usar essa coleção para filtrar os dados exibidos em um relatório, por exemplo, mostrando apenas os dados do usuário atual ou para exibir a ID do usuário, por exemplo, em um título do relatório. Na superfície de design, essas variáveis são exibidas prefixadas por um & (E comercial), por exemplo, `[&UserID]`.  
  
 A tabela a seguir descreve os membros da coleção de `User`.  
  
|**Membro**|**Tipo**|**Descrição**|  
|----------------|--------------|---------------------|  
|`Language`|`String`|O idioma do usuário que está executando o relatório. Por exemplo, `en-US`.|  
|`UserID`|`String`|A ID do usuário que está executando o relatório. Se a Autenticação do Windows estiver sendo usada, esse valor será a conta de domínio do usuário atual. O valor é determinado pela extensão de segurança do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que pode usar a Autenticação do Windows ou a autenticação personalizada.|  
  
 Para obter mais informações sobre como oferecer suporte a diversos idiomas em um relatório, consulte "Solution Design Considerations for Multi-Lingual or Global Deployments" (Considerações sobre design de solução para implantações globais ou em vários idiomas) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online do SQL Server](https://go.microsoft.com/fwlink/?LinkId=120955).  
  
### <a name="using-locale-settings"></a>Usando configurações de localidade  
 É possível usar expressões para se fazer referência a configurações de localidade em um computador cliente por meio do valor de `User.Language` para determinar como um relatório é exibido para o usuário. Por exemplo, você pode criar um relatório que usa uma expressão de consulta diferente baseada no valor da localidade. A consulta pode se alterada para recuperar informações localizadas de uma coluna diferente dependendo do idioma retornado. Também é possível usar uma expressão nas configurações do idioma do relatório ou de itens de relatório baseados nessa variável.  
  
> [!NOTE]  
>  Embora seja possível alterar as configurações do idioma de um relatório, você deve ter cuidado em relação a qualquer problema de exibição que isso possa provocar. Por exemplo, a alteração da configuração de localidade do relatório pode alterar o formato de data no relatório, mas também o formato da moeda. Isso pode fazer com que o símbolo da moeda incorreta seja exibido no relatório, a não ser que haja um processo de conversão de moeda. Para evitar isso, defina as informações de idioma sobre os itens individuais que você deseja alterar ou defina o item com os dados de moeda como um idioma específico.  
  
### <a name="identifying-userid-for-snapshot-or-history-reports"></a>Identificando a ID de usuário para relatórios de instantâneo ou de histórico  
 Em alguns casos, os relatórios que incluem a variável *User!UserID* não mostrarão os dados de relatório específicos do usuário atual que está exibindo o relatório.  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Caixa de diálogo expressão &#40;Construtor de Relatórios&#41;](../expression-dialog-box-report-builder.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Formatando números e datas &#40;Construtor de Relatórios e SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
  
