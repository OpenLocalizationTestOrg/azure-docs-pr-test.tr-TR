---
title: "aaaPreview Office 365 grupları Azure Active Directory'de sona erme | Microsoft Docs"
description: "Office 365 için sona erme yukarı tooset Azure Active Directory'de (Önizleme) nasıl grupları"
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
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a><span data-ttu-id="850f8-103">Office 365 grupları süre sonu (Önizleme) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="850f8-103">Configure Office 365 groups expiration (preview)</span></span>

<span data-ttu-id="850f8-104">Seçtiğiniz herhangi bir Office 365 grup için sona erme ayarlayarak artık Office 365 grupları hello yaşam döngüsü yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="850f8-104">You can now manage hello lifecycle of Office 365 groups by setting expiration for any Office 365 groups that you select.</span></span> <span data-ttu-id="850f8-105">Bu süre sonu ayarladıktan sonra bu grupları sahipleri olan hala hello grupları gerekiyorsa bunları gruplara toorenew sorulan.</span><span class="sxs-lookup"><span data-stu-id="850f8-105">Once this expiration is set, owners of those groups are asked toorenew their groups if they still need hello groups.</span></span> <span data-ttu-id="850f8-106">Değil yenilendiğinden herhangi bir Office 365 grubu silinir.</span><span class="sxs-lookup"><span data-stu-id="850f8-106">Any Office 365 group that is not renewed will be deleted.</span></span> <span data-ttu-id="850f8-107">Silindi herhangi bir Office 365 grubu 30 gün içinde hello Grup sahipleri veya hello Yöneticisi tarafından geri yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="850f8-107">Any Office 365 group that was deleted can be restored within 30 days by hello group owners or hello administrator.</span></span>  


> [!NOTE]
> <span data-ttu-id="850f8-108">Süre sonu yalnızca Office 365 grupları için ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="850f8-108">You can set expiration for only Office 365 groups.</span></span>
>
> <span data-ttu-id="850f8-109">O365 grupları için sona erme ayarlamak için bir Azure AD Premium lisansı atanmış gerekiyor</span><span class="sxs-lookup"><span data-stu-id="850f8-109">Setting expiration for O365 groups requires that an Azure AD Premium license is assigned to</span></span>
>   - <span data-ttu-id="850f8-110">Merhaba Kiracı hello süre sonu ayarlarını yapılandıran hello Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="850f8-110">hello administrator who configures hello expiration settings for hello tenant</span></span>
>   - <span data-ttu-id="850f8-111">Bu ayar için seçilmiş hello grupları tüm üyeleri</span><span class="sxs-lookup"><span data-stu-id="850f8-111">All members of hello groups selected for this setting</span></span>

## <a name="set-office-365-groups-expiration"></a><span data-ttu-id="850f8-112">Office 365 grupları sona erme ayarlayın</span><span class="sxs-lookup"><span data-stu-id="850f8-112">Set Office 365 groups expiration</span></span>

