---
title: "Active Directory kimlik koruması aaaAzure | Microsoft Docs"
description: "Nasıl Azure AD Identity Protection toolimit hello yeteneğini bir saldırganın tooexploit güvenliği aşılmış kimlik veya cihaz ve bir kimlik veya şüpheli veya bilinen toobe öncekinden bir aygıtı tehlikeye toosecure sağlar öğrenin."
services: active-directory
keywords: "Azure active directory kimlik koruması, cloud app discovery'yi, uygulamalar, güvenlik, risk, risk düzeyi, güvenlik açığı, güvenlik ilkesi yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: e7434eeb-4e98-4b6b-a895-b5598a6cccf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ecca4f3cdb65585687cf44a80024f26c7cab22ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="d4cc7-104">Azure Active Directory Kimlik Koruması</span><span class="sxs-lookup"><span data-stu-id="d4cc7-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="d4cc7-105">Azure Active Directory kimlik koruması sağlar hello Azure AD Premium P2 edition özelliğidir:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-105">Azure Active Directory Identity Protection is a feature of hello Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="d4cc7-106">Kuruluşunuzdaki kimlikleri etkileyen olası güvenlik açıklarını algılama</span><span class="sxs-lookup"><span data-stu-id="d4cc7-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="d4cc7-107">İlgili tooyour kuruluşunuzun kimlikleri otomatik yanıtlar toodetected şüpheli Eylemler yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d4cc7-107">Configure automated responses toodetected suspicious actions that are related tooyour organization’s identities</span></span>  

- <span data-ttu-id="d4cc7-108">Şüpheli olayları araştırmanıza ve uygun eylemi tooresolve ele bunları</span><span class="sxs-lookup"><span data-stu-id="d4cc7-108">Investigate suspicious incidents and take appropriate action tooresolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="d4cc7-109">Başlarken</span><span class="sxs-lookup"><span data-stu-id="d4cc7-109">Getting started</span></span>

<span data-ttu-id="d4cc7-110">Microsoft bulut tabanlı kimlikleri birden fazla bir süredir güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="d4cc7-111">Azure Active Directory kimlik koruması ile ortamınızda hello kullanabilirsiniz aynı koruma sistemleri Microsoft toosecure kimlikleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-111">With Azure Active Directory Identity Protection, in your environment, you can use hello same protection systems Microsoft uses toosecure identities.</span></span>

<span data-ttu-id="d4cc7-112">güvenlik ihlallerini ele Hello çoğunluğu saldırganların bir kullanıcının kimliğini çalarak erişim tooan ortamı elde zaman yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-112">hello vast majority of security breaches take place when attackers gain access tooan environment by stealing a user’s identity.</span></span> <span data-ttu-id="d4cc7-113">Merhaba yıllar içinde saldırganlar üçüncü taraf ihlallerini yararlanan ve Gelişmiş kimlik avı saldırıları kullanarak giderek etkin hale getirildi.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-113">Over hello years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="d4cc7-114">Bir saldırgan tooeven düşük ayrıcalıklı kullanıcı hesaplarına erişim kazanır hemen bunları toogain tooimportant şirket kaynaklarına yanal hareket aracılığıyla için görece olarak daha kolay.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-114">As soon as an attacker gains access tooeven low privileged user accounts, it is relatively easy for them toogain access tooimportant company resources through lateral movement.</span></span>

<span data-ttu-id="d4cc7-115">Bu gruplarındaki sonucu olarak, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="d4cc7-116">Ayrıcalık düzeylerini bağımsız olarak tüm kimlikleri koru</span><span class="sxs-lookup"><span data-stu-id="d4cc7-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="d4cc7-117">Proaktif olarak kötüye gelen güvenliği aşılmış kimlik engelle</span><span class="sxs-lookup"><span data-stu-id="d4cc7-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="d4cc7-118">Güvenliği aşılmış kimlikleri keşfetme hiçbir kolay bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="d4cc7-119">Buluşsal yöntemler toodetect anormallikleri ve potansiyel olarak belirtmek şüpheli olayları kimlikleri riske ve Azure Active Directory Uyarlamalı machine learning algoritmaları kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="d4cc7-120">Bu verileri kullanarak, kimlik koruması raporları oluşturur ve, tooevaluate hello etkinleştirmek uyarılar ilgili sorunlar algıladı ve uygun azaltma veya düzeltme eylemlerini gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-120">Using this data, Identity Protection generates reports and alerts that enable you tooevaluate hello detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="d4cc7-121">Azure Active Directory kimlik koruması izleme ve Raporlama Aracı büyük.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="d4cc7-122">tooprotect kuruluşunuzdaki kimlikleri, belirtilen risk düzeyi erişildiğinde toodetected sorunları otomatik olarak yanıt veren risk tabanlı ilkeleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-122">tooprotect your organization's identities, you can configure risk-based policies that automatically respond toodetected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="d4cc7-123">Bu ilkeler ayrıca tooother koşullu erişim kontrolü Azure Active Directory ve EMS tarafından sağlanan, otomatik olarak engellemek ya da parola sıfırlama ve çok faktörlü kimlik doğrulaması zorlama gibi uyarlamalı düzeltme eylemleri başlatmak.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-123">These policies, in addition tooother conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="d4cc7-124">Kimlik koruma özellikleri</span><span class="sxs-lookup"><span data-stu-id="d4cc7-124">Identity Protection capabilities</span></span>

<span data-ttu-id="d4cc7-125">**Algılama Güvenlik Açıkları ve riskli hesapları:**</span><span class="sxs-lookup"><span data-stu-id="d4cc7-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="d4cc7-126">Özel öneriler tooimprove sağlayan güvenlik açıkları vurgulama tarafından genel güvenlik duruşunu</span><span class="sxs-lookup"><span data-stu-id="d4cc7-126">Providing custom recommendations tooimprove overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="d4cc7-127">Oturum açma risk düzeyleri hesaplama</span><span class="sxs-lookup"><span data-stu-id="d4cc7-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="d4cc7-128">Kullanıcı risk düzeyleri hesaplama</span><span class="sxs-lookup"><span data-stu-id="d4cc7-128">Calculating user risk levels</span></span>


