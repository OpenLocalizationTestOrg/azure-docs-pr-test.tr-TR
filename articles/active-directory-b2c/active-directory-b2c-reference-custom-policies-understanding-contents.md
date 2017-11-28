---
title: "Azure Active Directory B2C: Başlangıç paketinin özel ilkelerini anlama | Microsoft Docs"
description: "Bir konu Azure Active Directory B2C özel ilkeler hakkında"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 9847bcfcc139a769847678c1cca6a8b9c3a30e93
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-the-custom-policies-of-the-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="3a08c-103">Azure AD B2C özel ilke başlangıç paketinin özel ilkelerini anlama</span><span class="sxs-lookup"><span data-stu-id="3a08c-103">Understanding the custom policies of the Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="3a08c-104">Bu bölümde birlikte B2C_1A_base ilkesinin tüm çekirdek öğeleri listeler **başlangıç paketi** ve devralma aracılığıyla kendi ilkelerinizi yazmak için de *B2C_1A_base_extensions İlkesi*.</span><span class="sxs-lookup"><span data-stu-id="3a08c-104">This section lists all the core elements of the B2C_1A_base policy that comes with the **Starter Pack** and that is leveraged for authoring your own policies through the inheritance of the *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="3a08c-105">Bu nedenle, bu daha özellikle odaklanılmaktadır. önceden tanımlanmış talep türleri, talep dönüştürmeleri, içerik tanımları, Talep sağlayıcı kendi teknik profillerini ve çekirdek kullanıcı Yolculuklar ile.</span><span class="sxs-lookup"><span data-stu-id="3a08c-105">As such, it more particularly focusses on the already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and the core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3a08c-106">Microsoft veya bundan böyle temin edilen bilgilere göre zımni hiçbir garanti vermez.</span><span class="sxs-lookup"><span data-stu-id="3a08c-106">Microsoft makes no warranties, express or implied, with respect to the information provided hereafter.</span></span> <span data-ttu-id="3a08c-107">Değişiklikleri GA süreden önce herhangi bir zamanda GA zaman ya da sonra sunulmasının.</span><span class="sxs-lookup"><span data-stu-id="3a08c-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="3a08c-108">Kendi ilkelerinizi ve B2C_1A_base_extensions İlkesi, bu tanımları geçersiz kılın ve bu ana ilke gerektiği gibi ek olanları sağlayarak genişletir.</span><span class="sxs-lookup"><span data-stu-id="3a08c-108">Both your own policies and the B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="3a08c-109">Çekirdek öğelerini *B2C_1A_base İlkesi* talep türleri, talep dönüştürmeleri ve içerik tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3a08c-109">The core elements of the *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="3a08c-110">Bu öğeleri açıktır. kendi ilkelerinizi de olarak başvurulan kullanılabilir *B2C_1A_base_extensions İlkesi*.</span><span class="sxs-lookup"><span data-stu-id="3a08c-110">These elements can susceptible to be referenced in your own policies as well as in the *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="3a08c-111">Talep şemaları</span><span class="sxs-lookup"><span data-stu-id="3a08c-111">Claims schemas</span></span>

<span data-ttu-id="3a08c-112">Başka bir talep şemaları, üç bölüme ayrılmıştır:</span><span class="sxs-lookup"><span data-stu-id="3a08c-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="3a08c-113">Kullanıcı Yolculuklar düzgün çalışması gerekli olan minimum talepleri listeler ilk bölümü.</span><span class="sxs-lookup"><span data-stu-id="3a08c-113">A first section that lists the minimum claims that are required for the user journeys to work properly.</span></span>
2.  <span data-ttu-id="3a08c-114">Talepleri listeler ikinci bir bölümü, özellikle login.microsoftonline.com kimlik doğrulaması için diğer talep sağlayıcılardan geçirilecek sorgu dizesi parametreleri ve diğer özel parametreler için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3a08c-114">A second section that lists the claims required for query string parameters and other special parameters to be passed to other claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="3a08c-115">**Lütfen bu talepler değiştirmeyin**.</span><span class="sxs-lookup"><span data-stu-id="3a08c-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="3a08c-116">Ve sonunda kullanıcıdan, toplanan herhangi bir ek, isteğe bağlı talep listeleyen üçüncü bir bölüm dizinde saklanan ve oturum açma sırasında belirteçleri gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3a08c-116">And eventually a third section that lists any additional, optional claims that can be collected from the user, stored in the directory and sent in tokens during sign in.</span></span> <span data-ttu-id="3a08c-117">Bu bölümde kullanıcıdan toplanan ve/veya belirteçte gönderilen yeni talep türü eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="3a08c-117">New claims type to be collected from the user and/or sent in the token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3a08c-118">Talep şema parolaları ve kullanıcı adları gibi belirli talepler kısıtlamaları içerir.</span><span class="sxs-lookup"><span data-stu-id="3a08c-118">The claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="3a08c-119">Herhangi bir talep sağlayıcısı olarak Azure AD güven Framework (TF) ilkesi değerlendirir ve tüm kısıtlamaları premium ilkesinde modelled.</span><span class="sxs-lookup"><span data-stu-id="3a08c-119">The Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in the premium policy.</span></span> <span data-ttu-id="3a08c-120">Daha fazla kısıtlama eklemek ya da başka bir talep sağlayıcı kendi kısıtlamaları olan kimlik bilgisi depolama için kullanmak için bir ilke değiştirilmesi.</span><span class="sxs-lookup"><span data-stu-id="3a08c-120">A policy could be modified to add more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="3a08c-121">Kullanılabilir talep türleri aşağıda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="3a08c-121">The available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-the-user-journeys"></a><span data-ttu-id="3a08c-122">Kullanıcı Yolculuklar için gerekli olan talepleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-122">Claims that are required for the user journeys</span></span>

