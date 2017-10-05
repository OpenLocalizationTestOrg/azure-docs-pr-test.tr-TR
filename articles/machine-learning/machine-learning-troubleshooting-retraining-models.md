---
title: "Bir Klasik Azure Machine Learning web hizmetini yeniden eğitme sorunlarını giderme | Microsoft Docs"
description: "Tanımlamak ve bir Azure Machine Learning Web hizmeti için modeli yeniden eğitme, ortak sorunları aygıtındaki düzeltin."
services: machine-learning
documentationcenter: 
author: VDonGlover
manager: raymondl
editor: 
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: fc36499ebff88c86635228ff899c85e9166aabed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-the-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="0672f-103">Bir Azure Machine Learning Klasik Web hizmeti yeniden eğitme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="0672f-103">Troubleshooting the retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="0672f-104">Yeniden eğitme genel bakış</span><span class="sxs-lookup"><span data-stu-id="0672f-104">Retraining overview</span></span>
<span data-ttu-id="0672f-105">Tahmine dayalı denemeye Puanlama web hizmeti olarak dağıttığınızda statik bir modelidir.</span><span class="sxs-lookup"><span data-stu-id="0672f-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="0672f-106">Yeni veriler kullanılabilir olduğunda ya da kendi veri tüketici API varsa, model retrained gerekir.</span><span class="sxs-lookup"><span data-stu-id="0672f-106">As new data becomes available or when the consumer of the API has their own data, the model needs to be retrained.</span></span> 

