---
title: "Azure CLI aaaCreate bir dahili yük dengeleyici - | Microsoft Docs"
description: "Nasıl toocreate kullanarak iç yük dengeleyiciye hello Azure CLI Kaynak Yöneticisi'nde öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a><span data-ttu-id="7436a-103">Hello Azure CLI kullanarak bir iç yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="7436a-103">Create an internal load balancer by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7436a-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7436a-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="7436a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7436a-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="7436a-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7436a-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="7436a-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="7436a-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="7436a-108">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7436a-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="7436a-109">Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](load-balancer-get-started-ilb-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7436a-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a><span data-ttu-id="7436a-110">Hello Azure CLI kullanarak Hello çözümü dağıtma</span><span class="sxs-lookup"><span data-stu-id="7436a-110">Deploy hello solution by using hello Azure CLI</span></span>

<span data-ttu-id="7436a-111">Aşağıdaki adımları hello nasıl toocreate bir Internet'e yönelik Yük Dengeleyici CLI ile Azure Kaynak Yöneticisi'ni kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="7436a-111">hello following steps show how toocreate an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="7436a-112">Azure Resource Manager ile her bir kaynak oluşturulur ve ayrı ayrı yapılandırılır ve toocreate kaynak bir araya getirin.</span><span class="sxs-lookup"><span data-stu-id="7436a-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="7436a-113">Nesneleri toodeploy bir yük dengeleyici aşağıdaki hello yapılandırmak ve toocreate gerekir:</span><span class="sxs-lookup"><span data-stu-id="7436a-113">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="7436a-114">**Ön uç IP yapılandırması**: Gelen ağ trafiği için genel IP adreslerini içerir</span><span class="sxs-lookup"><span data-stu-id="7436a-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="7436a-115">**Arka uç adres havuzu**: hello yük dengeleyiciden hello sanal makineleri tooreceive ağ trafiğini etkinleştiren ağ arabirimlerine (NIC'ler) içerir</span><span class="sxs-lookup"><span data-stu-id="7436a-115">**Back-end address pool**: contains network interfaces (NICs) that enable hello virtual machines tooreceive network traffic from hello load balancer</span></span>
* <span data-ttu-id="7436a-116">**Yük Dengeleme kuralları**: hello yük dengeleyici tooport hello arka uç adres havuzundaki ortak bir bağlantı noktası eşleme kurallarını içerir</span><span class="sxs-lookup"><span data-stu-id="7436a-116">**Load-balancing rules**: contains rules that map a public port on hello load balancer tooport in hello back-end address pool</span></span>
* <span data-ttu-id="7436a-117">**Gelen NAT kuralları**: bağlantı noktasında hello yük dengeleyici tooa hello arka uç adres havuzundaki belirli bir sanal makine için genel bir bağlantı noktası eşleme kurallarını içerir</span><span class="sxs-lookup"><span data-stu-id="7436a-117">**Inbound NAT rules**: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool</span></span>
* <span data-ttu-id="7436a-118">**Yoklamaları**: kullanılan toocheck hello kullanılabilirlik hello arka uç adres havuzundaki sanal makineler örnekleri olan sistem durumu araştırmalarının içerir</span><span class="sxs-lookup"><span data-stu-id="7436a-118">**Probes**: contains health probes that are used toocheck hello availability of virtual machines instances in hello back-end address pool</span></span>

<span data-ttu-id="7436a-119">Daha fazla bilgi için bkz. [Yük Dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="7436a-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="7436a-120">CLI toouse Kaynak Yöneticisi'ni ayarlayın</span><span class="sxs-lookup"><span data-stu-id="7436a-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="7436a-121">Azure CLI hiç kullanmadıysanız bkz [yükleyin ve hello Azure CLI yapılandırma](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7436a-121">If you have never used Azure CLI, see [Install and configure hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="7436a-122">Sonra Azure hesabınızı ve aboneliğinizi toohello noktaya Hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="7436a-122">Follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="7436a-123">Merhaba çalıştırmak **azure config modu** tooswitch tooResource Yöneticisi modu, aşağıdaki gibi komutu:</span><span class="sxs-lookup"><span data-stu-id="7436a-123">Run hello **azure config mode** command tooswitch tooResource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="7436a-124">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="7436a-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="7436a-125">Adım adım iç yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="7436a-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="7436a-126">TooAzure oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7436a-126">Sign in tooAzure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="7436a-127">İstendiğinde Azure kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="7436a-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="7436a-128">Merhaba komutu araçları tooAzure Resource Manager modunu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7436a-128">Change hello command tools tooAzure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="7436a-129">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7436a-129">Create a resource group</span></span>

<span data-ttu-id="7436a-130">Azure Resource Manager’daki tüm kaynaklar bir kaynak grubuyla ilişkilendirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7436a-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="7436a-131">Henüz yapmadıysanız, bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7436a-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="7436a-132">İç yük dengeleyici kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7436a-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="7436a-133">İç yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="7436a-133">Create an internal load balancer</span></span>

    <span data-ttu-id="7436a-134">Senaryo aşağıdaki hello, Doğu ABD bölgesinde nrprg adlı bir kaynak grubu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7436a-134">In hello following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="7436a-135">Sanal ağlar ve sanal ağ alt ağları gibi bir iç yük dengeleyicileri için tüm kaynakları olmalıdır hello aynı kaynak grubunu ve de aynı hello bölgesi.</span><span class="sxs-lookup"><span data-stu-id="7436a-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in hello same resource group and in hello same region.</span></span>

2. <span data-ttu-id="7436a-136">Merhaba iç yük dengeleyici için bir ön uç IP adresi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7436a-136">Create a front-end IP address for hello internal load balancer.</span></span>

    <span data-ttu-id="7436a-137">kullandığınız başlangıç IP adresi hello alt ağ aralığında sanal ağınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7436a-137">hello IP address that you use must be within hello subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="7436a-138">Merhaba arka uç adres havuzu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7436a-138">Create hello back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="7436a-139">Ön uç IP adresi ve arka uç adres havuzu tanımladıktan sonra yük dengeleyici kurallarını, gelen NAT kurallarını ve özel sistem durumu araştırmalarını oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7436a-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="7436a-140">Merhaba iç yük dengeleyici için yük dengeleyici kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7436a-140">Create a load balancer rule for hello internal load balancer.</span></span>

    <span data-ttu-id="7436a-141">Merhaba önceki adımları izlediğinizde, hello komutu dinleme tooport 1433 için bir yük dengeleyici kuralı hello ön uç havuzu ve gönderen yük dengeli ağ trafiği toohello arka uç adres havuzu, ayrıca bağlantı noktası 1433'ü kullanarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7436a-141">When you follow hello previous steps, hello command creates a load-balancer rule for listening tooport 1433 in hello front-end pool and sending load-balanced network traffic toohello back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="7436a-142">Gelen NAT kurallarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7436a-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="7436a-143">Gelen NAT kuralları tooa belirli bir sanal makine örneği ziyaret kullanılan toocreate yük dengeleyicideki noktalarıdır.</span><span class="sxs-lookup"><span data-stu-id="7436a-143">Inbound NAT rules are used toocreate endpoints in a load balancer that go tooa specific virtual machine instance.</span></span> <span data-ttu-id="7436a-144">Merhaba önceki adımları Uzak Masaüstü için iki NAT kuralı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7436a-144">hello previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="7436a-145">Sistem durumu araştırmalarının hello yük dengeleyici için oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7436a-145">Create health probes for hello load balancer.</span></span>

    <span data-ttu-id="7436a-146">Bir sistem durumu araştırması tüm sanal makine örnekleri toomake ağ trafiğinin gönderebilir emin denetler.</span><span class="sxs-lookup"><span data-stu-id="7436a-146">A health probe checks all virtual machine instances toomake sure they can send network traffic.</span></span> <span data-ttu-id="7436a-147">Merhaba sanal makine örneği başarısız araştırma denetimleri ile Merhaba yük dengeleyiciden tekrar çevrimiçi duruma geçtiğinde ve bir araştırma denetimi sağlıklı olduğunu belirler kadar kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="7436a-147">hello virtual machine instance with failed probe checks is removed from hello load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="7436a-148">Merhaba Microsoft Azure platformu statik, genel olarak yönlendirilebilir bir IPv4 adresi çeşitli yönetim senaryoları için kullanır.</span><span class="sxs-lookup"><span data-stu-id="7436a-148">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="7436a-149">Başlangıç IP adresi 168.63.129.16 değil.</span><span class="sxs-lookup"><span data-stu-id="7436a-149">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="7436a-150">Bu IP adresinin güvenlik duvarları tarafından engellenmesi beklenmeyen davranışlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="7436a-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="7436a-151">Saygı tooAzure iç Yük Dengeleme ile bu IP adresi yük dengeli kümesinde sanal makineler için hello yük dengeleyici toodetermine hello sistem durumu araştırmalarının izleme tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7436a-151">With respect tooAzure internal load balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="7436a-152">Bir ağ güvenlik grubu kullanılan toorestrict trafiği tooAzure sanal makineleri bir dahili yük dengeli kümesindeki ya uygulanan tooa sanal ağ alt ise, bir ağ güvenlik kuralı tooallow trafiği 168.63.129.16 eklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="7436a-152">If a network security group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa virtual network subnet, ensure that a network security rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="7436a-153">NIC’leri oluşturma</span><span class="sxs-lookup"><span data-stu-id="7436a-153">Create NICs</span></span>

<span data-ttu-id="7436a-154">Toocreate NIC gerekir (veya var olanları değiştirme) ve tooNAT kuralları, yük dengeleyici kuralları ve araştırmalar ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7436a-154">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="7436a-155">Adlı bir NIC oluşturun *lb nıc1 olması*ve hello ile ilişkilendirmek *rdp1* NAT kuralı ve hello *beilb* arka uç adres havuzu.</span><span class="sxs-lookup"><span data-stu-id="7436a-155">Create an NIC named *lb-nic1-be*, and then associate it with hello *rdp1* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="7436a-156">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="7436a-156">Expected output:</span></span>

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

2. <span data-ttu-id="7436a-157">Adlı bir NIC oluşturun *lb nic2 olması*ve hello ile ilişkilendirmek *rdp2* NAT kuralı ve hello *beilb* arka uç adres havuzu.</span><span class="sxs-lookup"><span data-stu-id="7436a-157">Create an NIC named *lb-nic2-be*, and then associate it with hello *rdp2* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="7436a-158">Adlı bir sanal makine oluşturmak *DB1*ve hello adlı NIC ile ilişkilendirme *lb nıc1 olması*.</span><span class="sxs-lookup"><span data-stu-id="7436a-158">Create a virtual machine named *DB1*, and then associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="7436a-159">Bir depolama hesabı olarak adlandırılan *web1nrp* komutu çalıştırır aşağıdaki hello önce oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="7436a-159">A storage account called *web1nrp* is created before hello following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="7436a-160">Bir yük dengeleyici gerek toobe içinde Vm'lerde aynı kullanılabilirlik kümesinde hello.</span><span class="sxs-lookup"><span data-stu-id="7436a-160">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="7436a-161">Kullanım `azure availset create` toocreate kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="7436a-161">Use `azure availset create` toocreate an availability set.</span></span>

4. <span data-ttu-id="7436a-162">Adlı sanal makine (VM) oluşturma *DB2*ve hello adlı NIC ile ilişkilendirme *lb nic2 olması*.</span><span class="sxs-lookup"><span data-stu-id="7436a-162">Create a virtual machine (VM) named *DB2*, and then associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="7436a-163">Bir depolama hesabı olarak adlandırılan *web1nrp* komutu aşağıdaki hello çalıştırmadan önce oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7436a-163">A storage account called *web1nrp* was created before running hello following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="7436a-164">Yük dengeleyici silme</span><span class="sxs-lookup"><span data-stu-id="7436a-164">Delete a load balancer</span></span>

<span data-ttu-id="7436a-165">tooremove bir yük dengeleyici hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7436a-165">tooremove a load balancer, use hello following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="7436a-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7436a-166">Next steps</span></span>

[<span data-ttu-id="7436a-167">Kaynak IP benzeşimi kullanarak yük dengeleyici dağıtım modunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7436a-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="7436a-168">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7436a-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

