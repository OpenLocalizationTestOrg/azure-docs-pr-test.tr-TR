---
title: "IPv6 - Azure CLI ile aaaCreate bir Internet'e yönelik Yük Dengeleyici | Microsoft Docs"
description: "Nasıl toocreate Azure Resource Manager kullanarak bir Internet'e yönelik Yük Dengeleyici IPv6 hello Azure CLI öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "IPv6, azure yük dengeleyici, çift yığın, genel IP, yerel IPv6, mobil, IOT"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a><span data-ttu-id="ff961-104">Internet'e yönelik Yük Dengeleyici IPv6 Azure kaynağı hello Azure CLI kullanarak Yöneticisi'nde oluşturun</span><span class="sxs-lookup"><span data-stu-id="ff961-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff961-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff961-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="ff961-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ff961-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="ff961-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="ff961-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="ff961-108">Azure Load Balancer bir Katman 4 (TCP, UDP) yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="ff961-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="ff961-109">Merhaba yük dengeleyici, gelen trafiği bulut Hizmetleri sağlıklı hizmet örnekleri veya bir yük dengeleyici kümesindeki sanal makineler arasında dağıtarak yüksek kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff961-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="ff961-110">Ayrıca, Azure Load Balancer bu hizmetleri birden çok bağlantı noktasında, birden çok IP adresinde ya da her ikisinde birden sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ff961-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="ff961-111">Örnek dağıtım senaryosu</span><span class="sxs-lookup"><span data-stu-id="ff961-111">Example deployment scenario</span></span>

<span data-ttu-id="ff961-112">Merhaba Aşağıdaki diyagramda gösterilmektedir hello yük dengeleme çözümü bu makalede açıklanan hello örnek şablon kullanılarak dağıtılan.</span><span class="sxs-lookup"><span data-stu-id="ff961-112">hello following diagram illustrates hello load balancing solution being deployed using hello example template described in this article.</span></span>

