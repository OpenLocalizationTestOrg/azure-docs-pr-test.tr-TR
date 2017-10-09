---
title: "azure'da Windows sanal makineleri için aaaResource grupları | Microsoft Docs"
description: "Azure altyapı Hizmetleri'nde kaynak gruplarını dağıtmak için hello anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0fbcabcd-e96d-4d71-a526-431984887451
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56b5670ec98bf3e80b7a622d5d760a57a7d20809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-group-guidelines-for-windows-vms"></a>Windows VM'ler için Azure kaynak grubu kılavuzları

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Bu makalede nasıl toologically ortamınızı yapı ve kaynak gruplarındaki tüm hello bileşenleri Grup anlamaya odaklanır.

## <a name="implementation-guidelines-for-resource-groups"></a>Kaynak grupları için uygulama rehberi
Kararları:

* Kaynak grupları çıkışı toobuild hello çekirdek altyapı bileşenlerini veya tam uygulama dağıtımı tarafından mısınız?
* Toorestrict erişim tooResource zorunda rol tabanlı erişim denetimlerini kullanarak gruplar?

Görevler:

* Hangi altyapı bileşenlerini çekirdek ve kaynak ihtiyacınız grupları ayrılmış tanımlayın.
* Gözden geçirme nasıl tooimplement Resource Manager şablonları tutarlı ve çoğaltılabilir dağıtımlar için.
* Erişimi denetlemek için gereksinim duyduğunuz hangi kullanıcı erişim rolleri tooResource gruplarını tanımlayın.
* Kaynak grupları, adlandırma kuralını kullanarak Hello kümesi oluşturun. Azure PowerShell veya hello portalı kullanabilirsiniz.

## <a name="resource-groups"></a>Kaynak Grupları
Azure'da, mantıksal olarak depolama hesapları, sanal ağlar ve sanal makineleri (VM'ler) toodeploy gibi ilgili kaynaklar grup, yönetmek ve tek bir varlık olarak korumak. Tüm hello tutma kaynakları birlikte bir yönetim Perspektif veya toogrant başkalarının ilişkili bir bu yaklaşımı daha kolay toodeploy uygulamaları kolaylaştırır kaynakların erişim toothat grubu. Kaynak grubu adları en fazla 90 karakter uzunluğunda olabilir. Kaynak grupları hakkında daha kapsamlı anlamak için hello okuma [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).

Bir anahtar özellik tooResource grupları özelliği toobuild şablonlarını kullanarak, ortamınız çıkışı değil. Bir şablon, hello depolama, ağ bildirir ve işlem kaynaklarını yalnızca bir JSON dosyasıdır. Ayrıca, herhangi bir ilgili özel komut dosyaları veya yapılandırmaları tooapply tanımlayabilirsiniz. Bu şablonlar kullanarak, uygulamalarınız için tutarlı ve çoğaltılabilir dağıtımları oluşturun. Bu yaklaşım geliştirme kolay toobuild bir ortam çıkışı yapar ve sonra o aynı şablon toocreate Üretim dağıtımı veya tam tersi. Şablonları kullanarak daha iyi anlamak için okuyun [şablonu Kılavuzu hello](../../azure-resource-manager/resource-manager-template-walkthrough.md) , bir şablonu dışarı hello binasının her adım yol gösterir.

Ortamınızı kaynak gruplarıyla tasarlarken izleyebileceğiniz iki farklı yaklaşım vardır:

* Merhaba depolama hesapları, sanal ağlar ve alt ağlar, sanal makineleri, birleştirir her uygulama dağıtımı için kaynak grupları yük Dengeleyiciler, vb..
* Çekirdek sanal ağ ve alt ağ veya depolama hesaplarınızı içeren merkezi kaynak gruplar. Uygulamalarınızın sonra yalnızca VM'ler, yük dengeleyici, ağ arabirimleri, vb. içeren, kendi kaynak grubunda olduğundan.

Şirket içi ağ bağlantıları karma bağlantı seçenekleri için sanal ağlar için merkezi kaynak grupları oluşturma ölçekleme ve alt ağları daha kolay toobuild sağlar. Merhaba alternatif her uygulama toohave için yapılandırma ve bakım gerektiren kendi sanal ağ yaklaşımdır.  [Rol tabanlı erişim denetimlerini](../../active-directory/role-based-access-control-what-is.md) tooResource grupları ayrıntılı şekilde toocontrol erişim sağlar. Üretim uygulamaları için bu kaynaklara erişebilir hello kullanıcılar denetleyebilir veya hello çekirdek altyapı kaynakları için yalnızca altyapı mühendisleri toowork bunları ile sınırlayabilirsiniz. Uygulama sahipleri erişim toohello uygulama bileşenleri ortamınızın Azure altyapı hello çekirdek değildir ve kaynak grubu içinde yeterlidir. Ortamınızı tasarlarken, toohello kaynaklarına erişim gerektiren ve kaynak gruplarınızı buna uygun olarak tasarlamanız hello kullanıcılar göz önünde bulundurun. 

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

