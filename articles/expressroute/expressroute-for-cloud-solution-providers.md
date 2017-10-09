---
title: "aaaAzure bulut çözüm sağlayıcıları için ExpressRoute | Microsoft Docs"
description: "Bu makalede, istediğiniz tooincorporate Azure bulut hizmeti sağlayıcıları için bilgi sağlar Hizmetleri ve ExpressRoute tekliflerini içine."
documentationcenter: na
services: expressroute
author: richcar
manager: carmonm
editor: 
ms.assetid: f6c5f8ee-40ba-41a1-ae31-67669ca419a6
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: richcar
ms.openlocfilehash: 062ecbb5e461e4384b01c4ac478cab696b7ed398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-for-cloud-solution-providers-csp"></a>Bulut Çözüm Sağlayıcıları (CSP) için ExpressRoute
Microsoft, geleneksel satıcılar veya dağıtımcıların (CSP) toobe mümkün toorapidly sağlama yeni hizmetler ve çözümler hello kalmadan müşterileriniz için yeni hizmetler geliştirmeye içinde tooinvest gereksinim hiper ölçekli hizmetler sağlar. tooallow hello bulut çözümü sağlayıcısı (CSP) hello özelliği toodirectly bu hizmetleri yönetmek için Microsoft programları ve hello CSP toomanage Microsoft Azure kaynaklarını müşterilerinizin adına izin API'ler sağlar. Bu kaynaklardan biri de ExpressRoute’dur. ExpressRoute hello CSP tooconnect varolan müşteri kaynakları tooAzure hizmetleri sağlar. ExpressRoute, yüksek hızlı özel iletişim bağlantı tooservices azure'da olur. 

Ekli tooa tek müşteri aboneliğine ve birden fazla müşteri tarafından paylaşılamayan devreler yüksek kullanılabilirlik için bir çift bağlantı hattından oluşur. Her bağlantı hattı farklı yönlendirici toomaintain hello yüksek oranda kullanılabilir sonlandırılmalıdır.

> [!NOTE]
> ExpressRoute’da bant genişliği ve bağlantı sınırları vardır, yani büyük/karmaşık uygulamalar tek bir müşteri için birden fazla bağlantı hattı gerektirir.
> 
> 

Microsoft Azure Hizmetleri artan sayıda tooyour müşteriler sunabileceğiniz sağlar.  Bu hizmetlerden toobest yararlanma hello kullan ExpressRoute bağlantıları tooprovide yüksek hızlı düşük gecikmeli erişim toohello Microsoft Azure ortamı gerektirir.

## <a name="microsoft-azure-management"></a>Microsoft Azure yönetimi
Microsoft CSP ile API'leri toomanage hello Azure müşteri aboneliklerini kendi hizmet yönetim Sistemlerinizle programlı tümleştirme vererek sağlar. Desteklenen yönetim özelliklerini [burada](https://msdn.microsoft.com/library/partnercenter/dn974944.aspx) bulabilirsiniz.

## <a name="microsoft-azure-resource-management"></a>Microsoft Azure kaynak yönetimi
Merhaba bağlı olarak Müşterinizle aranızdaki sözleşme hello abonelik nasıl yönetileceğini belirler. Merhaba CSP hello oluşturma doğrudan yönetebilir ve kaynakları veya hello müşterinin bakım hello Microsoft Azure aboneliği denetimi korumak ve ihtiyaç duydukları gibi hello Azure kaynakları oluşturun. Microsoft Azure aboneliğini kaynak hello oluşturmayı müşteri yönetir bunlar iki modelden birini kullanır: "Aracılı bağlantı" modeli veya "doğrudan" modeli. Bu modeller aşağıdaki bölümlerde hello ayrıntılı açıklanmıştır.  

### <a name="connect-through-model"></a>Aracılı bağlantı modeli
![alternatif metin](./media/expressroute-for-cloud-solution-providers/connect-through.png)  

