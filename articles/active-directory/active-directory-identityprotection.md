---
title: "Azure Active Directory kimlik koruması | Microsoft Docs"
description: "Azure AD kimlik koruması nasıl yeteneğini bir saldırgan güvenliği aşılmış kimlik veya aygıt yararlanmaya ve güvenli bir kimlik veya önceden şüpheli veya tehlikeye bilinen bir cihaz için sınırlamak sağladığını öğrenin."
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
ms.openlocfilehash: 0c7a8d68c0df729441e3f7faa5cd06066db1261d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-identity-protection"></a><span data-ttu-id="74702-104">Azure Active Directory Kimlik Koruması</span><span class="sxs-lookup"><span data-stu-id="74702-104">Azure Active Directory Identity Protection</span></span>

<span data-ttu-id="74702-105">Azure Active Directory kimlik koruması sağlayan Azure AD Premium P2 edition özelliğidir:</span><span class="sxs-lookup"><span data-stu-id="74702-105">Azure Active Directory Identity Protection is a feature of the Azure AD Premium P2 edition that enables you to:</span></span>

- <span data-ttu-id="74702-106">Kuruluşunuzdaki kimlikleri etkileyen olası güvenlik açıklarını algılama</span><span class="sxs-lookup"><span data-stu-id="74702-106">Detect potential vulnerabilities affecting your organization’s identities</span></span>

- <span data-ttu-id="74702-107">Kuruluşunuzdaki kimlikleri için ilgili algılanan kuşkulu eylemleri otomatik yanıtlar yapılandırın</span><span class="sxs-lookup"><span data-stu-id="74702-107">Configure automated responses to detected suspicious actions that are related to your organization’s identities</span></span>  

- <span data-ttu-id="74702-108">Şüpheli olayları araştırmanıza ve bunları gidermek için uygun eylemi gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="74702-108">Investigate suspicious incidents and take appropriate action to resolve them</span></span>   


## <a name="getting-started"></a><span data-ttu-id="74702-109">Başlarken</span><span class="sxs-lookup"><span data-stu-id="74702-109">Getting started</span></span>

<span data-ttu-id="74702-110">Microsoft bulut tabanlı kimlikleri birden fazla bir süredir güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="74702-110">Microsoft secures cloud-based identities for more than a decade.</span></span> <span data-ttu-id="74702-111">Azure Active Directory kimlik koruması ile ortamınızda Microsoft kimlikleri güvenli hale getirmek için kullandığı aynı koruma sistemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74702-111">With Azure Active Directory Identity Protection, in your environment, you can use the same protection systems Microsoft uses to secure identities.</span></span>

<span data-ttu-id="74702-112">Güvenlik ihlallerini çoğunluğu saldırganlar bir ortamda bir kullanıcının kimliğini çalarak erişmek zaman yer ayırın.</span><span class="sxs-lookup"><span data-stu-id="74702-112">The vast majority of security breaches take place when attackers gain access to an environment by stealing a user’s identity.</span></span> <span data-ttu-id="74702-113">Yıllar içinde saldırganlar üçüncü taraf ihlallerini yararlanan ve Gelişmiş kimlik avı saldırıları kullanarak giderek etkin hale getirildi.</span><span class="sxs-lookup"><span data-stu-id="74702-113">Over the years, attackers have become increasingly effective in leveraging third party breaches and using sophisticated phishing attacks.</span></span> <span data-ttu-id="74702-114">Bir saldırgan düşük ayrıcalıklı kullanıcı hesaplarına bile erişim elde hemen bunları yanal hareket önemli şirket kaynaklarına erişim kazanmak daha kolay olduğundan.</span><span class="sxs-lookup"><span data-stu-id="74702-114">As soon as an attacker gains access to even low privileged user accounts, it is relatively easy for them to gain access to important company resources through lateral movement.</span></span>

<span data-ttu-id="74702-115">Bu gruplarındaki sonucu olarak, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="74702-115">As a consequence of this, you need to:</span></span>

- <span data-ttu-id="74702-116">Ayrıcalık düzeylerini bağımsız olarak tüm kimlikleri koru</span><span class="sxs-lookup"><span data-stu-id="74702-116">Protect all identities regardless of their privilege level</span></span>

- <span data-ttu-id="74702-117">Proaktif olarak kötüye gelen güvenliği aşılmış kimlik engelle</span><span class="sxs-lookup"><span data-stu-id="74702-117">Proactively prevent compromised identities from being abused</span></span>

<span data-ttu-id="74702-118">Güvenliği aşılmış kimlikleri keşfetme hiçbir kolay bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="74702-118">Discovering compromised identities is no easy task.</span></span> <span data-ttu-id="74702-119">Daha fazla bilgi ve potansiyel olarak belirtmek şüpheli olayları algılamak için buluşsal yöntemler kimlikleri riske ve Azure Active Directory Uyarlamalı machine learning algoritmaları kullanır.</span><span class="sxs-lookup"><span data-stu-id="74702-119">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect anomalies and suspicious incidents that indicate potentially compromised identities.</span></span> <span data-ttu-id="74702-120">Bu verileri kullanarak, kimlik koruması, raporları ve algılanan sorunlarını değerlendirin ve uygun azaltma veya düzeltme eylemlerini gerçekleştirin sağlayan uyarıları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="74702-120">Using this data, Identity Protection generates reports and alerts that enable you to evaluate the detected issues and take appropriate mitigation or remediation actions.</span></span>

<span data-ttu-id="74702-121">Azure Active Directory kimlik koruması izleme ve Raporlama Aracı büyük.</span><span class="sxs-lookup"><span data-stu-id="74702-121">Azure Active Directory Identity Protection is more than a monitoring and reporting tool.</span></span> <span data-ttu-id="74702-122">Kuruluşunuzdaki kimlikleri korumak için belirtilen risk düzeyi erişildiğinde otomatik olarak algılanan sorunları yanıt risk tabanlı ilkeleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74702-122">To protect your organization's identities, you can configure risk-based policies that automatically respond to detected issues when a specified risk level has been reached.</span></span> <span data-ttu-id="74702-123">Azure Active Directory ve EMS tarafından sağlanan diğer koşullu erişim denetimlerini yanı sıra bu ilkeleri otomatik olarak engellemek ya da dahil olmak üzere parola sıfırlamaları Uyarlamalı düzeltme eylemleri ve çok faktörlü kimlik doğrulaması zorlama başlatın.</span><span class="sxs-lookup"><span data-stu-id="74702-123">These policies, in addition to other conditional access controls provided by Azure Active Directory and EMS, can either automatically block or initiate adaptive remediation actions including password resets and multi-factor authentication enforcement.</span></span>


#### <a name="identity-protection-capabilities"></a><span data-ttu-id="74702-124">Kimlik koruma özellikleri</span><span class="sxs-lookup"><span data-stu-id="74702-124">Identity Protection capabilities</span></span>

<span data-ttu-id="74702-125">**Algılama Güvenlik Açıkları ve riskli hesapları:**</span><span class="sxs-lookup"><span data-stu-id="74702-125">**Detecting vulnerabilities and risky accounts:**</span></span>  

* <span data-ttu-id="74702-126">Genel güvenlik duruşunu güvenlik açıkları vurgulayarak güvenliğini geliştirmek için özel öneriler sağlama</span><span class="sxs-lookup"><span data-stu-id="74702-126">Providing custom recommendations to improve overall security posture by highlighting vulnerabilities</span></span>
* <span data-ttu-id="74702-127">Oturum açma risk düzeyleri hesaplama</span><span class="sxs-lookup"><span data-stu-id="74702-127">Calculating sign-in risk levels</span></span>
* <span data-ttu-id="74702-128">Kullanıcı risk düzeyleri hesaplama</span><span class="sxs-lookup"><span data-stu-id="74702-128">Calculating user risk levels</span></span>


<span data-ttu-id="74702-129">**Risk olaylarını araştırma:**</span><span class="sxs-lookup"><span data-stu-id="74702-129">**Investigating risk events:**</span></span>

* <span data-ttu-id="74702-130">Risk olayları için bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="74702-130">Sending notifications for risk events</span></span>
* <span data-ttu-id="74702-131">Risk olaylarını ilgili ve bağlamsal bilgileri kullanarak araştırma</span><span class="sxs-lookup"><span data-stu-id="74702-131">Investigating risk events using relevant and contextual information</span></span>
* <span data-ttu-id="74702-132">Araştırmalar izlemek için temel iş akışı sağlama</span><span class="sxs-lookup"><span data-stu-id="74702-132">Providing basic workflows to track investigations</span></span>
* <span data-ttu-id="74702-133">Parola sıfırlama gibi düzeltme eylemleri kolay erişim sağlama</span><span class="sxs-lookup"><span data-stu-id="74702-133">Providing easy access to remediation actions such as password reset</span></span>

