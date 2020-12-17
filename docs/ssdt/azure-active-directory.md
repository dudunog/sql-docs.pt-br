---
title: Azure Active Directory no SSDT
description: Saiba mais sobre os métodos de autenticação do Azure Active Directory que o SSDT (SQL Server Data Tools) fornece para o Banco de Dados SQL do Azure e o Azure Synapse Analytics.
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
author: markingmyname
ms.author: maghan
reviewer: ''
ms.custom: seo-lt-2019
ms.date: 10/28/2019
monikerRange: = azuresqldb-current || = azure-sqldw-latest
ms.openlocfilehash: 564e6ad8cc4ab7cc14d816b34e5332412f912739
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489726"
---
# <a name="azure-active-directory-support-in-sql-server-data-tools-ssdt"></a>Suporte do Azure Active Directory no SSDT (SQL Server Data Tools)

[!INCLUDE[appliesto-xx-asdb-asdb-xxx-md.md](../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

O SSDT (SQL Server Data Tools) fornece vários métodos de autenticação do [Azure AD (Azure Active Directory)](/azure/active-directory/active-directory-whatis).

No Visual Studio, abra o **Pesquisador de Objetos do SQL Server** (no menu **Exibir**) e selecione **Adicionar SQL Server**:

![Caixa de diálogo de conexão do SSDT](media/azure-active-directory/interactive.png)

#### <a name="which-azure-sql-products"></a>Quais produtos Azure SQL?

Este artigo aborda o Azure AD para a seguinte lista de *produtos Azure SQL* na [nuvem do Azure](https://azure.microsoft.com/):

- Banco de Dados SQL do Azure
- Azure Synapse Analytics

## <a name="active-directory-password-authentication"></a>Autenticação da Senha do Active Directory

*A autenticação de senha do Active Directory* é um mecanismo de conexão com os produtos Azure SQL listados anteriormente. O mecanismo usa identidades no Azure AD (Azure Active Directory). Use esse método para conectar-se quando:

- Estiver conectado no Windows com credenciais de um domínio não federado com o Azure ou
- Estiver usando a autenticação do Azure AD com o Azure AD e ela for baseada no domínio cliente ou inicial.

Para saber mais, confira [Connecting to SQL Database By Using Azure Active Directory Authentication](/azure/sql-database/sql-database-aad-authentication) (Conectando-se ao Banco de Dados SQL usando a Autenticação do Azure Active Directory).  

## <a name="active-directory-integrated-authentication"></a>Autenticação Integrada do Active Directory

A *Autenticação Integrada do Active Directory* é um mecanismo de conexão com os produtos Azure SQL listados usando identidades no Azure AD (Azure Active Directory). Use esse método para se conectar, caso você entre no Windows com as credenciais de um domínio federado do Azure Active Directory. Para saber mais, confira [Connecting to SQL Database By Using Azure Active Directory Authentication](/azure/sql-database/sql-database-aad-authentication) (Conectando-se ao Banco de Dados SQL usando a Autenticação do Azure Active Directory).

## <a name="active-directory-interactive-authentication"></a>Autenticação Interativa do Active Directory

A *Autenticação Interativa do Active Directory* está disponível ao se conectar com os produtos listados Azure SQL listados com o SSDT, mas apenas com o [.NET Framework 4.7.2](/dotnet/api/?view=netframework-4.7.2&preserve-view=true) ou com uma versão posterior.

- [Baixe e instale para o .NET Framework, qualquer versão](https://www.microsoft.com/net/download/all).
- [Visual Studio 2017 versão 15.6](/visualstudio/releasenotes/vs2017-relnotes) ou uma versão posterior.

#### <a name="multi-factor-authentication-mfa"></a>Autenticação Multifator (MFA)

A Autenticação Interativa do Active Directory é compatível com uma autenticação interativa que permite usar a MFA (Autenticação Multifator) do Azure AD (Active Directory) para se autenticar com os produtos Azure SQL listados. Esse método é compatível com usuários nativos e federados do Azure AD e usuários convidados de outras contas. Os outros tipos de conta incluem:

- Usuários Azure AD B2B (entre empresas).
- Contas Microsoft, como @outlook.com, @hotmail.com e @live.com.
- Contas não Microsoft, como @gmail.com.

Se o método MFA for especificado, será necessário especificar o **Nome de usuário** e o campo **Senha** será desabilitado. 

#### <a name="password-entry"></a>Entrada de senha

Quando o usuário se autentica com o recurso *Autenticação Interativa do Active Directory*, o sistema exibe uma janela de autenticação que exige inserir uma senha manualmente.

![caixa de diálogo de entrada](media/azure-active-directory/sign-in.png)

A imposição da MFA é fornecida pelo Microsoft Azure AD por meio dessa janela pop-up adicional da MFA.

> [!NOTE]
> Fluxos de trabalho automatizados seriam bloqueados pelo uso da *Autenticação Interativa do Active Directory*. Deve haver uma pessoa disponível para interagir com o processo de autenticação inserindo uma senha manualmente.

## <a name="known-issues-and-limitations"></a>Limitações e problemas conhecidos

- A *Autenticação Interativa do Active Directory* só tem suporte durante a conexão com os produtos Azure SQL listados no início deste artigo. Ela não é compatível com SQL Server (local ou em uma VM).
- Não há suporte para a *Autenticação Interativa do Active Directory* na caixa de diálogo de conexão no *Gerenciador de Servidores*. É necessário se conectar usando o SSDT com o *Pesquisador de Objetos do SQL Server*.
- A integração de logon único com a conta conectada do Visual Studio não tem suporte para SSDT.
- O SQLPackage.exe instalado no diretório Extensões durante a instalação do Visual Studio não deve ser usado nesse local. Para usar SQLPackage.exe com o Azure AD, acesse [Estrutura do Aplicativo da Camada de Dados](https://www.microsoft.com/download/details.aspx?id=55088) 
- A Comparação de Dados do SSDT não é compatível com a autenticação do Azure AD.  


## <a name="see-also"></a>Consulte Também  

[Autenticação multifator](/azure/sql-database/sql-database-ssms-mfa-authentication)  
[Autenticação do Azure Active Directory com o Banco de Dados SQL](/azure/sql-database/sql-database-aad-authentication-configure)  
[Fórum do MSDN do SSDT](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[Blog da equipe do SSDT](/archive/blogs/ssdt/)  
[Baixar o SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)
