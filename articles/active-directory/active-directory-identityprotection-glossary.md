---
title: "Azure Active Directory kimlik koruması Kılavuzu sözlüğü | Microsoft Docs"
description: "Azure Active Directory kimlik koruması Kılavuzu sözlüğü"
services: active-directory
keywords: "Azure active directory kimlik koruması, cloud app discovery'yi, uygulamalar, güvenlik, risk, risk düzeyi, güvenlik açığı, güvenlik ilkesi, sözlük yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 833119a5-33d6-4482-adda-fa35218c72c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 2cf64925cff9a78cf83532a1cfd231f7a1d98304
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-glossary"></a><span data-ttu-id="86b93-104">Azure Active Directory kimlik koruması Kılavuzu sözlüğü</span><span class="sxs-lookup"><span data-stu-id="86b93-104">Azure Active Directory Identity Protection Glossary</span></span>
### <a name="at-risk-user"></a><span data-ttu-id="86b93-105">Risk (kullanıcı)</span><span class="sxs-lookup"><span data-stu-id="86b93-105">At risk (User)</span></span>
<span data-ttu-id="86b93-106">Bir veya daha fazla etkin risk olaylarına sahip bir kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="86b93-106">A user with one or more active risk events.</span></span> 

### <a name="atypical-sign-in-location"></a><span data-ttu-id="86b93-107">Oturum açma alışılmadık konumu</span><span class="sxs-lookup"><span data-stu-id="86b93-107">Atypical sign-in location</span></span>
<span data-ttu-id="86b93-108">Bir oturum açma bir coğrafi konumdan belirli kullanıcı, benzer kullanıcılar veya Kiracı için tipik değildir.</span><span class="sxs-lookup"><span data-stu-id="86b93-108">A sign-in from a geographic location that is not typical for the specific user, similar users, or the tenant.</span></span>

### <a name="azure-ad-identity-protection"></a><span data-ttu-id="86b93-109">Azure AD Kimlik Koruması</span><span class="sxs-lookup"><span data-stu-id="86b93-109">Azure AD Identity Protection</span></span>
<span data-ttu-id="86b93-110">Birleştirilmiş görünüme risk olaylarına ve olası güvenlik açıklarını kuruluşun kimlikleri etkileyen sağlayan Azure Active Directory güvenlik modül.</span><span class="sxs-lookup"><span data-stu-id="86b93-110">A security module of Azure Active Directory that provides a consolidated view into risk events and potential vulnerabilities affecting an organization’s identities.</span></span>

### <a name="conditional-access"></a><span data-ttu-id="86b93-111">Koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="86b93-111">Conditional access</span></span>
<span data-ttu-id="86b93-112">Kaynaklara erişim güvenliğini sağlamak için bir ilke.</span><span class="sxs-lookup"><span data-stu-id="86b93-112">A policy for securing access to resources.</span></span> <span data-ttu-id="86b93-113">Koşullu erişim kuralları Azure Active Directory'de depolanır ve kaynağa erişim izni vermeden önce Azure AD tarafından değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="86b93-113">Conditional access rules are stored in the Azure Active Directory and are evaluated by Azure AD before granting access to the resource.</span></span>  <span data-ttu-id="86b93-114">Örnek kuralları içeren kullanıcı konuma göre erişimi kısıtlama cihaz sistem durumu veya kullanıcı kimlik doğrulama yöntemi.</span><span class="sxs-lookup"><span data-stu-id="86b93-114">Example rules include restricting access based on user location, device health or user authentication method.</span></span>

### <a name="credentials"></a><span data-ttu-id="86b93-115">Kimlik Bilgileri</span><span class="sxs-lookup"><span data-stu-id="86b93-115">Credentials</span></span>
<span data-ttu-id="86b93-116">Tanımlama ve ağ kaynaklarını ve yerel erişim sağlamak için kullanılan kimlik kanıtı içeren bilgiler.</span><span class="sxs-lookup"><span data-stu-id="86b93-116">Information that includes identification and proof of identification that is used to gain access to local and network resources.</span></span> <span data-ttu-id="86b93-117">Kimlik bilgileri kullanıcı adları ve parolalar, akıllı kartlar ve sertifikalar gösterilebilir.</span><span class="sxs-lookup"><span data-stu-id="86b93-117">Examples of credentials are user names and passwords, smart cards, and certificates.</span></span>

