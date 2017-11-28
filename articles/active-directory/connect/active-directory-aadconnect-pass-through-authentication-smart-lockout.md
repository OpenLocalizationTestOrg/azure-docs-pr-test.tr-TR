---
title: "Azure AD Connect: Doğrudan kimlik doğrulaması - akıllı kilitleme | Microsoft Docs"
description: "Bu makalede, şirket içi hesaplarınızı Azure Active Directory (Azure AD) doğrudan kimlik doğrulama hello bulutta yanılma parola saldırılarından nasıl koruduğunu açıklanmaktadır."
services: active-directory
keywords: "Azure AD Connect doğrudan kimlik doğrulama, Active Directory yükleyin gerekli bileşenleri Azure AD, SSO, çoklu oturum açma"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: b02e315c3cc3eae00ca6408d735a416f34c2cdc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="cf5ae-104">Azure Active Directory doğrudan kimlik doğrulaması: Akıllı kilitleme</span><span class="sxs-lookup"><span data-stu-id="cf5ae-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="cf5ae-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cf5ae-105">Overview</span></span>

<span data-ttu-id="cf5ae-106">Azure AD yanılma parola saldırılarına karşı korur ve Office 365 ve SaaS uygulamalarını dışında kilitli orijinal kullanıcıların engeller.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="cf5ae-107">Adlı bu özelliği, **akıllı kilitleme**, oturum açma yönteminiz olarak doğrudan kimlik doğrulaması kullandığınızda desteklenir.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="cf5ae-108">Akıllı kilitleme tüm kiracılar için varsayılan olarak etkindir ve kullanıcı hesaplarınızı hello zaman koruyorsanız; hiçbir gerek tooturn yoktur üzerinde.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all hello time; there is no need tooturn it on.</span></span>

