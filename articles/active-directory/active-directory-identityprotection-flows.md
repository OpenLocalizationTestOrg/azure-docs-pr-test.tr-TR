---
title: "Azure AD Identity Protection deneyimleriyle aaaSign bileşenini | Microsoft Docs"
description: "Kimlik koruması azaltıldığından veya bir kullanıcı veya çok faktörlü kimlik doğrulama İlkesi tarafından ne zaman gerekli düzeltilen hello kullanıcı deneyimi genel bir bakış sağlar."
services: active-directory
keywords: "Azure active directory kimlik koruması, cloud app discovery'yi, uygulamalar, güvenlik, risk, risk düzeyi, güvenlik açığı, güvenlik ilkesi yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: de5bf637-75a7-4104-b6d8-03686372a319
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: fbdca5b86ed93d0a2f2b6df1dd0150da9c0c85c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="541e8-104">Oturum açma deneyimlerini Azure AD kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="541e8-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="541e8-105">Azure Active Directory kimlik koruması ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="541e8-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="541e8-106">Kullanıcıların tooregister çok faktörlü kimlik doğrulamasını gerektirir</span><span class="sxs-lookup"><span data-stu-id="541e8-106">require users tooregister for multi-factor authentication</span></span>
* <span data-ttu-id="541e8-107">riskli oturum açma işlemleri ve güvenliği aşılan kullanıcılar işleme</span><span class="sxs-lookup"><span data-stu-id="541e8-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="541e8-108">yalnızca doğrudan imzalama bir kullanıcı adı ve parola sağlayarak bileşenini artık mümkün olmayacaktır çünkü hello sistem toothese sorunları hello yanıtın bir kullanıcının oturum açma deneyimi üzerinde bir etkisi yoktur.</span><span class="sxs-lookup"><span data-stu-id="541e8-108">hello response of hello system toothese issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="541e8-109">Bir kullanıcı güvenli biçimde yedeklemeniz işletme gerekli tooget ek adımlardır.</span><span class="sxs-lookup"><span data-stu-id="541e8-109">Additional steps are required tooget a user safely back into business.</span></span>

<span data-ttu-id="541e8-110">Bu konu, oluşabilecek tüm durumlarda bir kullanıcının oturum açma deneyimini genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="541e8-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="541e8-111">**Multi-Factor Authentication**</span><span class="sxs-lookup"><span data-stu-id="541e8-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="541e8-112">Çok faktörlü kimlik doğrulaması kayıt</span><span class="sxs-lookup"><span data-stu-id="541e8-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="541e8-113">**Risk altında oturum aç**</span><span class="sxs-lookup"><span data-stu-id="541e8-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="541e8-114">Oturum açma riskli kurtarma</span><span class="sxs-lookup"><span data-stu-id="541e8-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="541e8-115">Riskli oturum engellenen açma</span><span class="sxs-lookup"><span data-stu-id="541e8-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="541e8-116">Çok faktörlü kimlik doğrulaması kayıt sırasında bir riskli oturum açma</span><span class="sxs-lookup"><span data-stu-id="541e8-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="541e8-117">**Risk kullanıcı**</span><span class="sxs-lookup"><span data-stu-id="541e8-117">**User at risk**</span></span>

* <span data-ttu-id="541e8-118">Gizliliği tehlikeye giren hesap kurtarma</span><span class="sxs-lookup"><span data-stu-id="541e8-118">Compromised account recovery</span></span>
* <span data-ttu-id="541e8-119">Engellenen gizliliği tehlikeye giren hesap</span><span class="sxs-lookup"><span data-stu-id="541e8-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="541e8-120">Çok faktörlü kimlik doğrulaması kayıt</span><span class="sxs-lookup"><span data-stu-id="541e8-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="541e8-121">her ikisi için de en iyi kullanıcı deneyimini Merhaba, gizliliği tehlikeye giren hesap kurtarma akışı hello ve oturum açma riskli akış Merhaba, hello kullanıcı kendi kendine kurtarabilirsiniz durumdur.</span><span class="sxs-lookup"><span data-stu-id="541e8-121">hello best user experience for both, hello compromised account recovery flow and hello risky sign-in flow, is when hello user can self-recover.</span></span> <span data-ttu-id="541e8-122">Kullanıcılar için multi-Factor authentication kaydettiyseniz, zaten kullanılan toopass güvenlik tehditlerine olabilir, hesabıyla ilişkili bir telefon numarası sahiptirler.</span><span class="sxs-lookup"><span data-stu-id="541e8-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used toopass security challenges.</span></span> <span data-ttu-id="541e8-123">Yardım masasına veya yöneticinize katılımı hesabı güvenliğinin aşılmasına gelen gerekli toorecover ' dir.</span><span class="sxs-lookup"><span data-stu-id="541e8-123">No help desk or administrator involvement is needed toorecover from account compromise.</span></span> <span data-ttu-id="541e8-124">Bu nedenle, tooget kullanıcılarınızın tavsiye çok faktörlü kimlik doğrulaması için kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="541e8-124">Thus, it’s highly recommended tooget your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="541e8-125">Yöneticiler şunları yapabilir:</span><span class="sxs-lookup"><span data-stu-id="541e8-125">Administrators can:</span></span>

