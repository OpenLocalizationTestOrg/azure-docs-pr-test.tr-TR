---
title: "Azure Active Directory'de yapılandırılabilir belirteci ömürleri | Microsoft Docs"
description: "Azure AD tarafından yayınlanan belirteçleri için yaşam süresi ayarlamak öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 06f5b317-053e-44c3-aaaa-cf07d8692735
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: billmath
ms.custom: aaddev
ms.reviewer: anchitn
ms.openlocfilehash: d23721eba308096a05211eb6e26e1338a69cae0c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="configurable-token-lifetimes-in-azure-active-directory-public-preview"></a><span data-ttu-id="4459a-103">Azure Active Directory'de (genel Önizleme) yapılandırılabilir belirteci yaşam süresi</span><span class="sxs-lookup"><span data-stu-id="4459a-103">Configurable token lifetimes in Azure Active Directory (Public Preview)</span></span>
<span data-ttu-id="4459a-104">Azure Active Directory (Azure AD) tarafından verilmiş bir belirteç ömrü belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-104">You can specify the lifetime of a token issued by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="4459a-105">Kuruluşunuzdaki tüm uygulamalar, kuruluşunuzda, çok kiracılı (çok kuruluş) uygulama veya belirli hizmet sorumlusu belirteci yaşam süresi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-105">You can set token lifetimes for all apps in your organization, for a multi-tenant (multi-organization) application, or for a specific service principal in your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="4459a-106">Bu özellik şu anda genel önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="4459a-106">This capability currently is in Public Preview.</span></span> <span data-ttu-id="4459a-107">Geri veya herhangi bir değişiklik kaldırmak hazırlıklı olun.</span><span class="sxs-lookup"><span data-stu-id="4459a-107">Be prepared to revert or remove any changes.</span></span> <span data-ttu-id="4459a-108">Genel Önizleme sırasında herhangi bir Azure Active Directory Abonelik özelliği kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-108">The feature is available in any Azure Active Directory subscription during Public Preview.</span></span> <span data-ttu-id="4459a-109">Ancak, özelliği genel kullanıma sunulduğunda özelliği bazı yönlerini gerektirebilir bir [Azure Active Directory Premium](active-directory-get-started-premium.md) abonelik.</span><span class="sxs-lookup"><span data-stu-id="4459a-109">However, when the feature becomes generally available, some aspects of the feature might require an [Azure Active Directory Premium](active-directory-get-started-premium.md) subscription.</span></span>
>
>

<span data-ttu-id="4459a-110">Azure AD'de bireysel uygulamaları ya da bir kuruluşta tüm uygulamaları zorlanan kuralları kümesi bir ilke nesnesi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="4459a-110">In Azure AD, a policy object represents a set of rules that are enforced on individual applications or on all applications in an organization.</span></span> <span data-ttu-id="4459a-111">Her ilke türü bir benzersiz yapısıyla atanmış olan nesnelere uygulanan özellikler kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="4459a-111">Each policy type has a unique structure, with a set of properties that are applied to objects to which they are assigned.</span></span>

<span data-ttu-id="4459a-112">Bir ilke, kuruluşunuz için varsayılan ilke olarak belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-112">You can designate a policy as the default policy for your organization.</span></span> <span data-ttu-id="4459a-113">Yüksek önceliğe sahip bir ilke tarafından kılınmayan sürece kuruluştaki herhangi bir uygulama ilkesi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-113">The policy is applied to any application in the organization, as long as it is not overridden by a policy with a higher priority.</span></span> <span data-ttu-id="4459a-114">Ayrıca, belirli uygulamalar için bir ilke atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-114">You also can assign a policy to specific applications.</span></span> <span data-ttu-id="4459a-115">Öncelik sırasını ilke türüne göre değişir.</span><span class="sxs-lookup"><span data-stu-id="4459a-115">The order of priority varies by policy type.</span></span>


## <a name="token-types"></a><span data-ttu-id="4459a-116">Belirteç türleri</span><span class="sxs-lookup"><span data-stu-id="4459a-116">Token types</span></span>

<span data-ttu-id="4459a-117">Yenileme belirteçleri, erişim belirteçleri, oturum belirteçleri ve kimlik belirteçlerini belirteç ömrü ilkelerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-117">You can set token lifetime policies for refresh tokens, access tokens, session tokens, and ID tokens.</span></span>

### <a name="access-tokens"></a><span data-ttu-id="4459a-118">Erişim belirteçleri</span><span class="sxs-lookup"><span data-stu-id="4459a-118">Access tokens</span></span>
<span data-ttu-id="4459a-119">İstemciler, korunan bir kaynağa erişmek için erişim belirteçleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="4459a-119">Clients use access tokens to access a protected resource.</span></span> <span data-ttu-id="4459a-120">Bir erişim belirteci, kullanıcı, istemci ve kaynak yalnızca belirli bir birleşim için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-120">An access token can be used only for a specific combination of user, client, and resource.</span></span> <span data-ttu-id="4459a-121">Erişim belirteci iptal edilemiyor ve bunların süre sonu kadar geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="4459a-121">Access tokens cannot be revoked and are valid until their expiry.</span></span> <span data-ttu-id="4459a-122">Bir erişim belirteci elde kötü amaçlı bir aktör yaşam uzantı için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-122">A malicious actor that has obtained an access token can use it for extent of its lifetime.</span></span> <span data-ttu-id="4459a-123">Bir erişim belirteci ömrü ayarlama sistem performansını artırmak ve kullanıcı hesabının devre dışı bırakıldıktan sonra istemci erişimi korur süre miktarını artırmayı arasında bir denge olur.</span><span class="sxs-lookup"><span data-stu-id="4459a-123">Adjusting the lifetime of an access token is a trade-off between improving system performance and increasing the amount of time that the client retains access after the user’s account is disabled.</span></span> <span data-ttu-id="4459a-124">Geliştirilmiş sistem performansı kez bir istemci yeni bir erişim belirteci alması gerekiyor sayısını azaltarak elde edilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-124">Improved system performance is achieved by reducing the number of times a client needs to acquire a fresh access token.</span></span>

### <a name="refresh-tokens"></a><span data-ttu-id="4459a-125">Yenileme belirteçlerini</span><span class="sxs-lookup"><span data-stu-id="4459a-125">Refresh tokens</span></span>
<span data-ttu-id="4459a-126">Bir istemci korunan bir kaynağa erişmek için bir erişim belirteci yaptığında, istemci bir yenileme belirteci ve bir erişim belirteci alır.</span><span class="sxs-lookup"><span data-stu-id="4459a-126">When a client acquires an access token to access a protected resource, the client receives both a refresh token and an access token.</span></span> <span data-ttu-id="4459a-127">Yenileme belirteci geçerli erişim belirtecinin süresi dolduğunda yeni erişim/yenileme belirteci çiftleri elde etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4459a-127">The refresh token is used to obtain new access/refresh token pairs when the current access token expires.</span></span> <span data-ttu-id="4459a-128">Bir yenileme belirteci birleşimi kullanıcı ve istemci bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4459a-128">A refresh token is bound to a combination of user and client.</span></span> <span data-ttu-id="4459a-129">Bir yenileme belirteci iptal edilebilir ve belirteç her kullanılışında belirtecin geçerlilik denetlenir.</span><span class="sxs-lookup"><span data-stu-id="4459a-129">A refresh token can be revoked, and the token's validity is checked every time the token is used.</span></span>

<span data-ttu-id="4459a-130">Özel ve ortak istemciler arasında ayrım yapmak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="4459a-130">It's important to make a distinction between confidential clients and public clients.</span></span> <span data-ttu-id="4459a-131">Farklı istemci türleri hakkında daha fazla bilgi için bkz: [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1).</span><span class="sxs-lookup"><span data-stu-id="4459a-131">For more information about different types of clients, see [RFC 6749](https://tools.ietf.org/html/rfc6749#section-2.1).</span></span>

#### <a name="token-lifetimes-with-confidential-client-refresh-tokens"></a><span data-ttu-id="4459a-132">Gizli istemci yenileme belirteçleri ile belirteci yaşam süresi</span><span class="sxs-lookup"><span data-stu-id="4459a-132">Token lifetimes with confidential client refresh tokens</span></span>
<span data-ttu-id="4459a-133">Gizli istemcileri güvenli bir şekilde bir istemci parolası (gizli) depolayabilirsiniz uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="4459a-133">Confidential clients are applications that can securely store a client password (secret).</span></span> <span data-ttu-id="4459a-134">İsteklerin istemci uygulamasından ve kötü amaçlı aktör değil, geldiğini kanıtlarlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-134">They can prove that requests are coming from the client application and not from a malicious actor.</span></span> <span data-ttu-id="4459a-135">Örneğin, bir web uygulaması web sunucusunda bir istemci parolası depolayabileceğiniz gizli bir istemcidir.</span><span class="sxs-lookup"><span data-stu-id="4459a-135">For example, a web app is a confidential client because it can store a client secret on the web server.</span></span> <span data-ttu-id="4459a-136">Bu açık değil.</span><span class="sxs-lookup"><span data-stu-id="4459a-136">It is not exposed.</span></span> <span data-ttu-id="4459a-137">Bu akışlar daha güvenlidir, yenileme belirteçleri bu akışlara verilen varsayılan ömrü çünkü `until-revoked`İlkesi kullanılarak değiştirilemez ve gönüllü parola sıfırlama üzerinde iptal değil.</span><span class="sxs-lookup"><span data-stu-id="4459a-137">Because these flows are more secure, the default lifetimes of refresh tokens issued to these flows is `until-revoked`, cannot be changed by using policy, and will not be revoked on voluntary password resets.</span></span>

#### <a name="token-lifetimes-with-public-client-refresh-tokens"></a><span data-ttu-id="4459a-138">Ortak istemci yenileme belirteçleri ile belirteci yaşam süresi</span><span class="sxs-lookup"><span data-stu-id="4459a-138">Token lifetimes with public client refresh tokens</span></span>

<span data-ttu-id="4459a-139">Ortak istemcileri güvenli bir şekilde bir istemci parolası (gizli) depolanamıyor.</span><span class="sxs-lookup"><span data-stu-id="4459a-139">Public clients cannot securely store a client password (secret).</span></span> <span data-ttu-id="4459a-140">Örneğin, ortak bir istemci olarak kabul edilir şekilde iOS/Android uygulama gizli anahtarı kaynak sahibinden belirsizleştirirseniz olamaz.</span><span class="sxs-lookup"><span data-stu-id="4459a-140">For example, an iOS/Android app cannot obfuscate a secret from the resource owner, so it is considered a public client.</span></span> <span data-ttu-id="4459a-141">İlkeleri yenileme belirteçleri belirtilen süresinden daha eski ortak istemcilerden gelen yeni bir erişim/yenileme belirteci çifti ele geçirmesini önlemek için kaynak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-141">You can set policies on resources to prevent refresh tokens from public clients older than a specified period from obtaining a new access/refresh token pair.</span></span> <span data-ttu-id="4459a-142">(Bunu yapmak için yenileme belirteci etkin olmayan zaman sınırı özelliğini kullanın.) Sonrasında artık yenileme belirteçleri kabul süresini ayarlamak için ilkelerini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-142">(To do this, use the Refresh Token Max Inactive Time property.) You also can use policies to set a period beyond which the refresh tokens are no longer accepted.</span></span> <span data-ttu-id="4459a-143">(Bunu yapmak için yenileme belirteci Maksimum yaş özelliğini kullanın.) Zaman ve ne sıklıkta kullanıcının sessiz bir şekilde, bir ortak istemci uygulamasını kullanırken, yeniden kimlik doğrulaması yerine kimlik bilgilerinizi yeniden girmeniz gerekir denetlemek için bir yenileme belirteci ömrü ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-143">(To do this, use the Refresh Token Max Age property.) You can adjust the lifetime of a refresh token to control when and how often the user is required to reenter credentials, instead of being silently reauthenticated, when using a public client application.</span></span>

