---
title: "aaaConfigure her zaman üzerinde kullanılabilirlik grubu dinleyicileri – Microsoft Azure | Microsoft Docs"
description: "Kullanılabilirlik grubu dinleyicileri hello Azure Resource Manager modeli, iç yük dengeleyiciye sahip bir veya daha fazla IP adresi kullanarak yapılandırın."
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a>Bir veya daha fazla Always On kullanılabilirlik grubu dinleyicileri - Kaynak Yöneticisi'ni yapılandırma
Bu konuda gösterilmektedir nasıl yapılır:

* Bir iç yük dengeleyici için PowerShell cmdlet'lerini kullanarak SQL Server kullanılabilirlik gruplarını oluşturun.
* Ek IP adreslerini tooa yük dengeleyici için birden çok kullanılabilirlik grubu ekleyin. 

Bir kullanılabilirlik grubu dinleyicisi, istemcilerin toofor veritabanı erişimi bağlanmasını bir sanal ağ adıdır. Azure sanal makinelerde hello dinleyici için başlangıç IP adresi bir yük dengeleyici tutar. Merhaba yük dengeleyici yollar hello araştırma bağlantı noktasında dinleme SQL Server'ın toohello örneğinin trafiği. Genellikle, bir iç yük dengeleyicisi bir kullanılabilirlik grubu kullanır. Azure iç yük dengeleyiciye bir veya daha çok IP adreslerini barındırabilir. Her IP adresi belirli araştırma bağlantı noktasını kullanır. Bu belge gösterir nasıl toouse PowerShell toocreate bir yük dengeleyici veya IP adresleri tooan var olan yük dengeleyici için SQL Server kullanılabilirlik gruplarını ekleyin. 