<span data-ttu-id="cf5ae-109">Başarısız oturum açma girişimleri izlemek tarafından ve belirli bir sonra Akıllı kilitleme çalışır **kilitleme eşiği**başlayan bir **kilitleme süresi**.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="cf5ae-110">Merhaba saldırgan hello kilitleme süresi sırasında tüm oturum açma denemeleri reddedilir.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-110">Any sign-in attempts from hello attacker during hello Lockout Duration are rejected.</span></span> <span data-ttu-id="cf5ae-111">Merhaba saldırı devam ederse, daha uzun kilitleme süreleri sonucunda hello kilitleme süresi sona erdikten sonra hello sonraki başarısız oturum açma çalışır.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-111">If hello attack continues, hello subsequent failed sign-in attempts after hello Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="cf5ae-112">Merhaba kilitleme eşiği 10 başarısız oturum açma girişimlerinin ve kilitleme süresi 60 saniyedir hello varsayılan varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-112">hello default Lockout Threshold is 10 failed attempts, and hello default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="cf5ae-113">Akıllı kilitleme, oturum açma işlemleri orijinal kullanıcılar ve saldırganların ve çoğu durumda hello saldırganlar çıkışı yalnızca kilitleri arasında ayırır.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out hello attackers in most cases.</span></span> <span data-ttu-id="cf5ae-114">Bu işlevsellik, orijinal kullanıcıları kötü amaçlı olarak kilitleme saldırganlar engeller.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="cf5ae-115">Oturum açma davranışı, kullanıcıların cihazları & tarayıcılar ve diğer sinyaller toodistinguish orijinal kullanıcılar ve saldırganların arasında geçen kullanırız.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-115">We use past sign-in behavior, users’ devices & browsers and other signals toodistinguish between genuine users and attackers.</span></span> <span data-ttu-id="cf5ae-116">Biz sürekli bizim algoritmaları geliştirme.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="cf5ae-117">Parola doğrulama isteklerini, şirket içi Active Directory (AD) üzerine doğrudan kimlik doğrulama ileten olduğundan, kullanıcılarınızın AD hesapları kilitleme tooprevent saldırganların gerekir.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need tooprevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="cf5ae-118">Kendi AD hesap kilitleme ilkeleri olduğundan (özellikle [ **hesap kilitleme eşiği** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) ve [ **hesap kilitleme sayaç sonra sıfırlamailkeleri** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), Azure AD tooconfigure kilitleme eşiği gerekir ve kilitleme süresi değerleri uygun şekilde saldırıları hello bulutta kullanıma toofilter şirket içi düşmeden önce AD.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need tooconfigure Azure AD’s Lockout Threshold and Lockout Duration values appropriately toofilter out attacks in hello cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="cf5ae-119">Merhaba akıllı kilitleme özelliğini ücretsiz ve _üzerinde_ tüm müşteriler için varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-119">hello Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="cf5ae-120">Ancak, Azure AD kilitleme eşiği ve grafik API'sini kullanarak kilitleme süresi değerleri değiştirme Kiracı toohave en az bir Azure AD Premium P2 lisansınızı gerekir.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant toohave at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="cf5ae-121">Bir Azure AD Premium P2 lisansı gerekmez _kullanıcı başına_ tooget hello akıllı kilitleme özelliğini doğrudan kimlik doğrulamasına sahip.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-121">You don't need an Azure AD Premium P2 license _per user_ tooget hello Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="cf5ae-122">Kullanıcılarınızın AD hesapları şirket içi olduğunu tooensure iyi korumalı, tooensure gerekir:</span><span class="sxs-lookup"><span data-stu-id="cf5ae-122">tooensure that your users’ on-premises AD accounts are well protected, you need tooensure that:</span></span>

1.  <span data-ttu-id="cf5ae-123">Azure AD kilitleme eşiği _daha az_ Reklamın hesap kilitleme eşiği değerinden.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="cf5ae-124">AD'ın hesap kilitleme eşiği en az iki ya da Azure AD kilitleme eşiği üç kez şekilde hello değerleri ayarlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-124">We recommend that you set hello values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="cf5ae-125">Azure AD kilitleme süresi (saniye cinsinden gösterilir) _uzun_ Reklamın sıfırlama hesap kilitleme sayaç (dakika cinsinden gösterilir) sonra daha.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="cf5ae-126">AD hesap kilitleme ilkeleri doğrulayın</span><span class="sxs-lookup"><span data-stu-id="cf5ae-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="cf5ae-127">Aşağıdaki yönergeler tooverify hello AD hesap kilitleme ilkeleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="cf5ae-127">Use hello following instructions tooverify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="cf5ae-128">Merhaba Grup İlkesi yönetim aracını açın.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-128">Open hello Group Policy Management tool.</span></span>
2.  <span data-ttu-id="cf5ae-129">Örneğin, uygulanan tooall kullanıcılar olan hello Grup İlkesi hello varsayılan etki alanı ilkesi düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-129">Edit hello group policy that is applied tooall users, for example, hello Default Domain Policy.</span></span>
3.  <span data-ttu-id="cf5ae-130">TooComputer Yapılandırması\İlkeler\Windows Ayarları\Güvenlik Ayarları\Hesap İlkeleri\Hesap kilitleme ilkesi gidin.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-130">Navigate tooComputer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="cf5ae-131">Hesap kilitleme eşiği ve hesap kilitleme sayaç sonra sıfırlama değerleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![AD ve hesap kilitleme ilkeleri](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-hello-graph-api-toomanage-your-tenants-smart-lockout-values"></a><span data-ttu-id="cf5ae-133">Merhaba grafik API'si toomanage, kiracının akıllı kilitleme değerlerini kullanın</span><span class="sxs-lookup"><span data-stu-id="cf5ae-133">Use hello Graph API toomanage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="cf5ae-134">Azure AD kilitleme eşiği ve grafik API'sini kullanarak kilitleme süresi değerleri değiştirerek bir Azure AD Premium P2 özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="cf5ae-135">Bu ayrıca, toobe kiracınızın genel yönetici gerekir.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-135">It also needs you toobe a Global Administrator on your tenant.</span></span>

<span data-ttu-id="cf5ae-136">Kullanabileceğiniz [Graph Explorer'a](https://developer.microsoft.com/graph/graph-explorer) tooread, ayarlayın ve Azure AD akıllı kilitleme değerlerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) tooread, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="cf5ae-137">Ancak, bu işlemlerin program aracılığıyla da yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="cf5ae-138">Okuma akıllı kilitleme değerleri</span><span class="sxs-lookup"><span data-stu-id="cf5ae-138">Read Smart Lockout values</span></span>

<span data-ttu-id="cf5ae-139">Bu adımları tooread, kiracının akıllı kilitleme değerleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="cf5ae-139">Follow these steps tooread your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="cf5ae-140">Graph Explorer'a kiracınızın genel yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="cf5ae-141">İstenirse, hello için erişim izni ver izinleri istedi.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-141">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="cf5ae-142">"İzinlerini değiştirme"'i tıklatın ve hello "Directory.ReadWrite.All" izni seçin.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-142">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="cf5ae-143">Merhaba grafik API'si istek gibi yapılandırma: kümesi versiyonunu çok "BETA" istek türü çok "GET" ve URL çok`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-143">Configure hello Graph API request as follows: Set version too“BETA”, request type too“GET” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="cf5ae-144">"Sorgu Çalıştır" toosee, kiracının akıllı kilitleme değerler'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-144">Click "Run Query" toosee your tenant's Smart Lockout values.</span></span> <span data-ttu-id="cf5ae-145">Önce kiracının değerleri ayarlamadıysanız boş bakın.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="cf5ae-146">Akıllı kilitleme değerlerini Ayarla</span><span class="sxs-lookup"><span data-stu-id="cf5ae-146">Set Smart Lockout values</span></span>

<span data-ttu-id="cf5ae-147">Bu adımları tooset, kiracının akıllı kilitleme değerlerini (Merhaba yalnızca ilk kez) izleyin:</span><span class="sxs-lookup"><span data-stu-id="cf5ae-147">Follow these steps tooset your tenant’s Smart Lockout values (for hello first time only):</span></span>

1. <span data-ttu-id="cf5ae-148">Graph Explorer'a kiracınızın genel yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="cf5ae-149">İstenirse, hello için erişim izni ver izinleri istedi.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-149">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="cf5ae-150">"İzinlerini değiştirme"'i tıklatın ve hello "Directory.ReadWrite.All" izni seçin.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-150">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="cf5ae-151">Merhaba grafik API'si istek gibi yapılandırma: kümesi versiyonunu çok "BETA" istek türü çok "POST" ve URL çok`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-151">Configure hello Graph API request as follows: Set version too“BETA”, request type too“POST” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="cf5ae-152">JSON istek hello "İstek gövdesi" alanına aşağıdaki hello kopyalayıp yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-152">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="cf5ae-153">Merhaba akıllı kilitleme değerlerini uygun şekilde değiştirin ve kullanmak için rastgele bir GUID `templateId`.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-153">Change hello Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="cf5ae-154">"Sorgu Çalıştır" tooset, kiracının akıllı kilitleme değerler'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-154">Click "Run Query" tooset your tenant's Smart Lockout values.</span></span>

```
{
  "templateId": "5cf42378-d67d-4f36-ba46-e8b86229381d",
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "300"
    },
    {
      "name": "LockoutThreshold",
      "value": "5"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

>[!NOTE]
><span data-ttu-id="cf5ae-155">Bunları kullanmıyorsanız hello bırakabilirsiniz **BannedPasswordList** ve **EnableBannedPasswordCheck** değerler boş olarak ("") ve "false" sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-155">If you are not using them, you can leave hello **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="cf5ae-156">Doğru kullanarak, kiracının akıllı kilitleme değerleri ayarladığınızdan emin olun [adımları](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="cf5ae-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="cf5ae-157">Akıllı kilitleme değerleri güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="cf5ae-157">Update Smart Lockout values</span></span>

<span data-ttu-id="cf5ae-158">(Önceden daha önce ayarlamış olmanız ise) bu adımları tooupdate, kiracının akıllı kilitleme değerleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="cf5ae-158">Follow these steps tooupdate your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="cf5ae-159">Graph Explorer'a kiracınızın genel yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="cf5ae-160">İstenirse, hello için erişim izni ver izinleri istedi.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-160">If prompted, grant access for hello requested permissions.</span></span>
2. <span data-ttu-id="cf5ae-161">"İzinlerini değiştirme"'i tıklatın ve hello "Directory.ReadWrite.All" izni seçin.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-161">Click “Modify permissions” and select hello “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="cf5ae-162">[Bu adımları tooread, kiracının akıllı kilitleme değerlerini izleyin](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="cf5ae-162">[Follow these steps tooread your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="cf5ae-163">Kopya hello `id` "PasswordRuleSettings" olarak "görünen adı" Merhaba öğesinin değeri (GUID).</span><span class="sxs-lookup"><span data-stu-id="cf5ae-163">Copy hello `id` value (a GUID) of hello item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="cf5ae-164">Hello grafik API'si istek gibi yapılandırma: sürümü çok Ayarla "BETA" çok istek türü "Düzeltme Eki" ve URL çok`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -kullanmak için adım 3 GUID hello `<id>`.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-164">Configure hello Graph API request as follows: Set version too“BETA”, request type too“PATCH” and URL too`https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use hello GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="cf5ae-165">JSON istek hello "İstek gövdesi" alanına aşağıdaki hello kopyalayıp yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-165">Copy and paste hello following JSON request into hello "Request Body" field.</span></span> <span data-ttu-id="cf5ae-166">Merhaba akıllı kilitleme değerleri uygun şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-166">Change hello Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="cf5ae-167">"Sorgu Çalıştır" tooupdate, kiracının akıllı kilitleme değerler'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-167">Click "Run Query" tooupdate your tenant's Smart Lockout values.</span></span>

```
{
  "values": [
    {
      "name": "LockoutDurationInSeconds",
      "value": "30"
    },
    {
      "name": "LockoutThreshold",
      "value": "4"
    },
    {
      "name" : "BannedPasswordList",
      "value": ""
    },
    {
      "name" : "EnableBannedPasswordCheck",
      "value": "false"
    }
  ]
}
```

<span data-ttu-id="cf5ae-168">Doğru kullanarak, kiracının akıllı kilitleme değerleri güncelleştirilmiş doğrulamak [adımları](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="cf5ae-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf5ae-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cf5ae-169">Next steps</span></span>
- <span data-ttu-id="cf5ae-170">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.</span><span class="sxs-lookup"><span data-stu-id="cf5ae-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
