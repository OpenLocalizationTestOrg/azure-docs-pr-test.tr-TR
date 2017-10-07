---
title: "bir Azure SAP çoklu SID yapılandırmasında aaaCreate | Microsoft Docs"
description: "Windows sanal makinelerde Kılavuzu toohigh kullanılabilirlik SAP NetWeaver çoklu SID yapılandırması"
services: virtual-machines-windows, virtual-network, storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 0b89b4f8-6d6c-45d7-8d20-fe93430217ca
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e2a4b12928231743c59af86dab72595ad38d364b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a><span data-ttu-id="f8201-103">SAP NetWeaver çoklu SID yapılandırması oluştur</span><span class="sxs-lookup"><span data-stu-id="f8201-103">Create an SAP NetWeaver multi-SID configuration</span></span>

[load-balancer-multivip-overview]:../../../load-balancer/load-balancer-multivip-overview.md
[sap-ha-guide]:sap-high-availability-guide.md 
[sap-ha-guide-figure-6001]:./media/virtual-machines-shared-sap-high-availability-guide/6001-sap-multi-sid-ascs-scs-sid1.png
[sap-ha-guide-figure-6002]:./media/virtual-machines-shared-sap-high-availability-guide/6002-sap-multi-sid-ascs-scs.png
[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png
[sap-ha-guide-figure-6004]:./media/virtual-machines-shared-sap-high-availability-guide/6004-sap-multi-sid-dns.png
[sap-ha-guide-figure-6005]:./media/virtual-machines-shared-sap-high-availability-guide/6005-sap-multi-sid-azure-portal.png
[sap-ha-guide-figure-6006]:./media/virtual-machines-shared-sap-high-availability-guide/6006-sap-multi-sid-sios-replication.png
[networking-limits-azure-resource-manager]:../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits
[sap-ha-guide-9.1.1]:sap-high-availability-guide.md#a97ad604-9094-44fe-a364-f89cb39bf097 
[sap-ha-guide-8.8]:sap-high-availability-guide.md#f19bd997-154d-4583-a46e-7f5a69d0153c
[sap-ha-guide-8.12.3.3]:sap-high-availability-guide.md#d9c1fc8e-8710-4dff-bec2-1f535db7b006 
[sap-ha-guide-9]:sap-high-availability-guide.md#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:sap-high-availability-guide.md#31c6bd4f-51df-4057-9fdf-3fcbc619c170 
[sap-ha-guide-9.1.2]:sap-high-availability-guide.md#eb5af918-b42f-4803-bb50-eff41f84b0b0 
[sap-ha-guide-9.1.3]:sap-high-availability-guide.md#e4caaab2-e90f-4f2c-bc84-2cd2e12a9556 
[sap-ha-guide-9.1.4]:sap-high-availability-guide.md#10822f4f-32e7-4871-b63a-9b86c76ce761 
[sap-ha-guide-9.4]:sap-high-availability-guide.md#094bc895-31d4-4471-91cc-1513b64e406a 
[sap-ha-guide-9.5]:sap-high-availability-guide.md#2477e58f-c5a7-4a5d-9ae3-7b91022cafb5 
[sap-ha-guide-9.6]:sap-high-availability-guide.md#0ba4a6c1-cc37-4bcf-a8dc-025de4263772 
[sap-ha-guide-10]:sap-high-availability-guide.md#18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9

<span data-ttu-id="f8201-104">Eylül 2016'da, Microsoft, birden çok sanal IP adreslerini Azure iç yük dengeleyicisi kullanarak yönetebileceğiniz bir özellik yayımladı.</span><span class="sxs-lookup"><span data-stu-id="f8201-104">In September 2016, Microsoft released a feature where you can manage multiple virtual IP addresses by using an Azure internal load balancer.</span></span> <span data-ttu-id="f8201-105">Bu işlev hello Azure dış yük dengeleyicide zaten var.</span><span class="sxs-lookup"><span data-stu-id="f8201-105">This functionality already exists in hello Azure external load balancer.</span></span>

<span data-ttu-id="f8201-106">Bir SAP dağıtımınız varsa, bir iç yük dengeleyici toocreate Windows Küme yapılandırması SAP ASCS/SCS için hello belirtildiği gibi kullanabileceğiniz [yüksek kullanılabilirlik SAP NetWeaver Kılavuzu Windows vm'lerde] [ sap-ha-guide].</span><span class="sxs-lookup"><span data-stu-id="f8201-106">If you have an SAP deployment, you can use an internal load balancer toocreate a Windows cluster configuration for SAP ASCS/SCS, as documented in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide].</span></span>

<span data-ttu-id="f8201-107">Bu makalede nasıl toomove ek SAP ASCS/SCS yükleyerek bir tek ASCS/SCS yükleme tooan SAP çoklu SID yapılandırmadan örneklerinin mevcut bir Windows Server Yük Devretme Kümelemesi (WSFC) kümesine kümelenmiş odaklanır.</span><span class="sxs-lookup"><span data-stu-id="f8201-107">This article focuses on how toomove from a single ASCS/SCS installation tooan SAP multi-SID configuration by installing additional SAP ASCS/SCS clustered instances into an existing Windows Server Failover Clustering (WSFC) cluster.</span></span> <span data-ttu-id="f8201-108">Bu işlem tamamlandığında, bir SAP çoklu SID küme yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="f8201-108">When this process is completed, you will have configured an SAP multi-SID cluster.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f8201-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f8201-109">Prerequisites</span></span>
<span data-ttu-id="f8201-110">Zaten bir SAP ASCS/SCS örnek için kullanılan bir WSFC kümesinin hello anlatıldığı gibi yapılandırdığınız [yüksek kullanılabilirlik SAP NetWeaver Kılavuzu Windows vm'lerde] [ sap-ha-guide] ve bu diyagramda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="f8201-110">You have already configured a WSFC cluster that is used for one SAP ASCS/SCS instance, as discussed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide] and as shown in this diagram.</span></span>

![Yüksek kullanılabilirlik SAP ASCS/SCS örneği][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a><span data-ttu-id="f8201-112">Hedef mimari</span><span class="sxs-lookup"><span data-stu-id="f8201-112">Target architecture</span></span>

<span data-ttu-id="f8201-113">Merhaba tooinstall birden çok SAP ABAP ASCS veya SAP Java SCS kümelenmiş örnekler hello aynı hedeftir WSFC küme, aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="f8201-113">hello goal is tooinstall multiple SAP ABAP ASCS or SAP Java SCS clustered instances in hello same WSFC cluster, as illustrated here:</span></span>

![Azure birden çok SAP ASCS/SCS kümelenmiş örneğinde][sap-ha-guide-figure-6002]

> [!NOTE]
><span data-ttu-id="f8201-115">Her Azure iç yük dengeleyici için özel ön uç IP sınırı toohello sayısı yoktur.</span><span class="sxs-lookup"><span data-stu-id="f8201-115">There is a limit toohello number of private front-end IPs for each Azure internal load balancer.</span></span>
>
><span data-ttu-id="f8201-116">Hello en fazla bir WSFC kümesinin SAP ASCS/SCS durumlarda her Azure iç yük dengeleyici için özel ön uç IP maksimum sayısı eşit toohello sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="f8201-116">hello maximum number of SAP ASCS/SCS instances in one WSFC cluster is equal toohello maximum number of private front-end IPs for each Azure internal load balancer.</span></span>
>

<span data-ttu-id="f8201-117">Yük Dengeleyici sınırları hakkında daha fazla bilgi için bkz: "özel ön uç IP yük dengeleyici başına" [ağ sınırları: Azure Resource Manager][networking-limits-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="f8201-117">For more information about load-balancer limits, see "Private front end IP per load balancer" in [Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager].</span></span>

<span data-ttu-id="f8201-118">Merhaba tam yatay iki yüksek kullanılabilirlik SAP sistemleriyle şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="f8201-118">hello complete landscape with two high-availability SAP systems would look like this:</span></span>

![SAP yüksek kullanılabilirlik multi-SID Kurulum iki SAP sistemiyle SID][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> <span data-ttu-id="f8201-120">Merhaba Kurulum hello aşağıdaki koşulları karşılaması gerekir:</span><span class="sxs-lookup"><span data-stu-id="f8201-120">hello setup must meet hello following conditions:</span></span>
> - <span data-ttu-id="f8201-121">Merhaba SAP ASCS/SCS örnekleri paylaşması aynı hello WSFC kümesi.</span><span class="sxs-lookup"><span data-stu-id="f8201-121">hello SAP ASCS/SCS instances must share hello same WSFC cluster.</span></span>
> - <span data-ttu-id="f8201-122">Her DBMS SID kendi adanmış WSFC kümesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8201-122">Each DBMS SID must have its own dedicated WSFC cluster.</span></span>
> - <span data-ttu-id="f8201-123">Tooone SAP sistem SID ait SAP uygulama sunucuları, kendi özel VM'ler olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8201-123">SAP application servers that belong tooone SAP system SID must have their own dedicated VMs.</span></span>


## <a name="prepare-hello-infrastructure"></a><span data-ttu-id="f8201-124">Merhaba altyapıyı hazırlama</span><span class="sxs-lookup"><span data-stu-id="f8201-124">Prepare hello infrastructure</span></span>
<span data-ttu-id="f8201-125">tooprepare altyapınızı, ek SAP ASCS/SCS örnek şu parametreler hello ile yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8201-125">tooprepare your infrastructure, you can install an additional SAP ASCS/SCS instance with hello following parameters:</span></span>

| <span data-ttu-id="f8201-126">Parametre adı</span><span class="sxs-lookup"><span data-stu-id="f8201-126">Parameter name</span></span> | <span data-ttu-id="f8201-127">Değer</span><span class="sxs-lookup"><span data-stu-id="f8201-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f8201-128">SAP ASCS/SCS SID</span><span class="sxs-lookup"><span data-stu-id="f8201-128">SAP ASCS/SCS SID</span></span> |<span data-ttu-id="f8201-129">pr1 lb ascs</span><span class="sxs-lookup"><span data-stu-id="f8201-129">pr1-lb-ascs</span></span> |
| <span data-ttu-id="f8201-130">SAP DBMS iç yük dengeleyici</span><span class="sxs-lookup"><span data-stu-id="f8201-130">SAP DBMS internal load balancer</span></span> | <span data-ttu-id="f8201-131">PR5</span><span class="sxs-lookup"><span data-stu-id="f8201-131">PR5</span></span> |
| <span data-ttu-id="f8201-132">SAP sanal ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="f8201-132">SAP virtual host name</span></span> | <span data-ttu-id="f8201-133">pr5 sap cl</span><span class="sxs-lookup"><span data-stu-id="f8201-133">pr5-sap-cl</span></span> |
| <span data-ttu-id="f8201-134">SAP ASCS/SCS sanal ana bilgisayar IP adresi (ek Azure yük dengeleyici IP adresi)</span><span class="sxs-lookup"><span data-stu-id="f8201-134">SAP ASCS/SCS virtual host IP address (additional Azure load balancer IP address)</span></span> | <span data-ttu-id="f8201-135">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="f8201-135">10.0.0.50</span></span> |
| <span data-ttu-id="f8201-136">SAP ASCS/SCS örnek sayısı</span><span class="sxs-lookup"><span data-stu-id="f8201-136">SAP ASCS/SCS instance number</span></span> | <span data-ttu-id="f8201-137">50</span><span class="sxs-lookup"><span data-stu-id="f8201-137">50</span></span> |
| <span data-ttu-id="f8201-138">Ek SAP ASCS/SCS örnek için ILB araştırmasını bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="f8201-138">ILB probe port for additional SAP ASCS/SCS instance</span></span> | <span data-ttu-id="f8201-139">62350</span><span class="sxs-lookup"><span data-stu-id="f8201-139">62350</span></span> |

> [!NOTE]
> <span data-ttu-id="f8201-140">SAP ASCS/SCS küme örnekleri için her IP adresi benzersiz sonda bağlantı noktası gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f8201-140">For SAP ASCS/SCS cluster instances, each IP address requires a unique probe port.</span></span> <span data-ttu-id="f8201-141">Örneğin, bir IP adresinde bir Azure iç yük dengeleyici araştırması bağlantı noktası 62300 kullanıyorsa, herhangi bir IP adresi, yük dengeleyicide sonda bağlantı noktası 62300 kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8201-141">For example, if one IP address on an Azure internal load balancer uses probe port 62300, no other IP address on that load balancer can use probe port 62300.</span></span>
>
><span data-ttu-id="f8201-142">Sonda bağlantı noktası 62300 zaten ayrılmış olduğundan bizim amaçlar için araştırma bağlantı noktası 62350 kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="f8201-142">For our purposes, because probe port 62300 is already reserved, we are using probe port 62350.</span></span>

<span data-ttu-id="f8201-143">Merhaba mevcut WSFC kümede iki düğümü ek SAP ASCS/SCS örnekleri yükleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8201-143">You can install additional SAP ASCS/SCS instances in hello existing WSFC cluster with two nodes:</span></span>

| <span data-ttu-id="f8201-144">Sanal makine rolü</span><span class="sxs-lookup"><span data-stu-id="f8201-144">Virtual machine role</span></span> | <span data-ttu-id="f8201-145">Sanal makine ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="f8201-145">Virtual machine host name</span></span> | <span data-ttu-id="f8201-146">Statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="f8201-146">Static IP address</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f8201-147">1. küme düğümü ASCS/SCS örneği için</span><span class="sxs-lookup"><span data-stu-id="f8201-147">1st cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="f8201-148">pr1 ascs 0</span><span class="sxs-lookup"><span data-stu-id="f8201-148">pr1-ascs-0</span></span> |<span data-ttu-id="f8201-149">10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="f8201-149">10.0.0.10</span></span> |
| <span data-ttu-id="f8201-150">ASCS/SCS örneği için 2 küme düğümü</span><span class="sxs-lookup"><span data-stu-id="f8201-150">2nd cluster node for ASCS/SCS instance</span></span> |<span data-ttu-id="f8201-151">pr1 ascs 1</span><span class="sxs-lookup"><span data-stu-id="f8201-151">pr1-ascs-1</span></span> |<span data-ttu-id="f8201-152">10.0.0.9</span><span class="sxs-lookup"><span data-stu-id="f8201-152">10.0.0.9</span></span> |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a><span data-ttu-id="f8201-153">Kümelenmiş hello SAP ASCS/SCS örneği için bir sanal ana bilgisayar adı hello DNS sunucusunda oluşturun</span><span class="sxs-lookup"><span data-stu-id="f8201-153">Create a virtual host name for hello clustered SAP ASCS/SCS instance on hello DNS server</span></span>

<span data-ttu-id="f8201-154">Şu parametreler hello kullanarak hello ASCS/SCS örneğinin hello sanal ana bilgisayar adı için bir DNS girişi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f8201-154">You can create a DNS entry for hello virtual host name of hello ASCS/SCS instance by using hello following parameters:</span></span>

| <span data-ttu-id="f8201-155">Yeni SAP ASCS/SCS sanal ana bilgisayar adı</span><span class="sxs-lookup"><span data-stu-id="f8201-155">New SAP ASCS/SCS virtual host name</span></span> | <span data-ttu-id="f8201-156">İlişkili IP adresi</span><span class="sxs-lookup"><span data-stu-id="f8201-156">Associated IP address</span></span> |
| --- | --- | --- |
|<span data-ttu-id="f8201-157">pr5 sap cl</span><span class="sxs-lookup"><span data-stu-id="f8201-157">pr5-sap-cl</span></span> |<span data-ttu-id="f8201-158">10.0.0.50</span><span class="sxs-lookup"><span data-stu-id="f8201-158">10.0.0.50</span></span> |

<span data-ttu-id="f8201-159">Merhaba yeni ana bilgisayar adı ve IP adresi hello DNS Yöneticisi'ni hello ekran aşağıdaki gösterildiği gibi görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="f8201-159">hello new host name and IP address are displayed in hello DNS Manager, as shown in hello following screenshot:</span></span>

![DNS Yöneticisi'ni liste Hello vurgulama hello yeni SAP ASCS/SCS küme sanal adı ve TCP/IP adresi için DNS girişi tanımlanan][sap-ha-guide-figure-6004]

<span data-ttu-id="f8201-161">bir DNS girişi oluşturmak için hello yordam hello ana ayrıntılı açıklanan de [yüksek kullanılabilirlik SAP NetWeaver Kılavuzu Windows vm'lerde][sap-ha-guide-9.1.1].</span><span class="sxs-lookup"><span data-stu-id="f8201-161">hello procedure for creating a DNS entry is also described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9.1.1].</span></span>

> [!NOTE]
> <span data-ttu-id="f8201-162">Merhaba hello ek ASCS/SCS örneğinin toohello sanal ana bilgisayar adı atayın, yeni IP adresi gerekir olması hello toohello SAP Azure yük dengeleyiciye atanan hello yeni IP adresi ile aynı.</span><span class="sxs-lookup"><span data-stu-id="f8201-162">hello new IP address that you assign toohello virtual host name of hello additional ASCS/SCS instance must be hello same as hello new IP address that you assigned toohello SAP Azure load balancer.</span></span>
>
><span data-ttu-id="f8201-163">Senaryomuzda 10.0.0.50 hello IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="f8201-163">In our scenario, hello IP address is 10.0.0.50.</span></span>

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a><span data-ttu-id="f8201-164">PowerShell kullanarak bir IP adresi tooan mevcut Azure iç yük dengeleyici ekleme</span><span class="sxs-lookup"><span data-stu-id="f8201-164">Add an IP address tooan existing Azure internal load balancer by using PowerShell</span></span>

<span data-ttu-id="f8201-165">bir SAP ASCS/SCS örneğinde birden çok toocreate hello aynı WSFC küme, Azure iç yük dengeleyici var olan bir IP adresi tooan PowerShell tooadd kullanın.</span><span class="sxs-lookup"><span data-stu-id="f8201-165">toocreate more than one SAP ASCS/SCS instance in hello same WSFC cluster, use PowerShell tooadd an IP address tooan existing Azure internal load balancer.</span></span> <span data-ttu-id="f8201-166">Her IP adresi, kendi Yük Dengeleme kuralları, araştırma bağlantı noktası, ön uç IP havuzu ve arka uç havuzu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f8201-166">Each IP address requires its own load-balancing rules, probe port, front-end IP pool, and back-end pool.</span></span>

<span data-ttu-id="f8201-167">Merhaba aşağıdaki betiği yeni IP adresi tooan var olan yük dengeleyici ekler.</span><span class="sxs-lookup"><span data-stu-id="f8201-167">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="f8201-168">Merhaba PowerShell değişkenleri ortamınız için güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f8201-168">Update hello PowerShell variables for your environment.</span></span> <span data-ttu-id="f8201-169">Merhaba betik tüm SAP ASCS/SCS bağlantı noktaları için gereken tüm Yük Dengeleme kuralları oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="f8201-169">hello script will create all needed load-balancing rules for all SAP ASCS/SCS ports.</span></span>

```powershell

# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>
Clear-Host
$ResourceGroupName = "SAP-MULTI-SID-Landscape"      # Existing resource group name
$VNetName = "pr2-vnet"                        # Existing virtual network name
$SubnetName = "Subnet"                        # Existing subnet name
$ILBName = "pr2-lb-ascs"                      # Existing ILB name                      
$ILBIP = "10.0.0.50"                          # New IP address
$VMNames = "pr2-ascs-0","pr2-ascs-1"          # Existing cluster virtual machine names
$SAPInstanceNumber = 50                       # SAP ASCS/SCS instance number: must be a unique value for each cluster
[int]$ProbePort = "623$SAPInstanceNumber"     # Probe port: must be a unique value for each IP and load balancer

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName

$count = $ILB.FrontendIpConfigurations.Count + 1
$FrontEndConfigurationName ="lbFrontendASCS$count"
$LBProbeName = "lbProbeASCS$count"

# Get hello Azure VNet and subnet
$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

# Add second front-end and probe configuration
Write-Host "Adding new front end IP Pool '$FrontEndConfigurationName' ..." -ForegroundColor Green
$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id
$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 10  | Set-AzureRmLoadBalancer

# Get new updated configuration
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
# Get new updated LP FrontendIP COnfig
$FEConfig = Get-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

# Add new back-end configuration into existing ILB
$BackEndConfigurationName  = "backendPoolASCS$count"
Write-Host "Adding new backend Pool '$BackEndConfigurationName' ..." -ForegroundColor Green
$BEConfig = Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB | Set-AzureRmLoadBalancer

# Get new updated config
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

# Assign VM NICs toobackend pool
$BEPool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
foreach($VMName in $VMNames){
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName
        $NICName = ($VM.NetworkInterfaceIDs[0].Split('/') | select -last 1)        
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName                
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools += $BEPool
        Write-Host "Assigning network card '$NICName' of hello '$VMName' VM toohello backend pool '$BackEndConfigurationName' ..." -ForegroundColor Green
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        #start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name
}


# Create load-balancing rules
$Ports = "445","32$SAPInstanceNumber","33$SAPInstanceNumber","36$SAPInstanceNumber","39$SAPInstanceNumber","5985","81$SAPInstanceNumber","5$SAPInstanceNumber`13","5$SAPInstanceNumber`14","5$SAPInstanceNumber`16"
$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName
$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB
$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB
$HealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

Write-Host "Creating load balancing rules for hello ports: '$Ports' ... " -ForegroundColor Green

foreach ($Port in $Ports) {

        $LBConfigrulename = "lbrule$Port" + "_$count"
        Write-Host "Creating load balancing rule '$LBConfigrulename' for hello port '$Port' ..." -ForegroundColor Green

        $ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $HealthProbe -Protocol tcp -FrontendPort  $Port -BackendPort $Port -IdleTimeoutInMinutes 30 -LoadDistribution Default -EnableFloatingIP   
}

$ILB | Set-AzureRmLoadBalancer

Write-Host "Succesfully added new IP '$ILBIP' toohello internal load balancer '$ILBName'!" -ForegroundColor Green

```
<span data-ttu-id="f8201-170">Merhaba betik çalıştıktan sonra sonuçları görüntülenir hello hello Azure portal hello ekran aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="f8201-170">After hello script has run, hello results are displayed in hello Azure portal, as shown in hello following screenshot:</span></span>

![Hello Azure portalında yeni ön uç IP havuzundaki][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a><span data-ttu-id="f8201-172">Diskleri toocluster makineleri ekleyin ve hello SIOS küme paylaşım disk yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f8201-172">Add disks toocluster machines, and configure hello SIOS cluster share disk</span></span>

<span data-ttu-id="f8201-173">Her ek SAP ASCS/SCS örneği için yeni bir küme paylaşım disk eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8201-173">You must add a new cluster share disk for each additional SAP ASCS/SCS instance.</span></span> <span data-ttu-id="f8201-174">Windows Server 2012 R2 için hello WSFC küme paylaşım disk şu anda kullanımda hello SIOS DataKeeper yazılım çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="f8201-174">For Windows Server 2012 R2, hello WSFC cluster share disk currently in use is hello SIOS DataKeeper software solution.</span></span>

<span data-ttu-id="f8201-175">Aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="f8201-175">Do hello following:</span></span>
1. <span data-ttu-id="f8201-176">Ek bir ekleme disk veya diskler hello aynı boyutta (gereken toostripe) hello tooeach küme düğümleri ve biçimlendirir.</span><span class="sxs-lookup"><span data-stu-id="f8201-176">Add an additional disk or disks of hello same size (which you need toostripe) tooeach of hello cluster nodes, and format them.</span></span>
2. <span data-ttu-id="f8201-177">Depolama çoğaltma SIOS DataKeeper ile yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f8201-177">Configure storage replication with SIOS DataKeeper.</span></span>

<span data-ttu-id="f8201-178">Bu yordam hello WSFC küme makinelerde SIOS DataKeeper zaten yüklediyseniz varsayar.</span><span class="sxs-lookup"><span data-stu-id="f8201-178">This procedure assumes that you have already installed SIOS DataKeeper on hello WSFC cluster machines.</span></span> <span data-ttu-id="f8201-179">Yüklediyseniz, çoğaltma hello makineler arasında şimdi yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f8201-179">If you have installed it, you must now configure replication between hello machines.</span></span> <span data-ttu-id="f8201-180">Merhaba işlem hello ana ayrıntılı açıklanan [yüksek kullanılabilirlik SAP NetWeaver Kılavuzu Windows vm'lerde][sap-ha-guide-8.12.3.3].</span><span class="sxs-lookup"><span data-stu-id="f8201-180">hello process is described in detail in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.12.3.3].</span></span>  

![DataKeeper hello yeni SAP ASCS/SCS paylaşım disk için yansıtma zaman uyumlu][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a><span data-ttu-id="f8201-182">SAP uygulama sunucuları ve DBMS küme için sanal makineleri dağıtma</span><span class="sxs-lookup"><span data-stu-id="f8201-182">Deploy VMs for SAP application servers and DBMS cluster</span></span>

<span data-ttu-id="f8201-183">toocomplete hello altyapı hazırlık hello ikinci SAP sistemi hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="f8201-183">toocomplete hello infrastructure preparation for hello second SAP system, do hello following:</span></span>

1. <span data-ttu-id="f8201-184">SAP uygulama sunucuları için özel VM'ler dağıtın ve bunları kendi özel kullanılabilirlik grubunda yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="f8201-184">Deploy dedicated VMs for SAP application servers and put them in their own dedicated availability group.</span></span>
2. <span data-ttu-id="f8201-185">DBMS küme için özel VM'ler dağıtın ve bunları kendi özel kullanılabilirlik grubunda yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="f8201-185">Deploy dedicated VMs for DBMS cluster and put them in their own dedicated availability group.</span></span>


## <a name="install-hello-second-sap-sid2-netweaver-system"></a><span data-ttu-id="f8201-186">Merhaba ikinci SAP SID2 NetWeaver sistemini yükleyin</span><span class="sxs-lookup"><span data-stu-id="f8201-186">Install hello second SAP SID2 NetWeaver system</span></span>

<span data-ttu-id="f8201-187">İkinci bir SAP SID2 sistemi yükleme hello tam işlem hello ana açıklanan [yüksek kullanılabilirlik SAP NetWeaver Kılavuzu Windows vm'lerde][sap-ha-guide-9].</span><span class="sxs-lookup"><span data-stu-id="f8201-187">hello complete process of installing a second SAP SID2 system is described in hello main [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-9].</span></span>

<span data-ttu-id="f8201-188">Merhaba üst düzey yordam aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="f8201-188">hello high-level procedure is as follows:</span></span>

1. <span data-ttu-id="f8201-189">[Merhaba SAP ilk küme düğümüne yüklemek][sap-ha-guide-9.1.2].</span><span class="sxs-lookup"><span data-stu-id="f8201-189">[Install hello SAP first cluster node][sap-ha-guide-9.1.2].</span></span>  
 <span data-ttu-id="f8201-190">Bu adımda, yüksek kullanılabilirlik ASCS/SCS örneğinde hello ile SAP yüklemekte olduğunuz **mevcut WSFC küme düğümü 1**.</span><span class="sxs-lookup"><span data-stu-id="f8201-190">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello **EXISTING WSFC cluster node 1**.</span></span>

2. <span data-ttu-id="f8201-191">[Merhaba ASCS/SCS örneğinin Hello SAP profilini değiştirmek][sap-ha-guide-9.1.3].</span><span class="sxs-lookup"><span data-stu-id="f8201-191">[Modify hello SAP profile of hello ASCS/SCS instance][sap-ha-guide-9.1.3].</span></span>

3. <span data-ttu-id="f8201-192">[Bir araştırma bağlantı noktası yapılandırın][sap-ha-guide-9.1.4].</span><span class="sxs-lookup"><span data-stu-id="f8201-192">[Configure a probe port][sap-ha-guide-9.1.4].</span></span>  
 <span data-ttu-id="f8201-193">Bu adımda, PowerShell kullanarak bir SAP küme kaynağı SAP SID2 IP sonda bağlantı noktası yapılandırmış olursunuz.</span><span class="sxs-lookup"><span data-stu-id="f8201-193">In this step, you are configuring an SAP cluster resource SAP-SID2-IP probe port by using PowerShell.</span></span> <span data-ttu-id="f8201-194">Bu yapılandırma hello SAP ASCS/SCS küme düğümlerinden birinin yürütün.</span><span class="sxs-lookup"><span data-stu-id="f8201-194">Execute this configuration on one of hello SAP ASCS/SCS cluster nodes.</span></span>

4. <span data-ttu-id="f8201-195">[Hello veritabanı örneğini yükleme] [sap-ha-Kılavuzu-9.2].</span><span class="sxs-lookup"><span data-stu-id="f8201-195">[Install hello database instance][sap-ha-guide-9.2].</span></span>  
 <span data-ttu-id="f8201-196">Bu adımda, adanmış bir WSFC kümesinde DBMS yüklüyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="f8201-196">In this step, you are installing DBMS on a dedicated WSFC cluster.</span></span>

5. <span data-ttu-id="f8201-197">[Hello ikinci küme düğümü yükleme] [sap-ha-Kılavuzu-9.3].</span><span class="sxs-lookup"><span data-stu-id="f8201-197">[Install hello second cluster node][sap-ha-guide-9.3].</span></span>  
 <span data-ttu-id="f8201-198">Bu adımda, hello mevcut WSFC Küme düğüm 2 üzerinde bir yüksek kullanılabilirlik ASCS/SCS örneği SAP yüklüyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="f8201-198">In this step, you are installing SAP with a high-availability ASCS/SCS instance on hello existing WSFC cluster node 2.</span></span>

6. <span data-ttu-id="f8201-199">Merhaba SAP ASCS/SCS örneği ve ProbePort için Windows Güvenlik Duvarı bağlantı noktalarını açın.</span><span class="sxs-lookup"><span data-stu-id="f8201-199">Open Windows Firewall ports for hello SAP ASCS/SCS instance and ProbePort.</span></span>  
 <span data-ttu-id="f8201-200">SAP ASCS/SCS örnekleri için kullanılan her iki küme düğümlerinde SAP ASCS/SCS tarafından kullanılan tüm Windows Güvenlik Duvarı bağlantı noktaları açıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="f8201-200">On both cluster nodes that are used for SAP ASCS/SCS instances, you are opening all Windows Firewall ports that are used by SAP ASCS/SCS.</span></span> <span data-ttu-id="f8201-201">Bu bağlantı noktaları hello listelenen [yüksek kullanılabilirlik SAP NetWeaver Kılavuzu Windows vm'lerde][sap-ha-guide-8.8].</span><span class="sxs-lookup"><span data-stu-id="f8201-201">These ports are listed in hello [guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide-8.8].</span></span>  
 <span data-ttu-id="f8201-202">Ayrıca bizim senaryoda 62350 olan hello Azure iç yük dengeleyici araştırması bağlantı noktası açın.</span><span class="sxs-lookup"><span data-stu-id="f8201-202">Also open hello Azure internal load balancer probe port, which is 62350 in our scenario.</span></span>

7. <span data-ttu-id="f8201-203">[Merhaba başlangıç türünü hello SAP ERS Windows hizmeti örneğinin][sap-ha-guide-9.4].</span><span class="sxs-lookup"><span data-stu-id="f8201-203">[Change hello start type of hello SAP ERS Windows service instance][sap-ha-guide-9.4].</span></span>

8. <span data-ttu-id="f8201-204">[Merhaba SAP birincil uygulama sunucusu yüklemeniz] [ sap-ha-guide-9.5] hello yeni VM ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="f8201-204">[Install hello SAP primary application server][sap-ha-guide-9.5] on hello new dedicated VM.</span></span>

9. <span data-ttu-id="f8201-205">[Merhaba SAP ek uygulama sunucusu yüklemeniz] [ sap-ha-guide-9.6] hello yeni VM ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="f8201-205">[Install hello SAP additional application server][sap-ha-guide-9.6] on hello new dedicated VM.</span></span>

10. <span data-ttu-id="f8201-206">[Test hello SAP ASCS/SCS örneği yük devretme ve SIOS çoğaltma][sap-ha-guide-10].</span><span class="sxs-lookup"><span data-stu-id="f8201-206">[Test hello SAP ASCS/SCS instance failover and SIOS replication][sap-ha-guide-10].</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8201-207">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f8201-207">Next steps</span></span>

- <span data-ttu-id="f8201-208">[Ağ sınırları: Azure Resource Manager][networking-limits-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="f8201-208">[Networking limits: Azure Resource Manager][networking-limits-azure-resource-manager]</span></span>
- <span data-ttu-id="f8201-209">[Azure için birden çok Vip yük dengeleyici][load-balancer-multivip-overview]</span><span class="sxs-lookup"><span data-stu-id="f8201-209">[Multiple VIPs for Azure Load Balancer][load-balancer-multivip-overview]</span></span>
- <span data-ttu-id="f8201-210">[Windows sanal makineleri üzerinde yüksek kullanılabilirlik SAP NetWeaver Kılavuzu][sap-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="f8201-210">[Guide for high-availability SAP NetWeaver on Windows VMs][sap-ha-guide]</span></span>
