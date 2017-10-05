---
title: "Hdınsight sanal ağ - Azure ile genişletmek | Microsoft Docs"
description: "Hdınsight diğer bulut kaynaklarına veya veri merkezinizdeki kaynaklarına bağlanmak için Azure sanal ağı kullanmayı öğrenin"
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
ms.openlocfilehash: 380423ec42ad4905c73fcd57501102e9f7062e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="3fc02-103">Bir Azure sanal ağı kullanarak Azure Hdınsight genişletme</span><span class="sxs-lookup"><span data-stu-id="3fc02-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="3fc02-104">Hdınsight ile kullanmayı öğrenin bir [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3fc02-104">Learn how to use HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="3fc02-105">Bir Azure sanal ağı kullanarak aşağıdaki senaryolar sağlar:</span><span class="sxs-lookup"><span data-stu-id="3fc02-105">Using an Azure Virtual Network enables the following scenarios:</span></span>

* <span data-ttu-id="3fc02-106">Hdınsight için doğrudan bir şirket içi ağ üzerinden bağlanılıyor.</span><span class="sxs-lookup"><span data-stu-id="3fc02-106">Connecting to HDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="3fc02-107">Hdınsight verilere bağlanma bir Azure sanal ağında depolar.</span><span class="sxs-lookup"><span data-stu-id="3fc02-107">Connecting HDInsight to data stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="3fc02-108">Doğrudan genel olarak internet üzerinden kullanılabilir değil Hadoop hizmetlerine erişme.</span><span class="sxs-lookup"><span data-stu-id="3fc02-108">Directly accessing Hadoop services that are not available publicly over the internet.</span></span> <span data-ttu-id="3fc02-109">Örneğin, Kafka API'leri veya HBase Java API.</span><span class="sxs-lookup"><span data-stu-id="3fc02-109">For example, Kafka APIs or the HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="3fc02-110">Bu belgedeki bilgiler TCP/IP ağı bilinmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-110">The information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="3fc02-111">TCP/IP ağ ile bilmiyorsanız, üretim ağları değişiklikler yapmadan önce olan bir kullanıcıyla ortak.</span><span class="sxs-lookup"><span data-stu-id="3fc02-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications to production networks.</span></span>

## <a name="planning"></a><span data-ttu-id="3fc02-112">Planlama</span><span class="sxs-lookup"><span data-stu-id="3fc02-112">Planning</span></span>

<span data-ttu-id="3fc02-113">Sanal bir ağa Hdınsight yüklemek planlama yaparken yanıt sorular şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3fc02-113">The following are the questions that you must answer when planning to install HDInsight in a virtual network:</span></span>

