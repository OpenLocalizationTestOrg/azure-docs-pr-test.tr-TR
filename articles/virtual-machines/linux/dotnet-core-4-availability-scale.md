---
title: "Kullanılabilirlik ve ölçek Azure Resource Manager şablonlarındaki | Microsoft Docs"
description: "Azure sanal makinesi DotNet çekirdek Öğreticisi"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8fcfea79-f017-4658-8c51-74242fcfb7f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0c0250b8152ed31b9a5d8b42ae139c9b38da0984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="2e881-103">Kullanılabilirlik ve ölçek Linux VM'ler için Azure Resource Manager şablonlarındaki</span><span class="sxs-lookup"><span data-stu-id="2e881-103">Availability and scale in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="2e881-104">Kullanılabilirlik ve ölçek açık kalma süresi ve isteğe bağlı Karşılama becerisini bakın.</span><span class="sxs-lookup"><span data-stu-id="2e881-104">Availability and scale refer to uptime and the ability to meet demand.</span></span> <span data-ttu-id="2e881-105">Bir uygulama süresi % 99,9 çalışma olması gerekiyorsa, birden çok eşzamanlı işlem kaynaklarını izin veren bir mimari olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2e881-105">If an application must be up 99.9% of the time, it needs to have an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="2e881-106">Örneği için tek bir Web sitesi yerine, daha yüksek düzeyde kullanılabilirlik yapılandırmasıyla bunları önünde teknolojisi Dengeleme ile aynı sitede birden çok örneğini içerir.</span><span class="sxs-lookup"><span data-stu-id="2e881-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of the same site, with balancing technology in front of them.</span></span> <span data-ttu-id="2e881-107">Kalan devam ederken çalışabilmesi bu yapılandırmada, uygulamanın bir örneği bakım için alınabilir.</span><span class="sxs-lookup"><span data-stu-id="2e881-107">In this configuration, one instance of the application can be taken down for maintenance, while the remaining continue to function.</span></span> <span data-ttu-id="2e881-108">Ölçek, diğer yandan isteğe hizmet verecek bir uygulama yeteneği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="2e881-108">Scale on the other hand refers to an applications ability to serve demand.</span></span> <span data-ttu-id="2e881-109">Bir yük dengeli uygulama ekleme veya örnekleri havuzdan kaldırma talebi karşılamak üzere ölçeklendirmek bir uygulama sağlar.</span><span class="sxs-lookup"><span data-stu-id="2e881-109">With a load balanced application, adding or removing instances from the pool allows an application to scale to meet demand.</span></span>

