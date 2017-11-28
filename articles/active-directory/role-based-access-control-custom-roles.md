---
title: "Azure RBAC için özel roller aaaCreate | Microsoft Docs"
description: "Bilgi nasıl toodefine Azure aboneliğinizde daha kesin kimlik yönetimi için Azure rol tabanlı erişim denetimi ile özel roller."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="65544-103">Azure rol tabanlı erişim denetimi için özel roller oluşturma</span><span class="sxs-lookup"><span data-stu-id="65544-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="65544-104">Merhaba yerleşik roller hiçbiri belirli erişim gereksinimlerinizi karşılıyorsa özel bir rol Azure rol tabanlı erişim denetimi (RBAC) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="65544-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of hello built-in roles meet your specific access needs.</span></span> <span data-ttu-id="65544-105">Özel roller kullanılarak oluşturulabilir [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure komut satırı arabirimi](role-based-access-control-manage-access-azure-cli.md) (CLI) ve hello [REST API](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="65544-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and hello [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="65544-106">Yalnızca yerleşik roller gibi özel roller toousers, grupları ve uygulamaları abonelik, kaynak grubu ve kaynak kapsamları atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65544-106">Just like built-in roles, you can assign custom roles toousers, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="65544-107">Özel roller Azure AD kiracısı içinde depolanır ve abonelikler arasında paylaşılabilir.</span><span class="sxs-lookup"><span data-stu-id="65544-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="65544-108">Her bir kiracı too2000 özel rolleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65544-108">Each tenant can create up too2000 custom roles.</span></span> 

<span data-ttu-id="65544-109">Merhaba aşağıdaki örnek izleme ve sanal makineleri yeniden başlatmayı için özel bir rol gösterir:</span><span class="sxs-lookup"><span data-stu-id="65544-109">hello following example shows a custom role for monitoring and restarting virtual machines:</span></span>

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a><span data-ttu-id="65544-110">Eylemler</span><span class="sxs-lookup"><span data-stu-id="65544-110">Actions</span></span>
<span data-ttu-id="65544-111">Merhaba **Eylemler** özel bir rol özelliği belirtir hello Azure işlemleri toowhich hello rol erişim verir.</span><span class="sxs-lookup"><span data-stu-id="65544-111">hello **Actions** property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span> <span data-ttu-id="65544-112">Azure kaynak sağlayıcıları güvenliği sağlanabilir işlemlerini tanımlayan işlemi dizelerin koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="65544-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="65544-113">İşlemi dizeleri izleyin hello biçimi `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span><span class="sxs-lookup"><span data-stu-id="65544-113">Operation strings follow hello format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="65544-114">Joker karakterler içeren işlemi dizeleri (\*) hello işlemi dizeyi eşleştir tooall işlemleri erişim verin.</span><span class="sxs-lookup"><span data-stu-id="65544-114">Operation strings that contain wildcards (\*) grant access tooall operations that match hello operation string.</span></span> <span data-ttu-id="65544-115">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="65544-115">For instance:</span></span>

* <span data-ttu-id="65544-116">`*/read`verir tooread işlemleri tüm Azure kaynak sağlayıcıları tüm kaynak türleri için erişim.</span><span class="sxs-lookup"><span data-stu-id="65544-116">`*/read` grants access tooread operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="65544-117">`Microsoft.Compute/*`verir tooall işlemleri hello Microsoft.Compute kaynak sağlayıcısındaki tüm kaynak türleri için erişim.</span><span class="sxs-lookup"><span data-stu-id="65544-117">`Microsoft.Compute/*` grants access tooall operations for all resource types in hello Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="65544-118">`Microsoft.Network/*/read`verir tooread işlemleri Azure hello Microsoft.Network kaynak Sağlayıcısı'nda tüm kaynak türleri için erişim.</span><span class="sxs-lookup"><span data-stu-id="65544-118">`Microsoft.Network/*/read` grants access tooread operations for all resource types in hello Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="65544-119">`Microsoft.Compute/virtualMachines/*`sanal makineler ve onun alt kaynak türleri tooall işlemleri verir erişin.</span><span class="sxs-lookup"><span data-stu-id="65544-119">`Microsoft.Compute/virtualMachines/*` grants access tooall operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="65544-120">`Microsoft.Web/sites/restart/Action`verir toorestart Web sitelerine erişim.</span><span class="sxs-lookup"><span data-stu-id="65544-120">`Microsoft.Web/sites/restart/Action` grants access toorestart websites.</span></span>

<span data-ttu-id="65544-121">Kullanım `Get-AzureRmProviderOperation` (PowerShell'de) veya `azure provider operations show` (içinde Azure CLI) toolist işlemleri Azure kaynak sağlayıcıları.</span><span class="sxs-lookup"><span data-stu-id="65544-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) toolist operations of Azure resource providers.</span></span> <span data-ttu-id="65544-122">Bu komutlar tooverify işlemi dizisi geçerli olduğunu ve tooexpand joker işlemi dizeleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65544-122">You may also use these commands tooverify that an operation string is valid, and tooexpand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![PowerShell ekran görüntüsü - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="65544-124">Azure CLI ekran görüntüsü - azure sağlayıcısı işlemleri göster "Microsoft.Compute/virtualMachines/ \* /eylem"</span><span class="sxs-lookup"><span data-stu-id="65544-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="65544-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="65544-125">NotActions</span></span>
<span data-ttu-id="65544-126">Kullanım hello **NotActions** tooallow istediğiniz işlem hello kümesi daha kolay kısıtlı işlemleri hariç tutarak tanımlanmışsa özelliği.</span><span class="sxs-lookup"><span data-stu-id="65544-126">Use hello **NotActions** property if hello set of operations that you wish tooallow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="65544-127">Merhaba özel bir rol tarafından verilen erişim hello çıkarılmasıyla hesaplanır **NotActions** hello işlemlerinden **Eylemler** işlemleri.</span><span class="sxs-lookup"><span data-stu-id="65544-127">hello access granted by a custom role is computed by subtracting hello **NotActions** operations from hello **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="65544-128">Bir kullanıcı bir işlemde dışlar bir rolü atanıp atanmadığını **NotActions**ve erişim veren ikinci bir rolü atanmış aynı işlemi, hello kullanıcı toohello izin tooperform bu işlemi.</span><span class="sxs-lookup"><span data-stu-id="65544-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access toohello same operation, hello user is allowed tooperform that operation.</span></span> <span data-ttu-id="65544-129">**NotActions** reddetme değil kural – belirli işlemleri dışarıda toobe gerektiğinde bir yöntemdir toocreate izin verilen işlem kümesi yalnızca olduğu.</span><span class="sxs-lookup"><span data-stu-id="65544-129">**NotActions** is not a deny rule – it is simply a convenient way toocreate a set of allowed operations when specific operations need toobe excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="65544-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="65544-130">AssignableScopes</span></span>
<span data-ttu-id="65544-131">Merhaba **AssignableScopes** hello özel rol özelliği içinde hangi hello özel rol atama için uygun hello kapsamları (abonelik, kaynak grupları veya kaynakları) belirtir.</span><span class="sxs-lookup"><span data-stu-id="65544-131">hello **AssignableScopes** property of hello custom role specifies hello scopes (subscriptions, resource groups, or resources) within which hello custom role is available for assignment.</span></span> <span data-ttu-id="65544-132">Merhaba özel rol ataması için kullanılabilir yalnızca hello Aboneliklerde yapabileceğiniz veya ve değil dağınıklığı kullanıcının gerektiren kaynak grupları hello kalanı hello abonelik veya kaynak grupları için karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65544-132">You can make hello custom role available for assignment in only hello subscriptions or resource groups that require it, and not clutter user experience for hello rest of hello subscriptions or resource groups.</span></span>

<span data-ttu-id="65544-133">Geçerli atanabilir kapsamların örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="65544-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="65544-134">"/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e", "/ subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624" - hello rol ataması için iki Aboneliklerde kullanılabilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="65544-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes hello role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="65544-135">"/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e" - kullanılabilir hale getirir hello rol ataması tek bir abonelik.</span><span class="sxs-lookup"><span data-stu-id="65544-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes hello role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="65544-136">"/ abonelikleri/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/ağ" - hello rol atamasını yalnızca hello ağ kaynak grubu için kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="65544-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes hello role available for assignment only in hello Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="65544-137">En az bir kullanmalısınız abonelik, kaynak grubu veya kaynak kimliği</span><span class="sxs-lookup"><span data-stu-id="65544-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="65544-138">Özel roller erişim denetimi</span><span class="sxs-lookup"><span data-stu-id="65544-138">Custom roles access control</span></span>
<span data-ttu-id="65544-139">Merhaba **AssignableScopes** hello özel rolünün özelliği de denetimleri kimin görüntüleyin, değiştirin ve hello rolünü silin.</span><span class="sxs-lookup"><span data-stu-id="65544-139">hello **AssignableScopes** property of hello custom role also controls who can view, modify, and delete hello role.</span></span>

* <span data-ttu-id="65544-140">Kimin özel bir rol oluşturabilir miyim?</span><span class="sxs-lookup"><span data-stu-id="65544-140">Who can create a custom role?</span></span>
    <span data-ttu-id="65544-141">Sahiplerinin (ve kullanıcı erişim Yöneticileri) Abonelikleri, kaynak grupları ve kaynakları kullanmak için özel roller bu kapsamları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65544-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="65544-142">Merhaba hello rol oluşturma kullanıcının ihtiyacı toobe mümkün tooperform `Microsoft.Authorization/roleDefinition/write` tüm hello işlemi **AssignableScopes** hello rolünün.</span><span class="sxs-lookup"><span data-stu-id="65544-142">hello user creating hello role needs toobe able tooperform `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of hello role.</span></span>
* <span data-ttu-id="65544-143">Özel bir rol değiştirebilecekleri?</span><span class="sxs-lookup"><span data-stu-id="65544-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="65544-144">Sahiplerinin (ve kullanıcı erişim Yöneticileri) Abonelikleri, kaynak grupları ve kaynakları bu kapsamları özel rollerinde değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65544-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="65544-145">Kullanıcıların gereksinim toobe mümkün tooperform hello `Microsoft.Authorization/roleDefinition/write` tüm hello işlemi **AssignableScopes** özel bir rol.</span><span class="sxs-lookup"><span data-stu-id="65544-145">Users need toobe able tooperform hello `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="65544-146">Kimin özel roller görebilir?</span><span class="sxs-lookup"><span data-stu-id="65544-146">Who can view custom roles?</span></span>
    <span data-ttu-id="65544-147">Azure RBAC yerleşik rolleri tüm rollerin atama için uygun olmayan görüntüleme izin verin.</span><span class="sxs-lookup"><span data-stu-id="65544-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="65544-148">Merhaba gerçekleştirebilirsiniz kullanıcılar `Microsoft.Authorization/roleDefinition/read` bir kapsamda işlemi bu kapsamda atama için kullanılabilir olan hello RBAC rolü görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65544-148">Users who can perform hello `Microsoft.Authorization/roleDefinition/read` operation at a scope can view hello RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="65544-149">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="65544-149">See also</span></span>
* <span data-ttu-id="65544-150">[Rol tabanlı erişim denetimi](role-based-access-control-configure.md): hello Azure portalında RBAC ile çalışmaya başlama.</span><span class="sxs-lookup"><span data-stu-id="65544-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="65544-151">Toomanage nasıl erişim ile bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="65544-151">Learn how toomanage access with:</span></span>
  * [<span data-ttu-id="65544-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="65544-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="65544-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="65544-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="65544-154">REST API</span><span class="sxs-lookup"><span data-stu-id="65544-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="65544-155">[Yerleşik roller](role-based-access-built-in-roles.md): Get RBAC standart gelen hello rolleri hakkında ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="65544-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
