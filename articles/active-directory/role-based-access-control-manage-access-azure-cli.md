---
title: "Rol tabanlı erişim denetimi (RBAC) Azure CLI ile aaaManage | Microsoft Docs"
description: "Nasıl toomanage rol tabanlı erişim denetimi (RBAC) ile hello Azure komut satırı arabirimi listeleme rolleri ve rol tarafından Eylemler öğrenin ve rolleri toohello abonelik ve uygulama kapsamları atayarak."
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
ms.openlocfilehash: 438418e5f6ee9b98908c9c264d516eb722a4e26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a><span data-ttu-id="1c248-103">Rol tabanlı erişim denetimi hello Azure komut satırı arabirimi ile yönetme</span><span class="sxs-lookup"><span data-stu-id="1c248-103">Manage Role-Based Access Control with hello Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1c248-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c248-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="1c248-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1c248-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="1c248-106">REST API</span><span class="sxs-lookup"><span data-stu-id="1c248-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="1c248-107">Rol tabanlı erişim denetimi (RBAC) hello Azure portal, Azure Kaynak Yöneticisi API'si toomanage erişim tooyour abonelik ve hassas düzeyinde kaynakları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1c248-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API toomanage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="1c248-108">Bu özellik ile bazı roller toothem belirli bir kapsamda atayarak Active Directory Kullanıcıları, grupları veya hizmet asıl adı için erişim izni verebilir.</span><span class="sxs-lookup"><span data-stu-id="1c248-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="1c248-109">Hello Azure komut satırı arabirimi (CLI) toomanage RBAC kullanmadan önce aşağıdaki önkoşullar hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1c248-109">Before you can use hello Azure command-line interface (CLI) toomanage RBAC, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="1c248-110">Azure CLI Sürüm 0.8.8 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="1c248-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="1c248-111">tooinstall hello en son sürümünü ve ilişkilendirme Azure aboneliğinizle görmek [hello Azure CLI yükleyip](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="1c248-111">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="1c248-112">Azure Resource Manager'da Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1c248-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="1c248-113">Çok Git[hello Resource Manager ile Azure CLI kullanarak hello](../xplat-cli-azure-resource-manager.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="1c248-113">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="1c248-114">Liste rolleri</span><span class="sxs-lookup"><span data-stu-id="1c248-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="1c248-115">Kullanılabilir tüm roller listesinde</span><span class="sxs-lookup"><span data-stu-id="1c248-115">List all available roles</span></span>
<span data-ttu-id="1c248-116">kullanılabilir tüm roller toolist kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c248-116">toolist all available roles, use:</span></span>

        azure role list

<span data-ttu-id="1c248-117">Merhaba aşağıdaki örnek hello listesini gösterir *kullanılabilir tüm roller*.</span><span class="sxs-lookup"><span data-stu-id="1c248-117">hello following example shows hello list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![RBAC Azure komut satırı - azure rol listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="1c248-119">Bir rolün liste eylemleri</span><span class="sxs-lookup"><span data-stu-id="1c248-119">List actions of a role</span></span>
<span data-ttu-id="1c248-120">bir rolün toolist hello eylemlerini kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c248-120">toolist hello actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="1c248-121">Merhaba aşağıdaki örnekte gösterilir hello hello eylemlerini *katkıda bulunan* ve *sanal makine Katılımcısı* rolleri.</span><span class="sxs-lookup"><span data-stu-id="1c248-121">hello following example shows hello actions of hello *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![RBAC Azure komut satırı - azure rol Göster - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="1c248-123">Liste erişim</span><span class="sxs-lookup"><span data-stu-id="1c248-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="1c248-124">Liste rol atamalarını bir kaynak grubu üzerinde etkin</span><span class="sxs-lookup"><span data-stu-id="1c248-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="1c248-125">bir kaynak grubunda kullanımı mevcut toolist hello rol atamaları:</span><span class="sxs-lookup"><span data-stu-id="1c248-125">toolist hello role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="1c248-126">Merhaba aşağıdaki örnek hello rol atamalarını hello gösterir *pharma satış projecforcast* grubu.</span><span class="sxs-lookup"><span data-stu-id="1c248-126">hello following example shows hello role assignments in hello *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![RBAC Azure komut satırı - grubuna göre azure rol ataması listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="1c248-128">Bir kullanıcı için rol atamalarını listesi</span><span class="sxs-lookup"><span data-stu-id="1c248-128">List role assignments for a user</span></span>
<span data-ttu-id="1c248-129">belirli bir kullanıcı için toolist hello rol atamalarını ve tooa kullanıcının gruplar, atanan hello atamalarını kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c248-129">toolist hello role assignments for a specific user and hello assignments that are assigned tooa user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="1c248-130">Merhaba komutu değiştirerek gruplarından devralınan rol atamalarını de görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1c248-130">You can also see role assignments that are inherited from groups by modifying hello command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="1c248-131">Merhaba aşağıdaki örnekte gösterilir toohello verilen hello rol atamalarını  *sameert@aaddemo.com*  kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="1c248-131">hello following example shows hello role assignments that are granted toohello *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="1c248-132">Bu, doğrudan toohello kullanıcı atanan rolleri ve gruplardan devralınan rolleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1c248-132">This includes roles that are assigned directly toohello user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![RBAC Azure komut satırı - kullanıcı tarafından azure rol ataması listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="1c248-134">Erişim verme</span><span class="sxs-lookup"><span data-stu-id="1c248-134">Grant access</span></span>
<span data-ttu-id="1c248-135">toogrant erişim hello rol tooassign istediğinizi belirledikten sonra kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c248-135">toogrant access after you have identified hello role that you want tooassign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a><span data-ttu-id="1c248-136">Merhaba abonelik kapsamında bir rol toogroup atayın</span><span class="sxs-lookup"><span data-stu-id="1c248-136">Assign a role toogroup at hello subscription scope</span></span>
<span data-ttu-id="1c248-137">tooassign rol tooa grubunu hello abonelik kapsamında kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c248-137">tooassign a role tooa group at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="1c248-138">Merhaba aşağıdaki örnek atar hello *okuyucu* rol çok*Christine Koch'ın takım* hello adresindeki *abonelik* kapsam.</span><span class="sxs-lookup"><span data-stu-id="1c248-138">hello following example assigns hello *Reader* role too*Christine Koch's Team* at hello *subscription* scope.</span></span>

![RBAC Azure komut satırı - azure rol ataması oluşturma grupla - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="1c248-140">Merhaba abonelik kapsamında bir rol tooan uygulama atama</span><span class="sxs-lookup"><span data-stu-id="1c248-140">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="1c248-141">tooassign rol tooan uygulama hello abonelik kapsamında kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c248-141">tooassign a role tooan application at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="1c248-142">Merhaba aşağıdaki örnek verir hello *katkıda bulunan* rol tooan *Azure AD* hello uygulama seçili abonelik.</span><span class="sxs-lookup"><span data-stu-id="1c248-142">hello following example grants hello *Contributor* role tooan *Azure AD* application on hello selected subscription.</span></span>

 ![RBAC Azure komut satırı - azure rol ataması oluşturma uygulama tarafından](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="1c248-144">Rol tooa kullanıcı hello kaynak grubu kapsamda atama</span><span class="sxs-lookup"><span data-stu-id="1c248-144">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="1c248-145">tooassign bir rol tooa kullanıcı hello Kaynak Grup kapsamı, kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c248-145">tooassign a role tooa user at hello resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="1c248-146">Merhaba aşağıdaki örnek verir hello *sanal makine Katılımcısı* rol çok *samert@aaddemo.com*  hello kullanıcı *Pharma satış ProjectForcast* Kaynak Grup kapsamı.</span><span class="sxs-lookup"><span data-stu-id="1c248-146">hello following example grants hello *Virtual Machine Contributor* role too*samert@aaddemo.com* user at hello *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![RBAC Azure komut satırı - azure rol ataması oluşturma kullanıcı - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="1c248-148">Bir rol tooa grubu hello kaynak kapsamda atama</span><span class="sxs-lookup"><span data-stu-id="1c248-148">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="1c248-149">tooassign rol tooa grubunu hello kaynak kapsamda kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c248-149">tooassign a role tooa group at hello resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="1c248-150">Merhaba aşağıdaki örnek verir hello *sanal makine Katılımcısı* rol tooan *Azure AD* grubunun bir *alt*.</span><span class="sxs-lookup"><span data-stu-id="1c248-150">hello following example grants hello *Virtual Machine Contributor* role tooan *Azure AD* group on a *subnet*.</span></span>

![RBAC Azure komut satırı - azure rol ataması oluşturma grupla - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="1c248-152">Erişimi kaldırma</span><span class="sxs-lookup"><span data-stu-id="1c248-152">Remove access</span></span>
<span data-ttu-id="1c248-153">bir rol ataması tooremove kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c248-153">tooremove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

<span data-ttu-id="1c248-154">Merhaba aşağıdaki örnek kaldırır hello *sanal makine Katılımcısı* hello gelen rol atamasını  *sammert@aaddemo.com*  hello kullanıcı *Pharma satış ProjectForcast* kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="1c248-154">hello following example removes hello *Virtual Machine Contributor* role assignment from hello *sammert@aaddemo.com* user on hello *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="1c248-155">Merhaba örneği bu durumda bir grup hello abonelik üzerinde hello rol ataması kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1c248-155">hello example then removes hello role assignment from a group on hello subscription.</span></span>

![RBAC Azure komut satırı - azure rol ataması delete - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="1c248-157">Özel bir rol oluşturun</span><span class="sxs-lookup"><span data-stu-id="1c248-157">Create a custom role</span></span>
<span data-ttu-id="1c248-158">toocreate özel bir rol kullanın:</span><span class="sxs-lookup"><span data-stu-id="1c248-158">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="1c248-159">Merhaba aşağıdaki örnekte oluşturur adlı özel bir rol *sanal makine işleci*.</span><span class="sxs-lookup"><span data-stu-id="1c248-159">hello following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="1c248-160">Bu özel rolü erişim tooall okuma işlemlerini verir *Microsoft.Compute*, *Microsoft.Storage*, ve *Microsoft.Network* kaynak sağlayıcıları ve verir erişimi toostart, yeniden başlatma ve sanal makineleri izleme.</span><span class="sxs-lookup"><span data-stu-id="1c248-160">This custom role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="1c248-161">Bu özel rolü iki Aboneliklerde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1c248-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="1c248-162">Bu örnek bir JSON dosyası bir giriş olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="1c248-162">This example uses a JSON file as an input.</span></span>

![JSON - özel rol tanımı - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![RBAC Azure komut satırı - azure rol oluşturma - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="1c248-165">Özel bir rol değiştirme</span><span class="sxs-lookup"><span data-stu-id="1c248-165">Modify a custom role</span></span>
<span data-ttu-id="1c248-166">toomodify özel bir rol ilk hello kullan `azure role show` tooretrieve rol tanımı komutu.</span><span class="sxs-lookup"><span data-stu-id="1c248-166">toomodify a custom role, first use hello `azure role show` command tooretrieve role definition.</span></span> <span data-ttu-id="1c248-167">İkinci olarak, hello istediğiniz değişiklikleri toohello rol tanımı dosyası olun.</span><span class="sxs-lookup"><span data-stu-id="1c248-167">Second, make hello desired changes toohello role definition file.</span></span> <span data-ttu-id="1c248-168">Son olarak, `azure role set` toosave hello rol tanımını değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="1c248-168">Finally, use `azure role set` toosave hello modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="1c248-169">Merhaba aşağıdaki örnek, hello *Microsoft.Insights/diagnosticSettings/* işlemi toohello **Eylemler**ve bir Azure aboneliği toohello **AssignableScopes**hello sanal makine işletmeni özel rolü.</span><span class="sxs-lookup"><span data-stu-id="1c248-169">hello following example adds hello *Microsoft.Insights/diagnosticSettings/* operation toohello **Actions**, and an Azure subscription toohello **AssignableScopes** of hello Virtual Machine Operator custom role.</span></span>

![JSON - özel rol tanımını - ekran görüntüsü değiştirme](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![RBAC Azure komut satırı - azure rol set - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="1c248-172">Bir özel rolü silmeyi</span><span class="sxs-lookup"><span data-stu-id="1c248-172">Delete a custom role</span></span>
<span data-ttu-id="1c248-173">toodelete özel bir rol ilk hello kullan `azure role show` komutu toodetermine hello **kimliği** hello rolünün.</span><span class="sxs-lookup"><span data-stu-id="1c248-173">toodelete a custom role, first use hello `azure role show` command toodetermine hello **ID** of hello role.</span></span> <span data-ttu-id="1c248-174">Ardından hello kullanın `azure role delete` hello belirterek komutu toodelete hello rol **kimliği**.</span><span class="sxs-lookup"><span data-stu-id="1c248-174">Then, use hello `azure role delete` command toodelete hello role by specifying hello **ID**.</span></span>

<span data-ttu-id="1c248-175">Merhaba aşağıdaki örnek kaldırır hello *sanal makine işleci* özel rol.</span><span class="sxs-lookup"><span data-stu-id="1c248-175">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

![RBAC Azure komut satırı - azure rol silme - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="1c248-177">Liste özel roller</span><span class="sxs-lookup"><span data-stu-id="1c248-177">List custom roles</span></span>
<span data-ttu-id="1c248-178">bir kapsamda atama için kullanılabilen toolist hello rolleri kullanmak hello `azure role list` komutu.</span><span class="sxs-lookup"><span data-stu-id="1c248-178">toolist hello roles that are available for assignment at a scope, use hello `azure role list` command.</span></span>

<span data-ttu-id="1c248-179">komutu aşağıdaki hello hello seçili Abonelikteki atama için kullanılabilen tüm rolleri listeler.</span><span class="sxs-lookup"><span data-stu-id="1c248-179">hello following command lists all roles that are available for assignment in hello selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![RBAC Azure komut satırı - azure rol listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="1c248-181">Aşağıdaki örneğine hello hello *sanal makine işleci* özel rol hello kullanılamaz *Production4* abonelik Bu abonelik hello olmadığından  **AssignableScopes** hello rolünün.</span><span class="sxs-lookup"><span data-stu-id="1c248-181">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![RBAC Azure komut satırı - özel roller için azure rol listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="1c248-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1c248-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

