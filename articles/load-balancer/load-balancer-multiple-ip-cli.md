---
title: "Azure CLI kullanarak birden çok IP yapılandırmalarını Dengeleme aaaLoad | Microsoft Docs"
description: "Nasıl tooassign birden çok IP adresleri öğrenin Azure CLI kullanarak tooa sanal makine | Resource Manager."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/10/2017
ms.author: annahar
ms.openlocfilehash: df81e1b8193f274bad435d6b506c7be824117416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations"></a><span data-ttu-id="f00b3-103">Yük Dengeleme üzerinde birden fazla IP yapılandırması</span><span class="sxs-lookup"><span data-stu-id="f00b3-103">Load balancing on multiple IP configurations</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f00b3-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f00b3-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="f00b3-105">CLI</span><span class="sxs-lookup"><span data-stu-id="f00b3-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="f00b3-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f00b3-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="f00b3-107">Bu makalede, nasıl bir ikincil ağ arabirimi (NIC) toouse Azure yük dengeleyici ile birden çok IP adresleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f00b3-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="f00b3-108">Bu senaryo için Windows, her birincil ve ikincil bir NIC ile çalışan iki VM sahibiz</span><span class="sxs-lookup"><span data-stu-id="f00b3-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="f00b3-109">Her ikincil hello NIC'lerin iki IP yapılandırmaları vardır.</span><span class="sxs-lookup"><span data-stu-id="f00b3-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="f00b3-110">Her VM Web siteleri contoso.com ve fabrikam.com barındırır. İlişkili tooone hello IP yapılandırmalarının hello ikincil NIC üzerinde her Web sitesi olan</span><span class="sxs-lookup"><span data-stu-id="f00b3-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="f00b3-111">Azure yük dengeleyici tooexpose iki ön uç IP adresi, her bir Web sitesi, toodistribute trafiği toohello ilgili IP hello Web sitesinin yapılandırması için bir tane kullanırız.</span><span class="sxs-lookup"><span data-stu-id="f00b3-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="f00b3-112">Bu senaryoda hem ön uçlar yanı sıra arasında her iki arka uç havuzu IP adreslerini hello aynı bağlantı noktası numarası kullanır.</span><span class="sxs-lookup"><span data-stu-id="f00b3-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![LB senaryo görüntüsü](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="f00b3-114">Adımları tooload bakiyesi birden fazla IP yapılandırması</span><span class="sxs-lookup"><span data-stu-id="f00b3-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="f00b3-115">Bu makalede açıklanan tooachieve hello senaryo Hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f00b3-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="f00b3-116">[Hello Azure CLI yükleyip](../cli-install-nodejs.md) Azure hesabınızda hello bağlantılı makale ve günlük hello adımları izleyerek Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="f00b3-116">[Install and Configure hello Azure CLI](../cli-install-nodejs.md) hello Azure CLI by following hello steps in hello linked article and log into your Azure account.</span></span>
2. <span data-ttu-id="f00b3-117">[Bir kaynak grubu oluşturmak](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) adlı *contosofabrikam* yukarıda açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="f00b3-117">[Create a resource group](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-resource-group) called *contosofabrikam* as described above.</span></span>

    ```azurecli
    azure group create contosofabrikam westcentralus
    ```

