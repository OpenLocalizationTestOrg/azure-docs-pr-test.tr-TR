---
title: "aaaManage paket yakalar Azure Ağ İzleyicisi - Azure CLI 2.0 | Microsoft Docs"
description: "Bu sayfayı nasıl toomanage hello paket yakalama özelliği ağ Azure CLI 2.0 kullanan izleyicisinin açıklar"
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
ms.openlocfilehash: d19cb7d0ca3b7a9bc0546859e07ef6d4df4f42d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="615a9-103">Paket yakalama Azure CLI 2.0 kullanan Azure Ağ İzleyicisi ile yönetme</span><span class="sxs-lookup"><span data-stu-id="615a9-103">Manage packet captures with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="615a9-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="615a9-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="615a9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="615a9-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="615a9-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="615a9-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="615a9-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="615a9-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="615a9-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="615a9-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="615a9-109">Ağ İzleyicisi paket yakalama toocreate yakalama oturumları tootrack trafiği tooand bir sanal makineden sağlar.</span><span class="sxs-lookup"><span data-stu-id="615a9-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="615a9-110">Filtreler, yalnızca istediğiniz hello trafiği yakalamak hello yakalama oturum tooensure için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="615a9-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="615a9-111">Paket yakalama toodiagnose ağ anormallikleri Tepkisel ve önceden yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="615a9-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="615a9-112">Diğer kullanımlar bilgi ağ yetkisiz erişim, toodebug istemci-sunucu iletişimleri ve daha fazlasını sağlamasını ağ istatistikleri toplama içerir.</span><span class="sxs-lookup"><span data-stu-id="615a9-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="615a9-113">Mümkün tooremotely tetikleyici paket yakalamaları olma yoluyla bu özelliği bir paket yakalama el ile ve değerli zaman kazandırır hello istenen makine üzerinde çalışan hello yük kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="615a9-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="615a9-114">Bu makalede bizim nesil CLI hello kaynak yönetimi dağıtım modeli için Azure CLI 2.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="615a9-114">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="615a9-115">Bu makaledeki adımları tooperform Merhaba, çok ihtiyacınız[hello Azure komut satırı arabirimi Mac, Linux ve Windows (Azure CLI) için yükleme](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="615a9-115">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

<span data-ttu-id="615a9-116">Bu makalede paket yakalama için şu anda kullanılabilir farklı yönetim görevleri hello alır.</span><span class="sxs-lookup"><span data-stu-id="615a9-116">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="615a9-117">**Paket yakalama Başlat**</span><span class="sxs-lookup"><span data-stu-id="615a9-117">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="615a9-118">**Paket yakalama işlemini durdurun**</span><span class="sxs-lookup"><span data-stu-id="615a9-118">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="615a9-119">**Paket yakalama Sil**</span><span class="sxs-lookup"><span data-stu-id="615a9-119">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="615a9-120">**Paket yakalama indirin**</span><span class="sxs-lookup"><span data-stu-id="615a9-120">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="615a9-121">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="615a9-121">Before you begin</span></span>

