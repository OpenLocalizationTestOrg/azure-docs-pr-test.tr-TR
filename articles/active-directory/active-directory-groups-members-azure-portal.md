---
title: "Azure Active Directory'deki bir gruba üye yönetme | Microsoft Docs"
description: "Ekleme veya Azure Active Directory'deki bir gruba kullanıcı ve cihazları kaldırma"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 044e88f95712e1cc5b5532f5492c78d711a8d858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="b755b-103">Azure Active Directory kiracınızdaki kullanıcıların Grup üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="b755b-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="b755b-104">Bu makalede, Azure Active Directory'de (Azure AD) bir grup üyelerini yönetmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b755b-104">This article explains how to manage the members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-the-members-and-manage-them"></a><span data-ttu-id="b755b-105">Nasıl üyeleri bulmak ve onları yönetmeyi?</span><span class="sxs-lookup"><span data-stu-id="b755b-105">How do I find the members and manage them?</span></span>
1. <span data-ttu-id="b755b-106">Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="b755b-106">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="b755b-107">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b755b-107">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcı yönetimi](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="b755b-109">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="b755b-109">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Grupları dikey penceresini açma](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="b755b-111">Üzerinde **kullanıcılar ve gruplar - tüm grupları** dikey penceresinde, bir grup seçin.</span><span class="sxs-lookup"><span data-stu-id="b755b-111">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="b755b-112">Üzerinde **grup - *groupname***  dikey penceresinde, select **üyeleri**.</span><span class="sxs-lookup"><span data-stu-id="b755b-112">On the **Group - *groupname*** blade, select **Members**.</span></span>

   ![Üyeleri dikey penceresini açma](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="b755b-114">Üzerinde grubuna üye eklemek için **Grup - üyeleri** dikey penceresinde, select **Add Members**.</span><span class="sxs-lookup"><span data-stu-id="b755b-114">To add members to the group, on the **Group - Members** blade, select **Add Members**.</span></span>

   ![Üyeleri komut ekleme](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="b755b-116">Üzerinde **üyeleri** dikey penceresinde, select bir veya daha fazla kullanıcılara veya cihazlara grubuna eklemeniz ve seçin **seçin** grubuna eklemek için dikey pencerenin altındaki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="b755b-116">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="b755b-117">**Kullanıcı** kutusu, bir kullanıcı veya aygıt adı herhangi bir kısmını girişe eşleşmesini temel alan görüntü filtreler.</span><span class="sxs-lookup"><span data-stu-id="b755b-117">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="b755b-118">Joker karakterler bu kutuya kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="b755b-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="b755b-119">Üzerinde grubundan üye kaldırma **Grup - üyeleri** dikey penceresinde, bir üye seçin.</span><span class="sxs-lookup"><span data-stu-id="b755b-119">To remove members from the group, on the **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="b755b-120">Üzerinde ***membername*** dikey penceresinde, select **kaldırmak** komut ve komut isteminde Seçiminizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="b755b-120">On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![Üyeleri komutu kaldırın](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="b755b-122">Grubunun üyelerini değiştirmeyi tamamladığınızda seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="b755b-122">When you finish changing members for the group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="b755b-123">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="b755b-123">Additional information</span></span>
<span data-ttu-id="b755b-124">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b755b-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="b755b-125">Var olan grupları bakın</span><span class="sxs-lookup"><span data-stu-id="b755b-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="b755b-126">Yeni bir grup oluşturun ve üye ekleme</span><span class="sxs-lookup"><span data-stu-id="b755b-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="b755b-127">Bir grubu ayarlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="b755b-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="b755b-128">Bir grubun üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="b755b-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="b755b-129">Bir gruptaki kullanıcılar için dinamik kurallarını yönet</span><span class="sxs-lookup"><span data-stu-id="b755b-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
