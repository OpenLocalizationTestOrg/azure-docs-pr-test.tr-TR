---
title: "Azure Active Directory koşullu erişim Teknik Başvurusu | Microsoft Docs"
description: "Koşullu erişim denetimi ile Azure Active Directory kullanıcı doğrulanırken ve uygulamaya erişimine izin vermeden önce çekme belirli koşullar denetler. Bu koşullar sağlandığında, kullanıcı kimlik doğrulaması ve uygulamaya erişim izni."
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
ms.openlocfilehash: ca16a5399f94fd1ab267e0798cade3fd83f75b13
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a><span data-ttu-id="440f7-104">Azure Active Directory koşullu erişim Teknik Başvurusu</span><span class="sxs-lookup"><span data-stu-id="440f7-104">Azure Active Directory Conditional Access technical reference</span></span>

## <a name="services-enabled-with-conditional-access"></a><span data-ttu-id="440f7-105">Koşullu erişimle etkin hizmetleri</span><span class="sxs-lookup"><span data-stu-id="440f7-105">Services enabled with conditional access</span></span>

<span data-ttu-id="440f7-106">Koşullu erişim kuralları, çeşitli Azure AD uygulama türleri arasında desteklenir.</span><span class="sxs-lookup"><span data-stu-id="440f7-106">Conditional Access rules are supported across various Azure AD application types.</span></span> <span data-ttu-id="440f7-107">Bu liste aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="440f7-107">This list includes:</span></span>


* <span data-ttu-id="440f7-108">Azure uygulama ara sunucusu ile kaydedilmiş uygulamaları</span><span class="sxs-lookup"><span data-stu-id="440f7-108">Applications registered with the Azure Application Proxy</span></span>
* <span data-ttu-id="440f7-109">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="440f7-109">Azure Remote App</span></span>
* <span data-ttu-id="440f7-110">İş ve Azure AD ile kayıtlı çok kiracılı uygulamalara geliştirilmiş kolu</span><span class="sxs-lookup"><span data-stu-id="440f7-110">Developed line of business and multi-tenant applications registered with Azure AD</span></span>
* <span data-ttu-id="440f7-111">Dynamics CRM</span><span class="sxs-lookup"><span data-stu-id="440f7-111">Dynamics CRM</span></span>
* <span data-ttu-id="440f7-112">Azure AD uygulama galerisinde Federasyon uygulamalardan</span><span class="sxs-lookup"><span data-stu-id="440f7-112">Federated applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="440f7-113">Microsoft Office 365 Yammer</span><span class="sxs-lookup"><span data-stu-id="440f7-113">Microsoft Office 365 Yammer</span></span>
* <span data-ttu-id="440f7-114">Microsoft Office 365 Exchange Online</span><span class="sxs-lookup"><span data-stu-id="440f7-114">Microsoft Office 365 Exchange Online</span></span>
* <span data-ttu-id="440f7-115">Microsoft Office 365 SharePoint (OneDrive iş içerir) çevrimiçi</span><span class="sxs-lookup"><span data-stu-id="440f7-115">Microsoft Office 365 SharePoint Online (includes OneDrive for Business)</span></span>
* <span data-ttu-id="440f7-116">Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="440f7-116">Microsoft Power BI</span></span> 
* <span data-ttu-id="440f7-117">Azure AD uygulama galerisinde'ndan parola SSO uygulamalar</span><span class="sxs-lookup"><span data-stu-id="440f7-117">Password SSO applications from the Azure AD application gallery</span></span>
* <span data-ttu-id="440f7-118">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="440f7-118">Visual Studio Team Services</span></span>
* <span data-ttu-id="440f7-119">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="440f7-119">Microsoft Teams</span></span>









## <a name="enable-access-rules"></a><span data-ttu-id="440f7-120">Erişim kurallarını etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="440f7-120">Enable access rules</span></span>
<span data-ttu-id="440f7-121">Her kural etkinleştirilebilir veya devre dışı bir uygulama tabanları başına.</span><span class="sxs-lookup"><span data-stu-id="440f7-121">Each rule can be enabled or disabled on a per application bases.</span></span> <span data-ttu-id="440f7-122">Kuralları olduğunda **ON** bunlar etkinleştirilecek ve uygulamaya erişen kullanıcılar için uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="440f7-122">When rules are **ON** they will be enabled and enforced for users accessing the application.</span></span> <span data-ttu-id="440f7-123">Olduklarında **OFF** kullanılmayacak ve kullanıcıların oturum açma deneyimini etkilemez.</span><span class="sxs-lookup"><span data-stu-id="440f7-123">When they are **OFF** they will not be used and will not impact the users sign in experience.</span></span>

