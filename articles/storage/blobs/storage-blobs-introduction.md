---
title: "Azure Blob Depolama giriş | Microsoft Docs"
description: "Azure Blob Depolama giriş"
services: storage
documentationcenter: 
author: tamram
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/28/2017
ms.author: tamram
ms.openlocfilehash: 0097f1c02b88343a135b6489130a6e0d35cf6fba
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/23/2018
---
# <a name="introduction-to-blob-storage"></a>Blob Storage'a giriş

Azure Blob Storage; HTTP veya HTTPS aracılığıyla dünyanın her yerinde erişilebilen metin veya ikili veriler gibi büyük miktarda yapılandırılmamış nesne verilerinin depolanması için bir hizmettir. Verileri genel olarak herkese açık kullanıma sunmak veya uygulama verilerini özel olarak depolamak için Blob Storage’ı kullanabilirsiniz.

Blob Storage’ın yaygın kullanımları şunlardır:

* Görüntülerin veya belgelerin doğrudan bir tarayıcıya sunulması
* Dağıtılan erişim için dosyaların depolanması
* Video ve ses akışları
* Yedekleme ve geri yükleme, olağanüstü durum kurtarma ve arşivleme için verilerin depolanması
* Şirket içi veya Azure barındırılan hizmetle analiz için verilerin depolanması

## <a name="blob-service-concepts"></a>Blob hizmeti kavramları

Blob hizmetinde şu bileşenler bulunur:

![Blob mimarisi](./media/storage-blobs-introduction/blob1.png)

* **Depolama Hesabı:** Tüm Azure Storage erişimi bir depolama hesabıyla yapılır. Bu depolama hesabı olabilir bir **genel amaçlı depolama hesabı (v1 veya v2)** veya **Blob storage hesapları**. Daha fazla bilgi için bkz. [Azure depolama hesapları hakkında](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

* **Kapsayıcı:** Kapsayıcı, bir dizi blobun gruplandırılmasını sağlar. Tüm bloblar bir kapsayıcıda olmalıdır. Bir hesapta sınırsız sayıda kapsayıcı olabilir. Kapsayıcıda sınırsız sayıda blob depolanabilir. Kapsayıcı adındaki harflerin küçük harf olması gerektiğini unutmayın.

* **Blob:** Herhangi bir türde ve boyutta bir dosya. Azure Storage üç tür BLOB sunar: blok blobları, [sayfa blobları](storage-blob-pageblob-overview.md)ve ilave blobları.
  
    *Blok blobları*, belgeler ve medya dosyaları gibi metin veya ikili dosyaların depolanması için idealdir. *Ekleme blobları* blok bloblarına benzer; bloklardan oluşturulmuş olsalar da ekleme işlemleri için iyileştirilmişlerdir; bu nedenle, günlük kaydı senaryoları için kullanışlıdırlar. Tek bir blok blobu, her birinin büyüklüğü 100 MB’a kadar olabilen 50.000 blok içerebilir; toplam boyut 4,75 TB'tan biraz fazladır (100 MB X 50.000). Tek bir ekleme blobu, her birinin büyüklüğü 4 MB’a kadar olabilen 50.000 blok içerebilir; toplam boyut 195 GB'tan biraz fazladır (4 MB X 50.000).
  
    *Sayfa blobları* boyutu 8 TB'ye kadar olabilir ve sık sık okuma/yazma işlemleri için daha verimlidir. Azure Virtual Machines sayfa bloblarını işletim sistemi ve veri diskleri olarak kullanır.
  
    Kapsayıcıları ve blobları adlandırma hakkında ayrıntılı bilgi için bkz. [Kapsayıcıları, Blobları ve Meta Verileri Adlandırma ve Bunlara Başvurma](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).

## <a name="next-steps"></a>Sonraki adımlar

* [Depolama hesabı oluşturma](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [.NET kullanarak Blob storage'ı kullanmaya başlama](storage-dotnet-how-to-use-blobs.md)
* [.NET kullanarak azure depolama örnekleri](../common/storage-samples-dotnet.md)
* [Java kullanarak azure depolama örnekleri](../common/storage-samples-java.md)