<span data-ttu-id="3a08c-123">Aşağıdaki talep kullanıcı Yolculuklar düzgün çalışması gereklidir:</span><span class="sxs-lookup"><span data-stu-id="3a08c-123">The following claims are required for user journeys to work properly:</span></span>

| <span data-ttu-id="3a08c-124">Talep türü</span><span class="sxs-lookup"><span data-stu-id="3a08c-124">Claims type</span></span> | <span data-ttu-id="3a08c-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a08c-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="3a08c-126">*Kullanıcı Kimliği*</span><span class="sxs-lookup"><span data-stu-id="3a08c-126">*UserId*</span></span> | <span data-ttu-id="3a08c-127">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="3a08c-127">Username</span></span> |
| <span data-ttu-id="3a08c-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="3a08c-128">*signInName*</span></span> | <span data-ttu-id="3a08c-129">Oturum adı</span><span class="sxs-lookup"><span data-stu-id="3a08c-129">Sign in name</span></span> |
| <span data-ttu-id="3a08c-130">*Tenantıd*</span><span class="sxs-lookup"><span data-stu-id="3a08c-130">*tenantId*</span></span> | <span data-ttu-id="3a08c-131">Azure AD B2C Premium kullanıcı nesnesinin Kiracı tanımlayıcısını (ID)</span><span class="sxs-lookup"><span data-stu-id="3a08c-131">Tenant identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="3a08c-132">*objectID*</span><span class="sxs-lookup"><span data-stu-id="3a08c-132">*objectId*</span></span> | <span data-ttu-id="3a08c-133">Azure AD B2C Premium kullanıcı nesnesinin nesne tanımlayıcısını (ID)</span><span class="sxs-lookup"><span data-stu-id="3a08c-133">Object identifier (ID) of the user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="3a08c-134">*Parola*</span><span class="sxs-lookup"><span data-stu-id="3a08c-134">*password*</span></span> | <span data-ttu-id="3a08c-135">Parola</span><span class="sxs-lookup"><span data-stu-id="3a08c-135">Password</span></span> |
| <span data-ttu-id="3a08c-136">*#newpassword*</span><span class="sxs-lookup"><span data-stu-id="3a08c-136">*newPassword*</span></span> | |
| <span data-ttu-id="3a08c-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="3a08c-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="3a08c-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="3a08c-138">*passwordPolicies*</span></span> | <span data-ttu-id="3a08c-139">Parola gücünü, sona erme vb. belirlemek için Azure AD B2C Premium tarafından kullanılan parola ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="3a08c-139">Password policies used by Azure AD B2C Premium to determine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="3a08c-140">*Sub*</span><span class="sxs-lookup"><span data-stu-id="3a08c-140">*sub*</span></span> | |
| <span data-ttu-id="3a08c-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="3a08c-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="3a08c-142">*Identityprovider*</span><span class="sxs-lookup"><span data-stu-id="3a08c-142">*identityProvider*</span></span> | |
| <span data-ttu-id="3a08c-143">*görünen adı*</span><span class="sxs-lookup"><span data-stu-id="3a08c-143">*displayName*</span></span> | |
| <span data-ttu-id="3a08c-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="3a08c-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="3a08c-145">Kullanıcının telefon numarası</span><span class="sxs-lookup"><span data-stu-id="3a08c-145">User's telephone number</span></span> |
| <span data-ttu-id="3a08c-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="3a08c-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="3a08c-147">*E-posta*</span><span class="sxs-lookup"><span data-stu-id="3a08c-147">*email*</span></span> | <span data-ttu-id="3a08c-148">Kullanıcıyla iletişim kurmak için kullanılan e-posta adresi</span><span class="sxs-lookup"><span data-stu-id="3a08c-148">Email address that can be used to contact the user</span></span> |
| <span data-ttu-id="3a08c-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="3a08c-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="3a08c-150">Kullanıcı oturum açmak için kullandığınız e-posta adresi</span><span class="sxs-lookup"><span data-stu-id="3a08c-150">Email address that the user can use to sign in</span></span> |
| <span data-ttu-id="3a08c-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="3a08c-151">*otherMails*</span></span> | <span data-ttu-id="3a08c-152">Kullanıcıyla iletişim kurmak için kullanılan e-posta adresleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-152">Email addresses that can be used to contact the user</span></span> |
| <span data-ttu-id="3a08c-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="3a08c-153">*userPrincipalName*</span></span> | <span data-ttu-id="3a08c-154">Azure AD B2C Premium içinde depolanan gibi kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="3a08c-154">Username as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="3a08c-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="3a08c-155">*upnUserName*</span></span> | <span data-ttu-id="3a08c-156">Kullanıcı asıl adı oluşturmak için kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="3a08c-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="3a08c-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="3a08c-157">*mailNickName*</span></span> | <span data-ttu-id="3a08c-158">Azure AD B2C Premium içinde depolanan gibi kullanıcının posta takma adı</span><span class="sxs-lookup"><span data-stu-id="3a08c-158">User's mail nick name as stored in the Azure AD B2C Premium</span></span> |
| <span data-ttu-id="3a08c-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="3a08c-159">*newUser*</span></span> | |
| <span data-ttu-id="3a08c-160">*yürütülen-SelfAsserted-giriş*</span><span class="sxs-lookup"><span data-stu-id="3a08c-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="3a08c-161">Talep, öznitelikler kullanıcıdan toplanan olup olmadığını belirtir</span><span class="sxs-lookup"><span data-stu-id="3a08c-161">Claim that specifies whether attributes were collected from the user</span></span> |
| <span data-ttu-id="3a08c-162">*yürütülen-PhoneFactor-giriş*</span><span class="sxs-lookup"><span data-stu-id="3a08c-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="3a08c-163">Talep, yeni bir telefon numarası kullanıcıdan toplanan olup olmadığını belirtir</span><span class="sxs-lookup"><span data-stu-id="3a08c-163">Claim that specifies whether a new phone number was collected from the user</span></span> |
| <span data-ttu-id="3a08c-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="3a08c-164">*authenticationSource*</span></span> | <span data-ttu-id="3a08c-165">Kullanıcının sosyal kimlik sağlayıcısı, login.microsoftonline.com veya yerel hesap doğrulanmış olduğunu belirtir</span><span class="sxs-lookup"><span data-stu-id="3a08c-165">Specifies whether the user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="3a08c-166">Sorgu dizesi parametreleri ve diğer özel parametreler için gereken talepleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="3a08c-167">Aşağıdaki talep varsayılan olarak, diğer talep sağlayıcıları (bazı sorgu dizesi parametreleri de dahil olmak üzere) özel parametrelere geçirmek için gereklidir:</span><span class="sxs-lookup"><span data-stu-id="3a08c-167">The following claims are required to pass on special parameters (including some query string parameters) to other claims providers:</span></span>

