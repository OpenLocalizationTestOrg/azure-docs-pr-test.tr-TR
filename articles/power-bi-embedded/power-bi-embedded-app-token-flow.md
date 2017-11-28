---
title: aaaAuthenticating ve Power BI Embedded ile yetkisi verme
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
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="89a6a-103">Power BI Embedded ile kimlik doğrulama ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="89a6a-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="89a6a-104">Merhaba Power BI Embedded hizmeti kullanan **anahtarları** ve **uygulama belirteçleri** kimlik doğrulaması ve yetkilendirme açık son kullanıcı kimlik doğrulaması yerine.</span><span class="sxs-lookup"><span data-stu-id="89a6a-104">hello Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="89a6a-105">Bu modelde, kimlik doğrulama ve yetkilendirme kullanıcılarınızın uygulamanızın yönetir.</span><span class="sxs-lookup"><span data-stu-id="89a6a-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="89a6a-106">Gerekli olduğunda, uygulamanızın oluşturur ve istenen rapor bizim hizmet toorender söyler hello uygulama belirteçleri hello gönderir.</span><span class="sxs-lookup"><span data-stu-id="89a6a-106">When necessary, your app creates and sends hello App Tokens that tells our service toorender hello requested report.</span></span> <span data-ttu-id="89a6a-107">Hala; ancak bu tasarım, uygulama toouse Azure Active Directory kullanıcı kimlik doğrulaması ve yetkilendirme için gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="89a6a-107">This design doesn't require your app toouse Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-tooauthenticate"></a><span data-ttu-id="89a6a-108">İki yolla tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="89a6a-108">Two ways tooauthenticate</span></span>

<span data-ttu-id="89a6a-109">**Anahtar** -tüm Power BI Embedded REST API çağrıları için tuşlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89a6a-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="89a6a-110">Merhaba anahtarları hello bulunabilir **Azure portal** tıklayarak **tüm ayarları** ve ardından **erişim anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="89a6a-110">hello keys can be found in hello **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="89a6a-111">Her zaman bir parola değilmiş gibi anahtarınızı kabul eder.</span><span class="sxs-lookup"><span data-stu-id="89a6a-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="89a6a-112">Bu anahtarlar tüm REST API çağrısı belirli çalışma alanı koleksiyonu üzerinde izinleri toomake sahiptir.</span><span class="sxs-lookup"><span data-stu-id="89a6a-112">These keys have permissions toomake any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="89a6a-113">toouse REST çağrısı bir anahtar authorization üstbilgisi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="89a6a-113">toouse a key on a REST call, add hello following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="89a6a-114">**Uygulama belirteci** -uygulama belirteçleri katıştırma tüm istekler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="89a6a-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="89a6a-115">Oldukları çalıştırmak tasarlanmış toobe istemci-tarafı, kısıtlı bulunmaları tooa tek raporu ve kendi en iyi yöntem tooset bir sona erme zamanı.</span><span class="sxs-lookup"><span data-stu-id="89a6a-115">They’re designed toobe run client-side, so they're restricted tooa single report and it’s best practice tooset an expiration time.</span></span>

<span data-ttu-id="89a6a-116">Uygulama belirteçleri anahtarlarınızı biri tarafından imzalanan JWT (JSON Web belirteci) var.</span><span class="sxs-lookup"><span data-stu-id="89a6a-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="89a6a-117">Uygulama belirtecinizi talepler aşağıdaki hello içerebilir:</span><span class="sxs-lookup"><span data-stu-id="89a6a-117">Your app token can contain hello following claims:</span></span>

