---
title: "aaaUse PowerShell toomanage Azure Service Bus kaynaklarını | Microsoft Docs"
description: "PowerShell modülü toocreate kullanma ve Service Bus kaynaklarını yönetme"
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a>PowerShell toomanage Service Bus kaynaklarını kullanma

Microsoft Azure PowerShell toocontrol kullanın ve hello dağıtımını ve Azure Hizmetleri yönetimini otomatikleştirmek bir komut dosyası ortamıdır. Bu makalede nasıl toouse hello [Service Bus Resource Manager PowerShell Modülü](/powershell/module/azurerm.servicebus) tooprovision ve hizmet veri yolu varlıklarını (ad alanları, kuyruklar, konular ve abonelikler) yönetmek yerel bir Azure PowerShell konsolunu kullanarak veya komut dosyası.

Hizmet veri yolu varlıklarını Azure Resource Manager şablonları kullanarak da yönetebilirsiniz. Daha fazla bilgi için hello makalesine bakın [oluşturma Service Bus kaynaklarını Azure Resource Manager şablonları kullanarak](service-bus-resource-manager-overview.md).

## <a name="prerequisites"></a>Ön koşullar

Başlamadan önce hello aşağıdakiler gerekir:

* Azure aboneliği. Bir aboneliği edinme hakkında daha fazla bilgi için bkz: [satın alma seçeneği][purchase options], [üye teklifleri][member offers], veya [boş Hesap][free account].
* Azure PowerShell ile bir bilgisayar. Yönergeler için bkz: [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/get-started-azureps).
* PowerShell komut dosyaları, NuGet paketlerini ve hello .NET Framework genel anlama.

## <a name="get-started"></a>başlarken

Merhaba ilk toouse PowerShell toolog tooyour Azure hesabı olarak ve Azure aboneliğine adımdır. Merhaba yönergeleri izleyin [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/get-started-azureps) toolog tooyour Azure hesabı ve Azure aboneliğinizde almak ve erişim hello kaynakları.

## <a name="provision-a-service-bus-namespace"></a>Bir hizmet veri yolu ad alanı sağlama

Hizmet veri yolu ad alanları ile çalışırken hello kullanabilirsiniz [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [yeni AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), ve [kümesi AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlet'leri.

Bu örnek, birkaç yerel değişkenler hello komut dosyasında oluşturur; `$Namespace` ve `$Location`.

* `$Namespace`Merhaba Service Bus ad alanı toowork ile istiyoruz Hello adıdır.
* `$Location`Merhaba veri merkezinde hangi tanımlayan hello ad sağlamak.
* `$CurrentNamespace`Biz almak (veya oluşturduğunuz) hello başvuru ad alanı depolar.

Gerçek bir betik içinde `$Namespace` ve `$Location` parametre olarak geçirilebilir.

Merhaba komut dosyasının bu bölümü, aşağıdaki hello:

1. Deneme tooretrieve hello ile Service Bus ad alanı adı belirtildi.
2. Merhaba ad bulunursa, bulunanları bildirir.
3. Merhaba ad alanı bulunmazsa hello ad alanı oluşturur ve sonra yeni ad alanı oluşturulan hello alır.
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a>Ad alanı yetkilendirme kuralı oluştur

Merhaba aşağıdaki örnekte nasıl toomanage ad alanı yetkilendirme kurallarını kullanarak hello gösterir [yeni AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Kümesi AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), ve [Kaldır AzureRmServiceBusNamespaceAuthorizationRule cmdlet'leri](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a>Bir kuyruk oluşturma

toocreate bir kuyruk veya konu hello önceki bölümde hello komut dosyası kullanarak bir ad alanı denetimi gerçekleştirir. Ardından, hello kuyruk oluşturun:

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a>Sıra özelliklerini değiştir

Önceki bölümde hello Hello betiği yürüttükten sonra hello kullanabilirsiniz [kümesi AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate hello aşağıdaki örneğine hello gibi bir sıranın özelliklerini:

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a>Diğer hizmet veri yolu varlıklarını sağlama

Merhaba kullanabilirsiniz [Service Bus PowerShell modülünü](/powershell/module/azurerm.servicebus) tooprovision konu başlıkları ve abonelikler gibi diğer varlıklar. Bu cmdlet'ler sözdizimsel olarak benzer toohello kuyruk oluşturma cmdlet'leri hello önceki bölümde gösterilen ' dir.

## <a name="next-steps"></a>Sonraki adımlar

- Merhaba tam Service Bus Resource Manager PowerShell modülü belgelerine bakın [burada](/powershell/module/azurerm.servicebus). Bu sayfa, tüm kullanılabilir cmdlet'leri listeler.
- Azure Resource Manager şablonları kullanma hakkında daha fazla bilgi için hello makalesine bakın [oluşturma Service Bus kaynaklarını Azure Resource Manager şablonları kullanarak](service-bus-resource-manager-overview.md).
- Hakkında bilgi [Service Bus .NET Yönetim kitaplıklarını](service-bus-management-libraries.md).

Bazı alternatif yolu vardır toomanage Service Bus varlıklar, bu Web günlüğü postaları açıklandığı gibi:

* [Nasıl toocreate Service Bus kuyrukları, konuları ve abonelikleri bir PowerShell Betiği kullanılarak](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Nasıl toocreate Service Bus Namespace ve bir Event Hub'ın bir PowerShell komut dosyası kullanma](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [Hizmet veri yolu PowerShell betikleri](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
