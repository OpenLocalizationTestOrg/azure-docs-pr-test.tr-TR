---
title: "aaaAzure PowerShell komut dosyası örneği - FTP kullanarak karşıya yükleme dosyaları tooa web uygulaması | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - FTP kullanarak karşıya yükleme dosyaları tooa web uygulaması"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: b7d46d6f-44fd-454c-8008-87dab6eefbc1
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 32a0a529e94c1315cc6730faf23fca2693c50ffb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-tooa-web-app-using-ftp"></a>FTP kullanarak dosyaları tooa web uygulaması karşıya yükle

Bu örnek komut dosyası ile ilgili kaynaklarını App Service'te bir web uygulaması oluşturur ve FTP kullanarak web uygulama kodunuzda dağıtır (aracılığıyla [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).

Gerekirse, Azure PowerShell hello yönerge kullanarak bulunan hello hello yükleyin [Azure PowerShell Kılavuzu](/powershell/azure/overview)ve ardından çalıştırın `Login-AzureRmAccount` toocreate Azure ile bir bağlantı.

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files tooa web app using FTP")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme 

Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, web uygulaması ve tüm ilişkili kaynakları olabilir.

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Yeni-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [AzureRmAppServicePlan yeni](/powershell/module/azurerm.websites/new-azurermappserviceplan) | App Service planı oluşturur. |
| [AzureRmWebApp yeni](/powershell/module/azurerm.websites/new-azurermwebapp) | Bir web uygulaması oluşturur. |
| [Get-AzureRmWebAppPublishingProfile](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | Web uygulamanızın yayımlama profili alın. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Azure App Service Web Apps ek Azure Powershell örnekleri hello bulunabilir [Azure PowerShell örnekleri](../app-service-powershell-samples.md).
