---
title: "Hızlı rota ile çalışmak için yapılandırma ayrıntılarını aaaNetwork"
description: "Uygulama hizmeti ortamları sanal ağlarda çalıştırmak için ağ yapılandırma ayrıntıları tooan expressroute bağlantı hattı bağlı."
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 34b49178-2595-4d32-9b41-110c96dde6bf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/14/2016
ms.author: stefsch
ms.openlocfilehash: 85bbc45cfed619485957ee2a898aa0a7604173cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="network-configuration-details-for-app-service-environments-with-expressroute"></a>ExpressRoute Bağlantılı App Service Ortamları için Ağ Yapılandırması Ayrıntıları
## <a name="overview"></a>Genel Bakış
Müşteriler bağlanabileceği bir [Azure ExpressRoute] [ ExpressRoute] hattı tootheir sanal ağ altyapısı, böylece kendi şirket içi ağ tooAzure genişletme.  Bu alt ağda bir uygulama hizmeti ortamı oluşturulabilir [sanal ağ] [ virtualnetwork] altyapı.  Uygulama hizmeti ortamı Hello üzerinde çalışan uygulamalar, ardından güvenli bağlantılar tooback uç kaynakları erişilebilir hello yalnızca ExpressRoute bağlantı kurabilirsiniz.  

Bir uygulama hizmeti ortamı oluşturulabilir **ya da** bir Azure Resource Manager sanal ağ **veya** Klasik dağıtım modeli sanal ağı.  Haziran 2016'da yapılan son bir değişiklikle ASEs de artık ortak adres aralıkları veya RFC1918 adres alanları (özel adresleri) kullanan sanal ağları içinde dağıtılabilir. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="required-network-connectivity"></a>Gerekli ağ bağlantısı
Bir sanal ağa bağlı tooan ExpressRoute başlangıçta karşılanır değil, App Service ortamları için ağ bağlantı gereksinimleri vardır.  Uygulama hizmeti ortamları düzgün tüm sipariş toofunction hello aşağıdakileri gerektirir:

* Giden ağ bağlantısı tooAzure depolama üzerindeki uç noktaları dünya çapında her iki bağlantı noktası 80 ve 443'tür.  Bu uç noktaları hello bulunan içerir bulunan depolama uç noktaları yanı sıra hello uygulama hizmeti ortamı aynı bölgede **diğer** Azure bölgeleri.  Azure depolama uç noktaları çözmek DNS etki alanı aşağıdaki hello altında: *table.core.windows.net*, *blob.core.windows.net*, *queue.core.windows.net* ve *file.core.windows.net*.  
* Giden ağ bağlantısı toohello Azure dosyaları hizmet bağlantı noktası 445.
* Giden ağ bağlantısı tooSql DB bitiş noktaları aynı hello bulunan uygulama hizmeti ortamı hello gibi bölge.  SQL DB uç noktaları çözmek etki alanı aşağıdaki hello altında: *database.windows.net*.  Bu erişim tooports 1433 11000 11999 ve 14000 14999 açma gerektirir.  Daha fazla bilgi için bkz [bu makalede Sql Database V12 bağlantı noktası kullanımı](../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md).
* Giden ağ bağlantısı toohello Azure yönetim düzlemi uç noktaları (ASM ve ARM uç noktaları).  Bu, giden bağlantı tooboth içerir *management.core.windows.net* ve *management.azure.com*. 
* Giden çok ağ bağlantısı*ocsp.msocsp.com*, *mscrl.microsoft.com* ve *crl.microsoft.com*.  Bu gerekli toosupport SSL işlevdir.
* Merhaba hello sanal ağ için DNS yapılandırmasını hello bitiş noktalarının tümü çözme yeteneğine sahip olmalı ve etki alanları belirtilen hello önceki noktaları.  Bu uç noktalar çözümlenemezse, uygulama hizmeti ortamı oluşturma denemeleri başarısız olur ve var olan uygulama hizmeti ortamları gibi sağlıksız olarak işaretlenecek.
* DNS sunucuları ile iletişim için bağlantı noktası 53 giden erişim gereklidir.
* Özel bir DNS sunucusu üzerinde varsa bir VPN ağ geçidi diğer ucundaki Merhaba, hello DNS sunucusu hello uygulama hizmeti ortamı içeren hello alt ağ üzerinden erişilebilir olması gerekir. 
* Merhaba giden ağ yolu iç kurumsal proxy'leri seyahat olamaz veya tooon içi zorlamalı tünel olabilir.  Değişiklikleri hello uygulama hizmeti ortamı giden ağ trafiğini etkili NAT adresi hello bunları yapmak.  Uygulama hizmeti ortamı'nın giden ağ trafiği Hello NAT adresi değiştirme hataları toomany hello uç noktaları yukarıda listelenen bağlantı neden olur.  Bu, başarısız uygulama hizmeti ortamı oluşturma girişimi, aynı zamanda daha önce sağlıklı App Service ortamları sorunlu olarak işaretlenen sonuçlanır.  
* Uygulama hizmeti ortamları, bu konuda açıklandığı gibi izin verilmelidir için ağ erişim toorequired bağlantı noktaları gelen [makale][requiredports].

