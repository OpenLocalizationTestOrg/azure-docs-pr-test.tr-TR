---
title: "İlk Azure Resource Manager şablonunu oluşturma | Microsoft Docs"
description: "İlk Azure Resource Manager şablonunuzu oluşturmaya yönelik adım adım kılavuz. Şablon oluşturmak için bir depolama hesabına ait şablon başvurusunun nasıl kullanılacağını gösterir."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 49086b51e2db1aebed45746306ae14b6f1feb631
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="67f30-104">İlk Azure Resource Manager şablonunuzu oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="67f30-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="67f30-105">Bu konu başlığında, ilk Azure Resource Manager şablonunuzu oluşturma adımları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="67f30-105">This topic walks you through the steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="67f30-106">Resource Manager şablonları, çözümünüz için dağıtmanız gereken kaynakları tanımlayan JSON dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="67f30-106">Resource Manager templates are JSON files that define the resources you need to deploy for your solution.</span></span> <span data-ttu-id="67f30-107">Azure çözümlerinizi dağıtma ve yönetmeyle ilgili kavramları anlamak için bkz. [Azure Resource Manager’a genel bakış](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67f30-107">To understand the concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="67f30-108">Kaynaklarınız varsa ve bu kaynaklara yönelik bir şablon almak istiyorsanız bkz. [Mevcut kaynaklardan Azure Resource Manager şablonunu dışarı aktarma](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="67f30-108">If you have existing resources and want to get a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="67f30-109">Şablonları oluşturup düzeltmek için bir JSON düzenleyicisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="67f30-109">To create and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="67f30-110">[Visual Studio Code](https://code.visualstudio.com/) basit, açık kaynaklı ve platformlar arası bir kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="67f30-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="67f30-111">Resource Manager şablonları oluşturmak için Visual Studio Code kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="67f30-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="67f30-112">Bu konu başlığı, VS Code kullandığınızı varsayar; ancak başka bir JSON düzenleyiciniz (Visual Studio gibi) varsa kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67f30-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67f30-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="67f30-113">Prerequisites</span></span>

* <span data-ttu-id="67f30-114">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="67f30-114">Visual Studio Code.</span></span> <span data-ttu-id="67f30-115">Gerekirse, [https://code.visualstudio.com/](https://code.visualstudio.com/) adresinden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="67f30-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="67f30-116">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="67f30-116">An Azure subscription.</span></span> <span data-ttu-id="67f30-117">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="67f30-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="67f30-118">Şablon oluşturma</span><span class="sxs-lookup"><span data-stu-id="67f30-118">Create template</span></span>

<span data-ttu-id="67f30-119">Aboneliğinize bir depolama hesabı dağıtan basit bir şablonla başlayalım.</span><span class="sxs-lookup"><span data-stu-id="67f30-119">Let's start with a simple template that deploys a storage account to your subscription.</span></span>

1. <span data-ttu-id="67f30-120">**Dosya** > **Yeni Dosya**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="67f30-120">Select **File** > **New File**.</span></span> 

   ![Yeni dosya](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="67f30-122">Aşağıdaki JSON söz dizimini kopyalayıp dosyanıza yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="67f30-122">Copy and paste the following JSON syntax into your file:</span></span>

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   <span data-ttu-id="67f30-123">Depolama hesabı adlarını ayarlamayı zorlaştıran birkaç kısıtlama vardır.</span><span class="sxs-lookup"><span data-stu-id="67f30-123">Storage account names have several restrictions that make them difficult to set.</span></span> <span data-ttu-id="67f30-124">Ad 3 ila 24 karakter uzunluğunda olmalı, yalnızca sayı ile küçük harf içermeli ve benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="67f30-124">The name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="67f30-125">Önceki şablonda bir karma değer oluşturmak için [uniqueString](resource-group-template-functions-string.md#uniquestring) kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="67f30-125">The preceding template uses the [uniqueString](resource-group-template-functions-string.md#uniquestring) function to generate a hash value.</span></span> <span data-ttu-id="67f30-126">Bu karma değere daha fazla anlam katmak için *storage* ön eki getirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="67f30-126">To give this hash value more meaning, it adds the prefix *storage*.</span></span> 

3. <span data-ttu-id="67f30-127">Bu dosyayı yerel bir klasöre **azuredeploy.json** olarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="67f30-127">Save this file as **azuredeploy.json** to a local folder.</span></span>

   ![Şablonu kaydetme](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="67f30-129">Şablon dağıtma</span><span class="sxs-lookup"><span data-stu-id="67f30-129">Deploy template</span></span>

<span data-ttu-id="67f30-130">Bu şablonu dağıtmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="67f30-130">You are ready to deploy this template.</span></span> <span data-ttu-id="67f30-131">Bir kaynak grubu oluşturmak için PowerShell veya Azure CLI kullanın.</span><span class="sxs-lookup"><span data-stu-id="67f30-131">You use either PowerShell or Azure CLI to create a resource group.</span></span> <span data-ttu-id="67f30-132">Ardından, bu kaynak grubuna bir depolama hesabı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="67f30-132">Then, you deploy a storage account to that resource group.</span></span>

* <span data-ttu-id="67f30-133">PowerShell için, şablonu içeren klasörden aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="67f30-133">For PowerShell, use the following commands from the folder containing the template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="67f30-134">Yerel bir Azure CLI yüklemesi için, şablonu içeren klasörden aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="67f30-134">For a local installation of Azure CLI, use the following commands from the folder containing the template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="67f30-135">Dağıtım tamamlandığında, depolama hesabınız kaynak grubunda mevcut olur.</span><span class="sxs-lookup"><span data-stu-id="67f30-135">When deployment finishes, your storage account exists in the resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="67f30-136">Cloud Shell'den şablon dağıtma</span><span class="sxs-lookup"><span data-stu-id="67f30-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="67f30-137">[Cloud Shell](../cloud-shell/overview.md)’i kullanarak, şablonunuzu dağıtmak için Azure CLI komutlarını çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67f30-137">You can use [Cloud Shell](../cloud-shell/overview.md) to run the Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="67f30-138">Ancak, ilk olarak şablonunuzu Cloud Shell dosya paylaşımına yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="67f30-138">However, you must first load your template into the file share for your Cloud Shell.</span></span> <span data-ttu-id="67f30-139">Daha önce Cloud Shell kullanmadıysanız, kurulumu hakkında bilgi için bkz. [Azure Cloud Shell’e Genel Bakış](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="67f30-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="67f30-140">[Azure Portal](https://portal.azure.com)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="67f30-140">Log in to the [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="67f30-141">Cloud Shell kaynak grubunuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="67f30-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="67f30-142">Ad deseni `cloud-shell-storage-<region>` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="67f30-142">The name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Kaynak grubu seçin](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="67f30-144">Cloud Shell için depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="67f30-144">Select the storage account for your Cloud Shell.</span></span>

   ![Depolama hesabı seçme](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="67f30-146">**Dosyalar**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="67f30-146">Select **Files**.</span></span>

   ![Dosya seçme](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="67f30-148">Cloud Shell için dosya paylaşımı seçin.</span><span class="sxs-lookup"><span data-stu-id="67f30-148">Select the file share for Cloud Shell.</span></span> <span data-ttu-id="67f30-149">Ad deseni `cs-<user>-<domain>-com-<uniqueGuid>` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="67f30-149">The name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Dosya paylaşımı seçme](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="67f30-151">**Dizin ekle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="67f30-151">Select **Add directory**.</span></span>

   ![Dizin ekleme](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="67f30-153">**Şablonlar** olarak adlandırıp **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="67f30-153">Name it **templates**, and select **Okay**.</span></span>

   ![Ad dizini](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="67f30-155">Yeni dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="67f30-155">Select your new directory.</span></span>

   ![Dizin seçme](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="67f30-157">**Karşıya Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="67f30-157">Select **Upload**.</span></span>

   ![Karşıya yükleme seçme](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="67f30-159">Şablonunuzu bulup karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="67f30-159">Find and upload your template.</span></span>

   ![Dosya yükleme](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="67f30-161">İstemi açın.</span><span class="sxs-lookup"><span data-stu-id="67f30-161">Open the prompt.</span></span>

   ![Cloud Shell’i açma](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="67f30-163">Cloud Shell’e aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="67f30-163">Enter the following commands in the Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="67f30-164">Dağıtım tamamlandığında, depolama hesabınız kaynak grubunda mevcut olur.</span><span class="sxs-lookup"><span data-stu-id="67f30-164">When deployment finishes, your storage account exists in the resource group.</span></span>

## <a name="customize-the-template"></a><span data-ttu-id="67f30-165">Şablonu özelleştirme</span><span class="sxs-lookup"><span data-stu-id="67f30-165">Customize the template</span></span>

<span data-ttu-id="67f30-166">Şablon düzgün çalışır, ancak esnek değildir.</span><span class="sxs-lookup"><span data-stu-id="67f30-166">The template works fine, but it is not flexible.</span></span> <span data-ttu-id="67f30-167">Şablon ABD Orta Güney bölgesine her zaman yerel olarak yedekli depolama dağıtır.</span><span class="sxs-lookup"><span data-stu-id="67f30-167">It always deploys a locally redundant storage to South Central US.</span></span> <span data-ttu-id="67f30-168">Ad her zaman *storage* ve ardından bir karma değer içerir.</span><span class="sxs-lookup"><span data-stu-id="67f30-168">The name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="67f30-169">Şablonu farklı senaryolar için kullanmak üzere şablona parametreler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="67f30-169">To enable using the template for different scenarios, add parameters to the template.</span></span>

<span data-ttu-id="67f30-170">Aşağıdaki örnekte iki parametre ile birlikte parametreler bölümü gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="67f30-170">The following example shows the parameters section with two parameters.</span></span> <span data-ttu-id="67f30-171">İlk `storageSKU` parametresi, yedeklilik türünü belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="67f30-171">The first parameter `storageSKU` enables you to specify the type of redundancy.</span></span> <span data-ttu-id="67f30-172">Bir depolama hesabı için geçerli olan değerlere geçirebileceğiniz değerleri sınırlar.</span><span class="sxs-lookup"><span data-stu-id="67f30-172">It limits the values you can pass in to values that are valid for a storage account.</span></span> <span data-ttu-id="67f30-173">Ayrıca, varsayılan bir değer belirtir.</span><span class="sxs-lookup"><span data-stu-id="67f30-173">It also specifies a default value.</span></span> <span data-ttu-id="67f30-174">İkinci `storageNamePrefix` parametresi en çok 11 karaktere izin verecek şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="67f30-174">The second parameter `storageNamePrefix` is set to allow a maximum of 11 characters.</span></span> <span data-ttu-id="67f30-175">Varsayılan bir değer belirtir.</span><span class="sxs-lookup"><span data-stu-id="67f30-175">It specifies a default value.</span></span>

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "The type of replication to use for the storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="67f30-176">Değişkenler bölümünde `storageName` adlı bir değişken ekleyin.</span><span class="sxs-lookup"><span data-stu-id="67f30-176">In the variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="67f30-177">Bu değişken, parametrelerden bir ön ek değerini [uniqueString](resource-group-template-functions-string.md#uniquestring) işlevindeki bir karma değer ile birleştirir.</span><span class="sxs-lookup"><span data-stu-id="67f30-177">It combines the prefix value from the parameters and a hash value from the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="67f30-178">Tüm karakterleri küçük harfe dönüştürmek için [toLower](resource-group-template-functions-string.md#tolower) işlevini kullanır.</span><span class="sxs-lookup"><span data-stu-id="67f30-178">It uses the [toLower](resource-group-template-functions-string.md#tolower) function to convert all characters to lowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="67f30-179">Depolama hesabınız için bu yeni değerleri kullanmak üzere kaynak tanımını değiştirin:</span><span class="sxs-lookup"><span data-stu-id="67f30-179">To use these new values for your storage account, change the resource definition:</span></span>

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

<span data-ttu-id="67f30-180">Depolama hesabı adının eklediğiniz değişkene ayarlandığına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="67f30-180">Notice that the name of the storage account is now set to the variable that you added.</span></span> <span data-ttu-id="67f30-181">SKU adı, parametre değerine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="67f30-181">The SKU name is set to the value of the parameter.</span></span> <span data-ttu-id="67f30-182">Konum, kaynak grubu ile aynı konuma ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="67f30-182">The location is set the same location as the resource group.</span></span>

<span data-ttu-id="67f30-183">Dosyanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="67f30-183">Save your file.</span></span> 

<span data-ttu-id="67f30-184">Bu makaledeki adımları tamamladıktan sonra, artık şablonunuz şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="67f30-184">After completing the steps in this article, your template now looks like:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "The type of replication to use for the storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "The value to use for starting the storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a><span data-ttu-id="67f30-185">Şablonu yeniden dağıtma</span><span class="sxs-lookup"><span data-stu-id="67f30-185">Redeploy template</span></span>

<span data-ttu-id="67f30-186">Şablonu farklı değerlerle yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="67f30-186">Redeploy the template with different values.</span></span>

<span data-ttu-id="67f30-187">PowerShell için şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="67f30-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="67f30-188">Azure CLI için şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="67f30-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="67f30-189">Cloud Shell için, değiştirdiğiniz şablonu dosya paylaşımına yükleyin.</span><span class="sxs-lookup"><span data-stu-id="67f30-189">For the Cloud Shell, upload your changed template to the file share.</span></span> <span data-ttu-id="67f30-190">Var olan dosyanın üzerine yazın.</span><span class="sxs-lookup"><span data-stu-id="67f30-190">Overwrite the existing file.</span></span> <span data-ttu-id="67f30-191">Ardından, aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="67f30-191">Then, use the following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="67f30-192">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="67f30-192">Clean up resources</span></span>

<span data-ttu-id="67f30-193">Artık gerekli değilse, kaynak grubunu silerek dağıttığınız kaynakları temizleyin.</span><span class="sxs-lookup"><span data-stu-id="67f30-193">When no longer needed, clean up the resources you deployed by deleting the resource group.</span></span>

<span data-ttu-id="67f30-194">PowerShell için şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="67f30-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="67f30-195">Azure CLI için şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="67f30-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="67f30-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="67f30-196">Next steps</span></span>
* <span data-ttu-id="67f30-197">Bir şablonun yapısı hakkında daha fazla bilgi edinmek için bkz. [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="67f30-197">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="67f30-198">Bir depolama hesabının özellikleri hakkında bilgi edinmek için bkz. [depolama hesapları şablon başvurusu](/azure/templates/microsoft.storage/storageaccounts).</span><span class="sxs-lookup"><span data-stu-id="67f30-198">To learn about the properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="67f30-199">Farklı türlerde çözümler için tam şablonları görüntülemek üzere bkz. [Azure Hızlı Başlangıç Şablonları](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="67f30-199">To view complete templates for many different types of solutions, see the [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
