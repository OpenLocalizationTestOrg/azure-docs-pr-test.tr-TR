---
title: "Azure AD'de ayrıcalıklı erişim aaaSecuring | Microsoft Docs"
description: "Azure, Azure Active Directory ve Microsoft Online Services ayrıcalıklı erişim güvenliğini sağlamak için hello açıklayan bir konu yaklaşıyor."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: 694835dc5c41640673dbd996d44b0d1f217220de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a><span data-ttu-id="cb3bd-103">Azure AD'de ayrıcalıklı erişimi güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="cb3bd-103">Securing privileged access in Azure AD</span></span>
<span data-ttu-id="cb3bd-104">Ayrıcalıklı güvenliğini sağlama erişim önemli bir ilk adım, toohelp korumak modern bir kuruluştaki iş varlıklar.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-104">Securing privileged access is a critical first step toohelp protect business assets in a modern organization.</span></span> <span data-ttu-id="cb3bd-105">Ayrıcalıklı hesapları yönetmek ve BT sistemleri yöneten hesaplarıdır.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-105">Privileged accounts are accounts that administer and manage IT systems.</span></span> <span data-ttu-id="cb3bd-106">Bu hesapları toogain erişim tooan kuruluşunuzun veri ve sistemler siber saldırganların hedefleyin.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-106">Cyber-attackers target these accounts toogain access tooan organization’s data and systems.</span></span> <span data-ttu-id="cb3bd-107">toosecure ayrıcalıklı erişimi, hello hesapları yalıtarak ve tooa kötü amaçlı kullanıcı olma hello risk sistemlerden gösteriliyor.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-107">toosecure privileged access, you should isolate hello accounts and systems from hello risk of being exposed tooa malicious user.</span></span>

<span data-ttu-id="cb3bd-108">Daha fazla kullanıcı tooget ayrıcalıklı erişim bulut Hizmetleri ile başlıyor.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-108">More users are starting tooget privileged access through cloud services.</span></span> <span data-ttu-id="cb3bd-109">Bu, Office365, genel Yöneticiler, Azure aboneliği yöneticileri ve VM'ler veya SaaS uygulamalarını yönetimsel erişime sahip kullanıcılar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-109">This can include global administrators of Office365, Azure subscription administrators, and users who have administrative access in VMs or on SaaS apps.</span></span>

