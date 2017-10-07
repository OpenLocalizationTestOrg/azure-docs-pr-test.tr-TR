---
title: "Azure uygulama hizmeti ortamı ile aaaNetworking konuları"
description: "Hello ana ağ trafiğini açıklar ve nasıl tooset Nsg'ler ve Udr'ler, ana ile"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 955a4d84-94ca-418d-aa79-b57a5eb8cb85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ccompy
ms.openlocfilehash: d4d3000f4d4d75814b1e6d47079d967334eb1a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-an-app-service-environment"></a>Uygulama hizmeti ortamı için ağ konuları #

## <a name="overview"></a>Genel Bakış ##

 Azure [uygulama hizmeti ortamı] [ Intro] bir Azure App Service, Azure sanal ağınıza (VNet) bir alt ağ içinde dağıtımıdır. Uygulama hizmeti ortamı (ana) için iki dağıtım türleri şunlardır:

- **Dış ana**: hello ana barındırılan uygulamalar internet'ten erişilebilen bir IP adresi üzerinde açığa çıkarır. Daha fazla bilgi için bkz: [bir dış ana oluşturma][MakeExternalASE].
- **ILB ana**: çıkarır hello ana barındırılan uygulamalar üzerinde bir IP adresi sanal ağınızın içinde. Merhaba dahili uç noktayı bir ILB ana çağırdı neden olan bir iç yük dengeleyici (ILB) ' dir. Daha fazla bilgi için bkz: [oluşturma ve kullanma bir ILB ana][MakeILBASE].

Artık uygulama hizmeti ortamı iki sürümü vardır: ASEv1 ve ASEv2. ASEv1 hakkında daha fazla bilgi için bkz: [giriş tooApp hizmeti ortamı v1][ASEv1Intro]. ASEv1 Klasik veya Resource Manager Vnet'i dağıtılabilir. ASEv2 yalnızca Resource Manager Vnet'i dağıtılabilir.

Bir ana gelen toohello Git tüm çağrıları Internet hello ana hello için atanan bir VIP aracılığıyla VNet bırakın. Merhaba bu VIP ortak IP hello kaynak IP toohello Git hello ana gelen tüm çağrıları için ise Internet. Hello kaynak IP, ana Hello uygulamalarında sanal ağınızın içinde veya bir VPN çağrıları tooresources yaparsanız, ana tarafından kullanılan hello alt ağdaki IP hello biridir. Merhaba ana hello VNet içinde olduğundan, ayrıca herhangi bir ek yapılandırma olmadan hello VNet içindeki kaynaklara erişebilir. Merhaba VNet bağlı tooyour şirket içi ağ ise, uygulamalar, ana de erişim tooresources sahip. Tooconfigure hello ana ya da uygulamanızı herhangi başka gerekmez.

![Dış ana][1] 

Bir dış ana varsa, hello genel VIP ayrıca ana uygulamalarınızı toofor gidermek hello uç noktadır:

* HTTP/S'DİR. 
* FTP/S'DİR. 
* Web dağıtımı.
* Uzaktan hata ayıklama.

![ILB ANA][2]

Bir ILB ana varsa, başlangıç IP adresi hello ILB HTTP/S, FTP/sn, web dağıtımı ve uzaktan hata ayıklama için hello uç noktadır.

Merhaba normal uygulama erişim bağlantı noktaları şunlardır:

| Kullanım | Kaynak | çok|
|----------|---------|-------------|
|  HTTP/HTTPS  | Kullanıcı tarafından yapılandırılabilir |  80, 443 |
|  FTP/FTPS    | Kullanıcı tarafından yapılandırılabilir |  21, 990, 10001-10020 |
|  Visual Studio uzaktan hata ayıklama  |  Kullanıcı tarafından yapılandırılabilir |  4016, 4018, 4020, 4022 |

