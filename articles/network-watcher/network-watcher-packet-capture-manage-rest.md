---
title: "Paket yakalama Azure Ağ İzleyicisi - REST API ile yönetme | Microsoft Docs"
description: "Bu sayfa, Azure REST API'sini kullanarak Ağ İzleyicisi'nin paket yakalama özelliği yönetmek açıklanmaktadır"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 53fe0324-835f-4005-afc8-145eeb314aeb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 49ec20802a252258d8493eb26510270b925e851a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="a525d-103">Paket yakalama Azure REST API'sini kullanarak Azure Ağ İzleyicisi ile yönetme</span><span class="sxs-lookup"><span data-stu-id="a525d-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a525d-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="a525d-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="a525d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a525d-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="a525d-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a525d-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="a525d-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a525d-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="a525d-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="a525d-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="a525d-109">Ağ İzleyicisi paket yakalama, bir sanal makine gelen ve giden trafiği izlemek için yakalama oturumları oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a525d-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="a525d-110">Filtreler yalnızca trafiği yakalama emin olmak yakalama oturumu için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="a525d-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="a525d-111">Paket yakalama Tepkisel hem de önceden ağ anormallikleri tanılamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a525d-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="a525d-112">Diğer kullanımlar ağ yetkisiz erişim, istemci-sunucu iletişimleri ve çok daha fazlasını hata ayıklamak için bilgi sağlamasını ağ istatistikleri toplama içerir.</span><span class="sxs-lookup"><span data-stu-id="a525d-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="a525d-113">Erişebildiklerinden uzaktan paket yakalamaları tetiklemek için bir paket yakalama el ile ve değerli zaman kazandırır istenen makine üzerinde çalışan iş yükünü Bu yetenek kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="a525d-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="a525d-114">Bu makalede paket yakalama için şu anda kullanılabilir farklı yönetim görevleri yoluyla alır.</span><span class="sxs-lookup"><span data-stu-id="a525d-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="a525d-115">**Paket yakalama Al**</span><span class="sxs-lookup"><span data-stu-id="a525d-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="a525d-116">**Tüm paket yakalamaları listesi**</span><span class="sxs-lookup"><span data-stu-id="a525d-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="a525d-117">**Paket yakalama durumunu sorgulama**</span><span class="sxs-lookup"><span data-stu-id="a525d-117">**Query the status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="a525d-118">**Paket yakalama Başlat**</span><span class="sxs-lookup"><span data-stu-id="a525d-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="a525d-119">**Paket yakalama işlemini durdurun**</span><span class="sxs-lookup"><span data-stu-id="a525d-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="a525d-120">**Paket yakalama Sil**</span><span class="sxs-lookup"><span data-stu-id="a525d-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="a525d-121">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="a525d-121">Before you begin</span></span>

<span data-ttu-id="a525d-122">Bu senaryoda, akış IP doğrulama çalıştırmak için Ağ İzleyicisi Rest API çağrısı.</span><span class="sxs-lookup"><span data-stu-id="a525d-122">In this scenario, you call the Network Watcher Rest API to run IP Flow Verify.</span></span> <span data-ttu-id="a525d-123">ARMclient PowerShell kullanarak REST API'sini çağırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a525d-123">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="a525d-124">ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="a525d-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="a525d-125">Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) bir Ağ İzleyicisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="a525d-125">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> <span data-ttu-id="a525d-126">Paket yakalama gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="a525d-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="a525d-127">Bir Windows VM uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Linux için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="a525d-127">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="a525d-128">Oturum ARMClient oturum</span><span class="sxs-lookup"><span data-stu-id="a525d-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="a525d-129">Bir sanal makine alma</span><span class="sxs-lookup"><span data-stu-id="a525d-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="a525d-130">Bir sanal makine döndürmek için aşağıdaki betiği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a525d-130">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="a525d-131">Bu bilgiler, bir paket yakalama başlatmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a525d-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="a525d-132">Aşağıdaki kod değişkenleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="a525d-132">The following code needs variables:</span></span>

