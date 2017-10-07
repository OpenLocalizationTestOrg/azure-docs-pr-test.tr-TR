---
title: "aaaDiagnose hataları ve özel durumları web uygulamaları Azure Application Insights ile | Microsoft Docs"
description: "ASP.NET uygulamaları isteği telemetri ile birlikte özel durumları yakalar."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d1e98390-3ce4-4d04-9351-144314a42aa2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 8930e6d2b29f83ea635c4ecb7afd11fc1d97d085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-exceptions-in-your-web-apps-with-application-insights"></a>Web uygulamalarınızı Application Insights ile özel durumları tanılama
Özel durumlar, canlı web uygulamanızda tarafından bildirilen [Application Insights](app-insights-overview.md). Böylece hızla hello nedenler tanılamak özel durumlar ve diğer olayları hello istemci ve sunucu, başarısız olan istekler ilişkilendirebilirsiniz.

## <a name="set-up-exception-reporting"></a>Set up reporting özel durumu
* Sunucu uygulamanızdan bildirilen toohave özel durumlar:
  * Yükleme [Application Insights SDK'sı](app-insights-asp-net.md) , uygulama kodunuzda veya
  * IIS web sunucuları: çalıştırmak [Application Insights Aracısı](app-insights-monitor-performance-live-website-now.md); veya
  * Azure web uygulamaları: hello eklemek [uygulama Öngörüler uzantısı](app-insights-azure-web-apps.md)
  * Java web uygulamaları: yükleme hello [Java aracı](app-insights-java-agent.md)
* Merhaba yüklemek [JavaScript kod parçacığı](app-insights-javascript.md) , web sayfaları toocatch tarayıcı özel durumlarda.
* Bazı uygulama çerçeveleri veya bazı ayarlar ile bazı ek adımlar toocatch tootake gereken daha fazla özel durum:
  * [Web formları](#web-forms)
  * [MVC](#mvc)
  * [Web API 1.*](#web-api-1)
  * [Web API 2.*](#web-api-2)
  * [WCF](#wcf)

## <a name="diagnosing-exceptions-using-visual-studio"></a>Visual Studio kullanarak tanılama özel durumlar
Hata ayıklama ile Visual Studio toohelp Hello uygulama çözümü açın.

Merhaba uygulama sunucunuzda veya geliştirme makinenizde F5 kullanarak çalıştırın.

Visual Studio'da Hello uygulama Insights arama penceresi açın ve uygulamanızdan toodisplay olayları ayarlayın. Hatalarını ayıkladığınız sırada yalnızca hello Application Insights düğmesine tıklayarak bunu yapabilirsiniz.

![Merhaba projesine sağ tıklayın ve Application Insights seçme açın.](./media/app-insights-asp-net-exceptions/34.png)

Merhaba rapor tooshow yalnızca özel durumlar filtreleyebilirsiniz dikkat edin.

*Özel durumlar gösteren? Bkz: [özel durumları yakalama](#exceptions).*

Bir özel durum raporu tooshow Yığın İzleme'yi tıklatın.
Merhaba yığın izlemesi, tooopen hello ilgili kod dosyası satırı başvurusunda'ı tıklatın.  

Merhaba kodda CodeLens hello özel durumlar hakkında veri gösterdiğine dikkat edin:

![Özel durumlar CodeLens bildirimi.](./media/app-insights-asp-net-exceptions/35.png)

## <a name="diagnosing-failures-using-hello-azure-portal"></a>Hello Azure portal kullanarak hataları tanılama
Merhaba Application Insights genel bakış, uygulamanızın hello hatalar kutucuğuna özel durumlar grafiklerini gösterir ve HTTP isteklerini hello listesini birlikte hello en sık rastlanan hatalarına neden URL'leri isteği başarısız.

![Ayarları, hataları seçin](./media/app-insights-asp-net-exceptions/012-start.png)

Merhaba birini geçişli tıklatma burada hello ayrıntıları görmek ve izleme yığın hello özel durum, özel durum türleri hello listesi tooget tooindividual oluşum içinde başarısız oldu:

![Başarısız bir istek ve özel durum ayrıntıları altında bir örnek seçin, hello özel durum tooinstances Al.](./media/app-insights-asp-net-exceptions/030-req-drill.png)

**Alternatif olarak,** istekleri hello listesinden başlama ve özel durumları ilgili tooit bulabilirsiniz.

*Özel durumlar gösteren? Bkz: [özel durumları yakalama](#exceptions).*


## <a name="custom-tracing-and-log-data"></a>Özel İzleme ve günlük verileri
tooget tanılama veri belirli tooyour uygulama, kod toosend ekleyebilirsiniz kendi telemetri verileri. Bu tanılama arama hello isteğinin, sayfa görünümü ve diğer otomatik olarak toplanan verileri yanında görüntülenir.

Birkaç seçeneğiniz vardır:

* [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) genellikle hello gönderdiği ayrıca veri tanılama Arama'da özel olayları altında görünür ancak kullanım desenlerini izlemek için kullanılır. Olayları adlandırılır ve dize özellikleri ve üzerinde yapabilecekleriniz sayısal ölçümleri taşıyabilir [tanılama aramalarınız filtre](app-insights-diagnostic-search.md).
* [TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) POST bilgileri gibi daha uzun veri göndermesini sağlar.
* [TrackException()](#exceptions) yığın izlemeler gönderir. [Özel durumlar hakkında daha fazla](#exceptions).
* Log4Net veya NLog gibi günlük framework kullanırsanız, yapabilecekleriniz [Bu günlükleri yakalama](app-insights-asp-net-trace-logs.md) ve bunları istek ve özel durum verilerin yanında tanılama arama bölümüne bakın.

Bu olaylar toosee açmak [arama](app-insights-diagnostic-search.md)filtre açın ve ardından özel olay, izleme veya özel durumu seçin.

![Detaylandırma](./media/app-insights-asp-net-exceptions/viewCustomEvents.png)

> [!NOTE]
> Uygulamanız çok sayıda telemetri oluşturuyorsa hello Uyarlamalı örnekleme modülü olayların yalnızca bir temsilci fraksiyonunu göndererek toohello portal gönderilen hello birim otomatik olarak azaltır. Aynı işlemi seçili veya bir grup olarak işaretli hello parçası olan ve böylece ilgili olaylar arasında gezinebilirsiniz olaylar. [Örnekleme hakkında bilgi edinin.](app-insights-sampling.md)
>
>

### <a name="how-toosee-request-post-data"></a>Nasıl toosee isteği gönderme verisi
İstek Ayrıntıları tooyour uygulama bir POST çağrısında gönderilen hello veri eklemeyin. Bu veriler bildirdiği toohave:

* [Merhaba SDK yükleme](app-insights-asp-net.md) uygulama projenizdeki.
* Kod, uygulama toocall ekleme [Microsoft.ApplicationInsights.TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace). Merhaba gönderme verisi hello ileti parametresinde gönderin. Olmadığından sınırı izin verilen toohello boyutu toosend yalnızca hello gerekli verileri denemelisiniz.
* Başarısız bir istek incelediğinizde, ilişkili hello izlemeleri bulun.  

![Detaylandırma](./media/app-insights-asp-net-exceptions/060-req-related.png)

## <a name="exceptions"></a>Özel durumlar ve ilgili Tanılama verileri yakalama
İlk başta, uygulamanızda hatalarına neden tüm hello özel durumları hello portalında görmez. Tarayıcı özel durumlar görürsünüz (Merhaba kullanıyorsanız [JavaScript SDK'sı](app-insights-javascript.md) web sayfalarınızda). Çoğu sunucu özel durumları IIS tarafından yakalanan ve toowrite biraz kod toosee sahip olan ancak bunları.

Şunları yapabilirsiniz:

* **Özel durumlar açıkça oturum** kodu özel durum işleyicileri tooreport hello durumlar ekleyerek.
* **Özel durumlar otomatik olarak yakalama** , ASP.NET framework yapılandırarak. Merhaba gerekli eklemeleri framework'ün farklı türleri için farklıdır.

## <a name="reporting-exceptions-explicitly"></a>Özel durumlar açıkça raporlama
Merhaba basit tooinsert çağrısı tooTrackException() bir özel durum işleyici içinde yoldur.

JavaScript

    try
    { ...
    }
    catch (ex)
    {
      appInsights.trackException(ex, "handler loc",
        {Game: currentGame.Name,
         State: currentGame.State.ToString()});
    }

C#

    var telemetry = new TelemetryClient();
    ...
    try
    { ...
    }
    catch (Exception ex)
    {
       // Set up some properties:
       var properties = new Dictionary <string, string>
         {{"Game", currentGame.Name}};

       var measurements = new Dictionary <string, double>
         {{"Users", currentGame.Users.Count}};

       // Send hello exception telemetry:
       telemetry.TrackException(ex, properties, measurements);
    }

VB

    Dim telemetry = New TelemetryClient
    ...
    Try
      ...
    Catch ex as Exception
      ' Set up some properties:
      Dim properties = New Dictionary (Of String, String)
      properties.Add("Game", currentGame.Name)

      Dim measurements = New Dictionary (Of String, Double)
      measurements.Add("Users", currentGame.Users.Count)

      ' Send hello exception telemetry:
      telemetry.TrackException(ex, properties, measurements)
    End Try

Merhaba özellikleri ve ölçülerini parametreler isteğe bağlıdır, ancak için yararlı olan [filtreleme ve ekleyerek](app-insights-diagnostic-search.md) ek bilgiler. Örneğin, birkaç oyunlar çalıştırabilirsiniz bir uygulamanız varsa, tüm hello özel durum raporları ilgili tooa belirli oyun bulunamadı. Tooeach sözlük gibi sayıda öğe ekleyebilirsiniz.

## <a name="browser-exceptions"></a>Tarayıcı özel durumları
Çoğu tarayıcı özel durumları raporlanır.

Web sayfanızın içerik teslim ağlara veya diğer etki alanından komut dosyaları içeriyorsa, komut dosyası etiketinin hello özniteliği olduğundan emin olun ```crossorigin="anonymous"```, ve hello sunucu gönderir [CORS üstbilgilerini](http://enable-cors.org/). Bu tooget yığın izlemesi ve bu kaynaklardan işlenmemiş JavaScript özel durumlarının ayrıntı sağlayacaktır.

## <a name="web-forms"></a>Web formları
Web formları için CustomErrors ile yapılandırılmış hiçbir yeniden yönlendirmeleri olduğunda hello HTTP modülü mümkün toocollect hello özel durumlar olacaktır.

Ancak etkin yeniden yönlendirmeleri varsa, aşağıdaki satırları toohello uygulama_hatası Global.asax.cs işlevinde hello ekleyin. (Zaten yoksa, Global.asax dosyası ekleyin.)

*C#*

    void Application_Error(object sender, EventArgs e)
    {
      if (HttpContext.Current.IsCustomErrorEnabled && Server.GetLastError  () != null)
      {
         var ai = new TelemetryClient(); // or re-use an existing instance

         ai.TrackException(Server.GetLastError());
      }
    }


## <a name="mvc"></a>MVC
Merhaba, [CustomErrors](https://msdn.microsoft.com/library/h0hfz6fc.aspx) Yapılandırması `Off`, özel durumlar hello için kullanılabilecek sonra [HTTP modülü](https://msdn.microsoft.com/library/ms178468.aspx) toocollect. Ancak, bu ise `RemoteOnly` (varsayılan) veya `On`, ardından hello özel durum temizlendi ve Application Insights için kullanılamaz tooautomatically topla. Hello geçersiz kılarak düzeltme [System.Web.Mvc.HandleErrorAttribute sınıfı](http://msdn.microsoft.com/library/system.web.mvc.handleerrorattribute.aspx)ve hello farklı MVC sürümleri için aşağıda gösterildiği gibi hello geçersiz sınıf uygulama ([github kaynağına](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions/blob/master/MVC2App/Controllers/AiHandleErrorAttribute.cs)):

    using System;
    using System.Web.Mvc;
    using Microsoft.ApplicationInsights;

    namespace MVC2App.Controllers
    {
      [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
      public class AiHandleErrorAttribute : HandleErrorAttribute
      {
        public override void OnException(ExceptionContext filterContext)
        {
            if (filterContext != null && filterContext.HttpContext != null && filterContext.Exception != null)
            {
                //If customError is Off, then AI HTTPModule will report hello exception
                if (filterContext.HttpContext.IsCustomErrorEnabled)
                {   //or reuse instance (recommended!). see note above  
                    var ai = new TelemetryClient();
                    ai.TrackException(filterContext.Exception);
                }
            }
            base.OnException(filterContext);
        }
      }
    }

#### <a name="mvc-2"></a>MVC 2
Merhaba HandleError özniteliği yeni özniteliğinizi denetleyicilerinizi değiştirin.

    namespace MVC2App.Controllers
    {
       [AiHandleError]
       public class HomeController : Controller
       {
    ...

[Örnek](https://github.com/AppInsightsSamples/Mvc2UnhandledExceptions)

#### <a name="mvc-3"></a>MVC 3
Kayıt `AiHandleErrorAttribute` Global.asax.cs genel filtre olarak:

    public class MyMvcApplication : System.Web.HttpApplication
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
         filters.Add(new AiHandleErrorAttribute());
      }
     ...

[Örnek](https://github.com/AppInsightsSamples/Mvc3UnhandledExceptionTelemetry)

#### <a name="mvc-4-mvc5"></a>MVC 4, MVC5
FilterConfig.cs genel filtre olarak AiHandleErrorAttribute kaydedin:

    public class FilterConfig
    {
      public static void RegisterGlobalFilters(GlobalFilterCollection filters)
      {
        // Default replaced with hello override tootrack unhandled exceptions
        filters.Add(new AiHandleErrorAttribute());
      }
    }

[Örnek](https://github.com/AppInsightsSamples/Mvc5UnhandledExceptionTelemetry)

## <a name="web-api-1x"></a>Web API 1.x
System.Web.Http.Filters.ExceptionFilterAttribute geçersiz kıl:

    using System.Web.Http.Filters;
    using Microsoft.ApplicationInsights;

    namespace WebAPI.App_Start
    {
      public class AiExceptionFilterAttribute : ExceptionFilterAttribute
      {
        public override void OnException(HttpActionExecutedContext actionExecutedContext)
        {
            if (actionExecutedContext != null && actionExecutedContext.Exception != null)
            {  //or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(actionExecutedContext.Exception);    
            }
            base.OnException(actionExecutedContext);
        }
      }
    }

Bu geçersiz kılınan özniteliği toospecific denetleyicileri ekleme ya da hello WebApiConfig sınıfının toohello genel filtre yapılandırması eklemek:

    using System.Web.Http;
    using WebApi1.x.App_Start;

    namespace WebApi1.x
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            config.Routes.MapHttpRoute(name: "DefaultApi", routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional });
            ...
            config.EnableSystemDiagnosticsTracing();

            // Capture exceptions for Application Insights:
            config.Filters.Add(new AiExceptionFilterAttribute());
        }
      }
    }

[Örnek](https://github.com/AppInsightsSamples/WebApi_1.x_UnhandledExceptions)

Merhaba özel durum filtreleri işleyemiyor durumlarda mevcuttur. Örneğin:

* Denetleyici oluşturucular oluşturulan özel durumları.
* İleti işleyicileri oluşturulan özel durumları.
* Yönlendirme sırasında oluşturulan özel durumları.
* Yanıtın içerik serileştirilmesi sırasında oluşturulan özel durumları.

## <a name="web-api-2x"></a>Web API 2.x
IExceptionLogger uygulaması ekleyin:

    using System.Web.Http.ExceptionHandling;
    using Microsoft.ApplicationInsights;

    namespace ProductsAppPureWebAPI.App_Start
    {
      public class AiExceptionLogger : ExceptionLogger
      {
        public override void Log(ExceptionLoggerContext context)
        {
            if (context !=null && context.Exception != null)
            {//or reuse instance (recommended!). see note above
                var ai = new TelemetryClient();
                ai.TrackException(context.Exception);
            }
            base.Log(context);
        }
      }
    }

Bu toohello Hizmetleri içinde WebApiConfig ekleyin:

    using System.Web.Http;
    using System.Web.Http.ExceptionHandling;
    using ProductsAppPureWebAPI.App_Start;

    namespace WebApi2WithMVC
    {
      public static class WebApiConfig
      {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );
            config.Services.Add(typeof(IExceptionLogger), new AiExceptionLogger());
        }
      }
  }

[Örnek](https://github.com/AppInsightsSamples/WebApi_2.x_UnhandledExceptions)

Alternatif, şunları yapabilir:

1. Yerine yalnızca ExceptionHandler IExceptionHandler, özel bir uygulama hello. Merhaba framework koruyabilmeyi toochoose hangi yanıt iletisi toosend (Merhaba bağlantısı örneği için iptal edildiğinde değil) olduğunda bu yalnızca çağrılır
2. Her durumda değil olarak adlandırılan özel durum filtreleri (açıklandığı gibi hello bölümünde Web API'sini 1.x denetleyicilerinde yukarıdaki) -.

## <a name="wcf"></a>WCF
Öznitelik genişleten ve IErrorHandler ve IServiceBehavior uygulayan bir sınıf ekleyin.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.ServiceModel.Description;
    using System.ServiceModel.Dispatcher;
    using System.Web;
    using Microsoft.ApplicationInsights;

    namespace WcfService4.ErrorHandling
    {
      public class AiLogExceptionAttribute : Attribute, IErrorHandler, IServiceBehavior
      {
        public void AddBindingParameters(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase,
            System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints,
            System.ServiceModel.Channels.BindingParameterCollection bindingParameters)
        {
        }

        public void ApplyDispatchBehavior(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
            foreach (ChannelDispatcher disp in serviceHostBase.ChannelDispatchers)
            {
                disp.ErrorHandlers.Add(this);
            }
        }

        public void Validate(ServiceDescription serviceDescription,
            System.ServiceModel.ServiceHostBase serviceHostBase)
        {
        }

        bool IErrorHandler.HandleError(Exception error)
        {//or reuse instance (recommended!). see note above
            var ai = new TelemetryClient();

            ai.TrackException(error);
            return false;
        }

        void IErrorHandler.ProvideFault(Exception error,
            System.ServiceModel.Channels.MessageVersion version,
            ref System.ServiceModel.Channels.Message fault)
        {
        }
      }
    }

Merhaba özniteliği toohello hizmet uygulamaları ekleyin:

    namespace WcfService4
    {
        [AiLogException]
        public class Service1 : IService1
        {
         ...

[Örnek](https://github.com/AppInsightsSamples/WCFUnhandledExceptions)

## <a name="exception-performance-counters"></a>Özel durum performans sayaçları
Varsa [hello Application Insights aracısı yüklü](app-insights-monitor-performance-live-website-now.md) sunucunuz üzerinde bir grafik .NET tarafından ölçülür hello özel durumlara oranı elde edebilirsiniz. Bu, işlenen ve işlenmeyen özel durumları .NET içerir.

Ölçüm Gezgini dikey penceresini açın, yeni bir grafik ekleyin ve seçin **özel durum oranı**, performans sayaçları altında listelenen.

Hello .NET framework ile özel durum sayısı hello bir zaman aralığı sayım ve hello hello aralığı uzunluğuna bölünmesi hello oranı hesaplar.

Merhaba Application Insights portalı tarafından TrackException raporları sayım tarafından hesaplanan hello 'özel durumları' sayısı farklı olacağını unutmayın. Merhaba örnekleme aralıkları farklıdır ve hello SDK TrackException raporları tüm işlenen ve işlenmeyen özel durumlar için göndermez.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="next-steps"></a>Sonraki adımlar
* [REST, SQL ve diğer çağrıları toodependencies izleme](app-insights-asp-net-dependencies.md)
* [Sayfa yükleme sürelerinin, tarayıcı özel durumlar ve AJAX çağrıları izleme](app-insights-javascript.md)
* [İzleyici performans sayaçları](app-insights-performance-counters.md)
