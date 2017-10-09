---
title: "aaaUse PowerShell toomanage Azure Event Hubs kaynakları | Microsoft Docs"
description: "PowerShell modülü toocreate kullanma ve olay hub'ları yönetme"
services: event-hubs
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: d79cb307c2b4a031d059ce6ca67117ffc0b4600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-event-hubs-resources"></a>PowerShell toomanage olay hub'ları kaynakları kullanın

Microsoft Azure PowerShell toocontrol kullanın ve hello dağıtımını ve Azure Hizmetleri yönetimini otomatikleştirmek bir komut dosyası ortamıdır. Bu makalede nasıl toouse hello [olay hub'ları Resource Manager PowerShell Modülü](/powershell/module/azurerm.eventhub) tooprovision ve Event Hubs varlıkları (ad, tek tek olay hub'ları ve tüketici grupları) yönetmek yerel bir Azure PowerShell konsolunu kullanarak veya komut dosyası.

Olay hub'ları kaynakları Azure Resource Manager şablonları kullanarak da yönetebilirsiniz. Daha fazla bilgi için hello makalesine bakın [bir Azure Resource Manager şablonu kullanarak olay hub'ı ve tüketici grubu ile bir olay hub'ları ad alanı oluşturma](event-hubs-resource-manager-namespace-event-hub.md).

## <a name="prerequisites"></a>Ön koşullar

Başlamadan önce hello aşağıdakiler gerekir:

* Azure aboneliği. Bir aboneliği edinme hakkında daha fazla bilgi için bkz: [satın alma seçeneği][purchase options], [üye teklifleri][member offers], veya [boş Hesap][free account].
* Azure PowerShell ile bir bilgisayar. Yönergeler için bkz: [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/get-started-azureps).
* PowerShell komut dosyaları, NuGet paketlerini ve hello .NET Framework genel anlama.

## <a name="get-started"></a>başlarken

Merhaba ilk toouse PowerShell toolog tooyour Azure hesabı olarak ve Azure aboneliğine adımdır. Merhaba yönergeleri izleyin [Azure PowerShell cmdlet'leri kullanmaya başlama](/powershell/azure/get-started-azureps) tooyour Azure hesabı toolog sonra almak ve Azure aboneliğinizde hello kaynaklarına erişim.

## <a name="provision-an-event-hubs-namespace"></a>Bir olay hub'ları ad alanı sağlama

Olay hub'ları ad alanları ile çalışırken hello kullanabilirsiniz [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [yeni AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Kaldır AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , ve [kümesi AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlet'leri.

Bu örnek, birkaç yerel değişkenler hello komut dosyasında oluşturur; `$Namespace` ve `$Location`.

* `$Namespace`Merhaba toowork ile istiyoruz hello olay hub'ları ad alanının adıdır.
* `$Location`Merhaba veri merkezinde hangi tanımlayan hello ad sağlamak.
* `$CurrentNamespace`Biz almak (veya oluşturduğunuz) hello başvuru ad alanı depolar.

Gerçek bir betik içinde `$Namespace` ve `$Location` parametre olarak geçirilebilir.

Merhaba komut dosyasının bu bölümü, aşağıdaki hello:

1. Deneme tooretrieve hello bir olay hub'ları ad alanı adı belirtildi.
2. Merhaba ad bulunursa, bulunanları bildirir.
3. Merhaba ad alanı bulunmazsa hello ad alanı oluşturur ve sonra yeni ad alanı oluşturulan hello alır.

    ```powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a>Olay hub’ı oluşturma

toocreate bir event hub hello önceki bölümde hello komut dosyası kullanarak bir ad alanı denetimi gerçekleştirin. Ardından hello kullanın [yeni AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello olay hub'ı:

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "hello event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $EventHubName event hub does not exist."
    Write-Host "Creating hello $EventHubName event hub in hello $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $EventHubName event hub in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a>Bir tüketici grubu oluştur

toocreate bir event hub tüketici grubunda hello önceki bölümde hello komut dosyalarını kullanarak hello ad alanı ve olay hub'ı denetimleri gerçekleştirin. Ardından hello kullanın [yeni AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello tüketici grubu hello olay hub'ı içinde. Örneğin:

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "hello consumer group $ConsumerGroupName in event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating hello $ConsumerGroupName consumer group in hello $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a>Set kullanıcı meta verileri

Önceki bölümlerde hello Hello betikleri yürüttükten sonra hello kullanabilirsiniz [kümesi AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate hello aşağıdaki örneğine hello gibi bir tüketici grubu özelliklerini:

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a>Olay hub'ı kaldırma

oluşturduğunuz tooremove hello olay hub'ları, kullanabileceğiniz hello `Remove-*` aşağıdaki örneğine hello olduğu gibi cmdlet:

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a>Sonraki adımlar

- Merhaba tam olay hub'ları Resource Manager PowerShell modülü belgelerine bakın [burada](/powershell/module/azurerm.eventhub). Bu sayfa, tüm kullanılabilir cmdlet'leri listeler.
- Azure Resource Manager şablonları kullanma hakkında daha fazla bilgi için bkz: hello makale [bir Azure Resource Manager şablonu kullanarak olay hub'ı ve tüketici grubu ile bir olay hub'ları ad alanı oluşturma](event-hubs-resource-manager-namespace-event-hub.md).
- Hakkında bilgi [olay hub'ları .NET Yönetim kitaplıklarını](event-hubs-management-libraries.md).

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
