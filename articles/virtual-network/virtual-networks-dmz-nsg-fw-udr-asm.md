---
title: "bir güvenlik duvarı, UDR ve NSG ağlarla aaaDMZ örnek – yapı DMZ tooProtect | Microsoft Docs"
description: "Bir güvenlik duvarı ile DMZ derleme, kullanıcı tanımlı yönlendirme (UDR) ve ağ güvenlik grupları (NSG)"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a>Örnek 3 – bir güvenlik duvarı, UDR ve NSG ağlarla DMZ tooProtect derleme
[Dönüş toohello güvenlik sınırı en iyi uygulamalar sayfası][HOME]

Bu örnek, bir güvenlik duvarı, dört windows sunucuları, kullanıcı tanımlı yönlendirme, IP iletimi ve ağ güvenlik grupları ile DMZ oluşturur. Bu da her hello ilgili komutları tooprovide her adımın daha derin bir anlayış yol gösterir. Ayrıca vardır bir trafik senaryo bölüm tooprovide ayrıntılı bir adım adım derinlemesine savunma hello katmanları üzerinden trafik geçer nasıl DMZ hello. Son olarak, hello references bölümünde hello tam kod ve yönerge toobuild bu ortam tootest çeşitli senaryoları ile deneme ise. 

![Çift yönlü DMZ NVA, NSG ve UDR][1]

## <a name="environment-setup"></a>Ortam Kurulumu
Bu örnekte hello aşağıdakileri içeren bir abonelik vardır:

* Üç bulut hizmetlerini: "SecSvc001", "FrontEnd001" ve "BackEnd001"
* Bir sanal ağ "CorpNetwork" üç alt ağ ile: "SecNet", "Ön uç" ve "Arka uç"
* Bu örnekte bir güvenlik duvarı, bir ağ sanal gereç toohello SecNet alt bağlı
* Uygulama web sunucusu ("IIS01") temsil eden bir Windows sunucusu
* Uygulama geri temsil eden iki windows sunucuları sunucuları ("AppVM01", "AppVM02") end
* Bir DNS sunucusu ("DNS01") temsil eden bir Windows sunucusu

Merhaba başvurular bölümünde yukarıda açıklanan hello ortamı çoğunu oluşturacak bir PowerShell komut dosyası yok. Yapı hello VM'ler ve sanal ağlar, bu belgede ayrıntılı hello örnek komut dosyası tarafından yapılır rağmen açıklanmamaktadır.

toobuild hello ortamı:

1. (Adları, konum ve IP adreslerini toomatch verilen hello senaryo güncelleştirilmiş) hello başvurular bölümüne dahil hello ağ yapılandırma xml dosyasını kaydedin
2. Güncelleştirme hello kullanıcı değişkenleri hello betik toomatch hello ortamı hello komut olan toobe Çalıştır (Abonelikleri, hizmet adlarını vb. karşı)
3. PowerShell'de Hello komut dosyası yürütme

**Not**: hello PowerShell Betiği miktarlara hello bölge hello ağ yapılandırması xml dosyasında miktarlara hello bölge eşleşmesi gerekir.

Merhaba komut dosyası başarıyla çalıştıktan sonra sonrası betik adımları izleyerek hello izlenebilir:

1. Merhaba güvenlik duvarı kuralları ayarlamak, bu başlıklı hello aşağıdaki bölümde ele alınmıştır: güvenlik duvarı kuralı açıklaması.
2. İsteğe bağlı olarak iki komut dosyaları tooset hello web sunucusu ve uygulama sunucusu bu DMZ yapılandırma ile test basit bir web uygulaması tooallow ile Merhaba başvurular bölümünde bulunur.

Merhaba komut dosyası başarıyla çalıştıktan sonra hello güvenlik duvarı kuralları tamamlandı toobe gerekir, bu başlıklı hello bölümde ele alınmıştır: güvenlik duvarı kuralları.

## <a name="user-defined-routing-udr"></a>Kullanıcı tanımlı yönlendirme (UDR)
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

Merhaba VNETLocal hello tanımlanan adres ön hello VNet (IE, her belirli VNet nasıl tanımlandığına bağlı olarak VNet tooVNet değiştirilecek), belirli bir ağ için her zaman olur. Merhaba kalan sistem yolları statik ve yukarıdaki varsayılan.

Öncelik, ettirilmesi yollar hello en uzun ön ek eşleşmesi (LPM) yöntemiyle işlenir, böylece hello hello tablosunda en belirgin yolu hedef adres verilen tooa geçerli olur.

Bu nedenle, trafiği (örneğin toohello DNS01 sunucusu 10.0.2.4) hello yerel ağ (10.0.0.0/16) hello VNet tooits hedef toohello 10.0.0.0/16 rota son üzerinden yönlendirilecektir. Diğer bir deyişle, 10.0.2.4 için hello 10.0.0.0/16 yol hello en belirgin, hello 10.0.0.0/8 ve 0.0.0.0/0 de geçerli olabilir, ancak daha az belirli olduğundan bu trafiği etkilemez olsa bile yoldur. Bu nedenle hello trafiği too10.0.2.4 yerel VNet hello ve yalnızca toohello hedef yol bir sonraki atlama olarak gerekir.

Trafik tasarlanmıştır 10.1.1.1 için örneğin, hello 10.0.0.0/16 rota olmayacaktır uygularsanız, ancak hello 10.0.0.0/8 hello en belirgin olacaktır ve bu hello trafiği olacaktır ("siyah holed") hello sonraki atlama değeri Null olduğundan bırakıldı. 

Merhaba hedef tooany hello Null önekleri veya hello VNETLocal önekleri uygulayın kaydetmedi ve hello az belirli izlersiniz yönlendirmek, 0.0.0.0/0 ve toohello hello sonraki atlama olarak Internet ve böylece Azure'nın Internet kenar çıkışı yönlendirilmesi.

Merhaba rota tablosunda iki aynı önekleri varsa hello tercih sırasına göre hello yolları "kaynak" özniteliğine dayanarak hello aşağıda verilmiştir:

1. "Değerinin VirtualAppliance" = kullanıcı tanımlı yol el ile eklenen toohello tablosu
2. "VPNGateway" dinamik rota (BGP), karma ağlarla kullanıldığında = hello dinamik Protokolü otomatik olarak eşlenmiş ağ değişiklikleri yansıtır gibi dinamik ağ protokolü tarafından eklenen, bu yollar zaman içinde değişebilir
3. "Varsayılan" Merhaba sistem yolları = hello rota tabloda yukarıda gösterildiği gibi yerel VNet ve hello statik girişleri hello.

> [!NOTE]
> Gelen şirket içi toobe yönlendirilmiş tooa ağ sanal gereç (NVA) trafiği ve giden ExpressRoute ve VPN ağ geçitleri tooforce ile artık kullanıcı tanımlı yönlendirme (UDR) kullanabilirsiniz.
> 
> 

#### <a name="creating-hello-local-routes"></a>Merhaba yerel yollar oluşturma
Bu örnekte, iki yönlendirme tablolarını gereklidir, her biri hello ön uç ve arka uç alt ağlar için. Her tablo için alt ağ verilen hello uygun statik yollar ile yüklenir. Bu örnek Hello amaçla her tablo üç yol vardır:

1. Tanımlanan bir sonraki atlama tooallow yerel alt ağ trafiği toobypass hello güvenlik duvarı olmayan yerel alt ağ trafiği
2. Bir sonraki güvenlik duvarı olarak tanımlanan atlama ile sanal ağ trafiği, bu yerel VNet trafiği tooroute doğrudan veren hello varsayılan kuralı geçersiz kılar
3. Bir sonraki atlama ile tüm kalan trafiği (0/0) güvenlik duvarı hello olarak tanımlanan

Merhaba yönlendirme tablolarını oluşturulduktan sonra bunların ilişkili tootheir alt ağlardır. Merhaba ön uç için alt ağ yönlendirme tablosu, oluşturup bağlı sonra toohello alt aşağıdaki gibi görünmelidir:

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


Bu örnek için kullanılan toobuild hello rota tablosundan hello aşağıdaki komutlar, kullanıcı tanımlı yol eklemek ve hello rota tablosu tooa alt ağa bağlamak (Not; dolar işareti ile başlayan altındaki öğeleri (örn: $BESubnet) hello komut dosyasından kullanıcı tanımlı değişkenler Merhaba başvuru bölümü, bu belgenin):

