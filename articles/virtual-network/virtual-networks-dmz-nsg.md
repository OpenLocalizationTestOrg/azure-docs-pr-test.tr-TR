---
title: "aaaAzure DMZ örnek – yapı Nsg'ler ile basit DMZ | Microsoft Docs"
description: "Bir çevre ağ güvenlik grupları (NSG) ile derleme"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a>Örnek 1 – Nsg'ler ile bir Azure Resource Manager şablonu kullanarak basit bir DMZ derleme
[Dönüş toohello güvenlik sınırı en iyi uygulamalar sayfası][HOME]

> [!div class="op_single_selector"]
> * [Resource Manager Şablonu](virtual-networks-dmz-nsg.md)
> * [Klasik - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

Bu örnekte basit DMZ dört Windows sunucuları ve ağ güvenlik grupları oluşturulur. Bu örnek hello ilgili şablonu bölümleri tooprovide her adımın daha derin bir anlayış açıklar. Trafik hello DMZ savunma hello katmanlar ile nasıl devam eder bir ayrıntılı adım adım bakış trafiği senaryo bölüm tooprovide bulunmaktadır. Son olarak, hello başvuruları hello tam şablon kodu ve yönergeleri toobuild bu ortam tootest ve çeşitli senaryoları ile deneme bölümündedir. 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

![NSG ile giriş DMZ][1]

## <a name="environment-description"></a>Ortam açıklaması
Bu örnekte, abonelik kaynakları aşağıdaki hello içerir:

* Tek bir kaynak grubu
* Sanal ağı iki alt ağ ile; "Ön uç" ve "Arka uç"
* Uygulanan tooboth alt ağıdır bir ağ güvenlik grubu
* Uygulama web sunucusu ("IIS01") temsil eden bir Windows sunucusu
* Uygulama arka uç sunucuları ("AppVM01", "AppVM02") temsil eden iki windows sunucuları
* Bir DNS sunucusu ("DNS01") temsil eden bir Windows sunucusu
* Merhaba uygulama web sunucusu ile ilişkili bir ortak IP adresi

Merhaba references bölümünde bu örnekte açıklanan hello ortamı derlemeler bir bağlantı tooan Azure Resource Manager şablonu yoktur. Yapı hello VM'ler ve sanal ağlar, bu belgede ayrıntılı hello örnek şablon tarafından yapılan rağmen açıklanmamaktadır. 

**toobuild bu ortam** (ayrıntılı yönergeler olduğunda hello references bölümünde bu belgenin);

1. Dağıtma sırasında Azure Resource Manager şablonu hello: [Azure hızlı başlangıç şablonları][Template]
2. Merhaba örnek uygulamayı yükleyin: [örnek uygulama betiği][SampleApp]

>[!NOTE]
>Bu örnekte, hello IIS sunucusu tooRDP tooany arka uç sunucuları, bir "atlama kutu." kullanılır İlk RDP toohello IIS sunucusunu ve sonra hello IIS sunucu RDP toohello arka uç sunucu. Alternatif olarak bir ortak IP her sunucu için daha kolay RDP NIC ile ilişkili olabilir.
> 
>

Merhaba aşağıdaki bölümlerde hello ağ güvenlik grubu ve nasıl hello Azure Resource Manager şablonu anahtar satırları arasında adım adım ilerlemenizi sağlayarak bu örnek için işlevleri ayrıntılı bir açıklama sağlayın.

## <a name="network-security-groups-nsg"></a>Ağ Güvenlik Grupları (NSG)
Bu örnekte, bir NSG grubu yerleşik ve altı kurallarıyla yüklendi. 

>[!TIP]
>Genel olarak bakıldığında, belirli "İzin ver" kurallarınızı ilk oluşturun ve daha genel "Deny" kuralları son hello gerekir. öncelik atanmış hello hangi kuralları ilk olarak değerlendirilir belirler. Trafik tooapply tooa belirli kural bulunduktan sonra başka hiçbir kural değerlendirilir. NSG kuralları hello ikisinde uygulayabileceğiniz gelen veya giden yön (Merhaba alt hello açısından).
>
>

Bildirimli olarak, kurallar aşağıdaki hello gelen trafik için oluşturulmakta:

1. İç DNS trafiğinin (bağlantı noktası 53) izin verilir
2. Merhaba Internet tooany VM gelen RDP trafiğine (3389 numaralı bağlantı noktası) izin verilir
3. Itanium tabanlı sistemler için HTTP trafiğine (bağlantı noktası 80) hello Internet tooweb sunucusundan (IIS01) izin verilir
4. IIS01 tooAppVM1 tüm trafiği (tüm bağlantı noktaları) izin verilir
5. Merhaba Internet toohello tüm trafiği (tüm bağlantı noktaları) tüm sanal ağ (her iki alt ağ) reddedildi
6. Merhaba ön uç alt toohello arka uç alt ağından gelen tüm trafiği (tüm bağlantı noktaları) reddedildi

Bu kurallar ilişkili tooeach alt ağ ile bir HTTP isteği hello Internet toohello web sunucusundan gelen ise her ikisi de kuralları 3 (izin verin) ve 5 (uygulamak reddetme), ancak 3 kuralı, yalnızca geçerli olur ve kural 5 oyuna değil gelen daha yüksek öncelikli olduğundan. Bu nedenle hello HTTP isteği toohello web sunucusu izin. Bu aynı trafiği tooreach hello DNS01 sunucusunu denemeden ise hello ilk tooapply ve hello trafiği toopass toohello sunucu verilmez kural 5 (Reddet) olabilir. Kural 6 (Reddet) toohello arka uç alt (dışında izin verilen trafiği kurallarında 1 ve 4) Konuşmayı gelen hello ön uç alt ağ blokları, hello saldırganın bir saldırganın güvenlik ihlalleri hello web uygulamasına hello ön uç misiniz durumunda bu kural kümesine hello arka uç ağ korur. arka uç "Korumalı ağ (yalnızca tooresources hello AppVM01 sunucu üzerinde gösterilen)" erişim toohello sınırlı.

Toohello giden trafiğe izin veren varsayılan giden kural Internet. Bu örnekte, biz giden trafiğe izin vermek ve herhangi bir giden kuralı değiştirme değil. Her iki yönde tooapply güvenlik ilkesi tootraffic, kullanıcı tanımlanan yönlendirme gereklidir ve "Örnek 3" Merhaba üzerinde incelediniz [güvenlik sınırı en iyi yöntemler sayfası][HOME].

Her kural aşağıdaki gibi daha ayrıntılı olarak ele alınmıştır:

1. Ağ güvenlik grubu kaynak örneklenen toohold hello kuralları olmalıdır:

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. Bu örnekte Hello ilk kural hello arka uç alt ağdaki tüm İç ağlara toohello DNS sunucusu arasında DNS trafiğine izin verir. Merhaba kuralı bazı önemli parametreler sahiptir:
  * "destinationAddressPrefix" - özel türde bir adres öneki "Varsayılan etiket" adlı kural kullanabilirsiniz, bu etiketler adres öneklerinin daha büyük bir kategori kolay bir yolu tooaddress sağlayan sistem tarafından sağlanan tanımlayıcılardır. Bu kural kullandığı varsayılan etiket "Internet" Merhaba toosignify VNet hello dışında herhangi bir adres. Diğer önek VirtualNetwork ve AzureLoadBalancer etiketleridir.
  * "Yönünü" trafik akışı hangi yönde bu kural etkinleşir belirtir. Merhaba yönünü (bağlı olarak bu NSG burada bağlı) hello açısından hello alt ağı veya sanal makine değil. Bu nedenle yönü "Giriş" ve trafiği hello alt girerek, hello kuralın ve hello alt ağdan çıkan trafiğe etkilenmez bu kural tarafından durumunda.
  * "Öncelik" Merhaba sırasını trafik akışı değerlendirileceğini belirler. Merhaba alt hello sayı hello yüksek hello önceliği. Tooa belirli bir trafik akışı bir kural uygulandığı zaman başka hiçbir kural işlenir. Bu nedenle öncelik 1 olan bir kural trafiğine izin verir ve trafiği, öncelik 2 olan bir kural reddeder ve tootraffic hem kuralları uygula durumunda hello trafiği tooflow izin (Kural 1 yüksek önceliğe sahip olduğundan etkisi sürdü ve başka hiçbir kural uygulanan).
  * "Erişim" Bu kural tarafından etkilenen trafiği engellenen ("Deny") veya izin verilen ("izin ver") olup olmadığını belirtir.

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. Bu kural, alt ağ RDP trafiğine tooflow hello herhangi bir sunucuda hello Internet toohello RDP bağlantı noktasından bağlı sağlar. 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. Bu kural gelen Internet trafiği toohit hello web sunucusu sağlar. Bu kural hello yönlendirme davranışını değiştirmez. Merhaba kural yalnızca IIS01 toopass giden trafiğe izin verir. Bu nedenle hello Internet trafiği bu kural izin ve daha fazla kural işlemeyi durdur hedef olarak hello web sunucusunun sahip. (Öncelikle hello kuralında 140 diğer tüm gelen Internet trafiğini engellendi). Yalnızca HTTP trafiğini işlemek, bu kural başka olabilir kısıtlı tooonly hedef bağlantı noktası 80 izin verin.

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. Bu kural hello IIS01 sunucusundan trafiği toopass toohello AppVM01 sunucu izin verir; bir sonraki kural diğer tüm ön uç tooBackend trafiği engeller. Bu kural, başlangıç bağlantı noktası biliniyorsa eklenmelidir tooimprove. Merhaba IIS sunucusu yalnızca SQL Server'da AppVM01 basarsa, örneğin, hello hedef bağlantı noktası aralığı değiştirildiği "*" (tüm) too1433 (Merhaba SQL bağlantı noktası) böylece Merhaba web uygulaması hiç tehlikeye AppVM01 üzerinde daha küçük bir gelen saldırı yüzeyini sağlar.

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. Bu kural hello Internet tooany sunucularından hello ağ üzerindeki trafiği engeller. Hello kurallarıyla öncelikli 110 ve 120 hello etkisi tooallow yalnızca gelen Internet trafiği toohello güvenlik duvarı ve sunucularda RDP bağlantı noktalarını ve şey engeller. Bu kural, "Ayrıcalık tanımayın" kural tooblock tüm beklenmeyen akışlar ' dir.

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. Merhaba son kural hello ön uç alt toohello arka uç alt ağından trafiği engeller. Bu kural yalnızca bir gelen kuralı olduğundan, geriye doğru trafiğinin (Merhaba arka uç toohello ön uç) izin verilir.

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a>Trafik senaryoları
#### <a name="allowed-internet-tooweb-server"></a>(*İzin verilen*) Internet tooweb sunucusu
1. NIC hello IIS01 NIC ile ilişkili hello hello ortak IP adresinden gelen HTTP sayfası bir Internet kullanıcı istekleri
2. Merhaba genel IP adresi trafik toohello VNet IIS01 doğru geçirir (Merhaba web sunucusu)
3. Ön uç alt gelen kuralı işleme başlar:
  1. NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı
  2. NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı
  3. NSG kural 3 (Internet tooIIS01) geçerli, izin verilen, Dur kural işlenirken trafiğidir
4. İç IP adresi hello web sunucusunun IIS01 (10.0.1.5) trafiği isabetler
5. IIS01 web trafiği için dinleme, bu isteği alır ve hello isteği işlemeye başlıyor
6. IIS01 hello SQL Server AppVM01 hakkında bilgi için sorar
7. Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir
8. Merhaba arka uç alt gelen kuralı işleme başlar:
  1. NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı
  2. NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı
  3. NSG kuralı 3 (Internet tooFirewall) değil, uygulama toonext kuralı Taşı
  4. NSG kuralı 4 (IIS01 tooAppVM01) geçerli, izin verilen, Dur kural işlenirken trafiğidir
9. AppVM01 hello SQL sorgusu alır ve yanıtlar
10. Merhaba arka uç alt ağda hiçbir giden kuralları olduğundan hello yanıt izin verilir
11. Ön uç alt gelen kuralı işleme başlar:
  1. Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok
  2. Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır.
12. Merhaba IIS sunucusu hello SQL yanıtı alır ve hello HTTP yanıtı tamamlar ve toohello isteyenin gönderir
13. Merhaba ön uç alt ağda hiçbir giden kuralları olduğundan, hello yanıt izin verilir ve hello web sayfasının hello Internet kullanıcı alır.

#### <a name="allowed-rdp-tooiis-server"></a>(*İzin verilen*) RDP tooIIS sunucu
1. Bir sunucu yöneticisi internet üzerindeki bir RDP oturumu tooIIS01 NIC hello IIS01 (Bu genel IP adresi Portal veya PowerShell hello bulunabilir) NIC ile ilişkili hello hello genel IP adresi üzerinde istekleri
2. Merhaba genel IP adresi trafik toohello VNet IIS01 doğru geçirir (Merhaba web sunucusu)
3. Ön uç alt gelen kuralı işleme başlar:
  1. NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı
  2. NSG kuralı 2 (RDP) uygulamak için izin verilen, Dur kural işlenirken trafiğidir
4. Hiçbir giden kuralları, varsayılan kuralları uygula ve dönüş trafiğine izin verilir
5. RDP oturumu etkin
6. IIS01 hello kullanıcı adı ve parola isteyen

>[!NOTE]
>Bu örnekte, hello IIS sunucusu tooRDP tooany arka uç sunucuları, bir "atlama kutu." kullanılır İlk RDP toohello IIS sunucusunu ve sonra hello IIS sunucu RDP toohello arka uç sunucu.
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a>(*İzin verilen*) Web sunucusu DNS araması DNS sunucusunda
1. Sunucu, IIS01, gereksinimlerini www.data.gov bir veri akışı web ancak tooresolve adresi hello.
2. Merhaba ağ yapılandırma hello VNet listeleri DNS01 (10.0.2.4 hello arka uç alt ağdaki) hello birincil DNS sunucusu olarak, IIS01 hello DNS isteği tooDNS01 gönderir
3. Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir
4. Arka uç alt gelen kuralı işleme başlar:
  * NSG kural 1 (DNS) uygulamak için izin verilen, Dur kural işlenirken trafiğidir
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

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(*İzin verilen*) Web sunucusu erişimini dosyasını AppVM01 üzerinde
1. Bir dosyanın AppVM01 IIS01 sorar
2. Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir
3. Merhaba arka uç alt gelen kuralı işleme başlar:
  1. NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı
  2. NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı
  3. NSG kuralı 3 (Internet tooIIS01) değil, uygulama toonext kuralı Taşı
  4. NSG kuralı 4 (IIS01 tooAppVM01) geçerli, izin verilen, Dur kural işlenirken trafiğidir
4. AppVM01 hello isteğini alır ve (erişim yetkisi varsayılarak) dosyası ile yanıt verir
5. Merhaba arka uç alt ağda hiçbir giden kuralları olduğundan hello yanıt izin verilir
6. Ön uç alt gelen kuralı işleme başlar:
  1. Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok
  2. Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır.
7. Merhaba IIS sunucu hello dosya alır

#### <a name="denied-rdp-toobackend"></a>(*Reddedildi*) RDP toobackend
1. Bir Internet kullanıcı tooRDP tooserver AppVM01 çalışır
2. Bu sunucular NIC ile ilişkili herhangi bir ortak IP adresi olduğundan, bu trafiği hello VNet hiçbir zaman girersiniz ve hello sunucusuna ulaşabilir olmayacaktır
3. Bir ortak IP adresi herhangi bir nedenden dolayı etkinleştirilirse, NSG kuralı 2 (RDP) bu trafiği ancak olanak tanır

>[!NOTE]
>Bu örnekte, hello IIS sunucusu tooRDP tooany arka uç sunucuları, bir "atlama kutu." kullanılır İlk RDP toohello IIS sunucusunu ve sonra hello IIS sunucu RDP toohello arka uç sunucu.
>
>

#### <a name="denied-web-toobackend-server"></a>(*Reddedildi*) Web toobackend sunucusu
1. Bir Internet kullanıcı tooaccess AppVM01 dosyada çalışır
2. Bu sunucular NIC ile ilişkili herhangi bir ortak IP adresi olduğundan, bu trafiği hello VNet hiçbir zaman girersiniz ve hello sunucusuna ulaşabilir olmayacaktır
3. Bir ortak IP adresi herhangi bir nedenden dolayı etkinleştirilirse, NSG kural 5 (Internet tooVNet) bu trafiği engeller

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Reddedildi*) DNS sunucusunda Web DNS araması
1. Bir Internet kullanıcı çalıştığında toolook DNS01 bir iç DNS kaydını ayarlama
2. Bu sunucular NIC ile ilişkili herhangi bir ortak IP adresi olduğundan, bu trafiği hello VNet hiçbir zaman girersiniz ve hello sunucusuna ulaşabilir olmayacaktır
3. Bir ortak IP adresi herhangi bir nedenden dolayı etkinleştirilirse, NSG kural 5 (Internet tooVNet) bu trafiği engeller (Not: is Internet hello ve kural 1 yalnızca toohello geçerlidir hello kaynak adresi istekleri için kuralı 1 (DNS) uygulanacak değil, yerel VNet hello kaynağı olarak)