3. <span data-ttu-id="f00b3-118">[Kullanılabilirlik kümesi oluştur](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor hello iki VM.</span><span class="sxs-lookup"><span data-stu-id="f00b3-118">[Create an availability set](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-an-availability-set) toofor hello two VMs.</span></span> <span data-ttu-id="f00b3-119">Bu senaryo için komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="f00b3-119">For this scenario, use hello following command:</span></span>

    ```azurecli
    azure availset create --resource-group contosofabrikam --location westcentralus --name myAvailabilitySet
    ```

4. <span data-ttu-id="f00b3-120">[Bir sanal ağ oluşturma](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) adlı *myVNet* ve bir alt ağ olarak adlandırılan *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="f00b3-120">[Create a virtual network](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-network-and-subnet) called *myVNet* and a subnet called *mySubnet*:</span></span>

    ```azurecli
    azure network vnet create --resource-group contosofabrikam --name myVnet --address-prefixes 10.0.0.0/16  --location westcentralus

    azure network vnet subnet create --resource-group contosofabrikam --vnet-name myVnet --name mySubnet --address-prefix 10.0.0.0/24
    ```

5. <span data-ttu-id="f00b3-121">[Merhaba yük dengeleyici oluşturma](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) adlı *mylb*:</span><span class="sxs-lookup"><span data-stu-id="f00b3-121">[Create hello load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) called *mylb*:</span></span>

    ```azurecli
    azure network lb create --resource-group contosofabrikam --location westcentralus --name mylb
    ```

6. <span data-ttu-id="f00b3-122">İki dinamik genel IP adresleri hello ön uç IP yapılandırmaları, yük dengeleyicinin oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f00b3-122">Create two dynamic public IP addresses for hello frontend IP configurations of your load balancer:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp1 --domain-name-label contoso --allocation-method Dynamic

    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name PublicIp2 --domain-name-label fabrikam --allocation-method Dynamic
    ```

7. <span data-ttu-id="f00b3-123">Merhaba iki ön uç IP yapılandırmaları oluşturma *contosofe* ve *fabrikamfe* sırasıyla:</span><span class="sxs-lookup"><span data-stu-id="f00b3-123">Create hello two frontend IP configurations, *contosofe* and *fabrikamfe* respectively:</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp1 --name contosofe
    azure network lb frontend-ip create --resource-group contosofabrikam --lb-name mylb --public-ip-name PublicIp2 --name fabrkamfe
    ```

8. <span data-ttu-id="f00b3-124">Arka uç adres havuzları - oluşturma *contosopool* ve *fabrikampool*, [araştırma](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*ve yükleme Dengeleme kuralları - *HTTPc* ve *HTTPf*:</span><span class="sxs-lookup"><span data-stu-id="f00b3-124">Create your backend address pools - *contosopool* and *fabrikampool*, a [probe](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) - *HTTP*, and your load balancing rules - *HTTPc* and *HTTPf*:</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name contosopool
    azure network lb address-pool create --resource-group contosofabrikam --lb-name mylb --name fabrikampool

    azure network lb probe create --resource-group contosofabrikam --lb-name mylb --name HTTP --protocol "http" --interval 15 --count 2 --path index.html

    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPc --protocol tcp --probe-name http--frontend-port 5000 --backend-port 5000 --frontend-ip-name contosofe --backend-address-pool-name contosopool
    azure network lb rule create --resource-group contosofabrikam --lb-name mylb --name HTTPf --protocol tcp --probe-name http --frontend-port 5000 --backend-port 5000 --frontend-ip-name fabrkamfe --backend-address-pool-name fabrikampool
    ```

9. <span data-ttu-id="f00b3-125">Çalışma hello aşağıdakileri aşağıda komut ve hello çıktısını çok denetleyin[, yük dengeleyici doğrulayın](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) doğru bir şekilde oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="f00b3-125">Run hello following command below and then check hello output too[verify your load balancer](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json) was created correctly:</span></span>

    ```azurecli
    azure network lb show --resource-group contosofabrikam --name mylb
    ```

10. <span data-ttu-id="f00b3-126">[Genel IP oluşturun](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, ve [depolama hesabı](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* ilk sanal makineniz aşağıda gösterildiği gibi VM1 için:</span><span class="sxs-lookup"><span data-stu-id="f00b3-126">[Create a public IP](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-public-ip-address), *myPublicIp*, and [storage account](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json), *mystorageaccont1* for your first virtual machine VM1 as shown below:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP --domain-name-label mypublicdns345 --allocation-method Dynamic

    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount1
    ```

11. <span data-ttu-id="f00b3-127">[Ağ arabirimleri Hello oluşturma](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) VM1 için ve ikinci bir IP yapılandırmasına ekleyin *VM1 ipconfig2*, ve [hello VM oluşturma](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="f00b3-127">[Create hello network interfaces](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-a-virtual-nic) for VM1 and add a second IP configuration, *VM1-ipconfig2*, and [create hello VM](../virtual-machines/linux/create-cli-complete.md?toc=%2fazure%2fvirtual-network%2ftoc.json#create-the-linux-vms) as shown below:</span></span>

    ```azurecli
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic1 --ip-config-name NIC1-ipconfig1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM1Nic2 --ip-config-name VM1-ipconfig1 --public-ip-name myPublicIP --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM1Nic2 --name VM1-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM1 --location westcentralus --os-type linux --nic-names VM1Nic1,VM1Nic2  --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount1 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

12. <span data-ttu-id="f00b3-128">Adımları 10-11 ikinci VM için yineleyin:</span><span class="sxs-lookup"><span data-stu-id="f00b3-128">Repeat steps 10-11 for your second VM:</span></span>

    ```azurecli
    azure network public-ip create --resource-group contosofabrikam --location westcentralus --name myPublicIP2 --domain-name-label mypublicdns785 --allocation-method Dynamic
    azure storage account create --location westcentralus --resource-group contosofabrikam --kind Storage --sku-name GRS mystorageaccount2
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic1
    azure network nic create --resource-group contosofabrikam --location westcentralus --subnet-vnet-name myVnet --subnet-name mySubnet --name VM2Nic2 --ip-config-name VM2-ipconfig1 --public-ip-name myPublicIP2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/contosopool"
    azure network nic ip-config create --resource-group contosofabrikam --nic-name VM2Nic2 --name VM2-ipconfig2 --lb-address-pool-ids "/subscriptions/<your subscription ID>/resourceGroups/contosofabrikam/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/fabrikampool"
    azure vm create --resource-group contosofabrikam --name VM2 --location westcentralus --os-type linux --nic-names VM2Nic1,VM2Nic2 --vnet-name VNet1 --vnet-subnet-name Subnet1 --availset-name myAvailabilitySet --vm-size Standard_DS3_v2 --storage-account-name mystorageaccount2 --image-urn canonical:UbuntuServer:16.04.0-LTS:latest --admin-username <your username>  --admin-password <your password>
    ```

13. <span data-ttu-id="f00b3-129">Son olarak, DNS kaynak kayıtlarını toopoint toohello ilgili ön uç IP adresi hello yük dengeleyici için yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f00b3-129">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="f00b3-130">Azure DNS'de etki alanlarınızı barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="f00b3-130">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="f00b3-131">Azure DNS yük dengeleyici ile kullanma hakkında daha fazla bilgi için bkz: [kullanarak Azure DNS diğer Azure hizmetleriyle](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="f00b3-131">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f00b3-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f00b3-132">Next steps</span></span>
- <span data-ttu-id="f00b3-133">Nasıl toocombine Yük Dengeleme Azure hizmetleri hakkında daha fazla bilgi [Azure'da Yük Dengeleme hizmetlerini kullanarak](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="f00b3-133">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="f00b3-134">Nasıl günlükleri farklı türlerde içinde Azure toomanage kullanın ve yük dengeleyici sorun giderme öğrenin [analytics Azure yük dengeleyici için oturum](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="f00b3-134">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
