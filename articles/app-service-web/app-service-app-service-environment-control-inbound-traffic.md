---
title: "aaaHow tooControl gelen trafiği tooan uygulama hizmeti ortamı"
description: "Nasıl tooconfigure ağ güvenlik kuralları toocontrol gelen hakkında trafiği tooan uygulama hizmeti ortamı hakkında bilgi edinin."
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: 
ms.assetid: 4cc82439-8791-48a4-9485-de6d8e1d1a08
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: stefsch
ms.openlocfilehash: e7c6e6201db6a1ea77f7a2eee29a3b5445175495
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocontrol-inbound-traffic-tooan-app-service-environment"></a>Nasıl tooControl gelen trafiği tooan uygulama hizmeti ortamı
## <a name="overview"></a>Genel Bakış
Bir uygulama hizmeti ortamı oluşturulabilir **ya da** bir Azure Resource Manager sanal ağ **veya** Klasik dağıtım modeli [sanal ağ] [ virtualnetwork].  Yeni sanal ağ ve yeni alt hello aynı anda bir uygulama hizmeti ortamı oluşturulan tanımlanabilir.  Alternatif olarak, bir uygulama hizmeti ortamı önceden var olan sanal ağ ve önceden var olan bir alt ağ içinde oluşturulabilir.  Haziran 2016'da yapılan bir değişiklikle ASEs ortak adres aralıkları veya RFC1918 adres alanları (özel adresleri) kullanan sanal ağları içinde dağıtılabilir.  Bir uygulama hizmeti ortamı oluşturma hakkında daha fazla bilgi için bkz [nasıl tooCreate bir uygulama hizmeti ortamı][HowToCreateAnAppServiceEnvironment].

Bir alt ağ gelen trafiğe Yukarı Akış aygıtlarını ve hizmetlerini arkasında basılı kullanılan toolock sağlayacak şekilde HTTP ve HTTPS trafiği yalnızca gelen belirli kabul olabilen bir ağ sınırında sağladığından bir uygulama hizmeti ortamı her zaman bir alt ağ içinde yukarı akış oluşturulmalıdır IP adresleri.

Bir alt ağdaki gelen ve giden ağ trafiğini kullanılarak denetlenir bir [ağ güvenlik grubu][NetworkSecurityGroups]. Gelen trafik denetleme ağ güvenlik kuralları bir ağ güvenlik grubu oluşturma ve hello ağ güvenlik grubu hello alt ağ içeren hello uygulama hizmeti ortamı atama gerektirir.

Bir ağ güvenlik grubu tooa alt atandıktan sonra gelen trafiği tooapps uygulama hizmeti ortamı hello üzerinde izin verilen ve engellenen dayalıdır hello içinde izin verme ve reddetme hello ağ güvenlik grubu tanımlanan kuralları.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="inbound-network-ports-used-in-an-app-service-environment"></a>Gelen ağ bir uygulama hizmeti ortamı'nda kullanılan bağlantı noktaları
Bir ağ güvenlik grubu ile gelen ağ trafiğini kilitlemek önce önemli tooknow hello bir uygulama hizmeti ortamı tarafından kullanılan gerekli ve isteğe bağlı ağ bağlantı noktaları kümesidir.  Yanlışlıkla trafiği toosome bağlantı noktalarını kapatma bir uygulama hizmeti ortamı işlev kaybı neden olabilir.

Merhaba, bir uygulama hizmeti ortamı tarafından kullanılan bağlantı noktalarının bir listesi verilmiştir. Tüm bağlantı noktaları **TCP**aksi açıkça belirtilmediği sürece:

