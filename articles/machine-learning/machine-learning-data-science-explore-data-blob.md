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
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="0f50a-103">Panda ile Azure blob depolama verilerini keşfedin</span><span class="sxs-lookup"><span data-stu-id="0f50a-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="0f50a-104">Bu belge kapsayıcısı kullanarak Azure'da depolanan tooexplore verileri nasıl blob kapsar [Pandas](http://pandas.pydata.org/) Python paket.</span><span class="sxs-lookup"><span data-stu-id="0f50a-104">This document covers how tooexplore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="0f50a-105">Merhaba aşağıdaki **menü** nasıl toouse tooexplore veri çeşitli depolama ortamlarından araçları açıklamak tootopics bağlar.</span><span class="sxs-lookup"><span data-stu-id="0f50a-105">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="0f50a-106">Bu görev bir hello adımdır [veri bilimi işlemi]().</span><span class="sxs-lookup"><span data-stu-id="0f50a-106">This task is a step in hello [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="0f50a-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0f50a-107">Prerequisites</span></span>
<span data-ttu-id="0f50a-108">Bu makalede, sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="0f50a-108">This article assumes that you have:</span></span>

* <span data-ttu-id="0f50a-109">Bir Azure depolama hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="0f50a-109">Created an Azure storage account.</span></span> <span data-ttu-id="0f50a-110">Yönergeler gerekiyorsa bkz [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="0f50a-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="0f50a-111">Verilerinizi bir Azure blob depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="0f50a-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="0f50a-112">Yönergeler gerekiyorsa bkz [hareketli veri tooand Azure depolama biriminden](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="0f50a-112">If you need instructions, see [Moving data tooand from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-hello-data-into-a-pandas-dataframe"></a><span data-ttu-id="0f50a-113">Pandas DataFrame içine hello veri yükleme</span><span class="sxs-lookup"><span data-stu-id="0f50a-113">Load hello data into a Pandas DataFrame</span></span>
<span data-ttu-id="0f50a-114">tooexplore ve bir veri kümesini değiştirmek, ardından bir Pandas DataFrame yüklenen hello blob kaynak tooa yerel dosya, ilk indirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="0f50a-114">tooexplore and manipulate a dataset, it must first be downloaded from hello blob source tooa local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="0f50a-115">Bu yordam için hello adımları toofollow şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0f50a-115">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="0f50a-116">Azure'dan Hello veri indirme blobu blob hizmeti kullanarak Python kodu örneği aşağıdaki hello ile.</span><span class="sxs-lookup"><span data-stu-id="0f50a-116">Download hello data from Azure blob with hello following Python code sample using blob service.</span></span> <span data-ttu-id="0f50a-117">Aşağıdaki kod, belirli değerleri içeren hello Hello değişkeninde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="0f50a-117">Replace hello variable in hello following code with your specific values:</span></span> 
   
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
2. <span data-ttu-id="0f50a-118">Bir Pandas verileri-çerçevesinden hello içine hello veri okuma dosya indirilir.</span><span class="sxs-lookup"><span data-stu-id="0f50a-118">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="0f50a-119">Şimdi, hazır tooexplore hello verileri ve bu veri kümesi özellikleri oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f50a-119">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="0f50a-120"><a name="blob-dataexploration"></a>Veri keşfi Pandas kullanma örnekleri</span><span class="sxs-lookup"><span data-stu-id="0f50a-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="0f50a-121">Pandas kullanarak tooexplore veri yolları bazı örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0f50a-121">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="0f50a-122">Merhaba incelemek **satır ve sütunların sayısı**</span><span class="sxs-lookup"><span data-stu-id="0f50a-122">Inspect hello **number of rows and columns**</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="0f50a-123">**İnceleme** ilk veya son birkaç hello **satırları** dataset aşağıdaki hello içinde:</span><span class="sxs-lookup"><span data-stu-id="0f50a-123">**Inspect** hello first or last few **rows** in hello following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="0f50a-124">Merhaba denetleyin **veri türü** her sütun örnek kod aşağıdaki hello kullanarak olarak içeri aktarıldı</span><span class="sxs-lookup"><span data-stu-id="0f50a-124">Check hello **data type** each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="0f50a-125">Merhaba denetleyin **temel istatistikleri** hello sütunlar gibi veri kümesi hello için</span><span class="sxs-lookup"><span data-stu-id="0f50a-125">Check hello **basic stats** for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="0f50a-126">Her bir sütunun değeri girişlerinde hello sayısı gibi bakın</span><span class="sxs-lookup"><span data-stu-id="0f50a-126">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="0f50a-127">**Eksik değerleri saymak** hello gerçek sayısı örnek kod aşağıdaki hello kullanarak her bir sütunun giriş karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="0f50a-127">**Count missing values** versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="0f50a-128">Varsa **eksik değerleri** için belirli bir sütun hello verilerdeki, bunları aşağıdaki gibi düşürebilir:</span><span class="sxs-lookup"><span data-stu-id="0f50a-128">If you have **missing values** for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="0f50a-129">dataframe_blobdata_noNA dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape =</span><span class="sxs-lookup"><span data-stu-id="0f50a-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="0f50a-130">Başka bir şekilde tooreplace eksik değerleri hello modu işleviyle şöyledir:</span><span class="sxs-lookup"><span data-stu-id="0f50a-130">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="0f50a-131">dataframe_blobdata_mode dataframe_blobdata.fillna = ({< column_name >: dataframe_blobdata ['< column_name >'] .mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="0f50a-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="0f50a-132">Oluşturma bir **histogram** depo tooplot hello dağıtım değişkenin değişken sayıda kullanarak Çiz</span><span class="sxs-lookup"><span data-stu-id="0f50a-132">Create a **histogram** plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="0f50a-133">Bakmak **bağıntıları** bir scatterplot veya hello yerleşik bağıntı işlevi kullanarak değişkenleri arasında</span><span class="sxs-lookup"><span data-stu-id="0f50a-133">Look at **correlations** between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