#### <a name="denied-sql-access-on-hello-web-server"></a>(*Reddedildi*) hello web sunucusunda SQL erişimi
1. Bir Internet kullanıcının SQL veri IIS01 istekleri
2. Bu sunucular NIC ile ilişkili herhangi bir ortak IP adresi olduğundan, bu trafiği hello VNet hiçbir zaman girersiniz ve hello sunucusuna ulaşabilir olmayacaktır
3. Bir ortak IP adresi herhangi bir nedenden dolayı etkinleştirilirse, hello ön uç alt gelen kuralı işleme başlar:
  1. NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı
  2. NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı
  3. NSG kural 3 (Internet tooIIS01) geçerli, izin verilen, Dur kural işlenirken trafiğidir
4. İç IP adresi hello IIS01 (10.0.1.5) trafiği isabetler
5. Bağlantı noktası 1433, bu nedenle hiçbir yanıt toohello isteği IIS01 dinleme değil

## <a name="conclusion"></a>Sonuç
Bu örnek hello arka uç alt ağından gelen trafiği yalıtma, görece basit ve basit bir yoludur.

Daha fazla örnekler ve ağ güvenlik sınırları genel bir bakış bulunabilir [burada][HOME].

## <a name="references"></a>Başvurular
### <a name="azure-resource-manager-template"></a>Azure Resource Manager şablonu
Bu örnek, önceden tanımlanmış bir Azure Resource Manager şablonu Microsoft tarafından yönetilen bir GitHub deposunu kullanır ve toohello topluluk açın. Bu şablon Github'dan sınırsız dağıtılabilir veya indirilir ve gereksinimlerinizi toofit değiştirdi. 

