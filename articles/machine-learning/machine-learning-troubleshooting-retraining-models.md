---
title: "bir Azure Machine Learning Klasik yeniden eğitme aaaTroubleshoot web hizmetini | Microsoft Docs"
description: "Tanımlamak ve bir Azure Machine Learning Web hizmeti için hello modeli yeniden eğitme, ortak sorunları aygıtındaki düzeltin."
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
ms.openlocfilehash: 2b6a78eaba161877106dccdc23437b5e454fca7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="5ad78-103">Bir Azure Machine Learning Klasik Web hizmeti Hello yeniden eğitme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="5ad78-103">Troubleshooting hello retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="5ad78-104">Yeniden eğitme genel bakış</span><span class="sxs-lookup"><span data-stu-id="5ad78-104">Retraining overview</span></span>
<span data-ttu-id="5ad78-105">Tahmine dayalı denemeye Puanlama web hizmeti olarak dağıttığınızda statik bir modelidir.</span><span class="sxs-lookup"><span data-stu-id="5ad78-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="5ad78-106">Yeni veriler kullanılabilir olduğunda ya da kendi veri hello API hello tüketicisi varsa, hello modeli retrained toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ad78-106">As new data becomes available or when hello consumer of hello API has their own data, hello model needs toobe retrained.</span></span> 