<span data-ttu-id="2e881-110">Bu belge, müzik deposu örnek dağıtım kullanılabilirliğini ve ölçeğini için nasıl yapılandırılacağı ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="2e881-110">This document details how the Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="2e881-111">Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="2e881-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="2e881-112">En iyi deneyim için Azure aboneliği ve Azure Resource Manager şablonu ile birlikte çalışma çözümü örneği önceden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="2e881-112">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="2e881-113">Tam veri şablonunun burada – bulunabilir [Ubuntu müzik deposu dağıtımı](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="2e881-113">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="availability-set"></a><span data-ttu-id="2e881-114">Kullanılabilirlik Kümesi</span><span class="sxs-lookup"><span data-stu-id="2e881-114">Availability Set</span></span>
<span data-ttu-id="2e881-115">Bir kullanılabilirlik kümesi mantıksal olarak Azure sanal makineleri fiziksel ana bilgisayarlar ve güç kaynakları ve fiziksel ağ donanımı gibi diğer infrastructural bileşenleri kapsar.</span><span class="sxs-lookup"><span data-stu-id="2e881-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="2e881-116">Kullanılabilirlik kümeleri bakım, aygıt hatası veya diğer kesinti sırasında tüm sanal makineleri etkilenir emin olun.</span><span class="sxs-lookup"><span data-stu-id="2e881-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="2e881-117">Visual Studio yeni kaynak Ekle Sihirbazı kullanarak veya bir şablona geçerli JSON ekleyerek bir Azure Resource Manager şablonu bir kullanılabilirlik kümesi eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="2e881-117">An Availability Set can be added to an Azure Resource Manager template using the Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="2e881-118">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [kullanılabilirlik kümesi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span><span class="sxs-lookup"><span data-stu-id="2e881-118">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "avalibility-set"
  },
  "properties": {
    "platformUpdateDomainCount": 5,
    "platformFaultDomainCount": 3
  }
}
```

<span data-ttu-id="2e881-119">Bir kullanılabilirlik kümesi, bir sanal makine kaynağı özelliği olarak bildirilir.</span><span class="sxs-lookup"><span data-stu-id="2e881-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="2e881-120">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [sanal makine kullanılabilirlik kümesi ilişkilendirmesini](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span><span class="sxs-lookup"><span data-stu-id="2e881-120">Follow this link to see the JSON sample within the Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="2e881-121">Kullanılabilirlik Azure portalından görülen kümesi.</span><span class="sxs-lookup"><span data-stu-id="2e881-121">The availability set as seen from the Azure portal.</span></span> <span data-ttu-id="2e881-122">Her bir sanal makine ve yapılandırması hakkında ayrıntılar aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2e881-122">Each virtual machine and details about the configuration are detailed here.</span></span>

![Kullanılabilirlik Kümesi](./media/dotnet-core-4-availability-scale/aset.png)

<span data-ttu-id="2e881-124">Kullanılabilirlik kümeleri hakkında ayrıntılı bilgi için bkz: [sanal makinelerin kullanılabilirliğini yönetme](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e881-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="2e881-125">Ağ Yükü Dengeleyici</span><span class="sxs-lookup"><span data-stu-id="2e881-125">Network Load Balancer</span></span>
<span data-ttu-id="2e881-126">Bir kullanılabilirlik kümesi uygulama hata toleransı sağlar ancak bir yük dengeleyici uygulamasının birçok örneklerini tek bir ağ adresi üzerinde kullanılabilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="2e881-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of the application available on a single network address.</span></span> <span data-ttu-id="2e881-127">Bir uygulama birden çok örneğini birçok sanal makinelerde, her biri bir yük dengeleyiciye bağlı barındırılabilir.</span><span class="sxs-lookup"><span data-stu-id="2e881-127">Multiple instances of an application can be hosted on many virtual machines, each one connected to a load balancer.</span></span> <span data-ttu-id="2e881-128">Uygulama erişilen gibi yük dengeleyici ekli üyeleri arasında gelen isteği yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="2e881-128">As the application is accessed, the load balancer routes the incoming request across the attached members.</span></span> <span data-ttu-id="2e881-129">Bir yük dengeleyici Visual Studio yeni kaynak Ekleme Sihirbazı kullanılarak eklenebilir veya düzgün ekleyerek JSON kaynak Azure Resource Manager şablonuna biçimlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="2e881-129">A Load Balancer can be added using the Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into the Azure Resource Manager template.</span></span>

<span data-ttu-id="2e881-130">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [Ağ Yük Dengeleyici](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="2e881-130">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-front"
  },
  ........<truncated>
}
```

<span data-ttu-id="2e881-131">Örnek uygulama bir ortak IP adresi ile Internet'e açık olduğu için bu yük dengeleyici ile ilişkili bir adresidir.</span><span class="sxs-lookup"><span data-stu-id="2e881-131">Because the sample application is exposed to the internet with a public IP address, this address is associated with the load balancer.</span></span> 

