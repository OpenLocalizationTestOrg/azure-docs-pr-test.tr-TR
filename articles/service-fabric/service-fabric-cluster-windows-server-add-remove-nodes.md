---
title: "aaaAdd veya kaldırma düğümleri tooa tek başına Service Fabric kümesi | Microsoft Docs"
description: "Nasıl tooadd veya kaldırma düğümleri tooan Azure Service Fabric kümesi bir fiziksel veya şirket içi olarak Windows Server çalıştıran sanal makine üzerinde veya tüm bulut bilgi edinin."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="5cb78-103">Windows Server'da çalışan düğümleri tooa tek başına Service Fabric kümesi Ekle Kaldır</span><span class="sxs-lookup"><span data-stu-id="5cb78-103">Add or remove nodes tooa standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="5cb78-104">Sonra [Windows Server makinelerde tek başına Service Fabric kümesi oluşturulan](service-fabric-cluster-creation-for-windows-server.md), iş gereksinimlerinize değiştirebilir ve düğümler tooyour kümesini kaldırmak veya tooadd ihtiyacınız olabilir.</span><span class="sxs-lookup"><span data-stu-id="5cb78-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need tooadd or remove nodes tooyour cluster.</span></span> <span data-ttu-id="5cb78-105">Bu makalede bu ayrıntılı adımlar tooachieve sağlar.</span><span class="sxs-lookup"><span data-stu-id="5cb78-105">This article provides detailed steps tooachieve this.</span></span> <span data-ttu-id="5cb78-106">Lütfen Ekle/Kaldır düğümü işlevselliği yerel geliştirme kümelerinde desteklenmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5cb78-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-tooyour-cluster"></a><span data-ttu-id="5cb78-107">Tooyour küme düğümleri Ekle</span><span class="sxs-lookup"><span data-stu-id="5cb78-107">Add nodes tooyour cluster</span></span>
1. <span data-ttu-id="5cb78-108">Prepare hello VM/makine hello bahsedilen hello adımları izleyerek tooadd tooyour küme istediğiniz [hazırlama hello makineleri Küme dağıtımı için toomeet hello Önkoşullar](service-fabric-cluster-creation-for-windows-server.md) bölümü</span><span class="sxs-lookup"><span data-stu-id="5cb78-108">Prepare hello VM/machine you want tooadd tooyour cluster by following hello steps mentioned in hello [Prepare hello machines toomeet hello prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="5cb78-109">Hangi hata etki alanı ve bu VM/makineye giderek tooadd olduğunuz yükseltme etki alanını tanımlayın</span><span class="sxs-lookup"><span data-stu-id="5cb78-109">Identify which fault domain and upgrade domain you are going tooadd this VM/machine to</span></span>
3. <span data-ttu-id="5cb78-110">Uzak Masaüstü (RDP) hello VM/makine tooadd toohello küme istediğiniz başlatın</span><span class="sxs-lookup"><span data-stu-id="5cb78-110">Remote desktop (RDP) into hello VM/machine that you want tooadd toohello cluster</span></span>
4. <span data-ttu-id="5cb78-111">Kopyalama veya [Windows Server için Service Fabric hello tek başına paketini indirin](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/makine ve hello paketin sıkıştırmasını açın</span><span class="sxs-lookup"><span data-stu-id="5cb78-111">Copy or [download hello standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine and unzip hello package</span></span>
5. <span data-ttu-id="5cb78-112">PowerShell yükseltilmiş ayrıcalıklarla çalıştırın ve hello sıkıştırması açılmış paketi toohello konumu gidin</span><span class="sxs-lookup"><span data-stu-id="5cb78-112">Run Powershell with elevated privileges, and navigate toohello location of hello unzipped package</span></span>
6. <span data-ttu-id="5cb78-113">Merhaba çalıştırmak *AddNode.ps1* betik hello yeni düğümü tooadd açıklayan hello parametrelere sahip.</span><span class="sxs-lookup"><span data-stu-id="5cb78-113">Run hello *AddNode.ps1* script with hello parameters describing hello new node tooadd.</span></span> <span data-ttu-id="5cb78-114">Aşağıdaki Hello örnek VM5 olarak adlandırılan yeni bir düğüm ekler, türüyle NodeType0 ve IP 182.17.34.52, UD1 ve fd halinde adresi: / dc1/r0.</span><span class="sxs-lookup"><span data-stu-id="5cb78-114">hello example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="5cb78-115">Merhaba *ExistingClusterConnectionEndPoint* hello mevcut kümede zaten bir bağlantı uç noktası bir düğüme hello IP adresini olabilen *herhangi* hello kümedeki düğüm.</span><span class="sxs-lookup"><span data-stu-id="5cb78-115">hello *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in hello existing cluster, which can be hello IP address of *any* node in hello cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="5cb78-116">Hello betik çalışması bittikten sonra hello yeni düğüm hello çalıştırarak eklenip eklenmediğini denetleyebilirsiniz [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="5cb78-116">Once hello script finishes running, you can check if hello new node has been added by running hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="5cb78-117">tooensure tutarlılık hello kümedeki farklı düğümleri arasındaki yapılandırma yükseltme başlatması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5cb78-117">tooensure consistency across different nodes in hello cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="5cb78-118">Çalıştırmak [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello son yapılandırma dosyasını ve hello yeni eklenen düğüm çok Ekle "Düğümleri" bölümü.</span><span class="sxs-lookup"><span data-stu-id="5cb78-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and add hello newly added node too"Nodes" section.</span></span> <span data-ttu-id="5cb78-119">Ayrıca tooalways hello son küme yapılandırması tooredploy hello kümeyle duyduğunuz hello durumda kullanılabilir olması önerilir aynı yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="5cb78-119">It is also recommended tooalways have hello latest cluster configuration available in hello case that you need tooredploy a cluster with hello same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="5cb78-120">Çalıştırma [başlangıç ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello yükseltme.</span><span class="sxs-lookup"><span data-stu-id="5cb78-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="5cb78-121">Service Fabric Explorer üzerinde hello yükseltme hello ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cb78-121">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="5cb78-122">Alternatif olarak, çalıştırabilirsiniz [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="5cb78-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="5cb78-123">Windows güvenliği kullanarak gMSA düğümleri tooclusters yapılandırılmış ekleme</span><span class="sxs-lookup"><span data-stu-id="5cb78-123">Add nodes tooclusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="5cb78-124">Grup yönetilen hizmet Account(gMSA) ile (https://technet.microsoft.com/library/hh831782.aspx) yapılandırılmış kümeler için yapılandırma yükseltme kullanarak yeni bir düğüm eklenebilir:</span><span class="sxs-lookup"><span data-stu-id="5cb78-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="5cb78-125">Çalıştırma [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) varolan herhangi bir hello düğüme tooget hello son yapılandırma dosyasını ve ayrıntılarını Ekle tooadd hello "düğümleri" bölümünde istediğiniz hello yeni düğümü.</span><span class="sxs-lookup"><span data-stu-id="5cb78-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of hello existing nodes tooget hello latest configuration file and add details about hello new node you want tooadd in hello "Nodes" section.</span></span> <span data-ttu-id="5cb78-126">Merhaba Yeni düğümün bir parçası olduğundan emin olun hello aynı grup yönetilen hesabı.</span><span class="sxs-lookup"><span data-stu-id="5cb78-126">Make sure hello new node is part of hello same group managed account.</span></span> <span data-ttu-id="5cb78-127">Bu hesap tüm makinelerde yönetici olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5cb78-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="5cb78-128">Çalıştırma [başlangıç ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello yükseltme.</span><span class="sxs-lookup"><span data-stu-id="5cb78-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    <span data-ttu-id="5cb78-129">Service Fabric Explorer üzerinde hello yükseltme hello ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cb78-129">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="5cb78-130">Alternatif olarak, çalıştırabilirsiniz [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="5cb78-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-tooyour-cluster"></a><span data-ttu-id="5cb78-131">Düğüm türleri tooyour kümesi Ekle</span><span class="sxs-lookup"><span data-stu-id="5cb78-131">Add node types tooyour cluster</span></span>
<span data-ttu-id="5cb78-132">İçinde yeni düğüm türü tooadd sipariş, yapılandırma tooinclude hello yeni düğüm türü "Özellikler" altında "NodeTypes" bölümündeki değiştirmek ve bir yapılandırmaya başlamadan kullanarak yükseltme [başlangıç ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="5cb78-132">In order tooadd a new node type, modify your configuration tooinclude hello new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="5cb78-133">Merhaba yükseltme işlemi tamamlandıktan sonra bu düğüm türü ile yeni düğümler tooyour küme ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cb78-133">Once hello upgrade completes, you can add new nodes tooyour cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="5cb78-134">Kümeden düğüm kaldırma</span><span class="sxs-lookup"><span data-stu-id="5cb78-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="5cb78-135">Bir yapılandırma yükseltme şekilde aşağıdaki hello kullanarak bir kümeden bir düğümü kaldırılabilir:</span><span class="sxs-lookup"><span data-stu-id="5cb78-135">A node can be removed from a cluster using a configuration upgrade, in hello following manner:</span></span>

1. <span data-ttu-id="5cb78-136">Çalıştırma [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello son yapılandırma dosyasını ve *kaldırmak* "Düğümleri" bölümünden hello düğümü.</span><span class="sxs-lookup"><span data-stu-id="5cb78-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and *remove* hello node from "Nodes" section.</span></span>
<span data-ttu-id="5cb78-137">Merhaba "NodesToBeRemoved" eklemek parametre çok "Kurulum" Bölüm "FabricSettings" bölüm içinde.</span><span class="sxs-lookup"><span data-stu-id="5cb78-137">Add hello "NodesToBeRemoved" parameter too"Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="5cb78-138">Merhaba "value" kaldırılan toobe gereken düğümleri düğüm adlarının virgülle ayrılmış bir listesi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5cb78-138">hello "value" should be a comma separated list of node names of nodes that need toobe removed.</span></span>

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. <span data-ttu-id="5cb78-139">Çalıştırma [başlangıç ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello yükseltme.</span><span class="sxs-lookup"><span data-stu-id="5cb78-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="5cb78-140">Service Fabric Explorer üzerinde hello yükseltme hello ilerlemesini izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5cb78-140">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="5cb78-141">Alternatif olarak, çalıştırabilirsiniz [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="5cb78-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="5cb78-142">Düğümleri kaldırma birden fazla yükseltme başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="5cb78-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="5cb78-143">Bazı düğümler işaretlenir `IsSeedNode=”true”` etiketi ve hello küme sorgulayarak tanımlanabilir kullanarak bildirim `Get-ServiceFabricClusterManifest`.</span><span class="sxs-lookup"><span data-stu-id="5cb78-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying hello cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="5cb78-144">Merhaba çekirdek düğümleri gibi senaryolarda taşınmış toobe gerekeceğinden bu düğümleri kaldırılmasını diğerlerinden daha uzun sürebilir.</span><span class="sxs-lookup"><span data-stu-id="5cb78-144">Removal of such nodes may take longer than others since hello seed nodes will have toobe moved around in such scenarios.</span></span> <span data-ttu-id="5cb78-145">Merhaba küme en az 3 birincil düğüm türü düğümleri bulundurmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5cb78-145">hello cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="5cb78-146">Düğüm türleri, kümeden kaldırma</span><span class="sxs-lookup"><span data-stu-id="5cb78-146">Remove node types from your cluster</span></span>
<span data-ttu-id="5cb78-147">Merhaba düğüm türü başvuran tüm düğümleri varsa bir düğüm türü kaldırmadan önce çift gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="5cb78-147">Before removing a node type, please double check if there are any nodes referencing hello node type.</span></span> <span data-ttu-id="5cb78-148">Bu düğümler hello karşılık gelen düğüm türü kaldırmadan önce kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5cb78-148">Remove these nodes before removing hello corresponding node type.</span></span> <span data-ttu-id="5cb78-149">Tüm ilgili düğümleri kaldırıldıktan sonra hello NodeType hello küme yapılandırmasından kaldırmak ve bir yapılandırmaya başlamadan kullanarak yükseltme [başlangıç ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="5cb78-149">Once all corresponding nodes are removed, you can remove hello NodeType from hello cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="5cb78-150">Birincil düğüm kümenizin değiştirin</span><span class="sxs-lookup"><span data-stu-id="5cb78-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="5cb78-151">birincil düğüm Hello değiştirme ardına toplu olarak ekleme ve kaldırma yerine gerçekleştirilen bir düğüm olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5cb78-151">hello replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5cb78-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5cb78-152">Next steps</span></span>
* [<span data-ttu-id="5cb78-153">Tek başına Windows kümesi için yapılandırma ayarları</span><span class="sxs-lookup"><span data-stu-id="5cb78-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="5cb78-154">Tek başına küme X509 kullanarak Windows güvenli sertifikaları</span><span class="sxs-lookup"><span data-stu-id="5cb78-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="5cb78-155">Azure VM'ler Windows çalıştıran bir tek başına Service Fabric kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="5cb78-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

