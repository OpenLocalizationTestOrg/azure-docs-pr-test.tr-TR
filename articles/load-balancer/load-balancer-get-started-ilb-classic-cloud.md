---
title: "Azure bulut Hizmetleri için bir iç yük dengeleyici aaaCreate | Microsoft Docs"
description: "Toocreate bir iç yük dengeleyici hello Klasik dağıtım modelinde PowerShell kullanarak nasıl öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
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
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a>Bulut hizmetleri için iç yük dengeleyici (klasik) oluşturmaya başlama

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Bulut hizmetleri](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).  Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](load-balancer-get-started-ilb-arm-ps.md).

## <a name="configure-internal-load-balancer-for-cloud-services"></a>Bulut hizmetleri için iç yük dengeleyiciyi yapılandırma

İç yük dengeleyici hem sanal makineler hem de bulut hizmetleri için desteklenmektedir. Bölgesel sanal ağ dışında bir bulut hizmetinde oluşturulan bir iç yük dengeleyici uç nokta yalnızca hello bulut hizmetinde erişilebilir olacaktır.

Merhaba iç yük dengeleyici yapılandırması hello bulut hizmeti, ilk dağıtımda hello hello oluşturulması sırasında örnek hello aşağıda gösterildiği gibi ayarlamak toobe sahiptir.

> [!IMPORTANT]
> Bir önkoşul toorun hello adımları toohave zaten hello bulut dağıtımı için oluşturulan bir sanal ağ olur. Sanal ağ adı ve alt ağ adı toocreate hello iç Yük Dengeleme hello gerekir.

### <a name="step-1"></a>1. Adım

Visual Studio bulut dağıtımınız için hello hizmet yapılandırma dosyasının (.cscfg) açın ve son bölümü toocreate hello iç Yük Dengeleme hello altında aşağıdaki hello Ekle "`</Role>`" Merhaba ağ yapılandırması için öğesi.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Merhaba ağ yapılandırma dosyası tooshow nasıl görüneceğine hello değerlerini ekleyelim. Merhaba örnekte test_subnet ve statik bir IP 10.0.0.4 adlı bir 10.0.0.0/24 alt ağıyla "test_vnet" adlı bir VNet oluşturulan varsayalım. Merhaba yük dengeleyici testLB adlandırılacaktır.

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

Merhaba yük dengeleyici şeması hakkında daha fazla bilgi için bkz: [Ekle yük dengeleyici](https://msdn.microsoft.com/library/azure/dn722411.aspx).

### <a name="step-2"></a>2. Adım

Merhaba hizmet açıklaması (.csdef) dosya tooadd uç noktaları toohello iç Yük Dengeleme değiştirin. Merhaba şu anda bir rol örneği oluşturulur, hello hizmet tanımı dosyası hello rol örnekleri toohello iç Yük Dengeleme ekleyeceksiniz.

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

Örnek hello yukarıdaki değerlerini aynı hello hello değerleri toohello hizmet tanımı dosyası ekleyelim.

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

Merhaba ağ trafiğini tooworker rol örneklerine de bağlantı noktası 80 üzerinde gönderme gelen istekler için 80 numaralı bağlantı noktasını kullanarak hello testLB yük dengeleyici kullanılarak Yük Dengeleme olacaktır.

## <a name="next-steps"></a>Sonraki adımlar

[Kaynak IP benzeşimi kullanarak yük dengeleyici dağıtım modunu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)

