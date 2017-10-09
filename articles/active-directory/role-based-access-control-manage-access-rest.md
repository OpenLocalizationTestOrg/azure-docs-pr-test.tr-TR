---
title: "aaaRole tabanlı erişim denetimini REST - Azure AD ile | Microsoft Docs"
description: "Rol tabanlı erişim denetimini hello REST API ile yönetme"
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a><span data-ttu-id="665ca-103">Rol tabanlı erişim denetimi hello REST API ile yönetme</span><span class="sxs-lookup"><span data-stu-id="665ca-103">Manage Role-Based Access Control with hello REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="665ca-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="665ca-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="665ca-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="665ca-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="665ca-106">REST API</span><span class="sxs-lookup"><span data-stu-id="665ca-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="665ca-107">Rol tabanlı erişim denetimi (RBAC) hello Azure portal'ın ve Azure Kaynak Yöneticisi API'si erişim tooyour abonelik ve ayrıntılı bir düzeyde kaynakları yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="665ca-107">Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API helps you manage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="665ca-108">Bu özellik ile bazı roller toothem belirli bir kapsamda atayarak Active Directory Kullanıcıları, grupları veya hizmet asıl adı için erişim izni verebilir.</span><span class="sxs-lookup"><span data-stu-id="665ca-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="665ca-109">Tüm rol atamalarını listesi</span><span class="sxs-lookup"><span data-stu-id="665ca-109">List all role assignments</span></span>
<span data-ttu-id="665ca-110">Listeleri tüm hello rol atamalarını belirtilen hello adresindeki kapsam ve subscopes.</span><span class="sxs-lookup"><span data-stu-id="665ca-110">Lists all hello role assignments at hello specified scope and subscopes.</span></span>

<span data-ttu-id="665ca-111">toolist rol atamaları gerekir erişiminiz çok`Microsoft.Authorization/roleAssignments/read` hello kapsamda işlemi.</span><span class="sxs-lookup"><span data-stu-id="665ca-111">toolist role assignments, you must have access too`Microsoft.Authorization/roleAssignments/read` operation at hello scope.</span></span> <span data-ttu-id="665ca-112">Tüm hello yerleşik roller erişim toothis işlemi verilir.</span><span class="sxs-lookup"><span data-stu-id="665ca-112">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="665ca-113">Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="665ca-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="665ca-114">İstek</span><span class="sxs-lookup"><span data-stu-id="665ca-114">Request</span></span>
<span data-ttu-id="665ca-115">Kullanım hello **almak** URI aşağıdaki hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="665ca-115">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="665ca-116">Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:</span><span class="sxs-lookup"><span data-stu-id="665ca-116">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="665ca-117">Değiştir *{kapsamı}* kendisi için istediğiniz toolist hello rol atamalarını hello kapsama sahip.</span><span class="sxs-lookup"><span data-stu-id="665ca-117">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="665ca-118">Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:</span><span class="sxs-lookup"><span data-stu-id="665ca-118">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="665ca-119">Abonelik: /subscriptions/ {subscrıptıon-ID}</span><span class="sxs-lookup"><span data-stu-id="665ca-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="665ca-120">Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="665ca-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="665ca-121">Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="665ca-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="665ca-122">Değiştir *{api-version}* 2015-07-01 ile.</span><span class="sxs-lookup"><span data-stu-id="665ca-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="665ca-123">Değiştir *{filtre}* hello koşuluyla tooapply toofilter hello rol ataması listesi istiyor:</span><span class="sxs-lookup"><span data-stu-id="665ca-123">Replace *{filter}* with hello condition that you wish tooapply toofilter hello role assignment list:</span></span>

   * <span data-ttu-id="665ca-124">Yalnızca hello listesi rol atamalarını hello rol atamaları subscopes olarak dahil edilmez kapsamı, belirtilen:`atScope()`</span><span class="sxs-lookup"><span data-stu-id="665ca-124">List role assignments for only hello specified scope, not including hello role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="665ca-125">Belirli bir kullanıcı, Grup veya uygulama için rol atamalarını listesi:`principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="665ca-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="665ca-126">Liste olanları gruplarından devralınan dahil olmak üzere belirli bir kullanıcı için rol atamalarını |`assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="665ca-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="665ca-127">Yanıt</span><span class="sxs-lookup"><span data-stu-id="665ca-127">Response</span></span>
<span data-ttu-id="665ca-128">Durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="665ca-128">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="665ca-129">Bir rol ataması hakkında bilgi alın</span><span class="sxs-lookup"><span data-stu-id="665ca-129">Get information about a role assignment</span></span>
<span data-ttu-id="665ca-130">Merhaba rol ataması tanımlayıcısı tarafından belirtilen bir tek bir rol ataması hakkında bilgi alır.</span><span class="sxs-lookup"><span data-stu-id="665ca-130">Gets information about a single role assignment specified by hello role assignment identifier.</span></span>

