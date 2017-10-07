---
title: "aaaWindows HPC Pack Merhaba bulut seçeneklerinde küme | Microsoft Docs"
description: "Microsoft HPC Pack toocreate seçeneklerle hakkında bilgi edinin ve bir Windows yüksek performanslı bilgi işlem (HPC) hello Azure bulut kümede yönetme"
services: virtual-machines-windows,cloud-services,batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management,hpc-pack
ms.assetid: 02c5566d-2129-483c-9ecf-0d61030442d7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/06/2017
ms.author: danlep
ms.openlocfilehash: 6158d9dd0cecda38b14f85a2b2080163f18e8cf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="options-with-hpc-pack-toocreate-and-manage-a-windows-hpc-cluster-in-azure"></a>Seçenekler ile HPC Pack toocreate ve bir Windows HPC kümesini azure'da yönetmek
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

Bu makalede seçenekleri toocreate HPC Pack kümeleri toorun Windows iş yükleri odaklanır. Ayrıca seçenek vardır toorun oluşturma HPC Pack kümeleri için [Linux HPC iş yükleri](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="run-an-hpc-pack-cluster-in-azure-vms"></a>HPC Pack küme Azure Vm'lerde çalıştırın
### <a name="azure-templates"></a>Azure şablonları
* (GitHub) [HPC Pack 2016 küme şablonları](https://github.com/MsHpcPack/HPCPack2016)
* (Market) [HPC paketi küme iş yükleri için](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/)
* (Market) [Excel iş yükleri için HPC paketi küme](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterexcelcn/)
* (Hızlı Başlangıç) [HPC kümesi oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster)
* (Hızlı Başlangıç) [Özel işlem düğümü görüntüsüyle HPC kümesi oluşturma](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster-custom-image)

### <a name="azure-vm-images"></a>Azure VM görüntüleri
* [Windows Server 2016 baş düğümünde HPC Pack 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2016?tab=Overview)
* [HPC Pack 2016 işlem düğümü üzerinde Windows Server 2016](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2016?tab=Overview)
* [Windows Server 2012 R2 HPC Pack 2016 baş düğüm](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016HeadNodeonWindowsServer2012R2?tab=Overview)
* [Windows Server 2012 R2 HPC Pack 2016 işlem düğümünde](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.HPCPack2016ComputeNodeonWindowsServer2012R2?tab=Overview)
* [Windows Server 2012 R2 baş düğümünde HPC Pack 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/)
* [Windows Server 2012 R2 HPC Pack 2012 R2 işlem düğümünde](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodeonwindowsserver2012r2/)
* [HPC Pack hesaplama düğümünün Excel Windows Server 2012 R2 ile](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2computenodewithexcelonwindowsserver2012r2/)

### <a name="powershell-deployment-script"></a>PowerShell dağıtım komut dosyası
* [HPC Pack Iaas dağıtım betiği hello ile HPC kümesi oluşturma](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Öğreticiler
* [Öğretici: Azure bir HPC Pack 2016 küme dağıtma](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Öğretici: Azure toorun Excel HPC Pack kümede ve SOA iş yükleri ile çalışmaya başlama](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-hello-azure-portal"></a>Hello Azure portal ile el ile dağıtımı
* [Bir Azure VM'de HPC paketi küme baş düğümüne hello ayarlama](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a>Küme yönetimi
* [Azure HPC Pack kümede işlem düğümlerine yönetme](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Büyüme ve Azure işlem kaynakları bir HPC Pack kümesindeki Daralt](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [İşlerini tooan HPC Pack Azure kümesinde gönderme](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [HPC Pack iş yönetimi](https://technet.microsoft.com/library/jj899585.aspx)
* [Azure Active Directory ile Azure HPC Pack kümede yönetme](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-tooan-hpc-pack-cluster"></a>Çalışan rolü düğümleri tooan HPC paketi küme ekleme
* [HPC Pack ile tooAzure çalışan örnekleri veri bloğu](https://technet.microsoft.com/library/gg481749.aspx)
* [Öğretici: Azure HPC paketi ile karma küme ayarlayın](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [Azure'da Azure "veri bloğu" düğümleri tooan HPC paketi üstbilgi düğümü Ekle](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a>Azure Batch ile tümleştirme
* [TooAzure HPC paketi ile toplu veri bloğu](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>MPI iş yükleri için RDMA kümeleri oluşturma
* [HPC Pack toorun MPI uygulamaları ile Windows RDMA kümesi ayarlama](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

