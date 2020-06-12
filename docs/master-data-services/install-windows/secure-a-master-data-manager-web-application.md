---
title: Proteger um aplicativo Web Master Data Manager
description: No SQL Server, você pode proteger o aplicativo Web Master Data Manager com HTTPS. Você deve ser um administrador e o MDS deve estar instalado no servidor Web.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: e360ba3a-e96b-4f85-b588-ed1f767fa973
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c87fd72a7257615ab83a7e9845fdd4c6a80d70f7
ms.sourcegitcommit: 903856818acc657e5c42faa16d1c770aeb4e1d1b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83731576"
---
# <a name="secure-a-master-data-manager-web-application"></a>Proteger um aplicativo Web Master Data Manager

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Você pode proteger o aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] com HTTPS.  
  
> [!NOTE]  
>  O aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] pode usar HTTP ou HTTPS, mas não ambos.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar o procedimento:  
  
-   Você deve ser um administrador no servidor Web onde o [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] é instalado.  
  
-   O MDS deve ser instalado no servidor Web e um aplicativo Web deve existir. Para obter mais informações, veja [Instalar o Master Data Services](../../master-data-services/install-windows/install-master-data-services.md) e [Criar um aplicativo Web do Master Data Manager &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md).  
  
### <a name="to-secure-the-master-data-manager-web-application-with-https"></a>Para proteger o aplicativo Web Master Data Manager com HTTPS  
  
1.  Depois que você confirmar que o aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] está configurado corretamente com HTTP, crie um certificado no IIS. Para obter mais informações, consulte [Configurando certificados de servidor no IIS 7](https://technet.microsoft.com/library/cc732230\(WS.10\).aspx).  
  
2.  No painel **Conexões** , em **Sites**, clique no site que hospeda o aplicativo Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] .  
  
3.  No painel **Ações**, clique em **Associações**.  
  
4.  Clique em **Adicionar**.  
  
5.  Na lista, selecione **https**.  
  
6.  Selecione o certificado TLS/SSL.  
  
7.  Clique em **OK**.  
  
8.  Opcional. Para remover o HTTP de forma que os usuários só possam acessar o site com HTTPS, na lista, clique na linha com **http**. Clique em **Remover** e, na caixa de diálogo de confirmação, clique em **Sim**.  
  
    > [!IMPORTANT]  
    >  Você deve alterar as configurações basicHttp e de wsHttpBinding depois de remover o HTTP.  
  
9. Para fechar a caixa de diálogo **Associações de Site** , clique em **Fechar**.  
  
10. Agora, abra o arquivo web.config de *drive*:\Arquivos de Programas\Microsoft SQL Server\130\Master Data Services\WebApplication.  
  
11. Localize a cadeia de caracteres `<security mode="Message">` e altere-a para `<security mode="Transport">`.  

12. Alterar `<serviceMetadata httpGetEnable="true" httpsGetEnabled="false">` para `<serviceMetadata httpGetEnable="false" httpsGetEnabled="true">` para evitar problemas que podem aparecer no cliente do Silverlight.

13. Salve e feche o arquivo. Se você receber um erro, pode ser porque o UAC está habilitado. Agora, os usuários devem ser capazes de usar HTTPS para acessar o site.  

  
## <a name="see-also"></a>Consulte Também  
 [Criar um aplicativo Web do Master Data Manager &#40;Master Data Services&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
