---
title: "aaaAzure Storage ölçeklenebilirlik ve performans hedefleri | Microsoft Docs"
description: "Azure depolama kapasitesi, istek hızı ve her iki standart ve premium depolama hesapları için gelen ve giden bant genişliği de dahil olmak üzere, Hello ölçeklenebilirlik ve performans hedefleri hakkında bilgi edinin. Bölümler içinde hello Azure Depolama hizmetlerinin her biri için performans hedefleri anlayın."
services: storage
documentationcenter: na
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: be721bd3-159f-40a1-88c1-96418537fe75
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 07/12/2017
ms.author: robinsh
ms.openlocfilehash: 7afe4366a02887b4e3d9781c26c8adda81adce95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a>Azure Depolama Ölçeklenebilirlik ve Performans Hedefleri
## <a name="overview"></a>Genel Bakış
Bu konuda, Microsoft Azure Storage için hello ölçeklenebilirlik ve performans konuları açıklanmaktadır. Diğer Azure sınırları özeti için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../../azure-subscription-service-limits.md).

> [!NOTE]
> Tüm depolama hesapları hello yeni düz ağ topolojisini çalıştırın ve ne zaman oluşturulduğu bağımsız olarak, aşağıda açıklanan hello ölçeklenebilirlik ve performans hedefleri destekler. Ölçeklenebilirlik ve hello Azure depolama düz ağ mimarisi üzerinde daha fazla bilgi için bkz: [Microsoft Azure Storage: yüksek oranda kullanılabilir bulut depolama hizmet güçlü tutarlılık](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).
> 
> [!IMPORTANT]
> Burada listelenen hello ölçeklenebilirlik ve performans hedefleri Gelişmiş hedefleri, ancak ulaşılabilir. Tüm durumlarda hello istek oranı ve depolama hesabınız tarafından elde edilen bant genişliği bağlıdır saklanan nesneleri hello boyutuna bağlı hello erişim desenlerini kullanılan ve uygulamanızı gerçekleştiren iş yükü türünü hello. Kendi performans gereksinimlerinizi karşılayıp karşılamadığını emin tootest hizmet toodetermine olabilir. Mümkünse, trafik hello oranı ani ani önlemek ve bölümler trafiği iyi dağıtılmış olduğundan emin olun.
> 
> Uygulamanızın ne bir bölüm için iş yükünü işleyebilir, hello sınırına ulaştığında, Azure Storage tooreturn hata kodu 503 (Sunucu meşgul) başlar veya hata kodu: 500 (işlemi zaman aşımı) yanıtlar. Bu durumda, Merhaba uygulaması için yeniden deneme üstel geri alma İlkesi kullanmanız gerekir. Merhaba üstel geri alma trafiği toothat bölümünde hello yük hello bölüm toodecrease ve tooease ani çıkışı sağlar.
> 
> 

