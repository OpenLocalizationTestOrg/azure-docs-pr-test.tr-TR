---
title: "Azure Linux VM boyutları - HPC | Microsoft Docs"
description: "Linux yüksek performanslı bilgi işlem azure'da sanal makineler için kullanılabilir farklı boyutlarını listeler."
services: virtual-machines-linux
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: b7a3844ce86b4efac8a4fc3c2540e7b6460873a2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="a80e6-103">Yüksek performanslı işlem Linux VM boyutları</span><span class="sxs-lookup"><span data-stu-id="a80e6-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="a80e6-104">RDMA özellikli örnekleri</span><span class="sxs-lookup"><span data-stu-id="a80e6-104">RDMA-capable instances</span></span>
<span data-ttu-id="a80e6-105">Bir alt işlem yoğunluklu örnekler (H16r, H16mr, A8 ve A9), doğrudan uzak bellek erişimi (RDMA) bağlantısı için bir ağ arabirimi özelliği.</span><span class="sxs-lookup"><span data-stu-id="a80e6-105">A subset of the compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="a80e6-106">Diğer VM boyutları için kullanılabilir standart Azure ağ arabirimi yanı sıra bu arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="a80e6-106">This interface is in addition to the standard Azure network interface available to other VM sizes.</span></span> 
  
<span data-ttu-id="a80e6-107">Bu arabirim H16r ve H16mr sanal makineler için FDR hızlarını ve A8 ve A9 sanal makineler için QDR hızlarını işletim bir InfiniBand ağ üzerinden iletişim kurmak RDMA özellikli örneklerini verir.</span><span class="sxs-lookup"><span data-stu-id="a80e6-107">This interface allows the RDMA-capable instances to communicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="a80e6-108">RDMA yeteneklere ölçeklenebilirlik ve ileti geçirme arabirimi (MPI) uygulamaların performansını artırabilir.</span><span class="sxs-lookup"><span data-stu-id="a80e6-108">These RDMA capabilities can boost the scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="a80e6-109">Azure RDMA ağ erişmek RDMA özellikli Linux VM'ler için gereksinimleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a80e6-109">Following are requirements for RDMA-capable Linux VMs to access the Azure RDMA network:</span></span>
 