Geçerli bir DNS altyapısının yapılandırılmış ve sanal ağ için hello saklanır sağlayarak Hello DNS gereksinimleri karşılanabilir.  Bir uygulama hizmeti ortamı oluşturulduktan sonra herhangi bir nedenle hello için DNS yapılandırması değiştirildiğinde, geliştiricilerin bir uygulama hizmeti ortamı toopick hello yeni DNS yapılandırması zorlayabilirsiniz.  Merhaba uygulama hizmeti ortamı yönetim dikey penceresinde hello hello üstündeki hello "Yeniden Başlat" simgesini kullanarak çalışırken bir ortamı yeniden başlatma tetikleme [Azure portal] [ NewPortal] hello ortamı toopick neden olur Merhaba yeni DNS yapılandırmasını.

Merhaba gelen ağ erişimi gereksinimleri yapılandırarak karşılanır bir [ağ güvenlik grubu] [ NetworkSecurityGroups] bu açıklandığıgibihellouygulamahizmetiortamı'nınalttooallowgereklihelloerişim[makale][requiredports].

## <a name="enabling-outbound-network-connectivity-for-an-app-service-environment"></a>Uygulama hizmeti ortamı için etkinleştirme giden ağ bağlantısı
Varsayılan olarak, yeni oluşturulan bir expressroute bağlantı hattı giden Internet bağlantısı sağlayan bir varsayılan yol tanıtır.  Bu yapılandırma bir uygulama hizmeti ortamı ile mümkün tooconnect tooother Azure uç noktaları olacaktır.

Genel Müşteri yapılandırma toodefine ancak giden Internet trafiği tooinstead akış zorlar kendi varsayılan yol (0.0.0.0/0) şirket içi.  Bu trafik akışı App Service ortamları hello giden trafiği ya da engellenen şirket içi veya NAT tooan tanınmayan artık çeşitli Azure uç noktaları ile çalışma adresleri kümesini 'd olduğundan neredeyse şaşmaz biçimde keser.

