---
title: TSQL ile SQL Data Warehouse aaaCreate | Microsoft Docs
description: "Nasıl toocreate bir Azure SQL Data Warehouse TSQL ile bilgi edinin"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a>Transact-SQL (TSQL) kullanarak SQL Data Warehouse oluşturma
> [!div class="op_single_selector"]
> * [Azure Portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Bu makalede nasıl toocreate bir SQL Data Warehouse T-SQL kullanarak gösterilmektedir.

## <a name="prerequisites"></a>Ön koşullar
başlatılan tooget, aşağıdakiler gerekir:

* **Azure hesabı**: ziyaret [Azure ücretsiz deneme sürümü] [ Azure Free Trial] veya [MSDN Azure KREDİLERİ] [ MSDN Azure Credits] toocreate bir hesap.
* **Azure SQL server**: bkz. [oluşturma hello Azure Portal ile Azure SQL Database mantıksal sunucusu] [hello Azure Portal ile Azure SQL Database mantıksal sunucusu Oluştur] veya [PowerShell ile Azure SQL Database mantıksal sunucusu oluşturma] [bir Azure SQL oluştur PowerShell ile Database mantıksal sunucusu] daha fazla ayrıntı için.
* **Kaynak grubu**: aynı kaynak grubu olarak Azure SQL sunucunuzun ya da bakın hello kullanın ya da [nasıl toocreate bir kaynak grubu][how toocreate a resource group].
* **Ortam tooexecute T-SQL**: kullanabileceğiniz [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], veya [SSMS] [ SSMS] tooexecute T-SQL.

> [!NOTE]
> Bir SQL Veri Ambarı'nın oluşturulması ek hizmet ücretlerinin alınmasına neden olabilir.  Fiyatlandırmayla ilgili ayrıntılı bilgi için bkz. [SQL Veri Ambarı fiyatlandırması][SQL Data Warehouse pricing].
>
>

## <a name="create-a-database-with-visual-studio"></a>Visual Studio ile veritabanı oluşturma
Yeni tooVisual Studio varsa, hello makalesine bakın [sorgu Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].  toostart, Visual Studio ile SQL Server nesne Gezgini'ni açın ve SQL Data Warehouse veritabanınızı barındıracak toohello sunucusuna bağlanın.  Bağlandıktan sonra aşağıdaki SQL komutunu hello hello çalıştırarak SQL Data Warehouse oluşturabilirsiniz **ana** veritabanı.  Bu komut, bir hizmet hedefi DW400 olan hello veritabanı olacak oluşturur ve hello veritabanı toogrow tooa maksimum boyutu 10 TB'lık izin.

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a>sqlcmd ile veritabanı oluşturma
Alternatif olarak, aynı komutu çalıştırarak sqlcmd ile Merhaba bir komut isteminde aşağıdaki hello çalıştırabilirsiniz.

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

belirtilmemişse hello varsayılan harmanlaması HARMANLAMA sql_latin1_general_cp1_cı_as ' dir.  Merhaba `MAXSIZE` 250 GB ile 240 TB arasında olabilir.  Merhaba `SERVICE_OBJECTIVE` DW100 ve DW2000 arasında olabilir [DWU][DWU].  Geçerli tüm değerlerin listesi için hello MSDN belgelerine bakın [CREATE DATABASE][CREATE DATABASE].  Merhaba MAXSIZE ve servıce_objectıve can ile değiştirilmesi bir [ALTER DATABASE] [ ALTER DATABASE] T-SQL komutu.  Veritabanı harmanlamasının Hello oluşturulduktan sonra değiştirilemez.   Yürütülen tüm sorguları iptal yeniden başlatma hizmetlerinin DWU değiştirme olarak değişen hello servıce_objectıve neden olduğunda dikkat kullanılmalıdır.  MAXSIZE parametresinin değiştirilmesi basit bir meta veri işlemi olduğundan hizmetler yeniden başlatılmaz.

## <a name="next-steps"></a>Sonraki adımlar
SQL veri ambarı yapabilecekleriniz Sağlama tamamlandıktan sonra [örnek verileri yükleme] [ load sample data] veya nasıl çok denetleyin[geliştirmek][develop], [yük][load], veya [geçirmek][migrate].

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
