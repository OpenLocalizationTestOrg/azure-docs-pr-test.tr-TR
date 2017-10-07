---
title: Blob Depolama aaaIntroduction tooAzure | Microsoft Docs
description: "Giriş tooAzure Blob Depolama"
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
ms.date: 08/17/2017
ms.author: robinsh
ms.openlocfilehash: 3431f826ae51d42dbced084ee60f9ff70a8168d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooblob-storage"></a>Giriş tooBlob depolama

Azure Blob depolama alanından herhangi bir yere Merhaba Dünya HTTP veya HTTPS üzerinden erişilebilen metin veya ikili veriler gibi yapılandırılmamış nesne verilerini büyük miktarlarda depolamak için bir hizmettir. Blob Depolama tooexpose verileri kullanabileceğiniz genel olarak toohello world veya toostore uygulama verilerini özel olarak.

Blob Storage’ın yaygın kullanımları şunlardır:

* Hizmet görüntüleri veya doğrudan tooa tarayıcı belgeleri
* Dağıtılan erişim için dosyaların depolanması
* Video ve ses akışları
* Yedekleme ve geri yükleme, olağanüstü durum kurtarma ve arşivleme için verilerin depolanması
* Şirket içi veya Azure barındırılan hizmetle analiz için verilerin depolanması

## <a name="blob-service-concepts"></a>Blob hizmeti kavramları

Merhaba Blob hizmeti hello aşağıdaki bileşenleri içerir:

![Blob mimarisi](./media/storage-blobs-introduction/blob1.png)

* **Depolama hesabı:** üzerinden depolama hesabı tüm erişim tooAzure depolama yapılır. Bu depolama hesabı olabilir bir **genel amaçlı depolama hesabı** veya **Blob storage hesabı** nesnelerin/blobların depolanması için özelleştirilmiş. Daha fazla bilgi için bkz. [Azure depolama hesapları hakkında](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

* **Kapsayıcı:** Kapsayıcı, bir dizi blobun gruplandırılmasını sağlar. Tüm bloblar bir kapsayıcıda olmalıdır. Bir hesapta sınırsız sayıda kapsayıcı olabilir. Kapsayıcıda sınırsız sayıda blob depolanabilir. Merhaba kapsayıcı adının küçük harfli olması gerektiğini unutmayın.

* **Blob:** Herhangi bir türde ve boyutta bir dosya. Azure Storage üç tür blob sunar: blok blobları, sayfa blobları ve ekleme blobları.
  
    *Blok blobları*, belgeler ve medya dosyaları gibi metin veya ikili dosyaların depolanması için idealdir. *Ekleme blobları* olan benzer tooblock BLOB'lar bunlar bloklardan oluşur ancak için iyileştirilmiş da ekleme işlemleri, günlük kaydı senaryoları için yararlı olacak şekilde. Tek bir blok blobu too50, her too100 MB yukarı 000 bloklarını yukarı içerebilir, biraz daha fazladır 4.75 TB (100 MB X 50.000) toplam boyut. Tek ek blob too50, her too4 MB yukarı 000 bloklarını yukarı içerebilir toplam boyut 195 GB'den biraz daha büyük (4 MB X 50.000).
  
    *Sayfa blobları* yukarı too1 TB boyutunda olabilir ve sık sık okuma/yazma işlemleri için daha verimlidir. Azure Virtual Machines sayfa bloblarını işletim sistemi ve veri diskleri olarak kullanır.
  
    Kapsayıcıları ve blobları adlandırma hakkında ayrıntılı bilgi için bkz. [Kapsayıcıları, Blobları ve Meta Verileri Adlandırma ve Bunlara Başvurma](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).

## <a name="next-steps"></a>Sonraki adımlar

* [Depolama hesabı oluşturma](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [.NET kullanarak Blob storage'ı kullanmaya başlama](storage-dotnet-how-to-use-blobs.md)