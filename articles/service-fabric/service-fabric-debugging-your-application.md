---
title: "aaaDebug Visual Studio uygulamanızda | Microsoft Docs"
description: "Merhaba güvenilirliğini ve performansını hizmetlerinizi geliştirmek ve bunları Visual Studio'da bir yerel geliştirme kümede hata ayıklama tarafından geliştirin."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a><span data-ttu-id="1c21b-103">Service Fabric uygulamanızı Visual Studio kullanarak hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="1c21b-103">Debug your Service Fabric application by using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c21b-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="1c21b-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="1c21b-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="1c21b-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a><span data-ttu-id="1c21b-106">Yerel bir Service Fabric uygulama hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="1c21b-106">Debug a local Service Fabric application</span></span>
<span data-ttu-id="1c21b-107">Saat ve para dağıtma ve yerel bilgisayar geliştirme küme Azure Service Fabric uygulamanızda hata ayıklama kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c21b-107">You can save time and money by deploying and debugging your Azure Service Fabric application in a local computer development cluster.</span></span> <span data-ttu-id="1c21b-108">Visual Studio 2017 veya Visual Studio 2015 hello uygulama toohello yerel küme dağıtabilir ve uygulamanızın hello hata ayıklayıcı tooall örnekleri otomatik olarak bağlan.</span><span class="sxs-lookup"><span data-stu-id="1c21b-108">Visual Studio 2017 or Visual Studio 2015 can deploy hello application toohello local cluster and automatically connect hello debugger tooall instances of your application.</span></span>

