---
title: "PowerShell ve şablon kaynaklarla dağıtma | Microsoft Docs"
description: "Azure Resource Manager ve Azure PowerShell bir kaynakları Azure'a dağıtmak için kullanın. Kaynaklar, bir Resource Manager şablonunda tanımlanır."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 5f395abf8ebdfbac18fd17d8183b392673e280ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="a4811-104">Kaynakları Resource Manager şablonları ve Azure PowerShell ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="a4811-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="a4811-105">Bu konu Azure PowerShell'i Resource Manager şablonları ile kaynakları Azure'a dağıtmak için nasıl kullanılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="a4811-105">This topic explains how to use Azure PowerShell with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="a4811-106">Dağıtma ile ilgili kavramları hakkında bilgi sahibi değilseniz ve Azure çözümlerinizi bkz [Azure Resource Manager'a genel bakış](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4811-106">If you are not familiar with the concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="a4811-107">Resource Manager şablonu ya da makinenizde yerel bir dosya ya da GitHub gibi bir havuzda bulunan dış dosyası dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4811-107">The Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="a4811-108">Bu makalede dağıttığınız şablonu kullanılabilir [örnek şablonu](#sample-template) bölümünde veya as [depolama hesabı şablonu github](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="a4811-108">The template you deploy in this article is available in the [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="a4811-109">Yerel makinenizde bir şablondan dağıtma</span><span class="sxs-lookup"><span data-stu-id="a4811-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="a4811-110">Kaynakları Azure'a dağıtırken:</span><span class="sxs-lookup"><span data-stu-id="a4811-110">When deploying resources to Azure, you:</span></span>

1. <span data-ttu-id="a4811-111">Azure hesabınızda oturum açın</span><span class="sxs-lookup"><span data-stu-id="a4811-111">Log in to your Azure account</span></span>
2. <span data-ttu-id="a4811-112">Dağıtılan kaynaklar için kapsayıcı görevi gören bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4811-112">Create a resource group that serves as the container for the deployed resources.</span></span> <span data-ttu-id="a4811-113">Kaynak grubu adı yalnızca alfasayısal karakterler, nokta, alt çizgi, kısa çizgi ve parantez içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a4811-113">The name of the resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="a4811-114">En fazla 90 karakter olabilir.</span><span class="sxs-lookup"><span data-stu-id="a4811-114">It can be up to 90 characters.</span></span> <span data-ttu-id="a4811-115">Bir nokta ile bitemez.</span><span class="sxs-lookup"><span data-stu-id="a4811-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="a4811-116">Kaynak grubu oluşturmak için kaynakları tanımlayan şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="a4811-116">Deploy to the resource group the template that defines the resources to create</span></span>

<span data-ttu-id="a4811-117">Bir şablon dağıtımı özelleştirmenize olanak sağlayan parametreler içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a4811-117">A template can include parameters that enable you to customize the deployment.</span></span> <span data-ttu-id="a4811-118">Örneğin, belirli bir ortamda (örneğin, geliştirme, test ve üretim) için uyarlanabilir değerler sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4811-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="a4811-119">Örnek şablon SKU depolama hesabı için bir parametre tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a4811-119">The sample template defines a parameter for the storage account SKU.</span></span>

<span data-ttu-id="a4811-120">Aşağıdaki örnek, bir kaynak grubu oluşturur ve yerel makinenize bir şablondan dağıtır:</span><span class="sxs-lookup"><span data-stu-id="a4811-120">The following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="a4811-121">Dağıtımın tamamlanması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="a4811-121">The deployment can take a few minutes to complete.</span></span> <span data-ttu-id="a4811-122">Tamamlandığında, sonuç içeren bir ileti görür:</span><span class="sxs-lookup"><span data-stu-id="a4811-122">When it finishes, you see a message that includes the result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="a4811-123">Bir dış kaynaktan şablon dağıtma</span><span class="sxs-lookup"><span data-stu-id="a4811-123">Deploy a template from an external source</span></span>

