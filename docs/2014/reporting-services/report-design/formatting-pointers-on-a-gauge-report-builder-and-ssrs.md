---
title: Formatando ponteiros em um medidor (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2fdf670a-5237-48fe-813d-97657c5c77d2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 294586f0d48ca96ca12d3e9eac70f5d2d288654f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105831"
---
# <a name="formatting-pointers-on-a-gauge-report-builder-and-ssrs"></a>Formatando ponteiros de um medidor (Construtor de Relatórios e SSRS)
  Um ponteiro do medidor indica o valor atual do medidor. Por padrão, quando um campo for adicionado, os valores contidos nele serão agregados a um valor mostrado pelo ponteiro do medidor. É possível adicionar vários ponteiros ao medidor para mostrar vários valores na mesma escala, ou adicionar várias escalas e um ponteiro para todas as escalas adicionadas. Depois de adicionar um campo a um medidor, defina os valores mínimo e máximo da escala correspondente para oferecer contexto ao valor do ponteiro. Outra opção é definir os valores mínimo e máximo em um intervalo, que mostra uma área crítica na escala.  
  
 É possível definir propriedades de aparência no ponteiro, clicando com o botão direito do mouse no ponteiro e selecionando **Propriedades de Ponteiro Radial** ou **Propriedades de Ponteiro Linear**. Cada ponteiro do medidor contém o mesmo conjunto de propriedades. Também há propriedades de aparência correspondentes exclusivas de cada tipo de medidor:  
  
-   Em um medidor radial, é possível especificar um ponteiro e uma extremidade de agulha.  
  
-   Em um medidor linear, você pode especificar um ponteiro de termômetro, que é uma variação do ponteiro de barra. O ponteiro de termômetro permite que você especifique a forma do bulbo.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="how-the-pointer-is-connected-to-data"></a><a name="HowPointer"></a> Como o ponteiro é conectado a dados  
 Por padrão, quando adicionado, um medidor contém um ponteiro sem campo associado. Isso é conhecido como ponteiro vazio. Ele exibirá zero até que um campo seja adicionado ao painel de dados. Quando você adiciona um campo ao painel de dados, o ponteiro é conectado a esse campo. Caso você exclua um campo do painel de dados, o ponteiro associado a esse campo também será excluído.  
  
 Depois de adicionar os dados, quando clicar com o botão direito do mouse no ponteiro, você obterá as opções **Limpar Valor do Ponteiro** e **Excluir Ponteiro** . A opção **Limpar Valor do Ponteiro** removerá o campo anexado ao medidor, mas o ponteiro continuará aparecendo no medidor. A opção **Excluir Ponteiro** removerá o campo do medidor e excluirá o ponteiro da exibição. Se você adicionar novamente um campo ao medidor, o ponteiro padrão reaparecerá. Quando você define a propriedade **Hidden** do ponteiro como `True`, o ponteiro não é ocultado na superfície de design, mas fica oculto em tempo de execução.  
  
  
##  <a name="displaying-multiple-pointers-on-the-gauge"></a><a name="DisplayingMultiple"></a> Exibindo vários ponteiros no medidor  
 É possível adicionar vários ponteiros ao medidor para apontar para vários valores na mesma escala. Isso pode ser útil para mostrar valores baixo e alto simultaneamente. Para especificar mais de um ponteiro do medidor na mesma escala, clique com o botão direito do mouse em qualquer lugar do medidor e clique em **Adicionar Ponteiro** no menu de atalho. Também é possível adicionar uma escala clicando com o botão direito do mouse em qualquer lugar do medidor e clicando em **Adicionar Escala**. Assim, você pode adicionar um ponteiro e ele será associado automaticamente à última escala.  
  
 Quando os ponteiros se sobrepõem, a ordem de desenho dos ponteiros é determinada pela ordem na qual eles são adicionados ao medidor. Não é possível reorganizar a ordem de desenho dos ponteiros alterando a ordem dos campos no painel de dados. Para alterar a ordem do desenho de vários ponteiros, abra o painel Propriedades e clique em **Ponteiros (…)** . Em seguida, altere a ordem dos ponteiros na coleção Ponteiro.  
  
  
##  <a name="setting-gradients-on-a-needle-cap"></a><a name="SettingGradients"></a> Definindo as gradações em uma extremidade de agulha  
 Você pode especificar uma extremidade de agulha que possa ser desenhada acima ou abaixo do ponteiro apenas em um ponteiro radial. Todos os estilos de extremidade de agulha são desenhados usando gradações internas que não podem ser modificadas. A exceção é o estilo `RoundedDark`, em que você pode especificar uma cor de gradiente e o estilo de gradiente.  
  
  
##  <a name="setting-a-snapping-interval"></a><a name="SettingSnappingInterval"></a> Como definir um intervalo de ajuste  
 Um intervalo de ajuste define o múltiplo para o qual os valores são arredondados. Por padrão, o medidor apontará para o valor exato do campo especificado no painel de dados. No entanto, talvez você queira arredondar o valor exato para cima ou para baixo de forma que o ponteiro se ajuste a um intervalo predefinido. Por exemplo, se o valor em seu medidor for 34,2 e você especificar um intervalo de ajuste de 5, o ponteiro do medidor apontará para 35. Se o valor em seu medidor for 31,2 e você especificar um intervalo de ajuste de 5, o ponteiro do medidor apontará para 30. Para obter mais informações, consulte [definir um intervalo de ajuste em um medidor &#40;Construtor de relatórios e SSRS&#41;](../set-a-snapping-interval-on-a-gauge-report-builder-and-ssrs.md).  
  
  
##  <a name="specifying-an-image-as-a-pointer-on-a-radial-gauge"></a><a name="SpecifyingImage"></a> Especificando uma imagem como um ponteiro em um medidor radial  
 Além da lista interna dos estilos de ponteiro, é possível especificar uma imagem como um ponteiro. Isso é muito efetivo quando você usa uma imagem para substituir um estilo de ponteiro de agulha existente. A imagem é sobreposta no ponteiro, mas toda a funcionalidade de ponteiro é aplicável. As opções de cor e de gradação não são aplicáveis quando uma imagem é usada no ponteiro.  
  
 Caso a forma da imagem do ponteiro seja irregular, você deve definir a cor como transparente para ocultar as áreas da imagem que não devem ser exibidas no medidor. Quando você define uma cor transparente, o medidor transpõe a imagem no ponteiro existente e corta a imagem para que apenas a forma do ponteiro seja exibida. O medidor redimensiona a imagem para ajustar o tamanho do ponteiro. Quando você especificar uma imagem de um ponteiro, todos os ponteiros subsequentes adicionados acima do medidor serão desenhados abaixo da imagem. Por esse motivo, é melhor não especificar uma imagem para o ponteiro caso haja vários ponteiros no medidor. Para obter mais informações, consulte [especificar uma imagem como um ponteiro em um medidor &#40;Construtor de relatórios e SSRS&#41;](../specify-an-image-as-a-pointer-on-a-gauge-report-builder-and-ssrs.md).  
  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando escalas em um medidor &#40;Construtor de Relatórios e SSRS&#41;](formatting-scales-on-a-gauge-report-builder-and-ssrs.md)   
 [Formatando intervalos de um medidor &#40;Construtor de Relatórios e SSRS&#41;](formatting-ranges-on-a-gauge-report-builder-and-ssrs.md)   
 [Medidores &#40;Construtor de Relatórios e SSRS&#41;](gauges-report-builder-and-ssrs.md)  
  
  
