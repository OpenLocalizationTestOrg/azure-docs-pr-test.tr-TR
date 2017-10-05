---
title: "Özel IP adresleri VM'ler - Azure CLI 2.0 için yapılandırma | Microsoft Docs"
description: "Azure komut satırı arabirimi (CLI) 2.0 kullanarak sanal makineleri için özel IP adresleri yapılandırmayı öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 071156367c1f819a00d31f1d0335e301391fda81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-cli-20"></a><span data-ttu-id="8d33c-103">Azure CLI 2.0 kullanarak bir sanal makine için özel IP adreslerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="8d33c-103">Configure private IP addresses for a virtual machine using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="8d33c-104">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="8d33c-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="8d33c-105">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8d33c-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="8d33c-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md): Klasik ve kaynak yönetimi dağıtım modellerine yönelik CLI’mız</span><span class="sxs-lookup"><span data-stu-id="8d33c-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span> 
- <span data-ttu-id="8d33c-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -bizim gelecek nesil CLI kaynak yönetimi dağıtım modeli (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="8d33c-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for the resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="8d33c-108">Bu makalede Resource Manager dağıtım modeli anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8d33c-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="8d33c-109">Ayrıca [Klasik dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8d33c-109">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="8d33c-110">Aşağıdaki örnek Azure CLI 2.0 komutları önceden oluşturulmuş basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="8d33c-110">The sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="8d33c-111">Bu belgede gösterildiği komutları çalıştırmak istiyorsanız, önce açıklanan test ortamı oluşturmak [vnet oluşturma](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8d33c-111">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="8d33c-112">Bir VM oluşturulurken özel bir statik IP adresi belirtin</span><span class="sxs-lookup"><span data-stu-id="8d33c-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="8d33c-113">Adlı bir VM oluşturmak için *DNS01* içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet* özel bir statik IP *192.168.1.101*, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8d33c-113">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="8d33c-114">Henüz henüz yükleyin ve en son yapılandırırsanız [Azure CLI 2.0](/cli/azure/install-az-cli2) ve bir Azure hesabı kullanarak oturum açma [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="8d33c-114">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="8d33c-115">VM için bir genel IP oluşturun [az ağ genel IP oluşturun](/cli/azure/network/public-ip#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="8d33c-115">Create a public IP for the VM with the [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="8d33c-116">Çıktıdan sonra gösterilen listede, kullanılan parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8d33c-116">The list shown after the output explains the parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8d33c-117">İstediğiniz ya da ortamınıza bağlı olarak bu, bağımsız değişkenler için farklı değerler ve sonraki adımları kullanmak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="8d33c-117">You may want or need to use different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="8d33c-118">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="8d33c-118">Expected output:</span></span>
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * <span data-ttu-id="8d33c-119">`--resource-group`: Genel IP oluşturulacağı kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="8d33c-119">`--resource-group`: Name of the resource group in which to create the public IP.</span></span>
   * <span data-ttu-id="8d33c-120">`--name`: Genel IP adı.</span><span class="sxs-lookup"><span data-stu-id="8d33c-120">`--name`: Name of the public IP.</span></span>
   * <span data-ttu-id="8d33c-121">`--location`: Genel IP oluşturulacağı azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="8d33c-121">`--location`: Azure region in which to create the public IP.</span></span>

3. <span data-ttu-id="8d33c-122">Çalıştırma [az ağ NIC oluşturmak](/cli/azure/network/nic#create) statik özel IP ile NIC grubu oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="8d33c-122">Run the [az network nic create](/cli/azure/network/nic#create) command to create a NIC with a static private IP.</span></span> <span data-ttu-id="8d33c-123">Çıktıdan sonra gösterilen listede, kullanılan parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8d33c-123">The list shown after the output explains the parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="8d33c-124">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="8d33c-124">Expected output:</span></span>
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    <span data-ttu-id="8d33c-125">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="8d33c-125">Parameters:</span></span>

    * <span data-ttu-id="8d33c-126">`--private-ip-address`: NIC özel statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="8d33c-126">`--private-ip-address`: Static private IP address for the NIC.</span></span>
    * <span data-ttu-id="8d33c-127">`--vnet-name`: İçinde NIC oluşturulacağı Vnet'in adı</span><span class="sxs-lookup"><span data-stu-id="8d33c-127">`--vnet-name`: Name of the VNet in wihch to create the NIC.</span></span>
    * <span data-ttu-id="8d33c-128">`--subnet`: İçinde NIC oluşturulacağı alt ağın adı</span><span class="sxs-lookup"><span data-stu-id="8d33c-128">`--subnet`: Name of the subnet in which to create the NIC.</span></span>

4. <span data-ttu-id="8d33c-129">Çalıştırma [azure vm oluşturma](/cli/azure/vm/nic#create) ortak IP yukarıda oluşturduğunuz NIC ile VM oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="8d33c-129">Run the [azure vm create](/cli/azure/vm/nic#create) command to create the VM using the public IP and NIC created above.</span></span> <span data-ttu-id="8d33c-130">Çıktıdan sonra gösterilen listede, kullanılan parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8d33c-130">The list shown after the output explains the parameters used.</span></span>
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    <span data-ttu-id="8d33c-131">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="8d33c-131">Expected output:</span></span>
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   <span data-ttu-id="8d33c-132">Parametreleri temel dışında [az vm oluşturma](/cli/azure/vm#create) parametreleri.</span><span class="sxs-lookup"><span data-stu-id="8d33c-132">Parameters other than the basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="8d33c-133">`--nics`: VM bağlı olduğu NIC adı.</span><span class="sxs-lookup"><span data-stu-id="8d33c-133">`--nics`: Name of the NIC to which the VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="8d33c-134">Bir VM için özel statik IP adresi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="8d33c-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="8d33c-135">Oluşturduğunuz statik özel IP adresini görüntülemek için Azure CLI ve aşağıdaki komutu çalıştırın değerlerini gözlemlemek *özel IP ayırma yöntemi* ve *özel IP adresi*:</span><span class="sxs-lookup"><span data-stu-id="8d33c-135">To view the static private IP address that you created, run the following Azure CLI command and observe the values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="8d33c-136">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="8d33c-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="8d33c-137">NIC bu VM için belirli IP bilgilerini görüntülemek için NIC özellikle sorgu:</span><span class="sxs-lookup"><span data-stu-id="8d33c-137">To display the specific IP information of the NIC for that VM, query the NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="8d33c-138">Çıktı aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="8d33c-138">The output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="8d33c-139">Özel bir statik IP adresi bir sanal makineden kaldırın</span><span class="sxs-lookup"><span data-stu-id="8d33c-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="8d33c-140">Resource manager dağıtımları için Azure CLI içinde nıc'den özel bir statik IP adresi kaldıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="8d33c-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="8d33c-141">Yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8d33c-141">You must:</span></span>
- <span data-ttu-id="8d33c-142">Dinamik IP kullanan yeni bir NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="8d33c-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="8d33c-143">NIC VM üzerinde yeni oluşturulan NIC ayarlayın</span><span class="sxs-lookup"><span data-stu-id="8d33c-143">Set the NIC on the VM do the newly created NIC.</span></span> 

<span data-ttu-id="8d33c-144">Yukarıdaki komutlarda kullanılan VM NIC değiştirmek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="8d33c-144">To change the NIC for the VM used in the commands above, follow the steps below.</span></span>

1. <span data-ttu-id="8d33c-145">Çalıştırma **azure ağı NIC grubu oluşturmak** dinamik IP ayırma ile yeni bir IP adresi kullanarak yeni bir NIC grubu oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="8d33c-145">Run the **azure network nic create** command to create a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="8d33c-146">IP adresi belirtildiğinden ayırma yöntemi olduğuna dikkat edin **dinamik**.</span><span class="sxs-lookup"><span data-stu-id="8d33c-146">Note that because no IP address is specified, the allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="8d33c-147">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="8d33c-147">Expected output:</span></span>

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. <span data-ttu-id="8d33c-148">Çalıştırma **azure vm kümesi** VM tarafından kullanılan NIC değiştirmek için komutu.</span><span class="sxs-lookup"><span data-stu-id="8d33c-148">Run the **azure vm set** command to change the NIC used by the VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="8d33c-149">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="8d33c-149">Expected output:</span></span>
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > <span data-ttu-id="8d33c-150">VM birden çok NIC için yeterince büyük olduğundan çalıştırırsanız **azure ağı NIC silme** eski NIC silmek için</span><span class="sxs-lookup"><span data-stu-id="8d33c-150">If the VM is large enough to have more than one NIC, run the **azure network nic delete** command to delete the old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="8d33c-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8d33c-151">Next steps</span></span>
* <span data-ttu-id="8d33c-152">Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="8d33c-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="8d33c-153">Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="8d33c-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="8d33c-154">Başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="8d33c-154">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

