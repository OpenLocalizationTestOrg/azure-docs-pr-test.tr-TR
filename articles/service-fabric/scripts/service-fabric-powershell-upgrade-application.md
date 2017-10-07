---
title: "PowerShell komut dosyası örneği - aaaAzure yükseltme Service Fabric uygulaması | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - yükseltme Service Fabric uygulaması."
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
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a>Service Fabric uygulama yükseltme

Bu örnek betik çalışan Service Fabric uygulaması örneği tooversion 1.3.0 yükseltir. Hello betik hello yeni uygulama paketi toohello küme görüntü deposuna kopyalar hello uygulama türü kaydeder, izlenen yükseltme başlar ve hello yükseltme tamamlanana veya geri alındığında kadar sürekli olarak hello yükseltme durumunu denetler. Merhaba parametrelerini gerektiği gibi özelleştirin. 

Gerekirse, hello ile Merhaba Service Fabric PowerShell modülünü yüklemek [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | Merhaba Service Fabric kümesi tüm hello uygulamalarında veya belirli bir uygulama alır.  |
| [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | Service Fabric uygulama yükseltme Hello durumunu alır. |
| [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | Merhaba Service Fabric kümesi üzerinde kayıtlı hello Service Fabric uygulama türlerini alır. |
| [Kaydı ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Service Fabric uygulama türü kaydını siler.  |
| [Kopyalama ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Kopya bir Service Fabric uygulama paketi toohello görüntüsünü depolayın.  |
| [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | Service Fabric uygulama türü kaydeder. |
| [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | Bir Service Fabric uygulaması toohello belirtilen uygulama türü sürümü yükseltir. |


## <a name="next-steps"></a>Sonraki adımlar

Merhaba Service Fabric PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/service-fabric/?view=azureservicefabricps).

Azure Service Fabric ek Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).
