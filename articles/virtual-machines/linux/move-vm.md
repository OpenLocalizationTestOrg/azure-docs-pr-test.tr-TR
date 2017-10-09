---
title: aaaMove azure'da bir Linux VM | Microsoft Docs
description: "Bir Linux VM tooanother Azure abonelik veya kaynak grubu hello Resource Manager dağıtım modelinde taşıyın."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a>Bir Linux VM tooanother abonelik veya kaynak grubu taşıma
Bu makalede nasıl anlatılmaktadır toomove bir Linux VM kaynak grupları veya abonelikler arasında. Bir VM abonelikler arasında taşıma kişisel bir abonelikte VM oluşturduysanız elinizin altında kullanılabilir ve şimdi toomove istediğiniz onu tooyour şirketin abonelik.

> [!IMPORTANT]
>Şu anda yönetilen diskleri taşınamıyor. 
>
>Yeni kaynak kimlikleri hello taşıma bir parçası olarak oluşturulur. Merhaba VM taşındıktan sonra Araçlar ve komut dosyaları toouse hello yeni kaynak kimlikleri tooupdate gerekir. 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a>Hello Azure CLI toomove VM kullanın
toosuccessfully VM taşımak, toomove hello VM ve tüm destekleyici kaynakları gerekir. Kullanım hello **azure Grup Göster** toolist tüm hello kaynaklar bir kaynak grubu ve kimlikleri komutu. Böylece kopyalayıp hello kimlikleri Yapıştır sonraki komutları toopipe hello bu komut tooa dosyasını çıkışını yardımcı olur.

    azure group show <resourceGroupName>

toomove VM ve kendi kaynakları tooanother kaynak grubu kullanmak hello **azure kaynak taşıma** CLI komutu. Aşağıdaki örneğine hello nasıl toomove VM ve hello en yaygın kaynakları gerektirdiği gösterir. Merhaba kullanırız **-i** parametre ve bir virgülle ayrılmış listesi (boşluksuz) kimlikleri için hello kaynakları toomove geçirin.

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

Toomove istiyorsanız, VM ve kaynakları tooa farklı aboneliğini Merhaba, hello eklemek **--hedef-Subscriptionıd &#60; destinationSubscriptionID &#62;** parametresi toospecify hello hedef abonelik.

Bir Windows bilgisayarda bir komut istemi hello çalışıyorsanız, tooadd gereken bir  **$**  bunları bildirirken değişken adları Merhaba öne. Bu Linux gerekli değildir.

Bunu Sorduğunuza toomove hello istediğiniz tooconfirm belirtilen kaynak. Tür **Y** tooconfirm toomove hello kaynakları istiyor.

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a>Sonraki adımlar
Birçok farklı türdeki kaynakların kaynak grupları ve abonelikler arasında taşıyabilirsiniz. Daha fazla bilgi için bkz: [kaynakları toonew kaynak grubuna veya aboneliğe taşıma](../../resource-group-move-resources.md).    