### <a name="id-tokens"></a><span data-ttu-id="4459a-144">Kimliği belirteçleri</span><span class="sxs-lookup"><span data-stu-id="4459a-144">ID tokens</span></span>
<span data-ttu-id="4459a-145">Kimlik belirteçlerini Web siteleri ve yerel istemcilerine geçirilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-145">ID tokens are passed to websites and native clients.</span></span> <span data-ttu-id="4459a-146">Kimlik belirteçlerini bir kullanıcı profili bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="4459a-146">ID tokens contain profile information about a user.</span></span> <span data-ttu-id="4459a-147">Bir kimliği belirteci kullanıcı ve istemci belirli bir birleşim bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4459a-147">An ID token is bound to a specific combination of user and client.</span></span> <span data-ttu-id="4459a-148">Kimlik belirteçlerini kendi süre sonu kadar geçerli kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-148">ID tokens are considered valid until their expiry.</span></span> <span data-ttu-id="4459a-149">Genellikle, bir kullanıcının bir web uygulaması eşleşip kimliği belirteç ömrü için uygulamada oturum yaşam kullanıcı için verilen.</span><span class="sxs-lookup"><span data-stu-id="4459a-149">Usually, a web application matches a user’s session lifetime in the application to the lifetime of the ID token issued for the user.</span></span> <span data-ttu-id="4459a-150">Ne sıklıkta web uygulaması uygulama oturum sona erer ve ne sıklıkta Azure AD ile (Sessiz veya etkileşimli) kimliğinin yeniden doğrulanması kullanıcının gerektiren denetlemek için bir kimliği belirteç ömrü ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-150">You can adjust the lifetime of an ID token to control how often the web application expires the application session, and how often it requires the user to be reauthenticated with Azure AD (either silently or interactively).</span></span>

### <a name="single-sign-on-session-tokens"></a><span data-ttu-id="4459a-151">Tek oturum açma oturumu belirteçleri</span><span class="sxs-lookup"><span data-stu-id="4459a-151">Single sign-on session tokens</span></span>
<span data-ttu-id="4459a-152">Ne zaman bir kullanıcı Azure AD ile doğrular ve seçer **Oturumumu açık bırak** onay kutusu, bir tek oturum açma (SSO) kullanıcının tarayıcı ve Azure AD ile oturumun.</span><span class="sxs-lookup"><span data-stu-id="4459a-152">When a user authenticates with Azure AD and selects the **Keep me signed in** check box, a single sign-on session (SSO) is established with the user’s browser and Azure AD.</span></span> <span data-ttu-id="4459a-153">Bir tanımlama bilgisi biçiminde SSO belirtecin bu oturumu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="4459a-153">The SSO token, in the form of a cookie, represents this session.</span></span> <span data-ttu-id="4459a-154">SSO Oturum belirteci bir belirli bir kaynak/istemci uygulaması ilişkilendirilmediğinden unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4459a-154">Note that the SSO session token is not bound to a specific resource/client application.</span></span> <span data-ttu-id="4459a-155">SSO oturum belirteçleri iptal edilebilir ve kullanıldıkları her zaman geçerliliği denetlenir.</span><span class="sxs-lookup"><span data-stu-id="4459a-155">SSO session tokens can be revoked, and their validity is checked every time they are used.</span></span>

<span data-ttu-id="4459a-156">Azure AD iki tür SSO oturum belirteçleri kullanır: kalıcı ve kalıcı olmayan.</span><span class="sxs-lookup"><span data-stu-id="4459a-156">Azure AD uses two kinds of SSO session tokens: persistent and nonpersistent.</span></span> <span data-ttu-id="4459a-157">Kalıcı oturum belirteç kalıcı tanımlama bilgileri tarayıcı tarafından depolanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-157">Persistent session tokens are stored as persistent cookies by the browser.</span></span> <span data-ttu-id="4459a-158">Kalıcı olmayan oturum belirteç oturum tanımlama bilgileri depolanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-158">Nonpersistent session tokens are stored as session cookies.</span></span> <span data-ttu-id="4459a-159">(Tarayıcı kapatıldığında oturum tanımlama bilgileri yok.)</span><span class="sxs-lookup"><span data-stu-id="4459a-159">(Session cookies are destroyed when the browser is closed.)</span></span>

<span data-ttu-id="4459a-160">Kalıcı olmayan oturum belirteçleri 24 saatlik bir ömrü vardır.</span><span class="sxs-lookup"><span data-stu-id="4459a-160">Nonpersistent session tokens have a lifetime of 24 hours.</span></span> <span data-ttu-id="4459a-161">Kalıcı belirteçleri 180 gün ömrü vardır.</span><span class="sxs-lookup"><span data-stu-id="4459a-161">Persistent tokens have a lifetime of 180 days.</span></span> <span data-ttu-id="4459a-162">SSO Oturum belirteci, geçerlilik süresi içinde kullanılan dilediğiniz zaman, başka bir 24 saat veya belirteç türüne bağlı olarak 180 gün geçerlilik süresini genişletilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-162">Any time an SSO session token is used within its validity period, the validity period is extended another 24 hours or 180 days, depending on the token type.</span></span> <span data-ttu-id="4459a-163">SSO Oturum belirteci, geçerlilik süresi içinde kullanılmazsa, olarak kabul süresi doldu ve artık kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-163">If an SSO session token is not used within its validity period, it is considered expired and is no longer accepted.</span></span>

<span data-ttu-id="4459a-164">İlk oturum belirteci hangi Oturum belirteci artık kabul edilen ötesinde verilmiş sonra süresini ayarlamak için bir ilke kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-164">You can use a policy to set the time after the first session token was issued beyond which the session token is no longer accepted.</span></span> <span data-ttu-id="4459a-165">(Bunu yapmak için oturum belirteci Maksimum yaş özelliğini kullanın.) Zaman ve ne sıklıkta bir kullanıcı sessiz bir şekilde, bir web uygulaması kullanırken kimlik doğrulaması gerçekleştirilen yerine kimlik bilgilerinizi yeniden girmeniz gereken denetlemek için bir oturum belirteci ömrü ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-165">(To do this, use the Session Token Max Age property.) You can adjust the lifetime of a session token to control when and how often a user is required to reenter credentials, instead of being silently authenticated, when using a web application.</span></span>

### <a name="token-lifetime-policy-properties"></a><span data-ttu-id="4459a-166">Belirteç ömrü ilkesi özellikleri</span><span class="sxs-lookup"><span data-stu-id="4459a-166">Token lifetime policy properties</span></span>
<span data-ttu-id="4459a-167">Belirteç ömrü ilkesi, belirteç ömrü kuralları içeren ilke nesne türüdür.</span><span class="sxs-lookup"><span data-stu-id="4459a-167">A token lifetime policy is a type of policy object that contains token lifetime rules.</span></span> <span data-ttu-id="4459a-168">Belirtilen belirteç yaşam süreleri denetlemek için bir ilkenin özelliklerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4459a-168">Use the properties of the policy to control specified token lifetimes.</span></span> <span data-ttu-id="4459a-169">Hiçbir ilke ayarlanırsa, sistem varsayılan yaşam süresi değeri zorlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-169">If no policy is set, the system enforces the default lifetime value.</span></span>

### <a name="configurable-token-lifetime-properties"></a><span data-ttu-id="4459a-170">Yapılandırılabilir belirteç ömrü özellikleri</span><span class="sxs-lookup"><span data-stu-id="4459a-170">Configurable token lifetime properties</span></span>
| <span data-ttu-id="4459a-171">Özellik</span><span class="sxs-lookup"><span data-stu-id="4459a-171">Property</span></span> | <span data-ttu-id="4459a-172">İlke özellik dizesi</span><span class="sxs-lookup"><span data-stu-id="4459a-172">Policy property string</span></span> | <span data-ttu-id="4459a-173">Etkiler</span><span class="sxs-lookup"><span data-stu-id="4459a-173">Affects</span></span> | <span data-ttu-id="4459a-174">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="4459a-174">Default</span></span> | <span data-ttu-id="4459a-175">Minimum</span><span class="sxs-lookup"><span data-stu-id="4459a-175">Minimum</span></span> | <span data-ttu-id="4459a-176">Maksimum</span><span class="sxs-lookup"><span data-stu-id="4459a-176">Maximum</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="4459a-177">Erişim belirteci ömrü</span><span class="sxs-lookup"><span data-stu-id="4459a-177">Access Token Lifetime</span></span> |<span data-ttu-id="4459a-178">AccessTokenLifetime</span><span class="sxs-lookup"><span data-stu-id="4459a-178">AccessTokenLifetime</span></span> |<span data-ttu-id="4459a-179">Erişim belirteçleri, kimlik belirteçlerini, SAML2 belirteçleri</span><span class="sxs-lookup"><span data-stu-id="4459a-179">Access tokens, ID tokens, SAML2 tokens</span></span> |<span data-ttu-id="4459a-180">1 saat</span><span class="sxs-lookup"><span data-stu-id="4459a-180">1 hour</span></span> |<span data-ttu-id="4459a-181">10 dakika</span><span class="sxs-lookup"><span data-stu-id="4459a-181">10 minutes</span></span> |<span data-ttu-id="4459a-182">1 gün</span><span class="sxs-lookup"><span data-stu-id="4459a-182">1 day</span></span> |
| <span data-ttu-id="4459a-183">Etkin olmayan zaman belirteci sınırı Yenile</span><span class="sxs-lookup"><span data-stu-id="4459a-183">Refresh Token Max Inactive Time</span></span> |<span data-ttu-id="4459a-184">MaxInactiveTime</span><span class="sxs-lookup"><span data-stu-id="4459a-184">MaxInactiveTime</span></span> |<span data-ttu-id="4459a-185">Yenileme belirteçlerini</span><span class="sxs-lookup"><span data-stu-id="4459a-185">Refresh tokens</span></span> |<span data-ttu-id="4459a-186">14 gün</span><span class="sxs-lookup"><span data-stu-id="4459a-186">14 days</span></span> |<span data-ttu-id="4459a-187">10 dakika</span><span class="sxs-lookup"><span data-stu-id="4459a-187">10 minutes</span></span> |<span data-ttu-id="4459a-188">90 gün</span><span class="sxs-lookup"><span data-stu-id="4459a-188">90 days</span></span> |
| <span data-ttu-id="4459a-189">Tek Faktörlü yenileme belirteci Maksimum yaş</span><span class="sxs-lookup"><span data-stu-id="4459a-189">Single-Factor Refresh Token Max Age</span></span> |<span data-ttu-id="4459a-190">MaxAgeSingleFactor</span><span class="sxs-lookup"><span data-stu-id="4459a-190">MaxAgeSingleFactor</span></span> |<span data-ttu-id="4459a-191">Yenileme belirteçlerini (tüm kullanıcılar için)</span><span class="sxs-lookup"><span data-stu-id="4459a-191">Refresh tokens (for any users)</span></span> |<span data-ttu-id="4459a-192">Kadar iptal</span><span class="sxs-lookup"><span data-stu-id="4459a-192">Until-revoked</span></span> |<span data-ttu-id="4459a-193">10 dakika</span><span class="sxs-lookup"><span data-stu-id="4459a-193">10 minutes</span></span> |<span data-ttu-id="4459a-194">Kadar iptal<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="4459a-194">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="4459a-195">Çok faktörlü yenileme belirteci Maksimum yaş</span><span class="sxs-lookup"><span data-stu-id="4459a-195">Multi-Factor Refresh Token Max Age</span></span> |<span data-ttu-id="4459a-196">MaxAgeMultiFactor</span><span class="sxs-lookup"><span data-stu-id="4459a-196">MaxAgeMultiFactor</span></span> |<span data-ttu-id="4459a-197">Yenileme belirteçlerini (tüm kullanıcılar için)</span><span class="sxs-lookup"><span data-stu-id="4459a-197">Refresh tokens (for any users)</span></span> |<span data-ttu-id="4459a-198">Kadar iptal</span><span class="sxs-lookup"><span data-stu-id="4459a-198">Until-revoked</span></span> |<span data-ttu-id="4459a-199">10 dakika</span><span class="sxs-lookup"><span data-stu-id="4459a-199">10 minutes</span></span> |<span data-ttu-id="4459a-200">Kadar iptal<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="4459a-200">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="4459a-201">Tek Faktörlü Oturum belirteci Maksimum yaş</span><span class="sxs-lookup"><span data-stu-id="4459a-201">Single-Factor Session Token Max Age</span></span> |<span data-ttu-id="4459a-202">MaxAgeSessionSingleFactor<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="4459a-202">MaxAgeSessionSingleFactor<sup>2</sup></span></span> |<span data-ttu-id="4459a-203">Oturum belirteçleri (kalıcı ve kalıcı olmayan)</span><span class="sxs-lookup"><span data-stu-id="4459a-203">Session tokens (persistent and nonpersistent)</span></span> |<span data-ttu-id="4459a-204">Kadar iptal</span><span class="sxs-lookup"><span data-stu-id="4459a-204">Until-revoked</span></span> |<span data-ttu-id="4459a-205">10 dakika</span><span class="sxs-lookup"><span data-stu-id="4459a-205">10 minutes</span></span> |<span data-ttu-id="4459a-206">Kadar iptal<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="4459a-206">Until-revoked<sup>1</sup></span></span> |
| <span data-ttu-id="4459a-207">Çok faktörlü Oturum belirteci Maksimum yaş</span><span class="sxs-lookup"><span data-stu-id="4459a-207">Multi-Factor Session Token Max Age</span></span> |<span data-ttu-id="4459a-208">MaxAgeSessionMultiFactor<sup>3</sup></span><span class="sxs-lookup"><span data-stu-id="4459a-208">MaxAgeSessionMultiFactor<sup>3</sup></span></span> |<span data-ttu-id="4459a-209">Oturum belirteçleri (kalıcı ve kalıcı olmayan)</span><span class="sxs-lookup"><span data-stu-id="4459a-209">Session tokens (persistent and nonpersistent)</span></span> |<span data-ttu-id="4459a-210">Kadar iptal</span><span class="sxs-lookup"><span data-stu-id="4459a-210">Until-revoked</span></span> |<span data-ttu-id="4459a-211">10 dakika</span><span class="sxs-lookup"><span data-stu-id="4459a-211">10 minutes</span></span> |<span data-ttu-id="4459a-212">Kadar iptal<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="4459a-212">Until-revoked<sup>1</sup></span></span> |

