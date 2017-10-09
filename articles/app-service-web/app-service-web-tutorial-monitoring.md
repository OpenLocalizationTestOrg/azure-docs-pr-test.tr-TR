---
title: "aaaMonitor bir Web uygulaması | Microsoft Docs"
description: "Bilgi nasıl tooset Web uygulamanızdan izleme ayarlama"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="87bd5-103">Uygulama Hizmeti izleme</span><span class="sxs-lookup"><span data-stu-id="87bd5-103">Monitor App Service</span></span>
<span data-ttu-id="87bd5-104">Bu öğreticide, uygulamanızı izleme ve bunlar ortaya çıktığında hello yerleşik platformu araçları toosolve sorunları kullanarak aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="87bd5-104">This tutorial walks you through monitoring your app and using hello built-in platform tools toosolve problems when they occur.</span></span>

<span data-ttu-id="87bd5-105">Bu belge her bir bölümünü belirli bir özelliği gider.</span><span class="sxs-lookup"><span data-stu-id="87bd5-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="87bd5-106">Merhaba özellikleri birlikte kullanarak şunları yapmanızı sağlar:</span><span class="sxs-lookup"><span data-stu-id="87bd5-106">Using hello features together let you:</span></span>
- <span data-ttu-id="87bd5-107">Uygulamanızı bir sorunu tanımlama.</span><span class="sxs-lookup"><span data-stu-id="87bd5-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="87bd5-108">Merhaba sorun kodu veya hello platformunuz tarafından ne zaman kaynaklanır belirleme.</span><span class="sxs-lookup"><span data-stu-id="87bd5-108">Determining when hello issue is caused by your code or hello platform.</span></span>
- <span data-ttu-id="87bd5-109">Merhaba kaynak kodunuzda hello sorununun daraltın.</span><span class="sxs-lookup"><span data-stu-id="87bd5-109">Narrow down hello source of hello problem in your code.</span></span>
- <span data-ttu-id="87bd5-110">Hata ayıklama ve hello sorunu düzeltme.</span><span class="sxs-lookup"><span data-stu-id="87bd5-110">Debugging and fixing hello issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="87bd5-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="87bd5-111">Before you begin</span></span>
- <span data-ttu-id="87bd5-112">Bir Web uygulaması toomonitor gerekir ve hello izleyin özetlenen adımları.</span><span class="sxs-lookup"><span data-stu-id="87bd5-112">You need a Web App toomonitor and follow hello outlined steps.</span></span>
    - <span data-ttu-id="87bd5-113">Hello açıklanan başlangıç adımları izleyerek bir uygulama oluşturabilir [Azure SQL veritabanı ile bir ASP.NET uygulaması oluşturma](app-service-web-tutorial-dotnet-sqldatabase.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="87bd5-113">You can create an application following hello steps described in hello [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="87bd5-114">Tootry istiyorsanız verilen **uzaktan hata ayıklama** uygulamanızın veya Visual Studio gerekir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-114">If you want tootry out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="87bd5-115">Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve hello ücretsiz kullanmak [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="87bd5-115">If you don’t already have Visual Studio 2017 installed, you can download and use hello free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="87bd5-116">Etkinleştirdiğinizden emin olun **Azure geliştirme** hello Visual Studio Kurulumu sırasında.</span><span class="sxs-lookup"><span data-stu-id="87bd5-116">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

## <span data-ttu-id="87bd5-117"><a name="metrics"></a>1. adım - metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="87bd5-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="87bd5-118">**Ölçümleri** yararlı toounderstand şunlardır:</span><span class="sxs-lookup"><span data-stu-id="87bd5-118">**Metrics** are useful toounderstand:</span></span>
- <span data-ttu-id="87bd5-119">Uygulama durumu</span><span class="sxs-lookup"><span data-stu-id="87bd5-119">Application health</span></span>
- <span data-ttu-id="87bd5-120">Uygulama performansı</span><span class="sxs-lookup"><span data-stu-id="87bd5-120">App performance</span></span>
- <span data-ttu-id="87bd5-121">Kaynak tüketimi</span><span class="sxs-lookup"><span data-stu-id="87bd5-121">Resource consumption</span></span>

<span data-ttu-id="87bd5-122">Bir uygulama sorunu araştırmaya ölçümleri gözden geçirmek iyi toostart olur.</span><span class="sxs-lookup"><span data-stu-id="87bd5-122">When investigating an application issue, reviewing metrics is a good place toostart.</span></span> <span data-ttu-id="87bd5-123">Azure portal sahiptir, uygulama kullanımının hello ölçümleri incelemek hızlı şekilde toovisually **Azure İzleyici**.</span><span class="sxs-lookup"><span data-stu-id="87bd5-123">Azure portal has a quick way toovisually inspect hello metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="87bd5-124">Ölçümleri, uygulamanız için birkaç anahtar toplamalar arasında bir geçmiş görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="87bd5-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="87bd5-125">App service içinde barındırılan herhangi bir uygulama için başlangıç Web uygulaması ve hello uygulama hizmeti planı izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-125">For any app hosted in app service, you should monitor both hello Web App and hello App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="87bd5-126">Bir uygulama hizmeti planı, uygulamalarınızı kullanılan fiziksel kaynakları toohost hello koleksiyonunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="87bd5-126">An App Service plan represents hello collection of physical resources used toohost your apps.</span></span> <span data-ttu-id="87bd5-127">Tüm uygulamaları tooan tanımladığı birden fazla uygulama barındırdığında toosave maliyet izin vererek uygulama hizmeti planı paylaşımı hello kaynaklara atanan.</span><span class="sxs-lookup"><span data-stu-id="87bd5-127">All applications assigned tooan App Service plan share hello resources defined by it allowing you toosave cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="87bd5-128">App Service planları şunları tanımlar:</span><span class="sxs-lookup"><span data-stu-id="87bd5-128">App Service plans define:</span></span>
> * <span data-ttu-id="87bd5-129">Bölge: Kuzey Avrupa, Doğu ABD, Güneydoğu Asya, vb.</span><span class="sxs-lookup"><span data-stu-id="87bd5-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="87bd5-130">Örnek boyutu: Küçük, Orta, büyük, vb.</span><span class="sxs-lookup"><span data-stu-id="87bd5-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="87bd5-131">Ölçek sayısı: bir, iki veya üç örnekleri, vb.</span><span class="sxs-lookup"><span data-stu-id="87bd5-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="87bd5-132">SKU: Ücretsiz, paylaşılan, temel, standart, Premium, vs.</span><span class="sxs-lookup"><span data-stu-id="87bd5-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="87bd5-133">Web uygulamanızın Git toohello tooreview ölçümleri **genel bakış** dikey penceresinde hello uygulamasının toomonitor istiyor.</span><span class="sxs-lookup"><span data-stu-id="87bd5-133">tooreview metrics for your Web App, go toohello **Overview** blade of hello app you want toomonitor.</span></span> <span data-ttu-id="87bd5-134">Buradan, uygulamanızın ölçümleri için bir grafik görüntüleyebilirsiniz bir **izleme kutucuğu**.</span><span class="sxs-lookup"><span data-stu-id="87bd5-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="87bd5-135">Merhaba döşeme tooedit'ı tıklatın, hangi ölçümleri tooview yapılandırmak ve zaman aralığı toodisplay hello.</span><span class="sxs-lookup"><span data-stu-id="87bd5-135">Click hello tile tooedit and configure what metrics tooview and hello time range toodisplay.</span></span>

<span data-ttu-id="87bd5-136">Varsayılan hello kaynak dikey tarafından hello uygulama istekleri için bir görünüm ve hataları hello son saat için sağlar.</span><span class="sxs-lookup"><span data-stu-id="87bd5-136">By default hello resource blade provides a view for hello Application Requests and errors for hello last hour.</span></span>
<span data-ttu-id="87bd5-137">![İzleyici uygulama](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="87bd5-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="87bd5-138">Merhaba örnekte de görüldüğü gibi birçok oluşturma uygulamanın sahibiz **HTTP sunucu hataları**.</span><span class="sxs-lookup"><span data-stu-id="87bd5-138">As you can see in hello example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="87bd5-139">Merhaba hacmi yüksek hatalar, bu uygulama tooinvestigate ihtiyacımız hello ilk göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-139">hello high volume of errors is hello first indication we need tooinvestigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="87bd5-140">Azure İzleyici hakkında daha fazla ile Merhaba bağlantılar aşağıdaki bilgi:</span><span class="sxs-lookup"><span data-stu-id="87bd5-140">Learn more about Azure Monitor with hello following links:</span></span>
> - [<span data-ttu-id="87bd5-141">Azure İzleyicisi ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="87bd5-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="87bd5-142">Azure ölçümleri</span><span class="sxs-lookup"><span data-stu-id="87bd5-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="87bd5-143">Azure İzleyicisi ile desteklenen ölçümleri</span><span class="sxs-lookup"><span data-stu-id="87bd5-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="87bd5-144">Azure panoları</span><span class="sxs-lookup"><span data-stu-id="87bd5-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="87bd5-145"><a name="alerts"></a>2. adım - uyarılarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="87bd5-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="87bd5-146">**Uyarıları** uygulamanız için belirli koşullar üzerinde yapılandırılmış tootrigger olabilir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-146">**Alerts** can be configured tootrigger on specific conditions for your app.</span></span>

<span data-ttu-id="87bd5-147">İçinde [adım 1 - görünüm ölçümleri](#metrics), Merhaba uygulaması çok sayıda hataları vardı gördük.</span><span class="sxs-lookup"><span data-stu-id="87bd5-147">In [Step 1 - View metrics](#metrics), we saw that hello application had a high number of errors.</span></span>

<span data-ttu-id="87bd5-148">Bir uyarı yapılandırmak sağlar tooautomatically hatası meydana geldiğinde bildirim.</span><span class="sxs-lookup"><span data-stu-id="87bd5-148">Lets configure an alert tooautomatically get notified when errors occur.</span></span> <span data-ttu-id="87bd5-149">Bu durumda, biz hello uyarı toosend istediğiniz ve belirli bir eşiğin üstünde hello HTTP 50 X hatalarının sayısı gider her zaman e-posta.</span><span class="sxs-lookup"><span data-stu-id="87bd5-149">In this case, we want hello alert toosend and e-mail every time hello number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="87bd5-150">bir uyarı, toocreate gidin çok**izleme** > **uyarıları** tıklatıp **[+] uyarı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="87bd5-150">toocreate an alert, navigate too**Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Uyarılar](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="87bd5-152">Değerleri hello uyarı yapılandırması sağlar:</span><span class="sxs-lookup"><span data-stu-id="87bd5-152">Provide values for hello Alert configuration:</span></span>
- <span data-ttu-id="87bd5-153">**Kaynak:** site toomonitor hello uyarı ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="87bd5-153">**Resource:** hello site toomonitor with hello alert.</span></span>
- <span data-ttu-id="87bd5-154">**Ad:** bu durumda, uyarı için bir ad: *yüksek HTTP 50 X*.</span><span class="sxs-lookup"><span data-stu-id="87bd5-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="87bd5-155">**Açıklama:** bu uyarı en arıyor düz metin açıklaması.</span><span class="sxs-lookup"><span data-stu-id="87bd5-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="87bd5-156">**Uyarı:** ölçümleri veya olayları uyarıları görünür, bu örnek için ölçümlere arıyoruz.</span><span class="sxs-lookup"><span data-stu-id="87bd5-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="87bd5-157">**Ölçüm:** bu durumda hangi ölçüm toomonitor: *HTTP sunucu hataları*.</span><span class="sxs-lookup"><span data-stu-id="87bd5-157">**Metric:** What metric toomonitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="87bd5-158">**Koşul:** tooalert, bu durumda seçtiğinizde hello *büyük* seçeneği.</span><span class="sxs-lookup"><span data-stu-id="87bd5-158">**Condition:** When tooalert, in this case select hello *greater than* option.</span></span>
- <span data-ttu-id="87bd5-159">**Eşiği:** değeri toolook için bu durumda nedir: *400*.</span><span class="sxs-lookup"><span data-stu-id="87bd5-159">**Threshold:** What is value toolook for, in this case: *400*.</span></span>
- <span data-ttu-id="87bd5-160">**Süresi:** uyarıları hello ortalama ölçüm değeri çalışır.</span><span class="sxs-lookup"><span data-stu-id="87bd5-160">**Period:** Alerts operate over hello average value of a metric.</span></span> <span data-ttu-id="87bd5-161">Daha küçük süreler daha hassas uyarılar verecek.</span><span class="sxs-lookup"><span data-stu-id="87bd5-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="87bd5-162">Bu durumda biz Baktığınız *5 dakika*.</span><span class="sxs-lookup"><span data-stu-id="87bd5-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="87bd5-163">**E-posta sahipleri ve katkıda bulunanlar:** bu durumda: *etkin*.</span><span class="sxs-lookup"><span data-stu-id="87bd5-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="87bd5-164">Merhaba uyarı bir e-posta oluşturulması tamamlandığına göre hello uygulama gider hello yapılandırılan eşiğin üstünde her zaman gönderilir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-164">Now that hello alert is created an email is sent every time hello app goes over hello configured threshold.</span></span> <span data-ttu-id="87bd5-165">Etkin uyarılar hello Azure portal gözden geçirilmesi.</span><span class="sxs-lookup"><span data-stu-id="87bd5-165">Active alerts can also be reviewed in hello Azure portal.</span></span>

![Tetiklenen uyarıları](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="87bd5-167">Azure Uyarıları hakkında daha fazla ile Merhaba bağlantılar aşağıdaki bilgi:</span><span class="sxs-lookup"><span data-stu-id="87bd5-167">Learn more about Azure Alerts with hello following links:</span></span>
> - [<span data-ttu-id="87bd5-168">Microsoft Azure içindeki uyarıları nedir</span><span class="sxs-lookup"><span data-stu-id="87bd5-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="87bd5-169">Ölçümleri eylem</span><span class="sxs-lookup"><span data-stu-id="87bd5-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="87bd5-170">Ölçüm uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="87bd5-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="87bd5-171"><a name="companion"></a>3. adım - uygulama hizmeti Yardımcısı</span><span class="sxs-lookup"><span data-stu-id="87bd5-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="87bd5-172">**Uygulama hizmeti Yardımcısı** uygun şekilde toomonitor uygulamanız mobil Cihazınızı (iOS veya Android) yerel bir deneyim sunar.</span><span class="sxs-lookup"><span data-stu-id="87bd5-172">**App Service companion** offers a convenient way toomonitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="87bd5-173">Uygulama hizmeti Yardımcısı'nı kullanın:</span><span class="sxs-lookup"><span data-stu-id="87bd5-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="87bd5-174">Uygulama ölçümleri gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="87bd5-174">Review application metrics</span></span>
- <span data-ttu-id="87bd5-175">Gözden geçirme ve act uygulama uyarıları ve öneriler</span><span class="sxs-lookup"><span data-stu-id="87bd5-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="87bd5-176">Temel sorun giderme (Gözat, Başlat, Durdur, yeniden başlatma hello uygulama) gerçekleştirir</span><span class="sxs-lookup"><span data-stu-id="87bd5-176">Perform basic troubleshooting (browse, start, stop, restart hello app)</span></span>
- <span data-ttu-id="87bd5-177">Kritik olaylar için anında iletme bildirimleri alın.</span><span class="sxs-lookup"><span data-stu-id="87bd5-177">Get push notifications for critical events.</span></span>

![Uygulama hizmeti Yardımcısı](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="87bd5-179">[![Uygulama hizmeti yardımcı uygulama mağazası](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![uygulama hizmeti Yahoo! Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="87bd5-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="87bd5-180">Uygulama hizmeti Yardımcısı hello yükleyebilirsiniz [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) veya [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="87bd5-180">You can install App Service companion from hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="87bd5-181"><a name="diagnose"></a>4. adım - tanılamak ve sorunları çözme</span><span class="sxs-lookup"><span data-stu-id="87bd5-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="87bd5-182">**Sorunları tanılamak ve** form platform sorunları uygulama sorunlarını ayrı yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="87bd5-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="87bd5-183">Web uygulaması geri toohealthy olası risk azaltmalarını tooget de önerebilir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-183">It can also suggest possible mitigations tooget your Web App back toohealthy.</span></span>

![Tanılama ve sorunları](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="87bd5-185">Merhaba örnek form önceki adımlara devam etmeden, biz Merhaba uygulaması sorunları tanımlanmasından sahip olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87bd5-185">Continuing with hello example form previous steps, we can see that hello application has been having availably issues.</span></span> <span data-ttu-id="87bd5-186">Buna karşılık, hello platform kullanılabilirlik % 100'den taşındı değil.</span><span class="sxs-lookup"><span data-stu-id="87bd5-186">In contrast, hello platform availability has not moved from 100%.</span></span>

<span data-ttu-id="87bd5-187">Ne zaman hello uygulama sorunu yaşıyor ve hello platform kalır yukarı biz ile uygulama sorununu giderme NET bir belirti olur.</span><span class="sxs-lookup"><span data-stu-id="87bd5-187">When hello app is having issue and hello platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="87bd5-188"><a name="logging"></a>Adım 5 - günlük kaydı</span><span class="sxs-lookup"><span data-stu-id="87bd5-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="87bd5-189">Biz hello hataları tooan uygulama sorunu belirlemelerine daraltıldığı, hello uygulama ve sunucu günlüklerini tooget daha fazla bilgi bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87bd5-189">Now that we have narrowed down hello failures tooan application issue, we can look at hello application and server logs tooget more information.</span></span>

<span data-ttu-id="87bd5-190">Günlük toocollect hem verir **uygulama tanılama** ve **Web sunucusu tanılama** Web uygulamanız için günlükleri.</span><span class="sxs-lookup"><span data-stu-id="87bd5-190">Logging allows you toocollect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="87bd5-191">Uygulama tanılama</span><span class="sxs-lookup"><span data-stu-id="87bd5-191">Application Diagnostics</span></span>
<span data-ttu-id="87bd5-192">Uygulama tanılama zamanında hello uygulama tarafından üretilen, toocapture izlemeleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="87bd5-192">Application diagnostics allows you toocapture traces produced by hello application at runtime.</span></span>

<span data-ttu-id="87bd5-193">İzleme tooyour ekleme uygulama büyük ölçüde özelliği toodebug ve sabitleme noktası sorunları artırır.</span><span class="sxs-lookup"><span data-stu-id="87bd5-193">Adding tracing tooyour application greatly improves your ability toodebug and pin-point issues.</span></span>

<span data-ttu-id="87bd5-194">ASP.NET, uygulama izlemelerini kullanarak oturum açabilir [System.Diagnostics.Trace sınıfı](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) hello günlük altyapısı tarafından yakalanan toogenerate olaylar.</span><span class="sxs-lookup"><span data-stu-id="87bd5-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate events that are captured by hello log infrastructure.</span></span> <span data-ttu-id="87bd5-195">Daha kolay filtreleme hello izleme hello önemini de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87bd5-195">You can also specify hello severity of hello trace for easier filtering.</span></span>

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
<span data-ttu-id="87bd5-196">tooenable uygulama günlüğü Git çok**izleme** > **tanılama günlüklerini** ve uygulama hello değiştirme düğmelerini kullanarak günlük kaydını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="87bd5-196">tooenable Application logging Go too**Monitoring** > **Diagnostic Logs** and Enable Application Logging using hello toggles.</span></span>

![İzleyici uygulama](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="87bd5-198">Uygulama günlüklerini saklı tooyour Web uygulamanızın dosya sistemi olabilir veya tooblob depolama gönderilir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-198">Application logs can be stored tooyour Web App's file system or pushed out tooblob storage.</span></span> <span data-ttu-id="87bd5-199">Üretim senaryoları için önerilen toouse blob depolama birimi değil.</span><span class="sxs-lookup"><span data-stu-id="87bd5-199">For production scenarios, it's recommended toouse blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="87bd5-200">Günlüğü etkinleştirme uygulama performans ve kaynak kullanımı üzerinde bir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="87bd5-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="87bd5-201">Üretim senaryoları için hata günlüklerini önerilir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="87bd5-202">Yalnızca sorunları araştırırken daha ayrıntılı günlük kaydını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="87bd5-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="87bd5-203">Web sunucu tanıları</span><span class="sxs-lookup"><span data-stu-id="87bd5-203">Web Server Diagnostics</span></span>
<span data-ttu-id="87bd5-204">Uygulamanızı değil izlenmiş olsa bile web sunucu günlükleri üretilir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="87bd5-205">Uygulama hizmeti sunucusu günlüklerini üç farklı türde toplayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="87bd5-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="87bd5-206">**Web sunucusu günlüğü**</span><span class="sxs-lookup"><span data-stu-id="87bd5-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="87bd5-207">Hello kullanarak HTTP işlemler hakkında bilgi [W3C Genişletilmiş günlük dosyası biçimi](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="87bd5-207">Information about HTTP transactions using hello [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="87bd5-208">İşlenen istek hello sayısı veya belirli bir IP adresinden kaç isteklerdir gibi genel site ölçümleri belirlerken yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="87bd5-208">Useful when determining overall site metrics such as hello number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="87bd5-209">**Ayrıntılı hata günlüğü**</span><span class="sxs-lookup"><span data-stu-id="87bd5-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="87bd5-210">(Durum kodu 400 veya daha büyük) hatası olduğunu gösteren HTTP durum kodları için ayrıntılı hata bilgileri.</span><span class="sxs-lookup"><span data-stu-id="87bd5-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="87bd5-211">Ayrıntılı hata günlüğü hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="87bd5-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="87bd5-212">**Başarısız istek izleme**</span><span class="sxs-lookup"><span data-stu-id="87bd5-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="87bd5-213">Merhaba IIS bileşenlerini izleme de dahil olmak üzere, başarısız istekler hakkında ayrıntılı bilgi, her bileşenin geçen tooprocess hello istek ve hello süre kullanılır.</span><span class="sxs-lookup"><span data-stu-id="87bd5-213">Detailed information on failed requests, including a trace of hello IIS components used tooprocess hello request and hello time taken in each component.</span></span>
    - <span data-ttu-id="87bd5-214">Başarısız istek günlükleri tooisolate belirli bir HTTP hata neden olan çalışırken yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="87bd5-214">Failed request logs are useful when trying tooisolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="87bd5-215">Başarısız istek izleme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="87bd5-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="87bd5-216">tooenable Server günlüğü:</span><span class="sxs-lookup"><span data-stu-id="87bd5-216">tooenable Server logging:</span></span>
- <span data-ttu-id="87bd5-217">çok Git**izleme** > **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="87bd5-217">go too**Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="87bd5-218">Web sunucusu tanılama hello değiştirme düğmelerini kullanarak farklı türlerde Hello etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="87bd5-218">Enable hello different types of Web Server Diagnostics using hello toggles.</span></span>

![İzleyici uygulama](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="87bd5-220">Günlüğü etkinleştirme uygulama performans ve kaynak kullanımı üzerinde bir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="87bd5-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="87bd5-221">Üretim senaryoları için hata günlüklerini önerilir, yalnızca etkinleştirmek sorunları incelemeye günlüğe kaydetme daha ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="87bd5-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="87bd5-222">Günlükleri erişme</span><span class="sxs-lookup"><span data-stu-id="87bd5-222">Accessing Logs</span></span>
<span data-ttu-id="87bd5-223">BLOB storage'da depolanan günlükleri, Azure Storage Gezgini kullanılarak erişilir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="87bd5-224">Merhaba Web uygulamanızın dosya sistemi içinde depolanan günlükleri yolları aşağıdaki hello altında FTP aracılığıyla erişilen:</span><span class="sxs-lookup"><span data-stu-id="87bd5-224">Logs stored in hello Web App's filesystem are accessed through FTP under hello following paths:</span></span>

- <span data-ttu-id="87bd5-225">**Uygulama günlüklerini** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="87bd5-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="87bd5-226">Bu klasör uygulama günlüğü tarafından üretilen bilgileri içeren bir veya daha fazla metin dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="87bd5-227">**Başarısız istek izlemelerin** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="87bd5-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="87bd5-228">Bu klasör bir XSL dosyası ve bir veya daha fazla XML dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="87bd5-229">**Ayrıntılı Hata günlüklerini** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="87bd5-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="87bd5-230">Bu klasör, uygulamanız tarafından oluşturulan HTTP hataları hakkında kapsamlı bilgi içeren bir veya daha fazla .htm dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="87bd5-231">**Web sunucu günlükleri** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="87bd5-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="87bd5-232">Bu klasör hello W3C Genişletilmiş günlük dosyası biçimi kullanılarak biçimlendirilmiş bir veya daha fazla metin dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-232">This folder contains one or more text files formatted using hello W3C extended log file format.</span></span>

## <span data-ttu-id="87bd5-233"><a name="streaming"></a>Adım 6 - akış günlük</span><span class="sxs-lookup"><span data-stu-id="87bd5-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="87bd5-234">Çok karşılaştırıldığında zaman kazandırır bu yana uygulama hata ayıklama sırasında akış günlükleri uygun[hello günlüklerine erişme](#Accessing-Logs) FTP aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="87bd5-234">Streaming logs are convenient when debugging an application since it saves time compared too[accessing hello logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="87bd5-235">Uygulama hizmeti akış **uygulama günlüklerini** ve **Web sunucu günlükleri** bunlar oluşturulduğunda.</span><span class="sxs-lookup"><span data-stu-id="87bd5-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="87bd5-236">Toostream günlükleri, denemeden önce hello açıklandığı gibi toplama günlükleri etkinleştirdiğinizden emin olun [günlüğü](#logging) bölümü.</span><span class="sxs-lookup"><span data-stu-id="87bd5-236">Before trying toostream logs, make sure you have enabled collecting logs as described in hello [Logging](#logging) section.</span></span>

<span data-ttu-id="87bd5-237">toostream günlükleri, Git çok**izleme**> **günlük akışı**.</span><span class="sxs-lookup"><span data-stu-id="87bd5-237">toostream logs, go too**Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="87bd5-238">Seçin **uygulama günlüklerini** veya **Web sunucu günlükleri** hangi bilgilere bağlı olarak, aradığınız.</span><span class="sxs-lookup"><span data-stu-id="87bd5-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="87bd5-239">Buradan, ayrıca Duraklat, yeniden başlatın ve hello arabellek temizleyin.</span><span class="sxs-lookup"><span data-stu-id="87bd5-239">From here, you can also pause, restart, and clear hello buffer.</span></span>

![Akış günlükleri](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="87bd5-241">Merhaba uygulamasını trafiği olduğunda günlükleri yalnızca oluşturulan, ayrıca daha fazla olayları veya bilgi günlükleri tooget hello ayrıntı düzeyini artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="87bd5-241">Logs are only generated when there is traffic on hello app, you can also increase hello verbosity of logs tooget more events or information.</span></span>

## <span data-ttu-id="87bd5-242"><a name="remote"></a>7. adım - uzaktan hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="87bd5-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="87bd5-243">Merhaba uygulamaları sorunları PIN işaret hello kaynağına sahip olduktan sonra kullanın **uzaktan hata ayıklama** hello kodlarda toowalk.</span><span class="sxs-lookup"><span data-stu-id="87bd5-243">Once you have pin-pointed hello source of hello applications problems, use **Remote Debugging** toowalk through hello code.</span></span>

<span data-ttu-id="87bd5-244">Uzaktan hata ayıklama sağlar, hata ayıklayıcı tooyour Web uygulaması ekleme hello bulutta çalışan.</span><span class="sxs-lookup"><span data-stu-id="87bd5-244">Remote debugging lets you attach a debugger tooyour Web App running in hello cloud.</span></span> <span data-ttu-id="87bd5-245">Kesme noktalarını ayarlayın, bellek doğrudan işlemek, kod üzerinden adım ve bile yerel olarak çalışan bir uygulama için gibi hello kod yolu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="87bd5-245">You can set breakpoints, manipulate memory directly, step through code, and even change hello code path just like you do for an app running locally.</span></span>

<span data-ttu-id="87bd5-246">Merhaba bulutta çalışan tooattach hello hata ayıklayıcı tooyour uygulama:</span><span class="sxs-lookup"><span data-stu-id="87bd5-246">tooattach hello debugger tooyour app running in hello cloud:</span></span>

- <span data-ttu-id="87bd5-247">Visual Studio 2017, hello uygulama için açık hello çözümü kullanarak toodebug istediğiniz</span><span class="sxs-lookup"><span data-stu-id="87bd5-247">Using Visual Studio 2017, open hello solution for hello app you want toodebug</span></span>
- <span data-ttu-id="87bd5-248">Yerel geliştirme için gibi bazı Fren noktaları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="87bd5-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="87bd5-249">Açık **cloud explorer** (CTRL + /, ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="87bd5-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="87bd5-250">Azure kimlik bilgilerinizle oturum açın, gerektiği gibi oturum açın.</span><span class="sxs-lookup"><span data-stu-id="87bd5-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="87bd5-251">Toodebug istediğiniz Bul hello uygulama</span><span class="sxs-lookup"><span data-stu-id="87bd5-251">Find hello app you want toodebug</span></span>
- <span data-ttu-id="87bd5-252">Seçin **Attach hata ayıklayıcı** form hello **Eylemler** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="87bd5-252">Select **Attach Debugger** form hello **Actions** pane.</span></span>

![Uzaktan hata ayıklama](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="87bd5-254">Visual Studio uzaktan hata ayıklama için uygulamanızı yapılandırır ve tooyour uygulama gider bir tarayıcı penceresi açar.</span><span class="sxs-lookup"><span data-stu-id="87bd5-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates tooyour app.</span></span> <span data-ttu-id="87bd5-255">Uygulama tootrigger kesme noktalarına göz ve aracılığıyla hello koda adım.</span><span class="sxs-lookup"><span data-stu-id="87bd5-255">Browse through your app tootrigger break points and step through hello code.</span></span>

> [!WARNING]
> <span data-ttu-id="87bd5-256">Hata ayıklama modunda üretimde çalışan önerilmez.</span><span class="sxs-lookup"><span data-stu-id="87bd5-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="87bd5-257">Üretim uygulamanız toomultiple sunucu örnekleri ölçeklenmez ise, yanıt veren tooother istekleri hello web sunucusundan engel hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="87bd5-257">If your production app is not scaled out toomultiple server instances, debugging prevent hello web server from responding tooother requests.</span></span> <span data-ttu-id="87bd5-258">Üretim ilgili sorunları gidermek için en iyi çok kaynaktır[günlüğe kaydetmeyi yapılandırmak](#logging) ve [Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="87bd5-258">For troubleshooting production problems, your best resource is too[configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="87bd5-259"><a name="explorer"></a>Adım 8 - işlem Gezgini'ni</span><span class="sxs-lookup"><span data-stu-id="87bd5-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="87bd5-260">Uygulamanız birden fazla, toomore çıkışı ölçeklendirilir zaman **işlem Gezgini'ni** örneği belirli sorunları belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-260">When your application is scaled out toomore than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="87bd5-261">Kullanım **işlem Gezgini'ni** için:</span><span class="sxs-lookup"><span data-stu-id="87bd5-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="87bd5-262">Tüm hello işlemleri farklı uygulama hizmeti planınızı örneklerinde sıralar.</span><span class="sxs-lookup"><span data-stu-id="87bd5-262">Enumerate all hello processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="87bd5-263">Detaya ve hello işleyicileri ve modülleri her işlemle ilişkili görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="87bd5-263">Drill down and view hello handles and modules associated with each process.</span></span>
- <span data-ttu-id="87bd5-264">Merhaba görünüm CPU, çalışma kümesine ve iş parçacığı sayısını işlem düzeyi toohelp kaçak işlemleri tanımlayın</span><span class="sxs-lookup"><span data-stu-id="87bd5-264">View CPU, Working Set, and Thread count at hello process level toohelp you identify runaway processes</span></span>
- <span data-ttu-id="87bd5-265">Açık dosya işlemesi bulun ve hatta belirli işlem örneği sonlandır.</span><span class="sxs-lookup"><span data-stu-id="87bd5-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="87bd5-266">İşlem Gezgini'ni altında bulunabilir **izleme** > **işlem Gezgini'ni**.</span><span class="sxs-lookup"><span data-stu-id="87bd5-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![İşlem Gezgini](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="87bd5-268"><a name="insights"></a>Adım 9 - Application Insights</span><span class="sxs-lookup"><span data-stu-id="87bd5-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="87bd5-269">**Application Insights** uygulamanız için uygulama profili oluşturma ve Gelişmiş izleme özelliklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="87bd5-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="87bd5-270">Özel durumlar ve Web uygulamanızda performans sorunlarını tanılamak ve Application Insights toodetect kullanın.</span><span class="sxs-lookup"><span data-stu-id="87bd5-270">Use Application Insights toodetect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="87bd5-271">Web uygulamanız için Application Insights etkinleştirebilirsiniz **izleme** > **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="87bd5-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="87bd5-272">Application Insights tooinstall hello Application Insights site uzantısı toostart veri toplamayı isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="87bd5-272">Application Insights might prompt you tooinstall hello Application Insights site extension toostart collecting data.</span></span> <span data-ttu-id="87bd5-273">Merhaba site uzantısı yükleme uygulama yeniden başlatma neden olur.</span><span class="sxs-lookup"><span data-stu-id="87bd5-273">Installing hello site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="87bd5-275">Application Insights sahip zengin bir özellik kümesi, toolearn daha izleyin hello içerdiği hello bağlantılar [sonraki adımlar](#next) bölümü.</span><span class="sxs-lookup"><span data-stu-id="87bd5-275">Application Insights has a rich feature set, toolearn more, follow hello links included in hello [Next Steps](#next) section.</span></span>

## <span data-ttu-id="87bd5-276"><a name="next"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="87bd5-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="87bd5-277">Application Insights nedir</span><span class="sxs-lookup"><span data-stu-id="87bd5-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="87bd5-278">Application Insights ile Azure web uygulaması performans izleme</span><span class="sxs-lookup"><span data-stu-id="87bd5-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="87bd5-279">İzleyici kullanılabilirliği ve yanıt hızını Application Insights ile herhangi bir web sitesi</span><span class="sxs-lookup"><span data-stu-id="87bd5-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
