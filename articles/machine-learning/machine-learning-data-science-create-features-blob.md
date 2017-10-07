---
title: "aaaCreate özellikleri Azure blob depolama veri Panda kullanarak | Microsoft Docs"
description: "Merhaba Panda Python paket ile Azure blob kapsayıcısında depolanan veriler için nasıl toocreate özellikleri."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 676b5fb0-4c89-4516-b3a8-e78ae3ca078d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: 8594046c5d76a36ad87fc77e407752489d30afcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a>Panda kullanarak Azure blob depolama verilerinin özelliklerini oluşturma
Bu belge toocreate hello kullanarak Azure blob kapsayıcısında depolanan verileri nasıl özellikleri gösterir [Pandas](http://pandas.pydata.org/) Python paket. Anahat oluşturma nasıl tooload hello veri Panda veri çerçevesine gösterir sonra nasıl göstergesi değerlerle Python komut dosyalarını kullanarak ve özellikleri binning toogenerate kategorik özellikleri.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Bu **menü** nasıl toocreate çeşitli ortamlarda veri özellikleri açıklamak tootopics bağlar. Bu görev bir hello adımdır [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Ön koşullar
Bu makale bir Azure blob storage hesabı oluşturduysanız ve verilerinizi var. depoladığınız varsayar. Bir hesap yönergeleri tooset gerekirse bkz [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account)

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Pandas veri çerçeveye Hello veri yükleme
Sipariş toodo keşfedin ve bir veri kümesini değiştirmek, ardından Pandas veri çerçevede yüklenen hello blob kaynak tooa yerel dosyasından indirilmelidir. Bu yordam için hello adımları toofollow şunlardır:

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

## <a name="blob-featuregen"></a>Özellik oluşturma
Merhaba sonraki iki bölümde nasıl toogenerate kategorik göstergesi değerleri ve binning özellikleri Python betiklerini kullanarak gösterir.

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
3. Merhaba verileri blob hello kullanarak okunabilir artık Azure Machine Learning hello [veri içeri aktarma](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) ekranda hello aşağıda gösterildiği gibi Modülü:

![Okuyucu blob](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