<span data-ttu-id="0672f-107">Klasik Web hizmeti yeniden eğitme işlemini eksiksiz bir anlatım için bkz [yeniden eğitme Machine Learning modellerini program aracılığıyla](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="0672f-107">For a complete walkthrough of the retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="0672f-108">İşlemi yeniden eğitme</span><span class="sxs-lookup"><span data-stu-id="0672f-108">Retraining process</span></span>
<span data-ttu-id="0672f-109">Web hizmeti yeniden eğitme gerektiğinde, bazı ek parçalar eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="0672f-109">When you need to retrain the Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="0672f-110">Eğitim denemenizi dağıtılan bir Web hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="0672f-110">A Web service deployed from the Training Experiment.</span></span> <span data-ttu-id="0672f-111">Denemeyi olmalıdır bir **Web hizmeti çıkış** modülünün çıkışına bağlı **Train Model** modülü.</span><span class="sxs-lookup"><span data-stu-id="0672f-111">The experiment must have a **Web Service Output** module attached to the output of the **Train Model** module.</span></span>  
  
    ![Web hizmeti çıkış train model ekleyin.][image1]
* <span data-ttu-id="0672f-113">Puanlama Web hizmetiniz için eklenen yeni bir uç noktası.</span><span class="sxs-lookup"><span data-stu-id="0672f-113">A new endpoint added to your scoring Web service.</span></span>  <span data-ttu-id="0672f-114">Program aracılığıyla Machine Learning yeniden eğitme modellerinde program aracılığıyla başvurulan örnek kodu kullanarak uç nokta ekleme konu veya Klasik Azure Portalı aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="0672f-114">You can add the endpoint programmatically using the sample code referenced in the Retrain Machine Learning models programmatically topic or through the Azure classic portal.</span></span>

<span data-ttu-id="0672f-115">Yeniden eğitme modeli için eğitim Web hizmetinin API Yardım sayfası örnek C# kodundan sonra kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0672f-115">You can then use the sample C# code from the Training Web Service's API help page to retrain model.</span></span> <span data-ttu-id="0672f-116">Sonuçları değerlendirilen ve bunlarla memnun sonra eklediğiniz yeni uç nokta kullanarak web hizmeti Puanlama eğitilen modeli güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0672f-116">Once you have evaluated the results and are satisfied with them, you update the trained model scoring web service using the new endpoint that you added.</span></span>

<span data-ttu-id="0672f-117">Tüm parçaları ile yerinde, model yeniden eğitme için uygulamanız gereken önemli adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="0672f-117">With all the pieces in place, the major steps you must take to retrain the model are as follows:</span></span>

1. <span data-ttu-id="0672f-118">Eğitim Web hizmeti çağrısı: Toplu yürütme hizmeti (BES için), değil istek yanıtı hizmeti (RRS) çağrıdır.</span><span class="sxs-lookup"><span data-stu-id="0672f-118">Call the Training Web Service:  The call is to the Batch Execution Service (BES), not the Request Response Service (RRS).</span></span> <span data-ttu-id="0672f-119">Arama yapmak için API Yardım sayfasında örnek C# kodu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0672f-119">You can use the sample C# code on the API help page to make the call.</span></span> 
2. <span data-ttu-id="0672f-120">Değerlerini bulmak *BaseLocation*, *RelativeLocation*, ve *SasBlobToken*: Bu değerleri eğitim Web hizmetine, çağrısından çıktıda döndürülür.</span><span class="sxs-lookup"><span data-stu-id="0672f-120">Find the values for the *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in the output from your call to the Training Web Service.</span></span> 
   <span data-ttu-id="0672f-121">![yeniden eğitme örnek ve BaseLocation, RelativeLocation ve SasBlobToken değerleri çıktısını gösteriliyor.][image6]</span><span class="sxs-lookup"><span data-stu-id="0672f-121">![showing the output of the retraining sample and the BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="0672f-122">İle yeni eğitilen modeli Puanlama web hizmetinden eklenen uç noktasını güncelleyin: Machine Learning yeniden eğitme modellerinde program aracılığıyla, sağlanan örnek kodu kullanarak güncelleştirme eklediğiniz yeni eğitilen modeli Puanlama modeliyle yeni uç noktası Eğitim Web hizmeti.</span><span class="sxs-lookup"><span data-stu-id="0672f-122">Update the added endpoint from the scoring web service with the new trained model: Using the sample code provided in the Retrain Machine Learning models programmatically, update the new endpoint you added to the scoring model with the newly trained model from the Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="0672f-123">Ortak engellerini</span><span class="sxs-lookup"><span data-stu-id="0672f-123">Common obstacles</span></span>
### <a name="check-to-see-if-you-have-the-correct-patch-url"></a><span data-ttu-id="0672f-124">Düzeltme eki URL'nin doğru olup olmadığını denetleyin</span><span class="sxs-lookup"><span data-stu-id="0672f-124">Check to see if you have the correct PATCH URL</span></span>
<span data-ttu-id="0672f-125">Düzeltme eki, kullanmakta olduğunuz URL Puanlama Web hizmetine eklediğiniz yeni Puanlama uç noktasıyla ilişkili bir olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0672f-125">The PATCH URL you are using must be the one associated with the new scoring endpoint you added to the scoring Web service.</span></span> <span data-ttu-id="0672f-126">Bir düzeltme eki URL'sini elde etmek için çeşitli yöntemler vardır:</span><span class="sxs-lookup"><span data-stu-id="0672f-126">There are a number of ways to obtain the PATCH URL:</span></span>

<span data-ttu-id="0672f-127">**Seçenek 1: programlı şekilde**</span><span class="sxs-lookup"><span data-stu-id="0672f-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="0672f-128">Düzeltme eki doğru URL'yi almak için:</span><span class="sxs-lookup"><span data-stu-id="0672f-128">To get the correct PATCH URL:</span></span>

1. <span data-ttu-id="0672f-129">Çalıştırma [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) örnek kodu.</span><span class="sxs-lookup"><span data-stu-id="0672f-129">Run the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="0672f-130">AddEndpoint çıktısından Bul *HelpLocation* değer ve URL'yi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0672f-130">From the output of AddEndpoint, find the *HelpLocation* value and copy the URL.</span></span>
   
   ![HelpLocation addEndpoint örnek çıktı.][image2]
3. <span data-ttu-id="0672f-132">Web hizmeti için Yardım bağlantıları sağlayan sayfaya gitmek için bir tarayıcı URL'sini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0672f-132">Paste the URL into a browser to navigate to a page that provides help links for the Web service.</span></span>
4. <span data-ttu-id="0672f-133">Tıklatın **güncelleştirme kaynağı** düzeltme eki Yardım sayfasını açmak için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="0672f-133">Click the **Update Resource** link to open the patch help page.</span></span>

<span data-ttu-id="0672f-134">**Seçenek 2: Klasik Azure portalını kullanın**</span><span class="sxs-lookup"><span data-stu-id="0672f-134">**Option 2: Use the Azure classic portal**</span></span>

1. <span data-ttu-id="0672f-135">[Klasik Azure portalında](https://manage.windowsazure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0672f-135">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0672f-136">Machine Learning sekmesini açın.</span><span class="sxs-lookup"><span data-stu-id="0672f-136">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="0672f-137">![Makine leaning sekmesini tıklatın.][image4]</span><span class="sxs-lookup"><span data-stu-id="0672f-137">![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="0672f-138">Çalışma alanı adınız ardından **Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="0672f-138">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="0672f-139">Birlikte çalıştığınız Puanlama Web hizmeti tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0672f-139">Click the scoring Web service you are working with.</span></span> <span data-ttu-id="0672f-140">(Web hizmeti varsayılan adını değiştirmezseniz bu [Puanlama Exp içinde.] sona erer.)</span><span class="sxs-lookup"><span data-stu-id="0672f-140">(If you did not modify the default name of the web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="0672f-141">Tıklatın **uç nokta ekleme**.</span><span class="sxs-lookup"><span data-stu-id="0672f-141">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="0672f-142">Uç nokta eklendikten sonra uç nokta adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0672f-142">After the endpoint is added, click the endpoint name.</span></span> <span data-ttu-id="0672f-143">Ardından **güncelleştirme kaynağı** düzeltme eki uygulama Yardım sayfasını açın.</span><span class="sxs-lookup"><span data-stu-id="0672f-143">Then click **Update Resource** to open the patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="0672f-144">Tahmine dayalı Web hizmeti yerine eğitim Web hizmeti için uç nokta eklediyseniz, tıklattığınızda aşağıdaki hatayı alırsınız **güncelleştirme kaynağı** bağlantı: özür dileriz, ancak bu özellik desteklenmiyor veya bu kullanılabilir değil bağlamı.</span><span class="sxs-lookup"><span data-stu-id="0672f-144">If you have added the endpoint to the Training Web Service instead of the Predictive Web Service, you will receive the following error when you click the **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="0672f-145">Bu Web Hizmeti'nin güncelleştirilebilir kaynağı olmayan.</span><span class="sxs-lookup"><span data-stu-id="0672f-145">This Web Service has no updatable resources.</span></span> <span data-ttu-id="0672f-146">Biz rahatsızlıktan dolayı özür dileriz ve bu iş akışı geliştirmeye çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="0672f-146">We apologize for the inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Yeni bir uç nokta Pano.][image3]

<span data-ttu-id="0672f-148">Düzeltme eki Yardım sayfası düzeltme eki kullanmalısınız URL içerir ve bu çağrı için kullanabileceğiniz örnek kod sağlar.</span><span class="sxs-lookup"><span data-stu-id="0672f-148">The PATCH help page contains the PATCH URL you must use and provides sample code you can use to call it.</span></span>

![Düzeltme eki URL'si.][image5]

### <a name="check-to-see-that-you-are-updating-the-correct-scoring-endpoint"></a><span data-ttu-id="0672f-150">Doğru Puanlama uç noktası güncelleştiriliyor denetleyin</span><span class="sxs-lookup"><span data-stu-id="0672f-150">Check to see that you are updating the correct scoring endpoint</span></span>
* <span data-ttu-id="0672f-151">Eğitim Web hizmeti düzeltme eki değil: Puanlama Web hizmetinde düzeltme eki işlemi gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0672f-151">Do not patch the Training Web Service: The patch operation must be performed on the scoring Web service.</span></span>
* <span data-ttu-id="0672f-152">Web hizmeti varsayılan uç noktada düzeltme eki değil: eklediğiniz yeni Puanlama Web Hizmeti uç noktası üzerinde düzeltme eki işlemi gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0672f-152">Do not patch the default endpoint on Web service: The patch operation must be performed on the new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="0672f-153">Klasik Azure portalını ziyaret ederek uç nokta açıktır hangi Web hizmeti doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0672f-153">You can verify which Web service the endpoint is on by visiting the Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="0672f-154">Tahmine dayalı Web hizmeti için eğitim Web Hizmeti uç noktası ekleme emin olun.</span><span class="sxs-lookup"><span data-stu-id="0672f-154">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="0672f-155">Eğitim ve Tahmine dayalı bir Web hizmeti doğru olarak dağıttıysanız, listelenen iki ayrı Web Hizmetleri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0672f-155">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="0672f-156">Tahmine dayalı Web hizmeti, "[Tahmine dayalı exp.]" bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="0672f-156">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="0672f-157">[Klasik Azure portalında](https://manage.windowsazure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0672f-157">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0672f-158">Machine Learning sekmesini açın.</span><span class="sxs-lookup"><span data-stu-id="0672f-158">Open the Machine Learning tab.</span></span> 
   <span data-ttu-id="0672f-159">![Machine learning çalışma alanı UI.][image4]</span><span class="sxs-lookup"><span data-stu-id="0672f-159">![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="0672f-160">Çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="0672f-160">Select your workspace.</span></span>
4. <span data-ttu-id="0672f-161">Tıklatın **Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="0672f-161">Click **Web Services**.</span></span>
5. <span data-ttu-id="0672f-162">Tahmine dayalı Web hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="0672f-162">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="0672f-163">Yeni uç noktanızı Web hizmetine eklendiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="0672f-163">Verify that your new endpoint was added to the Web service.</span></span>

### <a name="check-the-workspace-that-your-web-service-is-in-to-ensure-it-is-in-the-correct-region"></a><span data-ttu-id="0672f-164">Web hizmeti doğru bölgede olduğundan emin olmak için bulunduğu çalışma denetleyin</span><span class="sxs-lookup"><span data-stu-id="0672f-164">Check the workspace that your web service is in to ensure it is in the correct region</span></span>
1. <span data-ttu-id="0672f-165">[Klasik Azure portalında](https://manage.windowsazure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0672f-165">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0672f-166">Machine Learning menüsünden seçin.</span><span class="sxs-lookup"><span data-stu-id="0672f-166">Select Machine Learning from the menu.</span></span>
   <span data-ttu-id="0672f-167">![Machine learning bölge UI.][image4]</span><span class="sxs-lookup"><span data-stu-id="0672f-167">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="0672f-168">Çalışma alanınızı konumunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="0672f-168">Verify the location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
