---
title: "Tahmine dayalı varolan aaaRetrain web hizmetini | Microsoft Docs"
description: "Web hizmeti toouse hello yeni eğitilen modeli Azure Machine learning'de tooretrain bir model ve güncelleştirme nasıl hello öğrenin."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: fb0760d0a2adc34fc5f3df1ae41bdac075f91bf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="84a7f-103">Var olan bir Tahmine dayalı web hizmetini yeniden eğitme</span><span class="sxs-lookup"><span data-stu-id="84a7f-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="84a7f-104">Bu belgede senaryo aşağıdaki hello işlemlerinde yeniden eğitme hello açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="84a7f-104">This document describes hello retraining process for hello following scenario:</span></span>

* <span data-ttu-id="84a7f-105">Eğitim denemenizi ve kullanıma hazır hale getirilmiş web hizmeti olarak dağıttığınız bir tahmini deneme var.</span><span class="sxs-lookup"><span data-stu-id="84a7f-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="84a7f-106">Tahmine dayalı web hizmeti toouse tooperform kendi Puanlama istediğiniz yeni veriler var.</span><span class="sxs-lookup"><span data-stu-id="84a7f-106">You have new data that you want your predictive web service toouse tooperform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="84a7f-107">toodeploy yeni bir web hizmeti yeterli izniniz hello abonelik toowhich, hello web Hizmeti'ni dağıtma olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="84a7f-107">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="84a7f-108">Daha fazla bilgi için [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="84a7f-108">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="84a7f-109">Denemeler ve varolan web hizmeti ile başlayarak, aşağıdaki adımları toofollow gerekir:</span><span class="sxs-lookup"><span data-stu-id="84a7f-109">Starting with your existing web service and experiments, you need toofollow these steps:</span></span>

1. <span data-ttu-id="84a7f-110">Merhaba modeli güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="84a7f-110">Update hello model.</span></span>
   1. <span data-ttu-id="84a7f-111">Web hizmeti girişleri ve çıkışları, eğitim deneme tooallow değiştirin.</span><span class="sxs-lookup"><span data-stu-id="84a7f-111">Modify your training experiment tooallow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="84a7f-112">Merhaba eğitim denemenizi yeniden eğitme bir web hizmeti olarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="84a7f-112">Deploy hello training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="84a7f-113">Merhaba eğitim deneme toplu yürütme hizmeti (BES) tooretrain hello modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="84a7f-113">Use hello training experiment's Batch Execution Service (BES) tooretrain hello model.</span></span>
2. <span data-ttu-id="84a7f-114">Hello Azure Machine Learning PowerShell cmdlet'leri tooupdate hello Tahmine dayalı denemeye kullanın.</span><span class="sxs-lookup"><span data-stu-id="84a7f-114">Use hello Azure Machine Learning PowerShell cmdlets tooupdate hello predictive experiment.</span></span>
   1. <span data-ttu-id="84a7f-115">Tooyour Azure Resource Manager hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="84a7f-115">Sign in tooyour Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="84a7f-116">Merhaba web hizmeti tanımının alın.</span><span class="sxs-lookup"><span data-stu-id="84a7f-116">Get hello web service definition.</span></span>
   3. <span data-ttu-id="84a7f-117">Merhaba web hizmeti tanımının JSON olarak dışarı aktarın.</span><span class="sxs-lookup"><span data-stu-id="84a7f-117">Export hello web service definition as JSON.</span></span>
   4. <span data-ttu-id="84a7f-118">Merhaba başvuru toohello ilearner blob hello JSON güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="84a7f-118">Update hello reference toohello ilearner blob in hello JSON.</span></span>
   5. <span data-ttu-id="84a7f-119">Merhaba JSON web hizmeti tanımının alın.</span><span class="sxs-lookup"><span data-stu-id="84a7f-119">Import hello JSON into a web service definition.</span></span>
   6. <span data-ttu-id="84a7f-120">Merhaba web hizmeti ile yeni bir web hizmeti tanımının güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="84a7f-120">Update hello web service with a new web service definition.</span></span>

