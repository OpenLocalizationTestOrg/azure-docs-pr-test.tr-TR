---
title: "aaaManage paket yakalar Azure Ağ İzleyicisi - Azure CLI 1.0 | Microsoft Docs"
description: "Bu sayfayı nasıl toomanage hello paket yakalama özelliği ağ Azure CLI 1.0 kullanarak izleyicisinin açıklar"
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
ms.openlocfilehash: c4b710a8d82ccaaf65876a8c2ef845aa97b5f831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="02bfe-103">Paket yakalama Azure CLI 1.0 kullanarak Azure Ağ İzleyicisi ile yönetme</span><span class="sxs-lookup"><span data-stu-id="02bfe-103">Manage packet captures with Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="02bfe-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="02bfe-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="02bfe-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="02bfe-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="02bfe-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="02bfe-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="02bfe-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="02bfe-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="02bfe-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="02bfe-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="02bfe-109">Ağ İzleyicisi paket yakalama toocreate yakalama oturumları tootrack trafiği tooand bir sanal makineden sağlar.</span><span class="sxs-lookup"><span data-stu-id="02bfe-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="02bfe-110">Filtreler, yalnızca istediğiniz hello trafiği yakalamak hello yakalama oturum tooensure için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="02bfe-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="02bfe-111">Paket yakalama toodiagnose ağ anormallikleri Tepkisel ve önceden yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="02bfe-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="02bfe-112">Diğer kullanımlar bilgi ağ yetkisiz erişim, toodebug istemci-sunucu iletişimleri ve daha fazlasını sağlamasını ağ istatistikleri toplama içerir.</span><span class="sxs-lookup"><span data-stu-id="02bfe-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="02bfe-113">Mümkün tooremotely tetikleyici paket yakalamaları olma yoluyla bu özelliği bir paket yakalama el ile ve değerli zaman kazandırır hello istenen makine üzerinde çalışan hello yük kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="02bfe-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="02bfe-114">Bu makalede, platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="02bfe-114">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="02bfe-115">Bu makalede paket yakalama için şu anda kullanılabilir farklı yönetim görevleri hello alır.</span><span class="sxs-lookup"><span data-stu-id="02bfe-115">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="02bfe-116">**Paket yakalama Başlat**</span><span class="sxs-lookup"><span data-stu-id="02bfe-116">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="02bfe-117">**Paket yakalama işlemini durdurun**</span><span class="sxs-lookup"><span data-stu-id="02bfe-117">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="02bfe-118">**Paket yakalama Sil**</span><span class="sxs-lookup"><span data-stu-id="02bfe-118">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="02bfe-119">**Paket yakalama indirin**</span><span class="sxs-lookup"><span data-stu-id="02bfe-119">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="02bfe-120">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="02bfe-120">Before you begin</span></span>

<span data-ttu-id="02bfe-121">Bu makalede, kaynakları aşağıdaki hello olduğu varsayılır:</span><span class="sxs-lookup"><span data-stu-id="02bfe-121">This article assumes you have hello following resources:</span></span>

- <span data-ttu-id="02bfe-122">Bir örneği toocreate paket yakalama istediğiniz Ağ İzleyicisinin hello bölgede</span><span class="sxs-lookup"><span data-stu-id="02bfe-122">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="02bfe-123">Merhaba paket sahip bir sanal makine uzantısı etkin yakalayın.</span><span class="sxs-lookup"><span data-stu-id="02bfe-123">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02bfe-124">Paket yakalama hello sanal makine üzerinde çalışan bir aracı toobe gerektirir.</span><span class="sxs-lookup"><span data-stu-id="02bfe-124">Packet capture requires an agent toobe running on hello virtual machine.</span></span> <span data-ttu-id="02bfe-125">Merhaba Aracısı bir uzantısı olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="02bfe-125">hello Agent is installed as an extension.</span></span> <span data-ttu-id="02bfe-126">VM uzantıları hakkında yönergeler için ziyaret [sanal makine uzantıları ve özellikleri](../virtual-machines/windows/extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="02bfe-126">For instructions on VM extensions, visit [Virtual Machine extensions and features](../virtual-machines/windows/extensions-features.md).</span></span>

## <a name="install-vm-extension"></a><span data-ttu-id="02bfe-127">VM uzantısı yükleyin</span><span class="sxs-lookup"><span data-stu-id="02bfe-127">Install VM extension</span></span>