1. <span data-ttu-id="1c21b-109">Merhaba adımları izleyerek yerel bir geliştirme kümesi Başlat [, Service Fabric geliştirme ortamını ayarlama](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1c21b-109">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started.md).</span></span>
2. <span data-ttu-id="1c21b-110">Tuşuna **F5** veya **hata ayıklama** > **hata ayıklamayı Başlat**.</span><span class="sxs-lookup"><span data-stu-id="1c21b-110">Press **F5** or click **Debug** > **Start Debugging**.</span></span>
   
    ![Bir uygulamanın hata ayıklamayı Başlat][startdebugging]
3. <span data-ttu-id="1c21b-112">Kesme kodu ve adım hello uygulaması aracılığıyla hello komutlarda tıklayarak **hata ayıklama** menüsü.</span><span class="sxs-lookup"><span data-stu-id="1c21b-112">Set breakpoints in your code and step through hello application by clicking commands in hello **Debug** menu.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1c21b-113">Visual Studio uygulamanızı tooall örneklerini ekler.</span><span class="sxs-lookup"><span data-stu-id="1c21b-113">Visual Studio attaches tooall instances of your application.</span></span> <span data-ttu-id="1c21b-114">Kod atlama olsa da, kesme noktaları eşzamanlı oturumlarında kaynaklanan birden çok işlemler tarafından isabet.</span><span class="sxs-lookup"><span data-stu-id="1c21b-114">While you're stepping through code, breakpoints may get hit by multiple processes resulting in concurrent sessions.</span></span> <span data-ttu-id="1c21b-115">Bunlar, her kesme hello iş parçacığı kimliği koşullu yaparak veya tanılama olayları kullanarak isabet sonra hello kesme noktaları devre dışı bırakmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="1c21b-115">Try disabling hello breakpoints after they're hit, by making each breakpoint conditional on hello thread ID or by using diagnostic events.</span></span>
   > 
   > 
4. <span data-ttu-id="1c21b-116">Merhaba **tanılama olayları** penceresi gerçek zamanlı olarak tanılama olayları görebilecek şekilde otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="1c21b-116">hello **Diagnostic Events** window will automatically open so you can view diagnostic events in real time.</span></span>
   
    ![Gerçek zamanlı tanılama olaylarını görüntüle][diagnosticevents]
5. <span data-ttu-id="1c21b-118">Merhaba da açabilirsiniz **tanılama olayları** Cloud Explorer penceresinde.</span><span class="sxs-lookup"><span data-stu-id="1c21b-118">You can also open hello **Diagnostic Events** window in Cloud Explorer.</span></span>  <span data-ttu-id="1c21b-119">Altında **Service Fabric**, herhangi bir düğüme sağ tıklayın ve seçin **görünüm akış izlemeleri**.</span><span class="sxs-lookup"><span data-stu-id="1c21b-119">Under **Service Fabric**, right-click any node and choose **View Streaming Traces**.</span></span>
   
    ![Açık hello Tanılama Olayları penceresi][viewdiagnosticevents]
   
    <span data-ttu-id="1c21b-121">İzlemeler tooa belirli hizmeti veya uygulamayı toofilter istiyorsanız, yalnızca belirli hizmet veya uygulama akış izlemeleri etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1c21b-121">If you want toofilter your traces tooa specific service or application, simply enable streaming traces on that specific service or application.</span></span>
6. <span data-ttu-id="1c21b-122">Merhaba Tanılama Olayları otomatik olarak oluşturulan hello görülen **ServiceEventSource.cs** dosya ve uygulama kodundan denir.</span><span class="sxs-lookup"><span data-stu-id="1c21b-122">hello diagnostic events can be seen in hello automatically generated **ServiceEventSource.cs** file and are called from application code.</span></span>
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. <span data-ttu-id="1c21b-123">Merhaba **tanılama olayları** penceresi filtreleme, duraklatma ve gerçek zamanlı olayları inceleniyor destekler.</span><span class="sxs-lookup"><span data-stu-id="1c21b-123">hello **Diagnostic Events** window supports filtering, pausing, and inspecting events in real time.</span></span>  <span data-ttu-id="1c21b-124">Merhaba, hello olay iletisi içeriği de dahil olmak üzere, bir basit bir dize arama filtredir.</span><span class="sxs-lookup"><span data-stu-id="1c21b-124">hello filter is a simple string search of hello event message, including its contents.</span></span>
   
    ![Filtre, duraklatma ve sürdürme veya gerçek zamanlı olayları inceleyin.][diagnosticeventsactions]
8. <span data-ttu-id="1c21b-126">Hata Ayıklama Hizmetleri başka bir uygulama hata ayıklama gibi değildir.</span><span class="sxs-lookup"><span data-stu-id="1c21b-126">Debugging services is like debugging any other application.</span></span> <span data-ttu-id="1c21b-127">Kesme noktaları Visual Studio aracılığıyla kolay hata ayıklamak için normal olarak ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="1c21b-127">You will normally set Breakpoints through Visual Studio for easy debugging.</span></span> <span data-ttu-id="1c21b-128">Güvenilir koleksiyonları birden çok düğümü arasında çoğaltma olsa da, bunlar hala IEnumerable uygulayın.</span><span class="sxs-lookup"><span data-stu-id="1c21b-128">Even though Reliable Collections replicate across multiple nodes, they still implement IEnumerable.</span></span> <span data-ttu-id="1c21b-129">Bu, hello sonuçları görünümü Visual Studio'da toosee hata ayıklarken içine koyduğunuz kullanabileceğiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1c21b-129">This means that you can use hello Results View in Visual Studio while debugging toosee what you've stored inside.</span></span> <span data-ttu-id="1c21b-130">Yalnızca bir kesme noktası kodunuzda herhangi bir yere ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1c21b-130">Simply set a breakpoint anywhere in your code.</span></span>
   
    ![Bir uygulamanın hata ayıklamayı Başlat][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a><span data-ttu-id="1c21b-132">Uzak bir Service Fabric uygulaması hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="1c21b-132">Debug a remote Service Fabric application</span></span>
<span data-ttu-id="1c21b-133">Service Fabric uygulamalarınızı Azure Service Fabric kümesi üzerinde çalıştırıyorsanız, mümkün tooremotely bunlar, doğrudan Visual Studio'dan hata ayıklama.</span><span class="sxs-lookup"><span data-stu-id="1c21b-133">If your Service Fabric applications are running on a Service Fabric cluster in Azure, you are able tooremotely debug these, directly from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="1c21b-134">Merhaba özellik gerektirir [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) ve [.NET 2.9 için Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1c21b-134">hello feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>    
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="1c21b-135">Uzaktan hata ayıklama, geliştirme ve test senaryoları ve üretim ortamlarında çalışan uygulamalar hello hello etkisini nedeniyle kullanılan toobe için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1c21b-135">Remote debugging is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> 
> 

1. <span data-ttu-id="1c21b-136">Tooyour kümesinde gezinmek **Cloud Explorer**seçin ve sağ tıklatıp **etkinleştirmek hata ayıklama**</span><span class="sxs-lookup"><span data-stu-id="1c21b-136">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Debugging**</span></span>
   
    ![Uzaktan hata ayıklamayı etkinleştirme][enableremotedebugging]
   
    <span data-ttu-id="1c21b-138">Bu kapatma hello hata ayıklama uzantısı, küme düğümlerinde uzak etkinleştirme hello işlemini kazandırın yanı ağ yapılandırmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c21b-138">This will kick off hello process of enabling hello remote debugging extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="1c21b-139">Sağ hello küme düğümünde **Cloud Explorer**ve seçin **ekleme hata ayıklayıcı**</span><span class="sxs-lookup"><span data-stu-id="1c21b-139">Right-click hello cluster node in **Cloud Explorer**, and choose **Attach Debugger**</span></span>
   
    ![Hata ayıklayıcıyı Ekle][attachdebugger]
3. <span data-ttu-id="1c21b-141">Merhaba, **tooprocess Attach** iletişim kutusunda, toodebug istediğiniz ve tıklatın hello işlem seçin **Ekle**</span><span class="sxs-lookup"><span data-stu-id="1c21b-141">In hello **Attach tooprocess** dialog, choose hello process you want toodebug, and click **Attach**</span></span>
   
    ![İşlem seçin][chooseprocess]
   
    <span data-ttu-id="1c21b-143">Merhaba adı için tooattach istediğiniz hello işlemi, eşittir hello hizmet projesi derleme adı.</span><span class="sxs-lookup"><span data-stu-id="1c21b-143">hello name of hello process you want tooattach to, equals hello name of your service project assembly name.</span></span>
   
    <span data-ttu-id="1c21b-144">Merhaba hata ayıklayıcı hello işlem çalışan tooall düğümlerini ekleyecek.</span><span class="sxs-lookup"><span data-stu-id="1c21b-144">hello debugger will attach tooall nodes running hello process.</span></span>
   
   * <span data-ttu-id="1c21b-145">Bir durum bilgisi olmayan Hizmetin nerede ayıkladığınız hello durumda da, tüm düğümlerde hello hizmetin tüm örneklerine ait hello hata ayıklama oturumu bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="1c21b-145">In hello case where you are debugging a stateless service, all instances of hello service on all nodes are part of hello debug session.</span></span>
   * <span data-ttu-id="1c21b-146">Durum bilgisi olan hizmet hata ayıklama, yalnızca birincil çoğaltmasını herhangi bir bölümü hello etkin ve bu nedenle hello hata ayıklayıcı tarafından yakalanan olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1c21b-146">If you are debugging a stateful service, only hello primary replica of any partition will be active and therefore caught by hello debugger.</span></span> <span data-ttu-id="1c21b-147">Merhaba birincil çoğaltma hello hata ayıklama oturumu sırasında geçerse, bu çoğaltma hello işlenmesini hello hata ayıklama oturumunun parçası olmaya devam edecektir.</span><span class="sxs-lookup"><span data-stu-id="1c21b-147">If hello primary replica moves during hello debug session, hello processing of that replica will still be part of hello debug session.</span></span>
   * <span data-ttu-id="1c21b-148">Sipariş tooonly catch ilgili bölümleri veya belirli bir hizmeti örneklerini koşullu kesme noktaları tooonly sonu belirli bir bölüm veya örnek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c21b-148">In order tooonly catch relevant partitions or instances of a given service, you can use conditional breakpoints tooonly break a specific partition or instance.</span></span>
     
     ![Koşullu kesme noktası][conditionalbreakpoint]
     
     > [!NOTE]
     > <span data-ttu-id="1c21b-150">Service Fabric kümesi hello birden çok örneği ile hata ayıklama şu anda desteklemiyoruz aynı hizmet yürütülebilir dosya adı.</span><span class="sxs-lookup"><span data-stu-id="1c21b-150">Currently we do not support debugging a Service Fabric cluster with multiple instances of hello same service executable name.</span></span>
     > 
     > 
4. <span data-ttu-id="1c21b-151">Uygulamanızın hatalarını ayıklama tamamladıktan sonra hello uzaktan hata ayıklama uzantısı hello kümede sağ tıklayarak devre dışı bırakabilirsiniz **Cloud Explorer** ve **devre dışı bırakmak hata ayıklama**</span><span class="sxs-lookup"><span data-stu-id="1c21b-151">Once you finish debugging your application, you can disable hello remote debugging extension by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Debugging**</span></span>
   
    ![Uzaktan hata ayıklama devre dışı bırak][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a><span data-ttu-id="1c21b-153">Uzak küme düğümüne izlemeleri akış</span><span class="sxs-lookup"><span data-stu-id="1c21b-153">Streaming traces from a remote cluster node</span></span>
<span data-ttu-id="1c21b-154">Ayrıca, doğrudan bir uzak küme düğümü tooVisual Studio mümkün toostream izlemeleri de değildir.</span><span class="sxs-lookup"><span data-stu-id="1c21b-154">You are also able toostream traces directly from a remote cluster node tooVisual Studio.</span></span> <span data-ttu-id="1c21b-155">Bu özellik toostream ETW İzleme olayları, Service Fabric küme düğümünde üretilen sağlar.</span><span class="sxs-lookup"><span data-stu-id="1c21b-155">This feature allows you toostream ETW trace events, produced on a Service Fabric cluster node.</span></span>

> [!NOTE]
> <span data-ttu-id="1c21b-156">Bu özellik gerektirir [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) ve [.NET 2.9 için Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="1c21b-156">This feature requires [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) and [Azure SDK for .NET 2.9](https://azure.microsoft.com/downloads/).</span></span>
> <span data-ttu-id="1c21b-157">Bu özellik yalnızca Azure üzerinde çalışan kümelerle destekler.</span><span class="sxs-lookup"><span data-stu-id="1c21b-157">This feature only supports clusters running in Azure.</span></span>
> 
> 

<!-- -->
> [!WARNING]
> <span data-ttu-id="1c21b-158">İzlemeler akış geliştirme ve test senaryoları ve üretim ortamlarında çalışan uygulamalar hello hello etkisini nedeniyle kullanılan toobe için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1c21b-158">Streaming traces is meant for dev/test scenarios and not toobe used in production environments, because of hello impact on hello running applications.</span></span>
> <span data-ttu-id="1c21b-159">Bir üretim senaryosunda, Azure Tanılama'yı kullanarak olayları iletme yararlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1c21b-159">In a production scenario, you should rely on forwarding events using Azure Diagnostics.</span></span>
> 
> 

1. <span data-ttu-id="1c21b-160">Tooyour kümesinde gezinmek **Cloud Explorer**seçin ve sağ tıklatıp **akış izlemeleri etkinleştir**</span><span class="sxs-lookup"><span data-stu-id="1c21b-160">Navigate tooyour cluster in **Cloud Explorer**, right-click and choose **Enable Streaming Traces**</span></span>
   
    ![Uzak akış izlemeleri etkinleştir][enablestreamingtraces]
   
    <span data-ttu-id="1c21b-162">Bu, küme düğümlerinde izlemeleri uzantısı akış hello etkinleştirme işleminin hello kapalı kazandırın yanı ağ yapılandırmaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="1c21b-162">This will kick off hello process of enabling hello streaming traces extension on your cluster nodes, as well as required network configurations.</span></span>
2. <span data-ttu-id="1c21b-163">Merhaba genişletin **düğümleri** öğesinde **Cloud Explorer**, toostream izlemeleri istediğiniz ve seçin sağ hello düğümünü **görünüm akış izlemeleri**</span><span class="sxs-lookup"><span data-stu-id="1c21b-163">Expand hello **Nodes** element in **Cloud Explorer**, right-click hello node you want toostream traces from and choose **View Streaming Traces**</span></span>
   
    ![İzlemeler akış uzak görünümü][viewremotestreamingtraces]
   
    <span data-ttu-id="1c21b-165">Toosee izlemeleri istediğiniz sayıda düğümleri için 2. adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="1c21b-165">Repeat step 2 for as many nodes as you want toosee traces from.</span></span> <span data-ttu-id="1c21b-166">Her düğüm akış adanmış bir pencerede gösterir.</span><span class="sxs-lookup"><span data-stu-id="1c21b-166">Each nodes stream will show up in a dedicated window.</span></span>
   
    <span data-ttu-id="1c21b-167">Service Fabric ve hizmetlerinizi tarafından gösterilen mümkün toosee hello izlemeleri sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="1c21b-167">You are now able toosee hello traces emitted by Service Fabric, and your services.</span></span> <span data-ttu-id="1c21b-168">Belirli bir uygulama toofilter hello olayları tooonly Göster istiyorsanız, yalnızca hello hello filtresi hello uygulamanın adını yazın.</span><span class="sxs-lookup"><span data-stu-id="1c21b-168">If you want toofilter hello events tooonly show a specific application, simply type in hello name of hello application in hello filter.</span></span>
   
    ![İzlemeler akış görüntüleme][viewingstreamingtraces]
3. <span data-ttu-id="1c21b-170">Akış izlemeleri kümenizden tamamladıktan sonra uzak akış izlemeleri hello kümede sağ tıklayarak devre dışı bırakabilirsiniz **Cloud Explorer** ve **akış izlemelerini devre dışı bırak**</span><span class="sxs-lookup"><span data-stu-id="1c21b-170">Once you are done streaming traces from your cluster, you can disable remote streaming traces, by right-clicking hello cluster in **Cloud Explorer** and choose **Disable Streaming Traces**</span></span>
   
    ![Uzak akış izlemelerini devre dışı bırak][disablestreamingtraces]

## <a name="next-steps"></a><span data-ttu-id="1c21b-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1c21b-172">Next steps</span></span>
* <span data-ttu-id="1c21b-173">[Service Fabric hizmeti test](service-fabric-testability-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1c21b-173">[Test a Service Fabric service](service-fabric-testability-overview.md).</span></span>
* <span data-ttu-id="1c21b-174">[Visual Studio'da, Service Fabric uygulamaları yönetmek](service-fabric-manage-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="1c21b-174">[Manage your Service Fabric applications in Visual Studio](service-fabric-manage-application-in-visual-studio.md).</span></span>

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
