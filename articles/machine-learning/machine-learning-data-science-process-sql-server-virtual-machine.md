---
title: Azure SQL Server sanal makineye aaaExplore verileri | Microsoft Docs
description: "Verileri araştırmak ve özellikleri Azure üzerinde bir SQL Server sanal makine oluştur"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>SQL Server sanal makinede Azure üzerinde işlem verileri
Bu belgede ele alınmaktadır nasıl tooexplore veri ve Azure üzerinde bir SQL Server VM depolanan verilerin özelliklerini oluşturur. Bu SQL kullanarak veri wrangling veya Python gibi bir programlama dili kullanılarak yapılabilir.

> [!NOTE]
> Merhaba örnek SQL deyimleri bu belgedeki verileri SQL Server'da olduğunu varsayın. Öyle değilse, toohello bulut veri bilimi işlem harita toolearn nasıl başvurmak toomove, veri tooSQL sunucu.
> 
> 

## <a name="SQL"></a>SQL kullanarak
Biz veri wrangling görevleri SQL kullanarak bu bölümdeki aşağıdaki hello açıklanmaktadır:

1. [Veri keşfi](#sql-dataexploration)
2. [Özellik oluşturma](#sql-featuregen)

### <a name="sql-dataexploration"></a>Veri keşfi
Burada, SQL Server kullanılan tooexplore veri depolarında olabilecek birkaç örnek SQL komut dosyaları bulunmaktadır.

> [!NOTE]
> Pratik bir örnek için hello kullanabilirsiniz [NYC ücreti dataset](http://www.andresmh.com/nyctaxitrips/) ve toohello başlıklı IPNB başvuruda [IPython not defteri ve SQL Server kullanarak NYC veri wrangling](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) bir uçtan uca gözden geçirme.
> 
> 

1. Gün başına gözlemleri Hello sayısını alın
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Merhaba düzeylerini kategorik sütunda Al
   
    `select  distinct <column_name> from <databasename>`
3. İki kategorik sütun arada Hello düzey sayısını Al 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Merhaba dağıtım sayısal sütunlar için alma
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <a name="sql-featuregen"></a>Özellik oluşturma
Bu bölümde, SQL kullanarak özellik oluşturmanın yolları açıklanmaktadır:  

1. [Özellik oluşturma sayısına dayalı](#sql-countfeature)
2. [Binning özelliği oluşturma](#sql-binningfeature)
3. [Tek bir sütundan Hello özellikleri alınıyor](#sql-featurerollout)

> [!NOTE]
> Ek özellikler oluşturmak sonra sütunları toohello var olan tablo olarak ekleyin veya hello ek özellikler ve hello özgün tabloyla katılabilir birincil anahtar, ile yeni bir tablo oluşturun. 
> 
> 

### <a name="sql-countfeature"></a>Özellik oluşturma sayısına dayalı
Merhaba Aşağıdaki örnekler sayısı özellikleri oluşturmanın iki yolu gösterir. 'where' yan tümcesi hello ikinci yöntemi kullanır hello ve koşullu toplam Hello ilk yöntemi kullanır. Bunlar ardından özelliklerle hello özgün (birincil anahtar sütunlarını kullanarak) tablosu toohave sayısı hello özgün verilerin yanında katılabilir.

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <a name="sql-binningfeature"></a>Binning özelliği oluşturma
Merhaba aşağıdaki örnekte nasıl toogenerate özellikleri (beş depo kullanarak) binning bir özellik olarak bunun yerine kullanılabilir sayısal bir sütun binned gösterilmektedir:

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>Tek bir sütundan Hello özellikleri alınıyor
Bu bölümde gösterilmektedir nasıl tooroll tablo toogenerate ek özellikler tek bir sütun çıkışı. Merhaba örneği toogenerate özellikleri çalıştığınız hello tabloda enlem veya boylam bir sütun olduğunu varsayar.

Enlem/boylam konumu verileri kısa öncü İşte (stackoverflow kaynak var [nasıl toomeasure hello enlem ve boylam doğruluğunu?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)). Bu yararlı toounderstand featurizing hello konum alanı önce oluşur:

* Merhaba oturum bize biz Kuzey veya Güney, Doğu veya Batı Merhaba dünya üzerindeki olup söyler.
* Sıfır olmayan bir yüzlerce basamağın yuvarlanacağını belirtir bize boylam değil enlem kullanıyorsanız!
* Merhaba onlarca basamaklı bir konum tooabout 1.000 kilometre sağlar. Bize ne kıtada veya üzerinde duyuyoruz Okyanusu hakkında yararlı bilgiler sağlar.
* Merhaba birimleri basamak (bir ondalık derece) bir konum yukarı too111 kilometre (60 Deniz mili, yaklaşık 69 mil) sağlar. Bu kabaca hangi büyük durumunun veya biz bulunan ülke bize.
* Merhaba ilk ondalık yerdir değerinde too11.1 km: komşu büyük Şehir'dan büyük bir şehir hello konumunu ayırt edebilirsiniz.
* Merhaba ikinci ondalık yerdir değerinde too1.1 km: sonraki hello bir village ayırabilirsiniz.
* Merhaba üçüncü ondalık değer too110 m: büyük agricultural alan veya Kurumsal kampüs tanımlayabilirsiniz yerdir.
* Merhaba dördüncü ondalık değer too11 m: kara paket tanımlayabilirsiniz yerdir. Bu girişim olmadığı düzeltilemeyen bir GPS birimle tipik doğruluğunu karşılaştırılabilir toohello olur.
* Merhaba beşinci ondalık değer too1.1 m: ağaçları birbirinden ayırt yerdir. Doğruluk toothis düzeyi ticari GPS birimleri ile yalnızca ile fark düzeltme elde edilebilir.
* Merhaba altıncı ondalık değer bu yapıları Windows'un, tasarlamak için ayrıntılı yerleştirmek için yollar oluşturma kullanabileceğiniz too0.11 m: yerdir. Glaciers ve rivers hareketlerini izlemek için birden çok iyi yeterli olmalıdır. Bu differentially düzeltilmiş GPS gibi GPS ile painstaking ölçüleri gerçekleştirerek elde edilebilir.

Merhaba konum bilgileri featurized bölge, konum ve Şehir bilgilerini ayırma aşağıdaki gibi olabilir. Bing Haritalar API'si adresinde gibi bir REST uç noktası da çağırabilirsiniz Not [noktası tarafından bir konum bulun](https://msdn.microsoft.com/library/ff701710.aspx) tooget hello bölge/bölge bilgileri.

    select 
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

Daha önce açıklandığı gibi bu konum temelli özellikler kullanılan toogenerate ek sayısı özellikleri daha fazla olabilir. 

> [!TIP]
> Program aracılığıyla dilinizi tercih kullanarak hello kayıtları ekleyebilirsiniz. Tooinsert hello veri öbekleri tooimprove yazma verimliliği gerekebilir (nasıl bir örnek için toodo bu pyodbc kullanarak, bkz: [A HelloWorld örnek tooaccess SQLServer python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)). Hello kullanarak hello veritabanındaki tooinsert verileri başka bir alternatiftir [BCP yardımcı programı](https://msdn.microsoft.com/library/ms162802.aspx).
> 
> 

### <a name="sql-aml"></a>Machine Learning tooAzure bağlanma
Yeni oluşturulan hello özelliği sütun tooan var olan tablo olarak eklenebilir veya yeni bir tabloda depolanır ve machine learning için hello özgün tabloyla katılmış. Özellikler oluşturulan ya da zaten oluşturduysanız, hello kullanılarak erişilir [veri içeri aktarma] [ import-data] aşağıda gösterildiği gibi Azure Machine Learning modülünde:

![azureml okuyucuları][1] 

## <a name="python"></a>Python gibi programlama dilini kullanma
Python tooexplore verileri kullanarak ve veri olan SQL Server'da hello açıklandığı gibi Python kullanarak Azure blob benzer tooprocessing veri olduğunda Özellikleri Oluştur [veri bilimi ortamınızdaki işlem Azure Blob veri](machine-learning-data-science-process-data-blob.md). Merhaba veri pandas veri çerçeveye hello veritabanından yüklenen toobe gerekir ve ardından daha fazla işlenebilir. Biz toohello veritabanına bağlanma ve bu bölümdeki hello veri çerçevesine hello verileri yüklenirken hello işleminde belge.

bağlantı dizesi biçimi aşağıdaki hello pyodbc (Değiştir servername, dbname, kullanıcı adı ve parola, belirli değerleri içeren) kullanarak Python kullanılan tooconnect tooa SQL Server veritabanından olabilir:

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Merhaba [Pandas Kitaplığı](http://pandas.pydata.org/) Python içinde Python programlama için veri işleme için zengin bir veri yapılarını ve veri çözümleme araçları sağlar. Aşağıdaki Hello kodu hello sonuçları bir SQL Server veritabanından Pandas veri çerçeveye döndürülen okur:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Merhaba makalesinde anlatıldığı gibi hello Pandas veri çerçevesi ile çalışabilirsiniz artık [veri bilimi ortamınızdaki işlem Azure Blob veri](machine-learning-data-science-process-data-blob.md).

## <a name="azure-data-science-in-action-example"></a>Azure veri bilimi eylem örnekte
Hello Azure veri bilimi ortak bir veri kümesini kullanarak işlem uçtan uca kılavuz örneği için bkz: [Azure veri bilimi eylem işleminde](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

