---
title: "Office 365 grupları sona erme Azure Active Directory'de Önizleme | Microsoft Docs"
description: "Office 365 grupları Azure Active Directory'de (Önizleme) için sona erme kurma"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: 8a43df84fd050d7b4bd8d937b8c55e744cb805d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a><span data-ttu-id="212fc-103">Office 365 grupları süre sonu (Önizleme) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="212fc-103">Configure Office 365 groups expiration (preview)</span></span>

<span data-ttu-id="212fc-104">Seçtiğiniz herhangi bir Office 365 grup için sona erme ayarlayarak artık Office 365 grupları yaşam döngüsü yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="212fc-104">You can now manage the lifecycle of Office 365 groups by setting expiration for any Office 365 groups that you select.</span></span> <span data-ttu-id="212fc-105">Bu süre sonu ayarladıktan sonra bu grupları sahipleri hala grupları gerekiyorsa bunları gruplara yenileme istenir.</span><span class="sxs-lookup"><span data-stu-id="212fc-105">Once this expiration is set, owners of those groups are asked to renew their groups if they still need the groups.</span></span> <span data-ttu-id="212fc-106">Değil yenilendiğinden herhangi bir Office 365 grubu silinir.</span><span class="sxs-lookup"><span data-stu-id="212fc-106">Any Office 365 group that is not renewed will be deleted.</span></span> <span data-ttu-id="212fc-107">Silindi herhangi bir Office 365 grubu 30 gün içinde grup sahiplerine veya yönetici tarafından geri yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="212fc-107">Any Office 365 group that was deleted can be restored within 30 days by the group owners or the administrator.</span></span>  


> [!NOTE]
> <span data-ttu-id="212fc-108">Süre sonu yalnızca Office 365 grupları için ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="212fc-108">You can set expiration for only Office 365 groups.</span></span>
>
> <span data-ttu-id="212fc-109">O365 grupları için sona erme ayarlamak için bir Azure AD Premium lisansı atanmış gerekiyor</span><span class="sxs-lookup"><span data-stu-id="212fc-109">Setting expiration for O365 groups requires that an Azure AD Premium license is assigned to</span></span>
>   - <span data-ttu-id="212fc-110">Kiracı için sona erme ayarları yapılandıran yönetici</span><span class="sxs-lookup"><span data-stu-id="212fc-110">The administrator who configures the expiration settings for the tenant</span></span>
>   - <span data-ttu-id="212fc-111">Bu ayar için seçili grupların tüm üyeleri</span><span class="sxs-lookup"><span data-stu-id="212fc-111">All members of the groups selected for this setting</span></span>

## <a name="set-office-365-groups-expiration"></a><span data-ttu-id="212fc-112">Office 365 grupları sona erme ayarlayın</span><span class="sxs-lookup"><span data-stu-id="212fc-112">Set Office 365 groups expiration</span></span>

