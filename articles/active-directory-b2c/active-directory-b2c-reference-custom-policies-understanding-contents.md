---
title: "Azure Active Directory B2C: hello başlangıç paketinin özel ilkelerini anlama | Microsoft Docs"
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
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="a3041-103">Hello Azure AD B2C özel İlkesi başlangıç paketinin Hello özel ilkelerini anlama</span><span class="sxs-lookup"><span data-stu-id="a3041-103">Understanding hello custom policies of hello Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="a3041-104">Bu bölümde hello ile birlikte gelen hello B2C_1A_base ilkesinin tüm hello çekirdek öğeleri listeler **başlangıç paketi** ve kendi ilkelerinizi hello hello devralma aracılığıyla yazmak için de *B2C_1A_base_ Uzantıları İlkesi*.</span><span class="sxs-lookup"><span data-stu-id="a3041-104">This section lists all hello core elements of hello B2C_1A_base policy that comes with hello **Starter Pack** and that is leveraged for authoring your own policies through hello inheritance of hello *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="a3041-105">Bu nedenle, bu daha fazla özellikle odaklanılmaktadır. önceden tanımlanmış hello üzerinde talep türleri, talep dönüştürmeleri, içerik tanımları, Talep sağlayıcı ile bunların teknik profillerini ve çekirdek kullanıcı Yolculuklar hello.</span><span class="sxs-lookup"><span data-stu-id="a3041-105">As such, it more particularly focusses on hello already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and hello core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3041-106">Microsoft hiçbir açık veya zımni, bundan böyle sağlanan saygı toohello bilgilerle garantide bulunmaz.</span><span class="sxs-lookup"><span data-stu-id="a3041-106">Microsoft makes no warranties, express or implied, with respect toohello information provided hereafter.</span></span> <span data-ttu-id="a3041-107">Değişiklikleri GA süreden önce herhangi bir zamanda GA zaman ya da sonra sunulmasının.</span><span class="sxs-lookup"><span data-stu-id="a3041-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="a3041-108">Kendi ilkeleri ve hello B2C_1A_base_extensions İlkesi, bu tanımları geçersiz kılın ve bu ana ilke gerektiği gibi ek olanları sağlayarak genişletir.</span><span class="sxs-lookup"><span data-stu-id="a3041-108">Both your own policies and hello B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="a3041-109">Merhaba çekirdek öğeleri hello *B2C_1A_base İlkesi* talep türleri, talep dönüştürmeleri ve içerik tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a3041-109">hello core elements of hello *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="a3041-110">Bu öğeleri kendi ilkelerinizi de olduğu gibi hello başvurulan uygulanmadıkça toobe kullanılabilir *B2C_1A_base_extensions İlkesi*.</span><span class="sxs-lookup"><span data-stu-id="a3041-110">These elements can susceptible toobe referenced in your own policies as well as in hello *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="a3041-111">Talep şemaları</span><span class="sxs-lookup"><span data-stu-id="a3041-111">Claims schemas</span></span>

