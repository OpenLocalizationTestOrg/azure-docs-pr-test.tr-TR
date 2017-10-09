---
title: SQL Data Warehouse ile Azure Machine Learning aaaUse | Microsoft Docs
description: "Çözüm geliştirmek üzere Azure SQL Data Warehouse ile Azure Machine Learning kullanma öğreticisi."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: barbkess
editor: 
ms.assetid: ac6bc731-6add-47a9-b3fe-68996e656f4d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: fdfe8c936d2bb7a02163a0bbf6435e1ebd518d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-machine-learning-with-sql-data-warehouse"></a>SQL Data Warehouse ile Azure Machine Learning kullanın
Azure Machine Learning SQL Data Warehouse verilerinizi karşı toocreate Tahmine dayalı modelleri kullanın ve tüketmek hazır web Hizmetleri olarak yayımlama bir tam olarak yönetilen Tahmine dayalı analiz hizmetidir. Tahmine dayalı analiz hello temel bilgileri öğrenmek ve makine öğrenme okuyarak [giriş tooMachine Azure üzerinde öğrenme][Introduction tooMachine Learning on Azure].  Ardından nasıl toocreate, eğitme, Puanlama ve hello kullanarak bir makine öğrenimi modeline test öğrenebilirsiniz [oluşturma deneme öğretici][Create experiment tutorial].

Bu makalede, öğreneceksiniz nasıl hello kullanarak aşağıdaki toodo hello [Azure Machine Learning Studio][Azure Machine Learning Studio]:

* Veritabanı toocreate okuma verilerden eğitmek ve Tahmine dayalı bir modeli Puanlama
* Veri tooyour veritabanı yazma

## <a name="read-data-from-sql-data-warehouse"></a>SQL veri ambarından veri okuma
Merhaba AdventureWorksDW veritabanında Ürün tablosundan biz verileri okur.

### <a name="step-1"></a>1. Adım
Tıklayarak yeni bir deneme başlatın + hello Machine Learning Studio penceresinin hello altındaki Yeni DENEMEYİ seçin ve ardından boş denemeler'ı seçin. Select hello varsayılan hello tuvale hello başındaki ad denemeler ve toosomething anlamlı, örneğin, bir bisiklet fiyat tahmini yeniden adlandırın.

### <a name="step-2"></a>2. Adım
Veri kümelerinin hello paletindeki hello okuyucu modülü ve hello deneme tuvalinin hello solundaki modülleri arayın. Merhaba modülü toohello deneme tuvaline sürükleyin.
![][drag_reader]

### <a name="step-3"></a>3. Adım
Merhaba okuyucu modülü seçin ve hello Özellikler bölmesinde doldurun.

1. Azure SQL veritabanı hello veri kaynağı seçin.
2. Veritabanı sunucusu adı: tür hello sunucu adı. Merhaba kullanabilirsiniz [Azure portal] [ Azure portal] toofind bu.

![][server_name]

1. Veritabanı adı: yalnızca belirtilen hello sunucu bir veritabanı türü hello adı.
2. Sunucu kullanıcı hesabı adı: hello veritabanı için erişim izinlerine sahip bir hesap türü hello kullanıcı adı.
3. Sunucu kullanıcı hesabı parolası: sağlamak hello hello parolasını belirtilen kullanıcı hesabı.
4. Herhangi bir sunucu sertifikayı kabul edin: tooskip verilerinizi okumadan önce hello site sertifikası gözden geçirmek istiyorsanız (daha az güvenli) bu seçeneği kullanın.
5. Veritabanı Sorgusu: tooread istediğiniz hello verileri tanımlayan bir SQL deyimi girin. Bu durumda, biz sorgu aşağıdaki hello kullanarak Ürün tablosundan verileri okur.

```SQL
SELECT ProductKey, EnglishProductName, StandardCost,
        ListPrice, Size, Weight, DaysToManufacture,
        Class, Style, Color
FROM dbo.DimProduct;
```

![][reader_properties]

### <a name="step-4"></a>4. Adım
1. Merhaba deneme tuvalinin altında Çalıştır tıklayarak Hello denemeyi çalıştırın.
2. Merhaba deneme bittiğinde hello okuyucu modülü başarıyla tamamlandı yeşil onay işareti tooindicate sahip olur. Ayrıca hello sağ üst köşesinde çalışma durumu tamamlandı hello dikkat edin.

