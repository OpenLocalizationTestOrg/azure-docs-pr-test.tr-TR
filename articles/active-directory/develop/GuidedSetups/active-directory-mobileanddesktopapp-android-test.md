---
title: "Azure AD v2 Android alma başlatıldı - Test | Microsoft Docs"
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
ms.openlocfilehash: 6df64f4820f8409bd8897d5ac24f81bffeeef102
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
## <a name="test-your-code"></a><span data-ttu-id="4e174-103">Kodunuzu test</span><span class="sxs-lookup"><span data-stu-id="4e174-103">Test your code</span></span>

1. <span data-ttu-id="4e174-104">Kodunuzu Aygıt/Öykünücüsü için dağıtın.</span><span class="sxs-lookup"><span data-stu-id="4e174-104">Deploy your code to your device/emulator.</span></span>
2. <span data-ttu-id="4e174-105">Test etmek hazır olduğunuzda, oturum açmak için bir Microsoft Azure Active Directory (kuruluş hesabı) veya bir Microsoft Account (live.com, outlook.com) hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e174-105">When you're ready to test, use a Microsoft Azure Active Directory (organizational account) or a Microsoft Account (live.com, outlook.com) account to sign in.</span></span> 

<span data-ttu-id="4e174-106">![Örnek ekran görüntüsü](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span><span class="sxs-lookup"><span data-stu-id="4e174-106">![Sample screen shot](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
</span></span><br/><br/><span data-ttu-id="4e174-107">
![Oturum açma](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span><span class="sxs-lookup"><span data-stu-id="4e174-107">
![Sign-in](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)</span></span>

### <a name="consent"></a><span data-ttu-id="4e174-108">Onay</span><span class="sxs-lookup"><span data-stu-id="4e174-108">Consent</span></span>
<span data-ttu-id="4e174-109">Bir kullanıcı oturum açtığında, uygulama için ilk kez bunlar benzer bir onay ekranı sunulur aşağıda açıkça kabul etmek gereken yeri:</span><span class="sxs-lookup"><span data-stu-id="4e174-109">The first time a user signs in to your application, they will be presented with a consent screen similar to the below, where they need to explicitly accept:</span></span> 

![Onay](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a><span data-ttu-id="4e174-111">Beklenen sonuçları</span><span class="sxs-lookup"><span data-stu-id="4e174-111">Expected results</span></span>
<span data-ttu-id="4e174-112">Microsoft Graph API çağrısının sonuçlarını 'me' görmelisiniz uç noktası için kullanıcı profili - https://graph.microsoft.com/v1.0/me elde etmek üzere kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4e174-112">You should see the results of a call to Microsoft Graph API ‘me’ endpoint used to to obtain the user profile - https://graph.microsoft.com/v1.0/me.</span></span> <span data-ttu-id="4e174-113">Genel Microsoft Graph uç noktaları listesi için lütfen bu bakın [makale](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span><span class="sxs-lookup"><span data-stu-id="4e174-113">For a list of common Microsoft Graph endpoints, please see this [article](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="4e174-114">Kapsamlar ve temsilci izinleri hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="4e174-114">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="4e174-115">Microsoft Graph API gerektiriyor `user.read` kullanıcının profilini okumak için kapsam.</span><span class="sxs-lookup"><span data-stu-id="4e174-115">The Microsoft Graph API requires the `user.read` scope to read the user's profile.</span></span> <span data-ttu-id="4e174-116">Bu kapsam, varsayılan olarak, kayıt portal Kaydedilmekte her uygulama otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="4e174-116">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="4e174-117">Microsoft Graph için diğer bazı API'leri ve aynı zamanda, arka uç sunucusu için özel API'leri ek kapsamlar gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="4e174-117">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="4e174-118">Örneğin, Microsoft Graph, kapsam `Calendars.Read` kullanıcının takvimleri listelemek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4e174-118">For example, for Microsoft Graph, the scope `Calendars.Read` is required to list the user’s calendars.</span></span> <span data-ttu-id="4e174-119">Kullanıcının Takvim bir uygulama bağlamında erişmek için eklemeniz gerekir `Calendars.Read` izin uygulama kayıt ait bilgileri için temsilci ve ardından ekleyin `Calendars.Read` için kapsam `acquireTokenSilentAsync` çağırın.</span><span class="sxs-lookup"><span data-stu-id="4e174-119">In order to access the user’s calendar in a context of an application, you need to add the `Calendars.Read` delegated permission to the application registration’s information and then add the `Calendars.Read` scope to the `acquireTokenSilentAsync` call.</span></span> <span data-ttu-id="4e174-120">Kapsam sayısı arttıkça, kullanıcı için ek onayları istenebilir.</span><span class="sxs-lookup"><span data-stu-id="4e174-120">The user may be prompted for additional consents as you increase the number of scopes.</span></span>

<!--end-collapse-->