| <span data-ttu-id="3a08c-168">Talep türü</span><span class="sxs-lookup"><span data-stu-id="3a08c-168">Claims type</span></span> | <span data-ttu-id="3a08c-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a08c-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="3a08c-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="3a08c-170">*nux*</span></span> | <span data-ttu-id="3a08c-171">Yerel hesap kimlik doğrulaması için login.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="3a08c-171">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="3a08c-172">*NCA*</span><span class="sxs-lookup"><span data-stu-id="3a08c-172">*nca*</span></span> | <span data-ttu-id="3a08c-173">Yerel hesap kimlik doğrulaması için login.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="3a08c-173">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="3a08c-174">*istemi*</span><span class="sxs-lookup"><span data-stu-id="3a08c-174">*prompt*</span></span> | <span data-ttu-id="3a08c-175">Yerel hesap kimlik doğrulaması için login.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="3a08c-175">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="3a08c-176">*Mkt*</span><span class="sxs-lookup"><span data-stu-id="3a08c-176">*mkt*</span></span> | <span data-ttu-id="3a08c-177">Yerel hesap kimlik doğrulaması için login.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="3a08c-177">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="3a08c-178">*LC*</span><span class="sxs-lookup"><span data-stu-id="3a08c-178">*lc*</span></span> | <span data-ttu-id="3a08c-179">Yerel hesap kimlik doğrulaması için login.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="3a08c-179">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="3a08c-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="3a08c-180">*grant_type*</span></span> | <span data-ttu-id="3a08c-181">Yerel hesap kimlik doğrulaması için login.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="3a08c-181">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="3a08c-182">*Kapsam*</span><span class="sxs-lookup"><span data-stu-id="3a08c-182">*scope*</span></span> | <span data-ttu-id="3a08c-183">Yerel hesap kimlik doğrulaması için login.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="3a08c-183">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="3a08c-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="3a08c-184">*client_id*</span></span> | <span data-ttu-id="3a08c-185">Yerel hesap kimlik doğrulaması için login.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="3a08c-185">Special parameter passed for local account authentication to login.microsoftonline.com</span></span> |
| <span data-ttu-id="3a08c-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="3a08c-186">*objectIdFromSession*</span></span> | <span data-ttu-id="3a08c-187">Nesne Kimliği SSO oturumundan alındıktan göstermek için varsayılan oturum yönetimi sağlayıcısı tarafından sağlanan parametre</span><span class="sxs-lookup"><span data-stu-id="3a08c-187">Parameter provided by the default session management provider to indicate that the object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="3a08c-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="3a08c-188">*isActiveMFASession*</span></span> | <span data-ttu-id="3a08c-189">Kullanıcının etkin bir MFA oturumu olduğunu belirtmek için MFA oturum yönetimi tarafından sağlanan parametresi</span><span class="sxs-lookup"><span data-stu-id="3a08c-189">Parameter provided by the MFA session management to indicate that the user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="3a08c-190">Toplanabilir ek (isteğe bağlı) talepleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="3a08c-191">Aşağıdaki talep kullanıcılardan toplanan, dizinde saklanan ve belirteçte gönderilen ek taleplerdir.</span><span class="sxs-lookup"><span data-stu-id="3a08c-191">The following claims are additional claims that can be collected from the users, stored in the directory, and sent in the token.</span></span> <span data-ttu-id="3a08c-192">Önce özetlendiği gibi ek talep bu listeye eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="3a08c-192">As outlined before, additional claims can be added to this list.</span></span>

