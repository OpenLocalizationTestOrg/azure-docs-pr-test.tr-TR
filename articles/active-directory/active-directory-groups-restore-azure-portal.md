---
title: "Azure Active Directory'de aaaRestore silinmiş bir Office 365 Grup | Microsoft Docs"
description: "Azure Active Directory'deki bir gruba toorestore silinen bir grupta, görünüm geri yüklenebilen grupları ve permamnently delete nasıl"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a><span data-ttu-id="e2a80-103">Azure Active Directory silinen bir Office 365 grubunda geri yükleme</span><span class="sxs-lookup"><span data-stu-id="e2a80-103">Restore a deleted Office 365 group in Azure Active Directory</span></span>

<span data-ttu-id="e2a80-104">Hello Azure Active Directory (Azure AD) bir Office 365 grubunda sildiğinizde, silinen hello 30 gün boyunca hello silme tarihinden tutulan ancak görünür grubudur.</span><span class="sxs-lookup"><span data-stu-id="e2a80-104">When you delete an Office 365 group in hello Azure Active Directory (Azure AD), hello deleted group is retained but not visible for 30 days from hello deletion date.</span></span> <span data-ttu-id="e2a80-105">Bu, böylelikle Hello grup ve içeriği gerekirse geri yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="e2a80-105">This is so that hello group and its contents can be restored if needed.</span></span> <span data-ttu-id="e2a80-106">Bu işlev sınırlandırılır özel olarak tooOffice 365 gruplarında Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2a80-106">This functionality is restricted exclusively tooOffice 365 groups in Azure AD.</span></span> <span data-ttu-id="e2a80-107">Güvenlik grupları ve dağıtım grupları için kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="e2a80-107">It is not available for security groups and distribution groups.</span></span>

> [!NOTE] 
> <span data-ttu-id="e2a80-108">Kullanmayan `Remove-MsolGroup` hello Grup kalıcı olarak temizler olduğundan.</span><span class="sxs-lookup"><span data-stu-id="e2a80-108">Don't use `Remove-MsolGroup` because it purges hello group permanently.</span></span> <span data-ttu-id="e2a80-109">Her zaman kullanmak `Remove-AzureADMSGroup` toodelete bir O365 grubu.</span><span class="sxs-lookup"><span data-stu-id="e2a80-109">Always use `Remove-AzureADMSGroup` toodelete an O365 group.</span></span> 

<span data-ttu-id="e2a80-110">gerekli Hello izinler toorestore bir grup hello aşağıdakilerden herhangi birini olabilir:</span><span class="sxs-lookup"><span data-stu-id="e2a80-110">hello permissions required toorestore a group can be any of hello following:</span></span>

<span data-ttu-id="e2a80-111">Rol</span><span class="sxs-lookup"><span data-stu-id="e2a80-111">Role</span></span>  | <span data-ttu-id="e2a80-112">İzinler</span><span class="sxs-lookup"><span data-stu-id="e2a80-112">Permissions</span></span> 
--------- | ---------
<span data-ttu-id="e2a80-113">Şirket Yöneticisi, iş ortağı Tier2 destek ve Intune hizmet yöneticileri</span><span class="sxs-lookup"><span data-stu-id="e2a80-113">Company Administrator, Partner Tier2 support, and InTune Service Admins</span></span> | <span data-ttu-id="e2a80-114">Silinen tüm Office 365 grup geri yükleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e2a80-114">Can restore any deleted Office 365 group</span></span> 
<span data-ttu-id="e2a80-115">Kullanıcı hesabı yönetici ve iş ortağı Tier1 desteği</span><span class="sxs-lookup"><span data-stu-id="e2a80-115">User Account Administrator and Partner Tier1 support</span></span> | <span data-ttu-id="e2a80-116">Silinen herhangi bir Office 365 grup şirket yöneticisi rolüne atanan bu toohello dışında geri yükleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e2a80-116">Can restore any deleted Office 365 group except those assigned toohello Company Administrator role</span></span> 
<span data-ttu-id="e2a80-117">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="e2a80-117">User</span></span> | <span data-ttu-id="e2a80-118">Bunlar ait silinen tüm Office 365 grup geri yükleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="e2a80-118">Can restore any deleted Office 365 group that they owned</span></span> 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a><span data-ttu-id="e2a80-119">Görünüm Merhaba, kullanılabilir toorestore Office 365 gruplarını silindi</span><span class="sxs-lookup"><span data-stu-id="e2a80-119">View hello deleted Office 365 groups that are available toorestore</span></span>
<span data-ttu-id="e2a80-120">olanları ilgilendiğiniz değil henüz kalıcı olarak temizlenmiş veya cmdlet'leri aşağıdaki hello bir hello kullanılan tooview silinmiş hello grupları tooverify olabilir.</span><span class="sxs-lookup"><span data-stu-id="e2a80-120">hello following cmdlets can be used tooview hello deleted groups tooverify that hello one or ones you're interested in have not yet been permanently purged.</span></span> <span data-ttu-id="e2a80-121">Bu cmdlet'ler hello parçası olan [Azure AD PowerShell Modülü](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="e2a80-121">These cmdlets are part of hello [Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span> <span data-ttu-id="e2a80-122">Bu modül hakkında daha fazla bilgi hello bulunabilir [Azure Active Directory PowerShell sürüm 2](/powershell/azure/install-adv2?view=azureadps-2.0) makalesi.</span><span class="sxs-lookup"><span data-stu-id="e2a80-122">More information about this module can be found in hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0) article.</span></span>

