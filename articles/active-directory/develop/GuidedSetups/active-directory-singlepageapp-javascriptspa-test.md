---
title: aaaAzure AD v2 JS SPA destekli Kurulumu - Test | Microsoft Docs
description: "JavaScript SPA uygulamaları Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a><span data-ttu-id="a727c-103">Kodunuzu test</span><span class="sxs-lookup"><span data-stu-id="a727c-103">Test your code</span></span>

> ### <a name="testing-with-visual-studio"></a><span data-ttu-id="a727c-104">Visual Studio ile test etme</span><span class="sxs-lookup"><span data-stu-id="a727c-104">Testing with Visual Studio</span></span>
> <span data-ttu-id="a727c-105">Visual Studio kullanıyorsanız, basın `F5` toorun projenizi: hello tarayıcı açılır ve çok yönlendirir*http://localhost: {port}* hello gördüğünüz *Microsoft Graph API çağrısı* düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a727c-105">If you are using Visual Studio, press `F5` toorun your project: hello browser opens and directs you too*http://localhost:{port}* where you see hello *Call Microsoft Graph API* button.</span></span>

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a><span data-ttu-id="a727c-106">Python veya başka bir web sunucusu ile test etme</span><span class="sxs-lookup"><span data-stu-id="a727c-106">Testing with Python or another web server</span></span>
> <span data-ttu-id="a727c-107">Visual Studio kullanmıyorsanız, web sunucunuz başlatılır ve yapılandırıldığından emin olun toolisten tooa TCP bağlantı noktası tabanlı hello içeren klasör, *index.html* dosya.</span><span class="sxs-lookup"><span data-stu-id="a727c-107">If you are not using Visual Studio, make sure your web server is started and it is configured toolisten tooa TCP port based on hello folder containing your *index.html* file.</span></span> <span data-ttu-id="a727c-108">Python için dinleme başlatabilirsiniz çalıştırarak toohello bağlantı noktası hello hello uygulamanın klasöründen hello komut istemi / terminal, içinde:</span><span class="sxs-lookup"><span data-stu-id="a727c-108">For Python, you can start listening toohello port by running hello in hello command prompt/ terminal, from hello app's folder:</span></span>
> 
> ```bash
> python -m http.server 8080
> ```
>  <span data-ttu-id="a727c-109">Ardından, hello tarayıcı açıp *http://localhost: 8080* veya *http://localhost: {port}* - hello burada *bağlantı noktası* web sunucunuz toohello bağlantı noktası karşılık gelen dinleme.</span><span class="sxs-lookup"><span data-stu-id="a727c-109">Then, open hello browser and type *http://localhost:8080* or *http://localhost:{port}* - where hello *port* corresponds toohello port that your web server is listening to.</span></span> <span data-ttu-id="a727c-110">İndex.html sayfanızı hello ile Merhaba içeriğine görmelisiniz *Microsoft Graph API çağrısı* düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a727c-110">You should see hello contents of your index.html page with hello *Call Microsoft Graph API* button.</span></span>

## <a name="test-your-application"></a><span data-ttu-id="a727c-111">Uygulamanızı test edin</span><span class="sxs-lookup"><span data-stu-id="a727c-111">Test your application</span></span>

<span data-ttu-id="a727c-112">Sonra Hello tarayıcı yükler, *index.html*, hello tıklatın *Microsoft Graph API çağrısı* düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a727c-112">After hello browser loads your *index.html*, click hello *Call Microsoft Graph API* button.</span></span> <span data-ttu-id="a727c-113">Bu hello ilk kez kullanıyorsanız, hello tarayıcı yeniden yönlendirmeleri olduğunuz, toohello Microsoft Azure Active Directory v2 uç noktası, toosign içinde istenir.</span><span class="sxs-lookup"><span data-stu-id="a727c-113">If this is hello first time, hello browser redirects you toohello Microsoft Azure Active Directory v2 endpoint, where you are  prompted toosign in.</span></span>
 
