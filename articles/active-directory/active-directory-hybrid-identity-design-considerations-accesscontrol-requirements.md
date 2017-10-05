---
title: "Azure Active Directory karma kimlik tasarımı hakkında dikkat edilecek noktalar - belirlemek erişim denetimi gereksinimlerine | Microsoft Docs"
description: "Kimlik ve karma bir ortamda kullanıcıları için kaynaklar için erişim gereksinimleri tanımlama ayaklar kapsar."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6404940da460461632616fe49f055d50c2a7aba3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="b7de0-103">Karma kimlik çözümü için erişim denetimi gereksinimleri belirleme</span><span class="sxs-lookup"><span data-stu-id="b7de0-103">Determine access control requirements for your hybrid identity solution</span></span>
<span data-ttu-id="b7de0-104">Bir kuruluş kendi karma kimlik çözümü tasarlarken, bu fırsatı kullanıcılar için kullanılabilir hale getirmek için planlama kaynaklar için erişim gereksinimleri gözden geçirmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7de0-104">When an organization is designing their hybrid identity solution they can also use this opportunity to review access requirements for the resources that they are planning to make it available for users.</span></span> <span data-ttu-id="b7de0-105">Veri erişimi olan tüm dört ayaklar kimliğini, çapraz:</span><span class="sxs-lookup"><span data-stu-id="b7de0-105">The data access cross all four pillars of identity, which are:</span></span>

* <span data-ttu-id="b7de0-106">Yönetim</span><span class="sxs-lookup"><span data-stu-id="b7de0-106">Administration</span></span>
* <span data-ttu-id="b7de0-107">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="b7de0-107">Authentication</span></span>
* <span data-ttu-id="b7de0-108">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="b7de0-108">Authorization</span></span>
* <span data-ttu-id="b7de0-109">Denetim</span><span class="sxs-lookup"><span data-stu-id="b7de0-109">Auditing</span></span>

<span data-ttu-id="b7de0-110">Aşağıdaki bölümlerde, kimlik doğrulama ve yetkilendirme daha ayrıntılı ele alınacaktır, yönetim ve denetimi karma kimlik yaşam döngüsü parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="b7de0-110">The sections that follows will cover authentication and authorization in more details, administration and auditing are part of the hybrid identity lifecycle.</span></span> <span data-ttu-id="b7de0-111">Okuma [karma kimlik yönetimi görevleri belirlemek](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) bu özellikleri hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b7de0-111">Read [Determine hybrid identity management tasks](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) for more information about these capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="b7de0-112">Okuma [dört ayaklar kimliği - karma BT yaş Identity Management](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) bu dayanaklarından her biri hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="b7de0-112">Read [The Four Pillars of Identity - Identity Management in the Age of Hybrid IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) for more information about each one of those pillars.</span></span>
> 
> 

## <a name="authentication-and-authorization"></a><span data-ttu-id="b7de0-113">Kimlik doğrulama ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="b7de0-113">Authentication and authorization</span></span>
<span data-ttu-id="b7de0-114">Kimlik doğrulama ve yetkilendirme için farklı senaryolar vardır, bu senaryoların şirket benimsemeye gittiği karma kimlik çözümü tarafından yerine getirilmesi gereken belirli gereksinimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="b7de0-114">There are different scenarios for authentication and authorization, these scenarios will have specific requirements that must be fulfilled by the hybrid identity solution that the company is going to adopt.</span></span> <span data-ttu-id="b7de0-115">Kuruluş tarafından kullanılan kimlik doğrulama ve yetkilendirme yöntemi iş ortakları ile iletişim kurabildiğinden emin olun gerekir bu yana işletmeler için (B2B) iletişim içeren senaryoları için BT yöneticileri bir ek sınama ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b7de0-115">Scenarios involving Business to Business (B2B) communication can add an extra challenge for IT Admins since they will need to ensure that the authentication and authorization method used by the organization can communicate with their business partners.</span></span> <span data-ttu-id="b7de0-116">Kimlik doğrulama ve yetkilendirme gereksinimlerine yönelik tasarım işlemi sırasında aşağıdaki soruları yanıtlanır emin olun:</span><span class="sxs-lookup"><span data-stu-id="b7de0-116">During the designing process for authentication and authorization requirements, ensure that the following questions are answered:</span></span>

