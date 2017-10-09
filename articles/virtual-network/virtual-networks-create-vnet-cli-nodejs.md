---
title: "kullanarak bir sanal ağ aaaCreate hello Azure CLI 1.0 | Microsoft Docs"
description: "Azure CLI 1.0 kullanarak bir sanal ağ toocreate hello nasıl öğrenin | Resource Manager."
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a><span data-ttu-id="1a832-103">Hello Azure CLI kullanarak bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="1a832-103">Create a virtual network using hello Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="1a832-104">Azure'un iki dağıtım modeli vardır: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="1a832-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="1a832-105">Microsoft, kaynakları hello Resource Manager dağıtım modeli üzerinden oluşturma önerir.</span><span class="sxs-lookup"><span data-stu-id="1a832-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="1a832-106">Merhaba iki modelleri arasındaki farklar hakkında daha fazla bilgi toolearn hello okuma hello [anlamak Azure dağıtım modelleri](../azure-resource-manager/resource-manager-deployment-model.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="1a832-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="1a832-107">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="1a832-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="1a832-108">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="1a832-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="1a832-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="1a832-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span>
- <span data-ttu-id="1a832-110">[Azure CLI 1.0](#create-a-virtual-network) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="1a832-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for hello classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="1a832-111">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="1a832-111">Create a virtual network</span></span>

<span data-ttu-id="1a832-112">kullanarak bir sanal ağ toocreate Azure CLI, aşağıdaki adımları tam hello hello:</span><span class="sxs-lookup"><span data-stu-id="1a832-112">toocreate a virtual network using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="1a832-113">Azure CLI aşağıdaki hello tarafından adımları hello hello yükleyip [hello Azure CLI yükleyip](../cli-install-nodejs.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="1a832-113">Install and configure hello Azure CLI by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="1a832-114">VNet ve bir alt ağ oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1a832-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="1a832-115">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="1a832-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="1a832-116">Kullanılan parametreler:</span><span class="sxs-lookup"><span data-stu-id="1a832-116">Parameters used:</span></span>

   * <span data-ttu-id="1a832-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="1a832-117">**--vnet**.</span></span> <span data-ttu-id="1a832-118">Merhaba VNet toobe oluşturulan adı.</span><span class="sxs-lookup"><span data-stu-id="1a832-118">Name of hello VNet toobe created.</span></span> <span data-ttu-id="1a832-119">Bizim senaryomuz için bu *TestVNet* ’tir.</span><span class="sxs-lookup"><span data-stu-id="1a832-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="1a832-120">**-e (veya--adres alanı)**.</span><span class="sxs-lookup"><span data-stu-id="1a832-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="1a832-121">VNet adres alanı.</span><span class="sxs-lookup"><span data-stu-id="1a832-121">VNet address space.</span></span> <span data-ttu-id="1a832-122">Bizim senaryomuz için *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="1a832-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="1a832-123">**-i (veya - CIDR)**.</span><span class="sxs-lookup"><span data-stu-id="1a832-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="1a832-124">Ağ maskesi CIDR biçiminde.</span><span class="sxs-lookup"><span data-stu-id="1a832-124">Network mask in CIDR format.</span></span> <span data-ttu-id="1a832-125">Bizim senaryomuz için *16*.</span><span class="sxs-lookup"><span data-stu-id="1a832-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="1a832-126">**-n (veya--alt ağ adı**).</span><span class="sxs-lookup"><span data-stu-id="1a832-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="1a832-127">Merhaba ilk alt ağ adı.</span><span class="sxs-lookup"><span data-stu-id="1a832-127">Name of hello first subnet.</span></span> <span data-ttu-id="1a832-128">Bizim senaryomuz için bu *FrontEnd* ’dir.</span><span class="sxs-lookup"><span data-stu-id="1a832-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="1a832-129">**-p (veya--alt başlangıç IP'sini)**.</span><span class="sxs-lookup"><span data-stu-id="1a832-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="1a832-130">Alt ağ veya alt ağ adres alanı için başlangıç IP adresi.</span><span class="sxs-lookup"><span data-stu-id="1a832-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="1a832-131">Bizim senaryomuz için *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="1a832-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="1a832-132">**-r (veya--alt ağ CIDR)**.</span><span class="sxs-lookup"><span data-stu-id="1a832-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="1a832-133">Alt ağ için CIDR biçiminde ağ maskesi.</span><span class="sxs-lookup"><span data-stu-id="1a832-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="1a832-134">Bizim senaryomuz için *24*.</span><span class="sxs-lookup"><span data-stu-id="1a832-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="1a832-135">**-l (veya --location)**.</span><span class="sxs-lookup"><span data-stu-id="1a832-135">**-l (or --location)**.</span></span> <span data-ttu-id="1a832-136">Merhaba VNet oluşturulduğu azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="1a832-136">Azure region where hello VNet is created.</span></span> <span data-ttu-id="1a832-137">Bizim senaryomuz için *Orta ABD*.</span><span class="sxs-lookup"><span data-stu-id="1a832-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="1a832-138">Bir alt ağ oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1a832-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="1a832-139">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="1a832-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="1a832-140">Kullanılan parametreler:</span><span class="sxs-lookup"><span data-stu-id="1a832-140">Parameters used:</span></span>

   * <span data-ttu-id="1a832-141">**-t (veya--vnet-ad**.</span><span class="sxs-lookup"><span data-stu-id="1a832-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="1a832-142">Merhaba hello alt oluşturulacağı Vnet'in adı.</span><span class="sxs-lookup"><span data-stu-id="1a832-142">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="1a832-143">Bizim senaryomuz için bu *TestVNet* ’tir.</span><span class="sxs-lookup"><span data-stu-id="1a832-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="1a832-144">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="1a832-144">**-n (or --name)**.</span></span> <span data-ttu-id="1a832-145">Merhaba yeni alt ağ adı.</span><span class="sxs-lookup"><span data-stu-id="1a832-145">Name of hello new subnet.</span></span> <span data-ttu-id="1a832-146">Bizim senaryomuz için *arka uç*.</span><span class="sxs-lookup"><span data-stu-id="1a832-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="1a832-147">**-a (veya--adres-önek)**.</span><span class="sxs-lookup"><span data-stu-id="1a832-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="1a832-148">Alt ağ CIDR bloğu.</span><span class="sxs-lookup"><span data-stu-id="1a832-148">Subnet CIDR block.</span></span> <span data-ttu-id="1a832-149">Dört bizim senaryomuz *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="1a832-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="1a832-150">Yeni VNet tooview hello özelliklerini hello:</span><span class="sxs-lookup"><span data-stu-id="1a832-150">tooview hello properties of hello new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="1a832-151">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="1a832-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a><span data-ttu-id="1a832-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1a832-152">Next steps</span></span>

<span data-ttu-id="1a832-153">Bilgi nasıl tooconnect:</span><span class="sxs-lookup"><span data-stu-id="1a832-153">Learn how tooconnect:</span></span>

- <span data-ttu-id="1a832-154">Merhaba okuyarak sanal makine (VM) tooa sanal ağ [bir Linux VM oluşturma](../virtual-machines/linux/quick-create-cli.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="1a832-154">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="1a832-155">Merhaba makaleleri hello adımlarda bir VNet ve alt ağ oluşturmak yerine, bir VM'ye mevcut VNet ve alt ağ tooconnect seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a832-155">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="1a832-156">sanal ağ tooother sanal ağlar hello okuyarak hello [sanal ağlara bağlanma](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="1a832-156">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="1a832-157">bir siteden siteye sanal özel ağ (VPN) veya expressroute bağlantı hattı kullanarak hello sanal ağ tooan şirket içi ağ.</span><span class="sxs-lookup"><span data-stu-id="1a832-157">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="1a832-158">Bilgi hello okuyarak nasıl [bir siteden siteye VPN kullanarak bir VNet tooan şirket içi ağ bağlanmak](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) ve [VNet tooan expressroute bağlantı hattı bağlantı](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1a832-158">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