## <a name="applying-rules-to-specific-users"></a><span data-ttu-id="440f7-124">Belirli kullanıcılara uygulama kuralları</span><span class="sxs-lookup"><span data-stu-id="440f7-124">Applying rules to specific users</span></span>
<span data-ttu-id="440f7-125">Kurallar, belirli ayarlayarak güvenlik grubunu temel alan kullanıcı kümeleri için uygulanabilir **uygulamak için**.</span><span class="sxs-lookup"><span data-stu-id="440f7-125">Rules can be applied to specific sets of users based on security group by setting **Apply To**.</span></span> <span data-ttu-id="440f7-126">**Uygulanacak** ayarlanabilir **tüm kullanıcılar** veya **grupları**.</span><span class="sxs-lookup"><span data-stu-id="440f7-126">**Apply To** can be set to **All Users** or **Groups**.</span></span> <span data-ttu-id="440f7-127">Ayarlandığında **tüm kullanıcılar** kuralları uygulamaya erişimi olan herhangi bir kullanıcı için geçerli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="440f7-127">When set to **All Users** the rules will apply to any user with access to the application.</span></span> <span data-ttu-id="440f7-128">**Grupları** seçeneği, belirli güvenlik ve dağıtım grupları seçilmesine izin verir kuralları yalnızca zorunlu bu gruplara.</span><span class="sxs-lookup"><span data-stu-id="440f7-128">The **Groups** option allows specific security and distribution groups to be selected, rules will only be enforced for these groups.</span></span>

<span data-ttu-id="440f7-129">Bir kural dağıtırken, önce onu bir pilot gruplarının üyeleri olan kullanıcılar sınırlı kümesi uygulamak için yaygın bir sorundur.</span><span class="sxs-lookup"><span data-stu-id="440f7-129">When deploying a rule,  it is common to first apply it a limited set of users, that are members of a piloting groups.</span></span> <span data-ttu-id="440f7-130">Tamamlandıktan sonra kural uygulanabilir **tüm kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="440f7-130">Once complete the rule can be applied to **All Users**.</span></span> <span data-ttu-id="440f7-131">Bu kuralı kuruluştaki tüm kullanıcılar için zorlanacak neden olur.</span><span class="sxs-lookup"><span data-stu-id="440f7-131">This will cause the rule to be enforced for all users in the organization.</span></span>

<span data-ttu-id="440f7-132">Select ayrıca muaf tutulan gruplar İlkesi kullanarak **dışında** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="440f7-132">Select groups may also be exempted from policy using the **Except** option.</span></span> <span data-ttu-id="440f7-133">Dahil edilen grubunda göründükleri olsa bile bu grupların tüm üyelerinin muaf.</span><span class="sxs-lookup"><span data-stu-id="440f7-133">Any members of these groups will be exempted even if they appear in an included group.</span></span>

## <a name="at-work-networks"></a><span data-ttu-id="440f7-134">"İşyerindeki" ağları</span><span class="sxs-lookup"><span data-stu-id="440f7-134">“At work” networks</span></span>
<span data-ttu-id="440f7-135">Bir "işyerindeki" ağı kullanmayı koşullu erişim kuralları, Azure AD içinde yapılandırılmış güvenilen IP adres aralıklarını Bel veya AD FS'den "içinde corpnet" talep kullanın.</span><span class="sxs-lookup"><span data-stu-id="440f7-135">Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of the "inside corpnet" claim from AD FS.</span></span> <span data-ttu-id="440f7-136">Söz konusu kurallar aşağıda belirtilmiştir:</span><span class="sxs-lookup"><span data-stu-id="440f7-136">These rules include:</span></span>

* <span data-ttu-id="440f7-137">Çalışma zaman değil, çok faktörlü kimlik doğrulaması gerektirir</span><span class="sxs-lookup"><span data-stu-id="440f7-137">Require multi-factor authentication when not at work</span></span>
* <span data-ttu-id="440f7-138">İş olduğunda değil, erişimi engelle</span><span class="sxs-lookup"><span data-stu-id="440f7-138">Block access when not at work</span></span>

<span data-ttu-id="440f7-139">Belirtmeyi seçeneklerini "işyerindeki" ağları</span><span class="sxs-lookup"><span data-stu-id="440f7-139">Options for specifiying “at work” networks</span></span>