Merhaba aracılı bağlantı modelinde CSP hello veri merkeziniz ile müşterinizin Azure aboneliği arasında doğrudan bir bağlantı oluşturur. Merhaba doğrudan bağlantı ağınız ile Azure ExpressRoute kullanılarak yapılır. Ardından, müşteriniz tooyour ağına bağlanır. Bu senaryo o hello müşteri hello CSP ağ tooaccess Azure Hizmetleri geçirir gerektirir. 

Müşteri tarafından yönetilmeyen başka Azure abonelikleri varsa, Merhaba, hello genel Internet veya hello CSP olmayan aboneliklerinde sağlanan kendi özel bağlantı tooconnect toothose hizmetlerini kullanırsınız. 

Azure hizmetlerini yönetme CSP, o hello CSP, ardından Azure Active Directory'ye Yönetimi CSP aboneliklerinin tarafından (AOBO) üzerinden çoğaltılır depolamak bir daha önce oluşturulmuş bir müşteri kimliği vardır varsayılır. Bu senaryo için anahtar sürücüleri, burada belirtilen iş ortağı veya hizmet sağlayıcısı müşteriyle ilişki hello müşteri, hello müşteri sağlayıcı hizmetlerini zaten kullanıyor veya hello iş ortağı desire tooprovide sağlayıcı tarafından barındırılan bir birleşimini içeriyor içerir ve CSP'nin tek başına karşılanamayan Azure tarafından barındırılan çözümleri tooprovide esneklik ve adres Müşteri sınar. Bu model aşağıdaki **Şekilde** gösterilmiştir.

![alternatif metin](./media/expressroute-for-cloud-solution-providers/connect-through-model.png)

### <a name="connect-toomodel"></a>Bağlantı toomodel
![alternatif metin](./media/expressroute-for-cloud-solution-providers/connect-to.png)

Hello Bağlan toomodel, hello hizmet sağlayıcısı, müşterinin veri merkezi arasında doğrudan bir bağlantı oluşturur ve hello CSP sağlanan Azure aboneliği ExpressRoute hello müşterinin (müşteri) kullanarak ağ.

> [!NOTE]
> ExpressRoute için hello müşteri toocreate gerekir ve hello expressroute bağlantı hattı korumak.  
> 
> 

Bu bağlantı senaryosu, o hello müşteri doğrudan bir müşteri ağ tooaccess CSP tarafından yönetilen Azure aboneliğine oluşturulan, sahibi ve tamamen veya kısmen hello müşteri tarafından yönetilen bir doğrudan ağ kullanarak bağlanmasını gerektirir. Bu müşteriler için hello sağlayıcısı şu anda oluşturulmuş bir müşteri kimliği deposuna yok ve hello sağlayıcısı yardımcı hello müşteri yönetimi için Azure Active Directory'ye deposunu çoğaltmasında varsayılır kendi Abonelik AOBO üzerinden. Burada belirtilen iş ortağı veya hizmet sağlayıcısı müşteriyle ilişki hello müşteri, hello müşteri sağlayıcı hizmetlerini zaten kullanıyor veya hello ortağı yalnızca temel alan bir desire tooprovide Hizmetleri var. Bu senaryo için anahtar sürücülerini içerir Merhaba olmadan Azure tarafından barındırılan çözümleri, mevcut sağlayıcı veri merkezi veya altyapısı için gerekir.

![alternatif metin](./media/expressroute-for-cloud-solution-providers/connect-to-model.png)

Merhaba bu iki seçenek arasında seçim dayalı, müşterinizin gereksinimlerine ve geçerli gereken tooprovide Azure Hizmetleri. Rol tabanlı erişim denetimi, ağ, bu modeller ve hello Hello ayrıntılarını ilişkili ve kimlik tasarımı desenlerine hello bağlantılar aşağıdaki ayrıntıları ele alınmaktadır:

