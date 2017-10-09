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
# <span data-ttu-id="49707-103"><a name="heading"></a>Örnek verileri Azure blob depolama</span><span class="sxs-lookup"><span data-stu-id="49707-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="49707-104">Bu belge örnekleme verileri programlı olarak karşıdan yükleyip Python içinde yazılmış yordamları kullanarak örnekleme Azure blob storage'da depolanan kapsar.</span><span class="sxs-lookup"><span data-stu-id="49707-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="49707-105">Merhaba aşağıdaki **menü** açıklayan tootopics bağlantıları nasıl çeşitli depolama ortamları toosample verileri.</span><span class="sxs-lookup"><span data-stu-id="49707-105">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="49707-106">**Neden verilerinizi örnek?**</span><span class="sxs-lookup"><span data-stu-id="49707-106">**Why sample your data?**</span></span>
<span data-ttu-id="49707-107">Tooanalyze planladığınız hello veri kümesi, bu genellikle iyi bir fikir toodown örnek hello veri tooreduce büyükse, tooa daha küçük, ancak temsili ve daha kolay yönetilebilir boyutu.</span><span class="sxs-lookup"><span data-stu-id="49707-107">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="49707-108">Bu, veri anlama, keşfi ve özellik Mühendisliği kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="49707-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="49707-109">Kendi hello Cortana Analytics işlem içinde tooenable hızlı prototipi oluşturulurken hello veri işleme işlevleri ve makine öğrenimi modellerinin oluşturulmasına rolüdür.</span><span class="sxs-lookup"><span data-stu-id="49707-109">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="49707-110">Merhaba adımda bu örnekleme görevdir [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="49707-110">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="49707-111">Karşıdan yükleme ve aşağı örnek veriler</span><span class="sxs-lookup"><span data-stu-id="49707-111">Download and down-sample data</span></span>
1. <span data-ttu-id="49707-112">Merhaba veri hello blob örnek Python kodu aşağıdaki hello hizmetinden kullanarak Azure blob storage indirin:</span><span class="sxs-lookup"><span data-stu-id="49707-112">Download hello data from Azure blob storage using hello blob service from hello following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="49707-113">Yukarıda indirdiğiniz hello dosyasından Pandas verileri-çerçeve içine verilerini okur.</span><span class="sxs-lookup"><span data-stu-id="49707-113">Read data into a Pandas data-frame from hello file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="49707-114">Aşağı örnekli hello kullanarak hello veri `numpy`'s `random.choice` gibi:</span><span class="sxs-lookup"><span data-stu-id="49707-114">Down-sample hello data using hello `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="49707-115">Şimdi veri çerçevesi ile Merhaba yüzde 1 örnek daha fazla araştırması ve özellik oluşturmak için yukarıdaki hello çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49707-115">Now you can work with hello above data frame with hello 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="49707-116"><a name="heading"></a>Verileri yüklemek ve Azure Machine Learning okuma</span><span class="sxs-lookup"><span data-stu-id="49707-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="49707-117">Aşağıdaki örnek kod toodown örnek hello veri hello kullanmak ve doğrudan Azure Machine Learning kullanın:</span><span class="sxs-lookup"><span data-stu-id="49707-117">You can use hello following sample code toodown-sample hello data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="49707-118">Merhaba veri çerçeve tooa yerel dosyasına yazma</span><span class="sxs-lookup"><span data-stu-id="49707-118">Write hello data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="49707-119">Merhaba yerel dosya tooan Azure karşıya örnek kod aşağıdaki hello kullanarak blob:</span><span class="sxs-lookup"><span data-stu-id="49707-119">Upload hello local file tooan Azure blob using hello following sample code:</span></span>
   
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

3. <span data-ttu-id="49707-120">Azure Machine Learning kullanarak Azure blob hello Hello veri okuma [veri içeri aktarma](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) hello resimde gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="49707-120">Read hello data from hello Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in hello image below:</span></span>

![Okuyucu blob](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

