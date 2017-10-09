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
# <a name="publish-a-managed-application-for-internal-consumption"></a><span data-ttu-id="6b3c8-103">Dahili tüketim için yönetilen bir uygulama yayımlama</span><span class="sxs-lookup"><span data-stu-id="6b3c8-103">Publish a managed application for internal consumption</span></span>

<span data-ttu-id="6b3c8-104">Oluşturma ve Azure yayımlama [yönetilen uygulamaları](managed-application-overview.md) kuruluşunuzun üyeleri için yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-104">You can create and publish Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="6b3c8-105">Örneğin, bir BT departmanının kuruluş standartlarıyla uyumluluğu sağlamak yönetilen uygulamaları yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-105">For example, an IT department can publish managed applications that ensure compliance with organizational standards.</span></span> <span data-ttu-id="6b3c8-106">Bu yönetilen uygulamaların hello hizmet Kataloğu, hello Azure Market kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-106">These managed applications are available through hello service catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="6b3c8-107">toopublish bir yönetilen uygulama hello hizmet kataloğu için aşağıdakileri yapmalısınız:</span><span class="sxs-lookup"><span data-stu-id="6b3c8-107">toopublish a managed application for hello service catalog, you must:</span></span>

* <span data-ttu-id="6b3c8-108">Merhaba üç gerekli şablon dosyalarını içeren bir .zip paketi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-108">Create a .zip package that contains hello three required template files.</span></span>
* <span data-ttu-id="6b3c8-109">Hangi kullanıcı, Grup veya uygulama hello kullanıcının abonelik toohello kaynak grubunda erişimi gerektirir karar verin.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-109">Decide which user, group, or application needs access toohello resource group in hello user's subscription.</span></span>
* <span data-ttu-id="6b3c8-110">Toohello .zip paketi işaret ve hello kimliği için erişim isteğinde hello yönetilen uygulama tanımı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-110">Create hello managed application definition that points toohello .zip package and requests access for hello identity.</span></span>

## <a name="create-a-managed-application-package"></a><span data-ttu-id="6b3c8-111">Bir yönetilen uygulama paketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b3c8-111">Create a managed application package</span></span>

<span data-ttu-id="6b3c8-112">Merhaba ilk adımı toocreate hello üç gerekli şablon dosyalarını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-112">hello first step is toocreate hello three required template files.</span></span> <span data-ttu-id="6b3c8-113">Bir .zip dosyasına paket üç tüm dosyaları ve tooan erişilebilecek bir konuma, bir depolama hesabı gibi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-113">Package all three files into a .zip file, and upload it tooan accessible location, such as a storage account.</span></span> <span data-ttu-id="6b3c8-114">Uygulama tanımı oluşturma hello yönetilen bir bağlantı toothis .zip dosyasını geçirin.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-114">You pass a link toothis .zip file when creating hello managed application definition.</span></span>

* <span data-ttu-id="6b3c8-115">**applianceMainTemplate.json**: Bu dosya hello Azure tanımlar uygulaması yönetilen hello bir parçası olarak sağlanan kaynakları.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-115">**applianceMainTemplate.json**: This file defines hello Azure resources that are provisioned as part of hello managed application.</span></span> <span data-ttu-id="6b3c8-116">Merhaba şablon normal bir Resource Manager şablonu farklı değildir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-116">hello template is no different than a regular Resource Manager template.</span></span> <span data-ttu-id="6b3c8-117">Örneğin, yönetilen bir uygulama üzerinden depolama hesabı toocreate applianceMainTemplate.json içerir:</span><span class="sxs-lookup"><span data-stu-id="6b3c8-117">For example, toocreate a storage account through a managed application, applianceMainTemplate.json contains:</span></span>

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

