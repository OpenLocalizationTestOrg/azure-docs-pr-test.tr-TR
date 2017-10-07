---
title: "Azure Resource Manager şablonları kullanarak aaaCreate Azure Service Bus kaynakları | Microsoft Docs"
description: "Azure Resource Manager şablonları tooautomate hello Service Bus kaynaklarını oluşturulmasını kullanın"
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
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a><span data-ttu-id="57e09-103">Azure Resource Manager şablonları kullanarak Service Bus kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="57e09-103">Create Service Bus resources using Azure Resource Manager templates</span></span>

<span data-ttu-id="57e09-104">Bu makalede nasıl toocreate ve Service Bus kaynaklarını Azure Resource Manager şablonları, PowerShell ve hello Service Bus kaynak sağlayıcısı kullanarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="57e09-104">This article describes how toocreate and deploy Service Bus resources using Azure Resource Manager templates, PowerShell, and hello Service Bus resource provider.</span></span>

<span data-ttu-id="57e09-105">Azure Resource Manager şablonları şunları hello kaynakları toodeploy bir çözüm ve toospecify parametreleri ve farklı ortamlar için tooinput değerleri etkinleştir değişkenleri için tanımlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="57e09-105">Azure Resource Manager templates help you define hello resources toodeploy for a solution, and toospecify parameters and variables that enable you tooinput values for different environments.</span></span> <span data-ttu-id="57e09-106">JSON ve dağıtımınız için tooconstruct değerleri kullanabileceğiniz ifadeler Hello şablonu oluşur.</span><span class="sxs-lookup"><span data-stu-id="57e09-106">hello template consists of JSON and expressions that you can use tooconstruct values for your deployment.</span></span> <span data-ttu-id="57e09-107">Azure Resource Manager şablonları ve tartışma hello şablon biçimi için yazma hakkında ayrıntılı bilgi için bkz: [yapısı ve Azure Resource Manager şablonları sözdizimini](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="57e09-107">For detailed information about writing Azure Resource Manager templates, and a discussion of hello template format, see [structure and syntax of Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="57e09-108">Bu makale Göster örneklerde nasıl hello toouse Azure Resource Manager toocreate bir hizmet veri yolu ad alanı ve varlık (kuyruk) Mesajlaşma.</span><span class="sxs-lookup"><span data-stu-id="57e09-108">hello examples in this article show how toouse Azure Resource Manager toocreate a Service Bus namespace and messaging entity (queue).</span></span> <span data-ttu-id="57e09-109">Diğer şablon örnekler için hello ziyaret [Azure hızlı başlangıç Şablon Galerisi] [ Azure Quickstart Templates gallery] ve "Service Bus" için arama</span><span class="sxs-lookup"><span data-stu-id="57e09-109">For other template examples, visit hello [Azure Quickstart Templates gallery][Azure Quickstart Templates gallery] and search for "Service Bus."</span></span>
>
>

## <a name="service-bus-resource-manager-templates"></a><span data-ttu-id="57e09-110">Hizmet veri yolu Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="57e09-110">Service Bus Resource Manager templates</span></span>

<span data-ttu-id="57e09-111">Bu hizmet veri yolu Azure Resource Manager şablonları, yükleme ve dağıtım için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="57e09-111">These Service Bus Azure Resource Manager templates are available for download and deployment.</span></span> <span data-ttu-id="57e09-112">Her biri, github'da bağlantıları toohello şablonlarıyla hakkında ayrıntılı bilgi için bağlantılar aşağıdaki hello tıklatın:</span><span class="sxs-lookup"><span data-stu-id="57e09-112">Click hello following links for details about each one, with links toohello templates on GitHub:</span></span>

* [<span data-ttu-id="57e09-113">Hizmet veri yolu ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e09-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
* [<span data-ttu-id="57e09-114">Sıra ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e09-114">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
* [<span data-ttu-id="57e09-115">Hizmet veri yolu ad alanı konu ve abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e09-115">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
* [<span data-ttu-id="57e09-116">Kuyruk ve yetkilendirme kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e09-116">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
* [<span data-ttu-id="57e09-117">Konu, abonelik ve kuralı ile Service Bus ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e09-117">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a><span data-ttu-id="57e09-118">PowerShell ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="57e09-118">Deploy with PowerShell</span></span>

<span data-ttu-id="57e09-119">Merhaba aşağıdaki yordamda açıklanmıştır nasıl toouse PowerShell toodeploy bir Azure Resource Manager şablonu oluşturan bir **standart** Service Bus ad alanı ve bu ad alanı içindeki bir sıra katmanı.</span><span class="sxs-lookup"><span data-stu-id="57e09-119">hello following procedure describes how toouse PowerShell toodeploy an Azure Resource Manager template that creates a **Standard** tier Service Bus namespace, and a queue within that namespace.</span></span> <span data-ttu-id="57e09-120">Bu örnekte hello üzerinde temel [sıra ile Service Bus ad alanı oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) şablonu.</span><span class="sxs-lookup"><span data-stu-id="57e09-120">This example is based on hello [Create a Service Bus namespace with queue](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) template.</span></span> <span data-ttu-id="57e09-121">Merhaba yaklaşık iş akışı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="57e09-121">hello approximate workflow is as follows:</span></span>

1. <span data-ttu-id="57e09-122">PowerShell yükleyin.</span><span class="sxs-lookup"><span data-stu-id="57e09-122">Install PowerShell.</span></span>
2. <span data-ttu-id="57e09-123">Merhaba şablonu ve (isteğe bağlı) bir parametre dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="57e09-123">Create hello template and (optionally) a parameter file.</span></span>
3. <span data-ttu-id="57e09-124">PowerShell'de tooyour Azure hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="57e09-124">In PowerShell, log in tooyour Azure account.</span></span>
4. <span data-ttu-id="57e09-125">Bir mevcut değilse yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="57e09-125">Create a new resource group if one does not exist.</span></span>
5. <span data-ttu-id="57e09-126">Merhaba dağıtımını test edin.</span><span class="sxs-lookup"><span data-stu-id="57e09-126">Test hello deployment.</span></span>
6. <span data-ttu-id="57e09-127">İsterseniz, hello dağıtım modunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="57e09-127">If desired, set hello deployment mode.</span></span>
7. <span data-ttu-id="57e09-128">Merhaba şablon dağıtın.</span><span class="sxs-lookup"><span data-stu-id="57e09-128">Deploy hello template.</span></span>

<span data-ttu-id="57e09-129">Azure Resource Manager şablonları dağıtma hakkında tam bilgi için bkz: [kaynakları Azure Resource Manager şablonları ile dağıtma][Deploy resources with Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="57e09-129">For complete information about deploying Azure Resource Manager templates, see [Deploy resources with Azure Resource Manager templates][Deploy resources with Azure Resource Manager templates].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="57e09-130">PowerShell yükleme</span><span class="sxs-lookup"><span data-stu-id="57e09-130">Install PowerShell</span></span>

<span data-ttu-id="57e09-131">Merhaba yönergeleri takip ederek Azure PowerShell'i yükleme [Azure PowerShell ile çalışmaya başlama](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="57e09-131">Install Azure PowerShell by following hello instructions in [Getting started with Azure PowerShell](/powershell/azure/get-started-azureps).</span></span>

### <a name="create-a-template"></a><span data-ttu-id="57e09-132">Şablon oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e09-132">Create a template</span></span>

<span data-ttu-id="57e09-133">Kopya veya kopya hello [201-servicebus--kuyruk oluşturma](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) github'dan şablon:</span><span class="sxs-lookup"><span data-stu-id="57e09-133">Clone or copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) template from GitHub:</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
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

### <a name="create-a-parameters-file-optional"></a><span data-ttu-id="57e09-134">Bir parametre dosyası (isteğe bağlı) oluşturun</span><span class="sxs-lookup"><span data-stu-id="57e09-134">Create a parameters file (optional)</span></span>

<span data-ttu-id="57e09-135">toouse bir isteğe bağlı parametreler dosya kopyalama hello [201-servicebus--kuyruk oluşturma](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) dosya.</span><span class="sxs-lookup"><span data-stu-id="57e09-135">toouse an optional parameters file, copy hello [201-servicebus-create-queue](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) file.</span></span> <span data-ttu-id="57e09-136">Hello değerini `serviceBusNamespaceName` hello adıyla hello Service Bus ad alanı bu dağıtımdaki toocreate istediğiniz ve hello değerini değiştirin `serviceBusQueueName` toocreate istediğiniz hello sırasının hello adı.</span><span class="sxs-lookup"><span data-stu-id="57e09-136">Replace hello value of `serviceBusNamespaceName` with hello name of hello Service Bus namespace you want toocreate in this deployment, and replace hello value of `serviceBusQueueName` with hello name of hello queue you want toocreate.</span></span>

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

<span data-ttu-id="57e09-137">Daha fazla bilgi için bkz: Merhaba [parametreleri](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) konu.</span><span class="sxs-lookup"><span data-stu-id="57e09-137">For more information, see hello [Parameters](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) topic.</span></span>

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a><span data-ttu-id="57e09-138">İçinde tooAzure oturum ve hello Azure aboneliği ayarlama</span><span class="sxs-lookup"><span data-stu-id="57e09-138">Log in tooAzure and set hello Azure subscription</span></span>

<span data-ttu-id="57e09-139">Bir PowerShell isteminden hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="57e09-139">From a PowerShell prompt, run hello following command:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="57e09-140">İstendiğinde toolog tooyour Azure hesabı üzerinde var.</span><span class="sxs-lookup"><span data-stu-id="57e09-140">You are prompted toolog on tooyour Azure account.</span></span> <span data-ttu-id="57e09-141">Oturum açtıktan sonra komut tooview aşağıdaki hello kullanılabilir aboneliklerinizi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="57e09-141">After logging on, run hello following command tooview your available subscriptions.</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="57e09-142">Bu komut kullanılabilir Azure Aboneliklerin listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="57e09-142">This command returns a list of available Azure subscriptions.</span></span> <span data-ttu-id="57e09-143">Merhaba aşağıdaki komutu çalıştırarak geçerli oturumun hello için bir abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="57e09-143">Choose a subscription for hello current session by running hello following command.</span></span> <span data-ttu-id="57e09-144">Değiştir `<YourSubscriptionId>` hello Azure aboneliği için hello GUID ile toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="57e09-144">Replace `<YourSubscriptionId>` with hello GUID for hello Azure subscription you want toouse.</span></span>

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a><span data-ttu-id="57e09-145">Merhaba kaynak grubunu Ayarla</span><span class="sxs-lookup"><span data-stu-id="57e09-145">Set hello resource group</span></span>

<span data-ttu-id="57e09-146">Grup, hello ile yeni bir kaynak grubu oluşturmak için mevcut bir kaynağı yoksa ** New-AzureRmResourceGroup ** komutu.</span><span class="sxs-lookup"><span data-stu-id="57e09-146">If you do not have an existing resource group, create a new resource group with hello **New-AzureRmResourceGroup ** command.</span></span> <span data-ttu-id="57e09-147">Merhaba adını hello kaynak grubunu ve toouse istediğiniz konumu belirtin.</span><span class="sxs-lookup"><span data-stu-id="57e09-147">Provide hello name of hello resource group and location you want toouse.</span></span> <span data-ttu-id="57e09-148">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="57e09-148">For example:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

<span data-ttu-id="57e09-149">Başarılı olursa, hello yeni kaynak grubu bir özeti görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="57e09-149">If successful, a summary of hello new resource group is displayed.</span></span>

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a><span data-ttu-id="57e09-150">Merhaba dağıtımı test etme</span><span class="sxs-lookup"><span data-stu-id="57e09-150">Test hello deployment</span></span>

<span data-ttu-id="57e09-151">Merhaba çalıştırarak, dağıtımınızı doğrulama `Test-AzureRmResourceGroupDeployment` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="57e09-151">Validate your deployment by running hello `Test-AzureRmResourceGroupDeployment` cmdlet.</span></span> <span data-ttu-id="57e09-152">Tam olarak hello dağıtım yürütülürken gibi hello dağıtım sınarken parametreleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="57e09-152">When testing hello deployment, provide parameters exactly as you would when executing hello deployment.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a><span data-ttu-id="57e09-153">Merhaba dağıtımı oluşturma</span><span class="sxs-lookup"><span data-stu-id="57e09-153">Create hello deployment</span></span>

<span data-ttu-id="57e09-154">Merhaba çalıştırmak toocreate hello yeni dağıtım `New-AzureRmResourceGroupDeployment` cmdlet'ini ve istendiğinde hello gerekli parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="57e09-154">toocreate hello new deployment, run hello `New-AzureRmResourceGroupDeployment` cmdlet, and provide hello necessary parameters when prompted.</span></span> <span data-ttu-id="57e09-155">Merhaba parametreleri dağıtımınıza, kaynak grubu ve hello yolu veya URL'si toohello şablon dosyası hello adı için bir ad içerir.</span><span class="sxs-lookup"><span data-stu-id="57e09-155">hello parameters include a name for your deployment, hello name of your resource group, and hello path or URL toohello template file.</span></span> <span data-ttu-id="57e09-156">Merhaba, **modu** parametresi belirtilmezse, varsayılan değeri hello **artımlı** kullanılır.</span><span class="sxs-lookup"><span data-stu-id="57e09-156">If hello **Mode** parameter is not specified, hello default value of **Incremental** is used.</span></span> <span data-ttu-id="57e09-157">Daha fazla bilgi için bkz: [artımlı ve tam dağıtımları](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span><span class="sxs-lookup"><span data-stu-id="57e09-157">For more information, see [Incremental and complete deployments](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).</span></span>

<span data-ttu-id="57e09-158">komut istemlerini hello PowerShell penceresinde hello üç parametreler için hello:</span><span class="sxs-lookup"><span data-stu-id="57e09-158">hello following command prompts you for hello three parameters in hello PowerShell window:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

<span data-ttu-id="57e09-159">toospecify bir parametre dosyası, bunun yerine, komutu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="57e09-159">toospecify a parameters file instead, use hello following command.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

<span data-ttu-id="57e09-160">Merhaba deployment cmdlet'ini çalıştırdığınızda, satır içi parametreleri de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="57e09-160">You can also use inline parameters when you run hello deployment cmdlet.</span></span> <span data-ttu-id="57e09-161">Merhaba komut aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="57e09-161">hello command is as follows:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

<span data-ttu-id="57e09-162">toorun bir [tam](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) dağıtım, kümesi hello **modu** parametresi çok**tam**:</span><span class="sxs-lookup"><span data-stu-id="57e09-162">toorun a [complete](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) deployment, set hello **Mode** parameter too**Complete**:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a><span data-ttu-id="57e09-163">Merhaba dağıtımı doğrulama</span><span class="sxs-lookup"><span data-stu-id="57e09-163">Verify hello deployment</span></span>
<span data-ttu-id="57e09-164">Merhaba kaynakları başarıyla dağıtılan hello dağıtım özetini hello PowerShell penceresinde görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="57e09-164">If hello resources are deployed successfully, a summary of hello deployment is displayed in hello PowerShell window:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="57e09-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="57e09-165">Next steps</span></span>
<span data-ttu-id="57e09-166">Şimdi hello temel iş akışı ve Azure Resource Manager şablonunu dağıtmak için komutları gördünüz.</span><span class="sxs-lookup"><span data-stu-id="57e09-166">You've now seen hello basic workflow and commands for deploying an Azure Resource Manager template.</span></span> <span data-ttu-id="57e09-167">Daha ayrıntılı bilgi için bağlantılar aşağıdaki hello ziyaret edin:</span><span class="sxs-lookup"><span data-stu-id="57e09-167">For more detailed information, visit hello following links:</span></span>

* <span data-ttu-id="57e09-168">[Azure Resource Manager'a genel bakış][Azure Resource Manager overview]</span><span class="sxs-lookup"><span data-stu-id="57e09-168">[Azure Resource Manager overview][Azure Resource Manager overview]</span></span>
* <span data-ttu-id="57e09-169">[Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtma][Deploy resources with Azure Resource Manager templates]</span><span class="sxs-lookup"><span data-stu-id="57e09-169">[Deploy resources with Resource Manager templates and Azure PowerShell][Deploy resources with Azure Resource Manager templates]</span></span>
* [<span data-ttu-id="57e09-170">Azure Resource Manager şablonları yazma</span><span class="sxs-lookup"><span data-stu-id="57e09-170">Authoring Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
