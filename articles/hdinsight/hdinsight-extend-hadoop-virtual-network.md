---
title: "aaaExtend Hdınsight sanal ağ - Azure ile | Microsoft Docs"
description: "Toouse Azure Virtual Network tooconnect Hdınsight tooother nasıl bulut kaynakları veya kaynakları, veri merkezinizdeki öğrenin"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="67de4-103">Bir Azure sanal ağı kullanarak Azure Hdınsight genişletme</span><span class="sxs-lookup"><span data-stu-id="67de4-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="67de4-104">Bilgi nasıl toouse Hdınsight ile bir [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67de4-104">Learn how toouse HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="67de4-105">Bir Azure sanal ağı kullanarak aşağıdaki senaryolar hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="67de4-105">Using an Azure Virtual Network enables hello following scenarios:</span></span>

* <span data-ttu-id="67de4-106">TooHDInsight doğrudan bir şirket içi ağ üzerinden bağlanılıyor.</span><span class="sxs-lookup"><span data-stu-id="67de4-106">Connecting tooHDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="67de4-107">Hdınsight toodata bağlanan bir Azure sanal ağında depolar.</span><span class="sxs-lookup"><span data-stu-id="67de4-107">Connecting HDInsight toodata stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="67de4-108">Doğrudan internet üzerinde herkese açık şekilde kullanılamayan Hadoop hizmetlerine erişimi hello.</span><span class="sxs-lookup"><span data-stu-id="67de4-108">Directly accessing Hadoop services that are not available publicly over hello internet.</span></span> <span data-ttu-id="67de4-109">Örneğin, Kafka API'leri veya hello HBase Java API.</span><span class="sxs-lookup"><span data-stu-id="67de4-109">For example, Kafka APIs or hello HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="67de4-110">Merhaba bu belgedeki bilgiler, TCP/IP ağ bilinmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="67de4-110">hello information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="67de4-111">TCP/IP ağ ile bilmiyorsanız tooproduction ağlar değişiklikler yapmadan önce olan bir kullanıcıyla ortak.</span><span class="sxs-lookup"><span data-stu-id="67de4-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications tooproduction networks.</span></span>

## <a name="planning"></a><span data-ttu-id="67de4-112">Planlama</span><span class="sxs-lookup"><span data-stu-id="67de4-112">Planning</span></span>

<span data-ttu-id="67de4-113">Merhaba, bir sanal ağdaki tooinstall Hdınsight planlarken yanıt hello sorular şunlardır:</span><span class="sxs-lookup"><span data-stu-id="67de4-113">hello following are hello questions that you must answer when planning tooinstall HDInsight in a virtual network:</span></span>