### <a name="event"></a><span data-ttu-id="86b93-118">Olay</span><span class="sxs-lookup"><span data-stu-id="86b93-118">Event</span></span>
<span data-ttu-id="86b93-119">Azure Active Directory'de bir etkinliği kaydı.</span><span class="sxs-lookup"><span data-stu-id="86b93-119">A record of an activity in Azure Active Directory.</span></span>

### <a name="false-positive-risk-event"></a><span data-ttu-id="86b93-120">Hatalı pozitif (risk olay)</span><span class="sxs-lookup"><span data-stu-id="86b93-120">False-positive (risk event)</span></span>
<span data-ttu-id="86b93-121">Risk olay durumu risk olayı araştırılan ve hatalı bir risk olayı olarak bayrak eklenen gösteren bir kimlik koruması kullanıcı tarafından el ile ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="86b93-121">A risk event status set manually by an Identity Protection user, indicating that the risk event was investigated and was incorrectly flagged as a risk event.</span></span>

### <a name="identity"></a><span data-ttu-id="86b93-122">Kimlik</span><span class="sxs-lookup"><span data-stu-id="86b93-122">Identity</span></span>
<span data-ttu-id="86b93-123">Bir kişi veya parola veya sertifika gibi ölçütlere göre kimlik doğrulaması yoluyla doğrulanması gereken varlık.</span><span class="sxs-lookup"><span data-stu-id="86b93-123">A person or entity that must be verified by means of authentication, based on criteria such as password or a certificate.</span></span>

### <a name="identity-risk-event"></a><span data-ttu-id="86b93-124">Kimlik risk olayı</span><span class="sxs-lookup"><span data-stu-id="86b93-124">Identity risk event</span></span>
<span data-ttu-id="86b93-125">Anormal olarak kimlik koruması tarafından işaretlenen ve bir kimlik tehlikede olduğunu gösterebilecek AAD olay.</span><span class="sxs-lookup"><span data-stu-id="86b93-125">AAD event that was flagged as anomalous by Identity Protection, and may indicate that an identity has been compromised.</span></span>

### <a name="ignored-risk-event"></a><span data-ttu-id="86b93-126">Göz ardı (risk olay)</span><span class="sxs-lookup"><span data-stu-id="86b93-126">Ignored (risk event)</span></span>
<span data-ttu-id="86b93-127">Risk olay durumu risk olayı düzeltme eylemi yapılıyor olmadan kapalı olduğunu belirten bir kimlik koruması kullanıcı tarafından el ile ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="86b93-127">A risk event status set manually by an Identity Protection user, indicating that the risk event is closed without taking a remediation action.</span></span>

### <a name="impossible-travel-from-atypical-locations"></a><span data-ttu-id="86b93-128">Alışılmadık konumlardan imkansız seyahat</span><span class="sxs-lookup"><span data-stu-id="86b93-128">Impossible travel from atypical locations</span></span>
<span data-ttu-id="86b93-129">Aynı kullanıcı için iki oturum açma işleminden en az biri bir alışılmadık oturum açma konumundan olduğu ve oturum açma işlemleri arasındaki zaman fiziksel olarak bu konum arasında seyahat için harcanacak en düşük saat değerinden daha kısa olduğu algılandığında tetiklenen bir risk olayı.</span><span class="sxs-lookup"><span data-stu-id="86b93-129">A risk event triggered when two sign-ins for the same user are detected, where at least one of them is from an atypical sign-in location, and where the time between the sign-ins is shorter than the minimum time it would take to physically travel between these locations.</span></span>  

### <a name="investigation"></a><span data-ttu-id="86b93-130">Araştırma</span><span class="sxs-lookup"><span data-stu-id="86b93-130">Investigation</span></span>
<span data-ttu-id="86b93-131">Etkinlikler, günlükler ve düzeltme veya azaltma adımları gerekli olup olmadığını karar vermek için bir risk olayı ile ilgili diğer ilgili bilgileri gözden geçirme işlemi, varsa ve nasıl kimliğini aşılmış ve anlamak anlamak nasıl kimlik gizliliği kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="86b93-131">The process of reviewing the activities, logs, and other relevant information related to a risk event to decide whether remediation or mitigation steps are necessary, understand if and how the identity was compromised, and understand how the compromised identity was used.</span></span>