<span data-ttu-id="a3041-112">Başka bir talep şemaları, üç bölüme ayrılmıştır:</span><span class="sxs-lookup"><span data-stu-id="a3041-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="a3041-113">Düzgün şekilde hello kullanıcı Yolculuklar toowork için gerekli olan hello minimum talepleri listeler ilk bölümü.</span><span class="sxs-lookup"><span data-stu-id="a3041-113">A first section that lists hello minimum claims that are required for hello user journeys toowork properly.</span></span>
2.  <span data-ttu-id="a3041-114">Sorgu dizesi parametreleri için gereken talepleri listeler hello ve diğer özel parametreler toobe tooother talep sağlayıcıları, geçirilen ikinci bölümü özellikle login.microsoftonline.com kimlik doğrulaması için.</span><span class="sxs-lookup"><span data-stu-id="a3041-114">A second section that lists hello claims required for query string parameters and other special parameters toobe passed tooother claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="a3041-115">**Lütfen bu talepler değiştirmeyin**.</span><span class="sxs-lookup"><span data-stu-id="a3041-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="a3041-116">Ve sonunda hello kullanıcıdan toplanan herhangi bir ek, isteğe bağlı talep listeleyen üçüncü bir bölüm hello dizinde saklanan ve oturum açma sırasında belirteçleri gönderilen.</span><span class="sxs-lookup"><span data-stu-id="a3041-116">And eventually a third section that lists any additional, optional claims that can be collected from hello user, stored in hello directory and sent in tokens during sign in.</span></span> <span data-ttu-id="a3041-117">Bu bölümde türü toobe hello kullanıcıdan toplanan ve/veya hello belirteçte gönderilen yeni talep eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="a3041-117">New claims type toobe collected from hello user and/or sent in hello token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3041-118">Merhaba talep şema parolaları ve kullanıcı adları gibi belirli talepler kısıtlamaları içerir.</span><span class="sxs-lookup"><span data-stu-id="a3041-118">hello claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="a3041-119">Merhaba güven Framework (TF) ilke Azure AD herhangi bir talep sağlayıcısı olarak değerlendirir ve tüm kısıtlamaları hello premium ilkesinde modelled.</span><span class="sxs-lookup"><span data-stu-id="a3041-119">hello Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in hello premium policy.</span></span> <span data-ttu-id="a3041-120">Bir ilke, daha fazla kısıtlama değiştirilmiş tooadd olması veya başka bir talep sağlayıcı kendi kısıtlamaları olan kimlik bilgisi depolama alanını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3041-120">A policy could be modified tooadd more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="a3041-121">Merhaba kullanılabilir talep türleri aşağıda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="a3041-121">hello available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-hello-user-journeys"></a><span data-ttu-id="a3041-122">Merhaba kullanıcı Yolculuklar için gerekli olan talepleri</span><span class="sxs-lookup"><span data-stu-id="a3041-122">Claims that are required for hello user journeys</span></span>

<span data-ttu-id="a3041-123">Talepler aşağıdaki hello düzgün kullanıcı Yolculuklar toowork için gereklidir:</span><span class="sxs-lookup"><span data-stu-id="a3041-123">hello following claims are required for user journeys toowork properly:</span></span>