### <a name="step-1"></a><span data-ttu-id="02bfe-128">1. Adım</span><span class="sxs-lookup"><span data-stu-id="02bfe-128">Step 1</span></span>

<span data-ttu-id="02bfe-129">Merhaba çalıştırmak `azure vm extension set` cmdlet tooinstall hello paket Yakalama aracı hello Konuk sanal makinedeki.</span><span class="sxs-lookup"><span data-stu-id="02bfe-129">Run hello `azure vm extension set` cmdlet tooinstall hello packet capture agent on hello guest virtual machine.</span></span>

<span data-ttu-id="02bfe-130">Windows sanal makineler için:</span><span class="sxs-lookup"><span data-stu-id="02bfe-130">For Windows virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentWindows -o 1.4
```

<span data-ttu-id="02bfe-131">Linux sanal makineleri için:</span><span class="sxs-lookup"><span data-stu-id="02bfe-131">For Linux virtual machines:</span></span>

```azurecli
azure vm extension set -g resourceGroupName -m virtualMachineName -p Microsoft.Azure.NetworkWatcher -r AzureNetworkWatcherExtension -n NetworkWatcherAgentLinux -o 1.4
````

### <a name="step-2"></a><span data-ttu-id="02bfe-132">2. Adım</span><span class="sxs-lookup"><span data-stu-id="02bfe-132">Step 2</span></span>

<span data-ttu-id="02bfe-133">Aracı hello tooensure yüklü hello çalıştırmak `vm extension get` cmdlet'i ve hello kaynak grubu ve sanal makine adı geçirin.</span><span class="sxs-lookup"><span data-stu-id="02bfe-133">tooensure that hello agent is installed, run hello `vm extension get` cmdlet and pass it hello resource group and virtual machine name.</span></span> <span data-ttu-id="02bfe-134">Merhaba sonuç listesi tooensure hello aracısı yüklü olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="02bfe-134">Check hello resulting list tooensure hello agent is installed.</span></span>

```azurecli
azure vm extension get -g resourceGroupName -m virtualMachineName
```

<span data-ttu-id="02bfe-135">Aşağıdaki örnek hello hello yanıt çalışmasını örneğidir`azure vm extension get`</span><span class="sxs-lookup"><span data-stu-id="02bfe-135">hello following sample is an example of hello response from running `azure vm extension get`</span></span>

```
info:    Executing command vm extension get
+ Looking up hello VM "virtualMachineName"
data:    Publisher                       Name                        Version  State
data:    ------------------------------  -----------------------     -------  ---------
data:    Microsoft.Azure.NetworkWatcher  NetworkWatcherAgentWindows  1.4      Succeeded
info:    vm extension get command OK
```

## <a name="start-a-packet-capture"></a><span data-ttu-id="02bfe-136">Paket yakalama Başlat</span><span class="sxs-lookup"><span data-stu-id="02bfe-136">Start a packet capture</span></span>

<span data-ttu-id="02bfe-137">Merhaba önceki adımları tamamlandıktan sonra hello paket yakalama Aracısı hello sanal makineye yüklenir.</span><span class="sxs-lookup"><span data-stu-id="02bfe-137">Once hello preceding steps are complete, hello packet capture agent is installed on hello virtual machine.</span></span>

### <a name="step-1"></a><span data-ttu-id="02bfe-138">1. Adım</span><span class="sxs-lookup"><span data-stu-id="02bfe-138">Step 1</span></span>

<span data-ttu-id="02bfe-139">Merhaba sonraki adıma tooretrieve hello Ağ İzleyicisi örneğidir.</span><span class="sxs-lookup"><span data-stu-id="02bfe-139">hello next step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="02bfe-140">Bu değişken toohello geçirilen `network watcher show` 4. adımda cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="02bfe-140">This variable is passed toohello `network watcher show` cmdlet in step 4.</span></span>

```azurecli
azure network watcher show -g resourceGroup -n networkWatcherName
```

### <a name="step-2"></a><span data-ttu-id="02bfe-141">2. Adım</span><span class="sxs-lookup"><span data-stu-id="02bfe-141">Step 2</span></span>

<span data-ttu-id="02bfe-142">Bir depolama hesabı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02bfe-142">Retrieve a storage account.</span></span> <span data-ttu-id="02bfe-143">Bu depolama hesabı kullanılan toostore hello paket yakalama dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="02bfe-143">This storage account is used toostore hello packet capture file.</span></span>

