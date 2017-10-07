---
title: "Azure Application Insights ile Java eclipse'te aaaGet Başlarken | Microsoft docs"
description: "Merhaba Eclipse eklenti tooadd performans ve kullanım tooyour Java Web Application Insights ile izleme kullanın"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="6adcb-103">Application Insights ile Java eclipse'te kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6adcb-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="6adcb-104">Merhaba Application Insights SDK'sı, telemetri Java web uygulamanızı gönderir kullanımını ve performansını analiz edin.</span><span class="sxs-lookup"><span data-stu-id="6adcb-104">hello Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="6adcb-105">Merhaba kutusunu telemetri artı toowrite özel telemetri kullanabileceğiniz bir API dışında elde etmeniz hello Eclipse için Application Insights eklenti hello SDK projenize otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="6adcb-105">hello Eclipse plug-in for Application Insights automatically installs hello SDK in your project so that you get out of hello box telemetry, plus an API that you can use toowrite custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="6adcb-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6adcb-106">Prerequisites</span></span>
<span data-ttu-id="6adcb-107">Şu anda hello eklenti Maven projelerini ve Eclipse dinamik Web projeleri için çalışır.</span><span class="sxs-lookup"><span data-stu-id="6adcb-107">Currently hello plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="6adcb-108">([Application Insights Ekle tooother Java proje türleri][java].)</span><span class="sxs-lookup"><span data-stu-id="6adcb-108">([Add Application Insights tooother types of Java project][java].)</span></span>

<span data-ttu-id="6adcb-109">Gerekenler:</span><span class="sxs-lookup"><span data-stu-id="6adcb-109">You'll need:</span></span>

* <span data-ttu-id="6adcb-110">Oracle JRE 1.6 veya sonraki sürümleri</span><span class="sxs-lookup"><span data-stu-id="6adcb-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="6adcb-111">Bir abonelik çok[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="6adcb-111">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="6adcb-112">[Java EE geliştiricileri için Eclipse IDE](http://www.eclipse.org/downloads/), Indigo olarak biliniyordu veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="6adcb-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="6adcb-113">Windows 7 veya üzeri ya da Windows Server 2008 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="6adcb-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-hello-sdk-on-eclipse-one-time"></a><span data-ttu-id="6adcb-114">Eclipse (bir kez) üzerinde Hello SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="6adcb-114">Install hello SDK on Eclipse (one time)</span></span>
<span data-ttu-id="6adcb-115">Yalnızca bu makine başına bir kez toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="6adcb-115">You only have toodo this one time per machine.</span></span> <span data-ttu-id="6adcb-116">Bu adım, daha sonra hello SDK tooeach dinamik Web projesi ekleyebilirsiniz bir araç yükler.</span><span class="sxs-lookup"><span data-stu-id="6adcb-116">This step installs a toolkit which can then add hello SDK tooeach Dynamic Web Project.</span></span>

