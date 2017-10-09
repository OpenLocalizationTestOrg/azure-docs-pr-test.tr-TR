---
title: "aaaView Azure kaynak erişim atamalarını | Microsoft Docs"
description: "Görüntüleme ve herhangi bir kullanıcı veya grup hello Azure portal'ın tüm hello rol tabanlı erişim denetimi atamaları yönetme"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a><span data-ttu-id="91330-103">Kullanıcıları ve grupları hello Azure portalı için erişim atamalarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="91330-103">View access assignments for users and groups in hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="91330-104">Kullanıcı veya gruba göre erişimi yönetme</span><span class="sxs-lookup"><span data-stu-id="91330-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="91330-105">Kaynağa göre erişimi yönetme</span><span class="sxs-lookup"><span data-stu-id="91330-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="91330-106">Rol tabanlı erişim denetimi ile (RBAC) hello Azure Active Directory (Azure AD) içinde erişim tooyour Azure yönetebileceğiniz kaynakları.</span><span class="sxs-lookup"><span data-stu-id="91330-106">With role-based access control (RBAC) in hello Azure Active Directory (Azure AD), you can manage access tooyour Azure resources.</span></span> 

<span data-ttu-id="91330-107">İki yolla hello izinleri kısıtla olduğundan ile RBAC atanmış erişim ayrıntılıdır:</span><span class="sxs-lookup"><span data-stu-id="91330-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict hello permissions:</span></span>

