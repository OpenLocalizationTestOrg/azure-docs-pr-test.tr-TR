---
title: "aaaView Azure Ağ İzleyicisi topolojisi - Azure CLI 1.0 | Microsoft Docs"
description: "Bu makalede anlatmaktadır nasıl toouse Azure CLI 1.0 tooquery ağ topolojinizi."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 30679d6dc74e85bacfc86c63bd1afa873893c772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli-10"></a>Ağ İzleyicisi topolojisi Azure CLI 1.0 ile görüntüleme

> [!div class="op_single_selector"]
> - [PowerShell](network-watcher-topology-powershell.md)
> - [CLI 1.0](network-watcher-topology-cli-nodejs.md)
> - [CLI 2.0](network-watcher-topology-cli.md)
> - [REST API](network-watcher-topology-rest.md)

Ağ İzleyicisi Merhaba topoloji özelliği görsel bir abonelik hello ağ kaynaklarını sağlar. Merhaba Portalı'nda bu görselleştirme tooyou otomatik olarak sunulur. Merhaba topoloji görünümü hello portalında ardındaki Hello bilgileri PowerShell aracılığıyla alınabilir.
Bu özellik hello topoloji bilgilerini hello veri diğer araçları toobuild hello görselleştirme çıkışı tarafından kullanılabilecek daha verimli hale getirir.

Bu makalede, platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır. 

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

Bu senaryoda, kullandığınız hello `network watcher topology` cmdlet tooretrieve hello topoloji bilgilerini. Ayrıca bir makalesi vardır hakkında çok[ağ topolojisi REST API ile almak](network-watcher-topology-rest.md).

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.

## <a name="scenario"></a>Senaryo

Bu makalede ele alınan hello senaryo belirtilen kaynak grubu için hello topoloji yanıtını alır.

## <a name="retrieve-topology"></a>Topoloji alma

Merhaba `network watcher topology` cmdlet'i belirtilen kaynak grubu için hello topolojisini alır. Merhaba bağımsız değişken Ekle "--json" json biçiminde tooview hello oput

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a>Sonuçlar

Merhaba döndürülen sonuçları bir özellik "Merhaba json yanıt gövdesine hello için içeren adı" kaynaklarınız `network watcher topology` cmdlet'i.  Merhaba yanıt hello kaynaklarında hello ağ güvenlik grubu ve ilişkilendirmelerinin (diğer bir deyişle, içerir, ilişkilendirilmiş) içerir.

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a>Sonraki adımlar

Şu adresi ziyaret ederek uygulanan tooyour ağ kaynaklarına olan hello güvenlik kuralları hakkında daha fazla bilgi [güvenlik grubu Görünümü'ne genel bakış](network-watcher-security-group-view-overview.md)
