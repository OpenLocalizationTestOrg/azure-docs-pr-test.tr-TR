---
title: "Paket yakalama Azure Ağ İzleyicisi giriş | Microsoft Docs"
description: "Bu sayfa Ağ İzleyicisi paket yakalama özelliği genel bir bakış sağlar"
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
ms.openlocfilehash: 4fdd007c2cfad7b42f26ab2cacfba06d95c8dad3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-variable-packet-capture-in-azure-network-watcher"></a><span data-ttu-id="610ae-103">Azure Ağ İzleyicisi değişken paket yakalama giriş</span><span class="sxs-lookup"><span data-stu-id="610ae-103">Introduction to variable packet capture in Azure Network Watcher</span></span>

<span data-ttu-id="610ae-104">Ağ İzleyicisi değişken paket yakalama, bir sanal makine gelen ve giden trafiği izlemek için paket yakalama oturumları oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="610ae-104">Network Watcher variable packet capture allows you to create packet capture sessions to track traffic to and from a virtual machine.</span></span> <span data-ttu-id="610ae-105">Her iki ağ anormallikleri Tepkisel tanılamak için paket Yakalama yardımcı olur ve proactivity.</span><span class="sxs-lookup"><span data-stu-id="610ae-105">Packet capture helps to diagnose network anomalies both reactively and proactivity.</span></span> <span data-ttu-id="610ae-106">Diğer kullanımlar ağ yetkisiz erişim, istemci-sunucu iletişimleri ve çok daha fazlasını hata ayıklamak için bilgi sağlamasını ağ istatistikleri toplama içerir.</span><span class="sxs-lookup"><span data-stu-id="610ae-106">Other uses include gathering network statistics, gaining information on network intrusions, to debug client-server communications and much more.</span></span>

<span data-ttu-id="610ae-107">Paket yakalama Ağ İzleyicisi uzaktan başlatılan bir sanal makine uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="610ae-107">Packet capture is a virtual machine extension that is remotely started through Network Watcher.</span></span> <span data-ttu-id="610ae-108">Bu özellik, bir paket yakalama değerli zaman kazandırır istenen sanal makinesinin üzerinde el ile çalıştırmayı yükünü kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="610ae-108">This capability eases the burden of running a packet capture manually on the desired virtual machine, which saves valuable time.</span></span> <span data-ttu-id="610ae-109">Paket yakalama portal, PowerShell'i, CLI veya REST API tetiklenebilir.</span><span class="sxs-lookup"><span data-stu-id="610ae-109">Packet capture can be triggered through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="610ae-110">Paket yakalama nasıl tetiklenebilir bir sanal makine uyarılara örnektir.</span><span class="sxs-lookup"><span data-stu-id="610ae-110">One example of how packet capture can be triggered is with Virtual Machine alerts.</span></span> <span data-ttu-id="610ae-111">Filtreler sağlamak, izlemek istediğiniz trafiği yakalamak yakalama oturumu için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="610ae-111">Filters are provided for the capture session to ensure you capture traffic you want to monitor.</span></span> <span data-ttu-id="610ae-112">Filtreler, 5-tanımlama grubu üzerinde (protokolü, yerel IP adresi, uzak IP adresi, yerel bağlantı noktası ve uzak bağlantı noktası) dayalı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="610ae-112">Filters are based on 5-tuple (protocol, local IP address, remote IP address, local port, and remote port) information.</span></span> <span data-ttu-id="610ae-113">Yakalanan veriler, yerel disk veya bir depolama blob depolanır.</span><span class="sxs-lookup"><span data-stu-id="610ae-113">The captured data is stored in the local disk or a storage blob.</span></span> <span data-ttu-id="610ae-114">Her Abonelikteki bölge başına 10 paket yakalama oturumu sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="610ae-114">There is a limit of 10 packet capture sessions per region per subscription.</span></span> <span data-ttu-id="610ae-115">Bu sınır yalnızca oturumlar için geçerlidir ve kaydedilmiş paket yakalama dosyalarını VM yerel olarak veya bir depolama hesabı için geçerli değildir.</span><span class="sxs-lookup"><span data-stu-id="610ae-115">This limit applies only to the sessions and does not apply to the saved packet capture files either locally on the VM or in a storage account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="610ae-116">Paket yakalama gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="610ae-116">Packet capture requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="610ae-117">Bir Windows VM uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Linux için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="610ae-117">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

<span data-ttu-id="610ae-118">Yalnızca istediğiniz bilgileri yakalamak bilgi azaltmak için aşağıdaki seçenekleri paket yakalama oturum açmak için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="610ae-118">To reduce the information you capture to only the information you want, the following options are available for a packet capture session:</span></span>

<span data-ttu-id="610ae-119">**Yapılandırma Yakalama**</span><span class="sxs-lookup"><span data-stu-id="610ae-119">**Capture configuration**</span></span>

