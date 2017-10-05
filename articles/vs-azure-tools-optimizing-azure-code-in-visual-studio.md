---
title: Visual Studio'da Azure kodunuzu en iyi duruma getirme | Microsoft Docs
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
ms.openlocfilehash: 8f145502a856798d6e69ac11f324c72fa23f938e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="e13b9-103">Azure kodunuzu iyileştirme</span><span class="sxs-lookup"><span data-stu-id="e13b9-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="e13b9-104">Microsoft Azure kullanan uygulamalar programlama, uygulama ölçeklenebilirlik, davranış ve bulut ortamında bulunan performans sorunlarını önlemek için izlemeniz gereken bazı kodlama uygulamalarını vardır.</span><span class="sxs-lookup"><span data-stu-id="e13b9-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow to help avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="e13b9-105">Microsoft, tanır ve bu sık karşılaşılan sorunları çeşitli tanımlar ve bunları çözmenize yardımcı olacak bir Azure Kod Analizi aracı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e13b9-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="e13b9-106">Visual Studio'da NuGet aracılığıyla aracı yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e13b9-106">You can download the tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="e13b9-107">Azure Kod Analizi kuralları</span><span class="sxs-lookup"><span data-stu-id="e13b9-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="e13b9-108">Azure Kod Analizi aracı performansı etkileyen bilinen sorunlar bulduğunda otomatik olarak Azure kodunuzu bayrak için aşağıdaki kuralları kullanır.</span><span class="sxs-lookup"><span data-stu-id="e13b9-108">The Azure Code Analysis tool uses the following rules to automatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="e13b9-109">Sorunları görünen uyarıları olarak algılanan veya derleyici hataları.</span><span class="sxs-lookup"><span data-stu-id="e13b9-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="e13b9-110">Genellikle kod düzeltmeleri veya uyarı veya hata çözümlemek için öneriler ampul simgesi üzerinden sağlanır.</span><span class="sxs-lookup"><span data-stu-id="e13b9-110">Code fixes or suggestions to resolve the warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="e13b9-111">Varsayılan (işlemdeki) oturum durumu modunu kullanmaktan kaçının</span><span class="sxs-lookup"><span data-stu-id="e13b9-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="e13b9-112">Kimlik</span><span class="sxs-lookup"><span data-stu-id="e13b9-112">ID</span></span>
<span data-ttu-id="e13b9-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="e13b9-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="e13b9-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13b9-114">Description</span></span>
<span data-ttu-id="e13b9-115">Bulut uygulamaları için varsayılan (işlemdeki) oturum durumu modunu kullanıyorsanız, oturum durumu kaybedebilir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-115">If you use the default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="e13b9-116">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e13b9-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e13b9-117">Neden</span><span class="sxs-lookup"><span data-stu-id="e13b9-117">Reason</span></span>
<span data-ttu-id="e13b9-118">Varsayılan olarak, işlem içi oturum durumu modunu web.config dosyasında belirtilen.</span><span class="sxs-lookup"><span data-stu-id="e13b9-118">By default, the session state mode specified in the web.config file is in-process.</span></span> <span data-ttu-id="e13b9-119">Ayrıca, yapılandırma dosyasında belirtilen giriş varsa, oturum durumu modu işlemdeki varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="e13b9-119">Also, if no entry specified in the configuration file, the Session State mode defaults to in-process.</span></span> <span data-ttu-id="e13b9-120">İşlem içi modu oturum durumu web sunucusu üzerindeki bellekte depolar.</span><span class="sxs-lookup"><span data-stu-id="e13b9-120">The in-process mode stores session state in memory on the web server.</span></span> <span data-ttu-id="e13b9-121">Örneği yeniden ya da yeni bir örneğini Yük Dengeleme veya yük devretme desteği için kullanılan bellek web sunucusu üzerinde depolanan oturum durumu kaydedilmez.</span><span class="sxs-lookup"><span data-stu-id="e13b9-121">When an instance is restarted or a new instance is used for load balancing or failover support, the session state stored in memory on the web server isn’t saved.</span></span> <span data-ttu-id="e13b9-122">Bu durum, ölçeklenebilir bulut üzerinde engeller uygulama engeller.</span><span class="sxs-lookup"><span data-stu-id="e13b9-122">This situation prevents the application from being scalable on the cloud.</span></span>

