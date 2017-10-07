---
title: Azure Visual Studio'da kod aaaOptimizing | Microsoft Docs
description: "Kodunuzu daha sağlam ve çökmelerin yapmak en iyi duruma getirme araçları Visual Studio hakkında nasıl Azure Kod yardımcı öğrenin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="97a5d-103">Azure kodunuzu iyileştirme</span><span class="sxs-lookup"><span data-stu-id="97a5d-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="97a5d-104">Microsoft Azure kullanan uygulamalar programlama olduğunda toohelp izlediğiniz bazı kodlama uygulamalarını uygulama ölçeklenebilirlik, davranış ve bulut ortamında bulunan performans sorunları kaçının.</span><span class="sxs-lookup"><span data-stu-id="97a5d-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow toohelp avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="97a5d-105">Microsoft, tanır ve bu sık karşılaşılan sorunları çeşitli tanımlar ve bunları çözmenize yardımcı olacak bir Azure Kod Analizi aracı sağlar.</span><span class="sxs-lookup"><span data-stu-id="97a5d-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="97a5d-106">Visual Studio'da NuGet aracılığıyla hello aracı yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97a5d-106">You can download hello tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="97a5d-107">Azure Kod Analizi kuralları</span><span class="sxs-lookup"><span data-stu-id="97a5d-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="97a5d-108">Hello Azure Kod Analizi aracı tooautomatically bayrak Azure kodunuzu performansı etkileyen bilinen sorunlar bulduğunda kuralları aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="97a5d-108">hello Azure Code Analysis tool uses hello following rules tooautomatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="97a5d-109">Sorunları görünen uyarıları olarak algılanan veya derleyici hataları.</span><span class="sxs-lookup"><span data-stu-id="97a5d-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="97a5d-110">Kod düzeltmeleri veya önerileri tooresolve hello uyarı veya hata genellikle sağlanan ampul simgesi üzerinden.</span><span class="sxs-lookup"><span data-stu-id="97a5d-110">Code fixes or suggestions tooresolve hello warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="97a5d-111">Varsayılan (işlemdeki) oturum durumu modunu kullanmaktan kaçının</span><span class="sxs-lookup"><span data-stu-id="97a5d-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="97a5d-112">Kimlik</span><span class="sxs-lookup"><span data-stu-id="97a5d-112">ID</span></span>
<span data-ttu-id="97a5d-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="97a5d-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="97a5d-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97a5d-114">Description</span></span>
<span data-ttu-id="97a5d-115">Bulut uygulamaları için hello varsayılan (işlemdeki) oturum durumu modunu kullanıyorsanız, oturum durumu kaybedebilir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-115">If you use hello default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="97a5d-116">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="97a5d-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="97a5d-117">Neden</span><span class="sxs-lookup"><span data-stu-id="97a5d-117">Reason</span></span>
<span data-ttu-id="97a5d-118">Varsayılan olarak, işlem içi hello web.config dosyasında belirtilen hello oturum durumu modu.</span><span class="sxs-lookup"><span data-stu-id="97a5d-118">By default, hello session state mode specified in hello web.config file is in-process.</span></span> <span data-ttu-id="97a5d-119">Ayrıca, hello yapılandırma dosyasında belirtilen giriş varsa, hello oturum durumu modu tooin işlem varsayar.</span><span class="sxs-lookup"><span data-stu-id="97a5d-119">Also, if no entry specified in hello configuration file, hello Session State mode defaults tooin-process.</span></span> <span data-ttu-id="97a5d-120">Merhaba işlemdeki modu oturum durumu hello web sunucusu üzerindeki bellekte depolar.</span><span class="sxs-lookup"><span data-stu-id="97a5d-120">hello in-process mode stores session state in memory on hello web server.</span></span> <span data-ttu-id="97a5d-121">Örneği yeniden ya da yeni bir örneğini Yük Dengeleme veya yük devretme desteği için kullanılan bellek hello web sunucusunda depolanan hello oturum durumu kaydedilmez.</span><span class="sxs-lookup"><span data-stu-id="97a5d-121">When an instance is restarted or a new instance is used for load balancing or failover support, hello session state stored in memory on hello web server isn’t saved.</span></span> <span data-ttu-id="97a5d-122">Bu durum ölçeklenebilir hello bulutta engeller Merhaba uygulaması engeller.</span><span class="sxs-lookup"><span data-stu-id="97a5d-122">This situation prevents hello application from being scalable on hello cloud.</span></span>

