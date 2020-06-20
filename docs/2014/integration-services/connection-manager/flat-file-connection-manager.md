---
title: Gerenciador de Conexões de Arquivo Simples | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], Flat File
- connections [Integration Services], flat files
- files [Integration Services], connections
- Flat File connection manager
- flat files
- flat file connections [Integration Services]
ms.assetid: 7830f80d-af32-4e8f-a6fc-f03af6bc1946
author: janinezhang
ms.author: janinez
ms.openlocfilehash: e46c1ea54ba178fba73a1bfb2cc8ee296ca2b0d0
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84920854"
---
# <a name="flat-file-connection-manager"></a>Gerenciador de conexões de arquivos simples
  Um gerenciador de conexões de Arquivos Simples permite que um pacote acesse dados em um arquivo simples. Por exemplo, a origem e o destino dos Arquivos Simples podem usar gerenciadores de conexões de Arquivos Simples para extrair e carregar dados.  
  
 O gerenciador de conexões de arquivos simples pode acessar apenas um arquivo. Para consultar vários arquivos, utilize um gerenciador de conexões de vários arquivos simples em vez de um gerenciador de conexões de arquivos simples. Para obter mais informações, consulte [Gerenciador de conexões de vários arquivos simples](multiple-flat-files-connection-manager.md).  
  
## <a name="column-length"></a>Comprimento da coluna  
 Por padrão, o gerenciador de conexões de arquivos simples define o comprimento das colunas de cadeia de caracteres como 50 caracteres. Na caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** , você pode avaliar dados de exemplo e redimensionar automaticamente o comprimento dessas colunas para evitar truncamento dos dados ou excesso de largura da coluna. Mesmo assim, a menos que você redimensione subsequentemente o comprimento de coluna em uma fonte de arquivo simples ou em uma transformação, o comprimento da coluna da coluna de cadeia de caracteres permanece o mesmo durante o fluxo de dados. Se essas colunas de cadeia de caracteres forem mapeadas para colunas de destino que sejam menores, serão exibidos avisos na interface do usuário. Além disso, durante no tempo de execução, podem ocorrer erros devido ao truncamento de dados. Para evitar erros ou truncamento, você pode redimensionar as colunas para que sejam compatíveis com as colunas de destino no gerenciador de conexões de arquivos simples, na origem do arquivo simples ou na transformação. Para modificar o comprimento das colunas de saída, defina a `Length` propriedade da coluna saída na guia **Propriedades de entrada e saída** na caixa de diálogo **Editor avançado** .  
  
 Se você atualizar os comprimentos da coluna no gerenciador de conexões de arquivos simples após adicionar e configurar a fonte de arquivo simples que utiliza o gerenciador de conexões, não será necessário redimensionar manualmente as colunas de saída na origem do arquivo simples. Quando você abre a caixa de diálogo **Origem de Arquivo Simples** , a origem de arquivo simples fornece uma opção para sincronizar os metadados da coluna.  
  
## <a name="configuration-of-the-flat-file-connection-manager"></a>Configuração do gerenciador de conexões de arquivo simples  
 Quando você adiciona um Gerenciador de conexões de arquivo simples a um pacote, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o cria um Gerenciador de conexões que será resolvido para uma conexão de arquivo simples em tempo de execução, define as propriedades de conexão de arquivo simples e adiciona o Gerenciador de conexões de arquivo simples à `Connections` coleção do pacote.  
  
 A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `FLATFILE`.  
  
 Por padrão, o gerenciador de conexões de arquivos simples sempre verifica se há um delimitador de linha em dados sem aspas e inicia uma nova linha quando um delimitador de linha é localizado. Isso permite que o gerenciador de conexões analise corretamente arquivos com linhas que não têm campos de coluna.  
  
 Em alguns casos, desabilitar esse recurso pode melhorar o desempenho do pacote. Você pode desabilitar esse recurso definindo a propriedade do Gerenciador de conexões de arquivo simples, **AlwaysCheckForRowDelimiters**, para `False` .  
  
 Você pode configurar um gerenciador de conexões de arquivos simples dos seguintes modos:  
  
-   Especifique o arquivo, a localidade e a página de código que serão usados. A localidade é usada para interpretar dados confidenciais de localidade como datas, e a página de código é usada para converter dados de cadeia de caracteres para Unicode.  
  
-   Especifique o formato de arquivo. Você pode usar um formato delimitado, de largura fixa ou irregular à direita.  
  
-   Especifique uma linha de cabeçalho, fila de dados e delimitadores de coluna. Delimitadores de coluna podem ser definidos no nível de arquivo e ser sobrescritos no nível de coluna.  
  
-   Indique se a primeira linha nos arquivos contém nomes de coluna.  
  
-   Especifique um caractere de qualificador de texto. Cada coluna pode ser configurada para reconhecer um qualificador de texto.  
  
     Agora há suporte para o uso de um caractere qualificador para inserir um caractere qualificador em uma cadeia de caracteres qualificada. A instância dupla de um qualificador de texto é interpretada como uma instância literal única daquela cadeia de caracteres. Por exemplo, se o qualificador de texto for uma aspa simples e os dados de entrada forem 'abc', 'def', 'g'hi', os dados de saída serão abc, def, g'hi.  
  
-   Defina as propriedades, como o nome, o tipo de dados e a largura máxima em colunas individuais.  
  
 Você pode definir a propriedade ConnectionString para o gerenciador de conexões de arquivos simples especificando uma expressão na janela Propriedades do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para evitar um erro de validação, siga as etapas abaixo.  
  
-   Quando você usa uma expressão para especificar o arquivo, adiciona um caminho de arquivo na caixa **Nome do Arquivo** em **Editor do Gerenciador de Conexões de Arquivos Simples**.  
  
-   Defina a propriedade **DelayValidation** no gerenciador de conexões de Arquivos Simples para **True**.  
  
 Você pode usar uma expressão para criar um nome de arquivo em runtime usando o gerenciador de conexões de Arquivo Simples com o destino do Arquivo Simples.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Geral&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Colunas&#41;](../flat-file-connection-manager-editor-columns-page.md)  
  
-   [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Avançado&#41;](../flat-file-connection-manager-editor-advanced-page.md)  
  
-   [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Visualização&#41;](../flat-file-connection-manager-editor-preview-page.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
