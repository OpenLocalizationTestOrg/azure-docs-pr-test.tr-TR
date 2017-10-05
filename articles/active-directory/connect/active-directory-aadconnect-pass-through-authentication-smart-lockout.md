---
title: "Azure AD Connect: Doğrudan kimlik doğrulaması - akıllı kilitleme | Microsoft Docs"
description: "Bu makalede, şirket içi hesaplarınızı Azure Active Directory (Azure AD) doğrudan kimlik doğrulama bulutta yanılma parola saldırılarından nasıl koruduğunu açıklanmaktadır."
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
ms.openlocfilehash: c84b2406e6373701c83c509342129bd6d7d4034b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-pass-through-authentication-smart-lockout"></a><span data-ttu-id="a97ba-104">Azure Active Directory doğrudan kimlik doğrulaması: Akıllı kilitleme</span><span class="sxs-lookup"><span data-stu-id="a97ba-104">Azure Active Directory Pass-through Authentication: Smart Lockout</span></span>

## <a name="overview"></a><span data-ttu-id="a97ba-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a97ba-105">Overview</span></span>

<span data-ttu-id="a97ba-106">Azure AD yanılma parola saldırılarına karşı korur ve Office 365 ve SaaS uygulamalarını dışında kilitli orijinal kullanıcıların engeller.</span><span class="sxs-lookup"><span data-stu-id="a97ba-106">Azure AD protects against brute force password attacks and prevents genuine users from being locked out of their Office 365 and SaaS applications.</span></span> <span data-ttu-id="a97ba-107">Adlı bu özelliği, **akıllı kilitleme**, oturum açma yönteminiz olarak doğrudan kimlik doğrulaması kullandığınızda desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a97ba-107">This capability, called **Smart Lockout**, is supported when you use Pass-through Authentication as your sign-in method.</span></span> <span data-ttu-id="a97ba-108">Akıllı kilitleme tüm kiracılar için varsayılan olarak etkindir ve her zaman kullanıcı hesaplarınızı koruyorsanız; etkinleştirmek için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="a97ba-108">Smart Lockout is enabled by default for all tenants and are protecting your user accounts all the time; there is no need to turn it on.</span></span>

<span data-ttu-id="a97ba-109">Başarısız oturum açma girişimleri izlemek tarafından ve belirli bir sonra Akıllı kilitleme çalışır **kilitleme eşiği**başlayan bir **kilitleme süresi**.</span><span class="sxs-lookup"><span data-stu-id="a97ba-109">Smart Lockout works by keeping track of failed sign-in attempts, and after a certain **Lockout Threshold**, starting a **Lockout Duration**.</span></span> <span data-ttu-id="a97ba-110">Bir saldırgan kilitleme süresi sırasında oturum açma denemeleri reddedilir.</span><span class="sxs-lookup"><span data-stu-id="a97ba-110">Any sign-in attempts from the attacker during the Lockout Duration are rejected.</span></span> <span data-ttu-id="a97ba-111">Saldırı devam ederse, sonraki başarısız oturum açma uzun kilitleme süreleri sonucunda kilitleme süresi sona erdikten sonra çalışır.</span><span class="sxs-lookup"><span data-stu-id="a97ba-111">If the attack continues, the subsequent failed sign-in attempts after the Lockout Duration ends result in longer Lockout Durations.</span></span>

>[!NOTE]
><span data-ttu-id="a97ba-112">Kilitleme eşiği 10 başarısız oturum açma girişimlerinin varsayılandır ve kilitleme süresi varsayılan değer 60 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="a97ba-112">The default Lockout Threshold is 10 failed attempts, and the default Lockout Duration is 60 seconds.</span></span>