<span data-ttu-id="74702-134">**Risk bağlı olarak koşullu erişim ilkeleri:**</span><span class="sxs-lookup"><span data-stu-id="74702-134">**Risk-based conditional access policies:**</span></span>

* <span data-ttu-id="74702-135">Oturum açma işlemleri engelleme veya çok faktörlü kimlik doğrulaması zorluklarını gerektirerek riskli oturum açma işlemlerini azaltmak için ilke.</span><span class="sxs-lookup"><span data-stu-id="74702-135">Policy to mitigate risky sign-ins by blocking sign-ins or requiring multi-factor authentication challenges.</span></span>
* <span data-ttu-id="74702-136">Blok veya güvenli riskli kullanıcı hesapları için ilke</span><span class="sxs-lookup"><span data-stu-id="74702-136">Policy to block or secure risky user accounts</span></span>
* <span data-ttu-id="74702-137">Çok faktörlü kimlik doğrulaması için kullanıcıların İlkesi</span><span class="sxs-lookup"><span data-stu-id="74702-137">Policy to require users to register for multi-factor authentication</span></span>



## <a name="identity-protection-roles"></a><span data-ttu-id="74702-138">Kimlik koruması rolleri</span><span class="sxs-lookup"><span data-stu-id="74702-138">Identity Protection roles</span></span>

<span data-ttu-id="74702-139">Yük Dengelemesi için kimlik koruması uygulamanız geçici yönetimi etkinlikleri, çeşitli roller atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74702-139">To load balance the management activities around your Identity Protection implementation, you can assign several roles.</span></span> <span data-ttu-id="74702-140">Azure AD Identity Protection 3 dizin rollerini destekler:</span><span class="sxs-lookup"><span data-stu-id="74702-140">Azure AD Identity Protection supports 3 directory roles:</span></span>

| <span data-ttu-id="74702-141">Rol</span><span class="sxs-lookup"><span data-stu-id="74702-141">Role</span></span>                         | <span data-ttu-id="74702-142">Yapabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="74702-142">Can do</span></span>                          | <span data-ttu-id="74702-143">Yapamaz</span><span class="sxs-lookup"><span data-stu-id="74702-143">Cannot do</span></span>
| :--                          | ---                                |  ---   |
| <span data-ttu-id="74702-144">Genel yönetici</span><span class="sxs-lookup"><span data-stu-id="74702-144">Global administrator</span></span>         | <span data-ttu-id="74702-145">Kimlik koruması, yerleşik kimlik koruması için tam erişim</span><span class="sxs-lookup"><span data-stu-id="74702-145">Full access to Identity Protection, Onboard Identity Protection</span></span>| |
| <span data-ttu-id="74702-146">Güvenlik yöneticisi</span><span class="sxs-lookup"><span data-stu-id="74702-146">Security administrator</span></span>       | <span data-ttu-id="74702-147">Kimlik koruması için tam erişim</span><span class="sxs-lookup"><span data-stu-id="74702-147">Full access to Identity Protection</span></span> | <span data-ttu-id="74702-148">Yerleşik kimlik koruması, bir kullanıcı parolalarını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="74702-148">Onboard Identity Protection,  reset passwords for a user</span></span> |
| <span data-ttu-id="74702-149">Güvenlik okuyucusu</span><span class="sxs-lookup"><span data-stu-id="74702-149">Security reader</span></span>              | <span data-ttu-id="74702-150">Kimlik koruması yalnızca hazır erişimi</span><span class="sxs-lookup"><span data-stu-id="74702-150">Ready-only access to Identity Protection</span></span> | <span data-ttu-id="74702-151">Yerleşik kimlik koruması, remidiate kullanıcılar, ilkelerini yapılandırmak, parolaları sıfırlama</span><span class="sxs-lookup"><span data-stu-id="74702-151">Onboard Identity Protection, remidiate users, configure policies,  reset passwords</span></span> |