* **Rol Tabanlı Erişim Denetimi (RBAC)** – RBAC, Azure Active Directory’i temel alır.  Azure RBAC hakkında daha fazla bilgi için [buraya](../active-directory/role-based-access-control-configure.md) bakın.
* **Ağ** – hello Microsoft Azure ağ çeşitli konuları kapsar.
* **Azure Active Directory (AAD)** – AAD, Microsoft Azure ve 3 taraf SaaS uygulamaları için hello kimlik yönetimi sağlar. Azure AAD hakkında daha fazla bilgi için [ buraya](https://azure.microsoft.com/documentation/services/active-directory/) bakın.  

## <a name="network-speeds"></a>Ağ hızları
ExpressRoute, 50 Mb/sn too10Gb/s ağ hızlarını destekler. Bu, müşterilerin toopurchase hello benzersiz ortamları için gerekli ağ bant genişliği miktarını sağlar.

> [!NOTE]
> Ağ bant genişliği gerektiğinde iletişimleri bozmadan artırılabilir ancak tooreduce hello ağ hızı hello bağlantı hattının kaldırılması ve hello daha düşük ağ hızında yeniden oluşturulması gerekir.  
> 
> 

ExpressRoute hello yüksek hızlı bağlantıların daha iyi kullanımı için birden çok sanal ağlar tooa tek expressroute bağlantı hattı hello bağlantısını destekler. Tek bir expressroute bağlantı hattı tarafından hello ait birden çok Azure aboneliği arasında paylaşılabilir aynı müşteri.

## <a name="configuring-expressroute"></a>ExpressRoute’u yapılandırma
ExpressRoute, yapılandırılmış toosupport üç tür trafiği olabilir ([Yönlendirme etki alanları](#ExpressRoute-routing-domains)) tek bir expressroute bağlantı hattı üzerinden. Bu trafik; Microsoft eşliği, Azure genel eşliği ve özel eşliği olarak ayrılır. Tek bir expressroute bağlantı hattı gönderilen trafik toobe türlerinden birini veya hepsini seçin veya birden çok ExpressRoute bağlantı hatları hello boyutunu hello expressroute bağlantı hattı ve müşteriniz tarafından gerekli yalıtımı bağlı olarak kullanın. Müşterinizin güvenlik yaklaşımı Hello izin ortak trafiği ve özel trafiğin tootraverse üzerinden hello aynı bağlantı hattı.

### <a name="connect-through-model"></a>Aracılı bağlantı modeli
Bir bağlantı yapılandırmasında hello tüm müşterilerin veri merkezi kaynakları toohello aboneliklerinizi Azure üzerinde barındırılan bağlamasından tooconnect ağ hello sorumlu olacaktır. Her toouse Azure özelliklerini bırakılacak istediğiniz müşterinizin tarafından yönetilen kendi ExpressRoute bağlantısına hello. Merhaba hello kullanacağınız aynı yöntemleri hello müşteri tooprocure hello expressroute bağlantı hattı kullanır. Merhaba, hello hello makalesinde özetlenen aynı adımları izleyeceksiniz [ExpressRoute iş akışları](expressroute-workflows.md) devre sağlama ve devre durumları için. Merhaba hello şirket içi ağınız ve Azure vNet arasında akan hello sınır ağ geçidi Protokolü (BGP) yollar toocontrol hello trafiğin sonra yapılandırır.

### <a name="connect-toomodel"></a>Bağlantı toomodel
Bir connect-tooconfiguration, müşterinizin zaten varolan bir bağlantı tooAzure sahip veya ExpressRoute müşterinin kendi merkeziniz bağlama bir bağlantı toohello Internet servis sağlayıcısı başlatacaktır merkeziniz yerine doğrudan tooAzure. toobegin hello sağlama işlemi, müşterinizin hello aracılı bağlantı modelinde, yukarıda açıklandığı gibi hello adımları izleyeceksiniz. Merhaba hattı kurulduktan sonra müşterinizin, ağ ve Azure sanal ağlar tooconfigure hello şirket içi yönlendiricileri toobe mümkün tooaccess gerekir.

Merhaba bağlantısı ayarlama ile yardımcı olabilir ve hello yapılandırma tooallow hello kaynakları, inizdeki toocommunicate, veri merkezinizdeki hello istemci kaynaklarla ya da Azure'de barındırılan hello kaynaklarla içinde yönlendirir.

## <a name="expressroute-routing-domains"></a>ExpressRoute yönlendirme etki alanları
ExpressRoute üç yönlendirme etki alanı sunar: Genel, özel ve Microsoft eşlemesi. Her hello Yönlendirme etki alanları aynı yönlendiricilerle aktif-aktif yapılandırma yüksek kullanılabilirlik için. ExpressRoute yönlendirme etki alanları hakkında daha fazla ayrıntı için [buraya](expressroute-circuit-peerings.md) göz atın.

Tooallow istediğiniz veya ihtiyaç özel yollar filtreleri tooallow yalnızca hello route(s) tanımlayabilirsiniz. Daha fazla bilgi veya toosee toomake bu değişiklikleri nasıl bkz makale: [oluşturma ve PowerShell kullanarak bir expressroute bağlantı hattı için yönlendirmeyi değiştirme](expressroute-howto-routing-classic.md) yönlendirme filtreleri hakkında daha fazla ayrıntı için.

> [!NOTE]
> Microsoft ve genel eşleme için bağlantı ancak hello müşteri ya da CSP tarafından sahip olunan genel bir IP adresi olmalıdır ve tanımlanan tooall kurallarına uyması gerekir. Daha fazla bilgi için bkz: Merhaba [ExpressRoute önkoşulları](expressroute-prerequisites.md) sayfası.  
> 
> 

## <a name="routing"></a>Yönlendirme
ExpressRoute bağlayan toohello Azure hello Azure sanal ağ geçidi üzerinden ağlar. Ağ geçitleri, Azure sanal ağlarına yönlendirme sağlar.

Azure sanal ağları oluşturma hello vNet toodirect trafiğe çift hello vnet'in hello alt ağlar için varsayılan bir yönlendirme tablosu oluşturur. Merhaba varsayılan rota tablosu hello çözüm için yetersiz ise tooroute giden trafiği toocustom cihazları yollar oluşturulabilir veya toospecific alt ağlar ya da dış ağlara tooblock yönlendirir.

### <a name="default-routing"></a>Varsayılan yönlendirme
Merhaba varsayılan rota tablosu aşağıdaki yollar hello içerir:

* Bir alt ağ içinde yönlendirme
* Alt ağ alt hello sanal ağ içinde
* toohello Internet
* VPN ağ geçidi kullanarak sanal ağdan sanal ağa yönlendirme
* Bir VPN ya da ExpressRoute ağ geçidi kullanarak sanal ağdan şirket içi ağına yönlendirme

![alternatif metin](./media/expressroute-for-cloud-solution-providers/default-routing.png)  

### <a name="user-defined-routing-udr"></a>Kullanıcı tanımlı yönlendirme (UDR)
Kullanıcı tanımlı yollar hello denetim hello giden trafik alt ağı hello sanal ağındaki tooother alt ağların atanan veya diğer önceden tanımlanmış ağ geçitleri (ExpressRoute; internet veya VPN) birinin üzerine hello izin verin. Merhaba varsayılan sistem yönlendirme tablosu hello varsayılan yönlendirme tablosunu özel yollarla değiştiren bir kullanıcı tanımlı yönlendirme tablosu ile değiştirilebilir. Kullanıcı tanımlı yönlendirme ile müşteriler güvenlik duvarları veya izinsiz giriş algılama gereçlerine gibi belirli yollar tooappliances oluşturabilir, veya erişim toospecific hello alt hello kullanıcı tanımlı yolu barındıran alt ağlardan engelleyin. Kullanıcı Tanımlı Yollara genel bir bakış için [buraya](../virtual-network/virtual-networks-udr-overview.md) göz atın. 

## <a name="security"></a>Güvenlik
Kullanımda, Bağlan tooor aracılı bağlantı, hangi modeline bağlı olarak, müşteriniz kendi sanal ağında hello güvenlik ilkeleri tanımlar veya toohello CSP toodefine tootheir sanal ağlar hello güvenlik ilkesi gereksinimleri sağlar. Merhaba aşağıdaki güvenlik ölçütleri tanımlanabilir:

1. **Müşteri yalıtımı** — hello Azure platformu müşteri yalıtımı Müşteri Kimliği ve sanal ağ bilgisini kullanılan tooencapsulate olan bir güvenli veritabanında depolayarak her müşterinin trafik bilgisini bir GRE tünelinde sağlar.
2. **Ağ güvenlik grubu (NSG)** kurallardır içine ve dışına sanal ağlar Azure içindeki alt ağlara hello trafiğe izin tanımlamak için. Varsayılan olarak, hello NSG hello Internet toohello vNet ve sanal ağ içinde trafik için izin verme kuralları blok kuralları tooblock trafiği içerir. Ağ Güvenlik Grupları hakkında daha fazla bilgi için [buraya](https://azure.microsoft.com/blog/network-security-groups/) göz atın.
3. **Zorlamalı tünel** — Internet üzerinden şirket içi veri merkezi üzerinde hello ExpressRoute bağlantı toohello yeniden yönlendirilen Azure toobe kaynaklanan trafiğe bağlı bir seçenek tooredirect budur. Zorlamalı tünel görünümü hakkında daha fazla bilgi için[buraya](expressroute-routing.md#advertising-default-routes) göz atın.  
4. **Şifreleme** — hello ExpressRoute bağlantı hatları belirli bir müşteriye ayrılmış tooa olsa bile olduğundan ağ sağlayıcısı hello hello olasılığı ihlal, yapanların paket trafiğini tooexamine. Bu olası, müşteri ya da CSP trafiğini üzerinden şifreleyebilir tooaddress hello şirket kaynaklarına ve (müşteri 1 için toohello isteğe bağlı tünel modu IPSec başvurun Azure kaynakları arasında akan tüm trafiği IPSec tünel modu ilkelerine tanımlayarak bağlantı hello Şekil 5: ExpressRoute güvenliği, yukarıdaki). Merhaba ikinci seçenek toouse hello expressroute bağlantı hattı her hello uç noktasında bir güvenlik duvarı gerecini olabilir. Bu ek 3. taraf güvenlik duvarı hello expressroute bağlantı hattının her iki uca tooencrypt hello trafiğinde yüklü VM'ler/cihazları toobe gerektirir.

![alternatif metin](./media/expressroute-for-cloud-solution-providers/expressroute-security.png)  

## <a name="next-steps"></a>Sonraki adımlar
Merhaba bulut çözümü sağlayıcısı hizmeti değeri tooyour müşterilerinizin hello olmadan hello birincil dış kaynak sağlayıcısı olarak konumunuzu koruyarak pahalı altyapı ve özelliklere satın alma işlemleri, gereksinim bir şekilde tooincrease sağlar. Microsoft Azure ile sorunsuz tümleştirme hello toointegrate Microsoft Azure yönetimini mevcut yönetim altyapınızın içinde izin vererek CSP API'si aracılığıyla gerçekleştirilebilir.  

Ek bilgi bağlantıları aşağıdaki hello bulunabilir:

[Microsoft Bulut Çözümü Sağlayıcısı programı](https://partner.microsoft.com/en-US/Solutions/cloud-reseller-overview).  
[Bir bulut çözümü sağlayıcısı olarak hazır tootransact almak](https://partner.microsoft.com/en-us/solutions/cloud-reseller-pre-launch).  
[Microsoft Bulut Çözümü Sağlayıcısı kaynakları](https://partner.microsoft.com/en-us/solutions/cloud-reseller-resources).

