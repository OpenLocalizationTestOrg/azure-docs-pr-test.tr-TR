---
title: "Azure Application Insights aaaMonitor Docker uygulamalarında | Microsoft Docs"
description: "Docker performans sayaçları, olaylar ve özel durumları Application Insights üzerinde hello telemetri kapsayıcılı hello uygulamalardan birlikte görüntülenebilir."
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
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a><span data-ttu-id="f38ea-103">Application ınsights'ta Docker uygulama izleme</span><span class="sxs-lookup"><span data-stu-id="f38ea-103">Monitor Docker applications in Application Insights</span></span>
<span data-ttu-id="f38ea-104">Yaşam döngüsü olayları ve performans sayaçları [Docker](https://www.docker.com/) kapsayıcıları Application Insights grafiğinin.</span><span class="sxs-lookup"><span data-stu-id="f38ea-104">Lifecycle events and performance counters from [Docker](https://www.docker.com/) containers can be charted on Application Insights.</span></span> <span data-ttu-id="f38ea-105">Merhaba yüklemek [Application Insights](app-insights-overview.md) ana bilgisayarınız ve kapsayıcısında görüntü olarak için diğer görüntüleri hello gibi hello ana performans sayaçlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="f38ea-105">Install hello [Application Insights](app-insights-overview.md) image in a container in your host, and it will display performance counters for hello host, as well as for hello other images.</span></span>

<span data-ttu-id="f38ea-106">Docker ile uygulamalarınızı basit kapsayıcılarında tüm bağımlılıkları ile tam dağıtın.</span><span class="sxs-lookup"><span data-stu-id="f38ea-106">With Docker, you distribute your apps in lightweight containers complete with all dependencies.</span></span> <span data-ttu-id="f38ea-107">Bunlar, Docker altyapısına çalıştıran herhangi bir ana makinede çalıştıracaksınız.</span><span class="sxs-lookup"><span data-stu-id="f38ea-107">They'll run on any host machine that runs a Docker Engine.</span></span>

<span data-ttu-id="f38ea-108">Merhaba çalıştırdığınızda [Application Insights görüntü](https://hub.docker.com/r/microsoft/applicationinsights/) , Docker ana bilgisayarda bu avantajlarını elde edersiniz:</span><span class="sxs-lookup"><span data-stu-id="f38ea-108">When you run hello [Application Insights image](https://hub.docker.com/r/microsoft/applicationinsights/) on your Docker host, you get these benefits:</span></span>

* <span data-ttu-id="f38ea-109">Yaşam döngüsü telemetri çalıştıran tüm Merhaba kapsayıcılara hakkında hello konakta - başlatmak, durdurmak ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="f38ea-109">Lifecycle telemetry about all hello containers running on hello host - start, stop, and so on.</span></span>
* <span data-ttu-id="f38ea-110">Tüm Merhaba kapsayıcılara için performans sayaçları.</span><span class="sxs-lookup"><span data-stu-id="f38ea-110">Performance counters for all hello containers.</span></span> <span data-ttu-id="f38ea-111">CPU, bellek, ağ kullanımını ve daha fazlası.</span><span class="sxs-lookup"><span data-stu-id="f38ea-111">CPU, memory, network usage, and more.</span></span>
* <span data-ttu-id="f38ea-112">Varsa, [Java için Application Insights SDK'sı yüklü](app-insights-java-live.md) Merhaba kapsayıcılara çalıştıran hello uygulamalarında, bu uygulamaların tüm hello telemetri hello kapsayıcı ve ana bilgisayar makinesi tanımlama ek özellikleri sahip olur.</span><span class="sxs-lookup"><span data-stu-id="f38ea-112">If you [installed Application Insights SDK for Java](app-insights-java-live.md) in hello apps running in hello containers, all hello telemetry of those apps will have additional properties identifying hello container and host machine.</span></span> <span data-ttu-id="f38ea-113">Dolayısıyla örneğin bir uygulama içinde birden fazla ana çalışan örneklerini varsa, ana bilgisayar tarafından uygulama telemetrinizi kolayca filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f38ea-113">So for example, if you have instances of an app running in more than one host, you can easily filter your app telemetry by host.</span></span>

![Örnek](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a><span data-ttu-id="f38ea-115">Application Insights kaynağı ayarladıysanız</span><span class="sxs-lookup"><span data-stu-id="f38ea-115">Set up your Application Insights resource</span></span>
1. <span data-ttu-id="f38ea-116">Oturum [Microsoft Azure portal](https://azure.com) ve açın; uygulamanız için hello Application Insights kaynağı veya [yeni bir tane oluşturun](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="f38ea-116">Sign into [Microsoft Azure portal](https://azure.com) and open hello Application Insights resource for your app; or [create a new one](app-insights-create-new-resource.md).</span></span> 
   
    <span data-ttu-id="f38ea-117">*Hangi kaynak kullanmalıyım?*</span><span class="sxs-lookup"><span data-stu-id="f38ea-117">*Which resource should I use?*</span></span> <span data-ttu-id="f38ea-118">Konağınız üzerinde çalışan hello uygulamaları başka birisi tarafından geliştirilmiştir sonra çok ihtiyacınız[yeni bir Application Insights kaynağı oluşturma](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="f38ea-118">If hello apps that you are running on your host were developed by someone else, then you need too[create a new Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="f38ea-119">Burada görüntüleyebilir ve hello telemetriyi Çözümle budur.</span><span class="sxs-lookup"><span data-stu-id="f38ea-119">This is where you view and analyze hello telemetry.</span></span> <span data-ttu-id="f38ea-120">('Genel' hello uygulama türü için seçin.)</span><span class="sxs-lookup"><span data-stu-id="f38ea-120">(Select 'General' for hello app type.)</span></span>
   
    <span data-ttu-id="f38ea-121">Ancak hello uygulamaların hello Geliştirici değilseniz, daha sonra umuyoruz [Application Insights SDK'sı eklenen](app-insights-java-live.md) bunların tooeach.</span><span class="sxs-lookup"><span data-stu-id="f38ea-121">But if you're hello developer of hello apps, then we hope you [added Application Insights SDK](app-insights-java-live.md) tooeach of them.</span></span> <span data-ttu-id="f38ea-122">Gerçekten'ın tüm bileşenleri tek bir iş uygulaması değilseniz, ardından bunların tümünün toosend telemetri tooone kaynak yapılandırın ve bu aynı kaynak toodisplay hello Docker yaşam döngüsü ve performans verileri kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="f38ea-122">If they're all really components of a single business application, then you might configure all of them toosend telemetry tooone resource, and you'll use that same resource toodisplay hello Docker lifecycle and performance data.</span></span> 
   
    <span data-ttu-id="f38ea-123">Üçüncü senaryo hello uygulamaların çoğu geliştirilmiş, ancak bunların telemetri ayrı kaynaklar toodisplay kullanıyorsanız ' dir.</span><span class="sxs-lookup"><span data-stu-id="f38ea-123">A third scenario is that you developed most of hello apps, but you are using separate resources toodisplay their telemetry.</span></span> <span data-ttu-id="f38ea-124">Bu durumda, büyük olasılıkla da istediğiniz toocreate hello Docker verileri için ayrı bir kaynak.</span><span class="sxs-lookup"><span data-stu-id="f38ea-124">In that case, you probably also want toocreate a separate resource for hello Docker data.</span></span> 
2. <span data-ttu-id="f38ea-125">Ekle hello Docker döşeme: seçin **eklemek döşeme**hello Docker döşeme hello Galerisi'nden sürükleyin ve ardından **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="f38ea-125">Add hello Docker tile: Choose **Add Tile**, drag hello Docker tile from hello gallery, and then click **Done**.</span></span> 
   
    ![Örnek](./media/app-insights-docker/03.png)
3. <span data-ttu-id="f38ea-127">Merhaba tıklatın **Essentials** açılır ve hello izleme anahtarını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="f38ea-127">Click hello **Essentials** drop-down and copy hello Instrumentation Key.</span></span> <span data-ttu-id="f38ea-128">Bu tootell hello SDK kullandığınız nerede toosend kendi telemetri.</span><span class="sxs-lookup"><span data-stu-id="f38ea-128">You use this tootell hello SDK where toosend its telemetry.</span></span>

    ![Örnek](./media/app-insights-docker/02-props.png)

<span data-ttu-id="f38ea-130">Tooit en kısa sürede geri dönerseniz şekilde bu tarayıcı penceresini elinizin altında toolook, telemetrisini tutun.</span><span class="sxs-lookup"><span data-stu-id="f38ea-130">Keep that browser window handy, as you'll come back tooit soon toolook at your telemetry.</span></span>

## <a name="run-hello-application-insights-monitor-on-your-host"></a><span data-ttu-id="f38ea-131">Ana bilgisayarda Hello Application Insights izleyicisini Çalıştır</span><span class="sxs-lookup"><span data-stu-id="f38ea-131">Run hello Application Insights monitor on your host</span></span>
<span data-ttu-id="f38ea-132">Herhangi bir yerde toodisplay hello telemetri olduğuna göre toplamak ve göndermeden hello kapsayıcılı uygulaması ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f38ea-132">Now that you've got somewhere toodisplay hello telemetry, you can set up hello containerized app that will collect and send it.</span></span>

1. <span data-ttu-id="f38ea-133">Tooyour Docker ana bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f38ea-133">Connect tooyour Docker host.</span></span> 
2. <span data-ttu-id="f38ea-134">Bu komutta, izleme anahtarını düzenleyin ve ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f38ea-134">Edit your instrumentation key into this command, and then run it:</span></span>
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

<span data-ttu-id="f38ea-135">Docker ana bilgisayar başına yalnızca bir Application Insights görüntü gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f38ea-135">Only one Application Insights image is required per Docker host.</span></span> <span data-ttu-id="f38ea-136">Uygulamanız birden çok Docker ana bilgisayarda dağıtılırsa, her ana bilgisayarda hello komutu yineleyin.</span><span class="sxs-lookup"><span data-stu-id="f38ea-136">If your application is deployed on multiple Docker hosts, then repeat hello command on every host.</span></span>

## <a name="update-your-app"></a><span data-ttu-id="f38ea-137">Uygulamanızı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f38ea-137">Update your app</span></span>
<span data-ttu-id="f38ea-138">Uygulamanız ile Merhaba izlenmiş olan varsa [Java için Application Insights SDK](app-insights-java-get-started.md), satır hello altında projenizdeki hello Applicationınsights.xml dosyasına aşağıdaki hello eklemek `<TelemetryInitializers>` öğe:</span><span class="sxs-lookup"><span data-stu-id="f38ea-138">If your application is instrumented with hello [Application Insights SDK for Java](app-insights-java-get-started.md), add hello following line into hello ApplicationInsights.xml file in your project, under hello `<TelemetryInitializers>` element:</span></span>

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

<span data-ttu-id="f38ea-139">Bu, uygulamanızdan gönderilen kapsayıcı ve ana bilgisayar kimliği tooevery telemetri öğesi gibi Docker bilgileri ekler.</span><span class="sxs-lookup"><span data-stu-id="f38ea-139">This adds Docker information such as container and host id tooevery telemetry item sent from your app.</span></span>

## <a name="view-your-telemetry"></a><span data-ttu-id="f38ea-140">Telemetrinizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f38ea-140">View your telemetry</span></span>
<span data-ttu-id="f38ea-141">Tooyour Application Insights kaynağını hello Azure portalına geri dönün.</span><span class="sxs-lookup"><span data-stu-id="f38ea-141">Go back tooyour Application Insights resource in hello Azure portal.</span></span>

<span data-ttu-id="f38ea-142">Hello Docker kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f38ea-142">Click through hello Docker tile.</span></span>

<span data-ttu-id="f38ea-143">Özellikle, Docker altyapısı üzerinde çalışan diğer kapsayıcılar varsa, kısa süre içinde hello Docker uygulamadan gelen veri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="f38ea-143">You'll shortly see data arriving from hello Docker app, especially if you have other containers running on your Docker engine.</span></span>

<span data-ttu-id="f38ea-144">Hello görünümleri alabileceğiniz bazıları aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f38ea-144">Here are some of hello views you can get.</span></span>

### <a name="perf-counters-by-host-activity-by-image"></a><span data-ttu-id="f38ea-145">Ana bilgisayar, görüntü göre etkinlik tarafından performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="f38ea-145">Perf counters by host, activity by image</span></span>
![Örnek](./media/app-insights-docker/10.png)

![Örnek](./media/app-insights-docker/11.png)

<span data-ttu-id="f38ea-148">Herhangi bir ana bilgisayar veya görüntü adıyla daha fazla ayrıntı için'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f38ea-148">Click any host or image name for more detail.</span></span>

<span data-ttu-id="f38ea-149">toocustomize hello görünümü, herhangi bir grafik, başlık hello kılavuz'a tıklayın veya ekleme grafik kullanın.</span><span class="sxs-lookup"><span data-stu-id="f38ea-149">toocustomize hello view, click any chart, hello grid heading, or use Add Chart.</span></span> 

<span data-ttu-id="f38ea-150">[Ölçüm Gezgini hakkında daha fazla bilgi](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="f38ea-150">[Learn more about metrics explorer](app-insights-metrics-explorer.md).</span></span>

### <a name="docker-container-events"></a><span data-ttu-id="f38ea-151">Docker kapsayıcısı olayları</span><span class="sxs-lookup"><span data-stu-id="f38ea-151">Docker container events</span></span>
![Örnek](./media/app-insights-docker/13.png)

<span data-ttu-id="f38ea-153">olayları tek tek tooinvestigate, tıklatın [arama](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="f38ea-153">tooinvestigate individual events, click [Search](app-insights-diagnostic-search.md).</span></span> <span data-ttu-id="f38ea-154">İstediğiniz arama ve filtreleme toofind hello olaylar.</span><span class="sxs-lookup"><span data-stu-id="f38ea-154">Search and filter toofind hello events you want.</span></span> <span data-ttu-id="f38ea-155">Tüm olay tooget daha fazla ayrıntı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f38ea-155">Click any event tooget more detail.</span></span>

### <a name="exceptions-by-container-name"></a><span data-ttu-id="f38ea-156">Kapsayıcı adı tarafından özel durumlar</span><span class="sxs-lookup"><span data-stu-id="f38ea-156">Exceptions by container name</span></span>
![Örnek](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a><span data-ttu-id="f38ea-158">Docker bağlamı tooapp telemetri eklendi</span><span class="sxs-lookup"><span data-stu-id="f38ea-158">Docker context added tooapp telemetry</span></span>
<span data-ttu-id="f38ea-159">AI Docker bağlamla zenginleştirilmiş SDK'sı, izlenmiş hello uygulamasından gönderilen telemetri isteği:</span><span class="sxs-lookup"><span data-stu-id="f38ea-159">Request telemetry sent from hello application instrumented with AI SDK, enriched with Docker context:</span></span>

![Örnek](./media/app-insights-docker/16.png)

<span data-ttu-id="f38ea-161">İşlemci zamanı ve kullanılabilir bellek performans sayaçları, zenginleştirilmiş ve Docker kapsayıcısı adına göre gruplandırılır:</span><span class="sxs-lookup"><span data-stu-id="f38ea-161">Processor time and available memory performance counters, enriched and grouped by Docker container name:</span></span>

![Örnek](./media/app-insights-docker/15.png)

## <a name="q--a"></a><span data-ttu-id="f38ea-163">Soru-Cevap</span><span class="sxs-lookup"><span data-stu-id="f38ea-163">Q & A</span></span>
<span data-ttu-id="f38ea-164">*Ne Application Insights Docker elde edilemiyor bana veriyor?*</span><span class="sxs-lookup"><span data-stu-id="f38ea-164">*What does Application Insights give me that I can't get from Docker?*</span></span>

* <span data-ttu-id="f38ea-165">Performans sayaçları kapsayıcı ve görüntü tarafından ayrıntılı dökümü.</span><span class="sxs-lookup"><span data-stu-id="f38ea-165">Detailed breakdown of performance counters by container and image.</span></span>
* <span data-ttu-id="f38ea-166">Kapsayıcı ve uygulama verilerini tek bir Panoda tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="f38ea-166">Integrate container and app data in one dashboard.</span></span>
* <span data-ttu-id="f38ea-167">[Telemetri verme](app-insights-export-telemetry.md) daha fazla analiz tooa veritabanı, Power BI veya diğer Pano için.</span><span class="sxs-lookup"><span data-stu-id="f38ea-167">[Export telemetry](app-insights-export-telemetry.md) for further analysis tooa database, Power BI or other dashboard.</span></span>

<span data-ttu-id="f38ea-168">*Merhaba uygulamadan kendisini telemetri nasıl sağlarım?*</span><span class="sxs-lookup"><span data-stu-id="f38ea-168">*How do I get telemetry from hello app itself?*</span></span>

* <span data-ttu-id="f38ea-169">Merhaba Application Insights SDK'sı hello uygulamada yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f38ea-169">Install hello Application Insights SDK in hello app.</span></span> <span data-ttu-id="f38ea-170">Bilgi edinmek için nasıl: [Java web uygulamaları](app-insights-java-get-started.md), [Windows web uygulamaları](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="f38ea-170">Learn how for: [Java web apps](app-insights-java-get-started.md), [Windows web apps](app-insights-asp-net.md).</span></span>

## <a name="video"></a><span data-ttu-id="f38ea-171">Video</span><span class="sxs-lookup"><span data-stu-id="f38ea-171">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="f38ea-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f38ea-172">Next steps</span></span>

* [<span data-ttu-id="f38ea-173">Java için Application Insights</span><span class="sxs-lookup"><span data-stu-id="f38ea-173">Application Insights for Java</span></span>](app-insights-java-get-started.md)
* [<span data-ttu-id="f38ea-174">Node.js için Application Insights</span><span class="sxs-lookup"><span data-stu-id="f38ea-174">Application Insights for Node.js</span></span>](app-insights-nodejs.md)
* [<span data-ttu-id="f38ea-175">ASP.NET için Application Insights</span><span class="sxs-lookup"><span data-stu-id="f38ea-175">Application Insights for ASP.NET</span></span>](app-insights-asp-net.md)
