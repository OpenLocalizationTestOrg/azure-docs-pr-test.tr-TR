---
title: "(Azure App Service'te test beta) aaaFlighting dağıtımı"
description: "Uygulama veya beta tooflight yeni özellikler, güncelleştirmeleri bu uçtan uca öğretici test nasıl öğrenin. Ayrıca sürekli yayımlama, yuvaları, trafik yönlendirme ve Application Insights tümleştirme gibi uygulama hizmeti özellikleri araya getirir."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a>(Azure App Service'te test beta) flighting dağıtımı
Bu öğretici şunların nasıl yapıldığını gösterir toodo *flighting dağıtımları* tümleştirerek çeşitli özelliklerini hello [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) ve [Azure Application Insights](/services/application-insights/).

*Flighting* bir yeni özellik veya sınırlı sayıda gerçek müşteri değişiklikle doğrulayan bir dağıtım işlemidir ve ana üretim senaryosunda test etmektir. Akin toobeta olan sınama ve bazen "denetimli test uçuş" bilinir. Bir web varlığı çok büyük ölçekli işletmeler için erken doğrulama bunların bir uygulamada kendi uygulama güncelleştirmelerini almak üzere bu yaklaşımı kullanın [Çevik Geliştirme](https://en.wikipedia.org/wiki/Agile_software_development). Application Insights tooimplement hello aynı DevOps senaryo ve Azure uygulama hizmeti sürekli yayımlama ile üretimde toointegrate test sağlar. Bu yaklaşımın avantajları şunlardır:

* **Gerçek geri bildirim sağlamak *önce* güncelleştirmelerin yayımlanan tooproduction** -bırakmadan önce yayın hemen sonra geri bildirim sağlamasını daha iyi bir şey geribildirim sağlamasını yalnızca hello. Gerçek kullanıcı trafiği ve davranışları güncelleştirmeleriyle hello ürün yaşam döngüsünde işlemleriniz olabildiğince erken test edebilirsiniz.
* **Geliştirmek [sürekli teste dayalı geliştirme (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**  - kullanıcı doğrulama ürün yaşam döngüsünde erken ve otomatik olarak gerçekleşir üretim aşamasındaki bir test sürekli tümleştirme ve Application Insights ile araçları ile tümleştirme. Bu, el ile test yürütme zamanı yatırım azaltılmasına yardımcı olur.
* **Test iş akışı en iyi duruma getirme** -sürekli izleme araçları ile üretim aşamasındaki bir test otomatik hale getirerek, potansiyel olarak tek bir işlem testlerinde çeşitli hello amaçları gibi gerçekleştirebilirsiniz [tümleştirme](https://en.wikipedia.org/wiki/Integration_testing), [regresyon](https://en.wikipedia.org/wiki/Regression_testing), [kullanılabilirlik](https://en.wikipedia.org/wiki/Usability_testing), erişilebilirlik, yerelleştirme, [performans](https://en.wikipedia.org/wiki/Software_performance_testing), [güvenlik](https://en.wikipedia.org/wiki/Security_testing), ve [ kabul](https://en.wikipedia.org/wiki/Acceptance_testing).

Flighting dağıtım neredeyse dinamik trafik yönlendirme değil. Böyle bir dağıtımda toogain Insight mümkün olan en kısa sürede olması gerekmediğini beklenmeyen bir hata, bir performans düşüşü, kullanıcı deneyimi sorunları istiyor. Gerçek müşterilerle çalışıyorsanız unutmayın. Bunu toodo, sağ, içinde toomake bilinçli bir karar sonraki adımınız için sipariş tüm hello veri flighting, dağıtım toogather ayarladığınızdan emin olmanız gerekir. Bu öğreticide gösterilmiştir nasıl toocollect verilerin Application Insights, ancak New Relic veya kullanabilirler senaryonuza uygun diğer teknolojiler.

## <a name="what-you-will-do"></a>Ne yapacağını
Bu öğreticide şunları öğreneceksiniz nasıl toobring senaryoları birlikte tootest uygulama hizmeti uygulamanızı üretim hello:

* [Üretim trafiği yönlendirmek](app-service-web-test-in-production-get-start.md) tooyour beta uygulama
* [Uygulamanızı izleme](../application-insights/app-insights-web-track-usage.md) tooobtain yararlı ölçümler
* Sürekli olarak beta uygulamanızı dağıtma ve dinamik uygulama ölçümleri izleme
* Merhaba üretim uygulama ve kod nasıl değiştiğini hello beta uygulama toosee arasında karşılaştırma ölçümleri tooresults Çevir

## <a name="what-you-will-need"></a>İhtiyacınız olacak
* Bir Azure hesabı
* A [GitHub](https://github.com/) hesabı
* Visual Studio 2015 - hello yükleyebilir [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).
* Git Kabuğu (yüklenmiş [Windows için GitHub](https://windows.github.com/))-Bu, toorun hello hem hello Git ve PowerShell komutları sağlar aynı oturum
* En son [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) BITS
* Merhaba aşağıdaki temel anlama:
  * [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) şablon dağıtımı (bkz [beklendiği azure'da karmaşık bir uygulama dağıtmak](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Bu öğretici bir Azure hesabı toocomplete gerekir:
>
> * Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/) -krediler alırsınız Ücretli Azure hizmetlerini tootry çıkışı kullanabilirsiniz ve hatta kullanıldıktan sonra hello hesabı tutabilir ve ücretsiz Web uygulamaları gibi Azure hizmetlerini kullanabilirsiniz.
> * Yapabilecekleriniz [Visual Studio abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -bilgisayarınızı Visual Studio abonelik size kredi verir Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay.
>
> Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin](https://azure.microsoft.com/try/app-service/), burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz. Kredi kartı ve taahhüt gerekmez.
>
>

## <a name="set-up-your-production-web-app"></a>Üretim web uygulamanızı ayarlayın
> [!NOTE]
> Bu öğreticide kullanılan hello betik GitHub havuzunuzdan sürekli yayımlama otomatik olarak yapılandırır. Bu gerektirir GitHub kimlik bilgilerinizi zaten Azure'da depolanır, aksi takdirde komut dosyasıyla hello dağıtım tooconfigure kaynak denetim ayarları hello web uygulamaları için çalışırken başarısız olur.
>
> toostore, GitHub kimlik bilgileri, Azure'da hello bir web uygulaması oluşturma [Azure Portal](https://portal.azure.com/) ve [GitHub dağıtımını yapılandırma](app-service-continuous-deployment.md). Toodo yalnızca bu kez gerekir.
>
>

Tipik bir DevOps senaryo azure'da çalışan bir uygulamanız varsa ve sürekli yayımı üzerinden toomake değişiklikleri tooit istiyor. Bu senaryoda, tooproduction geliştirilen ve sınanmış bir şablon dağıtır.

1. Merhaba, kendi çatalı oluşturma [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) deposu. Çatalı oluşturma hakkında daha fazla bilgi için bkz: [bir depoyu Çatallaştırma](https://help.github.com/articles/fork-a-repo/). Çatalı oluşturulduktan sonra tarayıcınızı görebilirsiniz.

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Git kabuk oturumu açın. Git Kabuk henüz yoksa, yükleme [Windows için GitHub](https://windows.github.com/) şimdi.
3. Merhaba aşağıdaki komutu çalıştırarak, çatalı yerel bir kopyasını oluşturun:

     Git kopya https://github.com/<your_fork>/ToDoApp.git
4. Yerel kopya sahip olduğunda, çok gidin*&lt;repository_root >*\ARMTemplates ve çalışma hello deploy.ps1 aşağıdaki komut dosyası gösterildiği gibi benzersiz bir son eke sahip:

     .\deploy.ps1 – RepoUrl https://github.com/<your_fork>/todoapp.git - ResourceGroupSuffix < your_suffix >
5. İstendiğinde, istenen hello kullanıcı adı ve veritabanı erişimi için parola yazın. Veritabanınızı toospecify gerekir çünkü kimlik bilgilerini Hatırla onları yeniden zaman güncelleştirme hello kaynak grubu.

   Çeşitli Azure kaynaklarını ilerlemesini sağlama hello görmeniz gerekir. Dağıtım tamamlandığında hello betik hello tarayıcıda hello uygulamasını başlatın ve kolay bip sesi verin.
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. Geri Git Kabuk oturumunuzda çalıştırın:

     . \swap – adı ToDoApp < your_suffix >

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. Merhaba betik tamamlandığında toobrowse toohello frontend'ın adresi geri dönün (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) üretimde çalışan toosee Merhaba uygulaması.
8. Merhaba günlüğüne [Azure Portal](https://portal.azure.com/) ve ne oluşturulan bir göz atalım.

   Merhaba mümkün toosee iki web uygulamalarında olmalıdır aynı kaynak grubu, hello biriyle `Api` hello adı soneki. Merhaba kaynak grubu görünümü bakarsanız, hello SQL veritabanı ve sunucu, hello uygulama hizmeti planı ve hello web uygulamaları için hazırlama yuvası hello görürsünüz. Üzerinden Hello farklı kaynaklara göz atın ve bunlarla karşılaştırmak  *&lt;repository_root >*yapılandırmaya hello şablonunda \ARMTemplates\ProdAndStage.json toosee.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

Merhaba üretim uygulamasını ayarladınız.  Şimdi, şimdi hello uygulaması için kullanılabilirlik zayıftır geri bildirim alma düşünün. Bu nedenle tooinvestigate karar verin. Uygulama toogive tooinstrument oluşturacağız, geri bildirim.

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a>Araştırın: izleme izleme ölçümünün istemci uygulamanızı
1. Açık  *&lt;repository_root >*\src\MultiChannelToDo.sln Visual Studio.
2. Çözüm sağ tıklayarak tüm Nuget paketlerini geri yüklemek > **çözüm için NuGet paketlerini Yönet** > **geri**.
3. Sağ **MultiChannelToDo.Web** > **Application Insights Telemetrisi Ekle** > **ayarlarını yapılandır** > kaynak grubu Değiştir tooToDoApp*&lt;your_suffix >* > **Application Insights Ekle tooProject**.
4. Hello Azure Portal, hello hello dikey penceresini açmak **MultiChannelToDo.Web** uygulama Insight kaynak. Merhaba sonra **uygulama sistem** kısım, tıklatın **nasıl toocollect tarayıcı sayfası veri yükleme öğrenin** > kodu kopyalayın.
5. Merhaba kopyalanan JS araçları kodu çok eklemek*&lt;repository_root >*hello kapatmadan önce yalnızca \src\MultiChannelToDo.Web\app\Index.cshtml `<heading>` etiketi. Uygulama Insight kaynağınız hello benzersiz izleme anahtarını içermesi gerekir.

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. Özel olaylar, gövde kod toohello altına aşağıdaki hello ekleyerek fare tıklamaları için tooApplication Insights gönder:

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   Bir kullanıcı herhangi bir yere hello web uygulamasında, her zaman bu JavaScript kod parçacığı Öngörüler özel olay tooApplication gönderir.
7. Git Kabuğu'nda yürütme ve değişiklikleri tooyour çatalı Github'da gönderme. Daha sonra istemcileri toorefresh tarayıcı için bekleyin.

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. Dağıtılan hello uygulama değişiklikleri tooproduction değiştirme:

     . \swap – adı ToDoApp < your_suffix >
9. Yapılandırdığınız toohello Application Insights kaynağı göz atın. Özel olaylar'ı tıklatın.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   Özel olaylar için ölçümleri görmüyorsanız, birkaç dakika bekleyin ve tıklayın **yenileme**.

Bir grafik gördüğünüz varsayalım ister altında:

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

Ve olay kılavuz altındaki hello:

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

Tooyour ToDoApp uygulama koduna göre hello **düğmesini** olay karşılık gelen toohello Gönder düğmesi ve hello **giriş** olay toohello textbox karşılık gelir. Şu ana kadar şeyler anlamlıdır. Ancak, iyi miktarını tıklar ve çok az tıklama hello yapılacak işler öğelerinde gibi görünür (Merhaba **LI** olayları).

Bazı kullanıcılar, varsayımınızın hello hangi kısmına UI tıklanabilir ve hello liste öğelerini ve simgelerine geldiğinde hello imleç için metin seçimi stilde çünkü kafası bu formda, size temel.

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

Bu contrived bir örnek olabilir. Bununla birlikte, devam eden toomake geliştirme tooyour uygulama olduğunuz ve flighting bir dağıtım tooget kullanılabilirlik geri bildirim Canlı müşterilerden gerçekleştirin.

### <a name="instrument-your-server-app-for-monitoringmetrics"></a>Sunucu uygulamanız için izleme ölçümleri izleme
Bu öğreticide gösterilen hello senaryo yalnızca hello istemci uygulaması ile ilgilenir bu yana bir tanjantını budur. Ancak, bütünlük açısından hello sunucu tarafı uygulama ayarlama.

1. Sağ **MultiChannelToDo** > **Application Insights Telemetrisi Ekle** > **ayarlarını yapılandır** > kaynak grubu Değiştir tooToDoApp*&lt;your_suffix >* > **Application Insights Ekle tooProject**.
2. Git Kabuğu'nda yürütme ve değişiklikleri tooyour çatalı Github'da gönderme. Daha sonra istemcileri toorefresh tarayıcı için bekleyin.

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. Dağıtılan hello uygulama değişiklikleri tooproduction değiştirme:

     . \swap – adı ToDoApp < your_suffix >

İşte bu kadar!

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a>Araştır: yuvası özgü etiketler tooyour istemci uygulaması ölçüm Ekle
Bu bölümde, hello farklı dağıtım yuvası toosend yuva özel telemetri toohello yapılandıracak aynı Application Insights kaynağı. Bu şekilde telemetri karşılaştırabilirsiniz farklı yuvaları (dağıtım ortamlarda) tooeasily gelen trafiği arasında veri uygulama değişikliklerinizi hello etkisini bakın. AT hello aynı zaman, hello kalan kısmından, toomonitor üretim uygulamanız gerektiğinde devam edebilmeniz için şekilde hello üretim trafiği ayırabilirsiniz.

İstemci davranışı verisi toplama olduğundan, şunları yapacaksınız [telemetri Başlatıcı tooyour JavaScript kodu eklemek](../application-insights/app-insights-api-filtering-sampling.md) Index.cshtml içinde. Tootest sunucu tarafı performans isterseniz, örneğin, bunu da benzer şekilde, sunucu kodunuzda yapabilirsiniz (bkz [özel olayları ve ölçümleri için Application Insights API'si](../application-insights/app-insights-api-custom-events-metrics.md).

1. İlk olarak, hello kod bewteen hello iki ekleyin `//` toohello eklenen açıklamalar aşağıda hello JavaScript bloğu içinde `<heading>` önceki etiketi.

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    Bu Başlatıcı kod hello neden `appInsights` nesne tooadd hello adlı bir özel özellik `Environment` tooevery parçası telemetri gönderir.
2. Ardından, bu özel özellik olarak ekleme bir [yuva ayarı](web-sites-staged-publishing.md#AboutConfiguration) azure'da web uygulamanız için. toodo Git Kabuk oturumunuzda komutları aşağıdaki Bu, çalışma hello.

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    Projenizdeki Hello Web.config zaten hello tanımlar `environment` uygulama ayarı. Merhaba uygulama yerel olarak test ettiğinizde bu ayar, ölçümlerinizi ile Etiketlenecek `VS Debugger`. Ancak, değişiklikleri tooAzure bastığınızda, Azure bulabilir ve hello `environment` hello web uygulamanızın yapılandırmasında bunun yerine ayarı uygulama ve ölçümlerinizi etiketli ile `Production`.
3. Yürütme ve kod değişiklikleri tooyour çatalı Github'da gönderin ve kullanıcıların toouse hello yeni uygulamanız için (gerek toorefresh hello tarayıcısı) bekleyin. Application Insights'da yaklaşık 15 dakika hello yeni özellik tooshow işgal `MultiChannelToDo.Web` kaynak.

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. Şimdi, toohello Git **özel olayları** dikey penceresinde tekrar ve filtre üzerinde ölçümleri hello `Environment=Production`. Artık bu filtre ile tüm hello yeni özel olaylar hello üretim yuvası mümkün toosee olması gerekir.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. Merhaba tıklatın **Sık Kullanılanlar** düğmesini toosave hello Geçerli ölçüm Gezgini ayarları toosomething ister **özel olayları: üretim**. Kolayca bu görünümü ve bir dağıtım yuvası görünüm arasında daha sonra geçiş yapabilirsiniz.

   > [!TIP]
   > Daha güçlü analytics için göz önünde bulundurun [Application Insights kaynağınıza Power BI ile tümleştirme](../application-insights/app-insights-export-power-bi.md).
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a>Yuva özgü etiketler tooyour sunucu uygulama ölçüm Ekle
Yeniden, bütünlük açısından hello sunucu tarafı uygulama ayarlama. JavaScript'te izlenmiş hello istemci uygulaması, yuva özgü etiketler hello sunucu uygulaması için izlenmiş .NET koduyla.

1. Açık  *&lt;repository_root >*\src\MultiChannelToDo\Global.asax.cs. Yalnızca ad alanı kuşak kapatma hello önce aşağıda Hello kod bloğunu ekleyin.

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. Merhaba ekleyerek hello ad çözümleme hataları düzeltin `using` toohello başına aşağıdaki deyimleri hello dosyasının:

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. Merhaba toohello başlangıcını aşağıda Hello kodu ekleyin `Application_Start()` yöntemi:

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. Yürütme ve kod değişiklikleri tooyour çatalı Github'da gönderin ve kullanıcıların toouse hello yeni uygulamanız için (gerek toorefresh hello tarayıcısı) bekleyin. Application Insights'da yaklaşık 15 dakika hello yeni özellik tooshow işgal `MultiChannelToDo` kaynak.

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a>Güncelleştirmesi: Beta dal ayarlama
1. Açık  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json ve bulma hello `appsettings` kaynakları (arama `"name": "appsettings"`). Biri, her yuva için bir tane 4 vardır.
2. Her `appsettings` kaynak eklemek bir `"environment": "[parameters('slotName')]"` uygulama ayarı toohello hello sonuna `properties` dizi. Virgül ile tooend hello önceki satıra unutmayın.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    Merhaba eklemiş olduğunuz `environment` uygulama tooall hello yuvaları hello şablonunda ayarlama.
3. Buna Merhaba aynı dosya, hello bulur `slotconfignames` kaynakları (arama `"name": "slotconfignames"`). Her uygulama için bir tane bunların, 2 vardır.
4. Her `slotconfignames` kaynak eklemek `"environment"` hello toohello sonuna `appSettingNames` dizi. Virgül ile tooend hello önceki satıra unutmayın.

    Merhaba yaptığınız `environment` uygulama ayarı çubuğu tooits ilgili dağıtım yuvası hem uygulamalar için.  
5. Çalışma hello aşağıdaki Git Kabuk oturumunuzda hello ile aynı komutları önce kullandığınız kaynak grubu soneki.

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. İstendiğinde, belirtin öncekiyle aynı SQL veritabanı kimlik bilgileri hello. Ardından, ne zaman sorulan tooupdate hello kaynak grubu, türü `Y`, ardından `ENTER`.

    Merhaba betik tamamlandıktan, hello özgün kaynak grubundaki tüm kaynaklarınızı korunur, ancak "beta" adlı yeni bir yuva içinde hello ile aynı oluşturulduktan sonra hello'den itibaren oluşturulduğu hello "Hazırlama" yuvası yapılandırması.

   > [!NOTE]
   > Bu yöntem farklı dağıtım ortamları oluşturma hello yönteminden farklıdır [Azure App Service ile Çevik Yazılım Geliştirme](app-service-agile-software-development.md). Burada, beklenmediğini dağıtım ortamları kaynak gruplarıyla oluşturduğunuz dağıtım yuvası ile dağıtım ortamlar oluşturun. Dağıtım ortamları kaynak gruplarıyla yönetme tookeep hello üretim ortamı off-limits toodevelopers sağlar, ancak yuvası ile kolayca yapabilirsiniz üretim test kolay toodo değil.
   >
   >

İsterseniz, ayrıca bir alfa uygulamayı çalıştırarak oluşturabilirsiniz

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

Bu öğretici için yalnızca beta uygulamanızı kullanmaya devam eder.

## <a name="update-push-your-updates-toohello-beta-app"></a>Güncelleştirme: güncelleştirmeleri toohello beta uygulamanıza anında iletme
Tooimprove istediğiniz tooyour uygulama yedekleyin.

1. Şimdi, beta dalında olduğunuzdan emin olun

        git checkout beta
2. İçinde  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, Bul hello `<li>` etiketi ve hello eklemek `style="cursor:pointer"` , aşağıda gösterildiği gibi özniteliği.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. yürütme ve anında iletme tooAzure.
4. Merhaba değişiklik şimdi hello beta yuvada toohttp://todoapp giderek yansıtılır doğrulayın*&lt;your_suffix >*-beta.azurewebsites.net/. Değiştirme henüz, tarayıcı tooget hello yeni javascript kodu Yenile hello görmüyorsanız.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

Merhaba beta yuvasında çalıştıran değişikliğinizin sahip olduğunuza göre hazır tooperform flighting dağıtım olduğunuz.

## <a name="validate-route-traffic-toohello-beta-app"></a>Doğrulama: Rota trafiği toohello beta uygulama
Bu bölümde, trafik toohello beta uygulama yönlendirir. For sake of daha anlaşılır olması, tanıtım tooroute hello kullanıcı trafiği tooit önemli bir kısmını oluşturacağız. Gerçekte, tooroute belirli durumunuza bağlıdır istediğiniz trafik miktarı hello. Örneğin, siteniz microsoft.com hello ölçekte ise, toplam trafiğinizi sipariş toogain yararlı verilerdeki yüzde biri'den az gerekebilir.

1. Git Kabuk oturumunuzda komutları tooroute aşağıdaki hello hello üretim trafiği toohello beta yuvası yarısı çalıştırın:

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   Merhaba `ReroutePercentage=50` özelliği, % 50'hello üretim trafik yönlendirilmiş toohello beta uygulamanızın URL'sine olacağını belirtir (Merhaba tarafından belirtilen `ActionHostName` özelliği).
2. Şimdi toohttp://ToDoApp gidin*&lt;your_suffix >*. azurewebsites.net. % 50'hello trafik artık yeniden yönlendirilen toohello beta yuvası olması gerekir.
3. Application Insights kaynağınıza hello ölçümleri ortamı tarafından filtre "beta" =.

   > [!NOTE]
   > Bu filtre uygulanmış bir görünüm başka bir sık kullanılan olarak kaydederseniz, hello ölçüm Gezgini görünümler üretim ve beta görünümler arasında kolayca çevirebilirsiniz.
   >
   >

Application Insights'ta benzeri toohello aşağıdakilere bakın varsayın:

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

Yalnızca bu hello pek çok daha fazla tıklar olduğunu gösteriyor `<li>` etiketleri yok gibi görünüyor, ancak toobe dalgalanma tıklama `<li>` etiketler. Ardından kişiler hello yeni bulunmuş tamamlanabilmesi `<li>` etiketleri tıklanabilir ve tüm daha önce tamamlandı görevlerini hello uygulamasında artık temizleme.

Flighting dağıtımınızı Hello verilerini temel alarak yeni UI üretime hazır olduğuna karar verin.

## <a name="go-live-move-your-new-code-into-production"></a>Canlı gidin: yeni kodunuzu üretim ortamına taşıyın
Güncelleştirme tooproduction şimdi hazır toomove demektir. Artık güncelleştirmenizi zaten doğrulandı biliyorsunuz harika nedir olan *önce* tooproduction gönderilir. Artık bunu güvenle dağıtabilir. Bir güncelleştirme toohello AngularJS istemci uygulama tarafından olduğundan, yalnızca hello istemci-tarafı kodu doğrulandı. Toomake değişiklikleri toohello arka uç Web API uygulaması olsaydı, değişikliklerinizi benzer şekilde ve kolayca doğrulamak.

1. Git Kabuğu'nda hello trafik yönlendirme kuralı hello aşağıdaki komutu çalıştırarak kaldırın:

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. Merhaba Git komutları çalıştırın:

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. Yeni hello için bir kaç dakika hazırlık yuvasındaki dağıtılan toobe toohello kod sonra http://ToDoApp başlatma için beklemesi*&lt;your_suffix >*-yeni güncelleştirme hello staging.azurewebsites.net tooverify warmed hello hazırlama Yuva. Çatalı ait ana dala olduğundan bu hello bağlı toohello hazırlama unutmayın, uygulamanızın yuvası.
4. Şimdi, üretime hazırlık yuvasındaki hello değiştirme

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a>Özet
Azure uygulama hizmeti küçük toomedium-ölçekli işletmeler tootest müşterilerle uygulamalarını üretimde bir şey büyük kuruluşlarda bir geleneksel yapılan kolaylaştırır. Neyse ki bu öğretici verdiği hello ihtiyacınız toobring birlikte App Service ve Application Insights toomake olası flighting dağıtım ve hatta diğer test üretimde senaryoları DevOps dünyada bilgi.

## <a name="more-resources"></a>Diğer kaynaklar
* [Azure App Service ile Çevik Yazılım Geliştirme](app-service-agile-software-development.md)
* [Hazırlık ortamları için Azure App Service'te web uygulamalarını ayarlama](web-sites-staged-publishing.md)
* [Azure'nın beklendiği karmaşık bir uygulama dağıtma](app-service-deploy-complex-application-predictably.md)
* [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - hello JSON Doğrulayıcı](http://jsonlint.com/)
* [Git dallanma – temel dallandırma ve birleştirme](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Azure PowerShell](/powershell/azure/overview)
* [Proje Kudu Wiki](https://github.com/projectkudu/kudu/wiki)