| <span data-ttu-id="a3041-124">Talep türü</span><span class="sxs-lookup"><span data-stu-id="a3041-124">Claims type</span></span> | <span data-ttu-id="a3041-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3041-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="a3041-126">*Kullanıcı Kimliği*</span><span class="sxs-lookup"><span data-stu-id="a3041-126">*UserId*</span></span> | <span data-ttu-id="a3041-127">Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="a3041-127">Username</span></span> |
| <span data-ttu-id="a3041-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="a3041-128">*signInName*</span></span> | <span data-ttu-id="a3041-129">Oturum adı</span><span class="sxs-lookup"><span data-stu-id="a3041-129">Sign in name</span></span> |
| <span data-ttu-id="a3041-130">*Tenantıd*</span><span class="sxs-lookup"><span data-stu-id="a3041-130">*tenantId*</span></span> | <span data-ttu-id="a3041-131">Azure AD B2C Premium hello kullanıcı nesnesinin Kiracı tanımlayıcısını (ID)</span><span class="sxs-lookup"><span data-stu-id="a3041-131">Tenant identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="a3041-132">*objectID*</span><span class="sxs-lookup"><span data-stu-id="a3041-132">*objectId*</span></span> | <span data-ttu-id="a3041-133">Azure AD B2C Premium hello kullanıcı nesnesinin nesne tanımlayıcısını (ID)</span><span class="sxs-lookup"><span data-stu-id="a3041-133">Object identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="a3041-134">*Parola*</span><span class="sxs-lookup"><span data-stu-id="a3041-134">*password*</span></span> | <span data-ttu-id="a3041-135">Parola</span><span class="sxs-lookup"><span data-stu-id="a3041-135">Password</span></span> |
| <span data-ttu-id="a3041-136">*#newpassword*</span><span class="sxs-lookup"><span data-stu-id="a3041-136">*newPassword*</span></span> | |
| <span data-ttu-id="a3041-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="a3041-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="a3041-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="a3041-138">*passwordPolicies*</span></span> | <span data-ttu-id="a3041-139">Azure AD B2C Premium toodetermine parola gücünü, sona erme vb. tarafından kullanılan parola ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="a3041-139">Password policies used by Azure AD B2C Premium toodetermine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="a3041-140">*Sub*</span><span class="sxs-lookup"><span data-stu-id="a3041-140">*sub*</span></span> | |
| <span data-ttu-id="a3041-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="a3041-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="a3041-142">*Identityprovider*</span><span class="sxs-lookup"><span data-stu-id="a3041-142">*identityProvider*</span></span> | |
| <span data-ttu-id="a3041-143">*görünen adı*</span><span class="sxs-lookup"><span data-stu-id="a3041-143">*displayName*</span></span> | |
| <span data-ttu-id="a3041-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="a3041-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="a3041-145">Kullanıcının telefon numarası</span><span class="sxs-lookup"><span data-stu-id="a3041-145">User's telephone number</span></span> |
| <span data-ttu-id="a3041-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="a3041-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="a3041-147">*E-posta*</span><span class="sxs-lookup"><span data-stu-id="a3041-147">*email*</span></span> | <span data-ttu-id="a3041-148">Kullanılan toocontact hello kullanıcıya e-posta adresi</span><span class="sxs-lookup"><span data-stu-id="a3041-148">Email address that can be used toocontact hello user</span></span> |
| <span data-ttu-id="a3041-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="a3041-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="a3041-150">Kullanıcı hello e-posta adresi olarak toosign kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="a3041-150">Email address that hello user can use toosign in</span></span> |
| <span data-ttu-id="a3041-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="a3041-151">*otherMails*</span></span> | <span data-ttu-id="a3041-152">Kullanılan toocontact hello kullanıcıya e-posta adresleri</span><span class="sxs-lookup"><span data-stu-id="a3041-152">Email addresses that can be used toocontact hello user</span></span> |
| <span data-ttu-id="a3041-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="a3041-153">*userPrincipalName*</span></span> | <span data-ttu-id="a3041-154">Hello Azure AD B2C Premium depolandığı şekliyle kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="a3041-154">Username as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="a3041-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="a3041-155">*upnUserName*</span></span> | <span data-ttu-id="a3041-156">Kullanıcı asıl adı oluşturmak için kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="a3041-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="a3041-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="a3041-157">*mailNickName*</span></span> | <span data-ttu-id="a3041-158">Hello Azure AD B2C Premium depolandığı şekliyle kullanıcının posta takma adı</span><span class="sxs-lookup"><span data-stu-id="a3041-158">User's mail nick name as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="a3041-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="a3041-159">*newUser*</span></span> | |
| <span data-ttu-id="a3041-160">*yürütülen-SelfAsserted-giriş*</span><span class="sxs-lookup"><span data-stu-id="a3041-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="a3041-161">Talep, öznitelikler hello kullanıcıdan toplanan olup olmadığını belirtir</span><span class="sxs-lookup"><span data-stu-id="a3041-161">Claim that specifies whether attributes were collected from hello user</span></span> |
| <span data-ttu-id="a3041-162">*yürütülen-PhoneFactor-giriş*</span><span class="sxs-lookup"><span data-stu-id="a3041-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="a3041-163">Talep, yeni bir telefon numarası hello kullanıcıdan toplanan olup olmadığını belirtir</span><span class="sxs-lookup"><span data-stu-id="a3041-163">Claim that specifies whether a new phone number was collected from hello user</span></span> |
| <span data-ttu-id="a3041-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="a3041-164">*authenticationSource*</span></span> | <span data-ttu-id="a3041-165">Merhaba kullanıcı sosyal kimlik sağlayıcısı, login.microsoftonline.com veya yerel hesap kimlik doğrulamasının yapıldığı belirtir</span><span class="sxs-lookup"><span data-stu-id="a3041-165">Specifies whether hello user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="a3041-166">Sorgu dizesi parametreleri ve diğer özel parametreler için gereken talepleri</span><span class="sxs-lookup"><span data-stu-id="a3041-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="a3041-167">Merhaba aşağıdaki talep (bazı sorgu dizesi parametreleri de dahil olmak üzere) özel parametreler tooother talep sağlayıcıları gerekli toopass şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a3041-167">hello following claims are required toopass on special parameters (including some query string parameters) tooother claims providers:</span></span>