<span data-ttu-id="615a9-122">Bu makalede, kaynakları aşağıdaki hello olduğu varsayılır:</span><span class="sxs-lookup"><span data-stu-id="615a9-122">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="615a9-123">Bir örneği toocreate paket yakalama istediğiniz Ağ İzleyicisinin hello bölgede</span><span class="sxs-lookup"><span data-stu-id="615a9-123">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="615a9-124">Merhaba paket sahip bir sanal makine uzantısı etkin yakalayın.</span><span class="sxs-lookup"><span data-stu-id="615a9-124">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="615a9-125">Paket yakalama hello sanal makine üzerinde çalışan bir aracı toobe gerektirir.</span><span class="sxs-lookup"><span data-stu-id="615a9-125">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="615a9-126">Merhaba Aracısı bir uzantısı olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="615a9-126">hello Agent is installed as an extension.</span></span> <span data-ttu-id="615a9-127">VM uzantıları hakkında yönergeler için ziyaret [sanal makine uzantıları ve özellikleri](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="615a9-127">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="615a9-128">VM uzantısı yükleyin</span><span class="sxs-lookup"><span data-stu-id="615a9-128">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="615a9-129">1. Adım</span><span class="sxs-lookup"><span data-stu-id="615a9-129">Step 1</span></span>

<span data-ttu-id="615a9-130">Merhaba çalıştırmak `az vm extension set` cmdlet tooinstall hello paket Yakalama aracı hello Konuk sanal makinedeki.</span><span class="sxs-lookup"><span data-stu-id="615a9-130">Run hello `az vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="615a9-131">Windows sanal makineler için:</span><span class="sxs-lookup"><span data-stu-id="615a9-131">For Windows virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentWindows --version 1.4
```

<span data-ttu-id="615a9-132">Linux sanal makineleri için:</span><span class="sxs-lookup"><span data-stu-id="615a9-132">For Linux virtual machines:</span></span>

```azurecli
az vm extension set --resource-group resourceGroupName --vm-name virtualMachineName --publisher Microsoft.Azure.NetworkWatcher --name NetworkWatcherAgentLinux--version 1.4
````

### <a name="step-2"></a><span data-ttu-id="615a9-133">2. Adım</span><span class="sxs-lookup"><span data-stu-id="615a9-133">Step 2</span></span>

<span data-ttu-id="615a9-134">Aracı hello tooensure yüklü hello çalıştırmak `vm extension get` cmdlet'i ve hello kaynak grubu ve sanal makine adı geçirin.</span><span class="sxs-lookup"><span data-stu-id="615a9-134">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="615a9-135">Merhaba sonuç listesi tooensure hello aracısı yüklü olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="615a9-135">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
az vm extension show -resource-group resourceGroupName --vm-name virtualMachineName --name NetworkWatcherAgentWindows
```

<span data-ttu-id="615a9-136">Aşağıdaki örnek hello hello yanıt çalışmasını örneğidir`az vm extension show`</span><span class="sxs-lookup"><span data-stu-id="615a9-136">hello following sample is an example of hello response from running `az vm extension show`</span></span>

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

## <a name="start-a-packet-capture"></a><span data-ttu-id="615a9-137">Paket yakalama Başlat</span><span class="sxs-lookup"><span data-stu-id="615a9-137">Start a packet capture</span></span>

<span data-ttu-id="615a9-138">Merhaba önceki adımları tamamlandıktan sonra hello paket yakalama Aracısı hello sanal makineye yüklenir.</span><span class="sxs-lookup"><span data-stu-id="615a9-138">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="615a9-139">1. Adım</span><span class="sxs-lookup"><span data-stu-id="615a9-139">Step 1</span></span>

<span data-ttu-id="615a9-140">Merhaba sonraki adıma tooretrieve hello Ağ İzleyicisi örneğidir.</span><span class="sxs-lookup"><span data-stu-id="615a9-140">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="615a9-141">Ağ İzleyicisi Merhaba kurulacağı adını toohello geçirilen `az network watcher show` 4. adımda cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="615a9-141">TThe name of hello Network Watcher is passed toohello `az network watcher show` cmdlet in step 4.</span></span>

```azurecli
az network watcher show -resource-group resourceGroup -name networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="615a9-142">2. Adım</span><span class="sxs-lookup"><span data-stu-id="615a9-142">Step 2</span></span>

<span data-ttu-id="615a9-143">Bir depolama hesabı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="615a9-143">Retrieve a storage account.</span></span> <span data-ttu-id="615a9-144">Bu depolama hesabı kullanılan toostore hello paket yakalama dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="615a9-144">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="615a9-145">3. Adım</span><span class="sxs-lookup"><span data-stu-id="615a9-145">Step 3</span></span>

<span data-ttu-id="615a9-146">Filtreler hello paket yakalama tarafından depolanan kullanılan toolimit hello veriler olabilir.</span><span class="sxs-lookup"><span data-stu-id="615a9-146">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="615a9-147">Merhaba aşağıdaki örnekte bir paket yakalama kurduğunuzda birkaç filtrelerle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="615a9-147">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="615a9-148">Merhaba ilk üç filtreleri giden TCP trafiğine yalnızca yerel bir IP 10.0.0.3 toplamak 20, 80 ve 443 toodestination bağlantı noktaları.</span><span class="sxs-lookup"><span data-stu-id="615a9-148">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="615a9-149">Merhaba son filtre yalnızca UDP trafiğini toplar.</span><span class="sxs-lookup"><span data-stu-id="615a9-149">hello last filter collects only UDP traffic.</span></span>

```azurecli
az network watcher packet-capture create --resource-group {resoureceurceGroupName} --vm {vmName} --name packetCaptureName --storage-account gwteststorage123abc --filters "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="615a9-150">Merhaba aşağıdaki örnekte olduğu hello çalışmasını hello beklenen çıktı `az network watcher packet-capture create` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="615a9-150">hello following example is hello expected output from running hello `az network watcher packet-capture create` cmdlet.</span></span>

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

## <a name="get-a-packet-capture"></a><span data-ttu-id="615a9-151">Paket yakalama Al</span><span class="sxs-lookup"><span data-stu-id="615a9-151">Get a packet capture</span></span>

<span data-ttu-id="615a9-152">Merhaba çalıştıran `az network watcher packet-capture show` cmdlet, şu anda çalışan ya da tamamlanmış bir paket yakalama hello durumunu alır.</span><span class="sxs-lookup"><span data-stu-id="615a9-152">Running hello `az network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
az network watcher packet-capture show --name packetCaptureName --location westcentralus
```

<span data-ttu-id="615a9-153">Merhaba aşağıdaki örnekte olduğu hello hello çıktısını `az network watcher packet-capture show` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="615a9-153">hello following example is hello output from hello `az network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="615a9-154">Merhaba yakalama işlemi tamamlandıktan sonra hello aşağıdaki örnektir.</span><span class="sxs-lookup"><span data-stu-id="615a9-154">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="615a9-155">StopReason TimeExceeded ile Merhaba PacketCaptureStatus değer durdurulmuş.</span><span class="sxs-lookup"><span data-stu-id="615a9-155">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="615a9-156">Bu değer hello paket yakalama başarılı oldu ve onun kez çalıştıktan gösterir.</span><span class="sxs-lookup"><span data-stu-id="615a9-156">This value shows that hello packet capture was successful and ran its time.</span></span>

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

## <a name="stop-a-packet-capture"></a><span data-ttu-id="615a9-157">Paket yakalama işlemini durdurun</span><span class="sxs-lookup"><span data-stu-id="615a9-157">Stop a packet capture</span></span>

<span data-ttu-id="615a9-158">Merhaba çalıştırarak `az network watcher packet-capture stop` yakalama oturumu Sürüyor ise cmdlet durduruldu.</span><span class="sxs-lookup"><span data-stu-id="615a9-158">By running hello `az network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
az network watcher packet-capture stop --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="615a9-159">Hello cmdlet yanıt verir, o anda çalışan bir yakalama oturumu veya zaten durdurulmuş olan bir oturumu.</span><span class="sxs-lookup"><span data-stu-id="615a9-159">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="615a9-160">Paket yakalama Sil</span><span class="sxs-lookup"><span data-stu-id="615a9-160">Delete a packet capture</span></span>

```azurecli
az network watcher packet-capture delete --name packetCaptureName --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="615a9-161">Paket yakalama silindiğinde hello depolama hesabındaki hello dosya silinmez.</span><span class="sxs-lookup"><span data-stu-id="615a9-161">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="615a9-162">Paket yakalama indirin</span><span class="sxs-lookup"><span data-stu-id="615a9-162">Download a packet capture</span></span>

<span data-ttu-id="615a9-163">Paket yakalama oturumunuz tamamladıktan sonra hello yakalama dosyasını karşıya yüklenen tooblob depolama veya tooa yerel dosya hello VM üzerinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="615a9-163">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="615a9-164">Merhaba paket yakalama Hello depolama konumu hello oturum oluşturma sırasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="615a9-164">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="615a9-165">Bu yakalama uygun aracı tooaccess kaydedilmiş tooa depolama hesabıdır burada indirilebilir Microsoft Azure Storage Gezgini dosyaları: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="615a9-165">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="615a9-166">Bir depolama hesabı belirtilirse, paket yakalama dosyalarını tooa depolama hesabı konumu aşağıdaki hello kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="615a9-166">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="615a9-167">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="615a9-167">Next steps</span></span>

<span data-ttu-id="615a9-168">Nasıl sanal makine uyarılarla tooautomate paket görüntüleyerek yakalar öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="615a9-168">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="615a9-169">Belirli trafik içinde veya dışında VM ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="615a9-169">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
