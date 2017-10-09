---
title: aaaAzure AD v2 ASP.NET Web sunucusu Getting Started - Test | Microsoft Docs
description: "Microsoft oturum açma Openıd Connect standardını kullanan geleneksel web tarayıcı tabanlı bir uygulama ile ASP.NET çözümünü uygulama"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="ee32b-103">Kodunuzu test</span><span class="sxs-lookup"><span data-stu-id="ee32b-103">Test your code</span></span>

<span data-ttu-id="ee32b-104">Tuşuna `F5` toorun projenizi Visual Studio'da.</span><span class="sxs-lookup"><span data-stu-id="ee32b-104">Press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="ee32b-105">Merhaba tarayıcı açılır ve çok doğrudan*http://localhost: {port}* burada göreceksiniz hello *oturum oturum Microsoft* düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ee32b-105">hello browser will open and direct you too*http://localhost:{port}* where you’ll see hello *Sign in with Microsoft* button.</span></span> <span data-ttu-id="ee32b-106">Bir tane de toosign'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ee32b-106">Go ahead and click it toosign in.</span></span>

<span data-ttu-id="ee32b-107">Hazır tootest, bir iş, okul (Azure Active Directory) veya (live.com, outlook.com) kişisel hesap toosign içinde kullanım olduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="ee32b-107">When you're ready tootest, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account toosign in.</span></span> 

