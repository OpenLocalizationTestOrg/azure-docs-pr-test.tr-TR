---
title: "SQL ve Python kullanarak SQL Server verileri için aaaCreate özellikleri | Microsoft Docs"
description: "SQL Azure işlem verileri"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: 
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;fashah;garye
ms.openlocfilehash: 223352edb0377a159333e7528ad03c43902e6f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a>SQL ve Python kullanarak SQL Server’daki verilerin özelliklerini oluşturma
Bu belge nasıl toogenerate özellikleri algoritmaları Yardım Azure üzerinde bir SQL Server VM depolanan veriler için hello verileri daha verimli bir şekilde bilgi gösterir. Bu SQL kullanarak veya Python, her ikisi de aşağıda gösterildiği gibi bir programlama dili kullanılarak yapılabilir.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Bu **menü** nasıl toocreate çeşitli ortamlarda veri özellikleri açıklamak tootopics bağlar. Bu görev bir hello adımdır [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

> [!NOTE]
> Pratik bir örnek için hello başvurabilirsiniz [NYC ücreti dataset](http://www.andresmh.com/nyctaxitrips/) ve toohello başlıklı IPNB başvuruda [IPython not defteri ve SQL Server kullanarak NYC veri wrangling](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) bir uçtan uca gözden geçirme.
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu makalede, sahip olduğunuz varsayılmaktadır:

* Bir Azure depolama hesabı oluşturuldu. Yönergeler gerekiyorsa bkz [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Verilerinizi SQL Server içinde depolanır. Yüklemediyseniz, bkz: [Azure Machine Learning için verileri tooan Azure SQL veritabanı taşıma](machine-learning-data-science-move-sql-azure.md) nasıl toomove hello var. veri hakkında yönergeler için.

## <a name="sql-featuregen"></a>SQL ile özelliği oluşturma
Bu bölümde, SQL kullanarak özellik oluşturmanın yolları açıklanmaktadır:  

1. [Özellik oluşturma sayısına dayalı](#sql-countfeature)
2. [Binning özelliği oluşturma](#sql-binningfeature)
3. [Tek bir sütundan Hello özellikleri alınıyor](#sql-featurerollout)

> [!NOTE]
> Ek özellikler oluşturmak sonra sütunları toohello var olan tablo olarak ekleyin veya hello ek özellikler ve hello özgün tabloyla katılabilir birincil anahtar, ile yeni bir tablo oluşturun.
> 
> 

### <a name="sql-countfeature"></a>Özellik oluşturma sayısına dayalı
Bu belge sayısı özellikleri oluşturmanın iki yolu gösterir. 'where' yan tümcesi hello ikinci yöntemi kullanır hello ve koşullu toplam Hello ilk yöntemi kullanır. Bunlar ardından özelliklerle hello özgün (birincil anahtar sütunlarını kullanarak) tablosu toohave sayısı hello özgün verilerin yanında katılabilir.

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <a name="sql-binningfeature"></a>Binning özelliği oluşturma
Merhaba aşağıdaki örnekte nasıl toogenerate özellikleri (5 depo kullanarak) binning bir özellik olarak bunun yerine kullanılabilir sayısal bir sütun binned gösterilmektedir:

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>Tek bir sütundan Hello özellikleri alınıyor
Bu bölümde tooroll kullanıma tek bir sütun tablo toogenerate ek özellikler gösterilmektedir. Merhaba örneği toogenerate özellikleri çalıştığınız hello tabloda enlem veya boylam bir sütun olduğunu varsayar.

Enlem/boylam konumu verileri kısa öncü İşte (stackoverflow kaynak var `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`). Bu yararlı toounderstand featurizing hello konum alanı önce oluşur:

* Merhaba oturum bize biz Kuzey veya Güney, Doğu veya Batı Merhaba dünya üzerindeki olup söyler.
* Sıfır olmayan bir yüzlerce basamağın yuvarlanacağını belirtir bize biz boylam değil enlem kullanmakta olduğunuz!
* Merhaba onlarca basamaklı bir konum tooabout 1.000 kilometre sağlar. Bize ne kıtada veya üzerinde duyuyoruz Okyanusu hakkında yararlı bilgiler sağlar.
* Merhaba birimleri basamak (bir ondalık derece) bir konum yukarı too111 kilometre (60 Deniz mili, yaklaşık 69 mil) sağlar. Bu kabaca hangi büyük durumunun veya biz bulunan ülke bize.
* Merhaba ilk ondalık yerdir değerinde too11.1 km: komşu büyük Şehir'dan büyük bir şehir hello konumunu ayırt edebilirsiniz.
* Merhaba ikinci ondalık yerdir değerinde too1.1 km: sonraki hello bir village ayırabilirsiniz.
* Merhaba üçüncü ondalık değer too110 m: büyük agricultural alan veya Kurumsal kampüs tanımlayabilirsiniz yerdir.
* Merhaba dördüncü ondalık değer too11 m: kara paket tanımlayabilirsiniz yerdir. Bu girişim olmadığı düzeltilemeyen bir GPS birimle tipik doğruluğunu karşılaştırılabilir toohello olur.
* Merhaba beşinci ondalık basamak değerinde too1.1 m: olduğu ağaçlar birbirinden ayırt etmek. Doğruluk toothis düzeyi ticari GPS birimleri ile yalnızca ile fark düzeltme elde edilebilir.
* Merhaba altıncı ondalık değer bu yapıları Windows'un, tasarlamak için ayrıntılı yerleştirmek için yollar oluşturma kullanabileceğiniz too0.11 m: yerdir. Glaciers ve rivers hareketlerini izlemek için birden çok iyi yeterli olmalıdır. Bu differentially düzeltilmiş GPS gibi GPS ile painstaking ölçüleri gerçekleştirerek elde edilebilir.

Merhaba konum bilgileri featurized gibi bölge, konum ve Şehir bilgilerini ayırma olabilir. Bir kez Bing Haritalar API'si adresinde gibi bir REST uç noktası da çağırabilir Not `https://msdn.microsoft.com/library/ff701710.aspx` tooget hello bölge/bölge bilgileri.

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

temel özellikler daha fazla kullanılabilir konum yukarıda Hello toogenerate ek sayısı özellikleri daha önce açıklandığı gibi kullanılır.

> [!TIP]
> Program aracılığıyla dilinizi tercih kullanarak hello kayıtları ekleyebilirsiniz. Tooinsert hello veri öbekleri tooimprove yazma verimliliği gerekebilir [nasıl hello örnek denetleyin toodo bu pyodbc burada kullanarak](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).
> Başka bir alternatif veritabanı hello kullanarak tooinsert verilerdir [BCP yardımcı programı](https://msdn.microsoft.com/library/ms162802.aspx)
> 
> 

### <a name="sql-aml"></a>Machine Learning tooAzure bağlanma
Yeni oluşturulan hello özelliği sütun tooan var olan tablo olarak eklenebilir veya yeni bir tabloda depolanır ve machine learning için hello özgün tabloyla katılmış. Özellikler oluşturulan ya da zaten oluşturduysanız, hello kullanılarak erişilir [veri içeri aktarma](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) aşağıda gösterildiği gibi Azure ML modülünde:

![azureml okuyucuları](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <a name="python"></a>Python gibi programlama dilini kullanma
Merhaba veriler SQL Server'da olduğunda Python toogenerate özelliklerini kullanarak konusu benzer tooprocessing veri açıklandığı gibi Python kullanarak Azure blob [, veri bilimi ortamında işlem Azure Blob verileri](machine-learning-data-science-process-data-blob.md). Merhaba veri pandas veri çerçeveye hello veritabanından yüklenen toobe gerekir ve ardından daha fazla işlenebilir. Biz toohello veritabanına bağlanma ve bu bölümdeki hello veri çerçevesine hello verileri yüklenirken hello işleminde belge.

bağlantı dizesi biçimi aşağıdaki hello pyodbc (Değiştir servername, dbname, kullanıcı adı ve parola, belirli değerleri içeren) kullanarak Python kullanılan tooconnect tooa SQL Server veritabanından olabilir:

    #Set up hello SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Merhaba [Pandas Kitaplığı](http://pandas.pydata.org/) Python içinde Python programlama için veri işleme için zengin bir veri yapılarını ve veri çözümleme araçları sağlar. Aşağıdaki Hello kodu hello sonuçları bir SQL Server veritabanından Pandas veri çerçeveye döndürülen okur:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Konularda gibi hello Pandas veri çerçevesi ile çalışabilirsiniz artık [Panda kullanarak Azure blob depolama verileri için özellikler oluşturmak](machine-learning-data-science-create-features-blob.md).

