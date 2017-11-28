---
title: "Azure Power BI Embedded'de kümesinden yeni bir rapor aaaCreate | Microsoft Docs"
description: "Power BI Embedded raporları, kendi uygulamanızda kümesinden şimdi oluşturulabilir."
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
ms.openlocfilehash: 41a0a52e4c833313f495bb5ff14749203fef9b41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-report-from-a-dataset-in-power-bi-embedded"></a><span data-ttu-id="d0d00-103">Power BI Embedded'de kümesinden yeni rapor oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0d00-103">Create a new report from a dataset in Power BI Embedded</span></span>

<span data-ttu-id="d0d00-104">Power BI Embedded raporları, kendi uygulamanızda kümesinden şimdi oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="d0d00-104">Power BI Embedded reports can now be created from a dataset in your own application.</span></span> 

<span data-ttu-id="d0d00-105">Merhaba kimlik doğrulama yöntemini benzer toothat raporunun ekleme.</span><span class="sxs-lookup"><span data-stu-id="d0d00-105">hello authentication method is similar toothat of report embed.</span></span> <span data-ttu-id="d0d00-106">Belirli tooa dataset olan erişim belirteçleri dayanır.</span><span class="sxs-lookup"><span data-stu-id="d0d00-106">It is based on access tokens that are specific tooa dataset.</span></span> <span data-ttu-id="d0d00-107">Azure Active Directory (AAD tarafından) verilen belirteçler PowerBI.com için kullanılan ve Power BI Embedded belirteçleri kendi hizmeti tarafından verilir.</span><span class="sxs-lookup"><span data-stu-id="d0d00-107">Tokens used for PowerBI.com are issued by Azure Active Directory (AAD) and Power BI Embedded tokens are issued by your own service.</span></span>

<span data-ttu-id="d0d00-108">Yayınlanan belirteçleri createing katıştırılmış rapor hello için belirli bir veri kümesi olur.</span><span class="sxs-lookup"><span data-stu-id="d0d00-108">When createing an Embedded report, hello tokens issued are for a specific dataset.</span></span> <span data-ttu-id="d0d00-109">Belirteçleri ilişkili URL ile Merhaba katıştırmak hello üzerinde aynı öğesi tooensure her benzersiz belirtece sahip.</span><span class="sxs-lookup"><span data-stu-id="d0d00-109">Tokens should be associated with hello embed URL on hello same element tooensure each has a unique token.</span></span> <span data-ttu-id="d0d00-110">İçinde katıştırılmış rapor toocreate sipariş *Dataset.Read ve Workspace.Report.Create* kapsamları hello erişim belirtecinde yer sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0d00-110">In order toocreate an Embedded report, *Dataset.Read and Workspace.Report.Create* scopes must be provided in hello access token.</span></span>

## <a name="create-access-token-needed-toocreate-new-report"></a><span data-ttu-id="d0d00-111">Erişim belirteci gerekli toocreate yeni rapor oluşturma</span><span class="sxs-lookup"><span data-stu-id="d0d00-111">Create access token needed toocreate new report</span></span>

<span data-ttu-id="d0d00-112">Power BI Embedded kullanır ekleme belirteci, JSON Web belirteçlerini imzalı HMAC olduğu.</span><span class="sxs-lookup"><span data-stu-id="d0d00-112">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="d0d00-113">Merhaba belirteçleri hello erişim anahtarıyla Azure Power BI Embedded çalışma alanı koleksiyonu imzalanmıştır.</span><span class="sxs-lookup"><span data-stu-id="d0d00-113">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="d0d00-114">Varsayılan olarak belirteçleri, ekleme, olan okuma kullanılan tooprovide yalnızca erişim tooa rapor tooembed bir uygulamaya.</span><span class="sxs-lookup"><span data-stu-id="d0d00-114">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="d0d00-115">Embed belirteçleri için belirli bir rapor verilir ve bir embed URL'si ile ilişkili olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0d00-115">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="d0d00-116">Merhaba erişim tuşları kullanılan toosign/şifrelemek hello belirteçleri gibi erişim belirteçleri hello sunucusunda oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0d00-116">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="d0d00-117">Hakkında bilgi için bkz: toocreate bir erişim belirteci [Authenticating ve Power BI Embedded ile yetkilendirme](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="d0d00-117">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="d0d00-118">Merhaba gözden geçirebilirsiniz [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d0d00-118">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="d0d00-119">Burada, ne için Power BI hello .NET SDK kullanarak gibi görünür bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d0d00-119">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="d0d00-120">Bu örnekte, toocreat hello yeni rapor üzerinde istiyoruz bizim veri kümesi tanıtıcısı sahip.</span><span class="sxs-lookup"><span data-stu-id="d0d00-120">In this example, we have our dataset id that we want toocreat hello new report on.</span></span> <span data-ttu-id="d0d00-121">Ayrıca tooadd hello kapsamları için ihtiyacımız *Dataset.Read ve Workspace.Report.Create*.</span><span class="sxs-lookup"><span data-stu-id="d0d00-121">We also need tooadd hello scopes for *Dataset.Read and Workspace.Report.Create*.</span></span>

