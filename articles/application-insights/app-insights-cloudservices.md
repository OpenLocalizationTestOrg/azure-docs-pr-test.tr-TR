---
title: "aaaApplication Azure bulut Hizmetleri için Insights | Microsoft Docs"
description: "Application Insights ile web ve çalışan rollerinizi etkili bir şekilde izleyin"
services: application-insights
documentationcenter: 
keywords: "WAD2AI, Azure Tanılama"
author: CFreemanwa
manager: carmonm
editor: alancameronwills
ms.assetid: 5c7a5b34-329e-42b7-9330-9dcbb9ff1f88
ms.service: application-insights
ms.devlang: na
ms.tgt_pltfrm: ibiza
ms.topic: get-started-article
ms.workload: tbd
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 6956ce423eea1e2cf387bd98250bae32d9501ed0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-azure-cloud-services"></a>Azure Cloud Services için Application Insights
[Microsoft Azure Cloud hizmeti uygulamaları](https://azure.microsoft.com/services/cloud-services/), Application Insights SDK'larındaki verilerle Bulut Hizmetlerinizdeki [Azure Tanılama](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) verileri birleştirilerek kullanılabilirlik, performans, hata ve kullanım açısından [Application Insights][start] tarafından izlenebilir. Merhaba performans ve hello uygulamanızda verimliliğini hakkında joker elde hello geri bildirim ile her geliştirme yaşam döngüsündeki hello tasarım hello yönünü hakkında bilinçli seçimler yapabilirsiniz.

![Örnek](./media/app-insights-cloudservices/sample.png)

## <a name="before-you-start"></a>Başlamadan önce
Gerekenler:

* [Microsoft Azure](http://azure.com) içeren bir abonelik. Windows, XBox Live veya diğer Microsoft bulut hizmetlerinde kullanıyor olabileceğiniz bir Microsoft hesabıyla oturum açın. 
* Microsoft Azure araçları 2.9 veya üzeri
* Developer Analytics Tools 7.10 veya üzeri

## <a name="quick-start"></a>Hızlı başlangıç
Bulut hizmetinizi Application Insights ile hizmet tooAzure yayımladığınızda, seçenek toochoose olan hızlı ve kolay bir yol toomonitor hello.

![Örnek](./media/app-insights-cloudservices/azure-cloud-application-insights.png)

Bu seçenek Instruments toomonitor istekleri, özel durumlar ve bağımlılıkları, web rolü yanı sıra performans gereksinim duyduğunuz tüm hello telemetri vermiş, uygulamanızın çalışma zamanında çalışan rollerden sayaçları. Uygulamanız tarafından oluşturulan tüm tanılama izlemeleri de tooApplication Öngörüler gönderilir.

Tek ihtiyacınız olan buysa başka bir şey yapmanız gerekmez! Sonraki adımlar [uygulamanızdan alınan ölçümleri görüntüleme](app-insights-metrics-explorer.md), [Analytics ile verilerinizi sorgulama](app-insights-analytics.md) ve isteğe bağlı olarak bir [pano](app-insights-dashboards.md) ayarlama üzerinedir. Yukarı tooset isteyebilirsiniz [kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md) ve [kod tooyour web sayfaları ekleme](app-insights-javascript.md) hello tarayıcıda toomonitor performans.

Bununla birlikte, daha fazla seçeneğe de sahip olabilirsiniz:

* Farklı bileşenlerini veri göndermek ve yapılandırmaları tooseparate kaynakları oluşturun.
* Uygulamanızdan özel telemetri ekleyin.

Bu seçenekler ilgi tooyou varsa, okumaya devam edin.

## <a name="sample-application-instrumented-with-application-insights"></a>Application Insights ile izlenen Örnek Uygulama
Bu bir göz atalım [örnek uygulama](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) içinde Application Insights eklendiği tooa bulut hizmeti Azure üzerinde barındırılan iki çalışan rolleri ile. 

Aşağıda, nasıl tooadapt kendi bulut hizmeti projesi hello bildirir aynı şekilde.

## <a name="plan-resources-and-resource-groups"></a>Kaynakları ve kaynak gruplarını planlama
Merhaba telemetriyi uygulamanızdan depolanır, analiz ve Application Insights türünde bir Azure kaynak görüntülenir. 

Her bir kaynağın tooa kaynak grubuna ait. Kaynak grupları tooteam üyeleri, erişim izni verme için maliyetleri yönetmek için kullanılır ve tek bir Eşgüdümlü işlemde toodeploy güncelleştirir. Örneğin, verebilir [bir komut dosyası toodeploy yazma](../azure-resource-manager/resource-group-template-deploy.md) Azure bulut hizmeti ve bir işlemde tüm kaynakları izleyerek, Application Insights.

### <a name="resources-for-components"></a>Bileşenler için kaynaklar
Merhaba düzeni toocreate uygulamanızın - diğer bir deyişle, her web rolü ve çalışan rolü her bileşen için ayrı bir kaynak önerilir. Her bileşen ayrı olarak analiz edebilirsiniz, ancak oluşturabilirsiniz bir [Pano](app-insights-dashboards.md) , getirir birlikte hello anahtar grafikleri tüm hello bileşenlerini karşılaştırın ve bunları birlikte izleyebilirsiniz. 

Birden fazla rol toohello toosend hello telemetrisinden bir alternatif düzenidir aynı kaynak ancak [bir boyut özelliği tooeach telemetri öğesi ekleme](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer) kaynak rolünü tanımlar. Bu düzen ölçüm grafikleri özel durumlar gibi hello sayıları hello gelen toplamı farklı roller normal olarak göster. ancak hello grafik gerektiğinde Merhaba rol tanımlayıcısına göre kesimleyebilirsiniz. Aramaları ayrıca filtre hello tarafından aynı boyut. Bu alternatif kolaylaştırır biraz daha kolay tooview her şeye hello aynı zaman ancak toosome karışıklığı hello rolleri arasında da neden olabilir.

Tarayıcı telemetri hello genellikle dahil aynı kaynak sunucu tarafı web rolü olarak.

Merhaba farklı bileşenleri için Hello Application Insights kaynaklar bir kaynak grubuna yerleştirin. Bu, kolay toomanage kolaylaştırır birlikte bunları. 

### <a name="separating-development-test-and-production"></a>Ayırma, geliştirme, test ve üretim
Sonraki özellik için özel olaylar geliştiriyorsanız Hello önceki sürüm Canlı olsa toosend hello geliştirme telemetri tooa ayrı Application Insights kaynağı istiyor. Aksi takdirde, test telemetri arasında sabit toofind olacak tüm trafiği hello Canlı siteden hello.

tooavoid bu durumda, ayrı kaynakları için her bir yapı yapılandırması veya 'damgası' (geliştirme, test, üretim,...) sisteminizin oluşturun. Merhaba kaynakları her yapı yapılandırması için farklı bir kaynak grubunda yerleştirin. 

toosend hello telemetri toohello uygun kaynaklar, Application Insights SDK'sı hello hello yapı yapılandırmasına bağlı olarak farklı izleme anahtarı seçer şekilde ayarlayabilirsiniz. 

## <a name="create-an-application-insights-resource-for-each-role"></a>Her rol için bir Application Insights kaynağı oluşturma
Toocreate - her rol için ayrı bir kaynak karar verdiniz ve belki de ayrı bir ayarlamak için her yapı yapılandırması - sonra kolay toocreate olan hello Application Insights portalında tüm bunları. (Kaynakları çok oluşturursanız, yapabilecekleriniz [hello işlemini otomatikleştirmek](app-insights-powershell.md).

1. Merhaba, [Azure portal][portal], yeni bir Application Insights kaynağı oluşturun. Uygulama türü olarak ASP.NET uygulamasını seçin. 

    ![Yeni, Application Insights öğesine tıklayın](./media/app-insights-cloudservices/01-new.png)
2. Her kaynağın bir İzleme Anahtarı ile tanımlandığını unutmayın. Toomanually istiyorsanız, bunu daha sonra gerekebilecek yapılandırmak veya hello SDK hello yapılandırmasını doğrulayın.

    ![Özellikler'i tıklatın, başlangıç anahtarı seçin ve ctrl + C tuşlarına basın](./media/app-insights-cloudservices/02-props.png) 

## <a name="set-up-azure-diagnostics-for-each-role"></a>Her rol için Azure Tanılama ayarlama
Bu seçenek toomonitor Application Insights ile uygulamanızı ayarlayın. Bu seçenek, web rolleri için performans izleme, uyarılar ve tanılamanın yanı sıra kullanım analizi sağlar. Diğer roller için arama yapın ve yeniden başlatma, performans sayaçları ve çağrıları tooSystem.Diagnostics.Trace gibi Azure tanılama izleyin. 

1. Visual Studio Çözüm Gezgini'nde, altında &lt;YourCloudService&gt;, rolleri, her rol hello özelliklerini açın.
2. İçinde **yapılandırma**ayarlayın **tanılama veri tooApplication Öngörüler Gönder** ve hello daha önce oluşturduğunuz uygun Application Insights kaynağı seçin.

Toouse her yapı yapılandırması için ayrı bir Application Insights kaynağı karar verdiyseniz, ilk hello yapılandırmasını seçin.

![Her Azure rol Hello özelliklerinde Application Insights yapılandırın](./media/app-insights-cloudservices/configure-azure-diagnostics.png)

Bu, Application Insights izleme anahtarı adlı hello dosyalarıyla ekleme hello etkisi `ServiceConfiguration.*.cscfg`. ([Örnek kod](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/AzureEmailService/ServiceConfiguration.Cloud.cscfg)).

Gönderilen tanılama bilgileri tooApplication Öngörüler toovary hello düzeyi istiyorsanız, bunu yapabilirsiniz [hello düzenleyerek `.cscfg` doğrudan dosyaları](app-insights-azure-diagnostics.md).

## <a name="sdk"></a>Her projede Hello SDK yükleme
Bu seçenek hello özelliği tooadd özel iş telemetri tooany rol, uygulamanızın nasıl kullanılır ve gerçekleştirir daha yakın bir çözümleme için ekler.

Visual Studio'da Application Insights SDK'sı hello her bulut uygulaması projesi için yapılandırın.

1. **Web rolleri**: Merhaba projeyi sağ tıklatın ve seçin **yapılandırma Application Insights** veya **Ekle > Application Insights telemetri**.

2. **Çalışan rolleri**: 
 * Merhaba projesine sağ tıklatın ve **Nuget paketlerini Yönet**.
 * [Windows Sunucuları için Application Insights](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/)’ı ekleyin.

    !["Application Insights" araması yapın](./media/app-insights-cloudservices/04-ai-nuget.png)

3. Merhaba SDK toosend veri toohello Application Insights kaynağı yapılandırın.

    Uygun başlangıç işlevinde hello izleme anahtarını hello yapılandırma ayarından hello .cscfg dosyasında ayarlayın:
 
    ```C#
   
     TelemetryConfiguration.Active.InstrumentationKey = RoleEnvironment.GetConfigurationSettingValue("APPINSIGHTS_INSTRUMENTATIONKEY");
    ```
   
    Bunu uygulamanızdaki her rol için gerçekleştirin. Merhaba örneklere bakın:
   
   * [Web rolü](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Global.asax.cs#L27)
   * [Çalışan rolü](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L232)
   * [Web sayfaları için](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Views/Shared/_Layout.cshtml#L13) 
4. Kümesi hello Applicationınsights.config dosyası toobe her zaman toohello çıktı dizinine kopyalanır. 
   
    (Merhaba .config dosyasına, tooplace hello izleme anahtarını olmadığını soran iletiler görürsünüz. Ancak, daha iyi tooset olduğu bulut uygulamaları için bunu hello .cscfg dosyasından. Bu, hello rol doğru hello Portalı'nda tanımlanan sağlar.)

#### <a name="run-and-publish-hello-app"></a>Çalıştırın ve hello uygulama yayımlama
Uygulamanızı çalıştırın ve Azure'da oturum açın. Açık hello Application Insights kaynakları oluşturduğunuz ve tek tek veri noktalarını görüntülenmesini görürsünüz [arama](app-insights-diagnostic-search.md), ve verileri bir araya getirilir [ölçüm Gezgini](app-insights-metrics-explorer.md). 

Daha fazla telemetri ekleyin - aşağıdaki - hello bölümlere bakın ve ardından uygulama tooget Canlı tanılama ve kullanım görüşlerinizi yayımlayın. 

#### <a name="no-data"></a>Veri yok mu?
* Açık hello [arama] [ diagnostic] döşeme, olayları tek tek toosee.
* Birkaç telemetri oluşturması için farklı sayfaları açarak hello uygulamasını kullanın.
* Birkaç saniye bekleyin ve Yenile’ye tıklayın.
* Bkz. [Sorun giderme][qna].

## <a name="view-azure-diagnostic-events"></a>Azure Tanılama olaylarını görüntüleme
Burada toofind hello [Azure tanılama](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/azure-diagnostics) Application Insights bilgileri:

* Performans sayaçları özel ölçümler olarak görüntülenir. 
* Windows olay günlükleri izlemeler ve özel olaylar olarak gösterilir.
* Uygulama günlükleri, ETW günlükleri ve varsa tanılama altyapısı günlükleri izlemeler olarak görünür.

toosee performans sayaçları ve olay sayısı açmak [ölçüm Gezgini](app-insights-metrics-explorer.md) ve yeni bir grafik ekleyin:

![Azure tanılama verileri](./media/app-insights-cloudservices/23-wad.png)

Kullanım [arama](app-insights-diagnostic-search.md) veya bir [Analytics sorgu](app-insights-analytics-tour.md) toosearch çeşitli izleme günlüklerine Azure tanılama tarafından gönderilen hello arasında. Örneğin, bir rol toocrash ve Geri Dönüşüm neden işlenmeyen bir özel durum olduğunu varsayalım. Bu bilgileri hello uygulama kanal, Windows olay günlüğüne göstermeniz. Merhaba özel durum için hello tam yığın izlemesi almak ve Windows olay günlüğü hatası hello arama toolook kullanın. Hello kök hello sorunun nedenini bulmanıza yardımcı olur.

![Azure tanılama araması](./media/app-insights-cloudservices/25-wad.png)

## <a name="more-telemetry"></a>Daha fazla telemetri
Merhaba Göster aşağıdaki bölümlerde nasıl tooget ek farklı yönleri, uygulamanızın telemetrisinden.

## <a name="track-requests-from-worker-roles"></a>Çalışan rollerinden gelen İstekleri izleme
Web rollerinde hello istekleri modülü otomatik olarak HTTP istekleriyle ilgili verileri toplar. Merhaba bkz [MVCWebRole örnek](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole) örnekler nasıl hello varsayılan koleksiyon davranışı geçersiz kılabilirsiniz. 

Hello izleyerek hello performansı çağrıları tooworker rollerin yakalamak için HTTP isteklerini aynı şekilde. Application Insights'ta bir zaman aşımına ve bağımsız olarak başarılı veya başarısız adlandırılmış sunucu tarafı iş birimine hello istek telemetri türü ölçer. HTTP istekleri hello SDK'sı tarafından otomatik olarak yakalanır olsa da, kendi kod tootrack istekleri tooworker rolleri ekleyebilirsiniz.

Merhaba iki örnek çalışan rolleri Araçlı tooreport istekleri Bkz: [WorkerRoleA](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleA) ve [WorkerRoleB](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/WorkerRoleB)

## <a name="exceptions"></a>Özel durumlar
Farklı web uygulaması türlerinden işlenmeyen özel durumları nasıl toplayabileceğiniz konusunda bilgi edinmek için bkz. [Application Insights’ta Özel Durumları İzleme](app-insights-asp-net-exceptions.md).

Merhaba örnek web rolü MVC5 ve Web API 2 denetleyicisi vardır. Merhaba hello iki işlenmeyen özel durumlar işleyicileri aşağıdaki hello ile yakalanır.

* MVC5 denetleyicileri için [burada](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/FilterConfig.cs#L12) ayarlanmış [AiHandleErrorAttribute](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiHandleErrorAttribute.cs)
* Web API 2 denetleyicileri için [burada](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/App_Start/WebApiConfig.cs#L25) ayarlanmış [AiWebApiExceptionLogger](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/MvcWebRole/Telemetry/AiWebApiExceptionLogger.cs)

Çalışan rolleri için tootrack özel durumlar iki yolu vardır:

* TrackException(ex)
* Merhaba Application Insights İzleme dinleyicisi NuGet paketi eklediyseniz, kullanabileceğiniz **System.Diagnostics.Trace** toolog özel durumları. [Kod örneği.](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L107)

## <a name="performance-counters"></a>Performans Sayaçları
sayaçları aşağıdaki hello varsayılan olarak toplanır:

    * \Process(??APP_WIN32_PROC??)\% İşlemci Süresi
    * \Memory\Available Bytes
    * \.NET CLR Exceptions(??APP_CLR_PROC??)\# of Exceps Thrown / sec
    * \Process(??APP_WIN32_PROC??)\Private Bytes
    * \Process(??APP_WIN32_PROC??)\IO Data Bytes/sec
    * \Processor(_Total)\% Processor Time

Web rolleri için aşağıdaki sayaçlar da toplanır:

    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Requests/Sec
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Request Execution Time
    * \ASP.NET Applications(??APP_W3SVC_PROC??)\Requests In Application Queue

ApplicationInsights.config dosyasını [bu örnekte gösterildiği gibi](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/ApplicationInsights.config#L14) düzenleyerek ek özel sayaçlar veya başka Windows performans sayaçları belirtebilirsiniz.

  ![Performans sayaçları](./media/app-insights-cloudservices/OLfMo2f.png)

## <a name="correlated-telemetry-for-worker-roles"></a>Çalışan Rolleri için Bağıntılı Telemetri
Hangi neden tooa başarısız oldu veya yüksek gecikme isteği görebilirsiniz durumunda zengin bir tanılama deneyimi olur. Web rolleri ile ilgili telemetri hello SDK geçişi arasındaki bağıntı otomatik olarak ayarlar. Çalışan rolleri için özel telemetri Başlatıcı tooset ortak bir Operation.ID bağlamı özniteliği tüm hello telemetri tooachieve için bunu kullanabilirsiniz. Son tooa bağımlılık veya bir bakışta kodunuzu Hello gecikme/hata sorunu neden oldu olup olmadığını toosee böylece! 

Bunu yapmak için:

* Bir CallContext içine Hello bağıntı kimliği gösterilen şekilde ayarlayın [burada](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L36). Bu durumda, biz hello bağıntı kimliği hello istek kimliği kullanıyorsanız
* Özel bir TelemetryInitializer uygulaması, yukarıda belirlenen tooset hello Operation.ID toohello correlationıd değeri ekleyin. Örnek: [ItemCorrelationTelemetryInitializer](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/Telemetry/ItemCorrelationTelemetryInitializer.cs#L13)
* Merhaba özel telemetri başlatıcı ekleyin. Merhaba Applicationınsights.config dosyasında veya kodda gösterildiği gibi bunu [burada](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/Samples/AzureEmailService/WorkerRoleA/WorkerRoleA.cs#L233)

İşte bu kadar! toohelp bir bakışta tüm ilişkili telemetri gördüğünüz Hello portal deneyimi zaten Kablolu:

![Bağıntılı telemetri](./media/app-insights-cloudservices/bHxuUhd.png)

## <a name="client-telemetry"></a>İstemci telemetrisi
[Ekleme JavaScript SDK'sı tooyour web sayfalarını hello] [ client] tooget tarayıcı tabanlı telemetri sayfa görünümü sayısına, sayfa yükleme sürelerinin, komut dosyası özel durumlar ve sayfa komut dosyalarınızda özel telemetri yazma toolet gibi.

## <a name="availability-tests"></a>Kullanılabilirlik testleri
[Web testleri oluşturma] [ availability] toomake uygulamanızın canlı ve duyarlı kaldığından emin.

## <a name="display-everything-together"></a>Her şeyi birlikte görüntüleme
tooget sisteminizin genel bir resim, birlikte birinde izleme grafikleri hello anahtarını Getir [Pano](app-insights-dashboards.md). Örneğin, hello isteği sabitleme ve her rolü hatası sayar. 

Sisteminiz tarafından Stream Analytics gibi diğer Azure hizmetleri kullanılıyorsa bunların izleme grafiklerini de dahil edin. 

İstemci mobil uygulama varsa, kodu bazı toosend özel olaylar anahtar kullanıcı işlemlerini ekleme ve oluşturma bir [HockeyApp köprüsü](app-insights-hockeyapp-bridge-app.md). İçinde sorgu oluşturmanıza [Analytics](app-insights-analytics.md) toodisplay hello olay sayısı ve bunları toohello Pano sabitleyebilirsiniz.

## <a name="example"></a>Örnek
[Merhaba örneği](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService) web rolü ve iki çalışan rolleri içeren bir hizmeti izler.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Azure Cloud Services’da çalıştırma üzerine “yöntem bulunamadı” özel durumu
.NET 4.6 için mi oluşturdunuz? 4.6 sürümü Azure Cloud Services rollerinde otomatik olarak desteklenmez. Uygulamanızı çalıştırmadan önce [her role 4.6 sürümünü yükleyin](../cloud-services/cloud-services-dotnet-install-dotnet.md).

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Sonraki adımlar
* [Azure tanılama tooApplication Öngörüler gönderme yapılandırın](app-insights-azure-diagnostics.md)
* [Application Insights kaynakları oluşturmayı otomatikleştirme](app-insights-powershell.md)
* [Azure tanılamayı otomatikleştirme](app-insights-powershell-azure-diagnostics.md)
* [Azure İşlevleri](https://github.com/christopheranderson/azure-functions-app-insights-sample)

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[azure]: app-insights-azure.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[netlogs]: app-insights-asp-net-trace-logs.md
[portal]: http://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md 