* <span data-ttu-id="6b3c8-118">**mainTemplate.json**: hello oluşturma uygulama yönetildiğinde bu şablonu kullanıcılara dağıtma.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-118">**mainTemplate.json**: Users deploy this template when creating hello managed application.</span></span> <span data-ttu-id="6b3c8-119">Microsoft.Solutions/appliances kaynak türü hello yönetilen uygulama kaynağı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-119">It defines hello managed application resource, which is a Microsoft.Solutions/appliances resource type.</span></span> <span data-ttu-id="6b3c8-120">Bu dosya applianceMainTemplate.json hello kaynakları için gereksinim duyduğunuz tüm hello parametrelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-120">This file contains all hello parameters you need for hello resources in applianceMainTemplate.json.</span></span>

  <span data-ttu-id="6b3c8-121">Bu şablonda iki önemli özellikleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-121">You set two important properties in this template.</span></span> <span data-ttu-id="6b3c8-122">İlk olarak, hello **applianceDefinitionId** hello kimliği hello yönetilen uygulama tanımının bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-122">First, hello **applianceDefinitionId** property is hello ID of hello managed application definition.</span></span> <span data-ttu-id="6b3c8-123">Bu konunun ilerleyen bölümlerinde hello tanımı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-123">You create hello definition later in this topic.</span></span> <span data-ttu-id="6b3c8-124">Bu değer ayarlandığında, hangi abonelik ve kaynak grubu toouse depolamak için yönetilen uygulama tanımları hello karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-124">When setting this value, you must decide which subscription and resource group toouse for storing hello managed application definitions.</span></span> <span data-ttu-id="6b3c8-125">Ve hello tanımı için bir ad üzerinde karar vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-125">And, you must decide on a name for hello definition.</span></span> <span data-ttu-id="6b3c8-126">Merhaba kimliği hello biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="6b3c8-126">hello ID is in hello format:</span></span>

  `/subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Solutions/applianceDefinitions/<definition-name>`

  <span data-ttu-id="6b3c8-127">İkinci olarak, hello **managedResourceGroupId** özelliği hello Azure kaynaklarının oluşturulduğu hello kaynak grubunun hello kimliği değil.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-127">Second, hello **managedResourceGroupId** property is hello ID of hello resource group where hello Azure resources are created.</span></span> <span data-ttu-id="6b3c8-128">Bu kaynak grubu adı için bir değer atamak veya bir ad sağlayın hello kullanıcının izin verin.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-128">You can assign a value for this resource group name or let hello user provide a name.</span></span> <span data-ttu-id="6b3c8-129">Merhaba kimliğinin Hello biçimdedir:</span><span class="sxs-lookup"><span data-stu-id="6b3c8-129">hello format of hello ID is:</span></span>

  <span data-ttu-id="6b3c8-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-130">`/subscriptions/<subscription-id>/resourceGroups/<resoure-group-name>`.</span></span>

  <span data-ttu-id="6b3c8-131">Aşağıdaki örnek hello mainTemplate.json dosyasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-131">hello following example shows a mainTemplate.json file.</span></span> <span data-ttu-id="6b3c8-132">Dağıtılan hello kaynakları için bir kaynak grubu belirtir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-132">It specifies a resource group for hello deployed resources.</span></span> <span data-ttu-id="6b3c8-133">Merhaba tanımı kimliği olan bir tanımı adlı kümesi toouse **storageApp** bir kaynak grubunda adlı **managedApplicationGroup**.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-133">hello definition ID is set toouse a definition named **storageApp** in a resource group named **managedApplicationGroup**.</span></span> <span data-ttu-id="6b3c8-134">Bu değerleri toouse farklı adlarını değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-134">You can change these values toouse different names.</span></span> <span data-ttu-id="6b3c8-135">Merhaba tanımı kimliği kendi abonelik kimliği sağlayın</span><span class="sxs-lookup"><span data-stu-id="6b3c8-135">Provide your own subscription ID in hello definition ID.</span></span>

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

