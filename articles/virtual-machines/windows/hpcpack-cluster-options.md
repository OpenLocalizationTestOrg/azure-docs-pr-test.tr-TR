---
title: "Bulutta Microsoft HPC Pack küme seçenekleri | Microsoft Docs"
description: "Oluşturmak ve bir Windows yüksek performanslı bilgi işlem (HPC) küme Azure bulutta yönetmek için Microsoft HPC paketi ile seçenekleri hakkında bilgi edinin"
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
ms.openlocfilehash: 96a5520d8440af7d8a880c2675a5d4eb4121e9ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="options-with-hpc-pack-to-create-and-manage-a-windows-hpc-cluster-in-azure"></a>Azure'da Windows HPC Kümesi oluşturabileceğiniz ve yönetebileceğiniz için HPC paketi ile seçenekleri
[!INCLUDE [virtual-machines-common-hpcpack-cluster-options](../../../includes/virtual-machines-common-hpcpack-cluster-options.md)]

Bu makalede Windows iş yüklerini çalıştırmak için HPC Pack kümeleri oluşturma seçenekleri odaklanır. Ayrıca çalıştırmak için HPC Pack kümeleri oluşturmak için seçenekler vardır [Linux HPC iş yükleri](../linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


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
* [HPC Kümesi ile HPC Pack Iaas dağıtım komut dosyası oluşturma](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="tutorials"></a>Öğreticiler
* [Öğretici: Azure bir HPC Pack 2016 küme dağıtma](hpcpack-2016-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Öğretici: Azure Excel ve SOA iş yüklerini çalıştırmak için bir HPC paketi küme kullanmaya başlama](excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="manual-deployment-with-the-azure-portal"></a>Azure portal ile el ile dağıtımı
* [Bir Azure VM'de HPC paketi küme baş düğümüne ayarlama](hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="cluster-management"></a>Küme yönetimi
* [Azure HPC Pack kümede işlem düğümlerine yönetme](classic/hpcpack-cluster-node-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Büyüme ve Azure işlem kaynakları bir HPC Pack kümesindeki Daralt](classic/hpcpack-cluster-node-autogrowshrink.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Azure'da bir HPC Pack kümeye iş göndermek](hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [HPC Pack iş yönetimi](https://technet.microsoft.com/library/jj899585.aspx)
* [Azure Active Directory ile Azure HPC Pack kümede yönetme](hpcpack-cluster-active-directory.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="add-worker-role-nodes-to-an-hpc-pack-cluster"></a>Çalışan rolü düğümlerine bir HPC Pack kümeye ekleme
* [HPC paketi ile Azure çalışan örneklerine veri bloğu](https://technet.microsoft.com/library/gg481749.aspx)
* [Öğretici: Azure HPC paketi ile karma küme ayarlayın](../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md)
* [HPC paketi üstbilgi düğümü azure'da Azure "veri bloğu" düğümler ekleyin](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="integrate-with-azure-batch"></a>Azure Batch ile tümleştirme
* [HPC paketi ile Azure toplu işlem için veri bloğu](https://technet.microsoft.com/library/mt612877.aspx)

## <a name="create-rdma-clusters-for-mpi-workloads"></a>MPI iş yükleri için RDMA kümeleri oluşturma
* [MPI uygulamalarını çalıştırmak için kullanılan HPC Pack içeren Windows RDMA kümesi ayarlama](classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

