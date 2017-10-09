---
title: "Klasik Azure CLI aaaCreate bir Internet'e yönelik Yük Dengeleyici - | Microsoft Docs"
description: "Nasıl toocreate Klasik dağıtım modeli kullanarak bir Internet'e yönelik Yük Dengeleyici hello Azure CLI öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a><span data-ttu-id="62848-103">Internet'e yönelik yük dengeleyicisi (Klasik) hello Azure CLI oluşturmaya başlamak</span><span class="sxs-lookup"><span data-stu-id="62848-103">Get started creating an Internet facing load balancer (classic) in hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="62848-104">Klasik Azure Portalı</span><span class="sxs-lookup"><span data-stu-id="62848-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="62848-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="62848-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="62848-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="62848-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="62848-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="62848-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="62848-108">Azure kaynaklarıyla çalışmadan önce Azure'da şu anda iki dağıtım modeli olduğunu önemli toounderstand olduğu: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="62848-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="62848-109">Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarlarını](../azure-classic-rm.md) iyice anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="62848-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="62848-110">Bu makalenin hello üstünde hello sekmeleri tıklayarak farklı araçlarla ilgili hello belgeleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="62848-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="62848-111">Bu makalede, hello Klasik dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="62848-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="62848-112">Ayrıca [nasıl toocreate Internet'e yönelik Yük Dengeleyici Azure Resource Manager kullanarak bilgi](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="62848-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="62848-113">CLI kullanarak İnternet’e yönelik yük dengeleyici oluşturma adımları</span><span class="sxs-lookup"><span data-stu-id="62848-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="62848-114">Bu kılavuz, nasıl bir Internet yük dengeleyici toocreate yukarıdaki hello senaryosu üzerine temel gösterir.</span><span class="sxs-lookup"><span data-stu-id="62848-114">This guide shows how toocreate an Internet load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="62848-115">Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="62848-115">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="62848-116">Merhaba çalıştırmak **azure config modu** aşağıda gösterildiği gibi komut tooswitch tooclassic modu.</span><span class="sxs-lookup"><span data-stu-id="62848-116">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="62848-117">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="62848-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="62848-118">Uç nokta ve yük dengeleyici kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="62848-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="62848-119">Merhaba sanal makineler "web1" Merhaba senaryo varsayar ve "web2" oluşturulmadı.</span><span class="sxs-lookup"><span data-stu-id="62848-119">hello scenario assumes hello virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="62848-120">Bu kılavuzda hem genel hem de yerel bağlantı noktası olarak 80 numaralı bağlantı noktası kullanılarak bir yük dengeleyici kümesi oluşturulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="62848-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="62848-121">Sonda bağlantı noktası aynı zamanda bağlantı noktası 80 üzerinde yapılandırılmış olan ve "lbset" adlandırılmış hello yük dengeleyicisi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="62848-121">A probe port is also configured on port 80 and named hello load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="62848-122">1. Adım</span><span class="sxs-lookup"><span data-stu-id="62848-122">Step 1</span></span>

<span data-ttu-id="62848-123">Merhaba ilk uç noktası oluşturma ve yük dengeleyici kullanılarak ayarlanan `azure network vm endpoint create` "web1" bir sanal makine için.</span><span class="sxs-lookup"><span data-stu-id="62848-123">Create hello first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="62848-124">2. Adım</span><span class="sxs-lookup"><span data-stu-id="62848-124">Step 2</span></span>

<span data-ttu-id="62848-125">İkinci bir sanal makine "web2" toohello yük dengeleyici kümesini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="62848-125">Add a second virtual machine "web2" toohello load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="62848-126">3. Adım</span><span class="sxs-lookup"><span data-stu-id="62848-126">Step 3</span></span>

<span data-ttu-id="62848-127">Merhaba yük dengeleyici Yapılandırması kullanılarak doğrulayın `azure vm show` .</span><span class="sxs-lookup"><span data-stu-id="62848-127">Verify hello load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="62848-128">Merhaba çıkış olacaktır:</span><span class="sxs-lookup"><span data-stu-id="62848-128">hello output will be:</span></span>

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="62848-129">Bir sanal makine için uzak masaüstü uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="62848-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="62848-130">Uzak Masaüstü uç nokta tooforward ağ trafiğini kullanarak belirli bir sanal makine için bir genel bağlantı noktası tooa yerel bağlantı noktasından oluşturabileceğiniz `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="62848-130">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="62848-131">Sanal makineyi yük dengeleyiciden kaldırma</span><span class="sxs-lookup"><span data-stu-id="62848-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="62848-132">Yük Dengeleyici kümesi hello sanal makineden toodelete hello ilişkili uç nokta toohello sahip.</span><span class="sxs-lookup"><span data-stu-id="62848-132">You have toodelete hello endpoint associated toohello load balancer set from hello virtual machine.</span></span> <span data-ttu-id="62848-133">Merhaba endpoint kaldırıldıktan sonra hello sanal makine artık ayarlamak toohello yük dengeleyici ait değil.</span><span class="sxs-lookup"><span data-stu-id="62848-133">Once hello endpoint is removed, hello virtual machine doesn't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="62848-134">Yukarıdaki Hello örneği kullanarak, yük dengeleyiciden "Merhaba komutunu kullanarak lbset'e" Merhaba endpoint "web1" sanal makine için oluşturulmuş kaldırabilirsiniz `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="62848-134">Using hello example above, you can remove hello endpoint created for virtual machine "web1" from load balancer "lbset" using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="62848-135">Merhaba komutunu kullanarak daha fazla seçenekleri toomanage uç noktaları keşfedin`azure vm endpoint --help`</span><span class="sxs-lookup"><span data-stu-id="62848-135">You can explore more options toomanage endpoints using hello command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="62848-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="62848-136">Next steps</span></span>

[<span data-ttu-id="62848-137">Bir iç yük dengeleyici yapılandırmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="62848-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="62848-138">Yük dengeleyici dağıtım modu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="62848-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="62848-139">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="62848-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
