---
title: aaaVisualize SQL Data Warehouse verilerini Power BI Microsoft Azure ile
description: "Power BI ile SQL Data Warehouse verilerini görselleştirme"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a>Power BI ile verileri görselleştirme
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Bu öğretici şunların nasıl yapıldığını gösterir toouse Power BI tooconnect tooSQL veri ambarı ve birkaç temel görselleştirme oluşturmak.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a>Ön koşullar
toostep Bu öğreticide, aşağıdakiler gerekir:

* SQL Data Warehouse hello AdventureWorksDW veritabanıyla önceden yüklendi. tooprovision Bu, bkz: [SQL Data Warehouse oluşturma] [ Create a SQL Data Warehouse] ve tooload hello örnek verileri seçin. Bir veri ambarınız olmasına karşın örnek verileriniz yoksa [örnek verileri elle yükleyebilirsiniz][load sample data manually].

## <a name="1-connect-tooyour-database"></a>1. Tooyour veritabanına bağlanın
Power BI tooopen ve tooyour AdventureWorksDW veritabanına bağlanın:

1. Merhaba içine oturum [Azure portal][Azure portal].
2. **SQL veritabanları** seçeneğine tıklayın ve AdventureWorks SQL Data Warehouse veritabanınızı seçin.
   
    ![Veritabanınızı bulma][1]
3. Merhaba 'Power bı'da Aç' düğmesini tıklatın.
   
    ![Power BI düğmesi][2]
4. Ardından veritabanınızın web adresinin görüntüleme hello SQL Data Warehouse bağlantı sayfası görmelisiniz. İleri'yi tıklatın.
   
    ![Power BI bağlantısı][3]
5. Azure SQL server kullanıcı adı ve parola girin ve tam olarak bağlı tooyour SQL Data Warehouse veritabanı olacaktır.
   
    ![Power BI'da oturum açma][4]
6. Power BI'da oturum açtıktan sonra sol dikey penceresinde hello hello AdventureWorksDW veri kümesine tıklayın. Bu hello veritabanı açar.
   
    ![Power BI AdventureWorksDW'yi açma][5]

## <a name="2-create-a-report"></a>2. Bir rapor oluşturun
Artık hazır toouse Power BI tooanalyze AdventureWorksDW örnek verilerinizi şunlardır. tooperform hello analiz, AdventureWorksDW AggregateSales adlı bir görünüme sahiptir. Bu görünüm hello satış hello şirketin çözümlemek için anahtar ölçümleri hello bazılarını içerir.

1. toocreate hello taraftaki alanlar bölmesinde toopostal kod göre satış tutarlarının bir haritasını hello AggregateSales görünümüne tooexpand'ı tıklatın. Merhaba PostalCode ve SalesAmount sütunları tooselect tıklatın bunları.
   
    ![Power BI AggregateSales görünümünü seçme][6]
   
    Power BI otomatik olarak bu verilerin coğrafi veriler olduğunu tanır ve verileri sizin için bir haritaya yerleştirir.
   
    ![Power BI haritası][7]
2. Bu adımda müşteri geliri başına satış tutarını gösteren bir çubuk grafiği oluşturulur. toocreate AggregateSales görünümüne gidin bu toohello genişletilmiştir. Merhaba SalesAmount alanına tıklayın. Merhaba Müşteri geliri alanını toohello sola sürükleyip eksene bırakın.
   
    ![Power BI eksen seçme][8]
   
    Biz hello çubuk grafik hello sola taşındı.
   
    ![Power BI çubuğu][9]
3. Bu adımda, sipariş tarihi başına satış tutarını gösteren bir çizgi grafiği oluşturulur. toocreate AggregateSales görünümüne gidin bu toohello genişletilmiştir. SalesAmount ve OrderDate öğelerine tıklayın Merhaba görselleştirmeleri sütununda hello çizgi grafiği simgesine tıklayın; Bu hello ilk hello ikinci satırındaki içinde simgedir.
   
    ![Power BI çizgi grafiğini seçme][10]
   
    Artık hello verilerin üç farklı görselleştirmesini gösteren bir rapora sahipsiniz.
   
    ![Power BI çizgi grafiği][11]

**Dosya**'ya tıklayıp **Kaydet**'i seçerek ilerleme durumunuzu istediğiniz zaman kaydedebilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Biz bazı zaman toowarm hello örnek verilerle verdiniz, nasıl çok bkz[geliştirmek][develop], [yük][load], veya [ geçiş][migrate]. Veya hello bakalım [Power BI Web sitesi][Power BI website].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
