---
title: "Azure Active Directory'de koşullu erişim için aaaBest uygulamaları | Microsoft Docs"
description: "Bilmeniz gerekenler ve koşullu erişim ilkeleri yapılandırırken bunun kaçınmalısınız nedir hakkında bilgi edinin."
services: active-directory
keywords: "koşullu erişim tooapps, Azure AD ile koşullu erişim toocompany kaynaklarına, koşullu erişim ilkeleri güvenli erişim"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="52726-104">Azure Active Directory'de koşullu erişim için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="52726-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="52726-105">Bu konu, bilmeniz gerekenler ve koşullu erişim ilkeleri yapılandırırken bunun kaçınmalısınız nedir hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="52726-105">This topic provides you with information about things you should know and what it is you should avoid doing when configuring conditional access policies.</span></span> <span data-ttu-id="52726-106">Bu konu okumadan önce hello kavramları öğrenmeniz ve hello terminolojisi özetlenen [Azure Active Directory'de koşullu erişim](active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="52726-106">Before reading this topic, you should familiarize yourself with hello concepts and hello terminology outlined in [Conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal.md)</span></span>

## <a name="what-you-should-know"></a><span data-ttu-id="52726-107">Bilmeniz gerekenler</span><span class="sxs-lookup"><span data-stu-id="52726-107">What you should know</span></span>

### <a name="whats-required-toomake-a-policy-work"></a><span data-ttu-id="52726-108">Toomake bir ilke iş ne gereklidir?</span><span class="sxs-lookup"><span data-stu-id="52726-108">What’s required toomake a policy work?</span></span>

<span data-ttu-id="52726-109">Yeni bir ilke oluşturduğunuzda, hiçbir kullanıcıları, grupları, uygulamalar veya seçili erişim denetimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="52726-109">When you create a new policy, there are no users, groups, apps or access controls selected.</span></span>

![Bulut uygulamaları](./media/active-directory-conditional-access-best-practices/02.png)


<span data-ttu-id="52726-111">ilkeniz toomake çalışma, hello aşağıdakileri yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="52726-111">toomake your policy work, you must configure hello following:</span></span>


|<span data-ttu-id="52726-112">Ne</span><span class="sxs-lookup"><span data-stu-id="52726-112">What</span></span>           | <span data-ttu-id="52726-113">Nasıl</span><span class="sxs-lookup"><span data-stu-id="52726-113">How</span></span>                                  | <span data-ttu-id="52726-114">Neden</span><span class="sxs-lookup"><span data-stu-id="52726-114">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="52726-115">**Bulut uygulamaları**</span><span class="sxs-lookup"><span data-stu-id="52726-115">**Cloud apps**</span></span> |<span data-ttu-id="52726-116">Bir veya daha fazla uygulama tooselect gerekir.</span><span class="sxs-lookup"><span data-stu-id="52726-116">You need tooselect one or more apps.</span></span>  | <span data-ttu-id="52726-117">Merhaba koşullu erişim ilkesi hedefidir tooenable toofine ayarlama nasıl yetkili kullanıcılar, uygulamalara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="52726-117">hello goal of a conditional access policy is tooenable you toofine-tune how authorized users can access your apps.</span></span>|
| <span data-ttu-id="52726-118">**Kullanıcılar ve gruplar**</span><span class="sxs-lookup"><span data-stu-id="52726-118">**Users and groups**</span></span> | <span data-ttu-id="52726-119">En az bir tooselect gereken kullanıcı veya grup yetkili tooaccess hello bulut uygulamalarını seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="52726-119">You need tooselect at least one user or group that is authorized tooaccess hello cloud apps you have selected.</span></span> | <span data-ttu-id="52726-120">Hiçbir zaman yok kullanıcılar ve gruplar atanan bir koşullu erişim ilkesi tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="52726-120">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="52726-121">**Erişim denetimleri**</span><span class="sxs-lookup"><span data-stu-id="52726-121">**Access controls**</span></span> | <span data-ttu-id="52726-122">En az bir tooselect gereken erişim denetimi.</span><span class="sxs-lookup"><span data-stu-id="52726-122">You need tooselect at least one access control.</span></span> | <span data-ttu-id="52726-123">Koşullarınızı sağlanırsa, ilke işlemci hangi toodo tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="52726-123">Your policy processor needs tooknow what toodo if your conditions are satisfied.</span></span>|


<span data-ttu-id="52726-124">Toplama toothese temel gereksinimleri, çoğu durumda, bir koşul yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="52726-124">In addition toothese basic requirements, in many cases, you should also configure a condition.</span></span> <span data-ttu-id="52726-125">Bir ilke yapılandırılmış bir koşulu de çalışması sırasında erişim tooyour uygulamaları ince ayar yapmak için hello yönlendirmeli faktörü koşullardır.</span><span class="sxs-lookup"><span data-stu-id="52726-125">While a policy would also work without a configured condition, conditions are hello driving factor for fine-tuning access tooyour apps.</span></span>


![Bulut uygulamaları](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="52726-127">Atamaları nasıl değerlendirildiği?</span><span class="sxs-lookup"><span data-stu-id="52726-127">How are assignments evaluated?</span></span>

<span data-ttu-id="52726-128">Tüm atamaları mantıksal olarak olan **and işleciyle**.</span><span class="sxs-lookup"><span data-stu-id="52726-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="52726-129">Yapılandırılmış, birden fazla atama tootrigger bir ilke varsa, tüm atamaları sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="52726-129">If you have more than one assignment configured, tootrigger a policy, all assignments must be satisfied.</span></span>  

<span data-ttu-id="52726-130">Tooconfigure, kuruluşunuzun ağ dışından yapılan tooall bağlantılara uygulanır bir konum koşul gerekiyorsa, bunu gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="52726-130">If you need tooconfigure a location condition that applies tooall connections made from outside your organization's network, you can accomplish this by:</span></span>

- <span data-ttu-id="52726-131">Dahil olmak üzere **tüm konumları**</span><span class="sxs-lookup"><span data-stu-id="52726-131">Including **All locations**</span></span>
- <span data-ttu-id="52726-132">Hariç **tüm güvenilen IP'leri**</span><span class="sxs-lookup"><span data-stu-id="52726-132">Excluding **All trusted IPs**</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="52726-133">İlkeleri'nde hello Klasik Azure portalı ve Azure portalı yapılandırılmış varsa ne olur?</span><span class="sxs-lookup"><span data-stu-id="52726-133">What happens if you have policies in hello Azure classic portal and Azure portal configured?</span></span>  
<span data-ttu-id="52726-134">Her iki ilkeleri Azure Active Directory tarafından uygulanır ve yalnızca tüm gereksinimleri karşılandığında hello kullanıcı erişim alır.</span><span class="sxs-lookup"><span data-stu-id="52726-134">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a><span data-ttu-id="52726-135">Merhaba Intune Silverlight portal ilkelerinde ve hello Azure Portal varsa ne olur?</span><span class="sxs-lookup"><span data-stu-id="52726-135">What happens if you have policies in hello Intune Silverlight portal and hello Azure Portal?</span></span>
<span data-ttu-id="52726-136">Her iki ilkeleri Azure Active Directory tarafından uygulanır ve yalnızca tüm gereksinimleri karşılandığında hello kullanıcı erişim alır.</span><span class="sxs-lookup"><span data-stu-id="52726-136">Both policies are enforced by Azure Active Directory and hello user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a><span data-ttu-id="52726-137">Aynı kullanıcı tarafından yapılandırılmış hello için birden çok ilke varsa ne olur?</span><span class="sxs-lookup"><span data-stu-id="52726-137">What happens if I have multiple policies for hello same user configured?</span></span>  
<span data-ttu-id="52726-138">Her oturum açma için Azure Active Directory tüm ilkeler değerlendirir ve verilen toohello kullanıcıya erişim önce tüm gereksinimlerin karşılandığını sağlar.</span><span class="sxs-lookup"><span data-stu-id="52726-138">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access toohello user.</span></span>


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="52726-139">Koşullu erişim, Exchange ActiveSync ile çalışır mı?</span><span class="sxs-lookup"><span data-stu-id="52726-139">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="52726-140">Evet, Exchange ActiveSync bir koşullu erişim ilkesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52726-140">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>


## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="52726-141">Bunu yaptığınızda kaçınmanız gerekir</span><span class="sxs-lookup"><span data-stu-id="52726-141">What you should avoid doing</span></span>

<span data-ttu-id="52726-142">Merhaba koşullu erişim framework harika yapılandırma esnekliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="52726-142">hello conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="52726-143">Ancak, büyük esneklik ayrıca her yapılandırma İlkesi önceki tooreleasing dikkatle gözden geçirmelidir anlamına gelir, tooavoid istenmeyen sonuçları.</span><span class="sxs-lookup"><span data-stu-id="52726-143">However, great flexibility  also means that you should carefully review each configuration policy prior tooreleasing it tooavoid undesirable results.</span></span> <span data-ttu-id="52726-144">Bu bağlamda tam kümeleri gibi etkileyen özel dikkat tooassignments ödeme **tüm kullanıcıları / grupları / bulut uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="52726-144">In this context, you should pay special attention tooassignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="52726-145">Ortamınızda yapılandırmaları aşağıdaki hello kaçınmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="52726-145">In your environment, you should avoid hello following configurations:</span></span>


<span data-ttu-id="52726-146">**Tüm kullanıcılar için tüm bulut uygulamalarından:**</span><span class="sxs-lookup"><span data-stu-id="52726-146">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="52726-147">**Erişimi engelleme** -bu yapılandırmayı kesinlikle iyi bir fikir değil, tüm kuruluş engeller.</span><span class="sxs-lookup"><span data-stu-id="52726-147">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="52726-148">**Uyumlu aygıt gerektiren** - kullanıcılar için yok sahip kayıtlı cihazlarını henüz, bu ilke erişim toohello Intune portalı dahil olmak üzere tüm erişimini engeller.</span><span class="sxs-lookup"><span data-stu-id="52726-148">**Require compliant device** - For users that don't have enrolled their devices yet, this policy blocks all access including access toohello Intune portal.</span></span> <span data-ttu-id="52726-149">Kayıtlı bir cihazın olmadan bir yöneticiyseniz Bu ilke hello Azure portal toochange hello İlkesi'ne geri alamazsınız engeller.</span><span class="sxs-lookup"><span data-stu-id="52726-149">If you are an administrator without an enrolled device, this policy blocks you from getting back into hello Azure portal toochange hello policy.</span></span>

- <span data-ttu-id="52726-150">**Etki alanına katılmayı gerektirecek** - Bu ilke bloğu erişimi de hello olası tooblock erişim tüm kullanıcılar için kuruluşunuzdaki bir etki alanına katılmış cihazınız henüz yoksa.</span><span class="sxs-lookup"><span data-stu-id="52726-150">**Require domain join** - This policy block access has also hello potential tooblock access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="52726-151">**Tüm kullanıcılar, tüm bulut uygulamaları, tüm cihaz platformları için:**</span><span class="sxs-lookup"><span data-stu-id="52726-151">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="52726-152">**Erişimi engelleme** -bu yapılandırmayı kesinlikle iyi bir fikir değil, tüm kuruluş engeller.</span><span class="sxs-lookup"><span data-stu-id="52726-152">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="common-scenarios"></a><span data-ttu-id="52726-153">Genel senaryolar</span><span class="sxs-lookup"><span data-stu-id="52726-153">Common scenarios</span></span>

### <a name="requiring-multi-factor-authentication-for-apps"></a><span data-ttu-id="52726-154">Çok faktörlü kimlik doğrulaması gerektiren uygulamalar için</span><span class="sxs-lookup"><span data-stu-id="52726-154">Requiring multi-factor authentication for apps</span></span>

<span data-ttu-id="52726-155">Çoğu ortam daha yüksek düzeyde koruma hello daha başkalarının gerektiren uygulamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="52726-155">Many environments have apps requiring a higher level of protection than hello others.</span></span>
<span data-ttu-id="52726-156">Bu, örneğin, hello erişim toosensitive verilere sahip uygulamalar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="52726-156">This is, for example, hello case for apps that have access toosensitive data.</span></span>
<span data-ttu-id="52726-157">Koruma toothese uygulamaların başka bir katmana tooadd istiyorsanız, kullanıcılar bu uygulamaları erişirken, çok faktörlü kimlik doğrulaması gerektiren bir koşullu erişim ilkesi yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52726-157">If you want tooadd another layer of protection toothese apps, you can configure a conditional access policy that requires multi-factor authentication when users are accessing these apps.</span></span>


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a><span data-ttu-id="52726-158">Güvenilir olmayan ağlara erişim için çok faktörlü kimlik doğrulama gerektirme</span><span class="sxs-lookup"><span data-stu-id="52726-158">Requiring multi-factor authentication for access from networks that are not trusted</span></span>

<span data-ttu-id="52726-159">Bu senaryo benzer toohello önceki senaryoda nedeni, çok faktörlü kimlik doğrulama gereksinimini ekler.</span><span class="sxs-lookup"><span data-stu-id="52726-159">This scenario is similar toohello previous scenario because it adds a requirement for multi-factor authentication.</span></span>
<span data-ttu-id="52726-160">Ancak, hello temel fark hello bu gereksinim için bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="52726-160">However, hello main difference is hello condition for this requirement.</span></span>  
<span data-ttu-id="52726-161">Merhaba odak hello önceki senaryonun uygulamalara erişim toosensitve verilerle çalışırken, bu senaryonun hello odak güvenilen konumlarının noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="52726-161">While hello focus of hello previous scenario was on apps with access toosensitve data, hello focus of this scenario is on trusted locations.</span></span>  
<span data-ttu-id="52726-162">Diğer bir deyişle, bir uygulama güvenmediğiniz bir ağdan bir kullanıcı tarafından erişilen, çok faktörlü kimlik doğrulama gereksinimini olabilir.</span><span class="sxs-lookup"><span data-stu-id="52726-162">In other words, you might have a requirement for multi-factor authentication if an app is accessed by a user from a network you don't trust.</span></span>


### <a name="only-trusted-devices-can-access-office-365-services"></a><span data-ttu-id="52726-163">Yalnızca güvenilir cihazlar Office 365 hizmetlerine erişebilir</span><span class="sxs-lookup"><span data-stu-id="52726-163">Only trusted devices can access Office 365 services</span></span>

<span data-ttu-id="52726-164">Ortamınızda Intune kullanıyorsanız, hello koşullu erişim ilkesi hello Azure konsolunda arabiriminde kullanmaya hemen başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52726-164">If you are using Intune in your environment, you can immediately start using hello conditional access policy interface in hello Azure console.</span></span>

<span data-ttu-id="52726-165">Birçok Intune müşterileri yalnızca güvenilen cihazların Office 365 hizmetlerine erişmesini koşullu erişim tooensure kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="52726-165">Many Intune customers are using conditional access tooensure that only trusted devices can access Office 365 services.</span></span> <span data-ttu-id="52726-166">Bu, mobil cihazları Intune'a kayıtlı ve uyumluluk ilkesi gereksinimlerini ve Windows bilgisayarları şirket içi etki alanına katılmış tooan olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="52726-166">This means that mobile devices are enrolled with Intune and meet compliance policy requirements, and that Windows PCs are joined tooan on-premises domain.</span></span> <span data-ttu-id="52726-167">Önemli geliştirmelerden, olmadığı olduğu tooset hello aynı ilke her hello Office 365 Hizmetleri için.</span><span class="sxs-lookup"><span data-stu-id="52726-167">A key improvement is that you do not have tooset hello same policy for each of hello Office 365 services.</span></span>  <span data-ttu-id="52726-168">Yeni bir ilke oluşturduğunuzda, hello bulut uygulamaları tooinclude her ile koşullu erişim ile tooprotect istediğiniz hello O365 uygulamaların yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="52726-168">When you create a new policy, configure hello Cloud apps tooinclude each of hello O365 apps that you wish tooprotect with  with Conditional Access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52726-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="52726-169">Next steps</span></span>

<span data-ttu-id="52726-170">Tooknow nasıl tooconfigure bir koşullu erişim ilkesi görmek istiyorsanız [Azure Active Directory'de koşullu erişimi kullanmaya başlama](active-directory-conditional-access-azure-portal-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="52726-170">If you want tooknow how tooconfigure a conditional access policy, see [Get started with conditional access in Azure Active Directory](active-directory-conditional-access-azure-portal-get-started.md).</span></span>