* 454: **gerekli bağlantı noktası** yönetme ve SSL üzerinden uygulama hizmeti ortamları korumaya yönelik Azure altyapısı tarafından kullanılır.  Trafiği toothis bağlantı noktası engellemez.  Bu bağlantı noktası her zaman bir ana, genel VIP ilişkili toohello olur.
* 455: **gerekli bağlantı noktası** yönetme ve SSL üzerinden uygulama hizmeti ortamları korumaya yönelik Azure altyapısı tarafından kullanılır.  Trafiği toothis bağlantı noktası engellemez.  Bu bağlantı noktası her zaman bir ana, genel VIP ilişkili toohello olur.
* 80: varsayılan App Service planları bir uygulama hizmeti ortamında çalışan gelen HTTP trafiği tooapps için bağlantı noktası.  Bir ILB özellikli ana Bu bağlantı noktasına bağlı toohello ILB hello ana adresidir.
* 443: varsayılan App Service planları bir uygulama hizmeti ortamında çalışan gelen SSL trafiği tooapps için bağlantı noktası.  Bir ILB özellikli ana Bu bağlantı noktasına bağlı toohello ILB hello ana adresidir.
* 21: denetim kanalı FTP için.  FTP değil kullanılıyorsa, bu bağlantı noktası güvenli bir şekilde engellenebilir.  Bir ILB özellikli ana Bu bağlantı noktası için bir ana ilişkili toohello ILB adresi olabilir.
* 990: denetim kanalı FTPS için.  FTPS değil kullanılıyorsa, bu bağlantı noktası güvenli bir şekilde engellenebilir.  Bir ILB özellikli ana Bu bağlantı noktası için bir ana ilişkili toohello ILB adresi olabilir.
* 10001 10020: FTP için veri kanalı.  FTP değil kullanılıyorsa olarak hello denetim kanalı ile bu bağlantı noktalarının güvenli bir şekilde engellenebilir.  Bir ILB özellikli ana Bu bağlantı noktasına bağlı toohello ana'nın ILB adresi olabilir.
* 4016: Visual Studio 2012 ile uzaktan hata ayıklama için kullanılır.  Merhaba özelliği olmayan kullanılıyorsa, bu bağlantı noktası güvenli bir şekilde engellenebilir.  Bir ILB özellikli ana Bu bağlantı noktasına bağlı toohello ILB hello ana adresidir.
* 4018: Visual Studio 2013 ile uzaktan hata ayıklama için kullanılır.  Merhaba özelliği olmayan kullanılıyorsa, bu bağlantı noktası güvenli bir şekilde engellenebilir.  Bir ILB özellikli ana Bu bağlantı noktasına bağlı toohello ILB hello ana adresidir.
* 4020: Visual Studio 2015 ile uzaktan hata ayıklama için kullanılır.  Merhaba özelliği olmayan kullanılıyorsa, bu bağlantı noktası güvenli bir şekilde engellenebilir.  Bir ILB özellikli ana Bu bağlantı noktasına bağlı toohello ILB hello ana adresidir.

## <a name="outbound-connectivity-and-dns-requirements"></a>Giden bağlantısı ve DNS gereksinimleri
Bir uygulama hizmeti ortamı toofunction için düzgün şekilde de giden erişim toovarious uç nokta gerektiriyor. Tam bir ana tarafından kullanılan hello dış uç noktalar hello hello "Ağ bağlantısı gerekli" bölümünde listelenmiştir [ExpressRoute için ağ yapılandırması](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) makalesi.

Uygulama hizmeti ortamları hello sanal ağ için yapılandırılmış geçerli bir DNS altyapısı gerektirir.  Bir uygulama hizmeti ortamı oluşturulduktan sonra herhangi bir nedenle hello için DNS yapılandırması değiştirildiğinde, geliştiricilerin bir uygulama hizmeti ortamı toopick hello yeni DNS yapılandırması zorlayabilirsiniz.  Merhaba uygulama hizmeti ortamı yönetim dikey penceresinde hello hello üstündeki hello "Yeniden Başlat" simgesini kullanarak çalışırken bir ortamı yeniden başlatma tetikleme [Azure portal] [ NewPortal] hello ortamı toopick neden olur Merhaba yeni DNS yapılandırmasını.

Merhaba vnet hiçbir özel DNS sunucularında Kurulum zaman önceki toocreating bir uygulama hizmeti ortamı öncesinde olması önerilir.  Bir uygulama hizmeti ortamı oluşturulurken bir sanal ağın DNS yapılandırması değiştiyse, hello uygulama hizmeti ortamı oluşturma işlemi başarısız neden olur.  Özel bir DNS sunucusu üzerinde hello varsa, benzer bir damarlı içinde başka bir VPN ağ geçidi ve hello DNS sunucusu erişilemez veya kullanılamaz hello uygulama hizmeti ortamı oluşturma işlemi de başarısız olacak sonudur.

## <a name="creating-a-network-security-group"></a>Bir ağ güvenlik grubu oluşturma
Merhaba aşağıdaki nasıl iş ağ güvenlik grupları hakkında tam bilgi için bkz [bilgi][NetworkSecurityGroups].  Ağ güvenlik gruplarını yapılandırma ve bir uygulama hizmeti ortamı içeren bir ağ güvenlik grubu tooa alt uygulama odak rötuşları üzerinde aşağıdaki Hello Azure Hizmet Yönetimi örnekte vurgular.

