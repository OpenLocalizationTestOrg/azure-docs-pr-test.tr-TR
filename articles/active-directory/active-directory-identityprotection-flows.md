---
title: "Azure AD kimlik koruması ile karşılaştığında oturum açma | Microsoft Docs"
description: "Kimlik koruması azaltıldığından veya bir kullanıcı düzeltilen veya çok faktörlü kimlik doğrulama İlkesi tarafından istendiğinde kullanıcı deneyimini genel bir bakış sağlar."
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
ms.openlocfilehash: e45936280b51fb2e54012a688fceddcc8dabe984
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-experiences-with-azure-ad-identity-protection"></a><span data-ttu-id="43154-104">Oturum açma deneyimlerini Azure AD kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="43154-104">Sign-in experiences with Azure AD Identity Protection</span></span>
<span data-ttu-id="43154-105">Azure Active Directory kimlik koruması ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="43154-105">With Azure Active Directory Identity Protection, you can:</span></span>

* <span data-ttu-id="43154-106">çok faktörlü kimlik doğrulaması için kullanıcıların</span><span class="sxs-lookup"><span data-stu-id="43154-106">require users to register for multi-factor authentication</span></span>
* <span data-ttu-id="43154-107">riskli oturum açma işlemleri ve güvenliği aşılan kullanıcılar işleme</span><span class="sxs-lookup"><span data-stu-id="43154-107">handle risky sign-ins and compromised users</span></span>

<span data-ttu-id="43154-108">Bu sorunları sistem yanıta sahip bir kullanıcının oturum açma deneyimi üzerinde bir etkisi yalnızca doğrudan imzalama kullanıcı adını sağlayarak bileşenini olduğundan ve bir parola artık mümkün olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="43154-108">The response of the system to these issues has an impact on a user's sign-in experience because just directly signing-in by providing a user name and a password won't be possible anymore.</span></span> <span data-ttu-id="43154-109">Bir kullanıcı güvenli bir şekilde almak için gereken ek adımlar iş uygulamasına geri.</span><span class="sxs-lookup"><span data-stu-id="43154-109">Additional steps are required to get a user safely back into business.</span></span>

<span data-ttu-id="43154-110">Bu konu, oluşabilecek tüm durumlarda bir kullanıcının oturum açma deneyimini genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="43154-110">This topic gives you an overview of a user's sign-in experience for all cases that can occur.</span></span>

<span data-ttu-id="43154-111">**Multi-Factor Authentication**</span><span class="sxs-lookup"><span data-stu-id="43154-111">**Multi-factor authentication**</span></span>

* <span data-ttu-id="43154-112">Çok faktörlü kimlik doğrulaması kayıt</span><span class="sxs-lookup"><span data-stu-id="43154-112">Multi-factor authentication registration</span></span>

<span data-ttu-id="43154-113">**Risk altında oturum aç**</span><span class="sxs-lookup"><span data-stu-id="43154-113">**Sign-in at risk**</span></span>

* <span data-ttu-id="43154-114">Oturum açma riskli kurtarma</span><span class="sxs-lookup"><span data-stu-id="43154-114">Risky sign-in recovery</span></span>
* <span data-ttu-id="43154-115">Riskli oturum engellenen açma</span><span class="sxs-lookup"><span data-stu-id="43154-115">Risky sign-in blocked</span></span>
* <span data-ttu-id="43154-116">Çok faktörlü kimlik doğrulaması kayıt sırasında bir riskli oturum açma</span><span class="sxs-lookup"><span data-stu-id="43154-116">Multi-factor authentication registration during a risky sign-in</span></span>

<span data-ttu-id="43154-117">**Risk kullanıcı**</span><span class="sxs-lookup"><span data-stu-id="43154-117">**User at risk**</span></span>

* <span data-ttu-id="43154-118">Gizliliği tehlikeye giren hesap kurtarma</span><span class="sxs-lookup"><span data-stu-id="43154-118">Compromised account recovery</span></span>
* <span data-ttu-id="43154-119">Engellenen gizliliği tehlikeye giren hesap</span><span class="sxs-lookup"><span data-stu-id="43154-119">Compromised account blocked</span></span>

