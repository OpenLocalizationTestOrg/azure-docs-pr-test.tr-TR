---
title: Azure SQL Server'da verilerde aaaSample | Microsoft Docs
description: "Azure SQL Server'da örnek veri"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Azure üzerinde SQL Server örnek veri
Bu belgede Azure üzerinde SQL Server'daki toosample verilerin depolanma SQL veya hello Python programlama dili kullanılarak gösterir. Aynı zamanda, nasıl toomove verileri Azure Machine Learning tooa dosyası, onu karşıya kaydederek tooan Azure blob ve Azure Machine Learning Studio'ya okuma örneklenen gösterir.

Merhaba Python örnekleme kullanan hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC kitaplığı tooconnect tooSQL Azure ve hello sunucuda [Pandas](http://pandas.pydata.org/) kitaplığı toodo hello örnekleme.

> [!NOTE]
> Bu belgedeki Hello örnek SQL kodunu Azure üzerinde bir SQL Server veri bulunduğu bu hello varsayar. Lütfen değilse, çok bakın[Azure üzerinde veri tooSQL sunucu taşıma](machine-learning-data-science-move-sql-server-virtual-machine.md) konu hakkında yönergeler için toomove, veri tooSQL Azure sunucusunda.
> 
> 

Merhaba aşağıdaki **menü** açıklayan tootopics bağlantıları nasıl çeşitli depolama ortamları toosample verileri. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Neden verilerinizi örnek?**
Tooanalyze planladığınız hello veri kümesi, bu genellikle iyi bir fikir toodown örnek hello veri tooreduce büyükse, tooa daha küçük, ancak temsili ve daha kolay yönetilebilir boyutu. Bu, veri anlama, keşfi ve özellik Mühendisliği kolaylaştırır. Merhaba, rolde [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) tooenable hızlı prototipi oluşturulurken hello veri işleme işlevleri ve makine öğrenimi modellerinin oluşturulmasına olduğu.

Merhaba adımda bu örnekleme görevdir [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="SQL"></a>SQL kullanarak
Bu bölümde hello veritabanındaki SQL tooperform basit rastgele örnekleme hello veri karşı kullanarak çeşitli yöntemler açıklanmaktadır. Lütfen, veri boyutu ve onun dağıtım dayalı bir yöntem seçin.

Merhaba aşağıdaki iki öğeleri nasıl toouse NEWID SQL Server tooperform içinde hello örnekleme gösterir. Merhaba seçtiğiniz yöntemi nasıl rastgele hello örnek toobe istediğiniz bağlıdır (aşağıdaki hello örnek kodu pk_id toobe otomatik olarak oluşturulan bir birincil anahtar varsayılır).

1. Daha az kesin rasgele örnek
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. Daha fazla rasgele örnek 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

Tablesample için örnekleme kullanılan yanı sıra aşağıda gösterilmektedir. Bu daha iyi bir yaklaşım (sihirbazın farklı sayfalarında verileri değil bağıntılı varsayılarak), veri boyutu büyükse ve hello sorgu toocomplete için makul bir sürede olabilir.

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> Keşfetmek ve yeni bir tabloda depolayarak örneklenen bu verilerden Özellikleri Oluştur
> 
> 

### <a name="sql-aml"></a>Machine Learning tooAzure bağlanma
Hello Azure Machine Learning hello örnek sorgular yukarıda doğrudan kullanabilirsiniz [veri içeri aktarma] [ import-data] hello modülü toodown örnek hello verileri uçarak ve bir Azure Machine Learning deneme getirin. Merhaba okuyucu modülü tooread hello örneklenen verileri kullanarak bir ekran görüntüsü aşağıda gösterilmiştir:

![Okuyucu sql][1]

## <a name="python"></a>Merhaba Python programlama dilini kullanma
Bu bölüm hello kullanarak gösterir [pyodbc Kitaplığı](https://code.google.com/p/pyodbc/) tooestablish bir ODBC Python tooa SQL server veritabanına bağlan. Merhaba veritabanı bağlantı dizesi şu şekildedir: (servername, dbname, kullanıcı adı ve parola yapılandırmanızı değiştirin):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Merhaba [Pandas](http://pandas.pydata.org/) Python kitaplıkta Python programlama için veri işleme için zengin bir veri yapılarını ve veri çözümleme araçları sağlar. Aşağıdaki Hello kodu hello veri % 0,1 örneğini Azure SQL veritabanındaki bir tablo Pandas verisine okur:

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

Şimdi örneklenen hello veri hello Pandas veri çerçevesinde çalışabilirsiniz. 

### <a name="python-aml"></a>Machine Learning tooAzure bağlanma
Aşağıdaki örnek kod toosave hello aşağı örneklenen verileri tooa dosyasına hello kullanın ve tooan Azure blob yükleyin. Merhaba blob Hello verileri doğrudan okunabilir bir Azure Machine Learning deneme hello kullanarak [veri içeri aktarma] [ import-data] modülü. Merhaba adımlar aşağıdaki gibidir: 

1. Merhaba pandas veri çerçeve tooa yerel dosyasına yazma
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Yerel dosya tooAzure blob karşıya yükleme
   
        from azure.storage import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. Azure Machine Learning kullanarak Azure blob üzerinden veri okuma [veri içeri aktarma] [ import-data] Merhaba ekranında Al aşağıda gösterildiği gibi Modülü:

![Okuyucu blob][2]

## <a name="hello-team-data-science-process-in-action-example"></a>Eylem örnekte Hello takım veri bilimi işlemi
Bir ortak bir veri kümesini kullanarak hello takım veri bilimi işlemi bir uçtan uca kılavuz örneği için bkz [takım veri bilimi işlemi sürüyor: SQL sunucusu kullanarak](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