| <span data-ttu-id="a3041-168">Talep türü</span><span class="sxs-lookup"><span data-stu-id="a3041-168">Claims type</span></span> | <span data-ttu-id="a3041-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3041-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="a3041-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="a3041-170">*nux*</span></span> | <span data-ttu-id="a3041-171">Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="a3041-171">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3041-172">*NCA*</span><span class="sxs-lookup"><span data-stu-id="a3041-172">*nca*</span></span> | <span data-ttu-id="a3041-173">Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="a3041-173">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3041-174">*istemi*</span><span class="sxs-lookup"><span data-stu-id="a3041-174">*prompt*</span></span> | <span data-ttu-id="a3041-175">Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="a3041-175">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3041-176">*Mkt*</span><span class="sxs-lookup"><span data-stu-id="a3041-176">*mkt*</span></span> | <span data-ttu-id="a3041-177">Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="a3041-177">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3041-178">*LC*</span><span class="sxs-lookup"><span data-stu-id="a3041-178">*lc*</span></span> | <span data-ttu-id="a3041-179">Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="a3041-179">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3041-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="a3041-180">*grant_type*</span></span> | <span data-ttu-id="a3041-181">Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="a3041-181">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3041-182">*Kapsam*</span><span class="sxs-lookup"><span data-stu-id="a3041-182">*scope*</span></span> | <span data-ttu-id="a3041-183">Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="a3041-183">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3041-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="a3041-184">*client_id*</span></span> | <span data-ttu-id="a3041-185">Yerel hesap kimlik doğrulaması toologin.microsoftonline.com için geçirilen özel parametresi</span><span class="sxs-lookup"><span data-stu-id="a3041-185">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="a3041-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="a3041-186">*objectIdFromSession*</span></span> | <span data-ttu-id="a3041-187">Parametresi, nesne kimliği hello hello varsayılan oturum yönetimi sağlayıcısı tooindicate tarafından sağlanan bir SSO oturumundan alınan</span><span class="sxs-lookup"><span data-stu-id="a3041-187">Parameter provided by hello default session management provider tooindicate that hello object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="a3041-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="a3041-188">*isActiveMFASession*</span></span> | <span data-ttu-id="a3041-189">Merhaba kullanıcının etkin bir MFA oturumu sahip parametre hello MFA oturum yönetimi tooindicate tarafından sağlanan</span><span class="sxs-lookup"><span data-stu-id="a3041-189">Parameter provided by hello MFA session management tooindicate that hello user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="a3041-190">Toplanabilir ek (isteğe bağlı) talepleri</span><span class="sxs-lookup"><span data-stu-id="a3041-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="a3041-191">Merhaba aşağıdaki hello kullanıcılardan toplanan ek talep hello dizinde saklanan ve hello belirteçte gönderilen talepleri.</span><span class="sxs-lookup"><span data-stu-id="a3041-191">hello following claims are additional claims that can be collected from hello users, stored in hello directory, and sent in hello token.</span></span> <span data-ttu-id="a3041-192">Önce özetlendiği gibi ek talep toothis listesi eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="a3041-192">As outlined before, additional claims can be added toothis list.</span></span>

| <span data-ttu-id="a3041-193">Talep türü</span><span class="sxs-lookup"><span data-stu-id="a3041-193">Claims type</span></span> | <span data-ttu-id="a3041-194">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3041-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="a3041-195">*givenName*</span><span class="sxs-lookup"><span data-stu-id="a3041-195">*givenName*</span></span> | <span data-ttu-id="a3041-196">Kullanıcının verilen adı (ilk adı olarak da bilinir)</span><span class="sxs-lookup"><span data-stu-id="a3041-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="a3041-197">*Soyadı*</span><span class="sxs-lookup"><span data-stu-id="a3041-197">*surname*</span></span> | <span data-ttu-id="a3041-198">Kullanıcının soyadı (Aile adı ve Soyadı olarak da bilinir)</span><span class="sxs-lookup"><span data-stu-id="a3041-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="a3041-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="a3041-199">*Extension_picture*</span></span> | <span data-ttu-id="a3041-200">Sosyal kullanıcının resim</span><span class="sxs-lookup"><span data-stu-id="a3041-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="a3041-201">Talep dönüştürmeleri</span><span class="sxs-lookup"><span data-stu-id="a3041-201">Claim transformations</span></span>

<span data-ttu-id="a3041-202">Merhaba kullanılabilir talep dönüştürmeleri, aşağıda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="a3041-202">hello available claim transformations are listed below.</span></span>

| <span data-ttu-id="a3041-203">Talep dönüştürme</span><span class="sxs-lookup"><span data-stu-id="a3041-203">Claim transformation</span></span> | <span data-ttu-id="a3041-204">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3041-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="a3041-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="a3041-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="a3041-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="a3041-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="a3041-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="a3041-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="a3041-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="a3041-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="a3041-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="a3041-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="a3041-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="a3041-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="a3041-211">İçerik tanımları</span><span class="sxs-lookup"><span data-stu-id="a3041-211">Content definitions</span></span>

