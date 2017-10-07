---
title: "Azure Ağ İzleyicisi - Azure portal ile aaaCheck bağlantısı | Microsoft Docs"
description: "Bu sayfayı nasıl toocheck bağlantısına sahip Ağ İzleyicisi Merhaba Azure portal açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: gwallace
ms.openlocfilehash: 8560011906fcce46d31556fc52cbfa671e8e653a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="1ce27-103">Hello Azure portal kullanarak Azure Ağ İzleyicisi ile bağlantısını denetleyin</span><span class="sxs-lookup"><span data-stu-id="1ce27-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1ce27-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1ce27-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="1ce27-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ce27-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="1ce27-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1ce27-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="1ce27-107">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="1ce27-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="1ce27-108">Toouse bağlantı tooverify doğrudan TCP bağlantısı, uç nokta verilen bir sanal makine tooa nasıl kurulabilir öğrenin.</span><span class="sxs-lookup"><span data-stu-id="1ce27-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1ce27-109">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="1ce27-109">Before you begin</span></span>

<span data-ttu-id="1ce27-110">Bu makalede, kaynakları aşağıdaki hello olduğu varsayılır:</span><span class="sxs-lookup"><span data-stu-id="1ce27-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="1ce27-111">Bir örneği toocheck bağlantı istediğiniz Ağ İzleyicisinin hello bölgede.</span><span class="sxs-lookup"><span data-stu-id="1ce27-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="1ce27-112">Sanal makineler toocheck bağlantısına sahip.</span><span class="sxs-lookup"><span data-stu-id="1ce27-112">Virtual machines toocheck connectivity with.</span></span>

<span data-ttu-id="1ce27-113">ARMclient PowerShell kullanarak kullanılan toocall hello REST API ' dir.</span><span class="sxs-lookup"><span data-stu-id="1ce27-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="1ce27-114">ARMClient bulundu üzerinde adresindeki chocolatey [ARMClient Chocolatey üzerinde](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="1ce27-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient).</span></span>

<span data-ttu-id="1ce27-115">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="1ce27-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="1ce27-116">Bağlantı onay gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="1ce27-116">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="1ce27-117">Bir Windows VM Hello uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Azure Ağ İzleyicisi Aracısı sanal makine uzantısı Linuxiçin](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="1ce27-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="1ce27-118">Merhaba önizleme özelliği Kaydet</span><span class="sxs-lookup"><span data-stu-id="1ce27-118">Register hello preview capability</span></span>

