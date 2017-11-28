---
title: "aaaHow toomanage rol etkinleştirme ayarlarını | Microsoft Docs"
description: "Nasıl toochange hello ayrıcalıklı kimlikleri için varsayılan ayarları hello Azure Active Directory Privileged Identity Management uzantısı ile bilgi edinin."
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
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="72126-103">Nasıl toomanage rol etkinleştirme Azure AD Privileged Identity Management ayarlarında</span><span class="sxs-lookup"><span data-stu-id="72126-103">How toomanage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="72126-104">Ayrıcalıklı Rol Yöneticisi Azure AD Privileged Identity Management (PIM) uygun rol ataması etkinleştirme bir kullanıcı için hello deneyimi değiştirme gibi kuruluşlarındaki özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72126-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing hello experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-hello-role-activation-settings"></a><span data-ttu-id="72126-105">Merhaba rol etkinleştirme ayarlarını yönet</span><span class="sxs-lookup"><span data-stu-id="72126-105">Manage hello role activation settings</span></span>
1. <span data-ttu-id="72126-106">Toohello Git [Azure portal](https://portal.azure.com) ve select hello **Azure AD Privileged Identity Management** hello panosundan uygulama.</span><span class="sxs-lookup"><span data-stu-id="72126-106">Go toohello [Azure portal](https://portal.azure.com) and select hello **Azure AD Privileged Identity Management** app from hello dashboard.</span></span>
2. <span data-ttu-id="72126-107">Seçin **yönetmek ayrıcalıklı rolleri** > **ayarları** > **ayrıcalıklı rolleri**.</span><span class="sxs-lookup"><span data-stu-id="72126-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="72126-108">Merhaba rol ayarlarını seçin toomanage istiyor.</span><span class="sxs-lookup"><span data-stu-id="72126-108">Choose hello role whose settings you want toomanage.</span></span>

<span data-ttu-id="72126-109">Hello Ayarları sayfasında her rol için çeşitli yapılandırabileceğiniz ayarlar vardır.</span><span class="sxs-lookup"><span data-stu-id="72126-109">On hello settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="72126-110">Bu ayarlar yalnızca uygun yönetici, değil kalıcı yönetici sahip kullanıcıların etkiler.</span><span class="sxs-lookup"><span data-stu-id="72126-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="72126-111">**Etkinleştirme**: hello sürede sona ermeden önce bir rol etkin kalmasını saatleri.</span><span class="sxs-lookup"><span data-stu-id="72126-111">**Activations**: hello time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="72126-112">Bu, 1 ila 72 saat arasında olabilir.</span><span class="sxs-lookup"><span data-stu-id="72126-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="72126-113">**Bildirimleri**: hello sistem rol etkinleştirdikten onaylama e-postaları tooadmins gönderir olsun veya olmasın seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72126-113">**Notifications**: You can choose whether or not hello system sends emails tooadmins confirming that they have activated a role.</span></span> <span data-ttu-id="72126-114">Bu, yetkisiz veya aykırı etkinleştirmeleri algılamak için yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="72126-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="72126-115">**Olay/istek anahtarı**: rolleri etkinleştirdiğinizde toorequire uygun admins tooinclude bir bilet numarası olsun veya olmasın seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72126-115">**Incident/Request Ticket**: You can choose whether or not toorequire eligible admins tooinclude a ticket number when they activate their role.</span></span> <span data-ttu-id="72126-116">Rol erişim denetimleri gerçekleştirdiğinizde bu yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="72126-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="72126-117">**Çok faktörlü kimlik doğrulaması**: seçebileceğiniz desteklemediğini toorequire kullanıcılar tooverify kimliklerini rollerine etkinleştirilebilmesi MFA ile.</span><span class="sxs-lookup"><span data-stu-id="72126-117">**Multi-Factor Authentication**: You can choose whether or not toorequire users tooverify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="72126-118">Bunlar yalnızca bu kez her bir rolü etkinleştirmemek her zaman oturum tooverify gerekir.</span><span class="sxs-lookup"><span data-stu-id="72126-118">They only have tooverify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="72126-119">İki ipuçları tookeep göz önünde MFA etkinleştirin, vardır:</span><span class="sxs-lookup"><span data-stu-id="72126-119">There are two tips tookeep in mind when you enable MFA:</span></span>

* <span data-ttu-id="72126-120">E-postaları için Microsoft hesabına sahip kullanıcıların (genellikle @outlook.com, ancak her zaman) için Azure MFA kaydedilemiyor.</span><span class="sxs-lookup"><span data-stu-id="72126-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="72126-121">Microsoft hesaplarıyla tooassign rolleri toousers istiyorsanız, kalıcı yönetici yapın veya bu rol için MFA devre dışı bırakmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="72126-121">If you want tooassign roles toousers with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="72126-122">MFA için üst düzey ayrıcalıklı rolleri Azure AD için devre dışı bırakamazsınız ve Office365.</span><span class="sxs-lookup"><span data-stu-id="72126-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="72126-123">Bu, bu rolleri dikkatle korunması için bir güvenlik özelliğidir:</span><span class="sxs-lookup"><span data-stu-id="72126-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="72126-124">Uygulama Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="72126-124">Application administrator</span></span>
  * <span data-ttu-id="72126-125">Uygulama Proxy sunucusu Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="72126-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="72126-126">Faturalama Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="72126-126">Billing administrator</span></span>  
  * <span data-ttu-id="72126-127">Uyumluluk Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="72126-127">Compliance administrator</span></span>  
  * <span data-ttu-id="72126-128">CRM Hizmet Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="72126-128">CRM service administrator</span></span>
  * <span data-ttu-id="72126-129">Müşteri kasa erişimi onaylayıcı</span><span class="sxs-lookup"><span data-stu-id="72126-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="72126-130">Directory yazıcısı</span><span class="sxs-lookup"><span data-stu-id="72126-130">Directory writer</span></span>  
  * <span data-ttu-id="72126-131">Exchange Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="72126-131">Exchange administrator</span></span>  
  * <span data-ttu-id="72126-132">Genel yönetici</span><span class="sxs-lookup"><span data-stu-id="72126-132">Global administrator</span></span>
  * <span data-ttu-id="72126-133">Intune Hizmet Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="72126-133">Intune service administrator</span></span>
  * <span data-ttu-id="72126-134">Posta kutusu Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="72126-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="72126-135">İş ortağı tier1 desteği</span><span class="sxs-lookup"><span data-stu-id="72126-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="72126-136">İş ortağı tier2 desteği</span><span class="sxs-lookup"><span data-stu-id="72126-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="72126-137">Ayrıcalıklı Rol Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="72126-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="72126-138">Güvenlik yöneticisi</span><span class="sxs-lookup"><span data-stu-id="72126-138">Security administrator</span></span>  
  * <span data-ttu-id="72126-139">SharePoint Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="72126-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="72126-140">Skype Kurumsal yöneticisi</span><span class="sxs-lookup"><span data-stu-id="72126-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="72126-141">Kullanıcı Hesap Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="72126-141">User account administrator</span></span>  

<span data-ttu-id="72126-142">MFA ile PIM kullanma hakkında daha fazla bilgi için bkz: [nasıl tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="72126-142">For more information about using MFA with PIM see [How tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="72126-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72126-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

