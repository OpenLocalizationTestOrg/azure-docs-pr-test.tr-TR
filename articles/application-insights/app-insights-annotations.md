---
title: "Yayın Application Insights için ek açıklamalar | Microsoft Docs"
description: "Dağıtım ekleme veya Application Insights, ölçümleri explorer grafiklerde işaretleyicileri oluşturabilirsiniz."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: f7eb2f3cba535eb64db5544c498289c9e895987a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="937a0-103">Application ınsights'ta ölçüm grafiklerde ek açıklamaları</span><span class="sxs-lookup"><span data-stu-id="937a0-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="937a0-104">Ek açıklamalar [ölçüm Gezgini](app-insights-metrics-explorer.md) grafikleri Göster yeni bir yapı veya diğer önemli olay dağıtıldığı.</span><span class="sxs-lookup"><span data-stu-id="937a0-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="937a0-105">Bunlar değişikliklerinizi uygulamanızın performansı üzerinde hiçbir etkisi sahip olup olmadığını görmek kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="937a0-105">They make it easy to see whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="937a0-106">Tarafından otomatik olarak oluşturulabilir [Visual Studio Team Services yapı sistem](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="937a0-106">They can be automatically created by the [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="937a0-107">Tarafından gibi herhangi bir olay bayrak için ek açıklama oluşturabilirsiniz [Powershell'den oluşturma](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="937a0-107">You can also create annotations to flag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Sunucu yanıt süresi ile görünür bağıntı ile ek açıklama örneği](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="937a0-109">VSTS derleme ile yayın ek açıklama</span><span class="sxs-lookup"><span data-stu-id="937a0-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="937a0-110">Yayın ek açıklamalar, bulut tabanlı derleme özelliğidir ve Visual Studio Team Services hizmeti bırakın.</span><span class="sxs-lookup"><span data-stu-id="937a0-110">Release annotations are a feature of the cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-the-annotations-extension-one-time"></a><span data-ttu-id="937a0-111">Ek açıklamalar uzantısını (bir kez) yükleyin</span><span class="sxs-lookup"><span data-stu-id="937a0-111">Install the Annotations extension (one time)</span></span>
<span data-ttu-id="937a0-112">Yayın ek açıklamaları oluşturabilecek için Visual Studio Market'te bulunabilir birçok takım hizmet uzantılardan birine yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="937a0-112">To be able to create release annotations, you'll need to install one of the many Team Service extensions available in the Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="937a0-113">Oturum açın, [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) projesi.</span><span class="sxs-lookup"><span data-stu-id="937a0-113">Sign in to your [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="937a0-114">Visual Studio pazarında [yayın ek açıklamaları uzantı alınmaya](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)ve Team Services hesabınıza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="937a0-114">In Visual Studio Marketplace, [get the Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it to your Team Services account.</span></span>

![AT Team Services web sayfasının açık Market sağ üst.](./media/app-insights-annotations/10.png)

<span data-ttu-id="937a0-117">Yalnızca bu kez Visual Studio Team Services hesabınız için yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="937a0-117">You only need to do this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="937a0-118">Yayın ek açıklamaları artık hesabınıza herhangi bir projede için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="937a0-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="937a0-119">Yayın ek açıklamaları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="937a0-119">Configure release annotations</span></span>

<span data-ttu-id="937a0-120">Her VSTS yayın şablonu için ayrı bir API anahtarı edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="937a0-120">You need to get a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="937a0-121">Oturum [Microsoft Azure portalı](https://portal.azure.com) ve uygulamanızı izler Application Insights kaynağı açın.</span><span class="sxs-lookup"><span data-stu-id="937a0-121">Sign in to the [Microsoft Azure Portal](https://portal.azure.com) and open the Application Insights resource that monitors your application.</span></span> <span data-ttu-id="937a0-122">(Veya [şimdi oluşturmak](app-insights-overview.md), henüz yapmadıysanız.)</span><span class="sxs-lookup"><span data-stu-id="937a0-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="937a0-123">Açık **API erişimini**, **uygulama Öngörüler kimliği**.</span><span class="sxs-lookup"><span data-stu-id="937a0-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![Portal.Azure.com adresinde Application Insights kaynağınıza açın ve Ayarlar'ı seçin.](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="937a0-127">Ayrı bir tarayıcı penceresi açın (veya oluşturun) Visual Studio Team Services dağıtımlarınızı yönetir yayın şablonu.</span><span class="sxs-lookup"><span data-stu-id="937a0-127">In a separate browser window, open (or create) the release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="937a0-128">Bir görev eklemek ve uygulama Öngörüler yayın ek açıklama görev menüsünden seçin.</span><span class="sxs-lookup"><span data-stu-id="937a0-128">Add a task, and select the Application Insights Release Annotation task from the menu.</span></span>
   
    <span data-ttu-id="937a0-129">Yapıştır **uygulama kimliği** API erişimini dikey penceresinden kopyaladığınız.</span><span class="sxs-lookup"><span data-stu-id="937a0-129">Paste the **Application Id** that you copied from the API Access blade.</span></span>
   
    ![Visual Studio Team Services sürüm açın, bir yayın tanımı seçin ve Düzenle'yi seçin.](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="937a0-133">Ayarlama **apikey ile yapılan** bir değişkene alan `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="937a0-133">Set the **APIKey** field to a variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="937a0-134">Azure penceresine geri döndüğünüzde yeni bir API anahtar oluşturun ve bir kopyasını alın.</span><span class="sxs-lookup"><span data-stu-id="937a0-134">Back in the Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![Azure penceresinde API erişimini dikey penceresinde API anahtarı oluştur'a tıklayın.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="937a0-138">Yayın şablonu yapılandırma sekmesini açın.</span><span class="sxs-lookup"><span data-stu-id="937a0-138">Open the Configuration tab of the release template.</span></span>
   
    <span data-ttu-id="937a0-139">İçin bir değişken tanımı oluşturun `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="937a0-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="937a0-140">API anahtarınıza apikey ile yapılan değişken tanımını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="937a0-140">Paste your API key to the ApiKey variable definition.</span></span>
   
    ![Team Services penceresinde yapılandırma sekmesini seçin ve değişken Ekle'yi tıklatın.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="937a0-143">Son olarak, **kaydetmek** yayın tanımı.</span><span class="sxs-lookup"><span data-stu-id="937a0-143">Finally, **Save** the release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="937a0-144">Görünüm ek açıklamaları</span><span class="sxs-lookup"><span data-stu-id="937a0-144">View annotations</span></span>
<span data-ttu-id="937a0-145">Artık, yeni bir sürüm dağıtmak için yayın şablonu kullandığınızda, ek açıklamanın Application Insights'a gönderilir.</span><span class="sxs-lookup"><span data-stu-id="937a0-145">Now, whenever you use the release template to deploy a new release, an annotation will be sent to Application Insights.</span></span> <span data-ttu-id="937a0-146">Ek açıklamalar ölçüm Gezgini grafiklerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="937a0-146">The annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="937a0-147">İstek sahibi, kaynak denetimi dalı dahil olmak üzere, yayın ayrıntılarını açmak için hiçbir ek açıklama işaretçisi tıklayın, tanımı, ortam ve daha fazlasını bırakın.</span><span class="sxs-lookup"><span data-stu-id="937a0-147">Click on any annotation marker to open details about the release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Tüm yayın ek açıklama işaretçisi'ı tıklatın.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="937a0-149">Özel ek açıklama Powershell'den oluşturma</span><span class="sxs-lookup"><span data-stu-id="937a0-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="937a0-150">(VS Team System kullanmadan) gibi herhangi bir işlem ek açıklamaları da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="937a0-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="937a0-151">Yerel bir kopyasını [Powershell betiği github'dan](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="937a0-151">Make a local copy of the [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="937a0-152">Uygulama Kimliği alın ve API erişimini dikey penceresinden bir API anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="937a0-152">Get the Application ID and create an API key from the API Access blade.</span></span>

3. <span data-ttu-id="937a0-153">Bu gibi komut dosyası çağırın:</span><span class="sxs-lookup"><span data-stu-id="937a0-153">Call the script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="937a0-154">Ek açıklamalar için geçmiş oluşturmak örnek için betik değiştirmek çok kolaydır.</span><span class="sxs-lookup"><span data-stu-id="937a0-154">It's easy to modify the script, for example to create annotations for the past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="937a0-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="937a0-155">Next steps</span></span>

* [<span data-ttu-id="937a0-156">İş öğeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="937a0-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="937a0-157">PowerShell ile Automation</span><span class="sxs-lookup"><span data-stu-id="937a0-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
