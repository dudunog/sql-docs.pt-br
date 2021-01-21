---
title: SQL Server habilitado para Azure Arc – Notas sobre a versão
description: Notas sobre a versão mais recentes
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 12/08/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 372f4bec9acc4d4e170ddbc1a1fa6d66be1541e7
ms.sourcegitcommit: d8cdbb719916805037a9167ac4e964abb89c3909
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98596548"
---
# <a name="release-notes---azure-arc-enabled-sql-server-preview"></a>Notas sobre a versão – SQL Server habilitado para Azure Arc (versão prévia)

> [!NOTE]
> Como uma versão prévia do recurso, a tecnologia apresentada neste artigo está sujeita aos [Termos de uso complementares para versões prévias do Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## <a name="december-2020"></a>Dezembro de 2020

### <a name="breaking-change"></a>Alteração da falha

Esta versão apresenta um [provedor de recursos](/azure/azure-resource-manager/management/azure-services-resource-providers) atualizado chamado `Microsoft.AzureArcData`. Para continuar usando o SQL Server habilitado para Azure Arc, registre esse provedor de recursos. Confira as instruções de registro do provedor de recursos na seção [pré-requisitos](connect.md#prerequisites).

Se você tiver recursos existentes do SQL Server – Azure Arc, use estas etapas para migrá-los para o namespace Microsoft.AzureArcData.

1. Inicie o [Cloud Shell](https://shell.azure.com/). Para obter detalhes, [leia mais sobre o PowerShell no Cloud Shell](/azure/cloud-shell/quickstart-powershell).

2. Carregue o script no shell usando o seguinte comando:

    ```console
    curl https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/manage/azure-arc-enabled-sql-server/migrate-to-azure-arc-data.ps1 -o migrate-to-azure-arc-data.ps1
    ```
3. Execute o script.  

    ```console
   ./migrate-to-azure-arc-data.ps1
    ```

> [!NOTE]
> - Para colar os comandos no shell, use `Ctrl-Shift-V` no Windows ou `Cmd-v` no MacOS.
> - O script será carregado diretamente na pasta base associada à sua sessão do Cloud Shell.
> - O script solicitará o nome do grupo de recursos e imprimirá uma mensagem quando a migração for concluída.

### <a name="other-changes"></a>Outras alterações

* A propriedade *TCPPorts* no tipo de recurso **SQL Server – Azure Arc** foi renomeado para *TCPStaticPorts*
* As permissões necessárias não são tão amplas quanto costumavam ser. Confira a seção [Permissão necessária](overview.md#required-permissions) para obter detalhes.

### <a name="known-issues"></a>Problemas conhecidos

* A propriedade *CreateTime* não será adicionada a nenhum recurso recém-criado no namespace AzureArcData, incluindo os recursos **SQL Server – Azure Arc**.

## <a name="october-2020"></a>Outubro de 2020

A atualização de outubro inclui os seguintes aprimoramentos:

* Agora, a folha Registrar SQL Server habilitado para Azure Arc inclui a guia **Marcas**. As marcas são incluídas no script de registro e são refletidas no recurso **SQL Server – Azure Arc**. Para conhecer os detalhes, confira [Conectar o SQL Server ao Azure Arc](connect.md).

* Agora, a entrada **Integridade do Ambiente** dá suporte à ativação da **Avaliação do SQL** no Portal implantando uma *CustomScriptExtension*. Para conhecer os detalhes, confira [Configurar a Avaliação do SQL](assess.md#run-on-demand-sql-assessment).

### <a name="known-issues"></a>Problemas conhecidos

Os seguintes problemas se aplicam à versão de outubro:

* Conectar instâncias do SQL Server ao Azure Arc requer uma conta com um conjunto amplo de permissões. Para conhecer os detalhes, confira [Permissões necessárias](overview.md#required-permissions).

## <a name="september-2020"></a>Setembro de 2020

O SQL Server habilitado para Azure Arc foi lançado na versão prévia pública. O SQL Server habilitado para Azure Arc estende os serviços do Azure para instâncias do SQL Server hospedadas fora do Azure no datacenter do cliente, na borda ou em um ambiente de várias nuvens.

Para conhecer os detalhes, confira [Visão geral do SQL Server habilitado para Azure Arc](overview.md)

### <a name="known-issues"></a>Problemas conhecidos

Os seguintes problemas se aplicam à versão de setembro:

* A folha **Registrar o SQL Server habilitado para Azure Arc** não dá suporte à configuração de marcas personalizadas. Para adicionar marcas personalizadas, abra o recurso **SQL Server – Azure Arc** após o registro e altere as Marcas na página **Visão geral**.

* Conectar instâncias do SQL Server ao Azure Arc requer uma conta com um conjunto amplo de permissões. Para conhecer os detalhes, confira [Permissões necessárias](overview.md#required-permissions).

## <a name="next-steps"></a>Próximas etapas

**Quer apenas experimentar as novidades?**  Comece rapidamente em [Início rápido do SQL Server habilitado para Azure Arc](https://aka.ms/AzureArcSqlServerJumpstart).