Hello uygulamanızın veya tek bir depolama hesabına hello ölçeklenebilirlik hedefleri aşarsa, uygulama toouse birden çok depolama hesabı oluşturun ve bu depolama hesapları arasında veri nesnelerinizi bölüm. Bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/) birim fiyatlandırma hakkında bilgi için.

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a>BLOB, kuyruklar, tablolar ve dosyalar için ölçeklenebilirlik hedefleri
[!INCLUDE [azure-storage-limits](../../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
## <a name="scalability-targets-for-virtual-machine-disks"></a>Sanal makine disklerini için ölçeklenebilirlik hedefleri
[!INCLUDE [azure-storage-limits-vm-disks](../../../includes/azure-storage-limits-vm-disks.md)]

Bkz: [Windows VM boyutları](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) veya [Linux VM boyutları](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ek ayrıntılar için.

## <a name="managed-virtual-machine-disks"></a>Yönetilen sanal makine disklerini

[!INCLUDE [azure-storage-limits-vm-disks-managed](../../../includes/azure-storage-limits-vm-disks-managed.md)]

## <a name="unmanaged-virtual-machine-disks"></a>Yönetilmeyen sanal makine disklerini
[!INCLUDE [azure-storage-limits-vm-disks-standard](../../../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../../../includes/azure-storage-limits-vm-disks-premium.md)]

## <a name="scalability-targets-for-azure-resource-manager"></a>Azure kaynak yöneticisi için ölçeklenebilirlik hedefleri
[!INCLUDE [azure-storage-limits-azure-resource-manager](../../../includes/azure-storage-limits-azure-resource-manager.md)]

## <a name="partitions-in-azure-storage"></a>Azure depolama alanında bölümleri
Azure Storage (BLOB'ları, iletileri, varlıkları ve dosyaları) depolanan verileri tutar her nesne tooa bölüm ait ve bir bölüm anahtar tarafından tanımlanır. Merhaba bölüm, nasıl Azure depolama yükünü sunucuları toomeet hello trafiği ihtiyaçlarını bu nesneler arasında BLOB'ları, iletileri, varlıkları ve dosyaları dengeleyen belirler. Merhaba bölüm anahtarı benzersizdir ve kullanılan toolocate bir blob, ileti veya varlık kümesidir.

Yukarıda gösterilen hello tablo [standart depolama hesapları için ölçeklenebilirlik hedefleri](#standard-storage-accounts) listeleri hello performans hedefleri her hizmet için tek bir bölüm için.

Bölümler, her bir yolu aşağıdaki hello hello depolama hizmetleri için Yük Dengeleme ve ölçeklenebilirlik etkiler:

* **BLOB'ları**: hello bölüm anahtarı bir blob için olan hesap adını, kapsayıcı adı + blob adı. Başka bir deyişle, her bir blob hello blob üzerindeki yükü, talep varsa, kendi bölümü olabilir. BLOB'ları erişim toothem çıkış sırası tooscale çok sayıda sunucuya dağıtılmış olabilir, ancak tek bir blob yalnızca tek bir sunucu tarafından sunulabilen. BLOB'ları blob kapsayıcı mantıksal olarak gruplandırılabilir olsa da, bu gruplandırma bölümleme hiçbir etkileri vardır.
* **Dosyaları**: hello bölüm anahtarı bir dosya için hesabıdır adı + dosya paylaşımı adı. Bu, bir dosya paylaşımında tüm dosyaları da tek bir bölüm olduğu anlamına gelir.
* **İletileri**: hello bölüm anahtarı için bir ileti olduğundan hello hesap adı + kuyruk adı, sıradaki tüm iletileri tek bir bölümde gruplandırılır ve tek bir sunucu tarafından sunulan. Farklı sıraları toobalance hello yük için çok sayıda sıraları bir depolama hesabına sahip ancak farklı sunucular tarafından işlenebilir.
* **Varlıkları**: hello bölüm anahtarı bir varlık için hesap adı + tablo adı + hello bölüm anahtarı gerekli hello hello değeri olduğu bölüm anahtarı, kullanıcı tarafından tanımlanan **PartitionKey** hello varlığın özelliği. Aynı bölüm anahtarı değerini aynı bölüm ve aynı hello tarafından sunulan hello gruplandırılır hello tüm varlıklarla sunucu bölüm. Uygulamanızı tasarlamanın önemli bir nokta toounderstand budur. Uygulamanızı hello ölçeklenebilirlik avantajlarını, tek bir bölüm varlıklarda gruplandırma hello veri erişim yararları birden çok bölüm arasında varlıklar yayılmak dengelemeniz.  

Önemli bir avantajı toogrouping kümesine tek bir bölüm varlıklar bir tabloda, olası tooperform atomik toplu işlemleri bir bölüm tek bir sunucu üzerinde mevcut olduğundan aynı, bölüm hello varlıklar arasında olmasıdır. Toplu işlem varlık grubunun tooperform istiyorsanız, bu nedenle, hello ile gruplandırma düşünün aynı bölüm anahtarı. 

Üzerindeki diğer yandan Merhaba, aynı tablo ancak farklı bölüm anahtarlarının sahip hello olan varlıkları olası toohave daha yüksek ölçeklenebilirlik kolaylaştırarak farklı sunucular arasında dengeli olabilir.

Ayrıntılı tablolar bulunabilir stratejisi bölümleme tasarlama için öneriler [burada](https://msdn.microsoft.com/library/azure/hh508997.aspx).

## <a name="see-also"></a>Ayrıca Bkz.
* [Depolama fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/storage/)
* [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../../azure-subscription-service-limits.md)
* [Premium Depolama: Azure Sanal Makine İş Yükleri için Yüksek Performanslı Depolama](../storage-premium-storage.md)
* [Azure Storage çoğaltma](../storage-redundancy.md)
* [Microsoft Azure depolama performans ve ölçeklenebilirlik Yapılacaklar listesi](../storage-performance-checklist.md)
* [Microsoft Azure Storage: Yüksek oranda kullanılabilir depolama sahip bulut hizmeti güçlü tutarlılık](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

