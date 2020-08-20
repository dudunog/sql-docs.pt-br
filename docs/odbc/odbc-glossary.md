---
description: Glossário do ODBC
title: Glossário do ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], glossary
- glossary [ODBC]
ms.assetid: e8227000-1944-42e5-a881-1f549e1ff9d1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 57b08d48944ee288b4eba849917828b6fe1d4396
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466248"
---
# <a name="odbc-glossary"></a>Glossário do ODBC
## <a name="a"></a>Um  
 **plano de acesso**  
 Um plano gerado pelo mecanismo de banco de dados para executar uma instrução SQL. Equivalente ao código executável compilado de uma linguagem de terceira geração, como C.  
  
 **função de agregação**  
 Uma função que gera um único valor de um grupo de valores, geralmente usado com as cláusulas **Group by** e **having** . As funções de agregação incluem **AVG**, **Count**, **Max**, **min**e **sum**. Também conhecido como *funções Set*. *Consulte também* função escalar.  
  
 **ANSI**  
 American National Standards Institute. A API ODBC é baseada na interface de nível de chamada ANSI.  
  
 **APD**  
 *Consulte* descritor de parâmetro de aplicativo (APD).  
  
 **API**  
 Interface de programação de aplicativo. Um conjunto de rotinas que um aplicativo usa para solicitar e executar serviços de nível inferior. A API ODBC é composta pelas funções ODBC.  
  
 **aplicativo**  
 Um programa executável que chama funções na API ODBC.  
  
 **descritor de parâmetro de aplicativo (APD)**  
 Um descritor que descreve os parâmetros dinâmicos usados em uma instrução SQL antes de qualquer conversão especificada pelo aplicativo.  
  
 **descritor de linha de aplicativo (ARD)**  
 Um descritor que representa os metadados de coluna e os dados nos buffers do aplicativo, descrevendo uma linha de dados após qualquer conversão de dados especificada pelo aplicativo.  
  
 **ARD**  
 *Consulte* descritor de linha do aplicativo (ARD).  
  
 **modo de confirmação automática**  
 Um modo de confirmação de transação no qual as transações são confirmadas imediatamente após serem executadas.  
  
## <a name="b"></a>B  
 **alteração comportamental**  
 Uma alteração em determinadas funcionalidades do comportamento do ODBC *3. x* para o comportamento do ODBC *2. x* , ou vice-versa. Causado pela alteração do atributo de ambiente SQL_ATTR_ODBC_VERSION.  
  
 **Objeto binário grande (BLOB)**  
 Todos os dados binários em um determinado número de bytes, como 255. Normalmente é muito mais longo. Esses dados são geralmente enviados e recuperados da fonte de dados em partes. Também conhecido como *dados longos*.  
  
 **vinculação**  
 Como um verbo, o ato de associar uma coluna em um conjunto de resultados ou um parâmetro em uma instrução SQL com uma variável de aplicativo. Como um substantivo, a associação.  
  
 **deslocamento de associação**  
 Um valor adicionado aos endereços de buffer de dados e endereços de buffer de comprimento/indicador para todos os dados de coluna ou de parâmetro associados, produzindo novos endereços.  
  
 **cursor em bloco**  
 Um cursor capaz de buscar mais de uma linha de dados de cada vez.  
  
 **completo**  
 Uma parte da memória do aplicativo usada para passar dados entre o aplicativo e o driver. Os buffers geralmente vêm em pares: um *buffer de dados* e um buffer de comprimento de *dados*.  
  
 **byte**  
 Oito bits ou um octeto. *Consulte também* octeto.  
  
