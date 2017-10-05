---
title: "Azure Active Directory B2B işbirliği kullanıcılar için koşullu erişim | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği, şirket uygulamalarınıza seçmeli erişim için çok faktörlü kimlik doğrulaması (MFA) destekler."
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
ms.openlocfilehash: d85f711d6551a68d1248ae8ec61e2ecc1ddc8ecd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="c3c37-103">B2B işbirliği kullanıcılar için koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="c3c37-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="c3c37-104">B2B kullanıcılar için çok faktörlü kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="c3c37-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="c3c37-105">Azure AD B2B işbirliği ile kuruluşlar B2B kullanıcılar için çok faktörlü kimlik doğrulaması (MFA) ilkeleri uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3c37-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="c3c37-106">Bu ilkeler Kiracı, uygulama veya bireysel kullanıcı düzeyinde tam zamanlı çalışanlar ve kuruluşun üyeleri için etkinleştirilen aynı şekilde zorunlu tutulabilir.</span><span class="sxs-lookup"><span data-stu-id="c3c37-106">These policies can be enforced at the tenant, app, or individual user level, the same way that they are enabled for full-time employees and members of the organization.</span></span> <span data-ttu-id="c3c37-107">Kaynak kuruluşta MFA ilkeleri uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c3c37-107">MFA policies are enforced at the resource organization.</span></span>

<span data-ttu-id="c3c37-108">Örnek:</span><span class="sxs-lookup"><span data-stu-id="c3c37-108">Example:</span></span>
1. <span data-ttu-id="c3c37-109">Yönetici veya bilgi çalışanı şirketindeki başvurulmasını Şirket B kullanıcıdan uygulamaya *Foo* A. şirketteki</span><span class="sxs-lookup"><span data-stu-id="c3c37-109">Admin or information worker in Company A invites user from company B to an application *Foo* in company A.</span></span>
2. <span data-ttu-id="c3c37-110">Uygulama *Foo* şirkette A erişimi MFA gerektirecek şekilde yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="c3c37-110">Application *Foo* in company A is configured to require MFA on access.</span></span>
3. <span data-ttu-id="c3c37-111">Şirket B kullanıcıdan uygulamaya erişmeye çalıştığında *Foo* şirket bir kiracı, bunlar bir MFA testini tamamlamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="c3c37-111">When the user from company B attempts to access app *Foo* in the company A tenant, they are asked to complete an MFA challenge.</span></span>
4. <span data-ttu-id="c3c37-112">Kullanıcı kendi MFA Şirket A ile ayarlayabilirsiniz ve bunların MFA seçeneğini seçer.</span><span class="sxs-lookup"><span data-stu-id="c3c37-112">The user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="c3c37-113">Bu senaryo için herhangi bir kimlik çalışır (Azure AD veya örneğin, kullanıcıların şirket b sosyal kimliği kullanarak kimlik doğrulaması MSA)</span><span class="sxs-lookup"><span data-stu-id="c3c37-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="c3c37-114">Şirket A MFA desteği yeterli Azure AD Premium lisansı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3c37-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="c3c37-115">Bu lisans A. şirketten Şirket B kullanıcıdan kullanır</span><span class="sxs-lookup"><span data-stu-id="c3c37-115">The user from company B consumes this license from company A.</span></span>