- <span data-ttu-id="a525d-133">**Subscriptionıd** -abonelik kimliği ile aynı zamanda alınabilir **Get-AzureRMSubscription** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a525d-133">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="a525d-134">**resourceGroupName** -sanal makine içeren bir kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="a525d-134">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="a525d-135">Aşağıdaki çıktısını sonraki örnekte sanal makinenin kimliği kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a525d-135">From the following output, the id of the virtual machine is used in the next example.</span></span>

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


## <a name="get-a-packet-capture"></a><span data-ttu-id="a525d-136">Paket yakalama Al</span><span class="sxs-lookup"><span data-stu-id="a525d-136">Get a packet capture</span></span>

<span data-ttu-id="a525d-137">Aşağıdaki örnek bir tek Paket yakalama durumunu alır</span><span class="sxs-lookup"><span data-stu-id="a525d-137">The following example gets the status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="a525d-138">Aşağıdaki yanıtlar paket yakalama durumunu sorgulanırken döndürülen tipik bir yanıt gösterilebilir.</span><span class="sxs-lookup"><span data-stu-id="a525d-138">The following responses are examples of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Running",
  "packetCaptureError": []
}
```

```json
{
  "name": "TestPacketCapture5",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
  "captureStartTime": "2016-12-06T17:20:01.5671279Z",
  "packetCaptureStatus": "Stopped",
  "stopReason": "TimeExceeded",
  "packetCaptureError": []
}
```

## <a name="list-all-packet-captures"></a><span data-ttu-id="a525d-139">Tüm paket yakalamaları listesi</span><span class="sxs-lookup"><span data-stu-id="a525d-139">List all packet captures</span></span>

<span data-ttu-id="a525d-140">Aşağıdaki örnek, bir bölgede tüm paket yakalama oturumları alır.</span><span class="sxs-lookup"><span data-stu-id="a525d-140">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="a525d-141">Tüm paket alırken döndürülen tipik bir yanıt örneği yakalar aşağıdaki yanıt olan</span><span class="sxs-lookup"><span data-stu-id="a525d-141">The following response is an example of a typical response returned when getting all packet captures</span></span>

```json
{
  "value": [
    {
      "name": "TestPacketCapture6",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture6",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Succeeded",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_19_53_056.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    },
    {
      "name": "TestPacketCapture7",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/TestPacketCapture7",
      "etag": "W/\"091762e1-c23f-448b-89d5-37cf56e4c045\"",
      "properties": {
        "provisioningState": "Failed",
        "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute/virtualMachines/ContosoVM",
        "bytesToCapturePerPacket": 0,
        "totalBytesPerSession": 1073741824,
        "timeLimitInSeconds": 60,
        "storageLocation": {
          "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Storage/storageAccounts/contosoexamplergdiag374",
          "storagePath": "https://contosoexamplergdiag374.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/contosoexamplerg/providers/microsoft.compute/virtualmachines/contosovm/2016/12/06/packetcap
ture_17_23_15_364.cap",
          "filePath": "c:\\temp\\packetcapture.cap"
        },
        "filters": [
          {
            "protocol": "Any",
            "localIPAddress": "",
            "localPort": "",
            "remoteIPAddress": "",
            "remotePort": ""
          }
        ]
      }
    }
  ]
}
```

## <a name="query-packet-capture-status"></a><span data-ttu-id="a525d-142">Sorgu paket yakalama durumu</span><span class="sxs-lookup"><span data-stu-id="a525d-142">Query packet capture status</span></span>

<span data-ttu-id="a525d-143">Aşağıdaki örnek, bir bölgede tüm paket yakalama oturumları alır.</span><span class="sxs-lookup"><span data-stu-id="a525d-143">The following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="a525d-144">Aşağıdaki yanıtı, bir paket yakalama durumunu sorgulanırken döndürülen tipik bir yanıt örneğidir.</span><span class="sxs-lookup"><span data-stu-id="a525d-144">The following response is an example of a typical response returned when querying the status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="a525d-145">Paket yakalama Başlat</span><span class="sxs-lookup"><span data-stu-id="a525d-145">Start packet capture</span></span>

<span data-ttu-id="a525d-146">Aşağıdaki örnek, bir sanal makinede bir paket yakalama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a525d-146">The following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="a525d-147">Örnek oluşturma esneklik sağlamak amacıyla örnek parametreli.</span><span class="sxs-lookup"><span data-stu-id="a525d-147">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
$storageaccountname = "contosoexamplergdiag374"
$vmName = "ContosoVM"
$bytestoCaptureperPacket = "0"
$bytesPerSession = "1073741824"
$captureTimeinSeconds = "60"
$localIP = ""
$localPort = "" # Examples are: 80, or 80-120
$remoteIP = ""
$remotePort = "" # Examples are: 80, or 80-120
$protocol = "" # Valid values are TCP, UDP and Any.
$targetUri = "" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName
$storageId = "" # Example: "https://mytestaccountname.blob.core.windows.net/capture/vm1Capture.cap"
$storagePath = ""
$localFilePath = "c:\\temp\\packetcapture.cap" # Example: "d:\capture\vm1Capture.cap"

$requestBody = @"
{
    'properties':  {
                       'target':  '/${targetUri}',
                       'bytesToCapturePerPacket':  '${bytestoCaptureperPacket}',
                       'totalBytesPerSession':  '${bytesPerSession}',
                       'timeLimitinSeconds':  '${captureTimeinSeconds}',
                       'storageLocation':  {
                                               'storageId':  '${storageId}',
                                               'storagePath':  '${storagePath}',
                                               'filePath':  '${localFilePath}'
                                           },
                       'filters':  [
                                       {
                                           'protocol':  '${protocol}',
                                           'localIPAddress':  '${localIP}',
                                           'localPort':  '${localPort}',
                                           'remoteIPAddress':  '${remoteIP}',
                                           'remotePort':  '${remotePort}'
                                       }
                                   ]
                   }
}
"@

armclient PUT "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-07-01" $requestbody
```