<span data-ttu-id="2e881-132">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [genel IP adresi ile Ağ Yük Dengeleyici ilişkilendirmesini](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span><span class="sxs-lookup"><span data-stu-id="2e881-132">Follow this link to see the JSON sample within the Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span></span>

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

<span data-ttu-id="2e881-133">Azure portalından, Ağ Yük Dengeleyici genel bakış genel IP adresi ile ilişkilendirme gösterir.</span><span class="sxs-lookup"><span data-stu-id="2e881-133">From the Azure portal, the network load balancer overview shows the association with the public IP address.</span></span>

![Ağ Yükü Dengeleyici](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="2e881-135">Yük Dengeleyici kuralı</span><span class="sxs-lookup"><span data-stu-id="2e881-135">Load Balancer Rule</span></span>
<span data-ttu-id="2e881-136">Bir yük dengeleyici kullanırken, kuralları trafiği arasında hedeflenen kaynakların nasıl dengelenir denetleyen yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="2e881-136">When using a load balancer, rules are configured that control how traffic is balanced across the intended resources.</span></span> <span data-ttu-id="2e881-137">Örnek Müzik deposu uygulamayla trafiği ortak IP adresinin 80 bağlantı noktasına ulaşan ve 80 numaralı bağlantı noktasını, tüm sanal makineler arasında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="2e881-137">With the sample Music Store application, traffic arrives on port 80 of the public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="2e881-138">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [yük dengeleyici kuralı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="2e881-138">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span>

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

<span data-ttu-id="2e881-139">Ağ Yük Dengeleyici kuralı portalından görünümü.</span><span class="sxs-lookup"><span data-stu-id="2e881-139">A view of the network load balancer rule from the portal.</span></span>

![Ağ Yük Dengeleyici kuralı](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="2e881-141">Yük Dengeleyici araştırması</span><span class="sxs-lookup"><span data-stu-id="2e881-141">Load Balancer Probe</span></span>
<span data-ttu-id="2e881-142">Yük dengeleyicinin istekleri yalnızca sistemlerini çalıştıran için sunulan böylece her bir sanal makine izlemek de gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e881-142">The load balancer also needs to monitor each virtual machine so that requests are served only to running systems.</span></span> <span data-ttu-id="2e881-143">Bu izleme, sabit önceden tanımlı bir bağlantı yoklama yerini alır.</span><span class="sxs-lookup"><span data-stu-id="2e881-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="2e881-144">Müzik deposu dağıtımı dahil tüm sanal makineler üzerinde bağlantı noktası 80 araştırma için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="2e881-144">The Music Store deployment is configured to probe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="2e881-145">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [yük dengeleyici araştırması](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span><span class="sxs-lookup"><span data-stu-id="2e881-145">Follow this link to see the JSON sample within the Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span></span>

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

<span data-ttu-id="2e881-146">Yük Dengeleyici araştırmasını Azure portalından görülür.</span><span class="sxs-lookup"><span data-stu-id="2e881-146">The load balancer probe seen from the Azure portal.</span></span>

![Ağ Yük Dengeleyici araştırması](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="2e881-148">Gelen NAT Kuralları</span><span class="sxs-lookup"><span data-stu-id="2e881-148">Inbound NAT Rules</span></span>
<span data-ttu-id="2e881-149">Bir yük dengeleyici kullanırken, kuralları her sanal makineye olmayan yük dengeli erişim sağlayan yere yerleştirin gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e881-149">When using a Load Balancer, rules need to be put into place that provide non-load balanced access to each Virtual Machine.</span></span> <span data-ttu-id="2e881-150">Örneğin, bir SSH bağlantısı ile her bir sanal makine oluştururken, bu trafiği yükü dengelenmiş olmamalıdır, önceden belirlenen bir yol yerine yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e881-150">For instance, when creating an SSH connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="2e881-151">Önceden belirlenen yolları, bir gelen NAT kuralı kaynağı kullanılarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="2e881-151">pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="2e881-152">Bu kaynağı kullanan, tek tek sanal makinelere gelen iletişimi eşlenebilir.</span><span class="sxs-lookup"><span data-stu-id="2e881-152">Using this resource, inbound communication can be mapped to individual Virtual Machines.</span></span> 

<span data-ttu-id="2e881-153">Müzik mağazası uygulaması ile 5000 başlayan bir bağlantı noktası bağlantı noktası 22 her sanal makineye SSH erişim eşleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2e881-153">With the Music Store application, a port starting at 5000 is mapped to port 22 on each Virtual Machine for SSH access.</span></span> <span data-ttu-id="2e881-154">`copyindex()` İşlevi, ikinci bir sanal makinede 5001, üçüncü 5002 gelen bir bağlantı noktası alır, gelen bağlantı noktası artırmak üzere kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2e881-154">The `copyindex()` function is used to increment the incoming port, such that the second Virtual Machine receives an incoming port of 5001, the third 5002, and so on.</span></span> 

<span data-ttu-id="2e881-155">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [gelen NAT kuralları](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="2e881-155">Follow this link to see the JSON sample within the Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span> 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'SSH-VM', copyIndex())]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 22,
    "enableFloatingIP": false
  }
}
```

<span data-ttu-id="2e881-156">Azure portalında göründüğü gibi bir örnek gelen NAT kuralı.</span><span class="sxs-lookup"><span data-stu-id="2e881-156">One example inbound NAT rule as seen in the Azure portal.</span></span> <span data-ttu-id="2e881-157">Dağıtımdaki her bir sanal makine için bir SSH NAT kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2e881-157">An SSH NAT rule is created for each virtual machine in the deployment.</span></span>

![Gelen NAT kuralı](./media/dotnet-core-4-availability-scale/natrule.png)

<span data-ttu-id="2e881-159">Azure Ağ Yük Dengeleyici hakkında ayrıntılı bilgi için bkz: [Yük Dengeleme için Azure altyapı hizmetleri](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e881-159">For in-depth information on the Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="2e881-160">Birden çok VM dağıtma</span><span class="sxs-lookup"><span data-stu-id="2e881-160">Deploy multiple VMs</span></span>
<span data-ttu-id="2e881-161">Son olarak, bir kullanılabilirlik kümesi veya yük dengeleyici için etkili bir şekilde çalışması, birden çok sanal makine gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2e881-161">Finally, for an Availability Set or Load Balancer to effectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="2e881-162">Birden çok VM Azure Resource Manager şablonunu Kopyala işlevi kullanılarak dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="2e881-162">Multiple VMs can be deployed using the Azure Resource Manager template copy function.</span></span> <span data-ttu-id="2e881-163">Kopyalama işlevi kullanarak, sınırlı sayıda sanal makine tanımlamak gerekli değildir, bunun yerine bu değer dinamik olarak dağıtım zamanında sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2e881-163">Using the copy function, it is not necessary to define a finite number of Virtual Machines, rather this value can be dynamically provided at the time of deployment.</span></span> <span data-ttu-id="2e881-164">Kopyalama işlevi oluşturulan örneklerinin sayısını ve sanal makineleri ve ilişkili kaynakları doğru sayıda dağıtma tanıtıcıları tüketir.</span><span class="sxs-lookup"><span data-stu-id="2e881-164">The copy function consumes the number of instances to created and handles deploying the proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="2e881-165">Müzik deposu örnek şablonunda bir parametre alan bir örnek sayısı tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="2e881-165">In the Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="2e881-166">Bu sayı, sanal makineler ve ilgili kaynakları oluştururken şablonu kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2e881-166">This number is used throughout the template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances to be created behind load balancer."
  }
}
```

<span data-ttu-id="2e881-167">Sanal makine kaynakta kopyalama döngüsü, bir ad ve sonuçta elde edilen kopya sayısını kontrol etmek için kullanılan örnekleri parametre sayısı verilir.</span><span class="sxs-lookup"><span data-stu-id="2e881-167">On the Virtual Machine resource, the copy loop is given a name and the number of instances parameter used to control the number of resulting copies.</span></span>

<span data-ttu-id="2e881-168">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [sanal makine kopyalama işlevi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span><span class="sxs-lookup"><span data-stu-id="2e881-168">Follow this link to see the JSON sample within the Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span></span> 

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Compute/virtualMachines",
"name": "[concat(variables('vmName'),copyindex())]",
"location": "[resourceGroup().location]",
"copy": {
  "name": "virtualMachineLoop",
  "count": "[parameters('numberOfInstances')]"
}
```

<span data-ttu-id="2e881-169">Kopyalama işlevi geçerli yineleme ile erişilebilir `copyIndex()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="2e881-169">The current iteration of the copy function can be accessed with the `copyIndex()` function.</span></span> <span data-ttu-id="2e881-170">Kopyalama dizin işlevi değeri, sanal makineler ve diğer kaynakları adlandırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2e881-170">The value of the copy index function can be used to name virtual machines and other resources.</span></span> <span data-ttu-id="2e881-171">Örneğin, bir sanal makinenin iki kopyası dağıtılırsa, farklı adlar gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e881-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="2e881-172">`copyIndex()` İşlevi benzersiz bir ad oluşturmak için sanal makine adının bir parçası olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2e881-172">The `copyIndex()` function can be used as part of the virtual machine name to create a unique name.</span></span> <span data-ttu-id="2e881-173">Bir örneği `copyindex()` işlevi amacıyla adlandırmak için kullanılan sanal makine kaynak görülen.</span><span class="sxs-lookup"><span data-stu-id="2e881-173">An example of the `copyindex()` function used for naming purposes can be seen in the Virtual Machine resource.</span></span> <span data-ttu-id="2e881-174">Burada, bilgisayar adının bir birleşimini olduğundan `vmName` parametresi ve `copyIndex()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="2e881-174">Here, the computer name is a concatenation of the `vmName` parameter, and the `copyIndex()` function.</span></span> 

<span data-ttu-id="2e881-175">Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [kopyalama dizin işlevi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span><span class="sxs-lookup"><span data-stu-id="2e881-175">Follow this link to see the JSON sample within the Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span></span> 

```json
"osProfile": {
  "computerName": "[concat(parameters('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "linuxConfiguration": {
    "disablePasswordAuthentication": "true",
    "ssh": {
      "publicKeys": [
        {
          "path": "[variables('sshKeyPath')]",
          "keyData": "[parameters('sshKeyData')]"
        }
      ]
    }
  }
}
```

<span data-ttu-id="2e881-176">`copyIndex` İşlevi birkaç kez müzik deposu örnek şablonunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2e881-176">The `copyIndex` function is used several times in the Music Store sample template.</span></span> <span data-ttu-id="2e881-177">Kaynakları ve işlevleri kullanılarak `copyIndex` herhangi işlevlere bağlıdır ve ağ arabirimi, yük dengeleyici kuralları gibi sanal makine tek bir örneği için belirli bir şey içerir.</span><span class="sxs-lookup"><span data-stu-id="2e881-177">Resources and functions utilizing `copyIndex` include anything specific to a single instance of the virtual machine such as network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="2e881-178">Kopyalama işlevi ile ilgili daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="2e881-178">For more information on the copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="2e881-179">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="2e881-179">Next step</span></span>
<hr>

[<span data-ttu-id="2e881-180">4. adım - Azure Resource Manager şablonları ile uygulama dağıtımı</span><span class="sxs-lookup"><span data-stu-id="2e881-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

