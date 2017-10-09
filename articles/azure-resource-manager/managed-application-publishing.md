---
title: "aaaCreate ve Azure hizmet Kataloğu yönetilen uygulama yayımlama | Microsoft Docs"
description: "Kuruluşunuzun bir üyesi için hedeflenen uygulama toocreate Azure nasıl yönetileceğini gösterir."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 31f2f9e3b50f57dae7f4dcf2edefa7366bfff25c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-managed-application-for-internal-consumption"></a>Dahili tüketim için yönetilen bir uygulama yayımlama

Oluşturma ve Azure yayımlama [yönetilen uygulamaları](managed-application-overview.md) kuruluşunuzun üyeleri için yöneliktir. Örneğin, bir BT departmanının kuruluş standartlarıyla uyumluluğu sağlamak yönetilen uygulamaları yayımlayabilirsiniz. Bu yönetilen uygulamaların hello hizmet Kataloğu, hello Azure Market kullanılabilir.

toopublish bir yönetilen uygulama hello hizmet kataloğu için aşağıdakileri yapmalısınız:

* Merhaba üç gerekli şablon dosyalarını içeren bir .zip paketi oluşturun.
* Hangi kullanıcı, Grup veya uygulama hello kullanıcının abonelik toohello kaynak grubunda erişimi gerektirir karar verin.
* Toohello .zip paketi işaret ve hello kimliği için erişim isteğinde hello yönetilen uygulama tanımı oluşturun.

## <a name="create-a-managed-application-package"></a>Bir yönetilen uygulama paketi oluşturma

Merhaba ilk adımı toocreate hello üç gerekli şablon dosyalarını oluşturur. Bir .zip dosyasına paket üç tüm dosyaları ve tooan erişilebilecek bir konuma, bir depolama hesabı gibi yükleyin. Uygulama tanımı oluşturma hello yönetilen bir bağlantı toothis .zip dosyasını geçirin.

