---
title: "bir güvenlik duvarı ve Nsg'ler uygulamalarla aaaDMZ örnek – yapı DMZ tooprotect | Microsoft Docs"
description: "DMZ bir güvenlik duvarı ve ağ güvenlik grupları (NSG) ile derleme"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a>Örnek 2 – çevre tooprotect bir güvenlik duvarı ve Nsg'ler uygulamalarla yapı
[Dönüş toohello güvenlik sınırı en iyi uygulamalar sayfası][HOME]

Bu örnek, bir güvenlik duvarı, dört windows sunucuları ve ağ güvenlik grupları ile DMZ oluşturur. Bu da her hello ilgili komutları tooprovide her adımın daha derin bir anlayış yol gösterir. Ayrıca vardır bir trafik senaryo bölüm tooprovide ayrıntılı bir adım adım derinlemesine savunma hello katmanları üzerinden trafik geçer nasıl DMZ hello. Son olarak, hello references bölümünde hello tam kod ve yönerge toobuild bu ortam tootest çeşitli senaryoları ile deneme ise. 

![NVA ve NSG gelen DMZ][1]

## <a name="environment-description"></a>Ortam açıklaması
Bu örnekte hello aşağıdakileri içeren bir abonelik vardır:

* İki bulut hizmetlerini: "FrontEnd001" ve "BackEnd001"
* Bir sanal ağ "CorpNetwork" iki alt ağ ile: "Ön uç" ve "Arka uç"
* Tek bir ağ güvenlik uygulanan tooboth alt ağları olan Grup
* Bu örnekte Barracuda NextGen Firewall bir ağ sanal gereç toohello ön uç alt bağlı
* Uygulama web sunucusu ("IIS01") temsil eden bir Windows sunucusu
* Uygulama geri temsil eden iki windows sunucuları sunucuları ("AppVM01", "AppVM02") end
* Bir DNS sunucusu ("DNS01") temsil eden bir Windows sunucusu

> [!NOTE]
> Bu örnek birçok farklı ağ sanal Gereçleri Bu örnek için kullanılabilecek hello bir Barracuda NextGen Firewall kullansa da.
> 
> 

Merhaba başvurular bölümünde yukarıda açıklanan hello ortamı çoğunu oluşturacak bir PowerShell komut dosyası yok. Yapı hello VM'ler ve sanal ağlar, bu belgede ayrıntılı hello örnek komut dosyası tarafından yapılır rağmen açıklanmamaktadır.

toobuild hello ortamı:

1. (Adları, konum ve IP adreslerini toomatch verilen hello senaryo güncelleştirilmiş) hello başvurular bölümüne dahil hello ağ yapılandırma xml dosyasını kaydedin
2. Güncelleştirme hello kullanıcı değişkenleri hello betik toomatch hello ortamı hello komut olan toobe Çalıştır (Abonelikleri, hizmet adlarını vb. karşı)
3. PowerShell'de Hello komut dosyası yürütme

**Not**: hello PowerShell Betiği miktarlara hello bölge hello ağ yapılandırması xml dosyasında miktarlara hello bölge eşleşmesi gerekir.

Merhaba komut dosyası başarıyla çalıştıktan sonra sonrası betik adımları izleyerek hello izlenebilir:

1. Merhaba güvenlik duvarı kuralları ayarlamak, bu başlıklı hello aşağıdaki bölümde ele alınmıştır: güvenlik duvarı kuralları.
2. İsteğe bağlı olarak iki komut dosyaları tooset hello web sunucusu ve uygulama sunucusu bu DMZ yapılandırma ile test basit bir web uygulaması tooallow ile Merhaba başvurular bölümünde bulunur.

Merhaba sonraki bölümde hello betikleri deyimleri göreli tooNetwork güvenlik grupları çoğunu açıklar.

## <a name="network-security-groups-nsg"></a>Ağ Güvenlik Grupları (NSG)
Bu örnekte, bir NSG grubu yerleşik ve altı kurallarıyla yüklendi. 

> [!TIP]
> Genel olarak bakıldığında, belirli "İzin ver" kurallarınızı ilk oluşturun ve daha genel "Deny" kuralları son hello gerekir. öncelik atanmış hello hangi kuralları ilk olarak değerlendirilir belirler. Trafik tooapply tooa belirli kural bulunduktan sonra başka hiçbir kural değerlendirilir. NSG kuralları hello ikisinde uygulayabileceğiniz gelen veya giden yön (Merhaba alt hello açısından).
> 
> 

