---
title: "aaaAzure Active Directory koşullu erişim Teknik Başvurusu | Microsoft Docs"
description: "Koşullu erişim denetimi ile Azure Active Directory hello belirli koşullar hello kullanıcı kimlik doğrulaması ve erişim toohello uygulama izin vermeden önce çekme denetler. Bu koşullar sağlandığında hello kullanıcı kimlik doğrulaması ve erişim toohello uygulama izin verilir."
services: active-directory.
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ee201405d1d17f130607a95bf455b60cd222dd0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="a2043-104">Azure Active Directory koşullu erişim Teknik Başvurusu</span><span class="sxs-lookup"><span data-stu-id="a2043-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="a2043-105">Koşullu erişimle etkin hizmetleri</span><span class="sxs-lookup"><span data-stu-id="a2043-105">Services enabled with conditional access</span></span>

<span data-ttu-id="a2043-106">Koşullu erişim kuralları, çeşitli Azure AD uygulama türleri arasında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a2043-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="a2043-107">Bu liste aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="a2043-107">This list includes:</span></span>


* <span data-ttu-id="a2043-108">Azure uygulama proxy'si Hello ile kaydedilmiş uygulamaları</span><span class="sxs-lookup"><span data-stu-id="a2043-108">Applications registered with hello Azure Application Proxy</span></span>
* <span data-ttu-id="a2043-109">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="a2043-109">Azure Remote App</span></span>
* <span data-ttu-id="a2043-110">İş ve Azure AD ile kayıtlı çok kiracılı uygulamalara geliştirilmiş kolu</span><span class="sxs-lookup"><span data-stu-id="a2043-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="a2043-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="a2043-111">Dynamics CRM</span></span>
* <span data-ttu-id="a2043-112">Hello Azure AD uygulama galerisinde Federasyon uygulamalardan</span><span class="sxs-lookup"><span data-stu-id="a2043-112">Federated applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="a2043-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="a2043-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="a2043-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="a2043-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="a2043-115">Microsoft Office 365 SharePoint (OneDrive iş içerir) çevrimiçi</span><span class="sxs-lookup"><span data-stu-id="a2043-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="a2043-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="a2043-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="a2043-117">Parola SSO uygulamalardan hello Azure AD uygulama Galerisi</span><span class="sxs-lookup"><span data-stu-id="a2043-117">Password SSO applications from hello Azure AD application gallery</span></span>
* <span data-ttu-id="a2043-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a2043-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="a2043-119">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a2043-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="a2043-120">Erişim kurallarını etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="a2043-120">Enable access rules</span></span>
<span data-ttu-id="a2043-121">Her kural etkinleştirilebilir veya devre dışı bir uygulama tabanları başına.</span><span class="sxs-lookup"><span data-stu-id="a2043-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="a2043-122">Kuralları olduğunda **ON** bunlar etkinleştirilecek ve hello uygulamaya erişen kullanıcılar için uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="a2043-122">When rules are **ON** they will be enabled and enforced for users accessing hello application.</span></span> <span data-ttu-id="a2043-123">Olduklarında **OFF** değil kullanılır ve etkisi hello kullanıcı deneyimi imzalar.</span><span class="sxs-lookup"><span data-stu-id="a2043-123">When they are **OFF** they will not be used and will not impact hello users sign in experience.</span></span>

## <a name="applying-rules-toospecific-users"></a><span data-ttu-id="a2043-124">Kuralları toospecific kullanıcıların uygulama</span><span class="sxs-lookup"><span data-stu-id="a2043-124">Applying rules toospecific users</span></span>
<span data-ttu-id="a2043-125">Kuralları ayarlayarak güvenlik grubunu temel alan kullanıcı uygulanan toospecific kümeleri olabilir **uygulamak için**.</span><span class="sxs-lookup"><span data-stu-id="a2043-125">Rules can be applied toospecific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="a2043-126">**Uygulanacak** çok ayarlanabilir**tüm kullanıcılar** veya **grupları**.</span><span class="sxs-lookup"><span data-stu-id="a2043-126">**Apply To** can be set too**All Users** or **Groups**.</span></span> <span data-ttu-id="a2043-127">Ayarlandığında çok**tüm kullanıcılar** hello kuralları tooany kullanıcı erişimi toohello uygulamayla geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="a2043-127">When set too**All Users** hello rules will apply tooany user with access toohello application.</span></span> <span data-ttu-id="a2043-128">Merhaba **grupları** seçeneği sağlayan belirli güvenlik ve dağıtım grupları toobe seçili, kuralları yalnızca zorunlu bu gruplara.</span><span class="sxs-lookup"><span data-stu-id="a2043-128">hello **Groups** option allows specific security and distribution groups toobe selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="a2043-129">Bir kural dağıtırken yaygındır toofirst, pilot gruplarının üyeleri olan kullanıcılar, sınırlı sayıda uygulayın.</span><span class="sxs-lookup"><span data-stu-id="a2043-129">When deploying a rule,  it is common toofirst apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="a2043-130">Tam hello kural çok uygulanabilir sonra**tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="a2043-130">Once complete hello rule can be applied too**All Users**.</span></span> <span data-ttu-id="a2043-131">Bu toobe hello kuruluşunuzdaki tüm kullanıcılar için zorlanan hello kural neden olur.</span><span class="sxs-lookup"><span data-stu-id="a2043-131">This will cause hello rule toobe enforced for all users in hello organization.</span></span>

