---
title: "aaaConfigure özel IP adresleri VM'ler - Azure CLI 1.0 için | Microsoft Docs"
description: "Nasıl tooconfigure özel IP adresleri kullanarak sanal makineleri için Azure komut satırı arabirimi (CLI) 1.0 hello öğrenin."
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
ms.openlocfilehash: 6caae79c98c7bc5f246b7bb3bb8bd8f032eb2d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-10"></a><span data-ttu-id="89b6e-103">Hello Azure CLI 1.0 kullanarak bir sanal makine için özel IP adreslerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="89b6e-103">Configure private IP addresses for a virtual machine using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="89b6e-104">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="89b6e-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="89b6e-105">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="89b6e-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="89b6e-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="89b6e-106">[Azure CLI 1.0](#how-to-specify-a-static-private-ip-address-when-creating-a-vm) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="89b6e-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="89b6e-107">[Azure CLI 2.0](virtual-networks-static-private-ip-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="89b6e-108">Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="89b6e-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="89b6e-109">Ayrıca [hello Klasik dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="89b6e-109">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="89b6e-110">Merhaba aşağıdaki örnek Azure CLI komutları önceden oluşturulmuş basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="89b6e-110">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="89b6e-111">Bu belgede gösterildiği toorun hello komutları istiyorsanız, ilk derleme açıklanan hello test ortamı [vnet oluşturma](virtual-networks-create-vnet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="89b6e-111">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="89b6e-112">Nasıl toospecify bir statik özel IP adresi bir VM oluşturulurken</span><span class="sxs-lookup"><span data-stu-id="89b6e-112">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="89b6e-113">toocreate adlı bir VM'den *DNS01* hello içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet* özel bir statik IP *192.168.1.101*, Merhaba adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="89b6e-113">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="89b6e-114">Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="89b6e-114">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="89b6e-115">Merhaba çalıştırmak **azure config modu** aşağıda gösterildiği gibi komut tooswitch tooResource Yöneticisi modu.</span><span class="sxs-lookup"><span data-stu-id="89b6e-115">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="89b6e-116">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="89b6e-116">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="89b6e-117">Merhaba çalıştırmak **azure ağı ve genel IP oluşturun** toocreate hello VM için bir genel IP.</span><span class="sxs-lookup"><span data-stu-id="89b6e-117">Run hello **azure network public-ip create** toocreate a public IP for hello VM.</span></span> <span data-ttu-id="89b6e-118">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="89b6e-118">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network public-ip create -g TestRG -n TestPIP -l centralus
   
    <span data-ttu-id="89b6e-119">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="89b6e-119">Expected output:</span></span>
   
        info:    Executing command network public-ip create
        + Looking up hello public ip "TestPIP"
        + Creating public ip address "TestPIP"
        + Looking up hello public ip "TestPIP"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP
        data:    Name                            : TestPIP
        data:    Type                            : Microsoft.Network/publicIPAddresses
        data:    Location                        : centralus
        data:    Provisioning state              : Succeeded
        data:    Allocation method               : Dynamic
        data:    Idle timeout                    : 4
        info:    network public-ip create command OK
   
   * <span data-ttu-id="89b6e-120">**-g (veya --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="89b6e-120">**-g (or --resource-group)**.</span></span> <span data-ttu-id="89b6e-121">Merhaba kaynak grubu hello genel IP adı içinde oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="89b6e-121">Name of hello resource group hello public IP will be created in.</span></span>
   * <span data-ttu-id="89b6e-122">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="89b6e-122">**-n (or --name)**.</span></span> <span data-ttu-id="89b6e-123">Merhaba genel IP adı.</span><span class="sxs-lookup"><span data-stu-id="89b6e-123">Name of hello public IP.</span></span>
   * <span data-ttu-id="89b6e-124">**-l (veya --location)**.</span><span class="sxs-lookup"><span data-stu-id="89b6e-124">**-l (or --location)**.</span></span> <span data-ttu-id="89b6e-125">Merhaba genel IP oluşturulacağı azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="89b6e-125">Azure region where hello public IP will be created.</span></span> <span data-ttu-id="89b6e-126">Bizim senaryomuz için bu *centralus* ’tur.</span><span class="sxs-lookup"><span data-stu-id="89b6e-126">For our scenario, *centralus*.</span></span>
4. <span data-ttu-id="89b6e-127">Merhaba çalıştırmak **azure ağı NIC grubu oluşturmak** komutu toocreate NIC statik özel IP ile.</span><span class="sxs-lookup"><span data-stu-id="89b6e-127">Run hello **azure network nic create** command toocreate a NIC with a static private IP.</span></span> <span data-ttu-id="89b6e-128">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="89b6e-128">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure network nic create -g TestRG -n TestNIC -l centralus -a 192.168.1.101 -m TestVNet -k FrontEnd
   
    <span data-ttu-id="89b6e-129">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="89b6e-129">Expected output:</span></span>
   
        + Looking up hello network interface "TestNIC"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC"
        + Looking up hello network interface "TestNIC"
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
   
   * <span data-ttu-id="89b6e-130">**-a (veya--özel IP adresi)**.</span><span class="sxs-lookup"><span data-stu-id="89b6e-130">**-a (or --private-ip-address)**.</span></span> <span data-ttu-id="89b6e-131">Merhaba NIC özel statik IP adresi</span><span class="sxs-lookup"><span data-stu-id="89b6e-131">Static private IP address for hello NIC.</span></span>
   * <span data-ttu-id="89b6e-132">**-m (veya--alt sanal ağ adı)**.</span><span class="sxs-lookup"><span data-stu-id="89b6e-132">**-m (or --subnet-vnet-name)**.</span></span> <span data-ttu-id="89b6e-133">Merhaba hello NIC oluşturulacağı Vnet'in adı.</span><span class="sxs-lookup"><span data-stu-id="89b6e-133">Name of hello VNet where hello NIC will be created.</span></span>
   * <span data-ttu-id="89b6e-134">**-k (veya--alt ağ adı)**.</span><span class="sxs-lookup"><span data-stu-id="89b6e-134">**-k (or --subnet-name)**.</span></span> <span data-ttu-id="89b6e-135">Merhaba NIC oluşturulacağı hello alt ağ adı.</span><span class="sxs-lookup"><span data-stu-id="89b6e-135">Name of hello subnet where hello NIC will be created.</span></span>
5. <span data-ttu-id="89b6e-136">Merhaba çalıştırmak **azure vm oluşturma** hello genel IP NIC ile VM oluşturulan yukarıdaki komut toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="89b6e-136">Run hello **azure vm create** command toocreate hello VM using hello public IP and NIC created above.</span></span> <span data-ttu-id="89b6e-137">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="89b6e-137">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -g TestRG -n DNS01 -l centralus -y Windows -f TestNIC -i TestPIP -F TestVNet -j FrontEnd -o vnetstorage -q bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 -u adminuser -p AdminP@ssw0rd
   
    <span data-ttu-id="89b6e-138">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="89b6e-138">Expected output:</span></span>
   
        info:    Executing command vm create
        + Looking up hello VM "DNS01"
        info:    Using hello VM Size "Standard_A1"
        warn:    hello image "bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2" will be used for VM
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account vnetstorage
        + Looking up hello NIC "TestNIC"
        info:    Found an existing NIC "TestNIC"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd" in hello NIC "TestNIC"
        info:    Found public ip parameters, trying toosetup PublicIP profile
        + Looking up hello public ip "TestPIP"
        info:    Found an existing PublicIP "TestPIP"
        info:    Configuring identified NIC IP configuration with PublicIP "TestPIP"
        + Updating NIC "TestNIC"
        + Looking up hello NIC "TestNIC"
        + Creating VM "DNS01"
        info:    vm create command OK
   
   * <span data-ttu-id="89b6e-139">**-y (veya--işletim sistemi türü)**.</span><span class="sxs-lookup"><span data-stu-id="89b6e-139">**-y (or --os-type)**.</span></span> <span data-ttu-id="89b6e-140">İşletim sistemi hello VM için ya da türü *Windows* veya *Linux*.</span><span class="sxs-lookup"><span data-stu-id="89b6e-140">Type of operating system for hello VM, either *Windows* or *Linux*.</span></span>
   * <span data-ttu-id="89b6e-141">**-f (veya--NIC-name)**.</span><span class="sxs-lookup"><span data-stu-id="89b6e-141">**-f (or --nic-name)**.</span></span> <span data-ttu-id="89b6e-142">Merhaba NIC hello VM adını kullanır.</span><span class="sxs-lookup"><span data-stu-id="89b6e-142">Name of hello NIC hello VM will use.</span></span>
   * <span data-ttu-id="89b6e-143">**-i (veya--genel IP adı)**.</span><span class="sxs-lookup"><span data-stu-id="89b6e-143">**-i (or --public-ip-name)**.</span></span> <span data-ttu-id="89b6e-144">Merhaba ortak IP hello VM adını kullanır.</span><span class="sxs-lookup"><span data-stu-id="89b6e-144">Name of hello public IP hello VM will use.</span></span>
   * <span data-ttu-id="89b6e-145">**-F (veya--vnet-ad)**.</span><span class="sxs-lookup"><span data-stu-id="89b6e-145">**-F (or --vnet-name)**.</span></span> <span data-ttu-id="89b6e-146">Merhaba hello VM oluşturulacağı Vnet'in adı.</span><span class="sxs-lookup"><span data-stu-id="89b6e-146">Name of hello VNet where hello VM will be created.</span></span>
   * <span data-ttu-id="89b6e-147">**-j (veya--vnet alt ağ adı)**.</span><span class="sxs-lookup"><span data-stu-id="89b6e-147">**-j (or --vnet-subnet-name)**.</span></span> <span data-ttu-id="89b6e-148">Merhaba VM oluşturulacağı hello alt ağ adı.</span><span class="sxs-lookup"><span data-stu-id="89b6e-148">Name of hello subnet where hello VM will be created.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="89b6e-149">Nasıl tooretrieve statik özel IP adresi, bir VM için bilgi</span><span class="sxs-lookup"><span data-stu-id="89b6e-149">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="89b6e-150">tooview hello statik özel IP adresi VM, Azure CLI komutu aşağıdaki hello çalıştırmak yukarıdaki hello betiği ile oluşturulan bilgi hello için ve hello değerlerini uyun *özel IP ayırma yöntemi* ve *özel IP adresi*:</span><span class="sxs-lookup"><span data-stu-id="89b6e-150">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello values for *Private IP alloc-method* and *Private IP address*:</span></span>

    azure vm show -g TestRG -n DNS01

<span data-ttu-id="89b6e-151">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="89b6e-151">Expected output:</span></span>

    info:    Executing command vm show
    + Looking up hello VM "DNS01"
    + Looking up hello NIC "TestNIC"
    + Looking up hello public ip "TestPIP
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

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="89b6e-152">Nasıl tooremove bir statik özel IP adresi bir sanal makineden</span><span class="sxs-lookup"><span data-stu-id="89b6e-152">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="89b6e-153">Özel bir statik IP adresi, Azure CLI için Resource Manager içinde nıc'den kaldıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="89b6e-153">You cannot remove a static private IP address from a NIC in Azure CLI for Resource Manager.</span></span> <span data-ttu-id="89b6e-154">Dinamik IP kullanan yeni bir NIC oluşturun, Kaldır hello VM önceki NIC'den hello ve ardından hello yeni NIC toohello VM ekleyin.</span><span class="sxs-lookup"><span data-stu-id="89b6e-154">You must create a new NIC that uses a dynamic IP, remove hello previous NIC from hello VM, and then add hello new NIC toohello VM.</span></span> <span data-ttu-id="89b6e-155">toochange NIC hello kullanılan VM int eh yukarıdaki komutlarda Merhaba, hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="89b6e-155">toochange hello NIC for hello VM used int eh commands above, follow hello steps below.</span></span>

1. <span data-ttu-id="89b6e-156">Merhaba çalıştırmak **azure ağı NIC grubu oluşturmak** toocreate dinamik IP ayırma kullanarak yeni bir NIC komutu.</span><span class="sxs-lookup"><span data-stu-id="89b6e-156">Run hello **azure network nic create** command toocreate a new NIC using dynamic IP allocation.</span></span> <span data-ttu-id="89b6e-157">Nasıl toospecify başlangıç IP adresi bu kez zorunda değilsiniz dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="89b6e-157">Notice how you do not need toospecify hello IP address this time.</span></span>
   
        azure network nic create -g TestRG -n TestNIC2 -l centralus -m TestVNet -k FrontEnd
   
    <span data-ttu-id="89b6e-158">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="89b6e-158">Expected output:</span></span>
   
        info:    Executing command network nic create
        + Looking up hello network interface "TestNIC2"
        + Looking up hello subnet "FrontEnd"
        + Creating network interface "TestNIC2"
        + Looking up hello network interface "TestNIC2"
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
2. <span data-ttu-id="89b6e-159">Merhaba çalıştırmak **azure vm kümesi** komutu toochange hello NIC VM hello tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="89b6e-159">Run hello **azure vm set** command toochange hello NIC used by hello VM.</span></span>
   
        azure vm set -g TestRG -n DNS01 -N TestNIC2
   
    <span data-ttu-id="89b6e-160">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="89b6e-160">Expected output:</span></span>
   
        info:    Executing command vm set
        + Looking up hello VM "DNS01"
        + Looking up hello NIC "TestNIC2"
        + Updating VM "DNS01"
        info:    vm set command OK
3. <span data-ttu-id="89b6e-161">İstediyseniz, hello çalıştırmak **azure ağı NIC silme** toodelete hello eski NIC komutu</span><span class="sxs-lookup"><span data-stu-id="89b6e-161">If wanted, run hello **azure network nic delete** command toodelete hello old NIC.</span></span>
   
        azure network nic delete -g TestRG -n TestNIC --quiet
   
    <span data-ttu-id="89b6e-162">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="89b6e-162">Expected output:</span></span>
   
        info:    Executing command network nic delete
        + Looking up hello network interface "TestNIC"
        + Deleting network interface "TestNIC"
        info:    network nic delete command OK

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a><span data-ttu-id="89b6e-163">Nasıl tooadd statik özel IP adresi VM varolan tooan</span><span class="sxs-lookup"><span data-stu-id="89b6e-163">How tooadd a static private IP address tooan existing VM</span></span>
<span data-ttu-id="89b6e-164">tooadd bir statik özel IP adresi toohello hello betik yukarıdaki kullanılarak oluşturulan VM tarafından kullanılan NIC hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="89b6e-164">tooadd a static private IP address toohello NIC used by teh VM created using hello script above, run hello following command:</span></span>

    azure network nic set -g TestRG -n TestNIC2 -a 192.168.1.101

<span data-ttu-id="89b6e-165">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="89b6e-165">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNIC2"
    + Updating network interface "TestNIC2"
    + Looking up hello network interface "TestNIC2"
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

## <a name="next-steps"></a><span data-ttu-id="89b6e-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="89b6e-166">Next steps</span></span>
* <span data-ttu-id="89b6e-167">Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="89b6e-167">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="89b6e-168">Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="89b6e-168">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="89b6e-169">Merhaba başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="89b6e-169">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

