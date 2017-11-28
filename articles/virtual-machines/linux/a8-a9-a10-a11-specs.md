---
title: "Linux işlem yoğunluklu VM'ler hakkında | Microsoft Docs"
description: "Arka plan bilgileri ve Linux VM'ler için H-serisi ve A8, A9, A10 ve A11 işlem yoğunluklu boyutlarını kullanarak dikkat edilmesi gereken noktalar"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 16cf6e2d-f401-4b22-af8c-9a337179f5f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a2307f7055966ec7146b5da0b4daf1ad469abe2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="efb8e-103">Y-serisi ve işlem yoğunluklu A-series VM'ler hakkında için Linux</span><span class="sxs-lookup"><span data-stu-id="efb8e-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="efb8e-104">Arka plan bilgileri ve daha yeni Azure H serisi ve önceki A8, A9, A10 ve A11 boyutları olarak da bilinen kullanmak için bazı noktalar işte *işlem yoğunluklu* örnekleri.</span><span class="sxs-lookup"><span data-stu-id="efb8e-104">Here is background information and some considerations for using the newer Azure H-series and the earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="efb8e-105">Bu makalede, bu boyutlar Linux VM'ler için kullanımı üzerine odaklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="efb8e-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="efb8e-106">Bunlar için de kullanabilirsiniz [Windows VM'ler](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="efb8e-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="efb8e-107">Temel özellikleri, depolama kapasitesi ve disk Ayrıntılar için bkz: [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="efb8e-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-to-the-rdma-network"></a><span data-ttu-id="efb8e-108">RDMA ağ erişimi</span><span class="sxs-lookup"><span data-stu-id="efb8e-108">Access to the RDMA network</span></span>
<span data-ttu-id="efb8e-109">RDMA özellikli Linux çalışma aşağıdakilerden birini Linux HPC dağıtımları ve Azure RDMA ağ yararlanmak için desteklenen bir MPI uygulama desteklenen VM'lerin kümeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="efb8e-109">You can create clusters of RDMA-capable Linux VMs that run one of the following supported Linux HPC distributions and a supported MPI implementation to take advantage of the Azure RDMA network.</span></span> <span data-ttu-id="efb8e-110">Bkz: [MPI uygulamaları çalıştırmak için Linux RDMA küme ayarlama](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) dağıtım seçenekleri ve örnek yapılandırma adımları için.</span><span class="sxs-lookup"><span data-stu-id="efb8e-110">See [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="efb8e-111">**Dağıtımları** -Azure Marketi RDMA özellikli SUSE Linux Enterprise Server (SLES) ya da yanlış Wave yazılım (önceki adıyla OpenLogic) CentOS tabanlı HPC görüntülerden VM'ler dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="efb8e-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="efb8e-112">Aşağıdaki Market görüntülerini RDMA bağlantısı destekler:</span><span class="sxs-lookup"><span data-stu-id="efb8e-112">The following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="efb8e-113">SLES 12 SP1 HPC, SLES 12 için SP1 için HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="efb8e-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="efb8e-114">CentOS tabanlı 7.1 HPC, CentOS tabanlı 6.5 HPC</span><span class="sxs-lookup"><span data-stu-id="efb8e-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="efb8e-115">Y-serisi VM'ler için HPC görüntüsü için SLES 12 SP1 ya da CentOS tabanlı 7.1 HPC görüntü öneririz.</span><span class="sxs-lookup"><span data-stu-id="efb8e-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="efb8e-116">CentOS tabanlı HPC görüntülerinde çekirdek güncelleştirmeleri de devre dışı **yum** yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="efb8e-116">On the CentOS-based HPC images, kernel updates are disabled in the **yum** configuration file.</span></span> <span data-ttu-id="efb8e-117">Linux RDMA sürücüleri RPM paket olarak dağıtılır ve çekirdek güncelleştirdiyseniz sürücü güncelleştirmelerini çalışmayabilir nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="efb8e-117">This is because the Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if the kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="efb8e-118">**MPI** -Intel MPI kitaplığının 5.x</span><span class="sxs-lookup"><span data-stu-id="efb8e-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="efb8e-119">Market görüntüsü bağlı olarak, ayrı lisans, yükleme, seçtiğiniz veya Intel MPI yapılandırmasını, aşağıdaki gibi gerekli olabilir:</span><span class="sxs-lookup"><span data-stu-id="efb8e-119">Depending on the Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="efb8e-120">**SLES 12 SP1 HPC görüntü için** -Intel MPI paketleri VM dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="efb8e-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on the VM.</span></span> <span data-ttu-id="efb8e-121">Aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="efb8e-121">Install by running the following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="efb8e-122">**CentOS tabanlı HPC görüntüler** -Intel MPI 5.1 zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="efb8e-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="efb8e-123">Ek sistem yapılandırması, kümelenmiş sanal makinelerin MPI işlerini çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="efb8e-123">Additional system configuration is needed to run MPI jobs on clustered VMs.</span></span> <span data-ttu-id="efb8e-124">Örneğin, VM'lerin bir kümede işlem düğümleri arasında güven oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="efb8e-124">For example, on a cluster of VMs, you need to establish trust among the compute nodes.</span></span> <span data-ttu-id="efb8e-125">Tipik ayarları için bkz: [MPI uygulamaları çalıştırmak için Linux RDMA küme ayarlama](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="efb8e-125">For typical settings, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="efb8e-126">HPC Pack ve Linux değerlendirmeleri</span><span class="sxs-lookup"><span data-stu-id="efb8e-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="efb8e-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft'un ücretsiz HPC küme ve iş yönetimi çözümü, işlem yoğunluklu örnekler Linux ile kullanmanız için bir seçenek sunar.</span><span class="sxs-lookup"><span data-stu-id="efb8e-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you to use the compute-intensive instances with Linux.</span></span> <span data-ttu-id="efb8e-128">HPC Pack Destek'ın en son sürümlerine işlem bir Windows Server baş düğümü tarafından yönetilen Azure vm'lerinde dağıtılan düğümleri üzerinde çalışmak için birkaç Linux dağıtımları.</span><span class="sxs-lookup"><span data-stu-id="efb8e-128">The latest releases of HPC Pack support several Linux distributions to run on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="efb8e-129">Intel MPI çalıştıran RDMA özellikli Linux işlem düğümleri ile HPC Pack zamanlayabilir ve Linux MPI RDMA ağ erişim uygulamaları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="efb8e-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access the RDMA network.</span></span> <span data-ttu-id="efb8e-130">Başlamak için bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="efb8e-130">To get started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="efb8e-131">Ağ topolojisi hakkında önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="efb8e-131">Network topology considerations</span></span>
* <span data-ttu-id="efb8e-132">RDMA özellikli Linux VM'ler üzerinde Azure, Eth1 RDMA ağ trafiği için ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="efb8e-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="efb8e-133">Herhangi bir Eth1 ayarı veya bu ağa başvuran yapılandırma dosyasında herhangi bir bilgiyi değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="efb8e-133">Do not change any Eth1 settings or any information in the configuration file referring to this network.</span></span> <span data-ttu-id="efb8e-134">Eth0 normal Azure ağ trafiği için ayrılır.</span><span class="sxs-lookup"><span data-stu-id="efb8e-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="efb8e-135">Azure'da, IP üzerinden InfiniBand (IB) desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="efb8e-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="efb8e-136">Yalnızca IB üzerinden RDMA desteklenir.</span><span class="sxs-lookup"><span data-stu-id="efb8e-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="efb8e-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="efb8e-137">Next steps</span></span>
* <span data-ttu-id="efb8e-138">Kullanılabilirlik ve işlem yoğunluklu boyutlarını fiyatlandırma hakkında daha fazla ayrıntı için bkz: [sanal makineler fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="efb8e-138">For details about availability and pricing of the compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="efb8e-139">Depolama kapasitesi ve disk Ayrıntılar için bkz: [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="efb8e-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="efb8e-140">Dağıtma ve RDMA Linux üzerinde işlem yoğunluklu boyutları kullanarak başlamak için bkz: [MPI uygulamaları çalıştırmak için Linux RDMA küme ayarlama](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="efb8e-140">To get started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

