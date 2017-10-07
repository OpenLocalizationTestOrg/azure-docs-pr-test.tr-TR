---
title: "Azure Power BI Embedded raporlarda görüntüleme ve düzenleme modu arasında aaaToggle | Microsoft Docs"
description: "Bilgi nasıl tootoggle raporlarınızı Power BI Embedded içinde için görüntüleme ve düzenleme modu arasında."
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
ms.openlocfilehash: c9e3da5f9ae74d221af650adebde7c9d83b38a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="toggle-between-view-and-edit-mode-for-reports-in-power-bi-embedded"></a><span data-ttu-id="0520e-103">Görünüm arasında geçiş yapmak ve Power BI Embedded raporlarda modunu düzenleyin</span><span class="sxs-lookup"><span data-stu-id="0520e-103">Toggle between view and edit mode for reports in Power BI Embedded</span></span>

<span data-ttu-id="0520e-104">Bilgi nasıl tootoggle raporlarınızı Power BI Embedded içinde için görüntüleme ve düzenleme modu arasında.</span><span class="sxs-lookup"><span data-stu-id="0520e-104">Learn how tootoggle between view and edit mode for your reports within Power BI Embedded.</span></span>

## <a name="creating-an-access-token"></a><span data-ttu-id="0520e-105">Bir erişim belirteci oluşturma</span><span class="sxs-lookup"><span data-stu-id="0520e-105">Creating an access token</span></span>

<span data-ttu-id="0520e-106">Toocreate hello özelliği tooboth görüntüleme ve düzenleme bir rapor veren bir erişim belirteci gerekir.</span><span class="sxs-lookup"><span data-stu-id="0520e-106">You will need toocreate an access token that gives you hello ability tooboth view and edit a report.</span></span> <span data-ttu-id="0520e-107">tooedit ve bir raporu hello gerekir **Report.ReadWrite** belirteci izni.</span><span class="sxs-lookup"><span data-stu-id="0520e-107">tooedit and save a report, you will need hello **Report.ReadWrite** token permission.</span></span> <span data-ttu-id="0520e-108">Daha fazla bilgi için bkz: [Authenticating ve Power BI Embedded yetkilendirme](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="0520e-108">For more information, see [Authenticating and authorizing in Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0520e-109">Bu tooedit izin ver ve tooan varolan rapor değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0520e-109">This will allow you tooedit and save changes tooan existing report.</span></span> <span data-ttu-id="0520e-110">Ayrıca destekleme hello işlevi isterseniz **Kaydet**, toosupply ek izinler gerekir.</span><span class="sxs-lookup"><span data-stu-id="0520e-110">If you would also like hello function of supporting **Save As**, you will need toosupply additional permissions.</span></span> <span data-ttu-id="0520e-111">Daha fazla bilgi için bkz: [kapsamları](power-bi-embedded-app-token-flow.md#scopes).</span><span class="sxs-lookup"><span data-stu-id="0520e-111">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes).</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Report.ReadWrite";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="embed-configuration"></a><span data-ttu-id="0520e-112">Yapılandırma katıştırma</span><span class="sxs-lookup"><span data-stu-id="0520e-112">Embed configuration</span></span>

<span data-ttu-id="0520e-113">Toosupply izinleri ve viewMode sipariş toosee hello Kaydet düğmesine düzenleme modunda de gerekir.</span><span class="sxs-lookup"><span data-stu-id="0520e-113">You will need toosupply permissions and a viewMode in order toosee hello save button when in edit mode.</span></span> <span data-ttu-id="0520e-114">Daha fazla bilgi için bkz: [yapılandırma ayrıntılarını katıştırmak](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span><span class="sxs-lookup"><span data-stu-id="0520e-114">For more information, see [Embed configuration details](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embed-Configuration-Details).</span></span>

<span data-ttu-id="0520e-115">JavaScript'te örneğin:</span><span class="sxs-lookup"><span data-stu-id="0520e-115">For example in JavaScript:</span></span>

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
        permissions: models.Permissions.ReadWrite /*both save & save as buttons will be visible*/,
        viewMode: models.ViewMode.View,
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

<span data-ttu-id="0520e-116">Bu temel görünüm modunda tooembed hello rapor gösterecektir **viewMode** çok ayarlanan**modeller. ViewMode.View**.</span><span class="sxs-lookup"><span data-stu-id="0520e-116">This will indicate tooembed hello report in view mode based on **viewMode** being set too**models.ViewMode.View**.</span></span>

## <a name="view-mode"></a><span data-ttu-id="0520e-117">Görünüm modu</span><span class="sxs-lookup"><span data-stu-id="0520e-117">View mode</span></span>

<span data-ttu-id="0520e-118">Düzenleme modunda olduğunda, görünüm moduna JavaScript tooswitch aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0520e-118">You can use hello following JavaScript tooswitch into view mode, if you are in edit mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooview mode.
report.switchMode("view");

```

## <a name="edit-mode"></a><span data-ttu-id="0520e-119">Düzenleme modu</span><span class="sxs-lookup"><span data-stu-id="0520e-119">Edit mode</span></span>

<span data-ttu-id="0520e-120">Görünüm modu değilseniz JavaScript tooswitch düzenleme moduna aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0520e-120">You can use hello following JavaScript tooswitch into edit mode, if you are in view mode.</span></span>

```
// Get a reference toohello embedded report HTML element
var reportContainer = $('#reportContainer')[0];

// Get a reference toohello embedded report.
report = powerbi.get(reportContainer);

// Switch tooedit mode.
report.switchMode("edit");

```

## <a name="see-also"></a><span data-ttu-id="0520e-121">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="0520e-121">See also</span></span>

[<span data-ttu-id="0520e-122">Bir örnek ile kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0520e-122">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="0520e-123">Rapor ekleme</span><span class="sxs-lookup"><span data-stu-id="0520e-123">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="0520e-124">Power BI Embedded ile kimlik doğrulaması ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="0520e-124">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="0520e-125">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="0520e-125">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="0520e-126">JavaScript Örnek Ekleme</span><span class="sxs-lookup"><span data-stu-id="0520e-126">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="0520e-127">Powerbı CSharp Git deposu</span><span class="sxs-lookup"><span data-stu-id="0520e-127">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="0520e-128">Powerbı düğümlü Git deposu</span><span class="sxs-lookup"><span data-stu-id="0520e-128">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="0520e-129">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="0520e-129">More questions?</span></span> [<span data-ttu-id="0520e-130">Merhaba Power BI topluluk deneyin</span><span class="sxs-lookup"><span data-stu-id="0520e-130">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
