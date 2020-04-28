---
title: Definindo propriedades
ms.custom: microsoft-excel-add-in, seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cab1c662-5d40-4c16-9f5c-36ff9608810b
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6f3c303697ec3233935ec5c7743dcce0f18bfa01
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73727989"
---
# <a name="setting-properties-for-master-data-services-add-in-for-excel"></a>Definindo propriedades para o Suplemento do Master Data Services para Excel

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  As configurações do suplemento Master Data Services para Excel determinam como os dados são carregados do MDS para o suplemento do Excel e como os dados são publicados do suplemento do Excel para o MDS.  
  
 Para criar configurações para o suplemento do Excel, abra o **Excel**, clique no menu **Dados Mestres** e clique em **Configurações**. Qualquer um com acesso ao Excel pode alterar essas configurações. As configurações se aplicam ao computador em que o Excel está aberto.  
  
## <a name="excel-add-in-settings"></a>Configurações de suplemento do Excel  
  
||||  
|-|-|-|  
|Guia e seção|Configuração|Descrição|  
|Configurações: publicação|Mostrar a caixa de diálogo **Publicar e Anotar** ao publicar|Selecione para exibir a caixa de diálogo **Publicar e Anotar** depois de clicar em **Publicar**, permitindo a inserção de uma única anotação para todas as alterações ou a inserção de uma anotação para cada alteração.<br /><br /> Desmarque para especificar que o processo Publicar seja iniciado sem a exibição da caixa de diálogo **Publicar e Anotar** . Você não terá a oportunidade de inserir uma anotação.|  
|Configurações: versão|Seleção de versão|Selecione a versão dos dados mestres que será carregada no suplemento do Excel. Pode ser:<br /><br /> **Nenhuma** para que a versão não use como padrão nenhuma versão<br /><br /> **Mais antiga** para usar como padrão a versão mais antiga **Mais Nova** para usar como padrão a versão mais recente.|  
|Configurações: log|Ativar o log detalhado|Habilite o registro em log para o processo de carregar dados mestres do MDS para o Suplemento do Excel, para que o resultado de cada comando no serviço seja registrado em log.|  
|Configurações: telemetria|Ativar coleta de dados de telemetria|Habilite a telemetria para ajudar a melhorar a qualidade, a confiabilidade e o desempenho do Suplemento [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] do Excel.|  
|Configurações: tamanho de lotes|Número de células para carregamento|Selecione um número para indicar quantos milhares de células serão carregados em um lote carregado do servidor MDS para o Excel. O valor padrão é 50.000 células.|  
|Configurações: tamanho de lotes|Número de células para publicação|Selecione um número para indicar quantos milhares de células serão publicadas em um lote retornado do Excel para o servidor. O valor padrão é 50.000 células.|  
|Configurações: servidores adicionados à Lista de Confiança|Limpar Tudo|Clique para limpar a lista de conexões que foram designadas como seguras quando o arquivo de consulta de atalho associado foi aberto.|  
|Dados: filtros|Exibir aviso de filtro para conjuntos de dados grandes|Clique para exibir um aviso se o conjunto de dados sendo carregado do MDS para o Excel exceder o número máximo de linhas ou colunas.|  
|Dados: filtros|Máximo de linhas|Selecione o limite para o número de linhas sendo carregadas, além do qual um aviso de filtro será publicado.|  
|Dados: filtros|Máximo de colunas|Selecione o limite para o número de colunas sendo carregadas, além do qual um aviso de filtro será publicado.|  
|Dados: formato de célula|Alterar a cor quando: os valores de atributo foram alterados|Clique para especificar que a cor de uma célula será alterada se o valor de atributo nessa célula for alterado quando você atualizar a tabela de suplemento do Excel com novos dados do repositório MDS.|  
|Dados: formato de célula|Alterar a cor quando: membros forem adicionados|Clique para especificar que a cor das células de uma linha será alterada se um novo membro for adicionado à linha quando você atualizar a tabela de suplemento do Excel com novos dados do repositório MDS.|  
|Dados: formato de célula|Formato de exibição|Selecione o formato preferencial para exibir os valores dos atributos baseados em domínio. As opções são Código {Nome}, Código e Nome {Código}.|  
  
  
