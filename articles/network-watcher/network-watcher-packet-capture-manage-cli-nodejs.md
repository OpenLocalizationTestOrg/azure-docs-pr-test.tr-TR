---
title: "Paket yakalama Azure Ağ İzleyicisi - Azure CLI 1.0 ile yönetme | Microsoft Docs"
description: "Bu sayfa, Azure CLI 1.0 kullanarak Ağ İzleyicisi'nin paket yakalama özelliği yönetmek açıklanmaktadır"
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
ms.openlocfilehash: 91588910334859c1ea77186674d5bfb31b311b36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="36b51-103">Paket yakalama Azure CLI 1.0 kullanarak Azure Ağ İzleyicisi ile yönetme</span><span class="sxs-lookup"><span data-stu-id="36b51-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="36b51-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="36b51-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="36b51-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="36b51-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="36b51-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="36b51-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="36b51-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="36b51-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="36b51-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="36b51-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="36b51-109">Ağ İzleyicisi paket yakalama, bir sanal makine gelen ve giden trafiği izlemek için yakalama oturumları oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="36b51-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="36b51-110">Filtreler yalnızca trafiği yakalama emin olmak yakalama oturumu için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="36b51-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="36b51-111">Paket yakalama Tepkisel hem de önceden ağ anormallikleri tanılamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="36b51-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="36b51-112">Diğer kullanımlar ağ yetkisiz erişim, istemci-sunucu iletişimleri ve çok daha fazlasını hata ayıklamak için bilgi sağlamasını ağ istatistikleri toplama içerir.</span><span class="sxs-lookup"><span data-stu-id="36b51-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="36b51-113">Erişebildiklerinden uzaktan paket yakalamaları tetiklemek için bir paket yakalama el ile ve değerli zaman kazandırır istenen makine üzerinde çalışan iş yükünü Bu yetenek kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="36b51-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="36b51-114">Bu makalede, platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="36b51-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="36b51-115">Bu makalede paket yakalama için şu anda kullanılabilir farklı yönetim görevleri yoluyla alır.</span><span class="sxs-lookup"><span data-stu-id="36b51-115">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="36b51-116">**Paket yakalama Başlat**</span><span class="sxs-lookup"><span data-stu-id="36b51-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="36b51-117">**Paket yakalama işlemini durdurun**</span><span class="sxs-lookup"><span data-stu-id="36b51-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="36b51-118">**Paket yakalama Sil**</span><span class="sxs-lookup"><span data-stu-id="36b51-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="36b51-119">**Paket yakalama indirin**</span><span class="sxs-lookup"><span data-stu-id="36b51-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="36b51-120">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="36b51-120">Before you begin</span></span>

<span data-ttu-id="36b51-121">Bu makalede, aşağıdaki kaynaklara sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="36b51-121">This article assumes you have the following resources:</span></span>

