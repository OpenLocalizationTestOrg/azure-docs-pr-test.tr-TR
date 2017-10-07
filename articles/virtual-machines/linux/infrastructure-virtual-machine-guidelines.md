---
title: "Linux sanal makineleri yönergeleri aaaAzure | Microsoft Docs"
description: "Linux sanal makineleri Azure'a dağıtmak için hello anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin"
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 740767d7-9a40-407b-93e7-c29dd976ffd7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.openlocfilehash: 0f779f791005441b6b16e106a3dc5a095bb33034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-guidelines-for-linux"></a>Linux için Azure sanal makineleri yönergeleri
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Bu makalede Azure ortamınızda planlama adımları oluşturmak ve sanal makineleri (VM'ler) yönetmek için gereken anlama hello odaklanır.

## <a name="implementation-guidelines-for-vms"></a>VM'ler için uygulama rehberi
Kararları:

* Kaç tane sanal makineleri, çeşitli uygulama katmanları ve altyapınızın bileşenleri için gerektiriyor mu?
* Hangi CPU ve bellek kaynaklarının her VM'in mu ve hello depolama gereksinimleri nelerdir?

Görevler:

* Merhaba iş yükleri VM'ler, uygulama ve hello kaynakları hello için tanımlayın.
* Merhaba uygun VM boyutu ve depolama türü olan her bir VM için Hello kaynak taleplerini hizalayın.
* Kaynak gruplarınızı hello farklı katmanlara ve altyapınızın bileşenleri için tanımlayın.
* VM adlandırma kuralınızın tanımlayın.
* Hello Azure CLI, web portalı, ya da Resource Manager şablonları kullanarak, Vm'lerde oluşturun.

## <a name="virtual-machines"></a>Sanal makineler
Merhaba ana kaynaklar Azure ortamınızda olası VM'ler biridir. Bu uygulamaları, veritabanları, kimlik doğrulama hizmetleri, vb. çalıştırdığı bir kaynaktır.

Önemli toounderstand hello olan [farklı VM boyutları](sizes.md) toocorrectly ortamınızı performans ve maliyet açısından boyutu. Vm'leriniz yeterli CPU çekirdekleri veya bellek yoksa, uygulamanızın performansını ne kadar iyi onu tasarlanmış geliştirilen ve bağımsız olarak düşer. Her bileşen için hangi boyutu VM toouse altyapınızda karar gibi gözden geçirme hello iş yükleri bir başlangıç noktası olarak her VM dizisi için önerilen. Yapabilecekleriniz [VM hello boyutunu değiştirme](change-vm-size.md) dağıtımdan sonra.

Depolama VM performansı önemli bir rol oynar. Yüksek g/ç iş yükleri ve SSD diskleri kullanan en yüksek performans için normal dönen diskleri kullanan standart depolama veya Premium storage kullanabilirsiniz. Olarak hello VM boyutu ile var maliyet konuları tooselecting hello depolama ortamı. Merhaba okuyabilirsiniz [depolama altyapısı yönergeleri makale](infrastructure-storage-solutions-guidelines.md) toounderstand nasıl toodesign uygun depolama en iyi performansı Vm'leriniz için.

## <a name="resource-groups"></a>Kaynak grupları
Sanal makineleri gibi bileşenleri, yönetim ve Bakım kullanarak kolaylığı için mantıksal olarak gruplandırılır [Azure kaynak gruplarını](../../azure-resource-manager/resource-group-overview.md). Kaynak grupları kullanarak, oluşturmak, yönetmek ve belirli bir uygulamayı oluşturan tüm hello kaynakları izle. Ayrıca uygulayabilirsiniz [rol tabanlı erişim denetimlerini](../../active-directory/role-based-access-control-what-is.md) toogrant erişim tooothers gereksinim duydukları takım tooonly hello kaynaklarınızı içinde. Kaynak grupları ve rol atamalarını zaman tooplan alın. Tasarım ve uygulama kaynak grupları farklı yaklaşımlara tooactually vardır, bu nedenle emin tooread hello [kaynak grupları yönergeleri makale](infrastructure-resource-groups-guidelines.md) toounderstand en iyi nasıl toobuild Vm'leriniz çıkışı.

## <a name="templates"></a>Şablonlar
Toocreate bildirim temelli JSON dosyaları tarafından tanımlanan şablonları oluşturabilirsiniz Vm'leriniz. Şablonları genellikle de derleme gerekli hello depolama, ağ, ağ arabirimleri, IP adresleme, vb. hello VM'ler kendilerini yanı sıra. Geliştirme ve sınama amacıyla tooeasily üretim ortamlarında çoğaltmak için şablonlar toocreate tutarlı ve çoğaltılabilir ortamları kullanabilirsiniz ve tersi. Daha fazla bilgi edinebilirsiniz [oluşturma ve şablonlar kullanarak](../../azure-resource-manager/resource-group-overview.md#template-deployment) nasıl kullanabileceğiniz bunları oluşturma ve dağıtma Vm'leriniz için toounderstand.

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