<span data-ttu-id="665ca-131">bir rol ataması hakkında bilgi tooget, gereken erişiminiz çok`Microsoft.Authorization/roleAssignments/read` işlemi.</span><span class="sxs-lookup"><span data-stu-id="665ca-131">tooget information about a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="665ca-132">Tüm hello yerleşik roller erişim toothis işlemi verilir.</span><span class="sxs-lookup"><span data-stu-id="665ca-132">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="665ca-133">Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="665ca-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="665ca-134">İstek</span><span class="sxs-lookup"><span data-stu-id="665ca-134">Request</span></span>
<span data-ttu-id="665ca-135">Kullanım hello **almak** URI aşağıdaki hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="665ca-135">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="665ca-136">Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:</span><span class="sxs-lookup"><span data-stu-id="665ca-136">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="665ca-137">Değiştir *{kapsamı}* kendisi için istediğiniz toolist hello rol atamalarını hello kapsama sahip.</span><span class="sxs-lookup"><span data-stu-id="665ca-137">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="665ca-138">Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:</span><span class="sxs-lookup"><span data-stu-id="665ca-138">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="665ca-139">Abonelik: /subscriptions/ {subscrıptıon-ID}</span><span class="sxs-lookup"><span data-stu-id="665ca-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="665ca-140">Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="665ca-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="665ca-141">Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="665ca-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="665ca-142">Değiştir *{rol atama kimliği}* , hello rol atamasının hello GUID tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="665ca-142">Replace *{role-assignment-id}* with hello GUID identifier of hello role assignment.</span></span>
3. <span data-ttu-id="665ca-143">Değiştir *{api-version}* 2015-07-01 ile.</span><span class="sxs-lookup"><span data-stu-id="665ca-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="665ca-144">Yanıt</span><span class="sxs-lookup"><span data-stu-id="665ca-144">Response</span></span>
<span data-ttu-id="665ca-145">Durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="665ca-145">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a><span data-ttu-id="665ca-146">Bir rol ataması oluşturma</span><span class="sxs-lookup"><span data-stu-id="665ca-146">Create a Role Assignment</span></span>
<span data-ttu-id="665ca-147">Bir rol oluşturmak hello atamasının Belirtilen kapsam hello asıl izni veriliyor hello belirtilen rol belirtilen için.</span><span class="sxs-lookup"><span data-stu-id="665ca-147">Create a role assignment at hello specified scope for hello specified principal granting hello specified role.</span></span>

