---
title: "Yeni bir Azure Application Insights kaynağı aaaCreate | Microsoft Docs"
description: "El ile yeni dinamik bir uygulama için Application Insights izleme işlevini ayarlama."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="a3e04-103">Application Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a3e04-103">Create an Application Insights resource</span></span>
<span data-ttu-id="a3e04-104">Azure Application Insights, Microsoft Azure'da uygulamanızı hakkındaki verileri görüntüler *kaynak*.</span><span class="sxs-lookup"><span data-stu-id="a3e04-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="a3e04-105">Yeni kaynak oluşturma parçasıdır bu nedenle [Application Insights toomonitor yeni bir uygulama ayarı][start].</span><span class="sxs-lookup"><span data-stu-id="a3e04-105">Creating a new resource is therefore part of [setting up Application Insights toomonitor a new application][start].</span></span> <span data-ttu-id="a3e04-106">Çoğu durumda, kaynak oluştururken otomatik olarak IDE hello tarafından yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="a3e04-106">In many cases, creating a resource can be done automatically by hello IDE.</span></span> <span data-ttu-id="a3e04-107">Ancak bazı durumlarda, bir kaynak el ile oluşturmanız - Örneğin, geliştirme ve üretim için ayrı kaynaklar toohave uygulamanızın veya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a3e04-107">But in some cases, you create a resource manually - for example, toohave separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="a3e04-108">Merhaba kaynak oluşturduktan sonra kendi izleme anahtarı edinme ve Merhaba uygulaması bu tooconfigure hello SDK kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3e04-108">After you have created hello resource, you get its instrumentation key and use that tooconfigure hello SDK in hello application.</span></span> <span data-ttu-id="a3e04-109">Merhaba kaynak anahtar bağlantıları telemetri toohello kaynak hello.</span><span class="sxs-lookup"><span data-stu-id="a3e04-109">hello resource key links hello telemetry toohello resource.</span></span>