## <a name="multi-factor-authentication-registration"></a><span data-ttu-id="43154-120">Çok faktörlü kimlik doğrulaması kayıt</span><span class="sxs-lookup"><span data-stu-id="43154-120">Multi-factor authentication registration</span></span>
<span data-ttu-id="43154-121">En iyi kullanıcı deneyimi, gizliliği tehlikeye giren hesap kurtarma akışı hem hem de riskli oturum açma akışını, kullanıcının kendi kendine kurtarabilirsiniz durumdur.</span><span class="sxs-lookup"><span data-stu-id="43154-121">The best user experience for both, the compromised account recovery flow and the risky sign-in flow, is when the user can self-recover.</span></span> <span data-ttu-id="43154-122">Kullanıcılar için multi-Factor authentication kaydettiyseniz, zaten güvenlik tehditlerine geçirmek için kullanılan kendi hesabıyla ilişkili bir telefon numarası sahiptirler.</span><span class="sxs-lookup"><span data-stu-id="43154-122">If users are registered for multi-factor authentication, they already have a phone number associated with their account that can be used to pass security challenges.</span></span> <span data-ttu-id="43154-123">Yardım masasına veya yöneticinize katılımı hesap bozulmayacak kurtarmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="43154-123">No help desk or administrator involvement is needed to recover from account compromise.</span></span> <span data-ttu-id="43154-124">Bu nedenle, çok faktörlü kimlik doğrulaması için kayıtlı kullanıcılarınızın almak için tavsiye.</span><span class="sxs-lookup"><span data-stu-id="43154-124">Thus, it’s highly recommended to get your users registered for multi-factor authentication.</span></span> 

<span data-ttu-id="43154-125">Yöneticiler şunları yapabilir:</span><span class="sxs-lookup"><span data-stu-id="43154-125">Administrators can:</span></span>

* <span data-ttu-id="43154-126">ek güvenlik doğrulaması hesaplarını ayarlamak kullanıcıların gerektiren bir ilke ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="43154-126">set a policy that requires users to set up their accounts for additional security verification.</span></span> 
* <span data-ttu-id="43154-127">yetkisiz kullanım süresi kaydetmeden önce bir kullanıcılara vermek istediğiniz durumda 30 güne kadar çok faktörlü kimlik doğrulaması kaydı atlanıyor izin verir.</span><span class="sxs-lookup"><span data-stu-id="43154-127">allow skipping multi-factor authentication registration for up to 30 days, in case they want to give users a grace period before registering.</span></span>

<span data-ttu-id="43154-128">**Çok faktörlü kimlik doğrulaması kayıt üç adım vardır:**</span><span class="sxs-lookup"><span data-stu-id="43154-128">**The multi-factor authentication registration has three steps:**</span></span>