<span data-ttu-id="d4cc7-129">**Risk olaylarını araştırma:**</span><span class="sxs-lookup"><span data-stu-id="d4cc7-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="d4cc7-130">Risk olayları için bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="d4cc7-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="d4cc7-131">Risk olaylarını ilgili ve bağlamsal bilgileri kullanarak araştırma</span><span class="sxs-lookup"><span data-stu-id="d4cc7-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="d4cc7-132">Tootrack araştırmalar temel iş akışı sağlama</span><span class="sxs-lookup"><span data-stu-id="d4cc7-132">Providing basic workflows tootrack investigations</span></span>
* <span data-ttu-id="d4cc7-133">Parola sıfırlama gibi tooremediation eylemleri kolay erişim sağlama</span><span class="sxs-lookup"><span data-stu-id="d4cc7-133">Providing easy access tooremediation actions such as password reset</span></span>

<span data-ttu-id="d4cc7-134">**Risk bağlı olarak koşullu erişim ilkeleri:**</span><span class="sxs-lookup"><span data-stu-id="d4cc7-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="d4cc7-135">İlke toomitigate riskli gerçekleştirilen oturum açma tarafından gerçekleştirilen oturum açma engelleme veya çok faktörlü kimlik doğrulaması zorluklarını gerektirerek.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-135">Policy toomitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="d4cc7-136">İlke tooblock veya güvenli riskli kullanıcı hesapları</span><span class="sxs-lookup"><span data-stu-id="d4cc7-136">Policy tooblock or secure risky user accounts</span></span>
* <span data-ttu-id="d4cc7-137">Çok faktörlü kimlik doğrulama İlkesi toorequire kullanıcılar tooregister</span><span class="sxs-lookup"><span data-stu-id="d4cc7-137">Policy toorequire users tooregister for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="d4cc7-138">Kimlik koruması rolleri</span><span class="sxs-lookup"><span data-stu-id="d4cc7-138">Identity Protection roles</span></span>

<span data-ttu-id="d4cc7-139">tooload Bakiye hello yönetim etkinliklerini kimlik koruması uygulamanız geçici çeşitli roller atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-139">tooload balance hello management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="d4cc7-140">Azure AD Identity Protection 3 dizin rollerini destekler:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="d4cc7-141">Rol</span><span class="sxs-lookup"><span data-stu-id="d4cc7-141">Role</span></span>                         | <span data-ttu-id="d4cc7-142">Yapabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d4cc7-142">Can do</span></span>                          | <span data-ttu-id="d4cc7-143">Yapamaz</span><span class="sxs-lookup"><span data-stu-id="d4cc7-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="d4cc7-144">Genel yönetici</span><span class="sxs-lookup"><span data-stu-id="d4cc7-144">Global administrator</span></span>         | <span data-ttu-id="d4cc7-145">Tam erişim tooIdentity koruma, yerleşik kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="d4cc7-145">Full access tooIdentity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="d4cc7-146">Güvenlik yöneticisi</span><span class="sxs-lookup"><span data-stu-id="d4cc7-146">Security administrator</span></span>       | <span data-ttu-id="d4cc7-147">Tam erişim tooIdentity koruma</span><span class="sxs-lookup"><span data-stu-id="d4cc7-147">Full access tooIdentity Protection</span></span> | <span data-ttu-id="d4cc7-148">Yerleşik kimlik koruması, bir kullanıcı parolalarını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="d4cc7-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="d4cc7-149">Güvenlik okuyucusu</span><span class="sxs-lookup"><span data-stu-id="d4cc7-149">Security reader</span></span>              | <span data-ttu-id="d4cc7-150">Yalnızca hazır erişim tooIdentity koruma</span><span class="sxs-lookup"><span data-stu-id="d4cc7-150">Ready-only access tooIdentity Protection</span></span> | <span data-ttu-id="d4cc7-151">Yerleşik kimlik koruması, remidiate kullanıcılar, ilkelerini yapılandırmak, parolaları sıfırlama</span><span class="sxs-lookup"><span data-stu-id="d4cc7-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="d4cc7-152">Daha fazla ayrıntı için bkz: [Azure Active Directory'de yönetici rolleri atama](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d4cc7-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="d4cc7-153">Algılama</span><span class="sxs-lookup"><span data-stu-id="d4cc7-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="d4cc7-154">Güvenlik Açıkları</span><span class="sxs-lookup"><span data-stu-id="d4cc7-154">Vulnerabilities</span></span>