1. <span data-ttu-id="850f8-113">Açık hello [Azure AD Yönetim Merkezi](https://aad.portal.azure.com) Azure AD kiracınızda genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="850f8-113">Open hello [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="850f8-114">Açık Azure AD, select **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="850f8-114">Open Azure AD, select **Users and groups**.</span></span>

3. <span data-ttu-id="850f8-115">Seçin **grup ayarları** ve ardından **sona erme** tooopen hello sona erme ayarları.</span><span class="sxs-lookup"><span data-stu-id="850f8-115">Select **Group settings** and then select **Expiration** tooopen hello expiration settings.</span></span>
  
  ![Sona erme dikey penceresi](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. <span data-ttu-id="850f8-117">Merhaba üzerinde **sona erme** dikey penceresinde aşağıdakileri yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="850f8-117">On hello **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="850f8-118">Merhaba Grup ömrü gün olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="850f8-118">Set hello group lifetime in days.</span></span> <span data-ttu-id="850f8-119">Aşağıdakilerden birini seçebilirsiniz hello önceden değerleri veya (olmalıdır 31 gün veya daha fazla) özel bir değer.</span><span class="sxs-lookup"><span data-stu-id="850f8-119">You could select one of hello preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="850f8-120">Bir grup sahibi olduğunda burada hello yenileme ve süre sonu bildirimleri gönderilmesi gereken bir e-posta adresi belirtin.</span><span class="sxs-lookup"><span data-stu-id="850f8-120">Specify an email address where hello renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="850f8-121">Office 365 grupları sona seçin.</span><span class="sxs-lookup"><span data-stu-id="850f8-121">Select which Office 365 groups expire.</span></span> <span data-ttu-id="850f8-122">Süre sonu için etkinleştirebilirsiniz **tüm** Office 365 grupları hello Office 365 grupları kümelerini seçebilirsiniz veya seçtiğiniz **hiçbiri** süre sonu tüm gruplar için devre dışı bırakmak için.</span><span class="sxs-lookup"><span data-stu-id="850f8-122">You can enable expiration for **All** Office 365 groups, you can select from among hello Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="850f8-123">Seçerek bittiğinde ayarlarınızı kaydetmek **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="850f8-123">Save your settings when you're done by selecting **Save**.</span></span>

<span data-ttu-id="850f8-124">Microsoft PowerShell modülü tooconfigure sona erme tarihi Office 365 grupları PowerShell aracılığıyla nasıl toodownload ve yükleme hello ile ilgili yönergeler için bkz: [Azure Active Directory V2 PowerShell modülü - genel Önizleme sürümü 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span><span class="sxs-lookup"><span data-stu-id="850f8-124">For instructions on how toodownload and install hello Microsoft PowerShell module tooconfigure expiration for Office 365 groups via PowerShell, see [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

<span data-ttu-id="850f8-125">Bunun gibi e-posta bildirimleri toohello Office 365 Grup sahiplerinin 30 gün, 15 gün ve 1 gün önceki tooexpiration hello grubunun gönderilir.</span><span class="sxs-lookup"><span data-stu-id="850f8-125">Email notifications such as this one are sent toohello Office 365 group owners 30 days, 15 days, and 1 day prior tooexpiration of hello group.</span></span>

![Sona erme e-posta bildirimi](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

<span data-ttu-id="850f8-127">Merhaba Grup sahibi seçip **yenileme grup** toorenew Office 365 Grup hello ya da seçebilirsiniz **Git toogroup** toosee hello üyeleri ve ilgili diğer ayrıntıları hello grubu.</span><span class="sxs-lookup"><span data-stu-id="850f8-127">hello group owner can then select **Renew group** toorenew hello Office 365 group, or can select **Go toogroup** toosee hello members and other details about hello group.</span></span>

<span data-ttu-id="850f8-128">Bir grup süresi dolduğunda hello Grup bir gün hello sona erme tarihinden sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="850f8-128">When a group expires, hello group is deleted one day after hello expiration date.</span></span> <span data-ttu-id="850f8-129">Merhaba geçerlilik süresi ve bunların Office 365 grubunun sonraki silinmesi hakkında bildiren toohello Office 365 Grup sahipleri bunun gibi bir e-posta bildirimi gönderilir.</span><span class="sxs-lookup"><span data-stu-id="850f8-129">An email notification such as this one is sent toohello Office 365 group owners informing them about hello expiration and subsequent deletion of their Office 365 group.</span></span>

![Grup silme e-posta bildirimi](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

<span data-ttu-id="850f8-131">Merhaba grubu geri yükleyebilirsiniz seçerek **geri yükleme grup** veya [geri yükleme silinmiş bir Office 365 Grup Azure Active Directory'de] bölümünde açıklanan PowerShell cmdlet'lerini kullanarak (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-Restore-Azure-Portal).</span><span class="sxs-lookup"><span data-stu-id="850f8-131">hello group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span></span>
    
<span data-ttu-id="850f8-132">Merhaba grubu geri yüklemekte belgeler, SharePoint siteleri veya diğer kalıcı nesne içeriyorsa, too24 saatleri toofully geri yükleme hello grup ve içeriği alabilir.</span><span class="sxs-lookup"><span data-stu-id="850f8-132">If hello group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up too24 hours toofully restore hello group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="850f8-133">Merhaba sona erme ayarları dağıtırken hello sona erme penceresinden daha eski olan bazı grupları olabilir.</span><span class="sxs-lookup"><span data-stu-id="850f8-133">When deploying hello expiration settings, there might be some groups that are older than hello expiration window.</span></span> <span data-ttu-id="850f8-134">Bu gruplar olması hemen silinmez, ancak olan too30 gün dolmasına ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="850f8-134">These groups are not be immediately deleted, but are set too30 days until expiration.</span></span> <span data-ttu-id="850f8-135">bir gün içinde Hello ilk yenileme bildirim e-posta gönderilir.</span><span class="sxs-lookup"><span data-stu-id="850f8-135">hello first renewal notification email is sent out within a day.</span></span> <span data-ttu-id="850f8-136">Örneğin, grubu A, 400 gün önce oluşturulduğu ve hello sona erme aralığını ayarlanmış too180 gün.</span><span class="sxs-lookup"><span data-stu-id="850f8-136">For example, Group A was created 400 days ago, and hello expiration interval is set too180 days.</span></span> <span data-ttu-id="850f8-137">Sona erme tarihi geçerli olduğunda, onu hello sahibi yeniler sürece gruba silinmeden önce 30 gün sahiptir.</span><span class="sxs-lookup"><span data-stu-id="850f8-137">When you apply expiration settings, Group A has 30 days before it is deleted, unless hello owner renews it.</span></span>
> * <span data-ttu-id="850f8-138">Dinamik bir grup silinir ve geri, yeni Grup ve yeniden doldurulan according toohello kural görülür.</span><span class="sxs-lookup"><span data-stu-id="850f8-138">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according toohello rule.</span></span> <span data-ttu-id="850f8-139">Bu işlemin too24 saat sürebilir.</span><span class="sxs-lookup"><span data-stu-id="850f8-139">This process might take up too24 hours.</span></span>

## <a name="next-steps"></a><span data-ttu-id="850f8-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="850f8-140">Next steps</span></span>
<span data-ttu-id="850f8-141">Bu makaleler Azure AD grupları hakkında ek bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="850f8-141">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="850f8-142">Var olan grupları bakın</span><span class="sxs-lookup"><span data-stu-id="850f8-142">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="850f8-143">Bir grubu ayarlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="850f8-143">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="850f8-144">Bir grubun üyelerini yönetmek</span><span class="sxs-lookup"><span data-stu-id="850f8-144">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="850f8-145">Bir grubun üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="850f8-145">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="850f8-146">Bir gruptaki kullanıcılar için dinamik kurallarını yönet</span><span class="sxs-lookup"><span data-stu-id="850f8-146">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
