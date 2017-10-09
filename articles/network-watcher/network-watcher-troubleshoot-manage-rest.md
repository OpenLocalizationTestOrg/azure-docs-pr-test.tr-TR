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
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="81272-103">Sanal ağ geçidi ve Azure Ağ İzleyicisi'ni kullanarak bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="81272-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="81272-104">Portal</span><span class="sxs-lookup"><span data-stu-id="81272-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="81272-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="81272-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="81272-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="81272-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="81272-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="81272-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="81272-108">REST API</span><span class="sxs-lookup"><span data-stu-id="81272-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="81272-109">Ağ kaynaklarınızı Azure toounderstanding ilgili olarak Ağ İzleyicisi çok sayıda özellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="81272-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="81272-110">Bu özelliklerin biri kaynak sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="81272-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="81272-111">Kaynak sorun giderme hello portal, PowerShell'i, CLI veya REST API çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="81272-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="81272-112">Çağrıldığında, Ağ İzleyicisi Merhaba bir sanal ağ geçidi veya bağlantı durumunu inceler ve bulduklarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="81272-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="81272-113">Bu makalede kaynak sorun giderme için şu anda kullanılabilir hello farklı yönetim görevleri yoluyla alır.</span><span class="sxs-lookup"><span data-stu-id="81272-113">This article takes you through hello different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="81272-114">**Bir sanal ağ geçidi sorun giderme**</span><span class="sxs-lookup"><span data-stu-id="81272-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="81272-115">**Bir bağlantı sorunlarını giderme**</span><span class="sxs-lookup"><span data-stu-id="81272-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="81272-116">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="81272-116">Before you begin</span></span>

<span data-ttu-id="81272-117">ARMclient PowerShell kullanarak kullanılan toocall hello REST API ' dir.</span><span class="sxs-lookup"><span data-stu-id="81272-117">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="81272-118">ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="81272-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="81272-119">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="81272-119">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="81272-120">Desteklenen ağ geçidi türleri ziyaret listesi [desteklenen ağ geçidi türleri](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="81272-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="81272-121">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="81272-121">Overview</span></span>

<span data-ttu-id="81272-122">Ağ İzleyicisi sorun giderme hello yeteneği sağlar sanal ağ geçitlerini ve bağlantılarla ortaya çıkan sorunları giderme.</span><span class="sxs-lookup"><span data-stu-id="81272-122">Network Watcher troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="81272-123">Toohello kaynak bir istekte bulunulduğunda sorun giderme, günlükleri sorguladığınızda ve sahip denetlenir.</span><span class="sxs-lookup"><span data-stu-id="81272-123">When a request is made toohello resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="81272-124">İnceleme tamamlandığında hello sonuçlar döndürülür.</span><span class="sxs-lookup"><span data-stu-id="81272-124">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="81272-125">Merhaba, API ilgili sorunları giderme istekleri uzun çalışan birden çok dakika tooreturn bir sonuç ele geçirebilir isteklerin.</span><span class="sxs-lookup"><span data-stu-id="81272-125">hello troubleshoot API requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="81272-126">Günlükler, depolama hesabındaki bir kapsayıcıda depolanır.</span><span class="sxs-lookup"><span data-stu-id="81272-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="81272-127">Oturum ARMClient oturum</span><span class="sxs-lookup"><span data-stu-id="81272-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="81272-128">Bir sanal ağ geçidi sorun giderme</span><span class="sxs-lookup"><span data-stu-id="81272-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-hello-troubleshoot-request"></a><span data-ttu-id="81272-129">POST hello isteği sorun giderme</span><span class="sxs-lookup"><span data-stu-id="81272-129">POST hello troubleshoot request</span></span>

<span data-ttu-id="81272-130">Aşağıdaki örnek sorgular hello bir sanal ağ geçidi durumunu hello.</span><span class="sxs-lookup"><span data-stu-id="81272-130">hello following example queries hello status of a Virtual Network gateway.</span></span>

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