1.  <span data-ttu-id="e2a80-123">Aşağıdaki cmdlet'i toodisplay tüm çalışma hello hala kullanılabilir toorestore kiracınızda Office 365 grupları silindi.</span><span class="sxs-lookup"><span data-stu-id="e2a80-123">Run hello following cmdlet toodisplay all deleted Office 365 groups in your tenant that are still available toorestore.</span></span>
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  <span data-ttu-id="e2a80-124">Alternatif olarak, belirli bir grubun hello objectID bildiğiniz (ve 1. adımda hello cmdlet'inden alma varsa), belirli silinen grubun hello cmdlet tooverify aşağıdaki çalışma hello henüz kalıcı olarak temizlendi değil.</span><span class="sxs-lookup"><span data-stu-id="e2a80-124">Alternately, if you know hello objectID of a specific group (and you can get it from hello cmdlet in step 1), run hello following cmdlet tooverify that hello specific deleted group has not yet been permanently purged.</span></span>
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a><span data-ttu-id="e2a80-125">Nasıl toorestore, Office 365 grubu silindi</span><span class="sxs-lookup"><span data-stu-id="e2a80-125">How toorestore your deleted Office 365 group</span></span>
<span data-ttu-id="e2a80-126">Hala kullanılabilir toorestore bu hello grubudur doğruladıktan sonra geri yükleme hello aşağıdaki adımları hello biriyle grubu silindi.</span><span class="sxs-lookup"><span data-stu-id="e2a80-126">Once you have verified that hello group is still available toorestore, restore hello deleted group with one of hello following steps.</span></span> <span data-ttu-id="e2a80-127">Merhaba grubu belgeleri, SP siteleri veya diğer kalıcı nesne içeriyorsa, bir grup ve içeriği too24 saatleri toofully geri geçmesi gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e2a80-127">If hello group contains documents, SP sites, or other persistent objects, it might take up too24 hours toofully restore a group and its contents.</span></span>

1.  <span data-ttu-id="e2a80-128">Çalışma hello cmdlet toorestore hello grup ve içeriği aşağıdaki.</span><span class="sxs-lookup"><span data-stu-id="e2a80-128">Run hello following cmdlet toorestore hello group and its contents.</span></span>
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

<span data-ttu-id="e2a80-129">Alternatif olarak, hello aşağıdaki cmdlet'i toopermanently Kaldır silinmiş hello Grup çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e2a80-129">Alternatively, hello following cmdlet can be run toopermanently remove hello deleted group.</span></span>
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a><span data-ttu-id="e2a80-130">Bu çalışılan nasıl bilebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="e2a80-130">How do you know this worked?</span></span>
<span data-ttu-id="e2a80-131">Merhaba çalıştırmak bir Office 365 Grup başarıyla geri döndürdük tooverify `Get-AzureADGroup –ObjectId <objectId>` hello grubuyla ilgili cmdlet toodisplay bilgileri.</span><span class="sxs-lookup"><span data-stu-id="e2a80-131">tooverify that you’ve successfully restored an Office 365 group, run hello `Get-AzureADGroup –ObjectId <objectId>` cmdlet toodisplay information about hello group.</span></span> <span data-ttu-id="e2a80-132">Merhaba geri yüklendikten sonra isteği tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="e2a80-132">After hello restore request is completed:</span></span>
- <span data-ttu-id="e2a80-133">Merhaba Grup Exchange hello sol gezinti çubuğunda görünür</span><span class="sxs-lookup"><span data-stu-id="e2a80-133">hello group will appear in hello Left nav bar on Exchange</span></span>
- <span data-ttu-id="e2a80-134">Merhaba grubu için Hello planı Planlayıcı görünür</span><span class="sxs-lookup"><span data-stu-id="e2a80-134">hello plan for hello group will appear in Planner</span></span>
- <span data-ttu-id="e2a80-135">Tüm Sharepoint siteleri ve tüm içerikleri kullanılabilir olacak</span><span class="sxs-lookup"><span data-stu-id="e2a80-135">Any Sharepoint sites and all of their contents will be available</span></span>
- <span data-ttu-id="e2a80-136">Merhaba Grup herhangi hello Exchange uç noktaları ve Office 365 grupları destekleyen diğer Office 365 iş yükü erişilebilir</span><span class="sxs-lookup"><span data-stu-id="e2a80-136">hello group can be accessed from any of hello Exchange endpoints and other Office 365 workloads that support Office 365 groups</span></span>


## <a name="next-steps"></a><span data-ttu-id="e2a80-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e2a80-137">Next steps</span></span>
<span data-ttu-id="e2a80-138">Bu makaleler Azure Active Directory gruplarına ek bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="e2a80-138">These articles provide additional information on Azure Active Directory groups.</span></span>

* [<span data-ttu-id="e2a80-139">Var olan grupları bakın</span><span class="sxs-lookup"><span data-stu-id="e2a80-139">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="e2a80-140">Bir grubu ayarlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="e2a80-140">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="e2a80-141">Bir grubun üyelerini yönetmek</span><span class="sxs-lookup"><span data-stu-id="e2a80-141">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="e2a80-142">Bir grubun üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="e2a80-142">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="e2a80-143">Bir gruptaki kullanıcılar için dinamik kurallarını yönet</span><span class="sxs-lookup"><span data-stu-id="e2a80-143">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
