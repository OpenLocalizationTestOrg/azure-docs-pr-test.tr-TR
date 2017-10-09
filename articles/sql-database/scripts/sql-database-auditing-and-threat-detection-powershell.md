---
title: "aaaPowerShell örnek denetim tehdit algılama-Azure SQL veritabanı | Microsoft Docs"
description: "Azure PowerShell örnek komut dosyası tooconfigure denetim ve tehdit algılama bir Azure SQL veritabanı"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 97e057ac6efe5e730404ae796bc01e7e5c70df35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-sql-database-auditing-and-threat-detection"></a>PowerShell, tooconfigure SQL veritabanı denetim ve tehdit algılama kullanın

Bu PowerShell Betiği örneği SQL veritabanı denetim ve tehdit algılama yapılandırır. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme

Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Yeni-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [AzureRmSqlServer yeni](/powershell/module/azurerm.sql/new-azurermsqlserver) | Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur. |
| [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) | Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur. |
| [Yeni-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) | Bir depolama hesabı oluşturur. |
| [Set-AzureRmSqlDatabaseAuditingPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | Bir veritabanı için Denetim İlkesi Hello ayarlar. |
| [Set-AzureRmSqlDatabaseThreatDetectionPolicy](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | Tehdit algılama İlkesi, bir veritabanı üzerinde ayarlar. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |
|||

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Ek SQL veritabanı PowerShell Betiği örnekleri hello bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).
