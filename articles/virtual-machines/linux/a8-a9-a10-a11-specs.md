---
title: "aaaAbout işlem yoğunluklu Linux VM'ler | Microsoft Docs"
description: "Arka plan bilgileri ve Linux VM'ler için hello H-serisi ve A8, A9, A10 ve A11 işlem yoğunluklu boyutlarını kullanarak dikkat edilmesi gereken noktalar"
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
ms.openlocfilehash: 37636840a3f809ac19354a5a7993257216f675f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a><span data-ttu-id="58459-103">Y-serisi ve işlem yoğunluklu A-series VM'ler hakkında için Linux</span><span class="sxs-lookup"><span data-stu-id="58459-103">About H-series and compute-intensive A-series VMs for Linux</span></span>
<span data-ttu-id="58459-104">Arka plan bilgileri işte ve kullanmak için bazı noktalar yeni Azure H-serisi hello ve hello önceki A8, A9, A10 ve A11 boyutları olarak da bilinen *işlem yoğunluklu* örnekleri.</span><span class="sxs-lookup"><span data-stu-id="58459-104">Here is background information and some considerations for using hello newer Azure H-series and hello earlier A8, A9, A10, and A11 sizes, also known as *compute-intensive* instances.</span></span> <span data-ttu-id="58459-105">Bu makalede, bu boyutlar Linux VM'ler için kullanımı üzerine odaklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="58459-105">This article focuses on using these sizes for Linux VMs.</span></span> <span data-ttu-id="58459-106">Bunlar için de kullanabilirsiniz [Windows VM'ler](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58459-106">You can also use them for [Windows VMs](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="58459-107">Temel özellikleri, depolama kapasitesi ve disk Ayrıntılar için bkz: [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58459-107">For basic specs, storage capacities, and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a><span data-ttu-id="58459-108">Erişim toohello RDMA ağ</span><span class="sxs-lookup"><span data-stu-id="58459-108">Access toohello RDMA network</span></span>
<span data-ttu-id="58459-109">Desteklenen Linux HPC dağıtımları ve bir desteklenen MPI uygulama tootake avantajlarından hello Azure RDMA ağ aşağıdaki hello birini çalıştıran RDMA özellikli Linux VM'ler kümeleri oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58459-109">You can create clusters of RDMA-capable Linux VMs that run one of hello following supported Linux HPC distributions and a supported MPI implementation tootake advantage of hello Azure RDMA network.</span></span> <span data-ttu-id="58459-110">Bkz: [Linux RDMA küme toorun MPI uygulamalar ayarlamak](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) dağıtım seçenekleri ve örnek yapılandırma adımları için.</span><span class="sxs-lookup"><span data-stu-id="58459-110">See [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) for deployment options and sample configuration steps.</span></span>

* <span data-ttu-id="58459-111">**Dağıtımları** - VMs gelen RDMA özellikli SUSE Linux Enterprise Server (SLES) dağıtmanız gerekir veya yanlış Wave yazılım (önceki adıyla OpenLogic) CentOS tabanlı HPC görüntülerinde hello Azure Marketi.</span><span class="sxs-lookup"><span data-stu-id="58459-111">**Distributions** - You must deploy VMs from RDMA-capable SUSE Linux Enterprise Server (SLES) or Rogue Wave Software (formerly OpenLogic) CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="58459-112">Merhaba aşağıdaki Market görüntülerini RDMA bağlantısı destekler:</span><span class="sxs-lookup"><span data-stu-id="58459-112">hello following Marketplace images support RDMA connectivity:</span></span>
  
    * <span data-ttu-id="58459-113">SLES 12 SP1 HPC, SLES 12 için SP1 için HPC (Premium)</span><span class="sxs-lookup"><span data-stu-id="58459-113">SLES 12 SP1 for HPC, SLES 12 SP1 for HPC (Premium)</span></span>
    
    * <span data-ttu-id="58459-114">CentOS tabanlı 7.1 HPC, CentOS tabanlı 6.5 HPC</span><span class="sxs-lookup"><span data-stu-id="58459-114">CentOS-based 7.1 HPC, CentOS-based 6.5 HPC</span></span>  
 
        > [!NOTE]
        > <span data-ttu-id="58459-115">Y-serisi VM'ler için HPC görüntüsü için SLES 12 SP1 ya da CentOS tabanlı 7.1 HPC görüntü öneririz.</span><span class="sxs-lookup"><span data-stu-id="58459-115">For H-series VMs, we recommend either a SLES 12 SP1 for HPC image or CentOS-based 7.1 HPC image.</span></span>
        >
        > <span data-ttu-id="58459-116">Merhaba CentOS tabanlı HPC görüntülerinde hello çekirdek güncelleştirmeleri devre dışı **yum** yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="58459-116">On hello CentOS-based HPC images, kernel updates are disabled in hello **yum** configuration file.</span></span> <span data-ttu-id="58459-117">Hello Linux RDMA sürücüleri RPM paket olarak dağıtılır ve hello çekirdek güncelleştirdiyseniz sürücü güncelleştirmelerini çalışmayabilir nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="58459-117">This is because hello Linux RDMA drivers are distributed as an RPM package, and driver updates might not work if hello kernel is updated.</span></span>
        > 
        > 
* <span data-ttu-id="58459-118">**MPI** -Intel MPI kitaplığının 5.x</span><span class="sxs-lookup"><span data-stu-id="58459-118">**MPI** - Intel MPI Library 5.x</span></span>
  
    <span data-ttu-id="58459-119">Merhaba Market görüntüsü bağlı olarak, ayrı lisans, yükleme, seçtiğiniz veya Intel MPI yapılandırmasını, aşağıdaki gibi gerekli olabilir:</span><span class="sxs-lookup"><span data-stu-id="58459-119">Depending on hello Marketplace image you choose, separate licensing, installation, or configuration of Intel MPI may be needed, as follows:</span></span> 
  
  * <span data-ttu-id="58459-120">**SLES 12 SP1 HPC görüntü için** -Intel MPI paketleri hello VM üzerinde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="58459-120">**SLES 12 SP1 for HPC image** - Intel MPI packages are distributed on hello VM.</span></span> <span data-ttu-id="58459-121">Merhaba aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="58459-121">Install by running hello following command:</span></span>

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * <span data-ttu-id="58459-122">**CentOS tabanlı HPC görüntüler** -Intel MPI 5.1 zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="58459-122">**CentOS-based HPC images**  - Intel MPI 5.1 is already installed.</span></span>  
    
    <span data-ttu-id="58459-123">Ek sistem yapılandırması gerekli toorun MPI işlerini kümelenmiş sanal makineleri üzerinde değil.</span><span class="sxs-lookup"><span data-stu-id="58459-123">Additional system configuration is needed toorun MPI jobs on clustered VMs.</span></span> <span data-ttu-id="58459-124">Örneğin, VM'lerin bir kümede tooestablish ihtiyacınız hello arasında güven işlem düğümlerini.</span><span class="sxs-lookup"><span data-stu-id="58459-124">For example, on a cluster of VMs, you need tooestablish trust among hello compute nodes.</span></span> <span data-ttu-id="58459-125">Tipik ayarları için bkz: [Linux RDMA küme toorun MPI uygulamalar ayarlamak](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58459-125">For typical settings, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="considerations-for-hpc-pack-and-linux"></a><span data-ttu-id="58459-126">HPC Pack ve Linux değerlendirmeleri</span><span class="sxs-lookup"><span data-stu-id="58459-126">Considerations for HPC Pack and Linux</span></span>
<span data-ttu-id="58459-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft'un ücretsiz HPC küme ve iş yönetimi çözümü toouse hello işlem yoğunluklu örnekler Linux sizin için bir seçenek sunar.</span><span class="sxs-lookup"><span data-stu-id="58459-127">[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, provides one option for you toouse hello compute-intensive instances with Linux.</span></span> <span data-ttu-id="58459-128">HPC Pack Merhaba en son sürümleri toorun üzerinde işlem düğümlerini Azure Vm'leri, bir Windows Server baş düğümü tarafından yönetilen dağıtılmış birkaç Linux dağıtımları destekler.</span><span class="sxs-lookup"><span data-stu-id="58459-128">hello latest releases of HPC Pack support several Linux distributions toorun on compute nodes deployed in Azure VMs, managed by a Windows Server head node.</span></span> <span data-ttu-id="58459-129">Intel MPI çalıştıran RDMA özellikli Linux işlem düğümleri ile HPC Pack zamanlayabilir ve bu erişim hello RDMA ağ Linux MPI uygulamaları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="58459-129">With RDMA-capable Linux compute nodes running Intel MPI, HPC Pack can schedule and run Linux MPI applications that access hello RDMA network.</span></span> <span data-ttu-id="58459-130">başlatıldı, tooget bkz [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58459-130">tooget started, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="network-topology-considerations"></a><span data-ttu-id="58459-131">Ağ topolojisi hakkında önemli noktalar</span><span class="sxs-lookup"><span data-stu-id="58459-131">Network topology considerations</span></span>
* <span data-ttu-id="58459-132">RDMA özellikli Linux VM'ler üzerinde Azure, Eth1 RDMA ağ trafiği için ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="58459-132">On RDMA-enabled Linux VMs in Azure, Eth1 is reserved for RDMA network traffic.</span></span> <span data-ttu-id="58459-133">Herhangi bir Eth1 ayarı veya herhangi bir bilgi toothis ağ başvuran hello yapılandırma dosyasında değiştirmeyin.</span><span class="sxs-lookup"><span data-stu-id="58459-133">Do not change any Eth1 settings or any information in hello configuration file referring toothis network.</span></span> <span data-ttu-id="58459-134">Eth0 normal Azure ağ trafiği için ayrılır.</span><span class="sxs-lookup"><span data-stu-id="58459-134">Eth0 is reserved for regular Azure network traffic.</span></span>
* <span data-ttu-id="58459-135">Azure'da, IP üzerinden InfiniBand (IB) desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="58459-135">In Azure, IP over InfiniBand (IB) is not supported.</span></span> <span data-ttu-id="58459-136">Yalnızca IB üzerinden RDMA desteklenir.</span><span class="sxs-lookup"><span data-stu-id="58459-136">Only RDMA over IB is supported.</span></span>



## <a name="next-steps"></a><span data-ttu-id="58459-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="58459-137">Next steps</span></span>
* <span data-ttu-id="58459-138">Kullanılabilirlik ve hello işlem yoğunluklu boyutlarını fiyatlandırma hakkında daha fazla ayrıntı için bkz: [sanal makineler fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span><span class="sxs-lookup"><span data-stu-id="58459-138">For details about availability and pricing of hello compute-intensive sizes, see [Virtual Machines pricing](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).</span></span>
* <span data-ttu-id="58459-139">Depolama kapasitesi ve disk Ayrıntılar için bkz: [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58459-139">For storage capacities and disk details, see [Sizes for virtual machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="58459-140">dağıtma ve RDMA Linux üzerinde işlem yoğunluklu boyutları kullanarak başlatılan tooget bkz [Linux RDMA küme toorun MPI uygulamalar ayarlamak](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="58459-140">tooget started deploying and using compute-intensive sizes with RDMA on Linux, see [Set up a Linux RDMA cluster toorun MPI applications](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

