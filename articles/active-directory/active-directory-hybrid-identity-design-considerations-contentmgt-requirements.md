---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - içerik yönetimi gereksinimlerini belirleme | Microsoft Docs"
description: "İçine nasıl toodetermine hello işinizin içerik yönetimi gereksinimleri hakkında bilgi sağlar. Genellikle bir kullanıcı kendi aygıt olduğunda kendisi de kullandığı according toohello uygulama değişen birden çok kimlik olabilir. Bu, önemli toodifferentiate hangi içerik hello Kurumsal kimlik bilgileri kullanılarak oluşturulan olanları karşı kişisel kimlik bilgileri kullanılarak oluşturulmuş olur. Kimlik çözümünüzün bir deneyim toohello son kullanıcı sırasında bulut Hizmetleri tooprovide ile mümkün toointeract olmalıdır kendi gizlilik sağlamak ve veri sızıntısına karşı koruma hello artırın."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="42e45-106">Karma kimlik çözümü için içerik yönetimi gereksinimlerini belirleyin</span><span class="sxs-lookup"><span data-stu-id="42e45-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="42e45-107">İşinizi yönlendirebilir için hello içerik yönetimi gereksinimleri anlama kararınızı hangi karma kimlik çözümü toouse üzerindeki etkiler.</span><span class="sxs-lookup"><span data-stu-id="42e45-107">Understanding hello content management requirements for your business may direct affect your decision on which hybrid identity solution toouse.</span></span> <span data-ttu-id="42e45-108">İle birden çok aygıtların artışı ve kullanıcıların toobring hello yeteneğini kendi cihazlarını hello ([KCG](http://aka.ms/byodcg)), hello şirket kendi verilerini korumak gerekir, ancak bu ayrıca kullanıcının gizliliğini korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="42e45-108">With hello proliferation of multiple devices and hello capability of users toobring their own devices ([BYOD](http://aka.ms/byodcg)), hello company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="42e45-109">Genellikle bir kullanıcı kendi aygıt olduğunda kendisi de kullandığı according toohello uygulama değişen birden çok kimlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="42e45-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according toohello application that he uses.</span></span> <span data-ttu-id="42e45-110">Bu, önemli toodifferentiate hangi içerik hello Kurumsal kimlik bilgileri kullanılarak oluşturulan olanları karşı kişisel kimlik bilgileri kullanılarak oluşturulmuş olur.</span><span class="sxs-lookup"><span data-stu-id="42e45-110">It is important toodifferentiate what content was created using personal credentials versus hello ones created using corporate credentials.</span></span> <span data-ttu-id="42e45-111">Kimlik çözümünüzün bir deneyim toohello son kullanıcı sırasında bulut Hizmetleri tooprovide ile mümkün toointeract olmalıdır kendi gizlilik sağlamak ve veri sızıntısına karşı koruma hello artırın.</span><span class="sxs-lookup"><span data-stu-id="42e45-111">Your identity solution should be able toointeract with cloud services tooprovide a seamless experience toohello end user while ensure his privacy and increase hello protection against data leakage.</span></span> 

<span data-ttu-id="42e45-112">Kimlik çözümünüzü farklı teknik denetimler sipariş tooprovide İçerik Yönetimi'nde hello aşağıdaki çizimde gösterildiği gibi işlevden:</span><span class="sxs-lookup"><span data-stu-id="42e45-112">Your identity solution will be leveraged by different technical controls in order tooprovide content management as shown in hello figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="42e45-113">**Kimlik yönetimi sistemi yararlanarak güvenlik denetimleri**</span><span class="sxs-lookup"><span data-stu-id="42e45-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="42e45-114">Genel olarak, içerik yönetimi gereksinimlerini Kimlik Yönetimi sisteminizde alanları aşağıdaki hello özelliğinden yararlanır:</span><span class="sxs-lookup"><span data-stu-id="42e45-114">In general, content management requirements will leverage your identity management system in hello following areas:</span></span>

* <span data-ttu-id="42e45-115">Gizlilik: bir kaynağın sahibi hello kullanıcı tanımlama ve hello uygun denetimleri toomaintain bütünlüğü uygulanıyor.</span><span class="sxs-lookup"><span data-stu-id="42e45-115">Privacy: identifying hello user that owns a resource and applying hello appropriate controls toomaintain integrity.</span></span>
* <span data-ttu-id="42e45-116">Veri Sınıflandırması: hello kullanıcıyı veya grubu ve tooits sınıflandırma göre erişimi tooan nesnesi düzeyini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="42e45-116">Data Classification: identify hello user or group and level of access tooan object according tooits classification.</span></span> 
* <span data-ttu-id="42e45-117">Veri sızıntısı koruma: güvenlik denetimleri veri tooavoid sızıntısı koruma sorumluluğunu hello kimlik sistemi toovalidate hello kullanıcı kimliği ile toointeract gerekir.</span><span class="sxs-lookup"><span data-stu-id="42e45-117">Data Leakage Protection: security controls responsible for protecting data tooavoid leakage will need toointeract with hello identity system toovalidate hello user’s identity.</span></span> <span data-ttu-id="42e45-118">Bu da izi amacı denetimi için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="42e45-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="42e45-119">Okuma [bulut hazırlık için veri sınıflandırma](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) en iyi yöntemler ve veri sınıflandırması için yönergeleri hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="42e45-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="42e45-120">Karma kimlik çözümü planlama olun olduğunda aşağıdaki o hello tooyour kuruluşunuzun gereksinimlerine göre soruları yanıtlanır:</span><span class="sxs-lookup"><span data-stu-id="42e45-120">When planning your hybrid identity solution ensure that hello following questions are answered according tooyour organization’s requirements:</span></span>