<span data-ttu-id="665ca-148">bir rol ataması toocreate gerekir erişiminiz çok`Microsoft.Authorization/roleAssignments/write` işlemi.</span><span class="sxs-lookup"><span data-stu-id="665ca-148">toocreate a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="665ca-149">Merhaba yerleşik roller, yalnızca *sahibi* ve *kullanıcı erişimi Yöneticisi* erişim toothis işlemi verilir.</span><span class="sxs-lookup"><span data-stu-id="665ca-149">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="665ca-150">Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="665ca-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="665ca-151">İstek</span><span class="sxs-lookup"><span data-stu-id="665ca-151">Request</span></span>
<span data-ttu-id="665ca-152">Kullanım hello **PUT** URI aşağıdaki hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="665ca-152">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="665ca-153">Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:</span><span class="sxs-lookup"><span data-stu-id="665ca-153">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="665ca-154">Değiştir *{kapsamı}* aktarılma istediğiniz toocreate hello rol atamalarını hello kapsama sahip.</span><span class="sxs-lookup"><span data-stu-id="665ca-154">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="665ca-155">Bir üst kapsamda bir rol ataması oluşturduğunuzda, tüm alt kapsamlar hello devralır aynı rol ataması.</span><span class="sxs-lookup"><span data-stu-id="665ca-155">When you create a role assignment at a parent scope, all child scopes inherit hello same role assignment.</span></span> <span data-ttu-id="665ca-156">Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:</span><span class="sxs-lookup"><span data-stu-id="665ca-156">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="665ca-157">Abonelik: /subscriptions/ {subscrıptıon-ID}</span><span class="sxs-lookup"><span data-stu-id="665ca-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="665ca-158">Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="665ca-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="665ca-159">Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="665ca-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="665ca-160">Değiştir *{rol atama kimliği}* yeni bir GUID ile haline geldikten hello yeni rol ataması hello GUID tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="665ca-160">Replace *{role-assignment-id}* with a new GUID, which becomes hello GUID identifier of hello new role assignment.</span></span>
3. <span data-ttu-id="665ca-161">Değiştir *{api-version}* 2015-07-01 ile.</span><span class="sxs-lookup"><span data-stu-id="665ca-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="665ca-162">Merhaba istek gövdesi için biçim aşağıdaki hello hello değerleri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="665ca-162">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="665ca-163">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="665ca-163">Element Name</span></span> | <span data-ttu-id="665ca-164">Gerekli</span><span class="sxs-lookup"><span data-stu-id="665ca-164">Required</span></span> | <span data-ttu-id="665ca-165">Tür</span><span class="sxs-lookup"><span data-stu-id="665ca-165">Type</span></span> | <span data-ttu-id="665ca-166">Açıklama</span><span class="sxs-lookup"><span data-stu-id="665ca-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="665ca-167">Roledefinitionıd</span><span class="sxs-lookup"><span data-stu-id="665ca-167">roleDefinitionId</span></span> |<span data-ttu-id="665ca-168">Evet</span><span class="sxs-lookup"><span data-stu-id="665ca-168">Yes</span></span> |<span data-ttu-id="665ca-169">Dize</span><span class="sxs-lookup"><span data-stu-id="665ca-169">String</span></span> |<span data-ttu-id="665ca-170">Merhaba rol Hello tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="665ca-170">hello identifier of hello role.</span></span> <span data-ttu-id="665ca-171">Merhaba tanımlayıcısının Hello biçimdedir:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="665ca-171">hello format of hello identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="665ca-172">Principalıd</span><span class="sxs-lookup"><span data-stu-id="665ca-172">principalId</span></span> |<span data-ttu-id="665ca-173">Evet</span><span class="sxs-lookup"><span data-stu-id="665ca-173">Yes</span></span> |<span data-ttu-id="665ca-174">Dize</span><span class="sxs-lookup"><span data-stu-id="665ca-174">String</span></span> |<span data-ttu-id="665ca-175">hello Azure AD sorumlusu (kullanıcı, Grup veya hizmet sorumlusu) objectID toowhich hello rolü atanır.</span><span class="sxs-lookup"><span data-stu-id="665ca-175">objectId of hello Azure AD principal (user, group, or service principal) toowhich hello role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="665ca-176">Yanıt</span><span class="sxs-lookup"><span data-stu-id="665ca-176">Response</span></span>
<span data-ttu-id="665ca-177">Durum kodu: 201</span><span class="sxs-lookup"><span data-stu-id="665ca-177">Status code: 201</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a><span data-ttu-id="665ca-178">Bir rol atamasını silin</span><span class="sxs-lookup"><span data-stu-id="665ca-178">Delete a Role Assignment</span></span>
<span data-ttu-id="665ca-179">Delete hello rol atamasının kapsamı belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="665ca-179">Delete a role assignment at hello specified scope.</span></span>

