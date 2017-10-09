---
title: bir rapor Azure Power BI Embedded aaaEmbed | Microsoft Docs
description: "Bilgi nasıl tooembed olan Power BI Embedded uygulamanıza bir rapor."
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
ms.openlocfilehash: f25344bbd0b9c092ef19da04d0b455d453b426a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="909bf-103">Power BI Embedded içinde bir rapor ekleme</span><span class="sxs-lookup"><span data-stu-id="909bf-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="909bf-104">Bilgi nasıl tooembed olan Power BI Embedded uygulamanıza bir rapor.</span><span class="sxs-lookup"><span data-stu-id="909bf-104">Learn how tooembed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="909bf-105">Nasıl tooactually katıştırmak bir raporu uygulamanıza ele alacağız.</span><span class="sxs-lookup"><span data-stu-id="909bf-105">We will look at how tooactually embed a report into your application.</span></span> <span data-ttu-id="909bf-106">Bu, mevcut bir rapor içinde bir çalışma alanı, çalışma alanı koleksiyonu zaten varsayılır.</span><span class="sxs-lookup"><span data-stu-id="909bf-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="909bf-107">Bu adım henüz yapmadıysanız bkz [Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="909bf-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="909bf-108">Tooeasily Power BI Embedded ile uygulamanızı oluşturma, hello .NET (C#) veya Node.js SDK, JavaScript ile birlikte kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="909bf-108">You can use hello .NET (C#) or Node.js SDK, along with JavaScript, tooeasily build your application with Power BI Embedded.</span></span> 

## <a name="using-hello-access-keys-toouse-rest-apis"></a><span data-ttu-id="909bf-109">Merhaba erişim anahtarları toouse REST API'lerini kullanma</span><span class="sxs-lookup"><span data-stu-id="909bf-109">Using hello access keys toouse REST APIs</span></span>

<span data-ttu-id="909bf-110">Sipariş toocall hello REST API, hello belirli çalışma alanı koleksiyonu için Azure Portalı'ndan elde edebilirsiniz hello erişim tuşu geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="909bf-110">In order toocall hello REST API, you can pass hello access key which you can get from hello Azure portal for a given workspace collection.</span></span> <span data-ttu-id="909bf-111">Daha fazla bilgi için bkz: [Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="909bf-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="909bf-112">Bir rapor kimliği alma</span><span class="sxs-lookup"><span data-stu-id="909bf-112">Get a report id</span></span>

<span data-ttu-id="909bf-113">Her erişim belirteci bir raporda temel alır.</span><span class="sxs-lookup"><span data-stu-id="909bf-113">Every access token is based on a report.</span></span> <span data-ttu-id="909bf-114">Tooembed istediğiniz hello rapor için rapor kimliği belirtilen tooget hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="909bf-114">You will need tooget hello given report id for hello report that you want tooembed.</span></span> <span data-ttu-id="909bf-115">Bu çağrı toohello göre yapılabilir [raporları Al](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span><span class="sxs-lookup"><span data-stu-id="909bf-115">This can be done based on calls toohello [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="909bf-116">Bu kimliği ve hello url katıştırmak hello rapor döndürür.</span><span class="sxs-lookup"><span data-stu-id="909bf-116">This will return hello report id and hello embed url.</span></span> <span data-ttu-id="909bf-117">Bu yapılabilir hello Power BI .NET SDK kullanarak veya doğrudan hello REST API çağırma.</span><span class="sxs-lookup"><span data-stu-id="909bf-117">This can be done using hello Power BI .NET SDK or calling hello REST API directly.</span></span>

### <a name="using-hello-power-bi-net-sdk"></a><span data-ttu-id="909bf-118">Merhaba Power BI .NET SDK kullanarak</span><span class="sxs-lookup"><span data-stu-id="909bf-118">Using hello Power BI .NET SDK</span></span>

<span data-ttu-id="909bf-119">Merhaba .NET SDK'sı kullanırken toocreate hello Azure portal ' aldığınız hello erişim tuşu dayalı olan bir belirteç kimlik bilgisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="909bf-119">When using hello .NET SDK, you will need toocreate a token credential which is based on hello access key you get from hello Azure portal.</span></span> <span data-ttu-id="909bf-120">Bu hello yüklemenizi gerektirir [Power BI API'si NuGet paketi](https://www.nuget.org/profiles/powerbi).</span><span class="sxs-lookup"><span data-stu-id="909bf-120">This requires that you install hello [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="909bf-121">**NuGet paketi yüklemesi**</span><span class="sxs-lookup"><span data-stu-id="909bf-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="909bf-122">**C# kodu**</span><span class="sxs-lookup"><span data-stu-id="909bf-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select hello report that you want toowork with from hello collection of reports.
```

### <a name="calling-hello-rest-api-directly"></a><span data-ttu-id="909bf-123">Doğrudan çağırma hello REST API'si</span><span class="sxs-lookup"><span data-stu-id="909bf-123">Calling hello REST API directly</span></span>

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response tooget hello report you want toowork with.
    }

}
```

## <a name="create-an-access-token"></a><span data-ttu-id="909bf-124">Bir erişim belirteci oluşturma</span><span class="sxs-lookup"><span data-stu-id="909bf-124">Create an access token</span></span>

<span data-ttu-id="909bf-125">Power BI Embedded kullanır ekleme belirteci, JSON Web belirteçlerini imzalı HMAC olduğu.</span><span class="sxs-lookup"><span data-stu-id="909bf-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="909bf-126">Merhaba belirteçleri hello erişim anahtarıyla Azure Power BI Embedded çalışma alanı koleksiyonu imzalanmıştır.</span><span class="sxs-lookup"><span data-stu-id="909bf-126">hello tokens are signed with hello access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="909bf-127">Varsayılan olarak belirteçleri, ekleme, olan okuma kullanılan tooprovide yalnızca erişim tooa rapor tooembed bir uygulamaya.</span><span class="sxs-lookup"><span data-stu-id="909bf-127">Embed tokens, by default, are used tooprovide read only access tooa report tooembed into an application.</span></span> <span data-ttu-id="909bf-128">Embed belirteçleri için belirli bir rapor verilir ve bir embed URL'si ile ilişkili olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="909bf-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="909bf-129">Merhaba erişim tuşları kullanılan toosign/şifrelemek hello belirteçleri gibi erişim belirteçleri hello sunucusunda oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="909bf-129">Access tokens should be created on hello server as hello access keys are used toosign/encrypt hello tokens.</span></span> <span data-ttu-id="909bf-130">Hakkında bilgi için bkz: toocreate bir erişim belirteci [Authenticating ve Power BI Embedded ile yetkilendirme](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="909bf-130">For information on how toocreate an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="909bf-131">Merhaba gözden geçirebilirsiniz [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="909bf-131">You can also review hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="909bf-132">Burada, ne için Power BI hello .NET SDK kullanarak gibi görünür bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="909bf-132">Here is an example of what this would look like using hello .NET SDK for Power BI.</span></span>

<span data-ttu-id="909bf-133">Daha önce aldığınız hello rapor kimliği kullanır.</span><span class="sxs-lookup"><span data-stu-id="909bf-133">You will use hello report id that you retrieved earlier.</span></span> <span data-ttu-id="909bf-134">Hello katıştırmak sonra belirteç oluşturulur, ardından hello javascript açısından kullanabileceğiniz hello erişim anahtar toogenerate hello belirteci kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="909bf-134">Once hello embed token is created, you will then use hello access key toogenerate hello token which you can use from hello javascript perspective.</span></span> <span data-ttu-id="909bf-135">Merhaba *PowerBIToken sınıfı* hello yüklemenizi gerektirir [Power BI çekirdek NuGut paketi](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="909bf-135">hello *PowerBIToken class* requires that you install hello [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="909bf-136">**NuGet paketi yüklemesi**</span><span class="sxs-lookup"><span data-stu-id="909bf-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="909bf-137">**C# kodu**</span><span class="sxs-lookup"><span data-stu-id="909bf-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-tooembed-tokens"></a><span data-ttu-id="909bf-138">İzin kapsamları tooembed belirteçleri ekleme</span><span class="sxs-lookup"><span data-stu-id="909bf-138">Adding permission scopes tooembed tokens</span></span>

<span data-ttu-id="909bf-139">Embed belirteçleri kullanırken toorestrict kullanım hello kaynakların erişim hakkı vermek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="909bf-139">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="909bf-140">Bu nedenle, kapsamlı izinlere sahip bir belirteç oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="909bf-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="909bf-141">Daha fazla bilgi için bkz: [kapsamları](power-bi-embedded-app-token-flow.md#scopes)</span><span class="sxs-lookup"><span data-stu-id="909bf-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="909bf-142">JavaScript kullanarak ekleme</span><span class="sxs-lookup"><span data-stu-id="909bf-142">Embed using JavaScript</span></span>

<span data-ttu-id="909bf-143">Merhaba erişim belirtecini ve hello rapor kimliğini oluşturduktan sonra biz JavaScript kullanarak hello rapor eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="909bf-143">After you have hello access token and hello report id, we can embed hello report using JavaScript.</span></span> <span data-ttu-id="909bf-144">Bu hello nuget yüklemenizi gerektirir [Power BI JavaScript paket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="909bf-144">This requires that you install hello nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="909bf-145">Merhaba embedUrl yalnızca https://embedded.powerbi.com/appTokenReportEmbed olacaktır.</span><span class="sxs-lookup"><span data-stu-id="909bf-145">hello embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="909bf-146">Merhaba kullanabilirsiniz [JavaScript rapor katıştırmak örnek](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest işlevselliği.</span><span class="sxs-lookup"><span data-stu-id="909bf-146">You can use hello [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) tootest functionality.</span></span> <span data-ttu-id="909bf-147">Aynı zamanda kullanılabilir hello farklı işlemler için kod örnekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="909bf-147">It also gives code examples for hello different operations that are available.</span></span>

<span data-ttu-id="909bf-148">**NuGet paketi yüklemesi**</span><span class="sxs-lookup"><span data-stu-id="909bf-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="909bf-149">**JavaScript kodu**</span><span class="sxs-lookup"><span data-stu-id="909bf-149">**JavaScript code**</span></span>

```
<script src="/scripts/powerbi.js"></script>
<div id="reportContainer"></div>

var embedConfiguration = {
    type: 'report',
    accessToken: 'eyJ0eXAiO...Qron7qYpY9MI',
    id: '5dac7a4a-4452-46b3-99f6-a25915e0fe55',
    embedUrl: 'https://embedded.powerbi.com/appTokenReportEmbed'
};

var $reportContainer = $('#reportContainer');
var report = powerbi.embed($reportContainer.get(0), embedConfiguration);
```

### <a name="set-hello-size-of-embedded-elements"></a><span data-ttu-id="909bf-150">Katıştırılmış öğeleri Hello boyutunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="909bf-150">Set hello size of embedded elements</span></span>

<span data-ttu-id="909bf-151">Merhaba rapor kapsayıcısı hello boyutuna göre otomatik olarak katıştırılır.</span><span class="sxs-lookup"><span data-stu-id="909bf-151">hello report will automatically be embedded based on hello size of its container.</span></span> <span data-ttu-id="909bf-152">Merhaba toooverride hello varsayılan boyutu katıştırır yalnızca genişliği ve yüksekliği için bir CSS sınıfı özniteliği veya satır içi stil ekleyin.</span><span class="sxs-lookup"><span data-stu-id="909bf-152">toooverride hello default size of hello embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="909bf-153">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="909bf-153">See also</span></span>

[<span data-ttu-id="909bf-154">Bir örnek ile kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="909bf-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="909bf-155">Power BI Embedded ile kimlik doğrulaması ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="909bf-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="909bf-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="909bf-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="909bf-157">JavaScript Örnek Ekleme</span><span class="sxs-lookup"><span data-stu-id="909bf-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="909bf-158">Power BI JavaScript paketi</span><span class="sxs-lookup"><span data-stu-id="909bf-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="909bf-159">[Power BI API'si NuGet paketi](https://www.nuget.org/profiles/powerbi)
[Power BI çekirdek NuGut paketi](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="909bf-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="909bf-160">Powerbı CSharp Git deposu</span><span class="sxs-lookup"><span data-stu-id="909bf-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="909bf-161">Powerbı düğümlü Git deposu</span><span class="sxs-lookup"><span data-stu-id="909bf-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="909bf-162">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="909bf-162">More questions?</span></span> [<span data-ttu-id="909bf-163">Merhaba Power BI topluluk deneyin</span><span class="sxs-lookup"><span data-stu-id="909bf-163">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
