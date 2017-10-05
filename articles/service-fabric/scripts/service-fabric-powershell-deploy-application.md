---
title: "Azure PowerShell Betiği örnek - uygulama bir kümeye dağıtma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - Service Fabric kümesi için bir uygulamayı dağıtın."
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
ms.openlocfilehash: 2863823205dbd70f63948ecd4af8898220fe1ff8
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="deploy-an-application-to-a-service-fabric-cluster"></a>Service Fabric kümesi bir uygulamayı dağıtma

Bu örnek betik bir uygulama paketi bir küme görüntü deposuna kopyalar, kümede uygulama türü kaydeder ve uygulama türünden uygulama örneğini oluşturur.  Varsayılan hizmetlerin hedef uygulama türü uygulama bildiriminde tanımlanan yapıyorsanız, bu hizmetleri şu anda oluşturulur. Parametreleri gerektiği gibi özelleştirin. 

Gerekirse, ile Service Fabric PowerShell modülünü yüklemek [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[Ana](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "bir küme bir uygulamayı dağıtma")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Komut dosyası örneği gerçekleştirildikten sonra komut dosyasını [bir uygulamayı kaldırmak](service-fabric-powershell-remove-application.md) uygulama örneğini kaldırma, uygulama türü kaydını kaldırma ve uygulama paketi görüntü deposundan silmek için kullanılabilir.

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını aşağıdaki komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [Kopyalama ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Bir uygulama paketi küme görüntü deposuna kopyalama.  |
|[Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| Bir uygulama türü ve sürümü küme üzerinde kaydeder. |
|[ServiceFabricApplication yeni](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| Kayıtlı uygulama türünden bir uygulama oluşturur. |

## <a name="next-steps"></a>Sonraki adımlar

Service Fabric PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/service-fabric/?view=azureservicefabricps).

Azure Service Fabric ek Powershell örnekleri bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).
