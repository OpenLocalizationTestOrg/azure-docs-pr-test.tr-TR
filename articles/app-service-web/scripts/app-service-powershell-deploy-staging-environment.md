---
title: "aaaAzure PowerShell komut dosyası örneği - bir web uygulaması oluşturma ve ortam hazırlama kodu tooa dağıtma | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - bir web uygulaması oluşturma ve ortam hazırlama kodu tooa dağıtma"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5c74b962955770637173f1fd4f49342fec54ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a>Bir web uygulaması oluşturma ve ortam hazırlama kodu tooa dağıtma

Bu örnek betik "Hazırlama" adlı bir ek dağıtım yuvası ile App Service'te bir web uygulaması oluşturur ve ardından "yuvası Hazırlama" örnek uygulama toohello dağıtır.

Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code tooa staging environment")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, web uygulaması ve tüm ilişkili kaynakları olabilir.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Yeni-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [AzureRmAppServicePlan yeni](/powershell/module/azurerm.websites/new-azurermappserviceplan) | App Service planı oluşturur. |
| [AzureRmWebApp yeni](/powershell/module/azurerm.websites/new-azurermwebapp) | Bir web uygulaması oluşturur. |
| [Set-AzureRmAppServicePlan](/powershell/module/azurerm.websites/set-azurermappserviceplan) | Bir uygulama hizmeti planı toochange fiyatlandırma katmanı değiştirir. |
| [AzureRmWebAppSlot yeni](/powershell/module/azurerm.websites/new-azurermwebappslot) | Bir web uygulaması için bir dağıtım yuvası oluşturur. |
| [Set-AzureRmResource](/powershell/module/azurerm.resources/set-azurermresource) | Bir kaynak bir kaynak grubu olarak değiştirir. |
| [Takas AzureRmWebAppSlot](/powershell/module/azurerm.websites/swap-azurermwebappslot) | Web uygulamanızın dağıtım yuvası üretime değiştirir. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Azure App Service Web Apps ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).
