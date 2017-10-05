---
title: "Web Apps ile üretim testine başlayın"
description: "Azure App Service Web Apps üretim (TIP) özelliğinde testi hakkında bilgi edinin."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 9f38b635140cacf0513c75385bce3c110a930969
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a>Web Apps ile üretim testine başlayın
Üretimde test ya da canlı web uygulamanızı gerçek müşteri trafiğinden kullanarak sınama olan uygulama geliştiriciler giderek kolay bir şekilde entegre bir test stratejisi kendi [Çevik Geliştirme](https://en.wikipedia.org/wiki/Agile_software_development) Metodoloji. Bir test ortamında birleştirilen verileri aksine, üretim ortamında test uygulamalarınızı dinamik kullanıcı trafiği ile kalitesi sağlar. Yeni uygulamanızı gerçek kullanıcılara göstererek dağıtıldıktan sonra uygulamanızı karşılaşabilecekleri gerçek sorunlar hakkında haberdar olmak. İşlevselliği, performans ve uygulama güncelleştirmelerinizi birim, hız ve hiçbir zaman bir sınama ortamında yaklaşık gerçek kullanıcı trafiği çeşitli karşı değerini doğrulayabilirsiniz.

## <a name="traffic-routing-in-app-service-web-apps"></a>App Service Web Apps yönlendirme trafiği
Trafik yönlendirme özelliğindeki [Azure uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714), bir veya daha fazla dinamik kullanıcı trafiğinin bir kısmı yönlendirebilirsiniz [dağıtım yuvaları](web-sites-staged-publishing.md)ve uygulamanızı ile analiz etmek [Azure Application Insights](/services/application-insights/) veya [Azure Hdınsight](/services/hdinsight/), veya bir üçüncü taraf aracı [New Relic](/marketplace/partners/newrelic/newrelic/) değişikliğinizin doğrulamak için. Örneğin, App Service ile aşağıdaki senaryolar uygulayabilirsiniz:

* İşlev hataları bulmaya veya performans sorunları, güncelleştirmelerinin site genelinde dağıtımdan sabitleme
* Değişikliklerinizi "denetimli test uçuşlar" beta uygulama kullanılabilirlik ölçümleri ölçerek gerçekleştirin
* Aşamalı olarak yeni bir güncelleştirme kadar artırmalarını ve bir hata oluşursa düzgün biçimde geçerli sürüme geri 
* Çalıştırarak, uygulamanızın iş sonuçları en iyi duruma getirme [A / B testler](https://en.wikipedia.org/wiki/A/B_testing) veya [multivariate testleri](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) içinde birden çok dağıtım yuvası

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a>Trafik yönlendirme Web uygulamalarında kullanma gereksinimleri
* Web uygulamanızı çalıştırmak gerekir **standart** veya **Premium** birden çok dağıtım yuvası için gerekli olduğundan, katmanı.
* Düzgün çalışması için kullanıcıların tarayıcıda etkinleştirilmesi için tanımlama bilgileri trafik yönlendirme gerektirir. Trafik yönlendirme, bir dağıtım yuvası ömrü istemci tarayıcısına istemci oturumu sabitlemek için tanımlama bilgilerini kullanır.
* Trafik yönlendirme Azure PowerShell cmdlet'leri aracılığıyla Gelişmiş ipucu senaryolarını destekler.

## <a name="route-traffic-segment-to-a-deployment-slot"></a>Rota trafiği kesimine bir dağıtım yuvası
Her ipucu senaryosu temel düzeyde, bir üretim dışı dağıtım yuvası Canlı trafiğinizi önceden tanımlanmış yüzdesi rota. Bunu yapmak için aşağıdaki adımları izleyin:

> [!NOTE]
> Adımlar burada varsayar sahip olduğunuz bir [üretim dışı dağıtım yuvası](web-sites-staged-publishing.md) ve istenen web uygulama içeriğini zaten olan [dağıtılan](web-sites-deploy.md) ona.
> 
> 

1. İçine oturum [Azure Portal](https://portal.azure.com/).
2. Web uygulamanızın dikey penceresinde tıklayın **ayarları** > **trafik yönlendirme**.
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. Trafiği için ve işlemleriniz ve'ı tıklatın toplam trafiğin yüzde yönlendirmek istediğiniz yuvası seçin **kaydetmek**.
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. Dağıtım yuvanın dikey penceresine gidin. Dinamik trafik için yönlendirilen görmelisiniz.
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

Trafik yönlendirme yapılandırıldıktan sonra istemciler belirtilen yüzdesi, üretim dışı yuvasına rastgele yönlendirilir. Ancak, istemci otomatik olarak belirli bir yuva yönlendirilir sonra bunu "için bu istemci oturumu için o yuva sabitlenir olduğunu" dikkate almak önemlidir. Bu yapılan kullanıcı oturumunu sabitlemek için bir tanımlama bilgisi kullanarak. HTTP isteklerini inceleyin, bulacaksınız bir `TipMix` sonraki her istekte tanımlama bilgisi.

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-to-a-specific-slot"></a>İstemci isteklerini belirli bir yuva zorla
Otomatik trafik yönlendirme ek olarak, uygulama hizmeti rota isteklerini belirli bir yuva için kullanabilirsiniz. Kullanıcılarınızı opt içine yapılamıyor veya geri çevirin, beta uygulamanızın olarak istediğinizde kullanışlıdır. Bunu yapmak için kullandığınız `x-ms-routing-name` sorgu parametresi.

Belirli yuvası kullanarak kullanıcıların bildirmeksizin `x-ms-routing-name`, yuva trafik yönlendirme listesine zaten eklenmiş olduğundan emin olmanız gerekir. Bir yuva açıkça yönlendirmek istediğiniz olduğundan, ayarladığınız gerçek yönlendirme yüzdesi önemli değildir. İsterseniz, "beta uygulamaya erişmek için tıklatabileceği bir beta bağlantı" hazırlayabilirsiniz.

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a>Kullanıcılar beta uygulama dışında iptal et
Beta uygulamanızı dışında opt kullanıcılar izin vermek için örneğin, bu bağlantıyı web sayfanıza koyabilirsiniz:

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back to production app</a>

Dize `x-ms-routing-name=self` üretim yuvasına belirtir. İstemci tarayıcısı erişim sonra bağlantı, yalnızca üretim yuvasına yönlendirilir, ancak sonraki her istek içerecek `x-ms-routing-name=self` üretim yuvasına oturumuna sabitler tanımlama bilgisi.

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-to-beta-app"></a>Kullanıcılar beta uygulamasına iptal et
Beta uygulamanıza kabul kullanıcıların izin vermek için aynı sorgu parametresi örneğin üretim dışı yuva adını ayarlayın:

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a>Diğer kaynaklar
* [Hazırlık ortamları için Azure App Service'te web uygulamalarını ayarlama](web-sites-staged-publishing.md)
* [Azure'nın beklendiği karmaşık bir uygulama dağıtma](app-service-deploy-complex-application-predictably.md)
* [Azure App Service ile Çevik Yazılım Geliştirme](app-service-agile-software-development.md)
* [DevOps ortamları etkili bir şekilde web uygulamaları için kullanın](app-service-web-staged-publishing-realworld-scenarios.md)

