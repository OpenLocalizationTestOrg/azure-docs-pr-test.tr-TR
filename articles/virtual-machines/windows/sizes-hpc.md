---
title: "aaaAzure Windows VM boyutları - HPC | Microsoft Docs"
description: "Farklı boyutlarda Hello Windows yüksek performanslı bilgi işlem azure'da sanal makineler için kullanılabilir listeler."
services: virtual-machines-windows
documentationcenter: 
author: jonbeck7
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/28/2017
ms.author: jonbeck
ms.openlocfilehash: 092bc32cfe048f439ad833911bef4ed17eda7977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-compute-vm-sizes"></a><span data-ttu-id="1e373-103">Yüksek performanslı bilgi işlem VM boyutları</span><span class="sxs-lookup"><span data-stu-id="1e373-103">High performance compute VM sizes</span></span>

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a><span data-ttu-id="1e373-104">RDMA özellikli örnekleri</span><span class="sxs-lookup"><span data-stu-id="1e373-104">RDMA-capable instances</span></span>
<span data-ttu-id="1e373-105">Bir alt kümesini hello işlem yoğunluklu örnekler (H16r, H16mr, A8 ve A9) doğrudan uzak bellek erişimi (RDMA) bağlantısı için bir ağ arabirimi özelliği.</span><span class="sxs-lookup"><span data-stu-id="1e373-105">A subset of hello compute-intensive instances (H16r, H16mr, A8, and A9) feature a network interface for remote direct memory access (RDMA) connectivity.</span></span> <span data-ttu-id="1e373-106">Bu ayrıca toohello standart Azure ağ arabirimi kullanılabilir tooother VM boyutları arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="1e373-106">This interface is in addition toohello standard Azure network interface available tooother VM sizes.</span></span> 
  
<span data-ttu-id="1e373-107">Bu arabirim hello RDMA özellikli örnekleri toocommunicate H16r ve H16mr sanal makineler için FDR hızlarını ve A8 ve A9 sanal makineler için QDR hızlarını işletim bir InfiniBand ağ üzerinden verir.</span><span class="sxs-lookup"><span data-stu-id="1e373-107">This interface allows hello RDMA-capable instances toocommunicate over an InfiniBand network, operating at FDR rates for H16r and H16mr virtual machines, and QDR rates for A8 and A9 virtual machines.</span></span> <span data-ttu-id="1e373-108">RDMA yeteneklere hello ölçeklenebilirlik ve ileti geçirme arabirimi (MPI) uygulamaların performansını artırabilir.</span><span class="sxs-lookup"><span data-stu-id="1e373-108">These RDMA capabilities can boost hello scalability and performance of Message Passing Interface (MPI) applications.</span></span>

<span data-ttu-id="1e373-109">RDMA özelliğine sahip Windows VM'ler tooaccess Azure RDMA ağ hello için gereksinimleri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1e373-109">Following are requirements for RDMA-capable Windows VMs tooaccess hello Azure RDMA network:</span></span> 

* <span data-ttu-id="1e373-110">**İşletim Sistemi**</span><span class="sxs-lookup"><span data-stu-id="1e373-110">**Operating system**</span></span>
  
  <span data-ttu-id="1e373-111">Windows Server 2012 R2, Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="1e373-111">Windows Server 2012 R2, Windows Server 2012</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="1e373-112">Şu anda, Windows Server 2016 RDMA bağlantısı Azure'da desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="1e373-112">Currently, Windows Server 2016 does not support RDMA connectivity in Azure.</span></span>
  >

* <span data-ttu-id="1e373-113">**Kullanılabilirlik kümesi veya Bulut hizmeti** – dağıtma hello RDMA özellikli Vm'lerde hello aynı kullanılabilirlik kümesinde (hello Azure Resource Manager dağıtım modeli kullandığınızda) veya hello aynı bulut hizmetine (Merhaba Klasik dağıtım modeli kullandığınızda).</span><span class="sxs-lookup"><span data-stu-id="1e373-113">**Availability set or cloud service** – Deploy hello RDMA-capable VMs in hello same availability set (when you use hello Azure Resource Manager deployment model) or hello same cloud service (when you use hello classic deployment model).</span></span> <span data-ttu-id="1e373-114">Azure Batch kullanırsanız hello RDMA özellikli VM'ler hello olmalıdır aynı havuzu.</span><span class="sxs-lookup"><span data-stu-id="1e373-114">If you use Azure Batch, hello RDMA-capable VMs must be in hello same pool.</span></span>

* <span data-ttu-id="1e373-115">**MPI** -Microsoft MPI (MS-MPI) 2012 R2 veya sonraki sürümlerde, Intel MPI kitaplığının 5.x</span><span class="sxs-lookup"><span data-stu-id="1e373-115">**MPI** - Microsoft MPI (MS-MPI) 2012 R2 or later, Intel MPI Library 5.x</span></span>

  <span data-ttu-id="1e373-116">Desteklenen MPI uygulamaları hello Microsoft Network Direct arabirimi toocommunicate örnekleri arasında kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e373-116">Supported MPI implementations use hello Microsoft Network Direct interface toocommunicate between instances.</span></span> 

* <span data-ttu-id="1e373-117">**RDMA ağ adresi alanını** -hello RDMA ağ azure'da hello adres alanı 172.16.0.0/16 ayırır.</span><span class="sxs-lookup"><span data-stu-id="1e373-117">**RDMA network address space** - hello RDMA network in Azure reserves hello address space 172.16.0.0/16.</span></span> <span data-ttu-id="1e373-118">bir Azure sanal ağında dağıtılan örneklerinde toorun MPI uygulamaları hello sanal ağ adres alanı hello RDMA ağ çakışmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="1e373-118">toorun MPI applications on instances deployed in an Azure virtual network, make sure that hello virtual network address space does not overlap hello RDMA network.</span></span>

