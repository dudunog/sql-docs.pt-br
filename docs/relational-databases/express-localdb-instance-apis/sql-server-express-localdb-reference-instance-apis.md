---
description: Referência de LocalDB do SQL Server Express – APIs da instância
title: Referência da API da instância LocalDB do SQL Server Express | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: faec46da-0536-4de3-96f3-83e607c8a8b6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 892ccbc66070e7ef0d198daba60698502ee3bd0f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541176"
---
# <a name="sql-server-express-localdb-reference---instance-apis"></a>Referência de LocalDB do SQL Server Express – APIs da instância
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  No mundo do SQL Server tradicional baseado em serviço, as instâncias individuais do SQL Server instaladas em um único computador são separadas fisicamente; ou seja, cada instância deve ser instalada e removida separadamente, ter um conjunto separado de binários e ser executada em um processo de serviço separado. O nome da instância do SQL Server é usado para especificar a qual instância do SQL Server o usuário deseja se conectar.  
  
 A API da instância LocalDB do SQL Server Express usa um modelo de instância "leve" simplificado. Embora as instâncias de LocalDB individuais estejam separadas no disco e no Registro, elas usam o mesmo conjunto de binários de LocalDB compartilhados. Além disso, o LocalDB não usa serviços; as instâncias de LocalDB são iniciadas sob demanda através das chamadas de API da instância de LocalDB. No LocalDB, o nome de instância é usado para especificar com qual das instâncias de LocalDB o usuário deseja trabalhar.  
  
 Uma instância de LocalDB sempre é de propriedade de um único usuário e é visível e acessível somente do contexto desse usuário, a menos que o compartilhamento de instância esteja habilitado.  
  
 Embora, tecnicamente, as instâncias de LocalDB não sejam iguais às instâncias tradicionais do SQL Server, seu uso pretendido é similar. Elas são chamadas de *instâncias* para enfatizar essa similaridade e torná-las mais intuitivas para SQL Server usuários.  
  
 O LocalDB oferece suporte a dois tipos de instâncias: AI (instâncias automáticas) e NI (instâncias nomeadas). O identificador de uma instância de LocalDB é o nome da instância.  
  
## <a name="automatic-localdb-instances"></a>Instâncias automáticas de LocalDB  
 As instâncias automáticas de LocalDB são "públicas"; Eles são criados e gerenciados automaticamente para o usuário e podem ser usados por qualquer aplicativo. Existe uma instância de LocalDB automática para cada versão do LocalDB instalada no computador do usuário.  
  
 As instâncias automáticas de LocalDB fornecem gerenciamento de instância contínuo. O usuário não precisa criar a instância. Isso permite que os usuários instalem facilmente os aplicativos e migrem para computadores diferentes. Se o computador de destino tiver a versão especificada de LocalDB instalada, a instância automática de LocalDB para essa versão também estará disponível nesse computador.  
  
### <a name="automatic-instance-management"></a>Gerenciamento automático de instância  
 Um usuário não precisa criar uma instância automática de LocalDB. A instância é criada lentamente na primeira vez em que a instância é usada, desde que a versão especificada do LocalDB esteja disponível no computador do usuário. Do ponto de vista do usuário, a instância automática sempre estará presente se os binários LocalDB estiverem presentes.  
  
 Outras operações de gerenciamento de instância, como Excluir, Compartilhar e Descompartilhar, também funcionam para instâncias automáticas. Em particular, a exclusão de uma instância automática redefine a instância, que será recriada na próxima operação Iniciar. A exclusão de uma instância automática possivelmente será necessária se os bancos de dados do sistema forem danificados.  
  
### <a name="automatic-instance-naming-rules"></a>Regras de nomeação de instância automática  
 As instâncias automáticas de LocalDB têm um padrão especial para o nome de instância que pertence a um namespace reservado. Isso é necessário para impedir conflitos de nomes com instâncias de LocalDB nomeadas.  
  
 O nome de instância automática é o número de versão de linha de base LocalDB precedido por um único caractere "v". Isso se parece com "v" mais dois números com um ponto entre eles; por exemplo, v 11.0 ou V 12,00.  
  
 Exemplos de nomes de instância automática ilegais:  
  
-   11,0 (falta o caractere "v" no início)  
  
-   v11 (sem um ponto e o segundo número da versão)  
  
-   v11. (sem o segundo número da versão)  
  
-   v11.0.1.2 (o número de versão tem mais de duas partes)  
  
## <a name="named-localdb-instances"></a>Instancias de LocalDB nomeadas  
 As instâncias nomeadas LocalDB são "privadas"; uma instância pertence a um único aplicativo que é responsável por criar e gerenciar a instância. As instâncias de LocalDB nomeadas fornecem isolamento e melhoram o desempenho.  
  
### <a name="named-instance-creation"></a>Criação da instância nomeada  
 O usuário deve criar as instâncias nomeadas explicitamente através da API de gerenciamento de LocalDB ou implicitamente através do arquivo app.config de um aplicativo gerenciado. Um aplicativo gerenciado também pode usar a API.  
  
 Cada instância nomeada tem uma versão de LocalDB associada; ou seja, ela indica um conjunto especificado de binários de LocalDB. A versão da instância nomeada é definida durante o processo de criação de instância.  
  
