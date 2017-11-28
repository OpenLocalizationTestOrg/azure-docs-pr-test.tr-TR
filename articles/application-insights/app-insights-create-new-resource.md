---
title: "Yeni bir Azure Application Insights kaynağı oluşturun | Microsoft Docs"
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
ms.openlocfilehash: 5f8814ee943424c1c278ab3732129d4459f83819
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="1cb5a-103">Application Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cb5a-103">Create an Application Insights resource</span></span>
<span data-ttu-id="1cb5a-104">Azure Application Insights, Microsoft Azure'da uygulamanızı hakkındaki verileri görüntüler *kaynak*.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="1cb5a-105">Yeni kaynak oluşturma parçasıdır bu nedenle [yeni bir uygulama izlemek için Application Insights'ı ayarlama][start].</span><span class="sxs-lookup"><span data-stu-id="1cb5a-105">Creating a new resource is therefore part of [setting up Application Insights to monitor a new application][start].</span></span> <span data-ttu-id="1cb5a-106">Çoğu durumda, kaynak oluştururken otomatik olarak IDE tarafından yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-106">In many cases, creating a resource can be done automatically by the IDE.</span></span> <span data-ttu-id="1cb5a-107">Ancak bazı durumlarda, bir kaynak el ile - Örneğin, geliştirme için ayrı kaynaklarınız için oluşturduğunuz ve uygulamanızın veya üretim oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-107">But in some cases, you create a resource manually - for example, to have separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="1cb5a-108">Kaynak oluşturduktan sonra kendi izleme anahtarı edinme ve, uygulama SDK'yı yapılandırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-108">After you have created the resource, you get its instrumentation key and use that to configure the SDK in the application.</span></span> <span data-ttu-id="1cb5a-109">Kaynak anahtarı telemetri kaynağına bağlar.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-109">The resource key links the telemetry to the resource.</span></span>

