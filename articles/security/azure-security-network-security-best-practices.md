---
title: "en iyi güvenlik uygulamaları, ağ aaaAzure | Microsoft Docs"
description: "Bu makalede Azure özellikleri yerleşik güvenlik ağ kullanmaya yönelik en iyi yöntemler kümesi sağlar."
services: security
documentationcenter: na
author: TomShinder
manager: swadhwa
editor: TomShinder
ms.assetid: 7f6aa45f-138f-4fde-a611-aaf7e8fe56d1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/09/2017
ms.author: TomSh
ms.openlocfilehash: 5867dea358b4da65c65b3e52fcab7e687e981642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-security-best-practices"></a>Azure ağı en iyi güvenlik uygulamaları
Microsoft Azure Azure sanal ağlarda koyarak tooconnect sanal makineler ve cihazları ağa tooother aygıtları sağlar. Bir Azure sanal ağı tooconnect sanal ağ arabirimi kartları tooa sanal ağ tooallow TCP tabanlı iletişimleri etkin ağ aygıtları arasındaki sağlayan bir sanal ağ yapıdır. Azure sanal makineleri bağlı tooan Azure sanal ağ olan mümkün tooconnect toodevices aynı Azure sanal ağ, hello Internet üzerinde farklı Azure sanal ağlar hello ve hatta kendi şirket içi ağlarda.

Bu makalede en iyi güvenlik uygulamaları, Azure ağ koleksiyonu aşağıdakiler ele alınacaktır. Bu en iyi uygulamaları Azure ağ ile deneyimi bizim türetilmiş ve müşterilerin hello deneyimleri bulunun.

En iyi her uygulama için açıklayacağız:

* Hangi hello en iyi uygulamadır
* Neden bu en iyi uygulama tooenable istiyor
* Tooenable hello en iyi yöntem başarısız olursa ne hello sonucu olabilir
* Olası alternatifler toohello en iyi uygulama
* Tooenable hello en iyi yöntem nasıl öğrenin

Bu makalenin yazıldığı hello zamanında oldukları gibi bu Azure ağ güvenlik en iyi yöntemler makalesi anlaşma fikir ve Azure platformu özellikleri ve özellik kümeleri dayanır. Bu makalede olacaktır ve görüşlerini ve teknolojileri değiştirmek zaman içinde bu değişiklikleri düzenli olarak tooreflect üzerinde güncelleştirildi.

Bu makalede ele alınan azure ağ en iyi yöntemler şunlardır:

* Mantıksal kesim alt ağlar
* Yönlendirme davranışını denetlemek
* Zorlanan tünel etkinleştir
* Sanal ağ cihazları kullanın
* Güvenlik bölgesi için DMZ'ler dağıtma
* Ayrılmış WAN bağlantılarıyla Etkilenme toohello Internet kaçının
* Açık kalma süresi ve performansı en iyi duruma getirme
* Genel Yük Dengelemesi
* RDP erişimini tooAzure sanal makineleri devre dışı bırak
* Etkinleştirme Azure Güvenlik Merkezi
* Veri merkeziniz Azure genişletme