Merhaba, hello uygulama hizmeti ortamı içeren hello alt ağdaki bir (veya daha fazla) toodefine kullanıcı tanımlı yollar (Udr'ler) çözümüdür.  Bir UDR hello varsayılan yol yerine uyulacaktır alt özel yollar tanımlar.

Mümkünse, bu yapılandırma aşağıdaki toouse hello önerilir:

* Merhaba ExpressRoute yapılandırma 0.0.0.0/0 tanıtır ve varsayılan olarak tüm giden trafiği şirket içi zorlamalı tünel oluşturur.
* Merhaba uygulanan UDR toohello Hello uygulama hizmeti ortamı içeren alt ağ (buna örnek olarak bu makaledeki uzağına aşağı) Internet sonraki atlama türü olan 0.0.0.0/0 tanımlar.

Merhaba birleşik bu adımları hello alt düzey UDR hello zorlanan tünel, ExpressRoute böylece hello uygulama hizmeti ortamı'ndan giden Internet erişimi sağlama yapmaları işlemi etkisidir.

> [!IMPORTANT]
> Merhaba UDR içinde tanımlanan yollar **gerekir** önceliklidir tüm yollar üzerinden ExpressRoute yapılandırma hello tarafından tanıtılan çok yeterince spesifik olabilir.  Aşağıdaki Hello örnek hello geniş 0.0.0.0/0 adres aralığını kullanır ve bu nedenle olası yanlışlıkla daha belirli adres aralıkları kullanarak Yol tanıtımlarını tarafından geçersiz kılınabilir.
> 
> Uygulama hizmeti ortamları ExpressRoute yapılandırmalarla desteklenmiyor, **hello ortak eşleme yolu toohello özel eşleme yolu yolları arası tanıtma**.  Yapılandırılmış, ortak eşleme sahip ExpressRoute yapılandırmaları alacağı Yol tanıtımlarını Microsoft'tan çok sayıda Microsoft Azure IP adres aralıkları için.  Bu adres aralıklarını hello özel eşleme yoluna arası tanıtılan varsa, hello son hello uygulama hizmeti ortamı'nın alt ağdaki tüm giden ağ paketlerinin zorlamalı tünel tooa müşterinin şirket içi ağ altyapısı olacağını sonucudur.  Bu ağ akışı ile uygulama hizmeti ortamları şu anda desteklenmiyor.  Bir çözüm toothis hello ortak eşleme yolu toohello özel eşleme yolu toostop arası reklam yolları sorunudur.
> 
> 

Kullanıcı tanımlı yollar hakkında arka plan bilgileri kullanılabilir bu [genel bakış][UDROverview].  

Oluşturma ve kullanıcı tanımlı yollar yapılandırma ile ilgili ayrıntılar bu konuda kullanılabilir [nasıl tooGuide][UDRHowTo].

## <a name="example-udr-configuration-for-an-app-service-environment"></a>Uygulama hizmeti ortamı için örnek UDR yapılandırma
**Ön koşullar**

1. Hello Azure PowerShell'i yükleme [Azure indirmeler sayfası] [ AzureDownloads] (Haziran 2015 veya sonraki tarihli).  "Altında komut satırı araçları" Merhaba son Powershell cmdlet'lerini yükler "Windows Powershell" altında "Yükle" bağlantısı yoktur.
2. Benzersiz bir alt ağ bir uygulama hizmeti ortamı tarafından özel kullanım için oluşturulan önerilir.  Bu, o hello uygulanan Udr'ler toohello alt yalnızca giden trafik hello uygulama hizmeti ortamı için açık sağlar.
3. **Önemli**: dağıtmak uygulama hizmeti ortamı kadar hello **sonra** aşağıdaki yapılandırma adımları hello ardından.  Bu toodeploy bir uygulama hizmeti ortamı denemeden önce giden ağ bağlantısı kullanılabilir olmasını sağlar.

**1. adım: bir adlandırılmış yol tablosu oluşturma**

Merhaba aşağıdaki kod parçacığında hello BİZE Batı Azure bölgesinde "DirectInternetRouteTable" adında bir yol tablosu oluşturur:

    New-AzureRouteTable -Name 'DirectInternetRouteTable' -Location uswest

**2. adım: bir veya daha fazla yol hello rota tablosunda oluşturma**

Tooadd biri gerekir ya da daha fazla yollar toohello rota tablosunda sipariş tooenable giden Internet erişimi.  

Merhaba Internet toodefine aşağıda gösterildiği gibi 0.0.0.0/0 için bir yol olduğu giden erişim toohello yapılandırmaya yönelik bir yaklaşım önerilir.

    Get-AzureRouteTable -Name 'DirectInternetRouteTable' | Set-AzureRoute -RouteName 'Direct Internet Range 0' -AddressPrefix 0.0.0.0/0 -NextHopType Internet

Bu 0.0.0.0/0 geniş adres aralığı ve bu nedenle daha belirli adres aralıkları ExpressRoute hello tarafından tanıtılan tarafından geçersiz kılınacaktır unutmayın.  toore-hello yinelemek önceki öneri, bir 0.0.0.0/0 yol ile UDR, yalnızca 0.0.0.0/0 de tanıtır ExressRoute yapılandırma ile birlikte kullanılmalıdır. 

Alternatif olarak, Azure tarafından kullanılıyor CIDR aralıkları, kapsamlı ve güncelleştirilmiş listesini indirebilirsiniz.  Merhaba tüm hello Azure IP adres aralıklarını içeren Xml dosyasını hello kullanılabilir [Microsoft Download Center][DownloadCenterAddressRanges].  

Ancak, zaman içinde bu aralıklar değiştirmek, böylece düzenli el ile güncelleştirmeleri toohello araya kullanıcı tanımlı yollar tookeep eşitlenmiş dikkat edin.  Ayrıca, üst varsayılan olduğundan sınırı tek UDR, 100 yollar, çok "özetlemek" Merhaba Azure IP adresi aralıkları toofit hello 100 rota sınırı içinde bu UDR göz önünde bulundurarak tanımlanmış rotalar toobe tarafından tanıtılan hello yolları daha ayrıntılı gerekir, ExpressRoute.  

**3. adım: hello rota tablosu toohello alt ağ içeren hello uygulama hizmeti ortamı ilişkilendirme**

Uygulama hizmeti ortamı hello dağıtılacağı tooassociate hello rota tablosu toohello alt Hello son yapılandırma adımı var.  Merhaba aşağıdaki komutu hello "DirectInternetRouteTable" toohello "bir uygulama hizmeti ortamı sonunda içerecek ASESubnet" ilişkilendirir.

    Set-AzureSubnetRouteTable -VirtualNetworkName 'YourVirtualNetworkNameHere' -SubnetName 'ASESubnet' -RouteTableName 'DirectInternetRouteTable'


**4. adım: Son adımlar**

Merhaba yol tablosu ilişkili toohello alt eklendiğinde, toofirst test önerilir ve etkili hello hedeflenen onaylayın.  Örneğin, bir sanal makine hello alt ağ dağıtabilir ve onaylayın:

* Giden trafik tooboth Azure ve Azure dışı uç noktaları belirtiliyor daha önce bu makalede, **değil** expressroute bağlantı hattı hello akar.  Merhaba alt ağdan giden trafiği ise şirket içi, uygulama hizmeti ortamı oluşturma hala zorlamalı tünel beri bu davranış, her zaman görüntülenip tooverify başarısız çok önemlidir. 
* Tüm düzgün çözme hello uç noktaları için DNS araması daha önce bahsedilen. 

Yukarıdaki adımları Hello onaylanır sonra hello alt toobe uygulama hizmeti ortamı oluşturulan hello zaman hello "boş" gerektiğinden toodelete hello sanal makine gerekir.

Bir uygulama hizmeti ortamı oluşturma ile devam edin!

## <a name="getting-started"></a>Başlarken
Tüm makaleler ve nasıl-için uygulama hizmeti ortamları hello kullanılabilir için kullanıcının [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).

Uygulama hizmeti ortamları ile çalışmaya tooget bakın [giriş tooApp hizmeti ortamı][IntroToAppServiceEnvironment]

Hello Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service][AzureAppService].

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[requiredports]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[NetworkSecurityGroups]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[UDROverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-overview/
[UDRHowTo]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-how-to/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureDownloads]: http://azure.microsoft.com/en-us/downloads/ 
[DownloadCenterAddressRanges]: http://www.microsoft.com/download/details.aspx?id=41653  
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[NewPortal]:  https://portal.azure.com


<!-- IMAGES -->