1. <span data-ttu-id="6adcb-117">Eclipse'te, Yardım, yeni yazılım Yükle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="6adcb-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Yardım, yeni yazılım yükleme](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="6adcb-119">Merhaba SDK Azure Araç Seti altında http://dl.microsoft.com/eclipse kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="6adcb-119">hello SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="6adcb-120">İşaretini **tüm güncelleştirme siteleri başvurun...**</span><span class="sxs-lookup"><span data-stu-id="6adcb-120">Uncheck **Contact all update sites...**</span></span>

    ![Application Insights SDK'sı, temizlemek için kişi tüm siteleri güncelleştir](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="6adcb-122">Her bir Java projesi için adımları kalan hello izleyin.</span><span class="sxs-lookup"><span data-stu-id="6adcb-122">Follow hello remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="6adcb-123">Application Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6adcb-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="6adcb-124">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6adcb-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6adcb-125">Yeni Application Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6adcb-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="6adcb-126">Merhaba uygulama türü tooJava web uygulaması ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6adcb-126">Set hello application type tooJava web application.</span></span>  

    ![Tıklama + ve Application Insights seçme](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="6adcb-128">Hello hello yeni kaynağın izleme anahtarını bulun.</span><span class="sxs-lookup"><span data-stu-id="6adcb-128">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="6adcb-129">Toopaste Bu kod projenize kısa bir süre sonra ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6adcb-129">You'll need toopaste this into your code project shortly.</span></span>  

    ![Merhaba yeni kaynağa genel bakışta, Özellikler'i tıklatın ve hello izleme anahtarını kopyalama](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a><span data-ttu-id="6adcb-131">Application Insights tooyour proje ekleyin</span><span class="sxs-lookup"><span data-stu-id="6adcb-131">Add Application Insights tooyour project</span></span>
1. <span data-ttu-id="6adcb-132">Application Insights hello bağlam menüsünden Java web projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6adcb-132">Add Application Insights from hello context menu of your Java web project.</span></span>

    ![Merhaba yeni kaynağa genel bakışta, Özellikler'i tıklatın ve hello izleme anahtarını kopyalama](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="6adcb-134">Hello Azure portal ' aldığınız hello izleme anahtarını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="6adcb-134">Paste hello instrumentation key that you got from hello Azure portal.</span></span>

    ![Merhaba yeni kaynağa genel bakışta, Özellikler'i tıklatın ve hello izleme anahtarını kopyalama](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="6adcb-136">başlangıç anahtarı telemetrinin her öğesiyle birlikte gönderilir ve Application Insights toodisplay söyler kaynağınız içinde.</span><span class="sxs-lookup"><span data-stu-id="6adcb-136">hello key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>

## <a name="run-hello-application-and-see-metrics"></a><span data-ttu-id="6adcb-137">Merhaba uygulamayı çalıştırın ve ölçümleri bakın</span><span class="sxs-lookup"><span data-stu-id="6adcb-137">Run hello application and see metrics</span></span>
<span data-ttu-id="6adcb-138">Uygulamanızı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6adcb-138">Run your application.</span></span>

<span data-ttu-id="6adcb-139">Microsoft Azure'da tooyour Application Insights kaynağı döndür.</span><span class="sxs-lookup"><span data-stu-id="6adcb-139">Return tooyour Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="6adcb-140">HTTP istekleri verileri hello genel bakış dikey penceresinde görünür.</span><span class="sxs-lookup"><span data-stu-id="6adcb-140">HTTP requests data will appear on hello overview blade.</span></span> <span data-ttu-id="6adcb-141">(Orada değilse, birkaç saniye bekleyip Yenile’ye tıklayın.)</span><span class="sxs-lookup"><span data-stu-id="6adcb-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="6adcb-142">Sunucu yanıtı, istek sayısını ve hataları</span><span class="sxs-lookup"><span data-stu-id="6adcb-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="6adcb-143">Tıklatın herhangi grafik toosee ayrıntılı ölçümler.</span><span class="sxs-lookup"><span data-stu-id="6adcb-143">Click through any chart toosee more detailed metrics.</span></span>

![Ada göre istek sayısı](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="6adcb-145">[Ölçümler hakkında daha fazla bilgi edinin.][metrics]</span><span class="sxs-lookup"><span data-stu-id="6adcb-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="6adcb-146">Ve istek hello özellikleri görüntülendiğinde, istekler ve özel durumlar gibi ilişkili hello telemetri olayları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6adcb-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![Bu istek için tüm izlemeleri](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="6adcb-148">İstemci tarafı telemetri</span><span class="sxs-lookup"><span data-stu-id="6adcb-148">Client-side telemetry</span></span>
<span data-ttu-id="6adcb-149">Merhaba hızlı başlangıç dikey penceresinden Get kod toomonitor web sayfalarımı tıklayın:</span><span class="sxs-lookup"><span data-stu-id="6adcb-149">From hello QuickStart blade, click Get code toomonitor my web pages:</span></span>

![Uygulama genel bakış dikey pencerenizde, Hızlı Başlat'ı seçin, web sayfalarımı kod toomonitor alın.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="6adcb-152">HTML dosyalarınızı hello head içinde Hello kod parçacığını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6adcb-152">Insert hello code snippet in hello head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="6adcb-153">İstemci tarafı verileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="6adcb-153">View client-side data</span></span>
<span data-ttu-id="6adcb-154">Güncelleştirilmiş web sayfalarınıza açın ve bunları kullanın.</span><span class="sxs-lookup"><span data-stu-id="6adcb-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="6adcb-155">Veya iki dakika bekleyin, sonra tooApplication Öngörüler ve açık hello kullanım dikey döndürür.</span><span class="sxs-lookup"><span data-stu-id="6adcb-155">Wait a minute or two, then return tooApplication Insights and open hello usage blade.</span></span> <span data-ttu-id="6adcb-156">(Merhaba genel bakış dikey penceresinden aşağı kaydırın ve kullanımı'nı tıklatın.)</span><span class="sxs-lookup"><span data-stu-id="6adcb-156">(From hello Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="6adcb-157">Sayfa görünümü, kullanıcı ve oturum ölçümleri hello kullanım dikey penceresinde görünür:</span><span class="sxs-lookup"><span data-stu-id="6adcb-157">Page view, user, and session metrics will appear on hello usage blade:</span></span>

![Oturumlar, kullanıcılar ve sayfa görünümleri](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="6adcb-159">[İstemci tarafı telemetri için ayarlama hakkında daha fazla bilgi edinin.][usage]</span><span class="sxs-lookup"><span data-stu-id="6adcb-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="6adcb-160">Uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="6adcb-160">Publish your application</span></span>
<span data-ttu-id="6adcb-161">Artık uygulama toohello sunucunuza yayımlayın, kullanmak ve hello portalda hello telemetri izleyin, kullanıcıların izin verir.</span><span class="sxs-lookup"><span data-stu-id="6adcb-161">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="6adcb-162">Güvenlik duvarınızın, uygulama toosend telemetri toothese bağlantı noktaları verdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="6adcb-162">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="6adcb-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="6adcb-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="6adcb-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="6adcb-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="6adcb-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="6adcb-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="6adcb-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="6adcb-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="6adcb-167">Windows sunucularda yüklenecekler:</span><span class="sxs-lookup"><span data-stu-id="6adcb-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="6adcb-168">Microsoft Visual C++ Yeniden Dağıtılabilir</span><span class="sxs-lookup"><span data-stu-id="6adcb-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="6adcb-169">(Performans sayaçlarını etkinleştirir.)</span><span class="sxs-lookup"><span data-stu-id="6adcb-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="6adcb-170">Özel durumlar ve istek hataları</span><span class="sxs-lookup"><span data-stu-id="6adcb-170">Exceptions and request failures</span></span>
<span data-ttu-id="6adcb-171">İşlenmeyen özel durumlar otomatik olarak toplanır:</span><span class="sxs-lookup"><span data-stu-id="6adcb-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="6adcb-172">diğer özel durumlar toocollect verileri, iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="6adcb-172">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="6adcb-173">[INSERT çağırır tooTrackException kodunuzda](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="6adcb-173">[Insert calls tooTrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="6adcb-174">[Sunucunuza Hello Java Agent Yükleme](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="6adcb-174">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="6adcb-175">Toowatch istediğiniz hello yöntemleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="6adcb-175">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="6adcb-176">Yöntem çağrılarını ve dış bağımlılıkları izleme</span><span class="sxs-lookup"><span data-stu-id="6adcb-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="6adcb-177">[Merhaba Java Agent Yükleme](app-insights-java-agent.md) toolog belirtilen dahili yöntemleri ve zamanlama verileriyle JDBC yapılan çağrıları.</span><span class="sxs-lookup"><span data-stu-id="6adcb-177">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="6adcb-178">Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="6adcb-178">Performance counters</span></span>
<span data-ttu-id="6adcb-179">Genel Bakış dikey penceresini aşağı kaydırarak ve hello tıklatın **sunucuları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="6adcb-179">On your Overview blade, scroll down and click hello  **Servers** tile.</span></span> <span data-ttu-id="6adcb-180">Bir dizi performans sayacı göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="6adcb-180">You'll see a range of performance counters.</span></span>

![Tooclick hello sunucuları döşeme kaydırın](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="6adcb-182">Performans sayacı koleksiyonunu özelleştirme</span><span class="sxs-lookup"><span data-stu-id="6adcb-182">Customize performance counter collection</span></span>
<span data-ttu-id="6adcb-183">performans sayaçları, standart kümesi hello toodisable koleksiyonu hello hello Applicationınsights.XML dosyasının kök düğümü altında koddan hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6adcb-183">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="6adcb-184">Ek performans sayaçlarını toplama</span><span class="sxs-lookup"><span data-stu-id="6adcb-184">Collect additional performance counters</span></span>
<span data-ttu-id="6adcb-185">Ek performans sayaçları toobe toplanan belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6adcb-185">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="6adcb-186">JMX sayaçları (Java sanal makinesi hello tarafından gösterilen)</span><span class="sxs-lookup"><span data-stu-id="6adcb-186">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="6adcb-187">`displayName`– hello Application Insights portalında görüntülenen hello adı.</span><span class="sxs-lookup"><span data-stu-id="6adcb-187">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="6adcb-188">`objectName`– hello JMX nesne adı.</span><span class="sxs-lookup"><span data-stu-id="6adcb-188">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="6adcb-189">`attribute`– hello JMX nesne adı toofetch hello özniteliği</span><span class="sxs-lookup"><span data-stu-id="6adcb-189">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="6adcb-190">`type`(isteğe bağlı) - JMX nesnenin öznitelik türü hello:</span><span class="sxs-lookup"><span data-stu-id="6adcb-190">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="6adcb-191">Varsayılan: int veya long gibi basit bir tür.</span><span class="sxs-lookup"><span data-stu-id="6adcb-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="6adcb-192">`composite`: hello performans sayacı verileri 'Attribute.Data' hello biçiminde değil</span><span class="sxs-lookup"><span data-stu-id="6adcb-192">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="6adcb-193">`tabular`: hello performans sayacı verileri tablo satırı hello biçiminde değil</span><span class="sxs-lookup"><span data-stu-id="6adcb-193">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="6adcb-194">Windows performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="6adcb-194">Windows performance counters</span></span>
<span data-ttu-id="6adcb-195">Her [Windows performans sayacı](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) bir kategorinin üyesidir (Merhaba, bir alanın bir sınıf üyesi olduğunu aynı şekilde).</span><span class="sxs-lookup"><span data-stu-id="6adcb-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="6adcb-196">Kategoriler genel olabileceği gibi numaralı veya adlı örneklere de sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="6adcb-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="6adcb-197">displayName – hello Application Insights portalında görüntülenen hello adı.</span><span class="sxs-lookup"><span data-stu-id="6adcb-197">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="6adcb-198">categoryName – bu performans sayacı ilişkilendirildiği hello performans sayacı kategorisi (performans nesnesi).</span><span class="sxs-lookup"><span data-stu-id="6adcb-198">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="6adcb-199">counterName – hello hello performans sayacının adını.</span><span class="sxs-lookup"><span data-stu-id="6adcb-199">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="6adcb-200">instanceName – hello hello performans sayacı kategorisi örneğinin adını ya da boş bir dize (""), tek bir örnek hello kategorisi içerir.</span><span class="sxs-lookup"><span data-stu-id="6adcb-200">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="6adcb-201">Merhaba categoryName işlem toocollect istediğinizi hello performans sayacı olduğundan hello geçerli JVM işleminden ise, uygulamanızı çalıştıran, belirtin `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="6adcb-201">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="6adcb-202">Özel ölçümleriniz [Ölçüm Gezgini][metrics]'nde olduğundan performans sayaçlarınız görünürdür.</span><span class="sxs-lookup"><span data-stu-id="6adcb-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="6adcb-203">Unix Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="6adcb-203">Unix performance counters</span></span>
* <span data-ttu-id="6adcb-204">[Merhaba Application Insights eklentisiyle collectd yükleyin](app-insights-java-collectd.md) tooget çok çeşitli sistem ve ağ verileri.</span><span class="sxs-lookup"><span data-stu-id="6adcb-204">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="6adcb-205">Kullanılabilirlik web testleri</span><span class="sxs-lookup"><span data-stu-id="6adcb-205">Availability web tests</span></span>
<span data-ttu-id="6adcb-206">Application Insights olan yukarı düzenli aralıklarla toocheck ve düzgün yanıt Web sitenizi test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6adcb-206">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="6adcb-207">[Yukarı tooset][availability], tooclick kullanılabilirlik aşağı kaydırın.</span><span class="sxs-lookup"><span data-stu-id="6adcb-207">[tooset up][availability], scroll down tooclick Availability.</span></span>

![Aşağı kaydırıp, Kullanılabilirlik’e ve Web testi ekle’ye tıklama](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="6adcb-209">Yanıt süreleri grafiklerine ek olarak, siteniz devre dışı kalırsa e-posta bildirimleri de alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="6adcb-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Web testi örneği](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="6adcb-211">[Kullanılabilirlik web testleri hakkında daha fazla bilgi edinin.][availability]</span><span class="sxs-lookup"><span data-stu-id="6adcb-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="6adcb-212">Tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="6adcb-212">Diagnostic logs</span></span>
<span data-ttu-id="6adcb-213">Logback veya Log4J kullanıyorsanız (1.2 sürümü veya v2.0) izleme için otomatik olarak tooApplication burada keşfedin ve bunlar üzerinde arama Öngörüler gönderilen, izleme günlükleri sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="6adcb-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

<span data-ttu-id="6adcb-214">[Tanılama günlükleri hakkında daha fazla bilgi edinin][javalogs]</span><span class="sxs-lookup"><span data-stu-id="6adcb-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="6adcb-215">Özel telemetri</span><span class="sxs-lookup"><span data-stu-id="6adcb-215">Custom telemetry</span></span>
<span data-ttu-id="6adcb-216">Birkaç satır kod ile kullanıcıların gerçekleştirdiği çıkışı, Java web uygulaması toofind eklemek veya toohelp sorunları tanılayın.</span><span class="sxs-lookup"><span data-stu-id="6adcb-216">Insert a few lines of code in your Java web application toofind out what users are doing with it or toohelp diagnose problems.</span></span>

<span data-ttu-id="6adcb-217">Web sayfası JavaScript hem de hello sunucu tarafı Java kod ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6adcb-217">You can insert code both in web page JavaScript and in hello server-side Java.</span></span>

<span data-ttu-id="6adcb-218">[Özel telemetri hakkında bilgi edinin][track]</span><span class="sxs-lookup"><span data-stu-id="6adcb-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="6adcb-219">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6adcb-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="6adcb-220">Sorunlarını tanılamak ve Algıla</span><span class="sxs-lookup"><span data-stu-id="6adcb-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="6adcb-221">[Web istemcisi telemetrisini ekleyin] [ usage] tooget performans telemetrisini hello web istemcisi.</span><span class="sxs-lookup"><span data-stu-id="6adcb-221">[Add web client telemetry][usage] tooget performance telemetry from hello web client.</span></span>
* <span data-ttu-id="6adcb-222">[Web testleri oluşturma] [ availability] toomake uygulamanızın canlı ve duyarlı kaldığından emin.</span><span class="sxs-lookup"><span data-stu-id="6adcb-222">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>
* <span data-ttu-id="6adcb-223">[Olayları ve günlükleri arayın] [ diagnostic] toohelp sorunları tanılayın.</span><span class="sxs-lookup"><span data-stu-id="6adcb-223">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>
* <span data-ttu-id="6adcb-224">[Log4J veya Logback izlemelerini yakalama][javalogs]</span><span class="sxs-lookup"><span data-stu-id="6adcb-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="6adcb-225">Kullanımı İzleme</span><span class="sxs-lookup"><span data-stu-id="6adcb-225">Track usage</span></span>
* <span data-ttu-id="6adcb-226">[Web istemcisi telemetrisini ekleyin] [ usage] toomonitor sayfa görünümleri ve temel kullanıcı ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="6adcb-226">[Add web client telemetry][usage] toomonitor page views and basic user metrics.</span></span>
* <span data-ttu-id="6adcb-227">[Özel olayları ve ölçümleri izleme](app-insights-web-track-usage.md) nasıl uygulamanız, hem hello istemci ve hello sunucu kullanıldığı hakkında toolearn.</span><span class="sxs-lookup"><span data-stu-id="6adcb-227">[Track custom events and metrics](app-insights-web-track-usage.md) toolearn about how your application is used, both at hello client and hello server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