Bildirimli olarak, kurallar aşağıdaki hello gelen trafik için oluşturulmakta:

1. İç DNS trafiğinin (bağlantı noktası 53) izin verilir
2. Merhaba Internet tooany VM gelen RDP trafiğine (3389 numaralı bağlantı noktası) izin verilir
3. Merhaba Internet toohello NVA (Güvenlik Duvarı) gelen HTTP trafiği (bağlantı noktası 80) izin verilir
4. IIS01 tooAppVM1 tüm trafiği (tüm bağlantı noktaları) izin verilir
5. Merhaba Internet toohello tüm trafiği (tüm bağlantı noktaları) tüm sanal ağ (her iki alt ağ) reddedildi
6. Merhaba ön uç alt toohello arka uç alt ağından gelen tüm trafiği (tüm bağlantı noktaları) reddedildi

Bu kuralları ilişkili tooeach alt ağ ile bir HTTP isteği hello Internet toohello web sunucusundan gelen ise her ikisi de kuralları 3 (izin verin) ve 5 (uygulamak reddetme), ancak 3 kuralı, yalnızca geçerli olur ve kural 5 oyuna değil gelen daha yüksek öncelikli olduğundan. Bu nedenle hello HTTP isteği toohello güvenlik duvarı izin. Bu aynı trafiği tooreach hello DNS01 sunucusunu denemeden ise hello ilk tooapply ve hello trafiği toopass toohello sunucu verilmez kural 5 (Reddet) olabilir. Toohello arka uç alt (dışında izin verilen trafiği kurallarında 1 ve 4) Konuşmayı gelen 6 (Reddet) blokları hello Frontend alt ağı kural, bir saldırganın güvenlik ihlalleri hello web uygulamasına hello ön uç hello saldırganın yoktur durumunda bu hello arka uç ağ korur sınırlı erişim toohello arka uç "ağ (yalnızca tooresources hello AppVM01 sunucu üzerinde gösterilen) korumalı".

Toohello giden trafiğe izin veren varsayılan giden kural Internet. Bu örnekte, biz giden trafiğe izin vermek ve herhangi bir giden kuralı değiştirme değil. Her iki yönde trafik aşağı toolock, kullanıcı tanımlanan yönlendirme gereklidir, hello bulunabilir farklı bir örnekte keşfedilen bu [ana güvenlik sınırı belge][HOME].