<span data-ttu-id="81272-131">Bu işlem uzun olduğundan çalıştıran, hello işlemi sorgulamak için URI hello ve hello sonucu için URI hello hello yanıt üstbilgisinde hello yanıt aşağıdaki gösterildiği gibi döndürülür:</span><span class="sxs-lookup"><span data-stu-id="81272-131">Since this operation is long running, hello URI for querying hello operation and hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="81272-132">**Önemli değerleri**</span><span class="sxs-lookup"><span data-stu-id="81272-132">**Important Values**</span></span>

* <span data-ttu-id="81272-133">**Azure AsyncOperation** -bu özellik hello URI tooquery içerir hello zaman uyumsuz işlemi sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="81272-133">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="81272-134">**Konum** -hello URI hello sonuçları nerede hello olduğunda işlemi tamamlandığında bu özellik içerir</span><span class="sxs-lookup"><span data-stu-id="81272-134">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="81272-135">Merhaba zaman uyumsuz işlemin tamamlanması için sorgu</span><span class="sxs-lookup"><span data-stu-id="81272-135">Query hello async operation for completion</span></span>

<span data-ttu-id="81272-136">Merhaba işlemleri URI tooquery hello hello işlemin ilerlemesini hello aşağıdaki örnekte görüldüğü gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="81272-136">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="81272-137">Merhaba işlemi sürerken hello yanıt gösterir **devam ediyor** hello aşağıdaki örnekte görüldüğü gibi:</span><span class="sxs-lookup"><span data-stu-id="81272-137">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="81272-138">Merhaba işlem olduğunda tam hello durum değişikliklerini çok**başarılı**.</span><span class="sxs-lookup"><span data-stu-id="81272-138">When hello operation is complete hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a><span data-ttu-id="81272-139">Merhaba sonuçları Al</span><span class="sxs-lookup"><span data-stu-id="81272-139">Retrieve hello results</span></span>

