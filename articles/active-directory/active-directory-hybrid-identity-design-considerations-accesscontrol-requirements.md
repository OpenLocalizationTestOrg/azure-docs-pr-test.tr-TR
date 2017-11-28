---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - belirlemek erişim denetimi gereksinimlerine | Microsoft Docs"
description: "Kapak kimlik ve karma bir ortamda kullanıcıları için kaynaklar tanımlayıcı erişim gereksinimlerini ayaklar hello."
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
ms.openlocfilehash: f0c22629f732a4c13ee7a24456651bec7637c387
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="9a03d-103">Karma kimlik çözümü için erişim denetimi gereksinimleri belirleme</span><span class="sxs-lookup"><span data-stu-id="9a03d-103">Determine access control requirements for your hybrid identity solution</span></span>
<span data-ttu-id="9a03d-104">Bir kuruluş tasarlarken toomake planladığınıza gereksinimleri hello kaynaklar için erişim de kullanabilecekleri bu fırsatı tooreview kendi karma kimlik çözümü, kullanıcılar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9a03d-104">When an organization is designing their hybrid identity solution they can also use this opportunity tooreview access requirements for hello resources that they are planning toomake it available for users.</span></span> <span data-ttu-id="9a03d-105">Merhaba veri erişimi olan tüm dört ayaklar kimliğini, çapraz:</span><span class="sxs-lookup"><span data-stu-id="9a03d-105">hello data access cross all four pillars of identity, which are:</span></span>

* <span data-ttu-id="9a03d-106">Yönetim</span><span class="sxs-lookup"><span data-stu-id="9a03d-106">Administration</span></span>
* <span data-ttu-id="9a03d-107">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="9a03d-107">Authentication</span></span>
* <span data-ttu-id="9a03d-108">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="9a03d-108">Authorization</span></span>
* <span data-ttu-id="9a03d-109">Denetim</span><span class="sxs-lookup"><span data-stu-id="9a03d-109">Auditing</span></span>

<span data-ttu-id="9a03d-110">izleyen hello bölümleri kimlik doğrulama ve yetkilendirme daha ayrıntılı ele alınacaktır, yönetim ve denetimi hello karma kimlik yaşam döngüsü parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="9a03d-110">hello sections that follows will cover authentication and authorization in more details, administration and auditing are part of hello hybrid identity lifecycle.</span></span> <span data-ttu-id="9a03d-111">Okuma [karma kimlik yönetimi görevleri belirlemek](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) bu özellikleri hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="9a03d-111">Read [Determine hybrid identity management tasks](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) for more information about these capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="9a03d-112">Okuma [hello dört ayaklar kimliği - hello karma BT yaş Identity Management](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) bu dayanaklarından her biri hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="9a03d-112">Read [hello Four Pillars of Identity - Identity Management in hello Age of Hybrid IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) for more information about each one of those pillars.</span></span>
> 
> 

## <a name="authentication-and-authorization"></a><span data-ttu-id="9a03d-113">Kimlik doğrulama ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="9a03d-113">Authentication and authorization</span></span>
<span data-ttu-id="9a03d-114">Kimlik doğrulama ve yetkilendirme için farklı senaryolar vardır, bu senaryoların hello karma kimlik çözümü tarafından hello şirket giderek tooadopt olduğunu yerine getirilmesi gereken belirli gereksinimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="9a03d-114">There are different scenarios for authentication and authorization, these scenarios will have specific requirements that must be fulfilled by hello hybrid identity solution that hello company is going tooadopt.</span></span> <span data-ttu-id="9a03d-115">Merhaba kuruluş tarafından kullanılan kimlik doğrulama ve yetkilendirme yöntemi hello iş ortaklarıyla iletişim kurabilir tooensure gerekir bu yana iş tooBusiness (B2B) içeren senaryoları iletişimi için BT yöneticileri bir ek sınama ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a03d-115">Scenarios involving Business tooBusiness (B2B) communication can add an extra challenge for IT Admins since they will need tooensure that hello authentication and authorization method used by hello organization can communicate with their business partners.</span></span> <span data-ttu-id="9a03d-116">Kimlik doğrulama ve yetkilendirme gereksinimlerine yönelik işlemini tasarlama hello sırasında aşağıdaki soruları bu hello yanıtlanır emin olun:</span><span class="sxs-lookup"><span data-stu-id="9a03d-116">During hello designing process for authentication and authorization requirements, ensure that hello following questions are answered:</span></span>