Merhaba yukarıda açıklanan NSG kuralları olan çok benzer toohello NSG kuralları [örnek 1 - yapı Nsg'ler ile basit DMZ][Example1]. Lütfen her bir NSG kural ve onun özniteliklerini ayrıntılı bir bakış için bu belgedeki hello NSG açıklama gözden geçirin.

## <a name="firewall-rules"></a>Güvenlik Duvarı Kuralları
Bir yönetim istemcisi yüklü bir bilgisayar toomanage hello Güvenlik Duvarı'nı toobe gerekir ve gerekli hello yapılandırmaları oluşturun. Merhaba, Güvenlik Duvarı (veya diğer NVA) belgelerinden satıcı nasıl toomanage hello üzerinde aygıt bakın. Bu bölümde Hello kalanı hello hello güvenlik duvarı yapılandırmasını kendisini hello satıcılar Yönetimi istemcisi (yani hello Azure portal veya PowerShell) aracılığıyla anlatmaktadır.

İstemci Yükleme ve bağlantı toohello Bu örnekte kullanılan Barracuda için yönergeler şurada bulunabilir: [Barracuda NG yönetici](https://techlib.barracuda.com/NG61/NGAdmin)

Merhaba güvenlik duvarında kuralları iletme oluşturulan toobe gerekir. Bu örnek yalnızca Internet trafiği bağlı toohello güvenlik duvarı ve toohello web sunucusuna yönlendirir olduğundan, yalnızca bir iletme NAT kuralı gereklidir. Merhaba Barracuda NextGen Firewall Bu örnek hello kullanılan üzerinde hedef NAT kuralı ("Dst NAT") toopass Bu trafik, kural olacaktır.

toocreate hello aşağıdaki kural (veya var olan varsayılan kuralları doğrulayın), hello Barracuda NG yönetici istemci panodan başlatma, toohello yapılandırma sekmesine gidin, hello işletimsel yapılandırma bölümü Ruleset'ı tıklatın. Bir kılavuz olarak adlandırılan, "Ana kuralları" Merhaba Güvenlik Duvarı'nda etkin ve devre dışı bırakılan kuralları varolan hello gösterir. Merhaba sağ üst köşedeki bu kılavuz, küçük, yeşil olduğundan "+" düğmesini tıklatın, bu toocreate yeni bir kural tıklayın (Not: güvenlik duvarını "değişiklikleri kilitlenebilir", bir düğme "Kilitleme" olarak işaretlenmiş ve güncelleştirilemiyor toocreate olan veya kuralları düzenlemek, tıklatın görürseniz bu düğme çok "kilidini" Merhaba RuleSet ve düzenlenmesine izin verilir). Mevcut bir kuralı tooedit istiyorsanız, o kural seçin, sağ tıklayın ve kuralını Düzenle seçin.

Yeni bir kural oluşturmak ve "WebTraffic" gibi bir ad sağlayın. 

Merhaba hedef NAT kuralı simgesi şu şekilde görünür: ![hedef NAT simgesi][2]

Merhaba kural kendisini şunun gibi görünür:

![Güvenlik Duvarı Kuralı][3]

Burada isabet tooreach HTTP (80 veya 443 HTTPS için bağlantı noktası) çalışırken güvenlik duvarı hello herhangi bir gelen adresi gönderilecek hello güvenlik duvarının "DHCP1 yerel IP" arabirimi ve yeniden yönlendirilen toohello hello 10.0.1.5 IP adresi ile Web sunucusu. Merhaba trafiği 80 numaralı bağlantı noktası ve bağlantı noktası 80 üzerinde devam eden toohello web sunucusu üzerinde gelen bu yana hiçbir bağlantı noktası değişikliği gerekiyordu. Ancak, bizim Web sunucusu bağlantı noktası 8080 böylece çevirirken kulak varsa, hedef listesi 10.0.1.5:8080 neden olmuştur hello gelen bağlantı noktası 80 hello güvenlik duvarı tooinbound bağlantı noktası 8080 üzerinde hello web sunucusu hello.

Bağlantı yöntemi de, hello hedef kural hello Internet'ten gelen için "Dinamik SNAT" en uygun olan miktarlara. 

Yalnızca bir kural oluşturuldu ancak önceliği doğru ayarlandığından emin önemlidir. Merhaba Güvenlik Duvarı'nda tüm kuralların hello kılavuzunda Yeni kuralın (aşağıda hello "BLOCKALL" kuralı) hello altta ise hiçbir zaman oyuna gelecektir. Yeni oluşturulan hello kuralı web trafiği için hello BLOCKALL kuralı olduğundan emin olun.

Merhaba kural oluşturulduktan sonra olmalıdır gönderilen toohello Güvenlik Duvarı'nı ve etkinleştirildi, bu değişiklik değil kazanacak hello kural yapılmazsa. Merhaba itme ve etkinleştirme işlemi hello sonraki bölümde açıklanmıştır.

## <a name="rule-activation"></a>Kural etkinleştirme
Merhaba ile ruleset tooadd bu kural değiştiren, hello ruleset olmalıdır toohello Güvenlik Duvarı'nı karşıya ve etkinleştirildi.

![Güvenlik duvarı kuralını etkinleştirme][4]

Merhaba üst sağ köşesinde hello management istemcisi düğmeleri oluşan bir küme var. Merhaba "değişiklikleri" Gönder düğmesi toosend değiştiren hello kuralları toohello güvenlik duvarı, ardından hello "Etkinleştir" düğmesini tıklatın.

Merhaba güvenlik duvarı ruleset Hello etkinleştirme ile bu örnek ortamı yapı tamamlanır. İsteğe bağlı olarak, hello post yapı hello betiklerde bölüm olabilir başvuruları tooadd bir uygulama toothis ortam tootest hello trafiği senaryolar aşağıda çalıştırın.

> [!IMPORTANT]
> Bu, hello web sunucusuna doğrudan karşılaşır değil, kritik toorealize olur. Bir tarayıcı FrontEnd001.CloudApp.Net HTTP sayfası istediğinde, bu trafiği toohello Güvenlik Duvarı'nı değil hello hello HTTP uç noktası (bağlantı noktası 80) geçişleri web sunucusu. Güvenlik Duvarı hello sonra toohello kural according toohello Web sunucusu isteği NAT yukarıdaki oluşturuldu.
> 
> 

## <a name="traffic-scenarios"></a>Trafik senaryoları
#### <a name="allowed-web-tooweb-server-through-firewall"></a>(İzin verilir) Web tooWeb sunucu güvenlik duvarı üzerinden
1. Internet kullanıcı istekleri HTTP sayfasına FrontEnd001.CloudApp.Net (Internet'e yönelik bulut hizmeti)
2. Bulut hizmeti geçiş trafiği 80 numaralı bağlantı noktasını toofirewall yerel arabirimdeki 10.0.1.4:80 üzerinde açık uç noktası aracılığıyla
3. Ön uç alt gelen kuralı işleme başlar:
   1. NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı
   2. NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı
   3. NSG kural 3 (Internet tooFirewall) geçerli, izin verilen, Dur kural işlenirken trafiğidir
4. Merhaba Güvenlik Duvarı (10.0.1.4) iç IP adresi trafik isabetler
5. Güvenlik Duvarı iletme kuralı bkz: Bu bağlantı noktası 80 trafiği, toohello web sunucusuna IIS01 yönlendirir
6. IIS01 web trafiği için dinleme, bu isteği alır ve hello isteği işlemeye başlıyor
7. IIS01 hello SQL Server AppVM01 hakkında bilgi için sorar
8. Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir
9. Merhaba arka uç alt gelen kuralı işleme başlar:
   1. NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı
   2. NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı
   3. NSG kuralı 3 (Internet tooFirewall) değil, uygulama toonext kuralı Taşı
   4. NSG kuralı 4 (IIS01 tooAppVM01) geçerli, izin verilen, Dur kural işlenirken trafiğidir
10. AppVM01 hello SQL sorgusu alır ve yanıtlar
11. Olduğundan hiçbir giden kuralları hello arka uç alt hello yanıt üzerinde izin verilir
12. Ön uç alt gelen kuralı işleme başlar:
    1. Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok
    2. Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır.
13. Merhaba IIS sunucusu hello SQL yanıtı alır ve hello HTTP yanıtı tamamlar ve toohello istek gönderir
14. Bir NAT oturumu hello Güvenlik Duvarı'ndan olduğundan, hello yanıt hedef Merhaba Güvenlik Duvarı'nı (başlangıçta) kalır.
15. Merhaba güvenlik duvarı hello Web sunucusu hello yanıtı alır ve geri toohello Internet kullanıcı iletir
16. Olduğundan hiçbir giden kuralları hello ön uç alt hello yanıt üzerinde izin verilir ve hello web sayfasının hello Internet kullanıcı alır.

#### <a name="allowed-rdp-toobackend"></a>(İzin verilir) RDP tooBackend
1. Sunucu Yöneticisi internet üzerindeki istekleri xxxxx RDP tooAppVM01 hello rastgele atanan bağlantı noktası numarası olduğu BackEnd001.CloudApp.Net:xxxxx üzerinde RDP oturumu tooAppVM01 (Merhaba atanan bağlantı noktası bulunabilir hello Azure Portal veya PowerShell aracılığıyla)
2. Güvenlik Duvarı yalnızca FrontEnd001.CloudApp.Net adresi hello üzerinde dinleme hello itibaren bu trafik akışı ile dahil değil
3. Arka uç alt gelen kuralı işleme başlar:
   1. NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı
   2. NSG kuralı 2 (RDP) uygulamak için izin verilen, Dur kural işlenirken trafiğidir
4. Hiçbir giden kuralları, varsayılan kuralları uygula ve dönüş trafiğine izin verilir
5. RDP oturumu etkin
6. Kullanıcı adı ve parolasını AppVM01 ister

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(İzin verilir) DNS sunucusundaki Web sunucusu DNS araması
1. Sunucu, IIS01, gereksinimlerini www.data.gov bir veri akışı web ancak tooresolve adresi hello.
2. Merhaba ağ yapılandırma hello VNet listeleri DNS01 (10.0.2.4 hello arka uç alt ağdaki) hello birincil DNS sunucusu olarak, IIS01 hello DNS isteği tooDNS01 gönderir
3. Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir
4. Arka uç alt gelen kuralı işleme başlar:
   1. NSG kural 1 (DNS) uygulamak için izin verilen, Dur kural işlenirken trafiğidir
5. DNS sunucusu hello isteği alır
6. DNS sunucusu önbelleğe hello adresi yoksa ve bir kök DNS sunucusu üzerinde hello ister Internet
7. Hiçbir giden kuralları arka uç alt ağdaki trafiğe izin verilir
8. Bu oturumda dahili olarak başlatıldı beri Internet DNS sunucusu yanıt, hello yanıt izin verilir
9. DNS sunucusu hello yanıtı önbelleğe alır ve toohello ilk isteği geri tooIIS01 yanıt verir
10. Hiçbir giden kuralları arka uç alt ağdaki trafiğe izin verilir
11. Ön uç alt gelen kuralı işleme başlar:
    1. Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok
    2. Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır
12. IIS01 hello yanıt DNS01 alır.

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(İzin verilir) Web sunucusu erişimini dosyasını AppVM01 üzerinde
1. Bir dosyanın AppVM01 IIS01 sorar
2. Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir
3. Merhaba arka uç alt gelen kuralı işleme başlar:
   1. NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı
   2. NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı
   3. NSG kuralı 3 (Internet tooFirewall) değil, uygulama toonext kuralı Taşı
   4. NSG kuralı 4 (IIS01 tooAppVM01) geçerli, izin verilen, Dur kural işlenirken trafiğidir
4. AppVM01 hello isteğini alır ve (erişim yetkisi varsayılarak) dosyası ile yanıt verir
5. Olduğundan hiçbir giden kuralları hello arka uç alt hello yanıt üzerinde izin verilir
6. Ön uç alt gelen kuralı işleme başlar:
   1. Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok
   2. Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır.
7. Merhaba IIS sunucu hello dosya alır

#### <a name="denied-web-direct-tooweb-server"></a>(Reddedildi) Web doğrudan tooWeb sunucu
Merhaba Web sunucusu, IIS01 ve hello Güvenlik Duvarı bu yana olan hello paylaştıkları aynı bulut hizmetine hello aynı genel kullanıma yönelik IP adresi. Bu nedenle herhangi bir HTTP trafiğini yönlendirilmiş toohello güvenlik duvarı. Merhaba isteği başarıyla sundu, ancak toohello Web sunucusu, kendisine geçirilen doğrudan bu tasarlandığı gibi dönülemez güvenlik duvarı hello ilk. Bkz: Merhaba trafik akışı için bu bölümdeki ilk senaryoda hello.

#### <a name="denied-web-toobackend-server"></a>(Reddedildi) Web tooBackend sunucu
1. Internet kullanıcı tooaccess AppVM01 bir dosyada hello BackEnd001.CloudApp.Net hizmeti ile çalışır
2. Dosya Paylaşımı için açık uç nokta yok olduğundan bu hello bulut hizmeti geçip geçmeyeceğini değil ve hello sunucusuna ulaşabilir olmayacaktır
3. NSG kural 5 (Internet tooVNet) Hello uç noktaları için herhangi bir nedenle açıksa, bu trafiği engeller

#### <a name="denied-web-dns-lookup-on-dns-server"></a>(Reddedildi) DNS sunucusundaki Web DNS araması
1. Internet kullanıcı toolookup DNS01 hello BackEnd001.CloudApp.Net hizmeti aracılığıyla bir iç DNS kaydını çalışır
2. DNS için açık uç nokta yok olduğundan bu hello bulut hizmeti geçip geçmeyeceğini değil ve hello sunucusuna ulaşabilir olmayacaktır
3. NSG kural 5 (Internet tooVNet) Hello uç noktaları için herhangi bir nedenle açıksa, bu trafiği engeller (Not: Bu kural 1 (DNS), iki nedenden dolayı geçerli değil, ilk hello kaynak adresi Internet Merhaba, toohello yalnızca bu kuralın uygulanacağı hello olarak yerel VNet kaynak, aynı zamanda hiçbir zaman trafiği reddetmeye şekilde bir izin verme kuralı budur)

#### <a name="denied-web-toosql-access-through-firewall"></a>(Reddedildi) Güvenlik Duvarı aracılığıyla Web tooSQL erişimi
1. Internet kullanıcı SQL verileri FrontEnd001.CloudApp.Net (Internet'e yönelik bulut hizmeti) ' ister.
2. SQL için açık uç nokta yok olduğundan bu hello bulut hizmeti geçip geçmeyeceğini değil ve hello güvenlik duvarı ulaşmak olmayacaktır
3. Uç noktaları için herhangi bir nedenle açıksa, hello ön uç alt gelen kuralı işleme başlar:
   1. NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı
   2. NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı
   3. NSG Kural 2 (Internet tooFirewall) uygulamak için izin verilen, Dur kural işlenirken trafiğidir
4. Merhaba Güvenlik Duvarı (10.0.1.4) iç IP adresi trafik isabetler
5. Güvenlik Duvarı için SQL iletme kuralları yok ve trafik düşme hello

## <a name="conclusion"></a>Sonuç
Bu bir güvenlik duvarı ile uygulamanızı koruma ve hello arka uç alt ağından gelen trafiği yalıtma göreceli olarak doğrudan ileriye doğru bir yoludur.

Daha fazla örnekler ve ağ güvenlik sınırları genel bir bakış bulunabilir [burada][HOME].

## <a name="references"></a>Başvurular
### <a name="main-script-and-network-config"></a>Ana komut dosyası ve ağ yapılandırması
Merhaba tam komut dosyası bir PowerShell komut dosyası kaydedin. Merhaba ağ yapılandırma "NetworkConf2.xml" adlı bir dosyaya kaydedin.
Merhaba kullanıcı tanımlı değişkenleri gerektiği gibi değiştirin. Merhaba komut dosyasını çalıştırın, ardından hello güvenlik duvarı kuralı kurulum yönergeleri yukarıdaki izleyin.

#### <a name="full-script"></a>Tam komut dosyası
Merhaba kullanıcı tanımlı değişkenleri esas alarak bu betiği olur:

1. Tooan Azure aboneliğine bağlanma
2. Yeni depolama hesabı oluşturma
3. Yeni bir VNet ve hello ağ yapılandırma dosyasında tanımlanan iki alt ağ oluşturma
4. 4 windows server Vm'lerinin oluşturma
5. NSG dahil olmak üzere yapılandırın:
   * Bir NSG oluşturma
   * Kuralları ile doldurma
   * Merhaba NSG toohello uygun alt ağları bağlama

Bu PowerShell Betiği, bir bilgisayar veya sunucu, Internet'e yerel olarak çalıştırılmalıdır.

> [!IMPORTANT]
> Bu komut dosyasını çalıştırdığınızda, uyarı veya PowerShell'de pop diğer bilgilendirici iletileri olabilir. Yalnızca hata iletileri kırmızı sorunu nedeni edilir.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
       - Three Servers on hello BackEnd Subnet
       - Network Security Groups tooallow/deny traffic patterns as declared

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Security requirements are different for each use case and can be addressed in a
      myriad of ways. Please be sure that any sensitive data or applications are behind
      hello appropriate layer(s) of protection. This script serves as an example of some
      of hello techniques that can be used, but should not be used for all scenarios. You
      are responsible tooassess your security needs and hello appropriate protections
      needed, and then effectively implement those protections.

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       myFirewall - 10.0.1.4
       IIS01      - 10.0.1.5

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
            -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
            -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
            -Protocol *

        # Assign hello NSG toohello Subnets
            Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a>Ağ yapılandırma dosyası
Güncelleştirilmiş konumla bu xml dosyasını kaydedin ve hello bağlantı toothis toohello $NetworkConfigFile değişkeni yukarıdaki hello komut dosyası ekleyin.

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a>Örnek uygulama komut dosyaları
Bu ve diğer çevre örnekleri için örnek bir uygulama tooinstall istiyorsanız, bir bağlantı aşağıdaki hello sağlanmış: [örnek uygulama betiği][SampleApp]

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "NSG ile giriş DMZ"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Hedef NAT simgesi"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Güvenlik Duvarı Kuralı"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Güvenlik duvarı kuralını etkinleştirme"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
