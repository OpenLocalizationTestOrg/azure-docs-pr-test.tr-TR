---
title: "aaaAzure AD v2 Windows Masaüstü Getting Started - Test | Microsoft Docs"
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
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="d3788-103">Kodunuzu test</span><span class="sxs-lookup"><span data-stu-id="d3788-103">Test your code</span></span>

<span data-ttu-id="d3788-104">İçinde uygulamanızın tuşuna tootest sipariş `F5` toorun projenizi Visual Studio'da.</span><span class="sxs-lookup"><span data-stu-id="d3788-104">In order tootest your application, press `F5` toorun your project in Visual Studio.</span></span> <span data-ttu-id="d3788-105">Ana penceresi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="d3788-105">Your Main Window should appear:</span></span>

![Örnek ekran görüntüsü](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

<span data-ttu-id="d3788-107">Hazır tootest olduğunuzda tıklatın *Microsoft Graph API çağrısı* ve bir Microsoft Azure Active Directory (kuruluş hesabı) veya bir Microsoft Account (live.com, outlook.com) hesap toosign de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d3788-107">When you're ready tootest, click *Call Microsoft Graph API* and use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> <span data-ttu-id="d3788-108">Bu ilk kez hello ise, kullanıcı toosign isteyen bir pencere görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="d3788-108">It it is hello first time, you will see a window asking user toosign in:</span></span>

![oturum açma](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a><span data-ttu-id="d3788-110">Onay</span><span class="sxs-lookup"><span data-stu-id="d3788-110">Consent</span></span>
<span data-ttu-id="d3788-111">Merhaba tooyour uygulamada oturum ilk kez, bir onay ekranı benzer toohello ile aşağıdaki sunulur, ihtiyacınız olduğunda tooexplicitly kabul edin:</span><span class="sxs-lookup"><span data-stu-id="d3788-111">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Onay ekranı](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="d3788-113">Beklenen sonuçları</span><span class="sxs-lookup"><span data-stu-id="d3788-113">Expected results</span></span>
<span data-ttu-id="d3788-114">Kullanıcı profili bilgilerini hello API çağrısı sonuçları ekranda hello Microsoft Graph API çağrısı tarafından döndürülen görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d3788-114">You should see user profile information returned by hello Microsoft Graph API call on hello API Call Results screen.</span></span>

<span data-ttu-id="d3788-115">Merhaba belirteci aracılığıyla edinilen hakkında temel bilgiler görmeniz gerekir `AcquireTokenAsync` veya `AcquireTokenSilentAsync` hello belirteci bilgisi kutusunda:</span><span class="sxs-lookup"><span data-stu-id="d3788-115">You  should also see basic information about hello token acquired via `AcquireTokenAsync` or `AcquireTokenSilentAsync` in hello Token Info box:</span></span>

|<span data-ttu-id="d3788-116">Özellik</span><span class="sxs-lookup"><span data-stu-id="d3788-116">Property</span></span>  |<span data-ttu-id="d3788-117">Biçimi</span><span class="sxs-lookup"><span data-stu-id="d3788-117">Format</span></span>  |<span data-ttu-id="d3788-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d3788-118">Description</span></span> |
|---------|---------|---------|
|<span data-ttu-id="d3788-119">Ad</span><span class="sxs-lookup"><span data-stu-id="d3788-119">Name</span></span> | <span data-ttu-id="d3788-120">{Tam} kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="d3788-120">{User Full name}</span></span> |<span data-ttu-id="d3788-121">Merhaba kullanıcı adı ve Soyadı</span><span class="sxs-lookup"><span data-stu-id="d3788-121">hello user’s first and last name</span></span>|
|<span data-ttu-id="d3788-122">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="d3788-122">Username</span></span> |<span>user@domain.com</span> |<span data-ttu-id="d3788-123">kullanılan tooidentify hello kullanıcı Hello kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="d3788-123">hello username used tooidentify hello user</span></span>|
|<span data-ttu-id="d3788-124">Belirtecinin süresi</span><span class="sxs-lookup"><span data-stu-id="d3788-124">Token Expires</span></span> |<span data-ttu-id="d3788-125">{DateTime}</span><span class="sxs-lookup"><span data-stu-id="d3788-125">{DateTime}</span></span>         |<span data-ttu-id="d3788-126">hangi hello üzerinde belirteci hello ne kadar süre.</span><span class="sxs-lookup"><span data-stu-id="d3788-126">hello time on which hello token expires.</span></span> <span data-ttu-id="d3788-127">MSAL hello sona erme tarihi sizin için hello belirteci gerektiğinde yenileyerek uzatır</span><span class="sxs-lookup"><span data-stu-id="d3788-127">MSAL will extend hello expiration date for you by renewing hello token when necessary</span></span>|
|<span data-ttu-id="d3788-128">erişim belirteci</span><span class="sxs-lookup"><span data-stu-id="d3788-128">Access token</span></span> |<span data-ttu-id="d3788-129">{Dize}</span><span class="sxs-lookup"><span data-stu-id="d3788-129">{String}</span></span>         |<span data-ttu-id="d3788-130">bir yetkilendirme üst bilgisi gerektiren tooHTTP istekleri gönderilecek Hello belirteç dizesini gönderilen</span><span class="sxs-lookup"><span data-stu-id="d3788-130">hello token string sent that will be sent tooHTTP requests that require an authorization header</span></span>|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="d3788-131">Kapsamlar ve temsilci izinleri hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="d3788-131">More information about scopes and delegated permissions</span></span>
<span data-ttu-id="d3788-132">Grafik API'si gerektirir hello `user.read` kapsam tooread kullanıcı profili.</span><span class="sxs-lookup"><span data-stu-id="d3788-132">Graph API requires hello `user.read` scope tooread user profile.</span></span> <span data-ttu-id="d3788-133">Bu kapsam, varsayılan olarak, kayıt portal Kaydedilmekte her uygulama otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="d3788-133">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="d3788-134">Bazı diğer grafik API'leri yanı sıra, arka uç sunucusu için özel API'leri ek kapsamlar gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d3788-134">Some other Graph APIs as well as custom APIs for your backend server require additional scopes.</span></span> <span data-ttu-id="d3788-135">Örneğin, bir grafik `Calendars.Read` gerekli toolist kullanıcının takvimleri değil.</span><span class="sxs-lookup"><span data-stu-id="d3788-135">For example, for Graph, `Calendars.Read` is required toolist user’s calendars.</span></span> <span data-ttu-id="d3788-136">Sırada bir uygulama bağlamında kullanıcının Takvim tooaccess Merhaba, tooadd gerek `Calendars.Read` uygulama kaydı'nın bilgi temsilci ve ardından ekleyin `Calendars.Read` toohello `AcquireTokenAsync` çağırın.</span><span class="sxs-lookup"><span data-stu-id="d3788-136">In order tooaccess hello user’s calendar in a context of an application, you need tooadd `Calendars.Read` delegated application registration’s information and then add `Calendars.Read` toohello `AcquireTokenAsync` call.</span></span> <span data-ttu-id="d3788-137">Kapsam hello sayısı arttıkça, kullanıcı için ek onayları istenebilir.</span><span class="sxs-lookup"><span data-stu-id="d3788-137">User may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



