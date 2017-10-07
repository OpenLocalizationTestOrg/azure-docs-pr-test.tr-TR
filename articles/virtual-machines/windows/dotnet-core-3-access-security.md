---
title: "aaaAccess Azure Şablonları Windows VM'ler için güvenlik ve | Microsoft Docs"
description: "Azure sanal makinesi DotNet çekirdek Öğreticisi"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4b8227ae745b3b0a22d136e98d18479f8b1504c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="8d172-103">Azure Resource Manager Şablonları Windows VM'ler için güvenlik ve erişim</span><span class="sxs-lookup"><span data-stu-id="8d172-103">Access and security in Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="8d172-104">Barındırılan uygulamalarını Azure büyük olasılıkla toobe erişmeniz içinde hello internet veya VPN / Azure ile hızlı Rota bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="8d172-104">Applications hosted in Azure likely need toobe access over hello internet or a VPN / Express Route connection with Azure.</span></span> <span data-ttu-id="8d172-105">Merhaba müzik deposu uygulama örnekle hello web sitesi üzerinde kullanılabilir hale Internet bir ortak IP adresi ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="8d172-105">With hello Music Store application sample, hello web site is made available on hello internet with a public IP address.</span></span> <span data-ttu-id="8d172-106">Oluşturulan erişimle bağlantıları toohello uygulama ve erişim toohello sanal makine kaynakları kendilerini güvenli hale getirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="8d172-106">With access established, connections toohello application and access toohello virtual machine resources themselves should be secured.</span></span> <span data-ttu-id="8d172-107">Bu erişim güvenliği bir ağ güvenlik grubu ile sağlanır.</span><span class="sxs-lookup"><span data-stu-id="8d172-107">This access security is provided with a Network Security Group.</span></span> 

<span data-ttu-id="8d172-108">Bu belge hello müzik deposu uygulama hello örnek Azure Resource Manager şablonunda güvenliği nasıl ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8d172-108">This document details how hello Music Store application is secured in hello sample Azure Resource Manager template.</span></span> <span data-ttu-id="8d172-109">Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="8d172-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="8d172-110">Merhaba en iyi deneyim için önceden hello çözüm tooyour Azure aboneliği ve hello Azure Resource Manager şablonu ile birlikte çalışma örneği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="8d172-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="8d172-111">Merhaba tam şablon burada – bulunabilir [müzik deposu dağıtım Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="8d172-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="public-ip-address"></a><span data-ttu-id="8d172-112">Genel IP adresi</span><span class="sxs-lookup"><span data-stu-id="8d172-112">Public IP Address</span></span>
<span data-ttu-id="8d172-113">tooprovide genel erişim tooan Azure kaynak, bir ortak IP adresi kaynağı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8d172-113">tooprovide public access tooan Azure resource, a public IP address resource can be used.</span></span> <span data-ttu-id="8d172-114">Genel IP adresi statik veya dinamik IP adresi ile yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8d172-114">Public IP address can be configured with a static or dynamic IP address.</span></span> <span data-ttu-id="8d172-115">Bir dinamik adres kullanılır ve hello sanal makine durdurulmuş ve serbest, hello adresleri kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="8d172-115">If a dynamic address is used, and hello virtual machine is stopped and deallocated, hello addresses is removed.</span></span> <span data-ttu-id="8d172-116">Merhaba makine yeniden başlatıldığında, farklı bir ortak IP adresi atanmış.</span><span class="sxs-lookup"><span data-stu-id="8d172-116">When hello machine is started again, it may be assigned a different public IP address.</span></span> <span data-ttu-id="8d172-117">tooprevent bir IP adresini değiştirmesini, ayrılmış bir IP adresi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8d172-117">tooprevent an IP address from changing, a reserved IP address can be used.</span></span> 

<span data-ttu-id="8d172-118">Bir ortak IP adresi tooan Azure Resource Manager şablonu hello Visual Studio ekleme yeni kaynak Sihirbazı kullanılarak eklenebilir veya bir şablona geçerli JSON ekleyerek.</span><span class="sxs-lookup"><span data-stu-id="8d172-118">A Public IP Address can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span> 

