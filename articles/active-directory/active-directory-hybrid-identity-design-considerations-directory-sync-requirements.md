---
title: "Azure Active Directory karma kimlik tasarımı hakkında dikkat edilecek noktalar - dizin eşitleme gereksinimlerini belirleme | Microsoft Docs"
description: "Hangi gereksinimler tüm kullanıcılar arasında eşitlemek için gerekli olan tanımlamak şirket içi ve bulut kuruluş için on =."
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
ms.openlocfilehash: 5ef87e606f055359ca325befd6048353ce57ca2b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="determine-directory-synchronization-requirements"></a><span data-ttu-id="3ca2f-103">Dizin eşitleme gereksinimlerini belirleyin</span><span class="sxs-lookup"><span data-stu-id="3ca2f-103">Determine directory synchronization requirements</span></span>
<span data-ttu-id="3ca2f-104">Eşitleme, kullanıcıların kendi şirket içi kimliğine göre bulutta bir kimlik sağlama tüm hakkında olur.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-104">Synchronization is all about providing users an identity in the cloud based on their on-premises identity.</span></span> <span data-ttu-id="3ca2f-105">Kimlik doğrulaması veya şirket dışı kimlik doğrulaması için eşitlenmiş hesap kullanacakları olup olmadığına bakılmaksızın, kullanıcıların hala bulutta bir kimliğe sahip gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-105">Whether or not they will use synchronized account for authentication or federated authentication, the users will still need to have an identity in the cloud.</span></span>  <span data-ttu-id="3ca2f-106">Bu kimlik korunur ve düzenli aralıklarla güncelleştirilen gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-106">This identity will need to be maintained and updated periodically.</span></span>  <span data-ttu-id="3ca2f-107">Güncelleştirmeleri başlık değişikliklerden parola değişiklikleri için birçok biçimde olabilir.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-107">The updates can take many forms, from title changes to password changes.</span></span>  

<span data-ttu-id="3ca2f-108">Kuruluşlar şirket içi kimlik çözümü ve kullanıcı gereksinimleri değerlendirerek başlatın.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-108">Start by evaluating the organizations on-premises identity solution and user requirements.</span></span> <span data-ttu-id="3ca2f-109">Bu değerlendirme nasıl kullanıcı kimlikleri oluşturulacak ve bulutta saklanır teknik gereksinimlerini tanımlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-109">This evaluation is important to define the technical requirements for how user identities will be created and maintained in the cloud.</span></span>  <span data-ttu-id="3ca2f-110">Kuruluşların çoğunluğunun, şirket içi Active Directory verilir ve kullanıcılar tarafından olacak şirket içi dizin, ancak bazı durumlarda bu durumda olmayacaktır, eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-110">For a majority of organizations, Active Directory is on-premises and will be the on-premises directory that users will by synchronized from, however in some cases this will not be the case.</span></span>  

<span data-ttu-id="3ca2f-111">Aşağıdaki soruları yanıtlayın emin olun:</span><span class="sxs-lookup"><span data-stu-id="3ca2f-111">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="3ca2f-112">Bir AD ormanında, birden çok veya hiçbiri var mı?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-112">Do you have one AD forest, multiple, or none?</span></span>
  
  * <span data-ttu-id="3ca2f-113">Kaç tane Azure AD dizinler için eşitleme?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-113">How many Azure AD directories will you be synchronizing to?</span></span>
    
    1. <span data-ttu-id="3ca2f-114">Filtreleme kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-114">Are you using filtering?</span></span>
    2. <span data-ttu-id="3ca2f-115">Planlanan birden çok Azure AD Connect sunucuları var mı?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-115">Do you have multiple Azure AD Connect servers planned?</span></span>
* <span data-ttu-id="3ca2f-116">Şu anda bir eşitleme elinizde aracı şirket içi?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-116">Do you currently have a synchronization tool on-premises?</span></span>
  
  * <span data-ttu-id="3ca2f-117">Kullanıcıların kimliklerinin sanal bir dizin/tümleştirme varsa Evet ise, kullanıcılarınızın mu?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-117">If yes, does your users if users have a virtual directory/integration of identities?</span></span>
