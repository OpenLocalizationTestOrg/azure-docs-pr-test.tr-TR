---
title: "Python içinde Azure Data Lake Analytics U-SQL komut dosyaları genişletmek | Microsoft Docs"
description: "U-SQL betikleri Python kodu çalıştırma öğrenin"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: a8acaa16265070308753c2a0df3a9e7b8a3a841a
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a>Öğretici: U-SQL Python ile genişletme ile çalışmaya başlama

## <a name="prerequisites"></a>Ön koşullar

Başlamadan önce Python uzantıları Azure Data Lake Analytics hesabınızı yüklü olduğundan emin olun.

* Azure portalında, Data Lake Analytics hesabı gidin
* Soldaki menüde altında **BAŞLARKEN** tıklayın **örnek komut dosyaları**
* Tıklatın **yükleme U-SQL uzantıları** sonra **Tamam**

## <a name="overview"></a>Genel Bakış 

U-SQL için Python uzantıları Python kodu yüksek düzeyde Paralel yürütme gerçekleştirmeye geliştiriciler etkinleştirin. Aşağıdaki örnekte, temel adımlar gösterilmektedir:

* Kullanım `REFERENCE ASSEMBLY` deyimi için U-SQL betiği Python uzantılarını etkinleştirme
* Kullanarak `REDUCE` bir anahtar üzerindeki giriş verisi bölümlemek için işlemi
* U-SQL için Python uzantıları yerleşik reducer içerir (`Extension.Python.Reducer`), Python kodu üzerinde çalıştığı için reducer atanan her köşe
* U-SQL betiği adlı bir işlev katıştırılmış Python kodu içerir `usqlml_main` pandas DataFrame giriş olarak kabul eder ve pandas DataFrame çıktısı olarak döndürür.

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        TO "/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a>Python U-SQL ile nasıl tümleşik çalıştığını

### <a name="datatypes"></a>Veri türleri

* U-SQL dizesi ve sayısal sütunlarından olarak dönüştürülür-Pandas ve U-SQL arasında
* U-SQL null değerlere Pandas gelen ve giden dönüştürülür `NA` değerleri

### <a name="schemas"></a>Şemalar

* Dizin vektörlerinin Pandas, U-SQL desteklenmez. Python işlevi tüm giriş verilerini çerçevelere her zaman 0 eksi 1 satır sayısı ile 64-bit sayısal dizinden sahiptir. 
* U-SQL veri kümeleri yinelenen sütun adlarına sahip olamaz
* Dize olmayan U-SQL veri kümeleri sütun adları. 

### <a name="python-versions"></a>Python sürümleri
Yalnızca Python 3.5.1 (Windows için derlenmiş) desteklenir. 

### <a name="standard-python-modules"></a>Standart Python modülleri
Tüm standart Python modülleri dahil edilir.

### <a name="additional-python-modules"></a>Ek Python modülleri
Standart Python kitaplıkları yanı sıra birçok yaygın olarak kullanılan python kitaplıkları eklenmiştir:

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a>Özel durum iletileri
Şu anda Python kodu bir özel durum Genel köşe hata olarak görüntülenir. Gelecekte, U-SQL işi hata iletileri Python özel durum iletisi görüntülenir.

### <a name="input-and-output-size-limitations"></a>Giriş ve çıkış boyutu sınırlamaları
Her köşe atanmış bellek sınırlı miktarda sahiptir. Şu anda bu sınırı bir AU için 6 GB'tır. Giriş ve çıkış DataFrames Python kodu bellekte varolması gerektiğinden, giriş ve çıkış toplam boyutunu 6 GB aşamaz.

## <a name="see-also"></a>Ayrıca bkz.
* [Microsoft Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md)
* [Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme](data-lake-analytics-data-lake-tools-get-started.md)
* [Azure Data Lake Analytics işleri için U-SQL penceresi işlevlerini kullanma](data-lake-analytics-use-window-functions.md)
* [Azure Data Lake araçları Visual Studio kodunu kullanın](data-lake-analytics-data-lake-tools-for-vscode.md)