<span data-ttu-id="665ca-180">bir rol ataması toodelete, erişim toohello olmalıdır `Microsoft.Authorization/roleAssignments/delete` işlemi.</span><span class="sxs-lookup"><span data-stu-id="665ca-180">toodelete a role assignment, you must have access toohello `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="665ca-181">Merhaba yerleşik roller, yalnızca *sahibi* ve *kullanıcı erişimi Yöneticisi* erişim toothis işlemi verilir.</span><span class="sxs-lookup"><span data-stu-id="665ca-181">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="665ca-182">Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="665ca-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="665ca-183">İstek</span><span class="sxs-lookup"><span data-stu-id="665ca-183">Request</span></span>
<span data-ttu-id="665ca-184">Kullanım hello **silmek** URI aşağıdaki hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="665ca-184">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="665ca-185">Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:</span><span class="sxs-lookup"><span data-stu-id="665ca-185">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="665ca-186">Değiştir *{kapsamı}* aktarılma istediğiniz toocreate hello rol atamalarını hello kapsama sahip.</span><span class="sxs-lookup"><span data-stu-id="665ca-186">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="665ca-187">Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:</span><span class="sxs-lookup"><span data-stu-id="665ca-187">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="665ca-188">Abonelik: /subscriptions/ {subscrıptıon-ID}</span><span class="sxs-lookup"><span data-stu-id="665ca-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="665ca-189">Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="665ca-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="665ca-190">Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="665ca-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="665ca-191">Değiştir *{rol atama kimliği}* hello rol ataması kimliği GUID.</span><span class="sxs-lookup"><span data-stu-id="665ca-191">Replace *{role-assignment-id}* with hello role assignment id GUID.</span></span>
3. <span data-ttu-id="665ca-192">Değiştir *{api-version}* 2015-07-01 ile.</span><span class="sxs-lookup"><span data-stu-id="665ca-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="665ca-193">Yanıt</span><span class="sxs-lookup"><span data-stu-id="665ca-193">Response</span></span>
<span data-ttu-id="665ca-194">Durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="665ca-194">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a><span data-ttu-id="665ca-195">Tüm rolleri listeler</span><span class="sxs-lookup"><span data-stu-id="665ca-195">List all Roles</span></span>
<span data-ttu-id="665ca-196">Belirtilen hello atamasının kullanılabilir tüm hello rollerini listeler kapsamı.</span><span class="sxs-lookup"><span data-stu-id="665ca-196">Lists all hello roles that are available for assignment at hello specified scope.</span></span>

<span data-ttu-id="665ca-197">toolist rolleri gerekir erişiminiz çok`Microsoft.Authorization/roleDefinitions/read` hello kapsamda işlemi.</span><span class="sxs-lookup"><span data-stu-id="665ca-197">toolist roles, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation at hello scope.</span></span> <span data-ttu-id="665ca-198">Tüm hello yerleşik roller erişim toothis işlemi verilir.</span><span class="sxs-lookup"><span data-stu-id="665ca-198">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="665ca-199">Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="665ca-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="665ca-200">İstek</span><span class="sxs-lookup"><span data-stu-id="665ca-200">Request</span></span>
<span data-ttu-id="665ca-201">Kullanım hello **almak** URI aşağıdaki hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="665ca-201">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="665ca-202">Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:</span><span class="sxs-lookup"><span data-stu-id="665ca-202">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="665ca-203">Değiştir *{kapsamı}* kendisi için istediğiniz toolist hello rolleri hello kapsama sahip.</span><span class="sxs-lookup"><span data-stu-id="665ca-203">Replace *{scope}* with hello scope for which you wish toolist hello roles.</span></span> <span data-ttu-id="665ca-204">Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:</span><span class="sxs-lookup"><span data-stu-id="665ca-204">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="665ca-205">Abonelik: /subscriptions/ {subscrıptıon-ID}</span><span class="sxs-lookup"><span data-stu-id="665ca-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="665ca-206">Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="665ca-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="665ca-207">Kaynak /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="665ca-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="665ca-208">Değiştir *{api-version}* 2015-07-01 ile.</span><span class="sxs-lookup"><span data-stu-id="665ca-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="665ca-209">Değiştir *{filtre}* hello koşuluyla tooapply toofilter hello rollerin listesini istiyor:</span><span class="sxs-lookup"><span data-stu-id="665ca-209">Replace *{filter}* with hello condition that you wish tooapply toofilter hello list of roles:</span></span>

   * <span data-ttu-id="665ca-210">Liste rolleri hello atamasının kullanılabilir kapsamı ve tüm alt kapsamlarından belirtilen:`atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="665ca-210">List roles available for assignment at hello specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="665ca-211">Tam ekran adını kullanarak bir rolü arayın: `roleName%20eq%20'{role-display-name}'`.</span><span class="sxs-lookup"><span data-stu-id="665ca-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="665ca-212">Merhaba URL kodlanmış form hello rolünün hello tam görünen adını kullanın.</span><span class="sxs-lookup"><span data-stu-id="665ca-212">Use hello URL encoded form of hello exact display name of hello role.</span></span> <span data-ttu-id="665ca-213">Örneğin,`$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="665ca-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="665ca-214">Yanıt</span><span class="sxs-lookup"><span data-stu-id="665ca-214">Response</span></span>