**Not:** ağ güvenlik grupları, grafik hello kullanılarak yapılandırılabilir [Azure Portal](https://portal.azure.com) veya Azure PowerShell aracılığıyla.

Ağ güvenlik grupları, önce bir aboneliği ile ilişkili bir tek başına varlık olarak oluşturulur. Ağ güvenlik grupları bir Azure bölgesinde oluşturulduğundan, bu hello ağ güvenlik grubu hello aynı oluşturulur olun uygulama hizmeti ortamı hello gibi bölge.

bir ağ güvenlik grubu oluşturma Hello şunları gösterir:

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

Bir ağ güvenlik grubu oluşturulduktan sonra bir veya daha fazla ağ güvenlik kuralları tooit eklenir.  Kural kümesi Hello zaman içinde değişebilir gerektiğinden toospace numaralandırma şemasını hello çıkışı için kural önceliklerini toomake kolay tooinsert ek kurallar zamanla kullanılacağını önerilir.

Merhaba örnekte açıkça erişim toohello yönetim hello Azure altyapı toomanage tarafından gerekli bağlantı noktalarını verir ve uygulama hizmeti ortamını sürdürmek bir kural gösterilir.  Tüm yönetim trafiğini SSL üzerinden akar ve hello bağlantı noktaları açılmış olsa da, bunlar Azure Yönetim altyapısı dışında herhangi bir varlık tarafından erişilemez; bu nedenle istemci sertifikaları tarafından sağlanıyorsa unutmayın.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP


Kilitleme erişim tooport 80 ve 443 çok "gizle" Yukarı Akış aygıtları veya hizmetleri arkasındaki bir uygulama hizmeti ortamı, tooknow hello Yukarı Akış IP adresine ihtiyacınız olacaktır.  Bir web uygulaması Güvenlik Duvarı (WAF) kullanıyorsanız, örneğin, hello WAF kendi IP adresi (veya adresleri) ne zaman kullanan olacaktır proxy trafiği tooa aşağı akış uygulama hizmeti ortamı.  Bu IP adresi hello toouse gerekir *SourceAddressPrefix* bir ağ güvenlik kuralı parametresi.

Merhaba aşağıdaki örnekte, belirli bir Yukarı Akış IP adresinden gelen gelen trafiğe açıkça izin verilir.  Merhaba adresi *1.2.3.4* yer tutucu olarak için bir Yukarı Akış WAF hello IP adresi kullanılır.  Yukarı Akış aygıt veya hizmet tarafından kullanılan hello değeri toomatch hello adresini değiştirin.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTP" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT HTTPS" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

FTP desteği istenirse, kurallara hello bir şablon toogrant erişim toohello FTP denetim bağlantı ve veri kanalı bağlantı noktası kullanılabilir.  FTP durum bilgisi olan kuralıdır olduğundan, geleneksel bir HTTP/HTTPS güvenlik duvarı veya proxy aygıt üzerinden mümkün tooroute FTP trafiğine olmayabilir.  Bu durumda, tooset hello gerekir *SourceAddressPrefix* tooa farklı değer - örneğin hello IP adres aralığı geliştirici veya dağıtım makinelerin istemcileri hangi FTP üzerinde çalışıyor. 

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPCtrl" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '21' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT FTPDataRange" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '10001-10020' -Protocol TCP

(**Not:** hello veri kanalı bağlantı noktası aralığı hello Önizleme dönemi boyunca değişebilir.)

İle Visual Studio uzaktan hata ayıklama kullanılırsa, nasıl toogrant erişim kuralları aşağıdaki hello göstermektedir.  Her bir sürümü uzaktan hata ayıklama için farklı bir bağlantı noktasını kullandığından Visual Studio'nun desteklenen her sürümü için ayrı bir kural yok.  FTP erişimli olarak, uzaktan hata ayıklama trafiği geleneksel WAF ya da proxy aygıt akışı düzgün değil.  Merhaba *SourceAddressPrefix* bunun yerine Visual Studio çalıştıran Geliştirici makinelerinde toohello IP adres aralığı ayarlanabilir.

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2012" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4016' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2013" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4018' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityRule -Name "RESTRICT RemoteDebuggingVS2015" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '1.2.3.4/32'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '4020' -Protocol TCP

## <a name="assigning-a-network-security-group-tooa-subnet"></a>Ağ güvenlik grubu tooa alt ağ atama
Bir ağ güvenlik grubu erişim tooall dış trafiği engelleyen bir varsayılan güvenlik kuralını sahiptir.  Merhaba, yukarıda açıklanan hello ağ güvenlik kuralları birleştirme gelen sonuç ve hello gelen trafiği engelleyen varsayılan güvenlik kuralı, yalnızca kaynak adres aralıklarından trafiği ile ilişkili olan bir *izin* eylem erişebilir Uygulama hizmeti ortamı'nda çalışan toosend trafiği tooapps.

Bir ağ güvenlik grubu güvenlik kuralları ile doldurulduktan sonra hello uygulama hizmeti ortamı içeren atanan toobe toohello alt ağ gerekir.  Merhaba atama komutu hello sanal ağın hello uygulama hizmeti ortamı, hello uygulama hizmeti ortamı oluşturulduğu hello alt hello adını hem de bulunduğu her iki hello adı başvurur.  

Aşağıdaki Hello örnek, bir ağ güvenlik grubu tooa alt ağ ve sanal ağ atanmasını gösterir:

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

Merhaba ağ güvenlik grubu ataması başarılı olduktan sonra (Merhaba atama uzun süre çalışan işlemleri olduğu ve birkaç dakika toocomplete sürebilir), yalnızca trafik eşleşen gelen *izin* kuralları başarıyla hello uygulama uygulamalarında ulaşmak Hizmet ortamı.

Bütünlük hello için aşağıdaki örnekte nasıl hello alt ağdan tooremove ve bu nedenle parçalanmış ilişkilendirme hello ağ güvenlik grubu gösterilmektedir:

    Get-AzureNetworkSecurityGroup -Name "testNSGexample" | Remove-AzureNetworkSecurityGroupFromSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-test'

## <a name="special-considerations-for-explicit-ip-ssl"></a>Açık IP SSL için özel hususlar
Bir uygulama olan açık bir IP SSL adresi yapılandırılmışsa (uygulanabilir *yalnızca* genel VIP'ye sahip tooASEs), uygulama hizmeti ortamı hello hello varsayılan IP adresini kullanmak yerine, HTTP ve HTTPS trafiği hello alt akar 80 ve 443 numaralı bağlantı noktaları dışındaki bağlantı noktaları farklı bir küme üzerinde.

Merhaba tek tek her IP SSL adresi tarafından kullanılan bağlantı noktaları çiftinin hello uygulama hizmeti ortamı'nın ayrıntıları UX dikey penceresinden hello portal kullanıcı arabiriminde bulunabilir.  Select "tüm ayarları", "IP adreslerini"-->.  Merhaba "IP adreslerini" dikey penceresinde hello uygulama hizmeti ortamı için açıkça yapılandırılmış tüm IP SSL adresleri bir tablosu gösterir kullanılan tooroute hello özel bağlantı noktası çifti birlikte HTTP ve HTTPS trafiğini her IP SSL adresi ile ilişkili.  Bu kuralları içinde bir ağ güvenlik grubu yapılandırırken hello DestinationPortRange parametreleri için kullanılan toobe gerektiren bu bağlantı noktası çiftidir.

Bir uygulama bir ana üzerinde yapılandırılmış toouse IP SSL olduğunda, dış müşterileri görmezsiniz ve tooworry hello özel bağlantı noktası çifti eşlemesi hakkında gerekli değildir.  Trafiği toohello uygulamalar, normalde toohello yapılandırılmış IP SSL adresi akar.  Merhaba çeviri toohello özel bağlantı noktası çifti otomatik olarak dahili sırasında hello son leg yönlendirme trafiği hello alt ağ içeren hello ana gerçekleşir. 

## <a name="getting-started"></a>Başlarken
Uygulama hizmeti ortamları ile çalışmaya tooget bakın [giriş tooApp hizmeti ortamı][IntroToAppServiceEnvironment]

Tüm makaleler ve nasıl-için uygulama hizmeti ortamları hello kullanılabilir için kullanıcının [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).

Güvenli bir uygulama hizmeti ortamındaki toobackend kaynak bağlanan uygulamalara geçici daha fazla bilgi için bkz [güvenli bir uygulama hizmeti ortamındaki tooBackend kaynaklarına bağlanma][SecurelyConnecttoBackend]

Hello Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[SecurelyConnecttoBackend]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NewPortal]:  https://portal.azure.com  

<!-- IMAGES -->