* <span data-ttu-id="3ca2f-118">Tüm diğer dizin (örn. LDAP dizini, ik veritabanını, vb.) eşitlemek istediğiniz şirket içi var mı?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-118">Do you have any other directory on-premises that you want to synchronize (e.g. LDAP Directory, HR database, etc)?</span></span>
  * <span data-ttu-id="3ca2f-119">Tüm GALSync yaparak mısınız?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-119">Are you going to be doing any GALSync?</span></span>
  * <span data-ttu-id="3ca2f-120">UPN'ler geçerli durumu, kuruluşunuzda nedir?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-120">What is the current state of UPNs in your organization?</span></span> 
  * <span data-ttu-id="3ca2f-121">Kullanıcıların kimlik doğrulaması farklı bir dizin var mı?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-121">Do you have a different directory that users authenticate against?</span></span>
  * <span data-ttu-id="3ca2f-122">Şirketiniz Microsoft Exchange kullanıyor mu?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-122">Does your company use Microsoft Exchange?</span></span>
    * <span data-ttu-id="3ca2f-123">Bunlar, karma bir exchange dağıtım sahip planlıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-123">Do they plan of having a hybrid exchange deployment?</span></span>

<span data-ttu-id="3ca2f-124">Eşitleme gereksinimleri hakkında bir fikir sahip olduğunuza göre bu gereksinimleri karşılamak için doğru bir araçtır belirlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-124">Now that you have an idea about your synchronization requirements, you need to determine which tool is the correct one to meet these requirements.</span></span>  <span data-ttu-id="3ca2f-125">Microsoft directory tümleştirme ve eşitleme gerçekleştirmek için çeşitli araçlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-125">Microsoft provides several tools to accomplish directory integration and synchronization.</span></span>  <span data-ttu-id="3ca2f-126">Bkz: [karma kimlik dizini tümleştirme araçları karşılaştırması tablo](active-directory-hybrid-identity-design-considerations-tools-comparison.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-126">See the [Hybrid Identity directory integration tools comparison table](active-directory-hybrid-identity-design-considerations-tools-comparison.md) for more information.</span></span> 

<span data-ttu-id="3ca2f-127">Eşitleme gereksinimlerinizi ve bu, şirketiniz için yapabiliriz aracı sahip olduğunuza göre bu dizin hizmetleri kullanan uygulamalar değerlendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-127">Now that you have your synchronization requirements and the tool that will accomplish this for your company, you need to evaluate the applications that use these directory services.</span></span> <span data-ttu-id="3ca2f-128">Bu değerlendirme, bulut için bu uygulamaları tümleştirmek için teknik gereksinimleri tanımlamak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-128">This evaluation is important to define the technical requirements to integrate these applications to the cloud.</span></span> <span data-ttu-id="3ca2f-129">Aşağıdaki soruları yanıtlayın emin olun:</span><span class="sxs-lookup"><span data-stu-id="3ca2f-129">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="3ca2f-130">Bu uygulamalar buluta taşınır ve dizini kullanın?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-130">Will these applications be moved to the cloud and use the directory?</span></span>
* <span data-ttu-id="3ca2f-131">Bu uygulamalar başarıyla kullanabilmeniz için bulut için eşitlenmesi gereken özel öznitelikler var mı?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-131">Are there special attributes that need to be synchronized to the cloud so these applications can use them successfully?</span></span>
* <span data-ttu-id="3ca2f-132">Bu uygulamalar, bulut kimlik doğrulama yararlanmak için yeniden yazılması gerekecek mi?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-132">Will these applications need to be re-written to take advantage of cloud auth?</span></span>
* <span data-ttu-id="3ca2f-133">Bu uygulamaları kullanıcıların bulut kimliği kullanarak bunları erişirken şirket içi Canlı devam eder?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-133">Will these applications continue to live on-premises while users access them using the cloud identity?</span></span>

<span data-ttu-id="3ca2f-134">Ayrıca, güvenlik gereksinimleri ve kısıtlamaları dizin eşitleme belirlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-134">You also need to determine the security requirements and constraints directory synchronization.</span></span> <span data-ttu-id="3ca2f-135">Bu değerlendirme oluşturmak ve kullanıcının kimlikleri bulutta korumak için gerekli olan gereksinimleri listesini almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-135">This evaluation is important to get a list of the requirements that will be needed in order to create and maintain user’s identities in the cloud.</span></span> <span data-ttu-id="3ca2f-136">Aşağıdaki soruları yanıtlayın emin olun:</span><span class="sxs-lookup"><span data-stu-id="3ca2f-136">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="3ca2f-137">Burada eşitleme sunucusu bulunur?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-137">Where will the synchronization server be located?</span></span>
* <span data-ttu-id="3ca2f-138">Etki alanına katılmış olacak?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-138">Will it be domain joined?</span></span>
* <span data-ttu-id="3ca2f-139">Sunucu, kısıtlanmış bir ağda DMZ gibi bir güvenlik duvarının arkasında bulunur?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-139">Will the server be located on a restricted network behind a firewall, such as a DMZ?</span></span>
  * <span data-ttu-id="3ca2f-140">Eşitlemeyi desteklemek için gerekli güvenlik duvarı bağlantı noktalarını açmak erişebilecek mi?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-140">Will you be able to open the required firewall ports to support synchronization?</span></span>
* <span data-ttu-id="3ca2f-141">Eşitleme sunucusu için bir olağanüstü durum kurtarma planı var mı?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-141">Do you have a disaster recovery plan for the synchronization server?</span></span>
* <span data-ttu-id="3ca2f-142">İle eşitleme yapmak istediğiniz tüm orman için doğru izinlere sahip bir hesaba var mı?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-142">Do you have an account with the correct permissions for all forests you want to synch with?</span></span>
  * <span data-ttu-id="3ca2f-143">Şirketiniz bu soruya yanıt bilmiyor makaleyi "Parola Eşitleme izinlerini" bölümünde inceleyin [Azure Active Directory Eşitleme Hizmeti'ni yükleme](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) ve bir hesap zaten yüklü olup olmadığını belirleme Bu izinlere sahip olan veya oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-143">If your company doesn’t know the answer for this question, review the section “Permissions for password synchronization” in the article [Install the Azure Active Directory Sync Service](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) and determine if you already have an account with these permissions or if you need to create one.</span></span>
* <span data-ttu-id="3ca2f-144">Varsa belirleyebiliriz orman eşitleme eşitleme sunucusu her orman için almak mi?</span><span class="sxs-lookup"><span data-stu-id="3ca2f-144">If you have mutli-forest sync is the sync server able to get to each forest?</span></span>

> [!NOTE]
> <span data-ttu-id="3ca2f-145">Her yanıtı not alın ve yanıtın yanıtın arkasındaki mantığı anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-145">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="3ca2f-146">[Olay yanıtlama gereksinimlerini belirlemek](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) seçeneklerin geçilir.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-146">[Determine incident response requirements](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) will go over the options available.</span></span> <span data-ttu-id="3ca2f-147">Seçeneği, iş gereksinimlerinize en uygun belirleyeceksiniz bu soruları yanıtladığınızda gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-147">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3ca2f-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3ca2f-148">Next steps</span></span>
[<span data-ttu-id="3ca2f-149">Çok faktörlü kimlik doğrulama gereksinimlerini belirleyin</span><span class="sxs-lookup"><span data-stu-id="3ca2f-149">Determine multi-factor authentication requirements</span></span>](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a><span data-ttu-id="3ca2f-150">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="3ca2f-150">See also</span></span>
[<span data-ttu-id="3ca2f-151">Tasarım konularına genel bakış</span><span class="sxs-lookup"><span data-stu-id="3ca2f-151">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

