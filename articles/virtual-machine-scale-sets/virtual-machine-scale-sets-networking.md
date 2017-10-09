---
title: "Azure sanal makine ölçek kümeleri için aaaNetworking | Microsoft Docs"
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
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a><span data-ttu-id="fe3f8-103">Azure sanal makine ölçek kümeleri için ağ hizmeti</span><span class="sxs-lookup"><span data-stu-id="fe3f8-103">Networking for Azure virtual machine scale sets</span></span>

<span data-ttu-id="fe3f8-104">Bir Azure sanal makinesi ölçeği hello Portalı aracılığıyla Ayarla dağıttığınızda, belirli ağ özellikleri olarak ayarlanır, örneğin olan bir Azure yük dengeleyici gelen NAT kuralları.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-104">When you deploy an Azure virtual machine scale set through hello portal, certain network properties are defaulted, for example an Azure Load Balancer with inbound NAT rules.</span></span> <span data-ttu-id="fe3f8-105">Bu makalede nasıl toouse hello bazıları ölçekli yapılandırabilirsiniz ağ özellikleri daha gelişmiş ayarlar açıklanır.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-105">This article describes how toouse some of hello more advanced networking features that you can configure with scale sets.</span></span>

<span data-ttu-id="fe3f8-106">Tüm Azure Resource Manager şablonları kullanarak bu makalede ele alınan hello özelliklerini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-106">You can configure all of hello features covered in this article using Azure Resource Manager templates.</span></span> <span data-ttu-id="fe3f8-107">Belirli özellikler için Azure CLI ve PowerShell örnekleri de eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-107">Azure CLI and PowerShell examples are also included for selected features.</span></span> <span data-ttu-id="fe3f8-108">CLI 2.10 ve PowerShell 4.2.0 veya üstünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-108">Use CLI 2.10, and PowerShell 4.2.0 or later.</span></span>

## <a name="accelerated-networking"></a><span data-ttu-id="fe3f8-109">Hızlandırılmış Ağ</span><span class="sxs-lookup"><span data-stu-id="fe3f8-109">Accelerated Networking</span></span>
<span data-ttu-id="fe3f8-110">Azure [hızlandırılmış ağ](../virtual-network/virtual-network-create-vm-accelerated-networking.md) tek köklü g/ç Sanallaştırması (SR-IOV) tooa sanal makine etkinleştirerek ağ performansını artırır.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-110">Azure [Accelerated Networking](../virtual-network/virtual-network-create-vm-accelerated-networking.md) improves  network performance by enabling single root I/O virtualization (SR-IOV) tooa virtual machine.</span></span> <span data-ttu-id="fe3f8-111">toouse hızlandırılmış ölçek kümeleri ile ağ, enableAcceleratedNetworking çok ayarlamak**true** ölçek kümesinin Networkınterfaceconfiguration Ayarları'nda.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-111">toouse accelerated networking with scale sets, set enableAcceleratedNetworking too**true** in your scale set's networkInterfaceConfigurations settings.</span></span> <span data-ttu-id="fe3f8-112">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fe3f8-112">For example:</span></span>
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

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a><span data-ttu-id="fe3f8-113">Mevcut Azure Load Balancer’a başvuran bir ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe3f8-113">Create a scale set that references an existing Azure Load Balancer</span></span>
<span data-ttu-id="fe3f8-114">Ölçek kümesini hello Azure portal kullanarak oluşturulduğunda, yeni bir yük dengeleyici çoğu yapılandırma seçenekleri için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-114">When a scale set is created using hello Azure portal, a new load balancer is created for most configuration options.</span></span> <span data-ttu-id="fe3f8-115">Var olan bir yük dengeleyici tooreference gereken bir ölçek kümesi oluşturursanız, CLI kullanarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-115">If you create a scale set, which needs tooreference an existing load balancer, you can do this using CLI.</span></span> <span data-ttu-id="fe3f8-116">Aşağıdaki örnek komut dosyası hello bir yük dengeleyici ve başvurduğu bir ölçek kümesi oluşturur:</span><span class="sxs-lookup"><span data-stu-id="fe3f8-116">hello following example script creates a load balancer and then creates a scale set, which references it:</span></span>
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a><span data-ttu-id="fe3f8-117">Yapılandırılabilir DNS Ayarları</span><span class="sxs-lookup"><span data-stu-id="fe3f8-117">Configurable DNS Settings</span></span>
<span data-ttu-id="fe3f8-118">Varsayılan olarak, Ölçek kümeleri hello belirli DNS ayarlarını oluşturuldukları hello VNET ve alt ağ üzerinde yapın.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-118">By default, scale sets take on hello specific DNS settings of hello VNET and subnet they were created in.</span></span> <span data-ttu-id="fe3f8-119">Ancak, ölçeği doğrudan Ayarla için hello DNS ayarlarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-119">You can however, configure hello DNS settings for a scale set directly.</span></span>
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a><span data-ttu-id="fe3f8-120">Yapılandırılabilir DNS sunucularıyla ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe3f8-120">Creating a scale set with configurable DNS servers</span></span>
<span data-ttu-id="fe3f8-121">bir ölçek kümesi CLI 2.0 kullanan bir özel DNS yapılandırması ile toocreate eklemek hello **--dns sunucuları** bağımsız değişkeni toohello **vmss oluşturma** boşluk bırakarak komutu, sunucu IP adreslerini ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-121">toocreate a scale set with a custom DNS configuration using CLI 2.0, add hello **--dns-servers** argument toohello **vmss create** command, followed by space separated server ip addresses.</span></span> <span data-ttu-id="fe3f8-122">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fe3f8-122">For example:</span></span>
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
<span data-ttu-id="fe3f8-123">bir Azure şablonu tooconfigure özel DNS sunucuları ekleme Networkınterfaceconfiguration bölüm bir dnsSettings özelliği toohello ölçek kümesi.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-123">tooconfigure custom DNS servers in an Azure template, add a dnsSettings property toohello scale set networkInterfaceConfigurations section.</span></span> <span data-ttu-id="fe3f8-124">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fe3f8-124">For example:</span></span>
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a><span data-ttu-id="fe3f8-125">Yapılandırılabilir sanal makine etki alanı adlarıyla ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe3f8-125">Creating a scale set with configurable virtual machine domain names</span></span>
<span data-ttu-id="fe3f8-126">bir ölçek kümesi CLI 2.0 kullanarak sanal makineleri için özel bir DNS adı ile toocreate eklemek hello **--vm etki alanı adı** bağımsız değişkeni toohello **vmss oluşturma** hello etki alanı adını temsil eden bir dize tarafından izlenen komutu.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-126">toocreate a scale set with a custom DNS name for virtual machines using CLI 2.0, add hello **--vm-domain-name** argument toohello **vmss create** command, followed by a string representing hello domain name.</span></span>

