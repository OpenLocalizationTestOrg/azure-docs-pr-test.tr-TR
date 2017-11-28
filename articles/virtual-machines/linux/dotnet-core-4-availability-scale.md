---
title: "aaaAvailability ve Azure Resource Manager şablonlarındaki ölçek | Microsoft Docs"
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
ms.openlocfilehash: 6f830ca0a64e6b65859312bdf31dc0af59e2b978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="8f090-103">Kullanılabilirlik ve ölçek Linux VM'ler için Azure Resource Manager şablonlarındaki</span><span class="sxs-lookup"><span data-stu-id="8f090-103">Availability and scale in Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="8f090-104">Kullanılabilirlik ve ölçek toouptime ve hello özelliği toomeet talep bakın.</span><span class="sxs-lookup"><span data-stu-id="8f090-104">Availability and scale refer toouptime and hello ability toomeet demand.</span></span> <span data-ttu-id="8f090-105">Bir uygulama hello süre % 99,9 çalışma olması gerekiyorsa toohave birden çok eşzamanlı işlem kaynaklarını izin veren bir mimari gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f090-105">If an application must be up 99.9% of hello time, it needs toohave an architecture that allows for multiple concurrent compute resources.</span></span> <span data-ttu-id="8f090-106">Örneğin, tek bir Web sitesi yerine, daha yüksek düzeyde kullanılabilirlik yapılandırmasıyla aynı, bunları önünde teknolojisi Dengeleme ile site hello birden çok örneğini içerir.</span><span class="sxs-lookup"><span data-stu-id="8f090-106">For instance, rather than having a single website, a configuration with a higher level of availability includes multiple instances of hello same site, with balancing technology in front of them.</span></span> <span data-ttu-id="8f090-107">Kalan hello toofunction devam ederken bu yapılandırmada, hello uygulamanın bir örneği bakım için alınabilir.</span><span class="sxs-lookup"><span data-stu-id="8f090-107">In this configuration, one instance of hello application can be taken down for maintenance, while hello remaining continue toofunction.</span></span> <span data-ttu-id="8f090-108">Ölçek hello diğer yandan tooan uygulamaları özelliği tooserve isteğe başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="8f090-108">Scale on hello other hand refers tooan applications ability tooserve demand.</span></span> <span data-ttu-id="8f090-109">Bir yük dengeli uygulama ekleme veya örnekleri hello havuzdan kaldırma bir uygulama tooscale toomeet isteğe bağlı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8f090-109">With a load balanced application, adding or removing instances from hello pool allows an application tooscale toomeet demand.</span></span>

<span data-ttu-id="8f090-110">Bu belge hello müzik deposu örnek dağıtım kullanılabilirliğini ve ölçeğini için nasıl yapılandırılacağı ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8f090-110">This document details how hello Music Store sample deployment is configured for availability and scale.</span></span> <span data-ttu-id="8f090-111">Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır.</span><span class="sxs-lookup"><span data-stu-id="8f090-111">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="8f090-112">Merhaba en iyi deneyim için önceden hello çözüm tooyour Azure aboneliği ve hello Azure Resource Manager şablonu ile birlikte çalışma örneği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="8f090-112">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="8f090-113">Merhaba tam şablon burada – bulunabilir [Ubuntu müzik deposu dağıtımı](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="8f090-113">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="availability-set"></a><span data-ttu-id="8f090-114">Kullanılabilirlik Kümesi</span><span class="sxs-lookup"><span data-stu-id="8f090-114">Availability Set</span></span>
<span data-ttu-id="8f090-115">Bir kullanılabilirlik kümesi mantıksal olarak Azure sanal makineleri fiziksel ana bilgisayarlar ve güç kaynakları ve fiziksel ağ donanımı gibi diğer infrastructural bileşenleri kapsar.</span><span class="sxs-lookup"><span data-stu-id="8f090-115">An Availability Set logically spans Azure Virtual Machines across physical hosts and other infrastructural components such as power supplies and physical networking hardware.</span></span> <span data-ttu-id="8f090-116">Kullanılabilirlik kümeleri bakım, aygıt hatası veya diğer kesinti sırasında tüm sanal makineleri etkilenir emin olun.</span><span class="sxs-lookup"><span data-stu-id="8f090-116">Availability sets ensure that during maintenance, device failure, or other down time, not all virtual machines are effected.</span></span> <span data-ttu-id="8f090-117">Bir kullanılabilirlik kümesi hello Visual Studio yeni kaynak Ekle Sihirbazı kullanarak veya bir şablona geçerli JSON ekleme tooan Azure Resource Manager şablonu eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="8f090-117">An Availability Set can be added tooan Azure Resource Manager template using hello Visual Studio Add New Resource Wizard, or inserting valid JSON into a template.</span></span>

