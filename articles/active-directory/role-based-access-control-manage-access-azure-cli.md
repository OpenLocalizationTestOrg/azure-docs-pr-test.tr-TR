---
title: "Rol tabanlı erişim denetimi (RBAC) Azure CLI ile yönetme | Microsoft Docs"
description: "Rolleri ve rol eylemlerin listesini içeren ve rolleri için abonelik ve uygulama kapsamları atama rol tabanlı erişim denetimi (RBAC) Azure komut satırı arabirimi ile yönetmeyi öğrenin."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 3483ee01-8177-49e7-b337-4d5cb14f5e32
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: ad644de6d23950e699d99042d27381336626caab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-azure-command-line-interface"></a><span data-ttu-id="00d46-103">Rol tabanlı erişim denetimini Azure komut satırı arabirimi ile yönetme</span><span class="sxs-lookup"><span data-stu-id="00d46-103">Manage Role-Based Access Control with the Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="00d46-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="00d46-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="00d46-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="00d46-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="00d46-106">REST API</span><span class="sxs-lookup"><span data-stu-id="00d46-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="00d46-107">Abonelik ve ayrıntılı bir düzeyde kaynaklarınıza erişimi yönetmek için rol tabanlı erişim denetimi (RBAC) Azure portalında ve Azure Resource Manager API'sini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00d46-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API to manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="00d46-108">Bu özellik ile bazı roller belirli bir kapsamda atayarak Active Directory Kullanıcıları, grupları veya hizmet asıl adı için erişim izni verebilir.</span><span class="sxs-lookup"><span data-stu-id="00d46-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="00d46-109">RBAC yönetmek için Azure komut satırı arabirimi (CLI) kullanmadan önce aşağıdaki önkoşullara sahip olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="00d46-109">Before you can use the Azure command-line interface (CLI) to manage RBAC, you must have the following prerequisites:</span></span>

