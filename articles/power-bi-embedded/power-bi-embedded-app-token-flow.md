---
title: "Power BI Embedded ile kimlik doğrulama ve yetkilendirme"
description: "Power BI Embedded ile kimlik doğrulama ve yetkilendirme"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 93027f0f5467e0b21c47bbcbc84c67cdd50b26b8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="fdcb9-103">Power BI Embedded ile kimlik doğrulama ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="fdcb9-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="fdcb9-104">Power BI Embedded hizmet kullandığı **anahtarları** ve **uygulama belirteçleri** kimlik doğrulaması ve yetkilendirme açık son kullanıcı kimlik doğrulaması yerine.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-104">The Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="fdcb9-105">Bu modelde, kimlik doğrulama ve yetkilendirme kullanıcılarınızın uygulamanızın yönetir.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="fdcb9-106">Gerekli olduğunda, uygulamanızın oluşturur ve istenen rapor oluşturmak üzere hizmete bildirir uygulama belirteçleri gönderir.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-106">When necessary, your app creates and sends the App Tokens that tells our service to render the requested report.</span></span> <span data-ttu-id="fdcb9-107">Hala; ancak bu tasarımı uygulamanız Azure Active Directory kullanıcı kimlik doğrulaması ve yetkilendirme için kullanılacak gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-107">This design doesn't require your app to use Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-to-authenticate"></a><span data-ttu-id="fdcb9-108">Kimlik doğrulaması için iki yol</span><span class="sxs-lookup"><span data-stu-id="fdcb9-108">Two ways to authenticate</span></span>

<span data-ttu-id="fdcb9-109">**Anahtar** -tüm Power BI Embedded REST API çağrıları için tuşlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="fdcb9-110">Anahtarları bulunabilir **Azure portal** tıklayarak **tüm ayarları** ve ardından **erişim anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-110">The keys can be found in the **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="fdcb9-111">Her zaman bir parola değilmiş gibi anahtarınızı kabul eder.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="fdcb9-112">Bu anahtarlar üzerinde belirli çalışma alanı koleksiyonu çağrı herhangi bir REST API'nin yapma izinlerine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-112">These keys have permissions to make any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="fdcb9-113">Bir anahtar REST çağrısı kullanmak için aşağıdaki authorization üstbilgisi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fdcb9-113">To use a key on a REST call, add the following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="fdcb9-114">**Uygulama belirteci** -uygulama belirteçleri katıştırma tüm istekler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="fdcb9-115">Tek bir rapor sınırlı ve bir sona erme süresini ayarlamak için en iyi bir uygulamadır için istemci tarafı çalıştırılmak üzere tasarlanmışlardır.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-115">They’re designed to be run client-side, so they're restricted to a single report and it’s best practice to set an expiration time.</span></span>

<span data-ttu-id="fdcb9-116">Uygulama belirteçleri anahtarlarınızı biri tarafından imzalanan JWT (JSON Web belirteci) var.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="fdcb9-117">Uygulama belirteci aşağıdaki talep içerebilir:</span><span class="sxs-lookup"><span data-stu-id="fdcb9-117">Your app token can contain the following claims:</span></span>

