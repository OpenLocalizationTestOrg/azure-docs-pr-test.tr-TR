---
title: "Web uygulamaları için üretim aşamasındaki bir test kullanmaya aaaGet"
description: "Azure App Service Web Apps üretim (TIP) özelliğinde hello Test hakkında bilgi edinin."
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
ms.openlocfilehash: 2ddbd532ffe2a4f3e07fd386d9741a3fde3639ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a>Web Apps ile üretim testine başlayın
Üretimde test ya da canlı web uygulamanızı gerçek müşteri trafiğinden kullanarak sınama olan uygulama geliştiriciler giderek kolay bir şekilde entegre bir test stratejisi kendi [Çevik Geliştirme](https://en.wikipedia.org/wiki/Agile_software_development) Metodoloji. Tootest hello kalite uygulamalarınızın üretim ortamınızda dinamik kullanıcı trafiği ile bir sınama ortamında karşılıklı toosynthesized veri olarak sağlar. Yeni uygulama tooreal kullanıcılarınızın göstererek hello gerçek sorunlar Uygulamanız dağıtıldıktan sonra karşılaşabilecekleri üzerinde haberdar olmak. Merhaba işlevselliği, performans ve uygulama güncelleştirmelerinizi hello birim, hız ve hiçbir zaman bir sınama ortamında yaklaşık gerçek kullanıcı trafiği çeşitli karşı değerini doğrulayabilirsiniz.

## <a name="traffic-routing-in-app-service-web-apps"></a>App Service Web Apps yönlendirme trafiği
Hello ile trafik yönlendirme özelliğini [Azure uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714), dinamik kullanıcı trafiği tooone veya daha fazla bir bölümünü yönlendirebilirsiniz [dağıtım yuvası](web-sites-staged-publishing.md)ve ardından uygulamanızı analiz [Azure uygulama Öngörüler](/services/application-insights/) veya [Azure Hdınsight](/services/hdinsight/), veya bir üçüncü taraf aracı [New Relic](/marketplace/partners/newrelic/newrelic/) toovalidate değişikliğinizin. Örneğin, aşağıdaki senaryolarda uygulama hizmeti ile Merhaba uygulayabilirsiniz:

* İşlevsel hataları bulmaya veya performans sorunları güncelleştirmeleri önceki toosite genelinde dağıtımınızda sabitleme
* Değişikliklerinizi "denetimli test uçuşlar" Merhaba beta uygulama kullanılabilirlik ölçümleri ölçerek gerçekleştirin
* Aşamalı olarak yeni bir güncelleştirme tooa artırmalarını ve bir hata oluşursa toohello geçerli sürümü düzgün biçimde geri 
* Çalıştırarak, uygulamanızın iş sonuçları en iyi duruma getirme [A / B testler](https://en.wikipedia.org/wiki/A/B_testing) veya [multivariate testleri](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) içinde birden çok dağıtım yuvası

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a>Trafik yönlendirme Web uygulamalarında kullanma gereksinimleri
* Web uygulamanızı çalıştırmak gerekir **standart** veya **Premium** birden çok dağıtım yuvası için gerekli olduğundan, katmanı.
* Sipariş toowork düzgün bir şekilde, trafik yönlendirme hello kullanıcıların tarayıcıda etkin tanımlama bilgilerini toobe gerektirir. Trafik yönlendirme tanımlama bilgilerini toopin bir istemci tarayıcısı tooa dağıtım yuvası hello yaşam hello istemci oturumu için kullanır.
* Trafik yönlendirme Azure PowerShell cmdlet'leri aracılığıyla Gelişmiş ipucu senaryolarını destekler.

## <a name="route-traffic-segment-tooa-deployment-slot"></a>Rota trafiği segment tooa dağıtım yuvası
Merhaba temel düzeyde her ipucu senaryosunda, Canlı trafiği tooa üretim dışı dağıtım yuvası önceden tanımlanmış bir yüzdesini rota. toodo Bu, başlangıç adımları aşağıdaki:

> [!NOTE]
> Merhaba adımlar burada varsayar sahip olduğunuz bir [üretim dışı dağıtım yuvası](web-sites-staged-publishing.md) ve o hello istenen web uygulama içeriği, zaten [dağıtılan](web-sites-deploy.md) tooit.
> 
> 

1. Merhaba günlüğüne [Azure Portal](https://portal.azure.com/).
2. Web uygulamanızın dikey penceresinde tıklayın **ayarları** > **trafik yönlendirme**.
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. Tooroute trafiği tooand hello işlemleriniz, ardından tıklatın hello toplam trafik yüzdesi istediğiniz select hello yuvası **kaydetmek**.
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. Toohello dağıtım yuvanın dikey penceresine gidin. Yönlendirilmiş tooit olan dinamik trafik görmelisiniz.
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

Trafik yönlendirme yapılandırıldıktan sonra istemcilerin yüzdesi rastgele yönlendirilmiş tooyour üretim dışı yuvası olacaktır hello belirtildi. Ancak, istemci otomatik olarak yönlendirilmiş tooa belirli yuvası eklendiğinde, bu hello ömrünü bu istemci oturumu için "sabitlenmiş" toothat yuva olacaktır önemli toonote olur. Bu yapılan bir tanımlama bilgisi toopin hello kullanıcı oturumunu kullanarak. Merhaba HTTP isteklerini inceleyin, bulacaksınız bir `TipMix` sonraki her istekte tanımlama bilgisi.

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-tooa-specific-slot"></a>İstemci istekleri tooa belirli yuvası zorla
Toplama tooautomatic trafik yönlendirme, uygulama mümkün tooroute istekleri tooa belirli yuvası hizmetidir. Kullanıcıların toobe mümkün tooopt istediğinizde bu kullanışlıdır-içine veya geri çevirin, beta uygulamanızın. toodo bunu hello kullandığınız `x-ms-routing-name` sorgu parametresi.

tooreroute kullanıcılar tooa belirli yuvası kullanarak `x-ms-routing-name`, o hello yuva toohello trafik yönlendirme listesine zaten eklenmiş olduğundan emin olmalısınız. Tooroute tooa yuvası açıkça istediğinden hello gerçek yönlendirme yüzdesi belirlediğiniz önemli değildir. İsterseniz, "tıklatabileceği bir beta bağlantı" oluşturabileceği tooaccess hello beta uygulama.

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a>Kullanıcılar beta uygulama dışında iptal et
beta uygulamanızı dışında toolet kullanıcılar opt, örneğin, bu bağlantıyı web sayfanıza koyabilirsiniz:

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back tooproduction app</a>

Merhaba dize `x-ms-routing-name=self` hello üretim yuvasına belirtir. Merhaba istemci tarayıcı erişimi hello bağlantısı, yalnızca başladıktan sonra toohello üretim yuvasına yeniden yönlendirilen, ancak sonraki her istek hello içerecek `x-ms-routing-name=self` hello oturum toohello üretim yuvasına sabitler tanımlama bilgisi.

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-toobeta-app"></a>Kullanıcıların toobeta uygulamasında iptal et
toolet kullanıcıların kabul tooyour beta uygulamada, kümesi hello aynı sorgu parametresi toohello adı hello üretim dışı yuva, örneğin:

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a>Diğer kaynaklar
* [Hazırlık ortamları için Azure App Service'te web uygulamalarını ayarlama](web-sites-staged-publishing.md)
* [Azure'nın beklendiği karmaşık bir uygulama dağıtma](app-service-deploy-complex-application-predictably.md)
* [Azure App Service ile Çevik Yazılım Geliştirme](app-service-agile-software-development.md)
* [DevOps ortamları etkili bir şekilde web uygulamaları için kullanın](app-service-web-staged-publishing-realworld-scenarios.md)

