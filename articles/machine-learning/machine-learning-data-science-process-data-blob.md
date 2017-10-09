---
title: "aaaProcess Azure blob Gelişmiş analitik verilerle | Microsoft Docs"
description: "İşlem verileri Azure Blob depolamada."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8a59078-91d3-4440-b85c-430363c3f4d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5911d4211c4135680555a8cdd99e745499a24215
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Gelişmiş analytics ile Azure blob verileri işleme
Bu belge, araştırma veri ve Azure Blob storage'da depolanan verileri oluşturma özellikleri kapsar. 

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Pandas veri çerçeveye Hello veri yükleme
Sipariş tooexplore içinde ve bir veri kümesini değiştirmek, ardından Pandas veri çerçevede yüklenen hello blob kaynak tooa yerel dosyasından indirilmelidir. Bu yordam için hello adımları toofollow şunlardır:

1. Azure'dan Hello veri indirme blob hello blob hizmeti kullanarak örnek Python kodu aşağıdaki ile. Merhaba değişkeni hello kodda belirli değerleriniz ile değiştirin: 
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds toodownload "+blobname) % (t2 - t1))
2. Bir Pandas verileri-çerçevesinden hello içine hello veri okuma dosya indirilir.
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

Şimdi, hazır tooexplore hello verileri ve bu veri kümesi özellikleri oluşturur.

## <a name="blob-dataexploration"></a>Veri keşfi
Pandas kullanarak tooexplore veri yolları bazı örnekleri şunlardır:

1. Hello satır ve sütun sayılarını inceleyin. 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. Merhaba inceleyin veya aşağıdaki şekilde hello kümesindeki birkaç satır son:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Her sütunun örnek kod aşağıdaki hello kullanarak olarak içeri aktarıldı hello veri türünü denetleyin
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Merhaba temel istatistikleri hello veri kümesindeki hello sütunlar için aşağıdaki gibi denetleyin
   
        dataframe_blobdata.describe()
5. Her bir sütunun değeri girişlerinde hello sayısı gibi bakın
   
        dataframe_blobdata['<column_name>'].value_counts()
6. Merhaba gerçek sayısı örnek kod aşağıdaki hello kullanarak her bir sütunun giriş karşı eksik değerleri Say
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Belirli bir sütun için eksik değerleri hello verileri varsa, aşağıdaki gibi silebilirsiniz:
   
     dataframe_blobdata_noNA dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape =
   
   Başka bir şekilde tooreplace eksik değerleri hello modu işleviyle şöyledir:
   
     dataframe_blobdata_mode dataframe_blobdata.fillna = ({< column_name >: dataframe_blobdata ['< column_name >'] .mode()[0]})        
8. Değişken sayıda depo tooplot hello dağıtım değişkenin kullanarak bir histogram çizim oluşturma    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Bir scatterplot veya hello yerleşik bağıntı işlevi kullanarak değişkenleri arasındaki bağıntıları bakın
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <a name="blob-featuregen"></a>Özellik oluşturma
Biz, Python gibi kullanarak özellik oluşturabilirsiniz:

### <a name="blob-countfeature"></a>Gösterge değeri özellik nesil dayalı
Kategorik özellikler aşağıdaki gibi oluşturulabilir:

1. Merhaba dağıtım hello kategorik sütunun inceleyin:
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. Her hello sütun değerleri için gösterge değerlerini oluşturmak
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. Merhaba gösterge sütunu hello özgün veri çerçevesi ile birleştirme 
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. Özgün değişkeni Hello kendisini kaldırın:
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <a name="blob-binningfeature"></a>Binning özelliği oluşturma
Binned özellikleri oluşturmak için size aşağıdaki gibi ilerleyin:

1. Sütunları toobin sayısal bir sütun dizisi Ekle
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. Boolean değişkenleri binning tooa dizisini Dönüştür
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. Son olarak, hello kukla değişkenleri geri toohello özgün veri çerçevesi katılma
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <a name="sql-featuregen"></a>Veri yazmada tooAzure blob ve Azure Machine Learning kullanma yedekleyin
Merhaba veri incelediniz ve gerekli özellikleri hello oluşturulan sonra hello verilerini karşıya yükleyebilir (örneklenen veya featurized) tooan Azure blob ve hello aşağıdaki adımları kullanarak Azure Machine Learning ile kullanabilir: ek özellikler hello oluşturduğunuz unutmayın Azure Machine Learning Studio de. 

1. Merhaba veri çerçeve toolocal dosyasına yazma
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Merhaba veri tooAzure blob aşağıdaki gibi yükleyin:
   
        from azure.storage.blob import BlobService
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
3. Merhaba verileri blob hello kullanarak okunabilir artık Azure Machine Learning hello [veri içeri aktarma] [ import-data] ekranda hello aşağıda gösterildiği gibi Modülü:

![Okuyucu blob][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