<span data-ttu-id="81272-140">Merhaba durumu döndürülür sonra **başarılı**, GET yöntemi hello operationResult URI tooretrieve üzerinde hello çağrısının sonuçlarını.</span><span class="sxs-lookup"><span data-stu-id="81272-140">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="81272-141">Merhaba aşağıdaki yanıtlar hello sonuçlarını bir ağ geçidi sorun giderme sorgulanırken döndürülen tipik düşürülmüş yanıt gösterilebilir.</span><span class="sxs-lookup"><span data-stu-id="81272-141">hello following responses are examples of a typical degraded response returned when querying hello results of troubleshooting a gateway.</span></span> <span data-ttu-id="81272-142">Bkz: [hello sonuçlarını anlama](#understanding-the-results) hello yanıtı anlamına hangi hello özelliklerinde tooget açıklama.</span><span class="sxs-lookup"><span data-stu-id="81272-142">See [Understanding hello results](#understanding-the-results) tooget clarification on what hello properties in hello response mean.</span></span>

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


## <a name="troubleshoot-connections"></a><span data-ttu-id="81272-143">Bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="81272-143">Troubleshoot Connections</span></span>

<span data-ttu-id="81272-144">Aşağıdaki örnek sorgular hello bağlantısının durumunu hello.</span><span class="sxs-lookup"><span data-stu-id="81272-144">hello following example queries hello status of a Connection.</span></span>

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
> <span data-ttu-id="81272-145">Merhaba sorun giderme işlemi paralel bir bağlantı ve karşılık gelen alt ağ geçitleri üzerinde çalıştırılamaz.</span><span class="sxs-lookup"><span data-stu-id="81272-145">hello troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="81272-146">Merhaba işlemi, önceki toorunning tamamlamalısınız hello önceki kaynak üzerinde.</span><span class="sxs-lookup"><span data-stu-id="81272-146">hello operation must complete prior toorunning it on hello previous resource.</span></span>

<span data-ttu-id="81272-147">Bu hello yanıt üstbilgisinde, uzun süre çalışan bir işlem olduğundan hello işlemi ve hello URI hello sonucu için sorgulama için URI hello hello yanıt aşağıdaki gösterildiği gibi verilir:</span><span class="sxs-lookup"><span data-stu-id="81272-147">Since this is a long running transaction, in hello response header, hello URI for querying hello operation and hello URI for hello result is returned as shown in hello following response:</span></span>

<span data-ttu-id="81272-148">**Önemli değerleri**</span><span class="sxs-lookup"><span data-stu-id="81272-148">**Important Values**</span></span>

* <span data-ttu-id="81272-149">**Azure AsyncOperation** -bu özellik hello URI tooquery içerir hello zaman uyumsuz işlemi sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="81272-149">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="81272-150">**Konum** -hello URI hello sonuçları nerede hello olduğunda işlemi tamamlandığında bu özellik içerir</span><span class="sxs-lookup"><span data-stu-id="81272-150">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

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

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="81272-151">Merhaba zaman uyumsuz işlemin tamamlanması için sorgu</span><span class="sxs-lookup"><span data-stu-id="81272-151">Query hello async operation for completion</span></span>

<span data-ttu-id="81272-152">Merhaba işlemleri URI tooquery hello hello işlemin ilerlemesini hello aşağıdaki örnekte görüldüğü gibi kullanın:</span><span class="sxs-lookup"><span data-stu-id="81272-152">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="81272-153">Merhaba işlemi sürerken hello yanıt gösterir **devam ediyor** hello aşağıdaki örnekte görüldüğü gibi:</span><span class="sxs-lookup"><span data-stu-id="81272-153">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="81272-154">Merhaba işlemi tamamlandığında hello çok durumuna**başarılı**.</span><span class="sxs-lookup"><span data-stu-id="81272-154">When hello operation is complete, hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="81272-155">Merhaba aşağıdaki yanıtlar hello sonuçlarını bağlantı sorunlarını giderme sorgulanırken döndürülen tipik bir yanıt gösterilebilir.</span><span class="sxs-lookup"><span data-stu-id="81272-155">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

### <a name="retrieve-hello-results"></a><span data-ttu-id="81272-156">Merhaba sonuçları Al</span><span class="sxs-lookup"><span data-stu-id="81272-156">Retrieve hello results</span></span>

<span data-ttu-id="81272-157">Merhaba durumu döndürülür sonra **başarılı**, GET yöntemi hello operationResult URI tooretrieve üzerinde hello çağrısının sonuçlarını.</span><span class="sxs-lookup"><span data-stu-id="81272-157">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="81272-158">Merhaba aşağıdaki yanıtlar hello sonuçlarını bağlantı sorunlarını giderme sorgulanırken döndürülen tipik bir yanıt gösterilebilir.</span><span class="sxs-lookup"><span data-stu-id="81272-158">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

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

## <a name="understanding-hello-results"></a><span data-ttu-id="81272-159">Merhaba sonuçlarını anlama</span><span class="sxs-lookup"><span data-stu-id="81272-159">Understanding hello results</span></span>

<span data-ttu-id="81272-160">Merhaba eylem metni nasıl tooresolve hello üzerinde sorunu genel rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="81272-160">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="81272-161">Bir eylemin hello sorunu gerçekleştirilebiliyorsa bir bağlantı ile ek yönergeler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="81272-161">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="81272-162">Merhaba durumda hiçbir ek yönergeler olduğu hello yanıt hello url tooopen bir destek servis talebi sağlar..</span><span class="sxs-lookup"><span data-stu-id="81272-162">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="81272-163">Merhaba yanıt ve dahil edilen nedir hello özellikleri hakkında daha fazla bilgi için ziyaret [Ağ İzleyicisi sorun giderme genel bakış](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="81272-163">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="81272-164">Azure depolama hesaplarından dosyaları indirme ile ilgili yönergeler için çok başvuran[.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="81272-164">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="81272-165">Kullanılabilir başka bir Depolama Gezgini aracıdır.</span><span class="sxs-lookup"><span data-stu-id="81272-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="81272-166">Depolama Gezgini hakkında daha fazla bilgi bağlantısı aşağıdaki hello şurada bulunabilir: [Depolama Gezgini](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="81272-166">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="81272-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="81272-167">Next steps</span></span>

<span data-ttu-id="81272-168">Bu Dur VPN bağlantısı ayarları değiştirilmiş olup [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) söz konusu olabilecek hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.</span><span class="sxs-lookup"><span data-stu-id="81272-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
