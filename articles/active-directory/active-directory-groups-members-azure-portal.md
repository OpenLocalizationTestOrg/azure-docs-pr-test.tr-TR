---
title: "Azure Active Directory'deki bir gruba aaaManage hello üyeleri | Microsoft Docs"
description: "Nasıl tooadd veya Azure Active Directory'deki bir gruba kullanıcı ve cihazları kaldırma"
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
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="62bff-103">Azure Active Directory kiracınızdaki kullanıcıların Grup üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="62bff-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="62bff-104">Bu makalede nasıl toomanage hello Azure Active Directory'de (Azure AD) grubu için üyeleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="62bff-104">This article explains how toomanage hello members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-hello-members-and-manage-them"></a><span data-ttu-id="62bff-105">Nasıl hello üyeleri bulmak ve onları yönetmeyi?</span><span class="sxs-lookup"><span data-stu-id="62bff-105">How do I find hello members and manage them?</span></span>
1. <span data-ttu-id="62bff-106">İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="62bff-106">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="62bff-107">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="62bff-107">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcı yönetimi](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="62bff-109">Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="62bff-109">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Açılış hello grupları dikey penceresi](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="62bff-111">Merhaba üzerinde **kullanıcılar ve gruplar - tüm grupları** dikey penceresinde, bir grup seçin.</span><span class="sxs-lookup"><span data-stu-id="62bff-111">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="62bff-112">Merhaba üzerinde **grup - *groupname***  dikey penceresinde, select **üyeleri**.</span><span class="sxs-lookup"><span data-stu-id="62bff-112">On hello **Group - *groupname*** blade, select **Members**.</span></span>

   ![Açılış hello üyeleri dikey penceresi](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="62bff-114">Merhaba üzerinde tooadd üyeleri toohello grubu **Grup - üyeleri** dikey penceresinde, select **Add Members**.</span><span class="sxs-lookup"><span data-stu-id="62bff-114">tooadd members toohello group, on hello **Group - Members** blade, select **Add Members**.</span></span>

   ![Üyeleri komut ekleme](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="62bff-116">Merhaba üzerinde **üyeleri** dikey penceresinde, seçin veya daha fazla kullanıcı veya cihazları tooadd toohello grubu ve select hello **seçin** hello hello dikey tooadd sonunda bunları toohello Grup düğme.</span><span class="sxs-lookup"><span data-stu-id="62bff-116">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="62bff-117">Merhaba **kullanıcı** kutusunu filtreleri Merhaba, bir kullanıcı veya aygıt adı girişi tooany parçası eşleşmesini temel alan görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="62bff-117">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="62bff-118">Joker karakterler bu kutuya kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="62bff-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="62bff-119">Merhaba grubundan hello tooremove üyeleri **Grup - üyeleri** dikey penceresinde, bir üye seçin.</span><span class="sxs-lookup"><span data-stu-id="62bff-119">tooremove members from hello group, on hello **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="62bff-120">Merhaba üzerinde ***membername*** dikey penceresinde, select hello **kaldırmak** komut ve hello isteminde Seçiminizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="62bff-120">On hello ***membername*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![Üyeleri komutu kaldırın](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="62bff-122">Merhaba grubunun üyelerini değiştirmeyi tamamladığınızda seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="62bff-122">When you finish changing members for hello group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="62bff-123">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="62bff-123">Additional information</span></span>
<span data-ttu-id="62bff-124">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="62bff-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="62bff-125">Var olan grupları bakın</span><span class="sxs-lookup"><span data-stu-id="62bff-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="62bff-126">Yeni bir grup oluşturun ve üye ekleme</span><span class="sxs-lookup"><span data-stu-id="62bff-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="62bff-127">Bir grubu ayarlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="62bff-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="62bff-128">Bir grubun üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="62bff-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="62bff-129">Bir gruptaki kullanıcılar için dinamik kurallarını yönet</span><span class="sxs-lookup"><span data-stu-id="62bff-129">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
