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
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a>Rol tabanlı erişim denetimi hello Azure komut satırı arabirimi ile yönetme
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)


Rol tabanlı erişim denetimi (RBAC) hello Azure portal, Azure Kaynak Yöneticisi API'si toomanage erişim tooyour abonelik ve hassas düzeyinde kaynakları kullanabilirsiniz. Bu özellik ile bazı roller toothem belirli bir kapsamda atayarak Active Directory Kullanıcıları, grupları veya hizmet asıl adı için erişim izni verebilir.

Hello Azure komut satırı arabirimi (CLI) toomanage RBAC kullanmadan önce aşağıdaki önkoşullar hello sahip olmanız gerekir:

* Azure CLI Sürüm 0.8.8 veya sonraki bir sürümü. tooinstall hello en son sürümünü ve ilişkilendirme Azure aboneliğinizle görmek [hello Azure CLI yükleyip](../cli-install-nodejs.md).
* Azure Resource Manager'da Azure CLI. Çok Git[hello Resource Manager ile Azure CLI kullanarak hello](../xplat-cli-azure-resource-manager.md) daha fazla ayrıntı için.

## <a name="list-roles"></a>Liste rolleri
### <a name="list-all-available-roles"></a>Kullanılabilir tüm roller listesinde
kullanılabilir tüm roller toolist kullanın:

        azure role list

