---
title: "Windows için aaaAzure N-serisi sürücü kurulumu | Microsoft Docs"
description: "Nasıl tooset NVIDIA GPU sürücüleri Windows Azure'da çalışan N-serisi VM'ler için ayarlama"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3950c34-9406-48ae-bcd9-c0418607b37d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/07/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2acce57d4f9eb1d02bf3bc0303bcb9690475698c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="c9b1e-103">GPU sürücüleri Windows Server çalıştıran N-serisi VM'ler için ayarlama</span><span class="sxs-lookup"><span data-stu-id="c9b1e-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="c9b1e-104">tootake yeteneklerinden hello GPU Azure N-serisi, Windows Server 2016 veya Windows Server 2012 R2 çalıştıran VM'ler, yükleme desteklenen NVIDIA grafik sürücüleri.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-104">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="c9b1e-105">N-serisi VM dağıttıktan sonra bu makalede sürücü kurulum adımlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="c9b1e-106">Sürücü Kurulum bilgileri de için kullanılabilir [Linux VM'ler](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9b1e-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c9b1e-107">Temel özellikleri, depolama kapasitesi ve disk Ayrıntılar için bkz: [GPU Windows VM boyutları](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9b1e-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="c9b1e-108">Sürücü yükleme</span><span class="sxs-lookup"><span data-stu-id="c9b1e-108">Driver installation</span></span>

1. <span data-ttu-id="c9b1e-109">Uzak Masaüstü tooeach N-serisi VM tarafından bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-109">Connect by Remote Desktop tooeach N-series VM.</span></span>

2. <span data-ttu-id="c9b1e-110">İndirin, ayıklayın ve Windows işletim sistemi için desteklenen hello sürücüsünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-110">Download, extract, and install hello supported driver for your Windows operating system.</span></span>

<span data-ttu-id="c9b1e-111">Azure NV Vm'lerinde sürücü yüklendikten sonra bir yeniden başlatma gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="c9b1e-112">NC VM'ler üzerinde bir yeniden başlatma gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="c9b1e-113">Sürücü yükleme doğrulayın</span><span class="sxs-lookup"><span data-stu-id="c9b1e-113">Verify driver installation</span></span>

<span data-ttu-id="c9b1e-114">Sürücü yükleme Aygıt Yöneticisi'nde doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="c9b1e-115">Merhaba aşağıdaki örnek hello Tesla K80 kartının başarılı bir yapılandırma bir Azure NC VM gösterir.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-115">hello following example shows successful configuration of hello Tesla K80 card on an Azure NC VM.</span></span>

![GPU sürücüsünün özellikleri](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="c9b1e-117">Merhaba çalıştırmak tooquery hello GPU cihaz durumu, [NVIDIA SMI](https://developer.nvidia.com/nvidia-system-management-interface) komut satırı yardımcı programının hello sürücüsüyle yüklü.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-117">tooquery hello GPU device state, run hello [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with hello driver.</span></span>

1. <span data-ttu-id="c9b1e-118">Bir komut istemi açın ve toohello değiştirmek **C:\Program Files\NVIDIA Corporation\NVSMI** dizini.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-118">Open a command prompt and change toohello **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="c9b1e-119">Çalıştırma **NVIDIA SMI**.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="c9b1e-120">Merhaba sürücüsü yüklüyse çıkış benzer toobelow görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-120">If hello driver is installed you will see output similar toobelow.</span></span> <span data-ttu-id="c9b1e-121">Unutmayın **GPU kul** gösterir **%0** hello VM üzerinde şu anda bir GPU iş yükü çalıştırmıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on hello VM.</span></span>

![NVIDIA cihaz durumu](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="c9b1e-123">RDMA ağ NC24r VM'ler için</span><span class="sxs-lookup"><span data-stu-id="c9b1e-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="c9b1e-124">RDMA ağ bağlantısı NC24r hello dağıtılan VM'ler etkinleştirilebilir aynı kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-124">RDMA network connectivity can be enabled on NC24r VMs deployed in hello same availability set.</span></span> <span data-ttu-id="c9b1e-125">Merhaba HpcVmDrivers uzantısı RDMA bağlantıyı etkinleştirmek tooinstall Windows ağ aygıt sürücüleri eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-125">hello HpcVmDrivers extension must be added tooinstall Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="c9b1e-126">tooadd hello VM uzantısı tooan NC24r VM kullanmak [Azure PowerShell](/powershell/azure/overview) cmdlet'leri Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-126">tooadd hello VM extension tooan NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="c9b1e-127">Şu anda yalnızca Windows Server 2012 R2 hello RDMA ağ NC24r Vm'lerinde destekler.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-127">Currently, only Windows Server 2012 R2 supports hello RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="c9b1e-128">tooinstall hello en son sürüm 1.1 HpcVMDrivers uzantısı mevcut RDMA özellikli VM'de hello Batı ABD bölgesi, myVM adlı:</span><span class="sxs-lookup"><span data-stu-id="c9b1e-128">tooinstall hello latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in hello West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="c9b1e-129">Daha fazla bilgi için bkz: [sanal makine uzantıları ve özellikleri Windows için](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9b1e-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="c9b1e-130">Merhaba RDMA ağ ile çalışan uygulamalar için ileti geçirme arabirimi (MPI) trafiği destekleyen [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) veya Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="c9b1e-130">hello RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="c9b1e-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c9b1e-131">Next steps</span></span>

* <span data-ttu-id="c9b1e-132">Merhaba N-serisi VM'ler hello NVIDIA GPU hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="c9b1e-132">For more information about hello NVIDIA GPUs on hello N-series VMs, see:</span></span>
    * <span data-ttu-id="c9b1e-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (için Azure NC VM'ler)</span><span class="sxs-lookup"><span data-stu-id="c9b1e-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="c9b1e-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (için Azure NV VM'ler)</span><span class="sxs-lookup"><span data-stu-id="c9b1e-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="c9b1e-135">Merhaba NVIDIA Tesla GPU GPU hızlandırılmış uygulamaları oluşturan geliştiriciler ayrıca karşıdan yükleyip Merhaba CUDA Araç Seti 8 [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) veya [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="c9b1e-135">Developers building GPU-accelerated applications for hello NVIDIA Tesla GPUs can also download and install hello CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="c9b1e-136">Daha fazla bilgi için bkz: Merhaba [CUDA Yükleme Kılavuzu'na](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="c9b1e-136">For more information, see hello [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


