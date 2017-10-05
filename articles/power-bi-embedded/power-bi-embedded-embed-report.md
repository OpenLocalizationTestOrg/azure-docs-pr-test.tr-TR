---
title: Bir rapor Azure Power BI Embedded ekleme | Microsoft Docs
description: "Power BI Embedded içinde olduğu uygulamanıza bir rapor ekleme hakkında bilgi edinin."
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
ms.openlocfilehash: 3d865af2418c9c557c861a379766a125d75cebf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="embed-a-report-in-power-bi-embedded"></a><span data-ttu-id="91675-103">Power BI Embedded içinde bir rapor ekleme</span><span class="sxs-lookup"><span data-stu-id="91675-103">Embed a report in Power BI Embedded</span></span>

<span data-ttu-id="91675-104">Power BI Embedded içinde olduğu uygulamanıza bir rapor ekleme hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="91675-104">Learn how to embed a report that is in Power BI Embedded into your application.</span></span>

<span data-ttu-id="91675-105">Gerçekte uygulamanıza bir rapor eklemek nasıl ele alacağız.</span><span class="sxs-lookup"><span data-stu-id="91675-105">We will look at how to actually embed a report into your application.</span></span> <span data-ttu-id="91675-106">Bu, mevcut bir rapor içinde bir çalışma alanı, çalışma alanı koleksiyonu zaten varsayılır.</span><span class="sxs-lookup"><span data-stu-id="91675-106">This is assuming you already have a report that exists within a workspace in your workspace collection.</span></span> <span data-ttu-id="91675-107">Bu adım henüz yapmadıysanız bkz [Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="91675-107">If you haven't done that step yet, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

<span data-ttu-id="91675-108">Kolayca Power BI Embedded ile uygulamanızı .NET (C#) veya Node.js SDK, JavaScript ile birlikte kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91675-108">You can use the .NET (C#) or Node.js SDK, along with JavaScript, to easily build your application with Power BI Embedded.</span></span> 

## <a name="using-the-access-keys-to-use-rest-apis"></a><span data-ttu-id="91675-109">REST API'lerini kullanma için erişim anahtarlarını kullanma</span><span class="sxs-lookup"><span data-stu-id="91675-109">Using the access keys to use REST APIs</span></span>

<span data-ttu-id="91675-110">REST API çağrısı için belirtilen çalışma alanı koleksiyonu için Azure Portalı'ndan elde edebilirsiniz erişim anahtarı geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91675-110">In order to call the REST API, you can pass the access key which you can get from the Azure portal for a given workspace collection.</span></span> <span data-ttu-id="91675-111">Daha fazla bilgi için bkz: [Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="91675-111">For more information, see [Get started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="get-a-report-id"></a><span data-ttu-id="91675-112">Bir rapor kimliği alma</span><span class="sxs-lookup"><span data-stu-id="91675-112">Get a report id</span></span>

<span data-ttu-id="91675-113">Her erişim belirteci bir raporda temel alır.</span><span class="sxs-lookup"><span data-stu-id="91675-113">Every access token is based on a report.</span></span> <span data-ttu-id="91675-114">Eklemek istediğiniz rapor için belirli rapor kimliği alma gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="91675-114">You will need to get the given report id for the report that you want to embed.</span></span> <span data-ttu-id="91675-115">Bu temel alınarak çağrıları yapılabilir [raporları Al](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span><span class="sxs-lookup"><span data-stu-id="91675-115">This can be done based on calls to the [Get Reports](https://msdn.microsoft.com/library/azure/mt711510.aspx) REST API.</span></span> <span data-ttu-id="91675-116">Bu rapor kimliği ve embed URL'sini döndürür.</span><span class="sxs-lookup"><span data-stu-id="91675-116">This will return the report id and the embed url.</span></span> <span data-ttu-id="91675-117">Bu Power BI .NET SDK kullanarak veya doğrudan REST API çağırma yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="91675-117">This can be done using the Power BI .NET SDK or calling the REST API directly.</span></span>

### <a name="using-the-power-bi-net-sdk"></a><span data-ttu-id="91675-118">Power BI .NET SDK kullanarak</span><span class="sxs-lookup"><span data-stu-id="91675-118">Using the Power BI .NET SDK</span></span>

<span data-ttu-id="91675-119">.NET SDK'sı kullanırken, Azure portalından aldığınız erişim tuşu dayalı olan bir belirteç kimlik bilgisi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="91675-119">When using the .NET SDK, you will need to create a token credential which is based on the access key you get from the Azure portal.</span></span> <span data-ttu-id="91675-120">Bu, yüklemenizi gerektirir [Power BI API'si NuGet paketi](https://www.nuget.org/profiles/powerbi).</span><span class="sxs-lookup"><span data-stu-id="91675-120">This requires that you install the [Power BI API NuGet package](https://www.nuget.org/profiles/powerbi).</span></span>

<span data-ttu-id="91675-121">**NuGet paketi yüklemesi**</span><span class="sxs-lookup"><span data-stu-id="91675-121">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Api
```

<span data-ttu-id="91675-122">**C# kodu**</span><span class="sxs-lookup"><span data-stu-id="91675-122">**C# code**</span></span>

```
using Microsoft.PowerBI.Api.V1;
using Microsoft.Rest;

var credentials = new TokenCredentials("{access key}", "AppKey");
var client = new PowerBIClient(credentials);
client.BaseUri = new Uri(https://api.powerbi.com);

var reports = (IList<Report>)client.Reports.GetReports(workspaceCollectionName, workspaceId).Value;

// Select the report that you want to work with from the collection of reports.
```

### <a name="calling-the-rest-api-directly"></a><span data-ttu-id="91675-123">REST API doğrudan çağırma</span><span class="sxs-lookup"><span data-stu-id="91675-123">Calling the REST API directly</span></span>

```
System.Net.WebRequest request = System.Net.WebRequest.Create("https://api.powerbi.com/v1.0/collections/{collectionName}/workspaces/{workspaceId}/Reports") as System.Net.HttpWebRequest;

request.Method = "GET";
request.ContentLength = 0;
request.Headers.Add("Authorization", String.Format("AppKey {0}", accessToken.Value));

using (var response = request.GetResponse() as System.Net.HttpWebResponse)
{
    using (var reader = new System.IO.StreamReader(response.GetResponseStream()))
    {
        // Work with JSON response to get the report you want to work with.
    }

}
```

## <a name="create-an-access-token"></a><span data-ttu-id="91675-124">Bir erişim belirteci oluşturma</span><span class="sxs-lookup"><span data-stu-id="91675-124">Create an access token</span></span>

<span data-ttu-id="91675-125">Power BI Embedded kullanır ekleme belirteci, JSON Web belirteçlerini imzalı HMAC olduğu.</span><span class="sxs-lookup"><span data-stu-id="91675-125">Power BI Embedded uses embed token, which are HMAC signed JSON Web Tokens.</span></span> <span data-ttu-id="91675-126">Belirteçler, Azure Power BI Embedded çalışma alanı koleksiyonu erişim anahtarla imzalanmıştır.</span><span class="sxs-lookup"><span data-stu-id="91675-126">The tokens are signed with the access key from your Azure Power BI Embedded workspace collection.</span></span> <span data-ttu-id="91675-127">Varsayılan olarak belirteçleri, ekleme, bir uygulamaya eklemek için bir rapor için salt okunur erişim sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="91675-127">Embed tokens, by default, are used to provide read only access to a report to embed into an application.</span></span> <span data-ttu-id="91675-128">Embed belirteçleri için belirli bir rapor verilir ve bir embed URL'si ile ilişkili olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="91675-128">Embed tokens are issued for a specific report and should be associated with an embed URL.</span></span>

<span data-ttu-id="91675-129">Erişim tuşları belirteçleri oturum/şifrelemek için kullanılan erişim belirteçleri sunucuda oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="91675-129">Access tokens should be created on the server as the access keys are used to sign/encrypt the tokens.</span></span> <span data-ttu-id="91675-130">Bir erişim belirteci oluşturma hakkında daha fazla bilgi için bkz: [Authenticating ve Power BI Embedded ile yetkilendirme](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="91675-130">For information on how to create an access token, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span> <span data-ttu-id="91675-131">Ayrıca gözden geçirebilirsiniz [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="91675-131">You can also review the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) method.</span></span> <span data-ttu-id="91675-132">Burada, ne için Power BI .NET SDK kullanarak gibi görünür bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="91675-132">Here is an example of what this would look like using the .NET SDK for Power BI.</span></span>

<span data-ttu-id="91675-133">Daha önce aldığınız rapor kimliği kullanır.</span><span class="sxs-lookup"><span data-stu-id="91675-133">You will use the report id that you retrieved earlier.</span></span> <span data-ttu-id="91675-134">Ekleme belirteci oluşturulduktan sonra javascript açısından kullanabileceğiniz belirteci üretmek için erişim anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="91675-134">Once the embed token is created, you will then use the access key to generate the token which you can use from the javascript perspective.</span></span> <span data-ttu-id="91675-135">*PowerBIToken sınıfı* , yüklemenizi gerektirir [Power BI çekirdek NuGut paketi](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span><span class="sxs-lookup"><span data-stu-id="91675-135">The *PowerBIToken class* requires that you install the [Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/).</span></span>

<span data-ttu-id="91675-136">**NuGet paketi yüklemesi**</span><span class="sxs-lookup"><span data-stu-id="91675-136">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.Core
```

<span data-ttu-id="91675-137">**C# kodu**</span><span class="sxs-lookup"><span data-stu-id="91675-137">**C# code**</span></span>

```
using Microsoft.PowerBI.Security;

// rlsUsername, roles and scopes are optional.
embedToken = PowerBIToken.CreateReportEmbedToken(workspaceCollectionName, workspaceId, reportId, rlsUsername, roles, scopes);

var token = embedToken.Generate("{access key}");
```

### <a name="adding-permission-scopes-to-embed-tokens"></a><span data-ttu-id="91675-138">Belirteçleri katıştırmak için izin kapsamları ekleme</span><span class="sxs-lookup"><span data-stu-id="91675-138">Adding permission scopes to embed tokens</span></span>

<span data-ttu-id="91675-139">Embed belirteçleri kullanırken, erişim hakkı vermek kaynak kullanımını kısıtlamak istediğinizi düşünelim.</span><span class="sxs-lookup"><span data-stu-id="91675-139">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="91675-140">Bu nedenle, kapsamlı izinlere sahip bir belirteç oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91675-140">For this reason, you can generate a token with scoped permissions.</span></span> <span data-ttu-id="91675-141">Daha fazla bilgi için bkz: [kapsamları](power-bi-embedded-app-token-flow.md#scopes)</span><span class="sxs-lookup"><span data-stu-id="91675-141">For more information, see [Scopes](power-bi-embedded-app-token-flow.md#scopes)</span></span>

## <a name="embed-using-javascript"></a><span data-ttu-id="91675-142">JavaScript kullanarak ekleme</span><span class="sxs-lookup"><span data-stu-id="91675-142">Embed using JavaScript</span></span>

<span data-ttu-id="91675-143">Erişim belirteci ve rapor kimliği aldıktan sonra biz JavaScript kullanarak raporu eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="91675-143">After you have the access token and the report id, we can embed the report using JavaScript.</span></span> <span data-ttu-id="91675-144">Bu, nuget yüklemenizi gerektirir [Power BI JavaScript paket](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span><span class="sxs-lookup"><span data-stu-id="91675-144">This requires that you install the nuget [Power BI JavaScript package](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/).</span></span> <span data-ttu-id="91675-145">EmbedUrl yalnızca https://embedded.powerbi.com/appTokenReportEmbed olacaktır.</span><span class="sxs-lookup"><span data-stu-id="91675-145">The embedUrl will just be https://embedded.powerbi.com/appTokenReportEmbed.</span></span>

> [!NOTE]
> <span data-ttu-id="91675-146">Kullanabileceğiniz [JavaScript rapor katıştırmak örnek](https://microsoft.github.io/PowerBI-JavaScript/demo/) işlevselliğini test etmek için.</span><span class="sxs-lookup"><span data-stu-id="91675-146">You can use the [JavaScript Report Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) to test functionality.</span></span> <span data-ttu-id="91675-147">Aynı zamanda kullanılabilir farklı işlemler için kod örnekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="91675-147">It also gives code examples for the different operations that are available.</span></span>

<span data-ttu-id="91675-148">**NuGet paketi yüklemesi**</span><span class="sxs-lookup"><span data-stu-id="91675-148">**NuGet package install**</span></span>

```
Install-Package Microsoft.PowerBI.JavaScript
```

<span data-ttu-id="91675-149">**JavaScript kodu**</span><span class="sxs-lookup"><span data-stu-id="91675-149">**JavaScript code**</span></span>

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

### <a name="set-the-size-of-embedded-elements"></a><span data-ttu-id="91675-150">Katıştırılmış öğelerinin boyutunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="91675-150">Set the size of embedded elements</span></span>

<span data-ttu-id="91675-151">Rapor kapsayıcısı boyutuna göre otomatik olarak katıştırılır.</span><span class="sxs-lookup"><span data-stu-id="91675-151">The report will automatically be embedded based on the size of its container.</span></span> <span data-ttu-id="91675-152">Varsayılan boyutu geçersiz kılmak için katıştırır genişliği ve yüksekliği için bir CSS sınıfı özniteliği veya satır içi stil eklemeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="91675-152">To override the default size of the embeds simply add a CSS class attribute or inline styles for width & height.</span></span>

## <a name="see-also"></a><span data-ttu-id="91675-153">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="91675-153">See also</span></span>

[<span data-ttu-id="91675-154">Bir örnek ile kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="91675-154">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="91675-155">Power BI Embedded ile kimlik doğrulaması ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="91675-155">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="91675-156">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="91675-156">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="91675-157">JavaScript Örnek Ekleme</span><span class="sxs-lookup"><span data-stu-id="91675-157">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="91675-158">Power BI JavaScript paketi</span><span class="sxs-lookup"><span data-stu-id="91675-158">Power BI JavaScript package</span></span>](https://www.nuget.org/packages/Microsoft.PowerBI.JavaScript/)  
<span data-ttu-id="91675-159">[Power BI API'si NuGet paketi](https://www.nuget.org/profiles/powerbi)
[Power BI çekirdek NuGut paketi](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span><span class="sxs-lookup"><span data-stu-id="91675-159">[Power BI API NuGet package](https://www.nuget.org/profiles/powerbi)
[Power BI Core NuGut Package](https://www.nuget.org/packages/Microsoft.PowerBI.Core/)</span></span>  
[<span data-ttu-id="91675-160">Powerbı CSharp Git deposu</span><span class="sxs-lookup"><span data-stu-id="91675-160">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="91675-161">Powerbı düğümlü Git deposu</span><span class="sxs-lookup"><span data-stu-id="91675-161">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="91675-162">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="91675-162">More questions?</span></span> [<span data-ttu-id="91675-163">Power BI Topluluğu'nu deneyin</span><span class="sxs-lookup"><span data-stu-id="91675-163">Try the Power BI Community</span></span>](http://community.powerbi.com/)
