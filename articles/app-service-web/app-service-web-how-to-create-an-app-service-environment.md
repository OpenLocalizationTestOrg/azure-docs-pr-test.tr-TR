---
title: "aaaHow tooCreate bir uygulama hizmeti ortamı v1"
description: "Bir uygulama hizmeti ortamı v1 oluşturma akış açıklaması"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 81bd32cf-7ae5-454b-a0d2-23b57b51af47
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 95feb33854eee5bac02fa68b066e2fc10eb3fede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-app-service-environment-v1"></a>Nasıl tooCreate bir uygulama hizmeti ortamı v1 

> [!NOTE]
> Uygulama hizmeti ortamı v1 hello hakkında makaledir. Merhaba, daha kolay toouse ve daha güçlü altyapısı üzerinde çalışan uygulama hizmeti ortamı'nın daha yeni bir sürümü var. Merhaba yeni sürümü hakkında daha fazla ile Merhaba Başlat toolearn [giriş toohello uygulama hizmeti ortamı](../app-service/app-service-environment/intro.md).
> 

### <a name="overview"></a>Genel Bakış
Merhaba uygulama hizmeti ortamı (ana) bir Premium hizmet hello çok Kiracı damga olarak kullanılabilir bir Gelişmiş Yapılandırma özelliği sunan Azure App Service seçeneğidir. Merhaba ana özellik temelde hello Azure uygulama hizmeti bir müşterinin sanal ağda dağıtır. App Service ortamları tarafından hello yeteneklerini daha iyi bir anlayışa sunulan toogain okuma hello [bir uygulama hizmeti ortamı nedir] [ WhatisASE] belgeleri.

### <a name="before-you-create-your-ase"></a>Ana oluşturmadan önce
Önemli toobe değiştiremezsiniz hello şey uyumlu değil. Oluşturulduktan sonra ana hakkında değiştiremezsiniz bu yönleri şunlardır:

* Konum
* Abonelik
* Kaynak Grubu
* Kullanılan sanal ağ
* Kullanılan alt ağ 
* Alt ağ boyutu

Ne zaman bir VNet çekme ve bir alt ağ belirterek emin olun, gelecekteki büyümesine büyüklükte tooaccomodate değil. 

### <a name="creating-an-app-service-environment-v1"></a>Hizmet ortamı v1 bir uygulama oluşturma
toocreate toosearch gereken bir uygulama hizmeti ortamı v1 hello Azure Market ***uygulama hizmeti ortamı v1***, veya yeni giderek -> Web + mobil -> uygulama hizmeti ortamı. toocreate bir ASEv1:

1. Merhaba, ana adını sağlayın. Merhaba ana için belirtilen hello adı hello ana oluşturulan hello uygulamalar için kullanılır. Merhaba ana adı appsvcenvdemo ise hello alt etki alanı adı olacaktır. *appsvcenvdemo.p.azurewebsites.net*. Bu nedenle adlı bir uygulama oluşturduysanız *mytestapp* adresindeki adreslenebilir sonra *mytestapp.appsvcenvdemo.p.azurewebsites.net*. Merhaba, ana adlarında boşluk kullanamazsınız. Büyük harf karakterler hello adı kullanırsanız, hello etki alanı adı hello toplam küçük harfli sürümünü bu adı olacaktır. Bir ILB kullanırsanız, ardından ana adınızı alt etki alanı içinde kullanılmaz, ancak bunun yerine ana oluşturma sırasında açıkça belirtilmiştir
   
    ![][1]
2. Aboneliğinizi seçin. hello abonelik için ana kullanılan Ayrıca bu ana tüm uygulamaları ile oluşturulan hello bir yerdir. Başka bir abonelikte bir VNet içinde ana yerleştirilemiyor
3. Seçin veya yeni bir kaynak grubu belirtin. Merhaba kaynak grubu için ana kullanılan gerekir olması hello ağınız için kullanılan aynı. Önceden var olan bir sanal ağ seçin sonra hello kaynak grubu seçimi, ana için güncelleştirilmiş tooreflect olacaktır, sanal ağınızı.
   
    ![][2]