### <a name="leaked-credentials"></a><span data-ttu-id="86b93-132">Sızan kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="86b93-132">Leaked credentials</span></span>
<span data-ttu-id="86b93-133">Geçerli kullanıcı kimlik bilgilerini (kullanıcı adı ve parola) koyu web bizim Araştırmacıları tarafından yayımlandığını bulunduğunda tetiklenen bir risk olayı.</span><span class="sxs-lookup"><span data-stu-id="86b93-133">A risk event triggered when current user credentials (user name and password) are found posted publicly in the Dark   web by our researchers.</span></span>

### <a name="mitigation"></a><span data-ttu-id="86b93-134">Risk azaltma</span><span class="sxs-lookup"><span data-stu-id="86b93-134">Mitigation</span></span>
<span data-ttu-id="86b93-135">Sınırlamak veya saldırgan güvenliği aşılmış kimlik veya cihaz kimliği veya cihaza güvenli bir duruma geri yüklemeden yararlanma yeteneği ortadan kaldırmak için bir eylem.</span><span class="sxs-lookup"><span data-stu-id="86b93-135">An action to limit or eliminate the ability of an attacker to exploit a compromised identity or device without restoring the identity or device to a safe state.</span></span> <span data-ttu-id="86b93-136">Bir azaltma kimlik veya aygıtla ilişkili önceki risk olaylarını çözümlenmiyor.</span><span class="sxs-lookup"><span data-stu-id="86b93-136">A mitigation does not resolve previous risk events associated with the identity or device.</span></span>

### <a name="multi-factor-authentication"></a><span data-ttu-id="86b93-137">Multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="86b93-137">Multi-factor authentication</span></span>
<span data-ttu-id="86b93-138">Bir şeyler içerebilir, iki veya daha fazla kimlik doğrulama yöntemleri kullanıcının gerektiren bir kimlik doğrulama yöntemi, böyle bir sertifikası var; bir kullanıcı, kullanıcı adları, parolalar veya parolalar gibi bilir; bir parmak izi gibi fiziksel öznitelikleri; ve kişisel imza gibi kişisel öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="86b93-138">An authentication method that requires two or more authentication methods, which may include something the user has, such a certificate; something the user knows, such as user names, passwords, or pass phrases; physical attributes, such as a thumbprint; and personal attributes, such as a personal signature.</span></span>

### <a name="offline-detection"></a><span data-ttu-id="86b93-139">Çevrimdışı algılama</span><span class="sxs-lookup"><span data-stu-id="86b93-139">Offline detection</span></span>
<span data-ttu-id="86b93-140">Daha fazla bilgi ve oturum açma girişimi gibi bir olay risk değerlendirme zaten gerçekleştirilmedi bir olay için Olgu sonra algılanması.</span><span class="sxs-lookup"><span data-stu-id="86b93-140">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt after the fact, for an event that has already happened.</span></span>

### <a name="policy-condition"></a><span data-ttu-id="86b93-141">İlke durumu</span><span class="sxs-lookup"><span data-stu-id="86b93-141">Policy condition</span></span>
<span data-ttu-id="86b93-142">İlkesine dahil veya ondan dışlanan varlıklar (grupları, kullanıcıları, uygulamalar, cihaz platformları, cihaz durumları, IP aralıkları, istemci türlerinin) tanımlayan bir güvenlik ilkesi parçası.</span><span class="sxs-lookup"><span data-stu-id="86b93-142">A part of a security policy which defines the entities (groups, users, apps, device platforms, Device states, IP ranges, client types) included in the policy or excluded from it.</span></span>

### <a name="policy-rule"></a><span data-ttu-id="86b93-143">İlke kuralı</span><span class="sxs-lookup"><span data-stu-id="86b93-143">Policy rule</span></span>
<span data-ttu-id="86b93-144">İlkeyi ve ilke tetiklendiğinde gerçekleştirilen eylemleri tetikleyecek durumlarda tanımlayan bir güvenlik ilkesi parçası.</span><span class="sxs-lookup"><span data-stu-id="86b93-144">The part of a security policy which describes the circumstances that would trigger the policy, and the actions taken when the policy is triggered.</span></span>