<span data-ttu-id="97a5d-123">ASP.NET oturum durumu için oturum durumu verilerini birkaç farklı depolama seçeneklerini destekler: InProc, StateServer, SQLServer, özel ve kapalı.</span><span class="sxs-lookup"><span data-stu-id="97a5d-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="97a5d-124">Özel mod toohost veri bir dış oturum durumu deposunda gibi kullanmanız önerilir [Redis için Azure oturum durumu sağlayıcısı](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="97a5d-124">It’s recommended that you use Custom mode toohost data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="97a5d-125">Çözüm</span><span class="sxs-lookup"><span data-stu-id="97a5d-125">Solution</span></span>
<span data-ttu-id="97a5d-126">Bir önerilen bir yönetilen önbellek hizmeti toostore oturum durumu çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="97a5d-126">One recommended solution is toostore session state on a managed cache service.</span></span> <span data-ttu-id="97a5d-127">Bilgi nasıl toouse [Redis için Azure oturum durumu sağlayıcısı](http://go.microsoft.com/fwlink/?LinkId=401521) toostore, oturum durumu.</span><span class="sxs-lookup"><span data-stu-id="97a5d-127">Learn how toouse [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore your session state.</span></span> <span data-ttu-id="97a5d-128">Uygulamanızı hello bulut üzerinde ölçeklenebilir diğer yerler tooensure de deposu oturum durumu.</span><span class="sxs-lookup"><span data-stu-id="97a5d-128">You can also store session state in other places tooensure your application is scalable on hello cloud.</span></span> <span data-ttu-id="97a5d-129">Lütfen okuyun alternatif çözümleri hakkında daha fazla toolearn [oturum durumu modu](https://msdn.microsoft.com/library/ms178586).</span><span class="sxs-lookup"><span data-stu-id="97a5d-129">toolearn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="97a5d-130">Run yöntemini zaman uyumsuz olmamalıdır</span><span class="sxs-lookup"><span data-stu-id="97a5d-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="97a5d-131">Kimlik</span><span class="sxs-lookup"><span data-stu-id="97a5d-131">ID</span></span>
<span data-ttu-id="97a5d-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="97a5d-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="97a5d-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97a5d-133">Description</span></span>
<span data-ttu-id="97a5d-134">Zaman uyumsuz yöntemleri oluşturun (gibi [await](https://msdn.microsoft.com/library/hh156528.aspx)) hello dışında [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi ve çağrı hello zaman uyumsuz yöntemleri [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="97a5d-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call hello async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="97a5d-135">Merhaba bildirme [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi zaman uyumsuz olarak hello çalışan rolü tooenter bir yeniden başlatma döngü neden olur.</span><span class="sxs-lookup"><span data-stu-id="97a5d-135">Declaring hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes hello worker role tooenter a restart loop.</span></span>

<span data-ttu-id="97a5d-136">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="97a5d-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="97a5d-137">Neden</span><span class="sxs-lookup"><span data-stu-id="97a5d-137">Reason</span></span>
<span data-ttu-id="97a5d-138">Merhaba içinde zaman uyumsuz yöntemleri çağırma [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi hello bulut hizmeti çalışma zamanı toorecycle hello çalışan rolü neden olur.</span><span class="sxs-lookup"><span data-stu-id="97a5d-138">Calling async methods inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello cloud service runtime toorecycle hello worker role.</span></span> <span data-ttu-id="97a5d-139">Çalışan rolü başladığında, tüm program yürütme hello içinde gerçekleşir [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="97a5d-139">When a worker role starts, all program execution takes place inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="97a5d-140">Mevcut hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi hello çalışan rolü toorestart neden olur.</span><span class="sxs-lookup"><span data-stu-id="97a5d-140">Exiting hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello worker role toorestart.</span></span> <span data-ttu-id="97a5d-141">Merhaba async yöntemi Hello çalışan rolü çalışma zamanı geldiğinde, tüm işlemleri hello async yöntemi sonra gönderir ve ardından döndürür.</span><span class="sxs-lookup"><span data-stu-id="97a5d-141">When hello worker role runtime hits hello async method, it dispatches all operations after hello async method and then returns.</span></span> <span data-ttu-id="97a5d-142">Bu hello çalışan rolü tooexit hello neden [ [ [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi ve yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="97a5d-142">This causes hello worker role tooexit from hello [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="97a5d-143">Merhaba sonraki yinelemede yürütme, hello çalışan rolü yeniden hello async yöntemi ve hello çalışan rolü toorecycle de yeniden neden yeniden kadardır.</span><span class="sxs-lookup"><span data-stu-id="97a5d-143">In hello next iteration of execution, hello worker role hits hello async method again and restarts, causing hello worker role toorecycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="97a5d-144">Çözüm</span><span class="sxs-lookup"><span data-stu-id="97a5d-144">Solution</span></span>
<span data-ttu-id="97a5d-145">Merhaba dışında tüm zaman uyumsuz işlemler yerleştirin [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="97a5d-145">Place all async operations outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="97a5d-146">Ardından, yeniden hello zaman uyumsuz yöntemden'ı çağırın hello içinde [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) RunAsync () .wait gibi yöntemi.</span><span class="sxs-lookup"><span data-stu-id="97a5d-146">Then, call hello refactored async method from inside hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="97a5d-147">Hello Azure Kod Analizi aracı, bu sorunu gidermenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-147">hello Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="97a5d-148">Aşağıdaki kod parçacığını hello hello kod düzeltme bu sorunun gösterir:</span><span class="sxs-lookup"><span data-stu-id="97a5d-148">hello following code snippet demonstrates hello code fix for this issue:</span></span>

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="97a5d-149">Hizmet veri yolu paylaşılan erişim imzası kimlik doğrulamasını kullan</span><span class="sxs-lookup"><span data-stu-id="97a5d-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="97a5d-150">Kimlik</span><span class="sxs-lookup"><span data-stu-id="97a5d-150">ID</span></span>
<span data-ttu-id="97a5d-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="97a5d-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="97a5d-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97a5d-152">Description</span></span>
<span data-ttu-id="97a5d-153">Paylaşılan erişim imzası (SAS) kimlik doğrulaması için kullanın.</span><span class="sxs-lookup"><span data-stu-id="97a5d-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="97a5d-154">Erişim denetimi Hizmeti'nden (ACS) hizmet veri yolu kimlik doğrulaması için kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="97a5d-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="97a5d-155">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="97a5d-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="97a5d-156">Neden</span><span class="sxs-lookup"><span data-stu-id="97a5d-156">Reason</span></span>
<span data-ttu-id="97a5d-157">Gelişmiş güvenlik için Azure Active Directory ACS kimlik doğrulaması SAS kimlik doğrulaması ile değiştirmektir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="97a5d-158">Bkz: [Azure Active Directory olduğu hello ACS gelecekteki](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) hello geçiş planı hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="97a5d-158">See [Azure Active Directory is hello future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on hello transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="97a5d-159">Çözüm</span><span class="sxs-lookup"><span data-stu-id="97a5d-159">Solution</span></span>
<span data-ttu-id="97a5d-160">SAS kimlik doğrulaması uygulamalarınızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="97a5d-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="97a5d-161">Aşağıdaki örnek hello nasıl toouse var olan bir SAS belirteci tooaccess bir hizmet veri yolu ad alanı veya varlık gösterir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-161">hello following example shows how toouse an existing SAS token tooaccess a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="97a5d-162">Merhaba aşağıdaki konularda daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="97a5d-162">See hello following topics for more information.</span></span>

* <span data-ttu-id="97a5d-163">Genel bir bakış için bkz: [paylaşılan erişim imzası kimlik doğrulaması Service Bus ile](https://msdn.microsoft.com/library/dn170477.aspx)</span><span class="sxs-lookup"><span data-stu-id="97a5d-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="97a5d-164">Nasıl toouse Service Bus ile paylaşılan erişim imzası kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="97a5d-164">How toouse Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="97a5d-165">Örnek proje için bkz: [hizmet veri yolu abonelikleri ile kullanarak paylaşılan erişim imzası (SAS) kimlik doğrulaması](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span><span class="sxs-lookup"><span data-stu-id="97a5d-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a><span data-ttu-id="97a5d-166">"Döngü alırsınız" Onmessageoptions yöntemi tooavoid kullanmayı düşünün</span><span class="sxs-lookup"><span data-stu-id="97a5d-166">Consider using OnMessage method tooavoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="97a5d-167">Kimlik</span><span class="sxs-lookup"><span data-stu-id="97a5d-167">ID</span></span>
<span data-ttu-id="97a5d-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="97a5d-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="97a5d-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97a5d-169">Description</span></span>
<span data-ttu-id="97a5d-170">bir "alma döngü," giderek tooavoid arama hello **Onmessageoptions** yöntemdir arama hello daha iletileri almak için daha iyi bir çözüm **alma** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="97a5d-170">tooavoid going into a "receive loop," calling hello **OnMessage** method is a better solution for receiving messages than calling hello **Receive** method.</span></span> <span data-ttu-id="97a5d-171">Ancak, hello kullanmanız gerekiyorsa **alma** yöntemi ve varsayılan olmayan sunucu bekleme süresini belirtin, hello sunucu bekleme süresi bir dakikadan fazla olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="97a5d-171">However, if you must use hello **Receive** method, and you specify a non-default server wait time, make sure hello server wait time is more than one minute.</span></span>

<span data-ttu-id="97a5d-172">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="97a5d-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="97a5d-173">Neden</span><span class="sxs-lookup"><span data-stu-id="97a5d-173">Reason</span></span>
<span data-ttu-id="97a5d-174">Çağrılırken **Onmessageoptions**, hello istemci sürekli hello sıra ya da abonelik yokladığı bir dahili ileti Pompalama başlatır.</span><span class="sxs-lookup"><span data-stu-id="97a5d-174">When calling **OnMessage**, hello client starts an internal message pump that constantly polls hello queue or subscription.</span></span> <span data-ttu-id="97a5d-175">Bu ileti Pompalama tooreceive iletileri bir çağrı sorunları sonsuz bir döngüde içerir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-175">This message pump contains an infinite loop that issues a call tooreceive messages.</span></span> <span data-ttu-id="97a5d-176">Merhaba çağrısı zaman aşımına uğrarsa, yeni bir çağrı verir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-176">If hello call times out, it issues a new call.</span></span> <span data-ttu-id="97a5d-177">Merhaba zaman aşımı aralığı hello hello değeri tarafından belirlenir [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) hello özelliğinin [Eventhubclient](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)kullanılan.</span><span class="sxs-lookup"><span data-stu-id="97a5d-177">hello timeout interval is determined by hello value of hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="97a5d-178">Merhaba kullanmanın avantajı **Onmessageoptions** çok karşılaştırıldığında**alma** kullanıcılar yoklamak için iletileri, özel durumları işleme, birden fazla ileti paralel işleme ve tamamlamak hello toomanually gerekmemesidir iletileri.</span><span class="sxs-lookup"><span data-stu-id="97a5d-178">hello advantage of using **OnMessage** compared too**Receive** is that users don’t have toomanually poll for messages, handle exceptions, process multiple messages in parallel, and complete hello messages.</span></span>

<span data-ttu-id="97a5d-179">Çağırırsanız **alma** varsayılan değeri kullanmadan emin hello olması *ServerWaitTime* bir dakikadan fazla bir değerdir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-179">If you call **Receive** without using its default value, be sure hello *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="97a5d-180">Ayarı *ServerWaitTime* toomore bir dakika daha zaman aşımına uğruyor uygulamadan selamlama iletisine tam olarak alınan önce hello sunucu engeller.</span><span class="sxs-lookup"><span data-stu-id="97a5d-180">Setting *ServerWaitTime* toomore than one minute prevents hello server from timing out before hello message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="97a5d-181">Çözüm</span><span class="sxs-lookup"><span data-stu-id="97a5d-181">Solution</span></span>
<span data-ttu-id="97a5d-182">Önerilen kullanımlar için kod örnekleri aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="97a5d-182">Please see hello following code examples for recommended usages.</span></span> <span data-ttu-id="97a5d-183">Daha fazla ayrıntı için bkz: [QueueClient.OnMessage yöntemi (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)ve [QueueClient.Receive yöntemi (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span><span class="sxs-lookup"><span data-stu-id="97a5d-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="97a5d-184">hello Azure Mesajlaşma altyapısı tooimprove hello performansını görmek hello tasarım deseni [zaman uyumsuz Mesajlaşma Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="97a5d-184">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="97a5d-185">Merhaba kullanmaya ilişkin bir örnek verilmiştir **Onmessageoptions** tooreceive iletileri.</span><span class="sxs-lookup"><span data-stu-id="97a5d-185">hello following is an example of using **OnMessage** tooreceive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

<span data-ttu-id="97a5d-186">Merhaba kullanmaya ilişkin bir örnek verilmiştir **alma** hello varsayılan sunucusuyla bekleme süresi.</span><span class="sxs-lookup"><span data-stu-id="97a5d-186">hello following is an example of using **Receive** with hello default server wait time.</span></span>

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

<span data-ttu-id="97a5d-187">Merhaba kullanmaya ilişkin bir örnek verilmiştir **alma** varsayılan olmayan sunucusuyla bekleme süresi.</span><span class="sxs-lookup"><span data-stu-id="97a5d-187">hello following is an example of using **Receive** with a non-default server wait time.</span></span>

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="97a5d-188">Zaman uyumsuz hizmet veri yolu yöntemleri kullanmayı düşünün</span><span class="sxs-lookup"><span data-stu-id="97a5d-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="97a5d-189">Kimlik</span><span class="sxs-lookup"><span data-stu-id="97a5d-189">ID</span></span>
<span data-ttu-id="97a5d-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="97a5d-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="97a5d-191">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97a5d-191">Description</span></span>
<span data-ttu-id="97a5d-192">Zaman uyumsuz hizmet veri yolu yöntemleri tooimprove performans aracılı Mesajlaşma ile kullanın.</span><span class="sxs-lookup"><span data-stu-id="97a5d-192">Use asynchronous Service Bus methods tooimprove performance with brokered messaging.</span></span>

<span data-ttu-id="97a5d-193">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="97a5d-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="97a5d-194">Neden</span><span class="sxs-lookup"><span data-stu-id="97a5d-194">Reason</span></span>
<span data-ttu-id="97a5d-195">Her çağrısının hello ana iş parçacığı engellemesini devre dışı bırakmak için zaman uyumsuz yöntemleri kullanarak uygulama programı eşzamanlılık sağlar.</span><span class="sxs-lookup"><span data-stu-id="97a5d-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block hello main thread.</span></span> <span data-ttu-id="97a5d-196">Service Bus Mesajlaşma yöntemleri, bir işlemi gerçekleştirilirken kullanırken (gönderme, alma, silme, vb.) zaman alır.</span><span class="sxs-lookup"><span data-stu-id="97a5d-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="97a5d-197">Bu süre hello işlemi hello işlenmesini hello Service Bus hizmeti tarafından hello istek ve hello yanıt toohello gecikme ekleme içerir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-197">This time includes hello processing of hello operation by hello Service Bus service in addition toohello latency of hello request and hello reply.</span></span> <span data-ttu-id="97a5d-198">saat başına işlemlerinin tooincrease hello sayısı, işlemler aynı anda yürütmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-198">tooincrease hello number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="97a5d-199">Daha fazla bilgi için lütfen çok başvurun[performans iyileştirmeleri kullanarak Service Bus aracılı Mesajlaşma için en iyi uygulamaları](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span><span class="sxs-lookup"><span data-stu-id="97a5d-199">For more information please refer too[Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="97a5d-200">Çözüm</span><span class="sxs-lookup"><span data-stu-id="97a5d-200">Solution</span></span>
<span data-ttu-id="97a5d-201">Bkz: [QueueClient sınıfı (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) ne zaman uyumsuz yöntem toouse hello önerilen hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="97a5d-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how toouse hello recommended asynchronous method.</span></span>

<span data-ttu-id="97a5d-202">hello Azure Mesajlaşma altyapısı tooimprove hello performansını görmek hello tasarım deseni [zaman uyumsuz Mesajlaşma Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="97a5d-202">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="97a5d-203">Bölümleme Service Bus kuyrukları ve konuları göz önünde bulundurun</span><span class="sxs-lookup"><span data-stu-id="97a5d-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="97a5d-204">Kimlik</span><span class="sxs-lookup"><span data-stu-id="97a5d-204">ID</span></span>
<span data-ttu-id="97a5d-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="97a5d-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="97a5d-206">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97a5d-206">Description</span></span>
<span data-ttu-id="97a5d-207">Bölüm Service Bus kuyrukları ve konularından Service Bus Mesajlaşma ile daha iyi performans için.</span><span class="sxs-lookup"><span data-stu-id="97a5d-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="97a5d-208">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="97a5d-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="97a5d-209">Neden</span><span class="sxs-lookup"><span data-stu-id="97a5d-209">Reason</span></span>
<span data-ttu-id="97a5d-210">Merhaba bölümlenmiş kuyruk veya konu, genel üretilen işi artık tek ileti Aracısı ya da ileti deposu hello performans ile sınırlı olduğundan, Service Bus kuyrukları ve konularından bölümleme performans verimlilik ve hizmet kullanılabilirliğini artırır.</span><span class="sxs-lookup"><span data-stu-id="97a5d-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because hello overall throughput of a partitioned queue or topic is no longer limited by hello performance of a single message broker or messaging store.</span></span> <span data-ttu-id="97a5d-211">Ayrıca, bir Mesajlaşma deposu geçici bir kesinti bölümlenmiş kuyruk veya konu kullanılamaz hale değil.</span><span class="sxs-lookup"><span data-stu-id="97a5d-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="97a5d-212">Daha fazla bilgi için bkz: [Mesajlaşma varlıkları bölümleme](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span><span class="sxs-lookup"><span data-stu-id="97a5d-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="97a5d-213">Çözüm</span><span class="sxs-lookup"><span data-stu-id="97a5d-213">Solution</span></span>
<span data-ttu-id="97a5d-214">kod parçacığı gösterir nasıl aşağıdaki hello Mesajlaşma toopartition.</span><span class="sxs-lookup"><span data-stu-id="97a5d-214">hello following code snippet shows how toopartition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="97a5d-215">Daha fazla bilgi için bkz: [bölümlenmiş Service Bus kuyrukları ve konularından | Microsoft Azure blogu](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) ve hello denetleyin [Microsoft Azure hizmet veri yolu kuyruğu bölümlenmiş](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) örnek.</span><span class="sxs-lookup"><span data-stu-id="97a5d-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out hello [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="97a5d-216">SharedAccessStartTime ayarlı değil</span><span class="sxs-lookup"><span data-stu-id="97a5d-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="97a5d-217">Kimlik</span><span class="sxs-lookup"><span data-stu-id="97a5d-217">ID</span></span>
<span data-ttu-id="97a5d-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="97a5d-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="97a5d-219">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97a5d-219">Description</span></span>
<span data-ttu-id="97a5d-220">SharedAccessStartTimeset toohello tooimmediately hello paylaşılan erişim ilkesi geçerli başlattığınızda yapmaktan kaçınmalısınız.</span><span class="sxs-lookup"><span data-stu-id="97a5d-220">You should avoid using SharedAccessStartTimeset toohello current time tooimmediately start hello Shared Access policy.</span></span> <span data-ttu-id="97a5d-221">Daha sonraki bir zamanda toostart hello paylaşılan erişim ilkesi istiyorsanız, bu özellik yalnızca tooset gerekir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-221">You only need tooset this property if you want toostart hello Shared Access policy at a later time.</span></span>

<span data-ttu-id="97a5d-222">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="97a5d-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="97a5d-223">Neden</span><span class="sxs-lookup"><span data-stu-id="97a5d-223">Reason</span></span>
<span data-ttu-id="97a5d-224">Saati eşitleme veri merkezleri arasında küçük zaman farkı neden olur.</span><span class="sxs-lookup"><span data-stu-id="97a5d-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="97a5d-225">Örneğin, Hello DateTime.Now veya benzer bir yöntem kullanarak geçerli saati hello SAS İlkesi tootake etkisi hemen neden olacak şekilde bir depolama SAS İlkesi ayarı hello başlangıç saati mantıksal olarak düşünün.</span><span class="sxs-lookup"><span data-stu-id="97a5d-225">For example, you would logically think setting hello start time of a storage SAS policy as hello current time by using DateTime.Now or a similar method will cause hello SAS policy tootake effect immediately.</span></span> <span data-ttu-id="97a5d-226">Ancak, veri merkezi zamanlarda biraz daha öncesinde, diğerlerinin hello başlangıç saati olabileceğinden hello hafif saat farklılıklarını veri merkezleri arasında bu sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-226">However, hello slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than hello start time, while others ahead of it.</span></span> <span data-ttu-id="97a5d-227">Sonuç olarak, hello SAS İlkesi hızla (veya hatta hemen) dolabilir hello İlkesi yaşam süresi çok kısa olarak ayarlanmışsa.</span><span class="sxs-lookup"><span data-stu-id="97a5d-227">As a result, hello SAS policy can expire quickly (or even immediately) if hello policy lifetime is set too short.</span></span>

<span data-ttu-id="97a5d-228">Üzerinde Azure storage paylaşılan erişim imzası kullanma konusunda daha fazla yönergeler için bkz: [giriş tablosu SAS (paylaşılan erişim imzası), sıra SAS güncelleştirme tooBlob SAS - Microsoft Azure depolama ekibi blogu - Site ve giriş - MSDN Bloglarında](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="97a5d-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="97a5d-229">Çözüm</span><span class="sxs-lookup"><span data-stu-id="97a5d-229">Solution</span></span>
<span data-ttu-id="97a5d-230">Merhaba paylaşılan erişim ilkesi hello başlangıç saatini ayarlar hello deyimi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="97a5d-230">Remove hello statement that sets hello start time of hello shared access policy.</span></span> <span data-ttu-id="97a5d-231">Hello Azure Kod Analizi aracı bu sorun için düzeltme sağlar.</span><span class="sxs-lookup"><span data-stu-id="97a5d-231">hello Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="97a5d-232">Güvenlik yönetimi hakkında daha fazla bilgi için lütfen bkz hello tasarım deseni [Valet anahtar düzeni](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="97a5d-232">For more information on security management, please see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="97a5d-233">Aşağıdaki kod parçacığını hello hello kod düzeltme bu sorunun gösterir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-233">hello following code snippet demonstrates hello code fix for this issue.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="97a5d-234">Paylaşılan Erişim İlkesi sona erme saati beş dakikadan fazla olmalıdır</span><span class="sxs-lookup"><span data-stu-id="97a5d-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="97a5d-235">Kimlik</span><span class="sxs-lookup"><span data-stu-id="97a5d-235">ID</span></span>
<span data-ttu-id="97a5d-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="97a5d-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="97a5d-237">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97a5d-237">Description</span></span>
<span data-ttu-id="97a5d-238">Beş dakikalık fark kadar tooa koşul "saat eğme." bilinen son farklı konumlardaki veri merkezleri arasında saatleri içinde olabilir</span><span class="sxs-lookup"><span data-stu-id="97a5d-238">There can be as much as a five minute difference in clocks among datacenters at different locations due tooa condition known as "clock skew."</span></span> <span data-ttu-id="97a5d-239">zaman aşımına uğramak gelen tooprevent hello SAS İlkesi belirteci hello sona erme saati toobe beş dakikadan fazla planlanmış daha erken ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="97a5d-239">tooprevent hello SAS policy token from expiring earlier than planned, set hello expiry time toobe more than five minutes.</span></span>

<span data-ttu-id="97a5d-240">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="97a5d-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="97a5d-241">Neden</span><span class="sxs-lookup"><span data-stu-id="97a5d-241">Reason</span></span>
<span data-ttu-id="97a5d-242">Merhaba Dünya farklı konumlardaki veri merkezlerine saati sinyali ile eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="97a5d-242">Datacenters at different locations around hello world synchronize by a clock signal.</span></span> <span data-ttu-id="97a5d-243">Saat sinyal tootravel toodifferent konumları için zaman alır çünkü her şeyin beklendiği gibi eşitlenir ancak farklı coğrafi konumlardaki veri merkezlerine arasındaki zaman farkı olabilir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-243">Because it takes time for clock signal tootravel toodifferent locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="97a5d-244">Bu zaman farkı, saat ve sona erme tarihi hello paylaşılan erişim ilkesi başlangıç aralığı etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-244">This time difference can affect hello Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="97a5d-245">Bu nedenle, tooensure paylaşılan erişim ilke hemen etkili olur, hello başlangıç saati belirtmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="97a5d-245">Therefore, tooensure Shared Access policy takes effect immediately, don’t specify hello start time.</span></span> <span data-ttu-id="97a5d-246">Ayrıca, hello süre 5 dakika tooprevent erken zaman aşımından daha fazla olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="97a5d-246">In addition, make sure hello expiration time is more than 5 minutes tooprevent early timeout.</span></span>

<span data-ttu-id="97a5d-247">Azure depolama alanında paylaşılan erişim imzası kullanma hakkında daha fazla bilgi için bkz: [giriş tablosu SAS (paylaşılan erişim imzası), sıra SAS güncelleştirme tooBlob SAS - Microsoft Azure depolama ekibi blogu - Site ve giriş - MSDN Bloglarında](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="97a5d-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="97a5d-248">Çözüm</span><span class="sxs-lookup"><span data-stu-id="97a5d-248">Solution</span></span>
<span data-ttu-id="97a5d-249">Güvenlik yönetimi hakkında daha fazla bilgi için bkz: hello tasarım deseni [Valet anahtar düzeni](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="97a5d-249">For more information on security management, see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="97a5d-250">Merhaba, paylaşılan erişim ilkesi başlangıç zamanı belirtmeden bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-250">hello following is an example of not specifying a Shared Access policy start time.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="97a5d-251">Merhaba, beş dakikadan uzun bir ilke sona erme süresi ile bir paylaşılan erişim ilkesi başlangıç saati belirten bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-251">hello following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="97a5d-252">Daha fazla bilgi için bkz: [oluşturmak ve paylaşılan erişim imzası kullanmak](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="97a5d-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="97a5d-253">CloudConfigurationManager kullanın</span><span class="sxs-lookup"><span data-stu-id="97a5d-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="97a5d-254">Kimlik</span><span class="sxs-lookup"><span data-stu-id="97a5d-254">ID</span></span>
<span data-ttu-id="97a5d-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="97a5d-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="97a5d-256">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97a5d-256">Description</span></span>
<span data-ttu-id="97a5d-257">Hello kullanarak [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) sınıf projelerde gibi Azure Web sitesine gidin ve Azure mobil hizmetler çalışma zamanı sorunlarına neden olmaz.</span><span class="sxs-lookup"><span data-stu-id="97a5d-257">Using hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="97a5d-258">En iyi uygulama, ancak iyi bir fikir toouse bulut olan[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) tüm Azure bulut uygulamaları için yapılandırmaları yönetme birleşik bir yolu olarak.</span><span class="sxs-lookup"><span data-stu-id="97a5d-258">As a best practice, however, it's a good idea toouse Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="97a5d-259">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="97a5d-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="97a5d-260">Neden</span><span class="sxs-lookup"><span data-stu-id="97a5d-260">Reason</span></span>
<span data-ttu-id="97a5d-261">CloudConfigurationManager hello yapılandırma dosyasını uygun toohello uygulama ortamı okur.</span><span class="sxs-lookup"><span data-stu-id="97a5d-261">CloudConfigurationManager reads hello configuration file appropriate toohello application environment.</span></span>

[<span data-ttu-id="97a5d-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="97a5d-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="97a5d-263">Çözüm</span><span class="sxs-lookup"><span data-stu-id="97a5d-263">Solution</span></span>
<span data-ttu-id="97a5d-264">Kod toouse hello yeniden düzenlemeniz [CloudConfigurationManager sınıfı](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="97a5d-264">Refactor your code toouse hello [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="97a5d-265">Bu sorun için bir kod düzeltme hello Azure Kod Analizi aracı tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="97a5d-265">A code fix for this issue is provided by hello Azure Code Analysis tool.</span></span>

<span data-ttu-id="97a5d-266">Aşağıdaki kod parçacığını hello hello kod düzeltme bu sorunun gösterir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-266">hello following code snippet demonstrates hello code fix for this issue.</span></span> <span data-ttu-id="97a5d-267">Değiştir</span><span class="sxs-lookup"><span data-stu-id="97a5d-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="97a5d-268">İle</span><span class="sxs-lookup"><span data-stu-id="97a5d-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="97a5d-269">Burada, nasıl toostore hello yapılandırma ayarı App.config veya Web.config dosyasındaki bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-269">Here's an example of how toostore hello configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="97a5d-270">Hello ayarları toohello appSettings bölümünde hello yapılandırma dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="97a5d-270">Add hello settings toohello appSettings section of hello configuration file.</span></span> <span data-ttu-id="97a5d-271">Merhaba, hello önceki kod örneğinde hello bir Web.config dosyası aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="97a5d-271">hello following is hello Web.config file for hello previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="97a5d-272">Sabit kodlanmış bağlantı dizelerini kullanmaktan kaçının</span><span class="sxs-lookup"><span data-stu-id="97a5d-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="97a5d-273">Kimlik</span><span class="sxs-lookup"><span data-stu-id="97a5d-273">ID</span></span>
<span data-ttu-id="97a5d-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="97a5d-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="97a5d-275">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97a5d-275">Description</span></span>
<span data-ttu-id="97a5d-276">Sabit kodlanmış bağlantı dizelerini kullanın ve tooupdate ihtiyacınız varsa bunları daha sonra siz toomake değişiklikleri tooyour kaynak koduna sahip ve hello uygulama yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="97a5d-276">If you use hard-coded connection strings and you need tooupdate them later, you’ll have toomake changes tooyour source code and recompile hello application.</span></span> <span data-ttu-id="97a5d-277">Yapılandırma dosyasında bağlantı dizelerinizi depolarsanız, ancak, bunu daha sonra hello yapılandırma dosyasını güncelleştirerek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97a5d-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating hello configuration file.</span></span>

<span data-ttu-id="97a5d-278">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="97a5d-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="97a5d-279">Neden</span><span class="sxs-lookup"><span data-stu-id="97a5d-279">Reason</span></span>
<span data-ttu-id="97a5d-280">Sabit kodlama bağlantı dizeleri nedeni hatalı bir uygulama bağlantı dizeleri hızlı bir şekilde değiştirilmiş toobe gerektiğinde sorunları tanıtır.</span><span class="sxs-lookup"><span data-stu-id="97a5d-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need toobe changed quickly.</span></span> <span data-ttu-id="97a5d-281">Ayrıca, Hello proje toosource denetimindeki işaretli toobe gerekirse, sabit kodlanmış bağlantı dizeleri güvenlik açıkları hello dizeleri hello kaynak kodunda görüntülenebilir beri tanıtmaktadır.</span><span class="sxs-lookup"><span data-stu-id="97a5d-281">In addition, if hello project needs toobe checked in toosource control, hard-coded connection strings introduce security vulnerabilities since hello strings can be viewed in hello source code.</span></span>

### <a name="solution"></a><span data-ttu-id="97a5d-282">Çözüm</span><span class="sxs-lookup"><span data-stu-id="97a5d-282">Solution</span></span>
<span data-ttu-id="97a5d-283">Bağlantı dizeleri hello yapılandırma dosyalarının veya Azure ortamı depolar.</span><span class="sxs-lookup"><span data-stu-id="97a5d-283">Store connection strings in hello configuration files or Azure environments.</span></span>

* <span data-ttu-id="97a5d-284">Bağımsız uygulamalar için app.config toostore bağlantı dizesi ayarlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="97a5d-284">For standalone applications, use app.config toostore connection string settings.</span></span>
* <span data-ttu-id="97a5d-285">IIS tarafından barındırılan web uygulamaları için web.config toostore bağlantı dizelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="97a5d-285">For IIS-hosted web applications, use web.config toostore connection strings.</span></span>
* <span data-ttu-id="97a5d-286">ASP.NET vNext uygulamaları için configuration.json toostore bağlantı dizelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="97a5d-286">For ASP.NET vNext applications, use configuration.json toostore connection strings.</span></span>

<span data-ttu-id="97a5d-287">Web.config veya app.config gibi yapılandırma dosyalarını kullanma hakkında daha fazla bilgi için bkz: [ASP.NET Web yapılandırma yönergeleri](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span><span class="sxs-lookup"><span data-stu-id="97a5d-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="97a5d-288">Nasıl Azure ortam değişkenleri çalışma hakkında daha fazla bilgi için bkz: [Azure Web siteleri: nasıl uygulama dizeleri ve bağlantı dizeleri çalışma](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="97a5d-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="97a5d-289">Bağlantı dizesi kaynak denetiminde depolama hakkında daha fazla bilgi için bkz: [bağlantı dizeleri gibi hassas bilgileri kaynak kodu deposunda saklanır dosyalarında Geçirilmemesi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span><span class="sxs-lookup"><span data-stu-id="97a5d-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="97a5d-290">Tanılama yapılandırma dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="97a5d-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="97a5d-291">Kimlik</span><span class="sxs-lookup"><span data-stu-id="97a5d-291">ID</span></span>
<span data-ttu-id="97a5d-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="97a5d-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="97a5d-293">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97a5d-293">Description</span></span>
<span data-ttu-id="97a5d-294">API programlama Microsoft.WindowsAzure.Diagnostics Merhaba kullanarak kodunuzda gibi tanılama ayarları yapılandırmak yerine, hello diagnostics.wadcfg dosyasında tanılama ayarları yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-294">Instead of configuring diagnostics settings in your code such as by using hello Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in hello diagnostics.wadcfg file.</span></span> <span data-ttu-id="97a5d-295">(Ya da Azure SDK 2.5 kullanıyorsanız diagnostics.wadcfgx).</span><span class="sxs-lookup"><span data-stu-id="97a5d-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="97a5d-296">Bunu yaparak, kodunuzu toorecompile gerek kalmadan tanılama ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97a5d-296">By doing this, you can change diagnostics settings without having toorecompile your code.</span></span>

<span data-ttu-id="97a5d-297">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="97a5d-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="97a5d-298">Neden</span><span class="sxs-lookup"><span data-stu-id="97a5d-298">Reason</span></span>
<span data-ttu-id="97a5d-299">Azure SDK 2.5 (hangi Azure tanılama 1.3 kullanır), Azure tanılama (WAD) birkaç farklı yöntemler kullanarak yapılandırılabilir önce: depolama biriminde, toohello yapılandırma blob, kesinlik temelli kod, bildirim temelli yapılandırma veya hello varsayılan kullanarak ekleme yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="97a5d-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it toohello configuration blob in storage, by using imperative code, declarative configuration, or hello default configuration.</span></span> <span data-ttu-id="97a5d-300">Ancak, hello yolu tooconfigure tanılama toouse bir XML yapılandırma dosyasında (diagnostics.wadcfg veya diagnositcs.wadcfgx SDK 2.5 ve sonrası) hello uygulama projesi, tercih edilen.</span><span class="sxs-lookup"><span data-stu-id="97a5d-300">However, hello preferred way tooconfigure diagnostics is toouse an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in hello application project.</span></span> <span data-ttu-id="97a5d-301">Bu yaklaşımda, hello diagnostics.wadcfg dosya tamamen hello yapılandırmasını tanımlar ve güncelleştirilebilir ve gerçekleştirilse imzalanmasını.</span><span class="sxs-lookup"><span data-stu-id="97a5d-301">In this approach, hello diagnostics.wadcfg file completely defines hello configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="97a5d-302">Merhaba diagnostics.wadcfg yapılandırma dosyasının Hello kullanımı ile Merhaba hello kullanarak yapılandırmalarını ayarlama programlama yöntemleri karıştırma [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)veya [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) sınıfları tooconfusion yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-302">Mixing hello use of hello diagnostics.wadcfg configuration file with hello programmatic methods of setting configurations by using hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead tooconfusion.</span></span> <span data-ttu-id="97a5d-303">Bkz: [başlatılamadı ya da değişiklik Azure tanılama Yapılandırması](https://msdn.microsoft.com/library/azure/hh411537.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="97a5d-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="97a5d-304">WAD (Azure SDK 2.5 ile dahil) 1.3 ile başlayarak, olası toouse kod tooconfigure tanılama artık değildir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible toouse code tooconfigure diagnostics.</span></span> <span data-ttu-id="97a5d-305">Sonuç olarak, yalnızca uygulama ya da hello tanılama uzantısını güncelleştirilirken hello yapılandırması sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-305">As a result, you can only provide hello configuration when applying or updating hello diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="97a5d-306">Çözüm</span><span class="sxs-lookup"><span data-stu-id="97a5d-306">Solution</span></span>
<span data-ttu-id="97a5d-307">Merhaba tanılama yapılandırması Tasarımcı toomove tanılama ayarlarını toohello tanılama yapılandırma dosyası (diagnositcs.wadcfg veya diagnositcs.wadcfgx SDK 2.5 ve sonrası) kullanın.</span><span class="sxs-lookup"><span data-stu-id="97a5d-307">Use hello diagnostics configuration designer toomove diagnostic settings toohello diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="97a5d-308">Ayrıca, yüklemenizi tavsiye edilir [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) ve hello son Tanılama özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="97a5d-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use hello latest diagnostics feature.</span></span>

1. <span data-ttu-id="97a5d-309">Tooconfigure istediğiniz hello rolüne hello kısayol menüsünde Özellikler'i seçin ve sonra hello yapılandırma sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="97a5d-309">On hello shortcut menu for hello role that you want tooconfigure, choose Properties, and then choose hello Configuration tab.</span></span>
2. <span data-ttu-id="97a5d-310">Merhaba, **tanılama** bölümünde, o hello emin olun **tanılamayı etkinleştir** onay kutusu seçilidir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-310">In hello **Diagnostics** section, make sure that hello **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="97a5d-311">Merhaba seçin **yapılandırma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="97a5d-311">Choose hello **Configure** button.</span></span>

   ![Merhaba tanılamayı etkinleştir seçeneğine erişme](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="97a5d-313">Bkz: [yapılandırma tanılama Azure Cloud Services ve sanal makineler için](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="97a5d-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="97a5d-314">DbContext nesneleri statik olarak bildirme kaçının</span><span class="sxs-lookup"><span data-stu-id="97a5d-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="97a5d-315">Kimlik</span><span class="sxs-lookup"><span data-stu-id="97a5d-315">ID</span></span>
<span data-ttu-id="97a5d-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="97a5d-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="97a5d-317">Açıklama</span><span class="sxs-lookup"><span data-stu-id="97a5d-317">Description</span></span>
<span data-ttu-id="97a5d-318">toosave bellek DBContext nesneleri statik olarak bildirme kaçının.</span><span class="sxs-lookup"><span data-stu-id="97a5d-318">toosave memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="97a5d-319">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="97a5d-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="97a5d-320">Neden</span><span class="sxs-lookup"><span data-stu-id="97a5d-320">Reason</span></span>
<span data-ttu-id="97a5d-321">DBContext nesneleri hello sorgu sonuçlarındaki her çağrı basılı tutun.</span><span class="sxs-lookup"><span data-stu-id="97a5d-321">DBContext objects hold hello query results from each call.</span></span> <span data-ttu-id="97a5d-322">Merhaba uygulama etki alanı bellekten kaldırılana kadar statik DBContext nesneler atıldı değil.</span><span class="sxs-lookup"><span data-stu-id="97a5d-322">Static DBContext objects are not disposed until hello application domain is unloaded.</span></span> <span data-ttu-id="97a5d-323">Bu nedenle, bir statik DBContext nesnesi, büyük miktarlarda bellek kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="97a5d-324">Çözüm</span><span class="sxs-lookup"><span data-stu-id="97a5d-324">Solution</span></span>
<span data-ttu-id="97a5d-325">Bir yerel değişken ya da statik olmayan örnek alanı olarak DBContext bildirme, bir görev için kullanacağınız ve sonra kullanıldıktan sonra elden sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97a5d-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="97a5d-326">Aşağıdaki örnek MVC denetleyicisi sınıfı hello nasıl toouse hello DBContext nesne gösterir.</span><span class="sxs-lookup"><span data-stu-id="97a5d-326">hello following example MVC controller class shows how toouse hello DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a><span data-ttu-id="97a5d-327">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="97a5d-327">Next steps</span></span>
<span data-ttu-id="97a5d-328">en iyi duruma getirme ve Azure uygulamaları sorunlarını giderme hakkında daha fazla toolearn bkz [Visual Studio kullanarak Azure App Service web uygulamasında sorun giderme](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="97a5d-328">toolearn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
