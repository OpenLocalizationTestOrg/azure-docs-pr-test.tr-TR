---
title: "IPv6 - Azure CLI ile bir Internet'e yönelik Yük Dengeleyici oluşturma | Microsoft Docs"
description: "Internet'e yönelik Yük Dengeleyici IPv6 Azure kaynağı Azure CLI kullanarak Yöneticisi'nde oluşturmayı öğrenin"
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
ms.openlocfilehash: efb4771800c42df544c3cc37d1d164045fdcaf3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-the-azure-cli"></a><span data-ttu-id="0b9d8-104">Internet'e yönelik Yük Dengeleyici IPv6 Azure kaynağı Azure CLI kullanarak Yöneticisi'nde oluşturun</span><span class="sxs-lookup"><span data-stu-id="0b9d8-104">Create an Internet facing load balancer with IPv6 in Azure Resource Manager using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b9d8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b9d8-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="0b9d8-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0b9d8-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="0b9d8-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="0b9d8-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="0b9d8-108">Azure Load Balancer bir Katman 4 (TCP, UDP) yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="0b9d8-109">Yük dengeleyici, gelen trafiği bulut hizmetlerindeki sağlıklı hizmet örnekleri veya bir yük dengeleyici kümesindeki sanal makineler arasında dağıtarak yüksek kullanılabilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="0b9d8-110">Ayrıca, Azure Load Balancer bu hizmetleri birden çok bağlantı noktasında, birden çok IP adresinde ya da her ikisinde birden sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="0b9d8-111">Örnek dağıtım senaryosu</span><span class="sxs-lookup"><span data-stu-id="0b9d8-111">Example deployment scenario</span></span>

<span data-ttu-id="0b9d8-112">Aşağıdaki diyagram yük dengeleme çözümü gösterir bu makalede açıklanan örnek şablon kullanılarak dağıtılan.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-112">The following diagram illustrates the load balancing solution being deployed using the example template described in this article.</span></span>