1. <span data-ttu-id="212fc-113">Açık [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) Azure AD kiracınızda genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="212fc-113">Open the [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="212fc-114">Açık Azure AD, select **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="212fc-114">Open Azure AD, select **Users and groups**.</span></span>

3. <span data-ttu-id="212fc-115">Seçin **grup ayarları** ve ardından **sona erme** süre sonu ayarlarını açın.</span><span class="sxs-lookup"><span data-stu-id="212fc-115">Select **Group settings** and then select **Expiration** to open the expiration settings.</span></span>
  
  ![Sona erme dikey penceresi](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. <span data-ttu-id="212fc-117">Üzerinde **sona erme** dikey penceresinde aşağıdakileri yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="212fc-117">On the **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="212fc-118">Grup ömrü gün olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="212fc-118">Set the group lifetime in days.</span></span> <span data-ttu-id="212fc-119">Hazır değerlerden ya da (31 gün veya daha uzun olmalıdır) özel bir değer birini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="212fc-119">You could select one of the preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="212fc-120">Bir grup sahibi olduğunda burada yenileme ve süre sonu bildirimleri gönderilmesi gereken bir e-posta adresi belirtin.</span><span class="sxs-lookup"><span data-stu-id="212fc-120">Specify an email address where the renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="212fc-121">Office 365 grupları sona seçin.</span><span class="sxs-lookup"><span data-stu-id="212fc-121">Select which Office 365 groups expire.</span></span> <span data-ttu-id="212fc-122">Süre sonu için etkinleştirebilirsiniz **tüm** Office 365 grupları, Office 365 grupları kümelerini seçebilirsiniz veya seçtiğiniz **hiçbiri** süre sonu tüm gruplar için devre dışı bırakmak için.</span><span class="sxs-lookup"><span data-stu-id="212fc-122">You can enable expiration for **All** Office 365 groups, you can select from among the Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="212fc-123">Seçerek bittiğinde ayarlarınızı kaydetmek **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="212fc-123">Save your settings when you're done by selecting **Save**.</span></span>

<span data-ttu-id="212fc-124">Süre sonu için PowerShell aracılığıyla Office 365 grupları yapılandırmak yönergeler için karşıdan yüklemek ve Microsoft PowerShell modülünü yüklemek, bkz: [Azure Active Directory V2 PowerShell modülü - genel Önizleme sürümü 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span><span class="sxs-lookup"><span data-stu-id="212fc-124">For instructions on how to download and install the Microsoft PowerShell module to configure expiration for Office 365 groups via PowerShell, see [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

<span data-ttu-id="212fc-125">Bunun gibi e-posta bildirimleri 30 gün, 15 gün ve 1 gün grubunun süre sonundan önce Office 365 grup sahiplerine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="212fc-125">Email notifications such as this one are sent to the Office 365 group owners 30 days, 15 days, and 1 day prior to expiration of the group.</span></span>

![Sona erme e-posta bildirimi](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

<span data-ttu-id="212fc-127">Grup sahibi sonra seçebilirsiniz **yenileme grup** Office 365 yenilemek için grubu ya da seçebilirsiniz **Grup Git** üyeleri ve grubu ile ilgili diğer ayrıntıları görmek için.</span><span class="sxs-lookup"><span data-stu-id="212fc-127">The group owner can then select **Renew group** to renew the Office 365 group, or can select **Go to group** to see the members and other details about the group.</span></span>

<span data-ttu-id="212fc-128">Bir grup süresi dolduğunda, Grup bir gün sonra sona erme tarihini silinir.</span><span class="sxs-lookup"><span data-stu-id="212fc-128">When a group expires, the group is deleted one day after the expiration date.</span></span> <span data-ttu-id="212fc-129">Bunun gibi bir e-posta bildirimi geçerlilik süresi ve bunların Office 365 grubunun sonraki silinmesi hakkında bildiren Office 365 grup sahiplerine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="212fc-129">An email notification such as this one is sent to the Office 365 group owners informing them about the expiration and subsequent deletion of their Office 365 group.</span></span>

![Grup silme e-posta bildirimi](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

<span data-ttu-id="212fc-131">Grup seçerek geri yüklenebilir **geri yükleme grup** veya [geri yükleme silinmiş bir Office 365 Grup Azure Active Directory'de] bölümünde açıklanan PowerShell cmdlet'lerini kullanarak (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-Restore-Azure-Portal).</span><span class="sxs-lookup"><span data-stu-id="212fc-131">The group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span></span>
    
<span data-ttu-id="212fc-132">Geri yüklemekte grubu belgeleri, SharePoint siteleri veya diğer kalıcı nesne içeriyorsa, Grup ve içeriği tam olarak geri 24 saate kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="212fc-132">If the group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up to 24 hours to fully restore the group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="212fc-133">Sona erme ayarları dağıtırken, sona erme penceresinden daha eski olan bazı grupları olabilir.</span><span class="sxs-lookup"><span data-stu-id="212fc-133">When deploying the expiration settings, there might be some groups that are older than the expiration window.</span></span> <span data-ttu-id="212fc-134">Bu gruplar olması hemen silinmez, ancak 30 güne kadar sona erme ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="212fc-134">These groups are not be immediately deleted, but are set to 30 days until expiration.</span></span> <span data-ttu-id="212fc-135">Bir gün içinde ilk yenileme bildirim e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="212fc-135">The first renewal notification email is sent out within a day.</span></span> <span data-ttu-id="212fc-136">Örneğin, grubu A 400 gün önce oluşturulmuş ve sona erme aralığını 180 gün olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="212fc-136">For example, Group A was created 400 days ago, and the expiration interval is set to 180 days.</span></span> <span data-ttu-id="212fc-137">Sona erme tarihi geçerli olduğunda, gruba sahibi, yeniler sürece silinmeden önce 30 gün sahiptir.</span><span class="sxs-lookup"><span data-stu-id="212fc-137">When you apply expiration settings, Group A has 30 days before it is deleted, unless the owner renews it.</span></span>
> * <span data-ttu-id="212fc-138">Dinamik bir grup silinir ve geri, yeni bir grup olarak görülen ve kuralına göre yeniden doldurulur.</span><span class="sxs-lookup"><span data-stu-id="212fc-138">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according to the rule.</span></span> <span data-ttu-id="212fc-139">Bu işlem, 24 saate kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="212fc-139">This process might take up to 24 hours.</span></span>

## <a name="next-steps"></a><span data-ttu-id="212fc-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="212fc-140">Next steps</span></span>
<span data-ttu-id="212fc-141">Bu makaleler Azure AD grupları hakkında ek bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="212fc-141">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="212fc-142">Var olan grupları bakın</span><span class="sxs-lookup"><span data-stu-id="212fc-142">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="212fc-143">Bir grubu ayarlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="212fc-143">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="212fc-144">Bir grubun üyelerini yönetmek</span><span class="sxs-lookup"><span data-stu-id="212fc-144">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="212fc-145">Bir grubun üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="212fc-145">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="212fc-146">Bir gruptaki kullanıcılar için dinamik kurallarını yönet</span><span class="sxs-lookup"><span data-stu-id="212fc-146">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
