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
# <span data-ttu-id="432cb-103"><a name="heading"></a>Gelişmiş analytics ile Azure blob verileri işleme</span><span class="sxs-lookup"><span data-stu-id="432cb-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="432cb-104">Bu belge, araştırma veri ve Azure Blob storage'da depolanan verileri oluşturma özellikleri kapsar.</span><span class="sxs-lookup"><span data-stu-id="432cb-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="432cb-105">Pandas veri çerçeveye Hello veri yükleme</span><span class="sxs-lookup"><span data-stu-id="432cb-105">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="432cb-106">Sipariş tooexplore içinde ve bir veri kümesini değiştirmek, ardından Pandas veri çerçevede yüklenen hello blob kaynak tooa yerel dosyasından indirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="432cb-106">In order tooexplore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="432cb-107">Bu yordam için hello adımları toofollow şunlardır:</span><span class="sxs-lookup"><span data-stu-id="432cb-107">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="432cb-108">Azure'dan Hello veri indirme blob hello blob hizmeti kullanarak örnek Python kodu aşağıdaki ile.</span><span class="sxs-lookup"><span data-stu-id="432cb-108">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="432cb-109">Merhaba değişkeni hello kodda belirli değerleriniz ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="432cb-109">Replace hello variable in hello code below with your specific values:</span></span> 
   
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
2. <span data-ttu-id="432cb-110">Bir Pandas verileri-çerçevesinden hello içine hello veri okuma dosya indirilir.</span><span class="sxs-lookup"><span data-stu-id="432cb-110">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="432cb-111">Şimdi, hazır tooexplore hello verileri ve bu veri kümesi özellikleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="432cb-111">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="432cb-112"><a name="blob-dataexploration"></a>Veri keşfi</span><span class="sxs-lookup"><span data-stu-id="432cb-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="432cb-113">Pandas kullanarak tooexplore veri yolları bazı örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="432cb-113">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="432cb-114">Hello satır ve sütun sayılarını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="432cb-114">Inspect hello number of rows and columns</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="432cb-115">Merhaba inceleyin veya aşağıdaki şekilde hello kümesindeki birkaç satır son:</span><span class="sxs-lookup"><span data-stu-id="432cb-115">Inspect hello first or last few rows in hello dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="432cb-116">Her sütunun örnek kod aşağıdaki hello kullanarak olarak içeri aktarıldı hello veri türünü denetleyin</span><span class="sxs-lookup"><span data-stu-id="432cb-116">Check hello data type each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="432cb-117">Merhaba temel istatistikleri hello veri kümesindeki hello sütunlar için aşağıdaki gibi denetleyin</span><span class="sxs-lookup"><span data-stu-id="432cb-117">Check hello basic stats for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="432cb-118">Her bir sütunun değeri girişlerinde hello sayısı gibi bakın</span><span class="sxs-lookup"><span data-stu-id="432cb-118">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="432cb-119">Merhaba gerçek sayısı örnek kod aşağıdaki hello kullanarak her bir sütunun giriş karşı eksik değerleri Say</span><span class="sxs-lookup"><span data-stu-id="432cb-119">Count missing values versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="432cb-120">Belirli bir sütun için eksik değerleri hello verileri varsa, aşağıdaki gibi silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="432cb-120">If you have missing values for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="432cb-121">dataframe_blobdata_noNA dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape =</span><span class="sxs-lookup"><span data-stu-id="432cb-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="432cb-122">Başka bir şekilde tooreplace eksik değerleri hello modu işleviyle şöyledir:</span><span class="sxs-lookup"><span data-stu-id="432cb-122">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="432cb-123">dataframe_blobdata_mode dataframe_blobdata.fillna = ({< column_name >: dataframe_blobdata ['< column_name >'] .mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="432cb-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="432cb-124">Değişken sayıda depo tooplot hello dağıtım değişkenin kullanarak bir histogram çizim oluşturma</span><span class="sxs-lookup"><span data-stu-id="432cb-124">Create a histogram plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="432cb-125">Bir scatterplot veya hello yerleşik bağıntı işlevi kullanarak değişkenleri arasındaki bağıntıları bakın</span><span class="sxs-lookup"><span data-stu-id="432cb-125">Look at correlations between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="432cb-126"><a name="blob-featuregen"></a>Özellik oluşturma</span><span class="sxs-lookup"><span data-stu-id="432cb-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="432cb-127">Biz, Python gibi kullanarak özellik oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="432cb-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="432cb-128"><a name="blob-countfeature"></a>Gösterge değeri özellik nesil dayalı</span><span class="sxs-lookup"><span data-stu-id="432cb-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="432cb-129">Kategorik özellikler aşağıdaki gibi oluşturulabilir:</span><span class="sxs-lookup"><span data-stu-id="432cb-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="432cb-130">Merhaba dağıtım hello kategorik sütunun inceleyin:</span><span class="sxs-lookup"><span data-stu-id="432cb-130">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="432cb-131">Her hello sütun değerleri için gösterge değerlerini oluşturmak</span><span class="sxs-lookup"><span data-stu-id="432cb-131">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="432cb-132">Merhaba gösterge sütunu hello özgün veri çerçevesi ile birleştirme</span><span class="sxs-lookup"><span data-stu-id="432cb-132">Join hello indicator column with hello original data frame</span></span> 
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="432cb-133">Özgün değişkeni Hello kendisini kaldırın:</span><span class="sxs-lookup"><span data-stu-id="432cb-133">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="432cb-134"><a name="blob-binningfeature"></a>Binning özelliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="432cb-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="432cb-135">Binned özellikleri oluşturmak için size aşağıdaki gibi ilerleyin:</span><span class="sxs-lookup"><span data-stu-id="432cb-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="432cb-136">Sütunları toobin sayısal bir sütun dizisi Ekle</span><span class="sxs-lookup"><span data-stu-id="432cb-136">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="432cb-137">Boolean değişkenleri binning tooa dizisini Dönüştür</span><span class="sxs-lookup"><span data-stu-id="432cb-137">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="432cb-138">Son olarak, hello kukla değişkenleri geri toohello özgün veri çerçevesi katılma</span><span class="sxs-lookup"><span data-stu-id="432cb-138">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="432cb-139"><a name="sql-featuregen"></a>Veri yazmada tooAzure blob ve Azure Machine Learning kullanma yedekleyin</span><span class="sxs-lookup"><span data-stu-id="432cb-139"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="432cb-140">Merhaba veri incelediniz ve gerekli özellikleri hello oluşturulan sonra hello verilerini karşıya yükleyebilir (örneklenen veya featurized) tooan Azure blob ve hello aşağıdaki adımları kullanarak Azure Machine Learning ile kullanabilir: ek özellikler hello oluşturduğunuz unutmayın Azure Machine Learning Studio de.</span><span class="sxs-lookup"><span data-stu-id="432cb-140">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="432cb-141">Merhaba veri çerçeve toolocal dosyasına yazma</span><span class="sxs-lookup"><span data-stu-id="432cb-141">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="432cb-142">Merhaba veri tooAzure blob aşağıdaki gibi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="432cb-142">Upload hello data tooAzure blob as follows:</span></span>
   
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
3. <span data-ttu-id="432cb-143">Merhaba verileri blob hello kullanarak okunabilir artık Azure Machine Learning hello [veri içeri aktarma] [ import-data] ekranda hello aşağıda gösterildiği gibi Modülü:</span><span class="sxs-lookup"><span data-stu-id="432cb-143">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data][import-data] module as shown in hello screen below:</span></span>

![Okuyucu blob][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