<span data-ttu-id="a2043-132">Select ayrıca muaf tutulan gruplar hello kullanarak ilkesinden **dışında** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="a2043-132">Select groups may also be exempted from policy using hello **Except** option.</span></span> <span data-ttu-id="a2043-133">Dahil edilen grubunda göründükleri olsa bile bu grupların tüm üyelerinin muaf.</span><span class="sxs-lookup"><span data-stu-id="a2043-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="a2043-134">"İşyerindeki" ağları</span><span class="sxs-lookup"><span data-stu-id="a2043-134">“At work” networks</span></span>
<span data-ttu-id="a2043-135">Bir "işyerindeki" ağı kullanmayı koşullu erişim kuralları, Azure AD içinde yapılandırılmış güvenilen IP adres aralıklarını Bel veya hello "içinde corpnet" AD FS talep kullanımını.</span><span class="sxs-lookup"><span data-stu-id="a2043-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of hello "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="a2043-136">Söz konusu kurallar aşağıda belirtilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a2043-136">These rules include:</span></span>

* <span data-ttu-id="a2043-137">Çalışma zaman değil, çok faktörlü kimlik doğrulaması gerektirir</span><span class="sxs-lookup"><span data-stu-id="a2043-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="a2043-138">İş olduğunda değil, erişimi engelle</span><span class="sxs-lookup"><span data-stu-id="a2043-138">Block access when not at work</span></span>

<span data-ttu-id="a2043-139">Belirtmeyi seçeneklerini "işyerindeki" ağları</span><span class="sxs-lookup"><span data-stu-id="a2043-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="a2043-140">Hello güvenilen IP adres aralıklarını yapılandırma [çok faktörlü kimlik doğrulaması yapılandırma sayfası](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="a2043-140">Configure trusted IP address ranges in hello [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="a2043-141">Koşullu erişim ilkesini her kimlik doğrulama isteği ve belirteç verme tooevaluate kurallarında yapılandırılmış hello aralıklarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="a2043-141">Conditional Access policy will use hello configured ranges on each authentication request and token issuance tooevaluate rules.</span></span> 
2. <span data-ttu-id="a2043-142">Corpnet talep içinde hello kullanımını yapılandırmak, bu seçenek, AD FS kullanarak Federasyon dizinleri ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a2043-142">Configure use of hello inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="a2043-143">corpnet talepleri içinde hello hakkında daha fazla toolearn bkz [Tusted IP'leri](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="a2043-143">toolearn more about hello inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="a2043-144">Uygulama duyarlılığına göre kuralları</span><span class="sxs-lookup"><span data-stu-id="a2043-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="a2043-145">Kuralları, erişim tooother Hizmetleri etkilemeden güvenli hello yüksek değerli hizmetleri toobe izin vererek uygulama başına yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="a2043-145">Rules are configured per application allowing hello high value services toobe secured without impacting access tooother services.</span></span> <span data-ttu-id="a2043-146">Koşullu erişim kuralları hello üzerinde yapılandırılabilir **yapılandırma** hello uygulama sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="a2043-146">Conditional access rules can be configured on hello  **Configure** tab of hello application.</span></span> 

<span data-ttu-id="a2043-147">Şu anda sunulan kuralları:</span><span class="sxs-lookup"><span data-stu-id="a2043-147">Rules currently offered:</span></span>

* <span data-ttu-id="a2043-148">**Çok faktörlü kimlik doğrulaması gerektirir**</span><span class="sxs-lookup"><span data-stu-id="a2043-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="a2043-149">Bu ilke uygulanan toowill olan tüm kullanıcıların en az bir kez çok faktörlü kimlik doğrulaması aracılığıyla gerekli tooauthenticate olabilir.</span><span class="sxs-lookup"><span data-stu-id="a2043-149">All users that this policy is applied toowill be required tooauthenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="a2043-150">**Çalışma zaman değil, çok faktörlü kimlik doğrulaması gerektirir**</span><span class="sxs-lookup"><span data-stu-id="a2043-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="a2043-151">Bu ilkenin geçerli olduğu iş dışı uzak bir konumdan hello hizmet eriştiklerinde ise tüm kullanıcıların bu gerçekleştirilen gerekli toohave çok faktörlü kimlik doğrulaması en az bir kez olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a2043-151">If this policy is applied, all users will be required toohave performed multi-factor authentication at least once if they access hello service from a non-work remote location.</span></span> <span data-ttu-id="a2043-152">Bir iş tooremote konumundan taşırsanız, bunlar gerekli tooperform çok faktörlü kimlik doğrulama hello hizmet erişirken olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a2043-152">If they move from a work tooremote location, they will be required tooperform multifactor authentication when accessing hello service.</span></span>
* <span data-ttu-id="a2043-153">**İş olduğunda değil, erişimi engelle**</span><span class="sxs-lookup"><span data-stu-id="a2043-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="a2043-154">Kullanıcılar iş tooa uzak bir konumdan taşıdığınızda, bunlar hello "iş olduğunda değil, erişimi engelle" ilke uygulanan toothem ise engellenir.</span><span class="sxs-lookup"><span data-stu-id="a2043-154">When users move from work tooa remote location, they will be blocked if hello "Block access when not at work" policy is applied toothem.</span></span>  <span data-ttu-id="a2043-155">Bunlar erişimi olduğunda bir iş konumda yeniden izin verilir.</span><span class="sxs-lookup"><span data-stu-id="a2043-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="a2043-156">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="a2043-156">Related topics</span></span>
* [<span data-ttu-id="a2043-157">Active Directory tooAzure bağlı erişim tooOffice 365 ve diğer uygulamaların güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="a2043-157">Securing access tooOffice 365 and other apps connected tooAzure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="a2043-158">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="a2043-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

