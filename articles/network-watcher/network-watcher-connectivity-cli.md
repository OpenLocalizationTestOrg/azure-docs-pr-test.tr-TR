---
title: "Azure Ağ İzleyicisi - Azure CLI 2.0 aaaCheck bağlanabilirlik | Microsoft Docs"
description: "Bu sayfayı nasıl toouse bağlantısını denetleyin Ağ İzleyicisi Azure CLI 2.0 kullanan açıklar"
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
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: e94e0fad03fd36ebf4e1fdf9e3cfee934b289deb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="60f21-103">Azure CLI 2.0 kullanan Azure Ağ İzleyicisi ile bağlantısını denetleyin</span><span class="sxs-lookup"><span data-stu-id="60f21-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="60f21-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="60f21-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="60f21-105">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="60f21-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="60f21-106">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="60f21-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="60f21-107">Toouse bağlantı tooverify doğrudan TCP bağlantısı, uç nokta verilen bir sanal makine tooa nasıl kurulabilir öğrenin.</span><span class="sxs-lookup"><span data-stu-id="60f21-107">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="60f21-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="60f21-108">Before you begin</span></span>

<span data-ttu-id="60f21-109">Bu makalede, kaynakları aşağıdaki hello olduğu varsayılır:</span><span class="sxs-lookup"><span data-stu-id="60f21-109">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="60f21-110">Bir örneği toocheck bağlantı istediğiniz Ağ İzleyicisinin hello bölgede.</span><span class="sxs-lookup"><span data-stu-id="60f21-110">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="60f21-111">Sanal makineler toocheck bağlantısına sahip.</span><span class="sxs-lookup"><span data-stu-id="60f21-111">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="60f21-112">Bağlantı onay gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="60f21-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="60f21-113">Bir Windows VM Hello uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Azure Ağ İzleyicisi Aracısı sanal makine uzantısı Linuxiçin](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="60f21-113">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="60f21-114">Merhaba önizleme özelliği Kaydet</span><span class="sxs-lookup"><span data-stu-id="60f21-114">Register hello preview capability</span></span> 

