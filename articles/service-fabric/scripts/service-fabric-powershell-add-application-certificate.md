---
title: "PowerShell komut dosyası örneği - aaaAzure uygulama cert tooa küme ekleme | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir uygulama sertifika tooa Service Fabric kümesi ekleyin."
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
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a>Bir uygulama sertifika tooa Service Fabric kümesi Ekle

Bu örnek betik hello belirtilen Azure anahtar kasası içinde otomatik olarak imzalanan bir sertifika oluşturur ve hello Service Fabric kümesi tooall düğümlerinin yükler. Merhaba sertifika ayrıca tooa yerel klasöre indirir. indirilen hello sertifikanın Hello adı olduğu hello hello sertifikanın hello anahtar kasasında hello adı ile aynı. Merhaba parametrelerini gerektiği gibi özelleştirin.

Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview) ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı. 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır: hello tablosundaki her komut toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Ekleme AzureRmServiceFabricApplicationCertificate](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | Merhaba küme oluşturan bir yeni uygulama sertifika toohello sanal makine ölçek kümesi ekleyin.  |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Azure Service Fabric ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../service-fabric-powershell-samples.md).
