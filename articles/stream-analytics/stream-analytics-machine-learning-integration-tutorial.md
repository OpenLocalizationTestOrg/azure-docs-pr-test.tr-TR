---
title: "aaaAzure akış analizi ve makine öğrenme tümleştirme | Microsoft Docs"
description: "Nasıl toouse bir kullanıcı tanımlı işlev ve Machine Learning Stream Analytics işi"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="96a6e-103">Azure akış analizi ve Azure Machine Learning kullanarak düşünceleri analiz gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="96a6e-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="96a6e-104">Bu makalede, Azure Machine Learning tümleştiren basit bir Azure akış analizi işi tooquickly nasıl ayarlamak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="96a6e-104">This article describes how tooquickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="96a6e-105">Gerçek zamanlı hello düşünceleri puan belirlemek ve hello metin veri akışı Cortana Intelligence Galerisi tooanalyze Machine Learning düşünceleri analytics modelden kullanın.</span><span class="sxs-lookup"><span data-stu-id="96a6e-105">You use a Machine Learning sentiment analytics model from hello Cortana Intelligence Gallery tooanalyze streaming text data and determine hello sentiment score in real time.</span></span> <span data-ttu-id="96a6e-106">Merhaba Cortana Intelligence Suite kullanarak düşünceleri analiz modeli oluşturmanın hello ayrıntılı olarak incelenmektedir hakkında endişelenmeden bu görevi gerçekleştirirken olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="96a6e-106">Using hello Cortana Intelligence Suite lets you accomplish this task without worrying about hello intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="96a6e-107">Bu makale tooscenarios bunlar gibi gelen öğrenin uygulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="96a6e-107">You can apply what you learn from this article tooscenarios such as these:</span></span>

* <span data-ttu-id="96a6e-108">Twitter veri akışı üzerinde gerçek zamanlı düşünceleri çözümleniyor.</span><span class="sxs-lookup"><span data-stu-id="96a6e-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="96a6e-109">Müşteri kayıtlarını çözümleme destek personeli ile sohbetleri.</span><span class="sxs-lookup"><span data-stu-id="96a6e-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="96a6e-110">Forum, bloglar ve videolar açıklamaları değerlendiriliyor.</span><span class="sxs-lookup"><span data-stu-id="96a6e-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="96a6e-111">Birçok diğer gerçek zamanlı, Tahmine dayalı Puanlama senaryoları.</span><span class="sxs-lookup"><span data-stu-id="96a6e-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="96a6e-112">Gerçek dünya senaryoda hello verileri doğrudan bir Twitter veri akışından alın.</span><span class="sxs-lookup"><span data-stu-id="96a6e-112">In a real-world scenario, you would get hello data directly from a Twitter data stream.</span></span> <span data-ttu-id="96a6e-113">Böylece Hello akış analizi işi tweet'leri Azure Blob Depolama alanında bir CSV dosyasından alır toosimplify hello öğretici, biz yazdıktan.</span><span class="sxs-lookup"><span data-stu-id="96a6e-113">toosimplify hello tutorial, we've written it so that hello Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="96a6e-114">Kendi CSV dosyası oluşturabilirsiniz veya görüntü aşağıdaki hello gösterildiği örnek bir CSV dosyası kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="96a6e-114">You can create your own CSV file, or you can use a sample CSV file, as shown in hello following image:</span></span>

