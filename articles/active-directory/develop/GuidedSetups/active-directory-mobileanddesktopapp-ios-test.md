---
title: "aaaAzure AD v2 iOS Başlarken - Test | Microsoft Docs"
description: "İOS (Swift) uygulamaları, Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a><span data-ttu-id="1aa80-103">Test iOS uygulamanızdan Microsoft Graph API Hello sorgulama</span><span class="sxs-lookup"><span data-stu-id="1aa80-103">Test querying hello Microsoft Graph API from your iOS application</span></span>

<span data-ttu-id="1aa80-104">Tuşuna `Command`  +  `R` toorun hello hello simulator kodda.</span><span class="sxs-lookup"><span data-stu-id="1aa80-104">Press `Command` + `R` toorun hello code in hello simulator.</span></span>

![Örnek ekran görüntüsü](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

<span data-ttu-id="1aa80-106">Tootest hazır olduğunuzda, dokunun *'Microsoft Graph API çağrısı'* ve kullanıcı adı ve parola istendiğinde tootype olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1aa80-106">When you're ready tootest, tap *‘Call Microsoft Graph API’* and you will be prompted tootype your username and password.</span></span>

### <a name="consent"></a><span data-ttu-id="1aa80-107">Onay</span><span class="sxs-lookup"><span data-stu-id="1aa80-107">Consent</span></span>
<span data-ttu-id="1aa80-108">Merhaba tooyour uygulamada oturum ilk kez, bir onay ekranı benzer toohello ile aşağıdaki sunulur, ihtiyacınız olduğunda tooexplicitly kabul edin:</span><span class="sxs-lookup"><span data-stu-id="1aa80-108">hello first time you sign in tooyour application, you will be presented with a consent screen similar toohello below, where you need tooexplicitly accept:</span></span>

![Onay ekranı](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a><span data-ttu-id="1aa80-110">Beklenen sonuçları</span><span class="sxs-lookup"><span data-stu-id="1aa80-110">Expected results</span></span>
<span data-ttu-id="1aa80-111">Kullanıcı profili bilgilerini hello hello Microsoft Graph API çağrısında tarafından döndürülen görmelisiniz *günlüğü* bölümü.</span><span class="sxs-lookup"><span data-stu-id="1aa80-111">You should see user profile information returned by hello Microsoft Graph API call in hello *Logging* section.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="1aa80-112">Kapsamlar ve temsilci izinleri hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="1aa80-112">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="1aa80-113">Merhaba Microsoft Graph API gerektirir hello `user.read` tooread hello kullanıcının profilini kapsam.</span><span class="sxs-lookup"><span data-stu-id="1aa80-113">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="1aa80-114">Bu kapsam, varsayılan olarak, kayıt portal Kaydedilmekte her uygulama otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="1aa80-114">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="1aa80-115">Microsoft Graph için diğer bazı API'leri ve aynı zamanda, arka uç sunucusu için özel API'leri ek kapsamlar gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="1aa80-115">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="1aa80-116">Örneğin, Microsoft Graph için kapsam hello `Calendars.Read` gerekli toolist hello kullanıcının takvimleri değil.</span><span class="sxs-lookup"><span data-stu-id="1aa80-116">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="1aa80-117">Sırada bir uygulama bağlamında kullanıcının Takvim tooaccess Merhaba, tooadd hello gerek `Calendars.Read` izin toohello uygulama kayıt ait bilgileri temsilcisi ve hello ekleyin `Calendars.Read` kapsam toohello `acquireTokenSilent` çağırın.</span><span class="sxs-lookup"><span data-stu-id="1aa80-117">In order tooaccess hello user’s calendar in a context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="1aa80-118">Kapsam hello sayısı arttıkça hello kullanıcı için ek onayları istenebilir.</span><span class="sxs-lookup"><span data-stu-id="1aa80-118">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<!--end-collapse-->