<span data-ttu-id="1ce27-119">Bağlantı denetimi genel önizlemede toouse kayıtlı toobe gerekiyor bu özellik şu anda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1ce27-119">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="1ce27-120">toodo PowerShell örnek aşağıdaki Bu, çalışma hello:</span><span class="sxs-lookup"><span data-stu-id="1ce27-120">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="1ce27-121">Powershell örnek aşağıdaki hello çalıştırmak tooverify hello kaydı başarıyla kaldırıldı:</span><span class="sxs-lookup"><span data-stu-id="1ce27-121">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="1ce27-122">Merhaba özelliği düzgün şekilde kaydedilmemişse, hello çıktı hello aşağıdaki eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="1ce27-122">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName                             ProviderName      RegistrationState
-----------                             ------------      -----------------
AllowNetworkWatcherConnectivityCheck    Microsoft.Network Registered
```

## <a name="log-in-with-armclient"></a><span data-ttu-id="1ce27-123">Oturum ARMClient oturum</span><span class="sxs-lookup"><span data-stu-id="1ce27-123">Log in with ARMClient</span></span>

<span data-ttu-id="1ce27-124">İçinde tooarmclient Azure kimlik bilgilerinizle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="1ce27-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="1ce27-125">Bir sanal makine alma</span><span class="sxs-lookup"><span data-stu-id="1ce27-125">Retrieve a virtual machine</span></span>

<span data-ttu-id="1ce27-126">Komut dosyası tooreturn aşağıdaki hello bir sanal makine çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1ce27-126">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="1ce27-127">Bu bilgiler, bağlantı çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1ce27-127">This information is needed for running connectivity.</span></span> 

<span data-ttu-id="1ce27-128">koddan hello Merhaba değişkenleri aşağıdaki değerleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="1ce27-128">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="1ce27-129">**Subscriptionıd** -abonelik kimliği toouse hello.</span><span class="sxs-lookup"><span data-stu-id="1ce27-129">**subscriptionId** - hello subscription ID toouse.</span></span>
- <span data-ttu-id="1ce27-130">**resourceGroupName** - hello sanal makine içeren bir kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="1ce27-130">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="1ce27-131">Çıktı hello aşağıdakiler arasından hello kimliği hello sanal makinenin örnek aşağıdaki hello kullanılır:</span><span class="sxs-lookup"><span data-stu-id="1ce27-131">From hello following output, hello ID of hello virtual machine is used in hello following example:</span></span>

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

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="1ce27-132">Bağlantı tooa sanal makine kontrol edin</span><span class="sxs-lookup"><span data-stu-id="1ce27-132">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="1ce27-133">Bu örnekte, bağlantı noktası 80 üzerinden bağlantı tooa hedef sanal makine denetler.</span><span class="sxs-lookup"><span data-stu-id="1ce27-133">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="1ce27-134">Örnek</span><span class="sxs-lookup"><span data-stu-id="1ce27-134">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/Database0"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'resourceId': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="1ce27-135">Bu işlem uzun olduğundan çalıştıran, hello hello sonuç URI'sini hello yanıt üstbilgisinde hello yanıt aşağıdaki gösterildiği gibi verilir:</span><span class="sxs-lookup"><span data-stu-id="1ce27-135">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="1ce27-136">**Önemli değerleri**</span><span class="sxs-lookup"><span data-stu-id="1ce27-136">**Important Values**</span></span>

* <span data-ttu-id="1ce27-137">**Konum** -hello URI hello sonuçları nerede hello olduğunda işlemi tamamlandığında bu özellik içerir</span><span class="sxs-lookup"><span data-stu-id="1ce27-137">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: f09b55fe-1d3a-4df7-817f-bceb8d2a94c8
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/f09b55fe-1d3a-4df7-817f-bceb8d2a94c8?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 367a91aa-7142-436a-867d-d3a36f80bc54
x-ms-routing-request-id: WESTUS2:20170602T202117Z:367a91aa-7142-436a-867d-d3a36f80bc54
Date: Fri, 02 Jun 2017 20:21:16 GMT

null
```

### <a name="response"></a><span data-ttu-id="1ce27-138">Yanıt</span><span class="sxs-lookup"><span data-stu-id="1ce27-138">Response</span></span>

