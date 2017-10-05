---
title: "Rol etkinleştirme ayarlarını yönetme | Microsoft Docs"
description: "Azure Active Directory Privileged Identity Management uzantısı ile ayrıcalıklı kimlikleri için varsayılan ayarları değiştirmeyi öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 23605e89cd1846d2e06e48cb5d3e0191cb9e9b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="6dec0-103">Azure AD Privileged Identity Management'ın rol etkinleştirme ayarlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="6dec0-103">How to manage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="6dec0-104">Ayrıcalıklı Rol Yöneticisi Azure AD Privileged Identity Management (PIM) uygun rol ataması etkinleştirme bir kullanıcı deneyimini değiştirme gibi kuruluşlarındaki özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6dec0-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-the-role-activation-settings"></a><span data-ttu-id="6dec0-105">Rol etkinleştirme ayarlarını yönet</span><span class="sxs-lookup"><span data-stu-id="6dec0-105">Manage the role activation settings</span></span>
1. <span data-ttu-id="6dec0-106">Git [Azure portal](https://portal.azure.com) seçip **Azure AD Privileged Identity Management** panodan uygulama.</span><span class="sxs-lookup"><span data-stu-id="6dec0-106">Go to the [Azure portal](https://portal.azure.com) and select the **Azure AD Privileged Identity Management** app from the dashboard.</span></span>
2. <span data-ttu-id="6dec0-107">Seçin **yönetmek ayrıcalıklı rolleri** > **ayarları** > **ayrıcalıklı rolleri**.</span><span class="sxs-lookup"><span data-stu-id="6dec0-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="6dec0-108">Rolü ayarlarını seçin, yönetmek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="6dec0-108">Choose the role whose settings you want to manage.</span></span>

<span data-ttu-id="6dec0-109">Her rol için Ayarları sayfasında, ayarları yapılandırabileceğiniz bir dizi vardır.</span><span class="sxs-lookup"><span data-stu-id="6dec0-109">On the settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="6dec0-110">Bu ayarlar yalnızca uygun yönetici, değil kalıcı yönetici sahip kullanıcıların etkiler.</span><span class="sxs-lookup"><span data-stu-id="6dec0-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="6dec0-111">**Etkinleştirme**: süresi dolmadan önce bir rol etkin kalmasını saat cinsinden süre.</span><span class="sxs-lookup"><span data-stu-id="6dec0-111">**Activations**: The time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="6dec0-112">Bu, 1 ila 72 saat arasında olabilir.</span><span class="sxs-lookup"><span data-stu-id="6dec0-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="6dec0-113">**Bildirimleri**: rol etkinleştirdikten admins onaylayan Sistem e-posta gönderir olup olmadığını seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6dec0-113">**Notifications**: You can choose whether or not the system sends emails to admins confirming that they have activated a role.</span></span> <span data-ttu-id="6dec0-114">Bu, yetkisiz veya aykırı etkinleştirmeleri algılamak için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6dec0-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="6dec0-115">**Olay/istek anahtarı**: rolleri etkinleştirdiğinizde bilet numarası eklemek için uygun yöneticilerinin kullanmamayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6dec0-115">**Incident/Request Ticket**: You can choose whether or not to require eligible admins to include a ticket number when they activate their role.</span></span> <span data-ttu-id="6dec0-116">Rol erişim denetimleri gerçekleştirdiğinizde bu yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6dec0-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="6dec0-117">**Çok faktörlü kimlik doğrulaması**: kullanıcılar kendi rolleri etkinleştirilebilmesi MFA ile kullanıcıların kimliğini doğrulamak gerekli verilip verilmeyeceğini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6dec0-117">**Multi-Factor Authentication**: You can choose whether or not to require users to verify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="6dec0-118">Yalnızca bu kez her bir rolü etkinleştirmemek her zaman oturum doğrulamak sahiptirler.</span><span class="sxs-lookup"><span data-stu-id="6dec0-118">They only have to verify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="6dec0-119">MFA etkinleştirdiğinizde göz önünde bulundurmanız iki ipuçları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6dec0-119">There are two tips to keep in mind when you enable MFA:</span></span>

* <span data-ttu-id="6dec0-120">E-postaları için Microsoft hesabına sahip kullanıcıların (genellikle @outlook.com, ancak her zaman) için Azure MFA kaydedilemiyor.</span><span class="sxs-lookup"><span data-stu-id="6dec0-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="6dec0-121">Microsoft hesabı olan kullanıcılar için rol atamak istiyorsanız, bunları kalıcı yönetici yapın veya bu rol için MFA devre dışı bırakmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="6dec0-121">If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="6dec0-122">MFA için üst düzey ayrıcalıklı rolleri Azure AD için devre dışı bırakamazsınız ve Office365.</span><span class="sxs-lookup"><span data-stu-id="6dec0-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="6dec0-123">Bu, bu rolleri dikkatle korunması için bir güvenlik özelliğidir:</span><span class="sxs-lookup"><span data-stu-id="6dec0-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="6dec0-124">Uygulama Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="6dec0-124">Application administrator</span></span>
  * <span data-ttu-id="6dec0-125">Uygulama Proxy sunucusu Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="6dec0-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="6dec0-126">Faturalama Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="6dec0-126">Billing administrator</span></span>  
  * <span data-ttu-id="6dec0-127">Uyumluluk Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="6dec0-127">Compliance administrator</span></span>  
  * <span data-ttu-id="6dec0-128">CRM Hizmet Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="6dec0-128">CRM service administrator</span></span>
  * <span data-ttu-id="6dec0-129">Müşteri kasa erişimi onaylayıcı</span><span class="sxs-lookup"><span data-stu-id="6dec0-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="6dec0-130">Directory yazıcısı</span><span class="sxs-lookup"><span data-stu-id="6dec0-130">Directory writer</span></span>  
  * <span data-ttu-id="6dec0-131">Exchange Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="6dec0-131">Exchange administrator</span></span>  
  * <span data-ttu-id="6dec0-132">Genel yönetici</span><span class="sxs-lookup"><span data-stu-id="6dec0-132">Global administrator</span></span>
  * <span data-ttu-id="6dec0-133">Intune Hizmet Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="6dec0-133">Intune service administrator</span></span>
  * <span data-ttu-id="6dec0-134">Posta kutusu Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="6dec0-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="6dec0-135">İş ortağı tier1 desteği</span><span class="sxs-lookup"><span data-stu-id="6dec0-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="6dec0-136">İş ortağı tier2 desteği</span><span class="sxs-lookup"><span data-stu-id="6dec0-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="6dec0-137">Ayrıcalıklı Rol Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="6dec0-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="6dec0-138">Güvenlik yöneticisi</span><span class="sxs-lookup"><span data-stu-id="6dec0-138">Security administrator</span></span>  
  * <span data-ttu-id="6dec0-139">SharePoint Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="6dec0-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="6dec0-140">Skype Kurumsal yöneticisi</span><span class="sxs-lookup"><span data-stu-id="6dec0-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="6dec0-141">Kullanıcı Hesap Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="6dec0-141">User account administrator</span></span>  

<span data-ttu-id="6dec0-142">MFA ile PIM kullanma hakkında daha fazla bilgi için bkz: [gerektiren MFA nasıl](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="6dec0-142">For more information about using MFA with PIM see [How to Require MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what the temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="6dec0-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6dec0-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