```azurecli
azure storage account list
```

### <a name="step-3"></a><span data-ttu-id="02bfe-144">3. Adım</span><span class="sxs-lookup"><span data-stu-id="02bfe-144">Step 3</span></span>

<span data-ttu-id="02bfe-145">Filtreler hello paket yakalama tarafından depolanan kullanılan toolimit hello veriler olabilir.</span><span class="sxs-lookup"><span data-stu-id="02bfe-145">Filters can be used toolimit hello data that is stored by hello packet capture.</span></span> <span data-ttu-id="02bfe-146">Merhaba aşağıdaki örnekte bir paket yakalama kurduğunuzda birkaç filtrelerle ayarlar.</span><span class="sxs-lookup"><span data-stu-id="02bfe-146">hello following example sets up a packet capture with several  filters.</span></span>  <span data-ttu-id="02bfe-147">Merhaba ilk üç filtreleri giden TCP trafiğine yalnızca yerel bir IP 10.0.0.3 toplamak 20, 80 ve 443 toodestination bağlantı noktaları.</span><span class="sxs-lookup"><span data-stu-id="02bfe-147">hello first three filters collect outgoing TCP traffic only from local IP 10.0.0.3 toodestination ports 20, 80 and 443.</span></span>  <span data-ttu-id="02bfe-148">Merhaba son filtre yalnızca UDP trafiğini toplar.</span><span class="sxs-lookup"><span data-stu-id="02bfe-148">hello last filter collects only UDP traffic.</span></span>

```azurecli
azure network watcher packet-capture create -g resourceGroupName -w networkWatcherName -n packetCaptureName -t targetResourceId -o storageAccountResourceId -f "[{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"20\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"80\"},{\"protocol\":\"TCP\", \"remoteIPAddress\":\"1.1.1.1-255.255.255\",\"localIPAddress\":\"10.0.0.3\", \"remotePort\":\"443\"},{\"protocol\":\"UDP\"}]"
```

<span data-ttu-id="02bfe-149">Paket yakalama için birden çok filtre tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="02bfe-149">Multiple filters can be defined for a packet capture.</span></span> <span data-ttu-id="02bfe-150">Karmaşık filtre yapısı kullanıyorsanız, bir json dosyası tooavoid sözdizimi hatalı daha iyi toouse filtreleri sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="02bfe-150">If you are using a complex filter structure, it is better toouse filters as a json file tooavoid syntax errors.</span></span> <span data-ttu-id="02bfe-151">Örneğin, hello bayrağını kullanın "-r" (yerine "-f") ve filtreleri aşağıdaki hello içeren bir json dosyası hello konumunu geçirin:</span><span class="sxs-lookup"><span data-stu-id="02bfe-151">For example, use hello flag "-r" (instead of "-f") and pass hello location of a json file containing hello following filters:</span></span>

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


<span data-ttu-id="02bfe-152">Merhaba aşağıdaki örnekte olduğu hello çalışmasını hello beklenen çıktı `network watcher packet-capture create` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="02bfe-152">hello following example is hello expected output from running hello `network watcher packet-capture create` cmdlet.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture create command OK
```

## <a name="get-a-packet-capture"></a><span data-ttu-id="02bfe-153">Paket yakalama Al</span><span class="sxs-lookup"><span data-stu-id="02bfe-153">Get a packet capture</span></span>

<span data-ttu-id="02bfe-154">Merhaba çalıştıran `network watcher packet-capture show` cmdlet, şu anda çalışan ya da tamamlanmış bir paket yakalama hello durumunu alır.</span><span class="sxs-lookup"><span data-stu-id="02bfe-154">Running hello `network watcher packet-capture show` cmdlet, retrieves hello status of a currently running, or completed packet capture.</span></span>

```azurecli
azure network watcher packet-capture show -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