## <a name="c"></a>C  
 **Tipos de dados do C**  
 O tipo de dados de uma variável em um programa C, neste caso, o aplicativo.  
  
 **catalog**  
 O conjunto de tabelas do sistema em um banco de dados que descreve a forma do banco de dados. Também conhecido como um *esquema* ou *dicionário de dados*.  
  
 **função de catálogo**  
 Uma função ODBC usada para recuperar informações do catálogo do banco de dados.  
  
 **CLI**  
 *Consulte* API.  
  
 **cliente/servidor**  
 Uma estratégia de acesso ao banco de dados na qual um ou mais clientes acessam os dados por meio de um servidor. Os clientes geralmente implementam a interface do usuário enquanto o servidor controla o acesso ao banco de dados.  
  
 **column**  
 O contêiner de um único item de informações em uma linha. Também conhecido como *campo*.  
  
 **compromisso**  
 Para tornar as alterações em uma transação permanentes.  
  
 **corrente**  
 A capacidade de mais de uma transação acessar os mesmos dados ao mesmo tempo.  
  
 **nível de conformidade**  
 Um conjunto discreto de funcionalidades com suporte por um driver ou uma fonte de dados. O ODBC define os níveis de conformidade da API e os níveis de conformidade do SQL.  
  
 **connection**  
 Uma instância específica de um driver e uma fonte de dados.  
  
 **navegação de conexão**  
 Procurando fontes de dados na rede à qual se conectar. A navegação por conexão pode envolver várias etapas. Por exemplo, o usuário pode primeiro procurar servidores na rede e, em seguida, procurar um determinado servidor em um banco de dados.  
  
 **identificador de conexão**  
 Um identificador para uma estrutura de dados que contém informações sobre uma conexão.  
  
 **linha atual**  
 A linha apontada atualmente pelo cursor. Operações posicionadas atuam na linha atual.  
  
 **cursor**  
 Uma parte do software que retorna linhas de dados para o aplicativo. Provavelmente nomeado após o cursor piscando em um terminal de computador; assim como esse cursor indica a posição atual na tela, um cursor em um conjunto de resultados indica a posição atual no conjunto de resultados.  
  
## <a name="d"></a>D  
 **buffer de dados**  
 Um buffer usado para passar dados. Muitas vezes, associados a um buffer de dados são um *buffer de comprimento de dados*.  
  
 **dicionário de dados**  
 *Consulte* catálogo.  
  
 **buffer de comprimento de dados**  
 Um buffer usado para passar o comprimento do valor em um buffer de *dados*correspondente. O buffer de comprimento de dados também é usado para armazenar indicadores, como se o valor dos dados é encerrado em nulo.  
  
 **fonte de dados**  
 Os dados que o usuário deseja acessar e seu sistema operacional, DBMS e plataforma de rede associados (se houver).  
  
 **tipo de dados**  
 O tipo de um dado. O ODBC define os tipos de dados C e SQL. *Consulte também* indicador de tipo.  
  
 **coluna de dados em execução**  
 Uma coluna para a qual os dados são enviados após a chamada de **SQLSetPos** . Portanto, chamado porque os dados são enviados em tempo de execução em vez de serem colocados em um buffer de conjunto de linhas. Os dados longos geralmente são enviados em partes no momento da execução.  
  
 **parâmetro de dados em execução**  
 Um parâmetro para o qual os dados são enviados após **SQLExecute** ou **SQLExecDirect** é chamado. Portanto, nomeado porque os dados são enviados quando a instrução SQL é executada em vez de ser colocada em um buffer de parâmetros. Os dados longos geralmente são enviados em partes no momento da execução.  
  
 **database**  
 Uma coleção discreta de dados em um DBMS. Também um DBMS.  
  
 **mecanismo de banco de dados**  
 O software em um DBMS que analisa e executa instruções SQL e acessa os dados físicos.  
  
 **DBMS**  
 Sistema de gerenciamento de banco de dados. Uma camada de software entre um banco de dados físico e o usuário. O DBMS gerencia todo o acesso ao banco de dados.  
  
 **Driver baseado em DBMS**  
 Um driver que acessa dados físicos por meio de um mecanismo de banco de dados autônomo.  
  
 **DDL**  
 Linguagem de definição de dados. Essas instruções no SQL que definem, em vez de manipular, os dados. Por exemplo, **CREATE TABLE**, **criar índice**, **conceder**e **revogar**.  
  
 **identificador delimitado**  
 Um identificador que está incluído no identificador caracteres de aspas para que ele possa conter caracteres especiais ou corresponder palavras-chave (também conhecido como um identificador entre aspas).  
  
 **descritor**  
 Uma estrutura de dados que contém informações sobre os dados da coluna ou os parâmetros dinâmicos. A representação física do descritor não está definida; os aplicativos recebem acesso direto a um descritor apenas manipulando seus campos chamando funções ODBC com o identificador do descritor.  
  
 **banco de dados desktop**  
 Um DBMS projetado para ser executado em um computador pessoal. Em geral, esses DBMSs não fornecem um mecanismo de banco de dados autônomo e devem ser acessados por meio de um driver baseado em arquivo. Os mecanismos nesses drivers geralmente têm suporte reduzido para SQL e transações. Por exemplo, dBASE, Paradox, Btrieve ou Microsoft® FoxPro®.  
  
 **DPS**  
 Um registro que contém informações de diagnóstico sobre a última função chamada que usava um identificador específico. Os registros de diagnóstico são associados a identificadores de ambiente, conexão, instrução e descritor.  
  
 **DML**  
 Linguagem de manipulação de dados. Essas instruções no SQL que manipulam, em oposição a definir, os dados. Por exemplo, **Inserir**, **Atualizar**, **excluir**e **selecionar**.  
  
 **Driver**  
 Uma biblioteca de rotina que expõe as funções na API ODBC. Os drivers são específicos de um único DBMS.  
  
 **Gerenciador de Driver**  
 Uma biblioteca de rotina que gerencia o acesso a drivers para o aplicativo. O Gerenciador de driver carrega e descarrega (ou conecta e desconecta de) Drivers e passa chamadas para funções ODBC para o driver correto.  
  
 **DLL de instalação do driver**  
 Uma DLL que contém funções específicas de instalação e configuração de driver.  
  
 **cursor dinâmico**  
 Um cursor rolável capaz de detectar linhas atualizadas, excluídas ou inseridas no conjunto de resultados.  
  
 **SQL dinâmico**  
 Um tipo de SQL inserido no qual as instruções SQL são criadas e compiladas em tempo de execução. *Consulte também* SQL estático.  
  
