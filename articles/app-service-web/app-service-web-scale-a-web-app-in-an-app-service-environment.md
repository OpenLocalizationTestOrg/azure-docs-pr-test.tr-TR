---
title: "Bir uygulama hizmeti ortamı'nda bir uygulama ölçeklendirme"
description: "Bir uygulama hizmeti ortamı'nda bir uygulama ölçeklendirme"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: jimbe
ms.assetid: 78eb1e49-4fcd-49e7-b3c7-f1906f0f22e3
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: ccompy
ms.openlocfilehash: 240c2486c23b7cd84e2471bf5b2170e08ee1f150
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="scaling-apps-in-an-app-service-environment"></a><span data-ttu-id="bcb84-103">App Service Ortamında uygulamaları ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="bcb84-103">Scaling apps in an App Service Environment</span></span>
<span data-ttu-id="bcb84-104">Azure App Service'te normal şekilde ölçeklendirebilirsiniz üç şey vardır:</span><span class="sxs-lookup"><span data-stu-id="bcb84-104">In the Azure App Service there are normally three things you can scale:</span></span>

* <span data-ttu-id="bcb84-105">plan fiyatlandırması</span><span class="sxs-lookup"><span data-stu-id="bcb84-105">pricing plan</span></span>
* <span data-ttu-id="bcb84-106">çalışan boyutu</span><span class="sxs-lookup"><span data-stu-id="bcb84-106">worker size</span></span> 
* <span data-ttu-id="bcb84-107">örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="bcb84-107">number of instances.</span></span>

<span data-ttu-id="bcb84-108">ASE'de seçmek veya fiyatlandırma planı değiştirmek için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="bcb84-108">In an ASE there is no need to select or change the pricing plan.</span></span>  <span data-ttu-id="bcb84-109">Özellikleri bakımından Premium yetenek düzeyi fiyatlandırma zaten var.</span><span class="sxs-lookup"><span data-stu-id="bcb84-109">In terms of capabilities it is already at a Premium pricing capability level.</span></span>  

<span data-ttu-id="bcb84-110">Çalışan boyutları göre ana yönetim için her çalışan havuzunda kullanılacak işlem kaynak boyutu atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bcb84-110">With respect to worker sizes, the ASE admin can assign the size of the compute resource to be used for each worker pool.</span></span>  <span data-ttu-id="bcb84-111">P4 işlem kaynakları ile çalışan havuzu 1 olabilir ve çalışan Havuz 2 P1 ile işlem kaynakları, isterseniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="bcb84-111">That means you can have Worker Pool 1 with P4 compute resources and Worker Pool 2 with P1 compute resources, if desired.</span></span>  <span data-ttu-id="bcb84-112">Boyutu olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="bcb84-112">They do not have to be in size order.</span></span>  <span data-ttu-id="bcb84-113">Belgeyi burada boyutları ve bunların fiyatlandırma ayrıntıları görmek için [Azure App Service fiyatlandırması][AppServicePricing].</span><span class="sxs-lookup"><span data-stu-id="bcb84-113">For details around the sizes and their pricing see the document here [Azure App Service Pricing][AppServicePricing].</span></span>  <span data-ttu-id="bcb84-114">Bu, bir uygulama hizmeti olarak ortamında web uygulamaları ve App Service planları için ölçeklendirme seçenekleri bırakır:</span><span class="sxs-lookup"><span data-stu-id="bcb84-114">This leaves the scaling options for web apps and App Service Plans in an App Service Environment to be:</span></span>

* <span data-ttu-id="bcb84-115">çalışan havuzu seçimi</span><span class="sxs-lookup"><span data-stu-id="bcb84-115">worker pool selection</span></span>
* <span data-ttu-id="bcb84-116">örnek sayısı</span><span class="sxs-lookup"><span data-stu-id="bcb84-116">number of instances</span></span>