### <a name="prevention"></a><span data-ttu-id="86b93-145">Önleme</span><span class="sxs-lookup"><span data-stu-id="86b93-145">Prevention</span></span>
<span data-ttu-id="86b93-146">Bir kimlik veya aygıtın kötüye yoluyla kuruluşun zarar önlemek için bir eylem şüpheli veya tehlikeye bildirin.</span><span class="sxs-lookup"><span data-stu-id="86b93-146">An action to prevent damage to the organization through abuse of an identity or device suspected or know to be compromised.</span></span> <span data-ttu-id="86b93-147">Önleme eylem aygıt ya da kimlik güvenli değildir ve önceki risk olaylarını çözümlenmiyor.</span><span class="sxs-lookup"><span data-stu-id="86b93-147">A prevention action does not secure the device or identity, and does not resolve previous risk events.</span></span>

### <a name="privileged-user"></a><span data-ttu-id="86b93-148">Ayrıcalıklı (kullanıcı)</span><span class="sxs-lookup"><span data-stu-id="86b93-148">Privileged (user)</span></span>
<span data-ttu-id="86b93-149">Bir risk olayı zaman genel bir yönetici gibi Azure Active Directory'de bir veya daha fazla kaynak kalıcı veya geçici yönetim izinlerine sahip bir kullanıcı Faturalama Yöneticisi, Hizmet Yöneticisi, Kullanıcı Yöneticisi ve parola Yöneticisi.</span><span class="sxs-lookup"><span data-stu-id="86b93-149">A user that at the time of a risk event, had permanent or temporary admin permissions to one or more resource in Azure Active Directory, such as a Global Administrator, Billing Administrator, Service Administrator, User administrator, and Password Administrator.</span></span> 

### <a name="real-time"></a><span data-ttu-id="86b93-150">Gerçek zamanlı</span><span class="sxs-lookup"><span data-stu-id="86b93-150">Real-time</span></span>
<span data-ttu-id="86b93-151">Gerçek zamanlı algılama bakın.</span><span class="sxs-lookup"><span data-stu-id="86b93-151">See Real-time detection.</span></span>

### <a name="real-time-detection"></a><span data-ttu-id="86b93-152">Gerçek zamanlı algılama</span><span class="sxs-lookup"><span data-stu-id="86b93-152">Real-time detection</span></span>
<span data-ttu-id="86b93-153">Anomalilerin algılanması ve olay önce oturum açma girişimi gibi bir olay risk değerlendirmesine devam etmesine izin verilir.</span><span class="sxs-lookup"><span data-stu-id="86b93-153">The detection of anomalies and evaluation of the risk of an event such as sign-in attempt before the event is allowed to proceed.</span></span>

### <a name="remediated-risk-event"></a><span data-ttu-id="86b93-154">Çözümlendi (risk olay)</span><span class="sxs-lookup"><span data-stu-id="86b93-154">Remediated (risk event)</span></span>
<span data-ttu-id="86b93-155">Risk olay durumu risk olayı Bu risk olay türü için standart düzeltme eylemini kullanarak düzeltilme olduğunu gösteren kimlik koruması tarafından otomatik olarak ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="86b93-155">A risk event status set automatically by Identity Protection, indicating that the risk event was remediated using the standard remediation action for this type of risk event.</span></span> <span data-ttu-id="86b93-156">Örneğin, kullanıcı parolasını sıfırlama, önceki parola aşılmış belirten birçok risk olayları otomatik olarak düzeltilir.</span><span class="sxs-lookup"><span data-stu-id="86b93-156">For example, when the user password is reset, many risk events that indicate that the previous password was compromised are automatically remediated.</span></span>

### <a name="remediation"></a><span data-ttu-id="86b93-157">Düzeltme</span><span class="sxs-lookup"><span data-stu-id="86b93-157">Remediation</span></span>
<span data-ttu-id="86b93-158">Bir kimlik veya önceden şüpheli veya tehlikeye bilinen bir cihazı güvenli hale getirmek için bir eylem.</span><span class="sxs-lookup"><span data-stu-id="86b93-158">An action to secure an identity or a device that were previously suspected or known to be compromised.</span></span> <span data-ttu-id="86b93-159">Bir düzeltme eylemi kimliği veya cihaza güvenli bir duruma geri yükler ve kimlik veya aygıtla ilişkili önceki risk olaylarını giderir.</span><span class="sxs-lookup"><span data-stu-id="86b93-159">A remediation action restores the identity or device to a safe state, and resolves previous risk events associated with the identity or device.</span></span>

