---
title: Azure Machine Learning ile aaaAnalyze veri | Microsoft Docs
description: "Azure Machine Learning toobuild Tahmine dayalı machine learning Azure SQL veri ambarında depolanan verileri temel alan modeli kullanın."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin;barbkess
ms.openlocfilehash: 337a2cd77aaad4467683827c56e5015b262b2554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-with-azure-machine-learning"></a>Azure Machine Learning ile veri çözümleme
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Bu öğretici, Azure Machine Learning toobuild Tahmine dayalı machine learning Azure SQL veri ambarında depolanan verileri temel alan modeli kullanır. Özellikle, bu Adventure Works ' hello bisiklet satış mağazası için hedeflenen bir pazarlama kampanyası oluşturur, varsa tahmin ederek çalışmasını bir müşteri büyük olasılıkla toobuy bir bisiklet veya değil.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Ön koşullar
toostep Bu öğreticide, aşağıdakiler gerekir:

* AdventureWorksDW örnek verileri önceden yüklenmiş bir SQL Data Warehouse. tooprovision Bu, bkz: [SQL Data Warehouse oluşturma] [ Create a SQL Data Warehouse] ve tooload hello örnek verileri seçin. Bir veri ambarınız olmasına karşın örnek verileriniz yoksa [örnek verileri elle yükleyebilirsiniz][load sample data manually].

## <a name="1-get-hello-data"></a>1. Merhaba Veri Al
Merhaba hello AdventureWorksDW veritabanında hello bulunan dbo.vTargetMail görünümündeki verilerdir. tooread bu veriler:

1. [Azure Machine Learning Studio][Azure Machine Learning studio]'da oturum açıp denemelerim seçeneğine tıklayın.
2. **+NEW (+YENİ)** düğmesine tıklayıp **Blank Experiment (Boş Deneme)** öğesini seçin.
3. Denemeniz için bir ad girin: Hedeflenen Pazarlama.
4. Sürükleme hello **okuyucu** hello modülleri hello tuvale bölmesine modülünden.
5. SQL Data Warehouse veritabanınıza Hello ayrıntılarını hello Özellikler bölmesinde belirtin.
6. Merhaba veritabanını belirtin **sorgu** tooread hello verileri.

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

Tıklayarak Hello denemeyi çalıştırın **çalıştırmak** hello deneme tuvalinin altında.
![Merhaba denemeyi çalıştırın][1]

Hello denemeyi çalıştırma işlemi başarıyla sonlandıktan sonra hello okuyucu modülü hello sonundaki hello çıkış bağlantı noktasına tıklayın ve seçin **Görselleştir** toosee hello alınan veri.
![İçeri aktarılan verileri görüntüleme][3]

## <a name="2-clean-hello-data"></a>2. Temiz hello veri
tooclean hello veri hello modelle ilgili olmayan bazı sütunları bırakın. toodo bu:

1. Sürükleme hello **proje sütunları** hello tuvale modüle.
2. Tıklatın **başlatma Sütun seçiciyi** hangi sütunların toodrop istediğiniz hello Özellikler bölmesinde toospecify içinde.
   ![Proje Sütunları][4]
3. Şu iki sütunu dışlayın: CustomerAlternateKey ve GeographyKey.
   ![Gereksiz sütunları kaldırma][5]

## <a name="3-build-hello-model"></a>3. Merhaba model oluşturma
Biz hello veri 80-20 bölecek: %80 tootrain machine learning modelini ve % 20 tootest hello modeli. Yapacağız hello "İki sınıflı" algoritmalardan bu ikili sınıflandırma sorunu için kullanın.

1. Sürükleme hello **bölünmüş** hello tuvale modüle.
2. Merhaba ilk çıkış veri kümesinde hello Özellikler bölmesinde bulunan satırlar için kesir değerini 0,8 girin.
   ![Verileri eğitim ve test kümesi olarak bölme][6]
3. Sürükleme hello **iki-Class Boosted karar ağacı** hello tuvale modüle.
4. Sürükleme hello **Train Model** hello modüle tuvale ve hello girişleri belirtin. Ardından **başlatma Sütun seçiciyi** hello Özellikler bölmesinde.
   * İlk giriş: ML algoritması
   * İkinci giriş: veri tootrain hello algoritması üzerinde.
     ![Merhaba Train Model modülünü bağlama][7]
5. Select hello **BikeBuyer** sütun toopredict hello gibi sütun.
   ![Sütun toopredict seçin][8]

## <a name="4-score-hello-model"></a>4. Puan hello modeli
Şimdi, biz nasıl hello modeli test verileri üzerindeki işlevini test edeceğiz. Biz hello algoritması kendi Seçtiğimiz daha iyi gerçekleştiren farklı algoritma toosee ile karşılaştırır.

1. Sürükleme **Score Model** hello tuvale modüle.
    İlk giriş: eğitilmiş model ikinci giriş: Test verileri ![puan hello modeli][9]
2. Sürükleme hello **iki sınıflı Bayes noktası makinesi** hello deneme tuvalinin içine. Bu algoritma karşılaştırma toohello iki-Class Boosted karar ağacı nasıl gerçekleştireceğini karşılaştırın.
3. Kopyala ve Yapıştır hello modülleri Train Model ve Score Model hello tuvale.
4. Sürükleme hello **Evaluate Model** hello tuvale toocompare hello iki algoritmaları modüle.
5. **Çalıştırma** hello deneme.
   ![Merhaba denemeyi çalıştırın][10]
6. Merhaba Evaluate Model modülünün hello altındaki Hello çıkış bağlantı noktasına tıklayın ve Görselleştir'ı tıklatın.
   ![Değerlendirme sonuçlarını görselleştirme][11]

Merhaba Metrikler hello ROC eğrisi, duyarlık geri çekme diyagramı olan ve eğri kaldırın. Bu ölçümlere bakarak, ikinci bir hello daha iyi gerçekleştirilen hello birinci modelin görebiliriz. toolook ne first modeli tahmin Merhaba, hello Score Model çıkış bağlantı noktasına tıklayın ve Görselleştir tıklatın hello adresindeki.
![Puanlama sonuçlarını görselleştirme][12]

İki sütun daha tooyour test veri eklenen görürsünüz.

* Puanlanmış olasılıklar: hello bir müşterinin bir bisiklet alıcısı olma olasılığı.
* Puanlanmış etiketler: hello modeliyle – bisiklet Alıcısı (1) gerçekleştirilip hello sınıflandırması (0). Etiketleme bu olasılık eşiği too50% ayarlanır ve ayarlanabilir.

Merhaba sütununu BikeBuyer (gerçek) hello skoru etiketler (tahmin) ile karşılaştırarak, ne kadar iyi hello modeli verdiğini görebilirsiniz. Sonraki adımlarda bu modeli toomake tahminleri yeni müşteriler için kullanın ve bu modeli bir web hizmeti olarak yayımlamak veya sonuçları geri tooSQL veri ambarı yazma.

## <a name="next-steps"></a>Sonraki adımlar
Tahmine dayalı makine öğrenimi modelleri oluşturma hakkında daha fazla toolearn başvurmak çok[giriş tooMachine Azure üzerinde öğrenme][Introduction tooMachine Learning on Azure].

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction tooMachine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