* <span data-ttu-id="67de4-114">Mevcut sanal ağda tooinstall Hdınsight gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="67de4-114">Do you need tooinstall HDInsight into an existing virtual network?</span></span> <span data-ttu-id="67de4-115">Veya yeni bir ağ oluşturmak?</span><span class="sxs-lookup"><span data-stu-id="67de4-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="67de4-116">Varolan bir sanal ağı kullanıyorsanız, Hdınsight yükleyebilmek için önce toomodify hello ağ yapılandırması gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="67de4-116">If you are using an existing virtual network, you may need toomodify hello network configuration before you can install HDInsight.</span></span> <span data-ttu-id="67de4-117">Daha fazla bilgi için bkz: Merhaba [Hdınsight tooan var olan sanal ağ ekleme](#existingvnet) bölümü.</span><span class="sxs-lookup"><span data-stu-id="67de4-117">For more information, see hello [add HDInsight tooan existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="67de4-118">Hdınsight tooanother sanal ağ içeren tooconnect hello sanal ağ veya şirket içi ağınıza istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="67de4-118">Do you want tooconnect hello virtual network containing HDInsight tooanother virtual network or your on-premises network?</span></span>

    <span data-ttu-id="67de4-119">tooeasily iş ağlar kaynaklarla toocreate özel DNS ve gerekir DNS iletmeyi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="67de4-119">tooeasily work with resources across networks, you may need toocreate a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="67de4-120">Merhaba daha fazla bilgi için bkz: [birden çok ağları bağlama](#multinet) bölümü.</span><span class="sxs-lookup"><span data-stu-id="67de4-120">For more information, see hello [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="67de4-121">Toorestrict/yeniden yönlendirme istiyorsunuz gelen veya giden trafiği tooHDInsight?</span><span class="sxs-lookup"><span data-stu-id="67de4-121">Do you want toorestrict/redirect inbound or outbound traffic tooHDInsight?</span></span>

    <span data-ttu-id="67de4-122">Hdınsight hello Azure veri merkezinde belirli IP adresleri ile iletişim sınırsız gerekir.</span><span class="sxs-lookup"><span data-stu-id="67de4-122">HDInsight must have unrestricted communication with specific IP addresses in hello Azure data center.</span></span> <span data-ttu-id="67de4-123">Güvenlik duvarları üzerinden istemci iletişimi için izin verilmelidir çeşitli bağlantı noktaları da vardır.</span><span class="sxs-lookup"><span data-stu-id="67de4-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="67de4-124">Daha fazla bilgi için bkz: Merhaba [ağ trafiğini denetleme](#networktraffic) bölümü.</span><span class="sxs-lookup"><span data-stu-id="67de4-124">For more information, see hello [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="67de4-125"><a id="existingvnet"></a>Hdınsight tooan var olan sanal ağ ekleme</span><span class="sxs-lookup"><span data-stu-id="67de4-125"><a id="existingvnet"></a>Add HDInsight tooan existing virtual network</span></span>

<span data-ttu-id="67de4-126">Merhaba adımları Bu bölümde toodiscover kullanma tooadd Azure sanal ağı var olan yeni bir Hdınsight tooan.</span><span class="sxs-lookup"><span data-stu-id="67de4-126">Use hello steps in this section toodiscover how tooadd a new HDInsight tooan existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="67de4-127">Bir sanal ağ var olan bir Hdınsight kümesine eklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="67de4-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="67de4-128">Merhaba sanal ağ için bir Klasik veya Resource Manager dağıtım modeli kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="67de4-128">Are you using a classic or Resource Manager deployment model for hello virtual network?</span></span>

    <span data-ttu-id="67de4-129">Hdınsight 3.4 ve büyük bir Resource Manager sanal ağ gerektirir.</span><span class="sxs-lookup"><span data-stu-id="67de4-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="67de4-130">Hdınsight'ın önceki sürümlerini Klasik sanal ağ gereklidir.</span><span class="sxs-lookup"><span data-stu-id="67de4-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="67de4-131">Ardından, varolan ağınızda bir Klasik sanal ağı ise, Resource Manager sanal ağ oluşturma ve hello iki bağlantı gerekir.</span><span class="sxs-lookup"><span data-stu-id="67de4-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect hello two.</span></span> <span data-ttu-id="67de4-132">[Klasik sanal ağlar toonew sanal ağlara bağlanma](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="67de4-132">[Connecting classic VNets toonew VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="67de4-133">Birleştirilmiş sonra hello Resource Manager ağında yüklü Hdınsight hello Klasik ağ kaynakları ile etkileşim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="67de4-133">Once joined, HDInsight installed in hello Resource Manager network can interact with resources in hello classic network.</span></span>

2. <span data-ttu-id="67de4-134">Zorlamalı tünel kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="67de4-134">Do you use forced tunneling?</span></span> <span data-ttu-id="67de4-135">Zorlamalı tünel, giden Internet trafiği tooa aygıt İnceleme için zorlayan bir alt ağ ayarı ve günlüğe kaydetme olur.</span><span class="sxs-lookup"><span data-stu-id="67de4-135">Forced tunneling is a subnet setting that forces outbound Internet traffic tooa device for inspection and logging.</span></span> <span data-ttu-id="67de4-136">Hdınsight zorlamalı tünel desteklemez.</span><span class="sxs-lookup"><span data-stu-id="67de4-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="67de4-137">Bir alt ağ Hdınsight yüklemeden önce zorlamalı tünel kaldırmak veya Hdınsight için yeni bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="67de4-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="67de4-138">Ağ güvenlik grupları, kullanıcı tanımlı yollar veya sanal ağ uygulamaları toorestrict trafiği içine veya dışına hello sanal ağ kullanıyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="67de4-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances toorestrict traffic into or out of hello virtual network?</span></span>

    <span data-ttu-id="67de4-139">Yönetilen bir hizmet olarak Hdınsight Kısıtlanmamış erişim tooseveral IP adreslerini hello Azure veri merkezinde gerektirir.</span><span class="sxs-lookup"><span data-stu-id="67de4-139">As a managed service, HDInsight requires unrestricted access tooseveral IP addresses in hello Azure data center.</span></span> <span data-ttu-id="67de4-140">Bu IP adresleri ile tooallow iletişim herhangi bir mevcut ağ güvenlik grupları veya kullanıcı tanımlı yollar güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="67de4-140">tooallow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="67de4-141">Hdınsight çeşitli bağlantı noktaları kullanan birden çok hizmetleri barındırır.</span><span class="sxs-lookup"><span data-stu-id="67de4-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="67de4-142">Trafik toothese bağlantı noktalarını engellemez.</span><span class="sxs-lookup"><span data-stu-id="67de4-142">Do not block traffic toothese ports.</span></span> <span data-ttu-id="67de4-143">Bağlantı noktaları tooallow sanal gereç güvenlik duvarları üzerinden bir listesi için bkz: hello [güvenlik](#security) bölümü.</span><span class="sxs-lookup"><span data-stu-id="67de4-143">For a list of ports tooallow through virtual appliance firewalls, see hello [Security](#security) section.</span></span>

    <span data-ttu-id="67de4-144">toofind var olan güvenlik yapılandırmanızı Azure PowerShell veya Azure CLI komutları aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="67de4-144">toofind your existing security configuration, use hello following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="67de4-145">Ağ güvenlik grupları</span><span class="sxs-lookup"><span data-stu-id="67de4-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="67de4-146">Daha fazla bilgi için bkz: Merhaba [ağ güvenlik grupları sorun giderme](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) belge.</span><span class="sxs-lookup"><span data-stu-id="67de4-146">For more information, see hello [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="67de4-147">Ağ güvenlik grubu kural kuralı önceliği temelinde sırayla uygulanır.</span><span class="sxs-lookup"><span data-stu-id="67de4-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="67de4-148">Merhaba trafik desenle eşleşen hello ilk kural uygulanır ve hiçbir diğerlerinin bu trafiği için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="67de4-148">hello first rule that matches hello traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="67de4-149">Sipariş en fazla izne sahip tooleast izin veren kuralları.</span><span class="sxs-lookup"><span data-stu-id="67de4-149">Order rules from most permissive tooleast permissive.</span></span> <span data-ttu-id="67de4-150">Daha fazla bilgi için bkz: Merhaba [filtre ağ güvenlik grupları ile ağ trafiği](../virtual-network/virtual-networks-nsg.md) belge.</span><span class="sxs-lookup"><span data-stu-id="67de4-150">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="67de4-151">Kullanıcı tanımlı yollar</span><span class="sxs-lookup"><span data-stu-id="67de4-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="67de4-152">Merhaba daha fazla bilgi için bkz: [sorun giderme yolları](../virtual-network/virtual-network-routes-troubleshoot-portal.md) belge.</span><span class="sxs-lookup"><span data-stu-id="67de4-152">For more information, see hello [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="67de4-153">Hdınsight kümesi oluşturma ve yapılandırma sırasında hello Azure sanal ağı seçin.</span><span class="sxs-lookup"><span data-stu-id="67de4-153">Create an HDInsight cluster and select hello Azure Virtual Network during configuration.</span></span> <span data-ttu-id="67de4-154">Belgeleri toounderstand hello küme oluşturma işlemi aşağıdaki hello Hello adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="67de4-154">Use hello steps in hello following documents toounderstand hello cluster creation process:</span></span>

    * [<span data-ttu-id="67de4-155">Hello Azure portal kullanarak Hdınsight oluşturma</span><span class="sxs-lookup"><span data-stu-id="67de4-155">Create HDInsight using hello Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="67de4-156">Azure PowerShell kullanarak HDInsight oluşturma</span><span class="sxs-lookup"><span data-stu-id="67de4-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="67de4-157">Azure CLI 1.0 kullanarak Hdınsight oluşturma</span><span class="sxs-lookup"><span data-stu-id="67de4-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="67de4-158">Bir Azure Resource Manager şablonu kullanarak Hdınsight oluşturma</span><span class="sxs-lookup"><span data-stu-id="67de4-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="67de4-159">Hdınsight ekleme bir isteğe bağlı yapılandırma adımı tooa sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="67de4-159">Adding HDInsight tooa virtual network is an optional configuration step.</span></span> <span data-ttu-id="67de4-160">Merhaba küme yapılandırma emin tooselect hello sanal ağ olabilir.</span><span class="sxs-lookup"><span data-stu-id="67de4-160">Be sure tooselect hello virtual network when configuring hello cluster.</span></span>

## <span data-ttu-id="67de4-161"><a id="multinet"></a>Birden çok ağları bağlama</span><span class="sxs-lookup"><span data-stu-id="67de4-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="67de4-162">Hello büyük sınama birden fazla ağ yapılandırması ile Merhaba ağlar arasında ad çözümleme ' dir.</span><span class="sxs-lookup"><span data-stu-id="67de4-162">hello biggest challenge with a multi-network configuration is name resolution between hello networks.</span></span>

<span data-ttu-id="67de4-163">Azure ad çözümlemesi için sanal bir ağa yüklü olan Azure hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="67de4-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="67de4-164">Bu yerleşik ad çözümlemesi bir tam etki alanı adı (FQDN) kullanarak kaynaklarına aşağıdaki Hdınsight tooconnect toohello sağlar:</span><span class="sxs-lookup"><span data-stu-id="67de4-164">This built-in name resolution allows HDInsight tooconnect toohello following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="67de4-165">Kullanılabilir herhangi bir kaynağa Internet hello.</span><span class="sxs-lookup"><span data-stu-id="67de4-165">Any resource that is available on hello internet.</span></span> <span data-ttu-id="67de4-166">Örneğin, microsoft.com, google.com.</span><span class="sxs-lookup"><span data-stu-id="67de4-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="67de4-167">İçinde aynı Azure sanal ağ, hello kullanarak hello olan herhangi bir kaynağa __iç DNS ad__ hello kaynağının.</span><span class="sxs-lookup"><span data-stu-id="67de4-167">Any resource that is in hello same Azure Virtual Network, by using hello __internal DNS name__ of hello resource.</span></span> <span data-ttu-id="67de4-168">Örneğin, hello varsayılan ad çözümlemesi kullanırken hello örnek iç DNS adları atanan tooHDInsight çalışan düğümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="67de4-168">For example, when using hello default name resolution, hello following are example internal DNS names assigned tooHDInsight worker nodes:</span></span>

    * <span data-ttu-id="67de4-169">wn0 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="67de4-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="67de4-170">wn2 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="67de4-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="67de4-171">Bu her iki düğüm iç DNS adları kullanarak birbirine ve diğer düğümlere, hdınsight'ta ile doğrudan iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="67de4-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="67de4-172">Merhaba varsayılan ad çözümlemesini yapar __değil__ Hdınsight tooresolve kaynakların hello adları birleştirilmiş toohello sanal ağı olan ağlarda izin verin.</span><span class="sxs-lookup"><span data-stu-id="67de4-172">hello default name resolution does __not__ allow HDInsight tooresolve hello names of resources in networks that are joined toohello virtual network.</span></span> <span data-ttu-id="67de4-173">Örneğin, ortak toojoin şirket içi toohello sanal ağ ağ.</span><span class="sxs-lookup"><span data-stu-id="67de4-173">For example, it is common toojoin your on-premises network toohello virtual network.</span></span> <span data-ttu-id="67de4-174">Yalnızca hello varsayılan ad çözümlemesi ile Hdınsight adıyla hello şirket içi ağınızdaki kaynaklara erişemez.</span><span class="sxs-lookup"><span data-stu-id="67de4-174">With only hello default name resolution, HDInsight cannot access resources in hello on-premises network by name.</span></span> <span data-ttu-id="67de4-175">Şirket içi ağınızdaki kaynaklara adıyla hello sanal ağ kaynaklarına erişemez, Hello ters de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="67de4-175">hello opposite is also true, resources in your on-premises network cannot access resources in hello virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="67de4-176">Merhaba özel DNS sunucusu oluşturmak ve hello sanal ağ toouse yapılandırmanız gerekir, oluşturmadan önce hello Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="67de4-176">You must create hello custom DNS server and configure hello virtual network toouse it before creating hello HDInsight cluster.</span></span>

<span data-ttu-id="67de4-177">tooenable ad çözümlemesi hello sanal ağ ve birleştirilmiş ağlarda bulunan kaynaklar arasında hello aşağıdaki eylemleri gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="67de4-177">tooenable name resolution between hello virtual network and resources in joined networks, you must perform hello following actions:</span></span>

1. <span data-ttu-id="67de4-178">Özel bir DNS sunucusu hello tooinstall Hdınsight planlama burada Azure sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="67de4-178">Create a custom DNS server in hello Azure Virtual Network where you plan tooinstall HDInsight.</span></span>

2. <span data-ttu-id="67de4-179">Merhaba sanal ağ toouse hello özel DNS sunucusunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="67de4-179">Configure hello virtual network toouse hello custom DNS server.</span></span>

3. <span data-ttu-id="67de4-180">Azure sanal ağınızın DNS soneki atanan hello bulur.</span><span class="sxs-lookup"><span data-stu-id="67de4-180">Find hello Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="67de4-181">Bu değeri çok benzer`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="67de4-181">This value is similar too`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="67de4-182">Merhaba hello DNS soneki bulma hakkında daha fazla bilgi için bkz: [örnek: özel DNS](#example-dns) bölümü.</span><span class="sxs-lookup"><span data-stu-id="67de4-182">For information on finding hello DNS suffix, see hello [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="67de4-183">İletme hello DNS sunucuları arasında yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="67de4-183">Configure forwarding between hello DNS servers.</span></span> <span data-ttu-id="67de4-184">Merhaba yapılandırma uzak ağ hello türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="67de4-184">hello configuration depends on hello type of remote network.</span></span>

    * <span data-ttu-id="67de4-185">Merhaba uzak ağ bir şirket içi ağ ise, DNS aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="67de4-185">If hello remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="67de4-186">__Özel DNS__ (Merhaba sanal ağındaki):</span><span class="sxs-lookup"><span data-stu-id="67de4-186">__Custom DNS__ (in hello virtual network):</span></span>

            * <span data-ttu-id="67de4-187">Merhaba DNS sonekini hello sanal ağ toohello Azure özyinelemeli çözümleyici (168.63.129.16) istekleri ilet.</span><span class="sxs-lookup"><span data-stu-id="67de4-187">Forward requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="67de4-188">Azure hello sanal ağ içindeki kaynaklar için istekleri işleyen</span><span class="sxs-lookup"><span data-stu-id="67de4-188">Azure handles requests for resources in hello virtual network</span></span>

            * <span data-ttu-id="67de4-189">Tüm diğer istekleri toohello şirket içi DNS sunucusu iletin.</span><span class="sxs-lookup"><span data-stu-id="67de4-189">Forward all other requests toohello on-premises DNS server.</span></span> <span data-ttu-id="67de4-190">Merhaba DNS diğer tüm ad çözümleme isteklerini Internet kaynakların Microsoft.com gibi bile istekleri işleyen şirket içi.</span><span class="sxs-lookup"><span data-stu-id="67de4-190">hello on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="67de4-191">__Şirket içi DNS__: iletmek hello sanal ağ DNS soneki toohello özel DNS sunucusu için istek.</span><span class="sxs-lookup"><span data-stu-id="67de4-191">__On-premises DNS__: Forward requests for hello virtual network DNS suffix toohello custom DNS server.</span></span> <span data-ttu-id="67de4-192">Merhaba özel DNS sunucusu, daha sonra toohello Azure özyinelemeli çözümleyici iletir.</span><span class="sxs-lookup"><span data-stu-id="67de4-192">hello custom DNS server then forwards toohello Azure recursive resolver.</span></span>

        <span data-ttu-id="67de4-193">Bu yapılandırma yolları isteklerinde hello DNS sonekinde hello sanal ağ toohello özel DNS sunucusunun etki alanı adları tam.</span><span class="sxs-lookup"><span data-stu-id="67de4-193">This configuration routes requests for fully qualified domain names that contain hello DNS suffix of hello virtual network toohello custom DNS server.</span></span> <span data-ttu-id="67de4-194">(Hatta genel internet adresleri için) tüm diğer isteklerden hello şirket içi DNS sunucusu tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="67de4-194">All other requests (even for public internet addresses) are handled by hello on-premises DNS server.</span></span>

    * <span data-ttu-id="67de4-195">Merhaba uzak ağ başka bir Azure sanal ağ ise, DNS aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="67de4-195">If hello remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="67de4-196">__Özel DNS__ (her sanal ağındaki):</span><span class="sxs-lookup"><span data-stu-id="67de4-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="67de4-197">Merhaba DNS sonekini hello sanal ağlar için istekleri toohello özel DNS sunucularını iletilir.</span><span class="sxs-lookup"><span data-stu-id="67de4-197">Requests for hello DNS suffix of hello virtual networks are forwarded toohello custom DNS servers.</span></span> <span data-ttu-id="67de4-198">Merhaba DNS her sanal ağ içindeki alt ağ içindeki kaynakların çözümlemek için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="67de4-198">hello DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="67de4-199">Tüm diğer istekleri toohello Azure özyinelemeli çözümleyici iletin.</span><span class="sxs-lookup"><span data-stu-id="67de4-199">Forward all other requests toohello Azure recursive resolver.</span></span> <span data-ttu-id="67de4-200">Merhaba özyinelemeli çözümleyici yerel çözme ve Internet kaynakların sorumludur.</span><span class="sxs-lookup"><span data-stu-id="67de4-200">hello recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="67de4-201">Merhaba DNS sunucusu her ağ için DNS soneki göre diğer istekleri toohello iletir.</span><span class="sxs-lookup"><span data-stu-id="67de4-201">hello DNS server for each network forwards requests toohello other, based on DNS suffix.</span></span> <span data-ttu-id="67de4-202">Diğer istekleri hello Azure özyinelemeli çözümleyici kullanarak çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="67de4-202">Other requests are resolved using hello Azure recursive resolver.</span></span>

    <span data-ttu-id="67de4-203">Her yapılandırma örneği için bkz: Merhaba [örnek: özel DNS](#example-dns) bölümü.</span><span class="sxs-lookup"><span data-stu-id="67de4-203">For an example of each configuration, see hello [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="67de4-204">Daha fazla bilgi için bkz: Merhaba [VM'ler ve rol örnekleri için ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) belge.</span><span class="sxs-lookup"><span data-stu-id="67de4-204">For more information, see hello [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-toohadoop-services"></a><span data-ttu-id="67de4-205">TooHadoop Hizmetleri doğrudan bağlanın</span><span class="sxs-lookup"><span data-stu-id="67de4-205">Directly connect tooHadoop services</span></span>

<span data-ttu-id="67de4-206">Hdınsight üzerinde çoğu belgelerine hello erişim toohello küme sahip olduğunuzu varsayar Internet.</span><span class="sxs-lookup"><span data-stu-id="67de4-206">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="67de4-207">Https://CLUSTERNAME.azurehdinsight.net toohello kümesine bağlayabilirsiniz örneğin.</span><span class="sxs-lookup"><span data-stu-id="67de4-207">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="67de4-208">Bu adres Nsg'ler kullandınız veya Udr'ler toorestrict erişimden hello Internet kullanılabilir değilse hello ortak ağ geçidi, kullanır.</span><span class="sxs-lookup"><span data-stu-id="67de4-208">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="67de4-209">tooconnect tooAmbari ve diğer web sayfalarını hello sanal ağ üzerinden hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="67de4-209">tooconnect tooAmbari and other web pages through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="67de4-210">Merhaba Hdınsight küme düğümlerinin toodiscover hello iç tam etki alanı adları (FQDN) aşağıdaki yöntemleri hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="67de4-210">toodiscover hello internal fully qualified domain names (FQDN) of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    <span data-ttu-id="67de4-211">Verilen düğüm listesi Merhaba, hello FQDN Merhaba baş düğümler bulmak ve hello FQDN'ler tooconnect tooAmbari ve diğer web Hizmetleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="67de4-211">In hello list of nodes returned, find hello FQDN for hello head nodes and use hello FQDNs tooconnect tooAmbari and other web services.</span></span> <span data-ttu-id="67de4-212">Örneğin, `http://<headnode-fqdn>:8080` tooaccess Ambari.</span><span class="sxs-lookup"><span data-stu-id="67de4-212">For example, use `http://<headnode-fqdn>:8080` tooaccess Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="67de4-213">Merhaba baş düğümler üzerinde barındırılan bazı hizmetler aynı anda yalnızca bir düğümde etkin olur.</span><span class="sxs-lookup"><span data-stu-id="67de4-213">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="67de4-214">Bir hizmet bir baş düğüm üzerindeki erişmeyi deneyin ve bir 404 hatası döndürürse toohello diğer baş düğüm geçin.</span><span class="sxs-lookup"><span data-stu-id="67de4-214">If you try accessing a service on one head node and it returns a 404 error, switch toohello other head node.</span></span>

2. <span data-ttu-id="67de4-215">toodetermine hello düğümünü ve bir hizmet, kullanılabilir bağlantı noktası bkz hello [hdınsight'ta Hadoop Hizmetleri tarafından kullanılan bağlantı noktaları](./hdinsight-hadoop-port-settings-for-services.md) belge.</span><span class="sxs-lookup"><span data-stu-id="67de4-215">toodetermine hello node and port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="67de4-216"><a id="networktraffic"></a>Ağ trafiğini denetleme</span><span class="sxs-lookup"><span data-stu-id="67de4-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="67de4-217">Bir Azure sanal ağlarda ağ trafiğini, yöntemler aşağıdaki hello kullanılarak denetlenebilir:</span><span class="sxs-lookup"><span data-stu-id="67de4-217">Network traffic in an Azure Virtual Networks can be controlled using hello following methods:</span></span>

* <span data-ttu-id="67de4-218">**Ağ güvenlik grupları** (NSG) toofilter gelen ve giden trafik toohello ağ izin verin.</span><span class="sxs-lookup"><span data-stu-id="67de4-218">**Network security groups** (NSG) allow you toofilter inbound and outbound traffic toohello network.</span></span> <span data-ttu-id="67de4-219">Daha fazla bilgi için bkz: Merhaba [filtre ağ güvenlik grupları ile ağ trafiği](../virtual-network/virtual-networks-nsg.md) belge.</span><span class="sxs-lookup"><span data-stu-id="67de4-219">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="67de4-220">Hdınsight giden trafiği kısıtlama desteklemez.</span><span class="sxs-lookup"><span data-stu-id="67de4-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="67de4-221">**Kullanıcı tanımlı yollar** (UDR) nasıl hello ağ kaynakları arasında trafiği akan tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="67de4-221">**User-defined routes** (UDR) define how traffic flows between resources in hello network.</span></span> <span data-ttu-id="67de4-222">Daha fazla bilgi için bkz: Merhaba [kullanıcı tanımlı yollar ve IP iletimini](../virtual-network/virtual-networks-udr-overview.md) belge.</span><span class="sxs-lookup"><span data-stu-id="67de4-222">For more information, see hello [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="67de4-223">**Ağ sanal Gereçleri** çoğaltmak güvenlik duvarları ve yönlendiriciler gibi cihazların Merhaba işlevselliği.</span><span class="sxs-lookup"><span data-stu-id="67de4-223">**Network virtual appliances** replicate hello functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="67de4-224">Daha fazla bilgi için bkz: Merhaba [ağ uygulamaları](https://azure.microsoft.com/solutions/network-appliances) belge.</span><span class="sxs-lookup"><span data-stu-id="67de4-224">For more information, see hello [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="67de4-225">Yönetilen bir hizmet olarak Hdınsight Kısıtlanmamış erişim tooAzure sistem durumu ve yönetim Hizmetleri'nde hello Azure bulut gerektirir.</span><span class="sxs-lookup"><span data-stu-id="67de4-225">As a managed service, HDInsight requires unrestricted access tooAzure health and management services in hello Azure cloud.</span></span> <span data-ttu-id="67de4-226">Nsg'ler ve Udr'ler kullanırken Hdınsight hizmetlerin hala Hdınsight ile iletişim kurabildiğinden emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="67de4-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="67de4-227">Hdınsight, çeşitli bağlantı noktaları üzerinde hizmetleri sunar.</span><span class="sxs-lookup"><span data-stu-id="67de4-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="67de4-228">Bir sanal gereç Güvenlik Duvarı'nı kullanırken, bu hizmetler için kullanılan bağlantı noktaları hello üzerinde trafiğe izin vermelidir.</span><span class="sxs-lookup"><span data-stu-id="67de4-228">When using a virtual appliance firewall, you must allow traffic on hello ports used for these services.</span></span> <span data-ttu-id="67de4-229">Daha fazla bilgi için hello [gerekli bağlantı noktalarını] bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="67de4-229">For more information, see hello [Required ports] section.</span></span>

### <span data-ttu-id="67de4-230"><a id="hdinsight-ip"></a>Hdınsight ile ağ güvenlik gruplarını ve kullanıcı tanımlı yollar</span><span class="sxs-lookup"><span data-stu-id="67de4-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="67de4-231">Kullanmayı planlıyorsanız, **ağ güvenlik grubu** veya **kullanıcı tanımlı yollar** toocontrol ağ trafiğini, Eylemler Hdınsight'ı yüklemeden önce aşağıdaki hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="67de4-231">If you plan on using **network security groups** or **user-defined routes** toocontrol network traffic, perform hello following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="67de4-232">Merhaba toouse Hdınsight için planlama Azure bölgesi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="67de4-232">Identify hello Azure region that you plan toouse for HDInsight.</span></span>

2. <span data-ttu-id="67de4-233">Hdınsight tarafından gerekli hello IP adreslerini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="67de4-233">Identify hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="67de4-234">Daha fazla bilgi için bkz: Merhaba [Hdınsight tarafından gerekli IP adreslerini](#hdinsight-ip) bölüm.</span><span class="sxs-lookup"><span data-stu-id="67de4-234">For more information, see hello [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="67de4-235">Oluşturma veya hello ağ güvenlik grupları veya kullanıcı tanımlı yollar tooinstall Hdınsight planlama hello alt ağ için değiştirme içine.</span><span class="sxs-lookup"><span data-stu-id="67de4-235">Create or modify hello network security groups or user-defined routes for hello subnet that you plan tooinstall HDInsight into.</span></span>

    * <span data-ttu-id="67de4-236">__Ağ güvenlik grupları__: izin __gelen__ bağlantı noktasında trafik __443__ hello IP adreslerinden.</span><span class="sxs-lookup"><span data-stu-id="67de4-236">__Network security groups__: allow __inbound__ traffic on port __443__ from hello IP addresses.</span></span>
    * <span data-ttu-id="67de4-237">__Kullanıcı tanımlı yollar__: bir rota tooeach IP adresi oluşturma ve ayarlama hello __sonraki atlama türü__ too__Internet__.</span><span class="sxs-lookup"><span data-stu-id="67de4-237">__User-defined routes__: create a route tooeach IP address and set hello __Next hop type__ too__Internet__.</span></span>

<span data-ttu-id="67de4-238">Ağ güvenlik grupları veya kullanıcı tanımlı yollar hakkında daha fazla bilgi için belge aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="67de4-238">For more information on network security groups or user-defined routes, see hello following documentation:</span></span>

* [<span data-ttu-id="67de4-239">Ağ güvenlik grubu</span><span class="sxs-lookup"><span data-stu-id="67de4-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="67de4-240">Kullanıcı tanımlı yollar</span><span class="sxs-lookup"><span data-stu-id="67de4-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="67de4-241">Zorlamalı tünel oluşturma</span><span class="sxs-lookup"><span data-stu-id="67de4-241">Forced tunneling</span></span>

<span data-ttu-id="67de4-242">Zorlamalı tünel kullanıcı tanımlı yönlendirme yapılandırması bir alt ağdaki tüm trafiği zorunlu tooa belirli ağ veya şirket içi ağınız gibi konuma olduğu.</span><span class="sxs-lookup"><span data-stu-id="67de4-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced tooa specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="67de4-243">Hdınsight mu __değil__ destek zorlamalı tünel.</span><span class="sxs-lookup"><span data-stu-id="67de4-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="67de4-244"><a id="hdinsight-ip"></a>Gerekli IP adresi</span><span class="sxs-lookup"><span data-stu-id="67de4-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67de4-245">Azure sistem durumu hello ve Yönetim Hizmetleri Hdınsight ile mümkün toocommunicate olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="67de4-245">hello Azure health and management services must be able toocommunicate with HDInsight.</span></span> <span data-ttu-id="67de4-246">Ağ güvenlik grupları veya kullanıcı tanımlı yollar kullanıyorsanız, bu hizmetleri tooreach Hdınsight için IP adresleri hello trafiğinden izin verin.</span><span class="sxs-lookup"><span data-stu-id="67de4-246">If you use network security groups or user-defined routes, allow traffic from hello IP addresses for these services tooreach HDInsight.</span></span>
>
> <span data-ttu-id="67de4-247">Ağ güvenlik grupları veya kullanıcı tanımlı yollar toocontrol trafik kullanmıyorsanız, bu bölüm göz ardı edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67de4-247">If you do not use network security groups or user-defined routes toocontrol traffic, you can ignore this section.</span></span>

<span data-ttu-id="67de4-248">Ağ güvenlik grupları veya kullanıcı tanımlı yollar kullanıyorsanız, hello Azure sistem durumu ve Yönetim Hizmetleri tooreach Hdınsight gelen trafiğe izin vermelidir.</span><span class="sxs-lookup"><span data-stu-id="67de4-248">If you use network security groups or user-defined routes, you must allow traffic from hello Azure health and management services tooreach HDInsight.</span></span> <span data-ttu-id="67de4-249">İzin verilmiş olmalıdır adımları toofind hello IP adreslerini aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="67de4-249">Use hello following steps toofind hello IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="67de4-250">Her zaman IP adreslerini aşağıdaki hello gelen trafiğe izin vermeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="67de4-250">You must always allow traffic from hello following IP addresses:</span></span>

    | <span data-ttu-id="67de4-251">IP adresi</span><span class="sxs-lookup"><span data-stu-id="67de4-251">IP address</span></span> | <span data-ttu-id="67de4-252">İzin verilen bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="67de4-252">Allowed port</span></span> | <span data-ttu-id="67de4-253">Yön</span><span class="sxs-lookup"><span data-stu-id="67de4-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="67de4-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="67de4-254">168.61.49.99</span></span> | <span data-ttu-id="67de4-255">443</span><span class="sxs-lookup"><span data-stu-id="67de4-255">443</span></span> | <span data-ttu-id="67de4-256">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-256">Inbound</span></span> |
    | <span data-ttu-id="67de4-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="67de4-257">23.99.5.239</span></span> | <span data-ttu-id="67de4-258">443</span><span class="sxs-lookup"><span data-stu-id="67de4-258">443</span></span> | <span data-ttu-id="67de4-259">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-259">Inbound</span></span> |
    | <span data-ttu-id="67de4-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="67de4-260">168.61.48.131</span></span> | <span data-ttu-id="67de4-261">443</span><span class="sxs-lookup"><span data-stu-id="67de4-261">443</span></span> | <span data-ttu-id="67de4-262">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-262">Inbound</span></span> |
    | <span data-ttu-id="67de4-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="67de4-263">138.91.141.162</span></span> | <span data-ttu-id="67de4-264">443</span><span class="sxs-lookup"><span data-stu-id="67de4-264">443</span></span> | <span data-ttu-id="67de4-265">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-265">Inbound</span></span> |

2. <span data-ttu-id="67de4-266">Hdınsight kümenize bölgeleri aşağıdaki hello birinde ise, hello bölge için listelenen hello IP adreslerinden gelen trafiğe izin vermelidir:</span><span class="sxs-lookup"><span data-stu-id="67de4-266">If your HDInsight cluster is in one of hello following regions, then you must allow traffic from hello IP addresses listed for hello region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="67de4-267">Merhaba, kullanmakta olduğunuz Azure bölgesi listede yoksa, yalnızca hello dört IP adresleri adım 1'deki kullanın.</span><span class="sxs-lookup"><span data-stu-id="67de4-267">If hello Azure region you are using is not listed, then only use hello four IP addresses from step 1.</span></span>

    | <span data-ttu-id="67de4-268">Ülke</span><span class="sxs-lookup"><span data-stu-id="67de4-268">Country</span></span> | <span data-ttu-id="67de4-269">Bölge</span><span class="sxs-lookup"><span data-stu-id="67de4-269">Region</span></span> | <span data-ttu-id="67de4-270">İzin verilen IP adresi</span><span class="sxs-lookup"><span data-stu-id="67de4-270">Allowed IP addresses</span></span> | <span data-ttu-id="67de4-271">İzin verilen bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="67de4-271">Allowed port</span></span> | <span data-ttu-id="67de4-272">Yön</span><span class="sxs-lookup"><span data-stu-id="67de4-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="67de4-273">Asya</span><span class="sxs-lookup"><span data-stu-id="67de4-273">Asia</span></span> | <span data-ttu-id="67de4-274">Doğu Asya</span><span class="sxs-lookup"><span data-stu-id="67de4-274">East Asia</span></span> | <span data-ttu-id="67de4-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="67de4-275">23.102.235.122</span></span></br><span data-ttu-id="67de4-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="67de4-276">52.175.38.134</span></span> | <span data-ttu-id="67de4-277">443</span><span class="sxs-lookup"><span data-stu-id="67de4-277">443</span></span> | <span data-ttu-id="67de4-278">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="67de4-279">Güneydoğu Asya</span><span class="sxs-lookup"><span data-stu-id="67de4-279">Southeast Asia</span></span> | <span data-ttu-id="67de4-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="67de4-280">13.76.245.160</span></span></br><span data-ttu-id="67de4-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="67de4-281">13.76.136.249</span></span> | <span data-ttu-id="67de4-282">443</span><span class="sxs-lookup"><span data-stu-id="67de4-282">443</span></span> | <span data-ttu-id="67de4-283">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-283">Inbound</span></span> |
    | <span data-ttu-id="67de4-284">Avustralya</span><span class="sxs-lookup"><span data-stu-id="67de4-284">Australia</span></span> | <span data-ttu-id="67de4-285">Avustralya Doğu</span><span class="sxs-lookup"><span data-stu-id="67de4-285">Australia East</span></span> | <span data-ttu-id="67de4-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="67de4-286">104.210.84.115</span></span></br><span data-ttu-id="67de4-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="67de4-287">13.75.152.195</span></span> | <span data-ttu-id="67de4-288">443</span><span class="sxs-lookup"><span data-stu-id="67de4-288">443</span></span> | <span data-ttu-id="67de4-289">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="67de4-290">Avustralya Güneydoğu</span><span class="sxs-lookup"><span data-stu-id="67de4-290">Australia Southeast</span></span> | <span data-ttu-id="67de4-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="67de4-291">13.77.2.56</span></span></br><span data-ttu-id="67de4-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="67de4-292">13.77.2.94</span></span> | <span data-ttu-id="67de4-293">443</span><span class="sxs-lookup"><span data-stu-id="67de4-293">443</span></span> | <span data-ttu-id="67de4-294">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-294">Inbound</span></span> |
    | <span data-ttu-id="67de4-295">Brezilya</span><span class="sxs-lookup"><span data-stu-id="67de4-295">Brazil</span></span> | <span data-ttu-id="67de4-296">Güney Brezilya</span><span class="sxs-lookup"><span data-stu-id="67de4-296">Brazil South</span></span> | <span data-ttu-id="67de4-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="67de4-297">191.235.84.104</span></span></br><span data-ttu-id="67de4-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="67de4-298">191.235.87.113</span></span> | <span data-ttu-id="67de4-299">443</span><span class="sxs-lookup"><span data-stu-id="67de4-299">443</span></span> | <span data-ttu-id="67de4-300">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-300">Inbound</span></span> |
    | <span data-ttu-id="67de4-301">Kanada</span><span class="sxs-lookup"><span data-stu-id="67de4-301">Canada</span></span> | <span data-ttu-id="67de4-302">Doğu Kanada</span><span class="sxs-lookup"><span data-stu-id="67de4-302">Canada East</span></span> | <span data-ttu-id="67de4-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="67de4-303">52.229.127.96</span></span></br><span data-ttu-id="67de4-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="67de4-304">52.229.123.172</span></span> | <span data-ttu-id="67de4-305">443</span><span class="sxs-lookup"><span data-stu-id="67de4-305">443</span></span> | <span data-ttu-id="67de4-306">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="67de4-307">Orta Kanada</span><span class="sxs-lookup"><span data-stu-id="67de4-307">Canada Central</span></span> | <span data-ttu-id="67de4-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="67de4-308">52.228.37.66</span></span></br><span data-ttu-id="67de4-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="67de4-309">52.228.45.222</span></span> | <span data-ttu-id="67de4-310">443</span><span class="sxs-lookup"><span data-stu-id="67de4-310">443</span></span> | <span data-ttu-id="67de4-311">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-311">Inbound</span></span> |
    | <span data-ttu-id="67de4-312">Çin</span><span class="sxs-lookup"><span data-stu-id="67de4-312">China</span></span> | <span data-ttu-id="67de4-313">Çin Kuzey</span><span class="sxs-lookup"><span data-stu-id="67de4-313">China North</span></span> | <span data-ttu-id="67de4-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="67de4-314">42.159.96.170</span></span></br><span data-ttu-id="67de4-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="67de4-315">139.217.2.219</span></span> | <span data-ttu-id="67de4-316">443</span><span class="sxs-lookup"><span data-stu-id="67de4-316">443</span></span> | <span data-ttu-id="67de4-317">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="67de4-318">Çin Doğu</span><span class="sxs-lookup"><span data-stu-id="67de4-318">China East</span></span> | <span data-ttu-id="67de4-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="67de4-319">42.159.198.178</span></span></br><span data-ttu-id="67de4-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="67de4-320">42.159.234.157</span></span> | <span data-ttu-id="67de4-321">443</span><span class="sxs-lookup"><span data-stu-id="67de4-321">443</span></span> | <span data-ttu-id="67de4-322">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-322">Inbound</span></span> |
    | <span data-ttu-id="67de4-323">Avrupa</span><span class="sxs-lookup"><span data-stu-id="67de4-323">Europe</span></span> | <span data-ttu-id="67de4-324">Kuzey Avrupa</span><span class="sxs-lookup"><span data-stu-id="67de4-324">North Europe</span></span> | <span data-ttu-id="67de4-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="67de4-325">52.164.210.96</span></span></br><span data-ttu-id="67de4-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="67de4-326">13.74.153.132</span></span> | <span data-ttu-id="67de4-327">443</span><span class="sxs-lookup"><span data-stu-id="67de4-327">443</span></span> | <span data-ttu-id="67de4-328">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="67de4-329">Batı Avrupa</span><span class="sxs-lookup"><span data-stu-id="67de4-329">West Europe</span></span>| <span data-ttu-id="67de4-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="67de4-330">52.166.243.90</span></span></br><span data-ttu-id="67de4-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="67de4-331">52.174.36.244</span></span> | <span data-ttu-id="67de4-332">443</span><span class="sxs-lookup"><span data-stu-id="67de4-332">443</span></span> | <span data-ttu-id="67de4-333">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-333">Inbound</span></span> |
    | <span data-ttu-id="67de4-334">Almanya</span><span class="sxs-lookup"><span data-stu-id="67de4-334">Germany</span></span> | <span data-ttu-id="67de4-335">Almanya Orta</span><span class="sxs-lookup"><span data-stu-id="67de4-335">Germany Central</span></span> | <span data-ttu-id="67de4-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="67de4-336">51.4.146.68</span></span></br><span data-ttu-id="67de4-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="67de4-337">51.4.146.80</span></span> | <span data-ttu-id="67de4-338">443</span><span class="sxs-lookup"><span data-stu-id="67de4-338">443</span></span> | <span data-ttu-id="67de4-339">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="67de4-340">Almanya Kuzeydoğu</span><span class="sxs-lookup"><span data-stu-id="67de4-340">Germany Northeast</span></span> | <span data-ttu-id="67de4-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="67de4-341">51.5.150.132</span></span></br><span data-ttu-id="67de4-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="67de4-342">51.5.144.101</span></span> | <span data-ttu-id="67de4-343">443</span><span class="sxs-lookup"><span data-stu-id="67de4-343">443</span></span> | <span data-ttu-id="67de4-344">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-344">Inbound</span></span> |
    | <span data-ttu-id="67de4-345">Hindistan</span><span class="sxs-lookup"><span data-stu-id="67de4-345">India</span></span> | <span data-ttu-id="67de4-346">Orta Hindistan</span><span class="sxs-lookup"><span data-stu-id="67de4-346">Central India</span></span> | <span data-ttu-id="67de4-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="67de4-347">52.172.153.209</span></span></br><span data-ttu-id="67de4-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="67de4-348">52.172.152.49</span></span> | <span data-ttu-id="67de4-349">443</span><span class="sxs-lookup"><span data-stu-id="67de4-349">443</span></span> | <span data-ttu-id="67de4-350">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-350">Inbound</span></span> |
    | <span data-ttu-id="67de4-351">Japonya</span><span class="sxs-lookup"><span data-stu-id="67de4-351">Japan</span></span> | <span data-ttu-id="67de4-352">Japonya Doğu</span><span class="sxs-lookup"><span data-stu-id="67de4-352">Japan East</span></span> | <span data-ttu-id="67de4-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="67de4-353">13.78.125.90</span></span></br><span data-ttu-id="67de4-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="67de4-354">13.78.89.60</span></span> | <span data-ttu-id="67de4-355">443</span><span class="sxs-lookup"><span data-stu-id="67de4-355">443</span></span> | <span data-ttu-id="67de4-356">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="67de4-357">Japonya Batı</span><span class="sxs-lookup"><span data-stu-id="67de4-357">Japan West</span></span> | <span data-ttu-id="67de4-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="67de4-358">40.74.125.69</span></span></br><span data-ttu-id="67de4-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="67de4-359">138.91.29.150</span></span> | <span data-ttu-id="67de4-360">443</span><span class="sxs-lookup"><span data-stu-id="67de4-360">443</span></span> | <span data-ttu-id="67de4-361">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-361">Inbound</span></span> |
    | <span data-ttu-id="67de4-362">Kore</span><span class="sxs-lookup"><span data-stu-id="67de4-362">Korea</span></span> | <span data-ttu-id="67de4-363">Kore Orta</span><span class="sxs-lookup"><span data-stu-id="67de4-363">Korea Central</span></span> | <span data-ttu-id="67de4-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="67de4-364">52.231.39.142</span></span></br><span data-ttu-id="67de4-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="67de4-365">52.231.36.209</span></span> | <span data-ttu-id="67de4-366">433</span><span class="sxs-lookup"><span data-stu-id="67de4-366">433</span></span> | <span data-ttu-id="67de4-367">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="67de4-368">Kore Güney</span><span class="sxs-lookup"><span data-stu-id="67de4-368">Korea South</span></span> | <span data-ttu-id="67de4-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="67de4-369">52.231.203.16</span></span></br><span data-ttu-id="67de4-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="67de4-370">52.231.205.214</span></span> | <span data-ttu-id="67de4-371">443</span><span class="sxs-lookup"><span data-stu-id="67de4-371">443</span></span> | <span data-ttu-id="67de4-372">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-372">Inbound</span></span>
    | <span data-ttu-id="67de4-373">Birleşik Krallık</span><span class="sxs-lookup"><span data-stu-id="67de4-373">United Kingdom</span></span> | <span data-ttu-id="67de4-374">Birleşik Krallık Batı</span><span class="sxs-lookup"><span data-stu-id="67de4-374">UK West</span></span> | <span data-ttu-id="67de4-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="67de4-375">51.141.13.110</span></span></br><span data-ttu-id="67de4-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="67de4-376">51.141.7.20</span></span> | <span data-ttu-id="67de4-377">443</span><span class="sxs-lookup"><span data-stu-id="67de4-377">443</span></span> | <span data-ttu-id="67de4-378">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="67de4-379">Birleşik Krallık Güney</span><span class="sxs-lookup"><span data-stu-id="67de4-379">UK South</span></span> | <span data-ttu-id="67de4-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="67de4-380">51.140.47.39</span></span></br><span data-ttu-id="67de4-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="67de4-381">51.140.52.16</span></span> | <span data-ttu-id="67de4-382">443</span><span class="sxs-lookup"><span data-stu-id="67de4-382">443</span></span> | <span data-ttu-id="67de4-383">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-383">Inbound</span></span> |
    | <span data-ttu-id="67de4-384">Amerika Birleşik Devletleri</span><span class="sxs-lookup"><span data-stu-id="67de4-384">United States</span></span> | <span data-ttu-id="67de4-385">Orta ABD</span><span class="sxs-lookup"><span data-stu-id="67de4-385">Central US</span></span> | <span data-ttu-id="67de4-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="67de4-386">13.67.223.215</span></span></br><span data-ttu-id="67de4-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="67de4-387">40.86.83.253</span></span> | <span data-ttu-id="67de4-388">443</span><span class="sxs-lookup"><span data-stu-id="67de4-388">443</span></span> | <span data-ttu-id="67de4-389">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="67de4-390">Orta Kuzey ABD</span><span class="sxs-lookup"><span data-stu-id="67de4-390">North Central US</span></span> | <span data-ttu-id="67de4-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="67de4-391">157.56.8.38</span></span></br><span data-ttu-id="67de4-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="67de4-392">157.55.213.99</span></span> | <span data-ttu-id="67de4-393">443</span><span class="sxs-lookup"><span data-stu-id="67de4-393">443</span></span> | <span data-ttu-id="67de4-394">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="67de4-395">Batı Orta ABD</span><span class="sxs-lookup"><span data-stu-id="67de4-395">West Central US</span></span> | <span data-ttu-id="67de4-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="67de4-396">52.161.23.15</span></span></br><span data-ttu-id="67de4-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="67de4-397">52.161.10.167</span></span> | <span data-ttu-id="67de4-398">443</span><span class="sxs-lookup"><span data-stu-id="67de4-398">443</span></span> | <span data-ttu-id="67de4-399">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="67de4-400">Batı ABD 2</span><span class="sxs-lookup"><span data-stu-id="67de4-400">West US 2</span></span> | <span data-ttu-id="67de4-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="67de4-401">52.175.211.210</span></span></br><span data-ttu-id="67de4-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="67de4-402">52.175.222.222</span></span> | <span data-ttu-id="67de4-403">443</span><span class="sxs-lookup"><span data-stu-id="67de4-403">443</span></span> | <span data-ttu-id="67de4-404">Gelen</span><span class="sxs-lookup"><span data-stu-id="67de4-404">Inbound</span></span> |

    <span data-ttu-id="67de4-405">Merhaba hello IP hakkında bilgi için Azure kamu toouse adresleri için bkz: [Azure Kamu Intelligence + analiz](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) belge.</span><span class="sxs-lookup"><span data-stu-id="67de4-405">For information on hello IP addresses toouse for Azure Government, see hello [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="67de4-406">Sanal ağınız ile özel bir DNS sunucusu kullanıyorsanız, erişimden de izin vermeniz gerekir __168.63.129.16__.</span><span class="sxs-lookup"><span data-stu-id="67de4-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="67de4-407">Azure'nın özyinelemeli çözümleyici adresidir.</span><span class="sxs-lookup"><span data-stu-id="67de4-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="67de4-408">Daha fazla bilgi için bkz: Merhaba [VM'ler ve rol için ad çözümlemesi örnekleri](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) belge.</span><span class="sxs-lookup"><span data-stu-id="67de4-408">For more information, see hello [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="67de4-409">Daha fazla bilgi için bkz: Merhaba [ağ trafiğini denetleme](#networktraffic) bölümü.</span><span class="sxs-lookup"><span data-stu-id="67de4-409">For more information, see hello [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="67de4-410"><a id="hdinsight-ports"></a>Gerekli bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="67de4-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="67de4-411">Bir ağı kullanmayı planlıyorsanız, **sanal gereç Güvenlik Duvarı** toosecure hello sanal ağ, size izin vermelidir giden trafiği bağlantı noktaları aşağıdaki hello üzerinde:</span><span class="sxs-lookup"><span data-stu-id="67de4-411">If you plan on using a network **virtual appliance firewall** toosecure hello virtual network, you must allow outbound traffic on hello following ports:</span></span>

* <span data-ttu-id="67de4-412">53</span><span class="sxs-lookup"><span data-stu-id="67de4-412">53</span></span>
* <span data-ttu-id="67de4-413">443</span><span class="sxs-lookup"><span data-stu-id="67de4-413">443</span></span>
* <span data-ttu-id="67de4-414">1433</span><span class="sxs-lookup"><span data-stu-id="67de4-414">1433</span></span>
* <span data-ttu-id="67de4-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="67de4-415">11000-11999</span></span>
* <span data-ttu-id="67de4-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="67de4-416">14000-14999</span></span>

<span data-ttu-id="67de4-417">Merhaba belirli hizmetleri için bağlantı noktalarının listesi için bkz [hdınsight'ta Hadoop Hizmetleri tarafından kullanılan bağlantı noktaları](hdinsight-hadoop-port-settings-for-services.md) belge.</span><span class="sxs-lookup"><span data-stu-id="67de4-417">For a list of ports for specific services, see hello [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="67de4-418">Sanal gereçler için güvenlik duvarı kuralları hakkında daha fazla bilgi için bkz: Merhaba [sanal gereç senaryo](../virtual-network/virtual-network-scenario-udr-gw-nva.md) belge.</span><span class="sxs-lookup"><span data-stu-id="67de4-418">For more information on firewall rules for virtual appliances, see hello [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="67de4-419"><a id="hdinsight-nsg"></a>Örnek: ağ güvenlik grupları Hdınsight ile</span><span class="sxs-lookup"><span data-stu-id="67de4-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="67de4-420">Bu bölümdeki Hello örnekler, nasıl Azure Yönetim Hizmetleri ile Merhaba Hdınsight toocommunicate izin toocreate ağ güvenlik grubu kuralları gösterir.</span><span class="sxs-lookup"><span data-stu-id="67de4-420">hello examples in this section demonstrate how toocreate network security group rules that allow HDInsight toocommunicate with hello Azure management services.</span></span> <span data-ttu-id="67de4-421">Merhaba örnekler kullanmadan önce hello IP adreslerini toomatch Merhaba olanları hello kullanmakta olduğunuz Azure bölgesini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="67de4-421">Before using hello examples, adjust hello IP addresses toomatch hello ones for hello Azure region you are using.</span></span> <span data-ttu-id="67de4-422">Bu bilgileri hello bulabilirsiniz [Hdınsight ağ güvenlik gruplarını ve kullanıcı tanımlı yollar ile](#hdinsight-ip) bölümü.</span><span class="sxs-lookup"><span data-stu-id="67de4-422">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="67de4-423">Azure kaynak yönetimi şablonu</span><span class="sxs-lookup"><span data-stu-id="67de4-423">Azure Resource Management template</span></span>

<span data-ttu-id="67de4-424">Merhaba aşağıdaki kaynak yönetimi şablon gelen trafiği sınırlar, ancak Hdınsight tarafından gerekli hello IP adreslerinden gelen trafiğe izin veren bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="67de4-424">hello following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="67de4-425">Bu şablon, hello sanal ağında ayrıca bir Hdınsight kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="67de4-425">This template also creates an HDInsight cluster in hello virtual network.</span></span>

* [<span data-ttu-id="67de4-426">Güvenli bir Azure sanal ağ ve bir Hdınsight Hadoop kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="67de4-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="67de4-427">Bu örnek toomatch hello kullanmakta olduğunuz Azure bölgesi kullanılan hello IP adreslerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="67de4-427">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="67de4-428">Bu bilgileri hello bulabilirsiniz [Hdınsight ağ güvenlik gruplarını ve kullanıcı tanımlı yollar ile](#hdinsight-ip) bölümü.</span><span class="sxs-lookup"><span data-stu-id="67de4-428">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="67de4-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="67de4-429">Azure PowerShell</span></span>

<span data-ttu-id="67de4-430">PowerShell komut dosyası toocreate gelen trafiği kısıtlar ve hello trafiğinden hello Kuzey Avrupa bölge için IP adreslerini sağlayan bir sanal ağ aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="67de4-430">Use hello following PowerShell script toocreate a virtual network that restricts inbound traffic and allows traffic from hello IP addresses for hello North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67de4-431">Bu örnek toomatch hello kullanmakta olduğunuz Azure bölgesi kullanılan hello IP adreslerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="67de4-431">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="67de4-432">Bu bilgileri hello bulabilirsiniz [Hdınsight ağ güvenlik gruplarını ve kullanıcı tanımlı yollar ile](#hdinsight-ip) bölümü.</span><span class="sxs-lookup"><span data-stu-id="67de4-432">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="67de4-433">Bu örnek nasıl tooadd kuralları tooallow gelen gerekli hello IP adreslerindeki trafiği gösterir.</span><span class="sxs-lookup"><span data-stu-id="67de4-433">This example demonstrates how tooadd rules tooallow inbound traffic on hello required IP addresses.</span></span> <span data-ttu-id="67de4-434">Bir kural toorestrict içermiyor gelen diğer kaynaklardan erişim.</span><span class="sxs-lookup"><span data-stu-id="67de4-434">It does not contain a rule toorestrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="67de4-435">Aşağıdaki örneğine hello nasıl tooenable SSH erişim Internet hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="67de4-435">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="67de4-436">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="67de4-436">Azure CLI</span></span>

<span data-ttu-id="67de4-437">Aşağıdaki adımları toocreate gelen trafik sınırlar, ancak Hdınsight tarafından gerekli hello IP adreslerinden gelen trafiğe izin veren bir sanal ağ hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="67de4-437">Use hello following steps toocreate a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="67de4-438">Yeni bir ağ güvenlik grubu adlı komut toocreate aşağıdaki kullanım hello `hdisecure`.</span><span class="sxs-lookup"><span data-stu-id="67de4-438">Use hello following command toocreate a new network security group named `hdisecure`.</span></span> <span data-ttu-id="67de4-439">Değiştir **RESOURCEGROUPNAME** hello Azure sanal ağı içeren hello kaynak grubu ile.</span><span class="sxs-lookup"><span data-stu-id="67de4-439">Replace **RESOURCEGROUPNAME** with hello resource group that contains hello Azure Virtual Network.</span></span> <span data-ttu-id="67de4-440">Değiştir **konumu** hello konum (bölge) içinde bu hello grup oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="67de4-440">Replace **LOCATION** with hello location (region) that hello group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="67de4-441">Merhaba Grup oluşturulduktan sonra hello yeni grubu hakkında bilgi alabilir.</span><span class="sxs-lookup"><span data-stu-id="67de4-441">Once hello group has been created, you receive information on hello new group.</span></span>

2. <span data-ttu-id="67de4-442">Bağlantı noktası 443 üzerinden hello Azure Hdınsight sistem durumu ve yönetim hizmeti öğesinden gelen iletişime izin tooadd kuralları toohello yeni ağ güvenlik grubu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="67de4-442">Use hello following tooadd rules toohello new network security group that allow inbound communication on port 443 from hello Azure HDInsight health and management service.</span></span> <span data-ttu-id="67de4-443">Değiştir **RESOURCEGROUPNAME** hello Azure sanal ağı içeren hello kaynak grubunun hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="67de4-443">Replace **RESOURCEGROUPNAME** with hello name of hello resource group that contains hello Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="67de4-444">Bu örnek toomatch hello kullanmakta olduğunuz Azure bölgesi kullanılan hello IP adreslerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="67de4-444">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="67de4-445">Bu bilgileri hello bulabilirsiniz [Hdınsight ağ güvenlik gruplarını ve kullanıcı tanımlı yollar ile](#hdinsight-ip) bölümü.</span><span class="sxs-lookup"><span data-stu-id="67de4-445">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="67de4-446">tooretrieve bu ağ güvenlik grubu için benzersiz tanımlayıcı Merhaba, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="67de4-446">tooretrieve hello unique identifier for this network security group, use hello following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="67de4-447">Bu komut metnini izleyen bir değer benzer toohello döndürür:</span><span class="sxs-lookup"><span data-stu-id="67de4-447">This command returns a value similar toohello following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="67de4-448">Beklenen hello sonuç alamazsanız kimliği etrafında çift tırnak hello komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="67de4-448">Use double-quotes around id in hello command if you don't get hello expected results.</span></span>

4. <span data-ttu-id="67de4-449">Kullanım hello aşağıdaki tooapply hello ağ güvenlik grubu tooa alt komutu.</span><span class="sxs-lookup"><span data-stu-id="67de4-449">Use hello following command tooapply hello network security group tooa subnet.</span></span> <span data-ttu-id="67de4-450">Hello yerine __GUID__ ve __RESOURCEGROUPNAME__ hello olanları değerlerle hello önceki adımdaki döndürdü.</span><span class="sxs-lookup"><span data-stu-id="67de4-450">Replace hello __GUID__ and __RESOURCEGROUPNAME__ values with hello ones returned from hello previous step.</span></span> <span data-ttu-id="67de4-451">Değiştir __vnetname ADLI__ ve __SUBNETNAME__ hello sanal ağ adı ve alt ağ adıyla toocreate istiyor.</span><span class="sxs-lookup"><span data-stu-id="67de4-451">Replace __VNETNAME__ and __SUBNETNAME__ with hello virtual network name and subnet name that you want toocreate.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="67de4-452">Bu komut tamamlandıktan sonra sanal ağ hello Hdınsight yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67de4-452">Once this command completes, you can install HDInsight into hello Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67de4-453">Bu adımları yalnızca access toohello Hdınsight sistem durumu ve yönetim hizmetine hello Azure bulut açın.</span><span class="sxs-lookup"><span data-stu-id="67de4-453">These steps only open access toohello HDInsight health and management service on hello Azure cloud.</span></span> <span data-ttu-id="67de4-454">Tüm diğer erişim toohello Hdınsight kümeden dış hello sanal ağ engellendi.</span><span class="sxs-lookup"><span data-stu-id="67de4-454">Any other access toohello HDInsight cluster from outside hello Virtual Network is blocked.</span></span> <span data-ttu-id="67de4-455">tooenable erişim hello sanal ağ dışından, ek ağ güvenlik grubu kuralları eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="67de4-455">tooenable access from outside hello virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="67de4-456">Aşağıdaki örneğine hello nasıl tooenable SSH erişim Internet hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="67de4-456">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="67de4-457"><a id="example-dns"></a>Örnek: DNS yapılandırması</span><span class="sxs-lookup"><span data-stu-id="67de4-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="67de4-458">Sanal bir ağa bağlı şirket içi ağ arasındaki ad çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="67de4-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="67de4-459">Bu örnek varsayımlar aşağıdaki hello yapar:</span><span class="sxs-lookup"><span data-stu-id="67de4-459">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="67de4-460">Bir Azure sanal bir VPN ağ geçidi kullanarak bağlı tooan şirket içi ağ ağ var.</span><span class="sxs-lookup"><span data-stu-id="67de4-460">You have an Azure Virtual Network that is connected tooan on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="67de4-461">Merhaba özel DNS sunucusu hello sanal ağındaki hello işletim sistemi olarak Linux veya UNIX çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="67de4-461">hello custom DNS server in hello virtual network is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="67de4-462">[Bağlama](https://www.isc.org/downloads/bind/) hello özel DNS sunucusuna yüklenir.</span><span class="sxs-lookup"><span data-stu-id="67de4-462">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS server.</span></span>

<span data-ttu-id="67de4-463">Merhaba özel DNS sunucusunda hello sanal ağ içinde:</span><span class="sxs-lookup"><span data-stu-id="67de4-463">On hello custom DNS server in hello virtual network:</span></span>

1. <span data-ttu-id="67de4-464">Sanal ağ hello Azure PowerShell veya Azure CLI toofind hello DNS sonekini kullanın:</span><span class="sxs-lookup"><span data-stu-id="67de4-464">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of hello virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="67de4-465">Merhaba özel DNS sunucusunda hello sanal ağ için metin hello Merhaba içeriğine aşağıdaki hello kullanın `/etc/bind/named.conf.local` dosyası:</span><span class="sxs-lookup"><span data-stu-id="67de4-465">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="67de4-466">Hello yerine `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` hello sanal ağınızın DNS soneki ile değer.</span><span class="sxs-lookup"><span data-stu-id="67de4-466">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="67de4-467">Bu yapılandırma tüm DNS isteklerine hello sanal ağ toohello Azure özyinelemeli çözümleyici hello DNS soneki için yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="67de4-467">This configuration routes all DNS requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver.</span></span>

2. <span data-ttu-id="67de4-468">Merhaba özel DNS sunucusunda hello sanal ağ için metin hello Merhaba içeriğine aşağıdaki hello kullanın `/etc/bind/named.conf.options` dosyası:</span><span class="sxs-lookup"><span data-stu-id="67de4-468">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="67de4-469">Hello yerine `10.0.0.0/16` hello IP adres aralığını, sanal ağınızın değerle.</span><span class="sxs-lookup"><span data-stu-id="67de4-469">Replace hello `10.0.0.0/16` value with hello IP address range of your virtual network.</span></span> <span data-ttu-id="67de4-470">Bu giriş, ad çözümleme istekleri adreslerini bu aralıkta sağlar.</span><span class="sxs-lookup"><span data-stu-id="67de4-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="67de4-471">Merhaba şirket içi ağ toohello Hello IP adres aralığı Ekle `acl goodclients { ... }` bölümü.</span><span class="sxs-lookup"><span data-stu-id="67de4-471">Add hello IP address range of hello on-premises network toohello `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="67de4-472">Giriş ad çözümleme isteklerinin kaynaklardan hello şirket ağında sağlar.</span><span class="sxs-lookup"><span data-stu-id="67de4-472">entry allows name resolution requests from resources in hello on-premises network.</span></span>
    
    * <span data-ttu-id="67de4-473">Merhaba değeri değiştirin `192.168.0.1` hello şirket içi DNS sunucunuzun IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="67de4-473">Replace hello value `192.168.0.1` with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="67de4-474">Bu giriş, tüm diğer DNS isteklerini toohello şirket DNS sunucularına yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="67de4-474">This entry routes all other DNS requests toohello on-premises DNS server.</span></span>

3. <span data-ttu-id="67de4-475">toouse hello yapılandırma, bağlama yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="67de4-475">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="67de4-476">Örneğin, `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="67de4-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="67de4-477">Bir koşullu ileticisi toohello şirket içi DNS sunucusu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="67de4-477">Add a conditional forwarder toohello on-premises DNS server.</span></span> <span data-ttu-id="67de4-478">Adım 1 toohello özel DNS sunucusundan hello DNS soneki için Hello koşullu ileticisi toosend istekleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="67de4-478">Configure hello conditional forwarder toosend requests for hello DNS suffix from step 1 toohello custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="67de4-479">DNS yazılımınızın nasıl özellikleri için Hello belgelerine tooadd koşullu ileticisi.</span><span class="sxs-lookup"><span data-stu-id="67de4-479">Consult hello documentation for your DNS software for specifics on how tooadd a conditional forwarder.</span></span>

<span data-ttu-id="67de4-480">Bu adımları tamamladıktan sonra tam etki alanı adları (FQDN) kullanarak ya da ağ tooresources bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="67de4-480">After completing these steps, you can connect tooresources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="67de4-481">Bu gibi durumlarda, Hdınsight şimdi hello sanal ağınıza yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67de4-481">You can now install HDInsight into hello virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="67de4-482">İki bağlı sanal ağlar arasındaki ad çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="67de4-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="67de4-483">Bu örnek varsayımlar aşağıdaki hello yapar:</span><span class="sxs-lookup"><span data-stu-id="67de4-483">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="67de4-484">İki Azure sanal veya eşliği ya da, bir VPN ağ geçidi kullanarak bağlanan ağ var.</span><span class="sxs-lookup"><span data-stu-id="67de4-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="67de4-485">Her iki ağ Hello özel DNS sunucusu, Linux veya UNIX hello işletim sistemi olarak çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="67de4-485">hello custom DNS server in both networks is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="67de4-486">[Bağlama](https://www.isc.org/downloads/bind/) hello özel DNS sunucularında yüklü.</span><span class="sxs-lookup"><span data-stu-id="67de4-486">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS servers.</span></span>

1. <span data-ttu-id="67de4-487">Her iki sanal ağlar Azure PowerShell veya Azure CLI toofind hello DNS sonekini kullanın:</span><span class="sxs-lookup"><span data-stu-id="67de4-487">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="67de4-488">Metin hello Merhaba içeriğine aşağıdaki kullanım hello `/etc/bind/named.config.local` hello özel DNS sunucusunda dosya.</span><span class="sxs-lookup"><span data-stu-id="67de4-488">Use hello following text as hello contents of hello `/etc/bind/named.config.local` file on hello custom DNS server.</span></span> <span data-ttu-id="67de4-489">Merhaba özel DNS sunucusunda hem de sanal ağlarda bu değişikliği yapın.</span><span class="sxs-lookup"><span data-stu-id="67de4-489">Make this change on hello custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    <span data-ttu-id="67de4-490">Hello yerine `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` hello hello DNS soneki değeri __diğer__ sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="67de4-490">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of hello __other__ virtual network.</span></span> <span data-ttu-id="67de4-491">Bu girdi hello uzak ağ toohello hello DNS soneki için istekleri yönlendirir özel ağındaki DNS, o.</span><span class="sxs-lookup"><span data-stu-id="67de4-491">This entry routes requests for hello DNS suffix of hello remote network toohello custom DNS in that network.</span></span>

3. <span data-ttu-id="67de4-492">Metin hello Merhaba içeriğine aşağıdaki hello Hello özel DNS sunucularında hem de sanal ağlarda kullanmak `/etc/bind/named.conf.options` dosyası:</span><span class="sxs-lookup"><span data-stu-id="67de4-492">On hello custom DNS servers in both virtual networks, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="67de4-493">Hello yerine `10.0.0.0/16` ve `10.1.0.0/16` değerleri ile başlangıç IP adresi aralıkları, sanal ağların.</span><span class="sxs-lookup"><span data-stu-id="67de4-493">Replace hello `10.0.0.0/16` and `10.1.0.0/16` values with hello IP address ranges of your virtual networks.</span></span> <span data-ttu-id="67de4-494">Bu girdi her ağ kaynaklarında hello DNS sunucularının toomake isteklere izin verir.</span><span class="sxs-lookup"><span data-stu-id="67de4-494">This entry allows resources in each network toomake requests of hello DNS servers.</span></span>

    <span data-ttu-id="67de4-495">Merhaba sanal ağların (örneğin, microsoft.com) DNS soneklerini hello olmayan tüm istekler hello Azure özyinelemeli çözümleyici tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="67de4-495">Any requests that are not for hello DNS suffixes of hello virtual networks (for example, microsoft.com) is handled by hello Azure recursive resolver.</span></span>

4. <span data-ttu-id="67de4-496">toouse hello yapılandırma, bağlama yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="67de4-496">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="67de4-497">Örneğin, `sudo service bind9 restart` hem DNS sunucularında.</span><span class="sxs-lookup"><span data-stu-id="67de4-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="67de4-498">Bu adımları tamamladıktan sonra tam etki alanı adları (FQDN) kullanarak hello sanal ağ içinde tooresources bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="67de4-498">After completing these steps, you can connect tooresources in hello virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="67de4-499">Bu gibi durumlarda, Hdınsight şimdi hello sanal ağınıza yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67de4-499">You can now install HDInsight into hello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67de4-500">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="67de4-500">Next steps</span></span>

* <span data-ttu-id="67de4-501">Hdınsight tooconnect tooan şirket içi ağ yapılandırma uçtan uca örneği için bkz: [bağlanmak Hdınsight tooan şirket içi ağ](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="67de4-501">For an end-to-end example of configuring HDInsight tooconnect tooan on-premises network, see [Connect HDInsight tooan on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="67de4-502">Azure sanal ağlar hakkında daha fazla bilgi için bkz: Merhaba [Azure Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67de4-502">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="67de4-503">Ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="67de4-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="67de4-504">Kullanıcı tanımlı yollar hakkında daha fazla bilgi için bkz: [kullanıcı tanımlı yollar ve IP iletimini](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="67de4-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>