* <span data-ttu-id="6b3c8-136">**applianceCreateUiDefinition.json**: yönetilen uygulamayı oluşturan kullanıcıların hello hello Azure portal bu dosya toogenerate hello kullanıcı arabirimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-136">**applianceCreateUiDefinition.json**: hello Azure portal uses this file toogenerate hello user interface for users who create hello managed application.</span></span> <span data-ttu-id="6b3c8-137">Tanımladığınız nasıl kullanıcılar her parametre için değer girin.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-137">You define how users provide input for each parameter.</span></span> <span data-ttu-id="6b3c8-138">Bir açılan listesinden, metin kutusuna, parola kutusu ve diğer araçları giriş gibi seçeneklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-138">You can use options like a drop-down list, text box, password box, and other input tools.</span></span> <span data-ttu-id="6b3c8-139">toocreate UI tanım dosyası yönetilen bir uygulama için nasıl görürüm toolearn [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b3c8-139">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>

  <span data-ttu-id="6b3c8-140">Merhaba aşağıdaki örnek, kullanıcıların toospecify hello depolama hesabı adı öneki metin kutusu aracılığıyla sağlayan bir applianceCreateUiDefinition.json dosyayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-140">hello following example shows an applianceCreateUiDefinition.json file that enables users toospecify hello storage account name prefix through a textbox.</span></span>

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

<span data-ttu-id="6b3c8-141">Tüm gerekli hello dosyaları hazır olduktan sonra bunları bir .zip dosyası olarak paketleyin.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-141">After all hello needed files are ready, package them as a .zip file.</span></span> <span data-ttu-id="6b3c8-142">Merhaba üç dosyalar hello kök düzeyinde hello .zip dosyası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-142">hello three files must be at hello root level of hello .zip file.</span></span> <span data-ttu-id="6b3c8-143">Bir klasöre yerleştirin, hello oluşturma dosyalar yoksa hello gereken durumlar uygulama tanımı yönetildiğinde bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-143">If you put them in a folder, you receive an error when creating hello managed application definition that states hello required files are not present.</span></span> <span data-ttu-id="6b3c8-144">Burada tüketilebilir hello paket tooan erişilebilir konumdaki karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-144">Upload hello package tooan accessible location from where it can be consumed.</span></span> <span data-ttu-id="6b3c8-145">Bu makalenin sonraki bölümlerinde Hello hello .zip dosyası bir genel olarak erişilebilir depolama blob kapsayıcısında var. varsayar.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-145">hello remainder of this article assumes hello .zip file exists in a publicly accessible storage blob container.</span></span>

## <a name="create-an-azure-active-directory-user-group-or-application"></a><span data-ttu-id="6b3c8-146">Bir Azure Active Directory kullanıcı grubu veya uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b3c8-146">Create an Azure Active Directory user group or application</span></span>