<span data-ttu-id="cb3bd-110">Microsoft önerir bu yol haritası izlediğiniz [ayrıcalıklı erişimi güvenli hale getirme](https://technet.microsoft.com/library/mt631194.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb3bd-110">Microsoft recommends you follow this roadmap on [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx).</span></span>

<span data-ttu-id="cb3bd-111">Kullanıcı hesapları yönetilir ve Azure Active Directory veya Active Directory tarafından kimliği doğrulanmış olup olmadığını Azure Active Directory, Office 365 veya diğer Microsoft Hizmetleri ve uygulamaları kullanan müşteriler için bu kurallar uygulanır.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-111">For customers using Azure Active Directory, Office 365, or other Microsoft services and applications, these principles apply whether user accounts are managed and authenticated by Active Directory or in Azure Active Directory.</span></span> <span data-ttu-id="cb3bd-112">Merhaba aşağıdaki bölümlerde daha fazla bilgi üzerinde Azure AD özellikleri toosupport ayrıcalıklı erişim güvenliğini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-112">hello following sections provide more information on Azure AD features toosupport securing privileged access.</span></span>

## <a name="azure-multi-factor-authentication"></a><span data-ttu-id="cb3bd-113">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="cb3bd-113">Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="cb3bd-114">tooincrease hello güvenlik yönetici kimlik doğrulama ayrıcalıklarını verme önce iki aşamalı doğrulama istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-114">tooincrease hello security of administrator authentication, you should require two-step verification before granting privileges.</span></span> <span data-ttu-id="cb3bd-115">İki aşamalı doğrulama, olan doğrulama için bir yöntem hello kullanımını daha fazlasını bir kullanıcı adı ve parola gerektirmesidir.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-115">Two-step verification is a method of verifying who you are that requires hello use of more than just a username and password.</span></span> <span data-ttu-id="cb3bd-116">Güvenlik toouser oturum açmalarına ve işlemlerine ikinci bir katmanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-116">It provides a second layer of security toouser sign-ins and transactions.</span></span>

<span data-ttu-id="cb3bd-117">Azure multi-Factor Authentication (MFA) Microsoft'un iki aşamalı doğrulama çözüm, hangi erişim toodata ve uygulamaları basit bir oturum açma işlemi için kullanıcı talebine buluştururken korunmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-117">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution, which helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="cb3bd-118">Kolay doğrulama seçenekleri de dahil olmak üzere çeşitli aracılığıyla güçlü kimlik doğrulaması sunar:</span><span class="sxs-lookup"><span data-stu-id="cb3bd-118">It delivers strong authentication via a range of easy verification options including:</span></span>

- <span data-ttu-id="cb3bd-119">telefon aramaları</span><span class="sxs-lookup"><span data-stu-id="cb3bd-119">phone calls</span></span>
- <span data-ttu-id="cb3bd-120">Metin iletileri</span><span class="sxs-lookup"><span data-stu-id="cb3bd-120">text messages</span></span>
- <span data-ttu-id="cb3bd-121">Mobil uygulama bildirimleri</span><span class="sxs-lookup"><span data-stu-id="cb3bd-121">mobile app notifications</span></span>
- <span data-ttu-id="cb3bd-122">Mobil uygulama doğrulama kodları</span><span class="sxs-lookup"><span data-stu-id="cb3bd-122">mobile app verification codes</span></span>
- <span data-ttu-id="cb3bd-123">Üçüncü taraf OATH belirteçleri</span><span class="sxs-lookup"><span data-stu-id="cb3bd-123">third-party OATH tokens</span></span>

<span data-ttu-id="cb3bd-124">Azure multi-Factor Authentication nasıl çalıştığını genel bir bakış için aşağıdaki videoyu hello bakın:</span><span class="sxs-lookup"><span data-stu-id="cb3bd-124">For an overview of how Azure Multi-Factor Authentication works see hello following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

<span data-ttu-id="cb3bd-125">Daha fazla bilgi için bkz: [MFA Office 365 ve Azure MFA için](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span><span class="sxs-lookup"><span data-stu-id="cb3bd-125">For more information, see [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span></span>

## <a name="time-bound-privileges"></a><span data-ttu-id="cb3bd-126">Zaman sınırlı ayrıcalıkları</span><span class="sxs-lookup"><span data-stu-id="cb3bd-126">Time-bound privileges</span></span>
<span data-ttu-id="cb3bd-127">Bazı kuruluşlar, çok sayıda kullanıcı yüksek ayrıcalıklı rolleri olması fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-127">Some organizations may find that they have too many users in highly privileged roles.</span></span> <span data-ttu-id="cb3bd-128">Bir kullanıcı bir hizmet için toosign gibi belirli bir etkinliği için toohello rolü eklenmiş olabilir ancak bu ayrıcalıkları sık daha sonra kullanmadı.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-128">A user might have been added toohello role for a particular activity, like toosign up for a service, but didn't use those privileges frequently afterward.</span></span>

<span data-ttu-id="cb3bd-129">toolower hello Etkilenme zaman ayrıcalık ve bunların kullanılması ayrıcalıklarını üzerinde "tam zamanında" alma sınırı kullanıcılar tooonly, görünürlük artırma (JIT), bir görev tooperform gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-129">toolower hello exposure time of privileges and increase your visibility into their use, limit users tooonly taking on their privileges "just in time" (JIT), when they need tooperform a task.</span></span> <span data-ttu-id="cb3bd-130">Azure Active Directory ve Microsoft Online Services için kullanabileceğiniz [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span><span class="sxs-lookup"><span data-stu-id="cb3bd-130">For Azure Active Directory and Microsoft Online Services, you can use [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span></span>

![PIM Panosu][2]

## <a name="attack-detection"></a><span data-ttu-id="cb3bd-132">Saldırı algılama</span><span class="sxs-lookup"><span data-stu-id="cb3bd-132">Attack detection</span></span>
<span data-ttu-id="cb3bd-133">[Azure Active Directory kimlik koruması](../active-directory-identityprotection.md) risk olaylarına ve olası güvenlik açıklarını kuruluşunuzdaki kimlikleri etkileyen birleştirilmiş bir görünüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-133">[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) provides a consolidated view into risk events and potential vulnerabilities affecting your organization’s identities.</span></span> <span data-ttu-id="cb3bd-134">Risk olaylarına bağlı olarak, her kullanıcı için bir kullanıcı risk düzeyi kimlik koruması hesaplar, sağlayarak tooautomatically korumak tooconfigure risk tabanlı ilkeleri, kuruluşunuzun kimlikleri hello.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-134">Based on risk events, Identity Protection calculates a user risk level for each user, enabling you tooconfigure risk-based policies tooautomatically protect hello identities of your organization.</span></span> <span data-ttu-id="cb3bd-135">Azure Active Directory ve EMS tarafından sağlanan diğer koşullu erişim denetimlerle birlikte bu ilkeler, otomatik olarak hello kullanıcı engelleme veya parola sıfırlama ve çok faktörlü kimlik doğrulaması zorlama dahil öneriler sunar.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-135">These policies, along with other conditional access controls provided by Azure Active Directory and EMS, can automatically block hello user or offer suggestions that include password resets and multi-factor authentication enforcement.</span></span>

![Azure AD Kimlik Koruması][3]

## <a name="conditional-access"></a><span data-ttu-id="cb3bd-137">Koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="cb3bd-137">Conditional access</span></span>
<span data-ttu-id="cb3bd-138">Koşullu erişim denetimi ile Azure Active Directory erişimi tooan uygulama izin vermeden önce bir kullanıcının kimliğini doğrularken seçtiğiniz hello belirli koşullar denetler.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-138">With conditional access control, Azure Active Directory checks hello specific conditions you choose when authenticating a user, before allowing access tooan application.</span></span> <span data-ttu-id="cb3bd-139">Bu koşullar sağlandığında hello kullanıcı kimlik doğrulaması ve erişim toohello uygulama izin verilir.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-139">Once those conditions are met, hello user is authenticated and allowed access toohello application.</span></span>

![MFA ile koşullu erişim kurallarının ayarlanması][4]

## <a name="related-articles"></a><span data-ttu-id="cb3bd-141">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="cb3bd-141">Related articles</span></span>
* <span data-ttu-id="cb3bd-142">Etkinleştirme [Azure çok faktörlü kimlik doğrulaması](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="cb3bd-142">Enable [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span></span>
* <span data-ttu-id="cb3bd-143">Etkinleştirme [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span><span class="sxs-lookup"><span data-stu-id="cb3bd-143">Enable [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span></span>
* <span data-ttu-id="cb3bd-144">Etkinleştirme [Azure AD kimlik koruması](../active-directory-identityprotection.md)</span><span class="sxs-lookup"><span data-stu-id="cb3bd-144">Enable [Azure AD Identity Protection](../active-directory-identityprotection.md)</span></span>
* <span data-ttu-id="cb3bd-145">Etkinleştirme [koşullu erişim denetimleri](../active-directory-conditional-access.md)</span><span class="sxs-lookup"><span data-stu-id="cb3bd-145">Enable [conditional access controls](../active-directory-conditional-access.md)</span></span>

<span data-ttu-id="cb3bd-146">Tüm güvenlik yol haritası oluşturma ile ilgili daha fazla bilgi için hello hello "Müşteri sorumlulukları ve yol haritası" bölümüne bakın [Microsoft Cloud Security Kurumsal Mimarlar için](http://aka.ms/securecustomer) belge.</span><span class="sxs-lookup"><span data-stu-id="cb3bd-146">For more information on building a complete security roadmap, see hello “Customer responsibilities and roadmap” section of hello [Microsoft Cloud Security for Enterprise Architects](http://aka.ms/securecustomer) document.</span></span> <span data-ttu-id="cb3bd-147">Bu konularda biriyle Microsoft Hizmetleri tooassist çekici daha fazla bilgi için Microsoft temsilcinize başvurun veya ziyaret bizim [siber güvenlik çözümleri sayfa](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb3bd-147">For more information on engaging Microsoft services tooassist with any of these topics, contact your Microsoft representative or visit our [Cybersecurity solutions page](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span></span>

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
