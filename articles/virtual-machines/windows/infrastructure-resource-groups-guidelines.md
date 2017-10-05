---
title: "Azure'da Windows sanal makineleri için kaynak grupları | Microsoft Docs"
description: "Azure altyapı Hizmetleri'nde kaynak gruplarını dağıtmak için anahtar tasarım ve uygulama yönergeleri hakkında bilgi edinin."
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
ms.openlocfilehash: c0aca77af04f895d516f4943188d7890ae9586b7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-group-guidelines-for-windows-vms"></a>Windows VM'ler için Azure kaynak grubu kılavuzları

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

Bu makalede, mantıksal olarak ortamınızı yapı ve kaynak gruplarındaki tüm bileşenleri Grup nasıl anlamaya odaklanır.

## <a name="implementation-guidelines-for-resource-groups"></a>Kaynak grupları için uygulama rehberi
Kararları:

* Kaynak grupları çekirdek altyapı bileşenlerini veya tam uygulama dağıtımı tarafından yapı mısınız?
* Rol tabanlı erişim denetimlerini kullanarak kaynak gruplarına erişimi kısıtlamak gerekiyor mu?

Görevler:

* Hangi altyapı bileşenlerini çekirdek ve kaynak ihtiyacınız grupları ayrılmış tanımlayın.
* Tutarlı ve çoğaltılabilir dağıtımlar için Resource Manager şablonları uygulamak nasıl gözden geçirin.
* Kaynak grupları erişimi denetlemek için gereksinim duyduğunuz hangi kullanıcı erişim rolleri tanımlar.
* Kaynak grupları, adlandırma kuralını kullanarak kümesi oluşturun. Azure PowerShell veya portalı kullanabilirsiniz.

## <a name="resource-groups"></a>Kaynak Grupları
Azure'da, depolama hesapları, sanal ağlar ve dağıtmak, yönetmek ve tek bir varlık olarak korumak için sanal makineleri (VM'ler) gibi ilgili kaynakları mantıksal olarak gruplandırın. Bu yaklaşım, tüm ilgili kaynaklar birlikte yönetimi açısından tutarken uygulamaları dağıtmak için veya diğer kaynakların bu gruba erişim vermek için kolaylaştırır. Kaynak grubu adları en fazla 90 karakter uzunluğunda olabilir. Kaynak grupları hakkında daha kapsamlı anlamak için okuma [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).

Bir anahtar kaynak gruplarına şablonlarını kullanarak, ortamınız yapı yeteneği özelliğidir. Bir şablon, depolama, ağ bildirir ve işlem kaynaklarını yalnızca bir JSON dosyasıdır. Ayrıca, herhangi bir ilgili özel komut dosyaları veya uygulamak için yapılandırmaları tanımlayabilirsiniz. Bu şablonlar kullanarak, uygulamalarınız için tutarlı ve çoğaltılabilir dağıtımları oluşturun. Bu yaklaşım, geliştirme ortamında kullanıma oluşturmak ve bir üretim dağıtımı oluşturmak için aynı şablon kullanmak kolaylaştırır veya tam tersi. Şablonları kullanarak daha iyi anlamak için okuyun [şablonu Kılavuzu](../../azure-resource-manager/resource-manager-template-walkthrough.md) , bir şablonu oluşturmaya her adım yol gösterir.

Ortamınızı kaynak gruplarıyla tasarlarken izleyebileceğiniz iki farklı yaklaşım vardır:

* Kaynak grupları depolama hesapları, sanal ağlar ve alt ağlar, sanal makineleri, birleştirir her uygulama dağıtımı için yük Dengeleyiciler, vb..
* Çekirdek sanal ağ ve alt ağ veya depolama hesaplarınızı içeren merkezi kaynak gruplar. Uygulamalarınızın sonra yalnızca VM'ler, yük dengeleyici, ağ arabirimleri, vb. içeren, kendi kaynak grubunda olduğundan.

Sanal ağ ve alt ağlar için merkezi kaynak grupları oluşturma, ölçeklenebilir, yapı kolaylaştırır gibi şirket içi karma bağlantı seçenekleri bağlantılarında ağ. Yapılandırma ve bakım gerektiren kendi sanal ağ her uygulama için alternatif yaklaşımdır.  [Rol tabanlı erişim denetimlerini](../../active-directory/role-based-access-control-what-is.md) kaynak grupları erişimi denetlemek için ayrıntılı bir yolunu sağlar. Üretim uygulamaları için bu kaynaklara erişebilir kullanıcılar denetleyebilir veya çekirdek altyapı kaynakları için yalnızca altyapı mühendisleri bunlarla çalışmak için sınırlandırabilirsiniz. Uygulama sahipleri, yalnızca kendi kaynak grubu ve Azure altyapı ortamınızın çekirdek değildir içinde uygulama bileşenleri erişiminiz vardır. Ortamınızı tasarlarken, kaynaklara erişim gerektirir ve kaynak gruplarınızı buna uygun olarak tasarlamanız kullanıcıları göz önünde bulundurun. 

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

