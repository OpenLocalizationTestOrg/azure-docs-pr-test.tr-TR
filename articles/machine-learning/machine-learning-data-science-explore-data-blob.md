---
title: aaaExplore verileri Azure blob depolama Pandas ile | Microsoft Docs
description: "Azure'da depolanan tooexplore veri nasıl Pandas kullanarak kapsayıcı blob."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: feaa9e54-01e0-48c8-a917-1eba0f9d9ec7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 28f3c0aebf2300006066c4b19dcb1f0a76a1deb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a>Panda ile Azure blob depolama verilerini keşfedin
Bu belge kapsayıcısı kullanarak Azure'da depolanan tooexplore verileri nasıl blob kapsar [Pandas](http://pandas.pydata.org/) Python paket.

Merhaba aşağıdaki **menü** nasıl toouse tooexplore veri çeşitli depolama ortamlarından araçları açıklamak tootopics bağlar. Bu görev bir hello adımdır [veri bilimi işlemi]().

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Ön koşullar
Bu makalede, sahip olduğunuz varsayılmaktadır:

* Bir Azure depolama hesabı oluşturuldu. Yönergeler gerekiyorsa bkz [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Verilerinizi bir Azure blob depolama hesabında depolanır. Yönergeler gerekiyorsa bkz [hareketli veri tooand Azure depolama biriminden](../storage/common/storage-moving-data.md)

## <a name="load-hello-data-into-a-pandas-dataframe"></a>Pandas DataFrame içine hello veri yükleme
tooexplore ve bir veri kümesini değiştirmek, ardından bir Pandas DataFrame yüklenen hello blob kaynak tooa yerel dosya, ilk indirilmelidir. Bu yordam için hello adımları toofollow şunlardır:

1. Azure'dan Hello veri indirme blobu blob hizmeti kullanarak Python kodu örneği aşağıdaki hello ile. Aşağıdaki kod, belirli değerleri içeren hello Hello değişkeninde değiştirin: 
   
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

## <a name="blob-dataexploration"></a>Veri keşfi Pandas kullanma örnekleri
Pandas kullanarak tooexplore veri yolları bazı örnekleri şunlardır:

1. Merhaba incelemek **satır ve sütunların sayısı** 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. **İnceleme** ilk veya son birkaç hello **satırları** dataset aşağıdaki hello içinde:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Merhaba denetleyin **veri türü** her sütun örnek kod aşağıdaki hello kullanarak olarak içeri aktarıldı
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Merhaba denetleyin **temel istatistikleri** hello sütunlar gibi veri kümesi hello için
   
        dataframe_blobdata.describe()
5. Her bir sütunun değeri girişlerinde hello sayısı gibi bakın
   
        dataframe_blobdata['<column_name>'].value_counts()
6. **Eksik değerleri saymak** hello gerçek sayısı örnek kod aşağıdaki hello kullanarak her bir sütunun giriş karşılaştırması
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Varsa **eksik değerleri** için belirli bir sütun hello verilerdeki, bunları aşağıdaki gibi düşürebilir:
   
     dataframe_blobdata_noNA dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape =
   
   Başka bir şekilde tooreplace eksik değerleri hello modu işleviyle şöyledir:
   
     dataframe_blobdata_mode dataframe_blobdata.fillna = ({< column_name >: dataframe_blobdata ['< column_name >'] .mode()[0]})        
8. Oluşturma bir **histogram** depo tooplot hello dağıtım değişkenin değişken sayıda kullanarak Çiz    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Bakmak **bağıntıları** bir scatterplot veya hello yerleşik bağıntı işlevi kullanarak değişkenleri arasında
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