<span data-ttu-id="bcb84-117">Her iki öğeyi değiştirme App Service planları, ana barındırılan için gösterilen uygun kullanıcı Arabirimi aracılığıyla gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="bcb84-117">Changing either item is done through the appropriate UI shown for your ASE hosted App Service Plans.</span></span>  

![][1]

<span data-ttu-id="bcb84-118">ASP bulunduğu çalışan havuzunda kullanılabilir işlem kaynakları sayısı ötesinde, ASP ölçeklendirin olamaz.</span><span class="sxs-lookup"><span data-stu-id="bcb84-118">You can't scale up your ASP beyond the number of available compute resources in the worker pool that your ASP is in.</span></span>  <span data-ttu-id="bcb84-119">İşlem kaynaklarını çalışan havuzda varsa bunları eklemek için ana yöneticinize almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bcb84-119">If you need compute resources in that worker pool you need to get your ASE administrator to add them.</span></span>  <span data-ttu-id="bcb84-120">Burada yer alan bilgiler, ana yeniden yapılandırma geçici bilgileri okumak için: [bir uygulama hizmeti ortamını yapılandırma][HowtoConfigureASE].</span><span class="sxs-lookup"><span data-stu-id="bcb84-120">For information around re-configuring your ASE read the information here: [How to Configure an App Service environment][HowtoConfigureASE].</span></span>  <span data-ttu-id="bcb84-121">Zamanlama veya ölçümleri kapasite göre eklemek için ana otomatik ölçeklendirme özelliklerden yararlanmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bcb84-121">You may also want to take advantage of the ASE autoscale features to add capacity based on schedule or metrics.</span></span>  <span data-ttu-id="bcb84-122">Yapılandırma hakkında daha fazla bilgi almak için otomatik ölçeklendirme ana ortamı için bkz: [otomatik ölçeklendirme bir uygulama hizmeti ortamı için yapılandırma][ASEAutoscale].</span><span class="sxs-lookup"><span data-stu-id="bcb84-122">To get more details on configuring autoscale for the ASE environment itself see [How to configure autoscale for an App Service Environment][ASEAutoscale].</span></span>

<span data-ttu-id="bcb84-123">Birden çok uygulama farklı çalışan havuzlarından işlem kaynakları kullanılarak hizmet planları oluşturabilir veya aynı çalışan havuzu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bcb84-123">You can create multiple app service plans using compute resources from different worker pools, or you can use the same worker pool.</span></span>  <span data-ttu-id="bcb84-124">(4) kullanan çalışan havuzu 1'de (10) kullanılabilir işlem kaynakları varsa, (6) işlem kaynaklarını kullanan bir uygulama hizmeti planı oluşturmak seçebilirsiniz ve ikinci bir app service planı örneğin işlem kaynaklarını.</span><span class="sxs-lookup"><span data-stu-id="bcb84-124">For example if you have (10) available compute resources in Worker Pool 1, you can choose to create one app service plan using (6) compute resources, and a second app service plan that uses (4) compute resources.</span></span>

### <a name="scaling-the-number-of-instances"></a><span data-ttu-id="bcb84-125">Örnek sayısı ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="bcb84-125">Scaling the number of instances</span></span>
<span data-ttu-id="bcb84-126">Uygulama hizmeti ortamı'nda ilk web uygulamanızı oluşturduğunuzda ile 1 bir örneğini başlatır.</span><span class="sxs-lookup"><span data-stu-id="bcb84-126">When you first create your web app in an App Service Environment it starts with 1 instance.</span></span>  <span data-ttu-id="bcb84-127">Ardından çıkışı uygulamanız için ek işlem kaynaklarını sağlamaya ek örnekleri ölçekleme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bcb84-127">You can then scale out to additional instances to provide additional compute resources for your app.</span></span>   