<span data-ttu-id="8d172-119">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [genel IP adresi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span><span class="sxs-lookup"><span data-stu-id="8d172-119">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

<span data-ttu-id="8d172-120">Bir ortak IP adresi, bir sanal ağ bağdaştırıcısı veya bir yük dengeleyici ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="8d172-120">A Public IP Address can be associated with a Virtual Network Adapter, or a Load Balancer.</span></span> <span data-ttu-id="8d172-121">Merhaba müzik deposu Web sitesi birden fazla sanal makine genelinde dengelendiği olduğundan bu örnekte, ekli toohello yük dengeleyici hello genel IP adresi değildir.</span><span class="sxs-lookup"><span data-stu-id="8d172-121">In this example, because hello Music Store website is load balanced across several virtual machines, hello Public IP Address is attached toohello Load Balancer.</span></span>

<span data-ttu-id="8d172-122">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [yük dengeleyici genel IP adresi ilişkilendirmesini](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span><span class="sxs-lookup"><span data-stu-id="8d172-122">Follow this link toosee hello JSON sample within hello Resource Manager template – [Public IP Address association with Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="8d172-123">Merhaba ortak IP adresi olarak hello Azure portal görülür.</span><span class="sxs-lookup"><span data-stu-id="8d172-123">hello public IP Address as seen from hello Azure portal.</span></span> <span data-ttu-id="8d172-124">Merhaba genel IP adresi ilişkili tooa yük dengeleyicisi ve sanal makine olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="8d172-124">Notice that hello public IP address is associated tooa load balancer and not a virtual machine.</span></span> <span data-ttu-id="8d172-125">Ağ Yük Dengeleyici hello sonraki bu seri belgede ayrıntılı olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="8d172-125">Network load balancers are detailed in hello next document of this series.</span></span>

![Genel IP adresi](./media/dotnet-core-3-access-security/pubip-win.png)

<span data-ttu-id="8d172-127">Azure ortak IP adresleri hakkında daha fazla bilgi için bkz: [azure'daki IP adresleri](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8d172-127">For more information on Azure Public IP Addresses, see [IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>

## <a name="network-security-group"></a><span data-ttu-id="8d172-128">Ağ güvenlik grubu</span><span class="sxs-lookup"><span data-stu-id="8d172-128">Network Security Group</span></span>
<span data-ttu-id="8d172-129">Erişim kurulan tooAzure kaynakları silindikten sonra bu erişim sınırlandırılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8d172-129">Once access has been established tooAzure resources, this access should be limited.</span></span> <span data-ttu-id="8d172-130">Azure sanal makineler için bir ağ güvenlik grubu kullanılarak güvenli erişim elde edilir.</span><span class="sxs-lookup"><span data-stu-id="8d172-130">For Azure virtual machines, secure access is accomplished using a network security group.</span></span> <span data-ttu-id="8d172-131">Merhaba müzik deposu uygulama örneği ile tüm erişim toohello sanal makine http erişimi için bağlantı noktası 80 ve RDP erişim 3389 numaralı bağlantı noktası üzerinden dışında sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="8d172-131">With hello Music Store application sample, all access toohello virtual machine is restricted except for over port 80 for http access, and port 3389 for RDP access.</span></span> <span data-ttu-id="8d172-132">Bir ağ güvenlik grubu tooan Azure Resource Manager şablonu hello Visual Studio ekleme yeni kaynak Sihirbazı kullanılarak eklenebilir veya bir şablona geçerli JSON ekleyerek.</span><span class="sxs-lookup"><span data-stu-id="8d172-132">A Network Security Group can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or by inserting valid JSON into a template.</span></span>

<span data-ttu-id="8d172-133">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [ağ güvenlik grubu](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span><span class="sxs-lookup"><span data-stu-id="8d172-133">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).</span></span>

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

<span data-ttu-id="8d172-134">Bu örnekte, hello ağ güvenlik grubu hello sanal ağ kaynak bildirilen hello alt ağ nesnesini ilişkilendirmek ' dir.</span><span class="sxs-lookup"><span data-stu-id="8d172-134">In this example, hello network security group is associate with hello subnet object declared in hello Virtual Network resource.</span></span> 

<span data-ttu-id="8d172-135">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [sanal ağ ile ağ güvenlik grubu ilişkilendirmesini](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span><span class="sxs-lookup"><span data-stu-id="8d172-135">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Security Group association with Virtual Network](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).</span></span>

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
]
```

<span data-ttu-id="8d172-136">İşte hangi hello ağ güvenlik grubu gibi hello Azure portalında görünür.</span><span class="sxs-lookup"><span data-stu-id="8d172-136">Here is what hello network security group looks like from hello Azure portal.</span></span> <span data-ttu-id="8d172-137">Bir NSG'yi bir alt ağ veya ağ arabirimi ile ilişkilendirmek dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="8d172-137">Notice that an NSG can be associate with a subnet and / or network interface.</span></span> <span data-ttu-id="8d172-138">Bu durumda, hello NSG ilişkili tooa alt değil.</span><span class="sxs-lookup"><span data-stu-id="8d172-138">In this case, hello NSG is associated tooa subnet.</span></span> <span data-ttu-id="8d172-139">Bu yapılandırmada, hello gelen kuralları tooall bağlı sanal makineleri toohello alt uygulayın.</span><span class="sxs-lookup"><span data-stu-id="8d172-139">In this configuration, hello inbound rules apply tooall virtual machines connected toohello subnet.</span></span>

![Ağ güvenlik grubu](./media/dotnet-core-3-access-security/nsg-win.png)

<span data-ttu-id="8d172-141">Ağ güvenlik grupları hakkında ayrıntılı bilgi için bkz: [bir ağ güvenlik grubu nedir](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span><span class="sxs-lookup"><span data-stu-id="8d172-141">For in-depth information on Network Security Groups, see [What is a Network Security Group](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).</span></span>

## <a name="next-step"></a><span data-ttu-id="8d172-142">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="8d172-142">Next step</span></span>
<hr>

[<span data-ttu-id="8d172-143">3. adım - kullanılabilirliğini ve ölçeğini Azure Resource Manager şablonlarındaki</span><span class="sxs-lookup"><span data-stu-id="8d172-143">Step 3 - Availability and Scale in Azure Resource Manager Templates</span></span>](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