* <span data-ttu-id="4459a-213"><sup>1</sup>365 gündür bu öznitelikler için ayarlanabilir en fazla açık uzunluğu.</span><span class="sxs-lookup"><span data-stu-id="4459a-213"><sup>1</sup>365 days is the maximum explicit length that can be set for these attributes.</span></span>
* <span data-ttu-id="4459a-214"><sup>2</sup>varsa **MaxAgeSessionSingleFactor** ayarlanmazsa bu değeri alır **MaxAgeSingleFactor** değeri.</span><span class="sxs-lookup"><span data-stu-id="4459a-214"><sup>2</sup>If  **MaxAgeSessionSingleFactor** is not set, this value takes the **MaxAgeSingleFactor** value.</span></span> <span data-ttu-id="4459a-215">Hiçbir parametre ayarlanırsa, varsayılan değer (kadar iptal edilen) özelliği alır.</span><span class="sxs-lookup"><span data-stu-id="4459a-215">If neither parameter is set, the property takes the default value (until-revoked).</span></span>
* <span data-ttu-id="4459a-216"><sup>3</sup>varsa **MaxAgeSessionMultiFactor** ayarlanmazsa bu değeri alır **MaxAgeMultiFactor** değeri.</span><span class="sxs-lookup"><span data-stu-id="4459a-216"><sup>3</sup>If  **MaxAgeSessionMultiFactor** is not set, this value takes the **MaxAgeMultiFactor** value.</span></span> <span data-ttu-id="4459a-217">Hiçbir parametre ayarlanırsa, varsayılan değer (kadar iptal edilen) özelliği alır.</span><span class="sxs-lookup"><span data-stu-id="4459a-217">If neither parameter is set, the property takes the default value (until-revoked).</span></span>

### <a name="exceptions"></a><span data-ttu-id="4459a-218">Özel durumlar</span><span class="sxs-lookup"><span data-stu-id="4459a-218">Exceptions</span></span>
| <span data-ttu-id="4459a-219">Özellik</span><span class="sxs-lookup"><span data-stu-id="4459a-219">Property</span></span> | <span data-ttu-id="4459a-220">Etkiler</span><span class="sxs-lookup"><span data-stu-id="4459a-220">Affects</span></span> | <span data-ttu-id="4459a-221">Varsayılan</span><span class="sxs-lookup"><span data-stu-id="4459a-221">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4459a-222">Belirteç Maksimum yaş Yenile (yetersiz iptal bilgilerini federe kullanıcılar için verilen<sup>1</sup>)</span><span class="sxs-lookup"><span data-stu-id="4459a-222">Refresh Token Max Age (issued for federated users who have insufficient revocation information<sup>1</sup>)</span></span> |<span data-ttu-id="4459a-223">Yenileme belirteçlerini (yetersiz iptal bilgilerini federe kullanıcılar için verilen<sup>1</sup>)</span><span class="sxs-lookup"><span data-stu-id="4459a-223">Refresh tokens (issued for federated users who have insufficient revocation information<sup>1</sup>)</span></span> |<span data-ttu-id="4459a-224">12 saat</span><span class="sxs-lookup"><span data-stu-id="4459a-224">12 hours</span></span> |
| <span data-ttu-id="4459a-225">Belirteç etkin olmayan (gizli istemcileri için verilen) zaman sınırı Yenile</span><span class="sxs-lookup"><span data-stu-id="4459a-225">Refresh Token Max Inactive Time (issued for confidential clients)</span></span> |<span data-ttu-id="4459a-226">Yenileme belirteçlerini (gizli istemcileri için verilen)</span><span class="sxs-lookup"><span data-stu-id="4459a-226">Refresh tokens (issued for confidential clients)</span></span> |<span data-ttu-id="4459a-227">90 gün</span><span class="sxs-lookup"><span data-stu-id="4459a-227">90 days</span></span> |
| <span data-ttu-id="4459a-228">Belirteç Maksimum yaş (gizli istemcileri için verilen) Yenile</span><span class="sxs-lookup"><span data-stu-id="4459a-228">Refresh Token Max Age (issued for confidential clients)</span></span> |<span data-ttu-id="4459a-229">Yenileme belirteçlerini (gizli istemcileri için verilen)</span><span class="sxs-lookup"><span data-stu-id="4459a-229">Refresh tokens (issued for confidential clients)</span></span> |<span data-ttu-id="4459a-230">Kadar iptal</span><span class="sxs-lookup"><span data-stu-id="4459a-230">Until-revoked</span></span> |

* <span data-ttu-id="4459a-231"><sup>1</sup>yetersiz iptal bilgilerini sahip federe kullanıcılar eşitlenen "LastPasswordChangeTimestamp" özniteliğine sahip olmayan tüm kullanıcıları içerir.</span><span class="sxs-lookup"><span data-stu-id="4459a-231"><sup>1</sup>Federated users who have insufficient revocation information include any users who do not have the "LastPasswordChangeTimestamp" attribute synced.</span></span> <span data-ttu-id="4459a-232">AAD eski bir kimlik bilgisi (örneğin, değiştirilmiş bir parola) bağlıdır ve daha sık ilişkilendirilmiş belirteçleri ve kullanıcı yine de iyi yeri olduğundan emin olmak için geri denetlemelidir belirteçleri iptal etmek ne zaman doğrulayamadı olduğu için bu kullanıcılara bu kısa Maksimum yaş verilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-232">These users are given this short Max Age because AAD is unable to verify when to revoke tokens that are tied to an old credential (such as a password that has been changed) and must check back in more frequently to ensure that the user and associated tokens are still in good standing.</span></span> <span data-ttu-id="4459a-233">Bu deneyimini geliştirmek için Kiracı yöneticileri (Bu Powershell kullanarak kullanıcı nesnesindeki veya Modu'nu aracılığıyla ayarlanabilir) "LastPasswordChangeTimestamp" özniteliği eşitleniyor emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4459a-233">To improve this experience, tenant admins must ensure that they are syncing the “LastPasswordChangeTimestamp” attribute (this can be set on the user object using Powershell or through AADSync).</span></span>

### <a name="policy-evaluation-and-prioritization"></a><span data-ttu-id="4459a-234">İlke değerlendirmesi ve öncelik belirleme</span><span class="sxs-lookup"><span data-stu-id="4459a-234">Policy evaluation and prioritization</span></span>
<span data-ttu-id="4459a-235">Oluşturma ve bir belirteç ömrü ilkesi belirli bir uygulama, kuruluşunuz ve hizmet asıl adı atayın.</span><span class="sxs-lookup"><span data-stu-id="4459a-235">You can create and then assign a token lifetime policy to a specific application, to your organization, and to service principals.</span></span> <span data-ttu-id="4459a-236">Birden çok ilke belirli bir uygulama için geçerli.</span><span class="sxs-lookup"><span data-stu-id="4459a-236">Multiple policies might apply to a specific application.</span></span> <span data-ttu-id="4459a-237">Etkinleşir belirteç ömrü ilkesi bu kurallar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="4459a-237">The token lifetime policy that takes effect follows these rules:</span></span>

* <span data-ttu-id="4459a-238">Bir ilke açıkça hizmet sorumlusu atanmışsa zorlanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-238">If a policy is explicitly assigned to the service principal, it is enforced.</span></span>
* <span data-ttu-id="4459a-239">İlke yok açıkça hizmet sorumlusu atanırsa, açıkça hizmet sorumlusu üst kuruluşa atanan bir ilke uygulanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-239">If no policy is explicitly assigned to the service principal, a policy explicitly assigned to the parent organization of the service principal is enforced.</span></span>
* <span data-ttu-id="4459a-240">İlke yok açıkça hizmet sorumlusu veya kuruluş atanırsa, uygulamaya atanan ilkesi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-240">If no policy is explicitly assigned to the service principal or to the organization, the policy assigned to the application is enforced.</span></span>
* <span data-ttu-id="4459a-241">Hizmet sorumlusu, kuruluş veya uygulama nesnesi hiçbir ilke atanmışsa, varsayılan değerleri zorlanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-241">If no policy has been assigned to the service principal, the organization, or the application object, the default values is enforced.</span></span> <span data-ttu-id="4459a-242">(Bölümündeki tabloya bakın [yapılandırılabilir belirteç ömrü özellikleri](#configurable-token-lifetime-properties).)</span><span class="sxs-lookup"><span data-stu-id="4459a-242">(See the table in [Configurable token lifetime properties](#configurable-token-lifetime-properties).)</span></span>

