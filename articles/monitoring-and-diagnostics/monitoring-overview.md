---
title: Microsoft azure'da aaaMonitoring | Microsoft Docs
description: "Microsoft Azure'da toomonitor herhangi bir şey istediğiniz zaman Seçenekler. Azure İzleyici, uygulama Öngörüler günlük analizi"
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1b962c74-8d36-4778-b816-a893f738f92d
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: f5a4f32525c52613f01a913e09a9fe3fbcbaeb21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-monitoring-in-microsoft-azure"></a>Microsoft Azure'da izleme genel bakış
Bu makalede, Microsoft Azure izlemesi için kullanılabilen araçlar genel bir bakış sağlar. Çok uygular
- Microsoft Azure'da çalışan uygulamaları izleme 
- azure'da nesneleri izleyebilir Azure dışında çalışan araçlar/hizmetler. 

Bunu anlatılmaktadır çeşitli ürün ve hizmetlerini kullanılabilir hello ve nasıl çalıştığını birlikte. Bu, hangi araçların hangi durumlarda sizin için en uygun toodetermine yardımcı olabilir.  

## <a name="why-use-monitoring-and-diagnostics"></a>İzleme ve tanılama neden kullanılır?

Performans sorunlarını bulut uygulamanızda iş etkileyebilir. Birden çok birbirine bağlı bileşenleri ve sık sürümleri ile degradations herhangi bir zamanda oluşabilir. Ve kullanıcılarınızın bir uygulama geliştiriyorsanız, genellikle testinde bulamadı sorunları keşfedin. Bu hemen bilmeniz ve hello sorunlarını tanılamak ve araçları olması gerekir. Microsoft Azure Araçları bu sorunları tanımlamak için bir aralığı yok.

## <a name="how-do-i-monitor-my-azure-cloud-apps"></a>Azure bulut uygulamalarım nasıl izlerim?

Çeşitli araçlar Azure uygulamaları ve Hizmetleri izleme yoktur. Bazı özelliklerine çakışıyor. Geliştirme ve bir uygulamanın işlemi toohello Bulanıklaştırma son kısmen ve kısmen geçmiş nedenlerle budur. 

Merhaba asıl araçlar şunlardır:

-   **Azure İzleyici** Azure üzerinde çalışan hizmetleri izlemek için temel araçtır. Altyapı düzeyinde veri hizmeti ve ortam çevreleyen hello hello işleme hakkında sağlar. Uygulamalarınızda tüm Azure yönetiyorsanız, yukarı veya aşağı kaynakları tooscale, ardından Azure İzleyicisi, ne kullandığınız sunar olup olmadığını karar toostart.

-   **Application Insights** geliştirme için ve bir üretim izleme çözümü olarak kullanılabilir. Uygulamanıza bir paketi yükleyerek çalışır ve bu nedenle neler olup bittiğini daha iç bir görünümünü sağlar. Verileri bağımlılıkları, özel durum izleme, anlık görüntüler, yürütme profilleri hata ayıklama yanıt sürelerini içerir. Güçlü akıllı araçlar bu telemetri çözümlemek için bir uygulama ve hangi kullanıcıların ile yaptıklarını anlamak toohelp hata ayıklama hem toohelp sağlar. Bir ani artış yanıt süreleri nedeniyle mi olduğunu anlayabilirsiniz toosomething bir uygulama ya da dış bazı resourcing sorun. Bunu düzeltmek için Visual Studio kullanıyorsanız ve hello uygulama hataya neden olduğunu, doğru toohello sorun satır kod alınabilir.  

-   **Günlük analizi** tootune performans ve planı bakım üretimde çalışan uygulamalara gereksinim duyan olanlar içindir. Azure'da temel alır. Toplar ve 10 too15 dakikalık bir gecikme olsa birçok kaynaktan verileri toplar. Azure için bir bütünsel BT yönetim çözümü sunar şirket içi ve üçüncü taraf bulut tabanlı altyapı (örneğin, Amazon Web Hizmetleri). Daha zengin araçları tooanalyze veri arasında daha fazla kaynaklarına sağlar, karmaşık sorgular tüm günlükleri sağlar ve belirtilen koşullara proaktif olarak uyarabilir.  Özel verileri sorgulamak ve onu görselleştirmek için kendi merkezi depoya bile toplayabilirsiniz. 

-   **System Center Operations Manager (SCOM)** yönetme ve büyük bulut yüklemeleri izleme içindir. Zaten bir yönetim aracı için Windows Server ve Hyper-V tabanlı Bulutlar şirket içi ancak aynı zamanda tümleştirileceğini ve Azure uygulamalarını yönetme gibi ile bilgi sahibi olmanız. Bunun yanı sıra, Application Insights mevcut Canlı uygulamaları yükleyebilirsiniz.  Bir uygulama kullanılamaz hale gelirse, saniye cinsinden belirtir. Günlük analizi SCOM değiştirmez unutmayın. De onunla birlikte çalışır.  


## <a name="accessing-monitoring-in-hello-azure-portal"></a>İzleme Hello Azure portalına erişme
Tüm Azure izleme hizmetleri tek bir UI bölmesinde kullanıma sunulmuştur. Hakkında daha fazla bilgi için tooaccess bu alanı bkz [Azure İzleyicisi ile çalışmaya başlama](monitoring-get-started.md). 

İzleme işlevleri belirli kaynaklar için bu kaynakları vurgulama ve bunların izleme seçenekleri araştırıp de erişebilir. 

## <a name="examples-of-when-toouse-which-tool"></a>Ne zaman örnekler aracı toouse 

Aşağıdaki bölümlerde hello bazı temel senaryolar ve hangi araçların birlikte kullanılması gerektiğini gösterir. 

