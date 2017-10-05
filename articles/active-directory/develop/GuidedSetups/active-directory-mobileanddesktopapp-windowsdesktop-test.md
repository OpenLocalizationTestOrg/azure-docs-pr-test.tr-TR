---
title: "Azure AD v2 Windows Masaüstü tıklatmalarını başlatıldı - Test | Microsoft Docs"
description: "Windows Masaüstü .NET (XAML) uygulamaları, Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
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
ms.openlocfilehash: 972cc48057c13271d725b0c973c3ccf651ad27c4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="4d8b3-103">Kodunuzu test</span><span class="sxs-lookup"><span data-stu-id="4d8b3-103">Test your code</span></span>

<span data-ttu-id="4d8b3-104">Uygulamanızı test etmek için basın `F5` Visual Studio'da projeyi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4d8b3-104">In order to test your application, press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="4d8b3-105">Ana penceresi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="4d8b3-105">Your Main Window should appear:</span></span>

![Örnek ekran görüntüsü](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="4d8b3-107">Test etmek hazır olduğunuzda, tıklatın *Microsoft Graph API çağrısı* ve oturum açmak için bir Microsoft Azure Active Directory (kuruluş hesabı) veya bir Microsoft Account (live.com, outlook.com) hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d8b3-107">When you're ready to test, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> <span data-ttu-id="4d8b3-108">Bu ilk kez, oturum açmak için kullanıcı isteyen bir pencere görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="4d8b3-108">It it is the first time, you will see a window asking user to sign in:</span></span>

![oturum açma](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="4d8b3-110">Onay</span><span class="sxs-lookup"><span data-stu-id="4d8b3-110">Consent</span></span>
<span data-ttu-id="4d8b3-111">İlk kez oturum açtığınızda, uygulamanıza, benzer bir onay ekranı sunulur Aşağıda, burada açıkça kabul etmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d8b3-111">The first time you sign in to your application, you will be presented with a consent screen similar to the below, where you need to explicitly accept:</span></span>

![Onay ekranı](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="4d8b3-113">Beklenen sonuçları</span><span class="sxs-lookup"><span data-stu-id="4d8b3-113">Expected results</span></span>
<span data-ttu-id="4d8b3-114">Kullanıcı profili bilgilerini API çağrısı sonuçları ekranda Microsoft Graph API çağrısı tarafından döndürülen görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d8b3-114">You should see user profile information returned by the Microsoft Graph API call on the API Call Results screen.</span></span>

<span data-ttu-id="4d8b3-115">Aracılığıyla edinilen belirteci hakkında temel bilgiler görmeniz gerekir `AcquireTokenAsync` veya `AcquireTokenSilentAsync` belirteci bilgisi kutusunda:</span><span class="sxs-lookup"><span data-stu-id="4d8b3-115">You  should also see basic information about the token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in the Token Info box:</span></span>

|<span data-ttu-id="4d8b3-116">Özellik</span><span class="sxs-lookup"><span data-stu-id="4d8b3-116">Property</span></span>  |<span data-ttu-id="4d8b3-117">Biçimi</span><span class="sxs-lookup"><span data-stu-id="4d8b3-117">Format</span></span>  |<span data-ttu-id="4d8b3-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4d8b3-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="4d8b3-119">Ad</span><span class="sxs-lookup"><span data-stu-id="4d8b3-119">Name</span></span> | <span data-ttu-id="4d8b3-120">{Tam} kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="4d8b3-120">{User Full name}</span></span> |<span data-ttu-id="4d8b3-121">Kullanıcı adı ve Soyadı</span><span class="sxs-lookup"><span data-stu-id="4d8b3-121">The user’s first and last name</span></span>|
|<span data-ttu-id="4d8b3-122">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="4d8b3-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="4d8b3-123">Kullanıcıyı tanımlamak için kullanılan kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="4d8b3-123">The username used to identify the user</span></span>|
|<span data-ttu-id="4d8b3-124">Belirtecinin süresi</span><span class="sxs-lookup"><span data-stu-id="4d8b3-124">Token Expires</span></span> |<span data-ttu-id="4d8b3-125">{DateTime}</span><span class="sxs-lookup"><span data-stu-id="4d8b3-125">{DateTime}</span></span>         |<span data-ttu-id="4d8b3-126">Üzerinde belirtecin süresinin dolduğu zaman.</span><span class="sxs-lookup"><span data-stu-id="4d8b3-126">The time on which the token expires.</span></span> <span data-ttu-id="4d8b3-127">MSAL sona erme tarihini sizin için gerekli olduğunda belirteci yenileyerek uzatır</span><span class="sxs-lookup"><span data-stu-id="4d8b3-127">MSAL will extend the expiration date for you by renewing the token when necessary</span></span>|
|<span data-ttu-id="4d8b3-128">erişim belirteci</span><span class="sxs-lookup"><span data-stu-id="4d8b3-128">Access token</span></span> |<span data-ttu-id="4d8b3-129">{Dize}</span><span class="sxs-lookup"><span data-stu-id="4d8b3-129">{String}</span></span>         |<span data-ttu-id="4d8b3-130">Belirteç dizesini bir authorization üstbilgisi gerektiren HTTP isteklerini gönderilecek gönderilen</span><span class="sxs-lookup"><span data-stu-id="4d8b3-130">The token string sent that will be sent to HTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="4d8b3-131">Kapsamlar ve temsilci izinleri hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="4d8b3-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="4d8b3-132">Grafik API'si gerektirir `user.read` kullanıcı profilini okuma için kapsamı.</span><span class="sxs-lookup"><span data-stu-id="4d8b3-132">Graph API requires the `user.read` scope to read user profile.</span></span> <span data-ttu-id="4d8b3-133">Bu kapsam, varsayılan olarak, kayıt portal Kaydedilmekte her uygulama otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="4d8b3-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="4d8b3-134">Bazı diğer grafik API'leri yanı sıra, arka uç sunucusu için özel API'leri ek kapsamlar gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4d8b3-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="4d8b3-135">Örneğin, bir grafik `Calendars.Read` liste kullanıcının takvimleri için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4d8b3-135">For example, for Graph, `Calendars.Read` is required to list user’s calendars.</span></span> <span data-ttu-id="4d8b3-136">Kullanıcının Takvim bir uygulama bağlamında erişmek için eklemeniz gerekir `Calendars.Read` uygulama kaydı'nın bilgi temsilci ve ardından ekleyin `Calendars.Read` için `AcquireTokenAsync` çağırın.</span><span class="sxs-lookup"><span data-stu-id="4d8b3-136">In order to access the user’s calendar in a context of an application, you need to add `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` to the `AcquireTokenAsync` call.</span></span> <span data-ttu-id="4d8b3-137">Kapsam sayısı arttıkça, kullanıcı için ek onayları istenebilir.</span><span class="sxs-lookup"><span data-stu-id="4d8b3-137">User may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->



