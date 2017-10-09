---
title: "Always On kullanılabilirlik grupları için dış dinleyici aaaConfigure | Microsoft Docs"
description: "Bu öğretici yetenekte, harici olarak erişilebilir olan kullanarak azure'da bir her zaman üzerinde kullanılabilirlik grubu dinleyicisi oluşturma adımlarını genel sanal IP adresi hello ilişkili bulut hizmeti hello."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a2453032-94ab-4775-b976-c74d24716728
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: f8e2110bcc25d9cb7653675cb4ae5c8d717b6902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-external-listener-for-always-on-availability-groups-in-azure"></a>Always On kullanılabilirlik grupları için dış dinleyici Azure'da yapılandırın
> [!div class="op_single_selector"]
> * [İç dinleyicisi](../classic/ps-sql-int-listener.md)
> * [Dış dinleyici](../classic/ps-sql-ext-listener.md)
> 
> 

Bu konuda gösterilmektedir nasıl tooconfigure bir her zaman üzerinde kullanılabilirlik üzerinde Dışarıdan erişilebilen grubu için bir dinleyici hello Internet. Bu hello bulut hizmetin ilişkilendirerek mümkün hale getirilir **ortak sanal IP (VIP)** hello dinleyicisi adresiyle.

> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

Kullanılabilirlik grubu, şirket içi yalnızca Azure yalnızca çoğaltmaları içermiyor ya da şirket içi ve Azure karma yapılandırmalar için span. Azure çoğaltmaları hello içinde bulunduğu aynı bölge veya birden çok sanal ağlar (Vnet'ler) kullanarak birden çok bölgede. Merhaba adımları zaten sahip olduğunuzu varsayar [bir kullanılabilirlik grubu yapılandırılmış](../classic/portal-sql-alwayson-availability-groups.md) ancak dinleyici yapılandırılmamış.

## <a name="guidelines-and-limitations-for-external-listeners"></a>Kuralları ve sınırlamaları dış dinleyicileri
Merhaba bulut hizmeti pubic VIP adresi kullanarak dağıtıyorsanız azure'da hello kullanılabilirlik grubu dinleyicisi hakkında yönergeleri izleyerek hello dikkat edin:

* Merhaba kullanılabilirlik grubu dinleyicisi, Windows Server 2008 R2, Windows Server 2012 ve Windows Server 2012 R2 üzerinde desteklenir.
* Merhaba istemci uygulaması, kullanılabilirlik grubunuzun VM'ler içeren bir hello daha farklı bir bulut hizmeti bulunması gerekir. Bulut hizmeti Azure desteklemiyor doğrudan sunucu dönüşü istemci ve sunucu hello aynı.
* Varsayılan olarak, bu makaledeki adımları hello nasıl tooconfigure bir dinleyici toouse hello bulut hizmeti sanal IP (VIP) adresi gösterir. Ancak, olası tooreserve olduğu ve bulut hizmetiniz için birden çok VIP adresleri oluşturun. Bu, her birden çok dinleyici farklı bir VIP ile ilişkili Bu makale toocreate toouse hello adımları sağlar. Nasıl toocreate birden çok VIP adresini bakın hakkında bilgi için [bulut hizmeti başına birden çok Vip](../../../load-balancer/load-balancer-multivip.md).
* Karma bir ortamınız için bir dinleyici oluşturuyorsanız hello şirket içi ağ bağlantısı toohello olmalıdır toplama toohello ortak Internet siteden siteye VPN hello Azure sanal ağı ile. Hello zaman Azure alt ağ, hello kullanılabilirlik grubu dinleyicisi yalnızca hello genel IP adresi hello ilgili bulut hizmeti tarafından erişilebilir.
* Şu desteklenmeyen toocreate aynı bulut hizmetine da olduğu kullanarak bir iç dinleyicisi hello içinde dış dinleyici hello iç yük dengeleyici (ILB).

## <a name="determine-hello-accessibility-of-hello-listener"></a>Merhaba dinleyicisi Hello erişilebilirliğini belirleme
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

Bu makalede kullanan bir dinleyici oluşturmaya odaklıdır **dış Yük Dengeleme**. Özel tooyour sanal ağ bir dinleyici istiyorsanız, bu makalenin ayarlamak için adımları sağlar hello sürümü bakın bir [ILB ile dinleyicisi](../classic/ps-sql-int-listener.md)

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a>Yük dengeli VM uç noktalar ile doğrudan sunucu dönüş oluşturma
Dış Yük Dengeleme, sanal makineleri barındıran hello bulut hizmeti hello sanal hello ortak sanal IP adresini kullanır. Bu nedenle, değil toocreate gerekir veya hello yük dengeleyici, bu durumda yapılandırın.

Bir Azure çoğaltma barındıran her VM için bir yük dengeli uç noktası oluşturmanız gerekir. Birden çok bölgede çoğaltmalar varsa, her çoğaltma bu bölgede aynı bulut hizmetinde hello olmalıdır hello aynı sanal ağı. Birden fazla Azure bölgesine yayılan kullanılabilirlik grubu oluşturma çoğaltmaları birden çok sanal ağlar yapılandırma gerektirir. Çapraz VNet bağlantı yapılandırma hakkında daha fazla bilgi için bkz: [yapılandırma VNet tooVNet bağlantı](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

1. Hello Azure portal'de, çoğaltma ve görünüm hello ayrıntıları barındırma VM tooeach gidin.
2. Merhaba tıklatın **uç noktaları** hello VM'lerin her birinde sekmesi.
3. Bu hello doğrulayın **adı** ve **genel bağlantı noktası** hello dinleyicisi uç noktasını toouse değil zaten kullanımda olan istediğiniz. Hello aşağıdaki örnekte, "MyEndpoint" Merhaba adıdır ve başlangıç bağlantı noktası "1433" tür.
4. Yerel istemcide, indirme ve yükleme [hello son PowerShell Modülü](https://azure.microsoft.com/downloads/).
5. Başlatma **Azure PowerShell**. Oturumu açılmış yeni bir PowerShell yüklenen Azure yönetim modülleri hello.
6. Çalıştırma **Get-AzurePublishSettingsFile**. Bu cmdlet tooa tarayıcı toodownload yayımlama ayarları dosyası tooa yerel bir dizine yönlendirir. Azure aboneliğiniz için oturum açma kimlik bilgileriniz istenebilir.
7. Merhaba çalıştırmak **Import-AzurePublishSettingsFile** hello hello yolunu komutuyla yayımlama indirdiğiniz ayarları dosyası:
   
        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>
   
    Merhaba yayımladıktan sonra ayarları dosyası alınır, hello PowerShell oturumunda Azure aboneliğinizi yönetebilirsiniz.
    
1. Aşağıdaki Hello PowerShell komut dosyası bir metin düzenleyicisine kopyalayın ve hello değişken değerleri toosuit (Varsayılanları için bazı parametreler sağlanmış olan) ortamınızı ayarlayın. Kullanılabilirlik grubu Azure bölgeleri yayılıyorsa, hello komut dosyası bir kez hello bulut hizmeti ve bu veri merkezinde bulunan düğümler için her bir veri merkezinde çalıştırmanız gerektiğini unutmayın.
   
        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
   
        # Configure a load balanced endpoint for each node in $AGNodes, with direct server return enabled
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -Protocol "TCP" -PublicPort 1433 -LocalPort 1433 -LBSetName "ListenerEndpointLB" -ProbePort 59999 -ProbeProtocol "TCP" -DirectServerReturn $true | Update-AzureVM
        }

2. Merhaba değişkenleri ayarladıktan sonra kopyalama hello komut dosyası hello Metin Düzenleyicisi'nden, Azure PowerShell oturumu toorun onu. Merhaba istemi hala gösteriyorsa >>, toomake emin hello komut dosyasını başlatır çalıştıran yeniden girin.

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a>KB2854082 gerekirse yüklü olduğunu doğrulayın
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a>Kullanılabilirlik grubu düğümler Hello güvenlik duvarı bağlantı noktalarını açın
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a>Merhaba kullanılabilirlik grubu dinleyicisi oluşturma

Merhaba kullanılabilirlik grubu dinleyicisi iki adımda oluşturun. İlk olarak, hello istemci erişim noktası küme kaynağı oluşturun ve bağımlılıklarını yapılandırın. İkinci olarak, PowerShell ile Merhaba küme kaynaklarını yapılandırın.

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a>Merhaba istemci erişim noktası oluşturun ve hello küme bağımlılıklarını yapılandırın
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a>PowerShell'de Hello küme kaynaklarını yapılandırma
1. Dış Yük Dengeleme için hello genel sanal IP adresi çoğaltmalarınızı içeren hello bulut hizmetinde edinmeniz gerekir. Hello Azure portalında oturum açın. Kullanılabilirlik grubunuzun VM içeren toohello bulut hizmetine gidin. Açık hello **Pano** görünümü.
2. Not altında gösterilen hello adresi **ortak sanal IP (VIP) adresi**. Çözümünüzü sanal ağlara yayılıyorsa, bir çoğaltma barındıran bir VM içeren her bulut hizmeti için bu adımı yineleyin.
3. Merhaba VM'ler birinde hello aşağıdaki PowerShell komut dosyası bir metin düzenleyicisine kopyalayın ve daha önce not ettiğiniz toohello değerleri hello değişkenleri ayarlayın.
   
        # Define variables
        $ClusterNetworkName = "<ClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP Address resource name
        $CloudServiceIP = "<X.X.X.X>" # Public Virtual IP (VIP) address of your cloud service
   
        Import-Module FailoverClusters
   
        # If you are using Windows Server 2012 or higher, use hello Get-Cluster Resource command. If you are using Windows Server 2008 R2, use hello cluster res command. Both commands are commented out. Choose hello one applicable tooyour environment and remove hello # at hello beginning of hello line tooconvert hello comment tooan executable line of code.
   
        # Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$CloudServiceIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"OverrideAddressMatch"=1;"EnableDhcp"=0}
        # cluster res $IPResourceName /priv enabledhcp=0 overrideaddressmatch=1 address=$CloudServiceIP probeport=59999  subnetmask=255.255.255.255
4. Sonra hello değişkenleri ayarladığınız, yükseltilmiş bir Windows PowerShell penceresi açın sonra hello Metin Düzenleyicisi'nden hello betiği kopyalayın ve, Azure PowerShell oturumu toorun yapıştırın. Merhaba istemi hala gösteriyorsa >>, toomake emin hello komut dosyasını başlatır çalıştıran yeniden girin.
5. Her VM yineleyin. Bu komut dosyası hello bulut hizmetinin başlangıç IP adresi ile başlangıç IP adresi kaynağı yapılandırır ve diğer parametreleri hello sonda bağlantı noktası gibi ayarlar. Başlangıç IP adresi kaynağı çevrimiçi duruma getirildiğinde, bu öğreticide daha önce oluşturulan hello yük dengeli uç noktasından hello araştırma noktasında yoklama toohello yanıt verebilir.

## <a name="bring-hello-listener-online"></a>Merhaba dinleyicisi çevrimiçi duruma getirin
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a>İzleme öğeleri
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-vnet"></a>Test hello kullanılabilirlik grubu dinleyicisini (içinde hello aynı VNet)
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="test-hello-availability-group-listener-over-hello-internet"></a>Test hello kullanılabilirlik grubu dinleyicisini (üzerinden internet hello)
Sipariş tooaccess hello dinleyicisinde dış hello sanal ağdan, (Bu konuda açıklanan) dış/ortak Yük Dengeleme yalnızca hello içinde erişilebilir olan ILB yerine kullanıyor olmanız gerekir aynı sanal ağı. Merhaba bağlantı dizesinde hello bulut hizmeti adı belirtin. Örneğin, bir bulut hizmeti ile Merhaba adı olsaydı *mycloudservice*, hello sqlcmd deyimi şu şekilde olacaktır:

    sqlcmd -S "mycloudservice.cloudapp.net,<EndpointPort>" -d "<DatabaseName>" -U "<LoginId>" -P "<Password>"  -Q "select @@servername, db_name()" -l 15

Windows kimlik doğrulaması hello Hello çağıran kullanamadığından hello önceki örneğin aksine, SQL kimlik doğrulaması kullanılmalıdır. Internet. Daha fazla bilgi için bkz: [her zaman üzerindeki kullanılabilirlik grubu Azure VM içinde: istemci bağlantısı senaryoları](http://blogs.msdn.com/b/sqlcat/archive/2014/02/03/alwayson-availability-group-in-windows-azure-vm-client-connectivity-scenarios.aspx). SQL kimlik doğrulaması kullanırken, hello oluşturduğunuzdan emin olun hem çoğaltmaları aynı oturum açma. Oturumları kullanılabilirlik grupları ile ilgili sorunları giderme hakkında daha fazla bilgi için bkz: [nasıl toomap oturumlar veya kullanım SQL bulunan veritabanı kullanıcı tooconnect tooother çoğaltmaları ve tooavailability veritabanları eşleme](http://blogs.msdn.com/b/alwaysonpro/archive/2014/02/19/how-to-map-logins-or-use-contained-sql-database-user-to-connect-to-other-replicas-and-map-to-availability-databases.aspx).

İstemciler her zaman açık Hello çoğaltmaları farklı alt ağlarda olup olmadığını belirtmeniz **MultisubnetFailover = True** hello bağlantı dizesinde. Bu, paralel bağlantı denemeleri tooreplicas hello farklı alt ağlarda sonuçlanır. Bu senaryo bir çapraz bölge her zaman üzerindeki kullanılabilirlik grubu dağıtımı içerdiğine dikkat edin.

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]