* **applianceMainTemplate.json**: Bu dosya hello Azure tanımlar uygulaması yönetilen hello bir parçası olarak sağlanan kaynakları. Merhaba şablon normal bir Resource Manager şablonu farklı değildir. Örneğin, yönetilen bir uygulama üzerinden depolama hesabı toocreate applianceMainTemplate.json içerir:

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[concat(parameters('storageAccountNamePrefix'), uniqueString(resourceGroup().id))]",
            "apiVersion": "2016-01-01",
            "location": "[resourceGroup().location]",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "Storage",
            "properties": {}
        }
    ],
    "outputs": {}
  }
  ```

* **mainTemplate.json**: hello oluşturma uygulama yönetildiğinde bu şablonu kullanıcılara dağıtma. Microsoft.Solutions/appliances kaynak türü hello yönetilen uygulama kaynağı tanımlar. Bu dosya applianceMainTemplate.json hello kaynakları için gereksinim duyduğunuz tüm hello parametrelerini içerir.

  Bu şablonda iki önemli özellikleri ayarlayın. İlk olarak, hello **applianceDefinitionId** hello kimliği hello yönetilen uygulama tanımının bir özelliktir. Bu konunun ilerleyen bölümlerinde hello tanımı oluşturun. Bu değer ayarlandığında, hangi abonelik ve kaynak grubu toouse depolamak için yönetilen uygulama tanımları hello karar vermeniz gerekir. Ve hello tanımı için bir ad üzerinde karar vermeniz gerekir. Merhaba kimliği hello biçimdedir:

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  İkinci olarak, hello **managedResourceGroupId** özelliği hello Azure kaynaklarının oluşturulduğu hello kaynak grubunun hello kimliği değil. Bu kaynak grubu adı için bir değer atamak veya bir ad sağlayın hello kullanıcının izin verin. Merhaba kimliğinin Hello biçimdedir:

  `/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.

  Aşağıdaki örnek hello mainTemplate.json dosyasını gösterir. Dağıtılan hello kaynakları için bir kaynak grubu belirtir. Merhaba tanımı kimliği olan bir tanımı adlı kümesi toouse **storageApp** bir kaynak grubunda adlı **managedApplicationGroup**. Bu değerleri toouse farklı adlarını değiştirebilirsiniz. Merhaba tanımı kimliği kendi abonelik kimliği sağlayın

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountNamePrefix": {
            "type": "string"
        }
    },
    "variables": {
        "managedRGId": "[concat(resourceGroup().id,'-application-resources')]",
        "managedAppName": "[concat('managedStorage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
        {
            "type": "Microsoft.Solutions/appliances",
            "name": "[variables('managedAppName')]",
            "apiVersion": "2016-09-01-preview",
            "location": "[resourceGroup().location]",
            "kind": "ServiceCatalog",
            "properties": {
                "managedResourceGroupId": "[variables('managedRGId')]",
                "applianceDefinitionId": "/subscriptions/<subscription-id>/resourceGroups/managedApplicationGroup/providers/Microsoft.Solutions/applianceDefinitions/storageApp",
                "parameters": {
                    "storageAccountNamePrefix": {
                        "value": "[parameters('storageAccountNamePrefix')]"
                    }
                }
            }
        }
    ]
  }
  ```

* **applianceCreateUiDefinition.json**: yönetilen uygulamayı oluşturan kullanıcıların hello hello Azure portal bu dosya toogenerate hello kullanıcı arabirimini kullanır. Tanımladığınız nasıl kullanıcılar her parametre için değer girin. Bir açılan listesinden, metin kutusuna, parola kutusu ve diğer araçları giriş gibi seçeneklerini kullanabilirsiniz. toocreate UI tanım dosyası yönetilen bir uygulama için nasıl görürüm toolearn [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).

  Merhaba aşağıdaki örnek, kullanıcıların toospecify hello depolama hesabı adı öneki metin kutusu aracılığıyla sağlayan bir applianceCreateUiDefinition.json dosyayı gösterir.

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
    "handler": "Microsoft.Compute.MultiVm",
    "version": "0.1.2-preview",
    "parameters": {
        "basics": [
            {
                "name": "storageAccounts",
                "type": "Microsoft.Common.TextBox",
                "label": "Storage account name prefix",
                "defaultValue": "storage",
                "toolTip": "Provide a value that is used for hello prefix of your storage account. Limit too11 characters.",
                "constraints": {
                    "required": true,
                    "regex": "^[a-z0-9A-Z]{1,11}$",
                    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-11 characters long."
                },
                "visible": true
            }
        ],
        "steps": [],
        "outputs": {
            "storageAccountNamePrefix": "[basics('storageAccounts')]"
        }
    }
  }
  ```

Tüm gerekli hello dosyaları hazır olduktan sonra bunları bir .zip dosyası olarak paketleyin. Merhaba üç dosyalar hello kök düzeyinde hello .zip dosyası olmalıdır. Bir klasöre yerleştirin, hello oluşturma dosyalar yoksa hello gereken durumlar uygulama tanımı yönetildiğinde bir hata alırsınız. Burada tüketilebilir hello paket tooan erişilebilir konumdaki karşıya yükleyin. Bu makalenin sonraki bölümlerinde Hello hello .zip dosyası bir genel olarak erişilebilir depolama blob kapsayıcısında var. varsayar.

## <a name="create-an-azure-active-directory-user-group-or-application"></a>Bir Azure Active Directory kullanıcı grubu veya uygulama oluşturma

