---
title: "Azure Ağ İzleyicisi IP akış doğrulama - Azure CLI ile aaaVerify trafiği | Microsoft Docs"
description: "Bu makalede nasıl bir sanal makineden trafiği tooor izin verilen ya da Azure CLI kullanarak reddedildi toocheck"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 128a00b4296994551e7e17838a51e6d9de180e21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Trafik izin veya tooor VM IP akış doğrulayın ile Azure Ağ İzleyicisi bileşeni reddedildi olmadığını denetleyin

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API'si](network-watcher-check-ip-flow-verify-rest.md)


IP akış doğrulayın Ağ İzleyicisinin, trafiği bir sanal makineden tooor izin verilip verilmediğini tooverify sağlayan bir özelliktir. Bu senaryo kullanışlı tooget bir sanal makine tooan dış kaynak veya arka uç iletişim kurabilirsiniz, geçerli bir durumda olur. IP akış doğrulayın olabilir kullanılan tooverify ağ güvenlik grubu (NSG) kurallarınızı düzgün şekilde yapılandırılırsa ve NSG kuralları tarafından engellenen akışları sorun giderme. IP kullanan başka bir nedeni akış durumda engellenen istediğiniz tooensure trafiği engellenmiş düzgün şekilde NSG hello tarafından doğrulayın.

Bu makalede bizim nesil CLI hello kaynak yönetimi dağıtım modeli için Azure CLI 2.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.

Bu makaledeki adımları tooperform Merhaba, çok ihtiyacınız[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturmak](network-watcher-create.md) toocreate bir Ağ İzleyicisi'ni veya mevcut bir Ağ İzleyicisi örneği. Merhaba senaryo da geçerli bir sanal makine ile bir kaynak grubu kullanılan toobe var olduğunu varsayar.

## <a name="scenario"></a>Senaryo

Bu senaryo bir sanal makine tooa bilinen geçebildiğinden akış IP doğrulayın tooverify kullanıyorsa Bing IP adresi. Merhaba trafik reddedilirse, bu trafiğin reddediyor hello güvenlik kuralı döndürür. IP akış doğrulayın, hakkında daha fazla toolearn ziyaret [IP akış doğrulayın genel bakış](network-watcher-ip-flow-verify-overview.md)

## <a name="get-a-vm"></a>VM Al

IP akış testleri trafiği tooor bir sanal makine tooor uzaktan bir hedef üzerinde bir IP adresinden doğrulayın. Bir sanal makine kimliği hello cmdlet'i için gereklidir. Merhaba sanal makine toouse hello Kimliğini biliyorsanız, bu adımı atlayabilirsiniz.

```azurecli
az vm show --resource-group MyResourceGroup5431 --name MyVM-Web
```

## <a name="get-hello-nics"></a>Merhaba NIC alma

Bu örnekte, bir sanal makinede hello NIC'ler alıyoruz hello sanal makinede bir NIC Hello IP adresi gereklidir. Başlangıç IP adresini biliyorsanız tootest istediğiniz hello sanal makinede, bu adımı atlayabilirsiniz.

```azurecli
az network nic show --resource-group MyResourceGroup5431 --name MyNic-Web
```

## <a name="run-ip-flow-verify"></a>Çalışma IP akış doğrulayın

Toorun hello cmdlet hello bilgi sahibiz, biz hello çalıştırmak `az network watcher test-ip-flow` cmdlet tootest hello trafiği. Bu örnekte, hello ilk IP adresi hello ilk NIC üzerinde kullanıyoruz

```azurecli
az network watcher test-ip-flow --resource-group resourceGroupName --direction directionInboundorOutbound --protocol protocolTCPorUDP --local ipAddressandPort --remote ipAddressandPort --vm vmNameorID --nic nicNameorID
```

> [!NOTE]
> IP akış doğrulayın gerektirir hello VM kaynak toorun ayrılır.

## <a name="review-results"></a>Sonuçları gözden geçirin

Çalıştırdıktan sonra `az network watcher test-ip-flow` hello sonuçlarının döndürüldüğü, hello aşağıdaki adım önceki hello döndürülen hello sonuçları bir örnektir.

```azurecli
{
    "access": "Allow",
    "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

## <a name="next-steps"></a>Sonraki adımlar

Trafik engelleniyor ve olmamalıdır, bkz: [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tanımlanan hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.

Tooaudit NSG ayarlarınızı ziyaret ederek bilgi [denetim ağ güvenlik grupları (NSG) Ağ İzleyicisi ile](network-watcher-nsg-auditing-powershell.md).

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png