## <a name="e"></a>E  
 **SQL inserido**  
 Instruções SQL que são incluídas diretamente em um programa escrito em outra linguagem, como COBOL ou C. ODBC não usa SQL inserido. *Consulte também* SQL estático *e* SQL dinâmico.  
  
 **ambiente**  
 Um contexto global no qual acessar dados; associado ao ambiente, qualquer informação que seja global por natureza, como uma lista de todas as conexões nesse ambiente.  
  
 **identificador de ambiente**  
 Um identificador para uma estrutura de dados que contém informações sobre o ambiente.  
  
 **cláusula escape**  
 Uma cláusula em uma instrução SQL.  
  
 **executados**  
 Para executar uma instrução SQL.  
  
## <a name="f"></a>F  
 **cursor de Fat**  
 *Consulte* cursor de bloco.  
  
 **Obtida**  
 Para recuperar uma ou mais linhas de um conjunto de resultados.  
  
 **campo**  
 *Consulte* a coluna.  
  
 **Driver baseado em arquivo**  
 Um driver que acessa dados físicos diretamente. Nesse caso, o driver contém um mecanismo de banco de dados e atua como o driver e a fonte de dado.  
  
 **fonte de dados de arquivo**  
 Uma fonte de dados para a qual as informações de conexão são armazenadas em um arquivo. DSN.  
  
 **chave estrangeira**  
 Uma coluna ou colunas em uma tabela que corresponde à chave primária em outra tabela.  
  
 **cursor de somente avanço**  
 Um cursor que só pode avançar pelo conjunto de resultados e geralmente busca apenas uma linha por vez. A maioria dos bancos de dados relacionais dá suporte apenas a cursores somente de avanço.  
  
## <a name="h"></a>H  
 **processamento**  
 Um valor que identifica exclusivamente algo como uma estrutura de arquivo ou de dados. Os identificadores são significativos apenas para o software que os cria e os usa, mas são passados por outros softwares para identificar coisas. O ODBC define identificadores para ambientes, conexões, instruções e descritores.  
  
## <a name="i"></a>I  
 **descritor de parâmetro de implementação (IPD)**  
 Um descritor que descreve os parâmetros dinâmicos usados em uma instrução SQL após qualquer conversão especificada pelo aplicativo.  
  
 **descritor de linha de implementação (IRD)**  
 Um descritor que descreve uma linha de dados antes de qualquer conversão especificada pelo aplicativo.  
  
 **DLL do instalador**  
 Uma DLL que instala componentes ODBC e configura fontes de dados.  
  
 **Recurso de aprimoramento de integridade**  
 Um subconjunto de SQL projetado para manter a integridade de um banco de dados.  
  
 **nível de conformidade da interface**  
 O nível da interface ODBC 3,7 suportada por um driver; pode ser Core, Level 1 ou Level 2.  
  
 **interoperabilidade**  
 A capacidade de um aplicativo usar o mesmo código ao acessar dados em DBMSs diferentes.  
  
 **IPD**  
 *Consulte* Descritor de parâmetro de implementação (IPD).  
  
 **IRD**  
 *Consulte* Descritor de linha de implementação (IRD).  
  
 **ISO/IEC**  
 Organização/International Electrotechnical Commission de padrões internacionais. A API ODBC é baseada na interface de nível de chamada ISO/IEC.  
  
