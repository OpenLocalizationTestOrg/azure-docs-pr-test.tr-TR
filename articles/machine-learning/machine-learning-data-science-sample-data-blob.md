---
title: aaaSample verileri Azure blob depolamada | Microsoft Docs
description: "Örnek verileri Azure Blob Depolama"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8d9ad2c-86c5-43d6-80b8-d355b5c0dccf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: cceadf1fb1fb4804fc5b5a3da55c82854651026e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Örnek verileri Azure blob depolama
Bu belge örnekleme verileri programlı olarak karşıdan yükleyip Python içinde yazılmış yordamları kullanarak örnekleme Azure blob storage'da depolanan kapsar.

Merhaba aşağıdaki **menü** açıklayan tootopics bağlantıları nasıl çeşitli depolama ortamları toosample verileri. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Neden verilerinizi örnek?**
Tooanalyze planladığınız hello veri kümesi, bu genellikle iyi bir fikir toodown örnek hello veri tooreduce büyükse, tooa daha küçük, ancak temsili ve daha kolay yönetilebilir boyutu. Bu, veri anlama, keşfi ve özellik Mühendisliği kolaylaştırır. Kendi hello Cortana Analytics işlem içinde tooenable hızlı prototipi oluşturulurken hello veri işleme işlevleri ve makine öğrenimi modellerinin oluşturulmasına rolüdür.

Merhaba adımda bu örnekleme görevdir [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="download-and-down-sample-data"></a>Karşıdan yükleme ve aşağı örnek veriler
1. Merhaba veri hello blob örnek Python kodu aşağıdaki hello hizmetinden kullanarak Azure blob storage indirin: 
   
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

2. Yukarıda indirdiğiniz hello dosyasından Pandas verileri-çerçeve içine verilerini okur.
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. Aşağı örnekli hello kullanarak hello veri `numpy`'s `random.choice` gibi:
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

Şimdi veri çerçevesi ile Merhaba yüzde 1 örnek daha fazla araştırması ve özellik oluşturmak için yukarıdaki hello çalışabilirsiniz.

## <a name="heading"></a>Verileri yüklemek ve Azure Machine Learning okuma
Aşağıdaki örnek kod toodown örnek hello veri hello kullanmak ve doğrudan Azure Machine Learning kullanın:

1. Merhaba veri çerçeve tooa yerel dosyasına yazma
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. Merhaba yerel dosya tooan Azure karşıya örnek kod aşağıdaki hello kullanarak blob:
   
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
            print ("Something went wrong with uploading toohello blob:"+ BLOBNAME)

3. Azure Machine Learning kullanarak Azure blob hello Hello veri okuma [veri içeri aktarma](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) hello resimde gösterildiği gibi:

![Okuyucu blob](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

