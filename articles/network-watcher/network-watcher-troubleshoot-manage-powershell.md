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
ms.openlocfilehash: 0bdffbac18d1d236b7674feed4dbc784e50e0ea8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a><span data-ttu-id="bf4ec-103">Sanal ağ geçidi ve Azure Ağ İzleyicisi PowerShell kullanarak bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="bf4ec-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="bf4ec-104">Portal</span><span class="sxs-lookup"><span data-stu-id="bf4ec-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="bf4ec-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bf4ec-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="bf4ec-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="bf4ec-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="bf4ec-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="bf4ec-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="bf4ec-108">REST API</span><span class="sxs-lookup"><span data-stu-id="bf4ec-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="bf4ec-109">Ağ kaynaklarınızı Azure anlamak için ilgili olarak Ağ İzleyicisi çok sayıda özellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="bf4ec-110">Bu özelliklerin biri kaynak sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="bf4ec-111">Kaynak sorun giderme portalı, PowerShell, CLI veya REST API çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="bf4ec-112">Çağrıldığında, Ağ İzleyicisi bir sanal ağ geçidi veya bağlantı durumunu inceler ve bulduklarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bf4ec-113">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="bf4ec-113">Before you begin</span></span>

<span data-ttu-id="bf4ec-114">Bu senaryo zaten izlediğiniz adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) bir Ağ İzleyicisi oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="bf4ec-115">Desteklenen ağ geçidi türleri ziyaret listesi [desteklenen ağ geçidi türleri](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="bf4ec-115">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="bf4ec-116">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="bf4ec-116">Overview</span></span>

<span data-ttu-id="bf4ec-117">Kaynak sorunlarını giderme özelliği sağlar sanal ağ geçitleri ve bağlantılarla ortaya çıkan sorunları giderme.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-117">Resource troubleshooting provides the ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="bf4ec-118">Kaynak sorun giderme için bir istek yapıldığında, günlükleri yükleniyor sorgulanan ve sahip denetlenir.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-118">When a request is made to resource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="bf4ec-119">İnceleme tamamlandığında, sonuçları döndürülür.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-119">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="bf4ec-120">Sorun giderme istekleri uzun süredir çalışıp kaynak, hangi birden çok dakika sürebilir bir sonuç ister.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-120">Resource troubleshooting requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="bf4ec-121">Sorun giderme gelen günlükleri, belirtilen bir depolama hesabı üzerinde bir kapsayıcıda depolanır.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-121">The logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="bf4ec-122">Ağ İzleyicisi alma</span><span class="sxs-lookup"><span data-stu-id="bf4ec-122">Retrieve Network Watcher</span></span>

<span data-ttu-id="bf4ec-123">Ağ İzleyicisi örneği almak için ilk adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-123">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="bf4ec-124">`$networkWatcher` Değişkeni iletilir `Start-AzureRmNetworkWatcherResourceTroubleshooting` 4. adımda cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-124">The `$networkWatcher` variable is passed to the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet in step 4.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="bf4ec-125">Sanal ağ geçidi bağlantısı alma</span><span class="sxs-lookup"><span data-stu-id="bf4ec-125">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="bf4ec-126">Bu örnekte, kaynak sorun giderme olduğu olan tükendi bağlantı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-126">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="bf4ec-127">Ayrıca bir sanal ağ geçidi geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-127">You can also pass it a Virtual Network Gateway.</span></span>

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a><span data-ttu-id="bf4ec-128">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bf4ec-128">Create a storage account</span></span>

<span data-ttu-id="bf4ec-129">Kaynak durumu hakkında veriler kaynak sorun giderme döndürür, ayrıca gözden geçirilmesi için bir depolama hesabı günlükleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-129">Resource troubleshooting returns data about the health of the resource, it also saves logs to a storage account to be reviewed.</span></span> <span data-ttu-id="bf4ec-130">Bu adımda, biz depolama hesabı oluşturma, depolama hesabınız varsa bunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-130">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="bf4ec-131">Ağ İzleyicisi kaynak sorun giderme çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bf4ec-131">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="bf4ec-132">Kaynaklarla ilgili sorunları giderme `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-132">You troubleshoot resources with the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet.</span></span> <span data-ttu-id="bf4ec-133">Cmdlet Ağ İzleyicisi nesnesinin, bağlantı veya sanal ağ geçidi kimliği, depolama hesabı kimliği ve yol Sonuçların depolanacağı geçirin.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-133">We pass the cmdlet the Network Watcher object, the Id of the Connection or Virtual Network Gateway, the storage account id, and the path to store the results.</span></span>

> [!NOTE]
> <span data-ttu-id="bf4ec-134">`Start-AzureRmNetworkWatcherResourceTroubleshooting` Cmdlet uzun çalışıyor ve tamamlanması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-134">The `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet is long running and may take a few minutes to complete.</span></span>

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

<span data-ttu-id="bf4ec-135">Cmdlet'ini çalıştırdıktan sonra Ağ İzleyicisi sistem durumunu doğrulamak için kaynak inceler.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-135">Once you run the cmdlet, Network Watcher reviews the resource to verify the health.</span></span> <span data-ttu-id="bf4ec-136">Kabuk sonuçları döndürür ve belirtilen depolama hesabında günlüklerini sonuçlarını kaydeder.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-136">It returns the results to the shell and stores logs of the results in the storage account specified.</span></span>

## <a name="understanding-the-results"></a><span data-ttu-id="bf4ec-137">Sonuçları anlama</span><span class="sxs-lookup"><span data-stu-id="bf4ec-137">Understanding the results</span></span>

<span data-ttu-id="bf4ec-138">Eylem metin sorunun nasıl çözümleneceği hakkında genel kılavuzluk sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-138">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="bf4ec-139">Bir eylem için sorunu gerçekleştirilebiliyorsa bir bağlantı ile ek yönergeler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-139">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="bf4ec-140">Durumda hiçbir ek yönergeler bulunduğu bir destek servis talebi açmaya url yanıt sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-140">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="bf4ec-141">Yanıt ve dahil edilen nedir özellikleri hakkında daha fazla bilgi için ziyaret [Ağ İzleyicisi sorun giderme genel bakış](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bf4ec-141">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="bf4ec-142">Azure depolama hesaplarından dosyaları indirme ile ilgili yönergeler için bkz [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="bf4ec-142">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="bf4ec-143">Kullanılabilir başka bir Depolama Gezgini aracıdır.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-143">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="bf4ec-144">Aşağıdaki bağlantıda Depolama Gezgini hakkında daha fazla bilgi şurada bulunabilir: [Depolama Gezgini](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="bf4ec-144">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf4ec-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bf4ec-145">Next steps</span></span>

<span data-ttu-id="bf4ec-146">Bu Dur VPN bağlantısı ayarları değiştirilmiş olup [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) söz konusu olabilecek ağ güvenlik grubu ve güvenlik kuralları izlemek için.</span><span class="sxs-lookup"><span data-stu-id="bf4ec-146">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