* <span data-ttu-id="b7de0-117">Kuruluşunuzun kimlik doğrulaması ve kimlik yönetimi sistemlerine bulunan kullanıcıları yetkilendirmek?</span><span class="sxs-lookup"><span data-stu-id="b7de0-117">Will your organization authenticate and authorize only users located at their identity management system?</span></span>
  * <span data-ttu-id="b7de0-118">B2B senaryolarını için herhangi bir plan var mı?</span><span class="sxs-lookup"><span data-stu-id="b7de0-118">Are there any plans for B2B scenarios?</span></span>
  * <span data-ttu-id="b7de0-119">Yanıt Evet ise, hangi protokollerin (SAML, OAuth, Kerberos, belirteçleri veya sertifikaları) her iki işletmeler bağlanmak için kullanılan zaten biliyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="b7de0-119">If yes, do you already know which protocols (SAML, OAuth, Kerberos, Tokens or Certificates) will be used to connect both businesses?</span></span>
* <span data-ttu-id="b7de0-120">Destek benimsemeyi kalacaklarını karma kimlik çözümü protokollerin mu?</span><span class="sxs-lookup"><span data-stu-id="b7de0-120">Does the hybrid identity solution that you are going to adopt support those protocols?</span></span>

<span data-ttu-id="b7de0-121">Dikkate alınması gereken başka bir önemli olduğu kullanıcılar ve iş ortakları tarafından kullanılacak kimlik doğrulama deposu bulunur ve kullanılacak yönetim modeli noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="b7de0-121">Another important point to consider is where the authentication repository that will be used by users and partners will be located and the administrative model to be used.</span></span> <span data-ttu-id="b7de0-122">Aşağıdaki iki çekirdek seçenekleri göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="b7de0-122">Consider the following two core options:</span></span>

* <span data-ttu-id="b7de0-123">Merkezi: Bu modelde, kullanıcının kimlik bilgilerini, ilkeleri ve Yönetim Merkezi şirket içi olabilir veya bulutta.</span><span class="sxs-lookup"><span data-stu-id="b7de0-123">Centralized: in this model the user’s credentials, policies and administration can be centralized on-premises or in the cloud.</span></span>
* <span data-ttu-id="b7de0-124">Karma: Bu modelde, kullanıcının kimlik bilgilerini, ilkeleri ve Yönetim Merkezi şirket içi ve çoğaltılan bulutta olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b7de0-124">Hybrid: in this model the user’s credentials, policies and administration will be centralized on-premises and a replicated in the cloud.</span></span>

<span data-ttu-id="b7de0-125">Kuruluşunuz benimseyeceği hangi modeli iş gereksinimlerine göre farklılık gösterir, kimlik yönetimi sistemi bulunacağı ve kullanmak için yönetici moduna belirlemek için aşağıdaki soruları yanıtlayın istiyor:</span><span class="sxs-lookup"><span data-stu-id="b7de0-125">Which model your organization will adopt will vary according to their business requirements, you want to answer the following questions to identify where the identity management system will reside and the administrative mode to use:</span></span>

* <span data-ttu-id="b7de0-126">Kuruluşunuz şu anda bir kimlik yönetimi sahip şirket içi?</span><span class="sxs-lookup"><span data-stu-id="b7de0-126">Does your organization currently have an identity management on-premises?</span></span>
  * <span data-ttu-id="b7de0-127">Yanıt Evet ise, kalmasını sağlamak planlıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="b7de0-127">If yes, do they plan to keep it?</span></span>
  * <span data-ttu-id="b7de0-128">Kuruluşunuz bu belirtir kimlik yönetimi sistemi bulunduğu izlemelisiniz düzenleme veya uyumluluk gereksinimleri var mı?</span><span class="sxs-lookup"><span data-stu-id="b7de0-128">Are there any regulation or compliance requirements that your organization must follow that dictates where the identity management system should reside?</span></span>
* <span data-ttu-id="b7de0-129">Kuruluşunuz çoklu oturum açma bulunan uygulamalar şirket içi veya bulutta kullanıyor mu?</span><span class="sxs-lookup"><span data-stu-id="b7de0-129">Does your organization use single sign-on for apps located on-premises or in the cloud?</span></span>
  * <span data-ttu-id="b7de0-130">Yanıt Evet ise, bir karma kimlik modeli benimsenmesi bu işlem etkiliyor mu?</span><span class="sxs-lookup"><span data-stu-id="b7de0-130">If yes, does the adoption of a hybrid identity model affect this process?</span></span>

