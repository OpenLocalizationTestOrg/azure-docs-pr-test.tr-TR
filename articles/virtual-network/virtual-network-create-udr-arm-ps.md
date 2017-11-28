---
title: "Azure - PowerShell aaaControl Yönlendirme ve sanal gereçler | Microsoft Docs"
description: "Bilgi nasıl toocontrol Yönlendirme ve sanal gereçler PowerShell kullanarak."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 9582fdaa-249c-4c98-9618-8c30d496940f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: b7b8717529eb2cd8b1d28b8ab9c6e21159d14882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-powershell"></a><span data-ttu-id="5f8a3-103">Kullanıcı tanımlı yolları (UDR) PowerShell kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f8a3-103">Create User-Defined Routes (UDR) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5f8a3-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f8a3-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="5f8a3-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5f8a3-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="5f8a3-106">Şablon</span><span class="sxs-lookup"><span data-stu-id="5f8a3-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="5f8a3-107">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="5f8a3-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="5f8a3-108">CLI (Klasik)</span><span class="sxs-lookup"><span data-stu-id="5f8a3-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="5f8a3-109">Azure kaynaklarıyla çalışmadan önce Azure'da şu anda iki dağıtım modeli olduğunu önemli toounderstand olduğu: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="5f8a3-110">Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarlarını](../azure-resource-manager/resource-manager-deployment-model.md) iyice anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="5f8a3-111">Bu makalenin hello üstünde hello sekmeleri tıklayarak farklı araçlarla ilgili hello belgeleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-111">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span>
>