<span data-ttu-id="4459a-243">Uygulama nesneleri ve hizmet asıl nesneleri arasındaki ilişki hakkında daha fazla bilgi için bkz: [uygulama ve hizmet asıl nesneler Azure Active Directory'de](active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="4459a-243">For more information about the relationship between application objects and service principal objects, see [Application and service principal objects in Azure Active Directory](active-directory-application-objects.md).</span></span>

<span data-ttu-id="4459a-244">Bir belirtecin geçerlilik belirteç kullanıldığında değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-244">A token’s validity is evaluated at the time the token is used.</span></span> <span data-ttu-id="4459a-245">Erişiliyor uygulama üzerinde en yüksek öncelikli ilke etkili olur.</span><span class="sxs-lookup"><span data-stu-id="4459a-245">The policy with the highest priority on the application that is being accessed takes effect.</span></span>

> [!NOTE]
> <span data-ttu-id="4459a-246">Burada, örnek bir senaryo verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4459a-246">Here's an example scenario.</span></span>
>
> <span data-ttu-id="4459a-247">Bir kullanıcı iki web uygulamasından erişmek istiyor: bir Web uygulaması ve Web uygulama b</span><span class="sxs-lookup"><span data-stu-id="4459a-247">A user wants to access two web applications: Web Application A and Web Application B.</span></span>
> 
> <span data-ttu-id="4459a-248">Faktörleri:</span><span class="sxs-lookup"><span data-stu-id="4459a-248">Factors:</span></span>
> * <span data-ttu-id="4459a-249">Aynı üst kuruluştaki her iki web uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="4459a-249">Both web applications are in the same parent organization.</span></span>
> * <span data-ttu-id="4459a-250">Belirteç ömrü ilkesi 1 bir oturum belirteci Maksimum yaş sekiz saat ile üst kuruluşunuzun varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-250">Token Lifetime Policy 1 with a Session Token Max Age of eight hours is set as the parent organization’s default.</span></span>
> * <span data-ttu-id="4459a-251">Web uygulaması A normal kullanım web uygulaması ve tüm ilkeleri bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="4459a-251">Web Application A is a regular-use web application and isn’t linked to any policies.</span></span>
> * <span data-ttu-id="4459a-252">Web uygulaması B son derece hassas işlemler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4459a-252">Web Application B is used for highly sensitive processes.</span></span> <span data-ttu-id="4459a-253">Kendi hizmet sorumlusu belirteç ömrü ilkesi bir oturum belirteci Maksimum yaş 30 dakika olan 2'ye bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4459a-253">Its service principal is linked to Token Lifetime Policy 2, which has a Session Token Max Age of 30 minutes.</span></span>
>
> <span data-ttu-id="4459a-254">12:00 PM, kullanıcı yeni bir tarayıcı oturumu başlatır ve Web uygulaması A. erişmeyi dener Kullanıcı için Azure AD yönlendirilir ve oturum açması istenir.</span><span class="sxs-lookup"><span data-stu-id="4459a-254">At 12:00 PM, the user starts a new browser session and tries to access Web Application A. The user is redirected to Azure AD and is asked to sign in.</span></span> <span data-ttu-id="4459a-255">Oturum belirteci tarayıcıda sahip bir tanımlama bilgisi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4459a-255">This creates a cookie that has a session token in the browser.</span></span> <span data-ttu-id="4459a-256">Kullanıcı, kullanıcının uygulamaya erişim sağlayan bir kimliği belirteci ile bir Web uygulaması için yeniden yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-256">The user is redirected back to Web Application A with an ID token that allows the user to access the application.</span></span>
>
> <span data-ttu-id="4459a-257">12: 15'te, kullanıcı Web uygulama B. erişmeyi dener Tarayıcı oturumu tanımlama bilgisi algılar Azure AD yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="4459a-257">At 12:15 PM, the user tries to access Web Application B. The browser redirects to Azure AD, which detects the session cookie.</span></span> <span data-ttu-id="4459a-258">Web uygulaması B'nin hizmet sorumlusu belirteç ömrü ilkesi 2'ye bağlıdır, ancak üst kuruluşla varsayılan belirteç ömrü ilkesi 1 parçası olduğunu da.</span><span class="sxs-lookup"><span data-stu-id="4459a-258">Web Application B’s service principal is linked to Token Lifetime Policy 2, but it's also part of the parent organization, with default Token Lifetime Policy 1.</span></span> <span data-ttu-id="4459a-259">Hizmet sorumluları bağlantılı ilkeler kuruluşun varsayılan ilkelerden daha yüksek bir öncelik olduğundan belirteç ömrü ilkesi 2 etkinleşir.</span><span class="sxs-lookup"><span data-stu-id="4459a-259">Token Lifetime Policy 2 takes effect because policies linked to service principals have a higher priority than organization default policies.</span></span> <span data-ttu-id="4459a-260">Geçerli kabul edilir şekilde oturum belirteci son 30 dakika içinde ilk yayımlandığında.</span><span class="sxs-lookup"><span data-stu-id="4459a-260">The session token was originally issued within the last 30 minutes, so it is considered valid.</span></span> <span data-ttu-id="4459a-261">Kullanıcı erişim veren bir kimliği belirteci ile Web uygulaması B dön yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-261">The user is redirected back to Web Application B with an ID token that grants them access.</span></span>
>
> <span data-ttu-id="4459a-262">1: 00'da, kullanıcı Web uygulaması A. erişmeyi dener Kullanıcı, Azure AD ile yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-262">At 1:00 PM, the user tries to access Web Application A. The user is redirected to Azure AD.</span></span> <span data-ttu-id="4459a-263">Web Uygulama A tüm ilkeleri bağlı değil, ancak bu ilke, varsayılan belirteç ömrü ilkesi 1 olan bir kuruluşta olduğundan, etkili olur.</span><span class="sxs-lookup"><span data-stu-id="4459a-263">Web Application A is not linked to any policies, but because it is in an organization with default Token Lifetime Policy 1, that policy takes effect.</span></span> <span data-ttu-id="4459a-264">Son sekiz saat içinde ilk yayımlandığında oturum tanımlama bilgisi algılandı.</span><span class="sxs-lookup"><span data-stu-id="4459a-264">The session cookie that was originally issued within the last eight hours is detected.</span></span> <span data-ttu-id="4459a-265">Kullanıcı, yeni bir kimliği belirteci Web uygulamasıyla A dön sessizce yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-265">The user is silently redirected back to Web Application A with a new ID token.</span></span> <span data-ttu-id="4459a-266">Kullanıcı kimlik doğrulaması için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="4459a-266">The user is not required to authenticate.</span></span>
>
> <span data-ttu-id="4459a-267">Kullanıcı daha sonra Web uygulaması B. erişmeyi dener hemen Kullanıcı, Azure AD ile yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-267">Immediately afterward, the user tries to access Web Application B. The user is redirected to Azure AD.</span></span> <span data-ttu-id="4459a-268">Olarak daha önce belirteç ömrü ilkesi 2 etkinleşir.</span><span class="sxs-lookup"><span data-stu-id="4459a-268">As before, Token Lifetime Policy 2 takes effect.</span></span> <span data-ttu-id="4459a-269">Belirteç 30 dakikadan daha önce verilmiş olduğundan, kullanıcı oturum açma kimlik bilgilerini yeniden girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="4459a-269">Because the token was issued more than 30 minutes ago, the user is prompted to reenter their sign-in credentials.</span></span> <span data-ttu-id="4459a-270">Yeni Oturum belirteci ve kimliği belirteci verilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-270">A brand-new session token and ID token are issued.</span></span> <span data-ttu-id="4459a-271">Kullanıcı daha sonra Web uygulama B. erişebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4459a-271">The user can then access Web Application B.</span></span>
>
>

## <a name="configurable-policy-property-details"></a><span data-ttu-id="4459a-272">Yapılandırılabilir İlkesi özellik ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="4459a-272">Configurable policy property details</span></span>
### <a name="access-token-lifetime"></a><span data-ttu-id="4459a-273">Erişim belirteci ömrü</span><span class="sxs-lookup"><span data-stu-id="4459a-273">Access Token Lifetime</span></span>
<span data-ttu-id="4459a-274">**Dize:** AccessTokenLifetime</span><span class="sxs-lookup"><span data-stu-id="4459a-274">**String:** AccessTokenLifetime</span></span>

<span data-ttu-id="4459a-275">**Etkiler:** erişim belirteçleri, kimlik belirteçlerini</span><span class="sxs-lookup"><span data-stu-id="4459a-275">**Affects:** Access tokens, ID tokens</span></span>

<span data-ttu-id="4459a-276">**Özet:** Bu ilke ne kadar süreyle erişim ve kimliği belirteçleri bu kaynak için geçerli olarak kabul denetler.</span><span class="sxs-lookup"><span data-stu-id="4459a-276">**Summary:** This policy controls how long access and ID tokens for this resource are considered valid.</span></span> <span data-ttu-id="4459a-277">Erişim belirteci ömrü özelliği azaltma bir erişim belirteci veya kötü amaçlı bir oyuncu tarafından uzun bir süre için kullanılan kimliği belirteci riskini azaltır.</span><span class="sxs-lookup"><span data-stu-id="4459a-277">Reducing the Access Token Lifetime property mitigates the risk of an access token or ID token being used by a malicious actor for an extended period of time.</span></span> <span data-ttu-id="4459a-278">(Bu belirteçleri iptal edilemiyor.) Dengelemeyi performansı olumsuz şekilde etkilenir daha sık değiştirilecek belirteçlere sahip olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="4459a-278">(These tokens cannot be revoked.) The trade-off is that performance is adversely affected, because the tokens have to be replaced more often.</span></span>

### <a name="refresh-token-max-inactive-time"></a><span data-ttu-id="4459a-279">Etkin olmayan zaman belirteci sınırı Yenile</span><span class="sxs-lookup"><span data-stu-id="4459a-279">Refresh Token Max Inactive Time</span></span>
<span data-ttu-id="4459a-280">**Dize:** MaxInactiveTime</span><span class="sxs-lookup"><span data-stu-id="4459a-280">**String:** MaxInactiveTime</span></span>

<span data-ttu-id="4459a-281">**Etkiler:** yenileme belirteçleri</span><span class="sxs-lookup"><span data-stu-id="4459a-281">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="4459a-282">**Özet:** Bu ilke bir istemci artık bu kaynağa erişmeye çalışırken zaman yeni bir erişim/yenileme belirteci çifti almak üzere kullanabilmeniz için önce ne kadar eski bir yenileme belirteci olabilir denetler.</span><span class="sxs-lookup"><span data-stu-id="4459a-282">**Summary:** This policy controls how old a refresh token can be before a client can no longer use it to retrieve a new access/refresh token pair when attempting to access this resource.</span></span> <span data-ttu-id="4459a-283">Bir yenileme belirteci kullanıldığında, yeni bir yenileme belirteci genellikle döndürüldüğünden, istemcinin belirtilen süre boyunca geçerli yenileme belirtecini kullanarak herhangi bir kaynağa erişmeye çalışırsa, bu ilkeyi erişimi engeller.</span><span class="sxs-lookup"><span data-stu-id="4459a-283">Because a new refresh token usually is returned when a refresh token is used, this policy prevents access if the client tries to access any resource by using the current refresh token during the specified period of time.</span></span>

<span data-ttu-id="4459a-284">Bu ilke, yeni bir yenileme belirteci almak için yeniden kimlik doğrulamaya, istemcide etkin edilmemiş kullanıcılar zorlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-284">This policy forces users who have not been active on their client to reauthenticate to retrieve a new refresh token.</span></span>

<span data-ttu-id="4459a-285">Yenileme belirteci etkin olmayan zaman sınırı özelliğini tek Etmenli belirteci Maksimum yaş ve çok faktörlü yenileme belirteci Maksimum yaş Özellikler'den daha düşük bir değere ayarlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="4459a-285">The Refresh Token Max Inactive Time property must be set to a lower value than the Single-Factor Token Max Age and the Multi-Factor Refresh Token Max Age properties.</span></span>

### <a name="single-factor-refresh-token-max-age"></a><span data-ttu-id="4459a-286">Tek Faktörlü yenileme belirteci Maksimum yaş</span><span class="sxs-lookup"><span data-stu-id="4459a-286">Single-Factor Refresh Token Max Age</span></span>
<span data-ttu-id="4459a-287">**Dize:** MaxAgeSingleFactor</span><span class="sxs-lookup"><span data-stu-id="4459a-287">**String:** MaxAgeSingleFactor</span></span>

<span data-ttu-id="4459a-288">**Etkiler:** yenileme belirteçleri</span><span class="sxs-lookup"><span data-stu-id="4459a-288">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="4459a-289">**Özet:** bir kullanıcı bir yenileme belirteci son yalnızca tek bir faktörü kullanarak kimlik doğrulamasının sonra yeni bir erişim/yenileme belirteci çifti almak için kullanabileceğiniz ne kadar bu ilke denetler.</span><span class="sxs-lookup"><span data-stu-id="4459a-289">**Summary:** This policy controls how long a user can use a refresh token to get a new access/refresh token pair after they last authenticated successfully by using only a single factor.</span></span> <span data-ttu-id="4459a-290">Bir kullanıcının kimliğini doğrular ve yeni bir yenileme belirteci aldıktan sonra kullanıcı belirtilen süre yenileme belirteci akışı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-290">After a user authenticates and receives a new refresh token, the user can use the refresh token flow for the specified period of time.</span></span> <span data-ttu-id="4459a-291">(Bu geçerli yenileme belirteci iptal ve, etkin olmayan saatten daha uzun bir süre kullanılmayan bırakılır değil sürece geçerlidir.) Bu noktada, kullanıcı yeni bir yenileme belirteci almak için yeniden kimlik doğrulamaya zorlanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-291">(This is true as long as the current refresh token is not revoked, and it is not left unused for longer than the inactive time.) At that point, the user is forced to reauthenticate to receive a new refresh token.</span></span>

<span data-ttu-id="4459a-292">Maksimum yaş azaltarak daha sık kimlik doğrulaması yapmalarına zorlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-292">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="4459a-293">Tek faktörlü kimlik doğrulaması çok faktörlü kimlik doğrulamasından daha az güvenli olduğu kabul edildiği için bu özellik, eşit veya çok faktörlü yenileme belirteci Maksimum yaş özelliğinden daha düşük bir değere ayarlamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-293">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or lesser than the Multi-Factor Refresh Token Max Age property.</span></span>

### <a name="multi-factor-refresh-token-max-age"></a><span data-ttu-id="4459a-294">Çok faktörlü yenileme belirteci Maksimum yaş</span><span class="sxs-lookup"><span data-stu-id="4459a-294">Multi-Factor Refresh Token Max Age</span></span>
<span data-ttu-id="4459a-295">**Dize:** MaxAgeMultiFactor</span><span class="sxs-lookup"><span data-stu-id="4459a-295">**String:** MaxAgeMultiFactor</span></span>

<span data-ttu-id="4459a-296">**Etkiler:** yenileme belirteçleri</span><span class="sxs-lookup"><span data-stu-id="4459a-296">**Affects:** Refresh tokens</span></span>

<span data-ttu-id="4459a-297">**Özet:** bir kullanıcı bir yenileme belirteci son birden çok faktörünü kullanarak kimlik doğrulamasının sonra yeni bir erişim/yenileme belirteci çifti almak için kullanabileceğiniz ne kadar bu ilke denetler.</span><span class="sxs-lookup"><span data-stu-id="4459a-297">**Summary:** This policy controls how long a user can use a refresh token to get a new access/refresh token pair after they last authenticated successfully by using multiple factors.</span></span> <span data-ttu-id="4459a-298">Bir kullanıcının kimliğini doğrular ve yeni bir yenileme belirteci aldıktan sonra kullanıcı belirtilen süre yenileme belirteci akışı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-298">After a user authenticates and receives a new refresh token, the user can use the refresh token flow for the specified period of time.</span></span> <span data-ttu-id="4459a-299">(Bu geçerli yenileme belirteci iptal ve etkin olmayan saatten daha uzun bir süre kullanılmayan değil sürece geçerlidir.) Bu noktada, kullanıcıların yeni bir yenileme belirteci almak için yeniden kimlik doğrulamaya zorlanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-299">(This is true as long as the current refresh token is not revoked, and it is not unused for longer than the inactive time.) At that point, users are forced to reauthenticate to receive a new refresh token.</span></span>

<span data-ttu-id="4459a-300">Maksimum yaş azaltarak daha sık kimlik doğrulaması yapmalarına zorlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-300">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="4459a-301">Tek faktörlü kimlik doğrulaması çok faktörlü kimlik doğrulamasından daha az güvenli olduğu kabul edildiği için bu özellik, eşit veya bundan tek Faktörlü yenileme belirteci Maksimum yaş özelliği büyük bir değere ayarlamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-301">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or greater than the Single-Factor Refresh Token Max Age property.</span></span>

### <a name="single-factor-session-token-max-age"></a><span data-ttu-id="4459a-302">Tek Faktörlü Oturum belirteci Maksimum yaş</span><span class="sxs-lookup"><span data-stu-id="4459a-302">Single-Factor Session Token Max Age</span></span>
<span data-ttu-id="4459a-303">**Dize:** MaxAgeSessionSingleFactor</span><span class="sxs-lookup"><span data-stu-id="4459a-303">**String:** MaxAgeSessionSingleFactor</span></span>

<span data-ttu-id="4459a-304">**Etkiler:** oturum belirteçleri (kalıcı ve kalıcı olmayan)</span><span class="sxs-lookup"><span data-stu-id="4459a-304">**Affects:** Session tokens (persistent and nonpersistent)</span></span>

<span data-ttu-id="4459a-305">**Özet:** bir kullanıcı oturum belirteci son yalnızca tek bir faktörü kullanarak kimlik doğrulamasının sonra yeni kimliği ve oturum belirteci almak için kullanabileceğiniz ne kadar bu ilke denetler.</span><span class="sxs-lookup"><span data-stu-id="4459a-305">**Summary:** This policy controls how long a user can use a session token to get a new ID and session token after they last authenticated successfully by using only a single factor.</span></span> <span data-ttu-id="4459a-306">Bir kullanıcının kimliğini doğrular ve yeni oturum belirteci aldıktan sonra kullanıcı oturum belirteci akışı belirtilen süre için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-306">After a user authenticates and receives a new session token, the user can use the session token flow for the specified period of time.</span></span> <span data-ttu-id="4459a-307">(Geçerli oturum belirteci iptal ve süresi geçmemiş sürece bu doğrudur.) Belirtilen süre sonra kullanıcı yeni oturum belirteci almak için yeniden kimlik doğrulamaya zorlanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-307">(This is true as long as the current session token is not revoked and has not expired.) After the specified period of time, the user is forced to reauthenticate to receive a new session token.</span></span>

<span data-ttu-id="4459a-308">Maksimum yaş azaltarak daha sık kimlik doğrulaması yapmalarına zorlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-308">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="4459a-309">Tek faktörlü kimlik doğrulaması çok faktörlü kimlik doğrulamasından daha az güvenli olduğu kabul edildiği için bu özellik, eşit veya çok faktörlü Oturum belirteci Maksimum yaş özelliği'den büyük bir değere ayarlamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-309">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or less than the Multi-Factor Session Token Max Age property.</span></span>

### <a name="multi-factor-session-token-max-age"></a><span data-ttu-id="4459a-310">Çok faktörlü Oturum belirteci Maksimum yaş</span><span class="sxs-lookup"><span data-stu-id="4459a-310">Multi-Factor Session Token Max Age</span></span>
<span data-ttu-id="4459a-311">**Dize:** MaxAgeSessionMultiFactor</span><span class="sxs-lookup"><span data-stu-id="4459a-311">**String:** MaxAgeSessionMultiFactor</span></span>

<span data-ttu-id="4459a-312">**Etkiler:** oturum belirteçleri (kalıcı ve kalıcı olmayan)</span><span class="sxs-lookup"><span data-stu-id="4459a-312">**Affects:** Session tokens (persistent and nonpersistent)</span></span>

<span data-ttu-id="4459a-313">**Özet:** bir kullanıcının oturum belirteci yeni kimliği ve oturum doğrulandığını başarıyla birden çok faktörünü kullanarak son saatten sonra belirtecini almak için kullanabileceği Bu ilke denetimleri ne kadar.</span><span class="sxs-lookup"><span data-stu-id="4459a-313">**Summary:** This policy controls how long a user can use a session token to get a new ID and session token after the last time they authenticated successfully by using multiple factors.</span></span> <span data-ttu-id="4459a-314">Bir kullanıcının kimliğini doğrular ve yeni oturum belirteci aldıktan sonra kullanıcı oturum belirteci akışı belirtilen süre için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-314">After a user authenticates and receives a new session token, the user can use the session token flow for the specified period of time.</span></span> <span data-ttu-id="4459a-315">(Geçerli oturum belirteci iptal ve süresi geçmemiş sürece bu doğrudur.) Belirtilen süre sonra kullanıcı yeni oturum belirteci almak için yeniden kimlik doğrulamaya zorlanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-315">(This is true as long as the current session token is not revoked and has not expired.) After the specified period of time, the user is forced to reauthenticate to receive a new session token.</span></span>

<span data-ttu-id="4459a-316">Maksimum yaş azaltarak daha sık kimlik doğrulaması yapmalarına zorlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-316">Reducing the max age forces users to authenticate more often.</span></span> <span data-ttu-id="4459a-317">Tek faktörlü kimlik doğrulaması çok faktörlü kimlik doğrulamasından daha az güvenli olduğu kabul edildiği için bu özellik, eşit veya bundan tek Faktörlü Oturum belirteci Maksimum yaş özelliği büyük bir değere ayarlamanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="4459a-317">Because single-factor authentication is considered less secure than multi-factor authentication, we recommend that you set this property to a value that is equal to or greater than the Single-Factor Session Token Max Age property.</span></span>

## <a name="example-token-lifetime-policies"></a><span data-ttu-id="4459a-318">Örnek belirteç ömrü ilkeleri</span><span class="sxs-lookup"><span data-stu-id="4459a-318">Example token lifetime policies</span></span>
<span data-ttu-id="4459a-319">Birçok senaryoları oluşturabilir ve uygulamaları, hizmet asıl adı ve genel kuruluşunuz için belirteç ömürleri yönetmek zaman Azure AD'de mümkündür.</span><span class="sxs-lookup"><span data-stu-id="4459a-319">Many scenarios are possible in Azure AD when you can create and manage token lifetimes for apps, service principals, and your overall organization.</span></span> <span data-ttu-id="4459a-320">Bu bölümde, yeni kurallar için zorunlu tuttukları yardımcı olacak birkaç ilke senaryoları size rehberlik eder:</span><span class="sxs-lookup"><span data-stu-id="4459a-320">In this section, we walk through a few common policy scenarios that can help you impose new rules for:</span></span>

* <span data-ttu-id="4459a-321">Belirteç ömrü</span><span class="sxs-lookup"><span data-stu-id="4459a-321">Token Lifetime</span></span>
* <span data-ttu-id="4459a-322">Etkin olmayan zaman belirteci sınırı</span><span class="sxs-lookup"><span data-stu-id="4459a-322">Token Max Inactive Time</span></span>
* <span data-ttu-id="4459a-323">Belirteç Maksimum yaş</span><span class="sxs-lookup"><span data-stu-id="4459a-323">Token Max Age</span></span>

<span data-ttu-id="4459a-324">Örneklerde, öğrenebilir nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="4459a-324">In the examples, you can learn how to:</span></span>

* <span data-ttu-id="4459a-325">Bir kuruluşun varsayılan ilkesini yönetme</span><span class="sxs-lookup"><span data-stu-id="4459a-325">Manage an organization's default policy</span></span>
* <span data-ttu-id="4459a-326">Web oturum açma için bir ilke oluşturun</span><span class="sxs-lookup"><span data-stu-id="4459a-326">Create a policy for web sign-in</span></span>
* <span data-ttu-id="4459a-327">Web API'si çağıran yerel bir uygulama için bir ilke oluşturun</span><span class="sxs-lookup"><span data-stu-id="4459a-327">Create a policy for a native app that calls a web API</span></span>
* <span data-ttu-id="4459a-328">Gelişmiş ilkesini yönetme</span><span class="sxs-lookup"><span data-stu-id="4459a-328">Manage an advanced policy</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4459a-329">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4459a-329">Prerequisites</span></span>
<span data-ttu-id="4459a-330">Aşağıdaki örneklerde, oluşturmak, güncelleştirmek, bağlantı ve uygulamaları, hizmet asıl adı ve genel kuruluşunuz için ilkelerini silin.</span><span class="sxs-lookup"><span data-stu-id="4459a-330">In the following examples, you create, update, link, and delete policies for apps, service principals, and your overall organization.</span></span> <span data-ttu-id="4459a-331">Azure AD ile yeni başladıysanız, hakkında bilgi edinin öneririz [Azure AD kiracısı alma](active-directory-howto-tenant.md) bu örnekleri ile devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="4459a-331">If you are new to Azure AD, we recommend that you learn about [how to get an Azure AD tenant](active-directory-howto-tenant.md) before you proceed with these examples.</span></span>  

<span data-ttu-id="4459a-332">Başlamak için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="4459a-332">To get started, do the following steps:</span></span>

1. <span data-ttu-id="4459a-333">En son karşıdan [Azure AD PowerShell modülü genel Önizleme sürümü](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="4459a-333">Download the latest [Azure AD PowerShell Module Public Preview release](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>
2. <span data-ttu-id="4459a-334">Çalıştırma `Connect` komut Azure AD Yönetici hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4459a-334">Run the `Connect` command to sign in to your Azure AD admin account.</span></span> <span data-ttu-id="4459a-335">Her zaman bu komutu çalıştırmak yeni bir oturum başlatın.</span><span class="sxs-lookup"><span data-stu-id="4459a-335">Run this command each time you start a new session.</span></span>

    ```PowerShell
    Connect-AzureAD -Confirm
    ```

3. <span data-ttu-id="4459a-336">Kuruluşunuzda oluşturulan tüm ilkeleri görmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4459a-336">To see all policies that have been created in your organization, run the following command.</span></span> <span data-ttu-id="4459a-337">Aşağıdaki senaryolarda çoğu işlemlerinden sonra bu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4459a-337">Run this command after most operations in the following scenarios.</span></span> <span data-ttu-id="4459a-338">Komutunu çalıştırarak da yardımcı olur size ** **, ilkelerinizin.</span><span class="sxs-lookup"><span data-stu-id="4459a-338">Running the command also helps you get the ** ** of your policies.</span></span>

    ```PowerShell
    Get-AzureADPolicy
    ```

### <a name="example-manage-an-organizations-default-policy"></a><span data-ttu-id="4459a-339">Örnek: bir kuruluşun varsayılan ilkesini yönetme</span><span class="sxs-lookup"><span data-stu-id="4459a-339">Example: Manage an organization's default policy</span></span>
<span data-ttu-id="4459a-340">Bu örnekte, tüm kuruluş genelinde daha az sıklıkta oturum açın, kullanıcılarınızın sağlayan bir ilkesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4459a-340">In this example, you create a policy that lets your users sign in less frequently across your entire organization.</span></span> <span data-ttu-id="4459a-341">Bunu yapmak için tek Faktörlü Yenile kuruluşunuz genelinde uygulanan belirteçleri, bir belirteç ömrü ilkesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4459a-341">To do this, create a token lifetime policy for Single-Factor Refresh Tokens, which is applied across your organization.</span></span> <span data-ttu-id="4459a-342">Kuruluşunuzdaki her uygulama ve bir ilke kümesi zaten yok her hizmet sorumlusu ilkesi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-342">The policy is applied to every application in your organization, and to each service principal that doesn’t already have a policy set.</span></span>

1. <span data-ttu-id="4459a-343">Bir belirteç ömrü ilkesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4459a-343">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="4459a-344">Küme için tek Faktörlü yenileme belirtecini "kadar iptal edilen."</span><span class="sxs-lookup"><span data-stu-id="4459a-344">Set the Single-Factor Refresh Token to "until-revoked."</span></span> <span data-ttu-id="4459a-345">Erişimi iptal kadar belirtecin süresi sona ermiyor.</span><span class="sxs-lookup"><span data-stu-id="4459a-345">The token doesn't expire until access is revoked.</span></span> <span data-ttu-id="4459a-346">Aşağıdaki ilke tanımı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4459a-346">Create the following policy definition:</span></span>

        ```PowerShell
        @('{
            "TokenLifetimePolicy":
            {
                "Version":1,
                "MaxAgeSingleFactor":"until-revoked"
            }
        }')
        ```

    2.  <span data-ttu-id="4459a-347">Bir ilke oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4459a-347">To create the policy, run the following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    3.  <span data-ttu-id="4459a-348">Yeni ilke görmek için ve ilkenin almak için **objectID**, aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4459a-348">To see your new policy, and to get the policy's **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="4459a-349">İlke güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="4459a-349">Update the policy.</span></span>

    <span data-ttu-id="4459a-350">Bu örnekte, ayarladığınız ilk ilke hizmetiniz için gerekli olarak katı değil karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-350">You might decide that the first policy you set in this example is not as strict as your service requires.</span></span> <span data-ttu-id="4459a-351">Tek Faktörlü yenileme süresi iki gün içinde dolacak belirteci ayarlamak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4459a-351">To set your Single-Factor Refresh Token to expire in two days, run the following command:</span></span>

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId FROM GET COMMAND> -DisplayName "OrganizationDefaultPolicyUpdatedScenario" -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"2.00:00:00"}}')
    ```

### <a name="example-create-a-policy-for-web-sign-in"></a><span data-ttu-id="4459a-352">Örnek: web oturum açma için bir ilke oluşturun</span><span class="sxs-lookup"><span data-stu-id="4459a-352">Example: Create a policy for web sign-in</span></span>

<span data-ttu-id="4459a-353">Bu örnekte, kullanıcılar web uygulamanızı daha sık kimlik doğrulaması gerektiren bir ilke oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4459a-353">In this example, you create a policy that requires users to authenticate more frequently in your web app.</span></span> <span data-ttu-id="4459a-354">Bu ilke, web uygulamanızın hizmet sorumlusu erişim/kimlik belirteçlerini ömrü ve çok faktörlü Oturum belirteci Maksimum yaş ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-354">This policy sets the lifetime of the access/ID tokens and the max age of a multi-factor session token to the service principal of your web app.</span></span>

1. <span data-ttu-id="4459a-355">Bir belirteç ömrü ilkesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4459a-355">Create a token lifetime policy.</span></span>

    <span data-ttu-id="4459a-356">Bu ilke için web oturum açma, erişim/kimlik belirteç ömrü ve max tek Faktörlü Oturum belirteci yaş iki saate ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-356">This policy, for web sign-in, sets the access/ID token lifetime and the max single-factor session token age to two hours.</span></span>

    1.  <span data-ttu-id="4459a-357">Bir ilke oluşturmak için bu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4459a-357">To create the policy, run this command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"AccessTokenLifetime":"02:00:00","MaxAgeSessionSingleFactor":"02:00:00"}}') -DisplayName "WebPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="4459a-358">Yeni ilke görmek ve ilkeyi almak üzere **objectID**, aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4459a-358">To see your new policy, and to get the policy **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2.  <span data-ttu-id="4459a-359">İlke, hizmet sorumlusu atayın.</span><span class="sxs-lookup"><span data-stu-id="4459a-359">Assign the policy to your service principal.</span></span> <span data-ttu-id="4459a-360">Almanız gereken **objectID** hizmet asıl.</span><span class="sxs-lookup"><span data-stu-id="4459a-360">You also need to get the **ObjectId** of your service principal.</span></span> 

    1.  <span data-ttu-id="4459a-361">Kuruluşunuzun tüm hizmet asıl adı görmek için Sorgulayabileceğiniz [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span><span class="sxs-lookup"><span data-stu-id="4459a-361">To see all your organization's service principals, you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span></span> <span data-ttu-id="4459a-362">Veya, [Azure AD Graph Explorer'a](https://graphexplorer.cloudapp.net/), Azure AD hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4459a-362">Or, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), sign in to your Azure AD account.</span></span>

    2.  <span data-ttu-id="4459a-363">Olduğunda **objectID** aşağıdaki komutu çalıştırın, hizmet asıl:</span><span class="sxs-lookup"><span data-stu-id="4459a-363">When you have the **ObjectId** of your service principal, run the following command:</span></span>

        ```PowerShell
        Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
        ```


### <a name="example-create-a-policy-for-a-native-app-that-calls-a-web-api"></a><span data-ttu-id="4459a-364">Örnek: web API'si çağıran yerel bir uygulama için bir ilke oluşturun</span><span class="sxs-lookup"><span data-stu-id="4459a-364">Example: Create a policy for a native app that calls a web API</span></span>
<span data-ttu-id="4459a-365">Bu örnekte, daha az sıklıkta kimlik doğrulaması gerektiren bir ilke oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4459a-365">In this example, you create a policy that requires users to authenticate less frequently.</span></span> <span data-ttu-id="4459a-366">İlke, aynı zamanda kullanıcının sağlamalarını gerekir önce bir kullanıcının etkin olmayan kalabileceği süreyi uzatır.</span><span class="sxs-lookup"><span data-stu-id="4459a-366">The policy also lengthens the amount of time a user can be inactive before the user must reauthenticate.</span></span> <span data-ttu-id="4459a-367">Web API ilkesi uygulanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-367">The policy is applied to the web API.</span></span> <span data-ttu-id="4459a-368">Yerel uygulama web API'si bir kaynak olarak istediğinde, bu ilke uygulanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-368">When the native app requests the web API as a resource, this policy is applied.</span></span>

1. <span data-ttu-id="4459a-369">Bir belirteç ömrü ilkesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4459a-369">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="4459a-370">Web API'si için kesin bir ilke oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4459a-370">To create a strict policy for a web API, run the following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"30.00:00:00","MaxAgeMultiFactor":"until-revoked","MaxAgeSingleFactor":"180.00:00:00"}}') -DisplayName "WebApiDefaultPolicyScenario" -IsOrganizationDefault $false -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="4459a-371">Yeni ilke görmek ve ilkeyi almak üzere **objectID**, aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4459a-371">To see your new policy, and to get the policy **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="4459a-372">İlke web API'nize atayın.</span><span class="sxs-lookup"><span data-stu-id="4459a-372">Assign the policy to your web API.</span></span> <span data-ttu-id="4459a-373">Almanız gereken **objectID** uygulamanızın.</span><span class="sxs-lookup"><span data-stu-id="4459a-373">You also need to get the **ObjectId** of your application.</span></span> <span data-ttu-id="4459a-374">Uygulamanızın bulmak için en iyi yolu **objectID** kullanmaktır [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4459a-374">The best way to find your app's **ObjectId** is to use the [Azure portal](https://portal.azure.com/).</span></span>

   <span data-ttu-id="4459a-375">Olduğunda **objectID** , uygulamanızın, aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4459a-375">When you have the **ObjectId** of your app, run the following command:</span></span>

        ```PowerShell
        Add-AzureADApplicationPolicy -Id <ObjectId of the Application> -RefObjectId <ObjectId of the Policy>
        ```


### <a name="example-manage-an-advanced-policy"></a><span data-ttu-id="4459a-376">Örnek: bir Gelişmiş ilkesini yönetme</span><span class="sxs-lookup"><span data-stu-id="4459a-376">Example: Manage an advanced policy</span></span>
<span data-ttu-id="4459a-377">Bu örnekte, öncelik sistem nasıl çalıştığını öğrenmek için birkaç ilkeleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4459a-377">In this example, you create a few policies, to learn how the priority system works.</span></span> <span data-ttu-id="4459a-378">Ayrıca, bazı nesnelere uygulanan birden çok ilkelerini yönetmek nasıl öğrenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-378">You also can learn how to manage multiple policies that are applied to several objects.</span></span>

1. <span data-ttu-id="4459a-379">Bir belirteç ömrü ilkesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4459a-379">Create a token lifetime policy.</span></span>

    1.  <span data-ttu-id="4459a-380">30 gün için tek Faktörlü Yenile belirteç ömrü ayarlar bir kuruluş varsayılan ilkeyi oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4459a-380">To create an organization default policy that sets the Single-Factor Refresh Token lifetime to 30 days, run the following command:</span></span>

        ```PowerShell
        New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"30.00:00:00"}}') -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
        ```

    2.  <span data-ttu-id="4459a-381">Yeni ilke görmek için ve ilkenin almak için **objectID**, aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4459a-381">To see your new policy, and to get the policy's **ObjectId**, run the following command:</span></span>

        ```PowerShell
        Get-AzureADPolicy
        ```

2. <span data-ttu-id="4459a-382">İlke için bir hizmet sorumlusu atayın.</span><span class="sxs-lookup"><span data-stu-id="4459a-382">Assign the policy to a service principal.</span></span>

    <span data-ttu-id="4459a-383">Artık, tüm kuruluş genelinde geçerli bir ilkesi var.</span><span class="sxs-lookup"><span data-stu-id="4459a-383">Now, you have a policy that applies to the entire organization.</span></span> <span data-ttu-id="4459a-384">Bu 30 günlük ilkesi için bir özel hizmet sorumlusu korumak, ancak "kadar iptal edilen." sayısı üst sınırı için kuruluşunuzun varsayılan ilkesini değiştirmek isteyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="4459a-384">You might want to preserve this 30-day policy for a specific service principal, but change the organization default policy to the upper limit of "until-revoked."</span></span>

    1.  <span data-ttu-id="4459a-385">Kuruluşunuzun tüm hizmet asıl adı görmek için Sorgulayabileceğiniz [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span><span class="sxs-lookup"><span data-stu-id="4459a-385">To see all your organization's service principals, you can query [Microsoft Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity).</span></span> <span data-ttu-id="4459a-386">Veya, [Azure AD Graph Explorer'a](https://graphexplorer.cloudapp.net/), Azure AD hesabınızı kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="4459a-386">Or, in [Azure AD Graph Explorer](https://graphexplorer.cloudapp.net/), sign in by using your Azure AD account.</span></span>

    2.  <span data-ttu-id="4459a-387">Olduğunda **objectID** aşağıdaki komutu çalıştırın, hizmet asıl:</span><span class="sxs-lookup"><span data-stu-id="4459a-387">When you have the **ObjectId** of your service principal, run the following command:</span></span>

            ```PowerShell
            Add-AzureADServicePrincipalPolicy -Id <ObjectId of the ServicePrincipal> -RefObjectId <ObjectId of the Policy>
            ```
        
3. <span data-ttu-id="4459a-388">Ayarlama `IsOrganizationDefault` bayrağı false olarak ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="4459a-388">Set the `IsOrganizationDefault` flag to false:</span></span>

    ```PowerShell
    Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName "ComplexPolicyScenario" -IsOrganizationDefault $false
    ```

4. <span data-ttu-id="4459a-389">Yeni bir kuruluş varsayılan ilke oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4459a-389">Create a new organization default policy:</span></span>

    ```PowerShell
    New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "ComplexPolicyScenarioTwo" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"
    ```

    <span data-ttu-id="4459a-390">Şimdi, hizmet sorumlusuna bağlı özgün ilkesine sahip ve yeni ilke, kuruluş varsayılan ilke olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="4459a-390">You now have the original policy linked to your service principal, and the new policy is set as your organization default policy.</span></span> <span data-ttu-id="4459a-391">Hizmet sorumluları uygulanan ilkeler kuruluş varsayılan ilke önceliğe sahip unutmamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="4459a-391">It's important to remember that policies applied to service principals have priority over organization default policies.</span></span>

## <a name="cmdlet-reference"></a><span data-ttu-id="4459a-392">Cmdlet başvurusu</span><span class="sxs-lookup"><span data-stu-id="4459a-392">Cmdlet reference</span></span>

### <a name="manage-policies"></a><span data-ttu-id="4459a-393">İlkeleri yönetme</span><span class="sxs-lookup"><span data-stu-id="4459a-393">Manage policies</span></span>

<span data-ttu-id="4459a-394">Aşağıdaki cmdlet ilkelerini yönetmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-394">You can use the following cmdlets to manage policies.</span></span>

#### <a name="new-azureadpolicy"></a><span data-ttu-id="4459a-395">AzureADPolicy yeni</span><span class="sxs-lookup"><span data-stu-id="4459a-395">New-AzureADPolicy</span></span>

<span data-ttu-id="4459a-396">Yeni bir ilke oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4459a-396">Creates a new policy.</span></span>

```PowerShell
New-AzureADPolicy -Definition <Array of Rules> -DisplayName <Name of Policy> -IsOrganizationDefault <boolean> -Type <Policy Type>
```

| <span data-ttu-id="4459a-397">Parametreler</span><span class="sxs-lookup"><span data-stu-id="4459a-397">Parameters</span></span> | <span data-ttu-id="4459a-398">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4459a-398">Description</span></span> | <span data-ttu-id="4459a-399">Örnek</span><span class="sxs-lookup"><span data-stu-id="4459a-399">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Definition</code> |<span data-ttu-id="4459a-400">Tüm ilkesinin kuralları içeren stringified JSON dizisi.</span><span class="sxs-lookup"><span data-stu-id="4459a-400">Array of stringified JSON that contains all the policy's rules.</span></span> | `-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <code>&#8209;DisplayName</code> |<span data-ttu-id="4459a-401">İlke adı dizesi.</span><span class="sxs-lookup"><span data-stu-id="4459a-401">String of the policy name.</span></span> |`-DisplayName "MyTokenPolicy"` |
| <code>&#8209;IsOrganizationDefault</code> |<span data-ttu-id="4459a-402">TRUE ise, ilke kuruluşunuzun varsayılan ilke olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-402">If true, sets the policy as the organization's default policy.</span></span> <span data-ttu-id="4459a-403">False ise, hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="4459a-403">If false, does nothing.</span></span> |`-IsOrganizationDefault $true` |
| <code>&#8209;Type</code> |<span data-ttu-id="4459a-404">İlke türü.</span><span class="sxs-lookup"><span data-stu-id="4459a-404">Type of policy.</span></span> <span data-ttu-id="4459a-405">Belirteç yaşam süreleri her zaman "TokenLifetimePolicy." kullan</span><span class="sxs-lookup"><span data-stu-id="4459a-405">For token lifetimes, always use "TokenLifetimePolicy."</span></span> | `-Type "TokenLifetimePolicy"` |
| <span data-ttu-id="4459a-406"><code>&#8209;AlternativeIdentifier</code>[İsteğe bağlı]</span><span class="sxs-lookup"><span data-stu-id="4459a-406"><code>&#8209;AlternativeIdentifier</code> [Optional]</span></span> |<span data-ttu-id="4459a-407">İlke için alternatif bir kimlik ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-407">Sets an alternative ID for the policy.</span></span> |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="get-azureadpolicy"></a><span data-ttu-id="4459a-408">Get-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="4459a-408">Get-AzureADPolicy</span></span>
<span data-ttu-id="4459a-409">Tüm Azure AD ilkeleri veya belirtilen ilkesini alır.</span><span class="sxs-lookup"><span data-stu-id="4459a-409">Gets all Azure AD policies or a specified policy.</span></span>

