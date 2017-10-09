---
title: "aaaTroubleshoot Azure sanal ağ geçidi ve bağlantıları - Azure CLI 1.0 | Microsoft Docs"
description: "Bu sayfayı toouse hello Azure Ağ İzleyicisi Azure CLI 1.0 nasıl sorun giderme açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2838bc61-b182-4da8-8533-27db8fdbd177
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: a0511689d773f9c7216b0fe5470e27f754eb600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-azure-cli-10"></a><span data-ttu-id="19972-103">Sanal ağ geçidi ve Azure Ağ İzleyicisi Azure CLI 1.0 kullanarak bağlantı sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="19972-103">Troubleshoot Virtual Network Gateway and Connections using Azure Network Watcher Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="19972-104">Portal</span><span class="sxs-lookup"><span data-stu-id="19972-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="19972-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="19972-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="19972-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="19972-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="19972-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="19972-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="19972-108">REST API</span><span class="sxs-lookup"><span data-stu-id="19972-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="19972-109">Ağ kaynaklarınızı Azure toounderstanding ilgili olarak Ağ İzleyicisi çok sayıda özellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="19972-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="19972-110">Bu özelliklerin biri kaynak sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="19972-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="19972-111">Kaynak sorun giderme hello portal, PowerShell'i, CLI veya REST API çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="19972-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="19972-112">Çağrıldığında, Ağ İzleyicisi Merhaba bir sanal ağ geçidi veya bağlantı durumunu inceler ve bulduklarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="19972-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="19972-113">Bu makalede, platformlar arası Azure CLI 1.0, Windows, Mac ve Linux için kullanılabilir olduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="19972-113">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="19972-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="19972-114">Before you begin</span></span>

<span data-ttu-id="19972-115">Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi oluşturma](network-watcher-create.md) toocreate bir Ağ İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="19972-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="19972-116">Desteklenen ağ geçidi türleri ziyaret listesi [desteklenen ağ geçidi türleri](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="19972-116">For a list of supported gateway types visit, [Supported Gateway types](/network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="19972-117">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="19972-117">Overview</span></span>

<span data-ttu-id="19972-118">Kaynak sorun giderme hello yeteneği sağlar sanal ağ geçitleri ve bağlantılarla ortaya çıkan sorunları giderme.</span><span class="sxs-lookup"><span data-stu-id="19972-118">Resource troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network Gateways and Connections.</span></span> <span data-ttu-id="19972-119">Bir istek tooresource sorun giderme yapıldığında günlükleri yükleniyor sorgulanan ve sahip denetlenir.</span><span class="sxs-lookup"><span data-stu-id="19972-119">When a request is made tooresource troubleshooting, logs are being queried and inspected.</span></span> <span data-ttu-id="19972-120">İnceleme tamamlandığında hello sonuçlar döndürülür.</span><span class="sxs-lookup"><span data-stu-id="19972-120">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="19972-121">Hangi birden çok dakika tooreturn bir sonuç ele geçirebilir sorun giderme istekleri uzun süredir çalışıp kaynak ister.</span><span class="sxs-lookup"><span data-stu-id="19972-121">Resource troubleshooting requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="19972-122">sorun giderme gelen hello günlükleri, belirtilen bir depolama hesabı üzerinde bir kapsayıcıda depolanır.</span><span class="sxs-lookup"><span data-stu-id="19972-122">hello logs from troubleshooting are stored in a container on a storage account that is specified.</span></span>

## <a name="retrieve-a-virtual-network-gateway-connection"></a><span data-ttu-id="19972-123">Sanal ağ geçidi bağlantısı alma</span><span class="sxs-lookup"><span data-stu-id="19972-123">Retrieve a Virtual Network Gateway Connection</span></span>

<span data-ttu-id="19972-124">Bu örnekte, kaynak sorun giderme olduğu olan tükendi bağlantı üzerinde.</span><span class="sxs-lookup"><span data-stu-id="19972-124">In this example, resource troubleshooting is being ran on a Connection.</span></span> <span data-ttu-id="19972-125">Ayrıca bir sanal ağ geçidi geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19972-125">You can also pass it a Virtual Network Gateway.</span></span> <span data-ttu-id="19972-126">Merhaba aşağıdaki cmdlet'i bir kaynak grubunda hello vpn bağlantılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="19972-126">hello following cmdlet lists hello vpn-connections in a resource group.</span></span>

```azurecli
azure network vpn-connection list -g resourceGroupName
```

<span data-ttu-id="19972-127">Bir abonelikte hello bağlantıları hello komutu toosee de çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19972-127">You can also run hello command toosee hello connections in a subscription.</span></span>

```azurecli
azure network vpn-connection list -s subscription
```

<span data-ttu-id="19972-128">Hello bağlantısının hello adına sahip olduğunda, kendi kaynak kimliği bu komut tooget çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="19972-128">Once you have hello name of hello connection, you can run this command tooget its resource Id:</span></span>

```azurecli
azure network vpn-connection show -g resourceGroupName -n connectionName
```

## <a name="create-a-storage-account"></a><span data-ttu-id="19972-129">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="19972-129">Create a storage account</span></span>

