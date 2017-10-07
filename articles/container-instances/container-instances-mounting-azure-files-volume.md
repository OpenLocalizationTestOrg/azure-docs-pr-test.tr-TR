---
title: "Azure kapsayıcı örnekleri Azure dosyaları biriminde aaaMounting"
description: "Nasıl toomount Azure dosyaları öğrenin birim toopersist durumuyla Azure kapsayıcı örnekleri"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: d87215e06d5e5af40bfebcad17768ee45ccabbb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a>Azure kapsayıcı örneği ile bir Azure dosya paylaşımı oluşturma

Varsayılan olarak, Azure kapsayıcı durum bilgisiz örnekleridir. Merhaba kapsayıcı kilitlenmesine veya durdurur, durumuna kaybolur. toopersist durumu hello kapsayıcı hello ömür bir dış depodan bir birimi bağlayın. Bu makalede toomount Azure bir dosyayı nasıl paylaşmak Azure kapsayıcı örnekleri ile kullanılmak üzere gösterilmektedir.

## <a name="create-an-azure-file-share"></a>Bir Azure dosya paylaşımı oluşturma

Azure kapsayıcı örnekleri ile Azure dosya paylaşımının kullanmadan önce oluşturmanız gerekir. Bir depolama hesabı toohost hello dosya paylaşımı ve hello kendisini paylaşan betik toocreate aşağıdaki hello çalıştırın. Hello betik rastgele değer toohello taban dizesi ekler ve böylece bu hello depolama hesabı adı genel olarak benzersiz olmalıdır unutmayın.

```azurecli-interactive
# Change these four parameters
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM
ACI_PERS_RESOURCE_GROUP=myResourceGroup
ACI_PERS_LOCATION=eastus
ACI_PERS_SHARE_NAME=acishare

# Create hello storage account with hello parameters
az storage account create -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -l $ACI_PERS_LOCATION --sku Standard_LRS

# Export hello connection string as an environment variable, this is used when creating hello Azure file share
export AZURE_STORAGE_CONNECTION_STRING=`az storage account show-connection-string -n $ACI_PERS_STORAGE_ACCOUNT_NAME -g $ACI_PERS_RESOURCE_GROUP -o tsv`

# Create hello share
az storage share create -n $ACI_PERS_SHARE_NAME
```

## <a name="acquire-storage-account-access-details"></a>Depolama hesabı erişim ayrıntılarını alma

bir Azure dosya paylaşımı bir birim olarak Azure kapsayıcı durumlarda toomount üç değerden gerekir: Merhaba depolama hesabı adı, hello paylaşım adı ve hello depolama erişim tuşu. 

Merhaba betik yukarıdaki kullandıysanız, hello depolama hesabı adı hello sonunda rastgele bir değeri ile oluşturuldu. tooquery hello son dizede (dahil olmak üzere hello rastgele bölümü), hello aşağıdaki komutları kullanın:

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

Merhaba paylaşım adı zaten biliniyor (Bu *acishare* hello komut yukarıdaki), bu nedenle, kalan olan kullanılarak bulunan hello depolama hesabı anahtarı komutu aşağıdaki hello:

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a>Azure anahtar kasası ile depolama hesabı erişim ayrıntılarını depola

Bir Azure anahtar kasası depolamanızı öneririz şekilde tooyour verilere erişmek, depolama hesabı anahtarlarını koruyun. 

Bir anahtar kasası hello Azure CLI ile oluşturun:

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

Merhaba `enabled-for-template-deployment` anahtar dağıtım sırasında gizli anahtar Kasası'ndan Azure Resource Manager toopull sağlar.

Yeni parolayı hello anahtar kasasında olarak Hello depolama hesabı anahtarı depola:

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a>Merhaba birim

Bir kapsayıcıda bir birim olarak Azure dosya paylaşımının takma iki adımlı bir işlemdir. İlk olarak, bir veya daha fazla Merhaba kapsayıcılara hello grubundaki içinde takılı hello birim istediğiniz belirtip hello paylaşımı hello kapsayıcı grubu tanımlayan bir parçası olarak hello ayrıntılarını sağlayın.