Merhaba aşağıdaki örnek hello listesini gösterir *kullanılabilir tüm roller*.

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![RBAC Azure komut satırı - azure rol listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a>Bir rolün liste eylemleri
bir rolün toolist hello eylemlerini kullanın:

    azure role show "<role name>"

Merhaba aşağıdaki örnekte gösterilir hello hello eylemlerini *katkıda bulunan* ve *sanal makine Katılımcısı* rolleri.

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![RBAC Azure komut satırı - azure rol Göster - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a>Liste erişim
### <a name="list-role-assignments-effective-on-a-resource-group"></a>Liste rol atamalarını bir kaynak grubu üzerinde etkin
bir kaynak grubunda kullanımı mevcut toolist hello rol atamaları:

    azure role assignment list --resource-group <resource group name>

Merhaba aşağıdaki örnek hello rol atamalarını hello gösterir *pharma satış projecforcast* grubu.

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![RBAC Azure komut satırı - grubuna göre azure rol ataması listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a>Bir kullanıcı için rol atamalarını listesi
belirli bir kullanıcı için toolist hello rol atamalarını ve tooa kullanıcının gruplar, atanan hello atamalarını kullanın:

    azure role assignment list --signInName <user email>

Merhaba komutu değiştirerek gruplarından devralınan rol atamalarını de görebilirsiniz:

    azure role assignment list --expandPrincipalGroups --signInName <user email>

Merhaba aşağıdaki örnekte gösterilir toohello verilen hello rol atamalarını  *sameert@aaddemo.com*  kullanıcı. Bu, doğrudan toohello kullanıcı atanan rolleri ve gruplardan devralınan rolleri içerir.

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![RBAC Azure komut satırı - kullanıcı tarafından azure rol ataması listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a>Erişim verme
toogrant erişim hello rol tooassign istediğinizi belirledikten sonra kullanın:

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a>Merhaba abonelik kapsamında bir rol toogroup atayın
tooassign rol tooa grubunu hello abonelik kapsamında kullanın:

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

Merhaba aşağıdaki örnek atar hello *okuyucu* rol çok*Christine Koch'ın takım* hello adresindeki *abonelik* kapsam.

![RBAC Azure komut satırı - azure rol ataması oluşturma grupla - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a>Merhaba abonelik kapsamında bir rol tooan uygulama atama
tooassign rol tooan uygulama hello abonelik kapsamında kullanın:

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

Merhaba aşağıdaki örnek verir hello *katkıda bulunan* rol tooan *Azure AD* hello uygulama seçili abonelik.

 ![RBAC Azure komut satırı - azure rol ataması oluşturma uygulama tarafından](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a>Rol tooa kullanıcı hello kaynak grubu kapsamda atama
tooassign bir rol tooa kullanıcı hello Kaynak Grup kapsamı, kullanın:

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

Merhaba aşağıdaki örnek verir hello *sanal makine Katılımcısı* rol çok *samert@aaddemo.com*  hello kullanıcı *Pharma satış ProjectForcast* Kaynak Grup kapsamı.

![RBAC Azure komut satırı - azure rol ataması oluşturma kullanıcı - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a>Bir rol tooa grubu hello kaynak kapsamda atama
tooassign rol tooa grubunu hello kaynak kapsamda kullanın:

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

Merhaba aşağıdaki örnek verir hello *sanal makine Katılımcısı* rol tooan *Azure AD* grubunun bir *alt*.

![RBAC Azure komut satırı - azure rol ataması oluşturma grupla - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a>Erişimi kaldırma
bir rol ataması tooremove kullanın:

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

Merhaba aşağıdaki örnek kaldırır hello *sanal makine Katılımcısı* hello gelen rol atamasını  *sammert@aaddemo.com*  hello kullanıcı *Pharma satış ProjectForcast* kaynak grubu.
Merhaba örneği bu durumda bir grup hello abonelik üzerinde hello rol ataması kaldırır.

![RBAC Azure komut satırı - azure rol ataması delete - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a>Özel bir rol oluşturun
toocreate özel bir rol kullanın:

    azure role create --inputfile <file path>

Merhaba aşağıdaki örnekte oluşturur adlı özel bir rol *sanal makine işleci*. Bu özel rolü erişim tooall okuma işlemlerini verir *Microsoft.Compute*, *Microsoft.Storage*, ve *Microsoft.Network* kaynak sağlayıcıları ve verir erişimi toostart, yeniden başlatma ve sanal makineleri izleme. Bu özel rolü iki Aboneliklerde kullanılabilir. Bu örnek bir JSON dosyası bir giriş olarak kullanır.

![JSON - özel rol tanımı - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![RBAC Azure komut satırı - azure rol oluşturma - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a>Özel bir rol değiştirme
toomodify özel bir rol ilk hello kullan `azure role show` tooretrieve rol tanımı komutu. İkinci olarak, hello istediğiniz değişiklikleri toohello rol tanımı dosyası olun. Son olarak, `azure role set` toosave hello rol tanımını değiştirdi.

    azure role set --inputfile <file path>

Merhaba aşağıdaki örnek, hello *Microsoft.Insights/diagnosticSettings/* işlemi toohello **Eylemler**ve bir Azure aboneliği toohello **AssignableScopes**hello sanal makine işletmeni özel rolü.

![JSON - özel rol tanımını - ekran görüntüsü değiştirme](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![RBAC Azure komut satırı - azure rol set - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a>Bir özel rolü silmeyi
toodelete özel bir rol ilk hello kullan `azure role show` komutu toodetermine hello **kimliği** hello rolünün. Ardından hello kullanın `azure role delete` hello belirterek komutu toodelete hello rol **kimliği**.

Merhaba aşağıdaki örnek kaldırır hello *sanal makine işleci* özel rol.

![RBAC Azure komut satırı - azure rol silme - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a>Liste özel roller
bir kapsamda atama için kullanılabilen toolist hello rolleri kullanmak hello `azure role list` komutu.

komutu aşağıdaki hello hello seçili Abonelikteki atama için kullanılabilen tüm rolleri listeler.

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![RBAC Azure komut satırı - azure rol listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

Aşağıdaki örneğine hello hello *sanal makine işleci* özel rol hello kullanılamaz *Production4* abonelik Bu abonelik hello olmadığından  **AssignableScopes** hello rolünün.

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![RBAC Azure komut satırı - özel roller için azure rol listesi - ekran görüntüsü](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