<span data-ttu-id="c3c37-116">İş ortağı kuruluşun MFA yetenekleri olsa bile davet kiralama her zaman MFA için iş ortağı kuruluştan kullanıcılar sorumludur.</span><span class="sxs-lookup"><span data-stu-id="c3c37-116">The inviting tenancy is always responsible for MFA for users from the partner organization, even if the partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="c3c37-117">B2B işbirliği kullanıcılar için MFA'yı ayarlama</span><span class="sxs-lookup"><span data-stu-id="c3c37-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="c3c37-118">B2B işbirliği kullanıcılar için MFA'yı ayarlama ne kadar kolay olduğunu öğrenmek için bkz aşağıdaki videoda nasıl:</span><span class="sxs-lookup"><span data-stu-id="c3c37-118">To discover how easy it is to set up MFA for B2B collaboration users, see how in the following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="c3c37-119">Kullanım B2B kullanıcılar için MFA deneyimi sunar</span><span class="sxs-lookup"><span data-stu-id="c3c37-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="c3c37-120">Kullanım görmek için aşağıdaki animasyonu kullanıma alın deneyimi:</span><span class="sxs-lookup"><span data-stu-id="c3c37-120">Check out the following animation to see the redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="c3c37-121">MFA B2B işbirliği kullanıcılar için Sıfırla</span><span class="sxs-lookup"><span data-stu-id="c3c37-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="c3c37-122">Şu anda, yöneticinin B2B işbirliği kanıt kullanıcılara yukarı yeniden aşağıdaki PowerShell cmdlet'lerini kullanarak yalnızca gerektirebilir:</span><span class="sxs-lookup"><span data-stu-id="c3c37-122">Currently, the admin can require B2B collaboration users to proof up again only by using the following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="c3c37-123">Azure AD'ye Bağlanma</span><span class="sxs-lookup"><span data-stu-id="c3c37-123">Connect to Azure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="c3c37-124">Tüm kullanıcılara sağlama yöntemleri ile Al</span><span class="sxs-lookup"><span data-stu-id="c3c37-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="c3c37-125">Örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c3c37-125">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="c3c37-126">Güçlü yöntemlerini yeniden ayarlama B2B işbirliği kullanıcının gerektiren belirli bir kullanıcı için MFA yöntemi sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="c3c37-126">Reset the MFA method for a specific user to require the B2B collaboration user to set proof-up methods again.</span></span> <span data-ttu-id="c3c37-127">Örnek:</span><span class="sxs-lookup"><span data-stu-id="c3c37-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-the-resource-tenancy"></a><span data-ttu-id="c3c37-128">Neden şu kaynak kiralama MFA gerçekleştiriyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="c3c37-128">Why do we perform MFA at the resource tenancy?</span></span>

<span data-ttu-id="c3c37-129">Geçerli sürümde MFA kaynak Kiracı öngörülebilirlik nedenleri için her zaman kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="c3c37-129">In the current release, MFA is always in the resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="c3c37-130">Örneğin, Contoso kullanıcı (değiştirmemesi) Fabrikam için davet ettiğiniz ve Fabrikam B2B kullanıcılar için MFA etkinleştirilmiş varsayalım.</span><span class="sxs-lookup"><span data-stu-id="c3c37-130">For example, let’s say a Contoso user (Sally) is invited to Fabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="c3c37-131">Contoso etkin App1 ancak değil App2 için MFA ilkesi varsa, biz Contoso MFA talep belirteci bakarsanız sonra biz aşağıdaki sorunları görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c3c37-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at the Contoso MFA claim in the token, we might see the following issue:</span></span>

* <span data-ttu-id="c3c37-132">1. güne: Bir kullanıcının Contoso ağında MFA varsa ve App1 sonra hiçbir ek MFA erişme istemi Fabrikam ' gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c3c37-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="c3c37-133">2 gün: Kullanıcı, Fabrikam erişirken artık Contoso, uygulama 2 eriştiğini, var. MFA için kaydolması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3c37-133">Day 2: The user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="c3c37-134">Bu işlem kafa karıştırıcı olabilir ve oturum açma tamamlamalar içinde bırakmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="c3c37-134">This process can be confusing and could lead to drop in sign-in completions.</span></span>

<span data-ttu-id="c3c37-135">Contoso MFA yeteneği olsa bile, ayrıca, her zaman çalışması Fabrikam güven Contoso MFA İlkesi değildir.</span><span class="sxs-lookup"><span data-stu-id="c3c37-135">Moreover, even if Contoso has MFA capability, it is not always the case the Fabrikam would trust the Contoso MFA policy.</span></span>