## <a name="access-control"></a><span data-ttu-id="b7de0-131">Access Control</span><span class="sxs-lookup"><span data-stu-id="b7de0-131">Access Control</span></span>
<span data-ttu-id="b7de0-132">Kimlik doğrulama ve yetkilendirme kullanıcının doğrulama şirket verilerine erişimi etkinleştirmek için çekirdek öğeleri olsa da, ayrıca, bu kullanıcıların sahip ve erişim yöneticileri düzeyini yönetmekte olduğunuz kaynakları sahip erişim düzeyini denetlemek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="b7de0-132">While authentication and authorization are core elements to enable access to corporate data through user’s validation, it is also important to control the level of access that these users will have and the level of access administrators will have over the resources that they are managing.</span></span> <span data-ttu-id="b7de0-133">Karma kimlik çözümü kaynaklar, temsilci ve rol tabanlı erişim denetimini ayrıntılı erişim sağlamak mümkün olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b7de0-133">Your hybrid identity solution must be able to provide granular access to resources, delegation and role base access control.</span></span> <span data-ttu-id="b7de0-134">Aşağıdaki soruyu erişim denetimi ile ilgili yanıtlanır emin olun:</span><span class="sxs-lookup"><span data-stu-id="b7de0-134">Ensure that the following question are answered regarding access control:</span></span>

* <span data-ttu-id="b7de0-135">Şirketinizin yükseltilmiş ayrıcalığa sahip birden fazla kullanıcı, kimlik sistemi yönetmek için var mı?</span><span class="sxs-lookup"><span data-stu-id="b7de0-135">Does your company have more than one user with elevated privilege to manage your identity system?</span></span>
  * <span data-ttu-id="b7de0-136">Yanıt Evet ise, her kullanıcı aynı erişim düzeyini gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="b7de0-136">If yes, does each user need the same access level?</span></span>
* <span data-ttu-id="b7de0-137">Şirketinizin belirli kaynakları yönetmek için kullanıcılara erişim vermek gerekir?</span><span class="sxs-lookup"><span data-stu-id="b7de0-137">Would your company need to delegate access to users to manage specific resources?</span></span>
  * <span data-ttu-id="b7de0-138">Yanıt Evet ise, bu ne sıklıkta olur?</span><span class="sxs-lookup"><span data-stu-id="b7de0-138">If yes, how frequently this happens?</span></span>
* <span data-ttu-id="b7de0-139">Şirketiniz şirket içi ve bulut arasında erişim denetim özelliklerini tümleştiren gerek kaynakları?</span><span class="sxs-lookup"><span data-stu-id="b7de0-139">Would your company need to integrate access control capabilities between on-premises and cloud resources?</span></span>
* <span data-ttu-id="b7de0-140">Bazı koşullar uygun olarak kaynaklara erişimi sınırlamak, şirketinizin gerekir?</span><span class="sxs-lookup"><span data-stu-id="b7de0-140">Would your company need to limit access to resources according to some conditions?</span></span>
* <span data-ttu-id="b7de0-141">Şirketiniz bazı kaynaklar özel denetim erişmesi gereken herhangi bir uygulama bulunur?</span><span class="sxs-lookup"><span data-stu-id="b7de0-141">Would your company have any application that needs custom control access to some resources?</span></span>
  * <span data-ttu-id="b7de0-142">Yanıt Evet ise, burada uygulamalarla bulunur (şirket içi veya bulutta)?</span><span class="sxs-lookup"><span data-stu-id="b7de0-142">If yes, where are those apps located (on-premises or in the cloud)?</span></span>
  * <span data-ttu-id="b7de0-143">Yanıtınız evet ise, burada olan bu hedef kaynaklara (şirket içi veya bulutta)?</span><span class="sxs-lookup"><span data-stu-id="b7de0-143">If yes, where are those target resources located (on-premises or in the cloud)?</span></span>

> [!NOTE]
> <span data-ttu-id="b7de0-144">Her yanıtı not alın ve yanıtın yanıtın arkasındaki mantığı anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b7de0-144">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="b7de0-145">[Veri koruma stratejisini tanımlayın](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) seçenekleri ve her seçeneğin olumlu/olumsuz üzerinden geçer.</span><span class="sxs-lookup"><span data-stu-id="b7de0-145">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="b7de0-146">Bu soruyu yanıtlayarak, iş gereksinimlerinize en iyi hangi seçeneği en seçersiniz.</span><span class="sxs-lookup"><span data-stu-id="b7de0-146">By answering those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b7de0-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b7de0-147">Next steps</span></span>
[<span data-ttu-id="b7de0-148">Olay yanıtlama gereksinimlerini belirleyin</span><span class="sxs-lookup"><span data-stu-id="b7de0-148">Determine incident response requirements</span></span>](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a><span data-ttu-id="b7de0-149">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="b7de0-149">See Also</span></span>
[<span data-ttu-id="b7de0-150">Tasarım konularına genel bakış</span><span class="sxs-lookup"><span data-stu-id="b7de0-150">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

