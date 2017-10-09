---
title: "aaaTroubleshoot Azure sanal ağ geçidi ve bağlantıları - PowerShell | Microsoft Docs"
description: "Bu sayfayı toouse hello Azure Ağ İzleyicisi PowerShell cmdlet'ini nasıl sorun giderme açıklar"
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
ms.openlocfilehash: bd568d34091209390c57d22475559bdb99ad2c59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="edcd8-103">Sanal ağ geçidi ve Azure Ağ İzleyicisi PowerShell kullanarak bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="edcd8-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="edcd8-104">Portal</span><span class="sxs-lookup"><span data-stu-id="edcd8-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="edcd8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="edcd8-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="edcd8-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="edcd8-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="edcd8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="edcd8-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="edcd8-108">REST API</span><span class="sxs-lookup"><span data-stu-id="edcd8-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="edcd8-109">Ağ kaynaklarınızı Azure toounderstanding ilgili olarak Ağ İzleyicisi çok sayıda özellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="edcd8-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="edcd8-110">Bu özelliklerin biri kaynak sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="edcd8-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="edcd8-111">Kaynak sorun giderme hello portal, PowerShell'i, CLI veya REST API çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="edcd8-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="edcd8-112">Çağrıldığında, Ağ İzleyicisi Merhaba bir sanal ağ geçidi veya bağlantı durumunu inceler ve bulduklarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="edcd8-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="edcd8-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="edcd8-113">Before you begin</span></span>

<span data-ttu-id="edcd8-114">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="edcd8-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="edcd8-115">Desteklenen ağ geçidi türleri ziyaret listesi [desteklenen ağ geçidi türleri](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="edcd8-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="edcd8-116">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="edcd8-116">Overview</span></span>

<span data-ttu-id="edcd8-117">Kaynak sorun giderme hello yeteneği sağlar sanal ağ geçitleri ve bağlantılarla ortaya çıkan sorunları giderme.</span><span class="sxs-lookup"><span data-stu-id="edcd8-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="edcd8-118">Bir istek tooresource sorun giderme yapıldığında günlükleri yükleniyor sorgulanan ve sahip denetlenir.</span><span class="sxs-lookup"><span data-stu-id="edcd8-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="edcd8-119">İnceleme tamamlandığında hello sonuçlar döndürülür.</span><span class="sxs-lookup"><span data-stu-id="edcd8-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="edcd8-120">Hangi birden çok dakika tooreturn bir sonuç ele geçirebilir sorun giderme istekleri uzun süredir çalışıp kaynak ister.</span><span class="sxs-lookup"><span data-stu-id="edcd8-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="edcd8-121">sorun giderme gelen hello günlükleri, belirtilen bir depolama hesabı üzerinde bir kapsayıcıda depolanır.</span><span class="sxs-lookup"><span data-stu-id="edcd8-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="troubleshoot-a-gateway-or-connection"></a><span data-ttu-id="edcd8-122">Bir ağ geçidi veya bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="edcd8-122">Troubleshoot a gateway or connection</span></span>

