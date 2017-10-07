---
title: "aaaScenarios örnekleri ve abonelik yönetimi | Microsoft Docs"
description: "Örnekleri sağlar tooimplement ortak senaryolar için Azure aboneliği idare."
services: azure-resource-manager
documentationcenter: na
author: rdendtler
manager: timlt
editor: tysonn
ms.assetid: e8fbeeb8-d7a1-48af-804f-6fe1a6024bcb
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: rodend;karlku;tomfitz
ms.openlocfilehash: f750e834519c8e64f57f87e2067801feb38b5c29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-implementing-azure-enterprise-scaffold"></a>Azure enterprise iskele uygulamanın örnekleri
Bu konu kuruluş hello önerileri için nasıl uygulayabilirsiniz örnekler sağlayan bir [Azure enterprise iskele](resource-manager-subscription-governance.md). Contoso tooillustrate en iyi uygulamalar için genel senaryolar adlı kurgusal bir şirket kullanır.

## <a name="background"></a>Arka plan
Contoso, bir "Hizmet olarak yazılım" modeli tooa paketlenmiş modelinden her şeyi müşteriler için tedarik zinciri çözümleri sağlayan dünya çapında şirket içi dağıtılan ' dir.  Bunlar, Hindistan, hello ABD ve Kanada önemli geliştirme merkezleri ile Merhaba dünya genelinde yazılım geliştirin.

Merhaba ISV hello şirket kısmı önemli bir işletmede ürünleri Yönet birkaç bağımsız iş birimleri ayrılmıştır. Her iş birimi kendi geliştiriciler, ürün yöneticileri ve mimarları sahiptir.

Merhaba madde Kurumsal teknoloji Hizmetleri (işaretleri) departmanı merkezi BT yeteneği sağlar ve Departmanlar uygulamalarını ana bilgisayar birkaç veri merkezleri yönetir. Merhaba veri merkezleri yönetme, birlikte hello madde işaretleri kuruluş sağlar ve merkezi işbirliği (örneğin, e-posta ve Web siteleri) ve ağ/telefon hizmetleri yönetir. Bunlar ayrıca müşterilerle iş yükleri işletimsel personel sahip olmayan küçük iş birimleri için yönetin.

Bu konudaki kişiler aşağıdaki hello kullanılır:

* Dave hello madde işaretleri Azure yöneticisidir.
* Alice'i Contoso geliştirme Director hello tedarik zinciri departmandaki ' dir.

Contoso toobuild bir satır iş kolu uygulaması ve bir müşteri dönük uygulaması gerekir. Azure üzerinde toorun hello uygulamaları karar vermiştir. Dave okur hello [Düzenleyici abonelik idare](resource-manager-subscription-governance.md) konusuna ve şimdi hazır tooimplement hello öneriler.

## <a name="scenario-1-line-of-business-application"></a>Senaryo 1: İş kolu satır uygulama
Contoso Merhaba dünya genelindeki geliştiriciler tarafından kullanılan bir kaynak kod yönetim sistemi (BitBucket) toobe oluşturuyor.  Merhaba uygulaması barındırmak için bir hizmet (Iaas) olarak altyapısını kullanır ve web sunucuları ve bir veritabanı sunucusu oluşur. Geliştiriciler kendi geliştirme ortamlarında sunuculara erişmek, ancak bunlar toohello sunucularınızı erişmeyin. Contoso madde işaretleri tooallow hello uygulama sahibi ve ekip toomanage hello uygulama istiyor. Merhaba uygulaması yalnızca Contoso şirket ağında sırasında kullanılabilir. Dave tooset hello abonelik yukarı bu uygulama için gerekir. Hello abonelik hello Gelecekteki Geliştirici ilgili diğer yazılımda da barındırır.  

