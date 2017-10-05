---
title: "Azure sanal makine ölçek kümeleri için ağ hizmeti | Microsoft Docs"
description: "Azure sanal makine ölçek kümeleri için yapılandırma ağ hizmeti özellikleri."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: a8520c6d8962cc362fc935f6b515a299c0ce75b3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="494b1-103">Azure sanal makine ölçek kümeleri için ağ hizmeti</span><span class="sxs-lookup"><span data-stu-id="494b1-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="494b1-104">Portal aracılığıyla Azure sanal makine ölçek kümesinin dağıtımını yaptığınızda gelen NAT kurallarıyla Azure Load Balancer gibi bazı ağ özellikleri varsayılan olarak gelir.</span><span class="sxs-lookup"><span data-stu-id="494b1-104">When you deploy an Azure virtual machine scale set through the portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="494b1-105">Bu makalede, ölçek kümeleriyle yapılandırabileceğiniz daha gelişmiş ağ özelliklerinden bazılarının nasıl kullanıldığı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="494b1-105">This article describes how to use some of the more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="494b1-106">Bu makalede ele alınan özelliklerin tümünü Azure Resource Manager şablonlarını kullanarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="494b1-106">You can configure all of the features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="494b1-107">Belirli özellikler için Azure CLI ve PowerShell örnekleri de eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="494b1-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="494b1-108">CLI 2.10 ve PowerShell 4.2.0 veya üstünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="494b1-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="494b1-109">Hızlandırılmış Ağ</span><span class="sxs-lookup"><span data-stu-id="494b1-109">Accelerated Networking</span></span>
<span data-ttu-id="494b1-110">Azure [Hızlandırılmış Ağ](../virtual-network/virtual-network-create-vm-accelerated-networking.md), sanal makineye tek kökte G/Ç sanallaştırmasına (SR-IV) olanak tanıyarak ağ performansını geliştirir.</span><span class="sxs-lookup"><span data-stu-id="494b1-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) to a virtual machine.</span></span> <span data-ttu-id="494b1-111">Ölçek kümeleriyle hızlandırılmış ağ kullanmak için, ölçek kümenizin networkInterfaceConfigurations ayarlarında enableAcceleratedNetworking değerini **true** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="494b1-111">To use accelerated networking with scale sets, set enableAcceleratedNetworking to **true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="494b1-112">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="494b1-112">For example:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="494b1-113">Mevcut Azure Load Balancer’a başvuran bir ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="494b1-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="494b1-114">Azure portalı kullanılarak ölçek kümesi oluşturulduğunda, yapılandırma seçeneklerinin çoğunda yeni bir yük dengeleyici oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="494b1-114">When a scale set is created using the Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="494b1-115">Mevcut yük dengeleyiciye başvurması gereken bir ölçek kümesi oluşturuyorsanız, bunu CLI kullanarak yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="494b1-115">If you create a scale set, which needs to reference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="494b1-116">Aşağıdaki örnek betik bir yük dengeleyici ve ardından ona başvuran bir ölçek kümesi oluşturur:</span><span class="sxs-lookup"><span data-stu-id="494b1-116">The following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="494b1-117">Yapılandırılabilir DNS Ayarları</span><span class="sxs-lookup"><span data-stu-id="494b1-117">Configurable DNS Settings</span></span>
<span data-ttu-id="494b1-118">Varsayılan olarak, ölçek kümeleri içinde oluşturuldukları VNET ve alt ağın belirli DNS ayarlarını alır.</span><span class="sxs-lookup"><span data-stu-id="494b1-118">By default, scale sets take on the specific DNS settings of the VNET and subnet they were created in.</span></span> <span data-ttu-id="494b1-119">Bununla birlikte, ölçek kümesi için DNS ayarlarını doğrudan oluşturmanız da mümkündür.</span><span class="sxs-lookup"><span data-stu-id="494b1-119">You can however, configure the DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="494b1-120">Yapılandırılabilir DNS sunucularıyla ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="494b1-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="494b1-121">CLI 2.0 kullanarak özel DNS yapılandırmasıyla bir ölçek kümesi oluşturmak için, **vmss create** komutuna sunucu ip adreslerini ayıran boşluktan sonra **--dns-servers** bağımsız değişkenini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="494b1-121">To create a scale set with a custom DNS configuration using CLI 2.0, add the **--dns-servers** argument to the **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="494b1-122">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="494b1-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="494b1-123">Azure şablonunda özel DNS sunucularını yapılandırmak için, ölçek kümesinin networkInterfaceConfigurations bölümüne bir dnsSettings özelliği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="494b1-123">To configure custom DNS servers in an Azure template, add a dnsSettings property to the scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="494b1-124">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="494b1-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="494b1-125">Yapılandırılabilir sanal makine etki alanı adlarıyla ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="494b1-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="494b1-126">CLI 2.0 kullanarak özel DNS adıyla bir ölçek kümesi oluşturmak için, **vmss create** komutuna etki alanı adını temsil eden dizeden sonra **--vm-domain-name** bağımsız değişkenini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="494b1-126">To create a scale set with a custom DNS name for virtual machines using CLI 2.0, add the **--vm-domain-name** argument to the **vmss create** command, followed by a string representing the domain name.</span></span>