<span data-ttu-id="a4811-124">Resource Manager şablonları yerel makinenizde depolamak yerine bir dış konuma depolamak tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4811-124">Instead of storing Resource Manager templates on your local machine, you may prefer to store them in an external location.</span></span> <span data-ttu-id="a4811-125">Şablonları bir kaynak denetimi deponuza (örneğin, GitHub) depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4811-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="a4811-126">Veya, bunları paylaşılan erişim için bir Azure depolama hesabı, kuruluşunuzda depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4811-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="a4811-127">Dış bir şablonu dağıtmak için kullandığınız **TemplateUri** parametresi.</span><span class="sxs-lookup"><span data-stu-id="a4811-127">To deploy an external template, use the **TemplateUri** parameter.</span></span> <span data-ttu-id="a4811-128">URI örnekte github'dan örnek şablonu dağıtmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="a4811-128">Use the URI in the example to deploy the sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="a4811-129">Önceki örnekte şablonunuzu hassas bir veri içermemesi çünkü çoğu senaryo için çalışır ve şablona için genel olarak erişilebilir bir URI gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a4811-129">The preceding example requires a publicly accessible URI for the template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="a4811-130">Hassas veriler (örneğin, bir yönetici parolası) belirtmeniz gerekiyorsa, bu değeri güvenli bir parametre olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="a4811-130">If you need to specify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="a4811-131">Ancak, şablonunuzu genel olarak erişilebilir olmasını istemiyorsanız, bir özel depolama kapsayıcısı depolayarak koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4811-131">However, if you do not want your template to be publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="a4811-132">Bir paylaşılan erişim imzası (SAS) belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="a4811-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="a4811-133">Parametre dosyaları</span><span class="sxs-lookup"><span data-stu-id="a4811-133">Parameter files</span></span>

<span data-ttu-id="a4811-134">Satır içi değerler olarak komut parametreleri geçirme yerine parametre değerlerini içeren bir JSON dosyası kullanmak daha kolay.</span><span class="sxs-lookup"><span data-stu-id="a4811-134">Rather than passing parameters as inline values in your script, you may find it easier to use a JSON file that contains the parameter values.</span></span> <span data-ttu-id="a4811-135">Parametre dosyası şu biçimde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="a4811-135">The parameter file must be in the following format:</span></span>

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

<span data-ttu-id="a4811-136">Parametreler bölümünde şablonunuzda (storageAccountType) tanımlanan parametre eşleşen bir parametre adı içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="a4811-136">Notice that the parameters section includes a parameter name that matches the parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="a4811-137">Parametre dosyası parametresi için bir değer içerir.</span><span class="sxs-lookup"><span data-stu-id="a4811-137">The parameter file contains a value for the parameter.</span></span> <span data-ttu-id="a4811-138">Bu değer, dağıtım sırasında şablona otomatik olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="a4811-138">This value is automatically passed to the template during deployment.</span></span> <span data-ttu-id="a4811-139">Farklı dağıtım senaryoları için birden çok parametre dosyası oluşturun ve ardından uygun parametre dosyası geçirin.</span><span class="sxs-lookup"><span data-stu-id="a4811-139">You can create multiple parameter files for different deployment scenarios, and then pass in the appropriate parameter file.</span></span> 

