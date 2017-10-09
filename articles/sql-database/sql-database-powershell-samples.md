---
title: "SQL veritabanı için aaaAzure PowerShell komut dosyası örnekleri | Microsoft Docs"
description: "Oluşturma ve Azure SQL veritabanı sunucuları, esnek havuzlar, veritabanları ve güvenlik duvarları yönetme azure PowerShell komut dosyası örnekleri toohelp."
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: overview-samples
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 1130ffb0e1c2b94c676d564ad5c4eb3b86374dbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-azure-sql-database"></a>Azure SQL veritabanı için Azure PowerShell örnekleri

Merhaba aşağıdaki tabloda bağlantıları toosample Azure PowerShell komut dosyalarını Azure SQL veritabanı için içerir.

| |  |
|---|---|
|**Tek bir veritabanı ve esnek havuz oluşturma**||
| [Tek bir veritabanı oluşturun ve bir güvenlik duvarı kuralı yapılandırma](scripts/sql-database-create-and-configure-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bu PowerShell Betiği tek bir Azure SQL veritabanı oluşturur ve bir sunucu düzeyinde güvenlik duvarı kuralı yapılandırır. |
| [Esnek havuzları oluşturma ve havuza alınmış veritabanlarını taşıma](scripts/sql-database-move-database-between-pools-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bu PowerShell Betiği Azure SQL Database esnek havuzları, oluşturur ve havuza alınmış veritabanları taşır ve performans düzeyleri değiştirir.|
|**Coğrafi çoğaltma ve yük devretme yapılandırma**||
| [Yapılandırma ve yük devretme aktif coğrafi çoğaltma kullanarak tek bir veritabanı](scripts/sql-database-setup-geodr-and-failover-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Bu PowerShell komut dosyası etkin coğrafi çoğaltma tek bir Azure SQL veritabanı için yapılandırır ve toohello ikincil çoğaltma başarısız olur. |
| [Yapılandırma ve yük devretme aktif coğrafi çoğaltma kullanarak havuza alınmış bir veritabanı](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Bu PowerShell Betiği SQL esnek havuzu içinde bir Azure SQL veritabanı için etkin coğrafi çoğaltma yapılandırır ve toohello ikincil çoğaltma başarısız olur. |
| [Yapılandırma ve yük devretme yük devretme bir grup için tek bir veritabanına (Önizleme)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bir Azure SQL veritabanı sunucusu örneği için bir yük devretme grubu bu PowerShell Betiği yapılandırır, bir veritabanı toohello yük devretme grubu ekler ve toohello ikincil sunucu başarısız |
|**Tek veritabanları ve esnek havuz ölçekleme**||
| [Tek bir veritabanı ölçekleme](scripts/sql-database-monitor-and-scale-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bu PowerShell Betiği hello performans ölçümlerini bir Azure SQL veritabanı'nın izler, tooa daha yüksek performans düzeyi ölçeklendirir ve hello performans ölçümleri birinde bir uyarı kuralı oluşturur. |
| [Ölçek bir esnek havuz](scripts/sql-database-monitor-and-scale-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bu PowerShell Betiği hello performans ölçümlerini bir Azure SQL Database esnek havuzunu izler, tooa daha yüksek performans düzeyi ölçeklendirir ve hello performans ölçümleri birinde bir uyarı kuralı oluşturur.  |
| **Denetim ve tehdit algılama** |
| [Denetim ve tehdit algılama yapılandırın](scripts/sql-database-auditing-and-threat-detection-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Bu PowerShell komut dosyasını bir Azure SQL veritabanı için Denetim ve tehdit algılama ilkeleri yapılandırır. |
| **Geri yükleme, kopyalama ve veritabanı alma**||
| [Bir veritabanını geri yükle](scripts/sql-database-restore-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Bu PowerShell komut dosyasını bir Azure SQL veritabanı coğrafi olarak yedekli bir yedekten geri yükler ve Silinen Azure SQL veritabanı toohello en son yedeklemesini geri yükler. |
| [Bir veritabanı toonew sunucusuna kopyalayın](scripts/sql-database-copy-database-to-new-server-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Bu PowerShell Betiği yeni bir Azure SQL Server'da mevcut bir Azure SQL veritabanının bir kopyasını oluşturur. |
| [Bir veritabanı bir bacpac Dosyadan İçeri Aktar](scripts/sql-database-import-from-bacpac-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Bu PowerShell komut dosyasını bir bacpac dosyasından bir veritabanı tooan Azure SQL server içeri aktarır. |
| **Veritabanları arasında eşitleme verileri**||
| [SQL veritabanları arasında eşitleme verileri](scripts/sql-database-sync-data-between-sql-databases.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bu PowerShell Betiği birden fazla Azure SQL veritabanı arasında veri eşitlemeye toosync yapılandırır. |
| [Şirket içi SQL Database ve SQL Server arasında veri eşitleme](scripts/sql-database-sync-data-between-azure-onprem.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bu PowerShell komut dosyasını bir Azure SQL veritabanı ile bir SQL Server içi veritabanı arasında veri eşitlemeye toosync yapılandırır. |
|||
|||
