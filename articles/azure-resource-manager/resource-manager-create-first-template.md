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
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a>İlk Azure Resource Manager şablonunuzu oluşturma ve dağıtma
Bu konu, ilk Azure Resource Manager şablonu oluşturma hello adımlarda size yol gösterir. Resource Manager şablonları çözümünüz için toodeploy ihtiyacınız hello kaynakları tanımlayan JSON dosyalarıdır. Azure çözümlerinizi yönetme ve dağıtma ile ilişkili toounderstand hello bkz [Azure Resource Manager'a genel bakış](resource-group-overview.md). Mevcut bir kaynağı var ve bu kaynakları için tooget bir şablon istiyorsanız, bkz [mevcut kaynaklardan Azure Resource Manager şablonunu dışarı aktarma](resource-manager-export-template.md).

toocreate ve gözden geçirme şablonları, JSON düzenleyicisinin gerekir. [Visual Studio Code](https://code.visualstudio.com/) basit, açık kaynaklı ve platformlar arası bir kod düzenleyicisidir. Resource Manager şablonları oluşturmak için Visual Studio Code kullanılması önerilir. Bu konu başlığı, VS Code kullandığınızı varsayar; ancak başka bir JSON düzenleyiciniz (Visual Studio gibi) varsa kullanabilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

* Visual Studio Code. Gerekirse, [https://code.visualstudio.com/](https://code.visualstudio.com/) adresinden yükleyin.
* Azure aboneliği. Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

## <a name="create-template"></a>Şablon oluşturma

Bir depolama hesabı tooyour aboneliği dağıtır basit bir şablonla başlayalım.

1. **Dosya** > **Yeni Dosya**’yı seçin. 

   ![Yeni dosya](./media/resource-manager-create-first-template/new-file.png)

2. Kopyalama ve yapıştırma dosyanıza JSON söz dizimi aşağıdaki hello:

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

   Depolama hesabı adları zor tooset olun birkaç kısıtlamaları vardır. Merhaba adı uzunluğu, kullanım yalnızca sayılar ve küçük harfler 3 ile 24 karakter arasında olmalı ve benzersiz olması gerekir. Merhaba önceki şablonu kullanan hello [uniqueString](resource-group-template-functions-string.md#uniquestring) toogenerate bir karma değer işlev. toogive Bu karma değer daha anlamına gelir, hello önekini ekler *depolama*. 

3. Bu dosya olarak kaydetmek **azuredeploy.json** tooa yerel klasör.

   ![Şablonu kaydetme](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a>Şablon dağıtma

Bu şablonu hazır toodeploy şunlardır. PowerShell veya Azure CLI toocreate bir kaynak grubu kullanın. Ardından, bir depolama hesabı toothat kaynak grubu dağıtın.

* İçin PowerShell komutlarını hello şablonu içeren hello klasöründen aşağıdaki hello kullanın:

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* Azure CLI yerel yükleme için komutları hello şablonu içeren hello klasöründen aşağıdaki hello kullan:

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

Dağıtım tamamlandığında, depolama hesabınız hello kaynak grubunda yok.

## <a name="deploy-template-from-cloud-shell"></a>Cloud Shell'den şablon dağıtma

Kullanabileceğiniz [bulut Kabuk](../cloud-shell/overview.md) toorun hello Azure CLI komutları şablonunuzu dağıtmak için. Ancak, ilk şablonunuzu hello dosya paylaşım içine bulut Kabuğunuzu yüklemeniz gerekir. Daha önce Cloud Shell kullanmadıysanız, kurulumu hakkında bilgi için bkz. [Azure Cloud Shell’e Genel Bakış](../cloud-shell/overview.md).

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).   

2. Cloud Shell kaynak grubunuzu seçin. Merhaba adı deseni `cloud-shell-storage-<region>`.

   ![Kaynak grubu seçin](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. Bulut Kabuğunuzu Hello depolama hesabı seçin.

   ![Depolama hesabı seçme](./media/resource-manager-create-first-template/select-storage.png)

4. **Dosyalar**’ı seçin.

   ![Dosya seçme](./media/resource-manager-create-first-template/select-files.png)

5. Hello dosya paylaşımı için bulut Kabuğu'nu seçin. Merhaba adı deseni `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Dosya paylaşımı seçme](./media/resource-manager-create-first-template/select-file-share.png)

6. **Dizin ekle**’yi seçin.

   ![Dizin ekleme](./media/resource-manager-create-first-template/select-add-directory.png)

7. **Şablonlar** olarak adlandırıp **Tamam**’ı seçin.

   ![Ad dizini](./media/resource-manager-create-first-template/name-templates.png)

8. Yeni dizininizi seçin.

   ![Dizin seçme](./media/resource-manager-create-first-template/select-templates.png)

9. **Karşıya Yükle**’yi seçin.

   ![Karşıya yükleme seçme](./media/resource-manager-create-first-template/select-upload.png)

10. Şablonunuzu bulup karşıya yükleyin.

   ![Dosya yükleme](./media/resource-manager-create-first-template/upload-files.png)

11. Açık hello istemi.

   ![Cloud Shell’i açma](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. Merhaba bulut Kabuk komutları aşağıdaki hello girin:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

Dağıtım tamamlandığında, depolama hesabınız hello kaynak grubunda yok.

## <a name="customize-hello-template"></a>Merhaba şablonunu özelleştirme

Merhaba şablonu düzgün çalışır, ancak esnek değildir. Her zaman, yerel olarak yedekli depolama tooSouth Orta ABD dağıtır. Merhaba adıdır her zaman *depolama* bir karma değer tarafından izlenen. farklı senaryolar için Hello şablonu kullanarak tooenable parametreleri toohello şablonu ekleyin.

Merhaba aşağıdaki örnekte iki parametrelerle hello Parametreler bölümünde gösterilir. İlk parametre hello `storageSKU` toospecify hello türü artıklık sağlar. Bir depolama hesabı için geçerli toovalues içinde geçirebilirsiniz hello değerleri sınırlar. Ayrıca, varsayılan bir değer belirtir. İkinci parametre hello `storageNamePrefix` en çok 11 karakter kümesi tooallow değil. Varsayılan bir değer belirtir.

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

Adlı bir değişkende Hello değişkenler bölümünde eklemek `storageName`. Merhaba önek değeri hello parametrelerinden ve hello karma değerinden bir araya getiren [uniqueString](resource-group-template-functions-string.md#uniquestring) işlevi. Merhaba kullanan [toLower](resource-group-template-functions-string.md#tolower) tooconvert tüm karakterleri toolowercase işlev.

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

toouse depolama hesabınız için yeni bu değerleri değiştirmek hello kaynak tanımı:

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

Bu hello fark hello depolama hesabının adını eklediğiniz toohello değişkeni şimdi ayarlayın. Merhaba SKU adı toohello hello parametresinin değerini ayarlayın. Başlangıç konumu ayarlanmış hello hello kaynak grubu olarak aynı konumu.

Dosyanızı kaydedin. 

Bu makaledeki Hello adımları tamamladıktan sonra şablonunuzu artık şuna benzer:

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

## <a name="redeploy-template"></a>Şablonu yeniden dağıtma

Farklı değerleri olan Hello şablonu yeniden dağıtın.

PowerShell için şunu kullanın:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

Azure CLI için şunu kullanın:

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

Merhaba bulut Kabuk değiştirilmiş şablon toohello dosya paylaşımınızı karşıya yükleyin. Merhaba varolan dosyanın üzerine yazar. Ardından, komutu aşağıdaki hello kullanın:

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a>Kaynakları temizleme

Artık gerektiğinde Merhaba kaynak grubunu silerek dağıtılan hello kaynakları temizlemek.

PowerShell için şunu kullanın:

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

Azure CLI için şunu kullanın:

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a>Sonraki adımlar
* bir şablonun hello yapısı hakkında daha fazla toolearn bkz [Azure Resource Manager şablonları yazma](resource-group-authoring-templates.md).
* bir depolama hesabı hello özellikleri hakkında toolearn bkz [depolama hesapları şablon başvurusu](/azure/templates/microsoft.storage/storageaccounts).
* tooview tam şablonları farklı türlerde çözümler için bkz: hello [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/documentation/templates/).
