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
# <a name="manage-role-based-access-control-with-hello-rest-api"></a>Rol tabanlı erişim denetimi hello REST API ile yönetme
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)

Rol tabanlı erişim denetimi (RBAC) hello Azure portal'ın ve Azure Kaynak Yöneticisi API'si erişim tooyour abonelik ve ayrıntılı bir düzeyde kaynakları yönetmenize yardımcı olur. Bu özellik ile bazı roller toothem belirli bir kapsamda atayarak Active Directory Kullanıcıları, grupları veya hizmet asıl adı için erişim izni verebilir.

## <a name="list-all-role-assignments"></a>Tüm rol atamalarını listesi
Listeleri tüm hello rol atamalarını belirtilen hello adresindeki kapsam ve subscopes.

toolist rol atamaları gerekir erişiminiz çok`Microsoft.Authorization/roleAssignments/read` hello kapsamda işlemi. Tüm hello yerleşik roller erişim toothis işlemi verilir. Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).

### <a name="request"></a>İstek
Kullanım hello **almak** URI aşağıdaki hello yöntemiyle:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:

1. Değiştir *{kapsamı}* kendisi için istediğiniz toolist hello rol atamalarını hello kapsama sahip. Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:

   * Abonelik: /subscriptions/ {subscrıptıon-ID}  
   * Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1  
   * Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Değiştir *{api-version}* 2015-07-01 ile.
3. Değiştir *{filtre}* hello koşuluyla tooapply toofilter hello rol ataması listesi istiyor:

   * Yalnızca hello listesi rol atamalarını hello rol atamaları subscopes olarak dahil edilmez kapsamı, belirtilen:`atScope()`    
   * Belirli bir kullanıcı, Grup veya uygulama için rol atamalarını listesi:`principalId%20eq%20'{objectId of user, group, or service principal}'`  
   * Liste olanları gruplarından devralınan dahil olmak üzere belirli bir kullanıcı için rol atamalarını |`assignedTo('{objectId of user}')`

### <a name="response"></a>Yanıt
Durum kodu: 200

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

## <a name="get-information-about-a-role-assignment"></a>Bir rol ataması hakkında bilgi alın
Merhaba rol ataması tanımlayıcısı tarafından belirtilen bir tek bir rol ataması hakkında bilgi alır.

bir rol ataması hakkında bilgi tooget, gereken erişiminiz çok`Microsoft.Authorization/roleAssignments/read` işlemi. Tüm hello yerleşik roller erişim toothis işlemi verilir. Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).

### <a name="request"></a>İstek
Kullanım hello **almak** URI aşağıdaki hello yöntemiyle:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:

1. Değiştir *{kapsamı}* kendisi için istediğiniz toolist hello rol atamalarını hello kapsama sahip. Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:

   * Abonelik: /subscriptions/ {subscrıptıon-ID}  
   * Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1  
   * Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Değiştir *{rol atama kimliği}* , hello rol atamasının hello GUID tanımlayıcısı.
3. Değiştir *{api-version}* 2015-07-01 ile.

### <a name="response"></a>Yanıt
Durum kodu: 200

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

## <a name="create-a-role-assignment"></a>Bir rol ataması oluşturma
Bir rol oluşturmak hello atamasının Belirtilen kapsam hello asıl izni veriliyor hello belirtilen rol belirtilen için.

bir rol ataması toocreate gerekir erişiminiz çok`Microsoft.Authorization/roleAssignments/write` işlemi. Merhaba yerleşik roller, yalnızca *sahibi* ve *kullanıcı erişimi Yöneticisi* erişim toothis işlemi verilir. Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).

### <a name="request"></a>İstek
Kullanım hello **PUT** URI aşağıdaki hello yöntemiyle:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:

1. Değiştir *{kapsamı}* aktarılma istediğiniz toocreate hello rol atamalarını hello kapsama sahip. Bir üst kapsamda bir rol ataması oluşturduğunuzda, tüm alt kapsamlar hello devralır aynı rol ataması. Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:

   * Abonelik: /subscriptions/ {subscrıptıon-ID}  
   * Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1   
   * Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Değiştir *{rol atama kimliği}* yeni bir GUID ile haline geldikten hello yeni rol ataması hello GUID tanımlayıcısı.
3. Değiştir *{api-version}* 2015-07-01 ile.

