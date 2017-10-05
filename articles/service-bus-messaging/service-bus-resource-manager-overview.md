---
title: "Azure Resource Manager şablonları kullanarak Azure Service Bus kaynakları oluşturun | Microsoft Docs"
description: "Service Bus kaynaklarını oluşturmayı otomatikleştirmek için Azure Resource Manager şablonlarını kullanma"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: c8142d8edfd3a527b13d655bac21acf5332f2d14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="a0770-103">Azure Resource Manager şablonları kullanarak Service Bus kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="a0770-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="a0770-104">Bu makalede, Azure Resource Manager şablonları, PowerShell ve Service Bus kaynak sağlayıcısı kullanarak Service Bus kaynaklarını oluşturup açıklar.</span><span class="sxs-lookup"><span data-stu-id="a0770-104">This article describes how to create and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and the Service Bus resource provider.</span></span>

<span data-ttu-id="a0770-105">Azure Resource Manager şablonları bir çözümü dağıtmak ve parametreleri ve farklı ortamlar için değer girmesini sağlayan değişkenleri belirtmek için kaynakları tanımlamanıza yardımcı.</span><span class="sxs-lookup"><span data-stu-id="a0770-105">Azure Resource Manager templates help you define the resources to deploy for a solution, and to specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="a0770-106">JSON ve dağıtımınız için değerleri oluşturmada kullanabileceğiniz ifadeler, şablon oluşur.</span><span class="sxs-lookup"><span data-stu-id="a0770-106">The template consists of JSON and expressions that you can use to construct values for your deployment.</span></span> <span data-ttu-id="a0770-107">Azure Resource Manager şablonları ve şablon biçimi tartışması yazma hakkında ayrıntılı bilgi için bkz: [yapısı ve Azure Resource Manager şablonları sözdizimini](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a0770-107">For detailed information about writing Azure Resource Manager templates, and a discussion of the template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a0770-108">Bu makaledeki örnekler Azure Resource Manager bir hizmet veri yolu ad alanı ve mesajlaşma varlığıyla (kuyruk) oluşturmak için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="a0770-108">The examples in this article show how to use Azure Resource Manager to create a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="a0770-109">Diğer şablon örnekler için ziyaret [Azure hızlı başlangıç Şablon Galerisi] [ Azure Quickstart Templates gallery] ve "Service Bus" için arama</span><span class="sxs-lookup"><span data-stu-id="a0770-109">For other template examples, visit the [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="a0770-110">Hizmet veri yolu Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="a0770-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="a0770-111">Bu hizmet veri yolu Azure Resource Manager şablonları, yükleme ve dağıtım için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a0770-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="a0770-112">Her biri, GitHub şablonlar için bağlantılar ile birlikte hakkında ayrıntılı bilgi için aşağıdaki bağlantıları tıklatın:</span><span class="sxs-lookup"><span data-stu-id="a0770-112">Click the following links for details about each one, with links to the templates on GitHub:</span></span>

* [<span data-ttu-id="a0770-113">Hizmet veri yolu ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0770-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="a0770-114">Sıra ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0770-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="a0770-115">Hizmet veri yolu ad alanı konu ve abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0770-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="a0770-116">Kuyruk ve yetkilendirme kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0770-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="a0770-117">Konu, abonelik ve kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0770-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="a0770-118">PowerShell ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="a0770-118">Deploy with PowerShell</span></span>

<span data-ttu-id="a0770-119">Aşağıdaki yordam oluşturan bir Azure Resource Manager şablonu dağıtmak için PowerShell kullanmayı açıklar bir **standart** Service Bus ad alanı ve bu ad alanı içindeki bir sıra katmanı.</span><span class="sxs-lookup"><span data-stu-id="a0770-119">The following procedure describes how to use PowerShell to deploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="a0770-120">Bu örnek dayanır [sıra ile Service Bus ad alanı oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) şablonu.</span><span class="sxs-lookup"><span data-stu-id="a0770-120">This example is based on the [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="a0770-121">Yaklaşık iş akışı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="a0770-121">The approximate workflow is as follows:</span></span>

1. <span data-ttu-id="a0770-122">PowerShell yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a0770-122">Install PowerShell.</span></span>
2. <span data-ttu-id="a0770-123">Şablon ve (isteğe bağlı) bir parametre dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a0770-123">Create the template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="a0770-124">PowerShell'de, Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="a0770-124">In PowerShell, log in to your Azure account.</span></span>
4. <span data-ttu-id="a0770-125">Bir mevcut değilse yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a0770-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="a0770-126">Dağıtımı test etme.</span><span class="sxs-lookup"><span data-stu-id="a0770-126">Test the deployment.</span></span>
6. <span data-ttu-id="a0770-127">İsterseniz, dağıtım modu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a0770-127">If desired, set the deployment mode.</span></span>
7. <span data-ttu-id="a0770-128">Şablon dağıtın.</span><span class="sxs-lookup"><span data-stu-id="a0770-128">Deploy the template.</span></span>

<span data-ttu-id="a0770-129">Azure Resource Manager şablonları dağıtma hakkında tam bilgi için bkz: [kaynakları Azure Resource Manager şablonları ile dağıtma][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="a0770-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="a0770-130">PowerShell yükleme</span><span class="sxs-lookup"><span data-stu-id="a0770-130">Install PowerShell</span></span>

<span data-ttu-id="a0770-131">Azure PowerShell yönergelerini takip ederek yükleyin [Azure PowerShell ile çalışmaya başlama](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="a0770-131">Install Azure PowerShell by following the instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="a0770-132">Şablon oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0770-132">Create a template</span></span>

<span data-ttu-id="a0770-133">Kopya veya kopya [201-servicebus--kuyruk oluşturma](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) github'dan şablon:</span><span class="sxs-lookup"><span data-stu-id="a0770-133">Clone or copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of the Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by the template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="a0770-134">Bir parametre dosyası (isteğe bağlı) oluşturun</span><span class="sxs-lookup"><span data-stu-id="a0770-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="a0770-135">Bir isteğe bağlı parametreler dosyası kullanmak için kopyalamanız [201-servicebus--kuyruk oluşturma](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) dosya.</span><span class="sxs-lookup"><span data-stu-id="a0770-135">To use an optional parameters file, copy the [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="a0770-136">Değerini `serviceBusNamespaceName` bu dağıtımda oluşturun ve değerini değiştirmek istediğiniz hizmet veri yolu ad alanı ile `serviceBusQueueName` oluşturmak istediğiniz kuyruk adı.</span><span class="sxs-lookup"><span data-stu-id="a0770-136">Replace the value of `serviceBusNamespaceName` with the name of the Service Bus namespace you want to create in this deployment, and replace the value of `serviceBusQueueName` with the name of the queue you want to create.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

<span data-ttu-id="a0770-137">Daha fazla bilgi için bkz: [parametreleri](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) konu.</span><span class="sxs-lookup"><span data-stu-id="a0770-137">For more information, see the [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-to-azure-and-set-the-azure-subscription"></a><span data-ttu-id="a0770-138">Azure'da oturum açma ve Azure abonelik ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a0770-138">Log in to Azure and set the Azure subscription</span></span>

<span data-ttu-id="a0770-139">Bir PowerShell isteminden aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a0770-139">From a PowerShell prompt, run the following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="a0770-140">Azure hesabınızda oturum açmak için istenir.</span><span class="sxs-lookup"><span data-stu-id="a0770-140">You are prompted to log on to your Azure account.</span></span> <span data-ttu-id="a0770-141">Oturum açtıktan sonra kullanılabilir aboneliklerinizi görüntülemek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a0770-141">After logging on, run the following command to view your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="a0770-142">Bu komut kullanılabilir Azure Aboneliklerin listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="a0770-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="a0770-143">Aşağıdaki komutu çalıştırarak geçerli oturum için bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="a0770-143">Choose a subscription for the current session by running the following command.</span></span> <span data-ttu-id="a0770-144">Değiştir `<YourSubscriptionId>` kullanmak istediğiniz Azure aboneliği için GUID ile.</span><span class="sxs-lookup"><span data-stu-id="a0770-144">Replace `<YourSubscriptionId>` with the GUID for the Azure subscription you want to use.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-the-resource-group"></a><span data-ttu-id="a0770-145">Kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="a0770-145">Set the resource group</span></span>

<span data-ttu-id="a0770-146">Grup, yeni bir kaynak grubu oluşturmak için mevcut bir kaynağı yoksa ** New-AzureRmResourceGroup ** komutu.</span><span class="sxs-lookup"><span data-stu-id="a0770-146">If you do not have an existing resource group, create a new resource group with the **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="a0770-147">Kullanmak istediğiniz konumu ve kaynak grubu adını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a0770-147">Provide the name of the resource group and location you want to use.</span></span> <span data-ttu-id="a0770-148">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a0770-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="a0770-149">Başarılı olursa, yeni kaynak grubu bir özeti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a0770-149">If successful, a summary of the new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-the-deployment"></a><span data-ttu-id="a0770-150">Dağıtımı test etme</span><span class="sxs-lookup"><span data-stu-id="a0770-150">Test the deployment</span></span>

<span data-ttu-id="a0770-151">Çalıştırarak, dağıtımınızı doğrulama `Test-AzureRmResourceGroupDeployment` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a0770-151">Validate your deployment by running the `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="a0770-152">Tam dağıtım yürütülürken gibi dağıtım sınarken parametreleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="a0770-152">When testing the deployment, provide parameters exactly as you would when executing the deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="create-the-deployment"></a><span data-ttu-id="a0770-153">Dağıtım oluşturma</span><span class="sxs-lookup"><span data-stu-id="a0770-153">Create the deployment</span></span>

<span data-ttu-id="a0770-154">Yeni dağıtım oluşturmak için çalıştırın `New-AzureRmResourceGroupDeployment` cmdlet'ini ve istendiğinde gerekli parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="a0770-154">To create the new deployment, run the `New-AzureRmResourceGroupDeployment` cmdlet, and provide the necessary parameters when prompted.</span></span> <span data-ttu-id="a0770-155">Parametreleri adına, kaynak grubu ve yolu veya URL'si şablon dosyası, dağıtımınız için bir ad içerir.</span><span class="sxs-lookup"><span data-stu-id="a0770-155">The parameters include a name for your deployment, the name of your resource group, and the path or URL to the template file.</span></span> <span data-ttu-id="a0770-156">Varsa **modu** parametresi belirtilmezse, varsayılan değeri **artımlı** kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a0770-156">If the **Mode** parameter is not specified, the default value of **Incremental** is used.</span></span> <span data-ttu-id="a0770-157">Daha fazla bilgi için bkz: [artımlı ve tam dağıtımları](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="a0770-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="a0770-158">Aşağıdaki komutu PowerShell penceresinde üç parametre ister:</span><span class="sxs-lookup"><span data-stu-id="a0770-158">The following command prompts you for the three parameters in the PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

<span data-ttu-id="a0770-159">Bunun yerine bir parametre dosyası belirtmek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="a0770-159">To specify a parameters file instead, use the following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -TemplateParameterFile <path to parameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="a0770-160">Dağıtım cmdlet'ini çalıştırdığınızda, satır içi parametreleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a0770-160">You can also use inline parameters when you run the deployment cmdlet.</span></span> <span data-ttu-id="a0770-161">Komut aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="a0770-161">The command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="a0770-162">Çalıştırmak için bir [tam](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) dağıtımı, **modu** parametresi **tam**:</span><span class="sxs-lookup"><span data-stu-id="a0770-162">To run a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set the **Mode** parameter to **Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path to template file>\azuredeploy.json
```

### <a name="verify-the-deployment"></a><span data-ttu-id="a0770-163">Dağıtımı doğrulama</span><span class="sxs-lookup"><span data-stu-id="a0770-163">Verify the deployment</span></span>
<span data-ttu-id="a0770-164">Kaynakları başarıyla dağıtılmışsa, dağıtım özetini PowerShell penceresinde görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="a0770-164">If the resources are deployed successfully, a summary of the deployment is displayed in the PowerShell window:</span></span>

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a><span data-ttu-id="a0770-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a0770-165">Next steps</span></span>
<span data-ttu-id="a0770-166">Şimdi bir Azure Resource Manager şablonunu dağıtmak için komutları ve temel iş akışı gördünüz.</span><span class="sxs-lookup"><span data-stu-id="a0770-166">You've now seen the basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="a0770-167">Daha ayrıntılı bilgi için aşağıdaki bağlantıları ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="a0770-167">For more detailed information, visit the following links:</span></span>

* <span data-ttu-id="a0770-168">[Azure Resource Manager'a genel bakış][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="a0770-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="a0770-169">[Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtma][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="a0770-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="a0770-170">Azure Resource Manager şablonları yazma</span><span class="sxs-lookup"><span data-stu-id="a0770-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