| <span data-ttu-id="3a08c-193">Talep türü</span><span class="sxs-lookup"><span data-stu-id="3a08c-193">Claims type</span></span> | <span data-ttu-id="3a08c-194">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a08c-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="3a08c-195">*givenName*</span><span class="sxs-lookup"><span data-stu-id="3a08c-195">*givenName*</span></span> | <span data-ttu-id="3a08c-196">Kullanıcının verilen adı (ilk adı olarak da bilinir)</span><span class="sxs-lookup"><span data-stu-id="3a08c-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="3a08c-197">*Soyadı*</span><span class="sxs-lookup"><span data-stu-id="3a08c-197">*surname*</span></span> | <span data-ttu-id="3a08c-198">Kullanıcının soyadı (Aile adı ve Soyadı olarak da bilinir)</span><span class="sxs-lookup"><span data-stu-id="3a08c-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="3a08c-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="3a08c-199">*Extension_picture*</span></span> | <span data-ttu-id="3a08c-200">Sosyal kullanıcının resim</span><span class="sxs-lookup"><span data-stu-id="3a08c-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="3a08c-201">Talep dönüştürmeleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-201">Claim transformations</span></span>

<span data-ttu-id="3a08c-202">Kullanılabilir talep dönüştürmeleri, aşağıda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="3a08c-202">The available claim transformations are listed below.</span></span>

| <span data-ttu-id="3a08c-203">Talep dönüştürme</span><span class="sxs-lookup"><span data-stu-id="3a08c-203">Claim transformation</span></span> | <span data-ttu-id="3a08c-204">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a08c-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="3a08c-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="3a08c-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="3a08c-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="3a08c-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="3a08c-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="3a08c-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="3a08c-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="3a08c-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="3a08c-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="3a08c-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="3a08c-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="3a08c-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="3a08c-211">İçerik tanımları</span><span class="sxs-lookup"><span data-stu-id="3a08c-211">Content definitions</span></span>