Merhaba istek gövdesi için biçim aşağıdaki hello hello değerleri sağlayın:

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| Öğe adı | Gerekli | Tür | Açıklama |
| --- | --- | --- | --- |
| Roledefinitionıd |Evet |Dize |Merhaba rol Hello tanımlayıcısı. Merhaba tanımlayıcısının Hello biçimdedir:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}` |
| Principalıd |Evet |Dize |hello Azure AD sorumlusu (kullanıcı, Grup veya hizmet sorumlusu) objectID toowhich hello rolü atanır. |

### <a name="response"></a>Yanıt
Durum kodu: 201

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

## <a name="delete-a-role-assignment"></a>Bir rol atamasını silin
Delete hello rol atamasının kapsamı belirtilmiş.

bir rol ataması toodelete, erişim toohello olmalıdır `Microsoft.Authorization/roleAssignments/delete` işlemi. Merhaba yerleşik roller, yalnızca *sahibi* ve *kullanıcı erişimi Yöneticisi* erişim toothis işlemi verilir. Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).

### <a name="request"></a>İstek
Kullanım hello **silmek** URI aşağıdaki hello yöntemiyle:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:

1. Değiştir *{kapsamı}* aktarılma istediğiniz toocreate hello rol atamalarını hello kapsama sahip. Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:

   * Abonelik: /subscriptions/ {subscrıptıon-ID}  
   * Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1  
   * Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Değiştir *{rol atama kimliği}* hello rol ataması kimliği GUID.
3. Değiştir *{api-version}* 2015-07-01 ile.

### <a name="response"></a>Yanıt
Durum kodu: 200

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

## <a name="list-all-roles"></a>Tüm rolleri listeler
Belirtilen hello atamasının kullanılabilir tüm hello rollerini listeler kapsamı.

toolist rolleri gerekir erişiminiz çok`Microsoft.Authorization/roleDefinitions/read` hello kapsamda işlemi. Tüm hello yerleşik roller erişim toothis işlemi verilir. Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).

### <a name="request"></a>İstek
Kullanım hello **almak** URI aşağıdaki hello yöntemiyle:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:

1. Değiştir *{kapsamı}* kendisi için istediğiniz toolist hello rolleri hello kapsama sahip. Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:

   * Abonelik: /subscriptions/ {subscrıptıon-ID}  
   * Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1  
   * Kaynak /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Değiştir *{api-version}* 2015-07-01 ile.
3. Değiştir *{filtre}* hello koşuluyla tooapply toofilter hello rollerin listesini istiyor:

   * Liste rolleri hello atamasının kullanılabilir kapsamı ve tüm alt kapsamlarından belirtilen:`atScopeAndBelow()`
   * Tam ekran adını kullanarak bir rolü arayın: `roleName%20eq%20'{role-display-name}'`. Merhaba URL kodlanmış form hello rolünün hello tam görünen adını kullanın. Örneğin,`$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |

### <a name="response"></a>Yanıt
Durum kodu: 200

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

## <a name="get-information-about-a-role"></a>Bir rolü hakkında bilgi edinin
Merhaba rol tanımı tanımlayıcısı tarafından belirtilen tek bir rol bilgilerini alır. görünen adını kullanarak tek bir rol tooget bilgilere bakın [tüm rolleri listesinde](role-based-access-control-manage-access-rest.md#list-all-roles).

bir rolü hakkında tooget bilgi gerekir erişiminiz çok`Microsoft.Authorization/roleDefinitions/read` işlemi. Tüm hello yerleşik roller erişim toothis işlemi verilir. Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).

### <a name="request"></a>İstek
Kullanım hello **almak** URI aşağıdaki hello yöntemiyle:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:

1. Değiştir *{kapsamı}* kendisi için istediğiniz toolist hello rol atamalarını hello kapsama sahip. Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:

   * Abonelik: /subscriptions/ {subscrıptıon-ID}  
   * Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1  
   * Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Değiştir *{rol tanımı kimliği}* , hello rol tanımı hello GUID tanımlayıcısı.
3. Değiştir *{api-version}* 2015-07-01 ile.

### <a name="response"></a>Yanıt
Durum kodu: 200

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

## <a name="create-a-custom-role"></a>Özel bir rol oluşturun
Özel bir rol oluşturun.

toocreate özel bir rol, gereken erişiminiz çok`Microsoft.Authorization/roleDefinitions/write` tüm hello işlemi `AssignableScopes`. Merhaba yerleşik roller, yalnızca *sahibi* ve *kullanıcı erişimi Yöneticisi* erişim toothis işlemi verilir. Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).

### <a name="request"></a>İstek
Kullanım hello **PUT** URI aşağıdaki hello yöntemiyle:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:

1. Değiştir *{kapsamı}* hello ile ilk *AssignableScope* hello özel rolü. Örnek hello nasıl toospecify hello kapsam farklı düzeylerde gösterir.

   * Abonelik: /subscriptions/ {subscrıptıon-ID}  
   * Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1  
   * Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Değiştir *{rol tanımı kimliği}* yeni bir GUID ile haline geldikten hello yeni özel rol hello GUID tanımlayıcısı.
3. Değiştir *{api-version}* 2015-07-01 ile.

