---
title: "aaaNetwork güvenlik kavramları & Azure gereksinimleri | Microsoft Docs"
description: " Bu makalede, toounderstand ne kolaylaştırır Microsoft Azure ağ güvenliği hello alanında toooffer sahiptir. Çekirdek Ağ güvenlik kavramları ve gereksinimleri için temel açıklamaları sağladığımız ve hangi Azure ile ilgili bilgileri toooffer bu alanların her birinde sahiptir. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: bedf411a-0781-47b9-9742-d524cf3dbfc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: terrylan
ms.openlocfilehash: 87d336064b880ddcf90ae4fcb79b7823367682b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-overview"></a>Azure ağ güvenliğine genel bakış
Microsoft Azure, uygulama ve hizmet bağlantı gereksinimleri sağlam bir ağ altyapısı toosupport içerir. Azure'da, şirket içi arasında bulunan kaynaklar arasındaki ağ bağlantısı mümkündür ve Azure kaynakları ve hello Internet gelen tooand ve Azure barındırılır.

Merhaba, bu makalenin hedeftir toomake, toounderstand kolaylaştırır ne Microsoft Azure toooffer hello bölümünde sahip ağ güvenliği. Burada Çekirdek Ağ güvenlik kavramları ve gereksinimleri için temel açıklamalar sağlar. Ayrıca, hangi Azure hakkında bilgi toooffer bu alanların her birinde sahip yanı sıra ilginç alanları daha derin bir anlayış kazanmak toohelp bağlantılar sunuyoruz.

Bu Azure ağ güvenliğine genel bakış makalesi alanları aşağıdaki hello üzerinde odaklanır:

* Azure ağı
* Ağ erişim denetimi
* Güvenli uzaktan erişim ve şirket içi bağlantı
* Kullanılabilirlik
* Ad çözümlemesi
* DMZ mimarisi
* İzleme ve tehdit algılama


## <a name="azure-networking"></a>Azure Ağı
Sanal makinelerin ağ bağlantısı gerekir. toosupport bu gereksinim, Azure gerektirir bağlı sanal makineleri toobe tooan Azure sanal ağı. Bir Azure sanal ağı hello Azure fiziksel ağ yapısında en üstünde oluşturulmuş mantıksal bir yapıdır. Her mantıksal Azure sanal tüm diğer Azure sanal ağlardan yalıtılmış bir ağdır. Bu, ağ trafiğini dağıtımlarınızı erişilebilir tooother Microsoft Azure müşterilerin olmadığından emin güvence altına yardımcı olur.

Daha fazla bilgi edinin:

* [Sanal ağ genel bakış](../virtual-network/virtual-networks-overview.md)


## <a name="network-access-control"></a>Ağ erişim denetimi
Ağ erişim denetimi, belirli aygıtları veya bir Azure sanal ağ içindeki alt ağlara bağlantısı tooand sınırlama hello işlemidir. Merhaba ağ erişim denetimi toolimit erişim tooyour sanal makineleri ve Hizmetleri tooapproved kullanıcıları ve aygıtları hedefidir. Erişim denetimleri dayalı üzerinde izin ver veya bağlantıları tooand kararlar sanal makine ya da hizmet reddet.

Azure ağ erişim denetimi gibi çeşitli türlerini destekler:

* Ağ katmanı denetimi
* Denetim yönlendirmek ve zorlanan tünel
* Sanal ağ güvenlik uygulamaları

### <a name="network-layer-control"></a>Ağ katmanı denetimi
Tüm güvenli dağıtım bazı ölçü ağ erişim denetimi gerektirir. Merhaba ağ erişim denetimi toorestrict sanal makine iletişimi toohello gerekli sistemleri ve diğer iletişim girişimleri engellenir hedefidir.

