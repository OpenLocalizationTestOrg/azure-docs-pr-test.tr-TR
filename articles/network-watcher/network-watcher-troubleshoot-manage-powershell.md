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
ms.openlocfilehash: b7dbe6e44e0fa1ea0481223a84098d7a57c068a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="193f2-103">Sanal ağ geçidi ve Azure Ağ İzleyicisi PowerShell kullanarak bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="193f2-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="193f2-104">Portal</span><span class="sxs-lookup"><span data-stu-id="193f2-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="193f2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="193f2-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="193f2-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="193f2-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="193f2-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="193f2-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="193f2-108">REST API</span><span class="sxs-lookup"><span data-stu-id="193f2-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="193f2-109">Ağ kaynaklarınızı Azure toounderstanding ilgili olarak Ağ İzleyicisi çok sayıda özellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="193f2-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="193f2-110">Bu özelliklerin biri kaynak sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="193f2-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="193f2-111">Kaynak sorun giderme hello portal, PowerShell'i, CLI veya REST API çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="193f2-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="193f2-112">Çağrıldığında, Ağ İzleyicisi Merhaba bir sanal ağ geçidi veya bağlantı durumunu inceler ve bulduklarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="193f2-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="193f2-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="193f2-113">Before you begin</span></span>

<span data-ttu-id="193f2-114">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="193f2-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="193f2-115">Desteklenen ağ geçidi türleri ziyaret listesi [desteklenen ağ geçidi türleri](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="193f2-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="193f2-116">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="193f2-116">Overview</span></span>

<span data-ttu-id="193f2-117">Kaynak sorun giderme hello yeteneği sağlar sanal ağ geçitleri ve bağlantılarla ortaya çıkan sorunları giderme.</span><span class="sxs-lookup"><span data-stu-id="193f2-117">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="193f2-118">Bir istek tooresource sorun giderme yapıldığında günlükleri yükleniyor sorgulanan ve sahip denetlenir.</span><span class="sxs-lookup"><span data-stu-id="193f2-118">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="193f2-119">İnceleme tamamlandığında hello sonuçlar döndürülür.</span><span class="sxs-lookup"><span data-stu-id="193f2-119">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="193f2-120">Hangi birden çok dakika tooreturn bir sonuç ele geçirebilir sorun giderme istekleri uzun süredir çalışıp kaynak ister.</span><span class="sxs-lookup"><span data-stu-id="193f2-120">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="193f2-121">sorun giderme gelen hello günlükleri, belirtilen bir depolama hesabı üzerinde bir kapsayıcıda depolanır.</span><span class="sxs-lookup"><span data-stu-id="193f2-121">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="193f2-122">Ağ İzleyicisi alma</span><span class="sxs-lookup"><span data-stu-id="193f2-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="193f2-123">Merhaba ilk adımı tooretrieve hello Ağ İzleyicisi örneğidir.</span><span class="sxs-lookup"><span data-stu-id="193f2-123">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="193f2-124">Merhaba `$networkWatcher` değişkeni toohello geçirilen `Start-AzureRmNetworkWatcherResourceTroubleshooting` 4. adımda cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="193f2-124">hello `$networkWatcher` variable is passed toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="193f2-125">Sanal ağ geçidi bağlantısı alma</span><span class="sxs-lookup"><span data-stu-id="193f2-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="193f2-126">Bu örnekte, kaynak sorun giderme olduğu olan tükendi bağlantı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="193f2-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="193f2-127">Ayrıca bir sanal ağ geçidi geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="193f2-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="193f2-128">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="193f2-128">Create a storage account</span></span>

<span data-ttu-id="193f2-129">Kaynak sorun giderme hello kaynak hello durumunu ilgili verileri döndürür, günlükleri tooa depolama hesabı toobe gözden de kaydeder.</span><span class="sxs-lookup"><span data-stu-id="193f2-129">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="193f2-130">Bu adımda, biz depolama hesabı oluşturma, depolama hesabınız varsa bunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="193f2-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="193f2-131">Ağ İzleyicisi kaynak sorun giderme çalıştırın</span><span class="sxs-lookup"><span data-stu-id="193f2-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="193f2-132">Merhaba kaynaklarla ilgili sorunları giderme `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="193f2-132">You troubleshoot resources with hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="193f2-133">Biz hello cmdlet hello Ağ İzleyicisi nesnesinin, hello hello bağlantı kimliği veya sanal ağ geçidi, hello depolama hesabı kimliği ve hello yolu toostore hello sonuçları geçirin.</span><span class="sxs-lookup"><span data-stu-id="193f2-133">We pass hello cmdlet hello Network Watcher object, hello Id of hello Connection or Virtual Network Gateway, hello storage account id, and hello path toostore hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="193f2-134">Merhaba `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet uzun çalışıyor ve birkaç dakika toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="193f2-134">hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes toocomplete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="193f2-135">Merhaba cmdlet'ini çalıştırdıktan sonra Ağ İzleyicisi Merhaba kaynak tooverify hello durumu inceler.</span><span class="sxs-lookup"><span data-stu-id="193f2-135">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="193f2-136">Toohello Kabuk hello sonuçlar döndürür ve belirtilen hello depolama hesabında günlüklerini hello sonuçlarını kaydeder.</span><span class="sxs-lookup"><span data-stu-id="193f2-136">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="193f2-137">Merhaba sonuçlarını anlama</span><span class="sxs-lookup"><span data-stu-id="193f2-137">Understanding hello results</span></span>

<span data-ttu-id="193f2-138">Merhaba eylem metni nasıl tooresolve hello üzerinde sorunu genel rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="193f2-138">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="193f2-139">Bir eylemin hello sorunu gerçekleştirilebiliyorsa bir bağlantı ile ek yönergeler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="193f2-139">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="193f2-140">Merhaba durumda hiçbir ek yönergeler olduğu hello yanıt hello url tooopen bir destek servis talebi sağlar..</span><span class="sxs-lookup"><span data-stu-id="193f2-140">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="193f2-141">Merhaba yanıt ve dahil edilen nedir hello özellikleri hakkında daha fazla bilgi için ziyaret [Ağ İzleyicisi sorun giderme genel bakış](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="193f2-141">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="193f2-142">Azure depolama hesaplarından dosyaları indirme ile ilgili yönergeler için çok başvuran[.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="193f2-142">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="193f2-143">Kullanılabilir başka bir Depolama Gezgini aracıdır.</span><span class="sxs-lookup"><span data-stu-id="193f2-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="193f2-144">Depolama Gezgini hakkında daha fazla bilgi bağlantısı aşağıdaki hello şurada bulunabilir: [Depolama Gezgini](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="193f2-144">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="193f2-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="193f2-145">Next steps</span></span>

<span data-ttu-id="193f2-146">Bu Dur VPN bağlantısı ayarları değiştirilmiş olup [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) söz konusu olabilecek hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.</span><span class="sxs-lookup"><span data-stu-id="193f2-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
