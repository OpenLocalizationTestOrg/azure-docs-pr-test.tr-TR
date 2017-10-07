---
title: "aaaView Azure Ağ İzleyicisi topolojisi - PowerShell | Microsoft Docs"
description: "Bu makalede anlatmaktadır nasıl toouse PowerShell tooquery ağ topolojinizi."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a>PowerShell ile Ağ İzleyicisi topolojisini görüntülemek

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

Bu senaryoda, kullandığınız hello `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve hello topoloji bilgilerini. Ayrıca bir makalesi vardır hakkında çok[ağ topolojisi REST API ile almak](network-watcher-topology-rest.md).

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.

## <a name="scenario"></a>Senaryo

Bu makalede ele alınan hello senaryo belirtilen kaynak grubu için hello topoloji yanıtını alır.

## <a name="retrieve-network-watcher"></a>Ağ İzleyicisi alma

Merhaba ilk adımı tooretrieve hello Ağ İzleyicisi örneğidir. Merhaba `$networkWatcher` değişkeni toohello geçirilen `Get-AzureRmNetworkWatcherTopology` cmdlet'i.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a>Topoloji alma

Merhaba `Get-AzureRmNetworkWatcherTopology` cmdlet'i belirtilen kaynak grubu için hello topolojisini alır.

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a>Sonuçlar

Merhaba döndürülen sonuçları bir özellik "Merhaba json yanıt gövdesine hello için içeren adı" kaynaklarınız `Get-AzureRmNetworkWatcherTopology` cmdlet'i.  Merhaba yanıt hello kaynaklarında hello ağ güvenlik grubu ve ilişkilendirmelerinin (diğer bir deyişle, içerir, ilişkilendirilmiş) içerir.

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a>Sonraki adımlar

Toovisualize NSG akışınız Power BI ile ziyaret ederek nasıl oturum öğrenin [görselleştirmek NSG akar Power BI ile günlükleri](network-watcher-visualize-nsg-flow-logs-power-bi.md)


