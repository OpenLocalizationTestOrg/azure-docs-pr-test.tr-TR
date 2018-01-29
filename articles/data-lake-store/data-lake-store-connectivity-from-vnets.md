---
title: "Azure Data Lake Store'a sanal ağlara bağlanma | Microsoft Docs"
description: "Azure sanal ağları Azure Data Lake Store'a bağlama"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 029939eabc7283d7591576fa1b14731a9e626a88
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a>Erişim Azure Data Lake Store bir Azure sanal içinde vm'lerden
Azure Data Lake Store genel Internet IP adresleri üzerinde çalışan bir PaaS hizmetidir. Genel Internet'e bağlanabilir herhangi bir sunucu genellikle de Azure Data Lake Store Uç noktalara bağlanabilir. Varsayılan olarak, Azure Vnet'lerde olan tüm sanal makineleri Internet erişebilir ve bu nedenle Azure Data Lake Store erişebilir. Ancak, Internet erişimi için bir VNET içindeki sanal makineleri yapılandırmak mümkündür. Bu tür VM'ler için Azure Data Lake Store erişimi de sınırlıdır. Azure sanal ağlar VM'ler için genel Internet erişimi engelleme yapılabilir aşağıdaki yaklaşımlardan birini kullanarak.

* Ağ güvenlik grupları (NSG) yapılandırarak
* Kullanıcı tanımlı yolları (UDR) yapılandırarak
* Yollar BGP (endüstri standardı dinamik yönlendirme protokolü) üzerinden değişimi tarafından bu blok ExpressRoute kullanıldığında Internet erişimi

Bu makalede, Azure vm'lerden, yukarıda listelenen üç yöntemden birini kullanarak kaynaklara erişmek için sınırlandı Azure Data Lake Store erişimi etkinleştirmek üzere öğreneceksiniz.

## <a name="enabling-connectivity-to-azure-data-lake-store-from-vms-with-restricted-connectivity"></a>Etkinleştirme bağlantıyı Azure Data Lake Store'a vm'lerden sınırlı
Azure Data Lake Store böyle Vm'lerden erişmek için Azure Data Lake Store hesabı kullanılabilir olduğu IP adresi erişmeleri için yapılandırmanız gerekir. Hesaplarınızı DNS adlarını çözülerek Data Lake Store hesapları için IP adreslerini tanımlayabilirsiniz (`<account>.azuredatalakestore.net`). Bu araçları gibi kullanabileceğiniz **nslookup**. Bilgisayarınızı bir komut istemi açın ve aşağıdaki komutu çalıştırın.

    nslookup mydatastore.azuredatalakestore.net

Çıktı aşağıdakine benzer. Değerin karşı **adresi** özelliği, Data Lake Store hesabınızla ilişkili IP adresidir.

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a>NSG kullanarak sınırlı vm'lerden bağlantıyı etkinleştirme
Daha sonra Internet erişimi engellemek için bir NSG kural kullanıldığında, veri Gölü deposu IP adresi erişimine izin veren başka bir NSG oluşturabilirsiniz. NSG kuralları hakkında daha fazla bilgi için bkz. [bir ağ güvenlik grubu nedir?](../virtual-network/virtual-networks-nsg.md). Nsg'ler oluşturma hakkında yönergeler için bkz [Azure portalını kullanarak Nsg'ler yönetme](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a>UDR veya ExpressRoute kullanılarak kısıtlanmış VM'ler bağlantısını etkinleştirme
Yollar, Udr'ler ya da BGP alınıp yolları, Internet erişimi engellemek için kullanıldığında, özel bir rota bu tür alt VM'ler Data Lake Store uç noktaları erişebilmesi için yapılandırılması gerekir. Daha fazla bilgi için bkz: [kullanıcı tanımlı yollar nelerdir?](../virtual-network/virtual-networks-udr-overview.md). Udr'ler oluşturma ile ilgili yönergeler için bkz: [oluşturma Udr'ler Kaynak Yöneticisi'nde](../virtual-network/virtual-network-create-udr-arm-ps.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a>ExpressRoute kullanarak sınırlı vm'lerden bağlantıyı etkinleştirme
Bir expressroute bağlantı hattı yapılandırıldığında, şirket içi sunucular ortak eşleme aracılığıyla Data Lake Store erişebilir. Bunun için ortak eşleme adresinde Expressroute'u yapılandırma hakkında daha fazla ayrıntı [ExpressRoute SSS](../expressroute/expressroute-faqs.md).

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Data Lake Store'a Genel Bakış](data-lake-store-overview.md)
* [Azure Data Lake Store içinde depolanan verilerin güvenliğini sağlama](data-lake-store-security-overview.md)