* <span data-ttu-id="91330-108">**Kapsam:** RBAC rolü atamalarını olan kapsamlı tooa belirli abonelik, kaynak grubu veya kaynak.</span><span class="sxs-lookup"><span data-stu-id="91330-108">**Scope:** RBAC role assignments are scoped tooa specific subscription, resource group, or resource.</span></span> <span data-ttu-id="91330-109">Bir kullanıcı tarafından erişim tooa tek kaynak verilen hello alanındaki herhangi bir kaynağa erişemiyor aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="91330-109">A user given access tooa single resource cannot access any other resources in hello same subscription.</span></span>
* <span data-ttu-id="91330-110">**Rol:** hello atama hello kapsamında erişim daraltıldığı rol atama tarafından bile daha fazla.</span><span class="sxs-lookup"><span data-stu-id="91330-110">**Role:** Within hello scope of hello assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="91330-111">Rol sahibi gibi üst düzey ya da sanal makine okuyucu gibi belirli olabilir.</span><span class="sxs-lookup"><span data-stu-id="91330-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="91330-112">Roller yalnızca gelen hello abonelik, kaynak grubu veya hello kapsamı hello ataması için kaynak içinde atanabilir.</span><span class="sxs-lookup"><span data-stu-id="91330-112">Roles can only be assigned from within hello subscription, resource group, or resource that is hello scope for hello assignment.</span></span> <span data-ttu-id="91330-113">Ancak tüm hello erişim atamalarını belirli bir kullanıcı veya grup için tek bir yerde görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91330-113">But you can view all hello access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="91330-114">Her abonelik too2000 rol atamalarında yukarı sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="91330-114">You can have up too2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="91330-115">Çok hakkında daha fazla bilgi almak[rol atamalarını toomanage erişim tooyour Azure abonelik kaynaklarını kullanmak](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="91330-115">Get more information about how too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="91330-116">Erişim atamalarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="91330-116">View access assignments</span></span>
<span data-ttu-id="91330-117">toolook tek bir kullanıcı veya grup için hello erişim atamalarını hello Azure Active Directory'de Başlat [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="91330-117">toolook up hello access assignments for a single user or group, start in Azure Active Directory in hello [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="91330-118">Seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="91330-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="91330-119">Bu seçenek, gezinti listenizde görünür durumda değilse, seçin **daha Hizmetleri** toofind kaydırarak **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="91330-119">If this option is not visible on your navigation list, select **More Services** and then scroll down toofind **Azure Active Directory**.</span></span>
2. <span data-ttu-id="91330-120">Seçin **kullanıcılar ve gruplar**ve sonra da **tüm kullanıcılar** veya **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="91330-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="91330-121">Bu örnekte, bireysel kullanıcılar odaklanın.</span><span class="sxs-lookup"><span data-stu-id="91330-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="91330-122">![Kullanıcıları ve grupları Azure Active Directory'de - ekran görüntüsü yönetin](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="91330-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="91330-123">Merhaba kullanıcı adı veya kullanıcı adı tarafından arayın.</span><span class="sxs-lookup"><span data-stu-id="91330-123">Search for hello user by name or username.</span></span>
4. <span data-ttu-id="91330-124">Seçin **Azure kaynaklarını** hello kullanıcı dikey.</span><span class="sxs-lookup"><span data-stu-id="91330-124">Select **Azure resources** on hello user blade.</span></span> <span data-ttu-id="91330-125">Bu kullanıcı için tüm hello erişim atamaları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="91330-125">All hello access assignments for that user appear.</span></span>

### <a name="read-permissions-tooview-assignments"></a><span data-ttu-id="91330-126">Okuma izinleri tooview atamaları</span><span class="sxs-lookup"><span data-stu-id="91330-126">Read permissions tooview assignments</span></span>
<span data-ttu-id="91330-127">Bu sayfa yalnızca izin tooread sahip hello erişim atamalarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="91330-127">This page only shows hello access assignments that you have permission tooread.</span></span> <span data-ttu-id="91330-128">Örneğin, okuma erişimi toosubscription bir sahip ve bir kullanıcının atamaları toohello Azure kaynaklarını dikey toocheck gidin.</span><span class="sxs-lookup"><span data-stu-id="91330-128">For example, you have read access toosubscription A and go toohello Azure resources blade toocheck a user's assignments.</span></span> <span data-ttu-id="91330-129">Bir abonelik için kendi erişim atamalarını görebilirsiniz, ancak kendisi de B. abonelikte erişim atamaları olduğunu göremez</span><span class="sxs-lookup"><span data-stu-id="91330-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="91330-130">Erişim atamalarını silin</span><span class="sxs-lookup"><span data-stu-id="91330-130">Delete access assignments</span></span>
<span data-ttu-id="91330-131">Bu dikey pencereden tooa kullanıcı veya grup doğrudan atanmış erişim atamalarını silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91330-131">From this blade, you can delete access assignments that were assigned directly tooa user or group.</span></span> <span data-ttu-id="91330-132">Merhaba erişim atama üst gruptan devralınan, toogo toohello kaynak veya abonelik gerekir ve hello atama yönetin.</span><span class="sxs-lookup"><span data-stu-id="91330-132">If hello access assignment was inherited from a parent group, you need toogo toohello resource or subscription and manage hello assignment there.</span></span>

1. <span data-ttu-id="91330-133">Bir kullanıcı veya grup için tüm hello erişim atamalarını Hello listeden toodelete istediğiniz hello birini seçin.</span><span class="sxs-lookup"><span data-stu-id="91330-133">From hello list of all hello access assignments for a user or group, select hello one you want toodelete.</span></span>
2. <span data-ttu-id="91330-134">Seçin **kaldırmak** ve ardından **Evet** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="91330-134">Select **Remove** and then **Yes** tooconfirm.</span></span>
    <span data-ttu-id="91330-135">![Erişim atamayı - ekran görüntüsü](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="91330-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="91330-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="91330-136">Next steps</span></span>

* <span data-ttu-id="91330-137">Rol tabanlı erişim denetimi ile çok başlamak[rol atamalarını toomanage erişim tooyour Azure aboneliği kaynakları kullanın](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="91330-137">Get started with Role-Based Access Control too[Use role assignments toomanage access tooyour Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="91330-138">Merhaba bkz [RBAC yerleşik rolleri](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="91330-138">See hello [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