## <a name="deploy-hello-training-experiment"></a><span data-ttu-id="84a7f-121">Merhaba eğitim denemenizi dağıtma</span><span class="sxs-lookup"><span data-stu-id="84a7f-121">Deploy hello training experiment</span></span>
<span data-ttu-id="84a7f-122">toodeploy hello eğitim denemenizi yeniden eğitme web hizmeti olarak web hizmeti girişleri ve çıkışları toohello modeli eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="84a7f-122">toodeploy hello training experiment as a retraining web service, you must add web service inputs and outputs toohello model.</span></span> <span data-ttu-id="84a7f-123">Bağlanarak bir *Web hizmeti çıkış* modülü toohello deneme  *[Train Model] [ train-model]*  modülünde deneme eğitim hello etkinleştir Tahmine dayalı denemenizde kullanabileceğiniz yeni bir eğitilen model tooproduce.</span><span class="sxs-lookup"><span data-stu-id="84a7f-123">By connecting a *Web Service Output* module toohello experiment's *[Train Model][train-model]* module, you enable hello training experiment tooproduce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="84a7f-124">Varsa bir *Evaluate Model* modülü, çıktı olarak web hizmeti çıkış tooget hello değerlendirme sonuçlarını da ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84a7f-124">If you have an *Evaluate Model* module, you can also attach web service output tooget hello evaluation results as output.</span></span>

<span data-ttu-id="84a7f-125">tooupdate eğitim denemenizi:</span><span class="sxs-lookup"><span data-stu-id="84a7f-125">tooupdate your training experiment:</span></span>

1. <span data-ttu-id="84a7f-126">Bağlantı bir *Web hizmeti giriş* modülü tooyour veri girişi (örneğin, bir *Clean Missing Data* Modülü).</span><span class="sxs-lookup"><span data-stu-id="84a7f-126">Connect a *Web Service Input* module tooyour data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="84a7f-127">Genellikle, giriş verilerinizi içinde işlenir tooensure istediğiniz aynı hello özgün eğitim verilerinizi şekilde.</span><span class="sxs-lookup"><span data-stu-id="84a7f-127">Typically, you want tooensure that your input data is processed in hello same way as your original training data.</span></span>
2. <span data-ttu-id="84a7f-128">Bağlantı bir *Web hizmeti çıkış* modülü toohello çıktısı, *Train Model* modülü.</span><span class="sxs-lookup"><span data-stu-id="84a7f-128">Connect a *Web Service Output* module toohello output of your *Train Model* module.</span></span>
3. <span data-ttu-id="84a7f-129">Varsa bir *Evaluate Model* modülü ve toooutput hello değerlendirme sonuçlarını istiyorsanız, bağlanmak bir *Web hizmeti çıkış* modülü toohello çıktısı, *Evaluate Model* Modül.</span><span class="sxs-lookup"><span data-stu-id="84a7f-129">If you have an *Evaluate Model* module and you want toooutput hello evaluation results, connect a *Web Service Output* module toohello output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="84a7f-130">Denemenizi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="84a7f-130">Run your experiment.</span></span>

<span data-ttu-id="84a7f-131">Ardından, hello eğitim denemenizi eğitilen bir modelin ve model değerlendirme sonuçlarını üreten bir web hizmeti olarak dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="84a7f-131">Next, you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="84a7f-132">Merhaba deneme tuvalinin Hello altındaki tıklatın **Web hizmetinin ayarı**ve ardından **Web hizmeti dağıtma [Yeni]**.</span><span class="sxs-lookup"><span data-stu-id="84a7f-132">At hello bottom of hello experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="84a7f-133">Hello Azure Machine Learning Web Hizmetleri portalı açar toohello **Web hizmeti Dağıt** sayfası.</span><span class="sxs-lookup"><span data-stu-id="84a7f-133">hello Azure Machine Learning Web Services portal opens toohello **Deploy Web Service** page.</span></span> <span data-ttu-id="84a7f-134">Web hizmetiniz için bir ad yazın, ödeme planı seçin ve ardından **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="84a7f-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="84a7f-135">Eğitilmiş modeller oluşturmak için yalnızca hello toplu iş yürütme yöntemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84a7f-135">You can only use hello Batch Execution method for creating trained models.</span></span>