* <span data-ttu-id="9a03d-117">Kuruluşunuzun kimlik doğrulaması ve kimlik yönetimi sistemlerine bulunan kullanıcıları yetkilendirmek?</span><span class="sxs-lookup"><span data-stu-id="9a03d-117">Will your organization authenticate and authorize only users located at their identity management system?</span></span>
  * <span data-ttu-id="9a03d-118">B2B senaryolarını için herhangi bir plan var mı?</span><span class="sxs-lookup"><span data-stu-id="9a03d-118">Are there any plans for B2B scenarios?</span></span>
  * <span data-ttu-id="9a03d-119">Yanıt Evet ise, zaten hangi protokollerin (SAML, OAuth, Kerberos, belirteçleri veya Sertifikalar) olacak bilebilirsiniz hem işletmeler kullanılan tooconnect olabilir?</span><span class="sxs-lookup"><span data-stu-id="9a03d-119">If yes, do you already know which protocols (SAML, OAuth, Kerberos, Tokens or Certificates) will be used tooconnect both businesses?</span></span>
* <span data-ttu-id="9a03d-120">Merhaba karma kimlik çözümü tooadopt kalacaklarını protokollerin destekliyor mu?</span><span class="sxs-lookup"><span data-stu-id="9a03d-120">Does hello hybrid identity solution that you are going tooadopt support those protocols?</span></span>

<span data-ttu-id="9a03d-121">Başka bir önemli nokta tooconsider burada kullanıcılar ve iş ortakları tarafından kullanılacak hello kimlik doğrulama deposu bulunur ve kullanılan hello yönetim modeli toobe ' dir.</span><span class="sxs-lookup"><span data-stu-id="9a03d-121">Another important point tooconsider is where hello authentication repository that will be used by users and partners will be located and hello administrative model toobe used.</span></span> <span data-ttu-id="9a03d-122">Aşağıdaki iki çekirdek seçenekleri şu hello göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="9a03d-122">Consider hello following two core options:</span></span>

* <span data-ttu-id="9a03d-123">Merkezi: Bu modeli hello kullanıcının kimlik bilgilerini, ilkeleri ve Yönetim Merkezi şirket içi olabilir veya hello bulutta.</span><span class="sxs-lookup"><span data-stu-id="9a03d-123">Centralized: in this model hello user’s credentials, policies and administration can be centralized on-premises or in hello cloud.</span></span>
* <span data-ttu-id="9a03d-124">Karma: Bu modeli hello kullanıcının kimlik bilgilerini, ilkeleri ve Yönetim Merkezi şirket içi ve çoğaltılan hello bulutta olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9a03d-124">Hybrid: in this model hello user’s credentials, policies and administration will be centralized on-premises and a replicated in hello cloud.</span></span>

<span data-ttu-id="9a03d-125">Kuruluşunuz benimseyeceği hangi model according tootheir iş gereksinimleri farklılık gösterir, burada hello kimlik yönetimi sistem bulunan ve Yönetici modu toouse hello soruları tooidentify aşağıdaki tooanswer hello istiyor:</span><span class="sxs-lookup"><span data-stu-id="9a03d-125">Which model your organization will adopt will vary according tootheir business requirements, you want tooanswer hello following questions tooidentify where hello identity management system will reside and hello administrative mode toouse:</span></span>

* <span data-ttu-id="9a03d-126">Kuruluşunuz şu anda bir kimlik yönetimi sahip şirket içi?</span><span class="sxs-lookup"><span data-stu-id="9a03d-126">Does your organization currently have an identity management on-premises?</span></span>
  * <span data-ttu-id="9a03d-127">Yanıt Evet ise, tookeep planlıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="9a03d-127">If yes, do they plan tookeep it?</span></span>
  * <span data-ttu-id="9a03d-128">Kuruluşunuz bu belirtir hello kimlik yönetimi sistemi bulunduğu izlemelisiniz düzenleme veya uyumluluk gereksinimleri var mı?</span><span class="sxs-lookup"><span data-stu-id="9a03d-128">Are there any regulation or compliance requirements that your organization must follow that dictates where hello identity management system should reside?</span></span>
* <span data-ttu-id="9a03d-129">Kuruluşunuz çoklu oturum açma bulunan uygulamalar şirket içi veya hello bulutta kullanıyor mu?</span><span class="sxs-lookup"><span data-stu-id="9a03d-129">Does your organization use single sign-on for apps located on-premises or in hello cloud?</span></span>
  * <span data-ttu-id="9a03d-130">Yanıt Evet ise, bir karma kimlik modelin hello benimseme bu işlem etkiliyor mu?</span><span class="sxs-lookup"><span data-stu-id="9a03d-130">If yes, does hello adoption of a hybrid identity model affect this process?</span></span>