<span data-ttu-id="665ca-215">Durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="665ca-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a><span data-ttu-id="665ca-216">Bir rolü hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="665ca-216">Get information about a Role</span></span>
<span data-ttu-id="665ca-217">Merhaba rol tanımı tanımlayıcısı tarafından belirtilen tek bir rol bilgilerini alır.</span><span class="sxs-lookup"><span data-stu-id="665ca-217">Gets information about a single role specified by hello role definition identifier.</span></span> <span data-ttu-id="665ca-218">görünen adını kullanarak tek bir rol tooget bilgilere bakın [tüm rolleri listesinde](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="665ca-218">tooget information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="665ca-219">bir rolü hakkında tooget bilgi gerekir erişiminiz çok`Microsoft.Authorization/roleDefinitions/read` işlemi.</span><span class="sxs-lookup"><span data-stu-id="665ca-219">tooget information about a role, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="665ca-220">Tüm hello yerleşik roller erişim toothis işlemi verilir.</span><span class="sxs-lookup"><span data-stu-id="665ca-220">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="665ca-221">Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="665ca-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="665ca-222">İstek</span><span class="sxs-lookup"><span data-stu-id="665ca-222">Request</span></span>
<span data-ttu-id="665ca-223">Kullanım hello **almak** URI aşağıdaki hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="665ca-223">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="665ca-224">Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:</span><span class="sxs-lookup"><span data-stu-id="665ca-224">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="665ca-225">Değiştir *{kapsamı}* kendisi için istediğiniz toolist hello rol atamalarını hello kapsama sahip.</span><span class="sxs-lookup"><span data-stu-id="665ca-225">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="665ca-226">Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:</span><span class="sxs-lookup"><span data-stu-id="665ca-226">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="665ca-227">Abonelik: /subscriptions/ {subscrıptıon-ID}</span><span class="sxs-lookup"><span data-stu-id="665ca-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="665ca-228">Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="665ca-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="665ca-229">Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="665ca-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="665ca-230">Değiştir *{rol tanımı kimliği}* , hello rol tanımı hello GUID tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="665ca-230">Replace *{role-definition-id}* with hello GUID identifier of hello role definition.</span></span>
3. <span data-ttu-id="665ca-231">Değiştir *{api-version}* 2015-07-01 ile.</span><span class="sxs-lookup"><span data-stu-id="665ca-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="665ca-232">Yanıt</span><span class="sxs-lookup"><span data-stu-id="665ca-232">Response</span></span>
<span data-ttu-id="665ca-233">Durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="665ca-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a><span data-ttu-id="665ca-234">Özel bir rol oluşturun</span><span class="sxs-lookup"><span data-stu-id="665ca-234">Create a Custom Role</span></span>
<span data-ttu-id="665ca-235">Özel bir rol oluşturun.</span><span class="sxs-lookup"><span data-stu-id="665ca-235">Create a custom role.</span></span>

<span data-ttu-id="665ca-236">toocreate özel bir rol, gereken erişiminiz çok`Microsoft.Authorization/roleDefinitions/write` tüm hello işlemi `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="665ca-236">toocreate a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="665ca-237">Merhaba yerleşik roller, yalnızca *sahibi* ve *kullanıcı erişimi Yöneticisi* erişim toothis işlemi verilir.</span><span class="sxs-lookup"><span data-stu-id="665ca-237">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="665ca-238">Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="665ca-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="665ca-239">İstek</span><span class="sxs-lookup"><span data-stu-id="665ca-239">Request</span></span>
<span data-ttu-id="665ca-240">Kullanım hello **PUT** URI aşağıdaki hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="665ca-240">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="665ca-241">Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:</span><span class="sxs-lookup"><span data-stu-id="665ca-241">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="665ca-242">Değiştir *{kapsamı}* hello ile ilk *AssignableScope* hello özel rolü.</span><span class="sxs-lookup"><span data-stu-id="665ca-242">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="665ca-243">Örnek hello nasıl toospecify hello kapsam farklı düzeylerde gösterir.</span><span class="sxs-lookup"><span data-stu-id="665ca-243">hello following examples show how toospecify hello scope for different levels.</span></span>

   * <span data-ttu-id="665ca-244">Abonelik: /subscriptions/ {subscrıptıon-ID}</span><span class="sxs-lookup"><span data-stu-id="665ca-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="665ca-245">Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="665ca-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="665ca-246">Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="665ca-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="665ca-247">Değiştir *{rol tanımı kimliği}* yeni bir GUID ile haline geldikten hello yeni özel rol hello GUID tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="665ca-247">Replace *{role-definition-id}* with a new GUID, which becomes hello GUID identifier of hello new custom role.</span></span>
3. <span data-ttu-id="665ca-248">Değiştir *{api-version}* 2015-07-01 ile.</span><span class="sxs-lookup"><span data-stu-id="665ca-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="665ca-249">Merhaba istek gövdesi için biçim aşağıdaki hello hello değerleri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="665ca-249">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="665ca-250">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="665ca-250">Element Name</span></span> | <span data-ttu-id="665ca-251">Gerekli</span><span class="sxs-lookup"><span data-stu-id="665ca-251">Required</span></span> | <span data-ttu-id="665ca-252">Tür</span><span class="sxs-lookup"><span data-stu-id="665ca-252">Type</span></span> | <span data-ttu-id="665ca-253">Açıklama</span><span class="sxs-lookup"><span data-stu-id="665ca-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="665ca-254">ad</span><span class="sxs-lookup"><span data-stu-id="665ca-254">name</span></span> |<span data-ttu-id="665ca-255">Evet</span><span class="sxs-lookup"><span data-stu-id="665ca-255">Yes</span></span> |<span data-ttu-id="665ca-256">Dize</span><span class="sxs-lookup"><span data-stu-id="665ca-256">String</span></span> |<span data-ttu-id="665ca-257">Merhaba özel rol GUID tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="665ca-257">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="665ca-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="665ca-258">properties.roleName</span></span> |<span data-ttu-id="665ca-259">Evet</span><span class="sxs-lookup"><span data-stu-id="665ca-259">Yes</span></span> |<span data-ttu-id="665ca-260">Dize</span><span class="sxs-lookup"><span data-stu-id="665ca-260">String</span></span> |<span data-ttu-id="665ca-261">Merhaba özel rol adını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="665ca-261">Display name of hello custom role.</span></span> <span data-ttu-id="665ca-262">En büyük boyutu 128 karakter.</span><span class="sxs-lookup"><span data-stu-id="665ca-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="665ca-263">Properties.Description</span><span class="sxs-lookup"><span data-stu-id="665ca-263">properties.description</span></span> |<span data-ttu-id="665ca-264">Hayır</span><span class="sxs-lookup"><span data-stu-id="665ca-264">No</span></span> |<span data-ttu-id="665ca-265">Dize</span><span class="sxs-lookup"><span data-stu-id="665ca-265">String</span></span> |<span data-ttu-id="665ca-266">Merhaba özel rol tanımı.</span><span class="sxs-lookup"><span data-stu-id="665ca-266">Description of hello custom role.</span></span> <span data-ttu-id="665ca-267">En büyük boyutu 1024 karakter.</span><span class="sxs-lookup"><span data-stu-id="665ca-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="665ca-268">Properties.Type</span><span class="sxs-lookup"><span data-stu-id="665ca-268">properties.type</span></span> |<span data-ttu-id="665ca-269">Evet</span><span class="sxs-lookup"><span data-stu-id="665ca-269">Yes</span></span> |<span data-ttu-id="665ca-270">Dize</span><span class="sxs-lookup"><span data-stu-id="665ca-270">String</span></span> |<span data-ttu-id="665ca-271">Çok Ayarla "CustomRole."</span><span class="sxs-lookup"><span data-stu-id="665ca-271">Set too"CustomRole."</span></span> |
| <span data-ttu-id="665ca-272">Properties.Permissions.Actions</span><span class="sxs-lookup"><span data-stu-id="665ca-272">properties.permissions.actions</span></span> |<span data-ttu-id="665ca-273">Evet</span><span class="sxs-lookup"><span data-stu-id="665ca-273">Yes</span></span> |<span data-ttu-id="665ca-274">String]</span><span class="sxs-lookup"><span data-stu-id="665ca-274">String[]</span></span> |<span data-ttu-id="665ca-275">Bir dizi eylem hello özel rol tarafından verilen belirten hello işlemleri dizeleri.</span><span class="sxs-lookup"><span data-stu-id="665ca-275">An array of action strings specifying hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="665ca-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="665ca-276">properties.permissions.notActions</span></span> |<span data-ttu-id="665ca-277">Hayır</span><span class="sxs-lookup"><span data-stu-id="665ca-277">No</span></span> |<span data-ttu-id="665ca-278">String]</span><span class="sxs-lookup"><span data-stu-id="665ca-278">String[]</span></span> |<span data-ttu-id="665ca-279">Hello işlemleri tooexclude hello özel rol tarafından verilen hello Operations belirten bir eylem dizeler dizisi.</span><span class="sxs-lookup"><span data-stu-id="665ca-279">An array of action strings specifying hello operations tooexclude from hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="665ca-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="665ca-280">properties.assignableScopes</span></span> |<span data-ttu-id="665ca-281">Evet</span><span class="sxs-lookup"><span data-stu-id="665ca-281">Yes</span></span> |<span data-ttu-id="665ca-282">String]</span><span class="sxs-lookup"><span data-stu-id="665ca-282">String[]</span></span> |<span data-ttu-id="665ca-283">Hangi hello özel rol kullanılabilir kapsamları dizisi.</span><span class="sxs-lookup"><span data-stu-id="665ca-283">An array of scopes in which hello custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="665ca-284">Yanıt</span><span class="sxs-lookup"><span data-stu-id="665ca-284">Response</span></span>
<span data-ttu-id="665ca-285">Durum kodu: 201</span><span class="sxs-lookup"><span data-stu-id="665ca-285">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a><span data-ttu-id="665ca-286">Özel bir rol güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="665ca-286">Update a Custom Role</span></span>
<span data-ttu-id="665ca-287">Özel bir rol değiştirin.</span><span class="sxs-lookup"><span data-stu-id="665ca-287">Modify a custom role.</span></span>

<span data-ttu-id="665ca-288">toomodify özel bir rol, gereken erişiminiz çok`Microsoft.Authorization/roleDefinitions/write` tüm hello işlemi `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="665ca-288">toomodify a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="665ca-289">Merhaba yerleşik roller, yalnızca *sahibi* ve *kullanıcı erişimi Yöneticisi* erişim toothis işlemi verilir.</span><span class="sxs-lookup"><span data-stu-id="665ca-289">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="665ca-290">Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="665ca-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="665ca-291">İstek</span><span class="sxs-lookup"><span data-stu-id="665ca-291">Request</span></span>
<span data-ttu-id="665ca-292">Kullanım hello **PUT** URI aşağıdaki hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="665ca-292">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="665ca-293">Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:</span><span class="sxs-lookup"><span data-stu-id="665ca-293">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="665ca-294">Değiştir *{kapsamı}* hello ile ilk *AssignableScope* hello özel rolü.</span><span class="sxs-lookup"><span data-stu-id="665ca-294">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="665ca-295">Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:</span><span class="sxs-lookup"><span data-stu-id="665ca-295">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="665ca-296">Abonelik: /subscriptions/ {subscrıptıon-ID}</span><span class="sxs-lookup"><span data-stu-id="665ca-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="665ca-297">Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="665ca-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="665ca-298">Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="665ca-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="665ca-299">Değiştir *{rol tanımı kimliği}* ile Merhaba özel rol hello GUID tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="665ca-299">Replace *{role-definition-id}* with hello GUID identifier of hello custom role.</span></span>
3. <span data-ttu-id="665ca-300">Değiştir *{api-version}* 2015-07-01 ile.</span><span class="sxs-lookup"><span data-stu-id="665ca-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="665ca-301">Merhaba istek gövdesi için biçim aşağıdaki hello hello değerleri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="665ca-301">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="665ca-302">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="665ca-302">Element Name</span></span> | <span data-ttu-id="665ca-303">Gerekli</span><span class="sxs-lookup"><span data-stu-id="665ca-303">Required</span></span> | <span data-ttu-id="665ca-304">Tür</span><span class="sxs-lookup"><span data-stu-id="665ca-304">Type</span></span> | <span data-ttu-id="665ca-305">Açıklama</span><span class="sxs-lookup"><span data-stu-id="665ca-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="665ca-306">ad</span><span class="sxs-lookup"><span data-stu-id="665ca-306">name</span></span> |<span data-ttu-id="665ca-307">Evet</span><span class="sxs-lookup"><span data-stu-id="665ca-307">Yes</span></span> |<span data-ttu-id="665ca-308">Dize</span><span class="sxs-lookup"><span data-stu-id="665ca-308">String</span></span> |<span data-ttu-id="665ca-309">Merhaba özel rol GUID tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="665ca-309">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="665ca-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="665ca-310">properties.roleName</span></span> |<span data-ttu-id="665ca-311">Evet</span><span class="sxs-lookup"><span data-stu-id="665ca-311">Yes</span></span> |<span data-ttu-id="665ca-312">Dize</span><span class="sxs-lookup"><span data-stu-id="665ca-312">String</span></span> |<span data-ttu-id="665ca-313">Merhaba güncelleştirilmiş özel rol adını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="665ca-313">Display name of hello updated custom role.</span></span> |
| <span data-ttu-id="665ca-314">Properties.Description</span><span class="sxs-lookup"><span data-stu-id="665ca-314">properties.description</span></span> |<span data-ttu-id="665ca-315">Hayır</span><span class="sxs-lookup"><span data-stu-id="665ca-315">No</span></span> |<span data-ttu-id="665ca-316">Dize</span><span class="sxs-lookup"><span data-stu-id="665ca-316">String</span></span> |<span data-ttu-id="665ca-317">Merhaba açıklaması özel rol güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="665ca-317">Description of hello updated custom role.</span></span> |
| <span data-ttu-id="665ca-318">Properties.Type</span><span class="sxs-lookup"><span data-stu-id="665ca-318">properties.type</span></span> |<span data-ttu-id="665ca-319">Evet</span><span class="sxs-lookup"><span data-stu-id="665ca-319">Yes</span></span> |<span data-ttu-id="665ca-320">Dize</span><span class="sxs-lookup"><span data-stu-id="665ca-320">String</span></span> |<span data-ttu-id="665ca-321">Çok Ayarla "CustomRole."</span><span class="sxs-lookup"><span data-stu-id="665ca-321">Set too"CustomRole."</span></span> |
| <span data-ttu-id="665ca-322">Properties.Permissions.Actions</span><span class="sxs-lookup"><span data-stu-id="665ca-322">properties.permissions.actions</span></span> |<span data-ttu-id="665ca-323">Evet</span><span class="sxs-lookup"><span data-stu-id="665ca-323">Yes</span></span> |<span data-ttu-id="665ca-324">String]</span><span class="sxs-lookup"><span data-stu-id="665ca-324">String[]</span></span> |<span data-ttu-id="665ca-325">Merhaba işlemleri toowhich hello belirtme eylem dizisini özel rol verir erişim güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="665ca-325">An array of action strings specifying hello operations toowhich hello updated custom role grants access.</span></span> |
| <span data-ttu-id="665ca-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="665ca-326">properties.permissions.notActions</span></span> |<span data-ttu-id="665ca-327">Hayır</span><span class="sxs-lookup"><span data-stu-id="665ca-327">No</span></span> |<span data-ttu-id="665ca-328">String]</span><span class="sxs-lookup"><span data-stu-id="665ca-328">String[]</span></span> |<span data-ttu-id="665ca-329">Bir dizi eylem hangi hello özel rol verir güncelleştirilmiş hello Operations belirten hello işlemleri tooexclude dizeleri.</span><span class="sxs-lookup"><span data-stu-id="665ca-329">An array of action strings specifying hello operations tooexclude from hello operations which hello updated custom role grants.</span></span> |
| <span data-ttu-id="665ca-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="665ca-330">properties.assignableScopes</span></span> |<span data-ttu-id="665ca-331">Evet</span><span class="sxs-lookup"><span data-stu-id="665ca-331">Yes</span></span> |<span data-ttu-id="665ca-332">String]</span><span class="sxs-lookup"><span data-stu-id="665ca-332">String[]</span></span> |<span data-ttu-id="665ca-333">Hangi hello güncelleştirilmiş özel rol kullanılabilir kapsamları dizisi.</span><span class="sxs-lookup"><span data-stu-id="665ca-333">An array of scopes in which hello updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="665ca-334">Yanıt</span><span class="sxs-lookup"><span data-stu-id="665ca-334">Response</span></span>
<span data-ttu-id="665ca-335">Durum kodu: 201</span><span class="sxs-lookup"><span data-stu-id="665ca-335">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a><span data-ttu-id="665ca-336">Bir özel rolü silmeyi</span><span class="sxs-lookup"><span data-stu-id="665ca-336">Delete a Custom Role</span></span>
<span data-ttu-id="665ca-337">Özel bir rol silin.</span><span class="sxs-lookup"><span data-stu-id="665ca-337">Delete a custom role.</span></span>

