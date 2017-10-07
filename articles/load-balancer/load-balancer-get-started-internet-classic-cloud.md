---
title: "Azure bulut Hizmetleri için aaaCreate bir Internet'e yönelik Yük Dengeleyici | Microsoft Docs"
description: "Nasıl toocreate Internet'e yönelik Yük Dengeleyici bulut Hizmetleri için Klasik dağıtım modelinde öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 0bb16f96-56a6-429f-88f5-0de2d0136756
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: d93cf76d417cbfc744cf07ba48c43a63cc14df69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-for-cloud-services"></a>Bulut hizmetleri için İnternet’e yönelik yük dengeleyici oluşturmaya başlama

> [!div class="op_single_selector"]
> * [Klasik Azure portalı](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Azure kaynaklarıyla çalışmadan önce Azure'da şu anda iki dağıtım modeli olduğunu önemli toounderstand olduğu: Azure Resource Manager ve klasik. Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarlarını](../azure-classic-rm.md) iyice anladığınızdan emin olun. Bu makalenin hello üstünde hello sekmeleri tıklayarak farklı araçlarla ilgili hello belgeleri görüntüleyebilirsiniz. Bu makalede, hello Klasik dağıtım modeli yer almaktadır. Ayrıca [nasıl toocreate Internet'e yönelik Yük Dengeleyici Azure Resource Manager kullanarak bilgi](load-balancer-get-started-internet-arm-ps.md).

Bulut Hizmetleri, bir yük dengeleyici ile otomatik olarak yapılandırılır ve hello hizmet modeli özelleştirilebilir.

## <a name="create-a-load-balancer-using-hello-service-definition-file"></a>Merhaba hizmet tanımı dosyası kullanarak bir yük dengeleyici oluşturma

.NET 2.5 tooupdate için Azure SDK'sı Merhaba, bulut hizmetinden yararlanabilirsiniz. Bulut Hizmetleri için uç nokta ayarlarını hello yapılan [hizmet tanımı](https://msdn.microsoft.com/library/azure/gg557553.aspx) .csdef dosyası.

Merhaba aşağıdaki örnek bir bulut dağıtımı için bir servicedefinition.csdef dosyası nasıl yapılandırıldığını gösterir:

Bulut dağıtım tarafından oluşturulan hello .csdef dosyası için Hello parçacığı denetimi, 10000, 10001 ve 10002 bağlantı noktası hello yapılandırılan dış uç noktası toouse bağlantı noktaları HTTP görebilirsiniz.

```xml
<ServiceDefinition name=“Tenant“>
    <WorkerRole name=“FERole” vmsize=“Small“>
<Endpoints>
    <InputEndpoint name=“FE_External_Http” protocol=“http” port=“10000“ />
    <InputEndpoint name=“FE_External_Tcp“  protocol=“tcp“  port=“10001“ />
    <InputEndpoint name=“FE_External_Udp“  protocol=“udp“  port=“10002“ />

    <InputEndpointname=“HTTP_Probe” protocol=“http” port=“80” loadBalancerProbe=“MyProbe“ />

    <InstanceInputEndpoint name=“InstanceEP” protocol=“tcp” localPort=“80“>
        <AllocatePublicPortFrom>
            <FixedPortRange min=“10110” max=“10120“  />
        </AllocatePublicPortFrom>
    </InstanceInputEndpoint>
    <InternalEndpoint name=“FE_InternalEP_Tcp” protocol=“tcp“ />
</Endpoints>
    </WorkerRole>
</ServiceDefinition>
```

## <a name="check-load-balancer-health-status-for-cloud-services"></a>Bulut hizmetleri için yük dengeleyici sistem durumunu denetleme

Merhaba, bir sistem durumu araştırması örneği aşağıdadır:

```xml
<LoadBalancerProbes>
    <LoadBalancerProbe name=“MyProbe” protocol=“http” path=“Probe.aspx” intervalInSeconds=“5” timeoutInSeconds=“100“ />
</LoadBalancerProbes>
```

Merhaba yük dengeleyici hello araştırma toocreate hello uç noktasının hello bilgileri ve hello hello biçiminde bir URL birleştirir `http://{DIP of VM}:80/Probe.aspx` kullanılan tooquery hello hello hizmet durumunu olabilir.

Merhaba hizmeti algılar hello gelen düzenli araştırmalar aynı IP adresi. Merhaba sanal makinenin çalıştığı hello düğümü hello ana bilgisayardan gelen hello sistem durumu araştırma isteğinin budur. Merhaba hizmeti hello hizmet sağlıklı olduğunu hello yük dengeleyici tooassume için bir HTTP 200 durum koduyla toorespond sahiptir. Sanal makineyi döndürme dışına alır hello doğrudan diğer HTTP durum kodu (örneğin 503).

Merhaba araştırma tanımı da hello araştırma hello sıklığını denetler. Örneğimizde yukarıdaki hello yük dengeleyici hello uç nokta her 5 saniye yoklama. 10 saniye (iki yoklama aralıkları) olumlu bir yanıt alınmazsa, hello araştırma aşağı kabul edilir ve hello sanal makine dışına döndürme alınır. Benzer şekilde, döndürme dışında hello hizmetidir ve olumlu bir yanıt alındı, hello hizmeti geri toorotation hemen yerleştirilir. Merhaba hizmeti arasında sağlıklı ve sağlıksız dalgalı, araştırmalar sayısı için sağlıklı bırakıldı kadar hello yük dengeleyici toodelay hello yeniden giriş hello hizmeti geri toorotation karar verebilirsiniz.

Hello için Hello hizmet tanımı şemayı denetle [durumu araştırması](https://msdn.microsoft.com/library/azure/jj151530.aspx) daha fazla bilgi için.

## <a name="next-steps"></a>Sonraki adımlar

[Bir iç yük dengeleyici yapılandırmaya başlayın](load-balancer-get-started-ilb-arm-ps.md)

[Yük dengeleyici dağıtım modu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)