<span data-ttu-id="fe3f8-127">bir Azure şablonu tooset hello etki alanı adını eklemek bir **dnsSettings** özellik toohello ölçek kümesi **Networkınterfaceconfiguration** bölümü.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-127">tooset hello domain name in an Azure template, add a **dnsSettings** property toohello scale set **networkInterfaceConfigurations** section.</span></span> <span data-ttu-id="fe3f8-128">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fe3f8-128">For example:</span></span>

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

<span data-ttu-id="fe3f8-129">bir sanal makinenin dns adı için Hello çıkış form aşağıdaki hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="fe3f8-129">hello output, for an individual virtual machine dns name would be in hello following form:</span></span> 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a><span data-ttu-id="fe3f8-130">Sanal makine başına genel IPv4</span><span class="sxs-lookup"><span data-stu-id="fe3f8-130">Public IPv4 per virtual machine</span></span>
<span data-ttu-id="fe3f8-131">Genel olarak, Azure ölçek kümesi sanal makinelerinin kendi genel IP adresleri olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-131">In general, Azure scale set virtual machines do not require their own public IP addresses.</span></span> <span data-ttu-id="fe3f8-132">Çoğu senaryoda, olmasından daha ekonomik ve güvenli tooassociate bir ortak IP adresi tooa yük dengeleyici veya tooan tek tek sanal, ardından gelen bağlantıları tooscale kümesi sanal makineleri (örneğin, aracılığıyla gerektiğinde yönlendiren makine (diğer adıyla bir jumpbox), gelen NAT kuralları).</span><span class="sxs-lookup"><span data-stu-id="fe3f8-132">For most scenarios, it is more economical and secure tooassociate a public IP address tooa load balancer or tooan individual virtual machine (aka a jumpbox), which then routes incoming connections tooscale set virtual machines as needed (for example, through inbound NAT rules).</span></span>