1. İlk hello temel yönlendirme tablosu oluşturulması gerekir. Bu kod parçacığında hello arka uç alt ağ için hello tablosu hello oluşturulmasını gösterir. Merhaba komut dosyasında karşılık gelen bir tablo için hello ön uç alt da oluşturulur.
   
     AzureRouteTable yeni-ad $BERouteTableName '
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. Merhaba yol tablosu oluşturulduktan sonra belirli kullanıcı tanımlı yollar eklenebilir. Bu konuda kırpılmış, tüm trafik (0.0.0.0/0) (bir $VMIP [0], başlangıç IP adresi hello sanal gereç önceki hello komut dosyasında oluşturulduğunda atanan kullanılan toopass değişkendir) hello sanal gereç aracılığıyla yönlendirilir. Merhaba komut dosyasında karşılık gelen bir kural hello ön uç tablosunda da oluşturulur.
   
     Get-AzureRouteTable $BERouteTableName | `
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. Rota girişi yukarıda Hello kılar hello varsayılan "0.0.0.0/0" yol, ancak hala hangi belirleyebilmesini varolan hello varsayılan 10.0.0.0/16 kuralı trafiği hello VNet tooroute içinde doğrudan toohello hedef ve toohello ağ sanal gereç. toocorrect bu davranışı hello izleyin kural eklenmesi gerekir.
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. Bu noktada yaptığınız bir seçim toobe yoktur. İki yoldan yukarıda hello ile tüm trafik değerlendirmesi, tek bir alt ağ içindeki bile trafiği için Güvenlik Duvarı'nı toohello yönlendirilecek. Üçüncü, belirli bir kural eklenebilir hello Güvenlik Duvarı'nı müdahalesi olmadan yerel olarak bir alt ağ tooroute içinde tooallow trafiği ancak bu, istenebilir. Bu yol var bildiren herhangi bir adresi destine hello yerel alt ağ yalnızca için rota doğrudan (NextHopType VNETLocal =).
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. Son olarak, oluşturulur ve kullanıcı tanımlı yollar ile doldurulur hello yönlendirme tablosunu ile Merhaba tablo şimdi ilişkili tooa alt olmalıdır. Hello komut dosyasında hello ön uç yol tablosu da ilişkili toohello Frontend alt ağı var. Merhaba bağlama betik hello arka uç alt ağ için aşağıda verilmiştir.
   
     Set-AzureSubnetRouteTable - VirtualNetworkName $VNetName '
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a>IP İletimi
Bir yardımcı özelliği tooUDR olduğu IP iletimi. Bu özellikle tooreceive trafiğe izin veren bir sanal gereç ayarda toohello Gereci ele ve bu trafiği tooits ultimate hedef iletin.

AppVM01 trafiğinden istek toohello DNS01 sunucusu yaparsa örnek olarak, bu toohello güvenlik duvarı UDR rota. Etkin IP iletimi ile hello trafiği hello DNS01 hedef (10.0.2.4) için hello Gereci (10.0.0.4) tarafından kabul ve olması tooits ultimate hedef (10.0.2.4) iletilir. Merhaba yol tablosu hello güvenlik duvarı hello sonraki atlama olarak olmasına rağmen hello üzerinde Güvenlik Duvarı etkin IP iletimi, trafiği hello Gereci tarafından kabul değil. 

> [!IMPORTANT]
> Kritik tooremember tooenable IP iletimi kullanıcı tanımlı yönlendirme ile birlikte olur.
> 
> 

IP iletimi ayarlama tek bir komut ve VM oluşturma zamanında yapılabilir. Hello için bu örnek hello kod parçacığını akışını hello komut dosyasının hello sonuna doğru olduğundan ve hello UDR komutları ile gruplandırılmış:

1. Sanal gereç olan hello VM örneği çağrısı, Güvenlik Duvarı bu durumda hello ve IP iletimini etkinleştirme (Not; dolar işareti kırmızı başlayarak herhangi bir öğeye (örn: $VMName[0]), bu belgenin hello başvuru bölümünde hello komut dosyasından bir kullanıcı tanımlı değişkendir. köşeli ayraçlar [0] sıfır Merhaba, temsil VM'ler, hello dizideki hello örnek komut dosyası toowork değişiklik yapmadan için ilk VM Merhaba, ilk VM (VM 0) olmalıdır hello hello Güvenlik Duvarı):
   
     Get-AzureVM-$ServiceName [0] [0] $VMName - ServiceName adı | `
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a>Ağ Güvenlik Grupları (NSG)
Bu örnekte, bir NSG grubu yerleşik ve tek bir kural ile yüklenir. Bu grup ise yalnızca toohello ön uç ve arka uç alt ağlar (değil SecNet hello) bağlı. Bildirimli olarak kural aşağıdaki hello üretiliyor:

1. Merhaba Internet toohello tüm trafiği (tüm bağlantı noktaları) tüm sanal ağ (tüm alt ağlar) reddedildi

Nsg'ler Bu örnekte kullanılan cihazın ana amacı el ile yetersizliğini karşı savunma ikincil bir katmanı olarak olsa da. Hello Internet tooeither hello ön uç gelen tüm trafiği tooblock istiyoruz veya arka uç alt ağlar, trafiği yalnızca hello SecNet alt toohello güvenlik duvarı akış (ve ardından IF uygun toohello ön uç veya arka uç alt ağlar). Ayrıca, bir yerde, hello UDR kurallarla ön uç veya arka uç alt hello yaptı tüm trafik toohello Güvenlik Duvarı (teşekkürler tooUDR) yönlendirilmesi. Merhaba Güvenlik Duvarı'nı bu asimetrik bir akış halinde görür ve hello giden trafiği bırakma. Bu nedenle üç katmanlı güvenlik koruma hello ön uç ve arka uç alt ağları vardır; 1) hiçbir açık uç noktalarda hello FrontEnd001 ve BackEnd001 bulut Hizmetleri, 2) Nsg'ler reddetme trafiği hello 3) hello güvenlik duvarı asimetrik trafiğini atar.

Bu örnekte hello ağ güvenlik grubu ile ilgili bir ilginç noktası, yalnızca bir kural, aşağıda gösterilen hello güvenlik alt ağ içeren toodeny Internet trafiği toohello tüm sanal ağ olan içermesidir. 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

NSG, yalnızca hello toohello ön uç ve arka uç alt ağları bağlı olduğundan, hello kural trafiğinde ancak işlenen değil toohello güvenlik alt ağ gelen. Sonuç olarak, NSG gerçekleştirilemeyen hello toohello güvenlik alt ağa bağlı olduğundan hello NSG Kuralı Internet trafiği tooany adres Vnet'in hello üzerinde söyler. olsa bile, trafik toohello güvenlik alt ağ akar.

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a>Güvenlik Duvarı Kuralları
Merhaba güvenlik duvarında kuralları iletme oluşturulan toobe gerekir. Merhaba güvenlik duvarı engelleme veya iletme tüm gelen, giden ve içi-VNet trafiği olduğundan birçok güvenlik duvarı kuralları gerekir. Ayrıca, tüm gelen trafiği hello güvenlik hizmeti genel IP adresi karşılaşır (farklı bağlantı noktalarını), toobe hello güvenlik duvarı tarafından işlenir. Toodiagram hello mantıksal akışları hello alt ağları ve güvenlik duvarı kuralları tooavoid olacak yeniden çalışma ihtimalinden daha sonra ayarlama önce bir en iyi uygulamadır. Hello aşağıdaki şekilde hello güvenlik duvarı kuralları bu örnek için mantıksal bir görünümünü gösterilmiştir:

![Mantıksal görünümünü hello güvenlik duvarı kuralları][2]

> [!NOTE]
> Ağ sanal gereç kullanılan hello üzerinde bağlı olarak, hello yönetim bağlantı noktalarını değişir. Barracuda NextGen Firewall başvurulan Bu örnekte, bağlantı noktası 22, 801 ve 807 kullanır. Lütfen kullanılan hello aygıt yönetimi için kullanılan hello Gereci satıcı belgelerine toofind hello tam bağlantı noktalarını bakın.
> 
> 

### <a name="logical-rule-description"></a>Mantıksal kural açıklaması
Merhaba mantıksal Yukarıdaki diyagramda, hello güvenlik duvarı hello yalnızca o alt ağdaki kaynaktır ve bu diyagramda hello güvenlik duvarı kuralları ve nasıl mantıksal olarak izin ver veya Reddet trafik akışına ve hello gerçek yönlendirilmiş yol değil gösteren hello güvenlik alt ağ gösterilmez. Ayrıca, daha kolay okunabilir olması için yerel IP adresi hello iki sekizlisinin hello RDP trafiğine yüksek aralıklı bağlantı noktaları (8014 – 8026) olduğundan ve bundan seçili toosomewhat Hizala ile hello için seçilen hello dış bağlantı noktalarını en son (örneğin yerel sunucu adresi 10.0.1.4 ilişkili olduğu dış bağlantı noktası 8014), ancak daha yüksek herhangi çakışmayan bağlantı noktaları kullanılabilir.

