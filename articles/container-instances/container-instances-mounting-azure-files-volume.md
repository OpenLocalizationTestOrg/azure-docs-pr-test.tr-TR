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
# <a name="mounting-an-azure-file-share-with-azure-container-instances"></a><span data-ttu-id="b91e0-103">Azure kapsayıcı örneği ile bir Azure dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b91e0-103">Mounting an Azure file share with Azure Container Instances</span></span>

<span data-ttu-id="b91e0-104">Varsayılan olarak, Azure kapsayıcı durum bilgisiz örnekleridir.</span><span class="sxs-lookup"><span data-stu-id="b91e0-104">By default, Azure Container Instances are stateless.</span></span> <span data-ttu-id="b91e0-105">Merhaba kapsayıcı kilitlenmesine veya durdurur, durumuna kaybolur.</span><span class="sxs-lookup"><span data-stu-id="b91e0-105">If hello container crashes or stops, all of its state is lost.</span></span> <span data-ttu-id="b91e0-106">toopersist durumu hello kapsayıcı hello ömür bir dış depodan bir birimi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b91e0-106">toopersist state beyond hello lifetime of hello container, you must mount a volume from an external store.</span></span> <span data-ttu-id="b91e0-107">Bu makalede toomount Azure bir dosyayı nasıl paylaşmak Azure kapsayıcı örnekleri ile kullanılmak üzere gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b91e0-107">This article shows how toomount an Azure file share for use with Azure Container Instances.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="b91e0-108">Bir Azure dosya paylaşımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b91e0-108">Create an Azure file share</span></span>

<span data-ttu-id="b91e0-109">Azure kapsayıcı örnekleri ile Azure dosya paylaşımının kullanmadan önce oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b91e0-109">Before using an Azure file share with Azure Container Instances, you must create it.</span></span> <span data-ttu-id="b91e0-110">Bir depolama hesabı toohost hello dosya paylaşımı ve hello kendisini paylaşan betik toocreate aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b91e0-110">Run hello following script toocreate a storage account toohost hello file share and hello share itself.</span></span> <span data-ttu-id="b91e0-111">Hello betik rastgele değer toohello taban dizesi ekler ve böylece bu hello depolama hesabı adı genel olarak benzersiz olmalıdır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="b91e0-111">Note that hello storage account name must be globally unique, so hello script adds a random value toohello base string.</span></span>

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

## <a name="acquire-storage-account-access-details"></a><span data-ttu-id="b91e0-112">Depolama hesabı erişim ayrıntılarını alma</span><span class="sxs-lookup"><span data-stu-id="b91e0-112">Acquire storage account access details</span></span>

<span data-ttu-id="b91e0-113">bir Azure dosya paylaşımı bir birim olarak Azure kapsayıcı durumlarda toomount üç değerden gerekir: Merhaba depolama hesabı adı, hello paylaşım adı ve hello depolama erişim tuşu.</span><span class="sxs-lookup"><span data-stu-id="b91e0-113">toomount an Azure file share as a volume in Azure Container Instances, you need three values: hello storage account name, hello share name, and hello storage access key.</span></span> 

<span data-ttu-id="b91e0-114">Merhaba betik yukarıdaki kullandıysanız, hello depolama hesabı adı hello sonunda rastgele bir değeri ile oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="b91e0-114">If you used hello script above, hello storage account name was created with a random value at hello end.</span></span> <span data-ttu-id="b91e0-115">tooquery hello son dizede (dahil olmak üzere hello rastgele bölümü), hello aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="b91e0-115">tooquery hello final string (including hello random portion), use hello following commands:</span></span>

```azurecli-interactive
STORAGE_ACCOUNT=$(az storage account list --resource-group myResourceGroup --query "[?contains(name,'mystorageaccount')].[name]" -o tsv)
echo $STORAGE_ACCOUNT
```

<span data-ttu-id="b91e0-116">Merhaba paylaşım adı zaten biliniyor (Bu *acishare* hello komut yukarıdaki), bu nedenle, kalan olan kullanılarak bulunan hello depolama hesabı anahtarı komutu aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="b91e0-116">hello share name is already known (it is *acishare* in hello script above), so all that remains is hello storage account key, which can be found using hello following command:</span></span>

```azurecli-interactive
$STORAGE_KEY=$(az storage account keys list --resource-group myResourceGroup --account-name $STORAGE_ACCOUNT --query "[0].value" -o tsv)
echo $STORAGE_KEY
```

