---
title: "Azure VM'ler için aaaDisaster kurtarma senaryoları | Microsoft Docs"
description: "Bir Azure hizmet kesintisi Azure sanal makineleri etkiler hello olay hangi toodo öğrenin."
services: virtual-machines
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 65272148-ff06-4bce-91f1-851d706d4d40
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: kmouss;aglick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 839c6f9c51a7f35b48ef3636bc346eef332bb06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-that-an-azure-service-disruption-impacts-azure-vms"></a>Hangi toodo hello olay bir Azure hizmet kesintisi Azure sanal makineleri etkiler
Microsoft, sabit toomake gereksinim duyduğunuzda hizmetlerimizle her zaman kullanılabilir tooyou emin çalışır. Bizim denetim ötesinde zorlar bazen bize planlanmamış hizmet kesintilerine neden şekillerde etkiler.

Microsoft açık kalma süresi ve bağlantı için taahhüdü olarak hizmetlerinin için bir hizmet düzeyi sözleşmesi (SLA) sağlar. tek tek Azure Hizmetleri için başlangıç SLA bulunabilir [Azure hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/).

Azure, yüksek oranda kullanılabilir uygulamaları destekleyen birçok yerleşik platform özellikleri zaten var. Bu hizmetler hakkında daha fazla bilgi için okuma [Azure uygulamaları için yüksek kullanılabilirlik ve olağanüstü durum kurtarma](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

Tüm bölge kesinti son toomajor doğal afet veya yaygın bir hizmet kesintisi yaşadığında bu makalede bir true olağanüstü durum kurtarma senaryosunda kapsar. Nadir oluşum bunlar, ancak tüm bölgesinin bir kesinti olduğunu hello olasılığı için hazırlamanız gerekir. Tüm bir bölgeyi hizmet kesintisi yaşarsa, verilerinizin yerel olarak yedekli kopyasını hello geçici olarak kullanılamaz durumda olurdu. Coğrafi çoğaltma etkinleştirildiğinde, tabloları ve Azure Storage bloblarında üç ek kopyalarını farklı bir bölgede depolanır. Tam bölgesel bir kesintinin veya hangi hello birincil bölge kurtarılamaz olağanüstü durum Hello olayda Azure tüm hello DNS girişlerini toohello bölgenin coğrafi olarak çoğaltılmış remaps.

Bu nadir örnekleri ele toohelp, Azure sanal makinesi uygulamanızı dağıtıldığı hello tüm bölgenin hizmet kesintisi hello durumda Azure sanal makineleri için yönergeleri uygulayarak hello sunuyoruz.

## <a name="option-1-initiate-a-failover-by-using-azure-site-recovery"></a>Seçenek 1: Azure Site Recovery kullanarak bir yük devretme başlatın.
Tek bir tıklatmayla sağlasa da, uygulamanızın dakika kurtarabilmeleri için Azure Site Recovery Vm'leriniz için yapılandırabilirsiniz. Tercih ettiğiniz tooAzure bölgesini ve Kısıtlanmamış toopaired bölgeleri çoğaltabilirsiniz. Tarafından başlayabiliriz [sanal makinelerinizi çoğaltma](https://aka.ms/a2a-getting-started). Yapabilecekleriniz [bir kurtarma planı oluşturma](../site-recovery/site-recovery-create-recovery-plans.md) böylece uygulamanız için hello tüm yük devretme işlemini otomatik hale getirebilirsiniz. Yapabilecekleriniz [, yük devretme testi](../site-recovery/site-recovery-test-failover-to-azure.md) önceden üretim uygulama veya hello devam eden çoğaltmayı etkileyen olmadan. Bir birincil bölge kesintisi Hello olayda yeni [bir yük devretme başlatın](../site-recovery/site-recovery-failover.md) ve uygulamanızı hedef bölgede duruma getirin.


## <a name="option-2-wait-for-recovery"></a>Seçenek 2: Kurtarma için bekleyin
Bu durumda, herhangi bir eyleminiz gereklidir. Titizlikle toorestore hizmet kullanılabilirliği çalışıyoruz olduğunu bilirsiniz. Merhaba geçerli hizmet durumu görebilirsiniz bizim [Azure hizmet sağlığı panosunu](https://azure.microsoft.com/status/).

Azure Site Recovery, coğrafi olarak yedekli depolamaya okuma erişimi veya coğrafi olarak yedekli depolama önceki toohello kesintisi ayarlamadıysanız hello en iyi seçenek budur. Coğrafi olarak yedekli depolama veya okuma erişimli coğrafi olarak yedekli depolama hello depolama hesabı için VM sanal sabit diskleri (VHD) depolandığı ayarlamış olmanız durumunda toorecover hello temel görüntü VHD bakın ve tooprovision yeni bir VM'den deneyin. Veri Eşitleme garanti olduğundan, tercih edilen bir seçenek değil. Sonuç olarak, bu seçenek toowork garanti edilmez.


> [!NOTE]
> Bu işlem üzerinde herhangi bir denetim yoktur ve yalnızca bölge genelinde hizmet kesilmelerini meydana gelir unutmayın. Bu nedenle, aynı zamanda diğer uygulamaya özgü yedekleme stratejilerini tooachieve hello yüksek düzeyde kullanılabilirlik üzerinde kullanmanız gerekir. Daha fazla bilgi için üzerinde hello bölümüne bakın. [olağanüstü durum kurtarma veri stratejileri](https://docs.microsoft.com/azure/architecture/resiliency/disaster-recovery-azure-applications#data-strategies-for-disaster-recovery).
>
>

## <a name="next-steps"></a>Sonraki adımlar

- Başlat [Azure sanal makinelerde çalışan uygulamalarınızı korumaya](https://aka.ms/a2a-getting-started) Azure Site RECOVERY'yi kullanarak

- toolearn tooimplement bir olağanüstü durum kurtarma ve yüksek kullanılabilirlik stratejinizi nasıl görürüm hakkında daha fazla [Azure uygulamaları için yüksek kullanılabilirlik ve olağanüstü durum kurtarma](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

- toodevelop bir bulut platformun özellikleri ayrıntılı teknik bir anlayış bkz [Azure dayanıklılık teknik kılavuz](../resiliency/resiliency-technical-guidance.md).


- Merhaba yönergeleri açık değilse veya Microsoft toodo hello işlemleri sizin adınıza isterseniz başvurun [müşteri desteği](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
