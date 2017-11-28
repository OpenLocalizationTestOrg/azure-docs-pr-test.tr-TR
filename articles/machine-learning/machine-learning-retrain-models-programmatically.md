---
title: "aaaRetrain Machine Learning modellerini programlama aracılığıyla | Microsoft Docs"
description: "Tooprogrammatically bir model ve güncelleştirme hello web hizmeti toouse hello yeni eğitilen model Azure Machine Learning nasıl yeniden eğitme öğrenin."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: raymondl;garye;v-donglo
ms.openlocfilehash: edbb64c08f7d9edf3c76e23e0cc7e14c0125d697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="c871e-103">Machine Learning modellerini programlı olarak yeniden eğitme</span><span class="sxs-lookup"><span data-stu-id="c871e-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="c871e-104">Bu kılavuzda, tooprogrammatically bir Azure Machine Learning Web hizmeti C# ve makine öğrenme toplu yürütme hizmeti hello kullanarak nasıl yeniden eğitme öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c871e-104">In this walkthrough, you will learn how tooprogrammatically retrain an Azure Machine Learning Web Service using C# and hello Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="c871e-105">Merhaba modeli retrained sonra izlenecek yollar aşağıdaki hello nasıl tooupdate hello Tahmine dayalı web hizmetiniz modelinde göster:</span><span class="sxs-lookup"><span data-stu-id="c871e-105">Once you have retrained hello model, hello following walkthroughs show how tooupdate hello model in your predictive web service:</span></span>

