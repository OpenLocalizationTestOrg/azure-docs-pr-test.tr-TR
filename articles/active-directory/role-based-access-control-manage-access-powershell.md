---
title: "Rol tabanlı erişim denetimi (RBAC) Azure PowerShell ile aaaManage | Microsoft Docs"
description: "Nasıl toomanage rollerini listeleme, rol atama ve rol atamalarını silme de dahil olmak üzere Azure PowerShell ile RBAC."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 9e225dba-9044-4b13-b573-2f30d77925a9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: fa44991113e75b345177867b0bede38de4373e04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="c566b-103">Rol Tabanlı Access Control’ü Azure PowerShell İle Yönetme</span><span class="sxs-lookup"><span data-stu-id="c566b-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c566b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c566b-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="c566b-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c566b-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="c566b-106">REST API</span><span class="sxs-lookup"><span data-stu-id="c566b-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="c566b-107">Rol tabanlı erişim denetimi (RBAC) hello Azure portalı ve Azure kaynak yönetimi API toomanage erişim tooyour abonelik ayrıntılı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c566b-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Management API toomanage access tooyour subscription at a fine-grained level.</span></span> <span data-ttu-id="c566b-108">Bu özellik ile bazı roller toothem belirli bir kapsamda atayarak Active Directory Kullanıcıları, grupları veya hizmet asıl adı için erişim izni verebilir.</span><span class="sxs-lookup"><span data-stu-id="c566b-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="c566b-109">PowerShell toomanage RBAC kullanabilmeniz için önce aşağıdaki önkoşullar hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c566b-109">Before you can use PowerShell toomanage RBAC, you need hello following prerequisites:</span></span>

* <span data-ttu-id="c566b-110">Azure PowerShell sürüm 0.8.8 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="c566b-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="c566b-111">tooinstall hello en son sürümünü ve ilişkilendirme Azure aboneliğinizle görmek [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c566b-111">tooinstall hello latest version and associate it with your Azure subscription, see [how tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="c566b-112">Azure Resource Manager cmdlet'lerini.</span><span class="sxs-lookup"><span data-stu-id="c566b-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="c566b-113">Merhaba yüklemek [Azure Resource Manager cmdlet'lerini](/powershell/azure/overview) PowerShell'de.</span><span class="sxs-lookup"><span data-stu-id="c566b-113">Install hello [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="c566b-114">Liste rolleri</span><span class="sxs-lookup"><span data-stu-id="c566b-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="c566b-115">Kullanılabilir tüm roller listesinde</span><span class="sxs-lookup"><span data-stu-id="c566b-115">List all available roles</span></span>
<span data-ttu-id="c566b-116">atama ve tooinspect hello işlemleri toowhich bunlar erişim vermek için kullanılabilir olan toolist RBAC rolü kullanmak `Get-AzureRmRoleDefinition`.</span><span class="sxs-lookup"><span data-stu-id="c566b-116">toolist RBAC roles that are available for assignment and tooinspect hello operations toowhich they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell-Get AzureRmRoleDefinition - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="c566b-118">Bir rolün liste eylemleri</span><span class="sxs-lookup"><span data-stu-id="c566b-118">List actions of a role</span></span>
<span data-ttu-id="c566b-119">belirli bir rol için toolist hello eylemlerini kullanmak `Get-AzureRmRoleDefinition <role name>`.</span><span class="sxs-lookup"><span data-stu-id="c566b-119">toolist hello actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell-Get AzureRmRoleDefinition belirli bir rol için - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="c566b-121">Kimlerin erişebileceğini bakın</span><span class="sxs-lookup"><span data-stu-id="c566b-121">See who has access</span></span>
<span data-ttu-id="c566b-122">toolist RBAC erişim atamalarını kullanın `Get-AzureRmRoleAssignment`.</span><span class="sxs-lookup"><span data-stu-id="c566b-122">toolist RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="c566b-123">Belirli bir kapsamda listesi rol atamaları</span><span class="sxs-lookup"><span data-stu-id="c566b-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="c566b-124">Belirtilen abonelik, kaynak grubu ya da kaynak için tüm hello erişim atamalarını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c566b-124">You can see all hello access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="c566b-125">Örneğin, bir kaynak grubu kullanmak için tüm hello etkin atamaları hello toosee `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span><span class="sxs-lookup"><span data-stu-id="c566b-125">For example, toosee hello all hello active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment bir kaynak grubu için - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a><span data-ttu-id="c566b-127">Liste rolleri tooa kullanıcı atanmış.</span><span class="sxs-lookup"><span data-stu-id="c566b-127">List roles assigned tooa user</span></span>
<span data-ttu-id="c566b-128">tooa atanmış olan tüm hello rollerini belirtilen kullanıcı ve toowhich hello kullanıcının ait olduğu, toohello gruplarına atanır hello rolleri toolist kullanım `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span><span class="sxs-lookup"><span data-stu-id="c566b-128">toolist all hello roles that are assigned tooa specified user and hello roles that are assigned toohello groups toowhich hello user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment bir kullanıcı için - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="c566b-130">Klasik Hizmet Yöneticisi ve ortak yönetici rol atamalarını listesi</span><span class="sxs-lookup"><span data-stu-id="c566b-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="c566b-131">Merhaba Klasik Abonelik Yöneticisi ve coadministrators, toolist erişim atamalarını kullanın:</span><span class="sxs-lookup"><span data-stu-id="c566b-131">toolist access assignments for hello classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="c566b-132">Erişim verme</span><span class="sxs-lookup"><span data-stu-id="c566b-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="c566b-133">Nesne kimlikleri için arama</span><span class="sxs-lookup"><span data-stu-id="c566b-133">Search for object IDs</span></span>
<span data-ttu-id="c566b-134">tooassign bir rol, gereksinim duyduğunuz tooidentify hello nesne (kullanıcı, Grup veya uygulama) ve hello kapsamı.</span><span class="sxs-lookup"><span data-stu-id="c566b-134">tooassign a role, you need tooidentify both hello object (user, group, or application) and hello scope.</span></span>

