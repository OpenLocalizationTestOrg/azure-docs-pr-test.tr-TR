---
title: "Azure CLI aaaCreate bir Internet'e yönelik Yük Dengeleyici - | Microsoft Docs"
description: "Nasıl toocreate Kaynak Yöneticisi'ni kullanarak bir Internet'e yönelik Yük Dengeleyici hello Azure CLI öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a><span data-ttu-id="f011b-103">İnternet'Hello Azure CLI kullanarak bir yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="f011b-103">Creating an internet load balancer using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f011b-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f011b-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="f011b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f011b-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="f011b-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f011b-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="f011b-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="f011b-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="f011b-108">Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="f011b-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="f011b-109">Ayrıca [nasıl toocreate Internet'e yönelik Yük Dengeleyici Klasik dağıtım kullanarak bilgi edinin](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f011b-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="f011b-110">Hello Azure CLI kullanarak hello çözümü dağıtma</span><span class="sxs-lookup"><span data-stu-id="f011b-110">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="f011b-111">Aşağıdaki adımları hello nasıl toocreate Internet'e yönelik Yük Dengeleyici CLI ile Azure Resource Manager kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="f011b-111">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="f011b-112">Azure Resource her bir kaynak oluşturulur ve ayrı ayrı yapılandırılır Manager ile birlikte toocreate kaynak sonra yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="f011b-112">With Azure Resource Manager each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="f011b-113">Oluşturma ve nesneleri toodeploy bir yük dengeleyici aşağıdaki hello yapılandırmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f011b-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="f011b-114">Ön uç IP yapılandırması: Gelen ağ trafiği için genel IP adreslerini içerir.</span><span class="sxs-lookup"><span data-stu-id="f011b-114">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="f011b-115">Arka uç adres havuzu - hello yük dengeleyici gelen hello sanal makineleri tooreceive ağ trafiği için ağ arabirimlerine (NIC'ler) içerir.</span><span class="sxs-lookup"><span data-stu-id="f011b-115">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="f011b-116">Yük Dengeleme kuralları - hello yük dengeleyici tooport hello arka uç adres havuzundaki ortak bir bağlantı noktası eşleme kurallarını içerir.</span><span class="sxs-lookup"><span data-stu-id="f011b-116">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="f011b-117">Gelen NAT kuralları - noktasında hello yük dengeleyici tooa hello arka uç adres havuzundaki belirli bir sanal makine için genel bir bağlantı noktası eşleme kurallarını içerir.</span><span class="sxs-lookup"><span data-stu-id="f011b-117">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="f011b-118">Yoklamaları - sistem durumu kullanılan araştırmalar toocheck kullanılabilirliği hello arka uç adres havuzundaki sanal makineler örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="f011b-118">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="f011b-119">Daha fazla bilgi için bkz. [Yük Dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="f011b-119">For more information see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="f011b-120">CLI toouse Kaynak Yöneticisi'ni ayarlayın</span><span class="sxs-lookup"><span data-stu-id="f011b-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="f011b-121">Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="f011b-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="f011b-122">Merhaba çalıştırmak **azure config modu** aşağıda gösterildiği gibi komut tooswitch tooResource Yöneticisi modu.</span><span class="sxs-lookup"><span data-stu-id="f011b-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
        azure config mode arm
    ```

    <span data-ttu-id="f011b-123">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="f011b-123">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="f011b-124">Bir sanal ağ ve hello ön uç IP havuzu için bir ortak IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="f011b-124">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="f011b-125">Adlı bir sanal ağ (VNet) oluşturma *NRPVnet* hello Doğu ABD konumunda bir kaynak grubu kullanarak adlı *NRPRG*.</span><span class="sxs-lookup"><span data-stu-id="f011b-125">Create a virtual network (VNet) named *NRPVnet* in hello East US location using a resource group named *NRPRG*.</span></span>

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    <span data-ttu-id="f011b-126">*NRPVnet* içinde *NRPVnetSubnet* adına ve 10.0.0.0/24 CIDR bloğuna sahip bir alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f011b-126">Create a subnet named *NRPVnetSubnet* with a CIDR block of 10.0.0.0/24 in *NRPVnet*.</span></span>

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. <span data-ttu-id="f011b-127">Adlı bir ortak IP adresi oluşturma *NRPPublicIP* DNS adına sahip bir ön uç IP havuzu tarafından kullanılan toobe *loadbalancernrp.eastus.cloudapp.azure.com*. aşağıdaki hello komutu hello statik ayırma türü kullanır ve 4 dakika boşta kalma zaman aşımı.</span><span class="sxs-lookup"><span data-stu-id="f011b-127">Create a public IP address named *NRPPublicIP* toobe used by a front-end IP pool with DNS name *loadbalancernrp.eastus.cloudapp.azure.com*. hello command below uses hello static allocation type and idle timeout of 4 minutes.</span></span>

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="f011b-128">Merhaba yük dengeleyici hello etki alanı etiketi hello ortak IP FQDN'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="f011b-128">hello load balancer will use hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="f011b-129">Bu yük dengeleyici tam etki alanı adı (FQDN) hello gibi hello bulut hizmeti kullanan Klasik dağıtım değişiklik.</span><span class="sxs-lookup"><span data-stu-id="f011b-129">This a change from classic deployment, which uses hello cloud service as hello load balancer Fully Qualified Domain Name (FQDN).</span></span>
   > <span data-ttu-id="f011b-130">Bu örnekte, hello FQDN'sidir *loadbalancernrp.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="f011b-130">In this example, hello FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span>

## <a name="create-a-load-balancer"></a><span data-ttu-id="f011b-131">Yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="f011b-131">Create a load balancer</span></span>

<span data-ttu-id="f011b-132">Merhaba aşağıdaki komutu adlı bir yük dengeleyici oluşturur *NRPlb* hello içinde *NRPRG* hello kaynak grubunda *Doğu ABD* Azure konumu.</span><span class="sxs-lookup"><span data-stu-id="f011b-132">hello following command creates a load balancer named *NRPlb* in hello *NRPRG* resource group in hello *East US* Azure location.</span></span>

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a><span data-ttu-id="f011b-133">Ön uç IP havuzu ve arka uç adres havuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="f011b-133">Create a front-end IP pool and a backend address pool</span></span>
<span data-ttu-id="f011b-134">Bu örnek nasıl hello hello gelen ağ trafiğini alan toocreate hello ön uç IP havuzu yük dengeleyici ve arka uç IP havuzu burada hello ön uç havuzu hello yük dengeli ağ trafiği gönderir hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="f011b-134">This example demonstrates how toocreate hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello backend IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="f011b-135">Merhaba genel IP Hello önceki adımı ve hello yük dengeleyici oluşturulan ilişkilendirme bir ön uç IP havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f011b-135">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. <span data-ttu-id="f011b-136">Bir arka uç adres havuzu ayarlama tooreceive gelen trafiği hello ön uç IP havuzundan kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f011b-136">Set up a back-end address pool used tooreceive incoming traffic from hello front-end IP pool.</span></span>

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a><span data-ttu-id="f011b-137">LB kurallarını, NAT kurallarını ve araştırmayı oluşturma</span><span class="sxs-lookup"><span data-stu-id="f011b-137">Create LB rules, NAT rules, and probe</span></span>

<span data-ttu-id="f011b-138">Bu örnekte aşağıdaki öğelerindeki hello oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f011b-138">This example creates hello following items.</span></span>

* <span data-ttu-id="f011b-139">NAT kuralı tootranslate bağlantı noktası 21 tooport 22 tüm gelen trafiği<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f011b-139">a NAT rule tootranslate all incoming traffic on port 21 tooport 22<sup>1</sup></span></span>
* <span data-ttu-id="f011b-140">NAT kuralı tootranslate bağlantı noktası 23 tooport 22 tüm gelen trafiği</span><span class="sxs-lookup"><span data-stu-id="f011b-140">a NAT rule tootranslate all incoming traffic on port 23 tooport 22</span></span>
* <span data-ttu-id="f011b-141">bir yük dengeleyici kuralı toobalance hello arka uç havuzundaki tüm gelen trafiği hello üzerinde bağlantı noktası 80 tooport 80 giderir.</span><span class="sxs-lookup"><span data-stu-id="f011b-141">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="f011b-142">bir araştırma kural toocheck hello sistem durumu adlı bir sayfada *HealthProbe.aspx*.</span><span class="sxs-lookup"><span data-stu-id="f011b-142">a probe rule toocheck hello health status on a page named *HealthProbe.aspx*.</span></span>

<span data-ttu-id="f011b-143"><sup>1</sup> NAT kurallardır hello yük dengeleyicinin arkasındaki ilişkili tooa belirli bir sanal makine örneği.</span><span class="sxs-lookup"><span data-stu-id="f011b-143"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="f011b-144">21 bağlantı noktasına ulaşan hello ağ trafiği, bağlantı noktası 22 Bu NAT kuralı ile ilişkili tooa belirli bir sanal makine gönderilir.</span><span class="sxs-lookup"><span data-stu-id="f011b-144">hello network traffic arriving on port 21 is sent tooa specific virtual machine on port 22 associated with this NAT rule.</span></span> <span data-ttu-id="f011b-145">NAT kuralı için bir protokol (UDP veya TCP) belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f011b-145">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="f011b-146">Her iki protokole olamaz toohello aynı bağlantı noktasını atanmış.</span><span class="sxs-lookup"><span data-stu-id="f011b-146">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="f011b-147">Merhaba NAT kuralları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f011b-147">Create hello NAT rules.</span></span>

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. <span data-ttu-id="f011b-148">Yük dengeleyici kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f011b-148">Create a load balancer rule.</span></span>

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. <span data-ttu-id="f011b-149">Durum araştırması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f011b-149">Create a health probe.</span></span>

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. <span data-ttu-id="f011b-150">Ayarlarınızı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f011b-150">Check your settings.</span></span>

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    <span data-ttu-id="f011b-151">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="f011b-151">Expected output:</span></span>

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a><span data-ttu-id="f011b-152">NIC’leri oluşturma</span><span class="sxs-lookup"><span data-stu-id="f011b-152">Create NICs</span></span>

<span data-ttu-id="f011b-153">Toocreate NIC gerekir (veya var olanları değiştirme) ve tooNAT kuralları, yük dengeleyici kuralları ve araştırmalar ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f011b-153">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="f011b-154">Adlı bir NIC oluşturun *lb nıc1 olması*ve hello ile ilişkilendirmek *rdp1* NAT kuralı ve hello *NRPbackendpool* arka uç adres havuzu.</span><span class="sxs-lookup"><span data-stu-id="f011b-154">Create a NIC named *lb-nic1-be*, and associate it with hello *rdp1* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    <span data-ttu-id="f011b-155">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="f011b-155">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. <span data-ttu-id="f011b-156">Adlı bir NIC oluşturun *lb nic2 olması*ve hello ile ilişkilendirmek *rdp2* NAT kuralı ve hello *NRPbackendpool* arka uç adres havuzu.</span><span class="sxs-lookup"><span data-stu-id="f011b-156">Create a NIC named *lb-nic2-be*, and associate it with hello *rdp2* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. <span data-ttu-id="f011b-157">Adlı sanal makine (VM) oluşturma *web1*ve hello adlı NIC ile ilişkilendirme *lb nıc1 olması*.</span><span class="sxs-lookup"><span data-stu-id="f011b-157">Create a virtual machine (VM) named *web1*, and associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="f011b-158">Bir depolama hesabı olarak adlandırılan *web1nrp* aşağıdaki hello komutu çalıştırmadan önce oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="f011b-158">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="f011b-159">Bir yük dengeleyici gerek toobe içinde Vm'lerde aynı kullanılabilirlik kümesinde hello.</span><span class="sxs-lookup"><span data-stu-id="f011b-159">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="f011b-160">Kullanım `azure availset create` toocreate kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="f011b-160">Use `azure availset create` toocreate an availability set.</span></span>

    <span data-ttu-id="f011b-161">Merhaba çıkış benzer toohello aşağıdaki gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="f011b-161">hello output should be similar toohello following:</span></span>

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > <span data-ttu-id="f011b-162">Merhaba iletidir **yapılandırılmış Publicıp olmadan bir NIC budur** hello NIC oluşturulan hello yük dengeleyici genel IP adresi kullanarak tooInternet bağlanma hello yük dengeleyici için bu yana beklenir.</span><span class="sxs-lookup"><span data-stu-id="f011b-162">hello informational message **This is a NIC without publicIP configured** is expected since hello NIC created for hello load balancer connecting tooInternet using hello load balancer public IP address.</span></span>

    <span data-ttu-id="f011b-163">Merhaba itibaren *lb nıc1 olması* NIC hello ile ilişkili *rdp1* NAT kuralı, çok bağlanabilir*web1* 3441 hello yük dengeleyicideki bağlantı noktası üzerinden RDP kullanarak.</span><span class="sxs-lookup"><span data-stu-id="f011b-163">Since hello *lb-nic1-be* NIC is associated with hello *rdp1* NAT rule, you can connect too*web1* using RDP through port 3441 on hello load balancer.</span></span>

4. <span data-ttu-id="f011b-164">Adlı sanal makine (VM) oluşturma *web2*ve hello adlı NIC ile ilişkilendirme *lb nic2 olması*.</span><span class="sxs-lookup"><span data-stu-id="f011b-164">Create a virtual machine (VM) named *web2*, and associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="f011b-165">Bir depolama hesabı olarak adlandırılan *web1nrp* aşağıdaki hello komutu çalıştırmadan önce oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="f011b-165">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="f011b-166">Mevcut yük dengeleyiciyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f011b-166">Update an existing load balancer</span></span>
<span data-ttu-id="f011b-167">Var olan bir yük dengeleyiciye başvuran kurallar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f011b-167">You can add rules referencing an existing load balancer.</span></span> <span data-ttu-id="f011b-168">Merhaba sonraki örnekte yeni bir yük dengeleyici kuralı tooan varolan yük dengeleyicisi eklenir **NRPlb**</span><span class="sxs-lookup"><span data-stu-id="f011b-168">In hello next example, a new load balancer rule is added tooan existing load balancer **NRPlb**</span></span>

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="f011b-169">Yük dengeleyici silme</span><span class="sxs-lookup"><span data-stu-id="f011b-169">Delete a load balancer</span></span>
<span data-ttu-id="f011b-170">Komut tooremove bir yük dengeleyici aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="f011b-170">Use hello following command tooremove a load balancer:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a><span data-ttu-id="f011b-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f011b-171">Next steps</span></span>
[<span data-ttu-id="f011b-172">Bir iç yük dengeleyici yapılandırmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="f011b-172">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="f011b-173">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f011b-173">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="f011b-174">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f011b-174">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