<span data-ttu-id="3a08c-212">Bu bölümde zaten bildirilen içerik tanımları açıklanmaktadır *B2C_1A_base* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="3a08c-212">This section describes the content definitions already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="3a08c-213">Bu içerik tanımları başvurulan, geçersiz ve/veya kendi ilkelerinizi de olarak gerektiği şekilde genişletilmiş uygulanmadıkça *B2C_1A_base_extensions* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="3a08c-213">These content definitions are susceptible to be referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="3a08c-214">Talep sağlayıcı</span><span class="sxs-lookup"><span data-stu-id="3a08c-214">Claims provider</span></span> | <span data-ttu-id="3a08c-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a08c-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="3a08c-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="3a08c-216">*Facebook*</span></span> | |
| <span data-ttu-id="3a08c-217">*Yerel hesap oturum açma*</span><span class="sxs-lookup"><span data-stu-id="3a08c-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="3a08c-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="3a08c-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="3a08c-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="3a08c-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="3a08c-220">*Kendi kendine uygulanan*</span><span class="sxs-lookup"><span data-stu-id="3a08c-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="3a08c-221">*Yerel hesap*</span><span class="sxs-lookup"><span data-stu-id="3a08c-221">*Local Account*</span></span> | |
| <span data-ttu-id="3a08c-222">*Oturum yönetimi*</span><span class="sxs-lookup"><span data-stu-id="3a08c-222">*Session Management*</span></span> | |
| <span data-ttu-id="3a08c-223">*Trustframework ilke altyapısı*</span><span class="sxs-lookup"><span data-stu-id="3a08c-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="3a08c-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="3a08c-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="3a08c-225">*Belirteci veren*</span><span class="sxs-lookup"><span data-stu-id="3a08c-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="3a08c-226">Teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-226">Technical profiles</span></span>

