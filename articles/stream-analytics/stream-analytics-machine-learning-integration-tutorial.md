---
title: "Azure akış analizi ve makine öğrenme tümleştirme | Microsoft Docs"
description: "Bir kullanıcı tanımlı işlev ve Machine Learning Stream Analytics işinde kullanma"
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
ms.openlocfilehash: 023033d5479fcf0e2dff168b6604431eef283d3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a><span data-ttu-id="82eb2-103">Azure akış analizi ve Azure Machine Learning kullanarak düşünceleri analiz gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="82eb2-103">Performing sentiment analysis by using Azure Stream Analytics and Azure Machine Learning</span></span>
<span data-ttu-id="82eb2-104">Bu makalede, Azure Machine Learning tümleştiren basit bir Azure akış analizi işi hızlı bir şekilde ayarlamak açıklar.</span><span class="sxs-lookup"><span data-stu-id="82eb2-104">This article describes how to quickly set up a simple Azure Stream Analytics job that integrates Azure Machine Learning.</span></span> <span data-ttu-id="82eb2-105">Machine Learning düşünceleri analiz modeli Cortana Intelligence Galeriden akış metin verileri çözümlemek ve gerçek zamanlı düşünceleri puan belirlemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="82eb2-105">You use a Machine Learning sentiment analytics model from the Cortana Intelligence Gallery to analyze streaming text data and determine the sentiment score in real time.</span></span> <span data-ttu-id="82eb2-106">Cortana Intelligence Suite kullanarak düşünceleri analiz modeli oluşturmanın ayrıntılı olarak incelenmektedir hakkında endişelenmeden bu görevi gerçekleştirirken olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="82eb2-106">Using the Cortana Intelligence Suite lets you accomplish this task without worrying about the intricacies of building a sentiment analytics model.</span></span>

<span data-ttu-id="82eb2-107">Ne bunlar gibi senaryolar için bu makaleden öğrenin uygulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="82eb2-107">You can apply what you learn from this article to scenarios such as these:</span></span>

* <span data-ttu-id="82eb2-108">Twitter veri akışı üzerinde gerçek zamanlı düşünceleri çözümleniyor.</span><span class="sxs-lookup"><span data-stu-id="82eb2-108">Analyzing real-time sentiment on streaming Twitter data.</span></span>
* <span data-ttu-id="82eb2-109">Müşteri kayıtlarını çözümleme destek personeli ile sohbetleri.</span><span class="sxs-lookup"><span data-stu-id="82eb2-109">Analyzing records of customer chats with support staff.</span></span>
* <span data-ttu-id="82eb2-110">Forum, bloglar ve videolar açıklamaları değerlendiriliyor.</span><span class="sxs-lookup"><span data-stu-id="82eb2-110">Evaluating comments on forums, blogs, and videos.</span></span> 
* <span data-ttu-id="82eb2-111">Birçok diğer gerçek zamanlı, Tahmine dayalı Puanlama senaryoları.</span><span class="sxs-lookup"><span data-stu-id="82eb2-111">Many other real-time, predictive scoring scenarios.</span></span>

<span data-ttu-id="82eb2-112">Gerçek hayattaki bir senaryoda, doğrudan bir Twitter veri akışından veri almalıdır.</span><span class="sxs-lookup"><span data-stu-id="82eb2-112">In a real-world scenario, you would get the data directly from a Twitter data stream.</span></span> <span data-ttu-id="82eb2-113">Akış analizi işi, Azure Blob Depolama alanında bir CSV dosyasından tweet'leri alır. böylece biz yazılmış öğretici basitleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="82eb2-113">To simplify the tutorial, we've written it so that the Streaming Analytics job gets tweets from a CSV file in Azure Blob storage.</span></span> <span data-ttu-id="82eb2-114">Örnek bir CSV dosyası aşağıdaki görüntüde gösterildiği gibi kullanabilirsiniz veya kendi CSV dosyası oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="82eb2-114">You can create your own CSV file, or you can use a sample CSV file, as shown in the following image:</span></span>