## <a name="logically-segment-subnets"></a>Mantıksal kesim alt ağlar
[Azure sanal ağlar](https://azure.microsoft.com/documentation/services/virtual-network/) , şirket içi ağınızda benzer tooa LAN şunlardır. Merhaba bir Azure sanal ağı arkasında üzerinde yerleştirebileceğiniz tüm tek bir özel IP adresi alanı tabanlı ağı oluşturma olur, [Azure sanal makineleri](https://azure.microsoft.com/services/virtual-machines/). Merhaba özel IP adres alanlarından kullanılabilir hello sınıf A (10.0.0.0/8), sınıf B (172.16.0.0/12) ve C sınıfı (192.168.0.0/16) aralıktır.

Benzer toowhat, şirket içi, toosegment hello büyük adres alanı alt isteyeceksiniz. Kullanabileceğiniz [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing) ağlarınızı ilkeleri toocreate alt ağ oluşturma tabanlı.

Alt ağlar arasında yönlendirme gerçekleşir otomatik olarak ve ihtiyacınız olmayan toomanually yönlendirme tablolarını yapılandırın. Ancak, hello varsayılan olduğunu hiçbir ağ erişim denetimleri hello Azure sanal ağ üzerinde oluşturduğunuz hello alt ağlar arasında ayardır. Alt ağlar arasında sipariş toocreate ağ erişim denetimleri içinde tooput hello alt ağlar arasında bir şey gerekir.

Bu görev tooaccomplish hello özelliklerinden biri kullanabileceğiniz bir [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md) (NSG). Nsg'ler olan basit durum bilgisi olan paket incelemesi hello 5-tanımlama grubu (Merhaba kaynak IP, kaynak bağlantı noktası, hedef IP, hedef bağlantı noktası ve katman 4 Protokolü) kullanan cihazları yaklaşımını toocreate izin verme/reddetme kurallarını ağ trafiği için. İzin verebilir veya tek IP adresi, birden çok IP adreslerinden tooand veya hatta tooand tüm alt ağlar gelen trafiği tooand reddet.

Nsg'ler alt ağlar arasında ağ erişim denetimi toohello ait tooput kaynakları sağlar kullanarak aynı güvenlik bölgesi ya da kendi alt rolü. Örneğin bir web katmanı, bir uygulama mantığı katmanından ve veritabanı katmanından olan bir basit bir 3 katmanlı uygulama düşünün. Bu katmanların tooeach kendi alt ait sanal makineler yerleştirin. Ardından hello alt ağlar arasında Nsg'ler toocontrol trafiğinin kullanın:

* Web Katmanı sanal makineler yalnızca bağlantıları toohello uygulama mantığını makineleri başlatabilir ve yalnızca hello Internet bağlantılarını kabul edebilir
* Uygulama mantığı sanal makineler yalnızca veritabanı katmanı ile bağlantılar başlatabilir ve yalnızca hello web katmanı gelen bağlantıları kabul edebilir
* Veritabanı katmanı sanal makineleri, kendi alt ağı dışında herhangi bir şeyle bağlantı başlatılamıyor ve yalnızca hello uygulama mantığı katmanı gelen bağlantıları kabul edebilir

Ağ güvenlik grupları ve nasıl toologically segment kullanabilmek için hakkında daha fazla toolearn, Azure sanal ağlar hello makalesini okuyun [bir ağ güvenlik grubu nedir](../virtual-network/virtual-networks-nsg.md) (NSG).

## <a name="control-routing-behavior"></a>Yönlendirme davranışını denetlemek
Bir Azure sanal ağ üzerinde bir sanal makine geçirdiğinizde, hello sanal makinenin diğer sanal makine tooany bağlanabilir fark edeceksiniz üzerinde hello diğer sanal makineler farklı alt ağlarda olsa bile aynı Azure sanal ağ, hello. neden bu mümkündür hello neden bu tür iletişim izin varsayılan olarak etkin olan sistem yolları koleksiyonunu olmasıdır. Bu varsayılan yollar aynı Azure sanal ağ tooinitiate bağlantıları birbirleriyle ve Merhaba Internet (giden iletişimler toohello Internet yalnızca) ile Merhaba sanal makinelerde izin verin.

Merhaba varsayılan sistem yolları birçok dağıtım senaryoları için faydalı olsa da, dağıtımlarınızda toocustomize hello yönlendirme yapılandırması istediğinizde zamanlar vardır. Bu özelleştirmeler, tooconfigure hello sonraki atlama adresi tooreach belirli hedeflere izin verir.

Biz hakkında sonraki en iyi uygulama konuşun bir sanal ağ güvenlik Gereci dağıttığınızda kullanıcı tanımlı yollar yapılandırmanızı öneririz.

> [!NOTE]
> Kullanıcı tanımlı yollar gerekli değildir ve çoğu durumda hello varsayılan sistem yolları çalışır.
>
>

Kullanıcı tanımlı yollar hakkında daha fazla bilgi edinmek ve nasıl tooconfigure hello makale okuyarak bunları [kullanıcı tanımlı yollar ve IP iletimi nedir](../virtual-network/virtual-networks-udr-overview.md).

## <a name="enable-forced-tunneling"></a>Zorlanan tünel etkinleştir
toobetter anlamak zorlamalı tünel, hangi "bölünmüş tünel" olduğundan yararlı toounderstand.
Bölünmüş tünel hello en yaygın örnek VPN bağlantıları ile görülür. Otel odası tooyour Kurumsal ağınızdan VPN bağlantısı kuracak düşünün. Bu bağlantı, tooconnect tooresources şirket ağınızda tanır ve şirket ağınızdaki tüm iletişimler tooresources hello VPN tüneli gidin.

Merhaba Internet üzerinde tooconnect tooresources istediğiniz ne olur? Bölünmüş tünel etkinleştirildiğinde, bu bağlantılar doğrudan toohello Internet gidin ve hello değil VPN tünel. Bazı güvenlik Uzmanları bu toobe potansiyel bir risk düşünün ve bu nedenle bölünmüş tüneli devre dışı bırakılmasını önerilir ve tüm bağlantılar, Merhaba Internet hedefleyen ve şirket kaynakları için hedefleyen hello VPN tüneli gidin. Bunun yapılması hello avantajı Internet sonra toohello Internet hello VPN tüneli dışında hello VPN istemcisi bağlıysa, hello durumda olmayacaktır hello şirket ağı güvenlik aygıtları üzerinden zorla Bu bağlantıları toohello olmasıdır.

Şimdi şimdi bu Getir bir Azure sanal ağında toovirtual makineleri yedekleyin. Merhaba varsayılan yollar bir Azure sanal ağı için sanal makineleri tooinitiate trafiği toohello Internet izin verir. Bu giden bağlantılar bir sanal makine hello saldırı yüzeyini artırabilir ve saldırganlar tarafından işlevden bu bir güvenlik riski çok temsil edebilir.
Bu nedenle, şirket içi ağınızı Azure sanal ağınız arasında şirketler arası bağlantı varsa, sanal makinelere zorlamalı tünel etkinleştirmenizi öneririz. Biz hakkında bağlantı daha sonra bu belgede Azure ağ en iyi yöntemler çapraz konuşur.

Bir şirket içi ve dışı bağlantı yoksa, avantajından ağ güvenlik grupları (daha önce bahsedilen) veya Azure emin olun. sanal ağ güvenlik Gereçleri (ele yanında) tooprevent giden bağlantılar toohello, Azure sanal Internet'ten Makineler.

hakkında daha fazla bilgi toolearn zorlamalı tünel ve nasıl tooenable, hello makalesini okuyun [yapılandırma PowerShell ve Azure Resource Manager kullanarak zorlamalı tüneli](../vpn-gateway/vpn-gateway-forced-tunneling-rm.md).

## <a name="use-virtual-network-appliances"></a>Sanal ağ cihazları kullanın
Ağ güvenlik grupları ve kullanıcı tanımlı yönlendirme ağ güvenlik hello en belirli bir ölçü hello ağ ve Aktarım katmanı sağlayabilir sırada [OSI modeli](https://en.wikipedia.org/wiki/OSI_model), buradan istediğiniz veya tooenable gerek toobe durumlarda gitmeden olan Güvenlik, yüksek düzeyde hello yığınının. Böyle durumlarda, Azure iş ortakları tarafından sağlanan sanal ağ güvenlik Gereçleri dağıtmanızı öneririz.

Azure ağı güvenlik Gereçleri önemli ölçüde gelişmiş düzeyde güvenlik, ağ düzeyinde denetimler tarafından sağlanan üzerinden sunabilir. Sanal ağ güvenlik Gereçleri tarafından sağlanan hello ağ güvenlik özellikleri bazıları şunlardır:

* Saldırısından
* Yetkisiz erişim algılama/izinsiz giriş önleme
* Güvenlik Açığı Yönetimi
* Uygulama denetimi
* Ağ tabanlı anomali algılama
* Web filtreleme
* Virüsten koruma
* Botnet koruma

Ağ düzeyinde erişim denetimleriyle edinebilirsiniz olandan daha yüksek düzeyde ağ güvenlik gerektiriyorsa, ardından araştırın ve Azure sanal ağı güvenlik Gereçleri dağıtmak öneririz.

toolearn kendi yeteneklerini ve hangi Azure sanal ağı güvenlik Gereçleri kullanılabilir hakkında lütfen şu adresi ziyaret hello [Azure Marketi](https://azure.microsoft.com/marketplace/) ve "güvenlik" ve "ağ güvenliği" arayın.

## <a name="deploy-dmzs-for-security-zoning"></a>Güvenlik bölgesi için DMZ'ler dağıtma
DMZ "çevre ağı" olan bir fiziksel veya olduğundan mantıksal ağ kesimine tasarlanmış tooprovide ek bir varlıklar hello Internet arasındaki güvenlik katmanı. Merhaba DMZ Hello amacı, böylece hello ağ güvenlik aygıtı geçmiş ve Azure sanal ağınızda yalnızca istenen trafiğe izin tooplace ağ erişim denetimi aygıtları hello DMZ ağ hello kenarında özelleştirilmiş ' dir.

Ağ erişim denetimi Yönetimi izleme, günlüğe kaydetme ve Azure sanal ağınızda hello sınırında hello cihazlarda rapor odaklanabilirsiniz sağladığından DMZ'ler kullanışlıdır. Burada genellikle DDoS önleme, izinsiz giriş algılama/izinsiz giriş önleme sistemleri (Kimlikleri/IP), güvenlik duvarı kuralları ve ilkeleri, web filtreleme, ağ kötü amaçlı yazılımdan koruma ve daha fazlasını etkinleştirmeniz. Merhaba ağ güvenlik cihazlar hello Internet ve Azure sanal ağınız arasında yaslanın ve her iki ağda bir arabirim.

Merhaba temel DMZ tasarımını ederken vardır birçok farklı DMZ tasarımı, aşağıdaki gibi uçtan uca, üç konaklı, çok konaklı ve diğerleri.

Azure kaynaklarınız için ağ güvenlik DMZ tooenhance hello düzeyini dağıtmayı göz önünde bulundurun tüm yüksek güvenlikli dağıtımlarda öneririz.

toolearn DMZ'ler ve nasıl toodeploy bunları azure'da hello makalesini okuyun hakkında daha fazla [Microsoft bulut Hizmetleri ve ağ güvenliği](../best-practices-network-security.md).

## <a name="avoid-exposure-toohello-internet-with-dedicated-wan-links"></a>Ayrılmış WAN bağlantılarıyla Etkilenme toohello Internet kaçının
Birçok kuruluş hello karma BT rota seçtiniz. Başkalarının şirket içi kalırken karma BT hello şirketinizin bilgi varlıklarını bazıları Azure içinde değişir. Diğer bileşenleri şirket içi kalırken çoğu durumda, bir hizmetin bazı bileşenleri Azure'da çalıştırırsınız.

Merhaba karma BT senaryo, genellikle şirket içi bağlantılar tür yok. Bu hello şirket tooconnect kendi şirket içi ağlar tooAzure sanal ağlar olanak tanıyan şirketler arası. İki şirket içi bağlantısı çözümlerini vardır:

* Siteden siteye VPN
* ExpressRoute

[Siteden siteye VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md) şirket içi ağınız ve Azure sanal ağ arasında özel bir sanal bağlantı temsil eder. Bu bağlantı gerçekleşmesi üzerinde Internet hello ve sağlar çok "ağınız ve Azure arasında şifrelenmiş bir bağlantı içindeki bilgileri tünel". Siteden siteye VPN ölçekteki kurumların on yılları için dağıtılan güvenli, olgun bir teknolojidir. Tünel şifreleme kullanarak gerçekleştirilir [IPSec tünel modu](https://technet.microsoft.com/library/cc786385.aspx).

Siteden siteye VPN güvenilir, güvenilir ve yerleşik bir teknoloji olsa da, hello tünel içindeki trafiği hello Internet çapraz geçiş. Ayrıca, bant genişliği görece kısıtlanmış tooa en fazla 200 MB/sn hakkında olur.

Şirket içi bağlantılarınız için güvenlik ve performans olağanüstü bir düzeyi gerekiyorsa, şirket içi bağlantılar için Azure ExpressRoute kullanmanızı öneririz. Expressroute'dur ayrılmış WAN şirket içi konumunuz veya bir Exchange barındırma sağlayıcısı arasındaki bağlantı. Bu telco bağlantı olduğundan, verilerinizi hello Internet yolculuk değil ve bu nedenle değil gösterilen toohello olası riskleri Internet iletişimlerde devralınmış.

Azure ExpressRoute nasıl çalıştığı hakkında daha fazla toolearn ve nasıl toodeploy, hello makalesini okuyun [ExpressRoute teknik genel bakış](../expressroute/expressroute-introduction.md).

## <a name="optimize-uptime-and-performance"></a>Açık kalma süresi ve performansı en iyi duruma getirme
Gizlilik, bütünlük ve kullanılabilirlik (CIA) hello Üçlü bugünün en etkili güvenlik modelinin kapsar. Gizliliği şifreleme ve gizlilik, bütünlük verileri yetkisiz personeli tarafından değiştirilmez ve yetkili kişiler mümkün tooaccess hello bilgi yetkileri olduğundan emin olmanızı hedefler kullanılabilirliği olduğundan emin olmanızı hedefler tooaccess. Bu alanlar herhangi birinde başarısızlığı olası bir ihlali güvenlik temsil eder.

Kullanılabilirlik, açık kalma süresi ve performans hakkında olduğu düşünülebilir. Bir hizmeti çalışmıyorsa, bilgi erişilemiyor. Performans toomake hello veri kullanılamaz durumda kadar düşük olduğunda, ardından biz hello veri toobe erişilemez düşünebilirsiniz. Bu nedenle, güvenlik açısından bakıldığında, toodo ne olursa olsun ihtiyacımız toomake hizmetlerimizle en iyi çalışır durumda kalma süresi ve performans olmasını geçebiliriz.
Popüler ve etkili bir yöntem tooenhance kullanılabilirlik kullanıldığı ve performans toouse Yük Dengeleme. Yük Dengeleme, bir hizmetin parçası olan sunucular arasında ağ trafiğini dağıtmanın bir yöntemdir. Örneğin, ön uç web sunucuları, hizmetin bir parçası varsa, Yük Dengeleme, birden çok ön uç web sunucusu arasında toodistribute hello trafiğini kullanabilirsiniz.

Merhaba web sunuculardan biri kullanılamaz duruma gelirse, hello yük dengeleyici trafiğini toothat sunucuyu ve hala çevrimiçi olduğu yeniden yönlendirme trafiği toohello sunucuları göndermeyi durdurması çünkü bu dağıtım trafik kullanılabilirliğini artırır. Merhaba işlemci, ağ ve isteklere hizmet vermek için ek bellek dağıtılır çünkü tüm hello yük dengeli sunuculara Yük Dengeleme de performans, yardımcı olur.

Yük Dengeleme yapabilecekleriniz olduğunda ve hizmetleriniz için uygun şekilde kullanması önerilir. Biz, aşağıdaki bölümlerde hello site adres.
Hello Azure sanal ağ düzeyi Azure üç birincil sizinle Yük Dengeleme seçeneklerini sağlar:

* HTTP tabanlı Yük Dengeleme
* Dış Yük Dengeleme
* İç yük dengeleyici

## <a name="http-based-load-balancing"></a>HTTP tabanlı Yük Dengeleme
HTTP tabanlı Yük Dengeleme Özellikleri hello HTTP protokolü kullanarak hangi sunucu toosend bağlantıları hakkında kararlar alır. Azure uygulama ağ geçidi hello adı tarafından gelecek bir HTTP yük dengeleyici sahiptir.

Öneririz, bize Azure uygulama ağ geçidi zaman:

* İstekleri gerektiren uygulamalar hello aynı kullanıcı/istemci oturumu tooreach hello aynı arka uç sanal makine. Bu örnekleri Sepeti uygulamaları ve web posta sunucuları alışveriş.
* Toofree web sunucusu gruplarında SSL sonlandırma gelen ek yükü uygulama ağ geçidi yararlanarak istediğiniz uygulamaları [SSL boşaltma](https://f5.com/glossary/ssl-offloading) özelliği.
* Uygulamalar, bir içerik teslim ağı gibi aynı uzun süre çalışan TCP bağlantısı toobe yönlendirilmesini veya yük dengeli toodifferent arka uç sunucuları hello birden çok HTTP isteklerini gerektirir.

Azure uygulama ağ geçidi nasıl çalıştığı ve nasıl dağıtımlarınızda, kullanabileceğiniz hakkında daha fazla toolearn hello makalesini okuyun [uygulama ağ geçidi'ne genel bakış](../application-gateway/application-gateway-introduction.md).

## <a name="external-load-balancing"></a>Dış Yük Dengeleme
Merhaba Internet gelen bağlantılara bir Azure sanal ağınızda bulunan, sunucular arasında dengeli olduğunda dış Yük Dengeleme gerçekleşir. Hello Azure dış yük dengeleyici bu yeteneği sağlayabilir ve gerektiğinde bunu hello Yapışkan oturumları gerektirmeyen ya da SSL boşaltma kullanmanızı öneririz.

Buna karşılık, tooHTTP tabanlı Yük Dengeleme hello dış yük dengeleyici hello OSI ağ modeli toomake kararlarına hangi sunucu tooload Bakiye bağlantısı üzerinde hello ağ ve Aktarım katmanı adresindeki bilgileri kullanır.

Sahip olduğunuz her durumda, dış Yük Dengeleme kullanmanızı öneririz [durum bilgisiz uygulamaların](http://whatis.techtarget.com/definition/stateless-app) hello Internet öğesinden gelen istekleri kabul.

hello Azure dış yük dengeleyici nasıl çalıştığını ve onu nasıl dağıtabileceğiniz hakkında daha fazla toolearn hello makalesini okuyun [PowerShell kullanarak Kaynak Yöneticisi'nde bir Internet'e yönelik Yük dengeleyicinin oluşturmaya başlamak](../load-balancer/load-balancer-get-started-internet-arm-ps.md).

## <a name="internal-load-balancing"></a>İç Yük Dengeleme
İç Yük Dengeleme olan benzer tooexternal Yük Dengeleme ve kullandığı aynı mekanizması tooload Bakiye bağlantıları toohello sunucuları arkasına hello. Merhaba yalnızca o hello yük dengeleyici, bu durumda hello Internet üzerinde olmayan sanal makineleri gelen bağlantıları kabul farktır. Çoğu durumda, Yük Dengeleme için kabul edilen hello bağlantıları bir Azure sanal ağı üzerindeki cihazlar tarafından başlatılır.

İç Yük Dengeleme tooload Bakiye bağlantıları tooSQL sunucuları veya dahili web sunucularındaki gerektiğinde gibi bu özelliği, yararlı olacak senaryoları için kullanmanızı öneririz.

Azure iç Yük Dengeleme nasıl çalıştığını ve onu nasıl dağıtabileceğiniz hakkında daha fazla toolearn hello makalesini okuyun [PowerShell kullanarak bir iç yük dengeleyici oluşturmaya başlamak](../load-balancer/load-balancer-get-started-internet-arm-ps.md#update-an-existing-load-balancer).

## <a name="use-global-load-balancing"></a>Genel Yük Dengelemesi
Mümkün kılar genel bulut toodeploy genel Merhaba Dünya çapında veri merkezlerinde bulunan bileşenleri uygulamaları dağıtılmış. Bu tooAzure'nın genel datacenter varlığı Microsoft Azure üzerinde mümkün olur. Buna karşılık toohello Yük Dengeleme teknolojilerini daha önce hatta tüm veri merkezlerinde kullanılamaz hale gelebilir zaman genel Yük Dengeleme olası toomake Hizmetleri kullanılabilir hale getirir bahsedilen.

Bu tür Azure'daki yararlanarak genel Yük Dengeleme alabilirsiniz [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/). Trafik Yöneticisi yapar olası tooload Bakiye olan bağlantıları tooyour services tabanlı hello kullanıcı hello konumunu.

Örneğin, Hello kullanıcı hello AB isteği tooyour hizmetinden değiştirirken, bir AB veri merkezinde bulunan yönlendirilmiş tooyour Hizmetleri hello bağlantı olur. Bu yardımcı tooimprove performansı trafik Yöneticisi genel Yük Dengeleme datacenter en yakın toohello bağlanma çünkü uzakta olan toodatacenters bağlanmaktan daha hızlı bir parçasıdır.

Merhaba kullanılabilirlik tarafında, veri merkezinin tamamı kullanılamaz hale olsa bile hizmetinizi kullanılabilir olduğundan emin genel yük dengeleme sağlar.

Örneğin, bir Azure veri merkezi tooenvironmental nedenler veya son kullanılamaz hale gelirse toooutages (Bölgesel ağ hataları gibi), çevrimiçi datacenter en yakın toohello tooyour hizmet olacaktır bağlantıları yönlendirdi. Bu genel yük dengelemesi, trafik Yöneticisi'nde oluşturabilirsiniz DNS ilkeleri yararlanarak elde edilir.

Trafik Yöneticisi, birçok bölgeye yaygın olarak dağıtılan bir kapsama sahip ve çalışır durumda kalma süresi olası en yüksek düzeyde hello gerektiren geliştirme tüm bulut çözümü için kullanmanızı öneririz.

Azure trafik Yöneticisi hakkında daha fazla toolearn ve nasıl toodeploy, hello makalesini okuyun [trafik Yöneticisi nedir](../traffic-manager/traffic-manager-overview.md).

## <a name="disable-rdpssh-access-tooazure-virtual-machines"></a>RDP/SSH erişimini tooAzure sanal makineleri devre dışı bırak
Olası tooreach Azure sanal makineleri olduğundan hello kullanarak [Uzak Masaüstü Protokolü](https://en.wikipedia.org/wiki/Remote_Desktop_Protocol) (RDP) ve hello [Secure Shell](https://en.wikipedia.org/wiki/Secure_Shell) (SSH) protokoller. Bu protokollerin uzak konumlardan olası toomanage sanal makineler sağlamak ve veri merkezi bilgi standart.

Bu protokollerin hello Internet kullanarak hello olası güvenlik sorunudur saldırganlar çeşitli kullanabilirsiniz [yanılma](https://en.wikipedia.org/wiki/Brute-force_attack) teknikleri toogain erişim tooAzure sanal makineler. Hello saldırganlar erişim sonra sanal makinenizi Azure sanal ağınızdaki diğer makinelerin tehlikeye için bir başlatma noktası kullanın veya ağ bağlantılı cihazlar Azure dışında bile saldırı.

Bu nedenle, doğrudan RDP ve SSH erişim tooyour Azure sanal makineleri hello Internet gelen devre dışı bırakmanızı öneririz. Doğrudan RDP ve SSH Internet devre dışı hello eriştikten sonra tooaccess bu sanal makinelere uzaktan yönetim için kullanabileceğiniz diğer seçeneğiniz vardır:

* Noktadan siteye VPN
* Siteden siteye VPN
* ExpressRoute

[Noktadan siteye VPN](../vpn-gateway/vpn-gateway-point-to-site-create.md) uzaktan erişim VPN istemci/sunucu bağlantısı için başka bir terimdir. Bir noktadan siteye VPN hello Internet üzerinden bir tek kullanıcı tooconnect tooan Azure sanal ağ sağlar. Merhaba noktadan siteye bağlantı kurulur, hello kullanıcı mümkün toouse RDP olacaktır veya SSH tooconnect tooany sanal hello Azure sanal ağ üzerinde bulunan kullanıcı hello makineler bağlı toovia noktadan siteye sonra VPN. Bu hello kullanıcı varsayar yetkili tooreach bu sanal makineleri olduğundan.

Hello kullanıcı tooauthenticate iki kez bağlanan tooa sanal makine önce olduğundan noktadan siteye VPN doğrudan RDP veya SSH bağlantılarına göre daha güvenlidir. İlk olarak, kullanıcı gereksinimlerini tooauthenticate hello (ve yetkili olması) tooestablish hello noktadan siteye VPN bağlantısı; İkinci olarak, kullanıcı gereksinimlerini tooauthenticate hello (ve yetkili olması) tooestablish hello RDP veya SSH oturumu.

A [siteden siteye VPN](../vpn-gateway/vpn-gateway-site-to-site-create.md) tüm ağ tooanother ağ hello Internet bağlanır. Siteden siteye VPN tooconnect, şirket içi ağ tooan Azure sanal ağı kullanabilirsiniz. Siteden siteye VPN dağıtırsanız, şirket içi ağınızdaki kullanıcılar hello RDP kullanarak Azure sanal ağınızda mümkün tooconnect toovirtual makinelerde olacağını veya SSH protokolü üzerinde siteden siteye VPN bağlantısı hello ve tooallow doğrudan RDP veya SSH gerektirmez Merhaba Internet erişebilirsiniz.

Ayrılmış bir WAN bağlantısı tooprovide işlevselliği benzer toohello de kullanabilirsiniz siteden siteye VPN. Merhaba temel farklar 1 ' dir. Merhaba ayrılmış bir WAN bağlantısı hello Internet ve 2 çapraz geçiş değil. ayrılmış WAN genellikle daha fazla kararlı ve kullanıcı bağlantılardır. Azure, ayrılmış bir WAN bağlantısı çözümü hello biçiminde sağlar [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="enable-azure-security-center"></a>Etkinleştirme Azure Güvenlik Merkezi
Azure Güvenlik Merkezi, engellemenize, algılamanıza ve toothreats yanıt yardımcı olur ve artan, görünürlük ve denetim üzerinden, Azure kaynaklarınızın hello güvenlik sağlar. Aboneliklerinizde, tümleşik güvenlik izleme ve ilke yönetimi sağlar; normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.

Azure Güvenlik Merkezi en iyi duruma getirme ve ağ güvenliği tarafından izlemenize yardımcı olur:

* Ağ güvenlik önerileri sağlama
* Ağ güvenliği yapılandırması Hello durumunu izleme
* Temel toonetwork tehditleri hem hello uç ve ağ düzeylerinde uyarı

Azure Güvenlik Merkezi tüm Azure dağıtımları için etkinleştirmenizi öneririz.

Azure Güvenlik Merkezi ve nasıl tooenable, dağıtımları için hello makalesini okuyun hakkında daha fazla toolearn [giriş tooAzure Güvenlik Merkezi](../security-center/security-center-intro.md).

## <a name="securely-extend-your-datacenter-into-azure"></a>Güvenli bir şekilde veri merkeziniz Azure genişletme
Birçok kuruluş BT kuruluşları arıyor tooexpand, şirket içi veri merkezlerini büyüyen yerine hello buluta. Bu genişleme var olan BT altyapısının bir uzantı hello genel buluta temsil eder. Şirketler arası bağlantı seçenekleri olası tootreat olan yararlanarak, Azure sanal ağları olarak yalnızca başka bir alt ağda şirket içi altyapı ağ.

Ancak, çok sayıda planlama yoktur ve ilk toobe gereken tasarım konularını ele. Bu ağ güvenliği hello alanında özellikle önemlidir. Bir hello en iyi yolu toounderstand bu tür bir tasarım yaklaşımını nasıl toosee örneği değil.

Microsoft hello oluşturdu [Datacenter uzantısı başvuru mimarisi diyagramı](https://gallery.technet.microsoft.com/Datacenter-extension-687b1d84#content) ve yardımcı toohelp destekleyen, böyle bir veri merkezi uzantısı aşağıdaki gibi görünür anladığınızdan emin olun. Bu, tooplan kullanın ve bir güvenli kurumsal veri merkezi uzantısı toohello bulut tasarım örnek başvuru uygulaması sağlar. Bu belge tooget güvenli bir çözümdür hello anahtar bileşenleri hakkında bir fikir gözden geçirmenizi öneririz.

nasıl toosecurely genişletmek merkeziniz Azure hakkında daha fazla toolearn Lütfen hello video görüntülemek [genişletme bilgisayarınızı Datacenter tooMicrosoft Azure](https://www.youtube.com/watch?v=Th1oQQCb2KA).
