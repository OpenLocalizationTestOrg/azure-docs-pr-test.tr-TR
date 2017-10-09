---
title: "aaaManage paket yakalar Azure Ağ İzleyicisi - Azure portalı | Microsoft Docs"
description: "Bu sayfayı nasıl toomanage hello paket yakalama özelliği ağ Azure portalını kullanarak izleyicisinin açıklar"
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
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="de332-103">Paket yakalama hello portalı kullanarak Azure Ağ İzleyicisi ile yönetme</span><span class="sxs-lookup"><span data-stu-id="de332-103">Manage packet captures with Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="de332-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="de332-104">Azure portal</span></span>](network-watcher-packet-capture-manage-portal.md)
> - [<span data-ttu-id="de332-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="de332-105">PowerShell</span></span>](network-watcher-packet-capture-manage-powershell.md)
> - [<span data-ttu-id="de332-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="de332-106">CLI 1.0</span></span>](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [<span data-ttu-id="de332-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="de332-107">CLI 2.0</span></span>](network-watcher-packet-capture-manage-cli.md)
> - [<span data-ttu-id="de332-108">Azure REST API'si</span><span class="sxs-lookup"><span data-stu-id="de332-108">Azure REST API</span></span>](network-watcher-packet-capture-manage-rest.md)

<span data-ttu-id="de332-109">Ağ İzleyicisi paket yakalama toocreate yakalama oturumları tootrack trafiği tooand bir sanal makineden sağlar.</span><span class="sxs-lookup"><span data-stu-id="de332-109">Network Watcher packet capture allows you toocreate capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="de332-110">Filtreler, yalnızca istediğiniz hello trafiği yakalamak hello yakalama oturum tooensure için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="de332-110">Filters are provided for hello capture session tooensure you capture only hello traffic you want.</span></span> <span data-ttu-id="de332-111">Paket yakalama toodiagnose ağ anormallikleri Tepkisel ve önceden yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="de332-111">Packet capture helps toodiagnose network anomalies both reactively and proactively.</span></span> <span data-ttu-id="de332-112">Diğer kullanımlar bilgi ağ yetkisiz erişim, toodebug istemci-sunucu iletişimleri ve daha fazlasını sağlamasını ağ istatistikleri toplama içerir.</span><span class="sxs-lookup"><span data-stu-id="de332-112">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span> <span data-ttu-id="de332-113">Mümkün tooremotely tetikleyici paket yakalamaları olma yoluyla bu özelliği bir paket yakalama el ile ve değerli zaman kazandırır hello istenen makine üzerinde çalışan hello yük kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="de332-113">By being able tooremotely trigger packet captures, this capability eases hello burden of running a packet capture manually and on hello desired machine, which saves valuable time.</span></span>

<span data-ttu-id="de332-114">Bu makalede paket yakalama için şu anda kullanılabilir farklı yönetim görevleri hello alır.</span><span class="sxs-lookup"><span data-stu-id="de332-114">This article takes you through hello different management tasks that are currently available for packet capture.</span></span>

- [<span data-ttu-id="de332-115">**Paket yakalama Başlat**</span><span class="sxs-lookup"><span data-stu-id="de332-115">**Start a packet capture**</span></span>](#start-a-packet-capture)
- [<span data-ttu-id="de332-116">**Paket yakalama işlemini durdurun**</span><span class="sxs-lookup"><span data-stu-id="de332-116">**Stop a packet capture**</span></span>](#stop-a-packet-capture)
- [<span data-ttu-id="de332-117">**Paket yakalama Sil**</span><span class="sxs-lookup"><span data-stu-id="de332-117">**Delete a packet capture**</span></span>](#delete-a-packet-capture)
- [<span data-ttu-id="de332-118">**Paket yakalama indirin**</span><span class="sxs-lookup"><span data-stu-id="de332-118">**Download a packet capture**</span></span>](#download-a-packet-capture)

## <a name="before-you-begin"></a><span data-ttu-id="de332-119">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="de332-119">Before you begin</span></span>

<span data-ttu-id="de332-120">Bu makalede, kaynakları aşağıdaki hello sahibi olduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="de332-120">This article assumes that you have hello following resources:</span></span>

- <span data-ttu-id="de332-121">Bir örneği toocreate paket yakalama istediğiniz Ağ İzleyicisinin hello bölgede</span><span class="sxs-lookup"><span data-stu-id="de332-121">An instance of Network Watcher in hello region you want toocreate a packet capture</span></span>
- <span data-ttu-id="de332-122">Merhaba paket sahip bir sanal makine uzantısı etkin yakalayın.</span><span class="sxs-lookup"><span data-stu-id="de332-122">A virtual machine with hello packet capture extension enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de332-123">Paket yakalama gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="de332-123">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="de332-124">Bir Windows VM Hello uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Azure Ağ İzleyicisi Aracısı sanal makine uzantısı Linuxiçin](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="de332-124">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

### <a name="packet-capture-agent-extension-through-hello-portal"></a><span data-ttu-id="de332-125">Paket Yakalama aracı uzantısı hello portal üzerinden</span><span class="sxs-lookup"><span data-stu-id="de332-125">Packet Capture agent extension through hello portal</span></span>

<span data-ttu-id="de332-126">tooinstall hello paket yakalama VM Aracısı hello portal üzerinden tooyour sanal makine gidin, tıklatın **uzantıları** > **Ekle** arayın ve **için Ağ İzleyicisi Aracısı Windows**</span><span class="sxs-lookup"><span data-stu-id="de332-126">tooinstall hello packet capture VM agent through hello portal, navigate tooyour virtual machine, click **Extensions** > **Add** and search for **Network Watcher Agent for Windows**</span></span>

![Aracı görünümü][agent]

## <a name="packet-capture-overview"></a><span data-ttu-id="de332-128">Paket yakalama genel bakış</span><span class="sxs-lookup"><span data-stu-id="de332-128">Packet Capture overview</span></span>

<span data-ttu-id="de332-129">Toohello gidin [Azure portal](https://portal.azure.com) tıklatıp **ağ** > **Ağ İzleyicisi** > **paket yakalama**</span><span class="sxs-lookup"><span data-stu-id="de332-129">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **Packet Capture**</span></span>

<span data-ttu-id="de332-130">Tüm paket listesini hello durumu olsun mevcut yakalar Hello genel bakış sayfasında gösterilir.</span><span class="sxs-lookup"><span data-stu-id="de332-130">hello overview page shows a list of all packet captures that exist no matter hello state.</span></span>

> [!NOTE]
> <span data-ttu-id="de332-131">Paket yakalama bağlantı noktası 443 üzerinden bağlantı toohello depolama hesabı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="de332-131">Packet capture requires connectivity toohello storage account over port 443.</span></span>

![Paket yakalama genel bakış ekranı][1]

## <a name="start-a-packet-capture"></a><span data-ttu-id="de332-133">Paket yakalama Başlat</span><span class="sxs-lookup"><span data-stu-id="de332-133">Start a packet capture</span></span>

<span data-ttu-id="de332-134">Tıklatın **Ekle** toocreate paket yakalama.</span><span class="sxs-lookup"><span data-stu-id="de332-134">Click **Add** toocreate a packet capture.</span></span>

<span data-ttu-id="de332-135">bir paket yakalama tanımlanabilir hello özellikleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="de332-135">hello properties that can be defined on a packet capture are:</span></span>

<span data-ttu-id="de332-136">**Ana ayarları**</span><span class="sxs-lookup"><span data-stu-id="de332-136">**Main settings**</span></span>

- <span data-ttu-id="de332-137">**Abonelik** -bu değeri kullanılır hello abonelik, Ağ İzleyicisi örneği her abonelik için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="de332-137">**Subscription** - This value is hello subscription that is used, an instance of network watcher is needed in each subscription.</span></span>
- <span data-ttu-id="de332-138">**Kaynak grubu** -hello sanal makinesinin, hedef alındığını hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="de332-138">**Resource group** - hello resource group of hello virtual machine that is being targeted.</span></span>
- <span data-ttu-id="de332-139">**Hedef sanal makine** -hello paket yakalama çalıştıran hello sanal makine</span><span class="sxs-lookup"><span data-stu-id="de332-139">**Target virtual machine** - hello virtual machine that is running hello packet capture</span></span>
- <span data-ttu-id="de332-140">**Paket yakalama adı** -bu değer hello hello paket yakalama adıdır.</span><span class="sxs-lookup"><span data-stu-id="de332-140">**Packet capture name** - This value is hello name of hello packet capture.</span></span>

<span data-ttu-id="de332-141">**Yapılandırma Yakalama**</span><span class="sxs-lookup"><span data-stu-id="de332-141">**Capture configuration**</span></span>

- <span data-ttu-id="de332-142">**Depolama hesabı** -paket yakalama bir depolama hesabında kaydedilip kaydedilmeyeceğini belirler.</span><span class="sxs-lookup"><span data-stu-id="de332-142">**Storage Account** - Determines if packet capture is saved in a storage account.</span></span>
- <span data-ttu-id="de332-143">**Dosya** -paket yakalama hello sanal makinede yerel olarak kaydedilirse belirler.</span><span class="sxs-lookup"><span data-stu-id="de332-143">**File** - Determines if a packet capture is saved locally on hello virtual machine.</span></span>
- <span data-ttu-id="de332-144">**Depolama hesapları** -hello seçili depolama hesabına toosave hello paket yakalama.</span><span class="sxs-lookup"><span data-stu-id="de332-144">**Storage Accounts** - hello selected storage account toosave hello packet capture in.</span></span> <span data-ttu-id="de332-145">Varsayılan konumdur https://{storage hesap name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription kimliği} /resourcegroups/ {kaynak grubu name}/providers/microsoft.compute/virtualmachines/{virtual makine adı} / {YY} / {MM} / {gg} / {ss} packetcapture__{MM}_{SS} _ {XXX} .cap.</span><span class="sxs-lookup"><span data-stu-id="de332-145">Default location is https://{storage account name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription id}/resourcegroups/{resource group name}/providers/microsoft.compute/virtualmachines/{virtual machine name}/{YY}/{MM}/{DD}/packetcapture_{HH}_{MM}_{SS}_{XXX}.cap.</span></span> <span data-ttu-id="de332-146">(Yalnızca etkin olup **depolama** seçili)</span><span class="sxs-lookup"><span data-stu-id="de332-146">(Only enabled if **Storage** is selected)</span></span>
- <span data-ttu-id="de332-147">**Yerel dosya yolu** -bir sanal makine toosave hello paket yakalama hello yerel yol.</span><span class="sxs-lookup"><span data-stu-id="de332-147">**Local file path** - hello local path on a virtual machine toosave hello packet capture.</span></span> <span data-ttu-id="de332-148">(Yalnızca etkin olup **dosya** seçilir).</span><span class="sxs-lookup"><span data-stu-id="de332-148">(Only enabled if **File** is selected).</span></span> <span data-ttu-id="de332-149">Geçerli bir yol sağlanmalıdır</span><span class="sxs-lookup"><span data-stu-id="de332-149">A Valid path must be supplied</span></span>
- <span data-ttu-id="de332-150">**Paket başına en fazla bayt** -hello numarası yakalanan bayt gelen her paket, tüm baytlar boş bırakılırsa yakalanır.</span><span class="sxs-lookup"><span data-stu-id="de332-150">**Maximum bytes per packet** - hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span>
- <span data-ttu-id="de332-151">**Oturum başına en fazla bayt** - toplam hello değeri hello paket yakalama durakları ulaşıldıktan sonra yakalanan bayt sayısı.</span><span class="sxs-lookup"><span data-stu-id="de332-151">**Maximum bytes per session** - Total number of bytes that are captured, once hello value is reached hello packet capture stops.</span></span>
- <span data-ttu-id="de332-152">**Süre (saniye)** -hello paket yakalama toostop için zaman sınırını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="de332-152">**Time limit (seconds)** - Sets a time limit for hello packet capture toostop.</span></span> <span data-ttu-id="de332-153">Varsayılan değer 18000 saniyedir.</span><span class="sxs-lookup"><span data-stu-id="de332-153">Default is 18000 seconds.</span></span>

> [!NOTE]
> <span data-ttu-id="de332-154">Paket depolama yakalar için premium depolama hesapları şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="de332-154">Premium storage accounts are currently not supported for storing packet captures.</span></span>

<span data-ttu-id="de332-155">**(İsteğe bağlı) filtreleme**</span><span class="sxs-lookup"><span data-stu-id="de332-155">**Filtering (Optional)**</span></span>

- <span data-ttu-id="de332-156">**Protokol** -hello paket yakalama için Protokolü toofilter hello.</span><span class="sxs-lookup"><span data-stu-id="de332-156">**Protocol** - hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="de332-157">Merhaba değerleri TCP, UDP ve herhangi bir kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="de332-157">hello available values are TCP, UDP, and Any.</span></span>
- <span data-ttu-id="de332-158">**Yerel IP adresi** -hello yerel IP adresi bu filtre değeri eşleştiği hello paket yakalama toopackets bu değeri filtreler.</span><span class="sxs-lookup"><span data-stu-id="de332-158">**Local IP address** - This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>
- <span data-ttu-id="de332-159">**Yerel bağlantı noktası** -hello yerel bağlantı noktası bu filtre değeri eşleştiği hello paket yakalama toopackets bu değeri filtreler.</span><span class="sxs-lookup"><span data-stu-id="de332-159">**Local port** - This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>
- <span data-ttu-id="de332-160">**Uzak IP adresi** -hello uzak IP Bu filtre değeri eşleştiği hello paket yakalama toopackets bu değeri filtreler.</span><span class="sxs-lookup"><span data-stu-id="de332-160">**Remote IP address** - This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>
- <span data-ttu-id="de332-161">**Uzak bağlantı noktası** -hello uzak bağlantı noktası bu filtre değeri eşleştiği hello paket yakalama toopackets bu değeri filtreler.</span><span class="sxs-lookup"><span data-stu-id="de332-161">**Remote port** - This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>

> [!NOTE]
> <span data-ttu-id="de332-162">Bağlantı noktası ve IP adresi değerleri, tek bir değer, değer aralığı veya bir kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="de332-162">Port and IP address values can be a single value, range of values, or a set.</span></span> <span data-ttu-id="de332-163">(diğer bir deyişle, bağlantı noktası 80-1024 için) İstediğiniz sayıda filtreleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de332-163">(that is, 80-1024 for port) You can define as many filters as you want.</span></span>

<span data-ttu-id="de332-164">Merhaba değerleri doldurulduktan sonra tıklayın **Tamam** toocreate hello paket yakalama.</span><span class="sxs-lookup"><span data-stu-id="de332-164">Once hello values are filled out, click **OK** toocreate hello packet capture.</span></span>

![Paket yakalama oluşturma][2]

<span data-ttu-id="de332-166">Üzerinde Hello zaman sınırı ayarladıktan sonra hello paket yakalama süresi doldu, hello paket yakalama durdurur ve gözden geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="de332-166">After hello time limit set on hello packet capture has expired, hello packet capture will stop and can be reviewed.</span></span> <span data-ttu-id="de332-167">El ile de hello paket yakalamaları oturumları durdurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de332-167">You can also manually stop hello packet captures sessions.</span></span>

## <a name="delete-a-packet-capture"></a><span data-ttu-id="de332-168">Paket yakalama Sil</span><span class="sxs-lookup"><span data-stu-id="de332-168">Delete a packet capture</span></span>

<span data-ttu-id="de332-169">Merhaba pakette görünümünü yakalama, hello tıklatın **bağlam menüsü** (...) veya sağ tıklatın ve'ı tıklatın **silmek** toostop hello paket yakalama</span><span class="sxs-lookup"><span data-stu-id="de332-169">In hello packet capture view, click hello **context menu** (...) or right click, and click **delete** toostop hello packet capture</span></span>

![Paket yakalama Sil][3]

> [!NOTE]
> <span data-ttu-id="de332-171">Paket yakalama silindiğinde hello depolama hesabındaki hello dosya silinmez.</span><span class="sxs-lookup"><span data-stu-id="de332-171">Deleting a packet capture does not delete hello file in hello storage account.</span></span>

<span data-ttu-id="de332-172">Bunu Sorduğunuza toodelete hello paket yakalama istediğiniz tooconfirm tıklatın **Evet**</span><span class="sxs-lookup"><span data-stu-id="de332-172">You are asked tooconfirm you want toodelete hello packet capture, click **Yes**</span></span>

![Onaylama][4]

## <a name="stop-a-packet-capture"></a><span data-ttu-id="de332-174">Paket yakalama işlemini durdurun</span><span class="sxs-lookup"><span data-stu-id="de332-174">Stop a packet capture</span></span>

<span data-ttu-id="de332-175">Merhaba pakette görünümünü yakalama, hello tıklatın **bağlam menüsü** (...) veya sağ tıklatın ve'ı tıklatın **durdurmak** toostop hello paket yakalama</span><span class="sxs-lookup"><span data-stu-id="de332-175">In hello packet capture view, click hello **context menu** (...) or right click, and click **Stop** toostop hello packet capture</span></span>

## <a name="download-a-packet-capture"></a><span data-ttu-id="de332-176">Paket yakalama indirin</span><span class="sxs-lookup"><span data-stu-id="de332-176">Download a packet capture</span></span>

<span data-ttu-id="de332-177">Paket yakalama oturumunuz tamamladıktan sonra hello yakalama dosyasını karşıya yüklenen tooblob depolama veya tooa yerel hello VM üzerinde bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="de332-177">Once your packet capture session has completed, hello capture file is uploaded tooblob storage or tooa local file on hello VM.</span></span> <span data-ttu-id="de332-178">Merhaba paket yakalama Hello depolama konumu hello oturum oluşturma sırasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="de332-178">hello storage location of hello packet capture is defined at creation of hello session.</span></span> <span data-ttu-id="de332-179">Bu yakalama uygun aracı tooaccess kaydedilmiş tooa depolama hesabıdır burada indirilebilir Microsoft Azure Storage Gezgini dosyaları: http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="de332-179">A convenient tool tooaccess these capture files saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="de332-180">Bir depolama hesabı belirtilirse, paket yakalama dosyalarını tooa depolama hesabı konumu aşağıdaki hello kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="de332-180">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a><span data-ttu-id="de332-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="de332-181">Next steps</span></span>

<span data-ttu-id="de332-182">Nasıl sanal makine uyarılarla tooautomate paket görüntüleyerek yakalar öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="de332-182">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="de332-183">Belirli trafik içinde veya dışında VM ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="de332-183">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













