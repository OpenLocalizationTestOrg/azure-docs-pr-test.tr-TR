---
title: "Grubunuza ait Azure Active Directory içinde grupları yönetme | Microsoft Docs"
description: "Gruplar, diğer grupları Azure Active Directory'de içerebilir. Aşağıda, bu üyeliklerin yönetme verilmiştir."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 08e04a6590176c4084ca47b4bd6cbb22500eca2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="9c184-104">Yönetmek için hangi grupların Azure Active Directory kiracınızda bir grup ait</span><span class="sxs-lookup"><span data-stu-id="9c184-104">Manage to which groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="9c184-105">Gruplar, diğer grupları Azure Active Directory'de içerebilir.</span><span class="sxs-lookup"><span data-stu-id="9c184-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="9c184-106">Aşağıda, bu üyeliklerin yönetme verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9c184-106">Here's how to manage those memberships.</span></span>

## <a name="how-do-i-find-the-groups-my-group-is-a-member-of"></a><span data-ttu-id="9c184-107">Grubunuza üye olduğu grupları nasıl bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="9c184-107">How do I find the groups my group is a member of?</span></span>
1. <span data-ttu-id="9c184-108">Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="9c184-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="9c184-109">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="9c184-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcı yönetimi](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="9c184-111">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="9c184-111">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Grupları dikey penceresini açma](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="9c184-113">Üzerinde **kullanıcılar ve gruplar - tüm grupları** dikey penceresinde, bir grup seçin.</span><span class="sxs-lookup"><span data-stu-id="9c184-113">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="9c184-114">Üzerinde **grup - *groupname***  dikey penceresinde, select **grup üyeliklerini**.</span><span class="sxs-lookup"><span data-stu-id="9c184-114">On the **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Grup üyelikleri dikey penceresini açma](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="9c184-116">Grubunuzun başka bir grubun üyesi olarak eklemek için **Grup - grup üyeliklerini** dikey penceresinde, select **Ekle** komutu.</span><span class="sxs-lookup"><span data-stu-id="9c184-116">To add your group as a member of another group, on the **Group - Group memberships** blade, select the **Add** command.</span></span>
7. <span data-ttu-id="9c184-117">Bir grup seçin **Grup Seç** dikey ve ardından **seçin** dikey pencerenin altındaki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="9c184-117">Select a group from the **Select Group** blade, and then select the **Select** button at the bottom of the blade.</span></span> <span data-ttu-id="9c184-118">Grubunuzun aynı anda yalnızca bir gruba ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c184-118">You can add your group to only one group at a time.</span></span> <span data-ttu-id="9c184-119">**Kullanıcı** kutusu, bir kullanıcı veya aygıt adı herhangi bir kısmını girişe eşleşmesini temel alan görüntü filtreler.</span><span class="sxs-lookup"><span data-stu-id="9c184-119">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="9c184-120">Joker karakterler bu kutuya kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="9c184-120">No wildcard characters are accepted in that box.</span></span>

   ![Bir grup üyeliği ekleme](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="9c184-122">Başka bir grubun üyesi olarak grubunuzun kaldırmak için **Grup - grup üyeliklerini** dikey penceresinde, bir grup seçin.</span><span class="sxs-lookup"><span data-stu-id="9c184-122">To remove your group as a member of another group, on the **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="9c184-123">Üzerinde ***groupname*** dikey penceresinde, select **kaldırmak** komut ve komut isteminde Seçiminizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="9c184-123">On the ***groupname*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![Üyelik komutu kaldırın](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="9c184-125">Grubunuz için grup üyeliklerini değiştirme işiniz bittiğinde, seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="9c184-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="9c184-126">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="9c184-126">Additional information</span></span>
<span data-ttu-id="9c184-127">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="9c184-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="9c184-128">Var olan grupları bakın</span><span class="sxs-lookup"><span data-stu-id="9c184-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="9c184-129">Yeni bir grup oluşturun ve üye ekleme</span><span class="sxs-lookup"><span data-stu-id="9c184-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="9c184-130">Bir grubu ayarlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="9c184-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="9c184-131">Bir grubun üyelerini yönetmek</span><span class="sxs-lookup"><span data-stu-id="9c184-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="9c184-132">Bir gruptaki kullanıcılar için dinamik kurallarını yönet</span><span class="sxs-lookup"><span data-stu-id="9c184-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