## <a name="store-storage-account-access-details-with-azure-key-vault"></a><span data-ttu-id="b91e0-117">Azure anahtar kasası ile depolama hesabı erişim ayrıntılarını depola</span><span class="sxs-lookup"><span data-stu-id="b91e0-117">Store storage account access details with Azure key vault</span></span>

<span data-ttu-id="b91e0-118">Bir Azure anahtar kasası depolamanızı öneririz şekilde tooyour verilere erişmek, depolama hesabı anahtarlarını koruyun.</span><span class="sxs-lookup"><span data-stu-id="b91e0-118">Storage account keys protect access tooyour data, so we recommend storing them in an Azure key vault.</span></span> 

<span data-ttu-id="b91e0-119">Bir anahtar kasası hello Azure CLI ile oluşturun:</span><span class="sxs-lookup"><span data-stu-id="b91e0-119">Create a key vault with hello Azure CLI:</span></span>

```azurecli-interactive
KEYVAULT_NAME=aci-keyvault
az keyvault create -n $KEYVAULT_NAME --enabled-for-template-deployment -g myResourceGroup
```

<span data-ttu-id="b91e0-120">Merhaba `enabled-for-template-deployment` anahtar dağıtım sırasında gizli anahtar Kasası'ndan Azure Resource Manager toopull sağlar.</span><span class="sxs-lookup"><span data-stu-id="b91e0-120">hello `enabled-for-template-deployment` switch allows Azure Resource Manager toopull secrets from your key vault at deployment time.</span></span>

<span data-ttu-id="b91e0-121">Yeni parolayı hello anahtar kasasında olarak Hello depolama hesabı anahtarı depola:</span><span class="sxs-lookup"><span data-stu-id="b91e0-121">Store hello storage account key as a new secret in hello key vault:</span></span>

```azurecli-interactive
KEYVAULT_SECRET_NAME=azurefilesstoragekey
az keyvault secret set --vault-name $KEYVAULT_NAME --name $KEYVAULT_SECRET_NAME --value $STORAGE_KEY
```

## <a name="mount-hello-volume"></a><span data-ttu-id="b91e0-122">Merhaba birim</span><span class="sxs-lookup"><span data-stu-id="b91e0-122">Mount hello volume</span></span>

<span data-ttu-id="b91e0-123">Bir kapsayıcıda bir birim olarak Azure dosya paylaşımının takma iki adımlı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="b91e0-123">Mounting an Azure file share as a volume in a container is a two-step process.</span></span> <span data-ttu-id="b91e0-124">İlk olarak, bir veya daha fazla Merhaba kapsayıcılara hello grubundaki içinde takılı hello birim istediğiniz belirtip hello paylaşımı hello kapsayıcı grubu tanımlayan bir parçası olarak hello ayrıntılarını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="b91e0-124">First, you provide hello details of hello share as part of defining hello container group, then you specify how you want hello volume mounted within one or more of hello containers in hello group.</span></span>

<span data-ttu-id="b91e0-125">bağlama için kullanmak istediğiniz toomake kullanılabilir toodefine hello birimler eklemek bir `volumes` dizi toohello kapsayıcı Grup hello Azure Resource Manager şablonu tanımında, sonra bunları tek tek Merhaba kapsayıcılara hello tanımında başvuru.</span><span class="sxs-lookup"><span data-stu-id="b91e0-125">toodefine hello volumes you want toomake available for mounting, add a `volumes` array toohello container group definition in hello Azure Resource Manager template, then reference them in hello definition of hello individual containers.</span></span>

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

<span data-ttu-id="b91e0-126">Merhaba şablon ayrı Parametreler dosyasında sağlanan parametre olarak hello depolama hesabı adı ve anahtar içerir.</span><span class="sxs-lookup"><span data-stu-id="b91e0-126">hello template includes hello storage account name and key as parameters, which can be provided in a separate parameters file.</span></span> <span data-ttu-id="b91e0-127">toopopulate hello parametreler dosyası üç değerden gerekir: Merhaba depolama hesabı adı, Azure anahtar kasanızı kaynak Kimliğini hello ve hello toostore hello depolama anahtarı kullanılan anahtar kasasına gizli adı.</span><span class="sxs-lookup"><span data-stu-id="b91e0-127">toopopulate hello parameters file, you will need three values: hello storage account name, hello resource ID of your Azure key vault, and hello key vault secret name that you used toostore hello storage key.</span></span> <span data-ttu-id="b91e0-128">Önceki adımları izlediyseniz, komut dosyası izleyen hello ile bu değerleri alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b91e0-128">If you have followed previous steps, you can get these values with hello following script:</span></span>

