---
title: "aaaExtend U-SQL komut dosyaları Azure Data Lake Analytics Python ile | Microsoft Docs"
description: "U-SQL betikleri toorun Python kodu nasıl öğrenin"
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
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a>Öğretici: U-SQL Python ile genişletme ile çalışmaya başlama

U-SQL için Python uzantıları geliştiriciler Python kodu tooperform yüksek düzeyde Paralel yürütme etkinleştirin. Aşağıdaki örnek hello hello temel adımlar gösterilmektedir:

* Kullanım hello `REFERENCE ASSEMBLY` hello U-SQL betiği için deyimi tooenable Python uzantıları
* Hello kullanarak `REDUCE` işlemi toopartition hello giriş verileri bir anahtarı
* Merhaba U-SQL için Python uzantıları dahil yerleşik reducer (`Extension.Python.Reducer`) her atanan köşe toohello reducer Python kodu çalıştırır
* Hello U-SQL betiği içerir adlı bir işlev katıştırılmış hello Python kodu `usqlml_main` pandas DataFrame giriş olarak kabul eder ve pandas DataFrame çıktısı olarak döndürür.

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
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a>Python U-SQL ile nasıl tümleşik çalıştığını

### <a name="datatypes"></a>Veri türleri

* U-SQL dizesi ve sayısal sütunlarından olarak dönüştürülür-Pandas ve U-SQL arasında
* U-SQL null değerlere olan Pandas gelen dönüştürülmüş tooand `NA` değerleri

### <a name="schemas"></a>Şemalar

* Dizin vektörlerinin Pandas, U-SQL desteklenmez. Tüm giriş verilerini çerçeveleri hello Python işlevinde her zaman 0 hello sayıda satırı eksi 1 ile 64-bit sayısal dizinden sahiptir. 
* U-SQL veri kümeleri yinelenen sütun adlarına sahip olamaz
* Dize olmayan U-SQL veri kümeleri sütun adları. 

### <a name="python-versions"></a>Python sürümleri
Yalnızca Python 3.5.1 (Windows için derlenmiş) desteklenir. 

### <a name="standard-python-modules"></a>Standart Python modülleri
Tüm hello standart Python modülleri dahil edilir.

### <a name="additional-python-modules"></a>Ek Python modülleri
Standart Python kitaplıkları hello yanında birçok yaygın olarak kullanılan python kitaplıkları eklenmiştir:

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a>Özel durum iletileri
Şu anda Python kodu bir özel durum Genel köşe hata olarak görüntülenir. Hello gelecekteki, hello U-SQL işi hata iletileri hello Python özel durum iletisi görüntülenir.

### <a name="input-and-output-size-limitations"></a>Giriş ve çıkış boyutu sınırlamaları
Her köşe sınırlı bir tooit atanan bellek miktarı var. Şu anda bu sınırı bir AU için 6 GB'tır. Merhaba giriş ve çıkış DataFrames hello Python kodu bellekte varolması gerektiğinden, hello giriş ve çıkış toplam boyutu hello 6 GB aşamaz.

## <a name="see-also"></a>Ayrıca bkz.
* [Microsoft Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md)
* [Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme](data-lake-analytics-data-lake-tools-get-started.md)
* [Azure Data Lake Analytics işleri için U-SQL penceresi işlevlerini kullanma](data-lake-analytics-use-window-functions.md)

