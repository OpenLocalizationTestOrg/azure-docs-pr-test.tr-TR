---
title: "Azure Storage ölçeklenebilirlik ve performans hedefleri | Microsoft Docs"
description: "Azure depolama kapasitesi, istek hızı ve her iki standart ve premium depolama hesapları için gelen ve giden bant genişliği de dahil olmak üzere, ölçeklenebilirlik ve performans hedefleri hakkında bilgi edinin. Bölümler içinde Azure Storage hizmetlerinin her biri için performans hedefleri anlayın."
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
ms.openlocfilehash: 47a1d2b87269d40716b3dae02276207060b41c24
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-scalability-and-performance-targets"></a>Azure Depolama Ölçeklenebilirlik ve Performans Hedefleri
## <a name="overview"></a>Genel Bakış
Bu konuda, Microsoft Azure Storage ölçeklenebilirlik ve performans konuları açıklanmaktadır. Diğer Azure sınırları özeti için bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../../azure-subscription-service-limits.md).

> [!NOTE]
> Tüm depolama hesaplarının yeni düz ağ topolojisine çalıştırın ve ne zaman oluşturulduğu bağımsız olarak, aşağıda açıklanan ölçeklenebilirlik ve performans hedefleri destekler. Ölçeklenebilirlik ve Azure depolama düz ağ mimarisi üzerinde daha fazla bilgi için bkz: [Microsoft Azure Storage: yüksek oranda kullanılabilir bulut depolama hizmet güçlü tutarlılık](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).
> 
> [!IMPORTANT]
> Burada listelenen ölçeklenebilirlik ve performans hedefleri Gelişmiş hedefleri, ancak ulaşılabilir. Uygulamanızı iş yükü türünü gerçekleştirir ve tüm durumlarda, istek hızı ve bant genişliği, depolama birimi tarafından elde saklanan nesneleri kullanılan, erişim desenlerini boyutuna bağlı hesap bağlıdır. Hizmetinizin performansını gereksinimlerinizi karşılayıp karşılamadığını belirlemek için test emin olun. Mümkünse, trafiğinin oranını içindeki ani ani önlemek ve bölümler trafiği iyi dağıtılmış olduğundan emin olun.
> 
> Uygulamanızın ne bir bölüm için iş yükünü işleyebilir, sınırına ulaştığında, Azure depolama hata kodu 503 (Sunucu meşgul) veya hata kodu 500 (işlemi zaman aşımı) yanıtları döndürülecek başlar. Bu durumda, uygulama için yeniden deneme üstel geri alma İlkesi kullanmanız gerekir. Üstel geri alma yükü azaltmak ve o bölümün trafiğinin ani çıkışı kolaylaştırmak için bölüm olanak tanır.
> 
> 

Uygulamanızın gereksinimlerine tek bir depolama hesabı ölçeklenebilirlik hedeflerini aşarsa, birden çok depolama hesabı kullanmak için uygulamanızı oluşturmak ve bu depolama hesapları arasında veri nesnelerinizi bölüm. Bkz: [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/) birim fiyatlandırma hakkında bilgi için.

## <a name="scalability-targets-for-blobs-queues-tables-and-files"></a>BLOB, kuyruklar, tablolar ve dosyalar için ölçeklenebilirlik hedefleri
[!INCLUDE [azure-storage-limits](../../../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies to unmanaged and managed -->
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
Azure Storage (BLOB'ları, iletileri, varlıkları ve dosyaları) depolanan verileri tutar her nesne bir bölüme ait ve bir bölüm anahtar tarafından tanımlanır. Bölüm, nasıl Azure depolama yükünü bu nesneler trafiği ihtiyaçlarını karşılamak için sunucular arasında BLOB'ları, iletileri, varlıkları ve dosyaları dengeleyen belirler. Bölüm anahtarı benzersizdir ve blob, ileti veya varlık bulmak için kullanılır.

Yukarıda gösterilen tablo [standart depolama hesapları için ölçeklenebilirlik hedefleri](#standard-storage-accounts) her hizmet için tek bir bölüm için performans hedefleri listeler.

Bölümler Yük Dengeleme ve ölçeklenebilirlik her depolama hizmetleri için aşağıdaki şekillerde etkiler:

* **BLOB'ları**: blob bölüm anahtarı olan hesap adını, kapsayıcı adı + blob adı. Başka bir deyişle, her bir blob blob üzerindeki yükü, talep varsa, kendi bölümü olabilir. BLOB'ları onlara erişimi genişletmek için birçok sunucular arasında dağıtılabilir, ancak tek bir blob yalnızca tek bir sunucu tarafından sunulabilen. BLOB'ları blob kapsayıcı mantıksal olarak gruplandırılabilir olsa da, bu gruplandırma bölümleme hiçbir etkileri vardır.
* **Dosyaları**: bölüm anahtarı için bir dosya adı + dosya paylaşımı adı hesabıdır. Bu, bir dosya paylaşımında tüm dosyaları da tek bir bölüm olduğu anlamına gelir.
* **İletileri**: sıradaki tüm iletileri tek bir bölümde gruplandırılır tek bir sunucu tarafından sunulan bir ileti için bölüm anahtarı hesap adı + kuyruk adı olduğundan ve. Farklı kuyruklar birçok sıraları bir depolama hesabına sahip ancak için yükü dengelemek için farklı sunucular tarafından işlenebilir.
* **Varlıkları**: bölüm anahtarı bir varlık için hesap adı + tablo adı + bölüm anahtarı, bölüm anahtarı değerini gereken kullanıcı tanımlı olduğu **PartitionKey** varlığın özelliği. Aynı bölüm anahtarı değerine sahip tüm varlıkları aynı bölüme gruplandırılır ve aynı bölüm sunucu tarafından sunulan. Bu, uygulamanızın tasarlarken anlamak için önemli bir noktadır. Uygulamanızın veri erişim avantajları, tek bir bölüm varlıklarda gruplandırma birden çok bölüm arasında varlıklar yayılmak ölçeklenebilirlik avantajlarını dengelemeniz.  

Varlıklar bir tablodaki bir dizi tek bir bölümde gruplandırmak için önemli bir avantajı bir bölüm tek bir sunucu üzerinde mevcut olduğundan aynı bölüme varlıklar arasında atomik toplu işlemleri gerçekleştirmek olası olmasıdır. Bir grup varlıkların toplu işlemleri gerçekleştirmek isterseniz, bu nedenle, aynı bölüm anahtarı ile gruplandırma göz önünde bulundurun. 

Diğer taraftan, aynı olan varlıkları tablo ancak farklı bölüm anahtarları daha yüksek ölçeklenebilirlik olası hale getirerek farklı sunucular arasında yük dengeli.

Ayrıntılı tablolar bulunabilir stratejisi bölümleme tasarlama için öneriler [burada](https://msdn.microsoft.com/library/azure/hh508997.aspx).

## <a name="see-also"></a>Ayrıca Bkz.
* [Depolama fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/storage/)
* [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../../azure-subscription-service-limits.md)
* [Premium Depolama: Azure Sanal Makine İş Yükleri için Yüksek Performanslı Depolama](../storage-premium-storage.md)
* [Azure Storage çoğaltma](../storage-redundancy.md)
* [Microsoft Azure depolama performans ve ölçeklenebilirlik Yapılacaklar listesi](../storage-performance-checklist.md)
* [Microsoft Azure Storage: Yüksek oranda kullanılabilir depolama sahip bulut hizmeti güçlü tutarlılık](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