```PowerShell
Get-AzureADPolicy
```

| <span data-ttu-id="4459a-410">Parametreler</span><span class="sxs-lookup"><span data-stu-id="4459a-410">Parameters</span></span> | <span data-ttu-id="4459a-411">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4459a-411">Description</span></span> | <span data-ttu-id="4459a-412">Örnek</span><span class="sxs-lookup"><span data-stu-id="4459a-412">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4459a-413"><code>&#8209;Id</code>[İsteğe bağlı]</span><span class="sxs-lookup"><span data-stu-id="4459a-413"><code>&#8209;Id</code> [Optional]</span></span> |<span data-ttu-id="4459a-414">**ObjectID (ID)** istediğiniz ilke.</span><span class="sxs-lookup"><span data-stu-id="4459a-414">**ObjectId (Id)** of the policy you want.</span></span> |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadpolicyappliedobject"></a><span data-ttu-id="4459a-415">Get-AzureADPolicyAppliedObject</span><span class="sxs-lookup"><span data-stu-id="4459a-415">Get-AzureADPolicyAppliedObject</span></span>
<span data-ttu-id="4459a-416">Tüm uygulamaları ve bir ilke bağlantılı hizmet asıl adı alır.</span><span class="sxs-lookup"><span data-stu-id="4459a-416">Gets all apps and service principals that are linked to a policy.</span></span>

