---
title: "Azure CLI ve şablon aaaDeploy kaynaklarla | Microsoft Docs"
description: "Azure Resource Manager ve Azure CLI toodeploy kaynakları tooAzure kullanın. Merhaba kaynaklar bir Resource Manager şablonunda tanımlanır."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="c221f-104">Kaynakları Resource Manager şablonları ve Azure CLI ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="c221f-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="c221f-105">Bu konuda açıklanmaktadır nasıl toouse Azure CLI 2.0 Resource Manager şablonları toodeploy ile kaynakları tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c221f-105">This topic explains how toouse Azure CLI 2.0 with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="c221f-106">Dağıtma hello kavramları hakkında bilgi sahibi değilseniz ve Azure çözümlerinizi bkz [Azure Resource Manager'a genel bakış](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c221f-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="c221f-107">Merhaba Resource Manager şablonu ya da makinenizde yerel bir dosya ya da GitHub gibi bir havuzda bulunan dış dosyası dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c221f-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="c221f-108">Bu makalede dağıttığınız hello şablon hello kullanılabilir [örnek şablonu](#sample-template) bölümünde, ya da farklı bir [depolama hesabı şablonu github](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="c221f-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="c221f-109">Azure CLI yüklenmiş yoksa hello kullanabilirsiniz [bulut Kabuk](#deploy-template-from-cloud-shell).</span><span class="sxs-lookup"><span data-stu-id="c221f-109">If you do not have Azure CLI installed, you can use hello [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="c221f-110">Yerel şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="c221f-110">Deploy local template</span></span>

<span data-ttu-id="c221f-111">Kaynakları tooAzure dağıtırken:</span><span class="sxs-lookup"><span data-stu-id="c221f-111">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="c221f-112">Azure hesabı tooyour içinde oturum</span><span class="sxs-lookup"><span data-stu-id="c221f-112">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="c221f-113">Dağıtılan hello kaynaklar için hello kapsayıcı görevi gören bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c221f-113">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="c221f-114">Hello hello kaynak grubu adı yalnızca alfasayısal karakterler, nokta, alt çizgi, kısa çizgi ve parantez içerebilir.</span><span class="sxs-lookup"><span data-stu-id="c221f-114">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="c221f-115">Too90 karakter olabilir.</span><span class="sxs-lookup"><span data-stu-id="c221f-115">It can be up too90 characters.</span></span> <span data-ttu-id="c221f-116">Bir nokta ile bitemez.</span><span class="sxs-lookup"><span data-stu-id="c221f-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="c221f-117">Merhaba kaynakları toocreate tanımlar toohello kaynak grubu hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="c221f-117">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="c221f-118">Bir şablon toocustomize hello dağıtımını etkinleştirmek parametreleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="c221f-118">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="c221f-119">Örneğin, belirli bir ortamda (örneğin, geliştirme, test ve üretim) için uyarlanabilir değerler sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c221f-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="c221f-120">Merhaba örnek şablonu hello depolama hesabı SKU için bir parametre tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c221f-120">hello sample template defines a parameter for hello storage account SKU.</span></span> 

<span data-ttu-id="c221f-121">Aşağıdaki örnek hello bir kaynak grubu oluşturur ve yerel makinenize bir şablondan dağıtır:</span><span class="sxs-lookup"><span data-stu-id="c221f-121">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="c221f-122">Merhaba dağıtım birkaç dakika toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="c221f-122">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="c221f-123">Tamamlandığında, hello sonuç içeren bir ileti görür:</span><span class="sxs-lookup"><span data-stu-id="c221f-123">When it finishes, you see a message that includes hello result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="c221f-124">Dış şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="c221f-124">Deploy external template</span></span>

<span data-ttu-id="c221f-125">Resource Manager şablonları yerel makinenizde depolamak yerine toostore tercih edebilirsiniz harici bir konumda bunları.</span><span class="sxs-lookup"><span data-stu-id="c221f-125">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="c221f-126">Şablonları bir kaynak denetimi deponuza (örneğin, GitHub) depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c221f-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="c221f-127">Veya, bunları paylaşılan erişim için bir Azure depolama hesabı, kuruluşunuzda depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c221f-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="c221f-128">toodeploy dış bir şablonu kullanmak hello **şablonu URI** parametresi.</span><span class="sxs-lookup"><span data-stu-id="c221f-128">toodeploy an external template, use hello **template-uri** parameter.</span></span> <span data-ttu-id="c221f-129">Merhaba örnek toodeploy hello örnek şablonunu github'dan Hello URI kullanın.</span><span class="sxs-lookup"><span data-stu-id="c221f-129">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="c221f-130">Merhaba önceki örnekte genel olarak erişilebilir bir URI şablonunuzu hassas bir veri içermemesi çünkü çoğu senaryo için çalışır hello şablonu için gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c221f-130">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="c221f-131">Toospecify hassas verileri (örneğin, bir yönetici parolası) gerekiyorsa, bu değeri güvenli bir parametre olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="c221f-131">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="c221f-132">Ancak, şablon toobe genel olarak erişilebilir istemiyorsanız, bir özel depolama kapsayıcısı depolayarak koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c221f-132">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="c221f-133">Bir paylaşılan erişim imzası (SAS) belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="c221f-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="c221f-134">Cloud Shell'den şablon dağıtma</span><span class="sxs-lookup"><span data-stu-id="c221f-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="c221f-135">Kullanabileceğiniz [bulut Kabuk](../cloud-shell/overview.md) toorun hello Azure CLI komutları şablonunuzu dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="c221f-135">You can use [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="c221f-136">Ancak, ilk şablonunuzu hello dosya paylaşım içine bulut Kabuğunuzu yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c221f-136">However, you must first load your template into hello file share for your Cloud Shell.</span></span> <span data-ttu-id="c221f-137">Daha önce Cloud Shell kullanmadıysanız, kurulumu hakkında bilgi için bkz. [Azure Cloud Shell’e Genel Bakış](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="c221f-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="c221f-138">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c221f-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="c221f-139">Cloud Shell kaynak grubunuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="c221f-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="c221f-140">Merhaba adı deseni `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="c221f-140">hello name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Kaynak grubu seçin](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="c221f-142">Bulut Kabuğunuzu Hello depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="c221f-142">Select hello storage account for your Cloud Shell.</span></span>

   ![Depolama hesabı seçme](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="c221f-144">**Dosyalar**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="c221f-144">Select **Files**.</span></span>

   ![Dosya seçme](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="c221f-146">Hello dosya paylaşımı için bulut Kabuğu'nu seçin.</span><span class="sxs-lookup"><span data-stu-id="c221f-146">Select hello file share for Cloud Shell.</span></span> <span data-ttu-id="c221f-147">Merhaba adı deseni `cs-<user>-<domain>-com-<uniqueGuid>`.</span><span class="sxs-lookup"><span data-stu-id="c221f-147">hello name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Dosya paylaşımı seçme](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="c221f-149">**Dizin ekle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="c221f-149">Select **Add directory**.</span></span>

   ![Dizin ekleme](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="c221f-151">**Şablonlar** olarak adlandırıp **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="c221f-151">Name it **templates**, and select **Okay**.</span></span>

   ![Ad dizini](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="c221f-153">Yeni dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="c221f-153">Select your new directory.</span></span>

   ![Dizin seçme](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="c221f-155">**Karşıya Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="c221f-155">Select **Upload**.</span></span>

   ![Karşıya yükleme seçme](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="c221f-157">Şablonunuzu bulup karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c221f-157">Find and upload your template.</span></span>

   ![Dosya yükleme](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="c221f-159">Açık hello istemi.</span><span class="sxs-lookup"><span data-stu-id="c221f-159">Open hello prompt.</span></span>

   ![Cloud Shell’i açma](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="c221f-161">Merhaba bulut Kabuk komutları aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="c221f-161">Enter hello following commands in hello Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="c221f-162">Parametre dosyaları</span><span class="sxs-lookup"><span data-stu-id="c221f-162">Parameter files</span></span>

<span data-ttu-id="c221f-163">Satır içi değerler olarak komut parametreleri geçirme yerine daha kolay toouse hello parametre değerlerini içeren bir JSON dosyası bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c221f-163">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="c221f-164">Merhaba parametre dosyası biçimini izleyen hello olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="c221f-164">hello parameter file must be in hello following format:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

<span data-ttu-id="c221f-165">Merhaba Parametreler bölümünde şablonunuzda (storageAccountType) tanımlı hello parametresi ile eşleşen bir parametre adı içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c221f-165">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="c221f-166">Merhaba parametre dosyası hello parametresi için bir değer içerir.</span><span class="sxs-lookup"><span data-stu-id="c221f-166">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="c221f-167">Bu değer, dağıtım sırasında toohello şablonu otomatik olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="c221f-167">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="c221f-168">Farklı dağıtım senaryoları için birden çok parametre dosyası oluşturun ve hello uygun parametre dosyası geçirin.</span><span class="sxs-lookup"><span data-stu-id="c221f-168">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="c221f-169">Örnek önceki hello kopyalayın ve adlı bir dosya kaydedin `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="c221f-169">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="c221f-170">toopass yerel parametre dosyası kullanmak `@` toospecify storage.parameters.json adlı bir yerel dosya.</span><span class="sxs-lookup"><span data-stu-id="c221f-170">toopass a local parameter file, use `@` toospecify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="c221f-171">Şablon dağıtımı test etme</span><span class="sxs-lookup"><span data-stu-id="c221f-171">Test a template deployment</span></span>

<span data-ttu-id="c221f-172">herhangi bir kaynağa gerçekte dağıtımı olmadan şablonu ve parametre değerlerini tootest kullanmak [az grup dağıtımı doğrulamak](/cli/azure/group/deployment#validate).</span><span class="sxs-lookup"><span data-stu-id="c221f-172">tootest your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="c221f-173">Hiçbir hata algılanırsa, hello komut hello sınama dağıtımı hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="c221f-173">If no errors are detected, hello command returns information about hello test deployment.</span></span> <span data-ttu-id="c221f-174">Özellikle, bu hello fark **hata** değeri NULL'dur.</span><span class="sxs-lookup"><span data-stu-id="c221f-174">In particular, notice that hello **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="c221f-175">Bir hata algılandığında, hello komutu bir hata iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="c221f-175">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="c221f-176">Örneğin, toopass hello depolama hesabının SKU, yanlış bir değere çalışırken aşağıdaki hata hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="c221f-176">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

<span data-ttu-id="c221f-177">Şablonunuzun söz dizimi hatası varsa, hello komut hello şablon ayrıştırılamadı belirten bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="c221f-177">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="c221f-178">Merhaba iletisi hello satır numarasını ve ayrıştırma hatası hello konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="c221f-178">hello message indicates hello line number and position of hello parsing error.</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="c221f-179">toouse tam modu, kullanım hello `mode` parametre:</span><span class="sxs-lookup"><span data-stu-id="c221f-179">toouse complete mode, use hello `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="c221f-180">Örnek şablonu</span><span class="sxs-lookup"><span data-stu-id="c221f-180">Sample template</span></span>

<span data-ttu-id="c221f-181">Merhaba aşağıdaki şablonu bu konudaki hello örnekleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c221f-181">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="c221f-182">Kopyalayın ve storage.json adlı bir dosya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c221f-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="c221f-183">toounderstand nasıl toocreate bu şablonu bkz [, ilk Azure Resource Manager şablonu oluşturma](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="c221f-183">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="c221f-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c221f-184">Next steps</span></span>
* <span data-ttu-id="c221f-185">Bu makaledeki örneklerde Hello varsayılan aboneliğinizin kaynakları tooa kaynak grubuna dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c221f-185">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="c221f-186">toouse farklı bir abonelik bkz [birden çok Azure Aboneliklerini yönetmek](/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c221f-186">toouse a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="c221f-187">Bir şablon dağıtan bir tam örnek betik için bkz: [Resource Manager şablonu dağıtım betiği](resource-manager-samples-cli-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c221f-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="c221f-188">şablonunuzu toodefine parametrelerinde nasıl görürüm toounderstand [anlamak hello yapısı ve Azure Resource Manager şablonları sözdizimini](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c221f-188">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c221f-189">Genel dağıtım hatalarını giderme ipuçları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="c221f-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="c221f-190">Bir SAS belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="c221f-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="c221f-191">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="c221f-191">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
