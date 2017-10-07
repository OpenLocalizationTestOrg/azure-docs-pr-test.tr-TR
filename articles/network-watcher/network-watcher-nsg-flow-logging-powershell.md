---
title: "Ağ güvenlik grubu akış günlükleri Azure Ağ İzleyicisi - PowerShell aaaManage | Microsoft Docs"
description: "Bu sayfayı nasıl toomanage ağ güvenlik grubu akış PowerShell ile Azure Ağ İzleyicisi kaydeder açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 987e8728fb6459fd6ff8eb5cd3d36ff855f2ccfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-powershell"></a>Ağ güvenlik grubu akış günlükleri PowerShell ile yapılandırma

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

Ağ güvenlik grubu akış günlükleri, giriş ve çıkış IP trafiği bir ağ güvenlik grubu aracılığıyla tooview bilgilerini sağlayan Ağ İzleyicisi özelliğidir. Bu akış günlükleri json biçiminde yazılmıştır ve giden Göster gelen akış kuralı başına temelinde hello NIC hello akış uygular, 5-tanımlama grubu ilgili bilgilere hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, Protokolü) ve hello varsa trafiğine izin veya engellendi.

## <a name="register-insights-provider"></a>Öngörüler sağlayıcısını Kaydet

Merhaba başarıyla günlük toowork akış için sırayla **Microsoft.ınsights** sağlayıcı kaydedilmelidir. Merhaba, emin değilseniz **Microsoft.ınsights** sağlayıcısıdır kayıtlı, çalışma hello aşağıdaki komut dosyası.

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a>Ağ güvenlik grubu etkinleştirmek akış günlükleri

Merhaba komut tooenable akış günlükleri aşağıdaki örneğine hello gösterilir:

```powershell
$NW = Get-AzurermNetworkWatcher -ResourceGroupName NetworkWatcherRg -Name NetworkWatcher_westcentralus
$nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName nsgRG-Name nsgName
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName StorageRG -Name contosostorage123
Get-AzureRmNetworkWatcherFlowLogStatus -NetworkWatcher $NW -TargetResourceId $nsg.Id
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $true
```

## <a name="disable-network-security-group-flow-logs"></a>Ağ güvenlik grubu devre dışı akış günlükleri

Örnek toodisable akış günlükleri aşağıdaki kullanım hello:

```powershell
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $false
```

## <a name="download-a-flow-log"></a>Akış günlüğü indirin

Akış günlüğü Hello depolama konumuna oluşturma sırasında tanımlanır. Bu akış kaydedilen günlükler tooa depolama hesabıdır burada indirilebilir Microsoft Azure Storage Gezgini uygun aracı tooaccess: http://storageexplorer.com/

Bir depolama hesabı belirtilirse, paket yakalama dosyalarını tooa depolama hesabı konumu aşağıdaki hello kaydedilir:

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

Merhaba günlük hello yapısı hakkında bilgi için ziyaret [ağ güvenlik grubu akış günlüğüne genel bakış](network-watcher-nsg-flow-logging-overview.md)

## <a name="next-steps"></a>Sonraki Adımlar

Nasıl çok öğrenin[NSG akış günlüklerinizi Powerbı ile Görselleştirme](network-watcher-visualize-nsg-flow-logs-power-bi.md)

Nasıl çok öğrenin[NSG akış günlüklerinizi açık kaynaklı araçları ile Görselleştirme](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)
