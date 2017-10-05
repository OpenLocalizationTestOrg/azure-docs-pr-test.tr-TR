---
title: "Azure AD v2 ASP.NET Web sunucusu alma başlatıldı - Test | Microsoft Docs"
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
ms.openlocfilehash: 00cb963e85111274c36c3a84489894811ad2dabd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="5a4c7-103">Kodunuzu test</span><span class="sxs-lookup"><span data-stu-id="5a4c7-103">Test your code</span></span>

<span data-ttu-id="5a4c7-104">Tuşuna `F5` Visual Studio'da projeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-104">Press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="5a4c7-105">Tarayıcı açılır ve sizden *http://localhost: {port}* burada göreceksiniz *oturum Microsoft oturum* düğmesi.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-105">The browser will open and direct you to *http://localhost:{port}* where you’ll see the *Sign in with Microsoft* button.</span></span> <span data-ttu-id="5a4c7-106">Bir tane oturum açmak için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-106">Go ahead and click it to sign in.</span></span>

<span data-ttu-id="5a4c7-107">Test etmek hazır olduğunuzda, oturum açmak için bir iş, okul (Azure Active Directory) veya kişisel (live.com, outlook.com) hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-107">When you're ready to test, use a work or school (Azure Active Directory), or a personal (live.com, outlook.com) account to sign in.</span></span> 