<span data-ttu-id="494b1-127">Azure şablonunda etki alanı adını ayarlamak için, ölçek kümesinin **networkInterfaceConfigurations** bölümüne bir **dnsSettings** özelliği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="494b1-127">To set the domain name in an Azure template, add a **dnsSettings** property to the scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="494b1-128">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="494b1-128">For example:</span></span>

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

<span data-ttu-id="494b1-129">Tek bir sanal makine dns adı için çıkış şu biçimde olabilir:</span><span class="sxs-lookup"><span data-stu-id="494b1-129">The output, for an individual virtual machine dns name would be in the following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="494b1-130">Sanal makine başına genel IPv4</span><span class="sxs-lookup"><span data-stu-id="494b1-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="494b1-131">Genel olarak, Azure ölçek kümesi sanal makinelerinin kendi genel IP adresleri olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="494b1-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="494b1-132">Senaryoların çoğunda, bir genel IP adresini yük dengeleyiciyle veya tek bir sanal makineyle (başka bir deyişle, sıçrama kutusu) ilişkilendirmek daha ekonomik ve güvenlidir; daha sonra o da, gelen bağlantıları gerektiği gibi ölçek kümesi sanal makinelerine yönlendirir (örneğin, gelen NAT kuralları aracılığıyla).</span><span class="sxs-lookup"><span data-stu-id="494b1-132">For most scenarios, it is more economical and secure to associate a public IP address to a load balancer or to an individual virtual machine (aka a jumpbox), which then routes incoming connections to scale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="494b1-133">Öte yandan, bazı senaryolarda ölçek kümesi sanal makinelerinin kendi genel IP adresleri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="494b1-133">However, some scenarios do require scale set virtual machines to have their own public IP addresses.</span></span> <span data-ttu-id="494b1-134">Buna örnek olarak, konsolun oyunun fizik işlemlerini yapan bir bulut sanal makinesine doğrudan bağlanmasını gerektiren oyunları verebiliriz.</span><span class="sxs-lookup"><span data-stu-id="494b1-134">An example is gaming, where a console needs to make a direct connection to a cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="494b1-135">Bir diğer örnek de, dağıtılmış bir veritabanında sanal makinelerin birbiriyle dış bağlantılar kurması gerektiği durumlardır.</span><span class="sxs-lookup"><span data-stu-id="494b1-135">Another example is where virtual machines need to make external connections to one another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="494b1-136">Sanal makine başına bir genel IP ile ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="494b1-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="494b1-137">CLI 2.0 ile her sanal makineye bir genel IP adresi atayan bir ölçek kümesi oluşturmak için, **vmss create** komutuna **--public-ip-per-vm** parametresini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="494b1-137">To create a scale set that assigns a public IP address to each virtual machine with CLI 2.0, add the **--public-ip-per-vm** parameter to the **vmss create** command.</span></span> 

