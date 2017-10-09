---
title: "aaaCreate ilk Azure Resource Manager şablonu | Microsoft Docs"
description: "Adım Adım Kılavuzu toocreating ilk Azure Resource Manager şablonu. Nasıl toouse hello şablon başvurusu bir depolama hesabı toocreate hello şablon için gösterilir."
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
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a><span data-ttu-id="8fb23-104">İlk Azure Resource Manager şablonunuzu oluşturma ve dağıtma</span><span class="sxs-lookup"><span data-stu-id="8fb23-104">Create and deploy your first Azure Resource Manager template</span></span>
<span data-ttu-id="8fb23-105">Bu konu, ilk Azure Resource Manager şablonu oluşturma hello adımlarda size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="8fb23-105">This topic walks you through hello steps of creating your first Azure Resource Manager template.</span></span> <span data-ttu-id="8fb23-106">Resource Manager şablonları çözümünüz için toodeploy ihtiyacınız hello kaynakları tanımlayan JSON dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="8fb23-106">Resource Manager templates are JSON files that define hello resources you need toodeploy for your solution.</span></span> <span data-ttu-id="8fb23-107">Azure çözümlerinizi yönetme ve dağıtma ile ilişkili toounderstand hello bkz [Azure Resource Manager'a genel bakış](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8fb23-107">toounderstand hello concepts associated with deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span> <span data-ttu-id="8fb23-108">Mevcut bir kaynağı var ve bu kaynakları için tooget bir şablon istiyorsanız, bkz [mevcut kaynaklardan Azure Resource Manager şablonunu dışarı aktarma](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="8fb23-108">If you have existing resources and want tooget a template for those resources, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

<span data-ttu-id="8fb23-109">toocreate ve gözden geçirme şablonları, JSON düzenleyicisinin gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fb23-109">toocreate and revise templates, you need a JSON editor.</span></span> <span data-ttu-id="8fb23-110">[Visual Studio Code](https://code.visualstudio.com/) basit, açık kaynaklı ve platformlar arası bir kod düzenleyicisidir.</span><span class="sxs-lookup"><span data-stu-id="8fb23-110">[Visual Studio Code](https://code.visualstudio.com/) is a lightweight, open-source, cross-platform code editor.</span></span> <span data-ttu-id="8fb23-111">Resource Manager şablonları oluşturmak için Visual Studio Code kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="8fb23-111">We strongly recommend using Visual Studio Code for creating Resource Manager templates.</span></span> <span data-ttu-id="8fb23-112">Bu konu başlığı, VS Code kullandığınızı varsayar; ancak başka bir JSON düzenleyiciniz (Visual Studio gibi) varsa kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8fb23-112">This topic assumes you are using VS Code; however, if you have another JSON editor (like Visual Studio), you can use that editor.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fb23-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8fb23-113">Prerequisites</span></span>

* <span data-ttu-id="8fb23-114">Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="8fb23-114">Visual Studio Code.</span></span> <span data-ttu-id="8fb23-115">Gerekirse, [https://code.visualstudio.com/](https://code.visualstudio.com/) adresinden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8fb23-115">If needed, install it from [https://code.visualstudio.com/](https://code.visualstudio.com/).</span></span>
* <span data-ttu-id="8fb23-116">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="8fb23-116">An Azure subscription.</span></span> <span data-ttu-id="8fb23-117">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8fb23-117">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-template"></a><span data-ttu-id="8fb23-118">Şablon oluşturma</span><span class="sxs-lookup"><span data-stu-id="8fb23-118">Create template</span></span>

<span data-ttu-id="8fb23-119">Bir depolama hesabı tooyour aboneliği dağıtır basit bir şablonla başlayalım.</span><span class="sxs-lookup"><span data-stu-id="8fb23-119">Let's start with a simple template that deploys a storage account tooyour subscription.</span></span>

1. <span data-ttu-id="8fb23-120">**Dosya** > **Yeni Dosya**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="8fb23-120">Select **File** > **New File**.</span></span> 

   ![Yeni dosya](./media/resource-manager-create-first-template/new-file.png)

2. <span data-ttu-id="8fb23-122">Kopyalama ve yapıştırma dosyanıza JSON söz dizimi aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="8fb23-122">Copy and paste hello following JSON syntax into your file:</span></span>

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

   <span data-ttu-id="8fb23-123">Depolama hesabı adları zor tooset olun birkaç kısıtlamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="8fb23-123">Storage account names have several restrictions that make them difficult tooset.</span></span> <span data-ttu-id="8fb23-124">Merhaba adı uzunluğu, kullanım yalnızca sayılar ve küçük harfler 3 ile 24 karakter arasında olmalı ve benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fb23-124">hello name must be between 3 and 24 characters in length, use only numbers and lower-case letters, and be unique.</span></span> <span data-ttu-id="8fb23-125">Merhaba önceki şablonu kullanan hello [uniqueString](resource-group-template-functions-string.md#uniquestring) toogenerate bir karma değer işlev.</span><span class="sxs-lookup"><span data-stu-id="8fb23-125">hello preceding template uses hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function toogenerate a hash value.</span></span> <span data-ttu-id="8fb23-126">toogive Bu karma değer daha anlamına gelir, hello önekini ekler *depolama*.</span><span class="sxs-lookup"><span data-stu-id="8fb23-126">toogive this hash value more meaning, it adds hello prefix *storage*.</span></span> 

3. <span data-ttu-id="8fb23-127">Bu dosya olarak kaydetmek **azuredeploy.json** tooa yerel klasör.</span><span class="sxs-lookup"><span data-stu-id="8fb23-127">Save this file as **azuredeploy.json** tooa local folder.</span></span>

   ![Şablonu kaydetme](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a><span data-ttu-id="8fb23-129">Şablon dağıtma</span><span class="sxs-lookup"><span data-stu-id="8fb23-129">Deploy template</span></span>

<span data-ttu-id="8fb23-130">Bu şablonu hazır toodeploy şunlardır.</span><span class="sxs-lookup"><span data-stu-id="8fb23-130">You are ready toodeploy this template.</span></span> <span data-ttu-id="8fb23-131">PowerShell veya Azure CLI toocreate bir kaynak grubu kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fb23-131">You use either PowerShell or Azure CLI toocreate a resource group.</span></span> <span data-ttu-id="8fb23-132">Ardından, bir depolama hesabı toothat kaynak grubu dağıtın.</span><span class="sxs-lookup"><span data-stu-id="8fb23-132">Then, you deploy a storage account toothat resource group.</span></span>

* <span data-ttu-id="8fb23-133">İçin PowerShell komutlarını hello şablonu içeren hello klasöründen aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="8fb23-133">For PowerShell, use hello following commands from hello folder containing hello template:</span></span>

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* <span data-ttu-id="8fb23-134">Azure CLI yerel yükleme için komutları hello şablonu içeren hello klasöründen aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="8fb23-134">For a local installation of Azure CLI, use hello following commands from hello folder containing hello template:</span></span>

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

<span data-ttu-id="8fb23-135">Dağıtım tamamlandığında, depolama hesabınız hello kaynak grubunda yok.</span><span class="sxs-lookup"><span data-stu-id="8fb23-135">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="8fb23-136">Cloud Shell'den şablon dağıtma</span><span class="sxs-lookup"><span data-stu-id="8fb23-136">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="8fb23-137">Kullanabileceğiniz [bulut Kabuk](../cloud-shell/overview.md) toorun hello Azure CLI komutları şablonunuzu dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="8fb23-137">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="8fb23-138">Ancak, ilk şablonunuzu hello dosya paylaşım içine bulut Kabuğunuzu yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fb23-138">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="8fb23-139">Daha önce Cloud Shell kullanmadıysanız, kurulumu hakkında bilgi için bkz. [Azure Cloud Shell’e Genel Bakış](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="8fb23-139">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="8fb23-140">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8fb23-140">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="8fb23-141">Cloud Shell kaynak grubunuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="8fb23-141">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="8fb23-142">Merhaba adı deseni `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="8fb23-142">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Kaynak grubu seçin](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. <span data-ttu-id="8fb23-144">Bulut Kabuğunuzu Hello depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="8fb23-144">Select hello storage account for your Cloud Shell.</span></span>

   ![Depolama hesabı seçme](./media/resource-manager-create-first-template/select-storage.png)

4. <span data-ttu-id="8fb23-146">**Dosyalar**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="8fb23-146">Select **Files**.</span></span>

   ![Dosya seçme](./media/resource-manager-create-first-template/select-files.png)

5. <span data-ttu-id="8fb23-148">Hello dosya paylaşımı için bulut Kabuğu'nu seçin.</span><span class="sxs-lookup"><span data-stu-id="8fb23-148">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="8fb23-149">Merhaba adı deseni `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="8fb23-149">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Dosya paylaşımı seçme](./media/resource-manager-create-first-template/select-file-share.png)

6. <span data-ttu-id="8fb23-151">**Dizin ekle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="8fb23-151">Select **Add directory**.</span></span>

   ![Dizin ekleme](./media/resource-manager-create-first-template/select-add-directory.png)

7. <span data-ttu-id="8fb23-153">**Şablonlar** olarak adlandırıp **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="8fb23-153">Name it **templates**, and select **Okay**.</span></span>

   ![Ad dizini](./media/resource-manager-create-first-template/name-templates.png)

8. <span data-ttu-id="8fb23-155">Yeni dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="8fb23-155">Select your new directory.</span></span>

   ![Dizin seçme](./media/resource-manager-create-first-template/select-templates.png)

9. <span data-ttu-id="8fb23-157">**Karşıya Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="8fb23-157">Select **Upload**.</span></span>

   ![Karşıya yükleme seçme](./media/resource-manager-create-first-template/select-upload.png)

10. <span data-ttu-id="8fb23-159">Şablonunuzu bulup karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8fb23-159">Find and upload your template.</span></span>

   ![Dosya yükleme](./media/resource-manager-create-first-template/upload-files.png)

11. <span data-ttu-id="8fb23-161">Açık hello istemi.</span><span class="sxs-lookup"><span data-stu-id="8fb23-161">Open hello prompt.</span></span>

   ![Cloud Shell’i açma](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. <span data-ttu-id="8fb23-163">Merhaba bulut Kabuk komutları aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="8fb23-163">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

<span data-ttu-id="8fb23-164">Dağıtım tamamlandığında, depolama hesabınız hello kaynak grubunda yok.</span><span class="sxs-lookup"><span data-stu-id="8fb23-164">When deployment finishes, your storage account exists in hello resource group.</span></span>

## <a name="customize-hello-template"></a><span data-ttu-id="8fb23-165">Merhaba şablonunu özelleştirme</span><span class="sxs-lookup"><span data-stu-id="8fb23-165">Customize hello template</span></span>

<span data-ttu-id="8fb23-166">Merhaba şablonu düzgün çalışır, ancak esnek değildir.</span><span class="sxs-lookup"><span data-stu-id="8fb23-166">hello template works fine, but it is not flexible.</span></span> <span data-ttu-id="8fb23-167">Her zaman, yerel olarak yedekli depolama tooSouth Orta ABD dağıtır.</span><span class="sxs-lookup"><span data-stu-id="8fb23-167">It always deploys a locally redundant storage tooSouth Central US.</span></span> <span data-ttu-id="8fb23-168">Merhaba adıdır her zaman *depolama* bir karma değer tarafından izlenen.</span><span class="sxs-lookup"><span data-stu-id="8fb23-168">hello name is always *storage* followed by a hash value.</span></span> <span data-ttu-id="8fb23-169">farklı senaryolar için Hello şablonu kullanarak tooenable parametreleri toohello şablonu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8fb23-169">tooenable using hello template for different scenarios, add parameters toohello template.</span></span>

<span data-ttu-id="8fb23-170">Merhaba aşağıdaki örnekte iki parametrelerle hello Parametreler bölümünde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="8fb23-170">hello following example shows hello parameters section with two parameters.</span></span> <span data-ttu-id="8fb23-171">İlk parametre hello `storageSKU` toospecify hello türü artıklık sağlar.</span><span class="sxs-lookup"><span data-stu-id="8fb23-171">hello first parameter `storageSKU` enables you toospecify hello type of redundancy.</span></span> <span data-ttu-id="8fb23-172">Bir depolama hesabı için geçerli toovalues içinde geçirebilirsiniz hello değerleri sınırlar.</span><span class="sxs-lookup"><span data-stu-id="8fb23-172">It limits hello values you can pass in toovalues that are valid for a storage account.</span></span> <span data-ttu-id="8fb23-173">Ayrıca, varsayılan bir değer belirtir.</span><span class="sxs-lookup"><span data-stu-id="8fb23-173">It also specifies a default value.</span></span> <span data-ttu-id="8fb23-174">İkinci parametre hello `storageNamePrefix` en çok 11 karakter kümesi tooallow değil.</span><span class="sxs-lookup"><span data-stu-id="8fb23-174">hello second parameter `storageNamePrefix` is set tooallow a maximum of 11 characters.</span></span> <span data-ttu-id="8fb23-175">Varsayılan bir değer belirtir.</span><span class="sxs-lookup"><span data-stu-id="8fb23-175">It specifies a default value.</span></span>

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
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

<span data-ttu-id="8fb23-176">Adlı bir değişkende Hello değişkenler bölümünde eklemek `storageName`.</span><span class="sxs-lookup"><span data-stu-id="8fb23-176">In hello variables section, add a variable named `storageName`.</span></span> <span data-ttu-id="8fb23-177">Merhaba önek değeri hello parametrelerinden ve hello karma değerinden bir araya getiren [uniqueString](resource-group-template-functions-string.md#uniquestring) işlevi.</span><span class="sxs-lookup"><span data-stu-id="8fb23-177">It combines hello prefix value from hello parameters and a hash value from hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span> <span data-ttu-id="8fb23-178">Merhaba kullanan [toLower](resource-group-template-functions-string.md#tolower) tooconvert tüm karakterleri toolowercase işlev.</span><span class="sxs-lookup"><span data-stu-id="8fb23-178">It uses hello [toLower](resource-group-template-functions-string.md#tolower) function tooconvert all characters toolowercase.</span></span>

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

<span data-ttu-id="8fb23-179">toouse depolama hesabınız için yeni bu değerleri değiştirmek hello kaynak tanımı:</span><span class="sxs-lookup"><span data-stu-id="8fb23-179">toouse these new values for your storage account, change hello resource definition:</span></span>

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

<span data-ttu-id="8fb23-180">Bu hello fark hello depolama hesabının adını eklediğiniz toohello değişkeni şimdi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8fb23-180">Notice that hello name of hello storage account is now set toohello variable that you added.</span></span> <span data-ttu-id="8fb23-181">Merhaba SKU adı toohello hello parametresinin değerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8fb23-181">hello SKU name is set toohello value of hello parameter.</span></span> <span data-ttu-id="8fb23-182">Başlangıç konumu ayarlanmış hello hello kaynak grubu olarak aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="8fb23-182">hello location is set hello same location as hello resource group.</span></span>

<span data-ttu-id="8fb23-183">Dosyanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8fb23-183">Save your file.</span></span> 

<span data-ttu-id="8fb23-184">Bu makaledeki Hello adımları tamamladıktan sonra şablonunuzu artık şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="8fb23-184">After completing hello steps in this article, your template now looks like:</span></span>

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
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
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

## <a name="redeploy-template"></a><span data-ttu-id="8fb23-185">Şablonu yeniden dağıtma</span><span class="sxs-lookup"><span data-stu-id="8fb23-185">Redeploy template</span></span>

<span data-ttu-id="8fb23-186">Farklı değerleri olan Hello şablonu yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="8fb23-186">Redeploy hello template with different values.</span></span>

<span data-ttu-id="8fb23-187">PowerShell için şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8fb23-187">For PowerShell, use:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

<span data-ttu-id="8fb23-188">Azure CLI için şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8fb23-188">For Azure CLI, use:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

<span data-ttu-id="8fb23-189">Merhaba bulut Kabuk değiştirilmiş şablon toohello dosya paylaşımınızı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8fb23-189">For hello Cloud Shell, upload your changed template toohello file share.</span></span> <span data-ttu-id="8fb23-190">Merhaba varolan dosyanın üzerine yazar.</span><span class="sxs-lookup"><span data-stu-id="8fb23-190">Overwrite hello existing file.</span></span> <span data-ttu-id="8fb23-191">Ardından, komutu aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="8fb23-191">Then, use hello following command:</span></span>

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a><span data-ttu-id="8fb23-192">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="8fb23-192">Clean up resources</span></span>

<span data-ttu-id="8fb23-193">Artık gerektiğinde Merhaba kaynak grubunu silerek dağıtılan hello kaynakları temizlemek.</span><span class="sxs-lookup"><span data-stu-id="8fb23-193">When no longer needed, clean up hello resources you deployed by deleting hello resource group.</span></span>

<span data-ttu-id="8fb23-194">PowerShell için şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8fb23-194">For PowerShell, use:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

<span data-ttu-id="8fb23-195">Azure CLI için şunu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8fb23-195">For Azure CLI, use:</span></span>

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a><span data-ttu-id="8fb23-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8fb23-196">Next steps</span></span>
* <span data-ttu-id="8fb23-197">bir şablonun hello yapısı hakkında daha fazla toolearn bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="8fb23-197">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="8fb23-198">bir depolama hesabı hello özellikleri hakkında toolearn bkz [depolama hesapları şablon başvurusu](/azure/templates/microsoft.storage/storageaccounts).</span><span class="sxs-lookup"><span data-stu-id="8fb23-198">toolearn about hello properties for a storage account, see [storage accounts template reference](/azure/templates/microsoft.storage/storageaccounts).</span></span>
* <span data-ttu-id="8fb23-199">tooview tam şablonları farklı türlerde çözümler için bkz: hello [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="8fb23-199">tooview complete templates for many different types of solutions, see hello [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/).</span></span>
