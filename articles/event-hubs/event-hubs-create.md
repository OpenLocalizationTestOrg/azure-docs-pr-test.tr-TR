---
title: bir Azure event hub aaaCreate | Microsoft Docs
description: "Azure Event Hubs ad alanı ve bir event hub'hello Azure portal kullanarak oluşturma"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a>Bir olay hub'ları ad alanı ve bir event hub'hello Azure portal kullanarak oluşturma

## <a name="create-an-event-hubs-namespace"></a>Bir olay hub'ları ad alanı oluşturma
1. Toohello üzerinde oturum [Azure portal][Azure portal], tıklatıp **yeni** hello adresindeki hello ekranın sol üst.
1. Tıklatın **nesnelerin interneti**ve ardından **olay hub'ları**.
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. Merhaba, **ad alanı oluşturma** dikey penceresinde, bir ad alanı adı girin. Merhaba adı olup olmadığını hello sistem hemen toosee denetler.
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. Emin hello ad alanı adı yapmadan kullanılabilir olduktan sonra hello fiyatlandırma Katmanı (temel veya standart) seçin. Ayrıca, hangi toocreate hello kaynak bir Azure aboneliği, kaynak grubunu ve konumu seçin. 
1. Tıklatın **oluşturma** toocreate hello ad alanı. Merhaba sistem toofully sağlama hello kaynakları için bir kaç dakika toowait olabilir.
2. Merhaba portal listesinde ad alanları, yeni ad alanı oluşturulan hello'ı tıklatın.
2. Tıklatın **paylaşılan erişim ilkeleri**ve ardından **RootManageSharedAccessKey**.
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. Merhaba Kopyala düğmesine toocopy hello tıklatın **RootManageSharedAccessKey** bağlantı dizesi toohello Pano. Bu bağlantı dizesini Not Defteri, daha sonra toouse gibi geçici bir konuma kaydedin.
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a>Olay hub’ı oluşturma

1. Merhaba olay hub'ları ad listesinde yeni oluşturulan hello ad alanına tıklayın.      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. Merhaba ad alanı dikey penceresinde tıklayın **olay hub'ları**.
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. Merhaba dikey penceresinde Hello üstünde tıklatın **Event Hub'ı eklemek**.
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. Olay hub'ınız için bir ad yazın ve ardından **oluşturma**.
   
    ![](./media/event-hubs-create/create-event-hub5.png)

Olay hub'ınız şimdi oluşturulur ve toosend gerekir ve olayları alma hello bağlantı dizelerine sahipsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Event Hubs hakkında daha fazla toolearn bu bağlantıları ziyaret edin:

* [Event Hubs’a genel bakış](event-hubs-what-is-event-hubs.md)
* [Event Hubs API’sine genel bakış](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/