## <a name="j"></a>J  
 **join**  
 Uma operação em um banco de dados relacional que vincula as linhas em duas ou mais tabelas, combinando valores em colunas especificadas.  
  
## <a name="k"></a>K  
 **chave**  
 Uma coluna ou colunas cujos valores identificam uma linha. *Consulte também* chave estrangeira *e* chave primária.  
  
 **conjunto**  
 Um conjunto de chaves usadas por um cursor misto ou controlado por conjunto de teclas para buscar linhas novamente.  
  
 **cursor controlado por conjunto de chaves**  
 Um cursor rolável que detecta linhas atualizadas e excluídas usando um conjunto de chaves.  
  
## <a name="l"></a>L  
 **literal**  
 Uma representação de caractere de um valor de dados real em uma instrução SQL.  
  
 **bloqueio**  
 O processo pelo qual um DBMS restringe o acesso a uma linha em um ambiente multiusuário. O DBMS geralmente define um bit em uma linha ou a página física que contém uma linha que indica que a linha ou a página está bloqueada.  
  
 **dados longos**  
 Qualquer dado binário ou de caractere acima de um determinado comprimento, como 255 bytes ou caracteres. Normalmente é muito mais longo. Esses dados são geralmente enviados e recuperados da fonte de dados em partes. Também conhecido como *blob*s ou *CLOB*s.  
  
## <a name="m"></a>M  
 **fonte de dados do computador**  
 Uma fonte de dados para a qual as informações de conexão são armazenadas no sistema (por exemplo, o registro).  
  
 **modo de confirmação manual**  
 Um modo de confirmação de transação no qual as transações devem ser explicitamente confirmadas chamando **SQLTransact**.  
  
 **los**  
 Dados que descrevem um parâmetro em uma instrução SQL ou uma coluna em um conjunto de resultados. Por exemplo, o tipo de dados, o comprimento do byte e a precisão de um parâmetro.  
  
 **Driver de várias camadas**  
 *Consulte* Driver baseado em DBMS.  
  
## <a name="n"></a>N  
 **Valor nulo**  
 Sem valor atribuído explicitamente. Em particular, um valor nulo é diferente de zero ou em branco.  
  
## <a name="o"></a>O  
 **byte**  
 Oito bits ou um byte. *Consulte também* byte.  
  
 **comprimento do octeto**  
 O comprimento em octetos de um buffer ou os dados que ele contém.  
  
 **ODBC**  
 Conectividade de banco de dados aberta. Uma especificação para uma API que define um conjunto padrão de rotinas com as quais um aplicativo pode acessar dados em uma fonte de dados.  
  
 **Administrador ODBC**  
 Um programa executável que chama a DLL do instalador para configurar fontes de dados.  
  
 Abrir grupo  
 Uma empresa que publica padrões. Em particular, ele publica os padrões do SAG (grupo de acesso do SQL).  
  
 **simultaneidade otimista**  
 Uma estratégia para aumentar a simultaneidade em que as linhas não são bloqueadas. Em vez disso, antes de serem atualizados ou excluídos, um cursor verifica se eles foram alterados desde a última leitura. Nesse caso, a atualização ou exclusão falhará. *Consulte também* simultaneidade pessimista.  
  
 **junção externa**  
 Uma junção na qual as linhas correspondentes e não correspondentes são retornadas. Os valores de todas as colunas da tabela incompatível em linhas não correspondentes são definidos como NULL.  
  
 **proprietário**  
 O proprietário de uma tabela.  
  