### <a name="scenario-1--fix-errors-in-an-azure-application-under-development"></a>Senaryo 1 – Azure uygulaması geliştirme altında düzeltme hataları   

**Merhaba iyi toouse Application Insights, Azure İzleyici ve Visual Studio birlikte seçenektir**

Azure şimdi hello Visual Studio hata ayıklayıcısı hello bulutta hello gücünü sağlar. Azure İzleyici toosend telemetri tooApplication Öngörüler yapılandırın. Visual Studio tooinclude hello Application Insights SDK'sı, uygulamanızın etkinleştirin. Application Insights'ta hello uygulama eşlemesi toodiscover görsel olarak kullanabileceğiniz bir kez çalışan uygulamanızın hangi parçalarını veya kötü durumda. Bölümlerinde her zaman iyi durumda olmayan hataları ve özel durumları zaten araştırması için kullanılabilir. Kullanabileceğiniz çeşitli analizleri Application Insights toogo daha derin hello. Merhaba hatasıyla ilgili emin değilseniz, kodu ve PIN noktasına başka bir sorun hello Visual Studio hata ayıklayıcısı tootrace kullanabilirsiniz. 

Daha fazla bilgi için bkz: [Web uygulamaları izleme](../application-insights/app-insights-azure-web-apps.md) ve çeşitli uygulamaları ve diller hakkında yönergeler için toohello İçindekiler hello soldaki bakın.  

### <a name="scenario-2--debug-an-azure-net-web-application-for-errors-that-only-show-in-production"></a>Senaryo 2 – bir Azure .NET web uygulaması yalnızca üretimde Göster hataları için hata ayıklama 

> [!NOTE]
> Bu özellikler önizlemede. 

**Merhaba toouse Application Insights seçenektir ve mümkünse hello için Visual Studio tam hata ayıklama deneyimini en iyi.**

Merhaba uygulama Öngörüler anlık görüntü hata ayıklayıcı toodebug uygulamanızı kullanın. Belirli bir hata eşiği üretim bileşenleriyle oluştuğunda telemetri "anlık görüntüler." olarak adlandırılan zaman Windows hello sistem otomatik olarak yakalar. küçük olduğundan hello Yakalanan tutarı için bir üretim bulut güvenlidir yeterli değil tooaffect performans ancak yeterince önemli tooallow izleme.  Merhaba sistem birden çok anlık görüntü yakalayabilirsiniz. Bir noktada hello Azure portal zamanında bakın veya hello tam deneyimi için Visual Studio'yu kullanın. Gerçek zamanlı olarak debugging gibi Visual Studio ile geliştiriciler bu anlık görüntü yol. Yerel değişkenler, parametreleri, bellek ve çerçeveleri tüm kullanılabilir. Geliştiriciler bir RBAC rolü aracılığıyla erişim toothis üretim verileri verilmiş olması gerekir.  

Daha fazla bilgi için bkz: [anlık görüntü hata ayıklama](../application-insights/app-insights-snapshot-debugger.md). 

### <a name="scenario-3--debug-an-azure-application-that-uses-containers-or-microservices"></a>Senaryo 3 – kapsayıcıları veya mikro kullanan bir Azure uygulama hata ayıklama 

**Senaryo 1 ile aynıdır. Application Insights, Azure İzleyici ve Visual Studio birlikte kullanmak** Application Insights toplama telemetri kapsayıcılarda çalışan işlemleri ve mikro (Kubernetes, Docker, Azure Service Fabric) da destekler. Daha fazla bilgi için [kapsayıcıları ve mikro hata ayıklamayı bu video bkz](https://go.microsoft.com/fwlink/?linkid=848184). 


### <a name="scenario-4--fix-performance-issues-in-your-azure-application"></a>Senaryo 4 – Azure uygulamanızda düzeltme performans sorunları

Merhaba [Application Insights profil oluşturucu](../application-insights/app-insights-profiler.md) tasarlanmış toohelp sorun giderme bu tür sorunları. Belirleyin ve uygulama Hizmetleri (Web uygulamaları, Logic Apps, Mobile Apps, API uygulamaları) ve diğer işlem kaynakları gibi sanal makineler, sanal makine ölçek kümeleri (VMSS), Cloud Services ve Service Fabric çalışan uygulamalar için performans sorunlarını giderme. 

> [!NOTE]
> Sanal makineler, sanal makine ölçek kümeleri (VMSS) bulut Hizmetleri ve Hizmetleri doku yeteneği tooprofile önizlemede değil.   

Ayrıca, önceden belirli türde bir yavaş sayfa yükleme süreleri gibi hatalar hakkında e-postayla hello akıllı algılama aracı tarafından bildirilir.  Toodo bu araç hakkında herhangi bir yapılandırma gerekmez. Daha fazla bilgi için bkz: [akıllı algılama - performans Anormalliklerini](../application-insights/app-insights-proactive-performance-diagnostics.md) ve [akıllı algılama - performans Anormalliklerini](https://azure.microsoft.com/blog/Enhancments-ApplicationInsights-SmartDetection/preview).



## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinin

* [Azure İzleyicisi'nde Ignite 2016'den video](https://myignite.microsoft.com/videos/4977)
* [Azure İzleyicisi ile çalışmaya başlama](monitoring-get-started.md)
* [Azure tanılama](../azure-diagnostics.md) sanal makine, bulut hizmetinde toodiagnose sorunları çalışıyorsanız sanal makine ölçeklendirme ayarlayın veya Service Fabric uygulaması.
* [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) App Service Web uygulamanızda toodiagnostic sorunları çalışıyorsanız.
* [Günlük analizi](https://azure.microsoft.com/documentation/services/log-analytics/) ve hello [Operations Management Suite](https://www.microsoft.com/oms/) üretim izleme çözümü