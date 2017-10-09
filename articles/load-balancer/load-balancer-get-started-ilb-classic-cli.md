---
title: "Klasik Azure CLI aaaCreate bir dahili yük dengeleyici - | Microsoft Docs"
description: "Nasıl bir iç yük dengeleyici kullanarak toocreate hello Azure CLI hello Klasik dağıtım modelinde öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a><span data-ttu-id="48bbe-103">Hello Azure CLI kullanarak bir iç yük dengeleyici (Klasik) oluşturmaya başlamak</span><span class="sxs-lookup"><span data-stu-id="48bbe-103">Get started creating an internal load balancer (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="48bbe-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="48bbe-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="48bbe-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="48bbe-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="48bbe-106">Bulut hizmetleri</span><span class="sxs-lookup"><span data-stu-id="48bbe-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="48bbe-107">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="48bbe-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="48bbe-108">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="48bbe-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="48bbe-109">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="48bbe-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="48bbe-110">Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](load-balancer-get-started-ilb-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="48bbe-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="48bbe-111">sanal makineler için bir iç yük dengeleyici toocreate ayarlayın</span><span class="sxs-lookup"><span data-stu-id="48bbe-111">toocreate an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="48bbe-112">bir iç yük dengeleyicisi ayarlayın ve hello kendi trafiği tooit göndereceğiniz sunucuları toocreate gerçekleştirmelisiniz hello aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="48bbe-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you must do hello following:</span></span>

1. <span data-ttu-id="48bbe-113">İç yük iş yükünün bir yük dengeli kümesi hello sunucular arasında dengeli gelen trafik toobe hello uç nokta olacak Dengeleme örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="48bbe-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="48bbe-114">Merhaba gelen trafiği almak toohello sanal makineleri karşılık gelen uç noktalarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="48bbe-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="48bbe-115">Kendi trafiği toohello sanal IP (VIP) adresi iç Yük Dengeleme hello örneğinin toosend hello trafiği toobe yük dengeli gönderme hello sunucularını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="48bbe-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="48bbe-116">CLI kullanarak iç yük dengeleyici oluşturma adımları</span><span class="sxs-lookup"><span data-stu-id="48bbe-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="48bbe-117">Bu kılavuz, nasıl bir iç yük dengeleyici toocreate yukarıdaki hello senaryosu üzerine temel gösterir.</span><span class="sxs-lookup"><span data-stu-id="48bbe-117">This guide shows how toocreate an internal load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="48bbe-118">Azure CLI hiç kullanmadıysanız bkz [hello Azure CLI yükleyip](../cli-install-nodejs.md) ve sonra Azure hesabınızı ve aboneliğinizi toohello noktaya hello talimatlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="48bbe-118">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="48bbe-119">Merhaba çalıştırmak **azure config modu** aşağıda gösterildiği gibi komut tooswitch tooclassic modu.</span><span class="sxs-lookup"><span data-stu-id="48bbe-119">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="48bbe-120">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="48bbe-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="48bbe-121">Uç nokta ve yük dengeleyici kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="48bbe-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="48bbe-122">Merhaba senaryo hello sanal makineler "DB1" ve "DB2" "mytestcloud" adlı bir bulut hizmetinde varsayar.</span><span class="sxs-lookup"><span data-stu-id="48bbe-122">hello scenario assumes hello virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="48bbe-123">Her iki sanal makine de "subnet-1" alt ağına sahip "testvnet" adlı bir sanal ağ kullanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="48bbe-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="48bbe-124">Bu kılavuzda hem özel hem de yerel bağlantı noktası olarak 1433 numaralı bağlantı noktası kullanılarak bir iç yük dengeleyici kümesi oluşturulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="48bbe-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="48bbe-125">Bu, bir ortak IP adresini kullanarak doğrudan bir iç yük dengeleyici tooguarantee hello veritabanı sunucuları sunulan olmaz arka uç hello kullanarak SQL sanal makineleri sahip olduğu ortak bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="48bbe-125">This is a common scenario where you have SQL virtual machines on hello back end using an internal load balancer tooguarantee hello database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="48bbe-126">1. Adım</span><span class="sxs-lookup"><span data-stu-id="48bbe-126">Step 1</span></span>

