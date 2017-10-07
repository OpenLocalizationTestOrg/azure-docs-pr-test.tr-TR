---
title: "aaaHow toouninstall esnek veritabanı işleri aracı"
description: "Nasıl toouninstall hello esnek veritabanı işleri aracı"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a>Esnek veritabanı işleri bileşenlerini Kaldır
**Esnek veritabanı iş** bileşenleri hello Portal veya PowerShell kullanarak kaldırılması.

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a>Esnek veritabanı işleri bileşenlerini Hello Azure portal kullanarak Kaldır
1. Açık hello [Azure portal](https://portal.azure.com/).
2. İçeren toohello abonelik gidin **esnek veritabanı işleri** bileşenleri, yani hello abonelik hangi esnek veritabanı işleri bileşeni yüklenmedi.
3. Tıklatın **Gözat** tıklatıp **kaynak grupları**.
4. "__ElasticDatabaseJob" adlı select hello kaynak grubu.
5. Merhaba kaynak grubunu silin.

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a>PowerShell kullanarak esnek veritabanı işleri bileşenlerini Kaldır
1. Microsoft Azure PowerShell komut penceresini başlatın ve hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x klasörü altında toohello Araçlar alt dizinine gidin: türü **cd Araçları**.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x* > cd araçları
2. Merhaba.\UninstallElasticDatabaseJobs.ps1 PowerShell betiğini yürütün.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools > engellemesini dosya.\UninstallElasticDatabaseJobs.ps1 PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools >.\UninstallElasticDatabaseJobs.ps1

Veya yalnızca, aşağıdaki komut, varsayılanı kabul hello yürütme hello bileşenleri yüklemesinde kullanılan burada değerler:

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a>Sonraki adımlar
toore yükleme esnek veritabanı işleri görmek [hello esnek veritabanı iş hizmetini yükleme](sql-database-elastic-jobs-service-installation.md)

Esnek veritabanı işleri genel bakış için bkz: [esnek veritabanı işleri genel bakış](sql-database-elastic-jobs-overview.md).

<!--Image references-->