* <span data-ttu-id="00d46-110">Azure CLI Sürüm 0.8.8 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="00d46-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="00d46-111">En son sürümünü yükleyin ve Azure aboneliğinizle ilişkilendirmek için bkz: [Azure CLI'yi yükleme ve yapılandırma](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="00d46-111">To install the latest version and associate it with your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="00d46-112">Azure Resource Manager'da Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="00d46-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="00d46-113">Git [Resource Manager ile Azure CLI kullanarak](../xplat-cli-azure-resource-manager.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="00d46-113">Go to [Using the Azure CLI with the Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="00d46-114">Liste rolleri</span><span class="sxs-lookup"><span data-stu-id="00d46-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="00d46-115">Kullanılabilir tüm roller listesinde</span><span class="sxs-lookup"><span data-stu-id="00d46-115">List all available roles</span></span>
<span data-ttu-id="00d46-116">Kullanılabilir tüm roller listelemek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="00d46-116">To list all available roles, use:</span></span>

        azure role list

<span data-ttu-id="00d46-117">Aşağıdaki örnek listesini gösterir *kullanılabilir tüm roller*.</span><span class="sxs-lookup"><span data-stu-id="00d46-117">The following example shows the list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![RBAC Azure komut satırı - azure rol listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="00d46-119">Bir rolün liste eylemleri</span><span class="sxs-lookup"><span data-stu-id="00d46-119">List actions of a role</span></span>
<span data-ttu-id="00d46-120">Bir rolü Eylemler listelemek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="00d46-120">To list the actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="00d46-121">Aşağıdaki örnek, eylemleri gösterir *katkıda bulunan* ve *sanal makine Katılımcısı* rolleri.</span><span class="sxs-lookup"><span data-stu-id="00d46-121">The following example shows the actions of the *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![RBAC Azure komut satırı - azure rol Göster - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="00d46-123">Liste erişim</span><span class="sxs-lookup"><span data-stu-id="00d46-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="00d46-124">Liste rol atamalarını bir kaynak grubu üzerinde etkin</span><span class="sxs-lookup"><span data-stu-id="00d46-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="00d46-125">Bir kaynak grubunda mevcut rol atamalarını listelemek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="00d46-125">To list the role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="00d46-126">Aşağıdaki örnek, rol atamalarında gösterir *pharma satış projecforcast* grubu.</span><span class="sxs-lookup"><span data-stu-id="00d46-126">The following example shows the role assignments in the *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![RBAC Azure komut satırı - grubuna göre azure rol ataması listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="00d46-128">Bir kullanıcı için rol atamalarını listesi</span><span class="sxs-lookup"><span data-stu-id="00d46-128">List role assignments for a user</span></span>
<span data-ttu-id="00d46-129">Belirli bir kullanıcı için rol atamalarını ve kullanıcı gruplarına atanır atamalarını listelemek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="00d46-129">To list the role assignments for a specific user and the assignments that are assigned to a user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="00d46-130">Ayrıca komut değiştirerek gruplarından devralınan rol atamalarını görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="00d46-130">You can also see role assignments that are inherited from groups by modifying the command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="00d46-131">Aşağıdaki örnekte verilen rol atamalarını  *sameert@aaddemo.com*  kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="00d46-131">The following example shows the role assignments that are granted to the *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="00d46-132">Bu kullanıcıya atanan rollerin ve gruplardan devralınan rolleri içerir.</span><span class="sxs-lookup"><span data-stu-id="00d46-132">This includes roles that are assigned directly to the user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![RBAC Azure komut satırı - kullanıcı tarafından azure rol ataması listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="00d46-134">Erişim verme</span><span class="sxs-lookup"><span data-stu-id="00d46-134">Grant access</span></span>
<span data-ttu-id="00d46-135">Atamak istediğiniz rolü tanımladıktan sonra erişim vermek için kullanın:</span><span class="sxs-lookup"><span data-stu-id="00d46-135">To grant access after you have identified the role that you want to assign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-to-group-at-the-subscription-scope"></a><span data-ttu-id="00d46-136">Grup aboneliği kapsamında bir rol atayın</span><span class="sxs-lookup"><span data-stu-id="00d46-136">Assign a role to group at the subscription scope</span></span>
<span data-ttu-id="00d46-137">Bir grup aboneliği kapsamında bir rol atamak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="00d46-137">To assign a role to a group at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="00d46-138">Aşağıdaki örnek atar *okuyucu* rolüne *Christine Koch'ın takım* adresindeki *abonelik* kapsam.</span><span class="sxs-lookup"><span data-stu-id="00d46-138">The following example assigns the *Reader* role to *Christine Koch's Team* at the *subscription* scope.</span></span>

![RBAC Azure komut satırı - azure rol ataması oluşturma grupla - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="00d46-140">Uygulamanın abonelik kapsamında bir rol atayın</span><span class="sxs-lookup"><span data-stu-id="00d46-140">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="00d46-141">Bir uygulama abonelik kapsamında bir rol atamak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="00d46-141">To assign a role to an application at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="00d46-142">Aşağıdaki örnek verir *katkıda bulunan* rolüne bir *Azure AD* seçilen aboneliğe ilişkin uygulama.</span><span class="sxs-lookup"><span data-stu-id="00d46-142">The following example grants the *Contributor* role to an *Azure AD* application on the selected subscription.</span></span>

 ![RBAC Azure komut satırı - azure rol ataması oluşturma uygulama tarafından](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="00d46-144">Kaynak grubu kapsamındaki bir kullanıcıya rol atama</span><span class="sxs-lookup"><span data-stu-id="00d46-144">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="00d46-145">Kaynak grubu kapsamındaki bir kullanıcıya rol atamak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="00d46-145">To assign a role to a user at the resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="00d46-146">Aşağıdaki örnek verir *sanal makine Katılımcısı* rolüne  *samert@aaddemo.com*  kullanıcı *Pharma satış ProjectForcast* Kaynak Grup kapsamı.</span><span class="sxs-lookup"><span data-stu-id="00d46-146">The following example grants the *Virtual Machine Contributor* role to *samert@aaddemo.com* user at the *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![RBAC Azure komut satırı - azure rol ataması oluşturma kullanıcı - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="00d46-148">Kaynak kapsamdaki bir gruba rol atama</span><span class="sxs-lookup"><span data-stu-id="00d46-148">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="00d46-149">Rol kaynak kapsamdaki bir gruba atamak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="00d46-149">To assign a role to a group at the resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="00d46-150">Aşağıdaki örnek verir *sanal makine Katılımcısı* rolüne bir *Azure AD* grubunun bir *alt*.</span><span class="sxs-lookup"><span data-stu-id="00d46-150">The following example grants the *Virtual Machine Contributor* role to an *Azure AD* group on a *subnet*.</span></span>

![RBAC Azure komut satırı - azure rol ataması oluşturma grupla - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="00d46-152">Erişimi kaldırma</span><span class="sxs-lookup"><span data-stu-id="00d46-152">Remove access</span></span>
<span data-ttu-id="00d46-153">Bir rol atamasını kaldırmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="00d46-153">To remove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id to from which to remove role> --roleName "<role name>"

<span data-ttu-id="00d46-154">Aşağıdaki örnek kaldırır *sanal makine Katılımcısı* gelen rol atamasını  *sammert@aaddemo.com*  kullanıcı *Pharma satış ProjectForcast* kaynak Grup.</span><span class="sxs-lookup"><span data-stu-id="00d46-154">The following example removes the *Virtual Machine Contributor* role assignment from the *sammert@aaddemo.com* user on the *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="00d46-155">Örneğin bu durumda bir grup aboneliği üzerinde rol ataması kaldırır.</span><span class="sxs-lookup"><span data-stu-id="00d46-155">The example then removes the role assignment from a group on the subscription.</span></span>

![RBAC Azure komut satırı - azure rol ataması delete - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="00d46-157">Özel bir rol oluşturun</span><span class="sxs-lookup"><span data-stu-id="00d46-157">Create a custom role</span></span>
<span data-ttu-id="00d46-158">Özel bir rol oluşturmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="00d46-158">To create a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="00d46-159">Aşağıdaki örnek adlı özel bir rol oluşturur *sanal makine işleci*.</span><span class="sxs-lookup"><span data-stu-id="00d46-159">The following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="00d46-160">Bu özel rolü tüm okuma işlemlerini erişim veren *Microsoft.Compute*, *Microsoft.Storage*, ve *Microsoft.Network* kaynak sağlayıcıları ve verir erişmek için Başlat, yeniden başlatın ve sanal makineleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="00d46-160">This custom role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="00d46-161">Bu özel rolü iki Aboneliklerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="00d46-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="00d46-162">Bu örnek bir JSON dosyası bir giriş olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="00d46-162">This example uses a JSON file as an input.</span></span>

![JSON - özel rol tanımı - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![RBAC Azure komut satırı - azure rol oluşturma - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="00d46-165">Özel bir rol değiştirme</span><span class="sxs-lookup"><span data-stu-id="00d46-165">Modify a custom role</span></span>
<span data-ttu-id="00d46-166">Özel bir rol değiştirmek için önce kullanın `azure role show` rol tanımı almak için komutu.</span><span class="sxs-lookup"><span data-stu-id="00d46-166">To modify a custom role, first use the `azure role show` command to retrieve role definition.</span></span> <span data-ttu-id="00d46-167">İkinci olarak, rol tanımı dosyasına istediğiniz değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="00d46-167">Second, make the desired changes to the role definition file.</span></span> <span data-ttu-id="00d46-168">Son olarak, `azure role set` değiştirilmiş rol tanımı kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="00d46-168">Finally, use `azure role set` to save the modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="00d46-169">Aşağıdaki örnek, *Microsoft.Insights/diagnosticSettings/* işlemi için **Eylemler**ve bir Azure aboneliğine **AssignableScopes** , Sanal makine işletmeni özel rolü.</span><span class="sxs-lookup"><span data-stu-id="00d46-169">The following example adds the *Microsoft.Insights/diagnosticSettings/* operation to the **Actions**, and an Azure subscription to the **AssignableScopes** of the Virtual Machine Operator custom role.</span></span>

![JSON - özel rol tanımını - ekran görüntüsü değiştirme](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![RBAC Azure komut satırı - azure rol set - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="00d46-172">Bir özel rolü silmeyi</span><span class="sxs-lookup"><span data-stu-id="00d46-172">Delete a custom role</span></span>
<span data-ttu-id="00d46-173">Bir özel rolü silmek için önce kullanın `azure role show` belirlemek için komut **kimliği** rolünün.</span><span class="sxs-lookup"><span data-stu-id="00d46-173">To delete a custom role, first use the `azure role show` command to determine the **ID** of the role.</span></span> <span data-ttu-id="00d46-174">Ardından, `azure role delete` belirterek bu rolü silmek için komutu **kimliği**.</span><span class="sxs-lookup"><span data-stu-id="00d46-174">Then, use the `azure role delete` command to delete the role by specifying the **ID**.</span></span>

<span data-ttu-id="00d46-175">Aşağıdaki örnek kaldırır *sanal makine işleci* özel rol.</span><span class="sxs-lookup"><span data-stu-id="00d46-175">The following example removes the *Virtual Machine Operator* custom role.</span></span>

![RBAC Azure komut satırı - azure rol silme - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="00d46-177">Liste özel roller</span><span class="sxs-lookup"><span data-stu-id="00d46-177">List custom roles</span></span>
<span data-ttu-id="00d46-178">Bir kapsamda atama için kullanılabilen rolleri listelemek için kullanın `azure role list` komutu.</span><span class="sxs-lookup"><span data-stu-id="00d46-178">To list the roles that are available for assignment at a scope, use the `azure role list` command.</span></span>

<span data-ttu-id="00d46-179">Aşağıdaki komut, seçili Abonelikteki ataması için kullanılabilen tüm rolleri listeler.</span><span class="sxs-lookup"><span data-stu-id="00d46-179">The following command lists all roles that are available for assignment in the selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![RBAC Azure komut satırı - azure rol listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="00d46-181">Aşağıdaki örnekte, *sanal makine işleci* de özel rol kullanılamaz *Production4* abonelik bu aboneliği değil çünkü **AssignableScopes** rolünün.</span><span class="sxs-lookup"><span data-stu-id="00d46-181">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![RBAC Azure komut satırı - özel roller için azure rol listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="00d46-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="00d46-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