```PowerShell
Get-AzureADPolicyAppliedObject -Id <ObjectId of Policy>
```

| <span data-ttu-id="4459a-417">Parametreler</span><span class="sxs-lookup"><span data-stu-id="4459a-417">Parameters</span></span> | <span data-ttu-id="4459a-418">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4459a-418">Description</span></span> | <span data-ttu-id="4459a-419">Örnek</span><span class="sxs-lookup"><span data-stu-id="4459a-419">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="4459a-420">**ObjectID (ID)** istediğiniz ilke.</span><span class="sxs-lookup"><span data-stu-id="4459a-420">**ObjectId (Id)** of the policy you want.</span></span> |`-Id <ObjectId of Policy>` |

</br></br>

#### <a name="set-azureadpolicy"></a><span data-ttu-id="4459a-421">Set-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="4459a-421">Set-AzureADPolicy</span></span>
<span data-ttu-id="4459a-422">Mevcut bir ilkenin güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="4459a-422">Updates an existing policy.</span></span>

```PowerShell
Set-AzureADPolicy -Id <ObjectId of Policy> -DisplayName <string>
```

| <span data-ttu-id="4459a-423">Parametreler</span><span class="sxs-lookup"><span data-stu-id="4459a-423">Parameters</span></span> | <span data-ttu-id="4459a-424">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4459a-424">Description</span></span> | <span data-ttu-id="4459a-425">Örnek</span><span class="sxs-lookup"><span data-stu-id="4459a-425">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="4459a-426">**ObjectID (ID)** istediğiniz ilke.</span><span class="sxs-lookup"><span data-stu-id="4459a-426">**ObjectId (Id)** of the policy you want.</span></span> |`-Id <ObjectId of Policy>` |
| <code>&#8209;DisplayName</code> |<span data-ttu-id="4459a-427">İlke adı dizesi.</span><span class="sxs-lookup"><span data-stu-id="4459a-427">String of the policy name.</span></span> |`-DisplayName "MyTokenPolicy"` |
| <span data-ttu-id="4459a-428"><code>&#8209;Definition</code>[İsteğe bağlı]</span><span class="sxs-lookup"><span data-stu-id="4459a-428"><code>&#8209;Definition</code> [Optional]</span></span> |<span data-ttu-id="4459a-429">Tüm ilkesinin kuralları içeren stringified JSON dizisi.</span><span class="sxs-lookup"><span data-stu-id="4459a-429">Array of stringified JSON that contains all the policy's rules.</span></span> |`-Definition @('{"TokenLifetimePolicy":{"Version":1,"MaxInactiveTime":"20:00:00"}}')` |
| <span data-ttu-id="4459a-430"><code>&#8209;IsOrganizationDefault</code>[İsteğe bağlı]</span><span class="sxs-lookup"><span data-stu-id="4459a-430"><code>&#8209;IsOrganizationDefault</code> [Optional]</span></span> |<span data-ttu-id="4459a-431">TRUE ise, ilke kuruluşunuzun varsayılan ilke olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-431">If true, sets the policy as the organization's default policy.</span></span> <span data-ttu-id="4459a-432">False ise, hiçbir şey yapmaz.</span><span class="sxs-lookup"><span data-stu-id="4459a-432">If false, does nothing.</span></span> |`-IsOrganizationDefault $true` |
| <span data-ttu-id="4459a-433"><code>&#8209;Type</code>[İsteğe bağlı]</span><span class="sxs-lookup"><span data-stu-id="4459a-433"><code>&#8209;Type</code> [Optional]</span></span> |<span data-ttu-id="4459a-434">İlke türü.</span><span class="sxs-lookup"><span data-stu-id="4459a-434">Type of policy.</span></span> <span data-ttu-id="4459a-435">Belirteç yaşam süreleri her zaman "TokenLifetimePolicy." kullan</span><span class="sxs-lookup"><span data-stu-id="4459a-435">For token lifetimes, always use "TokenLifetimePolicy."</span></span> |`-Type "TokenLifetimePolicy"` |
| <span data-ttu-id="4459a-436"><code>&#8209;AlternativeIdentifier</code>[İsteğe bağlı]</span><span class="sxs-lookup"><span data-stu-id="4459a-436"><code>&#8209;AlternativeIdentifier</code> [Optional]</span></span> |<span data-ttu-id="4459a-437">İlke için alternatif bir kimlik ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-437">Sets an alternative ID for the policy.</span></span> |`-AlternativeIdentifier "myAltId"` |