|<span data-ttu-id="610ae-120">Özellik</span><span class="sxs-lookup"><span data-stu-id="610ae-120">Property</span></span>|<span data-ttu-id="610ae-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="610ae-121">Description</span></span>|
|---|---|
|<span data-ttu-id="610ae-122">**Paket (bayt) başına en fazla bayt sayısı**</span><span class="sxs-lookup"><span data-stu-id="610ae-122">**Maximum bytes per packet (bytes)**</span></span> | <span data-ttu-id="610ae-123">Sayı yakalanan bayt gelen her paket, tüm baytlar boş bırakılırsa yakalanır.</span><span class="sxs-lookup"><span data-stu-id="610ae-123">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="610ae-124">Sayı yakalanan bayt gelen her paket, tüm baytlar boş bırakılırsa yakalanır.</span><span class="sxs-lookup"><span data-stu-id="610ae-124">The number of bytes from each packet that are captured, all bytes are captured if left blank.</span></span> <span data-ttu-id="610ae-125">Yalnızca IPv4 üstbilgisi – gerekirse burada 34 belirtin</span><span class="sxs-lookup"><span data-stu-id="610ae-125">If you need only the IPv4 header – indicate 34 here</span></span> |
|<span data-ttu-id="610ae-126">**Oturum (bayt) başına en fazla bayt sayısı**</span><span class="sxs-lookup"><span data-stu-id="610ae-126">**Maximum bytes per session (bytes)**</span></span> | <span data-ttu-id="610ae-127">Oturum sona erdirilir değere ulaşıldığında, bayt toplam sayısı yakalanır.</span><span class="sxs-lookup"><span data-stu-id="610ae-127">Total number of bytes in that are captured, once the value is reached the session ends.</span></span>|
|<span data-ttu-id="610ae-128">**Süre (saniye)**</span><span class="sxs-lookup"><span data-stu-id="610ae-128">**Time limit (seconds)**</span></span> | <span data-ttu-id="610ae-129">Paket bir zaman kısıtlama kümelerini oturum yakalayın.</span><span class="sxs-lookup"><span data-stu-id="610ae-129">Sets a time constraint on the packet capture session.</span></span> <span data-ttu-id="610ae-130">Varsayılan değer 18000 saniye veya 5 saat olur.</span><span class="sxs-lookup"><span data-stu-id="610ae-130">The default value is 18000 seconds or 5 hours.</span></span>|

<span data-ttu-id="610ae-131">**(İsteğe bağlı) filtreleme**</span><span class="sxs-lookup"><span data-stu-id="610ae-131">**Filtering (optional)**</span></span>

|<span data-ttu-id="610ae-132">Özellik</span><span class="sxs-lookup"><span data-stu-id="610ae-132">Property</span></span>|<span data-ttu-id="610ae-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="610ae-133">Description</span></span>|
|---|---|
|<span data-ttu-id="610ae-134">**Protokol**</span><span class="sxs-lookup"><span data-stu-id="610ae-134">**Protocol**</span></span> | <span data-ttu-id="610ae-135">Paket yakalama için filtre uygulamak için protokol.</span><span class="sxs-lookup"><span data-stu-id="610ae-135">The protocol to filter for the packet capture.</span></span> <span data-ttu-id="610ae-136">Kullanılabilir TCP, UDP ve tüm değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="610ae-136">The available values are TCP, UDP, and All.</span></span>|
|<span data-ttu-id="610ae-137">**Yerel IP adresi**</span><span class="sxs-lookup"><span data-stu-id="610ae-137">**Local IP address**</span></span> | <span data-ttu-id="610ae-138">Bu değer, yerel IP adresi bu filtre değeri eşleştiği paket için paket yakalama filtreler.</span><span class="sxs-lookup"><span data-stu-id="610ae-138">This value filters the packet capture to packets where the local IP address matches this filter value.</span></span>|
|<span data-ttu-id="610ae-139">**Yerel bağlantı noktası**</span><span class="sxs-lookup"><span data-stu-id="610ae-139">**Local port**</span></span> | <span data-ttu-id="610ae-140">Bu değer, yerel bağlantı noktası bu filtre değeri eşleştiği paket için paket yakalama filtreler.</span><span class="sxs-lookup"><span data-stu-id="610ae-140">This value filters the packet capture to packets where the local port matches this filter value.</span></span>|
|<span data-ttu-id="610ae-141">**Uzak IP adresi**</span><span class="sxs-lookup"><span data-stu-id="610ae-141">**Remote IP address**</span></span> | <span data-ttu-id="610ae-142">Bu değer, uzak IP Bu filtre değeri eşleştiği paket için paket yakalama filtreler.</span><span class="sxs-lookup"><span data-stu-id="610ae-142">This value filters the packet capture to packets where the remote IP matches this filter value.</span></span>|
|<span data-ttu-id="610ae-143">**Uzak bağlantı noktası**</span><span class="sxs-lookup"><span data-stu-id="610ae-143">**Remote port**</span></span> | <span data-ttu-id="610ae-144">Bu değer, uzak bağlantı noktası bu filtre değeri eşleştiği paket için paket yakalama filtreler.</span><span class="sxs-lookup"><span data-stu-id="610ae-144">This value filters the packet capture to packets where the remote port matches this filter value.</span></span>|

### <a name="next-steps"></a><span data-ttu-id="610ae-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="610ae-145">Next steps</span></span>

<span data-ttu-id="610ae-146">Paket yakalama Portalı aracılığıyla ziyaret ederek nasıl yönetebileceğiniz öğrenin [paket yakalama Azure portalında yönetmek](network-watcher-packet-capture-manage-portal.md) veya şu adresi ziyaret ederek PowerShell ile [PowerShell ile paket yakalama yönetmek](network-watcher-packet-capture-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="610ae-146">Learn how you can manage packet captures through the portal by visiting [Manage packet capture in the Azure portal](network-watcher-packet-capture-manage-portal.md) or with PowerShell by visiting [Manage Packet Capture with PowerShell](network-watcher-packet-capture-manage-powershell.md).</span></span>

<span data-ttu-id="610ae-147">Sanal makine uyarılar ziyaret ederek temelinde öngörülü paket yakalamaları oluşturmayı öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="610ae-147">Learn how to create proactive packet captures based on virtual machine alerts by visiting [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













