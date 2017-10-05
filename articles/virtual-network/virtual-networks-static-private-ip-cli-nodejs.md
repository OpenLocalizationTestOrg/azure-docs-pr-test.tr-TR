---
title: "Özel IP adresleri VM'ler - Azure CLI 1.0 için yapılandırma | Microsoft Docs"
description: "Azure komut satırı arabirimi (CLI) 1.0 kullanarak sanal makineleri için özel IP adresleri yapılandırmayı öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9179319095c31d5eb454860e173ffa7c65fc9f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-cli-10"></a><span data-ttu-id="5d555-103">Azure CLI 1.0 kullanarak bir sanal makine için özel IP adreslerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5d555-103">Configure private IP addresses for a virtual machine using the Azure CLI 1.0</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="5d555-104">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="5d555-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="5d555-105">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5d555-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="5d555-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="5d555-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="5d555-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) -bizim nesil CLI kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="5d555-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) - our next-generation CLI for the resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="5d555-108">Bu makalede Resource Manager dağıtım modeli anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5d555-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="5d555-109">Ayrıca [Klasik dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5d555-109">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="5d555-110">Aşağıdaki örnek Azure CLI komutları önceden oluşturulmuş basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="5d555-110">The sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="5d555-111">Bu belgede gösterildiği komutları çalıştırmak istiyorsanız, önce açıklanan test ortamı oluşturmak [vnet oluşturma](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5d555-111">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="5d555-112">Bir VM oluşturulurken özel bir statik IP adresi belirtme</span><span class="sxs-lookup"><span data-stu-id="5d555-112">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="5d555-113">Adlı bir VM oluşturmak için *DNS01* içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet* özel bir statik IP *192.168.1.101*, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="5d555-113">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="5d555-114">Hiç Azure CLI kullanmadıysanız bkz. [Azure CLI’yi Yükleme ve Yapılandırma](../cli-install-nodejs.md); sonra da, Azure hesabınızı ve aboneliğinizi seçtiğiniz noktaya kadar yönergeleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="5d555-114">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="5d555-115">Resource Manager moduna geçmek için **azure config mode** komutunu aşağıda gösterildiği gibi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5d555-115">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="5d555-116">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="5d555-116">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="5d555-117">Çalıştırma **azure ağı ve genel IP oluşturun** VM için bir ortak IP oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="5d555-117">Run the **azure network public-ip create** to create a public IP for the VM.</span></span> <span data-ttu-id="5d555-118">Çıktıdan sonra gösterilen listede, kullanılan parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5d555-118">The list shown after the output explains the parameters used.</span></span>
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    <span data-ttu-id="5d555-119">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="5d555-119">Expected output:</span></span>
   
        info:    Executing command network public-ip create
        + Looking up the public ip "TestPIP"
        + Creating public ip address "TestPIP"
        + Looking up the public ip "TestPIP"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP
        data:    Name                            : TestPIP
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Dynamic
        data:    Idle timeout                    : 4
        info:    network public-ip create command OK
   
   * <span data-ttu-id="5d555-120">**-g (veya --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="5d555-120">**-g (or --resource-group)**.</span></span> <span data-ttu-id="5d555-121">Genel IP oluşturulduğu kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="5d555-121">Name of the resource group the public IP will be created in.</span></span>
   * <span data-ttu-id="5d555-122">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="5d555-122">**-n (or --name)**.</span></span> <span data-ttu-id="5d555-123">Genel IP adı.</span><span class="sxs-lookup"><span data-stu-id="5d555-123">Name of the public IP.</span></span>
   * <span data-ttu-id="5d555-124">**-l (veya --location)**.</span><span class="sxs-lookup"><span data-stu-id="5d555-124">**-l (or --location)**.</span></span> <span data-ttu-id="5d555-125">Genel IP oluşturulacağı azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="5d555-125">Azure region where the public IP will be created.</span></span> <span data-ttu-id="5d555-126">Bizim senaryomuz için bu *centralus* ’tur.</span><span class="sxs-lookup"><span data-stu-id="5d555-126">For our scenario, *centralus*.</span></span>
4. <span data-ttu-id="5d555-127">Çalıştırma **azure ağı NIC grubu oluşturmak** statik özel IP ile NIC grubu oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="5d555-127">Run the **azure network nic create** command to create a NIC with a static private IP.</span></span> <span data-ttu-id="5d555-128">Çıktıdan sonra gösterilen listede, kullanılan parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5d555-128">The list shown after the output explains the parameters used.</span></span>
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    <span data-ttu-id="5d555-129">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="5d555-129">Expected output:</span></span>
   
        + Looking up the network interface "TestNIC"
        + Looking up the subnet "FrontEnd"
        + Creating network interface "TestNIC"
        + Looking up the network interface "TestNIC"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
        data:    Name                            : TestNIC
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.101
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
   
   * <span data-ttu-id="5d555-130">**-a (veya--özel IP adresi)**.</span><span class="sxs-lookup"><span data-stu-id="5d555-130">**-a (or --private-ip-address)**.</span></span> <span data-ttu-id="5d555-131">NIC özel statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="5d555-131">Static private IP address for the NIC.</span></span>
   * <span data-ttu-id="5d555-132">**-m (veya--alt sanal ağ adı)**.</span><span class="sxs-lookup"><span data-stu-id="5d555-132">**-m (or --subnet-vnet-name)**.</span></span> <span data-ttu-id="5d555-133">NIC oluşturulacağı Vnet'in adı.</span><span class="sxs-lookup"><span data-stu-id="5d555-133">Name of the VNet where the NIC will be created.</span></span>
   * <span data-ttu-id="5d555-134">**-k (veya--alt ağ adı)**.</span><span class="sxs-lookup"><span data-stu-id="5d555-134">**-k (or --subnet-name)**.</span></span> <span data-ttu-id="5d555-135">NIC oluşturulacağı alt ağ adı.</span><span class="sxs-lookup"><span data-stu-id="5d555-135">Name of the subnet where the NIC will be created.</span></span>
5. <span data-ttu-id="5d555-136">Çalıştırma **azure vm oluşturma** ortak IP yukarıda oluşturduğunuz NIC ile VM oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="5d555-136">Run the **azure vm create** command to create the VM using the public IP and NIC created above.</span></span> <span data-ttu-id="5d555-137">Çıktıdan sonra gösterilen listede, kullanılan parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5d555-137">The list shown after the output explains the parameters used.</span></span>
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    <span data-ttu-id="5d555-138">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="5d555-138">Expected output:</span></span>
   
        info:    Executing command vm create
        + Looking up the VM "DNS01"
        info:    Using the VM Size "Standard_A1"
        warn:    The image "bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2" will be used for VM
        info:    The [OS, Data] Disk or image configuration requires storage account
        + Looking up the storage account vnetstorage
        + Looking up the NIC "TestNIC"
        info:    Found an existing NIC "TestNIC"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd" in the NIC "TestNIC"
        info:    Found public ip parameters, trying to setup PublicIP profile
        + Looking up the public ip "TestPIP"
        info:    Found an existing PublicIP "TestPIP"
        info:    Configuring identified NIC IP configuration with PublicIP "TestPIP"
        + Updating NIC "TestNIC"
        + Looking up the NIC "TestNIC"
        + Creating VM "DNS01"
        info:    vm create command OK
   
   * <span data-ttu-id="5d555-139">**-y (veya--işletim sistemi türü)**.</span><span class="sxs-lookup"><span data-stu-id="5d555-139">**-y (or --os-type)**.</span></span> <span data-ttu-id="5d555-140">Ya da VM için işletim sistemi türü *Windows* veya *Linux*.</span><span class="sxs-lookup"><span data-stu-id="5d555-140">Type of operating system for the VM, either *Windows* or *Linux*.</span></span>
   * <span data-ttu-id="5d555-141">**-f (veya--NIC-name)**.</span><span class="sxs-lookup"><span data-stu-id="5d555-141">**-f (or --nic-name)**.</span></span> <span data-ttu-id="5d555-142">NIC VM adını kullanır.</span><span class="sxs-lookup"><span data-stu-id="5d555-142">Name of the NIC the VM will use.</span></span>
   * <span data-ttu-id="5d555-143">**-i (veya--genel IP adı)**.</span><span class="sxs-lookup"><span data-stu-id="5d555-143">**-i (or --public-ip-name)**.</span></span> <span data-ttu-id="5d555-144">Genel IP VM adını kullanır.</span><span class="sxs-lookup"><span data-stu-id="5d555-144">Name of the public IP the VM will use.</span></span>
   * <span data-ttu-id="5d555-145">**-F (veya--vnet-ad)**.</span><span class="sxs-lookup"><span data-stu-id="5d555-145">**-F (or --vnet-name)**.</span></span> <span data-ttu-id="5d555-146">VM oluşturulacağı Vnet'in adı.</span><span class="sxs-lookup"><span data-stu-id="5d555-146">Name of the VNet where the VM will be created.</span></span>
   * <span data-ttu-id="5d555-147">**-j (veya--vnet alt ağ adı)**.</span><span class="sxs-lookup"><span data-stu-id="5d555-147">**-j (or --vnet-subnet-name)**.</span></span> <span data-ttu-id="5d555-148">VM oluşturulacağı alt ağ adı.</span><span class="sxs-lookup"><span data-stu-id="5d555-148">Name of the subnet where the VM will be created.</span></span>

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="5d555-149">Bir VM için özel statik IP adresi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="5d555-149">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="5d555-150">Komut dosyası yukarıdaki VM oluşturulan için statik özel IP adresi bilgilerini görüntülemek için Azure CLI ve aşağıdaki komutu çalıştırın değerlerini gözlemlemek *özel IP ayırma yöntemi* ve *özel IP adresi*:</span><span class="sxs-lookup"><span data-stu-id="5d555-150">To view the static private IP address information for the VM created with the script above, run the following Azure CLI command and observe the values for *Private IP alloc-method* and *Private IP address*:</span></span>

    azure vm show -g TestRG -n DNS01

<span data-ttu-id="5d555-151">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="5d555-151">Expected output:</span></span>

    info:    Executing command vm show
    + Looking up the VM "DNS01"
    + Looking up the NIC "TestNIC"
    + Looking up the public ip "TestPIP
    data:    Id                              :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    ProvisioningState               :Succeeded
    data:    Name                            :DNS01
    data:    Location                        :centralus
    data:    Type                            :Microsoft.Compute/virtualMachines
    data:
    data:    Hardware Profile:
    data:      Size                          :Standard_A1
    data:
    data:    Storage Profile:
    data:      Source image:
    data:        Id                          :/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/services/images/bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
    data:
    data:      OS Disk:
    data:        OSType                      :Windows
    data:        Name                        :cli08d7bd987a0112a8-os-1441774961355
    data:        Caching                     :ReadWrite
    data:        CreateOption                :FromImage
    data:        Vhd:
    data:          Uri                       :https://vnetstorage2.blob.core.windows.net/vhds/cli08d7bd987a0112a8-os-1441774961355vhd
    data:
    data:    OS Profile:
    data:      Computer Name                 :DNS01
    data:      User Name                     :adminuser
    data:      Windows Configuration:
    data:        Provision VM Agent          :true
    data:        Enable automatic updates    :true
    data:
    data:    Network Profile:
    data:      Network Interfaces:
    data:        Network Interface #1:
    data:          Id                        :/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    data:          Primary                   :true
    data:          MAC Address               :00-0D-3A-90-1A-A8
    data:          Provisioning State        :Succeeded
    data:          Name                      :TestNIC
    data:          Location                  :centralus
    data:            Private IP alloc-method :Static
    data:            Private IP address      :192.168.1.101
    data:            Public IP address       :40.122.213.159
    info:    vm show command OK

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="5d555-152">Özel bir statik IP adresi bir VM'den kaldırma</span><span class="sxs-lookup"><span data-stu-id="5d555-152">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="5d555-153">Özel bir statik IP adresi, Azure CLI için Resource Manager içinde nıc'den kaldıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="5d555-153">You cannot remove a static private IP address from a NIC in Azure CLI for Resource Manager.</span></span> <span data-ttu-id="5d555-154">Dinamik IP kullanan yeni bir NIC oluşturun, önceki NIC sanal makineden kaldırın ve ardından yeni NIC VM eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5d555-154">You must create a new NIC that uses a dynamic IP, remove the previous NIC from the VM, and then add the new NIC to the VM.</span></span> <span data-ttu-id="5d555-155">Yukarıdaki komutlarda kullanılan VM int eh NIC değiştirmek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="5d555-155">To change the NIC for the VM used int eh commands above, follow the steps below.</span></span>

1. <span data-ttu-id="5d555-156">Çalıştırma **azure ağı NIC grubu oluşturmak** dinamik IP ayırma kullanarak yeni bir NIC grubu oluşturmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="5d555-156">Run the **azure network nic create** command to create a new NIC using dynamic IP allocation.</span></span> <span data-ttu-id="5d555-157">Nasıl IP adresini bu süreyi belirtin gerekmez dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="5d555-157">Notice how you do not need to specify the IP address this time.</span></span>
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    <span data-ttu-id="5d555-158">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="5d555-158">Expected output:</span></span>
   
        info:    Executing command network nic create
        + Looking up the network interface "TestNIC2"
        + Looking up the subnet "FrontEnd"
        + Creating network interface "TestNIC2"
        + Looking up the network interface "TestNIC2"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
        data:    Name                            : TestNIC2
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.1.6
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:
        info:    network nic create command OK
2. <span data-ttu-id="5d555-159">Çalıştırma **azure vm kümesi** VM tarafından kullanılan NIC değiştirmek için komutu.</span><span class="sxs-lookup"><span data-stu-id="5d555-159">Run the **azure vm set** command to change the NIC used by the VM.</span></span>
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    <span data-ttu-id="5d555-160">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="5d555-160">Expected output:</span></span>
   
        info:    Executing command vm set
        + Looking up the VM "DNS01"
        + Looking up the NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. <span data-ttu-id="5d555-161">İstediyseniz, çalıştırmak **azure ağı NIC silme** eski NIC silmek için</span><span class="sxs-lookup"><span data-stu-id="5d555-161">If wanted, run the **azure network nic delete** command to delete the old NIC.</span></span>
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    <span data-ttu-id="5d555-162">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="5d555-162">Expected output:</span></span>
   
        info:    Executing command network nic delete
        + Looking up the network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-to-add-a-static-private-ip-address-to-an-existing-vm"></a><span data-ttu-id="5d555-163">Mevcut bir VM'yi özel bir statik IP adresi ekleme</span><span class="sxs-lookup"><span data-stu-id="5d555-163">How to add a static private IP address to an existing VM</span></span>
<span data-ttu-id="5d555-164">Yukarıdaki komut dosyası kullanılarak oluşturulan VM tarafından kullanılan NIC özel bir statik IP adresi eklemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="5d555-164">To add a static private IP address to the NIC used by teh VM created using the script above, run the following command:</span></span>

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

<span data-ttu-id="5d555-165">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="5d555-165">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up the network interface "TestNIC2"
    + Updating network interface "TestNIC2"
    + Looking up the network interface "TestNIC2"
    data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2
    data:    Name                            : TestNIC2
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : centralus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-90-29-25
    data:    Enable IP forwarding            : false
    data:    Virtual machine                 : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01
    data:    IP configurations:
    data:      Name                          : NIC-config
    data:      Provisioning state            : Succeeded
    data:      Private IP address            : 192.168.1.101
    data:      Private IP Allocation Method  : Static
    data:      Subnet                        : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

## <a name="next-steps"></a><span data-ttu-id="5d555-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5d555-166">Next steps</span></span>
* <span data-ttu-id="5d555-167">Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="5d555-167">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="5d555-168">Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="5d555-168">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="5d555-169">Başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="5d555-169">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

