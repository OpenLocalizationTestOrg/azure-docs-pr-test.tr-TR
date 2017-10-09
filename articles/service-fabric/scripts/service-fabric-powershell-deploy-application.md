---
title: "PowerShell komut dosyası örneği - aaaAzure uygulama tooa kümesini dağıtma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir uygulama tooa Service Fabric kümesi dağıtma."
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
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Bir uygulama tooa Service Fabric kümesi dağıtma

Bu örnek betik bir uygulama paketi tooa kümenin görüntü deposu kopyalar, hello kümede hello uygulama türü kaydeder ve hello uygulama türünden uygulama örneğini oluşturur.  Varsayılan hizmetlerin hello uygulama bildiriminde hello hedef uygulama türü olarak tanımlanmış olan, bu hizmetleri şu anda oluşturulur. Merhaba parametrelerini gerektiği gibi özelleştirin. 

Gerekirse, hello ile Merhaba Service Fabric PowerShell modülünü yüklemek [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Merhaba komut dosyası örneği çalıştırdıktan sonra komut dosyasında hello [bir uygulamayı kaldırmak](service-fabric-powershell-remove-application.md) kullanılan tooremove hello Uygulama örneğinin olması, hello uygulama türü kaydını kaldırma ve hello uygulama paketi hello görüntü deposundan silin.

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Kopyalama ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Bir uygulama paketi toohello kümenin görüntü deposu kopyalayın.  |
|[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| Bir uygulama türü ve sürümü hello kümede kaydeder. |
|[ServiceFabricApplication yeni](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| Kayıtlı uygulama türünden bir uygulama oluşturur. |

## <a name="next-steps"></a>Sonraki adımlar

Merhaba Service Fabric PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/service-fabric/?view=azureservicefabricps).

Azure Service Fabric ek Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).
