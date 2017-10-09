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
# <a name="about-h-series-and-compute-intensive-a-series-vms-for-linux"></a>Y-serisi ve işlem yoğunluklu A-series VM'ler hakkında için Linux
Arka plan bilgileri işte ve kullanmak için bazı noktalar yeni Azure H-serisi hello ve hello önceki A8, A9, A10 ve A11 boyutları olarak da bilinen *işlem yoğunluklu* örnekleri. Bu makalede, bu boyutlar Linux VM'ler için kullanımı üzerine odaklanmıştır. Bunlar için de kullanabilirsiniz [Windows VM'ler](../windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Temel özellikleri, depolama kapasitesi ve disk Ayrıntılar için bkz: [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-a8-a9-a10-a11-specs](../../../includes/virtual-machines-common-a8-a9-a10-a11-specs.md)]

## <a name="access-toohello-rdma-network"></a>Erişim toohello RDMA ağ
Desteklenen Linux HPC dağıtımları ve bir desteklenen MPI uygulama tootake avantajlarından hello Azure RDMA ağ aşağıdaki hello birini çalıştıran RDMA özellikli Linux VM'ler kümeleri oluşturabilirsiniz. Bkz: [Linux RDMA küme toorun MPI uygulamalar ayarlamak](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) dağıtım seçenekleri ve örnek yapılandırma adımları için.

* **Dağıtımları** - VMs gelen RDMA özellikli SUSE Linux Enterprise Server (SLES) dağıtmanız gerekir veya yanlış Wave yazılım (önceki adıyla OpenLogic) CentOS tabanlı HPC görüntülerinde hello Azure Marketi. Merhaba aşağıdaki Market görüntülerini RDMA bağlantısı destekler:
  
    * SLES 12 SP1 HPC, SLES 12 için SP1 için HPC (Premium)
    
    * CentOS tabanlı 7.1 HPC, CentOS tabanlı 6.5 HPC  
 
        > [!NOTE]
        > Y-serisi VM'ler için HPC görüntüsü için SLES 12 SP1 ya da CentOS tabanlı 7.1 HPC görüntü öneririz.
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
    
    Ek sistem yapılandırması gerekli toorun MPI işlerini kümelenmiş sanal makineleri üzerinde değil. Örneğin, VM'lerin bir kümede tooestablish ihtiyacınız hello arasında güven işlem düğümlerini. Tipik ayarları için bkz: [Linux RDMA küme toorun MPI uygulamalar ayarlamak](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="considerations-for-hpc-pack-and-linux"></a>HPC Pack ve Linux değerlendirmeleri
[HPC Pack](https://technet.microsoft.com/library/jj899572.aspx), Microsoft'un ücretsiz HPC küme ve iş yönetimi çözümü toouse hello işlem yoğunluklu örnekler Linux sizin için bir seçenek sunar. HPC Pack Merhaba en son sürümleri toorun üzerinde işlem düğümlerini Azure Vm'leri, bir Windows Server baş düğümü tarafından yönetilen dağıtılmış birkaç Linux dağıtımları destekler. Intel MPI çalıştıran RDMA özellikli Linux işlem düğümleri ile HPC Pack zamanlayabilir ve bu erişim hello RDMA ağ Linux MPI uygulamaları çalıştırın. başlatıldı, tooget bkz [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

## <a name="network-topology-considerations"></a>Ağ topolojisi hakkında önemli noktalar
* RDMA özellikli Linux VM'ler üzerinde Azure, Eth1 RDMA ağ trafiği için ayrılmış. Herhangi bir Eth1 ayarı veya herhangi bir bilgi toothis ağ başvuran hello yapılandırma dosyasında değiştirmeyin. Eth0 normal Azure ağ trafiği için ayrılır.
* Azure'da, IP üzerinden InfiniBand (IB) desteklenmiyor. Yalnızca IB üzerinden RDMA desteklenir.



## <a name="next-steps"></a>Sonraki adımlar
* Kullanılabilirlik ve hello işlem yoğunluklu boyutlarını fiyatlandırma hakkında daha fazla ayrıntı için bkz: [sanal makineler fiyatlandırma](https://azure.microsoft.com/pricing/details/virtual-machines/#Linux).
* Depolama kapasitesi ve disk Ayrıntılar için bkz: [sanal makineler için Boyutlar](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* dağıtma ve RDMA Linux üzerinde işlem yoğunluklu boyutları kullanarak başlatılan tooget bkz [Linux RDMA küme toorun MPI uygulamalar ayarlamak](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

