---
title: "aaaTenant yönetici yükseltmesine erişim - Azure AD | Microsoft Docs"
description: "Bu konu, rol tabanlı erişim denetimi (RBAC) rollerini yerleşik hello açıklar."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: rqureshi
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andredm
ms.openlocfilehash: 7996f2af3277dc40e2a1766cc4a7862a2399cdef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="fcf04-103">Rol tabanlı erişim denetimi ile bir kiracı Yöneticisi olarak erişimini yükseltme</span><span class="sxs-lookup"><span data-stu-id="fcf04-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="fcf04-104">Rol tabanlı erişim denetimi normalden daha yüksek izinleri verebilirsiniz geçici yükseltmeleri erişim elde Kiracı Yöneticiler yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="fcf04-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="fcf04-105">Bir kiracı Yöneticisi kendisini gerektiğinde toohello kullanıcı erişimi yöneticisi rolü yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcf04-105">A tenant admin can elevate herself toohello User Access Administrator role when needed.</span></span> <span data-ttu-id="fcf04-106">Bu rol hello verir yönetici izinleri toogrant kendisini veya başkalarının Kiracı hello rollerini "/" kapsamı.</span><span class="sxs-lookup"><span data-stu-id="fcf04-106">That role gives hello tenant admin permissions toogrant herself or others roles at hello "/" scope.</span></span>

<span data-ttu-id="fcf04-107">Bu özellik, tüm kuruluştaki mevcut abonelikleri Merhaba yönetici toosee hello Kiracı izin verdiği için önemlidir.</span><span class="sxs-lookup"><span data-stu-id="fcf04-107">This feature is important because it allows hello tenant admin toosee all hello subscriptions that exist in an organization.</span></span> <span data-ttu-id="fcf04-108">Ayrıca, otomasyon (örneğin, faturalama ve denetimi) uygulamaları tooaccess için tüm hello aboneliklere izin verir ve faturalama veya varlık yönetim hello kuruluş hello durumunu doğru bir görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="fcf04-108">It also allows for automation apps (like invoicing and auditing) tooaccess all hello subscriptions and provide an accurate view of hello state of hello organization for billing or asset management.</span></span>  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a><span data-ttu-id="fcf04-109">Nasıl toouse elevateAccess toogive Kiracı erişim</span><span class="sxs-lookup"><span data-stu-id="fcf04-109">How toouse elevateAccess toogive tenant access</span></span>

<span data-ttu-id="fcf04-110">Merhaba temel işlem aşağıdaki adımları hello ile çalışır:</span><span class="sxs-lookup"><span data-stu-id="fcf04-110">hello basic process works with hello following steps:</span></span>

1. <span data-ttu-id="fcf04-111">REST kullanarak, çağrı *elevateAccess*, kullanıcı erişimi yöneticisi rolü hello "/" kapsam hangi verir.</span><span class="sxs-lookup"><span data-stu-id="fcf04-111">Using REST, call *elevateAccess*, which grants you hello User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="fcf04-112">Oluşturma bir [rol ataması](/rest/api/authorization/roleassignments) tooassign herhangi kapsamındaki herhangi bir rolü.</span><span class="sxs-lookup"><span data-stu-id="fcf04-112">Create a [role assignment](/rest/api/authorization/roleassignments) tooassign any role at any scope.</span></span> <span data-ttu-id="fcf04-113">Aşağıdaki örneğine hello atamak için hello özellikleri, okuyucu rolüne hello "/" kapsam gösterir:</span><span class="sxs-lookup"><span data-stu-id="fcf04-113">hello following example shows hello properties for assigning hello Reader role at "/" scope:</span></span>

    ```
    { "properties":{
    "roleDefinitionId": "providers/Microsoft.Authorization/roleDefinitions/acdd72a7338548efbd42f606fba81ae7",
    "principalId": "cbc5e050-d7cd-4310-813b-4870be8ef5bb",
    "scope": "/"
    },
    "id": "providers/Microsoft.Authorization/roleAssignments/64736CA0-56D7-4A94-A551-973C2FE7888B",
    "type": "Microsoft.Authorization/roleAssignments",
    "name": "64736CA0-56D7-4A94-A551-973C2FE7888B"
    }
    ```

