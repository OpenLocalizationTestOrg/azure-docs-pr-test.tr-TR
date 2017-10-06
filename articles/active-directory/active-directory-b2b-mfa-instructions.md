---
title: "Azure Active Directory B2B işbirliği kullanıcılar aaaConditional erişimi | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği seçmeli erişim tooyour kurumsal uygulamalar için çok faktörlü kimlik doğrulaması (MFA) destekler"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: 3a05be4393f74ff8e87f32432a222a5fbac9af62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="407af-103">B2B işbirliği kullanıcılar için koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="407af-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="407af-104">B2B kullanıcılar için çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="407af-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="407af-105">Azure AD B2B işbirliği ile kuruluşlar B2B kullanıcılar için çok faktörlü kimlik doğrulaması (MFA) ilkeleri uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="407af-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="407af-106">Bu ilkeler hello Kiracı, uygulama veya bireysel kullanıcı düzeyinde hello zorunlu tutulabilir aynı şekilde tam zamanlı çalışanlar ve hello kuruluş üyeleri için etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="407af-106">These policies can be enforced at hello tenant, app, or individual user level, hello same way that they are enabled for full-time employees and members of hello organization.</span></span> <span data-ttu-id="407af-107">MFA ilkeleri hello kaynak kuruluştan uygulanır.</span><span class="sxs-lookup"><span data-stu-id="407af-107">MFA policies are enforced at hello resource organization.</span></span>

<span data-ttu-id="407af-108">Örnek:</span><span class="sxs-lookup"><span data-stu-id="407af-108">Example:</span></span>
1. <span data-ttu-id="407af-109">Yönetici veya bilgi çalışanı şirketindeki başvurulmasını Şirket B tooan uygulama kullanıcıdan *Foo* A. şirketteki</span><span class="sxs-lookup"><span data-stu-id="407af-109">Admin or information worker in Company A invites user from company B tooan application *Foo* in company A.</span></span>
2. <span data-ttu-id="407af-110">Uygulama *Foo* şirkette yapılandırılmış toorequire MFA erişimine açık.</span><span class="sxs-lookup"><span data-stu-id="407af-110">Application *Foo* in company A is configured toorequire MFA on access.</span></span>
3. <span data-ttu-id="407af-111">Şirket B hello kullanıcıdan tooaccess uygulama çalıştığında *Foo* oldukları hello şirket Kiracı'da, MFA testini toocomplete istedi.</span><span class="sxs-lookup"><span data-stu-id="407af-111">When hello user from company B attempts tooaccess app *Foo* in hello company A tenant, they are asked toocomplete an MFA challenge.</span></span>
4. <span data-ttu-id="407af-112">Merhaba kullanıcı kendi MFA Şirket A ile ayarlayabilirsiniz ve bunların MFA seçeneğini seçer.</span><span class="sxs-lookup"><span data-stu-id="407af-112">hello user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="407af-113">Bu senaryo için herhangi bir kimlik çalışır (Azure AD veya örneğin, kullanıcıların şirket b sosyal kimliği kullanarak kimlik doğrulaması MSA)</span><span class="sxs-lookup"><span data-stu-id="407af-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="407af-114">Şirket A MFA desteği yeterli Azure AD Premium lisansı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="407af-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="407af-115">Bu lisans A. şirketten Hello kullanıcı B şirketten kullanır</span><span class="sxs-lookup"><span data-stu-id="407af-115">hello user from company B consumes this license from company A.</span></span>

