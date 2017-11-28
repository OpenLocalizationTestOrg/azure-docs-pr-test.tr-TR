---
title: Azure Power BI Embedded aaaSave raporlarda | Microsoft Docs
description: "Power BI içinde toosave raporları nasıl katıştırılmış öğrenin. Bu sipariş toowork uygun izinleri başarıyla gerektirir."
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 984537ce1ce1afc787d6c6c9f61ae8d6226d1171
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="save-reports-in-power-bi-embedded"></a><span data-ttu-id="98a7f-104">Raporlar Power BI Embedded Kaydet</span><span class="sxs-lookup"><span data-stu-id="98a7f-104">Save reports in Power BI Embedded</span></span>

<span data-ttu-id="98a7f-105">Power BI içinde toosave raporları nasıl katıştırılmış öğrenin.</span><span class="sxs-lookup"><span data-stu-id="98a7f-105">Learn how toosave reports within Power BI embedded.</span></span> <span data-ttu-id="98a7f-106">Bu sipariş toowork uygun izinleri başarıyla gerektirir.</span><span class="sxs-lookup"><span data-stu-id="98a7f-106">This requires proper permissions in order toowork successfully.</span></span>

<span data-ttu-id="98a7f-107">Power BI Embedded içinde varolan raporları düzenleyebilir ve kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98a7f-107">Within Power BI Embedded, you can edit existing reports and save them.</span></span> <span data-ttu-id="98a7f-108">Ayrıca, yeni bir rapor oluşturmak ve bir yeni raporu toocreate bir kaydedin.</span><span class="sxs-lookup"><span data-stu-id="98a7f-108">You can also create a new report and save as a new report toocreate one.</span></span>

<span data-ttu-id="98a7f-109">Sipariş toosave bir rapor önce toocreate bir belirteç hello sağ kapsamlarla hello belirli rapor için gerekir:</span><span class="sxs-lookup"><span data-stu-id="98a7f-109">In order toosave a report you first need toocreate a token for hello specific report with hello right scopes:</span></span>

* <span data-ttu-id="98a7f-110">tooenable Report.ReadWrite kapsam kaydetme gereklidir</span><span class="sxs-lookup"><span data-stu-id="98a7f-110">tooenable save Report.ReadWrite scope is required</span></span>
* <span data-ttu-id="98a7f-111">olarak tooenable kaydetme Report.Read ve Workspace.Report.Copy kapsamları gereklidir</span><span class="sxs-lookup"><span data-stu-id="98a7f-111">tooenable save as, Report.Read and Workspace.Report.Copy scopes are required</span></span>
* <span data-ttu-id="98a7f-112">tooenable kaydedin ve kaydetme, Report.ReadWrite ve Workspace.Report.Copy gerekli</span><span class="sxs-lookup"><span data-stu-id="98a7f-112">tooenable save and save as, Report.ReadWrite and Workspace.Report.Copy are requierd</span></span>

<span data-ttu-id="98a7f-113">Embed rapor hello zaman sırasıyla sipariş tooenable hello kaydetme/Kaydet doğru dosya menüsünden düğmeleri gibi tooprovide hello hello Embed yapılandırma izni hemen:</span><span class="sxs-lookup"><span data-stu-id="98a7f-113">Respectively in order tooenable hello right save/save as buttons in file menu you need tooprovide hello right permission in hello Embed configuration when you Embed hello report:</span></span>

* <span data-ttu-id="98a7f-114">modeller. Permissions.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="98a7f-114">models.Permissions.ReadWrite</span></span>
* <span data-ttu-id="98a7f-115">modeller. Permissions.Copy</span><span class="sxs-lookup"><span data-stu-id="98a7f-115">models.Permissions.Copy</span></span>
* <span data-ttu-id="98a7f-116">modeller. Permissions.All</span><span class="sxs-lookup"><span data-stu-id="98a7f-116">models.Permissions.All</span></span>