<span data-ttu-id="a97ba-113">Akıllı kilitleme, oturum açma işlemleri orijinal kullanıcılar ve saldırganların ve çoğu durumda saldırganlar çıkışı yalnızca kilitleri arasında ayırır.</span><span class="sxs-lookup"><span data-stu-id="a97ba-113">Smart Lockout also distinguishes between sign-ins from genuine users and from attackers and only locks out the attackers in most cases.</span></span> <span data-ttu-id="a97ba-114">Bu işlevsellik, orijinal kullanıcıları kötü amaçlı olarak kilitleme saldırganlar engeller.</span><span class="sxs-lookup"><span data-stu-id="a97ba-114">This functionality prevents attackers from maliciously locking out genuine users.</span></span> <span data-ttu-id="a97ba-115">Oturum açma davranışı, kullanıcıların aygıtlarını & tarayıcılar ve diğer sinyaller orijinal kullanıcılar saldırganlar arasında ayrım yapmak için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="a97ba-115">We use past sign-in behavior, users’ devices & browsers and other signals to distinguish between genuine users and attackers.</span></span> <span data-ttu-id="a97ba-116">Biz sürekli bizim algoritmaları geliştirme.</span><span class="sxs-lookup"><span data-stu-id="a97ba-116">We are constantly improving our algorithms.</span></span>