![Yük dengeleyici senaryosu](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="0b9d8-114">Bu senaryoda aşağıdaki Azure kaynakları oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="0b9d8-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="0b9d8-115">iki sanal makine (VM)</span><span class="sxs-lookup"><span data-stu-id="0b9d8-115">two virtual machines (VMs)</span></span>
* <span data-ttu-id="0b9d8-116">atanan IPv4 ve IPv6 adreslerinin her VM için bir sanal ağ arabirimi</span><span class="sxs-lookup"><span data-stu-id="0b9d8-116">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="0b9d8-117">bir IPv4 ve IPv6 genel IP adresi olan bir Internet'e yönelik Yük Dengeleyici</span><span class="sxs-lookup"><span data-stu-id="0b9d8-117">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="0b9d8-118">bir kullanılabilirlik kümesi, iki VM içerir</span><span class="sxs-lookup"><span data-stu-id="0b9d8-118">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="0b9d8-119">iki Yük Dengeleme kuralları özel uç noktaları için ortak VIP'ler eşlemek için</span><span class="sxs-lookup"><span data-stu-id="0b9d8-119">two load balancing rules to map the public VIPs to the private endpoints</span></span>

## <a name="deploying-the-solution-using-the-azure-cli"></a><span data-ttu-id="0b9d8-120">Çözümü Azure CLI kullanarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="0b9d8-120">Deploying the solution using the Azure CLI</span></span>

<span data-ttu-id="0b9d8-121">Aşağıda Azure Resource Manager ve CLI kullanarak İnternet’e yönelik yük dengeleyici oluşturma adımları yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="0b9d8-122">Azure Resource Manager ile her bir kaynak ayrı ayrı oluşturulup yapılandırıldıktan sonra kaynak oluşturmak için bir araya getirilir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-122">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="0b9d8-123">Bir yük dengeleyici dağıtmayı oluşturun ve aşağıdaki nesneleri yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="0b9d8-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="0b9d8-124">Ön uç IP yapılandırması: Gelen ağ trafiği için genel IP adreslerini içerir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="0b9d8-125">Arka uç adres havuzu: Sanal makinelerin yük dengeleyiciden ağ trafiği alması için ağ arabirimlerini (NIC’ler) içerir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="0b9d8-126">Yük dengeleme kuralları: Yük dengeleyici üzerindeki bir genel bağlantı noktasını arka uç adres havuzundaki bağlantı noktasına eşleme kurallarını içerir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="0b9d8-127">Gelen NAT kuralları: Yük dengeleyici üzerindeki bir genel bağlantı noktasını arka uç adres havuzundaki belirli bir sanal makineye ait bağlantı noktasına eşleme kurallarını içerir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="0b9d8-128">Araştırmalar: Arka uç adres havuzundaki sanal makine örneklerinin kullanılabilirliğini kontrol etmek için kullanılan durum araştırmalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="0b9d8-129">Daha fazla bilgi için bkz. [Yük Dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="0b9d8-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-your-cli-environment-to-use-azure-resource-manager"></a><span data-ttu-id="0b9d8-130">Azure Kaynak Yöneticisi'ni kullanmak için CLI ortamınızı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="0b9d8-130">Set up your CLI environment to use Azure Resource Manager</span></span>

<span data-ttu-id="0b9d8-131">Bu örnekte, CLI araçlarını bir PowerShell komut penceresinde çalıştırılmakta olan.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-131">For this example, we are running the CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="0b9d8-132">Azure PowerShell cmdlet'lerini kullanmayan ancak PowerShell'in komut dosyası özellikleri okunabilirlik ve yeniden geliştirmek için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-132">We are not using the Azure PowerShell cmdlets but we use PowerShell's scripting capabilities to improve readability and reuse.</span></span>

1. <span data-ttu-id="0b9d8-133">Hiç Azure CLI kullanmadıysanız bkz. [Azure CLI’yi Yükleme ve Yapılandırma](../cli-install-nodejs.md); sonra da, Azure hesabınızı ve aboneliğinizi seçtiğiniz noktaya kadar yönergeleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-133">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="0b9d8-134">Çalıştırma **azure config modu** Resource Manager moduna geçmek için komutu.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-134">Run the **azure config mode** command to switch to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="0b9d8-135">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="0b9d8-135">Expected output:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="0b9d8-136">Azure'da oturum açın ve Aboneliklerin listesini alın.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-136">Sign in to Azure and get a list of subscriptions.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="0b9d8-137">İstendiğinde Azure kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-137">Enter your Azure credentials when prompted.</span></span>

    ```azurecli
    azure account list
    ```

    <span data-ttu-id="0b9d8-138">Kullanmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-138">Pick the subscription you want to use.</span></span> <span data-ttu-id="0b9d8-139">Sonraki adım için abonelik kimliğini not edin.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-139">Make note of the subscription Id for the next step.</span></span>

4. <span data-ttu-id="0b9d8-140">CLI komutları ile kullanmak için PowerShell değişkenleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-140">Set up PowerShell variables for use with the CLI commands.</span></span>

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

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="0b9d8-141">Bir kaynak grubu, bir yük dengeleyici, bir sanal ağ ve alt ağlar oluşturun</span><span class="sxs-lookup"><span data-stu-id="0b9d8-141">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="0b9d8-142">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b9d8-142">Create a resource group</span></span>

    ```azurecli
    azure group create $rgName $location
    ```

2. <span data-ttu-id="0b9d8-143">Yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b9d8-143">Create a load balancer</span></span>

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="0b9d8-144">Bir sanal ağ (VNet) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-144">Create a virtual network (VNet).</span></span>

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    <span data-ttu-id="0b9d8-145">Bu VNet iki alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-145">Create two subnets in this VNet.</span></span>

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-the-front-end-pool"></a><span data-ttu-id="0b9d8-146">Ortak IP adresleri için ön uç havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b9d8-146">Create public IP addresses for the front-end pool</span></span>

1. <span data-ttu-id="0b9d8-147">PowerShell değişkenlerini ayarlamak</span><span class="sxs-lookup"><span data-stu-id="0b9d8-147">Set up the PowerShell variables</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="0b9d8-148">Bir ortak IP adresi ön uç IP havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-148">Create a public IP address the front-end IP pool.</span></span>

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="0b9d8-149">Yük dengeleyici, FQDN olarak genel IP'nin etki alanı etiketini kullanır.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-149">The load balancer uses the domain label of the public IP as its FQDN.</span></span> <span data-ttu-id="0b9d8-150">Bu bulut hizmeti kullanan Klasik dağıtım değişiklik adı yük dengeleyici FQDN olarak.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-150">This a change from classic deployment, which uses the cloud service name as the load balancer FQDN.</span></span>
    > <span data-ttu-id="0b9d8-151">Bu örnekte FQDN'sidir *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-151">In this example, the FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="0b9d8-152">Ön uç ve arka uç havuzları oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b9d8-152">Create front-end and back-end pools</span></span>

<span data-ttu-id="0b9d8-153">Bu örnek, yük dengeleyici gelen ağ trafiği alır ön uç IP havuzu ve burada ön uç havuzu yük dengeli ağ trafiği gönderir arka uç IP havuzu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-153">This example creates the front-end IP pool that receives the incoming network traffic on the load balancer and the back-end IP pool where the front-end pool sends the load balanced network traffic.</span></span>

1. <span data-ttu-id="0b9d8-154">PowerShell değişkenlerini ayarlamak</span><span class="sxs-lookup"><span data-stu-id="0b9d8-154">Set up the PowerShell variables</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="0b9d8-155">Önceki adımda oluşturulan genel IP’yi ve yük dengeleyiciyi ilişkilendirerek bir ön uç IP havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-155">Create a front-end IP pool associating the public IP created in the previous step and the load balancer.</span></span>

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-the-probe-nat-rules-and-lb-rules"></a><span data-ttu-id="0b9d8-156">Yoklama, NAT kuralları ve LB kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b9d8-156">Create the probe, NAT rules, and LB rules</span></span>

<span data-ttu-id="0b9d8-157">Bu örnek aşağıdaki nesneleri oluşturur:</span><span class="sxs-lookup"><span data-stu-id="0b9d8-157">This example creates the following items:</span></span>

* <span data-ttu-id="0b9d8-158">TCP bağlantı noktası 80 bağlantısını denetlemek için bir araştırma kuralı</span><span class="sxs-lookup"><span data-stu-id="0b9d8-158">a probe rule to check for connectivity to TCP port 80</span></span>
* <span data-ttu-id="0b9d8-159">3389 numaralı bağlantı noktasına 3389 numaralı bağlantı noktasındaki tüm gelen trafiği için RDP çevirmek için NAT kuralı<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="0b9d8-159">a NAT rule to translate all incoming traffic on port 3389 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="0b9d8-160">bağlantı noktası 3391 3389 numaralı bağlantı noktasına gelen tüm trafiği için RDP çevirmek için NAT kuralı<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="0b9d8-160">a NAT rule to translate all incoming traffic on port 3391 to port 3389 for RDP<sup>1</sup></span></span>
* <span data-ttu-id="0b9d8-161">80 numaralı bağlantı noktasına gelen tüm trafiği arka uç havuzundaki adreslerin 80 numaralı bağlantı noktasıyla dengeleyen yük dengeleyici kuralı.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-161">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>

<span data-ttu-id="0b9d8-162"><sup>1</sup> NAT kuralları yük dengeleyici arkasındaki belirli sanal makine örnekleriyle ilişkilendirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-162"><sup>1</sup> NAT rules are associated to a specific virtual machine instance behind the load balancer.</span></span> <span data-ttu-id="0b9d8-163">Belirli bir sanal makine ve NAT kuralıyla ilişkili bağlantı noktası 3389 numaralı bağlantı noktasına gelen ağ trafiğini gönderilir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-163">The network traffic arriving on port 3389 is sent to the specific virtual machine and port associated with the NAT rule.</span></span> <span data-ttu-id="0b9d8-164">NAT kuralı için bir protokol (UDP veya TCP) belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-164">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="0b9d8-165">Her iki protokolü aynı bağlantı noktasına atayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-165">Both protocols can't be assigned to the same port.</span></span>

1. <span data-ttu-id="0b9d8-166">PowerShell değişkenlerini ayarlamak</span><span class="sxs-lookup"><span data-stu-id="0b9d8-166">Set up the PowerShell variables</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="0b9d8-167">Araştırma oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b9d8-167">Create the probe</span></span>

    <span data-ttu-id="0b9d8-168">Aşağıdaki örnek, 15 dakikada denetleyen bir TCP araştırması arka uç TCP bağlantı noktası 80 bağlantısını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-168">The following example creates a TCP probe that checks for connectivity to back-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="0b9d8-169">Bunu uç kaynak kullanılamıyor sonra iki ardışık hatalarını işaretler.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-169">It will mark the back-end resource unavailable after two consecutive failures.</span></span>

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. <span data-ttu-id="0b9d8-170">Arka uç kaynaklarına RDP bağlantılara izin veren gelen NAT kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b9d8-170">Create inbound NAT rules that allow RDP connections to the back-end resources</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="0b9d8-171">Bir yük dengeleyici hangi ön uç isteği aldığını bağlı olarak farklı arka uç bağlantı noktaları için trafiği göndermek kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b9d8-171">Create a load balancer rules that send traffic to different back-end ports depending on which front end received the request</span></span>

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="0b9d8-172">Ayarlarınızı denetleyin</span><span class="sxs-lookup"><span data-stu-id="0b9d8-172">Check your settings</span></span>

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="0b9d8-173">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="0b9d8-173">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up the load balancer "myIPv4IPv6Lb"
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

## <a name="create-nics"></a><span data-ttu-id="0b9d8-174">NIC’leri oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b9d8-174">Create NICs</span></span>

<span data-ttu-id="0b9d8-175">NIC oluşturun ve bunları NAT kuralları, yük dengeleyici kuralları ve araştırmalar ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-175">Create NICs and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="0b9d8-176">PowerShell değişkenlerini ayarlamak</span><span class="sxs-lookup"><span data-stu-id="0b9d8-176">Set up the PowerShell variables</span></span>

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

2. <span data-ttu-id="0b9d8-177">Her arka uç için bir NIC oluşturun ve IPv6 yapılandırmasını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-177">Create a NIC for each back-end and add an IPv6 configuration.</span></span>

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-the-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="0b9d8-178">Arka uç VM kaynakları oluşturun ve her NIC ekleme</span><span class="sxs-lookup"><span data-stu-id="0b9d8-178">Create the back-end VM resources and attach each NIC</span></span>

<span data-ttu-id="0b9d8-179">Sanal makineleri oluşturmak için bir depolama hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-179">To create VMs, you must have a storage account.</span></span> <span data-ttu-id="0b9d8-180">Yük Dengeleme için sanal makineleri bir kullanılabilirlik kümesi üyesi olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-180">For load balancing, the VMs need to be members of an availability set.</span></span> <span data-ttu-id="0b9d8-181">Sanal makineleri oluşturma hakkında daha fazla bilgi için bkz: [Azure PowerShell kullanarak bir VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0b9d8-181">For more information about creating VMs, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="0b9d8-182">PowerShell değişkenlerini ayarlamak</span><span class="sxs-lookup"><span data-stu-id="0b9d8-182">Set up the PowerShell variables</span></span>

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
    > <span data-ttu-id="0b9d8-183">Bu örnek, kullanıcı adı ve parola düz metin VM'ler için kullanır.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-183">This example uses the username and password for the VMs in clear text.</span></span> <span data-ttu-id="0b9d8-184">Açık bir şekilde kullanarak kimlik bilgileri değiştiğinde uygun dikkatli olunması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-184">Appropriate care must be taken when using credentials in the clear.</span></span> <span data-ttu-id="0b9d8-185">Daha güvenli bir yöntem PowerShell kimlik bilgilerini işleme bilgi için bkz: [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-185">For a more secure method of handling credentials in PowerShell, see the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="0b9d8-186">Depolama hesabı ve kullanılabilirlik kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="0b9d8-186">Create the storage account and availability set</span></span>

    <span data-ttu-id="0b9d8-187">Sanal makineleri oluşturduğunuzda, mevcut bir depolama hesabını kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-187">You may use an existing storage account when you create the VMs.</span></span> <span data-ttu-id="0b9d8-188">Aşağıdaki komut, yeni bir depolama hesabı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-188">The following command creates a new storage account.</span></span>

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    <span data-ttu-id="0b9d8-189">Ardından, kullanılabilirlik kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0b9d8-189">Next, create the availability set.</span></span>

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="0b9d8-190">Sanal makineler ile ilişkili NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="0b9d8-190">Create the virtual machines with the associated NICs</span></span>

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a><span data-ttu-id="0b9d8-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0b9d8-191">Next steps</span></span>

[<span data-ttu-id="0b9d8-192">Bir iç yük dengeleyici yapılandırmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="0b9d8-192">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="0b9d8-193">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0b9d8-193">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="0b9d8-194">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0b9d8-194">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