<span data-ttu-id="8f090-118">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [kullanılabilirlik kümesi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span><span class="sxs-lookup"><span data-stu-id="8f090-118">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).</span></span>

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

<span data-ttu-id="8f090-119">Bir kullanılabilirlik kümesi, bir sanal makine kaynağı özelliği olarak bildirilir.</span><span class="sxs-lookup"><span data-stu-id="8f090-119">An Availability Set is declared as a property of a Virtual Machine resource.</span></span> 

<span data-ttu-id="8f090-120">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [sanal makine kullanılabilirlik kümesi ilişkilendirmesini](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span><span class="sxs-lookup"><span data-stu-id="8f090-120">Follow this link toosee hello JSON sample within hello Resource Manager template – [Availability Set association with Virtual Machine](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).</span></span>

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
<span data-ttu-id="8f090-121">Merhaba kullanılabilirlik Hello Azure portal ' görüldüğü şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8f090-121">hello availability set as seen from hello Azure portal.</span></span> <span data-ttu-id="8f090-122">Her bir sanal makine ve hello yapılandırma ayrıntılarını burada açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8f090-122">Each virtual machine and details about hello configuration are detailed here.</span></span>

![Kullanılabilirlik Kümesi](./media/dotnet-core-4-availability-scale/aset.png)

<span data-ttu-id="8f090-124">Kullanılabilirlik kümeleri hakkında ayrıntılı bilgi için bkz: [sanal makinelerin kullanılabilirliğini yönetme](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f090-124">For in-depth information on Availability Sets, see [Manage availability of virtual machines](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

## <a name="network-load-balancer"></a><span data-ttu-id="8f090-125">Ağ Yükü Dengeleyici</span><span class="sxs-lookup"><span data-stu-id="8f090-125">Network Load Balancer</span></span>
<span data-ttu-id="8f090-126">Bir kullanılabilirlik kümesi uygulama hata toleransı sağlar ancak bir yük dengeleyici Merhaba uygulaması birçok örneklerini tek bir ağ adresi üzerinde kullanılabilmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8f090-126">Whereas an availability set provides application fault tolerance, a load balancer makes many instances of hello application available on a single network address.</span></span> <span data-ttu-id="8f090-127">Bir uygulama birden çok örneğini barındırılan birçok sanal makinelerde, her biri bağlı tooa yük dengeleyici.</span><span class="sxs-lookup"><span data-stu-id="8f090-127">Multiple instances of an application can be hosted on many virtual machines, each one connected tooa load balancer.</span></span> <span data-ttu-id="8f090-128">Merhaba uygulaması erişildiği gibi hello yük dengeleyici yollar bağlı hello üyeleri arasında gelen isteği hello.</span><span class="sxs-lookup"><span data-stu-id="8f090-128">As hello application is accessed, hello load balancer routes hello incoming request across hello attached members.</span></span> <span data-ttu-id="8f090-129">Bir yük dengeleyici hello Visual Studio yeni kaynak Ekleme Sihirbazı kullanılarak eklenebilir veya düzgün ekleyerek JSON kaynak hello Azure Resource Manager şablonuna biçimlendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="8f090-129">A Load Balancer can be added using hello Visual Studio Add New Resource Wizard, or by inserting properly formatted JSON resource into hello Azure Resource Manager template.</span></span>

<span data-ttu-id="8f090-130">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [Ağ Yük Dengeleyici](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span><span class="sxs-lookup"><span data-stu-id="8f090-130">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).</span></span>

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

<span data-ttu-id="8f090-131">Merhaba örnek uygulaması gösterilen toohello olduğundan Internet genel bir IP adresi ile bu adresi hello yük dengeleyici ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="8f090-131">Because hello sample application is exposed toohello internet with a public IP address, this address is associated with hello load balancer.</span></span> 

<span data-ttu-id="8f090-132">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [genel IP adresi ile Ağ Yük Dengeleyici ilişkilendirmesini](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span><span class="sxs-lookup"><span data-stu-id="8f090-132">Follow this link toosee hello JSON sample within hello Resource Manager template – [Network Load Balancer association with Public IP Address](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).</span></span>

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

<span data-ttu-id="8f090-133">Azure portal Hello hello Ağ Yük Dengeleyici genel bakış hello ilişkilendirme hello genel IP adresi ile gösterir.</span><span class="sxs-lookup"><span data-stu-id="8f090-133">From hello Azure portal, hello network load balancer overview shows hello association with hello public IP address.</span></span>

![Ağ Yükü Dengeleyici](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a><span data-ttu-id="8f090-135">Yük Dengeleyici kuralı</span><span class="sxs-lookup"><span data-stu-id="8f090-135">Load Balancer Rule</span></span>
<span data-ttu-id="8f090-136">Bir yük dengeleyici kullanırken, kuralları trafiği hedeflenen hello kaynaklarını nasıl dengelenir denetleyen yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="8f090-136">When using a load balancer, rules are configured that control how traffic is balanced across hello intended resources.</span></span> <span data-ttu-id="8f090-137">Merhaba örnek müzik deposu uygulamayla trafiği hello ortak IP adresinin 80 bağlantı noktasına ulaşan ve 80 numaralı bağlantı noktasını, tüm sanal makineler arasında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="8f090-137">With hello sample Music Store application, traffic arrives on port 80 of hello public IP address and is distributed across port 80 of all virtual machines.</span></span> 

<span data-ttu-id="8f090-138">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [yük dengeleyici kuralı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="8f090-138">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Rule](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span>

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

<span data-ttu-id="8f090-139">Merhaba ağ görünümünü dengeleyici kuralı hello Portalı'ndan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8f090-139">A view of hello network load balancer rule from hello portal.</span></span>

![Ağ Yük Dengeleyici kuralı](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a><span data-ttu-id="8f090-141">Yük Dengeleyici araştırması</span><span class="sxs-lookup"><span data-stu-id="8f090-141">Load Balancer Probe</span></span>
<span data-ttu-id="8f090-142">böylece yalnızca toorunning sistemleri isteklerinin karşılanmasını hello yük dengeleyicinin toomonitor her bir sanal makine de gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f090-142">hello load balancer also needs toomonitor each virtual machine so that requests are served only toorunning systems.</span></span> <span data-ttu-id="8f090-143">Bu izleme, sabit önceden tanımlı bir bağlantı yoklama yerini alır.</span><span class="sxs-lookup"><span data-stu-id="8f090-143">This monitoring takes place by constant probing of a pre-defined port.</span></span> <span data-ttu-id="8f090-144">yapılandırılmış tooprobe dahil bağlantı noktası 80 üzerinde tüm sanal makineleri Hello müzik deposu dağıtımıdır.</span><span class="sxs-lookup"><span data-stu-id="8f090-144">hello Music Store deployment is configured tooprobe port 80 on all included virtual machines.</span></span> 

<span data-ttu-id="8f090-145">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [yük dengeleyici araştırması](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span><span class="sxs-lookup"><span data-stu-id="8f090-145">Follow this link toosee hello JSON sample within hello Resource Manager template – [Load Balancer Probe](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).</span></span>

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

<span data-ttu-id="8f090-146">Merhaba yük dengeleyici araştırmasını Hello Azure portal ' görülür.</span><span class="sxs-lookup"><span data-stu-id="8f090-146">hello load balancer probe seen from hello Azure portal.</span></span>

![Ağ Yük Dengeleyici araştırması](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a><span data-ttu-id="8f090-148">Gelen NAT Kuralları</span><span class="sxs-lookup"><span data-stu-id="8f090-148">Inbound NAT Rules</span></span>
<span data-ttu-id="8f090-149">Bir yük dengeleyici kullanırken, kuralları toobe ihtiyacınız olmayan yük dengeli erişim tooeach sanal makine sağlayan yerine koyun.</span><span class="sxs-lookup"><span data-stu-id="8f090-149">When using a Load Balancer, rules need toobe put into place that provide non-load balanced access tooeach Virtual Machine.</span></span> <span data-ttu-id="8f090-150">Örneğin, bir SSH bağlantısı ile her bir sanal makine oluştururken, bu trafiği yükü dengelenmiş olmamalıdır, önceden belirlenen bir yol yerine yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f090-150">For instance, when creating an SSH connection with each virtual machine, this traffic should not be load balanced, rather a pre-determined path should be configured.</span></span> <span data-ttu-id="8f090-151">Önceden belirlenen yolları, bir gelen NAT kuralı kaynağı kullanılarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="8f090-151">pre-determined paths are configured using an Inbound NAT Rule resource.</span></span> <span data-ttu-id="8f090-152">Bu kaynağı kullanan, gelen iletişimi eşlenen tooindividual sanal makineler olabilir.</span><span class="sxs-lookup"><span data-stu-id="8f090-152">Using this resource, inbound communication can be mapped tooindividual Virtual Machines.</span></span> 

<span data-ttu-id="8f090-153">Merhaba müzik deposu uygulama eşlenen tooport 22 her sanal makineye SSH erişim 5000 başlayan bir bağlantı noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="8f090-153">With hello Music Store application, a port starting at 5000 is mapped tooport 22 on each Virtual Machine for SSH access.</span></span> <span data-ttu-id="8f090-154">Merhaba `copyindex()` işlevidir kullanılan tooincrement gelen bağlantı noktası Merhaba, ikinci sanal makine hello gibi bir gelen bağlantı noktası 5001 alır, üçüncü 5002 hello ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="8f090-154">hello `copyindex()` function is used tooincrement hello incoming port, such that hello second Virtual Machine receives an incoming port of 5001, hello third 5002, and so on.</span></span> 

<span data-ttu-id="8f090-155">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [gelen NAT kuralları](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span><span class="sxs-lookup"><span data-stu-id="8f090-155">Follow this link toosee hello JSON sample within hello Resource Manager template – [Inbound NAT Rules](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).</span></span> 

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

<span data-ttu-id="8f090-156">Azure portalı içinde görülen hello bir örnek gelen NAT kuralı.</span><span class="sxs-lookup"><span data-stu-id="8f090-156">One example inbound NAT rule as seen in hello Azure portal.</span></span> <span data-ttu-id="8f090-157">Merhaba dağıtımdaki her bir sanal makine için bir SSH NAT kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8f090-157">An SSH NAT rule is created for each virtual machine in hello deployment.</span></span>

![Gelen NAT kuralı](./media/dotnet-core-4-availability-scale/natrule.png)

<span data-ttu-id="8f090-159">Hello Azure Ağ Yük Dengeleyici hakkında ayrıntılı bilgi için bkz: [Yük Dengeleme için Azure altyapı hizmetleri](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f090-159">For in-depth information on hello Azure Network Load Balancer, see [Load balancing for Azure infrastructure services](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="deploy-multiple-vms"></a><span data-ttu-id="8f090-160">Birden çok VM dağıtma</span><span class="sxs-lookup"><span data-stu-id="8f090-160">Deploy multiple VMs</span></span>
<span data-ttu-id="8f090-161">Son olarak, birden çok sanal makine bir kullanılabilirlik kümesine ya da yük dengeleyici tooeffectively işlevi için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="8f090-161">Finally, for an Availability Set or Load Balancer tooeffectively function, multiple virtual machines are required.</span></span> <span data-ttu-id="8f090-162">Birden çok VM hello Azure Resource Manager şablonu kopyalama işlevi kullanılarak dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="8f090-162">Multiple VMs can be deployed using hello Azure Resource Manager template copy function.</span></span> <span data-ttu-id="8f090-163">Merhaba kopyalama işlevi kullanarak, gerekli toodefine sınırlı sayıda sanal makine değil, bunun yerine bu değer dinamik olarak hello dağıtım zamanında sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="8f090-163">Using hello copy function, it is not necessary toodefine a finite number of Virtual Machines, rather this value can be dynamically provided at hello time of deployment.</span></span> <span data-ttu-id="8f090-164">Merhaba kopyalama işlevi hello sayısı örnekleri toocreated ve sanal makineleri ve ilişkili kaynakları doğru sayıda hello dağıtma tanıtıcıları tüketir.</span><span class="sxs-lookup"><span data-stu-id="8f090-164">hello copy function consumes hello number of instances toocreated and handles deploying hello proper number of virtual machines and associated resources.</span></span>

<span data-ttu-id="8f090-165">Merhaba müzik deposu örnek şablonunda bir parametre alan bir örnek sayısı tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="8f090-165">In hello Music Store Sample template, a parameter is defined that takes in an instance count.</span></span> <span data-ttu-id="8f090-166">Bu sayı hello şablon sanal makineler ve ilgili kaynakları oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8f090-166">This number is used throughout hello template when creating virtual machines and related resources.</span></span>

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
}
```

<span data-ttu-id="8f090-167">Hello sanal makine kaynağı, hello kopyalama döngüsü bir ad verilir ve toocontrol hello elde edilen kopya sayısını hello örnekleri parametre sayısı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8f090-167">On hello Virtual Machine resource, hello copy loop is given a name and hello number of instances parameter used toocontrol hello number of resulting copies.</span></span>

<span data-ttu-id="8f090-168">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [sanal makine kopyalama işlevi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span><span class="sxs-lookup"><span data-stu-id="8f090-168">Follow this link toosee hello JSON sample within hello Resource Manager template – [Virtual Machine Copy Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300).</span></span> 

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

<span data-ttu-id="8f090-169">Merhaba geçerli yinelemeye hello kopyalama işlevi ile Merhaba erişilebilir `copyIndex()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="8f090-169">hello current iteration of hello copy function can be accessed with hello `copyIndex()` function.</span></span> <span data-ttu-id="8f090-170">Merhaba kopyalama dizin işlevi Hello değerini kullanılan tooname sanal makineler ve diğer kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="8f090-170">hello value of hello copy index function can be used tooname virtual machines and other resources.</span></span> <span data-ttu-id="8f090-171">Örneğin, bir sanal makinenin iki kopyası dağıtılırsa, farklı adlar gerekir.</span><span class="sxs-lookup"><span data-stu-id="8f090-171">For instance, if two instances of a virtual machine are deployed, they need different names.</span></span> <span data-ttu-id="8f090-172">Merhaba `copyIndex()` işlevi benzersiz bir ad toocreate hello sanal makinenin parçası adı olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8f090-172">hello `copyIndex()` function can be used as part of hello virtual machine name toocreate a unique name.</span></span> <span data-ttu-id="8f090-173">Merhaba örneği `copyindex()` amacıyla adlandırmak için kullanılan işlev hello sanal makine kaynağı görülen.</span><span class="sxs-lookup"><span data-stu-id="8f090-173">An example of hello `copyindex()` function used for naming purposes can be seen in hello Virtual Machine resource.</span></span> <span data-ttu-id="8f090-174">Burada, hello bilgisayar hello birleşimini adıdır `vmName` parametre ve hello `copyIndex()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="8f090-174">Here, hello computer name is a concatenation of hello `vmName` parameter, and hello `copyIndex()` function.</span></span> 

<span data-ttu-id="8f090-175">Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [kopyalama dizin işlevi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span><span class="sxs-lookup"><span data-stu-id="8f090-175">Follow this link toosee hello JSON sample within hello Resource Manager template – [Copy Index Function](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319).</span></span> 

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

<span data-ttu-id="8f090-176">Merhaba `copyIndex` işlevi birkaç kez hello müzik deposu örnek şablonunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8f090-176">hello `copyIndex` function is used several times in hello Music Store sample template.</span></span> <span data-ttu-id="8f090-177">Kaynakları ve işlevleri kullanılarak `copyIndex` hello sanal makinenin ağ arabirimi, yük dengeleyici kuralları gibi herhangi bir şey belirli tooa tek örnek içerir ve işlevlerini herhangi bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8f090-177">Resources and functions utilizing `copyIndex` include anything specific tooa single instance of hello virtual machine such as network interface, load balancer rules, and any depends on functions.</span></span> 

<span data-ttu-id="8f090-178">Merhaba kopyalama işlevi ile ilgili daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="8f090-178">For more information on hello copy function, see [Create multiple instances of resources in Azure Resource Manager](../../resource-group-create-multiple.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="8f090-179">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="8f090-179">Next step</span></span>
<hr>

[<span data-ttu-id="8f090-180">4. adım - Azure Resource Manager şablonları ile uygulama dağıtımı</span><span class="sxs-lookup"><span data-stu-id="8f090-180">Step 4 - Application Deployment with Azure Resource Manager Templates</span></span>](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