### <a name="resolved-risk-event"></a><span data-ttu-id="86b93-160">Çözümlendi (risk olay)</span><span class="sxs-lookup"><span data-stu-id="86b93-160">Resolved (risk event)</span></span>
<span data-ttu-id="86b93-161">Kullanıcı kimlik koruması dışında bir uygun düzeltme eylemi sürdü ve risk olayı düşünülmesi gereken gösteren el ile bir kimlik koruması kullanıcı tarafından ayarlanan bir risk olay durumu kapalı.</span><span class="sxs-lookup"><span data-stu-id="86b93-161">A risk event status set manually by an Identity Protection user, indicating that the user took an appropriate remediation action outside Identity Protection, and that the risk event should be considered closed.</span></span>

### <a name="risk-event-status"></a><span data-ttu-id="86b93-162">Risk olay durumu</span><span class="sxs-lookup"><span data-stu-id="86b93-162">Risk event status</span></span>
<span data-ttu-id="86b93-163">Risk olay özelliği, olayın etkin olup olmadığını ve gösteren kapalı, kapatma nedeni.</span><span class="sxs-lookup"><span data-stu-id="86b93-163">A property of a risk event, indicating whether the event is active, and if closed, the reason for closing it.</span></span>

### <a name="risk-event-type"></a><span data-ttu-id="86b93-164">Risk olay türü</span><span class="sxs-lookup"><span data-stu-id="86b93-164">Risk event type</span></span>
<span data-ttu-id="86b93-165">Riskli olarak kabul edilmesi olaya neden anomali türünü belirten risk olayı için bir kategori.</span><span class="sxs-lookup"><span data-stu-id="86b93-165">A category for the risk event, indicating the type of anomaly that caused the event to be considered risky.</span></span>

### <a name="risk-level-risk-event"></a><span data-ttu-id="86b93-166">Risk düzeyi (risk olay)</span><span class="sxs-lookup"><span data-stu-id="86b93-166">Risk level (risk event)</span></span>
<span data-ttu-id="86b93-167">Bir gösterge (yüksek, Orta veya düşük) eylemleri öncelik kimlik koruması kullanıcılara yardımcı olmak için risk olay önem derecesi, kuruluşları riskini azaltmak için aldıkları.</span><span class="sxs-lookup"><span data-stu-id="86b93-167">An indication (High, Medium, or Low) of the severity of the risk event to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span></span> 

### <a name="risk-level-sign-in"></a><span data-ttu-id="86b93-168">Risk düzeyi (oturum açma)</span><span class="sxs-lookup"><span data-stu-id="86b93-168">Risk level (sign-in)</span></span>
<span data-ttu-id="86b93-169">Bir göstergesi (yüksek, Orta veya düşük) bir özel oturum açma için başka birinin kullanıcının kimliğini kullanmaya çalışıyor olduğunu olasılığı.</span><span class="sxs-lookup"><span data-stu-id="86b93-169">An indication (High, Medium, or Low) of the likelihood that for a specific sign-in, someone else is attempting to use the user’s identity.</span></span>

### <a name="risk-level-user-compromise"></a><span data-ttu-id="86b93-170">Risk düzeyi (kullanıcı güvenliğinin aşılması)</span><span class="sxs-lookup"><span data-stu-id="86b93-170">Risk level (user compromise)</span></span>
<span data-ttu-id="86b93-171">Bir göstergesi (yüksek, Orta veya düşük) bir kimlik aşılmış olasılığı.</span><span class="sxs-lookup"><span data-stu-id="86b93-171">An indication (High, Medium, or Low) of the likelihood that an identity has been compromised.</span></span>

### <a name="risk-level-vulnerability"></a><span data-ttu-id="86b93-172">Risk düzeyi (güvenlik açığı)</span><span class="sxs-lookup"><span data-stu-id="86b93-172">Risk level (vulnerability)</span></span>
<span data-ttu-id="86b93-173">Bir gösterge (yüksek, Orta veya düşük) eylemleri öncelik kimlik koruması kullanıcılara yardımcı olmak için güvenlik açığının önem derecesi, kuruluşları riskini azaltmak için aldıkları.</span><span class="sxs-lookup"><span data-stu-id="86b93-173">An indication (High, Medium, or Low) of the severity of the vulnerability to help Identity Protection users prioritize the actions they take to reduce the risk to their organization.</span></span>

