---
title: "aaaPowerShell İzleyici ölçek tek örnek Azure SQL veritabanı | Microsoft Docs"
description: "Azure PowerShell örnek betiği toomonitor ve ölçek tek bir Azure SQL veritabanı"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: bd8f880fb47b1360ae4962d2b039faa742de258e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-single-sql-database"></a>PowerShell toomonitor kullanın ve tek bir SQL veritabanı ölçeklendirme

Bir veritabanı performans ölçümlerini izleyiciler hello bu PowerShell Betiği örneği tooa daha yüksek performans düzeyi ölçeklendirir ve bir uyarı kuralı hello performans ölçümleri birinde oluşturur. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>Örnek komut dosyası

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme

Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
 [Yeni-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [AzureRmSqlServer yeni](/powershell/module/azurerm.sql/new-azurermsqlserver) | Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur. |
| [Get-AzureRmMetric](/powershell/module/azurerm.insights/get-azurermmetric) | Merhaba veritabanı Hello boyutu kullanım bilgilerini gösterir.|
| [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase) | Veritabanı özellikleri güncelleştirir veya bir veritabanı içine, dışı veya esnek havuzlar arasında taşır. |
| [Ekleme AzureRMMetricAlertRule](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | Bir uyarı kuralı tooautomatically İzleyici Dtu'lar hello gelecekteki ayarlar. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |
|||

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Ek SQL veritabanı PowerShell Betiği örnekleri hello bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).
