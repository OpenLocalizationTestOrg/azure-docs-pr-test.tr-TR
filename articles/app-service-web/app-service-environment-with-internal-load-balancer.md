---
title: "aaaCreating ve bir iç yük dengeleyici bir uygulama hizmeti ortamı ile kullanma | Microsoft Docs"
description: "Oluşturma ve bir ana bir ILB ile kullanma"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: ad9a1e00-d5e5-413e-be47-e21e5b285dbf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 20799f260993d6e81499408e5b547a2e21430174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-an-internal-load-balancer-with-an-app-service-environment"></a>Bir iç yük dengeleyici ile uygulama hizmeti ortamı kullanma

> [!NOTE] 
> Uygulama hizmeti ortamı v1 hello hakkında makaledir. Merhaba, daha kolay toouse ve daha güçlü altyapısı üzerinde çalışan uygulama hizmeti ortamı'nın daha yeni bir sürümü var. Merhaba yeni sürümü hakkında daha fazla ile Merhaba Başlat toolearn [giriş toohello uygulama hizmeti ortamı](../app-service/app-service-environment/intro.md).
>

Merhaba uygulama hizmeti ortamı (ana) özelliği, hello çok Kiracı damga olarak kullanılabilir bir Gelişmiş Yapılandırma özelliği sunan Azure App Service'in Premium hizmet seçeneğidir. Merhaba ana özellik temelde hello Azure App Service, Azure sanal Network(VNet) içinde dağıtır. App Service ortamları tarafından hello yeteneklerini daha iyi bir anlayışa sunulan toogain okuma hello [bir uygulama hizmeti ortamı nedir] [ WhatisASE] belgeleri. Sanal ağ içinde işletim hello faydası hello bilmiyorsanız [Azure Virtual Network SSS][virtualnetwork]. 

## <a name="overview"></a>Genel Bakış
Bir ana sanal ağınızı bir IP adresi veya bir internet erişilebilir uç nokta ile dağıtılabilir. Sipariş tooset başlangıç IP adresi tooa VNet adres, ana bir iç yük Balancer(ILB) ile toodeploy gerekir. Ana bir ILB ile yapılandırıldığında, sağlar:

* kendi etki alanı veya alt etki alanı. toomake kolay, alt etki alanı, ancak bu belgenin varsayar, her iki durumda da yapılandırabilirsiniz. 
* HTTPS için kullanılan hello sertifikası
* Alt etki alanı için DNS yönetimi. 

Buna karşılık, sizin gibi şeyler yapabilir:

* İş kolu uygulamaları, güvenli bir şekilde hello içinde gibi ana bilgisayar intranet uygulamalarını hangi erişim Site tooSite veya ExpressRoute VPN aracılığıyla bulut
* ana bilgisayar genel DNS sunucuları listelenmeyen hello bulut uygulamalarında
* ön uç uygulamalarınızı güvenli bir şekilde ile tümleştirebilirsiniz yalıtılmış Internet arka uç uygulamaları oluşturma

#### <a name="disabled-functionality"></a>Devre dışı bırakılan işlevsellik
Bir ILB ana kullanırken yapamayacağınız bazı şeyler vardır. Bu konuları içerir:

* IPSSL kullanma
* IP toospecific uygulamaları adresleri atama
* satın alma ve hello portal aracılığıyla bir uygulama ile bir sertifika kullanıyor. Elbette yine bir sertifika yetkilisi ile doğrudan sertifikaları almak ve uygulamalarınızda hello Azure portalı üzerinden yalnızca değil kullanın.

## <a name="creating-an-ilb-ase"></a>Bir ILB ana oluşturma
Bir ILB ana oluşturma bir ana normalde oluşturma çok farklı değildir. Bir ana oluşturma hakkında daha ayrıntılı bir tartışma için okuma [nasıl tooCreate bir uygulama hizmeti ortamı][HowtoCreateASE]. bir ILB ana olduğu hello işlem toocreate hello ana oluşturma sırasında bir VNet oluşturma veya varolan bir sanal ağ seçme arasında aynı. bir ILB ana toocreate: 