* <span data-ttu-id="42e45-121">Şirketinizin güvenlik denetimleri yer tooenforce veri gizlilik var mı?</span><span class="sxs-lookup"><span data-stu-id="42e45-121">Does your company have security controls in place tooenforce data privacy?</span></span>
  * <span data-ttu-id="42e45-122">Yanıt Evet ise, bu güvenlik denetimleri, devam eden tooadopt olduğunuzu hello karma kimlik çözümü ile mümkün toointegrate olacak?</span><span class="sxs-lookup"><span data-stu-id="42e45-122">If yes, will those security controls be able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="42e45-123">Şirketiniz veri sınıflandırması kullanıyor mu?</span><span class="sxs-lookup"><span data-stu-id="42e45-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="42e45-124">Yanıt Evet ise, hello geçerli çözüm mümkün toointegrate hello karma kimlik çözümü giderek tooadopt olduğunuz ile mi?</span><span class="sxs-lookup"><span data-stu-id="42e45-124">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="42e45-125">Şirketiniz veri sızıntısı için herhangi bir çözümü şu anda var mı?</span><span class="sxs-lookup"><span data-stu-id="42e45-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="42e45-126">Yanıt Evet ise, hello geçerli çözüm mümkün toointegrate hello karma kimlik çözümü giderek tooadopt olduğunuz ile mi?</span><span class="sxs-lookup"><span data-stu-id="42e45-126">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="42e45-127">Şirketinizin tooaudit erişim tooresources gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="42e45-127">Does your company need tooaudit access tooresources?</span></span>
  * <span data-ttu-id="42e45-128">Yanıt Evet ise, hangi kaynakları tür?</span><span class="sxs-lookup"><span data-stu-id="42e45-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="42e45-129">Yanıt Evet ise, hangi bilgilerin düzeyini gerekli mi?</span><span class="sxs-lookup"><span data-stu-id="42e45-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="42e45-130">Yanıt Evet ise, hello denetim günlüğü bulunduğu gerekir?</span><span class="sxs-lookup"><span data-stu-id="42e45-130">If yes, where hello audit log must reside?</span></span> <span data-ttu-id="42e45-131">Şirket içi veya hello bulutta?</span><span class="sxs-lookup"><span data-stu-id="42e45-131">On-premises or in hello cloud?</span></span>
* <span data-ttu-id="42e45-132">Şirketinizin hassas veriler (Ssn'ler, kredi kartı numaraları, vb.) içeren e-postaları tooencrypt gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="42e45-132">Does your company need tooencrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="42e45-133">Şirketinizin tooencrypt dış iş ortaklarıyla paylaşılan tüm belgeler/içerik gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="42e45-133">Does your company need tooencrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="42e45-134">Şirketinizin e-postalar belirli türdeki tooenforce şirket ilkeleri gerekiyor mu (tüm yanıt yapmak için iletme)?</span><span class="sxs-lookup"><span data-stu-id="42e45-134">Does your company need tooenforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="42e45-135">Her yanıtı tootake Not emin olun ve hello yanıtın hello yanıt arkasındaki mantığı anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="42e45-135">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="42e45-136">[Veri koruma stratejisini tanımlayın](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) hello seçenekleri ve her seçeneğin olumlu/olumsuz üzerinden geçer.</span><span class="sxs-lookup"><span data-stu-id="42e45-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="42e45-137">Seçeneği, iş gereksinimlerinize en uygun belirleyeceksiniz bu soruları yanıtladığınızda gerekir.</span><span class="sxs-lookup"><span data-stu-id="42e45-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="42e45-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="42e45-138">Next steps</span></span>
[<span data-ttu-id="42e45-139">Erişim denetimi gereksinimlerini belirleme</span><span class="sxs-lookup"><span data-stu-id="42e45-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="42e45-140">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="42e45-140">See Also</span></span>
[<span data-ttu-id="42e45-141">Tasarım konularına genel bakış</span><span class="sxs-lookup"><span data-stu-id="42e45-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