<span data-ttu-id="d0d00-122">Merhaba *PowerBIToken sınıfı* hello yüklemenizi gerektirir [Power BI çekirdek NuGut paketi](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="d0d00-122">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="d0d00-123">**NuGet paketi yüklemesi**</span><span class="sxs-lookup"><span data-stu-id="d0d00-123">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="d0d00-124">**C# kodu**</span><span class="sxs-lookup"><span data-stu-id="d0d00-124">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername and roles are optional
string scopes = "Dataset.Read Workspace.Report.Create";
PowerBIToken embedToken = PowerBIToken.CreateReportEmbedTokenForCreation(workspaceCollectionName, workspaceId, datasetId, null, null, scopes);

var token = embedToken.Generate("{access key}");
```

## <a name="create-a-new-blank-report"></a><span data-ttu-id="d0d00-125">Yeni boş bir rapor oluşturun</span><span class="sxs-lookup"><span data-stu-id="d0d00-125">Create a new blank report</span></span>

<span data-ttu-id="d0d00-126">Sipariş toocreate yeni bir rapor, hello oluşturma yapılandırması sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d0d00-126">In order toocreate a new report, hello create configuration should be provided.</span></span> <span data-ttu-id="d0d00-127">Bu toocreate hello raporun, karşılarında istediğimiz hello erişim belirteci, hello embedURL ve hello Datasetıd içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d0d00-127">This should include hello access token, hello embedURL and hello datasetID that we want toocreate hello report against.</span></span> <span data-ttu-id="d0d00-128">Bu hello nuget yüklemenizi gerektirir [Power BI JavaScript paket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="d0d00-128">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="d0d00-129">Merhaba embedUrl yalnızca https://embedded.powerbi.com/appTokenReportEmbed olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d0d00-129">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="d0d00-130">Merhaba kullanabilirsiniz [JavaScript rapor katıştırmak örnek](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest işlevselliği.</span><span class="sxs-lookup"><span data-stu-id="d0d00-130">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="d0d00-131">Aynı zamanda kullanılabilir hello farklı işlemler için kod örnekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0d00-131">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="d0d00-132">**NuGet paketi yüklemesi**</span><span class="sxs-lookup"><span data-stu-id="d0d00-132">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="d0d00-133">**JavaScript kodu**</span><span class="sxs-lookup"><span data-stu-id="d0d00-133">**JavaScript code**</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);
```

<span data-ttu-id="d0d00-134">Çağırma *powerbi.createReport()* hello içinde görünür boş bir tuval düzenleme modunda yapacak *div* öğesi.</span><span class="sxs-lookup"><span data-stu-id="d0d00-134">Calling *powerbi.createReport()* will make a blank canvas in edit mode appear within hello *div* element.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-create-new-report.png)

## <a name="save-new-reports"></a><span data-ttu-id="d0d00-135">Yeni raporlar Kaydet</span><span class="sxs-lookup"><span data-stu-id="d0d00-135">Save new reports</span></span>

<span data-ttu-id="d0d00-136">Merhaba rapor gerçekte oluşturulmaz hello çağrısı tamamlanana kadar **Farklı Kaydet** işlemi.</span><span class="sxs-lookup"><span data-stu-id="d0d00-136">hello report will not actually be created until you call hello **save as** operation.</span></span> <span data-ttu-id="d0d00-137">Bu dosya menüsünden veya JavaScript yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="d0d00-137">This can be done from file menu or from JavaScript.</span></span>

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
> <span data-ttu-id="d0d00-138">Yeni bir rapor yalnızca sonra oluşturulan **Farklı Kaydet** olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="d0d00-138">A new report is created only after **save as** is called.</span></span> <span data-ttu-id="d0d00-139">Kaydettikten sonra hello tuvale hello dataset düzenleme modu ve değil hello raporda hala gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0d00-139">After you save, hello canvas will still show hello dataset in edit mode and not hello report.</span></span> <span data-ttu-id="d0d00-140">Herhangi bir raporu gibi tooreload hello yeni rapor gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0d00-140">You will need tooreload hello new report like you would any other report.</span></span>

![](media/power-bi-embedded-create-report-from-dataset/pbi-embedded-save-new-report.png)

## <a name="load-hello-new-report"></a><span data-ttu-id="d0d00-141">Yük hello yeni raporu</span><span class="sxs-lookup"><span data-stu-id="d0d00-141">Load hello new report</span></span>

