---
title: "Azure sanal ağ geçidi ve bağlantıları - PowerShell sorunlarını giderme | Microsoft Docs"
description: "Bu sayfa, Azure Ağ İzleyicisi'ni kullanma açıklanmaktadır PowerShell cmdlet'ini sorun giderme"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: e135e719d8f267f6a189d0f8a903a49980a5a035
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="b7b82-103">Sanal ağ geçidi ve Azure Ağ İzleyicisi PowerShell kullanarak bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="b7b82-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b7b82-104">Portal</span><span class="sxs-lookup"><span data-stu-id="b7b82-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="b7b82-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7b82-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="b7b82-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b7b82-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="b7b82-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b7b82-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="b7b82-108">REST API</span><span class="sxs-lookup"><span data-stu-id="b7b82-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="b7b82-109">Ağ kaynaklarınızı Azure anlamak için ilgili olarak Ağ İzleyicisi çok sayıda özellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7b82-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="b7b82-110">Bu özelliklerin biri kaynak sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="b7b82-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="b7b82-111">Kaynak sorun giderme portalı, PowerShell, CLI veya REST API çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="b7b82-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="b7b82-112">Çağrıldığında, Ağ İzleyicisi bir sanal ağ geçidi veya bağlantı durumunu inceler ve bulduklarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="b7b82-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b7b82-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b7b82-113">Before you begin</span></span>

<span data-ttu-id="b7b82-114">Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) bir Ağ İzleyicisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="b7b82-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="b7b82-115">Desteklenen ağ geçidi türleri ziyaret listesi [desteklenen ağ geçidi türleri](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="b7b82-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="b7b82-116">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b7b82-116">Overview</span></span>

<span data-ttu-id="b7b82-117">Kaynak sorunlarını giderme özelliği sağlar sanal ağ geçitleri ve bağlantılarla ortaya çıkan sorunları giderme.</span><span class="sxs-lookup"><span data-stu-id="b7b82-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="b7b82-118">Kaynak sorun giderme için bir istek yapıldığında, günlükleri yükleniyor sorgulanan ve sahip denetlenir.</span><span class="sxs-lookup"><span data-stu-id="b7b82-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="b7b82-119">İnceleme tamamlandığında, sonuçları döndürülür.</span><span class="sxs-lookup"><span data-stu-id="b7b82-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="b7b82-120">Sorun giderme istekleri uzun süredir çalışıp kaynak, hangi birden çok dakika sürebilir bir sonuç ister.</span><span class="sxs-lookup"><span data-stu-id="b7b82-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="b7b82-121">Sorun giderme gelen günlükleri, belirtilen bir depolama hesabı üzerinde bir kapsayıcıda depolanır.</span><span class="sxs-lookup"><span data-stu-id="b7b82-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="troubleshoot-a-gateway-or-connection"></a><span data-ttu-id="b7b82-122">Bir ağ geçidi veya bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="b7b82-122">Troubleshoot a gateway or connection</span></span>