<span data-ttu-id="bcb84-128">Ana yeterli kapasitesi varsa, daha sonra bu oldukça basittir.</span><span class="sxs-lookup"><span data-stu-id="bcb84-128">If your ASE has enough capacity then this is pretty simple.</span></span>  <span data-ttu-id="bcb84-129">Uygulama hizmeti ölçeği artırma ve ölçek seçmek istediğiniz siteleri tutan planınız için gidin.</span><span class="sxs-lookup"><span data-stu-id="bcb84-129">You go to your App Service Plan that holds the sites you want to scale up and select Scale.</span></span>  <span data-ttu-id="bcb84-130">Bu, burada el ile ölçek, ASP ayarlayabilir veya ASP için otomatik ölçeklendirme kurallarını yapılandırma kullanıcı arabirimini açar.</span><span class="sxs-lookup"><span data-stu-id="bcb84-130">This opens the UI where you can manually set the scale for your ASP or configure autoscale rules for your ASP.</span></span>  <span data-ttu-id="bcb84-131">El ile uygulamanız yeterlidir ölçeklendirme için ayarlanmış ***göre Ölçeklendirmeniz*** için ***el ile girdiğim bir örnek sayısı***.</span><span class="sxs-lookup"><span data-stu-id="bcb84-131">To manually scale your app simply set ***Scale by*** to ***an instance count that I enter manually***.</span></span>  <span data-ttu-id="bcb84-132">Buradan istenen miktar kaydırıcıyı sürükleyin ya da kaydırıcıyı yanındaki kutuya girin.</span><span class="sxs-lookup"><span data-stu-id="bcb84-132">From here either drag the slider to the desired quantity or enter it in the box next to the slider.</span></span>  

![][2] 