<span data-ttu-id="407af-116">Merhaba ortağı kuruluşu MFA yetenekleri olsa bile hello davet kiralama her zaman MFA için kullanıcıların hello iş ortağı kuruluştan sorumludur.</span><span class="sxs-lookup"><span data-stu-id="407af-116">hello inviting tenancy is always responsible for MFA for users from hello partner organization, even if hello partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="407af-117">B2B işbirliği kullanıcılar için MFA'yı ayarlama</span><span class="sxs-lookup"><span data-stu-id="407af-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="407af-118">B2B işbirliği kullanıcılar için MFA yukarı tooset olduğu ne kadar kolay toodiscover bkz nasıl içinde hello video:</span><span class="sxs-lookup"><span data-stu-id="407af-118">toodiscover how easy it is tooset up MFA for B2B collaboration users, see how in hello following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="407af-119">Kullanım B2B kullanıcılar için MFA deneyimi sunar</span><span class="sxs-lookup"><span data-stu-id="407af-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="407af-120">Animasyon toosee hello kullanım deneyimi aşağıdaki hello denetleyin:</span><span class="sxs-lookup"><span data-stu-id="407af-120">Check out hello following animation toosee hello redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="407af-121">MFA B2B işbirliği kullanıcılar için Sıfırla</span><span class="sxs-lookup"><span data-stu-id="407af-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="407af-122">Şu anda hello Yöneticisi B2B işbirliği kullanıcılar tooproof yukarı yeniden gerektirebilir PowerShell cmdlet'lerini aşağıdaki hello kullanarak yalnızca:</span><span class="sxs-lookup"><span data-stu-id="407af-122">Currently, hello admin can require B2B collaboration users tooproof up again only by using hello following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="407af-123">TooAzure AD connect</span><span class="sxs-lookup"><span data-stu-id="407af-123">Connect tooAzure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="407af-124">Tüm kullanıcılara sağlama yöntemleri ile Al</span><span class="sxs-lookup"><span data-stu-id="407af-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="407af-125">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="407af-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="407af-126">Merhaba MFA yöntemi bir özel kullanıcı toorequire hello B2B işbirliği kullanıcı tooset güçlü yöntemleri için yeniden Sıfırla.</span><span class="sxs-lookup"><span data-stu-id="407af-126">Reset hello MFA method for a specific user toorequire hello B2B collaboration user tooset proof-up methods again.</span></span> <span data-ttu-id="407af-127">Örnek:</span><span class="sxs-lookup"><span data-stu-id="407af-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-hello-resource-tenancy"></a><span data-ttu-id="407af-128">Neden biz hello kaynak kiralama MFA gerçekleştiriyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="407af-128">Why do we perform MFA at hello resource tenancy?</span></span>

<span data-ttu-id="407af-129">Merhaba geçerli sürümde, MFA öngörülebilirlik nedenlerle hello kaynak kiralama her zaman kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="407af-129">In hello current release, MFA is always in hello resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="407af-130">Örneğin, Contoso kullanıcı (değiştirmemesi) davet edilen tooFabrikam ve Fabrikam B2B kullanıcılar için MFA etkinleştirilmiş varsayalım.</span><span class="sxs-lookup"><span data-stu-id="407af-130">For example, let’s say a Contoso user (Sally) is invited tooFabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="407af-131">Contoso etkin App1 ancak değil App2 için MFA ilkesi varsa, biz hello Contoso MFA talep hello belirtecindeki bakarsanız sonra biz sorunu aşağıdaki hello görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="407af-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at hello Contoso MFA claim in hello token, we might see hello following issue:</span></span>

* <span data-ttu-id="407af-132">1. güne: Bir kullanıcının Contoso ağında MFA varsa ve App1 sonra hiçbir ek MFA erişme istemi Fabrikam ' gösterilir.</span><span class="sxs-lookup"><span data-stu-id="407af-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="407af-133">Günde 2: hello kullanıcı, Fabrikam erişirken artık Contoso, uygulama 2 eriştiğini, var. MFA için kaydolması gerekir.</span><span class="sxs-lookup"><span data-stu-id="407af-133">Day 2: hello user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="407af-134">Bu işlem kafa karıştırıcı olabilir ve oturum açma tamamlamalar içinde toodrop neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="407af-134">This process can be confusing and could lead toodrop in sign-in completions.</span></span>

<span data-ttu-id="407af-135">Contoso MFA yeteneği olsa bile, ayrıca, her zaman hello servis talebi hello Fabrikam hello Contoso MFA İlkesi güven değildir.</span><span class="sxs-lookup"><span data-stu-id="407af-135">Moreover, even if Contoso has MFA capability, it is not always hello case hello Fabrikam would trust hello Contoso MFA policy.</span></span>

