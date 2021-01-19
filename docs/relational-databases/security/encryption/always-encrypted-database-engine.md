---
title: Always Encrypted | Microsoft Docs
description: Visão geral do Always Encrypted que dá suporte à criptografia transparente do lado do cliente e à computação confidencial no SQL Server e no Banco de Dados SQL do Azure
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], Always Encrypted
- Always Encrypted
- TCE Always Encrypted
- Always Encrypted, about
- SQL13.SWB.COLUMNMASTERKEY.CLEANUP.F1
ms.assetid: 54757c91-615b-468f-814b-87e5376a960f
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 534d7238316fe2037ea0ce43e2b4aeeb11e6eea2
ms.sourcegitcommit: f29f74e04ba9c4d72b9bcc292490f3c076227f7c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98171328"
---
# <a name="always-encrypted"></a>Always Encrypted
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

  ![Always Encrypted](../../../relational-databases/security/encryption/media/always-encrypted.png "Always Encrypted")  
  
 O Always Encrypted é um recurso criado para proteger dados confidenciais, como números de cartão de crédito ou de identificação nacional (por exemplo, números de previdência social dos EUA), armazenados em bancos de dados do [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)] ou [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O Always Encrypted permite que os clientes criptografem os dados confidenciais em aplicativos de cliente e nunca revelem as chaves de criptografia para o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] ([!INCLUDE[ssSDS](../../../includes/sssds-md.md)] ou [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]). Como resultado, o Always Encrypted fornece uma separação entre aqueles que detêm os dados e podem exibi-lo e aqueles que gerenciam os dados, mas que não devem ter acesso. Ao garantir que os administradores de banco de dados local, operadores de banco de dados em nuvem ou outros usuários não autorizados com privilégios elevados não possam acessar os dados criptografados, o Always Encrypted permite que os clientes armazenem dados confidenciais com segurança fora de seu controle direto. Isso permite às organizações armazenar seus dados no Azure para habilitar a delegação de administração de banco de dados local para terceiros ou para reduzir os requisitos de espaço livre de segurança para sua própria equipe de DBA.

 O Always Encrypted fornece recursos de computação confidencial, permitindo que o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] processe algumas consultas em dados criptografados, preservando a confidencialidade dos dados e proporcionando os benefícios de segurança acima. Em [!INCLUDE[ssSQL15](../../../includes/sssql16-md.md)], [!INCLUDE[sssSQLv14](../../../includes/sssqlv14-md.md)] e [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)], o Always Encrypted dá suporte à comparação de igualdade por meio de criptografia determinística. Confira [Como selecionar criptografia determinística ou randomizada](#selecting--deterministic-or-randomized-encryption). 

  > [!NOTE] 
  > Em [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], os enclaves seguros estendem substancialmente os recursos de computação confidencial do Always Encrypted com correspondência de padrões, outros operadores de comparação e criptografia in-loco. Veja [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md).

 O Always Encrypted torna a criptografia transparente para os aplicativos. Um driver habilitado para Sempre criptografado instalado no computador cliente realiza isso automaticamente criptografando e descriptografando dados confidenciais no aplicativo cliente. O driver criptografa as colunas de dados confidenciais antes de passar os dados para o [!INCLUDE[ssDE](../../../includes/ssde-md.md)]e reconfigura automaticamente as consultas para que a semântica do aplicativo seja preservada. Da mesma forma, o driver descriptografa os dados de maneira transparente, armazenados em colunas de banco de dados criptografadas, contidas nos resultados da consulta.  
  
 O Always Encrypted está disponível em todas as edições do [!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)], começando com [!INCLUDE[ssSQL15](../../../includes/sssql16-md.md)] e todas as camadas de serviço do [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]. (Antes do [!INCLUDE[ssSQL15_md](../../../includes/sssql16-md.md)] SP1, o Always Encrypted limitava-se à versão Enterprise Edition). Para conferir uma apresentação do Channel 9 que inclui o Sempre Criptografado, confira [Keeping Sensitive Data Secure with Always Encrypted](https://channel9.msdn.com/events/DataDriven/SQLServer2016/AlwaysEncrypted)(Como manter os dados confidenciais seguros com o Sempre Criptografado).  

  
## <a name="typical-scenarios"></a>Cenários comuns  
  
### <a name="client-and-data-on-premises"></a>Cliente e dados locais  
 Um cliente tem um aplicativo cliente e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , ambos sendo executados localmente na empresa. O cliente deseja contratar um fornecedor externo para administrar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para proteger os dados confidenciais armazenados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o cliente usa o Always Encrypted para garantir a separação de tarefas entre os administradores de banco de dados e os administradores de aplicativos. O cliente armazena valores de texto não criptografado de chaves do Always Encrypted em um repositório de chaves confiável que o aplicativo cliente pode acessar. Os administradores do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não têm acesso às chaves e, portanto, não são capazes de descriptografar dados confidenciais armazenados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
### <a name="client-on-premises-with-data-in-azure"></a>Cliente local contendo dados no Azure  
 Um cliente tem um aplicativo local na empresa. O aplicativo opera com dados confidenciais armazenados em um banco de dados hospedado no Azure ([!INCLUDE[ssSDS](../../../includes/sssds-md.md)] ou [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em execução em uma máquina virtual no Microsoft Azure). O cliente usa o Always Encrypted e armazena as chaves do Always Encrypted em um repositório de chaves confiável hospedado localmente, a fim de garantir que os administradores de nuvem da [!INCLUDE[msCoName](../../../includes/msconame-md.md)] não tenham acesso a dados confidenciais.  
  
### <a name="client-and-data-in-azure"></a>Cliente e dados no Azure  
 Um cliente tem um aplicativo cliente, hospedado no Microsoft Azure (por exemplo, em uma função de trabalho ou uma função web), que opera em dados confidenciais armazenados em um banco de dados hospedado no Azure (Banco de Dados SQL ou SQL Server em execução em uma máquina virtual no Microsoft Azure). Embora o Always Encrypted não forneça isolamento completo dos dados dos administradores de nuvem, como ambos os dados e chaves ficam expostos para os administradores da nuvem da plataforma de hospedagem no nível do cliente, o cliente ainda se beneficia com a redução da área de superfície de ataque à segurança (os dados são Always Encrypted no banco de dados).  
 
## <a name="how-it-works"></a>Como funciona

Você pode configurar o Always Encrypted para colunas individuais do banco de dados contendo dados confidenciais. Ao configurar a criptografia para uma coluna, você pode especificar as informações do algoritmo de criptografia e chaves de criptografia usadas para proteger os dados na coluna. O Always Encrypted usa dois tipos de chave: chaves de criptografia de coluna e chaves mestras de coluna. Uma chave de criptografia de coluna é usada para criptografar dados em uma coluna criptografada. Uma chave mestra de coluna é uma chave de proteção de chaves que criptografa uma ou mais chaves de criptografia de coluna. 

O Mecanismo de Banco de Dados armazena a configuração de criptografia para cada coluna nos metadados do banco de dados. Observe, no entanto, que o Mecanismo de Banco de Dados nunca armazena ou usa as chaves de qualquer tipo em texto não criptografado. Ele apenas armazena os valores criptografados das chaves de criptografia de coluna e as informações sobre o local das chaves mestras de coluna, as quais são armazenadas em repositórios de chaves confiáveis externos, como o Cofre de Chaves do Azure, o Repositório de Certificados do Windows em um computador cliente ou um módulo de segurança de hardware.

Para acessar dados armazenados em uma coluna criptografada em texto não criptografado, um aplicativo deve usar um driver de cliente habilitado para Always Encrypted. Quando um aplicativo emite uma consulta parametrizada, o driver colabora de modo transparente com o Mecanismo de Banco de Dados para determinar quais parâmetros de destino de colunas criptografadas e, portanto, devem ser criptografados. Para cada parâmetro que precisa ser criptografado, o driver obtém as informações sobre o algoritmo de criptografia e o valor criptografado da chave de criptografia de coluna para a coluna, as metas de parâmetro, bem como o local da chave mestra de coluna correspondente.

Em seguida, o driver contata o repositório de chaves que contém a chave mestra de coluna para descriptografar o valor da chave de criptografia de coluna criptografada e usa a chave de criptografia da coluna de texto não criptografado para criptografar o parâmetro. A chave de criptografia de coluna de texto não criptografado resultante é armazenado em cache para reduzir o número de idas e voltas para o repositório de chaves em usos subsequentes da mesma chave de criptografia de coluna. O driver substitui os valores de texto não criptografado dos parâmetros de direcionamento colunas criptografadas com seus valores criptografados e envia a consulta para o servidor para processamento.

O servidor calcula o conjunto de resultados e, para as colunas criptografadas incluídas no conjunto de resultados, o driver anexa os metadados de criptografia da coluna, incluindo as informações sobre o algoritmo de criptografia e as chaves correspondentes. O driver primeiro tentará encontrar a chave de criptografia da coluna de texto não criptografado no cache local e fará apenas uma rodada para a chave mestra de coluna se não for possível encontrar a chave no cache. Em seguida, o driver descriptografa os resultados e retorna valores de texto não criptografado para o aplicativo.

 Um driver cliente interage com um repositório de chaves que contém uma chave mestra de coluna usando um provedor de repositório de chaves mestras de coluna, que é um componente de software do cliente que encapsula um repositório de chaves que contém a chave mestra de coluna. Os provedores para tipos comuns de repositório de chaves estão disponíveis em bibliotecas de drivers do lado do cliente da Microsoft ou como um download autônomo. Você também pode implementar seu próprio provedor. Recursos Always Encrypted, incluindo provedores de repositório de chaves mestras de coluna internas, variam de acordo com uma biblioteca de drivers e sua versão. 

Para obter detalhes sobre como desenvolver aplicativos usando Always Encrypted com drivers cliente específicos, confira [Desenvolver aplicativos usando Always Encrypted](always-encrypted-client-development.md).

## <a name="remarks"></a>Comentários

A criptografia e a descriptografia ocorrem por meio do driver do cliente. Isso significa que algumas ações que ocorrem somente no servidor não funcionarão ao usar Always Encrypted. Os exemplos incluem a cópia de dados de uma coluna para outra por meio de UPDATE, BULK INSERT(T-SQL), SELECT INTO, INSERT..SELECT. 

Aqui está um exemplo de uma ATUALIZAÇÃO que tenta mover dados de uma coluna criptografada para uma coluna não criptografada sem retornar um conjunto de resultados para o cliente: 

```sql
update dbo.Patients set testssn = SSN
```

Se o SSN for uma coluna criptografada usando Always Encrypted, a instrução de atualização acima falhará com um erro semelhante a:

```
Msg 206, Level 16, State 2, Line 89
Operand type clash: char(11) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_1', column_encryption_key_database_name = 'ssn') collation_name = 'Latin1_General_BIN2' is incompatible with char
```

Para atualizar com êxito a coluna, faça o seguinte:

1. SELECIONE os dados fora da coluna SSN e armazene-os como um conjunto de resultados no aplicativo. Isso permitirá que o aplicativo (*driver* do cliente) descriptografe a coluna.
2. INSIRA os dados do conjunto de resultados no SQL Server. 

 >[!IMPORTANT]
 > Nesse cenário, os dados serão descriptografados quando enviados de volta para o servidor porque a coluna de destino é um varchar regular que não aceita dados criptografados. 
  
## <a name="selecting-deterministic-or-randomized-encryption"></a><a name="selecting--deterministic-or-randomized-encryption"></a> Seleção de criptografia determinística ou aleatória  
 O Mecanismo de Banco de dados nunca opera em dados de texto não criptografado armazenados em colunas criptografadas, mas ela ainda dá suporte a algumas consultas em dados criptografados, dependendo do tipo de criptografia para a coluna. O Always Encrypted dá suporte a dois tipos de criptografia: criptografia aleatória e criptografia determinística.  
  
- A criptografia determinística sempre gera o mesmo valor criptografado para qualquer valor de texto sem formatação. Usar a criptografia determinística proporciona pesquisas de ponto, junções de igualdade, agrupamento e indexação em colunas criptografadas. No entanto, ela também pode permitir que usuários não autorizados estimem informações sobre os valores criptografados examinando padrões na coluna criptografada, especialmente se há um conjunto pequeno de valores criptografados possíveis, como Verdadeiro/Falso ou região Norte/Sul/Leste/Oeste. A criptografia determinística deve usar uma ordenação de colunas com uma ordem de classificação binary2 para as colunas de caracteres.

- A criptografia aleatória usa um método que criptografa os dados de uma maneira menos previsível. A criptografia aleatória é mais segura, mas impede o uso de pesquisas, agrupamento, indexação e junção em colunas criptografadas.

Use a criptografia determinística para colunas que serão usadas como parâmetros de pesquisa ou de agrupamento. Por exemplo, um número de ID do governo. Use a criptografia aleatória para dados como comentários de investigação confidencial, que não estão agrupados com outros registros e não são usados para unir tabelas.
Para obter detalhes sobre os algoritmos de criptografia Always Encrypted, confira [Criptografia Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-cryptography.md).

## <a name="configuring-always-encrypted"></a>Configuração Always Encrypted

 A configuração inicial do Always Encrypted em um banco de dados envolve a geração de chaves Always Encrypted, criação de metadados de chave, configurando as propriedades de criptografia de colunas do banco de dados selecionado e/ou criptografar dados que possam existir em colunas que precisam ser criptografados. Observe que algumas dessas tarefas não têm suporte no Transact-SQL e exigem o uso de ferramentas de cliente. Como chaves e dados confidenciais protegidos Always Encrypted nunca são reveladas em texto não criptografado para o servidor, o Mecanismo de Banco de Dados não pode ser envolvidos no provisionamento de chave e na execução de operações de criptografia ou descriptografia de dados. Você pode usar o SQL Server Management Studio ou o PowerShell para realizar essas tarefas. 

|Tarefa|SSMS|PowerShell|T-SQL|
|:---|:---|:---|:---
|Provisionamento de chaves mestras de coluna, chaves de criptografia de coluna e chaves de criptografia de coluna criptografada com suas chaves mestras de coluna correspondentes.|Sim|Sim|Não|
|Criação de metadados de chave no banco de dados.|Sim|Sim|Sim|
|Criando novas tabelas com colunas criptografadas|Sim|Sim|Sim|
|Criptografar os dados existentes nas colunas do banco de dados selecionado|Sim|Sim|Não|

> [!NOTE]
> O [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md), introduzido no [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], dá suporte à criptografia de dados existentes usando Transact-SQL. Ele também elimina a necessidade de mover os dados para fora dos dados para operações criptográficas.

> [!NOTE]
> Lembre-se de executar as ferramentas de provisionamento de chaves ou de criptografia de dados em um ambiente seguro e em um computador diferente daquele que hospeda o banco de dados. Caso contrário, dados confidenciais ou as chaves podem vazar no ambiente de servidor, reduzindo os benefícios de usar o Always Encrypted.  

Para obter detalhes sobre a configuração Always Encrypted, consulte:
- [Configurar Always Encrypted usando SSMS](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)
- [Configurar Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)

## <a name="getting-started-with-always-encrypted"></a>Introdução ao Always Encrypted

Use o [Assistente do Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-wizard.md) para iniciar rapidamente o uso do Always Encrypted. O assistente provisionará as chaves necessárias e configurará a criptografia para colunas selecionadas. Se as colunas para as quais você está definindo a criptografia já contêm alguns dados, o assistente as criptografa. O exemplo a seguir demonstra o processo de criptografia de uma coluna.

> [!NOTE]  
>  Para obter um vídeo que inclui o uso do assistente, confira [Introdução ao Always Encrypted com SSMS](https://channel9.msdn.com/Shows/Data-Exposed/Getting-Started-with-Always-Encrypted-with-SSMS).

1.  Conecte a um banco de dados existente que contém as tabelas com as colunas que você deseja criptografar usando o **Pesquisador de Objetos** do Management Studio ou crie um novo banco de dados, crie uma ou mais tabelas com colunas para criptografar e conecte-se a elas.
2.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas** e clique em **Criptografar Colunas** para abrir o **Assistente do Always Encrypted**.
3.  Examine a página **Introdução** e, em seguida, clique em **Avançar**.
4.  Na página **Seleção de Coluna** , expanda as tabelas e selecione as colunas que você deseja criptografar.
5.  Para cada coluna selecionada para criptografia, defina o **Tipo de Criptografia** como *Determinística* ou *Aleatória*.
6.  Para cada coluna selecionada para criptografia, selecione uma **Chave de Criptografia**. Se você ainda não criou nenhuma chave de criptografia para esse banco de dados, selecione a opção padrão de uma nova chave gerada automaticamente e clique em **Avançar**.
7.  Na página **Configuração da Chave Mestra** , selecione um local para armazenar a nova chave e uma fonte de chave mestra e clique em **Avançar**.
8.  Na página **Validação** , escolha se deseja executar o script imediatamente ou criar um script do PowerShell e, em seguida, clique em **Avançar**.
9.  Na página **Resumo**, examine as opções que você selecionou e clique em **Concluir**. Feche o assistente após a conclusão.

  
## <a name="feature-details"></a>Detalhes do recurso  
  
-   As consultas podem executar uma comparação de igualdade em colunas criptografadas usando a criptografia determinística, mas nenhuma outra operação (por exemplo, maior/menor que, correspondência de padrões usando o operador LIKE ou operações aritméticas).  
  
-   Consultas em colunas criptografadas usando a criptografia aleatória não podem executar operações em qualquer uma dessas colunas. Não há suporte para a indexação de colunas criptografadas usando a criptografia aleatória.  
 > [!NOTE] 
 > [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md), apresentado em [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], aborda a limitação acima, permitindo a correspondência de padrões, operadores de comparação e indexação em colunas usando criptografia aleatória.

-   Uma chave de criptografia de coluna pode ter até dois valores criptografados diferentes, cada um deles criptografado com uma chave mestra de coluna diferente. Isso facilita a rotação da chave mestra de coluna.  
  
-   A criptografia determinística exige que uma coluna tenha uma das [*ordenações* binary2](../../../relational-databases/collations/collation-and-unicode-support.md).  

-   Depois de alterar a definição de um objeto criptografado, execute [sp_refresh_parameter_encryption](../../../relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md) para atualizar os metadados Always Encrypted para o objeto.
  
Não há suporte para o Always Encrypted para as colunas com as características abaixo. Por exemplo, se alguma das condições a seguir se aplicar à coluna, a cláusula `ENCRYPTED WITH` não poderá ser usada em `CREATE TABLE/ALTER TABLE` para uma coluna:  
  
-   Colunas que usam um dos seguintes tipos de dados: `xml`, `timestamp`/`rowversion`, `image`, `ntext`, `text`, `sql_variant`, `hierarchyid`, `geography`, `geometry`, alias, tipos definidos pelo usuário.  
- Colunas `FILESTREAM`  
- Colunas com a propriedade `IDENTITY`.  
- Colunas com propriedade `ROWGUIDCOL`.  
- Colunas de cadeia de caracteres (`varchar`, `char` etc.) com ordenações não bin2.  
- Colunas que são chaves para índices clusterizados e não clusterizados ao usar a criptografia aleatória (há suporte para criptografia determinística).
- Colunas incluídas em índices de texto completo (Always Encrypted não dá suporte à [Pesquisa de Texto Completo](../../../relational-databases/search/full-text-search.md)).  
- Colunas computadas.
- Colunas referenciadas por colunas computadas (quando a expressão realiza operações sem suporte para o Always Encrypted).  
- Conjunto de colunas esparsas.  
- Colunas referenciadas por estatísticas ao usar a criptografia aleatória (há suporte para a criptografia determinística).  
- Colunas que usam os tipos de alias.  
- Colunas de particionamento.  
- Colunas com restrições padrão.  
- Colunas referenciadas por restrições exclusivas ao usar a criptografia aleatória (há suporte para a criptografia determinística).  
- Colunas de chave primária ao usar a criptografia aleatória (há suporte para a criptografia determinística).  
- Fazer referência a colunas em restrições de chave estrangeira ao usar a criptografia aleatória (ou ao usar a criptografia determinística) se as colunas referenciadas e de referência usarem algoritmos ou chaves diferentes.  
- Colunas referenciadas por restrições de verificação.  
- Colunas capturadas/controladas usando a captura de dados de alterações.  
- Colunas de chave primária em tabelas com controle de alterações.  
- Colunas mascaradas (usando a Máscara de Dados Dinâmicos).  
- Colunas em tabelas Stretch Database. (Tabelas com colunas criptografadas com o Sempre Criptografado podem ser habilitadas para Stretch.)  
- Colunas em tabelas externas (PolyBase) (observação: há suporte para o uso de tabelas externas e tabelas com colunas criptografadas na mesma consulta).  
- Não há suporte para parâmetros com valor de tabela com direcionamento a colunas criptografadas.  

As cláusulas a seguir não podem ser usadas para colunas criptografadas:

- `FOR XML`
- `FOR JSON PATH`

Os recursos a seguir não funcionam em colunas criptografadas:

- Replicação transacional ou de mesclagem
- Consultas distribuídas (servidores vinculados, `OPENROWSET`(T-SQL), `OPENDATASOURCE`(T-SQL))

Requisitos da ferramenta

- O SQL Server Management Studio versão 18 ou superior é recomendável para executar consultas que descriptografam os resultados recuperados de colunas criptografadas ou inserem, atualizam ou filtram colunas criptografadas. 
- Requer o `sqlcmd` versão 13.1 ou superior, que está disponível no [Centro de Download](https://go.microsoft.com/fwlink/?LinkID=825643).

  
## <a name="database-permissions"></a>Permissões de banco de dados  
 Há quatro permissões para Always Encrypted:  
  
*  `ALTER ANY COLUMN MASTER KEY` (Necessário para criar e excluir uma chave mestra de coluna).  
  
*  `ALTER ANY COLUMN ENCRYPTION KEY` (Necessário para criar e excluir uma chave de criptografia de coluna). 
  
*  `VIEW ANY COLUMN MASTER KEY DEFINITION` (Necessário para acessar e ler os metadados das chaves mestras de coluna para gerenciar as colunas criptografadas de chaves ou consultas).  
  
*  `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` (Necessário para acessar e ler os metadados da chave de criptografia de coluna para gerenciar as colunas criptografadas de chaves ou consultas).  
  
 A tabela a seguir resume as permissões necessárias para ações comuns.  
  
|Cenário|<code>ALTER ANY COLUMN MASTER KEY</code>|<code>ALTER ANY COLUMN ENCRYPTION KEY</code>|<code>VIEW ANY COLUMN MASTER KEY DEFINITION</code>|<code>VIEW ANY COLUMN ENCRYPTION KEY DEFINITION</code>|  
|--------------|-----------------------------------|---------------------------------------|---------------------------------------------|-------------------------------------------------|  
|Gerenciamento de chaves (criar/alterar/analisar metadados de chave no banco de dados)|X|X|X|X|  
|Consultando colunas criptografadas|||X|X|  
  
 **Observações importantes;**  
  
-   As permissões se aplicam às ações que usam [!INCLUDE[tsql](../../../includes/tsql-md.md)], [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] (caixas de diálogo e assistente) ou o PowerShell.  
  
-   As duas permissões *VIEW* são necessárias ao selecionar colunas criptografadas, mesmo se o usuário não tem permissão para descriptografar as colunas.  
  
-   No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], ambas as permissões *VIEW* são concedidas por padrão para a função de banco de dados fixa `public` . Um administrador de banco de dados poderá revogar (ou negar) as permissões *VIEW* para a função `public` e conceder para funções específicas ou usuários para implementar o controle mais restrito.  
  
-   No [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], as permissões *VIEW* não são concedidas por padrão para a função de banco de dados fixa `public`. Isso permite que determinadas ferramentas existentes herdadas (usando versões anteriores do DacFx) funcionem corretamente. Consequentemente, para trabalhar com colunas criptografadas (mesmo se não descriptografá-los) um administrador de banco de dados deve conceder explicitamente as duas permissões *VIEW* .  

  
## <a name="example"></a>Exemplo  
 O [!INCLUDE[tsql](../../../includes/tsql-md.md)] a seguir cria metadados de chave mestra de coluna, metadados de chave de criptografia de coluna e uma tabela com colunas criptografadas. Para informações sobre como criar chaves, referenciadas nos metadados, consulte:
- [Configurar Always Encrypted usando SSMS](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)
- [Configurar Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)

  
```sql  
CREATE COLUMN MASTER KEY MyCMK  
WITH (  
     KEY_STORE_PROVIDER_NAME = 'MSSQL_CERTIFICATE_STORE',   
     KEY_PATH = 'Current User/Personal/f2260f28d909d21c642a3d8e0b45a830e79a1420'  
   );  
---------------------------------------------  
CREATE COLUMN ENCRYPTION KEY MyCEK   
WITH VALUES  
(  
    COLUMN_MASTER_KEY = MyCMK,   
    ALGORITHM = 'RSA_OAEP',   
    ENCRYPTED_VALUE = 0x01700000016C006F00630061006C006D0061006300680069006E0065002F006D0079002F003200660061006600640038003100320031003400340034006500620031006100320065003000360039003300340038006100350064003400300032003300380065006600620063006300610031006300284FC4316518CF3328A6D9304F65DD2CE387B79D95D077B4156E9ED8683FC0E09FA848275C685373228762B02DF2522AFF6D661782607B4A2275F2F922A5324B392C9D498E4ECFC61B79F0553EE8FB2E5A8635C4DBC0224D5A7F1B136C182DCDE32A00451F1A7AC6B4492067FD0FAC7D3D6F4AB7FC0E86614455DBB2AB37013E0A5B8B5089B180CA36D8B06CDB15E95A7D06E25AACB645D42C85B0B7EA2962BD3080B9A7CDB805C6279FE7DD6941E7EA4C2139E0D4101D8D7891076E70D433A214E82D9030CF1F40C503103075DEEB3D64537D15D244F503C2750CF940B71967F51095BFA51A85D2F764C78704CAB6F015EA87753355367C5C9F66E465C0C66BADEDFDF76FB7E5C21A0D89A2FCCA8595471F8918B1387E055FA0B816E74201CD5C50129D29C015895CD073925B6EA87CAF4A4FAF018C06A3856F5DFB724F42807543F777D82B809232B465D983E6F19DFB572BEA7B61C50154605452A891190FB5A0C4E464862CF5EFAD5E7D91F7D65AA1A78F688E69A1EB098AB42E95C674E234173CD7E0925541AD5AE7CED9A3D12FDFE6EB8EA4F8AAD2629D4F5A18BA3DDCC9CF7F352A892D4BEBDC4A1303F9C683DACD51A237E34B045EBE579A381E26B40DCFBF49EFFA6F65D17F37C6DBA54AA99A65D5573D4EB5BA038E024910A4D36B79A1D4E3C70349DADFF08FD8B4DEE77FDB57F01CB276ED5E676F1EC973154F86  
);  
---------------------------------------------  
CREATE TABLE Customers (  
    CustName nvarchar(60)   
        COLLATE  Latin1_General_BIN2 ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = MyCEK,  
        ENCRYPTION_TYPE = RANDOMIZED,  
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'),   
    SSN varchar(11)   
        COLLATE  Latin1_General_BIN2 ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = MyCEK,  
        ENCRYPTION_TYPE = DETERMINISTIC ,  
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'),   
    Age int NULL  
);  
GO  
  
```  
## <a name="see-also"></a>Consulte Também  
- [Configurar Always Encrypted usando SSMS](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)   
- [Configurar Always Encrypted usando o PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)   
- [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md) 
- [Configurar a criptografia de coluna usando o Assistente do Always Encrypted](always-encrypted-wizard.md)
- [Criptografia Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-cryptography.md)   
- [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-column-master-key-transact-sql.md)   
- [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
- [CREATE TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-table-transact-sql.md)   
- [column_definition &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-column-definition-transact-sql.md)   
- [sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)  
- [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)   
- [sys.column_master_keys &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
- [sys.columns &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
- [sp_refresh_parameter_encryption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md)   
  
  
