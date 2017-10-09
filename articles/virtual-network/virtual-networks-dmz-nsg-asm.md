---
title: "aaaAzure DMZ örnek – yapı Nsg'ler ile basit DMZ | Microsoft Docs"
description: "Bir çevre ağ güvenlik grupları (NSG) ile derleme"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a>Örnek 1 – Nsg'ler ile klasik PowerShell kullanarak basit bir DMZ derleme
[Dönüş toohello güvenlik sınırı en iyi uygulamalar sayfası][HOME]

> [!div class="op_single_selector"]
> * [Resource Manager Şablonu](virtual-networks-dmz-nsg.md)
> * [Klasik - PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

Bu örnekte basit DMZ dört Windows sunucuları ve ağ güvenlik grupları oluşturulur. Bu örnek hello ilgili PowerShell komutları tooprovide her adımın daha derin bir anlayış açıklar. Ayrıca vardır bir trafik senaryo bölüm tooprovide ayrıntılı bir adım adım derinlemesine savunma hello katmanları üzerinden trafik geçer nasıl DMZ hello. Son olarak, hello references bölümünde hello tam kod ve yönerge toobuild bu ortam tootest çeşitli senaryoları ile deneme ise. 

![NSG ile giriş DMZ][1]

## <a name="environment-description"></a>Ortam açıklaması
Bu örnekte, abonelik kaynakları aşağıdaki hello içerir:

* İki bulut hizmetlerini: "FrontEnd001" ve "BackEnd001"
* Sanal ağ, "CorpNetwork" iki alt ağı; "Ön uç" ve "Arka uç"
* Uygulanan tooboth alt ağıdır bir ağ güvenlik grubu
* Uygulama web sunucusu ("IIS01") temsil eden bir Windows sunucusu
* Uygulama arka uç sunucuları ("AppVM01", "AppVM02") temsil eden iki windows sunucuları
* Bir DNS sunucusu ("DNS01") temsil eden bir Windows sunucusu

Merhaba references bölümünde bu örnekte açıklanan hello ortamı çoğunu derlemeler bir PowerShell komut dosyası yok. Yapı hello VM'ler ve sanal ağlar, bu belgede ayrıntılı hello örnek komut dosyası tarafından yapılır rağmen açıklanmamaktadır. 

toobuild hello ortam;

1. (Adları, konum ve IP adreslerini toomatch verilen hello senaryo güncelleştirilmiş) hello başvurular bölümüne dahil hello ağ yapılandırma xml dosyasını kaydedin
2. Güncelleştirme hello kullanıcı değişkenleri hello betik toomatch hello ortamı hello komut olan toobe Çalıştır (Abonelikleri, hizmet adlarını vb. karşı.)
3. PowerShell'de Hello komut dosyası yürütme

>[!Note]
>Merhaba PowerShell Betiği miktarlara hello bölge hello ağ yapılandırması xml dosyasında miktarlara hello bölge ile eşleşmelidir.
>
>

Merhaba komut dosyasını başarıyla ek çalıştırır sonra isteğe bağlı adımlar izlenebilir, hello references bölümünde hello web sunucusu ve uygulama sunucusu bu DMZ yapılandırma ile test basit bir web uygulaması tooallow ile iki komut dosyaları tooset.

Hello aşağıdaki bölümlerde ağ güvenlik grupları ve bunların Bu örnek için anahtar hello PowerShell Betiği satırları arasında adım adım ilerlemenizi sağlayarak işlevleri ayrıntılı bir açıklama belirtin.

## <a name="network-security-groups-nsg"></a>Ağ Güvenlik Grupları (NSG)
Bu örnekte, bir NSG grubu yerleşik ve altı kurallarıyla yüklendi. 

> [!TIP]
> Genel olarak bakıldığında, belirli "İzin ver" kurallarınızı ilk oluşturun ve daha genel "Deny" kuralları son hello gerekir. öncelik atanmış hello hangi kuralları ilk olarak değerlendirilir belirler. Trafik tooapply tooa belirli kural bulunduktan sonra başka hiçbir kural değerlendirilir. NSG kuralları hello ikisinde uygulayabileceğiniz gelen veya giden yön (Merhaba alt hello açısından).
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

Toohello giden trafiğe izin veren varsayılan giden kural Internet. Bu örnekte, biz giden trafiğe izin vermek ve herhangi bir giden kuralı değiştirme değil. Her iki yönde trafik aşağı toolock, kullanıcı tanımlanan yönlendirme gereklidir ve "Örnek 3" Merhaba üzerinde incelediniz [güvenlik sınırı en iyi yöntemler sayfası][HOME].

Her kural aşağıdaki gibi daha ayrıntılı olarak ele (**Not**: dolar işareti listesi başlayarak aşağıdaki hello herhangi bir öğeye (örneğin: $NSGName) kullanıcı tanımlı değişken hello başvuru bölümünde, bu belgenin hello betikten):

1. İlk ağ güvenlik grubu toohold hello kuralları oluşturulmalıdır:

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. Bu örnekte Hello ilk kural hello arka uç alt ağdaki tüm İç ağlara toohello DNS sunucusu arasında DNS trafiğine izin verir. Merhaba kuralı bazı önemli parametreler sahiptir:
   
   * "Tür" trafik akışı hangi yönde bu kural etkinleşir belirtir. Merhaba yönünü (bağlı olarak bu NSG burada bağlı) hello açısından hello alt ağı veya sanal makine değil. Bu nedenle türüdür "Giriş" ve trafiği hello alt girerek, hello kuralın ve hello alt ağdan çıkan trafiğe etkilenmemiştir bu kural tarafından durumunda.
   * "Öncelik" Merhaba sırasını trafik akışı değerlendirileceğini belirler. Merhaba alt hello sayı hello yüksek hello önceliği. Tooa belirli bir trafik akışı bir kural uygulandığı zaman başka hiçbir kural işlenir. Bu nedenle öncelik 1 olan bir kural trafiğine izin verir ve trafiği, öncelik 2 olan bir kural reddeder ve tootraffic hem kuralları uygula durumunda hello trafiği tooflow izin (Kural 1 yüksek önceliğe sahip olduğundan etkisi sürdü ve başka hiçbir kural uygulanan).
   * Bu kural tarafından etkilenen trafiği engellendi veya izin verilen "Eylem" belirtir.

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. Bu kural, alt ağ RDP trafiğine tooflow hello herhangi bir sunucuda hello Internet toohello RDP bağlantı noktasından bağlı sağlar. Bu kural adres öneklerini iki özel tür kullanır; "Vırtual_network" ve "INTERNET." Bu etiketler kolay bir yolu tooaddress adres öneklerini daha büyük bir kategoride var.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. Bu kural gelen Internet trafiği toohit hello web sunucusu sağlar. Bu kural hello yönlendirme davranışını değiştirmez. Merhaba kural yalnızca IIS01 toopass giden trafiğe izin verir. Bu nedenle hello Internet trafiği bu kural izin ve daha fazla kural işlemeyi durdur hedef olarak hello web sunucusunun sahip. (Öncelikle hello kuralında 140 diğer tüm gelen Internet trafiğini engellendi). Yalnızca HTTP trafiğini işlemek, bu kural başka olabilir kısıtlı tooonly hedef bağlantı noktası 80 izin verin.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. Bu kural hello IIS01 sunucusundan trafiği toopass toohello AppVM01 sunucu izin verir; bir sonraki kural diğer tüm ön uç tooBackend trafiği engeller. Bu kural, başlangıç bağlantı noktası biliniyorsa eklenmelidir tooimprove. Merhaba IIS sunucusu yalnızca SQL Server'da AppVM01 basarsa, örneğin, hello hedef bağlantı noktası aralığı değiştirildiği "*" (tüm) too1433 (Merhaba SQL bağlantı noktası) böylece Merhaba web uygulaması hiç tehlikeye AppVM01 üzerinde daha küçük bir gelen saldırı yüzeyini sağlar.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. Bu kural hello Internet tooany sunucularından hello ağ üzerindeki trafiği engeller. Hello kurallarıyla öncelikli 110 ve 120 hello etkisi tooallow yalnızca gelen Internet trafiği toohello güvenlik duvarı ve sunucularda RDP bağlantı noktalarını ve şey engeller. Bu kural, "Ayrıcalık tanımayın" kural tooblock tüm beklenmeyen akışlar ' dir.
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. Merhaba son kural hello ön uç alt toohello arka uç alt ağından trafiği engeller. Bu kural yalnızca bir gelen kuralı olduğundan, geriye doğru trafiğinin (Merhaba arka uç toohello ön uç) izin verilir.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a>Trafik senaryoları
#### <a name="allowed-internet-tooweb-server"></a>(*İzin verilen*) Internet tooweb sunucusu
1. Bir Internet kullanıcı FrontEnd001.CloudApp.Net (Internet'e yönelik bulut hizmeti) istekler bir HTTP sayfası
2. Bulut hizmeti geçişleri trafiğini açık uç noktasını IIS01 doğru bağlantı noktası 80 üzerinden (Merhaba web sunucusu)
3. Ön uç alt gelen kuralı işleme başlar:
   1. NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı
   2. NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı
   3. NSG kural 3 (Internet tooIIS01) geçerli, izin verilen, Dur kural işlenirken trafiğidir
4. İç IP adresi hello web sunucusunun IIS01 (10.0.1.5) trafiği isabetler
5. IIS01 web trafiği için dinleme, bu isteği alır ve hello isteği işlemeye başlıyor
6. IIS01 hello SQL Server AppVM01 hakkında bilgi için sorar
7. Ön uç alt ağda hiçbir giden kuralları olduğundan, trafiğe izin verilir
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
12. Merhaba IIS sunucusu hello SQL yanıtı alır ve hello HTTP yanıtı tamamlar ve toohello istek gönderir
13. Hello ön uç alt ağda hiçbir giden kuralları olduğundan hello yanıt izin verilir ve hello Internet kullanıcı hello web sayfasının alır.

#### <a name="allowed-rdp-toobackend"></a>(*İzin verilen*) RDP toobackend
1. Sunucu Yöneticisi internet üzerindeki istekleri xxxxx RDP tooAppVM01 hello rastgele atanan bağlantı noktası numarası olduğu BackEnd001.CloudApp.Net:xxxxx üzerinde RDP oturumu tooAppVM01 (Merhaba atanan bağlantı noktası bulunabilir hello Azure portal veya PowerShell aracılığıyla)
2. Arka uç alt gelen kuralı işleme başlar:
   1. NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı
   2. NSG kuralı 2 (RDP) uygulamak için izin verilen, Dur kural işlenirken trafiğidir
3. Hiçbir giden kuralları, varsayılan kuralları uygula ve dönüş trafiğine izin verilir
4. RDP oturumu etkin
5. AppVM01 hello kullanıcı adı ve parola isteyen

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

#### <a name="denied-web-toobackend-server"></a>(*Reddedildi*) Web toobackend sunucusu
1. Bir Internet kullanıcı tooaccess AppVM01 bir dosyada hello BackEnd001.CloudApp.Net hizmeti ile çalışır
2. Dosya Paylaşımı için açık uç nokta yok olduğundan, bu trafiği hello bulut hizmeti geçirmek değil'yı ve hello sunucusuna ulaşabilir olmayacaktır
3. NSG kural 5 (Internet tooVNet) Hello uç noktaları için herhangi bir nedenle açıksa, bu trafiği engeller

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Reddedildi*) DNS sunucusunda Web DNS araması
1. Bir Internet kullanıcı çalıştığında toolook DNS01 hello BackEnd001.CloudApp.Net hizmeti aracılığıyla bir iç DNS kaydını ayarlama
2. DNS için açık uç nokta yok olduğundan, bu trafiği hello bulut hizmeti geçirmek değil'yı ve hello sunucusuna ulaşabilir olmayacaktır
3. NSG kural 5 (Internet tooVNet) Hello uç noktaları için herhangi bir nedenle açıksa, bu trafiği engeller (Not: Bu kural 1 (DNS), iki nedenden dolayı geçerli değil, ilk hello kaynak adresi Internet Merhaba, toohello yalnızca bu kuralın uygulanacağı hello olarak yerel VNet kaynak, aynı zamanda Bu kural bir izin verme kuralı olduğundan, hiçbir zaman trafiği reddetmeye)

#### <a name="denied-web-toosql-access-through-firewall"></a>(*Reddedildi*) Web güvenlik duvarı aracılığıyla tooSQL erişimi
1. Bir Internet kullanıcının SQL verileri FrontEnd001.CloudApp.Net (Internet'e yönelik bulut hizmeti) ' ister.
2. SQL için açık uç nokta yok olduğundan, bu trafiği hello bulut hizmeti geçirmek değil'yı ve hello güvenlik duvarı ulaşmak olmayacaktır
3. Uç noktaları için herhangi bir nedenle açıksa, hello ön uç alt gelen kuralı işleme başlar:
   1. NSG kural 1 (DNS) uygulanmaz, taşıma toonext kuralı
   2. NSG kuralı 2 (RDP) uygulanmaz, taşıma toonext kuralı
   3. NSG kural 3 (Internet tooIIS01) geçerli, izin verilen, Dur kural işlenirken trafiğidir
4. İç IP adresi hello IIS01 (10.0.1.5) trafiği isabetler
5. Bağlantı noktası 1433, bu nedenle hiçbir yanıt toohello isteği IIS01 dinleme değil

## <a name="conclusion"></a>Sonuç
Bu örnek hello arka uç alt ağından gelen trafiği yalıtma, görece basit ve basit bir yoludur.

Daha fazla örnekler ve ağ güvenlik sınırları genel bir bakış bulunabilir [burada][HOME].

## <a name="references"></a>Başvurular
### <a name="main-script-and-network-config"></a>Ana komut dosyası ve ağ yapılandırma
Merhaba tam komut dosyası bir PowerShell komut dosyası kaydedin. Merhaba ağ yapılandırma "NetworkConf1.xml." adlı bir dosyaya kaydet
Merhaba kullanıcı tanımlı değişkenleri gerekli ve çalışma hello komut dosyası olarak değiştirin.

#### <a name="full-script"></a>Tam betik
Kullanıcı tanımlı hello değişkenleri esas alarak bu betiği olur;

1. Tooan Azure aboneliğine bağlanma
2. Depolama hesabı oluşturma
3. VNet ve hello ağ yapılandırma dosyasında tanımlanan iki alt ağ oluşturma
4. Dört windows server Vm'lerinin oluşturma
5. NSG dahil olmak üzere yapılandırın:
   * Bir NSG oluşturma
   * Kuralları ile doldurma
   * Merhaba NSG toohello uygun alt ağları bağlama

Bu PowerShell Betiği, bir bilgisayar veya sunucu, Internet'e yerel olarak çalıştırılmalıdır.

> [!IMPORTANT]
> Bu komut dosyasını çalıştırdığınızda, uyarı veya PowerShell'de pop diğer bilgilendirici iletileri olabilir. Yalnızca hata iletileri kırmızı sorunu nedeni edilir.
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
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

# User-Defined Global Variables
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
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
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
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
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
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
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
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a>Ağ yapılandırma dosyası
Güncelleştirilmiş konumla bu xml dosyasını kaydedin ve komut dosyası önceki hello hello bağlantı toothis dosya toohello $NetworkConfigFile değişkeni ekleyin.

```XML
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
```

#### <a name="sample-application-scripts"></a>Örnek uygulama komut dosyaları
Bu ve diğer çevre örnekleri için örnek bir uygulama tooinstall istiyorsanız, bir bağlantı aşağıdaki hello sağlanmış: [örnek uygulama betiği][SampleApp]

## <a name="next-steps"></a>Sonraki adımlar
* Güncelleştirme ve XML dosyasını kaydedin
* Merhaba PowerShell komut dosyası toobuild hello ortamı çalıştırın
* Merhaba örnek uygulaması yükleme
* Bu DMZ aracılığıyla farklı trafik akışları test etme

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "NSG ile giriş DMZ"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