- <span data-ttu-id="36b51-122">Paket yakalama oluşturmak istediğiniz bölgede Ağ İzleyicisi örneği</span><span class="sxs-lookup"><span data-stu-id="36b51-122">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="36b51-123">Bir sanal makine etkin paket yakalama uzantısına sahip.</span><span class="sxs-lookup"><span data-stu-id="36b51-123">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="36b51-124">Paket yakalama sanal makine üzerinde çalışan bir aracının gerektirir.</span><span class="sxs-lookup"><span data-stu-id="36b51-124">Packet capture requires an agent to be running on the virtual machine.</span></span> <span data-ttu-id="36b51-125">Aracı bir uzantısı olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="36b51-125">The Agent is installed as an extension.</span></span> <span data-ttu-id="36b51-126">VM uzantıları hakkında yönergeler için ziyaret [sanal makine uzantıları ve özellikleri](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="36b51-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="36b51-127">VM uzantısı yükleyin</span><span class="sxs-lookup"><span data-stu-id="36b51-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="36b51-128">1. Adım</span><span class="sxs-lookup"><span data-stu-id="36b51-128">Step 1</span></span>

<span data-ttu-id="36b51-129">Çalıştırma `azure vm extension set` cmdlet'ini paket yakalama Aracısı Konuk sanal makineye yükleyin.</span><span class="sxs-lookup"><span data-stu-id="36b51-129">Run the `azure vm extension set` cmdlet to install the packet capture agent on the guest virtual machine.</span></span>

<span data-ttu-id="36b51-130">Windows sanal makineler için:</span><span class="sxs-lookup"><span data-stu-id="36b51-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="36b51-131">Linux sanal makineleri için:</span><span class="sxs-lookup"><span data-stu-id="36b51-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="36b51-132">2. Adım</span><span class="sxs-lookup"><span data-stu-id="36b51-132">Step 2</span></span>

<span data-ttu-id="36b51-133">Aracının yüklü olduğundan emin olun, çalıştırmayı `vm extension get` cmdlet'i ve kaynak grubu ve sanal makine adı geçirin.</span><span class="sxs-lookup"><span data-stu-id="36b51-133">To ensure that the agent is installed, run the `vm extension get` cmdlet and pass it the resource group and virtual machine name.</span></span> <span data-ttu-id="36b51-134">Sonuçta elde edilen listenin aracısının yüklü olduğundan emin olmak için kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="36b51-134">Check the resulting list to ensure the agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="36b51-135">Aşağıdaki örnek yanıt çalışmasını örneğidir`azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="36b51-135">The following sample is an example of the response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up the VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="36b51-136">Paket yakalama Başlat</span><span class="sxs-lookup"><span data-stu-id="36b51-136">Start a packet capture</span></span>

<span data-ttu-id="36b51-137">Yukarıdaki adımları tamamlandıktan sonra paket yakalama Aracısı sanal makineye yüklenir.</span><span class="sxs-lookup"><span data-stu-id="36b51-137">Once the preceding steps are complete, the packet capture agent is installed on the virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="36b51-138">1. Adım</span><span class="sxs-lookup"><span data-stu-id="36b51-138">Step 1</span></span>

<span data-ttu-id="36b51-139">Ağ İzleyicisi örneği almak için sonraki adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="36b51-139">The next step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="36b51-140">Bu değişken geçirilir `network watcher show` 4. adımda cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="36b51-140">This variable is passed to the `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="36b51-141">2. Adım</span><span class="sxs-lookup"><span data-stu-id="36b51-141">Step 2</span></span>

<span data-ttu-id="36b51-142">Bir depolama hesabı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36b51-142">Retrieve a storage account.</span></span> <span data-ttu-id="36b51-143">Bu depolama hesabını paket yakalama dosyasını depolamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="36b51-143">This storage account is used to store the packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="36b51-144">3. Adım</span><span class="sxs-lookup"><span data-stu-id="36b51-144">Step 3</span></span>

<span data-ttu-id="36b51-145">Filtreler, paket yakalama tarafından depolanan verileri sınırlamak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="36b51-145">Filters can be used to limit the data that is stored by the packet capture.</span></span> <span data-ttu-id="36b51-146">Aşağıdaki örnek, bir paket yakalama kurduğunuzda birkaç filtrelerle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="36b51-146">The following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="36b51-147">İlk üç filtreleri giden TCP trafiğine yalnızca yerel bir IP 10.0.0.3 20, 80 ve 443 hedef bağlantı noktalarına toplayın.</span><span class="sxs-lookup"><span data-stu-id="36b51-147">The first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 to destination ports 20, 80 and 443.</span></span>  <span data-ttu-id="36b51-148">Son filtre yalnızca UDP trafiğini toplar.</span><span class="sxs-lookup"><span data-stu-id="36b51-148">The last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="36b51-149">Paket yakalama için birden çok filtre tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="36b51-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="36b51-150">Karmaşık filtre yapısı kullanıyorsanız, filtreleri sözdizimi hataları önlemek için bir json dosyası olarak kullanmak daha iyidir.</span><span class="sxs-lookup"><span data-stu-id="36b51-150">If you are using a complex filter structure, it is better to use filters as a json file to avoid syntax errors.</span></span> <span data-ttu-id="36b51-151">Örneğin, bayrağını kullanın "-r" (yerine "-f") ve aşağıdaki filtreleri içeren bir json dosyası konumu geçirin:</span><span class="sxs-lookup"><span data-stu-id="36b51-151">For example, use the flag "-r" (instead of "-f") and pass the location of a json file containing the following filters:</span></span>

```json
[
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"20"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"80"
    },
    {
        "protocol":"TCP",
        "remoteIPAddress":"1.1.1.1-255.255.255",
        "localIPAddress":"10.0.0.3",
        "remotePort":"443"
    },
    {
        "protocol":"UDP"
    }
]
```


<span data-ttu-id="36b51-152">Beklenen çıktı çalışmasını aşağıdaki örnekte olduğu `network watcher packet-capture create` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="36b51-152">The following example is the expected output from running the `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="36b51-153">Paket yakalama Al</span><span class="sxs-lookup"><span data-stu-id="36b51-153">Get a packet capture</span></span>