<span data-ttu-id="d0d00-142">Merhaba yeni bir rapor ile sipariş toointeract'hello Merhaba uygulaması katıştırır normal bir raporu, anlamı, yeni bir belirteç aynı şekilde özellikle hello yeni rapor için verilmiş olması gerekir ve ardından arama hello içinde katıştırma yöntemi tooembed ihtiyacı vardır.</span><span class="sxs-lookup"><span data-stu-id="d0d00-142">In order toointeract with hello new report you need tooembed it in hello same way hello application embeds a regular report, meaning, a new token must be issued specifically for hello new report and then call hello embed method.</span></span>

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

## <a name="automate-save-and-load-of-a-new-report-using-hello-saved-event"></a><span data-ttu-id="d0d00-143">Kaydetme otomatikleştirmek ve "olay kaydedilmiş" Merhaba kullanarak yeni bir rapor yükleme</span><span class="sxs-lookup"><span data-stu-id="d0d00-143">Automate save and load of a new report using hello "saved" event</span></span>

<span data-ttu-id="d0d00-144">"Farklı Kaydet" sipariş tooautomate hello işlemi içinde ve yapabilirsiniz hello yeni rapor yüklenirken "Olay kaydedilmiş" hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0d00-144">In order tooautomate hello process of "save as" and then loading hello new report you can make use of hello "saved" Event.</span></span> <span data-ttu-id="d0d00-145">Bu olay hello kaydetme işlemi tamamlandığında ve (varsa) hello yeni reportId, rapor adı, hello eski reportId içeren bir Json nesnesi döndürür ve hello işlemi Farklı Kaydet olduysa veya kaydetme ateşlenir.</span><span class="sxs-lookup"><span data-stu-id="d0d00-145">This event is fired when hello save operation is complete and it returns a Json object containing hello new reportId, report name, hello old reportId(if there was one) and if hello operation was saveAs or save.</span></span>

```
{
  "reportObjectId": "5dac7a4a-4452-46b3-99f6-a25915e0fe54",
  "reportName": "newReport",
  "saveAs": true,
  "originalReportObjectId": null
}
```

<span data-ttu-id="d0d00-146">"kaydedildi" Merhaba olayda dinleme, hello yeni reportId alabilir, hello yeni belirteç oluşturmak ve onunla hello yeni rapor ekleme tooAutomate hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="d0d00-146">tooAutomate hello process you can listen on hello "saved" event, take hello new reportId, create hello new token and embed hello new report with it.</span></span>

```
<div id="reportContainer"></div>
  
var embedCreateConfiguration = {
        accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        datasetId: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    };
    
    // Grab hello reference toohello div HTML element that will host hello report
    var reportContainer = $('#reportContainer')[0];

    // Create report
    var report = powerbi.createReport(reportContainer, embedCreateConfiguration);


   var saveAsParameters = {
        name: "newReport"
    };

    // SaveAs report
    report.saveAs(saveAsParameters);

    // report.on will add an event handler which prints tooLog window.
    report.on("saved", function(event) {
        
         // get new Token
         var newReportId =  event.detail.reportObjectId;

        // create new Token. This is a function that hello application should provide
        var newToken = createAccessToken(newReportId,scopes /*provide hello wanted scopes*/);
        
        
    var embedConfiguration = {
        accessToken: newToken ,
        embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed',
        reportId: newReportId,
    };

    // Embed report
    var report = powerbi.embed(reportContainer, embedConfiguration);
       
   // report.off removes a given event handler if it exists.
   report.off("saved");
    });
```

## <a name="see-also"></a><span data-ttu-id="d0d00-147">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d0d00-147">See also</span></span>

[<span data-ttu-id="d0d00-148">Bir örnek ile kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d0d00-148">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="d0d00-149">Raporları kaydetme</span><span class="sxs-lookup"><span data-stu-id="d0d00-149">Save reports</span></span>](power-bi-embedded-save-reports.md)  
[<span data-ttu-id="d0d00-150">Rapor ekleme</span><span class="sxs-lookup"><span data-stu-id="d0d00-150">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="d0d00-151">Power BI Embedded ile kimlik doğrulaması ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="d0d00-151">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="d0d00-152">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="d0d00-152">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="d0d00-153">JavaScript Örnek Ekleme</span><span class="sxs-lookup"><span data-stu-id="d0d00-153">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="d0d00-154">Power BI çekirdek NuGut paketi</span><span class="sxs-lookup"><span data-stu-id="d0d00-154">Power BI Core NuGut Package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)  
[<span data-ttu-id="d0d00-155">Power BI JavaScript paketi</span><span class="sxs-lookup"><span data-stu-id="d0d00-155">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="d0d00-156">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="d0d00-156">More questions?</span></span> [<span data-ttu-id="d0d00-157">Merhaba Power BI topluluk deneyin</span><span class="sxs-lookup"><span data-stu-id="d0d00-157">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