### <a name="named-instance-naming-rules"></a>Regras de nomeação de instância nomeada  
 Um nome de instância de LocalDB pode ter até um total de 128 caracteres (o limite é imposto pelo tipo de dados **sysname** ). Essa é uma diferença significativa se comparada aos nomes de instância tradicionais do SQL Server, que são limitados aos nomes NetBIOS de 16 caracteres ASCII. A razão para essa diferença é que o LocalDB trata os bancos de dados como arquivos e, portanto, implica a semântica baseada em arquivo, portanto, é intuitivo para os usuários terem mais liberdade na escolha de nomes de instância.  
  
 Um nome de instância de LocalDB pode conter qualquer caractere Unicode que seja legal no componente de nome de arquivo. Caracteres ilegais em um componente filename geralmente incluem os seguintes caracteres: caracteres ASCII/Unicode de 1 a 31, bem como aspas ("), menor que ( \<), greater than (> ), pipe (|), backspace (\b), tabulação (\t), dois-pontos (:), asterisco (*), ponto de interrogação (?), barra invertida ( \\ ) e barra (/) Observe que o caractere nulo (\0) é permitido porque é usado na terminação de cadeias de caracteres; tudo o que aparecer após o primeiro caractere nulo será ignorado.  
  
> [!NOTE]  
>  A lista de caracteres ilegais possivelmente dependerá do sistema operacional e mudará nas versões futuras.  
  
 Os espaços em branco à esquerda e à direita nos nomes de instância serão ignorados e cortados.  
  
 Para evitar conflitos de nomenclatura, as instâncias nomeadas LocalDB não podem ter um nome que siga o padrão de nomenclatura para instâncias automáticas, conforme descrito anteriormente em "regras de nomenclatura de instância automática". Uma tentativa de criar uma instância nomeada com um nome que segue o padrão de nomeação de instância automática cria efetivamente uma instância padrão.  
  
## <a name="sql-server-express-localdb-reference-topics"></a>Tópicos de referência de LocalDB do SQL Server Express  
 [Cabeçalho e informações de versão de LocalDB do SQL Server Express](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
 Fornece informações do arquivo de cabeçalho e chaves do Registro para localizar a API de instância de LocalDB.  
  
 [Ferramenta de gerenciamento da linha de comando: SqlLocalDB.exe](../../relational-databases/express-localdb-instance-apis/command-line-management-tool-sqllocaldb-exe.md)  
 Descreve o SqlLocalDB.exe, uma ferramenta para gerenciar instâncias de LocalDB na linha de comando.  
  
 [Função LocalDBCreateInstance](../../relational-databases/express-localdb-instance-apis/localdbcreateinstance-function.md)  
 Descreve a função que cria uma nova instância de LocalDB.  
  
 [Função LocalDBDeleteInstance](../../relational-databases/express-localdb-instance-apis/localdbdeleteinstance-function.md)  
 Descreve a função que remove uma instância de LocalDB.  
  
 [Função LocalDBFormatMessage](../../relational-databases/express-localdb-instance-apis/localdbformatmessage-function.md)  
 Descreve a função que retorna a descrição localizada de um erro de LocalDB.  
  
 [Função LocalDBGetInstanceInfo](../../relational-databases/express-localdb-instance-apis/localdbgetinstanceinfo-function.md)  
 Descreve a função que obtém informações sobre uma instância de LocalDB; por exemplo, se ela existe, as informações da versão, se ela está em execução etc.  
  
 [Função LocalDBGetInstances](../../relational-databases/express-localdb-instance-apis/localdbgetinstances-function.md)  
 Descreve a função que retorna todas as instância de LocalDB com uma versão especificada.  
  
 [Função LocalDBGetVersionInfo](../../relational-databases/express-localdb-instance-apis/localdbgetversioninfo-function.md)  
 Descreve a função que retorna informações sobre uma versão de LocalDB especificada.  
  
 [Função LocalDBGetVersions](../../relational-databases/express-localdb-instance-apis/localdbgetversions-function.md)  
 Descreve a função que retorna todas as versões de LocalDB disponíveis em um computador.  
  
 [Função LocalDBShareInstance](../../relational-databases/express-localdb-instance-apis/localdbshareinstance-function.md)  
 Descreve a função que compartilha uma instância de LocalDB especificada.  
  
 [Função LocalDBStartInstance](../../relational-databases/express-localdb-instance-apis/localdbstartinstance-function.md)  
 Descreve a função que inicia uma instância de LocalDB especificada.  
  
 [Função LocalDBStartTracing](../../relational-databases/express-localdb-instance-apis/localdbstarttracing-function.md)  
 Descreve a função que habilitar o rastreamento de API para um usuário.  
  
 [Função LocalDBStopInstance](../../relational-databases/express-localdb-instance-apis/localdbstopinstance-function.md)  
 Descreve a função que interrompe a execução de uma instância de LocalDB especificada.  
  
 [Função LocalDBStopTracing](../../relational-databases/express-localdb-instance-apis/localdbstoptracing-function.md)  
 Descreve a função que desabilita o rastramento de API para um usuário.  
  
 [Função LocalDBUnshareInstance](../../relational-databases/express-localdb-instance-apis/localdbunshareinstance-function.md)  
 Descreve a função que interrompe o compartilhamento de uma instância de LocalDB especificada.  
  
  
