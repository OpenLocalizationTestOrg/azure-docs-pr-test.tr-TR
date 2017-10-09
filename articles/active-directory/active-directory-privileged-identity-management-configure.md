---
title: Azure AD Privileged Identity Management aaaConfigure | Microsoft Docs
description: "Azure AD Privileged Identity Management nedir açıklayan bir konu ve nasıl toouse PIM tooimprove bulut güvenliğinizi."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: c548ed2e-06e3-4eaf-a63d-0f02ee72da25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: dbe49fe4a0f6e5b46ed5a17fc7e8dcdacafe3846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a><span data-ttu-id="902a2-103">Azure AD Privileged Identity Management nedir?</span><span class="sxs-lookup"><span data-stu-id="902a2-103">What is Azure AD Privileged Identity Management?</span></span>
<span data-ttu-id="902a2-104">Azure Active Directory (AD) Privileged Identity Management sayesinde kuruluşunuz içindeki erişimi yönetebilir, denetleyebilir ve izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="902a2-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="902a2-105">Bu erişim tooresources Azure AD'de ve Office 365 veya Microsoft Intune gibi diğer Microsoft online services içerir.</span><span class="sxs-lookup"><span data-stu-id="902a2-105">This includes access tooresources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

> [!NOTE]
> <span data-ttu-id="902a2-106">Privileged Identity Management yöneticilerinizi hello Premium P2 edition Azure Active Directory ile lisans kullanılabilir tooyour tüm kuruluş durumdur.</span><span class="sxs-lookup"><span data-stu-id="902a2-106">Privileged Identity Management is available tooyour entire organization when you license your Administrators with hello Premium P2 edition of Azure Active Directory.</span></span> <span data-ttu-id="902a2-107">Daha fazla bilgi için bkz. [Azure Active Directory sürümleri](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="902a2-107">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

<span data-ttu-id="902a2-108">Çünkü, bu erişim alma kötü niyetli bir kullanıcının hello olasılığını azaltır kuruluşlar toominimize hello toosecure bilgilere erişmek veya kaynaklarını olan kişiler sayısı istiyor.</span><span class="sxs-lookup"><span data-stu-id="902a2-108">Organizations want toominimize hello number of people who have access toosecure information or resources, because that reduces hello chance of a malicious user getting that access.</span></span> <span data-ttu-id="902a2-109">Ancak, kullanıcılar yine de Azure, Office 365 ya da SaaS uygulamalarında ayrıcalıklı işlemleri çıkışı toocarry gerekir.</span><span class="sxs-lookup"><span data-stu-id="902a2-109">However, users still need toocarry out privileged operations in Azure, Office 365, or SaaS apps.</span></span> <span data-ttu-id="902a2-110">Kuruluşlar, yönetici ayrıcalıklarını bu kullanıcıların ne yaptıklarını izleme olmadan, Azure AD'de kullanıcılar ayrıcalıklı erişim verin.</span><span class="sxs-lookup"><span data-stu-id="902a2-110">Organizations give users privileged access in Azure AD without monitoring what those users are doing with their admin privileges.</span></span> <span data-ttu-id="902a2-111">Azure AD Privileged Identity Management tooresolve bu riski yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="902a2-111">Azure AD Privileged Identity Management helps tooresolve this risk.</span></span>  

<span data-ttu-id="902a2-112">Azure AD Privileged Identity Management yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="902a2-112">Azure AD Privileged Identity Management helps you:</span></span>  

* <span data-ttu-id="902a2-113">Hangi kullanıcıların Azure AD yöneticilerdir bakın</span><span class="sxs-lookup"><span data-stu-id="902a2-113">See which users are Azure AD administrators</span></span>
* <span data-ttu-id="902a2-114">İsteğe bağlı, "Office 365 ve Intune yönetim erişimi tooMicrosoft çevrimiçi hizmetler gibi tam zamanında" etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="902a2-114">Enable on-demand, "just in time" administrative access tooMicrosoft Online Services like Office 365 and Intune</span></span>
* <span data-ttu-id="902a2-115">Yönetici erişim geçmişine ve değişiklikler hakkında raporlar yönetici atamaları alma</span><span class="sxs-lookup"><span data-stu-id="902a2-115">Get reports about administrator access history and changes in administrator assignments</span></span>
* <span data-ttu-id="902a2-116">Erişim tooa ayrıcalıklı rol hakkında uyarı alın</span><span class="sxs-lookup"><span data-stu-id="902a2-116">Get alerts about access tooa privileged role</span></span>
* <span data-ttu-id="902a2-117">Onay tooactivate (Önizleme) gerektirir</span><span class="sxs-lookup"><span data-stu-id="902a2-117">Require approval tooactivate (Preview)</span></span>

<span data-ttu-id="902a2-118">Azure AD Privileged Identity Management (ancak bunlarla sınırlı değil) hello yerleşik Azure AD kuruluş rolleri yönetebilir:</span><span class="sxs-lookup"><span data-stu-id="902a2-118">Azure AD Privileged Identity Management can manage hello built-in Azure AD organizational roles, including (but not limited to):</span></span>  

* <span data-ttu-id="902a2-119">Genel yönetici</span><span class="sxs-lookup"><span data-stu-id="902a2-119">Global Administrator</span></span>
* <span data-ttu-id="902a2-120">Faturalama Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="902a2-120">Billing Administrator</span></span>
* <span data-ttu-id="902a2-121">Hizmet Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="902a2-121">Service Administrator</span></span>  
* <span data-ttu-id="902a2-122">Kullanıcı Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="902a2-122">User Administrator</span></span>
* <span data-ttu-id="902a2-123">Parola Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="902a2-123">Password Administrator</span></span>

## <a name="just-in-time-administrator-access"></a><span data-ttu-id="902a2-124">Yalnızca süresi yönetici erişimi</span><span class="sxs-lookup"><span data-stu-id="902a2-124">Just in time administrator access</span></span>
<span data-ttu-id="902a2-125">Tarihsel olarak, bir kullanıcı tooan Yönetici rolü hello Klasik Azure portalı üzerinden veya Windows PowerShell atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="902a2-125">Historically, you could assign a user tooan admin role through hello Azure classic portal or Windows PowerShell.</span></span> <span data-ttu-id="902a2-126">Sonuç olarak, bu kullanıcının hale bir **kalıcı yönetici**, atanan hello rolündeki her zaman etkin.</span><span class="sxs-lookup"><span data-stu-id="902a2-126">As a result, that user becomes a **permanent admin**, always active in hello assigned role.</span></span> <span data-ttu-id="902a2-127">Azure AD Privileged Identity Management hello kavramını sunmaktadır bir **uygun yönetici**. Uygun admins şimdi yapıp ancak her gün ayrıcalıklı erişimi olması gereken kullanıcılar olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="902a2-127">Azure AD Privileged Identity Management introduces hello concept of an **eligible admin**. Eligible admins should be users that need privileged access now and then, but not every day.</span></span> <span data-ttu-id="902a2-128">bir etkinleştirme işlemini tamamlamak ve önceden belirlenen bir süre için etkin bir yönetim hale hello kullanıcının erişim, gerektiği kadar hello rolü etkin değil.</span><span class="sxs-lookup"><span data-stu-id="902a2-128">hello role is inactive until hello user needs access, then they complete an activation process and become an active admin for a predetermined amount of time.</span></span>

## <a name="enable-privileged-identity-management-for-your-directory"></a><span data-ttu-id="902a2-129">Privileged Identity Management dizininiz için etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="902a2-129">Enable Privileged Identity Management for your directory</span></span>
<span data-ttu-id="902a2-130">Azure AD Privileged Identity Management hello kullanmaya başlayabilmeniz için [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="902a2-130">You can start using Azure AD Privileged Identity Management in hello [Azure portal](https://portal.azure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="902a2-131">Bir kurumsal hesap ile genel yönetici olmanız gerekir (örneğin, @yourdomain.com), bir Microsoft hesabı (örneğin, @outlook.com), bir dizin için Azure AD Privileged Identity Management tooenable.</span><span class="sxs-lookup"><span data-stu-id="902a2-131">You must be a global administrator with an organizational account (for example, @yourdomain.com), not a Microsoft account (for example, @outlook.com), tooenable Azure AD Privileged Identity Management for a directory.</span></span>

1. <span data-ttu-id="902a2-132">İçinde toohello oturum [Azure portal](https://portal.azure.com/) dizininizin genel Yöneticisi olarak.</span><span class="sxs-lookup"><span data-stu-id="902a2-132">Sign in toohello [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span></span>
2. <span data-ttu-id="902a2-133">Kuruluşunuz birden fazla dizine sahipse, kullanıcı adınızı hello sağ üst köşesinde hello Azure portalı içinde seçin.</span><span class="sxs-lookup"><span data-stu-id="902a2-133">If your organization has more than one directory, select your username in hello upper right-hand corner of hello Azure portal.</span></span> <span data-ttu-id="902a2-134">Burada, Azure AD Privileged Identity Management kullanacağınız hello dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="902a2-134">Select hello directory where you will use Azure AD Privileged Identity Management.</span></span>
3. <span data-ttu-id="902a2-135">Seçin **daha fazla hizmet** ve hello filtre textbox toosearch **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="902a2-135">Select **More services** and use hello Filter textbox toosearch for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="902a2-136">Denetleme **PIN toodashboard** ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="902a2-136">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="902a2-137">Merhaba Privileged Identity Management uygulaması açılır.</span><span class="sxs-lookup"><span data-stu-id="902a2-137">hello Privileged Identity Management application opens.</span></span>

<span data-ttu-id="902a2-138">Dizininizde Azure AD Privileged Identity Management ilk kişinin toouse olduğunuz hello varsa, ardından hello [Güvenlik Sihirbazı](active-directory-privileged-identity-management-security-wizard.md) hello ilk atama deneyimi boyunca size yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="902a2-138">If you're hello first person toouse Azure AD Privileged Identity Management in your directory, then hello [security wizard](active-directory-privileged-identity-management-security-wizard.md) walks you through hello initial assignment experience.</span></span> <span data-ttu-id="902a2-139">Bundan sonra otomatik olarak hale hello ilk **Güvenlik Yöneticisi** ve **ayrıcalıklı Rol Yöneticisi** hello dizininin.</span><span class="sxs-lookup"><span data-stu-id="902a2-139">After that you automatically become hello first **Security administrator** and **Privileged role administrator** of hello directory.</span></span>

<span data-ttu-id="902a2-140">Yalnızca ayrıcalıklı Rol Yöneticisi, diğer yöneticiler için erişimi yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="902a2-140">Only a privileged role administrator can manage access for other administrators.</span></span> <span data-ttu-id="902a2-141">Yapabilecekleriniz [PIM diğer kullanıcıların hello özelliği toomanage vermek](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="902a2-141">You can [give other users hello ability toomanage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="privileged-identity-management-admin-dashboard"></a><span data-ttu-id="902a2-142">Privileged Identity Management Yönetim Panosu</span><span class="sxs-lookup"><span data-stu-id="902a2-142">Privileged Identity Management admin dashboard</span></span>
<span data-ttu-id="902a2-143">Azure AD Privileged Identity Manager gibi önemli bilgiler sağlayan bir Yönetim Panosu sağlar:</span><span class="sxs-lookup"><span data-stu-id="902a2-143">Azure AD Privileged Identity Manager provides an admin dashboard that gives you important information such as:</span></span>

* <span data-ttu-id="902a2-144">Fırsatları tooimprove güvenlik noktası uyarıları</span><span class="sxs-lookup"><span data-stu-id="902a2-144">Alerts that point out opportunities tooimprove security</span></span>
* <span data-ttu-id="902a2-145">Merhaba tooeach ayrıcalıklı role atanmış kullanıcıların sayısını</span><span class="sxs-lookup"><span data-stu-id="902a2-145">hello number of users who are assigned tooeach privileged role</span></span>  
* <span data-ttu-id="902a2-146">uygun ve kalıcı admins Hello sayısı</span><span class="sxs-lookup"><span data-stu-id="902a2-146">hello number of eligible and permanent admins</span></span>
* <span data-ttu-id="902a2-147">Ayrıcalıklı rolü etkinleştirme dizininizde grafiği</span><span class="sxs-lookup"><span data-stu-id="902a2-147">A graph of privileged role activations in your directory</span></span>

![PIM Pano - ekran görüntüsü][2]

## <a name="privileged-role-management"></a><span data-ttu-id="902a2-149">Ayrıcalıklı rol yönetimi</span><span class="sxs-lookup"><span data-stu-id="902a2-149">Privileged role management</span></span>
<span data-ttu-id="902a2-150">Azure AD Privileged Identity Management'ı ekleyerek veya kaldırarak kalıcı veya uygun Yöneticiler tooeach rolünün hello Yöneticiler yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="902a2-150">With Azure AD Privileged Identity Management, you can manage hello administrators by adding or removing permanent or eligible administrators tooeach role.</span></span>

![PIM Ekle/Kaldır yöneticileri - ekran görüntüsü][3]

## <a name="configure-hello-role-activation-settings"></a><span data-ttu-id="902a2-152">Merhaba rol etkinleştirme ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="902a2-152">Configure hello role activation settings</span></span>
<span data-ttu-id="902a2-153">Hello kullanarak [rol ayarlarını](active-directory-privileged-identity-management-how-to-change-default-settings.md) hello uygun rol etkinleştirme özellikleri dahil olmak üzere yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="902a2-153">Using hello [role settings](active-directory-privileged-identity-management-how-to-change-default-settings.md) you can configure hello eligible role activation properties including:</span></span>

* <span data-ttu-id="902a2-154">Merhaba rol etkinleştirme süresi başlangıç süresi</span><span class="sxs-lookup"><span data-stu-id="902a2-154">hello duration of hello role activation period</span></span>
* <span data-ttu-id="902a2-155">Merhaba rol etkinleştirme bildirimi</span><span class="sxs-lookup"><span data-stu-id="902a2-155">hello role activation notification</span></span>
* <span data-ttu-id="902a2-156">Merhaba bilgi kullanıcı tooprovide hello rol etkinleştirme işlemi sırasında gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="902a2-156">hello information a user needs tooprovide during hello role activation process</span></span>
* <span data-ttu-id="902a2-157">Hizmet bileti veya olay numarası</span><span class="sxs-lookup"><span data-stu-id="902a2-157">Service ticket or incident number</span></span>
* [<span data-ttu-id="902a2-158">Onay iş akışı gereksinimleri - Önizleme</span><span class="sxs-lookup"><span data-stu-id="902a2-158">Approval workflow requirements - Preview</span></span>](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![PIM ayarları - yönetici etkinleştirme - ekran görüntüsü][4]

<span data-ttu-id="902a2-160">Merhaba görüntüde için hello düğmeleri Not **çok faktörlü kimlik doğrulaması** devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="902a2-160">Note that in hello image, hello buttons for **Multi-Factor Authentication** are disabled.</span></span> <span data-ttu-id="902a2-161">Belirli, yüksek ayrıcalıklı rolleri, size daha fazla koruma için MFA gerekir.</span><span class="sxs-lookup"><span data-stu-id="902a2-161">For certain, highly privileged roles, we require MFA for heightened protection.</span></span>

## <a name="role-activation"></a><span data-ttu-id="902a2-162">Rol etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="902a2-162">Role activation</span></span>
<span data-ttu-id="902a2-163">çok[bir rolü etkinleştirmesi](active-directory-privileged-identity-management-how-to-activate-role.md), bir zaman sınırlı "etkinleştirme" Merhaba rolü için uygun yönetici ister.</span><span class="sxs-lookup"><span data-stu-id="902a2-163">too[activate a role](active-directory-privileged-identity-management-how-to-activate-role.md), an eligible admin requests a time-bound "activation" for hello role.</span></span> <span data-ttu-id="902a2-164">Merhaba etkinleştirme hello kullanarak istenebilir **my rolünü etkinleştirmek** Azure AD Privileged Identity Management seçeneği.</span><span class="sxs-lookup"><span data-stu-id="902a2-164">hello activation can be requested using hello **Activate my role** option in Azure AD Privileged Identity Management.</span></span>

<span data-ttu-id="902a2-165">Bir rolü tooactivate isteyen bir yönetici tooinitialize hello Azure portalında Azure AD Privileged Identity Management gerekir.</span><span class="sxs-lookup"><span data-stu-id="902a2-165">An admin who wants tooactivate a role needs tooinitialize Azure AD Privileged Identity Management in hello Azure portal.</span></span>

<span data-ttu-id="902a2-166">Rol etkinleştirme özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="902a2-166">Role activation is customizable.</span></span> <span data-ttu-id="902a2-167">Merhaba PIM ayarlarında hello etkinleştirme ve hangi bilgi hello Yöneticisi tooprovide tooactivate hello rolüne ihtiyacı hello uzunluğu belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="902a2-167">In hello PIM settings, you can determine hello length of hello activation and what information hello admin needs tooprovide tooactivate hello role.</span></span>

![PIM yönetici isteği rol etkinleştirme - ekran görüntüsü][5]

## <a name="review-role-activity"></a><span data-ttu-id="902a2-169">Gözden geçirme rol etkinliği</span><span class="sxs-lookup"><span data-stu-id="902a2-169">Review role activity</span></span>
<span data-ttu-id="902a2-170">İki yolu tootrack vardır, çalışanlarınızın ve admins nasıl kullandığını ayrıcalıklı rolleri.</span><span class="sxs-lookup"><span data-stu-id="902a2-170">There are two ways tootrack how your employees and admins are using privileged roles.</span></span> <span data-ttu-id="902a2-171">Merhaba ilk seçenek kullanıyor [Directory rolleri denetim geçmişi](active-directory-privileged-identity-management-how-to-use-audit-log.md).</span><span class="sxs-lookup"><span data-stu-id="902a2-171">hello first option is using [Directory Roles audit history](active-directory-privileged-identity-management-how-to-use-audit-log.md).</span></span> <span data-ttu-id="902a2-172">Merhaba denetim geçmişi Değişiklikleri İzle ayrıcalıklı rol atamaları ve rol etkinleştirme geçmişini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="902a2-172">hello audit history logs track changes in privileged role assignments and role activation history.</span></span>

![PIM etkinleştirme geçmişi - ekran görüntüsü][6]

<span data-ttu-id="902a2-174">Merhaba ikinci tooset normal yedekleme seçenektir [erişim incelemeler](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="902a2-174">hello second option is tooset up regular [access reviews](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="902a2-175">Bu erişim incelemeler tarafından gerçekleştirilen ve İnceleme (örneğin, bir takım Yöneticisi) atanmış veya hello çalışanlar kendilerini gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="902a2-175">These access reviews can be performed by and assigned reviewer (like a team manager) or hello employees can review themselves.</span></span> <span data-ttu-id="902a2-176">Kimin hala erişim gerektirir ve artık kilitlenmiyor hello en iyi şekilde toomonitor budur.</span><span class="sxs-lookup"><span data-stu-id="902a2-176">This is hello best way toomonitor who still requires access, and who no longer does.</span></span>

## <a name="azure-ad-pim-at-subscription-expiration"></a><span data-ttu-id="902a2-177">Abonelik sona erme adresindeki Azure AD PIM</span><span class="sxs-lookup"><span data-stu-id="902a2-177">Azure AD PIM at subscription expiration</span></span>
<span data-ttu-id="902a2-178">Önceki tooreaching kullanılabilirlik Azure AD PIM önizlemede oldu ve lisans vardı genel bir kiracı toopreview Azure AD PIM denetler.</span><span class="sxs-lookup"><span data-stu-id="902a2-178">Prior tooreaching general availability Azure AD PIM was in preview and there were no license checks for a tenant toopreview Azure AD PIM.</span></span>  <span data-ttu-id="902a2-179">Azure AD PIM genel kullanılabilirlik ulaştı, deneme aboneliği veya Ücretli lisans PIM kullanarak hello Kiracı toocontinue toohello yöneticileri atanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="902a2-179">Now that Azure AD PIM has reached general availability, trial or paid licenses must be assigned toohello administrators of hello tenant toocontinue using PIM.</span></span>  <span data-ttu-id="902a2-180">Kuruluşunuz Azure AD Premium P2 satın değil veya deneme süresi, genellikle tüm hello Azure AD PIM özellikler artık kiracınızda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="902a2-180">If your organization does not purchase Azure AD Premium P2 or your trial expires, mostly all of hello Azure AD PIM features will no longer be available in your tenant.</span></span>  <span data-ttu-id="902a2-181">Daha fazla bilgiyi hello içinde [Azure AD PIM abonelik gereksinimleri](./privileged-identity-management/subscription-requirements.md)</span><span class="sxs-lookup"><span data-stu-id="902a2-181">You can read more in hello [Azure AD PIM subscription requirements](./privileged-identity-management/subscription-requirements.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="902a2-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="902a2-182">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