1. <span data-ttu-id="b7b82-123">Gidin [Azure portal](https://portal.azure.com) tıklatıp **ağ** > **Ağ İzleyicisi** > **VPN tanılama**</span><span class="sxs-lookup"><span data-stu-id="b7b82-123">Navigate to the [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **VPN Diagnostics**</span></span>
2. <span data-ttu-id="b7b82-124">Seçin bir **abonelik**, **kaynak grubu**, ve **konumu**.</span><span class="sxs-lookup"><span data-stu-id="b7b82-124">Select a **Subscription**, **Resource Group**, and **Location**.</span></span>
3. <span data-ttu-id="b7b82-125">Kaynak sorun giderme kaynak sistem durumu hakkındaki verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="b7b82-125">Resource troubleshooting returns data about the health of the resource.</span></span> <span data-ttu-id="b7b82-126">Aynı zamanda ilgili günlükleri gözden geçirilmesi için bir depolama hesabı kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b7b82-126">It also saves relevant logs to a storage account to be reviewed.</span></span> <span data-ttu-id="b7b82-127">Tıklatın **depolama hesabı** bir depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="b7b82-127">Click **Storage Account** to select a storage account.</span></span>
4. <span data-ttu-id="b7b82-128">Üzerinde **depolama hesapları** dikey penceresinde, mevcut bir depolama hesabını seçin veya **+ depolama hesabı** yeni bir tane oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="b7b82-128">On the **Storage accounts** blade, select an existing storage account or click **+ Storage account** to create a new one.</span></span>
5. <span data-ttu-id="b7b82-129">Üzerinde **kapsayıcıları** dikey penceresinde, var olan bir kapsayıcı seçin veya tıklatın **+ kapsayıcı** yeni bir kapsayıcı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="b7b82-129">On the **Containers** blade, choose an existing container or click **+ Container** to create a new container.</span></span> <span data-ttu-id="b7b82-130">Tıklatın tamamlandığında **seçin**</span><span class="sxs-lookup"><span data-stu-id="b7b82-130">When complete click **Select**</span></span>
6. <span data-ttu-id="b7b82-131">Sorun giderme tıklatıp geçidi ve bağlantıyla kaynakları seçin **sorun gidermeyi Başlat**</span><span class="sxs-lookup"><span data-stu-id="b7b82-131">Select the Gateway and Connection resources to troubleshoot and click **Start Troubleshooting**</span></span>

<span data-ttu-id="b7b82-132">Birden fazla kaynak seçtiyseniz, sorun giderme ağ geçidi kaynaklarını aynı anda çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="b7b82-132">If multiple resources are selected, troubleshooting is run concurrently on gateway resources.</span></span> <span data-ttu-id="b7b82-133">Bir bağlantı üzerinden çalıştırılamaz ve aynı zamanda ağ geçidi ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="b7b82-133">It can not run on a connection and it's associated gateway at the same time.</span></span> <span data-ttu-id="b7b82-134">Ağ geçitlerinde sorun giderme için önerilen ilk gibi bağlantı sorunlarını giderme daha uzun bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="b7b82-134">It is recommended to troubleshoot gateways first as connection troubleshooting is a longer process.</span></span> <span data-ttu-id="b7b82-135">VPN tanılama bir kaynakta çalışırken **sorun giderme durum** sütununu durumunu göster **çalışan**</span><span class="sxs-lookup"><span data-stu-id="b7b82-135">While VPN Diagnostics is running on a resource the **TROUBLESHOOTING STATUS** column will show a status of **Running**</span></span>

<span data-ttu-id="b7b82-136">Tamamlandığında, Durum sütununda değişikliklerini **sağlıklı** veya **sağlıksız**.</span><span class="sxs-lookup"><span data-stu-id="b7b82-136">When complete, the status column changes to **Healthy** or **Unhealthy**.</span></span>

![eksiksiz sorun giderme][2]

## <a name="understanding-the-results"></a><span data-ttu-id="b7b82-138">Sonuçları anlama</span><span class="sxs-lookup"><span data-stu-id="b7b82-138">Understanding the results</span></span>

<span data-ttu-id="b7b82-139">İçinde **ayrıntıları** penceresi bölümünü **durum** sekmesi gösterir son sorun giderme durumunu çalışma seçili kaynağı.</span><span class="sxs-lookup"><span data-stu-id="b7b82-139">In the **Details** section of the window, the **Status** tab shows the status of the last troubleshooting run on the selected resource.</span></span> <span data-ttu-id="b7b82-140">En son Tanılama sonuçları gösterilen xx dakika sonra son çalıştırma olur.</span><span class="sxs-lookup"><span data-stu-id="b7b82-140">Results of the latest diagnostic are shown xx minutes after the last run.</span></span>

|<span data-ttu-id="b7b82-141">Özellik</span><span class="sxs-lookup"><span data-stu-id="b7b82-141">Property</span></span>  |<span data-ttu-id="b7b82-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b7b82-142">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="b7b82-143">Kaynak</span><span class="sxs-lookup"><span data-stu-id="b7b82-143">Resource</span></span>     | <span data-ttu-id="b7b82-144">Kaynak bağlantı.</span><span class="sxs-lookup"><span data-stu-id="b7b82-144">A link to the resource.</span></span>        |
|<span data-ttu-id="b7b82-145">Depolama alanı yolu</span><span class="sxs-lookup"><span data-stu-id="b7b82-145">Storage path</span></span>     |  <span data-ttu-id="b7b82-146">Depolama hesabı ve kapsayıcı günlükleri (herhangi bir çalışma sırasında oluşturulamadığı varsa) içeren yolu.</span><span class="sxs-lookup"><span data-stu-id="b7b82-146">Path to the storage account and container that contain the logs (if any were produced during the run).</span></span> <span data-ttu-id="b7b82-147">Portal çıktıktan sonra bu ayarı kalmaz.</span><span class="sxs-lookup"><span data-stu-id="b7b82-147">This setting does not persist after you leave the portal.</span></span>        |
|<span data-ttu-id="b7b82-148">Özet</span><span class="sxs-lookup"><span data-stu-id="b7b82-148">Summary</span></span>     | <span data-ttu-id="b7b82-149">Kaynak durumu özeti.</span><span class="sxs-lookup"><span data-stu-id="b7b82-149">Summary of the resource health.</span></span>        |
|<span data-ttu-id="b7b82-150">Ayrıntısı</span><span class="sxs-lookup"><span data-stu-id="b7b82-150">Detail</span></span>     | <span data-ttu-id="b7b82-151">Kaynak durumu hakkında ayrıntılı bilgiler.</span><span class="sxs-lookup"><span data-stu-id="b7b82-151">Detailed information on the resource health.</span></span>        |
|<span data-ttu-id="b7b82-152">Son çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b7b82-152">Last run</span></span>     | <span data-ttu-id="b7b82-153">Son sorun giderme zaman saat kaldı.</span><span class="sxs-lookup"><span data-stu-id="b7b82-153">The time the last time troubleshooting was ran.</span></span>        |


<span data-ttu-id="b7b82-154">**Eylem** sekmesi, sorunun nasıl çözümleneceği hakkında genel kılavuzluk sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7b82-154">The **Action** tab provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="b7b82-155">Bir eylem için sorunu gerçekleştirilebiliyorsa bir bağlantı ile ek yönergeler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="b7b82-155">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="b7b82-156">Durumda hiçbir ek yönergeler bulunduğu bir destek servis talebi açmaya url yanıt sağlar.</span><span class="sxs-lookup"><span data-stu-id="b7b82-156">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="b7b82-157">Yanıt ve dahil edilen nedir özellikleri hakkında daha fazla bilgi için ziyaret [Ağ İzleyicisi sorun giderme genel bakış](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b7b82-157">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>


## <a name="next-steps"></a><span data-ttu-id="b7b82-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b7b82-158">Next steps</span></span>

<span data-ttu-id="b7b82-159">Bu Dur VPN bağlantısı ayarları değiştirilmiş olup [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) söz konusu olabilecek ağ güvenlik grubu ve güvenlik kuralları izlemek için.</span><span class="sxs-lookup"><span data-stu-id="b7b82-159">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