<span data-ttu-id="1ce27-139">yanıt aşağıdaki hello hello önceki örnekten ' dir.</span><span class="sxs-lookup"><span data-stu-id="1ce27-139">hello following response is from hello previous example.</span></span>  <span data-ttu-id="1ce27-140">Bu yanıt olarak hello `ConnectionStatus` olan **ulaşılamıyor**.</span><span class="sxs-lookup"><span data-stu-id="1ce27-140">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="1ce27-141">Tüm başarısız gönderilen araştırmalar hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ce27-141">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="1ce27-142">Merhaba bağlantı başarısız hello sanal gereç son tooa kullanıcı tarafından yapılandırılan `NetworkSecurityRule` adlı **UserRule_Port80**, bağlantı noktası 80 üzerinde tooblock gelen trafiği yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="1ce27-142">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="1ce27-143">Bu bilgiler kullanılan tooresearch bağlantı sorunları olabilir.</span><span class="sxs-lookup"><span data-stu-id="1ce27-143">This information can be used tooresearch connection issues.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "0cb75c91-7ebf-4df8-8424-15594d6fb51c",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684",
      "address": "10.1.2.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "75e0cfa5-f9d2-48d8-b705-2c7016f81570"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "75e0cfa5-f9d2-48d8-b705-2c7016f81570",
      "address": "10.1.3.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "86caf6aa-33b0-48a1-b4da-f3c9ce785072"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule",
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ]
        }
      ]
    },
    {
      "type": "VnetLocal",
      "id": "86caf6aa-33b0-48a1-b4da-f3c9ce785072",
      "address": "10.1.4.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="1ce27-144">Yönlendirme sorunları doğrula</span><span class="sxs-lookup"><span data-stu-id="1ce27-144">Validate routing issues</span></span>

<span data-ttu-id="1ce27-145">Merhaba örnek bir sanal makine ve bir uzak uç noktası arasındaki bağlantıyı denetler.</span><span class="sxs-lookup"><span data-stu-id="1ce27-145">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="1ce27-146">Örnek</span><span class="sxs-lookup"><span data-stu-id="1ce27-146">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "13.107.21.200"
$destinationPort = "80"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="1ce27-147">Bu işlem uzun olduğundan çalıştıran, hello hello sonuç URI'sini hello yanıt üstbilgisinde hello yanıt aşağıdaki gösterildiği gibi verilir:</span><span class="sxs-lookup"><span data-stu-id="1ce27-147">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="1ce27-148">**Önemli değerleri**</span><span class="sxs-lookup"><span data-stu-id="1ce27-148">**Important Values**</span></span>

* <span data-ttu-id="1ce27-149">**Konum** -hello URI hello sonuçları nerede hello olduğunda işlemi tamamlandığında bu özellik içerir</span><span class="sxs-lookup"><span data-stu-id="1ce27-149">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 15eeeb69-fcef-41db-bc4a-e2adcf2658e0
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/15eeeb69-fcef-41db-bc4a-e2adcf2658e0?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4370b798-cd8b-4d3e-ba28-22232bc81dc5
x-ms-routing-request-id: WESTUS:20170602T202606Z:4370b798-cd8b-4d3e-ba28-22232bc81dc5
Date: Fri, 02 Jun 2017 20:26:05 GMT

null
```

### <a name="response"></a><span data-ttu-id="1ce27-150">Yanıt</span><span class="sxs-lookup"><span data-stu-id="1ce27-150">Response</span></span>

<span data-ttu-id="1ce27-151">Aşağıdaki örneğine hello hello `connectionStatus` olarak gösterilen **ulaşılamıyor**.</span><span class="sxs-lookup"><span data-stu-id="1ce27-151">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="1ce27-152">Merhaba, `hops` ayrıntıları görebilirsiniz altında `issues` hello trafiği son engellendiğini tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="1ce27-152">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "5528055a-b393-4751-97bc-353d8c0aaeff",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "66eefa79-5bfe-48b2-b6ca-eec8247457a3"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute",
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ]
        }
      ]
    },
    {
      "type": "Destination",
      "id": "66eefa79-5bfe-48b2-b6ca-eec8247457a3",
      "address": "13.107.21.200",
      "resourceId": "Unknown",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="1ce27-153">Web sitesi gecikme denetleyin</span><span class="sxs-lookup"><span data-stu-id="1ce27-153">Check website latency</span></span>

<span data-ttu-id="1ce27-154">Merhaba aşağıdaki örnek hello bağlantı tooa Web sitesini denetler.</span><span class="sxs-lookup"><span data-stu-id="1ce27-154">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="1ce27-155">Örnek</span><span class="sxs-lookup"><span data-stu-id="1ce27-155">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "http://bing.com"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="1ce27-156">Bu işlem uzun olduğundan çalıştıran, hello hello sonuç URI'sini hello yanıt üstbilgisinde hello yanıt aşağıdaki gösterildiği gibi verilir:</span><span class="sxs-lookup"><span data-stu-id="1ce27-156">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="1ce27-157">**Önemli değerleri**</span><span class="sxs-lookup"><span data-stu-id="1ce27-157">**Important Values**</span></span>

* <span data-ttu-id="1ce27-158">**Konum** -hello URI hello sonuçları nerede hello olduğunda işlemi tamamlandığında bu özellik içerir</span><span class="sxs-lookup"><span data-stu-id="1ce27-158">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: e49b12c7-c232-472c-b6d2-6c257ce80fa5
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/e49b12c7-c232-472c-b6d2-6c257ce80fa5?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: c3d9744f-5683-427d-bdd1-636b68ab01b6
x-ms-routing-request-id: WESTUS:20170602T203101Z:c3d9744f-5683-427d-bdd1-636b68ab01b6
Date: Fri, 02 Jun 2017 20:31:00 GMT

null
```

### <a name="response"></a><span data-ttu-id="1ce27-159">Yanıt</span><span class="sxs-lookup"><span data-stu-id="1ce27-159">Response</span></span>

<span data-ttu-id="1ce27-160">Yanıt aşağıdaki hello hello görebilirsiniz `connectionStatus` olarak gösterir **erişilebilir**.</span><span class="sxs-lookup"><span data-stu-id="1ce27-160">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="1ce27-161">Bağlantı başarılı olduğunda gecikme değerler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="1ce27-161">When a connection is successful, latency values are provided.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "204.79.197.200",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="1ce27-162">Bağlantı tooa storage uç denetleyin</span><span class="sxs-lookup"><span data-stu-id="1ce27-162">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="1ce27-163">Merhaba aşağıdaki örnek bir sanal makine tooa blog depolama hesabı hello bağlantısını denetler.</span><span class="sxs-lookup"><span data-stu-id="1ce27-163">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="1ce27-164">Örnek</span><span class="sxs-lookup"><span data-stu-id="1ce27-164">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "https://build2017nwdiag360.blob.core.windows.net/"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="1ce27-165">Bu işlem uzun olduğundan çalıştıran, hello hello sonuç URI'sini hello yanıt üstbilgisinde hello yanıt aşağıdaki gösterildiği gibi verilir:</span><span class="sxs-lookup"><span data-stu-id="1ce27-165">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="1ce27-166">**Önemli değerleri**</span><span class="sxs-lookup"><span data-stu-id="1ce27-166">**Important Values**</span></span>

* <span data-ttu-id="1ce27-167">**Konum** -hello URI hello sonuçları nerede hello olduğunda işlemi tamamlandığında bu özellik içerir</span><span class="sxs-lookup"><span data-stu-id="1ce27-167">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
x-ms-routing-request-id: WESTUS2:20170602T200504Z:93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
Date: Fri, 02 Jun 2017 20:05:03 GMT

null
```

### <a name="response"></a><span data-ttu-id="1ce27-168">Yanıt</span><span class="sxs-lookup"><span data-stu-id="1ce27-168">Response</span></span>

<span data-ttu-id="1ce27-169">Merhaba aşağıdaki hello önceki API çağrısı çalışmasını hello yanıt örnektir.</span><span class="sxs-lookup"><span data-stu-id="1ce27-169">hello following example is hello response from running hello previous API call.</span></span> <span data-ttu-id="1ce27-170">Merhaba onay başarılı olduğu gibi hello `connectionStatus` özelliği gösterildiğinden **erişilebilir**.</span><span class="sxs-lookup"><span data-stu-id="1ce27-170">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="1ce27-171">Merhaba sayısı atlama gerekli tooreach hello depolama blobu ve gecikme süresi ile ilgili hello Ayrıntılar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ce27-171">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "13.71.200.248",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="next-steps"></a><span data-ttu-id="1ce27-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ce27-172">Next steps</span></span>

<span data-ttu-id="1ce27-173">Nasıl sanal makine uyarılarla tooautomate paket görüntüleyerek yakalar öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="1ce27-173">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="1ce27-174">Belirli trafik içinde veya dışında VM ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1ce27-174">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














