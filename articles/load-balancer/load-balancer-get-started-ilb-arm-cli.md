---
title: "İç yük dengeleyicisi oluşturma - Azure CLI | Microsoft Docs"
description: "Azure CLI kullanarak Resource Manager’da iç yük dengeleyici oluşturmayı öğrenin"
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
ms.openlocfilehash: 128b91c685b5f7e494a69ca5b04165a0ee7cbb78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-by-using-the-azure-cli"></a><span data-ttu-id="9cc57-103">Azure CLI kullanarak iç yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cc57-103">Create an internal load balancer by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9cc57-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9cc57-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="9cc57-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9cc57-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="9cc57-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9cc57-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="9cc57-107">Şablon</span><span class="sxs-lookup"><span data-stu-id="9cc57-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="9cc57-108">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9cc57-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="9cc57-109">Bu makale, Microsoft’un çoğu yeni dağıtım için [klasik dağıtım modeli](load-balancer-get-started-ilb-classic-cli.md) yerine önerdiği Resource Manager dağıtım modelini açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="9cc57-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-solution-by-using-the-azure-cli"></a><span data-ttu-id="9cc57-110">Çözümü Azure CLI kullanarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="9cc57-110">Deploy the solution by using the Azure CLI</span></span>

<span data-ttu-id="9cc57-111">Aşağıda Azure Resource Manager ve CLI kullanarak İnternet’e yönelik yük dengeleyici oluşturma adımları yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="9cc57-111">The following steps show how to create an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="9cc57-112">Azure Resource Manager ile her bir kaynak ayrı ayrı oluşturulup yapılandırıldıktan sonra kaynak oluşturmak için bir araya getirilir.</span><span class="sxs-lookup"><span data-stu-id="9cc57-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="9cc57-113">Yük dengeleyici dağıtmak için aşağıdaki nesneleri oluşturmanız ve yapılandırmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9cc57-113">You need to create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="9cc57-114">**Ön uç IP yapılandırması**: Gelen ağ trafiği için genel IP adreslerini içerir</span><span class="sxs-lookup"><span data-stu-id="9cc57-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="9cc57-115">**Arka uç adres havuzu**: Sanal makinelerin yük dengeleyiciden ağ trafiği almasını sağlayan ağ arabirimlerini (NIC’ler) içerir</span><span class="sxs-lookup"><span data-stu-id="9cc57-115">**Back-end address pool**: contains network interfaces (NICs) that enable the virtual machines to receive network traffic from the load balancer</span></span>
* <span data-ttu-id="9cc57-116">**Yük dengeleme kuralları**: Yük dengeleyici üzerindeki bir genel bağlantı noktasını arka uç adres havuzundaki bağlantı noktasına eşleyen kuralları içerir</span><span class="sxs-lookup"><span data-stu-id="9cc57-116">**Load-balancing rules**: contains rules that map a public port on the load balancer to port in the back-end address pool</span></span>
* <span data-ttu-id="9cc57-117">**Gelen NAT kuralları**: Yük dengeleyici üzerindeki bir genel bağlantı noktasını arka uç adres havuzundaki belirli bir sanal makineye ait bağlantı noktasına eşleyen kuralları içerir</span><span class="sxs-lookup"><span data-stu-id="9cc57-117">**Inbound NAT rules**: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool</span></span>
* <span data-ttu-id="9cc57-118">**Araştırmalar**: Arka uç adres havuzundaki sanal makine örneklerinin kullanılabilirliğini kontrol etmek için kullanılan sistem durumu araştırmalarını içerir</span><span class="sxs-lookup"><span data-stu-id="9cc57-118">**Probes**: contains health probes that are used to check the availability of virtual machines instances in the back-end address pool</span></span>

