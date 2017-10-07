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
# <a name="manage-role-based-access-control-with-azure-powershell"></a>Rol Tabanlı Access Control’ü Azure PowerShell İle Yönetme
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)

Rol tabanlı erişim denetimi (RBAC) hello Azure portalı ve Azure kaynak yönetimi API toomanage erişim tooyour abonelik ayrıntılı kullanabilirsiniz. Bu özellik ile bazı roller toothem belirli bir kapsamda atayarak Active Directory Kullanıcıları, grupları veya hizmet asıl adı için erişim izni verebilir.

PowerShell toomanage RBAC kullanabilmeniz için önce aşağıdaki önkoşullar hello gerekir:

* Azure PowerShell sürüm 0.8.8 veya sonraki bir sürümü. tooinstall hello en son sürümünü ve ilişkilendirme Azure aboneliğinizle görmek [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).
* Azure Resource Manager cmdlet'lerini. Merhaba yüklemek [Azure Resource Manager cmdlet'lerini](/powershell/azure/overview) PowerShell'de.

## <a name="list-roles"></a>Liste rolleri
### <a name="list-all-available-roles"></a>Kullanılabilir tüm roller listesinde
atama ve tooinspect hello işlemleri toowhich bunlar erişim vermek için kullanılabilir olan toolist RBAC rolü kullanmak `Get-AzureRmRoleDefinition`.

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell-Get AzureRmRoleDefinition - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a>Bir rolün liste eylemleri
belirli bir rol için toolist hello eylemlerini kullanmak `Get-AzureRmRoleDefinition <role name>`.

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell-Get AzureRmRoleDefinition belirli bir rol için - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a>Kimlerin erişebileceğini bakın
toolist RBAC erişim atamalarını kullanın `Get-AzureRmRoleAssignment`.

### <a name="list-role-assignments-at-a-specific-scope"></a>Belirli bir kapsamda listesi rol atamaları
Belirtilen abonelik, kaynak grubu ya da kaynak için tüm hello erişim atamalarını görebilirsiniz. Örneğin, bir kaynak grubu kullanmak için tüm hello etkin atamaları hello toosee `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment bir kaynak grubu için - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a>Liste rolleri tooa kullanıcı atanmış.
tooa atanmış olan tüm hello rollerini belirtilen kullanıcı ve toowhich hello kullanıcının ait olduğu, toohello gruplarına atanır hello rolleri toolist kullanım `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment bir kullanıcı için - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a>Klasik Hizmet Yöneticisi ve ortak yönetici rol atamalarını listesi
Merhaba Klasik Abonelik Yöneticisi ve coadministrators, toolist erişim atamalarını kullanın:

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a>Erişim verme
### <a name="search-for-object-ids"></a>Nesne kimlikleri için arama
tooassign bir rol, gereksinim duyduğunuz tooidentify hello nesne (kullanıcı, Grup veya uygulama) ve hello kapsamı.

Merhaba abonelik kimliği bilmiyorsanız, hello bulabilirsiniz **abonelikleri** hello Azure portal dikey penceresinde. hello abonelik kimliği için tooquery nasıl görürüm toolearn [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) konusuna bakın.

bir Azure AD grubunun tooget hello nesne Kimliğini kullanın:

    Get-AzureRmADGroup -SearchString <group name in quotes>

Azure AD hizmet sorumlusu veya uygulama, kullanım için tooget hello nesne kimliği:

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Merhaba abonelik kapsamında bir rol tooan uygulama atama
toogrant erişim tooan uygulama hello abonelik kapsamında kullanın:

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - AzureRmRoleAssignment yeni - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Rol tooa kullanıcı hello kaynak grubu kapsamda atama
toogrant erişim tooa kullanıcı hello Kaynak Grup kapsamı, kullanın:

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - AzureRmRoleAssignment yeni - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Bir rol tooa grubu hello kaynak kapsamda atama
toogrant erişim tooa grubu hello kaynak kapsamda kullanın:

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - AzureRmRoleAssignment yeni - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a>Erişimi kaldırma
Kullanıcılar, gruplar ve uygulamalar, kullanım için tooremove erişim:

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a>Özel bir rol oluşturun
toocreate özel bir rol kullanın hello ```New-AzureRmRoleDefinition``` komutu. PSRoleDefinitionObject veya JSON şablonunu kullanarak hello rolünü yapılandırılması için iki yöntem vardır. 

