---
title: A função do SOAP no Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- SOAP [Reporting Services], role in Reporting Services
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: f229c3ef-f2ca-448f-98f1-b8df350b9992
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4e0b418e44436912b5ed1368ad7a316951872266
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62519191"
---
# <a name="the-role-of-soap-in-reporting-services"></a>The Role of SOAP in Reporting Services
  O serviço Web do servidor de relatório usa o sistema de mensagens SOAP (Simple Object Access Protocol) para enviar comandos baseados em texto por meio de uma rede. Esses comandos assumem a forma de texto XML que é enviado por meio da Web usando HTTP. Usando o SOAP como seu protocolo de comunicação, o serviço Web do servidor de relatório permite aplicativos e componentes para trocar dados com o servidor de relatório usando uma infraestrutura largamente aceita e aberta. O padrão de SOAP é definido em www.w3.org/TR/SOAP.  
  
 Qualquer aplicativo cliente pode agir como um cliente de SOAP desde que seja o SOAP-atento e pode enviar solicitações de SOAP. O Gerenciador de Relatórios é um cliente de SOAP. Ele fornece uma interface para o banco de dados do servidor de relatório em que todos os relatórios e conteúdo relacionado a relatório são armazenados. Os usuários finais podem usar o aplicativo para navegar bem como gerenciar relatórios e pastas no namespace de servidor de relatório. O Gerenciador de Relatórios é criado na infraestrutura de serviço Web do servidor de relatório.  
  
 Um servidor de relatório age como um servidor de SOAP, um serviço do SOAP-atento que pode aceitar solicitações de clientes de SOAP e criar respostas apropriadas. O servidor trata as solicitações e envia respostas codificadas novamente para o cliente.  
  
 As mensagens de SOAP no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] assumem muitas formas diferentes, dependendo do tipo de solicitação feita pelo cliente. O exemplo a seguir representa uma solicitação de cliente de SOAP simples para remover um item do banco de dados do servidor de relatório.  
  
```  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <soap:Body>  
        <DeleteItem xmlns="https://www.microsoft.com/sql/ReportingServer">  
            <item>/Samples/Report1</item>  
        </DeleteItem>  
    </soap:Body>  
</soap:Envelope>  
```  
  
 O SOAP em si requer que as mensagens sejam colocadas em um elemento `Envelope`, com o tamanho da mensagem em um elemento `Body`. Nesse exemplo, o corpo contém uma chamada para o método <xref:ReportService2010.ReportingService2010.DeleteItem%2A>, que assume um parâmetro de cadeia de caracteres representando o caminho do item a ser excluído. Você pode criar uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] classe de proxy de cliente que encapsula todas as operações SOAP em métodos. O método [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] a seguir representa o exemplo de SOAP fornecido anteriormente.  
  
```  
public void DeleteItem(string item);  
```  
  
 A resposta do servidor pode se parecer com o seguinte:  
  
```  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <soap:Body>  
        <DeleteItemResponse xmlns="https://www.microsoft.com/sql/ReportingServer" />  
    </soap:Body>  
</soap:Envelope>  
```  
  
 O método <xref:ReportService2010.ReportingService2010.DeleteItem%2A> não tem nenhum valor de retorno, portanto, uma resposta vazia é retornada.  
  
## <a name="see-also"></a>Consulte Também  
 [Acessando a API SOAP](accessing-the-soap-api.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Reporting Services servidor de relatório](../reporting-services-report-server.md)   
 [Serviço Web do Servidor de Relatório](report-server-web-service.md)  
  
  