<span data-ttu-id="e13b9-123">ASP.NET oturum durumu için oturum durumu verilerini birkaç farklı depolama seçeneklerini destekler: InProc, StateServer, SQLServer, özel ve kapalı.</span><span class="sxs-lookup"><span data-stu-id="e13b9-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="e13b9-124">Özel modu verileri barındırmak için bir dış oturum durumu deposunda gibi kullanmanız önerilir [Redis için Azure oturum durumu sağlayıcısı](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="e13b9-124">It’s recommended that you use Custom mode to host data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="e13b9-125">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e13b9-125">Solution</span></span>
<span data-ttu-id="e13b9-126">Bir önerilen bir yönetilen önbellek hizmetinde oturum durumunu depolamak için bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="e13b9-126">One recommended solution is to store session state on a managed cache service.</span></span> <span data-ttu-id="e13b9-127">Nasıl kullanacağınızı öğrenin [Redis için Azure oturum durumu sağlayıcısı](http://go.microsoft.com/fwlink/?LinkId=401521) oturum durumunu depolamak için.</span><span class="sxs-lookup"><span data-stu-id="e13b9-127">Learn how to use [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) to store your session state.</span></span> <span data-ttu-id="e13b9-128">Oturum durumu uygulamanızı bulutta ölçeklenebilir olduğundan emin olmak için diğer yerler depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e13b9-128">You can also store session state in other places to ensure your application is scalable on the cloud.</span></span> <span data-ttu-id="e13b9-129">Lütfen okuyun alternatif çözümleri hakkında daha fazla bilgi edinmek için [oturum durumu modu](https://msdn.microsoft.com/library/ms178586).</span><span class="sxs-lookup"><span data-stu-id="e13b9-129">To learn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="e13b9-130">Run yöntemini zaman uyumsuz olmamalıdır</span><span class="sxs-lookup"><span data-stu-id="e13b9-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="e13b9-131">Kimlik</span><span class="sxs-lookup"><span data-stu-id="e13b9-131">ID</span></span>
<span data-ttu-id="e13b9-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="e13b9-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="e13b9-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13b9-133">Description</span></span>
<span data-ttu-id="e13b9-134">Zaman uyumsuz yöntemleri oluşturun (gibi [await](https://msdn.microsoft.com/library/hh156528.aspx)) dışında [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi ve zaman uyumsuz yöntemleri çağırma [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="e13b9-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call the async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="e13b9-135">Bildirme [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi zaman uyumsuz olarak bir yeniden başlatma döngü girmek çalışan rolü neden olur.</span><span class="sxs-lookup"><span data-stu-id="e13b9-135">Declaring the [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes the worker role to enter a restart loop.</span></span>

<span data-ttu-id="e13b9-136">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e13b9-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e13b9-137">Neden</span><span class="sxs-lookup"><span data-stu-id="e13b9-137">Reason</span></span>
<span data-ttu-id="e13b9-138">İçinde zaman uyumsuz yöntemleri çağırma [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi çalışan rolü geri dönüştürmek bulut hizmeti çalışma zamanı neden olur.</span><span class="sxs-lookup"><span data-stu-id="e13b9-138">Calling async methods inside the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes the cloud service runtime to recycle the worker role.</span></span> <span data-ttu-id="e13b9-139">Çalışan rolü başladığında, tüm program yürütme içinde gerçekleşir [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e13b9-139">When a worker role starts, all program execution takes place inside the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="e13b9-140">Çıkma [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi yeniden başlatmak çalışan rolü neden olur.</span><span class="sxs-lookup"><span data-stu-id="e13b9-140">Exiting the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes the worker role to restart.</span></span> <span data-ttu-id="e13b9-141">Zaman uyumsuz yöntem çalışan rolü çalışma zamanı geldiğinde, tüm işlemleri sonra async yöntemi gönderir ve ardından döndürür.</span><span class="sxs-lookup"><span data-stu-id="e13b9-141">When the worker role runtime hits the async method, it dispatches all operations after the async method and then returns.</span></span> <span data-ttu-id="e13b9-142">Bu çalışan rolü'ndan çıkmak neden [ [ [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi ve yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="e13b9-142">This causes the worker role to exit from the [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="e13b9-143">Yinelemede sonraki yürütme, çalışan rolü zaman uyumsuz yöntem yeniden İsabetli ve çalışan rolü yeniden de geri dönüşüm yapmasına neden yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="e13b9-143">In the next iteration of execution, the worker role hits the async method again and restarts, causing the worker role to recycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="e13b9-144">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e13b9-144">Solution</span></span>
<span data-ttu-id="e13b9-145">Tüm zaman uyumsuz işlemleri dışında yerleştirin [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e13b9-145">Place all async operations outside of the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="e13b9-146">Ardından, içinde işlenmiş zaman uyumsuz yöntemden çağırın [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) RunAsync () .wait gibi yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e13b9-146">Then, call the refactored async method from inside the [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="e13b9-147">Azure Kod Analizi aracı, bu sorunu gidermenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-147">The Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="e13b9-148">Aşağıdaki kod parçacığını bu sorunla ilgili kod düzeltme gösterir:</span><span class="sxs-lookup"><span data-stu-id="e13b9-148">The following code snippet demonstrates the code fix for this issue:</span></span>

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

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="e13b9-149">Hizmet veri yolu paylaşılan erişim imzası kimlik doğrulamasını kullan</span><span class="sxs-lookup"><span data-stu-id="e13b9-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="e13b9-150">Kimlik</span><span class="sxs-lookup"><span data-stu-id="e13b9-150">ID</span></span>
<span data-ttu-id="e13b9-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="e13b9-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="e13b9-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13b9-152">Description</span></span>
<span data-ttu-id="e13b9-153">Paylaşılan erişim imzası (SAS) kimlik doğrulaması için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e13b9-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="e13b9-154">Erişim denetimi Hizmeti'nden (ACS) hizmet veri yolu kimlik doğrulaması için kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="e13b9-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="e13b9-155">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e13b9-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e13b9-156">Neden</span><span class="sxs-lookup"><span data-stu-id="e13b9-156">Reason</span></span>
<span data-ttu-id="e13b9-157">Gelişmiş güvenlik için Azure Active Directory ACS kimlik doğrulaması SAS kimlik doğrulaması ile değiştirmektir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="e13b9-158">Bkz: [Azure Active Directory olduğu ACS geleceği](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) geçiş planı hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e13b9-158">See [Azure Active Directory is the future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on the transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="e13b9-159">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e13b9-159">Solution</span></span>
<span data-ttu-id="e13b9-160">SAS kimlik doğrulaması uygulamalarınızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e13b9-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="e13b9-161">Aşağıdaki örnek, bir hizmet veri yolu ad alanı veya varlık erişmek için var olan bir SAS belirteci kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-161">The following example shows how to use an existing SAS token to access a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="e13b9-162">Daha fazla bilgi için aşağıdaki konulara bakın.</span><span class="sxs-lookup"><span data-stu-id="e13b9-162">See the following topics for more information.</span></span>

* <span data-ttu-id="e13b9-163">Genel bir bakış için bkz: [paylaşılan erişim imzası kimlik doğrulaması Service Bus ile](https://msdn.microsoft.com/library/dn170477.aspx)</span><span class="sxs-lookup"><span data-stu-id="e13b9-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="e13b9-164">Service Bus ile paylaşılan erişim imzası kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="e13b9-164">How to use Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="e13b9-165">Örnek proje için bkz: [hizmet veri yolu abonelikleri ile kullanarak paylaşılan erişim imzası (SAS) kimlik doğrulaması](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span><span class="sxs-lookup"><span data-stu-id="e13b9-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-to-avoid-receive-loop"></a><span data-ttu-id="e13b9-166">"Döngü alırsınız" önlemek için Onmessageoptions yöntemini kullanmayı deneyin</span><span class="sxs-lookup"><span data-stu-id="e13b9-166">Consider using OnMessage method to avoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="e13b9-167">Kimlik</span><span class="sxs-lookup"><span data-stu-id="e13b9-167">ID</span></span>
<span data-ttu-id="e13b9-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="e13b9-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="e13b9-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13b9-169">Description</span></span>
<span data-ttu-id="e13b9-170">Bir "alma döngü," uygulamasına giderek önlemek için çağırma **Onmessageoptions** yöntemdir arama daha iletileri almak için daha iyi bir çözüm **alma** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="e13b9-170">To avoid going into a "receive loop," calling the **OnMessage** method is a better solution for receiving messages than calling the **Receive** method.</span></span> <span data-ttu-id="e13b9-171">Ancak, kullanmanız gerekiyorsa **alma** yöntemi ve varsayılan olmayan sunucu bekleme süresini belirtin, sunucu bekleme süresi bir dakikadan fazla olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e13b9-171">However, if you must use the **Receive** method, and you specify a non-default server wait time, make sure the server wait time is more than one minute.</span></span>

<span data-ttu-id="e13b9-172">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e13b9-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e13b9-173">Neden</span><span class="sxs-lookup"><span data-stu-id="e13b9-173">Reason</span></span>
<span data-ttu-id="e13b9-174">Çağrılırken **Onmessageoptions**, istemci sürekli sıra veya abonelik yokladığı bir dahili ileti Pompalama başlatır.</span><span class="sxs-lookup"><span data-stu-id="e13b9-174">When calling **OnMessage**, the client starts an internal message pump that constantly polls the queue or subscription.</span></span> <span data-ttu-id="e13b9-175">Bu ileti Pompalama iletileri almak için bir çağrı sorunları sonsuz bir döngüde içerir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-175">This message pump contains an infinite loop that issues a call to receive messages.</span></span> <span data-ttu-id="e13b9-176">Arama zaman aşımına uğrarsa, yeni bir çağrı verir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-176">If the call times out, it issues a new call.</span></span> <span data-ttu-id="e13b9-177">Zaman aşımı aralığı değeri tarafından belirlenir [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) özelliği [Eventhubclient](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)kullanılan.</span><span class="sxs-lookup"><span data-stu-id="e13b9-177">The timeout interval is determined by the value of the [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of the [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="e13b9-178">Kullanmanın avantajı **Onmessageoptions** karşılaştırılan **alma** kullanıcıları el ile iletileri için yoklama, özel durumları işleme, birden fazla ileti paralel işlem ve iletiler tamamlama gerekmemesidir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-178">The advantage of using **OnMessage** compared to **Receive** is that users don’t have to manually poll for messages, handle exceptions, process multiple messages in parallel, and complete the messages.</span></span>

<span data-ttu-id="e13b9-179">Çağırırsanız **alma** emin olun, varsayılan değer kullanmadan *ServerWaitTime* değerdir bir dakikadan fazla.</span><span class="sxs-lookup"><span data-stu-id="e13b9-179">If you call **Receive** without using its default value, be sure the *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="e13b9-180">Ayarı *ServerWaitTime* bir dakikadan için sunucu ileti tamamen alınmadan önce zaman aşımına uğruyor engeller.</span><span class="sxs-lookup"><span data-stu-id="e13b9-180">Setting *ServerWaitTime* to more than one minute prevents the server from timing out before the message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="e13b9-181">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e13b9-181">Solution</span></span>
<span data-ttu-id="e13b9-182">Aşağıdaki kod örnekleri önerilen kullanımlar için bkz.</span><span class="sxs-lookup"><span data-stu-id="e13b9-182">Please see the following code examples for recommended usages.</span></span> <span data-ttu-id="e13b9-183">Daha fazla ayrıntı için bkz: [QueueClient.OnMessage yöntemi (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)ve [QueueClient.Receive yöntemi (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span><span class="sxs-lookup"><span data-stu-id="e13b9-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="e13b9-184">Azure Mesajlaşma altyapısı performansını geliştirmek için tasarım deseni bkz [zaman uyumsuz Mesajlaşma Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="e13b9-184">To improve the performance of the Azure messaging infrastructure, see the design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="e13b9-185">Kullanarak bir örnek verilmiştir **Onmessageoptions** iletileri almak için.</span><span class="sxs-lookup"><span data-stu-id="e13b9-185">The following is an example of using **OnMessage** to receive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if the message-pump should call complete on messages after the callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates the maximum number of concurrent calls to the callback the pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you to get notified of any errors encountered by the message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates the message pump and callback is invoked for each message that is recieved, calling close on the client will stop the pump.
    {
        // Process the message.
    }, options);
    Console.WriteLine("Press any key to exit.");
    Console.ReadKey();
```

<span data-ttu-id="e13b9-186">Kullanarak bir örnek verilmiştir **alma** varsayılan sunucusuyla bekleme süresi.</span><span class="sxs-lookup"><span data-stu-id="e13b9-186">The following is an example of using **Receive** with the default server wait time.</span></span>

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

<span data-ttu-id="e13b9-187">Kullanarak bir örnek verilmiştir **alma** varsayılan olmayan sunucusuyla bekleme süresi.</span><span class="sxs-lookup"><span data-stu-id="e13b9-187">The following is an example of using **Receive** with a non-default server wait time.</span></span>

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
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="e13b9-188">Zaman uyumsuz hizmet veri yolu yöntemleri kullanmayı düşünün</span><span class="sxs-lookup"><span data-stu-id="e13b9-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="e13b9-189">Kimlik</span><span class="sxs-lookup"><span data-stu-id="e13b9-189">ID</span></span>
<span data-ttu-id="e13b9-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="e13b9-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="e13b9-191">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13b9-191">Description</span></span>
<span data-ttu-id="e13b9-192">Aracılı Mesajlaşma ile performansını artırmak için zaman uyumsuz hizmet veri yolu yöntemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e13b9-192">Use asynchronous Service Bus methods to improve performance with brokered messaging.</span></span>

<span data-ttu-id="e13b9-193">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e13b9-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e13b9-194">Neden</span><span class="sxs-lookup"><span data-stu-id="e13b9-194">Reason</span></span>
<span data-ttu-id="e13b9-195">Her çağrısının ana iş parçacığı engellemesini devre dışı bırakmak için zaman uyumsuz yöntemleri kullanarak uygulama programı eşzamanlılık sağlar.</span><span class="sxs-lookup"><span data-stu-id="e13b9-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block the main thread.</span></span> <span data-ttu-id="e13b9-196">Service Bus Mesajlaşma yöntemleri, bir işlemi gerçekleştirilirken kullanırken (gönderme, alma, silme, vb.) zaman alır.</span><span class="sxs-lookup"><span data-stu-id="e13b9-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="e13b9-197">Bu süre, istek ve yanıt gecikmesi ek olarak Service Bus hizmeti tarafından işlemi işlenmesini içerir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-197">This time includes the processing of the operation by the Service Bus service in addition to the latency of the request and the reply.</span></span> <span data-ttu-id="e13b9-198">Saat başına işlem sayısını artırmak için işlemler aynı anda yürütmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-198">To increase the number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="e13b9-199">Daha fazla bilgi için lütfen [performans iyileştirmeleri kullanarak Service Bus aracılı Mesajlaşma için en iyi uygulamaları](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span><span class="sxs-lookup"><span data-stu-id="e13b9-199">For more information please refer to [Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="e13b9-200">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e13b9-200">Solution</span></span>
<span data-ttu-id="e13b9-201">Bkz: [QueueClient sınıfı (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) önerilen zaman uyumsuz yönteminin nasıl kullanılacağı hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e13b9-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how to use the recommended asynchronous method.</span></span>

<span data-ttu-id="e13b9-202">Azure Mesajlaşma altyapısı performansını geliştirmek için tasarım deseni bkz [zaman uyumsuz Mesajlaşma Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="e13b9-202">To improve the performance of the Azure messaging infrastructure, see the design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="e13b9-203">Bölümleme Service Bus kuyrukları ve konuları göz önünde bulundurun</span><span class="sxs-lookup"><span data-stu-id="e13b9-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="e13b9-204">Kimlik</span><span class="sxs-lookup"><span data-stu-id="e13b9-204">ID</span></span>
<span data-ttu-id="e13b9-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="e13b9-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="e13b9-206">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13b9-206">Description</span></span>
<span data-ttu-id="e13b9-207">Bölüm Service Bus kuyrukları ve konularından Service Bus Mesajlaşma ile daha iyi performans için.</span><span class="sxs-lookup"><span data-stu-id="e13b9-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="e13b9-208">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e13b9-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e13b9-209">Neden</span><span class="sxs-lookup"><span data-stu-id="e13b9-209">Reason</span></span>
<span data-ttu-id="e13b9-210">Bölümlenmiş kuyruk veya konu, genel üretilen işi artık tek ileti Aracısı ya da ileti deposu performans ile sınırlı olduğundan, Service Bus kuyrukları ve konularından bölümleme performans verimlilik ve hizmet kullanılabilirliğini artırır.</span><span class="sxs-lookup"><span data-stu-id="e13b9-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because the overall throughput of a partitioned queue or topic is no longer limited by the performance of a single message broker or messaging store.</span></span> <span data-ttu-id="e13b9-211">Ayrıca, bir Mesajlaşma deposu geçici bir kesinti bölümlenmiş kuyruk veya konu kullanılamaz hale değil.</span><span class="sxs-lookup"><span data-stu-id="e13b9-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="e13b9-212">Daha fazla bilgi için bkz: [Mesajlaşma varlıkları bölümleme](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span><span class="sxs-lookup"><span data-stu-id="e13b9-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="e13b9-213">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e13b9-213">Solution</span></span>
<span data-ttu-id="e13b9-214">Aşağıdaki kod parçacığında, Mesajlaşma varlıkları bölüm gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-214">The following code snippet shows how to partition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="e13b9-215">Daha fazla bilgi için bkz: [bölümlenmiş Service Bus kuyrukları ve konularından | Microsoft Azure blogu](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) ve kullanıma [Microsoft Azure hizmet veri yolu kuyruğu bölümlenmiş](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) örnek.</span><span class="sxs-lookup"><span data-stu-id="e13b9-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out the [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="e13b9-216">SharedAccessStartTime ayarlı değil</span><span class="sxs-lookup"><span data-stu-id="e13b9-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="e13b9-217">Kimlik</span><span class="sxs-lookup"><span data-stu-id="e13b9-217">ID</span></span>
<span data-ttu-id="e13b9-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="e13b9-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="e13b9-219">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13b9-219">Description</span></span>
<span data-ttu-id="e13b9-220">Paylaşılan Erişim İlkesi hemen başlatmak için geçerli zamanın SharedAccessStartTimeset kullanarak kaçınmalısınız.</span><span class="sxs-lookup"><span data-stu-id="e13b9-220">You should avoid using SharedAccessStartTimeset to the current time to immediately start the Shared Access policy.</span></span> <span data-ttu-id="e13b9-221">Yalnızca paylaşılan erişim ilkesi daha sonraki bir zamanda başlatmak istiyorsanız bu özelliği ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-221">You only need to set this property if you want to start the Shared Access policy at a later time.</span></span>

<span data-ttu-id="e13b9-222">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e13b9-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e13b9-223">Neden</span><span class="sxs-lookup"><span data-stu-id="e13b9-223">Reason</span></span>
<span data-ttu-id="e13b9-224">Saati eşitleme veri merkezleri arasında küçük zaman farkı neden olur.</span><span class="sxs-lookup"><span data-stu-id="e13b9-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="e13b9-225">Örneğin, mantıksal olarak DateTime.Now kullanarak geçerli zaman olarak başlangıç zamanı depolama SAS İlkesi ayarlama düşündüğünüz veya benzer bir yöntem hemen etkinleşmesini SAS İlkesi neden olur.</span><span class="sxs-lookup"><span data-stu-id="e13b9-225">For example, you would logically think setting the start time of a storage SAS policy as the current time by using DateTime.Now or a similar method will cause the SAS policy to take effect immediately.</span></span> <span data-ttu-id="e13b9-226">Ancak, veri merkezi zamanlarda diğerlerinin bu öncesinde başlangıç saatinden sonraki biraz olabileceğinden veri merkezleri arasında hafif saat farklılıklarını bu sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-226">However, the slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than the start time, while others ahead of it.</span></span> <span data-ttu-id="e13b9-227">Sonuç olarak, SAS İlkesi hızla (veya hatta hemen) dolabilir İlkesi yaşam süresi çok kısa olarak ayarlanmışsa.</span><span class="sxs-lookup"><span data-stu-id="e13b9-227">As a result, the SAS policy can expire quickly (or even immediately) if the policy lifetime is set too short.</span></span>

<span data-ttu-id="e13b9-228">Üzerinde Azure storage paylaşılan erişim imzası kullanma konusunda daha fazla yönergeler için bkz: [giriş tablosu SAS (paylaşılan erişim imzası) kuyruğu SAS ve Blob SAS - Microsoft Azure depolama ekibi blogu - güncelleştirmeye Site giriş - MSDN Bloglarında](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="e13b9-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="e13b9-229">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e13b9-229">Solution</span></span>
<span data-ttu-id="e13b9-230">Paylaşılan erişim ilkesinin başlangıç saatini ayarlar deyimi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e13b9-230">Remove the statement that sets the start time of the shared access policy.</span></span> <span data-ttu-id="e13b9-231">Azure Kod Analizi aracı bu sorun için düzeltme sağlar.</span><span class="sxs-lookup"><span data-stu-id="e13b9-231">The Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="e13b9-232">Güvenlik yönetimi hakkında daha fazla bilgi için lütfen bkz tasarım deseni [Valet anahtar düzeni](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="e13b9-232">For more information on security management, please see the design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="e13b9-233">Aşağıdaki kod parçacığını bu sorunla ilgili kod düzeltme gösterir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-233">The following code snippet demonstrates the code fix for this issue.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="e13b9-234">Paylaşılan Erişim İlkesi sona erme saati beş dakikadan fazla olmalıdır</span><span class="sxs-lookup"><span data-stu-id="e13b9-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="e13b9-235">Kimlik</span><span class="sxs-lookup"><span data-stu-id="e13b9-235">ID</span></span>
<span data-ttu-id="e13b9-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="e13b9-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="e13b9-237">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13b9-237">Description</span></span>
<span data-ttu-id="e13b9-238">Beş dakikalık fark kadar "saat eğme." bilinen bir koşul nedeniyle farklı konumlardaki veri merkezleri arasında saatleri içinde olabilir</span><span class="sxs-lookup"><span data-stu-id="e13b9-238">There can be as much as a five minute difference in clocks among datacenters at different locations due to a condition known as "clock skew."</span></span> <span data-ttu-id="e13b9-239">SAS önlemek için zaman aşımına uğramak gelen ilke belirteci planlanan daha erken sona erme saati beş dakikadan fazla olacak şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e13b9-239">To prevent the SAS policy token from expiring earlier than planned, set the expiry time to be more than five minutes.</span></span>

<span data-ttu-id="e13b9-240">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e13b9-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e13b9-241">Neden</span><span class="sxs-lookup"><span data-stu-id="e13b9-241">Reason</span></span>
<span data-ttu-id="e13b9-242">Dünyanın dört farklı konumlardaki veri merkezlerine saati sinyali ile eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="e13b9-242">Datacenters at different locations around the world synchronize by a clock signal.</span></span> <span data-ttu-id="e13b9-243">Farklı bir konuma seyahat saat sinyal zaman alır çünkü her şeyin beklendiği gibi eşitlenir ancak farklı coğrafi konumlardaki veri merkezlerine arasındaki zaman farkı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-243">Because it takes time for clock signal to travel to different locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="e13b9-244">Bu zaman farkı, paylaşılan erişim ilkesi başlangıç saati ve sona erme aralığını etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-244">This time difference can affect the Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="e13b9-245">Bu nedenle, paylaşılan erişim ilkesi hemen etkinleşir emin olmak için başlangıç saati belirtmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="e13b9-245">Therefore, to ensure Shared Access policy takes effect immediately, don’t specify the start time.</span></span> <span data-ttu-id="e13b9-246">Ayrıca, sona erme zamanı erken zaman aşımını önlemek için birden fazla 5 dakika olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e13b9-246">In addition, make sure the expiration time is more than 5 minutes to prevent early timeout.</span></span>

<span data-ttu-id="e13b9-247">Azure depolama alanında paylaşılan erişim imzası kullanma hakkında daha fazla bilgi için bkz: [giriş tablosu SAS (paylaşılan erişim imzası) kuyruğu SAS ve Blob SAS - Microsoft Azure depolama ekibi blogu - güncelleştirmeye Site giriş - MSDN Bloglarında](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="e13b9-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="e13b9-248">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e13b9-248">Solution</span></span>
<span data-ttu-id="e13b9-249">Güvenlik yönetimi hakkında daha fazla bilgi için bkz: tasarım deseni [Valet anahtar düzeni](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="e13b9-249">For more information on security management, see the design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="e13b9-250">Paylaşılan Erişim İlkesi başlangıç zamanı belirtmeden bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-250">The following is an example of not specifying a Shared Access policy start time.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="e13b9-251">Bir ilke sona erme süresi beş dakikadan fazla ile bir paylaşılan erişim ilkesi başlangıç saati belirten bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-251">The following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="e13b9-252">Daha fazla bilgi için bkz: [oluşturmak ve paylaşılan erişim imzası kullanmak](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="e13b9-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="e13b9-253">CloudConfigurationManager kullanın</span><span class="sxs-lookup"><span data-stu-id="e13b9-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="e13b9-254">Kimlik</span><span class="sxs-lookup"><span data-stu-id="e13b9-254">ID</span></span>
<span data-ttu-id="e13b9-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="e13b9-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="e13b9-256">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13b9-256">Description</span></span>
<span data-ttu-id="e13b9-257">Kullanarak [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) sınıf projelerde gibi Azure Web sitesine gidin ve Azure mobil hizmetler çalışma zamanı sorunlarına neden olmaz.</span><span class="sxs-lookup"><span data-stu-id="e13b9-257">Using the [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="e13b9-258">En iyi uygulama, ancak bunu bulut kullanmak için iyi bir fikirdir[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) tüm Azure bulut uygulamaları için yapılandırmaları yönetme birleşik bir yolu olarak.</span><span class="sxs-lookup"><span data-stu-id="e13b9-258">As a best practice, however, it's a good idea to use Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="e13b9-259">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e13b9-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e13b9-260">Neden</span><span class="sxs-lookup"><span data-stu-id="e13b9-260">Reason</span></span>
<span data-ttu-id="e13b9-261">CloudConfigurationManager uygulama ortamınız için uygun yapılandırma dosyasını okur.</span><span class="sxs-lookup"><span data-stu-id="e13b9-261">CloudConfigurationManager reads the configuration file appropriate to the application environment.</span></span>

[<span data-ttu-id="e13b9-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="e13b9-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="e13b9-263">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e13b9-263">Solution</span></span>
<span data-ttu-id="e13b9-264">Kullanmak için kodunuzu yeniden düzenlemeniz [CloudConfigurationManager sınıfı](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="e13b9-264">Refactor your code to use the [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="e13b9-265">Bu sorun için bir kod düzeltme Azure Kod Analizi aracı tarafından sağlanır.</span><span class="sxs-lookup"><span data-stu-id="e13b9-265">A code fix for this issue is provided by the Azure Code Analysis tool.</span></span>

<span data-ttu-id="e13b9-266">Aşağıdaki kod parçacığını bu sorunla ilgili kod düzeltme gösterir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-266">The following code snippet demonstrates the code fix for this issue.</span></span> <span data-ttu-id="e13b9-267">Değiştir</span><span class="sxs-lookup"><span data-stu-id="e13b9-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="e13b9-268">İle</span><span class="sxs-lookup"><span data-stu-id="e13b9-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="e13b9-269">Yapılandırma ayarı App.config veya Web.config dosyasında depolamak nasıl bir örneği burada verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-269">Here's an example of how to store the configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="e13b9-270">Ayarları yapılandırma dosyasının appSettings bölümünü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e13b9-270">Add the settings to the appSettings section of the configuration file.</span></span> <span data-ttu-id="e13b9-271">Önceki kod örneğinde için Web.config dosyasının verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-271">The following is the Web.config file for the previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="e13b9-272">Sabit kodlanmış bağlantı dizelerini kullanmaktan kaçının</span><span class="sxs-lookup"><span data-stu-id="e13b9-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="e13b9-273">Kimlik</span><span class="sxs-lookup"><span data-stu-id="e13b9-273">ID</span></span>
<span data-ttu-id="e13b9-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="e13b9-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="e13b9-275">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13b9-275">Description</span></span>
<span data-ttu-id="e13b9-276">Sabit kodlanmış bağlantı dizelerini kullanın ve daha sonra güncelleştirmek ihtiyacınız varsa, kaynak kodunuzu değişiklikleri yapın ve uygulamayı yeniden derlemenize gerekir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-276">If you use hard-coded connection strings and you need to update them later, you’ll have to make changes to your source code and recompile the application.</span></span> <span data-ttu-id="e13b9-277">Yapılandırma dosyasında bağlantı dizelerinizi depolarsanız, ancak bunu daha sonra yapılandırma dosyasını güncelleştirerek değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e13b9-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating the configuration file.</span></span>

<span data-ttu-id="e13b9-278">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e13b9-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e13b9-279">Neden</span><span class="sxs-lookup"><span data-stu-id="e13b9-279">Reason</span></span>
<span data-ttu-id="e13b9-280">Sabit kodlama bağlantı dizeleri nedeni hatalı bir uygulama bağlantı dizeleri hızlı bir şekilde değiştirilmesi gerektiğinde sorunları tanıtır.</span><span class="sxs-lookup"><span data-stu-id="e13b9-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need to be changed quickly.</span></span> <span data-ttu-id="e13b9-281">Ayrıca, proje kaynak denetimine iade edilmesi gerekirse, sabit kodlanmış bağlantı dizeleri güvenlik açıkları dizeleri kaynak kodunda görüntülenebilir beri tanıtmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e13b9-281">In addition, if the project needs to be checked in to source control, hard-coded connection strings introduce security vulnerabilities since the strings can be viewed in the source code.</span></span>

### <a name="solution"></a><span data-ttu-id="e13b9-282">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e13b9-282">Solution</span></span>
<span data-ttu-id="e13b9-283">Bağlantı dizelerini yapılandırma dosyaları ya da Azure ortamı depolar.</span><span class="sxs-lookup"><span data-stu-id="e13b9-283">Store connection strings in the configuration files or Azure environments.</span></span>

* <span data-ttu-id="e13b9-284">Bağımsız uygulamalar için app.config bağlantı dizesi ayarlarını depolamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e13b9-284">For standalone applications, use app.config to store connection string settings.</span></span>
* <span data-ttu-id="e13b9-285">IIS tarafından barındırılan web uygulamaları için web.config bağlantı dizeleri depolamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e13b9-285">For IIS-hosted web applications, use web.config to store connection strings.</span></span>
* <span data-ttu-id="e13b9-286">ASP.NET vNext uygulamaları için bağlantı dizelerini depolamak için configuration.json kullanın.</span><span class="sxs-lookup"><span data-stu-id="e13b9-286">For ASP.NET vNext applications, use configuration.json to store connection strings.</span></span>

<span data-ttu-id="e13b9-287">Web.config veya app.config gibi yapılandırma dosyalarını kullanma hakkında daha fazla bilgi için bkz: [ASP.NET Web yapılandırma yönergeleri](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span><span class="sxs-lookup"><span data-stu-id="e13b9-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="e13b9-288">Nasıl Azure ortam değişkenleri çalışma hakkında daha fazla bilgi için bkz: [Azure Web siteleri: nasıl uygulama dizeleri ve bağlantı dizeleri çalışma](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="e13b9-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="e13b9-289">Bağlantı dizesi kaynak denetiminde depolama hakkında daha fazla bilgi için bkz: [bağlantı dizeleri gibi hassas bilgileri kaynak kodu deposunda saklanır dosyalarında Geçirilmemesi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span><span class="sxs-lookup"><span data-stu-id="e13b9-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="e13b9-290">Tanılama yapılandırma dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="e13b9-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="e13b9-291">Kimlik</span><span class="sxs-lookup"><span data-stu-id="e13b9-291">ID</span></span>
<span data-ttu-id="e13b9-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="e13b9-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="e13b9-293">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13b9-293">Description</span></span>
<span data-ttu-id="e13b9-294">Tanılama ayarları gibi kodunuzda API programlama Microsoft.WindowsAzure.Diagnostics kullanarak yapılandırmak yerine, diagnostics.wadcfg dosyasında tanılama ayarlarını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-294">Instead of configuring diagnostics settings in your code such as by using the Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in the diagnostics.wadcfg file.</span></span> <span data-ttu-id="e13b9-295">(Ya da Azure SDK 2.5 kullanıyorsanız diagnostics.wadcfgx).</span><span class="sxs-lookup"><span data-stu-id="e13b9-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="e13b9-296">Bunu yaparak, kodunuzu yeniden derlemenize gerek kalmadan tanılama ayarlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e13b9-296">By doing this, you can change diagnostics settings without having to recompile your code.</span></span>

<span data-ttu-id="e13b9-297">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e13b9-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e13b9-298">Neden</span><span class="sxs-lookup"><span data-stu-id="e13b9-298">Reason</span></span>
<span data-ttu-id="e13b9-299">Azure SDK 2.5 (hangi Azure tanılama 1.3 kullanır), Azure tanılama (WAD) birkaç farklı yöntemler kullanarak yapılandırılabilir önce: Bu yapılandırma blob depolama, kesinlik temelli kodu, bildirim temelli yapılandırma veya varsayılan kullanarak ekleme yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="e13b9-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it to the configuration blob in storage, by using imperative code, declarative configuration, or the default configuration.</span></span> <span data-ttu-id="e13b9-300">Ancak, tanılama yapılandırmak için tercih edilen yöntem bir XML yapılandırma dosyasında (diagnostics.wadcfg veya diagnositcs.wadcfgx SDK 2.5 ve sonrası) uygulama projesi kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="e13b9-300">However, the preferred way to configure diagnostics is to use an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in the application project.</span></span> <span data-ttu-id="e13b9-301">Bu yaklaşımda, diagnostics.wadcfg dosya tamamen yapılandırmasını tanımlar ve güncelleştirilebilir ve gerçekleştirilse imzalanmasını.</span><span class="sxs-lookup"><span data-stu-id="e13b9-301">In this approach, the diagnostics.wadcfg file completely defines the configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="e13b9-302">Diagnostics.wadcfg yapılandırma dosyasının kullanımını kullanarak yapılandırmalarını ayarlama programlama yöntemleri ile karıştırma [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)veya [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)sınıfları olabilir karışıklığa yol açar.</span><span class="sxs-lookup"><span data-stu-id="e13b9-302">Mixing the use of the diagnostics.wadcfg configuration file with the programmatic methods of setting configurations by using the [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead to confusion.</span></span> <span data-ttu-id="e13b9-303">Bkz: [başlatılamadı ya da değişiklik Azure tanılama Yapılandırması](https://msdn.microsoft.com/library/azure/hh411537.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e13b9-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="e13b9-304">WAD 1.3 (Azure SDK 2.5 ile dahil) itibaren artık kod tanılama yapılandırmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="e13b9-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible to use code to configure diagnostics.</span></span> <span data-ttu-id="e13b9-305">Sonuç olarak, yalnızca uygulama ya da tanılama uzantısını güncelleştirilirken yapılandırması sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-305">As a result, you can only provide the configuration when applying or updating the diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="e13b9-306">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e13b9-306">Solution</span></span>
<span data-ttu-id="e13b9-307">Tanılama ayarları tanılama yapılandırma dosyasına (diagnositcs.wadcfg veya diagnositcs.wadcfgx SDK 2.5 ve sonrası) taşımak için tanılama yapılandırma Tasarımcısı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e13b9-307">Use the diagnostics configuration designer to move diagnostic settings to the diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="e13b9-308">Ayrıca, yüklemenizi tavsiye edilir [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) ve en son Tanılama özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e13b9-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use the latest diagnostics feature.</span></span>

1. <span data-ttu-id="e13b9-309">Yapılandırmak istediğiniz rolü için kısayol menüsünde, Özellikler'i seçin ve ardından yapılandırma sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="e13b9-309">On the shortcut menu for the role that you want to configure, choose Properties, and then choose the Configuration tab.</span></span>
2. <span data-ttu-id="e13b9-310">İçinde **tanılama** bölümünde, olduğundan emin olun **tanılamayı etkinleştir** onay kutusu seçilidir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-310">In the **Diagnostics** section, make sure that the **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="e13b9-311">Seçin **yapılandırma** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e13b9-311">Choose the **Configure** button.</span></span>

   ![Tanılamayı etkinleştir seçeneğine erişme](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="e13b9-313">Bkz: [yapılandırma tanılama Azure Cloud Services ve sanal makineler için](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="e13b9-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="e13b9-314">DbContext nesneleri statik olarak bildirme kaçının</span><span class="sxs-lookup"><span data-stu-id="e13b9-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="e13b9-315">Kimlik</span><span class="sxs-lookup"><span data-stu-id="e13b9-315">ID</span></span>
<span data-ttu-id="e13b9-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="e13b9-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="e13b9-317">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e13b9-317">Description</span></span>
<span data-ttu-id="e13b9-318">Bellek kaydetmek için statik olarak DBContext nesne bildirme kaçının.</span><span class="sxs-lookup"><span data-stu-id="e13b9-318">To save memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="e13b9-319">Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="e13b9-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="e13b9-320">Neden</span><span class="sxs-lookup"><span data-stu-id="e13b9-320">Reason</span></span>
<span data-ttu-id="e13b9-321">DBContext nesneleri her çağrı sorgu sonuçlarından barındırır.</span><span class="sxs-lookup"><span data-stu-id="e13b9-321">DBContext objects hold the query results from each call.</span></span> <span data-ttu-id="e13b9-322">Uygulama etki alanı bellekten kaldırılana kadar statik DBContext nesneler atıldı değil.</span><span class="sxs-lookup"><span data-stu-id="e13b9-322">Static DBContext objects are not disposed until the application domain is unloaded.</span></span> <span data-ttu-id="e13b9-323">Bu nedenle, bir statik DBContext nesnesi, büyük miktarlarda bellek kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="e13b9-324">Çözüm</span><span class="sxs-lookup"><span data-stu-id="e13b9-324">Solution</span></span>
<span data-ttu-id="e13b9-325">Bir yerel değişken ya da statik olmayan örnek alanı olarak DBContext bildirme, bir görev için kullanacağınız ve sonra kullanıldıktan sonra elden sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e13b9-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="e13b9-326">Aşağıdaki örnek MVC denetleyicisi sınıfı DBContext nesnesinin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e13b9-326">The following example MVC controller class shows how to use the DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass to DbContext        
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

## <a name="next-steps"></a><span data-ttu-id="e13b9-327">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e13b9-327">Next steps</span></span>
<span data-ttu-id="e13b9-328">Daha fazla hakkında en iyi duruma getirme ve Azure uygulamaları sorunlarını giderme öğrenmek için bkz: [Visual Studio kullanarak Azure App Service web uygulamasında sorun giderme](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="e13b9-328">To learn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
