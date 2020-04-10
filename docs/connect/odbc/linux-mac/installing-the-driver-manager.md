---
title: Instalando o Gerenciador de Driver (Driver ODBC para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Driver Manager, installing
ms.assetid: 7c4b6fb4-f45a-4973-adb9-a4d83f0a2a7a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f2179df0018d227fc12dd545f4e846c475b120ca
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921908"
---
# <a name="installing-the-driver-manager"></a>Instalando o Gerenciador de Driver
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este artigo contém instruções para instalar o Gerenciador de Driver unixODBC para uso com todas as versões do Microsoft ODBC Driver for SQL Server no Linux e macOS.  

> [!IMPORTANT]  
> Exclua qualquer pacote de gerenciador de driver instalado em seu computador antes de instalar o Gerenciador de Driver unixODBC. A instalação do Gerenciador de Driver unixODBC pode causar uma falha em um Gerenciador de Driver existente.  

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-13-131-and-17"></a>Instalando o Gerenciador de Driver para o Microsoft ODBC Driver 13, 13.1 e 17
A dependência do gerenciador de driver é resolvida automaticamente pelo sistema de gerenciamento de pacotes quando você instala o Microsoft ODBC Driver 13, 13.1 ou 17 for SQL Server em Linux ou no macOS seguindo as instruções dos seguintes artigos:

- [Como instalar o Microsoft ODBC Driver for SQL Server em Linux](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [Como instalar o Microsoft ODBC Driver for SQL Server no macOS](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-11-for-sql-server"></a>Instalando o Gerenciador de Driver para o Microsoft ODBC Driver 11 for SQL Server  

(Apenas para o Red Hat Linux e SUSE.)

**Uso do script de instalação**  
  
> [!IMPORTANT]  
> Estas instruções referem-se ao `msodbcsql-11.0.2270.0.tar.gz`, que é o arquivo de instalação para o Red Hat Linux. Se estiver instalando a Versão Prévia para SUSE Linux, o nome do arquivo será `msodbcsql-11.0.2260.0.tar.gz`.  

Para instalar o gerenciador de driver:  
  
1.  Verifique se você tem permissão de raiz.  
  
2.  Vá para o diretório em que o download do [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC Driver colocou o arquivo chamado `msodbcsql-11.0.2270.0.tar.gz`. Verifique se você tem o arquivo \*.tar.gz que corresponde à sua versão do Linux. Para extrair os arquivos, execute o seguinte comando: **tar xvzf msodbcsql-11.0.2270.0.tar.gz**.  

3.  Altere para o diretório `msodbcsql-11.0.2270.0`. Lá, você verá um arquivo chamado `build_dm.sh`. Você pode executar `build_dm.sh` para instalar o Gerenciador de Driver unixODBC.

4.  Para ver uma lista das opções disponíveis, execute o seguinte comando: **./build_dm.sh --help**.  
  
5.  Quando estiver pronto para instalar, e se o computador puder acessar um site externo por meio de FTP, execute o seguinte comando: **./build_dm.sh**.

Se o computador não puder acessar um site externo por meio de FTP, obtenha `unixODBC-2.3.0.tar.gz`. Você pode obter `unixODBC-2.3.0.tar.gz` de [http://www.unixodbc.org](http://www.unixodbc.org/). Clique no link **Download** no lado esquerdo da página para ir para a página de download. Em seguida, clique no link apropriado para baixar o unixODBC-2.3.0 (não o unixODBC-2.3.1). O unixODBC-2.3.1 não é compatível com esta versão do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Execute o seguinte comando para iniciar a instalação do Gerenciador de Driver unixODBC: **./build_dm.sh --download-url=file://unixODBC-2.3.0.tar.gz**.  

6.  Digite **YES** para prosseguir com a descompactação dos arquivos. Esta parte do processo pode levar até cinco minutos para ser concluída.  

7.  Depois que o script terminar a execução, siga as instruções na tela para instalar o gerenciador do driver unixODBC.

Agora você pode instalar o driver. Para obter mais informações, confira as instruções de instalação do driver ODBC para [Linux](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) ou [macOS](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md).

**Instalação manual**

Se não for possível concluir o script de instalação, configure e compile o gerenciador de driver correto por conta própria.

1.  Remova qualquer versão mais antiga do unixODBC instalada (por exemplo, unixODBC 2.2.11). No Red Hat Enterprise Linux 5 ou 6, execute o seguinte comando: **yum remove unixODBC**. No SUSE Linux Enterprise, **zypper remover unixODBC**.  
  
2.  Ir para [http://www.unixodbc.org](http://www.unixodbc.org/). Clique no link **Download** no lado esquerdo da página para ir para a página de download. Em seguida, clique no link apropriado para salvar o arquivo unixODBC-2.3.0.tar.gz no seu computador. O UnixODBC-2.3.1 não é compatível com esta versão do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
3.  No seu computador Linux, execute o comando: **tar xvzf unixODBC-2.3.0.tar.gz**.  
  
4.  Altere para o diretório unixODBC-2.3.0.  
  
5.  No prompt de comando, execute o comando: **CPPFLAGS="-DSIZEOF_LONG_INT=8"** .  
  
6.  Em um prompt de comando, execute o comando: **export CPPFLAGS**.  
  
7.  Em um prompt de comando, execute o comando: **"./configure --prefix=/usr --libdir=/usr/lib64 --sysconfdir=/etc --enable-gui=no --enable-drivers=no --enable-iconv --with-iconv-char-enc=UTF8 --with-iconv-ucode-enc=UTF16LE"** .  
  
8.  No prompt de comando (conectado como raiz), execute o comando: **make**.  
  
9. No prompt de comando (conectado como raiz), execute o comando: **make install**.  

Agora você pode instalar o driver. Para obter mais informações, confira as instruções de instalação do driver ODBC para [Linux](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) ou [macOS](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md).
  
## <a name="see-also"></a>Consulte Também

- [Como instalar o Microsoft ODBC Driver for SQL Server em Linux](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)
- [Como instalar o Microsoft ODBC Driver for SQL Server no macOS](../../../connect/odbc/linux-mac/install-microsoft-odbc-driver-sql-server-macos.md)
- [Notas de Versão](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)
