---
title: "Pandas ile Azure blob storage keşfedin | Microsoft Docs"
description: "Pandas kullanarak Azure blob kapsayıcısında depolanan verileri araştırmak nasıl."
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
ms.openlocfilehash: e1b33b17270122a38228484a56c8324c5b4505a0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a><span data-ttu-id="1a9e7-103">Panda ile Azure blob depolama verilerini keşfedin</span><span class="sxs-lookup"><span data-stu-id="1a9e7-103">Explore data in Azure blob storage with Pandas</span></span>
<span data-ttu-id="1a9e7-104">Bu belge, Azure blob kapsayıcısını kullanarak depolanan verileri araştırmak alınmaktadır [Pandas](http://pandas.pydata.org/) Python paket.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-104">This document covers how to explore data that is stored in Azure blob container using [Pandas](http://pandas.pydata.org/) Python package.</span></span>

<span data-ttu-id="1a9e7-105">Aşağıdaki **menü** araçları çeşitli depolama ortamlarından verileri araştırmak için nasıl kullanılacağını açıklayan konulara bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-105">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="1a9e7-106">Bu görev bir adımdır [veri bilimi işlemi]().</span><span class="sxs-lookup"><span data-stu-id="1a9e7-106">This task is a step in the [Data Science Process]().</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a><span data-ttu-id="1a9e7-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1a9e7-107">Prerequisites</span></span>
<span data-ttu-id="1a9e7-108">Bu makalede, sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="1a9e7-108">This article assumes that you have:</span></span>

* <span data-ttu-id="1a9e7-109">Bir Azure depolama hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-109">Created an Azure storage account.</span></span> <span data-ttu-id="1a9e7-110">Yönergeler gerekiyorsa bkz [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="1a9e7-110">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="1a9e7-111">Verilerinizi bir Azure blob depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-111">Stored your data in an Azure blob storage account.</span></span> <span data-ttu-id="1a9e7-112">Yönergeler gerekiyorsa bkz [için ve Azure Storage veri taşıma](../storage/common/storage-moving-data.md)</span><span class="sxs-lookup"><span data-stu-id="1a9e7-112">If you need instructions, see [Moving data to and from Azure Storage](../storage/common/storage-moving-data.md)</span></span>

## <a name="load-the-data-into-a-pandas-dataframe"></a><span data-ttu-id="1a9e7-113">Pandas DataFrame veri yükleme</span><span class="sxs-lookup"><span data-stu-id="1a9e7-113">Load the data into a Pandas DataFrame</span></span>
<span data-ttu-id="1a9e7-114">Keşfetmek ve bir veri kümesini değiştirmek için önce blob kaynağından bir Pandas DataFrame yüklenebilir yerel bir dosyaya yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-114">To explore and manipulate a dataset, it must first be downloaded from the blob source to a local file, which can then be loaded in a Pandas DataFrame.</span></span> <span data-ttu-id="1a9e7-115">Bu yordam için izlemeniz gereken adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1a9e7-115">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="1a9e7-116">Verileri Azure blob'tan blob hizmeti kullanarak aşağıdaki Python kodu örneği ile indirme.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-116">Download the data from Azure blob with the following Python code sample using blob service.</span></span> <span data-ttu-id="1a9e7-117">Aşağıdaki kodda değişkeni belirli değerleriniz ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1a9e7-117">Replace the variable in the following code with your specific values:</span></span> 
   
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
        print(("It takes %s seconds to download "+blobname) % (t2 - t1))
2. <span data-ttu-id="1a9e7-118">İndirilen Dosya Pandas verileri-çerçeve içine verilerini okur.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-118">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="1a9e7-119">Şimdi verileri araştırmak ve bu veri kümesi özellikleri oluşturmak hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="1a9e7-119">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="1a9e7-120"><a name="blob-dataexploration"></a>Veri keşfi Pandas kullanma örnekleri</span><span class="sxs-lookup"><span data-stu-id="1a9e7-120"><a name="blob-dataexploration"></a>Examples of data exploration using Pandas</span></span>
<span data-ttu-id="1a9e7-121">Pandas kullanarak verileri araştırmak için yollar bazı örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1a9e7-121">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="1a9e7-122">İnceleme **satır ve sütunların sayısı**</span><span class="sxs-lookup"><span data-stu-id="1a9e7-122">Inspect the **number of rows and columns**</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="1a9e7-123">**İnceleme** ilk veya son birkaç **satırları** aşağıdaki kümesindeki:</span><span class="sxs-lookup"><span data-stu-id="1a9e7-123">**Inspect** the first or last few **rows** in the following dataset:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="1a9e7-124">Denetleme **veri türü** her sütun, aşağıdaki örnek kod kullanarak olarak içeri aktarıldı</span><span class="sxs-lookup"><span data-stu-id="1a9e7-124">Check the **data type** each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="1a9e7-125">Denetleme **temel istatistikleri** için aşağıdaki gibi ayarlayın veri sütunları</span><span class="sxs-lookup"><span data-stu-id="1a9e7-125">Check the **basic stats** for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="1a9e7-126">Her bir sütunun değeri için girdi sayısı gibi bakın</span><span class="sxs-lookup"><span data-stu-id="1a9e7-126">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="1a9e7-127">**Eksik değerleri saymak** gerçek sayısı aşağıdaki örnek kod kullanarak her bir sütunun giriş karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="1a9e7-127">**Count missing values** versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="1a9e7-128">Varsa **eksik değerleri** verileri belirli bir sütun için bunları aşağıdaki gibi bıraktığınız:</span><span class="sxs-lookup"><span data-stu-id="1a9e7-128">If you have **missing values** for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="1a9e7-129">dataframe_blobdata_noNA dataframe_blobdata.dropna() dataframe_blobdata_noNA.shape =</span><span class="sxs-lookup"><span data-stu-id="1a9e7-129">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="1a9e7-130">Eksik değerleri değiştirmek için başka bir yol ile modu işlevi şu şekildedir:</span><span class="sxs-lookup"><span data-stu-id="1a9e7-130">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="1a9e7-131">dataframe_blobdata_mode dataframe_blobdata.fillna = ({< column_name >: dataframe_blobdata ['< column_name >'] .mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="1a9e7-131">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="1a9e7-132">Oluşturma bir **histogram** bir değişken dağıtımını çizmek için depo değişken sayıda kullanarak çizim</span><span class="sxs-lookup"><span data-stu-id="1a9e7-132">Create a **histogram** plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="1a9e7-133">Bakmak **bağıntıları** bir scatterplot veya yerleşik bağıntı işlevi kullanarak değişkenleri arasında</span><span class="sxs-lookup"><span data-stu-id="1a9e7-133">Look at **correlations** between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

