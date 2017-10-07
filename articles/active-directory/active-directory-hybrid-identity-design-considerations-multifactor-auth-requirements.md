---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - çok faktörlü kimlik doğrulama gereksinimlerini belirleme"
description: "Koşullu erişim denetimi ile Azure Active Directory hello belirli koşullar hello kullanıcı kimlik doğrulaması ve erişim toohello uygulama izin vermeden önce çekme denetler. Bu koşullar sağlandığında hello kullanıcı kimlik doğrulaması ve erişim toohello uygulama izin verilir."
documentationcenter: 
services: active-directory
author: femila
manager: billmath
editor: 
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 49fa7b43772fb3a2d6664747477c60a34cddde2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="161e1-104">Karma kimlik çözümü çok faktörlü kimlik doğrulama gereksinimlerini belirleme</span><span class="sxs-lookup"><span data-stu-id="161e1-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="161e1-105">Veri ve uygulamaları hello bulutta ve herhangi bir CİHAZDAN erişen kullanıcılar ile yeteneği bu dünyasında bu bilgileri güvenlik altına almanın en önemli haline gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="161e1-105">In this world of mobility, with users accessing data and applications in hello cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="161e1-106">Her gün yeni bir başlık güvenlik ihlali hakkında yoktur.</span><span class="sxs-lookup"><span data-stu-id="161e1-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="161e1-107">Çok faktörlü kimlik doğrulaması, olmasına karşın, bu tür ihlallerine karşı garanti, ek bir katman sağlar güvenliğini toohelp önlemek bu ihlallerini.</span><span class="sxs-lookup"><span data-stu-id="161e1-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security toohelp prevent these breaches.</span></span>
<span data-ttu-id="161e1-108">Çok faktörlü kimlik doğrulaması için Hello kuruluşların gereksinimleri değerlendirerek başlatın.</span><span class="sxs-lookup"><span data-stu-id="161e1-108">Start by evaluating hello organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="161e1-109">Diğer bir deyişle, hello kuruluş çalışırken toosecure nedir.</span><span class="sxs-lookup"><span data-stu-id="161e1-109">That is, what is hello organization trying toosecure.</span></span>  <span data-ttu-id="161e1-110">Bu değerlendirme önemli toodefine hello teknik gereksinimlerine ayarlama ve çok faktörlü kimlik doğrulaması için hello kuruluşların kullanıcıları etkinleştirme olur.</span><span class="sxs-lookup"><span data-stu-id="161e1-110">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="161e1-111">MFA ile ne yaptığını bilmiyorsanız, hello makalesini okuyun önerilir [Azure multi-Factor Authentication nedir?](../multi-factor-authentication/multi-factor-authentication.md) bu bölümü okumadan önce toocontinue.</span><span class="sxs-lookup"><span data-stu-id="161e1-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read hello article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior toocontinue reading this section.</span></span>
> 
> 

<span data-ttu-id="161e1-112">Emin tooanswer hello aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="161e1-112">Make sure tooanswer hello following:</span></span>

* <span data-ttu-id="161e1-113">Şirketiniz toosecure Microsoft uygulamaları çalışıyor?</span><span class="sxs-lookup"><span data-stu-id="161e1-113">Is your company trying toosecure Microsoft apps?</span></span> 
* <span data-ttu-id="161e1-114">Bu uygulamaları nasıl yayımlanacak?</span><span class="sxs-lookup"><span data-stu-id="161e1-114">How these apps are published?</span></span>
* <span data-ttu-id="161e1-115">Şirketiniz uzaktan erişim tooallow çalışanlar tooaccess şirket içi uygulamalar sağlar?</span><span class="sxs-lookup"><span data-stu-id="161e1-115">Does your company provide remote access tooallow employees tooaccess on-premises apps?</span></span>

<span data-ttu-id="161e1-116">Yanıt Evet ise, hangi uzaktan erişimi tür? Ayrıca bu uygulamalara erişen hello kullanıcılar nerede yer alacağı tooevaluate gerekir.</span><span class="sxs-lookup"><span data-stu-id="161e1-116">If yes, what type of remote access?You also need tooevaluate where hello users who are accessing these applications will be located.</span></span> <span data-ttu-id="161e1-117">Bu değerlendirme başka bir önemli adım toodefine hello uygun çok faktörlü kimlik doğrulama stratejisi ' dir.</span><span class="sxs-lookup"><span data-stu-id="161e1-117">This evaluation is another important step toodefine hello proper multi-factor authentication strategy.</span></span> <span data-ttu-id="161e1-118">Aşağıdaki sorular emin tooanswer hello olun:</span><span class="sxs-lookup"><span data-stu-id="161e1-118">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="161e1-119">Toobe giderek hello kullanıcıların bulunduğu?</span><span class="sxs-lookup"><span data-stu-id="161e1-119">Where are hello users going toobe located?</span></span>
* <span data-ttu-id="161e1-120">Bunlar herhangi bir yerde bulunan olabilir mi?</span><span class="sxs-lookup"><span data-stu-id="161e1-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="161e1-121">Şirketiniz toohello kullanıcının konumuna göre tooestablish kısıtlamaları istiyor mu?</span><span class="sxs-lookup"><span data-stu-id="161e1-121">Does your company want tooestablish restrictions according toohello user’s location?</span></span>

