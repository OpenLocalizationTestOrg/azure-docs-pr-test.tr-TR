---
title: "aaaLinux HPC paketi küme seçenekleri hello bulutta | Microsoft Docs"
description: "Microsoft HPC Pack toocreate seçeneklerle hakkında bilgi edinin ve bir Linux yüksek performanslı bilgi işlem (HPC) hello Azure bulut kümede yönetme"
services: virtual-machines-linux,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 60d093b466f44a0391815842c421c328e8c7a0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a><span data-ttu-id="23cdf-103">HPC Pack toocreate ile seçenekleri ve Azure Linux iş yükleri için bir HPC küme yönetme</span><span class="sxs-lookup"><span data-stu-id="23cdf-103">Options with HPC Pack toocreate and manage an HPC cluster in Azure for Linux workloads</span></span>
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

<span data-ttu-id="23cdf-104">Bu makalede seçenekleri toouse HPC Pack toorun Linux iş yükünü odaklanır.</span><span class="sxs-lookup"><span data-stu-id="23cdf-104">This article focuses on options toouse HPC Pack toorun Linux workloads.</span></span> <span data-ttu-id="23cdf-105">Ayrıca çalıştırmak için seçenek vardır [HPC paketi ile Windows HPC iş yüklerini](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="23cdf-105">There are also options for running [Windows HPC workloads with HPC Pack](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a><span data-ttu-id="23cdf-106">HPC Pack küme Azure Vm'lerde çalıştırın</span><span class="sxs-lookup"><span data-stu-id="23cdf-106">Run an HPC Pack cluster in Azure VMs</span></span>
### <a name="azure-templates"></a><span data-ttu-id="23cdf-107">Azure şablonları</span><span class="sxs-lookup"><span data-stu-id="23cdf-107">Azure templates</span></span>
* <span data-ttu-id="23cdf-108">(GitHub) [HPC Pack 2016 küme şablonları](https://github.com/MsHpcPack/HPCPack2016)</span><span class="sxs-lookup"><span data-stu-id="23cdf-108">(GitHub) [HPC Pack 2016 cluster templates](https://github.com/MsHpcPack/HPCPack2016)</span></span>
* <span data-ttu-id="23cdf-109">(Market) [Linux iş yükleri için HPC paketi küme](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span><span class="sxs-lookup"><span data-stu-id="23cdf-109">(Marketplace) [HPC Pack cluster for Linux workloads](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)</span></span>
* <span data-ttu-id="23cdf-110">(Hızlı Başlangıç) [Linux işlem düğümleri ile bir HPC kümesi oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span><span class="sxs-lookup"><span data-stu-id="23cdf-110">(Quickstart) [Create an HPC cluster with Linux compute nodes](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)</span></span>

### <a name="powershell-deployment-script"></a><span data-ttu-id="23cdf-111">PowerShell dağıtım komut dosyası</span><span class="sxs-lookup"><span data-stu-id="23cdf-111">PowerShell deployment script</span></span>
* [<span data-ttu-id="23cdf-112">HPC Pack Iaas dağıtım betiği hello ile Linux HPC küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="23cdf-112">Create a Linux HPC cluster with hello HPC Pack IaaS deployment script</span></span>](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a><span data-ttu-id="23cdf-113">Öğreticiler</span><span class="sxs-lookup"><span data-stu-id="23cdf-113">Tutorials</span></span>
* [<span data-ttu-id="23cdf-114">Öğretici: Azure HPC Pack kümesinde Linux işlem düğümlerine kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="23cdf-114">Tutorial: Get started with Linux compute nodes in an HPC Pack cluster in Azure</span></span>](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="23cdf-115">Öğretici: Çalıştır NAMD Microsoft HPC paketi ile Linux işlem düğümlerini Azure</span><span class="sxs-lookup"><span data-stu-id="23cdf-115">Tutorial: Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="23cdf-116">Öğretici: Azure Linux RDMA kümesinde Microsoft HPC paketi ile çalışma OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="23cdf-116">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="23cdf-117">Öğretici: Çalıştır yıldız-CCM + Linux RDMA üzerinde Microsoft HPC Pack ile Azure'da küme</span><span class="sxs-lookup"><span data-stu-id="23cdf-117">Tutorial: Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a><span data-ttu-id="23cdf-118">Küme yönetimi</span><span class="sxs-lookup"><span data-stu-id="23cdf-118">Cluster management</span></span>
* [<span data-ttu-id="23cdf-119">İşlerini tooan HPC Pack Azure kümesinde gönderme</span><span class="sxs-lookup"><span data-stu-id="23cdf-119">Submit jobs tooan HPC Pack cluster in Azure</span></span>](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="23cdf-120">HPC Pack iş yönetimi</span><span class="sxs-lookup"><span data-stu-id="23cdf-120">Job management in HPC Pack</span></span>](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a><span data-ttu-id="23cdf-121">MPI iş yükleri için RDMA kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="23cdf-121">Create RDMA clusters for MPI workloads</span></span>
* [<span data-ttu-id="23cdf-122">Öğretici: Azure Linux RDMA kümesinde Microsoft HPC paketi ile çalışma OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="23cdf-122">Tutorial: Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="23cdf-123">Bir Linux RDMA küme toorun MPI uygulama ayarlama</span><span class="sxs-lookup"><span data-stu-id="23cdf-123">Set up a Linux RDMA cluster toorun MPI applications</span></span>](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