<span data-ttu-id="60f21-115">Bağlantı denetimi genel önizlemede toouse kayıtlı toobe gerekiyor bu özellik şu anda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="60f21-115">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="60f21-116">toodo CLI örnek aşağıdaki Bu, çalışma hello</span><span class="sxs-lookup"><span data-stu-id="60f21-116">toodo this, run hello following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="60f21-117">CLI komutu aşağıdaki hello çalıştırmak tooverify hello kaydı başarıyla kaldırıldı:</span><span class="sxs-lookup"><span data-stu-id="60f21-117">tooverify hello registration was successful, run hello following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="60f21-118">Merhaba özelliği düzgün şekilde kaydedilmemişse, hello çıktı hello aşağıdaki eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="60f21-118">If hello feature was properly registered, hello output should match hello following:</span></span> 

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Features/providers/Microsoft.Network/features/AllowNetworkWatcherConnectivityCheck",
  "name": "Microsoft.Network/AllowNetworkWatcherConnectivityCheck",
  "properties": {
    "state": "Registered"
  },
  "type": "Microsoft.Features/providers/features"
}
``` 

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="60f21-119">Bağlantı tooa sanal makine kontrol edin</span><span class="sxs-lookup"><span data-stu-id="60f21-119">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="60f21-120">Bu örnekte, bağlantı noktası 80 üzerinden bağlantı tooa hedef sanal makine denetler.</span><span class="sxs-lookup"><span data-stu-id="60f21-120">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="60f21-121">Örnek</span><span class="sxs-lookup"><span data-stu-id="60f21-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="60f21-122">Yanıt</span><span class="sxs-lookup"><span data-stu-id="60f21-122">Response</span></span>

<span data-ttu-id="60f21-123">yanıt aşağıdaki hello hello önceki örnekten ' dir.</span><span class="sxs-lookup"><span data-stu-id="60f21-123">hello following response is from hello previous example.</span></span>  <span data-ttu-id="60f21-124">Bu yanıt olarak hello `ConnectionStatus` olan **ulaşılamıyor**.</span><span class="sxs-lookup"><span data-stu-id="60f21-124">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="60f21-125">Tüm başarısız gönderilen araştırmalar hello görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60f21-125">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="60f21-126">Merhaba bağlantı başarısız hello sanal gereç son tooa kullanıcı tarafından yapılandırılan `NetworkSecurityRule` adlı **UserRule_Port80**, bağlantı noktası 80 üzerinde tooblock gelen trafiği yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="60f21-126">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="60f21-127">Bu bilgiler kullanılan tooresearch bağlantı sorunları olabilir.</span><span class="sxs-lookup"><span data-stu-id="60f21-127">This information can be used tooresearch connection issues.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "bb01d336-d881-4808-9fbc-72f091974d68",
      "issues": [],
      "nextHopIds": [
        "f8b074e9-9980-496b-a35e-619f9bcbf648"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "10.1.2.4",
      "id": "f8b074e9-9980-496b-a35e-619f9bcbf648",
      "issues": [],
      "nextHopIds": [
        "8a5857f3-6ab8-4b11-b9bf-a046d66b8696"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fw
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.3.4",
      "id": "8a5857f3-6ab8-4b11-b9bf-a046d66b8696",
      "issues": [
        {
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule"
        }
      ],
      "nextHopIds": [
        "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/au
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.4.4",
      "id": "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/db
Nic0/ipConfigurations/ipconfig1",
      "type": "VnetLocal"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="60f21-128">Yönlendirme sorunları doğrula</span><span class="sxs-lookup"><span data-stu-id="60f21-128">Validate routing issues</span></span>

<span data-ttu-id="60f21-129">Merhaba örnek bir sanal makine ve bir uzak uç noktası arasındaki bağlantıyı denetler.</span><span class="sxs-lookup"><span data-stu-id="60f21-129">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="60f21-130">Örnek</span><span class="sxs-lookup"><span data-stu-id="60f21-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="60f21-131">Yanıt</span><span class="sxs-lookup"><span data-stu-id="60f21-131">Response</span></span>

<span data-ttu-id="60f21-132">Aşağıdaki örneğine hello hello `connectionStatus` olarak gösterilen **ulaşılamıyor**.</span><span class="sxs-lookup"><span data-stu-id="60f21-132">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="60f21-133">Merhaba, `hops` ayrıntıları görebilirsiniz altında `issues` hello trafiği son engellendiğini tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="60f21-133">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "f2cb1868-2049-4839-b8ed-57a480d06f95",
      "issues": [
        {
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute"
        }
      ],
      "nextHopIds": [
        "da4022db-0ab0-48c4-a507-dd4c03561ca5"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "13.107.21.200",
      "id": "da4022db-0ab0-48c4-a507-dd4c03561ca5",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Unknown",
      "type": "Destination"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="60f21-134">Web sitesi gecikme denetleyin</span><span class="sxs-lookup"><span data-stu-id="60f21-134">Check website latency</span></span>

<span data-ttu-id="60f21-135">Merhaba aşağıdaki örnek hello bağlantı tooa Web sitesini denetler.</span><span class="sxs-lookup"><span data-stu-id="60f21-135">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="60f21-136">Örnek</span><span class="sxs-lookup"><span data-stu-id="60f21-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="60f21-137">Yanıt</span><span class="sxs-lookup"><span data-stu-id="60f21-137">Response</span></span>

<span data-ttu-id="60f21-138">Yanıt aşağıdaki hello hello görebilirsiniz `connectionStatus` olarak gösterir **erişilebilir**.</span><span class="sxs-lookup"><span data-stu-id="60f21-138">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="60f21-139">Bağlantı başarılı olduğunda gecikme değerler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="60f21-139">When a connection is successful, latency values are provided.</span></span>

```json
{
  "avgLatencyInMs": 2,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "639c2d19-e163-4dfd-8737-5018dd1168ae",
      "issues": [],
      "nextHopIds": [
        "fd43a6e7-c758-4f48-90aa-8db99105a4a3"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "204.79.197.200",
      "id": "fd43a6e7-c758-4f48-90aa-8db99105a4a3",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="60f21-140">Bağlantı tooa storage uç denetleyin</span><span class="sxs-lookup"><span data-stu-id="60f21-140">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="60f21-141">Merhaba aşağıdaki örnek bir sanal makine tooa blog depolama hesabı hello bağlantısını denetler.</span><span class="sxs-lookup"><span data-stu-id="60f21-141">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="60f21-142">Örnek</span><span class="sxs-lookup"><span data-stu-id="60f21-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="60f21-143">Yanıt</span><span class="sxs-lookup"><span data-stu-id="60f21-143">Response</span></span>

<span data-ttu-id="60f21-144">Merhaba aşağıdaki json hello Önceki cmdlet çalıştırılarak hello örnek yanıt şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="60f21-144">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="60f21-145">Merhaba onay başarılı olduğu gibi hello `connectionStatus` özelliği gösterildiğinden **erişilebilir**.</span><span class="sxs-lookup"><span data-stu-id="60f21-145">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="60f21-146">Merhaba sayısı atlama gerekli tooreach hello depolama blobu ve gecikme süresi ile ilgili hello Ayrıntılar verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="60f21-146">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "avgLatencyInMs": 1,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "5136acff-bf26-4c93-9966-4edb7dd40353",
      "issues": [],
      "nextHopIds": [
        "f8d958b7-3636-4d63-9441-602c1eb2fd56"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "1.2.3.4",
      "id": "f8d958b7-3636-4d63-9441-602c1eb2fd56",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="next-steps"></a><span data-ttu-id="60f21-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="60f21-147">Next steps</span></span>

<span data-ttu-id="60f21-148">Nasıl sanal makine uyarılarla tooautomate paket görüntüleyerek yakalar öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="60f21-148">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="60f21-149">Belirli trafik içinde veya dışında VM ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="60f21-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
