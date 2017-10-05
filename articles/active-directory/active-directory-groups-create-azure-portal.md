---
title: "Azure Active Directory'de kullanıcılar için bir grubu oluşturma | Microsoft Docs"
description: "Azure Active Directory'de bir grup oluşturma ve gruba üye ekleme"
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
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d3d37761a9fdf9bd9801396d45f2fcd47efb0be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="a663d-103">Bir grup oluşturun ve Azure Active Directory'de üye ekleme</span><span class="sxs-lookup"><span data-stu-id="a663d-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a663d-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="a663d-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="a663d-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="a663d-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="a663d-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a663d-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="a663d-107">Bu makalede, oluşturma ve Azure Active Directory'de yeni bir grubu doldurmak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a663d-107">This article explains how to create and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="a663d-108">Lisans veya izinleri bir kullanıcı veya cihaz sayısı için aynı anda atama gibi yönetim görevleri gerçekleştirmek için bir grup kullanın.</span><span class="sxs-lookup"><span data-stu-id="a663d-108">Use a group to perform management tasks such as assigning licenses or permissions to a number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="a663d-109">Nasıl grup oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="a663d-109">How do I create a group?</span></span>
1. <span data-ttu-id="a663d-110">Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="a663d-110">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="a663d-111">Seçin **daha fazla hizmet**, girin **kullanıcı ve grupları** metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="a663d-111">Select **More services**, enter **User and groups** in the text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcı yönetimi](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="a663d-113">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="a663d-113">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Grupları dikey penceresini açma](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="a663d-115">Üzerinde **kullanıcılar ve gruplar - tüm grupları** dikey penceresinde, select **Ekle** komutu.</span><span class="sxs-lookup"><span data-stu-id="a663d-115">On the **Users and groups - All groups** blade, select the **Add** command.</span></span>

   ![Ekle komutu seçme](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="a663d-117">Üzerinde **grup** dikey penceresinde, bir ad ve Grup açıklamasını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a663d-117">On the **Group** blade, add a name and description for the group.</span></span>
6. <span data-ttu-id="a663d-118">Gruba eklenecek üyeleri seçmek için **atanan** içinde **üyelik türü** kutusuna ve ardından **üyeleri**.</span><span class="sxs-lookup"><span data-stu-id="a663d-118">To select members to add to the group, select **Assigned** in the **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="a663d-119">Bir grubun üyeliğini dinamik olarak yönetme hakkında daha fazla bilgi için bkz: [grup üyeliği için Gelişmiş kurallar oluşturmak için öznitelikleri kullanma](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a663d-119">For more information about how to manage the membership of a group dynamically, see [Using attributes to create advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Eklenecek üyeleri seçme](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="a663d-121">Üzerinde **üyeleri** dikey penceresinde, select bir veya daha fazla kullanıcılara veya cihazlara grubuna eklemeniz ve seçin **seçin** grubuna eklemek için dikey pencerenin altındaki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="a663d-121">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="a663d-122">**Kullanıcı** kutusu, bir kullanıcı veya aygıt adı herhangi bir kısmını girişe eşleşmesini temel alan görüntü filtreler.</span><span class="sxs-lookup"><span data-stu-id="a663d-122">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="a663d-123">Joker karakterler bu kutuya kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="a663d-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="a663d-124">Üyeleri gruba eklemeyi bitirdiğinizde, seçin **oluşturma** üzerinde **grup** dikey.</span><span class="sxs-lookup"><span data-stu-id="a663d-124">When you finish adding members to the group, select **Create** on the **Group** blade.</span></span>    

   ![Grubu onayı oluşturma](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="a663d-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a663d-126">Next steps</span></span>
<span data-ttu-id="a663d-127">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a663d-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="a663d-128">Var olan grupları bakın</span><span class="sxs-lookup"><span data-stu-id="a663d-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="a663d-129">Bir grubu ayarlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="a663d-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="a663d-130">Bir grubun üyelerini yönetmek</span><span class="sxs-lookup"><span data-stu-id="a663d-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="a663d-131">Bir grubun üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="a663d-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="a663d-132">Bir gruptaki kullanıcılar için dinamik kurallarını yönet</span><span class="sxs-lookup"><span data-stu-id="a663d-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
