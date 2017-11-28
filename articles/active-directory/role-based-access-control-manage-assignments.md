---
title: "Azure kaynak erişim atamalarını görüntüleyin | Microsoft Docs"
description: "Görüntüleme ve tüm rol tabanlı erişim denetimi atamaları herhangi bir kullanıcı veya grup Azure portalında yönetme"
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
ms.openlocfilehash: 72c695d08bdf5de003d51ffb0768184e1e4d00ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-the-azure-portal"></a><span data-ttu-id="f09c8-103">Kullanıcılar ve gruplar Azure portalında için erişim atamalarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="f09c8-103">View access assignments for users and groups in the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f09c8-104">Kullanıcı veya gruba göre erişimi yönetme</span><span class="sxs-lookup"><span data-stu-id="f09c8-104">Manage access by user or group</span></span>](role-based-access-control-manage-assignments.md)
> * [<span data-ttu-id="f09c8-105">Kaynağa göre erişimi yönetme</span><span class="sxs-lookup"><span data-stu-id="f09c8-105">Manage access by resource</span></span>](role-based-access-control-configure.md)

<span data-ttu-id="f09c8-106">Rol tabanlı erişim denetimi ile (RBAC) Azure Active Directory'de (Azure AD), Azure kaynaklarınıza erişimi yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f09c8-106">With role-based access control (RBAC) in the Azure Active Directory (Azure AD), you can manage access to your Azure resources.</span></span> 

<span data-ttu-id="f09c8-107">RBAC ile atanmış erişim izinleri kısıtla iki yolla olduğundan ayrıntılıdır:</span><span class="sxs-lookup"><span data-stu-id="f09c8-107">Access assigned with RBAC is fine-grained because there are two ways you can restrict the permissions:</span></span>

