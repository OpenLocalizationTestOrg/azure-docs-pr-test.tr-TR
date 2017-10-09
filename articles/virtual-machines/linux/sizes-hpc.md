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
# <a name="high-performance-compute-linux-vm-sizes"></a>Yüksek performanslı işlem Linux VM boyutları

[!INCLUDE [virtual-machines-common-sizes-hpc](../../../includes/virtual-machines-common-sizes-hpc.md)]

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../../includes/virtual-machines-common-sizes-table-defs.md)]

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="rdma-capable-instances"></a>RDMA özellikli örnekleri
Bir alt kümesini hello işlem yoğunluklu örnekler (H16r, H16mr, A8 ve A9) doğrudan uzak bellek erişimi (RDMA) bağlantısı için bir ağ arabirimi özelliği. Bu ayrıca toohello standart Azure ağ arabirimi kullanılabilir tooother VM boyutları arabirimidir. 
  
Bu arabirim hello RDMA özellikli örnekleri toocommunicate H16r ve H16mr sanal makineler için FDR hızlarını ve A8 ve A9 sanal makineler için QDR hızlarını işletim bir InfiniBand ağ üzerinden verir. RDMA yeteneklere hello ölçeklenebilirlik ve ileti geçirme arabirimi (MPI) uygulamaların performansını artırabilir.

RDMA özellikli Linux VM'ler tooaccess Azure RDMA ağ hello için gereksinimleri aşağıda verilmiştir:
 
* **Dağıtımları** - VMs gelen RDMA özellikli SUSE Linux Enterprise Server (SLES) dağıtmanız gerekir veya yanlış Wave yazılım (önceki adıyla OpenLogic) CentOS tabanlı HPC görüntülerinde hello Azure Marketi. Merhaba aşağıdaki Market görüntülerini RDMA bağlantısı destekler:
  
    * SLES 12 SP1 HPC veya SLES 12 için SP1 için HPC (Premium)
    
    * CentOS tabanlı 7.3 HPC, CentOS tabanlı 7.1 HPC, CentOS tabanlı 6.8 HPC veya CentOS tabanlı 6.5 HPC  
 
        > [!NOTE]
        > Y-serisi VM'ler için HPC görüntüsü için SLES 12 SP1 veya CentOS tabanlı 7.1 veya sonraki HPC görüntü öneririz.
        >
        > Merhaba CentOS tabanlı HPC görüntülerinde hello çekirdek güncelleştirmeleri devre dışı **yum** yapılandırma dosyası. Hello Linux RDMA sürücüleri RPM paket olarak dağıtılır ve hello çekirdek güncelleştirdiyseniz sürücü güncelleştirmelerini çalışmayabilir nedeni budur.
        > 
        > 
* **MPI** -Intel MPI kitaplığının 5.x
  
    Merhaba Market görüntüsü bağlı olarak, ayrı lisans, yükleme, seçtiğiniz veya Intel MPI yapılandırmasını, aşağıdaki gibi gerekli olabilir: 
  
  * **SLES 12 SP1 HPC görüntü için** -Intel MPI paketleri hello VM üzerinde dağıtılır. Merhaba aşağıdaki komutu çalıştırarak yükleyin:

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * **CentOS tabanlı HPC görüntüler** -Intel MPI 5.1 zaten yüklü.  
    
    Ek sistem yapılandırması gerekli toorun MPI işlerini kümelenmiş sanal makineleri üzerinde değil. Örneğin, VM'lerin bir kümede tooestablish ihtiyacınız hello arasında güven işlem düğümlerini. Tipik ayarları için bkz: [bir Linux RDMA küme toorun MPI uygulama ayarlama](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="network-topology-considerations"></a>Ağ topolojisi hakkında önemli noktalar
* RDMA özellikli Linux VM'ler üzerinde Azure, Eth1 RDMA ağ trafiği için ayrılmış. Herhangi bir Eth1 ayarı veya herhangi bir bilgi toothis ağ başvuran hello yapılandırma dosyasında değiştirmeyin. Eth0 normal Azure ağ trafiği için ayrılır.

* Azure'da, IP üzerinden InfiniBand (IB) desteklenmiyor. Yalnızca IB üzerinden RDMA desteklenir.

## <a name="using-hpc-pack"></a>HPC Pack kullanma
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft'un ücretsiz HPC küme ve iş yönetimi, bir çözümdür, Linux toouse hello işlem yoğunluklu örnekler için bir seçenek. HPC Pack Merhaba en son sürümleri toorun üzerinde işlem düğümlerini Azure Vm'leri, bir Windows Server baş düğümü tarafından yönetilen dağıtılmış birkaç Linux dağıtımları destekler. Intel MPI çalıştıran RDMA özellikli Linux işlem düğümleri ile HPC Pack zamanlayabilir ve bu erişim hello RDMA ağ Linux MPI uygulamaları çalıştırın. Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="other-sizes"></a>Diğer boyutlara
- [Genel amaçlı](sizes-general.md)
- [İşlem için iyileştirilmiş](sizes-compute.md)
- [Bellek için iyileştirilmiş](sizes-memory.md)
- [Depolama için iyileştirilmiş](sizes-storage.md)
- [GPU](../windows/sizes-gpu.md)


## <a name="next-steps"></a>Sonraki adımlar

- dağıtma ve RDMA Linux üzerinde işlem yoğunluklu boyutları kullanarak başlatılan tooget bkz [Linux RDMA küme toorun MPI uygulamalar ayarlamak](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

- Hakkında daha fazla bilgi [Azure işlem birimleri (ACU)](acu.md) Azure SKU'ları üzerinde işlem performans karşılaştırmanıza yardımcı olur.




