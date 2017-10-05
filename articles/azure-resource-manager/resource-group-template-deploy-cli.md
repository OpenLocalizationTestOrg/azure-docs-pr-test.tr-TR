---
title: "Azure CLI ve şablon kaynaklarla dağıtma | Microsoft Docs"
description: "Bir kaynakları Azure'a dağıtmak için Azure Resource Manager ve Azure CLI kullanın. Kaynaklar, bir Resource Manager şablonunda tanımlanır."
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
ms.openlocfilehash: 4f1d5f4cc48470f8906edb28628006dd1996bd3a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a><span data-ttu-id="e7a04-104">Kaynakları Resource Manager şablonları ve Azure CLI ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="e7a04-104">Deploy resources with Resource Manager templates and Azure CLI</span></span>

<span data-ttu-id="e7a04-105">Bu konu Azure CLI 2.0 Resource Manager şablonları ile kaynakları Azure'a dağıtmak için nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="e7a04-105">This topic explains how to use Azure CLI 2.0 with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="e7a04-106">Dağıtma ile ilgili kavramları hakkında bilgi sahibi değilseniz ve Azure çözümlerinizi bkz [Azure Resource Manager'a genel bakış](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7a04-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>  

<span data-ttu-id="e7a04-107">Resource Manager şablonu ya da makinenizde yerel bir dosya ya da GitHub gibi bir havuzda bulunan dış dosyası dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7a04-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="e7a04-108">Bu makalede dağıttığınız şablonu kullanılabilir [örnek şablonu](#sample-template) bölümünde, ya da farklı bir [depolama hesabı şablonu github](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="e7a04-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as a [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

<span data-ttu-id="e7a04-109">Azure CLI yüklenmiş yoksa kullanabileceğiniz [bulut Kabuk](#deploy-template-from-cloud-shell).</span><span class="sxs-lookup"><span data-stu-id="e7a04-109">If you do not have Azure CLI installed, you can use the [Cloud Shell](#deploy-template-from-cloud-shell).</span></span>

## <a name="deploy-local-template"></a><span data-ttu-id="e7a04-110">Yerel şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="e7a04-110">Deploy local template</span></span>

<span data-ttu-id="e7a04-111">Kaynakları Azure'a dağıtırken:</span><span class="sxs-lookup"><span data-stu-id="e7a04-111">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="e7a04-112">Azure hesabınızda oturum açın</span><span class="sxs-lookup"><span data-stu-id="e7a04-112">Log in to your Azure account</span></span>
2. <span data-ttu-id="e7a04-113">Dağıtılan kaynaklar için kapsayıcı görevi gören bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e7a04-113">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="e7a04-114">Kaynak grubu adı yalnızca alfasayısal karakterler, nokta, alt çizgi, kısa çizgi ve parantez içerebilir.</span><span class="sxs-lookup"><span data-stu-id="e7a04-114">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="e7a04-115">En fazla 90 karakter olabilir.</span><span class="sxs-lookup"><span data-stu-id="e7a04-115">It can be up to 90 characters.</span></span> <span data-ttu-id="e7a04-116">Bir nokta ile bitemez.</span><span class="sxs-lookup"><span data-stu-id="e7a04-116">It cannot end in a period.</span></span>
3. <span data-ttu-id="e7a04-117">Kaynak grubu oluşturmak için kaynakları tanımlayan şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="e7a04-117">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="e7a04-118">Bir şablon dağıtımı özelleştirmenize olanak sağlayan parametreler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="e7a04-118">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="e7a04-119">Örneğin, belirli bir ortamda (örneğin, geliştirme, test ve üretim) için uyarlanabilir değerler sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7a04-119">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="e7a04-120">Örnek şablon SKU depolama hesabı için bir parametre tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e7a04-120">The sample template defines a parameter for the storage account SKU.</span></span> 

<span data-ttu-id="e7a04-121">Aşağıdaki örnek, bir kaynak grubu oluşturur ve yerel makinenize bir şablondan dağıtır:</span><span class="sxs-lookup"><span data-stu-id="e7a04-121">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="e7a04-122">Dağıtımın tamamlanması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="e7a04-122">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="e7a04-123">Tamamlandığında, sonuç içeren bir ileti görür:</span><span class="sxs-lookup"><span data-stu-id="e7a04-123">When it finishes, you see a message that includes the result:</span></span>

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a><span data-ttu-id="e7a04-124">Dış şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="e7a04-124">Deploy external template</span></span>

<span data-ttu-id="e7a04-125">Resource Manager şablonları yerel makinenizde depolamak yerine bir dış konuma depolamak tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7a04-125">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="e7a04-126">Şablonları bir kaynak denetimi deponuza (örneğin, GitHub) depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7a04-126">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="e7a04-127">Veya, bunları paylaşılan erişim için bir Azure depolama hesabı, kuruluşunuzda depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7a04-127">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="e7a04-128">Dış bir şablonu dağıtmak için kullandığınız **şablonu URI** parametresi.</span><span class="sxs-lookup"><span data-stu-id="e7a04-128">To deploy an external template, use the **template-uri** parameter.</span></span> <span data-ttu-id="e7a04-129">URI örnekte github'dan örnek şablonu dağıtmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e7a04-129">Use the URI in the example to deploy the sample template from GitHub.</span></span>
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

<span data-ttu-id="e7a04-130">Önceki örnekte şablonunuzu hassas bir veri içermemesi çünkü çoğu senaryo için çalışır ve şablona için genel olarak erişilebilir bir URI gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e7a04-130">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="e7a04-131">Hassas veriler (örneğin, bir yönetici parolası) belirtmeniz gerekiyorsa, bu değeri güvenli bir parametre olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="e7a04-131">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="e7a04-132">Ancak, şablonunuzu genel olarak erişilebilir olmasını istemiyorsanız, bir özel depolama kapsayıcısı depolayarak koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7a04-132">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="e7a04-133">Bir paylaşılan erişim imzası (SAS) belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="e7a04-133">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>

## <a name="deploy-template-from-cloud-shell"></a><span data-ttu-id="e7a04-134">Cloud Shell'den şablon dağıtma</span><span class="sxs-lookup"><span data-stu-id="e7a04-134">Deploy template from Cloud Shell</span></span>

<span data-ttu-id="e7a04-135">[Cloud Shell](../cloud-shell/overview.md)’i kullanarak, şablonunuzu dağıtmak için Azure CLI komutlarını çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e7a04-135">You can use [Cloud Shell](../cloud-shell/overview.md) to run the Azure CLI commands for deploying your template.</span></span> <span data-ttu-id="e7a04-136">Ancak, ilk olarak şablonunuzu Cloud Shell dosya paylaşımına yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e7a04-136">However, you must first load your template into the file share for your Cloud Shell.</span></span> <span data-ttu-id="e7a04-137">Daha önce Cloud Shell kullanmadıysanız, kurulumu hakkında bilgi için bkz. [Azure Cloud Shell’e Genel Bakış](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7a04-137">If you have not used Cloud Shell, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md) for information about setting it up.</span></span>

1. <span data-ttu-id="e7a04-138">[Azure Portal](https://portal.azure.com)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e7a04-138">Log in to the [Azure portal](https://portal.azure.com).</span></span>   

2. <span data-ttu-id="e7a04-139">Cloud Shell kaynak grubunuzu seçin.</span><span class="sxs-lookup"><span data-stu-id="e7a04-139">Select your Cloud Shell resource group.</span></span> <span data-ttu-id="e7a04-140">Ad deseni `cloud-shell-storage-<region>` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="e7a04-140">The name pattern is `cloud-shell-storage-<region>`.</span></span>

   ![Kaynak grubu seçin](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. <span data-ttu-id="e7a04-142">Cloud Shell için depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="e7a04-142">Select the storage account for your Cloud Shell.</span></span>

   ![Depolama hesabı seçme](./media/resource-group-template-deploy-cli/select-storage.png)

4. <span data-ttu-id="e7a04-144">**Dosyalar**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e7a04-144">Select **Files**.</span></span>

   ![Dosya seçme](./media/resource-group-template-deploy-cli/select-files.png)

5. <span data-ttu-id="e7a04-146">Cloud Shell için dosya paylaşımı seçin.</span><span class="sxs-lookup"><span data-stu-id="e7a04-146">Select the file share for Cloud Shell.</span></span> <span data-ttu-id="e7a04-147">Ad deseni `cs-<user>-<domain>-com-<uniqueGuid>` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="e7a04-147">The name pattern is `cs-<user>-<domain>-com-<uniqueGuid>`.</span></span>

   ![Dosya paylaşımı seçme](./media/resource-group-template-deploy-cli/select-file-share.png)

6. <span data-ttu-id="e7a04-149">**Dizin ekle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e7a04-149">Select **Add directory**.</span></span>

   ![Dizin ekleme](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. <span data-ttu-id="e7a04-151">**Şablonlar** olarak adlandırıp **Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e7a04-151">Name it **templates**, and select **Okay**.</span></span>

   ![Ad dizini](./media/resource-group-template-deploy-cli/name-templates.png)

8. <span data-ttu-id="e7a04-153">Yeni dizininizi seçin.</span><span class="sxs-lookup"><span data-stu-id="e7a04-153">Select your new directory.</span></span>

   ![Dizin seçme](./media/resource-group-template-deploy-cli/select-templates.png)

9. <span data-ttu-id="e7a04-155">**Karşıya Yükle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e7a04-155">Select **Upload**.</span></span>

   ![Karşıya yükleme seçme](./media/resource-group-template-deploy-cli/select-upload.png)

10. <span data-ttu-id="e7a04-157">Şablonunuzu bulup karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="e7a04-157">Find and upload your template.</span></span>

   ![Dosya yükleme](./media/resource-group-template-deploy-cli/upload-files.png)

11. <span data-ttu-id="e7a04-159">İstemi açın.</span><span class="sxs-lookup"><span data-stu-id="e7a04-159">Open the prompt.</span></span>

   ![Cloud Shell’i açma](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. <span data-ttu-id="e7a04-161">Cloud Shell’e aşağıdaki komutları girin:</span><span class="sxs-lookup"><span data-stu-id="e7a04-161">Enter the following commands in the Cloud Shell:</span></span>

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

## <a name="parameter-files"></a><span data-ttu-id="e7a04-162">Parametre dosyaları</span><span class="sxs-lookup"><span data-stu-id="e7a04-162">Parameter files</span></span>

<span data-ttu-id="e7a04-163">Satır içi değerler olarak komut parametreleri geçirme yerine parametre değerlerini içeren bir JSON dosyası kullanmak daha kolay.</span><span class="sxs-lookup"><span data-stu-id="e7a04-163">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="e7a04-164">Parametre dosyası şu biçimde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="e7a04-164">The parameter file must be in the following format:</span></span>

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

<span data-ttu-id="e7a04-165">Parametreler bölümünde şablonunuzda (storageAccountType) tanımlanan parametre eşleşen bir parametre adı içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e7a04-165">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="e7a04-166">Parametre dosyası parametresi için bir değer içerir.</span><span class="sxs-lookup"><span data-stu-id="e7a04-166">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="e7a04-167">Bu değer, dağıtım sırasında şablona otomatik olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="e7a04-167">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="e7a04-168">Farklı dağıtım senaryoları için birden çok parametre dosyası oluşturun ve ardından uygun parametre dosyası geçirin.</span><span class="sxs-lookup"><span data-stu-id="e7a04-168">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="e7a04-169">Önceki örnekte kopyalayın ve adlı bir dosya kaydedin `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="e7a04-169">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="e7a04-170">Bir yerel parametre dosyası geçirmek için kullanmak `@` storage.parameters.json adlı bir yerel dosya belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="e7a04-170">To pass a local parameter file, use `@` to specify a local file named storage.parameters.json.</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a><span data-ttu-id="e7a04-171">Şablon dağıtımı test etme</span><span class="sxs-lookup"><span data-stu-id="e7a04-171">Test a template deployment</span></span>

<span data-ttu-id="e7a04-172">Herhangi bir kaynağa dağıtmadan şablonu ve parametre değerlerini sınamak için kullanın [az grup dağıtımı doğrulamak](/cli/azure/group/deployment#validate).</span><span class="sxs-lookup"><span data-stu-id="e7a04-172">To test your template and parameter values without actually deploying any resources, use [az group deployment validate](/cli/azure/group/deployment#validate).</span></span> 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

<span data-ttu-id="e7a04-173">Hiçbir hata algılanırsa, komut sınama dağıtımı hakkında bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="e7a04-173">If no errors are detected, the command returns information about the test deployment.</span></span> <span data-ttu-id="e7a04-174">Özellikle dikkat **hata** değeri NULL'dur.</span><span class="sxs-lookup"><span data-stu-id="e7a04-174">In particular, notice that the **error** value is null.</span></span>

```azurecli
{
  "error": null,
  "properties": {
      ...
```

<span data-ttu-id="e7a04-175">Bir hata algılandığında, komutu bir hata iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="e7a04-175">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="e7a04-176">Örneğin, SKU, depolama hesabı için hatalı bir değer geçirmek çalışılırken aşağıdaki hata döndürür:</span><span class="sxs-lookup"><span data-stu-id="e7a04-176">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'The provided value 'badSKU' for the template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. The parameter value is not part of the allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

<span data-ttu-id="e7a04-177">Şablonunuzun söz dizimi hatası varsa, komut şablon ayrıştırılamadı belirten bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="e7a04-177">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="e7a04-178">İleti satır numarası ve ayrıştırma hatası konumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="e7a04-178">The message indicates the line number and position of the parsing error.</span></span>

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

<span data-ttu-id="e7a04-179">Tam modu kullanmak için `mode` parametre:</span><span class="sxs-lookup"><span data-stu-id="e7a04-179">To use complete mode, use the `mode` parameter:</span></span>

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

## <a name="sample-template"></a><span data-ttu-id="e7a04-180">Örnek şablonu</span><span class="sxs-lookup"><span data-stu-id="e7a04-180">Sample template</span></span>

<span data-ttu-id="e7a04-181">Aşağıdaki şablonu, bu konudaki örnekler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e7a04-181">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="e7a04-182">Kopyalayın ve storage.json adlı bir dosya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e7a04-182">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="e7a04-183">Bu şablonun nasıl oluşturulacağını anlamak için bkz: [, ilk Azure Resource Manager şablonu oluşturma](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="e7a04-183">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="e7a04-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e7a04-184">Next steps</span></span>
* <span data-ttu-id="e7a04-185">Bu makaledeki örneklerde kaynakları varsayılan aboneliğinizde bir kaynak grubuna dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e7a04-185">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="e7a04-186">Farklı bir abonelik kullanmak için bkz: [birden çok Azure Aboneliklerini yönetmek](/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e7a04-186">To use a different subscription, see [Manage multiple Azure subscriptions](/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>
* <span data-ttu-id="e7a04-187">Bir şablon dağıtan bir tam örnek betik için bkz: [Resource Manager şablonu dağıtım betiği](resource-manager-samples-cli-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e7a04-187">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-cli-deploy.md).</span></span>
* <span data-ttu-id="e7a04-188">Şablonunuzda parametrelerini tanımlamak nasıl anlamak için bkz: [yapısı ve Azure Resource Manager şablonları sözdizimini anlamanız](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e7a04-188">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e7a04-189">Genel dağıtım hatalarını giderme ipuçları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="e7a04-189">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="e7a04-190">Bir SAS belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-cli-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="e7a04-190">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-cli-sas-token.md).</span></span>
* <span data-ttu-id="e7a04-191">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="e7a04-191">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