<span data-ttu-id="3a08c-227">Bu bölümde Talep sağlayıcı başına zaten tanımlanmış teknik profilleri gösterilmektedir *B2C_1A_base* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="3a08c-227">This section depicts the technical profiles already declared per claim provider in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="3a08c-228">Bu teknik profiller daha fazla başvurulan, geçersiz ve/veya kendi ilkelerinizi de olarak gerektiği şekilde genişletilmiş uygulanmadıkça *B2C_1A_base_extensions* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="3a08c-228">These technical profiles are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="3a08c-229">Facebook için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="3a08c-230">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-230">Technical profile</span></span> | <span data-ttu-id="3a08c-231">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a08c-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3a08c-232">*Facebook OAUTH*</span><span class="sxs-lookup"><span data-stu-id="3a08c-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="3a08c-233">Yerel hesap oturum açma için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="3a08c-234">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-234">Technical profile</span></span> | <span data-ttu-id="3a08c-235">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a08c-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3a08c-236">*Oturum açma etkileşimsiz*</span><span class="sxs-lookup"><span data-stu-id="3a08c-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="3a08c-237">Telefon faktörü için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="3a08c-238">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-238">Technical profile</span></span> | <span data-ttu-id="3a08c-239">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a08c-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3a08c-240">*PhoneFactor giriş*</span><span class="sxs-lookup"><span data-stu-id="3a08c-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="3a08c-241">*PhoneFactor InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="3a08c-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="3a08c-242">*PhoneFactor doğrulayın*</span><span class="sxs-lookup"><span data-stu-id="3a08c-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="3a08c-243">Azure Active Directory için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="3a08c-244">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-244">Technical profile</span></span> | <span data-ttu-id="3a08c-245">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a08c-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3a08c-246">*AAD-genel*</span><span class="sxs-lookup"><span data-stu-id="3a08c-246">*AAD-Common*</span></span> | <span data-ttu-id="3a08c-247">Diğer AAD xxx teknik profilleri dahil teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-247">Technical profile included by the other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="3a08c-248">*AAD UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="3a08c-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="3a08c-249">Sosyal oturum açma teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="3a08c-250">*AAD UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="3a08c-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="3a08c-251">Sosyal oturum açma teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="3a08c-252">*AAD UserReadUsingAlternativeSecurityId NoError*</span><span class="sxs-lookup"><span data-stu-id="3a08c-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="3a08c-253">Sosyal oturum açma teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="3a08c-254">*AAD UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="3a08c-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="3a08c-255">Yerel hesaplar için teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="3a08c-256">*AAD UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="3a08c-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="3a08c-257">Yerel hesaplar için teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="3a08c-258">*AAD UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="3a08c-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="3a08c-259">ObjectID kullanarak kullanıcı kaydını güncelleştirmek için teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="3a08c-260">*AAD UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="3a08c-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="3a08c-261">ObjectID kullanarak kullanıcı kaydını güncelleştirmek için teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="3a08c-262">*AAD UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="3a08c-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="3a08c-263">ObjectID kullanarak kullanıcı kaydını güncelleştirmek için teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="3a08c-264">*AAD UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="3a08c-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="3a08c-265">Teknik profili kullanıcı kimlik doğrulaması yaptıktan sonra verileri okumak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="3a08c-265">Technical profile is used to read data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="3a08c-266">Kendi kendine uygulanan için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="3a08c-267">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-267">Technical profile</span></span> | <span data-ttu-id="3a08c-268">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a08c-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3a08c-269">*SelfAsserted sosyal*</span><span class="sxs-lookup"><span data-stu-id="3a08c-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="3a08c-270">*SelfAsserted ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="3a08c-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="3a08c-271">Yerel hesap için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="3a08c-272">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-272">Technical profile</span></span> | <span data-ttu-id="3a08c-273">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a08c-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3a08c-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="3a08c-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="3a08c-275">Oturum yönetimi için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="3a08c-276">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-276">Technical profile</span></span> | <span data-ttu-id="3a08c-277">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a08c-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3a08c-278">*SM sekmeyi*</span><span class="sxs-lookup"><span data-stu-id="3a08c-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="3a08c-279">*SM AAD*</span><span class="sxs-lookup"><span data-stu-id="3a08c-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="3a08c-280">*SM SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="3a08c-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="3a08c-281">AAD oturum oturum arasında belirsizliğini ortadan kaldırmak ve oturum açma profili adı kullanılıyor</span><span class="sxs-lookup"><span data-stu-id="3a08c-281">Profile name is being used to disambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="3a08c-282">*SM SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="3a08c-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="3a08c-283">*SM MFA*</span><span class="sxs-lookup"><span data-stu-id="3a08c-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="3a08c-284">Trustframework ilke altyapısı TechnicalProfiles için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="3a08c-285">Şu anda hiçbir teknik profilleri tanımlanmış **Trustframework ilke altyapısı TechnicalProfiles** Talep sağlayıcı.</span><span class="sxs-lookup"><span data-stu-id="3a08c-285">Currently, no technical profiles are defined for the **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="3a08c-286">Belirteç Verenin için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="3a08c-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="3a08c-287">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="3a08c-287">Technical profile</span></span> | <span data-ttu-id="3a08c-288">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a08c-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3a08c-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="3a08c-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="3a08c-290">Kullanıcı Yolculuklar</span><span class="sxs-lookup"><span data-stu-id="3a08c-290">User journeys</span></span>

<span data-ttu-id="3a08c-291">Bu bölümde zaten bildirilen kullanıcı Yolculuklar gösterilmektedir *B2C_1A_base* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="3a08c-291">This section depicts the user journeys already declared in the *B2C_1A_base* policy.</span></span> <span data-ttu-id="3a08c-292">Bu kullanıcı Yolculuklar daha fazla başvurulan, geçersiz ve/veya kendi ilkelerinizi de olarak gerektiği şekilde genişletilmiş uygulanmadıkça *B2C_1A_base_extensions* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="3a08c-292">These user journeys are susceptible to be further referenced, overridden, and/or extended as needed in your own policies as well as in the *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="3a08c-293">Kullanıcı gezisine</span><span class="sxs-lookup"><span data-stu-id="3a08c-293">User journey</span></span> | <span data-ttu-id="3a08c-294">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a08c-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="3a08c-295">*Kaydolma*</span><span class="sxs-lookup"><span data-stu-id="3a08c-295">*SignUp*</span></span> | |
| <span data-ttu-id="3a08c-296">*Oturum açma*</span><span class="sxs-lookup"><span data-stu-id="3a08c-296">*SignIn*</span></span> | |
| <span data-ttu-id="3a08c-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="3a08c-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="3a08c-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="3a08c-298">*EditProfile*</span></span> | |
| <span data-ttu-id="3a08c-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="3a08c-299">*PasswordReset*</span></span> | |
