---
title: "aaaAzure ağ güvenlik en iyi uygulamalar | Microsoft Docs"
description: "Bazı hello anahtar özellikleri Azure toohelp kullanılabilir güvenli ağ ortamları oluşturma öğrenin"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: d169387a-1243-4867-a602-01d6f2d8a2a1
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: b851b2862428a8bd5e7525c85584fc1c14ffcabe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-cloud-services-and-network-security"></a>Microsoft bulut Hizmetleri ve ağ güvenliği
Microsoft bulut hizmetlerine hiper ölçekli hizmetler ve altyapı, Kurumsal düzeydeki özellikleri ve karma bağlantı için birçok seçenek sunar. Müşteriler, bu hizmetleri hello Internet üzerinden veya özel ağ bağlantısı sağlayan Azure ExpressRoute ile tooaccess seçebilirsiniz. Merhaba Microsoft Azure platformu tooseamlessly altyapılarını hello bulutunu oluşturmak ve genişletmek için çok katmanlı mimarileri müşterilerin olanak tanır. Ayrıca, üçüncü tarafların güvenlik hizmetleri ve sanal gereçler sunarak Gelişmiş özellikleri etkinleştirebilirsiniz. Bu teknik incelemede güvenlik ve müşteriler, ExpressRoute aracılığıyla erişilebilir Microsoft bulut hizmetlerini kullanırken dikkate almanız gereken mimari sorunları genel bakış sağlar. Ayrıca, Azure sanal ağları daha güvenli Hizmetleri oluşturulması ele alınmaktadır.

## <a name="fast-start"></a>Hızlı Başlat
mantığı grafiği aşağıdaki Merhaba, tooa belirli örneği hello birçok güvenlik teknikleri hello Azure platformu ile yönlendirebilirsiniz. Hızlı başvuru için en iyi durumunuz uyan hello örnek bulun. Genişletilmiş açıklamalar için hello kağıt okuma devam edin.
[![0]][0]

