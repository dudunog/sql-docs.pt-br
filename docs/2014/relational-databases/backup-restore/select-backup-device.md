---
title: Selecionar dispositivo de backup | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.selectbackupdevice.f1
ms.assetid: 7887c9fd-15ce-4cc8-b069-845c1d09088c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2ec38139f2939fb967b9e24900bf160e27273358
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84956496"
---
# <a name="select-backup-device"></a>Selecionar Dispositivo de Backup
  Use a caixa de diálogo **Selecionar Dispositivo de Backup** para selecionar um dispositivo lógico de backup para a operação de restauração.  
  
 O dispositivo lógico de backup é definido pelo usuário e correspondente a um dispositivo físico, que pode ser uma unidade de fita ou de disco fornecidas pelo sistema operacional.  
  
> [!NOTE]  
>  Para que um backup possa utilizar vários dispositivos de backup, todos precisam corresponder a um único tipo de dispositivo.  
  
 **Para usar o SQL Server Management Studio para exibir o conteúdo de um dispositivo de backup**  
  
-   [Exibir o conteúdo de um arquivo ou fita de backup &#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Exibir as propriedades e o conteúdo de um dispositivo de backup lógico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
## <a name="options"></a>Opções  
 **Dispositivo de backup**  
 Na caixa de listagem, selecione o nome de um dispositivo lógico de backup do qual você deseja restaurar.  
  
 Para obter informações sobre como exibir o conteúdo de um dispositivo de backup, veja [Exibir as propriedades e o conteúdo de um dispositivo de backup lógico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md).  
  
## <a name="remarks"></a>Comentários  
 Caso não se observe um dispositivo lógico de backup que contenha um backup procurado na lista, isso indica que o backup pode ter sido gravado diretamente em um ou mais arquivos ou unidades de fita. Nesse caso, cancele a caixa de diálogo **Selecionar Dispositivo de Backup** . Na caixa de diálogo **Especificar Backup** , selecione **Arquivo** ou **Fita** na caixa de listagem **Mídia do backup** .  
  
## <a name="see-also"></a>Consulte Também  
 [Dispositivos de backup &#40;SQL Server&#41;](backup-devices-sql-server.md)  
  
  