<span data-ttu-id="494b1-138">Azure şablonu kullanarak ölçek kümesi oluşturmak için, Microsoft.Compute/virtualMachineScaleSets kaynağı API sürümünün en az **2017-03-30** olduğundan emin olun ve ölçek kümesinin ipConfigurations bölümüne **publicIpAddressConfiguration** JSON özelliği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="494b1-138">To create a scale set using an Azure template, make sure the API version of the Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property to the scale set ipConfigurations section.</span></span> <span data-ttu-id="494b1-139">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="494b1-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="494b1-140">Örnek şablon: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="494b1-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-the-public-ip-addresses-of-the-virtual-machines-in-a-scale-set"></a><span data-ttu-id="494b1-141">Ölçek kümesinde sanal makinelerin genel IP adreslerini sorgulama</span><span class="sxs-lookup"><span data-stu-id="494b1-141">Querying the public IP addresses of the virtual machines in a scale set</span></span>
<span data-ttu-id="494b1-142">CLI 2.0 kullanarak ölçek kümesi sanal makinelerine atanmış genel IP adreslerini listelemek için, **az vmss list-instance-public-ips** komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="494b1-142">To list the public IP addresses assigned to scale set virtual machines using CLI 2.0, use the **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="494b1-143">PowerShell kullanarak ölçek kümesi genel IP adreslerini listelemek için, _Get-AzureRmPublicIpAddress_ komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="494b1-143">To list scale set public IP addresses using PowerShell, use the _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="494b1-144">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="494b1-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="494b1-145">Doğrudan genel IP adresi yapılandırmasının kaynak kimliğine başvuruda bulunarak da genel IP adreslerini sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="494b1-145">You can also query the public IP addresses by referencing the resource id of the public IP address configuration directly.</span></span> <span data-ttu-id="494b1-146">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="494b1-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="494b1-147">Ölçek kümesi sanal makinelerine atanan genel IP adreslerini, [Azure Kaynak Gezgini](https://resources.azure.com)’ni ve Azure REST API’nin **2017-03-30** veya üstü sürümlerini kullanarak da sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="494b1-147">To query the public IP addresses assigned to scale set virtual machines using the [Azure Resource Explorer](https://resources.azure.com), or the Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="494b1-148">Kaynak kümesinin genel IP adreslerini Kaynak Gezgini’ni kullanarak görüntülemek için, ölçek kümenizin altındaki **publicipaddresses** bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="494b1-148">To view public IP addresses for a scale set using the Resource Explorer, look at the **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="494b1-149">Örneğin: https://resources.azure.com/subscriptions/_sub_kimliğiniz_/resourceGroups/_rg_değeriniz_/providers/Microsoft.Compute/virtualMachineScaleSets/_vmss_değeriniz_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="494b1-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="494b1-150">Örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="494b1-150">Example output:</span></span>
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="494b1-151">NIC başına birden çok IP adresi</span><span class="sxs-lookup"><span data-stu-id="494b1-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="494b1-152">Ölçek kümesinde bir sanal makineye bağlanan her NIC ile ilişkilendirilmiş bir veya birden çok IP yapılandırması olabilir.</span><span class="sxs-lookup"><span data-stu-id="494b1-152">Every NIC attached to a VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="494b1-153">Her yapılandırma bir özel IP adresine atanır.</span><span class="sxs-lookup"><span data-stu-id="494b1-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="494b1-154">Her yapılandırmayla ilişkilendirilmiş bir genel IP adresi kaynağı da olabilir.</span><span class="sxs-lookup"><span data-stu-id="494b1-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="494b1-155">NIC’ye kaç IP adresi atanabileceğini ve Azure aboneliğinde kaç genel IP adresi kullanabileceğinizi anlamak için, [Azure sınırlarına](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) bakın.</span><span class="sxs-lookup"><span data-stu-id="494b1-155">To understand how many IP addresses can be assigned to a NIC, and how many public IP addresses you can use in an Azure subscription, refer to [Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="494b1-156">Sanal makine başına birden çok NIC</span><span class="sxs-lookup"><span data-stu-id="494b1-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="494b1-157">Sanal makinenin boyutuna bağlı olarak, sanal makine başına en çok 8 NIC’niz olabilir.</span><span class="sxs-lookup"><span data-stu-id="494b1-157">You can have up to 8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="494b1-158">Makine başına NIC sayısı üst sınırı, [Sanal makine boyutu makalesinde](../virtual-machines/windows/sizes.md) verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="494b1-158">The maximum number of NICs per machine is available in the [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="494b1-159">Aşağıdaki örnek, sanal makine başına birden çok NIC girdisi ve birden çok genel IP gösteren bir ölçek kümesi ağ profilidir:</span><span class="sxs-lookup"><span data-stu-id="494b1-159">The following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a><span data-ttu-id="494b1-160">Ölçek kümesi başına NSG</span><span class="sxs-lookup"><span data-stu-id="494b1-160">NSG per scale set</span></span>
<span data-ttu-id="494b1-161">Ağ Güvenlik Grupları, ölçek kümesi sanal makine özelliklerinin ağ arabirimi yapılandırması bölümüne bir başvuru eklemek yoluyla doğrudan ölçek kümesine uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="494b1-161">Network Security Groups can be applied directly to a scale set, by adding a reference to the network interface configuration section of the scale set virtual machine properties.</span></span>

<span data-ttu-id="494b1-162">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="494b1-162">For example:</span></span> 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a><span data-ttu-id="494b1-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="494b1-163">Next steps</span></span>
<span data-ttu-id="494b1-164">Azure sanal ağları hakkında daha fazla bilgi için, [bu belgelere](../virtual-network/virtual-networks-overview.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="494b1-164">For more information about Azure virtual networks, refer to [this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