| <span data-ttu-id="fdcb9-118">İste</span><span class="sxs-lookup"><span data-stu-id="fdcb9-118">Claim</span></span> | <span data-ttu-id="fdcb9-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdcb9-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fdcb9-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="fdcb9-120">**ver**</span></span> |<span data-ttu-id="fdcb9-121">Uygulama belirteci sürümü.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-121">The version of the app token.</span></span> <span data-ttu-id="fdcb9-122">0.2.0 geçerli sürümdür.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-122">0.2.0 is the current version.</span></span> |
| <span data-ttu-id="fdcb9-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="fdcb9-123">**aud**</span></span> |<span data-ttu-id="fdcb9-124">Belirtecin hedeflenen alıcı.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-124">The intended recipient of the token.</span></span> <span data-ttu-id="fdcb9-125">Power BI Embedded kullanılacak: "https://analysis.windows.net/powerbi/api".</span><span class="sxs-lookup"><span data-stu-id="fdcb9-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="fdcb9-126">**ISS**</span><span class="sxs-lookup"><span data-stu-id="fdcb9-126">**iss**</span></span> |<span data-ttu-id="fdcb9-127">Belirtecin uygulama gösteren bir dize.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-127">A string indicating the application which issued the token.</span></span> |
| <span data-ttu-id="fdcb9-128">**türü**</span><span class="sxs-lookup"><span data-stu-id="fdcb9-128">**type**</span></span> |<span data-ttu-id="fdcb9-129">Oluşturulan uygulama Belirtecin türü.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-129">The type of app token which is being created.</span></span> <span data-ttu-id="fdcb9-130">Geçerli tek desteklenen türüdür **katıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-130">Current the only supported type is **embed**.</span></span> |
| <span data-ttu-id="fdcb9-131">**WCN**</span><span class="sxs-lookup"><span data-stu-id="fdcb9-131">**wcn**</span></span> |<span data-ttu-id="fdcb9-132">Çalışma alanı koleksiyonu adı belirteci için yayımlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-132">Workspace collection name the token is being issued for.</span></span> |
| <span data-ttu-id="fdcb9-133">**WID**</span><span class="sxs-lookup"><span data-stu-id="fdcb9-133">**wid**</span></span> |<span data-ttu-id="fdcb9-134">Çalışma alanı kimliği belirteci için yayımlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-134">Workspace ID the token is being issued for.</span></span> |
| <span data-ttu-id="fdcb9-135">**RID**</span><span class="sxs-lookup"><span data-stu-id="fdcb9-135">**rid**</span></span> |<span data-ttu-id="fdcb9-136">Rapor Kimliği belirteci için yayımlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-136">Report ID the token is being issued for.</span></span> |
| <span data-ttu-id="fdcb9-137">**Kullanıcı adı** (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="fdcb9-137">**username** (optional)</span></span> |<span data-ttu-id="fdcb9-138">RLS ile kullanıldığında, bu kullanıcının RLS kuralları uygularken belirlemenize yardımcı olabilecek bir dize değeridir.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-138">Used with RLS, this is a string that can help identify the user when applying RLS rules.</span></span> |
| <span data-ttu-id="fdcb9-139">**rolleri** (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="fdcb9-139">**roles** (optional)</span></span> |<span data-ttu-id="fdcb9-140">Satır düzeyi güvenlik kuralları uygularken seçmek için rolleri içeren bir dize.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-140">A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="fdcb9-141">Birden fazla rol geçirilirse, dizesi dizisi olarak aktarılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="fdcb9-142">**SCP** (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="fdcb9-142">**scp** (optional)</span></span> |<span data-ttu-id="fdcb9-143">İzinleri kapsamları içeren bir dize.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-143">A string containing the permissions scopes.</span></span> <span data-ttu-id="fdcb9-144">Birden fazla rol geçirilirse, dizesi dizisi olarak aktarılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="fdcb9-145">**exp** (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="fdcb9-145">**exp** (optional)</span></span> |<span data-ttu-id="fdcb9-146">Belirteç sona erecek süresini gösterir.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-146">Indicates the time in which the token will expire.</span></span> <span data-ttu-id="fdcb9-147">Bu UNIX zaman damgaları geçirilmesi.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="fdcb9-148">**NBF** (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="fdcb9-148">**nbf** (optional)</span></span> |<span data-ttu-id="fdcb9-149">İçinde belirtecin geçerli olan başladığı saati belirtir.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-149">Indicates the time in which the token starts being valid.</span></span> <span data-ttu-id="fdcb9-150">Bu UNIX zaman damgaları geçirilmesi.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="fdcb9-151">Örnek bir uygulama belirtecini şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="fdcb9-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="fdcb9-152">Kodunu çözdü, şunun gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="fdcb9-152">When decoded, it will look something like this:</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

<span data-ttu-id="fdcb9-153">Apptokens oluşturulmasını kolaylaştırmak SDK içinde kullanılabilir yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-153">There are methods available within the SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="fdcb9-154">Örneğin, .NET için bakabilirsiniz [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) sınıfı ve [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-154">For example, for .NET you can look at the [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="fdcb9-155">.NET SDK için başvurabilirsiniz [kapsamları](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="fdcb9-155">For the .NET SDK, you can refer to [Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="fdcb9-156">Kapsamları</span><span class="sxs-lookup"><span data-stu-id="fdcb9-156">Scopes</span></span>

<span data-ttu-id="fdcb9-157">Embed belirteçleri kullanırken, erişim hakkı vermek kaynak kullanımını kısıtlamak istediğinizi düşünelim.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-157">When using Embed tokens, you may want to restrict usage of the resources you give access to.</span></span> <span data-ttu-id="fdcb9-158">Bu nedenle, kapsamlı izinlere sahip bir belirteç oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="fdcb9-159">Power BI Embedded kullanılabilir kapsamlarının verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-159">The following are the available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="fdcb9-160">Kapsam</span><span class="sxs-lookup"><span data-stu-id="fdcb9-160">Scope</span></span>|<span data-ttu-id="fdcb9-161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fdcb9-161">Description</span></span>|
|---|---|
|<span data-ttu-id="fdcb9-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="fdcb9-162">Dataset.Read</span></span>|<span data-ttu-id="fdcb9-163">Belirtilen veri okuma izni sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-163">Provides permission to read the specified dataset.</span></span>|
|<span data-ttu-id="fdcb9-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="fdcb9-164">Dataset.Write</span></span>|<span data-ttu-id="fdcb9-165">Belirtilen veri kümesi için yazma izni sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-165">Provides permission to write to the specified dataset.</span></span>|
|<span data-ttu-id="fdcb9-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="fdcb9-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="fdcb9-167">Belirtilen veri kümesine okumasına ve yazmasına izin sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-167">Provides permission to read and write to the specificed dataset.</span></span>|
|<span data-ttu-id="fdcb9-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="fdcb9-168">Report.Read</span></span>|<span data-ttu-id="fdcb9-169">Belirtilen rapor görüntüleme izni sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-169">Provides permission to view the specified report.</span></span>|
|<span data-ttu-id="fdcb9-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="fdcb9-170">Report.ReadWrite</span></span>|<span data-ttu-id="fdcb9-171">Görüntülemek ve belirtilen rapor düzenleme izni sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-171">Provides permission to view and edit the specified report.</span></span>|
|<span data-ttu-id="fdcb9-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="fdcb9-172">Workspace.Report.Create</span></span>|<span data-ttu-id="fdcb9-173">Belirtilen çalışma alanı içinde yeni bir rapor oluşturma izni sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-173">Provides permission to create a new report within the specified workspace.</span></span>|
|<span data-ttu-id="fdcb9-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="fdcb9-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="fdcb9-175">Var olan bir raporu belirtilen çalışma alanı içindeki kopyalamaya izin sağlar.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-175">Provides permission to clone an existing report within the specified workspace.</span></span>|

<span data-ttu-id="fdcb9-176">Aşağıdaki gibi kapsamları arasında bir boşluk kullanarak birden çok kapsam sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-176">You can supply multiple scopes by using a space between the scopes like the following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="fdcb9-177">**Gerekli talep - kapsamları**</span><span class="sxs-lookup"><span data-stu-id="fdcb9-177">**Required claims - scopes**</span></span>

<span data-ttu-id="fdcb9-178">SCP: {scopesClaim} scopesClaim bir dize veya bir çalışma alanı kaynaklarına (rapor, veri kümesi, vb.) izin verilen izinleri belirterek bir dizeler dizisi olabilir</span><span class="sxs-lookup"><span data-stu-id="fdcb9-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting the allowed permissions to workspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="fdcb9-179">Kodu çözülmüş bir belirteç tanımlanan kapsamlarla aşağıdakine benzer görünecektir.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-179">A decoded token, with scopes defined, would look similar to the following.</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a><span data-ttu-id="fdcb9-180">İşlemler ve kapsamlar</span><span class="sxs-lookup"><span data-stu-id="fdcb9-180">Operations and scopes</span></span>

|<span data-ttu-id="fdcb9-181">İşlem</span><span class="sxs-lookup"><span data-stu-id="fdcb9-181">Operation</span></span>|<span data-ttu-id="fdcb9-182">Hedef kaynak</span><span class="sxs-lookup"><span data-stu-id="fdcb9-182">Target resource</span></span>|<span data-ttu-id="fdcb9-183">Belirteç izinleri</span><span class="sxs-lookup"><span data-stu-id="fdcb9-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="fdcb9-184">(Bellek içi) dayalı bir veri kümesine yeni bir rapor oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="fdcb9-185">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="fdcb9-185">Dataset</span></span>|<span data-ttu-id="fdcb9-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="fdcb9-186">Dataset.Read</span></span>|
|<span data-ttu-id="fdcb9-187">(Bellek içi) dayalı bir veri kümesine yeni bir rapor oluşturun ve raporu kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-187">Create (in-memory) a new report based on a dataset and save the report.</span></span>|<span data-ttu-id="fdcb9-188">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="fdcb9-188">Dataset</span></span>|<span data-ttu-id="fdcb9-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="fdcb9-189">* Dataset.Read</span></span><br><span data-ttu-id="fdcb9-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="fdcb9-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="fdcb9-191">Görüntüleyin ve (bellek içi) var olan bir raporu keşfedin/düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="fdcb9-192">Report.Read Dataset.Read anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="fdcb9-193">Bu düzenlemeleri kaydetmek için izinlere izin vermez.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-193">This will not allow permissions to save edits.</span></span>|<span data-ttu-id="fdcb9-194">Rapor</span><span class="sxs-lookup"><span data-stu-id="fdcb9-194">Report</span></span>|<span data-ttu-id="fdcb9-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="fdcb9-195">Report.Read</span></span>|
|<span data-ttu-id="fdcb9-196">Düzenle ve var olan bir raporu kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-196">Edit and save an existing report.</span></span>|<span data-ttu-id="fdcb9-197">Rapor</span><span class="sxs-lookup"><span data-stu-id="fdcb9-197">Report</span></span>|<span data-ttu-id="fdcb9-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="fdcb9-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="fdcb9-199">(Farklı Kaydet) bir raporun bir kopyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="fdcb9-200">Rapor</span><span class="sxs-lookup"><span data-stu-id="fdcb9-200">Report</span></span>|<span data-ttu-id="fdcb9-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="fdcb9-201">* Report.Read</span></span><br><span data-ttu-id="fdcb9-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="fdcb9-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-the-flow-works"></a><span data-ttu-id="fdcb9-203">İşte akışı nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="fdcb9-203">Here's how the flow works</span></span>
1. <span data-ttu-id="fdcb9-204">API anahtarları uygulamanıza kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-204">Copy the API keys to your application.</span></span> <span data-ttu-id="fdcb9-205">Anahtarları alabileceğiniz **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-205">You can get the keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="fdcb9-206">Belirteç talep onaylar ve sona erme süresi vardır.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="fdcb9-207">Belirteci bir API erişim anahtarlarla imzalanması.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="fdcb9-208">Bir raporu görüntülemek için kullanıcı istekleri.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-208">User requests to view a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="fdcb9-209">Belirteç API'si erişim tuşları ile doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="fdcb9-210">Power BI Embedded, kullanıcıya bir rapor gönderir.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-210">Power BI Embedded sends a report to user.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="fdcb9-211">Sonra **Power BI Embedded** rapor kullanıcı, kullanıcı için bir özel uygulamanızda raporunu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-211">After **Power BI Embedded** sends a report to the user, the user can view the report in your custom app.</span></span> <span data-ttu-id="fdcb9-212">Örneğin, içeri aktardığınız [çözümleme satış verileri PBIX örnek](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), örnek web uygulaması şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="fdcb9-212">For example, if you imported the [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="fdcb9-213">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="fdcb9-213">See Also</span></span>

[<span data-ttu-id="fdcb9-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="fdcb9-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="fdcb9-215">Microsoft Power BI Embedded örneği kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="fdcb9-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="fdcb9-216">Microsoft Power BI Embedded senaryoları</span><span class="sxs-lookup"><span data-stu-id="fdcb9-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="fdcb9-217">Microsoft Power BI Embedded ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="fdcb9-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="fdcb9-218">Powerbı CSharp Git deposu</span><span class="sxs-lookup"><span data-stu-id="fdcb9-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="fdcb9-219">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="fdcb9-219">More questions?</span></span> [<span data-ttu-id="fdcb9-220">Power BI Topluluğu'nu deneyin</span><span class="sxs-lookup"><span data-stu-id="fdcb9-220">Try the Power BI Community</span></span>](http://community.powerbi.com/)