## <a name="sign-up-to-microsoft-azure"></a><span data-ttu-id="1cb5a-110">Microsoft Azure'a kaydolun</span><span class="sxs-lookup"><span data-stu-id="1cb5a-110">Sign up to Microsoft Azure</span></span>
<span data-ttu-id="1cb5a-111">Henüz geldiyseniz bir [Microsoft hesabı, hemen edinin](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="1cb5a-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="1cb5a-112">(Outlook.com, OneDrive, Windows Phone veya XBox LIVE gibi hizmetleri kullanıyorsanız, zaten bir Microsoft hesabınız vardır.)</span><span class="sxs-lookup"><span data-stu-id="1cb5a-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="1cb5a-113">Ayrıca bir aboneliğe ihtiyacınız [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="1cb5a-113">You also need a subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="1cb5a-114">Ekibinizin ve kuruluşunuzun bir Azure aboneliğiniz varsa, sahibi, Windows Live ID'nizi kullanarak ekleyebileceğiniz</span><span class="sxs-lookup"><span data-stu-id="1cb5a-114">If your team or organization has an Azure subscription, the owner can add you to it, using your Windows Live ID.</span></span> <span data-ttu-id="1cb5a-115">Yalnızca, kullanım için ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-115">You're only charged for what you use.</span></span> <span data-ttu-id="1cb5a-116">Belirli bir miktar ücretsiz Deneysel kullanım için varsayılan temel plan sağlar.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-116">The default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="1cb5a-117">Bir abonelik erişimi var olduğunda Application Insights oturum [http://portal.azure.com](https://portal.azure.com)ve Live ID'nizi oturum açmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-117">When you've got access to a subscription, log in to Application Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID to login.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="1cb5a-118">Application Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cb5a-118">Create an Application Insights resource</span></span>
<span data-ttu-id="1cb5a-119">İçinde [portal.azure.com](https://portal.azure.com), Application Insights kaynağı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1cb5a-119">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Yeni, Application Insights öğesine tıklayın](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="1cb5a-121">**Uygulama türü** genel bakış dikey penceresinde ve kullanılabilir özellikler Görünenleri etkiler [ölçüm Gezgini][metrics].</span><span class="sxs-lookup"><span data-stu-id="1cb5a-121">**Application type** affects what you see on the overview blade and the properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="1cb5a-122">Uygulama, türünü görmüyorsanız, genel seçin.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="1cb5a-123">**Abonelik** ödeme hesabınız azure'da.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="1cb5a-124">**Kaynak grubu** özelliklerini yönetmek için kullanışlı olan erişim denetimi ister.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="1cb5a-125">Diğer Azure kaynaklarına zaten oluşturduysanız, bu yeni kaynak aynı gruba yerleştirmek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-125">If you have already created other Azure resources, you can choose to put this new resource in the same group.</span></span>
* <span data-ttu-id="1cb5a-126">**Konum** burada biz verilerinizi tutmak olduğu.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="1cb5a-127">**Panoya Sabitle** kaynağınız için hızlı erişim kutucuğu, Azure giriş sayfasında koyar.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-127">**Pin to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="1cb5a-128">Önerilir.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-128">Recommended.</span></span>

<span data-ttu-id="1cb5a-129">Uygulamanızı oluştururken yeni bir dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="1cb5a-130">Bu dikey pencere, performans ve kullanım verileri uygulamanız hakkında gördüğünüz ' dir.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="1cb5a-131">İçin bir sonraki Azure'a oturum açışınızda dönmek için uygulamanızın hızlı başlangıç döşeme başlangıç panosunda (giriş ekranı) arayın.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-131">To get back to it next time you log in to Azure, look for your app's quick-start tile on the start board (home screen).</span></span> <span data-ttu-id="1cb5a-132">Veya dosyayı bulmak için Gözat'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-132">Or click Browse to find it.</span></span>

## <a name="copy-the-instrumentation-key"></a><span data-ttu-id="1cb5a-133">İzleme anahtarını kopyalama</span><span class="sxs-lookup"><span data-stu-id="1cb5a-133">Copy the instrumentation key</span></span>
<span data-ttu-id="1cb5a-134">İzleme anahtarını oluşturduğunuz kaynak tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-134">The instrumentation key identifies the resource that you created.</span></span> <span data-ttu-id="1cb5a-135">SDK vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-135">You need it to give to the SDK.</span></span>

![Essentials'ı tıklatın, CTRL + C izleme anahtarı](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-the-sdk-in-your-app"></a><span data-ttu-id="1cb5a-137">Uygulamanıza SDK yükleme</span><span class="sxs-lookup"><span data-stu-id="1cb5a-137">Install the SDK in your app</span></span>
<span data-ttu-id="1cb5a-138">Application Insights SDK, uygulamayı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-138">Install the Application Insights SDK in your app.</span></span> <span data-ttu-id="1cb5a-139">Bu adım, yoğun bir şekilde uygulamanızı türüne göre değişir.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-139">This step depends heavily on the type of your application.</span></span> 

<span data-ttu-id="1cb5a-140">İzleme anahtarını yapılandırmak için kullanın [uygulamanızda yüklediğiniz SDK][start].</span><span class="sxs-lookup"><span data-stu-id="1cb5a-140">Use the instrumentation key to configure [the SDK that you install in your application][start].</span></span>

<span data-ttu-id="1cb5a-141">SDK'sı telemetri herhangi bir kod yazmaya gerek kalmadan Gönder Standart modüller içerir.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-141">The SDK includes standard modules that send telemetry without you having to write any code.</span></span> <span data-ttu-id="1cb5a-142">Kullanıcı eylemlerini izlemek veya daha fazla ayrıntı sorunları tanılamak için [API kullanan] [ api] kendi telemetrinizi göndermek için.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-142">To track user actions or diagnose issues in more detail, [use the API][api] to send your own telemetry.</span></span>

## <span data-ttu-id="1cb5a-143"><a name="monitor"></a>Telemetri verileri bakın</span><span class="sxs-lookup"><span data-stu-id="1cb5a-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="1cb5a-144">Azure portalında uygulama dikey pencerenize geri dönmek için hızlı başlangıç dikey penceresini kapatın.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-144">Close the quick start blade to return to your application blade in the Azure portal.</span></span>

<span data-ttu-id="1cb5a-145">Görmek için arama kutucuğuna tıklayın [tanılama arama][diagnostic], ilk olayları burada görünür.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-145">Click the Search tile to see [Diagnostic Search][diagnostic], where the first events appear.</span></span> 

<span data-ttu-id="1cb5a-146">Daha fazla veri bekliyorsunuz tıklatmak **yenileme** birkaç saniye sonra.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="1cb5a-147">Bir kaynak otomatik olarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cb5a-147">Creating a resource automatically</span></span>
<span data-ttu-id="1cb5a-148">Yazma bir [PowerShell Betiği](app-insights-powershell.md) otomatik olarak bir kaynak oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="1cb5a-148">You can write a [PowerShell script](app-insights-powershell.md) to create a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1cb5a-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1cb5a-149">Next steps</span></span>
* [<span data-ttu-id="1cb5a-150">Pano oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cb5a-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="1cb5a-151">Tanılama Araması</span><span class="sxs-lookup"><span data-stu-id="1cb5a-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="1cb5a-152">Ölçümleri keşfetme</span><span class="sxs-lookup"><span data-stu-id="1cb5a-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="1cb5a-153">Analytics sorguları yazma</span><span class="sxs-lookup"><span data-stu-id="1cb5a-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

