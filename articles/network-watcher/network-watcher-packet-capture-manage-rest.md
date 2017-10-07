---
title: "aaaManage paket yakalar Azure Ağ İzleyicisi - REST API | Microsoft Docs"
description: "Bu sayfayı nasıl toomanage hello paket yakalama Özelliği Azure REST API'sini kullanarak Ağ İzleyicisinin açıklar"
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
ms.openlocfilehash: 7a531fbe796e85e94961bd192d171defb299be05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="de01e-103">Paket yakalama Azure REST API'sini kullanarak Azure Ağ İzleyicisi ile yönetme</span><span class="sxs-lookup"><span data-stu-id="de01e-103">Manage packet captures with Azure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="de01e-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="de01e-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="de01e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="de01e-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="de01e-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="de01e-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="de01e-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="de01e-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="de01e-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="de01e-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="de01e-109">Ağ İzleyicisi paket yakalama toocreate yakalama oturumları tootrack trafiği tooand bir sanal makineden sağlar.</span><span class="sxs-lookup"><span data-stu-id="de01e-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="de01e-110">Filtreler, yalnızca istediğiniz hello trafiği yakalamak hello yakalama oturum tooensure için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="de01e-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="de01e-111">Paket yakalama toodiagnose ağ anormallikleri Tepkisel ve önceden yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="de01e-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="de01e-112">Diğer kullanımlar bilgi ağ yetkisiz erişim, toodebug istemci-sunucu iletişimleri ve daha fazlasını sağlamasını ağ istatistikleri toplama içerir.</span><span class="sxs-lookup"><span data-stu-id="de01e-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="de01e-113">Mümkün tooremotely tetikleyici paket yakalamaları olma yoluyla bu özelliği bir paket yakalama el ile ve değerli zaman kazandırır hello istenen makine üzerinde çalışan hello yük kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="de01e-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="de01e-114">Bu makalede paket yakalama için şu anda kullanılabilir farklı yönetim görevleri hello alır.</span><span class="sxs-lookup"><span data-stu-id="de01e-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="de01e-115">**Paket yakalama Al**</span><span class="sxs-lookup"><span data-stu-id="de01e-115">**Get a packet capture**</span></span>](#get-a-packet-capture)
- [<span data-ttu-id="de01e-116">**Tüm paket yakalamaları listesi**</span><span class="sxs-lookup"><span data-stu-id="de01e-116">**List all packet captures**</span></span>](#list-all-packet-captures)
- [<span data-ttu-id="de01e-117">**Paket yakalama sorgu hello durumu**</span><span class="sxs-lookup"><span data-stu-id="de01e-117">**Query hello status of a packet capture**</span></span>](#query-packet-capture-status)
- [<span data-ttu-id="de01e-118">**Paket yakalama Başlat**</span><span class="sxs-lookup"><span data-stu-id="de01e-118">**Start a packet capture**</span></span>](#start-packet-capture)
- [<span data-ttu-id="de01e-119">**Paket yakalama işlemini durdurun**</span><span class="sxs-lookup"><span data-stu-id="de01e-119">**Stop a packet capture**</span></span>](#stop-packet-capture)
- [<span data-ttu-id="de01e-120">**Paket yakalama Sil**</span><span class="sxs-lookup"><span data-stu-id="de01e-120">**Delete a packet capture**</span></span>](#delete-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="de01e-121">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="de01e-121">Before you begin</span></span>

<span data-ttu-id="de01e-122">Bu senaryoda, hello Ağ İzleyicisi Rest API'si toorun akış IP doğrulayın çağırın.</span><span class="sxs-lookup"><span data-stu-id="de01e-122">In this scenario, you call hello Network Watcher Rest API toorun IP Flow Verify.</span></span> <span data-ttu-id="de01e-123">ARMclient PowerShell kullanarak kullanılan toocall hello REST API ' dir.</span><span class="sxs-lookup"><span data-stu-id="de01e-123">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="de01e-124">ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="de01e-124">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="de01e-125">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="de01e-125">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> <span data-ttu-id="de01e-126">Paket yakalama gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="de01e-126">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="de01e-127">Bir Windows VM Hello uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Azure Ağ İzleyicisi Aracısı sanal makine uzantısı Linuxiçin](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="de01e-127">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="de01e-128">Oturum ARMClient oturum</span><span class="sxs-lookup"><span data-stu-id="de01e-128">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="de01e-129">Bir sanal makine alma</span><span class="sxs-lookup"><span data-stu-id="de01e-129">Retrieve a virtual machine</span></span>

<span data-ttu-id="de01e-130">Komut dosyası tooreturn aşağıdaki hello bir sanal makine çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="de01e-130">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="de01e-131">Bu bilgiler, bir paket yakalama başlatmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="de01e-131">This information is needed for starting a packet capture.</span></span>

<span data-ttu-id="de01e-132">Merhaba aşağıdaki kodu değişkenleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="de01e-132">hello following code needs variables:</span></span>

- <span data-ttu-id="de01e-133">**Subscriptionıd** -hello abonelik kimliği ile Merhaba da alınabilir **Get-AzureRMSubscription** cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="de01e-133">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="de01e-134">**resourceGroupName** - hello sanal makine içeren bir kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="de01e-134">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="de01e-135">Çıktı hello aşağıdakiler arasından hello kimliği hello sanal makinenin hello sonraki örnekte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="de01e-135">From hello following output, hello id of hello virtual machine is used in hello next example.</span></span>

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


## <a name="get-a-packet-capture"></a><span data-ttu-id="de01e-136">Paket yakalama Al</span><span class="sxs-lookup"><span data-stu-id="de01e-136">Get a packet capture</span></span>

<span data-ttu-id="de01e-137">Merhaba aşağıdaki örnek hello durumunu tek Paket yakalama alır</span><span class="sxs-lookup"><span data-stu-id="de01e-137">hello following example gets hello status of a single packet capture</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="de01e-138">Merhaba aşağıdaki yanıtlar paket yakalama hello durumunu sorgulanırken döndürülen tipik bir yanıt gösterilebilir.</span><span class="sxs-lookup"><span data-stu-id="de01e-138">hello following responses are examples of a typical response returned when querying hello status of a packet capture.</span></span>

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

## <a name="list-all-packet-captures"></a><span data-ttu-id="de01e-139">Tüm paket yakalamaları listesi</span><span class="sxs-lookup"><span data-stu-id="de01e-139">List all packet captures</span></span>

<span data-ttu-id="de01e-140">Aşağıdaki örnek hello tüm paket yakalama oturumları bir bölgede alır.</span><span class="sxs-lookup"><span data-stu-id="de01e-140">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures?api-version=2016-12-01"
```

<span data-ttu-id="de01e-141">Merhaba aşağıdaki yanıt tüm paket alırken döndürülen tipik bir yanıt örneği yakalar olan</span><span class="sxs-lookup"><span data-stu-id="de01e-141">hello following response is an example of a typical response returned when getting all packet captures</span></span>

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

## <a name="query-packet-capture-status"></a><span data-ttu-id="de01e-142">Sorgu paket yakalama durumu</span><span class="sxs-lookup"><span data-stu-id="de01e-142">Query packet capture status</span></span>

<span data-ttu-id="de01e-143">Aşağıdaki örnek hello tüm paket yakalama oturumları bir bölgede alır.</span><span class="sxs-lookup"><span data-stu-id="de01e-143">hello following example gets all packet capture sessions in a region.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient get "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/querystatus?api-version=2016-12-01"
```

<span data-ttu-id="de01e-144">Merhaba aşağıdaki yanıtı paket yakalama hello durumunu sorgulanırken döndürülen tipik bir yanıt örneğidir.</span><span class="sxs-lookup"><span data-stu-id="de01e-144">hello following response is an example of a typical response returned when querying hello status of a packet capture.</span></span>

```json
{
    "name": "vm1PacketCapture",     "id": "/subscriptions/{guid}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkWatchers/{networkWatche rName}/packetCaptures/{packetCaptureName}",
   "captureStartTime" : "9/7/2016 12:35:24PM",
   "packetCaptureStatus" : "Stopped",
   "stopReason" : "TimeExceeded"
   "packetCaptureError" : [ ]
}
```

## <a name="start-packet-capture"></a><span data-ttu-id="de01e-145">Paket yakalama Başlat</span><span class="sxs-lookup"><span data-stu-id="de01e-145">Start packet capture</span></span>

<span data-ttu-id="de01e-146">Aşağıdaki örneğine hello bir sanal makinede bir paket yakalama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="de01e-146">hello following example creates a packet capture on a virtual machine.</span></span>  <span data-ttu-id="de01e-147">Merhaba, örnek oluşturma esneklik için parametreli tooallow örnektir.</span><span class="sxs-lookup"><span data-stu-id="de01e-147">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

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

## <a name="stop-packet-capture"></a><span data-ttu-id="de01e-148">Paket yakalama işlemini durdurun</span><span class="sxs-lookup"><span data-stu-id="de01e-148">Stop packet capture</span></span>

<span data-ttu-id="de01e-149">Aşağıdaki örneğine hello bir sanal makinede bir paket yakalama durdurur.</span><span class="sxs-lookup"><span data-stu-id="de01e-149">hello following example stops a packet capture on a virtual machine.</span></span>  <span data-ttu-id="de01e-150">Merhaba, örnek oluşturma esneklik için parametreli tooallow örnektir.</span><span class="sxs-lookup"><span data-stu-id="de01e-150">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}/stop?api-version=2016-12-01"
```

## <a name="delete-packet-capture"></a><span data-ttu-id="de01e-151">Paket yakalama Sil</span><span class="sxs-lookup"><span data-stu-id="de01e-151">Delete packet capture</span></span>

<span data-ttu-id="de01e-152">Paket yakalama bir sanal makinede aşağıdaki örneğine hello siler.</span><span class="sxs-lookup"><span data-stu-id="de01e-152">hello following example deletes a packet capture on a virtual machine.</span></span>  <span data-ttu-id="de01e-153">Merhaba, örnek oluşturma esneklik için parametreli tooallow örnektir.</span><span class="sxs-lookup"><span data-stu-id="de01e-153">hello example is parameterized tooallow for flexibility in creating an example.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$packetCaptureName = "TestPacketCapture5"

armclient delete "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/packetCaptures/${packetCaptureName}?api-version=2016-12-01"
```

> [!NOTE]
> <span data-ttu-id="de01e-154">Paket yakalama silinmesi hello depolama hesabı hello dosyasında silmez</span><span class="sxs-lookup"><span data-stu-id="de01e-154">Deleting a packet capture does not delete hello file in hello storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="de01e-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="de01e-155">Next steps</span></span>

<span data-ttu-id="de01e-156">Azure depolama hesaplarından dosyaları indirme ile ilgili yönergeler için çok başvuran[.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="de01e-156">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="de01e-157">Kullanılabilir başka bir Depolama Gezgini aracıdır.</span><span class="sxs-lookup"><span data-stu-id="de01e-157">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="de01e-158">Depolama Gezgini hakkında daha fazla bilgi bağlantısı aşağıdaki hello şurada bulunabilir: [Depolama Gezgini](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="de01e-158">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

<span data-ttu-id="de01e-159">Nasıl sanal makine uyarılarla tooautomate paket görüntüleyerek yakalar öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="de01e-159">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>