## <a name="sign-up-toomicrosoft-azure"></a><span data-ttu-id="a3e04-110">Azure tooMicrosoft oturum</span><span class="sxs-lookup"><span data-stu-id="a3e04-110">Sign up tooMicrosoft Azure</span></span>
<span data-ttu-id="a3e04-111">Henüz geldiyseniz bir [Microsoft hesabı, hemen edinin](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="a3e04-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="a3e04-112">(Outlook.com, OneDrive, Windows Phone veya XBox LIVE gibi hizmetleri kullanıyorsanız, zaten bir Microsoft hesabınız vardır.)</span><span class="sxs-lookup"><span data-stu-id="a3e04-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="a3e04-113">Bir abonelik çok etmeniz[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3e04-113">You also need a subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="a3e04-114">Ekibinizin ve kuruluşunuzun bir Azure aboneliğiniz varsa, hello sahibi, tooit, Windows Live ID'nizi kullanarak ekleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a3e04-114">If your team or organization has an Azure subscription, hello owner can add you tooit, using your Windows Live ID.</span></span> <span data-ttu-id="a3e04-115">Yalnızca, kullanım için ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="a3e04-115">You're only charged for what you use.</span></span> <span data-ttu-id="a3e04-116">Merhaba varsayılan temel plan, belirli bir miktar ücretsiz Deneysel kullanım için sağlar.</span><span class="sxs-lookup"><span data-stu-id="a3e04-116">hello default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="a3e04-117">TooApplication bilgiler erişim tooa abonelik var olduğunda oturum [http://portal.azure.com](https://portal.azure.com)ve Live ID toologin kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3e04-117">When you've got access tooa subscription, log in tooApplication Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID toologin.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="a3e04-118">Application Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a3e04-118">Create an Application Insights resource</span></span>
<span data-ttu-id="a3e04-119">Merhaba, [portal.azure.com](https://portal.azure.com), Application Insights kaynağı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a3e04-119">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Yeni, Application Insights öğesine tıklayın](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="a3e04-121">**Uygulama türü** hello genel bakış dikey penceresinde ve hello özellikler kullanılabilir Görünenleri etkiler [ölçüm Gezgini][metrics].</span><span class="sxs-lookup"><span data-stu-id="a3e04-121">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="a3e04-122">Uygulama, türünü görmüyorsanız, genel seçin.</span><span class="sxs-lookup"><span data-stu-id="a3e04-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="a3e04-123">**Abonelik** ödeme hesabınız azure'da.</span><span class="sxs-lookup"><span data-stu-id="a3e04-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="a3e04-124">**Kaynak grubu** özelliklerini yönetmek için kullanışlı olan erişim denetimi ister.</span><span class="sxs-lookup"><span data-stu-id="a3e04-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="a3e04-125">Diğer Azure kaynaklarına zaten oluşturduysanız, tooput bu yeni kaynak hello seçebilirsiniz aynı grubu.</span><span class="sxs-lookup"><span data-stu-id="a3e04-125">If you have already created other Azure resources, you can choose tooput this new resource in hello same group.</span></span>
* <span data-ttu-id="a3e04-126">**Konum** burada biz verilerinizi tutmak olduğu.</span><span class="sxs-lookup"><span data-stu-id="a3e04-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="a3e04-127">**PIN toodashboard** kaynağınız için hızlı erişim kutucuğu, Azure giriş sayfasında koyar.</span><span class="sxs-lookup"><span data-stu-id="a3e04-127">**Pin toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="a3e04-128">Önerilir.</span><span class="sxs-lookup"><span data-stu-id="a3e04-128">Recommended.</span></span>

<span data-ttu-id="a3e04-129">Uygulamanızı oluştururken yeni bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="a3e04-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="a3e04-130">Bu dikey pencere, performans ve kullanım verileri uygulamanız hakkında gördüğünüz ' dir.</span><span class="sxs-lookup"><span data-stu-id="a3e04-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="a3e04-131">tooget geri tooit tooAzure içinde oturum hello uygulamanızın hızlı başlangıç kutucuğu arayın başlatıldığında Panosu (giriş ekranı).</span><span class="sxs-lookup"><span data-stu-id="a3e04-131">tooget back tooit next time you log in tooAzure, look for your app's quick-start tile on hello start board (home screen).</span></span> <span data-ttu-id="a3e04-132">Veya Gözat toofind'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a3e04-132">Or click Browse toofind it.</span></span>

## <a name="copy-hello-instrumentation-key"></a><span data-ttu-id="a3e04-133">Merhaba izleme anahtarını kopyalama</span><span class="sxs-lookup"><span data-stu-id="a3e04-133">Copy hello instrumentation key</span></span>
<span data-ttu-id="a3e04-134">Merhaba izleme anahtarı oluşturduğunuz hello kaynak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a3e04-134">hello instrumentation key identifies hello resource that you created.</span></span> <span data-ttu-id="a3e04-135">Bu toogive toohello SDK gerekir.</span><span class="sxs-lookup"><span data-stu-id="a3e04-135">You need it toogive toohello SDK.</span></span>

![Essentials'ı tıklatın, hello izleme anahtarı, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a><span data-ttu-id="a3e04-137">Uygulamanızda Hello SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="a3e04-137">Install hello SDK in your app</span></span>
<span data-ttu-id="a3e04-138">Merhaba Application Insights SDK'sı, uygulamanızın yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a3e04-138">Install hello Application Insights SDK in your app.</span></span> <span data-ttu-id="a3e04-139">Bu adım, son derece uygulamanızın hello türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a3e04-139">This step depends heavily on hello type of your application.</span></span> 

<span data-ttu-id="a3e04-140">Merhaba araçları anahtar tooconfigure kullanmak [uygulamanızda yüklediğiniz SDK hello][start].</span><span class="sxs-lookup"><span data-stu-id="a3e04-140">Use hello instrumentation key tooconfigure [hello SDK that you install in your application][start].</span></span>

<span data-ttu-id="a3e04-141">Merhaba SDK telemetri toowrite kalmadan herhangi bir kod Gönder Standart modüller içerir.</span><span class="sxs-lookup"><span data-stu-id="a3e04-141">hello SDK includes standard modules that send telemetry without you having toowrite any code.</span></span> <span data-ttu-id="a3e04-142">tootrack kullanıcı eylemleri veya daha fazla ayrıntı sorunları tanılamak [hello API kullanan] [ api] toosend kendi telemetrinizi.</span><span class="sxs-lookup"><span data-stu-id="a3e04-142">tootrack user actions or diagnose issues in more detail, [use hello API][api] toosend your own telemetry.</span></span>

## <span data-ttu-id="a3e04-143"><a name="monitor"></a>Telemetri verileri bakın</span><span class="sxs-lookup"><span data-stu-id="a3e04-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="a3e04-144">Kapat hello hızlı hello Azure portal dikey penceresinde tooreturn tooyour uygulama Dikey başlatın.</span><span class="sxs-lookup"><span data-stu-id="a3e04-144">Close hello quick start blade tooreturn tooyour application blade in hello Azure portal.</span></span>

<span data-ttu-id="a3e04-145">Merhaba arama döşeme toosee tıklatın [tanılama arama][diagnostic], burada hello ilk olaylar görünür.</span><span class="sxs-lookup"><span data-stu-id="a3e04-145">Click hello Search tile toosee [Diagnostic Search][diagnostic], where hello first events appear.</span></span> 

<span data-ttu-id="a3e04-146">Daha fazla veri bekliyorsunuz tıklatmak **yenileme** birkaç saniye sonra.</span><span class="sxs-lookup"><span data-stu-id="a3e04-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="a3e04-147">Bir kaynak otomatik olarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="a3e04-147">Creating a resource automatically</span></span>
<span data-ttu-id="a3e04-148">Yazma bir [PowerShell Betiği](app-insights-powershell.md) toocreate kaynak otomatik olarak.</span><span class="sxs-lookup"><span data-stu-id="a3e04-148">You can write a [PowerShell script](app-insights-powershell.md) toocreate a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3e04-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a3e04-149">Next steps</span></span>
* [<span data-ttu-id="a3e04-150">Pano oluşturma</span><span class="sxs-lookup"><span data-stu-id="a3e04-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="a3e04-151">Tanılama Araması</span><span class="sxs-lookup"><span data-stu-id="a3e04-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="a3e04-152">Ölçümleri keşfetme</span><span class="sxs-lookup"><span data-stu-id="a3e04-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="a3e04-153">Analytics sorguları yazma</span><span class="sxs-lookup"><span data-stu-id="a3e04-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