1. Hello Azure portal seçin, **yeni -> Web + mobil -> uygulama hizmeti ortamı**
2. Aboneliğinizi seçin
3. Bir kaynak grubu seçin veya oluşturun
4. Bir VNet oluşturun veya seçin
5. Bir sanal ağı seçerek bir alt ağ oluşturun
6. Seçin **sanal ağ konumu sanal ağ yapılandırması ->** ve kümesi hello VIP türü tooInternal
7. (Bu ana içinde oluşturulan uygulamaları için kullanılan hello alt etki alanı olacaktır) alt etki alanı adı sağlayın
8. Tamam'ı seçin ve ardından oluşturun

![][1]

Merhaba sanal ağ Dikey içinde bir sanal ağ yapılandırma seçeneği yoktur. Bir dış VIP veya iç VIP arasında bu sağlar. Merhaba, dış varsayılandır. TooExternal ayarlanmalıdır varsa, ana Internet erişilebilir VIP kullanır. Dahili seçerseniz, ana sanal ağınızın içinde bir IP adresinde bir ILB ile yapılandırılır. 

Dahili seçtikten sonra ana kaldırılır tooyour daha fazla IP adres özelliği tooadd hello ve bunun yerine hello ana tooprovide hello alt etki gerekir. Bir dış VIP hello ile bir ana hello ana adını hello alt etki alanı içinde bu ana oluşturulan uygulamalar için kullanılır. Ana çağrıldıklarında ***contosotest*** ve o ana uygulamanızda çağrıldı ***mytest*** hello alt etki alanı hello biçimi şu şekilde olacaktır ***contosotest.p.azurewebsites.net*** ve Merhaba bu uygulama için URL olacaktır ***mytest.contosotest.p.azurewebsites.net***. Merhaba VIP türü tooInternal ayarlarsanız, ana adınızı hello alt etki alanı içinde ana hello için kullanılmaz. Merhaba alt etki alanı açıkça belirtin. Alt etki alanı varsa ***contoso.corp.net*** ve ana adlı içeren bir uygulama tarafından ***timereporting*** bu uygulama olacaktır için URL hello ***timereporting.contoso.corp.net***.

## <a name="apps-in-an-ilb-ase"></a>Bir ILB ana uygulamalar
ILB ASE'de bir uygulama oluşturma olduğu hello ASE'de normalde bir uygulama oluşturma aynıdır. 

1. Hello Azure portal seçin, **yeni -> Web + mobil -> Web** veya **mobil** veya **API uygulaması**
2. Uygulama adını girin
3. Abonelik seçme
4. Kaynak grubu seçin veya oluşturun
5. Uygulama hizmeti Plan(ASP) oluşturun veya seçin. Yeni bir ASP ardından oluşturarak, ana hello konumu ve select hello çalışan havuzunda belirlerseniz, oluşturulan, ASP toobe istiyorsunuz. Merhaba ASP oluşturduğunuzda hello konumu ve hello çalışan havuzu, ana seçin. Bu hello alt etki alanı altında görürsünüz hello uygulamasının hello adı belirttiğinizde, uygulama adı, ana için hello alt etki alanına değiştirilir. 
6. Bu seçeneği belirleyin. Merhaba seçmelisiniz **PIN toodashboard** hello uygulama tooshow yukarı Panonuzda istiyorsanız onay kutusunu. 

![][2]

Merhaba uygulama altında hello alt etki alanı adı, ana güncelleştirilmiş tooreflect hello alt etki alır. 

## <a name="post-ilb-ase-creation-validation"></a>POST ILB ana oluşturma doğrulama
Bir ILB ana hello olmayan - ILB ana değerinden biraz farklıdır. Zaten kendi DNS toomanage gerekir ve tooprovide kullanarak kendi sertifikanızı HTTPS bağlantıları için de not almıştınız. 