## <a name="access-control"></a><span data-ttu-id="9a03d-131">Access Control</span><span class="sxs-lookup"><span data-stu-id="9a03d-131">Access Control</span></span>
<span data-ttu-id="9a03d-132">Kimlik doğrulama ve yetkilendirme çekirdek öğeleri tooenable erişim toocorporate verilerine kullanıcının doğrulama olsa da, bu da önemli toocontrol hello bu kullanıcıların ve erişim yöneticileri hello düzeyini hello olacak bir erişim düzeyidir yönetmekte olduğunuz kaynaklar.</span><span class="sxs-lookup"><span data-stu-id="9a03d-132">While authentication and authorization are core elements tooenable access toocorporate data through user’s validation, it is also important toocontrol hello level of access that these users will have and hello level of access administrators will have over hello resources that they are managing.</span></span> <span data-ttu-id="9a03d-133">Karma kimlik çözümü mümkün tooprovide ayrıntılı erişim tooresources, temsilci seçme ve rol tabanlı erişim denetimini olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a03d-133">Your hybrid identity solution must be able tooprovide granular access tooresources, delegation and role base access control.</span></span> <span data-ttu-id="9a03d-134">Soru aşağıdaki o Merhaba, erişim denetimi ile ilgili yanıtlanır emin olun:</span><span class="sxs-lookup"><span data-stu-id="9a03d-134">Ensure that hello following question are answered regarding access control:</span></span>

* <span data-ttu-id="9a03d-135">Şirketiniz yükseltilmiş ayrıcalık toomanage ile birden fazla kullanıcı, kimlik sistemi var mı?</span><span class="sxs-lookup"><span data-stu-id="9a03d-135">Does your company have more than one user with elevated privilege toomanage your identity system?</span></span>
  * <span data-ttu-id="9a03d-136">Evet, her kullanıcı hello mu gerekiyorsa aynı erişim düzeyi?</span><span class="sxs-lookup"><span data-stu-id="9a03d-136">If yes, does each user need hello same access level?</span></span>
* <span data-ttu-id="9a03d-137">Şirket gerek toodelegate erişim toousers toomanage belirli kaynaklarınıza musunuz?</span><span class="sxs-lookup"><span data-stu-id="9a03d-137">Would your company need toodelegate access toousers toomanage specific resources?</span></span>
  * <span data-ttu-id="9a03d-138">Yanıt Evet ise, bu ne sıklıkta olur?</span><span class="sxs-lookup"><span data-stu-id="9a03d-138">If yes, how frequently this happens?</span></span>
* <span data-ttu-id="9a03d-139">Şirket içi ve bulut arasında toointegrate erişim denetimi özelliklerinden gerekir kaynakları?</span><span class="sxs-lookup"><span data-stu-id="9a03d-139">Would your company need toointegrate access control capabilities between on-premises and cloud resources?</span></span>
* <span data-ttu-id="9a03d-140">Şirketiniz toosome koşullara göre toolimit erişim tooresources gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="9a03d-140">Would your company need toolimit access tooresources according toosome conditions?</span></span>
* <span data-ttu-id="9a03d-141">Şirketiniz özel denetim toosome kaynaklarına erişim gerektiren herhangi bir uygulama bulunur?</span><span class="sxs-lookup"><span data-stu-id="9a03d-141">Would your company have any application that needs custom control access toosome resources?</span></span>
  * <span data-ttu-id="9a03d-142">Yanıt Evet ise, burada uygulamalarla bulunur (şirket içi veya hello bulutta)?</span><span class="sxs-lookup"><span data-stu-id="9a03d-142">If yes, where are those apps located (on-premises or in hello cloud)?</span></span>
  * <span data-ttu-id="9a03d-143">Yanıtınız evet ise, burada olan bu hedef kaynaklara (şirket içi veya hello bulutta)?</span><span class="sxs-lookup"><span data-stu-id="9a03d-143">If yes, where are those target resources located (on-premises or in hello cloud)?</span></span>

> [!NOTE]
> <span data-ttu-id="9a03d-144">Her yanıtı tootake Not emin olun ve hello yanıtın hello yanıt arkasındaki mantığı anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9a03d-144">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="9a03d-145">[Veri koruma stratejisini tanımlayın](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) hello seçenekleri ve her seçeneğin olumlu/olumsuz üzerinden geçer.</span><span class="sxs-lookup"><span data-stu-id="9a03d-145">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="9a03d-146">Bu soruyu yanıtlayarak, iş gereksinimlerinize en iyi hangi seçeneği en seçersiniz.</span><span class="sxs-lookup"><span data-stu-id="9a03d-146">By answering those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9a03d-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9a03d-147">Next steps</span></span>
[<span data-ttu-id="9a03d-148">Olay yanıtlama gereksinimlerini belirleyin</span><span class="sxs-lookup"><span data-stu-id="9a03d-148">Determine incident response requirements</span></span>](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a><span data-ttu-id="9a03d-149">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="9a03d-149">See Also</span></span>
[<span data-ttu-id="9a03d-150">Tasarım konularına genel bakış</span><span class="sxs-lookup"><span data-stu-id="9a03d-150">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

