---
title: Klasik mod kullanarak Nsg'ler aaaHow toocreate hello Azure CLI | Microsoft Docs
description: "Bilgi nasıl toocreate ve hello Azure CLI kullanarak Klasik modda Nsg'leri dağıtın"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a><span data-ttu-id="c892f-103">Azure CLI toocreate Nsg'ler (Klasik) nasıl hello</span><span class="sxs-lookup"><span data-stu-id="c892f-103">How toocreate NSGs (classic) in hello Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c892f-104">Bu makalede, hello Klasik dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="c892f-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="c892f-105">Ayrıca [hello Resource Manager dağıtım modelinde Nsg'leri oluşturma](virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c892f-105">You can also [create NSGs in hello Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="c892f-106">Merhaba aşağıdaki örnek Azure CLI komutları zaten senaryosunda hello yukarıdaki göre oluşturulan basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="c892f-106">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="c892f-107">Bu belgede gösterildiği toorun hello komutları istiyorsanız, önce hello test ortamı tarafından yapı [bir VNet oluşturma](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c892f-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="c892f-108">Ön uç alt toocreate hello nasıl için NSG hello</span><span class="sxs-lookup"><span data-stu-id="c892f-108">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="c892f-109">adlı bir NSG adlı toocreate **NSG ön uç** senaryosunda hello yukarıdaki bağlı olarak, aşağıdaki hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="c892f-109">toocreate an NSG named named **NSG-FrontEnd** based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="c892f-110">Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="c892f-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="c892f-111">Merhaba çalıştırmak  **`azure config mode`**  aşağıda gösterildiği gibi komut tooswitch tooclassic modu.</span><span class="sxs-lookup"><span data-stu-id="c892f-111">Run hello **`azure config mode`** command tooswitch tooclassic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="c892f-112">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="c892f-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="c892f-113">Merhaba çalıştırmak  **`azure network nsg create`**  komutu toocreate bir NSG.</span><span class="sxs-lookup"><span data-stu-id="c892f-113">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="c892f-114">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="c892f-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="c892f-115">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="c892f-115">Parameters:</span></span>
   
   * <span data-ttu-id="c892f-116">**-l (veya --location)**.</span><span class="sxs-lookup"><span data-stu-id="c892f-116">**-l (or --location)**.</span></span> <span data-ttu-id="c892f-117">Merhaba yeni NSG oluşturulacağı azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="c892f-117">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="c892f-118">Bizim senaryomuz için *westus*.</span><span class="sxs-lookup"><span data-stu-id="c892f-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="c892f-119">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="c892f-119">**-n (or --name)**.</span></span> <span data-ttu-id="c892f-120">Hello için ad yeni NSG.</span><span class="sxs-lookup"><span data-stu-id="c892f-120">Name for hello new NSG.</span></span> <span data-ttu-id="c892f-121">Bizim senaryomuz için *NSG ön uç*.</span><span class="sxs-lookup"><span data-stu-id="c892f-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="c892f-122">Merhaba çalıştırmak  **`azure network nsg rule create`**  komutu toocreate hello Internet gelen erişim tooport 3389 (RDP) sağlayan bir kural.</span><span class="sxs-lookup"><span data-stu-id="c892f-122">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="c892f-123">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="c892f-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="c892f-124">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="c892f-124">Parameters:</span></span>
   
   * <span data-ttu-id="c892f-125">**-a (veya--nsg-name)**.</span><span class="sxs-lookup"><span data-stu-id="c892f-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="c892f-126">Hangi hello kuralı oluşturulacak hello NSG adı.</span><span class="sxs-lookup"><span data-stu-id="c892f-126">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="c892f-127">Bizim senaryomuz için *NSG ön uç*.</span><span class="sxs-lookup"><span data-stu-id="c892f-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="c892f-128">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="c892f-128">**-n (or --name)**.</span></span> <span data-ttu-id="c892f-129">Merhaba yeni kural adı.</span><span class="sxs-lookup"><span data-stu-id="c892f-129">Name for hello new rule.</span></span> <span data-ttu-id="c892f-130">Bizim senaryomuz için *rdp kural*.</span><span class="sxs-lookup"><span data-stu-id="c892f-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="c892f-131">**-c (veya--eylem)**.</span><span class="sxs-lookup"><span data-stu-id="c892f-131">**-c (or --action)**.</span></span> <span data-ttu-id="c892f-132">Erişim düzeyi hello kuralın (Engelle veya izin ver).</span><span class="sxs-lookup"><span data-stu-id="c892f-132">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="c892f-133">**-p (veya--Protokolü)**.</span><span class="sxs-lookup"><span data-stu-id="c892f-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="c892f-134">Protokolü (Tcp, Udp veya *) hello kuralı için.</span><span class="sxs-lookup"><span data-stu-id="c892f-134">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="c892f-135">**-r (veya--türü)**.</span><span class="sxs-lookup"><span data-stu-id="c892f-135">**-r (or --type)**.</span></span> <span data-ttu-id="c892f-136">Bağlantı (gelen veya giden) yönü.</span><span class="sxs-lookup"><span data-stu-id="c892f-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="c892f-137">**-y (veya--öncelik)**.</span><span class="sxs-lookup"><span data-stu-id="c892f-137">**-y (or --priority)**.</span></span> <span data-ttu-id="c892f-138">Merhaba kuralı için öncelik.</span><span class="sxs-lookup"><span data-stu-id="c892f-138">Priority for hello rule.</span></span>
   * <span data-ttu-id="c892f-139">**-f (veya--kaynak adres öneki)**.</span><span class="sxs-lookup"><span data-stu-id="c892f-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="c892f-140">Kaynak adres ön eki CIDR veya varsayılan etiketleri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c892f-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="c892f-141">**-o (veya--kaynak bağlantı noktası aralığı)**.</span><span class="sxs-lookup"><span data-stu-id="c892f-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="c892f-142">Kaynak bağlantı noktası veya bağlantı noktası aralığı.</span><span class="sxs-lookup"><span data-stu-id="c892f-142">Source port, or port range.</span></span>
   * <span data-ttu-id="c892f-143">**-e (veya--hedef adres öneki)**.</span><span class="sxs-lookup"><span data-stu-id="c892f-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="c892f-144">Hedef adres ön eki CIDR veya varsayılan etiketleri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c892f-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="c892f-145">**-u (veya--hedef bağlantı noktası aralığı)**.</span><span class="sxs-lookup"><span data-stu-id="c892f-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="c892f-146">Hedef bağlantı noktası veya bağlantı noktası aralığı.</span><span class="sxs-lookup"><span data-stu-id="c892f-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="c892f-147">Merhaba çalıştırmak  **`azure network nsg rule create`**  komutu toocreate hello Internet gelen erişim tooport 80 (HTTP) sağlayan bir kural.</span><span class="sxs-lookup"><span data-stu-id="c892f-147">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="c892f-148">Beklenen putput:</span><span class="sxs-lookup"><span data-stu-id="c892f-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="c892f-149">Merhaba çalıştırmak  **`azure network nsg subnet add`**  komutu toolink hello NSG toohello ön uç alt.</span><span class="sxs-lookup"><span data-stu-id="c892f-149">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="c892f-150">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="c892f-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="c892f-151">Nasıl geri hello toocreate Merhaba NSG bitiş alt ağı</span><span class="sxs-lookup"><span data-stu-id="c892f-151">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="c892f-152">adlı bir NSG adlı toocreate *NSG arka uç* senaryosunda hello yukarıdaki bağlı olarak, aşağıdaki hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="c892f-152">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="c892f-153">Merhaba çalıştırmak  **`azure network nsg create`**  komutu toocreate bir NSG.</span><span class="sxs-lookup"><span data-stu-id="c892f-153">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="c892f-154">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="c892f-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="c892f-155">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="c892f-155">Parameters:</span></span>
   
   * <span data-ttu-id="c892f-156">**-l (veya --location)**.</span><span class="sxs-lookup"><span data-stu-id="c892f-156">**-l (or --location)**.</span></span> <span data-ttu-id="c892f-157">Merhaba yeni NSG oluşturulacağı azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="c892f-157">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="c892f-158">Bizim senaryomuz için *westus*.</span><span class="sxs-lookup"><span data-stu-id="c892f-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="c892f-159">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="c892f-159">**-n (or --name)**.</span></span> <span data-ttu-id="c892f-160">Hello için ad yeni NSG.</span><span class="sxs-lookup"><span data-stu-id="c892f-160">Name for hello new NSG.</span></span> <span data-ttu-id="c892f-161">Bizim senaryomuz için *NSG ön uç*.</span><span class="sxs-lookup"><span data-stu-id="c892f-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="c892f-162">Merhaba çalıştırmak  **`azure network nsg rule create`**  komutu toocreate hello ön uç alt ağından erişim tooport 1433 (SQL) sağlayan bir kural.</span><span class="sxs-lookup"><span data-stu-id="c892f-162">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="c892f-163">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="c892f-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="c892f-164">Merhaba çalıştırmak  **`azure network nsg rule create`**  komutu toocreate erişim toohello Internet engellediği bir kural.</span><span class="sxs-lookup"><span data-stu-id="c892f-164">Run hello **`azure network nsg rule create`** command toocreate a rule that denies access toohello Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="c892f-165">Beklenen putput:</span><span class="sxs-lookup"><span data-stu-id="c892f-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="c892f-166">Merhaba çalıştırmak  **`azure network nsg subnet add`**  toolink hello NSG toohello geri bitiş alt ağı komutu.</span><span class="sxs-lookup"><span data-stu-id="c892f-166">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="c892f-167">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="c892f-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

