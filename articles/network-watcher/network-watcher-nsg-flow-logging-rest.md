---
title: "Ağ güvenlik grubu akışı aaaManage günlüklerini Azure Ağ İzleyicisi - REST API | Microsoft Docs"
description: "Bu sayfayı toomanage ağ güvenlik grubu akış Azure Ağ İzleyicisi REST API ile nasıl kaydeder açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2ab25379-0fd3-4bfe-9d82-425dfc7ad6bb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: be81e35f4d01c67efef99773e9b4e2ae4b8e209e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="6a992-103">REST API kullanarak ağ güvenlik grubu yapılandırma akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="6a992-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6a992-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6a992-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="6a992-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6a992-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="6a992-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6a992-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="6a992-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6a992-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="6a992-108">REST API</span><span class="sxs-lookup"><span data-stu-id="6a992-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="6a992-109">Ağ güvenlik grubu akış günlükleri, giriş ve çıkış IP trafiği bir ağ güvenlik grubu aracılığıyla tooview bilgilerini sağlayan Ağ İzleyicisi özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="6a992-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="6a992-110">Bu akış günlükleri json biçiminde yazılmıştır ve giden Göster gelen akış kuralı başına temelinde hello NIC hello akış uygular, 5-tanımlama grubu ilgili bilgilere hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, Protokolü) ve hello varsa trafiğine izin veya engellendi.</span><span class="sxs-lookup"><span data-stu-id="6a992-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6a992-111">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="6a992-111">Before you begin</span></span>

<span data-ttu-id="6a992-112">ARMclient PowerShell kullanarak kullanılan toocall hello REST API ' dir.</span><span class="sxs-lookup"><span data-stu-id="6a992-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="6a992-113">ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="6a992-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="6a992-114">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="6a992-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="6a992-115">Ağ İzleyicisi REST API çağrıları hello tanılama eylemleri gerçekleştirdiğiniz hello kaynakları değil hello Ağ İzleyicisi'ni içeren hello kaynak grubunu URI'dir hello isteğindeki kaynak grubu adı hello.</span><span class="sxs-lookup"><span data-stu-id="6a992-115">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="6a992-116">Senaryo</span><span class="sxs-lookup"><span data-stu-id="6a992-116">Scenario</span></span>

<span data-ttu-id="6a992-117">Bu makalede ele alınan hello senaryo tooenable, devre dışı bırakma ve sorgu hello REST API kullanarak günlüklerini nasıl gerçekleştiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="6a992-117">hello scenario covered in this article shows you how tooenable, disable, and query flow logs using hello REST API.</span></span> <span data-ttu-id="6a992-118">Ağ güvenlik grubu akışı loggings hakkında daha fazla toolearn ziyaret [ağ güvenlik grubu akışı günlüğü - genel bakış](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6a992-118">toolearn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="6a992-119">Bu senaryoda, şunları yapacaksınız:</span><span class="sxs-lookup"><span data-stu-id="6a992-119">In this scenario, you will:</span></span>

* <span data-ttu-id="6a992-120">Akış günlükleri etkinleştir</span><span class="sxs-lookup"><span data-stu-id="6a992-120">Enable flow logs</span></span>
* <span data-ttu-id="6a992-121">Akış günlükleri devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="6a992-121">Disable flow logs</span></span>
* <span data-ttu-id="6a992-122">Sorgu akış günlükleri durumu</span><span class="sxs-lookup"><span data-stu-id="6a992-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="6a992-123">Oturum ARMClient oturum</span><span class="sxs-lookup"><span data-stu-id="6a992-123">Log in with ARMClient</span></span>

<span data-ttu-id="6a992-124">İçinde tooarmclient Azure kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6a992-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="6a992-125">Öngörüler sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="6a992-125">Register Insights provider</span></span>

<span data-ttu-id="6a992-126">Merhaba başarıyla günlük toowork akış için sırayla **Microsoft.ınsights** sağlayıcı kaydedilmelidir.</span><span class="sxs-lookup"><span data-stu-id="6a992-126">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="6a992-127">Merhaba, emin değilseniz **Microsoft.ınsights** sağlayıcısıdır kayıtlı, çalışma hello aşağıdaki komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="6a992-127">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="6a992-128">Ağ güvenlik grubu etkinleştirmek akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="6a992-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="6a992-129">Merhaba komut tooenable akış günlükleri aşağıdaki örneğine hello gösterilir:</span><span class="sxs-lookup"><span data-stu-id="6a992-129">hello command tooenable flow logs is shown in hello following example:</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'true',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="6a992-130">Merhaba yanıt hello önceki örnek şöyledir döndürdü:</span><span class="sxs-lookup"><span data-stu-id="6a992-130">hello response returned from hello preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="6a992-131">Ağ güvenlik grubu devre dışı akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="6a992-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="6a992-132">Örnek toodisable akış aşağıdaki kullanım hello günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="6a992-132">Use hello following example toodisable flow logs.</span></span> <span data-ttu-id="6a992-133">Merhaba aynı dışında akış günlükleri, etkinleştirme olarak hello çağrıdır **false** etkin hello özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6a992-133">hello call is hello same as enabling flow logs, except **false** is set for hello enabled property.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'false',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="6a992-134">Merhaba yanıt hello önceki örnek şöyledir döndürdü:</span><span class="sxs-lookup"><span data-stu-id="6a992-134">hello response returned from hello preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": false,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="query-flow-logs"></a><span data-ttu-id="6a992-135">Sorgu akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="6a992-135">Query flow logs</span></span>

<span data-ttu-id="6a992-136">Akış durumunu sorgular hello REST çağrısı aşağıdaki hello bir ağ güvenlik grubuna kaydeder.</span><span class="sxs-lookup"><span data-stu-id="6a992-136">hello following REST call queries hello status of flow logs on a Network Security Group.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/queryFlowLogStatus?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="6a992-137">Merhaba, döndürülen hello yanıt örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="6a992-137">hello following is an example of hello response returned:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
   "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="download-a-flow-log"></a><span data-ttu-id="6a992-138">Akış günlüğü indirin</span><span class="sxs-lookup"><span data-stu-id="6a992-138">Download a flow log</span></span>

<span data-ttu-id="6a992-139">Akış günlüğü Hello depolama konumuna oluşturma sırasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="6a992-139">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="6a992-140">Bu akış kaydedilen günlükler tooa depolama hesabıdır burada indirilebilir Microsoft Azure Storage Gezgini uygun aracı tooaccess: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="6a992-140">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="6a992-141">Bir depolama hesabı belirtilirse, paket yakalama dosyalarını tooa depolama hesabı konumu aşağıdaki hello kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="6a992-141">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="6a992-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6a992-142">Next steps</span></span>

<span data-ttu-id="6a992-143">Nasıl çok öğrenin[NSG akış günlüklerinizi Powerbı ile Görselleştirme](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="6a992-143">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="6a992-144">Nasıl çok öğrenin[NSG akış günlüklerinizi açık kaynaklı araçları ile Görselleştirme](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="6a992-144">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
