---
title: "Hive tabloları Hive sorguları ile aaaExplore verileri | Microsoft Docs"
description: "Hive sorgularını kullanarak Hive tablolarındaki verileri keşfedin."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0d46cea5-2b4c-4384-9bfa-fa20f6f75148
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 2ede3d41682aa08ced19284f7a83ec95e0c2a93a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-hive-tables-with-hive-queries"></a>Hive sorguları ile Hive tablosundaki verileri keşfedin
Bu belgede kullanılan tooexplore verileri bir Hdınsight Hadoop kümesindeki Hive tablolardaki örnek Hive komut dosyaları sağlar.

Merhaba aşağıdaki **menü** nasıl toouse tooexplore veri çeşitli depolama ortamlarından araçları açıklamak tootopics bağlar.

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Ön koşullar
Bu makalede, sahip olduğunuz varsayılmaktadır:

* Bir Azure depolama hesabı oluşturuldu. Yönergeler gerekiyorsa bkz [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Özelleştirilmiş bir Hadoop kümesine hello Hdınsight hizmeti ile sağlandı. Yönergeler gerekiyorsa bkz [Advanced Analytics için Azure Hdınsight Hadoop kümeleri özelleştirme](machine-learning-data-science-customize-hadoop-cluster.md).
* Merhaba veri Azure Hdınsight Hadoop kümeleri karşıya yüklenen tooHive tablolarda olmuştur. Sahip değil, hello yönergeleri izleyin. [oluşturma ve yük veri tooHive tabloları](machine-learning-data-science-move-hive-tables.md) tooupload veri tooHive tabloları ilk.
* Uzaktan erişim toohello küme etkin. Yönergeler gerekiyorsa bkz [erişim hello Hadoop kümesi, baş düğüm](machine-learning-data-science-customize-hadoop-cluster.md#headnode).
* Yönergeler gerekiyorsa bkz: toosubmit Hive sorguları [nasıl tooSubmit Hive sorguları](machine-learning-data-science-move-hive-tables.md#submit)

## <a name="example-hive-query-scripts-for-data-exploration"></a>Veri keşfi için örnek Hive sorgusu komut dosyaları
1. Bölüm başına gözlemleri Hello sayısını alın`SELECT <partitionfieldname>, count(*) from <databasename>.<tablename> group by <partitionfieldname>;`
2. Gün başına gözlemleri Hello sayısını alın`SELECT to_date(<date_columnname>), count(*) from <databasename>.<tablename> group by to_date(<date_columnname>);`
3. Merhaba düzeylerini kategorik sütunda Al  
    `SELECT  distinct <column_name> from <databasename>.<tablename>`
4. İki kategorik sütun arada Hello düzey sayısını Al`SELECT <column_a>, <column_b>, count(*) from <databasename>.<tablename> group by <column_a>, <column_b>`
5. Merhaba dağıtım sayısal sütunlar için alma  
    `SELECT <column_name>, count(*) from <databasename>.<tablename> group by <column_name>`
6. İki tablo birleştirme kayıtları Ayıkla
   
        SELECT
            a.<common_columnname1> as <new_name1>,
            a.<common_columnname2> as <new_name2>,
            a.<a_column_name1> as <new_name3>,
            a.<a_column_name2> as <new_name4>,
            b.<b_column_name1> as <new_name5>,
            b.<b_column_name2> as <new_name6>
        FROM
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <a_column_name1>,
                <a_column_name2>,
            FROM <databasename>.<tablename1>
            ) a
            join
            (
            SELECT <common_columnname1>,
                <common_columnname2>,
                <b_column_name1>,
                <b_column_name2>,
            FROM <databasename>.<tablename2>
            ) b
            ON a.<common_columnname1>=b.<common_columnname1> and a.<common_columnname2>=b.<common_columnname2>

## <a name="additional-query-scripts-for-taxi-trip-data-scenarios"></a>Ücreti seyahat veri senaryoları için ek sorgu komut dosyaları
Çok belirli sorguları örnekleri[NYC ücreti seyahat veri](http://chriswhong.com/open-data/foil_nyc_taxi/) senaryoları burada da sunulmaktadır [GitHub deposunu](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Bu sorgular zaten belirtilen veri şeması varsa ve gönderilen hazır toobe toorun.