<span data-ttu-id="a3041-212">Bu bölümde zaten hello bildirilen hello içerik tanımları açıklanmaktadır *B2C_1A_base* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="a3041-212">This section describes hello content definitions already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="a3041-213">Bu içerik tanımları başvurulan, geçersiz ve/veya kendi ilkelerinizi de olduğu gibi hello gerektiği şekilde genişletilmiş uygulanmadıkça toobe olan *B2C_1A_base_extensions* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="a3041-213">These content definitions are susceptible toobe referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="a3041-214">Talep sağlayıcı</span><span class="sxs-lookup"><span data-stu-id="a3041-214">Claims provider</span></span> | <span data-ttu-id="a3041-215">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3041-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="a3041-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="a3041-216">*Facebook*</span></span> | |
| <span data-ttu-id="a3041-217">*Yerel hesap oturum açma*</span><span class="sxs-lookup"><span data-stu-id="a3041-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="a3041-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="a3041-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="a3041-219">*Azure Active Directory*</span><span class="sxs-lookup"><span data-stu-id="a3041-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="a3041-220">*Kendi kendine uygulanan*</span><span class="sxs-lookup"><span data-stu-id="a3041-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="a3041-221">*Yerel hesap*</span><span class="sxs-lookup"><span data-stu-id="a3041-221">*Local Account*</span></span> | |
| <span data-ttu-id="a3041-222">*Oturum yönetimi*</span><span class="sxs-lookup"><span data-stu-id="a3041-222">*Session Management*</span></span> | |
| <span data-ttu-id="a3041-223">*Trustframework ilke altyapısı*</span><span class="sxs-lookup"><span data-stu-id="a3041-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="a3041-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="a3041-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="a3041-225">*Belirteci veren*</span><span class="sxs-lookup"><span data-stu-id="a3041-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="a3041-226">Teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="a3041-226">Technical profiles</span></span>

