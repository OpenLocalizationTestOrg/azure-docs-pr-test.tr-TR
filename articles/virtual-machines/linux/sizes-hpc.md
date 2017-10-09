---
title: "aaaAzure Linux VM boyutları - HPC | Microsoft Docs"
description: "Farklı boyutlarda Hello Linux yüksek performanslı bilgi işlem azure'da sanal makineler için kullanılabilir listeler."
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
ms.openlocfilehash: 0b02ee592902ff8097a71898faea1ac17a947d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-linux-vm-sizes"></a><span data-ttu-id="3684c-103">Yüksek performanslı işlem Linux VM boyutları</span><span class="sxs-lookup"><span data-stu-id="3684c-103">High performance compute Linux VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="3684c-104">RDMA özellikli örnekleri</span><span class="sxs-lookup"><span data-stu-id="3684c-104">RDMA-capable instances</span></span>
<span data-ttu-id="3684c-105">Bir alt kümesini hello işlem yoğunluklu örnekler (H16r, H16mr, A8 ve A9) doğrudan uzak bellek erişimi (RDMA) bağlantısı için bir ağ arabirimi özelliği.</span><span class="sxs-lookup"><span data-stu-id="3684c-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="3684c-106">Bu ayrıca toohello standart Azure ağ arabirimi kullanılabilir tooother VM boyutları arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="3684c-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="3684c-107">Bu arabirim hello RDMA özellikli örnekleri toocommunicate H16r ve H16mr sanal makineler için FDR hızlarını ve A8 ve A9 sanal makineler için QDR hızlarını işletim bir InfiniBand ağ üzerinden verir.</span><span class="sxs-lookup"><span data-stu-id="3684c-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="3684c-108">RDMA yeteneklere hello ölçeklenebilirlik ve ileti geçirme arabirimi (MPI) uygulamaların performansını artırabilir.</span><span class="sxs-lookup"><span data-stu-id="3684c-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="3684c-109">RDMA özellikli Linux VM'ler tooaccess Azure RDMA ağ hello için gereksinimleri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3684c-109">Following are requirements for RDMA-capable Linux VMs tooaccess hello Azure RDMA network:</span></span>
 
* <span data-ttu-id="3684c-110">**Dağıtımları** - VMs gelen RDMA özellikli SUSE Linux Enterprise Server (SLES) dağıtmanız gerekir veya yanlış Wave yazılım (önceki adıyla OpenLogic) CentOS tabanlı HPC görüntülerinde hello Azure Marketi.</span><span class="sxs-lookup"><span data-stu-id="3684c-110">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="3684c-111">Merhaba aşağıdaki Market görüntülerini RDMA bağlantısı destekler:</span><span class="sxs-lookup"><span data-stu-id="3684c-111">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="3684c-112">SLES 12 SP1 HPC veya SLES 12 için SP1 için HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="3684c-112">SLES 12 SP1 for HPC, or SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="3684c-113">CentOS tabanlı 7.3 HPC, CentOS tabanlı 7.1 HPC, CentOS tabanlı 6.8 HPC veya CentOS tabanlı 6.5 HPC</span><span class="sxs-lookup"><span data-stu-id="3684c-113">CentOS-based 7.3 HPC, CentOS-based 7.1 HPC, CentOS-based 6.8 HPC, or CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="3684c-114">Y-serisi VM'ler için HPC görüntüsü için SLES 12 SP1 veya CentOS tabanlı 7.1 veya sonraki HPC görüntü öneririz.</span><span class="sxs-lookup"><span data-stu-id="3684c-114">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 or later HPC image.</span></span>
        >
        > <span data-ttu-id="3684c-115">Merhaba CentOS tabanlı HPC görüntülerinde hello çekirdek güncelleştirmeleri devre dışı **yum** yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="3684c-115">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="3684c-116">Hello Linux RDMA sürücüleri RPM paket olarak dağıtılır ve hello çekirdek güncelleştirdiyseniz sürücü güncelleştirmelerini çalışmayabilir nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="3684c-116">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="3684c-117">**MPI** -Intel MPI kitaplığının 5.x</span><span class="sxs-lookup"><span data-stu-id="3684c-117">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="3684c-118">Merhaba Market görüntüsü bağlı olarak, ayrı lisans, yükleme, seçtiğiniz veya Intel MPI yapılandırmasını, aşağıdaki gibi gerekli olabilir:</span><span class="sxs-lookup"><span data-stu-id="3684c-118">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="3684c-119">**SLES 12 SP1 HPC görüntü için** -Intel MPI paketleri hello VM üzerinde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="3684c-119">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="3684c-120">Merhaba aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="3684c-120">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="3684c-121">**CentOS tabanlı HPC görüntüler** -Intel MPI 5.1 zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="3684c-121">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="3684c-122">Ek sistem yapılandırması gerekli toorun MPI işlerini kümelenmiş sanal makineleri üzerinde değil.</span><span class="sxs-lookup"><span data-stu-id="3684c-122">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="3684c-123">Örneğin, VM'lerin bir kümede tooestablish ihtiyacınız hello arasında güven işlem düğümlerini.</span><span class="sxs-lookup"><span data-stu-id="3684c-123">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="3684c-124">Tipik ayarları için bkz: [bir Linux RDMA küme toorun MPI uygulama ayarlama](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3684c-124">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

