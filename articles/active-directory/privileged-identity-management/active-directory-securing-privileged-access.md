---
title: "Azure AD'de ayrıcalıklı erişimi güvenli hale getirme | Microsoft Docs"
description: "Azure, Azure Active Directory ve Microsoft Online Services ayrıcalıklı erişim güvenliği yaklaşımları açıklayan bir konu."
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
ms.openlocfilehash: acd1c11cecfa37f607fe5d82a76a40647093f43f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="securing-privileged-access-in-azure-ad"></a><span data-ttu-id="ef5aa-103">Azure AD'de ayrıcalıklı erişimi güvenli hale getirme</span><span class="sxs-lookup"><span data-stu-id="ef5aa-103">Securing privileged access in Azure AD</span></span>
<span data-ttu-id="ef5aa-104">Ayrıcalıklı erişimi güvenli hale getirme iş varlıklar modern bir kuruluşta korunmasına yardımcı olmak için bir kritik ilk adımdır.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-104">Securing privileged access is a critical first step to help protect business assets in a modern organization.</span></span> <span data-ttu-id="ef5aa-105">Ayrıcalıklı hesapları yönetmek ve BT sistemleri yöneten hesaplarıdır.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-105">Privileged accounts are accounts that administer and manage IT systems.</span></span> <span data-ttu-id="ef5aa-106">Siber saldırganların bir kuruluşun veriler ve sistemlerle erişmek için bu hesaplar hedef.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-106">Cyber-attackers target these accounts to gain access to an organization’s data and systems.</span></span> <span data-ttu-id="ef5aa-107">Ayrıcalıklı erişim güvenliğini sağlamak için hesapları ve kötü niyetli bir kullanıcı için maruz kalma riskini sistemlerden yalıtmak.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-107">To secure privileged access, you should isolate the accounts and systems from the risk of being exposed to a malicious user.</span></span>

<span data-ttu-id="ef5aa-108">Bulut Hizmetleri üzerinden ayrıcalıklı erişim kazanmak daha fazla kullanıcı başlıyor.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-108">More users are starting to get privileged access through cloud services.</span></span> <span data-ttu-id="ef5aa-109">Bu, Office365, genel Yöneticiler, Azure aboneliği yöneticileri ve VM'ler veya SaaS uygulamalarını yönetimsel erişime sahip kullanıcılar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-109">This can include global administrators of Office365, Azure subscription administrators, and users who have administrative access in VMs or on SaaS apps.</span></span>

