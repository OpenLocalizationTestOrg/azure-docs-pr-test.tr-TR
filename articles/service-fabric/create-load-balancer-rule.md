---
title: "aaaCreate bir küme için bir Azure yük dengeleyici kuralı"
description: "Azure Service Fabric kümesi için bir Azure yük dengeleyici tooopen bağlantı noktalarını yapılandırın."
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a>Service Fabric kümesi için bağlantı noktalarını açın

Azure Service Fabric kümenizle dağıtılan hello yük dengeleyici bir düğümde çalışan trafiği tooyour uygulama yönlendirir. Uygulama toouse farklı bir bağlantı noktasını değiştirirseniz, bu bağlantı noktasını kullanıma (veya farklı bir bağlantı noktası rota gerekir) hello Azure yük dengeleyici içinde.

Service fabric kümesi tooAzure dağıtıldığında, bir yük dengeleyici sizin için otomatik olarak oluşturuldu. Bir yük dengeleyici yoksa bkz [bir Internet'e yönelik Yük Dengeleyici yapılandırma](..\load-balancer\load-balancer-get-started-internet-portal.md).

## <a name="configure-service-fabric"></a>Service fabric yapılandırın

Service Fabric uygulamanızı **ServiceManifest.xml** yapılandırma dosyasını, uygulamanızın bekliyor toouse hello uç noktaları tanımlar. Hello config dosya güncelleştirilmiş toodefine bir uç nokta oluşturulduktan sonra hello yük dengeleyici güncelleştirilmiş tooexpose o (veya farklı bir) olmalıdır bağlantı noktası. Nasıl toocreate hello hizmet yapı uç noktası ile ilgili daha fazla bilgi için bkz: [bir uç nokta Kurulum](service-fabric-service-manifest-resources.md).

## <a name="create-a-load-balancer-rule"></a>Yük Dengeleyici kuralı oluşturma

Yük Dengeleyici kuralı, bir internet'e yönelik bağlantı açar ve uygulamanız tarafından kullanılan trafiği toohello iç düğümün bağlantı iletir. Bir yük dengeleyici yoksa bkz [bir Internet'e yönelik Yük Dengeleyici yapılandırma](..\load-balancer\load-balancer-get-started-internet-portal.md).

toocreate bir yük dengeleyici kuralı için aşağıdaki bilgilerle toocollect hello gerekir:

- Yük dengeleyicisi adı.
- Kaynak grubu Merhaba, yük dengeleyici ve service fabric kümesi.
- Dış bağlantı noktası.
- İç bağlantı noktası.

## <a name="azure-cli"></a>Azure CLI
>[!NOTE]
>Merhaba yük dengeleyici toodetermine hello adı gerekiyorsa, bu komutu tooquickly get tüm yük dengeleyicileri ve ilişkili hello kaynak grupları listesini kullanın.
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

Yük Dengeleyici kuralı hello ile yalnızca tek bir komut toocreate alır **Azure CLI**. Tooknow hello yük dengeleyici ve kaynak grubu toocreate yeni bir kural hem hello adını yeterlidir.

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

Hello Azure CLI komutu aşağıdaki tablonun hello açıklanan birkaç parametreleri içerir:

| Parametre | Açıklama |
| --------- | ----------- |
| `--backend-port`  | Merhaba bağlantı noktası hello service fabric uygulaması için dinliyor. |
| `--frontend-port` | başlangıç bağlantı noktası hello yük dengeleyici çıkarır dış bağlantıları için. |
| `-lb-name` | Yük Dengeleyici toochange hello Hello adı. |
| `-g`       | Merhaba yük dengeleyici ve service fabric kümesi sahip hello kaynak grubu. |
| `-n`       | Merhaba hello kuralın adını seçildi. |


>[!NOTE]
>Bir yük dengeleyici hello Azure CLI ile nasıl toocreate bakın hakkında daha fazla bilgi için [hello Azure CLI ile bir yük dengeleyici oluşturma](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).

## <a name="powershell"></a>PowerShell

>[!NOTE]
>Merhaba yük dengeleyici toodetermine hello adı gerekiyorsa, bu komutu tooquickly get tüm yük dengeleyicileri ve ilişkili kaynak grupları listesini kullanın.
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

PowerShell Azure CLI hello biraz daha karmaşıktır. Kavramsal olarak, aşağıdaki adımları toocreate hello bir kural yapın.

1. Merhaba yük dengeleyici Azure'dan alın.
2. Bir kural oluşturun.
3. Merhaba kural toohello yük dengeleyiciye ekleyin.
4. Merhaba yük dengeleyicisi güncelleştirilemiyor.

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

Merhaba ilgili `New-AzureRmLoadBalancerRuleConfig` , hello komut `-FrontendPort` temsil hello bağlantı noktası hello yük dengeleyici gösteren dış bağlantılar ve hello `-BackendPort` temsil hello bağlantı noktası hello service fabric uygulaması dinlerken.

>[!NOTE]
>Bir yük dengeleyici PowerShell ile nasıl toocreate bakın hakkında daha fazla bilgi için [PowerShell ile bir yük dengeleyici oluşturma](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).