Bu örnek için 7 tür kuralların ihtiyacımız, bu kural türleri aşağıda açıklanmıştır:

* Dış kuralları (için gelen trafiği):
  1. Güvenlik Duvarı Yönetimi kuralı: Bu uygulama yeniden yönlendirme kuralı hello ağ sanal gereç trafiği toopass toohello yönetim bağlantı noktaları sağlar.
  2. RDP kuralları (her windows server için): Bu dört kurallar (her sunucu için bir tane) hello Yönetimi tek tek sunucular RDP aracılığıyla izin verir. Bu ayrıca hello kullanılan ağ sanal gereç hello yeteneklerini bağlı olarak tek bir kural içine paketlenmiş.
  3. Uygulama trafiği kuralları: İki uygulama trafiği kuralları, hello hello ön uç web trafiği için ilk ve ikinci hello arka uç trafiği (örneğin web sunucusu toodata katmanı) için hello vardır. Bu kurallar Hello yapılandırmasını hello ağ mimarisi (sunucularınızı yerleştirildiği) ve (hangi yönde hello trafik akışlarının ve hangi bağlantı noktalarının kullanılacağını) trafiği akışı değişir.
     * Merhaba ilk kural hello gerçek uygulama trafiği tooreach hello uygulama sunucusu izin verir. Merhaba diğer kurallar izin verirken, güvenlik, yönetim, vb. için uygulama ne hello uygulamaları dış kullanıcı ve hizmet tooaccess izin kurallardır. Bu örnek için bağlantı noktası 80 üzerinde tek bir web sunucusu yoktur, böylece bir tek uygulama güvenlik duvarını gelen trafiği toohello dış IP, toohello web sunucuları iç IP adresi yönlendirir. Hello vardı NAT trafiği oturumu yeniden yönlendirilen toohello iç sunucu.
     * İkinci uygulama trafik kuralı hello herhangi bir bağlantı arka uç kural tooallow hello Web sunucusu tootalk toohello AppVM01 sunucu (ancak değil AppVM02) hello.
* İç kurallardan (içi-VNet trafiği)
  1. Giden tooInternet kuralı: Bu kural herhangi bir ağ trafiğinden toopass seçili toohello ağlar izin verir. Bu genellikle varsayılan bir kural zaten hello güvenlik duvarı, ancak devre dışı durumdayken kuralıdır. Bu kural, bu örnek için etkinleştirilmelidir.
  2. DNS kuralı: Bu kural yalnızca DNS (bağlantı noktası 53) trafiği toopass toohello DNS sunucusu sağlar. Merhaba ön uç toohello arka uç çoğu trafiğinden engellenen bu ortam için bu kural tüm yerel alt ağ üzerinden DNS özellikle sağlar.
  3. Alt ağ tooSubnet kuralı: herhangi bir sunucuda hello arka uç alt tooconnect tooany sunucusu hello ön uç alt ağdaki (ancak hello geriye doğru değil) tooallow bu kuralıdır.
* Yedek operatördür kuralı (yukarıdaki hello birini karşılamıyor trafiği):
  1. Tüm trafik kuralı Reddet: Bu her zaman son bir kural hello (bakımından öncelik) olmalıdır ve trafik akışlarına şekilde toomatch bu kural tarafından bırakılacak kuralları önceki hello hiçbirini başarısız olur. Bu varsayılan bir kural ve genellikle etkin, değişikliğe genellikle gereklidir.

> [!TIP]
> Merhaba ikinci uygulama trafik kuralı, herhangi bir bağlantı için bu örneği kolay izin verilir, gerçek senaryo hello bu kural, kullanılan tooreduce hello saldırı yüzeyini en belirli bağlantı noktasının ve adres aralıkları olmalıdır.
> 
> 

<br />

> [!IMPORTANT]
> Tüm kuralları yukarıda hello oluşturulduktan sonra tooreview hello her kural tooensure trafiğin önceliğini izin verilen veya istendiği gibi reddedilen önemlidir. Bu örnekte, hello öncelik sırasına göre kurallardır. Merhaba güvenlik duvarı kuralları toomis sipariş son dışında kilitli kolay toobe olur. En azından hello Yönetimi hello güvenlik duvarı kendisi için her zaman hello mutlak en yüksek öncelik kuralı olduğundan emin olun.
> 
> 

### <a name="rule-prerequisites"></a>Kural önkoşulları
Merhaba sanal makine çalışan hello Güvenlik Duvarı için önkoşul vardır ortak uç noktaları. Merhaba güvenlik duvarı tooprocess trafiği için hello uygun ortak bitiş noktalarının açık olması gerekir. Bu örnekte trafiğin üç tür vardır; 1) yönetim trafiğini toocontrol hello güvenlik duvarı ve güvenlik duvarı kuralları, 2) RDP trafiğine toocontrol hello windows sunucuları ve 3) uygulama trafiği. Merhaba üç sütun üst hello trafik türlerinin hello güvenlik duvarı kuralları mantıksal görünümünü yarısı bunlar.

> [!IMPORTANT]
> Burada anahtar takeway tooremember olduğundan, **tüm** trafiği hello güvenlik duvarı üzerinden gelen. Bunu tooremote Masaüstü toohello IIS01 sunucu, onu hello ön uç bulut hizmeti ve hello ön uç alt tooaccess tooRDP toohello güvenlik duvarı üzerinde ihtiyacımız bu sunucu olsa bile 8014 bağlantı noktası ve hello güvenlik duvarı tooroute hello RDP isteği dahili izin toohello IIS01 RDP bağlantı noktası. Merhaba "Azure portal'ın Bağlan düğmesini olduğu için hiçbir doğrudan RDP yolu tooIIS01 (Merhaba portal görebilirsiniz uzaklığa kadar) çalışmaz". Tüm bağlantılar yani hello Internet toohello güvenlik hizmeti ve bir bağlantı noktası, örneğin secscv001.cloudapp.net:xxxx (başvuru hello hello eşleme harici bağlantı noktası, iç IP ve bağlantı noktası diyagramı yukarıda) olacaktır.
> 
> 

Bir uç nokta hello zaman VM oluşturma ya da açılabilir veya yapı hello örnek komut dosyasında yapılan ve aşağıda bu kod parçacığında gösterildiği gibi post (Not; herhangi bir dolar işareti öğesi başlayarak (örn: $VMName[$i]) olan bir kullanıcı tanımlı değişken hello referen hello betikten Bu belgenin CE bölümü. köşeli ayraçlar [$i] "$i" Hello hello dizi sayısını VM'ler dizisindeki belirli bir VM'yi temsil eder):

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

Değişkenleri, ancak uç noktalar toohello kullanımı, son değil açıkça burada gösterilen ancak **yalnızca** hello güvenlik bulut hizmeti üzerinde açılır. Tüm gelen trafiği işlenir tooensure budur (yönlendirilmiş NAT bırakılan) hello güvenlik duvarı tarafından.

Bir yönetim istemcisi yüklü bir bilgisayar toomanage hello Güvenlik Duvarı'nı toobe gerekir ve gerekli hello yapılandırmaları oluşturun. Merhaba, Güvenlik Duvarı (veya diğer NVA) belgelerinden satıcı nasıl toomanage hello üzerinde aygıt bakın. Bu bölümde ve hello sonraki bölümde, güvenlik duvarı kuralları oluşturma, Hello kalanı hello hello güvenlik duvarı yapılandırmasını kendisini hello satıcılar Yönetimi istemcisi (yani hello Azure portal veya PowerShell) aracılığıyla anlatmaktadır.

