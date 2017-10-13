---
title: "Azure Cloud Services için İç yük dengeleyicisi oluşturma | Microsoft Docs"
description: "Klasik dağıtım modelinde PowerShell kullanarak iç yük dengeleyici oluşturmayı öğrenin"
services: load-balancer
documentationcenter: na
author: KumudD
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6616c26ede13919b94a098dc38bdd6e2f0fc0b5b
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a>Bulut hizmetleri için iç yük dengeleyici (klasik) oluşturmaya başlama

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Bulut hizmetleri](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).  Bu makale klasik dağıtım modelini incelemektedir. Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir. [Bu adımları Resource Manager modeli kullanarak gerçekleştirmeyi](load-balancer-get-started-ilb-arm-ps.md) öğrenin.

## <a name="configure-internal-load-balancer-for-cloud-services"></a>Bulut hizmetleri için iç yük dengeleyiciyi yapılandırma

İç yük dengeleyici hem sanal makineler hem de bulut hizmetleri için desteklenmektedir. Bölgesel bir sanal ağın dışındaki bulut hizmetinde oluşturulmuş olan iç yük dengeleyici uç noktasına yalnızca bulut hizmetinden erişilebilir.

İç yük dengeleyici yapılandırmasının aşağıdaki örnekte gösterilen şekilde bulut hizmetindeki ilk dağıtımın oluşturulması sırasında yapılması gerekir.

> [!IMPORTANT]
> Aşağıdaki adımları çalıştırmanın ön koşulu, bulut dağıtımı için sanal ağ oluşturmuş olmaktır. İç Yük Dengeleme oluşturmak için sanal ağ adına ve alt ağ adına ihtiyacınız olacaktır.

### <a name="step-1"></a>1. Adım

Bulut dağıtımınıza ait hizmet yapılandırma dosyasını (.cscfg) Visual Studio’da açın ve İç Yük Dengeleme oluşturmak için ağ yapılandırmasının son "`</Role>`" öğesinin altına aşağıdaki bölümü ekleyin.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of the load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Şimdi nasıl görüneceğini görmek için ağ yapılandırma dosyasına değerleri ekleyelim. Bu örnekte test_subnet adına ve 10.0.0.0/24 alt ağına sahip, 10.0.0.4 statik IP numaralı ve "test_vnet" adlı bir VNet oluşturduğunuzu varsayın. Yük dengeleyici testLB olarak adlandırılacaktır.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Yük dengeleyici şeması hakkında daha fazla bilgi için bkz. [Yük dengeleyici ekleme](https://msdn.microsoft.com/library/azure/dn722411.aspx).

### <a name="step-2"></a>2. Adım

İç Yük Dengeleme uç noktalarını eklemek için hizmet tanımı (.csdef) dosyasını değiştirin. Rol örneği oluşturulduğunda hizmet tanım dosyası rol örneklerini İç Yük Dengeleyiciye ekleyecektir.

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

Yukarıdaki örnekteki değerleri kullanarak bu değerleri hizmet tanımı dosyasına ekleyelim.

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

Ağ trafiği gelen isteklere için 80 numaralı bağlantı noktasını kullana e çalışan rolü örneklerini de 80 numaralı bağlantı noktasına gönderen testLB adlı yük dengeleyiciyi kullanarak yük dengeleme yapılacaktır.

## <a name="next-steps"></a>Sonraki adımlar

[Kaynak IP benzeşimi kullanarak yük dengeleyici dağıtım modunu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)