```azurecli-interactive
echo $STORAGE_ACCOUNT
echo $KEYVAULT_SECRET_NAME
az keyvault show --name $KEYVAULT_NAME --query [id] -o tsv
```

<span data-ttu-id="b91e0-129">Merhaba değerleri hello parametreleri dosyaya ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b91e0-129">Insert hello values into hello parameters file:</span></span>

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

## <a name="deploy-hello-container-and-manage-files"></a><span data-ttu-id="b91e0-130">Merhaba kapsayıcıyı dağıtmak ve dosyalarını yönetme</span><span class="sxs-lookup"><span data-stu-id="b91e0-130">Deploy hello container and manage files</span></span>

<span data-ttu-id="b91e0-131">Tanımlanan hello şablonla hello kapsayıcı oluşturun ve hello Azure CLI kullanarak, birim.</span><span class="sxs-lookup"><span data-stu-id="b91e0-131">With hello template defined, you can create hello container and mount its volume using hello Azure CLI.</span></span> <span data-ttu-id="b91e0-132">Merhaba şablon dosyası adlı varsayılarak *azuredeploy.json* ve o hello parametreler dosyası adlı *azuredeploy.parameters.json*, hello komut satırı sonra:</span><span class="sxs-lookup"><span data-stu-id="b91e0-132">Assuming that hello template file is named *azuredeploy.json* and that hello parameters file is named *azuredeploy.parameters.json*, then hello command line is:</span></span>

```azurecli-interactive
az group deployment create --name hellofilesdeployment --template-file azuredeploy.json --parameters @azuredeploy.parameters.json --resource-group myResourceGroup
```

<span data-ttu-id="b91e0-133">Merhaba kapsayıcı başlatıldığında sonra hello dağıtılan hello basit web uygulaması kullanarak **aci/seanmckenna-hellofiles** görüntüsü toohello yönetmek belirttiğiniz hello bağlama yolundaki hello Azure dosya paylaşımında dosyalar.</span><span class="sxs-lookup"><span data-stu-id="b91e0-133">Once hello container starts up, you can use hello simple web app deployed via hello **seanmckenna/aci-hellofiles** image, toohello manage files in hello Azure file share at hello mount path that you specified.</span></span> <span data-ttu-id="b91e0-134">Hello aşağıdaki aracılığıyla hello web uygulaması için başlangıç IP adresi alın:</span><span class="sxs-lookup"><span data-stu-id="b91e0-134">Obtain hello ip address for hello web app via hello following:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name hellofiles -o table
```

<span data-ttu-id="b91e0-135">Hello gibi bir araç kullanabilirsiniz [Microsoft Azure Storage Gezgini](http://storageexplorer.com) tooretrieve ve hello dosya writen toohello dosya paylaşımı inceleyin.</span><span class="sxs-lookup"><span data-stu-id="b91e0-135">You can use a tool like hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) tooretrieve and inspect hello file writen toohello file share.</span></span>

>[!NOTE]
> <span data-ttu-id="b91e0-136">Parametre dosyaları, Azure Resource Manager şablonları kullanarak ve hello Azure CLI ile dağıtma hakkında daha fazla toolearn bkz [Resource Manager şablonları ve Azure CLI kaynaklarla dağıtmak](../azure-resource-manager/resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="b91e0-136">toolearn more about using Azure Resource Manager templates, parameter files, and deploying with hello Azure CLI, see [Deploy resources with Resource Manager templates and Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b91e0-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b91e0-137">Next steps</span></span>

- <span data-ttu-id="b91e0-138">Hello Azure kapsayıcı örneği kullanarak, ilk kapsayıcıyı dağıtmak [hızlı başlangıç](container-instances-quickstart.md)</span><span class="sxs-lookup"><span data-stu-id="b91e0-138">Deploy for your first container using hello Azure Container Instances [quick start](container-instances-quickstart.md)</span></span>
- <span data-ttu-id="b91e0-139">Merhaba hakkında bilgi edinin [Azure kapsayıcı örnekleri ile kapsayıcı orchestrators arasındaki ilişki](container-instances-orchestrator-relationship.md)</span><span class="sxs-lookup"><span data-stu-id="b91e0-139">Learn about hello [relationship between Azure Container Instances and container orchestrators](container-instances-orchestrator-relationship.md)</span></span>