<span data-ttu-id="665ca-338">toodelete özel bir rol, gereken erişiminiz çok`Microsoft.Authorization/roleDefinitions/delete` tüm hello işlemi `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="665ca-338">toodelete a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/delete` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="665ca-339">Merhaba yerleşik roller, yalnızca *sahibi* ve *kullanıcı erişimi Yöneticisi* erişim toothis işlemi verilir.</span><span class="sxs-lookup"><span data-stu-id="665ca-339">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="665ca-340">Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="665ca-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="665ca-341">İstek</span><span class="sxs-lookup"><span data-stu-id="665ca-341">Request</span></span>
<span data-ttu-id="665ca-342">Kullanım hello **silmek** URI aşağıdaki hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="665ca-342">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="665ca-343">Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:</span><span class="sxs-lookup"><span data-stu-id="665ca-343">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="665ca-344">Değiştir *{kapsamı}* toodelete hello rol tanımı istediğiniz hello kapsama sahip.</span><span class="sxs-lookup"><span data-stu-id="665ca-344">Replace *{scope}* with hello scope at which you wish toodelete hello role definition.</span></span> <span data-ttu-id="665ca-345">Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:</span><span class="sxs-lookup"><span data-stu-id="665ca-345">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="665ca-346">Abonelik: /subscriptions/ {subscrıptıon-ID}</span><span class="sxs-lookup"><span data-stu-id="665ca-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="665ca-347">Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="665ca-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="665ca-348">Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="665ca-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="665ca-349">Değiştir *{rol tanımı kimliği}* hello GUID rol tanımı kimliği hello özel rol.</span><span class="sxs-lookup"><span data-stu-id="665ca-349">Replace *{role-definition-id}* with hello GUID role definition id of hello custom role.</span></span>
3. <span data-ttu-id="665ca-350">Değiştir *{api-version}* 2015-07-01 ile.</span><span class="sxs-lookup"><span data-stu-id="665ca-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="665ca-351">Yanıt</span><span class="sxs-lookup"><span data-stu-id="665ca-351">Response</span></span>
<span data-ttu-id="665ca-352">Durum kodu: 200</span><span class="sxs-lookup"><span data-stu-id="665ca-352">Status code: 200</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a><span data-ttu-id="665ca-353">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="665ca-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