![][run]

1. toosee alınan verileri Merhaba, hello hello alt hello otomobil veri kümesinin çıkış bağlantı noktasına tıklayın ve görsel öğe seçin.

## <a name="create-train-and-score-a-model"></a>Oluşturmak, eğitmek ve bir modeli Puanlama
Şimdi bu veri kümesi için kullanabilirsiniz:

* Bir Model oluşturmak: verileri işlemek ve özellikleri tanımlar
* Tren hello modeli: seçin ve bir öğrenme algoritmasını Uygula
* Puan ve test hello modeli: yeni bir bisiklet fiyatını tahmin etme

![][model]

toolearn nasıl toocreate, eğitme, Puanlama ve machine learning modelini kullanmak hello test hakkında daha fazla [oluşturma deneme öğretici][Create experiment tutorial].

## <a name="write-data-tooazure-sql-data-warehouse"></a>Veri tooAzure SQL veri ambarı yazma
Biz hello sonuç kümesi tooProductPriceForecast tablosundaki hello AdventureWorksDW veritabanında yazma.

### <a name="step-1"></a>1. Adım
Veri kümeleri hello paletini hello yazan modülünde ve hello deneme tuvalinin hello solundaki modülleri arayın. Merhaba modülü toohello deneme tuvaline sürükleyin.

![][drag_writer]

### <a name="step-2"></a>2. Adım
Merhaba yazıcı modülü seçin ve hello Özellikler bölmesinde doldurun.

1. Azure SQL veritabanı veri hedef hello seçin.
2. Veritabanı sunucusu adı: tür hello sunucu adı. Merhaba kullanabilirsiniz [Azure portal] [ Azure portal] toofind bu.
3. Veritabanı adı: yalnızca belirtilen hello sunucu bir veritabanı türü hello adı.
4. Sunucu kullanıcı hesabı adı: hello veritabanı için yazma izinlerine sahip bir hesap türü hello kullanıcı adı.
5. Sunucu kullanıcı hesabı parolası: sağlamak hello hello parolasını belirtilen kullanıcı hesabı.
6. Herhangi bir sunucu sertifikası (güvensiz) kabul edin: tooview hello sertifika istemiyorsanız bu seçeneği belirleyin.
7. Kaydedilen sütunları toobe virgülle ayrılmış listesi: toooutput istediğiniz hello dataset ya da sonuç sütun listesini sağlar.
8. Veri tablosu adı: hello veri tablosu hello adını belirtin.
9. Datatable sütunun virgülle ayrılmış listesini: hello yeni tabloda hello sütun adları toouse belirtin. Merhaba sütun adları hello olanları hello kaynak veri kümesinde farklı olabilir, ancak liste gerekir hello hello çıkış tablosu için tanımladığınız aynı sayıda sütun burada.
10. SQL Azure işlem yazılan satır sayısı: Merhaba tooa SQL veritabanı tek bir işlemde yazılan satır sayısını yapılandırabilirsiniz.

![][writer_properties]

### <a name="step-3"></a>3. Adım
1. Merhaba deneme tuvalinin altında Çalıştır tıklayarak Hello denemeyi çalıştırın.
2. Merhaba deneme sona erdiğinde, tüm modüllerin başarıyla tamamlandı yeşil onay işareti tooindicate sahip olur.

## <a name="next-steps"></a>Sonraki adımlar
Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].

<!--Image references-->

[drag_reader]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-reader.png
[server_name]: ./media/sql-data-warehouse-integrate-azure-machine-learning/dw-server-name.png
[reader_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-reader-properties.png
[run]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-finished-running.png
[model]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-create-train-score-model.png
[drag_writer]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-drag-writer.png
[writer_properties]: ./media/sql-data-warehouse-integrate-azure-machine-learning/ml-writer-properties.png

<!--Article references-->

[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Create experiment tutorial]: https://azure.microsoft.com/documentation/articles/machine-learning-create-experiment/
[Introduction toomachine learning on Azure]: https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[Azure Machine Learning Studio]: https://studio.azureml.net/Home
[Azure portal]: https://portal.azure.com/

<!--MSDN references-->

<!--Other Web references-->

[Azure Machine Learning documentation]: http://azure.microsoft.com/documentation/services/machine-learning/
