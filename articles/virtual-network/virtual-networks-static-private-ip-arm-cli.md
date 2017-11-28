---
title: "aaaConfigure özel IP adresleri VM'ler - Azure CLI 2.0 için | Microsoft Docs"
description: "Nasıl tooconfigure özel IP adresleri kullanarak sanal makineleri için Azure komut satırı arabirimi (CLI) 2.0 hello öğrenin."
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
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a><span data-ttu-id="ebc0d-103">Hello Azure CLI 2.0 kullanarak bir sanal makine için özel IP adreslerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ebc0d-103">Configure private IP addresses for a virtual machine using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="ebc0d-104">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="ebc0d-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="ebc0d-105">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="ebc0d-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="ebc0d-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için</span><span class="sxs-lookup"><span data-stu-id="ebc0d-106">[Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="ebc0d-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -bizim gelecek nesil CLI hello kaynak yönetimi dağıtım modeli (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="ebc0d-107">[Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="ebc0d-108">Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="ebc0d-109">Ayrıca [hello Klasik dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ebc0d-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> <span data-ttu-id="ebc0d-110">Merhaba aşağıdaki örnek Azure CLI 2.0 komutları önceden oluşturulmuş basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-110">hello sample Azure CLI 2.0 commands below expect a simple environment already created.</span></span> <span data-ttu-id="ebc0d-111">Bu belgede gösterildiği toorun hello komutları istiyorsanız, ilk derleme açıklanan hello test ortamı [vnet oluşturma](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ebc0d-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="ebc0d-112">Bir VM oluşturulurken özel bir statik IP adresi belirtin</span><span class="sxs-lookup"><span data-stu-id="ebc0d-112">Specify a static private IP address when creating a VM</span></span>

<span data-ttu-id="ebc0d-113">toocreate adlı bir VM'den *DNS01* hello içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet* özel bir statik IP *192.168.1.101*, Merhaba adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="ebc0d-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="ebc0d-114">Henüz henüz, yüklemek ve hello son yapılandırırsanız [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ebc0d-114">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="ebc0d-115">Merhaba VM için bir genel IP ile Merhaba oluşturma [az ağ genel IP oluşturun](/cli/azure/network/public-ip#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-115">Create a public IP for hello VM with hello [az network public-ip create](/cli/azure/network/public-ip#create) command.</span></span> <span data-ttu-id="ebc0d-116">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-116">hello list shown after hello output explains hello parameters used.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ebc0d-117">İstediğiniz ya da ortamınıza bağlı olarak bu, bağımsız değişkenler için farklı değerler toouse ve sonraki adımları gerekir.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-117">You may want or need toouse different values for your arguments in this and subsequent steps, depending upon your environment.</span></span>
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    <span data-ttu-id="ebc0d-118">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="ebc0d-118">Expected output:</span></span>
   
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

   * <span data-ttu-id="ebc0d-119">`--resource-group`: Hangi toocreate hello ortak IP hello kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-119">`--resource-group`: Name of hello resource group in which toocreate hello public IP.</span></span>
   * <span data-ttu-id="ebc0d-120">`--name`: Hello genel IP adı.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-120">`--name`: Name of hello public IP.</span></span>
   * <span data-ttu-id="ebc0d-121">`--location`: Hangi toocreate hello genel IP azure bölgesinde.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-121">`--location`: Azure region in which toocreate hello public IP.</span></span>

3. <span data-ttu-id="ebc0d-122">Merhaba çalıştırmak [az ağ NIC oluşturmak](/cli/azure/network/nic#create) komutu toocreate NIC statik özel IP ile.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-122">Run hello [az network nic create](/cli/azure/network/nic#create) command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="ebc0d-123">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-123">hello list shown after hello output explains hello parameters used.</span></span> 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="ebc0d-124">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="ebc0d-124">Expected output:</span></span>
   
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
    
    <span data-ttu-id="ebc0d-125">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="ebc0d-125">Parameters:</span></span>

    * <span data-ttu-id="ebc0d-126">`--private-ip-address`: Merhaba NIC özel statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="ebc0d-126">`--private-ip-address`: Static private IP address for hello NIC.</span></span>
    * <span data-ttu-id="ebc0d-127">`--vnet-name`: Hangi toocreate NIC hello hello Vnet'in adı</span><span class="sxs-lookup"><span data-stu-id="ebc0d-127">`--vnet-name`: Name of hello VNet in wihch toocreate hello NIC.</span></span>
    * <span data-ttu-id="ebc0d-128">`--subnet`: Hangi toocreate hello NIC hello alt ağ adı</span><span class="sxs-lookup"><span data-stu-id="ebc0d-128">`--subnet`: Name of hello subnet in which toocreate hello NIC.</span></span>

4. <span data-ttu-id="ebc0d-129">Merhaba çalıştırmak [azure vm oluşturma](/cli/azure/vm/nic#create) hello genel IP NIC ile VM oluşturulan yukarıdaki komut toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-129">Run hello [azure vm create](/cli/azure/vm/nic#create) command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="ebc0d-130">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-130">hello list shown after hello output explains hello parameters used.</span></span>
   
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

    <span data-ttu-id="ebc0d-131">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="ebc0d-131">Expected output:</span></span>
   
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
   
   <span data-ttu-id="ebc0d-132">Merhaba temel dışında parametreleri [az vm oluşturma](/cli/azure/vm#create) parametreleri.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-132">Parameters other than hello basic [az vm create](/cli/azure/vm#create) parameters.</span></span>

   * <span data-ttu-id="ebc0d-133">`--nics`: Hello NIC toowhich hello VM adını eklenir.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-133">`--nics`: Name of hello NIC toowhich hello VM is attached.</span></span>
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="ebc0d-134">Bir VM için özel statik IP adresi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="ebc0d-134">Retrieve static private IP address information for a VM</span></span>

<span data-ttu-id="ebc0d-135">oluşturduğunuz tooview hello statik özel IP adresi Azure CLI komutu aşağıdaki hello çalıştırın ve hello değerlerini uyun *özel IP ayırma yöntemi* ve *özel IP adresi*:</span><span class="sxs-lookup"><span data-stu-id="ebc0d-135">tooview hello static private IP address that you created, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

<span data-ttu-id="ebc0d-136">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="ebc0d-136">Expected output:</span></span>

```json
"192.168.1.101"
```

<span data-ttu-id="ebc0d-137">toodisplay hello NIC belirli IP bilgilerini bu VM, sorgu hello NIC özellikle hello:</span><span class="sxs-lookup"><span data-stu-id="ebc0d-137">toodisplay hello specific IP information of hello NIC for that VM, query hello NIC specifically:</span></span>

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

<span data-ttu-id="ebc0d-138">Merhaba çıktısı aşağıdakine benzer şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ebc0d-138">hello output is something like:</span></span>

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="ebc0d-139">Özel bir statik IP adresi bir sanal makineden kaldırın</span><span class="sxs-lookup"><span data-stu-id="ebc0d-139">Remove a static private IP address from a VM</span></span>

<span data-ttu-id="ebc0d-140">Resource manager dağıtımları için Azure CLI içinde nıc'den özel bir statik IP adresi kaldıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-140">You cannot remove a static private IP address from a NIC in Azure CLI for resource manager deployments.</span></span> <span data-ttu-id="ebc0d-141">Yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ebc0d-141">You must:</span></span>
- <span data-ttu-id="ebc0d-142">Dinamik IP kullanan yeni bir NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="ebc0d-142">Create a new NIC that uses a dynamic IP</span></span>
- <span data-ttu-id="ebc0d-143">NIC yeni oluşturulan VM hello hello üzerinde Hello NIC ayarlayın</span><span class="sxs-lookup"><span data-stu-id="ebc0d-143">Set hello NIC on hello VM do hello newly created NIC.</span></span> 

<span data-ttu-id="ebc0d-144">VM kullanılan yukarıdaki hello komutları hello toochange Merhaba NIC hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-144">toochange hello NIC for hello VM used in hello commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="ebc0d-145">Merhaba çalıştırmak **azure ağı NIC grubu oluşturmak** toocreate dinamik IP ayırma ile yeni bir IP adresi kullanarak yeni bir NIC komutu.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-145">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation with a new IP address.</span></span> <span data-ttu-id="ebc0d-146">IP adresi belirtildiğinden, hello ayırma yöntemi olduğuna dikkat edin **dinamik**.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-146">Note that because no IP address is specified, hello allocation method is **Dynamic**.</span></span>

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    <span data-ttu-id="ebc0d-147">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="ebc0d-147">Expected output:</span></span>

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

2. <span data-ttu-id="ebc0d-148">Merhaba çalıştırmak **azure vm kümesi** komutu toochange hello NIC VM hello tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-148">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    <span data-ttu-id="ebc0d-149">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="ebc0d-149">Expected output:</span></span>
   
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
    > <span data-ttu-id="ebc0d-150">Merhaba VM büyüklükte toohave ise hello çalıştıran birden çok NIC **azure ağı NIC silme** toodelete hello eski NIC komutu</span><span class="sxs-lookup"><span data-stu-id="ebc0d-150">If hello VM is large enough toohave more than one NIC, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="ebc0d-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ebc0d-151">Next steps</span></span>
* <span data-ttu-id="ebc0d-152">Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-152">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="ebc0d-153">Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="ebc0d-153">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="ebc0d-154">Merhaba başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="ebc0d-154">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

