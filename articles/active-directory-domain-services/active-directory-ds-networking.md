---
title: "Azure AD etki alanı Hizmetleri: Ağ yönergeleri | Microsoft Docs"
description: "Azure Active Directory etki alanı Hizmetleri için ağ konuları"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 23a857a5-2720-400a-ab9b-1ba61e7b145a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: maheshu
ms.openlocfilehash: 804d4ea7d1b3b07b6d224855c7adb90bdfe24022
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-azure-ad-domain-services"></a>Azure AD etki alanı Hizmetleri için ağ konuları
## <a name="how-tooselect-an-azure-virtual-network"></a>Nasıl tooselect bir Azure sanal ağı
Hello aşağıdaki yönergeler, Azure AD etki alanı Hizmetleri ile bir sanal ağ toouse seçmenize yardımcı.

### <a name="type-of-azure-virtual-network"></a>Azure sanal ağ türü
* Klasik Azure sanal ağı Azure AD Etki Alanı Hizmetleri'nde etkinleştirebilirsiniz.
* Azure AD etki alanı Hizmetleri **Azure Resource Manager kullanılarak oluşturulan sanal ağlarda etkinleştirilemez**.
* Azure AD etki alanı Hizmetleri etkin olduğu bir Resource Manager tabanlı sanal ağ tooa Klasik sanal ağına bağlanabilir. Bundan sonra Azure AD Etki Alanı Hizmetleri'ni hello Resource Manager tabanlı sanal ağlarda kullanabilirsiniz. Daha fazla bilgi için bkz: Merhaba [ağ bağlantınızı](active-directory-ds-networking.md#network-connectivity) bölümü.
* **Bölgesel sanal ağlar**: toouse varolan bir sanal ağı planlıyorsanız bunun bölgesel bir sanal ağ olduğundan emin olun.

  * Merhaba eski benzeşim grupları mekanizmasını kullanan sanal ağlar Azure AD etki alanı Hizmetleri ile kullanılamaz.
  * Azure AD etki alanı Hizmetleri, toouse [eski sanal ağları tooregional sanal ağlar geçirmek](../virtual-network/virtual-networks-migrate-to-regional-vnet.md).

