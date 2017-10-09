---
title: "Klasik Azure PowerShell aaaCreate bir Internet'e yönelik Yük Dengeleyici - | Microsoft Docs"
description: "Nasıl toocreate Internet'e yönelik Yük Dengeleyici PowerShell kullanarak Klasik modda öğrenin"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a>PowerShell’de İnternet’e yönelik yük dengeleyici (klasik) oluşturmaya başlama

> [!div class="op_single_selector"]
> * [Klasik Azure portalı](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Azure kaynaklarıyla çalışmadan önce Azure'da şu anda iki dağıtım modeli olduğunu önemli toounderstand olduğu: Azure Resource Manager ve klasik. Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarlarını](../azure-classic-rm.md) iyice anladığınızdan emin olun. Bu makalenin hello üstünde hello sekmeleri tıklayarak farklı araçlarla ilgili hello belgeleri görüntüleyebilirsiniz. Bu makalede, hello Klasik dağıtım modeli yer almaktadır. Ayrıca [nasıl toocreate Internet'e yönelik Yük Dengeleyici Azure Resource Manager kullanarak bilgi](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a>PowerShell kullanarak iç yük dengeleyici kurma

powershell kullanarak bir yük dengeleyici yukarı tooset hello adımları izleyin:

1. Azure PowerShell'i hiç kullanmadıysanız bkz [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azure/overview) ve tüm hello yolu toohello toosign Azure'da sonlandırmak ve aboneliğinizi seçin hello yönergeleri izleyin.
2. Bir sanal makine oluşturduktan sonra PowerShell cmdlet'leri tooadd bir yük dengeleyici tooa sanal makine kullanabilirsiniz hello içinde aynı bulut hizmeti.

Hello aşağıdaki örnek, bir yük dengeleyici Küme hizmeti "mytestcloud" (veya myctestcloud.cloudapp.net) hello uç noktaları hello için yük dengeleyici toovirtual ekleme makineler "webfarm" toocloud adlı ekleyeceksiniz "web1" ve "web2" adlı. Merhaba yük dengeleyici ağ trafiği 80 numaralı bağlantı noktasında alır ve yükünü dengeleyen hello yerel uç (Bu örnek bağlantı noktası 80) tarafından tanımlanan hello sanal makineler arasında TCP kullanarak.

### <a name="step-1"></a>1. Adım

Merhaba ilk VM "web1" için bir yük dengeli uç noktası oluşturma

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a>2. Adım

Merhaba ikinci hello kullanarak VM "web2" aynı dengeleyici kümesi adı yüklemek için başka bir uç noktası oluşturun.

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a>Yük dengeleyiciden sanal makineyi kaldırma

Remove-AzureEndpoint tooremove hello yük dengeleyiciden sanal makine uç noktası kullanabilirsiniz

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a>Sonraki adımlar

[İç yük dengeleyici oluşturmaya başlayabilir](load-balancer-get-started-ilb-classic-ps.md) ve belirli bir yük dengeleyici ağ trafiği davranışı için [dağıtım modu](load-balancer-distribution-mode.md) türünü yapılandırabilirsiniz.

Uygulamanızı tookeep bağlantıları canlı bir yük dengeleyicinin arkasındaki sunucular için gerekiyorsa, daha fazla hakkında anlayabileceği [boşta bir yük dengeleyici için TCP zaman aşımı ayarları](load-balancer-tcp-idle-timeout.md). Azure yük dengeleyici kullanırken toolearn boştaki bağlantı davranışı konusunda yardımcı olur.
