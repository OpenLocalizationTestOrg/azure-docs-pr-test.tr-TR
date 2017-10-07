---
title: Data Lake Deposu'ndan veri Vnet'ler aaaConnect tooAzure | Microsoft Docs
description: "Azure sanal ağlar tooAzure Data Lake Store Bağlan"
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
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c695dcf49fe4e1a87a90729cf085a938f3b51fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a>Erişim Azure Data Lake Store bir Azure sanal içinde vm'lerden
Azure Data Lake Store genel Internet IP adresleri üzerinde çalışan bir PaaS hizmetidir. Toohello ortak Internet can genellikle bağlanabilir herhangi bir sunucu tooAzure Data Lake Store uç noktalarını da bağlayın. Varsayılan olarak, Azure Vnet'lerde olan tüm VM'ler hello Internet erişebilir ve bu nedenle Azure Data Lake Store erişebilir. Ancak, bir VNET toonot olası tooconfigure Vm'lerde olan erişim toohello Internet sahip. Bu tür VM'ler için erişim tooAzure Data Lake Store de sınırlıdır. Azure sanal ağlar VM'ler için genel Internet erişimi engelleme yapılabilir yaklaşımı izleyerek hello birini kullanarak.

* Ağ güvenlik grupları (NSG) yapılandırarak
* Kullanıcı tanımlı yolları (UDR) yapılandırarak
* Yollar BGP (endüstri standardı dinamik yönlendirme protokolü) üzerinden değişimi tarafından bu blok ExpressRoute kullanıldığında toohello Internet erişimi

Bu makalede, nasıl tooenable erişim toohello Azure Data Lake Store hello üç yöntemden birini kullanarak kaynak yukarıda listelenen kısıtlı tooaccess silinmiş Azure vm'lerden öğreneceksiniz.

## <a name="enabling-connectivity-tooazure-data-lake-store-from-vms-with-restricted-connectivity"></a>Bağlantı tooAzure vm'lerden Data Lake Store ile kısıtlı bağlantıyı etkinleştirme
tooaccess Azure Data Lake deposuna böyle Vm'lerden, hello Azure Data Lake Store hesabı kullanılabilir olduğu tooaccess başlangıç IP adresi yapılandırmanız gerekir. Hesaplarınız hello DNS adları çözme tarafından Data Lake Store hesapları için hello IP adreslerini tanımlayabilirsiniz (`<account>.azuredatalakestore.net`). Bu araçları gibi kullanabileceğiniz **nslookup**. Bilgisayarınızı bir komut istemi açın ve hello aşağıdaki komutu çalıştırın.

    nslookup mydatastore.azuredatalakestore.net

Merhaba çıktı hello aşağıdakine benzer. Merhaba karşı değer **adresi** başlangıç IP adresi, Data Lake Store hesabınızla ilişkili bir özelliktir.

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a>NSG kullanarak sınırlı vm'lerden bağlantıyı etkinleştirme
Bir NSG kural kullanıldığında tooblock erişim toohello Internet, ardından erişim toohello Data Lake deposu IP adresi sağlayan başka bir NSG oluşturabilirsiniz. NSG kuralları hakkında daha fazla bilgi için bkz. [bir ağ güvenlik grubu nedir?](../virtual-network/virtual-networks-nsg.md). Yönergeler için nasıl toocreate Nsg'ler bkz [nasıl Azure portal kullanarak toomanage Nsg'ler hello](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a>UDR veya ExpressRoute kullanılarak kısıtlanmış VM'ler bağlantısını etkinleştirme
Yollar, Udr'ler ya da BGP alınıp yolları, kullanılan tooblock erişim toohello Internet olduğunda, özel bir rota bu tür alt VM'ler Data Lake Store uç noktaları erişebilmesi için yapılandırılmış toobe gerekir. Daha fazla bilgi için bkz: [kullanıcı tanımlı yollar nelerdir?](../virtual-network/virtual-networks-udr-overview.md). Udr'ler oluşturma ile ilgili yönergeler için bkz: [oluşturma Udr'ler Kaynak Yöneticisi'nde](../virtual-network/virtual-network-create-udr-arm-ps.md).

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a>ExpressRoute kullanarak sınırlı vm'lerden bağlantıyı etkinleştirme
Bir expressroute bağlantı hattı yapılandırıldığında, hello şirket içi sunucular ortak eşleme aracılığıyla Data Lake Store erişebilir. Bunun için ortak eşleme adresinde Expressroute'u yapılandırma hakkında daha fazla ayrıntı [ExpressRoute SSS](../expressroute/expressroute-faqs.md).

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Data Lake Store'a Genel Bakış](data-lake-store-overview.md)
* [Azure Data Lake Store içinde depolanan verilerin güvenliğini sağlama](data-lake-store-security-overview.md)

