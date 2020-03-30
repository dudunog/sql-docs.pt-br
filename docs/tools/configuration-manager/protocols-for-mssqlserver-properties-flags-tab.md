---
title: Protocolos para propriedades MSSQLSERVER (guia Sinalizadores)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- MSSQLSERVER property protocols
ms.assetid: 4d38e6e9-f95f-4e79-ae45-89f631037528
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: cb903479b3fb7bd5f5c8ce709a74b797aec68371
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307744"
---
# <a name="protocols-for-mssqlserver-properties-flags-tab"></a>Protocolos para propriedades MSSQLSERVER (guia Sinalizadores)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  Quando um certificado estiver instalado no servidor, use a guia **Sinalizadores** na caixa de diálogo **Protocolos para Propriedades MSSQLSERVER** para exibir ou especificar a criptografia do protocolo e ocultar as opções da instância. O [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser reiniciado para habilitar ou desabilitar a configuração **ForceEncryption**.  
  
 Para criptografar conexões, é necessário provisionar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] com um certificado. Se um certificado não estiver instalado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vai gerar um certificado autoassinado quando a instância for iniciada. Esse certificado pode ser usado em vez de um certificado de uma autoridade de certificação confiável, mas ele não fornece autenticação ou não repúdio.  
  
> [!CAUTION]  
>  As conexões SSL criptografadas com um certificado autoassinado não fornecem alta segurança. Elas são suscetíveis a ataques “man-in-the-middle”. Não se deve confiar no SSL usando certificados autoassinados em um ambiente de produção ou em servidores conectados à Internet.  
  
 Para obter mais informações sobre criptografia, consulte "Criptografando conexões com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 O processo de logon sempre é criptografado. Quando **ForceEncryption** estiver definido como **Yes**, toda a comunicação cliente/servidor será criptografada, e os clientes que se conectarem ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] deverão estar configurados para confiar na autoridade raiz do certificado do servidor. Para obter mais informações, confira "Como habilitar conexões criptografadas no [!INCLUDE[ssDE](../../includes/ssde-md.md)] (Configuration Manager [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="cluster-servers"></a>Servidores clusterizados  
 Para usar criptografia com um cluster de failover, você deve instalar o certificado de servidor com o nome DNS totalmente qualificado do servidor virtual em todos os nós no cluster de failover. Por exemplo, se você tiver um cluster de dois nós, com os nomes "test1. *\<your company>* .com" e "test2. *\<your company>* .com" e um servidor virtual chamado "virtsql", será necessário instalar um certificado para "virtsql. *\<your company>* .com" em ambos os nós. Você então poderá marcar a caixa de seleção **ForceEncryption** no **SQL Server Configuration Manager** para configurar o cluster de failover para criptografia.  
  
## <a name="options"></a>Opções  
 **ForceEncryption**  
 Forçar a criptografia do protocolo. Criptografia é um método para manter a confidencialidade das informações com a alteração dos dados em uma forma ilegível. A criptografia assegura que os dados permaneçam seguros, mesmo que os pacotes de transmissão sejam exibidos durante o processo de transmissão. Para usar a ligação de canal, defina **Forçar Criptografia** como **Ativada** e configure **Proteção Estendida** na guia **Avançado** .  
  
 **HideInstance**  
 Impede que o Serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exponha essa instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] nos computadores cliente que tentarem localizá-la usando o botão **Procurar** . No caso de instâncias nomeadas no servidor, para conexão, os aplicativos cliente devem especificar as informações de ponto de extremidade do protocolo. Por exemplo, o número da porta ou o nome do pipe nomeado, como **tcp:server,5000**. Para obter mais informações, consulte [Logging In to SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md).  
  
 Para obter mais informações, consulte "Como habilitar conexões criptografadas no mecanismo de banco de dados (SQL Server Configuration Manager)" nos Manuais Online.  
  
  
