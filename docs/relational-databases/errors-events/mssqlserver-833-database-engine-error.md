---
description: MSSQLSERVER_833
title: MSSQLSERVER_833 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 833 (Database Engine error)
ms.assetid: 14129cc4-be80-4772-9e3f-0e5da4d0696b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 132e33d7bf2b03df21a1d6a3475ca625675b3328
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988754"
---
# <a name="mssqlserver_833"></a>MSSQLSERVER_833
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sql-asdbmi.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|833|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|BUF_LONG_IO|  
|Texto da mensagem|O SQL Server encontrou %d ocorrências de solicitações de E/S demorando mais do que %d segundos para serem concluídas no arquivo [%ls] no banco de dados `[%ls] (%d)`.  O identificador de arquivo do SO é 0x%p.  O deslocamento da E/S mais demorada é: %#016I64x.|  
  
## <a name="explanation"></a>Explicação  
Esta mensagem indica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emitiu uma solicitação de leitura ou gravação de disco, e que a solicitação demorou mais de 15 segundos para retornar. Esse erro é informado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e indica um problema com o subsistema de E/S. Você também pode observar outros sintomas associados à mensagem: tempos de espera altos para esperas de PAGEIOLATCH, avisos ou erros no log de eventos do sistema e indicações de problemas de latência de disco nos contadores do monitor do sistema. Monitore o [sys.dm_io_virtual_file_stats](../system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) e escolha a camada de armazenamento e a IOPS apropriadas para a sua taxa de transferência do armazenamento. 
  
### <a name="possible-causes"></a>Possíveis causas  
Esse problema pode ser causado por problemas de desempenho do sistema operacional, erros de hardware, erros de firmware, problemas de driver de dispositivo ou intervenção de driver de filtro no processo de E/S ou no caminho de armazenamento dos arquivos de banco de dados. O SQL Server registra a hora em que iniciou uma solicitação de E/S e a hora em que a E/S foi concluída. Se a diferença entre elas for de 15 segundos ou mais, essa condição será detectada. Isso também significa que o SQL Server não é a causa de uma condição de E/S atrasada que essa mensagem descreve e relata. Essa condição é conhecida como "E/S paralisada". A maioria das solicitações de disco ocorre dentro da velocidade típica do disco. Essa velocidade geralmente é conhecida como "tempo de busca no disco". O tempo de busca no disco para a maioria dos discos padrão é de dez milissegundos ou menos. Portanto, 15 segundos é um tempo muito longo para o caminho de E/S do sistema retornar ao SQL Server. 
  
## <a name="user-action"></a>Ação do usuário  
Solucione este erro procurando mensagens de erros relacionados a hardware no log de eventos de sistema. Examine também os logs específicos do hardware, se estiverem disponíveis. Você deve usar as técnicas e os métodos necessários para determinar a causa do atraso no sistema operacional, com os drivers ou com o hardware de E/S. A resolução desse problema pode envolver a atualização de todos os drivers e firmware do dispositivo ou a execução de outros diagnósticos associados ao sistema de disco. 
  
Use o Monitor de Desempenho para examinar os seguintes contadores:  
  
-   **Média de seg/transferência do disco**  
  
-   **Média de comprimento da fila do disco**  
  
-   **Comprimento atual da fila do disco**  
  
Por exemplo, o tempo da **Média de seg/transferência do disco** em um computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], normalmente, é inferior a 15 milissegundos. Se o valor da **Média de seg/transferência do disco** aumentar, isso indicará que o subsistema de E/S não está acompanhando a demanda de E/S.

Você também pode usar recursos como o [registro em log do ETW do Storport](/archive/blogs/ntdebugging/storport-etw-logging-to-measure-requests-made-to-a-disk-unit) para medir a latência de solicitações feitas em uma unidade de disco. Outro kit semelhante de solução de problemas de E/S de disco está disponível como um perfil interno do [Windows Performance Recorder](/windows-hardware/test/wpt/introduction-to-wpr).
  
> [!NOTE]  
> O acesso ao disco pode ficar mais lento devido a um programa antivírus. Para aumentar a velocidade de acesso, exclua os arquivos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificados na mensagem de erro das verificações ativas de vírus. Você pode usar o [utilitário de linha de comando fltmc.exe](/windows-hardware/drivers/ifs/development-and-testing-tools#fltmcexe-control-program) para consultar todos os drivers de filtro instalados no sistema e entender as funções que ele executa no caminho de armazenamento para os arquivos de banco de dados. 
  
Para obter mais informações sobre erros de E/S, consulte [Noções básicas de E/S do Microsoft SQL Server, Capítulo 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10)) e o artigo da Base de Dados de Conhecimento em [https://support.microsoft.com/kb/897284/en-us](https://support.microsoft.com/kb/897284/en-us).  
