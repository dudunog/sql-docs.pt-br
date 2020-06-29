---
title: Destino do Arquivo Bruto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rawfiledest.f1
helpviewer_keywords:
- append options [Integration Services]
- destinations [Integration Services], Raw File
- raw data [Integration Services]
- writing raw data
- Raw File destination
ms.assetid: d311b458-aefc-4b4d-b1a1-4c0ebbb34214
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 899ca6d278a3117989f2e2371020e98589d67c4b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85431613"
---
# <a name="raw-file-destination"></a>Destino do Arquivo Bruto
  O destino Arquivo Bruto grava dados brutos em um arquivo. Devido ao formato dos dados ser nativo para o destino, os dados não requerem nenhuma tradução e pouca análise. Isso significa que o destino do Arquivo Bruto pode gravar dados mais rápido que outros destinos, tais como o Arquivo Plano e os destinos de OLE DB.  
  
 Além de gravar dados brutos em um arquivo, você também pode usar o destino Arquivo Bruto para gerar um arquivo bruto vazio que contém somente as colunas (arquivo somente de metadados), sem ter que executar o pacote. Use a fonte Arquivo Bruto para recuperar dados brutos que foram escritos previamente pelo destino. Você também pode apontar a fonte Arquivo Bruto para o arquivo somente de metadados.  
  
 O formato de arquivo bruto contém informações de classificação. O destino Arquivo Bruto salva todas as informações de classificação incluindo os sinalizadores de comparação para as colunas de cadeia de caracteres. A fonte Arquivo Bruto lê e segue as informações de classificação. Você tem a opção de configurar fonte Arquivo Bruto para ignorar os sinalizadores de classificação no arquivo, usando o Editor Avançado. Para obter mais informações sobre os sinalizadores de comparação, consulte [Comparando dados de cadeia de caracteres](comparing-string-data.md).  
  
 Você pode configurar o destino de Arquivo Bruto das seguintes formas:  
  
-   Especifique um modo de acesso que seja o nome do arquivo ou uma variável que contenha o nome do arquivo para qual o destino do Arquivo Bruto grava.  
  
-   Indique se o destino do Arquivo Bruto anexa dados a um arquivo existente que tenha o mesmo nome ou cria um arquivo novo.  
  
 O destino do Arquivo Bruto frequentemente é usado para gravar resultados intermediários de dados parcialmente processados entre as execuções de pacotes. Armazenar dados brutos significa que os dados podem ser lidos rapidamente por uma fonte de Arquivo Bruto e posteriormente ser transformados antes que ele seja carregado em seu destino final. Por exemplo, um pacote poderia ser executado várias vezes e cada vez gravar dados brutos em arquivos. Depois, um pacote diferente pode usar a fonte do Arquivo Bruto para ler a partir de cada arquivo, utilizar uma transformação do Union All para intercalar os dados em um conjunto de dados e então aplicar transformações adicionais que resumam os dados antes de carregá-los em seu destino final, tais como uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  O destino do Arquivo Bruto aceita dados nulos, mas não dados de objeto binário grande (BLOB).  
  
> [!NOTE]  
>  O destino do Arquivo Bruto não usa um gerenciador de conexões.  
  
 Esta fonte tem uma entrada normal. Não dá suporte a uma saída de erro.  
  
## <a name="append-and-new-file-options"></a>Opções de acréscimo e arquivo novo  
 A propriedade WriteOption inclui opções para acrescentar dados a um arquivo existente ou criar um arquivo novo.  
  
 A tabela seguinte descreve as opções disponíveis para a propriedade WriteOption.  
  
|Opção|DESCRIÇÃO|  
|------------|-----------------|  
|Acrescentar|Acrescenta dados a um arquivo existente. Os metadados dos dados adicionados devem corresponder ao formato do arquivo.|  
|Criar sempre|Sempre cria um arquivo novo.|  
|Criar uma vez|Cria um arquivo novo. Se o arquivo já existir, o componente falha.|  
|Truncar e acrescentar|Trunca um arquivo existente e depois grava os dados no arquivo. Os metadados dos dados adicionados devem corresponder ao formato do arquivo.|  
  
 Os itens a seguir são importantes sobre como adicionar dados:  
  
