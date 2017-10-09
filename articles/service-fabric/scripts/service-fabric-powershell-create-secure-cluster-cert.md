---
title: "aaaAzure PowerShell komut dosyası örneği - Service Fabric kümesi oluştur | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - Service Fabric kümesi oluşturur."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 12fdc201bd51688cb850cd456b1e00442b79c22d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster"></a>Service Fabric kümesi oluştur

Bu örnek betik, beş düğümlü bir küme bir X.509 sertifikası ile güvenli bir Service Fabric kümesi oluşturur.  Merhaba komutu otomatik olarak imzalanan bir sertifika oluşturur ve yeni anahtar kasası tooa yükler. Merhaba sertifika ayrıca kopyalanan tooa yerel dizin yok.  Set hello *-OS* parametresi toochoose hello sürümü Windows veya Linux hello küme düğümleri üzerinde çalışır.  Merhaba parametrelerini gerektiği gibi özelleştirin.

Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview) ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı. 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Create a Service Fabric cluster")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, küme ve tüm ilişkili kaynakları olabilir.

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [AzureRmServiceFabricCluster yeni](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | Yeni bir Service Fabric kümesi oluşturur. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Azure Service Fabric ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).