<span data-ttu-id="9cc57-119">Daha fazla bilgi için bkz. [Yük Dengeleyici için Azure Resource Manager desteği](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9cc57-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-to-use-resource-manager"></a><span data-ttu-id="9cc57-120">CLI’yi Resource Manager’ı kullanacak şekilde ayarlama</span><span class="sxs-lookup"><span data-stu-id="9cc57-120">Set up CLI to use Resource Manager</span></span>

1. <span data-ttu-id="9cc57-121">Hiç Azure CLI kullanmadıysanız bkz. [Azure CLI hizmetini yükleme ve yapılandırma](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9cc57-121">If you have never used Azure CLI, see [Install and configure the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="9cc57-122">Talimatları Azure hesabı ve abonelik seçme adımına kadar uygulayın.</span><span class="sxs-lookup"><span data-stu-id="9cc57-122">Follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="9cc57-123">Resource Manager moduna geçmek için **azure config mode** komutunu aşağıdaki gibi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9cc57-123">Run the **azure config mode** command to switch to Resource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="9cc57-124">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="9cc57-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="9cc57-125">Adım adım iç yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cc57-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="9cc57-126">Azure'da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9cc57-126">Sign in to Azure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="9cc57-127">İstendiğinde Azure kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="9cc57-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="9cc57-128">Komut araçlarını Azure Resource Manager moduna alın.</span><span class="sxs-lookup"><span data-stu-id="9cc57-128">Change the command tools to Azure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="9cc57-129">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cc57-129">Create a resource group</span></span>

<span data-ttu-id="9cc57-130">Azure Resource Manager’daki tüm kaynaklar bir kaynak grubuyla ilişkilendirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9cc57-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="9cc57-131">Henüz yapmadıysanız, bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cc57-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="9cc57-132">İç yük dengeleyici kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cc57-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="9cc57-133">İç yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cc57-133">Create an internal load balancer</span></span>

    <span data-ttu-id="9cc57-134">Aşağıdaki senaryoda Doğu ABD bölgesinde nrprg adlı bir kaynak grubu oluşturulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9cc57-134">In the following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="9cc57-135">Sanal ağlar ve sanal ağ alt ağları gibi tüm iç yük dengeleyici kaynaklarının aynı kaynak grubunda ve aynı bölgede olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9cc57-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in the same resource group and in the same region.</span></span>

2. <span data-ttu-id="9cc57-136">İç yük dengeleyici için ön uç IP adresi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cc57-136">Create a front-end IP address for the internal load balancer.</span></span>

    <span data-ttu-id="9cc57-137">Kullandığınız IP adresi sanal ağınızla aynı alt ağ aralığında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9cc57-137">The IP address that you use must be within the subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="9cc57-138">Arka uç adres havuzunu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cc57-138">Create the back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="9cc57-139">Ön uç IP adresi ve arka uç adres havuzu tanımladıktan sonra yük dengeleyici kurallarını, gelen NAT kurallarını ve özel sistem durumu araştırmalarını oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9cc57-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="9cc57-140">İç yük dengeleyici için yük dengeleyici kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cc57-140">Create a load balancer rule for the internal load balancer.</span></span>

    <span data-ttu-id="9cc57-141">Önceki adımları uyguladığınızda verilen komut ön uç havuzunun 1433 numaralı bağlantı noktasında dinleme yapan ve yük dengelenmiş ağ trafiğini yine 1433 numaralı bağlantı noktasını kullanarak arka uç adres havuzuna gönderen bir yük dengeleyici kuralı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9cc57-141">When you follow the previous steps, the command creates a load-balancer rule for listening to port 1433 in the front-end pool and sending load-balanced network traffic to the back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="9cc57-142">Gelen NAT kurallarını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cc57-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="9cc57-143">Gelen NAT kuralları, yük dengeleyicide belirli bir sanal makine örneğine giden uç noktaları oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9cc57-143">Inbound NAT rules are used to create endpoints in a load balancer that go to a specific virtual machine instance.</span></span> <span data-ttu-id="9cc57-144">Önceki adımlarda uzak masaüstü için iki NAT kuralı oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="9cc57-144">The previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="9cc57-145">Yük dengeleyici için sistem durumu araştırmaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9cc57-145">Create health probes for the load balancer.</span></span>

    <span data-ttu-id="9cc57-146">Sistem durumu araştırması tüm sanal makine örneklerini denetleyerek ağ trafiği gönderdiklerinden emin olur.</span><span class="sxs-lookup"><span data-stu-id="9cc57-146">A health probe checks all virtual machine instances to make sure they can send network traffic.</span></span> <span data-ttu-id="9cc57-147">Sistem durumu denetimi başarısız olan sanal makine örnekleri tekrar çevrimiçi olana ve sistem durumu denetimi iyi olduğuna karar verene kadar yük dengeleyiciden kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="9cc57-147">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="9cc57-148">Microsoft Azure platformu, farklı yönetim senaryoları için genel olarak yönlendirilebilen statik bir IPv4 adresi kullanır.</span><span class="sxs-lookup"><span data-stu-id="9cc57-148">The Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="9cc57-149">IP adresi: 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="9cc57-149">The IP address is 168.63.129.16.</span></span> <span data-ttu-id="9cc57-150">Bu IP adresinin güvenlik duvarları tarafından engellenmesi beklenmeyen davranışlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="9cc57-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="9cc57-151">Azure iç yük dengeleme açısından bu IP adresi, araştırmaların yük dengeleyiciden izlenerek yük dengeli kümede yer alan sanal makinelerin durumunun belirlenmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="9cc57-151">With respect to Azure internal load balancing, this IP address is used by monitoring probes from the load balancer to determine the health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="9cc57-152">Bir iç yük dengeli kümedeki Azure sanal makinelerine gelen trafiği kısıtlamak için bir ağ güvenlik grubu kullanılması veya sanal alt ağ uygulanması halinde 168.63.129.16 adresinden gelen trafiğe izin verecek şekilde bir ağ güvenlik kuralının uygulandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="9cc57-152">If a network security group is used to restrict traffic to Azure virtual machines in an internally load-balanced set or is applied to a virtual network subnet, ensure that a network security rule is added to allow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="9cc57-153">NIC’leri oluşturma</span><span class="sxs-lookup"><span data-stu-id="9cc57-153">Create NICs</span></span>

<span data-ttu-id="9cc57-154">NIC’ler oluşturmanız (veya var olanları düzenlemeniz) ve bunları NAT kuralları, yük dengeleyici kuralları ve araştırmalarla ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9cc57-154">You need to create NICs (or modify existing ones) and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="9cc57-155">*lb-nic1-be* adlı bir NIC oluşturup *rdp1* NAT kuralı ve *beilb* arka uç adres havuzuyla ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="9cc57-155">Create an NIC named *lb-nic1-be*, and then associate it with the *rdp1* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="9cc57-156">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="9cc57-156">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up the network interface "lb-nic1-be"
        + Looking up the subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up the network interface "lb-nic1-be"
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

2. <span data-ttu-id="9cc57-157">*lb-nic2-be* adlı bir NIC oluşturup *rdp2* NAT kuralı ve *beilb* arka uç adres havuzuyla ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="9cc57-157">Create an NIC named *lb-nic2-be*, and then associate it with the *rdp2* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="9cc57-158">*DB1* adlı bir sanal makine oluşturun ve *lb-nic1-be* adlı NIC ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="9cc57-158">Create a virtual machine named *DB1*, and then associate it with the NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="9cc57-159">Önceden aşağıdaki komutla *web1nrp* adlı bir depolama hesabı oluşturulmuştu:</span><span class="sxs-lookup"><span data-stu-id="9cc57-159">A storage account called *web1nrp* is created before the following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="9cc57-160">Bir yük dengeleyiciye ait VM’lerin aynı kullanılabilirlik kümesinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9cc57-160">VMs in a load balancer need to be in the same availability set.</span></span> <span data-ttu-id="9cc57-161">Kullanılabilirlik kümesi oluşturmak için `azure availset create` kullanın.</span><span class="sxs-lookup"><span data-stu-id="9cc57-161">Use `azure availset create` to create an availability set.</span></span>

4. <span data-ttu-id="9cc57-162">*DB2* adlı bir sanal makine (VM) oluşturun ve *lb-nic2-be* adlı NIC ile ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="9cc57-162">Create a virtual machine (VM) named *DB2*, and then associate it with the NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="9cc57-163">Önceden aşağıdaki komutla *web1nrp* adlı bir depolama hesabı oluşturulmuştu.</span><span class="sxs-lookup"><span data-stu-id="9cc57-163">A storage account called *web1nrp* was created before running the following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="9cc57-164">Yük dengeleyici silme</span><span class="sxs-lookup"><span data-stu-id="9cc57-164">Delete a load balancer</span></span>

<span data-ttu-id="9cc57-165">Bir yük dengeleyiciyi kaldırmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="9cc57-165">To remove a load balancer, use the following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="9cc57-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9cc57-166">Next steps</span></span>

[<span data-ttu-id="9cc57-167">Kaynak IP benzeşimi kullanarak yük dengeleyici dağıtım modunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9cc57-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="9cc57-168">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9cc57-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