<span data-ttu-id="ef5aa-110">Microsoft önerir bu yol haritası izlediğiniz [ayrıcalıklı erişimi güvenli hale getirme](https://technet.microsoft.com/library/mt631194.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef5aa-110">Microsoft recommends you follow this roadmap on [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx).</span></span>

<span data-ttu-id="ef5aa-111">Kullanıcı hesapları yönetilir ve Azure Active Directory veya Active Directory tarafından kimliği doğrulanmış olup olmadığını Azure Active Directory, Office 365 veya diğer Microsoft Hizmetleri ve uygulamaları kullanan müşteriler için bu kurallar uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-111">For customers using Azure Active Directory, Office 365, or other Microsoft services and applications, these principles apply whether user accounts are managed and authenticated by Active Directory or in Azure Active Directory.</span></span> <span data-ttu-id="ef5aa-112">Aşağıdaki bölümler, ayrıcalıklı erişim güvenliği desteklemek için Azure AD özelliklerini daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-112">The following sections provide more information on Azure AD features to support securing privileged access.</span></span>

## <a name="azure-multi-factor-authentication"></a><span data-ttu-id="ef5aa-113">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ef5aa-113">Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="ef5aa-114">Yönetici kimlik doğrulaması güvenliğini artırmak için iki aşamalı doğrulamayı ayrıcalıklarını verme önce istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-114">To increase the security of administrator authentication, you should require two-step verification before granting privileges.</span></span> <span data-ttu-id="ef5aa-115">İki aşamalı doğrulama, olan doğrulama yöntemi daha fazlasını bir kullanıcı adı ve parola kullanımını gerektirmesidir.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-115">Two-step verification is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="ef5aa-116">İkinci bir kullanıcı oturum açmaları ve işlemleri için güvenlik katmanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-116">It provides a second layer of security to user sign-ins and transactions.</span></span>

<span data-ttu-id="ef5aa-117">Azure multi-Factor Authentication (MFA) hangi yardımcı koruma veri ve uygulamalarınıza erişmek için kullanıcının toplantı sırasında isteğe bağlı bir basit oturum açma işlemi için Microsoft'un iki aşamalı doğrulama, bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-117">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution, which helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="ef5aa-118">Kolay doğrulama seçenekleri de dahil olmak üzere çeşitli aracılığıyla güçlü kimlik doğrulaması sunar:</span><span class="sxs-lookup"><span data-stu-id="ef5aa-118">It delivers strong authentication via a range of easy verification options including:</span></span>

- <span data-ttu-id="ef5aa-119">telefon aramaları</span><span class="sxs-lookup"><span data-stu-id="ef5aa-119">phone calls</span></span>
- <span data-ttu-id="ef5aa-120">Metin iletileri</span><span class="sxs-lookup"><span data-stu-id="ef5aa-120">text messages</span></span>
- <span data-ttu-id="ef5aa-121">Mobil uygulama bildirimleri</span><span class="sxs-lookup"><span data-stu-id="ef5aa-121">mobile app notifications</span></span>
- <span data-ttu-id="ef5aa-122">Mobil uygulama doğrulama kodları</span><span class="sxs-lookup"><span data-stu-id="ef5aa-122">mobile app verification codes</span></span>
- <span data-ttu-id="ef5aa-123">Üçüncü taraf OATH belirteçleri</span><span class="sxs-lookup"><span data-stu-id="ef5aa-123">third-party OATH tokens</span></span>

<span data-ttu-id="ef5aa-124">Azure multi-Factor Authentication nasıl çalıştığını genel bir bakış için aşağıdaki videoya bakın:</span><span class="sxs-lookup"><span data-stu-id="ef5aa-124">For an overview of how Azure Multi-Factor Authentication works see the following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]

