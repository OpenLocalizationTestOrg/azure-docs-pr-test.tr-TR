---
title: "azure'da Windows sanal makineleri için aaaAvailability kümesi | Microsoft Docs"
description: "Azure altyapı Hizmetleri'nde kullanılabilirlik kümeleri dağıtmak için hello anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f9449f58-664b-4d5d-82f6-84c5d083047f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cc35fd1e913434d9facb94116edb1b1c30447c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-availability-sets-guidelines-for-windows-vms"></a>Azure kullanılabilirlik yönergeleri Windows VM'ler için ayarlar

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Bu makalede gerekli anlama hello üzerinde odaklanır kullanılabilirlik tooensure uygulamalarınızı ayarlar için planlama adımları kalır erişilebilir sırasında planlanmış veya planlanmamış olaylar.

## <a name="implementation-guidelines-for-availability-sets"></a>Kullanılabilirlik kümeleri için uygulama rehberi
Kararları:

* Kaç tane kullanılabilirlik kümeleri, hello için çeşitli rolleri ve katmanları uygulama altyapınızda gerekiyor mu?

Görevler:

* VM Hello sayısı ihtiyaç duyduğunuz her uygulama katmanında tanımlayın.
* Uygulamanız için kullanılan hatası veya güncelleştirme etki alanları toobe tooadjust hello sayısı gerekip gerekmediğini belirleyin.
* Adlandırma kuralı ve ne kullanarak gerekli hello kullanılabilirlik kümelerini tanımlayın VM'ler bunları bulunur. Bir VM, bir kullanılabilirlik kümesinde yalnızca bulunabilir.

## <a name="availability-sets"></a>Kullanılabilirlik kümeleri
Azure'da sanal makineleri (VM'ler) olarak adlandırılan bir kullanılabilirlik kümesi tooa mantıksal gruplandırma yerleştirilebilir. Sanal makineleri bir kullanılabilirlik kümesi içinde oluşturduğunuzda, hello Azure platformu bu VM'lerin hello yerleştirme altyapısını temel hello arasında dağıtır. Planlanan bakım olayı toohello Azure platformu veya temel alınan donanım var olmalıdır / altyapı arıza, kullanılabilirlik kümeleri hello kullanımı en az bir VM çalışan kalmasını sağlar.

En iyi uygulama, uygulamaları tek bir VM üzerinde bulunmalıdır değil. Tek bir VM'ye içeren bir kullanılabilirlik kümesi planlanmış veya planlanmamış olaylardan hello Azure platformu içinde herhangi bir koruma sahip değil. Merhaba [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines) bir kullanılabilirlik kümesi tooallow hello VM'ler arasında dağıtımı altyapısını temel hello içinde iki veya daha fazla VM gerektirir. Kullanıyorsanız [Azure Premium Storage](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello Azure SLA geçerlidir tooa tek VM.

azure'da Hello altyapının toomultiple donanım kümelerde ayrılmıştır. Her donanım küme aralığı, VM boyutlarını destekler. Bir kullanılabilirlik kümesi, yalnızca zaman içinde herhangi bir noktada tek donanım kümede barındırılabilir. Bu nedenle, bir tek kullanılabilirlik kümesinde bulunabilir hello aralığı, VM boyutlarını hello donanım küme tarafından desteklenen sınırlı toohello aralığı, VM boyutlarını olur. Merhaba donanım küme hello kullanılabilirlik kümesi için hello hello kullanılabilirlik kümesindeki ilk VM dağıtıldığında veya başlangıç Merhaba, tüm sanal makineleri şu anda durduruldu-serbest hello durumda olduğu bir kullanılabilirlik kümesinde ilk VM seçilir. PowerShell komutunu aşağıdaki hello kullanılan toodetermine hello aralığı, VM boyutları için bir kullanılabilirlik kümesi kullanılabilir olabilir: "Get-AzureRmVMSize - ResourceGroupName \<dize\> - AvailabilitySetName \<dize\> "

Her donanım küme toomultiple güncelleştirme etki alanları ve hata etki alanları ayrılmıştır. Bu etki alanlarının bir ortak güncelleştirme döngüsü veya paylaşım benzer fiziksel altyapı, güç ve ağ gibi hangi ana bilgisayarı tarafından paylaşma tanımlanır. Azure Vm'leriniz kullanılabilirlik etki alanları toomaintain kullanılabilirlik ve hataya dayanıklılık arasında kümesi içinde otomatik olarak dağıtır. Merhaba boyutuna uygulama ve sanal makineleri bir kullanılabilirlik kümesi içinde hello sayısı, hello numarası ayarlayabilirsiniz etki alanlarının toouse istiyor. Daha fazla bilgi edinebilirsiniz [kullanılabilirlik ve güncelleştirme ve hata etki alanları kullanımını yönetme](manage-availability.md).

Uygulama altyapınızı tasarlarken, kullandığınız hello uygulama katmanları planlayın. Merhaba hizmet grubu sanal makineleri aynı kullanılabilirlik IIS çalıştıran Vm'leriniz ön uç için kümesi gibi tooavailability kümelerinde amaç. SQL Server çalıştıran arka uç Vm'leriniz için ayrı bir kullanılabilirlik oluşturun. Merhaba, uygulamanızın her bileşenin bir kullanılabilirlik kümesi tarafından korunmaktadır ve en az bir kez örneği her zaman çalışır durumda kaldığını tooensure hedefidir.

Yük dengeleyici her uygulama katmanı toowork bir kullanılabilirlik kümesi yanında önünde kullanılabilir ve trafiği yönlendirilmiş tooa örneğini çalıştıran her zaman olabilir emin olun. Bir yük dengeleyici olmadan Vm'leriniz planlanmış ve planlanmamış bakım olayları boyunca çalışmasını devam edebilir, ancak son kullanıcı mümkün tooresolve bunları Merhaba, birincil VM kullanılamıyor olabilir.

Depolama katmanında yüksek kullanılabilirlik için uygulamanızı tasarlayın. Merhaba en iyi uygulamadır çok[bir kullanılabilirlik kümesindeki sanal makineleri için yönetilen diskler kullanan](manage-availability.md#use-managed-disks-for-vms-in-an-availability-set). Yönetilmeyen diskler kullanıyorsanız, yüksek oranda çok öneririz[sanal makineleri kullanılabilirlik kümesi toouse yönetilen disklerde Dönüştür](convert-unmanaged-to-managed-disks.md#convert-vms-in-an-availability-set).

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]
