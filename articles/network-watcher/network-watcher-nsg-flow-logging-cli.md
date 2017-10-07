---
title: "Ağ güvenlik grubu akış günlükleri Azure Ağ İzleyicisi - Azure CLI aaaManage | Microsoft Docs"
description: "Bu sayfayı nasıl toomanage ağ güvenlik grubu akış Azure CLI ile Azure Ağ İzleyicisi kaydeder açıklar"
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
ms.openlocfilehash: 2d0b02e7d0a5a9ab20beb491d49a5747f976a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a>Azure CLI ile ağ güvenlik grubu akış günlüklerini yapılandırma

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

Ağ güvenlik grubu akış günlükleri, giriş ve çıkış IP trafiği bir ağ güvenlik grubu aracılığıyla tooview bilgilerini sağlayan Ağ İzleyicisi özelliğidir. Bu akış günlükleri json biçiminde yazılmıştır ve giden Göster gelen akış kuralı başına temelinde hello NIC hello akış uygular, 5-tanımlama grubu ilgili bilgilere hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, Protokolü) ve hello varsa trafiğine izin veya engellendi.

Bu makalede bizim nesil CLI hello kaynak yönetimi dağıtım modeli için Azure CLI 2.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.

Bu makaledeki adımları tooperform Merhaba, çok ihtiyacınız[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="register-insights-provider"></a>Öngörüler sağlayıcısını Kaydet

Merhaba başarıyla günlük toowork akış için sırayla **Microsoft.ınsights** sağlayıcı kaydedilmelidir. Merhaba, emin değilseniz **Microsoft.ınsights** sağlayıcısıdır kayıtlı, çalışma hello aşağıdaki komut dosyası.

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a>Ağ güvenlik grubu etkinleştirmek akış günlükleri

Merhaba komut tooenable akış günlükleri aşağıdaki örneğine hello gösterilir:

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a>Ağ güvenlik grubu devre dışı akış günlükleri

Örnek toodisable akış günlükleri aşağıdaki kullanım hello:

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
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
