---
title: aaaAzure Active Directory ile ilgili SSS | Microsoft Docs
description: "Azure Active Directory ile ilgili SSS tooaccess Azure ve Azure Active Directory, parola yönetimi ve uygulama nasıl erişim sorular yanıtlanmaktadır."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 63c30c4aeda4551bf02c6b968f98cded5a3b2c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-faq"></a><span data-ttu-id="7127e-103">Azure Active Directory ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="7127e-103">Azure Active Directory FAQ</span></span>
<span data-ttu-id="7127e-104">Azure Active Directory (Azure AD), kimlik, erişim yönetimi ve güvenliği tüm yönleriyle kapsayan bir hizmet olarak kimlik (IDaaS) çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="7127e-104">Azure Active Directory (Azure AD) is a comprehensive identity as a service (IDaaS) solution that spans all aspects of identity, access management, and security.</span></span>

<span data-ttu-id="7127e-105">Daha fazla bilgi için bkz. [Azure Active Directory nedir?](active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7127e-105">For more information, see [What is Azure Active Directory?](active-directory-whatis.md).</span></span>


## <a name="access-azure-and-azure-active-directory"></a><span data-ttu-id="7127e-106">Azure ve Azure Active Directory erişimi</span><span class="sxs-lookup"><span data-stu-id="7127e-106">Access Azure and Azure Active Directory</span></span>
<span data-ttu-id="7127e-107">**Merhaba Klasik Azure portalı, Azure AD tooaccess çalıştığımda neden "abonelik bulunamadı" sağlarım?**</span><span class="sxs-lookup"><span data-stu-id="7127e-107">**Q: Why do I get “No subscriptions found” when I try tooaccess Azure AD in hello Azure classic portal?**</span></span>

<span data-ttu-id="7127e-108">**Y:** tooaccess Merhaba Klasik Azure portalı, her bir kullanıcı Azure aboneliği ile izinleri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7127e-108">**A:** tooaccess hello Azure classic portal, each user needs permissions with an Azure subscription.</span></span> <span data-ttu-id="7127e-109">Ücretli bir Azure AD ve Office 365 aboneliği varsa, çok gidin[http://aka.ms/accessAAD](http://aka.ms/accessAAD) bir kerelik etkinleştirme adımı için.</span><span class="sxs-lookup"><span data-stu-id="7127e-109">If you have a paid Office 365 or Azure AD subscription, go too[http://aka.ms/accessAAD](http://aka.ms/accessAAD) for a one-time activation step.</span></span> <span data-ttu-id="7127e-110">Aksi durumda, tooactivate ücretsiz gerekir [Azure hesabı](https://azure.microsoft.com/pricing/free-trial/) veya Ücretli abonelik.</span><span class="sxs-lookup"><span data-stu-id="7127e-110">Otherwise, you will need tooactivate a free [Azure account](https://azure.microsoft.com/pricing/free-trial/) or a paid subscription.</span></span>

<span data-ttu-id="7127e-111">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="7127e-111">For more information, see:</span></span>

* [<span data-ttu-id="7127e-112">Azure aboneliklerinin Azure Active Directory ile ilişkisi</span><span class="sxs-lookup"><span data-stu-id="7127e-112">How Azure subscriptions are associated with Azure Active Directory</span></span>](active-directory-how-subscriptions-associated-directory.md)
* [<span data-ttu-id="7127e-113">Azure'da Office 365 aboneliğinize Hello dizini yönetme</span><span class="sxs-lookup"><span data-stu-id="7127e-113">Manage hello directory for your Office 365 subscription in Azure</span></span>](active-directory-manage-o365-subscription.md)

- - -
<span data-ttu-id="7127e-114">**S: Azure AD arasındaki hello ilişki nedir Office 365 ve Azure?**</span><span class="sxs-lookup"><span data-stu-id="7127e-114">**Q: What’s hello relationship between Azure AD, Office 365, and Azure?**</span></span>

<span data-ttu-id="7127e-115">**Y:** Azure AD, ortak kimlik ve erişim yetenekleri ile tooall web hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="7127e-115">**A:** Azure AD provides you with common identity and access capabilities tooall web services.</span></span> <span data-ttu-id="7127e-116">Office 365, Microsoft Azure, Intune veya diğer, size, kullanıp kullanmadığınızı olduğunuz zaten Azure AD toohelp kullanarak aç Bu hizmetler için oturum açma ve erişim yönetimi.</span><span class="sxs-lookup"><span data-stu-id="7127e-116">Whether you are using Office 365, Microsoft Azure, Intune, or others, you're already using Azure AD toohelp turn on sign-on and access management for all these services.</span></span>

<span data-ttu-id="7127e-117">Toouse web hizmetlerini ayarlama tüm kullanıcılar, bir veya daha fazla Azure AD örneğinde kullanıcı hesapları olarak tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="7127e-117">All users who are set up toouse web services are defined as user accounts in one or more Azure AD instances.</span></span> <span data-ttu-id="7127e-118">Bulut uygulama erişimi gibi ücretsiz Azure AD özellikleri için bu hesapları ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7127e-118">You can set up these accounts for free Azure AD capabilities like cloud application access.</span></span>

<span data-ttu-id="7127e-119">Enterprise Mobility + Security gibi ücretli Azure AD hizmetleri, kurumsal ölçekte kapsamlı yönetim ve güvenlik çözümleriyle Office 365 ve Microsoft Azure gibi diğer web hizmetlerini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="7127e-119">Azure AD paid services like Enterprise Mobility + Security complement other web services like Office 365 and Microsoft Azure with comprehensive enterprise-scale management and security solutions.</span></span>
- - -
<span data-ttu-id="7127e-120">**Neden ı toohello Azure portalında oturum ancak klasik Azure portalı hello değil mi?**</span><span class="sxs-lookup"><span data-stu-id="7127e-120">**Q:  Why can I sign in toohello Azure portal but not hello Azure classic portal?**</span></span>

<span data-ttu-id="7127e-121">**Y:** hello Azure portal geçerli bir abonelik gerektirmez ve hello Klasik portal geçerli bir abonelik gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7127e-121">**A:**  hello Azure portal does not require a valid subscription, and hello classic portal does require a valid subscription.</span></span>  <span data-ttu-id="7127e-122">Bir abonelik yoksa da toohello Klasik Portalı'nda oturum açamazsınız.</span><span class="sxs-lookup"><span data-stu-id="7127e-122">If you do not have a subscription, you can't sign in toohello classic portal.</span></span>
- - -
<span data-ttu-id="7127e-123">**S: hello farklarını Abonelik Yöneticisi ve dizin Yöneticisi nelerdir?**</span><span class="sxs-lookup"><span data-stu-id="7127e-123">**Q:  What are hello differences between Subscription Administrator and Directory Administrator?**</span></span>

<span data-ttu-id="7127e-124">**Y:** varsayılan olarak, Azure için kaydolduğunuzda hello Abonelik Yöneticisi rolü atanır.</span><span class="sxs-lookup"><span data-stu-id="7127e-124">**A:** By default, you are assigned hello Subscription Administrator role when you sign up for Azure.</span></span> <span data-ttu-id="7127e-125">Abonelik Yöneticisi bir Microsoft hesabı ya da bir iş kullanabilir veya Okul hesabı Azure aboneliği hello hello dizininden ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="7127e-125">A subscription admin can use either a Microsoft account or a work or school account from hello directory that hello Azure subscription is associated with.</span></span>  <span data-ttu-id="7127e-126">Bu rol hello Azure portal yetkili toomanage Hizmetleri'nde değildir.</span><span class="sxs-lookup"><span data-stu-id="7127e-126">This role is authorized toomanage services in hello Azure portal.</span></span>

<span data-ttu-id="7127e-127">Diğerleri de toosign gerekir ve Hizmetleri tarafından erişirseniz, Merhaba aynı aboneliği kullanarak, ortak yöneticileri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7127e-127">If others need toosign in and access services by using hello same subscription, you can add them as co-admins.</span></span> <span data-ttu-id="7127e-128">Bu rol hello sahip aynı erişim ayrıcalıkları hello Hizmet Yöneticisi, ancak abonelikleri tooAzure dizinleri hello ilişkisini değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="7127e-128">This role has hello same access privileges as hello service admin, but can’t change hello association of subscriptions tooAzure directories.</span></span>  <span data-ttu-id="7127e-129">Abonelik yöneticileri hakkında ek bilgi için bkz: [nasıl tooadd ya da değişiklik Azure yönetici rolleri](../billing-add-change-azure-subscription-administrator.md) ve [Azure aboneliklerinin Azure Active Directory ile ilişkili](active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="7127e-129">For additional information on subscription admins, see [How tooadd or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) and [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span></span>


<span data-ttu-id="7127e-130">Azure AD'de yönetici rolleri toomanage hello dizin ve kimlik güvenlikle ilgili özellikler farklı kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="7127e-130">Azure AD has a different set of admin roles toomanage hello directory and identity-related features.</span></span>  <span data-ttu-id="7127e-131">Bu yöneticileri erişim toovarious özelliğiniz hello Azure portalında veya Klasik Azure portalı hello.</span><span class="sxs-lookup"><span data-stu-id="7127e-131">These admins will have access toovarious features in hello Azure portal or hello Azure classic portal.</span></span> <span data-ttu-id="7127e-132">Hello Yöneticisi'nin rol, oluşturmak veya kullanıcıları Düzenle, yönetici rollerini tooothers ata, kullanıcı parolalarını sıfırlama, kullanıcı lisanslarını yönetme veya etki alanlarını yönetme gibi yapabileceklerini belirler.</span><span class="sxs-lookup"><span data-stu-id="7127e-132">hello admin's role determines what they can do, like create or edit users, assign administrative roles tooothers, reset user passwords, manage user licenses, or manage domains.</span></span>  <span data-ttu-id="7127e-133">Azure AD dizin yöneticileri ve rolleri hakkında daha fazla bilgi için bkz. [Azure Active Directory’de yönetici rolü atama](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="7127e-133">For additional information on Azure AD directory admins and their roles, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="7127e-134">Ayrıca, Enterprise Mobility + Security gibi ücretli Azure AD hizmetleri, kurumsal ölçekte kapsamlı yönetim ve güvenlik çözümleriyle Office 365 ve Microsoft Azure gibi diğer web hizmetlerini tamamlar.</span><span class="sxs-lookup"><span data-stu-id="7127e-134">Additionally, Azure AD paid services like Enterprise Mobility + Security complement other web services, such as Office 365 and Microsoft Azure, with comprehensive enterprise-scale management and security solutions.</span></span>

- - -
<span data-ttu-id="7127e-135">**S: Azure AD kullanıcı lisanslarımın ne zaman sona ereceğini gösteren bir rapor var mı?**</span><span class="sxs-lookup"><span data-stu-id="7127e-135">**Q: Is there a report that shows when my Azure AD user licenses will expire?**</span></span>

<span data-ttu-id="7127e-136">**C:** Hayır.</span><span class="sxs-lookup"><span data-stu-id="7127e-136">**A:** No.</span></span>  <span data-ttu-id="7127e-137">Bu özellik şu an kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="7127e-137">This is not currently available.</span></span>

- - -

## <a name="get-started-with-hybrid-azure-ad"></a><span data-ttu-id="7127e-138">Karma Azure AD ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="7127e-138">Get started with Hybrid Azure AD</span></span>


<span data-ttu-id="7127e-139">**S: Ortak çalışan olarak eklendiğimde kiracıdan nasıl ayrılabilirim?**</span><span class="sxs-lookup"><span data-stu-id="7127e-139">**Q: How do I leave a tenant when I am added as a collaborator?**</span></span>

<span data-ttu-id="7127e-140">**Y:** tooanother kuruluşunuzun Kiracı ortak çalışanı eklendiğinde, hello "Kiracı değiştirici" Merhaba üst sağ tooswitch, kiracılar arasında kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7127e-140">**A:** When you are added tooanother organization's tenant as a collaborator, you can use hello "tenant switcher" in hello upper right tooswitch between tenants.</span></span>  <span data-ttu-id="7127e-141">Şu anda, kuruluş davet hiçbir şekilde tooleave hello yoktur ve Microsoft bu işlevselliği sağlayan üzerinde çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7127e-141">Currently, there is no way tooleave hello inviting organization, and Microsoft is working on providing this functionality.</span></span>  <span data-ttu-id="7127e-142">Bu özellik kullanılabilir oluncaya kadar kuruluş tooremove davet hello sorabileceğiniz kendi Kiracı sizden.</span><span class="sxs-lookup"><span data-stu-id="7127e-142">Until this feature is available, you can ask hello inviting organization tooremove you from their tenant.</span></span>
- - -
<span data-ttu-id="7127e-143">**S: my şirket içi dizin tooAzure AD nasıl bağlanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="7127e-143">**Q: How can I connect my on-premises directory tooAzure AD?**</span></span>

<span data-ttu-id="7127e-144">**Y:** Azure AD Connect kullanarak şirket içi dizin tooAzure AD bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7127e-144">**A:** You can connect your on-premises directory tooAzure AD by using Azure AD Connect.</span></span>

<span data-ttu-id="7127e-145">Daha fazla bilgi için bkz. [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="7127e-145">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="7127e-146">**S: Şirket içi dizinim ve bulut uygulamalarım arasında SSO'yu nasıl ayarlarım?**</span><span class="sxs-lookup"><span data-stu-id="7127e-146">**Q: How do I set up SSO between my on-premises directory and my cloud applications?**</span></span>

<span data-ttu-id="7127e-147">**Y:** çoklu oturum açma (SSO) şirket içi dizin ve Azure AD arasındaki yukarı tooset yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="7127e-147">**A:** You only need tooset up single sign-on (SSO) between your on-premises directory and Azure AD.</span></span> <span data-ttu-id="7127e-148">Bulut uygulamalarınıza Azure AD üzerinden eriştiğiniz sürece hello hizmet toocorrectly kendi şirket içi kimlik bilgileriyle kimlik doğrulaması, kullanıcıların otomatik olarak yürütür.</span><span class="sxs-lookup"><span data-stu-id="7127e-148">As long as you access your cloud applications through Azure AD, hello service automatically drives your users toocorrectly authenticate with their on-premises credentials.</span></span>

<span data-ttu-id="7127e-149">Şirket içi konumdan SSO uygulama işlemi, Active Directory Federation Services (ADFS) gibi federasyon çözümleri veya parola karma eşitlemesini yapılandırma işlemi ile kolayca gerçekleştirilebilir. Hello Azure AD Connect yapılandırma sihirbazını kullanarak her iki seçeneği de kolayca dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7127e-149">Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using hello Azure AD Connect configuration wizard.</span></span>

<span data-ttu-id="7127e-150">Daha fazla bilgi için bkz. [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="7127e-150">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="7127e-151">**S: Azure AD, kuruluşumdaki kullanıcılar için bir self servis portal sağlar mı?**</span><span class="sxs-lookup"><span data-stu-id="7127e-151">**Q: Does Azure AD provide a self-service portal for users in my organization?**</span></span>

<span data-ttu-id="7127e-152">**Y:** Evet, Azure AD, ile Merhaba sağlar [Azure AD erişim paneli](http://myapps.microsoft.com) kullanıcı Self Servis ve uygulama erişimi.</span><span class="sxs-lookup"><span data-stu-id="7127e-152">**A:** Yes, Azure AD provides you with hello [Azure AD Access Panel](http://myapps.microsoft.com) for user self-service and application access.</span></span> <span data-ttu-id="7127e-153">Bir Office 365 müşterisiyseniz, birçok hello aynı yetenekleri hello Office 365 Portalı'nda bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7127e-153">If you are an Office 365 customer, you can find many of hello same capabilities in hello Office 365 portal.</span></span>

<span data-ttu-id="7127e-154">Daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7127e-154">For more information, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

- - -
<span data-ttu-id="7127e-155">**S: Azure AD, şirket içi altyapımı yönetmeme yardımcı olur mu?**</span><span class="sxs-lookup"><span data-stu-id="7127e-155">**Q: Does Azure AD help me manage my on-premises infrastructure?**</span></span>

<span data-ttu-id="7127e-156">**Y:** Evet.</span><span class="sxs-lookup"><span data-stu-id="7127e-156">**A:** Yes.</span></span> <span data-ttu-id="7127e-157">Hello Azure AD Premium edition Azure AD Connect Health ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="7127e-157">hello Azure AD Premium edition provides you with Azure AD Connect Health.</span></span> <span data-ttu-id="7127e-158">Azure AD Connect Health, izleme ve altyapı ve hello Eşitleme Hizmetleri, şirket içi kimlik kavramanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7127e-158">Azure AD Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and hello synchronization services.</span></span>  

<span data-ttu-id="7127e-159">Daha fazla bilgi için bkz: [hello bulutta, şirket içi kimlik altyapınızı ve Eşitleme hizmetlerini izlemek](active-directory-aadconnect-health.md).</span><span class="sxs-lookup"><span data-stu-id="7127e-159">For more information, see [Monitor your on-premises identity infrastructure and synchronization services in hello cloud](active-directory-aadconnect-health.md).</span></span>  

- - -
## <a name="password-management"></a><span data-ttu-id="7127e-160">Parola yönetimi</span><span class="sxs-lookup"><span data-stu-id="7127e-160">Password management</span></span>
<span data-ttu-id="7127e-161">**S: Azure AD parola geri yazma özelliğini parola eşitleme olmadan kullanabilir miyim? (Bu senaryoda, olası toouse Azure AD Self Servis parola sıfırlama (SSPR) parola geri yazma ve değil deposu parolaları hello bulutta olduğu?)**</span><span class="sxs-lookup"><span data-stu-id="7127e-161">**Q: Can I use Azure AD password write-back without password sync? (In this scenario, is it possible toouse Azure AD self-service password reset (SSPR) with password write-back and not store passwords in hello cloud?)**</span></span>

<span data-ttu-id="7127e-162">**Y:** , Active Directory parolaları tooAzure AD tooenable sonradan yazma toosynchronize gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7127e-162">**A:** You do not need toosynchronize your Active Directory passwords tooAzure AD tooenable write-back.</span></span> <span data-ttu-id="7127e-163">Federasyon ortamında, Azure AD çoklu oturum açma (SSO) hello şirket içi dizin tooauthenticate hello kullanıcı kullanır.</span><span class="sxs-lookup"><span data-stu-id="7127e-163">In a federated environment, Azure AD single sign-on (SSO) relies on hello on-premises directory tooauthenticate hello user.</span></span> <span data-ttu-id="7127e-164">Bu senaryo, Azure AD'de izlenen hello şirket içi parola toobe gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="7127e-164">This scenario does not require hello on-premises password toobe tracked in Azure AD.</span></span>

- - -
<span data-ttu-id="7127e-165">**S: ne kadar süreyle tooActive şirket içi dizin geri yazılmış bir parola toobe için sürer?**</span><span class="sxs-lookup"><span data-stu-id="7127e-165">**Q: How long does it take for a password toobe written back tooActive Directory on-premises?**</span></span>

<span data-ttu-id="7127e-166">**Y:** Parola geri yazma işlemi gerçek zamanlı olarak gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="7127e-166">**A:** Password write-back operates in real time.</span></span>

<span data-ttu-id="7127e-167">Daha fazla bilgi için bkz. [Parola yönetimine başlarken](active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="7127e-167">For more information, see [Getting started with password management](active-directory-passwords-getting-started.md).</span></span>

- - -
<span data-ttu-id="7127e-168">**S: Parola geri yazma özelliğini bir yönetici tarafından yönetilen parolalarla kullanabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="7127e-168">**Q: Can I use password write-back with passwords that are managed by an admin?**</span></span>

<span data-ttu-id="7127e-169">**Y:** parola geri yazma özelliğini etkinleştirdiyseniz varsa, Evet, bir yönetici tarafından gerçekleştirilen parola işlemleri hello geri tooyour şirket içi ortamına yazılır.</span><span class="sxs-lookup"><span data-stu-id="7127e-169">**A:** Yes, if you have password write-back enabled, hello password operations performed by an admin are written back tooyour on-premises environment.</span></span>  

<span data-ttu-id="7127e-170">Toopassword ilgili sorular ve yanıtları için bkz [parola yönetimi sık sorulan sorular](active-directory-passwords-faq.md).</span><span class="sxs-lookup"><span data-stu-id="7127e-170">For more answers toopassword-related questions, see [Password management frequently asked questions](active-directory-passwords-faq.md).</span></span>
- - -
<span data-ttu-id="7127e-171">**S: ı mevcut Office 365/Azure AD parolamı parolamı toochange çalışırken anımsamıyorsanız ne yapabilirim?**</span><span class="sxs-lookup"><span data-stu-id="7127e-171">**Q:  What can I do if I can't remember my existing Office 365/Azure AD password while trying toochange my password?**</span></span>

<span data-ttu-id="7127e-172">**Y:** Bu tür bir durum için birkaç seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="7127e-172">**A:** For this type of situation, there are a couple of options.</span></span>  <span data-ttu-id="7127e-173">Varsa, self servis parola sıfırlama (SSPR) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7127e-173">Use self-service password reset (SSPR) if it's available.</span></span>  <span data-ttu-id="7127e-174">SSPR’nin çalışıp çalışmaması nasıl yapılandırıldığına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="7127e-174">Whether SSPR works depends on how it's configured.</span></span>  <span data-ttu-id="7127e-175">Daha fazla bilgi için bkz: [nasıl hello parola sıfırlama portalı iş](active-directory-passwords-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="7127e-175">For more information, see [How does hello password reset portal work](active-directory-passwords-best-practices.md).</span></span>

<span data-ttu-id="7127e-176">Office 365 kullanıcıları için yöneticinize hello parola özetlenen hello adımları kullanarak sıfırlayabilirsiniz [kullanıcı parolalarını sıfırlama](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="7127e-176">For Office 365 users, your admin can reset hello password by using hello steps outlined in [Reset user passwords](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span></span>

<span data-ttu-id="7127e-177">Azure AD hesapları için admins hello aşağıdakilerden birini kullanarak parolaları sıfırlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7127e-177">For Azure AD accounts, admins can reset passwords by using one of hello following:</span></span>

- [<span data-ttu-id="7127e-178">Hello Azure portal hesapları sıfırla</span><span class="sxs-lookup"><span data-stu-id="7127e-178">Reset accounts in hello Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
- [<span data-ttu-id="7127e-179">Merhaba Klasik Portalı'nda hesapları sıfırla</span><span class="sxs-lookup"><span data-stu-id="7127e-179">Reset accounts in hello classic portal</span></span>](active-directory-create-users-reset-password.md)
- [<span data-ttu-id="7127e-180">PowerShell’i kullanma</span><span class="sxs-lookup"><span data-stu-id="7127e-180">Using PowerShell</span></span>](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a><span data-ttu-id="7127e-181">Güvenlik</span><span class="sxs-lookup"><span data-stu-id="7127e-181">Security</span></span>
<span data-ttu-id="7127e-182">**S: Hesaplar belirli sayıda girişim başarısız olduktan sonra kilitleniyor mu, yoksa kullanılan daha karmaşık bir strateji mi var?**</span><span class="sxs-lookup"><span data-stu-id="7127e-182">**Q: Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?**</span></span></br>
<span data-ttu-id="7127e-183">Daha karmaşık bir strateji toolock hesapları kullanırız.</span><span class="sxs-lookup"><span data-stu-id="7127e-183">We use a more sophisticated strategy toolock accounts.</span></span>  <span data-ttu-id="7127e-184">Bu hello istek ve girilen hello parolalar hello IP temel alır.</span><span class="sxs-lookup"><span data-stu-id="7127e-184">This is based on hello IP of hello request and hello passwords entered.</span></span> <span data-ttu-id="7127e-185">Merhaba hello kilitleme süresini aynı zamanda bir saldırı olduğunu hello olasılığını göre artırır.</span><span class="sxs-lookup"><span data-stu-id="7127e-185">hello duration of hello lockout also increases based on hello likelihood that it is an attack.</span></span>  

<span data-ttu-id="7127e-186">**'Bu parolayı kullanılan toomany kez denendi' s: (ortak) parolaları ile Merhaba reddedilen belirli iletileri, bu hello geçerli active directory içinde kullanılan toopasswords bakın mu?**</span><span class="sxs-lookup"><span data-stu-id="7127e-186">**Q:  Certain (common) passwords get rejected with hello messages ‘this password has been used toomany times’, does this refer toopasswords used in hello current active directory?**</span></span></br>
<span data-ttu-id="7127e-187">Bu, tüm çeşitlemelerini "Parola" ve "123456" gibi genel olarak ortak toopasswords ifade eder.</span><span class="sxs-lookup"><span data-stu-id="7127e-187">This refers toopasswords that are globally common, such as any variants of “Password” and “123456”.</span></span>

<span data-ttu-id="7127e-188">**S: Güvenilmez kaynaklardan (botnet, tor uç noktası) gelen oturum açma istekleri bir B2C kiracısında engellenir mi veya bir Temel ya da Premium sürüm kiracı gerekir mi?**</span><span class="sxs-lookup"><span data-stu-id="7127e-188">**Q: Will a sign-in request from dubious sources (botnets, tor endpoint) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?**</span></span></br>
<span data-ttu-id="7127e-189">İstekleri filtreleyen ve botnetlere karşı koruma sağlayıp tüm B2C kiracılarına uygulanan bir ağ geçidine sahibiz.</span><span class="sxs-lookup"><span data-stu-id="7127e-189">We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.</span></span>

## <a name="application-access"></a><span data-ttu-id="7127e-190">Uygulama erişimi</span><span class="sxs-lookup"><span data-stu-id="7127e-190">Application access</span></span>
<span data-ttu-id="7127e-191">**S: Azure AD ile önceden tümleştirilmiş olan uygulamaların ve özelliklerinin listesini nereden bulabilirim?**</span><span class="sxs-lookup"><span data-stu-id="7127e-191">**Q: Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**</span></span>

<span data-ttu-id="7127e-192">**Y:** Azure AD, Microsoft'a, uygulama hizmeti sağlayıcılarına ve iş ortaklarına ait 2.600'ü aşkın önceden tümleştirilmiş uygulama içerir.</span><span class="sxs-lookup"><span data-stu-id="7127e-192">**A:** Azure AD has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners.</span></span> <span data-ttu-id="7127e-193">Önceden tümleştirilmiş tüm uygulamalar çoklu oturum açmayı (SSO) destekler.</span><span class="sxs-lookup"><span data-stu-id="7127e-193">All pre-integrated applications support single sign-on (SSO).</span></span> <span data-ttu-id="7127e-194">SSO, kuruluş kimlik bilgilerini tooaccess uygulamalarınızı kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="7127e-194">SSO lets you use your organizational credentials tooaccess your apps.</span></span> <span data-ttu-id="7127e-195">Bazı hello uygulamalar aynı zamanda otomatik hazırlama ve sağlamayı kaldırma özelliklerini destekler.</span><span class="sxs-lookup"><span data-stu-id="7127e-195">Some of hello applications also support automated provisioning and de-provisioning.</span></span>

<span data-ttu-id="7127e-196">Merhaba hello önceden tümleştirilmiş uygulamaların tam listesi için bkz: [Active Directory Marketi](https://azure.microsoft.com/marketplace/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="7127e-196">For a complete list of hello pre-integrated applications, see hello [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span></span>

- - -
<span data-ttu-id="7127e-197">**S: Peki hello ihtiyacım uygulama hello Azure AD marketinde değil misiniz?**</span><span class="sxs-lookup"><span data-stu-id="7127e-197">**Q: What if hello application I need is not in hello Azure AD marketplace?**</span></span>

<span data-ttu-id="7127e-198">**Y:** Azure AD Premium ile istediğiniz uygulamayı ekleyip yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7127e-198">**A:** With Azure AD Premium, you can add and configure any application that you want.</span></span> <span data-ttu-id="7127e-199">Uygulamanızın özelliklerine ve tercihlerinize bağlı olarak, SSO'yu ve otomatik hazırlamayı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7127e-199">Depending on your application’s capabilities and your preferences, you can configure SSO and automated provisioning.</span></span>  

<span data-ttu-id="7127e-200">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="7127e-200">For more information, see:</span></span>

* [<span data-ttu-id="7127e-201">Hello Azure Active Directory Uygulama galerisinde olmayan tek oturum açma tooapplications yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7127e-201">Configuring single sign-on tooapplications that are not in hello Azure Active Directory application gallery</span></span>](active-directory-saas-custom-apps.md)
* [<span data-ttu-id="7127e-202">SCIM'yi tooenable otomatik kullanıcıların ve grupların Azure Active Directory tooapplications sağlama kullanma</span><span class="sxs-lookup"><span data-stu-id="7127e-202">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)

- - -
<span data-ttu-id="7127e-203">**S: nasıl kullanıcılar Azure AD kullanarak tooapplications içinde oturum?**</span><span class="sxs-lookup"><span data-stu-id="7127e-203">**Q: How do users sign in tooapplications by using Azure AD?**</span></span>

<span data-ttu-id="7127e-204">**Y:** Azure AD kullanıcıların tooview için çeşitli yollar sağlar ve erişim gibi kendi uygulamalarında:</span><span class="sxs-lookup"><span data-stu-id="7127e-204">**A:** Azure AD provides several ways for users tooview and access their applications, such as:</span></span>

* <span data-ttu-id="7127e-205">Hello Azure AD erişim paneli</span><span class="sxs-lookup"><span data-stu-id="7127e-205">hello Azure AD access panel</span></span>
* <span data-ttu-id="7127e-206">Merhaba Office 365 uygulama Başlatıcı</span><span class="sxs-lookup"><span data-stu-id="7127e-206">hello Office 365 application launcher</span></span>
* <span data-ttu-id="7127e-207">Oturum açma doğrudan toofederated uygulamalar</span><span class="sxs-lookup"><span data-stu-id="7127e-207">Direct sign-in toofederated apps</span></span>
* <span data-ttu-id="7127e-208">Ayrıntılı bağlantılar toofederated, parola tabanlı veya var olan uygulamalar</span><span class="sxs-lookup"><span data-stu-id="7127e-208">Deep links toofederated, password-based, or existing apps</span></span>

<span data-ttu-id="7127e-209">Daha fazla bilgi için bkz: [dağıtma Azure AD tümleşik uygulamalarını toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span><span class="sxs-lookup"><span data-stu-id="7127e-209">For more information, see [Deploying Azure AD integrated applications toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

- - -
<span data-ttu-id="7127e-210">**S: hello farklı şekillerde Azure AD nelerdir kimlik doğrulaması ve çoklu oturum açma tooapplications sağlar?**</span><span class="sxs-lookup"><span data-stu-id="7127e-210">**Q: What are hello different ways Azure AD enables authentication and single sign-on tooapplications?**</span></span>

<span data-ttu-id="7127e-211">**Y:** Azure AD; SAML 2.0, OpenID Connect, OAuth 2.0 ve WS-Federasyon gibi birçok standartlaştırılmış kimlik doğrulaması ve yetkilendirme protokolünü destekler.</span><span class="sxs-lookup"><span data-stu-id="7127e-211">**A:** Azure AD supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation.</span></span> <span data-ttu-id="7127e-212">Azure AD aynı zamanda, yalnızca form tabanlı kimlik doğrulamasını destekleyen uygulamalar için parola kasası oluşturma ve otomatik oturum açma işlevlerini de destekler.</span><span class="sxs-lookup"><span data-stu-id="7127e-212">Azure AD also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.</span></span>  

<span data-ttu-id="7127e-213">Daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="7127e-213">For more information, see:</span></span>

* [<span data-ttu-id="7127e-214">Azure AD için Kimlik Doğrulama Senaryoları</span><span class="sxs-lookup"><span data-stu-id="7127e-214">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)
* [<span data-ttu-id="7127e-215">Active Directory kimlik doğrulama protokolleri</span><span class="sxs-lookup"><span data-stu-id="7127e-215">Active Directory authentication protocols</span></span>](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [<span data-ttu-id="7127e-216">Çoklu oturum açma özelliği, Azure Active Directory ile nasıl kullanılır?</span><span class="sxs-lookup"><span data-stu-id="7127e-216">How does single sign-on with Azure Active Directory work?</span></span>](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
<span data-ttu-id="7127e-217">**S: Şirket içi olarak çalıştırdığım uygulamaları ekleyebilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="7127e-217">**Q: Can I add applications I’m running on-premises?**</span></span>

<span data-ttu-id="7127e-218">**Y:** Azure AD uygulama proxy'si, kolay ve güvenli erişim ile seçtiğiniz tooon içi web uygulamaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="7127e-218">**A:** Azure AD Application Proxy provides you with easy and secure access tooon-premises web applications that you choose.</span></span> <span data-ttu-id="7127e-219">Bu uygulamaların hello erişmek için aynı şekilde Azure AD'de hizmet (SaaS) uygulamaları olarak yazılımınızı erişim.</span><span class="sxs-lookup"><span data-stu-id="7127e-219">You can access these applications in hello same way that you access your software as a service (SaaS) apps in Azure AD.</span></span> <span data-ttu-id="7127e-220">Ağ altyapınızın bir VPN veya toochange gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="7127e-220">There is no need for a VPN or toochange your network infrastructure.</span></span>  

<span data-ttu-id="7127e-221">Daha fazla bilgi için bkz: [nasıl tooprovide güvenli uzaktan erişim tooon içi uygulamaları](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7127e-221">For more information, see [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>

- - -
<span data-ttu-id="7127e-222">**S: Belirli bir uygulamaya erişen kullanıcılar için çok faktörlü kimlik doğrulamasını nasıl isteyebilirim?**</span><span class="sxs-lookup"><span data-stu-id="7127e-222">**Q: How do I require multi-factor authentication for users who access a particular application?**</span></span>

<span data-ttu-id="7127e-223">**Y:** Azure AD koşullu erişimi ile her bir uygulama için benzersiz bir erişim ilkesi atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7127e-223">**A:** With Azure AD conditional access, you can assign a unique access policy for each application.</span></span> <span data-ttu-id="7127e-224">İlkenizde, her zaman çok faktörlü kimlik doğrulamasını zorunlu kılabilir veya ne zaman kullanıcılar yerel ağa bağlı toohello olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="7127e-224">In your policy, you can require multi-factor authentication always, or when users are not connected toohello local network.</span></span>  

<span data-ttu-id="7127e-225">Daha fazla bilgi için bkz: [tooOffice 365 ve diğer uygulamalar erişim güvenliği bağlı tooAzure Active Directory](active-directory-conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="7127e-225">For more information, see [Securing access tooOffice 365 and other apps connected tooAzure Active Directory](active-directory-conditional-access.md).</span></span>

- - -
<span data-ttu-id="7127e-226">**S: SaaS uygulamaları için otomatik kullanıcı hazırlama nedir?**</span><span class="sxs-lookup"><span data-stu-id="7127e-226">**Q: What is automated user provisioning for SaaS apps?**</span></span>

<span data-ttu-id="7127e-227">**Y:** kullanım Azure AD tooautomate hello oluşturulması, Bakım ve birçok popüler bulut SaaS uygulamalarına kullanıcı kimliklerini kaldırılması.</span><span class="sxs-lookup"><span data-stu-id="7127e-227">**A:** Use Azure AD tooautomate hello creation, maintenance, and removal of user identities in many popular cloud SaaS apps.</span></span>

<span data-ttu-id="7127e-228">Daha fazla bilgi için bkz: [otomatikleştirmek kullanıcı sağlama ve Azure Active Directory ile tooSaaS uygulamaları etkinleştirmektir](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="7127e-228">For more information, see [Automate user provisioning and deprovisioning tooSaaS applications with Azure Active Directory](active-directory-saas-app-provisioning.md).</span></span>

- - -
<span data-ttu-id="7127e-229">**S:  Azure AD ile güvenli bir LDAP bağlantısı oluşturabilir miyim?**</span><span class="sxs-lookup"><span data-stu-id="7127e-229">**Q:  Can I set up a secure LDAP connection with Azure AD?**</span></span>

<span data-ttu-id="7127e-230">**Y:** Hayır.</span><span class="sxs-lookup"><span data-stu-id="7127e-230">**A:**  No.</span></span> <span data-ttu-id="7127e-231">Azure AD hello LDAP protokolünü desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="7127e-231">Azure AD does not support hello LDAP protocol.</span></span>