Merhaba ikinci adım hello kaynakları hello müşteri adına yönetmek için tooselect bir kullanıcı grubu veya uygulamadır. Bu kullanıcı grubu veya uygulama izinleri atanan hello yönetilen kaynak grubu according toohello rolü vardır. Merhaba rol sahibi veya katkıda gibi herhangi bir yerleşik rol tabanlı erişim denetimi (RBAC) rolüne olabilir. Tek bir kullanıcı izni toomanage hello kaynakları verebilirsiniz, ancak genellikle bu izni tooa kullanıcı grubuna atayın. Yeni bir Active Directory kullanıcı grubu toocreate bkz [bir grup oluşturun ve Azure Active Directory'de üye ekleme](../active-directory/active-directory-groups-create-azure-portal.md).

Merhaba kaynakları yönetmek için hello kullanıcı grubu toouse hello nesne kimliği gerekir. Aşağıdaki örnek hello nasıl tooget hello hello grubun görünen ad nesne kimliği gösterir:

```azurecli-interactive
az ad group show --group exampleGroupName
```

Merhaba örnek komut, çıktı aşağıdaki hello döndürür:

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

tooretrieve yalnızca hello nesne kimliği, kullanın:

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a>Merhaba rol tanımı kimliği alma

Ardından, hello RBAC yerleşik rol toogrant erişim toohello kullanıcı, kullanıcı grubu veya uygulama istediğiniz hello rol tanımı kimliği gerekir. Genellikle, hello sahibi veya katkıda bulunan veya okuyucu rolüne kullanın. komutu aşağıdaki hello nasıl tooget hello hello sahibi rol için rol tanımı kimliği gösterir:


```azurecli-interactive
az role definition list --name owner
```

Bu komut çıktı aşağıdaki hello döndürür:

```azurecli
{
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/roleDefinitions/8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "name": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
    "properties": {
      "assignableScopes": [
        "/"
      ],
      "description": "Lets you manage everything, including access tooresources.",
      "permissions": [
        {
          "actions": [
            "*"
         ],
         "notActions": []
        }
      ],
      "roleName": "Owner",
      "type": "BuiltInRole"
    },
    "type": "Microsoft.Authorization/roleDefinitions"
}
```

Merhaba değerini örnek önceki hello hello "name" özelliği gerekir. Bu özellik yalnızca ile alabilirsiniz:

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a>Yönetilen hello uygulama tanımı oluşturun

Zaten bir kaynak grubu, yönetilen uygulama tanımını depolamak için yoksa, şimdi oluşturun:

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

Şimdi, yönetilen hello uygulama tanımı kaynağı oluşturun.

```azurecli-interactive
az managedapp definition create \
  --name storageApp \
  --location "westcentralus" \
  --resource-group managedApplicationGroup \
  --lock-level ReadOnly \
  --display-name myteststorageapp \
  --description storageapp \
  --authorizations "$groupid:$roleid" \
  --package-file-uri <uri-path-to-zip-file>
```

Örnek önceki hello kullanılan hello Parametreler şunlardır:

* **kaynak grubu**: hello hello uygulama tanımı yönetildiği hello kaynak grubunun adını oluşturulur.
* **Kilit düzeyi**: kilit hello türünü hello yönetilen kaynak grubuna yerleştirilir. Merhaba müşteri bu kaynak grubu üzerindeki istenmeyen işlemlerini gerçekleştirmesini engeller. Şu anda salt okunur hello kilit düzeyi yalnızca desteklenen olur. Salt okunur belirtildiğinde, hello müşteri hello kaynakları hello yönetilen kaynak grubunda mevcut yalnızca okuyabilir.
* **yetkilerini**: kullanılan toogrant izin toohello yönetilen kaynak grubu olan hello sorumlu kimliği ve hello rol tanımı kimliği açıklar. Merhaba biçiminde belirtilen `<principalId>:<roleDefinitionId>`. Bu özellik için birden çok değer de belirtilebilir. Birden çok değer gerekirse hello biçiminde belirtilmelidir `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`. Birden çok değeri boşlukla ayrılır.
* **Paket dosyası URI**: Merhaba hello yönetilen uygulamayı bir Azure Storage blobu olabilir hello şablon dosyalarını içeren bir paket konumu.

## <a name="next-steps"></a>Sonraki adımlar

* Bir giriş toomanaged uygulamalar için bkz [yönetilen uygulama genel bakış](managed-application-overview.md).
* Merhaba dosyaları örnekleri için bkz: [yönetilen uygulama örnekleri](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).
* Hizmet Kataloğu yönetilen uygulama kullanma hakkında daha fazla bilgi için bkz: [bir hizmet Kataloğu yönetilen uygulama tüketen](managed-application-consumption.md).
* Yönetilen uygulamaların toohello Azure Marketi'nde yayımlama hakkında daha fazla bilgi için bkz: [Azure hello Market uygulamalarda yönetilen](managed-application-author-marketplace.md).
* Merhaba Market yönetilen bir uygulamadan kullanma hakkında daha fazla bilgi için bkz: [tüketen Azure hello Market uygulamalarda yönetilen](managed-application-consume-marketplace.md).
* toocreate UI tanım dosyası yönetilen bir uygulama için nasıl görürüm toolearn [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).
