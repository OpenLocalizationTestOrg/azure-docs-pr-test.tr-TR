---
title: aaaMove Azure Windows VM kaynak | Microsoft Docs
description: "Bir Windows VM tooanother Azure abonelik veya kaynak grubu hello Resource Manager dağıtım modelinde taşıyın."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 859e78dce9acf1168780d4ee8e9f6dac0e3c11cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-windows-vm-tooanother-azure-subscription-or-resource-group"></a>Bir Windows VM tooanother Azure abonelik veya kaynak grubu taşıma
Bu makalede nasıl anlatılmaktadır toomove bir Windows VM kaynak grupları veya abonelikler arasında. Abonelikler arasında taşıma kişisel bir abonelikte ilk olarak bir VM oluşturduysanız, kullanışlı ve şimdi toomove istiyorsanız bunu tooyour şirketin abonelik toocontinue çalışmanızı.

> [!IMPORTANT]
>Şu anda yönetilen diskleri taşınamıyor. 
>
>Yeni kaynak kimlikleri hello taşıma bir parçası olarak oluşturulur. Merhaba VM taşındıktan sonra Araçlar ve komut dosyaları toouse hello yeni kaynak kimlikleri tooupdate gerekir. 
> 
> 

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="use-powershell-toomove-a-vm"></a>PowerShell toomove VM kullanın
bir sanal makine tooanother kaynak grubu toomove, toomake, ayrıca tüm hello bağımlı kaynakları taşıdığınızdan emin gerekir. toouse hello taşıma AzureRMResource cmdlet hello kaynak adı ve kaynak hello türü gerekir. Merhaba Bul AzureRMResource cmdlet'i her ikisini de alabilirsiniz.

    Find-AzureRMResource -ResourceGroupNameContains "<sourceResourceGroupName>"


birden fazla kaynak toomove ihtiyacımız VM toomove. Yalnızca her kaynak için ayrı değişkeni oluşturun ve bunları listeleyin. Bu örnek, bir VM için hello temel kaynakların çoğunu içerir, ancak gerektiğinde daha fazla ekleyebilirsiniz.

    $sourceRG = "<sourceResourceGroupName>"
    $destinationRG = "<destinationResourceGroupName>"

    $vm = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Compute/virtualMachines" -ResourceName "<vmName>"
    $storageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<storageAccountName>"
    $diagStorageAccount = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Storage/storageAccounts" -ResourceName "<diagnosticStorageAccountName>"
    $vNet = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/virtualNetworks" -ResourceName "<vNetName>"
    $nic = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkInterfaces" -ResourceName "<nicName>"
    $ip = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/publicIPAddresses" -ResourceName "<ipName>"
    $nsg = Get-AzureRmResource -ResourceGroupName $sourceRG -ResourceType "Microsoft.Network/networkSecurityGroups" -ResourceName "<nsgName>"

    Move-AzureRmResource -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId

toomove Merhaba kaynakları toodifferent abonelik, hello dahil **- DestinationSubscriptionId** parametresi. 

    Move-AzureRmResource -DestinationSubscriptionId "<destinationSubscriptionID>" -DestinationResourceGroupName $destinationRG -ResourceId $vm.ResourceId, $storageAccount.ResourceId, $diagStorageAccount.ResourceId, $vNet.ResourceId, $nic.ResourceId, $ip.ResourceId, $nsg.ResourceId



Sizden istenir toomove hello istediğiniz tooconfirm belirtilen kaynaklar. Tür **Y** tooconfirm toomove hello kaynakları istiyor.

## <a name="next-steps"></a>Sonraki adımlar
Birçok farklı türdeki kaynakların kaynak grupları ve abonelikler arasında taşıyabilirsiniz. Daha fazla bilgi için bkz: [kaynakları toonew kaynak grubuna veya aboneliğe taşıma](../../resource-group-move-resources.md).    

