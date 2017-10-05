---
title: "Kullanılabilirlik ve ölçek Azure Resource Manager şablonlarındaki | Microsoft Docs"
description: "Azure sanal makinesi DotNet çekirdek Öğreticisi"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 494724b5-06af-4dea-a774-ba580cf27527
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c351950fa3fc1023e339c0dc63b034c5e0d910f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-windows-vms"></a>Kullanılabilirlik ve ölçek Windows VM'ler için Azure Resource Manager şablonlarındaki

Kullanılabilirlik ve ölçek açık kalma süresi ve isteğe bağlı Karşılama becerisini bakın. Bir uygulama süresi % 99,9 çalışma olması gerekiyorsa, birden çok eşzamanlı işlem kaynaklarını izin veren bir mimari olmalıdır. Örneği için tek bir Web sitesi yerine, daha yüksek düzeyde kullanılabilirlik yapılandırmasıyla bunları önünde teknolojisi Dengeleme ile aynı sitede birden çok örneğini içerir. Kalan devam ederken çalışabilmesi bu yapılandırmada, uygulamanın bir örneği bakım için alınabilir. Ölçek, diğer yandan isteğe hizmet verecek bir uygulama yeteneği anlamına gelir. Bir yük dengeli uygulama ekleme veya örnekleri havuzdan kaldırma talebi karşılamak üzere ölçeklendirmek bir uygulama sağlar.

Bu belge, müzik deposu örnek dağıtım kullanılabilirliğini ve ölçeğini için nasıl yapılandırılacağı ayrıntıları. Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır. En iyi deneyim için Azure aboneliği ve Azure Resource Manager şablonu ile birlikte çalışma çözümü örneği önceden dağıtın. Tam veri şablonunun burada – bulunabilir [müzik deposu dağıtım Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="availability-set"></a>Kullanılabilirlik Kümesi
Bir kullanılabilirlik kümesi mantıksal olarak Azure sanal makineleri fiziksel ana bilgisayarlar ve güç kaynakları ve fiziksel ağ donanımı gibi diğer infrastructural bileşenleri kapsar. Kullanılabilirlik kümeleri bakım, aygıt hatası veya diğer kesinti sırasında tüm sanal makineleri etkilenir emin olun. Visual Studio yeni kaynak Ekle Sihirbazı kullanarak veya bir şablona geçerli JSON ekleyerek bir Azure Resource Manager şablonu bir kullanılabilirlik kümesi eklenebilir.

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [kullanılabilirlik kümesi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L368).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "availability-set"
  },
  "properties": {
  }
}
```

Bir kullanılabilirlik kümesi, bir sanal makine kaynağı özelliği olarak bildirilir. 

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [sanal makine kullanılabilirlik kümesi ilişkilendirmesini](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L302).

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
Kullanılabilirlik Azure portalından görülen kümesi. Her bir sanal makine ve yapılandırması hakkında ayrıntılar aşağıda açıklanmıştır.

![Kullanılabilirlik Kümesi](./media/dotnet-core-4-availability-scale/ase-win.png)

Kullanılabilirlik kümeleri hakkında ayrıntılı bilgi için bkz: [sanal makinelerin kullanılabilirliğini yönetme](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

## <a name="network-load-balancer"></a>Ağ Yükü Dengeleyici
Bir kullanılabilirlik kümesi uygulama hata toleransı sağlar ancak bir yük dengeleyici uygulamasının birçok örneklerini tek bir ağ adresi üzerinde kullanılabilmesini sağlar. Bir uygulama birden çok örneğini birçok sanal makinelerde, her biri bir yük dengeleyiciye bağlı barındırılabilir. Uygulama erişilen gibi yük dengeleyici ekli üyeleri arasında gelen isteği yönlendirir. Bir yük dengeleyici Visual Studio yeni kaynak Ekleme Sihirbazı kullanılarak eklenebilir veya düzgün ekleyerek JSON kaynak Azure Resource Manager şablonuna biçimlendirilmiş.

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [Ağ Yük Dengeleyici](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L198).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer"
  },
  ........<truncated>
}
```

Örnek uygulama bir ortak IP adresi ile Internet'e açık olduğu için bu yük dengeleyici ile ilişkili bir adresidir. 

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [genel IP adresi ile Ağ Yük Dengeleyici ilişkilendirmesini](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).

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

Azure portalından, Ağ Yük Dengeleyici genel bakış genel IP adresi ile ilişkilendirme gösterir.

![Ağ Yükü Dengeleyici](./media/dotnet-core-4-availability-scale/nlb-win.png)

## <a name="load-balancer-rule"></a>Yük Dengeleyici kuralı
Bir yük dengeleyici kullanırken, kuralları trafiği arasında hedeflenen kaynakların nasıl dengelenir denetleyen yapılandırılır. Örnek Müzik deposu uygulamayla trafiği ortak IP adresinin 80 bağlantı noktasına ulaşan ve 80 numaralı bağlantı noktasını, tüm sanal makineler arasında dağıtılır. 

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [yük dengeleyici kuralı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L226).

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

Ağ Yük Dengeleyici kuralı portalından görünümü.

![Ağ Yük Dengeleyici kuralı](./media/dotnet-core-4-availability-scale/lbrule-win.png)