<span data-ttu-id="ef5aa-125">Daha fazla bilgi için bkz: [MFA Office 365 ve Azure MFA için](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span><span class="sxs-lookup"><span data-stu-id="ef5aa-125">For more information, see [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span></span>

## <a name="time-bound-privileges"></a><span data-ttu-id="ef5aa-126">Zaman sınırlı ayrıcalıkları</span><span class="sxs-lookup"><span data-stu-id="ef5aa-126">Time-bound privileges</span></span>
<span data-ttu-id="ef5aa-127">Bazı kuruluşlar, çok sayıda kullanıcı yüksek ayrıcalıklı rolleri olması fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-127">Some organizations may find that they have too many users in highly privileged roles.</span></span> <span data-ttu-id="ef5aa-128">Bir kullanıcı belirli bir etkinliği için rolüne gibi bir hizmet için kaydolmak için eklenmiş olabilir, ancak o ayrıcalıkları sık daha sonra kullanmadı.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-128">A user might have been added to the role for a particular activity, like to sign up for a service, but didn't use those privileges frequently afterward.</span></span>

<span data-ttu-id="ef5aa-129">Ayrıcalıkları Etkilenme süresini azaltmak ve bunların kullanılması, görünürlük artırmak için yalnızca "tam zamanında" ayrıcalıklarını üzerinde alan kullanıcıların sınırla (JIT), bir görev gerçekleştirmeniz gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-129">To lower the exposure time of privileges and increase your visibility into their use, limit users to only taking on their privileges "just in time" (JIT), when they need to perform a task.</span></span> <span data-ttu-id="ef5aa-130">Azure Active Directory ve Microsoft Online Services için kullanabileceğiniz [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span><span class="sxs-lookup"><span data-stu-id="ef5aa-130">For Azure Active Directory and Microsoft Online Services, you can use [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span></span>

![PIM Panosu][2]

## <a name="attack-detection"></a><span data-ttu-id="ef5aa-132">Saldırı algılama</span><span class="sxs-lookup"><span data-stu-id="ef5aa-132">Attack detection</span></span>
<span data-ttu-id="ef5aa-133">[Azure Active Directory kimlik koruması](../active-directory-identityprotection.md) risk olaylarına ve olası güvenlik açıklarını kuruluşunuzdaki kimlikleri etkileyen birleştirilmiş bir görünüm sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-133">[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) provides a consolidated view into risk events and potential vulnerabilities affecting your organization’s identities.</span></span> <span data-ttu-id="ef5aa-134">Risk olaylara göre risk tabanlı ilkeleri, kuruluşunuzun kimlikleri otomatik olarak korunacak yapılandırmanızı sağlayacak şekilde her bir kullanıcı için bir kullanıcı risk düzeyi kimlik koruması hesaplar.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-134">Based on risk events, Identity Protection calculates a user risk level for each user, enabling you to configure risk-based policies to automatically protect the identities of your organization.</span></span> <span data-ttu-id="ef5aa-135">Azure Active Directory ve EMS tarafından sağlanan diğer koşullu erişim denetimlerle birlikte bu ilkeler, otomatik olarak kullanıcı engelleme veya parola sıfırlama ve çok faktörlü kimlik doğrulaması zorlama dahil öneriler sunar.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-135">These policies, along with other conditional access controls provided by Azure Active Directory and EMS, can automatically block the user or offer suggestions that include password resets and multi-factor authentication enforcement.</span></span>

![Azure AD Kimlik Koruması][3]

## <a name="conditional-access"></a><span data-ttu-id="ef5aa-137">Koşullu erişim</span><span class="sxs-lookup"><span data-stu-id="ef5aa-137">Conditional access</span></span>
<span data-ttu-id="ef5aa-138">Koşullu erişim denetimi ile bir kullanıcı bir uygulamaya erişimine izin vermeden önce kimlik doğrulaması sırasında seçtiğiniz belirli koşullar Azure Active Directory denetler.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-138">With conditional access control, Azure Active Directory checks the specific conditions you choose when authenticating a user, before allowing access to an application.</span></span> <span data-ttu-id="ef5aa-139">Bu koşullar sağlandığında, kullanıcı kimlik doğrulaması ve uygulamaya erişim izni.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-139">Once those conditions are met, the user is authenticated and allowed access to the application.</span></span>

![MFA ile koşullu erişim kurallarının ayarlanması][4]

## <a name="related-articles"></a><span data-ttu-id="ef5aa-141">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="ef5aa-141">Related articles</span></span>
* <span data-ttu-id="ef5aa-142">Etkinleştirme [Azure çok faktörlü kimlik doğrulaması](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="ef5aa-142">Enable [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span></span>
* <span data-ttu-id="ef5aa-143">Etkinleştirme [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span><span class="sxs-lookup"><span data-stu-id="ef5aa-143">Enable [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span></span>
* <span data-ttu-id="ef5aa-144">Etkinleştirme [Azure AD kimlik koruması](../active-directory-identityprotection.md)</span><span class="sxs-lookup"><span data-stu-id="ef5aa-144">Enable [Azure AD Identity Protection](../active-directory-identityprotection.md)</span></span>
* <span data-ttu-id="ef5aa-145">Etkinleştirme [koşullu erişim denetimleri](../active-directory-conditional-access.md)</span><span class="sxs-lookup"><span data-stu-id="ef5aa-145">Enable [conditional access controls](../active-directory-conditional-access.md)</span></span>

<span data-ttu-id="ef5aa-146">Tüm güvenlik yol haritası oluşturma ile ilgili daha fazla bilgi için "Müşteri sorumlulukları ve yol haritası" bölümüne bakın [Microsoft Cloud Security Kurumsal Mimarlar için](http://aka.ms/securecustomer) belge.</span><span class="sxs-lookup"><span data-stu-id="ef5aa-146">For more information on building a complete security roadmap, see the “Customer responsibilities and roadmap” section of the [Microsoft Cloud Security for Enterprise Architects](http://aka.ms/securecustomer) document.</span></span> <span data-ttu-id="ef5aa-147">Aşağıdaki konulardan birini yardımcı olmak için Microsoft Hizmetleri katılımcılarını sürece dahil etme hakkında daha fazla bilgi için Microsoft temsilcinize başvurun veya ziyaret bizim [siber güvenlik çözümleri sayfa](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef5aa-147">For more information on engaging Microsoft services to assist with any of these topics, contact your Microsoft representative or visit our [Cybersecurity solutions page](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).</span></span>

<!--Image references-->
[1]: ../media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: ../media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: ../media/active-directory-identityprotection/29.png
[4]: ../media/active-directory-conditional-access/conditionalaccess-saas-apps.png
