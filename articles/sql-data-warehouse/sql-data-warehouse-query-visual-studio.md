---
title: aaaConnect tooAzure SQL Data Warehouse - VSTS | Microsoft Docs
description: "Visual Studio ile SQL Data Warehouse'u sorgulayın."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a>Visual Studio ve SSDT ile tooSQL veri ambarına bağlanma
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Visual Studio tooquery Azure SQL Data Warehouse yalnızca birkaç dakika içinde kullanın. Bu yöntem, Visual Studio'da hello SQL Server veri Araçları (SSDT) uzantısını kullanır. 

## <a name="prerequisites"></a>Ön koşullar
toouse Bu öğretici, gerekir:

* Var olan bir SQL veri ambarı. toocreate biri bkz [SQL Data Warehouse oluşturma][Create a SQL Data Warehouse].
* Visual Studio için SSDT. Visual Studio varsa büyük olasılıkla buna da sahip olursunuz. Yükleme yönergeleri ve seçenekleri için bkz. [Visual Studio’yu ve SSDT’yi yükleme][Installing Visual Studio and SSDT].
* Merhaba SQL server tam adı. toofind Bu, bkz: [tooSQL veri ambarına bağlanmak][Connect tooSQL Data Warehouse].

## <a name="1-connect-tooyour-sql-data-warehouse"></a>1. SQL veri ambarı tooyour Bağlan
1. Visual Studio 2013 veya Visual Studio 2015'i açın.
2. SQL Server Nesne Gezgini'ni açın. toodo Bu, select **Görünüm** > **SQL Server Nesne Gezgini**.
   
    ![SQL Server Nesne Gezgini][1]
3. Merhaba tıklatın **SQL Server Ekle** simgesi.
   
    ![SQL Server ekleme][2]
4. Merhaba Bağlan tooServer penceresinde hello alanları doldurun.
   
    ![TooServer Bağlan][3]
   
   * **Sunucu adı** Merhaba girin **sunucu adı** önceden tanımlanmış.
   * **Kimlik Doğrulaması**. **SQL Server Kimlik Doğrulaması**'nı veya **Active Directory Tümleşik Kimlik Doğrulaması**'nı seçin.
   * **Kullanıcı Adı** ve **Parola**. Yukarıda SQL Server Kimlik Doğrulaması seçiliyse kullanıcı adını ve parolayı girin.
   * **Bağlan**'a tıklayın.
5. tooexplore, Azure SQL sunucunuzu genişletin. Merhaba sunucuyla ilişkili hello veritabanlarını görüntüleyebilirsiniz. Örnek veritabanınızdaki AdventureWorksDW toosee hello tabloları genişletin.
   
    ![AdventureWorksDW'yi araştırma][4]

## <a name="2-run-a-sample-query"></a>2. Örnek sorgu çalıştırma
Bir bağlantı kurulan tooyour veritabanı kaldırıldı, bir sorgu yazalım.

1. SQL Server Nesne Gezgini'nde veritabanınıza sağ tıklayın.
2. **Yeni Sorgu**'yu seçin. Yeni bir sorgu penceresi açılır.
   
    ![Yeni sorgu][5]
3. Şu TSQL sorgusunu hello sorgu penceresine kopyalayın:
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. Merhaba sorgu çalıştırın. toodo Bu, hello yeşil ok simgesine tıklayın veya kısayol aşağıdaki hello kullanın: `CTRL` + `SHIFT` + `E`.
   
    ![Sorgu çalıştırma][6]
5. Merhaba sorgu sonuçlarına bakın. Bu örnekte, hello Factınternetsales tablosunda 60398 satır var.
   
    ![Sorgu sonuçları][7]

## <a name="next-steps"></a>Sonraki adımlar
Bağlanma ve sorgulama şimdi deneyin [hello Powerbı ile verileri görselleştirmeyi][visualizing hello data with PowerBI].

ortamınız için Azure Active Directory kimlik doğrulaması, tooconfigure bkz [tooSQL veri ambarı kimlik doğrulaması][Authenticate tooSQL Data Warehouse].

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