<span data-ttu-id="d4cc7-155">Azure Active Directory kimlik koruması yapılandırmanızı analizleri yaparken ve kullanıcı kimlikleri üzerinde bir etkisi olabilir güvenlik açıkları algılar.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="d4cc7-156">Daha fazla ayrıntı için bkz: [Azure Active Directory kimlik koruması tarafından algılanan Güvenlik Açığı](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="d4cc7-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="d4cc7-157">Risk olayı</span><span class="sxs-lookup"><span data-stu-id="d4cc7-157">Risk events</span></span>

<span data-ttu-id="d4cc7-158">Azure Active Directory Uyarlamalı machine learning, ilgili tooyour kullanıcının kimlikleri algoritmaları ve buluşsal yöntemler toodetect şüpheli eylemleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user's identities.</span></span> <span data-ttu-id="d4cc7-159">Merhaba sistem algılanan her şüpheli eylemi için bir kayıt oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-159">hello system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="d4cc7-160">Bu kayıtları olarak da bilinen risk olaylardır.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="d4cc7-161">Daha ayrıntılı bilgi için bkz. [Azure Active Directory risk olayları](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="d4cc7-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="d4cc7-162">Araştırma</span><span class="sxs-lookup"><span data-stu-id="d4cc7-162">Investigation</span></span>
<span data-ttu-id="d4cc7-163">Yolculuğunuzun kimlik koruması aracılığıyla genellikle hello kimlik koruması panosu ile başlar.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-163">Your journey through Identity Protection typically starts with hello Identity Protection dashboard.</span></span>

<span data-ttu-id="d4cc7-164">![Düzeltme](./media/active-directory-identityprotection/1000.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="d4cc7-165">Merhaba Pano erişmenizi sağlar:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-165">hello dashboard gives you access to:</span></span>

* <span data-ttu-id="d4cc7-166">Gibi raporları **bayrak eklenen kullanıcılar için risk**, **Risk olayları** ve **güvenlik açıkları**</span><span class="sxs-lookup"><span data-stu-id="d4cc7-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="d4cc7-167">Merhaba yapılandırması gibi ayarları, **güvenlik ilkeleri**, **bildirimleri** ve **çok faktörlü kimlik doğrulaması kayıt**</span><span class="sxs-lookup"><span data-stu-id="d4cc7-167">Settings such as hello configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="d4cc7-168">Genellikle hello etkinlikleri, günlükler ve diğer ilgili bilgileri ilgili tooa risk olayı toodecide düzeltme veya azaltma adımları gerekli olup olmadığını gözden geçirme hello işlemidir, araştırma ve nasıl hello kimlik olduğu için başlangıç noktası. gizliliği ve nasıl hello kimlik tehlikeye anlamak kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-168">It is typically your starting point for investigation, which is hello process of reviewing hello activities, logs, and other relevant information related tooa risk event toodecide whether remediation or mitigation steps are necessary,  and how hello identity was compromised, and understand how hello compromised identity was used.</span></span>

<span data-ttu-id="d4cc7-169">Araştırma etkinlikleri toohello bağlayabilirsiniz [bildirimleri](active-directory-identityprotection-notifications.md) Azure Active Directory koruma e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-169">You can tie your investigation activities toohello [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="d4cc7-170">Merhaba aşağıdaki bölümler, daha fazla ayrıntı ve ilgili tooan araştırma hello adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-170">hello following sections provide you with more details and hello steps that are related tooan investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="d4cc7-171">Riskli oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="d4cc7-171">Risky sign-ins</span></span>

<span data-ttu-id="d4cc7-172">Azure Active Directory algılar [risk olayı türleri](active-directory-reporting-risk-events.md#risk-event-types) gerçek zamanlı ve çevrimdışı.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="d4cc7-173">Bir oturum açma için kullanıcı algılanan her risk olayı tooa mantıksal kavram riskli oturum açma adı verilen katkıda bulunur.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-173">Each risk event that has been detected for a sign-in of a user contributes tooa logical concept called risky sign-in.</span></span> <span data-ttu-id="d4cc7-174">Bir riskli oturum açma bir hello yasal sahibi bir kullanıcı hesabı tarafından gerçekleştirilmiş olabilecek olmayan bir oturum açma girişimi için göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by hello legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="d4cc7-175">Oturum açma risk düzeyi</span><span class="sxs-lookup"><span data-stu-id="d4cc7-175">Sign-in risk level</span></span>

<span data-ttu-id="d4cc7-176">Oturum açma risk düzeyi bir oturum açma girişimi hello yasal sahibi bir kullanıcı hesabı tarafından gerçekleştirilmedi bir (yüksek, Orta veya düşük) hello olasılığını göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-176">A sign-in risk level is an indication (High, Medium, or Low) of hello likelihood that a sign-in attempt was not performed by hello legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="d4cc7-177">Oturum açma riski olaylar azaltılması</span><span class="sxs-lookup"><span data-stu-id="d4cc7-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="d4cc7-178">Bir azaltma bir eylem toolimit hello bir saldırganın tooexploit güvenliği aşılmış kimlik veya hello kimliği veya cihaza tooa güvenli geri yükleme durumunda olmadan cihaz özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-178">A mitigation is an action toolimit hello ability of an attacker tooexploit a compromised identity or device without restoring hello identity or device tooa safe state.</span></span> <span data-ttu-id="d4cc7-179">Bir azaltma hello kimlik veya aygıtla ilişkili önceki oturum açma risk olaylarını çözümlenmiyor.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-179">A mitigation does not resolve previous sign-in risk events associated with hello identity or device.</span></span>

<span data-ttu-id="d4cc7-180">toomitigate riskli gerçekleştirilen oturum açma, oturum açma riski güvenlik policicies otomatik olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-180">toomitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="d4cc7-181">Hello kullanıcı veya oturum açma hello tooblock hello risk düzeyi riskli oturum açma işlemleri göz önünde bulundurun bu ilkeleri kullanarak veya hello kullanıcı tooperform çok faktörlü kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-181">Using these policies, you consider hello risk level of hello user or hello sign-in tooblock risky sign-ins or require hello user tooperform multi-factor authentication.</span></span> <span data-ttu-id="d4cc7-182">Bu Eylemler, bir saldırganın çalınan kimlik toocause zarar yararlanmasını engelleyebilir ve bazı zaman toosecure hello kimlik verebilir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-182">These actions may prevent an attacker from exploiting a stolen identity toocause damage, and may give you some time toosecure hello identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="d4cc7-183">Oturum açma riski güvenlik ilkesi</span><span class="sxs-lookup"><span data-stu-id="d4cc7-183">Sign-in risk security policy</span></span>
<span data-ttu-id="d4cc7-184">Oturum açma riski hello risk tooa belirli oturum açma değerlendirir ve önceden tanımlanmış koşullara ve kurallarına göre Azaltıcı geçerlidir bir koşullu erişim ilkesi ilkesidir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-184">A sign-in risk policy is a conditional access policy that evaluates hello risk tooa specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="d4cc7-185">![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1014.png "risk ilkesine oturum açma")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="d4cc7-186">Azure AD kimlik koruması olanak tanıyarak hello azaltma riskli oturum açma işlemleri durumunu yönetmenize yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-186">Azure AD Identity Protection helps you manage hello mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="d4cc7-187">Kullanıcılar ve gruplar hello ilkenin uygulandığı hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-187">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="d4cc7-188">![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1015.png "risk ilkesine oturum açma")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="d4cc7-189">Hello İlkesi tetikleyen hello oturum açma risk düzeyi eşiği (düşük, Orta veya yüksek) ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-189">Set hello sign-in risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="d4cc7-190">![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1016.png "risk ilkesine oturum açma")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="d4cc7-191">Set hello denetimleri toobe Hello İlkesi tetikler zorunlu tutulur:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-191">Set hello controls toobe enforced when hello policy triggers:</span></span>  

    <span data-ttu-id="d4cc7-192">![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1017.png "risk ilkesine oturum açma")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="d4cc7-193">Anahtar hello durumunu ilkenizin:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-193">Switch hello state of your policy:</span></span>

    <span data-ttu-id="d4cc7-194">![MFA kayıt](./media/active-directory-identityprotection/403.png "MFA kayıt")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="d4cc7-195">Gözden geçirin ve onu etkinleştirmek önce bir değişiklik hello etkisini değerlendirin:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-195">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="d4cc7-196">![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1018.png "risk ilkesine oturum açma")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-tooknow"></a><span data-ttu-id="d4cc7-197">Gerekenler tooknow</span><span class="sxs-lookup"><span data-stu-id="d4cc7-197">What you need tooknow</span></span>
<span data-ttu-id="d4cc7-198">Bir oturum açma riski güvenlik ilkesi toorequire multi-Factor authentication yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-198">You can configure a sign-in risk security policy toorequire multi-factor authentication:</span></span>

<span data-ttu-id="d4cc7-199">![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1017.png "risk ilkesine oturum açma")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="d4cc7-200">Ancak, güvenlik nedeniyle, bu ayar yalnızca çok faktörlü kimlik doğrulaması için önceden kaydedilmiş olan kullanıcılar için çalışır.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="d4cc7-201">Merhaba koşulu toorequire çok faktörlü kimlik doğrulama için multi-Factor authentication henüz kaydedilmemiş bir kullanıcı için sağlanıyorsa hello kullanıcı engellendi.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-201">If hello condition toorequire multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, hello user is blocked.</span></span>

<span data-ttu-id="d4cc7-202">Riskli oturum açma işlemleri için toorequire çok faktörlü kimlik doğrulamasını istiyorsanız, en iyi uygulama, aşağıdakileri yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-202">As a best practice, if you want toorequire multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="d4cc7-203">Merhaba etkinleştirmek [çok faktörlü kimlik doğrulaması kayıt ilkesi](#multi-factor-authentication-registration-policy) Merhaba etkilenen kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-203">Enable hello [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for hello affected users.</span></span>
2. <span data-ttu-id="d4cc7-204">Merhaba riskli olmayan oturum tooperform, kullanıcıların toologin MFA kayıt etkilenen gerektirir</span><span class="sxs-lookup"><span data-stu-id="d4cc7-204">Require hello affected users toologin in a non-risky session tooperform a MFA registration</span></span>

<span data-ttu-id="d4cc7-205">Bu adımları tamamladıktan, çok faktörlü kimlik doğrulamasının bir riskli oturum açma için gerekli sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="d4cc7-206">En iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="d4cc7-206">Best practices</span></span>
<span data-ttu-id="d4cc7-207">Seçerek bir **yüksek** eşik bir ilke tetiklenir ve hello etkisi toousers en aza indirir hello sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-207">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>  

<span data-ttu-id="d4cc7-208">Ancak, dışlar **düşük** ve **orta** gerçekleştirilen oturum açma bayrağı güvenliği aşılmış kimlik bilgisinden faydalanmakta saldırganın engelleyebilir değil hello ilkesinden risk için.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from hello policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="d4cc7-209">Ne zaman ayarı hello İlkesi</span><span class="sxs-lookup"><span data-stu-id="d4cc7-209">When setting hello policy,</span></span>

* <span data-ttu-id="d4cc7-210">Sağlamadığı / çok faktörlü kimlik doğrulamasına sahip olmadığınız kullanıcılar Dışla</span><span class="sxs-lookup"><span data-stu-id="d4cc7-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="d4cc7-211">Hello İlkesi etkinleştirme olduğu pratik yerel kullanıcılar hariç tutmak (örneğin hiçbir erişim toohelpdesk)</span><span class="sxs-lookup"><span data-stu-id="d4cc7-211">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="d4cc7-212">Büyük olasılıkla toogenerate çok fazla yanlış pozitifler (geliştiriciler, güvenlik analistleri) olan kullanıcıların Dışla</span><span class="sxs-lookup"><span data-stu-id="d4cc7-212">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="d4cc7-213">Kullanım bir **yüksek** eşiği ilk ilke dağıtımı, sırasında veya son kullanıcılar tarafından görülen sorunları en aza gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="d4cc7-214">Kullanım bir **düşük** kuruluşunuz daha yüksek güvenlik gerektiriyorsa eşiği.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="d4cc7-215">Seçerek bir **düşük** eşik ek kullanıcı oturum açma zorluklar, ancak daha yüksek düzeyde güvenlik sunar.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="d4cc7-216">Çoğu kuruluş için tooconfigure bir kural için önerilen varsayılan hello bir **orta** eşik toostrike kullanılabilirlik ile güvenlik arasında bir denge.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-216">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="d4cc7-217">Merhaba oturum açma risk ilkesine şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-217">hello sign-in risk policy is:</span></span>

* <span data-ttu-id="d4cc7-218">Uygulanan tooall tarayıcı trafiğini ve modern kimlik doğrulaması kullanarak oturum açma işlemleri.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-218">Applied tooall browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="d4cc7-219">Devre dışı bırakarak eski güvenlik protokollerini kullanarak uygulanmamış tooapplications WS-Trust uç noktada ADFS gibi Federasyon hello IDP hello.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-219">Not applied tooapplications using older security protocols by disabling hello WS-Trust endpoint at hello federated IDP, such as ADFS.</span></span>

<span data-ttu-id="d4cc7-220">Merhaba **Risk olaylarını** hello kimlik koruması konsolundaki sayfasında tüm olayları listeler:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-220">hello **Risk Events** page in hello Identity Protection console lists all events:</span></span>

* <span data-ttu-id="d4cc7-221">Bu ilkenin uygulandığı</span><span class="sxs-lookup"><span data-stu-id="d4cc7-221">This policy was applied to</span></span>
* <span data-ttu-id="d4cc7-222">Merhaba etkinliği gözden geçirin ve hello eylem uygun olup olmadığını belirleme</span><span class="sxs-lookup"><span data-stu-id="d4cc7-222">You can review hello activity and determine whether hello action was appropriate or not</span></span>

<span data-ttu-id="d4cc7-223">Merhaba genel bakış için kullanıcı deneyimi, ilgili bakın:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-223">For an overview of hello related user experience, see:</span></span>

* [<span data-ttu-id="d4cc7-224">Oturum açma riskli kurtarma</span><span class="sxs-lookup"><span data-stu-id="d4cc7-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="d4cc7-225">Riskli oturum engellenen açma</span><span class="sxs-lookup"><span data-stu-id="d4cc7-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="d4cc7-226">Oturum açma deneyimlerini Azure AD kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="d4cc7-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="d4cc7-227">**tooopen hello ilgili yapılandırma iletişim**:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-227">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="d4cc7-228">Merhaba üzerinde **Azure AD Identity Protection** dikey penceresinde hello **yapılandırma** 'yi tıklatın **oturum açma risk ilkesine**.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-228">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="d4cc7-229">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1014.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="d4cc7-230">Riskli oldukları belirlenen kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="d4cc7-230">Users flagged for risk</span></span>

<span data-ttu-id="d4cc7-231">Tüm etkin [risk olayları](active-directory-identity-protection-risk-events.md) , algılandı Azure Active Directory tarafından bir kullanıcıya katkıda bulunan için tooa mantıksal kavram kullanıcı risk çağrılır.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute tooa logical concept called user risk.</span></span> <span data-ttu-id="d4cc7-232">Risk bayrak eklenen kullanıcı geçirildiğini bir kullanıcı hesabı için bir göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Riskli oldukları belirlenen kullanıcılar](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="d4cc7-234">Kullanıcı risk düzeyi</span><span class="sxs-lookup"><span data-stu-id="d4cc7-234">User risk level</span></span>

<span data-ttu-id="d4cc7-235">Bir kullanıcı risk düzeyi hello kullanıcının kimliğini aşılmış bir (yüksek, Orta veya düşük) hello olasılığını göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-235">A user risk level is an indication (High, Medium, or Low) of hello likelihood that hello user’s identity has been compromised.</span></span> <span data-ttu-id="d4cc7-236">Bir kullanıcı kimliğiyle ilişkili hello kullanıcı risk olaylarına göre hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-236">It is calculated based on hello user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="d4cc7-237">Merhaba bir risk olayı ya da durumudur **etkin** veya **kapalı**.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-237">hello status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="d4cc7-238">Yalnızca olayları risk **etkin** toohello kullanıcı risk düzeyi hesaplama katkıda bulunun.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-238">Only risk events that are **Active** contribute toohello user risk level calculation.</span></span>

<span data-ttu-id="d4cc7-239">Merhaba kullanıcı risk düzeyi girişleri aşağıdaki hello kullanılarak hesaplanır:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-239">hello user risk level is calculated using hello following inputs:</span></span>

* <span data-ttu-id="d4cc7-240">Merhaba kullanıcı etkileyen etkin risk olayları</span><span class="sxs-lookup"><span data-stu-id="d4cc7-240">Active risk events impacting hello user</span></span>
* <span data-ttu-id="d4cc7-241">Bu olayların risk düzeyi</span><span class="sxs-lookup"><span data-stu-id="d4cc7-241">Risk level of these events</span></span>
* <span data-ttu-id="d4cc7-242">Gerçekleştirilen tüm düzeltme eylemlerini olup önlemlerin</span><span class="sxs-lookup"><span data-stu-id="d4cc7-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="d4cc7-243">![Kullanıcı riskleri](./media/active-directory-identityprotection/1031.png "kullanıcı riskleri")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="d4cc7-244">Oturum açma riskli kullanıcıların engellemek hello kullanıcı risk düzeyleri toocreate koşullu erişim ilkeleri kullanın veya bunları zorla toosecurely parolasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-244">You can use hello user risk levels toocreate conditional access policies that block risky users from signing in, or force them toosecurely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="d4cc7-245">Risk olaylarını el ile kapatma</span><span class="sxs-lookup"><span data-stu-id="d4cc7-245">Closing risk events manually</span></span>

<span data-ttu-id="d4cc7-246">Çoğu durumda, tooautomatically Kapat risk olaylarını güvenli bir parola sıfırlama gibi düzeltme eylemleri gerçekleştirecek.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-246">In most cases, you will take remediation actions such as a secure password reset tooautomatically close risk events.</span></span> <span data-ttu-id="d4cc7-247">Ancak, bu her zaman mümkün olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="d4cc7-248">Bu, örneğin, hello bir durumdur, ne zaman:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-248">This is, for example, hello case, when:</span></span>

* <span data-ttu-id="d4cc7-249">Etkin risk olaylarına sahip bir kullanıcı silindi</span><span class="sxs-lookup"><span data-stu-id="d4cc7-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="d4cc7-250">Bildirilen risk olayı sahip olan gerçekleştireceğini hello yasal kullanıcı tarafından bir araştırma ortaya çıkarır</span><span class="sxs-lookup"><span data-stu-id="d4cc7-250">An investigation reveals that a reported risk event has been perform by hello legitimate user</span></span>

<span data-ttu-id="d4cc7-251">Risk olaylarını olduğundan **etkin** toohello kullanıcı risk hesaplama katkıda, risk olaylarını el ile kapatarak risk düzeyi alt toomanually olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-251">Because risk events that are **Active** contribute toohello user risk calculation, you may have toomanually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="d4cc7-252">Araştırma Hello sürecinde tootake herhangi bir risk olayı bu eylemler toochange hello durumunu birini seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-252">During hello course of investigation, you can choose tootake any of these actions toochange hello status of a risk event:</span></span>

<span data-ttu-id="d4cc7-253">![Eylemler](./media/active-directory-identityprotection/34.png "Eylemler")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="d4cc7-254">**Gidermek** - bir risk olayı araştırdıktan sonra uygun düzeltme eylemi kimlik koruması dışında sürdü ve kapalı, işareti hello olayı çözümlenmiş olarak hello risk olay sayılacağı düşünüyorsanız.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that hello risk event should be considered closed, mark hello event as Resolved.</span></span> <span data-ttu-id="d4cc7-255">Çözümlenmiş olaylar hello risk olayın durumu tooClosed ayarlanır ve hello risk olay artık toouser risk katkıda bulunur.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-255">Resolved events will set hello risk event’s status tooClosed and hello risk event will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="d4cc7-256">**Hatalı pozitif olarak işaretlemek** -bazı durumlarda, bir risk olayı araştırmak ve olabilirsiniz, yanlış bir riskli işaretlenen olduğunu bulmak.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="d4cc7-257">Merhaba risk olayı hatalı pozitif olarak işaretleyerek hello böyle sayısı azaltmaya yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-257">You can help reduce hello number of such occurrences by marking hello risk event as False-positive.</span></span> <span data-ttu-id="d4cc7-258">Bu hello machine learning algoritmaları tooimprove hello sınıflandırma hello gelecekteki benzer olayların yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-258">This will help hello machine learning algorithms tooimprove hello classification of similar events in hello future.</span></span> <span data-ttu-id="d4cc7-259">Merhaba hatalı pozitif olayların durumudur çok**kapalı** ve toouser risk artık katkıda bulunur.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-259">hello status of false-positive events is too**Closed** and they will no longer contribute toouser risk.</span></span>
* <span data-ttu-id="d4cc7-260">**Yoksay** - herhangi bir düzeltme eylemi olmadı ancak hello etkin listesinden kaldırıldı risk olayı toobe Merhaba, risk olayı yoksay işaretleyebilirsiniz ve hello olay durumu kapatılacak istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-260">**Ignore** - If you have not taken any remediation action, but want hello risk event toobe removed from hello active list, you can mark a risk event Ignore and hello event status will be Closed.</span></span> <span data-ttu-id="d4cc7-261">Yoksayılan olayları toouser risk katkıda bulunmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-261">Ignored events do not contribute toouser risk.</span></span> <span data-ttu-id="d4cc7-262">Bu seçenek yalnızca olağan dışı durumlarda kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="d4cc7-263">**Yeniden etkinleştirme** -Risk el ile kapatılan olaylar (seçerek **gidermek**, **yanlış pozitif**, veya **Yoksay**) hello ayarı etkinleştirilebilir Olay durumunu geri çok**etkin**.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting hello event status back too**Active**.</span></span> <span data-ttu-id="d4cc7-264">Yeniden etkinleştirilen risk olaylarını toohello kullanıcı risk düzeyi hesaplama katkıda.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-264">Reactivated risk events contribute toohello user risk level calculation.</span></span> <span data-ttu-id="d4cc7-265">Risk olaylarına (güvenli bir parola sıfırlama gibi) düzeltme aracılığıyla kapalı etkinleştirilemez.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="d4cc7-266">**tooopen hello ilgili yapılandırma iletişim**:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-266">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="d4cc7-267">Merhaba üzerinde **Azure AD Identity Protection** dikey altında **Araştır**, tıklatın **Risk olayları**.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-267">On hello **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="d4cc7-268">![El ile parola sıfırlama](./media/active-directory-identityprotection/1002.png "el ile parola sıfırlama")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="d4cc7-269">Merhaba, **Risk olayları** listesinde, bir risk tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-269">In hello **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="d4cc7-270">![El ile parola sıfırlama](./media/active-directory-identityprotection/1003.png "el ile parola sıfırlama")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="d4cc7-271">Merhaba risk dikey penceresinde, bir kullanıcı sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-271">On hello risk blade, right-click a user.</span></span>

    <span data-ttu-id="d4cc7-272">![El ile parola sıfırlama](./media/active-directory-identityprotection/1004.png "el ile parola sıfırlama")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="d4cc7-273">Bir kullanıcı için tüm risk olaylarını el ile kapatma</span><span class="sxs-lookup"><span data-stu-id="d4cc7-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="d4cc7-274">El ile bir kullanıcı için risk olayları ayrı ayrı kapatmak yerine, Azure Active Directory kimlik koruması Ayrıca, bir yöntem tooclose ile tüm olayları tek bir tıklatmayla bir kullanıcı için sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method tooclose all events for a user with one click.</span></span>

<span data-ttu-id="d4cc7-275">![Eylemler](./media/active-directory-identityprotection/2222.png "Eylemler")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="d4cc7-276">Tıkladığınızda **tüm olayları kapatmak**, tüm olayları kapatılır ve etkilenen hello kullanıcının, artık risk altında.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-276">When you click **Dismiss all events**, all events are closed and hello affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="d4cc7-277">Düzelterek kullanıcı risk olayı</span><span class="sxs-lookup"><span data-stu-id="d4cc7-277">Remediating user risk events</span></span>

<span data-ttu-id="d4cc7-278">Bir düzeltme bir kimlik veya önceden şüpheli veya toobe bilinen bir cihaz tehlikeye bir eylem toosecure ' dir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-278">A remediation is an action toosecure an identity or a device that was previously suspected or known toobe compromised.</span></span> <span data-ttu-id="d4cc7-279">Bir düzeltme eylemi hello kimlik veya aygıt tooa güvenli bir duruma geri yükler ve hello kimlik veya aygıtla ilişkili önceki risk olaylarını çözümler.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-279">A remediation action restores hello identity or device tooa safe state, and resolves previous risk events associated with hello identity or device.</span></span>

<span data-ttu-id="d4cc7-280">tooremediate kullanıcı risk olaylarına, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-280">tooremediate user risk events, you can:</span></span>

* <span data-ttu-id="d4cc7-281">Güvenli parola sıfırlama tooremediate kullanıcı risk olaylarına el ile gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="d4cc7-281">Perform a secure password reset tooremediate user risk events manually</span></span>
* <span data-ttu-id="d4cc7-282">Kullanıcı risk olayları otomatik olarak düzeltmek veya bir kullanıcı risk güvenlik ilkesi toomitigate yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d4cc7-282">Configure a user risk security policy toomitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="d4cc7-283">Etkilenen hello aygıt yeniden görüntü</span><span class="sxs-lookup"><span data-stu-id="d4cc7-283">Re-image hello infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="d4cc7-284">El ile güvenli parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="d4cc7-284">Manual secure password reset</span></span>
<span data-ttu-id="d4cc7-285">Güvenli parola sıfırlama birçok risk olayı için geçerli bir düzeltme ve gerçekleştirildiğinde, otomatik olarak bu risk olaylarını kapatır ve hello kullanıcı risk düzeyi yeniden hesaplar.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates hello user risk level.</span></span> <span data-ttu-id="d4cc7-286">Merhaba kimlik koruması Pano tooinitiate parola sıfırlama riskli bir kullanıcı için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-286">You can use hello Identity Protection dashboard tooinitiate a password reset for a risky user.</span></span>

<span data-ttu-id="d4cc7-287">Merhaba ilgili iletişim iki farklı yöntemler tooreset bir parola sağlar:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-287">hello related dialog provides two different methods tooreset a password:</span></span>

<span data-ttu-id="d4cc7-288">**Parola sıfırlama** - seçin **parolalarını hello kullanıcı tooreset gerektiren** hello kullanıcı çok faktörlü kimlik doğrulaması için kaydedildiyse tooallow hello kullanıcı tooself-Kurtar.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-288">**Reset password** - Select **Require hello user tooreset their password** tooallow hello user tooself-recover if hello user has registered for multi-factor authentication.</span></span> <span data-ttu-id="d4cc7-289">Merhaba kullanıcının sonraki oturum açma sırasında hello kullanıcı çok faktörlü kimlik doğrulaması sınama başarıyla gerekli toosolve ve ardından, zorunlu toochange hello parola olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-289">During hello user's next sign-in, hello user will be required toosolve a multi-factor authentication challenge successfully and then, forced toochange hello password.</span></span> <span data-ttu-id="d4cc7-290">Merhaba kullanıcı hesabı kayıtlı çok faktörlü kimlik doğrulama değilse, bu seçenek kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-290">This option isn't available if hello user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="d4cc7-291">**Geçici parolayı** - seçin **geçici bir parola oluşturmak** tooimmediately hello mevcut parolayı geçersiz kılmak ve hello kullanıcı için yeni bir geçici parola oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-291">**Temporary password** - Select **Generate a temporary password** tooimmediately invalidate hello existing password, and create a new temporary password for hello user.</span></span> <span data-ttu-id="d4cc7-292">Merhaba yeni geçici parola tooan alternatif e-posta adresi hello kullanıcı veya toohello kullanıcının yöneticisini gönderin.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-292">Send hello new temporary password tooan alternate email address for hello user or toohello user's manager.</span></span> <span data-ttu-id="d4cc7-293">Merhaba parola geçici olduğundan hello kullanıcı oturum açma sırasında istendiğinde toochange hello parola olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-293">Because hello password is temporary, hello user will be prompted toochange hello password upon sign-in.</span></span>

<span data-ttu-id="d4cc7-294">![İlke](./media/active-directory-identityprotection/1005.png "İlkesi")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="d4cc7-295">**tooopen hello ilgili yapılandırma iletişim**:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-295">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="d4cc7-296">Merhaba üzerinde **Azure AD Identity Protection** dikey penceresinde tıklatın **bayrak eklenen kullanıcılar için risk**.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-296">On hello **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="d4cc7-297">![El ile parola sıfırlama](./media/active-directory-identityprotection/1006.png "el ile parola sıfırlama")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="d4cc7-298">Kullanıcıların Hello listeden en az bir risk olaylarına sahip bir kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-298">From hello list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="d4cc7-299">![El ile parola sıfırlama](./media/active-directory-identityprotection/1007.png "el ile parola sıfırlama")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="d4cc7-300">Merhaba kullanıcı dikey penceresinde **parola sıfırlama**.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-300">On hello user blade, click **Reset password**.</span></span>

    <span data-ttu-id="d4cc7-301">![El ile parola sıfırlama](./media/active-directory-identityprotection/1008.png "el ile parola sıfırlama")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="d4cc7-302">Kullanıcı risk güvenlik ilkesi</span><span class="sxs-lookup"><span data-stu-id="d4cc7-302">User risk security policy</span></span>
<span data-ttu-id="d4cc7-303">Bir kullanıcı risk güvenlik ilkesi hello risk düzeyi tooa belirli kullanıcı ve önceden tanımlanmış koşullara ve kurallarına göre düzeltme ve azaltma Eylemler uyguladığında bir koşullu erişim ilkesi var.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-303">A user risk security policy is a conditional access policy that evaluates hello risk level tooa specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="d4cc7-304">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1009.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="d4cc7-305">Azure AD kimlik koruması hello azaltma ve risk olanak tanıyarak bayrak eklenen kullanıcılar düzeltmesi yönetmenize yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-305">Azure AD Identity Protection helps you manage hello mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="d4cc7-306">Kullanıcılar ve gruplar hello ilkenin uygulandığı hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-306">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="d4cc7-307">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1010.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="d4cc7-308">Hello İlkesi tetikleyen hello kullanıcı risk düzeyi eşiği (düşük, Orta veya yüksek) ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-308">Set hello user risk level threshold (low, medium, or high) that triggers hello policy:</span></span>

    <span data-ttu-id="d4cc7-309">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1011.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="d4cc7-310">Set hello denetimleri toobe Hello İlkesi tetikler zorunlu tutulur:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-310">Set hello controls toobe enforced when hello policy triggers:</span></span>

    <span data-ttu-id="d4cc7-311">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1012.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="d4cc7-312">Anahtar hello durumunu ilkenizin:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-312">Switch hello state of your policy:</span></span>

    <span data-ttu-id="d4cc7-313">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/403.png "MFA kayıt")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="d4cc7-314">Gözden geçirin ve onu etkinleştirmek önce bir değişiklik hello etkisini değerlendirin:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-314">Review and evaluate hello impact of a change before activating it:</span></span>

    <span data-ttu-id="d4cc7-315">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1013.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="d4cc7-316">Seçerek bir **yüksek** eşik bir ilke tetiklenir ve hello etkisi toousers en aza indirir hello sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-316">Choosing a **High** threshold reduces hello number of times a policy is triggered and minimizes hello impact toousers.</span></span>
<span data-ttu-id="d4cc7-317">Ancak, dışlar **düşük** ve **orta** kimlikleri veya cihazları, güvenli değil hello ilkesinden risk için işaretlenmiş kullanıcılar önceden şüpheli veya bilinen tehlikeye toobe.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-317">However, it excludes **Low** and **Medium** users flagged for risk from hello policy, which may not secure identities or devices that were previously suspected or known toobe compromised.</span></span>

<span data-ttu-id="d4cc7-318">Ne zaman ayarı hello İlkesi</span><span class="sxs-lookup"><span data-stu-id="d4cc7-318">When setting hello policy,</span></span>

* <span data-ttu-id="d4cc7-319">Büyük olasılıkla toogenerate çok fazla yanlış pozitifler (geliştiriciler, güvenlik analistleri) olan kullanıcıların Dışla</span><span class="sxs-lookup"><span data-stu-id="d4cc7-319">Exclude users who are likely toogenerate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="d4cc7-320">Hello İlkesi etkinleştirme olduğu pratik yerel kullanıcılar hariç tutmak (örneğin hiçbir erişim toohelpdesk)</span><span class="sxs-lookup"><span data-stu-id="d4cc7-320">Exclude users in locales where enabling hello policy is not practical (for example no access toohelpdesk)</span></span>
* <span data-ttu-id="d4cc7-321">Kullanım bir **yüksek** eşiği ilk ilke dağıtımı, sırasında veya son kullanıcılar tarafından görülen sorunları en aza gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="d4cc7-322">Kullanım bir **düşük** kuruluşunuz daha yüksek güvenlik gerektiriyorsa eşiği.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="d4cc7-323">Seçerek bir **düşük** eşik ek kullanıcı oturum açma zorluklar, ancak daha yüksek düzeyde güvenlik sunar.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="d4cc7-324">Çoğu kuruluş için tooconfigure bir kural için önerilen varsayılan hello bir **orta** eşik toostrike kullanılabilirlik ile güvenlik arasında bir denge.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-324">hello recommended default for most organizations is tooconfigure a rule for a **Medium** threshold toostrike a balance between usability and security.</span></span>

<span data-ttu-id="d4cc7-325">Merhaba genel bakış için kullanıcı deneyimi, ilgili bakın:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-325">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="d4cc7-326">[Hesap kurtarma akışı tehlikeye](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="d4cc7-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="d4cc7-327">[Hesap engellendi akış tehlikeye](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="d4cc7-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="d4cc7-328">**tooopen hello ilgili yapılandırma iletişim**:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-328">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="d4cc7-329">Merhaba üzerinde **Azure AD Identity Protection** dikey penceresinde hello **yapılandırma** 'yi tıklatın **kullanıcı risk ilkesine**.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-329">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="d4cc7-330">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1009.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="d4cc7-331">Kullanıcı risk olaylar azaltılması</span><span class="sxs-lookup"><span data-stu-id="d4cc7-331">Mitigating user risk events</span></span>
<span data-ttu-id="d4cc7-332">Yöneticiler kullanıcı risk güvenlik ilkesi tooblock kullanıcılar oturum açma sırasında hello risk düzeyine bağlı olarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-332">Administrators can set a user risk security policy tooblock users upon sign-in depending on hello risk level.</span></span>

<span data-ttu-id="d4cc7-333">Bir oturum açma engelleme:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="d4cc7-334">Etkilenen hello kullanıcı için yeni kullanıcı risk olaylarına Hello oluşturulmasını engeller</span><span class="sxs-lookup"><span data-stu-id="d4cc7-334">Prevents hello generation of new user risk events for hello affected user</span></span>
* <span data-ttu-id="d4cc7-335">Etkinleştirir Yöneticiler toomanually hello kullanıcının kimliğini etkileyen hello risk olaylarını düzeltmek ve tooa güvenli durumunu geri yükle</span><span class="sxs-lookup"><span data-stu-id="d4cc7-335">Enables administrators toomanually remediate hello risk events affecting hello user's identity and restore it tooa secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="d4cc7-336">Çok faktörlü kimlik doğrulaması kayıt ilkesi</span><span class="sxs-lookup"><span data-stu-id="d4cc7-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="d4cc7-337">Azure çok faktörlü kimlik doğrulaması hello kullanımını daha fazlasını bir kullanıcı adı ve parolası gerektiren kim olduğunuzu doğrulama bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-337">Azure multi-factor authentication is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="d4cc7-338">Güvenlik toouser oturum açmalarına ve işlemlerine ikinci bir katmanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-338">It provides a second layer of security toouser sign-ins and transactions.</span></span>  
<span data-ttu-id="d4cc7-339">Çünkü kullanıcı oturum açma işlemleri için Azure çok faktörlü kimlik doğrulaması ihtiyaç duyduğunuz öneririz:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="d4cc7-340">Kolay doğrulama seçeneklerini aralıklı güçlü kimlik doğrulaması sunar</span><span class="sxs-lookup"><span data-stu-id="d4cc7-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="d4cc7-341">Kuruluş tooprotect hazırlanırken önemli bir rol oynar ve hesap ödün kurtarma</span><span class="sxs-lookup"><span data-stu-id="d4cc7-341">Plays a key role in preparing your organization tooprotect and recover from account compromises</span></span>

<span data-ttu-id="d4cc7-342">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1019.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="d4cc7-343">Daha fazla ayrıntı için bkz: [Azure multi-Factor Authentication nedir?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d4cc7-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="d4cc7-344">Azure AD kimlik koruması sağlayan bir ilkesi yapılandırarak hello üretimini çok faktörlü kimlik doğrulaması kayıt yönetmenize yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-344">Azure AD Identity Protection helps you manage hello roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="d4cc7-345">Kullanıcılar ve gruplar hello ilkenin uygulandığı hello ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-345">Set hello users and groups hello policy applies to:</span></span>

    <span data-ttu-id="d4cc7-346">![MFA ilkesini](./media/active-directory-identityprotection/1020.png "MFA İlkesi")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="d4cc7-347">Hello İlkesi tetikler zorunlu tutulur kümesi hello denetimleri toobe::</span><span class="sxs-lookup"><span data-stu-id="d4cc7-347">Set hello controls toobe enforced when hello policy triggers::</span></span>  

    <span data-ttu-id="d4cc7-348">![MFA ilkesini](./media/active-directory-identityprotection/1021.png "MFA İlkesi")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="d4cc7-349">Anahtar hello durumunu ilkenizin:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-349">Switch hello state of your policy:</span></span>

    <span data-ttu-id="d4cc7-350">![MFA ilkesini](./media/active-directory-identityprotection/403.png "MFA İlkesi")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="d4cc7-351">Merhaba geçerli kayıt durumunu görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-351">View hello current registration status:</span></span>

    <span data-ttu-id="d4cc7-352">![MFA ilkesini](./media/active-directory-identityprotection/1022.png "MFA İlkesi")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="d4cc7-353">Merhaba genel bakış için kullanıcı deneyimi, ilgili bakın:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-353">For an overview of hello related user experience, see:</span></span>

* <span data-ttu-id="d4cc7-354">[Çok faktörlü kimlik doğrulaması kayıt akışı](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="d4cc7-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="d4cc7-355">[Azure AD kimlik koruması ile karşılaştığında oturum açma](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="d4cc7-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="d4cc7-356">**tooopen hello ilgili yapılandırma iletişim**:</span><span class="sxs-lookup"><span data-stu-id="d4cc7-356">**tooopen hello related configuration dialog**:</span></span>

- <span data-ttu-id="d4cc7-357">Merhaba üzerinde **Azure AD Identity Protection** dikey penceresinde hello **yapılandırma** 'yi tıklatın **çok faktörlü kimlik doğrulaması kayıt**.</span><span class="sxs-lookup"><span data-stu-id="d4cc7-357">On hello **Azure AD Identity Protection** blade, in hello **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="d4cc7-358">![MFA ilkesini](./media/active-directory-identityprotection/1019.png "MFA İlkesi")</span><span class="sxs-lookup"><span data-stu-id="d4cc7-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4cc7-359">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d4cc7-359">Next steps</span></span>
* [<span data-ttu-id="d4cc7-360">Kanal 9: Azure AD ve kimlik göster: kimlik koruması Önizleme</span><span class="sxs-lookup"><span data-stu-id="d4cc7-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="d4cc7-361">Azure Active Directory kimlik koruması etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d4cc7-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="d4cc7-362">Azure Active Directory kimlik koruması tarafından algılanan güvenlik açığı</span><span class="sxs-lookup"><span data-stu-id="d4cc7-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="d4cc7-363">Azure Active Directory risk olayları</span><span class="sxs-lookup"><span data-stu-id="d4cc7-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="d4cc7-364">Azure Active Directory kimlik koruması bildirimleri</span><span class="sxs-lookup"><span data-stu-id="d4cc7-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="d4cc7-365">Azure Active Directory kimlik koruması Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="d4cc7-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="d4cc7-366">Azure Active Directory kimlik koruması Kılavuzu sözlüğü</span><span class="sxs-lookup"><span data-stu-id="d4cc7-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="d4cc7-367">Oturum açma deneyimlerini Azure AD kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="d4cc7-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="d4cc7-368">Azure Active Directory kimlik koruması - nasıl toounblock kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="d4cc7-368">Azure Active Directory Identity Protection - How toounblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="d4cc7-369">Azure Active Directory kimlik koruması ve Microsoft Graph kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d4cc7-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