### <a name="secure-identity"></a><span data-ttu-id="86b93-174">(Kimlik) güvenli</span><span class="sxs-lookup"><span data-stu-id="86b93-174">Secure (identity)</span></span>
<span data-ttu-id="86b93-175">Parola değiştirme veya riskli bir kimlik güvenliği aşılmamış bir duruma geri yüklemek için yeniden görüntüsünü oluşturuyor makine gibi düzeltme eylemi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="86b93-175">Take remediation action such as a password change or machine reimaging to restore a potentially compromised identity to an uncompromised state.</span></span>

### <a name="security-policy"></a><span data-ttu-id="86b93-176">Güvenlik ilkesi</span><span class="sxs-lookup"><span data-stu-id="86b93-176">Security policy</span></span>
<span data-ttu-id="86b93-177">İlke kuralları ve koşul koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="86b93-177">A collection of policy rules and condition.</span></span> <span data-ttu-id="86b93-178">Kullanıcılar, gruplar, uygulamalar, cihazları, cihaz platformları, cihaz durumları, IP aralıkları ve Auth2.0 istemci türleri gibi varlıklar için bir ilke uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="86b93-178">A policy can be applied to entities such as users, groups, apps, devices, device platforms, device states, IP ranges, and Auth2.0 client types.</span></span> <span data-ttu-id="86b93-179">Bir ilke etkinleştirildiğinde, bir kaynak için bir belirteç ilkesine dahil bir varlık verilen her değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="86b93-179">When a policy is enabled, it is evaluated whenever an entity included in the policy is issued a token for a resource.</span></span>

### <a name="sign-in-v"></a><span data-ttu-id="86b93-180">(V'de) oturum açın</span><span class="sxs-lookup"><span data-stu-id="86b93-180">Sign in (v)</span></span>
<span data-ttu-id="86b93-181">Azure Active Directory'de bir kimlik doğrulamaya.</span><span class="sxs-lookup"><span data-stu-id="86b93-181">To authenticate to an identity in Azure Active Directory.</span></span>

### <a name="sign-in-n"></a><span data-ttu-id="86b93-182">Oturum açma (n)</span><span class="sxs-lookup"><span data-stu-id="86b93-182">Sign-in (n)</span></span>
<span data-ttu-id="86b93-183">Azure Active Directory ve bu işlem yakalar olay bir kimlik doğrulama eylemi veya işlemi.</span><span class="sxs-lookup"><span data-stu-id="86b93-183">The process or action of authenticating an identity in Azure Active Directory, and the event that captures this operation.</span></span>

### <a name="sign-in-from-anonymous-ip-address"></a><span data-ttu-id="86b93-184">Anonim IP adresinden oturum açın</span><span class="sxs-lookup"><span data-stu-id="86b93-184">Sign-in from anonymous IP address</span></span>
<span data-ttu-id="86b93-185">Bir başarılı oturum açma anonim Ara sunucu IP adresi olarak tanımlanan IP adresinden sonra bir risk olayı tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="86b93-185">A risk event triggered after a successful sign-in from IP address that has been identified as an anonymous proxy IP address.</span></span>

### <a name="sign-in-from-infected-device"></a><span data-ttu-id="86b93-186">Etkilenen aygıttan oturum aç</span><span class="sxs-lookup"><span data-stu-id="86b93-186">Sign-in from infected device</span></span>
<span data-ttu-id="86b93-187">Bir oturum açma etkin bir şekilde bir bot sunucusu ile iletişim kurmak için çalıştığınız bir veya daha fazla güvenliği aşılmış cihazlara tarafından kullanılmak üzere bilinen bir IP adresi kaynaklanan harekete bir risk olayı.</span><span class="sxs-lookup"><span data-stu-id="86b93-187">A risk event triggered when a sign-in originates from an IP address which is known to be used by one or more compromised devices, which are actively attempting to communicate with a bot server.</span></span>

### <a name="sign-in-from-ip-address-with-suspicious-activity"></a><span data-ttu-id="86b93-188">Oturum IP adresinden kuşkulu etkinliği ile açma</span><span class="sxs-lookup"><span data-stu-id="86b93-188">Sign-in from IP address with suspicious activity</span></span>
<span data-ttu-id="86b93-189">Birden çok kullanıcı hesapları arasında kısa bir süre boyunca çok sayıda başarısız oturum açma denemesi bir başarılı oturum açma gelen bir IP adresi sonra risk olay tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="86b93-189">A risk event triggered after a successful sign-in from an IP address with a high number of failed login attempts across multiple user accounts over a short period of time.</span></span>