### <a name="naming-standards--resource-groups"></a>& Kaynak grupları adlandırma standartları
Dave tüm hello iş birimleri arasında ortak olan toosupport geliştirici araçları bir abonelik oluşturur. Kendisine toocreate anlamlı adlar hello abonelik ve kaynak grupları (Merhaba uygulaması ve hello ağlar için) gerekir. Abonelik ve kaynak grupları aşağıdaki hello oluşturur:

| Öğe | Ad | Açıklama |
| --- | --- | --- |
| Abonelik |Contoso madde işaretleri DeveloperTools üretim |Ortak geliştirici araçları destekler |
| Kaynak Grubu |rgBitBucket |Merhaba uygulama web sunucusu ve veritabanı sunucusu içerir |
| Kaynak Grubu |rgCoreNetworks |Merhaba sanal ağlar ve siteden siteye ağ geçidi bağlantısı içerir |

### <a name="role-based-access-control"></a>Rol tabanlı erişim denetimi
Kendi abonelik oluşturduktan sonra uygun takımlar hello tooensure Dave istediği ve uygulama sahipleri kaynaklarına erişebilir. Dave her takım farklı gereksinimlere sahip olduğunu algılar. Kendisine Contoso'nun şirket içi Active Directory (AD) tooAzure Active Directory eşitlenen hello grupları kullanır ve erişim toohello takımlar doğru düzeyde hello sağlar.

Dave hello abonelik için rolleri aşağıdaki hello atar:

| Rol | Çok atanan| Açıklama |
| --- | --- | --- |
| [Sahibi](../active-directory/role-based-access-built-in-roles.md#owner) |Contoso'nun kimliği yönetilen AD |Bu kimliği ile sadece anında (JIT) erişim Contoso'nun kimlik yönetimi aracı üzerinden denetlenir ve abonelik sahibi erişim tam olarak denetlenir sağlar. |
| [Güvenlik Yöneticisi](../active-directory/role-based-access-built-in-roles.md#security-manager) |Güvenliği ve risk yönetimi bölümü |Bu rolü hello Azure Güvenlik Merkezi, kullanıcıların toolook ve hello hello kaynakların durumunu sağlar. |
| [Ağ Katılımcısı](../active-directory/role-based-access-built-in-roles.md#network-contributor) |Ağ ekibi |Bu rolü Contoso'nun ağ takım toomanage hello Site tooSite VPN verir ve sanal ağlar hello. |
| *Özel rol* |Uygulama sahibi |Dave hello özelliği toomodify kaynakları hello kaynak grubunda veren bir rolü oluşturur. Daha fazla bilgi için bkz: [Azure rbac'de özel roller](../active-directory/role-based-access-control-custom-roles.md) |

### <a name="policies"></a>İlkeler
Dave hello abonelik kaynaklarını yönetmek için gereksinimler aşağıdaki hello sahiptir:

* Merhaba geliştirme araçları Merhaba dünya genelindeki geliştiriciler desteklediğinden, kendisinin tooblock kullanıcıların herhangi bir bölgede kaynakları oluşturma istememektedir. Ancak, kaynaklar nerede oluşturulacağını tooknow gerekir.
* Müşterinizle maliyetleri ile ilgili. Bu nedenle, gereksiz yere pahalı sanal makineler oluşturmasına tooprevent uygulama sahipleri istediği.  
* Geliştiriciler birçok iş birimleri bu uygulamaya hizmet çünkü tootag her bir kaynağın hello iş birimi ve uygulama sahibiyle istediği. Bu etiketler kullanarak madde işaretleri hello uygun takımlar faturalandıracaktır.

Merhaba aşağıdaki oluşturur [Resource Manager ilkeleri](resource-manager-policy.md):

| Alan | Etki | Açıklama |
| --- | --- | --- |
| location |Denetim |Tüm bölgelerdeki hello kaynakların hello oluşturmayı denetle |
| type |Reddet |G-serisi sanal makinelerin oluşturulmasını Reddet |
| etiketler |Reddet |Uygulama sahibi etiketi gerektirir |
| etiketler |Reddet |Maliyet merkezi etiketi gerektirir |
| etiketler |ekleme |Etiket adı append **departmanı** ve etiket değeri **madde işaretleri** tooall kaynakları |

### <a name="resource-tags"></a>Kaynak etiketleri
Dave pastaya hello fatura tooidentify hello maliyet merkezi toohave belirli bilgileri hello BitBucket uygulanması için ihtiyacı bilir. Ayrıca, tüm madde işaretleri sahip kaynaklar hello tooknow Dave istemektedir.

Müşterinizle hello aşağıdaki ekler [etiketleri](resource-group-using-tags.md) toohello kaynak grupları ve kaynakları.

| Etiket adı | Etiket değeri |
| --- | --- |
| ApplicationOwner |Bu uygulama yöneten hello kişinin adını Hello. |
| costCenter |hello Azure tüketim için ödeme hello grubunun Hello maliyet merkezi. |
| Departmanı |**Madde işaretleri** (Merhaba abonelikle ilişkili hello departman) |

### <a name="core-network"></a>Çekirdek Ağ
Merhaba Contoso bilgi güvenliği ve risk yönetimi ekibi Dave'nın inceleyene önerilen madde işaretleri toomove hello uygulama tooAzure planlayın. Merhaba uygulaması değil tooensure açığa toohello istedikleri Internet.  Dave, gelecekteki hello taşınan tooAzure olacak Geliştirici uygulamaları da sahiptir. Bu uygulamalar genel arabirimler gerektirir.  toomeet bu gereksinimleri kendisinin hem iç ve dış sanal ağlar ve ağ güvenlik grubu toorestrict erişim sağlar.

Kaynakları aşağıdaki hello oluşturur:

| Kaynak türü | Ad | Açıklama |
| --- | --- | --- |
| Sanal Ağ |vnInternal |BitBucket uygulama Hello ile kullanılan ve ExpressRoute tooContoso'nın şirket ağına bağlı.  Bir alt ağ (sbBitBucket) belirli bir IP adres alanı ile Merhaba uygulaması sağlar. |
| Sanal Ağ |vnExternal |Genel kullanıma yönelik uç noktalar gerektiren gelecekteki uygulamalar için kullanılabilir. |
| Ağ güvenlik grubu |nsgBitBucket |Bu hello sağlar, bu iş yükü saldırı yüzeyini en aza nerede Merhaba uygulaması yaşıyor (sbBitBucket) yalnızca bağlantı noktası 443 üzerinden hello alt ağ için bağlantılara izin vererek. |

### <a name="resource-locks"></a>Kaynak kilitleri
Contoso şirket ağı toohello iç sanal ağ hello bağlantısı herhangi bir wayward komut dosyası veya yanlışlıkla silinmesini korunmalıdır Dave tanır.

Merhaba aşağıdaki oluşturur [kaynak kilidi](resource-group-lock-resources.md):

| Kilit türü | Kaynak | Açıklama |
| --- | --- | --- |
| **CanNotDelete** |vnInternal |Kullanıcıları silme hello sanal ağ veya alt ağlar engeller, ancak yeni alt ağlar hello eklenmesi engellemez. |

### <a name="azure-automation"></a>Azure Otomasyonu
Dave sahip hiçbir şey bu uygulama için tooautomate. Kendisine bir Azure Otomasyonu hesabı oluşturuldu ancak kendisine başlangıçta kullanmaz.

### <a name="azure-security-center"></a>Azure Güvenlik Merkezi
Contoso BT hizmet yönetimi gereksinimlerini tooquickly tanımlamak ve işlemek tehditleri. Ayrıca toounderstand hangi sorunları bulunabilecek isterler.  

toofulfill bu gereksinimleri, Dave etkinleştirir hello [Azure Güvenlik Merkezi](../security-center/security-center-intro.md)ve erişim toohello güvenlik yöneticisi rolü sağlar.

## <a name="scenario-2-customer-facing-app"></a>Senaryo 2: Müşteri dönük uygulama
Merhaba iş liderlik hello tedarik zinciri departmandaki bağlılık kart kullanarak Contoso'nun müşterilerle çeşitli fırsatlar tooincrease katılım belirledi. Alice'in ekibi, bu uygulama oluşturmanız gerekir ve Azure kendi yeteneği toomeet artırır karar hello iş gereksinimi. Alice, madde işaretleri tooconfigure iki aboneliklerinden geliştirme ve bu uygulamayı işletim Dave ile çalışır.

### <a name="azure-subscriptions"></a>Azure abonelikleri
Dave toohello Azure Enterprise Portal günlüğe kaydeder ve bu hello tedarik zinciri departmanı zaten görür.  Ancak, bu proje hello ilk geliştirme projeyi azure'da hello tedarik zinciri ekibi için olduğu gibi Dave Alice'in geliştirme ekibi yeni bir hesaba hello gereksinimini tanır.  Kendisi ekibi için hello "R & D" hesabı oluşturur ve erişim tooAlice atar. Alice hello Azure portal günlüğe kaydeder ve iki abonelikleri oluşturur: bir toohold hello geliştirme sunucuları ve bir toohold hello üretim sunucuları.  Aynen abonelikleri aşağıdaki hello oluştururken, daha önce oluşturulmuş hello adlandırma standartları aşağıdaki gibidir:

| Abonelik kullan | Ad |
| --- | --- |
| Geliştirme |SupplyChain ResearchDevelopment LoyaltyCard geliştirme |
| Üretim |SupplyChain işlemleri LoyaltyCard üretim |

### <a name="policies"></a>İlkeler
Dave Alice Merhaba uygulaması görüşmek ve bu uygulamaya yalnızca Müşteriler hello Kuzey Amerika bölgede hizmet tanımlayın.  Alice ve ekibi toouse Azure'nın uygulama hizmeti ortamı ve Azure SQL toocreate Merhaba uygulaması planlayın. Geliştirme sırasında ihtiyaç duydukları toocreate sanal makineler.  Alice, kendi geliştiriciler tooexplore ihtiyaç duydukları ve madde işaretleri içinde çekme olmadan sorunları inceleyin hello kaynaklarınız tooensure istemektedir.

Hello için **geliştirme abonelik**, ilke aşağıdaki hello oluşturun:

| Alan | Etki | Açıklama |
| --- | --- | --- |
| location |Denetim |Tüm bölgelerdeki hello kaynakları Hello oluşturulmasını denetim. |

Bir kullanıcı geliştirme oluşturabilirsiniz sku hello türü sınırlamaz ve bunların etiketlerini herhangi bir kaynak grupları veya kaynaklar için gerektirmez.

Hello için **üretim abonelik**, ilkelere hello oluşturun:

| Alan | Etki | Açıklama |
| --- | --- | --- |
| location |Reddet |Merhaba ABD veri merkezleri dışında herhangi bir kaynağa Hello oluşturulmasına izin verme. |
| etiketler |Reddet |Uygulama sahibi etiketi gerektirir |
| etiketler |Reddet |Departman etiketi gerektirir. |
| etiketler |ekleme |Üretim ortamında gösterir etiketi tooeach kaynak grubu ekleyin. |

Bir kullanıcı üretimde oluşturabilirsiniz sku hello türü sınırlamaz.

### <a name="resource-tags"></a>Kaynak etiketleri
Dave faturalama ve sahipliği pastaya toohave belirli bilgiler tooidentify hello doğru iş grupları ihtiyacı olduğunu bilir. Hüseyin, kaynak grupları ve kaynaklar için kaynak etiketleri tanımlar.

| Etiket adı | Etiket değeri |
| --- | --- |
| ApplicationOwner |Bu uygulama yöneten hello kişinin adını Hello. |
| Bölüm |hello Azure tüketim için ödeme hello grubunun Hello maliyet merkezi. |
| EnvironmentType |**Üretim** (Merhaba abonelik olsa bile **üretim** hello adlarında bu etiketi de dahil olmak üzere kolay bir şekilde tanımlanması hello portalında veya hello fatura kaynakları bakıldığında etkinleştirir.) |

### <a name="core-networks"></a>Çekirdek Ağ
Merhaba Contoso bilgi güvenliği ve risk yönetimi ekibi Dave'nın inceleyene önerilen madde işaretleri toomove hello uygulama tooAzure planlayın. Bağlılık kartı uygulama hello tooensure düzgün bir şekilde yalıtılmış ve bir çevre ağında korumalı isterler.  toofulfill, bu gereksinim, Dave ve Gamze hello Contoso şirket ağından bir dış sanal ağ ve ağ güvenlik grubu tooisolate hello Bağlılık kartı uygulama oluşturun.  

Hello için **geliştirme abonelik**, bunlar oluşturur:

| Kaynak türü | Ad | Açıklama |
| --- | --- | --- |
| Sanal Ağ |vnInternal |Merhaba Contoso Bağlılık kartı geliştirme ortamı sunar ve ExpressRoute tooContoso'nın şirket ağına bağlanır. |

Hello için **üretim abonelik**, bunlar oluşturur:

| Kaynak türü | Ad | Açıklama |
| --- | --- | --- |
| Sanal Ağ |vnExternal |Merhaba Bağlılık kartı uygulaması barındırır ve ExpressRoute tooContoso kullanıcının doğrudan bağlı değil. Kod kaynak kodu sistemlerine gönderilen doğrudan toohello PaaS Hizmetleri. |
| Ağ güvenlik grubu |nsgBitBucket |Bu hello sağlar bu iş yükü, saldırı yüzeyini en aza bağlı iletişimi yalnızca TCP 443 numaralı vererek.  Contoso ek koruma için bir Web uygulaması Güvenlik Duvarı'nı kullanarak da incelemektedir. |

### <a name="resource-locks"></a>Kaynak kilitleri
Dave Alice confer ve tooadd kaynak kilitleri bazı hello anahtar kaynakları hello ortamı tooprevent yanlışlıkla silme yalıtılarak bir kodun sırasında karar verin.

Bunlar, kilit aşağıdaki hello oluşturun:

| Kilit türü | Kaynak | Açıklama |
| --- | --- | --- |
| **CanNotDelete** |vnExternal |Merhaba sanal ağ veya alt ağları silme tooprevent kişilerin. Merhaba kilit yeni alt ağlar hello eklenmesi engellemez. |

### <a name="azure-automation"></a>Azure Otomasyonu
Alice ve geliştirme ekibi bu uygulama için kapsamlı runbook'lar toomanage hello ortamına sahip. Merhaba runbook'ları Merhaba uygulaması için düğümleri hello eklendiği/silindiği ve diğer DevOps görevler için izin verir.

toouse bu runbook'lar bunlar etkinleştirmek [Otomasyon](../automation/automation-intro.md).

### <a name="azure-security-center"></a>Azure Güvenlik Merkezi
Contoso BT hizmet yönetimi gereksinimlerini tooquickly tanımlamak ve işlemek tehditleri. Ayrıca toounderstand hangi sorunları bulunabilecek isterler.  

toofulfill bu gereksinimleri Dave Azure Güvenlik Merkezi sağlar. Kendisine hello Azure Güvenlik Merkezi hello kaynakları izleme ve toohello DevOps ve güvenlik ekipleri erişim sağlayan sağlar.

## <a name="next-steps"></a>Sonraki adımlar
* Resource Manager şablonları oluşturma hakkında daha fazla toolearn bkz [en iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](resource-manager-template-best-practices.md).