* <span data-ttu-id="1e373-119">**HpcVmDrivers VM uzantısı** -RDMA özellikli Vm'lerinde hello HpcVmDrivers uzantısı tooinstall Windows ağ aygıt sürücüleri RDMA bağlantısı için eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e373-119">**HpcVmDrivers VM extension** - On RDMA-capable VMs, you must add hello HpcVmDrivers extension tooinstall Windows network device drivers for RDMA connectivity.</span></span> <span data-ttu-id="1e373-120">(A8 ve A9 örneklerinin bazı dağıtımlarda hello HpcVmDrivers uzantısı otomatik olarak eklenir.) kullanabileceğiniz tooadd hello VM uzantısı tooa VM, [Azure PowerShell](/powershell/azure/overview) cmdlet'leri.</span><span class="sxs-lookup"><span data-stu-id="1e373-120">(In certain deployments of A8 and A9 instances, hello HpcVmDrivers extension is added automatically.) tooadd hello VM extension tooa VM, you can use [Azure PowerShell](/powershell/azure/overview) cmdlets.</span></span> 

  
  <span data-ttu-id="1e373-121">yükler hello adlı varolan bir RDMA özelliğine sahip VM üzerindeki en son sürüm 1.1 HpcVMDrivers uzantısı komutu aşağıdaki hello *myVM* adlı hello kaynak grubunda dağıtılan *myResourceGroup* hello içinde *Batı ABD* bölge:</span><span class="sxs-lookup"><span data-stu-id="1e373-121">hello following command installs hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named *myVM* deployed in hello resource group named *myResourceGroup* in hello *West US* region:</span></span>

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  <span data-ttu-id="1e373-122">Daha fazla bilgi için bkz: [sanal makine uzantıları ve özellikleri](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e373-122">For more information, see [Virtual machine extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="1e373-123">Hello dağıtılan VM'ler uzantıları ile çalışabilirsiniz [Klasik dağıtım modeli](classic/manage-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="1e373-123">You can also work with extensions for VMs deployed in hello [classic deployment model](classic/manage-extensions.md).</span></span>


## <a name="using-hpc-pack"></a><span data-ttu-id="1e373-124">HPC Pack kullanma</span><span class="sxs-lookup"><span data-stu-id="1e373-124">Using HPC Pack</span></span>

<span data-ttu-id="1e373-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft'un ücretsiz HPC küme ve iş yönetimi çözümü olan Azure toorun MPI Windows tabanlı uygulamalar ve diğer HPC iş yükleri bir işlem kümesi toocreate için bir seçenek.</span><span class="sxs-lookup"><span data-stu-id="1e373-125">[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft’s free HPC cluster and job management solution, is one option for you toocreate a compute cluster in Azure toorun Windows-based MPI applications and other HPC workloads.</span></span> <span data-ttu-id="1e373-126">HPC Pack 2012 R2 ve sonraki sürümler için RDMA özellikli Vm'lerinde dağıtılan hello Azure RDMA ağ kullanan MS MPI çalışma zamanı ortamı içerir.</span><span class="sxs-lookup"><span data-stu-id="1e373-126">HPC Pack 2012 R2 and later versions include a runtime environment for MS-MPI that uses hello Azure RDMA network when deployed on RDMA-capable VMs.</span></span>




## <a name="other-sizes"></a><span data-ttu-id="1e373-127">Diğer boyutlara</span><span class="sxs-lookup"><span data-stu-id="1e373-127">Other sizes</span></span>
- [<span data-ttu-id="1e373-128">Genel amaçlı</span><span class="sxs-lookup"><span data-stu-id="1e373-128">General purpose</span></span>](sizes-general.md)
- [<span data-ttu-id="1e373-129">İşlem için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="1e373-129">Compute optimized</span></span>](sizes-compute.md)
- [<span data-ttu-id="1e373-130">Bellek için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="1e373-130">Memory optimized</span></span>](../virtual-machines-windows-sizes-memory.md)
- [<span data-ttu-id="1e373-131">Depolama için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="1e373-131">Storage optimized</span></span>](../virtual-machines-windows-sizes-storage.md)
- [<span data-ttu-id="1e373-132">GPU için iyileştirilmiş</span><span class="sxs-lookup"><span data-stu-id="1e373-132">GPU optimized</span></span>](sizes-gpu.md)

## <a name="next-steps"></a><span data-ttu-id="1e373-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e373-133">Next steps</span></span>

- <span data-ttu-id="1e373-134">Windows Server'da HPC paketi ile denetim listeleri toouse hello işlem yoğunluklu örnekler için bkz: [HPC Pack toorun MPI uygulamaları Windows RDMA kümeyle ayarlama](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1e373-134">For checklists toouse hello compute-intensive instances with HPC Pack on Windows Server, see [Set up a Windows RDMA cluster with HPC Pack toorun MPI applications](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

- <span data-ttu-id="1e373-135">MPI uygulamaları Azure Batch ile çalıştırırken toouse işlem yoğunluklu örnekleri görmek [kullanımı çok örnekli görevler toorun ileti geçirme arabirimi (MPI) Azure Batch uygulamalarda](../../batch/batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="1e373-135">toouse compute-intensive instances when running MPI applications with Azure Batch, see [Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Azure Batch](../../batch/batch-mpi.md).</span></span>

- <span data-ttu-id="1e373-136">Hakkında daha fazla bilgi [Azure işlem birimleri (ACU)](acu.md) Azure SKU'ları üzerinde işlem performans karşılaştırmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1e373-136">Learn more about how [Azure compute units (ACU)](acu.md) can help you compare compute performance across Azure SKUs.</span></span>