<span data-ttu-id="fe3f8-133">Ancak, bazı senaryolar ölçek kümesi sanal makineleri toohave kendi ortak IP gerektiren adresleri.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-133">However, some scenarios do require scale set virtual machines toohave their own public IP addresses.</span></span> <span data-ttu-id="fe3f8-134">Bir örnek oyun, burada bir konsol toomake doğrudan bağlantı tooa bulut sanal hangi oyun fizik işlem yaptığını makine gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-134">An example is gaming, where a console needs toomake a direct connection tooa cloud virtual machine, which is doing game physics processing.</span></span> <span data-ttu-id="fe3f8-135">Sanal makineler toomake dış bağlantıları tooone gereken yeri başka bir örnektir başka bölgelere dağıtılan bir veritabanı içinde.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-135">Another example is where virtual machines need toomake external connections tooone another across regions in a distributed database.</span></span>

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a><span data-ttu-id="fe3f8-136">Sanal makine başına bir genel IP ile ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe3f8-136">Creating a scale set with public IP per virtual machine</span></span>
<span data-ttu-id="fe3f8-137">toocreate ortak IP adresi tooeach sahip bir sanal makine CLI 2.0 atar ölçek kümesi ekleme hello **--vm başına ortak IP** parametresi toohello **vmss oluşturma** komutu.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-137">toocreate a scale set that assigns a public IP address tooeach virtual machine with CLI 2.0, add hello **--public-ip-per-vm** parameter toohello **vmss create** command.</span></span> 

<span data-ttu-id="fe3f8-138">bir Azure şablonu kullanarak bir ölçek toocreate hello Microsoft.Compute/virtualMachineScaleSets kaynak hello API sürümü en az olduğundan emin olun **2017-03-30**ve ekleme bir **publicIpAddressConfiguration**JSON özellik toohello ölçek kümesi Ipconfigurations bölümü.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-138">toocreate a scale set using an Azure template, make sure hello API version of hello Microsoft.Compute/virtualMachineScaleSets resource is at least **2017-03-30**, and add a **publicIpAddressConfiguration** JSON property toohello scale set ipConfigurations section.</span></span> <span data-ttu-id="fe3f8-139">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fe3f8-139">For example:</span></span>

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
<span data-ttu-id="fe3f8-140">Örnek şablon: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span><span class="sxs-lookup"><span data-stu-id="fe3f8-140">Example template: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)</span></span>

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a><span data-ttu-id="fe3f8-141">Merhaba sanal makinelerin bir ölçek adreslerini kümesini Hello genel IP sorgulama</span><span class="sxs-lookup"><span data-stu-id="fe3f8-141">Querying hello public IP addresses of hello virtual machines in a scale set</span></span>
<span data-ttu-id="fe3f8-142">CLI 2.0 kullanarak kümesi sanal makineleri atanmış tooscale toolist hello ortak IP adresleri, hello kullan **az vmss listesi-örnek-genel-IP'leri** komutu.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-142">toolist hello public IP addresses assigned tooscale set virtual machines using CLI 2.0, use hello **az vmss list-instance-public-ips** command.</span></span>

<span data-ttu-id="fe3f8-143">toolist ölçek kümesi PowerShell kullanarak genel IP adresleri, hello kullan _Get-AzureRmPublicIpAddress_ komutu.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-143">toolist scale set public IP addresses using PowerShell, use hello _Get-AzureRmPublicIpAddress_ command.</span></span> <span data-ttu-id="fe3f8-144">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fe3f8-144">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

<span data-ttu-id="fe3f8-145">Sorgu hello genel IP adresleri ayrıca hello ortak IP adresi yapılandırması hello kaynak kimliği doğrudan başvurarak erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-145">You can also query hello public IP addresses by referencing hello resource id of hello public IP address configuration directly.</span></span> <span data-ttu-id="fe3f8-146">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fe3f8-146">For example:</span></span>
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