<span data-ttu-id="a97ba-117">Parola doğrulama isteklerini, şirket içi Active Directory (AD) üzerine doğrudan kimlik doğrulama ileten olduğundan, kullanıcılarınızın AD hesapları kilitleme saldırganların önlemek gerekir.</span><span class="sxs-lookup"><span data-stu-id="a97ba-117">Because Pass-through Authentication forwards password validation requests onto your on-premises Active Directory (AD), you need to prevent attackers from locking out your users’ AD accounts.</span></span> <span data-ttu-id="a97ba-118">Kendi AD hesap kilitleme ilkeleri olduğundan (özellikle [ **hesap kilitleme eşiği** ](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) ve [ **hesap kilitleme sayaç sonra sıfırlamailkeleri** ](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), Azure AD kilitleme eşiği ve kilitleme süresi değerleri uygun şekilde saldırıları bulutta şirket içi düşmeden önce filtrelemek için yapılandırmanız gereken AD.</span><span class="sxs-lookup"><span data-stu-id="a97ba-118">Since you have your own AD Account Lockout policies (specifically, [**Account Lockout Threshold**](https://technet.microsoft.com/library/hh994574(v=ws.11).aspx) and [**Reset Account Lockout Counter After policies**](https://technet.microsoft.com/library/hh994568(v=ws.11).aspx)), you need to configure Azure AD’s Lockout Threshold and Lockout Duration values appropriately to filter out attacks in the cloud before they reach your on-premises AD.</span></span>

>[!NOTE]
><span data-ttu-id="a97ba-119">Akıllı kilitleme özelliğini ücretsiz ve _üzerinde_ tüm müşteriler için varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="a97ba-119">The Smart Lockout feature is free and is _on_ by default for all customers.</span></span> <span data-ttu-id="a97ba-120">Ancak, Azure AD kilitleme eşiği ve grafik API'sini kullanarak kilitleme süresi değerleri değiştirme kiracınız en az bir Azure AD Premium P2 lisansına sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a97ba-120">However, modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API needs your tenant to have at least one Azure AD Premium P2 license.</span></span> <span data-ttu-id="a97ba-121">Bir Azure AD Premium P2 lisansı gerekmez _kullanıcı başına_ doğrudan kimlik doğrulaması ile akıllı kilitleme özelliğini almak için.</span><span class="sxs-lookup"><span data-stu-id="a97ba-121">You don't need an Azure AD Premium P2 license _per user_ to get the Smart Lockout feature with Pass-through Authentication.</span></span>

<span data-ttu-id="a97ba-122">Kullanıcılarınızın emin olmak için şirket içi AD hesapları iyi korumalı, emin olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a97ba-122">To ensure that your users’ on-premises AD accounts are well protected, you need to ensure that:</span></span>

1.  <span data-ttu-id="a97ba-123">Azure AD kilitleme eşiği _daha az_ Reklamın hesap kilitleme eşiği değerinden.</span><span class="sxs-lookup"><span data-stu-id="a97ba-123">Azure AD’s Lockout Threshold is _less_ than AD’s Account Lockout Threshold.</span></span> <span data-ttu-id="a97ba-124">AD'ın hesap kilitleme eşiği en az iki ya da Azure AD kilitleme eşiği üç kez şekilde değerleri ayarlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="a97ba-124">We recommend that you set the values such that AD’s Account Lockout Threshold is at least two or three times Azure AD’s Lockout Threshold.</span></span>
2.  <span data-ttu-id="a97ba-125">Azure AD kilitleme süresi (saniye cinsinden gösterilir) _uzun_ Reklamın sıfırlama hesap kilitleme sayaç (dakika cinsinden gösterilir) sonra daha.</span><span class="sxs-lookup"><span data-stu-id="a97ba-125">Azure AD’s Lockout Duration (represented in seconds) is _longer_ than AD’s Reset Account Lockout Counter After (represented in minutes).</span></span>

## <a name="verify-your-ad-account-lockout-policies"></a><span data-ttu-id="a97ba-126">AD hesap kilitleme ilkeleri doğrulayın</span><span class="sxs-lookup"><span data-stu-id="a97ba-126">Verify your AD Account Lockout policies</span></span>

<span data-ttu-id="a97ba-127">AD hesap kilitleme ilkeleri doğrulamak için aşağıdaki yönergeleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="a97ba-127">Use the following instructions to verify your AD Account Lockout policies:</span></span>

1.  <span data-ttu-id="a97ba-128">Grup İlkesi yönetim aracını açın.</span><span class="sxs-lookup"><span data-stu-id="a97ba-128">Open the Group Policy Management tool.</span></span>
2.  <span data-ttu-id="a97ba-129">Tüm kullanıcılar, örneğin, varsayılan etki alanı ilkesi uygulanan Grup İlkesi düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="a97ba-129">Edit the group policy that is applied to all users, for example, the Default Domain Policy.</span></span>
3.  <span data-ttu-id="a97ba-130">Bilgisayar Yapılandırması\İlkeler\Windows Ayarları\Güvenlik Ayarları\Hesap İlkeleri\Hesap kilitleme ilkesi için gidin.</span><span class="sxs-lookup"><span data-stu-id="a97ba-130">Navigate to Computer Configuration\Policies\Windows Settings\Security Settings\Account Policies\Account Lockout Policy.</span></span>
4.  <span data-ttu-id="a97ba-131">Hesap kilitleme eşiği ve hesap kilitleme sayaç sonra sıfırlama değerleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a97ba-131">Verify your Account Lockout Threshold and Reset Account Lockout Counter After values.</span></span>

![AD ve hesap kilitleme ilkeleri](./media/active-directory-aadconnect-pass-through-authentication/pta5.png)

## <a name="use-the-graph-api-to-manage-your-tenants-smart-lockout-values"></a><span data-ttu-id="a97ba-133">Kiracı'nın akıllı kilitleme değerleri yönetmek için grafik API'sini kullanın</span><span class="sxs-lookup"><span data-stu-id="a97ba-133">Use the Graph API to manage your tenant’s Smart Lockout values</span></span>

>[!IMPORTANT]
><span data-ttu-id="a97ba-134">Azure AD kilitleme eşiği ve grafik API'sini kullanarak kilitleme süresi değerleri değiştirerek bir Azure AD Premium P2 özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="a97ba-134">Modifying Azure AD’s Lockout Threshold and Lockout Duration values using Graph API is an Azure AD Premium P2 feature.</span></span> <span data-ttu-id="a97ba-135">Ayrıca, kiracınızın genel yönetici olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a97ba-135">It also needs you to be a Global Administrator on your tenant.</span></span>

<span data-ttu-id="a97ba-136">Kullanabileceğiniz [Graph Explorer'a](https://developer.microsoft.com/graph/graph-explorer) okuyun, ayarlayın ve Azure AD akıllı kilitleme değerleri güncelleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="a97ba-136">You can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to read, set, and update Azure AD’s Smart Lockout values.</span></span> <span data-ttu-id="a97ba-137">Ancak, bu işlemlerin program aracılığıyla da yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a97ba-137">But you can also do these operations programmatically.</span></span>

### <a name="read-smart-lockout-values"></a><span data-ttu-id="a97ba-138">Okuma akıllı kilitleme değerleri</span><span class="sxs-lookup"><span data-stu-id="a97ba-138">Read Smart Lockout values</span></span>

<span data-ttu-id="a97ba-139">Kiracı'nın akıllı kilitleme değerleri okumak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="a97ba-139">Follow these steps to read your tenant’s Smart Lockout values:</span></span>

1. <span data-ttu-id="a97ba-140">Graph Explorer'a kiracınızın genel yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a97ba-140">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="a97ba-141">İstenirse, istenen izinler için erişim verin.</span><span class="sxs-lookup"><span data-stu-id="a97ba-141">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="a97ba-142">"Değiştirme izinleri"'i tıklatın ve "Directory.ReadWrite.All" izni seçin.</span><span class="sxs-lookup"><span data-stu-id="a97ba-142">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="a97ba-143">Grafik API'si istek gibi yapılandırma: kümesi versiyonunu "BETA", istek türü için "GET" ve URL `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="a97ba-143">Configure the Graph API request as follows: Set version to “BETA”, request type to “GET” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="a97ba-144">Kiracı'nın akıllı kilitleme değerleri görmek için "Sorgu Çalıştır"'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a97ba-144">Click "Run Query" to see your tenant's Smart Lockout values.</span></span> <span data-ttu-id="a97ba-145">Önce kiracının değerleri ayarlamadıysanız boş bakın.</span><span class="sxs-lookup"><span data-stu-id="a97ba-145">If you haven't set your tenant's values before, you see an empty set.</span></span>

### <a name="set-smart-lockout-values"></a><span data-ttu-id="a97ba-146">Akıllı kilitleme değerlerini Ayarla</span><span class="sxs-lookup"><span data-stu-id="a97ba-146">Set Smart Lockout values</span></span>

<span data-ttu-id="a97ba-147">(İlk kez yalnızca), kiracının akıllı kilitleme değerlerini ayarlamak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="a97ba-147">Follow these steps to set your tenant’s Smart Lockout values (for the first time only):</span></span>

1. <span data-ttu-id="a97ba-148">Graph Explorer'a kiracınızın genel yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a97ba-148">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="a97ba-149">İstenirse, istenen izinler için erişim verin.</span><span class="sxs-lookup"><span data-stu-id="a97ba-149">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="a97ba-150">"Değiştirme izinleri"'i tıklatın ve "Directory.ReadWrite.All" izni seçin.</span><span class="sxs-lookup"><span data-stu-id="a97ba-150">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="a97ba-151">Grafik API'si istek gibi yapılandırma: sürüm "BETA" olarak ayarlamak, istek türü "POST" ve URL `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span><span class="sxs-lookup"><span data-stu-id="a97ba-151">Configure the Graph API request as follows: Set version to “BETA”, request type to “POST” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings`.</span></span>
4. <span data-ttu-id="a97ba-152">Kopyalayın ve aşağıdaki JSON isteği "İstek gövdesi" alanına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a97ba-152">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="a97ba-153">Akıllı kilitleme değerleri uygun şekilde değiştirin ve kullanmak için rastgele bir GUID `templateId`.</span><span class="sxs-lookup"><span data-stu-id="a97ba-153">Change the Smart Lockout values as appropriate and use a random GUID for `templateId`.</span></span>
5. <span data-ttu-id="a97ba-154">Kiracı'nın akıllı kilitleme değerlerini ayarlamak için "Sorgu Çalıştır"'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a97ba-154">Click "Run Query" to set your tenant's Smart Lockout values.</span></span>

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
><span data-ttu-id="a97ba-155">Bunları kullanmıyorsanız, bırakabilirsiniz **BannedPasswordList** ve **EnableBannedPasswordCheck** değerler boş olarak ("") ve "false" sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="a97ba-155">If you are not using them, you can leave the **BannedPasswordList** and **EnableBannedPasswordCheck** values as empty ("") and "false" respectively.</span></span>

<span data-ttu-id="a97ba-156">Doğru kullanarak, kiracının akıllı kilitleme değerleri ayarladığınızdan emin olun [adımları](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="a97ba-156">Verify that you have set your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

### <a name="update-smart-lockout-values"></a><span data-ttu-id="a97ba-157">Akıllı kilitleme değerleri güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="a97ba-157">Update Smart Lockout values</span></span>

<span data-ttu-id="a97ba-158">(Önceden daha önce ayarlamış olmanız durumunda), kiracının akıllı kilitleme değerleri güncelleştirmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="a97ba-158">Follow these steps to update your tenant’s Smart Lockout values (if you have already set them before):</span></span>

1. <span data-ttu-id="a97ba-159">Graph Explorer'a kiracınızın genel yönetici olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a97ba-159">Sign into Graph Explorer as a Global Administrator of your tenant.</span></span> <span data-ttu-id="a97ba-160">İstenirse, istenen izinler için erişim verin.</span><span class="sxs-lookup"><span data-stu-id="a97ba-160">If prompted, grant access for the requested permissions.</span></span>
2. <span data-ttu-id="a97ba-161">"Değiştirme izinleri"'i tıklatın ve "Directory.ReadWrite.All" izni seçin.</span><span class="sxs-lookup"><span data-stu-id="a97ba-161">Click “Modify permissions” and select the “Directory.ReadWrite.All” permission.</span></span>
3. <span data-ttu-id="a97ba-162">[Bu adımları, kiracının akıllı kilitleme değerleri okumak için](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="a97ba-162">[Follow these steps to read your tenant's Smart Lockout values](#read-smart-lockout-values).</span></span> <span data-ttu-id="a97ba-163">Kopya `id` "PasswordRuleSettings" olarak "görünen adı" öğesinin değeri (GUID).</span><span class="sxs-lookup"><span data-stu-id="a97ba-163">Copy the `id` value (a GUID) of the item with "displayName" as "PasswordRuleSettings".</span></span>
4. <span data-ttu-id="a97ba-164">Grafik API'si istek gibi yapılandırma: kümesi versiyonunu "BETA", istek türü için "Düzeltme Eki" ve URL `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` -adım 3 için GUID kullanmak `<id>`.</span><span class="sxs-lookup"><span data-stu-id="a97ba-164">Configure the Graph API request as follows: Set version to “BETA”, request type to “PATCH” and URL to `https://graph.microsoft.com/beta/<your-tenant-domain>/settings/<id>` - use the GUID from Step 3 for `<id>`.</span></span>
5. <span data-ttu-id="a97ba-165">Kopyalayın ve aşağıdaki JSON isteği "İstek gövdesi" alanına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a97ba-165">Copy and paste the following JSON request into the "Request Body" field.</span></span> <span data-ttu-id="a97ba-166">Akıllı kilitleme değerleri uygun şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="a97ba-166">Change the Smart Lockout values as appropriate.</span></span>
6. <span data-ttu-id="a97ba-167">Kiracı'nın akıllı kilitleme değerleri güncelleştirmek için "Sorgu Çalıştır"'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a97ba-167">Click "Run Query" to update your tenant's Smart Lockout values.</span></span>

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

<span data-ttu-id="a97ba-168">Doğru kullanarak, kiracının akıllı kilitleme değerleri güncelleştirilmiş doğrulamak [adımları](#read-smart-lockout-values).</span><span class="sxs-lookup"><span data-stu-id="a97ba-168">Verify that you have updated your tenant's Smart Lockout values correctly using [these steps](#read-smart-lockout-values).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a97ba-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a97ba-169">Next steps</span></span>
- <span data-ttu-id="a97ba-170">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.</span><span class="sxs-lookup"><span data-stu-id="a97ba-170">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
