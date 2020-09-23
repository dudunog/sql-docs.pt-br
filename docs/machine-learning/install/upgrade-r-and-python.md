---
title: Atualizar runtimes do Python e do R (associação)
description: Atualize os runtimes do Python e do R nos Serviços de Machine Learning do SQL Server ou no SQL Server R Services usando sqlbindr.exe para associação ao Machine Learning Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/17/2020
ms.topic: how-to
author: cawrites
ms.author: chadam
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 63bd14d9229d276966a3e118d097316a3ab58a4f
ms.sourcegitcommit: 5f658b286f56001b055a8898d97e74906516dc99
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009372"
---
# <a name="upgrade-python-and-r-runtime-with-binding-in-sql-server-machine-learning-services"></a>Atualizar os runtimes do Python e do R com a associação nos Serviços de Machine Learning do SQL Server
[!INCLUDE [SQL Server 2016 and 2017](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

Este artigo descreve como usar um processo de instalação chamado **associação** para atualizar os runtimes do R ou do Python no [SQL Server 2016 R Services](../r/sql-server-r-services.md) ou nos [Serviços de Machine Learning do SQL Server 2017](../sql-server-machine-learning-services.md).

> [!IMPORTANT]
> Este artigo descreve um método antigo para atualizar os runtimes do R e do Python, chamado de *associação*. Se você tiver instalado a **CU (Atualização Cumulativa) 14 ou posterior para o SP (Services Pack) 2 do SQL Server 2016** ou a **CU 22 ou posterior para o SQL Server 2017**, confira como [alterar o runtime de linguagem R ou Python padrão para uma versão posterior](change-default-language-runtime-version.md) em vez disso.

Você pode obter as [versões mais recentes do Python e do R](#version-map) por meio da *associação* ao Microsoft Machine Learning Server. A versão se aplica aos Serviços de Machine Learning do SQL Server (no banco de dados) e aos SQL Server R Services (no banco de dados).

## <a name="what-is-binding"></a>O que é associação?

A associação é um processo de instalação que altera o conteúdo das pastas **R_SERVICES** e **PYTHON_SERVICES** com executáveis, bibliotecas e ferramentas mais recentes do [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index).

Os componentes carregados incluídos com o modelo de serviço foram alterados. As atualizações de serviço correspondem à [Linha do tempo de suporte para Microsoft R Server & Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-servicing-support) no [Ciclo de vida moderno](https://support.microsoft.com/help/30881/modern-lifecycle-policy).

Exceto para versões de componente e atualizações de serviço, a associação não altera os conceitos básicos de sua instalação:

- A integração do Python e do R ainda faz parte de uma instância do mecanismo de banco de dados.
- O licenciamento não foi alterado (nenhum custo adicional vinculado à associação).
- As políticas de suporte do SQL Server ainda são mantidas para o mecanismo de banco de dados.

O restante deste artigo explica o mecanismo de associação e como ele funciona para cada versão do SQL Server.

> [!NOTE]
> A associação aplica-se a somente instâncias no banco de dados que estão associadas a instâncias do SQL Server. Nesse caso, a associação não é necessária para uma instalação autônoma.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**Considerações de associação do SQL Server 2016**

Para clientes do SQL Server 2016 R Services, a associação fornece:

- Pacotes R atualizados.
- Novos pacotes que não fazem parte da instalação original ([MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package))
- [Modelos](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) de machine learning pré-treinados para análise de sentimento e detecção de imagem.

Toda a associação pode ser atualizada a cada nova versão principal e secundária do [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/index).
::: moniker-end

## <a name="version-map"></a>Mapa de versão

As tabelas a seguir são mapas de versão. Cada mapa mostra as versões de pacote entre lançamentos. Você pode examinar os caminhos de atualização ao fazer a associação ao Microsoft Machine Learning Server (anteriormente conhecido como R Server, antes da adição do suporte do Python iniciado no Machine Learning Server 9.2.1).

A associação não garante a versão mais recente do R ou do Anaconda. Ao associar-se ao Microsoft Machine Learning Server, você obtém a versão do R ou Python disponibilizada por meio da Instalação, que pode não ser a versão mais recente disponível na Web.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
[**SQL Server 2016 R Services**](../install/sql-r-services-windows-install.md)

Componente |Versão inicial | [R Server 9.0.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) | [Machine Learning Server 9.2.1](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) | [Machine Learning Server 9.3](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) |
----------|----------------|----------------|--------------|---------|-------|
MRO (Microsoft R Open) pelo R | R 3.2.2     | R 3.3.2   |R 3.3.3   | R 3.4.1  | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | 8.0.3  | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)| n.d. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[modelos pré-treinados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models)| n.d. | 9.0.1 |  9.1 |  9.2.1 |  9.3 |
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| n.d. | 1.0 |  1.0 |  1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | n.d. | 1.0 |  1.0 |  1.0 |  1.0 |
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
[**Serviços de Machine Learning do SQL Server 2017**](../install/sql-machine-learning-services-windows-install.md)

Componente |Versão inicial | Machine Learning Server 9.3 |
----------|----------------|---------|
MRO (Microsoft R Open) pelo R | R 3.3.3 | R 3.4.3 |
[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) |   9.2 |  9.3 |
[MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package) | 9.2  | 9.3|
[sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)| 1.0 |  1.0 |
[olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 1.0 |  1.0 |
Anaconda 4.2 no Python 3.5  | 4.2/3.5.2 | 4.2/3.5.2 |
[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2  | 9.3|
[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2  | 9.3|
[modelos pré-treinados](https://docs.microsoft.com/machine-learning-server/install/microsoftml-install-pretrained-models) | 9.2 | 9.3|
::: moniker-end

## <a name="how-component-upgrade-works"></a>Como funciona a atualização de componentes

As bibliotecas de arquivos executáveis, Python e R são atualizadas quando você associa uma instalação existente do Python e do R ao Machine Learning Server.

A associação é realizada pelo [instalador do Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) quando você executa a Instalação em uma instância do mecanismo de banco de dados do SQL Server existente que tem a integração do Python ou do R. 

A Instalação detecta os recursos existentes e solicita que você se associe novamente ao Machine Learning Server.

Durante a associação, o conteúdo de `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES` e `\PYTHON_SERVICES` é substituído pelos arquivos executáveis e bibliotecas mais recentes de `C:\Program Files\Microsoft\ML Server\R_SERVER` e `\PYTHON_SERVER`.

A associação aplica-se apenas aos recursos do Python e do R. Os pacotes de software livre para Python e R consistem em:

- Anaconda
- Microsoft R Open
- Pacotes proprietários RevoScaleR
- Revoscalepy

A associação não altera o modelo de suporte da instância do mecanismo de banco de dados ou a versão do SQL Server.

A associação é reversível. Você pode reverter para a manutenção do SQL Server [desassociando a instância](#bkmk_Unbind) e reparando a instância do mecanismo de banco de dados do SQL Server.

<a name="bkmk_BindWizard"></a>

## <a name="bind-to-machine-learning-server-using-setup"></a>Fazer a associação ao Machine Learning Server usando a Instalação

Siga as etapas abaixo para associar o SQL Server ao Microsoft Machine Learning Server usando a instalação. 

1. No SSMS, execute `SELECT @@version` para verificar se o servidor atende aos requisitos mínimos de build.

   Para SQL Server 2016 R Services, o mínimo é o [Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276) e a [CU3](https://support.microsoft.com/help/4019916/cumulative-update-3-for-sql-server-2016-sp1).

1. Verifique a versão dos pacotes R base e RevoScaleR para confirmar se as versões existentes são menores do que aquelas pelas quais você planeja substituí-las. 

    ```sql
    EXECUTE sp_execute_external_script
    @language=N'R'
    ,@script = N'str(OutputDataSet);
    packagematrix <- installed.packages();
    Name <- packagematrix[,1];
    Version <- packagematrix[,3];
    OutputDataSet <- data.frame(Name, Version);'
    , @input_data_1 = N''
    WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
    ```

1. Feche o SSMS e outras ferramentas que têm uma conexão aberta com o SQL Server. A associação substitui arquivos de programa. Se o SQL Server tiver sessões abertas, a associação falhará com o código de erro de associação 6.

1. Baixe o Microsoft Machine Learning Server para o computador que tem a instância que você deseja atualizar. Recomendamos a [versão mais recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer).

1. Descompacte a pasta e inicie ServerSetup.exe, localizado em MLSWIN93.

1. Em **Configurar a instalação**, confirme os componentes a serem atualizados e examine a lista de instâncias compatíveis.

1. Na página **Contrato de licença**, selecione **Aceito esses termos** para aceitar os termos de licenciamento do Machine Learning Server. 

1. Em páginas sucessivas, forneça consentimento para condições de licenciamento adicionais para componentes de software livre selecionados, como o Microsoft R Open ou a distribuição Python Anaconda.

1. Na página **Quase lá**, anote a pasta de instalação. A pasta padrão é \Arquivos de Programas\Microsoft\ML Server.

    Se desejar alterar a pasta de instalação, clique em **Avançado** para voltar para a primeira página do assistente. No entanto, você deve repetir todas as seleções anteriores.

Se a atualização falhar, verifique os [códigos de erro do SqlBindR](#sqlbindr-error-codes) para obter mais informações.

## <a name="offline-binding-no-internet-access"></a>Associação offline (sem acesso à Internet)

Para sistemas sem conectividade com a Internet, você pode baixar o instalador e os arquivos .cab para um computador conectado à Internet e transferir os arquivos para o servidor isolado.

O instalador (ServerSetup.exe) inclui os pacotes da Microsoft (RevoScaleR, MicrosoftML, olapR, sqlRUtils). Os arquivos .cab fornecem outros componentes principais. Por exemplo, o cab “SRO” fornece o R Open, a distribuição do R de software livre da Microsoft.

As instruções a seguir explicam como inserir os arquivos para uma instalação offline.

1. Baixe o instalador do MLSWIN93. Ele é baixado como um arquivo compactado único. Recomendamos a [versão mais recente](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install#download-machine-learning-server-installer), mas você também pode instalar [versões anteriores](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components).

1. Baixe os arquivos .cab. Os links a seguir são para a versão 9.3. Se você precisar de versões anteriores, poderão ser encontrados links adicionais no [R Server 9.1](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows-offline#download-required-components). Lembre-se de que o Python/Anaconda só podem ser adicionados a uma instância dos Serviços de Machine Learning do SQL Server. Há modelos pré-treinados para o Python e o R; o .cab fornece modelos nas linguagens que você está usando.

    | Recurso | Baixar |
    |---------|----------|
    | R       | [SRO_3.4.3.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=867186&clcid=1033) |
    | Python  | [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054) | 
    | Modelos previamente treinados | [MLM_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859053) |

1. Transfira arquivos .zip e .cab para o servidor de destino.

1. No servidor, digite `%temp%` em Executar comando para obter a localização física do diretório temporário. O caminho físico varia de acordo com o computador, mas geralmente é `C:\Users\<your-user-name>\AppData\Local\Temp`.

1. Coloque os arquivos .cab na pasta %temp%.

1. Descompacte o Instalador.

1. Execute ServerSetup.exe e siga os prompts na tela para concluir a instalação.

## <a name="command-line-operations"></a><a name="bkmk_BindCmd"></a>Operações de linha de comando


> [!TIP]
> Não é possível localizar o SqlBindR? Você provavelmente não executou a Instalação.
> O SqlBindR está disponível somente após executar a Instalação do Machine Learning Server.

1. Abra um prompt de comando como administrador e navegue até a pasta que contém sqlbindr.exe. A localização padrão é C:\Arquivos de Programas\Microsoft\MLServer\Setup

2. Digite o seguinte comando para exibir uma lista das instâncias disponíveis: `SqlBindR.exe /list`
  
   Tome nota do nome completo da instância conforme listado. Por exemplo, o nome da instância pode ser MSSQL14.MSSQLSERVER para uma instância padrão ou algo como SERVERNAME.MYNAMEDINSTANCE.

3. Execute o comando **sqlbindr.exe** com o argumento */bind*. Especifique o nome da instância a ser atualizada, usando o nome de instância retornado na etapa anterior.

   Por exemplo, para atualizar a instância padrão, digite: `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. Quando a atualização tiver sido concluída, reinicie o serviço Launchpad associado a qualquer instância que foi modificada.

## <a name="revert-or-unbind-an-instance"></a><a name="bkmk_Unbind"></a>Reverter ou desassociar uma instância

Você pode restaurar uma instância associada para uma instalação inicial dos componentes do Python e do R, estabelecida pela Instalação do SQL Server. Há três partes para reverter para os serviços do SQL Server.

+ [Etapa 1: Desassociar-se do Microsoft Machine Learning Server](#step-1-unbind)
+ [Etapa 2: Restaurar a instância para o status original](#step-2-restore)
+ [Etapa 3: Reinstalar pacotes que você adicionou à instalação](#step-3-reinstall-packages)

<a name="step-1-unbind"></a> 

### <a name="step-1-unbind"></a>Etapa 1: Desassociar

Há duas opções para reverter a associação: executar novamente a instalação ou usar o utilitário de linha de comando do SqlBindR.

#### <a name="unbind-using-setup"></a><a name="bkmk_wizunbind"></a> Desassociar usando a Instalação

1. Localize o instalador para o Machine Learning Server. Se você removeu o instalador, pode ser necessário baixá-lo novamente ou copiá-lo de outro computador.
2. Execute o instalador no computador que tem a instância que você deseja desassociar.
2. O instalador identifica as instâncias locais que são candidatas à desassociação.
3. Desmarque a caixa de seleção ao lado da instância que você deseja reverter para a configuração original.
4. Aceite todos os contratos de licença.
5. Clique em **Concluir**. O processo leva algum tempo.

#### <a name="unbind-using-the-command-line"></a><a name="bkmk_cmdunbind"></a> Desassociar usando a linha de comando

1. Abra um prompt de comando e navegue até a pasta que contém **sqlbindr.exe**, conforme descrito na seção anterior.

2. Execute o comando **SqlBindR.exe** com o argumento */unbind* e especifique a instância.

   Por exemplo, o comando a seguir reverte a instância padrão:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

<a name="step-2-restore"></a> 

###  <a name="step-2-repair-the-sql-server-instance"></a>Etapa 2: Reparar a instância do SQL Server

Execute a Instalação do SQL Server para reparar a instância do mecanismo de banco de dados que tem os recursos do Python e do R. As atualizações já existentes são preservadas. A próxima etapa se aplicará se tiver sido perdida uma das atualizações de serviço nos pacotes Python e R.

Solução alternativa: desinstalar totalmente e reinstalar a instância do mecanismo de banco de dados, depois aplicar todas as atualizações de serviço.

<a name="step-3-reinstall-packages"></a> 

### <a name="step-3-add-any-third-party-packages"></a>Etapa 3: Adicionar pacotes de terceiros

Você pode ter adicionado outros pacotes de software livre ou de terceiros à sua biblioteca de pacotes. Já que reverter a associação alterna o local da biblioteca de pacotes padrão, você deve instalar novamente os pacotes na biblioteca que o Python e o R estão usando agora. Para obter mais informações, confira [Informações sobre pacotes do R](../package-management/r-package-information.md) e [instalação](../package-management/install-additional-r-packages-on-sql-server.md) e [Informações sobre pacotes do Python](../package-management/python-package-information.md) e [instalação](../package-management/install-additional-python-packages-on-sql-server.md).

## <a name="sqlbindrexe-command-syntax"></a>Sintaxe de comando do SqlBindR.exe

### <a name="usage"></a>Uso

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>Parâmetros

|Nome|Descrição|
|------|------|
|*list*| Exibe uma lista de todas as IDs de instância do SQL Server no computador atual|
|*bind*| Atualiza a instância do SQL Server especificada para a última versão do R Server e garante que a instância obtenha automaticamente as atualizações futuras do R Server|
|*unbind*|Desinstala a última versão do R Server da instância do SQL Server especificada e impede que atualizações futuras do R Server afetem a instância|

<a name="sqlbindr-error-codes"><a/>

## <a name="binding-errors"></a>Erros de associação

O Instalador do Machine Learning Server e o SqlBindR retornam os códigos de erro e mensagens a seguir.

|Código do erro  | Mensagem           | Detalhes               |
|------------|-------------------|-----------------------|
|Erro de associação 0 | Ok (êxito) | Associação aprovada sem erros. |
|Erro de associação 1 | Argumentos inválidos | Erro de sintaxe. |
|Erro de associação 2 | Ação inválida | Erro de sintaxe. |
|Erro de associação 3 | Instância inválida | Existe uma instância, mas não é válida para associação. |
|Erro de associação 4 | Não associável | |
|Erro de associação 5 | Já associado | Você executou o comando *bind* , mas a instância especificada já está associada. |
|Erro de associação 6 | Falha na associação | Ocorreu um erro ao desassociar a instância. Esse erro poderá ocorrer se você tiver executado o instalador do Machine Learning Server sem selecionar nenhum recurso. A associação requer que você selecione uma instância do MSSQL e o Python e o R, supondo que a instância seja o SQL Server 2017. Esse erro também poderá ocorrer se o SqlBindR não puder ser gravado na pasta Arquivos de Programas. Sessões ou identificadores abertos para o SQL Server gerarão esse erro. Se você receber esse erro, reinicialize o computador e refaça as etapas de associação antes de iniciar novas sessões.|
|Erro de associação 7 | Não associado | A instância do mecanismo de banco de dados tem os R Services ou os Serviços de Machine Learning do SQL Server. A instância não está associada ao Microsoft Machine Learning Server. |
|Erro de associação 8 | Falha na desassociação | Ocorreu um erro ao desassociar a instância. |
|Erro de associação 9 | Nenhuma instância encontrada | Nenhuma instância do mecanismo de banco de dados foi encontrada neste computador. |

## <a name="known-issues"></a>Problemas conhecidos

Esta seção lista problemas conhecidos para o uso do utilitário SqlBindR.exe ou para atualizações do Machine Learning Server que podem afetar as instâncias do SQL Server.

### <a name="restoring-packages-that-were-previously-installed"></a>Restaurar pacotes que foram instalados anteriormente

O sqlbinder.exe falha ao restaurar os pacotes originais ou os componentes do R com a atualização para o Microsoft R Server 9.0.1. Use o reparo do SQL Server na instância e aplique todas as versões de serviço. Reinicie a instância.

A versão mais recente do SqlBindR restaura automaticamente os recursos originais do R, acabando com a necessidade de reinstalar os componentes do R ou aplicar patch novamente no servidor. No entanto, você deve instalar as atualizações de pacote do R que podem ter sido adicionadas após a instalação inicial.

Use comandos do R para sincronizar pacotes instalados no sistema de arquivos usando os registros no banco de dados. Para obter mais informações, confira [Gerenciamento de Pacotes do R para o SQL Server](https://docs.microsoft.com/sql/machine-learning/package-management/install-additional-r-packages-on-sql-server).

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>Problemas com várias atualizações do SQL Server

Cenário: Instância atualizada anteriormente do SQL Server 2016 R Services para o 9.0.1. Foi executado o novo instalador para o Microsoft R Server 9.1.0. O instalador exibe uma lista de todas as instâncias válidas.
Por padrão, o instalador seleciona as instâncias associadas anteriormente. Se você continuar, as instâncias associadas anteriormente serão desassociadas. O resultado é a remoção da instalação anterior da versão 9.0.1 e de todos os pacotes relacionados, mas a nova versão do Microsoft R Server (9.1.0) não é instalada.

Como uma alternativa, você pode modificar a instalação existente do R Server da seguinte maneira:
1. No Painel de Controle, abra **Adicionar ou Remover Programas**.
2. Localize o Microsoft R Server e clique em **Alterar/Modificar**.
3. Quando o instalador for iniciado, selecione as instâncias que deseja associar à versão 9.1.0.

O Microsoft Machine Learning Server 9.2.1 e 9.3 não têm esse problema.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>A associação ou a desassociação deixa várias pastas temporárias

Remova as pastas temporárias após a conclusão da instalação.

> [!NOTE]
> Aguarde até que a instalação seja concluída. Pode demorar um pouco para remover bibliotecas do R associadas a uma versão e adicionar as novas bibliotecas do R. Quando a operação for concluída, as pastas temporárias serão removidas.

## <a name="see-also"></a>Confira também

+ [Instalar o Machine Learning Server para Windows (conectado à Internet)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Instalar o Machine Learning Server para Windows (offline)](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)
+ [Problemas Conhecidos no Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues)
+ [Anúncios de recursos de uma versão anterior do R Server](https://docs.microsoft.com/r-server/whats-new-in-r-server)
+ [Recursos preteridos, que não têm mais suporte ou alterados](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