* <span data-ttu-id="3fc02-114">Mevcut bir sanal ağı Hdınsight yükleme gerekiyor mu?</span><span class="sxs-lookup"><span data-stu-id="3fc02-114">Do you need to install HDInsight into an existing virtual network?</span></span> <span data-ttu-id="3fc02-115">Veya yeni bir ağ oluşturmak?</span><span class="sxs-lookup"><span data-stu-id="3fc02-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="3fc02-116">Varolan bir sanal ağı kullanıyorsanız, Hdınsight yükleyebilmek için önce ağ yapılandırmasını değiştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-116">If you are using an existing virtual network, you may need to modify the network configuration before you can install HDInsight.</span></span> <span data-ttu-id="3fc02-117">Daha fazla bilgi için bkz: [Hdınsight mevcut bir sanal ağa eklemek](#existingvnet) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3fc02-117">For more information, see the [add HDInsight to an existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="3fc02-118">Başka bir sanal ağ veya şirket içi ağınız için Hdınsight içeren sanal ağa bağlanmak istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="3fc02-118">Do you want to connect the virtual network containing HDInsight to another virtual network or your on-premises network?</span></span>

    <span data-ttu-id="3fc02-119">Kolayca ağlarda kaynakları ile çalışmak için bir özel DNS oluşturma ve DNS iletmeyi yapılandırma gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-119">To easily work with resources across networks, you may need to create a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="3fc02-120">Daha fazla bilgi için bkz: [birden çok ağları bağlama](#multinet) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3fc02-120">For more information, see the [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="3fc02-121">Hdınsight gelen veya giden trafiği kısıtlama/yeniden yönlendirme etmek istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="3fc02-121">Do you want to restrict/redirect inbound or outbound traffic to HDInsight?</span></span>

    <span data-ttu-id="3fc02-122">Hdınsight Azure veri merkezindeki belirli IP adresleri ile iletişim sınırsız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-122">HDInsight must have unrestricted communication with specific IP addresses in the Azure data center.</span></span> <span data-ttu-id="3fc02-123">Güvenlik duvarları üzerinden istemci iletişimi için izin verilmelidir çeşitli bağlantı noktaları da vardır.</span><span class="sxs-lookup"><span data-stu-id="3fc02-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="3fc02-124">Daha fazla bilgi için bkz: [ağ trafiğini denetleme](#networktraffic) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3fc02-124">For more information, see the [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="3fc02-125"><a id="existingvnet"></a>Mevcut bir sanal ağa Hdınsight Ekle</span><span class="sxs-lookup"><span data-stu-id="3fc02-125"><a id="existingvnet"></a>Add HDInsight to an existing virtual network</span></span>

<span data-ttu-id="3fc02-126">Yeni Hdınsight var olan bir Azure sanal ağı eklemek nasıl keşfetmek için bu bölümdeki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-126">Use the steps in this section to discover how to add a new HDInsight to an existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="3fc02-127">Bir sanal ağ var olan bir Hdınsight kümesine eklenemiyor.</span><span class="sxs-lookup"><span data-stu-id="3fc02-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="3fc02-128">Sanal ağ için bir Klasik veya Resource Manager dağıtım modeli kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="3fc02-128">Are you using a classic or Resource Manager deployment model for the virtual network?</span></span>

    <span data-ttu-id="3fc02-129">Hdınsight 3.4 ve büyük bir Resource Manager sanal ağ gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="3fc02-130">Hdınsight'ın önceki sürümlerini Klasik sanal ağ gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="3fc02-131">Ardından, varolan ağınızda bir Klasik sanal ağı ise, Resource Manager sanal ağ oluşturma ve iki bağlantı gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect the two.</span></span> <span data-ttu-id="3fc02-132">[Klasik sanal ağlar için yeni sanal ağlara bağlanma](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3fc02-132">[Connecting classic VNets to new VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="3fc02-133">Birleştirilmiş sonra kaynak yöneticisi ağ yüklü Hdınsight Klasik ağ kaynakları ile etkileşim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-133">Once joined, HDInsight installed in the Resource Manager network can interact with resources in the classic network.</span></span>

2. <span data-ttu-id="3fc02-134">Zorlamalı tünel kullanıyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="3fc02-134">Do you use forced tunneling?</span></span> <span data-ttu-id="3fc02-135">Zorlamalı tünel, giden Internet trafiğini incelemesi için bir cihaz için zorlar bir alt ağ ayarı ve günlüğe kaydetme olur.</span><span class="sxs-lookup"><span data-stu-id="3fc02-135">Forced tunneling is a subnet setting that forces outbound Internet traffic to a device for inspection and logging.</span></span> <span data-ttu-id="3fc02-136">Hdınsight zorlamalı tünel desteklemez.</span><span class="sxs-lookup"><span data-stu-id="3fc02-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="3fc02-137">Bir alt ağ Hdınsight yüklemeden önce zorlamalı tünel kaldırmak veya Hdınsight için yeni bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3fc02-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="3fc02-138">İçine veya dışına sanal ağ trafiği kısıtlamak için ağ güvenlik grupları, kullanıcı tanımlı yollar ya da sanal ağ cihazları kullanıyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="3fc02-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances to restrict traffic into or out of the virtual network?</span></span>

    <span data-ttu-id="3fc02-139">Yönetilen bir hizmet olarak Hdınsight Azure veri merkezinde birden fazla IP adresi Kısıtlanmamış erişim gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-139">As a managed service, HDInsight requires unrestricted access to several IP addresses in the Azure data center.</span></span> <span data-ttu-id="3fc02-140">Bu IP adresleri ile iletişime izin verecek şekilde herhangi bir mevcut ağ güvenlik grupları veya kullanıcı tanımlı yollar güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3fc02-140">To allow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="3fc02-141">Hdınsight çeşitli bağlantı noktaları kullanan birden çok hizmetleri barındırır.</span><span class="sxs-lookup"><span data-stu-id="3fc02-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="3fc02-142">Bu bağlantı noktaları için trafiği engellemez.</span><span class="sxs-lookup"><span data-stu-id="3fc02-142">Do not block traffic to these ports.</span></span> <span data-ttu-id="3fc02-143">Sanal gereç güvenlik duvarlarından izin vermek için bağlantı noktalarının listesi için bkz [güvenlik](#security) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3fc02-143">For a list of ports to allow through virtual appliance firewalls, see the [Security](#security) section.</span></span>

    <span data-ttu-id="3fc02-144">Var olan güvenlik yapılandırmanızı bulmak için aşağıdaki Azure PowerShell veya Azure CLI komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="3fc02-144">To find your existing security configuration, use the following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="3fc02-145">Ağ güvenlik grupları</span><span class="sxs-lookup"><span data-stu-id="3fc02-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="3fc02-146">Daha fazla bilgi için bkz: [ağ güvenlik grupları sorun giderme](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) belge.</span><span class="sxs-lookup"><span data-stu-id="3fc02-146">For more information, see the [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="3fc02-147">Ağ güvenlik grubu kural kuralı önceliği temelinde sırayla uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3fc02-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="3fc02-148">Trafik desenle eşleşen ilk kural uygulanır ve hiçbir diğerlerinin bu trafiği için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3fc02-148">The first rule that matches the traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="3fc02-149">Sipariş kurallardan en fazla izne sahip az izin veren için.</span><span class="sxs-lookup"><span data-stu-id="3fc02-149">Order rules from most permissive to least permissive.</span></span> <span data-ttu-id="3fc02-150">Daha fazla bilgi için bkz: [filtre ağ güvenlik grupları ile ağ trafiği](../virtual-network/virtual-networks-nsg.md) belge.</span><span class="sxs-lookup"><span data-stu-id="3fc02-150">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="3fc02-151">Kullanıcı tanımlı yollar</span><span class="sxs-lookup"><span data-stu-id="3fc02-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="3fc02-152">Daha fazla bilgi için bkz: [sorun giderme yolları](../virtual-network/virtual-network-routes-troubleshoot-portal.md) belge.</span><span class="sxs-lookup"><span data-stu-id="3fc02-152">For more information, see the [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="3fc02-153">Hdınsight kümesi oluşturma ve yapılandırma sırasında Azure sanal ağı seçin.</span><span class="sxs-lookup"><span data-stu-id="3fc02-153">Create an HDInsight cluster and select the Azure Virtual Network during configuration.</span></span> <span data-ttu-id="3fc02-154">Küme oluşturma işlemi anlamak için aşağıdaki belgelerde adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="3fc02-154">Use the steps in the following documents to understand the cluster creation process:</span></span>

    * [<span data-ttu-id="3fc02-155">Azure portalını kullanarak HDInsight oluşturma</span><span class="sxs-lookup"><span data-stu-id="3fc02-155">Create HDInsight using the Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="3fc02-156">Azure PowerShell kullanarak HDInsight oluşturma</span><span class="sxs-lookup"><span data-stu-id="3fc02-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="3fc02-157">Azure CLI 1.0 kullanarak Hdınsight oluşturma</span><span class="sxs-lookup"><span data-stu-id="3fc02-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="3fc02-158">Bir Azure Resource Manager şablonu kullanarak Hdınsight oluşturma</span><span class="sxs-lookup"><span data-stu-id="3fc02-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="3fc02-159">Bir sanal ağa Hdınsight ekleyerek bir isteğe bağlı yapılandırma adımdır.</span><span class="sxs-lookup"><span data-stu-id="3fc02-159">Adding HDInsight to a virtual network is an optional configuration step.</span></span> <span data-ttu-id="3fc02-160">Küme yapılandırırken sanal ağı seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3fc02-160">Be sure to select the virtual network when configuring the cluster.</span></span>

## <span data-ttu-id="3fc02-161"><a id="multinet"></a>Birden çok ağları bağlama</span><span class="sxs-lookup"><span data-stu-id="3fc02-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="3fc02-162">Büyük çok ağ yapılandırması ile ağlar arasında ad çözümleme iştir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-162">The biggest challenge with a multi-network configuration is name resolution between the networks.</span></span>

<span data-ttu-id="3fc02-163">Azure ad çözümlemesi için sanal bir ağa yüklü olan Azure hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fc02-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="3fc02-164">Bu yerleşik ad çözümlemesi bir tam etki alanı adı (FQDN) kullanarak aşağıdaki kaynaklara bağlanmak Hdınsight sağlar:</span><span class="sxs-lookup"><span data-stu-id="3fc02-164">This built-in name resolution allows HDInsight to connect to the following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="3fc02-165">İnternet'te kullanılabilir herhangi bir kaynağa.</span><span class="sxs-lookup"><span data-stu-id="3fc02-165">Any resource that is available on the internet.</span></span> <span data-ttu-id="3fc02-166">Örneğin, microsoft.com, google.com.</span><span class="sxs-lookup"><span data-stu-id="3fc02-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="3fc02-167">Kullanarak aynı Azure sanal ağında, olan herhangi bir kaynağa __iç DNS ad__ kaynağının.</span><span class="sxs-lookup"><span data-stu-id="3fc02-167">Any resource that is in the same Azure Virtual Network, by using the __internal DNS name__ of the resource.</span></span> <span data-ttu-id="3fc02-168">Örneğin, varsayılan ad çözümlemesi kullanırken, Hdınsight çalışan düğümlerine atanan örnek iç DNS adları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3fc02-168">For example, when using the default name resolution, the following are example internal DNS names assigned to HDInsight worker nodes:</span></span>

    * <span data-ttu-id="3fc02-169">wn0 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="3fc02-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="3fc02-170">wn2 hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="3fc02-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="3fc02-171">Bu her iki düğüm iç DNS adları kullanarak birbirine ve diğer düğümlere, hdınsight'ta ile doğrudan iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="3fc02-172">Varsayılan ad çözümlemesi mu __değil__ ağlarda, sanal ağa katılan kaynakların adları çözümlemek Hdınsight izin verin.</span><span class="sxs-lookup"><span data-stu-id="3fc02-172">The default name resolution does __not__ allow HDInsight to resolve the names of resources in networks that are joined to the virtual network.</span></span> <span data-ttu-id="3fc02-173">Örneğin, sanal ağa şirket içi ağınıza katılmak için yaygındır.</span><span class="sxs-lookup"><span data-stu-id="3fc02-173">For example, it is common to join your on-premises network to the virtual network.</span></span> <span data-ttu-id="3fc02-174">Yalnızca varsayılan ad çözümlemesi ile Hdınsight, ada göre şirket içi ağ kaynaklarına erişemez.</span><span class="sxs-lookup"><span data-stu-id="3fc02-174">With only the default name resolution, HDInsight cannot access resources in the on-premises network by name.</span></span> <span data-ttu-id="3fc02-175">Şirket içi ağınızdaki kaynaklara ada göre sanal ağ kaynaklarına erişemez, bunun tersi de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-175">The opposite is also true, resources in your on-premises network cannot access resources in the virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="3fc02-176">Özel DNS sunucusu oluşturmak ve Hdınsight küme oluşturmadan önce kullanılacak sanal ağ yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-176">You must create the custom DNS server and configure the virtual network to use it before creating the HDInsight cluster.</span></span>

<span data-ttu-id="3fc02-177">Sanal ağ ve birleştirilmiş ağlarda bulunan kaynaklar arasındaki ad çözümlemesi etkinleştirmek için aşağıdaki eylemleri gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3fc02-177">To enable name resolution between the virtual network and resources in joined networks, you must perform the following actions:</span></span>

1. <span data-ttu-id="3fc02-178">Özel bir DNS sunucusu, Azure sanal Hdınsight yüklemeyi planladığınız Ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3fc02-178">Create a custom DNS server in the Azure Virtual Network where you plan to install HDInsight.</span></span>

2. <span data-ttu-id="3fc02-179">Sanal ağ özel DNS sunucusunu kullanacak şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-179">Configure the virtual network to use the custom DNS server.</span></span>

3. <span data-ttu-id="3fc02-180">Azure sanal ağınızın DNS soneki atanan bulun.</span><span class="sxs-lookup"><span data-stu-id="3fc02-180">Find the Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="3fc02-181">Bu değer benzer `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="3fc02-181">This value is similar to `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="3fc02-182">DNS son eki bulma hakkında daha fazla bilgi için bkz: [örnek: özel DNS](#example-dns) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3fc02-182">For information on finding the DNS suffix, see the [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="3fc02-183">DNS sunucuları arasında iletme yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-183">Configure forwarding between the DNS servers.</span></span> <span data-ttu-id="3fc02-184">Yapılandırma uzak ağ türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="3fc02-184">The configuration depends on the type of remote network.</span></span>

    * <span data-ttu-id="3fc02-185">Uzak ağ bir şirket içi ağ ise, DNS aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="3fc02-185">If the remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="3fc02-186">__Özel DNS__ (sanal ağındaki):</span><span class="sxs-lookup"><span data-stu-id="3fc02-186">__Custom DNS__ (in the virtual network):</span></span>

            * <span data-ttu-id="3fc02-187">Sanal ağın Azure özyinelemeli çözümleyici (168.63.129.16) için DNS soneki için istekleri ilet.</span><span class="sxs-lookup"><span data-stu-id="3fc02-187">Forward requests for the DNS suffix of the virtual network to the Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="3fc02-188">Azure sanal ağındaki kaynaklara yönelik isteklerin işleme</span><span class="sxs-lookup"><span data-stu-id="3fc02-188">Azure handles requests for resources in the virtual network</span></span>

            * <span data-ttu-id="3fc02-189">Şirket içi DNS sunucusuna tüm diğer isteklerden iletin.</span><span class="sxs-lookup"><span data-stu-id="3fc02-189">Forward all other requests to the on-premises DNS server.</span></span> <span data-ttu-id="3fc02-190">Şirket içi DNS bile istekleri Internet kaynakların Microsoft.com gibi diğer tüm ad çözümleme isteklerini işler.</span><span class="sxs-lookup"><span data-stu-id="3fc02-190">The on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="3fc02-191">__Şirket içi DNS__: iletmek sanal ağ DNS soneki özel DNS sunucusu için istek.</span><span class="sxs-lookup"><span data-stu-id="3fc02-191">__On-premises DNS__: Forward requests for the virtual network DNS suffix to the custom DNS server.</span></span> <span data-ttu-id="3fc02-192">Özel DNS sunucusu, daha sonra Azure özyinelemeli çözümleyici iletir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-192">The custom DNS server then forwards to the Azure recursive resolver.</span></span>

        <span data-ttu-id="3fc02-193">Bu yapılandırma yolları istekleri için sanal ağ özel DNS sunucusuna DNS sonekini içeren etki alanı adları tam.</span><span class="sxs-lookup"><span data-stu-id="3fc02-193">This configuration routes requests for fully qualified domain names that contain the DNS suffix of the virtual network to the custom DNS server.</span></span> <span data-ttu-id="3fc02-194">Tüm diğer isteklerden (hatta genel internet adresleri için) şirket içi DNS sunucusu tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-194">All other requests (even for public internet addresses) are handled by the on-premises DNS server.</span></span>

    * <span data-ttu-id="3fc02-195">Uzak ağ başka bir Azure sanal ağ ise, DNS aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="3fc02-195">If the remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="3fc02-196">__Özel DNS__ (her sanal ağındaki):</span><span class="sxs-lookup"><span data-stu-id="3fc02-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="3fc02-197">DNS soneki sanal ağlar için istekleri özel DNS sunucularına iletilir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-197">Requests for the DNS suffix of the virtual networks are forwarded to the custom DNS servers.</span></span> <span data-ttu-id="3fc02-198">Her sanal ağındaki DNS, alt ağ içindeki kaynakların çözümlemek için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="3fc02-198">The DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="3fc02-199">Tüm diğer isteklerden Azure özyinelemeli çözümleyici iletin.</span><span class="sxs-lookup"><span data-stu-id="3fc02-199">Forward all other requests to the Azure recursive resolver.</span></span> <span data-ttu-id="3fc02-200">Özyinelemeli çözümleyici yerel çözme ve Internet kaynakların sorumludur.</span><span class="sxs-lookup"><span data-stu-id="3fc02-200">The recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="3fc02-201">Her ağ diğerini isteklerini iletir için DNS sunucusu DNS son ekini temel alarak.</span><span class="sxs-lookup"><span data-stu-id="3fc02-201">The DNS server for each network forwards requests to the other, based on DNS suffix.</span></span> <span data-ttu-id="3fc02-202">Diğer istekleri Azure özyinelemeli çözümleyici kullanarak çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-202">Other requests are resolved using the Azure recursive resolver.</span></span>

    <span data-ttu-id="3fc02-203">Her yapılandırma örneği için bkz: [örnek: özel DNS](#example-dns) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3fc02-203">For an example of each configuration, see the [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="3fc02-204">Daha fazla bilgi için bkz: [VM'ler ve rol örnekleri için ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) belge.</span><span class="sxs-lookup"><span data-stu-id="3fc02-204">For more information, see the [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-to-hadoop-services"></a><span data-ttu-id="3fc02-205">Hadoop Services'e doğrudan bağlanmak</span><span class="sxs-lookup"><span data-stu-id="3fc02-205">Directly connect to Hadoop services</span></span>

<span data-ttu-id="3fc02-206">Hdınsight üzerinde çoğu belgeleri Internet üzerinden kümesine erişimi olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="3fc02-206">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="3fc02-207">Https://CLUSTERNAME.azurehdinsight.net konumundaki küme bağlanabileceği bir örnek için.</span><span class="sxs-lookup"><span data-stu-id="3fc02-207">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="3fc02-208">Bu adres Nsg'ler veya Udr'ler kullandıysanız internet'ten erişimi kısıtlamak için kullanılabilir olmayan ortak ağ geçidi, kullanır.</span><span class="sxs-lookup"><span data-stu-id="3fc02-208">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="3fc02-209">Ambari ve sanal ağ üzerinden diğer web sayfalarına bağlanmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="3fc02-209">To connect to Ambari and other web pages through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="3fc02-210">Hdınsight küme düğümlerinin iç tam etki alanı adları (FQDN) bulmak için aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="3fc02-210">To discover the internal fully qualified domain names (FQDN) of the HDInsight cluster nodes, use one of the following methods:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

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

    <span data-ttu-id="3fc02-211">Verilen düğüm listesi, baş düğümler için FQDN bulun ve Ambari ve diğer web hizmetlerine bağlanmak için FQDN'leri kullanın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-211">In the list of nodes returned, find the FQDN for the head nodes and use the FQDNs to connect to Ambari and other web services.</span></span> <span data-ttu-id="3fc02-212">Örneğin, `http://<headnode-fqdn>:8080` Ambari erişmek için.</span><span class="sxs-lookup"><span data-stu-id="3fc02-212">For example, use `http://<headnode-fqdn>:8080` to access Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3fc02-213">Baş düğümler üzerinde barındırılan bazı hizmetler aynı anda yalnızca bir düğümde etkin olur.</span><span class="sxs-lookup"><span data-stu-id="3fc02-213">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="3fc02-214">Bir hizmet bir baş düğüm üzerindeki erişmeyi deneyin ve bir 404 hatası döndürür, diğer baş düğüme geçiş yapar.</span><span class="sxs-lookup"><span data-stu-id="3fc02-214">If you try accessing a service on one head node and it returns a 404 error, switch to the other head node.</span></span>

2. <span data-ttu-id="3fc02-215">Düğüm ve bir hizmet kullanılabilir bağlantı noktasını belirlemek için bkz: [hdınsight'ta Hadoop Hizmetleri tarafından kullanılan bağlantı noktaları](./hdinsight-hadoop-port-settings-for-services.md) belge.</span><span class="sxs-lookup"><span data-stu-id="3fc02-215">To determine the node and port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="3fc02-216"><a id="networktraffic"></a>Ağ trafiğini denetleme</span><span class="sxs-lookup"><span data-stu-id="3fc02-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="3fc02-217">Bir Azure sanal ağlarda ağ trafiğini aşağıdaki yöntemler kullanılarak denetlenebilir:</span><span class="sxs-lookup"><span data-stu-id="3fc02-217">Network traffic in an Azure Virtual Networks can be controlled using the following methods:</span></span>

* <span data-ttu-id="3fc02-218">**Ağ güvenlik grupları** (NSG) ağa gelen ve giden trafiği filtrelemek olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fc02-218">**Network security groups** (NSG) allow you to filter inbound and outbound traffic to the network.</span></span> <span data-ttu-id="3fc02-219">Daha fazla bilgi için bkz: [filtre ağ güvenlik grupları ile ağ trafiği](../virtual-network/virtual-networks-nsg.md) belge.</span><span class="sxs-lookup"><span data-stu-id="3fc02-219">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="3fc02-220">Hdınsight giden trafiği kısıtlama desteklemez.</span><span class="sxs-lookup"><span data-stu-id="3fc02-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="3fc02-221">**Kullanıcı tanımlı yollar** (UDR) nasıl trafiği ağ kaynakları arasında akan tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-221">**User-defined routes** (UDR) define how traffic flows between resources in the network.</span></span> <span data-ttu-id="3fc02-222">Daha fazla bilgi için bkz: [kullanıcı tanımlı yollar ve IP iletimini](../virtual-network/virtual-networks-udr-overview.md) belge.</span><span class="sxs-lookup"><span data-stu-id="3fc02-222">For more information, see the [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="3fc02-223">**Ağ sanal Gereçleri** güvenlik duvarları ve yönlendiriciler gibi cihazların işlevselliğiyle Çoğalt.</span><span class="sxs-lookup"><span data-stu-id="3fc02-223">**Network virtual appliances** replicate the functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="3fc02-224">Daha fazla bilgi için bkz: [ağ uygulamaları](https://azure.microsoft.com/solutions/network-appliances) belge.</span><span class="sxs-lookup"><span data-stu-id="3fc02-224">For more information, see the [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="3fc02-225">Yönetilen bir hizmet olarak Hdınsight Azure bulutta Azure sistem durumu ve Yönetim hizmetlerine Kısıtlanmamış erişim gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-225">As a managed service, HDInsight requires unrestricted access to Azure health and management services in the Azure cloud.</span></span> <span data-ttu-id="3fc02-226">Nsg'ler ve Udr'ler kullanırken Hdınsight hizmetlerin hala Hdınsight ile iletişim kurabildiğinden emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="3fc02-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="3fc02-227">Hdınsight, çeşitli bağlantı noktaları üzerinde hizmetleri sunar.</span><span class="sxs-lookup"><span data-stu-id="3fc02-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="3fc02-228">Bir sanal gereç Güvenlik Duvarı'nı kullanırken, bu hizmetler için kullanılan bağlantı noktaları üzerinde trafiğe izin vermelidir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-228">When using a virtual appliance firewall, you must allow traffic on the ports used for these services.</span></span> <span data-ttu-id="3fc02-229">Daha fazla bilgi için [gerekli bağlantı noktalarını] bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-229">For more information, see the [Required ports] section.</span></span>

### <span data-ttu-id="3fc02-230"><a id="hdinsight-ip"></a>Hdınsight ile ağ güvenlik gruplarını ve kullanıcı tanımlı yollar</span><span class="sxs-lookup"><span data-stu-id="3fc02-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="3fc02-231">Kullanmayı planlıyorsanız, **ağ güvenlik grubu** veya **kullanıcı tanımlı yollar** ağ trafiğini denetlemek için Hdınsight'ı yüklemeden önce aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="3fc02-231">If you plan on using **network security groups** or **user-defined routes** to control network traffic, perform the following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="3fc02-232">Hdınsight için kullanmayı planladığınız Azure bölgesi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-232">Identify the Azure region that you plan to use for HDInsight.</span></span>

2. <span data-ttu-id="3fc02-233">Hdınsight tarafından gerekli IP adreslerini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="3fc02-233">Identify the IP addresses required by HDInsight.</span></span> <span data-ttu-id="3fc02-234">Daha fazla bilgi için bkz: [Hdınsight tarafından gerekli IP adreslerini](#hdinsight-ip) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3fc02-234">For more information, see the [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="3fc02-235">Oluşturun veya ağ güvenlik grupları veya kullanıcı tanımlı yollar Hdınsight'a yüklemeyi planladığınız alt ağ için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3fc02-235">Create or modify the network security groups or user-defined routes for the subnet that you plan to install HDInsight into.</span></span>

    * <span data-ttu-id="3fc02-236">__Ağ güvenlik grupları__: izin __gelen__ bağlantı noktasında trafik __443__ IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="3fc02-236">__Network security groups__: allow __inbound__ traffic on port __443__ from the IP addresses.</span></span>
    * <span data-ttu-id="3fc02-237">__Kullanıcı tanımlı yollar__: her IP adresi için bir yol oluşturun ve ayarlayın __sonraki atlama türü__ için __Internet__.</span><span class="sxs-lookup"><span data-stu-id="3fc02-237">__User-defined routes__: create a route to each IP address and set the __Next hop type__ to __Internet__.</span></span>

<span data-ttu-id="3fc02-238">Ağ güvenlik grupları veya kullanıcı tanımlı yollar hakkında daha fazla bilgi için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="3fc02-238">For more information on network security groups or user-defined routes, see the following documentation:</span></span>

* [<span data-ttu-id="3fc02-239">Ağ güvenlik grubu</span><span class="sxs-lookup"><span data-stu-id="3fc02-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="3fc02-240">Kullanıcı tanımlı yollar</span><span class="sxs-lookup"><span data-stu-id="3fc02-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="3fc02-241">Zorlamalı tünel oluşturma</span><span class="sxs-lookup"><span data-stu-id="3fc02-241">Forced tunneling</span></span>

<span data-ttu-id="3fc02-242">Zorlamalı tünel bir kullanıcı tanımlı yönlendirme burada bir alt ağdaki tüm trafiği belirli ağ veya şirket içi ağınız gibi konuma zorlanır yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="3fc02-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced to a specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="3fc02-243">Hdınsight mu __değil__ destek zorlamalı tünel.</span><span class="sxs-lookup"><span data-stu-id="3fc02-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="3fc02-244"><a id="hdinsight-ip"></a>Gerekli IP adresi</span><span class="sxs-lookup"><span data-stu-id="3fc02-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3fc02-245">Azure sistem durumu ve Yönetim Hizmetleri Hdınsight ile iletişim kurabilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-245">The Azure health and management services must be able to communicate with HDInsight.</span></span> <span data-ttu-id="3fc02-246">Ağ güvenlik grupları veya kullanıcı tanımlı yollar kullanıyorsanız, Hdınsight ulaşmak bu hizmetler için IP adreslerinden gelen trafiğe izin verecek.</span><span class="sxs-lookup"><span data-stu-id="3fc02-246">If you use network security groups or user-defined routes, allow traffic from the IP addresses for these services to reach HDInsight.</span></span>
>
> <span data-ttu-id="3fc02-247">Trafiği denetlemek için ağ güvenlik grupları veya kullanıcı tanımlı yollar kullanmıyorsanız, bu bölüm göz ardı edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fc02-247">If you do not use network security groups or user-defined routes to control traffic, you can ignore this section.</span></span>

<span data-ttu-id="3fc02-248">Ağ güvenlik grupları veya kullanıcı tanımlı yollar kullanıyorsanız, Hdınsight erişmek için Azure sistem durumu ve Yönetim hizmetlerinden trafiğe izin vermelidir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-248">If you use network security groups or user-defined routes, you must allow traffic from the Azure health and management services to reach HDInsight.</span></span> <span data-ttu-id="3fc02-249">İzin verilmiş olmalıdır IP adresleri bulmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="3fc02-249">Use the following steps to find the IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="3fc02-250">Her zaman aşağıdaki IP adreslerinden gelen trafiğe izin vermeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3fc02-250">You must always allow traffic from the following IP addresses:</span></span>

    | <span data-ttu-id="3fc02-251">IP adresi</span><span class="sxs-lookup"><span data-stu-id="3fc02-251">IP address</span></span> | <span data-ttu-id="3fc02-252">İzin verilen bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="3fc02-252">Allowed port</span></span> | <span data-ttu-id="3fc02-253">Yön</span><span class="sxs-lookup"><span data-stu-id="3fc02-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="3fc02-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="3fc02-254">168.61.49.99</span></span> | <span data-ttu-id="3fc02-255">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-255">443</span></span> | <span data-ttu-id="3fc02-256">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-256">Inbound</span></span> |
    | <span data-ttu-id="3fc02-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="3fc02-257">23.99.5.239</span></span> | <span data-ttu-id="3fc02-258">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-258">443</span></span> | <span data-ttu-id="3fc02-259">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-259">Inbound</span></span> |
    | <span data-ttu-id="3fc02-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="3fc02-260">168.61.48.131</span></span> | <span data-ttu-id="3fc02-261">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-261">443</span></span> | <span data-ttu-id="3fc02-262">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-262">Inbound</span></span> |
    | <span data-ttu-id="3fc02-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="3fc02-263">138.91.141.162</span></span> | <span data-ttu-id="3fc02-264">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-264">443</span></span> | <span data-ttu-id="3fc02-265">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-265">Inbound</span></span> |

2. <span data-ttu-id="3fc02-266">Hdınsight kümenizi aşağıdaki bölgeler birinde ise, bölge için listelenen IP adreslerinden gelen trafiğe izin vermelidir:</span><span class="sxs-lookup"><span data-stu-id="3fc02-266">If your HDInsight cluster is in one of the following regions, then you must allow traffic from the IP addresses listed for the region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3fc02-267">Kullanmakta olduğunuz Azure bölgesi listede yoksa, yalnızca 1. adım dört IP adreslerinden kullanın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-267">If the Azure region you are using is not listed, then only use the four IP addresses from step 1.</span></span>

    | <span data-ttu-id="3fc02-268">Ülke</span><span class="sxs-lookup"><span data-stu-id="3fc02-268">Country</span></span> | <span data-ttu-id="3fc02-269">Bölge</span><span class="sxs-lookup"><span data-stu-id="3fc02-269">Region</span></span> | <span data-ttu-id="3fc02-270">İzin verilen IP adresi</span><span class="sxs-lookup"><span data-stu-id="3fc02-270">Allowed IP addresses</span></span> | <span data-ttu-id="3fc02-271">İzin verilen bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="3fc02-271">Allowed port</span></span> | <span data-ttu-id="3fc02-272">Yön</span><span class="sxs-lookup"><span data-stu-id="3fc02-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="3fc02-273">Asya</span><span class="sxs-lookup"><span data-stu-id="3fc02-273">Asia</span></span> | <span data-ttu-id="3fc02-274">Doğu Asya</span><span class="sxs-lookup"><span data-stu-id="3fc02-274">East Asia</span></span> | <span data-ttu-id="3fc02-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="3fc02-275">23.102.235.122</span></span></br><span data-ttu-id="3fc02-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="3fc02-276">52.175.38.134</span></span> | <span data-ttu-id="3fc02-277">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-277">443</span></span> | <span data-ttu-id="3fc02-278">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="3fc02-279">Güneydoğu Asya</span><span class="sxs-lookup"><span data-stu-id="3fc02-279">Southeast Asia</span></span> | <span data-ttu-id="3fc02-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="3fc02-280">13.76.245.160</span></span></br><span data-ttu-id="3fc02-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="3fc02-281">13.76.136.249</span></span> | <span data-ttu-id="3fc02-282">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-282">443</span></span> | <span data-ttu-id="3fc02-283">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-283">Inbound</span></span> |
    | <span data-ttu-id="3fc02-284">Avustralya</span><span class="sxs-lookup"><span data-stu-id="3fc02-284">Australia</span></span> | <span data-ttu-id="3fc02-285">Avustralya Doğu</span><span class="sxs-lookup"><span data-stu-id="3fc02-285">Australia East</span></span> | <span data-ttu-id="3fc02-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="3fc02-286">104.210.84.115</span></span></br><span data-ttu-id="3fc02-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="3fc02-287">13.75.152.195</span></span> | <span data-ttu-id="3fc02-288">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-288">443</span></span> | <span data-ttu-id="3fc02-289">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="3fc02-290">Avustralya Güneydoğu</span><span class="sxs-lookup"><span data-stu-id="3fc02-290">Australia Southeast</span></span> | <span data-ttu-id="3fc02-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="3fc02-291">13.77.2.56</span></span></br><span data-ttu-id="3fc02-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="3fc02-292">13.77.2.94</span></span> | <span data-ttu-id="3fc02-293">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-293">443</span></span> | <span data-ttu-id="3fc02-294">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-294">Inbound</span></span> |
    | <span data-ttu-id="3fc02-295">Brezilya</span><span class="sxs-lookup"><span data-stu-id="3fc02-295">Brazil</span></span> | <span data-ttu-id="3fc02-296">Güney Brezilya</span><span class="sxs-lookup"><span data-stu-id="3fc02-296">Brazil South</span></span> | <span data-ttu-id="3fc02-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="3fc02-297">191.235.84.104</span></span></br><span data-ttu-id="3fc02-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="3fc02-298">191.235.87.113</span></span> | <span data-ttu-id="3fc02-299">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-299">443</span></span> | <span data-ttu-id="3fc02-300">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-300">Inbound</span></span> |
    | <span data-ttu-id="3fc02-301">Kanada</span><span class="sxs-lookup"><span data-stu-id="3fc02-301">Canada</span></span> | <span data-ttu-id="3fc02-302">Doğu Kanada</span><span class="sxs-lookup"><span data-stu-id="3fc02-302">Canada East</span></span> | <span data-ttu-id="3fc02-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="3fc02-303">52.229.127.96</span></span></br><span data-ttu-id="3fc02-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="3fc02-304">52.229.123.172</span></span> | <span data-ttu-id="3fc02-305">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-305">443</span></span> | <span data-ttu-id="3fc02-306">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="3fc02-307">Orta Kanada</span><span class="sxs-lookup"><span data-stu-id="3fc02-307">Canada Central</span></span> | <span data-ttu-id="3fc02-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="3fc02-308">52.228.37.66</span></span></br><span data-ttu-id="3fc02-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="3fc02-309">52.228.45.222</span></span> | <span data-ttu-id="3fc02-310">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-310">443</span></span> | <span data-ttu-id="3fc02-311">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-311">Inbound</span></span> |
    | <span data-ttu-id="3fc02-312">Çin</span><span class="sxs-lookup"><span data-stu-id="3fc02-312">China</span></span> | <span data-ttu-id="3fc02-313">Çin Kuzey</span><span class="sxs-lookup"><span data-stu-id="3fc02-313">China North</span></span> | <span data-ttu-id="3fc02-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="3fc02-314">42.159.96.170</span></span></br><span data-ttu-id="3fc02-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="3fc02-315">139.217.2.219</span></span> | <span data-ttu-id="3fc02-316">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-316">443</span></span> | <span data-ttu-id="3fc02-317">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="3fc02-318">Çin Doğu</span><span class="sxs-lookup"><span data-stu-id="3fc02-318">China East</span></span> | <span data-ttu-id="3fc02-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="3fc02-319">42.159.198.178</span></span></br><span data-ttu-id="3fc02-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="3fc02-320">42.159.234.157</span></span> | <span data-ttu-id="3fc02-321">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-321">443</span></span> | <span data-ttu-id="3fc02-322">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-322">Inbound</span></span> |
    | <span data-ttu-id="3fc02-323">Avrupa</span><span class="sxs-lookup"><span data-stu-id="3fc02-323">Europe</span></span> | <span data-ttu-id="3fc02-324">Kuzey Avrupa</span><span class="sxs-lookup"><span data-stu-id="3fc02-324">North Europe</span></span> | <span data-ttu-id="3fc02-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="3fc02-325">52.164.210.96</span></span></br><span data-ttu-id="3fc02-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="3fc02-326">13.74.153.132</span></span> | <span data-ttu-id="3fc02-327">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-327">443</span></span> | <span data-ttu-id="3fc02-328">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="3fc02-329">Batı Avrupa</span><span class="sxs-lookup"><span data-stu-id="3fc02-329">West Europe</span></span>| <span data-ttu-id="3fc02-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="3fc02-330">52.166.243.90</span></span></br><span data-ttu-id="3fc02-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="3fc02-331">52.174.36.244</span></span> | <span data-ttu-id="3fc02-332">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-332">443</span></span> | <span data-ttu-id="3fc02-333">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-333">Inbound</span></span> |
    | <span data-ttu-id="3fc02-334">Almanya</span><span class="sxs-lookup"><span data-stu-id="3fc02-334">Germany</span></span> | <span data-ttu-id="3fc02-335">Almanya Orta</span><span class="sxs-lookup"><span data-stu-id="3fc02-335">Germany Central</span></span> | <span data-ttu-id="3fc02-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="3fc02-336">51.4.146.68</span></span></br><span data-ttu-id="3fc02-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="3fc02-337">51.4.146.80</span></span> | <span data-ttu-id="3fc02-338">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-338">443</span></span> | <span data-ttu-id="3fc02-339">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="3fc02-340">Almanya Kuzeydoğu</span><span class="sxs-lookup"><span data-stu-id="3fc02-340">Germany Northeast</span></span> | <span data-ttu-id="3fc02-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="3fc02-341">51.5.150.132</span></span></br><span data-ttu-id="3fc02-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="3fc02-342">51.5.144.101</span></span> | <span data-ttu-id="3fc02-343">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-343">443</span></span> | <span data-ttu-id="3fc02-344">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-344">Inbound</span></span> |
    | <span data-ttu-id="3fc02-345">Hindistan</span><span class="sxs-lookup"><span data-stu-id="3fc02-345">India</span></span> | <span data-ttu-id="3fc02-346">Orta Hindistan</span><span class="sxs-lookup"><span data-stu-id="3fc02-346">Central India</span></span> | <span data-ttu-id="3fc02-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="3fc02-347">52.172.153.209</span></span></br><span data-ttu-id="3fc02-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="3fc02-348">52.172.152.49</span></span> | <span data-ttu-id="3fc02-349">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-349">443</span></span> | <span data-ttu-id="3fc02-350">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-350">Inbound</span></span> |
    | <span data-ttu-id="3fc02-351">Japonya</span><span class="sxs-lookup"><span data-stu-id="3fc02-351">Japan</span></span> | <span data-ttu-id="3fc02-352">Japonya Doğu</span><span class="sxs-lookup"><span data-stu-id="3fc02-352">Japan East</span></span> | <span data-ttu-id="3fc02-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="3fc02-353">13.78.125.90</span></span></br><span data-ttu-id="3fc02-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="3fc02-354">13.78.89.60</span></span> | <span data-ttu-id="3fc02-355">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-355">443</span></span> | <span data-ttu-id="3fc02-356">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="3fc02-357">Japonya Batı</span><span class="sxs-lookup"><span data-stu-id="3fc02-357">Japan West</span></span> | <span data-ttu-id="3fc02-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="3fc02-358">40.74.125.69</span></span></br><span data-ttu-id="3fc02-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="3fc02-359">138.91.29.150</span></span> | <span data-ttu-id="3fc02-360">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-360">443</span></span> | <span data-ttu-id="3fc02-361">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-361">Inbound</span></span> |
    | <span data-ttu-id="3fc02-362">Kore</span><span class="sxs-lookup"><span data-stu-id="3fc02-362">Korea</span></span> | <span data-ttu-id="3fc02-363">Kore Orta</span><span class="sxs-lookup"><span data-stu-id="3fc02-363">Korea Central</span></span> | <span data-ttu-id="3fc02-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="3fc02-364">52.231.39.142</span></span></br><span data-ttu-id="3fc02-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="3fc02-365">52.231.36.209</span></span> | <span data-ttu-id="3fc02-366">433</span><span class="sxs-lookup"><span data-stu-id="3fc02-366">433</span></span> | <span data-ttu-id="3fc02-367">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="3fc02-368">Kore Güney</span><span class="sxs-lookup"><span data-stu-id="3fc02-368">Korea South</span></span> | <span data-ttu-id="3fc02-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="3fc02-369">52.231.203.16</span></span></br><span data-ttu-id="3fc02-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="3fc02-370">52.231.205.214</span></span> | <span data-ttu-id="3fc02-371">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-371">443</span></span> | <span data-ttu-id="3fc02-372">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-372">Inbound</span></span>
    | <span data-ttu-id="3fc02-373">Birleşik Krallık</span><span class="sxs-lookup"><span data-stu-id="3fc02-373">United Kingdom</span></span> | <span data-ttu-id="3fc02-374">Birleşik Krallık Batı</span><span class="sxs-lookup"><span data-stu-id="3fc02-374">UK West</span></span> | <span data-ttu-id="3fc02-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="3fc02-375">51.141.13.110</span></span></br><span data-ttu-id="3fc02-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="3fc02-376">51.141.7.20</span></span> | <span data-ttu-id="3fc02-377">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-377">443</span></span> | <span data-ttu-id="3fc02-378">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="3fc02-379">Birleşik Krallık Güney</span><span class="sxs-lookup"><span data-stu-id="3fc02-379">UK South</span></span> | <span data-ttu-id="3fc02-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="3fc02-380">51.140.47.39</span></span></br><span data-ttu-id="3fc02-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="3fc02-381">51.140.52.16</span></span> | <span data-ttu-id="3fc02-382">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-382">443</span></span> | <span data-ttu-id="3fc02-383">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-383">Inbound</span></span> |
    | <span data-ttu-id="3fc02-384">Amerika Birleşik Devletleri</span><span class="sxs-lookup"><span data-stu-id="3fc02-384">United States</span></span> | <span data-ttu-id="3fc02-385">Orta ABD</span><span class="sxs-lookup"><span data-stu-id="3fc02-385">Central US</span></span> | <span data-ttu-id="3fc02-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="3fc02-386">13.67.223.215</span></span></br><span data-ttu-id="3fc02-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="3fc02-387">40.86.83.253</span></span> | <span data-ttu-id="3fc02-388">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-388">443</span></span> | <span data-ttu-id="3fc02-389">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="3fc02-390">Orta Kuzey ABD</span><span class="sxs-lookup"><span data-stu-id="3fc02-390">North Central US</span></span> | <span data-ttu-id="3fc02-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="3fc02-391">157.56.8.38</span></span></br><span data-ttu-id="3fc02-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="3fc02-392">157.55.213.99</span></span> | <span data-ttu-id="3fc02-393">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-393">443</span></span> | <span data-ttu-id="3fc02-394">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="3fc02-395">Batı Orta ABD</span><span class="sxs-lookup"><span data-stu-id="3fc02-395">West Central US</span></span> | <span data-ttu-id="3fc02-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="3fc02-396">52.161.23.15</span></span></br><span data-ttu-id="3fc02-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="3fc02-397">52.161.10.167</span></span> | <span data-ttu-id="3fc02-398">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-398">443</span></span> | <span data-ttu-id="3fc02-399">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="3fc02-400">Batı ABD 2</span><span class="sxs-lookup"><span data-stu-id="3fc02-400">West US 2</span></span> | <span data-ttu-id="3fc02-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="3fc02-401">52.175.211.210</span></span></br><span data-ttu-id="3fc02-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="3fc02-402">52.175.222.222</span></span> | <span data-ttu-id="3fc02-403">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-403">443</span></span> | <span data-ttu-id="3fc02-404">Gelen</span><span class="sxs-lookup"><span data-stu-id="3fc02-404">Inbound</span></span> |

    <span data-ttu-id="3fc02-405">Azure kamu için kullanılacak IP adresleri hakkında daha fazla bilgi için bkz: [Azure Kamu Intelligence + analiz](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) belge.</span><span class="sxs-lookup"><span data-stu-id="3fc02-405">For information on the IP addresses to use for Azure Government, see the [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="3fc02-406">Sanal ağınız ile özel bir DNS sunucusu kullanıyorsanız, erişimden de izin vermeniz gerekir __168.63.129.16__.</span><span class="sxs-lookup"><span data-stu-id="3fc02-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="3fc02-407">Azure'nın özyinelemeli çözümleyici adresidir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="3fc02-408">Daha fazla bilgi için bkz: [VM'ler ve rol için ad çözümlemesi örnekleri](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) belge.</span><span class="sxs-lookup"><span data-stu-id="3fc02-408">For more information, see the [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="3fc02-409">Daha fazla bilgi için bkz: [ağ trafiğini denetleme](#networktraffic) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3fc02-409">For more information, see the [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="3fc02-410"><a id="hdinsight-ports"></a>Gerekli bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="3fc02-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="3fc02-411">Bir ağı kullanmayı planlıyorsanız, **sanal gereç Güvenlik Duvarı** sanal ağ güvenliğini sağlamak için aşağıdaki bağlantı noktaları üzerinde giden trafiğe izin vermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="3fc02-411">If you plan on using a network **virtual appliance firewall** to secure the virtual network, you must allow outbound traffic on the following ports:</span></span>

* <span data-ttu-id="3fc02-412">53</span><span class="sxs-lookup"><span data-stu-id="3fc02-412">53</span></span>
* <span data-ttu-id="3fc02-413">443</span><span class="sxs-lookup"><span data-stu-id="3fc02-413">443</span></span>
* <span data-ttu-id="3fc02-414">1433</span><span class="sxs-lookup"><span data-stu-id="3fc02-414">1433</span></span>
* <span data-ttu-id="3fc02-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="3fc02-415">11000-11999</span></span>
* <span data-ttu-id="3fc02-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="3fc02-416">14000-14999</span></span>

<span data-ttu-id="3fc02-417">Belirli hizmetleri için bağlantı noktalarını bir listesi için bkz: [hdınsight'ta Hadoop Hizmetleri tarafından kullanılan bağlantı noktaları](hdinsight-hadoop-port-settings-for-services.md) belge.</span><span class="sxs-lookup"><span data-stu-id="3fc02-417">For a list of ports for specific services, see the [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="3fc02-418">Sanal gereçler için güvenlik duvarı kuralları hakkında daha fazla bilgi için bkz: [sanal gereç senaryo](../virtual-network/virtual-network-scenario-udr-gw-nva.md) belge.</span><span class="sxs-lookup"><span data-stu-id="3fc02-418">For more information on firewall rules for virtual appliances, see the [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="3fc02-419"><a id="hdinsight-nsg"></a>Örnek: ağ güvenlik grupları Hdınsight ile</span><span class="sxs-lookup"><span data-stu-id="3fc02-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="3fc02-420">Bu bölümdeki örnekleri ağ güvenliği Hdınsight Azure Yönetim Hizmetleri ile iletişim kurmasına izin ver Grup kuralları oluşturmak nasıl ekleyebileceğiniz gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-420">The examples in this section demonstrate how to create network security group rules that allow HDInsight to communicate with the Azure management services.</span></span> <span data-ttu-id="3fc02-421">Örnekler kullanmadan önce kullanmakta olduğunuz Azure bölgesinin olanlarla eşleşmesi için IP adreslerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-421">Before using the examples, adjust the IP addresses to match the ones for the Azure region you are using.</span></span> <span data-ttu-id="3fc02-422">Bu bilgiler bulabilirsiniz [Hdınsight ağ güvenlik gruplarını ve kullanıcı tanımlı yollar ile](#hdinsight-ip) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3fc02-422">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="3fc02-423">Azure kaynak yönetimi şablonu</span><span class="sxs-lookup"><span data-stu-id="3fc02-423">Azure Resource Management template</span></span>

<span data-ttu-id="3fc02-424">Aşağıdaki kaynak yönetimi şablon gelen trafiği sınırlar, ancak Hdınsight tarafından gerekli IP adreslerinden gelen trafiğe izin veren bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3fc02-424">The following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span> <span data-ttu-id="3fc02-425">Bu şablon, ayrıca bir Hdınsight kümesi sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3fc02-425">This template also creates an HDInsight cluster in the virtual network.</span></span>

* [<span data-ttu-id="3fc02-426">Güvenli bir Azure sanal ağ ve bir Hdınsight Hadoop kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="3fc02-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="3fc02-427">Bu örnekte, kullanmakta olduğunuz Azure bölgesi eşleştirmek için kullanılan IP adreslerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3fc02-427">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="3fc02-428">Bu bilgiler bulabilirsiniz [Hdınsight ağ güvenlik gruplarını ve kullanıcı tanımlı yollar ile](#hdinsight-ip) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3fc02-428">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="3fc02-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3fc02-429">Azure PowerShell</span></span>

<span data-ttu-id="3fc02-430">Gelen trafik kısıtlar ve Kuzey Avrupa bölgesinin IP adreslerinden gelen trafiğe izin veren bir sanal ağ oluşturmak için aşağıdaki PowerShell betiğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-430">Use the following PowerShell script to create a virtual network that restricts inbound traffic and allows traffic from the IP addresses for the North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3fc02-431">Bu örnekte, kullanmakta olduğunuz Azure bölgesi eşleştirmek için kullanılan IP adreslerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3fc02-431">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="3fc02-432">Bu bilgiler bulabilirsiniz [Hdınsight ağ güvenlik gruplarını ve kullanıcı tanımlı yollar ile](#hdinsight-ip) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3fc02-432">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with the resource group the virtual network is in"
$subnetName = "Replace with the name of the subnet that you plan to use for HDInsight"
# Get the Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get the region the Virtual network is in.
$location = $vnet.Location
# Get the subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for the HDInsight health and management services.
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
# Set the changes to the security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply the NSG to the subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="3fc02-433">Bu örnek gerekli IP adreslerini gelen trafiğe izin verme kuralları ekleneceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-433">This example demonstrates how to add rules to allow inbound traffic on the required IP addresses.</span></span> <span data-ttu-id="3fc02-434">Diğer kaynaklardan gelen erişimi kısıtlamak için bir kural içermiyor.</span><span class="sxs-lookup"><span data-stu-id="3fc02-434">It does not contain a rule to restrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="3fc02-435">Aşağıdaki örnek, Internet'ten SSH erişimini etkinleştirmek gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3fc02-435">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="3fc02-436">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3fc02-436">Azure CLI</span></span>

<span data-ttu-id="3fc02-437">Gelen trafik sınırlar, ancak Hdınsight tarafından gerekli IP adreslerinden gelen trafiğe izin veren bir sanal ağ oluşturmak için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-437">Use the following steps to create a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="3fc02-438">Adlı yeni bir ağ güvenlik grubu oluşturmak için aşağıdaki komutu kullanın `hdisecure`.</span><span class="sxs-lookup"><span data-stu-id="3fc02-438">Use the following command to create a new network security group named `hdisecure`.</span></span> <span data-ttu-id="3fc02-439">Değiştir **RESOURCEGROUPNAME** Azure sanal ağı içeren kaynak grubunu ile.</span><span class="sxs-lookup"><span data-stu-id="3fc02-439">Replace **RESOURCEGROUPNAME** with the resource group that contains the Azure Virtual Network.</span></span> <span data-ttu-id="3fc02-440">Değiştir **konumu** grubunun oluşturulduğu konum (bölge).</span><span class="sxs-lookup"><span data-stu-id="3fc02-440">Replace **LOCATION** with the location (region) that the group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="3fc02-441">Grup oluşturulduktan sonra yeni grubu hakkında bilgi alabilir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-441">Once the group has been created, you receive information on the new group.</span></span>

2. <span data-ttu-id="3fc02-442">Bağlantı noktası 443 üzerinden Azure Hdınsight sistem durumu ve yönetim hizmetinden gelen iletişime izin verecek yeni bir ağ güvenlik grubu kural eklemek için aşağıdakileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-442">Use the following to add rules to the new network security group that allow inbound communication on port 443 from the Azure HDInsight health and management service.</span></span> <span data-ttu-id="3fc02-443">Değiştir **RESOURCEGROUPNAME** Azure sanal ağı içeren kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="3fc02-443">Replace **RESOURCEGROUPNAME** with the name of the resource group that contains the Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="3fc02-444">Bu örnekte, kullanmakta olduğunuz Azure bölgesi eşleştirmek için kullanılan IP adreslerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="3fc02-444">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="3fc02-445">Bu bilgiler bulabilirsiniz [Hdınsight ağ güvenlik gruplarını ve kullanıcı tanımlı yollar ile](#hdinsight-ip) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3fc02-445">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="3fc02-446">Bu ağ güvenlik grubu için benzersiz tanımlayıcı almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="3fc02-446">To retrieve the unique identifier for this network security group, use the following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="3fc02-447">Bu komutu aşağıdaki metni benzer bir değer döndürür:</span><span class="sxs-lookup"><span data-stu-id="3fc02-447">This command returns a value similar to the following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="3fc02-448">Beklenen sonuç alamazsanız kimliği etrafında çift tırnak komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-448">Use double-quotes around id in the command if you don't get the expected results.</span></span>

4. <span data-ttu-id="3fc02-449">Bir alt ağ için ağ güvenlik grubu uygulamak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-449">Use the following command to apply the network security group to a subnet.</span></span> <span data-ttu-id="3fc02-450">Değiştir __GUID__ ve __RESOURCEGROUPNAME__ olanları değerlerle önceki adımda döndürülen.</span><span class="sxs-lookup"><span data-stu-id="3fc02-450">Replace the __GUID__ and __RESOURCEGROUPNAME__ values with the ones returned from the previous step.</span></span> <span data-ttu-id="3fc02-451">Değiştir __vnetname ADLI__ ve __SUBNETNAME__ oluşturmak istediğiniz alt ağ adı ve sanal ağ adı.</span><span class="sxs-lookup"><span data-stu-id="3fc02-451">Replace __VNETNAME__ and __SUBNETNAME__ with the virtual network name and subnet name that you want to create.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="3fc02-452">Bu komut tamamlandıktan sonra sanal ağa Hdınsight yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fc02-452">Once this command completes, you can install HDInsight into the Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3fc02-453">Bu adımları yalnızca Azure Bulutu üzerinde Hdınsight sistem durumu ve yönetim hizmetine erişim açın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-453">These steps only open access to the HDInsight health and management service on the Azure cloud.</span></span> <span data-ttu-id="3fc02-454">Hdınsight küme sanal ağ dışındaki diğer tüm erişimi engellenir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-454">Any other access to the HDInsight cluster from outside the Virtual Network is blocked.</span></span> <span data-ttu-id="3fc02-455">Sanal Ağ dışından erişim etkinleştirmek için ek ağ güvenlik grubu kuralları eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-455">To enable access from outside the virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="3fc02-456">Aşağıdaki örnek, Internet'ten SSH erişimini etkinleştirmek gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3fc02-456">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="3fc02-457"><a id="example-dns"></a>Örnek: DNS yapılandırması</span><span class="sxs-lookup"><span data-stu-id="3fc02-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="3fc02-458">Sanal bir ağa bağlı şirket içi ağ arasındaki ad çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="3fc02-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="3fc02-459">Bu örnekte aşağıdaki varsayımlar yapar:</span><span class="sxs-lookup"><span data-stu-id="3fc02-459">This example makes the following assumptions:</span></span>

* <span data-ttu-id="3fc02-460">Bir Azure sanal bir VPN ağ geçidi kullanarak bir şirket ağına bağlı ağ var.</span><span class="sxs-lookup"><span data-stu-id="3fc02-460">You have an Azure Virtual Network that is connected to an on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="3fc02-461">Özel sanal ağın DNS sunucusu, Linux veya UNIX işletim sistemi olarak çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="3fc02-461">The custom DNS server in the virtual network is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="3fc02-462">[Bağlama](https://www.isc.org/downloads/bind/) özel DNS sunucusuna yüklenir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-462">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS server.</span></span>

<span data-ttu-id="3fc02-463">Özel DNS sunucusunda sanal ağda:</span><span class="sxs-lookup"><span data-stu-id="3fc02-463">On the custom DNS server in the virtual network:</span></span>

1. <span data-ttu-id="3fc02-464">Sanal ağın DNS soneki bulmak için Azure PowerShell veya Azure CLI kullanın:</span><span class="sxs-lookup"><span data-stu-id="3fc02-464">Use either Azure PowerShell or Azure CLI to find the DNS suffix of the virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="3fc02-465">Sanal ağ için özel DNS sunucusunda aşağıdaki metni içeriğini kullanmak `/etc/bind/named.conf.local` dosyası:</span><span class="sxs-lookup"><span data-stu-id="3fc02-465">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="3fc02-466">Değiştir `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` sanal ağınızın DNS soneki ile değer.</span><span class="sxs-lookup"><span data-stu-id="3fc02-466">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="3fc02-467">Bu yapılandırma sanal ağın DNS soneki için tüm DNS isteklerine Azure özyinelemeli çözümleyici yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-467">This configuration routes all DNS requests for the DNS suffix of the virtual network to the Azure recursive resolver.</span></span>

2. <span data-ttu-id="3fc02-468">Sanal ağ için özel DNS sunucusunda aşağıdaki metni içeriğini kullanmak `/etc/bind/named.conf.options` dosyası:</span><span class="sxs-lookup"><span data-stu-id="3fc02-468">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    // TODO: Add the IP range of the joined network to this list
    acl goodclients {
        10.0.0.0/16; # IP address range of the virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent to the following
            forwarders {
                192.168.0.1; # Replace with the IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="3fc02-469">Değiştir `10.0.0.0/16` sanal ağınızdaki IP adres aralığı ile değer.</span><span class="sxs-lookup"><span data-stu-id="3fc02-469">Replace the `10.0.0.0/16` value with the IP address range of your virtual network.</span></span> <span data-ttu-id="3fc02-470">Bu giriş, ad çözümleme istekleri adreslerini bu aralıkta sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fc02-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="3fc02-471">Şirket içi ağ için IP adres aralığı Ekle `acl goodclients { ... }` bölümü.</span><span class="sxs-lookup"><span data-stu-id="3fc02-471">Add the IP address range of the on-premises network to the `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="3fc02-472">Giriş ad çözümleme isteklerinin kaynaklardan şirket içi ağ sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fc02-472">entry allows name resolution requests from resources in the on-premises network.</span></span>
    
    * <span data-ttu-id="3fc02-473">Değeri değiştirme `192.168.0.1` şirket içi DNS sunucunuzun IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="3fc02-473">Replace the value `192.168.0.1` with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="3fc02-474">Bu giriş diğer tüm DNS isteklerine şirket DNS sunucusuna yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-474">This entry routes all other DNS requests to the on-premises DNS server.</span></span>

3. <span data-ttu-id="3fc02-475">Yapılandırmayı kullanmak için bağlama yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-475">To use the configuration, restart Bind.</span></span> <span data-ttu-id="3fc02-476">Örneğin, `sudo service bind9 restart`.</span><span class="sxs-lookup"><span data-stu-id="3fc02-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="3fc02-477">Koşullu ileticisi şirket DNS sunucusuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3fc02-477">Add a conditional forwarder to the on-premises DNS server.</span></span> <span data-ttu-id="3fc02-478">Adım 1'den özel DNS sunucusuna DNS soneki için istekleri göndermesine koşullu ileticisi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-478">Configure the conditional forwarder to send requests for the DNS suffix from step 1 to the custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3fc02-479">Koşullu ileticisi ekleme özellikleri için DNS yazılımınızın belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-479">Consult the documentation for your DNS software for specifics on how to add a conditional forwarder.</span></span>

<span data-ttu-id="3fc02-480">Bu adımları tamamladıktan sonra tam etki alanı adları (FQDN) kullanarak ya da ağdaki kaynaklara bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-480">After completing these steps, you can connect to resources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="3fc02-481">Bu gibi durumlarda, Hdınsight artık sanal ağınıza yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fc02-481">You can now install HDInsight into the virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="3fc02-482">İki bağlı sanal ağlar arasındaki ad çözümlemesi</span><span class="sxs-lookup"><span data-stu-id="3fc02-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="3fc02-483">Bu örnekte aşağıdaki varsayımlar yapar:</span><span class="sxs-lookup"><span data-stu-id="3fc02-483">This example makes the following assumptions:</span></span>

* <span data-ttu-id="3fc02-484">İki Azure sanal veya eşliği ya da, bir VPN ağ geçidi kullanarak bağlanan ağ var.</span><span class="sxs-lookup"><span data-stu-id="3fc02-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="3fc02-485">Her iki ağlarda özel DNS sunucusu, Linux veya UNIX işletim sistemi olarak çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="3fc02-485">The custom DNS server in both networks is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="3fc02-486">[Bağlama](https://www.isc.org/downloads/bind/) özel DNS sunucularında yüklü.</span><span class="sxs-lookup"><span data-stu-id="3fc02-486">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS servers.</span></span>

1. <span data-ttu-id="3fc02-487">Her iki sanal ağ DNS sonekini bulmak için Azure PowerShell veya Azure CLI kullanın:</span><span class="sxs-lookup"><span data-stu-id="3fc02-487">Use either Azure PowerShell or Azure CLI to find the DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="3fc02-488">Aşağıdaki metni içeriğini kullanmak `/etc/bind/named.config.local` özel DNS sunucusunda dosya.</span><span class="sxs-lookup"><span data-stu-id="3fc02-488">Use the following text as the contents of the `/etc/bind/named.config.local` file on the custom DNS server.</span></span> <span data-ttu-id="3fc02-489">Özel DNS sunucusunda hem de sanal ağlarda bu değişikliği yapın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-489">Make this change on the custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The IP address of the DNS server in the other virtual network
    };
    ```

    <span data-ttu-id="3fc02-490">Değiştir `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` DNS soneki değeri __diğer__ sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="3fc02-490">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of the __other__ virtual network.</span></span> <span data-ttu-id="3fc02-491">Bu giriş özel DNS, ağ istekleri uzak ağın DNS soneki için yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-491">This entry routes requests for the DNS suffix of the remote network to the custom DNS in that network.</span></span>

3. <span data-ttu-id="3fc02-492">Her iki sanal ağlarda özel DNS sunucularında aşağıdaki metni içeriğini kullanın `/etc/bind/named.conf.options` dosyası:</span><span class="sxs-lookup"><span data-stu-id="3fc02-492">On the custom DNS servers in both virtual networks, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    acl goodclients {
        10.1.0.0/16; # The IP address range of one virtual network
        10.0.0.0/16; # The IP address range of the other virtual network
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

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="3fc02-493">Değiştir `10.0.0.0/16` ve `10.1.0.0/16` değerleri ile IP adresi aralıkları, sanal ağların.</span><span class="sxs-lookup"><span data-stu-id="3fc02-493">Replace the `10.0.0.0/16` and `10.1.0.0/16` values with the IP address ranges of your virtual networks.</span></span> <span data-ttu-id="3fc02-494">Bu girdi kaynakları her ağın DNS sunucularını istekler yapmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="3fc02-494">This entry allows resources in each network to make requests of the DNS servers.</span></span>

    <span data-ttu-id="3fc02-495">Sanal ağlar (örneğin, microsoft.com) DNS sonekleri için değil tüm istekleri Azure özyinelemeli çözümleyici tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-495">Any requests that are not for the DNS suffixes of the virtual networks (for example, microsoft.com) is handled by the Azure recursive resolver.</span></span>

4. <span data-ttu-id="3fc02-496">Yapılandırmayı kullanmak için bağlama yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="3fc02-496">To use the configuration, restart Bind.</span></span> <span data-ttu-id="3fc02-497">Örneğin, `sudo service bind9 restart` hem DNS sunucularında.</span><span class="sxs-lookup"><span data-stu-id="3fc02-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="3fc02-498">Bu adımları tamamladıktan sonra tam etki alanı adları (FQDN) kullanarak sanal ağınızdaki kaynaklara bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="3fc02-498">After completing these steps, you can connect to resources in the virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="3fc02-499">Bu gibi durumlarda, Hdınsight artık sanal ağınıza yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fc02-499">You can now install HDInsight into the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3fc02-500">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3fc02-500">Next steps</span></span>

* <span data-ttu-id="3fc02-501">Bir şirket ağına bağlanmak için Hdınsight yapılandırma uçtan uca örneği için bkz: [bir şirket içi ağınıza bağlanmak Hdınsight](./connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="3fc02-501">For an end-to-end example of configuring HDInsight to connect to an on-premises network, see [Connect HDInsight to an on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="3fc02-502">Azure sanal ağlar hakkında daha fazla bilgi için bkz: [Azure Virtual Network'e genel bakış](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3fc02-502">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="3fc02-503">Ağ güvenlik grupları hakkında daha fazla bilgi için bkz: [ağ güvenlik grupları](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="3fc02-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="3fc02-504">Kullanıcı tanımlı yollar hakkında daha fazla bilgi için bkz: [kullanıcı tanımlı yollar ve IP iletimini](../virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3fc02-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>