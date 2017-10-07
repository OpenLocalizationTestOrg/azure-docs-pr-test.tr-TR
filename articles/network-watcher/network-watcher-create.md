---
title: "aaaCreate Azure Ağ İzleyicisi örneği | Microsoft Docs"
description: "Bu sayfa, hello portalı ve Azure REST API'sini kullanarak Ağ İzleyicisi örneği hello adımları toocreate sağlar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a>Bir Azure Ağ İzleyicisi örneği oluşturma

Ağ İzleyicisi'ni ve koşullar bir ağ düzeyinde senaryo içinde gelen ve giden Azure Tanılama, toomonitor sağlayan bölgesel bir hizmettir. Senaryo düzeyi izleme bir bitiş tooend ağ düzey görünümü adresindeki toodiagnose sorunları sağlar. Ağ Tanılama ve görselleştirme Ağ İzleyicisi ile kullanılabilen araçlar anlamak, tanılama ve Öngörüler tooyour Azure ağında geçirmesine yardımcı olur.

> [!NOTE]
> Ağ İzleyicisi'ni şu anda yalnızca CLI 1.0 destekler gibi hello yönergeleri toocreate CLI 1.0 için yeni bir Ağ İzleyicisi örnek sağlanır.

## <a name="create-a-network-watcher-in-hello-portal"></a>Ağ İzleyicisi Merhaba Portalı'nda oluşturma

Çok gidin**daha Hizmetleri** > **ağ** > **Ağ İzleyicisi**. Ağ İzleyicisi tooenable istediğiniz tüm hello abonelikleri seçebilirsiniz için. Bu eylem, kullanılabilir olan her bölgede bir Ağ İzleyicisi oluşturur.

![Ağ İzleyicisi oluşturma][1]

Ağ İzleyicisi Merhaba Portal kullanarak etkinleştirdiğinizde hello hello Ağ İzleyicisi örneğinin adını otomatik olarak tooNetworkWatcher_region_name nerede region_name toohello Azure hello örneği etkinleştirdiğiniz bölge karşılık gelen ayarlanır.  Örneğin, Batı Orta ABD bölgesinde etkin bir Ağ İzleyicisi NetworkWatcher_westcentralus adlandırılır

Ayrıca, hello Ağ İzleyicisi örneği NetworkWatcherRG adlı bir kaynak grubuna otomatik olarak eklenir.  Bu kaynak grubu, zaten yoksa, oluşturulur.

Ağ İzleyicisi örneği ve hello toocustomize hello adı istiyorsanız içine yerleştirilen kaynak grubu, aşağıda açıklanan Powershell, hello REST API veya ARMClient yöntemlerini kullanabilirsiniz.  Ağ İzleyicisi Merhaba içine yerleştirmeden önce her seçenekte, hello kaynak grubu mevcut olmalıdır.  

## <a name="create-a-network-watcher-with-powershell"></a>PowerShell ile bir Ağ İzleyicisi oluşturma

toocreate Ağ İzleyicisi, aşağıdaki örneğine hello çalıştırmak örneği:

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a>Ağ İzleyicisi Merhaba REST API ile oluşturma

ARMclient PowerShell kullanarak kullanılan toocall hello REST API ' dir. ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)

### <a name="log-in-with-armclient"></a>Oturum ARMClient oturum

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a>Merhaba Ağ İzleyicisi oluşturma

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a>Sonraki adımlar

Ağ İzleyicisi örneği sahip olduğunuza göre kullanılabilir hello özellikleri hakkında bilgi edinin:

* [Topoloji](network-watcher-topology-overview.md)
* [Paket yakalama](network-watcher-packet-capture-overview.md)
* [IP akışı doğrulama](network-watcher-ip-flow-verify-overview.md)
* [Sonraki atlama](network-watcher-next-hop-overview.md)
* [Güvenlik grubu görünümü](network-watcher-security-group-view-overview.md)
* [NSG akış günlüğe kaydetme](network-watcher-nsg-flow-logging-overview.md)
* [Sanal ağ geçidi sorunlarını giderme](network-watcher-troubleshoot-overview.md)

Paket yakalama Ağ İzleyicisi örneği oluşturulduktan sonra aşağıdaki hello makalesiyle yapılandırılabilir: [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)

[1]: ./media/network-watcher-create/figure1.png











