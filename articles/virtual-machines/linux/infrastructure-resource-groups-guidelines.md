---
title: "Azure Linux VM'ler için aaaResource grupları | Microsoft Docs"
description: "Azure altyapı Hizmetleri'nde kaynak gruplarını dağıtmak için hello anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 93ab9d93-965a-46b9-9c87-a10d652a6422
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8809cb5eeb9a166d2bcf1946cd26b0ee748f8cd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-group-guidelines-for-linux-vms"></a>Azure kaynak grubu kılavuzları Linux VM'ler 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

Bu makalede nasıl toologically ortamınızı yapı ve kaynak gruplarındaki tüm hello bileşenleri Grup anlamaya odaklanır.

## <a name="implementation-guidelines-for-resource-groups"></a>Kaynak grupları için uygulama rehberi
Kararları:

* Kaynak grupları çıkışı toobuild hello çekirdek altyapı bileşenlerini veya tam uygulama dağıtımı tarafından mısınız?
* Toorestrict erişim tooResource zorunda rol tabanlı erişim denetimlerini kullanarak gruplar?

Görevler:

* Hangi altyapı bileşenlerini çekirdek ve kaynak ihtiyacınız grupları ayrılmış tanımlayın.
* Gözden geçirme nasıl tooimplement Resource Manager şablonları tutarlı ve çoğaltılabilir dağıtımlar için.
* Erişimi denetlemek için gereksinim duyduğunuz hangi kullanıcı erişim rolleri tooResource gruplarını tanımlayın.
* Kaynak grupları, adlandırma kuralını kullanarak Hello kümesi oluşturun. Hello Azure CLI veya portalını kullanabilirsiniz.

## <a name="resource-groups"></a>Kaynak Grupları
Azure'da, mantıksal olarak depolama hesapları, sanal ağlar ve sanal makineleri (VM'ler) toodeploy gibi ilgili kaynaklar grup, yönetmek ve tek bir varlık olarak korumak. Tüm hello tutma kaynakları birlikte bir yönetim Perspektif veya toogrant başkalarının ilişkili bir bu yaklaşımı daha kolay toodeploy uygulamaları kolaylaştırır kaynakların erişim toothat grubu. Kaynak grubu adları en fazla 90 karakter uzunluğunda olabilir. Kaynak grupları hakkında daha kapsamlı anlamak için hello okuyabilirsiniz [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).

TooResource grupları bir anahtar özellik hello depolama, ağ, bildiren bir JSON dosyası kullanarak, ortamınız özelliği toobuild hello ve işlem kaynaklarını. Ayrıca, herhangi bir ilgili özel komut dosyaları veya yapılandırmaları tooapply tanımlayabilirsiniz. Bu JSON şablonları kullanarak, uygulamalarınız için tutarlı ve çoğaltılabilir dağıtımları oluşturun. Bu yaklaşım geliştirme ortamında oluşturun ve o aynı şablon toocreate Üretim dağıtımı kullanmanıza olanak tanır (veya tersi). Daha iyi şablonları kullanma hakkında anlamak için okuma [şablonu Kılavuzu hello](../../azure-resource-manager/resource-manager-template-walkthrough.md) , her bir JSON şablonu oluşturmaya adım yol gösterir.

Ortamınızı kaynak gruplarıyla tasarlarken izleyebileceğiniz iki farklı yaklaşım vardır:

* Merhaba depolama hesapları, sanal ağlar ve alt ağlar, sanal makineleri, birleştirir her uygulama dağıtımı için kaynak grupları yük Dengeleyiciler, vb..
* Çekirdek sanal ağ ve alt ağ veya depolama hesaplarınızı içeren merkezi kaynak gruplar. Uygulamalarınızın sonra yalnızca VM'ler, yük dengeleyici, ağ arabirimleri, vb. içeren, kendi kaynak grubunda olduğundan.

Şirket içi ağ bağlantıları karma bağlantı seçenekleri için sanal ağlar için merkezi kaynak grupları oluşturma ölçekleme ve alt ağları daha kolay toobuild sağlar. Merhaba alternatif her uygulama toohave için yapılandırma ve bakım gerektiren kendi sanal ağ yaklaşımdır. [Rol tabanlı erişim denetimlerini](../../active-directory/role-based-access-control-what-is.md) tooResource grupları ayrıntılı şekilde toocontrol erişim sağlar. Üretim uygulamaları için bu kaynaklara erişebilir hello kullanıcılar denetleyebilir veya hello çekirdek altyapı kaynakları için yalnızca altyapı mühendisleri toowork bunları ile sınırlayabilirsiniz. Uygulama sahipleri erişim toohello uygulama bileşenleri ortamınızın Azure altyapı hello çekirdek değildir ve kaynak grubu içinde yeterlidir. Ortamınızı tasarlarken, toohello kaynaklarına erişim gerektiren ve kaynak gruplarınızı buna uygun olarak tasarlamanız hello kullanıcılar göz önünde bulundurun. 

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