"azuredeploy.json." adlı hello dosyasında Hello ana şablon. Bu şablon PowerShell veya CLI (Merhaba ilişkili "azuredeploy.parameters.json" dosyasıyla) gönderilebilir toodeploy bu şablonu. Hello en kolay yolu toouse hello github'da hello README.md sayfasındaki "Dağıtma tooAzure" düğmesi olan bulabilirim.

Bu örnek GitHub ve hello Azure portal, derlemeler toodeploy hello şablon şu adımları izleyin:

1. Tarayıcıdan toohello gidin [şablonu][Template]
2. Merhaba "Dağıtma tooAzure" düğmesine (veya hello "Görselleştir" düğmesine toosee bu şablonu grafik gösterimi) tıklatın
3. Merhaba parametreler dikey penceresinde Hello depolama hesabı, kullanıcı adı ve parola girin ve ardından **Tamam**
5. Bu dağıtım için bir kaynak grubu oluşturun (mevcut bir kullanabilirsiniz, ancak yeni bir en iyi sonuçlar için önerilir)
6. Gerekirse, sanal ağınızı hello abonelik ve konumda ayarlarını değiştirin.
7. Tıklatın **yasal koşulları gözden geçir**hello koşullarını okuyun ve tıklatın **satın alma** tooagree.
8. Tıklatın **oluşturma** bu şablonu toobegin hello dağıtımı.
9. Merhaba dağıtım başarıyla tamamlandıktan sonra kaynak grubu içinde yapılandırılmış bu dağıtım toosee hello kaynaklar için oluşturulan toohello gidin.

>[!NOTE]
>Bu şablon RDP toohello IIS01 yalnızca sunucu (IIS01 için genel IP hello portalı üzerinde Bul hello) sağlar. Bu örnekte, hello IIS sunucusu tooRDP tooany arka uç sunucuları, bir "atlama kutu." kullanılır İlk RDP toohello IIS sunucusunu ve sonra hello IIS sunucu RDP toohello arka uç sunucu.
>
>

tooremove bu dağıtım, delete hello kaynak grubu ve tüm alt kaynaklar da silinir.

#### <a name="sample-application-scripts"></a>Örnek uygulama komut dosyaları
Merhaba şablonu başarıyla çalıştıktan sonra bu DMZ yapılandırma ile test basit bir web uygulaması tooallow ile Merhaba web sunucusu ve uygulama sunucusu ayarlayabilirsiniz. tooinstall örnek bir uygulama bu ve diğer çevre örnekleri için bir sağlamış bağlantıyı izleyerek hello: [örnek uygulama betiği][SampleApp]

## <a name="next-steps"></a>Sonraki adımlar

* Bu örnek dağıtma
* Merhaba örnek uygulaması oluşturma
* Bu DMZ aracılığıyla farklı trafik akışları test etme

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "NSG ile giriş DMZ"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md