## <a name="get-actions-for-a-resource-provider"></a>Bir kaynak sağlayıcısı için Eylemler Al
Özel roller sıfırdan oluştururken, önemli tooknow olan tüm olası işlemleri hello kaynak sağlayıcılarından hello.
Kullanım hello ```Get-AzureRMProviderOperation``` tooget bu bilgileri komutu.
Örneğin, toocheck istiyorsanız hello kullanılabilir tüm işlemlerin sanal makine için bu komutu kullanın:

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a>Rolü PSRoleDefinitionObject ile oluşturma
PowerShell toocreate özel bir rol kullandığınızda, baştan başlayın veya hello birini kullanın [yerleşik roller](role-based-access-built-in-roles.md) bir başlangıç noktası olarak. Bu bölümdeki Hello örnek ile yerleşik bir rol başlatır ve daha fazla ayrıcalıklarla özelleştirir. Merhaba öznitelikleri tooadd hello Düzenle *Eylemler*, *notActions*, veya *kapsamları* ve ardından yeni bir rol olarak hello değişiklikleri kaydedin.

Merhaba aşağıdaki örnek başlatır ile Merhaba *sanal makine Katılımcısı* rolü ve kullandığı bu toocreate özel bir rol olarak adlandırılan *sanal makine işleci*. Merhaba yeni rol verir erişim tooall okuma işlemlerini *Microsoft.Compute*, *Microsoft.Storage*, ve *Microsoft.Network* kaynak sağlayıcıları ve verir erişimi toostart, yeniden başlatma ve sanal makineleri izleme. Merhaba özel rol iki Aboneliklerde kullanılabilir.

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

### <a name="create-role-with-json-template"></a>Rol JSON şablon oluştur
Bir JSON şablonu hello kaynak tanımı olarak hello özel rolü için kullanılabilir. Merhaba aşağıdaki örnekte oluşturur okuma erişimi toostorage sağlar ve işlem kaynaklarını, toosupport erişmek ve bu rol eklediği özel bir rol tootwo abonelikleri. Yeni bir dosya oluşturun `C:\CustomRoles\customrole1.json` hello aşağıdaki örneğine sahip. Merhaba kimliği çok ayarlanmalıdır`null` yeni kimliği olarak ilk rol oluşturma sırasında otomatik olarak oluşturulur. 

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
PowerShell komutunu aşağıdaki hello çalıştırmak tooadd hello rol toohello abonelikleri:
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a>Özel bir rol değiştirme
Benzer toocreating özel bir rol, var olan bir özel rol hello PSRoleDefinitionObject ya da bir JSON şablonu kullanarak değiştirebilirsiniz.

### <a name="modify-role-with-psroledefinitionobject"></a>PSRoleDefinitionObject rolüyle Değiştir
toomodify özel bir rol ilk olarak, hello kullanın `Get-AzureRmRoleDefinition` tooretrieve hello rol tanımı komutu. İkinci olarak, toohello rol tanımı hello gerekli değişiklikleri yapın. Son olarak, hello kullan `Set-AzureRmRoleDefinition` komutu toosave hello rol tanımını değiştirdi.

Merhaba aşağıdaki örnek, hello `Microsoft.Insights/diagnosticSettings/*` işlemi toohello *sanal makine işleci* özel rol.

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

Merhaba aşağıdaki örnek, bir Azure aboneliği toohello atanabilir kapsamların hello *sanal makine işleci* özel rol.

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a>JSON şablonunu rolüyle Değiştir
Merhaba önceki JSON şablonunu kullanarak, kolayca var olan bir özel rol tooadd değiştirebilir veya eylemleri kaldırın. Merhaba JSON şablonunu güncelleştirmek ve ağ iletişimi için okuma eylemini hello hello aşağıdaki örnekte gösterildiği gibi ekleyin. Merhaba şablonunda listelenen hello tanımları hello şablonunda tam olarak belirttiğiniz gibi bu hello rol görünür anlamı üst üste uygulanan tooan varolan tanımı olup olmadığı. Ayrıca tooupdate hello Kimliği alanı hello rol hello kimliği gerekir. Bu değer nedir emin değilseniz, hello kullanabilirsiniz `Get-AzureRmRoleDefinition` cmdlet tooget bu bilgileri.

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

tooupdate hello varolan rolü, hello aşağıdaki PowerShell komutunu çalıştırın:
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a>Bir özel rolü silmeyi
toodelete özel bir rol kullanın hello `Remove-AzureRmRoleDefinition` komutu.

Merhaba aşağıdaki örnek kaldırır hello *sanal makine işleci* özel rol.

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a>Liste özel roller
bir kapsamda atama için kullanılabilen toolist hello rolleri kullanmak hello `Get-AzureRmRoleDefinition` komutu.

Aşağıdaki örneğine hello hello seçili Abonelikteki atama için kullanılabilen tüm rolleri listeler.

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell-Get AzureRmRoleDefinition - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

Aşağıdaki örneğine hello hello *sanal makine işleci* özel rol hello kullanılamaz *Production4* abonelik Bu abonelik hello olmadığından  **AssignableScopes** hello rolünün.

![RBAC PowerShell-Get AzureRmRoleDefinition - ekran görüntüsü](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Resource Manager ile Azure PowerShell'i kullanma](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

