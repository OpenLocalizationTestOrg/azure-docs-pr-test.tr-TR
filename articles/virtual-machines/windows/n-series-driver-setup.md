---
title: "Windows için Azure N-serisi sürücü kurulumu | Microsoft Docs"
description: "Windows Azure'da çalışan N-serisi VM'ler için NVIDIA GPU sürücüleri ayarlama"
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
ms.openlocfilehash: b480d10df777a2757c073ff77e1845d33d63163a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a><span data-ttu-id="a3fe3-103">GPU sürücüleri Windows Server çalıştıran N-serisi VM'ler için ayarlama</span><span class="sxs-lookup"><span data-stu-id="a3fe3-103">Set up GPU drivers for N-series VMs running Windows Server</span></span>
<span data-ttu-id="a3fe3-104">Windows Server 2016 veya Windows Server 2012 R2 çalıştıran Azure N-serisi VM'ler GPU yeteneklerinden yararlanabilmek için desteklenen NVIDIA grafik sürücüleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-104">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, install supported NVIDIA graphics drivers.</span></span> <span data-ttu-id="a3fe3-105">N-serisi VM dağıttıktan sonra bu makalede sürücü kurulum adımlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-105">This article provides driver setup steps after you deploy an N-series VM.</span></span> <span data-ttu-id="a3fe3-106">Sürücü Kurulum bilgileri de için kullanılabilir [Linux VM'ler](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a3fe3-106">Driver setup information is also available for [Linux VMs](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="a3fe3-107">Temel özellikleri, depolama kapasitesi ve disk Ayrıntılar için bkz: [GPU Windows VM boyutları](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a3fe3-107">For basic specs, storage capacities, and disk details, see [GPU Windows VM sizes](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a><span data-ttu-id="a3fe3-108">Sürücü yükleme</span><span class="sxs-lookup"><span data-stu-id="a3fe3-108">Driver installation</span></span>

1. <span data-ttu-id="a3fe3-109">Uzak Masaüstü'nü her N-serisi VM tarafından bağlayın.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-109">Connect by Remote Desktop to each N-series VM.</span></span>

2. <span data-ttu-id="a3fe3-110">İndirin, ayıklayın ve Windows işletim sistemi için desteklenen bir sürücü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-110">Download, extract, and install the supported driver for your Windows operating system.</span></span>

<span data-ttu-id="a3fe3-111">Azure NV Vm'lerinde sürücü yüklendikten sonra bir yeniden başlatma gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-111">On Azure NV VMs, a restart is required after driver installation.</span></span> <span data-ttu-id="a3fe3-112">NC VM'ler üzerinde bir yeniden başlatma gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-112">On NC VMs, a restart is not required.</span></span>

## <a name="verify-driver-installation"></a><span data-ttu-id="a3fe3-113">Sürücü yükleme doğrulayın</span><span class="sxs-lookup"><span data-stu-id="a3fe3-113">Verify driver installation</span></span>

<span data-ttu-id="a3fe3-114">Sürücü yükleme Aygıt Yöneticisi'nde doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-114">You can verify driver installation in Device Manager.</span></span> <span data-ttu-id="a3fe3-115">Aşağıdaki örnek, bir Azure NC VM Tesla K80 kartı başarılı yapılandırması gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-115">The following example shows successful configuration of the Tesla K80 card on an Azure NC VM.</span></span>

![GPU sürücüsünün özellikleri](./media/n-series-driver-setup/GPU_driver_properties.png)

<span data-ttu-id="a3fe3-117">GPU aygıt durumunu sorgulamak için aşağıdaki komutu çalıştırın [NVIDIA SMI](https://developer.nvidia.com/nvidia-system-management-interface) komut satırı yardımcı programının sürücüsüyle yüklü.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-117">To query the GPU device state, run the [nvidia-smi](https://developer.nvidia.com/nvidia-system-management-interface) command-line utility installed with the driver.</span></span>

1. <span data-ttu-id="a3fe3-118">Bir komut istemi açın ve değiştirmek **C:\Program Files\NVIDIA Corporation\NVSMI** dizini.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-118">Open a command prompt and change to the **C:\Program Files\NVIDIA Corporation\NVSMI** directory.</span></span>

2. <span data-ttu-id="a3fe3-119">Çalıştırma **NVIDIA SMI**.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-119">Run **nvidia-smi**.</span></span> <span data-ttu-id="a3fe3-120">Sürücü yüklüyse, aşağıda için benzer bir çıktı göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-120">If the driver is installed you will see output similar to below.</span></span> <span data-ttu-id="a3fe3-121">Unutmayın **GPU kul** gösterir **%0** GPU iş yükü VM çalıştırmakta olduğunuz sürece.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-121">Note that **GPU-Util** shows **0%** unless you are currently running a GPU workload on the VM.</span></span>

![NVIDIA cihaz durumu](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a><span data-ttu-id="a3fe3-123">RDMA ağ NC24r VM'ler için</span><span class="sxs-lookup"><span data-stu-id="a3fe3-123">RDMA network for NC24r VMs</span></span>

<span data-ttu-id="a3fe3-124">RDMA ağ bağlantısı NC24r aynı kullanılabilirlik kümesinde dağıtılan VM'ler üzerinde etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-124">RDMA network connectivity can be enabled on NC24r VMs deployed in the same availability set.</span></span> <span data-ttu-id="a3fe3-125">RDMA bağlantısını etkinleştirmek Windows ağ aygıt sürücülerini yüklemek için HpcVmDrivers uzantısı eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-125">The HpcVmDrivers extension must be added to install Windows network device drivers that enable RDMA connectivity.</span></span> <span data-ttu-id="a3fe3-126">NC24r VM için VM uzantısı eklemek için kullanın [Azure PowerShell](/powershell/azure/overview) cmdlet'leri Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-126">To add the VM extension to an NC24r VM, use [Azure PowerShell](/powershell/azure/overview) cmdlets for Azure Resource Manager.</span></span>

> [!NOTE]
> <span data-ttu-id="a3fe3-127">Şu anda yalnızca Windows Server 2012 R2 RDMA ağ NC24r Vm'lerinde destekler.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-127">Currently, only Windows Server 2012 R2 supports the RDMA network on NC24r VMs.</span></span>
> 

<span data-ttu-id="a3fe3-128">En son sürüm 1.1 yüklemek için mevcut bir RDMA özellikli VM'yi HpcVMDrivers uzantısı Batı ABD bölgesi, myVM adlı:</span><span class="sxs-lookup"><span data-stu-id="a3fe3-128">To install the latest version 1.1 HpcVMDrivers extension on an existing RDMA-capable VM named myVM in the West US region:</span></span>
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  <span data-ttu-id="a3fe3-129">Daha fazla bilgi için bkz: [sanal makine uzantıları ve özellikleri Windows için](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a3fe3-129">For more information, see [Virtual machine extensions and features for Windows](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="a3fe3-130">RDMA ağ ile çalışan uygulamalar için ileti geçirme arabirimi (MPI) trafiğini destekler [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) veya Intel MPI 5.x.</span><span class="sxs-lookup"><span data-stu-id="a3fe3-130">The RDMA network supports Message Passing Interface (MPI) traffic for applications running with [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) or Intel MPI 5.x.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="a3fe3-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a3fe3-131">Next steps</span></span>

* <span data-ttu-id="a3fe3-132">N-serisi VM'ler NVIDIA GPU hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="a3fe3-132">For more information about the NVIDIA GPUs on the N-series VMs, see:</span></span>
    * <span data-ttu-id="a3fe3-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (için Azure NC VM'ler)</span><span class="sxs-lookup"><span data-stu-id="a3fe3-133">[NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (for Azure NC VMs)</span></span>
    * <span data-ttu-id="a3fe3-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (için Azure NV VM'ler)</span><span class="sxs-lookup"><span data-stu-id="a3fe3-134">[NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (for Azure NV VMs)</span></span>

* <span data-ttu-id="a3fe3-135">NVIDIA Tesla GPU GPU hızlandırılmış uygulamaları oluşturan geliştiriciler ayrıca karşıdan yükleyip CUDA Araç Seti 8 için [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) veya [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span><span class="sxs-lookup"><span data-stu-id="a3fe3-135">Developers building GPU-accelerated applications for the NVIDIA Tesla GPUs can also download and install the CUDA Toolkit 8 for [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) or [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe).</span></span> <span data-ttu-id="a3fe3-136">Daha fazla bilgi için bkz: [CUDA Yükleme Kılavuzu'na](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span><span class="sxs-lookup"><span data-stu-id="a3fe3-136">For more information, see the [CUDA Installation Guide](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).</span></span>


