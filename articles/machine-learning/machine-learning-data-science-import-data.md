---
title: Machine Learning Studio aaaImport verisine | Microsoft Docs
description: "Nasıl tooimport Azure Machine Learning Studio çeşitli veri kaynaklarından verilerinizi. Hangi veri türleri ve veri biçimleri desteklenir öğrenin."
keywords: "veriler, veri biçimi, veri türleri, veri kaynakları, eğitim verilerini içeri aktarma"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a>Eğitim verilerinizi çeşitli veri kaynaklarından Azure Machine Learning Studio’ya alma
toouse kendi verilerinizi Machine Learning Studio toodevelop ve tren bir Tahmine dayalı analiz çözümü şunları yapabilirsiniz: 

* Verileri yüklemek bir **yerel dosya** ilerisinde çalışma alanınızda bir veri kümesi modülü, sabit sürücü toocreate saat
* erişim verileri birinden birkaç **çevrimiçi veri kaynakları** denemenizi hello kullanarak çalışırken [veri içeri aktarma] [ import-data] Modülü 
* verileri başka bir Azure Machine learning kullanarak **denemeler** bir veri kümesi kaydedildi
* Şirket içi verileri kullanan **SQL Server veritabanı**

Bu seçeneklerin her biri hello konulardan birine hello menüsünde aşağıda açıklanmıştır. Bu konularda size nasıl toouse Machine Learning Studio'da tooimport verileri bu çeşitli veri kaynakları gösterir. 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> Eğitim verileri için kullanabileceğiniz bir Machine Learning Studio'da kullanılabilir birçok örnek veri kümesi yok. Bunlar hakkında daha fazla bilgi için bkz: [hello örnek veri kümelerini Azure Machine Learning Studio'da kullanan](machine-learning-use-sample-datasets.md)).
> 
> 

Bu giriş konu aynı zamanda tooget veri için hazır Machine Learning Studio'da kullanımını açıklar ve hangi veri biçimleri ve veri türleri desteklenir açıklar. 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a>Azure Machine Learning Studio'da kullanılmaya hazır veri al
Machine Learning Studio, ayrılmış veya bazı durumlarda dikdörtgen olmayan veri kullanılabilmesine rağmen bir veritabanındaki verileri yapılandırılmış metin verileri gibi dikdörtgen veya tablo verilerle tasarlanmış toowork ' dir.

Verilerinizi görece temiz ise en iyisidir. Diğer bir deyişle, denemenize hello verileri karşıya yüklemeden önce tootake tırnak işareti olmayan dizeler gibi sorunlar care of isteyeceksiniz.

Ancak, yok modülleri Machine Learning Studio'daki, bazı işleme denemenizi içindeki verilerin etkinleştirin. Kullanıyor hello machine learning algoritmaları bağlı olarak, toodecide nasıl gerekebilir eksik değerleri ve seyrek veri gibi veri yapısal sorunları ele alacağız ve ile yardımcı olabilecek modülleri vardır. Hello Ara **veri dönüştürme** hello modül paleti bu işlevleri gerçekleştirmek modüller bölümü.

Denemenizin herhangi bir noktada görüntüleyebilir veya hello çıkış bağlantı noktasına tıklayarak modülü tarafından üretilen hello veri indirin. Merhaba modülü bağlı olarak farklı indirme seçenekleri kullanılabilir olabilir veya Machine Learning Studio'da web tarayıcınızdan mümkün toovisualize hello veri olabilir.

## <a name="data-formats-and-data-types-supported"></a>Desteklenen veri biçimleri ve veri türleri
Veri türlerinin sayısı denemenize içeri aktarabilirsiniz, bağlı olarak hangi mekanizması tooimport veri ve burada bu geldiği kullanın:

* Düz metin (.txt)
* Virgülle ayrılmış değerler (CSV bir başlık (.csv) ile veya olmadan) (. nh.csv)
* Sekmeyle ayrılmış değerler (TSV bir başlık (.tsv) ile veya olmadan) (. nh.tsv)
* Excel dosyası
* Azure tablo
* Hive tablosu
* SQL veritabanı tablosu
* OData değerleri
* SVMLight veri (.svmlight) (Merhaba bkz [SVMLight tanımı](http://svmlight.joachims.org/) biçimi bilgileri için)
* Öznitelik ilişkisi dosya biçimi'ne (ARFF) veri (.arff) (Merhaba bkz [ARFF tanımı](http://weka.wikispaces.com/ARFF) biçimi bilgileri için)
* Zip dosyası (.zip)
* R nesne ya da çalışma dosyası (. RData)

Meta verileri içeren ARFF gibi biçiminde veri içe aktarırsanız, Machine Learning Studio bu meta verileri toodefine hello başlığı ve her sütunun veri türünü kullanır.

Bu meta verileri içermeyen TSV veya CSV biçiminde gibi verileri içe aktarırsanız, Machine Learning Studio hello veri örnekleyerek her sütun için hello veri türü oluşturur. Merhaba veri sütun başlıkları de yoksa, Machine Learning Studio varsayılan adlarını sağlar.

Açıkça belirtin veya hello kullanarak sütunlar için hello başlıkları ve veri türlerini değiştirme [Düzenle meta veri][edit-metadata].

Merhaba aşağıdaki **veri türleri** Machine Learning Studio tarafından tanınan:

* Dize
* Tamsayı
* Çift
* Boole değeri
* Tarih saat
* TimeSpan

Machine Learning Studio adlı bir iç veri türü kullanan ***veri tablosu*** modülleri arasında toopass veri. Verilerinizi açıkça hello kullanarak veri tablosu biçime dönüştürebilirsiniz [Dönüştür tooDataset] [ convert-to-dataset] modülü.

Veri tablosu dışında biçimlerini kabul eden herhangi bir modül hello veri tooData tablo toohello sonraki modüle geçirmeden önce sessiz bir şekilde dönüştürür.

Gerekirse, veri tablosu biçime geri CSV, TSV, ARFF veya diğer dönüştürme modülleri kullanarak SVMLight biçimine dönüştürebilirsiniz.
Hello Ara **veri formatı dönüştürme** hello modül paleti bu işlevleri gerçekleştirmek modüller bölümü.

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