| <span data-ttu-id="89a6a-118">İste</span><span class="sxs-lookup"><span data-stu-id="89a6a-118">Claim</span></span> | <span data-ttu-id="89a6a-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="89a6a-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="89a6a-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="89a6a-120">**ver**</span></span> |<span data-ttu-id="89a6a-121">Merhaba uygulama belirteci Hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="89a6a-121">hello version of hello app token.</span></span> <span data-ttu-id="89a6a-122">0.2.0 hello geçerli sürümdür.</span><span class="sxs-lookup"><span data-stu-id="89a6a-122">0.2.0 is hello current version.</span></span> |
| <span data-ttu-id="89a6a-123">**aud**</span><span class="sxs-lookup"><span data-stu-id="89a6a-123">**aud**</span></span> |<span data-ttu-id="89a6a-124">Merhaba alıcı hello belirtecin amacı.</span><span class="sxs-lookup"><span data-stu-id="89a6a-124">hello intended recipient of hello token.</span></span> <span data-ttu-id="89a6a-125">Power BI Embedded kullanılacak: "https://analysis.windows.net/powerbi/api".</span><span class="sxs-lookup"><span data-stu-id="89a6a-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="89a6a-126">**ISS**</span><span class="sxs-lookup"><span data-stu-id="89a6a-126">**iss**</span></span> |<span data-ttu-id="89a6a-127">Merhaba belirteç Merhaba uygulaması gösteren bir dize.</span><span class="sxs-lookup"><span data-stu-id="89a6a-127">A string indicating hello application which issued hello token.</span></span> |
| <span data-ttu-id="89a6a-128">**türü**</span><span class="sxs-lookup"><span data-stu-id="89a6a-128">**type**</span></span> |<span data-ttu-id="89a6a-129">oluşturulan uygulama belirteci Hello türü.</span><span class="sxs-lookup"><span data-stu-id="89a6a-129">hello type of app token which is being created.</span></span> <span data-ttu-id="89a6a-130">Geçerli hello yalnızca desteklenen tür **katıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="89a6a-130">Current hello only supported type is **embed**.</span></span> |
| <span data-ttu-id="89a6a-131">**WCN**</span><span class="sxs-lookup"><span data-stu-id="89a6a-131">**wcn**</span></span> |<span data-ttu-id="89a6a-132">Çalışma alanı koleksiyonu ad hello simgesi için yayımlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="89a6a-132">Workspace collection name hello token is being issued for.</span></span> |
| <span data-ttu-id="89a6a-133">**WID**</span><span class="sxs-lookup"><span data-stu-id="89a6a-133">**wid**</span></span> |<span data-ttu-id="89a6a-134">Çalışma alanı kimliği hello belirteci için yayımlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="89a6a-134">Workspace ID hello token is being issued for.</span></span> |
| <span data-ttu-id="89a6a-135">**RID**</span><span class="sxs-lookup"><span data-stu-id="89a6a-135">**rid**</span></span> |<span data-ttu-id="89a6a-136">Kimliği hello belirteci verilen bildirin.</span><span class="sxs-lookup"><span data-stu-id="89a6a-136">Report ID hello token is being issued for.</span></span> |
| <span data-ttu-id="89a6a-137">**Kullanıcı adı** (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="89a6a-137">**username** (optional)</span></span> |<span data-ttu-id="89a6a-138">RLS ile kullanıldığında, bu RLS kuralları uygularken hello kullanıcı belirlemenize yardımcı olabilecek bir dize değeridir.</span><span class="sxs-lookup"><span data-stu-id="89a6a-138">Used with RLS, this is a string that can help identify hello user when applying RLS rules.</span></span> |
| <span data-ttu-id="89a6a-139">**rolleri** (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="89a6a-139">**roles** (optional)</span></span> |<span data-ttu-id="89a6a-140">Satır düzeyi güvenlik kuralları uygularken Hello rolleri tooselect içeren bir dize.</span><span class="sxs-lookup"><span data-stu-id="89a6a-140">A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="89a6a-141">Birden fazla rol geçirilirse, dizesi dizisi olarak aktarılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="89a6a-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="89a6a-142">**SCP** (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="89a6a-142">**scp** (optional)</span></span> |<span data-ttu-id="89a6a-143">Merhaba izinleri kapsamları içeren bir dize.</span><span class="sxs-lookup"><span data-stu-id="89a6a-143">A string containing hello permissions scopes.</span></span> <span data-ttu-id="89a6a-144">Birden fazla rol geçirilirse, dizesi dizisi olarak aktarılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="89a6a-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="89a6a-145">**exp** (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="89a6a-145">**exp** (optional)</span></span> |<span data-ttu-id="89a6a-146">Hangi hello belirteci dolacak hello süresini gösterir.</span><span class="sxs-lookup"><span data-stu-id="89a6a-146">Indicates hello time in which hello token will expire.</span></span> <span data-ttu-id="89a6a-147">Bu UNIX zaman damgaları geçirilmesi.</span><span class="sxs-lookup"><span data-stu-id="89a6a-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="89a6a-148">**NBF** (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="89a6a-148">**nbf** (optional)</span></span> |<span data-ttu-id="89a6a-149">Hangi hello belirteci geçerli olan hello başlatılışında gösterir.</span><span class="sxs-lookup"><span data-stu-id="89a6a-149">Indicates hello time in which hello token starts being valid.</span></span> <span data-ttu-id="89a6a-150">Bu UNIX zaman damgaları geçirilmesi.</span><span class="sxs-lookup"><span data-stu-id="89a6a-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="89a6a-151">Örnek bir uygulama belirtecini şuna benzeyecektir:</span><span class="sxs-lookup"><span data-stu-id="89a6a-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="89a6a-152">Kodunu çözdü, şunun gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="89a6a-152">When decoded, it will look something like this:</span></span>

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

<span data-ttu-id="89a6a-153">Merhaba apptokens oluşturulmasını kolaylaştırmak SDK'ları içinde kullanılabilir yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="89a6a-153">There are methods available within hello SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="89a6a-154">Örneğin, .NET için hello bakabilir [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) sınıfı ve hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="89a6a-154">For example, for .NET you can look at hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="89a6a-155">Çok başvurabilir Hello .NET SDK'sı için[kapsamları](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="89a6a-155">For hello .NET SDK, you can refer too[Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="89a6a-156">Kapsamları</span><span class="sxs-lookup"><span data-stu-id="89a6a-156">Scopes</span></span>

<span data-ttu-id="89a6a-157">Embed belirteçleri kullanırken toorestrict kullanım hello kaynakların erişim hakkı vermek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89a6a-157">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="89a6a-158">Bu nedenle, kapsamlı izinlere sahip bir belirteç oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89a6a-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="89a6a-159">Merhaba, Power BI Embedded için kullanılabilir kapsamı hello verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="89a6a-159">hello following are hello available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="89a6a-160">Kapsam</span><span class="sxs-lookup"><span data-stu-id="89a6a-160">Scope</span></span>|<span data-ttu-id="89a6a-161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="89a6a-161">Description</span></span>|
|---|---|
|<span data-ttu-id="89a6a-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="89a6a-162">Dataset.Read</span></span>|<span data-ttu-id="89a6a-163">İzin sağlar tooread hello belirtilen veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="89a6a-163">Provides permission tooread hello specified dataset.</span></span>|
|<span data-ttu-id="89a6a-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="89a6a-164">Dataset.Write</span></span>|<span data-ttu-id="89a6a-165">Belirtilen izin toowrite toohello sağlayan veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="89a6a-165">Provides permission toowrite toohello specified dataset.</span></span>|
|<span data-ttu-id="89a6a-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="89a6a-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="89a6a-167">İzin tooread ve yazma toohello komutla veri kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="89a6a-167">Provides permission tooread and write toohello specificed dataset.</span></span>|
|<span data-ttu-id="89a6a-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="89a6a-168">Report.Read</span></span>|<span data-ttu-id="89a6a-169">İzin sağlar tooview hello belirtilen rapor.</span><span class="sxs-lookup"><span data-stu-id="89a6a-169">Provides permission tooview hello specified report.</span></span>|
|<span data-ttu-id="89a6a-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="89a6a-170">Report.ReadWrite</span></span>|<span data-ttu-id="89a6a-171">Belirtilen rapor izni tooview ve düzenleme hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="89a6a-171">Provides permission tooview and edit hello specified report.</span></span>|
|<span data-ttu-id="89a6a-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="89a6a-172">Workspace.Report.Create</span></span>|<span data-ttu-id="89a6a-173">Yeni bir rapor içinde belirtilen hello izni toocreate sağlar çalışma.</span><span class="sxs-lookup"><span data-stu-id="89a6a-173">Provides permission toocreate a new report within hello specified workspace.</span></span>|
|<span data-ttu-id="89a6a-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="89a6a-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="89a6a-175">Var olan bir raporu belirtilen hello içinde izin tooclone sağlar çalışma.</span><span class="sxs-lookup"><span data-stu-id="89a6a-175">Provides permission tooclone an existing report within hello specified workspace.</span></span>|

<span data-ttu-id="89a6a-176">Merhaba aşağıdaki gibi hello kapsamları arasında bir boşluk kullanarak birden çok kapsam sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="89a6a-176">You can supply multiple scopes by using a space between hello scopes like hello following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="89a6a-177">**Gerekli talep - kapsamları**</span><span class="sxs-lookup"><span data-stu-id="89a6a-177">**Required claims - scopes**</span></span>

<span data-ttu-id="89a6a-178">SCP: {scopesClaim} scopesClaim bir dize veya hello izin verilen izinleri tooworkspace kaynakları (rapor, veri kümesi, vb.) belirlenerek bir dizeler dizisi olabilir</span><span class="sxs-lookup"><span data-stu-id="89a6a-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting hello allowed permissions tooworkspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="89a6a-179">Tanımlı, kapsamları bir kodu çözülmüş belirteciyle benzer toohello aşağıdaki görünür.</span><span class="sxs-lookup"><span data-stu-id="89a6a-179">A decoded token, with scopes defined, would look similar toohello following.</span></span>

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

### <a name="operations-and-scopes"></a><span data-ttu-id="89a6a-180">İşlemler ve kapsamlar</span><span class="sxs-lookup"><span data-stu-id="89a6a-180">Operations and scopes</span></span>

|<span data-ttu-id="89a6a-181">İşlem</span><span class="sxs-lookup"><span data-stu-id="89a6a-181">Operation</span></span>|<span data-ttu-id="89a6a-182">Hedef kaynak</span><span class="sxs-lookup"><span data-stu-id="89a6a-182">Target resource</span></span>|<span data-ttu-id="89a6a-183">Belirteç izinleri</span><span class="sxs-lookup"><span data-stu-id="89a6a-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="89a6a-184">(Bellek içi) dayalı bir veri kümesine yeni bir rapor oluşturun.</span><span class="sxs-lookup"><span data-stu-id="89a6a-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="89a6a-185">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="89a6a-185">Dataset</span></span>|<span data-ttu-id="89a6a-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="89a6a-186">Dataset.Read</span></span>|
|<span data-ttu-id="89a6a-187">(Bellek içi) dayalı bir veri kümesine yeni bir rapor oluşturun ve hello raporu kaydedin.</span><span class="sxs-lookup"><span data-stu-id="89a6a-187">Create (in-memory) a new report based on a dataset and save hello report.</span></span>|<span data-ttu-id="89a6a-188">Veri kümesi</span><span class="sxs-lookup"><span data-stu-id="89a6a-188">Dataset</span></span>|<span data-ttu-id="89a6a-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="89a6a-189">* Dataset.Read</span></span><br><span data-ttu-id="89a6a-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="89a6a-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="89a6a-191">Görüntüleyin ve (bellek içi) var olan bir raporu keşfedin/düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="89a6a-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="89a6a-192">Report.Read Dataset.Read anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="89a6a-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="89a6a-193">Bu izinleri toosave düzenlemeleri izin vermez.</span><span class="sxs-lookup"><span data-stu-id="89a6a-193">This will not allow permissions toosave edits.</span></span>|<span data-ttu-id="89a6a-194">Rapor</span><span class="sxs-lookup"><span data-stu-id="89a6a-194">Report</span></span>|<span data-ttu-id="89a6a-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="89a6a-195">Report.Read</span></span>|
|<span data-ttu-id="89a6a-196">Düzenle ve var olan bir raporu kaydedin.</span><span class="sxs-lookup"><span data-stu-id="89a6a-196">Edit and save an existing report.</span></span>|<span data-ttu-id="89a6a-197">Rapor</span><span class="sxs-lookup"><span data-stu-id="89a6a-197">Report</span></span>|<span data-ttu-id="89a6a-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="89a6a-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="89a6a-199">(Farklı Kaydet) bir raporun bir kopyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="89a6a-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="89a6a-200">Rapor</span><span class="sxs-lookup"><span data-stu-id="89a6a-200">Report</span></span>|<span data-ttu-id="89a6a-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="89a6a-201">* Report.Read</span></span><br><span data-ttu-id="89a6a-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="89a6a-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-hello-flow-works"></a><span data-ttu-id="89a6a-203">İşte hello akışı nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="89a6a-203">Here's how hello flow works</span></span>
1. <span data-ttu-id="89a6a-204">Merhaba API anahtarları tooyour uygulaması kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="89a6a-204">Copy hello API keys tooyour application.</span></span> <span data-ttu-id="89a6a-205">Merhaba anahtarları alabileceğiniz **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="89a6a-205">You can get hello keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="89a6a-206">Belirteç talep onaylar ve sona erme süresi vardır.</span><span class="sxs-lookup"><span data-stu-id="89a6a-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="89a6a-207">Belirteci bir API erişim anahtarlarla imzalanması.</span><span class="sxs-lookup"><span data-stu-id="89a6a-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="89a6a-208">Kullanıcı bir rapor tooview ister.</span><span class="sxs-lookup"><span data-stu-id="89a6a-208">User requests tooview a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="89a6a-209">Belirteç API'si erişim tuşları ile doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="89a6a-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="89a6a-210">Power BI Embedded rapor toouser gönderir.</span><span class="sxs-lookup"><span data-stu-id="89a6a-210">Power BI Embedded sends a report toouser.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="89a6a-211">Sonra **Power BI Embedded** bir rapor toohello kullanıcı gönderir hello kullanıcı özel uygulamanızda hello raporu görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89a6a-211">After **Power BI Embedded** sends a report toohello user, hello user can view hello report in your custom app.</span></span> <span data-ttu-id="89a6a-212">Örneğin, hello aldıysanız [çözümleme satış verileri PBIX örnek](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello örnek web uygulaması şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="89a6a-212">For example, if you imported hello [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="89a6a-213">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="89a6a-213">See Also</span></span>

[<span data-ttu-id="89a6a-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="89a6a-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="89a6a-215">Microsoft Power BI Embedded örneği kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="89a6a-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="89a6a-216">Microsoft Power BI Embedded senaryoları</span><span class="sxs-lookup"><span data-stu-id="89a6a-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="89a6a-217">Microsoft Power BI Embedded ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="89a6a-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="89a6a-218">Powerbı CSharp Git deposu</span><span class="sxs-lookup"><span data-stu-id="89a6a-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="89a6a-219">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="89a6a-219">More questions?</span></span> [<span data-ttu-id="89a6a-220">Merhaba Power BI topluluk deneyin</span><span class="sxs-lookup"><span data-stu-id="89a6a-220">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

