---
title: "Paket yakalama Azure Ağ İzleyicisi - Azure portal ile yönetme | Microsoft Docs"
description: "Bu sayfa, Azure portalını kullanarak Ağ İzleyicisi'nin paket yakalama özelliği yönetmek açıklanmaktadır"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 33390532cc4fc1129a4f960d589f41bc95e5a1ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-the-portal"></a><span data-ttu-id="9c059-103">Paket yakalama Portalı'nı kullanarak Azure Ağ İzleyicisi ile yönetme</span><span class="sxs-lookup"><span data-stu-id="9c059-103">Manage packet captures with Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="9c059-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="9c059-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="9c059-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9c059-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="9c059-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9c059-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="9c059-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9c059-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="9c059-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="9c059-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="9c059-109">Ağ İzleyicisi paket yakalama, bir sanal makine gelen ve giden trafiği izlemek için yakalama oturumları oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="9c059-109">Network Watcher packet capture allows you to create capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="9c059-110">Filtreler yalnızca trafiği yakalama emin olmak yakalama oturumu için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="9c059-110">Filters are provided for the capture session to ensure you capture only the traffic you want.</span></span> <span data-ttu-id="9c059-111">Paket yakalama Tepkisel hem de önceden ağ anormallikleri tanılamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9c059-111">Packet capture helps to diagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="9c059-112">Diğer kullanımlar ağ yetkisiz erişim, istemci-sunucu iletişimleri ve çok daha fazlasını hata ayıklamak için bilgi sağlamasını ağ istatistikleri toplama içerir.</span><span class="sxs-lookup"><span data-stu-id="9c059-112">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span> <span data-ttu-id="9c059-113">Erişebildiklerinden uzaktan paket yakalamaları tetiklemek için bir paket yakalama el ile ve değerli zaman kazandırır istenen makine üzerinde çalışan iş yükünü Bu yetenek kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="9c059-113">By being able to remotely trigger packet captures, this capability eases the burden of running a packet capture manually and on the desired machine, which saves valuable time.</span></span>

<span data-ttu-id="9c059-114">Bu makalede paket yakalama için şu anda kullanılabilir farklı yönetim görevleri yoluyla alır.</span><span class="sxs-lookup"><span data-stu-id="9c059-114">This article takes you through the different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="9c059-115">**Paket yakalama Başlat**</span><span class="sxs-lookup"><span data-stu-id="9c059-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="9c059-116">**Paket yakalama işlemini durdurun**</span><span class="sxs-lookup"><span data-stu-id="9c059-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="9c059-117">**Paket yakalama Sil**</span><span class="sxs-lookup"><span data-stu-id="9c059-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="9c059-118">**Paket yakalama indirin**</span><span class="sxs-lookup"><span data-stu-id="9c059-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="9c059-119">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="9c059-119">Before you begin</span></span>

<span data-ttu-id="9c059-120">Bu makalede, aşağıdaki kaynaklara sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="9c059-120">This article assumes that you have the following resources:</span></span>

- <span data-ttu-id="9c059-121">Paket yakalama oluşturmak istediğiniz bölgede Ağ İzleyicisi örneği</span><span class="sxs-lookup"><span data-stu-id="9c059-121">An instance of Network Watcher in the region you want to create a packet capture</span></span>
- <span data-ttu-id="9c059-122">Bir sanal makine etkin paket yakalama uzantısına sahip.</span><span class="sxs-lookup"><span data-stu-id="9c059-122">A virtual machine with the packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c059-123">Paket yakalama gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="9c059-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="9c059-124">Bir Windows VM uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Linux için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="9c059-124">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-the-portal"></a><span data-ttu-id="9c059-125">Paket Yakalama aracı uzantısı portal üzerinden</span><span class="sxs-lookup"><span data-stu-id="9c059-125">Packet Capture agent extension through the portal</span></span>

