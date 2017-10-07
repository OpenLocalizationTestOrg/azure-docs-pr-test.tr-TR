---
title: "Azure web uygulaması performans aaaMonitor | Microsoft Docs"
description: "Azure web uygulamaları için uygulama performansını izleme. Yük, yanıt süresi ve bağımlılık bilgilerinin grafiğini çıkarın ve performansa bağlı uyarılar ayarlayın."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0b2deb30-6ea8-4bc4-8ed0-26765b85149f
ms.service: azure-portal
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: d1083254e5c504b18f2ac5ae2368610dc2790436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-web-app-performance"></a>Azure web uygulaması performansını izleme
Merhaba, [Azure Portal](https://portal.azure.com) için uygulama performansı izleme yukarı ayarlayabilir, [Azure web uygulamaları](../app-service-web/app-service-web-overview.md). [Azure Application Insights](app-insights-overview.md) hakkında kendi etkinlikleri toohello nerede depolandığı ve analiz Application Insights hizmeti, uygulama toosend telemetrinizi Instruments. Burada, ölçüm grafikler ve arama araçları kullanılabilir toohelp sorunlarını tanılamak, performansı ve kullanımı değerlendirin.

## <a name="run-time-or-build-time"></a>Çalışma zamanı veya derleme zamanı
İki yoldan biriyle hello uygulamada işaretlenerek izleme yapılandırabilirsiniz:

* **Çalışma zamanı**: Web uygulamanız zaten yayındayken bir performans izleme uzantısını seçebilirsiniz. Gerekli toorebuild değil veya uygulamanızı yeniden yükleyin. Yanıt süreleri, başarı oranları, özel durumlar ve bağımlılıklar gibi değişkenleri izleyen standart bir paket kümesine sahip olursunuz. 
* **Derleme zamanı**: Geliştirme sırasında uygulamanıza bir paket yükleyebilirsiniz. Bu seçenek daha kullanışlıdır. Toplama toohello içinde aynı standart paketleri yazabilirsiniz kod toocustomize hello telemetri veya toosend kendi telemetrinizi. Belirli etkinlikleri veya uygulama etki alanınızın toohello semantiği göre kayıt olayları oturum açabilir. 

## <a name="run-time-instrumentation-with-application-insights"></a>Application Insights ile çalışma zamanında izleme
Azure’da çalışmakta olan bir web uygulamanız varsa zaten bazı izleme verileri alırsınız: İstek ve hata oranları. Application Insights tooget daha fazla yanıt sürelerini ve izleme çağrıları toodependencies, akıllı algılama ve hello güçlü günlük analizi sorgu dili gibi ekleyin. 

1. **Application Insights seçin** web uygulamanız için hello Azure Denetim Masası'nda.
   
    ![İzleme bölümünden Application Insights’ı seçin](./media/app-insights-azure-web-apps/05-extend.png)
   
   * Zaten bu uygulama için Application Insights kaynağı başka bir yol ayarlamadıysanız toocreate yeni bir kaynak seçin.
2. Application Insights yüklendikten sonra **web uygulamanızı izleyin** . 
   
    ![Web uygulamanızı izleme](./media/app-insights-azure-web-apps/restart-web-app-for-insights.png)

   Sayfa görüntülemesi ve kullanıcı telemetrisi için **istemci tarafı izlemeyi etkinleştirin**.

   * Ayarlar > Uygulama Ayarları'nı seçin.
   * Uygulama Ayarları'nın altında yeni bir anahtar değer çifti ekleyin: 
   
    Anahtar: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Değer:`true`
   * **Kaydet** hello ayarları ve **yeniden** uygulamanızı.
3. **Uygulamanızı izleyin**.  [Expore hello veri](#explore-the-data).

Daha sonra isterseniz hello uygulama Application Insights ile oluşturabilirsiniz.

*Nasıl kaldırabilirim Application Insights, veya toosending tooanother kaynak geçiş?*

* Azure, açık hello web uygulaması denetim dikey ve geliştirme araçları altında açmak **uzantıları**. Merhaba Application Insights uzantısını silin. Ardından altında izleme, Application Insights'ı seçin ve oluşturmak veya istediğiniz hello kaynağı seçin.

## <a name="build-hello-app-with-application-insights"></a>Application Insights ile Merhaba uygulaması oluşturma
Application Insights, uygulamanıza bir SDK yükleyerek daha ayrıntılı telemetri sağlayabilir. Bunların başında izleme günlüklerini toplama, [özel telemetri yazma](app-insights-api-custom-events-metrics.md) ve daha ayrıntılı özel durum raporları alma gelir.

1. **Visual Studio**’da (2013 güncelleştirme 2 veya sonraki sürümler), projeniz için Application Insights’ı yapılandırın.

    Merhaba web projesine sağ tıklayın ve seçin **Ekle > Application Insights** veya **yapılandırma Application Insights**.
   
    ![Merhaba web projesine sağ tıklayın ve Ekle veya yapılandırma Application Insights'ı seçin](./media/app-insights-azure-web-apps/03-add.png)
   
    İçinde toosign sorulursa hello kimlik Azure hesabınız için kullanın.
   
    Merhaba işlemi iki etkilere sahiptir:
   
   1. Azure’da telemetrinin depolanacağı, analiz edileceği ve görüntüleneceği bir Application Insights kaynağı oluşturulur.
   2. Merhaba (Bu zaten yoksa) uygulama Öngörüler NuGet paket tooyour kodu ekler ve toosend telemetri toohello Azure kaynak yapılandırır.
2. **Test hello telemetri** çalışan hello uygulama geliştirme makinenizdeki (F5) tarafından.
3. **Merhaba uygulama yayımlama** hello tooAzure her zamanki gibi. 

*Toosending tooa farklı Application Insights kaynağı nasıl geçiş yapabilirim?*

* Visual Studio'da, sağ hello proje **yapılandırma Application Insights** ve istediğiniz hello kaynağı seçin. Yeni bir kaynak hello seçeneği toocreate alın. Yeniden derleyin ve dağıtın.

## <a name="explore-hello-data"></a>Merhaba veri keşfedin
1. Merhaba Application Insights dikey penceresinde, web uygulama Denetim Masası'nın ikinci bir veya iki bunların içinde istekleri ve hataları gösterir Canlı ölçümlerini görmek gerçekleşen. Uygulamanızı yeniden yayımlıyorsanız herhangi bir sorunu anında görmenizi sağlayan bu ekran çok kullanışlıdır.
2. Toohello tam Application Insights kaynağı ' ı tıklatın.

    ![Tıklayarak gitme](./media/app-insights-azure-web-apps/view-in-application-insights.png)

    Kaynağa doğrudan Azure kaynak gezintisinden de gidebilirsiniz.

1. Tüm grafik tooget daha fazla ayrıntı tıklatın:
   
    ![Bir grafik Hello Application Insights genel bakış dikey penceresinde](./media/app-insights-azure-web-apps/07-dependency.png)
   
    [Ölçüm dikey pencerelerini özelleştirme](app-insights-metrics-explorer.md) olanağınız vardır.
2. Daha fazla toosee olayları tek tek ve bunların özelliklerini tıklatın:
   
    ![Bir arama, o türde filtre uygulanmış bir olay türü tooopen tıklatın](./media/app-insights-azure-web-apps/08-requests.png)
   
    Bağlantı tooopen tüm özellikleri "..." Merhaba dikkat edin.
   
    [Aramaları özelleştirme](app-insights-diagnostic-search.md) olanağınız vardır.

Merhaba telemetrinizi üzerinden daha güçlü arar kullanmak [günlük analizi sorgu dili](app-insights-analytics-tour.md).

## <a name="more-telemetry"></a>Daha fazla telemetri

* [Web sayfası yükleme verileri](app-insights-javascript.md)
* [Özel telemetri](app-insights-api-custom-events-metrics.md)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Sonraki adımlar
* [Canlı uygulamanızı üzerinde Hello profil oluşturucu çalıştırma](app-insights-profiler.md).
* [Azure İşlevleri](https://github.com/christopheranderson/azure-functions-app-insights-sample) - Application Insights ile Azure İşlevlerini izleyin
* [Azure Tanılama'yı etkinleştirmek](app-insights-azure-diagnostics.md) gönderilen toobe tooApplication Insights.
* [İzleme hizmeti sistem durumu ölçümleri](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) toomake hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin.
* İşletimsel olaylar gerçekleştiğinde ya da ölçümler bir eşiği aştığında [uyarı bildirimleri alın](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).
* Kullanım [JavaScript uygulamaları ve web sayfaları için Application Insights](app-insights-javascript.md) tooget istemci telemetri hello tarayıcılardan bir web sayfasını ziyaret edin.
* [Kullanılabilirlik web testleri oluşturma](app-insights-monitor-web-app-availability.md) sitenizi kapalı olduğunda uyarı toobe.