Ana oluşturduktan sonra bu hello alt etki alanı gösterir hello alt etki alanı belirttiğiniz ve hello yeni bir öğe olduğu fark edeceksiniz **ayarı** adlı menüsü **ILB sertifika**. Merhaba ana daha kolay tootest HTTPS kolaylaştırır otomatik olarak imzalanan bir sertifika ile oluşturulur. Merhaba portalı kullanarak kendi sertifikanızı tooprovide HTTPS için gerekir, ancak toodrive budur size bildirir, alt etki alanı ile giden bir sertifika toohave. 

![][3]

IIS MMC şeyler yalnızca çalıştığınız ve nasıl toocreate bir sertifika, kullanabileceğiniz bilmiyorsanız hello self bir konsol uygulaması toocreate imzalı sertifika. Bir kez oluşturulduktan sonra bir .pfx dosyası olarak dışarı aktarma ve hello ILB sertifika UI yükleyin. Ne zaman otomatik olarak imzalanan bir sertifika, tarayıcınızı güvenli bir site eriştiğiniz site hello bir uyarı verir erişim toohello bağlanamama toovalidate hello sertifika güvenli değildir. Bu uyarı tooavoid istiyorsanız, alt etki alanı ile eşleşen ve bir tarayıcınız tarafından kabul edilen güven zinciri olan doğru imzalı bir sertifika gerekir.

![][6]

İsterseniz tootry hello kendi sertifikalarla akış ve HTTP ve HTTPS erişim tooyour ana test:

1. Ana oluşturulduktan sonra tooASE UI Git **ana ayarları -> ILB sertifikalar ->**
2. Sertifika pfx dosyasını seçerek ILB sertifika ayarlayın ve parola belirtin. Bu adım sırasında tooprocess biraz alır ve bir ölçeklendirme işlemi devam ediyor hello iletisi gösterilir.
3. Merhaba ILB adresini almak için ana (**ana -> Özellikler sanal IP adresi ->**)
4. İçinde ana oluşturulduktan sonra bir web uygulaması oluşturma 
5. Bu VNET içinde yoksa, bir VM oluşturma (de hello aynı alt ağda hello ana veya şeyler sonu)
6. DNS alt etki alanı için ayarlayın. Joker karakter ile alt etki alanı DNS sunucunuzun kullanın veya bazı basit testler toodo istiyorsanız VM tooset web uygulaması adı tooVIP IP adresinizi hello hosts dosyasını düzenleyin. Merhaba alt etki alanı adı, ana olsaydı. ilbase.com ve yapılan mytestapp.ilbase.com ele ardından hosts dosyasında kümesi böylece web uygulama mytestapp hello. (Windows hello hosts C:\Windows\System32\drivers\etc\ dosyasıdır)
7. Bu VM üzerinde bir tarayıcı kullanın ve toohttp://mytestapp.ilbase.com (veya web uygulaması adı, alt etki alanı ile ne olursa olsun) gidin
8. Bu VM üzerinde bir tarayıcı kullanın ve kendinden imzalı bir sertifika kullanıyorsanız tooaccept hello güvenlik olmaması gerekir toohttps://mytestapp.ilbase.com gidin. 

Başlangıç IP adresi, ILB için özelliklerinizi hello sanal IP adresi listelenir

![][4]

## <a name="using-an-ilb-ase"></a>Bir ILB ana kullanma
#### <a name="network-security-groups"></a>Ağ Güvenlik Grupları
Bir ILB ana etkinleştirir ağ yalıtımı, uygulamalarınız için hello uygulamaları erişilebilir veya olarak da bilinen olmayan gibi internet hello. İş kolu uygulamaları gibi intranet siteleri barındırmak için mükemmel budur. Toorestrict erişim bile gerektiğinde daha fazla ağ güvenlik Groups(NSGs) toocontrol erişim hello ağ düzeyinde kullanmaya devam edebilirsiniz. 

