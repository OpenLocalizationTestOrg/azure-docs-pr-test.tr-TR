---
title: aaaAzure AD v2 Android Getting Started - Test | Microsoft Docs
description: "Nasıl bir Android uygulaması bir erişim belirteci alın ve Microsoft Graph API veya Azure Active Directory v2 uç noktasından erişim belirteçleri gerektiren API'larını çağırma"
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="fa2b0-103">Kodunuzu test</span><span class="sxs-lookup"><span data-stu-id="fa2b0-103">Test your code</span></span>

1. <span data-ttu-id="fa2b0-104">Kod tooyour Aygıt/Öykünücüsü dağıtın.</span><span class="sxs-lookup"><span data-stu-id="fa2b0-104">Deploy your code tooyour device/emulator.</span></span>
2. <span data-ttu-id="fa2b0-105">Tootest hazır olduğunuzda, bir Microsoft Azure Active Directory (kuruluş hesabı) veya bir Microsoft Account (live.com, outlook.com) hesabı toosign içinde kullanın.</span><span class="sxs-lookup"><span data-stu-id="fa2b0-105">When you're ready tootest, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account toosign in.</span></span> 

<span data-ttu-id="fa2b0-106">![Örnek ekran görüntüsü](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="fa2b0-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="fa2b0-107">
![Oturum açma](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="fa2b0-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="fa2b0-108">Onay</span><span class="sxs-lookup"><span data-stu-id="fa2b0-108">Consent</span></span>
<span data-ttu-id="fa2b0-109">Merhaba tooyour uygulamada bir kullanıcı oturum açtığında ilk kez bunlar bir onay ekranı benzer toohello ile aşağıdaki sunulur, gereksinim duydukları burada tooexplicitly kabul edin:</span><span class="sxs-lookup"><span data-stu-id="fa2b0-109">hello first time a user signs in tooyour application, they will be presented with a consent screen similar toohello below, where they need tooexplicitly accept:</span></span> 

![Onay](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="fa2b0-111">Beklenen sonuçları</span><span class="sxs-lookup"><span data-stu-id="fa2b0-111">Expected results</span></span>
<span data-ttu-id="fa2b0-112">'Me' hello çağrısı tooMicrosoft grafik API'si sonuçlarını görmeniz gerekir uç nokta kullanılan tootooobtain hello kullanıcı profili - https://graph.microsoft.com/v1.0/me.</span><span class="sxs-lookup"><span data-stu-id="fa2b0-112">You should see hello results of a call tooMicrosoft Graph API ‘me’ endpoint used tootooobtain hello user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="fa2b0-113">Genel Microsoft Graph uç noktaları listesi için lütfen bu bakın [makale](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="fa2b0-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="fa2b0-114">Kapsamlar ve temsilci izinleri hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="fa2b0-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="fa2b0-115">Merhaba Microsoft Graph API gerektirir hello `user.read` tooread hello kullanıcının profilini kapsam.</span><span class="sxs-lookup"><span data-stu-id="fa2b0-115">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="fa2b0-116">Bu kapsam, varsayılan olarak, kayıt portal Kaydedilmekte her uygulama otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="fa2b0-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="fa2b0-117">Microsoft Graph için diğer bazı API'leri ve aynı zamanda, arka uç sunucusu için özel API'leri ek kapsamlar gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="fa2b0-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="fa2b0-118">Örneğin, Microsoft Graph için kapsam hello `Calendars.Read` gerekli toolist hello kullanıcının takvimleri değil.</span><span class="sxs-lookup"><span data-stu-id="fa2b0-118">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="fa2b0-119">Sırada bir uygulama bağlamında kullanıcının Takvim tooaccess Merhaba, tooadd hello gerek `Calendars.Read` izin toohello uygulama kayıt ait bilgileri temsilcisi ve hello ekleyin `Calendars.Read` kapsam toohello `acquireTokenSilentAsync` çağırın.</span><span class="sxs-lookup"><span data-stu-id="fa2b0-119">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="fa2b0-120">Kapsam hello sayısı arttıkça hello kullanıcı için ek onayları istenebilir.</span><span class="sxs-lookup"><span data-stu-id="fa2b0-120">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->