![bir CSV dosyasında örnek tweet'leri](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

<span data-ttu-id="82eb2-116">Oluşturduğunuz akış analizi işi düşünceleri analiz modeli kullanıcı tanımlı işlevi (UDF) blob depolama alanından örnek metin verilere uygular.</span><span class="sxs-lookup"><span data-stu-id="82eb2-116">The Streaming Analytics job that you create applies the sentiment analytics model as a user-defined function (UDF) on the sample text data from the blob store.</span></span> <span data-ttu-id="82eb2-117">Çıktı (düşünceleri analiz sonucunu) aynı blob Mağazası'nda farklı bir CSV dosyası yazılır.</span><span class="sxs-lookup"><span data-stu-id="82eb2-117">The output (the result of the sentiment analysis) is written to the same blob store in a different CSV file.</span></span> 

<span data-ttu-id="82eb2-118">Aşağıdaki şekilde, bu yapılandırma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="82eb2-118">The following figure demonstrates this configuration.</span></span> <span data-ttu-id="82eb2-119">Belirtilenler daha gerçekçi bir senaryo için blob depolama Twitter verilerini Azure Event Hubs'a giriş akış ile değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82eb2-119">As noted, for a more realistic scenario, you can replace blob storage with streaming Twitter data from an Azure Event Hubs input.</span></span> <span data-ttu-id="82eb2-120">Ayrıca, oluşturacağınız bir [Microsoft Power BI](https://powerbi.microsoft.com/) gerçek zamanlı görsel olarak birleşik düşünceleri.</span><span class="sxs-lookup"><span data-stu-id="82eb2-120">Additionally, you could build a [Microsoft Power BI](https://powerbi.microsoft.com/) real-time visualization of the aggregate sentiment.</span></span>    

![Stream Analytics Machine Learning tümleştirmesine genel bakış](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a><span data-ttu-id="82eb2-122">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="82eb2-122">Prerequisites</span></span>
<span data-ttu-id="82eb2-123">Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="82eb2-123">Before you start, make sure you have the following:</span></span>

* <span data-ttu-id="82eb2-124">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="82eb2-124">An active Azure subscription.</span></span>
* <span data-ttu-id="82eb2-125">Bazı veriler içeren bir CSV dosyası.</span><span class="sxs-lookup"><span data-stu-id="82eb2-125">A CSV file with some data in it.</span></span> <span data-ttu-id="82eb2-126">Öğesinden daha önce gösterilen dosyayı indirebilirsiniz [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), ya da kendi dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82eb2-126">You can download the file shown earlier from [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), or you can create your own file.</span></span> <span data-ttu-id="82eb2-127">Bu makale için GitHub dosyasından kullandığınız varsayılmıştır.</span><span class="sxs-lookup"><span data-stu-id="82eb2-127">For this article, we assume that you're using the file from GitHub.</span></span>

<span data-ttu-id="82eb2-128">Yüksek düzeyde, bu makalede gösterilen görevleri tamamlamak için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="82eb2-128">At a high level, to complete the tasks demonstrated in this article, you do the following:</span></span>

1. <span data-ttu-id="82eb2-129">Bir Azure depolama hesabı ve blob depolama kapsayıcısını oluşturun ve CSV olarak biçimlendirilmiş bir giriş dosyası kapsayıcısına yükleyin.</span><span class="sxs-lookup"><span data-stu-id="82eb2-129">Create an Azure storage account and a blob storage container, and upload a CSV-formatted input file to the container.</span></span>
3. <span data-ttu-id="82eb2-130">Düşünceleri analiz modeli Cortana Intelligence Galeriden Azure Machine Learning çalışma alanına eklemek ve bu model Machine Learning çalışma alanında bir web hizmeti olarak dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82eb2-130">Add a sentiment analytics model from the Cortana Intelligence Gallery to your Azure Machine Learning workspace and deploy this model as a web service in the Machine Learning workspace.</span></span>
5. <span data-ttu-id="82eb2-131">Metin girişi için düşünceleri belirlemek için bir işlevi olarak bu web hizmeti çağrıları Stream Analytics işi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82eb2-131">Create a Stream Analytics job that calls this web service as a function in order to determine sentiment for the text input.</span></span>
6. <span data-ttu-id="82eb2-132">Stream Analytics işini başlatmak ve çıktısını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="82eb2-132">Start the Stream Analytics job and check the output.</span></span>

## <a name="create-a-storage-container-and-upload-the-csv-input-file"></a><span data-ttu-id="82eb2-133">Depolama kapsayıcısı oluşturun ve CSV giriş dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="82eb2-133">Create a storage container and upload the CSV input file</span></span>
<span data-ttu-id="82eb2-134">Bu adım için Github'da kullanılabilir bir gibi herhangi bir CSV dosyası kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82eb2-134">For this step, you can use any CSV file, such as the one available from GitHub.</span></span>

1. <span data-ttu-id="82eb2-135">Azure portalında tıklatın **yeni** &gt; **depolama** &gt; **depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-135">In the Azure portal, click **New** &gt; **Storage** &gt; **Storage account**.</span></span>

   ![Yeni depolama hesabı oluştur](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. <span data-ttu-id="82eb2-137">Bir ad sağlayın (`samldemo` örnekte).</span><span class="sxs-lookup"><span data-stu-id="82eb2-137">Provide a name (`samldemo` in the example).</span></span> <span data-ttu-id="82eb2-138">Ad yalnızca küçük harfler ve sayılar kullanabilirsiniz ve Azure arasında benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="82eb2-138">The name can use only lowercase letters and numbers, and it must be unique across Azure.</span></span> 

3. <span data-ttu-id="82eb2-139">Varolan bir kaynak grubu belirtin ve bir konum belirtin.</span><span class="sxs-lookup"><span data-stu-id="82eb2-139">Specify an existing resource group and specify a location.</span></span> <span data-ttu-id="82eb2-140">Konum için Bu öğreticide oluşturduğunuz tüm kaynakların aynı konumu kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="82eb2-140">For location, we recommend that all the resources created in this tutorial use the same location.</span></span>

    ![Depolama hesabı ayrıntılarını sağlayın](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. <span data-ttu-id="82eb2-142">Azure Portal'da depolama hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="82eb2-142">In the Azure portal, select the storage account.</span></span> <span data-ttu-id="82eb2-143">Depolama hesabı dikey penceresinde tıklayın **kapsayıcıları** ve ardından  **+ &nbsp;kapsayıcı** blob depolama alanı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="82eb2-143">In the storage account blade, click **Containers** and then click **+&nbsp;Container** to create blob storage.</span></span>

    ![BLOB kapsayıcı oluşturun](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. <span data-ttu-id="82eb2-145">Kapsayıcı için bir ad (`azuresamldemoblob` örnekte) doğrulayın **erişim türüne** ayarlanır **Blob**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-145">Provide a name for the container (`azuresamldemoblob` in the example) and verify that **Access type** is set to **Blob**.</span></span> <span data-ttu-id="82eb2-146">İşiniz bittiğinde, **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="82eb2-146">When you're done, click **OK**.</span></span>

    ![BLOB kapsayıcı ayrıntıları belirtin](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. <span data-ttu-id="82eb2-148">İçinde **kapsayıcıları** dikey penceresinde, bu kapsayıcı için bir dikey pencere açılır yeni kapsayıcıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="82eb2-148">In the **Containers** blade, select the new container, which opens the blade for that container.</span></span>

7. <span data-ttu-id="82eb2-149">**Karşıya Yükle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="82eb2-149">Click **Upload**.</span></span>

    ![Bir kapsayıcı 'Karşıya' düğmesi](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. <span data-ttu-id="82eb2-151">İçinde **karşıya yükleme blob** dikey penceresinde, Bu öğretici için kullanmak istediğiniz CSV dosyasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="82eb2-151">In the **Upload blob** blade, specify the CSV file that you want to use for this tutorial.</span></span> <span data-ttu-id="82eb2-152">İçin **Blob türü**seçin **blok blobu** ve blok boyutu Bu öğretici için yeterliyse 4 MB olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="82eb2-152">For **Blob type**, select **Block blob** and set the block size to 4 MB, which is sufficient for this tutorial.</span></span>

    ![BLOB dosya karşıya yükleme](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. <span data-ttu-id="82eb2-154">Tıklatın **karşıya** dikey pencerenin altındaki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="82eb2-154">Click the **Upload** button at the bottom of the blade.</span></span>

## <a name="add-the-sentiment-analytics-model-from-the-cortana-intelligence-gallery"></a><span data-ttu-id="82eb2-155">Cortana Intelligence Galeriden düşünceleri analiz modeli ekleme</span><span class="sxs-lookup"><span data-stu-id="82eb2-155">Add the sentiment analytics model from the Cortana Intelligence Gallery</span></span>

<span data-ttu-id="82eb2-156">Örnek verileri bir blob'a olduğundan, Cortana Intelligence Galerisi düşünceleri analiz modelinde etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82eb2-156">Now that the sample data is in a blob, you can enable the sentiment analysis model in Cortana Intelligence Gallery.</span></span>

1. <span data-ttu-id="82eb2-157">Git [Tahmine dayalı düşünceleri analiz modeli](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) Cortana Intelligence Galerisi'nde sayfasında.</span><span class="sxs-lookup"><span data-stu-id="82eb2-157">Go to the [predictive sentiment analytics model](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) page in the Cortana Intelligence Gallery.</span></span>  

2. <span data-ttu-id="82eb2-158">Tıklatın **Studio'da Aç**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-158">Click **Open in Studio**.</span></span>  
   
   ![Stream Analytics Machine Learning, açık Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. <span data-ttu-id="82eb2-160">Çalışma alanına gidin için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="82eb2-160">Sign in to go to the workspace.</span></span> <span data-ttu-id="82eb2-161">Bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="82eb2-161">Select a location.</span></span>

4. <span data-ttu-id="82eb2-162">Tıklatın **çalıştırmak** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="82eb2-162">Click **Run** at the bottom of the page.</span></span> <span data-ttu-id="82eb2-163">İşlem çalışır ve hangi yaklaşık bir dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="82eb2-163">The process runs, which takes about a minute.</span></span>

   ![denemeyi Machine Learning Studio'da çalıştırın](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. <span data-ttu-id="82eb2-165">İşlem başarıyla çalıştırıldıktan sonra seçin **Web hizmeti Dağıt** sayfanın sonundaki.</span><span class="sxs-lookup"><span data-stu-id="82eb2-165">After the process has run successfully, select **Deploy Web Service** at the bottom of the page.</span></span>

   ![denemeyi Machine Learning Studio'da bir web hizmeti olarak dağıtma](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. <span data-ttu-id="82eb2-167">Düşünceleri analiz modeli kullanıma hazır olduğunu doğrulamak için tıklatın **Test** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="82eb2-167">To validate that the sentiment analytics model is ready to use, click the **Test** button.</span></span> <span data-ttu-id="82eb2-168">Metin "ı Microsoft memnuniyet"gibi giriş sağlar.</span><span class="sxs-lookup"><span data-stu-id="82eb2-168">Provide text input such as "I love Microsoft".</span></span> 

   ![Machine Learning Studio'da Test deneme](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    <span data-ttu-id="82eb2-170">Test çalışırsa, aşağıdaki örneğe benzer bir sonuç bakın:</span><span class="sxs-lookup"><span data-stu-id="82eb2-170">If the test works, you see a result similar to the following example:</span></span>

   ![Machine Learning Studio'da test sonuçları](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. <span data-ttu-id="82eb2-172">İçinde **uygulamaları** sütun tıklatın **Excel 2010 veya önceki çalışma kitabı** bir Excel çalışma kitabı indirmek için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="82eb2-172">In the **Apps** column, click the **Excel 2010 or earlier workbook** link to download an Excel workbook.</span></span> <span data-ttu-id="82eb2-173">Çalışma kitabını içeren bir API anahtarı ve daha sonra Stream Analytics işi ayarlamak için gereken URL.</span><span class="sxs-lookup"><span data-stu-id="82eb2-173">The workbook contains the an API key and the URL that you need later to set up the Stream Analytics job.</span></span>

    ![Stream Analytics Machine Learning, Hızlı Bakış](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-the-machine-learning-model"></a><span data-ttu-id="82eb2-175">Machine Learning modelini kullanan bir Stream Analytics işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="82eb2-175">Create a Stream Analytics job that uses the Machine Learning model</span></span>

<span data-ttu-id="82eb2-176">Artık blob depolamada CSV dosyasından örnek tweet'leri okuyan akış analizi işi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82eb2-176">You can now create a Stream Analytics job that reads the sample tweets from the CSV file in blob storage.</span></span> 

### <a name="create-the-job"></a><span data-ttu-id="82eb2-177">Proje oluşturma</span><span class="sxs-lookup"><span data-stu-id="82eb2-177">Create the job</span></span>

1. <span data-ttu-id="82eb2-178">[Azure Portal](https://portal.azure.com) gidin.</span><span class="sxs-lookup"><span data-stu-id="82eb2-178">Go to the [Azure portal](https://portal.azure.com).</span></span>  

2. <span data-ttu-id="82eb2-179">Tıklatın **yeni** > **nesnelerin interneti** > **Stream Analytics işi**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-179">Click **New** > **Internet of Things** > **Stream Analytics job**.</span></span> 

   ![Yeni bir akış analizi işi almak için azure portal yolu](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. <span data-ttu-id="82eb2-181">İş adı `azure-sa-ml-demo`bir abonelik belirtin, varolan bir kaynak grubu belirtin veya yeni bir tane oluşturun ve iş konumunu seçin.</span><span class="sxs-lookup"><span data-stu-id="82eb2-181">Name the job `azure-sa-ml-demo`, specify a subscription, specify an existing resource group or create a new one, and select the location for the job.</span></span>

   ![Yeni akış analizi işi için ayarları belirtin](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-the-job-input"></a><span data-ttu-id="82eb2-183">İş Girişi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="82eb2-183">Configure the job input</span></span>
<span data-ttu-id="82eb2-184">İş kendi giriş blob depolama alanına daha önce yüklediğiniz CSV dosyasından alır.</span><span class="sxs-lookup"><span data-stu-id="82eb2-184">The job gets its input from the CSV file that you uploaded earlier to blob storage.</span></span>

1. <span data-ttu-id="82eb2-185">İş, altında oluşturulduktan sonra **iş topoloji** iş dikey penceresinde tıklayın **girişleri** kutusu.</span><span class="sxs-lookup"><span data-stu-id="82eb2-185">After the job has been created, under **Job Topology** in the job blade, click the **Inputs** box.</span></span>  
   
   ![Akış analizi işi dikey penceresinde 'Girişleri' kutusu](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. <span data-ttu-id="82eb2-187">İçinde **girişleri** dikey penceresinde tıklatın **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-187">In the **Inputs** blade, click **+ Add**.</span></span>

   ![Bir akış analizi işine giriş eklemek için 'Add' düğmesi](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. <span data-ttu-id="82eb2-189">Doldurmak **yeni giriş** dikey penceresinde bu değerleri içeren:</span><span class="sxs-lookup"><span data-stu-id="82eb2-189">Fill out the **New input** blade with these values:</span></span>

    * <span data-ttu-id="82eb2-190">**Giriş diğer adı**: adını kullanmak `datainput`.</span><span class="sxs-lookup"><span data-stu-id="82eb2-190">**Input alias**: Use the name `datainput`.</span></span>
    * <span data-ttu-id="82eb2-191">**Kaynak türünü**: seçin **veri akışı**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-191">**Source type**: Select **Data stream**.</span></span>
    * <span data-ttu-id="82eb2-192">**Kaynak**: seçin **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-192">**Source**: Select **Blob storage**.</span></span>
    * <span data-ttu-id="82eb2-193">**Alma seçeneği**: seçin **blob storage'ı geçerli aboneliğe ilişkin kullanma**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-193">**Import option**: Select **Use blob storage from current subscription**.</span></span> 
    * <span data-ttu-id="82eb2-194">**Depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-194">**Storage account**.</span></span> <span data-ttu-id="82eb2-195">Daha önce oluşturduğunuz depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="82eb2-195">Select the storage account you created earlier.</span></span>
    * <span data-ttu-id="82eb2-196">**Kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-196">**Container**.</span></span> <span data-ttu-id="82eb2-197">Daha önce oluşturduğunuz kapsayıcısı seçin (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="82eb2-197">Select the container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="82eb2-198">**Olayı seri hale getirme biçimi**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-198">**Event serialization format**.</span></span> <span data-ttu-id="82eb2-199">Seçin **CSV**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-199">Select **CSV**.</span></span>

    ![Yeni iş girişi için ayarlar](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. <span data-ttu-id="82eb2-201">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="82eb2-201">Click **Create**.</span></span>

### <a name="configure-the-job-output"></a><span data-ttu-id="82eb2-202">İş çıktısı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="82eb2-202">Configure the job output</span></span>
<span data-ttu-id="82eb2-203">İş yeri giriş sonuçları aynı blob depolama alanına gönderir.</span><span class="sxs-lookup"><span data-stu-id="82eb2-203">The job sends results to the same blob storage where it gets input.</span></span> 

1. <span data-ttu-id="82eb2-204">Altında **iş topoloji** iş dikey penceresinde tıklayın **çıkışları** kutusu.</span><span class="sxs-lookup"><span data-stu-id="82eb2-204">Under **Job Topology** in the job blade, click the **Outputs** box.</span></span>  
  
   ![Akış analizi işi için yeni çıkış oluşturma](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. <span data-ttu-id="82eb2-206">İçinde **çıkışları** dikey penceresinde tıklatın **+ Ekle**ve ardından diğer ada sahip bir çıkış ekleyin `datamloutput`.</span><span class="sxs-lookup"><span data-stu-id="82eb2-206">In the **Outputs** blade, click **+ Add**, and then add an output with the alias `datamloutput`.</span></span> 

3. <span data-ttu-id="82eb2-207">İçin **havuzu**seçin **Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-207">For **Sink**, select **Blob storage**.</span></span> <span data-ttu-id="82eb2-208">Ardından giriş için blob depolama için kullanılan aynı değerleri kullanarak çıktı ayarların geri kalanı doldurun:</span><span class="sxs-lookup"><span data-stu-id="82eb2-208">Then fill in the rest of the output settings using the same values that you used for the blob storage for input:</span></span>

    * <span data-ttu-id="82eb2-209">**Depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-209">**Storage account**.</span></span> <span data-ttu-id="82eb2-210">Daha önce oluşturduğunuz depolama hesabını seçin.</span><span class="sxs-lookup"><span data-stu-id="82eb2-210">Select the storage account you created earlier.</span></span>
    * <span data-ttu-id="82eb2-211">**Kapsayıcı**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-211">**Container**.</span></span> <span data-ttu-id="82eb2-212">Daha önce oluşturduğunuz kapsayıcısı seçin (`azuresamldemoblob`).</span><span class="sxs-lookup"><span data-stu-id="82eb2-212">Select the container you created earlier (`azuresamldemoblob`).</span></span>
    * <span data-ttu-id="82eb2-213">**Olayı seri hale getirme biçimi**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-213">**Event serialization format**.</span></span> <span data-ttu-id="82eb2-214">Seçin **CSV**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-214">Select **CSV**.</span></span>

   ![Yeni iş çıktısı için ayarları](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. <span data-ttu-id="82eb2-216">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="82eb2-216">Click **Create**.</span></span>   


### <a name="add-the-machine-learning-function"></a><span data-ttu-id="82eb2-217">Machine Learning işlevi ekleme</span><span class="sxs-lookup"><span data-stu-id="82eb2-217">Add the Machine Learning function</span></span> 
<span data-ttu-id="82eb2-218">Daha önce bir web hizmetine bir Machine Learning modeli yayımladı.</span><span class="sxs-lookup"><span data-stu-id="82eb2-218">Earlier you published a Machine Learning model to a web service.</span></span> <span data-ttu-id="82eb2-219">Akış analizi işi çalıştığında, Senaryomuzda her örnek tweet girdisinden düşünceleri çözümleme için web hizmetine gönderir.</span><span class="sxs-lookup"><span data-stu-id="82eb2-219">In our scenario, when the Stream Analysis job runs, it sends each sample tweet from the input to the web service for sentiment analysis.</span></span> <span data-ttu-id="82eb2-220">Machine Learning web hizmeti bir düşünceleri döndürür (`positive`, `neutral`, veya `negative`) ve pozitif olması tweet bir olasılık.</span><span class="sxs-lookup"><span data-stu-id="82eb2-220">The Machine Learning web service returns a sentiment (`positive`, `neutral`, or `negative`) and a probability of the tweet being positive.</span></span> 

<span data-ttu-id="82eb2-221">Öğreticinin bu bölümünde, akış analizi işi işlevinde tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="82eb2-221">In this section of the tutorial, you define a function in the Stream Analysis job.</span></span> <span data-ttu-id="82eb2-222">İşlev, web hizmetine tweet gönderecek ve yanıt geri almak için çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="82eb2-222">The function can be invoked to send a tweet to the web service and get the response back.</span></span> 

1. <span data-ttu-id="82eb2-223">Excel çalışma kitabında daha önce yüklediğiniz web hizmeti URL'sini ve API anahtarını olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="82eb2-223">Make sure you have the web service URL and API key that you downloaded earlier in the Excel workbook.</span></span>

2. <span data-ttu-id="82eb2-224">İş genel bakış dikey penceresine geri dönün.</span><span class="sxs-lookup"><span data-stu-id="82eb2-224">Return to the job overview blade.</span></span>

3. <span data-ttu-id="82eb2-225">Altında **ayarları**seçin **işlevleri** ve ardından **+ Ekle**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-225">Under **Settings**, select **Functions** and then click **+ Add**.</span></span>

   ![Stream Analytics işi için bir işlev Ekle](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. <span data-ttu-id="82eb2-227">Girin `sentiment` işlevi diğer adını ve bu değerleri kullanarak dikey kalan doldururken olarak:</span><span class="sxs-lookup"><span data-stu-id="82eb2-227">Enter `sentiment` as the function alias and fill out the rest of the blade using these values:</span></span>

    * <span data-ttu-id="82eb2-228">**İşlev türü**: seçin **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-228">**Function type**: Select **Azure ML**.</span></span>
    * <span data-ttu-id="82eb2-229">**Alma seçeneği**: seçin **farklı bir abonelik alma**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-229">**Import option**: Select **Import from a different subscription**.</span></span> <span data-ttu-id="82eb2-230">Bu anahtarı ve URL girin olanağı verir.</span><span class="sxs-lookup"><span data-stu-id="82eb2-230">This gives you a chance to enter the URL and key.</span></span>
    * <span data-ttu-id="82eb2-231">**URL**: web hizmeti URL'si yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="82eb2-231">**URL**: Paste in the web service URL.</span></span>
    * <span data-ttu-id="82eb2-232">**Anahtar**: API anahtarını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="82eb2-232">**Key**: Paste in the API key.</span></span>
  
    ![Machine Learning işlevi Stream Analytics işi eklemek için ayarlar](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. <span data-ttu-id="82eb2-234">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="82eb2-234">Click **Create**.</span></span>

### <a name="create-a-query-to-transform-the-data"></a><span data-ttu-id="82eb2-235">Verileri dönüştürmek için bir sorgu oluşturun</span><span class="sxs-lookup"><span data-stu-id="82eb2-235">Create a query to transform the data</span></span>

<span data-ttu-id="82eb2-236">Akış analizi giriş inceleyin ve işleme için bir bildirim temelli, SQL tabanlı sorgu kullanır.</span><span class="sxs-lookup"><span data-stu-id="82eb2-236">Stream Analytics uses a declarative, SQL-based query to examine the input and process it.</span></span> <span data-ttu-id="82eb2-237">Bu bölümde, her tweet girişten okuyan ve düşünceleri analizi yapmak için Machine Learning işlevi çağıran bir sorgu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82eb2-237">In this section, you create a query that reads each tweet from input and then invokes the Machine Learning function to perform sentiment analysis.</span></span> <span data-ttu-id="82eb2-238">Sorgu sonucu sonra (blob depolama) tanımlanan çıkış gönderir.</span><span class="sxs-lookup"><span data-stu-id="82eb2-238">The query then sends the result to the output that you defined (blob storage).</span></span>

1. <span data-ttu-id="82eb2-239">İş genel bakış dikey penceresine geri dönün.</span><span class="sxs-lookup"><span data-stu-id="82eb2-239">Return to the job overview blade.</span></span>

2.  <span data-ttu-id="82eb2-240">Altında **iş topoloji**, tıklatın **sorgu** kutusu.</span><span class="sxs-lookup"><span data-stu-id="82eb2-240">Under **Job Topology**, click the **Query** box.</span></span>

    ![Akış analizi işi için bir sorgu oluşturun](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. <span data-ttu-id="82eb2-242">Aşağıdaki sorguyu girin:</span><span class="sxs-lookup"><span data-stu-id="82eb2-242">Enter the following query:</span></span>

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    <span data-ttu-id="82eb2-243">Sorgu daha önce oluşturduğunuz işlevi çağırır (`sentiment`) her tweet giriş üzerinde düşünceleri analiz gerçekleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="82eb2-243">The query invokes the function you created earlier (`sentiment`) in order to perform sentiment analysis on each tweet in the input.</span></span> 

4. <span data-ttu-id="82eb2-244">Tıklatın **kaydetmek** sorguyu kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="82eb2-244">Click **Save** to save the query.</span></span>


## <a name="start-the-stream-analytics-job-and-check-the-output"></a><span data-ttu-id="82eb2-245">Stream Analytics işini başlatmak ve çıktısını denetleyin</span><span class="sxs-lookup"><span data-stu-id="82eb2-245">Start the Stream Analytics job and check the output</span></span>

<span data-ttu-id="82eb2-246">Stream Analytics işi şimdi başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82eb2-246">You can now start the Stream Analytics job.</span></span>

### <a name="start-the-job"></a><span data-ttu-id="82eb2-247">İşi Başlat</span><span class="sxs-lookup"><span data-stu-id="82eb2-247">Start the job</span></span>
1. <span data-ttu-id="82eb2-248">İş genel bakış dikey penceresine geri dönün.</span><span class="sxs-lookup"><span data-stu-id="82eb2-248">Return to the job overview blade.</span></span>

2. <span data-ttu-id="82eb2-249">Tıklatın **Başlat** dikey pencerenin üstündeki.</span><span class="sxs-lookup"><span data-stu-id="82eb2-249">Click **Start** at the top of the blade.</span></span>

    ![Akış analizi işi için bir sorgu oluşturun](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. <span data-ttu-id="82eb2-251">İçinde **başlangıç işi**seçin **özel**ve ardından bir blob depolama alanına CSV dosyasını karşıya önce gün seçin.</span><span class="sxs-lookup"><span data-stu-id="82eb2-251">In the **Start job**, select **Custom**, and then select one day prior to when you uploaded the CSV file to blob storage.</span></span> <span data-ttu-id="82eb2-252">İşiniz bittiğinde tıklatın **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-252">When you're done, click **Start**.</span></span>  


### <a name="check-the-output"></a><span data-ttu-id="82eb2-253">Çıktı denetleyin</span><span class="sxs-lookup"><span data-stu-id="82eb2-253">Check the output</span></span>
1. <span data-ttu-id="82eb2-254">Etkinliğinde görene kadar birkaç dakika için iş izin **izleme** kutusu.</span><span class="sxs-lookup"><span data-stu-id="82eb2-254">Let the job run for a few minutes until you see activity in the **Monitoring** box.</span></span> 

2. <span data-ttu-id="82eb2-255">Blob depolama içeriğini incelemek için normalde kullandığınız bir aracı varsa, incelemek için bu aracı kullanın `azuresamldemoblob` kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="82eb2-255">If you have a tool that you normally use to examine the contents of blob storage, use that tool to examine the `azuresamldemoblob` container.</span></span> <span data-ttu-id="82eb2-256">Alternatif olarak, Azure portalında aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="82eb2-256">Alternatively, do the following steps in the Azure portal:</span></span>

    1. <span data-ttu-id="82eb2-257">Portalı'nda bulmak `samldemo` depolama hesabı ve hesaptaki Bul `azuresamldemoblob` kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="82eb2-257">In the portal, find the `samldemo` storage account, and within the account, find the `azuresamldemoblob` container.</span></span> <span data-ttu-id="82eb2-258">Kapsayıcı iki dosyada bkz: örnek tweet'leri içeren dosya ve akış analizi işi tarafından oluşturulan bir CSV dosyası.</span><span class="sxs-lookup"><span data-stu-id="82eb2-258">You see two files in the container: the file that contains the sample tweets and a CSV file generated by the Stream Analytics job.</span></span>
    2. <span data-ttu-id="82eb2-259">Oluşturulan dosyaya sağ tıklayın ve ardından **karşıdan**.</span><span class="sxs-lookup"><span data-stu-id="82eb2-259">Right-click the generated file and then select **Download**.</span></span> 

   ![Blob depolama alanından CSV iş çıktısı indirme](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. <span data-ttu-id="82eb2-261">Oluşturulan CSV dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="82eb2-261">Open the generated CSV file.</span></span> <span data-ttu-id="82eb2-262">Aşağıdaki örneğe benzer bir şey görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="82eb2-262">You see something like the following example:</span></span>  
   
   ![Stream Analytics Machine Learning, CSV görünümü](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a><span data-ttu-id="82eb2-264">Metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="82eb2-264">View metrics</span></span>
<span data-ttu-id="82eb2-265">Azure Machine Learning işlevi ödemeyle ilgili ölçümlerini de görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82eb2-265">You also can view Azure Machine Learning function-related metrics.</span></span> <span data-ttu-id="82eb2-266">Aşağıdaki işlevi ödemeyle ilgili ölçümlerini görüntülenen **izleme** iş dikey penceresinde kutusunda:</span><span class="sxs-lookup"><span data-stu-id="82eb2-266">The following function-related metrics are displayed in the **Monitoring** box in the job blade:</span></span>

* <span data-ttu-id="82eb2-267">**İşlev istekleri** Machine Learning web hizmetine gönderilen istek sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="82eb2-267">**Function Requests** indicates the number of requests sent to a Machine Learning web service.</span></span>  
* <span data-ttu-id="82eb2-268">**İşlev olayları** olayları isteği sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="82eb2-268">**Function Events** indicates the number of events in the request.</span></span> <span data-ttu-id="82eb2-269">Varsayılan olarak, her bir Machine Learning web hizmeti isteğine en çok 1.000 olayları içerir.</span><span class="sxs-lookup"><span data-stu-id="82eb2-269">By default, each request to a Machine Learning web service contains up to 1,000 events.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="82eb2-270">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="82eb2-270">Next steps</span></span>

* [<span data-ttu-id="82eb2-271">Azure Stream Analytics'e giriş</span><span class="sxs-lookup"><span data-stu-id="82eb2-271">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="82eb2-272">Azure Akış Analizi Sorgu Dili Başvurusu</span><span class="sxs-lookup"><span data-stu-id="82eb2-272">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="82eb2-273">REST API tümleştirme ve makine öğrenme</span><span class="sxs-lookup"><span data-stu-id="82eb2-273">Integrate REST API and Machine Learning</span></span>](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [<span data-ttu-id="82eb2-274">Azure Akış Analizi Yönetimi REST API'si Başvurusu</span><span class="sxs-lookup"><span data-stu-id="82eb2-274">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)



