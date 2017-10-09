---
title: "PowerShell komut dosyası örneği - bir kümeden kaldır uygulama aaaAzure | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - uygulama bir Service Fabric kümesinden Kaldır."
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
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Bir uygulama Service Fabric kümeden kaldırma

Bu örnek betik çalışan bir Service Fabric uygulaması örneği siler, bir uygulama türü ve sürümü hello kümeden kaydını siler ve hello küme görüntü deposundan hello uygulama paketini siler.  Silme hello uygulama örneği, bu uygulama ile ilişkili hizmet örneklerini çalıştıran tüm hello da siler. Merhaba parametrelerini gerektiği gibi özelleştirin. 

Gerekirse, hello ile Merhaba Service Fabric PowerShell modülünü yüklemek [Service Fabric SDK](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | Çalışan bir Service Fabric uygulaması örneği hello kümeden kaldırır.  |
| [Kaydı ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Bir Service Fabric uygulama türü ve sürümü hello kümeden kaydını siler. |
| [Remove-ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | Service Fabric uygulama paketi hello görüntü deposundan kaldırır.|

## <a name="next-steps"></a>Sonraki adımlar

Merhaba Service Fabric PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/service-fabric/?view=azureservicefabricps).

Azure Service Fabric ek Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).