1. <span data-ttu-id="440f7-140">Güvenilen IP adres aralıklarını yapılandırma [çok faktörlü kimlik doğrulaması yapılandırma sayfası](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="440f7-140">Configure trusted IP address ranges in the [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md).</span></span> <span data-ttu-id="440f7-141">Koşullu erişim ilkesini yapılandırılmış aralıkları her kimlik doğrulama isteği ve belirteç verme kuralları değerlendirmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="440f7-141">Conditional Access policy will use the configured ranges on each authentication request and token issuance to evaluate rules.</span></span> 
2. <span data-ttu-id="440f7-142">İç kullanımını yapılandır corpnet talep, bu seçenek, AD FS kullanarak Federasyon dizinleri ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="440f7-142">Configure use of the inside corpnet claim, this option can be used with federated directories, using AD FS.</span></span> <span data-ttu-id="440f7-143">İç hakkında daha fazla bilgi edinmek için corpnet talep bkz [Tusted IP'leri](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span><span class="sxs-lookup"><span data-stu-id="440f7-143">To learn more about the inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).</span></span>


## <a name="rules-based-on-application-sensitivity"></a><span data-ttu-id="440f7-144">Uygulama duyarlılığına göre kuralları</span><span class="sxs-lookup"><span data-stu-id="440f7-144">Rules based on application sensitivity</span></span>
<span data-ttu-id="440f7-145">Kuralları diğer hizmetlere erişimi etkilemeden korunması yüksek değerli hizmetleri izin vererek uygulama başına yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="440f7-145">Rules are configured per application allowing the high value services to be secured without impacting access to other services.</span></span> <span data-ttu-id="440f7-146">Koşullu erişim kuralları yapılandırılabilir **yapılandırma** uygulama sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="440f7-146">Conditional access rules can be configured on the  **Configure** tab of the application.</span></span> 

<span data-ttu-id="440f7-147">Şu anda sunulan kuralları:</span><span class="sxs-lookup"><span data-stu-id="440f7-147">Rules currently offered:</span></span>

* <span data-ttu-id="440f7-148">**Çok faktörlü kimlik doğrulaması gerektirir**</span><span class="sxs-lookup"><span data-stu-id="440f7-148">**Require multi-factor authentication**</span></span>
  
  * <span data-ttu-id="440f7-149">Bu ilkenin uygulandığı tüm kullanıcılar en az bir kez çok faktörlü kimlik doğrulaması kimlik doğrulaması için gerekli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="440f7-149">All users that this policy is applied to will be required to authenticate via multi-factor authentication at least once.</span></span>
* <span data-ttu-id="440f7-150">**Çalışma zaman değil, çok faktörlü kimlik doğrulaması gerektirir**</span><span class="sxs-lookup"><span data-stu-id="440f7-150">**Require multi-factor authentication when not at work**</span></span>
  
  * <span data-ttu-id="440f7-151">Bu ilke uygulandığında, tüm kullanıcılar İş dışı uzak bir konumdan hizmet erişirseniz en az bir kez çok faktörlü kimlik doğrulaması gerçekleştirmiş gerekli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="440f7-151">If this policy is applied, all users will be required to have performed multi-factor authentication at least once if they access the service from a non-work remote location.</span></span> <span data-ttu-id="440f7-152">Bunlar bir işten uzak bir konuma taşırsanız, çok faktörlü kimlik doğrulama hizmeti erişirken gerçekleştirmek için gerekir.</span><span class="sxs-lookup"><span data-stu-id="440f7-152">If they move from a work to remote location, they will be required to perform multifactor authentication when accessing the service.</span></span>
* <span data-ttu-id="440f7-153">**İş olduğunda değil, erişimi engelle**</span><span class="sxs-lookup"><span data-stu-id="440f7-153">**Block access when not at work**</span></span> 
  
  * <span data-ttu-id="440f7-154">Kullanıcılar uzak bir konuma işten taşıdığınızda, bunlar için "iş olduğunda değil, erişimi engelle" ilkesi uygulanırsa engellenir.</span><span class="sxs-lookup"><span data-stu-id="440f7-154">When users move from work to a remote location, they will be blocked if the "Block access when not at work" policy is applied to them.</span></span>  <span data-ttu-id="440f7-155">Bunlar erişimi olduğunda bir iş konumda yeniden izin verilir.</span><span class="sxs-lookup"><span data-stu-id="440f7-155">They will be re-allowed access when at a work location.</span></span>

## <a name="related-topics"></a><span data-ttu-id="440f7-156">İlgili konular</span><span class="sxs-lookup"><span data-stu-id="440f7-156">Related topics</span></span>
* [<span data-ttu-id="440f7-157">Azure Active Directory'ye bağlı Office 365 ve diğer uygulamalar için erişim güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="440f7-157">Securing access to Office 365 and other apps connected to Azure Active Directory</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="440f7-158">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="440f7-158">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)