<span data-ttu-id="48bbe-127">`azure network service internal-load-balancer add` kullanarak iç yük dengeleyici kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="48bbe-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="48bbe-128">Daha fazla bilgi için bkz. `azure service internal-load-balancer --help`.</span><span class="sxs-lookup"><span data-stu-id="48bbe-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="48bbe-129">Merhaba komutunu kullanarak hello iç yük dengeleyici özelliklerini kontrol edebilirsiniz `azure service internal-load-balancer list` *bulut hizmeti adı*.</span><span class="sxs-lookup"><span data-stu-id="48bbe-129">You can check hello internal load balancer properties using hello command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="48bbe-130">Burada hello çıktısı örneği aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="48bbe-130">Here follows an example of hello output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="48bbe-131">2. Adım</span><span class="sxs-lookup"><span data-stu-id="48bbe-131">Step 2</span></span>

<span data-ttu-id="48bbe-132">Merhaba iç yük dengeleyici hello Birinci uç nokta eklediğinizde Ayarla yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="48bbe-132">You configure hello internal load balancer set when you add hello first endpoint.</span></span> <span data-ttu-id="48bbe-133">Bu adımda ayarlama hello uç noktasını, sanal makine ve araştırma bağlantı noktası toohello iç yük dengeleyici ilişkilendireceğiniz.</span><span class="sxs-lookup"><span data-stu-id="48bbe-133">You will associate hello endpoint, virtual machine and probe port toohello internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="48bbe-134">3. Adım</span><span class="sxs-lookup"><span data-stu-id="48bbe-134">Step 3</span></span>

<span data-ttu-id="48bbe-135">Merhaba yük dengeleyici Yapılandırması kullanılarak doğrulayın `azure vm show` *sanal makine adı*</span><span class="sxs-lookup"><span data-stu-id="48bbe-135">Verify hello load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="48bbe-136">Merhaba çıkış olacaktır:</span><span class="sxs-lookup"><span data-stu-id="48bbe-136">hello output will be:</span></span>

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="48bbe-137">Bir sanal makine için uzak masaüstü uç noktası oluşturma</span><span class="sxs-lookup"><span data-stu-id="48bbe-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="48bbe-138">Uzak Masaüstü uç nokta tooforward ağ trafiğini kullanarak belirli bir sanal makine için bir genel bağlantı noktası tooa yerel bağlantı noktasından oluşturabileceğiniz `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="48bbe-138">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="48bbe-139">Sanal makineyi yük dengeleyiciden kaldırma</span><span class="sxs-lookup"><span data-stu-id="48bbe-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="48bbe-140">İlişkili hello uç noktası siliniyor tarafından ayarlanmış bir iç yük dengeleyici sanal makine kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48bbe-140">You can remove a virtual machine from an internal load balancer set by deleting hello associated endpoint.</span></span> <span data-ttu-id="48bbe-141">Merhaba endpoint kaldırıldıktan sonra hello sanal makine artık ayarlamak toohello yük dengeleyici ait olmaz.</span><span class="sxs-lookup"><span data-stu-id="48bbe-141">Once hello endpoint is removed, hello virtual machine won't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="48bbe-142">Yukarıdaki Hello örneği kullanarak, "DB1" sanal makine için oluşturulmuş hello endpoint iç yük dengeleyiciden "ilbset" Merhaba komutunu kullanarak kaldırabilirsiniz `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="48bbe-142">Using hello example above, you can remove hello endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="48bbe-143">Daha fazla bilgi için bkz. `azure vm endpoint --help`.</span><span class="sxs-lookup"><span data-stu-id="48bbe-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48bbe-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48bbe-144">Next steps</span></span>

[<span data-ttu-id="48bbe-145">Kaynak IP benzeşimi kullanarak yük dengeleyici dağıtım modunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="48bbe-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="48bbe-146">Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="48bbe-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