<span data-ttu-id="c3c37-136">Son olarak, kaynak Kiracı MFA ayarladığınız MFA olmayan iş ortağı kuruluşu ve Msa'lar ve sosyal kimlikleri için çalışır.</span><span class="sxs-lookup"><span data-stu-id="c3c37-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="c3c37-137">Bu nedenle, mfa B2B kullanıcılar için her zaman davet kiracısında MFA gerektirecek şekilde önerilir.</span><span class="sxs-lookup"><span data-stu-id="c3c37-137">Therefore, the recommendation for MFA for B2B users is to always require MFA in the inviting tenant.</span></span> <span data-ttu-id="c3c37-138">Bu gereksinim bazı durumlarda çift MFA neden olabilir, ancak davet Kiracı erişimi olduğunda, son kullanıcıların deneyimini tahmin edilebilir: değiştirmemesi MFA için davet Kiracı ile kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3c37-138">This requirement could lead to double MFA in some cases, but whenever accessing the inviting tenant, the end-users experience is predictable: Sally must register for MFA with the inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="c3c37-139">B2B kullanıcılar için cihaz, konum ve risk tabanlı koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="c3c37-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="c3c37-140">Contoso şirket verilerini için cihaz temelli koşullu erişim ilkeleri etkinleştirdiğinde, Contoso tarafından yönetilen ve Contoso cihaz ilkeleriyle uyumlu olmayan cihazlar üzerinden erişimi engelledi.</span><span class="sxs-lookup"><span data-stu-id="c3c37-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with the Contoso device policies.</span></span>

<span data-ttu-id="c3c37-141">B2B kullanıcının cihaz tarafından Contoso yönetilen değil, bu ilkeleri zorunlu herhangi bir bağlamı içinde iş ortağı kuruluşlardan B2B kullanıcıların erişim engellendi.</span><span class="sxs-lookup"><span data-stu-id="c3c37-141">If the B2B user’s device isn't managed by Contoso, access of B2B users from the partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="c3c37-142">Ancak, Contoso cihaz temelli koşullu erişim ilkesinden hariç tutulacak belirli iş ortağı kullanıcıları içeren bir dışlama listesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3c37-142">However, Contoso can create exclusion lists containing specific partner users to exclude them from the device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="c3c37-143">Konum temelli B2B için koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="c3c37-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="c3c37-144">Davet kuruluşun kendi ortak kuruluşlar tanımlayan güvenilir bir IP adresi aralığı oluşturmak mümkün ise B2B kullanıcılar için konum temelli koşullu erişim ilkeleri uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="c3c37-144">Location-based conditional access policies can be enforced for B2B users if the inviting organization is able to create a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="c3c37-145">Risk tabanlı B2B için koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="c3c37-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="c3c37-146">Şu anda, risk değerlendirmesine B2B kullanıcının ev kuruluştan yapıldığından risk tabanlı oturum açma ilkeleri B2B kullanıcılara uygulanamaz.</span><span class="sxs-lookup"><span data-stu-id="c3c37-146">Currently, risk-based sign-in policies cannot be applied to B2B users because the risk evaluation is performed at the B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3c37-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c3c37-147">Next steps</span></span>

<span data-ttu-id="c3c37-148">Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:</span><span class="sxs-lookup"><span data-stu-id="c3c37-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="c3c37-149">Azure AD B2B işbirliği nedir?</span><span class="sxs-lookup"><span data-stu-id="c3c37-149">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="c3c37-150">Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="c3c37-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="c3c37-151">Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?</span><span class="sxs-lookup"><span data-stu-id="c3c37-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="c3c37-152">B2B işbirliği davet e-posta öğeleri</span><span class="sxs-lookup"><span data-stu-id="c3c37-152">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="c3c37-153">B2B işbirliği davet kullanım</span><span class="sxs-lookup"><span data-stu-id="c3c37-153">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="c3c37-154">Azure AD B2B işbirliği lisanslama</span><span class="sxs-lookup"><span data-stu-id="c3c37-154">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="c3c37-155">Azure Active Directory B2B işbirliği sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="c3c37-155">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="c3c37-156">Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)</span><span class="sxs-lookup"><span data-stu-id="c3c37-156">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="c3c37-157">Azure Active Directory B2B işbirliği API ve özelleştirme</span><span class="sxs-lookup"><span data-stu-id="c3c37-157">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="c3c37-158">B2B işbirliği kullanıcıları davet olmadan ekleme</span><span class="sxs-lookup"><span data-stu-id="c3c37-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="c3c37-159">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="c3c37-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