Bu, bir dış ana ya da bir ILB ana iseniz geçerlidir. Bir dış ana üzerinde değilseniz, bu bağlantı noktalarına hello genel VIP ulaştı. Bir ILB ana değilseniz, bu bağlantı noktalarına hello ILB ulaştı. Bağlantı noktası 443 kilitlemek hello portalda kullanıma bazı özellikler üzerinde bir etkisi olabilir. Daha fazla bilgi için bkz: [Portal bağımlılıkları](#portaldep).

## <a name="ase-dependencies"></a>Ana bağımlılıkları ##

Bir ana gelen erişim bağımlılık:

| Kullanım | Kaynak | çok|
|-----|------|----|
| Yönetim | App Service management adresleri | ANA alt: 454, 455 |
|  ANA iç iletişim | ANA alt: tüm bağlantı noktaları | ANA alt: tüm bağlantı noktaları
|  Azure yük dengeleyici izin gelen | Azure yük dengeleyici | ANA alt: tüm bağlantı noktaları
|  Uygulama atanmış IP adresleri | Atanmış adresleri uygulama | ANA alt: tüm bağlantı noktaları

Hello gelen trafiği komut ve toosystem ek izleme hello ana denetim sağlar. Bu trafik için Hello kaynak IP'leri hello listelenen [adresleri ana Yönetimi] [ ASEManagement] belge. Merhaba ağ güvenliği yapılandırması 454 ve 455 bağlantı noktalarında tüm IP'ler tooallow erişimden gerekir.

Vardır hello ana alt ağ içindeki birçok bağlantı noktası iç bileşeni iletişim için kullanılan ve değişiklik.  Bu, tüm hello ana alt toobe hello ana alt ağdan erişilebilir hello bağlantı noktalarını gerektirir. 

Bu gereksinim toobe açık hello Azure yük dengeleyici hello ana alt hello minimum bağlantı noktaları arasında hello iletişimi için 454 ve 455 16001 olan. Merhaba 16001 bağlantı noktası hello yük dengeleyici ve hello ana arasındaki Koru canlı akış için kullanılır. Bir ILB ana kullanıyorsanız, trafik toojust hello 454, 455, 16001 bağlantı noktalarını aşağı kilitleyebilirsiniz.  Daha sonra bir dış ana kullanıyorsanız, hesabı hello normal uygulama erişim bağlantı noktasına tootake gerekir.  Atanan uygulamayı adresleri kullanıyorsanız tooopen gerekir, tooall bağlantı noktaları.  Bir adresi tooa belirli uygulama atandığında, hello yük dengeleyici önceden toosend HTTP ve HTTPS trafiği toohello ana Bilinmeyen bağlantı noktalarını kullanır.

Uygulama atanmış IP adresleri kullanıyorsanız tooyour uygulamaları toohello ana alt IP'leri atanan hello tooallow trafiğinden gerekir.

Giden erişim için bir ana birden çok dış sistemlerde bağlıdır. Bu sistem bağımlılıkları DNS adları ile tanımlanır ve IP adresleri kümesini sabit tooa eşleme yok. Bu nedenle, hello ana hello ana alt tooall giden erişim gerektiren çeşitli bağlantı noktaları üzerinden dış IP. Bir ana giden bağımlılıklar aşağıdaki hello sahiptir:

| Kullanım | Kaynak | çok|
|-----|------|----|
| Azure Storage | ANA alt ağ | Table.Core.Windows.NET, blob.core.windows.net, queue.core.windows.net, file.core.windows.net: 80, 443, 445 (445 yalnızca gereklidir ASEv1 için.) |
| Azure SQL Database | ANA alt ağ | Database.Windows.NET: 1433 11000 11999, 14000 14999 (daha fazla bilgi için bkz: [SQL Database V12 bağlantı noktası kullanımı](../../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md).)|
| Azure Yönetimi | ANA alt ağ | Management.Core.Windows.NET, management.azure.com: 443 
| SSL sertifika doğrulama |  ANA alt ağ            |  OCSP.msocsp.com, mscrl.microsoft.com, crl.microsoft.com: 443
| Azure Active Directory        | ANA alt ağ            |  Internet: 443
| Uygulama Hizmeti Yönetimi        | ANA alt ağ            |  Internet: 443
| Azure DNS                     | ANA alt ağ            |  Internet: 53
| ANA iç iletişim    | ANA alt: tüm bağlantı noktaları |  ANA alt: tüm bağlantı noktaları

Merhaba ana toothese bağımlılıkları erişimi kaybederse, çalışmayı durdurur. Ana hello uzun yeterli, durumda, askıya alınmış durumda.

### <a name="customer-dns"></a>Müşteri DNS ###

Merhaba VNet müşteri tanımlı bir DNS sunucusu ile yapılandırılmışsa, hello Kiracı İş yükleri bunu kullanın. Merhaba ana hala yönetim amacıyla Azure DNS ile toocommunicate gerekiyor. 

Merhaba VNet müşteriyle DNS üzerinde yapılandırılmışsa, VPN diğer tarafını Merhaba, hello DNS sunucusu hello ana içeren hello alt ağ üzerinden erişilebilir olması gerekir.

<a name="portaldep"></a>

## <a name="portal-dependencies"></a>Portal bağımlılıkları ##

Toplama toohello ana işlevsel bağımlılıkları, birkaç ek öğeler ilgili toohello portal deneyimi vardır. Hello Azure Portalı'nda hello özelliklerden bazıları üzerinde doğrudan erişim too_SCM site_ bağlıdır. Azure App Service'te her uygulama için iki URL'leri vardır. Merhaba ilk URL uygulamanızı tooaccess değil. Merhaba ikinci hello olarak da bilinir tooaccess hello SCM site URL'dir _Kudu konsol_. Merhaba SCM site kullanan özellikler şunlardır:

-   Web işleri
-   İşlevler
-   Akış günlüğü
-   Kudu
-   Uzantılar
-   İşlem Gezgini
-   Konsol

Bir ILB ana kullandığınızda, hello SCM site Internet VNet hello dışında erişilebilir değildir. Uygulamanızı bir ILB ana barındırıldığında, bazı özellikleri hello portalından çalışmaz.  

Birçok hello SCM site bağımlı bu yetenekleri de doğrudan hello Kudu konsolunda kullanılabilir. Tooit yerine doğrudan hello portalını kullanarak bağlanabilir. Uygulamanızı ILB ASE'de barındırılıyorsa, yayımlama kimlik bilgileri toosign kullanın. Merhaba URL tooaccess hello SCM site ILB ASE'de barındırılan bir uygulamanın biçimini izleyen hello sahiptir: 

```
<appname>.scm.<domain name hello ILB ASE was created with> 
```

ILB ana hello etki alanı adı ise *contoso.net* ve uygulama adınız *testapp*, hello uygulama adresindeki ulaşıldığında *testapp.contoso.net*. ile gidiyor hello SCM site adresindeki ulaşıldığında *testapp.scm.contoso.net*.

### <a name="functions-and-web-jobs"></a>İşlevler ve Web işleri ###

İşlevler ve Web işleri hello SCM siteye bağımlı olan ancak tarayıcınız hello SCM site ulaşabilir sürece, uygulamalarınızı ILB ASE'de olsa bile hello portalı kullanmak için desteklenir.  İle ILB ana kendinden imzalı bir sertifika kullanıyorsanız, sertifika, tarayıcı tootrust tooenable gerekir.  IE ve hello sertifika anlamına gelir kenar depolamak toobe hello bilgisayar güvende sahiptir.  Merhaba sertifika hello tarayıcıda önceki büyük olasılıkla hello scm site doğrudan basarsa tarafından kabul ettiğiniz anlamına gelir sonra Chrome kullanıyorsanız.  Merhaba en iyi toouse hello tarayıcı zincirindeki güven bir ticari sertifikası çözümüdür.  

## <a name="ase-ip-addresses"></a>ANA IP adresleri ##

Bir ana birkaç IP adreslerini toobe farkında sahiptir. Bunlar:

- **Gelen ortak IP adresi**: bir dış ana uygulama trafiği ve bir dış ana ve bir ILB ana yönetim trafiği için kullanılır.
- **Giden genel IP**: IP "Kimden" Merhaba ana giden bağlantılar için bu bırakın hello VNet, hangi VPN yönlendirilen olmayan hello olarak kullanılır.
- **ILB IP adresi**: bir ILB ana kullanıyorsanız.
- **Uygulama tarafından atanan IP tabanlı SSL adresleri**: bir dış ana ve IP tabanlı SSL yapılandırıldığında mümkün.

Bu IP adreslerine hello ana UI ' kolayca bir ASEv2 hello Azure portal'ın içinde görülebilir. Bir ILB ana varsa, hello IP hello ILB için listelenir.

![IP adresleri][3]

### <a name="app-assigned-ip-addresses"></a>Uygulama tarafından atanan IP adresleri ###

Bir dış ana ile tooindividual uygulamalar IP adresleri atayabilirsiniz. Bir ILB ana ile yapamazsınız. Hakkında daha fazla bilgi için tooconfigure uygulama toohave kendi IP adresini bakın [bir var olan özel SSL sertifikası tooAzure web uygulamaları bağlamak](../../app-service-web/app-service-web-tutorial-custom-ssl.md).

Uygulama kendi IP tabanlı SSL adresine sahipse, ana hello iki bağlantı noktaları toomap toothat IP adresi ayırır. Bir bağlantı noktası HTTP trafiği için ve hello diğer bağlantı noktası için HTTPS. Bu bağlantı noktalarını hello ana UI hello IP adresleri bölümünde listelenir. Trafiği, bu bağlantı noktalarından mümkün tooreach olmalıdır hello VIP veya hello uygulamalar erişilemez. Ağ güvenlik grupları (Nsg'ler) yapılandırdığınızda bu önemli tooremember gereksinimdir.

## <a name="network-security-groups"></a>Ağ Güvenlik Grupları ##

[Ağ güvenlik grupları] [ NSGs] bir sanal ağ içindeki hello özelliği toocontrol ağ erişim sağlar. Merhaba portal'ı kullanmanızı olduğunda örtülü reddetme kuralı en düşük öncelik toodeny hello her şeyi. Derleme olan, kuralları izin verir.

ASE'de, erişim toohello kullanılan VM'ler toohost hello ana kendisini yok. Bunlar, Microsoft tarafından yönetilen bir abonelikte demektir. Merhaba ana toorestrict erişim toohello uygulamaları istiyorsanız Nsg'ler hello ana alt ağda ayarlayın. Bunu yaparken dikkatli toohello ana bağımlılıkları dikkat edin. Bağımlılıkları engellerseniz hello ana çalışmayı durdurur.

Nsg'ler hello Azure portal veya PowerShell aracılığıyla yapılandırılabilir. Burada Hello bilgileri hello Azure portal gösterir. Oluşturma ve altında en üst düzey bir kaynak olarak hello Portalı'nda Nsg'ler yönetme **ağ**.

Merhaba gelen ve giden gereksinimlerini dikkate alınır, hello Nsg'ler Bu örnekte gösterilen benzer toohello Nsg'ler görünmelidir. Merhaba VNet adres aralığı olan _192.168.250.0/16_, ve hello ana bulunduğu hello alt _192.168.251.128/25_.

Bu örnekte hello listesinin hello üstünde ilk iki gelen gereksinimleri hello ana toofunction Hello gösterilmektedir. Bunlar ana yönetim etkinleştirin ve hello ana toocommunicate kendisiyle verin. Merhaba diğer girişler tüm Kiracı yapılandırılabilir ve ağ erişim toohello ana barındırılan uygulamalar yönetebilirler. 

![Gelen güvenlik kuralları][4]

Varsayılan kural hello IP'leri hello sanal tootalk toohello ana alt sağlar. Başka bir varsayılan kural hello yük dengeleyici, olarak da bilinen hello genel VIP hello ana ile toocommunicate sağlar. toosee hello varsayılan kuralları seçin **varsayılan kuralları** sonraki toohello **Ekle** simgesi. Merhaba NSG gösterilen kuralları sonra şey kural reddetme yerleştirirseniz hello VIP ve hello ana arasındaki trafiği engeller. gelen tooprevent trafik Vnet'in hello içinde kendi kural tooallow ekleme gelen. Bir hedef kaynak eşit tooAzureLoadBalancer kullanmak **herhangi** ve bir bağlantı noktası aralığı  **\*** . Merhaba NSG kural uygulanan toohello ana alt ağı olduğundan, toobe özel hello hedef gerekmez.

Bir IP adresi tooyour uygulama atanmışsa, bağlantı noktalarını açmak hello tutmak emin olun. toosee hello bağlantı noktalarını seçin **uygulama hizmeti ortamı** > **IP adreslerini**.  

Giden Kuralları aşağıdaki hello gösterilen tüm hello öğeler hello son öğenin dışında gereklidir. Bunlar, bu makalenin önceki bölümlerinde belirtilenlerle ağ erişim toohello ana bağımlılıkları etkinleştirin. Bunlardan herhangi birinin engellerseniz, ana çalışmayı durdurur. Merhaba listesindeki son öğeyi Merhaba, ana toocommunicate kullanarak sanal ağınızdaki diğer kaynaklarla sağlar.

![Giden güvenlik kuralları][5]

Nsg'lerinizi tanımlandıktan sonra bunları, ana açıktır toohello alt atayın. Merhaba ana sanal ağ veya alt ağ hatırlamıyorsanız hello ana Yönetim Portalı'ndan görebilirsiniz. tooassign NSG tooyour alt Merhaba, toohello alt UI gidin ve hello NSG seçin.

## <a name="routes"></a>Yollar ##

Azure ExpressRoute ile ağınızı yapılandırırken yollara en yaygın olarak sorunlu dönüşür. Üç türde bir sanal ağda yollar vardır:

-   Sistem yolları
-   BGP yolları
-   Kullanıcı tanımlı yollar (Udr'ler)

BGP yolları sistem yolları geçersiz kılar. BGP yolları Udr'ler geçersiz. Azure sanal ağlar yollar hakkında daha fazla bilgi için bkz: [kullanıcı tanımlı yollar genel bakış][UDRs].

Hello ana toomanage hello sistem kullandığını hello Azure SQL veritabanı güvenlik duvarı vardır. Merhaba ana genel VIP gelen iletişimi toooriginate gerektirir. Merhaba ExpressRoute bağlantısı aşağı ve başka bir IP adresi çıkış gönderilirse bağlantıları toohello SQL hello ana veritabanından reddedilir.

ExpressRoute hello yanıtları tooincoming yönetim isteği gönderirse hello yanıt adresi hello özgün hedef farklıdır. Bu uyuşmazlık hello TCP iletişimi keser.

Sanal ağınızı bir ExpressRoute ile yapılandırılırken, ana toowork için hello kolay şey toodo şöyledir:

-   ExpressRoute tooadvertise yapılandırma _0.0.0.0/0_. Varsayılan olarak, zorla tünel giden tüm trafiği şirket içi.
-   Bir UDR oluşturun. Bir adres öneki ile Merhaba ana içeren toohello alt ağ geçerli _0.0.0.0/0_ ve bir sonraki atlama türü _Internet_.

Bu iki değişiklik yaparsanız, hello ana alt ağdan kaynaklanan Internet hedefleyen trafiğe works hello ExpressRoute ve hello ana aşağı zorlanmaz. 

> [!IMPORTANT]
> bir UDR tanımlanan hello rotalar yeterince spesifik tootake öncelik hello ExpressRoute yapılandırma tarafından tanıtılan yollar üzerinde olmalıdır. Merhaba önceki örnekte hello geniş 0.0.0.0/0 adres aralığını kullanır. Bu büyük olasılıkla yanlışlıkla daha belirli adres aralıkları Yol tanıtımlarını tarafından geçersiz kılınabilir.
>
> ASEs yolundan hello ortak eşleme yolu toohello özel eşliği yollarını arası tanıtmanız ExpressRoute yapılandırmalarla desteklenmez. Microsoft'tan Yol tanıtımlarını ilgili yapılandırılmış ortak eşleme ile ExpressRoute yapılandırmaları. Merhaba reklam çok sayıda Microsoft Azure IP adres aralıklarını içerir. Merhaba özel eşliği yolda arası tanıtılan Hello adres aralıkları, tüm giden ağ paketlerinin hello ana'nın alt ağdan zorlamalı tünel tooa müşterinin şirket içi ağ altyapısı demektir. Bu ağ akışı ASEs ile şu anda desteklenmiyor. Bir çözüm toothis hello ortak eşleme yolu toohello özel eşliği yolu toostop arası reklam yolları sorunudur.

toocreate bir UDR şu adımları izleyin:

1. Toohello Azure portalına gidin. Seçin **ağ** > **yol tablosu**.

2. Hello yeni bir yol tablosu oluşturmanız sanal ağınızı aynı bölgede.

3. Kullanıcı Arabirimi, rota tablosu içindeki seçin **yollar** > **Ekle**.

4. Set hello **sonraki atlama türü** çok**Internet** ve hello **adres ön eki** çok**0.0.0.0/0**. **Kaydet**’i seçin.

    Ardından hello aşağıdaki gibi bir şey görürsünüz:

    ![İşlev yolları][6]

5. Merhaba yeni yol tablosu oluşturduktan sonra ana içeren toohello alt gidin. Yol tablosu hello portalında hello listeden seçin. Merhaba değişiklik kaydettikten sonra hello Nsg'ler ve yolları, alt ağ ile belirtildiği sonra görmeniz gerekir.

    ![Nsg'ler ve yolları][7]

### <a name="deploy-into-existing-azure-virtual-networks-that-are-integrated-with-expressroute"></a>ExpressRoute ile tümleşik olan Azure sanal ağlarda dağıtma ###

toodeploy, ana ExpressRoute ile tümleşik bir VNet içine önceden dağıtılan hello ana istediğiniz hello alt ağ. Resource Manager şablonu toodeploy kullanın. toocreate bir ana sanal ağda zaten yapılandırılmış ExpressRoute sahiptir:

- Bir alt ağ toohost hello ana oluşturun.

    > [!NOTE]
    > Hiçbir şey hello alt ancak hello ana olabilir. Emin toochoose Gelecekteki büyümeyi de izin veren bir adres alanı olması. Bu ayarı daha sonra değiştiremezsiniz. Dosya boyutu öneririz `/25` 128 adreslerine sahip.

- Daha önce açıklandığı gibi Udr'ler (örneğin, yol tablolarını) oluşturun ve hello alt ağda ayarlayın.
- Hello ana açıklandığı gibi bir Resource Manager şablonunu kullanarak oluşturduğunuz [Resource Manager şablonu kullanarak bir ana oluşturma][MakeASEfromTemplate].

<!--Image references-->
[1]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow.png
[2]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow2.png
[3]: ./media/network_considerations_with_an_app_service_environment/networkase-ipaddresses.png
[4]: ./media/network_considerations_with_an_app_service_environment/networkase-inboundnsg.png
[5]: ./media/network_considerations_with_an_app_service_environment/networkase-outboundnsg.png
[6]: ./media/network_considerations_with_an_app_service_environment/networkase-udr.png
[7]: ./media/network_considerations_with_an_app_service_environment/networkase-subnet.png

<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[ASEManagement]: ./management-addresses.md
