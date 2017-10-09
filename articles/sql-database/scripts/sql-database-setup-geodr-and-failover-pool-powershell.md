---
title: "aaaPowerShell örnek etkin coğrafi çoğaltma havuza Azure SQL veritabanı | Microsoft Docs"
description: "Azure PowerShell örnek betiği tooset havuza alınmış bir Azure SQL veritabanı için etkin coğrafi çoğaltma ayarlama"
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/25/2017
ms.author: carlrab
ms.openlocfilehash: 9d183f08dcc07ba864e42fe70a562fef8bd572f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-pooled-azure-sql-database"></a>Havuza alınmış bir Azure SQL veritabanı için PowerShell tooconfigure etkin coğrafi çoğaltma kullanın

Bu PowerShell Betiği örneği etkin coğrafi çoğaltma için bir Azure SQL veritabanını bir esnek havuz yapılandırır ve toohello hello Azure SQL veritabanı'nın ikincil çoğaltma başarısız olur.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a>Örnek komut dosyaları

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme

Merhaba komut dosyası örneği çalıştırdıktan sonra komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu ve onunla ilişkili tüm kaynakları olabilir.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [Yeni-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [AzureRmSqlServer yeni](/powershell/module/azurerm.sql/new-azurermsqlserver) | Bir veritabanı veya esnek havuzu barındıran bir mantıksal sunucu oluşturur. |
| [Yeni-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | Bir esnek havuz bir mantıksal sunucu içinde oluşturur. |
| [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) | Tek bir ya da bir havuza veritabanı olarak mantıksal sunucu bir veritabanı oluşturur. |
| [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqldatabase) | Veritabanı özellikleri güncelleştirir veya bir veritabanı içine, dışı veya esnek havuzlar arasında taşır. |
| [AzureRmSqlDatabaseSecondary yeni](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| Var olan bir veritabanı için ikincil bir veritabanı oluşturur ve veri çoğaltma başlatır. |
| [Get-AzureRmSqlDatabase](/powershell/module/azurerm.sql/get-azurermsqldatabase)| Bir veya daha fazla veritabanı alır. |
| [Set-AzureRmSqlDatabaseSecondary](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| İkincil veritabanı toobe birincil sipariş tooinitiate yük devretme kümesinde geçer.|
| [Get-AzureRmSqlDatabaseReplicationLink](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | Bir Azure SQL Database ve bir kaynak grubu veya SQL Server arasındaki Hello coğrafi Çoğaltma bağlantılarını alır. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |
|||

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure PowerShell hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).

Ek SQL veritabanı PowerShell Betiği örnekleri hello bulunabilir [Azure SQL veritabanı PowerShell komut dosyalarını](../sql-database-powershell-samples.md).
