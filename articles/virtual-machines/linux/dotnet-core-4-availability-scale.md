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
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a>Kullanılabilirlik ve ölçek Linux VM'ler için Azure Resource Manager şablonlarındaki

Kullanılabilirlik ve ölçek toouptime ve hello özelliği toomeet talep bakın. Bir uygulama hello süre % 99,9 çalışma olması gerekiyorsa toohave birden çok eşzamanlı işlem kaynaklarını izin veren bir mimari gerekir. Örneğin, tek bir Web sitesi yerine, daha yüksek düzeyde kullanılabilirlik yapılandırmasıyla aynı, bunları önünde teknolojisi Dengeleme ile site hello birden çok örneğini içerir. Kalan hello toofunction devam ederken bu yapılandırmada, hello uygulamanın bir örneği bakım için alınabilir. Ölçek hello diğer yandan tooan uygulamaları özelliği tooserve isteğe başvuruyor. Bir yük dengeli uygulama ekleme veya örnekleri hello havuzdan kaldırma bir uygulama tooscale toomeet isteğe bağlı sağlar.

Bu belge hello müzik deposu örnek dağıtım kullanılabilirliğini ve ölçeğini için nasıl yapılandırılacağı ayrıntıları verilmektedir. Tüm bağımlılıkları ve benzersiz yapılandırmaları vurgulanır. Merhaba en iyi deneyim için önceden hello çözüm tooyour Azure aboneliği ve hello Azure Resource Manager şablonu ile birlikte çalışma örneği dağıtın. Merhaba tam şablon burada – bulunabilir [Ubuntu müzik deposu dağıtımı](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="availability-set"></a>Kullanılabilirlik Kümesi
Bir kullanılabilirlik kümesi mantıksal olarak Azure sanal makineleri fiziksel ana bilgisayarlar ve güç kaynakları ve fiziksel ağ donanımı gibi diğer infrastructural bileşenleri kapsar. Kullanılabilirlik kümeleri bakım, aygıt hatası veya diğer kesinti sırasında tüm sanal makineleri etkilenir emin olun. Bir kullanılabilirlik kümesi hello Visual Studio yeni kaynak Ekle Sihirbazı kullanarak veya bir şablona geçerli JSON ekleme tooan Azure Resource Manager şablonu eklenebilir.

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [kullanılabilirlik kümesi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).

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

Bir kullanılabilirlik kümesi, bir sanal makine kaynağı özelliği olarak bildirilir. 

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [sanal makine kullanılabilirlik kümesi ilişkilendirmesini](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
Merhaba kullanılabilirlik Hello Azure portal ' görüldüğü şekilde ayarlayın. Her bir sanal makine ve hello yapılandırma ayrıntılarını burada açıklanmıştır.

![Kullanılabilirlik Kümesi](./media/dotnet-core-4-availability-scale/aset.png)

Kullanılabilirlik kümeleri hakkında ayrıntılı bilgi için bkz: [sanal makinelerin kullanılabilirliğini yönetme](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

## <a name="network-load-balancer"></a>Ağ Yükü Dengeleyici
Bir kullanılabilirlik kümesi uygulama hata toleransı sağlar ancak bir yük dengeleyici Merhaba uygulaması birçok örneklerini tek bir ağ adresi üzerinde kullanılabilmesini sağlar. Bir uygulama birden çok örneğini barındırılan birçok sanal makinelerde, her biri bağlı tooa yük dengeleyici. Merhaba uygulaması erişildiği gibi hello yük dengeleyici yollar bağlı hello üyeleri arasında gelen isteği hello. Bir yük dengeleyici hello Visual Studio yeni kaynak Ekleme Sihirbazı kullanılarak eklenebilir veya düzgün ekleyerek JSON kaynak hello Azure Resource Manager şablonuna biçimlendirilmiş.

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [Ağ Yük Dengeleyici](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).

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

Merhaba örnek uygulaması gösterilen toohello olduğundan Internet genel bir IP adresi ile bu adresi hello yük dengeleyici ile ilişkili. 

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [genel IP adresi ile Ağ Yük Dengeleyici ilişkilendirmesini](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).

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

Azure portal Hello hello Ağ Yük Dengeleyici genel bakış hello ilişkilendirme hello genel IP adresi ile gösterir.

![Ağ Yükü Dengeleyici](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a>Yük Dengeleyici kuralı
Bir yük dengeleyici kullanırken, kuralları trafiği hedeflenen hello kaynaklarını nasıl dengelenir denetleyen yapılandırılır. Merhaba örnek müzik deposu uygulamayla trafiği hello ortak IP adresinin 80 bağlantı noktasına ulaşan ve 80 numaralı bağlantı noktasını, tüm sanal makineler arasında dağıtılır. 

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [yük dengeleyici kuralı](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).

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

Merhaba ağ görünümünü dengeleyici kuralı hello Portalı'ndan yükleyin.

![Ağ Yük Dengeleyici kuralı](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a>Yük Dengeleyici araştırması
böylece yalnızca toorunning sistemleri isteklerinin karşılanmasını hello yük dengeleyicinin toomonitor her bir sanal makine de gerekir. Bu izleme, sabit önceden tanımlı bir bağlantı yoklama yerini alır. yapılandırılmış tooprobe dahil bağlantı noktası 80 üzerinde tüm sanal makineleri Hello müzik deposu dağıtımıdır. 

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [yük dengeleyici araştırması](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).

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

Merhaba yük dengeleyici araştırmasını Hello Azure portal ' görülür.

![Ağ Yük Dengeleyici araştırması](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a>Gelen NAT Kuralları
Bir yük dengeleyici kullanırken, kuralları toobe ihtiyacınız olmayan yük dengeli erişim tooeach sanal makine sağlayan yerine koyun. Örneğin, bir SSH bağlantısı ile her bir sanal makine oluştururken, bu trafiği yükü dengelenmiş olmamalıdır, önceden belirlenen bir yol yerine yapılandırılmış olması gerekir. Önceden belirlenen yolları, bir gelen NAT kuralı kaynağı kullanılarak yapılandırılır. Bu kaynağı kullanan, gelen iletişimi eşlenen tooindividual sanal makineler olabilir. 

Merhaba müzik deposu uygulama eşlenen tooport 22 her sanal makineye SSH erişim 5000 başlayan bir bağlantı noktasıdır. Merhaba `copyindex()` işlevidir kullanılan tooincrement gelen bağlantı noktası Merhaba, ikinci sanal makine hello gibi bir gelen bağlantı noktası 5001 alır, üçüncü 5002 hello ve benzeri. 

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [gelen NAT kuralları](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270). 

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

Azure portalı içinde görülen hello bir örnek gelen NAT kuralı. Merhaba dağıtımdaki her bir sanal makine için bir SSH NAT kuralı oluşturulur.

![Gelen NAT kuralı](./media/dotnet-core-4-availability-scale/natrule.png)

Hello Azure Ağ Yük Dengeleyici hakkında ayrıntılı bilgi için bkz: [Yük Dengeleme için Azure altyapı hizmetleri](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="deploy-multiple-vms"></a>Birden çok VM dağıtma
Son olarak, birden çok sanal makine bir kullanılabilirlik kümesine ya da yük dengeleyici tooeffectively işlevi için gerekli değildir. Birden çok VM hello Azure Resource Manager şablonu kopyalama işlevi kullanılarak dağıtılabilir. Merhaba kopyalama işlevi kullanarak, gerekli toodefine sınırlı sayıda sanal makine değil, bunun yerine bu değer dinamik olarak hello dağıtım zamanında sağlanabilir. Merhaba kopyalama işlevi hello sayısı örnekleri toocreated ve sanal makineleri ve ilişkili kaynakları doğru sayıda hello dağıtma tanıtıcıları tüketir.

Merhaba müzik deposu örnek şablonunda bir parametre alan bir örnek sayısı tanımlanır. Bu sayı hello şablon sanal makineler ve ilgili kaynakları oluşturulurken kullanılır.

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

Hello sanal makine kaynağı, hello kopyalama döngüsü bir ad verilir ve toocontrol hello elde edilen kopya sayısını hello örnekleri parametre sayısı kullanılır.

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [sanal makine kopyalama işlevi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300). 

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

Merhaba geçerli yinelemeye hello kopyalama işlevi ile Merhaba erişilebilir `copyIndex()` işlevi. Merhaba kopyalama dizin işlevi Hello değerini kullanılan tooname sanal makineler ve diğer kaynakları olabilir. Örneğin, bir sanal makinenin iki kopyası dağıtılırsa, farklı adlar gerekir. Merhaba `copyIndex()` işlevi benzersiz bir ad toocreate hello sanal makinenin parçası adı olarak kullanılabilir. Merhaba örneği `copyindex()` amacıyla adlandırmak için kullanılan işlev hello sanal makine kaynağı görülen. Burada, hello bilgisayar hello birleşimini adıdır `vmName` parametre ve hello `copyIndex()` işlevi. 

Bu bağlantıyı toosee hello JSON örnek hello Resource Manager şablonu içinde– izleyin [kopyalama dizin işlevi](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319). 

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

Merhaba `copyIndex` işlevi birkaç kez hello müzik deposu örnek şablonunda kullanılır. Kaynakları ve işlevleri kullanılarak `copyIndex` hello sanal makinenin ağ arabirimi, yük dengeleyici kuralları gibi herhangi bir şey belirli tooa tek örnek içerir ve işlevlerini herhangi bağlıdır. 

Merhaba kopyalama işlevi ile ilgili daha fazla bilgi için bkz: [Azure Resource Manager'da kaynakları birden çok örneğini oluşturma](../../resource-group-create-multiple.md).

## <a name="next-step"></a>Sonraki adım
<hr>

[4. adım - Azure Resource Manager şablonları ile uygulama dağıtımı](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

