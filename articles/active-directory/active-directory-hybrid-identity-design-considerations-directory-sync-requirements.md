---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - dizin eşitleme gereksinimlerini belirleme | Microsoft Docs"
description: "Hangi gereksinimler tüm hello kullanıcılar arasında eşitlemek için gerekli olan tanımlamak şirket içi ve bulut hello kuruluş için on =."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6646e3792c65f37c3d62eecdb6c6f3bd257f04f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-directory-synchronization-requirements"></a><span data-ttu-id="cefcd-103">Dizin eşitleme gereksinimlerini belirleyin</span><span class="sxs-lookup"><span data-stu-id="cefcd-103">Determine directory synchronization requirements</span></span>
<span data-ttu-id="cefcd-104">Eşitleme, kullanıcıların kendi şirket içi kimliğine göre hello bulutta bir kimlik sağlama tüm hakkında olur.</span><span class="sxs-lookup"><span data-stu-id="cefcd-104">Synchronization is all about providing users an identity in hello cloud based on their on-premises identity.</span></span> <span data-ttu-id="cefcd-105">Kimlik doğrulaması veya şirket dışı kimlik doğrulaması için eşitlenmiş hesap kullanacakları olmadığını hello kullanıcılar yine toohave hello bulutta bir kimlik gerekir.</span><span class="sxs-lookup"><span data-stu-id="cefcd-105">Whether or not they will use synchronized account for authentication or federated authentication, hello users will still need toohave an identity in hello cloud.</span></span>  <span data-ttu-id="cefcd-106">Bu kimlik korunur ve düzenli aralıklarla güncelleştirilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="cefcd-106">This identity will need toobe maintained and updated periodically.</span></span>  <span data-ttu-id="cefcd-107">Merhaba güncelleştirmeleri başlık değişiklikleri toopassword değişikliklerden birçok biçimde olabilir.</span><span class="sxs-lookup"><span data-stu-id="cefcd-107">hello updates can take many forms, from title changes toopassword changes.</span></span>  

<span data-ttu-id="cefcd-108">Çözüm ve kullanıcı Hello kuruluşlar şirket içi kimlik gereksinimleri değerlendirerek başlatın.</span><span class="sxs-lookup"><span data-stu-id="cefcd-108">Start by evaluating hello organizations on-premises identity solution and user requirements.</span></span> <span data-ttu-id="cefcd-109">Bu değerlendirme nasıl kullanıcı kimlikleri oluşturulacak ve hello bulutta saklanır önemli toodefine hello teknik gereksinimleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="cefcd-109">This evaluation is important toodefine hello technical requirements for how user identities will be created and maintained in hello cloud.</span></span>  <span data-ttu-id="cefcd-110">Kuruluşların çoğunluğunun, şirket içi Active Directory verilir ve kullanıcılar tarafından olacak hello şirket içi dizin, ancak bazı durumlarda bu hello durumda olmayacaktır, eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="cefcd-110">For a majority of organizations, Active Directory is on-premises and will be hello on-premises directory that users will by synchronized from, however in some cases this will not be hello case.</span></span>  

<span data-ttu-id="cefcd-111">Aşağıdaki sorular emin tooanswer hello olun:</span><span class="sxs-lookup"><span data-stu-id="cefcd-111">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="cefcd-112">Bir AD ormanında, birden çok veya hiçbiri var mı?</span><span class="sxs-lookup"><span data-stu-id="cefcd-112">Do you have one AD forest, multiple, or none?</span></span>
  
  * <span data-ttu-id="cefcd-113">Kaç tane Azure AD dizinler için eşitleme?</span><span class="sxs-lookup"><span data-stu-id="cefcd-113">How many Azure AD directories will you be synchronizing to?</span></span>
    
    1. <span data-ttu-id="cefcd-114">Filtreleme kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="cefcd-114">Are you using filtering?</span></span>
    2. <span data-ttu-id="cefcd-115">Planlanan birden çok Azure AD Connect sunucuları var mı?</span><span class="sxs-lookup"><span data-stu-id="cefcd-115">Do you have multiple Azure AD Connect servers planned?</span></span>
* <span data-ttu-id="cefcd-116">Şu anda bir eşitleme elinizde aracı şirket içi?</span><span class="sxs-lookup"><span data-stu-id="cefcd-116">Do you currently have a synchronization tool on-premises?</span></span>
  
  * <span data-ttu-id="cefcd-117">Kullanıcıların kimliklerinin sanal bir dizin/tümleştirme varsa Evet ise, kullanıcılarınızın mu?</span><span class="sxs-lookup"><span data-stu-id="cefcd-117">If yes, does your users if users have a virtual directory/integration of identities?</span></span>
