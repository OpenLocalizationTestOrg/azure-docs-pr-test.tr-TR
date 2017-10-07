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
# <a name="create-an-sap-netweaver-multi-sid-configuration"></a>SAP NetWeaver çoklu SID yapılandırması oluştur

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

Eylül 2016'da, Microsoft, birden çok sanal IP adreslerini Azure iç yük dengeleyicisi kullanarak yönetebileceğiniz bir özellik yayımladı. Bu işlev hello Azure dış yük dengeleyicide zaten var.

Bir SAP dağıtımınız varsa, bir iç yük dengeleyici toocreate Windows Küme yapılandırması SAP ASCS/SCS için hello belirtildiği gibi kullanabileceğiniz [yüksek kullanılabilirlik SAP NetWeaver Kılavuzu Windows vm'lerde] [ sap-ha-guide].

Bu makalede nasıl toomove ek SAP ASCS/SCS yükleyerek bir tek ASCS/SCS yükleme tooan SAP çoklu SID yapılandırmadan örneklerinin mevcut bir Windows Server Yük Devretme Kümelemesi (WSFC) kümesine kümelenmiş odaklanır. Bu işlem tamamlandığında, bir SAP çoklu SID küme yapılandırılmış.


## <a name="prerequisites"></a>Ön koşullar
Zaten bir SAP ASCS/SCS örnek için kullanılan bir WSFC kümesinin hello anlatıldığı gibi yapılandırdığınız [yüksek kullanılabilirlik SAP NetWeaver Kılavuzu Windows vm'lerde] [ sap-ha-guide] ve bu diyagramda gösterildiği gibi.

![Yüksek kullanılabilirlik SAP ASCS/SCS örneği][sap-ha-guide-figure-6001]

## <a name="target-architecture"></a>Hedef mimari

Merhaba tooinstall birden çok SAP ABAP ASCS veya SAP Java SCS kümelenmiş örnekler hello aynı hedeftir WSFC küme, aşağıda gösterildiği gibi:

![Azure birden çok SAP ASCS/SCS kümelenmiş örneğinde][sap-ha-guide-figure-6002]

> [!NOTE]
>Her Azure iç yük dengeleyici için özel ön uç IP sınırı toohello sayısı yoktur.
>
>Hello en fazla bir WSFC kümesinin SAP ASCS/SCS durumlarda her Azure iç yük dengeleyici için özel ön uç IP maksimum sayısı eşit toohello sayısıdır.
>

Yük Dengeleyici sınırları hakkında daha fazla bilgi için bkz: "özel ön uç IP yük dengeleyici başına" [ağ sınırları: Azure Resource Manager][networking-limits-azure-resource-manager].

Merhaba tam yatay iki yüksek kullanılabilirlik SAP sistemleriyle şöyle olabilir:

![SAP yüksek kullanılabilirlik multi-SID Kurulum iki SAP sistemiyle SID][sap-ha-guide-figure-6003]

> [!IMPORTANT]
> Merhaba Kurulum hello aşağıdaki koşulları karşılaması gerekir:
> - Merhaba SAP ASCS/SCS örnekleri paylaşması aynı hello WSFC kümesi.
> - Her DBMS SID kendi adanmış WSFC kümesi olması gerekir.
> - Tooone SAP sistem SID ait SAP uygulama sunucuları, kendi özel VM'ler olması gerekir.


## <a name="prepare-hello-infrastructure"></a>Merhaba altyapıyı hazırlama
tooprepare altyapınızı, ek SAP ASCS/SCS örnek şu parametreler hello ile yükleyebilirsiniz:

| Parametre adı | Değer |
| --- | --- |
| SAP ASCS/SCS SID |pr1 lb ascs |
| SAP DBMS iç yük dengeleyici | PR5 |
| SAP sanal ana bilgisayar adı | pr5 sap cl |
| SAP ASCS/SCS sanal ana bilgisayar IP adresi (ek Azure yük dengeleyici IP adresi) | 10.0.0.50 |
| SAP ASCS/SCS örnek sayısı | 50 |
| Ek SAP ASCS/SCS örnek için ILB araştırmasını bağlantı noktası | 62350 |

> [!NOTE]
> SAP ASCS/SCS küme örnekleri için her IP adresi benzersiz sonda bağlantı noktası gerektirir. Örneğin, bir IP adresinde bir Azure iç yük dengeleyici araştırması bağlantı noktası 62300 kullanıyorsa, herhangi bir IP adresi, yük dengeleyicide sonda bağlantı noktası 62300 kullanabilirsiniz.
>
>Sonda bağlantı noktası 62300 zaten ayrılmış olduğundan bizim amaçlar için araştırma bağlantı noktası 62350 kullanıyoruz.

Merhaba mevcut WSFC kümede iki düğümü ek SAP ASCS/SCS örnekleri yükleyebilirsiniz:

| Sanal makine rolü | Sanal makine ana bilgisayar adı | Statik IP adresi |
| --- | --- | --- |
| 1. küme düğümü ASCS/SCS örneği için |pr1 ascs 0 |10.0.0.10 |
| ASCS/SCS örneği için 2 küme düğümü |pr1 ascs 1 |10.0.0.9 |

### <a name="create-a-virtual-host-name-for-hello-clustered-sap-ascsscs-instance-on-hello-dns-server"></a>Kümelenmiş hello SAP ASCS/SCS örneği için bir sanal ana bilgisayar adı hello DNS sunucusunda oluşturun

Şu parametreler hello kullanarak hello ASCS/SCS örneğinin hello sanal ana bilgisayar adı için bir DNS girişi oluşturabilirsiniz:

| Yeni SAP ASCS/SCS sanal ana bilgisayar adı | İlişkili IP adresi |
| --- | --- | --- |
|pr5 sap cl |10.0.0.50 |

Merhaba yeni ana bilgisayar adı ve IP adresi hello DNS Yöneticisi'ni hello ekran aşağıdaki gösterildiği gibi görüntülenir:

![DNS Yöneticisi'ni liste Hello vurgulama hello yeni SAP ASCS/SCS küme sanal adı ve TCP/IP adresi için DNS girişi tanımlanan][sap-ha-guide-figure-6004]

bir DNS girişi oluşturmak için hello yordam hello ana ayrıntılı açıklanan de [yüksek kullanılabilirlik SAP NetWeaver Kılavuzu Windows vm'lerde][sap-ha-guide-9.1.1].

> [!NOTE]
> Merhaba hello ek ASCS/SCS örneğinin toohello sanal ana bilgisayar adı atayın, yeni IP adresi gerekir olması hello toohello SAP Azure yük dengeleyiciye atanan hello yeni IP adresi ile aynı.
>
>Senaryomuzda 10.0.0.50 hello IP adresidir.

### <a name="add-an-ip-address-tooan-existing-azure-internal-load-balancer-by-using-powershell"></a>PowerShell kullanarak bir IP adresi tooan mevcut Azure iç yük dengeleyici ekleme

bir SAP ASCS/SCS örneğinde birden çok toocreate hello aynı WSFC küme, Azure iç yük dengeleyici var olan bir IP adresi tooan PowerShell tooadd kullanın. Her IP adresi, kendi Yük Dengeleme kuralları, araştırma bağlantı noktası, ön uç IP havuzu ve arka uç havuzu gerektirir.

Merhaba aşağıdaki betiği yeni IP adresi tooan var olan yük dengeleyici ekler. Merhaba PowerShell değişkenleri ortamınız için güncelleştirin. Merhaba betik tüm SAP ASCS/SCS bağlantı noktaları için gereken tüm Yük Dengeleme kuralları oluşturacaksınız.

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
Merhaba betik çalıştıktan sonra sonuçları görüntülenir hello hello Azure portal hello ekran aşağıdaki gösterildiği gibi:

![Hello Azure portalında yeni ön uç IP havuzundaki][sap-ha-guide-figure-6005]

### <a name="add-disks-toocluster-machines-and-configure-hello-sios-cluster-share-disk"></a>Diskleri toocluster makineleri ekleyin ve hello SIOS küme paylaşım disk yapılandırma

Her ek SAP ASCS/SCS örneği için yeni bir küme paylaşım disk eklemeniz gerekir. Windows Server 2012 R2 için hello WSFC küme paylaşım disk şu anda kullanımda hello SIOS DataKeeper yazılım çözümüdür.

Aşağıdaki hello:
1. Ek bir ekleme disk veya diskler hello aynı boyutta (gereken toostripe) hello tooeach küme düğümleri ve biçimlendirir.
2. Depolama çoğaltma SIOS DataKeeper ile yapılandırın.

Bu yordam hello WSFC küme makinelerde SIOS DataKeeper zaten yüklediyseniz varsayar. Yüklediyseniz, çoğaltma hello makineler arasında şimdi yapılandırmanız gerekir. Merhaba işlem hello ana ayrıntılı açıklanan [yüksek kullanılabilirlik SAP NetWeaver Kılavuzu Windows vm'lerde][sap-ha-guide-8.12.3.3].  

![DataKeeper hello yeni SAP ASCS/SCS paylaşım disk için yansıtma zaman uyumlu][sap-ha-guide-figure-6006]

### <a name="deploy-vms-for-sap-application-servers-and-dbms-cluster"></a>SAP uygulama sunucuları ve DBMS küme için sanal makineleri dağıtma

toocomplete hello altyapı hazırlık hello ikinci SAP sistemi hello aşağıdaki:

1. SAP uygulama sunucuları için özel VM'ler dağıtın ve bunları kendi özel kullanılabilirlik grubunda yerleştirin.
2. DBMS küme için özel VM'ler dağıtın ve bunları kendi özel kullanılabilirlik grubunda yerleştirin.


## <a name="install-hello-second-sap-sid2-netweaver-system"></a>Merhaba ikinci SAP SID2 NetWeaver sistemini yükleyin

İkinci bir SAP SID2 sistemi yükleme hello tam işlem hello ana açıklanan [yüksek kullanılabilirlik SAP NetWeaver Kılavuzu Windows vm'lerde][sap-ha-guide-9].

Merhaba üst düzey yordam aşağıdaki gibidir:

1. [Merhaba SAP ilk küme düğümüne yüklemek][sap-ha-guide-9.1.2].  
 Bu adımda, yüksek kullanılabilirlik ASCS/SCS örneğinde hello ile SAP yüklemekte olduğunuz **mevcut WSFC küme düğümü 1**.

2. [Merhaba ASCS/SCS örneğinin Hello SAP profilini değiştirmek][sap-ha-guide-9.1.3].

3. [Bir araştırma bağlantı noktası yapılandırın][sap-ha-guide-9.1.4].  
 Bu adımda, PowerShell kullanarak bir SAP küme kaynağı SAP SID2 IP sonda bağlantı noktası yapılandırmış olursunuz. Bu yapılandırma hello SAP ASCS/SCS küme düğümlerinden birinin yürütün.

4. [Hello veritabanı örneğini yükleme] [sap-ha-Kılavuzu-9.2].  
 Bu adımda, adanmış bir WSFC kümesinde DBMS yüklüyorsunuz.

5. [Hello ikinci küme düğümü yükleme] [sap-ha-Kılavuzu-9.3].  
 Bu adımda, hello mevcut WSFC Küme düğüm 2 üzerinde bir yüksek kullanılabilirlik ASCS/SCS örneği SAP yüklüyorsunuz.

6. Merhaba SAP ASCS/SCS örneği ve ProbePort için Windows Güvenlik Duvarı bağlantı noktalarını açın.  
 SAP ASCS/SCS örnekleri için kullanılan her iki küme düğümlerinde SAP ASCS/SCS tarafından kullanılan tüm Windows Güvenlik Duvarı bağlantı noktaları açıyorsunuz. Bu bağlantı noktaları hello listelenen [yüksek kullanılabilirlik SAP NetWeaver Kılavuzu Windows vm'lerde][sap-ha-guide-8.8].  
 Ayrıca bizim senaryoda 62350 olan hello Azure iç yük dengeleyici araştırması bağlantı noktası açın.

7. [Merhaba başlangıç türünü hello SAP ERS Windows hizmeti örneğinin][sap-ha-guide-9.4].

8. [Merhaba SAP birincil uygulama sunucusu yüklemeniz] [ sap-ha-guide-9.5] hello yeni VM ayrılmış.

9. [Merhaba SAP ek uygulama sunucusu yüklemeniz] [ sap-ha-guide-9.6] hello yeni VM ayrılmış.

10. [Test hello SAP ASCS/SCS örneği yük devretme ve SIOS çoğaltma][sap-ha-guide-10].

## <a name="next-steps"></a>Sonraki adımlar

- [Ağ sınırları: Azure Resource Manager][networking-limits-azure-resource-manager]
- [Azure için birden çok Vip yük dengeleyici][load-balancer-multivip-overview]
- [Windows sanal makineleri üzerinde yüksek kullanılabilirlik SAP NetWeaver Kılavuzu][sap-ha-guide]
