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
# <a name="set-up-gpu-drivers-for-n-series-vms-running-windows-server"></a>GPU sürücüleri Windows Server çalıştıran N-serisi VM'ler için ayarlama
tootake yeteneklerinden hello GPU Azure N-serisi, Windows Server 2016 veya Windows Server 2012 R2 çalıştıran VM'ler, yükleme desteklenen NVIDIA grafik sürücüleri. N-serisi VM dağıttıktan sonra bu makalede sürücü kurulum adımlarını sağlar. Sürücü Kurulum bilgileri de için kullanılabilir [Linux VM'ler](../linux/n-series-driver-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Temel özellikleri, depolama kapasitesi ve disk Ayrıntılar için bkz: [GPU Windows VM boyutları](sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 


[!INCLUDE [virtual-machines-n-series-windows-support](../../../includes/virtual-machines-n-series-windows-support.md)]



## <a name="driver-installation"></a>Sürücü yükleme

1. Uzak Masaüstü tooeach N-serisi VM tarafından bağlayın.

2. İndirin, ayıklayın ve Windows işletim sistemi için desteklenen hello sürücüsünü yükleyin.

Azure NV Vm'lerinde sürücü yüklendikten sonra bir yeniden başlatma gereklidir. NC VM'ler üzerinde bir yeniden başlatma gerekli değildir.

## <a name="verify-driver-installation"></a>Sürücü yükleme doğrulayın

Sürücü yükleme Aygıt Yöneticisi'nde doğrulayabilirsiniz. Merhaba aşağıdaki örnek hello Tesla K80 kartının başarılı bir yapılandırma bir Azure NC VM gösterir.

![GPU sürücüsünün özellikleri](./media/n-series-driver-setup/GPU_driver_properties.png)

Merhaba çalıştırmak tooquery hello GPU cihaz durumu, [NVIDIA SMI](https://developer.nvidia.com/nvidia-system-management-interface) komut satırı yardımcı programının hello sürücüsüyle yüklü.

1. Bir komut istemi açın ve toohello değiştirmek **C:\Program Files\NVIDIA Corporation\NVSMI** dizini.

2. Çalıştırma **NVIDIA SMI**. Merhaba sürücüsü yüklüyse çıkış benzer toobelow görürsünüz. Unutmayın **GPU kul** gösterir **%0** hello VM üzerinde şu anda bir GPU iş yükü çalıştırmıyorsanız.

![NVIDIA cihaz durumu](./media/n-series-driver-setup/smi.png)  

## <a name="rdma-network-for-nc24r-vms"></a>RDMA ağ NC24r VM'ler için

RDMA ağ bağlantısı NC24r hello dağıtılan VM'ler etkinleştirilebilir aynı kullanılabilirlik kümesi. Merhaba HpcVmDrivers uzantısı RDMA bağlantıyı etkinleştirmek tooinstall Windows ağ aygıt sürücüleri eklenmesi gerekir. tooadd hello VM uzantısı tooan NC24r VM kullanmak [Azure PowerShell](/powershell/azure/overview) cmdlet'leri Azure Resource Manager.

> [!NOTE]
> Şu anda yalnızca Windows Server 2012 R2 hello RDMA ağ NC24r Vm'lerinde destekler.
> 

tooinstall hello en son sürüm 1.1 HpcVMDrivers uzantısı mevcut RDMA özellikli VM'de hello Batı ABD bölgesi, myVM adlı:
  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  Daha fazla bilgi için bkz: [sanal makine uzantıları ve özellikleri Windows için](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Merhaba RDMA ağ ile çalışan uygulamalar için ileti geçirme arabirimi (MPI) trafiği destekleyen [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) veya Intel MPI 5.x. 


## <a name="next-steps"></a>Sonraki adımlar

* Merhaba N-serisi VM'ler hello NVIDIA GPU hakkında daha fazla bilgi için bkz:
    * [NVIDIA Tesla K80](http://www.nvidia.com/object/tesla-k80.html) (için Azure NC VM'ler)
    * [NVIDIA Tesla M60](http://www.nvidia.com/object/tesla-m60.html) (için Azure NV VM'ler)

* Merhaba NVIDIA Tesla GPU GPU hızlandırılmış uygulamaları oluşturan geliştiriciler ayrıca karşıdan yükleyip Merhaba CUDA Araç Seti 8 [Windows Server 2016](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_win10-exe) veya [Windows Server 2012 R2](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_windows-exe). Daha fazla bilgi için bkz: Merhaba [CUDA Yükleme Kılavuzu'na](http://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html#axzz4ZcwJvqYi).