### <a name="azure-region-for-hello-virtual-network"></a>Merhaba sanal ağ için Azure bölgesi
* Azure AD etki alanı hizmetlerinizi yönetilen etki alanı içinde dağıtılan hello sanal ağ tooenable hello hizmetinde seçin olduğu Azure bölgesinin hello.
* Azure AD etki alanı Hizmetleri tarafından desteklenen bir Azure bölgesindeki bir sanal ağı seçin.
* Merhaba bkz [bölgeye göre Azure Hizmetleri](https://azure.microsoft.com/regions/#services/) sayfa tooknow hello Azure bölgeleri Azure AD etki alanı Hizmetleri olduğu kullanılabilir.

### <a name="requirements-for-hello-virtual-network"></a>Merhaba sanal ağ gereksinimleri
* **Yakınlık tooyour Azure iş yükleri**: Merhaba şu anda barındıran/tooAzure AD Etki Alanı Hizmetleri'ne erişebilmek sanal makineleri barındıracak sanal ağı seçin.
* **DNS sunucuları özel/Getir kendi**: hello sanal ağ için yapılandırılmış hiçbir özel DNS sunucusunun olduğundan emin olun.
* **Mevcut etki alanlarıyla hello aynı etki alanı adı**: hello ile mevcut bir etki alanına sahip değil sağlamak aynı etki alanı adı bu sanal ağ üzerinde kullanılabilir. Örneğin, "contoso.com" zaten mevcut hello seçilen sanal ağ üzerinde adlı bir etki alanına sahip olduğunuzu varsayar. Daha sonra tooenable hello içeren bir Azure AD etki alanı Hizmetleri yönetilen etki alanı deneyin (yani "contoso.com") aynı etki alanı adı bu sanal ağ üzerinde. Tooenable Azure AD etki alanı Hizmetleri çalışırken bir hatayla karşılaşırsınız. Bu sanal ağ üzerinde hello etki alanı adı için tooname çakışmaları nedeniyle bu başarısız olur. Bu durumda, Azure AD etki alanı Hizmetleri yönetilen etki alanını farklı bir ad tooset kullanmanız gerekir. Alternatif olarak, hello varolan etki alanının sağlanmasını ve tooenable Azure AD etki alanı Hizmetleri devam edin.

> [!WARNING]
> Merhaba hizmetini etkinleştirdikten sonra etki alanı Hizmetleri tooa farklı sanal ağ taşıyamazsınız.
>
>

## <a name="network-security-groups-and-subnet-design"></a>Ağ güvenlik grupları ve alt ağ tasarımı
A [ağ güvenlik grubu (NSG)](../virtual-network/virtual-networks-nsg.md) izin veren veya bir sanal ağ tooyour VM örnekleri ağ trafiği reddeden erişim denetimi listesi (ACL) kurallarının bir listesini içerir. NSG'ler alt ağlarla veya bu alt ağların içindeki tekil VM örnekleriyle ilişkili olabilir. Bir NSG'yi bir alt ağ ile ilişkili olduğunda hello ACL kuralları bu alt ağdaki tooall hello VM örnekleri uygulayın. Buna ek olarak, trafiği tooan tek tek VM kısıtlanabilir başka bir NSG ilişkilendirerek doğrudan toothat VM.

![Önerilen alt ağ tasarımı](./media/active-directory-domain-services-design-guide/vnet-subnet-design.png)

### <a name="best-practices-for-choosing-a-subnet"></a>Bir alt ağı seçmeye yönelik en iyi uygulamalar
* Azure AD etki alanı Hizmetleri tooa dağıtmak **ayrı ayrılmış bir alt ağ** Azure sanal ağınızın içinde.
* Nsg'ler ayrılmış toohello alt yönetilen etki alanınız için geçerli değildir. Nsg'ler ayrılmış toohello alt uygulamalısınız olmanız **değil hello bağlantı noktalarını gerekli tooservice engellemek ve etki alanınızı yönetmek**.
* Aşırı yönetilen etki alanınız için ayrılmış hello alt ağ içindeki kullanılabilir IP adresleri hello sayısını kısıtlamaz. Bu kısıtlama, iki etki alanı denetleyicisi, yönetilen etki alanınız için kullanılabilir bulunmasını hello hizmet önler.
* **Azure AD Etki Alanı Hizmetleri'nde hello ağ geçidi alt ağı etkinleştirmeyin** sanal ağınızın.

> [!WARNING]
> İlişkilendirdiğinizde, bir NSG bir alt ağ içinde Azure AD etki alanı Hizmetleri ile etkinleştirildiğinde, Microsoft'un özelliği tooservice kesintiye neden ve hello etki alanını yönetme. Ayrıca, Azure AD kiracınız, yönetilen etki alanınız arasında eşitleme bozulur. **Burada bir NSG engelleyen Azure AD etki alanı Hizmetleri güncelleştirme ve etki alanınızı yönetme uygulanmış toodeployments Hello SLA geçerli değildir.**
>
>

### <a name="ports-required-for-azure-ad-domain-services"></a>Azure AD etki alanı Hizmetleri için gereken bağlantı noktaları
Merhaba aşağıdaki bağlantı noktaları için Azure AD etki alanı Hizmetleri tooservice gereklidir ve yönetilen etki alanınızı sürdürün. Bu bağlantı noktaları, yönetilen etki alanınız etkinleştirdiğiniz hello alt ağı için engellenmez emin olun.

| Bağlantı noktası numarası | Amaç |
| --- | --- |
| 443 |Azure AD kiracınıza ile eşitleme |
| 3389 |Etki alanınızın Yönetimi |
| 5986 |Etki alanınızın Yönetimi |
| 636 |Güvenli LDAP (LDAPS) erişim tooyour yönetilen etki alanı |

### <a name="sample-nsg-for-virtual-networks-with-azure-ad-domain-services"></a>Azure AD etki alanı Hizmetleri ile sanal ağlar için örnek NSG
Aşağıdaki tablonun hello örnek bir Azure AD etki alanı Hizmetleri yönetilen etki alanına sahip bir sanal ağ için yapılandırabileceğiniz NSG gösterilmektedir. Bu kuralı belirli bağlantı noktaları tooensure yukarıda hello gelen trafiği kalır düzeltme eki, güncelleştirilmiş ve Microsoft tarafından izlenen yönetilen etki alanınızı verir. Merhaba varsayılan 'DenyAll' Kural tooall diğer gelen trafiği hello geçerlidir Internet.

Ayrıca, hello NSG de Internet üzerinden güvenli LDAP erişim tuşunu toolock hello nasıl gösterilmektedir. Bu kural Atla üzerinden güvenli LDAP erişim tooyour yönetilen etki alanı etkinleştirmediyseniz, Internet hello. Merhaba NSG gelen LDAPS erişim TCP bağlantı noktası IP adreslerinin üzerinden 636 belirtilen kümesinden yalnızca izin veren kurallar kümesini içerir. Merhaba NSG kuralı tooallow LDAPS erişimi hello üzerinden internet'ten belirtilen IP adreslerini hello DenyAll NSG kural daha yüksek önceliğe sahiptir.

![Merhaba Internet üzerinden örnek NSG toosecure LDAPS erişim](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Daha fazla bilgi** - [bir ağ güvenlik grubu oluşturun](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).


## <a name="network-connectivity"></a>Ağ bağlantısı
Azure AD etki alanı Hizmetleri yönetilen etki alanı yalnızca tek bir Klasik sanal ağı Azure içinde etkinleştirilebilir. Azure Resource Manager kullanılarak oluşturulan sanal ağlar desteklenmez.

### <a name="scenarios-for-connecting-azure-networks"></a>Azure ağları bağlama senaryoları
Azure sanal ağlar toouse hello yönetilen etki alanı herhangi bir dağıtım senaryoları aşağıdaki hello Bağlan:

#### <a name="use-hello-managed-domain-in-more-than-one-azure-classic-virtual-network"></a>Etki alanında birden fazla Azure Klasik sanal ağı kullan hello yönetilen
Diğer Azure Klasik sanal ağlar toohello Azure bağlanabilirsiniz Azure AD etki alanı Hizmetleri içinde etkinleştirdiğiniz Klasik sanal ağı. Bu VPN bağlantısının diğer sanal ağlarda dağıtılan iş yüklerinizi ile toouse hello yönetilen etki alanı sağlar.

![Klasik sanal ağ bağlantısı](./media/active-directory-domain-services-design-guide/classic-vnet-connectivity.png)

#### <a name="use-hello-managed-domain-in-a-resource-manager-based-virtual-network"></a>Merhaba Resource Manager tabanlı bir sanal ağdaki yönetilen etki alanı kullanın
Resource Manager tabanlı sanal ağ toohello Azure bağlanabilirsiniz Azure AD etki alanı Hizmetleri içinde etkinleştirdiğiniz Klasik sanal ağı. Bu bağlantı hello Resource Manager tabanlı sanal ağda dağıtılmış iş yüklerinizi ile toouse hello yönetilen etki alanı sağlar.

![Resource Manager tooclassic sanal ağ bağlantısı](./media/active-directory-domain-services-design-guide/classic-arm-vnet-connectivity.png)

### <a name="network-connection-options"></a>Ağ bağlantısı seçenekleri
* **Siteden siteye VPN bağlantıları kullanarak VNet-VNet bağlantıları**: benzer tooconnecting bir sanal ağ tooan şirket içi site konumuna olan bir sanal ağ tooanother sanal ağ (VNet-VNet) bağlanma. Her iki bağlantı türü bir VPN ağ geçidi tooprovide IPSec/IKE kullanarak güvenli bir tünel kullanın.

    ![VPN ağ geçidi kullanarak sanal ağ bağlantısı](./media/active-directory-domain-services-design-guide/vnet-connection-vpn-gateway.jpg)

    [Daha fazla bilgi - VPN ağ geçidi kullanarak sanal ağlara bağlanabilir](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* **VNet-VNet bağlantıları kullanarak sanal ağ eşlemesi**: sanal ağ eşlemesi mekanizmasıdır hello içindeki iki sanal ağları birbirine bağlayan bir hello Azure omurga ağı aracılığıyla aynı bölgede. Eşlendikten sonra iki sanal ağ hello tüm bağlantı amaçlar için bir tane olarak görünür. Bunlar ayrı kaynaklar olarak yönetilmeye devam eder, ancak bu sanal ağlardaki sanal makineler özel IP adresleri kullanarak birbirleriyle doğrudan iletişim kurabilir.

    ![Eşleme kullanarak sanal ağ bağlantısı](./media/active-directory-domain-services-design-guide/vnet-peering.png)

    [Daha fazla bilgi - sanal ağ eşlemesi](../virtual-network/virtual-network-peering-overview.md)

<br>

## <a name="related-content"></a>İlgili İçerik
* [Azure sanal ağ eşlemesi](../virtual-network/virtual-network-peering-overview.md)
* [Merhaba Klasik dağıtım modeli için VNet-VNet bağlantı yapılandırma](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md)
* [Azure ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md)
* [Bir ağ güvenlik grubu oluşturun](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