-   Adicionar dados a um arquivo bruto existente não reclassifica os dados.  
  
     Você precisa verificar se as chaves classificadas permanecem na ordem correta.  
  
-   Adicionar dados a um arquivo bruto existente não altera os metadados do arquivo (informações de classificação).  
  
 Por exemplo, um pacote lê os dados classificados no PK (ProductKey). O fluxo de dados de pacote adiciona os dados a um arquivo bruto existente. Na primeira vez que o pacote é executado, três linhas são recebidas (PK 1000, 1100, 1200). O arquivo bruto agora contém os seguintes dados.  
  
-   1000, produtoA  
  
-   1100, produtoB  
  
-   1200, produtoC  
  
 Na segunda vez que o pacote é executado, duas novas linhas são recebidas (PK 1001, 1300). O arquivo bruto agora contém os seguintes dados.  
  
-   1000, produtoA  
  
-   1100, produtoB  
  
-   1200, produtoC  
  
-   1001, produtoD  
  
-   1300, produtoE  
  
 Os novos dados são adicionados no final do arquivo bruto e as chaves classificadas (PK) estão fora de ordem. Além disso, a operação de acrescentar não alterou os metadados do arquivo (informações de classificação). Se você ler o arquivo usando a fonte Arquivo Bruto, o componente indicará que o arquivo ainda está classificado em PK, embora os dados no arquivo não estejam mais na ordem correta.  
  
 Para manter as chaves classificadas na ordem correta enquanto adiciona dados, você pode criar o fluxo de dados de pacote da seguinte maneira:  
  
1.  Recupere novas linhas usando a Origem A.  
  
2.  Recupere linhas existentes de RawFile1 usando a Origem B.  
  
3.  Combine as entradas de Origem A e Origem B usando a transformação Union All.  
  
4.  Classifique em PK.  
  
5.  Grave no RawFile2 usando o destino Arquivo Bruto.  
  
     RawFile1 está bloqueado porque está sendo lido no fluxo de dados.  
  
6.  Substitua RawFile1 por RawFile2.  
  
### <a name="using-the-raw-file-destination-in-a-loop"></a>Usando o destino do Arquivo Bruto em um loop  
 Se o fluxo de dados que usa o destino do Arquivo Bruto estiver em um loop, talvez você precise criar o arquivo uma vez e, em seguida, acrescentar dados ao arquivo quando o loop se repetir. Para acrescentar dados ao arquivo, os dados que são acrescentados devem corresponder ao formato do arquivo existente.  
  
 Para criar o arquivo na primeira iteração do loop e então acrescentar filas nas iterações subsequentes do loop, você precisa fazer o seguinte na hora do design:  
  
1.  Defina a propriedade WriteOption como **CreateOnce** ou **CreateAlways**e execute uma iteração do loop. O arquivo é criado. Isto assegura que os metadados de dados acrescentados e o arquivo correspondam.  
  
2.  Redefina a propriedade WriteOption como **Append** e defina a propriedade ValidateExternalMetadata como `False` .  
  
 Se você usar a opção **TruncateAppend** em vez da opção **Append** , truncará filas que foram adicionadas a qualquer iteração anterior e então acrescentará novas filas. Usar a opção **TruncateAppend** também requer que os dados correspondam ao formato do arquivo.  
  
## <a name="configuration-of-the-raw-file-destination"></a>Configuração do destino Arquivo Bruto  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../common-properties.md)  
  
-   [Propriedades personalizadas de arquivo bruto](raw-file-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como definir as propriedades do componente, consulte [Definir as propriedades de um componente de fluxo de dados](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Entrada de blog, [Raw Files Are Awesome](https://www.sqlservercentral.com/blogs/31-days-of-ssis-%e2%80%93-raw-files-are-awesome-131)(Arquivos brutos são incríveis), em sqlservercentral.com.  
  
## <a name="see-also"></a>Consulte Também  
 [Fonte de arquivo bruto](raw-file-source.md)   
 [Fluxo de Dados](data-flow.md)  
  
  
