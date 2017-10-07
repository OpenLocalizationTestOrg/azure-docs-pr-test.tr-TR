---
title: "aaaWindows HPC Pack Merhaba bulut seçeneklerinde küme | Microsoft Docs"
description: "Microsoft HPC Pack toocreate seçeneklerle hakkında bilgi edinin ve bir Windows yüksek performanslı bilgi işlem (HPC) hello Azure bulut kümede yönetme"
services: virtual-machines-windows,cloud-services,batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 6158d9dd0cecda38b14f85a2b2080163f18e8cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a><span data-ttu-id="2f6a6-103">Seçenekler ile HPC Pack toocreate ve bir Windows HPC kümesini azure'da yönetmek</span><span class="sxs-lookup"><span data-stu-id="2f6a6-103">Options with HPC Pack toocreate and manage a Windows HPC cluster in Azure</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="2f6a6-104">Bu makalede seçenekleri toocreate HPC Pack kümeleri toorun Windows iş yükleri odaklanır.</span><span class="sxs-lookup"><span data-stu-id="2f6a6-104">This article focuses on options toocreate HPC Pack clusters toorun Windows workloads.</span></span> <span data-ttu-id="2f6a6-105">Ayrıca seçenek vardır toorun oluşturma HPC Pack kümeleri için [Linux HPC iş yükleri](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f6a6-105">There are also options for creating HPC Pack clusters toorun [Linux HPC workloads](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="2f6a6-106">HPC Pack küme Azure Vm'lerde çalıştırın</span><span class="sxs-lookup"><span data-stu-id="2f6a6-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="2f6a6-107">Azure şablonları</span><span class="sxs-lookup"><span data-stu-id="2f6a6-107">Azure templates</span></span>
* <span data-ttu-id="2f6a6-108">(GitHub) [HPC Pack 2016 küme şablonları](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="2f6a6-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="2f6a6-109">(Market) [HPC paketi küme iş yükleri için](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span><span class="sxs-lookup"><span data-stu-id="2f6a6-109">(Marketplace) [HPC Pack cluster for Windows workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)</span></span>
* <span data-ttu-id="2f6a6-110">(Market) [Excel iş yükleri için HPC paketi küme](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span><span class="sxs-lookup"><span data-stu-id="2f6a6-110">(Marketplace) [HPC Pack cluster for Excel workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)</span></span>
* <span data-ttu-id="2f6a6-111">(Hızlı Başlangıç) [HPC kümesi oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span><span class="sxs-lookup"><span data-stu-id="2f6a6-111">(Quickstart) [Create an HPC cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)</span></span>
* <span data-ttu-id="2f6a6-112">(Hızlı Başlangıç) [Özel işlem düğümü görüntüsüyle HPC kümesi oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span><span class="sxs-lookup"><span data-stu-id="2f6a6-112">(Quickstart) [Create an HPC cluster with custom compute node image](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)</span></span>

### <a name="azure-vm-images"></a><span data-ttu-id="2f6a6-113">Azure VM görüntüleri</span><span class="sxs-lookup"><span data-stu-id="2f6a6-113">Azure VM images</span></span>
* [<span data-ttu-id="2f6a6-114">Windows Server 2016 baş düğümünde HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="2f6a6-114">HPC Pack 2016 head node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="2f6a6-115">HPC Pack 2016 işlem düğümü üzerinde Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2f6a6-115">HPC Pack 2016 compute node on Windows Server 2016</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [<span data-ttu-id="2f6a6-116">Windows Server 2012 R2 HPC Pack 2016 baş düğüm</span><span class="sxs-lookup"><span data-stu-id="2f6a6-116">HPC Pack 2016 head node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="2f6a6-117">Windows Server 2012 R2 HPC Pack 2016 işlem düğümünde</span><span class="sxs-lookup"><span data-stu-id="2f6a6-117">HPC Pack 2016 compute node on Windows Server 2012 R2</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [<span data-ttu-id="2f6a6-118">Windows Server 2012 R2 baş düğümünde HPC Pack 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2f6a6-118">HPC Pack 2012 R2 head node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [<span data-ttu-id="2f6a6-119">Windows Server 2012 R2 HPC Pack 2012 R2 işlem düğümünde</span><span class="sxs-lookup"><span data-stu-id="2f6a6-119">HPC Pack 2012 R2 compute node on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [<span data-ttu-id="2f6a6-120">HPC Pack hesaplama düğümünün Excel Windows Server 2012 R2 ile</span><span class="sxs-lookup"><span data-stu-id="2f6a6-120">HPC Pack compute node with Excel on Windows Server 2012 R2</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a><span data-ttu-id="2f6a6-121">PowerShell dağıtım komut dosyası</span><span class="sxs-lookup"><span data-stu-id="2f6a6-121">PowerShell deployment script</span></span>
* [<span data-ttu-id="2f6a6-122">HPC Pack Iaas dağıtım betiği hello ile HPC kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f6a6-122">Create an HPC cluster with hello HPC Pack IaaS deployment script</span></span>](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="2f6a6-123">Öğreticiler</span><span class="sxs-lookup"><span data-stu-id="2f6a6-123">Tutorials</span></span>
* [<span data-ttu-id="2f6a6-124">Öğretici: Azure bir HPC Pack 2016 küme dağıtma</span><span class="sxs-lookup"><span data-stu-id="2f6a6-124">Tutorial: Deploy an HPC Pack 2016 cluster in Azure</span></span>](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2f6a6-125">Öğretici: Azure toorun Excel HPC Pack kümede ve SOA iş yükleri ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="2f6a6-125">Tutorial: Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads</span></span>](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a><span data-ttu-id="2f6a6-126">Hello Azure portal ile el ile dağıtımı</span><span class="sxs-lookup"><span data-stu-id="2f6a6-126">Manual deployment with hello Azure portal</span></span>
* [<span data-ttu-id="2f6a6-127">Bir Azure VM'de HPC paketi küme baş düğümüne hello ayarlama</span><span class="sxs-lookup"><span data-stu-id="2f6a6-127">Set up hello head node of an HPC Pack cluster in an Azure VM</span></span>](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="2f6a6-128">Küme yönetimi</span><span class="sxs-lookup"><span data-stu-id="2f6a6-128">Cluster management</span></span>
* [<span data-ttu-id="2f6a6-129">Azure HPC Pack kümede işlem düğümlerine yönetme</span><span class="sxs-lookup"><span data-stu-id="2f6a6-129">Manage compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="2f6a6-130">Büyüme ve Azure işlem kaynakları bir HPC Pack kümesindeki Daralt</span><span class="sxs-lookup"><span data-stu-id="2f6a6-130">Grow and shrink Azure compute resources in an HPC Pack cluster</span></span>](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="2f6a6-131">İşlerini tooan HPC Pack Azure kümesinde gönderme</span><span class="sxs-lookup"><span data-stu-id="2f6a6-131">Submit jobs tooan HPC Pack cluster in Azure</span></span>](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="2f6a6-132">HPC Pack iş yönetimi</span><span class="sxs-lookup"><span data-stu-id="2f6a6-132">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)
* [<span data-ttu-id="2f6a6-133">Azure Active Directory ile Azure HPC Pack kümede yönetme</span><span class="sxs-lookup"><span data-stu-id="2f6a6-133">Manage an HPC Pack cluster in Azure with Azure Active Directory</span></span>](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a><span data-ttu-id="2f6a6-134">Çalışan rolü düğümleri tooan HPC paketi küme ekleme</span><span class="sxs-lookup"><span data-stu-id="2f6a6-134">Add worker role nodes tooan HPC Pack cluster</span></span>
* [<span data-ttu-id="2f6a6-135">HPC Pack ile tooAzure çalışan örnekleri veri bloğu</span><span class="sxs-lookup"><span data-stu-id="2f6a6-135">Burst tooAzure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="2f6a6-136">Öğretici: Azure HPC paketi ile karma küme ayarlayın</span><span class="sxs-lookup"><span data-stu-id="2f6a6-136">Tutorial: Set up a hybrid cluster with HPC Pack in Azure</span></span>](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [<span data-ttu-id="2f6a6-137">Azure'da Azure "veri bloğu" düğümleri tooan HPC paketi üstbilgi düğümü Ekle</span><span class="sxs-lookup"><span data-stu-id="2f6a6-137">Add Azure "burst" nodes tooan HPC Pack head node in Azure</span></span>](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a><span data-ttu-id="2f6a6-138">Azure Batch ile tümleştirme</span><span class="sxs-lookup"><span data-stu-id="2f6a6-138">Integrate with Azure Batch</span></span>
* [<span data-ttu-id="2f6a6-139">TooAzure HPC paketi ile toplu veri bloğu</span><span class="sxs-lookup"><span data-stu-id="2f6a6-139">Burst tooAzure Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="2f6a6-140">MPI iş yükleri için RDMA kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="2f6a6-140">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="2f6a6-141">HPC Pack toorun MPI uygulamaları ile Windows RDMA kümesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="2f6a6-141">Set up a Windows RDMA cluster with HPC Pack toorun MPI applications</span></span>](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