bağlama için kullanmak istediğiniz toomake kullanılabilir toodefine hello birimler eklemek bir `volumes` dizi toohello kapsayıcı Grup hello Azure Resource Manager şablonu tanımında, sonra bunları tek tek Merhaba kapsayıcılara hello tanımında başvuru.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "type": "string"
    },
    "storageaccountkey": {
      "type": "securestring"
    }
  },
  "resources":[{
    "name": "hellofiles",
    "type": "Microsoft.ContainerInstance/containerGroups",
    "apiVersion": "2017-08-01-preview",
    "location": "[resourceGroup().location]",
    "properties": {
      "containers": [{
        "name": "hellofiles",
        "properties": {
          "image": "seanmckenna/aci-hellofiles",
          "resources": {
            "requests": {
              "cpu": 1,
              "memoryInGb": 1.5
            }
          },
          "ports": [{
            "port": 80
          }],
          "volumeMounts": [{
            "name": "myvolume",
            "mountPath": "/aci/logs/"
          }]
        }  
      }],
      "osType": "Linux",
      "ipAddress": {
        "type": "Public",
        "ports": [{
          "protocol": "tcp",
          "port": "80"
        }]
      },
      "volumes": [{
        "name": "myvolume",
        "azureFile": {
          "shareName": "acishare",
          "storageAccountName": "[parameters('storageaccountname')]",
          "storageAccountKey": "[parameters('storageaccountkey')]"
        }
      }]
    }
  }]
}
```

Merhaba şablon ayrı Parametreler dosyasında sağlanan parametre olarak hello depolama hesabı adı ve anahtar içerir. toopopulate hello parametreler dosyası üç değerden gerekir: Merhaba depolama hesabı adı, Azure anahtar kasanızı kaynak Kimliğini hello ve hello toostore hello depolama anahtarı kullanılan anahtar kasasına gizli adı. Önceki adımları izlediyseniz, komut dosyası izleyen hello ile bu değerleri alabilirsiniz:

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

Merhaba değerleri hello parametreleri dosyaya ekleyin:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageaccountname": {
      "value": "<my_storage_account_name>"
    },    
   "storageaccountkey": {
      "reference": {
        "keyVault": {
          "id": "<my_keyvault_id>"
        },
        "secretName": "<my_storage_account_key_secret_name>"
      }
    }
  }
}
```

## <a name="deploy-hello-container-and-manage-files"></a>Merhaba kapsayıcıyı dağıtmak ve dosyalarını yönetme

Tanımlanan hello şablonla hello kapsayıcı oluşturun ve hello Azure CLI kullanarak, birim. Merhaba şablon dosyası adlı varsayılarak *azuredeploy.json* ve o hello parametreler dosyası adlı *azuredeploy.parameters.json*, hello komut satırı sonra:

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

Merhaba kapsayıcı başlatıldığında sonra hello dağıtılan hello basit web uygulaması kullanarak **aci/seanmckenna-hellofiles** görüntüsü toohello yönetmek belirttiğiniz hello bağlama yolundaki hello Azure dosya paylaşımında dosyalar. Hello aşağıdaki aracılığıyla hello web uygulaması için başlangıç IP adresi alın:

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

Hello gibi bir araç kullanabilirsiniz [Microsoft Azure Storage Gezgini](http://storageexplorer.com) tooretrieve ve hello dosya writen toohello dosya paylaşımı inceleyin.

>[!NOTE]
> Parametre dosyaları, Azure Resource Manager şablonları kullanarak ve hello Azure CLI ile dağıtma hakkında daha fazla toolearn bkz [Resource Manager şablonları ve Azure CLI kaynaklarla dağıtmak](../azure-resource-manager/resource-group-template-deploy-cli.md).

## <a name="next-steps"></a>Sonraki adımlar

- Hello Azure kapsayıcı örneği kullanarak, ilk kapsayıcıyı dağıtmak [hızlı başlangıç](container-instances-quickstart.md)
- Merhaba hakkında bilgi edinin [Azure kapsayıcı örnekleri ile kapsayıcı orchestrators arasındaki ilişki](container-instances-orchestrator-relationship.md)
