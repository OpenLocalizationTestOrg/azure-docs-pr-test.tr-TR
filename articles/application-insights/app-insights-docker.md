---
title: "Azure Application Insights Docker uygulamalarında izleme | Microsoft Docs"
description: "Docker performans sayaçları, olaylar ve özel durumları Application Insights üzerinde kapsayıcılı uygulamalardan telemetri ile birlikte görüntülenebilir."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: b082e345ca1bb3b12c548e05e699474d3aa9306c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="c7658-103">Application ınsights'ta Docker uygulama izleme</span><span class="sxs-lookup"><span data-stu-id="c7658-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="c7658-104">Yaşam döngüsü olayları ve performans sayaçları [Docker](https://www.docker.com/) kapsayıcıları Application Insights grafiğinin.</span><span class="sxs-lookup"><span data-stu-id="c7658-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="c7658-105">Yükleme [Application Insights](app-insights-overview.md) ana bilgisayarınız ve kapsayıcısında görüntü diğer görüntüleri yanı sıra, ana bilgisayar için performans sayaçlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c7658-105">Install the [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for the host, as well as for the other images.</span></span>

<span data-ttu-id="c7658-106">Docker ile uygulamalarınızı basit kapsayıcılarında tüm bağımlılıkları ile tam dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c7658-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="c7658-107">Bunlar, Docker altyapısına çalıştıran herhangi bir ana makinede çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="c7658-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="c7658-108">Çalıştırdığınızda [Application Insights görüntü](https://hub.docker.com/r/microsoft/applicationinsights/) , Docker ana bilgisayarda bu avantajlarını elde edersiniz:</span><span class="sxs-lookup"><span data-stu-id="c7658-108">When you run the [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="c7658-109">Yaşam döngüsü telemetri çalıştıran tüm kapsayıcıları hakkında konakta - başlatmak, durdurmak ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="c7658-109">Lifecycle telemetry about all the containers running on the host - start, stop, and so on.</span></span>
* <span data-ttu-id="c7658-110">Tüm kapsayıcıları için performans sayaçları.</span><span class="sxs-lookup"><span data-stu-id="c7658-110">Performance counters for all the containers.</span></span> <span data-ttu-id="c7658-111">CPU, bellek, ağ kullanımını ve daha fazlası.</span><span class="sxs-lookup"><span data-stu-id="c7658-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="c7658-112">Varsa, [Java için Application Insights SDK'sı yüklü](app-insights-java-live.md) kapsayıcılarında çalışan uygulamalar, bu uygulamaların tüm telemetri kapsayıcı ve ana bilgisayar makine tanımlayan ek özellikleri sahip olur.</span><span class="sxs-lookup"><span data-stu-id="c7658-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in the apps running in the containers, all the telemetry of those apps will have additional properties identifying the container and host machine.</span></span> <span data-ttu-id="c7658-113">Dolayısıyla örneğin bir uygulama içinde birden fazla ana çalışan örneklerini varsa, ana bilgisayar tarafından uygulama telemetrinizi kolayca filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7658-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![Örnek](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="c7658-115">Application Insights kaynağı ayarladıysanız</span><span class="sxs-lookup"><span data-stu-id="c7658-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="c7658-116">Oturum [Microsoft Azure portal](https://azure.com) ve; uygulamanız için Application Insights kaynağını açma veya [yeni bir tane oluşturun](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="c7658-116">Sign into [Microsoft Azure portal](https://azure.com) and open the Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="c7658-117">*Hangi kaynak kullanmalıyım?*</span><span class="sxs-lookup"><span data-stu-id="c7658-117">*Which resource should I use?*</span></span> <span data-ttu-id="c7658-118">Konağınız üzerinde çalışan uygulamalar başka birisi tarafından geliştirilen sonra yapmanız [yeni bir Application Insights kaynağı oluşturma](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="c7658-118">If the apps that you are running on your host were developed by someone else, then you need to [create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="c7658-119">Burada görüntüleyebilir ve telemetriyi Çözümle budur.</span><span class="sxs-lookup"><span data-stu-id="c7658-119">This is where you view and analyze the telemetry.</span></span> <span data-ttu-id="c7658-120">(Uygulama türü için ' genel' seçin.)</span><span class="sxs-lookup"><span data-stu-id="c7658-120">(Select 'General' for the app type.)</span></span>
   
    <span data-ttu-id="c7658-121">Ancak uygulama geliştiricisi olduğunuz sonra umuyoruz [Application Insights SDK'sı eklenen](app-insights-java-live.md) bunların her biri için.</span><span class="sxs-lookup"><span data-stu-id="c7658-121">But if you're the developer of the apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) to each of them.</span></span> <span data-ttu-id="c7658-122">Gerçekten'ın tüm bileşenleri tek bir iş uygulaması olup olmadıklarını, sonra tüm bir kaynağa telemetri gönderecek şekilde yapılandırmanız ve Docker yaşam döngüsü ve performans verilerini görüntülemek için aynı kaynak kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c7658-122">If they're all really components of a single business application, then you might configure all of them to send telemetry to one resource, and you'll use that same resource to display the Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="c7658-123">Üçüncü senaryo uygulamaları çoğunu geliştirilmiş, ancak bunların telemetri görüntülemek için ayrı kaynakları kullanarak ' dir.</span><span class="sxs-lookup"><span data-stu-id="c7658-123">A third scenario is that you developed most of the apps, but you are using separate resources to display their telemetry.</span></span> <span data-ttu-id="c7658-124">Bu durumda, Docker verileri için ayrı bir kaynak oluşturmak için büyük olasılıkla de istersiniz.</span><span class="sxs-lookup"><span data-stu-id="c7658-124">In that case, you probably also want to create a separate resource for the Docker data.</span></span> 
2. <span data-ttu-id="c7658-125">Docker kutucuğu ekleyin: seçin **eklemek döşeme**, Docker döşeme Galeriden sürükleyin ve ardından **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="c7658-125">Add the Docker tile: Choose **Add Tile**, drag the Docker tile from the gallery, and then click **Done**.</span></span> 
   
    ![Örnek](./media/app-insights-docker/03.png)
3. <span data-ttu-id="c7658-127">Tıklatın **Essentials** açılır ve izleme anahtarını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c7658-127">Click the **Essentials** drop-down and copy the Instrumentation Key.</span></span> <span data-ttu-id="c7658-128">Bu SDK, telemetri gönderileceği yeri bildirmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7658-128">You use this to tell the SDK where to send its telemetry.</span></span>

    ![Örnek](./media/app-insights-docker/02-props.png)

<span data-ttu-id="c7658-130">En kısa sürede, telemetrisini görünmesini için geri gelin gibi bu tarayıcı penceresini elinizin altında tutun.</span><span class="sxs-lookup"><span data-stu-id="c7658-130">Keep that browser window handy, as you'll come back to it soon to look at your telemetry.</span></span>

## <a name="run-the-application-insights-monitor-on-your-host"></a><span data-ttu-id="c7658-131">Ana bilgisayarda Application Insights İzleyicisi'ni çalıştırın</span><span class="sxs-lookup"><span data-stu-id="c7658-131">Run the Application Insights monitor on your host</span></span>
<span data-ttu-id="c7658-132">Telemetri görüntülemek için bir yere olduğuna göre toplar ve göndermeden kapsayıcılı uygulama ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c7658-132">Now that you've got somewhere to display the telemetry, you can set up the containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="c7658-133">Docker ana bilgisayara bağlanın.</span><span class="sxs-lookup"><span data-stu-id="c7658-133">Connect to your Docker host.</span></span> 
2. <span data-ttu-id="c7658-134">Bu komutta, izleme anahtarını düzenleyin ve ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c7658-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="c7658-135">Docker ana bilgisayar başına yalnızca bir Application Insights görüntü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c7658-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="c7658-136">Uygulamanız birden çok Docker ana bilgisayarda dağıtılırsa, her ana bilgisayarda komutu yineleyin.</span><span class="sxs-lookup"><span data-stu-id="c7658-136">If your application is deployed on multiple Docker hosts, then repeat the command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="c7658-137">Uygulamanızı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="c7658-137">Update your app</span></span>
<span data-ttu-id="c7658-138">Uygulamanız ile işaretlenir varsa [Java için Application Insights SDK](app-insights-java-get-started.md), altında aşağıdaki satırı projenizdeki Applicationınsights.xml dosyasına ekleyin `<TelemetryInitializers>` öğe:</span><span class="sxs-lookup"><span data-stu-id="c7658-138">If your application is instrumented with the [Application Insights SDK for Java](app-insights-java-get-started.md), add the following line into the ApplicationInsights.xml file in your project, under the `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="c7658-139">Bu kapsayıcı ve ana bilgisayar kimliği gibi Docker bilgileri uygulamanızdan gönderilen her telemetri öğesi ekler.</span><span class="sxs-lookup"><span data-stu-id="c7658-139">This adds Docker information such as container and host id to every telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="c7658-140">Telemetrinizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="c7658-140">View your telemetry</span></span>
<span data-ttu-id="c7658-141">Azure portalında Application Insights kaynağınıza dönün.</span><span class="sxs-lookup"><span data-stu-id="c7658-141">Go back to your Application Insights resource in the Azure portal.</span></span>

<span data-ttu-id="c7658-142">Docker kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7658-142">Click through the Docker tile.</span></span>

<span data-ttu-id="c7658-143">Özellikle, Docker altyapısı üzerinde çalışan diğer kapsayıcılar varsa, kısa süre içinde Docker uygulamadan gelen veri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c7658-143">You'll shortly see data arriving from the Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="c7658-144">Alabileceğiniz görünümleri bazıları aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c7658-144">Here are some of the views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="c7658-145">Ana bilgisayar, görüntü göre etkinlik tarafından performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="c7658-145">Perf counters by host, activity by image</span></span>
![Örnek](./media/app-insights-docker/10.png)

![Örnek](./media/app-insights-docker/11.png)

<span data-ttu-id="c7658-148">Herhangi bir ana bilgisayar veya görüntü adıyla daha fazla ayrıntı için'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c7658-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="c7658-149">Görünümü özelleştirmek için herhangi Grafik başlığı kılavuz'a tıklayın veya ekleme grafik kullanın.</span><span class="sxs-lookup"><span data-stu-id="c7658-149">To customize the view, click any chart, the grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="c7658-150">[Ölçüm Gezgini hakkında daha fazla bilgi](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="c7658-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="c7658-151">Docker kapsayıcısı olayları</span><span class="sxs-lookup"><span data-stu-id="c7658-151">Docker container events</span></span>
![Örnek](./media/app-insights-docker/13.png)

<span data-ttu-id="c7658-153">Olayları tek tek incelemek için tıklatın [arama](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="c7658-153">To investigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="c7658-154">Arama ve istediğiniz olayları bulmak için filtre.</span><span class="sxs-lookup"><span data-stu-id="c7658-154">Search and filter to find the events you want.</span></span> <span data-ttu-id="c7658-155">Daha fazla ayrıntı almak için herhangi bir etkinliğe tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c7658-155">Click any event to get more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="c7658-156">Kapsayıcı adı tarafından özel durumlar</span><span class="sxs-lookup"><span data-stu-id="c7658-156">Exceptions by container name</span></span>
![Örnek](./media/app-insights-docker/14.png)

### <a name="docker-context-added-to-app-telemetry"></a><span data-ttu-id="c7658-158">Uygulama telemetri eklenen docker bağlamı</span><span class="sxs-lookup"><span data-stu-id="c7658-158">Docker context added to app telemetry</span></span>
<span data-ttu-id="c7658-159">AI Docker bağlamla zenginleştirilmiş SDK'sı, izlenmiş uygulamasından gönderilen telemetri isteği:</span><span class="sxs-lookup"><span data-stu-id="c7658-159">Request telemetry sent from the application instrumented with AI SDK, enriched with Docker context:</span></span>

![Örnek](./media/app-insights-docker/16.png)

<span data-ttu-id="c7658-161">İşlemci zamanı ve kullanılabilir bellek performans sayaçları, zenginleştirilmiş ve Docker kapsayıcısı adına göre gruplandırılır:</span><span class="sxs-lookup"><span data-stu-id="c7658-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![Örnek](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="c7658-163">Soru-Cevap</span><span class="sxs-lookup"><span data-stu-id="c7658-163">Q & A</span></span>
<span data-ttu-id="c7658-164">*Ne Application Insights Docker elde edilemiyor bana veriyor?*</span><span class="sxs-lookup"><span data-stu-id="c7658-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="c7658-165">Performans sayaçları kapsayıcı ve görüntü tarafından ayrıntılı dökümü.</span><span class="sxs-lookup"><span data-stu-id="c7658-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="c7658-166">Kapsayıcı ve uygulama verilerini tek bir Panoda tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="c7658-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="c7658-167">[Telemetri verme](app-insights-export-telemetry.md) daha fazla çözümleme için bir veritabanı, Power BI veya diğer Pano için.</span><span class="sxs-lookup"><span data-stu-id="c7658-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis to a database, Power BI or other dashboard.</span></span>

<span data-ttu-id="c7658-168">*Telemetri uygulamasından nasıl sağlarım?*</span><span class="sxs-lookup"><span data-stu-id="c7658-168">*How do I get telemetry from the app itself?*</span></span>

* <span data-ttu-id="c7658-169">Application Insights SDK uygulamada yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c7658-169">Install the Application Insights SDK in the app.</span></span> <span data-ttu-id="c7658-170">Bilgi edinmek için nasıl: [Java web uygulamaları](app-insights-java-get-started.md), [Windows web uygulamaları](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="c7658-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="c7658-171">Video</span><span class="sxs-lookup"><span data-stu-id="c7658-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="c7658-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c7658-172">Next steps</span></span>

* [<span data-ttu-id="c7658-173">Java için Application Insights</span><span class="sxs-lookup"><span data-stu-id="c7658-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="c7658-174">Node.js için Application Insights</span><span class="sxs-lookup"><span data-stu-id="c7658-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="c7658-175">ASP.NET için Application Insights</span><span class="sxs-lookup"><span data-stu-id="c7658-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
