---
title: "(Azure App Service'te test beta) flighting dağıtımı"
description: "Yeni özellikler, uygulamanızda uçuş veya beta bu uçtan uca öğretici, güncelleştirmeleri test öğrenin. Ayrıca sürekli yayımlama, yuvaları, trafik yönlendirme ve Application Insights tümleştirme gibi uygulama hizmeti özellikleri araya getirir."
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
ms.openlocfilehash: 83e3247310461ac148fff3c4ade3aa7216478537
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a>(Azure App Service'te test beta) flighting dağıtımı
Bu öğretici nasıl yapılacağını gösterir *flighting dağıtımları* çeşitli özelliklerini tümleştirme tarafından [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) ve [Azure Application Insights](/services/application-insights/).

*Flighting* bir yeni özellik veya sınırlı sayıda gerçek müşteri değişiklikle doğrulayan bir dağıtım işlemidir ve ana üretim senaryosunda test etmektir. Bu beta test benzer ve bazen "denetimli test uçuş" bilinir. Bir web varlığı çok büyük ölçekli işletmeler için erken doğrulama bunların bir uygulamada kendi uygulama güncelleştirmelerini almak üzere bu yaklaşımı kullanın [Çevik Geliştirme](https://en.wikipedia.org/wiki/Agile_software_development). Azure uygulama hizmeti, üretim aşamasındaki bir test sürekli yayımlama ve aynı DevOps senaryosunu uygulamak için Application Insights ile tümleştirmenize olanak sağlar. Bu yaklaşımın avantajları şunlardır:

* **Gerçek geri bildirim sağlamak *önce* güncelleştirmeleri üretime serbest** -bırakmadan önce yayın hemen sonra geri bildirim sağlamasını daha iyi tek şey geri bildirim alma. Gerçek kullanıcı trafiği ve davranışları güncelleştirmeleriyle ürün yaşam döngüsünde işlemleriniz olabildiğince erken test edebilirsiniz.
* **Geliştirmek [sürekli teste dayalı geliştirme (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)**  - kullanıcı doğrulama ürün yaşam döngüsünde erken ve otomatik olarak gerçekleşir üretim aşamasındaki bir test sürekli tümleştirme ve Application Insights ile araçları ile tümleştirme. Bu, el ile test yürütme zamanı yatırım azaltılmasına yardımcı olur.
* **Test iş akışı en iyi duruma getirme** -sürekli izleme araçları ile üretim aşamasındaki bir test otomatik hale getirerek, potansiyel olarak çeşitli tek bir işlem içinde Test amaçları gibi gerçekleştirebilirsiniz [tümleştirme](https://en.wikipedia.org/wiki/Integration_testing), [regresyon](https://en.wikipedia.org/wiki/Regression_testing), [kullanılabilirlik](https://en.wikipedia.org/wiki/Usability_testing), erişilebilirlik, yerelleştirme, [performans](https://en.wikipedia.org/wiki/Software_performance_testing), [güvenlik](https://en.wikipedia.org/wiki/Security_testing), ve [kabul](https://en.wikipedia.org/wiki/Acceptance_testing).

Flighting dağıtım neredeyse dinamik trafik yönlendirme değil. Mümkün olan en kısa sürede iyi kavramak için istediğiniz böyle bir dağıtımda, olması beklenmeyen bir hata, bir performans düşüşü, kullanıcı deneyimi sorunları. Gerçek müşterilerle çalışıyorsanız unutmayın. Bu nedenle yapmak için sağ, sonraki adımınız için bilinçli bir karar yapmak için gereken tüm verileri toplamak için flighting dağıtımınızın ayarladığınızdan emin olmanız gerekir. Bu öğretici, Application Insights ile verileri toplamak nasıl gösterir, ancak New Relic veya senaryonuza uygun diğer teknolojileri kullanabilirsiniz.

## <a name="what-you-will-do"></a>Ne yapacağını
Bu öğreticide, birlikte üretimde uygulama hizmeti uygulamanızı test etmek için aşağıdaki senaryoları Getir öğreneceksiniz:

* [Üretim trafiği yönlendirmek](app-service-web-test-in-production-get-start.md) beta uygulamanıza
* [Uygulamanızı izleme](../application-insights/app-insights-web-track-usage.md) yararlı ölçümler edinme
* Sürekli olarak beta uygulamanızı dağıtma ve dinamik uygulama ölçümleri izleme
* Ölçümleri üretim uygulamasına nasıl kod değişiklikleri sonuçları Çevir görmek için beta uygulama arasında karşılaştırma

## <a name="what-you-will-need"></a>İhtiyacınız olacak
* Bir Azure hesabı
* A [GitHub](https://github.com/) hesabı
* Visual Studio 2015 - yükleyebilir [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).
* Git Kabuğu (yüklenmiş [Windows için GitHub](https://windows.github.com/))-Bu, aynı oturumunda Git ve PowerShell komutlarını çalıştırmanıza olanak sağlar
* En son [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) BITS
* Aşağıdaki temel bilgilere:
  * [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) şablon dağıtımı (bkz [beklendiği azure'da karmaşık bir uygulama dağıtmak](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Bu öğreticiyi tamamlamak için bir Azure hesabınızın olması gerekir:
>
> * Yapabilecekleriniz [ücretsiz bir Azure hesabı açabilirsiniz](https://azure.microsoft.com/pricing/free-trial/) -krediler alırsınız, ücretli Azure hizmetlerini denemek için kullanabileceğiniz ve bunlar bitmiş bile hesabı sürdürebilir ve ücretsiz Web uygulamaları gibi Azure hizmetlerini kullanabilirsiniz.
> * Yapabilecekleriniz [Visual Studio abone Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) -bilgisayarınızı Visual Studio abonelik size kredi verir Ücretli Azure hizmetlerinizi kullanabildiğiniz her ay.
>
> Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin. Kredi kartı ve taahhüt gerekmez.
>
>

## <a name="set-up-your-production-web-app"></a>Üretim web uygulamanızı ayarlayın
> [!NOTE]
> Bu öğreticide kullanılan komut dosyası, GitHub havuzunuzdan sürekli yayımlama otomatik olarak yapılandırır. Bu gerektirir GitHub kimlik bilgilerinizi zaten Azure'da depolanır, aksi takdirde komut dosyalı dağıtım web uygulamaları için kaynak denetim ayarları yapılandırmak çalışırken başarısız olur.
>
> Azure'da GitHub kimlik bilgilerinizi depolamak için bir web uygulaması oluşturmak [Azure Portal](https://portal.azure.com/) ve [GitHub dağıtımını yapılandırma](app-service-continuous-deployment.md). Yalnızca bu kez yapmanız gerekir.
>
>

Tipik bir DevOps senaryo azure'da çalışan bir uygulamanız varsa ve kullanarak sürekli yayımlama değişiklik istiyor. Bu senaryoda üretime geliştirilen ve sınanmış bir şablon dağıtır.

1. Kendi çatalı oluşturma [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) deposu. Çatalı oluşturma hakkında daha fazla bilgi için bkz: [bir depoyu Çatallaştırma](https://help.github.com/articles/fork-a-repo/). Çatalı oluşturulduktan sonra tarayıcınızı görebilirsiniz.

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Git kabuk oturumu açın. Git Kabuk henüz yoksa, yükleme [Windows için GitHub](https://windows.github.com/) şimdi.
3. Aşağıdaki komutu çalıştırarak, çatalı yerel bir kopyasını oluşturun:

     Git kopya https://github.com/<your_fork>/ToDoApp.git
4. Yerel kopya oluşturduktan sonra gidin  *&lt;repository_root >*\ARMTemplates ve deploy.ps1 komut dosyası benzersiz bir sonek ile aşağıda gösterildiği gibi çalıştırın:

     .\deploy.ps1 – RepoUrl https://github.com/<your_fork>/todoapp.git - ResourceGroupSuffix < your_suffix >
5. İstendiğinde, istenilen kullanıcı adı ve veritabanı erişimi için parolayı yazın. Bunları kaynak grubu güncelleştirilirken yeniden belirtmeniz gerekir çünkü veritabanı kimlik bilgilerinizi unutmayın.

   Çeşitli Azure kaynaklarını hazırlama sürecini görmeniz gerekir. Dağıtım tamamlandığında, komut dosyası uygulamayı tarayıcıda başlatmak ve kolay bip sesi verin.
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. Geri Git Kabuk oturumunuzda çalıştırın:

     . \swap – adı ToDoApp < your_suffix >

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. Komut tamamlandığında, ön uç'ın adresine göz atın dönün (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) üretimde çalışan uygulama görmek için.
8. İçine oturum [Azure Portal](https://portal.azure.com/) ve ne oluşturulan bir göz atalım.

   Aynı kaynak grubunda biriyle iki web uygulamaları görmeye olmalıdır `Api` adı soneki. Kaynak grubu görünümü bakarsanız, SQL veritabanı ve sunucu, uygulama hizmeti planı ve web uygulamaları için hazırlama yuvası görürsünüz. Farklı kaynaklara göz atın ve bunlarla karşılaştırmak  *&lt;repository_root >*\ARMTemplates\ProdAndStage.json şablonda nasıl yapılandırıldıklarına bakın.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

Üretim uygulamasını ayarladınız.  Şimdi, şimdi uygulama için kullanılabilirlik zayıftır geri bildirim alma düşünün. Bu nedenle, araştırmak karar verin. Geribildirim vermek için uygulamayı izlemek oluşturacağız.

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a>Araştırın: izleme izleme ölçümünün istemci uygulamanızı
1. Açık  *&lt;repository_root >*\src\MultiChannelToDo.sln Visual Studio.
2. Çözüm sağ tıklayarak tüm Nuget paketlerini geri yüklemek > **çözüm için NuGet paketlerini Yönet** > **geri**.
3. Sağ **MultiChannelToDo.Web** > **Application Insights Telemetrisi Ekle** > **ayarlarını yapılandır** > ToDoApp değişiklik kaynak grubuna*&lt;your_suffix >* > **projeye Application Insights Ekle**.
4. Azure Portalı'nda dikey penceresini açmak **MultiChannelToDo.Web** uygulama Insight kaynak. Ardından **uygulama sistem** kısım, tıklatın **tarayıcı sayfa yükü veri toplamak öğrenin** > kodu kopyalayın.
5. Kopyalanan JS araçları koda ekleyin  *&lt;repository_root >*kapatmadan önce yalnızca \src\MultiChannelToDo.Web\app\Index.cshtml `<heading>` etiketi. Uygulama Insight kaynağınız benzersiz izleme anahtarını içermesi gerekir.

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. Özel olaylar için Application Insights için fare tıklatma gövde altına aşağıdaki kodu ekleyerek gönder:

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   Bir kullanıcı web uygulamasında her yerden, her zaman bu JavaScript kod parçacığı özel bir olay Application Insights'a gönderir.
7. Git Kabuğu'nda yürütme ve değişikliklerinizi github, çatalı iletin. Daha sonra istemcilerin tarayıcıyı yenilemek için bekleyin.

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. Üretim dağıtılmış bir uygulamayı değişiklikleri değiştirme:

     . \swap – adı ToDoApp < your_suffix >
9. Yapılandırdığınız Application Insights kaynağı göz atın. Özel olaylar'ı tıklatın.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   Özel olaylar için ölçümleri görmüyorsanız, birkaç dakika bekleyin ve tıklayın **yenileme**.

Bir grafik gördüğünüz varsayalım ister altında:

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

Ve altındaki olay kılavuz:

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

ToDoApp uygulama kodunuz göre **düğmesini** olay gönderme düğmesi için karşılık gelen ve **giriş** olay metin kutusuna karşılık gelir. Şu ana kadar şeyler anlamlıdır. Ancak, iyi miktarını tıklar ve çok az tıklama yapılacak işler öğelerinde gibi görünür ( **LI** olayları).

Bu bilgisayarda, form tabanlı bazı kullanıcılar, varsayımınızın kullanıcı arabiriminin hangi bölümünün tıklanabilir kafası ve liste öğeleri ve simgelerine geldiğinde imleci için metin seçimi stilde olmasıdır.

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

Bu contrived bir örnek olabilir. Bununla birlikte, uygulamanız için bir geliştirme yapmak ve canlı müşterilerden kullanılabilirlik geri bildirim almak için flighting bir dağıtım gerçekleştirin oluşturacağız.

### <a name="instrument-your-server-app-for-monitoringmetrics"></a>Sunucu uygulamanız için izleme ölçümleri izleme
Bu öğreticide gösterilen senaryo yalnızca istemci uygulaması ile ilgilenir bu yana bir tanjantını budur. Ancak, bütünlük açısından sunucu tarafı uygulama ayarlama.

1. Sağ **MultiChannelToDo** > **Application Insights Telemetrisi Ekle** > **ayarlarını yapılandır** > ToDoApp değişiklik kaynak grubuna*&lt;your_suffix >* > **projeye Application Insights Ekle**.
2. Git Kabuğu'nda yürütme ve değişikliklerinizi github, çatalı iletin. Daha sonra istemcilerin tarayıcıyı yenilemek için bekleyin.

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. Üretim dağıtılmış bir uygulamayı değişiklikleri değiştirme:

     . \swap – adı ToDoApp < your_suffix >

İşte bu kadar!

## <a name="investigate-add-slot-specific-tags-to-your-client-app-metrics"></a>Araştırmak: istemci uygulama ölçümlerinizi yuva özel etiketler ekleyin
Bu bölümde, yuva özel telemetri aynı Application Insights kaynağa göndermek için farklı dağıtım yuvası yapılandırır. Bu şekilde kolayca uygulama değişikliklerinizi etkisini görmek için farklı yuvaları (dağıtım ortamlarda) gelen trafiği arasında telemetri verileri karşılaştırabilirsiniz. Aynı anda gerektiğinde üretim uygulamanızı izlemek devam edebilmek için kalan kısmından üretim trafiği ayırabilirsiniz.

İstemci davranışı verisi toplama olduğundan, şunları yapacaksınız [JavaScript kodunuzu bir telemetri başlatıcı ekleyin](../application-insights/app-insights-api-filtering-sampling.md) Index.cshtml içinde. Sunucu tarafı performansını test etmek isterseniz, örneğin, bunu da benzer şekilde, sunucu kodunuzda yapabilirsiniz (bkz [özel olayları ve ölçümleri için Application Insights API'si](../application-insights/app-insights-api-custom-events-metrics.md).

1. İlk olarak, iki kod bewteen ekleyin `//` JavaScript aşağıda açıklamaları engellemek, eklenen `<heading>` daha önce etiketi.

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

    Bu Başlatıcı kod neden `appInsights` eklenecek nesne bir özel özellik adında `Environment` her parçasına telemetri gönderir.
2. Ardından, bu özel özellik olarak ekleme bir [yuva ayarı](web-sites-staged-publishing.md#AboutConfiguration) azure'da web uygulamanız için. Bunu yapmak için Git Kabuk oturumunda aşağıdaki komutları çalıştırın.

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    Projenizdeki Web.config zaten tanımlar `environment` uygulama ayarı. Uygulamayı yerel olarak test ettiğinizde bu ayar, ölçümlerinizi ile Etiketlenecek `VS Debugger`. Değişikliklerinizi Azure'a gönderin, ancak Azure Bul kullanın ve `environment` web uygulamanızın yapılandırmasında bunun yerine ayarı uygulama ve ölçümlerinizi etiketli ile `Production`.
3. Yürütme ve kod değişikliklerinizi GitHub üzerinde sayfanızı çatala gönderin ve yeni uygulamayı (tarayıcıyı yenilemek için gereklidir) kullanmak, kullanıcılarınız için bekleyin. Application Insights'ta gösterilmesini yeni özellik için yaklaşık 15 dakika sürer `MultiChannelToDo.Web` kaynak.

        git add -A :/
        git commit -m "add environment property to AI events for client app"
        git push origin master
4. Şimdi, Git **özel olayları** dikey penceresini yeniden ve ölçümleri filtre `Environment=Production`. Şimdi bu filtre ile tüm yeni özel olayları üretim yuvasına görüyor olmalısınız.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. Tıklatın **Sık Kullanılanlar** gibi bir geçerli ölçüm Gezgini ayarları kaydetmek için düğmesini **özel olayları: üretim**. Kolayca bu görünümü ve bir dağıtım yuvası görünüm arasında daha sonra geçiş yapabilirsiniz.

   > [!TIP]
   > Daha güçlü analytics için göz önünde bulundurun [Application Insights kaynağınıza Power BI ile tümleştirme](../application-insights/app-insights-export-power-bi.md).
   >
   >

### <a name="add-slot-specific-tags-to-your-server-app-metrics"></a>Sunucu uygulaması ölçümlerinizi yuva özel etiketler ekleyin
Yeniden, bütünlük açısından sunucu tarafı uygulama ayarlama. JavaScript'te izlenmiş olan istemci uygulaması yuvası özgü etiketler sunucu uygulaması için izlenmiş .NET koduyla.

1. Açık  *&lt;repository_root >*\src\MultiChannelToDo\Global.asax.cs. Aşağıdaki kod bloğu yalnızca kapatmadan önce eklemek ad alanı kaşlı ayraç.

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
2. Ekleyerek ad çözümleme hataları düzeltin `using` aşağıda dosyasının deyimleri başına:

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. Aşağıdaki kodu ekleyin `Application_Start()` yöntemi:

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. Yürütme ve kod değişikliklerinizi GitHub üzerinde sayfanızı çatala gönderin ve yeni uygulamayı (tarayıcıyı yenilemek için gereklidir) kullanmak, kullanıcılarınız için bekleyin. Application Insights'ta gösterilmesini yeni özellik için yaklaşık 15 dakika sürer `MultiChannelToDo` kaynak.

        git add -A :/
        git commit -m "add environment property to AI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a>Güncelleştirmesi: Beta dal ayarlama
1. Açık  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json ve bulma `appsettings` kaynakları (arama `"name": "appsettings"`). Biri, her yuva için bir tane 4 vardır.
2. Her `appsettings` kaynak eklemek bir `"environment": "[parameters('slotName')]"` uygulama ayarı sonuna `properties` dizi. Virgül ile önceki satırın sonuna unutmayın.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    Eklemiş olduğunuz `environment` şablondaki tüm yuvalarına uygulama ayarı.
3. Aynı dosyada Bul `slotconfignames` kaynakları (arama `"name": "slotconfignames"`). Her uygulama için bir tane bunların, 2 vardır.
4. Her `slotconfignames` kaynak eklemek `"environment"` sonuna `appSettingNames` dizi. Virgül ile önceki satırın sonuna unutmayın.

    Yapmış olduğunuz `environment` uygulama çubuğu hem uygulamalar için kendi ilgili dağıtım yuvası için ayarlama.  
5. Git Kabuk oturumunuzda önce kullandığınız aynı kaynak grubu soneki aşağıdaki komutları çalıştırın.

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. İstendiğinde, aynı SQL veritabanı kimlik bilgileri olarak önce belirtin. Sonra kaynak grubunu güncelleştirmek için sorulduğunda yazın `Y`, ardından `ENTER`.

    Komut dosyası tamamlandıktan, özgün kaynak grubundaki tüm kaynaklarınızı korunur, ancak yeni bir yuva "beta" adlı bir kez içinde ' den itibaren oluşturuldu "Hazırlama" yuvası aynı yapılandırmaya sahip oluşturulur.

   > [!NOTE]
   > Bu yöntem farklı dağıtım ortamları oluşturma yönteminden farklıdır [Azure App Service ile Çevik Yazılım Geliştirme](app-service-agile-software-development.md). Burada, beklenmediğini dağıtım ortamları kaynak gruplarıyla oluşturduğunuz dağıtım yuvası ile dağıtım ortamlar oluşturun. Dağıtım ortamları kaynak grupları ile yönetme, üretim ortamı için geliştiricilere off-limits olmanızı sağlar, ancak yuvası ile kolayca yapabilirsiniz üretim testi yapmak kolay değildir.
   >
   >

İsterseniz, ayrıca bir alfa uygulamayı çalıştırarak oluşturabilirsiniz

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

Bu öğretici için yalnızca beta uygulamanızı kullanmaya devam eder.

## <a name="update-push-your-updates-to-the-beta-app"></a>Güncelleştirme: güncelleştirmelerinizi beta uygulamasına anında iletme
İyileştirmek istediğiniz geri uygulamanıza.

1. Şimdi, beta dalında olduğunuzdan emin olun

        git checkout beta
2. İçinde  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, bulma `<li>` etiketi ve ekleme `style="cursor:pointer"` , aşağıda gösterildiği gibi özniteliği.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. yürütme ve azure'a gönderin.
4. Bu değişiklik şimdi beta yuvasında için http://todoapp giderek yansıtılır doğrulayın*&lt;your_suffix >*-beta.azurewebsites.net/. Değişiklik henüz görmüyorsanız, yeni javascript kodu almak için tarayıcınızı yenileyin.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

Beta yuvasında çalıştıran değişikliğinizin sahip olduğunuza göre flighting dağıtım gerçekleştirmek hazır olursunuz.

## <a name="validate-route-traffic-to-the-beta-app"></a>Doğrulama: Beta uygulamasına yolu trafiğini
Bu bölümde, beta uygulamaya trafiğini yönlendirir. For sake of daha anlaşılır olması, tanıtım kullanıcı trafiğinin önemli bir kısmını yönlendirmekte paylaşacağız. Gerçekte, yönlendirmek istediğiniz trafik miktarı belirli durumunuza bağlıdır. Sitenizi microsoft.com ölçekte ise, örneğin, daha sonra toplam trafiğin yüzde biri'den az yararlı veri sağlamak için gerekebilir.

1. Git Kabuk oturumunuzda, beta yuvaya yarısı üretim trafiği yönlendirmek için aşağıdaki komutları çalıştırın:

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   `ReroutePercentage=50` Özelliği, üretim trafiği % 50'si beta uygulamanızın URL'sine yönlendirilir belirtir (tarafından belirtilen `ActionHostName` özelliği).
2. Şimdi http://ToDoApp için gidin*&lt;your_suffix >*. azurewebsites.net. % 50'trafiğin şimdi beta yuvaya yönlendirilmeniz gerekir.
3. Application Insights kaynağınıza ölçümleri ortamı tarafından filtre "beta" =.

   > [!NOTE]
   > Bu filtre uygulanmış bir görünüm başka bir sık kullanılan olarak kaydederseniz ölçüm Gezgini Görünüm üretim ve beta görünümler arasında kolayca çevirebilirsiniz.
   >
   >

Application Insights'ta, aşağıdakine benzer bir şey görürsünüz varsayın:

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

Yalnızca bu olduğunu üzerinde çok daha fazla tıklama gösteriyor `<li>` etiketleri olduğu anlaşılıyor ancak üzerinde ani artışı işleme tıklama olmasını `<li>` etiketler. Ardından kişiler yeni bulunmuş tamamlanabilmesi `<li>` etiketleri tıklanabilir ve tüm daha önce tamamlandı görevlerini uygulamasında artık temizleme.

Flighting dağıtımınızı verilerini temel alarak yeni UI üretime hazır olduğuna karar verin.

## <a name="go-live-move-your-new-code-into-production"></a>Canlı gidin: yeni kodunuzu üretim ortamına taşıyın
Artık güncelleştirmenizi üretime taşımak hazırsınız. Artık güncelleştirmenizi zaten doğrulandı biliyorsunuz harika nedir olan *önce* üretime gönderilir. Artık bunu güvenle dağıtabilir. AngularJS istemci uygulamaları için bir güncelleştirme yapılan olduğundan, yalnızca istemci tarafında kodu doğrulandı. Arka uç Web API uygulamasına değişiklik yapmak için olsaydı, değişikliklerinizi benzer şekilde ve kolayca doğrulamak.

1. Git Kabuğu'nda, aşağıdaki komutu çalıştırarak trafik yönlendirme kuralı kaldırın:

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. Git komutları çalıştırın:

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. Hazırlama yuvasını dağıtılacak yeni kodu için bir kaç dakika bekleyin, sonra http://ToDoApp başlatma*&lt;your_suffix >*-staging.azurewebsites.net yeni güncelleştirme hazırlama yuvası warmed olduğunu doğrulayın. Unutmayın, uygulamanızın hazırlama yuvasını çatalı ait ana dala bağlı.
4. Şimdi, üretime hazırlama yuvası takas

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a>Özet
Azure uygulama hizmeti bir şey üretimde müşterilerle uygulamalarını test etmek küçük - için orta ölçekli işletmeler için geleneksel olarak yapılan büyük kuruluşlarda kolaylaştırır. Neyse ki bu öğretici, App Service ve Application Insights olası flighting dağıtım ve hatta diğer test üretimde senaryoları DevOps dünyada yapmak için bir araya getirme gerek bilgi verdiği.

## <a name="more-resources"></a>Diğer kaynaklar
* [Azure App Service ile Çevik Yazılım Geliştirme](app-service-agile-software-development.md)
* [Hazırlık ortamları için Azure App Service'te web uygulamalarını ayarlama](web-sites-staged-publishing.md)
* [Azure'nın beklendiği karmaşık bir uygulama dağıtma](app-service-deploy-complex-application-predictably.md)
* [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - JSON Doğrulayıcı](http://jsonlint.com/)
* [Git dallanma – temel dallandırma ve birleştirme](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Azure PowerShell](/powershell/azure/overview)
* [Proje Kudu Wiki](https://github.com/projectkudu/kudu/wiki)