3. <span data-ttu-id="fcf04-114">Kullanıcı erişim yönetimi sırasında de rol atamaları olarak sil "/" kapsam.</span><span class="sxs-lookup"><span data-stu-id="fcf04-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="fcf04-115">Gerektiğinde kadar kullanıcı erişimi yönetici ayrıcalıkları iptal edin.</span><span class="sxs-lookup"><span data-stu-id="fcf04-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-tooundo-hello-elevateaccess-action"></a><span data-ttu-id="fcf04-116">Nasıl tooundo hello elevateAccess eylem</span><span class="sxs-lookup"><span data-stu-id="fcf04-116">How tooundo hello elevateAccess action</span></span>

<span data-ttu-id="fcf04-117">Çağırdığınızda *elevateAccess* kendiniz için bir rol ataması oluşturma, toorevoke olanlar ayrıcalıkları şekilde toodelete atama hello.</span><span class="sxs-lookup"><span data-stu-id="fcf04-117">When you call *elevateAccess* you create a role assignment for yourself, so toorevoke those privileges you need toodelete hello assignment.</span></span>

1.  <span data-ttu-id="fcf04-118">Çağrı [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) burada roleName = kullanıcı erişimi Yöneticisi toodetermine hello adı hello kullanıcı erişimi yöneticisi rolünün bir GUID.</span><span class="sxs-lookup"><span data-stu-id="fcf04-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator toodetermine hello name GUID of hello User Access Administrator role.</span></span> <span data-ttu-id="fcf04-119">Merhaba yanıt aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="fcf04-119">hello response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access tooAzure resources.",
    "assignableScopes":["/"],
    "permissions":[{"actions":["*/read","Microsoft.Authorization/*","Microsoft.Support/*"],"notActions":[]}],
    "createdOn":"0001-01-01T08:00:00.0000000Z",
    "updatedOn":"2016-05-31T23:14:04.6964687Z",
    "createdBy":null,
    "updatedBy":null},
    "id":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "type":"Microsoft.Authorization/roleDefinitions",
    "name":"18d7d88d-d35e-4fb5-a5c3-7773c20a72d9"}],
    "nextLink":null}
    ```

    <span data-ttu-id="fcf04-120">Hello Hello GUID Kaydet *adı* parametresi, bu durumda **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="fcf04-120">Save hello GUID from hello *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="fcf04-121">Çağrı [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) burada Principalıd kendi objectID =.</span><span class="sxs-lookup"><span data-stu-id="fcf04-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="fcf04-122">Bu, tüm atamalarınızı hello kiracısında listeler.</span><span class="sxs-lookup"><span data-stu-id="fcf04-122">This lists all your assignments in hello tenant.</span></span> <span data-ttu-id="fcf04-123">Merhaba kapsam olduğu Hello için bir Ara "/" ve hello Roledefinitionıd biter hello rol adı 1. adımda bulduğunuz GUID.</span><span class="sxs-lookup"><span data-stu-id="fcf04-123">Look for hello one where hello scope is "/" and hello RoleDefinitionId ends with hello role name GUID you found in step 1.</span></span> <span data-ttu-id="fcf04-124">Merhaba rol ataması aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="fcf04-124">hello role assignment should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleDefinitionId":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "principalId":"{objectID}",
    "scope":"/",
    "createdOn":"2016-08-17T19:21:16.3422480Z",
    "updatedOn":"2016-08-17T19:21:16.3422480Z",
    "createdBy":"93ce6722-3638-4222-b582-78b75c5c6d65",
    "updatedBy":"93ce6722-3638-4222-b582-78b75c5c6d65"},
    "id":"/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099",
    "type":"Microsoft.Authorization/roleAssignments",
    "name":"e7dd75bc-06f6-4e71-9014-ee96a929d099"}],
    "nextLink":null}
    ```

    <span data-ttu-id="fcf04-125">Merhaba GUID hello kaydetmeyi yeniden, *adı* parametresi, bu durumda **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="fcf04-125">Again, save hello GUID from hello *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="fcf04-126">Son olarak, arama [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) burada roleAssignmentId = 2. adımda bulduğunuz GUID'i hello adı.</span><span class="sxs-lookup"><span data-stu-id="fcf04-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = hello name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fcf04-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fcf04-127">Next steps</span></span>

- <span data-ttu-id="fcf04-128">Daha fazla bilgi edinmek [rol tabanlı erişim denetimini REST ile yönetme](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="fcf04-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="fcf04-129">[Erişim atamalarını yönetmeyi](role-based-access-control-manage-assignments.md) hello Azure portal'ın</span><span class="sxs-lookup"><span data-stu-id="fcf04-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in hello Azure portal</span></span>