<span data-ttu-id="5f8a3-112">Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-112">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="5f8a3-113">Ayrıca [Udr'ler hello Klasik dağıtım modelinde oluşturabilirsiniz](virtual-network-create-udr-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5f8a3-113">You can also [create UDRs in hello classic deployment model](virtual-network-create-udr-classic-ps.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="5f8a3-114">Merhaba örnek PowerShell önceden oluşturulmuş basit bir ortam aşağıdaki komutları beklediğiniz senaryosunda hello yukarıdaki temel.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-114">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="5f8a3-115">Bu belgede gösterildiği toorun hello komutları istiyorsanız, önce hello test ortamı dağıtarak yapı [bu şablonu](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), tıklatın **tooAzure dağıtmak**, hello varsayılan parametre değerlerini değiştirin Gerekirse ve izleme hello yönergelerinde portal hello durumunda.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="5f8a3-116">Merhaba UDR hello ön uç alt ağ için oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f8a3-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="5f8a3-117">Yukarıdaki adımları izleyerek tam hello hello senaryoya toocreate hello yol tablosu ve rota hello ön uç alt ağ için gereken temel:</span><span class="sxs-lookup"><span data-stu-id="5f8a3-117">toocreate hello route table and route needed for hello front-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="5f8a3-118">Tüm giden trafiğe toohello arka uç alt ağ (192.168.2.0/24) yönlendirilen toobe toohello kullanılan rota toosend oluşturma **FW1** sanal gereç (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="5f8a3-118">Create a route used toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToBackEnd `
    -AddressPrefix 192.168.2.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="5f8a3-119">Adlı bir yol tablosu oluşturmanız **UDR ön uç** hello içinde **westus** hello rota içeren bölge.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-119">Create a route table named **UDR-FrontEnd** in hello **westus** region that contains hello route.</span></span>

    ```powershell
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-FrontEnd -Route $route
    ```

3. <span data-ttu-id="5f8a3-120">Merhaba hello alt olduğu VNet içeren bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-120">Create a variable that contains hello VNet where hello subnet is.</span></span> <span data-ttu-id="5f8a3-121">Senaryomuzda hello VNet adlı **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-121">In our scenario, hello VNet is named **TestVNet**.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

4. <span data-ttu-id="5f8a3-122">İlişkilendirme hello yol tablosu toohello oluşturulan **ön uç** alt ağ.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-122">Associate hello route table created above toohello **FrontEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -RouteTable $routeTable
    ```

    > [!WARNING]
    > <span data-ttu-id="5f8a3-123">Yukarıdaki hello komutu için Hello çıktı hello içerik yalnızca PowerShell çalıştırdığınız hello bilgisayarda mevcut hello sanal ağ yapılandırma nesnesi için gösterilir.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-123">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="5f8a3-124">Toorun hello gereksinim **kümesi AzureVirtualNetwork** cmdlet toosave bu ayarları tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-124">You need toorun hello **Set-AzureVirtualNetwork** cmdlet toosave these settings tooAzure.</span></span>
    > 

5. <span data-ttu-id="5f8a3-125">Azure'da Hello yeni alt ağ yapılandırması kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-125">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="5f8a3-126">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="5f8a3-126">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                                ...,
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              },
                                ...
                            ]    

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="5f8a3-127">Merhaba UDR hello arka uç alt ağ için oluşturma</span><span class="sxs-lookup"><span data-stu-id="5f8a3-127">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="5f8a3-128">toocreate hello yol tablosu ve yukarıdaki hello senaryoyu temel hello arka uç alt ağ için gereken rota hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-128">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="5f8a3-129">Tüm giden trafiğe toohello ön uç alt ağı (192.168.1.0/24) yönlendirilen toobe toohello kullanılan rota toosend oluşturma **FW1** sanal gereç (192.168.0.4).</span><span class="sxs-lookup"><span data-stu-id="5f8a3-129">Create a route used toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toobe routed toohello **FW1** virtual appliance (192.168.0.4).</span></span>

    ```powershell
    $route = New-AzureRmRouteConfig -Name RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

2. <span data-ttu-id="5f8a3-130">Adlı bir yol tablosu oluşturmanız **UDR arka uç** hello içinde **uswest** hello rota içeren bölge oluşturulan üstünde.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-130">Create a route table named **UDR-BackEnd** in hello **uswest** region that contains hello route created above.</span></span>

    ```
    $routeTable = New-AzureRmRouteTable -ResourceGroupName TestRG -Location westus `
    -Name UDR-BackEnd -Route $route
    ```

3. <span data-ttu-id="5f8a3-131">İlişkilendirme hello yol tablosu toohello oluşturulan **arka uç** alt ağ.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-131">Associate hello route table created above toohello **BackEnd** subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd `
    -AddressPrefix 192.168.2.0/24 -RouteTable $routeTable
    ```

4. <span data-ttu-id="5f8a3-132">Azure'da Hello yeni alt ağ yapılandırması kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-132">Save hello new subnet configuration in Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="5f8a3-133">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="5f8a3-133">Expected output:</span></span>
   
        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : westus
        Id                : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              : 
                            Name         Value
                            ===========  =====
                            displayName  VNet 
   
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              ...,
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL2/ipConfigurations/ipconfig1"
                                  },
                                  {
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICSQL1/ipConfigurations/ipconfig1"
                                  }
                                ],
                                "NetworkSecurityGroup": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BacEnd"
                                },
                                "RouteTable": {
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd"
                                },
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="5f8a3-134">FW1 üstünde IP iletimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="5f8a3-134">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="5f8a3-135">Merhaba tarafından kullanılan NIC tooenable IP iletme **FW1**, hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-135">tooenable IP forwarding in hello NIC used by **FW1**, follow hello steps below.</span></span>

1. <span data-ttu-id="5f8a3-136">Merhaba FW1 tarafından kullanılan NIC hello ayarları içeren bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-136">Create a variable that contains hello settings for hello NIC used by FW1.</span></span> <span data-ttu-id="5f8a3-137">Senaryomuzda hello NIC adlı **NICFW1**.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-137">In our scenario, hello NIC is named **NICFW1**.</span></span>

    ```powershell
    $nicfw1 = Get-AzureRmNetworkInterface -ResourceGroupName TestRG -Name NICFW1
    ```

2. <span data-ttu-id="5f8a3-138">IP iletimini etkinleştirmeniz ve hello NIC ayarları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5f8a3-138">Enable IP forwarding, and save hello NIC settings.</span></span>

    ```powershell
    $nicfw1.EnableIPForwarding = 1
    Set-AzureRmNetworkInterface -NetworkInterface $nicfw1
    ```
   
    <span data-ttu-id="5f8a3-139">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="5f8a3-139">Expected output:</span></span>
   
        Name                 : NICFW1
        ResourceGroupName    : TestRG
        Location             : westus
        Id                   : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1
        Etag                 : W/"[Id]"
        ProvisioningState    : Succeeded
        Tags                 : 
                               Name         Value                  
                               ===========  =======================
                               displayName  NetworkInterfaces - DMZ
   
        VirtualMachine       : {
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/FW1"
                               }
        IpConfigurations     : [
                                 {
                                   "Name": "ipconfig1",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICFW1/ipConfigurations/ipconfig1",
                                   "PrivateIpAddress": "192.168.0.4",
                                   "PrivateIpAllocationMethod": "Static",
                                   "Subnet": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/DMZ"
                                   },
                                   "PublicIpAddress": {
                                     "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/PIPFW1"
                                   },
                                   "LoadBalancerBackendAddressPools": [],
                                   "LoadBalancerInboundNatRules": [],
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
        DnsSettings          : {
                                 "DnsServers": [],
                                 "AppliedDnsServers": [],
                                 "InternalDnsNameLabel": null,
                                 "InternalFqdn": null
                               }
        EnableIPForwarding   : True
        NetworkSecurityGroup : null
        Primary              : True