<span data-ttu-id="fe3f8-147">atanmış tooscale tooquery hello ortak IP adresleri hello kullanarak kümesi sanal makineleri [Azure kaynak Gezgini](https://resources.azure.com), ya da Azure REST API sürümü ile Merhaba **2017-03-30** ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-147">tooquery hello public IP addresses assigned tooscale set virtual machines using hello [Azure Resource Explorer](https://resources.azure.com), or hello Azure REST API with version **2017-03-30** or higher.</span></span>

<span data-ttu-id="fe3f8-148">tooview genel IP adresleri hello kaynak Gezgini, kullanılarak ayarlanan bir ölçek için konum hello **publicıpaddresses** bölümü, Ölçek kümesi altında.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-148">tooview public IP addresses for a scale set using hello Resource Explorer, look at hello **publicipaddresses** section under your scale set.</span></span> <span data-ttu-id="fe3f8-149">Örneğin: https://resources.azure.com/subscriptions/_sub_kimliğiniz_/resourceGroups/_rg_değeriniz_/providers/Microsoft.Compute/virtualMachineScaleSets/_vmss_değeriniz_/publicipaddresses</span><span class="sxs-lookup"><span data-stu-id="fe3f8-149">For example: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses</span></span>

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

<span data-ttu-id="fe3f8-150">Örnek çıktı:</span><span class="sxs-lookup"><span data-stu-id="fe3f8-150">Example output:</span></span>
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

## <a name="multiple-ip-addresses-per-nic"></a><span data-ttu-id="fe3f8-151">NIC başına birden çok IP adresi</span><span class="sxs-lookup"><span data-stu-id="fe3f8-151">Multiple IP addresses per NIC</span></span>
<span data-ttu-id="fe3f8-152">Her NIC VM ölçek kümesindeki kendisiyle ilişkili bir veya daha fazla IP yapılandırmaları olabilir tooa bağlı.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-152">Every NIC attached tooa VM in a scale set can have one or more IP configurations associated with it.</span></span> <span data-ttu-id="fe3f8-153">Her yapılandırma bir özel IP adresine atanır.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-153">Each configuration is assigned one private IP address.</span></span> <span data-ttu-id="fe3f8-154">Her yapılandırmayla ilişkilendirilmiş bir genel IP adresi kaynağı da olabilir.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-154">Each configuration may also have one public IP address resource associated with it.</span></span> <span data-ttu-id="fe3f8-155">kaç tane IP adresleri toounderstand tooa NIC, atanacağını ve bir Azure aboneliği kullanabileceğiniz kaç genel IP adresleri başvuruda çok[Azure sınırları](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span><span class="sxs-lookup"><span data-stu-id="fe3f8-155">toounderstand how many IP addresses can be assigned tooa NIC, and how many public IP addresses you can use in an Azure subscription, refer too[Azure limits](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).</span></span>

## <a name="multiple-nics-per-virtual-machine"></a><span data-ttu-id="fe3f8-156">Sanal makine başına birden çok NIC</span><span class="sxs-lookup"><span data-stu-id="fe3f8-156">Multiple NICs per virtual machine</span></span>
<span data-ttu-id="fe3f8-157">Makine boyutuna bağlı olarak sanal makine başına too8 NIC'ler yukarı sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-157">You can have up too8 NICs per virtual machine, depending on machine size.</span></span> <span data-ttu-id="fe3f8-158">Merhaba en fazla sayıda NIC makine başına hello kullanılabilir [VM boyutu makale](../virtual-machines/windows/sizes.md).</span><span class="sxs-lookup"><span data-stu-id="fe3f8-158">hello maximum number of NICs per machine is available in hello [VM size article](../virtual-machines/windows/sizes.md).</span></span> <span data-ttu-id="fe3f8-159">Merhaba aşağıdaki ağ profili birden çok NIC girişleri ve sanal makine başına birden çok ortak IP gösteren bir ölçek kümesi örneğidir:</span><span class="sxs-lookup"><span data-stu-id="fe3f8-159">hello following example is a scale set network profile showing multiple NIC entries, and multiple public IPs per virtual machine:</span></span>
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

## <a name="nsg-per-scale-set"></a><span data-ttu-id="fe3f8-160">Ölçek kümesi başına NSG</span><span class="sxs-lookup"><span data-stu-id="fe3f8-160">NSG per scale set</span></span>
<span data-ttu-id="fe3f8-161">Tooa ölçek kümesi, bir başvuru toohello ağ arabirimi yapılandırması bölümü hello ölçeğin ekleyerek sanal makine özelliklerini ayarla doğrudan ağ güvenlik grupları uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="fe3f8-161">Network Security Groups can be applied directly tooa scale set, by adding a reference toohello network interface configuration section of hello scale set virtual machine properties.</span></span>

<span data-ttu-id="fe3f8-162">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fe3f8-162">For example:</span></span> 
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

## <a name="next-steps"></a><span data-ttu-id="fe3f8-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fe3f8-163">Next steps</span></span>
<span data-ttu-id="fe3f8-164">Azure sanal ağlar hakkında daha fazla bilgi için çok başvurun[bu belgeleri](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fe3f8-164">For more information about Azure virtual networks, refer too[this documentation](../virtual-network/virtual-networks-overview.md).</span></span>