</br></br>

#### <a name="remove-azureadpolicy"></a><span data-ttu-id="4459a-438">Remove-AzureADPolicy</span><span class="sxs-lookup"><span data-stu-id="4459a-438">Remove-AzureADPolicy</span></span>
<span data-ttu-id="4459a-439">Belirtilen ilke siler.</span><span class="sxs-lookup"><span data-stu-id="4459a-439">Deletes the specified policy.</span></span>

```PowerShell
 Remove-AzureADPolicy -Id <ObjectId of Policy>
```

| <span data-ttu-id="4459a-440">Parametreler</span><span class="sxs-lookup"><span data-stu-id="4459a-440">Parameters</span></span> | <span data-ttu-id="4459a-441">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4459a-441">Description</span></span> | <span data-ttu-id="4459a-442">Örnek</span><span class="sxs-lookup"><span data-stu-id="4459a-442">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="4459a-443">**ObjectID (ID)** istediğiniz ilke.</span><span class="sxs-lookup"><span data-stu-id="4459a-443">**ObjectId (Id)** of the policy you want.</span></span> | `-Id <ObjectId of Policy>` |

</br></br>

### <a name="application-policies"></a><span data-ttu-id="4459a-444">Uygulama ilkeleri</span><span class="sxs-lookup"><span data-stu-id="4459a-444">Application policies</span></span>
<span data-ttu-id="4459a-445">Uygulama ilkeleri için aşağıdaki cmdlet'leri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-445">You can use the following cmdlets for application policies.</span></span></br></br>

