---
title: "Azure PowerShell Betiği örnek - Service Fabric kümesi oluşturun. | Microsoft Docs"
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
ms.openlocfilehash: 7cbeb3da695af3815ba660f9cc2e3388abb6f87d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-service-fabric-cluster"></a>Service Fabric kümesi oluştur

Bu örnek betik, beş düğümlü bir küme bir X.509 sertifikası ile güvenli bir Service Fabric kümesi oluşturur.  Komut otomatik olarak imzalanan bir sertifika oluşturur ve yeni bir anahtar Kasası'na yükler. Sertifikanın da yerel bir dizine kopyalanır.  Ayarlama *-OS* parametresini kullanarak Windows veya küme düğümleri üzerinde çalıştırılan Linux sürümünü seçin.  Parametreleri gerektiği gibi özelleştirin.

Gerekirse, bulunan yönergeleri kullanarak Azure PowerShell'i yükleme [Azure PowerShell Kılavuzu](/powershell/azure/overview) ve ardından çalıştırın `Login-AzureRmAccount` Azure ile bir bağlantı oluşturmak için. 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[Ana](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Service Fabric kümesi oluştur")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Komut dosyası örneği çalıştırdıktan sonra kaynak grubu, küme ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu kullanılabilir.

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını aşağıdaki komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [AzureRmServiceFabricCluster yeni](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | Yeni bir Service Fabric kümesi oluşturur. |

## <a name="next-steps"></a>Sonraki adımlar

Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Azure Service Fabric ek Azure Powershell örnekleri bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).
