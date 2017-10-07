---
title: aaaConnect tooAzure SQL Data Warehouse - SSMS | Microsoft Docs
description: "SQL Server Management Studio (SSMS) tooconnect tooand sorgu Azure SQL Data Warehouse kullanın."
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS) ile tooSQL veri ambarına bağlanma
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

SQL Server Management Studio (SSMS) tooconnect tooand sorgu Azure SQL Data Warehouse kullanın. 

## <a name="prerequisites"></a>Ön koşullar
toouse Bu öğretici, gerekir:

* Var olan bir SQL veri ambarı. toocreate biri bkz [SQL Data Warehouse oluşturma][Create a SQL Data Warehouse].
* SQL Server Management Studio (yüklü SSMS). [SSMS yükleme] [ Install SSMS] ücretsiz, zaten yoksa.
* Merhaba SQL server tam adı. toofind Bu, bkz: [tooSQL veri ambarına bağlanmak][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. SQL veri ambarı tooyour Bağlan
1. SSMS açın.
2. Nesne Gezgini'ni açın. toodo Bu, select **dosya** > **bağlanmak Nesne Gezgini**.
   
    ![SQL Server Nesne Gezgini][1]
3. Merhaba Bağlan tooServer penceresinde hello alanları doldurun.
   
    ![TooServer Bağlan][2]
   
   * **Sunucu adı** Merhaba girin **sunucu adı** önceden tanımlanmış.
   * **Kimlik Doğrulaması**. **SQL Server Kimlik Doğrulaması**'nı veya **Active Directory Tümleşik Kimlik Doğrulaması**'nı seçin.
   * **Kullanıcı Adı** ve **Parola**. Yukarıda SQL Server Kimlik Doğrulaması seçiliyse kullanıcı adını ve parolayı girin.
   * **Bağlan**'a tıklayın.
4. tooexplore, Azure SQL sunucunuzu genişletin. Merhaba sunucuyla ilişkili hello veritabanlarını görüntüleyebilirsiniz. Örnek veritabanınızdaki AdventureWorksDW toosee hello tabloları genişletin.
   
    ![AdventureWorksDW'yi araştırma][3]

## <a name="2-run-a-sample-query"></a>2. Örnek sorgu çalıştırma
Bir bağlantı kurulan tooyour veritabanı kaldırıldı, bir sorgu yazalım.

1. SQL Server Nesne Gezgini'nde veritabanınıza sağ tıklayın.
2. **Yeni Sorgu**'yu seçin. Yeni bir sorgu penceresi açılır.
   
    ![Yeni sorgu][4]
3. Şu TSQL sorgusunu hello sorgu penceresine kopyalayın:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Merhaba sorgu çalıştırın. toodo bunu, `Execute` veya kullanım hello aşağıdaki kısayol: `F5`.
   
    ![Sorgu çalıştırma][5]
5. Merhaba sorgu sonuçlarına bakın. Bu örnekte, hello Factınternetsales tablosunda 60398 satır var.
   
    ![Sorgu sonuçları][6]

## <a name="next-steps"></a>Sonraki adımlar
Bağlanma ve sorgulama şimdi deneyin [hello Powerbı ile verileri görselleştirmeyi][visualizing hello data with PowerBI].

ortamınız için Azure Active Directory kimlik doğrulaması, tooconfigure bkz [tooSQL veri ambarı kimlik doğrulaması][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
