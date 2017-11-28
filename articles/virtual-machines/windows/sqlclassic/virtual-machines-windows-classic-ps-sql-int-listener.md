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
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="bd065-103">Azure'da bir ILB dinleyicisi Always On kullanılabilirlik grupları için yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bd065-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd065-104">İç dinleyicisi</span><span class="sxs-lookup"><span data-stu-id="bd065-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="bd065-105">Dış dinleyici</span><span class="sxs-lookup"><span data-stu-id="bd065-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="bd065-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="bd065-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bd065-107">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bd065-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bd065-108">Bu makalede hello Klasik dağıtım modeli hello kullanımını da kapsar.</span><span class="sxs-lookup"><span data-stu-id="bd065-108">This article covers hello use of hello classic deployment model.</span></span> <span data-ttu-id="bd065-109">En yeni dağıtımların hello Resource Manager modelini kullanmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="bd065-109">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="bd065-110">tooconfigure bir Always On kullanılabilirlik grubunda hello Resource Manager modeli için bir dinleyici bkz [Azure'da bir Always On kullanılabilirlik grubu için yük dengeleyici yapılandırma](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="bd065-110">tooconfigure a listener for an Always On availability group in hello Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="bd065-111">Kullanılabilirlik grubu yalnızca şirket içinde veya Azure yalnızca olan ya da karma yapılandırmalar için şirket içi ve Azure span çoğaltmaları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="bd065-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="bd065-112">Azure çoğaltmaları hello içinde bulunduğu aynı bölge veya birden çok sanal ağ kullanan birden çok bölgede.</span><span class="sxs-lookup"><span data-stu-id="bd065-112">Azure replicas can reside within hello same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="bd065-113">Merhaba yordamlarda bu makalede sahip olduğunuz varsayılmıştır [bir kullanılabilirlik grubu yapılandırılmış](../classic/portal-sql-alwayson-availability-groups.md) ancak henüz bir dinleyici yapılandırmadınız.</span><span class="sxs-lookup"><span data-stu-id="bd065-113">hello procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="bd065-114">Kuralları ve sınırlamaları iç dinleyicileri</span><span class="sxs-lookup"><span data-stu-id="bd065-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="bd065-115">yönergeleri izleyerek konu toohello Hello Azure'bir kullanılabilirlik grubu dinleyicisiyle bir iç yük dengeleyici (ILB) kullanılır:</span><span class="sxs-lookup"><span data-stu-id="bd065-115">hello use of an internal load balancer (ILB) with an availability group listener in Azure is subject toohello following guidelines:</span></span>

* <span data-ttu-id="bd065-116">Merhaba kullanılabilirlik grubu dinleyicisi, Windows Server 2008 R2, Windows Server 2012 ve Windows Server 2012 R2 üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="bd065-116">hello availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="bd065-117">Yalnızca bir hello dinleyici olduğundan iç kullanılabilirlik grubu dinleyicisi her bulut hizmeti için desteklenen toohello ILB yapılandırılmış ve her bir bulut hizmeti için yalnızca bir ILB yok.</span><span class="sxs-lookup"><span data-stu-id="bd065-117">Only one internal availability group listener is supported for each cloud service, because hello listener is configured toohello ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="bd065-118">Ancak, olası toocreate olan birden çok dış dinleyici.</span><span class="sxs-lookup"><span data-stu-id="bd065-118">However, it is possible toocreate multiple external listeners.</span></span> <span data-ttu-id="bd065-119">Daha fazla bilgi için bkz: [Azure'da Always On kullanılabilirlik grupları için dış dinleyici yapılandırın](../classic/ps-sql-ext-listener.md).</span><span class="sxs-lookup"><span data-stu-id="bd065-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-hello-accessibility-of-hello-listener"></a><span data-ttu-id="bd065-120">Merhaba dinleyicisi Hello erişilebilirliğini belirleme</span><span class="sxs-lookup"><span data-stu-id="bd065-120">Determine hello accessibility of hello listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="bd065-121">Bu makale, ILB kullanan bir dinleyici oluşturmaya odaklıdır.</span><span class="sxs-lookup"><span data-stu-id="bd065-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="bd065-122">Bir genel veya dış dinleyici ihtiyacınız varsa hello yukarı ayarı ele bu makalenin sürümü için bkz. bir [dış dinleyici](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bd065-122">If you need an public or external listener, see hello version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="bd065-123">Yük dengeli VM uç noktalar ile doğrudan sunucu dönüş oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd065-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="bd065-124">Bir ILB ilk hello betik daha sonra bu bölümde çalıştırarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bd065-124">You first create an ILB by running hello script later in this section.</span></span>

<span data-ttu-id="bd065-125">Yük dengeli bir uç nokta için bir Azure çoğaltması barındıran her VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bd065-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="bd065-126">Birden çok bölgede çoğaltmalar varsa, her çoğaltma bu bölgede aynı bulut hizmetinde hello olmalıdır hello aynı Azure sanal ağı.</span><span class="sxs-lookup"><span data-stu-id="bd065-126">If you have replicas in multiple regions, each replica for that region must be in hello same cloud service in hello same Azure virtual network.</span></span> <span data-ttu-id="bd065-127">Birden fazla Azure bölgesine yayılan grubu çoğaltmalarının kullanılabilirlik oluşturmak için birden çok sanal ağ yapılandırma gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd065-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="bd065-128">Sanal ağ bağlantısı yapılandırma hakkında daha fazla bilgi için bkz: [sanal ağ toovirtual ağ bağlantısını yapılandır](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="bd065-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network toovirtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="bd065-129">Hello Azure portal, tooeach çoğaltma tooview hello ayrıntıları barındıran VM gidin.</span><span class="sxs-lookup"><span data-stu-id="bd065-129">In hello Azure portal, go tooeach VM that hosts a replica tooview hello details.</span></span>

2. <span data-ttu-id="bd065-130">Merhaba tıklatın **uç noktaları** sekmesini her VM için.</span><span class="sxs-lookup"><span data-stu-id="bd065-130">Click hello **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="bd065-131">Bu hello doğrulayın **adı** ve **genel bağlantı noktası** toouse olmayan zaten kullanmak istediğiniz hello dinleyicisi uç noktası.</span><span class="sxs-lookup"><span data-stu-id="bd065-131">Verify that hello **Name** and **Public Port** of hello listener endpoint that you want toouse are not already in use.</span></span> <span data-ttu-id="bd065-132">Bu bölümdeki Hello örnekte hello adıdır *MyEndpoint*, ve başlangıç bağlantı noktası *1433*.</span><span class="sxs-lookup"><span data-stu-id="bd065-132">In hello example in this section, hello name is *MyEndpoint*, and hello port is *1433*.</span></span>

4. <span data-ttu-id="bd065-133">Yerel istemcide yükleyip hello son [PowerShell Modülü](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bd065-133">On your local client, download and install hello latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="bd065-134">Azure PowerShell'i başlatın.</span><span class="sxs-lookup"><span data-stu-id="bd065-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="bd065-135">Yeni bir PowerShell oturumu açılır ve hello Azure ile yüklenen yönetim modülleri.</span><span class="sxs-lookup"><span data-stu-id="bd065-135">A new PowerShell session opens, with hello Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="bd065-136">`Get-AzurePublishSettingsFile` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bd065-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="bd065-137">Bu cmdlet tooa tarayıcı toodownload yayımlama ayarları dosyası tooa yerel bir dizine yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="bd065-137">This cmdlet directs you tooa browser toodownload a publish settings file tooa local directory.</span></span> <span data-ttu-id="bd065-138">Azure aboneliğiniz için oturum açma kimlik bilgileriniz istenebilir.</span><span class="sxs-lookup"><span data-stu-id="bd065-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="bd065-139">Merhaba aşağıdaki komutu çalıştırarak `Import-AzurePublishSettingsFile` hello hello yolunu komutuyla yayımlama indirdiğiniz ayarları dosyası:</span><span class="sxs-lookup"><span data-stu-id="bd065-139">Run hello following `Import-AzurePublishSettingsFile` command with hello path of hello publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="bd065-140">Merhaba yayımladıktan sonra ayarları dosyası alınır, hello PowerShell oturumunda Azure aboneliğinizi yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd065-140">After hello publish settings file is imported, you can manage your Azure subscription in hello PowerShell session.</span></span>

8. <span data-ttu-id="bd065-141">İçin *ILB*, statik bir IP adresi atayın.</span><span class="sxs-lookup"><span data-stu-id="bd065-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="bd065-142">Merhaba aşağıdaki komutu çalıştırarak Hello geçerli sanal ağ yapılandırmasını inceleyin:</span><span class="sxs-lookup"><span data-stu-id="bd065-142">Examine hello current virtual network configuration by running hello following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="bd065-143">Not hello *alt* hello çoğaltmaları barındıran hello VM'ler içeren hello alt ağ için ad.</span><span class="sxs-lookup"><span data-stu-id="bd065-143">Note hello *Subnet* name for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="bd065-144">Bu ad hello betiği $SubnetName hello parametresinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bd065-144">This name is used in hello $SubnetName parameter in hello script.</span></span>

10. <span data-ttu-id="bd065-145">Not hello *VirtualNetworkSite* adlandırın ve başlangıç hello *AddressPrefix* hello çoğaltmaları barındıran hello VM'ler içeren hello alt ağ için.</span><span class="sxs-lookup"><span data-stu-id="bd065-145">Note hello *VirtualNetworkSite* name and hello starting *AddressPrefix* for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="bd065-146">Kullanılabilir bir IP adresi için hem değerleri toohello geçirerek Ara `Test-AzureStaticVNetIP` komutu ile Merhaba inceleniyor *AvailableAddresses*.</span><span class="sxs-lookup"><span data-stu-id="bd065-146">Look for an available IP address by passing both values toohello `Test-AzureStaticVNetIP` command and by examining hello *AvailableAddresses*.</span></span> <span data-ttu-id="bd065-147">Örneğin, sanal ağ hello varsa adlı *MyVNet* ve başlar bir alt ağ adres aralığı *172.16.0.128*, hello aşağıdaki komut kullanılabilir adresleri listesi:</span><span class="sxs-lookup"><span data-stu-id="bd065-147">For example, if hello virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, hello following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="bd065-148">Merhaba kullanılabilir adresler birini seçin ve hello komut hello sonraki adımda hello $ILBStaticIP parametresinde kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd065-148">Select one of hello available addresses, and use it in hello $ILBStaticIP parameter of hello script in hello next step.</span></span>

12. <span data-ttu-id="bd065-149">PowerShell komut dosyası tooa metin düzenleyicisi aşağıdaki hello kopyalayın ve hello değişken değerleri toosuit ortamınızı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bd065-149">Copy hello following PowerShell script tooa text editor, and set hello variable values toosuit your environment.</span></span> <span data-ttu-id="bd065-150">Varsayılanlar için bazı parametreler belirtildi.</span><span class="sxs-lookup"><span data-stu-id="bd065-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="bd065-151">Benzeşim grupları kullanan var olan dağıtımlar bir ILB ekleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd065-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="bd065-152">ILB gereksinimleri hakkında daha fazla bilgi için bkz: [iç yük dengeleyiciye genel bakış](../../../load-balancer/load-balancer-internal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd065-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="bd065-153">Ayrıca, kullanılabilirlik grubunuzun Azure bölgeleri yayılırsa hello betik hello bulut hizmeti ve bu veri merkezinde bulunan düğümler için her bir veri merkezinde bir kez çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd065-153">Also, if your availability group spans Azure regions, you must run hello script once in each datacenter for hello cloud service and nodes that reside in that datacenter.</span></span>

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

13. <span data-ttu-id="bd065-154">Merhaba değişkenleri ayarladıktan sonra kopyalama hello komut dosyası hello metin düzenleyicisi tooyour PowerShell oturumu toorun onu.</span><span class="sxs-lookup"><span data-stu-id="bd065-154">After you have set hello variables, copy hello script from hello text editor tooyour PowerShell session toorun it.</span></span> <span data-ttu-id="bd065-155">Merhaba istemi hala gösteriyorsa  **>>** , yeniden toomake emin hello komut dosyasını başlatır çalıştıran Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="bd065-155">If hello prompt still shows **>>**, press Enter again toomake sure hello script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="bd065-156">KB2854082 gerekirse yüklü olduğunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="bd065-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="bd065-157">Kullanılabilirlik grubu düğümler Hello güvenlik duvarı bağlantı noktalarını açın</span><span class="sxs-lookup"><span data-stu-id="bd065-157">Open hello firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a><span data-ttu-id="bd065-158">Merhaba kullanılabilirlik grubu dinleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd065-158">Create hello availability group listener</span></span>

<span data-ttu-id="bd065-159">Merhaba kullanılabilirlik grubu dinleyicisi iki adımda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bd065-159">Create hello availability group listener in two steps.</span></span> <span data-ttu-id="bd065-160">İlk olarak, hello istemci erişim noktası küme kaynağı oluşturun ve bağımlılıklarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bd065-160">First, create hello client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="bd065-161">İkinci olarak, PowerShell'de hello küme kaynaklarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="bd065-161">Second, configure hello cluster resources in PowerShell.</span></span>

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a><span data-ttu-id="bd065-162">Merhaba istemci erişim noktası oluşturun ve hello küme bağımlılıklarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="bd065-162">Create hello client access point and configure hello cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a><span data-ttu-id="bd065-163">PowerShell'de Hello küme kaynaklarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="bd065-163">Configure hello cluster resources in PowerShell</span></span>
1. <span data-ttu-id="bd065-164">ILB için hello daha önce oluşturulan ILB hello IP adresini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bd065-164">For ILB, you must use hello IP address of hello ILB that was created earlier.</span></span> <span data-ttu-id="bd065-165">Bu IP adresi PowerShell, komut dosyası izleyen kullanım hello tooobtain:</span><span class="sxs-lookup"><span data-stu-id="bd065-165">tooobtain this IP address in PowerShell, use hello following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="bd065-166">Hello VM'ler birinde hello PowerShell Betiği için işletim sistemi tooa metin düzenleyicisi kopyalayın ve ardından daha önce not ettiğiniz toohello değerleri hello değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="bd065-166">On one of hello VMs, copy hello PowerShell script for your operating system tooa text editor, and then set hello variables toohello values you noted earlier.</span></span>

    <span data-ttu-id="bd065-167">Windows Server 2012 veya sonraki sürümlerde, komut dosyası izleyen hello kullan:</span><span class="sxs-lookup"><span data-stu-id="bd065-167">For Windows Server 2012 or later, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="bd065-168">Windows Server 2008 R2 için komut dosyası izleyen hello kullan:</span><span class="sxs-lookup"><span data-stu-id="bd065-168">For Windows Server 2008 R2, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="bd065-169">Set hello değişkenleri yükseltilmiş bir Windows PowerShell penceresi açın, sonra Yapıştır hello komut dosyası hello Metin Düzenleyicisi'nden, PowerShell oturumu toorun onu.</span><span class="sxs-lookup"><span data-stu-id="bd065-169">After you have set hello variables, open an elevated Windows PowerShell window, paste hello script from hello text editor into your PowerShell session toorun it.</span></span> <span data-ttu-id="bd065-170">Merhaba istemi hala gösteriyorsa  **>>** , Enter tuşuna basarak yeniden hello betik çalıştıran başladığından emin toomake.</span><span class="sxs-lookup"><span data-stu-id="bd065-170">If hello prompt still shows **>>**, Press Enter again toomake sure that hello script starts running.</span></span>

4. <span data-ttu-id="bd065-171">Her VM için adımları önceki hello yineleyin.</span><span class="sxs-lookup"><span data-stu-id="bd065-171">Repeat hello preceding steps for each VM.</span></span>  
    <span data-ttu-id="bd065-172">Bu komut dosyası hello bulut hizmetinin başlangıç IP adresi ile başlangıç IP adresi kaynağı yapılandırır ve diğer parametreleri hello sonda bağlantı noktası gibi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="bd065-172">This script configures hello IP address resource with hello IP address of hello cloud service and sets other parameters, such as hello probe port.</span></span> <span data-ttu-id="bd065-173">Başlangıç IP adresi kaynağı çevrimiçi duruma getirildiğinde, daha önce oluşturduğunuz hello yük dengeli uç noktasından hello araştırma noktasında yoklama toohello yanıt verebilir.</span><span class="sxs-lookup"><span data-stu-id="bd065-173">When hello IP address resource is brought online, it can respond toohello polling on hello probe port from hello load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-hello-listener-online"></a><span data-ttu-id="bd065-174">Merhaba dinleyicisi çevrimiçi duruma getirin</span><span class="sxs-lookup"><span data-stu-id="bd065-174">Bring hello listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="bd065-175">İzleme öğeleri</span><span class="sxs-lookup"><span data-stu-id="bd065-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a><span data-ttu-id="bd065-176">Test hello kullanılabilirlik grubu dinleyicisini (içinde hello aynı sanal ağ)</span><span class="sxs-lookup"><span data-stu-id="bd065-176">Test hello availability group listener (within hello same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="bd065-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd065-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