<span data-ttu-id="c566b-135">Merhaba abonelik kimliği bilmiyorsanız, hello bulabilirsiniz **abonelikleri** hello Azure portal dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="c566b-135">If you don't know hello subscription ID, you can find it in hello **Subscriptions** blade on hello Azure portal.</span></span> <span data-ttu-id="c566b-136">hello abonelik kimliği için tooquery nasıl görürüm toolearn [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="c566b-136">toolearn how tooquery for hello subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="c566b-137">bir Azure AD grubunun tooget hello nesne Kimliğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="c566b-137">tooget hello object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="c566b-138">Azure AD hizmet sorumlusu veya uygulama, kullanım için tooget hello nesne kimliği:</span><span class="sxs-lookup"><span data-stu-id="c566b-138">tooget hello object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="c566b-139">Merhaba abonelik kapsamında bir rol tooan uygulama atama</span><span class="sxs-lookup"><span data-stu-id="c566b-139">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="c566b-140">toogrant erişim tooan uygulama hello abonelik kapsamında kullanın:</span><span class="sxs-lookup"><span data-stu-id="c566b-140">toogrant access tooan application at hello subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - AzureRmRoleAssignment yeni - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="c566b-142">Rol tooa kullanıcı hello kaynak grubu kapsamda atama</span><span class="sxs-lookup"><span data-stu-id="c566b-142">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="c566b-143">toogrant erişim tooa kullanıcı hello Kaynak Grup kapsamı, kullanın:</span><span class="sxs-lookup"><span data-stu-id="c566b-143">toogrant access tooa user at hello resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - AzureRmRoleAssignment yeni - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="c566b-145">Bir rol tooa grubu hello kaynak kapsamda atama</span><span class="sxs-lookup"><span data-stu-id="c566b-145">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="c566b-146">toogrant erişim tooa grubu hello kaynak kapsamda kullanın:</span><span class="sxs-lookup"><span data-stu-id="c566b-146">toogrant access tooa group at hello resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - AzureRmRoleAssignment yeni - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="c566b-148">Erişimi kaldırma</span><span class="sxs-lookup"><span data-stu-id="c566b-148">Remove access</span></span>
<span data-ttu-id="c566b-149">Kullanıcılar, gruplar ve uygulamalar, kullanım için tooremove erişim:</span><span class="sxs-lookup"><span data-stu-id="c566b-149">tooremove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="c566b-151">Özel bir rol oluşturun</span><span class="sxs-lookup"><span data-stu-id="c566b-151">Create a custom role</span></span>
<span data-ttu-id="c566b-152">toocreate özel bir rol kullanın hello ```New-AzureRmRoleDefinition``` komutu.</span><span class="sxs-lookup"><span data-stu-id="c566b-152">toocreate a custom role, use hello ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="c566b-153">PSRoleDefinitionObject veya JSON şablonunu kullanarak hello rolünü yapılandırılması için iki yöntem vardır.</span><span class="sxs-lookup"><span data-stu-id="c566b-153">There are two methods of structuring hello role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="c566b-154">Bir kaynak sağlayıcısı için Eylemler Al</span><span class="sxs-lookup"><span data-stu-id="c566b-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="c566b-155">Özel roller sıfırdan oluştururken, önemli tooknow olan tüm olası işlemleri hello kaynak sağlayıcılarından hello.</span><span class="sxs-lookup"><span data-stu-id="c566b-155">When You are creating custom roles from scratch, it is important tooknow all hello possible operations from hello resource providers.</span></span>
<span data-ttu-id="c566b-156">Kullanım hello ```Get-AzureRMProviderOperation``` tooget bu bilgileri komutu.</span><span class="sxs-lookup"><span data-stu-id="c566b-156">Use hello ```Get-AzureRMProviderOperation``` command tooget this information.</span></span>
<span data-ttu-id="c566b-157">Örneğin, toocheck istiyorsanız hello kullanılabilir tüm işlemlerin sanal makine için bu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="c566b-157">For example, if you want toocheck all hello available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="c566b-158">Rolü PSRoleDefinitionObject ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="c566b-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="c566b-159">PowerShell toocreate özel bir rol kullandığınızda, baştan başlayın veya hello birini kullanın [yerleşik roller](role-based-access-built-in-roles.md) bir başlangıç noktası olarak.</span><span class="sxs-lookup"><span data-stu-id="c566b-159">When you use PowerShell toocreate a custom role, you can start from scratch or use one of hello [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="c566b-160">Bu bölümdeki Hello örnek ile yerleşik bir rol başlatır ve daha fazla ayrıcalıklarla özelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c566b-160">hello example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="c566b-161">Merhaba öznitelikleri tooadd hello Düzenle *Eylemler*, *notActions*, veya *kapsamları* ve ardından yeni bir rol olarak hello değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c566b-161">Edit hello attributes tooadd hello *Actions*, *notActions*, or *scopes* that you want, and then save hello changes as a new role.</span></span>