İstemci Yükleme ve bağlantı toohello Bu örnekte kullanılan Barracuda için yönergeler şurada bulunabilir: [Barracuda NG yönetici](https://techlib.barracuda.com/NG61/NGAdmin)

Merhaba güvenlik duvarı üzerine ancak güvenlik duvarı kuralları oluşturmadan önce oturum sonra oluşturma hello kuralları kolaylaştırabilir iki önkoşul nesne sınıfları vardır; Ağ & hizmeti nesneleri.

Bu örnekte, üç adlandırılmış ağ nesneleri tanımlı (Merhaba Frontend alt ağı ve hello arka uç alt ağ, ayrıca hello hello DNS sunucusunun IP adresi için bir ağ nesnesi için bir) olmalıdır. Adlandırılmış ağ toocreate; Merhaba Barracuda NG yönetici istemci panodan başlayarak, toohello yapılandırma sekmesine gidin, hello işletimsel yapılandırma bölümü Ruleset, ardından "Ağlar" Merhaba güvenlik duvarı nesneleri menüsünün altında'ı tıklatın, ardından yeni hello Düzenle ağları menüde tıklatın. Merhaba ağ nesnesi artık, hello adını ve hello önekini ekleyerek oluşturulabilir:

![Bir ön uç ağ nesnesi oluşturun][3]

Bu hello FrontEnd alt ağı için bir adlandırılmış ağ oluşturur, benzer bir nesne de hello arka uç alt oluşturulmalıdır. Şimdi hello alt hello güvenlik duvarı kuralları ada göre daha kolay başvurulabilir.

Merhaba DNS sunucu nesnesi için:

![Bir DNS sunucusu nesnesi oluşturun][4]

Bu tek IP adresi başvurusu DNS kuralı hello belgenin devamındaki kullanılmadan.

Merhaba ikinci önkoşul nesneleri Hizmetleri nesneleridir. Bunlar, her sunucu için hello RDP bağlantı noktaları temsil eder. Merhaba varolan RDP hizmet nesnesi ilişkili toohello varsayılan RDP bağlantı noktası olduğundan, 3389, yeni hizmetler hello dış bağlantı noktalarından (8014-8026) tooallow trafiği oluşturulabilir. Merhaba yeni bağlantı noktaları ayrıca toohello varolan RDP hizmeti eklenemedi, ancak tanıtım kolaylığı için her sunucu için tek bir kuralı oluşturulabilir. bir sunucu için yeni bir RDP kural toocreate; Merhaba Barracuda NG yönetici istemci panodan başlangıç toohello yapılandırma sekmesine gidin, hello işletimsel yapılandırma bölümü Ruleset, tıklatın ardından hello güvenlik duvarı nesneleri menüsünde hello hizmetlerin listesini aşağı kaydırın altında "Hizmetler"'i tıklatın ve hello seçin "RDP" hizmet. Sağ tıklayın ve kopyalayın, sonra sağ tıklatın ve Yapıştır seçin. Düzenlenebilir bir RDP Copy1 hizmet nesnesi artık yok. RDP Copy1 sağ tıklayın ve Düzenle'yi seçin, hizmet penceresi aşağıda gösterildiği gibi açılır nesnesi Düzenle hello:

![Varsayılan RDP kuralı kopyası][5]

Merhaba değerler sonra düzenlenen toorepresent hello RDP hizmeti belirli bir sunucu olabilir. Varsayılan yukarıda AppVM01 hello için RDP kural değiştirilmiş tooreflect yeni bir hizmet adı, açıklama, olmalıdır ve dış RDP bağlantı noktası kullanılan hello Şekil 8 diyagramı (Not: hello bağlantı noktalarını hello RDP varsayılan bağlantı noktasının bu amaçla kullanılan 3389 toohello dış değiştirildi belirli AppVM01 hello dış bağlantı noktasının hello durumda sunucudur 8025) hello değiştirilmiş hizmeti aşağıda gösterilmiştir:

![AppVM01 kuralı][6]

Bu işlem, yinelenen toocreate sunucuları kalan hello için RDP Hizmetleri olmalıdır; AppVM02, DNS01 ve IIS01. Bu hizmetler Hello oluşturulmasını hello kural oluşturma daha basit ve daha belirgin hello sonraki bölümde hale getirir.

> [!NOTE]
> Bir RDP hizmeti hello Güvenlik Duvarı için iki nedenden dolayı gerekli değildir; 1) ilk hello güvenlik duvarı VM olduğu bir Linux tabanlı görüntüsü SSH bağlantı noktası 22 RDP ve 2) bağlantı noktası 22 yerine VM yönetimi için kullanılabilir ve diğer yönetim bağlantı noktalarına iki hello tooallow yönetim bağlantısı için aşağıda açıklanan ilk yönetim kuralında izin verilir.
> 
> 

### <a name="firewall-rules-creation"></a>Güvenlik duvarı kuralları oluşturma
Bu örnekte kullanılan güvenlik duvarı kuralları üç tür vardır, hepsinin ayrı simgeler vardır:

Merhaba uygulama yeniden yönlendirme kuralı: ![uygulama yeniden yönlendirme simgesi][7]

Merhaba hedef NAT kuralı: ![hedef NAT simgesi][8]

Merhaba geçişi kuralı: ![geçirmek simgesi][9]

Bu kural hakkında daha fazla bilgi hello Barracuda web sitesinde bulunabilir.

toocreate kuralları aşağıdaki hello (veya var olan varsayılan kuralları doğrulayın), hello Barracuda NG yönetici istemci panodan başlatma, toohello yapılandırma sekmesine gidin, hello işletimsel yapılandırma bölümü Ruleset'ı tıklatın. Bir kılavuz olarak adlandırılan, "Ana kuralları" Merhaba etkin ve devre dışı bırakılan kuralları bu Güvenlik Duvarı'nda mevcut gösterir. Merhaba sağ üst köşedeki bu kılavuz, küçük, yeşil olduğundan "+" düğmesini tıklatın, bu toocreate yeni bir kural tıklayın (Not: güvenlik duvarını "değişiklikleri kilitlenebilir", bir düğme "Kilit" olarak işaretlenmiş ve güncelleştirilemiyor toocreate olan veya kuralları düzenlemek, bu düğmeye tıkladığınızda görürseniz çok "kilidini" kural se hello t ve düzenlenmesine izin verilir). Mevcut bir kuralı tooedit istiyorsanız, o kural seçin, sağ tıklayın ve kuralını Düzenle seçin.

Kurallarınızı oluşturulan ve/veya değiştirilmiş sonra olmalıdırlar gönderilen toohello Güvenlik Duvarı'nı ve etkinleştirildi, bu değişiklikler değil kazanacak hello kural yapılmazsa. Merhaba itme ve etkinleştirme işlemi hello ayrıntıları kural açıklamaları açıklanmıştır.

Bu örnekte aşağıdaki gibi açıklanmıştır her kural gerekli toocomplete Hello özellikleri:

* **Güvenlik Duvarı yönetimi kural**: Bu uygulama yeniden yönlendirme kuralı trafiği hello ağ sanal gereç, bu örnekte Barracuda NextGen Firewall toopass toohello yönetim bağlantı noktaları sağlar. 801, 807 ve isteğe bağlı olarak 22 Hello yönetim bağlantı noktalarıdır. Merhaba iç ve dış bağlantı noktaları olan hello aynı (yani hiçbir bağlantı noktası çevirisi). Bu kural, Kurulum MGMT erişim, varsayılan bir kural ve varsayılan (olarak Barracuda NextGen Firewall sürüm 6.1) etkinleştirilmiş.
  
    ![Güvenlik Duvarı Yönetimi kuralı][10]

> [!TIP]
> Merhaba bu kuralın kaynak adres alanında herhangi, hello yönetim IP adres aralıklarını bilinen, bu kapsamı azaltma ayrıca hello saldırı yüzeyini toohello yönetim bağlantı noktalarını azaltmak.
> 
> 

* **RDP kuralları**: Bu hedef NAT kuralları tek tek sunucular RDP aracılığıyla hello yönetimini izin.
  Bu kural dört gereken kritik alanları toocreate vardır:
  
  1. Kaynak – tooallow RDP yerden hello başvurusu "Any" Merhaba kaynak alanında kullanılır.
  2. Merhaba dış bağlantı noktaları toohello sunucuları yerel IP adresi ve tooport 3386 (Merhaba varsayılan RDP bağlantı noktası) yeniden yönlendirme, hizmeti – uygun hizmeti nesnesi, bu durumda "AppVM01 RDP" daha önce oluşturduğunuz hello kullanın. RDP erişim tooAppVM01 için bu belirli kuralıdır.
  3. Hedef – hello olmalıdır *hello Güvenlik Duvarı'nda yerel bağlantı noktası*, "DCHP 1 yerel IP" ya da statik IP kullanıyorsanız eth0. Başlangıç sıra numarası (eth0, eth1, vb.), ağ Gereci birden çok yerel arabirimi varsa, farklı olabilir. Bu hello bağlantı noktasıdır hello güvenlik duvarı göndermesinin (olabilir aynı bağlantı noktasını almayı hello hello), hello gerçek yönlendirilmiş hedefi olan hello hedef listesinin alanında.
  4. Yeniden yönlendirme – Bu bölümde tooultimately bu trafiği burada yeniden yönlendirme hello sanal gereç söyler. Merhaba basit yeniden yönlendirme tooplace hello IP ve bağlantı noktası (isteğe bağlı) hello hedef liste alanda ' dir. Bağlantı noktası yok hello gelen istekte kullanılan hello hedef bağlantı noktası ise olacaktır (IE hiçbir çevirisi), bir bağlantı noktası başlangıç bağlantı noktası belirlendiyse kullanılan de NAT birlikte hello IP adresi olur.
     
     ![Güvenlik Duvarı RDP kuralı][11]
     
     Dört RDP kuralları toplam oluşturulan toobe gerekir: 
     
     | Kural Adı | Sunucu | Hizmet | Hedef listesi |
     | --- | --- | --- | --- |
     | RDP IIS01 |IIS01 |IIS01 RDP |10.0.1.4:3389 |
     | RDP DNS01 |DNS01 |DNS01 RDP |10.0.2.4:3389 |
     | RDP AppVM01 |AppVM01 |AppVM01 RDP |10.0.2.5:3389 |
     | RDP AppVM02 |AppVM02 |AppVm02 RDP |10.0.2.6:3389 |