1. <span data-ttu-id="43154-129">İlk adımda, kullanıcı hesabı çok faktörlü kimlik doğrulama kaydınızı ayarlamak için gereksinimi hakkında bir bildirim alır.</span><span class="sxs-lookup"><span data-stu-id="43154-129">In the first step, the user gets a notification about the requirement to set the account up for multi-factor authentication.</span></span> 
   
    <span data-ttu-id="43154-130">![Düzeltme](./media/active-directory-identityprotection-flows/140.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="43154-130">![Remediation](./media/active-directory-identityprotection-flows/140.png "Remediation")</span></span>
2. <span data-ttu-id="43154-131">Çok faktörlü kimlik doğrulamasını ayarlamak için nasıl kurulmasını istediğinizi bilmeniz sistem izin gerekir.</span><span class="sxs-lookup"><span data-stu-id="43154-131">To set multi-factor authentication up, you need to let the system know how you want to be contacted.</span></span>
   
    <span data-ttu-id="43154-132">![Düzeltme](./media/active-directory-identityprotection-flows/141.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="43154-132">![Remediation](./media/active-directory-identityprotection-flows/141.png "Remediation")</span></span>
3. <span data-ttu-id="43154-133">Sistem için bir sınama gönderir ve yanıt vermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="43154-133">The system submits a challenge to you and you need to respond.</span></span>
   
    <span data-ttu-id="43154-134">![Düzeltme](./media/active-directory-identityprotection-flows/142.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="43154-134">![Remediation](./media/active-directory-identityprotection-flows/142.png "Remediation")</span></span>

## <a name="risky-sign-in-recovery"></a><span data-ttu-id="43154-135">Oturum açma riskli kurtarma</span><span class="sxs-lookup"><span data-stu-id="43154-135">Risky sign-in recovery</span></span>
<span data-ttu-id="43154-136">Yönetici oturum açma riskler için bir ilke yapılandırıldığında, bu oturum açma çalıştıklarında etkilenen kullanıcılara bildirilir.</span><span class="sxs-lookup"><span data-stu-id="43154-136">When an administrator has configured a policy for sign-in risks, the affected users are notified when they try to sign-in.</span></span> 

<span data-ttu-id="43154-137">**Riskli oturum açma akışını iki adımı vardır:**</span><span class="sxs-lookup"><span data-stu-id="43154-137">**The risky sign-in flow has two steps:**</span></span> 

1. <span data-ttu-id="43154-138">Olağan dışı bir şey hakkında kendi oturum yeni konumu, cihaz veya uygulama oturum açma gibi algılandı kullanıcı bilgilendirilir.</span><span class="sxs-lookup"><span data-stu-id="43154-138">The user is informed that something unusual was detected about their sign-in, such as signing in from a new location, device, or app.</span></span> 
   
    <span data-ttu-id="43154-139">![Düzeltme](./media/active-directory-identityprotection-flows/120.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="43154-139">![Remediation](./media/active-directory-identityprotection-flows/120.png "Remediation")</span></span>
2. <span data-ttu-id="43154-140">Kullanıcı güvenlik sınaması çözme tarafından kimliğini kanıtlamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="43154-140">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="43154-141">Kullanıcı çok faktörlü kimlik doğrulaması için kayıtlı değilse kullanıcıların telefon numarasına bir güvenlik kodu gidiş için gerekir.</span><span class="sxs-lookup"><span data-stu-id="43154-141">If the user is registered for multi-factor authentication they need to round-trip a security code to their phone number.</span></span> <span data-ttu-id="43154-142">Bu yalnızca bir olduğundan riskli bir oturum açma ve güvenliği aşılmış bir hesabı değil, kullanıcı bu akış parolayı değiştirmek zorunda kalmazsınız.</span><span class="sxs-lookup"><span data-stu-id="43154-142">Since this is a just a risky sign in and not a compromised account, the user won’t have to change the password in this flow.</span></span> 
   
    <span data-ttu-id="43154-143">![Düzeltme](./media/active-directory-identityprotection-flows/121.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="43154-143">![Remediation](./media/active-directory-identityprotection-flows/121.png "Remediation")</span></span>

## <a name="risky-sign-in-blocked"></a><span data-ttu-id="43154-144">Riskli oturum engellenen açma</span><span class="sxs-lookup"><span data-stu-id="43154-144">Risky sign-in blocked</span></span>
<span data-ttu-id="43154-145">Yöneticiler, blok kullanıcılar oturum açma risk düzeyine bağlı olarak bağlı bir oturum açma riski ilkesini ayarlamak de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43154-145">Administrators can also choose to set a Sign-In Risk policy to block users upon sign-in depending on the risk level.</span></span> <span data-ttu-id="43154-146">Engeli almak için son kullanıcıların bir yönetici veya yardım masasına başvurmanız gerekir veya tanıdık konumu ya da cihaz açmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="43154-146">To get unblocked, end users must contact an administrator or help desk, or they can try signing in from a familiar location or device.</span></span> <span data-ttu-id="43154-147">Çok faktörlü kimlik doğrulaması çözme tarafından otomatik olarak kurtarma seçeneği bu durumda değil.</span><span class="sxs-lookup"><span data-stu-id="43154-147">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="43154-148">![Düzeltme](./media/active-directory-identityprotection-flows/200.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="43154-148">![Remediation](./media/active-directory-identityprotection-flows/200.png "Remediation")</span></span>

## <a name="compromised-account-recovery"></a><span data-ttu-id="43154-149">Gizliliği tehlikeye giren hesap kurtarma</span><span class="sxs-lookup"><span data-stu-id="43154-149">Compromised account recovery</span></span>
<span data-ttu-id="43154-150">Bir kullanıcı risk Güvenlik İlkesi yapılandırıldığında kullanıcı karşılayan kullanıcılar risk düzeyi İlkesi'nde belirtilen (ve bu nedenle varsayılır tehlikeye), oturum açma önce kullanıcı güvenliğinin aşılmasına kurtarma aktığı gitmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="43154-150">When a user risk security policy has been configured, users who meet the user risk level specified in the policy (and are therefore assumed compromised) must go through the user compromise recovery flow before they can sign-in.</span></span> 

<span data-ttu-id="43154-151">**Kullanıcı güvenlik aşılması kurtarma akışı üç adım vardır:**</span><span class="sxs-lookup"><span data-stu-id="43154-151">**The user compromise recovery flow has three steps:**</span></span>

1. <span data-ttu-id="43154-152">Kullanıcı, kendi hesabı güvenlik riski nedeniyle şüpheli etkinlik olduğu veya kimlik bilgilerini sızmasını bilgilendirilir.</span><span class="sxs-lookup"><span data-stu-id="43154-152">The user is informed that their account security is at risk because of suspicious activity or leaked credentials.</span></span>
   
    <span data-ttu-id="43154-153">![Düzeltme](./media/active-directory-identityprotection-flows/101.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="43154-153">![Remediation](./media/active-directory-identityprotection-flows/101.png "Remediation")</span></span>
2. <span data-ttu-id="43154-154">Kullanıcı güvenlik sınaması çözme tarafından kimliğini kanıtlamak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="43154-154">The user is required to prove their identity by solving a security challenge.</span></span> <span data-ttu-id="43154-155">Kullanıcı çok faktörlü kimlik doğrulaması için kayıtlı değilse, güvenliğinin bozulması riskini Self kurtarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="43154-155">If the user is registered for multi-factor authentication they can self-recover from being compromised.</span></span> <span data-ttu-id="43154-156">Bunlar için gidiş telefon numarasına bir güvenlik kodu gerekir.</span><span class="sxs-lookup"><span data-stu-id="43154-156">They will need to round-trip a security code to their phone number.</span></span> 
   
   <span data-ttu-id="43154-157">![Düzeltme](./media/active-directory-identityprotection-flows/110.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="43154-157">![Remediation](./media/active-directory-identityprotection-flows/110.png "Remediation")</span></span>
3. <span data-ttu-id="43154-158">Son olarak, kullanıcı, başka birinin kendi hesaplarına erişim sağlamış olma ihtimaline parolalarını değiştirmek için zorlanır.</span><span class="sxs-lookup"><span data-stu-id="43154-158">Finally, the user is forced to change their password since someone else may have had access to their account.</span></span> 
   <span data-ttu-id="43154-159">Aşağıda bu deneyim ekran görüntüleri verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="43154-159">Screenshots of this experience are below.</span></span>
   
   <span data-ttu-id="43154-160">![Düzeltme](./media/active-directory-identityprotection-flows/111.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="43154-160">![Remediation](./media/active-directory-identityprotection-flows/111.png "Remediation")</span></span>

## <a name="compromised-account-blocked"></a><span data-ttu-id="43154-161">Engellenen gizliliği tehlikeye giren hesap</span><span class="sxs-lookup"><span data-stu-id="43154-161">Compromised account blocked</span></span>
<span data-ttu-id="43154-162">Engeli kaldırılmış bir kullanıcı risk güvenlik ilkesi tarafından engellenen bir kullanıcı almak için kullanıcı bir yöneticiye başvurun veya Yardım Masası gerekir.</span><span class="sxs-lookup"><span data-stu-id="43154-162">To get a user that was blocked by a user risk security policy unblocked, the user must contact an administrator or help desk.</span></span> <span data-ttu-id="43154-163">Çok faktörlü kimlik doğrulaması çözme tarafından otomatik olarak kurtarma seçeneği bu durumda değil.</span><span class="sxs-lookup"><span data-stu-id="43154-163">Self-recovering by solving multi-factor authentication is not an option in this case.</span></span>

<span data-ttu-id="43154-164">![Düzeltme](./media/active-directory-identityprotection-flows/104.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="43154-164">![Remediation](./media/active-directory-identityprotection-flows/104.png "Remediation")</span></span>

## <a name="reset-password"></a><span data-ttu-id="43154-165">Parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="43154-165">Reset password</span></span>
<span data-ttu-id="43154-166">Güvenliği aşılmış kullanıcıların açmasını engellenirse yönetici kendileri için geçici bir parola oluşturun.</span><span class="sxs-lookup"><span data-stu-id="43154-166">If compromised users are blocked from signing in, an administrator can generate a temporary password for them.</span></span> <span data-ttu-id="43154-167">Kullanıcıların, bir sonraki oturum açma sırasında parolalarını değiştirmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="43154-167">The users will have to change their password during a next sign-in.</span></span>

<span data-ttu-id="43154-168">![Düzeltme](./media/active-directory-identityprotection-flows/160.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="43154-168">![Remediation](./media/active-directory-identityprotection-flows/160.png "Remediation")</span></span>

## <a name="see-also"></a><span data-ttu-id="43154-169">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="43154-169">See also</span></span>
* [<span data-ttu-id="43154-170">Azure Active Directory kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="43154-170">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md) 