* <span data-ttu-id="f09c8-108">**Kapsam:** RBAC rolü atamalarını kapsamlı bir belirli aboneliğe, kaynak grubu ya da kaynak.</span><span class="sxs-lookup"><span data-stu-id="f09c8-108">**Scope:** RBAC role assignments are scoped to a specific subscription, resource group, or resource.</span></span> <span data-ttu-id="f09c8-109">Tek bir kaynağa erişim verilen bir kullanıcı aynı abonelik alanındaki herhangi bir kaynağa erişemez.</span><span class="sxs-lookup"><span data-stu-id="f09c8-109">A user given access to a single resource cannot access any other resources in the same subscription.</span></span>
* <span data-ttu-id="f09c8-110">**Rol:** atama kapsamında erişim daraltıldığı rol atama tarafından bile daha fazla.</span><span class="sxs-lookup"><span data-stu-id="f09c8-110">**Role:** Within the scope of the assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="f09c8-111">Rol sahibi gibi üst düzey ya da sanal makine okuyucu gibi belirli olabilir.</span><span class="sxs-lookup"><span data-stu-id="f09c8-111">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="f09c8-112">Roller yalnızca gelen abonelik, kaynak grubu veya atama kapsamı kaynak içinde atanabilir.</span><span class="sxs-lookup"><span data-stu-id="f09c8-112">Roles can only be assigned from within the subscription, resource group, or resource that is the scope for the assignment.</span></span> <span data-ttu-id="f09c8-113">Ancak, belirli bir kullanıcı veya grup için tüm erişim atamalarını tek bir yerde görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f09c8-113">But you can view all the access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="f09c8-114">Her abonelik 2000 rol atamalarında kadar olabilir.</span><span class="sxs-lookup"><span data-stu-id="f09c8-114">You can have up to 2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="f09c8-115">Hakkında daha fazla bilgi almak [Azure aboneliği kaynaklarınıza erişimi yönetmek için rol atamalarını kullanın](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f09c8-115">Get more information about how to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="f09c8-116">Erişim atamalarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="f09c8-116">View access assignments</span></span>
<span data-ttu-id="f09c8-117">Tek bir kullanıcı veya grup erişimi atamaları bakmak için Azure Active Directory'de başlatmak [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f09c8-117">To look up the access assignments for a single user or group, start in Azure Active Directory in the [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="f09c8-118">Seçin **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f09c8-118">Select **Azure Active Directory**.</span></span> <span data-ttu-id="f09c8-119">Bu seçenek, gezinti listenizde görünür durumda değilse, seçin **daha Hizmetleri** ve Bul aşağıya doğru kaydırma **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f09c8-119">If this option is not visible on your navigation list, select **More Services** and then scroll down to find **Azure Active Directory**.</span></span>
2. <span data-ttu-id="f09c8-120">Seçin **kullanıcılar ve gruplar**ve sonra da **tüm kullanıcılar** veya **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="f09c8-120">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="f09c8-121">Bu örnekte, bireysel kullanıcılar odaklanın.</span><span class="sxs-lookup"><span data-stu-id="f09c8-121">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="f09c8-122">![Kullanıcıları ve grupları Azure Active Directory'de - ekran görüntüsü yönetin](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="f09c8-122">![Manage users and groups in Azure Active Directory - screenshot](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="f09c8-123">Kullanıcı adı veya kullanıcı adı tarafından arayın.</span><span class="sxs-lookup"><span data-stu-id="f09c8-123">Search for the user by name or username.</span></span>
4. <span data-ttu-id="f09c8-124">Kullanıcı dikey penceresinde **Azure kaynakları**'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="f09c8-124">Select **Azure resources** on the user blade.</span></span> <span data-ttu-id="f09c8-125">Söz konusu kullanıcının tüm erişim atamaları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f09c8-125">All the access assignments for that user appear.</span></span>

### <a name="read-permissions-to-view-assignments"></a><span data-ttu-id="f09c8-126">Atamalarını görüntülemek için Okuma izinleri</span><span class="sxs-lookup"><span data-stu-id="f09c8-126">Read permissions to view assignments</span></span>
<span data-ttu-id="f09c8-127">Bu sayfa yalnızca okuma iznine sahip olması için erişim atamalarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f09c8-127">This page only shows the access assignments that you have permission to read.</span></span> <span data-ttu-id="f09c8-128">Örneğin, abonelik A okuma erişimine sahip olması ve bir kullanıcının atamaları denetlemek için Azure kaynaklarını dikey penceresine gidin.</span><span class="sxs-lookup"><span data-stu-id="f09c8-128">For example, you have read access to subscription A and go to the Azure resources blade to check a user's assignments.</span></span> <span data-ttu-id="f09c8-129">Bir abonelik için kendi erişim atamalarını görebilirsiniz, ancak kendisi de B. abonelikte erişim atamaları olduğunu göremez</span><span class="sxs-lookup"><span data-stu-id="f09c8-129">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="f09c8-130">Erişim atamalarını silin</span><span class="sxs-lookup"><span data-stu-id="f09c8-130">Delete access assignments</span></span>
<span data-ttu-id="f09c8-131">Bu dikey pencereden bir kullanıcı veya grup için atanmış erişim atamalarını silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f09c8-131">From this blade, you can delete access assignments that were assigned directly to a user or group.</span></span> <span data-ttu-id="f09c8-132">Erişim atama üst gruptan devralınan, kaynak veya abonelik gidin ve atama var. yönetmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="f09c8-132">If the access assignment was inherited from a parent group, you need to go to the resource or subscription and manage the assignment there.</span></span>

1. <span data-ttu-id="f09c8-133">Bir kullanıcı veya grup için tüm erişim atamalarını listesinden silmek istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="f09c8-133">From the list of all the access assignments for a user or group, select the one you want to delete.</span></span>
2. <span data-ttu-id="f09c8-134">Seçin **kaldırmak** ve ardından **Evet** onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="f09c8-134">Select **Remove** and then **Yes** to confirm.</span></span>
    <span data-ttu-id="f09c8-135">![Erişim atamayı - ekran görüntüsü](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="f09c8-135">![Remove access assignment - screenshot](./media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f09c8-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f09c8-136">Next steps</span></span>

* <span data-ttu-id="f09c8-137">Rol tabanlı erişim denetimi ile çalışmaya başlama [Azure aboneliği kaynaklarınıza erişimi yönetmek için rol atamalarını kullanın](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="f09c8-137">Get started with Role-Based Access Control to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="f09c8-138">Bkz. [RBAC yerleşik rolleri](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="f09c8-138">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>

