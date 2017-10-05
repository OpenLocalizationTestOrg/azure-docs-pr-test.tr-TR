---
title: "Linux HPC küme dağıtmak için PowerShell komut dosyası | Microsoft Docs"
description: "Azure sanal makinelerde Linux HPC Pack 2012 R2 küme dağıtmak için bir PowerShell betiğini çalıştırın"
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
ms.openlocfilehash: c15dc66718a855e22f8109448cb8c8a23787b9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="e5f62-103">Yüksek performanslı bilgi işlem (HPC) küme Linux ile HPC Pack Iaas dağıtım komut dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e5f62-103">Create a Linux high-performance computing (HPC) cluster with the HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="e5f62-104">HPC Pack Iaas dağıtımı Azure sanal makinelerde Linux iş yükleri için tam bir HPC Pack 2012 R2 küme dağıtmak için PowerShell betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e5f62-104">Run the HPC Pack IaaS deployment PowerShell script to deploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="e5f62-105">Küme Windows Server ve Microsoft HPC Pack çalıştıran bir Active Directory katılmış baş düğüm ve HPC paketi tarafından desteklenen Linux dağıtımları birini çalıştırın işlem düğümleri oluşur.</span><span class="sxs-lookup"><span data-stu-id="e5f62-105">The cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of the Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="e5f62-106">Windows Azure iş yükleri HPC Pack kümesinde dağıtmak istiyorsanız, bkz: [bir Windows HPC Kümesi ile HPC Pack Iaas dağıtım komut dosyası oluşturma](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e5f62-106">If you want to deploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with the HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="e5f62-107">Bir Azure Resource Manager şablonu, bir HPC paketi küme dağıtmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5f62-107">You can also use an Azure Resource Manager template to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="e5f62-108">Bir örnek için bkz: [Linux işlem düğümleri ile bir HPC kümesi oluşturma](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span><span class="sxs-lookup"><span data-stu-id="e5f62-108">For an example, see [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e5f62-109">Bu makalede açıklanan PowerShell Betiği Azure'da Klasik dağıtım modeli kullanarak bir Microsoft HPC Pack 2012 R2 kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e5f62-109">The PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using the classic deployment model.</span></span> <span data-ttu-id="e5f62-110">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="e5f62-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="e5f62-111">Ayrıca, bu makalede açıklanan betik HPC Pack 2016 desteklemez.</span><span class="sxs-lookup"><span data-stu-id="e5f62-111">In addition, the script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="e5f62-112">Örnek yapılandırma dosyası</span><span class="sxs-lookup"><span data-stu-id="e5f62-112">Example configuration file</span></span>
<span data-ttu-id="e5f62-113">Aşağıdaki yapılandırma dosyası, bir etki alanı denetleyicisi ve etki alanı ormanı oluşturur ve yerel veritabanlarını tek bir baş düğüm ve 10 Linux işlem düğümlerini içeren bir HPC Pack kümesi dağıtır.</span><span class="sxs-lookup"><span data-stu-id="e5f62-113">The following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="e5f62-114">Tüm bulut hizmetlerine doğrudan Doğu Asya konumda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e5f62-114">All the cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="e5f62-115">Linux işlem düğümlerini iki bulut Hizmetleri ve iki depolama hesabı oluşturulduğunda (diğer bir deyişle, *MyLnxCN 0001* için *MyLnxCN 0005* içinde *MyLnxCNService01* ve *mylnxstorage01*, ve *MyLnxCN-0006* için *MyLnxCN 0010* içinde *MyLnxCNService02* ve *mylnxstorage02*).</span><span class="sxs-lookup"><span data-stu-id="e5f62-115">The Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="e5f62-116">İşlem düğümleri OpenLogic CentOS sürüm 7.0 Linux görüntüden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e5f62-116">The compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="e5f62-117">Abonelik adı ve hesap ve hizmet adları için kendi değerlerinizi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="e5f62-117">Substitute your own values for your subscription name and the account and service names.</span></span>

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
## <a name="troubleshooting"></a><span data-ttu-id="e5f62-118">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="e5f62-118">Troubleshooting</span></span>
* <span data-ttu-id="e5f62-119">**"Sanal ağ yok" hatası**.</span><span class="sxs-lookup"><span data-stu-id="e5f62-119">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="e5f62-120">Bir abonelik altında eşzamanlı olarak birden çok küme azure'da dağıtmak için HPC Pack Iaas dağıtım betik çalıştırırsanız, bir veya daha fazla dağıtım hatasıyla başarısız olabilir "VNet *VNet\_adı* yok".</span><span class="sxs-lookup"><span data-stu-id="e5f62-120">If you run the HPC Pack IaaS deployment script to deploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with the error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="e5f62-121">Bu hata oluşursa, başarısız dağıtım için komut dosyası yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e5f62-121">If this error occurs, rerun the script for the failed deployment.</span></span>
* <span data-ttu-id="e5f62-122">**Azure sanal ağdan Internet erişirken sorun**.</span><span class="sxs-lookup"><span data-stu-id="e5f62-122">**Problem accessing the Internet from the Azure virtual network**.</span></span> <span data-ttu-id="e5f62-123">Dağıtım komut dosyası kullanarak yeni bir etki alanı denetleyicisi ile bir HPC paketi küme oluşturma veya etki alanı denetleyicisine bir üstbilgi düğüm VM'ine el ile yükseltmek, Azure sanal ağ içindeki VM'ler Internet'e bağlanmasını sorunlarla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5f62-123">If you create an HPC Pack cluster with a new domain controller by using the deployment script, or you manually promote a head node VM to domain controller, you may experience problems connecting the VMs in the Azure virtual network to the Internet.</span></span> <span data-ttu-id="e5f62-124">İletici DNS sunucusu etki alanı denetleyicisinde otomatik olarak yapılandırılır ve bu iletici DNS sunucusu düzgün sorunu çözmezse, bu durum ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="e5f62-124">This can occur if a forwarder DNS server is automatically configured on the domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="e5f62-125">Etki alanı denetleyicisi ve kaldırın veya iletici yapılandırma ayarı oturumunu bu soruna geçici bir çözüm veya geçerli iletici DNS sunucusunu yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="e5f62-125">To work around this problem, log on to the domain controller and either remove the forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="e5f62-126">Bu, Sunucu Yöneticisi'ni tıklatın yapmak için **Araçları** > **DNS** DNS Yöneticisi'ni açın ve ardından **İleticiler**.</span><span class="sxs-lookup"><span data-stu-id="e5f62-126">To do this, in Server Manager click **Tools** > **DNS** to open DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5f62-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e5f62-127">Next steps</span></span>
* <span data-ttu-id="e5f62-128">Bkz: [Linux işlem düğümlerini Azure bir HPC Pack kümesindeki kullanmaya başlama](hpcpack-cluster.md) desteklenen Linux dağıtımları hakkında daha fazla bilgi için veri taşıma ve Linux HPC Pack kümeyle işlerini gönderme işlem düğümleri.</span><span class="sxs-lookup"><span data-stu-id="e5f62-128">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs to an HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="e5f62-129">Bir küme oluşturmak ve Linux HPC iş yükü çalıştırmak için komut dosyası kullanma öğreticileri için bkz:</span><span class="sxs-lookup"><span data-stu-id="e5f62-129">For tutorials that use the script to create a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="e5f62-130">Linux işlem düğümlerinde Azure ile birlikte Microsoft HPC Pack NAMD çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e5f62-130">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="e5f62-131">Linux işlem düğümlerinde Azure ile birlikte Microsoft HPC Pack OpenFOAM çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e5f62-131">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="e5f62-132">Yıldız Çalıştır-CCM + Microsoft HPC Pack Linux işlem düğümlerini Azure</span><span class="sxs-lookup"><span data-stu-id="e5f62-132">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)