<span data-ttu-id="74702-152">Daha fazla ayrıntı için bkz: [Azure Active Directory'de yönetici rolleri atama](active-directory-assign-admin-roles-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="74702-152">For more details, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles-azure-portal.md)</span></span>



## <a name="detection"></a><span data-ttu-id="74702-153">Algılama</span><span class="sxs-lookup"><span data-stu-id="74702-153">Detection</span></span>

### <a name="vulnerabilities"></a><span data-ttu-id="74702-154">Güvenlik Açıkları</span><span class="sxs-lookup"><span data-stu-id="74702-154">Vulnerabilities</span></span>

<span data-ttu-id="74702-155">Azure Active Directory kimlik koruması yapılandırmanızı analizleri yaparken ve kullanıcı kimlikleri üzerinde bir etkisi olabilir güvenlik açıkları algılar.</span><span class="sxs-lookup"><span data-stu-id="74702-155">Azure Active Directory Identity Protection analyses your configuration and detects vulnerabilities that can have an impact on your user's identities.</span></span> <span data-ttu-id="74702-156">Daha fazla ayrıntı için bkz: [Azure Active Directory kimlik koruması tarafından algılanan Güvenlik Açığı](active-directory-identityprotection-vulnerabilities.md).</span><span class="sxs-lookup"><span data-stu-id="74702-156">For more details, see [Vulnerabilities detected by Azure Active Directory Identity Protection](active-directory-identityprotection-vulnerabilities.md).</span></span>

### <a name="risk-events"></a><span data-ttu-id="74702-157">Risk olayı</span><span class="sxs-lookup"><span data-stu-id="74702-157">Risk events</span></span>

<span data-ttu-id="74702-158">Azure Active Directory kullanıcı kimlikleri ilgili kuşkulu eylemleri algılamak için Uyarlamalı machine learning algoritmaları ve buluşsal yöntemler kullanır.</span><span class="sxs-lookup"><span data-stu-id="74702-158">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user's identities.</span></span> <span data-ttu-id="74702-159">Sistem algılanan her şüpheli eylemi için bir kayıt oluşturur.</span><span class="sxs-lookup"><span data-stu-id="74702-159">The system creates a record for each detected suspicious action.</span></span> <span data-ttu-id="74702-160">Bu kayıtları olarak da bilinen risk olaylardır.</span><span class="sxs-lookup"><span data-stu-id="74702-160">These records are also known as risk events.</span></span>  
<span data-ttu-id="74702-161">Daha ayrıntılı bilgi için bkz. [Azure Active Directory risk olayları](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="74702-161">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span>


## <a name="investigation"></a><span data-ttu-id="74702-162">Araştırma</span><span class="sxs-lookup"><span data-stu-id="74702-162">Investigation</span></span>
<span data-ttu-id="74702-163">Yolculuğunuzun kimlik koruması aracılığıyla genellikle kimlik koruması panosu ile başlar.</span><span class="sxs-lookup"><span data-stu-id="74702-163">Your journey through Identity Protection typically starts with the Identity Protection dashboard.</span></span>

<span data-ttu-id="74702-164">![Düzeltme](./media/active-directory-identityprotection/1000.png "düzeltme")</span><span class="sxs-lookup"><span data-stu-id="74702-164">![Remediation](./media/active-directory-identityprotection/1000.png "Remediation")</span></span>

<span data-ttu-id="74702-165">Pano, erişmenizi sağlar:</span><span class="sxs-lookup"><span data-stu-id="74702-165">The dashboard gives you access to:</span></span>

* <span data-ttu-id="74702-166">Gibi raporları **bayrak eklenen kullanıcılar için risk**, **Risk olayları** ve **güvenlik açıkları**</span><span class="sxs-lookup"><span data-stu-id="74702-166">Reports such as **Users flagged for risk**, **Risk events** and **Vulnerabilities**</span></span>
* <span data-ttu-id="74702-167">Yapılandırması gibi ayarları, **güvenlik ilkeleri**, **bildirimleri** ve **çok faktörlü kimlik doğrulaması kayıt**</span><span class="sxs-lookup"><span data-stu-id="74702-167">Settings such as the configuration of your **Security Policies**, **Notifications** and **multi-factor authentication registration**</span></span>

<span data-ttu-id="74702-168">Genellikle, etkinlikleri, günlükler ve düzeltme veya azaltma adımları gerekli olup olmadığını karar vermek için bir risk olayı ile ilgili diğer ilgili bilgileri gözden geçirme işlemi olduğundan, araştırma ve kimliğini nasıl değiştirildiği için başlangıç noktası. gizliliği ve güvenliği aşılmış kimlik nasıl kullanıldığını anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="74702-168">It is typically your starting point for investigation, which is the process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary,  and how the identity was compromised, and understand how the compromised identity was used.</span></span>

<span data-ttu-id="74702-169">Araştırma etkinliklerinizi bağlayabilirsiniz [bildirimleri](active-directory-identityprotection-notifications.md) Azure Active Directory koruma e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="74702-169">You can tie your investigation activities to the [notifications](active-directory-identityprotection-notifications.md) Azure Active Directory Protection sends per email.</span></span>

<span data-ttu-id="74702-170">Aşağıdaki bölümlerde daha fazla ayrıntı ve bir araştırma ilgili adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="74702-170">The following sections provide you with more details and the steps that are related to an investigation.</span></span>  


## <a name="risky-sign-ins"></a><span data-ttu-id="74702-171">Riskli oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="74702-171">Risky sign-ins</span></span>

<span data-ttu-id="74702-172">Azure Active Directory algılar [risk olayı türleri](active-directory-reporting-risk-events.md#risk-event-types) gerçek zamanlı ve çevrimdışı.</span><span class="sxs-lookup"><span data-stu-id="74702-172">Azure Active Directory detects [risk event types](active-directory-reporting-risk-events.md#risk-event-types) in real-time and offline.</span></span> <span data-ttu-id="74702-173">Bir oturum açma için kullanıcı algılanan her risk olayı riskli oturum açma adı verilen mantıksal bir kavramken katkıda bulunur.</span><span class="sxs-lookup"><span data-stu-id="74702-173">Each risk event that has been detected for a sign-in of a user contributes to a logical concept called risky sign-in.</span></span> <span data-ttu-id="74702-174">Bir riskli oturum açma bir meşru bir kullanıcı hesabı sahibi tarafından gerçekleştirilmiş olabilecek olmayan bir oturum açma girişimi için göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="74702-174">A risky sign-in is an indicator for a sign-in attempt that might not have been performed by the legitimate owner of a user account.</span></span>


### <a name="sign-in-risk-level"></a><span data-ttu-id="74702-175">Oturum açma risk düzeyi</span><span class="sxs-lookup"><span data-stu-id="74702-175">Sign-in risk level</span></span>

<span data-ttu-id="74702-176">Oturum açma risk düzeyi bir oturum açma girişimi meşru bir kullanıcı hesabı sahibi tarafından gerçekleştirilmedi bir (yüksek, Orta veya düşük) olasılığını göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="74702-176">A sign-in risk level is an indication (High, Medium, or Low) of the likelihood that a sign-in attempt was not performed by the legitimate owner of a user account.</span></span>

### <a name="mitigating-sign-in-risk-events"></a><span data-ttu-id="74702-177">Oturum açma riski olaylar azaltılması</span><span class="sxs-lookup"><span data-stu-id="74702-177">Mitigating sign-in risk events</span></span>

<span data-ttu-id="74702-178">Bir azaltma, saldırgan güvenliği aşılmış kimlik veya cihaz kimliği veya cihaza güvenli bir duruma geri yüklemeden yararlanma yeteneği sınırlamak için bir eylemdir.</span><span class="sxs-lookup"><span data-stu-id="74702-178">A mitigation is an action to limit the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="74702-179">Bir azaltma kimlik veya aygıtla ilişkili önceki oturum açma risk olaylarını çözümlenmiyor.</span><span class="sxs-lookup"><span data-stu-id="74702-179">A mitigation does not resolve previous sign-in risk events associated with the identity or device.</span></span>

<span data-ttu-id="74702-180">Riskli oturum açma işlemleri otomatik olarak azaltmak için oturum açma riski güvenlik policicies yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74702-180">To mitigate risky sign-ins automatically, you can configure sign-in risk security policicies.</span></span> <span data-ttu-id="74702-181">Bu ilkeleri kullanarak, kullanıcı veya oturum açma riskli oturum açma işlemleri engelleme veya kullanıcının gerektiren çok faktörlü kimlik doğrulaması gerçekleştirmek için risk düzeyini göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="74702-181">Using these policies, you consider the risk level of the user or the sign-in to block risky sign-ins or require the user to perform multi-factor authentication.</span></span> <span data-ttu-id="74702-182">Bu Eylemler, bir saldırgan zarar görmesine neden bir çalınan kimlik bilgisinden faydalanmakta engelleyebilir ve kimliğini güvenli hale getirmek için biraz zaman verebilir.</span><span class="sxs-lookup"><span data-stu-id="74702-182">These actions may prevent an attacker from exploiting a stolen identity to cause damage, and may give you some time to secure the identity.</span></span>

### <a name="sign-in-risk-security-policy"></a><span data-ttu-id="74702-183">Oturum açma riski güvenlik ilkesi</span><span class="sxs-lookup"><span data-stu-id="74702-183">Sign-in risk security policy</span></span>
<span data-ttu-id="74702-184">Bir özel oturum açma riski değerlendirir ve önceden tanımlanmış koşullara ve kurallarına göre Azaltıcı Etkenler geçerli bir koşullu erişim ilkesi oturum açma riski ilkesidir.</span><span class="sxs-lookup"><span data-stu-id="74702-184">A sign-in risk policy is a conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

<span data-ttu-id="74702-185">![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1014.png "risk ilkesine oturum açma")</span><span class="sxs-lookup"><span data-stu-id="74702-185">![Sign-in risk policy](./media/active-directory-identityprotection/1014.png "Sign-in risk policy")</span></span>

<span data-ttu-id="74702-186">Azure AD kimlik koruması olanak tanıyarak riskli oturum açma işlemleri azaltma yönetmenize yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="74702-186">Azure AD Identity Protection helps you manage the mitigation of risky sign-ins by enabling you to:</span></span>

* <span data-ttu-id="74702-187">Kullanıcılar ve gruplar ilkenin uygulandığı ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="74702-187">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="74702-188">![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1015.png "risk ilkesine oturum açma")</span><span class="sxs-lookup"><span data-stu-id="74702-188">![Sign-in risk policy](./media/active-directory-identityprotection/1015.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="74702-189">İlke tetikleyen oturum açma risk düzeyi eşiği (düşük, Orta veya yüksek) ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="74702-189">Set the sign-in risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="74702-190">![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1016.png "risk ilkesine oturum açma")</span><span class="sxs-lookup"><span data-stu-id="74702-190">![Sign-in risk policy](./media/active-directory-identityprotection/1016.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="74702-191">İlke harekete geçirdiğinde zorlanacak denetimleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="74702-191">Set the controls to be enforced when the policy triggers:</span></span>  

    <span data-ttu-id="74702-192">![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1017.png "risk ilkesine oturum açma")</span><span class="sxs-lookup"><span data-stu-id="74702-192">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>
* <span data-ttu-id="74702-193">İlkeniz durumunu anahtarı:</span><span class="sxs-lookup"><span data-stu-id="74702-193">Switch the state of your policy:</span></span>

    <span data-ttu-id="74702-194">![MFA kayıt](./media/active-directory-identityprotection/403.png "MFA kayıt")</span><span class="sxs-lookup"><span data-stu-id="74702-194">![MFA Registration](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="74702-195">Gözden geçirin ve onu etkinleştirmek önce değişikliğin etkisini değerlendirin:</span><span class="sxs-lookup"><span data-stu-id="74702-195">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="74702-196">![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1018.png "risk ilkesine oturum açma")</span><span class="sxs-lookup"><span data-stu-id="74702-196">![Sign-in risk policy](./media/active-directory-identityprotection/1018.png "Sign-in risk policy")</span></span>

#### <a name="what-you-need-to-know"></a><span data-ttu-id="74702-197">Bilmeniz gerekenler</span><span class="sxs-lookup"><span data-stu-id="74702-197">What you need to know</span></span>
<span data-ttu-id="74702-198">Çok faktörlü kimlik doğrulaması istemek için bir oturum açma riski güvenlik ilkesini yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="74702-198">You can configure a sign-in risk security policy to require multi-factor authentication:</span></span>

<span data-ttu-id="74702-199">![Oturum açma risk ilkesine](./media/active-directory-identityprotection/1017.png "risk ilkesine oturum açma")</span><span class="sxs-lookup"><span data-stu-id="74702-199">![Sign-in risk policy](./media/active-directory-identityprotection/1017.png "Sign-in risk policy")</span></span>

<span data-ttu-id="74702-200">Ancak, güvenlik nedeniyle, bu ayar yalnızca çok faktörlü kimlik doğrulaması için önceden kaydedilmiş olan kullanıcılar için çalışır.</span><span class="sxs-lookup"><span data-stu-id="74702-200">However, for security reasons, this setting only works for users that have already been registered for multi-factor authentication.</span></span> <span data-ttu-id="74702-201">Çok faktörlü kimlik doğrulaması için henüz kaydedilmemiş bir kullanıcı için çok faktörlü kimlik doğrulama gerektirecek şekilde Koşul gerçekleştiyse, kullanıcı engellendi.</span><span class="sxs-lookup"><span data-stu-id="74702-201">If the condition to require multi-factor authentication is satisfied for a user who is not yet registered for multi-factor authentication, the user is blocked.</span></span>

<span data-ttu-id="74702-202">Riskli oturum açmalar için çok faktörlü kimlik doğrulamasını zorunlu kılmak istiyorsanız en iyi uygulama, aşağıdakileri yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="74702-202">As a best practice, if you want to require multi-factor authentication for risky sign-ins, you should:</span></span>

1. <span data-ttu-id="74702-203">Etkinleştirme [çok faktörlü kimlik doğrulaması kayıt ilkesi](#multi-factor-authentication-registration-policy) etkilenen kullanıcılar için.</span><span class="sxs-lookup"><span data-stu-id="74702-203">Enable the [multi-factor authentication registration policy](#multi-factor-authentication-registration-policy) for the affected users.</span></span>
2. <span data-ttu-id="74702-204">Etkilenen kullanıcılar oturum açmak için MFA kayıt gerçekleştirmek için riskli olmayan bir oturumda gerektirir</span><span class="sxs-lookup"><span data-stu-id="74702-204">Require the affected users to login in a non-risky session to perform a MFA registration</span></span>

<span data-ttu-id="74702-205">Bu adımları tamamladıktan, çok faktörlü kimlik doğrulamasının bir riskli oturum açma için gerekli sağlar.</span><span class="sxs-lookup"><span data-stu-id="74702-205">Completing these steps ensures that multi-factor authentication is required for a risky sign-in.</span></span>

#### <a name="best-practices"></a><span data-ttu-id="74702-206">En iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="74702-206">Best practices</span></span>
<span data-ttu-id="74702-207">Seçerek bir **yüksek** eşik bir ilke tetiklenir ve kullanıcılara etkisini en aza indirger zamanların sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="74702-207">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>  

<span data-ttu-id="74702-208">Ancak, dışlar **düşük** ve **orta** gerçekleştirilen oturum açma bayrağı risk ilkesinden, saldırgan güvenliği aşılmış kimlik bilgisinden faydalanmakta gelen engelleyebilir değil.</span><span class="sxs-lookup"><span data-stu-id="74702-208">However, it excludes **Low** and **Medium** sign-ins flagged for risk from the policy, which may not block an attacker from exploiting a compromised identity.</span></span>

<span data-ttu-id="74702-209">İlke ayarlarken</span><span class="sxs-lookup"><span data-stu-id="74702-209">When setting the policy,</span></span>

* <span data-ttu-id="74702-210">Sağlamadığı / çok faktörlü kimlik doğrulamasına sahip olmadığınız kullanıcılar Dışla</span><span class="sxs-lookup"><span data-stu-id="74702-210">Exclude users who do not/cannot have multi-factor authentication</span></span>
* <span data-ttu-id="74702-211">Yerel ayarlar ilkesini etkinleştirme olduğu pratik kullanıcılar hariç tutmak (örneğin hiçbir erişim Yardım Masası)</span><span class="sxs-lookup"><span data-stu-id="74702-211">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="74702-212">Çok fazla yanlış pozitifler (geliştiriciler, güvenlik analistleri) oluşturmak büyük olasılıkla kullanıcıları dışlama</span><span class="sxs-lookup"><span data-stu-id="74702-212">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="74702-213">Kullanım bir **yüksek** eşiği ilk ilke dağıtımı, sırasında veya son kullanıcılar tarafından görülen sorunları en aza gerekir.</span><span class="sxs-lookup"><span data-stu-id="74702-213">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="74702-214">Kullanım bir **düşük** kuruluşunuz daha yüksek güvenlik gerektiriyorsa eşiği.</span><span class="sxs-lookup"><span data-stu-id="74702-214">Use a **Low**  threshold if your organization requires greater security.</span></span> <span data-ttu-id="74702-215">Seçerek bir **düşük** eşik ek kullanıcı oturum açma zorluklar, ancak daha yüksek düzeyde güvenlik sunar.</span><span class="sxs-lookup"><span data-stu-id="74702-215">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="74702-216">İçin bir kural yapılandırmak için çoğu kuruluş için önerilen varsayılan olan bir **orta** kullanılabilirlik ve güvenlik arasında bir denge eşiği.</span><span class="sxs-lookup"><span data-stu-id="74702-216">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="74702-217">Oturum açma risk ilkesine şöyledir:</span><span class="sxs-lookup"><span data-stu-id="74702-217">The sign-in risk policy is:</span></span>

* <span data-ttu-id="74702-218">Tüm tarayıcı trafiğini ve modern kimlik doğrulaması kullanarak oturum açma işlemleri için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="74702-218">Applied to all browser traffic and sign-ins using modern authentication.</span></span>
* <span data-ttu-id="74702-219">WS-Trust uç noktada ADFS gibi Federasyon IDP devre dışı bırakarak eski güvenlik protokollerini kullanarak uygulamalar için geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="74702-219">Not applied to applications using older security protocols by disabling the WS-Trust endpoint at the federated IDP, such as ADFS.</span></span>

<span data-ttu-id="74702-220">**Risk olaylarını** kimlik koruması konsolundaki sayfasında tüm olayları listeler:</span><span class="sxs-lookup"><span data-stu-id="74702-220">The **Risk Events** page in the Identity Protection console lists all events:</span></span>

* <span data-ttu-id="74702-221">Bu ilkenin uygulandığı</span><span class="sxs-lookup"><span data-stu-id="74702-221">This policy was applied to</span></span>
* <span data-ttu-id="74702-222">Gözden geçirme etkinliği ve eylem uygun olup olmadığını belirleme</span><span class="sxs-lookup"><span data-stu-id="74702-222">You can review the activity and determine whether the action was appropriate or not</span></span>

<span data-ttu-id="74702-223">İlgili kullanıcı deneyimi genel bakış için bkz:</span><span class="sxs-lookup"><span data-stu-id="74702-223">For an overview of the related user experience, see:</span></span>

* [<span data-ttu-id="74702-224">Oturum açma riskli kurtarma</span><span class="sxs-lookup"><span data-stu-id="74702-224">Risky sign-in recovery</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-recovery)
* [<span data-ttu-id="74702-225">Riskli oturum engellenen açma</span><span class="sxs-lookup"><span data-stu-id="74702-225">Risky sign-in blocked</span></span>](active-directory-identityprotection-flows.md#risky-sign-in-blocked)  
* [<span data-ttu-id="74702-226">Oturum açma deneyimlerini Azure AD kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="74702-226">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)  

<span data-ttu-id="74702-227">**İlgili yapılandırma iletişim kutusunu açmak için**:</span><span class="sxs-lookup"><span data-stu-id="74702-227">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="74702-228">Üzerinde **Azure AD Identity Protection** dikey penceresinde, **yapılandırma** 'yi tıklatın **oturum açma risk ilkesine**.</span><span class="sxs-lookup"><span data-stu-id="74702-228">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Sign-in risk policy**.</span></span>

    <span data-ttu-id="74702-229">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1014.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="74702-229">![User ridk policy](./media/active-directory-identityprotection/1014.png "User ridk policy")</span></span>



## <a name="users-flagged-for-risk"></a><span data-ttu-id="74702-230">Riskli oldukları belirlenen kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="74702-230">Users flagged for risk</span></span>

<span data-ttu-id="74702-231">Tüm etkin [risk olayları](active-directory-identity-protection-risk-events.md) , algılandı Azure Active Directory tarafından katkıda bulunan bir kullanıcı için kullanıcı risk adlı mantıksal bir kavramken.</span><span class="sxs-lookup"><span data-stu-id="74702-231">All active [risk events](active-directory-identity-protection-risk-events.md) that were detected by Azure Active Directory for a user contribute to a logical concept called user risk.</span></span> <span data-ttu-id="74702-232">Risk bayrak eklenen kullanıcı geçirildiğini bir kullanıcı hesabı için bir göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="74702-232">A user flagged for risk is an indicator for a user account that might have been compromised.</span></span>

![Riskli oldukları belirlenen kullanıcılar](./media/active-directory-identityprotection/1200.png)


### <a name="user-risk-level"></a><span data-ttu-id="74702-234">Kullanıcı risk düzeyi</span><span class="sxs-lookup"><span data-stu-id="74702-234">User risk level</span></span>

<span data-ttu-id="74702-235">Bir kullanıcı risk düzeyi (yüksek, Orta veya düşük), kullanıcının kimliğini aşılmış olasılığını göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="74702-235">A user risk level is an indication (High, Medium, or Low) of the likelihood that the user’s identity has been compromised.</span></span> <span data-ttu-id="74702-236">Bir kullanıcı kimliğiyle ilişkili kullanıcı risk olaylarına göre hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="74702-236">It is calculated based on the user risk events that are associated with a user's identity.</span></span>

<span data-ttu-id="74702-237">Bir risk olayı ya da durumudur **etkin** veya **kapalı**.</span><span class="sxs-lookup"><span data-stu-id="74702-237">The status of a risk event is either **Active** or **Closed**.</span></span> <span data-ttu-id="74702-238">Yalnızca olayları risk **etkin** kullanıcı risk düzeyi hesaplamaya katkıda.</span><span class="sxs-lookup"><span data-stu-id="74702-238">Only risk events that are **Active** contribute to the user risk level calculation.</span></span>

<span data-ttu-id="74702-239">Kullanıcı risk düzeyi, aşağıdaki girişleri kullanılarak hesaplanır:</span><span class="sxs-lookup"><span data-stu-id="74702-239">The user risk level is calculated using the following inputs:</span></span>

* <span data-ttu-id="74702-240">Kullanıcı etkileyen etkin risk olayları</span><span class="sxs-lookup"><span data-stu-id="74702-240">Active risk events impacting the user</span></span>
* <span data-ttu-id="74702-241">Bu olayların risk düzeyi</span><span class="sxs-lookup"><span data-stu-id="74702-241">Risk level of these events</span></span>
* <span data-ttu-id="74702-242">Gerçekleştirilen tüm düzeltme eylemlerini olup önlemlerin</span><span class="sxs-lookup"><span data-stu-id="74702-242">Whether any remediation actions have been taken</span></span>

<span data-ttu-id="74702-243">![Kullanıcı riskleri](./media/active-directory-identityprotection/1031.png "kullanıcı riskleri")</span><span class="sxs-lookup"><span data-stu-id="74702-243">![User risks](./media/active-directory-identityprotection/1031.png "User risks")</span></span>

<span data-ttu-id="74702-244">Oturum açma riskli kullanıcıların engellemek koşullu erişim ilkeleri oluşturmak için kullanıcı risk düzeyleri kullanın veya güvenli bir şekilde parolalarını değiştirmek için bunları zorlayın.</span><span class="sxs-lookup"><span data-stu-id="74702-244">You can use the user risk levels to create conditional access policies that block risky users from signing in, or force them to securely change their password.</span></span>

### <a name="closing-risk-events-manually"></a><span data-ttu-id="74702-245">Risk olaylarını el ile kapatma</span><span class="sxs-lookup"><span data-stu-id="74702-245">Closing risk events manually</span></span>

<span data-ttu-id="74702-246">Çoğu durumda, risk olayları otomatik olarak kapatmak için sıfırlama güvenli bir parola gibi düzeltme eylemleri gerçekleştirecek.</span><span class="sxs-lookup"><span data-stu-id="74702-246">In most cases, you will take remediation actions such as a secure password reset to automatically close risk events.</span></span> <span data-ttu-id="74702-247">Ancak, bu her zaman mümkün olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="74702-247">However, this might not always be possible.</span></span>  
<span data-ttu-id="74702-248">Bu, örneğin, bir durumdur, ne zaman:</span><span class="sxs-lookup"><span data-stu-id="74702-248">This is, for example, the case, when:</span></span>

* <span data-ttu-id="74702-249">Etkin risk olaylarına sahip bir kullanıcı silindi</span><span class="sxs-lookup"><span data-stu-id="74702-249">A user with Active risk events has been deleted</span></span>
* <span data-ttu-id="74702-250">Bildirilen risk olayı sahip olan gerçekleştireceğini yasal kullanıcı tarafından bir araştırma ortaya çıkarır</span><span class="sxs-lookup"><span data-stu-id="74702-250">An investigation reveals that a reported risk event has been perform by the legitimate user</span></span>

<span data-ttu-id="74702-251">Risk olaylarını olduğundan **etkin** kullanıcı risk hesaplama katkıda, el ile risk olaylarını el ile kapatarak risk düzeyini düşürmek olabilir.</span><span class="sxs-lookup"><span data-stu-id="74702-251">Because risk events that are **Active** contribute to the user risk calculation, you may have to manually lower a risk level by closing risk events manually.</span></span>  
<span data-ttu-id="74702-252">Araştırma sürecinde herhangi bir risk olayı durumunu değiştirmek için aşağıdaki eylemlerden birini gerçekleştirin seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="74702-252">During the course of investigation, you can choose to take any of these actions to change the status of a risk event:</span></span>

<span data-ttu-id="74702-253">![Eylemler](./media/active-directory-identityprotection/34.png "Eylemler")</span><span class="sxs-lookup"><span data-stu-id="74702-253">![Actions](./media/active-directory-identityprotection/34.png "Actions")</span></span>

* <span data-ttu-id="74702-254">**Gidermek** - bir risk olayı araştırdıktan sonra uygun düzeltme eylemi kimlik koruması dışında sürdü ve risk olayı kapalı, düşünülmesi gereken düşünüyorsanız olayı çözümlenmiş olarak işaretler.</span><span class="sxs-lookup"><span data-stu-id="74702-254">**Resolve** - If after investigating a risk event, you took an appropriate remediation action outside Identity Protection, and you believe that the risk event should be considered closed, mark the event as Resolved.</span></span> <span data-ttu-id="74702-255">Çözümlenmiş olaylar risk olayın durumu kapalı olarak ayarlanır ve risk olay artık kullanıcı risk katkıda bulunur.</span><span class="sxs-lookup"><span data-stu-id="74702-255">Resolved events will set the risk event’s status to Closed and the risk event will no longer contribute to user risk.</span></span>
* <span data-ttu-id="74702-256">**Hatalı pozitif olarak işaretlemek** -bazı durumlarda, bir risk olayı araştırmak ve olabilirsiniz, yanlış bir riskli işaretlenen olduğunu bulmak.</span><span class="sxs-lookup"><span data-stu-id="74702-256">**Mark as false-positive** - In some cases, you may investigate a risk event and discover that it was incorrectly flagged as a risky.</span></span> <span data-ttu-id="74702-257">Risk olayı hatalı pozitif olarak işaretleyerek bu tür yinelenme sayısını azaltmaya yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="74702-257">You can help reduce the number of such occurrences by marking the risk event as False-positive.</span></span> <span data-ttu-id="74702-258">Bu, makine öğrenimi algoritmaları sınıflandırma benzer olayların gelecekte geliştirmeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="74702-258">This will help the machine learning algorithms to improve the classification of similar events in the future.</span></span> <span data-ttu-id="74702-259">Hatalı pozitif olayları için durumudur **kapalı** ve kullanıcı risk artık katkıda bulunur.</span><span class="sxs-lookup"><span data-stu-id="74702-259">The status of false-positive events is to **Closed** and they will no longer contribute to user risk.</span></span>
* <span data-ttu-id="74702-260">**Yoksay** - herhangi bir düzeltme eylemi olmadı ancak etkin listeden kaldırılacak risk olayı istiyorsanız bir risk olayı yoksay işaretleyebilirsiniz ve olay durumu kapatılacak.</span><span class="sxs-lookup"><span data-stu-id="74702-260">**Ignore** - If you have not taken any remediation action, but want the risk event to be removed from the active list, you can mark a risk event Ignore and the event status will be Closed.</span></span> <span data-ttu-id="74702-261">Yoksayılan olayları için kullanıcı riski katkıda bulunmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="74702-261">Ignored events do not contribute to user risk.</span></span> <span data-ttu-id="74702-262">Bu seçenek yalnızca olağan dışı durumlarda kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="74702-262">This option should only be used under unusual circumstances.</span></span>
* <span data-ttu-id="74702-263">**Yeniden etkinleştirme** -Risk el ile kapatılan olaylar (seçerek **gidermek**, **yanlış pozitif**, veya **Yoksay**) olayı ayarlanırken etkinleştirilebilir Durum geri **etkin**.</span><span class="sxs-lookup"><span data-stu-id="74702-263">**Reactivate** - Risk events that were manually closed (by choosing **Resolve**, **False positive**, or **Ignore**) can be reactivated, setting the event status back to **Active**.</span></span> <span data-ttu-id="74702-264">Yeniden etkinleştirilen risk olaylarını kullanıcı risk düzeyi hesaplama katkıda.</span><span class="sxs-lookup"><span data-stu-id="74702-264">Reactivated risk events contribute to the user risk level calculation.</span></span> <span data-ttu-id="74702-265">Risk olaylarına (güvenli bir parola sıfırlama gibi) düzeltme aracılığıyla kapalı etkinleştirilemez.</span><span class="sxs-lookup"><span data-stu-id="74702-265">Risk events closed through remediation (such as a secure password reset) cannot be reactivated.</span></span>

<span data-ttu-id="74702-266">**İlgili yapılandırma iletişim kutusunu açmak için**:</span><span class="sxs-lookup"><span data-stu-id="74702-266">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="74702-267">Üzerinde **Azure AD Identity Protection** dikey altında **Araştır**, tıklatın **Risk olayları**.</span><span class="sxs-lookup"><span data-stu-id="74702-267">On the **Azure AD Identity Protection** blade, under **Investigate**, click **Risk events**.</span></span>

    <span data-ttu-id="74702-268">![El ile parola sıfırlama](./media/active-directory-identityprotection/1002.png "el ile parola sıfırlama")</span><span class="sxs-lookup"><span data-stu-id="74702-268">![Manual password reset](./media/active-directory-identityprotection/1002.png "Manual password reset")</span></span>
2. <span data-ttu-id="74702-269">İçinde **Risk olayları** listesinde, bir risk tıklayın.</span><span class="sxs-lookup"><span data-stu-id="74702-269">In the **Risk events** list, click a risk.</span></span>

    <span data-ttu-id="74702-270">![El ile parola sıfırlama](./media/active-directory-identityprotection/1003.png "el ile parola sıfırlama")</span><span class="sxs-lookup"><span data-stu-id="74702-270">![Manual password reset](./media/active-directory-identityprotection/1003.png "Manual password reset")</span></span>
3. <span data-ttu-id="74702-271">Risk dikey penceresinde, bir kullanıcı sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="74702-271">On the risk blade, right-click a user.</span></span>

    <span data-ttu-id="74702-272">![El ile parola sıfırlama](./media/active-directory-identityprotection/1004.png "el ile parola sıfırlama")</span><span class="sxs-lookup"><span data-stu-id="74702-272">![Manual password reset](./media/active-directory-identityprotection/1004.png "Manual password reset")</span></span>

### <a name="closing-all-risk-events-for-a-user-manually"></a><span data-ttu-id="74702-273">Bir kullanıcı için tüm risk olaylarını el ile kapatma</span><span class="sxs-lookup"><span data-stu-id="74702-273">Closing all risk events for a user manually</span></span>
<span data-ttu-id="74702-274">El ile bir kullanıcı için risk olayları ayrı ayrı kapatmak yerine, Azure Active Directory kimlik koruması Ayrıca, tek bir tıklatmayla bir kullanıcı için tüm olayları kapatmak için bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="74702-274">Instead of manually closing risk events for a user individually, Azure Active Directory Identity Protection also provides you with a method to close all events for a user with one click.</span></span>

<span data-ttu-id="74702-275">![Eylemler](./media/active-directory-identityprotection/2222.png "Eylemler")</span><span class="sxs-lookup"><span data-stu-id="74702-275">![Actions](./media/active-directory-identityprotection/2222.png "Actions")</span></span>

<span data-ttu-id="74702-276">Tıkladığınızda **tüm olayları kapatmak**, tüm olayları kapatılır ve etkilenen kullanıcı artık risk altında.</span><span class="sxs-lookup"><span data-stu-id="74702-276">When you click **Dismiss all events**, all events are closed and the affected user is no longer at risk.</span></span>

### <a name="remediating-user-risk-events"></a><span data-ttu-id="74702-277">Düzelterek kullanıcı risk olayı</span><span class="sxs-lookup"><span data-stu-id="74702-277">Remediating user risk events</span></span>

<span data-ttu-id="74702-278">Bir düzeltme güvenli bir kimlik veya önceden şüpheli veya tehlikeye bilinen bir cihaz için bir eylemdir.</span><span class="sxs-lookup"><span data-stu-id="74702-278">A remediation is an action to secure an identity or a device that was previously suspected or known to be compromised.</span></span> <span data-ttu-id="74702-279">Bir düzeltme eylemi kimliği veya cihaza güvenli bir duruma geri yükler ve kimlik veya aygıtla ilişkili önceki risk olaylarını giderir.</span><span class="sxs-lookup"><span data-stu-id="74702-279">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

<span data-ttu-id="74702-280">Kullanıcı risk olaylarını düzeltmek için şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="74702-280">To remediate user risk events, you can:</span></span>

* <span data-ttu-id="74702-281">Güvenli parola kullanıcı risk olaylarına elle düzeltmek için sıfırlaması gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="74702-281">Perform a secure password reset to remediate user risk events manually</span></span>
* <span data-ttu-id="74702-282">Bir kullanıcı risk Güvenlik İlkesi'azaltılmasına veya kullanıcı risk olayları otomatik olarak düzeltmek için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="74702-282">Configure a user risk security policy to mitigate or remediate user risk events automatically</span></span>
* <span data-ttu-id="74702-283">Etkilenen aygıt yeniden görüntü</span><span class="sxs-lookup"><span data-stu-id="74702-283">Re-image the infected device</span></span>  

#### <a name="manual-secure-password-reset"></a><span data-ttu-id="74702-284">El ile güvenli parola sıfırlama</span><span class="sxs-lookup"><span data-stu-id="74702-284">Manual secure password reset</span></span>
<span data-ttu-id="74702-285">Güvenli parola sıfırlama birçok risk olayı için geçerli bir düzeltme ve gerçekleştirildiğinde, otomatik olarak bu risk olaylarını kapatır ve kullanıcı risk düzeyi yeniden hesaplar.</span><span class="sxs-lookup"><span data-stu-id="74702-285">A secure password reset is an effective remediation for many risk events, and when performed, automatically closes these risk events and recalculates the user risk level.</span></span> <span data-ttu-id="74702-286">Parola için riskli bir kullanıcı sıfırlama başlatmak için kimlik koruması panoyu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74702-286">You can use the Identity Protection dashboard to initiate a password reset for a risky user.</span></span>

<span data-ttu-id="74702-287">İlgili iletişim kutusu, bir parola sıfırlama için iki farklı yöntem sunar:</span><span class="sxs-lookup"><span data-stu-id="74702-287">The related dialog provides two different methods to reset a password:</span></span>

<span data-ttu-id="74702-288">**Parola sıfırlama** - seçin **parolasını sıfırlamak kullanıcının gerektiren** kullanıcı çok faktörlü kimlik doğrulaması için kaydedildiyse otomatik olarak kurtarmaya izin vermek için.</span><span class="sxs-lookup"><span data-stu-id="74702-288">**Reset password** - Select **Require the user to reset their password** to allow the user to self-recover if the user has registered for multi-factor authentication.</span></span> <span data-ttu-id="74702-289">Kullanıcının bir sonraki oturum açma sırasında kullanıcı çok faktörlü kimlik doğrulaması sınaması başarılı bir şekilde çözmek için gereken ve daha sonra parolayı değiştirmek zorunda.</span><span class="sxs-lookup"><span data-stu-id="74702-289">During the user's next sign-in, the user will be required to solve a multi-factor authentication challenge successfully and then, forced to change the password.</span></span> <span data-ttu-id="74702-290">Kullanıcı hesabı kayıtlı çok faktörlü kimlik doğrulama değilse, bu seçenek kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="74702-290">This option isn't available if the user account is not already registered multi-factor authentication.</span></span>

<span data-ttu-id="74702-291">**Geçici parolayı** - seçin **geçici bir parola oluşturmak** hemen mevcut parolayı geçersiz kılmak ve kullanıcı için yeni bir geçici parola oluşturun.</span><span class="sxs-lookup"><span data-stu-id="74702-291">**Temporary password** - Select **Generate a temporary password** to immediately invalidate the existing password, and create a new temporary password for the user.</span></span> <span data-ttu-id="74702-292">Yeni bir geçici parola kullanıcı için bir alternatif e-posta adresi veya Kullanıcı Yöneticisi göndermek.</span><span class="sxs-lookup"><span data-stu-id="74702-292">Send the new temporary password to an alternate email address for the user or to the user's manager.</span></span> <span data-ttu-id="74702-293">Parola geçici olduğundan, kullanıcı oturum açma sırasında parola değiştirme istenir.</span><span class="sxs-lookup"><span data-stu-id="74702-293">Because the password is temporary, the user will be prompted to change the password upon sign-in.</span></span>

<span data-ttu-id="74702-294">![İlke](./media/active-directory-identityprotection/1005.png "İlkesi")</span><span class="sxs-lookup"><span data-stu-id="74702-294">![Policy](./media/active-directory-identityprotection/1005.png "Policy")</span></span>

<span data-ttu-id="74702-295">**İlgili yapılandırma iletişim kutusunu açmak için**:</span><span class="sxs-lookup"><span data-stu-id="74702-295">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="74702-296">Üzerinde **Azure AD Identity Protection** dikey penceresinde tıklatın **bayrak eklenen kullanıcılar için risk**.</span><span class="sxs-lookup"><span data-stu-id="74702-296">On the **Azure AD Identity Protection** blade, click **Users flagged for risk**.</span></span>

    <span data-ttu-id="74702-297">![El ile parola sıfırlama](./media/active-directory-identityprotection/1006.png "el ile parola sıfırlama")</span><span class="sxs-lookup"><span data-stu-id="74702-297">![Manual password reset](./media/active-directory-identityprotection/1006.png "Manual password reset")</span></span>
2. <span data-ttu-id="74702-298">Kullanıcılar listesinden en az bir risk olaylarına sahip bir kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="74702-298">From the list of users, select a user with at least one risk events.</span></span>

    <span data-ttu-id="74702-299">![El ile parola sıfırlama](./media/active-directory-identityprotection/1007.png "el ile parola sıfırlama")</span><span class="sxs-lookup"><span data-stu-id="74702-299">![Manual password reset](./media/active-directory-identityprotection/1007.png "Manual password reset")</span></span>
3. <span data-ttu-id="74702-300">Kullanıcı dikey penceresinde **parola sıfırlama**.</span><span class="sxs-lookup"><span data-stu-id="74702-300">On the user blade, click **Reset password**.</span></span>

    <span data-ttu-id="74702-301">![El ile parola sıfırlama](./media/active-directory-identityprotection/1008.png "el ile parola sıfırlama")</span><span class="sxs-lookup"><span data-stu-id="74702-301">![Manual password reset](./media/active-directory-identityprotection/1008.png "Manual password reset")</span></span>

### <a name="user-risk-security-policy"></a><span data-ttu-id="74702-302">Kullanıcı risk güvenlik ilkesi</span><span class="sxs-lookup"><span data-stu-id="74702-302">User risk security policy</span></span>
<span data-ttu-id="74702-303">Kullanıcı risk güvenlik ilkesi belirli bir kullanıcıya risk düzeyi değerlendirir ve önceden tanımlanmış koşullara ve kurallarına göre düzeltme ve azaltma Eylemler uyguladığında bir koşullu erişim ilkesi var.</span><span class="sxs-lookup"><span data-stu-id="74702-303">A user risk security policy is a conditional access policy that evaluates the risk level to a specific user and applies remediation and mitigation actions based on predefined conditions and rules.</span></span>

<span data-ttu-id="74702-304">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1009.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="74702-304">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

<span data-ttu-id="74702-305">Azure AD kimlik koruması azaltma ve risk olanak tanıyarak bayrak eklenen kullanıcılar düzeltmesi yönetmenize yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="74702-305">Azure AD Identity Protection helps you manage the mitigation and remediation of users flagged for risk by enabling you to:</span></span>

* <span data-ttu-id="74702-306">Kullanıcılar ve gruplar ilkenin uygulandığı ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="74702-306">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="74702-307">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1010.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="74702-307">![User ridk policy](./media/active-directory-identityprotection/1010.png "User ridk policy")</span></span>
* <span data-ttu-id="74702-308">İlke tetikleyen kullanıcı risk düzeyi eşiği (düşük, Orta veya yüksek) ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="74702-308">Set the user risk level threshold (low, medium, or high) that triggers the policy:</span></span>

    <span data-ttu-id="74702-309">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1011.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="74702-309">![User ridk policy](./media/active-directory-identityprotection/1011.png "User ridk policy")</span></span>
* <span data-ttu-id="74702-310">İlke harekete geçirdiğinde zorlanacak denetimleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="74702-310">Set the controls to be enforced when the policy triggers:</span></span>

    <span data-ttu-id="74702-311">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1012.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="74702-311">![User ridk policy](./media/active-directory-identityprotection/1012.png "User ridk policy")</span></span>
* <span data-ttu-id="74702-312">İlkeniz durumunu anahtarı:</span><span class="sxs-lookup"><span data-stu-id="74702-312">Switch the state of your policy:</span></span>

    <span data-ttu-id="74702-313">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/403.png "MFA kayıt")</span><span class="sxs-lookup"><span data-stu-id="74702-313">![User ridk policy](./media/active-directory-identityprotection/403.png "MFA Registration")</span></span>
* <span data-ttu-id="74702-314">Gözden geçirin ve onu etkinleştirmek önce değişikliğin etkisini değerlendirin:</span><span class="sxs-lookup"><span data-stu-id="74702-314">Review and evaluate the impact of a change before activating it:</span></span>

    <span data-ttu-id="74702-315">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1013.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="74702-315">![User ridk policy](./media/active-directory-identityprotection/1013.png "User ridk policy")</span></span>

<span data-ttu-id="74702-316">Seçerek bir **yüksek** eşik bir ilke tetiklenir ve kullanıcılara etkisini en aza indirger zamanların sayısını azaltır.</span><span class="sxs-lookup"><span data-stu-id="74702-316">Choosing a **High** threshold reduces the number of times a policy is triggered and minimizes the impact to users.</span></span>
<span data-ttu-id="74702-317">Ancak, dışlar **düşük** ve **orta** kimlikleri veya cihazları, güvenli değil ilkesinden risk için işaretlenmiş kullanıcılar önceden şüpheli veya tehlikeye bilinmektedir.</span><span class="sxs-lookup"><span data-stu-id="74702-317">However, it excludes **Low** and **Medium** users flagged for risk from the policy, which may not secure identities or devices that were previously suspected or known to be compromised.</span></span>

<span data-ttu-id="74702-318">İlke ayarlarken</span><span class="sxs-lookup"><span data-stu-id="74702-318">When setting the policy,</span></span>

* <span data-ttu-id="74702-319">Çok fazla yanlış pozitifler (geliştiriciler, güvenlik analistleri) oluşturmak büyük olasılıkla kullanıcıları dışlama</span><span class="sxs-lookup"><span data-stu-id="74702-319">Exclude users who are likely to generate a lot of false-positives (developers, security analysts)</span></span>
* <span data-ttu-id="74702-320">Yerel ayarlar ilkesini etkinleştirme olduğu pratik kullanıcılar hariç tutmak (örneğin hiçbir erişim Yardım Masası)</span><span class="sxs-lookup"><span data-stu-id="74702-320">Exclude users in locales where enabling the policy is not practical (for example no access to helpdesk)</span></span>
* <span data-ttu-id="74702-321">Kullanım bir **yüksek** eşiği ilk ilke dağıtımı, sırasında veya son kullanıcılar tarafından görülen sorunları en aza gerekir.</span><span class="sxs-lookup"><span data-stu-id="74702-321">Use a **High** threshold during initial policy roll out, or if you must minimize challenges seen by end users.</span></span>
* <span data-ttu-id="74702-322">Kullanım bir **düşük** kuruluşunuz daha yüksek güvenlik gerektiriyorsa eşiği.</span><span class="sxs-lookup"><span data-stu-id="74702-322">Use a **Low** threshold if your organization requires greater security.</span></span> <span data-ttu-id="74702-323">Seçerek bir **düşük** eşik ek kullanıcı oturum açma zorluklar, ancak daha yüksek düzeyde güvenlik sunar.</span><span class="sxs-lookup"><span data-stu-id="74702-323">Selecting a **Low** threshold introduces additional user sign-in challenges, but increased security.</span></span>

<span data-ttu-id="74702-324">İçin bir kural yapılandırmak için çoğu kuruluş için önerilen varsayılan olan bir **orta** kullanılabilirlik ve güvenlik arasında bir denge eşiği.</span><span class="sxs-lookup"><span data-stu-id="74702-324">The recommended default for most organizations is to configure a rule for a **Medium** threshold to strike a balance between usability and security.</span></span>

<span data-ttu-id="74702-325">İlgili kullanıcı deneyimi genel bakış için bkz:</span><span class="sxs-lookup"><span data-stu-id="74702-325">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="74702-326">[Hesap kurtarma akışı tehlikeye](active-directory-identityprotection-flows.md#compromised-account-recovery).</span><span class="sxs-lookup"><span data-stu-id="74702-326">[Compromised account recovery flow](active-directory-identityprotection-flows.md#compromised-account-recovery).</span></span>  
* <span data-ttu-id="74702-327">[Hesap engellendi akış tehlikeye](active-directory-identityprotection-flows.md#compromised-account-blocked).</span><span class="sxs-lookup"><span data-stu-id="74702-327">[Compromised account blocked flow](active-directory-identityprotection-flows.md#compromised-account-blocked).</span></span>  

<span data-ttu-id="74702-328">**İlgili yapılandırma iletişim kutusunu açmak için**:</span><span class="sxs-lookup"><span data-stu-id="74702-328">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="74702-329">Üzerinde **Azure AD Identity Protection** dikey penceresinde, **yapılandırma** 'yi tıklatın **kullanıcı risk ilkesine**.</span><span class="sxs-lookup"><span data-stu-id="74702-329">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **User risk policy**.</span></span>

    <span data-ttu-id="74702-330">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1009.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="74702-330">![User ridk policy](./media/active-directory-identityprotection/1009.png "User ridk policy")</span></span>

### <a name="mitigating-user-risk-events"></a><span data-ttu-id="74702-331">Kullanıcı risk olaylar azaltılması</span><span class="sxs-lookup"><span data-stu-id="74702-331">Mitigating user risk events</span></span>
<span data-ttu-id="74702-332">Yöneticiler kullanıcı risk güvenlik ilkesi oturum açma risk düzeyine bağlı olarak bağlı kullanıcıları engelle ayarlayabilir.</span><span class="sxs-lookup"><span data-stu-id="74702-332">Administrators can set a user risk security policy to block users upon sign-in depending on the risk level.</span></span>

<span data-ttu-id="74702-333">Bir oturum açma engelleme:</span><span class="sxs-lookup"><span data-stu-id="74702-333">Blocking a sign-in:</span></span>

* <span data-ttu-id="74702-334">Etkilenen kullanıcı için yeni kullanıcı risk olaylarına oluşturulmasını engeller</span><span class="sxs-lookup"><span data-stu-id="74702-334">Prevents the generation of new user risk events for the affected user</span></span>
* <span data-ttu-id="74702-335">Yöneticilerin el ile kullanıcı kimliğini etkileyen risk olaylarına düzeltin ve güvenli bir duruma geri olanak tanır</span><span class="sxs-lookup"><span data-stu-id="74702-335">Enables administrators to manually remediate the risk events affecting the user's identity and restore it to a secure state</span></span>



## <a name="multi-factor-authentication-registration-policy"></a><span data-ttu-id="74702-336">Çok faktörlü kimlik doğrulaması kayıt ilkesi</span><span class="sxs-lookup"><span data-stu-id="74702-336">Multi-factor authentication registration policy</span></span>
<span data-ttu-id="74702-337">Azure çok faktörlü kimlik doğrulaması daha fazlasını bir kullanıcı adı ve parola kullanılmasını gerektiren kim olduğunuzu doğrulama bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="74702-337">Azure multi-factor authentication is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="74702-338">İkinci bir kullanıcı oturum açmaları ve işlemleri için güvenlik katmanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="74702-338">It provides a second layer of security to user sign-ins and transactions.</span></span>  
<span data-ttu-id="74702-339">Çünkü kullanıcı oturum açma işlemleri için Azure çok faktörlü kimlik doğrulaması ihtiyaç duyduğunuz öneririz:</span><span class="sxs-lookup"><span data-stu-id="74702-339">We recommend that you require Azure multi-factor authentication for user sign-ins because it:</span></span>

* <span data-ttu-id="74702-340">Kolay doğrulama seçeneklerini aralıklı güçlü kimlik doğrulaması sunar</span><span class="sxs-lookup"><span data-stu-id="74702-340">Delivers strong authentication with a range of easy verification options</span></span>
* <span data-ttu-id="74702-341">Kuruluşunuz korumak ve hesap ödün kurtarmak için hazırlama önemli bir rol oynar</span><span class="sxs-lookup"><span data-stu-id="74702-341">Plays a key role in preparing your organization to protect and recover from account compromises</span></span>

<span data-ttu-id="74702-342">![Kullanıcı ridk İlkesi](./media/active-directory-identityprotection/1019.png "kullanıcı ridk İlkesi")</span><span class="sxs-lookup"><span data-stu-id="74702-342">![User ridk policy](./media/active-directory-identityprotection/1019.png "User ridk policy")</span></span>

<span data-ttu-id="74702-343">Daha fazla ayrıntı için bkz: [Azure multi-Factor Authentication nedir?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="74702-343">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

<span data-ttu-id="74702-344">Azure AD kimlik koruması sağlayan bir ilkesi yapılandırarak üretimini çok faktörlü kimlik doğrulaması kayıt yönetmenize yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="74702-344">Azure AD Identity Protection helps you manage the roll-out of multi-factor authentication registration by configuring a policy that enables you to:</span></span>

* <span data-ttu-id="74702-345">Kullanıcılar ve gruplar ilkenin uygulandığı ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="74702-345">Set the users and groups the policy applies to:</span></span>

    <span data-ttu-id="74702-346">![MFA ilkesini](./media/active-directory-identityprotection/1020.png "MFA İlkesi")</span><span class="sxs-lookup"><span data-stu-id="74702-346">![MFA policy](./media/active-directory-identityprotection/1020.png "MFA policy")</span></span>
* <span data-ttu-id="74702-347">İlke harekete geçirdiğinde yürütülebilmesi için denetimleri ayarlama::</span><span class="sxs-lookup"><span data-stu-id="74702-347">Set the controls to be enforced when the policy triggers::</span></span>  

    <span data-ttu-id="74702-348">![MFA ilkesini](./media/active-directory-identityprotection/1021.png "MFA İlkesi")</span><span class="sxs-lookup"><span data-stu-id="74702-348">![MFA policy](./media/active-directory-identityprotection/1021.png "MFA policy")</span></span>
* <span data-ttu-id="74702-349">İlkeniz durumunu anahtarı:</span><span class="sxs-lookup"><span data-stu-id="74702-349">Switch the state of your policy:</span></span>

    <span data-ttu-id="74702-350">![MFA ilkesini](./media/active-directory-identityprotection/403.png "MFA İlkesi")</span><span class="sxs-lookup"><span data-stu-id="74702-350">![MFA policy](./media/active-directory-identityprotection/403.png "MFA policy")</span></span>
* <span data-ttu-id="74702-351">Geçerli kayıt durumunu görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="74702-351">View the current registration status:</span></span>

    <span data-ttu-id="74702-352">![MFA ilkesini](./media/active-directory-identityprotection/1022.png "MFA İlkesi")</span><span class="sxs-lookup"><span data-stu-id="74702-352">![MFA policy](./media/active-directory-identityprotection/1022.png "MFA policy")</span></span>

<span data-ttu-id="74702-353">İlgili kullanıcı deneyimi genel bakış için bkz:</span><span class="sxs-lookup"><span data-stu-id="74702-353">For an overview of the related user experience, see:</span></span>

* <span data-ttu-id="74702-354">[Çok faktörlü kimlik doğrulaması kayıt akışı](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span><span class="sxs-lookup"><span data-stu-id="74702-354">[Multi-factor authentication registration flow](active-directory-identityprotection-flows.md#multi-factor-authentication-registration).</span></span>  
* <span data-ttu-id="74702-355">[Azure AD kimlik koruması ile karşılaştığında oturum açma](active-directory-identityprotection-flows.md).</span><span class="sxs-lookup"><span data-stu-id="74702-355">[Sign-in experiences with Azure AD Identity Protection](active-directory-identityprotection-flows.md).</span></span>  

<span data-ttu-id="74702-356">**İlgili yapılandırma iletişim kutusunu açmak için**:</span><span class="sxs-lookup"><span data-stu-id="74702-356">**To open the related configuration dialog**:</span></span>

- <span data-ttu-id="74702-357">Üzerinde **Azure AD Identity Protection** dikey penceresinde, **yapılandırma** 'yi tıklatın **çok faktörlü kimlik doğrulaması kayıt**.</span><span class="sxs-lookup"><span data-stu-id="74702-357">On the **Azure AD Identity Protection** blade, in the **Configure** section, click **Multi-factor authentication registration**.</span></span>

    <span data-ttu-id="74702-358">![MFA ilkesini](./media/active-directory-identityprotection/1019.png "MFA İlkesi")</span><span class="sxs-lookup"><span data-stu-id="74702-358">![MFA policy](./media/active-directory-identityprotection/1019.png "MFA policy")</span></span>

## <a name="next-steps"></a><span data-ttu-id="74702-359">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="74702-359">Next steps</span></span>
* [<span data-ttu-id="74702-360">Kanal 9: Azure AD ve kimlik göster: kimlik koruması Önizleme</span><span class="sxs-lookup"><span data-stu-id="74702-360">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

* [<span data-ttu-id="74702-361">Azure Active Directory kimlik koruması etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="74702-361">Enabling Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-enable.md)

* [<span data-ttu-id="74702-362">Azure Active Directory kimlik koruması tarafından algılanan güvenlik açığı</span><span class="sxs-lookup"><span data-stu-id="74702-362">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-vulnerabilities.md)

* [<span data-ttu-id="74702-363">Azure Active Directory risk olayları</span><span class="sxs-lookup"><span data-stu-id="74702-363">Azure Active Directory risk events</span></span>](active-directory-identity-protection-risk-events.md)

* [<span data-ttu-id="74702-364">Azure Active Directory kimlik koruması bildirimleri</span><span class="sxs-lookup"><span data-stu-id="74702-364">Azure Active Directory Identity Protection notifications</span></span>](active-directory-identityprotection-notifications.md)

* [<span data-ttu-id="74702-365">Azure Active Directory kimlik koruması Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="74702-365">Azure Active Directory Identity Protection playbook</span></span>](active-directory-identityprotection-playbook.md)

* [<span data-ttu-id="74702-366">Azure Active Directory kimlik koruması Kılavuzu sözlüğü</span><span class="sxs-lookup"><span data-stu-id="74702-366">Azure Active Directory Identity Protection glossary</span></span>](active-directory-identityprotection-glossary.md)

* [<span data-ttu-id="74702-367">Oturum açma deneyimlerini Azure AD kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="74702-367">Sign-in experiences with Azure AD Identity Protection</span></span>](active-directory-identityprotection-flows.md)

* [<span data-ttu-id="74702-368">Azure Active Directory kimlik koruması - kullanıcıların engelini kaldırma</span><span class="sxs-lookup"><span data-stu-id="74702-368">Azure Active Directory Identity Protection - How to unblock users</span></span>](active-directory-identityprotection-unblock-howto.md)

* [<span data-ttu-id="74702-369">Azure Active Directory kimlik koruması ve Microsoft Graph kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="74702-369">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>](active-directory-identityprotection-graph-getting-started.md)
