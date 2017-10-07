---
title: "aaaAzure Active Directory koşullu erişim ile ilgili SSS | Microsoft Docs"
description: "Azure Active Directory'de koşullu erişim hakkında sorular yanıtlar toofrequently alın."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="ef617-103">Azure Active Directory koşullu erişim ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="ef617-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="ef617-104">Hangi uygulamaların koşullu erişim ilkeleriyle birlikte çalışır?</span><span class="sxs-lookup"><span data-stu-id="ef617-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="ef617-105">Koşullu erişim ilkeleriyle birlikte çalışan uygulamalar hakkında daha fazla bilgi için bkz: [uygulamalar ve Azure Active Directory'de koşullu erişim kuralları kullanma tarayıcılar](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="ef617-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="ef617-106">Koşullu erişim ilkeleri, B2B işbirliğinin ve Konuk kullanıcılar için uygulanır?</span><span class="sxs-lookup"><span data-stu-id="ef617-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="ef617-107">İlkeleri işletmeden işletmeye (B2B) işbirliği kullanıcılar için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ef617-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="ef617-108">Ancak, bazı durumlarda, bir kullanıcı mümkün toosatisfy hello ilkesi gereksinimlerini olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="ef617-108">However, in some cases, a user might not be able toosatisfy hello policy requirements.</span></span> <span data-ttu-id="ef617-109">Örneğin, bir Konuk kullanıcı kuruluşunun çok faktörlü kimlik doğrulamasını desteklemiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="ef617-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a><span data-ttu-id="ef617-110">SharePoint Online İlkesi de tooOneDrive iş için uygulanacak?</span><span class="sxs-lookup"><span data-stu-id="ef617-110">Does a SharePoint Online policy also apply tooOneDrive for Business?</span></span>

<span data-ttu-id="ef617-111">Evet.</span><span class="sxs-lookup"><span data-stu-id="ef617-111">Yes.</span></span> <span data-ttu-id="ef617-112">SharePoint Online İlkesi tooOneDrive işletmeler için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ef617-112">A SharePoint Online policy also applies tooOneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="ef617-113">Neden t istemci uygulamaları, Word veya Outlook gibi bir ilke ayarlanamaz?</span><span class="sxs-lookup"><span data-stu-id="ef617-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="ef617-114">Bir koşullu erişim ilkesi, bir hizmete erişim gereksinimleri ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ef617-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="ef617-115">Kimlik doğrulama toothat hizmeti oluştuğunda zorlanır.</span><span class="sxs-lookup"><span data-stu-id="ef617-115">It's enforced when authentication toothat service occurs.</span></span> <span data-ttu-id="ef617-116">Hello İlkesi doğrudan bir istemci uygulaması ayarlanmadı.</span><span class="sxs-lookup"><span data-stu-id="ef617-116">hello policy is not set directly on a client application.</span></span> <span data-ttu-id="ef617-117">Bunun yerine, bir istemci bir hizmet çağırdığında uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ef617-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="ef617-118">Örneğin, SharePoint üzerinde ayarlanmış bir ilkeyle SharePoint çağırma tooclients geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ef617-118">For example, a policy set on SharePoint applies tooclients calling SharePoint.</span></span> <span data-ttu-id="ef617-119">Bir ilke Exchange'de kümesi tooOutlook geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ef617-119">A policy set on Exchange applies tooOutlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a><span data-ttu-id="ef617-120">Bir koşullu erişim ilkesi tooservice hesapları uygulanacak?</span><span class="sxs-lookup"><span data-stu-id="ef617-120">Does a conditional access policy apply tooservice accounts?</span></span>

<span data-ttu-id="ef617-121">Koşullu erişim ilkeleri, tooall kullanıcı hesapları uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ef617-121">Conditional access policies apply tooall user accounts.</span></span> <span data-ttu-id="ef617-122">Bu, hizmet hesapları olarak kullanılan kullanıcı hesaplarını içerir.</span><span class="sxs-lookup"><span data-stu-id="ef617-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="ef617-123">Genellikle, katılımsız çalışan bir hizmet hesabı hello gereksinimleri koşullu erişim ilkesinin gerçekleştiremiyor.</span><span class="sxs-lookup"><span data-stu-id="ef617-123">Often, a service account that runs unattended can't satisfy hello requirements of a conditional access policy.</span></span> <span data-ttu-id="ef617-124">Örneğin, çok faktörlü kimlik doğrulaması gerekli olabilir.</span><span class="sxs-lookup"><span data-stu-id="ef617-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="ef617-125">Hizmet hesapları, koşullu erişim ilkesi yönetimi ayarları kullanarak bir ilkeden tutulabilir.</span><span class="sxs-lookup"><span data-stu-id="ef617-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="ef617-126">Graph API koşullu erişim ilkelerini yapılandırma için kullanılabilir mi?</span><span class="sxs-lookup"><span data-stu-id="ef617-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="ef617-127">Şu anda yok.</span><span class="sxs-lookup"><span data-stu-id="ef617-127">Currently, no.</span></span> 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="ef617-128">Desteklenmeyen cihaz platformları için hello varsayılan dışlama İlkesi nedir?</span><span class="sxs-lookup"><span data-stu-id="ef617-128">What is hello default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="ef617-129">Şu anda, koşullu erişim ilkeleri seçmeli olarak iOS ve Android cihazlarının kullanıcıları uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ef617-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="ef617-130">Uygulamalar diğer cihaz platformları üzerinde varsayılan olarak, iOS ve Android cihazlar için hello koşullu erişim ilkesi tarafından etkilenmez.</span><span class="sxs-lookup"><span data-stu-id="ef617-130">Applications on other device platforms are, by default, not affected by hello conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="ef617-131">Bir kiracı Yöneticisi toooverride hello genel ilke toodisallow erişim toousers desteklenmeyen platformlarda seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef617-131">A tenant admin can choose toooverride hello global policy toodisallow access toousers on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="ef617-132">Koşullu erişim ilkeleri Microsoft Teams nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="ef617-132">How do conditional access policies work for Microsoft Teams?</span></span>  

<span data-ttu-id="ef617-133">Microsoft Teams yoğun olarak Exchange Online ve SharePoint Online toplantılar, takvimler ve dosya paylaşımı gibi temel üretkenlik senaryolar için dayanır.</span><span class="sxs-lookup"><span data-stu-id="ef617-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="ef617-134">Bir kullanıcı oturum açtığında bu bulut uygulamaları için ayarlanan koşullu erişim ilkeleri tooMicrosoft takımlar uygulayın.</span><span class="sxs-lookup"><span data-stu-id="ef617-134">Conditional access policies that are set for these cloud apps apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="ef617-135">Microsoft Teams de Azure Active Directory koşullu erişim ilkeleri, bir bulut uygulamasında olarak ayrı olarak desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ef617-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="ef617-136">Bir kullanıcı oturum açtığında bir bulut uygulaması için ayarlanan sertifika yetkilisi ilkeleri tooMicrosoft takımlar uygulayın.</span><span class="sxs-lookup"><span data-stu-id="ef617-136">Certificate authority policies that are set for a cloud app apply tooMicrosoft Teams when a user signs in.</span></span>

<span data-ttu-id="ef617-137">Windows ve Mac için Microsoft Teams Masaüstü istemcileri modern kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="ef617-137">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="ef617-138">Modern kimlik doğrulaması oturum platformlarında hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office istemci uygulamalarını temel açma getirir.</span><span class="sxs-lookup"><span data-stu-id="ef617-138">Modern authentication brings sign-in based on hello Azure Active Directory Authentication Library (ADAL) tooMicrosoft Office client applications across platforms.</span></span> 
