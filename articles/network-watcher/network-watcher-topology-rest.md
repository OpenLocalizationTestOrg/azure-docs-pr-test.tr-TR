---
title: "aaaView Azure Ağ İzleyicisi topolojisi - REST API | Microsoft Docs"
description: "Bu makalede, nasıl toouse REST API tooquery ağ topolojinizi anlatmaktadır."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a>Ağ İzleyicisi topolojisi REST API ile görüntüleme

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [REST API](network-watcher-topology-rest.md)

Ağ İzleyicisi Merhaba topoloji özelliği görsel bir abonelik hello ağ kaynaklarını sağlar. Merhaba Portalı'nda bu görselleştirme tooyou otomatik olarak sunulur. Merhaba topoloji görünümü hello portalında ardındaki Hello bilgileri PowerShell aracılığıyla alınabilir.
Bu özellik hello topoloji bilgilerini hello veri diğer araçları toobuild hello görselleştirme çıkışı tarafından kullanılabilecek daha verimli hale getirir.

Merhaba bağlantısı altında iki ilişki modellenir.

- **Kapsama** -örnek: VNet bir alt ağ içeren bir NIC içerir
- **İlişkili** -örnek: NIC VM ile ilişkili

Merhaba aşağıdaki hello topoloji REST API'si sorgulanırken döndürülen özellikler listelenmiştir.

* **ad** - hello hello kaynak adı
* **Kimliği** -hello kaynak URI'si hello.
* **Konum** -hello hello kaynak bulunduğu konumu.
* **ilişkileri** -ilişkilendirmeleri toohello listesini başvurulan nesne.
    * **ad** -hello hello adını başvurulan kaynak.
    * **ResourceId** -hello ResourceId olduğu hello association'ında başvurulan hello kaynağının hello URI.
    * **associationType** -bu değer hello ilişkisi hello alt nesne hello üst başvuruyor. Geçerli değerler **içerir** veya **ilişkilendirilmiş**.

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryoda, hello topoloji bilgilerini alır. ARMclient PowerShell kullanarak kullanılan toocall hello REST API ' dir. ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.

## <a name="scenario"></a>Senaryo

Bu makalede ele alınan hello senaryo belirtilen kaynak grubu için hello topoloji yanıtını alır.

## <a name="log-in-with-armclient"></a>Oturum ARMClient oturum

İçinde tooarmclient Azure kimlik bilgilerinizle oturum açın.

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a>Topoloji alma

Aşağıdaki örneğine hello hello topoloji hello REST API ' ister.  Merhaba, örnek oluşturma esneklik için parametreli tooallow örnektir.  Tüm değerlerle değiştirin \< \> bunları çevreleyen.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

yanıt aşağıdaki hello örneği olduğunda döndürülen kısaltılmış bir yanıt almak için bir kaynak grubu topolojisi şöyledir:

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a>Sonraki adımlar

Toovisualize NSG akışınız Power BI ile ziyaret ederek nasıl oturum öğrenin [görselleştirmek NSG akar Power BI ile günlükleri](network-watcher-visualize-nsg-flow-logs-power-bi.md)