1. <span data-ttu-id="edcd8-123">Toohello gidin [Azure portal](https://portal.azure.com) tıklatıp **ağ** > **Ağ İzleyicisi** > **VPN tanılama**</span><span class="sxs-lookup"><span data-stu-id="edcd8-123">Navigate toohello [Azure portal](https://portal.azure.com) and click **Networking** > **Network Watcher** > **VPN Diagnostics**</span></span>
2. <span data-ttu-id="edcd8-124">Seçin bir **abonelik**, **kaynak grubu**, ve **konumu**.</span><span class="sxs-lookup"><span data-stu-id="edcd8-124">Select a **Subscription**, **Resource Group**, and **Location**.</span></span>
3. <span data-ttu-id="edcd8-125">Kaynak sorun giderme hello kaynak hello durumunu ilgili verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="edcd8-125">Resource troubleshooting returns data about hello health of hello resource.</span></span> <span data-ttu-id="edcd8-126">Ayrıca, ilgili günlükleri tooa depolama hesabı toobe gözden kaydeder.</span><span class="sxs-lookup"><span data-stu-id="edcd8-126">It also saves relevant logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="edcd8-127">Tıklatın **depolama hesabı** tooselect bir depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="edcd8-127">Click **Storage Account** tooselect a storage account.</span></span>
4. <span data-ttu-id="edcd8-128">Merhaba üzerinde **depolama hesapları** dikey penceresinde, mevcut bir depolama hesabını seçin veya **+ depolama hesabı** toocreate yeni bir tane.</span><span class="sxs-lookup"><span data-stu-id="edcd8-128">On hello **Storage accounts** blade, select an existing storage account or click **+ Storage account** toocreate a new one.</span></span>
5. <span data-ttu-id="edcd8-129">Merhaba üzerinde **kapsayıcıları** dikey penceresinde, var olan bir kapsayıcı seçin veya tıklatın **+ kapsayıcı** toocreate yeni bir kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="edcd8-129">On hello **Containers** blade, choose an existing container or click **+ Container** toocreate a new container.</span></span> <span data-ttu-id="edcd8-130">Tıklatın tamamlandığında **seçin**</span><span class="sxs-lookup"><span data-stu-id="edcd8-130">When complete click **Select**</span></span>
6. <span data-ttu-id="edcd8-131">Hello geçidi ve bağlantıyla kaynakları tootroubleshoot tıklatıp **sorun gidermeyi Başlat**</span><span class="sxs-lookup"><span data-stu-id="edcd8-131">Select hello Gateway and Connection resources tootroubleshoot and click **Start Troubleshooting**</span></span>

<span data-ttu-id="edcd8-132">Birden fazla kaynak seçtiyseniz, sorun giderme ağ geçidi kaynaklarını aynı anda çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="edcd8-132">If multiple resources are selected, troubleshooting is run concurrently on gateway resources.</span></span> <span data-ttu-id="edcd8-133">Bir bağlantıda çalıştırılamaz ve hello konumundaki ağ geçidine ilişkilendirilmiş aynı anda.</span><span class="sxs-lookup"><span data-stu-id="edcd8-133">It can not run on a connection and it's associated gateway at hello same time.</span></span> <span data-ttu-id="edcd8-134">Tootroubleshoot ağ geçitleri önerilen ilk gibi bağlantı sorunlarını giderme daha uzun bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="edcd8-134">It is recommended tootroubleshoot gateways first as connection troubleshooting is a longer process.</span></span> <span data-ttu-id="edcd8-135">VPN tanılama kaynak hello üzerinde çalışırken **sorun giderme durum** sütununu durumunu göster **çalışan**</span><span class="sxs-lookup"><span data-stu-id="edcd8-135">While VPN Diagnostics is running on a resource hello **TROUBLESHOOTING STATUS** column will show a status of **Running**</span></span>

<span data-ttu-id="edcd8-136">Tamamlandığında, durum sütun değişiklikleri çok hello**sağlıklı** veya **sağlıksız**.</span><span class="sxs-lookup"><span data-stu-id="edcd8-136">When complete, hello status column changes too**Healthy** or **Unhealthy**.</span></span>

![eksiksiz sorun giderme][2]

## <a name="understanding-hello-results"></a><span data-ttu-id="edcd8-138">Merhaba sonuçlarını anlama</span><span class="sxs-lookup"><span data-stu-id="edcd8-138">Understanding hello results</span></span>

<span data-ttu-id="edcd8-139">Merhaba, **ayrıntıları** bölüm hello pencerenin hello **durum** sekmesi gösterir hello son sorun giderme hello durumu çalışma seçili hello kaynakta.</span><span class="sxs-lookup"><span data-stu-id="edcd8-139">In hello **Details** section of hello window, hello **Status** tab shows hello status of hello last troubleshooting run on hello selected resource.</span></span> <span data-ttu-id="edcd8-140">Merhaba son Tanılama sonuçları gösterilen xx dakika sonra son çalıştırma hello olur.</span><span class="sxs-lookup"><span data-stu-id="edcd8-140">Results of hello latest diagnostic are shown xx minutes after hello last run.</span></span>

|<span data-ttu-id="edcd8-141">Özellik</span><span class="sxs-lookup"><span data-stu-id="edcd8-141">Property</span></span>  |<span data-ttu-id="edcd8-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="edcd8-142">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="edcd8-143">Kaynak</span><span class="sxs-lookup"><span data-stu-id="edcd8-143">Resource</span></span>     | <span data-ttu-id="edcd8-144">Bir bağlantı toohello kaynağıdır.</span><span class="sxs-lookup"><span data-stu-id="edcd8-144">A link toohello resource.</span></span>        |
|<span data-ttu-id="edcd8-145">Depolama alanı yolu</span><span class="sxs-lookup"><span data-stu-id="edcd8-145">Storage path</span></span>     |  <span data-ttu-id="edcd8-146">Yol toohello depolama hesabı ve kapsayıcı hello günlükleri (herhangi bir çalıştırma hello sırasında oluşturulamadığı varsa) içeren.</span><span class="sxs-lookup"><span data-stu-id="edcd8-146">Path toohello storage account and container that contain hello logs (if any were produced during hello run).</span></span> <span data-ttu-id="edcd8-147">Bu ayar hello portal çıktıktan sonra devam etmez.</span><span class="sxs-lookup"><span data-stu-id="edcd8-147">This setting does not persist after you leave hello portal.</span></span>        |
|<span data-ttu-id="edcd8-148">Özet</span><span class="sxs-lookup"><span data-stu-id="edcd8-148">Summary</span></span>     | <span data-ttu-id="edcd8-149">Merhaba kaynak durumu özeti.</span><span class="sxs-lookup"><span data-stu-id="edcd8-149">Summary of hello resource health.</span></span>        |
|<span data-ttu-id="edcd8-150">Ayrıntısı</span><span class="sxs-lookup"><span data-stu-id="edcd8-150">Detail</span></span>     | <span data-ttu-id="edcd8-151">Merhaba kaynak durumu hakkında ayrıntılı bilgiler.</span><span class="sxs-lookup"><span data-stu-id="edcd8-151">Detailed information on hello resource health.</span></span>        |
|<span data-ttu-id="edcd8-152">Son çalıştırma</span><span class="sxs-lookup"><span data-stu-id="edcd8-152">Last run</span></span>     | <span data-ttu-id="edcd8-153">Son zaman hello hello olduğu zaman sorun giderme çalıştı.</span><span class="sxs-lookup"><span data-stu-id="edcd8-153">hello time hello last time troubleshooting was ran.</span></span>        |


<span data-ttu-id="edcd8-154">Merhaba **eylem** sekmesi nasıl tooresolve hello üzerinde sorunu genel rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="edcd8-154">hello **Action** tab provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="edcd8-155">Bir eylemin hello sorunu gerçekleştirilebiliyorsa bir bağlantı ile ek yönergeler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="edcd8-155">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="edcd8-156">Merhaba durumda hiçbir ek yönergeler olduğu hello yanıt hello url tooopen bir destek servis talebi sağlar..</span><span class="sxs-lookup"><span data-stu-id="edcd8-156">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="edcd8-157">Merhaba yanıt ve dahil edilen nedir hello özellikleri hakkında daha fazla bilgi için ziyaret [Ağ İzleyicisi sorun giderme genel bakış](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="edcd8-157">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>


## <a name="next-steps"></a><span data-ttu-id="edcd8-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="edcd8-158">Next steps</span></span>

<span data-ttu-id="edcd8-159">Bu Dur VPN bağlantısı ayarları değiştirilmiş olup [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) söz konusu olabilecek hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.</span><span class="sxs-lookup"><span data-stu-id="edcd8-159">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>


[2]: ./media/network-watcher-troubleshoot-manage-portal/2.png
