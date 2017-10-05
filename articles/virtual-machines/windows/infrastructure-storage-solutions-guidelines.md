---
title: "Azure'da Windows sanal makineleri için depolama çözümleri | Microsoft Docs"
description: "Azure altyapı Hizmetleri'nde depolama çözümlerini dağıtma anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ceb7d32-7a0d-4004-b701-c2bbcaff6b0b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ba0d66c5af771ebcb3ca8e6742e15a5506d8fd61
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-windows-vms"></a>Windows sanal makineleri için Azure depolama altyapısı yönergeleri

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Bu makalede, depolama gereksinimlerini ve sanal makine (VM) en iyi performans elde etmek için tasarım konuları anlamaya odaklanır.

## <a name="implementation-guidelines-for-storage"></a>Depolama için uygulama rehberi
Kararları:

* Azure diskleri yönetilen veya yönetilmeyen diskleri kullanmak için yapacaksınız?
* İş yükü için standart veya Premium storage'ı kullanma gerekiyor mu?
* Diskler 4 TB'den büyük oluşturmak için disk şeritleme gerekiyor mu?
* İş yükü için en iyi g/ç performansı elde etmek için disk şeritleme gerekiyor mu?
* Hangi depolama hesaplarının BT iş yükü veya altyapı barındırmak gerekiyor mu?

Görevler:

* G/ç gereksinimlerini dağıtıyorsanız ve uygun sayıda ve depolama hesapları türünü planlama uygulamaları gözden geçirin.
* Depolama hesapları, adlandırma kuralını kullanarak kümesini oluşturun. Azure PowerShell veya portalı kullanabilirsiniz.