![Yük dengeleyici senaryosu](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="ff961-114">Bu senaryoda aşağıdaki Azure kaynakları hello oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="ff961-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="ff961-115">iki sanal makine (VM)</span><span class="sxs-lookup"><span data-stu-id="ff961-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="ff961-116">atanan IPv4 ve IPv6 adreslerinin her VM için bir sanal ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="ff961-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="ff961-117">bir IPv4 ve IPv6 genel IP adresi olan bir Internet'e yönelik Yük Dengeleyici</span><span class="sxs-lookup"><span data-stu-id="ff961-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="ff961-118">Merhaba iki sanal makineleri bir kullanılabilirlik kümesi toothat içerir</span><span class="sxs-lookup"><span data-stu-id="ff961-118">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="ff961-119">iki Yük Dengeleme kuralları toomap hello ortak VIP'ler toohello özel uç noktaları</span><span class="sxs-lookup"><span data-stu-id="ff961-119">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="ff961-120">Hello Azure CLI kullanarak hello çözümü dağıtma</span><span class="sxs-lookup"><span data-stu-id="ff961-120">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="ff961-121">Aşağıdaki adımları hello nasıl toocreate Internet'e yönelik Yük Dengeleyici CLI ile Azure Resource Manager kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff961-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="ff961-122">Azure Resource Manager ile her bir kaynak oluşturulur ve ayrı ayrı yapılandırılır ve toocreate kaynak bir araya getirin.</span><span class="sxs-lookup"><span data-stu-id="ff961-122">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="ff961-123">oluşturma ve nesneleri aşağıdaki hello yapılandırma toodeploy bir yük dengeleyici:</span><span class="sxs-lookup"><span data-stu-id="ff961-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="ff961-124">Ön uç IP yapılandırması: Gelen ağ trafiği için genel IP adreslerini içerir.</span><span class="sxs-lookup"><span data-stu-id="ff961-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="ff961-125">Arka uç adres havuzu - hello yük dengeleyici gelen hello sanal makineleri tooreceive ağ trafiği için ağ arabirimlerine (NIC'ler) içerir.</span><span class="sxs-lookup"><span data-stu-id="ff961-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="ff961-126">Yük Dengeleme kuralları - hello yük dengeleyici tooport hello arka uç adres havuzundaki ortak bir bağlantı noktası eşleme kurallarını içerir.</span><span class="sxs-lookup"><span data-stu-id="ff961-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="ff961-127">Gelen NAT kuralları - noktasında hello yük dengeleyici tooa hello arka uç adres havuzundaki belirli bir sanal makine için genel bir bağlantı noktası eşleme kurallarını içerir.</span><span class="sxs-lookup"><span data-stu-id="ff961-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="ff961-128">Yoklamaları - sistem durumu kullanılan araştırmalar toocheck kullanılabilirliği hello arka uç adres havuzundaki sanal makineler örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="ff961-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="ff961-129">Daha fazla bilgi için bkz. [Yük Dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ff961-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a><span data-ttu-id="ff961-130">CLI ortamı toouse Azure Resource Manager ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ff961-130">Set up your CLI environment toouse Azure Resource Manager</span></span>

<span data-ttu-id="ff961-131">Bu örnekte, biz bir PowerShell komut penceresinde hello CLI araçlarını çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="ff961-131">For this example, we are running hello CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="ff961-132">Hello Azure PowerShell cmdlet'lerini kullanmayan ancak PowerShell'in komut dosyası özellikleri tooimprove okunabilirlik ve yeniden kullanırız.</span><span class="sxs-lookup"><span data-stu-id="ff961-132">We are not using hello Azure PowerShell cmdlets but we use PowerShell's scripting capabilities tooimprove readability and reuse.</span></span>

1. <span data-ttu-id="ff961-133">Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="ff961-133">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="ff961-134">Merhaba çalıştırmak **azure config modu** komutu tooswitch tooResource Yöneticisi modu.</span><span class="sxs-lookup"><span data-stu-id="ff961-134">Run hello **azure config mode** command tooswitch tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="ff961-135">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="ff961-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="ff961-136">İçinde tooAzure oturum ve Aboneliklerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="ff961-136">Sign in tooAzure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="ff961-137">İstendiğinde Azure kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="ff961-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="ff961-138">Merhaba aboneliğini toouse seçin.</span><span class="sxs-lookup"><span data-stu-id="ff961-138">Pick hello subscription you want toouse.</span></span> <span data-ttu-id="ff961-139">Merhaba sonraki adımınız hello abonelik kimliği not edin.</span><span class="sxs-lookup"><span data-stu-id="ff961-139">Make note of hello subscription Id for hello next step.</span></span>

4. <span data-ttu-id="ff961-140">Merhaba CLI komutları ile kullanmak için PowerShell değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ff961-140">Set up PowerShell variables for use with hello CLI commands.</span></span>

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="ff961-141">Bir kaynak grubu, bir yük dengeleyici, bir sanal ağ ve alt ağlar oluşturun</span><span class="sxs-lookup"><span data-stu-id="ff961-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="ff961-142">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff961-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="ff961-143">Yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff961-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="ff961-144">Bir sanal ağ (VNet) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff961-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="ff961-145">Bu VNet iki alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff961-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a><span data-ttu-id="ff961-146">Ortak IP adresleri hello ön uç havuzu için oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff961-146">Create public IP addresses for hello front-end pool</span></span>

1. <span data-ttu-id="ff961-147">Merhaba PowerShell değişkenlerini ayarlamak</span><span class="sxs-lookup"><span data-stu-id="ff961-147">Set up hello PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="ff961-148">Bir ortak IP adresi hello ön uç IP havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff961-148">Create a public IP address hello front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="ff961-149">Merhaba yük dengeleyicisi hello etki alanı etiketi hello ortak IP FQDN'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ff961-149">hello load balancer uses hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="ff961-150">Bu yük dengeleyici FQDN hello gibi hello bulut hizmeti adı kullanan Klasik dağıtım değişiklik.</span><span class="sxs-lookup"><span data-stu-id="ff961-150">This a change from classic deployment, which uses hello cloud service name as hello load balancer FQDN.</span></span>
    > <span data-ttu-id="ff961-151">Bu örnekte, hello FQDN'sidir *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="ff961-151">In this example, hello FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="ff961-152">Ön uç ve arka uç havuzları oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff961-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="ff961-153">Bu örnek hello hello yük dengeleyici gelen ağ trafiğini alan hello ön uç IP havuzu ve burada hello ön uç havuzu hello yük dengeli ağ trafiği gönderir hello arka uç IP havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff961-153">This example creates hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello back-end IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="ff961-154">Merhaba PowerShell değişkenlerini ayarlamak</span><span class="sxs-lookup"><span data-stu-id="ff961-154">Set up hello PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="ff961-155">Merhaba genel IP Hello önceki adımı ve hello yük dengeleyici oluşturulan ilişkilendirme bir ön uç IP havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff961-155">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="ff961-156">Merhaba araştırma, NAT kuralları ve LB kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff961-156">Create hello probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="ff961-157">Bu örnekte aşağıdaki öğelerindeki hello oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ff961-157">This example creates hello following items:</span></span>

* <span data-ttu-id="ff961-158">bir araştırma kural toocheck bağlantı tooTCP bağlantı noktası 80</span><span class="sxs-lookup"><span data-stu-id="ff961-158">a probe rule toocheck for connectivity tooTCP port 80</span></span>
* <span data-ttu-id="ff961-159">NAT kuralı tootranslate 3389 numaralı bağlantı noktası 3389 tooport tüm gelen trafiği için RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="ff961-159">a NAT rule tootranslate all incoming traffic on port 3389 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="ff961-160">NAT kuralı tootranslate 3389 numaralı bağlantı noktası 3391 tooport tüm gelen trafiği için RDP<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="ff961-160">a NAT rule tootranslate all incoming traffic on port 3391 tooport 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="ff961-161">bir yük dengeleyici kuralı toobalance hello arka uç havuzundaki tüm gelen trafiği hello üzerinde bağlantı noktası 80 tooport 80 giderir.</span><span class="sxs-lookup"><span data-stu-id="ff961-161">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>

<span data-ttu-id="ff961-162"><sup>1</sup> NAT kurallardır hello yük dengeleyicinin arkasındaki ilişkili tooa belirli bir sanal makine örneği.</span><span class="sxs-lookup"><span data-stu-id="ff961-162"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="ff961-163">Merhaba ağ trafiği 3389 numaralı bağlantı noktasına ulaşan toohello belirli bir sanal makine ve bağlantı noktası hello NAT kuralıyla ilişkili gönderilir.</span><span class="sxs-lookup"><span data-stu-id="ff961-163">hello network traffic arriving on port 3389 is sent toohello specific virtual machine and port associated with hello NAT rule.</span></span> <span data-ttu-id="ff961-164">NAT kuralı için bir protokol (UDP veya TCP) belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff961-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="ff961-165">Her iki protokole olamaz toohello aynı bağlantı noktasını atanmış.</span><span class="sxs-lookup"><span data-stu-id="ff961-165">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="ff961-166">Merhaba PowerShell değişkenlerini ayarlamak</span><span class="sxs-lookup"><span data-stu-id="ff961-166">Set up hello PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="ff961-167">Merhaba araştırması oluştur</span><span class="sxs-lookup"><span data-stu-id="ff961-167">Create hello probe</span></span>

    <span data-ttu-id="ff961-168">Merhaba aşağıdaki örnek denetleyen bir TCP araştırması bağlantı tooback uç TCP bağlantı noktası 80 için 15 dakikada oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff961-168">hello following example creates a TCP probe that checks for connectivity tooback-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="ff961-169">Bunu hello arka uç kaynak kullanılamıyor sonra iki ardışık hatalarını işaretler.</span><span class="sxs-lookup"><span data-stu-id="ff961-169">It will mark hello back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="ff961-170">Toohello arka uç kaynaklarına RDP bağlantılara izin veren gelen NAT kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff961-170">Create inbound NAT rules that allow RDP connections toohello back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="ff961-171">Bir yük dengeleyici trafiği toodifferent arka uç bağlantı noktaları bağlı olarak hangi ön uç alınan hello isteği gönderme kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff961-171">Create a load balancer rules that send traffic toodifferent back-end ports depending on which front end received hello request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="ff961-172">Ayarlarınızı denetleyin</span><span class="sxs-lookup"><span data-stu-id="ff961-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="ff961-173">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="ff961-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a><span data-ttu-id="ff961-174">NIC’leri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff961-174">Create NICs</span></span>

<span data-ttu-id="ff961-175">NIC oluşturun ve bunları tooNAT kuralları, yük dengeleyici kuralları ve araştırmalar ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="ff961-175">Create NICs and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="ff961-176">Merhaba PowerShell değişkenlerini ayarlamak</span><span class="sxs-lookup"><span data-stu-id="ff961-176">Set up hello PowerShell variables</span></span>

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. <span data-ttu-id="ff961-177">Her arka uç için bir NIC oluşturun ve IPv6 yapılandırmasını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ff961-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="ff961-178">Merhaba arka uç VM kaynakları oluşturun ve her NIC ekleme</span><span class="sxs-lookup"><span data-stu-id="ff961-178">Create hello back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="ff961-179">toocreate VM'ler, bir depolama hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff961-179">toocreate VMs, you must have a storage account.</span></span> <span data-ttu-id="ff961-180">Yük Dengeleme için hello sanal makineleri bir kullanılabilirlik kümesi toobe üyeleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff961-180">For load balancing, hello VMs need toobe members of an availability set.</span></span> <span data-ttu-id="ff961-181">Sanal makineleri oluşturma hakkında daha fazla bilgi için bkz: [Azure PowerShell kullanarak bir VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="ff961-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="ff961-182">Merhaba PowerShell değişkenlerini ayarlamak</span><span class="sxs-lookup"><span data-stu-id="ff961-182">Set up hello PowerShell variables</span></span>

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > <span data-ttu-id="ff961-183">Bu örnek düz metin hello VM'ler için hello kullanıcı adını ve parolasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="ff961-183">This example uses hello username and password for hello VMs in clear text.</span></span> <span data-ttu-id="ff961-184">Kullanarak hello temizleyin kimlik bilgileri değiştiğinde uygun dikkatli olunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff961-184">Appropriate care must be taken when using credentials in hello clear.</span></span> <span data-ttu-id="ff961-185">Merhaba daha güvenli bir yöntem PowerShell kimlik bilgilerini işleme bilgi için bkz: [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ff961-185">For a more secure method of handling credentials in PowerShell, see hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="ff961-186">Merhaba depolama hesabı ve kullanılabilirlik kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="ff961-186">Create hello storage account and availability set</span></span>

    <span data-ttu-id="ff961-187">Merhaba VM'ler oluşturduğunuzda, mevcut bir depolama hesabını kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="ff961-187">You may use an existing storage account when you create hello VMs.</span></span> <span data-ttu-id="ff961-188">komutu aşağıdaki hello yeni bir depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ff961-188">hello following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="ff961-189">Ardından, hello kullanılabilirlik kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff961-189">Next, create hello availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="ff961-190">İle ilişkili hello NIC Hello sanal makineler oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff961-190">Create hello virtual machines with hello associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="ff961-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff961-191">Next steps</span></span>

[<span data-ttu-id="ff961-192">Bir iç yük dengeleyici yapılandırmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="ff961-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="ff961-193">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ff961-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="ff961-194">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ff961-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
