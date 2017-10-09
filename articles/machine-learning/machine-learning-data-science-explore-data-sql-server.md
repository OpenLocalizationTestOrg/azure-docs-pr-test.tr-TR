---
title: "aaaExplore verileri içindeki SQL Server sanal makinede Azure | Microsoft Docs"
description: "Nasıl bir SQL Server VM Azure üzerinde depolanan tooexplore veri."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a>Azure üzerindeki SQL Server Sanal Makinesi verilerini keşfetme
Bu belgede ele alınmaktadır nasıl Azure üzerinde bir SQL Server VM depolanan tooexplore veri. Bu SQL kullanarak veri wrangling veya Python gibi bir programlama dili kullanılarak yapılabilir.

Merhaba aşağıdaki **menü** nasıl toouse tooexplore veri çeşitli depolama ortamlarından araçları açıklamak tootopics bağlar. Bu görev hello Cortana analitik işlem (CAP) bir adımdır.

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> Merhaba örnek SQL deyimleri bu belgedeki verileri SQL Server'da olduğunu varsayın. Öyle değilse, toohello bulut veri bilimi işlem harita toolearn nasıl başvurmak toomove, veri tooSQL sunucu.
> 
> 

## <a name="sql-dataexploration"></a>SQL komut dosyaları ile SQL veri keşfedin
Burada, SQL Server kullanılan tooexplore veri depolarında olabilecek birkaç örnek SQL komut dosyaları bulunmaktadır.

1. Gün başına gözlemleri Hello sayısını alın
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Merhaba düzeylerini kategorik sütunda Al
   
    `select  distinct <column_name> from <databasename>`
3. İki kategorik sütun arada Hello düzey sayısını Al 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Merhaba dağıtım sayısal sütunlar için alma
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> Pratik bir örnek için hello kullanabilirsiniz [NYC ücreti dataset](http://www.andresmh.com/nyctaxitrips/) ve toohello başlıklı IPNB başvuruda [IPython not defteri ve SQL Server kullanarak NYC veri wrangling](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) bir uçtan uca gözden geçirme.
> 
> 

## <a name="python"></a>Python ile SQL veri keşfedin
Python tooexplore verileri kullanarak ve veri olan SQL Server'da hello benzer tooprocessing veri Python kullanarak Azure blob içinde açıklandığı gibi olduğunda Özellikleri Oluştur [veri bilimi ortamınızdaki işlem Azure Blob veri](machine-learning-data-science-process-data-blob.md). Merhaba veri pandas DataFrame hello veritabanından yüklenen toobe gerekir ve ardından daha fazla işlenebilir. Biz toohello veritabanına bağlanma ve bu bölümdeki DataFrame hello içine hello veri yükleme hello işleminde belge.

bağlantı dizesi biçimi aşağıdaki hello pyodbc (Değiştir servername, dbname, kullanıcı adı ve parola, belirli değerleri içeren) kullanarak Python kullanılan tooconnect tooa SQL Server veritabanından olabilir:

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Merhaba [Pandas Kitaplığı](http://pandas.pydata.org/) Python içinde Python programlama için veri işleme için zengin bir veri yapılarını ve veri çözümleme araçları sağlar. Merhaba aşağıdaki kodu hello sonuçları bir SQL Server veritabanından Pandas veri çerçeveye döndürülen okur:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Merhaba konuda anlatıldığı gibi hello Pandas DataFrame ile çalışabilirsiniz artık [veri bilimi ortamınızdaki işlem Azure Blob veri](machine-learning-data-science-process-data-blob.md).

## <a name="cortana-analytics-process-in-action-example"></a>Eylem örnekte Cortana Analytics işlemi
Merhaba Cortana Analytics ortak bir veri kümesini kullanarak işlem uçtan uca kılavuz örneği için bkz: [takım veri bilimi işlemi eylemde hello: SQL Server'ı kullanarak](machine-learning-data-science-process-sql-walkthrough.md).

