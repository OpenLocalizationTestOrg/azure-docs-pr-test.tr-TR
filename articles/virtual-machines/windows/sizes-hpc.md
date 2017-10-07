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
# <a name="high-performance-compute-vm-sizes"></a>Yüksek performanslı bilgi işlem VM boyutları

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>RDMA özellikli örnekleri
Bir alt kümesini hello işlem yoğunluklu örnekler (H16r, H16mr, A8 ve A9) doğrudan uzak bellek erişimi (RDMA) bağlantısı için bir ağ arabirimi özelliği. Bu ayrıca toohello standart Azure ağ arabirimi kullanılabilir tooother VM boyutları arabirimidir. 
  
Bu arabirim hello RDMA özellikli örnekleri toocommunicate H16r ve H16mr sanal makineler için FDR hızlarını ve A8 ve A9 sanal makineler için QDR hızlarını işletim bir InfiniBand ağ üzerinden verir. RDMA yeteneklere hello ölçeklenebilirlik ve ileti geçirme arabirimi (MPI) uygulamaların performansını artırabilir.

RDMA özelliğine sahip Windows VM'ler tooaccess Azure RDMA ağ hello için gereksinimleri aşağıda verilmiştir: 

* **İşletim Sistemi**
  
  Windows Server 2012 R2, Windows Server 2012
  
  > [!NOTE]
  > Şu anda, Windows Server 2016 RDMA bağlantısı Azure'da desteklemiyor.
  >

* **Kullanılabilirlik kümesi veya Bulut hizmeti** – dağıtma hello RDMA özellikli Vm'lerde hello aynı kullanılabilirlik kümesinde (hello Azure Resource Manager dağıtım modeli kullandığınızda) veya hello aynı bulut hizmetine (Merhaba Klasik dağıtım modeli kullandığınızda). Azure Batch kullanırsanız hello RDMA özellikli VM'ler hello olmalıdır aynı havuzu.

* **MPI** -Microsoft MPI (MS-MPI) 2012 R2 veya sonraki sürümlerde, Intel MPI kitaplığının 5.x

  Desteklenen MPI uygulamaları hello Microsoft Network Direct arabirimi toocommunicate örnekleri arasında kullanın. 

* **RDMA ağ adresi alanını** -hello RDMA ağ azure'da hello adres alanı 172.16.0.0/16 ayırır. bir Azure sanal ağında dağıtılan örneklerinde toorun MPI uygulamaları hello sanal ağ adres alanı hello RDMA ağ çakışmadığından emin olun.

* **HpcVmDrivers VM uzantısı** -RDMA özellikli Vm'lerinde hello HpcVmDrivers uzantısı tooinstall Windows ağ aygıt sürücüleri RDMA bağlantısı için eklemeniz gerekir. (A8 ve A9 örneklerinin bazı dağıtımlarda hello HpcVmDrivers uzantısı otomatik olarak eklenir.) kullanabileceğiniz tooadd hello VM uzantısı tooa VM, [Azure PowerShell](/powershell/azure/overview) cmdlet'leri. 

  
  yükler hello adlı varolan bir RDMA özelliğine sahip VM üzerindeki en son sürüm 1.1 HpcVMDrivers uzantısı komutu aşağıdaki hello *myVM* adlı hello kaynak grubunda dağıtılan *myResourceGroup* hello içinde *Batı ABD* bölge:

  ```PowerShell
  Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup" -Location "westus" -VMName "myVM" -ExtensionName "HpcVmDrivers" -Publisher "Microsoft.HpcCompute" -Type "HpcVmDrivers" -TypeHandlerVersion "1.1"
  ```
  
  Daha fazla bilgi için bkz: [sanal makine uzantıları ve özellikleri](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Hello dağıtılan VM'ler uzantıları ile çalışabilirsiniz [Klasik dağıtım modeli](classic/manage-extensions.md).


## <a name="using-hpc-pack"></a>HPC Pack kullanma

[Microsoft HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft'un ücretsiz HPC küme ve iş yönetimi çözümü olan Azure toorun MPI Windows tabanlı uygulamalar ve diğer HPC iş yükleri bir işlem kümesi toocreate için bir seçenek. HPC Pack 2012 R2 ve sonraki sürümler için RDMA özellikli Vm'lerinde dağıtılan hello Azure RDMA ağ kullanan MS MPI çalışma zamanı ortamı içerir.




## <a name="other-sizes"></a>Diğer boyutlara
- [Genel amaçlı](sizes-general.md)
- [İşlem için iyileştirilmiş](sizes-compute.md)
- [Bellek için iyileştirilmiş](../virtual-machines-windows-sizes-memory.md)
- [Depolama için iyileştirilmiş](../virtual-machines-windows-sizes-storage.md)
- [GPU için iyileştirilmiş](sizes-gpu.md)

## <a name="next-steps"></a>Sonraki adımlar

- Windows Server'da HPC paketi ile denetim listeleri toouse hello işlem yoğunluklu örnekler için bkz: [HPC Pack toorun MPI uygulamaları Windows RDMA kümeyle ayarlama](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

- MPI uygulamaları Azure Batch ile çalıştırırken toouse işlem yoğunluklu örnekleri görmek [kullanımı çok örnekli görevler toorun ileti geçirme arabirimi (MPI) Azure Batch uygulamalarda](../../batch/batch-mpi.md).

- Hakkında daha fazla bilgi [Azure işlem birimleri (ACU)](acu.md) Azure SKU'ları üzerinde işlem performans karşılaştırmanıza yardımcı olur.