<span data-ttu-id="a4811-140">Önceki örnekte kopyalayın ve adlı bir dosya kaydedin `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="a4811-140">Copy the preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="a4811-141">Bir yerel parametre dosyası geçirmek için kullanmak **TemplateParameterFile** parametre:</span><span class="sxs-lookup"><span data-stu-id="a4811-141">To pass a local parameter file, use the **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="a4811-142">Bir dış parametre dosyasına geçirmek için kullanmak **TemplateParameterUri** parametre:</span><span class="sxs-lookup"><span data-stu-id="a4811-142">To pass an external parameter file, use the **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="a4811-143">Satır içi parametreleri ve aynı dağıtım işlemi yerel parametre dosyasında kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4811-143">You can use inline parameters and a local parameter file in the same deployment operation.</span></span> <span data-ttu-id="a4811-144">Örneğin, bazı değerler yerel parametresini belirtin ve dağıtım sırasında diğer değerleri satır içi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a4811-144">For example, you can specify some values in the local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="a4811-145">Hem yerel parametre dosyası, hem de satır içi bir parametre için değer sağlarsanız, satır içi değer önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="a4811-145">If you provide values for a parameter in both the local parameter file and inline, the inline value takes precedence.</span></span>

<span data-ttu-id="a4811-146">Bir dış parametre dosyası kullandığınızda, ancak, diğer değerler ya da satır içi geçiremezsiniz veya yerel bir dosya.</span><span class="sxs-lookup"><span data-stu-id="a4811-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="a4811-147">Bir parametre dosyası belirttiğinizde **TemplateParameterUri** parametresi, tüm satır içi parametreleri yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="a4811-147">When you specify a parameter file in the **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="a4811-148">Dış dosyadaki tüm parametre değerlerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a4811-148">Provide all parameter values in the external file.</span></span> <span data-ttu-id="a4811-149">Şablonunuzu parametre dosyasında içeremez duyarlı bir değer içeriyorsa, bu değer bir anahtar Kasası'na ekleyin ya da dinamik olarak tüm parametre değerleri satır içi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a4811-149">If your template includes a sensitive value that you cannot include in the parameter file, either add that value to a key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="a4811-150">Şablonunuzu PowerShell komutunda parametrelerden biri aynı ada sahip bir parametre içeriyorsa, PowerShell şablonunuzu parametresinden sonek ile sayısını gösterir. **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="a4811-150">If your template includes a parameter with the same name as one of the parameters in the PowerShell command, PowerShell presents the parameter from your template with the postfix **FromTemplate**.</span></span> <span data-ttu-id="a4811-151">Örneğin, adlı bir parametre **ResourceGroupName** ile şablonu çakışıyor **ResourceGroupName** parametresinde [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a4811-151">For example, a parameter named **ResourceGroupName** in your template conflicts with the **ResourceGroupName** parameter in the [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="a4811-152">İçin bir değer sağlamanız istenir **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="a4811-152">You are prompted to provide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="a4811-153">Genel olarak, Karışıklığı önlemek için bu parametreleri dağıtım işlemleri için kullanılan parametreleri aynı ada sahip adlandırılmasıyla değil kaçınmalısınız.</span><span class="sxs-lookup"><span data-stu-id="a4811-153">In general, you should avoid this confusion by not naming parameters with the same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="a4811-154">Şablon dağıtımı test etme</span><span class="sxs-lookup"><span data-stu-id="a4811-154">Test a template deployment</span></span>

<span data-ttu-id="a4811-155">Herhangi bir kaynağa dağıtmadan şablonu ve parametre değerlerini sınamak için kullanın [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="a4811-155">To test your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="a4811-156">Hiçbir hata algılanırsa, komutu bir yanıt tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="a4811-156">If no errors are detected, the command finishes without a response.</span></span> <span data-ttu-id="a4811-157">Bir hata algılandığında, komutu bir hata iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="a4811-157">If an error is detected, the command returns an error message.</span></span> <span data-ttu-id="a4811-158">Örneğin, SKU, depolama hesabı için hatalı bir değer geçirmek çalışılırken aşağıdaki hata döndürür:</span><span class="sxs-lookup"><span data-stu-id="a4811-158">For example, attempting to pass an incorrect value for the storage account SKU, returns the following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'The provided value 'badSku' for the template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. The parameter value is not part of the allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="a4811-159">Şablonunuzun söz dizimi hatası varsa, komut şablon ayrıştırılamadı belirten bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="a4811-159">If your template has a syntax error, the command returns an error indicating it could not parse the template.</span></span> <span data-ttu-id="a4811-160">İleti satır numarası ve ayrıştırma hatası konumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4811-160">The message indicates the line number and position of the parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="a4811-161">Tam modu kullanmak için `Mode` parametre:</span><span class="sxs-lookup"><span data-stu-id="a4811-161">To use complete mode, use the `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="a4811-162">Örnek şablonu</span><span class="sxs-lookup"><span data-stu-id="a4811-162">Sample template</span></span>

<span data-ttu-id="a4811-163">Aşağıdaki şablonu, bu konudaki örnekler için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a4811-163">The following template is used for the examples in this topic.</span></span> <span data-ttu-id="a4811-164">Kopyalayın ve storage.json adlı bir dosya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a4811-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="a4811-165">Bu şablonun nasıl oluşturulacağını anlamak için bkz: [, ilk Azure Resource Manager şablonu oluşturma](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="a4811-165">To understand how to create this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="a4811-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4811-166">Next steps</span></span>
* <span data-ttu-id="a4811-167">Bu makaledeki örneklerde kaynakları varsayılan aboneliğinizde bir kaynak grubuna dağıtın.</span><span class="sxs-lookup"><span data-stu-id="a4811-167">The examples in this article deploy resources to a resource group in your default subscription.</span></span> <span data-ttu-id="a4811-168">Farklı bir abonelik kullanmak için bkz: [birden çok Azure Aboneliklerini yönetmek](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="a4811-168">To use a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="a4811-169">Bir şablon dağıtan bir tam örnek betik için bkz: [Resource Manager şablonu dağıtım betiği](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a4811-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="a4811-170">Şablonunuzda parametrelerini tanımlamak nasıl anlamak için bkz: [yapısı ve Azure Resource Manager şablonları sözdizimini anlamanız](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a4811-170">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="a4811-171">Genel dağıtım hatalarını giderme ipuçları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="a4811-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="a4811-172">Bir SAS belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="a4811-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="a4811-173">Kuruluşların abonelikleri etkili bir şekilde yönetmek için Resource Manager'ı nasıl kullanabileceği hakkında yönergeler için bkz. [Azure kurumsal iskelesi: öngörücü abonelik idaresi](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="a4811-173">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

