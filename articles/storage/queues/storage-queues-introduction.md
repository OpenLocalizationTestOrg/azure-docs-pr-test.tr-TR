---
title: Kuyruk depolama aaaIntroduction tooAzure | Microsoft Docs
description: "Giriş tooAzure kuyruk depolama"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a>Giriş tooQueues

Azure kuyruk depolama alanından herhangi bir yere Merhaba Dünya HTTP veya HTTPS kullanarak kimlik doğrulaması yapılmış çağrılar aracılığıyla erişilebilen iletileri çok sayıda depolamak için bir hizmettir. Tek bir kuyruk iletisinin boyutu too64 KB yukarı olabilir ve bir kuyruk iletileri, bir depolama hesabı toohello toplam kapasite sınırına milyonlarca içerebilir.

## <a name="common-uses"></a>Ortak kullanımlar

Kuyruk depolamanın yaygın kullanımları şunlardır:

* Zaman uyumsuz olarak biriktirme çalışma tooprocess listesi oluşturma
* İletileri Azure web rolü tooan Azure çalışan rolüne geçirme

## <a name="queue-service-concepts"></a>Kuyruk hizmeti kavramları

Merhaba sıra hizmeti hello aşağıdaki bileşenleri içerir:

![Sıra kavramları](./media/storage-queues-introduction/queue1.png)

* **URL biçimi:** sıraları hello şu URL biçimi kullanılarak adreslenebilir:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    URL aşağıdaki hello hello diyagramı kuyrukta ele alır:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Depolama hesabı:** üzerinden depolama hesabı tüm erişim tooAzure depolama yapılır. Depolama hesabı kapasitesi hakkında ayrıntılı bilgi için bkz. [Azure Storage Ölçeklenebilirlik ve Performans Hedefleri](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).

* **Kuyruk:** Kuyrukta bir dizi ileti vardır. Tüm iletiler bir kuyrukta olmalıdır. Bu hello sıra adı tüm küçük harfli olması gerektiğini unutmayın. Kuyrukların adlandırılması hakkında daha fazla bilgi için bkz. [Kuyrukları ve Meta Verileri Adlandırma](https://msdn.microsoft.com/library/azure/dd179349.aspx).

* **İleti:** bir ileti görüntülenirse, herhangi bir biçimde too64 KB. bir ileti hello kuyrukta kalabileceği en uzun süre hello yedi gündür.

## <a name="next-steps"></a>Sonraki adımlar

* [Depolama hesabı oluşturma](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [.NET kullanarak kuyruklarla çalışmaya başlama](storage-dotnet-how-to-use-queues.md)