Merhaba istek gövdesi için biçim aşağıdaki hello hello değerleri sağlayın:

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

| Öğe adı | Gerekli | Tür | Açıklama |
| --- | --- | --- | --- |
| ad |Evet |Dize |Merhaba özel rol GUID tanımlayıcısı. |
| properties.roleName |Evet |Dize |Merhaba özel rol adını görüntüler. En büyük boyutu 128 karakter. |
| Properties.Description |Hayır |Dize |Merhaba özel rol tanımı. En büyük boyutu 1024 karakter. |
| Properties.Type |Evet |Dize |Çok Ayarla "CustomRole." |
| Properties.Permissions.Actions |Evet |String] |Bir dizi eylem hello özel rol tarafından verilen belirten hello işlemleri dizeleri. |
| properties.permissions.notActions |Hayır |String] |Hello işlemleri tooexclude hello özel rol tarafından verilen hello Operations belirten bir eylem dizeler dizisi. |
| properties.assignableScopes |Evet |String] |Hangi hello özel rol kullanılabilir kapsamları dizisi. |

### <a name="response"></a>Yanıt
Durum kodu: 201

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

## <a name="update-a-custom-role"></a>Özel bir rol güncelleştirme
Özel bir rol değiştirin.

toomodify özel bir rol, gereken erişiminiz çok`Microsoft.Authorization/roleDefinitions/write` tüm hello işlemi `AssignableScopes`. Merhaba yerleşik roller, yalnızca *sahibi* ve *kullanıcı erişimi Yöneticisi* erişim toothis işlemi verilir. Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).

### <a name="request"></a>İstek
Kullanım hello **PUT** URI aşağıdaki hello yöntemiyle:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:

1. Değiştir *{kapsamı}* hello ile ilk *AssignableScope* hello özel rolü. Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:

   * Abonelik: /subscriptions/ {subscrıptıon-ID}  
   * Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1  
   * Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Değiştir *{rol tanımı kimliği}* ile Merhaba özel rol hello GUID tanımlayıcısı.
3. Değiştir *{api-version}* 2015-07-01 ile.

Merhaba istek gövdesi için biçim aşağıdaki hello hello değerleri sağlayın:

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

| Öğe adı | Gerekli | Tür | Açıklama |
| --- | --- | --- | --- |
| ad |Evet |Dize |Merhaba özel rol GUID tanımlayıcısı. |
| properties.roleName |Evet |Dize |Merhaba güncelleştirilmiş özel rol adını görüntüler. |
| Properties.Description |Hayır |Dize |Merhaba açıklaması özel rol güncelleştirildi. |
| Properties.Type |Evet |Dize |Çok Ayarla "CustomRole." |
| Properties.Permissions.Actions |Evet |String] |Merhaba işlemleri toowhich hello belirtme eylem dizisini özel rol verir erişim güncelleştirildi. |
| properties.permissions.notActions |Hayır |String] |Bir dizi eylem hangi hello özel rol verir güncelleştirilmiş hello Operations belirten hello işlemleri tooexclude dizeleri. |
| properties.assignableScopes |Evet |String] |Hangi hello güncelleştirilmiş özel rol kullanılabilir kapsamları dizisi. |

### <a name="response"></a>Yanıt
Durum kodu: 201

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

## <a name="delete-a-custom-role"></a>Bir özel rolü silmeyi
Özel bir rol silin.

toodelete özel bir rol, gereken erişiminiz çok`Microsoft.Authorization/roleDefinitions/delete` tüm hello işlemi `AssignableScopes`. Merhaba yerleşik roller, yalnızca *sahibi* ve *kullanıcı erişimi Yöneticisi* erişim toothis işlemi verilir. Rol atamaları ve Azure kaynakları için erişimi yönetme hakkında daha fazla bilgi için bkz: [Azure rol tabanlı erişim denetimi](role-based-access-control-configure.md).

### <a name="request"></a>İstek
Kullanım hello **silmek** URI aşağıdaki hello yöntemiyle:

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

Merhaba URI değişimler toocustomize aşağıdaki hello isteğiniz olun:

1. Değiştir *{kapsamı}* toodelete hello rol tanımı istediğiniz hello kapsama sahip. Örnek hello nasıl toospecify hello farklı düzeylerde kapsam göster:

   * Abonelik: /subscriptions/ {subscrıptıon-ID}  
   * Kaynak grubu: /subscriptions/ {subscrıptıon-ID} / resourceGroups/myresourcegroup1  
   * Kaynak: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1  
2. Değiştir *{rol tanımı kimliği}* hello GUID rol tanımı kimliği hello özel rol.
3. Değiştir *{api-version}* 2015-07-01 ile.

### <a name="response"></a>Yanıt
Durum kodu: 200

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

## <a name="next-steps"></a>Sonraki adımlar

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