![Microsoft tarayıcı penceresi ile oturum aç](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Microsoft tarayıcı penceresi ile oturum aç](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="ee32b-110">Beklenen sonuçları</span><span class="sxs-lookup"><span data-stu-id="ee32b-110">Expected results</span></span>
<span data-ttu-id="ee32b-111">Oturum açma işleminden sonra hello yeniden yönlendirilen toohello giriş sayfası, web sitenizin hello HTTPS uygulama kayıt bilgilerinizi hello Microsoft uygulama kayıt Portalı'nda belirtilen URL olan kullanıcıdır.</span><span class="sxs-lookup"><span data-stu-id="ee32b-111">After sign-in, hello user is redirected toohello home page of your web site which is hello HTTPS URL specified in your application registration information in hello Microsoft Application Registration Portal.</span></span> <span data-ttu-id="ee32b-112">Bu sayfayı artık gösterir *Hello {User}* ve bir bağlantı toosign genişletme ve bir bağlantı toohello Authorize denetleyicisi bağlantı toosee hello kullanıcının talepleri – oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="ee32b-112">This page now shows *Hello {User}* and a link toosign-out, and a link toosee hello user’s claims – which is a link toohello Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="ee32b-113">Kullanıcının talepleri bakın</span><span class="sxs-lookup"><span data-stu-id="ee32b-113">See user's claims</span></span>
<span data-ttu-id="ee32b-114">Merhaba köprü toosee hello kullanıcının talepleri seçin.</span><span class="sxs-lookup"><span data-stu-id="ee32b-114">Select hello hyperlink toosee hello user's claims.</span></span> <span data-ttu-id="ee32b-115">Bu, toohello denetleyici ve yalnızca kimlik doğrulaması kullanılabilir toousers görünüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee32b-115">This leads you toohello controller and view that is only available toousers that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="ee32b-116">Beklenen sonuçları</span><span class="sxs-lookup"><span data-stu-id="ee32b-116">Expected results</span></span>
 <span data-ttu-id="ee32b-117">Merhaba oturum açmış kullanıcı hello temel özelliklerini içeren bir tablo görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="ee32b-117">You should see a table containing hello basic properties of hello logged user:</span></span>

| <span data-ttu-id="ee32b-118">Özellik</span><span class="sxs-lookup"><span data-stu-id="ee32b-118">Property</span></span> | <span data-ttu-id="ee32b-119">Değer</span><span class="sxs-lookup"><span data-stu-id="ee32b-119">Value</span></span> | <span data-ttu-id="ee32b-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee32b-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="ee32b-121">Ad</span><span class="sxs-lookup"><span data-stu-id="ee32b-121">Name</span></span> | <span data-ttu-id="ee32b-122">{Tam} kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="ee32b-122">{User Full Name}</span></span> | <span data-ttu-id="ee32b-123">Merhaba kullanıcı adı ve Soyadı</span><span class="sxs-lookup"><span data-stu-id="ee32b-123">hello user’s first and last name</span></span>
|<span data-ttu-id="ee32b-124">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="ee32b-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="ee32b-125">kullanılan tooidentify hello oturum açmış kullanıcı Hello kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="ee32b-125">hello username used tooidentify hello logged user</span></span>
| <span data-ttu-id="ee32b-126">Konu</span><span class="sxs-lookup"><span data-stu-id="ee32b-126">Subject</span></span>| <span data-ttu-id="ee32b-127">{Konu}</span><span class="sxs-lookup"><span data-stu-id="ee32b-127">{Subject}</span></span>|<span data-ttu-id="ee32b-128">Bir dize toouniquely hello web üzerinden hello kullanıcı oturum açma tanımlayın</span><span class="sxs-lookup"><span data-stu-id="ee32b-128">A string toouniquely identify hello user logon across hello web</span></span>|
| <span data-ttu-id="ee32b-129">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="ee32b-129">Tenant ID</span></span>| <span data-ttu-id="ee32b-130">{GUID}</span><span class="sxs-lookup"><span data-stu-id="ee32b-130">{Guid}</span></span>| <span data-ttu-id="ee32b-131">A *GUID* toouniquely hello kullanıcının Azure Active Directory kuruluş temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ee32b-131">A *guid* toouniquely represent hello user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="ee32b-132">Ayrıca, kimlik doğrulama isteğine dahil tüm kullanıcı talepleri de dahil olmak üzere bir tablo görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ee32b-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="ee32b-133">Tüm talep bir belirteç kimliği ve açıklama listesi için lütfen bkz [makale](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "listesi, talepleri kimliği belirteci").</span><span class="sxs-lookup"><span data-stu-id="ee32b-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="ee32b-134">Test içeren bir yöntem erişen bir *[Authorize]* özniteliği (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="ee32b-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="ee32b-135">Bu adımda, anonim kullanıcı olarak erişen hello kimliği doğrulanmış denetleyicisi sınayacak:</span><span class="sxs-lookup"><span data-stu-id="ee32b-135">In this step, you will test accessing hello Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="ee32b-136">Merhaba bağlantı toosign kullanıma hello kullanıcı ve tam hello oturum kapatma işlemini seçin.</span><span class="sxs-lookup"><span data-stu-id="ee32b-136">Select hello link toosign-out hello user and complete hello sign-out process.</span></span><br/>
<span data-ttu-id="ee32b-137">Şimdi, tarayıcıda http://localhost yazın: {port} / tooaccess hello ile korunan denetleyicinizi kimliği doğrulanmış `[Authorize]` özniteliği</span><span class="sxs-lookup"><span data-stu-id="ee32b-137">Now in your browser, type http://localhost:{port}/authenticated tooaccess your controller that is protected with hello `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="ee32b-138">Beklenen sonuçları</span><span class="sxs-lookup"><span data-stu-id="ee32b-138">Expected results</span></span>
<span data-ttu-id="ee32b-139">Tooauthenticate toosee hello görünüm gerektiren hello istemi almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee32b-139">You should receive hello prompt requiring you tooauthenticate toosee hello view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="ee32b-140">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="ee32b-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="ee32b-141">Tüm web sitenize koruma</span><span class="sxs-lookup"><span data-stu-id="ee32b-141">Protect your entire web site</span></span>
<span data-ttu-id="ee32b-142">tooprotect tüm web sitenizin hello eklemek `AuthorizeAttribute` çok`GlobalFilters` içinde `Global.asax` `Application_Start` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="ee32b-142">tooprotect your entire web site, add hello `AuthorizeAttribute` too`GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="ee32b-143">**Nasıl tooyour uygulamada yalnızca bir kuruluş toosign toorestrict kullanıcılardan**</span><span class="sxs-lookup"><span data-stu-id="ee32b-143">**How toorestrict users from only one organization toosign in tooyour application**</span></span>

> <span data-ttu-id="ee32b-144">Varsayılan olarak, herhangi bir şirket veya Azure Active Directory ile tümleşik olan kuruluşunuzun iş ve Okul hesaplarını yanı sıra kişisel hesaplar (dahil olmak üzere outlook.com, live.com ve diğerleri) oturum açma tooyour uygulama.</span><span class="sxs-lookup"><span data-stu-id="ee32b-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in tooyour application.</span></span> 

> <span data-ttu-id="ee32b-145">Merhaba, uygulama tooaccept oturum açma işlemleri yalnızca bir Azure Active Directory kuruluştan isterseniz, değiştirmek `Tenant` parametresinde *web.config* gelen `Common` hello kuruluşun – toohello Kiracı adı örnek, *contoso.onmicrosoft.com*. Bundan sonra hello değiştirme `ValidateIssuer` bağımsız değişkeni, *OWIN başlangıç sınıfı* çok`true`.</span><span class="sxs-lookup"><span data-stu-id="ee32b-145">If you want your application tooaccept sign-ins from only one Azure Active Directory organization, replace hello `Tenant` parameter in *web.config* from `Common` toohello tenant name of hello organization – example, *contoso.onmicrosoft.com*. After that, change hello `ValidateIssuer` argument in your *OWIN Startup class* too`true`.</span></span>

> <span data-ttu-id="ee32b-146">yalnızca belirli kuruluşların listesi tooallow kullanıcılardan ayarlamak `ValidateIssuer` tootrue ve kullanım hello `ValidIssuers` parametresi toospecify kuruluşların listesi.</span><span class="sxs-lookup"><span data-stu-id="ee32b-146">tooallow users from only a list of specific organizations, set `ValidateIssuer` tootrue and use hello `ValidIssuers` parameter toospecify a list of organizations.</span></span>

> <span data-ttu-id="ee32b-147">Başka bir seçenek IssuerValidator parametresini kullanarak toovalidate hello verenler tooimplement özel bir yöntem olduğu.</span><span class="sxs-lookup"><span data-stu-id="ee32b-147">Another option is tooimplement a custom method toovalidate hello issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="ee32b-148">Hakkında daha fazla bilgi için `TokenValidationParameters`, lütfen bkz [bu](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "tokenvalidationparameters değerini MSDN makalesine") MSDN makalesi.</span><span class="sxs-lookup"><span data-stu-id="ee32b-148">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

