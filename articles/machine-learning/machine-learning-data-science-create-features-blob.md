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
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="883f7-103">Panda kullanarak Azure blob depolama verilerinin özelliklerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="883f7-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="883f7-104">Bu belge toocreate hello kullanarak Azure blob kapsayıcısında depolanan verileri nasıl özellikleri gösterir [Pandas](http://pandas.pydata.org/) Python paket.</span><span class="sxs-lookup"><span data-stu-id="883f7-104">This document shows how toocreate features for data that is stored in Azure blob container using hello [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="883f7-105">Anahat oluşturma nasıl tooload hello veri Panda veri çerçevesine gösterir sonra nasıl göstergesi değerlerle Python komut dosyalarını kullanarak ve özellikleri binning toogenerate kategorik özellikleri.</span><span class="sxs-lookup"><span data-stu-id="883f7-105">After outlining how tooload hello data into a Panda data frame, it shows how toogenerate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="883f7-106">Bu **menü** nasıl toocreate çeşitli ortamlarda veri özellikleri açıklamak tootopics bağlar.</span><span class="sxs-lookup"><span data-stu-id="883f7-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="883f7-107">Bu görev bir hello adımdır [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="883f7-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="883f7-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="883f7-108">Prerequisites</span></span>
<span data-ttu-id="883f7-109">Bu makale bir Azure blob storage hesabı oluşturduysanız ve verilerinizi var. depoladığınız varsayar.</span><span class="sxs-lookup"><span data-stu-id="883f7-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="883f7-110">Bir hesap yönergeleri tooset gerekirse bkz [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="883f7-110">If you need instructions tooset up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="883f7-111">Pandas veri çerçeveye Hello veri yükleme</span><span class="sxs-lookup"><span data-stu-id="883f7-111">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="883f7-112">Sipariş toodo keşfedin ve bir veri kümesini değiştirmek, ardından Pandas veri çerçevede yüklenen hello blob kaynak tooa yerel dosyasından indirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="883f7-112">In order toodo explore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="883f7-113">Bu yordam için hello adımları toofollow şunlardır:</span><span class="sxs-lookup"><span data-stu-id="883f7-113">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="883f7-114">Azure'dan Hello veri indirme blob hello blob hizmeti kullanarak örnek Python kodu aşağıdaki ile.</span><span class="sxs-lookup"><span data-stu-id="883f7-114">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="883f7-115">Merhaba değişkeni hello kodda belirli değerleriniz ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="883f7-115">Replace hello variable in hello code below with your specific values:</span></span>
   
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
2. <span data-ttu-id="883f7-116">Bir Pandas verileri-çerçevesinden hello içine hello veri okuma dosya indirilir.</span><span class="sxs-lookup"><span data-stu-id="883f7-116">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="883f7-117">Şimdi, hazır tooexplore hello verileri ve bu veri kümesi özellikleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="883f7-117">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="883f7-118"><a name="blob-featuregen"></a>Özellik oluşturma</span><span class="sxs-lookup"><span data-stu-id="883f7-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="883f7-119">Merhaba sonraki iki bölümde nasıl toogenerate kategorik göstergesi değerleri ve binning özellikleri Python betiklerini kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="883f7-119">hello next two sections show how toogenerate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="883f7-120"><a name="blob-countfeature"></a>Gösterge değeri özellik nesil dayalı</span><span class="sxs-lookup"><span data-stu-id="883f7-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="883f7-121">Kategorik özellikler aşağıdaki gibi oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="883f7-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="883f7-122">Merhaba dağıtım hello kategorik sütunun inceleyin:</span><span class="sxs-lookup"><span data-stu-id="883f7-122">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="883f7-123">Her hello sütun değerleri için gösterge değerlerini oluşturmak</span><span class="sxs-lookup"><span data-stu-id="883f7-123">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="883f7-124">Merhaba gösterge sütunu hello özgün veri çerçevesi ile birleştirme</span><span class="sxs-lookup"><span data-stu-id="883f7-124">Join hello indicator column with hello original data frame</span></span>
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="883f7-125">Özgün değişkeni Hello kendisini kaldırın:</span><span class="sxs-lookup"><span data-stu-id="883f7-125">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="883f7-126"><a name="blob-binningfeature"></a>Binning özelliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="883f7-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="883f7-127">Binned özellikleri oluşturmak için size aşağıdaki gibi ilerleyin:</span><span class="sxs-lookup"><span data-stu-id="883f7-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="883f7-128">Sütunları toobin sayısal bir sütun dizisi Ekle</span><span class="sxs-lookup"><span data-stu-id="883f7-128">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="883f7-129">Boolean değişkenleri binning tooa dizisini Dönüştür</span><span class="sxs-lookup"><span data-stu-id="883f7-129">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="883f7-130">Son olarak, hello kukla değişkenleri geri toohello özgün veri çerçevesi katılma</span><span class="sxs-lookup"><span data-stu-id="883f7-130">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="883f7-131"><a name="sql-featuregen"></a>Veri yazmada tooAzure blob ve Azure Machine Learning kullanma yedekleyin</span><span class="sxs-lookup"><span data-stu-id="883f7-131"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="883f7-132">Merhaba veri incelediniz ve gerekli özellikleri hello oluşturulan sonra hello verilerini karşıya yükleyebilir (örneklenen veya featurized) tooan Azure blob ve hello aşağıdaki adımları kullanarak Azure Machine Learning ile kullanabilir: ek özellikler hello oluşturduğunuz unutmayın Azure Machine Learning Studio de.</span><span class="sxs-lookup"><span data-stu-id="883f7-132">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="883f7-133">Merhaba veri çerçeve toolocal dosyasına yazma</span><span class="sxs-lookup"><span data-stu-id="883f7-133">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="883f7-134">Merhaba veri tooAzure blob aşağıdaki gibi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="883f7-134">Upload hello data tooAzure blob as follows:</span></span>
   
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
3. <span data-ttu-id="883f7-135">Merhaba verileri blob hello kullanarak okunabilir artık Azure Machine Learning hello [veri içeri aktarma](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) ekranda hello aşağıda gösterildiği gibi Modülü:</span><span class="sxs-lookup"><span data-stu-id="883f7-135">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in hello screen below:</span></span>

![Okuyucu blob](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