Toouse Nsg'ler toofurther erişimi kısıtlayın sonra toomake hello iletişimi bozmadığını emin ihtiyacınız istiyorsanız bu hello ana sipariş toooperate gerekir. Hello HTTP/HTTPS erişim olsa bile yalnızca hello ILB ana hala kaynak hello VNet dışında bağlıdır ana hello hello tarafından kullanılır. hangi ağ erişimi toosee hala gerekli hello belgedeki hello bilgiler göz [gelen trafiği denetleme tooan uygulama hizmeti ortamı] [ ControlInbound] ve hello belgeyi [ağ ExpressRoute ile uygulama hizmeti ortamları için yapılandırma ayrıntılarını][ExpressRoute]. 

Nsg'lerinizi tooknow hello IP ihtiyacınız olan adres tooconfigure, ana Azure toomanage tarafından kullanılır. Internet istekleri yapıyorsa bu IP adresi hello giden IP adresinden, ana de değil. Merhaba, ana giden IP adresini, ana hello yaşam süreleri boyunca statik kalır. Ana silip yeni bir IP adresi alırsınız. Bu IP adresi Git çok toofind**ayarlar -> Özellikler** ve hello bulur **giden IP adresi**. 

![][5]

#### <a name="general-ilb-ase-management"></a>Genel ILB ana Yönetimi
Bir ILB ana yönetme olan büyük ölçüde hello bir ana normalde yönetme aynıdır. Ön uç sunucuları artan toohandle miktarda HTTP/HTTPS trafiğini ölçeklendirme ve daha fazla ASP örnekleri, çalışan havuzları toohost tooscale gerekir. Bir ana hello yapılandırmasını yönetme ile ilgili genel bilgiler için hello belgeyi okumaya devam [uygulama hizmeti ortamını yapılandırma][ASEConfig]. 

Merhaba ek yönetim sertifikası ve DNS Yönetimi öğelerdir. ILB ana oluşturulduktan sonra HTTPS için kullanılan hello sertifikasını karşıya yükle tooobtain gerekir ve süresi dolmadan önce değiştirin. Azure hello temel etki alanına sahip olduğundan biz ASEs bir dış VIP ile sertifikalar sağlayabilir. Merhaba alt etki alanı bir ILB ana tarafından kullanılan herhangi bir şey olamayacağından tooprovide HTTPS için kendi sertifika gerekir. 

#### <a name="dns-configuration"></a>DNS yapılandırması
Ne zaman bir dış VIP hello DNS kullanılarak Azure tarafından yönetilir. Ana oluşturulan herhangi bir uygulama tooAzure ortak bir DNS olan DNS otomatik olarak eklenir. ILB ASE'de kendi DNS toomanage sahip. Belirli bir alt etki alanı contoso.corp.net gibi bu noktası tooyour ILB adres için DNS A kayıtlarını toocreate gerekir:

    * 
    *.SCM ftp yayımlama 


## <a name="getting-started"></a>Başlarken
Tüm makaleler ve nasıl-için uygulama hizmeti ortamları hello kullanılabilir için kullanıcının [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).

Uygulama hizmeti ortamları ile çalışmaya tooget bakın [giriş tooApp Service ortamları][WhatisASE]

Hello Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createilbase.png
[2]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createapp.png
[3]: ./media/app-service-environment-with-internal-load-balancer/ilbase-newase.png
[4]: ./media/app-service-environment-with-internal-load-balancer/ilbase-vip.png
[5]: ./media/app-service-environment-with-internal-load-balancer/ilbase-externalvip.png
[6]: ./media/app-service-environment-with-internal-load-balancer/ilbase-ilbcertificate.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[vnetnsgs]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
