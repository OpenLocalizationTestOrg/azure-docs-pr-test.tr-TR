---
title: "aaaOpen bağlantı noktalarını tooa Azure PowerShell kullanarak bir VM | Microsoft Docs"
description: "Bilgi nasıl tooopen bir bağlantı noktası / bir uç nokta tooyour Windows VM oluşturma hello Azure Kaynak Yöneticisi dağıtım modu ve Azure PowerShell kullanma"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a><span data-ttu-id="114dc-103">Nasıl tooopen bağlantı noktalarını ve uç noktaları tooa PowerShell kullanarak azure'da VM</span><span class="sxs-lookup"><span data-stu-id="114dc-103">How tooopen ports and endpoints tooa VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="114dc-104">Hızlı komutlar</span><span class="sxs-lookup"><span data-stu-id="114dc-104">Quick commands</span></span>
<span data-ttu-id="114dc-105">toocreate bir ağ güvenlik grubu ve ACL kurallarını ihtiyacınız [Azure PowerShell'in yüklü en son sürümünü hello](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="114dc-105">toocreate a Network Security Group and ACL rules you need [hello latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="114dc-106">Ayrıca [hello Azure portal kullanarak aşağıdaki adımları gerçekleştirin](nsg-quickstart-portal.md).</span><span class="sxs-lookup"><span data-stu-id="114dc-106">You can also [perform these steps using hello Azure portal](nsg-quickstart-portal.md).</span></span>

<span data-ttu-id="114dc-107">Azure hesabı tooyour oturum:</span><span class="sxs-lookup"><span data-stu-id="114dc-107">Log in tooyour Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="114dc-108">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="114dc-108">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="114dc-109">Örnek parametre adları dahil *myResourceGroup*, *myNetworkSecurityGroup*, ve *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="114dc-109">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="114dc-110">Bir kural oluştururken [yeni AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="114dc-110">Create a rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="114dc-111">Merhaba aşağıdaki örnek adlı bir kural oluşturur *myNetworkSecurityGroupRule* tooallow *tcp* bağlantı noktasında trafik *80*:</span><span class="sxs-lookup"><span data-stu-id="114dc-111">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow *tcp* traffic on port *80*:</span></span>

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

<span data-ttu-id="114dc-112">Ardından, ağ güvenlik grubu ile oluşturma [yeni AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) ve yeni oluşturduğunuz gibi Ata hello HTTP kural.</span><span class="sxs-lookup"><span data-stu-id="114dc-112">Next, create your Network Security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) and assign hello HTTP rule you just created as follows.</span></span> <span data-ttu-id="114dc-113">Merhaba aşağıdaki örnekte oluşturur adlı bir ağ güvenlik grubu *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="114dc-113">hello following example creates a Network Security Group named *myNetworkSecurityGroup*:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

<span data-ttu-id="114dc-114">Şimdi şimdi ağ güvenlik grubu tooa alt ağınızı atayın.</span><span class="sxs-lookup"><span data-stu-id="114dc-114">Now let's assign your Network Security Group tooa subnet.</span></span> <span data-ttu-id="114dc-115">Merhaba aşağıdaki örnek atar adlı varolan bir sanal ağ *myVnet* toohello değişkeni *$vnet* ile [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="114dc-115">hello following example assigns an existing virtual network named *myVnet* toohello variable *$vnet* with [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="114dc-116">Ağ güvenlik grubu, alt ağ ile ilişkilendirmek [kümesi AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="114dc-116">Associate your Network Security Group with your subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="114dc-117">Merhaba aşağıdaki örnek ilişkilendirir adlı hello alt *mySubnet* ağ güvenlik grubu ile:</span><span class="sxs-lookup"><span data-stu-id="114dc-117">hello following example associates hello subnet named *mySubnet* with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="114dc-118">Son olarak, sanal ağınızla güncelleştirme [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) sırada, değişiklikleri tootake efekti için:</span><span class="sxs-lookup"><span data-stu-id="114dc-118">Finally, update your virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) in order for your changes tootake effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="114dc-119">Ağ güvenlik grupları hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="114dc-119">More information on Network Security Groups</span></span>
<span data-ttu-id="114dc-120">Burada hızlı komutları Hello tooget yukarı ve trafik boyunca tooyour VM ile çalışmaya izin verir.</span><span class="sxs-lookup"><span data-stu-id="114dc-120">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="114dc-121">Ağ güvenlik grupları, birçok harika özellikler ve denetleme tooyour kaynaklara erişmek için ayrıntı düzeyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="114dc-121">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="114dc-122">Daha fazla bilgi edinebilirsiniz [bir ağ güvenlik grubu ve ACL oluşturma kuralları burada](tutorial-virtual-network.md#manage-internal-traffic).</span><span class="sxs-lookup"><span data-stu-id="114dc-122">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#manage-internal-traffic).</span></span>

<span data-ttu-id="114dc-123">Yüksek oranda kullanılabilir web uygulamaları için Azure yük dengeleyici arkasında Vm'leriniz yerleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="114dc-123">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="114dc-124">Merhaba yük dengeleyici trafik filtreleme sağlar bir ağ güvenlik grubuyla trafiği tooVMs dağıtır.</span><span class="sxs-lookup"><span data-stu-id="114dc-124">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="114dc-125">Daha fazla bilgi için bkz: [nasıl tooload Bakiye Linux sanal yüksek oranda kullanılabilir bir uygulama içinde Azure toocreate makineleri](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="114dc-125">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="114dc-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="114dc-126">Next steps</span></span>
<span data-ttu-id="114dc-127">Bu örnekte, bir basit kural tooallow HTTP trafiği oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="114dc-127">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="114dc-128">Aşağıdaki makaleleri hello ayrıntılı ortamları oluşturma hakkında bilgi bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="114dc-128">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="114dc-129">Azure Resource Manager'a genel bakış</span><span class="sxs-lookup"><span data-stu-id="114dc-129">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="114dc-130">Ağ Güvenlik Grubu (NSG) Nedir?</span><span class="sxs-lookup"><span data-stu-id="114dc-130">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="114dc-131">Yük Dengeleyiciler için Azure Resource Manager'a genel bakış</span><span class="sxs-lookup"><span data-stu-id="114dc-131">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