<span data-ttu-id="02bfe-155">Merhaba aşağıdaki örnekte olduğu hello hello çıktısını `network watcher packet-capture show` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="02bfe-155">hello following example is hello output from hello `network watcher packet-capture show` cmdlet.</span></span> <span data-ttu-id="02bfe-156">Merhaba yakalama işlemi tamamlandıktan sonra hello aşağıdaki örnektir.</span><span class="sxs-lookup"><span data-stu-id="02bfe-156">hello following example is after hello capture is complete.</span></span> <span data-ttu-id="02bfe-157">StopReason TimeExceeded ile Merhaba PacketCaptureStatus değer durdurulmuş.</span><span class="sxs-lookup"><span data-stu-id="02bfe-157">hello PacketCaptureStatus value is Stopped, with a StopReason of TimeExceeded.</span></span> <span data-ttu-id="02bfe-158">Bu değer hello paket yakalama başarılı oldu ve onun kez çalıştıktan gösterir.</span><span class="sxs-lookup"><span data-stu-id="02bfe-158">This value shows that hello packet capture was successful and ran its time.</span></span>

```
data:    Name                            : packetCaptureName
data:    Etag                            : W/"d59bb2d2-dc95-43da-b740-e0ef8fcacecb"
data:    Target                          : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Compute/virtualMachines/testVM
data:    Bytes tooCapture Per Packet     : 0
data:    Total Bytes Per Session         : 1073741824
data:    Time Limit In Seconds           : 18000
data:    Storage Location:
data:      Storage Id                    : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/resourceGroupName/providers/Microsoft.Storage/storageAccounts/testStorage
data:      Storage Path                  : https://testStorage.blob.core.windows.net/network-watcher-logs/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/testRG/providers/microsoft.compute/virtualmachines/testVM/2017/02/17/packetcapture_01_21_18_145.cap
data:    Filters                         : []
data:    Provisioning State              : Succeeded
info:    network watcher packet-capture show command OK
```

## <a name="stop-a-packet-capture"></a><span data-ttu-id="02bfe-159">Paket yakalama işlemini durdurun</span><span class="sxs-lookup"><span data-stu-id="02bfe-159">Stop a packet capture</span></span>

<span data-ttu-id="02bfe-160">Merhaba çalıştırarak `network watcher packet-capture stop` yakalama oturumu Sürüyor ise cmdlet durduruldu.</span><span class="sxs-lookup"><span data-stu-id="02bfe-160">By running hello `network watcher packet-capture stop` cmdlet, if a capture session is in progress it is stopped.</span></span>

```azurecli
azure network watcher packet-capture stop -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="02bfe-161">Hello cmdlet yanıt verir, o anda çalışan bir yakalama oturumu veya zaten durdurulmuş olan bir oturumu.</span><span class="sxs-lookup"><span data-stu-id="02bfe-161">hello cmdlet returns no response when ran on a currently running capture session or an existing session that has already stopped.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="02bfe-162">Paket yakalama Sil</span><span class="sxs-lookup"><span data-stu-id="02bfe-162">Delete a packet capture</span></span>

```azurecli
azure network watcher packet-capture delete -g resourceGroupName -w networkWatcherName -n packetCaptureName
```

> [!NOTE]
> <span data-ttu-id="02bfe-163">Paket yakalama silindiğinde hello depolama hesabındaki hello dosya silinmez.</span><span class="sxs-lookup"><span data-stu-id="02bfe-163">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="02bfe-164">Paket yakalama indirin</span><span class="sxs-lookup"><span data-stu-id="02bfe-164">Download a packet capture</span></span>

<span data-ttu-id="02bfe-165">Paket yakalama oturumunuz tamamladıktan sonra hello yakalama dosyasını karşıya yüklenen tooblob depolama veya tooa yerel dosya hello VM üzerinde olabilir.</span><span class="sxs-lookup"><span data-stu-id="02bfe-165">Once your packet capture session has completed, hello capture file can be uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="02bfe-166">Merhaba paket yakalama Hello depolama konumu hello oturum oluşturma sırasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="02bfe-166">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="02bfe-167">Bu yakalama uygun aracı tooaccess kaydedilmiş tooa depolama hesabıdır burada indirilebilir Microsoft Azure Storage Gezgini dosyaları: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="02bfe-167">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="02bfe-168">Bir depolama hesabı belirtilirse, paket yakalama dosyalarını tooa depolama hesabı konumu aşağıdaki hello kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="02bfe-168">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="02bfe-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="02bfe-169">Next steps</span></span>

<span data-ttu-id="02bfe-170">Nasıl sanal makine uyarılarla tooautomate paket görüntüleyerek yakalar öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="02bfe-170">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="02bfe-171">Belirli trafik içinde veya dışında VM ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="02bfe-171">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
