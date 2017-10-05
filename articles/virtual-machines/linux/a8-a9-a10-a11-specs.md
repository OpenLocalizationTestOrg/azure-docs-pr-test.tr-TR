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
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a>Y-serisi ve işlem yoğunluklu A-series VM'ler hakkında için Linux
Arka plan bilgileri ve daha yeni Azure H serisi ve önceki A8, A9, A10 ve A11 boyutları olarak da bilinen kullanmak için bazı noktalar işte *işlem yoğunluklu* örnekleri. Bu makalede, bu boyutlar Linux VM'ler için kullanımı üzerine odaklanmıştır. Bunlar için de kullanabilirsiniz [Windows VM'ler](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Temel özellikleri, depolama kapasitesi ve disk Ayrıntılar için bkz: [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-to-the-rdma-network"></a>RDMA ağ erişimi
RDMA özellikli Linux çalışma aşağıdakilerden birini Linux HPC dağıtımları ve Azure RDMA ağ yararlanmak için desteklenen bir MPI uygulama desteklenen VM'lerin kümeleri oluşturabilirsiniz. Bkz: [MPI uygulamaları çalıştırmak için Linux RDMA küme ayarlama](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) dağıtım seçenekleri ve örnek yapılandırma adımları için.

* **Dağıtımları** -Azure Marketi RDMA özellikli SUSE Linux Enterprise Server (SLES) ya da yanlış Wave yazılım (önceki adıyla OpenLogic) CentOS tabanlı HPC görüntülerden VM'ler dağıtmanız gerekir. Aşağıdaki Market görüntülerini RDMA bağlantısı destekler:
  
    * SLES 12 SP1 HPC, SLES 12 için SP1 için HPC (Premium)
    
    * CentOS tabanlı 7.1 HPC, CentOS tabanlı 6.5 HPC  
 
        > [!NOTE]
        > Y-serisi VM'ler için HPC görüntüsü için SLES 12 SP1 ya da CentOS tabanlı 7.1 HPC görüntü öneririz.
        >
        > CentOS tabanlı HPC görüntülerinde çekirdek güncelleştirmeleri de devre dışı **yum** yapılandırma dosyası. Linux RDMA sürücüleri RPM paket olarak dağıtılır ve çekirdek güncelleştirdiyseniz sürücü güncelleştirmelerini çalışmayabilir nedeni budur.
        > 
        > 
* **MPI** -Intel MPI kitaplığının 5.x
  
    Market görüntüsü bağlı olarak, ayrı lisans, yükleme, seçtiğiniz veya Intel MPI yapılandırmasını, aşağıdaki gibi gerekli olabilir: 
  
  * **SLES 12 SP1 HPC görüntü için** -Intel MPI paketleri VM dağıtılır. Aşağıdaki komutu çalıştırarak yükleyin:

      ```bash
      sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
      ```

  * **CentOS tabanlı HPC görüntüler** -Intel MPI 5.1 zaten yüklü.  
    
    Ek sistem yapılandırması, kümelenmiş sanal makinelerin MPI işlerini çalıştırmak için gereklidir. Örneğin, VM'lerin bir kümede işlem düğümleri arasında güven oluşturmanız gerekir. Tipik ayarları için bkz: [MPI uygulamaları çalıştırmak için Linux RDMA küme ayarlama](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="considerations-for-hpc-pack-and-linux"></a>HPC Pack ve Linux değerlendirmeleri
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft'un ücretsiz HPC küme ve iş yönetimi çözümü, işlem yoğunluklu örnekler Linux ile kullanmanız için bir seçenek sunar. HPC Pack Destek'ın en son sürümlerine işlem bir Windows Server baş düğümü tarafından yönetilen Azure vm'lerinde dağıtılan düğümleri üzerinde çalışmak için birkaç Linux dağıtımları. Intel MPI çalıştıran RDMA özellikli Linux işlem düğümleri ile HPC Pack zamanlayabilir ve Linux MPI RDMA ağ erişim uygulamaları çalıştırın. Başlamak için bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="network-topology-considerations"></a>Ağ topolojisi hakkında önemli noktalar
* RDMA özellikli Linux VM'ler üzerinde Azure, Eth1 RDMA ağ trafiği için ayrılmış. Herhangi bir Eth1 ayarı veya bu ağa başvuran yapılandırma dosyasında herhangi bir bilgiyi değiştirmeyin. Eth0 normal Azure ağ trafiği için ayrılır.
* Azure'da, IP üzerinden InfiniBand (IB) desteklenmiyor. Yalnızca IB üzerinden RDMA desteklenir.



## <a name="next-steps"></a>Sonraki adımlar
* Kullanılabilirlik ve işlem yoğunluklu boyutlarını fiyatlandırma hakkında daha fazla ayrıntı için bkz: [sanal makineler fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).
* Depolama kapasitesi ve disk Ayrıntılar için bkz: [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Dağıtma ve RDMA Linux üzerinde işlem yoğunluklu boyutları kullanarak başlamak için bkz: [MPI uygulamaları çalıştırmak için Linux RDMA küme ayarlama](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

