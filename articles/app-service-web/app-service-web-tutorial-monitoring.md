---
title: "Bir Web uygulaması izleme | Microsoft Docs"
description: "Web uygulamanızdan izleme ayarlama öğrenin"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: 29df824062d00e01b786533033097948c008588f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-app-service"></a><span data-ttu-id="5845d-103">Uygulama Hizmeti izleme</span><span class="sxs-lookup"><span data-stu-id="5845d-103">Monitor App Service</span></span>
<span data-ttu-id="5845d-104">Bu öğreticide, uygulamanızı izleme ve ortaya çıkan sorunları çözmek için yerleşik platform araçlarını kullanarak aracılığıyla açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5845d-104">This tutorial walks you through monitoring your app and using the built-in platform tools to solve problems when they occur.</span></span>

<span data-ttu-id="5845d-105">Bu belge her bir bölümünü belirli bir özelliği gider.</span><span class="sxs-lookup"><span data-stu-id="5845d-105">Each section of this document goes over a specific feature.</span></span> <span data-ttu-id="5845d-106">Özellikleri birlikte kullanarak şunları yapmanızı sağlar:</span><span class="sxs-lookup"><span data-stu-id="5845d-106">Using the features together let you:</span></span>
- <span data-ttu-id="5845d-107">Uygulamanızı bir sorunu tanımlama.</span><span class="sxs-lookup"><span data-stu-id="5845d-107">Identifying an issue in your app.</span></span>
- <span data-ttu-id="5845d-108">Ne zaman sorun kodunuzu platform nedeni veya belirleniyor.</span><span class="sxs-lookup"><span data-stu-id="5845d-108">Determining when the issue is caused by your code or the platform.</span></span>
- <span data-ttu-id="5845d-109">Kodunuzda sorunun kaynağını daraltın.</span><span class="sxs-lookup"><span data-stu-id="5845d-109">Narrow down the source of the problem in your code.</span></span>
- <span data-ttu-id="5845d-110">Hata ayıklama ve sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="5845d-110">Debugging and fixing the issue.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5845d-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="5845d-111">Before you begin</span></span>
- <span data-ttu-id="5845d-112">Açıklanan adımları izleyin ve izlemek için bir Web uygulaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5845d-112">You need a Web App to monitor and follow the outlined steps.</span></span>
    - <span data-ttu-id="5845d-113">Açıklanan adımları izleyerek bir uygulama oluşturabilir [Azure SQL veritabanı ile bir ASP.NET uygulaması oluşturma](app-service-web-tutorial-dotnet-sqldatabase.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="5845d-113">You can create an application following the steps described in the [Create an ASP.NET app in Azure with SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md) tutorial.</span></span>

- <span data-ttu-id="5845d-114">Denemek istiyorsanız, **uzaktan hata ayıklama** uygulamanızın veya Visual Studio gerekir.</span><span class="sxs-lookup"><span data-stu-id="5845d-114">If you want to try out **Remote Debugging** of your application, you need Visual Studio.</span></span>
    - <span data-ttu-id="5845d-115">Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve ücretsiz kullanmak [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5845d-115">If you don’t already have Visual Studio 2017 installed, you can download and use the free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span>
    - <span data-ttu-id="5845d-116">Visual Studio kurulumu sırasında **Azure dağıtımını** etkinleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5845d-116">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

## <span data-ttu-id="5845d-117"><a name="metrics"></a>1. adım - metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="5845d-117"><a name="metrics"></a> Step 1 - View metrics</span></span>
<span data-ttu-id="5845d-118">**Ölçümleri** anlamak kullanışlıdır:</span><span class="sxs-lookup"><span data-stu-id="5845d-118">**Metrics** are useful to understand:</span></span>
- <span data-ttu-id="5845d-119">Uygulama durumu</span><span class="sxs-lookup"><span data-stu-id="5845d-119">Application health</span></span>
- <span data-ttu-id="5845d-120">Uygulama performansı</span><span class="sxs-lookup"><span data-stu-id="5845d-120">App performance</span></span>
- <span data-ttu-id="5845d-121">Kaynak tüketimi</span><span class="sxs-lookup"><span data-stu-id="5845d-121">Resource consumption</span></span>

<span data-ttu-id="5845d-122">Uygulama sorununu araştırırken ölçümleri gözden geçirme başlatmak için uygun bir yerdir.</span><span class="sxs-lookup"><span data-stu-id="5845d-122">When investigating an application issue, reviewing metrics is a good place to start.</span></span> <span data-ttu-id="5845d-123">Azure portal sahiptir, uygulama kullanımının ölçümleri görsel olarak incelemek için hızlı bir yolu **Azure İzleyici**.</span><span class="sxs-lookup"><span data-stu-id="5845d-123">Azure portal has a quick way to visually inspect the metrics of your app using **Azure Monitor**.</span></span>

<span data-ttu-id="5845d-124">Ölçümleri, uygulamanız için birkaç anahtar toplamalar arasında bir geçmiş görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="5845d-124">Metrics provide a historical view across several key aggregations for your app.</span></span> <span data-ttu-id="5845d-125">App service içinde barındırılan herhangi bir uygulama için Web App ve uygulama hizmeti planı izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5845d-125">For any app hosted in app service, you should monitor both the Web App and the App Service plan.</span></span>

> [!NOTE]
> <span data-ttu-id="5845d-126">App Service planı, uygulamalarınızı barındırmak için kullanılan fiziksel kaynakları içeren koleksiyonu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="5845d-126">An App Service plan represents the collection of physical resources used to host your apps.</span></span> <span data-ttu-id="5845d-127">Bir App Service planına atanan tüm uygulamalar plan tarafından tanımlanan kaynakları paylaşarak birden çok uygulamayı barındırırken maliyetten tasarruf etmenize imkan sağlar.</span><span class="sxs-lookup"><span data-stu-id="5845d-127">All applications assigned to an App Service plan share the resources defined by it allowing you to save cost when hosting multiple apps.</span></span>
>
> <span data-ttu-id="5845d-128">App Service planları şunları tanımlar:</span><span class="sxs-lookup"><span data-stu-id="5845d-128">App Service plans define:</span></span>
> * <span data-ttu-id="5845d-129">Bölge: Kuzey Avrupa, Doğu ABD, Güneydoğu Asya, vb.</span><span class="sxs-lookup"><span data-stu-id="5845d-129">Region: North Europe, East US, Southeast Asia, etc.</span></span>
> * <span data-ttu-id="5845d-130">Örnek boyutu: Küçük, Orta, büyük, vb.</span><span class="sxs-lookup"><span data-stu-id="5845d-130">Instance Size: Small, Medium, Large, etc.</span></span>
> * <span data-ttu-id="5845d-131">Ölçek sayısı: bir, iki veya üç örnekleri, vb.</span><span class="sxs-lookup"><span data-stu-id="5845d-131">Scale Count: one, two, or three instances, etc.</span></span>
> * <span data-ttu-id="5845d-132">SKU: Ücretsiz, paylaşılan, temel, standart, Premium, vs.</span><span class="sxs-lookup"><span data-stu-id="5845d-132">SKU: Free, Shared, Basic, Standard, Premium, etc.</span></span>

<span data-ttu-id="5845d-133">Web uygulamanız için ölçümleri gözden geçirmek için Git **genel bakış** izlemek istediğiniz uygulamayı dikey.</span><span class="sxs-lookup"><span data-stu-id="5845d-133">To review metrics for your Web App, go to the **Overview** blade of the app you want to monitor.</span></span> <span data-ttu-id="5845d-134">Buradan, uygulamanızın ölçümleri için bir grafik görüntüleyebilirsiniz bir **izleme kutucuğu**.</span><span class="sxs-lookup"><span data-stu-id="5845d-134">From here, you can view a chart for your app's metrics as a **Monitoring tile**.</span></span> <span data-ttu-id="5845d-135">Düzenle ve hangi ölçümleri görüntülemek ve görüntülemek için zaman aralığı için yapılandırmak için kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5845d-135">Click the tile to edit and configure what metrics to view and the time range to display.</span></span>

<span data-ttu-id="5845d-136">Varsayılan olarak kaynak dikey penceresini görüntüleme uygulama istekleri ve hataları için son saat için sağlar.</span><span class="sxs-lookup"><span data-stu-id="5845d-136">By default the resource blade provides a view for the Application Requests and errors for the last hour.</span></span>
<span data-ttu-id="5845d-137">![İzleyici uygulama](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span><span class="sxs-lookup"><span data-stu-id="5845d-137">![Monitor App](media/app-service-web-tutorial-monitoring/app-service-monitor.png)</span></span>

<span data-ttu-id="5845d-138">Örnekte de görüldüğü gibi birçok oluşturma uygulamanın sahibiz **HTTP sunucu hataları**.</span><span class="sxs-lookup"><span data-stu-id="5845d-138">As you can see in the example, we have an application that is generating many **HTTP Server Errors**.</span></span> <span data-ttu-id="5845d-139">Yüksek hacimli hataların bu uygulamayı araştırmak ihtiyacımız ilk göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="5845d-139">The high volume of errors is the first indication we need to investigate this application.</span></span>

> [!TIP]
> <span data-ttu-id="5845d-140">Azure İzleyici hakkında daha fazla ile aşağıdaki bağlantılardan öğrenin:</span><span class="sxs-lookup"><span data-stu-id="5845d-140">Learn more about Azure Monitor with the following links:</span></span>
> - [<span data-ttu-id="5845d-141">Azure İzleyicisi ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="5845d-141">Get started with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="5845d-142">Azure ölçümleri</span><span class="sxs-lookup"><span data-stu-id="5845d-142">Azure Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [<span data-ttu-id="5845d-143">Azure İzleyicisi ile desteklenen ölçümleri</span><span class="sxs-lookup"><span data-stu-id="5845d-143">Supported metrics with Azure Monitor</span></span>](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [<span data-ttu-id="5845d-144">Azure panoları</span><span class="sxs-lookup"><span data-stu-id="5845d-144">Azure Dashboards</span></span>](..\azure-portal\azure-portal-dashboards.md)

## <span data-ttu-id="5845d-145"><a name="alerts"></a>2. adım - uyarılarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5845d-145"><a name="alerts"></a> Step 2 - Configure Alerts</span></span>
<span data-ttu-id="5845d-146">**Uyarıları** yapılandırılabilir uygulamanız için belirli koşullar tetikleyici için.</span><span class="sxs-lookup"><span data-stu-id="5845d-146">**Alerts** can be configured to trigger on specific conditions for your app.</span></span>

<span data-ttu-id="5845d-147">İçinde [adım 1 - görünüm ölçümleri](#metrics), uygulamanın çok sayıda hataları vardı gördük.</span><span class="sxs-lookup"><span data-stu-id="5845d-147">In [Step 1 - View metrics](#metrics), we saw that the application had a high number of errors.</span></span>

<span data-ttu-id="5845d-148">Hata oluştuğunda otomatik olarak bildirim almak için bir uyarı yapılandırmak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5845d-148">Lets configure an alert to automatically get notified when errors occur.</span></span> <span data-ttu-id="5845d-149">Bu durumda, gönderme ve HTTP 50 X hatalarının sayısı belirli bir eşiğin üstünde gider her zaman e-posta uyarı istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="5845d-149">In this case, we want the alert to send and e-mail every time the number of HTTP 50X errors goes over a certain threshold.</span></span>

<span data-ttu-id="5845d-150">Bir uyarı oluşturmak için gidin **izleme** > **uyarıları** tıklatıp **[+] uyarı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5845d-150">To create an alert, navigate to **Monitoring** > **Alerts** and click **[+] Add Alert**.</span></span>

![Uyarılar](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

<span data-ttu-id="5845d-152">Uyarı yapılandırması için değerleri girin:</span><span class="sxs-lookup"><span data-stu-id="5845d-152">Provide values for the Alert configuration:</span></span>
- <span data-ttu-id="5845d-153">**Kaynak:** uyarıyla izlemek için site.</span><span class="sxs-lookup"><span data-stu-id="5845d-153">**Resource:** The site to monitor with the alert.</span></span>
- <span data-ttu-id="5845d-154">**Ad:** bu durumda, uyarı için bir ad: *yüksek HTTP 50 X*.</span><span class="sxs-lookup"><span data-stu-id="5845d-154">**Name:** A name for your alert, in this case: *High HTTP 50X*.</span></span>
- <span data-ttu-id="5845d-155">**Açıklama:** bu uyarı en arıyor düz metin açıklaması.</span><span class="sxs-lookup"><span data-stu-id="5845d-155">**Description:** Plain text explanation of what this alert is looking at.</span></span>
- <span data-ttu-id="5845d-156">**Uyarı:** ölçümleri veya olayları uyarıları görünür, bu örnek için ölçümlere arıyoruz.</span><span class="sxs-lookup"><span data-stu-id="5845d-156">**Alert on:** Alerts can look at Metrics or Events, for this example we are looking at metrics.</span></span>
- <span data-ttu-id="5845d-157">**Ölçüm:** bu durumda, izlemek için hangi ölçüm: *HTTP sunucu hataları*.</span><span class="sxs-lookup"><span data-stu-id="5845d-157">**Metric:** What metric to monitor, in this case: *HTTP Server Errors*.</span></span>
- <span data-ttu-id="5845d-158">**Koşul:** ne zaman uyarı, bu durumda select *büyük* seçeneği.</span><span class="sxs-lookup"><span data-stu-id="5845d-158">**Condition:** When to alert, in this case select the *greater than* option.</span></span>
- <span data-ttu-id="5845d-159">**Eşiği:** , bu durumda aramak için değer nedir: *400*.</span><span class="sxs-lookup"><span data-stu-id="5845d-159">**Threshold:** What is value to look for, in this case: *400*.</span></span>
- <span data-ttu-id="5845d-160">**Süresi:** uyarılar ölçüm ortalama değer üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="5845d-160">**Period:** Alerts operate over the average value of a metric.</span></span> <span data-ttu-id="5845d-161">Daha küçük süreler daha hassas uyarılar verecek.</span><span class="sxs-lookup"><span data-stu-id="5845d-161">Smaller periods of time yield more sensitive alerts.</span></span> <span data-ttu-id="5845d-162">Bu durumda biz Baktığınız *5 dakika*.</span><span class="sxs-lookup"><span data-stu-id="5845d-162">in this case we are looking at *5 Minutes*.</span></span>
- <span data-ttu-id="5845d-163">**E-posta sahipleri ve katkıda bulunanlar:** bu durumda: *etkin*.</span><span class="sxs-lookup"><span data-stu-id="5845d-163">**Email Owners and contributors:** in this case: *Enabled*.</span></span>

<span data-ttu-id="5845d-164">Uyarı oluşturduğunuza göre uygulama yapılandırılan eşiğin üstünde gider her zaman bir e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="5845d-164">Now that the alert is created an email is sent every time the app goes over the configured threshold.</span></span> <span data-ttu-id="5845d-165">Etkin uyarılar ayrıca Azure portalında incelenebilir.</span><span class="sxs-lookup"><span data-stu-id="5845d-165">Active alerts can also be reviewed in the Azure portal.</span></span>

![Tetiklenen uyarıları](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> <span data-ttu-id="5845d-167">Azure Uyarıları hakkında daha fazla ile aşağıdaki bağlantılardan öğrenin:</span><span class="sxs-lookup"><span data-stu-id="5845d-167">Learn more about Azure Alerts with the following links:</span></span>
> - [<span data-ttu-id="5845d-168">Microsoft Azure içindeki uyarıları nedir</span><span class="sxs-lookup"><span data-stu-id="5845d-168">What are alerts in Microsoft Azure</span></span>](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [<span data-ttu-id="5845d-169">Ölçümleri eylem</span><span class="sxs-lookup"><span data-stu-id="5845d-169">Take Action On Metrics</span></span>](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [<span data-ttu-id="5845d-170">Ölçüm uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5845d-170">Create metric alerts</span></span>](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <span data-ttu-id="5845d-171"><a name="companion"></a>3. adım - uygulama hizmeti Yardımcısı</span><span class="sxs-lookup"><span data-stu-id="5845d-171"><a name="companion"></a> Step 3 - App Service Companion</span></span>
<span data-ttu-id="5845d-172">**Uygulama hizmeti Yardımcısı** mobil Cihazınızı (iOS veya Android) yerel bir deneyim uygulamanızı izlemek için kullanışlı bir yol sunar.</span><span class="sxs-lookup"><span data-stu-id="5845d-172">**App Service companion** offers a convenient way to monitor your app with a native experience in your mobile device (iOS or Android).</span></span>

<span data-ttu-id="5845d-173">Uygulama hizmeti Yardımcısı'nı kullanın:</span><span class="sxs-lookup"><span data-stu-id="5845d-173">Use App Service Companion to:</span></span>
- <span data-ttu-id="5845d-174">Uygulama ölçümleri gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="5845d-174">Review application metrics</span></span>
- <span data-ttu-id="5845d-175">Gözden geçirme ve act uygulama uyarıları ve öneriler</span><span class="sxs-lookup"><span data-stu-id="5845d-175">Review and act on application alerts and recommendations</span></span>
- <span data-ttu-id="5845d-176">Temel sorun giderme gerçekleştirir (göz atın, başlatabilir, durdurabilir, uygulamayı yeniden başlatın)</span><span class="sxs-lookup"><span data-stu-id="5845d-176">Perform basic troubleshooting (browse, start, stop, restart the app)</span></span>
- <span data-ttu-id="5845d-177">Kritik olaylar için anında iletme bildirimleri alın.</span><span class="sxs-lookup"><span data-stu-id="5845d-177">Get push notifications for critical events.</span></span>

![Uygulama hizmeti Yardımcısı](media/app-service-web-tutorial-monitoring/app-service-companion.png)

<span data-ttu-id="5845d-179">[![Uygulama hizmeti yardımcı uygulama mağazası](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![uygulama hizmeti Yahoo! Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="5845d-179">[![App Service Companion App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![App Service Companion Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

<span data-ttu-id="5845d-180">Uygulama hizmeti kılavuz yükleyebilirsiniz [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) veya [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span><span class="sxs-lookup"><span data-stu-id="5845d-180">You can install App Service companion from the [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) or [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)</span></span>

## <span data-ttu-id="5845d-181"><a name="diagnose"></a>4. adım - tanılamak ve sorunları çözme</span><span class="sxs-lookup"><span data-stu-id="5845d-181"><a name="diagnose"></a> Step 4 - Diagnose and solve problems</span></span>
<span data-ttu-id="5845d-182">**Sorunları tanılamak ve** form platform sorunları uygulama sorunlarını ayrı yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="5845d-182">**Diagnose and solve problems** helps you separate application issues form platform issues.</span></span> <span data-ttu-id="5845d-183">Ayrıca, Web uygulamanıza geri sağlıklı almak için olası risk azaltmalarını de önerebilir.</span><span class="sxs-lookup"><span data-stu-id="5845d-183">It can also suggest possible mitigations to get your Web App back to healthy.</span></span>

![Tanılama ve sorunları](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

<span data-ttu-id="5845d-185">Örnek form önceki adımlara devam etmeden, uygulama konusunda tanımlanmasından sorun olduğunu görebiliriz.</span><span class="sxs-lookup"><span data-stu-id="5845d-185">Continuing with the example form previous steps, we can see that the application has been having availably issues.</span></span> <span data-ttu-id="5845d-186">Buna karşılık, platform kullanılabilirlik % 100'den taşındı değil.</span><span class="sxs-lookup"><span data-stu-id="5845d-186">In contrast, the platform availability has not moved from 100%.</span></span>

<span data-ttu-id="5845d-187">Uygulama sorun ve platform kalır yukarı içerdiğinde biz ile uygulama sorununu giderme NET bir belirti değil.</span><span class="sxs-lookup"><span data-stu-id="5845d-187">When the app is having issue and the platform stays up, it's a clear indication that we are dealing with an application issue.</span></span>

## <span data-ttu-id="5845d-188"><a name="logging"></a>Adım 5 - günlük kaydı</span><span class="sxs-lookup"><span data-stu-id="5845d-188"><a name="logging"></a> Step 5 - Logging</span></span>
<span data-ttu-id="5845d-189">Biz uygulama sorununu hatalarını aşağı daraltıldığı, size daha fazla bilgi almak için uygulama ve sunucu günlüklerini bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5845d-189">Now that we have narrowed down the failures to an application issue, we can look at the application and server logs to get more information.</span></span>

<span data-ttu-id="5845d-190">Günlük her ikisi de toplamanızı sağlar **uygulama tanılama** ve **Web sunucusu tanılama** Web uygulamanız için günlükleri.</span><span class="sxs-lookup"><span data-stu-id="5845d-190">Logging allows you to collect both **Application Diagnostics** and **Web Server Diagnostics** logs for your Web App.</span></span>

### <a name="application-diagnostics"></a><span data-ttu-id="5845d-191">Uygulama tanılama</span><span class="sxs-lookup"><span data-stu-id="5845d-191">Application Diagnostics</span></span>
<span data-ttu-id="5845d-192">Uygulama tanılama çalışma zamanında uygulama tarafından üretilen izlemeleri yakalamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5845d-192">Application diagnostics allows you to capture traces produced by the application at runtime.</span></span>

<span data-ttu-id="5845d-193">Uygulamanız için büyük ölçüde izleme ekleme hata ayıklama ve sabitleme noktası sorunları yeteneğinizi geliştirir.</span><span class="sxs-lookup"><span data-stu-id="5845d-193">Adding tracing to your application greatly improves your ability to debug and pin-point issues.</span></span>

<span data-ttu-id="5845d-194">ASP.NET, uygulama izlemelerini kullanarak oturum açabilir [System.Diagnostics.Trace sınıfı](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) günlük altyapısı tarafından yakalanan olaylar oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="5845d-194">In ASP.NET, you can log application traces using [System.Diagnostics.Trace class](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) to generate events that are captured by the log infrastructure.</span></span> <span data-ttu-id="5845d-195">Önem derecesi daha kolay filtreleme için izleme de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5845d-195">You can also specify the severity of the trace for easier filtering.</span></span>

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
<span data-ttu-id="5845d-196">Uygulama günlüğü etkinleştirmek için Git **izleme** > **tanılama günlüklerini** ve uygulama değiştirme düğmelerini kullanarak günlük kaydını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5845d-196">To enable Application logging Go to **Monitoring** > **Diagnostic Logs** and Enable Application Logging using the toggles.</span></span>

![İzleyici uygulama](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

<span data-ttu-id="5845d-198">Uygulama günlükleri, Web uygulamanızın dosya sistemine depolanan veya blob depolama için gönderilir.</span><span class="sxs-lookup"><span data-stu-id="5845d-198">Application logs can be stored to your Web App's file system or pushed out to blob storage.</span></span> <span data-ttu-id="5845d-199">Üretim senaryoları için blob storage kullanma önerilir.</span><span class="sxs-lookup"><span data-stu-id="5845d-199">For production scenarios, it's recommended to use blob storage.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5845d-200">Günlüğü etkinleştirme uygulama performans ve kaynak kullanımı üzerinde bir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="5845d-200">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="5845d-201">Üretim senaryoları için hata günlüklerini önerilir.</span><span class="sxs-lookup"><span data-stu-id="5845d-201">For production scenarios, error logs are recommended.</span></span> <span data-ttu-id="5845d-202">Yalnızca sorunları araştırırken daha ayrıntılı günlük kaydını etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5845d-202">Only enable more verbose logging when investigating issues.</span></span>

 ### <a name="web-server-diagnostics"></a><span data-ttu-id="5845d-203">Web sunucu tanıları</span><span class="sxs-lookup"><span data-stu-id="5845d-203">Web Server Diagnostics</span></span>
<span data-ttu-id="5845d-204">Uygulamanızı değil izlenmiş olsa bile web sunucu günlükleri üretilir.</span><span class="sxs-lookup"><span data-stu-id="5845d-204">Web Server logs are generated even if your app is not instrumented.</span></span> <span data-ttu-id="5845d-205">Uygulama hizmeti sunucusu günlüklerini üç farklı türde toplayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5845d-205">App Service can collect three different types of server logs:</span></span>

- <span data-ttu-id="5845d-206">**Web sunucusu günlüğü**</span><span class="sxs-lookup"><span data-stu-id="5845d-206">**Web Server Logging**</span></span>
    - <span data-ttu-id="5845d-207">HTTP işlemlerini kullanma hakkında bilgi [W3C Genişletilmiş günlük dosyası biçimi](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span><span class="sxs-lookup"><span data-stu-id="5845d-207">Information about HTTP transactions using the [W3C extended log file format](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).</span></span>
    - <span data-ttu-id="5845d-208">Belirli bir IP adresinden işlenen isteklerin ya da kaç istek sayısı gibi genel site ölçümleri belirlerken yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="5845d-208">Useful when determining overall site metrics such as the number of requests handled or how many requests are from a specific IP address.</span></span>
- <span data-ttu-id="5845d-209">**Ayrıntılı hata günlüğü**</span><span class="sxs-lookup"><span data-stu-id="5845d-209">**Detailed Error Logging**</span></span>
    - <span data-ttu-id="5845d-210">(Durum kodu 400 veya daha büyük) hatası olduğunu gösteren HTTP durum kodları için ayrıntılı hata bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5845d-210">Detailed error information for HTTP status codes that indicate a failure (status code 400 or greater).</span></span>
    - [<span data-ttu-id="5845d-211">Ayrıntılı hata günlüğü hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="5845d-211">Learn more about detailed error logging</span></span>](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- <span data-ttu-id="5845d-212">**Başarısız istek izleme**</span><span class="sxs-lookup"><span data-stu-id="5845d-212">**Failed Request Tracing**</span></span>
    - <span data-ttu-id="5845d-213">İstek ve her bileşenin geçen süre işlemek için kullanılan IIS bileşenlerini izleme de dahil olmak üzere, başarısız istekler hakkında ayrıntılı bilgiler.</span><span class="sxs-lookup"><span data-stu-id="5845d-213">Detailed information on failed requests, including a trace of the IIS components used to process the request and the time taken in each component.</span></span>
    - <span data-ttu-id="5845d-214">Günlükleri ne yalıtmak çalışılırken bir özel HTTP hata neden olduğunda yararlı isteği başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="5845d-214">Failed request logs are useful when trying to isolate what is causing a specific HTTP error.</span></span>
    - [<span data-ttu-id="5845d-215">Başarısız istek izleme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="5845d-215">Learn more about failed request tracing</span></span>](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

<span data-ttu-id="5845d-216">Sunucu günlük kaydını etkinleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="5845d-216">To enable Server logging:</span></span>
- <span data-ttu-id="5845d-217">Git **izleme** > **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="5845d-217">go to **Monitoring** > **Diagnostic Logs**.</span></span>
- <span data-ttu-id="5845d-218">Web sunucusu değiştirme düğmelerini kullanarak tanılama farklı türde etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5845d-218">Enable the different types of Web Server Diagnostics using the toggles.</span></span>

![İzleyici uygulama](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> <span data-ttu-id="5845d-220">Günlüğü etkinleştirme uygulama performans ve kaynak kullanımı üzerinde bir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="5845d-220">Enabling logging has an impact on your application performance and resource utilization.</span></span> <span data-ttu-id="5845d-221">Üretim senaryoları için hata günlüklerini önerilir, yalnızca etkinleştirmek sorunları incelemeye günlüğe kaydetme daha ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="5845d-221">For Production Scenarios, Error logs are recommended, Only Enable more verbose logging when investigating issues.</span></span>

### <a name="accessing-logs"></a><span data-ttu-id="5845d-222">Günlükleri erişme</span><span class="sxs-lookup"><span data-stu-id="5845d-222">Accessing Logs</span></span>
<span data-ttu-id="5845d-223">BLOB storage'da depolanan günlükleri, Azure Storage Gezgini kullanılarak erişilir.</span><span class="sxs-lookup"><span data-stu-id="5845d-223">Logs stored in blob storage are accessed using Azure Storage Explorer.</span></span> <span data-ttu-id="5845d-224">Web uygulamanızın dosya sistemi içinde depolanan günlükleri şu yolların altında FTP aracılığıyla erişilen:</span><span class="sxs-lookup"><span data-stu-id="5845d-224">Logs stored in the Web App's filesystem are accessed through FTP under the following paths:</span></span>

- <span data-ttu-id="5845d-225">**Uygulama günlüklerini** - `%HOME%/LogFiles/Application/`.</span><span class="sxs-lookup"><span data-stu-id="5845d-225">**Application logs** - `%HOME%/LogFiles/Application/`.</span></span>
    - <span data-ttu-id="5845d-226">Bu klasör uygulama günlüğü tarafından üretilen bilgileri içeren bir veya daha fazla metin dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="5845d-226">This folder contains one or more text files containing information produced by application logging.</span></span>
- <span data-ttu-id="5845d-227">**Başarısız istek izlemelerin** - `%HOME%/LogFiles/W3SVC#########/`.</span><span class="sxs-lookup"><span data-stu-id="5845d-227">**Failed Request Traces** - `%HOME%/LogFiles/W3SVC#########/`.</span></span>
    - <span data-ttu-id="5845d-228">Bu klasör bir XSL dosyası ve bir veya daha fazla XML dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="5845d-228">This folder contains an XSL file and one or more XML files.</span></span>
- <span data-ttu-id="5845d-229">**Ayrıntılı Hata günlüklerini** - `%HOME%/LogFiles/DetailedErrors/`.</span><span class="sxs-lookup"><span data-stu-id="5845d-229">**Detailed Error Logs** - `%HOME%/LogFiles/DetailedErrors/`.</span></span>
    - <span data-ttu-id="5845d-230">Bu klasör, uygulamanız tarafından oluşturulan HTTP hataları hakkında kapsamlı bilgi içeren bir veya daha fazla .htm dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="5845d-230">This folder contains one or more .htm files with extensive information on HTTP errors generated by your app.</span></span>
- <span data-ttu-id="5845d-231">**Web sunucu günlükleri** - `%HOME%/LogFiles/http/RawLogs`.</span><span class="sxs-lookup"><span data-stu-id="5845d-231">**Web Server Logs** - `%HOME%/LogFiles/http/RawLogs`.</span></span>
    - <span data-ttu-id="5845d-232">Bu klasör, W3C Genişletilmiş günlük dosyası biçimi kullanılarak biçimlendirilmiş bir veya daha fazla metin dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="5845d-232">This folder contains one or more text files formatted using the W3C extended log file format.</span></span>

## <span data-ttu-id="5845d-233"><a name="streaming"></a>Adım 6 - akış günlük</span><span class="sxs-lookup"><span data-stu-id="5845d-233"><a name="streaming"></a> Step 6 - Log Streaming</span></span>
<span data-ttu-id="5845d-234">Karşılaştırılan zaman kazandırır bu yana uygulama hata ayıklama sırasında akış günlükleri uygun [günlükleri erişme](#Accessing-Logs) FTP aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="5845d-234">Streaming logs are convenient when debugging an application since it saves time compared to [accessing the logs](#Accessing-Logs) through FTP.</span></span>

<span data-ttu-id="5845d-235">Uygulama hizmeti akış **uygulama günlüklerini** ve **Web sunucu günlükleri** bunlar oluşturulduğunda.</span><span class="sxs-lookup"><span data-stu-id="5845d-235">App Service can stream **Application Logs** and **Web Server Logs** as they are generated.</span></span>

> [!TIP]
> <span data-ttu-id="5845d-236">Akış günlükleri, emin olmak denemeden önce toplama günlükleri açıklandığı gibi etkinleştirdiğiniz [günlüğü](#logging) bölümü.</span><span class="sxs-lookup"><span data-stu-id="5845d-236">Before trying to stream logs, make sure you have enabled collecting logs as described in the [Logging](#logging) section.</span></span>

<span data-ttu-id="5845d-237">Akış günlükleri, Git **izleme**> **günlük akışı**.</span><span class="sxs-lookup"><span data-stu-id="5845d-237">To stream logs, go to **Monitoring**> **Log Stream**.</span></span> <span data-ttu-id="5845d-238">Seçin **uygulama günlüklerini** veya **Web sunucu günlükleri** hangi bilgilere bağlı olarak, aradığınız.</span><span class="sxs-lookup"><span data-stu-id="5845d-238">Select **Application Logs** or **Web server logs** depending what information you are looking for.</span></span> <span data-ttu-id="5845d-239">Buradan, ayrıca Duraklat, yeniden başlatın ve arabellek temizleyin.</span><span class="sxs-lookup"><span data-stu-id="5845d-239">From here, you can also pause, restart, and clear the buffer.</span></span>

![Akış günlükleri](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> <span data-ttu-id="5845d-241">Uygulamasını trafiği olduğunda günlükleri yalnızca oluşturulur, daha fazla olayları veya bilgi almak için günlüklerini ayrıntı da artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5845d-241">Logs are only generated when there is traffic on the app, you can also increase the verbosity of logs to get more events or information.</span></span>

## <span data-ttu-id="5845d-242"><a name="remote"></a>7. adım - uzaktan hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="5845d-242"><a name="remote"></a> Step 7 - Remote Debugging</span></span>
<span data-ttu-id="5845d-243">PIN-uygulamaları sorunları kaynağı işaret sonra kullanarak **uzaktan hata ayıklama** kod yürütmek için.</span><span class="sxs-lookup"><span data-stu-id="5845d-243">Once you have pin-pointed the source of the applications problems, use **Remote Debugging** to walk through the code.</span></span>

<span data-ttu-id="5845d-244">Uzaktan hata ayıklama sağlar, bir hata ayıklayıcısı bulutta çalışan Web uygulamanıza ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="5845d-244">Remote debugging lets you attach a debugger to your Web App running in the cloud.</span></span> <span data-ttu-id="5845d-245">Kesme noktalarını ayarlayın, bellek doğrudan yönetmek, aracılığıyla koda adım ve yerel olarak çalışan bir uygulama için gibi bile kod yolu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5845d-245">You can set breakpoints, manipulate memory directly, step through code, and even change the code path just like you do for an app running locally.</span></span>

<span data-ttu-id="5845d-246">Hata ayıklayıcı bulutta çalışan uygulamanıza eklemek için:</span><span class="sxs-lookup"><span data-stu-id="5845d-246">To attach the debugger to your app running in the cloud:</span></span>

- <span data-ttu-id="5845d-247">Visual Studio 2017'nı kullanarak hata ayıklama istediğiniz uygulama için çözüm açın</span><span class="sxs-lookup"><span data-stu-id="5845d-247">Using Visual Studio 2017, open the solution for the app you want to debug</span></span>
- <span data-ttu-id="5845d-248">Yerel geliştirme için gibi bazı Fren noktaları ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5845d-248">Set some brake points just like you would for local development.</span></span>
- <span data-ttu-id="5845d-249">Açık **cloud explorer** (CTRL + /, ctrl + x).</span><span class="sxs-lookup"><span data-stu-id="5845d-249">Open **cloud explorer** (ctr + /, ctrl + x).</span></span>
- <span data-ttu-id="5845d-250">Azure kimlik bilgilerinizle oturum açın, gerektiği gibi oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5845d-250">Log in with your azure credentials as needed.</span></span>
- <span data-ttu-id="5845d-251">Hata ayıklamak istediğiniz uygulamayı bulun</span><span class="sxs-lookup"><span data-stu-id="5845d-251">Find the app you want to debug</span></span>
- <span data-ttu-id="5845d-252">Seçin **Attach hata ayıklayıcı** form **Eylemler** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="5845d-252">Select **Attach Debugger** form the **Actions** pane.</span></span>

![Uzaktan hata ayıklama](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

<span data-ttu-id="5845d-254">Visual Studio uzaktan hata ayıklama için uygulamanızı yapılandırır ve uygulamanıza gider bir tarayıcı penceresi açar.</span><span class="sxs-lookup"><span data-stu-id="5845d-254">Visual Studio configures your application for remote debugging and launches a browser window that navigates to your app.</span></span> <span data-ttu-id="5845d-255">Kesme noktaları ve kod aracılığıyla adım tetiklemek için uygulamanızın göz atın.</span><span class="sxs-lookup"><span data-stu-id="5845d-255">Browse through your app to trigger break points and step through the code.</span></span>

> [!WARNING]
> <span data-ttu-id="5845d-256">Hata ayıklama modunda üretimde çalışan önerilmez.</span><span class="sxs-lookup"><span data-stu-id="5845d-256">Running in debug mode in production is not recommended.</span></span> <span data-ttu-id="5845d-257">Üretim uygulamanız çıkışı için birden fazla sunucu örneğinin ölçeklenmez ise, hata ayıklama engel web sunucusu diğer isteklere yanıt.</span><span class="sxs-lookup"><span data-stu-id="5845d-257">If your production app is not scaled out to multiple server instances, debugging prevent the web server from responding to other requests.</span></span> <span data-ttu-id="5845d-258">Üretim ilgili sorunları gidermek için en iyi şekilde kaynaktır [günlüğe kaydetmeyi yapılandırmak](#logging) ve [Application Insights](#insights).</span><span class="sxs-lookup"><span data-stu-id="5845d-258">For troubleshooting production problems, your best resource is to [configure logging](#logging) and [Application Insights](#insights).</span></span>



## <span data-ttu-id="5845d-259"><a name="explorer"></a>Adım 8 - işlem Gezgini'ni</span><span class="sxs-lookup"><span data-stu-id="5845d-259"><a name="explorer"></a> Step 8 - Process Explorer</span></span>
<span data-ttu-id="5845d-260">Uygulamanız birden fazla örneğine çıkışı ölçeklendirilir zaman **işlem Gezgini'ni** örneği belirli sorunları belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="5845d-260">When your application is scaled out to more than one instance, **process explorer** can help you identify instance specific problems.</span></span>

<span data-ttu-id="5845d-261">Kullanım **işlem Gezgini'ni** için:</span><span class="sxs-lookup"><span data-stu-id="5845d-261">Use **Process Explorer** to:</span></span>

- <span data-ttu-id="5845d-262">Tüm işlemler farklı uygulama hizmeti planınızı örneklerinde sıralar.</span><span class="sxs-lookup"><span data-stu-id="5845d-262">Enumerate all the processes across different instances of your App Service plan.</span></span>
- <span data-ttu-id="5845d-263">Detaya ve işleyicileri ve modülleri her işlemle ilişkili görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="5845d-263">Drill down and view the handles and modules associated with each process.</span></span>
- <span data-ttu-id="5845d-264">CPU, çalışma kümesi, görüntüleyin ve iş parçacığı sayısı kaçak işlemleri tanımlamanıza yardımcı olması için işlem düzeyinde</span><span class="sxs-lookup"><span data-stu-id="5845d-264">View CPU, Working Set, and Thread count at the process level to help you identify runaway processes</span></span>
- <span data-ttu-id="5845d-265">Açık dosya işlemesi bulun ve hatta belirli işlem örneği sonlandır.</span><span class="sxs-lookup"><span data-stu-id="5845d-265">Find open file handles, and even kill a specific process instance.</span></span>

<span data-ttu-id="5845d-266">İşlem Gezgini'ni altında bulunabilir **izleme** > **işlem Gezgini'ni**.</span><span class="sxs-lookup"><span data-stu-id="5845d-266">Process Explorer can be found under **Monitoring** > **Process Explorer**.</span></span>

![İşlem Gezgini](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <span data-ttu-id="5845d-268"><a name="insights"></a>Adım 9 - Application Insights</span><span class="sxs-lookup"><span data-stu-id="5845d-268"><a name="insights"></a> Step 9 - Application Insights</span></span>
<span data-ttu-id="5845d-269">**Application Insights** uygulamanız için uygulama profili oluşturma ve Gelişmiş izleme özelliklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="5845d-269">**Application Insights** provides application profiling and advanced monitoring capabilities for your app.</span></span>

<span data-ttu-id="5845d-270">Application Insights algılamak ve özel durumları ve Web uygulamanızda performans sorunlarını tanılamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="5845d-270">Use Application Insights to detect and diagnose exceptions and performance issues in your Web App.</span></span>

<span data-ttu-id="5845d-271">Web uygulamanız için Application Insights etkinleştirebilirsiniz **izleme** > **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="5845d-271">You can enable Application Insights for your Web App under **Monitoring** > **Application Insights**</span></span>

> [!NOTE]
> <span data-ttu-id="5845d-272">Application Insights veri toplama başlatmak için Application Insights site uzantıyı yüklemek isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="5845d-272">Application Insights might prompt you to install the Application Insights site extension to start collecting data.</span></span> <span data-ttu-id="5845d-273">Site uzantısı yükleme uygulama yeniden başlatma neden olur.</span><span class="sxs-lookup"><span data-stu-id="5845d-273">Installing the site extension causes an application restart.</span></span>

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

<span data-ttu-id="5845d-275">Application Insights ayarlanırsa, daha fazla bilgi edinmek için dahil bağlantıları izleyin zengin bir özellik olan [sonraki adımlar](#next) bölümü.</span><span class="sxs-lookup"><span data-stu-id="5845d-275">Application Insights has a rich feature set, to learn more, follow the links included in the [Next Steps](#next) section.</span></span>

## <span data-ttu-id="5845d-276"><a name="next"></a> Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5845d-276"><a name="next"></a> Next steps</span></span>

 - [<span data-ttu-id="5845d-277">Application Insights nedir</span><span class="sxs-lookup"><span data-stu-id="5845d-277">What is Application Insights</span></span>](..\application-insights\app-insights-overview.md)
 - [<span data-ttu-id="5845d-278">Application Insights ile Azure web uygulaması performans izleme</span><span class="sxs-lookup"><span data-stu-id="5845d-278">Monitor Azure web app performance with Application Insights</span></span>](..\application-insights\app-insights-azure-web-apps.md)
 - [<span data-ttu-id="5845d-279">İzleyici kullanılabilirliği ve yanıt hızını Application Insights ile herhangi bir web sitesi</span><span class="sxs-lookup"><span data-stu-id="5845d-279">Monitor availability and responsiveness of any web site with Application Insights</span></span>](..\application-insights\app-insights-monitor-web-app-availability.md)