birden çok IP adresleri tooan iç yük dengeleyici yeni tooAzure edilmiştir ve yalnızca Resource Manager modelinde kullanılabilir yeteneği tooassign hello. toocomplete bu görev bir SQL Server kullanılabilirlik grubu dağıtılan Resource Manager modelinde Azure sanal makinelerde toohave gerekir. Her iki SQL Server sanal makineleri toohello ait olmalıdır aynı kullanılabilirlik kümesi. Merhaba kullanabilirsiniz [Microsoft şablonu](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically Azure Kaynak Yöneticisi'nde hello kullanılabilirlik grubu oluşturun. Bu şablon, sizin için hello iç yük dengeleyici gibi hello kullanılabilirlik grubu otomatik olarak oluşturur. İsterseniz, aşağıdakileri yapabilirsiniz [el ile bir Always On kullanılabilirlik grubu yapılandırmak](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

Bu konu, kullanılabilirlik grupları zaten yapılandırılmış olmasını gerektirir.  

İlgili Konular şunlardır:

* [Azure VM (GUI) AlwaysOn Kullanılabilirlik Grupları Yapılandırma](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Azure Resource Manager ve PowerShell kullanarak VNet-VNet bağlantı yapılandırma](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a>Merhaba Windows Güvenlik Duvarı'nı yapılandırma
Merhaba Windows Güvenlik Duvarı tooallow SQL Server erişimi yapılandırın. Merhaba güvenlik duvarı kuralları hello SQL Server örneği ve hello dinleyicisi yoklama TCP bağlantıları toohello bağlantı noktalarını kullanma izin verir. Ayrıntılı yönergeler için bkz: [veritabanı altyapısı erişimi için Windows Güvenlik Duvarı Yapılandırma](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1). Merhaba sonda bağlantı noktası ve hello SQL Server bağlantı noktası için bir gelen kuralı oluşturun.

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a>Örnek komut dosyası: PowerShell ile bir iç yük dengeleyici oluşturma
> [!NOTE]
> Kullanılabilirlik grubu ile Merhaba oluşturduysanız [Microsoft şablonu](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello iç yük dengeleyici zaten oluşturuldu. 
> 
> 

Merhaba aşağıdaki PowerShell betiğini bir iç yük dengeleyici oluşturur, hello Yük Dengeleme kuralları yapılandırır ve hello yük dengeleyici için bir IP adresini ayarlar. toorun hello komut dosyası, Windows PowerShell ISE açın ve hello betik bölmesinde hello betiğini yapıştırın. Kullanım `Login-AzureRMAccount` tooPowerShell toolog. Birden çok Azure aboneliğiniz varsa, kullanmak `Select-AzureRmSubscription ` tooset hello abonelik. 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <a name="Add-IP"></a>Örnek komut dosyası: bir IP adresi tooan varolan yük dengeleyicisi PowerShell ile ekleme
bir kullanılabilirlik grubu birden çok toouse bir ek IP adresi toohello yük dengeleyiciye ekleyin. Her IP adresi, kendi Yük Dengeleme kuralı, araştırma bağlantı noktası ve ön bağlantı noktası gerektirir.

Merhaba ön uç bağlantı noktası uygulamaları tooconnect toohello SQL Server örneğini kullan hello bağlantı noktasıdır. IP adresleri farklı kullanılabilirlik grupları kullanabilir hello aynı ön uç bağlantı noktası.

> [!NOTE]
> SQL Server kullanılabilirlik grupları için her IP adresi belirli sonda bağlantı noktası gerektirir. Örneğin, bir IP adresi bir yük dengeleyicideki sonda bağlantı noktası 59999 kullanıyorsa, herhangi bir IP adresi üzerinde bu yük dengeleyici araştırması bağlantı noktası 59999 kullanabilirsiniz.

* Yük Dengeleyici sınırları hakkında daha fazla bilgi için bkz: **özel ön uç IP yük dengeleyici başına** altında [ağ sınırları - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).
* Kullanılabilirlik grubu sınırları hakkında daha fazla bilgi için bkz: [kısıtlamaları (kullanılabilirlik grupları)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).

Merhaba aşağıdaki betiği yeni IP adresi tooan var olan yük dengeleyici ekler. Merhaba ILB hello dinleyicisi bağlantı noktası hello Yükü Dengeleme ön uç bağlantı noktasını kullanır. Bu bağlantı noktası, SQL Server üzerinde dinleme hello bağlantı noktası olabilir. SQL Server'ın varsayılan örnekleri için başlangıç bağlantı noktası 1433'tür. Merhaba Yük Dengeleme kuralı bir kullanılabilirlik grubu için bir kayan IP (doğrudan sunucu dönüşü) hello arka uç bağlantı noktası olacak şekilde hello aynı hello ön uç bağlantı noktası olarak gerektirir. Merhaba değişkenleri ortamınız için güncelleştirin. 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-hello-listener"></a>Merhaba dinleyicisini yapılandırın

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a>SQL Server Management Studio'da Hello dinleyicisi bağlantı noktası ayarlama

1. SQL Server Management Studio'yu başlatın ve toohello birincil çoğaltma bağlanın.

1. Çok gidin**AlwaysOn yüksek kullanılabilirlik** | **kullanılabilirlik grupları** | **kullanılabilirlik grubu dinleyicileri**. 

1. Yük Devretme Kümesi Yöneticisi'nde oluşturulan hello dinleyici adı görmelisiniz. Merhaba dinleyicisi adını sağ tıklatıp **özellikleri**.

1. Merhaba, **bağlantı noktası** kutusunda, daha önce kullandığınız $EndpointPort hello kullanarak hello hello kullanılabilirlik grubu dinleyicisinin bağlantı noktası numarası belirtin (1433 olduğu hello varsayılan), ardından **Tamam**.

## <a name="test-hello-connection-toohello-listener"></a>Test hello bağlantı toohello dinleyicisi

tootest hello bağlantısı:

1. RDP tooa hello SQL Server aynı sanal ağ, ancak kendi hello çoğaltma. Bu olması hello hello kümedeki diğer SQL Server.

1. Kullanım **sqlcmd** yardımcı programı tootest hello bağlantı. Örneğin, komut dosyası izleyen hello kurar bir **sqlcmd** bağlantı toohello birincil çoğaltma Windows kimlik doğrulaması ile Merhaba dinleyicisi aracılığıyla:
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    Merhaba dinleyicisi dışında bir bağlantı noktası kullanıyorsa, varsayılan hello (1433) bağlantı noktası, başlangıç bağlantı noktası başlangıç bağlantı dizesinde belirtin. Örneğin, hello aşağıdaki sqlcmd komut tooa dinleyicisi bağlantı noktası 1435 bağlanır: 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Merhaba SQLCMD bağlantı toowhichever örneğini SQL Server konakları hello birincil çoğaltma otomatik olarak bağlanır. 

> [!NOTE]
> Belirttiğiniz başlangıç bağlantı noktası hem SQL sunucuları hello güvenlik duvarı açık olduğundan emin olun. Her iki sunucuyu hello kullandığınız TCP bağlantı noktası için bir gelen kuralı gerektirir. Bkz: [Ekle veya güvenlik duvarı kuralını Düzenle](http://technet.microsoft.com/library/cc753558.aspx) daha fazla bilgi için. 
> 
> 

## <a name="guidelines-and-limitations"></a>Kılavuzlar ve sınırlamalar
Kullanılabilirlik grubu dinleyicisi iç yük dengeleyicisi kullanarak azure'da yönergeleri izleyerek hello dikkat edin:

* Bir iç yük dengeleyici ile size yalnızca hello içinde hello dinleyicisi gelen erişim aynı sanal ağ.


## <a name="for-more-information"></a>Daha fazla bilgi için
Daha fazla bilgi için bkz: [yapılandırma Always On kullanılabilirlik grubu Azure VM'de el ile](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

## <a name="powershell-cmdlets"></a>PowerShell cmdlet'leri
PowerShell cmdlet'leri toocreate Azure sanal makineler için bir iç yük dengeleyici aşağıdaki hello kullanın.

* [AzureRmLoadBalancer yeni](http://msdn.microsoft.com/library/mt619450.aspx) bir yük dengeleyici oluşturur. 
* [AzureRMLoadBalancerFrontendIpConfig yeni](http://msdn.microsoft.com/library/mt603510.aspx) bir yük dengeleyici için bir ön uç IP yapılandırmasını oluşturur. 
* [AzureRmLoadBalancerRuleConfig yeni](http://msdn.microsoft.com/library/mt619391.aspx) bir yük dengeleyici için bir kural yapılandırma oluşturur. 
* [AzureRmLoadBalancerBackendAddressPoolConfig yeni](http://msdn.microsoft.com/library/mt603791.aspx) bir yük dengeleyici için arka uç adres havuzu yapılandırması oluşturur. 
* [AzureRmLoadBalancerProbeConfig yeni](http://msdn.microsoft.com/library/mt603847.aspx) bir yük dengeleyici için bir araştırma yapılandırma oluşturur.
* [Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) bir yük dengeleyici Azure kaynak grubundan kaldırır.
