---
title: "Azure Cloud Services etkiler bir Azure hizmet kesintisi hello olayı içinde aaaWhat toodo | Microsoft Docs"
description: "Azure Cloud Services etkiler bir Azure hizmet kesintisi hello olayı içinde hangi toodo öğrenin."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: e52634ab-003d-4f1e-85fa-794f6cd12ce4
ms.service: cloud-services
ms.workload: cloud-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: mmccrory
ms.openlocfilehash: bb1f1835fc91a23772f81801b67d5786c190ba19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-in-hello-event-of-an-azure-service-disruption-that-impacts-azure-cloud-services"></a>Azure Cloud Services etkiler bir Azure hizmet kesintisi hello olayı içinde hangi toodo
Microsoft, sabit toomake gereksinim duyduğunuzda hizmetlerimizle her zaman kullanılabilir tooyou emin çalışır. Bizim denetim ötesinde zorlar bazen bize planlanmamış hizmet kesintilerine neden şekillerde etkiler.

Microsoft açık kalma süresi ve bağlantı için taahhüdü olarak hizmetlerinin için bir hizmet düzeyi sözleşmesi (SLA) sağlar. tek tek Azure Hizmetleri için başlangıç SLA bulunabilir [Azure hizmet düzeyi sözleşmeleri](https://azure.microsoft.com/support/legal/sla/).

Azure, yüksek oranda kullanılabilir uygulamaları destekleyen birçok yerleşik platform özellikleri zaten var. Bu hizmetler hakkında daha fazla bilgi için okuma [Azure uygulamaları için yüksek kullanılabilirlik ve olağanüstü durum kurtarma](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

Tüm bölge kesinti son toomajor doğal afet veya yaygın bir hizmet kesintisi yaşadığında bu makalede bir true olağanüstü durum kurtarma senaryosunda kapsar. Nadir oluşum bunlar, ancak tüm bölgesinin bir kesinti olduğunu hello olasılığı için hazırlamanız gerekir. Tüm bir bölgeyi hizmet kesintisi yaşarsa, verilerinizin yerel olarak yedekli kopyasını hello geçici olarak kullanılamaz durumda olurdu. Coğrafi çoğaltma etkinleştirildiğinde, tabloları ve Azure Storage bloblarında üç ek kopyalarını farklı bir bölgede depolanır. Tam bölgesel bir kesintinin veya hangi hello birincil bölge kurtarılamaz olağanüstü durum Hello olayda Azure tüm hello DNS girişlerini toohello bölgenin coğrafi olarak çoğaltılmış remaps.

> [!NOTE]
> Bu işlemi üzerinde hiçbir denetimi yoktur ve yalnızca veri merkezi çapında hizmet kesilmelerini meydana gelir unutmayın. Bu nedenle, aynı zamanda diğer uygulamaya özgü yedekleme stratejilerini tooachieve hello yüksek düzeyde kullanılabilirlik üzerinde kullanmanız gerekir. Daha fazla bilgi için bkz: [Microsoft Azure üzerinde oluşturulan uygulamalar için yüksek kullanılabilirlik ve olağanüstü durum kurtarma](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md). Toobe mümkün tooaffect isterseniz kendi yük devretme tooconsider hello kullanımını isteyebilirsiniz [okuma erişimli coğrafi olarak yedekli depolama (RA-GRS)](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage), başka bir bölgede verilerinizin salt okunur bir kopyasını oluşturur.
>
>


## <a name="option-1-use-a-backup-deployment-through-azure-traffic-manager"></a>Seçenek 1: yedekleme dağıtım aracılığıyla Azure trafik Yöneticisi'ni kullanın
Merhaba en güçlü olağanüstü durum kurtarma çözümü içerir farklı bölgelerde, uygulamanızın birden çok dağıtım koruyarak ve ardından kullanarak [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) aralarındaki toodirect trafik. Azure Traffic Manager sağlayan birden çok [yönlendirme yöntemleri](../traffic-manager/traffic-manager-routing-methods.md), toomanage arasındaki birincil/yedekleme modeli veya toosplit kullanarak dağıtımlarınızı trafiği olup olmadığını seçebilmeniz bunları.

![Bölgelere Azure Traffic Manager ile Azure Cloud Services Dengeleme](./media/cloud-services-disaster-recovery-guidance/using-azure-traffic-manager.png)

Merhaba en hızlı yanıt toohello kaybı bir bölge için trafik Yöneticisi'nin yapılandırma önemli [uç nokta izleme](../traffic-manager/traffic-manager-monitoring.md).

## <a name="option-2-deploy-your-application-tooa-new-region"></a>Seçenek 2: uygulama tooa yeni bölge dağıtma
Merhaba önceki seçeneğinde açıklandığı gibi birden fazla etkin dağıtımlarını sürdürme ek devam eden maliyetler doğurur. Kurtarma süresi hedefi (RTO) yeterince esnektir ve hello özgün kod veya derlenmiş bulut Hizmetleri paket varsa, başka bir bölgede, uygulamanızın yeni bir örneğini oluşturmak ve DNS kayıtları toopoint toohello yeni dağıtımınızı güncelleştirin.

Nasıl hakkında daha fazla ayrıntı için toocreate ve bir bulut hizmeti uygulaması dağıtma, bkz: [nasıl toocreate ve bir bulut hizmeti dağıtma](cloud-services-how-to-create-deploy-portal.md).

Uygulama veri kaynaklarınıza bağlı olarak, uygulama veri kaynağı için toocheck hello kurtarma yordamları gerekebilir.

* Azure Storage veri kaynakları için bkz: [Azure Storage çoğaltma](../storage/common/storage-redundancy.md#read-access-geo-redundant-storage) toocheck hello üzerinde temel kullanılabilir hello seçenekleri seçtiğiniz uygulamanız için çoğaltma modeli.
* SQL veritabanı kaynakları için okuma [genel bakış: Bulut iş devamlılığı ve veritabanı olağanüstü durum kurtarma SQL Database](../sql-database/sql-database-business-continuity.md) toocheck kullanılabilir hello seçenekleri hakkında temel alarak, uygulamanız için seçilen hello çoğaltma modeli.


## <a name="option-3-wait-for-recovery"></a>Seçenek 3: Kurtarma için bekleyin
Bu durumda, herhangi bir eyleminiz gereklidir, ancak hello bölge geri yüklenene kadar hizmet kullanılamaz. Merhaba üzerinde hello geçerli hizmet durumu görebilirsiniz [Azure hizmet sağlığı panosunu](https://azure.microsoft.com/status/).

## <a name="next-steps"></a>Sonraki adımlar
toolearn tooimplement bir olağanüstü durum kurtarma ve yüksek kullanılabilirlik stratejinizi nasıl görürüm hakkında daha fazla [Azure uygulamaları için yüksek kullanılabilirlik ve olağanüstü durum kurtarma](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

toodevelop bir bulut platformun özellikleri ayrıntılı teknik bir anlayış bkz [Azure dayanıklılık teknik kılavuz](../resiliency/resiliency-technical-guidance.md).