* <span data-ttu-id="c871e-106">Merhaba Machine Learning Web Hizmetleri portalında bir Klasik web hizmeti dağıttıysanız bkz [bir Klasik web hizmeti yeniden eğitme](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="c871e-106">If you deployed a Classic web service in hello Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="c871e-107">Yeni bir web hizmetini dağıttıysanız bkz [hello makine öğrenme yönetimi cmdlet'lerini kullanarak yeni bir web hizmeti yeniden eğitme](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c871e-107">If you deployed a New web service, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="c871e-108">İşlemi yeniden eğitme hello genel bakış için bkz: [makine öğrenimi modeline yeniden eğitme](machine-learning-retrain-machine-learning-model.md).</span><span class="sxs-lookup"><span data-stu-id="c871e-108">For an overview of hello retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="c871e-109">Yeni Azure Resource Manager web hizmeti bağlı olarak, var olan toostart istiyorsanız, bkz: [var olan bir Tahmine dayalı web hizmetini yeniden eğitme](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="c871e-109">If you want toostart with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="c871e-110">Eğitim denemenizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c871e-110">Create a training experiment</span></span>
<span data-ttu-id="c871e-111">Bu örnek için kullanacağınız "örnek 5: Eğitimi, Test, değerlendir ikili sınıflandırma: yetişkinlere yönelik veri kümesi" Merhaba Microsoft Azure Machine Learning örnekleri gelen.</span><span class="sxs-lookup"><span data-stu-id="c871e-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from hello Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="c871e-112">toocreate hello deneme:</span><span class="sxs-lookup"><span data-stu-id="c871e-112">toocreate hello experiment:</span></span>

1. <span data-ttu-id="c871e-113">Azure Machine Learning Studio tooMicrosoft oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c871e-113">Sign into tooMicrosoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="c871e-114">Merhaba üzerinde hello panosunu sağ alt köşesindeki, tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="c871e-114">On hello bottom right corner of hello dashboard, click **New**.</span></span>
3. <span data-ttu-id="c871e-115">Microsoft Samples Hello örnek 5'i seçin.</span><span class="sxs-lookup"><span data-stu-id="c871e-115">From hello Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="c871e-116">Merhaba deneme tuvalinin hello üstündeki toorename hello denemeyi hello deneme adını seçin "örnek 5: Eğitimi, Test, değerlendir ikili sınıflandırma: yetişkinlere yönelik veri kümesi".</span><span class="sxs-lookup"><span data-stu-id="c871e-116">toorename hello experiment, at hello top of hello experiment canvas, select hello experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="c871e-117">Tür Census modeli.</span><span class="sxs-lookup"><span data-stu-id="c871e-117">Type Census Model.</span></span>
6. <span data-ttu-id="c871e-118">Merhaba deneme tuvalinin Hello altındaki tıklatın **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="c871e-118">At hello bottom of hello experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="c871e-119">Tıklatın **Ayarla web hizmeti** seçip **web hizmeti yeniden eğitme**.</span><span class="sxs-lookup"><span data-stu-id="c871e-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="c871e-120">Merhaba aşağıdaki hello ilk deneme gösterir.</span><span class="sxs-lookup"><span data-stu-id="c871e-120">hello following shows hello initial experiment.</span></span>
   
   ![İlk deneme.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="c871e-122">Tahmine dayalı bir deneme oluşturma ve bir web hizmeti olarak Yayımla</span><span class="sxs-lookup"><span data-stu-id="c871e-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="c871e-123">Ardından bir Predicative deneme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c871e-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="c871e-124">Merhaba deneme tuvalinin Hello altındaki tıklatın **Web hizmetinin ayarı** seçip **Tahmine dayalı Web hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="c871e-124">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="c871e-125">Bu hello modeli eğitilen Model olarak kaydeder ve web hizmeti giriş ve çıkış modülleri ekler.</span><span class="sxs-lookup"><span data-stu-id="c871e-125">This saves hello model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="c871e-126">**Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c871e-126">Click **Run**.</span></span> 
3. <span data-ttu-id="c871e-127">Merhaba deneme çalışması bittikten sonra tıklatın **Web hizmeti Dağıt [Klasik]** veya **Web hizmeti dağıtma [Yeni]**.</span><span class="sxs-lookup"><span data-stu-id="c871e-127">After hello experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="c871e-128">toodeploy yeni bir web hizmeti yeterli izniniz hello abonelik toowhich, hello web Hizmeti'ni dağıtma olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c871e-128">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="c871e-129">Daha fazla bilgi için [hello Azure Machine Learning Web Hizmetleri portalı kullanarak bir Web hizmeti yönetmek](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="c871e-129">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-hello-training-experiment-as-a-training-web-service"></a><span data-ttu-id="c871e-130">Merhaba eğitim denemenizi eğitim web hizmeti olarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="c871e-130">Deploy hello training experiment as a Training web service</span></span>
<span data-ttu-id="c871e-131">tooretrain hello eğitilen model, Retraining web hizmeti olarak oluşturulan hello eğitim denemenizi dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c871e-131">tooretrain hello trained model, you must deploy hello training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="c871e-132">Bu web hizmeti gereken bir *Web hizmeti çıkış* modülü bağlı toohello  *[Train Model] [ train-model]*  modülü, toobe mümkün tooproduce yeni eğitilmiş modeller.</span><span class="sxs-lookup"><span data-stu-id="c871e-132">This web service needs a *Web Service Output* module connected toohello *[Train Model][train-model]* module, toobe able tooproduce new trained models.</span></span>

1. <span data-ttu-id="c871e-133">tooreturn toohello eğitim denemenizi hello sol bölmesinde hello denemeler simgesine tıklayın, sonra Census modeli adlı hello denemeye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c871e-133">tooreturn toohello training experiment, click hello Experiments icon in hello left pane, then click hello experiment named Census Model.</span></span>  
2. <span data-ttu-id="c871e-134">Web hizmeti Hello arama deneme öğeleri arama kutusuna yazın.</span><span class="sxs-lookup"><span data-stu-id="c871e-134">In hello Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="c871e-135">Sürükleme bir *Web hizmeti girişi* hello modülü tuvale denemek ve çıktı toohello bağlanmak *Clean Missing Data* modülü.</span><span class="sxs-lookup"><span data-stu-id="c871e-135">Drag a *Web Service Input* module onto hello experiment canvas and connect its output toohello *Clean Missing Data* module.</span></span>  <span data-ttu-id="c871e-136">Bu yeniden eğitme verilerinizi işlenir sağlar aynı hello özgün eğitim verilerinizi şekilde.</span><span class="sxs-lookup"><span data-stu-id="c871e-136">This ensures that your retraining data is processed hello same way as your original training data.</span></span>
4. <span data-ttu-id="c871e-137">İki *web hizmeti çıkış* hello üzerine modülleri deneme tuvaline.</span><span class="sxs-lookup"><span data-stu-id="c871e-137">Drag two *web service Output* modules onto hello experiment canvas.</span></span> <span data-ttu-id="c871e-138">Merhaba Hello çıkışına bağlayın *Train Model* hello modülü tooone ve hello çıktısı *Evaluate Model* toohello modülü diğer.</span><span class="sxs-lookup"><span data-stu-id="c871e-138">Connect hello output of hello *Train Model* module tooone and hello output of hello *Evaluate Model* module toohello other.</span></span> <span data-ttu-id="c871e-139">Merhaba için web hizmeti çıkış **Train Model** bize hello yeni eğitilen modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="c871e-139">hello web service output for **Train Model** gives us hello new trained model.</span></span> <span data-ttu-id="c871e-140">Merhaba çok bağlı çıktı**Evaluate Model** bu modül çıkış, hangi hello performans sonuçlarını döndürür.</span><span class="sxs-lookup"><span data-stu-id="c871e-140">hello output attached too**Evaluate Model** returns that module’s output, which is hello performance results.</span></span>
5. <span data-ttu-id="c871e-141">**Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c871e-141">Click **Run**.</span></span> 

<span data-ttu-id="c871e-142">Sonraki hello eğitim denemenizi eğitilen bir modelin ve model değerlendirme sonuçlarını üreten bir web hizmeti olarak dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c871e-142">Next you must deploy hello training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="c871e-143">Bu, sonraki kümenizi Eylemler, Klasik web hizmeti veya yeni bir web hizmeti ile çalışma hakkında bağımlı tooaccomplish.</span><span class="sxs-lookup"><span data-stu-id="c871e-143">tooaccomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="c871e-144">**Klasik web hizmeti**</span><span class="sxs-lookup"><span data-stu-id="c871e-144">**Classic web service**</span></span>

<span data-ttu-id="c871e-145">Merhaba deneme tuvalinin Hello altındaki tıklatın **Web hizmetinin ayarı** seçip **Web hizmeti Dağıt [Klasik]**.</span><span class="sxs-lookup"><span data-stu-id="c871e-145">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="c871e-146">Merhaba Web hizmeti **Pano** için toplu iş yürütme hello API anahtarı ve hello API Yardım sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c871e-146">hello Web Service **Dashboard** is displayed with hello API Key and hello API help page for Batch Execution.</span></span> <span data-ttu-id="c871e-147">Yalnızca hello toplu iş yürütme yöntemi, eğitilmiş modeller oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c871e-147">Only hello Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="c871e-148">**Yeni web hizmeti**</span><span class="sxs-lookup"><span data-stu-id="c871e-148">**New web service**</span></span>

<span data-ttu-id="c871e-149">Merhaba deneme tuvalinin Hello altındaki tıklatın **Web hizmetinin ayarı** seçip **Web hizmeti dağıtma [Yeni]**.</span><span class="sxs-lookup"><span data-stu-id="c871e-149">At hello bottom of hello experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="c871e-150">Merhaba Web hizmeti Azure Machine Learning Web Hizmetleri portalı toohello dağıtma web hizmeti sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="c871e-150">hello Web Service Azure Machine Learning Web Services portal opens toohello Deploy web service page.</span></span> <span data-ttu-id="c871e-151">Web hizmetiniz için bir ad yazın ve ödeme planı seçin ve ardından **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="c871e-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="c871e-152">Yalnızca hello toplu iş yürütme yöntemi eğitilmiş modeller oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c871e-152">Only hello Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="c871e-153">Tamamlanan çalışan deneme sahip olduktan sonra her iki durumda da hello elde edilen iş akışı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="c871e-153">In either case, after experiment has completed running, hello resulting workflow should look as follows:</span></span>

![Çalıştırdıktan sonra elde edilen iş akışı.][4]



## <a name="retrain-hello-model-with-new-data-using-bes"></a><span data-ttu-id="c871e-155">Merhaba modeli BES kullanarak yeni verilerle yeniden eğitme</span><span class="sxs-lookup"><span data-stu-id="c871e-155">Retrain hello model with new data using BES</span></span>
<span data-ttu-id="c871e-156">Bu örnekte, toocreate uygulama yeniden eğitme C# hello kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="c871e-156">For this example, you are using C# toocreate hello retraining application.</span></span> <span data-ttu-id="c871e-157">Bu görev hello Python veya R örnek kodu tooaccomplish de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c871e-157">You can also use hello Python or R sample code tooaccomplish this task.</span></span>

<span data-ttu-id="c871e-158">toocall yeniden eğitme API'lerini hello:</span><span class="sxs-lookup"><span data-stu-id="c871e-158">toocall hello Retraining APIs:</span></span>

1. <span data-ttu-id="c871e-159">Visual Studio'da bir C# konsol uygulaması oluşturun: **yeni** > **proje** > **Visual C#** > **Windows Klasik Masaüstü** > **konsol uygulaması (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="c871e-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="c871e-160">İçinde toohello Machine Learning Web hizmeti portalı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c871e-160">Sign in toohello Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="c871e-161">Klasik web hizmeti ile çalışıyorsanız, tıklatın **Klasik Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="c871e-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="c871e-162">Birlikte çalıştığınız hello web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c871e-162">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="c871e-163">Merhaba varsayılan uç noktasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c871e-163">Click hello default endpoint.</span></span>
   3. <span data-ttu-id="c871e-164">Tıklatın **tüketen**.</span><span class="sxs-lookup"><span data-stu-id="c871e-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="c871e-165">Merhaba hello sonundaki **Tüket** sayfasında hello **örnek kod** 'yi tıklatın **toplu**.</span><span class="sxs-lookup"><span data-stu-id="c871e-165">At hello bottom of hello **Consume** page, in hello **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="c871e-166">Bu yordamın 5 toostep devam edin.</span><span class="sxs-lookup"><span data-stu-id="c871e-166">Continue toostep 5 of this procedure.</span></span>
4. <span data-ttu-id="c871e-167">Yeni bir web hizmeti ile çalışıyorsanız, tıklatın **Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="c871e-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="c871e-168">Birlikte çalıştığınız hello web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c871e-168">Click hello web service you are working with.</span></span>
   2. <span data-ttu-id="c871e-169">Tıklatın **tüketen**.</span><span class="sxs-lookup"><span data-stu-id="c871e-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="c871e-170">Merhaba de hello Tüket sayfasında hello sonundaki **örnek kod** 'yi tıklatın **toplu**.</span><span class="sxs-lookup"><span data-stu-id="c871e-170">At hello bottom of hello Consume page, in hello **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="c871e-171">Toplu iş yürütme Hello örnek C# kodu kopyalayın ve hello ad olduğu gibi kalır emin hello Program.cs dosyasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="c871e-171">Copy hello sample C# code for batch execution and paste it into hello Program.cs file, making sure hello namespace remains intact.</span></span>

<span data-ttu-id="c871e-172">Merhaba açıklamaları belirtildiği gibi Hello Nuget paketini Microsoft.AspNet.WebApi.Client ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c871e-172">Add hello Nuget package Microsoft.AspNet.WebApi.Client as specified in hello comments.</span></span> <span data-ttu-id="c871e-173">tooadd hello başvuru tooMicrosoft.WindowsAzure.Storage.dll, Microsoft Azure depolama hizmetleri için tooinstall hello istemci kitaplığı ilk gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c871e-173">tooadd hello reference tooMicrosoft.WindowsAzure.Storage.dll, you might first need tooinstall hello client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="c871e-174">Daha fazla bilgi için bkz: [Windows depolama hizmetleri](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="c871e-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-hello-apikey-declaration"></a><span data-ttu-id="c871e-175">Merhaba apikey ile yapılan bildirimini güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="c871e-175">Update hello apikey declaration</span></span>
<span data-ttu-id="c871e-176">Merhaba bulun **apikey ile yapılan** bildirimi.</span><span class="sxs-lookup"><span data-stu-id="c871e-176">Locate hello **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with hello API key for hello web service

<span data-ttu-id="c871e-177">Merhaba, **temel tüketim bilgileri** hello bölümünü **Tüket** sayfasında hello birincil anahtarını bulun ve toohello kopyalama **apikey ile yapılan** bildirimi.</span><span class="sxs-lookup"><span data-stu-id="c871e-177">In hello **Basic consumption info** section of hello **Consume** page, locate hello primary key and copy it toohello **apikey** declaration.</span></span>

### <a name="update-hello-azure-storage-information"></a><span data-ttu-id="c871e-178">Hello Azure depolama bilgilerini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="c871e-178">Update hello Azure Storage information</span></span>
<span data-ttu-id="c871e-179">Merhaba BES örnek kod (örneğin "C:\temp\CensusIpnput.csv") yerel sürücü tooAzure depolama bir dosyadan yükler, işler ve hello sonuçları geri tooAzure depolama yazar.</span><span class="sxs-lookup"><span data-stu-id="c871e-179">hello BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") tooAzure Storage, processes it, and writes hello results back tooAzure Storage.</span></span>  

<span data-ttu-id="c871e-180">tooaccomplish bu görev için depolama hesabınızdan hello Klasik Azure portalı ve değerlerini hello kod içinde karşılık gelen hello güncelleştirme Merhaba, depolama hesabı adı, anahtar ve kapsayıcı bilgi almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c871e-180">tooaccomplish this task, you must retrieve hello Storage account name, key, and container information for your Storage account from hello classic Azure portal and hello update corresponding values in hello code.</span></span> 

1. <span data-ttu-id="c871e-181">Toohello Klasik Azure Portalı'nda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c871e-181">Sign in toohello classic Azure portal.</span></span>
2. <span data-ttu-id="c871e-182">Merhaba sol gezinti sütununda **depolama**.</span><span class="sxs-lookup"><span data-stu-id="c871e-182">In hello left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="c871e-183">Depolama hesapları Hello listeden seçim bir toostore hello modeli retrained.</span><span class="sxs-lookup"><span data-stu-id="c871e-183">From hello list of storage accounts, select one toostore hello retrained model.</span></span>
4. <span data-ttu-id="c871e-184">Merhaba sayfasının Hello altında tıklatın **erişim anahtarlarını Yönet**.</span><span class="sxs-lookup"><span data-stu-id="c871e-184">At hello bottom of hello page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="c871e-185">Kopyalayın ve hello kaydedin **birincil erişim anahtarını** ve Kapat hello iletişim.</span><span class="sxs-lookup"><span data-stu-id="c871e-185">Copy and save hello **Primary Access Key** and close hello dialog.</span></span> 
6. <span data-ttu-id="c871e-186">Merhaba hello sayfanın en üstünde, tıklatın **kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="c871e-186">At hello top of hello page, click **Containers**.</span></span>
7. <span data-ttu-id="c871e-187">Var olan bir kapsayıcı seçin veya yeni bir tane oluşturun ve hello adı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c871e-187">Select an existing container or create a new one and save hello name.</span></span>

<span data-ttu-id="c871e-188">Merhaba bulun *StorageAccountName*, *StorageAccountKey*, ve *StorageContainerName* bildirimler ve güncelleştirme hello değerleri, kaydettiğiniz hello Azure portalı.</span><span class="sxs-lookup"><span data-stu-id="c871e-188">Locate hello *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update hello values you saved from hello Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="c871e-189">Ayrıca, hello giriş dosyası, hello kodda belirtme hello konumda kullanılabilir olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="c871e-189">You also must ensure hello input file is available at hello location you specify in hello code.</span></span> 

### <a name="specify-hello-output-location"></a><span data-ttu-id="c871e-190">Merhaba çıkış konumunu belirtin</span><span class="sxs-lookup"><span data-stu-id="c871e-190">Specify hello output location</span></span>
<span data-ttu-id="c871e-191">Merhaba çıkış konumu hello Request yükü belirtirken, belirtilen hello dosyasının uzantısını hello *RelativeLocation* ilearner belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="c871e-191">When specifying hello output location in hello Request Payload, hello extension of hello file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="c871e-192">Aşağıdaki örnek hello bakın:</span><span class="sxs-lookup"><span data-stu-id="c871e-192">See hello following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with hello location you would like toouse for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="c871e-193">Çıktı konumlarınıza Hello adlarını olanları bu kılavuzda hello web hizmeti çıkış modülleri eklenen hello siparişi temel alarak hello farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c871e-193">hello names of your output locations may be different from hello ones in this walkthrough based on hello order in which you added hello web service output modules.</span></span> <span data-ttu-id="c871e-194">Bu eğitim denemenizi iki çıkışları ile ayarlama beri hello sonuçları her ikisi için depolama konumu bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="c871e-194">Since you set up this training experiment with two outputs, hello results include storage location information for both of them.</span></span>  
> 
> 

![Çıktı yeniden eğitme][6]

<span data-ttu-id="c871e-196">Diyagram 4: çıkış yeniden eğitme.</span><span class="sxs-lookup"><span data-stu-id="c871e-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-hello-retraining-results"></a><span data-ttu-id="c871e-197">Merhaba yeniden eğitme sonuçları değerlendirin</span><span class="sxs-lookup"><span data-stu-id="c871e-197">Evaluate hello Retraining Results</span></span>
<span data-ttu-id="c871e-198">Merhaba uygulamayı çalıştırdığınızda, SAS belirteci gerekli tooaccess değerlendirme sonuçlarını hello ve hello çıktı hello URL içerir.</span><span class="sxs-lookup"><span data-stu-id="c871e-198">When you run hello application, hello output includes hello URL and SAS token necessary tooaccess hello evaluation results.</span></span>

<span data-ttu-id="c871e-199">Merhaba birleştirerek retrained hello modelinin hello performans sonuçlarını görebilirsiniz *BaseLocation*, *RelativeLocation*, ve *SasBlobToken* hello çıkış sonuçlarından için *output2* (Merhaba çıktı görüntü yeniden eğitme önceki gösterildiği gibi) ve hello tam URL hello tarayıcınızın adres çubuğuna yapıştırma.</span><span class="sxs-lookup"><span data-stu-id="c871e-199">You can see hello performance results of hello retrained model by combining hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results for *output2* (as shown in hello preceding retraining output image) and pasting hello complete URL in hello browser address bar.</span></span>  

<span data-ttu-id="c871e-200">Merhaba yeni eğitilen model bir varolan iyi yeterli tooreplace hello gerçekleştiğini hello sonuçları toodetermine inceleyin.</span><span class="sxs-lookup"><span data-stu-id="c871e-200">Examine hello results toodetermine whether hello newly trained model performs well enough tooreplace hello existing one.</span></span>

<span data-ttu-id="c871e-201">Kopya hello *BaseLocation*, *RelativeLocation*, ve *SasBlobToken* hello çıkış sonuçlarından, bunları işlem yeniden eğitme hello sırasında kullanın.</span><span class="sxs-lookup"><span data-stu-id="c871e-201">Copy hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from hello output results, you will use them during hello retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c871e-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c871e-202">Next steps</span></span>
<span data-ttu-id="c871e-203">Tıklayarak hello Tahmine dayalı web hizmetini dağıttıysanız **Web hizmeti Dağıt [Klasik]**, bkz: [bir Klasik web hizmeti yeniden eğitme](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="c871e-203">If you deployed hello predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="c871e-204">Tıklayarak hello Tahmine dayalı web hizmetini dağıttıysanız **Web hizmeti dağıtma [Yeni]**, bkz: [hello makine öğrenme yönetimi cmdlet'lerini kullanarak yeni bir web hizmeti yeniden eğitme](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c871e-204">If you deployed hello predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using hello Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using hello Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