## <a name="p"></a>P  
 **meter**  
 Uma variável em uma instrução SQL, marcada com um marcador de parâmetro ou ponto de interrogação (?). Os parâmetros são associados a variáveis de aplicativo e seus valores recuperados quando a instrução é executada.  
  
 **descritor de parâmetro**  
 Um descritor que descreve os parâmetros de tempo de execução usados em uma instrução SQL, seja antes de qualquer conversão especificada pelo aplicativo (um descritor de parâmetro de aplicativo ou APD) ou após qualquer conversão especificada pelo aplicativo (um descritor de parâmetro de implementação ou IPD).  
  
 **matriz de operação de parâmetro**  
 Uma matriz que contém valores que um aplicativo pode definir para indicar que o parâmetro correspondente deve ser ignorado em uma operação **SQLExecDirect** ou **SQLExecute** .  
  
 **matriz de status de parâmetro**  
 Uma matriz que contém o status de um parâmetro após uma chamada para **SQLExecDirect** ou **SQLExecute**.  
  
 **Simultaneidade pessimista**  
 Uma estratégia para implementar serialização, em que as linhas são bloqueadas para que outras transações não possam alterá-las. *Consulte também* simultaneidade otimista *e* serialização.  
  
 **operação posicionada**  
 Qualquer operação que atue na linha atual. Por exemplo, posicionou as instruções UPDATE e Delete, **SQLGetData**e **SQLSetPos**.  
  
 **instrução UPDATE posicionada**  
 Uma instrução SQL usada para atualizar os valores na linha atual.  
  
 **instrução DELETE posicionada**  
 Uma instrução SQL usada para excluir a linha atual.  
  
 **deixar**  
 Para compilar uma instrução SQL. Um plano de acesso é criado por meio da preparação de uma instrução SQL.  
  
 **chave primária**  
 Uma coluna ou colunas que identifica exclusivamente uma linha em uma tabela.  
  
 **procedimento**  
 Um grupo de uma ou mais instruções SQL pré-compiladas que são armazenadas como um objeto nomeado em um banco de dados.  
  
 **coluna de procedimento**  
 Um argumento em uma chamada de procedimento, o valor retornado por um procedimento ou uma coluna em um conjunto de resultados criado por um procedimento.  
  
## <a name="q"></a>Q  
 **qualificado**  
 Um banco de dados que contém uma ou mais tabelas.  
  
 **consulta**  
 Uma instrução SQL. Às vezes, usado para significar uma instrução **Select** .  
  
 **identificador entre aspas**  
 Um identificador que é colocado em caracteres de aspas de identificador para que ele possa conter caracteres especiais ou palavras-chave de correspondência (também conhecidas em SQL-92 como um identificador delimitado).  
  
## <a name="r"></a>R  
 **Radix**  
 A base de um sistema numérico. Geralmente 2 ou 10.  
  
 **gravável**  
 *Consulte* linha.  
  
 **conjunto de resultados**  
 O conjunto de linhas criado pela execução de uma instrução **Select** .  
  
 **código de retorno**  
 O valor retornado por uma função ODBC.  
  
 **reverter**  
 Para retornar os valores alterados por uma transação para seu estado original.  
  
 **fila**  
 Um conjunto de colunas relacionadas que descrevem uma entidade específica. Também conhecido como *registro*.  
  
 **descritor de linha**  
 Um descritor que descreve as colunas de um conjunto de resultados, seja antes de qualquer conversão especificada pelo aplicativo (um descritor de linha de implementação ou IRD) ou após qualquer conversão especificada pelo aplicativo (um descritor de linha de aplicativo ou ARD).  
  
 **matriz de operação de linha**  
 Uma matriz que contém valores que um aplicativo pode definir para indicar que a linha correspondente deve ser ignorada em uma operação **SQLSetPos** .  
  
 **matriz de status de linha**  
 Uma matriz que contém o status de uma linha após uma chamada para **SQLFetch**, **SQLFetchScroll**ou **SQLSetPos**.  
  
 **linhas**  
 O conjunto de linhas retornado em uma única busca por um cursor de bloco.  
  
 **buffers de conjunto de linhas**  
 Os buffers associados às colunas de um conjunto de resultados e em que os dados de um conjunto de linhas inteiro são retornados.  
  