<span data-ttu-id="19972-130">Kaynak sorun giderme hello kaynak hello durumunu ilgili verileri döndürür, günlükleri tooa depolama hesabı toobe gözden de kaydeder.</span><span class="sxs-lookup"><span data-stu-id="19972-130">Resource troubleshooting returns data about hello health of hello resource, it also saves logs tooa storage account toobe reviewed.</span></span> <span data-ttu-id="19972-131">Bu adımda, biz depolama hesabı oluşturma, depolama hesabınız varsa bunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="19972-131">In this step, we create a storage account, if an existing storage account exists you can use it.</span></span>

1. <span data-ttu-id="19972-132">Merhaba depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="19972-132">Create hello storage account</span></span>

    ```azurecli
    azure storage account create -n storageAccountName -l location -g resourceGroupName
    ```

1. <span data-ttu-id="19972-133">Merhaba depolama hesabı anahtarlarını alma</span><span class="sxs-lookup"><span data-stu-id="19972-133">Get hello storage account keys</span></span>

    ```azurecli
    azure storage account keys list storageAccountName -g resourcegroupName
    ```

1. <span data-ttu-id="19972-134">Merhaba kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="19972-134">Create hello container</span></span>

    ```azurecli
    azure storage container create --account-name storageAccountName -g resourcegroupName --account-key {storageAccountKey} --container logs
    ```

## <a name="run-network-watcher-resource-troubleshooting"></a><span data-ttu-id="19972-135">Ağ İzleyicisi kaynak sorun giderme çalıştırın</span><span class="sxs-lookup"><span data-stu-id="19972-135">Run Network Watcher resource troubleshooting</span></span>

<span data-ttu-id="19972-136">Merhaba kaynaklarla ilgili sorunları giderme `network watcher troubleshoot` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="19972-136">You troubleshoot resources with hello `network watcher troubleshoot` cmdlet.</span></span> <span data-ttu-id="19972-137">Biz hello cmdlet hello kaynak grubu geçirebilir, hello hello Ağ İzleyicisi, hello hello bağlantının kimliği adını hello hello depolama hesabının kimliğini ve hello yolu toohello blob toostore hello sonuçlarında sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="19972-137">We pass hello cmdlet hello resource group, hello name of hello Network Watcher, hello Id of hello connection, hello Id of hello storage account, and hello path toohello blob toostore hello troubleshoot results in.</span></span>

```azurecli
azure network watcher troubleshoot -g resourceGroupName -n networkWatcherName -t connectionId -i storageId -p storagePath
```

<span data-ttu-id="19972-138">Merhaba cmdlet'ini çalıştırdıktan sonra Ağ İzleyicisi Merhaba kaynak tooverify hello durumu inceler.</span><span class="sxs-lookup"><span data-stu-id="19972-138">Once you run hello cmdlet, Network Watcher reviews hello resource tooverify hello health.</span></span> <span data-ttu-id="19972-139">Toohello Kabuk hello sonuçlar döndürür ve belirtilen hello depolama hesabında günlüklerini hello sonuçlarını kaydeder.</span><span class="sxs-lookup"><span data-stu-id="19972-139">It returns hello results toohello shell and stores logs of hello results in hello storage account specified.</span></span>

## <a name="understanding-hello-results"></a><span data-ttu-id="19972-140">Merhaba sonuçlarını anlama</span><span class="sxs-lookup"><span data-stu-id="19972-140">Understanding hello results</span></span>

<span data-ttu-id="19972-141">Merhaba eylem metni nasıl tooresolve hello üzerinde sorunu genel rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="19972-141">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="19972-142">Bir eylemin hello sorunu gerçekleştirilebiliyorsa bir bağlantı ile ek yönergeler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="19972-142">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="19972-143">Merhaba durumda hiçbir ek yönergeler olduğu hello yanıt hello url tooopen bir destek servis talebi sağlar..</span><span class="sxs-lookup"><span data-stu-id="19972-143">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="19972-144">Merhaba yanıt ve dahil edilen nedir hello özellikleri hakkında daha fazla bilgi için ziyaret [Ağ İzleyicisi sorun giderme genel bakış](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="19972-144">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="19972-145">Azure depolama hesaplarından dosyaları indirme ile ilgili yönergeler için çok başvuran[.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="19972-145">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="19972-146">Kullanılabilir başka bir Depolama Gezgini aracıdır.</span><span class="sxs-lookup"><span data-stu-id="19972-146">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="19972-147">Depolama Gezgini hakkında daha fazla bilgi bağlantısı aşağıdaki hello şurada bulunabilir: [Depolama Gezgini](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="19972-147">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="19972-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="19972-148">Next steps</span></span>

<span data-ttu-id="19972-149">Bu Dur VPN bağlantısı ayarları değiştirilmiş olup [ağ güvenlik grupları yönet](../virtual-network/virtual-network-manage-nsg-arm-portal.md) söz konusu olabilecek hello ağ güvenlik grubu ve güvenlik kuralları aşağı tootrack.</span><span class="sxs-lookup"><span data-stu-id="19972-149">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