<span data-ttu-id="5ad78-107">Klasik Web hizmeti işlemi yeniden eğitme hello tam kılavuzu için bkz [yeniden eğitme Machine Learning modellerini program aracılığıyla](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="5ad78-107">For a complete walkthrough of hello retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="5ad78-108">İşlemi yeniden eğitme</span><span class="sxs-lookup"><span data-stu-id="5ad78-108">Retraining process</span></span>
<span data-ttu-id="5ad78-109">Web hizmeti tooretrain hello gerektiğinde, bazı ek parçalar eklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="5ad78-109">When you need tooretrain hello Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="5ad78-110">Eğitim denemenizi Hello dağıtılan bir Web hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="5ad78-110">A Web service deployed from hello Training Experiment.</span></span> <span data-ttu-id="5ad78-111">Merhaba deneme olmalıdır bir **Web hizmeti çıkış** modülü bağlı hello toohello çıktısını **Train Model** modülü.</span><span class="sxs-lookup"><span data-stu-id="5ad78-111">hello experiment must have a **Web Service Output** module attached toohello output of hello **Train Model** module.</span></span>  
  
    ![Merhaba web hizmeti çıkış toohello train model ekleyin.][image1]
* <span data-ttu-id="5ad78-113">Yeni bir uç noktası, Web hizmeti Puanlama tooyour eklendi.</span><span class="sxs-lookup"><span data-stu-id="5ad78-113">A new endpoint added tooyour scoring Web service.</span></span>  <span data-ttu-id="5ad78-114">Program aracılığıyla hello uç nokta ekleme hello başvurulan hello örnek kodu kullanarak yeniden eğitme Machine Learning program aracılığıyla konu modellerini veya hello Klasik Azure Portalı aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="5ad78-114">You can add hello endpoint programmatically using hello sample code referenced in hello Retrain Machine Learning models programmatically topic or through hello Azure classic portal.</span></span>

<span data-ttu-id="5ad78-115">Merhaba örnek C# kod hello eğitim Web Service'in API Yardım sayfası tooretrain modelinden daha sonra kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ad78-115">You can then use hello sample C# code from hello Training Web Service's API help page tooretrain model.</span></span> <span data-ttu-id="5ad78-116">Merhaba sonuçları değerlendirilen ve bunlarla memnun sonra hello eğitilen modeli Puanlama eklediğiniz hello yeni uç nokta kullanarak web hizmeti güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5ad78-116">Once you have evaluated hello results and are satisfied with them, you update hello trained model scoring web service using hello new endpoint that you added.</span></span>

<span data-ttu-id="5ad78-117">Yerinde tüm hello parça ile tooretrain hello modeli gerçekleştirmeniz gereken hello önemli adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="5ad78-117">With all hello pieces in place, hello major steps you must take tooretrain hello model are as follows:</span></span>

1. <span data-ttu-id="5ad78-118">Merhaba eğitim Web hizmeti çağrısı: hello çağrıdır toohello toplu yürütme hizmeti (BES), istek yanıtı hizmeti (RRS) hello değil.</span><span class="sxs-lookup"><span data-stu-id="5ad78-118">Call hello Training Web Service:  hello call is toohello Batch Execution Service (BES), not hello Request Response Service (RRS).</span></span> <span data-ttu-id="5ad78-119">Merhaba API Yardım sayfası toomake hello çağrıda hello örnek C# kodu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ad78-119">You can use hello sample C# code on hello API help page toomake hello call.</span></span> 
2. <span data-ttu-id="5ad78-120">Merhaba Hello değerleri bulma *BaseLocation*, *RelativeLocation*, ve *SasBlobToken*: Bu değerleri hello çıktısında çağrısı toohello eğitim Web döndürülür Hizmet.</span><span class="sxs-lookup"><span data-stu-id="5ad78-120">Find hello values for hello *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in hello output from your call toohello Training Web Service.</span></span> 
   <span data-ttu-id="5ad78-121">![örnek ve hello BaseLocation, RelativeLocation ve SasBlobToken değerleri yeniden eğitme hello Hello çıktısını gösteriliyor.][image6]</span><span class="sxs-lookup"><span data-stu-id="5ad78-121">![showing hello output of hello retraining sample and hello BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="5ad78-122">Güncelleştirme hello eklenen uç noktasından yeni web hizmeti ile Merhaba Puanlama hello eğitilmiş model: hello Machine Learning yeniden eğitme modelleri programlı olarak hello yeni uç noktasını güncelleyin. sağlanan hello örnek kodu kullanarak hello modeliyle yeni Puanlama toohello eklendi Merhaba eğitim Web hizmeti eğitilen modeli.</span><span class="sxs-lookup"><span data-stu-id="5ad78-122">Update hello added endpoint from hello scoring web service with hello new trained model: Using hello sample code provided in hello Retrain Machine Learning models programmatically, update hello new endpoint you added toohello scoring model with hello newly trained model from hello Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="5ad78-123">Ortak engellerini</span><span class="sxs-lookup"><span data-stu-id="5ad78-123">Common obstacles</span></span>
### <a name="check-toosee-if-you-have-hello-correct-patch-url"></a><span data-ttu-id="5ad78-124">Düzeltme eki URL'yi düzeltin hello varsa toosee denetleyin</span><span class="sxs-lookup"><span data-stu-id="5ad78-124">Check toosee if you have hello correct PATCH URL</span></span>
<span data-ttu-id="5ad78-125">Merhaba kullanmakta olduğunuz URL düzeltme eki hello bir hello ile ilişkili olmalıdır Web hizmeti Puanlama toohello eklediğiniz yeni Puanlama uç noktası.</span><span class="sxs-lookup"><span data-stu-id="5ad78-125">hello PATCH URL you are using must be hello one associated with hello new scoring endpoint you added toohello scoring Web service.</span></span> <span data-ttu-id="5ad78-126">Yolları tooobtain hello düzeltme eki URL vardır:</span><span class="sxs-lookup"><span data-stu-id="5ad78-126">There are a number of ways tooobtain hello PATCH URL:</span></span>

<span data-ttu-id="5ad78-127">**Seçenek 1: programlı şekilde**</span><span class="sxs-lookup"><span data-stu-id="5ad78-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="5ad78-128">tooget hello düzeltme eki URL düzeltin:</span><span class="sxs-lookup"><span data-stu-id="5ad78-128">tooget hello correct PATCH URL:</span></span>

1. <span data-ttu-id="5ad78-129">Merhaba çalıştırmak [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) örnek kodu.</span><span class="sxs-lookup"><span data-stu-id="5ad78-129">Run hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="5ad78-130">Merhaba AddEndpoint Hello çıktısını Bul *HelpLocation* değer ve hello URL'yi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5ad78-130">From hello output of AddEndpoint, find hello *HelpLocation* value and copy hello URL.</span></span>
   
   ![HelpLocation hello addEndpoint örneğinin hello çıkışı.][image2]
3. <span data-ttu-id="5ad78-132">Yardım bağlantıları hello Web hizmeti için bir tarayıcı toonavigate tooa sayfası Hello URL yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="5ad78-132">Paste hello URL into a browser toonavigate tooa page that provides help links for hello Web service.</span></span>
4. <span data-ttu-id="5ad78-133">Merhaba tıklatın **güncelleştirme kaynağı** bağlantı tooopen hello düzeltme eki Yardım sayfası.</span><span class="sxs-lookup"><span data-stu-id="5ad78-133">Click hello **Update Resource** link tooopen hello patch help page.</span></span>

<span data-ttu-id="5ad78-134">**Seçenek 2: hello Klasik Azure portalını kullanın**</span><span class="sxs-lookup"><span data-stu-id="5ad78-134">**Option 2: Use hello Azure classic portal**</span></span>

1. <span data-ttu-id="5ad78-135">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5ad78-135">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="5ad78-136">Açık hello Machine Learning sekmesini tıklatın. ![Makine leaning sekmesini tıklatın.][image4]</span><span class="sxs-lookup"><span data-stu-id="5ad78-136">Open hello Machine Learning tab. ![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="5ad78-137">Çalışma alanı adınız ardından **Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="5ad78-137">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="5ad78-138">Web hizmeti birlikte çalıştığınız Puanlama hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5ad78-138">Click hello scoring Web service you are working with.</span></span> <span data-ttu-id="5ad78-139">(Merhaba varsayılan hello web hizmeti adını değiştirmezseniz bu [Puanlama Exp içinde.] sona erer.)</span><span class="sxs-lookup"><span data-stu-id="5ad78-139">(If you did not modify hello default name of hello web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="5ad78-140">Tıklatın **uç nokta ekleme**.</span><span class="sxs-lookup"><span data-stu-id="5ad78-140">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="5ad78-141">Merhaba endpoint eklendikten sonra hello uç nokta adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5ad78-141">After hello endpoint is added, click hello endpoint name.</span></span> <span data-ttu-id="5ad78-142">Ardından **güncelleştirme kaynağı** tooopen hello düzeltme eki uygulama Yardım sayfası.</span><span class="sxs-lookup"><span data-stu-id="5ad78-142">Then click **Update Resource** tooopen hello patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="5ad78-143">Merhaba Tahmine dayalı Web hizmeti yerine hello uç nokta toohello eğitim Web hizmeti eklediyseniz, hello tıklattığınızda aşağıdaki hata hello alacak **güncelleştirme kaynağı** bağlantı: özür dileriz, ancak bu özellik desteklenmiyor veya Bu bağlamda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5ad78-143">If you have added hello endpoint toohello Training Web Service instead of hello Predictive Web Service, you will receive hello following error when you click hello **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="5ad78-144">Bu Web Hizmeti'nin güncelleştirilebilir kaynağı olmayan.</span><span class="sxs-lookup"><span data-stu-id="5ad78-144">This Web Service has no updatable resources.</span></span> <span data-ttu-id="5ad78-145">Biz hello rahatsızlıktan ötürü özür dileriz ve bu iş akışı geliştirmeye çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="5ad78-145">We apologize for hello inconvenience and are working on improving this workflow.</span></span>
> 
> 

![Yeni bir uç nokta Pano.][image3]

<span data-ttu-id="5ad78-147">Hello düzeltme eki Yardım sayfası hello kullanmalısınız URL düzeltme eki içerir ve örnek kodu kullanabilirsiniz sağlar toocall onu.</span><span class="sxs-lookup"><span data-stu-id="5ad78-147">hello PATCH help page contains hello PATCH URL you must use and provides sample code you can use toocall it.</span></span>

![Düzeltme eki URL'si.][image5]

### <a name="check-toosee-that-you-are-updating-hello-correct-scoring-endpoint"></a><span data-ttu-id="5ad78-149">Onay toosee hello doğru Puanlama uç noktası güncelleştiriliyor</span><span class="sxs-lookup"><span data-stu-id="5ad78-149">Check toosee that you are updating hello correct scoring endpoint</span></span>
* <span data-ttu-id="5ad78-150">Merhaba eğitim Web hizmeti düzeltme eki değil: hello düzeltme eki işlemi üzerinde Web hizmeti Puanlama hello gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ad78-150">Do not patch hello Training Web Service: hello patch operation must be performed on hello scoring Web service.</span></span>
* <span data-ttu-id="5ad78-151">Web hizmeti üzerinde Hello varsayılan uç nokta düzeltme eki değil: hello düzeltme eki işlemi üzerinde yeni eklediğiniz Web Hizmeti uç noktası Puanlama hello gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ad78-151">Do not patch hello default endpoint on Web service: hello patch operation must be performed on hello new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="5ad78-152">Hangi Web hizmeti hello uç noktası tarafından ziyaret hello Klasik Azure portalı açıktır doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ad78-152">You can verify which Web service hello endpoint is on by visiting hello Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="5ad78-153">Merhaba uç nokta toohello Tahmine dayalı Web hizmeti, hello eğitim Web hizmeti ekleme emin olun.</span><span class="sxs-lookup"><span data-stu-id="5ad78-153">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="5ad78-154">Eğitim ve Tahmine dayalı bir Web hizmeti doğru olarak dağıttıysanız, listelenen iki ayrı Web Hizmetleri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ad78-154">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="5ad78-155">Merhaba Tahmine dayalı Web hizmeti, "[Tahmine dayalı exp.]" bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="5ad78-155">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="5ad78-156">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5ad78-156">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="5ad78-157">Açık hello Machine Learning sekmesini tıklatın. ![Machine learning çalışma alanı UI.][image4]</span><span class="sxs-lookup"><span data-stu-id="5ad78-157">Open hello Machine Learning tab. ![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="5ad78-158">Çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="5ad78-158">Select your workspace.</span></span>
4. <span data-ttu-id="5ad78-159">Tıklatın **Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="5ad78-159">Click **Web Services**.</span></span>
5. <span data-ttu-id="5ad78-160">Tahmine dayalı Web hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="5ad78-160">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="5ad78-161">Yeni uç noktanızı toohello Web hizmeti eklendiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5ad78-161">Verify that your new endpoint was added toohello Web service.</span></span>

### <a name="check-hello-workspace-that-your-web-service-is-in-tooensure-it-is-in-hello-correct-region"></a><span data-ttu-id="5ad78-162">Merhaba doğru bölgede olması tooensure, web hizmetidir hello çalışma denetleyin</span><span class="sxs-lookup"><span data-stu-id="5ad78-162">Check hello workspace that your web service is in tooensure it is in hello correct region</span></span>
1. <span data-ttu-id="5ad78-163">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5ad78-163">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="5ad78-164">Machine Learning hello menüsünden seçin.</span><span class="sxs-lookup"><span data-stu-id="5ad78-164">Select Machine Learning from hello menu.</span></span>
   <span data-ttu-id="5ad78-165">![Machine learning bölge UI.][image4]</span><span class="sxs-lookup"><span data-stu-id="5ad78-165">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="5ad78-166">Çalışma alanınızı Hello konumunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="5ad78-166">Verify hello location of your workspace.</span></span>

<!-- Image Links -->

[image1]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: ./media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png