* <span data-ttu-id="a80e6-110">**Dağıtımları** -Azure Marketi RDMA özellikli SUSE Linux Enterprise Server (SLES) ya da yanlış Wave yazılım (önceki adıyla OpenLogic) CentOS tabanlı HPC görüntülerden VM'ler dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a80e6-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="a80e6-111">Aşağıdaki Market görüntülerini RDMA bağlantısı destekler:</span><span class="sxs-lookup"><span data-stu-id="a80e6-111">The following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="a80e6-112">SLES 12 SP1 HPC veya SLES 12 için SP1 için HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="a80e6-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="a80e6-113">CentOS tabanlı 7.3 HPC, CentOS tabanlı 7.1 HPC, CentOS tabanlı 6.8 HPC veya CentOS tabanlı 6.5 HPC</span><span class="sxs-lookup"><span data-stu-id="a80e6-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="a80e6-114">Y-serisi VM'ler için HPC görüntüsü için SLES 12 SP1 veya CentOS tabanlı 7.1 veya sonraki HPC görüntü öneririz.</span><span class="sxs-lookup"><span data-stu-id="a80e6-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="a80e6-115">CentOS tabanlı HPC görüntülerinde çekirdek güncelleştirmeleri de devre dışı **yum** yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="a80e6-115">On the CentOS-based HPC images, kernel updates are disabled in the **yum** configuration file.</span></span> <span data-ttu-id="a80e6-116">Linux RDMA sürücüleri RPM paket olarak dağıtılır ve çekirdek güncelleştirdiyseniz sürücü güncelleştirmelerini çalışmayabilir nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="a80e6-116">This is because the Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if the kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="a80e6-117">**MPI** -Intel MPI kitaplığının 5.x</span><span class="sxs-lookup"><span data-stu-id="a80e6-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="a80e6-118">Market görüntüsü bağlı olarak, ayrı lisans, yükleme, seçtiğiniz veya Intel MPI yapılandırmasını, aşağıdaki gibi gerekli olabilir:</span><span class="sxs-lookup"><span data-stu-id="a80e6-118">Depending on the Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="a80e6-119">**SLES 12 SP1 HPC görüntü için** -Intel MPI paketleri VM dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="a80e6-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on the VM.</span></span> <span data-ttu-id="a80e6-120">Aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="a80e6-120">Install by running the following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="a80e6-121">**CentOS tabanlı HPC görüntüler** -Intel MPI 5.1 zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="a80e6-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="a80e6-122">Ek sistem yapılandırması, kümelenmiş sanal makinelerin MPI işlerini çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a80e6-122">Additional system configuration is needed to run MPI jobs on clustered VMs.</span></span> <span data-ttu-id="a80e6-123">Örneğin, VM'lerin bir kümede işlem düğümleri arasında güven oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a80e6-123">For example, on a cluster of VMs, you need to establish trust among the compute nodes.</span></span> <span data-ttu-id="a80e6-124">Tipik ayarları için bkz: [MPI uygulamaları çalıştırmak için Linux RDMA küme ayarlama](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="a80e6-124">For typical settings, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="a80e6-125">Ağ topolojisi hakkında önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="a80e6-125">Network topology considerations</span></span>
* <span data-ttu-id="a80e6-126">RDMA özellikli Linux VM'ler üzerinde Azure, Eth1 RDMA ağ trafiği için ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="a80e6-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="a80e6-127">Herhangi bir Eth1 ayarı veya bu ağa başvuran yapılandırma dosyasında herhangi bir bilgiyi değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="a80e6-127">Do not change any Eth1 settings or any information in the configuration file referring to this network.</span></span> <span data-ttu-id="a80e6-128">Eth0 normal Azure ağ trafiği için ayrılır.</span><span class="sxs-lookup"><span data-stu-id="a80e6-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="a80e6-129">Azure'da, IP üzerinden InfiniBand (IB) desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="a80e6-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="a80e6-130">Yalnızca IB üzerinden RDMA desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a80e6-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="a80e6-131">HPC Pack kullanma</span><span class="sxs-lookup"><span data-stu-id="a80e6-131">Using HPC Pack</span></span>
<span data-ttu-id="a80e6-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft'un ücretsiz HPC küme ve iş yönetimi çözümü, işlem yoğunluklu örnekler Linux ile kullanmanız için bir seçenek değil.</span><span class="sxs-lookup"><span data-stu-id="a80e6-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you to use the compute-intensive instances with Linux.</span></span> <span data-ttu-id="a80e6-133">HPC Pack Destek'ın en son sürümlerine işlem bir Windows Server baş düğümü tarafından yönetilen Azure vm'lerinde dağıtılan düğümleri üzerinde çalışmak için birkaç Linux dağıtımları.</span><span class="sxs-lookup"><span data-stu-id="a80e6-133">The latest releases of HPC Pack support several Linux distributions to run on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="a80e6-134">Intel MPI çalıştıran RDMA özellikli Linux işlem düğümleri ile HPC Pack zamanlayabilir ve Linux MPI RDMA ağ erişim uygulamaları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a80e6-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access the RDMA network.</span></span> <span data-ttu-id="a80e6-135">Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a80e6-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="a80e6-136">Diğer boyutlara</span><span class="sxs-lookup"><span data-stu-id="a80e6-136">Other sizes</span></span>
- [<span data-ttu-id="a80e6-137">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="a80e6-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="a80e6-138">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="a80e6-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="a80e6-139">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="a80e6-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="a80e6-140">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="a80e6-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="a80e6-141">GPU</span><span class="sxs-lookup"><span data-stu-id="a80e6-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="a80e6-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a80e6-142">Next steps</span></span>

- <span data-ttu-id="a80e6-143">Dağıtma ve RDMA Linux üzerinde işlem yoğunluklu boyutları kullanarak başlamak için bkz: [MPI uygulamaları çalıştırmak için Linux RDMA küme ayarlama](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a80e6-143">To get started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster to run MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="a80e6-144">Hakkında daha fazla bilgi [Azure işlem birimleri (ACU)](acu.md) Azure SKU'ları üzerinde işlem performans karşılaştırmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a80e6-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




