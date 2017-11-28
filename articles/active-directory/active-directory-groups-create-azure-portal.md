---
title: "Azure Active Directory'de kullanıcılar için bir grubu aaaCreate | Microsoft Docs"
description: "Nasıl toocreate Azure Active Directory'deki bir grup ve üye toohello grubu Ekle"
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
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="decd7-103">Bir grup oluşturun ve Azure Active Directory'de üye ekleme</span><span class="sxs-lookup"><span data-stu-id="decd7-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="decd7-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="decd7-104">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="decd7-105">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="decd7-105">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="decd7-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="decd7-106">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="decd7-107">Bu makalede açıklanır nasıl toocreate ve Azure Active Directory'de yeni bir grubu doldurur.</span><span class="sxs-lookup"><span data-stu-id="decd7-107">This article explains how toocreate and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="decd7-108">Lisans veya izinleri tooa sayısı kullanıcılardan veya aygıtlardan aynı anda atama gibi bir grup tooperform yönetim görevleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="decd7-108">Use a group tooperform management tasks such as assigning licenses or permissions tooa number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="decd7-109">Nasıl grup oluşturulur?</span><span class="sxs-lookup"><span data-stu-id="decd7-109">How do I create a group?</span></span>
1. <span data-ttu-id="decd7-110">İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="decd7-110">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="decd7-111">Seçin **daha fazla hizmet**, girin **kullanıcı ve grupları** hello metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="decd7-111">Select **More services**, enter **User and groups** in hello text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcı yönetimi](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="decd7-113">Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="decd7-113">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Açılış hello grupları dikey penceresi](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="decd7-115">Merhaba üzerinde **kullanıcılar ve gruplar - tüm grupları** dikey penceresinde, select hello **Ekle** komutu.</span><span class="sxs-lookup"><span data-stu-id="decd7-115">On hello **Users and groups - All groups** blade, select hello **Add** command.</span></span>

   ![Merhaba Ekle komutu seçme](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="decd7-117">Merhaba üzerinde **grup** dikey penceresinde, bir ad ve açıklama hello grubu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="decd7-117">On hello **Group** blade, add a name and description for hello group.</span></span>
6. <span data-ttu-id="decd7-118">tooselect üyeleri tooadd toohello grubu, select **atanan** hello içinde **üyelik türü** kutusuna ve ardından **üyeleri**.</span><span class="sxs-lookup"><span data-stu-id="decd7-118">tooselect members tooadd toohello group, select **Assigned** in hello **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="decd7-119">Nasıl toomanage hello bir grubun üyeliğini dinamik olarak hakkında daha fazla bilgi için bkz: [öznitelikleri toocreate kullanarak Gelişmiş Grup üyeliği kuralları](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="decd7-119">For more information about how toomanage hello membership of a group dynamically, see [Using attributes toocreate advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Üyeleri tooadd seçme](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="decd7-121">Merhaba üzerinde **üyeleri** dikey penceresinde, seçin veya daha fazla kullanıcı veya cihazları tooadd toohello grubu ve select hello **seçin** hello hello dikey tooadd sonunda bunları toohello Grup düğme.</span><span class="sxs-lookup"><span data-stu-id="decd7-121">On hello **Members** blade, select one or more users or devices tooadd toohello group and select hello **Select** button at hello bottom of hello blade tooadd them toohello group.</span></span> <span data-ttu-id="decd7-122">Merhaba **kullanıcı** kutusunu filtreleri Merhaba, bir kullanıcı veya aygıt adı girişi tooany parçası eşleşmesini temel alan görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="decd7-122">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="decd7-123">Joker karakterler bu kutuya kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="decd7-123">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="decd7-124">Üyeler toohello grubu eklemeyi bitirdiğinizde, seçin **oluşturma** hello üzerinde **grup** dikey.</span><span class="sxs-lookup"><span data-stu-id="decd7-124">When you finish adding members toohello group, select **Create** on hello **Group** blade.</span></span>    

   ![Grubu onayı oluşturma](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="decd7-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="decd7-126">Next steps</span></span>
<span data-ttu-id="decd7-127">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="decd7-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="decd7-128">Var olan grupları bakın</span><span class="sxs-lookup"><span data-stu-id="decd7-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="decd7-129">Bir grubu ayarlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="decd7-129">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="decd7-130">Bir grubun üyelerini yönetmek</span><span class="sxs-lookup"><span data-stu-id="decd7-130">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="decd7-131">Bir grubun üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="decd7-131">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="decd7-132">Bir gruptaki kullanıcılar için dinamik kurallarını yönet</span><span class="sxs-lookup"><span data-stu-id="decd7-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
