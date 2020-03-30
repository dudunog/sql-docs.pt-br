---
title: Extensão da instância gerenciada do Banco de Dados SQL do Azure
titleSuffix: Azure Data Studio
description: Usar o Azure Data Studio com a instância gerenciada do SQL do Azure
ms.custom: seodec18
ms.date: 10/07/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
manager: alanyu
ms.openlocfilehash: 2269c594bd0fff036d4fe5d5d722aa5d78d4ca6d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75883993"
---
# <a name="azure-sql-database-managed-instance-dashboard-for-azure-data-studio-preview"></a>Painel de instância gerenciada do Banco de Dados SQL do Azure para o Azure Data Studio (versão prévia)

A extensão da instância gerenciada do Banco de Dados SQL do Azure fornece um painel para trabalhar com uma [instância gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-index) no [Azure Data Studio](https://github.com/Microsoft/azuredatastudio). Essa extensão fornece os seguintes recursos:

- Mostra as propriedades da instância gerenciada, incluindo vCores e armazenamento usado
- Monitora o uso de CPU e de armazenamento nas duas horas anteriores
- Exibir avisos de configuração e recomendações de ajuste
- Mostra o estado das réplicas de bancos de dados
- Exibir logs de erros filtrados

## <a name="install"></a>Instalar

Você pode instalar a versão oficial dessa extensão. Siga as etapas na [documentação do Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/extensions).
No painel **Extensões**, pesquise "instância gerenciada" e instale-a nele. Depois da instalação, você será notificado automaticamente sobre atualizações futuras de extensão.

Com a extensão instalada, você verá uma guia **Instância Gerenciada** no Azure Data Studio. Aqui, é possível encontrar informações específicas para sua instância gerenciada.

## <a name="properties"></a>Propriedades

A extensão exibe características técnicas e alguns usos de recursos de sua instância gerenciada.

[ ![Propriedades da instância gerenciada](media/azure-sql-mi-extension/ads-mi-tab1.png )](media/azure-sql-mi-extension/ads-mi-tab1.png#lightbox)

O painel superior mostra os seguintes detalhes:

- **Propriedades**. Obtenha informações básicas sobre sua instância gerenciada, incluindo vCores, memória e armazenamento disponíveis. Encontre também sua camada de serviço, geração de hardware e características de E/S atuais, como taxa de transferência de gravação de log de instância ou características de taxa de transferência de E/S de arquivo.
- **Armazenamento SSD local**. Na camada de serviço de uso geral, arquivos **TempDB** são armazenados localmente. Na camada de serviço comercialmente crítica, _todos_ os arquivos de banco de dados são colocados no armazenamento SSD local. Nessa seção, você pode ver quanto espaço do armazenamento local é usado pela sua instância gerenciada.
- **Armazenamento em Disco Premium do Azure**. Se você tiver a camada de serviço de uso geral, os arquivos de banco de dados do usuário e do sistema serão colocados no armazenamento Premium do Azure. Nesta seção, você pode ver a quantidade de dados usados, o número de arquivos e o armazenamento disponível. Na camada de serviço comercialmente crítica, esta seção fica vazia.
- **Uso de recurso**. Exiba o percentual de armazenamento e a CPU que sua instância gerenciada usou nas duas horas anteriores. Dessa forma, você poderá aumentar o tamanho da instância se ela estiver se aproximando do limite.

## <a name="recommendations"></a>Recomendações

Ao selecionar o segundo painel na guia **Instância Gerenciada**, você recebe recomendações e alertas para ajudar a otimizar sua instância gerenciada.

[ ![Recomendações para instância gerenciada](media/azure-sql-mi-extension/ads-mi-tab2.png )](media/azure-sql-mi-extension/ads-mi-tab2.png#lightbox)

Você pode ver algumas das seguintes recomendações:

- **Atingindo o limite de espaço de armazenamento**. Exclua dados desnecessários ou aumente o tamanho do armazenamento da instância. Os bancos de dados que atingem o limite de armazenamento podem falhar ao processar até mesmo consultas lidas.
- **Atingindo o limite de taxa de transferência da instância**. Notifica quando você está chegando perto do limite de sua camada de serviço: 22 MB/s para uso geral ou 48 MB/s para comercialmente crítico. Sua instância gerenciada limitará a carga para garantir que os backups possam ser feitos.
- **Pressão de memória**. Baixa duração prevista da página ou muitas estatísticas de espera de `PAGEIOLATCH` podem indicar que sua instância está removendo páginas da memória e tentando constantemente carregar mais páginas do disco.
- **Limites do arquivo de log**. Caso os arquivos de logs estejam se aproximando dos [limites de E/S de arquivo na camada de serviço de uso geral](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier), talvez seja necessário aumentar o tamanho do arquivo de log para melhorar o desempenho.
- **Limites do arquivo de dados**. Caso os arquivos de dados estejam se aproximando dos [limites de E/S de arquivo na camada de serviço de uso geral](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-resource-limits#file-io-characteristics-in-general-purpose-tier), talvez seja necessário aumentar o tamanho do arquivo para melhorar o desempenho. Esse problema pode causar demanda de memória e reduzir os backups.
- **Problemas de disponibilidade**. Um grande número de arquivos de log virtuais pode afetar o desempenho. Se houver uma falha de processo, esses problemas poderão resultar em uma recuperação de banco de dados mais longa na camada de serviço de uso geral.

Examine periodicamente essas recomendações, investigue as causas raiz e adote ações corretivas. A extensão de instância gerenciada do Banco de Dados SQL do Azure fornece scripts que você pode executar para atenuar alguns dos problemas relatados.

## <a name="replicas"></a>Réplicas

O terceiro painel na guia **Instância Gerenciada** mostra o estado das réplicas de banco de dados em sua instância gerenciada.

[ ![Réplicas de instância gerenciada](media/azure-sql-mi-extension/ads-mi-tab3.png )](media/azure-sql-mi-extension/ads-mi-tab3.png#lightbox)

Na camada de serviço de uso geral, cada banco de dados tem uma única réplica (primária). Em uma instância de nível comercialmente crítico, cada banco de dados tem uma réplica primária e três secundárias, uma das quais é usada para cargas de trabalho somente leitura. No painel **Réplicas**, você pode monitorar o processo de sincronização e verificar se todas as réplicas secundárias estão sincronizadas com a réplica primária.

## <a name="logs"></a>Logs

O quarto painel da **Instância Gerenciada** mostra as entradas de log de erros do SQL mais recentes e relevantes.

[ ![Entradas de log de instância gerenciada](media/azure-sql-mi-extension/ads-mi-tab4.png )](media/azure-sql-mi-extension/ads-mi-tab4.png#lightbox)

Embora sua instância gerenciada gere um grande número de entradas de log, a maioria contém informações internas/do sistema. Além disso, algumas entradas de log mostram nomes de bancos de dados físicos (valores `GUID`) em vez de nomes de banco de dados lógicos reais.

A extensão de instância gerenciada do Banco de Dados SQL do Azure filtra entradas de log desnecessárias com base no [método de Dimitri Furman](https://techcommunity.microsoft.com/t5/DataCAT/Azure-SQL-DB-Managed-Instance-sp-readmierrorlog/ba-p/305506). A extensão também exibe nomes de arquivos lógicos reais, em vez de nomes físicos.

## <a name="reporting-problems"></a>Relatar problemas

Se você tiver problemas com a extensão da instância gerenciada do Banco de Dados SQL do Azure, vá para o [projeto GitHub da Extensão](https://github.com/JocaPC/AzureDataStudio-Managed-Instance/issues) e relate seu problema.

## <a name="code-of-conduct"></a>Código de conduta

Este projeto adotou o [Código de Conduta de Software Livre da Microsoft][conduct-code].

Para saber mais, confira as [Perguntas frequentes sobre o Código de Conduta][conduct-FAQ] ou contate o [opencode@microsoft.com][conduct-email] caso tenha outras dúvidas ou comentários.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, acesse o [projeto GitHub](https://github.com/JocaPC/AzureDataStudio-Managed-Instance/).

[conduct-code]: https://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: https://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