## <a name="load-balancer-probe"></a>Yük Dengeleyici araştırması
Yük dengeleyicinin istekleri yalnızca sistemlerini çalıştıran için sunulan böylece her bir sanal makine izlemek de gerekir. Bu izleme, sabit önceden tanımlı bir bağlantı yoklama yerini alır. Müzik deposu dağıtımı dahil tüm sanal makineler üzerinde bağlantı noktası 80 araştırma için yapılandırılır. 

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [yük dengeleyici araştırması](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L247).

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

Yük Dengeleyici araştırmasını Azure portalından görülür.

![Ağ Yük Dengeleyici araştırması](./media/dotnet-core-4-availability-scale/lbprobe-win.png)

## <a name="inbound-nat-rules"></a>Gelen NAT Kuralları
Bir yük dengeleyici kullanırken, kuralları her sanal makineye olmayan yük dengeli erişim sağlayan yere yerleştirin gerekir. Örneğin, RDP bağlantısı ile her bir sanal makine oluştururken, bu trafiği yükü dengelenmiş olmamalıdır, önceden belirlenen bir yol yerine yapılandırılmış olması gerekir. Önceden belirlenen yolları, bir gelen NAT kuralı kaynağı kullanılarak yapılandırılır. Bu kaynağı kullanan, tek tek sanal makinelere gelen iletişimi eşlenebilir. 

Müzik mağazası uygulaması ile 5000 başlayan bir bağlantı noktası RDP erişim için her bir sanal makine üzerinde 3389 numaralı bağlantı noktasına eşlenir. `copyindex()` İşlevi, ikinci bir sanal makinede 5001, üçüncü 5002 gelen bir bağlantı noktası alır, gelen bağlantı noktası artırmak üzere kullanılır.

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [gelen NAT kuralları](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L260). 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'RDP-VM', copyIndex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
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
    "backendPort": 3389,
    "enableFloatingIP": false
  }
}
```

Azure portalında göründüğü gibi bir örnek gelen NAT kuralı. Dağıtımdaki her bir sanal makine için bir RDP NAT kuralı oluşturulur.

![Gelen NAT kuralı](./media/dotnet-core-4-availability-scale/natrule-win.png)

Azure Ağ Yük Dengeleyici hakkında ayrıntılı bilgi için bkz: [Yük Dengeleme için Azure altyapı hizmetleri](load-balance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="deploy-multiple-vms"></a>Birden çok VM dağıtma
Son olarak, bir kullanılabilirlik kümesi veya yük dengeleyici için etkili bir şekilde çalışması, birden çok sanal makine gereklidir. Birden çok VM Azure Resource Manager şablonunu Kopyala işlevi kullanılarak dağıtılabilir. Kopyalama işlevi kullanarak, sınırlı sayıda sanal makine tanımlamak gerekli değildir, bunun yerine bu değer dinamik olarak dağıtım zamanında sağlanabilir. Kopyalama işlevi oluşturulacak örneklerinin sayısını ve sanal makineleri ve ilişkili kaynakları doğru sayıda dağıtma tanıtıcıları tüketir.

Müzik deposu örnek şablonunda bir parametre alan bir örnek sayısı tanımlanır. Bu sayı, sanal makineler ve ilgili kaynakları oluştururken şablonu kullanılır.

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 2,
  "metadata": {
    "description": "Number of VM instances to be created behind load balancer."
  }
},
```

Sanal makine kaynakta kopyalama döngüsü, bir ad ve sonuçta elde edilen kopya sayısını kontrol etmek için kullanılan örnekleri parametre sayısı verilir.

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [sanal makine kopyalama işlevi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L290). 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  }
```

Kopyalama işlevi geçerli yineleme ile erişilebilir `copyIndex()` işlevi. Kopyalama dizin işlevi değeri, sanal makineler ve diğer kaynakları adlandırmak için kullanılabilir. Örneğin, bir sanal makinenin iki kopyası dağıtılırsa, farklı adlar gerekir. `copyIndex()` İşlevi benzersiz bir ad oluşturmak için sanal makine adının bir parçası olarak kullanılabilir. Bir örneği `copyindex()` işlevi amacıyla adlandırmak için kullanılan sanal makine kaynak görülen. Burada, bilgisayar adının bir birleşimini olduğundan `vmName` parametresi ve `copyIndex()` işlevi. 

Resource Manager şablonu – içindeki JSON örnek görmek için bu bağlantıyı izleyin [kopyalama dizin işlevi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L309). 

```json
"osProfile": {
  "computerName": "[concat(variables('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "adminPassword": "[parameters('adminPassword')]"
}
```

`copyIndex` İşlevi birkaç kez müzik deposu örnek şablonunda kullanılır. Kaynakları ve işlevleri kullanılarak `copyIndex` bir sanal makine gibi tek örneği ve ağ arabirimi, yük dengeleyici kuralları, belirli herhangi bir şey içerir ve işlevlerini herhangi bağlıdır. 

Kopyalama işlevi ile ilgili daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](../../resource-group-create-multiple.md).

## <a name="next-step"></a>Sonraki adım
<hr>

[4. adım - Azure Resource Manager şablonları ile uygulama dağıtımı](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

