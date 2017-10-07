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
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a>Azure Resource Manager şablonları kullanarak Service Bus kaynakları oluşturun

Bu makalede nasıl toocreate ve Service Bus kaynaklarını Azure Resource Manager şablonları, PowerShell ve hello Service Bus kaynak sağlayıcısı kullanarak dağıtın.

Azure Resource Manager şablonları şunları hello kaynakları toodeploy bir çözüm ve toospecify parametreleri ve farklı ortamlar için tooinput değerleri etkinleştir değişkenleri için tanımlamanıza yardımcı olur. JSON ve dağıtımınız için tooconstruct değerleri kullanabileceğiniz ifadeler Hello şablonu oluşur. Azure Resource Manager şablonları ve tartışma hello şablon biçimi için yazma hakkında ayrıntılı bilgi için bkz: [yapısı ve Azure Resource Manager şablonları sözdizimini](../azure-resource-manager/resource-group-authoring-templates.md).

> [!NOTE]
> Bu makale Göster örneklerde nasıl hello toouse Azure Resource Manager toocreate bir hizmet veri yolu ad alanı ve varlık (kuyruk) Mesajlaşma. Diğer şablon örnekler için hello ziyaret [Azure hızlı başlangıç Şablon Galerisi] [ Azure Quickstart Templates gallery] ve "Service Bus" için arama
>
>

## <a name="service-bus-resource-manager-templates"></a>Hizmet veri yolu Resource Manager şablonları

Bu hizmet veri yolu Azure Resource Manager şablonları, yükleme ve dağıtım için kullanılabilir. Her biri, github'da bağlantıları toohello şablonlarıyla hakkında ayrıntılı bilgi için bağlantılar aşağıdaki hello tıklatın:

* [Hizmet veri yolu ad alanı oluşturma](service-bus-resource-manager-namespace.md)
* [Sıra ile Service Bus ad alanı oluşturma](service-bus-resource-manager-namespace-queue.md)
* [Hizmet veri yolu ad alanı konu ve abonelik oluşturma](service-bus-resource-manager-namespace-topic.md)
* [Kuyruk ve yetkilendirme kuralı ile Service Bus ad alanı oluşturma](service-bus-resource-manager-namespace-auth-rule.md)
* [Konu, abonelik ve kuralı ile Service Bus ad alanı oluşturma](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a>PowerShell ile dağıtma

Merhaba aşağıdaki yordamda açıklanmıştır nasıl toouse PowerShell toodeploy bir Azure Resource Manager şablonu oluşturan bir **standart** Service Bus ad alanı ve bu ad alanı içindeki bir sıra katmanı. Bu örnekte hello üzerinde temel [sıra ile Service Bus ad alanı oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) şablonu. Merhaba yaklaşık iş akışı aşağıdaki gibidir:

1. PowerShell yükleyin.
2. Merhaba şablonu ve (isteğe bağlı) bir parametre dosyası oluşturun.
3. PowerShell'de tooyour Azure hesabı oturum açın.
4. Bir mevcut değilse yeni bir kaynak grubu oluşturun.
5. Merhaba dağıtımını test edin.
6. İsterseniz, hello dağıtım modunu ayarlayın.
7. Merhaba şablon dağıtın.

Azure Resource Manager şablonları dağıtma hakkında tam bilgi için bkz: [kaynakları Azure Resource Manager şablonları ile dağıtma][Deploy resources with Azure Resource Manager templates].

### <a name="install-powershell"></a>PowerShell yükleme

Merhaba yönergeleri takip ederek Azure PowerShell'i yükleme [Azure PowerShell ile çalışmaya başlama](/powershell/azure/get-started-azureps).

### <a name="create-a-template"></a>Şablon oluşturma

Kopya veya kopya hello [201-servicebus--kuyruk oluşturma](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) github'dan şablon:

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

### <a name="create-a-parameters-file-optional"></a>Bir parametre dosyası (isteğe bağlı) oluşturun

toouse bir isteğe bağlı parametreler dosya kopyalama hello [201-servicebus--kuyruk oluşturma](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) dosya. Hello değerini `serviceBusNamespaceName` hello adıyla hello Service Bus ad alanı bu dağıtımdaki toocreate istediğiniz ve hello değerini değiştirin `serviceBusQueueName` toocreate istediğiniz hello sırasının hello adı.

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

Daha fazla bilgi için bkz: Merhaba [parametreleri](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) konu.

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a>İçinde tooAzure oturum ve hello Azure aboneliği ayarlama

Bir PowerShell isteminden hello aşağıdaki komutu çalıştırın:

```powershell
Login-AzureRmAccount
```

İstendiğinde toolog tooyour Azure hesabı üzerinde var. Oturum açtıktan sonra komut tooview aşağıdaki hello kullanılabilir aboneliklerinizi çalıştırın.

```powershell
Get-AzureRMSubscription
```

Bu komut kullanılabilir Azure Aboneliklerin listesini döndürür. Merhaba aşağıdaki komutu çalıştırarak geçerli oturumun hello için bir abonelik seçin. Değiştir `<YourSubscriptionId>` hello Azure aboneliği için hello GUID ile toouse istiyor.

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a>Merhaba kaynak grubunu Ayarla

Grup, hello ile yeni bir kaynak grubu oluşturmak için mevcut bir kaynağı yoksa ** New-AzureRmResourceGroup ** komutu. Merhaba adını hello kaynak grubunu ve toouse istediğiniz konumu belirtin. Örneğin:

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

Başarılı olursa, hello yeni kaynak grubu bir özeti görüntülenir.

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a>Merhaba dağıtımı test etme

Merhaba çalıştırarak, dağıtımınızı doğrulama `Test-AzureRmResourceGroupDeployment` cmdlet'i. Tam olarak hello dağıtım yürütülürken gibi hello dağıtım sınarken parametreleri sağlar.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a>Merhaba dağıtımı oluşturma

Merhaba çalıştırmak toocreate hello yeni dağıtım `New-AzureRmResourceGroupDeployment` cmdlet'ini ve istendiğinde hello gerekli parametreleri belirtin. Merhaba parametreleri dağıtımınıza, kaynak grubu ve hello yolu veya URL'si toohello şablon dosyası hello adı için bir ad içerir. Merhaba, **modu** parametresi belirtilmezse, varsayılan değeri hello **artımlı** kullanılır. Daha fazla bilgi için bkz: [artımlı ve tam dağıtımları](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).

komut istemlerini hello PowerShell penceresinde hello üç parametreler için hello:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

toospecify bir parametre dosyası, bunun yerine, komutu aşağıdaki hello kullanın.

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

Merhaba deployment cmdlet'ini çalıştırdığınızda, satır içi parametreleri de kullanabilirsiniz. Merhaba komut aşağıdaki gibidir:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

toorun bir [tam](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) dağıtım, kümesi hello **modu** parametresi çok**tam**:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a>Merhaba dağıtımı doğrulama
Merhaba kaynakları başarıyla dağıtılan hello dağıtım özetini hello PowerShell penceresinde görüntülenir:

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

## <a name="next-steps"></a>Sonraki adımlar
Şimdi hello temel iş akışı ve Azure Resource Manager şablonunu dağıtmak için komutları gördünüz. Daha ayrıntılı bilgi için bağlantılar aşağıdaki hello ziyaret edin:

* [Azure Resource Manager'a genel bakış][Azure Resource Manager overview]
* [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtma][Deploy resources with Azure Resource Manager templates]
* [Azure Resource Manager şablonları yazma](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