## <a name="s"></a>S  
 **SAG**  
 *Consulte* Grupo de acesso do SQL (SAG).  
  
 **função escalar**  
 Uma função que gera um único valor de um único valor. Por exemplo, uma função que altera o caso de dados de caractere.  
  
 **schema**  
 *Consulte* catálogo.  
  
 **cursor rolável**  
 Um cursor que pode avançar ou retroceder por meio do conjunto de resultados.  
  
 **serialização**  
 Se duas transações em execução simultaneamente produzem um resultado igual à execução serial (ou sequencial) dessas transações. As transações serializáveis são necessárias para manter a integridade do banco de dados.  
  
 **banco de dados do servidor**  
 Um DBMS projetado para ser executado em um ambiente cliente/servidor. Esses DBMSs fornecem um mecanismo de banco de dados autônomo que fornece suporte avançado para SQL e transações. Eles são acessados por meio de drivers baseados em DBMS. Por exemplo, Oracle, Informix, DB/2 ou Microsoft® SQL Server.  
  
 **função Set**  
 *Consulte* função de agregação.  
  
 **DLL de instalação**  
 *Consulte* dll de instalação *de driver e dll de* instalação do tradutor.  
  
 **Driver de camada única**  
 *Consulte* driver baseado em arquivo.  
  
 **SQL**  
 linguagem SQL. Uma linguagem usada por bancos de dados relacionais para consulta, atualização e gerenciamento de data.  
  
 **Grupo de acesso do SQL (SAG)**  
 Um consórcio da indústria de empresas que se preocupa com DBMSs do SQL. A interface de nível de chamada do grupo aberto baseia-se no trabalho feito originalmente pelo grupo de acesso do SQL.  
  
 **Nível de conformidade do SQL**  
 O nível de gramática do SQL-92 com suporte de um driver; pode ser entrada, de transição FIPS, intermediária ou completa.  
  
 **Tipo de dados SQL**  
 O tipo de dados de uma coluna ou parâmetro como armazenado na fonte de dados.  
  
 **SQLSTATE**  
 Um valor de cinco caracteres que indica um erro específico.  
  
 **Instrução SQL**  
 Uma frase completa no SQL que começa com uma palavra-chave e descreve completamente uma ação a ser executada. Por exemplo, selecione * em pedidos. As instruções SQL não devem ser confundidas com instruções.  
  
 **state**  
 Uma condição bem definida de um item. Por exemplo, uma conexão tem sete Estados, incluindo os dados não alocados, alocados, conectados e de necessidade. Determinadas operações só podem ser feitas quando um item está em um estado específico. Por exemplo, uma conexão só pode ser liberada quando está em um estado alocado e não, por exemplo, quando está em um estado conectado.  
  
 **transição de estado**  
 A movimentação de um item de um estado para outro. O ODBC define transições de estado rigorosas para ambientes, conexões e instruções.  
  
 **instrução**  
 Um contêiner para todas as informações relacionadas a uma instrução SQL. As instruções não devem ser confundidas com instruções SQL.  
  
 **identificador de instrução**  
 Um identificador para uma estrutura de dados que contém informações sobre uma instrução.  
  
 **cursor estático**  
 Um cursor rolável que não pode detectar atualizações, exclusões ou inserções no conjunto de resultados. Geralmente implementado, fazendo uma cópia do conjunto de resultados.  
  
 **SQL estático**  
 Um tipo de SQL inserido no qual as instruções SQL são embutidas em código e compiladas quando o restante do programa é compilado. *Consulte também* SQL dinâmico.  
  
 **procedimento armazenado**  
 *Consulte* o procedimento.  
  
## <a name="t"></a>T  
 **table**  
 Uma coleção de linhas.  
  
 **conversão**  
 A conversão de endereços de 16 bits em endereços de 32 bits, ou vice-versa, quando os aplicativos de 16 bits são usados com drivers ODBC de 32 bits.  
  
 **transaction**  
 Uma unidade atômica de trabalho. O trabalho em uma transação deve ser concluído como um todo; se qualquer parte da transação falhar, a transação inteira falhará.  
  
 **isolamento de transação**  
 O ato de isolar uma transação dos efeitos de todas as outras transações.  
  
 **nível de isolamento da transação**  
 Uma medida de quão bem uma transação é isolada. Há cinco níveis de isolamento de transação: leitura não confirmada, leitura confirmada, leitura repetida, serializável e controle de versão.  
  
 **DLL do Tradutor**  
 Uma DLL usada para converter dados de um conjunto de caracteres para outro.  
  
 **DLL de instalação do Tradutor**  
 Uma DLL que contém funções de instalação e configuração específicas do tradutor.  
  
 **confirmação de duas fases**  
 O processo de confirmar uma transação distribuída em duas fases. Na primeira fase, o processador de transação verifica se todas as partes da transação podem ser confirmadas. Na segunda fase, todas as partes da transação são confirmadas. Se qualquer parte da transação indicar na primeira fase que ela não pode ser confirmada, a segunda fase não ocorrerá. O ODBC não dá suporte a confirmações de duas fases.  
  
 **indicador de tipo**  
 Um valor inteiro passado para ou retornado de uma função ODBC para indicar o tipo de dados de uma variável de aplicativo, um parâmetro ou uma coluna. O ODBC define os indicadores de tipo para os tipos de dados C e SQL.  
  
## <a name="v"></a>V  
 **exibição**  
 Uma maneira alternativa de observar os dados em uma ou mais tabelas. Uma exibição geralmente é criada como um subconjunto das colunas de uma ou mais tabelas. No ODBC, as exibições geralmente são equivalentes às tabelas.
