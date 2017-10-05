---
title: "Machine Learning modellerini program aracılığıyla yeniden eğitme | Microsoft Docs"
description: "Program aracılığıyla bir modeli yeniden eğitme ve Azure Machine Learning ile yeni eğitilen modelini kullanmak için web hizmetini güncelleştirmek hakkında bilgi edinin."
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
ms.openlocfilehash: cf7a39e14a935d0d0e0df07e66a8f37480ec9687
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="aaa1c-103">Machine Learning modellerini programlı olarak yeniden eğitme</span><span class="sxs-lookup"><span data-stu-id="aaa1c-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="aaa1c-104">Bu kılavuzda, bir Azure Machine Learning Web hizmeti C# ve makine öğrenme toplu yürütme hizmeti kullanarak program aracılığıyla yeniden eğitme öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-104">In this walkthrough, you will learn how to programmatically retrain an Azure Machine Learning Web Service using C# and the Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="aaa1c-105">Model retrained sonra aşağıdaki izlenecek Tahmine dayalı web hizmetiniz modelinde güncelleştirmek nasıl göster:</span><span class="sxs-lookup"><span data-stu-id="aaa1c-105">Once you have retrained the model, the following walkthroughs show how to update the model in your predictive web service:</span></span>

* <span data-ttu-id="aaa1c-106">Machine Learning Web Hizmetleri portalında bir Klasik web hizmeti dağıttıysanız bkz [bir Klasik web hizmeti yeniden eğitme](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="aaa1c-106">If you deployed a Classic web service in the Machine Learning Web Services portal, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="aaa1c-107">Yeni bir web hizmetini dağıttıysanız bkz [makine öğrenme yönetimi cmdlet'lerini kullanarak yeni bir web hizmeti yeniden eğitme](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="aaa1c-107">If you deployed a New web service, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="aaa1c-108">Yeniden eğitme işlemine genel bakış için bkz: [makine öğrenimi modeline yeniden eğitme](machine-learning-retrain-machine-learning-model.md).</span><span class="sxs-lookup"><span data-stu-id="aaa1c-108">For an overview of the retraining process, see [Retrain a Machine Learning Model](machine-learning-retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="aaa1c-109">Mevcut yeni Azure Resource Manager temelli web hizmetiniz ile başlatmak istiyorsanız, bkz: [var olan bir Tahmine dayalı web hizmetini yeniden eğitme](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="aaa1c-109">If you want to start with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](machine-learning-retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="aaa1c-110">Eğitim denemenizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="aaa1c-110">Create a training experiment</span></span>
<span data-ttu-id="aaa1c-111">Bu örnek için kullanacağınız "örnek 5: Eğitimi, Test, değerlendir ikili sınıflandırma: yetişkinlere yönelik veri kümesi" Microsoft Azure Machine Learning örnekleri gelen.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from the Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="aaa1c-112">Deneme oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="aaa1c-112">To create the experiment:</span></span>

1. <span data-ttu-id="aaa1c-113">Oturum açın Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-113">Sign into to Microsoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="aaa1c-114">Üzerinde Pano sağ alt köşesindeki, tıklatın **yeni**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-114">On the bottom right corner of the dashboard, click **New**.</span></span>
3. <span data-ttu-id="aaa1c-115">Microsoft Samples örnek 5'i seçin.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-115">From the Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="aaa1c-116">Deneme tuvalinin üstündeki denemeyi yeniden adlandırmak için deneme adını seçin "örnek 5: Eğitimi, Test, değerlendir ikili sınıflandırma: yetişkinlere yönelik veri kümesi".</span><span class="sxs-lookup"><span data-stu-id="aaa1c-116">To rename the experiment, at the top of the experiment canvas, select the experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="aaa1c-117">Tür Census modeli.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-117">Type Census Model.</span></span>
6. <span data-ttu-id="aaa1c-118">Deneme tuvalinin altındaki tıklatın **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-118">At the bottom of the experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="aaa1c-119">Tıklatın **Ayarla web hizmeti** seçip **web hizmeti yeniden eğitme**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="aaa1c-120">İlk deneme gösterir.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-120">The following shows the initial experiment.</span></span>
   
   ![İlk deneme.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="aaa1c-122">Tahmine dayalı bir deneme oluşturma ve bir web hizmeti olarak Yayımla</span><span class="sxs-lookup"><span data-stu-id="aaa1c-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="aaa1c-123">Ardından bir Predicative deneme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="aaa1c-124">Deneme tuvalinin altındaki tıklatın **Web hizmetinin ayarı** seçip **Tahmine dayalı Web hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-124">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="aaa1c-125">Bu model eğitilen Model olarak kaydeder ve web hizmeti giriş ve çıkış modülleri ekler.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-125">This saves the model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="aaa1c-126">**Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-126">Click **Run**.</span></span> 
3. <span data-ttu-id="aaa1c-127">Denemeyi çalışması bittikten sonra tıklatın **Web hizmeti Dağıt [Klasik]** veya **Web hizmeti dağıtma [Yeni]**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-127">After the experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="aaa1c-128">Yeni bir web hizmeti dağıtmak için yeterli izinleri olan Abonelikteki, web hizmetini dağıtma olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-128">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="aaa1c-129">Daha fazla bilgi için [Azure Machine Learning Web Hizmetleri Portalı'nı kullanarak bir Web hizmetini yönetmek](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="aaa1c-129">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

## <a name="deploy-the-training-experiment-as-a-training-web-service"></a><span data-ttu-id="aaa1c-130">Eğitim denemenizi eğitim web hizmeti olarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="aaa1c-130">Deploy the training experiment as a Training web service</span></span>
<span data-ttu-id="aaa1c-131">Eğitim modeli yeniden eğitme Retraining web hizmeti olarak oluşturulan eğitim denemenizi dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-131">To retrain the trained model, you must deploy the training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="aaa1c-132">Bu web hizmeti gereken bir *Web hizmeti çıkış* bağlı Modülü  *[Train Model] [ train-model]*  yeni üretmek için modülü, eğitilmiş modeller.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-132">This web service needs a *Web Service Output* module connected to the *[Train Model][train-model]* module, to be able to produce new trained models.</span></span>

1. <span data-ttu-id="aaa1c-133">Eğitim denemenizi dönmek için sol bölmede denemeler simgesini tıklatın, sonra Census modeli adlı denemeye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-133">To return to the training experiment, click the Experiments icon in the left pane, then click the experiment named Census Model.</span></span>  
2. <span data-ttu-id="aaa1c-134">Web hizmeti arama deneme öğeleri arama kutusuna yazın.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-134">In the Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="aaa1c-135">Sürükleme bir *Web hizmeti girişi* deneme modülü tuvale ve çıktısını için bağlanmak *Clean Missing Data* modülü.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-135">Drag a *Web Service Input* module onto the experiment canvas and connect its output to the *Clean Missing Data* module.</span></span>  <span data-ttu-id="aaa1c-136">Bu yeniden eğitme verilerinizi özgün eğitim verilerinizi aynı şekilde işlenir sağlar.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-136">This ensures that your retraining data is processed the same way as your original training data.</span></span>
4. <span data-ttu-id="aaa1c-137">İki *web hizmeti çıkış* deneme tuvale modüller.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-137">Drag two *web service Output* modules onto the experiment canvas.</span></span> <span data-ttu-id="aaa1c-138">Çıkışına bağlayın *Train Model* biri ve çıktısını modülüne *Evaluate Model* diğer modülü.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-138">Connect the output of the *Train Model* module to one and the output of the *Evaluate Model* module to the other.</span></span> <span data-ttu-id="aaa1c-139">İçin web hizmeti çıktı **Train Model** bize yeni eğitilen modeli sağlar.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-139">The web service output for **Train Model** gives us the new trained model.</span></span> <span data-ttu-id="aaa1c-140">Çıktı bağlı **Evaluate Model** bu modül animasyonun çıktı, performans sonuçları olduğu döndürür.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-140">The output attached to **Evaluate Model** returns that module’s output, which is the performance results.</span></span>
5. <span data-ttu-id="aaa1c-141">**Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-141">Click **Run**.</span></span> 

<span data-ttu-id="aaa1c-142">Sonraki eğitim denemenizi eğitilen bir modelin ve model değerlendirme sonuçlarını üreten bir web hizmeti olarak dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-142">Next you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="aaa1c-143">Bunu başarmak için sonraki eylemler kümesidir, Klasik web hizmeti veya yeni bir web hizmeti ile çalışma hakkında bağımlı.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-143">To accomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="aaa1c-144">**Klasik web hizmeti**</span><span class="sxs-lookup"><span data-stu-id="aaa1c-144">**Classic web service**</span></span>

<span data-ttu-id="aaa1c-145">Deneme tuvalinin altındaki tıklatın **Web hizmetinin ayarı** seçip **Web hizmeti Dağıt [Klasik]**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-145">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="aaa1c-146">Web hizmeti **Pano** toplu iş yürütme için API anahtarı ve API Yardım sayfası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-146">The Web Service **Dashboard** is displayed with the API Key and the API help page for Batch Execution.</span></span> <span data-ttu-id="aaa1c-147">Yalnızca toplu iş yürütme yöntemi, eğitilmiş modeller oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-147">Only the Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="aaa1c-148">**Yeni web hizmeti**</span><span class="sxs-lookup"><span data-stu-id="aaa1c-148">**New web service**</span></span>

<span data-ttu-id="aaa1c-149">Deneme tuvalinin altındaki tıklatın **Web hizmetinin ayarı** seçip **Web hizmeti dağıtma [Yeni]**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-149">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="aaa1c-150">Web hizmeti Azure Machine Learning Web Hizmetleri Portalı'nı dağıtma web hizmeti sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-150">The Web Service Azure Machine Learning Web Services portal opens to the Deploy web service page.</span></span> <span data-ttu-id="aaa1c-151">Web hizmetiniz için bir ad yazın ve ödeme planı seçin ve ardından **dağıtma**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="aaa1c-152">Yalnızca toplu iş yürütme yöntemi eğitilmiş modeller oluşturmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-152">Only the Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="aaa1c-153">Deneme çalışması, tamamlandıktan sonra her iki durumda da, sonuçta elde edilen iş akışı şu şekilde görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="aaa1c-153">In either case, after experiment has completed running, the resulting workflow should look as follows:</span></span>

![Çalıştırdıktan sonra elde edilen iş akışı.][4]



## <a name="retrain-the-model-with-new-data-using-bes"></a><span data-ttu-id="aaa1c-155">Model BES kullanarak yeni verilerle yeniden eğitme</span><span class="sxs-lookup"><span data-stu-id="aaa1c-155">Retrain the model with new data using BES</span></span>
<span data-ttu-id="aaa1c-156">Bu örnekte, C# yeniden eğitme uygulaması oluşturmak için kullandığınız.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-156">For this example, you are using C# to create the retraining application.</span></span> <span data-ttu-id="aaa1c-157">Python veya R örnek kod, bu görevi gerçekleştirmek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-157">You can also use the Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="aaa1c-158">Yeniden eğitme API'lerini çağırmak için:</span><span class="sxs-lookup"><span data-stu-id="aaa1c-158">To call the Retraining APIs:</span></span>

1. <span data-ttu-id="aaa1c-159">Visual Studio'da bir C# konsol uygulaması oluşturun: **yeni** > **proje** > **Visual C#** > **Windows Klasik Masaüstü** > **konsol uygulaması (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="aaa1c-160">Machine Learning Web hizmeti portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-160">Sign in to the Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="aaa1c-161">Klasik web hizmeti ile çalışıyorsanız, tıklatın **Klasik Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="aaa1c-162">Çalıştığınız web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-162">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="aaa1c-163">Varsayılan uç noktasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-163">Click the default endpoint.</span></span>
   3. <span data-ttu-id="aaa1c-164">Tıklatın **tüketen**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="aaa1c-165">Ekranın alt kısmındaki **Tüket** sayfasında **örnek kod** 'yi tıklatın **toplu**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-165">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="aaa1c-166">Bu yordamın 5 adıma geçin.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-166">Continue to step 5 of this procedure.</span></span>
4. <span data-ttu-id="aaa1c-167">Yeni bir web hizmeti ile çalışıyorsanız, tıklatın **Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="aaa1c-168">Çalıştığınız web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-168">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="aaa1c-169">Tıklatın **tüketen**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="aaa1c-170">AT Tüket alt sayfası, buna **örnek kod** 'yi tıklatın **toplu**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-170">At the bottom of the Consume page, in the **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="aaa1c-171">Toplu iş yürütme için örnek C# kodu kopyalayın ve ad alanı olduğu gibi kalır emin Program.cs dosyasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-171">Copy the sample C# code for batch execution and paste it into the Program.cs file, making sure the namespace remains intact.</span></span>

<span data-ttu-id="aaa1c-172">Açıklamaları belirtildiği gibi Microsoft.AspNet.WebApi.Client Nuget paketini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-172">Add the Nuget package Microsoft.AspNet.WebApi.Client as specified in the comments.</span></span> <span data-ttu-id="aaa1c-173">Microsoft.WindowsAzure.Storage.dll başvuru eklemek için önce Microsoft Azure depolama hizmetleri için istemci kitaplığı yüklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-173">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="aaa1c-174">Daha fazla bilgi için bkz: [Windows depolama hizmetleri](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="aaa1c-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="aaa1c-175">Apikey ile yapılan bildirimini güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="aaa1c-175">Update the apikey declaration</span></span>
<span data-ttu-id="aaa1c-176">Bulun **apikey ile yapılan** bildirimi.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-176">Locate the **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="aaa1c-177">İçinde **temel tüketim bilgileri** bölümünü **Tüket** sayfasında, birincil anahtarını bulun ve kopyalayın **apikey ile yapılan** bildirimi.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-177">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="aaa1c-178">Azure depolama bilgilerini güncelleştir</span><span class="sxs-lookup"><span data-stu-id="aaa1c-178">Update the Azure Storage information</span></span>
<span data-ttu-id="aaa1c-179">BES örnek kod (örneğin "C:\temp\CensusIpnput.csv") yerel bir sürücüden bir dosyayı Azure Storage'a yükler, işler ve sonuçları Azure depolama birimine geri yazar.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-179">The BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="aaa1c-180">Bu görevi gerçekleştirmek için depolama hesabınızdan Klasik Azure portalı ve kodunda güncelleştirme karşılık gelen değerler için depolama hesabı adı, anahtar ve kapsayıcı bilgi almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-180">To accomplish this task, you must retrieve the Storage account name, key, and container information for your Storage account from the classic Azure portal and the update corresponding values in the code.</span></span> 

1. <span data-ttu-id="aaa1c-181">Klasik Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-181">Sign in to the classic Azure portal.</span></span>
2. <span data-ttu-id="aaa1c-182">Sol gezinti sütununda tıklatın **depolama**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-182">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="aaa1c-183">Depolama hesapları listesinden bir retrained modelini depolamak için seçin.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-183">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="aaa1c-184">Sayfanın alt kısmındaki tıklatın **erişim anahtarlarını Yönet**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-184">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="aaa1c-185">Kopyalayıp kaydedin **birincil erişim anahtarını** ve iletişim kutusunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-185">Copy and save the **Primary Access Key** and close the dialog.</span></span> 
6. <span data-ttu-id="aaa1c-186">Sayfanın üstündeki **kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-186">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="aaa1c-187">Var olan bir kapsayıcı seçin veya yeni bir tane oluşturun ve ad kaydedin.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-187">Select an existing container or create a new one and save the name.</span></span>

<span data-ttu-id="aaa1c-188">Bulun *StorageAccountName*, *StorageAccountKey*, ve *StorageContainerName* bildirimleri ve Azure portalından kaydettiğiniz değerlerini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-188">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update the values you saved from the Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="aaa1c-189">Ayrıca, girdi dosyası, kodda belirttiğiniz konumda kullanılabilir olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-189">You also must ensure the input file is available at the location you specify in the code.</span></span> 

### <a name="specify-the-output-location"></a><span data-ttu-id="aaa1c-190">Çıkış konumu belirtin</span><span class="sxs-lookup"><span data-stu-id="aaa1c-190">Specify the output location</span></span>
<span data-ttu-id="aaa1c-191">Çıkış konumu istek yükünde belirtirken, dosya uzantısını belirtilen *RelativeLocation* ilearner belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-191">When specifying the output location in the Request Payload, the extension of the file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="aaa1c-192">Aşağıdaki örneğe bakın:</span><span class="sxs-lookup"><span data-stu-id="aaa1c-192">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you would like to use for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="aaa1c-193">Çıktı konumlarınıza adlarını web hizmeti çıkış modülleri eklenen sırasına göre bu kılavuzda gördüğünüzden farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-193">The names of your output locations may be different from the ones in this walkthrough based on the order in which you added the web service output modules.</span></span> <span data-ttu-id="aaa1c-194">Bu eğitim denemenizi iki çıkışları ile ayarlama olduğundan, sonuçlar her ikisi için depolama konumu bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-194">Since you set up this training experiment with two outputs, the results include storage location information for both of them.</span></span>  
> 
> 

![Çıktı yeniden eğitme][6]

<span data-ttu-id="aaa1c-196">Diyagram 4: çıkış yeniden eğitme.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="aaa1c-197">Yeniden eğitme sonuçları değerlendirin</span><span class="sxs-lookup"><span data-stu-id="aaa1c-197">Evaluate the Retraining Results</span></span>
<span data-ttu-id="aaa1c-198">Uygulamayı çalıştırdığınızda, çıktı değerlendirme sonuçlarını erişmek gerekli URL ve SAS belirteci içerir.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-198">When you run the application, the output includes the URL and SAS token necessary to access the evaluation results.</span></span>

<span data-ttu-id="aaa1c-199">Birleştirerek retrained modeli performans sonuçlarını görebilirsiniz *BaseLocation*, *RelativeLocation*, ve *SasBlobToken* içinçıktısonuçlarından*output2* (yukarıdaki yeniden eğitme çıkış görüntüde gösterildiği gibi) ve tam URL'sini tarayıcınızın adres çubuğuna yapıştırma.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-199">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL in the browser address bar.</span></span>  

<span data-ttu-id="aaa1c-200">Yeni eğitilen model yeterince iyi var olan dosyayla gerçekleştirip gerçekleştirmeyeceğini belirlemek için sonuçlarını inceleyin.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-200">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="aaa1c-201">Kopya *BaseLocation*, *RelativeLocation*, ve *SasBlobToken* çıkış sonuçlarından, bunları yeniden eğitme işlemi sırasında kullanın.</span><span class="sxs-lookup"><span data-stu-id="aaa1c-201">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results, you will use them during the retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aaa1c-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aaa1c-202">Next steps</span></span>
<span data-ttu-id="aaa1c-203">Tıklayarak Tahmine dayalı web hizmetini dağıttıysanız **Web hizmeti Dağıt [Klasik]**, bkz: [bir Klasik web hizmeti yeniden eğitme](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="aaa1c-203">If you deployed the predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="aaa1c-204">Tıklayarak Tahmine dayalı web hizmetini dağıttıysanız **Web hizmeti dağıtma [Yeni]**, bkz: [makine öğrenme yönetimi cmdlet'lerini kullanarak yeni bir web hizmeti yeniden eğitme](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="aaa1c-204">If you deployed the predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using the Machine Learning Management cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using the Machine Learning Management REST API -->


[1]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/machine-learning-retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