## <a name="retrain-hello-model-with-new-data-by-using-bes"></a><span data-ttu-id="84a7f-136">BES kullanarak Hello modeli yeni verilerle birlikte yeniden eğitme</span><span class="sxs-lookup"><span data-stu-id="84a7f-136">Retrain hello model with new data by using BES</span></span>
<span data-ttu-id="84a7f-137">Bu örnekte, biz toocreate uygulama yeniden eğitme C# hello kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="84a7f-137">For this example, we're using C# toocreate hello retraining application.</span></span> <span data-ttu-id="84a7f-138">Bu görev Python veya R örnek kodu tooaccomplish de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84a7f-138">You can also use Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="84a7f-139">yeniden eğitme API'lerini toocall hello:</span><span class="sxs-lookup"><span data-stu-id="84a7f-139">toocall hello retraining APIs:</span></span>

1. <span data-ttu-id="84a7f-140">Visual Studio'da bir C# konsol uygulaması oluşturun: **yeni** > **proje** > **Visual C#** > **Windows Klasik Masaüstü** > **konsol uygulaması (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="84a7f-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="84a7f-141">İçinde toohello Machine Learning Web Hizmetleri portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="84a7f-141">Sign in toohello Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="84a7f-142">Üzerinde çalıştığınız hello web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="84a7f-142">Click hello web service that you're working with.</span></span>
4. <span data-ttu-id="84a7f-143">Tıklatın **tüketen**.</span><span class="sxs-lookup"><span data-stu-id="84a7f-143">Click **Consume**.</span></span>
5. <span data-ttu-id="84a7f-144">Merhaba hello sonundaki **Tüket** sayfasında hello **örnek kod** 'yi tıklatın **toplu**.</span><span class="sxs-lookup"><span data-stu-id="84a7f-144">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="84a7f-145">Toplu iş yürütme Hello örnek C# kodu kopyalayın ve hello Program.cs dosyasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="84a7f-145">Copy hello sample C# code for batch execution and paste it into hello Program.cs file.</span></span> <span data-ttu-id="84a7f-146">Merhaba ad olduğu gibi kalır emin olun.</span><span class="sxs-lookup"><span data-stu-id="84a7f-146">Make sure that hello namespace remains intact.</span></span>

