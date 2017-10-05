---
title: "Azure Application Insights ile Java eclipse'te kullanmaya başlama | Microsoft docs"
description: "Eklenti Eclipse performansı ve Application Insights ile Java Web sitenize kullanımı izleme eklemek için kullanın"
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
ms.openlocfilehash: f2f696a3bbe7893c1f521a3e5588f4f93805d6a2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a><span data-ttu-id="b9a63-103">Application Insights ile Java eclipse'te kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b9a63-103">Get started with Application Insights with Java in Eclipse</span></span>
<span data-ttu-id="b9a63-104">Application Insights SDK'sı, telemetri Java web uygulamanızı gönderir kullanımını ve performansını analiz edin.</span><span class="sxs-lookup"><span data-stu-id="b9a63-104">The Application Insights SDK sends telemetry from your Java web application so that you can analyze usage and performance.</span></span> <span data-ttu-id="b9a63-105">Böylece kutusunu telemetri artı özel telemetri yazmak için kullanabileceğiniz bir API dışında almak için Application Insights eklenti Eclipse SDK projenize otomatik olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="b9a63-105">The Eclipse plug-in for Application Insights automatically installs the SDK in your project so that you get out of the box telemetry, plus an API that you can use to write custom telemetry.</span></span>   

## <a name="prerequisites"></a><span data-ttu-id="b9a63-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b9a63-106">Prerequisites</span></span>
<span data-ttu-id="b9a63-107">Şu anda eklenti works Maven projelerini ve Eclipse dinamik Web projeleri için.</span><span class="sxs-lookup"><span data-stu-id="b9a63-107">Currently the plug-in works for Maven projects and Dynamic Web Projects in Eclipse.</span></span>
<span data-ttu-id="b9a63-108">([Java projesi diğer türleri için Application Insights Ekle][java].)</span><span class="sxs-lookup"><span data-stu-id="b9a63-108">([Add Application Insights to other types of Java project][java].)</span></span>

<span data-ttu-id="b9a63-109">Gerekenler:</span><span class="sxs-lookup"><span data-stu-id="b9a63-109">You'll need:</span></span>