[Örnek 1: bir çevre ağında (DMZ, sivil bölge veya denetimli alt ağ olarak da bilinir) yapı toohelp koruma uygulamaları ile ağ güvenlik grupları (Nsg'ler).](#example-1-build-a-perimeter-network-to-help-protect-applications-with-nsgs)</br>
[Örnek 2: bir çevre yapı ağ toohelp uygulamaları bir güvenlik duvarı ve Nsg'ler ile koruyun.](#example-2-build-a-perimeter-network-to-help-protect-applications-with-a-firewall-and-nsgs)</br>
[Örnek 3: bir çevre yapı ağ toohelp ağ güvenlik duvarı, kullanıcı tanımlı yönlendirme (UDR) ve NSG ile koruyun.](#example-3-build-a-perimeter-network-to-help-protect-networks-with-a-firewall-and-udr-and-nsg)</br>
[Örnek 4: bir siteden siteye, sanal Gereci sanal özel ağ (VPN) ile karma bağlantı ekleyin.](#example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn)</br>
[Örnek 5: bir siteden siteye Azure VPN ağ geçidi ile karma bağlantı ekleyin.](#example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway)</br>
[Örnek 6: ExpressRoute ile karma bağlantı ekleyin.](#example-6-add-a-hybrid-connection-with-expressroute)</br>
Sanal ağlar, yüksek kullanılabilirlik ve hizmet zincirleme arasındaki bağlantıları ekleme örnekleri, sonraki birkaç ay hello toothis belge eklenir.

## <a name="microsoft-compliance-and-infrastructure-protection"></a>Microsoft uyumluluk ve altyapısını koruma
toohelp kuruluşlar ile national, bölgesel, uyumlu ve hello koleksiyonu ve bireylerin verilerin kullanımını yöneten sektöre özgü gereksinimler Microsoft 40'dan sertifikaları ve attestations sunar. Merhaba en kapsamlı herhangi bir bulut hizmeti sağlayıcısına ayarlayın.

Daha fazla bilgi için hello uyumluluk hello hakkında bilgi [Microsoft Trust Center][TrustCenter].

Microsoft, bir kapsamlı bir yaklaşım tooprotect bulut gerekli altyapıyı toorun hiper ölçekli küresel hizmetler sahiptir. Microsoft bulut altyapısı içeren donanım, yazılım, ağlar ve yönetim ve işlem personeli, ayrıca toohello fiziksel veri merkezi.

![2]

Bu yaklaşım, kendi hello Microsoft bulut hizmetlerinde müşteriler toodeploy için daha güvenli bir temel sağlar. Hello sonraki adım için müşteriler toodesign olduğu ve bu Hizmetleri güvenlik mimarisi tooprotect oluşturun.

## <a name="traditional-security-architectures-and-perimeter-networks"></a>Geleneksel güvenlik mimarisi ve Çevre ağları
Microsoft yoğun hello bulut altyapısı koruma invests rağmen müşterilerin da bulut hizmetlerinin ve kaynak grupları korumanız gerekir. Çok katmanlı bir yaklaşım toosecurity hello en iyi savunma sağlar. Bir çevre ağ güvenlik bölgesi iç ağ kaynaklarına güvenilmeyen bir ağdan korur. Bir çevre ağına toohello kenarları veya hello Internet ve korumalı hello kurumsal BT altyapısı arasında sit hello ağ parçalarını gösterir.

Tipik kurumsal ağlarda, hello çekirdek altyapıyı yoğun olarak birden çok katmanlı güvenlik cihazların Merhaba çevreyi adresindeki fortified. Her bir katmanın Hello sınır, aygıtları ve ilke zorlama noktaları oluşur. Her katman ağ güvenlik aygıtları aşağıdaki hello bir birleşimini içerebilir: güvenlik duvarları, hizmet reddi (DoS) önleme, izinsiz giriş algılama veya koruma sistemleri (Kimlikleri/IP) ve VPN aygıtları. İlke zorlama güvenlik duvarı ilkeleri, erişim denetim listelerini (ACL'ler) ya da belirli yönlendirme hello form alabilir. Merhaba ilk doğrudan hello Internet'ten gelen trafiği kabul hello ağındaki savunma hattı hello ağınıza daha fazla meşru istekler verirken bir bu düzenekleri tooblock saldırıları ve zararlı trafiği birleşimidir. Bu trafiği doğrudan hello çevre ağında tooresources yönlendirir. Bu kaynak sonra "Merhaba sonraki sınır doğrulama için transiting hello ağındaki derin tooresources ilk konuşun". Bu hello ağ gösterilen toohello her iki tarafında koruma bazı formuyla genellikle Internet parçası olduğundan hello en dıştaki katman hello çevre ağ olarak adlandırılır. Merhaba aşağıdaki şekilde bir tek alt ağ çevre ağı örneği iki güvenlik sınırları ile bir şirket ağında gösterilmektedir.

![3]

Bir çevre ağına birçok kullanılan mimarileri tooimplement vardır. Bu mimari her sınır tooblock trafiği en çok çeşitli olduğundan farklı mekanizmaları ile bir basit yük dengeleyici tooa birden çok alt ağ çevre ağından aralığı ve hello daha derin Katmanlar hello şirket ağının koruyun. Merhaba çevre ağı nasıl yapılandırıldığını hello kuruluş ve genel kendi risk toleransınıza hello belirli gereksinimlerinize bağlıdır.

Müşteriler kendi iş yükleri toopublic Bulutlar taşımak gibi çevre ağ mimarisinde Azure toomeet uyumluluk ve güvenlik gereksinimleri için kritik toosupport benzer özellikleri gereklidir. Bu belge, müşterilerin Azure güvenli ağ ortamında nasıl oluşturabileceğiniz yönergeleri sağlar. Merhaba çevre ağı üzerinde odaklanır, ancak ağ güvenliği pek çok görünüşünün kapsamlı bir tartışma de içerir. Bu tartışma sorular aşağıdaki hello bildirin:

* Nasıl bir çevre ağında Azure yerleştirilmiş olabilir?
* Hello Azure özellikleri kullanılabilir toobuild hello çevre ağı bazıları nelerdir?
* Arka uç iş yükleri nasıl korunabilir?
* Nasıl Internet iletişimi denetlenen toohello azure'da iş yüklerini misiniz?
* Nasıl hello şirket içi ağlar Azure dağıtımlardan korunabilir?
* Ne zaman yerel Azure güvenlik özellikleri üçüncü taraf uygulamaları veya hizmetleri karşı kullanılsın mı?

Aşağıdaki diyagramda hello Azure toocustomers sağlayan güvenlik çeşitli katmanları gösterilmektedir. Bu katmanlar hello Azure platformu kendisini yerel ve müşteri tarafından tanımlanan özellikler şunlardır:

![4]

Merhaba Internet, Azure Azure karşı büyük ölçekli saldırılara karşı korunmasına yardımcı DDoS geldiği. Merhaba sonraki hangi trafiğin hello bulut hizmeti toohello sanal ağ üzerinden geçebilmesi kullanılan toodetermine olan müşteri tanımlı genel IP adresleri (Bitiş) katmanıdır. Yerel Azure sanal ağ yalıtımı diğer ağlarla tam yalıtımı sağlar ve trafik yalnızca yapılandırılan kullanıcı yolları ve yöntemleri akar. Bu yolları ve yöntemleri Nsg'ler, UDR ve ağ sanal Gereçleri korumalı hello ağda kullanılan toocreate güvenlik sınırları tooprotect hello uygulama dağıtımları burada olabilir hello İleri, katmandır.

Merhaba sonraki bölümde, Azure sanal ağlar genel bir bakış sağlar. Bu sanal ağlar müşteriler tarafından oluşturulan ve dağıtılan yüklerini ne bağlanan olan. Sanal ağlar tüm hello ağ güvenlik özellikleri hello temelini tooestablish Azure bir çevre ağ tooprotect müşteri dağıtımlarında gereklidir.

## <a name="overview-of-azure-virtual-networks"></a>Azure sanal ağlar genel bakış
Internet trafiğini toohello Azure sanal ağlar sağlayabilmek için önce güvenlik devralınan toohello Azure platformu iki katmanı vardır:

1.    **DDoS koruması**: DDoS koruması olan bir hello hello Azure platformu kendisini büyük ölçekli Internet tabanlı saldırılara karşı korur Azure fiziksel ağ katmanı. Bu saldırıların birden çok "bot" düğümleri bir girişim toooverwhelm Internet hizmetini kullanır. Azure sağlam bir DDoS koruması kafes tüm gelen, giden ve çapraz Azure bölgesi bağlantı vardır. Bu DDoS koruma katmanı kullanıcı yapılandırılabilir özniteliklere sahip ve erişilebilir toohello müşteri değildir. büyük ölçekli saldırılara karşı bir platform olarak Azure Hello DDoS koruma katmanı korur, dışarı bağlı ve çapraz Azure bölgesini trafiği de izler. Ağ sanal Gereçleri hello VNet üzerinde kullanarak, esnek ek katmanlar, hello platform düzeyinde koruma seyahat değil daha küçük bir ölçek saldırılara karşı hello müşteri tarafından yapılandırılabilir. DDoS örneği eylem; internet'e yönelik IP adresi büyük ölçekli bir DDoS saldırılarına gerçekleşirse Azure hello kaynakları hello saldırıları algılamak ve hedeflenen hedefine ulaşıldı önce trafiği sorunlu hello kaydırın. Neredeyse tüm durumlarda hello Saldırıya uğrayan bitiş noktası tarafından hello saldırı etkilenmez. Bir uç nokta etkilenir hello nadir durumlarda, hiçbir, etkilenen tooother uç noktaları, uç nokta saldırıya hello trafiğidir. Bu nedenle diğer müşteriler ve Hizmetleri bu saldırılara karşı etkisi görür. Azure DDoS yalnızca için büyük ölçekli saldırıları arıyor kritik toonote olur. Merhaba platform düzeyinde koruma eşikleri aşıldı önce belirli hizmetinizi çok mümkündür. Örneğin, tek bir A0 IIS sunucusunda bir web sitesi alınması çevrimdışı bir DDoS saldırılarına Azure platformu düzeyi DDoS koruma bir tehdit kayıtlı önce.

2.  **Genel IP adresleri**: genel IP adresleri (hizmet uç noktaları, genel IP adresleri, uygulama ağ geçidi ve bir ortak IP adresi toohello yönlendirilmiş Internet tooyour kaynağı sunmak diğer Azure özellikleri etkin) bulut Hizmetleri izin vermek veya Kaynak toohave ortak Internet IP adresleri ve bağlantı noktaları kullanıma sunulan gruplandırır. Merhaba endpoint hello Azure sanal ağı üzerinde ağ adresi çevirisi (NAT) tooroute trafiği toohello iç adresi ve bağlantı noktasını kullanır. Bu yol hello birincil dış trafiğin toopass hello sanal ağda yoludur. hangi trafik geçirilen yapılandırılabilir toodetermine Hello genel IP adresleri olan ve nasıl ve nerede toohello sanal ağda çevrilir.

Trafik hello sanal ağ ulaştığında, oyuna gelen birçok özellik vardır. Azure sanal ağları olan hello foundation müşteriler tooattach için iş yüklerini ve temel ağ düzeyinde güvenlik geçerli olduğu. Bu özel ağ (sanal ağ kaplama) Azure'da hello sahip müşteriler için olan özellikleri ve özelliklere aşağıdaki:

* **Trafik yalıtımı**: Merhaba trafik yalıtımı hello Azure platformu sınırında sanal ağdır. Farklı bir sanal ağ, her iki sanal ağ tarafından oluşturulan olsa bile tooVMs aynı müşteri hello doğrudan bir sanal ağdaki sanal makinelerden (VM'ler) iletişim kuramıyor. Yalıtım müşteri sanal makineleri sağlar önemli bir özelliktir ve iletişim bir sanal ağ içindeki özel kalır.

>[!NOTE]
>Trafik yalıtımı başvuruyor yalnızca tootraffic *gelen* toohello sanal ağ. Merhaba VNet toohello giden trafiği varsayılan olarak Internet izin verilir, ancak Nsg'ler tarafından istenirse engellenebilir.
>
>

* **Çok katmanlı topoloji**: sanal ağlar alt ağların ayırma ve farklı öğeler veya kendi iş yüklerinin "katmanları" için ayrı adres alanlarını belirleme tarafından toodefine çok katmanlı topoloji müşteriler izin. Bu mantıksal gruplar ve Topolojileri hello iş yükü türlerine göre müşteriler toodefine farklı erişim ilkesini etkinleştirmek ve ayrıca hello katmanları arasında trafik akışına denetim.
* **Şirket içi bağlantılar**: müşteriler Azure'da bir sanal ağ ve birden çok şirket içi siteler veya diğer sanal ağlar arasında şirketler arası bağlantı kurmak. bir bağlantı tooconstruct, müşterilerin VNet eşlemesi, Azure VPN ağ geçitleri, üçüncü taraf ağ sanal Gereçleri veya ExpressRoute kullanabilirsiniz. Azure standart IPSec/IKE protokolleri ve ExpressRoute özel bağlantıyı kullanarak siteden siteye (S2S) VPN destekler.
* **NSG** müşterilerin toocreate kuralları (ACL) istenen hello ayrıntı düzeyinde olanak tanır: ağ arabirimleri, tek tek sanal makineleri veya sanal alt ağlar. Müşteriler erişimine izin verme veya reddetme hello iş yükleri bir sanal ağdan şirket içi bağlantılar aracılığıyla müşterinin ağlarındaki sistemleri arasındaki iletişimi tarafından erişimi denetlemek veya Internet iletişimi doğrudan.
* **UDR** ve **IP iletimi** müşteriler toodefine hello iletişim yolları bir sanal ağ içindeki farklı katmanları arasında izin. Müşteriler bir güvenlik duvarı, Kimlikleri/IP'leri ve diğer sanal gereçler dağıtmak ve bu güvenlik Gereçleri güvenlik sınırı İlkesi zorlaması, Denetim ve denetleme yoluyla ağ trafiğini yönlendirmek.
* **Ağ sanal Gereçleri** hello Azure Marketi içinde: güvenlik duvarları, yük Dengeleyiciler ve Kimlikler/IP'leri gibi güvenlik Gereçleri hello Azure Marketi kullanılabilir olduğunu ve VM görüntü Galerisi hello. Müşteriler bu cihazları kendi sanal ağlara ve özellikle, kendi güvenlik sınırları (Merhaba çevre ağ alt ağları dahil) toocomplete çok katmanlı güvenli ağ ortamında dağıtabilir.

Bu özellik ve yetenekler diyagramı aşağıdaki hello bir çevre ağ mimarisi ile Azure nasıl oluşturulabilir, bir örnek verilmiştir:

![5]

## <a name="perimeter-network-characteristics-and-requirements"></a>Çevre ağ özellikleri ve gereksinimleri
Merhaba çevre ağı hello ön uç hello ağın, doğrudan hello Internet iletişimi arabirim ' dir. Karşılama gelen paketleri hello güvenlik duvarı, Kimlikleri ve IP'leri, gibi hello güvenlik Gereçleri hello arka uç sunucularına ulaşması önce akışına. Internet'e bağlı paketler hello iş yükleri de ilke zorlaması, denetleme ve denetim amacıyla, hello ağ ayrılmadan önce hello çevre ağında hello güvenlik Gereçleri aracılığıyla akabilir. Ayrıca, hello çevre ağındaki müşteri sanal ağlar ve şirket içi ağlar arasında şirket içi VPN ağ geçitleri barındırabilir.

### <a name="perimeter-network-characteristics"></a>Çevre ağ özellikleri
Merhaba önceki şekil başvuran, iyi çevre ağı hello özelliklerini bazıları şunlardır:

* Internet'e yönelik:
  * Merhaba çevre ağ alt kendisini İnternete dönük, doğrudan hello Internet ile iletişim kurmasını ' dir.
  * Genel IP adresleri, VIP'ler ve/veya hizmet uç noktaları Internet trafiği toohello ön uç ağ ve aygıt geçirin.
  * Merhaba ön uç ağ üzerindeki diğer kaynakları önce güvenlik cihazları Internet geçtiği hello trafiğinden gelen.
  * Giden güvenlik etkinleştirilirse, trafiği toohello Internet geçirmeden önce hello son adım olarak, güvenlik aygıtları geçirir.
* Korumalı ağ:
  * Merhaba Internet toohello çekirdek altyapısından doğrudan hiçbir yolu yoktur.
  * Nsg'ler, güvenlik duvarları veya VPN cihazları gibi güvenlik cihazlarını aracılığıyla kanalları toohello çekirdek altyapısına çapraz geçiş gerekir.
  * Diğer cihazları Internet ve hello çekirdek altyapıyı köprü değil.
  * Her ikisi de güvenlik cihazlarda hello Internet'e ve hello korumalı ağ hello çevre ağına (Merhaba önceki resimde gösterildiği gibi hello iki güvenlik duvarı simgeleri) sınırlarının karşılıklı farklı kurallara sahip tek bir sanal gereç gerçekte olabilir veya Her sınır arabirimleri. Merhaba çevre ağına hem sınırları için Hello yükü işleme mantıksal olarak ayrılmış, örneğin, bir fiziksel aygıt.
* Diğer ortak yöntemler ve sınırlamalar:
  * İş yükleri, iş kritik bilgileri depolamamayı gerekir.
  * Erişim ve güncelleştirmeleri tooperimeter ağ yapılandırmalara ve dağıtımlara yetkili sınırlı tooonly yöneticilerdir.

### <a name="perimeter-network-requirements"></a>Çevre ağ gereksinimleri
tooenable şu özelliklere sanal ağ gereksinimleri tooimplement başarılı çevre ağ üzerinde bu yönergeleri izleyin:

* **Alt ağ mimarisi:** belirt hello sanal ağ alt ağın tamamını hello çevre ağı ayrılmış şekilde ayrılmış hello diğer alt ağlara gelen aynı sanal ağ. Bu ayrım hello çevre ağı ve bir güvenlik duvarı ya da Kimlikleri/IP'leri sanal gereç yoluyla diğer iç veya özel alt katmanları akışları arasında hello trafiği sağlar.  Kullanıcı tanımlı yollar alt ağlardır hello sınırında tooforward bu trafiği toohello sanal gereç gereklidir.
* **NSG:** hello çevre ağ alt kendisini hello Internet ile açık tooallow iletişim olmalıdır, ancak bu gelmez müşteriler Nsg'ler atlayarak. Ortak Güvenlik yöntemler toominimize hello ağ kullanıma sunulan yüzeyleri toohello Internet izleyin. Merhaba uzak adres aralıklarını tooaccess hello dağıtımları veya hello özel uygulama protokolleri ve açık bağlantı noktalarını izin kilitleyin. Bir tam kilitleme mümkün olmayan durumlar olabilir. Örneğin, müşterilerin Azure üzerinde bir dış Web sitesi varsa, hello çevre ağındaki tüm ortak IP adreslerinden gelen web isteklerini hello izin vermesi gerekir, ancak yalnızca hello web uygulaması bağlantı noktalarını açmanız gerekir: TCP bağlantı noktası 80 üzerinde ve/veya TCP bağlantı noktası 443'tür.
* **Yönlendirme tablosu:** hello çevre ağ alt kendisini mümkün toocommunicate toohello Internet doğrudan olmalı, ancak bir güvenlik duvarı üzerinden geçmeden doğrudan iletişim tooand ağlardan hello arka uç veya şirket içi izin vermemelidir veya Güvenlik Gereci.
* **Güvenlik Gereci yapılandırması:** tooroute ve hello çevre ağı ve hello rest korumalı hello ağlar arasında paketlerin inceleyin, Güvenlik Duvarı ' nı Kimlikleri, gibi güvenlik Gereçleri hello ve IP'leri cihazları çok konaklı olabilir. Bunlar hello çevre ağı ve hello arka uç alt ağlar için ayrı NIC'ler olabilir. Merhaba NIC'ler hello çevre ağında hello Internet gelen tooand doğrudan iletişim, yönlendirme tablosu ile Merhaba karşılık gelen Nsg'ler ve hello çevre ağ. toohello arka uç alt bağlanma hello NIC'ler daha Nsg'ler ve hello karşılık gelen arka uç alt ağ yönlendirme tablolarını sınırlı.
* **Güvenlik uygulama işlevinin:** hello çevre ağında genellikle dağıtılan hello güvenlik Gereçleri işlevselliği aşağıdaki hello gerçekleştirin:
  * Güvenlik Duvarı: güvenlik duvarı kurallarının veya erişim denetimi ilkeleri hello gelen istekler için zorlamayı.
  * Tehdit algılama ve önleme: algılama ve kötü amaçlı saldırılara karşı hello Internet Azaltıcı.
  * Denetim ve günlük: denetim ve çözümleme için ayrıntılı günlük koruma.
  * Ters proxy: hello gelen yeniden yönlendirme istekleri toohello karşılık gelen arka uç sunucuları. Bu yeniden yönlendirme hello hedef adresleri hello ön uç cihazlarda çevirme genellikle güvenlik duvarları, toohello arka uç sunucu adresleri ve eşleme içerir.
  * İletme proxy: NAT sağlayarak ve hello sanal ağ toohello Internet içinde başlatıldığına iletişimi için denetimi gerçekleştiriliyor.
  * Yönlendirici: gelen ve çapraz alt ağ trafiği hello sanal ağ içinde iletme.
  * VPN cihazı: hello VPN ağ geçitleri için şirketler arası işlevi gören şirketler arası VPN bağlantısı müşterinin şirket içi ağlar ve Azure sanal ağlar arasında.
  * VPN sunucusu: tooAzure sanal ağları birbirine bağlayan VPN istemcileri kabul etme.

> [!TIP]
> İki grupları ayrı aşağıdaki hello tutun: hello kişiler yetkili uygulama geliştirme, dağıtım veya işlemleri yönetici olarak yetkilendirilmiş tooaccess hello çevre ağ güvenlik dişli ve hello kişiler. Bu gruplar ayrı tutmak görevlerini ayrımı için sağlar ve uygulamaların güvenlik ve ağ güvenlik denetimleri atlayarak tek bir kişinin önler.
>
>

### <a name="questions-toobe-asked-when-building-network-boundaries"></a>Ağ sınırları oluştururken sorulan sorular toobe
Bu bölümde, özellikle belirtilmediği sürece, hello terimi "ağlar" tooprivate Azure başvuran bir abonelik Yöneticisi tarafından oluşturulan sanal ağlar. Merhaba terim toohello temel alınan fiziksel ağlar Azure içinde anlamına gelmez.

Ayrıca, Azure sanal ağlar genellikle kullanılan tooextend içi geleneksel ağlardır. Olası tooincorporate olduğu siteden siteye veya ExpressRoute karma ağ çevre ağ mimarisi ile çözümler. Bu karma bağlantı, ağ güvenlik sınırları oluşturmanın önemli bir konudur.

bir çevre ağ ve birden çok güvenlik sınırı olan bir ağ oluştururken hello aşağıdaki üç sorular kritik tooanswer vardır.

#### <a name="1-how-many-boundaries-are-needed"></a>1) kaç tane sınırları gerekli mi?
Merhaba ilk karar noktası kaç güvenlik sınırları içinde belirli bir senaryo gerekli toodecide şöyledir:

* Tek bir sınır: hello sanal ağ ve Internet hello arasındaki hello ön uç çevre ağ üzerinde bir tane.
* İki sınır: hello Internet tarafı hello çevre ağ üzerinde diğeri hello çevre ağ alt ağı ve hello arka uç alt ağlar arasında Azure sanal ağlar hello.
* Üç sınırları: hello çevre ağı hello Internet tarafındaki bir, bir hello çevre ağı ve arka uç alt ağları arasında ve bir hello arka uç alt ağlar arasında ve hello şirket içi ağ.
* N sınırları: değişken numarası. Güvenlik gereksinimlerine bağlı olarak, hiçbir toohello sayısı sınırı belirli bir ağda uygulanabilir güvenlik sınırı yoktur.

Merhaba sayısı ve türü farklılık gerekli sınırları uygulanan bir şirketin riski dayanıklılık ve hello belirli senaryoya bağlı. Bu genellikle genellikle bir risk ve uyumluluk takım, bir ağ ve platform ekip ve bir uygulama geliştirme ekipleri dahil olmak üzere, bir kuruluştaki birden çok grubu ile birlikte kararı verilir. Güvenlik, söz konusu hello veri ve kullanılan hello teknolojileri bilgisine sahip kişilerin, bu kararı tooensure hello uygun güvenlik tutum sergilemek her uygulama için bir say olması gerekir.

> [!TIP]
> Belirli bir durumda hello güvenlik gereksinimlerini karşılayan sınırları en az sayıda Hello kullanın. Daha fazla sınırlarıyla işlemlerini ve sorun giderme daha zor yanı yönetim hello yönetmeye ek yükü söz konusu zaman içinde birden fazla sınır ilkeleri hello. Ancak, yetersiz sınırları riski artırır. Bulma hello Bakiye önemlidir.
>
>

![6]

Merhaba önceki şekil üç güvenlik sınır ağ üst düzey bir görünümünü gösterir. Merhaba hello çevre ağı hello Internet, hello Azure ön uç ve arka uç özel alt ağlar ve hello Azure arka uç alt ağ ve hello şirket içi kurumsal ağ arasında sınırlarıdır.

#### <a name="2-where-are-hello-boundaries-located"></a>2) hello sınırları bulunduğu?
Sınırları Hello sayısı karar sonra burada onları olduğu tooimplement hello sonraki karar noktası. Genellikle üç seçenek vardır:

* Bir Internet tabanlı aracı hizmetini (Bu belgede ele alınan değil, örneğin, bir bulut tabanlı Web uygulaması güvenlik duvarı,) kullanarak
* Azure'da yerel özellikleri ve/veya ağ sanal Gereçleri kullanma
* Fiziksel aygıtların hello şirket içi ağda kullanma

Tamamen Azure ağlarda hello seçenekleri yerel Azure özellikleri (örneğin, Azure yük dengeleyicileri) ya da Azure zengin iş ortağı ekosistemi (örneğin, Check Point güvenlik duvarları) gelen ağ sanal Gereçleri hello.

Bir sınır Azure ile şirket içi ağınız arasında gerekirse hello güvenlik aygıtları hello bağlantısı (veya her iki tarafında da) iki tarafında bulunabilir. Bu nedenle bir karar hello konumu tooplace güvenlik araçları üzerine yapılması gerekir.

Merhaba önceki şekildeki hello Internet çevre ağı ve Merhaba öne için arka uç sınırları tamamen Azure içinde yer alır ve yerel Azure özellikleri ya da ağ sanal Gereçleri olması gerekir. Azure (arka uç alt ağ) arasında sınır güvenlik cihazlarda hello ve hello şirket ağı hello Azure yan üzerinde veya hello şirket içi yan veya iki tarafı da cihazlarda bile bir birleşimi olabilir. Önemli avantajlar ve ciddi düşünülmelidir dezavantajları tooeither seçeneği olabilir.

Örneğin, üzerinde hello mevcut fiziksel güvenlik araçları kullanarak ağ yan yeni bir dişli gereklidir hello avantajı vardır, şirket içi. Yalnızca, yeniden yapılandırılması gerekir. Hello dezavantajı, ancak tüm trafiği hello güvenlik dişli tarafından görülen Azure toohello şirket içi ağ toobe alanından geri gelmesi olur. Böylece Azure Azure trafik önemli gecikme doğurur ve uygulama performansı ve kullanıcı deneyimi etkiler, geri toohello zorlandı, şirket içi güvenlik ilkesi zorlaması için ağ.

#### <a name="3-how-are-hello-boundaries-implemented"></a>3) Merhaba sınırları nasıl uygulanır?
Her güvenlik sınırı, büyük olasılıkla farklı yetenek gereksinimleri (örneğin, Kimlikleri ve güvenlik duvarı kurallarında hello hello çevre ağına, ancak yalnızca hello çevre ağ ve arka uç alt ağ arasında ACL'leri Internet tarafı) vardır. Karar toouse bağlı olarak hangi cihaz (veya cihaz) hello senaryo ve güvenlik gereksinimleri. Bölümden hello örnekler 1, 2 ve 3 kullanılabilecek bazı seçenekler açıklanmaktadır. Hello Azure yerel ağ özellikleri ve hello cihazların Merhaba iş ortağı ekosistemi mevcut gözden geçirerek hello çok seçenekleri kullanılabilir toosolve neredeyse tüm senaryo gösterilmektedir.

Başka bir anahtar uygulama karar nasıl tooconnect hello ağ Azure ile şirket içi noktasıdır. Hello Azure sanal ağ geçidi veya bir ağ sanal gereç kullanmalısınız? Bu seçenekler hello bölümden (örnekler 4, 5 ve 6) içinde daha ayrıntılı ele alınmıştır.

Ayrıca, azure'daki sanal ağlar arasında trafiği gerekli olabilir. Bu senaryolar hello gelecekteki eklenir.

Merhaba yanıtlar toohello önceki sorular öğrendikten sonra hello [Hızlı Başlat](#fast-start) bölümü hangi örnekleri belirli bir senaryo için en uygun tanımlamaya yardımcı olabilir.

## <a name="examples-building-security-boundaries-with-azure-virtual-networks"></a>Örnekler: Azure sanal ağlar ile güvenlik sınırları oluşturma
### <a name="example-1-build-a-perimeter-network-toohelp-protect-applications-with-nsgs"></a>Örnek 1 yapı bir çevre ağ toohelp uygulamaları Nsg'ler ile koruma
[TooFast başlangıç geri](#fast-start) | [ayrıntılı yönergeler için bu örnek oluşturma][Example1]

[![7]][7]

#### <a name="environment-description"></a>Ortam açıklaması
Bu örnekte, kaynakları aşağıdaki hello içeren bir abonelik vardır:

- Tek bir kaynak grubu
- İki alt ağa sahip bir sanal ağ: "Ön uç" ve "Arka uç"
- Uygulanan tooboth alt ağıdır bir ağ güvenlik grubu
- Uygulama web sunucusu ("IIS01") temsil eden bir Windows sunucusu
- Uygulama arka uç sunucuları ("AppVM01", "AppVM02") temsil eden iki Windows sunucuları
- Bir DNS sunucusu ("DNS01") temsil eden bir Windows sunucusu
- Merhaba uygulama web sunucusu ile ilişkili bir ortak IP

Komut dosyaları ve Azure Resource Manager şablonu hello bkz [ayrıntılı yapılandırma yönergeleri][Example1].

#### <a name="nsg-description"></a>NSG açıklaması
Bu örnekte, bir NSG grubu yerleşik ve altı kurallarıyla yüklendi.

> [!TIP]
> Genel olarak bakıldığında, belirli "İzin ver" kurallarınızı ilk olarak, hello daha genel ve ardından oluşturduğunuz "Reddet" kuralları. öncelik verilmiş hello hangi kuralları ilk olarak değerlendirilir belirler. Trafik tooapply tooa belirli kural bulunduktan sonra başka hiçbir kural değerlendirilir. NSG kuralları uygulayabilir ya da (Merhaba alt hello açısından) gelen veya giden yön hello.
>
>

Bildirimli olarak, kurallar aşağıdaki hello gelen trafik için oluşturulmakta:

1. İç DNS trafiğinin (bağlantı noktası 53) izin verilir.
2. Merhaba Internet tooany sanal makine gelen RDP trafiğine (3389 numaralı bağlantı noktası) izin verilir.
3. Merhaba Internet tooweb sunucusundan (IIS01) HTTP trafiği (bağlantı noktası 80) izin verilir.
4. IIS01 tooAppVM1 tüm trafiği (tüm bağlantı noktaları) izin verilir.
5. Merhaba Internet toohello tüm sanal ağ (her iki alt ağ) tüm trafiği (tüm bağlantı noktaları) reddedildi.
6. Merhaba ön uç alt toohello arka uç alt ağından gelen tüm trafiği (tüm bağlantı noktaları) reddedildi.

Bu kurallar ilişkili tooeach alt ağ ile bir HTTP isteği hello Internet toohello web sunucusundan gelen ise her ikisi de kuralları 3 (izin verin) ve 5 (Reddet) geçerli olur. Ancak 3 kuralı daha yüksek öncelikli olduğundan, yalnızca geçerli olur ve kural 5, oyuna gelen değil. Bu nedenle hello HTTP isteği toohello web sunucusu izin. Bu aynı trafiği tooreach hello DNS01 sunucu çalışırken, 5 kural (Reddet) ilk tooapply hello ve hello trafiği izin verilmeyecek toopass toohello sunucusu olacaktır. Kural 6 (bloklar hello toohello arka uç alt (dışında izin verilen trafiği kurallarında 1 ve 4) Konuşmayı gelen ön uç alt reddetme). Merhaba web uygulaması hello ön ucunda bir saldırganın etkilediğinde durumunda bu kural kümesine hello arka uç ağ korur. Merhaba saldırgan erişim toohello arka uç "korumalı" ağ (yalnızca tooresources hello AppVM01 sunucu üzerinde gösterilen) sınırlı.

Toohello Internet giden trafiğe izin veren varsayılan bir giden kuralı yok. Bu örnekte, biz giden trafiğe izin vermek ve herhangi bir giden kuralı değiştirme değil. Her iki yönde trafik aşağı toolock, kullanıcı tanımlı yönlendirme gereklidir (örnek 3 bakın).

#### <a name="conclusion"></a>Sonuç
Bu örnek, hello arka uç alt ağından gelen trafiği yalıtma, nispeten basit ve kolay bir yoludur. Daha fazla bilgi için bkz: Merhaba [ayrıntılı yapılandırma yönergeleri][Example1]. Bu yönergeleri içerir:

* Nasıl toobuild bu çevre ağ Klasik PowerShell komut dosyaları.
* Nasıl toobuild bu çevre ağ bir Azure Resource Manager şablonu ile.
* Her NSG komutu ayrıntılı açıklamaları.
* Nasıl trafiğine izin verilen veya her katmanda reddedildi gösteren, ayrıntılı trafik akışı senaryoları.


### <a name="example-2-build-a-perimeter-network-toohelp-protect-applications-with-a-firewall-and-nsgs"></a>Örnek 2 derleme bir çevre ağ toohelp bir güvenlik duvarı ve Nsg'ler ile uygulamaları koruma
[TooFast başlangıç geri](#fast-start) | [ayrıntılı yönergeler için bu örnek oluşturma][Example2]

[![8]][8]

#### <a name="environment-description"></a>Ortam açıklaması
Bu örnekte, kaynakları aşağıdaki hello içeren bir abonelik vardır:

* Tek bir kaynak grubu
* İki alt ağa sahip bir sanal ağ: "Ön uç" ve "Arka uç"
* Uygulanan tooboth alt ağıdır bir ağ güvenlik grubu
* Güvenlik Duvarı bir bu durumda bir ağ sanal gereç toohello ön uç alt bağlı
* Uygulama web sunucusu ("IIS01") temsil eden bir Windows sunucusu
* Uygulama arka uç sunucuları ("AppVM01", "AppVM02") temsil eden iki Windows sunucuları
* Bir DNS sunucusu ("DNS01") temsil eden bir Windows sunucusu

Komut dosyaları ve Azure Resource Manager şablonu hello bkz [ayrıntılı yapılandırma yönergeleri][Example2].

#### <a name="nsg-description"></a>NSG açıklaması
Bu örnekte, bir NSG grubu yerleşik ve altı kurallarıyla yüklendi.

> [!TIP]
> Genel olarak bakıldığında, belirli "İzin ver" kurallarınızı ilk olarak, hello daha genel ve ardından oluşturduğunuz "Reddet" kuralları. öncelik verilmiş hello hangi kuralları ilk olarak değerlendirilir belirler. Trafik tooapply tooa belirli kural bulunduktan sonra başka hiçbir kural değerlendirilir. NSG kuralları uygulayabilir ya da (Merhaba alt hello açısından) gelen veya giden yön hello.
>
>

Bildirimli olarak, kurallar aşağıdaki hello gelen trafik için oluşturulmakta:

1. İç DNS trafiğinin (bağlantı noktası 53) izin verilir.
2. Merhaba Internet tooany sanal makine gelen RDP trafiğine (3389 numaralı bağlantı noktası) izin verilir.
3. Tüm Internet trafiği (tüm bağlantı noktaları) toohello ağ sanal gereç (Güvenlik Duvarı) izin verilir.
4. IIS01 tooAppVM1 tüm trafiği (tüm bağlantı noktaları) izin verilir.
5. Merhaba Internet toohello tüm sanal ağ (her iki alt ağ) tüm trafiği (tüm bağlantı noktaları) reddedildi.
6. Merhaba ön uç alt toohello arka uç alt ağından gelen tüm trafiği (tüm bağlantı noktaları) reddedildi.

Bu kural bağımlı tooeach alt ağ ile bir HTTP isteği hello Internet toohello Güvenlik Duvarı'ndan, gelen ise her ikisi de kuralları 3 (izin verin) ve 5 (Reddet) geçerli olur. Ancak 3 kuralı daha yüksek öncelikli olduğundan, yalnızca geçerli olur ve kural 5, oyuna gelen değil. Bu nedenle hello HTTP isteği toohello güvenlik duvarı izin. Merhaba ön uç alt ağda olsa bile, aynı trafik tooreach hello IIS01 sunucu çalışıyordu, 5 kural (uygulamak reddetme), ve hello trafiği izin verilmeyecek toopass toohello sunucu. Kural 6 (bloklar hello toohello arka uç alt (dışında izin verilen trafiği kurallarında 1 ve 4) Konuşmayı gelen ön uç alt reddetme). Merhaba web uygulaması hello ön ucunda bir saldırganın etkilediğinde durumunda bu kural kümesine hello arka uç ağ korur. Merhaba saldırgan erişim toohello arka uç "korumalı" ağ (yalnızca tooresources hello AppVM01 sunucu üzerinde gösterilen) sınırlı.

Toohello Internet giden trafiğe izin veren varsayılan bir giden kuralı yok. Bu örnekte, biz giden trafiğe izin vermek ve herhangi bir giden kuralı değiştirme değil. Her iki yönde trafik aşağı toolock, kullanıcı tanımlı yönlendirme gereklidir (örnek 3 bakın).

#### <a name="firewall-rule-description"></a>Güvenlik duvarı kuralı açıklaması
Merhaba güvenlik duvarında kuralları iletme oluşturulmalıdır. Bu örnek yalnızca yollar Internet trafiği de bağlantılı toohello güvenlik duvarı ve ardından toohello web sunucusu, yalnızca bir iletme ağ adresi çevirisi (NAT) bu yana kuralı gereklidir.

Kural iletme hello tooreach HTTP (80 veya 443 HTTPS için bağlantı noktası) çalışırken hello Güvenlik Duvarı'nı isabetler herhangi bir gelen kaynak adresi kabul eder. Merhaba duvarınızın yerel arabirim dışında gönderilen ve toohello web sunucusu hello 10.0.1.5 IP adresi ile yeniden yönlendirilen.

#### <a name="conclusion"></a>Sonuç
Bu örnek, bir güvenlik duvarı ile uygulamanızı koruma ve hello arka uç alt ağından gelen trafiği yalıtma görece basit bir yoludur. Daha fazla bilgi için bkz: Merhaba [ayrıntılı yapılandırma yönergeleri][Example2]. Bu yönergeleri içerir:

* Nasıl toobuild bu çevre ağ Klasik PowerShell komut dosyaları.
* Nasıl toobuild Bu örnek bir Azure Resource Manager şablonu ile.
* Her NSG komutu ve güvenlik duvarı kuralı ayrıntılı açıklamaları.
* Nasıl trafiğine izin verilen veya her katmanda reddedildi gösteren, ayrıntılı trafik akışı senaryoları.

### <a name="example-3-build-a-perimeter-network-toohelp-protect-networks-with-a-firewall-and-udr-and-nsg"></a>Örnek 3 derleme bir çevre ağ toohelp ağ güvenlik duvarı ve UDR ve NSG ile koruma
[TooFast başlangıç geri](#fast-start) | [ayrıntılı yönergeler için bu örnek oluşturma][Example3]

[![9]][9]

#### <a name="environment-description"></a>Ortam açıklaması
Bu örnekte, kaynakları aşağıdaki hello içeren bir abonelik vardır:

* Tek bir kaynak grubu
* Bir sanal ağ üç alt ağ ile: "SecNet", "Ön uç" ve "Arka uç"
* Güvenlik Duvarı bir bu durumda bir ağ sanal gereç toohello SecNet alt bağlı
* Uygulama web sunucusu ("IIS01") temsil eden bir Windows sunucusu
* Uygulama arka uç sunucuları ("AppVM01", "AppVM02") temsil eden iki Windows sunucuları
* Bir DNS sunucusu ("DNS01") temsil eden bir Windows sunucusu

Komut dosyaları ve Azure Resource Manager şablonu hello bkz [ayrıntılı yapılandırma yönergeleri][Example3].

#### <a name="udr-description"></a>UDR açıklaması
Varsayılan olarak, sistem yolları aşağıdaki hello olarak tanımlanır:

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

Merhaba VNETLocal olduğu her zaman, belirli bir ağ için sanal ağ hello oluşturan bir veya daha fazla tanımlanan adres öneklerini (diğer bir deyişle, bu sanal ağ toovirtual ağ her belirli bir sanal ağı nasıl tanımlandığına bağlı olarak değiştirilir). Merhaba kalan sistem yolları statik ve hello tabloda belirtildiği gibi varsayılan.

Bu örnekte, iki yönlendirme tablolarını oluşturulur ve her biri hello ön uç ve arka uç alt ağlar için. Her tablo için alt ağ verilen hello uygun statik yollar ile yüklenir. Bu örnekte, her tabloda tüm trafiği (0.0.0.0/0) doğrudan üç yollar hello güvenlik duvarı üzerinden bulunur (sonraki atlama = sanal Gereci IP adresi):

1. Yerel alt ağ trafiği hiçbir sonraki atlama ile tooallow yerel alt ağ trafiği toobypass hello güvenlik duvarı tanımlanır.
2. Bir sonraki güvenlik duvarı olarak tanımlanan atlama ile sanal ağ trafiği. Bu sonraki atlama doğrudan yerel sanal ağ trafiğini tooroute veren hello varsayılan kuralı geçersiz kılar.
3. Bir sonraki atlama ile tüm kalan trafiği (0/0), güvenlik duvarı hello olarak tanımlanmış.

> [!TIP]
> Merhaba yerel alt girişi hello UDR sonları yerel alt ağ iletişimleri olmaması.
>
> * Bizim örneğimizde, tooVNETLocal işaret eden 10.0.1.0/24 önemlidir! Toohello NVA gönderilecek şekilde bu olmadan hello Web sunucusu (10.0.1.4) hedefleyen tooanother yerel sunucu (örneğin) 10.0.1.25 bırakarak paket başarısız olur. Merhaba NVA toohello alt gönderir ve hello alt toohello NVA sonsuz bir döngüde içinde gönderecektir.
> * bir yönlendirme döngüsü Hello olasılığını Geleneksel, şirket içi cihazları görülür bağlı tooseparate alt ağları birden çok NIC ile cihazları genellikle daha yüksektir.
>
>

Merhaba yönlendirme tablolarını oluşturulduktan sonra bunların ilişkili tootheir alt olması gerekir. ön uç alt ağ yönlendirme tablosunu Merhaba, oluşturulduktan sonra ve toohello alt ağ bağlıysa, bu çıkış gibi görünür:

        Effective routes :
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active

> [!NOTE]
> UDR artık uygulanan toohello ağ geçidi alt ağı hangi hello ExpressRoute bağlantı hattı bağlı olabilir.
>
> Örnek 3 ve 4 nasıl tooenable, çevre ağ ExpressRoute veya siteden siteye ağ örnekleri gösterilmektedir.
>
>

#### <a name="ip-forwarding-description"></a>IP iletimi açıklaması
IP iletimi Yardımcısı özelliği tooUDR olur. IP iletimi tooreceive özellikle trafiği toohello Gereci sağlar ve bu trafiği tooits ultimate hedef iletmek sanal gereç üzerinde bir ayardır.

Örneğin, AppVM01 toohello DNS01 sunucu isteği yaparsa, UDR bu trafiği toohello Güvenlik Duvarı'nı rota. Etkin IP iletimi ile hello trafiği hello DNS01 hedef (10.0.2.4) için hello Gereci (10.0.0.4) tarafından kabul edilir ve tooits ultimate hedef (10.0.2.4) iletilir. Merhaba yol tablosu hello güvenlik duvarı hello sonraki atlama olarak olmasına rağmen hello Güvenlik Duvarı'nı etkin IP iletimi, trafiği hello Gereci tarafından kabul değil. toouse sanal gereç, bu kritik tooremember tooenable IP UDR birlikte iletme olur.

#### <a name="nsg-description"></a>NSG açıklaması
Bu örnekte, bir NSG grubu yerleşik ve tek bir kural ile yüklenir. Bu grup ise yalnızca toohello ön uç ve arka uç alt ağlar (değil SecNet hello) bağlı. Bildirimli olarak kural aşağıdaki hello üretiliyor:

* Hello Internet toohello tüm sanal ağ (tüm alt ağlar) gelen tüm trafik (tüm bağlantı noktaları) reddedildi.

Nsg'ler Bu örnekte kullanılan ana amacı el ile yetersizliğini karşı savunma ikincil bir katmanı olarak olsa da. Merhaba tooblock gelen tüm gelen trafiği hedeftir hello Internet tooeither hello ön uç veya arka uç alt ağ. Trafik hello SecNet alt toohello güvenlik duvarı üzerinden yalnızca akış (ve daha sonra uygunsa, alt ağlardaki toohello ön uç veya arka uç). Ayrıca, bir yerde, hello UDR kurallarla ön uç veya arka uç alt hello yaptı tüm trafik toohello Güvenlik Duvarı (teşekkürler tooUDR) yönlendirilmesi. Merhaba Güvenlik Duvarı'nı bu trafiği asimetrik bir akış halinde görür ve hello giden trafiği bırakma. Bu nedenle hello alt ağ korumaya güvenlik üç katmanı vardır:

* Herhangi bir ön uç veya arka uç NIC'ler üzerinde hiçbir ortak IP adresleri.
* Nsg'ler hello Internet trafiği engelleme.
* Merhaba güvenlik duvarı bırakma asimetrik trafiği.

Bu örnekte hello NSG ile ilgili bir ilginç noktası hello güvenlik alt ağ dahil olmak üzere toodeny Internet trafiği toohello tüm sanal ağ, yalnızca bir kural içermesidir. Ancak, NSG Only'dir hello bağlı toohello ön uç ve arka uç alt ağlar, hello kural trafiğinde işlenen değil toohello güvenlik alt ağ gelen. Sonuç olarak, trafiği toohello güvenlik alt ağ akar.

#### <a name="firewall-rules"></a>Güvenlik duvarı kuralları
Merhaba güvenlik duvarında kuralları iletme oluşturulmalıdır. Merhaba güvenlik duvarı engelleme veya iletme tüm gelen, giden ve içi sanal ağ trafiğini olduğundan, birçok güvenlik duvarı kuralları gerekir. Ayrıca, tüm gelen trafiği hello güvenlik hizmeti genel IP adresi isabetler (farklı bağlantı noktalarını), toobe hello güvenlik duvarı tarafından işlenir. Toodiagram hello mantıksal akış hello alt ayarlamadan önce en iyi uygulamadır ve güvenlik duvarı kuralları, tooavoid daha sonra rework. Hello aşağıdaki şekilde hello güvenlik duvarı kuralları bu örnek için mantıksal bir görünümünü gösterilmiştir:

![10]

> [!NOTE]
> Ağ sanal gereç kullanılan hello üzerinde bağlı olarak, hello yönetim bağlantı noktalarını farklılık gösterir. Bu örnekte, bağlantı noktası 22, 801 ve 807 kullanan bir Barracuda NextGen Firewall başvuruluyor. Kullanılan hello aygıt yönetimi için kullanılan hello Gereci satıcı belgelerine toofind hello tam bağlantı noktalarını başvurun.
>
>

#### <a name="firewall-rules-description"></a>Güvenlik duvarı kuralları açıklaması
Merhaba güvenlik duvarı hello yalnızca kaynak o alt ağdaki olduğundan mantıksal diyagramı önceki hello hello güvenlik alt ağ gösterilmez. Merhaba diyagramı hello güvenlik duvarı kuralları ve nasıl mantıksal olarak izin ver veya Reddet trafiği akışı, hello gerçek yönlendirilmiş yol değil gösteriyor. Ayrıca, daha kolay okunabilir olması için yerel IP adresi hello iki sekizlisinin hello RDP trafiğine yüksek aralıklı bağlantı noktaları (8014 – 8026) olduğundan ve bundan seçili tooloosely Hizala ile hello için seçilen hello dış bağlantı noktalarını en son (örneğin, yerel sunucu adresi 10.0.1.4 ilişkili. dış bağlantı noktası ile 8014). Ancak, tüm yüksek çakışmayan bağlantı noktaları, kullanılabilir.

Bu örnekte, yedi tür kuralların gerekir:

* Dış kuralları (için gelen trafiği):
  1. Güvenlik Duvarı Yönetimi kuralı: Bu uygulama yeniden yönlendirme kuralı trafiği toopass hello ağ sanal gereç toohello yönetim bağlantı noktaları sağlar.
  2. RDP kuralları (her Windows server için): Bu dört kuralları (her sunucu için bir tane) hello Yönetimi tek tek sunucular RDP aracılığıyla izin verir. Merhaba dört RDP kuralları hello ağ sanal gereç kullanılan hello yeteneklerini bağlı olarak bir kural içine de daraltılmış.
  3. Uygulama trafiği kuralları: Bu kurallar, hello hello ön uç web trafiği için ilk ve ikinci hello arka uç trafiği (örneğin, web sunucusu toodata katmanı) için hello iki vardır. Bu kurallar Hello yapılandırmasını hello ağ mimarisi (sunucularınızı yerleştirildiği) ve (hangi yönde hello trafik akışlarının ve hangi bağlantı noktalarının kullanılacağını) trafiği akışı bağlıdır.
     * Merhaba ilk kural hello gerçek uygulama trafiği tooreach hello uygulama sunucusu sağlar. Merhaba diğer kuralları güvenlik ve Yönetim için izin verirken, uygulama trafiği ne hello uygulamaları dış kullanıcı ve hizmet tooaccess izin kurallardır. Bu örnekte, bağlantı noktası 80 üzerinde tek bir web sunucusu yok. Bu nedenle bir tek uygulama güvenlik duvarını gelen trafiği toohello dış IP, toohello web sunucuları iç IP adresi yeniden yönlendirir. Merhaba yeniden yönlendirilen trafiği oturum NAT toohello iç sunucu çevrilmesi.
     * Merhaba ikinci hello arka uç kural tooallow hello web server tootalk toohello AppVM01 sunucusu (ancak AppVM02 değil) herhangi bir bağlantı kuralıdır.
* İç kurallardan (içi sanal ağ trafiği)
  1. Giden tooInternet kuralı: Bu kural herhangi bir ağ trafiğinden toopass seçili toohello ağlar sağlar. Bu genellikle varsayılan bir kural zaten hello güvenlik duvarı, ancak devre dışı durumdayken kuralıdır. Bu kural, bu örnek için etkinleştirilmelidir.
  2. DNS kuralı: Bu kural yalnızca DNS (bağlantı noktası 53) trafiği toopass toohello DNS sunucusunun izin verir. Bu ortam için hello ön uç toohello arka uçtan çoğu trafiği engellenir. Bu kural, tüm yerel alt ağ üzerinden DNS özellikle sağlar.
  3. Alt ağ toosubnet kuralı: Bu kural tooallow sunucuda hello arka uç alt tooconnect tooany hello ön uç alt ağ (ancak değil ters hello) herhangi bir sunucudur.
* Yedek operatördür kuralı (Merhaba önceki birini karşılamıyor trafiği):
  1. Reddetme tüm trafik kuralı: Bu reddetme kuralı her zaman son bir kural hello (bakımından öncelik) olmalıdır ve bu nedenle bir trafik akışı toomatch kuralları önceki hello hiçbirini başarısız olursa bu kural tarafından yoksayılır. Bu kural varsayılan kuralıdır ve genellikle yerinde ve etkin. Hiçbir değişikliğe genellikle gerekli toothis kuralı var.

> [!TIP]
> Merhaba üzerinde ikinci uygulama trafik kuralı, toosimplify Bu örnekte, tüm bağlantı izin verilir. Gerçek bir senaryoda, bu kural, kullanılan tooreduce hello saldırı yüzeyini hello en belirli bağlantı noktasının ve adres aralıkları olmalıdır.
>
>

Merhaba önceki kural oluşturulduktan sonra tooreview hello her kural tooensure trafiğin önceliğini izin verilen ya da istediğiniz gibi reddedildi önemlidir. Bu örnekte, hello öncelik sırasına göre kurallardır.

#### <a name="conclusion"></a>Sonuç
Daha karmaşık ancak bu örnekte, koruma ve daha önceki örneklerde hello hello ağ yalıtma şekilde tamamlayın. (Yalnızca Merhaba uygulaması örnek 2 korur ve örnek 1 yalnızca alt ağlar yalıtır). Bu tasarım her iki yönde trafik izlenmesini sağlar ve yalnızca hello gelen uygulama sunucusu korur ancak bu ağdaki tüm sunucular için ağ güvenlik ilkeleri uygular. Ayrıca, tam trafiği denetim ve tanıma kullanılan hello Gereci bağlı olarak sağlanabilir. Daha fazla bilgi için bkz: Merhaba [ayrıntılı yapılandırma yönergeleri][Example3]. Bu yönergeleri içerir:

* Nasıl toobuild Bu örnek çevre ağ Klasik PowerShell komut dosyaları.
* Nasıl toobuild Bu örnek bir Azure Resource Manager şablonu ile.
* Ayrıntılı her UDR NSG açıklamalarını komut ve güvenlik duvarı kuralı.
* Nasıl trafiğine izin verilen veya her katmanda reddedildi gösteren, ayrıntılı trafik akışı senaryoları.

### <a name="example-4-add-a-hybrid-connection-with-a-site-to-site-virtual-appliance-vpn"></a>Siteden siteye, sanal bir Gereci VPN ile karma bağlantı örnek 4 ekleme
[TooFast başlangıç geri](#fast-start) | Ayrıntılı yapılandırma yönergeleri kullanılabilir yakında

[![11]][11]

#### <a name="environment-description"></a>Ortam açıklaması
Bir ağ sanal gereç (NVA) kullanarak karma ağ 1, 2 veya 3 örneklerde açıklanan hello çevre ağ türlerinin tooany eklenebilir.

Merhaba önceki çizimde gösterildiği gibi hello Internet (siteden siteye) bir VPN bağlantısı kullanılan tooconnect bir şirket içi ağ tooan bir NVA aracılığıyla Azure sanal ağı olur.

> [!NOTE]
> ExpressRoute hello Azure ortak eşleme seçeneği etkinken kullanırsanız, statik yol oluşturulmalıdır. Bu statik yol toohello NVA VPN IP adresi, Kurumsal Internet ve hello ExpressRoute bağlantısı aracılığıyla değil rota. Merhaba ExpressRoute Azure ortak eşleme seçeneği hello üzerinde gerekli NAT hello VPN oturumu bozulabilir.
>
>

VPN, bulunduğundan hello hello sonra NVA tüm ağları ve alt ağlar için merkezi hub hello hale gelir. Merhaba güvenlik duvarı iletme kurallarını hangi trafik akışları izin verilir, NAT çevrilir, yönlendirilir veya (için bile hello şirket içi ağınız ve Azure arasında trafik akışına) bırakılan belirleyin.

İyileştirilebilir veya bu tasarım deseni tarafından düşürülmüş hello bağlı olarak belirli kullanım örneğini gibi trafik akışına dikkatlice değerlendirilmelidir.

Örnek 3 yerleşik hello ortamı kullanarak ve siteden siteye VPN karma ağ bağlantısı ekleme tasarım aşağıdaki hello üretir:

[![12]][12]

Merhaba şirket içi yönlendirici veya VPN için NVA ile uyumlu herhangi bir ağ aygıtı hello VPN istemcisi olacaktır. Bu fiziksel aygıt başlatma ve hello VPN bağlantısı, NVA birlikte bulundurma sorumlu olacaktır.

Mantıksal olarak toohello NVA, hello ağ dört ayrı hello kurallarla "güvenlik bölgeleri" Merhaba NVA olan benzer hello birincil director Bu bölgeler arasında trafiği:

![13]

#### <a name="conclusion"></a>Sonuç
bir siteden siteye VPN karma ağ bağlantısı tooan Azure sanal ağı Hello eklenmesi hello şirket içi ağ Azure'da güvenli bir şekilde genişletebilirsiniz. Bir VPN bağlantısı kullanarak, trafiğinizin şifrelenir ve yönlendiren hello Internet üzerinden. Merhaba NVA Bu örnekte, bir merkezi konumda tooenforce sağlar ve hello güvenlik ilkesi yönetin. Daha fazla bilgi için bkz: ayrıntılı hello yönergeleri (yeni çıkacak) oluşturun. Bu yönergeleri içerir:

* Nasıl toobuild Bu örnek çevre ağ PowerShell komut dosyaları.
* Nasıl toobuild Bu örnek bir Azure Resource Manager şablonu ile.
* Bu tasarım trafiğinin nasıl akacağını gösteren, ayrıntılı trafik akışı senaryoları.

### <a name="example-5-add-a-hybrid-connection-with-a-site-to-site-azure-vpn-gateway"></a>Örnek 5 bir siteden siteye Azure VPN ağ geçidi ile karma bağlantı ekleyin
[TooFast başlangıç geri](#fast-start) | Ayrıntılı yapılandırma yönergeleri kullanılabilir yakında

[![14]][14]

#### <a name="environment-description"></a>Ortam açıklaması
Bir Azure VPN ağ geçidi kullanarak karma ağ 1 veya 2 örneklerde açıklanan tooeither çevre ağ türü eklenebilir.

Şekil önceki hello gösterildiği gibi hello Internet (siteden siteye) bir VPN bağlantısı kullanılan tooconnect bir şirket içi ağ tooan Azure VPN ağ geçidi aracılığıyla Azure sanal ağı olur.

> [!NOTE]
> ExpressRoute hello Azure ortak eşleme seçeneği etkinken kullanırsanız, statik yol oluşturulmalıdır. Bu statik yol toohello NVA VPN IP adresi, Kurumsal Internet ve hello ExpressRoute WAN üzerinden değil rota. Merhaba ExpressRoute Azure ortak eşleme seçeneği hello üzerinde gerekli NAT hello VPN oturumu bozulabilir.
>
>

Merhaba aşağıdaki şekilde hello iki ağ kenarları Bu örnekte gösterilmiştir. Merhaba ilk kenar NVA hello ve Nsg'ler trafik akışına içi Azure ağları ile Azure arasında denetlemek ve Internet hello. Merhaba ikinci kenar ayrı ve yalıtılmış ağ ucunun şirket içi ve Azure arasında hello Azure VPN ağ geçididir.

İyileştirilebilir veya bu tasarım deseni tarafından düşürülmüş hello bağlı olarak belirli kullanım örneğini gibi trafik akışına dikkatlice değerlendirilmelidir.

Örnek 1 yerleşik hello ortamı kullanarak ve siteden siteye VPN karma ağ bağlantısı ekleme tasarım aşağıdaki hello üretir:

[![15]][15]

#### <a name="conclusion"></a>Sonuç
bir siteden siteye VPN karma ağ bağlantısı tooan Azure sanal ağı Hello eklenmesi hello şirket içi ağ Azure'da güvenli bir şekilde genişletebilirsiniz. Merhaba yerel Azure VPN ağ geçidi kullanarak trafiğinizi şifrelenmiş IPSec ve hello Internet yönlendirir. Ayrıca, hello Azure VPN ağ geçidi kullanarak (hiçbir ek gibi üçüncü taraf NVAs ile maliyet Lisansı) daha düşük maliyetli seçeneği sağlayabilirsiniz. Bu seçenek, hiçbir NVA kullanıldığı örnek 1, en ekonomik olur. Daha fazla bilgi için bkz: ayrıntılı hello yönergeleri (yeni çıkacak) oluşturun. Bu yönergeleri içerir:

* Nasıl toobuild Bu örnek çevre ağ PowerShell komut dosyaları.
* Nasıl toobuild Bu örnek bir Azure Resource Manager şablonu ile.
* Bu tasarım trafiğinin nasıl akacağını gösteren, ayrıntılı trafik akışı senaryoları.

### <a name="example-6-add-a-hybrid-connection-with-expressroute"></a>ExpressRoute ile karma bağlantı örnek 6 ekleme
[TooFast başlangıç geri](#fast-start) | Ayrıntılı yapılandırma yönergeleri kullanılabilir yakında

[![16]][16]

#### <a name="environment-description"></a>Ortam açıklaması
Özel eşleme bağlantısında olabilir bir ExpressRoute kullanarak karma ağ 1 veya 2 örneklerde açıklanan tooeither çevre ağ türü eklendi.

Şekil önceki hello gösterildiği gibi ExpressRoute özel eşleme hello Azure sanal ağı ve şirket içi ağınızı arasında doğrudan bir bağlantı sağlar. Yalnızca hello hizmet sağlayıcısı ağ ve hiçbir zaman hello Internet temas hello Microsoft Azure ağ trafiği transits.

> [!TIP]
> ExpressRoute kullanarak kurumsal ağ trafiğini Internet hello tutar. Ayrıca hizmet düzeyi sözleşmeleri için ExpressRoute sağlayıcınızdan sağlar. siteden siteye VPN ile 200 MB/sn hello Azure ağ geçidi en yüksek verimlilik iken hello Azure ağ geçidi ExpressRoute ile too10 Gbps yukarı geçirebilirsiniz.
>
>

Hello Aşağıdaki diyagramda görüldüğü gibi bu seçenek hello ile ortamı iki ağ kenarları artık sahiptir. Merhaba NVA ve NSG denetim trafik akışı içi Azure ağları için ve Azure ile Merhaba hello ağ geçidi şirket içi ve Azure arasında ayrı ve yalıtılmış ağ kenar olsa da Internet arasında.

İyileştirilebilir veya bu tasarım deseni tarafından düşürülmüş hello bağlı olarak belirli kullanım örneğini gibi trafik akışına dikkatlice değerlendirilmelidir.

Örnek 1 yerleşik hello ortamı kullanarak ve ardından bir ExpressRoute karma ağ bağlantısı ekleyerek tasarım aşağıdaki hello üretir:

[![17]][17]

#### <a name="conclusion"></a>Sonuç
bir ExpressRoute özel eşleme ağ bağlantısı Hello eklenmesi, daha yüksek bir şekilde gerçekleştirme bir güvenli, daha düşük gecikme, Azure'da hello şirket içi ağ genişletebilirsiniz. Ayrıca, hello kullanarak yerel Azure ağ geçidi, bu örnekte olduğu gibi daha düşük maliyetli seçeneği (üçüncü taraf NVAs gibi ile lisans Hayır ek) sağlar. Daha fazla bilgi için bkz: ayrıntılı hello yönergeleri (yeni çıkacak) oluşturun. Bu yönergeleri içerir:

* Nasıl toobuild Bu örnek çevre ağ PowerShell komut dosyaları.
* Nasıl toobuild Bu örnek bir Azure Resource Manager şablonu ile.
* Bu tasarım trafiğinin nasıl akacağını gösteren, ayrıntılı trafik akışı senaryoları.

## <a name="references"></a>Başvurular
### <a name="helpful-websites-and-documentation"></a>Yararlı Web siteleri ve belgeler
* Erişim Azure Azure Resource Manager ile:
* Azure PowerShell ile erişme: [https://docs.microsoft.com/powershell/azureps-cmdlets-docs/](/powershell/azure/overview)
* Sanal ağ belgeleri: [https://docs.microsoft.com/azure/virtual-network/](https://docs.microsoft.com/azure/virtual-network/)
* Ağ güvenlik grubu belgelerine: [https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg](virtual-network/virtual-networks-nsg.md)
* Kullanıcı tanımlı yönlendirme belgelerine: [https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview](virtual-network/virtual-networks-udr-overview.md)
* Azure sanal ağ geçitleri: [https://docs.microsoft.com/azure/vpn-gateway/](https://docs.microsoft.com/azure/vpn-gateway/)
* Siteden siteye VPN: [https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell](vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* ExpressRoute belgeleri (olması hello "Başlarken" ve "Nasıl yapılır" bölümlerine çıkışı emin toocheck): [https://docs.microsoft.com/azure/expressroute/](https://docs.microsoft.com/azure/expressroute/)

<!--Image References-->
[0]: ./media/best-practices-network-security/flowchart.png "Güvenlik seçenekleri akış çizelgesi"
[2]: ./media/best-practices-network-security/azuresecurityfeatures.png "azure güvenlik özellikleri"
[3]: ./media/best-practices-network-security/dmzcorporate.png "bir şirket ağında bir DMZ"
[4]: ./media/best-practices-network-security/azuresecurityarchitecture.png "azure güvenlik mimarisi"
[5]: ./media/best-practices-network-security/dmzazure.png "bir Azure sanal ağında DMZ"
[6]: ./media/best-practices-network-security/dmzhybrid.png "üç güvenlik sınırlarla karma ağ"
[7]: ./media/best-practices-network-security/example1design.png "NSG ile giriş DMZ"
[8]: ./media/best-practices-network-security/example2design.png "NVA ve NSG gelen DMZ"
[9]: ./media/best-practices-network-security/example3design.png "Çift yönlü DMZ NVA, NSG ve UDR"
[10]: ./media/best-practices-network-security/example3firewalllogical.png "mantıksal görünümünü hello güvenlik duvarı kuralları"
[11]: ./media/best-practices-network-security/example3designoptions.png "Karma ağ DMZ NVA ile bağlı"
[12]: ./media/best-practices-network-security/example4designs2s.png "Siteden siteye VPN kullanarak bağlanan NVA ile DMZ"
[13]: ./media/best-practices-network-security/example4networklogical.png "NVA açısından mantıksal ağ"
[14]: ./media/best-practices-network-security/example5designoptions.png "DMZ Azure ağ geçidi ile siteden siteye karma ağa bağlı"
[15]: ./media/best-practices-network-security/example5designs2s.png "Siteden siteye VPN kullanarak Azure ağ geçidi ile DMZ"
[16]: ./media/best-practices-network-security/example6designoptions.png "ExpressRoute karma ağ DMZ Azure ağ geçidi ile bağlı"
[17]: ./media/best-practices-network-security/example6designexpressroute.png "Bir ExpressRoute bağlantı kullanarak Azure ağ geçidi ile DMZ"

<!--Link References-->
[TrustCenter]: https://azure.microsoft.com/support/trust-center/compliance/
[Example1]: ./virtual-network/virtual-networks-dmz-nsg.md
[Example2]: ./virtual-network/virtual-networks-dmz-nsg-fw-asm.md
[Example3]: ./virtual-network/virtual-networks-dmz-nsg-fw-udr-asm.md
[Example4]: ./virtual-network/virtual-networks-hybrid-s2s-nva-asm.md
[Example5]: ./virtual-network/virtual-networks-hybrid-s2s-agw-asm.md
[Example6]: ./virtual-network/virtual-networks-hybrid-expressroute-asm.md
[Example7]: ./virtual-network/virtual-networks-vnet2vnet-direct-asm.md
[Example8]: ./virtual-network/virtual-networks-vnet2vnet-transit-asm.md
