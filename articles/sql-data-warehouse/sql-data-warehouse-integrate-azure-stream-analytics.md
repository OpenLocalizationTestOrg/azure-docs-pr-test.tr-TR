---
title: "aaaUse SQL Data Warehouse ile Azure akış analizi | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse ile Azure akış analizi kullanımı hakkında ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a>SQL Data Warehouse ile Azure akış analizi kullanın
Azure Stream Analytics hello bulutta veri akış üzerinden düşük gecikmeli, yüksek oranda kullanılabilir, ölçeklenebilir karmaşık olay işlemesi sağlayan tam olarak yönetilen bir hizmettir. Okuyarak hello temel kavramları öğrenebilirsiniz [giriş tooAzure Stream Analytics][Introduction tooAzure Stream Analytics]. Ardından nasıl toocreate izleyerek bir uçtan uca çözüm akış Analizi ile Merhaba öğrenebilirsiniz [Azure Stream Analytics ile çalışmaya başlamak] [ Get started using Azure Stream Analytics] Öğreticisi.

Bu makalede, Azure SQL veri ambarı nasıl toouse veritabanı akış analizi işleriniz için çıkış havuzu olarak öğreneceksiniz.

## <a name="prerequisites"></a>Ön koşullar
Öncelikle hello adımlarını izleyerek hello aracılığıyla çalıştırın [Azure Stream Analytics ile çalışmaya başlamak] [ Get started using Azure Stream Analytics] Öğreticisi.  

1. Olay hub'ı giriş oluştur
2. Yapılandırma ve olay Oluşturucu uygulamasını başlatın
3. Akış analizi işi sağlama
4. İş Girişi ve sorgu belirtin

Ardından, bir Azure SQL Data Warehouse veritabanı oluşturma

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a>İş çıktısı belirtin: Azure SQL veri ambarı veritabanı
### <a name="step-1"></a>1. Adım
Stream Analytics işinde tıklatın **çıkış** hello sayfasının ve ardından hello üstten **Çıktı Ekle**.

### <a name="step-2"></a>2. Adım
SQL veritabanı'nı seçin ve İleri'yi tıklatın.

![][add-output]

### <a name="step-3"></a>3. Adım
Merhaba sonraki sayfada değerleri aşağıdaki hello girin:

* *Diğer ad çıktı*: Bu iş çıktısı için bir kolay ad girin.
* *Abonelik*:
  * SQL Data Warehouse veritabanınıza hello ise hello Stream Analytics işi, aynı abonelik geçerli abonelikten kullanım SQL veritabanı seçin.
  * Veritabanınız farklı bir abonelikte ise, SQL veritabanını kullan başka bir abonelik seçin.
* *Veritabanı*: hello bir hedef veritabanı adını belirtin.
* *Sunucu adı*: yalnızca belirtilen hello veritabanı için hello sunucu adı belirtin. Merhaba Klasik Azure portalı toofind bunu kullanabilirsiniz.

![][server-name]

* *Kullanıcı adı*: hello hello veritabanı için yazma izinlerine sahip bir hesabın kullanıcı adını belirtin.
* *Parola*: sağlamak hello hello parolasını belirtilen kullanıcı hesabı.
* *Tablo*: hello veritabanında hello hello hedef tablo adını belirtin.

![][add-database]

### <a name="step-4"></a>4. Adım
Merhaba onay düğmesine tooadd bu iş çıktısı ve akış analizi toohello veritabanı başarıyla bağlanabildiğinizi tooverify'ı tıklatın.

![][test-connection]

Merhaba bağlantı toohello veritabanı başarılı olduğunda hello portal hello altındaki bir bildirim görürsünüz. Bağlantıyı Sına hello alt tootest hello bağlantı toohello veritabanını tıklatabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
Tümleştirme genel bakış için bkz: [SQL Data Warehouse tümleştirme genel bakış][SQL Data Warehouse integration overview].

Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