> [!TIP]
> Merhaba kaynak Hello kapsamını ve hizmet alanları aşağı daraltma hello saldırı yüzeyini azaltır. işlevselliği sağlayacak en sınırlı hello kapsam kullanılmalıdır.
> 
> 

* **Uygulama trafik kurallarını**: iki uygulama trafiği kuralları, hello hello ön uç web trafiği için ilk ve ikinci hello arka uç trafiği (örneğin web sunucusu toodata katmanı) için hello vardır. Bu kurallar hello ağ mimarisi (sunucularınızı yerleştirildiği) ve (hangi yönde hello trafik akışlarının ve hangi bağlantı noktalarının kullanılacağını) trafiği akışı değişir.
  
    Önce ele alınan hello ön uç web trafiği için kuraldır:
  
    ![Güvenlik Duvarı Web kuralı][12]
  
    Bu hedef NAT kuralı hello gerçek uygulama trafiği tooreach hello uygulama sunucusu sağlar. Merhaba diğer kurallar izin verirken, güvenlik, yönetim, vb. için uygulama ne hello uygulamaları dış kullanıcı ve hizmet tooaccess izin kurallardır. Bu örnek için bağlantı noktası 80 üzerinde bir tek bir web sunucusu olduğundan, böylece hello tek uygulama güvenlik duvarını gelen trafiği toohello dış IP, toohello web sunucuları iç IP adresi yönlendirir.
  
    **Not**: hello hedef listesi alanına atanan bağlantı noktası yok, bu nedenle hello gelen bağlantı noktası 80 (veya hello seçili hizmet için 443'tür) hello web sunucusu hello yönlendirilmesini kullanılacak. Merhaba web sunucusunun farklı bir bağlantı noktasında dinleme, örneğin 8080 bağlantı noktası, hello hedef listesi alan güncelleştirilmiş too10.0.1.4:8080 tooallow hello bağlantı noktası yeniden yönlendirmesi için de olabilir.
  
    sonraki uygulama trafik kuralı hello herhangi bir hizmeti arka uç kural tooallow hello Web sunucusu tootalk toohello AppVM01 sunucu (ancak değil AppVM02) hello:
  
    ![Güvenlik Duvarı AppVM01 kuralı][13]
  
    Bu geçiş kuralı hello web uygulama tarafından gerek duyulan tüm Protokolü tooaccess verileri kullanarak tüm IIS sunucusunda hello ön uç alt tooreach hello AppVM01 (IP adresi 10.0.2.5) herhangi bir bağlantı noktasında verir.
  
    Bu ekran görüntüsü, bir "\<taşınmaya açık\>" Merhaba hedef alan toosignify 10.0.2.5 hello hedef olarak kullanılır. Bu şunlardan biri olabilir gösterildiği gibi veya açık adlı ağ (Merhaba DNS sunucusu hello önkoşulları içinde'da yapıldığı gibi) nesnesi. Toowhich yöntemi kullanılacağından bu toohello hello Güvenlik Duvarı'nın yöneticisidir. tooadd Explict Desitnation olarak 10.0.2.5 çift hello ilk boş satır altında \<taşınmaya açık\> ve açılır hello penceresinde hello adresini girin.
  
    Böylece Hello bağlantı yöntemini çok ayarlayabilirsiniz bu dahili trafiği olduğundan geçirmek bu kural, NAT gerekli "No SNAT".
  
    **Not**: hello kaynak bu kuralda ağdır hello FrontEnd alt ağı üzerinde herhangi bir kaynak yalnızca olacaktır bir veya daha belirli toothose tam IP adreslerinin yerine web sunucuları, kaynak olabilir bir ağ nesnesi bilinen belirli sayıda oluşturduysanız toobe ön uç alt ağın tamamını Hello.

> [!TIP]
> Bu kural "Tüm" toomake örnek uygulama daha kolay toosetup hello ve kullanmak hello hizmeti kullanıyorsa, bu da Icmpv4 izin verir (ping) tek bir kural. Ancak, önerilen bir uygulama değildir. Merhaba bağlantı noktalarını ve protokolleri ("Hizmetler") bu sınırından uygulama işlemi tooreduce hello saldırı yüzeyini veren daraltılmış toohello minimum mümkün olması gerekir.
> 
> 

<br />

> [!TIP]
> Bu kural kullanılan bir hedef açık başvuru gösterir, ancak hello güvenlik duvarı yapılandırmasını tutarlı bir yaklaşım kullanılmalıdır. Ağ nesnesi adlı bu hello kullanılabilir boyunca daha kolay okunabilir olması ve desteklenebilirlik için önerilir. Merhaba açık taşınmaya kullanılan burada yalnızca tooshow bir alternatif başvuru yöntemidir ve (özellikle karmaşık yapılandırmalar için) genellikle önerilmez.
> 
> 

* **Giden tooInternet kural**: Bu geçirmek kuralı izin ver hiçbir kaynak ağ toopass toohello seçili hedef ağ trafiği. Bu kural hello Barracuda NextGen Güvenlik Duvarı'nda genellikle zaten varsayılan kural, ancak devre dışı durumda. Bu kurala sağ hello etkinleştirme kural komutu erişebilirsiniz. Burada gösterilen hello kural hello önkoşul bölüm bu kural, bu belge toohello kaynak özniteliğinin başvurular olarak oluşturulan değiştirilmiş tooadd hello iki yerel alt ağları olmuştur.
  
    ![Giden güvenlik duvarı kuralı][14]
* **DNS kuralı**: Bu geçirmek kural yalnızca DNS (bağlantı noktası 53) trafiği toopass toohello DNS sunucusu izin verir. Bu kural, hello ön uç toohello arka uç çoğu trafiğinden engellenen bu ortam için DNS özellikle sağlar.
  
    ![Güvenlik Duvarı DNS kuralı][15]
  
    **Not**: Bu ekran görüntüsü hello bağlantı yöntemini bulunur. Bu kural iç IP toointernal IP adresi trafiği için olduğundan, hiçbir NATing gerekli değildir, bu hello bağlantı yönteminin çok ayarlandığını bu geçişi kuralı için "Hayır SNAT".
* **Alt ağ tooSubnet kural**: Bu geçirmek etkinleştirildi varsayılan bir kural kuralıdır ve herhangi bir sunucuya geri hello uç alt tooconnect tooany sunucusu üzerinde değiştirilmiş tooallow hello ön uç alt. Bu kural tüm iç trafiği olduğundan Hello bağlantı yöntemini tooNo SNAT ayarlanabilir.
  
    ![Güvenlik Duvarı içi sanal ağ kuralı][16]
  
    **Not**: hello çift yönlü onay kutusu işaretli (veya, çoğu kurallarında işaretli değil), bu "tek yönlü" kural sağlar, bu kural için önemli budur, bir bağlantı hello arka uç alt toohello ön uç ağ üzerinden başlatılabilir ancak ters hello değil. Bu onay kutusu işaretli değilse bu kural bizim mantıksal diyagramdan istenmediği çift yönlü trafiği etkinleştirir.
* **Reddetme tüm trafik kuralı**: Bu her zaman son bir kural hello (bakımından öncelik) olmalıdır ve trafik başarısız toomatch kuralları önceki hello hiçbirini akışlar, bu nedenle, bu kural tarafından düşürülür. Bu varsayılan bir kural ve genellikle etkin, değişikliğe genellikle gereklidir. 
  
    ![Güvenlik duvarı kuralı Reddet][17]

> [!IMPORTANT]
> Tüm kuralları yukarıda hello oluşturulduktan sonra tooreview hello her kural tooensure trafiğin önceliğini izin verilen veya istendiği gibi reddedilen önemlidir. Bu örnekte, hello hello hello Barracuda Management istemcisi kurallarında iletme, ana kılavuz görüntülenmelidir hello sırayla kurallardır.
> 
> 

## <a name="rule-activation"></a>Kural etkinleştirme
Merhaba değiştiren ruleset toohello belirtimiyle hello mantığı diyagramı, hello ruleset olmalıdır toohello Güvenlik Duvarı'nı karşıya ve ardından etkinleştirildi.

![Güvenlik duvarı kuralını etkinleştirme][18]

Merhaba üst sağ köşesinde hello management istemcisi düğmeleri oluşan bir küme var. Merhaba "değişiklikleri" Gönder düğmesi toosend değiştiren hello kuralları toohello güvenlik duvarı, ardından hello "Etkinleştir" düğmesini tıklatın.

Merhaba güvenlik duvarı ruleset Hello etkinleştirme ile bu örnek ortamı yapı tamamlanır.

## <a name="traffic-scenarios"></a>Trafik senaryoları
> [!IMPORTANT]
> Bir anahtar takeway tooremember olduğundan, **tüm** trafiği hello güvenlik duvarı üzerinden gelen. Bunu tooremote Masaüstü toohello IIS01 sunucu, onu hello ön uç bulut hizmeti ve hello ön uç alt tooaccess tooRDP toohello güvenlik duvarı üzerinde ihtiyacımız bu sunucu olsa bile 8014 bağlantı noktası ve hello güvenlik duvarı tooroute hello RDP isteği dahili izin toohello IIS01 RDP bağlantı noktası. Merhaba "Azure portal'ın Bağlan düğmesini olduğu için hiçbir doğrudan RDP yolu tooIIS01 (Merhaba portal görebilirsiniz uzaklığa kadar) çalışmaz". Tüm bağlantılar yani hello Internet toohello güvenlik hizmeti ve bir bağlantı noktası, örneğin secscv001.cloudapp.net:xxxx olacaktır.
> 
> 

Bu senaryolarda, güvenlik duvarı kuralları aşağıdaki hello yerinde olmalıdır:

1. Güvenlik Duvarı Yönetimi
2. RDP tooIIS01
3. RDP tooDNS01
4. RDP tooAppVM01
5. RDP tooAppVM02
6. Web uygulaması trafiği toohello
7. Uygulama trafiği tooAppVM01
8. Giden toohello Internet
9. Ön uç tooDNS01
10. İçi alt ağ trafiği (yalnızca arka uç toofront ucu)
11. Tümünü Reddet

Hello gerçek güvenlik duvarı ruleset, büyük olasılıkla başka birçok kurala toplama toothese vardır, olanları burada listelenen hello daha hello kurallarında belirtilen herhangi bir güvenlik duvarını ayrıca farklı öncelik numaraları gerekir. Bu liste ve ilişkili numaralar yalnızca bu on kurallar ve bunları arasında hello göreli öncelik arasında tooprovide ilgi markalarıdır. Diğer bir deyişle; Merhaba gerçek Güvenlik Duvarı'nı, kural numarası 5 olabilir, ancak hello "Güvenlik duvarı Yönetimi" kural altında ve bu listeyi hello amacı ile hizalamaya hello "RDP tooDNS01" kural üstünde olduğu sürece hello "RDP tooIIS01" olabilir. Başlangıç listesi, büyük bir de kısaltma izin vererek senaryolar aşağıda hello yardımcı olur; Örneğin "FW kuralı 9 (DNS)". Ayrıca okumanızdır dört RDP kuralları topluca olacaktır hello olarak adlandırılan, "RDP kuralları hello" Merhaba trafik senaryo ilgisiz tooRDP olduğunda.

Ağ güvenlik grupları yerinde gelen Internet trafiği hello ön uç ve arka uç alt ağları olduğunu da geri çağırma.

#### <a name="allowed-internet-tooweb-server"></a>(İzin verilir) Internet tooWeb sunucu
1. Internet kullanıcı istekleri HTTP sayfasına SecSvc001.CloudApp.Net (Internet'e yönelik bulut hizmeti)
2. Bulut hizmeti geçiş trafiği 80 numaralı bağlantı noktasını toofirewall arabirimde 10.0.0.4:80 açık uç noktası aracılığıyla
3. Sistem NSG kuralları trafiği toofirewall izin verecek şekilde tooSecurity alt ağ, hiçbir NSG atanan
4. Merhaba Güvenlik Duvarı (10.0.1.4) iç IP adresi trafik isabetler
5. Güvenlik duvarı kuralı işleme başlar:
   1. FW kural 1'i (FW Mgmt) uygulanmaz, taşıma toonext kuralı
   2. FW kuralları 2-5 (RDP kurallar) yok, uygulama toonext kuralı Taşı
   3. FW kural 6 (uygulama: Web) uygulama trafiğine izin verilir, güvenlik duvarı NAT onu too10.0.1.4 (IIS01)
6. Merhaba ön uç alt gelen kuralı işleme başlar:
   1. Olmayan NSG kural 1'i (blok Internet) uygulama (Bu trafiği NAT edildi hello güvenlik duvarı tarafından gerekir, böylece hello kaynak adresi şimdi hello güvenlik alt ağ üzerinde olan hello güvenlik duvarı ve hello ön uç alt ağa göre NSG toobe "yerel" trafik görülen ve böylece izin verilir), toonext kuralı Taşı
   2. Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur
7. IIS01 web trafiği için dinleme, bu isteği alır ve hello isteği işlemeye başlıyor
8. Arka uç alt ağdaki bir FTP oturumunun tooAppVM01 tooinitiates IIS01 çalışır
9. ön uç alt ağdaki Hello UDR rota hello güvenlik duvarı hello sonraki atlama yapar
10. Ön uç alt ağdaki hiçbir giden kuralları, trafiğe izin verilir
11. Güvenlik duvarı kuralı işleme başlar:
    1. FW kural 1'i (FW Mgmt) uygulanmaz, taşıma toonext kuralı
    2. FW kuralı 2-5 (RDP kurallar) uygulanmaz, taşıma toonext kuralı
    3. FW kural 6 (uygulama: Web) uygulamak için değil, toonext kuralı Taşı
    4. FW kural 7 ' (uygulama: arka uç) uygulama trafiğine izin verilir, güvenlik duvarı iletir trafiği too10.0.2.5 (AppVM01)
12. Merhaba arka uç alt gelen kuralı işleme başlar:
    1. NSG kural 1'i (blok Internet) uygulanmaz, taşıma toonext kuralı
    2. Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur
13. AppVM01 hello isteği alır ve hello oturumu başlatır ve yanıtlar
14. arka uç alt ağdaki Hello UDR rota hello güvenlik duvarı hello sonraki atlama yapar
15. Olduğundan giden hiçbir NSG kuralları hello arka uç alt hello yanıt üzerinde izin verilir
16. Bu trafik üzerinde döndürüyor çünkü kurulan oturum hello güvenlik duvarı hello yanıt geri toohello web sunucusu (IIS01) geçirir.
17. Ön uç alt gelen kuralı işleme başlar:
    1. NSG kural 1'i (blok Internet) uygulanmaz, taşıma toonext kuralı
    2. Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur
18. Hello IIS sunucusu hello yanıtı alır, AppVM01 hello işlemle tamamlar ve yapı hello HTTP yanıtı tamamlandıktan, toohello istek sahibi gönderilen bu HTTP yanıtı
19. Olduğundan giden hiçbir NSG kuralları hello ön uç alt hello yanıt üzerinde izin verilir
20. HTTP yanıt isabet hello güvenlik duvarı hello ve bu hello yanıt tooan kurulmuş olduğundan NAT oturum hello güvenlik duvarı tarafından kabul edilir
21. Merhaba güvenlik duvarı hello yanıt geri toohello Internet kullanıcı ardından yönlendirir.
22. Hiçbir giden NSG kuralları veya UDR atlama olduğundan hello ön uç alt ağda hello yanıt izin verilir ve hello web sayfasının hello Internet kullanıcı alır.

#### <a name="allowed-internet-rdp-toobackend"></a>(İzin verilir) Internet RDP tooBackend
1. Sunucu Yöneticisi Internet üzerinde RDP oturumu tooAppVM01 8025 hello "RDP tooAppVM01" güvenlik duvarı kuralı için hello kullanıcıya atanan bağlantı noktası numarası olduğu SecSvc001.CloudApp.Net:8025 aracılığıyla istekleri
2. Hello bulut hizmeti, bağlantı noktası 8025 toofirewall 10.0.0.4:8025 arabirimde üzerinde hello açık uç noktası üzerinden trafiğe geçirir.
3. Sistem NSG kuralları trafiği toofirewall izin verecek şekilde tooSecurity alt ağ, hiçbir NSG atanan
4. Güvenlik duvarı kuralı işleme başlar:
   1. FW kural 1'i (FW Mgmt) uygulanmaz, taşıma toonext kuralı
   2. FW Kural 2 (RDP IIS) için geçerli değildir, taşıma toonext kuralı
   3. FW kuralı 3 (RDP DNS01) değil, uygulama toonext kuralı Taşı
   4. FW kuralı 4 (RDP AppVM01) uygulamak için trafik verilir, güvenlik duvarı NAT onu too10.0.2.5:3386 (AppVM01 üzerinde RDP noktasına)
5. Merhaba arka uç alt gelen kuralı işleme başlar:
   1. Olmayan NSG kural 1'i (blok Internet) uygulama (Bu trafiği NAT edildi hello güvenlik duvarı tarafından gerekir, böylece hello kaynak adresi şimdi hello güvenlik alt ağ üzerinde olan hello güvenlik duvarı ve hello arka uç alt ağa göre NSG toobe "yerel" trafik görülen ve böylece izin verilir), toonext kuralı Taşı
   2. Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur
6. AppVM01 RDP trafiği için dinleme ve yanıtlar
7. Giden hiçbir NSG kuralları, varsayılan kuralları uygula ve dönüş trafiğine izin verilir
8. UDR giden trafiği toohello güvenlik duvarı hello sonraki atlama olarak yönlendirir.
9. Bu trafik üzerinde döndürüyor çünkü kurulan oturum hello güvenlik duvarı hello yanıt geri toohello Internet kullanıcı geçirir.
10. RDP oturumu etkin
11. Kullanıcı adı ve parolasını AppVM01 ister

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(İzin verilir) DNS sunucusundaki Web sunucusu DNS araması
1. Sunucu, IIS01, gereksinimlerini www.data.gov bir veri akışı web ancak tooresolve adresi hello.
2. Merhaba ağ yapılandırma hello VNet listeleri DNS01 (10.0.2.4 hello arka uç alt ağdaki) hello birincil DNS sunucusu olarak, IIS01 hello DNS isteği tooDNS01 gönderir
3. UDR giden trafiği toohello güvenlik duvarı hello sonraki atlama olarak yönlendirir.
4. Giden hiçbir NSG kuralları ilişkili toohello Frontend alt ağı olan, trafiğe izin verilir
5. Güvenlik duvarı kuralı işleme başlar:
   1. FW kural 1'i (FW Mgmt) uygulanmaz, taşıma toonext kuralı
   2. FW kuralı 2-5 (RDP kurallar) uygulanmaz, taşıma toonext kuralı
   3. FW kuralları 6 ve 7 (uygulama kuralları) uygulama, taşıma toonext kuralı
   4. FW kural 8 (tooInternet) değil, uygulama toonext kuralı Taşı
   5. FW kural 9 (DNS) geçerli, trafiğe izin verilir, güvenlik duvarı trafiği too10.0.2.4 (DNS01) iletir
6. Merhaba arka uç alt gelen kuralı işleme başlar:
   1. NSG kural 1'i (blok Internet) uygulanmaz, taşıma toonext kuralı
   2. Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur
7. DNS sunucusu hello isteği alır
8. DNS sunucusu önbelleğe hello adresi yoksa ve bir kök DNS sunucusu üzerinde hello ister Internet
9. UDR giden trafiği toohello güvenlik duvarı hello sonraki atlama olarak yönlendirir.
10. Giden hiçbir NSG kuralları arka uç alt ağdaki trafiğe izin verilir
11. Güvenlik duvarı kuralı işleme başlar:
    1. FW kural 1'i (FW Mgmt) uygulanmaz, taşıma toonext kuralı
    2. FW kuralı 2-5 (RDP kurallar) uygulanmaz, taşıma toonext kuralı
    3. FW kuralları 6 ve 7 (uygulama kuralları) uygulama, taşıma toonext kuralı
    4. FW kural 8 (tooInternet) geçerli, trafiğe izin verilir, oturum SNAT hello Internet DNS sunucusunda tooroot çıkışı
12. Bu oturumda hello Güvenlik Duvarı'ndan başlatılan olduğundan, Internet DNS sunucusu yanıt, hello yanıt hello güvenlik duvarı tarafından kabul edilir
13. Yerleşik bir oturum olarak hello güvenlik duvarı sunucusu, DNS01 başlatma hello yanıt toohello iletir.
14. Merhaba arka uç alt gelen kuralı işleme başlar:
    1. NSG kural 1'i (blok Internet) uygulanmaz, taşıma toonext kuralı
    2. Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur
15. Merhaba DNS sunucusu ve hello yanıtı önbelleğe alır ve toohello ilk isteği geri tooIIS01 yanıt verir
16. arka uç alt ağdaki Hello UDR rota hello güvenlik duvarı hello sonraki atlama yapar
17. Giden hiçbir NSG kuralları hello arka uç alt ağda var, trafiğe izin verilir
18. Bu yerleşik bir oturum hello Güvenlik Duvarı'nda, hello yanıt hello Güvenlik Duvarı'nı geri toohello IIS sunucu tarafından iletilen
19. Ön uç alt gelen kuralı işleme başlar:
    1. Merhaba NSG kuralları hiçbiri geçerli şekilde hello arka uç alt toohello ön uç alt ağından tooInbound trafiği uygulayan NSG kural yok
    2. Merhaba trafiğe izin şekilde hello varsayılan sistem kuralı alt ağlar arasında trafiğe izin vermek bu trafiği olanak tanır
20. IIS01 hello yanıt DNS01 alır.

#### <a name="allowed-backend-server-toofrontend-server"></a>(İzin verilir) Arka uç sunucusu tooFrontend
1. Windows dosya Gezgini üzerinden hello IIS01 sunucu doğrudan bir dosya tooAppVM02 RDP aracılığıyla oturum açmış bir yönetici istekleri
2. arka uç alt ağdaki Hello UDR rota hello güvenlik duvarı hello sonraki atlama yapar
3. Olduğundan giden hiçbir NSG kuralları hello arka uç alt hello yanıt üzerinde izin verilir
4. Güvenlik duvarı kuralı işleme başlar:
   1. FW kural 1'i (FW Mgmt) uygulanmaz, taşıma toonext kuralı
   2. FW kuralı 2-5 (RDP kurallar) uygulanmaz, taşıma toonext kuralı
   3. FW kuralları 6 ve 7 (uygulama kuralları) uygulama, taşıma toonext kuralı
   4. FW kural 8 (tooInternet) değil, uygulama toonext kuralı Taşı
   5. FW kural 9 (DNS) uygulanmaz, taşıma toonext kuralı
   6. FW kural 10 (içi alt ağ) geçerli, trafiğe izin verilir, güvenlik duvarı trafiği too10.0.1.4 (IIS01) geçirir
5. Ön uç alt gelen kuralı işleme başlar:
   1. NSG kural 1'i (blok Internet) uygulanmaz, taşıma toonext kuralı
   2. Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur
6. Uygun kimlik doğrulama ve yetkilendirme varsayıldığında, IIS01 hello isteği kabul eder ve yanıtlar
7. ön uç alt ağdaki Hello UDR rota hello güvenlik duvarı hello sonraki atlama yapar
8. Olduğundan giden hiçbir NSG kuralları hello ön uç alt hello yanıt üzerinde izin verilir
9. Bu hello Güvenlik Duvarı'nda var olan bir oturum olarak bu yanıt izin verilir ve hello güvenlik duvarı hello yanıt tooAppVM02 döndürür
10. Arka uç alt gelen kuralı işleme başlar:
    1. NSG kural 1'i (blok Internet) uygulanmaz, taşıma toonext kuralı
    2. Varsayılan NSG kuralları alt toosubnet trafiğe izin verecek, trafiğe izin verilir, NSG kuralının işlenmesi Durdur
11. AppVM02 hello yanıtı alır

#### <a name="denied-internet-direct-tooweb-server"></a>(Reddedildi) Internet doğrudan tooWeb sunucu
1. Internet kullanıcı tooaccess hello web sunucusu, IIS01, hello FrontEnd001.CloudApp.Net hizmeti ile çalışır
2. HTTP trafiği için açık uç nokta yok olduğundan bu hello bulut hizmeti geçip geçmeyeceğini değil ve hello sunucusuna ulaşabilir olmayacaktır
3. Hello NSG (blok Internet) hello ön uç alt ağdaki Hello uç noktaları için herhangi bir nedenle açıksa, bu trafiği engeller
4. Son olarak, hello ön uç alt UDR rota hello sonraki atlama olarak IIS01 toohello Güvenlik Duvarı'ndan tüm giden trafiği gönderebilir ve hello Güvenlik Duvarı'nı bu asimetrik trafiği olarak görebilir ve hello giden yanıt en az üç bağımsız katmanı vardır nedenle bırakma Merhaba arasında yetkisiz/uygunsuz erişimi engelleme kendi bulut hizmeti Internet ve IIS01 yolu.

#### <a name="denied-internet-toobackend-server"></a>(Reddedildi) Internet tooBackend sunucu
1. Internet kullanıcı tooaccess AppVM01 bir dosyada hello BackEnd001.CloudApp.Net hizmeti ile çalışır
2. Dosya Paylaşımı için açık uç nokta yok olduğundan bu hello bulut hizmeti geçip geçmeyeceğini değil ve hello sunucusuna ulaşabilir olmayacaktır
3. Herhangi bir nedenden dolayı Hello uç noktaları açıksa hello NSG (blok Internet) bu trafiği engeller
4. Son olarak, hello UDR rota hello sonraki atlama olarak AppVM01 toohello Güvenlik Duvarı'ndan tüm giden trafiği gönderebilir ve hello Güvenlik Duvarı'nı bu asimetrik trafiği olarak görebilir ve hello giden yanıt en az üç bağımsız katmanlar arasında savunma vardır nedenle bırakma Internet ve AppVM01 yetkisiz/uygunsuz erişimi engelleme kendi bulut hizmeti ile Merhaba.

#### <a name="denied-frontend-server-toobackend-server"></a>(Reddedildi) Ön uç sunucusu tooBackend sunucu
1. IIS01 aşılmış ve kötü amaçlı kod tooscan hello arka uç sunucuları alt çalışırken çalıştığını varsayar.
2. Merhaba ön uç alt UDR rota tüm giden trafiği IIS01 toohello Güvenlik Duvarı'nı hello sonraki atlama olarak gönderebilir. Bu tarafından değiştirilmiş bir şey değil hello tehlikeye VM.
3. Hello isteği tooAppVM01 veya trafiği hello Güvenlik Duvarı'nı (son tooFW kuralları 7 ve 9) tarafından izin verilebilir DNS araması için toohello DNS sunucusu olduğunda hello güvenlik duvarı hello trafiği işleme. Diğer tüm trafik FW kural 11 göre (tüm reddetme) engellenebilir.
4. Tehdit algılama Gelişmiş hello güvenlik duvarı etkinleştirildi (da değil kapsanan bu belgede, Gelişmiş tehdit özellikleri, belirli bir ağ Gereci hello satıcı belgelerine bakın), hatta tarafından hello kuralları iletme temel izin trafiği Bu konuda ele alınan belge engelledi hello trafiği bilinen imzaları ya da bir Gelişmiş tehdit kuralı bayrak desenler içeriyorsa.

#### <a name="denied-internet-dns-lookup-on-dns-server"></a>(Reddedildi) DNS sunucusunda Internet DNS araması
1. Internet kullanıcı toolookup DNS01 BackEnd001.CloudApp.Net hizmeti aracılığıyla bir iç DNS kaydını çalışır 
2. DNS trafiği için açık uç nokta yok olduğundan bu hello bulut hizmeti geçip geçmeyeceğini değil ve hello sunucusuna ulaşabilir olmayacaktır
3. Herhangi bir nedenden dolayı Hello uç noktaları açıksa hello ön uç alt ağdaki hello NSG kuralının (blok Internet) bu trafiği engeller
4. Son olarak, hello arka uç alt UDR rota hello sonraki atlama olarak DNS01 toohello Güvenlik Duvarı'ndan tüm giden trafiği gönderebilir ve hello Güvenlik Duvarı'nı bu asimetrik trafiği olarak görebilir ve hello giden yanıt en az üç bağımsız katmanı vardır nedenle bırakma Merhaba arasında yetkisiz/uygunsuz erişimi engelleme kendi bulut hizmeti Internet ve DNS01 yolu.

#### <a name="denied-internet-toosql-access-through-firewall"></a>(Reddedildi) Güvenlik Duvarı üzerinden Internet tooSQL erişimi
1. Internet kullanıcı SQL verileri SecSvc001.CloudApp.Net (Internet'e yönelik bulut hizmeti) ' ister.
2. SQL için açık uç nokta yok olduğundan bu hello bulut hizmeti geçip geçmeyeceğini değil ve hello güvenlik duvarı ulaşmak olmayacaktır
3. Herhangi bir nedenden dolayı SQL uç noktaları açıksa hello güvenlik duvarı kuralı işlemeye başlamak:
   1. FW kural 1'i (FW Mgmt) uygulanmaz, taşıma toonext kuralı
   2. FW kuralları 2-5 (RDP kurallar) yok, uygulama toonext kuralı Taşı
   3. FW kural 6 ve 7 (uygulama kuralları) uygulama, taşıma toonext kuralı
   4. FW kural 8 (tooInternet) değil, uygulama toonext kuralı Taşı
   5. FW kural 9 (DNS) uygulanmaz, taşıma toonext kuralı
   6. FW kural 10 (içi alt ağ) değil, uygulama toonext kuralı Taşı
   7. FW kural 11 (Tümünü Reddet) geçerli, engellenmiş, Dur kural işlenirken trafiğidir

## <a name="references"></a>Başvurular
### <a name="main-script-and-network-config"></a>Ana komut dosyası ve ağ yapılandırması
Merhaba tam komut dosyası bir PowerShell komut dosyası kaydedin. Merhaba ağ yapılandırma "NetworkConf2.xml" adlı bir dosyaya kaydedin.
Merhaba kullanıcı tanımlı değişkenleri gerektiği gibi değiştirin. Merhaba komut dosyasını çalıştırın, ardından hello güvenlik duvarı kuralı kurulum yönergeleri yukarıdaki izleyin.

#### <a name="full-script"></a>Tam komut dosyası
Merhaba kullanıcı tanımlı değişkenleri esas alarak bu betiği olur:

1. Tooan Azure aboneliğine bağlanma
2. Yeni depolama hesabı oluşturma
3. Yeni bir VNet ve hello ağ yapılandırma dosyasında tanımlanan üç alt ağlar oluşturun
4. Beş sanal makineler oluşturun; Güvenlik Duvarı'nı 1 ve 4 windows server Vm'leri
5. UDR dahil olmak üzere yapılandırın:
   1. İki yeni yönlendirme tabloları oluşturma
   2. Yollar toohello tabloları ekleyin
   3. Tablolar tooappropriate alt ağları bağlama
6. IP iletimi NVA hello üzerinde etkinleştir
7. NSG dahil olmak üzere yapılandırın:
   1. Bir NSG oluşturma
   2. Bir kural ekleme
   3. Merhaba NSG toohello uygun alt ağları bağlama

Bu PowerShell Betiği, bir bilgisayar veya sunucu, Internet'e yerel olarak çalıştırılmalıdır.

> [!IMPORTANT]
> Bu komut dosyasını çalıştırdığınızda, uyarı veya PowerShell'de pop diğer bilgilendirici iletileri olabilir. Yalnızca hata iletileri kırmızı sorunu nedeni edilir.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

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
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

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

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

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
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
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
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
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
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
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
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Çift yönlü DMZ NVA, NSG ve UDR"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Mantıksal görünümünü hello güvenlik duvarı kuralları"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Bir ön uç ağ nesnesi oluşturun"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Bir DNS sunucusu nesnesi oluşturun"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Varsayılan RDP kuralı kopyası"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "AppVM01 kuralı"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Uygulama yeniden yönlendirme simgesi"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Hedef NAT simgesi"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Geçişi simgesi"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Güvenlik Duvarı Yönetimi kuralı"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Güvenlik Duvarı RDP kuralı"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Güvenlik Duvarı Web kuralı"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Güvenlik Duvarı AppVM01 kuralı"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Giden güvenlik duvarı kuralı"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Güvenlik Duvarı DNS kuralı"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Güvenlik Duvarı içi sanal ağ kuralı"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Güvenlik duvarı kuralı Reddet"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Güvenlik duvarı kuralını etkinleştirme"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
