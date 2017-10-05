---
title: "Bir küme için bir Azure yük dengeleyici kuralı oluşturma"
description: "Azure Service Fabric kümesi için bağlantı noktalarını açmak için bir Azure yük dengeleyici yapılandırın."
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
ms.openlocfilehash: c99c4d9f343ca97fd3cd363fb54feaf5507bb77c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a>Service Fabric kümesi için bağlantı noktalarını açın

Yük Dengeleyici, Azure Service Fabric kümesi ile dağıtılmış bir düğüm üzerinde çalışan ve uygulamanızın trafiğini yönlendirir. Farklı bir bağlantı noktası kullanmak için uygulamanızı değiştirirseniz, bu bağlantı noktasını kullanıma (veya farklı bir bağlantı noktası rota gerekir), Azure yük dengeleyici.

Azure service fabric kümesi dağıtıldığında, bir yük dengeleyici sizin için otomatik olarak oluşturuldu. Bir yük dengeleyici yoksa bkz [bir Internet'e yönelik Yük Dengeleyici yapılandırma](..\load-balancer\load-balancer-get-started-internet-portal.md).

## <a name="configure-service-fabric"></a>Service fabric yapılandırın

Service Fabric uygulamanızı **ServiceManifest.xml** yapılandırma dosyasını, uygulamanızın bekliyor kullanmak için uç noktalar tanımlar. (Veya farklı bir) kullanıma sunmak için bir uç nokta tanımlamak için yapılandırma dosyası güncelleştirildikten sonra Yük Dengeleyici güncelleştirilmelidir bağlantı noktası. Hizmet yapı uç noktası oluşturma hakkında daha fazla bilgi için bkz: [bir uç nokta Kurulum](service-fabric-service-manifest-resources.md).

## <a name="create-a-load-balancer-rule"></a>Yük Dengeleyici kuralı oluşturma

Yük Dengeleyici kuralı bir internet'e yönelik bağlantı açar ve uygulamanız tarafından kullanılan iç düğümün bağlantı trafiğini iletir. Bir yük dengeleyici yoksa bkz [bir Internet'e yönelik Yük Dengeleyici yapılandırma](..\load-balancer\load-balancer-get-started-internet-portal.md).

Yük Dengeleyici kuralı oluşturmak için aşağıdaki bilgileri toplayın gerekir:

- Yük dengeleyicisi adı.
- Yük Dengeleyici ve service fabric küme kaynak grubu.
- Dış bağlantı noktası.
- İç bağlantı noktası.

## <a name="azure-cli"></a>Azure CLI
>[!NOTE]
>Yük Dengeleyici adını belirlemek gerekiyorsa, hızlı bir şekilde tüm yük dengeleyicileri ve ilişkili kaynak grupların listesini almak için bu komutu kullanın.
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

Yalnızca bir yük dengeleyici kuralı ile oluşturmak için tek bir komut alır **Azure CLI**. Her iki yeni bir kural oluşturmak için yük dengeleyici ve kaynak grubunun adını bilmeniz yeterlidir.

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

Azure CLI komutu aşağıdaki tabloda açıklanan birkaç parametreleri içerir:

| Parametre | Açıklama |
| --------- | ----------- |
| `--backend-port`  | Service fabric uygulaması bağlantı noktası için dinliyor. |
| `--frontend-port` | Bağlantı noktası yük dengeleyicinin dış bağlantılar için kullanıma sunar. |
| `-lb-name` | Değiştirmek için yük dengeleyicinin adı. |
| `-g`       | Yük Dengeleyici ve service fabric kümesi sahip kaynak grubu. |
| `-n`       | Kural seçilen adı. |


>[!NOTE]
>Azure CLI ile bir yük dengeleyici oluşturma hakkında daha fazla bilgi için bkz: [Azure CLI ile bir yük dengeleyici oluşturma](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).

## <a name="powershell"></a>PowerShell

>[!NOTE]
>Yük Dengeleyici adını belirlemek gerekiyorsa, hızlı bir şekilde tüm yük dengeleyicileri ve ilişkili kaynak grupların listesini almak için bu komutu kullanın.
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

PowerShell Azure CLI biraz daha karmaşıktır. Kavramsal olarak, bir kural oluşturmak için aşağıdaki adımları uygulayın.

1. Yük Dengeleyici Azure'dan alın.
2. Bir kural oluşturun.
3. Kuralı yük dengeleyiciye ekleyin.
4. Yük Dengeleyici güncelleştirin.

```powershell
# Get the load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create the rule based on information from the load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add the rule to the load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update the load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

İlgili `New-AzureRmLoadBalancerRuleConfig` komutu, `-FrontendPort` yük dengeleyici gösteren dış bağlantıları için bağlantı noktasını temsil eder ve `-BackendPort` service fabric uygulaması için dinlediği bağlantı noktasını temsil eder.

>[!NOTE]
>PowerShell ile bir yük dengeleyici oluşturma hakkında daha fazla bilgi için bkz: [PowerShell ile bir yük dengeleyici oluşturma](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).

