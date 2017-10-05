---
title: "Azure'da bir ILB dinleyicisi Always On kullanılabilirlik grupları için yapılandırma | Microsoft Docs"
description: "Bu öğretici Klasik dağıtım modeliyle oluşturulan kaynakları kullanır ve bir iç yük dengeleyici kullanan Azure'da bir Always On kullanılabilirlik grubu dinleyicisi oluşturur."
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
ms.openlocfilehash: fea70b389b1f1d6af963e3f14fdc48e8d857dd53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="9492c-103">Azure'da bir ILB dinleyicisi Always On kullanılabilirlik grupları için yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9492c-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9492c-104">İç dinleyicisi</span><span class="sxs-lookup"><span data-stu-id="9492c-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="9492c-105">Dış dinleyici</span><span class="sxs-lookup"><span data-stu-id="9492c-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="9492c-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9492c-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9492c-107">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9492c-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="9492c-108">Bu makalede Klasik dağıtım modeli kullanımını da kapsar.</span><span class="sxs-lookup"><span data-stu-id="9492c-108">This article covers the use of the classic deployment model.</span></span> <span data-ttu-id="9492c-109">En yeni dağıtımların Resource Manager modelini kullanmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="9492c-109">We recommend that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="9492c-110">Resource Manager modelinde bir Always On kullanılabilirlik grubu için bir dinleyici yapılandırmak için bkz: [Azure'da bir Always On kullanılabilirlik grubu için yük dengeleyici yapılandırma](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="9492c-110">To configure a listener for an Always On availability group in the Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="9492c-111">Kullanılabilirlik grubu yalnızca şirket içinde veya Azure yalnızca olan ya da karma yapılandırmalar için şirket içi ve Azure span çoğaltmaları içerebilir.</span><span class="sxs-lookup"><span data-stu-id="9492c-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="9492c-112">Azure çoğaltmaları aynı bölge içinde veya birden çok sanal ağ kullanan birden çok bölgeye bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="9492c-112">Azure replicas can reside within the same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="9492c-113">Bu makaledeki yordamlar zaten olduğunu varsayın [bir kullanılabilirlik grubu yapılandırılmış](../classic/portal-sql-alwayson-availability-groups.md) ancak henüz bir dinleyici oluşturmamış.</span><span class="sxs-lookup"><span data-stu-id="9492c-113">The procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="9492c-114">Kuralları ve sınırlamaları iç dinleyicileri</span><span class="sxs-lookup"><span data-stu-id="9492c-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="9492c-115">Azure'da bir kullanılabilirlik grubu dinleyicisiyle bir iç yük dengeleyici (ILB) aşağıdaki yönergeleri tabi kullanılır:</span><span class="sxs-lookup"><span data-stu-id="9492c-115">The use of an internal load balancer (ILB) with an availability group listener in Azure is subject to the following guidelines:</span></span>

* <span data-ttu-id="9492c-116">Kullanılabilirlik grubu dinleyicisi, Windows Server 2008 R2, Windows Server 2012 ve Windows Server 2012 R2 üzerinde desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9492c-116">The availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="9492c-117">Yalnızca bir iç kullanılabilirlik grubu dinleyicisi her bulut hizmeti için dinleyici ILB için yapılandırılır ve her bir bulut hizmeti için yalnızca bir ILB için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9492c-117">Only one internal availability group listener is supported for each cloud service, because the listener is configured to the ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="9492c-118">Ancak, birden çok dış dinleyici oluşturmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="9492c-118">However, it is possible to create multiple external listeners.</span></span> <span data-ttu-id="9492c-119">Daha fazla bilgi için bkz: [Azure'da Always On kullanılabilirlik grupları için dış dinleyici yapılandırın](../classic/ps-sql-ext-listener.md).</span><span class="sxs-lookup"><span data-stu-id="9492c-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-the-accessibility-of-the-listener"></a><span data-ttu-id="9492c-120">Dinleyici erişilebilirliğini belirleme</span><span class="sxs-lookup"><span data-stu-id="9492c-120">Determine the accessibility of the listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="9492c-121">Bu makale, ILB kullanan bir dinleyici oluşturmaya odaklıdır.</span><span class="sxs-lookup"><span data-stu-id="9492c-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="9492c-122">Bir genel veya dış dinleyici ihtiyacınız varsa, yedekleme ayarı ele bu makalenin sürümü bkz bir [dış dinleyici](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9492c-122">If you need an public or external listener, see the version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="9492c-123">Yük dengeli VM uç noktalar ile doğrudan sunucu dönüş oluşturma</span><span class="sxs-lookup"><span data-stu-id="9492c-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="9492c-124">Bir ILB ilk komut daha sonra bu bölümde çalıştırarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9492c-124">You first create an ILB by running the script later in this section.</span></span>

<span data-ttu-id="9492c-125">Yük dengeli bir uç nokta için bir Azure çoğaltması barındıran her VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9492c-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="9492c-126">Birden çok bölgede çoğaltmalar varsa, o bölge için her çoğaltma aynı Azure sanal ağı aynı bulut hizmeti olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9492c-126">If you have replicas in multiple regions, each replica for that region must be in the same cloud service in the same Azure virtual network.</span></span> <span data-ttu-id="9492c-127">Birden fazla Azure bölgesine yayılan grubu çoğaltmalarının kullanılabilirlik oluşturmak için birden çok sanal ağ yapılandırma gerekir.</span><span class="sxs-lookup"><span data-stu-id="9492c-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="9492c-128">Sanal ağ bağlantısı yapılandırma hakkında daha fazla bilgi için bkz: [sanal ağ bağlantısı sanal ağa yapılandırma](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="9492c-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network to virtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="9492c-129">Azure portalında ayrıntılarını görüntülemek için bir çoğaltma barındıran her VM gidin.</span><span class="sxs-lookup"><span data-stu-id="9492c-129">In the Azure portal, go to each VM that hosts a replica to view the details.</span></span>

2. <span data-ttu-id="9492c-130">Tıklatın **uç noktaları** sekmesini her VM için.</span><span class="sxs-lookup"><span data-stu-id="9492c-130">Click the **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="9492c-131">Doğrulayın **adı** ve **genel bağlantı noktası** dinleyicisi olarak kullanmak istediğiniz uç noktası olmayan zaten kullanımda.</span><span class="sxs-lookup"><span data-stu-id="9492c-131">Verify that the **Name** and **Public Port** of the listener endpoint that you want to use are not already in use.</span></span> <span data-ttu-id="9492c-132">Bu bölümdeki örnekte addır *MyEndpoint*, ve bağlantı noktası *1433*.</span><span class="sxs-lookup"><span data-stu-id="9492c-132">In the example in this section, the name is *MyEndpoint*, and the port is *1433*.</span></span>

4. <span data-ttu-id="9492c-133">Yerel istemcinize karşıdan yükle ve en son yükleme [PowerShell Modülü](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9492c-133">On your local client, download and install the latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="9492c-134">Azure PowerShell'i başlatın.</span><span class="sxs-lookup"><span data-stu-id="9492c-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="9492c-135">Yeni bir PowerShell oturumunda, yüklenen Azure yönetim modülleri açar.</span><span class="sxs-lookup"><span data-stu-id="9492c-135">A new PowerShell session opens, with the Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="9492c-136">`Get-AzurePublishSettingsFile` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9492c-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="9492c-137">Bu cmdlet, yerel bir dizine yayımlama ayarları dosyasını indirmek için bir tarayıcı yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="9492c-137">This cmdlet directs you to a browser to download a publish settings file to a local directory.</span></span> <span data-ttu-id="9492c-138">Azure aboneliğiniz için oturum açma kimlik bilgileriniz istenebilir.</span><span class="sxs-lookup"><span data-stu-id="9492c-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="9492c-139">Aşağıdaki komutu çalıştırarak `Import-AzurePublishSettingsFile` komutunu indirdiğiniz yayımlama ayarları dosyası yolu:</span><span class="sxs-lookup"><span data-stu-id="9492c-139">Run the following `Import-AzurePublishSettingsFile` command with the path of the publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="9492c-140">Yayımlama ayarları dosyasını içeri aktarıldıktan sonra PowerShell oturumunda Azure aboneliğinizi yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9492c-140">After the publish settings file is imported, you can manage your Azure subscription in the PowerShell session.</span></span>

8. <span data-ttu-id="9492c-141">İçin *ILB*, statik bir IP adresi atayın.</span><span class="sxs-lookup"><span data-stu-id="9492c-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="9492c-142">Aşağıdaki komutu çalıştırarak geçerli sanal ağ yapılandırmasını inceleyin:</span><span class="sxs-lookup"><span data-stu-id="9492c-142">Examine the current virtual network configuration by running the following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="9492c-143">Not *alt* çoğaltmaları barındıran sanal makineleri içeren alt ağ için ad.</span><span class="sxs-lookup"><span data-stu-id="9492c-143">Note the *Subnet* name for the subnet that contains the VMs that host the replicas.</span></span> <span data-ttu-id="9492c-144">Bu ad, betiği $SubnetName parametresinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9492c-144">This name is used in the $SubnetName parameter in the script.</span></span>

10. <span data-ttu-id="9492c-145">Not *VirtualNetworkSite* adı ve başlangıç *AddressPrefix* çoğaltmaları barındıran sanal makineleri içeren alt ağ için.</span><span class="sxs-lookup"><span data-stu-id="9492c-145">Note the *VirtualNetworkSite* name and the starting *AddressPrefix* for the subnet that contains the VMs that host the replicas.</span></span> <span data-ttu-id="9492c-146">Her iki değerin geçirerek kullanılabilir bir IP adresi arayın `Test-AzureStaticVNetIP` komut ve göre inceleyerek *AvailableAddresses*.</span><span class="sxs-lookup"><span data-stu-id="9492c-146">Look for an available IP address by passing both values to the `Test-AzureStaticVNetIP` command and by examining the *AvailableAddresses*.</span></span> <span data-ttu-id="9492c-147">Örneğin, sanal ağ adlı *MyVNet* ve başlar bir alt ağ adres aralığı *172.16.0.128*, aşağıdaki komut kullanılabilir adresleri listesi:</span><span class="sxs-lookup"><span data-stu-id="9492c-147">For example, if the virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, the following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="9492c-148">Kullanılabilir adresler birini seçin ve komut dosyasının bir sonraki adımda $ILBStaticIP parametresinde kullanın.</span><span class="sxs-lookup"><span data-stu-id="9492c-148">Select one of the available addresses, and use it in the $ILBStaticIP parameter of the script in the next step.</span></span>

12. <span data-ttu-id="9492c-149">Aşağıdaki PowerShell komut dosyasını bir metin düzenleyicisine kopyalayın ve ortamınıza uygun değişken değerlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9492c-149">Copy the following PowerShell script to a text editor, and set the variable values to suit your environment.</span></span> <span data-ttu-id="9492c-150">Varsayılanlar için bazı parametreler belirtildi.</span><span class="sxs-lookup"><span data-stu-id="9492c-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="9492c-151">Benzeşim grupları kullanan var olan dağıtımlar bir ILB ekleyemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="9492c-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="9492c-152">ILB gereksinimleri hakkında daha fazla bilgi için bkz: [iç yük dengeleyiciye genel bakış](../../../load-balancer/load-balancer-internal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9492c-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="9492c-153">Ayrıca, kullanılabilirlik grubunuzun Azure bölgeleri yayılırsa, komut dosyası her veri merkezinde, veri merkezinde bulunan düğümler ve bulut hizmeti için bir kez çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9492c-153">Also, if your availability group spans Azure regions, you must run the script once in each datacenter for the cloud service and nodes that reside in that datacenter.</span></span>

        # Define variables
        $ServiceName = "<MyCloudService>" # the name of the cloud service that contains the availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in the same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that the replicas use in the virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for the ILB in the subnet
        $ILBName = "AGListenerLB" # customize the ILB name or use this default value

        # Create the ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. <span data-ttu-id="9492c-154">Değişkenleri ayarladıktan sonra komut dosyasını çalıştırmak için PowerShell oturumunuzun Metin Düzenleyicisi'nden kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="9492c-154">After you have set the variables, copy the script from the text editor to your PowerShell session to run it.</span></span> <span data-ttu-id="9492c-155">İstemi hala gösteriyorsa  **>>** , yeniden komut dosyasını başlatır çalıştıran emin olmak için Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="9492c-155">If the prompt still shows **>>**, press Enter again to make sure the script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="9492c-156">KB2854082 gerekirse yüklü olduğunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="9492c-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-the-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="9492c-157">Kullanılabilirlik grubu düğümler güvenlik duvarı bağlantı noktalarını açın</span><span class="sxs-lookup"><span data-stu-id="9492c-157">Open the firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-the-availability-group-listener"></a><span data-ttu-id="9492c-158">Kullanılabilirlik grubu dinleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9492c-158">Create the availability group listener</span></span>

<span data-ttu-id="9492c-159">Kullanılabilirlik grubu dinleyicisi iki adımda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9492c-159">Create the availability group listener in two steps.</span></span> <span data-ttu-id="9492c-160">İlk olarak, istemci erişim noktası küme kaynağı oluşturun ve bağımlılıklarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9492c-160">First, create the client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="9492c-161">İkinci olarak, küme kaynaklarını PowerShell'de yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="9492c-161">Second, configure the cluster resources in PowerShell.</span></span>

### <a name="create-the-client-access-point-and-configure-the-cluster-dependencies"></a><span data-ttu-id="9492c-162">İstemci erişim noktası oluşturun ve küme bağımlılıklarını yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9492c-162">Create the client access point and configure the cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-the-cluster-resources-in-powershell"></a><span data-ttu-id="9492c-163">PowerShell'de küme kaynaklarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9492c-163">Configure the cluster resources in PowerShell</span></span>
1. <span data-ttu-id="9492c-164">ILB için daha önce oluşturulan ILB'nin IP adresini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9492c-164">For ILB, you must use the IP address of the ILB that was created earlier.</span></span> <span data-ttu-id="9492c-165">PowerShell'de bu IP adresi almak için aşağıdaki komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="9492c-165">To obtain this IP address in PowerShell, use the following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # the name of the cloud service that contains the AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="9492c-166">Sanal makineleri birinde işletim sisteminiz için PowerShell komut dosyası bir metin düzenleyicisine kopyalayın ve ardından daha önce not ettiğiniz değerleri değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9492c-166">On one of the VMs, copy the PowerShell script for your operating system to a text editor, and then set the variables to the values you noted earlier.</span></span>

    <span data-ttu-id="9492c-167">Windows Server 2012 veya sonraki sürümlerde, aşağıdaki komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="9492c-167">For Windows Server 2012 or later, use the following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
        $IPResourceName = "<IPResourceName>" # the IP address resource name
        $ILBIP = “<X.X.X.X>” # the IP address of the ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="9492c-168">Windows Server 2008 R2 için aşağıdaki komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="9492c-168">For Windows Server 2008 R2, use the following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # the cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher to find the name)
        $IPResourceName = "<IPResourceName>" # the IP address resource name
        $ILBIP = “<X.X.X.X>” # the IP address of the ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="9492c-169">Değişkenleri ayarladıktan sonra yükseltilmiş bir Windows PowerShell penceresi açın, metin düzenleyici komut dosyasını çalıştırmak için PowerShell oturumunuza yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="9492c-169">After you have set the variables, open an elevated Windows PowerShell window, paste the script from the text editor into your PowerShell session to run it.</span></span> <span data-ttu-id="9492c-170">İstemi hala gösteriyorsa  **>>** , yeniden komut dosyası çalışmaya başladıktan emin olmak için ENTER'a basın.</span><span class="sxs-lookup"><span data-stu-id="9492c-170">If the prompt still shows **>>**, Press Enter again to make sure that the script starts running.</span></span>

4. <span data-ttu-id="9492c-171">Her VM için önceki adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="9492c-171">Repeat the preceding steps for each VM.</span></span>  
    <span data-ttu-id="9492c-172">Bu komut dosyası Bulut hizmeti IP adresi ile IP adresi kaynağı yapılandırır ve diğer parametreleri gibi araştırma bağlantı noktasını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="9492c-172">This script configures the IP address resource with the IP address of the cloud service and sets other parameters, such as the probe port.</span></span> <span data-ttu-id="9492c-173">IP adresi kaynağı çevrimiçi duruma getirildiğinde, araştırma bağlantı noktası üzerinde sorgulama yük dengeli uç noktasından daha önce oluşturduğunuz yanıt verebilir.</span><span class="sxs-lookup"><span data-stu-id="9492c-173">When the IP address resource is brought online, it can respond to the polling on the probe port from the load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-the-listener-online"></a><span data-ttu-id="9492c-174">Dinleyici çevrimiçi duruma getirin</span><span class="sxs-lookup"><span data-stu-id="9492c-174">Bring the listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="9492c-175">İzleme öğeleri</span><span class="sxs-lookup"><span data-stu-id="9492c-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-the-availability-group-listener-within-the-same-virtual-network"></a><span data-ttu-id="9492c-176">Kullanılabilirlik grubu dinleyicisini (aynı sanal ağda) test edin</span><span class="sxs-lookup"><span data-stu-id="9492c-176">Test the availability group listener (within the same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="9492c-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9492c-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