> [!NOTE]
> <span data-ttu-id="98a7f-117">Erişim belirteci hello uygun kapsamları da gerekir.</span><span class="sxs-lookup"><span data-stu-id="98a7f-117">Your access token also needs hello appropriate scopes.</span></span> <span data-ttu-id="98a7f-118">Daha fazla bilgi için bkz: [kapsamları](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="98a7f-118">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

## <a name="embed-report-in-edit-mode"></a><span data-ttu-id="98a7f-119">Rapor düzenleme modunda ekleme</span><span class="sxs-lookup"><span data-stu-id="98a7f-119">Embed report in edit mode</span></span>

<span data-ttu-id="98a7f-120">Şimdi tooEmbed bir rapor düzenleme modunda uygulamanızı içinde deyin istediğiniz, toodo böylece yalnızca Embed yapılandırmasında hello hakkı özellikleri geçirmek ve powerbi.embed() çağırın.</span><span class="sxs-lookup"><span data-stu-id="98a7f-120">Let's say you want tooEmbed a report in edit mode inside your app, toodo so just pass hello right properties in Embed configuration and call powerbi.embed().</span></span> <span data-ttu-id="98a7f-121">Düğmeleri düzenleme modunda olarak toosupply izinleri ve viewMode sipariş toosee hello kaydetmek ve kaydetme de gerekir.</span><span class="sxs-lookup"><span data-stu-id="98a7f-121">You will need toosupply permissions and a viewMode in order toosee hello save and save as buttons when in edit mode.</span></span> <span data-ttu-id="98a7f-122">Daha fazla bilgi için bkz: [yapılandırma ayrıntılarını katıştırmak](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span><span class="sxs-lookup"><span data-stu-id="98a7f-122">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="98a7f-123">JavaScript'te örneğin:</span><span class="sxs-lookup"><span data-stu-id="98a7f-123">For example in JavaScript:</span></span>

```
   <div id="reportContainer"></div>

    // Get models. Models, it contains enums that can be used.
    var models = window['powerbi-client'].models;

    // Embed configuration used toodescribe hello what and how tooembed.
    // This object is used when calling powerbi.embed.
    // This also includes settings and options such as filters.
    // You can find more information at https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details.
    var config= {
        type: 'report',
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        id:  '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
        permissions: models.Permissions.All /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.Edit,
        settings: {
            filterPaneEnabled: true,
            navContentPaneEnabled: true
        }
    };

    // Get a reference toohello embedded report HTML element
    var reportContainer = $('#reportContainer')[0];

    // Embed hello report and display it within hello div container.
    var report = powerbi.embed(reportContainer, config);
```

<span data-ttu-id="98a7f-124">Şimdi bir rapor düzenleme modunda, uygulamanızda katıştırılır.</span><span class="sxs-lookup"><span data-stu-id="98a7f-124">Now a report will be embedded in your app in edit mode.</span></span>

## <a name="save-report"></a><span data-ttu-id="98a7f-125">Raporu kaydetme</span><span class="sxs-lookup"><span data-stu-id="98a7f-125">Save report</span></span>

<span data-ttu-id="98a7f-126">Embbeding hello raporda düzenledikten sonra hello sağ belirteci ve izinleri moduyla hello Dosya menüsünden veya javascript hello rapor kaydedebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="98a7f-126">After Embbeding hello report in edit mode with hello right token and permissions you can save hello report from hello file menu or from javascript:</span></span>

```
 // Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);

 // Save report
    report.save();
```

## <a name="save-as"></a><span data-ttu-id="98a7f-127">Farklı kaydet</span><span class="sxs-lookup"><span data-stu-id="98a7f-127">Save as</span></span>

```
// Get a reference toohello embedded report.
    report = powerbi.get(reportContainer);
    
    var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);
```

> [!IMPORTANT]
> <span data-ttu-id="98a7f-128">Yalnızca sonra *Farklı Kaydet* oluşturulan yeni bir rapor.</span><span class="sxs-lookup"><span data-stu-id="98a7f-128">Only after *save as* is a new report created.</span></span> <span data-ttu-id="98a7f-129">Merhaba kaydettikten sonra hello tuvale hala hello eski rapor düzenleme modu ve değil hello yeni raporu gösteriliyor.</span><span class="sxs-lookup"><span data-stu-id="98a7f-129">After hello save, hello canvas is still showing hello old report in edit mode and not hello new report.</span></span> <span data-ttu-id="98a7f-130">Oluşturulan tooembed hello yeni rapor gerekir.</span><span class="sxs-lookup"><span data-stu-id="98a7f-130">You will need tooembed hello new report that was created.</span></span> <span data-ttu-id="98a7f-131">Bu, rapor oluşturuldukça yeni bir erişim belirteci gerektirir.</span><span class="sxs-lookup"><span data-stu-id="98a7f-131">This requires a new access token as they are created per report.</span></span>

<span data-ttu-id="98a7f-132">Ardından tooload hello sonra yeni bir rapor gerekir bir *Farklı Kaydet*.</span><span class="sxs-lookup"><span data-stu-id="98a7f-132">You will then need tooload hello new report after a *save as*.</span></span> <span data-ttu-id="98a7f-133">Bu benzer tooembedding bir rapordur.</span><span class="sxs-lookup"><span data-stu-id="98a7f-133">This is similar tooembedding any report.</span></span>

```
<div id="reportContainer"></div>
  
var embedConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MJ',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: '5dac7a4a-4452-46b3-99f6-a25915e0fe54',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
```

## <a name="see-also"></a><span data-ttu-id="98a7f-134">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="98a7f-134">See also</span></span>

[<span data-ttu-id="98a7f-135">Bir örnek ile kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="98a7f-135">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="98a7f-136">Rapor ekleme</span><span class="sxs-lookup"><span data-stu-id="98a7f-136">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="98a7f-137">Veri kümesinden yeni rapor oluşturma</span><span class="sxs-lookup"><span data-stu-id="98a7f-137">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="98a7f-138">Power BI Embedded ile kimlik doğrulaması ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="98a7f-138">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="98a7f-139">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="98a7f-139">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="98a7f-140">JavaScript Örnek Ekleme</span><span class="sxs-lookup"><span data-stu-id="98a7f-140">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="98a7f-141">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="98a7f-141">More questions?</span></span> [<span data-ttu-id="98a7f-142">Merhaba Power BI topluluk deneyin</span><span class="sxs-lookup"><span data-stu-id="98a7f-142">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

