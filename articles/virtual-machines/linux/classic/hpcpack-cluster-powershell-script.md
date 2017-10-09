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
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="05023-103">Yüksek performanslı bilgi işlem (HPC) Linux küme ile Merhaba HPC Pack Iaas dağıtım komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="05023-103">Create a Linux high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="05023-104">Merhaba HPC Pack Iaas dağıtım PowerShell komut dosyası toodeploy tam bir HPC Pack 2012 R2 küme Linux iş yükleri için Azure sanal makinelerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="05023-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="05023-105">Windows Server ve Microsoft HPC Pack çalıştıran bir Active Directory katılmış baş düğüm ve bir hello HPC paketi tarafından desteklenen Linux dağıtımları çalışacak işlem düğümleri Hello küme oluşur.</span><span class="sxs-lookup"><span data-stu-id="05023-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of hello Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="05023-106">Windows Azure iş yükleri bir HPC paketi küme toodeploy istiyorsanız, bkz: [hello HPC Pack Iaas dağıtım betiği ile bir Windows HPC küme oluşturma](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="05023-106">If you want toodeploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="05023-107">Azure Resource Manager şablonu toodeploy bir HPC paketi küme de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05023-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="05023-108">Bir örnek için bkz: [Linux işlem düğümleri ile bir HPC kümesi oluşturma](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span><span class="sxs-lookup"><span data-stu-id="05023-108">For an example, see [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="05023-109">Bu makalede açıklanan PowerShell betiğini Hello Azure'da hello Klasik dağıtım modeli kullanarak Microsoft HPC Pack 2012 R2 küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="05023-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="05023-110">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="05023-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="05023-111">Ayrıca, bu makalede açıklanan hello betik HPC Pack 2016 desteklemez.</span><span class="sxs-lookup"><span data-stu-id="05023-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="05023-112">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="05023-112">Example configuration file</span></span>
<span data-ttu-id="05023-113">Merhaba aşağıdaki yapılandırma dosyası bir etki alanı denetleyicisi ve etki alanı ormanı oluşturur ve yerel veritabanlarını tek bir baş düğüm ve 10 Linux işlem düğümlerini içeren bir HPC paketi küme dağıtır.</span><span class="sxs-lookup"><span data-stu-id="05023-113">hello following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="05023-114">Tüm hello bulut Hizmetleri doğrudan hello Doğu Asya konumda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="05023-114">All hello cloud services are created directly in hello East Asia location.</span></span> <span data-ttu-id="05023-115">Merhaba Linux işlem düğümlerini iki bulut Hizmetleri ve iki depolama hesabı oluşturulur (diğer bir deyişle, *MyLnxCN 0001* için *MyLnxCN 0005* içinde *MyLnxCNService01* ve *mylnxstorage01*, ve *MyLnxCN-0006* için *MyLnxCN 0010* içinde *MyLnxCNService02* ve *mylnxstorage02* ).</span><span class="sxs-lookup"><span data-stu-id="05023-115">hello Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="05023-116">Merhaba işlem düğümleri OpenLogic CentOS sürüm 7.0 Linux görüntüden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="05023-116">hello compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="05023-117">Abonelik adı ve hello hesabı ve hizmet adları için kendi değerlerinizi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="05023-117">Substitute your own values for your subscription name and hello account and service names.</span></span>

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
## <a name="troubleshooting"></a><span data-ttu-id="05023-118">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="05023-118">Troubleshooting</span></span>
* <span data-ttu-id="05023-119">**"Sanal ağ yok" hatası**.</span><span class="sxs-lookup"><span data-stu-id="05023-119">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="05023-120">Merhaba HPC Pack Iaas dağıtım komut dosyası toodeploy birden fazla küme Azure içinde eşzamanlı olarak bir abonelik altında çalıştırırsanız, bir veya daha fazla dağıtım hello hatasıyla başarısız olabilir "VNet *VNet\_adı* yok".</span><span class="sxs-lookup"><span data-stu-id="05023-120">If you run hello HPC Pack IaaS deployment script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="05023-121">Bu hata oluşursa hello betik hello başarısız dağıtım için yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="05023-121">If this error occurs, rerun hello script for hello failed deployment.</span></span>
* <span data-ttu-id="05023-122">**Hello Azure sanal ağı ' hello Internet sorun erişme**.</span><span class="sxs-lookup"><span data-stu-id="05023-122">**Problem accessing hello Internet from hello Azure virtual network**.</span></span> <span data-ttu-id="05023-123">Merhaba dağıtım komut dosyası kullanarak yeni bir etki alanı denetleyicisi ile bir HPC paketi küme oluşturma ya da bir baş düğüm VM toodomain denetleyicisi el ile yükseltmek, hello Azure sanal ağı toohello Internet hello Vm'lerde bağlanma sorunlarla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="05023-123">If you create an HPC Pack cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs in hello Azure virtual network toohello Internet.</span></span> <span data-ttu-id="05023-124">İletici DNS sunucusu hello etki alanı denetleyicisi üzerinde otomatik olarak yapılandırılır ve bu iletici DNS sunucusu düzgün sorunu çözmezse, bu durum ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="05023-124">This can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="05023-125">Bu soruna geçici bir çözüm toowork toohello etki alanı denetleyicisi ve her iki Kaldır hello ileticisi yapılandırma ayarı oturum veya geçerli iletici DNS sunucusunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="05023-125">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="05023-126">Bu, Sunucu Yöneticisi'nde tıklatın toodo **Araçları** > **DNS** tooopen DNS Yöneticisi'ni çift tıklayın ve ardından **İleticiler**.</span><span class="sxs-lookup"><span data-stu-id="05023-126">toodo this, in Server Manager click **Tools** > **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05023-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="05023-127">Next steps</span></span>
* <span data-ttu-id="05023-128">Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md) desteklenen Linux dağıtımları hakkında daha fazla bilgi için veri taşıma ve işleri tooan HPC paketi küme Linux gönderme işlem düğümleri.</span><span class="sxs-lookup"><span data-stu-id="05023-128">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs tooan HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="05023-129">Merhaba betik toocreate bir küme kullanan ve Linux HPC iş yükünü çalıştırmak öğreticileri için bkz:</span><span class="sxs-lookup"><span data-stu-id="05023-129">For tutorials that use hello script toocreate a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="05023-130">Linux işlem düğümlerinde Azure ile birlikte Microsoft HPC Pack NAMD çalıştırın</span><span class="sxs-lookup"><span data-stu-id="05023-130">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="05023-131">Linux işlem düğümlerinde Azure ile birlikte Microsoft HPC Pack OpenFOAM çalıştırın</span><span class="sxs-lookup"><span data-stu-id="05023-131">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="05023-132">Yıldız Çalıştır-CCM + Microsoft HPC Pack Linux işlem düğümlerini Azure</span><span class="sxs-lookup"><span data-stu-id="05023-132">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)