<span data-ttu-id="407af-136">Son olarak, kaynak Kiracı MFA ayarladığınız MFA olmayan iş ortağı kuruluşu ve Msa'lar ve sosyal kimlikleri için çalışır.</span><span class="sxs-lookup"><span data-stu-id="407af-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="407af-137">Bu nedenle, hello mfa B2B kullanıcılar için tooalways Kiracı davet hello MFA gerektirecek önerilir.</span><span class="sxs-lookup"><span data-stu-id="407af-137">Therefore, hello recommendation for MFA for B2B users is tooalways require MFA in hello inviting tenant.</span></span> <span data-ttu-id="407af-138">Bu gereksinim toodouble MFA bazı durumlarda neden olabilir, ancak hello davet Kiracı erişen her hello son kullanıcıların deneyimini tahmin edilebilir: değiştirmemesi MFA için hello davet Kiracı ile kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="407af-138">This requirement could lead toodouble MFA in some cases, but whenever accessing hello inviting tenant, hello end-users experience is predictable: Sally must register for MFA with hello inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="407af-139">B2B kullanıcılar için cihaz, konum ve risk tabanlı koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="407af-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="407af-140">Contoso şirket verilerini için cihaz temelli koşullu erişim ilkeleri etkinleştirdiğinde, Contoso ve hello Contoso cihaz ilkeleriyle uyumlu olmayan yönetilmeyen cihazlar üzerinden erişimi engelledi.</span><span class="sxs-lookup"><span data-stu-id="407af-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with hello Contoso device policies.</span></span>

<span data-ttu-id="407af-141">Hello B2B kullanıcının cihaz Contoso tarafından yönetilmiyor, bu ilkeleri zorunlu ne olursa olsun bağlamda hello iş ortağı kuruluşlardan B2B kullanıcıların erişim engellendi.</span><span class="sxs-lookup"><span data-stu-id="407af-141">If hello B2B user’s device isn't managed by Contoso, access of B2B users from hello partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="407af-142">Ancak, Contoso belirli iş ortağı kullanıcıların tooexclude içeren liste onlardan cihaz temelli koşullu erişim ilkesi hello dışlama oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="407af-142">However, Contoso can create exclusion lists containing specific partner users tooexclude them from hello device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="407af-143">Konum temelli B2B için koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="407af-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="407af-144">Merhaba davet kuruluş mümkün toocreate kendi ortak kuruluşlar tanımlayan güvenilir bir IP adresi aralığı ise B2B kullanıcılar için konum temelli koşullu erişim ilkeleri uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="407af-144">Location-based conditional access policies can be enforced for B2B users if hello inviting organization is able toocreate a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="407af-145">Risk tabanlı B2B için koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="407af-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="407af-146">Şu anda Hello risk değerlendirme hello B2B kullanıcının ev kuruluştan yapıldığından risk tabanlı oturum açma ilkeleri uygulanan tooB2B kullanıcılar olamaz.</span><span class="sxs-lookup"><span data-stu-id="407af-146">Currently, risk-based sign-in policies cannot be applied tooB2B users because hello risk evaluation is performed at hello B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="407af-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="407af-147">Next steps</span></span>

<span data-ttu-id="407af-148">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="407af-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="407af-149">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="407af-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="407af-150">Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="407af-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="407af-151">Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="407af-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="407af-152">Merhaba B2B işbirliği davet e-posta Hello öğeleri</span><span class="sxs-lookup"><span data-stu-id="407af-152">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="407af-153">B2B işbirliği davet kullanım</span><span class="sxs-lookup"><span data-stu-id="407af-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="407af-154">Azure AD B2B işbirliği lisanslama</span><span class="sxs-lookup"><span data-stu-id="407af-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="407af-155">Azure Active Directory B2B işbirliği sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="407af-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="407af-156">Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="407af-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="407af-157">Azure Active Directory B2B işbirliği API ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="407af-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="407af-158">B2B işbirliği kullanıcıları davet olmadan ekleme</span><span class="sxs-lookup"><span data-stu-id="407af-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="407af-159">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="407af-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