<span data-ttu-id="36b51-154">Çalışan `network watcher packet-capture show` cmdlet, şu anda çalışan ya da tamamlanmış bir paket yakalama durumunu alır.</span><span class="sxs-lookup"><span data-stu-id="36b51-154">Running the `network watcher packet-capture show` cmdlet, retrieves the status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="36b51-155">Aşağıdaki örnek çıktısı olan `network watcher packet-capture show` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="36b51-155">The following example is the output from the `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="36b51-156">Yakalama işlemi tamamlandıktan sonra aşağıdaki örnektir.</span><span class="sxs-lookup"><span data-stu-id="36b51-156">The following example is after the capture is complete.</span></span> <span data-ttu-id="36b51-157">StopReason TimeExceeded ile PacketCaptureStatus değer durdurulmuş.</span><span class="sxs-lookup"><span data-stu-id="36b51-157">The PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="36b51-158">Bu değer, paket yakalama başarılı oldu ve onun kez çalıştıktan gösterir.</span><span class="sxs-lookup"><span data-stu-id="36b51-158">This value shows that the packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes To Capture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="36b51-159">Paket yakalama işlemini durdurun</span><span class="sxs-lookup"><span data-stu-id="36b51-159">Stop a packet capture</span></span>

<span data-ttu-id="36b51-160">Çalıştırarak `network watcher packet-capture stop` yakalama oturumu Sürüyor ise cmdlet durduruldu.</span><span class="sxs-lookup"><span data-stu-id="36b51-160">By running the `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="36b51-161">Cmdlet yanıt verir, o anda çalışan bir yakalama oturumu veya zaten durdurulmuş olan bir oturumu.</span><span class="sxs-lookup"><span data-stu-id="36b51-161">The cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="36b51-162">Paket yakalama Sil</span><span class="sxs-lookup"><span data-stu-id="36b51-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="36b51-163">Paket yakalama silindiğinde depolama hesabındaki dosya silinmez.</span><span class="sxs-lookup"><span data-stu-id="36b51-163">Deleting a packet capture does not delete the file in the storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="36b51-164">Paket yakalama indirin</span><span class="sxs-lookup"><span data-stu-id="36b51-164">Download a packet capture</span></span>

<span data-ttu-id="36b51-165">Paket yakalama oturumunuz tamamladıktan sonra blob depolama alanına veya VM üzerindeki yerel bir dosyaya yakalama dosyasını karşıya yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="36b51-165">Once your packet capture session has completed, the capture file can be uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="36b51-166">Paket yakalama depolama konumunu oturum oluşturma sırasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="36b51-166">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="36b51-167">Bunlar erişmek için uygun bir aracı yakalama dosyalarını bir depolama hesabına kaydedilmiş olan burada indirilebilir Microsoft Azure Storage Gezgini: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="36b51-167">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="36b51-168">Bir depolama hesabı belirtilirse, paket yakalama dosyaları şu konumda bir depolama hesabına kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="36b51-168">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="36b51-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="36b51-169">Next steps</span></span>

<span data-ttu-id="36b51-170">Sanal makine uyarılarla paket yakalamaları görüntüleyerek otomatikleştirmeyi öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="36b51-170">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="36b51-171">Belirli trafik içinde veya dışında VM ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="36b51-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
