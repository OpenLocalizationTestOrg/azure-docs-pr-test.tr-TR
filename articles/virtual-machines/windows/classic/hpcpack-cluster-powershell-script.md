---
title: "Windows HPC Kümesi dağıtmak için PowerShell komut dosyası | Microsoft Docs"
description: "Azure sanal makinelerde Windows HPC Pack 2012 R2 küme dağıtmak için bir PowerShell betiğini çalıştırın"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 286b2be8-2533-40df-b02a-26156b1f1133
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 85b125ab19671b61d2541af6378c95feb88bf952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="4a6b4-103">Yüksek performanslı bilgi işlem (HPC) küme Windows HPC Pack Iaas dağıtım komut dosyası ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="4a6b4-103">Create a Windows high-performance computing (HPC) cluster with the HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="4a6b4-104">HPC Pack Iaas dağıtımı Azure sanal makinelerde Windows iş yükleri için tam bir HPC Pack 2012 R2 küme dağıtmak için PowerShell betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-104">Run the HPC Pack IaaS deployment PowerShell script to deploy a complete HPC Pack 2012 R2 cluster for Windows workloads in Azure virtual machines.</span></span> <span data-ttu-id="4a6b4-105">Küme Windows Server ve Microsoft HPC Pack çalıştıran bir Active Directory katılmış baş düğümü içerir ve ek Windows işlem kaynaklarını, belirtin.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-105">The cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and additional Windows compute resources you specify.</span></span> <span data-ttu-id="4a6b4-106">Azure Linux iş yükleri için bir HPC paketi küme dağıtmak istiyorsanız, bkz: [Linux HPC Kümesi ile HPC Pack Iaas dağıtım komut dosyası oluşturma](../../linux/classic/hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="4a6b4-106">If you want to deploy an HPC Pack cluster in Azure for Linux workloads, see [Create a Linux HPC cluster with the HPC Pack IaaS deployment script](../../linux/classic/hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="4a6b4-107">Bir Azure Resource Manager şablonu, bir HPC paketi küme dağıtmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-107">You can also use an Azure Resource Manager template to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="4a6b4-108">Örnekler için bkz: [bir HPC Kümesi oluşturmayı](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) ve [bir özel işlem düğümü görüntüsüyle HPC kümesi oluşturma](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span><span class="sxs-lookup"><span data-stu-id="4a6b4-108">For examples, see [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) and [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4a6b4-109">Bu makalede açıklanan PowerShell Betiği Azure'da Klasik dağıtım modeli kullanarak bir Microsoft HPC Pack 2012 R2 kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-109">The PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using the classic deployment model.</span></span> <span data-ttu-id="4a6b4-110">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="4a6b4-111">Ayrıca, bu makalede açıklanan betik HPC Pack 2016 desteklemez.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-111">In addition, the script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a><span data-ttu-id="4a6b4-112">Örnek yapılandırma dosyaları</span><span class="sxs-lookup"><span data-stu-id="4a6b4-112">Example configuration files</span></span>
<span data-ttu-id="4a6b4-113">Aşağıdaki örneklerde, abonelik kimliği için kendi değerlerinizi veya adını ve hesap ve hizmet adlarını yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-113">In the following examples, substitute your own values for your subscription Id or name and the account and service names.</span></span>

### <a name="example-1"></a><span data-ttu-id="4a6b4-114">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="4a6b4-114">Example 1</span></span>
<span data-ttu-id="4a6b4-115">Aşağıdaki yapılandırma dosyası bir baş düğüm yerel veritabanlarıyla bir HPC Pack kümeye dağıtır ve beş işlem düğümleri Windows Server 2012 R2 işletim sistemini çalıştıran.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-115">The following configuration file deploys an HPC Pack cluster that has a head node with local databases and five compute nodes running the Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="4a6b4-116">Tüm bulut hizmetlerine doğrudan Batı ABD konumunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-116">All the cloud services are created directly in the West US location.</span></span> <span data-ttu-id="4a6b4-117">Baş düğüm etki alanı ormanı etki alanı denetleyicisi olarak işlev görür.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-117">The head node acts as domain controller of the domain forest.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionId>08701940-C02E-452F-B0B1-39D50119F267</SubscriptionId>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%1000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>5</NodeCount>
    <OSVersion>WindowsServer2012R2</OSVersion>
  </ComputeNodes>
</IaaSClusterConfig>
```

### <a name="example-2"></a><span data-ttu-id="4a6b4-118">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="4a6b4-118">Example 2</span></span>
<span data-ttu-id="4a6b4-119">Aşağıdaki yapılandırma dosyası var olan bir etki alanı ormanı HPC Pack kümede dağıtır.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-119">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="4a6b4-120">Küme yerel veritabanlarıyla 1 baş düğüm vardır ve işlem düğümleri uygulanan Bgınfo VM uzantısı ile 12.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-120">The cluster has 1 head node with local databases and 12 compute nodes with the BGInfo VM extension applied.</span></span>
<span data-ttu-id="4a6b4-121">Windows güncelleştirmeleri otomatik yüklemesini etki alanı ormanındaki tüm sanal makineleri devre dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-121">Automatic installation of Windows updates is disabled for all the VMs in the domain forest.</span></span> <span data-ttu-id="4a6b4-122">Tüm bulut hizmetlerine doğrudan Doğu Asya konumda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-122">All the cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="4a6b4-123">İşlem düğümlerine oluşturulduğunu üç bulut Hizmetleri ve üç depolama hesabı: *MyHPCCN 0001* için *MyHPCCN 0005* içinde *MyHPCCNService01* ve *mycnstorage01*; *MyHPCCN-0006* için *MyHPCCN0010* içinde *MyHPCCNService02* ve *mycnstorage02*; ve *MyHPCCN 0011* için *MyHPCCN 0012* içinde *MyHPCCNService03* ve *mycnstorage03*).</span><span class="sxs-lookup"><span data-stu-id="4a6b4-123">The compute nodes are created in three cloud services and three storage accounts: *MyHPCCN-0001* to *MyHPCCN-0005* in *MyHPCCNService01* and *mycnstorage01*; *MyHPCCN-0006* to *MyHPCCN0010* in *MyHPCCNService02* and *mycnstorage02*; and *MyHPCCN-0011* to *MyHPCCN-0012* in *MyHPCCNService03* and *mycnstorage03*).</span></span> <span data-ttu-id="4a6b4-124">İşlem düğümleri, bir işlem düğümünden yakalanan bir görüntüden varolan özel oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-124">The compute nodes are created from an existing private image captured from a compute node.</span></span> <span data-ttu-id="4a6b4-125">Otomatik büyüme ve küçültme hizmeti varsayılan olarak etkin büyür ve küçültme aralıkları.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-125">The auto grow and shrink service is enabled with default grow and shrink intervals.</span></span>

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
     <NoWindowsAutoUpdate />
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
  </Certificates>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0001%</VMNamePattern>
<ServiceNamePattern>MyHPCCNService%01%</ServiceNamePattern>
<MaxNodeCountPerService>5</MaxNodeCountPerService>
<StorageAccountNamePattern>mycnstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>12</NodeCount>
    <ImageName HPCPackInstalled=”true”>MyHPCComputeNodeImage</ImageName>
    <VMExtensions>
       <VMExtension>
          <ExtensionName>BGInfo</ExtensionName>
          <Publisher>Microsoft.Compute</Publisher>
          <Version>1.*</Version>
       </VMExtension>
    </VMExtensions>
  </ComputeNodes>
  <AutoGrowShrink>
    <CertificateId>1</CertificateId>
  </AutoGrowShrink>
</IaaSClusterConfig>

```

### <a name="example-3"></a><span data-ttu-id="4a6b4-126">Örnek 3</span><span class="sxs-lookup"><span data-stu-id="4a6b4-126">Example 3</span></span>
<span data-ttu-id="4a6b4-127">Aşağıdaki yapılandırma dosyası var olan bir etki alanı ormanı HPC Pack kümede dağıtır.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-127">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="4a6b4-128">Küme bir baş düğüm, 500 GB veri diski olan bir veritabanı sunucusu, iki Aracısı düğümleri Windows Server 2012 R2 işletim sistemini çalıştıran ve Windows Server 2012 R2 işletim sistemi çalıştıran beş işlem düğümleri içerir.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-128">The cluster contains one head node, one database server with a 500 GB data disk, two broker nodes running the Windows Server 2012 R2 operating system, and five compute nodes running the Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="4a6b4-129">Bulut hizmeti, MyHPCCNService benzeşim grubunda oluşturuldu *MyIBAffinityGroup*, ve diğer bulut hizmetlerine benzeşim grubunda oluşturulan *MyAffinityGroup*.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-129">The cloud service MyHPCCNService is created in the affinity group *MyIBAffinityGroup*, and the other cloud services are created in the affinity group *MyAffinityGroup*.</span></span> <span data-ttu-id="4a6b4-130">HPC web portalı ve HPC iş Scheduler REST API baş düğümünde etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-130">The HPC Job Scheduler REST API and HPC web portal are enabled on the head node.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>    
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>NewRemoteDB</DBOption>
    <DBVersion>SQLServer2014_Enterprise</DBVersion>
    <DBServer>
      <VMName>MyDBServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>ExtraLarge</VMSize>
      <DataDiskSizeInGB>500</DataDiskSizeInGB>
    </DBServer>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>A8</VMSize>
<NodeCount>5</NodeCount>
<AffinityGroup>MyIBAffinityGroup</AffinityGroup>
  </ComputeNodes>
  <BrokerNodes>
    <VMNamePattern>MyHPCBN-%0000%</VMNamePattern>
    <ServiceName>MyHPCBNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>2</NodeCount>
  </BrokerNodes>
</IaaSClusterConfig>
```



### <a name="example-4"></a><span data-ttu-id="4a6b4-131">Örnek 4</span><span class="sxs-lookup"><span data-stu-id="4a6b4-131">Example 4</span></span>
<span data-ttu-id="4a6b4-132">Aşağıdaki yapılandırma dosyası var olan bir etki alanı ormanı HPC Pack kümede dağıtır.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-132">The following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="4a6b4-133">Yerel veritabanlarıyla iki baş düğüm kümesi olduğundan, iki Azure düğümü şablonları oluşturulur ve üç boyut Orta Azure düğümleri için Azure düğüm şablonu oluşturulur *AzureTemplate1*.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-133">The cluster has two head node with local databases, two Azure node templates are created, and three size Medium Azure nodes are created for Azure node template *AzureTemplate1*.</span></span> <span data-ttu-id="4a6b4-134">Baş düğüm yapılandırıldıktan sonra bir komut dosyası baş düğüm üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-134">A script file runs on the head node after the head node is configured.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
<VMSize>ExtraLarge</VMSize>
    <PostConfigScript>c:\MyHNPostActions.ps1</PostConfigScript>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
    <Certificate>
      <Id>2</Id>
      <PfxFile>d:\mytestcert2.pfx</PfxFile>
    </Certificate>    
  </Certificates>
  <AzureBurst>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate1</TemplateName>
      <SubscriptionId>bb9252ba-831f-4c9d-ae14-9a38e6da8ee4</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc1</ServiceName>
      <StorageAccount>myteststorage1</StorageAccount>
      <NodeCount>3</NodeCount>
      <RoleSize>Medium</RoleSize>
    </AzureNodeTemplate>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate2</TemplateName>
      <SubscriptionId>ad4b9f9f-05f2-4c74-a83f-f2eb73000e0b</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc2</ServiceName>
      <StorageAccount>myteststorage2</StorageAccount>
      <Proxy>
        <UsesStaticProxyCount>false</UsesStaticProxyCount>     
        <ProxyRatio>100</ProxyRatio>
        <ProxyRatioBase>400</ProxyRatioBase>
      </Proxy>
      <OSVersion>WindowsServer2012</OSVersion>
    </AzureNodeTemplate>
  </AzureBurst>
</IaaSClusterConfig>
```

## <a name="troubleshooting"></a><span data-ttu-id="4a6b4-135">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="4a6b4-135">Troubleshooting</span></span>
* <span data-ttu-id="4a6b4-136">**"Sanal ağ yok" hatası** -eşzamanlı olarak bir abonelik altında Azure birden çok kümeler dağıtmak için betik çalıştırırsanız, bir veya daha fazla dağıtım hatasıyla başarısız olabilir "VNet *VNet\_adı* yok".</span><span class="sxs-lookup"><span data-stu-id="4a6b4-136">**“VNet doesn’t exist” error** - If you run the script to deploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with the error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="4a6b4-137">Bu hata oluşursa, komut dosyası başarısız dağıtım için yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-137">If this error occurs, run the script again for the failed deployment.</span></span>
* <span data-ttu-id="4a6b4-138">**Azure sanal ağdan Internet erişirken sorun** - dağıtım komut dosyası kullanarak yeni bir etki alanı denetleyicisi ile bir küme oluşturma veya etki alanı denetleyicisine bir üstbilgi düğüm VM'ine el ile yükseltmek, Internet'e sanal makinelerini bağlamak sorunlarla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-138">**Problem accessing the Internet from the Azure virtual network** - If you create a cluster with a new domain controller by using the deployment script, or you manually promote a head node VM to domain controller, you may experience problems connecting the VMs to the Internet.</span></span> <span data-ttu-id="4a6b4-139">Bu sorun bir iletici DNS sunucusu etki alanı denetleyicisinde otomatik olarak yapılandırılır ve bu iletici DNS sunucusu düzgün sorunu çözmezse ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-139">This problem can occur if a forwarder DNS server is automatically configured on the domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="4a6b4-140">Etki alanı denetleyicisi ve kaldırın veya iletici yapılandırma ayarı oturumunu bu soruna geçici bir çözüm veya geçerli iletici DNS sunucusunu yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-140">To work around this problem, log on to the domain controller and either remove the forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="4a6b4-141">Bu ayar Sunucu Yöneticisi'ni yapılandırmak için **Araçları** >
    **DNS** DNS Yöneticisi'ni açın ve ardından **İleticiler**.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-141">To configure this setting, in Server Manager click **Tools** >
    **DNS** to open DNS Manager, and then double-click **Forwarders**.</span></span>
* <span data-ttu-id="4a6b4-142">**RDMA ağ yoğun Vm'lerden erişirken sorun** - Windows Server işlem eklemek veya Aracısı düğümü bir RDMA özellikli kullanarak VM'ler boyut A8 veya A9 gibi bu VM'lerin RDMA uygulama ağ bağlantısı sorunlarla karşılaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-142">**Problem accessing RDMA network from compute-intensive VMs** - If you add Windows Server compute or broker node VMs using an RDMA-capable size such as A8 or A9, you may experience problems connecting those VMs to the RDMA application network.</span></span> <span data-ttu-id="4a6b4-143">Bu sorun bir kümeye VM'ler eklendiğinde HpcVmDrivers uzantısı düzgün yüklenmemiş varsa nedenidir.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-143">One reason this problem occurs is if the HpcVmDrivers extension is not properly installed when the VMs are added to the cluster.</span></span> <span data-ttu-id="4a6b4-144">Örneğin, uzantı yükleme durumda takılmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-144">For example, the extension might be stuck in the installing state.</span></span>
  
    <span data-ttu-id="4a6b4-145">Bu sorunu geçici olarak çözmek için önce sanal makineleri uzantı durumunu denetleyin.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-145">To work around this problem, first check the state of the extension in the VMs.</span></span> <span data-ttu-id="4a6b4-146">Uzantısı düzgün yüklü değilse, HPC küme düğümleri kaldırmayı deneyin ve ardından düğümler yeniden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-146">If the extension is not properly installed, try removing the nodes from the HPC cluster and then add the nodes again.</span></span> <span data-ttu-id="4a6b4-147">Örneğin, işlem düğümü VM'ler baş düğümünde Ekle HpcIaaSNode.ps1 komut dosyası çalıştırarak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-147">For example, you can add compute node VMs by running the Add-HpcIaaSNode.ps1 script on the head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a6b4-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4a6b4-148">Next steps</span></span>
* <span data-ttu-id="4a6b4-149">Küme üzerinde bir test iş yükü çalıştırmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-149">Try running a test workload on the cluster.</span></span> <span data-ttu-id="4a6b4-150">Bir örnek için bkz: HPC paketi [Başlangıç Kılavuzu](https://technet.microsoft.com/library/jj884144).</span><span class="sxs-lookup"><span data-stu-id="4a6b4-150">For an example, see the HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>
* <span data-ttu-id="4a6b4-151">Küme dağıtımı komut dosyası ve bir HPC iş yükü çalıştırmak bir öğretici için bkz: [Excel ve SOA iş yüklerini çalıştırmak için Azure HPC Pack kümede kullanmaya başlama](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4a6b4-151">For a tutorial to script the cluster deployment and run an HPC workload, see [Get started with an HPC Pack cluster in Azure to run Excel and SOA workloads](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="4a6b4-152">Başlatabilir, durdurabilir, eklemek için HPC paketi araçları deneyin ve işlem düğümlerini, oluşturduğunuz bir kümeden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="4a6b4-152">Try HPC Pack's tools to start, stop, add, and remove compute nodes from a cluster you create.</span></span> <span data-ttu-id="4a6b4-153">Bkz: [bir HPC Pack Yönet işlem düğümleri küme Azure'da](hpcpack-cluster-node-manage.md).</span><span class="sxs-lookup"><span data-stu-id="4a6b4-153">See [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md).</span></span>
* <span data-ttu-id="4a6b4-154">Yerel bilgisayardan kümeye iş göndermek için ayarladığınız için bkz: [bir HPC Pack gönderme HPC işlerini bir şirket içi bilgisayardan küme Azure'da](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4a6b4-154">To get set up to submit jobs to the cluster from a local computer, see [Submit HPC jobs from an on-premises computer to an HPC Pack cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