![Microsoft tarayıcı penceresi ile oturum aç](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Microsoft tarayıcı penceresi ile oturum aç](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="5a4c7-110">Beklenen sonuçları</span><span class="sxs-lookup"><span data-stu-id="5a4c7-110">Expected results</span></span>
<span data-ttu-id="5a4c7-111">Oturum açma işleminden sonra kullanıcı uygulama kayıt bilgilerinizi Microsoft uygulama kayıt Portalı'nda belirtilen HTTPS URL'si olan web sitesinin giriş sayfasına yeniden yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-111">After sign-in, the user is redirected to the home page of your web site which is the HTTPS URL specified in your application registration information in the Microsoft Application Registration Portal.</span></span> <span data-ttu-id="5a4c7-112">Bu sayfayı artık gösterir *Hello {User}* ve bir bağlantı oturum kapatma ve Yetkilendir denetleyicisinin bağlantısını olan kullanıcı taleplerini görmek için bir bağlantıyı oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-112">This page now shows *Hello {User}* and a link to sign-out, and a link to see the user’s claims – which is a link to the Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="5a4c7-113">Kullanıcının talepleri bakın</span><span class="sxs-lookup"><span data-stu-id="5a4c7-113">See user's claims</span></span>
<span data-ttu-id="5a4c7-114">Kullanıcının talepleri görmek için köprü seçin.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-114">Select the hyperlink to see the user's claims.</span></span> <span data-ttu-id="5a4c7-115">Bu, yalnızca kimliği doğrulanan kullanıcılar tarafından kullanılabilir görünüm ve denetleyici için yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-115">This leads you to the controller and view that is only available to users that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="5a4c7-116">Beklenen sonuçları</span><span class="sxs-lookup"><span data-stu-id="5a4c7-116">Expected results</span></span>
 <span data-ttu-id="5a4c7-117">Oturum açmış olan kullanıcının temel özelliklerini içeren bir tablo görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="5a4c7-117">You should see a table containing the basic properties of the logged user:</span></span>

| <span data-ttu-id="5a4c7-118">Özellik</span><span class="sxs-lookup"><span data-stu-id="5a4c7-118">Property</span></span> | <span data-ttu-id="5a4c7-119">Değer</span><span class="sxs-lookup"><span data-stu-id="5a4c7-119">Value</span></span> | <span data-ttu-id="5a4c7-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5a4c7-120">Description</span></span>|
|---|---|---|
| <span data-ttu-id="5a4c7-121">Ad</span><span class="sxs-lookup"><span data-stu-id="5a4c7-121">Name</span></span> | <span data-ttu-id="5a4c7-122">{Tam} kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="5a4c7-122">{User Full Name}</span></span> | <span data-ttu-id="5a4c7-123">Kullanıcı adı ve Soyadı</span><span class="sxs-lookup"><span data-stu-id="5a4c7-123">The user’s first and last name</span></span>
|<span data-ttu-id="5a4c7-124">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="5a4c7-124">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="5a4c7-125">Oturum açmış kullanıcıyı tanımlamak için kullanılan kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="5a4c7-125">The username used to identify the logged user</span></span>
| <span data-ttu-id="5a4c7-126">Konu</span><span class="sxs-lookup"><span data-stu-id="5a4c7-126">Subject</span></span>| <span data-ttu-id="5a4c7-127">{Konu}</span><span class="sxs-lookup"><span data-stu-id="5a4c7-127">{Subject}</span></span>|<span data-ttu-id="5a4c7-128">Kullanıcı oturum açma web üzerinden benzersiz şekilde tanımlamak için bir dize</span><span class="sxs-lookup"><span data-stu-id="5a4c7-128">A string to uniquely identify the user logon across the web</span></span>|
| <span data-ttu-id="5a4c7-129">Kiracı Kimliği</span><span class="sxs-lookup"><span data-stu-id="5a4c7-129">Tenant ID</span></span>| <span data-ttu-id="5a4c7-130">{GUID}</span><span class="sxs-lookup"><span data-stu-id="5a4c7-130">{Guid}</span></span>| <span data-ttu-id="5a4c7-131">A *GUID* kullanıcının Azure Active Directory kuruluş benzersiz olarak gösterecek.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-131">A *guid* to uniquely represent the user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="5a4c7-132">Ayrıca, kimlik doğrulama isteğine dahil tüm kullanıcı talepleri de dahil olmak üzere bir tablo görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-132">In addition, you will see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="5a4c7-133">Tüm talep bir belirteç kimliği ve açıklama listesi için lütfen bkz [makale](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "listesi, talepleri kimliği belirteci").</span><span class="sxs-lookup"><span data-stu-id="5a4c7-133">For a list of all claims in an Id Token and explanation please see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in Id Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="5a4c7-134">Test içeren bir yöntem erişen bir *[Authorize]* özniteliği (isteğe bağlı)</span><span class="sxs-lookup"><span data-stu-id="5a4c7-134">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="5a4c7-135">Bu adımda, bir anonim kullanıcı olarak kimlik doğrulaması yapılmış denetleyicisi erişimi test:</span><span class="sxs-lookup"><span data-stu-id="5a4c7-135">In this step, you will test accessing the Authenticated controller as an anonymous user:</span></span><br/>
<span data-ttu-id="5a4c7-136">Kullanıcı oturum kapatma bağlantısını seçin ve oturum kapatma işlemini tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-136">Select the link to sign-out the user and complete the sign-out process.</span></span><br/>
<span data-ttu-id="5a4c7-137">Şimdi, tarayıcıda http://localhost yazın: {port} / ile korunan denetleyicinizi erişmek için kimliği doğrulanmış `[Authorize]` özniteliği</span><span class="sxs-lookup"><span data-stu-id="5a4c7-137">Now in your browser, type http://localhost:{port}/authenticated to access your controller that is protected with the `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="5a4c7-138">Beklenen sonuçları</span><span class="sxs-lookup"><span data-stu-id="5a4c7-138">Expected results</span></span>
<span data-ttu-id="5a4c7-139">Görmek için kimlik doğrulaması gerektirmek istemi almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-139">You should receive the prompt requiring you to authenticate to see the view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="5a4c7-140">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="5a4c7-140">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="5a4c7-141">Tüm web sitenize koruma</span><span class="sxs-lookup"><span data-stu-id="5a4c7-141">Protect your entire web site</span></span>
<span data-ttu-id="5a4c7-142">Tüm web sitenize korumak için add `AuthorizeAttribute` için `GlobalFilters` içinde `Global.asax` `Application_Start` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="5a4c7-142">To protect your entire web site, add the `AuthorizeAttribute` to `GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> <span data-ttu-id="5a4c7-143">**Kullanıcılar uygulamanıza oturum açmak için yalnızca bir kuruluştan kısıtlama**</span><span class="sxs-lookup"><span data-stu-id="5a4c7-143">**How to restrict users from only one organization to sign in to your application**</span></span>

> <span data-ttu-id="5a4c7-144">Varsayılan olarak, kişisel (outlook.com, live.com ve diğerleri dahil) hesaplarının yanı sıra iş ve Okul hesapları herhangi bir şirket veya Azure Active Directory ile tümleşik olan Kuruluş oturum uygulamanıza bileşenini.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-144">By default, personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory can sign-in to your application.</span></span> 

> <span data-ttu-id="5a4c7-145">Oturum açma işlemleri yalnızca bir Azure Active Directory kuruluştan kabul etmek için uygulamanızın isterseniz Değiştir `Tenant` parametresinde *web.config* gelen `Common` kuruluşun – Kiracı adı için örnek, *contoso.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-145">If you want your application to accept sign-ins from only one Azure Active Directory organization, replace the `Tenant` parameter in *web.config* from `Common` to the tenant name of the organization – example, *contoso.onmicrosoft.com*.</span></span> <span data-ttu-id="5a4c7-146">Bundan sonra değiştirmek `ValidateIssuer` bağımsız değişkeni, *OWIN başlangıç sınıfı* için `true`.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-146">After that, change the `ValidateIssuer` argument in your *OWIN Startup class* to `true`.</span></span>

> <span data-ttu-id="5a4c7-147">Yalnızca belirli kuruluşların listesi kullanıcılardan izin verecek şekilde ayarlamanız `ValidateIssuer` true ve kullanmak için `ValidIssuers` kuruluşların listesini belirtmek için parametre.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-147">To allow users from only a list of specific organizations, set `ValidateIssuer` to true and use the `ValidIssuers` parameter to specify a list of organizations.</span></span>

> <span data-ttu-id="5a4c7-148">Başka bir seçenek IssuerValidator parametresini kullanarak verenler doğrulamak için özel bir yöntem uygulamaktır.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-148">Another option is to implement a custom method to validate the issuers using IssuerValidator parameter.</span></span> <span data-ttu-id="5a4c7-149">Hakkında daha fazla bilgi için `TokenValidationParameters`, lütfen bkz [bu](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "tokenvalidationparameters değerini MSDN makalesine") MSDN makalesi.</span><span class="sxs-lookup"><span data-stu-id="5a4c7-149">For more information about `TokenValidationParameters`, please see [this](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article") MSDN article.</span></span>

