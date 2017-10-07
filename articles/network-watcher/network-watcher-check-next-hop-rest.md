---
title: "aaaFind sonraki atlama Azure Ağ İzleyicisi sonraki atlama - REST ile | Microsoft Docs"
description: "Bu makalede nasıl hangi hello sonraki atlama türü olan ve sonraki atlama kullanarak IP adresi hello Azure REST API bulabilirsiniz açıklayın"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a>Hangi hello sonraki atlama türü hello sonraki atlama yetenek Azure REST API'sini kullanarak işlemleri Ağ İzleyicisi içinde kullandığını bulmak

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-next-hop-cli.md)
> - [Azure REST API'si](network-watcher-check-next-hop-rest.md)

Sonraki atlama bir özelliği olan Ağ İzleyicisi'hello yeteneği sağlar, hello sonraki atlama türü ve belirtilen bir sanal makineye dayalı IP adresi al ' dir. Bu özellik, bir sanal makine trafiğe bir ağ geçidi, internet veya sanal ağlar tooget tooits hedef geçiyorsa belirlemede yararlıdır.

## <a name="before-you-begin"></a>Başlamadan önce

ARMclient PowerShell kullanarak kullanılan toocall hello REST API ' dir. ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.

## <a name="scenario"></a>Senaryo

Bu makalede ele alınan hello senaryosu, sonraki atlama, bir özelliği olan Ağ İzleyicisi'hello sonraki atlama türü ve IP adresi için bir kaynak bulur kullanır. Sonraki atlama, hakkında daha fazla toolearn ziyaret [sonraki atlama genel bakış](network-watcher-next-hop-overview.md).

Bu senaryoda, şunları yapacaksınız:

* Bir sanal makine için sonraki atlama Hello alın.

## <a name="log-in-with-armclient"></a>Oturum ARMClient oturum

İçinde tooarmclient Azure kimlik bilgilerinizle oturum açın.

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a>Bir sanal makine alma

Komut dosyası tooreturn aşağıdaki hello bir sanal makine çalıştırın. Bu bilgiler sonraki atlama çalıştırmak için gereklidir.

koddan hello Merhaba değişkenleri aşağıdaki değerleri gerekir:

- **Subscriptionıd** -abonelik kimliği toouse hello.
- **resourceGroupName** - hello sanal makine içeren bir kaynak grubu adı.

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

Çıktı hello aşağıdakiler arasından hello kimliği hello sanal makinenin örnek aşağıdaki hello kullanılır:

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a>Sonraki atlama Al

Merhaba authorization üstbilgisi oluşturulduktan sonra bir sanal makineden hello sonraki atlama alınabilir. Merhaba aşağıdaki değerleri hello kod örnek toowork için değiştirilmesi gerekir.

> [!Important]
> Ağ İzleyicisi REST API çağrıları hello tanılama eylemleri gerçekleştirdiğiniz hello kaynakları değil hello Ağ İzleyicisi'ni içeren hello kaynak grubunu URI'dir hello isteğindeki kaynak grubu adı hello.

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> Sonraki atlama hello VM kaynak toorun ayrılır gerektirir.

## <a name="results"></a>Sonuçlar

Merhaba aşağıdaki kod parçacığında, alınan hello çıkış örneğidir. Merhaba sonuçları değerleri aşağıdaki hello içerir:

* **nextHopType** -bu değer değerleri aşağıdaki hello biridir: Internet değerinin VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway veya yok.
* **Nexthopıpaddress** -hello hello sonraki atlamanın IP adresi.
* **routeTableId** - hello değerdir hello rota ile ilişkili hello yol tablosu için bir ya da bir URI veya kullanıcı tanımlı Hayır ise rota tanımlı hello değeri *sistem yolu* döndürülür.

Merhaba, json biçiminde hello sonuçları verilmiştir.

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a>Sonraki adımlar

Bir sanal makine için sonraki atlama hello çıkışı mümkün toofind işlendikten sonra ağ kaynaklarının hello güvenlik ziyaret ederek görüntüleyebilirsiniz [güvenlik görünümüne genel bakış](network-watcher-security-group-view-overview.md)