<span data-ttu-id="a3041-227">Bu bölümde hello talep sağlayıcısı başına zaten tanımlanmış hello teknik profilleri gösterilmektedir *B2C_1A_base* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="a3041-227">This section depicts hello technical profiles already declared per claim provider in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="a3041-228">Daha fazla başvurulan, geçersiz ve/veya kendi ilkelerinizi de olduğu gibi hello gerektiği şekilde genişletilmiş uygulanmadıkça toobe Bu teknik profillerdir *B2C_1A_base_extensions* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="a3041-228">These technical profiles are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="a3041-229">Facebook için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="a3041-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="a3041-230">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-230">Technical profile</span></span> | <span data-ttu-id="a3041-231">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3041-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3041-232">*Facebook OAUTH*</span><span class="sxs-lookup"><span data-stu-id="a3041-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="a3041-233">Yerel hesap oturum açma için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="a3041-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="a3041-234">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-234">Technical profile</span></span> | <span data-ttu-id="a3041-235">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3041-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3041-236">*Oturum açma etkileşimsiz*</span><span class="sxs-lookup"><span data-stu-id="a3041-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="a3041-237">Telefon faktörü için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="a3041-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="a3041-238">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-238">Technical profile</span></span> | <span data-ttu-id="a3041-239">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3041-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3041-240">*PhoneFactor giriş*</span><span class="sxs-lookup"><span data-stu-id="a3041-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="a3041-241">*PhoneFactor InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="a3041-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="a3041-242">*PhoneFactor doğrulayın*</span><span class="sxs-lookup"><span data-stu-id="a3041-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="a3041-243">Azure Active Directory için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="a3041-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="a3041-244">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-244">Technical profile</span></span> | <span data-ttu-id="a3041-245">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3041-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3041-246">*AAD-genel*</span><span class="sxs-lookup"><span data-stu-id="a3041-246">*AAD-Common*</span></span> | <span data-ttu-id="a3041-247">Teknik profili tarafından dahil hello diğer AAD xxx teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="a3041-247">Technical profile included by hello other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="a3041-248">*AAD UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="a3041-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="a3041-249">Sosyal oturum açma teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="a3041-250">*AAD UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="a3041-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="a3041-251">Sosyal oturum açma teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="a3041-252">*AAD UserReadUsingAlternativeSecurityId NoError*</span><span class="sxs-lookup"><span data-stu-id="a3041-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="a3041-253">Sosyal oturum açma teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="a3041-254">*AAD UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="a3041-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="a3041-255">Yerel hesaplar için teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="a3041-256">*AAD UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="a3041-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="a3041-257">Yerel hesaplar için teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="a3041-258">*AAD UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="a3041-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="a3041-259">ObjectID kullanarak kullanıcı kaydını güncelleştirmek için teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="a3041-260">*AAD UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="a3041-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="a3041-261">ObjectID kullanarak kullanıcı kaydını güncelleştirmek için teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="a3041-262">*AAD UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="a3041-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="a3041-263">ObjectID kullanarak kullanıcı kaydını güncelleştirmek için teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="a3041-264">*AAD UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="a3041-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="a3041-265">Kullanıcı kimlik doğrulaması yaptıktan sonra teknik kullanılan tooread veri profilidir</span><span class="sxs-lookup"><span data-stu-id="a3041-265">Technical profile is used tooread data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="a3041-266">Kendi kendine uygulanan için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="a3041-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="a3041-267">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-267">Technical profile</span></span> | <span data-ttu-id="a3041-268">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3041-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3041-269">*SelfAsserted sosyal*</span><span class="sxs-lookup"><span data-stu-id="a3041-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="a3041-270">*SelfAsserted ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="a3041-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="a3041-271">Yerel hesap için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="a3041-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="a3041-272">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-272">Technical profile</span></span> | <span data-ttu-id="a3041-273">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3041-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3041-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="a3041-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="a3041-275">Oturum yönetimi için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="a3041-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="a3041-276">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-276">Technical profile</span></span> | <span data-ttu-id="a3041-277">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3041-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3041-278">*SM sekmeyi*</span><span class="sxs-lookup"><span data-stu-id="a3041-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="a3041-279">*SM AAD*</span><span class="sxs-lookup"><span data-stu-id="a3041-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="a3041-280">*SM SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="a3041-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="a3041-281">Profil adı yukarı kullanılan toodisambiguate AAD oturum oturum arasında olması ve oturum açın</span><span class="sxs-lookup"><span data-stu-id="a3041-281">Profile name is being used toodisambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="a3041-282">*SM SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="a3041-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="a3041-283">*SM MFA*</span><span class="sxs-lookup"><span data-stu-id="a3041-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="a3041-284">Trustframework ilke altyapısı TechnicalProfiles için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="a3041-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="a3041-285">Hiçbir teknik profilleri Merhaba şu anda tanımlanmış **Trustframework ilke altyapısı TechnicalProfiles** Talep sağlayıcı.</span><span class="sxs-lookup"><span data-stu-id="a3041-285">Currently, no technical profiles are defined for hello **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="a3041-286">Belirteç Verenin için teknik profilleri</span><span class="sxs-lookup"><span data-stu-id="a3041-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="a3041-287">Teknik profili</span><span class="sxs-lookup"><span data-stu-id="a3041-287">Technical profile</span></span> | <span data-ttu-id="a3041-288">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3041-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="a3041-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="a3041-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="a3041-290">Kullanıcı Yolculuklar</span><span class="sxs-lookup"><span data-stu-id="a3041-290">User journeys</span></span>

<span data-ttu-id="a3041-291">Bu bölümde zaten hello bildirilen hello kullanıcı Yolculuklar gösterilmektedir *B2C_1A_base* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="a3041-291">This section depicts hello user journeys already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="a3041-292">Bu kullanıcı Yolculuklar daha fazla başvurulan, geçersiz ve/veya kendi ilkelerinizi de olduğu gibi hello gerektiği şekilde genişletilmiş uygulanmadıkça toobe olan *B2C_1A_base_extensions* ilkesi.</span><span class="sxs-lookup"><span data-stu-id="a3041-292">These user journeys are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="a3041-293">Kullanıcı gezisine</span><span class="sxs-lookup"><span data-stu-id="a3041-293">User journey</span></span> | <span data-ttu-id="a3041-294">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3041-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="a3041-295">*Kaydolma*</span><span class="sxs-lookup"><span data-stu-id="a3041-295">*SignUp*</span></span> | |
| <span data-ttu-id="a3041-296">*Oturum açma*</span><span class="sxs-lookup"><span data-stu-id="a3041-296">*SignIn*</span></span> | |
| <span data-ttu-id="a3041-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="a3041-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="a3041-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="a3041-298">*EditProfile*</span></span> | |
| <span data-ttu-id="a3041-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="a3041-299">*PasswordReset*</span></span> | |