### <a name="network-topology-considerations"></a><span data-ttu-id="3684c-125">Ağ topolojisi hakkında önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="3684c-125">Network topology considerations</span></span>
* <span data-ttu-id="3684c-126">RDMA özellikli Linux VM'ler üzerinde Azure, Eth1 RDMA ağ trafiği için ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="3684c-126">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="3684c-127">Herhangi bir Eth1 ayarı veya herhangi bir bilgi toothis ağ başvuran hello yapılandırma dosyasında değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="3684c-127">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="3684c-128">Eth0 normal Azure ağ trafiği için ayrılır.</span><span class="sxs-lookup"><span data-stu-id="3684c-128">Eth0 is reserved for regular Azure network traffic.</span></span>

* <span data-ttu-id="3684c-129">Azure'da, IP üzerinden InfiniBand (IB) desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="3684c-129">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="3684c-130">Yalnızca IB üzerinden RDMA desteklenir.</span><span class="sxs-lookup"><span data-stu-id="3684c-130">Only RDMA over IB is supported.</span></span>

## <a name="using-hpc-pack"></a><span data-ttu-id="3684c-131">HPC Pack kullanma</span><span class="sxs-lookup"><span data-stu-id="3684c-131">Using HPC Pack</span></span>
<span data-ttu-id="3684c-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft'un ücretsiz HPC küme ve iş yönetimi, bir çözümdür, Linux toouse hello işlem yoğunluklu örnekler için bir seçenek.</span><span class="sxs-lookup"><span data-stu-id="3684c-132">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="3684c-133">HPC Pack Merhaba en son sürümleri toorun üzerinde işlem düğümlerini Azure Vm'leri, bir Windows Server baş düğümü tarafından yönetilen dağıtılmış birkaç Linux dağıtımları destekler.</span><span class="sxs-lookup"><span data-stu-id="3684c-133">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="3684c-134">Intel MPI çalıştıran RDMA özellikli Linux işlem düğümleri ile HPC Pack zamanlayabilir ve bu erişim hello RDMA ağ Linux MPI uygulamaları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3684c-134">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="3684c-135">Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3684c-135">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="other-sizes"></a><span data-ttu-id="3684c-136">Diğer boyutlara</span><span class="sxs-lookup"><span data-stu-id="3684c-136">Other sizes</span></span>
- [<span data-ttu-id="3684c-137">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="3684c-137">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="3684c-138">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="3684c-138">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="3684c-139">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="3684c-139">Memory optimized</span></span>](sizes-memory.md)
- [<span data-ttu-id="3684c-140">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="3684c-140">Storage optimized</span></span>](sizes-storage.md)
- [<span data-ttu-id="3684c-141">GPU</span><span class="sxs-lookup"><span data-stu-id="3684c-141">GPU</span></span>](../windows/sizes-gpu.md)


## <a name="next-steps"></a><span data-ttu-id="3684c-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3684c-142">Next steps</span></span>

- <span data-ttu-id="3684c-143">dağıtma ve RDMA Linux üzerinde işlem yoğunluklu boyutları kullanarak başlatılan tooget bkz [Linux RDMA küme toorun MPI uygulamalar ayarlamak](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3684c-143">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="3684c-144">Hakkında daha fazla bilgi [Azure işlem birimleri (ACU)](acu.md) Azure SKU'ları üzerinde işlem performans karşılaştırmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="3684c-144">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




