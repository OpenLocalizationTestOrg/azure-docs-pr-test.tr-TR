---
title: "Paket yakalama Azure Ağ İzleyicisi - Azure CLI 2.0 ile yönetme | Microsoft Docs"
description: "Bu sayfa, Azure CLI 2.0 kullanan Ağ İzleyicisi'nin paket yakalama özelliği yönetmek açıklanmaktadır"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: cb0c1d10-f7f2-4c34-b08c-f73452430be8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c94eb46f31f2f19b843ccd7bf77b8a39943a07d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="7d11d-103">Paket yakalama Azure CLI 2.0 kullanan Azure Ağ İzleyicisi ile yönetme</span><span class="sxs-lookup"><span data-stu-id="7d11d-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7d11d-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="7d11d-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="7d11d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d11d-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="7d11d-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7d11d-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="7d11d-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7d11d-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="7d11d-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="7d11d-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="7d11d-109">Ağ İzleyicisi paket yakalama, bir sanal makine gelen ve giden trafiği izlemek için yakalama oturumları oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d11d-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="7d11d-110">Filtreler yalnızca trafiği yakalama emin olmak yakalama oturumu için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7d11d-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="7d11d-111">Paket yakalama Tepkisel hem de önceden ağ anormallikleri tanılamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7d11d-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="7d11d-112">Diğer kullanımlar ağ yetkisiz erişim, istemci-sunucu iletişimleri ve çok daha fazlasını hata ayıklamak için bilgi sağlamasını ağ istatistikleri toplama içerir.</span><span class="sxs-lookup"><span data-stu-id="7d11d-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="7d11d-113">Erişebildiklerinden uzaktan paket yakalamaları tetiklemek için bir paket yakalama el ile ve değerli zaman kazandırır istenen makine üzerinde çalışan iş yükünü Bu yetenek kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="7d11d-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="7d11d-114">Bu makalede, Windows, Mac ve Linux için kullanılabilir olduğu, kaynak yönetimi için dağıtım modelini, Azure CLI 2.0 bizim nesil CLI kullanılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7d11d-114">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="7d11d-115">Bu makaledeki adımları gerçekleştirmek için gerek [Mac, Linux ve Windows (Azure CLI) için Azure komut satırı arabirimini yükleyin](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="7d11d-115">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="7d11d-116">Bu makalede paket yakalama için şu anda kullanılabilir farklı yönetim görevleri yoluyla alır.</span><span class="sxs-lookup"><span data-stu-id="7d11d-116">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="7d11d-117">**Paket yakalama Başlat**</span><span class="sxs-lookup"><span data-stu-id="7d11d-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="7d11d-118">**Paket yakalama işlemini durdurun**</span><span class="sxs-lookup"><span data-stu-id="7d11d-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="7d11d-119">**Paket yakalama Sil**</span><span class="sxs-lookup"><span data-stu-id="7d11d-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="7d11d-120">**Paket yakalama indirin**</span><span class="sxs-lookup"><span data-stu-id="7d11d-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="7d11d-121">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="7d11d-121">Before you begin</span></span>

<span data-ttu-id="7d11d-122">Bu makalede, aşağıdaki kaynaklara sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="7d11d-122">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="7d11d-123">Paket yakalama oluşturmak istediğiniz bölgede Ağ İzleyicisi örneği</span><span class="sxs-lookup"><span data-stu-id="7d11d-123">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="7d11d-124">Bir sanal makine etkin paket yakalama uzantısına sahip.</span><span class="sxs-lookup"><span data-stu-id="7d11d-124">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d11d-125">Paket yakalama sanal makine üzerinde çalışan bir aracının gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7d11d-125">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="7d11d-126">Aracı bir uzantısı olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="7d11d-126">The Agent is installed as an extension.</span></span> <span data-ttu-id="7d11d-127">VM uzantıları hakkında yönergeler için ziyaret [sanal makine uzantıları ve özellikleri](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="7d11d-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="7d11d-128">VM uzantısı yükleyin</span><span class="sxs-lookup"><span data-stu-id="7d11d-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="7d11d-129">1. Adım</span><span class="sxs-lookup"><span data-stu-id="7d11d-129">Step 1</span></span>

<span data-ttu-id="7d11d-130">Çalıştırma `az vm extension set` cmdlet'ini paket yakalama Aracısı Konuk sanal makineye yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7d11d-130">Run the `az vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="7d11d-131">Windows sanal makineler için:</span><span class="sxs-lookup"><span data-stu-id="7d11d-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="7d11d-132">Linux sanal makineleri için:</span><span class="sxs-lookup"><span data-stu-id="7d11d-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="7d11d-133">2. Adım</span><span class="sxs-lookup"><span data-stu-id="7d11d-133">Step 2</span></span>

<span data-ttu-id="7d11d-134">Aracının yüklü olduğundan emin olun, çalıştırmayı `vm extension get` cmdlet'i ve kaynak grubu ve sanal makine adı geçirin.</span><span class="sxs-lookup"><span data-stu-id="7d11d-134">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="7d11d-135">Sonuçta elde edilen listenin aracısının yüklü olduğundan emin olmak için kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="7d11d-135">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="7d11d-136">Aşağıdaki örnek yanıt çalışmasını örneğidir`az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="7d11d-136">The following sample is an example of the response from running `az vm extension show`</span></span>

```json
{
  "autoUpgradeMinorVersion": true,
  "forceUpdateTag": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}/extensions/NetworkWatcherAgentWindows",
  "instanceView": null,
  "location": "westcentralus",
  "name": "NetworkWatcherAgentWindows",
  "protectedSettings": null,
  "provisioningState": "Succeeded",
  "publisher": "Microsoft.Azure.NetworkWatcher",
  "resourceGroup": "{resourceGroupName}",
  "settings": null,
  "tags": null,
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "typeHandlerVersion": "1.4",
  "virtualMachineExtensionType": "NetworkWatcherAgentWindows"
}
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="7d11d-137">Paket yakalama Başlat</span><span class="sxs-lookup"><span data-stu-id="7d11d-137">Start a packet capture</span></span>

<span data-ttu-id="7d11d-138">Yukarıdaki adımları tamamlandıktan sonra paket yakalama Aracısı sanal makineye yüklenir.</span><span class="sxs-lookup"><span data-stu-id="7d11d-138">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="7d11d-139">1. Adım</span><span class="sxs-lookup"><span data-stu-id="7d11d-139">Step 1</span></span>

<span data-ttu-id="7d11d-140">Ağ İzleyicisi örneği almak için sonraki adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="7d11d-140">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="7d11d-141">Ağ İzleyicisi'ni kurulacağı adını iletilir `az network watcher show` 4. adımda cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7d11d-141">TThe name of the Network Watcher is passed to the `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="7d11d-142">2. Adım</span><span class="sxs-lookup"><span data-stu-id="7d11d-142">Step 2</span></span>

<span data-ttu-id="7d11d-143">Bir depolama hesabı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d11d-143">Retrieve a storage account.</span></span> <span data-ttu-id="7d11d-144">Bu depolama hesabını paket yakalama dosyasını depolamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d11d-144">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="7d11d-145">3. Adım</span><span class="sxs-lookup"><span data-stu-id="7d11d-145">Step 3</span></span>

<span data-ttu-id="7d11d-146">Filtreler, paket yakalama tarafından depolanan verileri sınırlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7d11d-146">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="7d11d-147">Aşağıdaki örnek, bir paket yakalama kurduğunuzda birkaç filtrelerle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="7d11d-147">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="7d11d-148">İlk üç filtreleri giden TCP trafiğine yalnızca yerel bir IP 10.0.0.3 20, 80 ve 443 hedef bağlantı noktalarına toplayın.</span><span class="sxs-lookup"><span data-stu-id="7d11d-148">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="7d11d-149">Son filtre yalnızca UDP trafiğini toplar.</span><span class="sxs-lookup"><span data-stu-id="7d11d-149">The last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="7d11d-150">Beklenen çıktı çalışmasını aşağıdaki örnekte olduğu `az network watcher packet-capture create` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7d11d-150">The following example is the expected output from running the `az network watcher packet-capture create` cmdlet.</span></span>

```json
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/pa
cketCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/p
roviders/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapture_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="7d11d-151">Paket yakalama Al</span><span class="sxs-lookup"><span data-stu-id="7d11d-151">Get a packet capture</span></span>

<span data-ttu-id="7d11d-152">Çalışan `az network watcher packet-capture show` cmdlet, şu anda çalışan ya da tamamlanmış bir paket yakalama durumunu alır.</span><span class="sxs-lookup"><span data-stu-id="7d11d-152">Running the `az network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="7d11d-153">Aşağıdaki örnek çıktısı olan `az network watcher packet-capture show` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7d11d-153">The following example is the output from the `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="7d11d-154">Yakalama işlemi tamamlandıktan sonra aşağıdaki örnektir.</span><span class="sxs-lookup"><span data-stu-id="7d11d-154">The following example is after the capture is complete.</span></span> <span data-ttu-id="7d11d-155">StopReason TimeExceeded ile PacketCaptureStatus değer durdurulmuş.</span><span class="sxs-lookup"><span data-stu-id="7d11d-155">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="7d11d-156">Bu değer, paket yakalama başarılı oldu ve onun kez çalıştıktan gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d11d-156">This value shows that the packet capture was successful and ran its time.</span></span>

```
{
  "bytesToCapturePerPacket": 0,
  "etag": "W/\"b8cf3528-2e14-45cb-a7f3-5712ffb687ac\"",
  "filters": [
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "20"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "80"
    },
    {
      "localIpAddress": "10.0.0.3",
      "localPort": "",
      "protocol": "TCP",
      "remoteIpAddress": "1.1.1.1-255.255.255",
      "remotePort": "443"
    },
    {
      "localIpAddress": "",
      "localPort": "",
      "protocol": "UDP",
      "remoteIpAddress": "",
      "remotePort": ""
    }
  ],
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/NetworkWatcherRG/providers/Microsoft.Network/networkWatchers/NetworkWatcher_westcentralus/packetCaptures/packetCaptureName",
  "name": "packetCaptureName",
  "provisioningState": "Succeeded",
  "resourceGroup": "NetworkWatcherRG",
  "storageLocation": {
    "filePath": null,
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/gwteststorage123abc",
    "storagePath": "https://gwteststorage123abc.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/{resourceGroupName}/providers/microsoft.compute/virtualmachines/{vmName}/2017/05/25/packetcapt
ure_16_22_34_630.cap"
  },
  "target": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute/virtualMachines/{vmName}",
  "timeLimitInSeconds": 18000,
  "totalBytesPerSession": 1073741824
}
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="7d11d-157">Paket yakalama işlemini durdurun</span><span class="sxs-lookup"><span data-stu-id="7d11d-157">Stop a packet capture</span></span>

<span data-ttu-id="7d11d-158">Çalıştırarak `az network watcher packet-capture stop` yakalama oturumu Sürüyor ise cmdlet durduruldu.</span><span class="sxs-lookup"><span data-stu-id="7d11d-158">By running the `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="7d11d-159">Cmdlet yanıt verir, o anda çalışan bir yakalama oturumu veya zaten durdurulmuş olan bir oturumu.</span><span class="sxs-lookup"><span data-stu-id="7d11d-159">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="7d11d-160">Paket yakalama Sil</span><span class="sxs-lookup"><span data-stu-id="7d11d-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="7d11d-161">Paket yakalama silindiğinde depolama hesabındaki dosya silinmez.</span><span class="sxs-lookup"><span data-stu-id="7d11d-161">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="7d11d-162">Paket yakalama indirin</span><span class="sxs-lookup"><span data-stu-id="7d11d-162">Download a packet capture</span></span>

<span data-ttu-id="7d11d-163">Paket yakalama oturumunuz tamamladıktan sonra blob depolama alanına veya VM üzerindeki yerel bir dosyaya yakalama dosyasını karşıya yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="7d11d-163">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="7d11d-164">Paket yakalama depolama konumunu oturum oluşturma sırasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="7d11d-164">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="7d11d-165">Bunlar erişmek için uygun bir aracı yakalama dosyalarını bir depolama hesabına kaydedilmiş olan burada indirilebilir Microsoft Azure Storage Gezgini: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="7d11d-165">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="7d11d-166">Bir depolama hesabı belirtilirse, paket yakalama dosyaları şu konumda bir depolama hesabına kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="7d11d-166">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="7d11d-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7d11d-167">Next steps</span></span>

<span data-ttu-id="7d11d-168">Sanal makine uyarılarla paket yakalamaları görüntüleyerek otomatikleştirmeyi öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="7d11d-168">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="7d11d-169">Belirli trafik içinde veya dışında VM ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7d11d-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