4. Sanal ağ ve konum seçimlerinizi yapın. Yeni bir VNet toocreate seçin veya önceden var olan bir sanal ağı seçin. Ardından, yeni bir sanal ağ seçerseniz bir ad ve konum belirtebilirsiniz. Merhaba yeni VNet hello adres aralığı 192.168.250.0/23 adlı bir alt ağ olacaktır **varsayılan** 192.168.250.0/24 tanımlanır. Önceden varolan Klasik veya Resource Manager Vnet'i kısaca seçebilirsiniz. Merhaba VIP türü seçimi belirler, ana hello doğrudan erişilebilir değilse Internet (harici) veya bir iç yük dengeleyici (ILB) kullanır. bunları okuyun hakkında daha fazla toolearn [bir uygulama hizmeti ortamı ile bir iç yük dengeleyici kullanarak][ILBASE]. Dış VIP türü seçerseniz kaç dış IP adresleri hello sistem IPSSL amacıyla oluşturulur seçebilirsiniz. Daha sonra iç seçerseniz, ana kullanacağı toospecify hello alt etki alanı gerekir. ASEs kullanan sanal ağları içinde dağıtılabilir *ya da* ortak adres aralıklarını *veya* RFC1918 adres alanları (özel adresleri). Sipariş toouse bir ortak adres aralığına sahip bir sanal ağ'da, önceden toocreate hello VNet gerekir. Önceden var olan bir VNet seçtiğinizde ana oluşturma sırasında toocreate yeni bir alt ağ gerekir. **Merhaba Portalı'nda önceden oluşturulmuş bir alt ağ kullanılamıyor. Resource manager şablonu kullanarak, ana oluşturursanız, önceden var olan bir alt ağ ile bir ana oluşturabilirsiniz.** bir şablondan bir ana toocreate hello bilgileri burada kullanır [şablonundan bir uygulama hizmeti ortamı oluşturma] [ ILBAseTemplate] ve burada [şablonundanbirILBuygulamahizmetiortamıoluşturma] [ASEfromTemplate].

### <a name="details"></a>Ayrıntılar
Bir ana 2 ön uçlar ve 2 çalışan ile oluşturulur. Merhaba ön uçlar hello HTTP/HTTPS uç noktalar olarak davranmasına ve uygulamalarınızı barındırmak hello rolleri olan toohello çalışanları trafiği göndermek. Ana oluşturulduktan sonra hello miktar ayarlayabilir ve hatta ayarlama Bu kaynak havuzlarının otomatik ölçeklendirme kurallarını kullanabilirsiniz. Yönetim ve izleme bir uygulama hizmeti ortamı el ile ölçeklendirme geçici daha fazla ayrıntı için buraya gidin: [nasıl tooconfigure bir uygulama hizmeti ortamı][ASEConfig] 

Yalnızca hello bir ana hello alt ağdaki ana hello tarafından kullanılan bulunabilir. Merhaba alt hello ana dışında her şey için kullanılamaz

### <a name="after-app-service-environment-v1-creation"></a>Uygulama hizmeti ortamı v1 oluşturulduktan sonra
Ana oluşturulduktan sonra ayarlayabilirsiniz:

* Ön uçlar miktarını (en az: 2)
* Çalışanlar miktarını (en az: 2)
* IP SSL için kullanılabilir IP adresleri miktarı
* Ön uçlar veya çalışanları Hello tarafından kullanılan kaynak boyutları işlem (ön uç minimum boyut olan P2)

El ile ölçeklendirme, yönetim ve burada App Service ortamları izleme etrafında daha fazla ayrıntı: [nasıl tooconfigure bir uygulama hizmeti ortamı][ASEConfig] 

Otomatik ölçeklendirme hakkında bilgi için yoktur burada bir kılavuz: [nasıl tooconfigure otomatik bir uygulama hizmeti ortamı için ölçeklendirme][ASEAutoscale]

Özelleştirme gibi hello veritabanı ve depolama için kullanılabilir olmayan ek bağımlılıklar vardır. Bunlar Azure tarafından işlenen ve hello sistemi ile gelir. tüm uygulama hizmeti ortamı için too500 GB yukarı Hello sistem depolama destekler hello ve hello veritabanı hello sistem hello ölçek tarafından gerektiği şekilde Azure tarafından ayarlanır.

## <a name="getting-started"></a>Başlarken
Tüm makaleler ve nasıl-için uygulama hizmeti ortamları hello kullanılabilir için kullanıcının [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).

Uygulama hizmeti ortamı v1 ile başlatılan tooget bakın [giriş toohello uygulama hizmeti ortamı v1][WhatisASE]

Hello Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-basecreateblade.png
[2]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-vnetcreation.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
[ILBAseTemplate]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-create/
[ASEfromTemplate]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-create-ilb-ase-resourcemanager/