Temel ağ düzeyinde erişim denetimi (IP adresi ve hello TCP veya UDP protokollerini göre) ihtiyacınız varsa, ağ güvenlik gruplarını kullanabilirsiniz. Ağ güvenlik grubu (NSG) temel bir durum bilgisi olan paket güvenlik duvarı filtreleme olduğundan ve temel toocontrol erişim bir [5-tanımlama grubu](https://www.techopedia.com/definition/28190/5-tuple). Nsg'ler erişim denetimleri kimlik doğrulamalı veya uygulama katmanı denetleme sağlamaz.

Daha fazla bilgi edinin:

* [Ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md)

### <a name="route-control-and-forced-tunneling"></a>Rota denetimi ve zorlamalı tünel
Merhaba özelliği toocontrol yönlendirme, Azure sanal ağlar üzerindeki bir kritik ağ güvenliği ve erişim denetimi özelliği davranıştır. Yönlendirme hatalı yapılandırıldıysa, uygulamaları ve Hizmetleri, sanal makinede barındırılan ait ve potansiyel saldırganlar tarafından işletilen sistemleri toounauthorized aygıtlar bağlanabilir.

Azure ağı hello özelliği toocustomize hello yönlendirme davranışı, Azure sanal ağlarda ağ trafiğini destekler. Bu, tooalter hello varsayılan yönlendirme tablosu girdileri Azure sanal ağınızda sağlar. Yönlendirme davranışını denetimi, belirli bir aygıt veya cihaz grubunu gelen tüm trafiği girdiğinde veya sanal ağınız belirli bir konuma bırakır emin olun yardımcı olur.

Örneğin, Azure sanal ağınızda bir sanal ağ güvenlik Gereci olabilir. Azure sanal ağınızda gelen tüm trafiği tooand bu sanal güvenlik gereç yoluyla gider emin toomake istiyor. Bunu yapılandırarak yapmak [kullanıcı tanımlı yollar](../virtual-network/virtual-networks-udr-overview.md) azure'da.

[Zorlanan tünel](https://www.petri.com/azure-forced-tunneling) olan hizmetlerinizi olmayan tooensure kullanabileceğiniz bir mekanizma hello Internet üzerinde bir bağlantı toodevices tooinitiate izin. Bu gelen bağlantıları kabul etmek ve ardından yanıt farklı olduğuna dikkat edin toothem. Internet kaynaklanan trafiğe izin şekilde gelen toothese web sunucuları ve hello web sunucuları toorespond izin verilir ve ön uç web sunucuları Internet konakları toorespond toorequests gerekir.

Hangi ön uç web sunucusu tooinitiate bir giden talep tooallow olan istemezsiniz. Bu bağlantılar kullanılan toodownload kötü amaçlı yazılım olabilir çünkü bu tür istekleri bir güvenlik riski oluşturabilir. Bu ön uç bile istiyorsanız sunucuları tooinitiate Giden istekleri toohello Internet, tooforce isteyebilirsiniz bunları şirket içi aracılığıyla toogo web proxy böylece filtreleme ve günlüğe kaydetme URL yararlanabilir.

Bunun yerine, bu tünel tooprevent toouse zorladı istersiniz. Zorlamalı tünel etkinleştirdiğinizde, tüm bağlantılar toohello Internet zorla, şirket içi ağ geçidi üzerinden. Kullanıcı tanımlı yollar yararlanarak zorlamalı tünel yapılandırabilirsiniz.

Daha fazla bilgi edinin:

* [Kullanıcı tanımlı yollar ve IP iletimi nedir](../virtual-network/virtual-networks-udr-overview.md)

### <a name="virtual-network-security-appliances"></a>Sanal ağ güvenlik uygulamaları
Ağ güvenlik grupları, kullanıcı tanımlı yollar ve zorlamalı tünel hello hello ağ ve Aktarım katmanı güvenlik düzeyini sunarken [OSI modeli](https://en.wikipedia.org/wiki/OSI_model), daha yüksek düzeylerde tooenable güvenlik istediğinizde zamanlar olabilir Merhaba ağ.

Örneğin, güvenlik gereksinimlerinizi şunlar olabilir:

* Kimlik doğrulama ve yetkilendirme access tooyour uygulaması izin vermeden önce
* İzinsiz giriş algılama ve yetkisiz erişim yanıtı
* Üst düzey protokoller için uygulama katmanı denetleme
* URL filtreleme
* Ağ düzeyinde virüsten koruma ve kötü amaçlı yazılımdan koruma
* Koruma bot koruma
* Uygulama erişim denetimi
* Ek DDoS Koruması (yukarıda hello DDoS sağlanan koruma hello Azure doku kendisini)

Bir Azure iş ortağı çözümü kullanarak bu Gelişmiş ağ güvenliği özelliklere erişebilir. Merhaba ziyaret ederek en güncel Azure iş ortağı ağ güvenlik çözümlerini hello bulabilirsiniz [Azure Marketi](https://azure.microsoft.com/marketplace/) ve "güvenlik" ve "ağ güvenliği" için arama

## <a name="secure-remote-access-and-cross-premises-connectivity"></a>Güvenli uzaktan erişim ve şirket içi ve dışı bağlantı
Kurulum, yapılandırma ve Azure kaynaklarınızın yönetimi, uzaktan yapılan toobe gerekir. Ayrıca, toodeploy isteyebilirsiniz [karma BT](http://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) içi bileşenleri çözümleri ve'hello Azure genel bulut. Bu senaryolar güvenli uzaktan erişim gerektirir.

Azure ağı güvenli uzaktan erişim senaryoları aşağıdaki hello destekler:

* Ayrı iş istasyonları tooan Azure Virtual Network Bağlan
* VPN ile şirket içi ağ tooan Azure Virtual Network Bağlan
* Ayrılmış bir WAN bağlantısı ile şirket içi ağ tooan Azure Virtual Network Bağlan
* Diğer Azure sanal ağlar tooeach Bağlan

### <a name="connect-individual-workstations-tooan-azure-virtual-network"></a>Ayrı iş istasyonları tooan Azure Virtual Network Bağlan
Tooenable tek tek geliştiriciler veya işlemleri personel toomanage sanal makineleri ve Hizmetleri Azure istediğinizde zamanlar olabilir. Örneğin, bir Azure sanal ağı tooa sanal makineye erişim ve güvenlik ilkeniz tooindividual sanal makineleri RDP veya SSH uzaktan erişime izin vermiyor. Bu durumda, bir noktadan siteye VPN bağlantısı kullanabilirsiniz.

Merhaba noktası site VPN bağlantısı kullanır hello [SSTP VPN](https://technet.microsoft.com/library/cc731352.aspx) Protokolü tooenable, tooset hello kullanıcı ile hello Azure sanal ağ arasında özel ve güvenli bir bağlantı. Merhaba VPN bağlantısı kurulduktan sonra SSH hello VPN üzerinden bağlantı hello Azure sanal ağ (Merhaba kullanıcı kimlik doğrulaması yapabilir ve yetkili varsayılarak) herhangi bir sanal makinede içine veya hello kullanıcı mümkün tooRDP olacaktır.

Daha fazla bilgi edinin:

* [Sanal ağ PowerShell kullanarak bir noktadan siteye bağlantı tooa yapılandırın](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-vpn"></a>VPN ile şirket içi ağınızı tooan Azure Virtual Network Bağlan
Tüm şirket ağı veya onu tooan Azure Virtual Network bölümlerini tooconnect isteyebilirsiniz. Bu karma BT ortak senaryolar burada şirketler [Azure'da kendi şirket içi veri merkezine genişletmek](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84). Çoğu durumda şirketler Azure bölümleri şirket içi ve Azure ve arka uç veritabanı şirket içi bir çözüm ön uç web sunucuları ne zaman içerir gibi hizmet bölümlerini barındırır. Bu tür "şirket içi" bağlantılar da bulunan Azure Yönetimi olun kaynakları daha güvenli ve Azure Active Directory etki alanı denetleyicileri genişletme gibi senaryolar etkinleştirin.

Tek yönlü tooaccomplish toouse budur bir [siteden siteye VPN](https://www.techopedia.com/definition/30747/site-to-site-vpn). Merhaba arasındaki siteden siteye VPN ve noktadan siteye VPN siteden siteye VPN (örneğin, şirket içi ağınıza) tüm ağ tooan Azure Virtual Network bağlanırken bir noktadan siteye VPN tek aygıt tooan Azure sanal ağ bağlayan farktır . Siteden siteye VPN tooan Azure Virtual Network hello yüksek güvenlikli IPSec tünel modu VPN protokolü kullanın.

Daha fazla bilgi edinin:

* [Resource Manager Vnet'i hello Azure Portal kullanarak bir siteden siteye VPN bağlantısı ile oluşturma](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [VPN ağ geçidi için planlama ve tasarım](../vpn-gateway/vpn-gateway-plan-design.md)

### <a name="connect-your-on-premises-network-tooan-azure-virtual-network-with-a-dedicated-wan-link"></a>Ayrılmış bir WAN bağlantısıyla, şirket içi ağ tooan Azure Virtual Network Bağlan
Noktadan siteye ve siteden siteye VPN bağlantıları, şirket içi bağlantılar etkinleştirmek için geçerlidir. Ancak, bazı kuruluşlar bunları dezavantajları aşağıdaki toohave hello göz önünde bulundurun:

* VPN bağlantıları hello Internet veri taşıma – bu bu bağlantıları toopotential ilgili güvenlik konularını ortak bir ağ üzerinden veri taşıma ile kullanıma sunar. Ayrıca, güvenilirlik ve Internet bağlantıları için kullanılabilirlik garanti edilemez.
* VPN bağlantıları tooAzure sanal ağlar, bazı uygulamalar ve olarak yaklaşık 200 MB/sn hızında max çıkışı amaçlar için bant genişliği kısıtlı kabul.

En yüksek düzeyde güvenlik ve kullanılabilirlik kendi şirket içi bağlantılar için genellikle hello kuruluşlar adanmış WAN bağlantılarını tooconnect tooremote siteleri kullanın. Azure özelliği toouse, şirket içi ağ tooan Azure Virtual Network tooconnect kullanabileceğiniz ayrılmış bir WAN bağlantısı hello sağlar. Bu Azure ExpressRoute aracılığıyla etkinleştirilir.

Daha fazla bilgi edinin:

* [ExpressRoute teknik genel bakış](../expressroute/expressroute-introduction.md)

### <a name="connect-azure-virtual-networks-tooeach-other"></a>Azure sanal ağlar tooEach bağlanmak diğer
Toouse mümkündür dağıtımlarınız için çok sayıda Azure sanal ağlar. Neden bunu yapabilirsiniz pek çok neden vardır. Merhaba nedenlerden biri dolayısıyla toosimplify yönetim olabilir; başka bir güvenlik nedenleriyle olabilir. Merhaba motivasyon veya kaynakları farklı Azure sanal ağlarda yerleştirme stratejinin bağımsız olarak her bir diğeriyle hello ağları tooconnect kaynakları istediğinizde zamanlar olabilir.

Bir seçenek olacaktır başka bir Azure sanal ağındaki bir Azure sanal ağ tooconnect tooservices Hizmetleri için "geri döngü yapmasıyla" Merhaba Internet üzerinden. Merhaba bağlantı, bir Azure sanal ağ üzerinde hello Internet gidin ve toohello hedef Azure sanal ağ geri dönün. Bu seçenek hello bağlantı toohello güvenlik sorunları devralınan tooany Internet tabanlı iletişim kullanıma sunar.

Daha iyi bir seçenek bir Azure sanal ağı Azure sanal ağ siteden siteye VPN toocreate olabilir. Siteden siteye VPN kullanan bu Azure sanal ağı Azure sanal ağ aynı hello [IPSec tünel modu](https://technet.microsoft.com/library/cc786385.aspx) Protokolü yukarıda belirtilen hello şirket içi siteden siteye VPN bağlantısı olarak.

bir Azure sanal ağı Azure sanal ağ siteden siteye VPN kullanarak hello avantajı hello VPN bağlantısı hello hello Internet bağlanma yerine Azure ağ yapısı üzerinden kurulur olmasıdır. Bu, ek bir güvenlik katmanı hello Internet bağlanma toosite siteye VPN'lerde karşılaştırıldığında sağlar.

Daha fazla bilgi edinin:

* [Azure Resource Manager ve PowerShell kullanarak VNet-VNet bağlantı yapılandırma](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

## <a name="availability"></a>Kullanılabilirlik
Kullanılabilirlik herhangi bir güvenlik programı anahtar bir bileşenidir. Kullanıcılar ve sistemlerden erişemiyor, hangi bunlar hello üzerinden tooaccess hello ağ, hizmet güvenliği ihlal olarak kabul edilmelidir. Azure ağ teknolojileri yüksek kullanılabilirlik mekanizmaları aşağıdaki Bu destek hello sahiptir:

* HTTP tabanlı Yük Dengeleme
* Ağ düzeyinde Yük Dengeleme
* Genel Yük Dengeleme

Yük Dengeleme tasarlanmış mekanizması tooequally dağıtmak birden çok aygıt arasında bağlantı olur. Yük Dengelemesi hello hedefleri şunlardır:

* Kullanılabilirlik – Bakiye bağlantıları birçok cihaz arasında yük, bir veya daha fazla hello aygıtları kullanılamaz hale gelebilir ve çevrimiçi aygıtları kalan hello üzerinde çalışan hello Hizmetleri hello hizmet tooserve Merhaba içeriğine devam edebilirsiniz artırın
* Performansı artırmak – birden çok cihazda Bakiye bağlantıları yüklediğinizde, tek bir cihazı tootake hello işlemci yok ulaştı. Bunun yerine, hello içeriği sunması için hello işleme ve bellek taleplerini yayılır birçok cihaz arasında.

### <a name="http-based-load-balancing"></a>HTTP tabanlı Yük Dengeleme
Kuruluşlar çalışma web tabanlı hizmetler genellikle bir HTTP tabanlı yük dengeleyici bu web hizmetleri toohelp önünde toohave işlemleriniz güvence altına yeterli düzeyde performans ve yüksek kullanılabilirlik. Buna karşılık tootraditional ağ tabanlı yük dengeleyici, hello tarafından HTTP tabanlı yük dengeleyici Yük Dengeleme kararlara hello ağ ve Aktarım katmanı protokolleri üzerinde hello HTTP protokolü özelliklere dayanır.

tooprovide, web tabanlı hizmetler için HTTP tabanlı Yük Dengeleme Azure Azure uygulama ağ geçidi hello sağlar. Hello Azure uygulama ağ geçidi destekler:

* HTTP tabanlı yük dengelemesi – Yük Dengeleme kararları yapılma tabanlı özellik özel toohello HTTP Protokolü
* Tanımlama bilgisi tabanlı oturum benzeşimi – bu özellik bu yük dengeleyici arkasında hello sunucularının tooone hello istemci ve sunucu arasında değişmeden kalır bağlantı kuran emin olur. Bu işlemler kararlılığını oluşturmasını sağlar.
* Bir istemci bağlantı kurulur zaman hello yük dengeleyici ile oturum hello yük dengeleyici ile Merhaba istemci arasında hello HTTPS kullanılarak şifrelenir SSL boşaltma – (SSL /) protokolü. Ancak, sipariş tooincrease performans hello seçeneği toohave hello hello yük dengeleyici arkasında hello yük dengeleyici kullanım hello (şifrelenmemiş) HTTP protokolü hello web sunucusu arasındaki bağlantınız. Merhaba web sunucuları hello yük dengeleyicinin arkasındaki hello işlemci yükü şifrelemeyle ilgili deneyimi yok ve bu nedenle mümkün tooservice istekleri daha hızlı olmalıdır başvurulan tooas "SSL boşaltma" olmasıdır.
* URL tabanlı içerik yönlendirme – bu özellik, burada tooforward bağlantıları hello hedef URL temel alınarak hello yük dengeleyici toomake ilgili kararları için mümkün kılar. Bu, Yük Dengeleme kararları IP adreslerine dayalı olun çözümleri çok daha fazla esneklik sağlar.

Daha fazla bilgi edinin:

* [Uygulama ağ geçidi'ne genel bakış](../application-gateway/application-gateway-introduction.md)

### <a name="network-level-load-balancing"></a>Ağ düzeyinde Yük Dengeleme
Buna karşılık, tooHTTP tabanlı Yük Dengeleme ağ düzeyinde Yük Dengeleme Yük Dengeleme kararları IP adresi ve bağlantı noktası (TCP veya UDP) sayılara göre yapar.
Azure'da hello Azure yük dengeleyici kullanarak ağ düzeyinde yük dengelemenin hello avantajları elde. Hello Azure yük dengeleyici anahtar bazı özellikleri şunlardır:

* IP adresi ve bağlantı noktası numaralarını temel ağ düzeyinde Yük Dengelemesi
* Tüm uygulama katmanı protokol desteği
* TooAzure sanal makinelerin yükünü dengeleyen ve rol örnekleri bulut Hizmetleri
* İnternete dönük (Dış Yük Dengeleme) ve Internet olmayan için kullanılabilir (iç Yük Dengeleme) uygulamalar ve sanal makineleri karşılıklı
* Merhaba yük dengeleyicinin arkasındaki hello hizmetlerinden herhangi biri kullanılamaz duruma gelmiş varsa, kullanılan toodetermine olan, uç noktası izleme

Daha fazla bilgi edinin:

* [Birden çok Sanal Makine veya hizmet arasında İnternet’e yönelik yük dengeleyici](../load-balancer/load-balancer-internet-overview.md)
* [İç yük dengeleyiciye genel bakış](../load-balancer/load-balancer-internal-overview.md)

### <a name="global-load-balancing"></a>Genel Yük Dengeleme
Bazı kuruluşlar hello yüksek düzeyde kullanılabilirlik olası isteyeceksiniz. Bu toohost uygulamalarda genel hedeftir tek yönlü tooreach veri merkezleri dağıtılmış. Merhaba dünya genelinde bulunan veri merkezlerinde uygulama barındırıldığında, bir tüm jeopolitik bölge toobecome kullanılamaz ve hala için Merhaba uygulaması olası ve çalışır durumdadır.

Ayrıca uygulamalar genel olarak dağıtılmış veri merkezlerinde barındırarak almak toohello kullanılabilirlik avantajları performans avantajı da alabilirsiniz. Bu performans avantajı hello isteği yapan toohello aygıt en yakın hello hizmet toohello datacenter isteklerinde yönlendiren bir mekanizma kullanılarak elde edilebilir.

Genel Yük Dengeleme avantajlar hem de sağlayabilir. Azure'da hello Azure trafik Yöneticisi'ni kullanarak genel Yükü Dengeleme faydaları elde edebilirsiniz.

Daha fazla bilgi edinin:

* [Traffic Manager nedir?](../traffic-manager/traffic-manager-overview.md)


## <a name="name-resolution"></a>Ad çözümlemesi
Ad çözümlemesi, tüm hizmetleri Azure'da barındırmak için kritik bir işlevdir. Güvenlik açısından bakıldığında, hello ad çözümleme işlevini tooan saldırgan yeniden yönlendirme istekleri siteleri tooan saldırganın sitesinden bırakılmasına neden olabilir. Güvenli ad çözümlemesi tüm barındırılan bulut Hizmetleri için gerekli değildir.

İki tür, ad çözümlemesinin tooaddress ihtiyacınız vardır:

* Dahili ad çözümlemesi – dahili ad çözümlemesi, Azure sanal ağlar, şirket içi ağlarınızı ya da her ikisini de Hizmetleri tarafından kullanılır. İç ad çözümlemesi için kullanılan adları hello Internet erişilebilir değildir. En iyi güvenlik için iç ad çözümlemesi düzeninizi değil erişilebilir tooexternal kullanıcılar olması önemlidir.
* Dış ad çözümlemesi – dış ad çözümlemesi, insanların ve cihazların şirket içi ve Azure sanal ağlar dışında tarafından kullanılır. Bunlar görünür toohello Internet ve kullanılan toodirect bağlantı tooyour bulut tabanlı hizmetler hello adlardır.

Dahili ad çözümlemesi için iki seçeneğiniz vardır:

* Yeni bir Azure sanal ağ, oluşturduğunuzda, bir Azure sanal ağ DNS sunucusu – bir DNS sunucusu sizin için oluşturulur. Bu DNS sunucusu, Azure sanal ağınızda bulunan hello makinelerin hello adlarını çözümleyebilir. Bu DNS sunucusu yapılandırılabilir değildir ve dolayısıyla güvenli ad çözümlemesi çözüm yapmadan hello Azure doku Yöneticisi tarafından yönetilir.
* DNS sunucunuzun Getir – kendi Azure sanal ağınızda seçme bir DNS sunucusu koyma hello seçeneğiniz vardır. Bu DNS sunucusu, DNS sunucusu veya Azure Marketi hello edinebilirsiniz bir Azure ortak tarafından sağlanan adanmış bir DNS sunucusu çözümü bir Active Directory tümleşik olabilir.

Daha fazla bilgi edinin:

* [Sanal ağ genel bakış](../virtual-network/virtual-networks-overview.md)
* [Bir sanal ağ (VNet) tarafından kullanılan DNS sunucularını yönetin](../virtual-network/virtual-network-manage-network.md#dns-servers)

Dış DNS çözümlemesi için iki seçeneğiniz vardır:

* Kendi dış DNS sunucusu şirket içi ana bilgisayar
* Kendi dış DNS sunucusu hizmeti sağlayıcısı ile ana bilgisayar

Birçok büyük kuruluşların kendi DNS sunucuları şirket içi barındırır. Bu nedenle ağ uzmanlık ve genel varlığından toodo hello sahip oldukları için bunlar bunu yapabilirsiniz.

Çoğu durumda bu DNS ad çözümlemesi ile bir hizmet sağlayıcısı Hizmetleri daha iyi toohost olur. Bu hizmet sağlayıcıları ad çözümleme hizmetleri için genel varlığından tooensure çok yüksek kullanılabilirlik ve hello ağ uzmanlığa sahip. Başarısız, ad çözümleme hizmetleri, hiç kimse olur çünkü DNS hizmetleri için kullanılabilirlik gerekli hizmetleri, Internet'e mümkün tooreach olabilir.

Azure sağlar, yüksek oranda kullanılabilir ve kullanıcı dış DNS çözüm Azure DNS hello biçiminde. Bu dış ad çözümlemesi çözüm Merhaba Dünya çapında Azure DNS altyapısı yararlanır. Toohost tanır Azure kullanarak, etki alanı, diğer Azure hizmetleriyle aynı kimlik bilgileri, API'leri, Araçlar ve faturalama hello. Azure bir parçası olarak hello platformuna yerleşik hello güçlü güvenlik denetimleri de devralır.

Daha fazla bilgi edinin:

* [Azure DNS'ye genel bakış](../dns/dns-overview.md)

## <a name="dmz-architecture"></a>DMZ mimarisi
Birçok büyük kuruluşlar kendi ağları toocreate arabellek bölge hello Internet ve kendi hizmetleri arasında DMZ'ler toosegment kullanın. Merhaba DMZ hello ağ kısmı düşük güvenlikli bölgenin olarak kabul edilir ve hiçbir yüksek değerli varlıklar, ağ kesimine yerleştirilir. Merhaba DMZ segment ve sanal makineleri ve gelen hello Internet bağlantılarını kabul Hizmetleri sahip başka bir ağ arabirimi bağlı tooa ağ bir ağ arabirimine sahip ağ güvenlik aygıtları genellikle görürsünüz.

DMZ tasarım ve hello karar toodeploy DMZ ve ardından bir toouse karar verirseniz DMZ toouse ne tür ağ güvenlik gereksinimlerinizi temel alarak çeşidi vardır.

Daha fazla bilgi edinin:

* [Microsoft bulut Hizmetleri ve ağ güvenliği](../best-practices-network-security.md)


## <a name="monitoring-and-threat-detection"></a>İzleme ve tehdit algılama

Azure özellikleri toohelp sağlar, bu anahtar alanında erken algılama, izleme ve hello özelliği toocollect ve gözden geçirme ağ trafiği ile.

### <a name="azure-network-watcher"></a>Azure Ağ İzleyicisi
Azure Ağ İzleyicisi çok sayıda gidermeye yardımcı olarak araçları tooassist yepyeni bir dizi güvenlik sorunları hello kimliği ile sağlayın özellikleri içerir.

[Güvenlik grubu görünümü ](/network-watcher/network-watcher-security-group-view-overview.md) kullanılan tooperform her Vm'leriniz için kuruluş tooeffective kurallarınızı tarafından tanımlanan hello temelleri ilkeleri karşılaştırma programlı denetimleri olabilir ve sanal makineleri denetim ve güvenlik uyumluluğunu ile yardımcı olur. Bu, tüm yapılandırma değişikliklerini belirlemenize yardımcı olabilir.

[Paket yakalama](/network-watcher/network-watcher-packet-capture-overview.md) toocapture ağ trafiği tooand hello sanal makineden sağlar. Yardımcı toocollect ağ istatistikleri sağlayarak ve hello uygulamasının sorun giderme yanı sıra sorunları paket yakalama ağ yetkisiz hello araştırma içinde çok yararlı olabilir. Bu işlev Azure toostart ağ yakalamaları yanıt toospecific Azure işlevleri ile birlikte de kullanabilirsiniz uyarıları.

Azure Ağ İzleyicisi'ni ve nasıl bazı hello işlevlerini, Labs'de sınama toostart hello bakalım hakkında daha fazla bilgi için [Azure Ağ İzleyicisi izlemeye genel bakış](/network-watcher/network-watcher-monitoring-overview.md)

>[!NOTE]
Bunu değil sahip hello şekilde azure Ağ İzleyicisi kullanılabilirliği ve güvenilirliği genel kullanılabilirlik sürümü, hizmetler olarak aynı düzeyde hala genel önizlemede değil. Belirli özellikler desteklenmiyor olabilir, yetenekleri kısıtlı ve tüm Azure konumlarda kullanılamayabilir. Merhaba Hello en güncel bildirimleri için kullanılabilirlik ve bu hizmetin durumunu denetleme [Azure güncelleştirmeler sayfası](https://azure.microsoft.com/updates/?product=network-watcher)

### <a name="azure-security-center"></a>Azure Güvenlik Merkezi
Güvenlik Merkezi, engellemenize, algılamanıza ve toothreats yanıt yardımcı olur ve artan, görünürlük ve denetim üzerinden, Azure kaynaklarınızın hello güvenlik sağlar. Azure aboneliklerinize arasında tümleşik güvenlik izleme ve ilke yönetimi sağlar, kaçabilecek tehditleri ve çok sayıda güvenlik çözümleri çalışır algılamaya yardımcı olur.

Azure Güvenlik Merkezi en iyi duruma getirme ve ağ güvenliği tarafından izlemenize yardımcı olur:

* Ağ güvenlik önerileri sağlama
* Ağ güvenliği yapılandırması Hello durumunu izleme
* Temel toonetwork tehditleri hem hello uç ve ağ düzeylerinde uyarı

Daha fazla bilgi edinin:

* [Giriş tooAzure Güvenlik Merkezi](../security-center/security-center-intro.md)


### <a name="logging"></a>Günlüğe kaydetme
Ağ düzeyinde günlüğe kaydetme, bir ağ güvenlik senaryonuz için anahtar bir işlevdir. Azure üzerinde ağ güvenlik grupları tooget ağ düzeyi bilgileri günlüğe kaydetme için elde edilen bilgilerle oturum açabilir. NSG günlüğüyle bilgileri alın:

* [Etkinlik günlükleri](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) – Bu günlükler kullanılan tooview olan tüm işlemleri tooyour Azure gönderilen abonelikleri. Bu günlükler varsayılan olarak etkindir ve hello Azure portalı içinde kullanılabilir. Daha önce "Denetim günlüklerini" veya "İşletimsel Logs" olarak bilinirdi.
* Olay günlükleri – Bu günlükler hangi NSG kuralları uygulanan hakkında bilgi sağlar.
* Sayaç günlükleri – Bu günlükler uygulanan toodeny her NSG kural edildi kaç kez bildiğiniz izin izin verme veya trafiği.

Aynı zamanda [Microsoft Power BI](https://powerbi.microsoft.com/what-is-power-bi/), güçlü veri görselleştirme aracı, tooview ve bu günlüklerini analiz edin.

Daha fazla bilgi edinin:

* [Ağ güvenlik grupları (Nsg'ler) için günlük analizi](../virtual-network/virtual-network-nsg-manage-log.md)
