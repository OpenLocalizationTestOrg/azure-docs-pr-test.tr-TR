---
title: "PowerShell komut dosyası örneği - yük dengeleyici açık uygulama bağlantı noktası aaaAzure | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - açık hello Azure yük dengeleyici Service Fabric uygulaması için bir bağlantı noktası."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 6acb28942851dce63f89f7de362b7cf1dc7b1fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="open-an-application-port-in-hello-azure-load-balancer"></a>Hello Azure yük dengeleyici bir uygulama bağlantı noktasını açın

Azure'da çalışan Service Fabric uygulaması hello Azure yük dengeleyici bulunur. Bu örnek betik, bir bağlantı noktası bir Azure yük dengeleyici açar, böylece Service Fabric uygulaması dış istemcilerle iletişim kurabilir. Merhaba parametrelerini gerektiği gibi özelleştirin. 

Gerekirse, hello ile Merhaba Service Fabric PowerShell modülünü yüklemek [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in hello load balancer")]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand özgü belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Get-AzureRmResource](/powershell/module/azurerm.resources/get-azurermresource) | Bir Azure kaynağı alır.  |
| [Get-AzureRmLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer) | Hello Azure yük dengeleyici alır. |
| [Ekleme AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | Bir araştırma yapılandırma tooa yük dengeleyici ekler.|
| [Get-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | Bir yük dengeleyici için bir araştırma yapılandırmasını alır. |
| [Ekleme AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | Bir kural yapılandırma tooa yük dengeleyici ekler. |
| [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer) | Ayarlar, bir yük dengeleyici için hedef durumu hello. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Azure Service Fabric ek Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).