## <a name="stop-packet-capture"></a><span data-ttu-id="a525d-148">Paket yakalama işlemini durdurun</span><span class="sxs-lookup"><span data-stu-id="a525d-148">Stop packet capture</span></span>

<span data-ttu-id="a525d-149">Aşağıdaki örnek, bir sanal makinede bir paket yakalama durdurur.</span><span class="sxs-lookup"><span data-stu-id="a525d-149">The following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="a525d-150">Örnek oluşturma esneklik sağlamak amacıyla örnek parametreli.</span><span class="sxs-lookup"><span data-stu-id="a525d-150">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="a525d-151">Paket yakalama Sil</span><span class="sxs-lookup"><span data-stu-id="a525d-151">Delete packet capture</span></span>

<span data-ttu-id="a525d-152">Aşağıdaki örnek, bir sanal makinede bir paket yakalama siler.</span><span class="sxs-lookup"><span data-stu-id="a525d-152">The following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="a525d-153">Örnek oluşturma esneklik sağlamak amacıyla örnek parametreli.</span><span class="sxs-lookup"><span data-stu-id="a525d-153">The example is parameterized to allow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="a525d-154">Paket yakalama silmek depolama hesabını dosyasında silmez</span><span class="sxs-lookup"><span data-stu-id="a525d-154">Deleting a packet capture does not delete the file in the storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="a525d-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a525d-155">Next steps</span></span>

<span data-ttu-id="a525d-156">Azure depolama hesaplarından dosyaları indirme ile ilgili yönergeler için bkz [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="a525d-156">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="a525d-157">Kullanılabilir başka bir Depolama Gezgini aracıdır.</span><span class="sxs-lookup"><span data-stu-id="a525d-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="a525d-158">Aşağıdaki bağlantıda Depolama Gezgini hakkında daha fazla bilgi şurada bulunabilir: [Depolama Gezgini](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="a525d-158">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="a525d-159">Sanal makine uyarılarla paket yakalamaları görüntüleyerek otomatikleştirmeyi öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="a525d-159">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













