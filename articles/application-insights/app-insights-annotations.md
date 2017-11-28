---
title: "Application Insights için aaaRelease ek açıklamalar | Microsoft Docs"
description: "Dağıtım ekleme veya tooyour ölçümleri explorer Application Insights grafiklerde işaretçileri oluşturabilirsiniz."
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
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="f5046-103">Application ınsights'ta ölçüm grafiklerde ek açıklamaları</span><span class="sxs-lookup"><span data-stu-id="f5046-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="f5046-104">Ek açıklamalar [ölçüm Gezgini](app-insights-metrics-explorer.md) grafikleri Göster yeni bir yapı veya diğer önemli olay dağıtıldığı.</span><span class="sxs-lookup"><span data-stu-id="f5046-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="f5046-105">Uygulamanızın performansı üzerinde hiçbir etkisi değişikliklerinizi verip vermediğini bunlar kolay toosee kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="f5046-105">They make it easy toosee whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="f5046-106">Merhaba tarafından otomatik olarak oluşturulabilir [Visual Studio Team Services yapı sistem](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="f5046-106">They can be automatically created by hello [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="f5046-107">Ek açıklamalar tooflag tarafından gibi herhangi bir olay oluşturabilirsiniz [Powershell'den oluşturma](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="f5046-107">You can also create annotations tooflag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Sunucu yanıt süresi ile görünür bağıntı ile ek açıklama örneği](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="f5046-109">VSTS derleme ile yayın ek açıklama</span><span class="sxs-lookup"><span data-stu-id="f5046-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="f5046-110">Yayın ek açıklamaları hello bulut tabanlı derleme özelliğidir ve Visual Studio Team Services hizmeti bırakın.</span><span class="sxs-lookup"><span data-stu-id="f5046-110">Release annotations are a feature of hello cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-hello-annotations-extension-one-time"></a><span data-ttu-id="f5046-111">Merhaba ek açıklamaları uzantısını (bir kez) yükleyin</span><span class="sxs-lookup"><span data-stu-id="f5046-111">Install hello Annotations extension (one time)</span></span>
<span data-ttu-id="f5046-112">toobe mümkün toocreate yayın ek açıklamalar, tooinstall biri gerekir Merhaba Visual Studio Market'te bulunan çok sayıda takım hizmeti uzantıları hello.</span><span class="sxs-lookup"><span data-stu-id="f5046-112">toobe able toocreate release annotations, you'll need tooinstall one of hello many Team Service extensions available in hello Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="f5046-113">İçinde tooyour oturum [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) projesi.</span><span class="sxs-lookup"><span data-stu-id="f5046-113">Sign in tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="f5046-114">Visual Studio pazarında [hello yayın ek açıklamaları uzantı alınmaya](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)ve tooyour Team Services hesabı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f5046-114">In Visual Studio Marketplace, [get hello Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it tooyour Team Services account.</span></span>

![AT Team Services web sayfasının açık Market sağ üst.](./media/app-insights-annotations/10.png)

<span data-ttu-id="f5046-117">Yalnızca toodo bu kez Visual Studio Team Services hesabınız için gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5046-117">You only need toodo this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="f5046-118">Yayın ek açıklamaları artık hesabınıza herhangi bir projede için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f5046-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="f5046-119">Yayın ek açıklamaları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f5046-119">Configure release annotations</span></span>

<span data-ttu-id="f5046-120">Her VSTS yayın şablonu için tooget ayrı bir API anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="f5046-120">You need tooget a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="f5046-121">İçinde toohello oturum [Microsoft Azure portalı](https://portal.azure.com) ve uygulamanızı izler hello Application Insights kaynağı açın.</span><span class="sxs-lookup"><span data-stu-id="f5046-121">Sign in toohello [Microsoft Azure Portal](https://portal.azure.com) and open hello Application Insights resource that monitors your application.</span></span> <span data-ttu-id="f5046-122">(Veya [şimdi oluşturmak](app-insights-overview.md), henüz yapmadıysanız.)</span><span class="sxs-lookup"><span data-stu-id="f5046-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="f5046-123">Açık **API erişimini**, **uygulama Öngörüler kimliği**.</span><span class="sxs-lookup"><span data-stu-id="f5046-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![Portal.Azure.com adresinde Application Insights kaynağınıza açın ve Ayarlar'ı seçin.](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="f5046-127">Ayrı bir tarayıcı penceresi açın (veya oluşturun) Visual Studio Team Services dağıtımlarınızı yönetir hello yayın şablonu.</span><span class="sxs-lookup"><span data-stu-id="f5046-127">In a separate browser window, open (or create) hello release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="f5046-128">Bir görev ekleyin ve Başlangıç menüsünden hello uygulama Öngörüler yayın ek açıklama görevi seçin.</span><span class="sxs-lookup"><span data-stu-id="f5046-128">Add a task, and select hello Application Insights Release Annotation task from hello menu.</span></span>
   
    <span data-ttu-id="f5046-129">Yapıştır hello **uygulama kimliği** API erişimini dikey penceresinde hello kopyalanan.</span><span class="sxs-lookup"><span data-stu-id="f5046-129">Paste hello **Application Id** that you copied from hello API Access blade.</span></span>
   
    ![Visual Studio Team Services sürüm açın, bir yayın tanımı seçin ve Düzenle'yi seçin.](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="f5046-133">Set hello **apikey ile yapılan** alanı tooa değişkeninin `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="f5046-133">Set hello **APIKey** field tooa variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="f5046-134">Hello Azure penceresi, geri döndüğünüzde yeni bir API anahtar oluşturun ve bir kopyasını alın.</span><span class="sxs-lookup"><span data-stu-id="f5046-134">Back in hello Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![Hello API erişimini dikey penceresinde hello Azure penceresi, API anahtarı oluştur'a tıklayın.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="f5046-138">Merhaba yapılandırma sekmesi hello yayın şablonu açın.</span><span class="sxs-lookup"><span data-stu-id="f5046-138">Open hello Configuration tab of hello release template.</span></span>
   
    <span data-ttu-id="f5046-139">İçin bir değişken tanımı oluşturun `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="f5046-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="f5046-140">API anahtar toohello apikey ile yapılan değişken tanımını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="f5046-140">Paste your API key toohello ApiKey variable definition.</span></span>
   
    ![Merhaba Team Services penceresinde hello yapılandırma sekmesini seçin ve değişken Ekle'yi tıklatın.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="f5046-143">Son olarak, **kaydetmek** hello yayın tanımı.</span><span class="sxs-lookup"><span data-stu-id="f5046-143">Finally, **Save** hello release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="f5046-144">Görünüm ek açıklamaları</span><span class="sxs-lookup"><span data-stu-id="f5046-144">View annotations</span></span>
<span data-ttu-id="f5046-145">Şimdi, hello yayın şablonu toodeploy yeni bir sürüm kullandığında açıklamanın tooApplication Öngörüler gönderilir.</span><span class="sxs-lookup"><span data-stu-id="f5046-145">Now, whenever you use hello release template toodeploy a new release, an annotation will be sent tooApplication Insights.</span></span> <span data-ttu-id="f5046-146">Merhaba ek açıklamaları ölçüm Gezgini grafiklerinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f5046-146">hello annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="f5046-147">Hello sürüm, istek sahibi, kaynak denetimi dalı, sürüm tanımı, ortam ve daha fazlasını dahil olmak üzere hiçbir ek açıklama işaret tooopen ayrıntılarını tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f5046-147">Click on any annotation marker tooopen details about hello release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Tüm yayın ek açıklama işaretçisi'ı tıklatın.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="f5046-149">Özel ek açıklama Powershell'den oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5046-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="f5046-150">(VS Team System kullanmadan) gibi herhangi bir işlem ek açıklamaları da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f5046-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="f5046-151">Merhaba yerel bir kopyasını [Powershell betiği github'dan](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="f5046-151">Make a local copy of hello [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="f5046-152">Merhaba uygulama kimliği alın ve API erişimini dikey penceresinde hello bir API anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f5046-152">Get hello Application ID and create an API key from hello API Access blade.</span></span>

3. <span data-ttu-id="f5046-153">Bu gibi Hello betik arayın:</span><span class="sxs-lookup"><span data-stu-id="f5046-153">Call hello script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="f5046-154">Bu, kolay toomodify hello komut dosyası, örneğin toocreate ek açıklamalarını hello geçmiş olur.</span><span class="sxs-lookup"><span data-stu-id="f5046-154">It's easy toomodify hello script, for example toocreate annotations for hello past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5046-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f5046-155">Next steps</span></span>

* [<span data-ttu-id="f5046-156">İş öğeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="f5046-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="f5046-157">PowerShell ile Automation</span><span class="sxs-lookup"><span data-stu-id="f5046-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