<span data-ttu-id="84a7f-147">Merhaba açıklamaları belirtildiği gibi Hello NuGet paketini Microsoft.AspNet.WebApi.Client, ekleyin.</span><span class="sxs-lookup"><span data-stu-id="84a7f-147">Add hello NuGet package Microsoft.AspNet.WebApi.Client, as specified in hello comments.</span></span> <span data-ttu-id="84a7f-148">tooadd hello başvuru tooMicrosoft.WindowsAzure.Storage.dll ilk ihtiyacınız olabilecek tooinstall hello [Azure depolama hizmetleri için İstemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="84a7f-148">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="84a7f-149">Merhaba aşağıdaki ekran gösterilir hello **Tüket** hello Azure Machine Learning Web Hizmetleri portalında sayfası.</span><span class="sxs-lookup"><span data-stu-id="84a7f-149">hello following screenshot shows hello **Consume** page in hello Azure Machine Learning Web Services portal.</span></span>

![Sayfa kullanma][1]

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="84a7f-151">Merhaba apikey ile yapılan bildirimini güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="84a7f-151">Update hello apikey declaration</span></span>
<span data-ttu-id="84a7f-152">Merhaba bulun **apikey ile yapılan** bildirimi:</span><span class="sxs-lookup"><span data-stu-id="84a7f-152">Locate hello **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="84a7f-153">Merhaba, **temel tüketim bilgileri** hello bölümünü **Tüket** sayfasında hello birincil anahtarını bulun ve toohello kopyalama **apikey ile yapılan** bildirimi.</span><span class="sxs-lookup"><span data-stu-id="84a7f-153">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="84a7f-154">Hello Azure depolama bilgilerini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="84a7f-154">Update hello Azure Storage information</span></span>
<span data-ttu-id="84a7f-155">Merhaba BES örnek kod bir yerel sürücüye (örneğin, "C:\temp\CensusIpnput.csv") tooAzure depolama bir dosyadan yükler, işler ve hello sonuçları geri tooAzure depolama yazar.</span><span class="sxs-lookup"><span data-stu-id="84a7f-155">hello BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="84a7f-156">tooupdate hello Azure depolama bilgilerini hello depolama hesabı adı, anahtar ve kapsayıcı bilgilerini depolama hesabınızdan hello Klasik Azure portalı ve denemenizi, çalıştırdıktan sonra güncelleştirme hello correspondi kaynaklanan hello almanız gerekir İş akışı benzer toohello aşağıdaki gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="84a7f-156">tooupdate hello Azure Storage information, you must retrieve hello storage account name, key, and container information for your storage account from hello Azure classic portal, and then update hello correspondi After running your experiment, hello resulting workflow should be similar toohello following:</span></span>

![Çalıştırdıktan sonra elde edilen iş akışı][4]<span data-ttu-id="84a7f-158">Merhaba kod NG değerleri.</span><span class="sxs-lookup"><span data-stu-id="84a7f-158">ng values in hello code.</span></span>

1. <span data-ttu-id="84a7f-159">İçinde toohello Klasik Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="84a7f-159">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="84a7f-160">Merhaba sol gezinti sütununda **depolama**.</span><span class="sxs-lookup"><span data-stu-id="84a7f-160">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="84a7f-161">Depolama hesapları Hello listeden seçim bir toostore hello modeli retrained.</span><span class="sxs-lookup"><span data-stu-id="84a7f-161">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="84a7f-162">Merhaba sayfasının Hello altında tıklatın **erişim anahtarlarını Yönet**.</span><span class="sxs-lookup"><span data-stu-id="84a7f-162">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="84a7f-163">Kopyalayın ve hello kaydedin **birincil erişim anahtarını** ve Kapat hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="84a7f-163">Copy and save hello **Primary Access Key** and close hello dialog.</span></span>
6. <span data-ttu-id="84a7f-164">Merhaba hello sayfanın en üstünde, tıklatın **kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="84a7f-164">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="84a7f-165">Var olan bir kapsayıcıyı seçin veya yeni bir tane oluşturun ve hello adı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="84a7f-165">Select an existing container, or create a new one and save hello name.</span></span>

<span data-ttu-id="84a7f-166">Merhaba bulun *StorageAccountName*, *StorageAccountKey*, ve *StorageContainerName* bildirimler ve hello Klasik portalından kaydedilen güncelleştirme hello değerleri .</span><span class="sxs-lookup"><span data-stu-id="84a7f-166">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update hello values that you saved from hello classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="84a7f-167">Ayrıca bu hello giriş dosyası, hello kodda belirtme hello konumda kullanılabilir olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="84a7f-167">You also must ensure that hello input file is available at hello location that you specify in hello code.</span></span>

### <a name="specify-hello-output-location"></a><span data-ttu-id="84a7f-168">Merhaba çıkış konumunu belirtin</span><span class="sxs-lookup"><span data-stu-id="84a7f-168">Specify hello output location</span></span>
<span data-ttu-id="84a7f-169">Merhaba Request yükü hello çıkış konumu belirttiğinizde, belirtilen hello dosya uzantısını hello *RelativeLocation* olarak belirtilmelidir `ilearner`.</span><span class="sxs-lookup"><span data-stu-id="84a7f-169">When you specify hello output location in hello Request Payload, hello extension of hello file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="84a7f-170">Aşağıdaki örnek hello bakın:</span><span class="sxs-lookup"><span data-stu-id="84a7f-170">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you want toouse for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="84a7f-171">Merhaba çıkış yeniden eğitme bir örnek şudur: ![çıkış yeniden eğitme][6]</span><span class="sxs-lookup"><span data-stu-id="84a7f-171">hello following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="84a7f-172">Sonuçları yeniden eğitme hello değerlendir</span><span class="sxs-lookup"><span data-stu-id="84a7f-172">Evaluate hello retraining results</span></span>
<span data-ttu-id="84a7f-173">Merhaba uygulamayı çalıştırdığınızda, hello çıktı hello URL ve gerekli tooaccess hello değerlendirme sonuçları paylaşılan erişim imzaları belirteci içerir.</span><span class="sxs-lookup"><span data-stu-id="84a7f-173">When you run hello application, hello output includes hello URL and shared access signatures token that are necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="84a7f-174">Merhaba birleştirerek retrained hello modelinin hello performans sonuçlarını görebilirsiniz *BaseLocation*, *RelativeLocation*, ve *SasBlobToken* hello çıkış sonuçlarından için *output2* (Merhaba çıktı görüntü yeniden eğitme önceki gösterildiği gibi) ve hello tam URL hello tarayıcınızın adres çubuğuna yapıştırma.</span><span class="sxs-lookup"><span data-stu-id="84a7f-174">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL into hello browser address bar.</span></span>  

<span data-ttu-id="84a7f-175">Merhaba yeni eğitilen model bir varolan iyi yeterli tooreplace hello gerçekleştiğini hello sonuçları toodetermine inceleyin.</span><span class="sxs-lookup"><span data-stu-id="84a7f-175">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="84a7f-176">Kopya hello *BaseLocation*, *RelativeLocation*, ve *SasBlobToken* hello çıkış sonuçlarından.</span><span class="sxs-lookup"><span data-stu-id="84a7f-176">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results.</span></span>

## <a name="retrain-hello-web-service"></a><span data-ttu-id="84a7f-177">Merhaba web hizmeti yeniden eğitme</span><span class="sxs-lookup"><span data-stu-id="84a7f-177">Retrain hello web service</span></span>
<span data-ttu-id="84a7f-178">Yeni bir web hizmeti yeniden eğitme, hello Tahmine dayalı web hizmeti tanımı tooreference hello yeni eğitilen modeli güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="84a7f-178">When you retrain a new web service, you update hello predictive web service definition tooreference hello new trained model.</span></span> <span data-ttu-id="84a7f-179">Merhaba web hizmeti tanımının hello eğitilen model hello web hizmetinin iç bir gösterimini ve doğrudan değiştirilebilir değil.</span><span class="sxs-lookup"><span data-stu-id="84a7f-179">hello web service definition is an internal representation of hello trained model of hello web service and is not directly modifiable.</span></span> <span data-ttu-id="84a7f-180">Tahmine dayalı denemenizi ve değil eğitim denemenizi hello web hizmeti tanımının alırsınız emin olun.</span><span class="sxs-lookup"><span data-stu-id="84a7f-180">Make sure that you are retrieving hello web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-tooazure-resource-manager"></a><span data-ttu-id="84a7f-181">TooAzure Resource Manager oturum</span><span class="sxs-lookup"><span data-stu-id="84a7f-181">Sign in tooAzure Resource Manager</span></span>
<span data-ttu-id="84a7f-182">Öncelikle tooyour hello PowerShell ortamında Azure hesabından içinde hello kullanarak oturum açmanız gerekir [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="84a7f-182">You must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-hello-web-service-definition-object"></a><span data-ttu-id="84a7f-183">Merhaba Web hizmeti tanımının nesnesini alın</span><span class="sxs-lookup"><span data-stu-id="84a7f-183">Get hello Web Service Definition object</span></span>
<span data-ttu-id="84a7f-184">Ardından, arama hello tarafından hello Web hizmeti tanımının nesne get [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="84a7f-184">Next, get hello Web Service Definition object by calling hello [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="84a7f-185">toodetermine hello kaynak grubu adı var olan bir web hizmeti, aboneliğinizdeki tüm parametreleri toodisplay hello web Hizmetleri olmadan hello Get-AzureRmMlWebService cmdlet'ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="84a7f-185">toodetermine hello resource group name of an existing web service, run hello Get-AzureRmMlWebService cmdlet without any parameters toodisplay hello web services in your subscription.</span></span> <span data-ttu-id="84a7f-186">Merhaba web hizmetini bulun ve sonra web hizmeti kimliğini arayın</span><span class="sxs-lookup"><span data-stu-id="84a7f-186">Locate hello web service, and then look at its web service ID.</span></span> <span data-ttu-id="84a7f-187">Hello hello kaynak grubunun adıdır hello dördüncü hello kimliği öğesinde yalnızca hello sonra *resourceGroups* öğesi.</span><span class="sxs-lookup"><span data-stu-id="84a7f-187">hello name of hello resource group is hello fourth element in hello ID, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="84a7f-188">Aşağıdaki örneğine hello hello kaynak grubu adı varsayılan MachineLearning SouthCentralUS ' dir.</span><span class="sxs-lookup"><span data-stu-id="84a7f-188">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="84a7f-189">Varolan bir alternatif olarak, toodetermine hello kaynak grubu adı web hizmeti, toohello Azure Machine Learning Web Hizmetleri portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="84a7f-189">Alternatively, toodetermine hello resource group name of an existing web service, sign in toohello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="84a7f-190">Merhaba web hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="84a7f-190">Select hello web service.</span></span> <span data-ttu-id="84a7f-191">Merhaba kaynak grubu adı öğedir hello beşinci hello hello web hizmeti URL'sini hemen sonra hello *resourceGroups* öğesi.</span><span class="sxs-lookup"><span data-stu-id="84a7f-191">hello resource group name is hello fifth element of hello URL of hello web service, just after hello *resourceGroups* element.</span></span> <span data-ttu-id="84a7f-192">Aşağıdaki örneğine hello hello kaynak grubu adı varsayılan MachineLearning SouthCentralUS ' dir.</span><span class="sxs-lookup"><span data-stu-id="84a7f-192">In hello following example, hello resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-hello-web-service-definition-object-as-json"></a><span data-ttu-id="84a7f-193">JSON olarak Hello Web hizmeti tanımının nesneyi ver</span><span class="sxs-lookup"><span data-stu-id="84a7f-193">Export hello Web Service Definition object as JSON</span></span>
<span data-ttu-id="84a7f-194">Merhaba, eğitilen model toouse hello toomodify hello tanımını yeni eğitilmiş model, önce hello kullanmanız gerekir [verme AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport onu tooa JSON biçimli dosya.</span><span class="sxs-lookup"><span data-stu-id="84a7f-194">toomodify hello definition of hello trained model toouse hello newly trained model, you must first use hello [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet tooexport it tooa JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-hello-reference-toohello-ilearner-blob"></a><span data-ttu-id="84a7f-195">Güncelleştirme hello başvuru toohello ilearner blob</span><span class="sxs-lookup"><span data-stu-id="84a7f-195">Update hello reference toohello ilearner blob</span></span>
<span data-ttu-id="84a7f-196">Merhaba [eğitilen model], güncelleştirme hello Hello varlıkları bulun *URI* hello değerinde *locationInfo* hello hello ilearner blob URI'si düğümle.</span><span class="sxs-lookup"><span data-stu-id="84a7f-196">In hello assets, locate hello [trained model], update hello *uri* value in hello *locationInfo* node with hello URI of hello ilearner blob.</span></span> <span data-ttu-id="84a7f-197">Merhaba URI hello birleştirerek oluşturulan *BaseLocation* ve hello *RelativeLocation* hello BES yeniden eğitme çağrısı hello çıktısından.</span><span class="sxs-lookup"><span data-stu-id="84a7f-197">hello URI is generated by combining hello *BaseLocation* and hello *RelativeLocation* from hello output of hello BES retraining call.</span></span>

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-hello-json-into-a-web-service-definition-object"></a><span data-ttu-id="84a7f-198">Bir Web hizmeti tanımının nesnesine Hello JSON aktarın</span><span class="sxs-lookup"><span data-stu-id="84a7f-198">Import hello JSON into a Web Service Definition object</span></span>
<span data-ttu-id="84a7f-199">Merhaba kullanmalısınız [alma AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello geri tooupdate hello predicative deneme kullanabileceğiniz bir Web hizmeti tanımının nesnesine JSON dosyasını değiştirdi.</span><span class="sxs-lookup"><span data-stu-id="84a7f-199">You must use hello [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet tooconvert hello modified JSON file back into a Web Service Definition object that you can use tooupdate hello predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-hello-web-service"></a><span data-ttu-id="84a7f-200">Merhaba web hizmetini güncelleştirmek</span><span class="sxs-lookup"><span data-stu-id="84a7f-200">Update hello web service</span></span>
<span data-ttu-id="84a7f-201">Son olarak, hello kullan [güncelleştirme AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello tahmini deneme.</span><span class="sxs-lookup"><span data-stu-id="84a7f-201">Finally, use hello [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet tooupdate hello predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
