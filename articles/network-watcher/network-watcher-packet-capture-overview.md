---
title: "Azure Ağ İzleyicisi aaaIntroduction tooPacket yakalama | Microsoft Docs"
description: "Bu sayfa hello Ağ İzleyicisi paket yakalama özelliği genel bir bakış sağlar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="772fe-103">Azure Ağ İzleyicisi giriş toovariable paket yakalama</span><span class="sxs-lookup"><span data-stu-id="772fe-103">Introduction toovariable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="772fe-104">Ağ İzleyicisi değişken paket yakalama toocreate paket yakalama oturumları tootrack trafiği tooand bir sanal makineden sağlar.</span><span class="sxs-lookup"><span data-stu-id="772fe-104">Network Watcher variable packet capture allows you toocreate packet capture sessions tootrack traffic tooand from a virtual machine.</span></span> <span data-ttu-id="772fe-105">Paket yakalama toodiagnose ağ anormallikleri hem Tepkisel yardımcı olur ve proactivity.</span><span class="sxs-lookup"><span data-stu-id="772fe-105">Packet capture helps toodiagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="772fe-106">Diğer kullanımlar bilgi ağ yetkisiz erişim, toodebug istemci-sunucu iletişimleri ve daha fazlasını sağlamasını ağ istatistikleri toplama içerir.</span><span class="sxs-lookup"><span data-stu-id="772fe-106">Other uses include gathering network statistics, gaining information on network intrusions, toodebug client-server communications and much more.</span></span>

<span data-ttu-id="772fe-107">Paket yakalama Ağ İzleyicisi uzaktan başlatılan bir sanal makine uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="772fe-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="772fe-108">Bu özellik, bir paket yakalama istenen hello sanal değerli zaman kazandırır makineye el ile çalışan hello yük kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="772fe-108">This capability eases hello burden of running a packet capture manually on hello desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="772fe-109">Paket yakalama hello portal, PowerShell'i, CLI veya REST API tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="772fe-109">Packet capture can be triggered through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="772fe-110">Paket yakalama nasıl tetiklenebilir bir sanal makine uyarılara örnektir.</span><span class="sxs-lookup"><span data-stu-id="772fe-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="772fe-111">Filtreler toomonitor istediğiniz trafiği yakalamak için Hello yakalama oturum tooensure sağlanır.</span><span class="sxs-lookup"><span data-stu-id="772fe-111">Filters are provided for hello capture session tooensure you capture traffic you want toomonitor.</span></span> <span data-ttu-id="772fe-112">Filtreler, 5-tanımlama grubu üzerinde (protokolü, yerel IP adresi, uzak IP adresi, yerel bağlantı noktası ve uzak bağlantı noktası) dayalı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="772fe-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="772fe-113">Merhaba Yakalanan veriler hello yerel disk veya bir depolama blob depolanır.</span><span class="sxs-lookup"><span data-stu-id="772fe-113">hello captured data is stored in hello local disk or a storage blob.</span></span> <span data-ttu-id="772fe-114">Her Abonelikteki bölge başına 10 paket yakalama oturumu sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="772fe-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="772fe-115">Bu sınır yalnızca toohello oturumları uygular ve paket yakalama dosyalarını hello VM yerel olarak veya bir depolama hesabı kaydedilmiş toohello geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="772fe-115">This limit applies only toohello sessions and does not apply toohello saved packet capture files either locally on hello VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="772fe-116">Paket yakalama gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="772fe-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="772fe-117">Bir Windows VM Hello uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Azure Ağ İzleyicisi Aracısı sanal makine uzantısı Linuxiçin](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="772fe-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="772fe-118">tooreduce hello bilgileri tooonly hello bilgileri yakalamak, hello paket yakalama oturum açmak için kullanılabilen seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="772fe-118">tooreduce hello information you capture tooonly hello information you want, hello following options are available for a packet capture session:</span></span>

<span data-ttu-id="772fe-119">**Yapılandırma Yakalama**</span><span class="sxs-lookup"><span data-stu-id="772fe-119">**Capture configuration**</span></span>

