---
title: "PowerShell ve şablon aaaDeploy kaynaklarla | Microsoft Docs"
description: "Azure Resource Manager ve Azure PowerShell toodeploy kaynakları tooAzure kullanın. Merhaba kaynaklar bir Resource Manager şablonunda tanımlanır."
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
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a><span data-ttu-id="6ec8e-104">Kaynakları Resource Manager şablonları ve Azure PowerShell ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="6ec8e-104">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>

<span data-ttu-id="6ec8e-105">Bu konuda açıklanmaktadır nasıl toouse Azure PowerShell'i Resource Manager şablonları toodeploy ile kaynakları tooAzure.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-105">This topic explains how toouse Azure PowerShell with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="6ec8e-106">Dağıtma hello kavramları hakkında bilgi sahibi değilseniz ve Azure çözümlerinizi bkz [Azure Resource Manager'a genel bakış](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-106">If you are not familiar with hello concepts of deploying and managing your Azure solutions, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="6ec8e-107">Merhaba Resource Manager şablonu ya da makinenizde yerel bir dosya ya da GitHub gibi bir havuzda bulunan dış dosyası dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-107">hello Resource Manager template you deploy can either be a local file on your machine, or an external file that is located in a repository like GitHub.</span></span> <span data-ttu-id="6ec8e-108">Bu makalede dağıttığınız hello şablon hello kullanılabilir [örnek şablonu](#sample-template) bölümünde veya as [depolama hesabı şablonu github](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-108">hello template you deploy in this article is available in hello [Sample template](#sample-template) section, or as [storage account template in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a><span data-ttu-id="6ec8e-109">Yerel makinenizde bir şablondan dağıtma</span><span class="sxs-lookup"><span data-stu-id="6ec8e-109">Deploy a template from your local machine</span></span>

<span data-ttu-id="6ec8e-110">Kaynakları tooAzure dağıtırken:</span><span class="sxs-lookup"><span data-stu-id="6ec8e-110">When deploying resources tooAzure, you:</span></span>

1. <span data-ttu-id="6ec8e-111">Azure hesabı tooyour içinde oturum</span><span class="sxs-lookup"><span data-stu-id="6ec8e-111">Log in tooyour Azure account</span></span>
2. <span data-ttu-id="6ec8e-112">Dağıtılan hello kaynaklar için hello kapsayıcı görevi gören bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-112">Create a resource group that serves as hello container for hello deployed resources.</span></span> <span data-ttu-id="6ec8e-113">Hello hello kaynak grubu adı yalnızca alfasayısal karakterler, nokta, alt çizgi, kısa çizgi ve parantez içerebilir.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-113">hello name of hello resource group can only include alphanumeric characters, periods, underscores, hyphens, and parenthesis.</span></span> <span data-ttu-id="6ec8e-114">Too90 karakter olabilir.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-114">It can be up too90 characters.</span></span> <span data-ttu-id="6ec8e-115">Bir nokta ile bitemez.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-115">It cannot end in a period.</span></span>
3. <span data-ttu-id="6ec8e-116">Merhaba kaynakları toocreate tanımlar toohello kaynak grubu hello şablonu dağıtma</span><span class="sxs-lookup"><span data-stu-id="6ec8e-116">Deploy toohello resource group hello template that defines hello resources toocreate</span></span>

<span data-ttu-id="6ec8e-117">Bir şablon toocustomize hello dağıtımını etkinleştirmek parametreleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-117">A template can include parameters that enable you toocustomize hello deployment.</span></span> <span data-ttu-id="6ec8e-118">Örneğin, belirli bir ortamda (örneğin, geliştirme, test ve üretim) için uyarlanabilir değerler sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-118">For example, you can provide values that are tailored for a particular environment (such as dev, test, and production).</span></span> <span data-ttu-id="6ec8e-119">Merhaba örnek şablonu hello depolama hesabı SKU için bir parametre tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-119">hello sample template defines a parameter for hello storage account SKU.</span></span>

<span data-ttu-id="6ec8e-120">Aşağıdaki örnek hello bir kaynak grubu oluşturur ve yerel makinenize bir şablondan dağıtır:</span><span class="sxs-lookup"><span data-stu-id="6ec8e-120">hello following example creates a resource group, and deploys a template from your local machine:</span></span>

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="6ec8e-121">Merhaba dağıtım birkaç dakika toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-121">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="6ec8e-122">Tamamlandığında, hello sonuç içeren bir ileti görür:</span><span class="sxs-lookup"><span data-stu-id="6ec8e-122">When it finishes, you see a message that includes hello result:</span></span>

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a><span data-ttu-id="6ec8e-123">Bir dış kaynaktan şablon dağıtma</span><span class="sxs-lookup"><span data-stu-id="6ec8e-123">Deploy a template from an external source</span></span>

<span data-ttu-id="6ec8e-124">Resource Manager şablonları yerel makinenizde depolamak yerine toostore tercih edebilirsiniz harici bir konumda bunları.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-124">Instead of storing Resource Manager templates on your local machine, you may prefer toostore them in an external location.</span></span> <span data-ttu-id="6ec8e-125">Şablonları bir kaynak denetimi deponuza (örneğin, GitHub) depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-125">You can store templates in a source control repository (such as GitHub).</span></span> <span data-ttu-id="6ec8e-126">Veya, bunları paylaşılan erişim için bir Azure depolama hesabı, kuruluşunuzda depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-126">Or, you can store them in an Azure storage account for shared access in your organization.</span></span>

<span data-ttu-id="6ec8e-127">toodeploy dış bir şablonu kullanmak hello **TemplateUri** parametresi.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-127">toodeploy an external template, use hello **TemplateUri** parameter.</span></span> <span data-ttu-id="6ec8e-128">Merhaba örnek toodeploy hello örnek şablonunu github'dan Hello URI kullanın.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-128">Use hello URI in hello example toodeploy hello sample template from GitHub.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

<span data-ttu-id="6ec8e-129">Merhaba önceki örnekte genel olarak erişilebilir bir URI şablonunuzu hassas bir veri içermemesi çünkü çoğu senaryo için çalışır hello şablonu için gerektirir.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-129">hello preceding example requires a publicly accessible URI for hello template, which works for most scenarios because your template should not include sensitive data.</span></span> <span data-ttu-id="6ec8e-130">Toospecify hassas verileri (örneğin, bir yönetici parolası) gerekiyorsa, bu değeri güvenli bir parametre olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-130">If you need toospecify sensitive data (like an admin password), pass that value as a secure parameter.</span></span> <span data-ttu-id="6ec8e-131">Ancak, şablon toobe genel olarak erişilebilir istemiyorsanız, bir özel depolama kapsayıcısı depolayarak koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-131">However, if you do not want your template toobe publicly accessible, you can protect it by storing it in a private storage container.</span></span> <span data-ttu-id="6ec8e-132">Bir paylaşılan erişim imzası (SAS) belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-132">For information about deploying a template that requires a shared access signature (SAS) token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>

## <a name="parameter-files"></a><span data-ttu-id="6ec8e-133">Parametre dosyaları</span><span class="sxs-lookup"><span data-stu-id="6ec8e-133">Parameter files</span></span>

<span data-ttu-id="6ec8e-134">Satır içi değerler olarak komut parametreleri geçirme yerine daha kolay toouse hello parametre değerlerini içeren bir JSON dosyası bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-134">Rather than passing parameters as inline values in your script, you may find it easier toouse a JSON file that contains hello parameter values.</span></span> <span data-ttu-id="6ec8e-135">Merhaba parametre dosyası biçimini izleyen hello olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="6ec8e-135">hello parameter file must be in hello following format:</span></span>

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

<span data-ttu-id="6ec8e-136">Merhaba Parametreler bölümünde şablonunuzda (storageAccountType) tanımlı hello parametresi ile eşleşen bir parametre adı içerdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-136">Notice that hello parameters section includes a parameter name that matches hello parameter defined in your template (storageAccountType).</span></span> <span data-ttu-id="6ec8e-137">Merhaba parametre dosyası hello parametresi için bir değer içerir.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-137">hello parameter file contains a value for hello parameter.</span></span> <span data-ttu-id="6ec8e-138">Bu değer, dağıtım sırasında toohello şablonu otomatik olarak geçirilir.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-138">This value is automatically passed toohello template during deployment.</span></span> <span data-ttu-id="6ec8e-139">Farklı dağıtım senaryoları için birden çok parametre dosyası oluşturun ve hello uygun parametre dosyası geçirin.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-139">You can create multiple parameter files for different deployment scenarios, and then pass in hello appropriate parameter file.</span></span> 

<span data-ttu-id="6ec8e-140">Örnek önceki hello kopyalayın ve adlı bir dosya kaydedin `storage.parameters.json`.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-140">Copy hello preceding example and save it as a file named `storage.parameters.json`.</span></span>

<span data-ttu-id="6ec8e-141">toopass yerel parametre dosyası kullanmak hello **TemplateParameterFile** parametre:</span><span class="sxs-lookup"><span data-stu-id="6ec8e-141">toopass a local parameter file, use hello **TemplateParameterFile** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

<span data-ttu-id="6ec8e-142">toopass bir dış parametre dosyası kullanmak hello **TemplateParameterUri** parametre:</span><span class="sxs-lookup"><span data-stu-id="6ec8e-142">toopass an external parameter file, use hello **TemplateParameterUri** parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

<span data-ttu-id="6ec8e-143">Satır içi parametreleri kullanabilirsiniz ve yerel bir parametre dosyası hello aynı dağıtım işlemi.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-143">You can use inline parameters and a local parameter file in hello same deployment operation.</span></span> <span data-ttu-id="6ec8e-144">Örneğin, bazı değerler hello yerel parametre dosyasında belirtin ve dağıtım sırasında diğer değerleri satır içi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-144">For example, you can specify some values in hello local parameter file and add other values inline during deployment.</span></span> <span data-ttu-id="6ec8e-145">Merhaba yerel parametre dosyası ve satır içi bir parametre için değer sağlarsanız, hello satır içi değer önceliklidir.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-145">If you provide values for a parameter in both hello local parameter file and inline, hello inline value takes precedence.</span></span>

<span data-ttu-id="6ec8e-146">Bir dış parametre dosyası kullandığınızda, ancak, diğer değerler ya da satır içi geçiremezsiniz veya yerel bir dosya.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-146">However, when you use an external parameter file, you cannot pass other values either inline or from a local file.</span></span> <span data-ttu-id="6ec8e-147">Bir parametre dosyası hello belirttiğinizde **TemplateParameterUri** parametresi, tüm satır içi parametreleri yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-147">When you specify a parameter file in hello **TemplateParameterUri** parameter, all inline parameters are ignored.</span></span> <span data-ttu-id="6ec8e-148">Merhaba dış dosyadaki tüm parametre değerlerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-148">Provide all parameter values in hello external file.</span></span> <span data-ttu-id="6ec8e-149">Şablonunuzu hello parametre dosyasında içeremez duyarlı bir değer içeriyorsa, bu değer tooa anahtar kasası ekleyin ya da dinamik olarak tüm parametre değerleri satır içi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-149">If your template includes a sensitive value that you cannot include in hello parameter file, either add that value tooa key vault, or dynamically provide all parameter values inline.</span></span>

<span data-ttu-id="6ec8e-150">Şablonunuzu aynı adı hello PowerShell komutunu hello parametrelerinde biri olarak hello parametresiyle içeriyorsa, PowerShell şablonunuzu hello parametresinden hello sonek ile sayısını gösterir. **FromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-150">If your template includes a parameter with hello same name as one of hello parameters in hello PowerShell command, PowerShell presents hello parameter from your template with hello postfix **FromTemplate**.</span></span> <span data-ttu-id="6ec8e-151">Örneğin, adlı bir parametre **ResourceGroupName** hello ile şablonu çakışıyor **ResourceGroupName** hello parametresinde [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-151">For example, a parameter named **ResourceGroupName** in your template conflicts with hello **ResourceGroupName** parameter in hello [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) cmdlet.</span></span> <span data-ttu-id="6ec8e-152">İstendiğinde tooprovide için bir değer olan **ResourceGroupNameFromTemplate**.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-152">You are prompted tooprovide a value for **ResourceGroupNameFromTemplate**.</span></span> <span data-ttu-id="6ec8e-153">Genel olarak, aynı dağıtım işlemleri için kullanılan parametreler olarak ad hello parametrelerle adlandırılmasıyla değil Bu Karışıklığı önlemek.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-153">In general, you should avoid this confusion by not naming parameters with hello same name as parameters used for deployment operations.</span></span>

## <a name="test-a-template-deployment"></a><span data-ttu-id="6ec8e-154">Şablon dağıtımı test etme</span><span class="sxs-lookup"><span data-stu-id="6ec8e-154">Test a template deployment</span></span>

<span data-ttu-id="6ec8e-155">herhangi bir kaynağa gerçekte dağıtımı olmadan şablonu ve parametre değerlerini tootest kullanmak [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-155">tootest your template and parameter values without actually deploying any resources, use [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment).</span></span> 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

<span data-ttu-id="6ec8e-156">Hiçbir hata algılanırsa, bir yanıt hello komutu tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-156">If no errors are detected, hello command finishes without a response.</span></span> <span data-ttu-id="6ec8e-157">Bir hata algılandığında, hello komutu bir hata iletisi döndürür.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-157">If an error is detected, hello command returns an error message.</span></span> <span data-ttu-id="6ec8e-158">Örneğin, toopass hello depolama hesabının SKU, yanlış bir değere çalışırken aşağıdaki hata hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="6ec8e-158">For example, attempting toopass an incorrect value for hello storage account SKU, returns hello following error:</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

<span data-ttu-id="6ec8e-159">Şablonunuzun söz dizimi hatası varsa, hello komut hello şablon ayrıştırılamadı belirten bir hata döndürür.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-159">If your template has a syntax error, hello command returns an error indicating it could not parse hello template.</span></span> <span data-ttu-id="6ec8e-160">Merhaba iletisi hello satır numarasını ve ayrıştırma hatası hello konumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-160">hello message indicates hello line number and position of hello parsing error.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

<span data-ttu-id="6ec8e-161">toouse tam modu, kullanım hello `Mode` parametre:</span><span class="sxs-lookup"><span data-stu-id="6ec8e-161">toouse complete mode, use hello `Mode` parameter:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a><span data-ttu-id="6ec8e-162">Örnek şablonu</span><span class="sxs-lookup"><span data-stu-id="6ec8e-162">Sample template</span></span>

<span data-ttu-id="6ec8e-163">Merhaba aşağıdaki şablonu bu konudaki hello örnekleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-163">hello following template is used for hello examples in this topic.</span></span> <span data-ttu-id="6ec8e-164">Kopyalayın ve storage.json adlı bir dosya kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-164">Copy and save it as a file named storage.json.</span></span> <span data-ttu-id="6ec8e-165">toounderstand nasıl toocreate bu şablonu bkz [, ilk Azure Resource Manager şablonu oluşturma](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-165">toounderstand how toocreate this template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>  

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

## <a name="next-steps"></a><span data-ttu-id="6ec8e-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6ec8e-166">Next steps</span></span>
* <span data-ttu-id="6ec8e-167">Bu makaledeki örneklerde Hello varsayılan aboneliğinizin kaynakları tooa kaynak grubuna dağıtın.</span><span class="sxs-lookup"><span data-stu-id="6ec8e-167">hello examples in this article deploy resources tooa resource group in your default subscription.</span></span> <span data-ttu-id="6ec8e-168">toouse farklı bir abonelik bkz [birden çok Azure Aboneliklerini yönetmek](/powershell/azure/manage-subscriptions-azureps).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-168">toouse a different subscription, see [Manage multiple Azure subscriptions](/powershell/azure/manage-subscriptions-azureps).</span></span>
* <span data-ttu-id="6ec8e-169">Bir şablon dağıtan bir tam örnek betik için bkz: [Resource Manager şablonu dağıtım betiği](resource-manager-samples-powershell-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-169">For a complete sample script that deploys a template, see [Resource Manager template deployment script](resource-manager-samples-powershell-deploy.md).</span></span>
* <span data-ttu-id="6ec8e-170">şablonunuzu toodefine parametrelerinde nasıl görürüm toounderstand [anlamak hello yapısı ve Azure Resource Manager şablonları sözdizimini](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-170">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="6ec8e-171">Genel dağıtım hatalarını giderme ipuçları için bkz: [ortak Azure dağıtım hataları Azure Resource Manager ile ilgili sorunları giderme](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-171">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="6ec8e-172">Bir SAS belirteci gerektiren şablonu dağıtma hakkında daha fazla bilgi için bkz: [dağıtma özel şablonu SAS belirteci ile](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-172">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="6ec8e-173">Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="6ec8e-173">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

