---
title: "aaaConfigure özel IP adresleri VM'ler (Klasik) - Azure CLI 1.0 için | Microsoft Docs"
description: "Nasıl tooconfigure özel IP adresleri kullanarak sanal makineleri (Klasik) için Azure komut satırı arabirimi (CLI) 1.0 hello öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a><span data-ttu-id="107b4-103">Hello Azure CLI 1.0 kullanarak sanal makine (Klasik) için özel IP adreslerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="107b4-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="107b4-104">Bu makalede, hello Klasik dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="107b4-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="107b4-105">Ayrıca [hello Resource Manager dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="107b4-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span></span>

<span data-ttu-id="107b4-106">Merhaba aşağıdaki örnek Azure CLI komutları önceden oluşturulmuş basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="107b4-106">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="107b4-107">Bu belgede gösterildiği toorun hello komutları istiyorsanız, ilk derleme açıklanan hello test ortamı [vnet oluşturma](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="107b4-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="107b4-108">Nasıl toospecify bir statik özel IP adresi bir VM oluşturulurken</span><span class="sxs-lookup"><span data-stu-id="107b4-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="107b4-109">toocreate adlı yeni bir VM *DNS01* adlı yeni bir bulut hizmetinde *TestService* senaryosunda hello yukarıdaki bağlı olarak, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="107b4-109">toocreate a new VM named *DNS01* in a new cloud service named *TestService* based on hello scenario above, follow these steps:</span></span>

1. <span data-ttu-id="107b4-110">Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="107b4-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="107b4-111">Merhaba çalıştırmak **azure hizmet oluşturma** toocreate hello bulut hizmeti komutu.</span><span class="sxs-lookup"><span data-stu-id="107b4-111">Run hello **azure service create** command toocreate hello cloud service.</span></span>
   
        azure service create TestService --location uscentral
   
    <span data-ttu-id="107b4-112">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="107b4-112">Expected output:</span></span>
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. <span data-ttu-id="107b4-113">Merhaba çalıştırmak **azure vm oluşturma** komutu toocreate hello VM.</span><span class="sxs-lookup"><span data-stu-id="107b4-113">Run hello **azure create vm** command toocreate hello VM.</span></span> <span data-ttu-id="107b4-114">Özel bir statik IP adresi için Hello değer dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="107b4-114">Notice hello value for a static private IP address.</span></span> <span data-ttu-id="107b4-115">Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="107b4-115">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    <span data-ttu-id="107b4-116">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="107b4-116">Expected output:</span></span>
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * <span data-ttu-id="107b4-117">**-l (veya --location)**.</span><span class="sxs-lookup"><span data-stu-id="107b4-117">**-l (or --location)**.</span></span> <span data-ttu-id="107b4-118">Merhaba VM oluşturulacağı azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="107b4-118">Azure region where hello VM will be created.</span></span> <span data-ttu-id="107b4-119">Bizim senaryomuz için bu *centralus* ’tur.</span><span class="sxs-lookup"><span data-stu-id="107b4-119">For our scenario, *centralus*.</span></span>
   * <span data-ttu-id="107b4-120">**-n (veya--vm adı)**.</span><span class="sxs-lookup"><span data-stu-id="107b4-120">**-n (or --vm-name)**.</span></span> <span data-ttu-id="107b4-121">Merhaba VM toobe oluşturulan adı.</span><span class="sxs-lookup"><span data-stu-id="107b4-121">Name of hello VM toobe created.</span></span>
   * <span data-ttu-id="107b4-122">**-w (veya--ağ adı sanal)**.</span><span class="sxs-lookup"><span data-stu-id="107b4-122">**-w (or --virtual-network-name)**.</span></span> <span data-ttu-id="107b4-123">Merhaba hello VM oluşturulacağı Vnet'in adı.</span><span class="sxs-lookup"><span data-stu-id="107b4-123">Name of hello VNet where hello VM will be created.</span></span> 
   * <span data-ttu-id="107b4-124">**-S (veya--statik IP)**.</span><span class="sxs-lookup"><span data-stu-id="107b4-124">**-S (or --static-ip)**.</span></span> <span data-ttu-id="107b4-125">Özel için statik IP adresi hello VM.</span><span class="sxs-lookup"><span data-stu-id="107b4-125">Static private IP address for hello VM.</span></span>
   * <span data-ttu-id="107b4-126">**TestService**.</span><span class="sxs-lookup"><span data-stu-id="107b4-126">**TestService**.</span></span> <span data-ttu-id="107b4-127">Merhaba VM oluşturulacağı hello bulut hizmeti adı.</span><span class="sxs-lookup"><span data-stu-id="107b4-127">Name of hello cloud service where hello VM will be created.</span></span>
   * <span data-ttu-id="107b4-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span><span class="sxs-lookup"><span data-stu-id="107b4-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span></span> <span data-ttu-id="107b4-129">Görüntü toocreate hello VM kullanılır.</span><span class="sxs-lookup"><span data-stu-id="107b4-129">Image used toocreate hello VM.</span></span>
   * <span data-ttu-id="107b4-130">**AdminUser**.</span><span class="sxs-lookup"><span data-stu-id="107b4-130">**adminuser**.</span></span> <span data-ttu-id="107b4-131">Merhaba Windows VM için yerel yönetici.</span><span class="sxs-lookup"><span data-stu-id="107b4-131">Local administrator for hello Windows VM.</span></span>
   * <span data-ttu-id="107b4-132">**AdminP@ssw0rd**.</span><span class="sxs-lookup"><span data-stu-id="107b4-132">**AdminP@ssw0rd**.</span></span> <span data-ttu-id="107b4-133">Merhaba Windows VM için yerel yönetici parolası.</span><span class="sxs-lookup"><span data-stu-id="107b4-133">Local administrator password for hello Windows VM.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="107b4-134">Nasıl tooretrieve statik özel IP adresi, bir VM için bilgi</span><span class="sxs-lookup"><span data-stu-id="107b4-134">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="107b4-135">tooview hello statik özel IP adresi VM, Azure CLI komutu aşağıdaki hello çalıştırmak yukarıdaki hello betiği ile oluşturulan bilgi hello için ve hello değeri uyun *ağ StaticIP*:</span><span class="sxs-lookup"><span data-stu-id="107b4-135">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello value for *Network StaticIP*:</span></span>

    azure vm static-ip show DNS01

<span data-ttu-id="107b4-136">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="107b4-136">Expected output:</span></span>

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="107b4-137">Nasıl tooremove bir statik özel IP adresi bir sanal makineden</span><span class="sxs-lookup"><span data-stu-id="107b4-137">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="107b4-138">tooremove hello statik özel IP adresi, yukarıda, Azure CLI komutu aşağıdaki çalışma hello hello komut toohello VM eklendi:</span><span class="sxs-lookup"><span data-stu-id="107b4-138">tooremove hello static private IP address added toohello VM in hello script above, run hello following Azure CLI command:</span></span>

    azure vm static-ip remove DNS01

<span data-ttu-id="107b4-139">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="107b4-139">Expected output:</span></span>

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a><span data-ttu-id="107b4-140">Nasıl tooadd statik özel bir IP tooan var olan VM</span><span class="sxs-lookup"><span data-stu-id="107b4-140">How tooadd a static private IP tooan existing VM</span></span>
<span data-ttu-id="107b4-141">bir statik özel IP adresi toohello komutu aşağıdaki yukarıdaki çalışma hello komut dosyası kullanılarak oluşturulan VM tooadd:</span><span class="sxs-lookup"><span data-stu-id="107b4-141">tooadd a static private IP address toohello VM created using hello script above, runt he following command:</span></span>

    azure vm static-ip set DNS01 192.168.1.101

<span data-ttu-id="107b4-142">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="107b4-142">Expected output:</span></span>

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a><span data-ttu-id="107b4-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="107b4-143">Next steps</span></span>
* <span data-ttu-id="107b4-144">Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="107b4-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="107b4-145">Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.</span><span class="sxs-lookup"><span data-stu-id="107b4-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="107b4-146">Merhaba başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="107b4-146">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