* <span data-ttu-id="b9a63-110">Oracle JRE 1.6 veya sonraki sürümleri</span><span class="sxs-lookup"><span data-stu-id="b9a63-110">Oracle JRE 1.6 or later</span></span>
* <span data-ttu-id="b9a63-111">Bir [Microsoft Azure](https://azure.microsoft.com/) aboneliği.</span><span class="sxs-lookup"><span data-stu-id="b9a63-111">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="b9a63-112">[Java EE geliştiricileri için Eclipse IDE](http://www.eclipse.org/downloads/), Indigo olarak biliniyordu veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="b9a63-112">[Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/), Indigo or later.</span></span>
* <span data-ttu-id="b9a63-113">Windows 7 veya üzeri ya da Windows Server 2008 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="b9a63-113">Windows 7 or later, or Windows Server 2008 or later</span></span>

## <a name="install-the-sdk-on-eclipse-one-time"></a><span data-ttu-id="b9a63-114">Eclipse (bir kez) üzerinde SDK'sını yükleyin</span><span class="sxs-lookup"><span data-stu-id="b9a63-114">Install the SDK on Eclipse (one time)</span></span>
<span data-ttu-id="b9a63-115">Yalnızca bu makine başına bir kez yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9a63-115">You only have to do this one time per machine.</span></span> <span data-ttu-id="b9a63-116">Bu adım, daha sonra SDK her dinamik Web projesi ekleyebilirsiniz bir araç yükler.</span><span class="sxs-lookup"><span data-stu-id="b9a63-116">This step installs a toolkit which can then add the SDK to each Dynamic Web Project.</span></span>

1. <span data-ttu-id="b9a63-117">Eclipse'te, Yardım, yeni yazılım Yükle'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b9a63-117">In Eclipse, click Help, Install New Software.</span></span>

    ![Yardım, yeni yazılım yükleme](./media/app-insights-java-eclipse/0-plugin.png)
2. <span data-ttu-id="b9a63-119">SDK Azure Araç Seti altında http://dl.microsoft.com/eclipse kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="b9a63-119">The SDK is in http://dl.microsoft.com/eclipse, under Azure Toolkit.</span></span>
3. <span data-ttu-id="b9a63-120">İşaretini **tüm güncelleştirme siteleri başvurun...**</span><span class="sxs-lookup"><span data-stu-id="b9a63-120">Uncheck **Contact all update sites...**</span></span>

    ![Application Insights SDK'sı, temizlemek için kişi tüm siteleri güncelleştir](./media/app-insights-java-eclipse/1-plugin.png)

<span data-ttu-id="b9a63-122">Her bir Java projesi için kalan adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="b9a63-122">Follow the remaining steps for each Java project.</span></span>

## <a name="create-an-application-insights-resource-in-azure"></a><span data-ttu-id="b9a63-123">Application Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b9a63-123">Create an Application Insights resource in Azure</span></span>
1. <span data-ttu-id="b9a63-124">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b9a63-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b9a63-125">Yeni Application Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b9a63-125">Create a new Application Insights resource.</span></span> <span data-ttu-id="b9a63-126">Uygulama türünü Java web uygulaması olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b9a63-126">Set the application type to Java web application.</span></span>  

    ![Tıklama + ve Application Insights seçme](./media/app-insights-java-eclipse/01-create.png)  

4. <span data-ttu-id="b9a63-128">Yeni kaynağın izleme anahtarını bulun.</span><span class="sxs-lookup"><span data-stu-id="b9a63-128">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="b9a63-129">Bunu hemen kod projenize yapıştırmalısınız.</span><span class="sxs-lookup"><span data-stu-id="b9a63-129">You'll need to paste this into your code project shortly.</span></span>  

    ![Yeni kaynağa genel bakışta, Özellikler'e tıklayıp izleme anahtarını kopyalama](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-to-your-project"></a><span data-ttu-id="b9a63-131">Projenize Application Insights ekleyin</span><span class="sxs-lookup"><span data-stu-id="b9a63-131">Add Application Insights to your project</span></span>
1. <span data-ttu-id="b9a63-132">Application Insights Java web projeniz bağlam menüsünden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b9a63-132">Add Application Insights from the context menu of your Java web project.</span></span>

    ![Yeni kaynağa genel bakışta, Özellikler'e tıklayıp izleme anahtarını kopyalama](./media/app-insights-java-eclipse/02-context-menu.png)
2. <span data-ttu-id="b9a63-134">Azure portalından aldığınız izleme anahtarını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b9a63-134">Paste the instrumentation key that you got from the Azure portal.</span></span>

    ![Yeni kaynağa genel bakışta, Özellikler'e tıklayıp izleme anahtarını kopyalama](./media/app-insights-java-eclipse/03-ikey.png)

<span data-ttu-id="b9a63-136">Anahtarı telemetrinin her öğesiyle birlikte gönderilir ve Application Insights kaynağınıza içinde görüntülemek için söyler.</span><span class="sxs-lookup"><span data-stu-id="b9a63-136">The key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>

## <a name="run-the-application-and-see-metrics"></a><span data-ttu-id="b9a63-137">Uygulamayı çalıştırın ve ölçümleri bakın</span><span class="sxs-lookup"><span data-stu-id="b9a63-137">Run the application and see metrics</span></span>
<span data-ttu-id="b9a63-138">Uygulamanızı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b9a63-138">Run your application.</span></span>

<span data-ttu-id="b9a63-139">Microsoft Azure Application Insights kaynağınıza dönün.</span><span class="sxs-lookup"><span data-stu-id="b9a63-139">Return to your Application Insights resource in Microsoft Azure.</span></span>

<span data-ttu-id="b9a63-140">HTTP verilerin genel bakış dikey penceresinde görüntülenmesini ister.</span><span class="sxs-lookup"><span data-stu-id="b9a63-140">HTTP requests data will appear on the overview blade.</span></span> <span data-ttu-id="b9a63-141">(Orada değilse, birkaç saniye bekleyip Yenile’ye tıklayın.)</span><span class="sxs-lookup"><span data-stu-id="b9a63-141">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![<span data-ttu-id="b9a63-142">Sunucu yanıtı, istek sayısını ve hataları</span><span class="sxs-lookup"><span data-stu-id="b9a63-142">Server response, request counts, and failures</span></span> ](./media/app-insights-java-eclipse/5-results.png)

<span data-ttu-id="b9a63-143">Daha ayrıntılı ölçümler görmek için herhangi bir grafiğe tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b9a63-143">Click through any chart to see more detailed metrics.</span></span>

![Ada göre istek sayısı](./media/app-insights-java-eclipse/6-barchart.png)

<span data-ttu-id="b9a63-145">[Ölçümler hakkında daha fazla bilgi edinin.][metrics]</span><span class="sxs-lookup"><span data-stu-id="b9a63-145">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="b9a63-146">Ve istek özellikleri görüntülendiğinde, istekler ve özel durumlar gibi ilişkili telemetri olayları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9a63-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![Bu istek için tüm izlemeleri](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a><span data-ttu-id="b9a63-148">İstemci tarafı telemetri</span><span class="sxs-lookup"><span data-stu-id="b9a63-148">Client-side telemetry</span></span>
<span data-ttu-id="b9a63-149">Hızlı Başlangıç dikey penceresinden web sayfalarımı izlemeyi sağlayan kodu Al'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="b9a63-149">From the QuickStart blade, click Get code to monitor my web pages:</span></span>

![Uygulamaya genel bakış dikey pencerenizde, Hızlı Başlat, Web sayfalarımı izlemeyi sağlayan kodu al'ı seçin.](./media/app-insights-java-eclipse/02-monitor-web-page.png)

<span data-ttu-id="b9a63-152">Kod parçacığı, HTML dosyaları head içinde ekler.</span><span class="sxs-lookup"><span data-stu-id="b9a63-152">Insert the code snippet in the head of your HTML files.</span></span>

#### <a name="view-client-side-data"></a><span data-ttu-id="b9a63-153">İstemci tarafı verileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="b9a63-153">View client-side data</span></span>
<span data-ttu-id="b9a63-154">Güncelleştirilmiş web sayfalarınıza açın ve bunları kullanın.</span><span class="sxs-lookup"><span data-stu-id="b9a63-154">Open your updated web pages and use them.</span></span> <span data-ttu-id="b9a63-155">Veya iki dakika bekleyin, sonra Application Insights'a dönün ve kullanım dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="b9a63-155">Wait a minute or two, then return to Application Insights and open the usage blade.</span></span> <span data-ttu-id="b9a63-156">(Genel bakış dikey penceresinden aşağı kaydırın ve kullanımı'nı tıklatın.)</span><span class="sxs-lookup"><span data-stu-id="b9a63-156">(From the Overview blade, scroll down and click Usage.)</span></span>

<span data-ttu-id="b9a63-157">Sayfa görünümü, kullanıcı ve oturum ölçümleri kullanım dikey penceresinde görünür:</span><span class="sxs-lookup"><span data-stu-id="b9a63-157">Page view, user, and session metrics will appear on the usage blade:</span></span>

![Oturumlar, kullanıcılar ve sayfa görünümleri](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

<span data-ttu-id="b9a63-159">[İstemci tarafı telemetri için ayarlama hakkında daha fazla bilgi edinin.][usage]</span><span class="sxs-lookup"><span data-stu-id="b9a63-159">[Learn more about setting up client-side telemetry.][usage]</span></span>

## <a name="publish-your-application"></a><span data-ttu-id="b9a63-160">Uygulamanızı yayımlama</span><span class="sxs-lookup"><span data-stu-id="b9a63-160">Publish your application</span></span>
<span data-ttu-id="b9a63-161">Artık uygulamanızı sunucuya yayımlayın, herkesin kullanmasını sağlayın ve portalda gösterilen telemetriye bakın.</span><span class="sxs-lookup"><span data-stu-id="b9a63-161">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="b9a63-162">Güvenlik duvarınızın, uygulamanıza şu bağlantı noktalarına telemetri göndermesine izin verdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="b9a63-162">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="b9a63-163">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="b9a63-163">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="b9a63-164">dc.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="b9a63-164">dc.services.visualstudio.com:80</span></span>
  * <span data-ttu-id="b9a63-165">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="b9a63-165">f5.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="b9a63-166">f5.services.visualstudio.com:80</span><span class="sxs-lookup"><span data-stu-id="b9a63-166">f5.services.visualstudio.com:80</span></span>
* <span data-ttu-id="b9a63-167">Windows sunucularda yüklenecekler:</span><span class="sxs-lookup"><span data-stu-id="b9a63-167">On Windows servers, install:</span></span>

  * [<span data-ttu-id="b9a63-168">Microsoft Visual C++ Yeniden Dağıtılabilir</span><span class="sxs-lookup"><span data-stu-id="b9a63-168">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="b9a63-169">(Performans sayaçlarını etkinleştirir.)</span><span class="sxs-lookup"><span data-stu-id="b9a63-169">(This enables performance counters.)</span></span>

## <a name="exceptions-and-request-failures"></a><span data-ttu-id="b9a63-170">Özel durumlar ve istek hataları</span><span class="sxs-lookup"><span data-stu-id="b9a63-170">Exceptions and request failures</span></span>
<span data-ttu-id="b9a63-171">İşlenmeyen özel durumlar otomatik olarak toplanır:</span><span class="sxs-lookup"><span data-stu-id="b9a63-171">Unhandled exceptions are automatically collected:</span></span>

![](./media/app-insights-java-eclipse/21-exceptions.png)

<span data-ttu-id="b9a63-172">Diğer özel durumlar hakkında veri toplamak için iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="b9a63-172">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="b9a63-173">[Kodunuzda TrackException çağrıları ekleme](app-insights-api-custom-events-metrics.md#trackexception).</span><span class="sxs-lookup"><span data-stu-id="b9a63-173">[Insert calls to TrackException in your code](app-insights-api-custom-events-metrics.md#trackexception).</span></span>
* <span data-ttu-id="b9a63-174">[Sunucunuza Java Agent yükleme](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="b9a63-174">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="b9a63-175">İzlemek istediğiniz yöntemleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="b9a63-175">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="b9a63-176">Yöntem çağrılarını ve dış bağımlılıkları izleme</span><span class="sxs-lookup"><span data-stu-id="b9a63-176">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="b9a63-177">Zamanlama verileriyle JDBC üzerinden yapılan belirli dahili yöntemleri ve çağrıları kaydetmek için [Java Agent yükleme](app-insights-java-agent.md) işlemini gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b9a63-177">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="b9a63-178">Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="b9a63-178">Performance counters</span></span>
<span data-ttu-id="b9a63-179">Genel Bakış dikey penceresini aşağı kaydırarak ve tıklayın **sunucuları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="b9a63-179">On your Overview blade, scroll down and click the  **Servers** tile.</span></span> <span data-ttu-id="b9a63-180">Bir dizi performans sayacı göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b9a63-180">You'll see a range of performance counters.</span></span>

![Sunucular bölmesi tıklatın aşağı kaydırın](./media/app-insights-java-eclipse/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="b9a63-182">Performans sayacı koleksiyonunu özelleştirme</span><span class="sxs-lookup"><span data-stu-id="b9a63-182">Customize performance counter collection</span></span>
<span data-ttu-id="b9a63-183">Standart performans sayaçları dizisinin koleksiyonunu devre dışı bırakmak için aşağıdaki kodu ApplicationInsights.xml dosyasının kök düğümü altına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b9a63-183">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML

    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="b9a63-184">Ek performans sayaçlarını toplama</span><span class="sxs-lookup"><span data-stu-id="b9a63-184">Collect additional performance counters</span></span>
<span data-ttu-id="b9a63-185">Toplanacak ek performans sayaçları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9a63-185">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="b9a63-186">JMX sayaçları (Java Sanal Makinesi tarafından gösterilen)</span><span class="sxs-lookup"><span data-stu-id="b9a63-186">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML

    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="b9a63-187">`displayName` – Application Insights portalında görüntülenen ad.</span><span class="sxs-lookup"><span data-stu-id="b9a63-187">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="b9a63-188">`objectName` – JMX nesne adı.</span><span class="sxs-lookup"><span data-stu-id="b9a63-188">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="b9a63-189">`attribute` – Getirilecek JMX nesne adının özniteliği</span><span class="sxs-lookup"><span data-stu-id="b9a63-189">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="b9a63-190">`type` (isteğe bağlı) - JMX nesnenin öznitelik türü:</span><span class="sxs-lookup"><span data-stu-id="b9a63-190">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="b9a63-191">Varsayılan: int veya long gibi basit bir tür.</span><span class="sxs-lookup"><span data-stu-id="b9a63-191">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="b9a63-192">`composite`: performans sayacı verileri 'Attribute.Data' biçimindedir</span><span class="sxs-lookup"><span data-stu-id="b9a63-192">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="b9a63-193">`tabular`: performans sayacı verileri tablo satırı biçimindedir</span><span class="sxs-lookup"><span data-stu-id="b9a63-193">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="b9a63-194">Windows performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="b9a63-194">Windows performance counters</span></span>
<span data-ttu-id="b9a63-195">Her [Windows performans sayacı](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) bir kategorinin üyesidir (alanın bir sınıf üyesi olması gibi).</span><span class="sxs-lookup"><span data-stu-id="b9a63-195">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="b9a63-196">Kategoriler genel olabileceği gibi numaralı veya adlı örneklere de sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="b9a63-196">Categories can either be global, or can have numbered or named instances.</span></span>

```XML

    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="b9a63-197">displayName – Application Insights portalında görüntülenen ad.</span><span class="sxs-lookup"><span data-stu-id="b9a63-197">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="b9a63-198">categoryName – Bu performans sayacıyla ilişkili performans sayacı kategorisi (performans nesnesi).</span><span class="sxs-lookup"><span data-stu-id="b9a63-198">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="b9a63-199">counterName – Performans sayacının adı.</span><span class="sxs-lookup"><span data-stu-id="b9a63-199">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="b9a63-200">instanceName – Performans sayacı kategorisi örneğinin adı veya kategoride tek örnek varsa boş bir dize ("").</span><span class="sxs-lookup"><span data-stu-id="b9a63-200">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="b9a63-201">categoryName adı Process olursa ve uygulamanızın çalıştığı geçerli JVM işleminden performans sayacını toplamak istiyorsanız `"__SELF__"` öğesini belirtin.</span><span class="sxs-lookup"><span data-stu-id="b9a63-201">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="b9a63-202">Özel ölçümleriniz [Ölçüm Gezgini][metrics]'nde olduğundan performans sayaçlarınız görünürdür.</span><span class="sxs-lookup"><span data-stu-id="b9a63-202">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="b9a63-203">Unix Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="b9a63-203">Unix performance counters</span></span>
* <span data-ttu-id="b9a63-204">Çok çeşitli sistem ve ağ verisi almak için [Application Insights eklentisiyle collectd yükleyin](app-insights-java-collectd.md).</span><span class="sxs-lookup"><span data-stu-id="b9a63-204">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="b9a63-205">Kullanılabilirlik web testleri</span><span class="sxs-lookup"><span data-stu-id="b9a63-205">Availability web tests</span></span>
<span data-ttu-id="b9a63-206">Kullanıma hazır ve düzgün yanıt verdiğini denetlemek için Application Insights belirli aralıklarla web sitenizi test edebilir.</span><span class="sxs-lookup"><span data-stu-id="b9a63-206">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="b9a63-207">[Ayarlamak için][availability], kullanılabilirlik tıklattığınızdan aşağı kaydırın.</span><span class="sxs-lookup"><span data-stu-id="b9a63-207">[To set up][availability], scroll down to click Availability.</span></span>

![Aşağı kaydırıp, Kullanılabilirlik’e ve Web testi ekle’ye tıklama](./media/app-insights-java-eclipse/31-config-web-test.png)

<span data-ttu-id="b9a63-209">Yanıt süreleri grafiklerine ek olarak, siteniz devre dışı kalırsa e-posta bildirimleri de alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b9a63-209">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Web testi örneği](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

<span data-ttu-id="b9a63-211">[Kullanılabilirlik web testleri hakkında daha fazla bilgi edinin.][availability]</span><span class="sxs-lookup"><span data-stu-id="b9a63-211">[Learn more about availability web tests.][availability]</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="b9a63-212">Tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="b9a63-212">Diagnostic logs</span></span>
<span data-ttu-id="b9a63-213">Logback veya Log4J kullanıyorsanız (1.2 sürümü veya v2.0) için izlemeyi, izleme günlüklerinizi uygulama burada keşfedin ve bunlar üzerinde arama Öngörüler otomatik olarak gönderilen sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="b9a63-213">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

<span data-ttu-id="b9a63-214">[Tanılama günlükleri hakkında daha fazla bilgi edinin][javalogs]</span><span class="sxs-lookup"><span data-stu-id="b9a63-214">[Learn more about diagnostic logs][javalogs]</span></span>

## <a name="custom-telemetry"></a><span data-ttu-id="b9a63-215">Özel telemetri</span><span class="sxs-lookup"><span data-stu-id="b9a63-215">Custom telemetry</span></span>
<span data-ttu-id="b9a63-216">Java web uygulamanızdaki kullanıcıların ne ile yaptıklarını bulmak için veya sorunlarını tanılamaya yardımcı olmak için birkaç satır kod ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b9a63-216">Insert a few lines of code in your Java web application to find out what users are doing with it or to help diagnose problems.</span></span>

<span data-ttu-id="b9a63-217">Kod, web sayfası JavaScript hem sunucu tarafı Java de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9a63-217">You can insert code both in web page JavaScript and in the server-side Java.</span></span>

<span data-ttu-id="b9a63-218">[Özel telemetri hakkında bilgi edinin][track]</span><span class="sxs-lookup"><span data-stu-id="b9a63-218">[Learn about custom telemetry][track]</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9a63-219">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b9a63-219">Next steps</span></span>
#### <a name="detect-and-diagnose-issues"></a><span data-ttu-id="b9a63-220">Sorunlarını tanılamak ve Algıla</span><span class="sxs-lookup"><span data-stu-id="b9a63-220">Detect and diagnose issues</span></span>
* <span data-ttu-id="b9a63-221">[Web istemcisi telemetrisini ekleyin] [ usage] performans telemetrisini web istemcisinde almanın.</span><span class="sxs-lookup"><span data-stu-id="b9a63-221">[Add web client telemetry][usage] to get performance telemetry from the web client.</span></span>
* <span data-ttu-id="b9a63-222">Uygulamanızın canlı ve duyarlı kaldığından emin olmak için [web testleri oluşturun][availability].</span><span class="sxs-lookup"><span data-stu-id="b9a63-222">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>
* <span data-ttu-id="b9a63-223">Sorunların tanımlanması için [Olayları ve günlükleri arayın][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="b9a63-223">[Search events and logs][diagnostic] to help diagnose problems.</span></span>
* <span data-ttu-id="b9a63-224">[Log4J veya Logback izlemelerini yakalama][javalogs]</span><span class="sxs-lookup"><span data-stu-id="b9a63-224">[Capture Log4J or Logback traces][javalogs]</span></span>

#### <a name="track-usage"></a><span data-ttu-id="b9a63-225">Kullanımı İzleme</span><span class="sxs-lookup"><span data-stu-id="b9a63-225">Track usage</span></span>
* <span data-ttu-id="b9a63-226">[Web istemcisi telemetrisini ekleyin] [ usage] İzleyici sayfa görünümleri ve temel kullanıcı ölçümleri.</span><span class="sxs-lookup"><span data-stu-id="b9a63-226">[Add web client telemetry][usage] to monitor page views and basic user metrics.</span></span>
* <span data-ttu-id="b9a63-227">[Özel olayları ve ölçümleri izleme](app-insights-web-track-usage.md) nasıl uygulamanız, hem istemci ve sunucu kullanıldığı hakkında bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="b9a63-227">[Track custom events and metrics](app-insights-web-track-usage.md) to learn about how your application is used, both at the client and the server.</span></span>

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