<span data-ttu-id="161e1-122">Bu gereksinimleri anladığınızda, tooalso değerlendirmek için çok faktörlü kimlik doğrulaması hello kullanıcının gereksinimleri önemlidir.</span><span class="sxs-lookup"><span data-stu-id="161e1-122">Once you understand these requirements, it is important tooalso evaluate hello user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="161e1-123">Bu değerlendirme önemlidir, çünkü çok faktörlü kimlik doğrulaması çalışırken hello gereksinimleri tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="161e1-123">This evaluation is important because it will define hello requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="161e1-124">Aşağıdaki sorular emin tooanswer hello olun:</span><span class="sxs-lookup"><span data-stu-id="161e1-124">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="161e1-125">Merhaba kullanıcıların çok faktörlü kimlik doğrulaması ile bilinen misiniz?</span><span class="sxs-lookup"><span data-stu-id="161e1-125">Are hello users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="161e1-126">Bazı kullanımlarını gerekli tooprovide ek kimlik doğrulama olacak?</span><span class="sxs-lookup"><span data-stu-id="161e1-126">Will some uses be required tooprovide additional authentication?</span></span>  
  * <span data-ttu-id="161e1-127">Yanıt Evet ise, tüm Merhaba, dış ağlara ya da erişimi belirli uygulamalar veya diğer koşullar altında çıkarken zaman?</span><span class="sxs-lookup"><span data-stu-id="161e1-127">If yes, all hello time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="161e1-128">Merhaba kullanıcıların nasıl eğitim gerektirir toosetup ve uygulama çok faktörlü kimlik doğrulaması?</span><span class="sxs-lookup"><span data-stu-id="161e1-128">Will hello users require training on how toosetup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="161e1-129">Şirket kullanıcılarının tooenable çok faktörlü kimlik doğrulamasını istediği hello temel senaryolar nelerdir?</span><span class="sxs-lookup"><span data-stu-id="161e1-129">What are hello key scenarios that your company wants tooenable multi-factor authentication for their users?</span></span>

<span data-ttu-id="161e1-130">Merhaba önceki sorulara yanıt verilmesi sonra çok faktörlü kimlik doğrulaması zaten uygulanmış şirket içi varsa mümkün toounderstand olacaktır.</span><span class="sxs-lookup"><span data-stu-id="161e1-130">After answering hello previous questions, you will be able toounderstand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="161e1-131">Bu değerlendirme önemli toodefine hello teknik gereksinimlerine ayarlama ve çok faktörlü kimlik doğrulaması için hello kuruluşların kullanıcıları etkinleştirme olur.</span><span class="sxs-lookup"><span data-stu-id="161e1-131">This evaluation is important toodefine hello technical requirements for setting up and enabling hello organizations users for multi-factor authentication.</span></span> <span data-ttu-id="161e1-132">Aşağıdaki sorular emin tooanswer hello olun:</span><span class="sxs-lookup"><span data-stu-id="161e1-132">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="161e1-133">Şirketinizin tooprotect ayrıcalıklı hesapları MFA ile gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="161e1-133">Does your company need tooprotect privileged accounts with MFA?</span></span>
* <span data-ttu-id="161e1-134">Şirketinizin tooenable MFA belirli uygulama uyumluluk nedenleriyle gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="161e1-134">Does your company need tooenable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="161e1-135">Şirketiniz, bu uygulama ya da yalnızca Yöneticiler tüm uygun kullanıcılar için tooenable MFA gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="161e1-135">Does your company need tooenable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="161e1-136">Her zaman etkin MFA veya yalnızca zaman hello kullanıcılar şirket ağının dışından oturum olmak zorunda?</span><span class="sxs-lookup"><span data-stu-id="161e1-136">Do you need have MFA always enabled or only when hello users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="161e1-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="161e1-137">Next steps</span></span>
[<span data-ttu-id="161e1-138">Bir karma kimlik benimseme stratejinizi tanımlayın</span><span class="sxs-lookup"><span data-stu-id="161e1-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="161e1-139">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="161e1-139">See also</span></span>
[<span data-ttu-id="161e1-140">Tasarım konularına genel bakış</span><span class="sxs-lookup"><span data-stu-id="161e1-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