<span data-ttu-id="bcb84-133">Bunlar her zamanki gibi bir ana bir ASP için otomatik ölçeklendirme kurallarını aynı çalışır.</span><span class="sxs-lookup"><span data-stu-id="bcb84-133">The autoscale rules for an ASP in an ASE work the same as they do normally.</span></span>  <span data-ttu-id="bcb84-134">Seçebileceğiniz ***CPU yüzdesi*** altında ***göre Ölçeklendirmeniz*** ve CPU yüzdesi veya, göre ASP kullanarak daha karmaşık kurallar oluşturabilirsiniz için otomatik ölçeklendirme kuralları oluşturmak ***zamanlama ve performans kuralları ***.</span><span class="sxs-lookup"><span data-stu-id="bcb84-134">You can select ***CPU Percentage*** under ***Scale by*** and create autoscale rules for your ASP based on CPU Percentage or you can create more complex rules using ***schedule and performance rules***.</span></span>  <span data-ttu-id="bcb84-135">Yapılandırma hakkında daha kapsamlı ayrıntıları görmek için otomatik ölçeklendirme kullanmak Kılavuzu burada [bir uygulama Azure App Service'te ölçeklendirme][AppScale].</span><span class="sxs-lookup"><span data-stu-id="bcb84-135">To see more complete details on configuring autoscale use the guide here [Scale an app in Azure App Service][AppScale].</span></span> 

### <a name="worker-pool-selection"></a><span data-ttu-id="bcb84-136">Çalışan havuzu seçimi</span><span class="sxs-lookup"><span data-stu-id="bcb84-136">Worker Pool selection</span></span>
<span data-ttu-id="bcb84-137">Daha önce belirtildiği gibi çalışan havuzu seçimi ASP Arabiriminden erişilir.</span><span class="sxs-lookup"><span data-stu-id="bcb84-137">As noted earlier, the worker pool selection is accessed from the ASP UI.</span></span>  <span data-ttu-id="bcb84-138">Ölçek ve çalışan havuzunda seçmek için istediğiniz ASP için dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="bcb84-138">Open the blade for the ASP that you want to scale and select worker pool.</span></span>  <span data-ttu-id="bcb84-139">Tüm uygulama hizmeti ortamı'nda yapılandırılan çalışan havuzlarında görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="bcb84-139">You will see all of the worker pools which you have configured in your App Service Environment.</span></span>  <span data-ttu-id="bcb84-140">Yalnızca bir çalışan havuzu varsa listelenen bir havuz yalnızca görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="bcb84-140">If you have only one worker pool then you will only see the one pool listed.</span></span>  <span data-ttu-id="bcb84-141">ASP bulunduğu hangi çalışan havuzunu değiştirmek için yalnızca uygulama hizmeti taşımak için planınız istediğiniz çalışan havuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="bcb84-141">To change what worker pool your ASP is in, you simply select the worker pool you want your App Service Plan to move to.</span></span>  

![][3]

<span data-ttu-id="bcb84-142">ASP bir çalışan havuzundan diğerine geçmeden önce ASP için yeterli kapasiteye sahip emin olmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="bcb84-142">Before moving your ASP from one worker pool to another it is important to make sure you will have adequate capacity for your ASP.</span></span>  <span data-ttu-id="bcb84-143">Çalışan havuzlarında listesinde yalnızca çalışan havuzu adı listelenen ancak, kaç tane çalışanları, çalışan havuzunda kullanılabilir olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bcb84-143">In the list of worker pools, not only is the worker pool name listed but you can also see how many workers are available in that worker pool.</span></span>  <span data-ttu-id="bcb84-144">Yeterli örnekleri içeren uygulama hizmeti planınız kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="bcb84-144">Make sure that there are enough instances available to contain your App Service Plan.</span></span>  <span data-ttu-id="bcb84-145">Daha fazla işlem kaynaklarını taşımak istediğiniz çalışan havuzunda varsa, bunları eklemek için ana yöneticinize alın.</span><span class="sxs-lookup"><span data-stu-id="bcb84-145">If you need more compute resources in the worker pool you wish to move to, then get your ASE administrator to add them.</span></span>  

> [!NOTE]
> <span data-ttu-id="bcb84-146">Bu ASP uygulamalarının bir çalışan havuzundan bir ASP soğuk neden olacak taşıma başlatır.</span><span class="sxs-lookup"><span data-stu-id="bcb84-146">Moving an ASP from one worker pool will cause cold starts of the apps in that ASP.</span></span>  <span data-ttu-id="bcb84-147">Bu istekleri uygulamanızı yeni işlem kaynakları üzerinde çalışmaya soğuk olarak yavaş çalışmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="bcb84-147">This can cause requests to run slowly as your app is cold started on the new compute resources.</span></span>  <span data-ttu-id="bcb84-148">Soğuk başlangıç kullanılarak önlenebilir [uygulama yeteneğini sıcak] [ AppWarmup] Azure App Service'te.</span><span class="sxs-lookup"><span data-stu-id="bcb84-148">The cold start can be avoided by using the [application warm up capability][AppWarmup] in Azure App Service.</span></span>  <span data-ttu-id="bcb84-149">Yeni işlem kaynakları üzerinde çalışmaya uygulamaları soğuk olduğunda başlatma işlemi de çağrılan çünkü makalede açıklanan uygulama başlatma modül soğuk başlıyor de çalışır.</span><span class="sxs-lookup"><span data-stu-id="bcb84-149">The Application Initialization module described in the article also works for cold starts because the initialization process is also invoked when apps are cold started on new compute resources.</span></span> 
> 
> 

## <a name="getting-started"></a><span data-ttu-id="bcb84-150">Başlarken</span><span class="sxs-lookup"><span data-stu-id="bcb84-150">Getting started</span></span>
<span data-ttu-id="bcb84-151">Uygulama hizmeti ortamları ile çalışmaya başlamak için bkz: [nasıl için oluşturma bir uygulama hizmeti ortamı][HowtoCreateASE]</span><span class="sxs-lookup"><span data-stu-id="bcb84-151">To get started with App Service Environments, see [How To Create An App Service Environment][HowtoCreateASE]</span></span>

<span data-ttu-id="bcb84-152">Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="bcb84-152">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<!--Image references-->
[1]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-aspblade.png
[2]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-manualscale.png
[3]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-sizescale.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ScaleWebapp]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[CreateWebappinASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-a-web-app-in-an-ase/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[AppScale]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[AppWarmup]: http://ruslany.net/2015/09/how-to-warm-up-azure-web-app-during-deployment-slots-swap/
