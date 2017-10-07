---
title: "aaaLinux HPC paketi küme seçenekleri hello bulutta | Microsoft Docs"
description: "Microsoft HPC Pack toocreate seçeneklerle hakkında bilgi edinin ve bir Linux yüksek performanslı bilgi işlem (HPC) hello Azure bulut kümede yönetme"
services: virtual-machines-linux,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: ac60624e-aefa-40c3-8bc1-ef6d5c0ef1a2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 60d093b466f44a0391815842c421c328e8c7a0d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-an-hpc-cluster-in-azure-for-linux-workloads"></a>HPC Pack toocreate ile seçenekleri ve Azure Linux iş yükleri için bir HPC küme yönetme
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

Bu makalede seçenekleri toouse HPC Pack toorun Linux iş yükünü odaklanır. Ayrıca çalıştırmak için seçenek vardır [HPC paketi ile Windows HPC iş yüklerini](../windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>HPC Pack küme Azure Vm'lerde çalıştırın
### <a name="azure-templates"></a>Azure şablonları
* (GitHub) [HPC Pack 2016 küme şablonları](https://github.com/MsHpcPack/HPCPack2016)
* (Market) [Linux iş yükleri için HPC paketi küme](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/)
* (Hızlı Başlangıç) [Linux işlem düğümleri ile bir HPC kümesi oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-linux-cn)

### <a name="powershell-deployment-script"></a>PowerShell dağıtım komut dosyası
* [HPC Pack Iaas dağıtım betiği hello ile Linux HPC küme oluşturma](../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Öğreticiler
* [Öğretici: Azure HPC Pack kümesinde Linux işlem düğümlerine kullanmaya başlama](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Öğretici: Çalıştır NAMD Microsoft HPC paketi ile Linux işlem düğümlerini Azure](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Öğretici: Azure Linux RDMA kümesinde Microsoft HPC paketi ile çalışma OpenFOAM](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Öğretici: Çalıştır yıldız-CCM + Linux RDMA üzerinde Microsoft HPC Pack ile Azure'da küme](classic/hpcpack-cluster-starccm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="cluster-management"></a>Küme yönetimi
* [İşlerini tooan HPC Pack Azure kümesinde gönderme](../windows/hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [HPC Pack iş yönetimi](https://technet.microsoft.com/library/jj899585.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>MPI iş yükleri için RDMA kümeleri oluşturma
* [Öğretici: Azure Linux RDMA kümesinde Microsoft HPC paketi ile çalışma OpenFOAM](classic/hpcpack-cluster-openfoam.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Bir Linux RDMA küme toorun MPI uygulama ayarlama](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