<span data-ttu-id="9c059-126">Portal üzerinden paket yakalama VM aracısı yüklemek için sanal makinenize gidin, **uzantıları** > **Ekle** arayın ve **için Ağ İzleyicisi Aracısı Windows**</span><span class="sxs-lookup"><span data-stu-id="9c059-126">To install the packet capture VM agent through the portal, navigate to your virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![Aracı görünümü][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="9c059-128">Paket yakalama genel bakış</span><span class="sxs-lookup"><span data-stu-id="9c059-128">Packet Capture overview</span></span>

<span data-ttu-id="9c059-129">Gidin [Azure portal](https://portal.azure.com) tıklatıp **ağ** > **Ağ İzleyicisi** > **paket yakalama**</span><span class="sxs-lookup"><span data-stu-id="9c059-129">Navigate to the [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="9c059-130">Genel bakış sayfasında, tüm paket listesini olsun durumu mevcut yakalar gösterir.</span><span class="sxs-lookup"><span data-stu-id="9c059-130">The overview page shows a list of all packet captures that exist no matter the state.</span></span>

> [!NOTE]
> <span data-ttu-id="9c059-131">Paket yakalama bağlantı noktası 443 üzerinden depolama hesabı bağlantı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9c059-131">Packet capture requires connectivity to the storage account over port 443.</span></span>

![Paket yakalama genel bakış ekranı][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="9c059-133">Paket yakalama Başlat</span><span class="sxs-lookup"><span data-stu-id="9c059-133">Start a packet capture</span></span>

<span data-ttu-id="9c059-134">Tıklatın **Ekle** bir paket yakalama oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9c059-134">Click **Add** to create a packet capture.</span></span>

<span data-ttu-id="9c059-135">Bir paket yakalama tanımlanabilir özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9c059-135">The properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="9c059-136">**Ana ayarları**</span><span class="sxs-lookup"><span data-stu-id="9c059-136">**Main settings**</span></span>

- <span data-ttu-id="9c059-137">**Abonelik** -bu değeri kullanılan abonelik, Ağ İzleyicisi örneği her abonelik için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9c059-137">**Subscription** - This value is the subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="9c059-138">**Kaynak grubu** -sanal makinenin hedeflenen kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="9c059-138">**Resource group** - The resource group of the virtual machine that is being targeted.</span></span>
- <span data-ttu-id="9c059-139">**Hedef sanal makine** -paket yakalama çalıştıran sanal makine</span><span class="sxs-lookup"><span data-stu-id="9c059-139">**Target virtual machine** - The virtual machine that is running the packet capture</span></span>
- <span data-ttu-id="9c059-140">**Paket yakalama adı** -bu değer paket yakalama adıdır.</span><span class="sxs-lookup"><span data-stu-id="9c059-140">**Packet capture name** - This value is the name of the packet capture.</span></span>

<span data-ttu-id="9c059-141">**Yapılandırma Yakalama**</span><span class="sxs-lookup"><span data-stu-id="9c059-141">**Capture configuration**</span></span>

- <span data-ttu-id="9c059-142">**Depolama hesabı** -paket yakalama bir depolama hesabında kaydedilip kaydedilmeyeceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="9c059-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="9c059-143">**Dosya** -paket yakalama sanal makinede yerel olarak kaydedilirse belirler.</span><span class="sxs-lookup"><span data-stu-id="9c059-143">**File** - Determines if a packet capture is saved locally on the virtual machine.</span></span>
- <span data-ttu-id="9c059-144">**Depolama hesapları** - seçili paket yakalama kaydetmek için depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="9c059-144">**Storage Accounts** - The selected storage account to save the packet capture in.</span></span> <span data-ttu-id="9c059-145">Varsayılan konumdur https://{storage hesap name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription kimliği} /resourcegroups/ {kaynak grubu name}/providers/microsoft.compute/virtualmachines/{virtual makine adı} / {YY} / {MM} / {gg} / {ss} packetcapture__{MM}_{SS} _ {XXX} .cap.</span><span class="sxs-lookup"><span data-stu-id="9c059-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="9c059-146">(Yalnızca etkin olup **depolama** seçili)</span><span class="sxs-lookup"><span data-stu-id="9c059-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="9c059-147">**Yerel dosya yolu** -paket yakalama kaydetmek için bir sanal makinede yerel yolu.</span><span class="sxs-lookup"><span data-stu-id="9c059-147">**Local file path** - The local path on a virtual machine to save the packet capture.</span></span> <span data-ttu-id="9c059-148">(Yalnızca etkin olup **dosya** seçilir).</span><span class="sxs-lookup"><span data-stu-id="9c059-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="9c059-149">Geçerli bir yol sağlanmalıdır</span><span class="sxs-lookup"><span data-stu-id="9c059-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="9c059-150">**Paket başına en fazla bayt** - sayı yakalanan bayt gelen her paket, tüm baytlar boş bırakılırsa yakalanır.</span><span class="sxs-lookup"><span data-stu-id="9c059-150">**Maximum bytes per packet** - The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="9c059-151">**Oturum başına en fazla bayt** - toplam değeri paket yakalama durakları ulaşıldıktan sonra yakalanan bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="9c059-151">**Maximum bytes per session** - Total number of bytes that are captured, once the value is reached the packet capture stops.</span></span>
- <span data-ttu-id="9c059-152">**Süre (saniye)** -durdurmak paket yakalama için zaman sınırını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="9c059-152">**Time limit (seconds)** - Sets a time limit for the packet capture to stop.</span></span> <span data-ttu-id="9c059-153">Varsayılan değer 18000 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="9c059-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="9c059-154">Paket depolama yakalar için premium depolama hesapları şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="9c059-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="9c059-155">**(İsteğe bağlı) filtreleme**</span><span class="sxs-lookup"><span data-stu-id="9c059-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="9c059-156">**Protokol** -paket yakalama için filtre uygulamak için protokol.</span><span class="sxs-lookup"><span data-stu-id="9c059-156">**Protocol** - The protocol to filter for the packet capture.</span></span> <span data-ttu-id="9c059-157">Kullanılabilir TCP, UDP ve herhangi bir değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="9c059-157">The available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="9c059-158">**Yerel IP adresi** -bu değer, yerel IP adresi bu filtre değeri eşleştiği paket için paket yakalama filtreler.</span><span class="sxs-lookup"><span data-stu-id="9c059-158">**Local IP address** - This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>
- <span data-ttu-id="9c059-159">**Yerel bağlantı noktası** -bu değer, yerel bağlantı noktası bu filtre değeri eşleştiği paket için paket yakalama filtreler.</span><span class="sxs-lookup"><span data-stu-id="9c059-159">**Local port** - This value filters the packet capture to packets where the local port matches this filter value.</span></span>
- <span data-ttu-id="9c059-160">**Uzak IP adresi** -uzak IP Bu filtre değeri eşleştiği paket için paket yakalama bu değeri filtreler.</span><span class="sxs-lookup"><span data-stu-id="9c059-160">**Remote IP address** - This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>
- <span data-ttu-id="9c059-161">**Uzak bağlantı noktası** -uzak bağlantı noktası bu filtre değeri eşleştiği paket için paket yakalama bu değeri filtreler.</span><span class="sxs-lookup"><span data-stu-id="9c059-161">**Remote port** - This value filters the packet capture to packets where the remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="9c059-162">Bağlantı noktası ve IP adresi değerleri, tek bir değer, değer aralığı veya bir kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="9c059-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="9c059-163">(diğer bir deyişle, bağlantı noktası 80-1024 için) İstediğiniz sayıda filtreleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c059-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="9c059-164">Değerleri doldurulduktan sonra tıklayın **Tamam** paket yakalama oluşturma.</span><span class="sxs-lookup"><span data-stu-id="9c059-164">Once the values are filled out, click **OK** to create the packet capture.</span></span>

![Paket yakalama oluşturma][2]

<span data-ttu-id="9c059-166">Paket yakalama ayarlamak süre sona erdiğinde, paket yakalama durdurur ve gözden geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9c059-166">After the time limit set on the packet capture has expired, the packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="9c059-167">Paket yakalama oturumları el ile de durdurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9c059-167">You can also manually stop the packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="9c059-168">Paket yakalama Sil</span><span class="sxs-lookup"><span data-stu-id="9c059-168">Delete a packet capture</span></span>

<span data-ttu-id="9c059-169">Paket yakalama Görüntüle'yi tıklatın **bağlam menüsü** (...) veya sağ tıklayın ve tıklayın **silmek** paket yakalama durdurmak için</span><span class="sxs-lookup"><span data-stu-id="9c059-169">In the packet capture view, click the **context menu** (...) or right click, and click **delete** to stop the packet capture</span></span>

![Paket yakalama Sil][3]

> [!NOTE]
> <span data-ttu-id="9c059-171">Paket yakalama silindiğinde depolama hesabındaki dosya silinmez.</span><span class="sxs-lookup"><span data-stu-id="9c059-171">Deleting a packet capture does not delete the file in the storage account.</span></span>

<span data-ttu-id="9c059-172">Paket yakalama silmek, tıklatın istediğinizi onaylamak için sorulur **Evet**</span><span class="sxs-lookup"><span data-stu-id="9c059-172">You are asked to confirm you want to delete the packet capture, click **Yes**</span></span>

![Onaylama][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="9c059-174">Paket yakalama işlemini durdurun</span><span class="sxs-lookup"><span data-stu-id="9c059-174">Stop a packet capture</span></span>

<span data-ttu-id="9c059-175">Paket yakalama Görüntüle'yi tıklatın **bağlam menüsü** (...) veya sağ tıklayın ve tıklayın **durdurmak** paket yakalama durdurmak için</span><span class="sxs-lookup"><span data-stu-id="9c059-175">In the packet capture view, click the **context menu** (...) or right click, and click **Stop** to stop the packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="9c059-176">Paket yakalama indirin</span><span class="sxs-lookup"><span data-stu-id="9c059-176">Download a packet capture</span></span>

<span data-ttu-id="9c059-177">Paket yakalama oturumunuz tamamladıktan sonra yakalama dosyasını blob depolama alanına veya VM üzerindeki yerel bir dosyaya yüklenir.</span><span class="sxs-lookup"><span data-stu-id="9c059-177">Once your packet capture session has completed, the capture file is uploaded to blob storage or to a local file on the VM.</span></span> <span data-ttu-id="9c059-178">Paket yakalama depolama konumunu oturum oluşturma sırasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="9c059-178">The storage location of the packet capture is defined at creation of the session.</span></span> <span data-ttu-id="9c059-179">Bunlar erişmek için uygun bir aracı yakalama dosyalarını bir depolama hesabına kaydedilmiş olan burada indirilebilir Microsoft Azure Storage Gezgini: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="9c059-179">A convenient tool to access these capture files saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="9c059-180">Bir depolama hesabı belirtilirse, paket yakalama dosyaları şu konumda bir depolama hesabına kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="9c059-180">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="9c059-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9c059-181">Next steps</span></span>

<span data-ttu-id="9c059-182">Sanal makine uyarılarla paket yakalamaları görüntüleyerek otomatikleştirmeyi öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="9c059-182">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="9c059-183">Belirli trafik içinde veya dışında VM ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9c059-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













