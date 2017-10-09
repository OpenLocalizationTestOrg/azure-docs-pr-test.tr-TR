---
title: "aaaPowerShell betik toodeploy Linux HPC küme | Microsoft Docs"
description: "PowerShell komut dosyası toodeploy Linux HPC Pack 2012 R2 küme Azure sanal makinelerinde çalıştırma"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a>Yüksek performanslı bilgi işlem (HPC) Linux küme ile Merhaba HPC Pack Iaas dağıtım komut dosyası oluşturma
Merhaba HPC Pack Iaas dağıtım PowerShell komut dosyası toodeploy tam bir HPC Pack 2012 R2 küme Linux iş yükleri için Azure sanal makinelerinde çalıştırın. Windows Server ve Microsoft HPC Pack çalıştıran bir Active Directory katılmış baş düğüm ve bir hello HPC paketi tarafından desteklenen Linux dağıtımları çalışacak işlem düğümleri Hello küme oluşur. Windows Azure iş yükleri bir HPC paketi küme toodeploy istiyorsanız, bkz: [hello HPC Pack Iaas dağıtım betiği ile bir Windows HPC küme oluşturma](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Azure Resource Manager şablonu toodeploy bir HPC paketi küme de kullanabilirsiniz. Bir örnek için bkz: [Linux işlem düğümleri ile bir HPC kümesi oluşturma](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).

> [!IMPORTANT] 
> Bu makalede açıklanan PowerShell betiğini Hello Azure'da hello Klasik dağıtım modeli kullanarak Microsoft HPC Pack 2012 R2 küme oluşturur. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.
> Ayrıca, bu makalede açıklanan hello betik HPC Pack 2016 desteklemez.

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a>Örnek yapılandırma dosyası
Merhaba aşağıdaki yapılandırma dosyası bir etki alanı denetleyicisi ve etki alanı ormanı oluşturur ve yerel veritabanlarını tek bir baş düğüm ve 10 Linux işlem düğümlerini içeren bir HPC paketi küme dağıtır. Tüm hello bulut Hizmetleri doğrudan hello Doğu Asya konumda oluşturulur. Merhaba Linux işlem düğümlerini iki bulut Hizmetleri ve iki depolama hesabı oluşturulur (diğer bir deyişle, *MyLnxCN 0001* için *MyLnxCN 0005* içinde *MyLnxCNService01* ve *mylnxstorage01*, ve *MyLnxCN-0006* için *MyLnxCN 0010* içinde *MyLnxCNService02* ve *mylnxstorage02* ). Merhaba işlem düğümleri OpenLogic CentOS sürüm 7.0 Linux görüntüden oluşturulur. 

Abonelik adı ve hello hesabı ve hizmet adları için kendi değerlerinizi yerleştirin.

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
    </DomainController>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a>Sorun giderme
* **"Sanal ağ yok" hatası**. Merhaba HPC Pack Iaas dağıtım komut dosyası toodeploy birden fazla küme Azure içinde eşzamanlı olarak bir abonelik altında çalıştırırsanız, bir veya daha fazla dağıtım hello hatasıyla başarısız olabilir "VNet *VNet\_adı* yok".
  Bu hata oluşursa hello betik hello başarısız dağıtım için yeniden çalıştırın.
* **Hello Azure sanal ağı ' hello Internet sorun erişme**. Merhaba dağıtım komut dosyası kullanarak yeni bir etki alanı denetleyicisi ile bir HPC paketi küme oluşturma ya da bir baş düğüm VM toodomain denetleyicisi el ile yükseltmek, hello Azure sanal ağı toohello Internet hello Vm'lerde bağlanma sorunlarla karşılaşabilirsiniz. İletici DNS sunucusu hello etki alanı denetleyicisi üzerinde otomatik olarak yapılandırılır ve bu iletici DNS sunucusu düzgün sorunu çözmezse, bu durum ortaya çıkabilir.
  
    Bu soruna geçici bir çözüm toowork toohello etki alanı denetleyicisi ve her iki Kaldır hello ileticisi yapılandırma ayarı oturum veya geçerli iletici DNS sunucusunu yapılandırın. Bu, Sunucu Yöneticisi'nde tıklatın toodo **Araçları** > **DNS** tooopen DNS Yöneticisi'ni çift tıklayın ve ardından **İleticiler**.

## <a name="next-steps"></a>Sonraki adımlar
* Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md) desteklenen Linux dağıtımları hakkında daha fazla bilgi için veri taşıma ve işleri tooan HPC paketi küme Linux gönderme işlem düğümleri.
* Merhaba betik toocreate bir küme kullanan ve Linux HPC iş yükünü çalıştırmak öğreticileri için bkz:
  * [Linux işlem düğümlerinde Azure ile birlikte Microsoft HPC Pack NAMD çalıştırın](hpcpack-cluster-namd.md)
  * [Linux işlem düğümlerinde Azure ile birlikte Microsoft HPC Pack OpenFOAM çalıştırın](hpcpack-cluster-openfoam.md)
  * [Yıldız Çalıştır-CCM + Microsoft HPC Pack Linux işlem düğümlerini Azure](hpcpack-cluster-starccm.md)