<span data-ttu-id="c566b-162">Merhaba aşağıdaki örnek başlatır ile Merhaba *sanal makine Katılımcısı* rolü ve kullandığı bu toocreate özel bir rol olarak adlandırılan *sanal makine işleci*.</span><span class="sxs-lookup"><span data-stu-id="c566b-162">hello following example starts with hello *Virtual Machine Contributor* role and uses that toocreate a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="c566b-163">Merhaba yeni rol verir erişim tooall okuma işlemlerini *Microsoft.Compute*, *Microsoft.Storage*, ve *Microsoft.Network* kaynak sağlayıcıları ve verir erişimi toostart, yeniden başlatma ve sanal makineleri izleme.</span><span class="sxs-lookup"><span data-stu-id="c566b-163">hello new role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="c566b-164">Merhaba özel rol iki Aboneliklerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c566b-164">hello custom role can be used in two subscriptions.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Contributor"
$role.Id = $null
$role.Name = "Virtual Machine Operator"
$role.Description = "Can monitor and restart virtual machines."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/*/read")
$role.Actions.Add("Microsoft.Network/*/read")
$role.Actions.Add("Microsoft.Compute/*/read")
$role.Actions.Add("Microsoft.Compute/virtualMachines/start/action")
$role.Actions.Add("Microsoft.Compute/virtualMachines/restart/action")
$role.Actions.Add("Microsoft.Authorization/*/read")
$role.Actions.Add("Microsoft.Resources/subscriptions/resourceGroups/read")
$role.Actions.Add("Microsoft.Insights/alertRules/*")
$role.Actions.Add("Microsoft.Support/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e")
$role.AssignableScopes.Add("/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624")
New-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell-Get AzureRmRoleDefinition - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/2-new-azurermroledefinition.png)