* <span data-ttu-id="cefcd-118">Tüm diğer dizin toosynchronize (örn. LDAP dizini, ik veritabanını, vb.) istediğiniz şirket içi var mı?</span><span class="sxs-lookup"><span data-stu-id="cefcd-118">Do you have any other directory on-premises that you want toosynchronize (e.g. LDAP Directory, HR database, etc)?</span></span>
  * <span data-ttu-id="cefcd-119">Tüm GALSync yapılması toobe mısınız?</span><span class="sxs-lookup"><span data-stu-id="cefcd-119">Are you going toobe doing any GALSync?</span></span>
  * <span data-ttu-id="cefcd-120">Merhaba geçerli durumunu UPN'ler kuruluşunuzdaki nedir?</span><span class="sxs-lookup"><span data-stu-id="cefcd-120">What is hello current state of UPNs in your organization?</span></span> 
  * <span data-ttu-id="cefcd-121">Kullanıcıların kimlik doğrulaması farklı bir dizin var mı?</span><span class="sxs-lookup"><span data-stu-id="cefcd-121">Do you have a different directory that users authenticate against?</span></span>
  * <span data-ttu-id="cefcd-122">Şirketiniz Microsoft Exchange kullanıyor mu?</span><span class="sxs-lookup"><span data-stu-id="cefcd-122">Does your company use Microsoft Exchange?</span></span>
    * <span data-ttu-id="cefcd-123">Bunlar, karma bir exchange dağıtım sahip planlıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="cefcd-123">Do they plan of having a hybrid exchange deployment?</span></span>

