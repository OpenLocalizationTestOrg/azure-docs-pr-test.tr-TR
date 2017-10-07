---
title: "Always On kullanılabilirlik grupları Azure için bir ILB dinleyicisi aaaConfigure | Microsoft Docs"
description: "Bu öğretici hello Klasik dağıtım modeli kullanılarak oluşturulmuş kaynakları kullanır ve bir iç yük dengeleyici kullanan Azure'da bir Always On kullanılabilirlik grubu dinleyicisi oluşturur."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a>Azure'da bir ILB dinleyicisi Always On kullanılabilirlik grupları için yapılandırın
> [!div class="op_single_selector"]
> * [İç dinleyicisi](../classic/ps-sql-int-listener.md)
> * [Dış dinleyici](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a>Genel Bakış

> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede hello Klasik dağıtım modeli hello kullanımını da kapsar. En yeni dağıtımların hello Resource Manager modelini kullanmasını öneririz.

tooconfigure bir Always On kullanılabilirlik grubunda hello Resource Manager modeli için bir dinleyici bkz [Azure'da bir Always On kullanılabilirlik grubu için yük dengeleyici yapılandırma](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).

Kullanılabilirlik grubu yalnızca şirket içinde veya Azure yalnızca olan ya da karma yapılandırmalar için şirket içi ve Azure span çoğaltmaları içerebilir. Azure çoğaltmaları hello içinde bulunduğu aynı bölge veya birden çok sanal ağ kullanan birden çok bölgede. Merhaba yordamlarda bu makalede sahip olduğunuz varsayılmıştır [bir kullanılabilirlik grubu yapılandırılmış](../classic/portal-sql-alwayson-availability-groups.md) ancak henüz bir dinleyici yapılandırmadınız.

## <a name="guidelines-and-limitations-for-internal-listeners"></a>Kuralları ve sınırlamaları iç dinleyicileri
yönergeleri izleyerek konu toohello Hello Azure'bir kullanılabilirlik grubu dinleyicisiyle bir iç yük dengeleyici (ILB) kullanılır:

* Merhaba kullanılabilirlik grubu dinleyicisi, Windows Server 2008 R2, Windows Server 2012 ve Windows Server 2012 R2 üzerinde desteklenir.
* Yalnızca bir hello dinleyici olduğundan iç kullanılabilirlik grubu dinleyicisi her bulut hizmeti için desteklenen toohello ILB yapılandırılmış ve her bir bulut hizmeti için yalnızca bir ILB yok. Ancak, olası toocreate olan birden çok dış dinleyici. Daha fazla bilgi için bkz: [Azure'da Always On kullanılabilirlik grupları için dış dinleyici yapılandırın](../classic/ps-sql-ext-listener.md).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Merhaba dinleyicisi Hello erişilebilirliğini belirleme
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Bu makale, ILB kullanan bir dinleyici oluşturmaya odaklıdır. Bir genel veya dış dinleyici ihtiyacınız varsa hello yukarı ayarı ele bu makalenin sürümü için bkz. bir [dış dinleyici](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Yük dengeli VM uç noktalar ile doğrudan sunucu dönüş oluşturma
Bir ILB ilk hello betik daha sonra bu bölümde çalıştırarak oluşturun.

Yük dengeli bir uç nokta için bir Azure çoğaltması barındıran her VM oluşturun. Birden çok bölgede çoğaltmalar varsa, her çoğaltma bu bölgede aynı bulut hizmetinde hello olmalıdır hello aynı Azure sanal ağı. Birden fazla Azure bölgesine yayılan grubu çoğaltmalarının kullanılabilirlik oluşturmak için birden çok sanal ağ yapılandırma gerekir. Sanal ağ bağlantısı yapılandırma hakkında daha fazla bilgi için bkz: [sanal ağ toovirtual ağ bağlantısını yapılandır](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. Hello Azure portal, tooeach çoğaltma tooview hello ayrıntıları barındıran VM gidin.

2. Merhaba tıklatın **uç noktaları** sekmesini her VM için.

3. Bu hello doğrulayın **adı** ve **genel bağlantı noktası** toouse olmayan zaten kullanmak istediğiniz hello dinleyicisi uç noktası. Bu bölümdeki Hello örnekte hello adıdır *MyEndpoint*, ve başlangıç bağlantı noktası *1433*.

4. Yerel istemcide yükleyip hello son [PowerShell Modülü](https://azure.microsoft.com/downloads/).

5. Azure PowerShell'i başlatın.  
    Yeni bir PowerShell oturumu açılır ve hello Azure ile yüklenen yönetim modülleri.

6. `Get-AzurePublishSettingsFile` öğesini çalıştırın. Bu cmdlet tooa tarayıcı toodownload yayımlama ayarları dosyası tooa yerel bir dizine yönlendirir. Azure aboneliğiniz için oturum açma kimlik bilgileriniz istenebilir.

7. Merhaba aşağıdaki komutu çalıştırarak `Import-AzurePublishSettingsFile` hello hello yolunu komutuyla yayımlama indirdiğiniz ayarları dosyası:

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    Merhaba yayımladıktan sonra ayarları dosyası alınır, hello PowerShell oturumunda Azure aboneliğinizi yönetebilirsiniz.

8. İçin *ILB*, statik bir IP adresi atayın. Merhaba aşağıdaki komutu çalıştırarak Hello geçerli sanal ağ yapılandırmasını inceleyin:

        (Get-AzureVNetConfig).XMLConfiguration
9. Not hello *alt* hello çoğaltmaları barındıran hello VM'ler içeren hello alt ağ için ad. Bu ad hello betiği $SubnetName hello parametresinde kullanılır.

10. Not hello *VirtualNetworkSite* adlandırın ve başlangıç hello *AddressPrefix* hello çoğaltmaları barındıran hello VM'ler içeren hello alt ağ için. Kullanılabilir bir IP adresi için hem değerleri toohello geçirerek Ara `Test-AzureStaticVNetIP` komutu ile Merhaba inceleniyor *AvailableAddresses*. Örneğin, sanal ağ hello varsa adlı *MyVNet* ve başlar bir alt ağ adres aralığı *172.16.0.128*, hello aşağıdaki komut kullanılabilir adresleri listesi:

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. Merhaba kullanılabilir adresler birini seçin ve hello komut hello sonraki adımda hello $ILBStaticIP parametresinde kullanın.

12. PowerShell komut dosyası tooa metin düzenleyicisi aşağıdaki hello kopyalayın ve hello değişken değerleri toosuit ortamınızı ayarlayın. Varsayılanlar için bazı parametreler belirtildi.  

    Benzeşim grupları kullanan var olan dağıtımlar bir ILB ekleyemezsiniz. ILB gereksinimleri hakkında daha fazla bilgi için bkz: [iç yük dengeleyiciye genel bakış](../../../load-balancer/load-balancer-internal-overview.md).

    Ayrıca, kullanılabilirlik grubunuzun Azure bölgeleri yayılırsa hello betik hello bulut hizmeti ve bu veri merkezinde bulunan düğümler için her bir veri merkezinde bir kez çalıştırmanız gerekir.

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. Merhaba değişkenleri ayarladıktan sonra kopyalama hello komut dosyası hello metin düzenleyicisi tooyour PowerShell oturumu toorun onu. Merhaba istemi hala gösteriyorsa  **>>** , yeniden toomake emin hello komut dosyasını başlatır çalıştıran Enter tuşuna basın.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>KB2854082 gerekirse yüklü olduğunu doğrulayın
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Kullanılabilirlik grubu düğümler Hello güvenlik duvarı bağlantı noktalarını açın
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Merhaba kullanılabilirlik grubu dinleyicisi oluşturma

Merhaba kullanılabilirlik grubu dinleyicisi iki adımda oluşturun. İlk olarak, hello istemci erişim noktası küme kaynağı oluşturun ve bağımlılıklarını yapılandırın. İkinci olarak, PowerShell'de hello küme kaynaklarını yapılandırın.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Merhaba istemci erişim noktası oluşturun ve hello küme bağımlılıklarını yapılandırın
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>PowerShell'de Hello küme kaynaklarını yapılandırma
1. ILB için hello daha önce oluşturulan ILB hello IP adresini kullanmanız gerekir. Bu IP adresi PowerShell, komut dosyası izleyen kullanım hello tooobtain:

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. Hello VM'ler birinde hello PowerShell Betiği için işletim sistemi tooa metin düzenleyicisi kopyalayın ve ardından daha önce not ettiğiniz toohello değerleri hello değişkenleri ayarlayın.

    Windows Server 2012 veya sonraki sürümlerde, komut dosyası izleyen hello kullan:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    Windows Server 2008 R2 için komut dosyası izleyen hello kullan:

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. Set hello değişkenleri yükseltilmiş bir Windows PowerShell penceresi açın, sonra Yapıştır hello komut dosyası hello Metin Düzenleyicisi'nden, PowerShell oturumu toorun onu. Merhaba istemi hala gösteriyorsa  **>>** , Enter tuşuna basarak yeniden hello betik çalıştıran başladığından emin toomake.

4. Her VM için adımları önceki hello yineleyin.  
    Bu komut dosyası hello bulut hizmetinin başlangıç IP adresi ile başlangıç IP adresi kaynağı yapılandırır ve diğer parametreleri hello sonda bağlantı noktası gibi ayarlar. Başlangıç IP adresi kaynağı çevrimiçi duruma getirildiğinde, daha önce oluşturduğunuz hello yük dengeli uç noktasından hello araştırma noktasında yoklama toohello yanıt verebilir.

## <a name="bring-hello-listener-online"></a>Merhaba dinleyicisi çevrimiçi duruma getirin
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>İzleme öğeleri
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a>Test hello kullanılabilirlik grubu dinleyicisini (içinde hello aynı sanal ağ)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
