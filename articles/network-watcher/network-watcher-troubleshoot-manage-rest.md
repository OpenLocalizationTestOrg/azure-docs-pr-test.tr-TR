---
title: "aaaTroubleshoot sanal ağ geçidi ve bağlantıları kullanarak Azure Ağ İzleyicisi - REST | Microsoft Docs"
description: "Bu sayfayı nasıl tootroubleshoot sanal ağ geçitleri ve Azure Ağ İzleyicisi'ni kullanarak bağlantıları REST açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e4d5f195-b839-4394-94ef-a04192766e55
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: cc89b46643fdbfefe53727b45d6b7d06914b58a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a>Sanal ağ geçidi ve Azure Ağ İzleyicisi'ni kullanarak bağlantı sorunlarını giderme

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [CLI 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [REST API](network-watcher-troubleshoot-manage-rest.md)

Ağ kaynaklarınızı Azure toounderstanding ilgili olarak Ağ İzleyicisi çok sayıda özellik sağlar. Bu özelliklerin biri kaynak sorun giderme. Kaynak sorun giderme hello portal, PowerShell'i, CLI veya REST API çağrılabilir. Çağrıldığında, Ağ İzleyicisi Merhaba bir sanal ağ geçidi veya bağlantı durumunu inceler ve bulduklarını döndürür.

Bu makalede kaynak sorun giderme için şu anda kullanılabilir hello farklı yönetim görevleri yoluyla alır.

- [**Bir sanal ağ geçidi sorun giderme**](#troubleshoot-a-virtual-network-gateway)
- [**Bir bağlantı sorunlarını giderme**](#troubleshoot-connections)

## <a name="before-you-begin"></a>Başlamadan önce

ARMclient PowerShell kullanarak kullanılan toocall hello REST API ' dir. ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.

Desteklenen ağ geçidi türleri ziyaret listesi [desteklenen ağ geçidi türleri](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Genel Bakış

Ağ İzleyicisi sorun giderme hello yeteneği sağlar sanal ağ geçitlerini ve bağlantılarla ortaya çıkan sorunları giderme. Toohello kaynak bir istekte bulunulduğunda sorun giderme, günlükleri sorguladığınızda ve sahip denetlenir. İnceleme tamamlandığında hello sonuçlar döndürülür. Merhaba, API ilgili sorunları giderme istekleri uzun çalışan birden çok dakika tooreturn bir sonuç ele geçirebilir isteklerin. Günlükler, depolama hesabındaki bir kapsayıcıda depolanır.

## <a name="log-in-with-armclient"></a>Oturum ARMClient oturum

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a>Bir sanal ağ geçidi sorun giderme


### <a name="post-hello-troubleshoot-request"></a>POST hello isteği sorun giderme

Aşağıdaki örnek sorgular hello bir sanal ağ geçidi durumunu hello.

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$vnetGatewayName = "ContosoVNETGateway"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @"
{
'TargetResourceId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/virtualNetworkGateways/${vnetGatewayName}',
'Properties': {
'StorageId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}',
'StoragePath': 'https://${storageAccountName}.blob.core.windows.net/${containerName}'
}
}
"@

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

Bu işlem uzun olduğundan çalıştıran, hello işlemi sorgulamak için URI hello ve hello sonucu için URI hello hello yanıt üstbilgisinde hello yanıt aşağıdaki gösterildiği gibi döndürülür:

**Önemli değerleri**

* **Azure AsyncOperation** -bu özellik hello URI tooquery içerir hello zaman uyumsuz işlemi sorunlarını giderme
* **Konum** -hello URI hello sonuçları nerede hello olduğunda işlemi tamamlandığında bu özellik içerir

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a>Merhaba zaman uyumsuz işlemin tamamlanması için sorgu

Merhaba işlemleri URI tooquery hello hello işlemin ilerlemesini hello aşağıdaki örnekte görüldüğü gibi kullanın:

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

Merhaba işlemi sürerken hello yanıt gösterir **devam ediyor** hello aşağıdaki örnekte görüldüğü gibi:

```json
{
  "status": "InProgress"
}
```

Merhaba işlem olduğunda tam hello durum değişikliklerini çok**başarılı**.

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a>Merhaba sonuçları Al

Merhaba durumu döndürülür sonra **başarılı**, GET yöntemi hello operationResult URI tooretrieve üzerinde hello çağrısının sonuçlarını.

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

Merhaba aşağıdaki yanıtlar hello sonuçlarını bir ağ geçidi sorun giderme sorgulanırken döndürülen tipik düşürülmüş yanıt gösterilebilir. Bkz: [hello sonuçlarını anlama](#understanding-the-results) hello yanıtı anlamına hangi hello özelliklerinde tooget açıklama.

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN gateway is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```


## <a name="troubleshoot-connections"></a>Bağlantı sorunlarını giderme

Aşağıdaki örnek sorgular hello bağlantısının durumunu hello.

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$connectionName = "VNET2toVNET1Connection"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @{
"TargetResourceId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/connections/${connectionName}",
"Properties": {
"StorageId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}",
"StoragePath": "https://${storageAccountName}.blob.core.windows.net/${containerName}"
}

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

> [!NOTE]
> Merhaba sorun giderme işlemi paralel bir bağlantı ve karşılık gelen alt ağ geçitleri üzerinde çalıştırılamaz. Merhaba işlemi, önceki toorunning tamamlamalısınız hello önceki kaynak üzerinde.

Bu hello yanıt üstbilgisinde, uzun süre çalışan bir işlem olduğundan hello işlemi ve hello URI hello sonucu için sorgulama için URI hello hello yanıt aşağıdaki gösterildiği gibi verilir:

**Önemli değerleri**

* **Azure AsyncOperation** -bu özellik hello URI tooquery içerir hello zaman uyumsuz işlemi sorunlarını giderme
* **Konum** -hello URI hello sonuçları nerede hello olduğunda işlemi tamamlandığında bu özellik içerir

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a>Merhaba zaman uyumsuz işlemin tamamlanması için sorgu

Merhaba işlemleri URI tooquery hello hello işlemin ilerlemesini hello aşağıdaki örnekte görüldüğü gibi kullanın:

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

Merhaba işlemi sürerken hello yanıt gösterir **devam ediyor** hello aşağıdaki örnekte görüldüğü gibi:

```json
{
  "status": "InProgress"
}
```

Merhaba işlemi tamamlandığında hello çok durumuna**başarılı**.

```json
{
  "status": "Succeeded"
}
```

Merhaba aşağıdaki yanıtlar hello sonuçlarını bağlantı sorunlarını giderme sorgulanırken döndürülen tipik bir yanıt gösterilebilir.

### <a name="retrieve-hello-results"></a>Merhaba sonuçları Al

Merhaba durumu döndürülür sonra **başarılı**, GET yöntemi hello operationResult URI tooretrieve üzerinde hello çağrısının sonuçlarını.

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

Merhaba aşağıdaki yanıtlar hello sonuçlarını bağlantı sorunlarını giderme sorgulanırken döndürülen tipik bir yanıt gösterilebilir.

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN Connection is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```

## <a name="understanding-hello-results"></a>Merhaba sonuçlarını anlama

Merhaba eylem metni nasıl tooresolve hello üzerinde sorunu genel rehberlik sağlar. Bir eylemin hello sorunu gerçekleştirilebiliyorsa bir bağlantı ile ek yönergeler sağlanır. Merhaba durumda hiçbir ek yönergeler olduğu hello yanıt hello url tooopen bir destek servis talebi sağlar..  Merhaba yanıt ve dahil edilen nedir hello özellikleri hakkında daha fazla bilgi için ziyaret [Ağ İzleyicisi sorun giderme genel bakış](network-watcher-troubleshoot-overview.md)

Azure depolama hesaplarından dosyaları indirme ile ilgili yönergeler için çok başvuran[.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Kullanılabilir başka bir Depolama Gezgini aracıdır. Depolama Gezgini hakkında daha fazla bilgi bağlantısı aşağıdaki hello şurada bulunabilir: [Depolama Gezgini](http://storageexplorer.com/)

## <a name="next-steps"></a>Sonraki adımlar

Bu Dur VPN bağlantısı ayarları değiştirilmiş olup [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) söz konusu olabilecek hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.