<span data-ttu-id="cefcd-124">Eşitleme gereksinimleri hakkında bir fikir sahip olduğunuza göre bu gereksinimleri hello doğru bir toomeet araçtır toodetermine gerekir.</span><span class="sxs-lookup"><span data-stu-id="cefcd-124">Now that you have an idea about your synchronization requirements, you need toodetermine which tool is hello correct one toomeet these requirements.</span></span>  <span data-ttu-id="cefcd-125">Microsoft, çeşitli araçlar tooaccomplish dizin tümleştirme ve eşitleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="cefcd-125">Microsoft provides several tools tooaccomplish directory integration and synchronization.</span></span>  <span data-ttu-id="cefcd-126">Merhaba bkz [karma kimlik dizini tümleştirme araçları karşılaştırması tablo](active-directory-hybrid-identity-design-considerations-tools-comparison.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="cefcd-126">See hello [Hybrid Identity directory integration tools comparison table](active-directory-hybrid-identity-design-considerations-tools-comparison.md) for more information.</span></span> 

<span data-ttu-id="cefcd-127">Eşitleme gereksinimlerini ve bu, şirketiniz için yapabiliriz hello aracı sahip olduğunuza göre bu dizin hizmetleri kullanan tooevaluate hello uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="cefcd-127">Now that you have your synchronization requirements and hello tool that will accomplish this for your company, you need tooevaluate hello applications that use these directory services.</span></span> <span data-ttu-id="cefcd-128">Bu değerlendirme toodefine hello teknik gereksinimleri toointegrate bu uygulamaları toohello bulut önemlidir.</span><span class="sxs-lookup"><span data-stu-id="cefcd-128">This evaluation is important toodefine hello technical requirements toointegrate these applications toohello cloud.</span></span> <span data-ttu-id="cefcd-129">Aşağıdaki sorular emin tooanswer hello olun:</span><span class="sxs-lookup"><span data-stu-id="cefcd-129">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="cefcd-130">Bu uygulamalar taşınan toohello olur Bulut ve hello dizini kullanmak?</span><span class="sxs-lookup"><span data-stu-id="cefcd-130">Will these applications be moved toohello cloud and use hello directory?</span></span>
* <span data-ttu-id="cefcd-131">Bu uygulamalar başarıyla kullanabilmeniz için eşitlenen toobe toohello bulut gereken özel öznitelikler var mı?</span><span class="sxs-lookup"><span data-stu-id="cefcd-131">Are there special attributes that need toobe synchronized toohello cloud so these applications can use them successfully?</span></span>
* <span data-ttu-id="cefcd-132">Bu uygulamalar, bulut kimlik doğrulama tootake avantajlarından yeniden yazılmış toobe gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="cefcd-132">Will these applications need toobe re-written tootake advantage of cloud auth?</span></span>
* <span data-ttu-id="cefcd-133">Kullanıcıların erişmesine karşın bu uygulamaları içi toolive devam edecek hello bulut kimliği kullanarak?</span><span class="sxs-lookup"><span data-stu-id="cefcd-133">Will these applications continue toolive on-premises while users access them using hello cloud identity?</span></span>

<span data-ttu-id="cefcd-134">Ayrıca toodetermine hello güvenlik gereksinimleri ve kısıtlamaları dizin eşitlemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="cefcd-134">You also need toodetermine hello security requirements and constraints directory synchronization.</span></span> <span data-ttu-id="cefcd-135">Bu değerlendirme önemli tooget bir sipariş toocreate gerekli olacağını ve kullanıcının kimlikleri hello bulutta korumak hello gereksinimleri listesi olur.</span><span class="sxs-lookup"><span data-stu-id="cefcd-135">This evaluation is important tooget a list of hello requirements that will be needed in order toocreate and maintain user’s identities in hello cloud.</span></span> <span data-ttu-id="cefcd-136">Aşağıdaki sorular emin tooanswer hello olun:</span><span class="sxs-lookup"><span data-stu-id="cefcd-136">Make sure tooanswer hello following questions:</span></span>

* <span data-ttu-id="cefcd-137">Burada hello eşitleme sunucusu bulunur?</span><span class="sxs-lookup"><span data-stu-id="cefcd-137">Where will hello synchronization server be located?</span></span>
* <span data-ttu-id="cefcd-138">Etki alanına katılmış olacak?</span><span class="sxs-lookup"><span data-stu-id="cefcd-138">Will it be domain joined?</span></span>
* <span data-ttu-id="cefcd-139">Merhaba sunucu kısıtlanmış bir ağda DMZ gibi bir güvenlik duvarının arkasında bulunan?</span><span class="sxs-lookup"><span data-stu-id="cefcd-139">Will hello server be located on a restricted network behind a firewall, such as a DMZ?</span></span>
  * <span data-ttu-id="cefcd-140">Mümkün tooopen hello gerekli güvenlik duvarı bağlantı noktaları toosupport eşitleme olacak?</span><span class="sxs-lookup"><span data-stu-id="cefcd-140">Will you be able tooopen hello required firewall ports toosupport synchronization?</span></span>
* <span data-ttu-id="cefcd-141">Merhaba eşitleme sunucusu için bir olağanüstü durum kurtarma planı var mı?</span><span class="sxs-lookup"><span data-stu-id="cefcd-141">Do you have a disaster recovery plan for hello synchronization server?</span></span>
* <span data-ttu-id="cefcd-142">Merhaba toosynch ile istediğiniz tüm orman için doğru izinlere sahip bir hesap var mı?</span><span class="sxs-lookup"><span data-stu-id="cefcd-142">Do you have an account with hello correct permissions for all forests you want toosynch with?</span></span>
  * <span data-ttu-id="cefcd-143">Şirketiniz Bu soru için hello yanıt bilmiyor hello makale "Parola Eşitleme izinlerini" bölümünde hello inceleyin [yükleme hello Azure Active Directory eşitleme hizmeti](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) ve zaten olup olmadığını belirlemek bir Bu izinlere sahip olan hesabı veya bir toocreate ihtiyacınız varsa.</span><span class="sxs-lookup"><span data-stu-id="cefcd-143">If your company doesn’t know hello answer for this question, review hello section “Permissions for password synchronization” in hello article [Install hello Azure Active Directory Sync Service](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) and determine if you already have an account with these permissions or if you need toocreate one.</span></span>
* <span data-ttu-id="cefcd-144">Varsa belirleyebiliriz orman eşitleme hello eşitleme sunucusu mümkün tooget tooeach orman mı?</span><span class="sxs-lookup"><span data-stu-id="cefcd-144">If you have mutli-forest sync is hello sync server able tooget tooeach forest?</span></span>

> [!NOTE]
> <span data-ttu-id="cefcd-145">Her yanıtı tootake Not emin olun ve hello yanıtın hello yanıt arkasındaki mantığı anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cefcd-145">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="cefcd-146">[Olay yanıtlama gereksinimlerini belirlemek](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) hello seçeneklerin geçilir.</span><span class="sxs-lookup"><span data-stu-id="cefcd-146">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over hello options available.</span></span> <span data-ttu-id="cefcd-147">Seçeneği, iş gereksinimlerinize en uygun belirleyeceksiniz bu soruları yanıtladığınızda gerekir.</span><span class="sxs-lookup"><span data-stu-id="cefcd-147">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="cefcd-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cefcd-148">Next steps</span></span>
[<span data-ttu-id="cefcd-149">Çok faktörlü kimlik doğrulama gereksinimlerini belirleyin</span><span class="sxs-lookup"><span data-stu-id="cefcd-149">Determine multi-factor authentication requirements</span></span>](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a><span data-ttu-id="cefcd-150">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="cefcd-150">See also</span></span>
[<span data-ttu-id="cefcd-151">Tasarım konularına genel bakış</span><span class="sxs-lookup"><span data-stu-id="cefcd-151">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