![bir CSV dosyasında örnek tweet'leri](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="96a6e-116">oluşturduğunuz hello akış analizi işi hello düşünceleri analiz modeli kullanıcı tanımlı işlevi (UDF) hello blob Mağazası'ndan hello örnek metin verilere uygular.</span><span class="sxs-lookup"><span data-stu-id="96a6e-116">hello Streaming Analytics job that you create applies hello sentiment analytics model as a user-defined function (UDF) on hello sample text data from hello blob store.</span></span> <span data-ttu-id="96a6e-117">Merhaba çıkış (Merhaba düşünceleri analiz sonucunu hello) toohello yazılmış aynı blob Mağazası'nda farklı bir CSV dosyası.</span><span class="sxs-lookup"><span data-stu-id="96a6e-117">hello output (hello result of hello sentiment analysis) is written toohello same blob store in a different CSV file.</span></span> 

<span data-ttu-id="96a6e-118">Merhaba aşağıdaki şekilde bu yapılandırma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="96a6e-118">hello following figure demonstrates this configuration.</span></span> <span data-ttu-id="96a6e-119">Belirtilenler daha gerçekçi bir senaryo için blob depolama Twitter verilerini Azure Event Hubs'a giriş akış ile değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96a6e-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="96a6e-120">Ayrıca, oluşturacağınız bir [Microsoft Power BI](https://powerbi.microsoft.com/) gerçek zamanlı görsel olarak hello toplama düşünceleri.</span><span class="sxs-lookup"><span data-stu-id="96a6e-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of hello aggregate sentiment.</span></span>    

![Stream Analytics Machine Learning tümleştirmesine genel bakış](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="96a6e-122">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="96a6e-122">Prerequisites</span></span>
<span data-ttu-id="96a6e-123">Başlamadan önce hello aşağıdaki sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="96a6e-123">Before you start, make sure you have hello following:</span></span>

* <span data-ttu-id="96a6e-124">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="96a6e-124">An active Azure subscription.</span></span>
* <span data-ttu-id="96a6e-125">Bazı veriler içeren bir CSV dosyası.</span><span class="sxs-lookup"><span data-stu-id="96a6e-125">A CSV file with some data in it.</span></span> <span data-ttu-id="96a6e-126">Öğesinden daha önce gösterilen hello dosyayı indirebilirsiniz [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), ya da kendi dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96a6e-126">You can download hello file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="96a6e-127">Bu makale için GitHub hello dosyasından kullandığınız varsayalım.</span><span class="sxs-lookup"><span data-stu-id="96a6e-127">For this article, we assume that you're using hello file from GitHub.</span></span>

<span data-ttu-id="96a6e-128">Yüksek düzeyde, bu makalede, toocomplete hello görevleri gösterilen, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="96a6e-128">At a high level, toocomplete hello tasks demonstrated in this article, you do hello following:</span></span>

1. <span data-ttu-id="96a6e-129">Bir Azure depolama hesabı ve blob depolama kapsayıcısını oluşturun ve CSV biçimlendirilmiş giriş dosyası toohello kapsayıcı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="96a6e-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file toohello container.</span></span>
3. <span data-ttu-id="96a6e-130">Hello Cortana Intelligence Galerisi tooyour Azure Machine Learning çalışma alanından düşünceleri analiz modeli ekleyin ve bu model hello Machine Learning çalışma alanında bir web hizmeti olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96a6e-130">Add a sentiment analytics model from hello Cortana Intelligence Gallery tooyour Azure Machine Learning workspace and deploy this model as a web service in hello Machine Learning workspace.</span></span>
5. <span data-ttu-id="96a6e-131">Bu web hizmeti olarak sipariş toodetermine düşünceleri işlevinde hello metin girişi için çağıran Stream Analytics işi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96a6e-131">Create a Stream Analytics job that calls this web service as a function in order toodetermine sentiment for hello text input.</span></span>
6. <span data-ttu-id="96a6e-132">Merhaba Stream Analytics işini başlatmak ve hello çıktısını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="96a6e-132">Start hello Stream Analytics job and check hello output.</span></span>

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a><span data-ttu-id="96a6e-133">Depolama kapsayıcısı oluşturmak ve hello CSV giriş dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="96a6e-133">Create a storage container and upload hello CSV input file</span></span>
<span data-ttu-id="96a6e-134">Bu adım için Github'da kullanılabilir bir hello gibi herhangi bir CSV dosyası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96a6e-134">For this step, you can use any CSV file, such as hello one available from GitHub.</span></span>

1. <span data-ttu-id="96a6e-135">Hello Azure portal'ı tıklatın **yeni** &gt; **depolama** &gt; **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-135">In hello Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![Yeni depolama hesabı oluştur](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="96a6e-137">Bir ad sağlayın (`samldemo` hello örnekte).</span><span class="sxs-lookup"><span data-stu-id="96a6e-137">Provide a name (`samldemo` in hello example).</span></span> <span data-ttu-id="96a6e-138">Merhaba adı yalnızca küçük harfler ve sayılar kullanabilirsiniz ve Azure arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="96a6e-138">hello name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="96a6e-139">Varolan bir kaynak grubu belirtin ve bir konum belirtin.</span><span class="sxs-lookup"><span data-stu-id="96a6e-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="96a6e-140">Konum için Bu öğretici kullanımda oluşturulan tüm hello kaynaklar aynı hello olan öneririz konumu.</span><span class="sxs-lookup"><span data-stu-id="96a6e-140">For location, we recommend that all hello resources created in this tutorial use hello same location.</span></span>

    ![Depolama hesabı ayrıntılarını sağlayın](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="96a6e-142">Hello Azure portal, hello depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="96a6e-142">In hello Azure portal, select hello storage account.</span></span> <span data-ttu-id="96a6e-143">Merhaba depolama hesabı dikey penceresinde tıklayın **kapsayıcıları** ve ardından  **+ &nbsp;kapsayıcı** toocreate blob depolama.</span><span class="sxs-lookup"><span data-stu-id="96a6e-143">In hello storage account blade, click **Containers** and then click **+&nbsp;Container** toocreate blob storage.</span></span>

    ![BLOB kapsayıcı oluşturun](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="96a6e-145">Merhaba kapsayıcı için bir ad (`azuresamldemoblob` hello örnekte) doğrulayın **erişim türüne** çok ayarlanır**Blob**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-145">Provide a name for hello container (`azuresamldemoblob` in hello example) and verify that **Access type** is set too**Blob**.</span></span> <span data-ttu-id="96a6e-146">İşiniz bittiğinde, **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="96a6e-146">When you're done, click **OK**.</span></span>

    ![BLOB kapsayıcı ayrıntıları belirtin](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="96a6e-148">Merhaba, **kapsayıcıları** dikey penceresinde, bu kapsayıcı için hello dikey pencere açılır select hello yeni kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="96a6e-148">In hello **Containers** blade, select hello new container, which opens hello blade for that container.</span></span>

7. <span data-ttu-id="96a6e-149">**Karşıya Yükle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="96a6e-149">Click **Upload**.</span></span>

    ![Bir kapsayıcı 'Karşıya' düğmesi](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="96a6e-151">Merhaba, **karşıya yükleme blob** dikey penceresinde hello CSV dosyası Bu öğretici için toouse istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="96a6e-151">In hello **Upload blob** blade, specify hello CSV file that you want toouse for this tutorial.</span></span> <span data-ttu-id="96a6e-152">İçin **Blob türü**seçin **blok blobu** ve kümesi hello blok Bu öğretici için yeterliyse too4 MB cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="96a6e-152">For **Blob type**, select **Block blob** and set hello block size too4 MB, which is sufficient for this tutorial.</span></span>

    ![BLOB dosya karşıya yükleme](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="96a6e-154">Merhaba tıklatın **karşıya** hello dikey penceresinde hello sonundaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="96a6e-154">Click hello **Upload** button at hello bottom of hello blade.</span></span>

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a><span data-ttu-id="96a6e-155">Cortana Intelligence Galerisi hello Hello düşünceleri analiz modeli ekleme</span><span class="sxs-lookup"><span data-stu-id="96a6e-155">Add hello sentiment analytics model from hello Cortana Intelligence Gallery</span></span>

<span data-ttu-id="96a6e-156">Bir blob'a Hello örnek veriler değil, hello düşünceleri çözümleme modeli Cortana Intelligence Galerisi'nde etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96a6e-156">Now that hello sample data is in a blob, you can enable hello sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="96a6e-157">Toohello Git [Tahmine dayalı düşünceleri analiz modeli](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) hello Cortana Intelligence Galerisi sayfasında.</span><span class="sxs-lookup"><span data-stu-id="96a6e-157">Go toohello [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in hello Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="96a6e-158">Tıklatın **Studio'da Aç**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-158">Click **Open in Studio**.</span></span>  
   
   ![Stream Analytics Machine Learning, açık Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="96a6e-160">Toogo toohello çalışma alanını açın.</span><span class="sxs-lookup"><span data-stu-id="96a6e-160">Sign in toogo toohello workspace.</span></span> <span data-ttu-id="96a6e-161">Bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="96a6e-161">Select a location.</span></span>

4. <span data-ttu-id="96a6e-162">Tıklatın **çalıştırmak** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="96a6e-162">Click **Run** at hello bottom of hello page.</span></span> <span data-ttu-id="96a6e-163">Merhaba işlem çalışır ve hangi yaklaşık bir dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="96a6e-163">hello process runs, which takes about a minute.</span></span>

   ![denemeyi Machine Learning Studio'da çalıştırın](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="96a6e-165">Merhaba işlem başarıyla çalıştırıldıktan sonra seçin **Web hizmeti Dağıt** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="96a6e-165">After hello process has run successfully, select **Deploy Web Service** at hello bottom of hello page.</span></span>

   ![denemeyi Machine Learning Studio'da bir web hizmeti olarak dağıtma](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="96a6e-167">analytics modeldir hazır toouse düşünceleri hello toovalidate tıklatın hello **Test** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="96a6e-167">toovalidate that hello sentiment analytics model is ready toouse, click hello **Test** button.</span></span> <span data-ttu-id="96a6e-168">Metin "ı Microsoft memnuniyet"gibi giriş sağlar.</span><span class="sxs-lookup"><span data-stu-id="96a6e-168">Provide text input such as "I love Microsoft".</span></span> 

   ![Machine Learning Studio'da Test deneme](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="96a6e-170">Merhaba test çalışırsa, örnek izleyen bir sonuç benzer toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="96a6e-170">If hello test works, you see a result similar toohello following example:</span></span>

   ![Machine Learning Studio'da test sonuçları](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="96a6e-172">Merhaba, **uygulamaları** sütun hello tıklatın **Excel 2010 veya önceki çalışma kitabı** bağlantı toodownload bir Excel çalışma kitabı.</span><span class="sxs-lookup"><span data-stu-id="96a6e-172">In hello **Apps** column, click hello **Excel 2010 or earlier workbook** link toodownload an Excel workbook.</span></span> <span data-ttu-id="96a6e-173">Merhaba çalışma kitabı hello bir API anahtarı ve hello Stream Analytics işi daha sonra tooset gerektiğini hello URL içerir.</span><span class="sxs-lookup"><span data-stu-id="96a6e-173">hello workbook contains hello an API key and hello URL that you need later tooset up hello Stream Analytics job.</span></span>

    ![Stream Analytics Machine Learning, Hızlı Bakış](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a><span data-ttu-id="96a6e-175">Merhaba Machine Learning modelini kullanan bir Stream Analytics işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="96a6e-175">Create a Stream Analytics job that uses hello Machine Learning model</span></span>

<span data-ttu-id="96a6e-176">Artık blob storage'da hello CSV dosyasından hello örnek tweet'leri okuyan akış analizi işi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96a6e-176">You can now create a Stream Analytics job that reads hello sample tweets from hello CSV file in blob storage.</span></span> 

### <a name="create-hello-job"></a><span data-ttu-id="96a6e-177">Merhaba işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="96a6e-177">Create hello job</span></span>

1. <span data-ttu-id="96a6e-178">Toohello Git [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="96a6e-178">Go toohello [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="96a6e-179">Tıklatın **yeni** > **nesnelerin interneti** > **Stream Analytics işi**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![Tooa yeni akış analizi işi almak için azure portal yolu](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="96a6e-181">Ad hello iş `azure-sa-ml-demo`bir abonelik belirtin, varolan bir kaynak grubu belirtin veya yeni bir tane oluşturun ve hello işi için başlangıç konumu seçin.</span><span class="sxs-lookup"><span data-stu-id="96a6e-181">Name hello job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select hello location for hello job.</span></span>

   ![Yeni akış analizi işi için ayarları belirtin](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a><span data-ttu-id="96a6e-183">Merhaba iş giriş yapılandırın</span><span class="sxs-lookup"><span data-stu-id="96a6e-183">Configure hello job input</span></span>
<span data-ttu-id="96a6e-184">Merhaba iş kendi giriş önceki tooblob depolama karşıya hello CSV dosyasından alır.</span><span class="sxs-lookup"><span data-stu-id="96a6e-184">hello job gets its input from hello CSV file that you uploaded earlier tooblob storage.</span></span>

1. <span data-ttu-id="96a6e-185">Merhaba işi, altında oluşturulduktan sonra **iş topoloji** hello iş dikey penceresinde hello tıklayın **girişleri** kutusu.</span><span class="sxs-lookup"><span data-stu-id="96a6e-185">After hello job has been created, under **Job Topology** in hello job blade, click hello **Inputs** box.</span></span>  
   
   ![Akış analizi işi dikey penceresinde 'Girişleri' kutusu](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="96a6e-187">Merhaba, **girişleri** dikey penceresinde tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-187">In hello **Inputs** blade, click **+ Add**.</span></span>

   !['Bir giriş toohello Stream Analytics işi ekleme düğmesi ekleme'](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="96a6e-189">Merhaba dolgu **yeni giriş** dikey penceresinde bu değerleri içeren:</span><span class="sxs-lookup"><span data-stu-id="96a6e-189">Fill out hello **New input** blade with these values:</span></span>

    * <span data-ttu-id="96a6e-190">**Giriş diğer adı**: hello adını kullan `datainput`.</span><span class="sxs-lookup"><span data-stu-id="96a6e-190">**Input alias**: Use hello name `datainput`.</span></span>
    * <span data-ttu-id="96a6e-191">**Kaynak türünü**: seçin **veri akışı**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="96a6e-192">**Kaynak**: seçin **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="96a6e-193">**Alma seçeneği**: seçin **blob storage'ı geçerli aboneliğe ilişkin kullanma**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="96a6e-194">**Depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-194">**Storage account**.</span></span> <span data-ttu-id="96a6e-195">Daha önce oluşturduğunuz hello depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="96a6e-195">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="96a6e-196">**Kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-196">**Container**.</span></span> <span data-ttu-id="96a6e-197">Daha önce oluşturduğunuz select hello kapsayıcı (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="96a6e-197">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="96a6e-198">**Olayı seri hale getirme biçimi**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-198">**Event serialization format**.</span></span> <span data-ttu-id="96a6e-199">Seçin **CSV**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-199">Select **CSV**.</span></span>

    ![Yeni iş girişi için ayarlar](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="96a6e-201">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="96a6e-201">Click **Create**.</span></span>

### <a name="configure-hello-job-output"></a><span data-ttu-id="96a6e-202">Merhaba iş çıktısı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="96a6e-202">Configure hello job output</span></span>
<span data-ttu-id="96a6e-203">Merhaba işi gönderir sonuçları toohello aynı blob depolama burada giriş.</span><span class="sxs-lookup"><span data-stu-id="96a6e-203">hello job sends results toohello same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="96a6e-204">Altında **iş topoloji** hello iş dikey penceresinde hello tıklayın **çıkışları** kutusu.</span><span class="sxs-lookup"><span data-stu-id="96a6e-204">Under **Job Topology** in hello job blade, click hello **Outputs** box.</span></span>  
  
   ![Akış analizi işi için yeni çıkış oluşturma](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="96a6e-206">Merhaba, **çıkışları** dikey penceresinde tıklatın **+ Ekle**ve hello diğer ada sahip bir çıkış ekleyin `datamloutput`.</span><span class="sxs-lookup"><span data-stu-id="96a6e-206">In hello **Outputs** blade, click **+ Add**, and then add an output with hello alias `datamloutput`.</span></span> 

3. <span data-ttu-id="96a6e-207">İçin **havuzu**seçin **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="96a6e-208">Merhaba hello kalanını doldurun hello blob depolama girdisi için kullandığınız aynı değerleri kullanarak ayarlarını hello çıktı:</span><span class="sxs-lookup"><span data-stu-id="96a6e-208">Then fill in hello rest of hello output settings using hello same values that you used for hello blob storage for input:</span></span>

    * <span data-ttu-id="96a6e-209">**Depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-209">**Storage account**.</span></span> <span data-ttu-id="96a6e-210">Daha önce oluşturduğunuz hello depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="96a6e-210">Select hello storage account you created earlier.</span></span>
    * <span data-ttu-id="96a6e-211">**Kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-211">**Container**.</span></span> <span data-ttu-id="96a6e-212">Daha önce oluşturduğunuz select hello kapsayıcı (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="96a6e-212">Select hello container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="96a6e-213">**Olayı seri hale getirme biçimi**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-213">**Event serialization format**.</span></span> <span data-ttu-id="96a6e-214">Seçin **CSV**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-214">Select **CSV**.</span></span>

   ![Yeni iş çıktısı için ayarları](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="96a6e-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="96a6e-216">Click **Create**.</span></span>   


### <a name="add-hello-machine-learning-function"></a><span data-ttu-id="96a6e-217">Add Hello Machine Learning işlevi</span><span class="sxs-lookup"><span data-stu-id="96a6e-217">Add hello Machine Learning function</span></span> 
<span data-ttu-id="96a6e-218">Daha önce bir Machine Learning modeli tooa web hizmeti yayımladı.</span><span class="sxs-lookup"><span data-stu-id="96a6e-218">Earlier you published a Machine Learning model tooa web service.</span></span> <span data-ttu-id="96a6e-219">Merhaba akış analizi işi çalıştırıldığında Senaryomuzda her örnek tweet hello giriş toohello web hizmetinden düşünceleri çözümleme için gönderir.</span><span class="sxs-lookup"><span data-stu-id="96a6e-219">In our scenario, when hello Stream Analysis job runs, it sends each sample tweet from hello input toohello web service for sentiment analysis.</span></span> <span data-ttu-id="96a6e-220">Merhaba Machine Learning web hizmeti bir düşünceleri döndürür (`positive`, `neutral`, veya `negative`) ve hello tweet pozitif olması olasılığını.</span><span class="sxs-lookup"><span data-stu-id="96a6e-220">hello Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of hello tweet being positive.</span></span> 

<span data-ttu-id="96a6e-221">Merhaba öğreticinin bu bölümünde hello akış analizi işi işlevinde tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="96a6e-221">In this section of hello tutorial, you define a function in hello Stream Analysis job.</span></span> <span data-ttu-id="96a6e-222">Merhaba işlevi bir tweet toohello web hizmeti çağrılan toosend olması ve hello yanıt geri alın.</span><span class="sxs-lookup"><span data-stu-id="96a6e-222">hello function can be invoked toosend a tweet toohello web service and get hello response back.</span></span> 

1. <span data-ttu-id="96a6e-223">Daha önce hello Excel çalışma kitabında indirdiğiniz hello web hizmeti URL'sini ve API anahtarını olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="96a6e-223">Make sure you have hello web service URL and API key that you downloaded earlier in hello Excel workbook.</span></span>

2. <span data-ttu-id="96a6e-224">Toohello iş genel bakış dikey penceresine dönün.</span><span class="sxs-lookup"><span data-stu-id="96a6e-224">Return toohello job overview blade.</span></span>

3. <span data-ttu-id="96a6e-225">Altında **ayarları**seçin **işlevleri** ve ardından **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![Bir işlev toohello Stream Analytics işi ekleme](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="96a6e-227">Girin `sentiment` hello işlev alias ve bu değerleri kullanarak hello dikey penceresinde hello kalan doldurun:</span><span class="sxs-lookup"><span data-stu-id="96a6e-227">Enter `sentiment` as hello function alias and fill out hello rest of hello blade using these values:</span></span>

    * <span data-ttu-id="96a6e-228">**İşlev türü**: seçin **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="96a6e-229">**Alma seçeneği**: seçin **farklı bir abonelik alma**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="96a6e-230">Bu, bir fırsat tooenter hello URL'si ve anahtar sağlar.</span><span class="sxs-lookup"><span data-stu-id="96a6e-230">This gives you a chance tooenter hello URL and key.</span></span>
    * <span data-ttu-id="96a6e-231">**URL**: hello web hizmeti URL'sini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="96a6e-231">**URL**: Paste in hello web service URL.</span></span>
    * <span data-ttu-id="96a6e-232">**Anahtar**: hello API anahtarını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="96a6e-232">**Key**: Paste in hello API key.</span></span>
  
    ![Machine Learning işlevi toohello akış analizi işi eklemek için ayarlar](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="96a6e-234">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="96a6e-234">Click **Create**.</span></span>

### <a name="create-a-query-tootransform-hello-data"></a><span data-ttu-id="96a6e-235">Bir sorgu tootransform hello verileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="96a6e-235">Create a query tootransform hello data</span></span>

<span data-ttu-id="96a6e-236">Akış analizi sorgu bildirim temelli, SQL tabanlı tooexamine hello giriş kullanır ve işleme.</span><span class="sxs-lookup"><span data-stu-id="96a6e-236">Stream Analytics uses a declarative, SQL-based query tooexamine hello input and process it.</span></span> <span data-ttu-id="96a6e-237">Bu bölümde, her tweet girişten okuyan ve hello Machine Learning işlevi tooperform düşünceleri analiz çağıran bir sorgu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="96a6e-237">In this section, you create a query that reads each tweet from input and then invokes hello Machine Learning function tooperform sentiment analysis.</span></span> <span data-ttu-id="96a6e-238">Merhaba sorgu daha sonra hello sonuç toohello (blob depolama) tanımlanan çıkış gönderir.</span><span class="sxs-lookup"><span data-stu-id="96a6e-238">hello query then sends hello result toohello output that you defined (blob storage).</span></span>

1. <span data-ttu-id="96a6e-239">Toohello iş genel bakış dikey penceresine dönün.</span><span class="sxs-lookup"><span data-stu-id="96a6e-239">Return toohello job overview blade.</span></span>

2.  <span data-ttu-id="96a6e-240">Altında **iş topoloji**, hello tıklatın **sorgu** kutusu.</span><span class="sxs-lookup"><span data-stu-id="96a6e-240">Under **Job Topology**, click hello **Query** box.</span></span>

    ![Akış analizi işi için bir sorgu oluşturun](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="96a6e-242">Sorgu aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="96a6e-242">Enter hello following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="96a6e-243">Merhaba sorgu daha önce oluşturduğunuz hello işlevi çağırır (`sentiment`) sipariş tooperform düşünceleri analizi hello girişte her tweet üzerinde.</span><span class="sxs-lookup"><span data-stu-id="96a6e-243">hello query invokes hello function you created earlier (`sentiment`) in order tooperform sentiment analysis on each tweet in hello input.</span></span> 

4. <span data-ttu-id="96a6e-244">Tıklatın **kaydetmek** toosave hello sorgu.</span><span class="sxs-lookup"><span data-stu-id="96a6e-244">Click **Save** toosave hello query.</span></span>


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a><span data-ttu-id="96a6e-245">Merhaba Stream Analytics işini başlatmak ve hello çıktısını denetleyin</span><span class="sxs-lookup"><span data-stu-id="96a6e-245">Start hello Stream Analytics job and check hello output</span></span>

<span data-ttu-id="96a6e-246">Şimdi hello Stream Analytics işi başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96a6e-246">You can now start hello Stream Analytics job.</span></span>

### <a name="start-hello-job"></a><span data-ttu-id="96a6e-247">Merhaba işi Başlat</span><span class="sxs-lookup"><span data-stu-id="96a6e-247">Start hello job</span></span>
1. <span data-ttu-id="96a6e-248">Toohello iş genel bakış dikey penceresine dönün.</span><span class="sxs-lookup"><span data-stu-id="96a6e-248">Return toohello job overview blade.</span></span>

2. <span data-ttu-id="96a6e-249">Tıklatın **Başlat** hello dikey penceresinde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="96a6e-249">Click **Start** at hello top of hello blade.</span></span>

    ![Akış analizi işi için bir sorgu oluşturun](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="96a6e-251">Merhaba, **başlangıç işi**seçin **özel**ve ardından bir gün önceki toowhen hello CSV dosyası tooblob depolama karşıya seçin.</span><span class="sxs-lookup"><span data-stu-id="96a6e-251">In hello **Start job**, select **Custom**, and then select one day prior toowhen you uploaded hello CSV file tooblob storage.</span></span> <span data-ttu-id="96a6e-252">İşiniz bittiğinde tıklatın **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-252">When you're done, click **Start**.</span></span>  


### <a name="check-hello-output"></a><span data-ttu-id="96a6e-253">Merhaba çıktısını denetleyin</span><span class="sxs-lookup"><span data-stu-id="96a6e-253">Check hello output</span></span>
1. <span data-ttu-id="96a6e-254">Merhaba etkinliğinde görene kadar birkaç dakika let hello iş **izleme** kutusu.</span><span class="sxs-lookup"><span data-stu-id="96a6e-254">Let hello job run for a few minutes until you see activity in hello **Monitoring** box.</span></span> 

2. <span data-ttu-id="96a6e-255">Normalde tooexamine Merhaba içeriğine blob depolama kullanan bir aracı varsa, bu aracı tooexamine hello kullanın `azuresamldemoblob` kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="96a6e-255">If you have a tool that you normally use tooexamine hello contents of blob storage, use that tool tooexamine hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="96a6e-256">Alternatif olarak, aşağıdaki adımları hello Azure portal'ın hello:</span><span class="sxs-lookup"><span data-stu-id="96a6e-256">Alternatively, do hello following steps in hello Azure portal:</span></span>

    1. <span data-ttu-id="96a6e-257">Merhaba Hello Portalı'nda bulmak `samldemo` depolama hesabı ve hello hesabında hello bulur `azuresamldemoblob` kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="96a6e-257">In hello portal, find hello `samldemo` storage account, and within hello account, find hello `azuresamldemoblob` container.</span></span> <span data-ttu-id="96a6e-258">Merhaba kapsayıcısında iki dosya bkz: Merhaba hello örnek tweet'leri içeren dosya ve hello akış analizi işi tarafından oluşturulan bir CSV dosyası.</span><span class="sxs-lookup"><span data-stu-id="96a6e-258">You see two files in hello container: hello file that contains hello sample tweets and a CSV file generated by hello Stream Analytics job.</span></span>
    2. <span data-ttu-id="96a6e-259">Oluşturulan hello dosyasını sağ tıklatın ve ardından **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="96a6e-259">Right-click hello generated file and then select **Download**.</span></span> 

   ![Blob depolama alanından CSV iş çıktısı indirme](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="96a6e-261">Açık hello CSV dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="96a6e-261">Open hello generated CSV file.</span></span> <span data-ttu-id="96a6e-262">Aşağıdaki örneğine hello gibi bir şey görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="96a6e-262">You see something like hello following example:</span></span>  
   
   ![Stream Analytics Machine Learning, CSV görünümü](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="96a6e-264">Metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="96a6e-264">View metrics</span></span>
<span data-ttu-id="96a6e-265">Azure Machine Learning işlevi ödemeyle ilgili ölçümlerini de görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96a6e-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="96a6e-266">işlevi ile ilgili ölçümleri aşağıdaki hello hello görüntülenen **izleme** hello iş dikey penceresinde kutusunda:</span><span class="sxs-lookup"><span data-stu-id="96a6e-266">hello following function-related metrics are displayed in hello **Monitoring** box in hello job blade:</span></span>

* <span data-ttu-id="96a6e-267">**İşlev istekleri** gönderilen istekleri tooa Machine Learning web hizmeti hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="96a6e-267">**Function Requests** indicates hello number of requests sent tooa Machine Learning web service.</span></span>  
* <span data-ttu-id="96a6e-268">**İşlev olayları** hello olayları hello isteği sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="96a6e-268">**Function Events** indicates hello number of events in hello request.</span></span> <span data-ttu-id="96a6e-269">Varsayılan olarak, her isteği tooa Machine Learning web hizmeti too1, 000 olaylarını içerir.</span><span class="sxs-lookup"><span data-stu-id="96a6e-269">By default, each request tooa Machine Learning web service contains up too1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="96a6e-270">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="96a6e-270">Next steps</span></span>

* [<span data-ttu-id="96a6e-271">Giriş tooAzure akış analizi</span><span class="sxs-lookup"><span data-stu-id="96a6e-271">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="96a6e-272">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="96a6e-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="96a6e-273">REST API tümleştirme ve makine öğrenme</span><span class="sxs-lookup"><span data-stu-id="96a6e-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="96a6e-274">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="96a6e-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