### <a name="sign-in-from-unfamiliar-location"></a><span data-ttu-id="86b93-190">Tanınmayan bir konumdan oturum aç</span><span class="sxs-lookup"><span data-stu-id="86b93-190">Sign-in from unfamiliar location</span></span>
<span data-ttu-id="86b93-191">Kullanıcı başarıyla yeni bir konumdan (IP, enlem/boylam ve ASN) oturum açtığında tetiklenen bir risk olayı.</span><span class="sxs-lookup"><span data-stu-id="86b93-191">A risk event triggered when a user successfully signs in from a new location (IP, Latitude/Longitude and ASN).</span></span>

### <a name="sign-in-risk"></a><span data-ttu-id="86b93-192">Oturum açma riski</span><span class="sxs-lookup"><span data-stu-id="86b93-192">Sign-in risk</span></span>
<span data-ttu-id="86b93-193">Risk bkz düzeyi (oturum açma)</span><span class="sxs-lookup"><span data-stu-id="86b93-193">See Risk level (sign-in)</span></span>

### <a name="sign-in-risk-policy"></a><span data-ttu-id="86b93-194">Oturum açma riski İlkesi</span><span class="sxs-lookup"><span data-stu-id="86b93-194">Sign-in risk policy</span></span>
<span data-ttu-id="86b93-195">Bir özel oturum açma riski değerlendirir ve önceden tanımlanmış koşullara ve kurallarına göre Azaltıcı Etkenler geçerli koşullu erişim ilkesi.</span><span class="sxs-lookup"><span data-stu-id="86b93-195">A conditional access policy that evaluates the risk to a specific sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="user-compromise-risk"></a><span data-ttu-id="86b93-196">Kullanıcı güvenlik aşılması riski</span><span class="sxs-lookup"><span data-stu-id="86b93-196">User compromise risk</span></span>
<span data-ttu-id="86b93-197">Risk bakın (kullanıcı güvenliğinin aşılması) düzeyi</span><span class="sxs-lookup"><span data-stu-id="86b93-197">See Risk level (user compromise)</span></span>

### <a name="user-risk"></a><span data-ttu-id="86b93-198">Kullanıcı riski</span><span class="sxs-lookup"><span data-stu-id="86b93-198">User risk</span></span>
<span data-ttu-id="86b93-199">Risk bakın (kullanıcı güvenliğinin aşılması) düzeyi.</span><span class="sxs-lookup"><span data-stu-id="86b93-199">See Risk level (user compromise).</span></span>

### <a name="user-risk-policy"></a><span data-ttu-id="86b93-200">Kullanıcı risk İlkesi</span><span class="sxs-lookup"><span data-stu-id="86b93-200">User risk policy</span></span>
<span data-ttu-id="86b93-201">Oturum açma göz önünde bulundurur ve önceden tanımlanmış koşullara ve kurallarına göre Azaltıcı geçerlidir koşullu erişim ilkesi.</span><span class="sxs-lookup"><span data-stu-id="86b93-201">A conditional access policy that considers the sign-in and applies mitigations based on predefined conditions and rules.</span></span>

### <a name="users-flagged-for-risk"></a><span data-ttu-id="86b93-202">Riskli oldukları belirlenen kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="86b93-202">Users flagged for risk</span></span>
<span data-ttu-id="86b93-203">Etkin ya da düzeltilen risk olaylarına sahip kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="86b93-203">Users that have risk events which are either active or remediated</span></span>

### <a name="vulnerability"></a><span data-ttu-id="86b93-204">Güvenlik Açığı</span><span class="sxs-lookup"><span data-stu-id="86b93-204">Vulnerability</span></span>
<span data-ttu-id="86b93-205">Bir yapılandırma veya Azure Active Directory'de dizin açıklarına maruz kalabilir kılan koşul veya tehditleri.</span><span class="sxs-lookup"><span data-stu-id="86b93-205">A configuration or condition in Azure Active Directory which makes the directory susceptible to exploits or threats.</span></span>

## <a name="see-also"></a><span data-ttu-id="86b93-206">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="86b93-206">See also</span></span>
* [<span data-ttu-id="86b93-207">Azure Active Directory kimlik koruması</span><span class="sxs-lookup"><span data-stu-id="86b93-207">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

