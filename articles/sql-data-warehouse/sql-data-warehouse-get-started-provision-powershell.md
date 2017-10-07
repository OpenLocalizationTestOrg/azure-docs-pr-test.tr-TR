---
title: PowerShell kullanarak SQL Data Warehouse aaaCreate | Microsoft Docs
description: "PowerShell kullanarak SQL Data Warehouse oluşturma"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a>PowerShell kullanarak SQL Data Warehouse oluşturma
> [!div class="op_single_selector"]
> * [Azure Portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Bu makalede nasıl toocreate bir SQL Data Warehouse PowerShell kullanarak gösterilmektedir.

## <a name="prerequisites"></a>Ön koşullar
başlatılan tooget, aşağıdakiler gerekir:

* **Azure hesabı**: ziyaret [Azure ücretsiz deneme sürümü] [ Azure Free Trial] veya [MSDN Azure KREDİLERİ] [ MSDN Azure Credits] toocreate bir hesap.
* **Azure SQL server**: bkz [hello Azure portalı bir Azure SQL veritabanı oluşturma] [ Create an Azure SQL database in hello Azure Portal] veya [PowerShell ile bir Azure SQL veritabanı oluşturma] [ Create an Azure SQL database with PowerShell] daha fazla ayrıntı için.
* **Kaynak grubu**: aynı kaynak grubu olarak Azure SQL sunucunuzun ya da bakın hello kullanın ya da [nasıl toocreate bir kaynak grubu](../azure-resource-manager/resource-group-portal.md).
* **PowerShell 1.0.3 sürümü veya sonraki bir sürümü**: **Get-Module -ListAvailable -Name Azure** komutunu çalıştırarak sürümünüzü kontrol edebilirsiniz.  Merhaba en son sürümünü yüklenebilir [Microsoft Web Platformu yükleyicisi][Microsoft Web Platform Installer].  Merhaba en son sürümü yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma][How tooinstall and configure Azure PowerShell].

> [!NOTE]
> Bir SQL Veri Ambarı'nın oluşturulması ek hizmet ücretlerinin alınmasına neden olabilir.  Fiyatlandırmayla ilgili ayrıntılı bilgi için bkz. [SQL Veri Ambarı fiyatlandırması][SQL Data Warehouse pricing].
>
>

## <a name="create-a-sql-data-warehouse"></a>SQL Data Warehouse oluşturma
1. Windows PowerShell'i açın.
2. Bu cmdlet toologin tooAzure Kaynak Yöneticisi'ni çalıştırın.

    ```Powershell
    Login-AzureRmAccount
    ```
3. Geçerli oturumunuz için toouse istediğiniz hello aboneliği seçin.

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. Veritabanı oluşturun. Bu örnekte "mywesteuroperesgp1" hizmet hedefi düzeyi "DW400", "mywesteuroperesgp1" adlı hello kaynak grubunda bulunan "sqldwserver1" adlı toohello sunucu adlı bir veritabanı oluşturur.

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

Gerekli Parametreler şunlardır:

* **RequestedServiceObjectiveName**: hello miktarını [DWU] [ DWU] isteğinde bulunduğunuzu.  Desteklenen değerler: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 ve DW6000.
* **DatabaseName**: hello oluşturmakta olduğunuz SQL Data Warehouse hello adı.
* **ServerName**: hello oluşturmak için kullandığınız hello sunucunun adını (V12 olmalıdır).
* **ResourceGroupName**: Kullandığınız kaynak grubu.  aboneliğinizde toofind kullanılabilir kaynak gruplarını Get-azureresource komutunu kullanın.
* **Edition**: "DataWarehouse" toocreate SQL Data Warehouse olması gerekir.

İsteğe Bağlı Parametreler şunlardır:

* **CollationName**: belirtilmezse hello varsayılan harmanlama sql_latin1_general_cp1_cı_as olduğu.  Bir veritabanı üzerinde harmanlama değiştirilemez.
* **MaxSizeBytes**: veritabanı hello varsayılan en büyük boyut olan 10 GB.

Merhaba parametre seçenekleri hakkında daha fazla bilgi için bkz: [New-AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] ve [veritabanı (Azure SQL Data Warehouse) oluşturma][Create Database (Azure SQL Data Warehouse)].

## <a name="next-steps"></a>Sonraki adımlar
SQL veri ambarı tamamlandıktan sonra sağlama tootry isteyebilirsiniz [örnek veri yükleme] [ loading sample data] veya nasıl çok denetleyin[geliştirmek] [ develop] , [yük][load], veya [geçirmek][migrate].

Nasıl daha fazla bilgi ilginizi çekiyorsa toomanage SQL Data Warehouse programlı olarak kullanıma nasıl makalesini toouse [PowerShell cmdlet'leri ve REST API'lerinin][PowerShell cmdlets and REST APIs].

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