## <a name="storage"></a>Depolama
Azure depolama, sanal makineleri (VM'ler) ve uygulamaları dağıtma ve yönetme, önemli bir parçasıdır. Sanal makineleri destekleyen altyapı parçası olduğunu da ve Azure depolama dosya verileri, yapılandırılmamış verilerinizi ve iletileri depolamak için hizmetler sağlar.

[Azure yönetilen diskleri](../../storage/storage-managed-disks-overview.md) depolama arka planda işler. Yönetilmeyen disklerle Azure Vm'leriniz için diskleri (VHD dosyaları) tutmak için depolama hesapları oluşturun. Yukarı ölçeklendirilirken tüm disklerinizi depolama IOPS sınırı aşmayan için ek depolama hesapları oluşturulan emin olmanız gerekir. Yönetilen depolama işleme diskler ile depolama hesabı sınırları tarafından artık sınırlıdır (20.000 IOPS gibi / hesabını). Ayrıca artık birden çok depolama hesabı için kendi özel görüntülerinizi (VHD dosyaları) kopyalamanız gerekir. Bunları merkezi bir konumda – Azure bölgesi başına bir depolama hesabı – yönetebilir ve bunları bir abonelikte VM'ler yüzlerce oluşturmak için kullanın. Yeni dağıtımlar için yönetilen diskleri kullanmanızı öneririz.

Sanal makineleri desteklemek için kullanılabilen iki tür depolama hesabı vardır:

* Table storage, kuyruk depolama ve dosya depolama (Azure VM diskleri depolamak için kullanılan) blob depolama alanına erişim standart depolama hesapları verin.
* [Premium depolama](../../storage/storage-premium-storage.md) hesapları teslim g/ç yoğun iş yükleri için bir AlwaysOn kümedeki SQL sunucuları gibi yüksek performanslı, düşük gecikmeli disk desteği. Premium depolama şu anda yalnızca Azure VM diskleri destekler.

Azure, bir işletim sistemi diski, geçici bir disk ve sıfır veya daha fazla isteğe bağlı veri diskleri VM'ler oluşturur. Geçici disk nerede makine yaşıyor düğümde yerel olarak depolanan ise işletim sistemi diski ve veri diskleri Azure sayfa bloblarını olur. VM bir bakım olayı sırasında konaklar arasında geçişi yapılacak olarak yalnızca bu geçici disk kalıcı olmayan verileri için kullanılacak uygulamaları tasarlarken dikkatli olun. Geçici diskte depolanan tüm verileri kaybolacak.

Dayanıklılık ve yüksek kullanılabilirlik, verilerinizi planlanmamış Bakım veya donanım arızalarına karşı korumalı kaldığından emin olmak için temel alınan Azure depolama ortamı tarafından sağlanır. Azure depolama ortamınızı tasarlarken, VM depolama çoğaltmak seçebilirsiniz:

* yerel olarak bir belirtilen Azure veri merkezi içinde
* belirli bir bölgedeki içerisinde Azure veri merkezi arasında
* farklı bölgelere Azure veri merkezi arasında

Okuyabilirsiniz [yüksek kullanılabilirlik için çoğaltma seçenekleri hakkında daha fazla](../../storage/storage-introduction.md#replication-for-durability-and-high-availability).

İşletim sistemi ve veri disklerle 4 TB maksimum boyuta sahip. Veri diskleri mantıksal birimler 4 TB'den büyük VM'nize sunmak için birlikte havuzu tarafından bu sınırı aşan depolama alanları Windows Server 2012 veya sonraki sürümlerinde kullanabilirsiniz.

Bazı ölçeklenebilirlik sınırları - daha fazla bilgi için Azure Storage dağıtımlarınızın tasarlarken bkz [Microsoft Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../../azure-subscription-service-limits.md#storage-limits). Ayrıca bkz. [Azure storage ölçeklenebilirlik ve performans hedefleri](../../storage/storage-scalability-targets.md).

Uygulama depolaması için belgeler, görüntüler, yedeklemeler, yapılandırma verileri, günlükleri, vb. gibi yapılandırılmamış nesne verilerini depolayabilir. BLOB storage kullanarak. Uygulamanızı yerine VM'ye bağlı bir sanal disk yazma uygulama doğrudan Azure blob depolama alanına yazabilirsiniz. BLOB Depolama Birimi, bir seçenek de sağlar [sık erişimli ve seyrek erişimli depolama katmanları](../../storage/storage-blob-storage-tiers.md) kullanılabilirlik gereksinimlerini ve maliyet kısıtlamaları bağlı olarak.

## <a name="striped-disks"></a>Şeritli diskleri
Çoğu durumda, 4 TB'den büyük diskler oluşturmanızı sağlayan yanı sıra veri diskleri için şeritleme kullanarak performans tek bir birimde depolama yedeklemek birden çok BLOB vererek geliştirir. Şeritleme ile paralel olarak yazmak ve tek bir mantıksal diskten verileri okumak için gerekli g/ç işlemi devam eder.

Azure veri diski sayısı ve VM boyutuna bağlı olarak kullanılabilir bant genişliği miktarını sınırlar uygular. Ayrıntılar için bkz [sanal makineler için Boyutlar](sizes.md).

Azure veri diski için disk şeritleme kullanıyorsanız, aşağıdaki yönergeleri dikkate alın:

* VM boyutu için izin verilen maksimum veri diskleri bağlayın.
* Depolama alanları kullanın.
* Azure veri diski önbelleğe alma seçeneklerini kullanmaktan kaçının (ilke önbelleğe alma = yok).

Daha fazla bilgi için bkz: [depolama alanları - performans için tasarlama](http://social.technet.microsoft.com/wiki/contents/articles/15200.storage-spaces-designing-for-performance.aspx).

## <a name="multiple-storage-accounts"></a>Birden çok depolama hesabı
Bu bölümde uygulanmaz [Azure yönetilen diskleri](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)ayrı depolama hesapları oluşturma gibi. 

Yönetilmeyen diskler için Azure Storage ortamınızı tasarlarken, birden çok depolama hesabı kullanabilirsiniz VM'lerin sayısını dağıttığınız artar. Bu yaklaşım, g/ç VM'ler ve uygulamalar için en iyi performansı korumak için Azure Storage altyapının dağıtmasına yardımcı olur. Dağıttığınız uygulamaları tasarlarken, her VM sahip g/ç gereksinimleri ve bu VM'lerin dengeyi Azure depolama hesapları arasında göz önünde bulundurun. Yalnızca bir veya iki depolama hesaplarına Vm'lerde yoğun tüm yüksek g/ç gruplandırma kaçınmaya çalışın.

G/ç özelliklerine farklı Azure depolama seçenekleri hakkında daha fazla bilgi ve bazı öneri üst sınırlar için bkz: [Azure storage ölçeklenebilirlik ve performans hedefleri](../../storage/storage-scalability-targets.md).

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