|<span data-ttu-id="772fe-120">Özellik</span><span class="sxs-lookup"><span data-stu-id="772fe-120">Property</span></span>|<span data-ttu-id="772fe-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="772fe-121">Description</span></span>|
|---|---|
|<span data-ttu-id="772fe-122">**Paket (bayt) başına en fazla bayt sayısı**</span><span class="sxs-lookup"><span data-stu-id="772fe-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="772fe-123">Merhaba numarası yakalanan bayt gelen her paket, tüm baytlar boş bırakılırsa yakalanır.</span><span class="sxs-lookup"><span data-stu-id="772fe-123">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="772fe-124">Merhaba numarası yakalanan bayt gelen her paket, tüm baytlar boş bırakılırsa yakalanır.</span><span class="sxs-lookup"><span data-stu-id="772fe-124">hello number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="772fe-125">Yalnızca hello IPv4 üst bilgisi – gerekirse burada 34 belirtin</span><span class="sxs-lookup"><span data-stu-id="772fe-125">If you need only hello IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="772fe-126">**Oturum (bayt) başına en fazla bayt sayısı**</span><span class="sxs-lookup"><span data-stu-id="772fe-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="772fe-127">Merhaba değeri hello oturumu sonra erene ulaşıldığında, bayt toplam sayısı yakalanır.</span><span class="sxs-lookup"><span data-stu-id="772fe-127">Total number of bytes in that are captured, once hello value is reached hello session ends.</span></span>|
|<span data-ttu-id="772fe-128">**Süre (saniye)**</span><span class="sxs-lookup"><span data-stu-id="772fe-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="772fe-129">Hello paket zaman kısıtlama kümelerini oturum yakalayın.</span><span class="sxs-lookup"><span data-stu-id="772fe-129">Sets a time constraint on hello packet capture session.</span></span> <span data-ttu-id="772fe-130">Merhaba varsayılan 18000 saniye veya 5 saat değeridir.</span><span class="sxs-lookup"><span data-stu-id="772fe-130">hello default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="772fe-131">**(İsteğe bağlı) filtreleme**</span><span class="sxs-lookup"><span data-stu-id="772fe-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="772fe-132">Özellik</span><span class="sxs-lookup"><span data-stu-id="772fe-132">Property</span></span>|<span data-ttu-id="772fe-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="772fe-133">Description</span></span>|
|---|---|
|<span data-ttu-id="772fe-134">**Protokol**</span><span class="sxs-lookup"><span data-stu-id="772fe-134">**Protocol**</span></span> | <span data-ttu-id="772fe-135">Merhaba Protokolü toofilter hello paket için yakalayın.</span><span class="sxs-lookup"><span data-stu-id="772fe-135">hello protocol toofilter for hello packet capture.</span></span> <span data-ttu-id="772fe-136">Merhaba değerleri TCP, UDP ve tüm kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="772fe-136">hello available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="772fe-137">**Yerel IP adresi**</span><span class="sxs-lookup"><span data-stu-id="772fe-137">**Local IP address**</span></span> | <span data-ttu-id="772fe-138">Bu değer, hello yerel IP adresi bu filtre değeri eşleştiği hello paket yakalama toopackets filtreler.</span><span class="sxs-lookup"><span data-stu-id="772fe-138">This value filters hello packet capture toopackets where hello local IP address matches this filter value.</span></span>|
|<span data-ttu-id="772fe-139">**Yerel bağlantı noktası**</span><span class="sxs-lookup"><span data-stu-id="772fe-139">**Local port**</span></span> | <span data-ttu-id="772fe-140">Bu değer filtreleri hello paket hello yerel bağlantı noktası bu filtre değeri eşleştiği toopackets yakalayın.</span><span class="sxs-lookup"><span data-stu-id="772fe-140">This value filters hello packet capture toopackets where hello local port matches this filter value.</span></span>|
|<span data-ttu-id="772fe-141">**Uzak IP adresi**</span><span class="sxs-lookup"><span data-stu-id="772fe-141">**Remote IP address**</span></span> | <span data-ttu-id="772fe-142">Bu değer filtreleri hello paket hello uzak IP Bu filtre değeri eşleştiği toopackets yakalayın.</span><span class="sxs-lookup"><span data-stu-id="772fe-142">This value filters hello packet capture toopackets where hello remote IP matches this filter value.</span></span>|
|<span data-ttu-id="772fe-143">**Uzak bağlantı noktası**</span><span class="sxs-lookup"><span data-stu-id="772fe-143">**Remote port**</span></span> | <span data-ttu-id="772fe-144">Bu değer filtreleri hello paket hello uzak bağlantı noktası bu filtre değeri eşleştiği toopackets yakalayın.</span><span class="sxs-lookup"><span data-stu-id="772fe-144">This value filters hello packet capture toopackets where hello remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="772fe-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="772fe-145">Next steps</span></span>

<span data-ttu-id="772fe-146">Paket yakalama hello Portalı aracılığıyla ziyaret ederek nasıl yönetebileceğiniz öğrenin [paket yakalama hello Azure portalı Yönet](network-watcher-packet-capture-manage-portal.md) veya şu adresi ziyaret ederek PowerShell ile [PowerShell ile paket yakalama yönetmek](network-watcher-packet-capture-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="772fe-146">Learn how you can manage packet captures through hello portal by visiting [Manage packet capture in hello Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="772fe-147">Sanal makine uyarılar ziyaret ederek temelinde nasıl toocreate öngörülü paket yakalar öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="772fe-147">Learn how toocreate proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