### <a name="create-role-with-json-template"></a><span data-ttu-id="c566b-166">Rol JSON şablon oluştur</span><span class="sxs-lookup"><span data-stu-id="c566b-166">Create role with JSON template</span></span>
<span data-ttu-id="c566b-167">Bir JSON şablonu hello kaynak tanımı olarak hello özel rolü için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c566b-167">A JSON template can be used as hello source definition for hello custom role.</span></span> <span data-ttu-id="c566b-168">Merhaba aşağıdaki örnekte oluşturur okuma erişimi toostorage sağlar ve işlem kaynaklarını, toosupport erişmek ve bu rol eklediği özel bir rol tootwo abonelikleri.</span><span class="sxs-lookup"><span data-stu-id="c566b-168">hello following example creates a custom role that allows read access toostorage and compute resources, access toosupport, and adds that role tootwo subscriptions.</span></span> <span data-ttu-id="c566b-169">Yeni bir dosya oluşturun `C:\CustomRoles\customrole1.json` hello aşağıdaki örneğine sahip.</span><span class="sxs-lookup"><span data-stu-id="c566b-169">Create a new file `C:\CustomRoles\customrole1.json` with hello following example.</span></span> <span data-ttu-id="c566b-170">Merhaba kimliği çok ayarlanmalıdır`null` yeni kimliği olarak ilk rol oluşturma sırasında otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c566b-170">hello Id should be set too`null` on initial role creation as a new ID is generated automatically.</span></span> 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```
<span data-ttu-id="c566b-171">PowerShell komutunu aşağıdaki hello çalıştırmak tooadd hello rol toohello abonelikleri:</span><span class="sxs-lookup"><span data-stu-id="c566b-171">tooadd hello role toohello subscriptions, run hello following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="c566b-172">Özel bir rol değiştirme</span><span class="sxs-lookup"><span data-stu-id="c566b-172">Modify a custom role</span></span>
<span data-ttu-id="c566b-173">Benzer toocreating özel bir rol, var olan bir özel rol hello PSRoleDefinitionObject ya da bir JSON şablonu kullanarak değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c566b-173">Similar toocreating a custom role, you can modify an existing custom role using either hello PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="c566b-174">PSRoleDefinitionObject rolüyle Değiştir</span><span class="sxs-lookup"><span data-stu-id="c566b-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="c566b-175">toomodify özel bir rol ilk olarak, hello kullanın `Get-AzureRmRoleDefinition` tooretrieve hello rol tanımı komutu.</span><span class="sxs-lookup"><span data-stu-id="c566b-175">toomodify a custom role, first, use hello `Get-AzureRmRoleDefinition` command tooretrieve hello role definition.</span></span> <span data-ttu-id="c566b-176">İkinci olarak, toohello rol tanımı hello gerekli değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="c566b-176">Second, make hello desired changes toohello role definition.</span></span> <span data-ttu-id="c566b-177">Son olarak, hello kullan `Set-AzureRmRoleDefinition` komutu toosave hello rol tanımını değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="c566b-177">Finally, use hello `Set-AzureRmRoleDefinition` command toosave hello modified role definition.</span></span>

<span data-ttu-id="c566b-178">Merhaba aşağıdaki örnek, hello `Microsoft.Insights/diagnosticSettings/*` işlemi toohello *sanal makine işleci* özel rol.</span><span class="sxs-lookup"><span data-stu-id="c566b-178">hello following example adds hello `Microsoft.Insights/diagnosticSettings/*` operation toohello *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="c566b-180">Merhaba aşağıdaki örnek, bir Azure aboneliği toohello atanabilir kapsamların hello *sanal makine işleci* özel rol.</span><span class="sxs-lookup"><span data-stu-id="c566b-180">hello following example adds an Azure subscription toohello assignable scopes of hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="c566b-182">JSON şablonunu rolüyle Değiştir</span><span class="sxs-lookup"><span data-stu-id="c566b-182">Modify role with JSON template</span></span>
<span data-ttu-id="c566b-183">Merhaba önceki JSON şablonunu kullanarak, kolayca var olan bir özel rol tooadd değiştirebilir veya eylemleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="c566b-183">Using hello previous JSON template, you can easily modify an existing custom role tooadd or remove Actions.</span></span> <span data-ttu-id="c566b-184">Merhaba JSON şablonunu güncelleştirmek ve ağ iletişimi için okuma eylemini hello hello aşağıdaki örnekte gösterildiği gibi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c566b-184">Update hello JSON template and add hello read action for networking as shown in hello following example.</span></span> <span data-ttu-id="c566b-185">Merhaba şablonunda listelenen hello tanımları hello şablonunda tam olarak belirttiğiniz gibi bu hello rol görünür anlamı üst üste uygulanan tooan varolan tanımı olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="c566b-185">hello definitions listed in hello template are not cumulatively applied tooan existing definition, meaning that hello role appears exactly as you specify in hello template.</span></span> <span data-ttu-id="c566b-186">Ayrıca tooupdate hello Kimliği alanı hello rol hello kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="c566b-186">You also need tooupdate hello Id field with hello ID of hello role.</span></span> <span data-ttu-id="c566b-187">Bu değer nedir emin değilseniz, hello kullanabilirsiniz `Get-AzureRmRoleDefinition` cmdlet tooget bu bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c566b-187">If you aren't sure what this value is, you can use hello `Get-AzureRmRoleDefinition` cmdlet tooget this information.</span></span>

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```

<span data-ttu-id="c566b-188">tooupdate hello varolan rolü, hello aşağıdaki PowerShell komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c566b-188">tooupdate hello existing role, run hello following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="c566b-189">Bir özel rolü silmeyi</span><span class="sxs-lookup"><span data-stu-id="c566b-189">Delete a custom role</span></span>
<span data-ttu-id="c566b-190">toodelete özel bir rol kullanın hello `Remove-AzureRmRoleDefinition` komutu.</span><span class="sxs-lookup"><span data-stu-id="c566b-190">toodelete a custom role, use hello `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="c566b-191">Merhaba aşağıdaki örnek kaldırır hello *sanal makine işleci* özel rol.</span><span class="sxs-lookup"><span data-stu-id="c566b-191">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="c566b-193">Liste özel roller</span><span class="sxs-lookup"><span data-stu-id="c566b-193">List custom roles</span></span>
<span data-ttu-id="c566b-194">bir kapsamda atama için kullanılabilen toolist hello rolleri kullanmak hello `Get-AzureRmRoleDefinition` komutu.</span><span class="sxs-lookup"><span data-stu-id="c566b-194">toolist hello roles that are available for assignment at a scope, use hello `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="c566b-195">Aşağıdaki örneğine hello hello seçili Abonelikteki atama için kullanılabilen tüm rolleri listeler.</span><span class="sxs-lookup"><span data-stu-id="c566b-195">hello following example lists all roles that are available for assignment in hello selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell-Get AzureRmRoleDefinition - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="c566b-197">Aşağıdaki örneğine hello hello *sanal makine işleci* özel rol hello kullanılamaz *Production4* abonelik Bu abonelik hello olmadığından  **AssignableScopes** hello rolünün.</span><span class="sxs-lookup"><span data-stu-id="c566b-197">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

![RBAC PowerShell-Get AzureRmRoleDefinition - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="c566b-199">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="c566b-199">See also</span></span>
* <span data-ttu-id="c566b-200">[Azure Resource Manager ile Azure PowerShell'i kullanma](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span><span class="sxs-lookup"><span data-stu-id="c566b-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