#### <a name="add-azureadapplicationpolicy"></a><span data-ttu-id="4459a-446">Ekleme AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="4459a-446">Add-AzureADApplicationPolicy</span></span>
<span data-ttu-id="4459a-447">Belirtilen ilke uygulama bağlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-447">Links the specified policy to an application.</span></span>

```PowerShell
Add-AzureADApplicationPolicy -Id <ObjectId of Application> -RefObjectId <ObjectId of Policy>
```

| <span data-ttu-id="4459a-448">Parametreler</span><span class="sxs-lookup"><span data-stu-id="4459a-448">Parameters</span></span> | <span data-ttu-id="4459a-449">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4459a-449">Description</span></span> | <span data-ttu-id="4459a-450">Örnek</span><span class="sxs-lookup"><span data-stu-id="4459a-450">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="4459a-451">**ObjectID (ID)** uygulamanın.</span><span class="sxs-lookup"><span data-stu-id="4459a-451">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |<span data-ttu-id="4459a-452">**ObjectID** ilkesi.</span><span class="sxs-lookup"><span data-stu-id="4459a-452">**ObjectId** of the policy.</span></span> | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadapplicationpolicy"></a><span data-ttu-id="4459a-453">Get-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="4459a-453">Get-AzureADApplicationPolicy</span></span>
<span data-ttu-id="4459a-454">Bir uygulamaya atanan ilkesini alır.</span><span class="sxs-lookup"><span data-stu-id="4459a-454">Gets the policy that is assigned to an application.</span></span>

```PowerShell
Get-AzureADApplicationPolicy -Id <ObjectId of Application>
```

| <span data-ttu-id="4459a-455">Parametreler</span><span class="sxs-lookup"><span data-stu-id="4459a-455">Parameters</span></span> | <span data-ttu-id="4459a-456">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4459a-456">Description</span></span> | <span data-ttu-id="4459a-457">Örnek</span><span class="sxs-lookup"><span data-stu-id="4459a-457">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="4459a-458">**ObjectID (ID)** uygulamanın.</span><span class="sxs-lookup"><span data-stu-id="4459a-458">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadapplicationpolicy"></a><span data-ttu-id="4459a-459">Remove-AzureADApplicationPolicy</span><span class="sxs-lookup"><span data-stu-id="4459a-459">Remove-AzureADApplicationPolicy</span></span>
<span data-ttu-id="4459a-460">Bir ilke bir uygulamadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4459a-460">Removes a policy from an application.</span></span>

```PowerShell
Remove-AzureADApplicationPolicy -Id <ObjectId of Application> -PolicyId <ObjectId of Policy>
```

| <span data-ttu-id="4459a-461">Parametreler</span><span class="sxs-lookup"><span data-stu-id="4459a-461">Parameters</span></span> | <span data-ttu-id="4459a-462">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4459a-462">Description</span></span> | <span data-ttu-id="4459a-463">Örnek</span><span class="sxs-lookup"><span data-stu-id="4459a-463">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="4459a-464">**ObjectID (ID)** uygulamanın.</span><span class="sxs-lookup"><span data-stu-id="4459a-464">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |<span data-ttu-id="4459a-465">**ObjectID** ilkesi.</span><span class="sxs-lookup"><span data-stu-id="4459a-465">**ObjectId** of the policy.</span></span> | `-PolicyId <ObjectId of Policy>` |

</br></br>

### <a name="service-principal-policies"></a><span data-ttu-id="4459a-466">Hizmet asıl ilkeleri</span><span class="sxs-lookup"><span data-stu-id="4459a-466">Service principal policies</span></span>
<span data-ttu-id="4459a-467">Aşağıdaki cmdlet'leri için hizmet asıl ilkeleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4459a-467">You can use the following cmdlets for service principal policies.</span></span>

#### <a name="add-azureadserviceprincipalpolicy"></a><span data-ttu-id="4459a-468">Ekleme AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="4459a-468">Add-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="4459a-469">Belirtilen ilke için bir hizmet sorumlusu bağlar.</span><span class="sxs-lookup"><span data-stu-id="4459a-469">Links the specified policy to a service principal.</span></span>

```PowerShell
Add-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal> -RefObjectId <ObjectId of Policy>
```

| <span data-ttu-id="4459a-470">Parametreler</span><span class="sxs-lookup"><span data-stu-id="4459a-470">Parameters</span></span> | <span data-ttu-id="4459a-471">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4459a-471">Description</span></span> | <span data-ttu-id="4459a-472">Örnek</span><span class="sxs-lookup"><span data-stu-id="4459a-472">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="4459a-473">**ObjectID (ID)** uygulamanın.</span><span class="sxs-lookup"><span data-stu-id="4459a-473">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;RefObjectId</code> |<span data-ttu-id="4459a-474">**ObjectID** ilkesi.</span><span class="sxs-lookup"><span data-stu-id="4459a-474">**ObjectId** of the policy.</span></span> | `-RefObjectId <ObjectId of Policy>` |

</br></br>

#### <a name="get-azureadserviceprincipalpolicy"></a><span data-ttu-id="4459a-475">Get-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="4459a-475">Get-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="4459a-476">Belirtilen hizmet sorumlusuna bağlı herhangi bir ilke alır.</span><span class="sxs-lookup"><span data-stu-id="4459a-476">Gets any policy linked to the specified service principal.</span></span>

```PowerShell
Get-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>
```

| <span data-ttu-id="4459a-477">Parametreler</span><span class="sxs-lookup"><span data-stu-id="4459a-477">Parameters</span></span> | <span data-ttu-id="4459a-478">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4459a-478">Description</span></span> | <span data-ttu-id="4459a-479">Örnek</span><span class="sxs-lookup"><span data-stu-id="4459a-479">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="4459a-480">**ObjectID (ID)** uygulamanın.</span><span class="sxs-lookup"><span data-stu-id="4459a-480">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |

</br></br>

#### <a name="remove-azureadserviceprincipalpolicy"></a><span data-ttu-id="4459a-481">Remove-AzureADServicePrincipalPolicy</span><span class="sxs-lookup"><span data-stu-id="4459a-481">Remove-AzureADServicePrincipalPolicy</span></span>
<span data-ttu-id="4459a-482">İlke asıl belirtilen hizmetinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="4459a-482">Removes the policy from the specified service principal.</span></span>

```PowerShell
Remove-AzureADServicePrincipalPolicy -Id <ObjectId of ServicePrincipal>  -PolicyId <ObjectId of Policy>
```

| <span data-ttu-id="4459a-483">Parametreler</span><span class="sxs-lookup"><span data-stu-id="4459a-483">Parameters</span></span> | <span data-ttu-id="4459a-484">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4459a-484">Description</span></span> | <span data-ttu-id="4459a-485">Örnek</span><span class="sxs-lookup"><span data-stu-id="4459a-485">Example</span></span> |
| --- | --- | --- |
| <code>&#8209;Id</code> |<span data-ttu-id="4459a-486">**ObjectID (ID)** uygulamanın.</span><span class="sxs-lookup"><span data-stu-id="4459a-486">**ObjectId (Id)** of the application.</span></span> | `-Id <ObjectId of Application>` |
| <code>&#8209;PolicyId</code> |<span data-ttu-id="4459a-487">**ObjectID** ilkesi.</span><span class="sxs-lookup"><span data-stu-id="4459a-487">**ObjectId** of the policy.</span></span> | `-PolicyId <ObjectId of Policy>` |