* <span data-ttu-id="541e8-126">Kullanıcıların tooset kendi hesaplarını ek güvenlik doğrulaması gerektiren bir ilke ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="541e8-126">set a policy that requires users tooset up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="541e8-127">çok faktörlü kimlik doğrulaması kayıt too30 günlerini atlanıyor toogive kullanıcıların istedikleri durumunda izin kaydetmeden önce bir yetkisiz kullanım süresi.</span><span class="sxs-lookup"><span data-stu-id="541e8-127">allow skipping multi-factor authentication registration for up too30 days, in case they want toogive users a grace period before registering.</span></span>

<span data-ttu-id="541e8-128">**Merhaba çok faktörlü kimlik doğrulaması kayıt üç adım vardır:**</span><span class="sxs-lookup"><span data-stu-id="541e8-128">**hello multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="541e8-129">Merhaba ilk adımda hello kullanıcı hello gereksinim tooset hello hesabı çok faktörlü kimlik doğrulama kaydınızı hakkında bir bildirim alır.</span><span class="sxs-lookup"><span data-stu-id="541e8-129">In hello first step, hello user gets a notification about hello requirement tooset hello account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="541e8-130">![Düzeltme](./media/active-directory-identityprotection-flows/140.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="541e8-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="541e8-131">tooset çok faktörlü kimlik doğrulamasını kurma toolet hello sistem ihtiyacınız temas toobe istediğiniz bildirin.</span><span class="sxs-lookup"><span data-stu-id="541e8-131">tooset multi-factor authentication up, you need toolet hello system know how you want toobe contacted.</span></span>
   
    <span data-ttu-id="541e8-132">![Düzeltme](./media/active-directory-identityprotection-flows/141.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="541e8-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="541e8-133">bir challenge tooyou Hello sistem gönderir ve toorespond gerekir.</span><span class="sxs-lookup"><span data-stu-id="541e8-133">hello system submits a challenge tooyou and you need toorespond.</span></span>
   
    <span data-ttu-id="541e8-134">![Düzeltme](./media/active-directory-identityprotection-flows/142.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="541e8-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="541e8-135">Oturum açma riskli kurtarma</span><span class="sxs-lookup"><span data-stu-id="541e8-135">Risky sign-in recovery</span></span>
<span data-ttu-id="541e8-136">Yönetici oturum açma riskler için bir ilke şekilde yapılandırdığında toosign içinde çalıştıklarında hello etkilenen kullanıcılara bildirilir.</span><span class="sxs-lookup"><span data-stu-id="541e8-136">When an administrator has configured a policy for sign-in risks, hello affected users are notified when they try toosign-in.</span></span> 

<span data-ttu-id="541e8-137">**oturum açma Hello riskli akışı iki adımı vardır:**</span><span class="sxs-lookup"><span data-stu-id="541e8-137">**hello risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="541e8-138">olağan dışı bir şey hakkında kendi oturum yeni konumu, cihaz veya uygulama oturum açma gibi algılandı Hello kullanıcı bilgilendirilir.</span><span class="sxs-lookup"><span data-stu-id="541e8-138">hello user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="541e8-139">![Düzeltme](./media/active-directory-identityprotection-flows/120.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="541e8-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="541e8-140">Merhaba kullanıcı gerekli tooprove kendi güvenlik sınaması çözme tarafından kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="541e8-140">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="541e8-141">Merhaba kullanıcı çok faktörlü kimlik doğrulaması için kayıtlı değilse tooround seyahat bir güvenlik kodu tootheir telefon numarası ihtiyaç duyar.</span><span class="sxs-lookup"><span data-stu-id="541e8-141">If hello user is registered for multi-factor authentication they need tooround-trip a security code tootheir phone number.</span></span> <span data-ttu-id="541e8-142">Bu yalnızca bir olduğundan riskli bir oturum açma ve güvenliği aşılmış bir hesabı değil, hello kullanıcı bu akışında toochange hello parola sahip olmaz.</span><span class="sxs-lookup"><span data-stu-id="541e8-142">Since this is a just a risky sign in and not a compromised account, hello user won’t have toochange hello password in this flow.</span></span> 
   
    <span data-ttu-id="541e8-143">![Düzeltme](./media/active-directory-identityprotection-flows/121.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="541e8-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="541e8-144">Riskli oturum engellenen açma</span><span class="sxs-lookup"><span data-stu-id="541e8-144">Risky sign-in blocked</span></span>
<span data-ttu-id="541e8-145">Yöneticiler, bir oturum açma riski İlkesi tooblock kullanıcılar oturum açma hello risk düzeyi bağlı olarak bağlı tooset de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="541e8-145">Administrators can also choose tooset a Sign-In Risk policy tooblock users upon sign-in depending on hello risk level.</span></span> <span data-ttu-id="541e8-146">engeli kaldırılmış tooget, son kullanıcıların yöneticinize veya yardım masasına başvurun veya tanıdık konumu ya da cihaz açmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="541e8-146">tooget unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="541e8-147">Çok faktörlü kimlik doğrulaması çözme tarafından otomatik olarak kurtarma seçeneği bu durumda değil.</span><span class="sxs-lookup"><span data-stu-id="541e8-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="541e8-148">![Düzeltme](./media/active-directory-identityprotection-flows/200.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="541e8-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="541e8-149">Gizliliği tehlikeye giren hesap kurtarma</span><span class="sxs-lookup"><span data-stu-id="541e8-149">Compromised account recovery</span></span>
<span data-ttu-id="541e8-150">Bir kullanıcı risk Güvenlik İlkesi yapılandırıldığında hello kullanıcı karşılayan kullanıcılar risk düzeyi hello İlkesi'nde belirtilen (ve bu nedenle varsayılır tehlikeye), oturum açma önce hello kullanıcı güvenliğinin aşılmasına kurtarma aktığı gitmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="541e8-150">When a user risk security policy has been configured, users who meet hello user risk level specified in hello policy (and are therefore assumed compromised) must go through hello user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="541e8-151">**Merhaba kullanıcı güvenliğinin aşılmasına kurtarma akışı üç adım vardır:**</span><span class="sxs-lookup"><span data-stu-id="541e8-151">**hello user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="541e8-152">Merhaba kullanıcı, kendi hesabı güvenlik riski nedeniyle şüpheli etkinlik olduğu veya kimlik bilgilerini sızmasını bilgilendirilir.</span><span class="sxs-lookup"><span data-stu-id="541e8-152">hello user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="541e8-153">![Düzeltme](./media/active-directory-identityprotection-flows/101.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="541e8-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="541e8-154">Merhaba kullanıcı gerekli tooprove kendi güvenlik sınaması çözme tarafından kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="541e8-154">hello user is required tooprove their identity by solving a security challenge.</span></span> <span data-ttu-id="541e8-155">Merhaba kullanıcı çok faktörlü kimlik doğrulaması için kayıtlı değilse, güvenliğinin bozulması riskini Self kurtarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="541e8-155">If hello user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="541e8-156">Bunlar tooround seyahat bir güvenlik kodu tootheir telefon numarası gerekir.</span><span class="sxs-lookup"><span data-stu-id="541e8-156">They will need tooround-trip a security code tootheir phone number.</span></span> 
   
   <span data-ttu-id="541e8-157">![Düzeltme](./media/active-directory-identityprotection-flows/110.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="541e8-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="541e8-158">Son olarak, kullanıcı hello zorlanmış toochange parolalarını olduğu başka birisi erişim tootheir hesabı olmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="541e8-158">Finally, hello user is forced toochange their password since someone else may have had access tootheir account.</span></span> 
   <span data-ttu-id="541e8-159">Aşağıda bu deneyim ekran görüntüleri verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="541e8-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="541e8-160">![Düzeltme](./media/active-directory-identityprotection-flows/111.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="541e8-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="541e8-161">Engellenen gizliliği tehlikeye giren hesap</span><span class="sxs-lookup"><span data-stu-id="541e8-161">Compromised account blocked</span></span>
<span data-ttu-id="541e8-162">tooget engeli kaldırılmış bir kullanıcı risk güvenlik ilkesi tarafından engellenen bir kullanıcı, hello kullanıcı bir yönetici veya yardım masasına başvurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="541e8-162">tooget a user that was blocked by a user risk security policy unblocked, hello user must contact an administrator or help desk.</span></span> <span data-ttu-id="541e8-163">Çok faktörlü kimlik doğrulaması çözme tarafından otomatik olarak kurtarma seçeneği bu durumda değil.</span><span class="sxs-lookup"><span data-stu-id="541e8-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="541e8-164">![Düzeltme](./media/active-directory-identityprotection-flows/104.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="541e8-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="541e8-165">Parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="541e8-165">Reset password</span></span>
<span data-ttu-id="541e8-166">Güvenliği aşılmış kullanıcıların açmasını engellenirse yönetici kendileri için geçici bir parola oluşturun.</span><span class="sxs-lookup"><span data-stu-id="541e8-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="541e8-167">Merhaba kullanıcılar toochange, bir sonraki oturum açma sırasında parolalarını sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="541e8-167">hello users will have toochange their password during a next sign-in.</span></span>

<span data-ttu-id="541e8-168">![Düzeltme](./media/active-directory-identityprotection-flows/160.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="541e8-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="541e8-169">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="541e8-169">See also</span></span>
* [<span data-ttu-id="541e8-170">Azure Active Directory kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="541e8-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