<span data-ttu-id="6b3c8-147">Merhaba ikinci adım hello kaynakları hello müşteri adına yönetmek için tooselect bir kullanıcı grubu veya uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-147">hello second step is tooselect a user group or application for managing hello resources on behalf of hello customer.</span></span> <span data-ttu-id="6b3c8-148">Bu kullanıcı grubu veya uygulama izinleri atanan hello yönetilen kaynak grubu according toohello rolü vardır.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-148">This user group or application has permissions on hello managed resource group according toohello role that is assigned.</span></span> <span data-ttu-id="6b3c8-149">Merhaba rol sahibi veya katkıda gibi herhangi bir yerleşik rol tabanlı erişim denetimi (RBAC) rolüne olabilir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-149">hello role can be any built-in Role-Based Access Control (RBAC) role like Owner or Contributor.</span></span> <span data-ttu-id="6b3c8-150">Tek bir kullanıcı izni toomanage hello kaynakları verebilirsiniz, ancak genellikle bu izni tooa kullanıcı grubuna atayın.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-150">You also can give an individual user permission toomanage hello resources, but typically you assign this permission tooa user group.</span></span> <span data-ttu-id="6b3c8-151">Yeni bir Active Directory kullanıcı grubu toocreate bkz [bir grup oluşturun ve Azure Active Directory'de üye ekleme](../active-directory/active-directory-groups-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6b3c8-151">toocreate a new Active Directory user group, see [Create a group and add members in Azure Active Directory](../active-directory/active-directory-groups-create-azure-portal.md).</span></span>

<span data-ttu-id="6b3c8-152">Merhaba kaynakları yönetmek için hello kullanıcı grubu toouse hello nesne kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-152">You need hello object ID of hello user group toouse for managing hello resources.</span></span> <span data-ttu-id="6b3c8-153">Aşağıdaki örnek hello nasıl tooget hello hello grubun görünen ad nesne kimliği gösterir:</span><span class="sxs-lookup"><span data-stu-id="6b3c8-153">hello following example shows how tooget hello object ID from hello group's display name:</span></span>

```azurecli-interactive
az ad group show --group exampleGroupName
```

<span data-ttu-id="6b3c8-154">Merhaba örnek komut, çıktı aşağıdaki hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="6b3c8-154">hello example command returns hello following output:</span></span>

```azurecli
{
    "displayName": "exampleGroupName",
    "mail": null,
    "objectId": "9aabd3ad-3716-4242-9d8e-a85df479d5d9",
    "objectType": "Group",
    "securityEnabled": true
}
```

<span data-ttu-id="6b3c8-155">tooretrieve yalnızca hello nesne kimliği, kullanın:</span><span class="sxs-lookup"><span data-stu-id="6b3c8-155">tooretrieve just hello object ID, use:</span></span>

```azurecli-interactive
groupid=$(az ad group show --group exampleGroupName --query objectId --output tsv)
```

## <a name="get-hello-role-definition-id"></a><span data-ttu-id="6b3c8-156">Merhaba rol tanımı kimliği alma</span><span class="sxs-lookup"><span data-stu-id="6b3c8-156">Get hello role definition ID</span></span>

<span data-ttu-id="6b3c8-157">Ardından, hello RBAC yerleşik rol toogrant erişim toohello kullanıcı, kullanıcı grubu veya uygulama istediğiniz hello rol tanımı kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-157">Next, you need hello role definition ID of hello RBAC built-in role you want toogrant access toohello user, user group, or application.</span></span> <span data-ttu-id="6b3c8-158">Genellikle, hello sahibi veya katkıda bulunan veya okuyucu rolüne kullanın.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-158">Typically, you use hello Owner or Contributor or Reader role.</span></span> <span data-ttu-id="6b3c8-159">komutu aşağıdaki hello nasıl tooget hello hello sahibi rol için rol tanımı kimliği gösterir:</span><span class="sxs-lookup"><span data-stu-id="6b3c8-159">hello following command shows how tooget hello role definition ID for hello Owner role:</span></span>


```azurecli-interactive
az role definition list --name owner
```

<span data-ttu-id="6b3c8-160">Bu komut çıktı aşağıdaki hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="6b3c8-160">That command returns hello following output:</span></span>

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

<span data-ttu-id="6b3c8-161">Merhaba değerini örnek önceki hello hello "name" özelliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-161">You need hello value of hello "name" property from hello preceding example.</span></span> <span data-ttu-id="6b3c8-162">Bu özellik yalnızca ile alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6b3c8-162">You can retrieve just that property with:</span></span>

```azurecli-interactive
roleid=$(az role definition list --name Owner --query [].name --output tsv)
```

## <a name="create-hello-managed-application-definition"></a><span data-ttu-id="6b3c8-163">Yönetilen hello uygulama tanımı oluşturun</span><span class="sxs-lookup"><span data-stu-id="6b3c8-163">Create hello managed application definition</span></span>

<span data-ttu-id="6b3c8-164">Zaten bir kaynak grubu, yönetilen uygulama tanımını depolamak için yoksa, şimdi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="6b3c8-164">If you do not already have a resource group for storing your managed application definition, create one now:</span></span>

```azurecli-interactive
az group create --name managedApplicationGroup --location westcentralus
```

<span data-ttu-id="6b3c8-165">Şimdi, yönetilen hello uygulama tanımı kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-165">Now, create hello managed application definition resource.</span></span>

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

<span data-ttu-id="6b3c8-166">Örnek önceki hello kullanılan hello Parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6b3c8-166">hello parameters used in hello preceding example are:</span></span>

* <span data-ttu-id="6b3c8-167">**kaynak grubu**: hello hello uygulama tanımı yönetildiği hello kaynak grubunun adını oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-167">**resource-group**: hello name of hello resource group where hello managed application definition is created.</span></span>
* <span data-ttu-id="6b3c8-168">**Kilit düzeyi**: kilit hello türünü hello yönetilen kaynak grubuna yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-168">**lock-level**: hello type of lock placed on hello managed resource group.</span></span> <span data-ttu-id="6b3c8-169">Merhaba müşteri bu kaynak grubu üzerindeki istenmeyen işlemlerini gerçekleştirmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-169">It prevents hello customer from performing undesirable operations on this resource group.</span></span> <span data-ttu-id="6b3c8-170">Şu anda salt okunur hello kilit düzeyi yalnızca desteklenen olur.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-170">Currently, ReadOnly is hello only supported lock level.</span></span> <span data-ttu-id="6b3c8-171">Salt okunur belirtildiğinde, hello müşteri hello kaynakları hello yönetilen kaynak grubunda mevcut yalnızca okuyabilir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-171">When ReadOnly is specified, hello customer can only read hello resources present in hello managed resource group.</span></span>
* <span data-ttu-id="6b3c8-172">**yetkilerini**: kullanılan toogrant izin toohello yönetilen kaynak grubu olan hello sorumlu kimliği ve hello rol tanımı kimliği açıklar.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-172">**authorizations**: Describes hello principal ID and hello role definition ID that are used toogrant permission toohello managed resource group.</span></span> <span data-ttu-id="6b3c8-173">Merhaba biçiminde belirtilen `<principalId>:<roleDefinitionId>`.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-173">It's specified in hello format of `<principalId>:<roleDefinitionId>`.</span></span> <span data-ttu-id="6b3c8-174">Bu özellik için birden çok değer de belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-174">Multiple values also can be specified for this property.</span></span> <span data-ttu-id="6b3c8-175">Birden çok değer gerekirse hello biçiminde belirtilmelidir `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-175">If multiple values are needed, they should be specified in hello form `<principalId1>:<roleDefinitionId1> <principalId2>:<roleDefinitionId2>`.</span></span> <span data-ttu-id="6b3c8-176">Birden çok değeri boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-176">Multiple values are separated by a space.</span></span>
* <span data-ttu-id="6b3c8-177">**Paket dosyası URI**: Merhaba hello yönetilen uygulamayı bir Azure Storage blobu olabilir hello şablon dosyalarını içeren bir paket konumu.</span><span class="sxs-lookup"><span data-stu-id="6b3c8-177">**package-file-uri**: hello location of hello managed application package that contains hello template files, which can be an Azure Storage blob.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b3c8-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6b3c8-178">Next steps</span></span>

* <span data-ttu-id="6b3c8-179">Bir giriş toomanaged uygulamalar için bkz [yönetilen uygulama genel bakış](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b3c8-179">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="6b3c8-180">Merhaba dosyaları örnekleri için bkz: [yönetilen uygulama örnekleri](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span><span class="sxs-lookup"><span data-stu-id="6b3c8-180">For examples of hello files, see [Managed application samples](https://github.com/Azure/azure-managedapp-samples/tree/master/samples).</span></span>
* <span data-ttu-id="6b3c8-181">Hizmet Kataloğu yönetilen uygulama kullanma hakkında daha fazla bilgi için bkz: [bir hizmet Kataloğu yönetilen uygulama tüketen](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="6b3c8-181">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
* <span data-ttu-id="6b3c8-182">Yönetilen uygulamaların toohello Azure Marketi'nde yayımlama hakkında daha fazla bilgi için bkz: [Azure hello Market uygulamalarda yönetilen](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="6b3c8-182">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="6b3c8-183">Merhaba Market yönetilen bir uygulamadan kullanma hakkında daha fazla bilgi için bkz: [tüketen Azure hello Market uygulamalarda yönetilen](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="6b3c8-183">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="6b3c8-184">toocreate UI tanım dosyası yönetilen bir uygulama için nasıl görürüm toolearn [CreateUiDefinition ile çalışmaya başlama](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6b3c8-184">toolearn how toocreate a UI definition file for a managed application, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