![Örnek ekran görüntüsü](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a><span data-ttu-id="a727c-115">Onay</span><span class="sxs-lookup"><span data-stu-id="a727c-115">Consent</span></span>
<span data-ttu-id="a727c-116">Merhaba tooyour uygulamada oturum çok ilk kez, bir onay ekranı benzer toohello aşağıdakileri ile tooaccept ihtiyaç duyacağınız sunulur:</span><span class="sxs-lookup"><span data-stu-id="a727c-116">hello very first time you sign in tooyour application, you are presented with a consent screen similar toohello following, where you need tooaccept:</span></span>

 ![Onay ekranı](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a><span data-ttu-id="a727c-118">Beklenen sonuçları</span><span class="sxs-lookup"><span data-stu-id="a727c-118">Expected results</span></span>
<span data-ttu-id="a727c-119">Kullanıcı profili bilgilerini Microsoft Graph API çağrısı yanıt hello tarafından döndürülen görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a727c-119">You should see user profile information returned by hello Microsoft Graph API call response.</span></span>
 
 ![Sonuçlar](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

<span data-ttu-id="a727c-121">Hello edinilen hello belirteci hakkındaki temel bilgileri de görebilirsiniz *erişim belirteci* ve *belirteç talep kimliği* kutuları.</span><span class="sxs-lookup"><span data-stu-id="a727c-121">You also see basic information about hello token acquired in hello *Access Token* and *ID Token Claims* boxes.</span></span>

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a><span data-ttu-id="a727c-122">Kapsamlar ve temsilci izinleri hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="a727c-122">More information about scopes and delegated permissions</span></span>

<span data-ttu-id="a727c-123">Merhaba Microsoft Graph API gerektirir hello `user.read` tooread hello kullanıcının profilini kapsam.</span><span class="sxs-lookup"><span data-stu-id="a727c-123">hello Microsoft Graph API requires hello `user.read` scope tooread hello user's profile.</span></span> <span data-ttu-id="a727c-124">Bu kapsam, varsayılan olarak, kayıt portal Kaydedilmekte her uygulama otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="a727c-124">This scope is automatically added by default in every application being registered on our registration portal.</span></span> <span data-ttu-id="a727c-125">Microsoft Graph için diğer bazı API'leri ve aynı zamanda, arka uç sunucusu için özel API'leri ek kapsamlar gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="a727c-125">Some other APIs for Microsoft Graph as well as custom APIs for your backend server may require additional scopes.</span></span> <span data-ttu-id="a727c-126">Örneğin, Microsoft Graph için kapsam hello `Calendars.Read` gerekli toolist hello kullanıcının takvimleri değil.</span><span class="sxs-lookup"><span data-stu-id="a727c-126">For example, for Microsoft Graph, hello scope `Calendars.Read` is required toolist hello user’s calendars.</span></span> <span data-ttu-id="a727c-127">Sırada bir uygulama hello bağlamında kullanıcının Takvim tooaccess Merhaba, tooadd hello gerek `Calendars.Read` izin toohello uygulama kayıt ait bilgileri temsilcisi ve hello ekleyin `Calendars.Read` kapsam toohello `acquireTokenSilent` çağırın.</span><span class="sxs-lookup"><span data-stu-id="a727c-127">In order tooaccess hello user’s calendar in hello context of an application, you need tooadd hello `Calendars.Read` delegated permission toohello application registration’s information and then add hello `Calendars.Read` scope toohello `acquireTokenSilent` call.</span></span> <span data-ttu-id="a727c-128">Kapsam hello sayısı arttıkça hello kullanıcı için ek onayları istenebilir.</span><span class="sxs-lookup"><span data-stu-id="a727c-128">hello user may be prompted for additional consents as you increase hello number of scopes.</span></span>

<span data-ttu-id="a727c-129">Arka uç API'si (önerilmez) bir kapsam gerektirmiyorsa hello kullanabilirsiniz `clientId` hello hello kapsamda olarak `acquireTokenSilent` ve/veya `acquireTokenRedirect` çağrıları.</span><span class="sxs-lookup"><span data-stu-id="a727c-129">If a backend API does not require a scope (not recommended), you can use hello `clientId` as hello scope in hello `acquireTokenSilent` and/or `acquireTokenRedirect` calls.</span></span>

<!--end-collapse-->
