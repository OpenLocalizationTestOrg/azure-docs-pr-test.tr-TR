---
title: "Klasik web hizmeti yeniden eğitme | Microsoft Docs"
description: "Program aracılığıyla bir modeli yeniden eğitme ve Azure Machine Learning ile yeni eğitilen modelini kullanmak için web hizmetini güncelleştirmek hakkında bilgi edinin."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondlaghaeian
editor: 
ms.assetid: e36e1961-9e8b-4801-80ef-46d80b140452
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3f9f4cd5ed36262845f7a3139073ccd4e49f472a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="48c61-103">Klasik web hizmetini yeniden eğitme</span><span class="sxs-lookup"><span data-stu-id="48c61-103">Retrain a Classic web service</span></span>
<span data-ttu-id="48c61-104">Dağıttığınız Tahmine dayalı Web Hizmeti uç noktası Puanlama varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="48c61-104">The Predictive Web Service you deployed is the default scoring endpoint.</span></span> <span data-ttu-id="48c61-105">Varsayılan uç noktalar özgün eğitim ve puanlama denemeler ile eşitlenmiş tutulur ve bu nedenle varsayılan uç noktası için eğitilen model değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="48c61-105">Default endpoints are kept in sync with the original training and scoring experiments, and therefore the trained model for the default endpoint cannot be replaced.</span></span> <span data-ttu-id="48c61-106">Web hizmeti çağırma için yeni bir uç noktası için web hizmeti eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="48c61-106">To retrain the web service, you must add a new endpoint to the web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="48c61-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="48c61-107">Prerequisites</span></span>
<span data-ttu-id="48c61-108">Eğitim denemenizi ve Tahmine dayalı denemeye gösterildiği gibi ayarlamış olmanız gerekir [yeniden eğitme Machine Learning modellerini programlama aracılığıyla](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="48c61-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="48c61-109">Tahmine dayalı denemeye Klasik machine learning web hizmeti dağıtılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="48c61-109">The predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="48c61-110">Web hizmetleri dağıtma hakkında ek bilgi için bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="48c61-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="48c61-111">Yeni bir uç nokta ekleyin</span><span class="sxs-lookup"><span data-stu-id="48c61-111">Add a new Endpoint</span></span>
<span data-ttu-id="48c61-112">Dağıttığınız Tahmine dayalı Web hizmeti özgün eğitim ile eşitlenmiş olarak saklanmasını endpoint Puanlama ve denemeler eğitilen modeli Puanlama varsayılan içerir.</span><span class="sxs-lookup"><span data-stu-id="48c61-112">The Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with the original training and scoring experiments trained model.</span></span> <span data-ttu-id="48c61-113">Web hizmetiniz ile yeni bir eğitilen modeli güncelleştirmek için yeni bir Puanlama uç noktası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="48c61-113">To update your web service to with a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="48c61-114">Yeni bir Puanlama uç noktası, eğitilen model ile güncelleştirilebilir Tahmine dayalı Web hizmeti oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="48c61-114">To create a new scoring endpoint, on the Predictive Web Service that can be updated with the trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="48c61-115">Tahmine dayalı Web hizmeti için eğitim Web Hizmeti uç noktası ekleme emin olun.</span><span class="sxs-lookup"><span data-stu-id="48c61-115">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="48c61-116">Eğitim ve Tahmine dayalı bir Web hizmeti doğru olarak dağıttıysanız, listelenen iki ayrı bir web hizmetleri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="48c61-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="48c61-117">Tahmine dayalı Web hizmeti, "[Tahmine dayalı exp.]" bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="48c61-117">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="48c61-118">Yeni bir uç noktası için web hizmeti olarak Ekle üç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="48c61-118">There are three ways in which you can add a new end point to a web service:</span></span>

1. <span data-ttu-id="48c61-119">Programlama yoluyla</span><span class="sxs-lookup"><span data-stu-id="48c61-119">Programmatically</span></span>
2. <span data-ttu-id="48c61-120">Microsoft Azure Web Hizmetleri Portalı'nı kullanın</span><span class="sxs-lookup"><span data-stu-id="48c61-120">Use the Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="48c61-121">Klasik Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="48c61-121">Use the Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="48c61-122">Program aracılığıyla bir uç nokta ekleme</span><span class="sxs-lookup"><span data-stu-id="48c61-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="48c61-123">Bu konuda sağlanan örnek kodu kullanarak Puanlama uç noktalar ekleyebilirsiniz [github deposunu](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="48c61-123">You can add scoring endpoints using the sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-the-microsoft-azure-web-services-portal-to-add-an-endpoint"></a><span data-ttu-id="48c61-124">Bir uç noktası eklemek için Microsoft Azure Web Hizmetleri Portalı'nı kullanın</span><span class="sxs-lookup"><span data-stu-id="48c61-124">Use the Microsoft Azure Web Services portal to add an endpoint</span></span>
1. <span data-ttu-id="48c61-125">Machine Learning Studio'da Web Hizmetleri sol gezinti sütunu,'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="48c61-125">In Machine Learning Studio, on the left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="48c61-126">Web hizmeti Pano altındaki tıklatın **yönetin uç noktaları Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="48c61-126">At the bottom of the web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="48c61-127">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="48c61-127">Click **Add**.</span></span>
4. <span data-ttu-id="48c61-128">Bir ad ve yeni uç noktası için bir açıklama yazın.</span><span class="sxs-lookup"><span data-stu-id="48c61-128">Type a name and description for the new endpoint.</span></span> <span data-ttu-id="48c61-129">Günlüğe kaydetme düzeyi ve örnek verileri etkinleştirilip etkinleştirilmediğini seçin.</span><span class="sxs-lookup"><span data-stu-id="48c61-129">Select the logging level and whether sample data is enabled.</span></span> <span data-ttu-id="48c61-130">Günlüğe kaydetme hakkında daha fazla bilgi için bkz: [Machine Learning web hizmetleri için günlüğe kaydetmeyi etkinleştirmek](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="48c61-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-the-azure-classic-portal-to-add-an-endpoint"></a><span data-ttu-id="48c61-131">Bir uç noktası eklemek için Klasik Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="48c61-131">Use the Azure classic portal to add an endpoint</span></span>
1. <span data-ttu-id="48c61-132">Oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="48c61-132">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="48c61-133">Soldaki menüde tıklatın **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="48c61-133">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="48c61-134">Adı altında çalışma alanına tıklayın ve ardından **Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="48c61-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="48c61-135">Adı altında tıklatın **Census modeli [Tahmine dayalı exp.]** .</span><span class="sxs-lookup"><span data-stu-id="48c61-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="48c61-136">Sayfanın alt kısmındaki tıklatın **uç nokta Ekle**.</span><span class="sxs-lookup"><span data-stu-id="48c61-136">At the bottom of the page, click **Add Endpoint**.</span></span> <span data-ttu-id="48c61-137">Uç noktaları ekleme hakkında daha fazla bilgi için bkz: [uç noktaları oluşturma](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="48c61-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-the-added-endpoints-trained-model"></a><span data-ttu-id="48c61-138">Eklenen uç noktanın eğitilen Model güncelleştir</span><span class="sxs-lookup"><span data-stu-id="48c61-138">Update the added endpoint’s Trained Model</span></span>
<span data-ttu-id="48c61-139">Yeniden eğitme işlemini tamamlamak için eklediğiniz yeni uç nokta eğitilen modelini güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="48c61-139">To complete the retraining process, you must update the trained model of the new endpoint that you added.</span></span>

* <span data-ttu-id="48c61-140">Klasik Azure Portalı'nı kullanarak yeni uç nokta eklediyseniz, portal yeni uç noktanın adını tıklatabilirsiniz sonra **UpdateResource** uç noktanın modeli güncelleştirmek gerekir URL almak için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="48c61-140">If you added the new endpoint using the classic Azure portal, you can click the new endpoint's name in the portal, then the **UpdateResource** link to get the URL you would need to update the endpoint's model.</span></span>
* <span data-ttu-id="48c61-141">Örnek kodu kullanarak uç nokta eklediyseniz, bu tarafından tanımlanan Yardım URL'si konumunu içeren *HelpLocationURL* çıktı değeri.</span><span class="sxs-lookup"><span data-stu-id="48c61-141">If you added the endpoint using the sample code, this includes location of the help URL identified by the *HelpLocationURL* value in the output.</span></span>

<span data-ttu-id="48c61-142">Yol URL'sini almak için:</span><span class="sxs-lookup"><span data-stu-id="48c61-142">To retrieve the path URL:</span></span>

1. <span data-ttu-id="48c61-143">URL'sini kopyalayıp tarayıcınıza yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="48c61-143">Copy and paste the URL into your browser.</span></span>
2. <span data-ttu-id="48c61-144">Güncelleştirme kaynağı bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="48c61-144">Click the Update Resource link.</span></span>
3. <span data-ttu-id="48c61-145">PATCH isteği gönderme URL'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="48c61-145">Copy the POST URL of the PATCH request.</span></span> <span data-ttu-id="48c61-146">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="48c61-146">For example:</span></span>
   
     <span data-ttu-id="48c61-147">DÜZELTME EKİ URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="48c61-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="48c61-148">Daha önce oluşturduğunuz Puanlama uç nokta güncelleştirmek için eğitilen modeli şimdi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48c61-148">You can now use the trained model to update the scoring endpoint that you created previously.</span></span>

<span data-ttu-id="48c61-149">Aşağıdaki örnek kod, nasıl kullanılacağını gösterir *BaseLocation*, *RelativeLocation*, *SasBlobToken*ve düzeltme eki URL uç noktasını güncelleyin.</span><span class="sxs-lookup"><span data-stu-id="48c61-149">The following sample code shows you how to use the *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL to update the endpoint.</span></span>

    private async Task OverwriteModel()
    {
        var resourceLocations = new
        {
            Resources = new[]
            {
                new
                {
                    Name = "Census Model [trained model]",
                    Location = new AzureBlobDataReference()
                    {
                        BaseLocation = "https://esintussouthsus.blob.core.windows.net/",
                        RelativeLocation = "your endpoint relative location", //from the output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from the output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
                    }
                }
            }
        };

        using (var client = new HttpClient())
        {
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", apiKey);

            using (var request = new HttpRequestMessage(new HttpMethod("PATCH"), endpointUrl))
            {
                request.Content = new StringContent(JsonConvert.SerializeObject(resourceLocations), System.Text.Encoding.UTF8, "application/json");
                HttpResponseMessage response = await client.SendAsync(request);

                if (!response.IsSuccessStatusCode)
                {
                    await WriteFailedResponse(response);
                }

                // Do what you want with a successful response here.
            }
        }
    }

<span data-ttu-id="48c61-150">*Apikey ile yapılan* ve *endpointUrl* çağrı uç nokta panodan elde edilebilir için.</span><span class="sxs-lookup"><span data-stu-id="48c61-150">The *apiKey* and the *endpointUrl* for the call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="48c61-151">Değeri *adı* parametresinde *kaynakları* Tahmine dayalı denemeye kaydedilmiş eğitilen modele kaynak adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="48c61-151">The value of the *Name* parameter in *Resources* should match the Resource Name of the saved Trained Model in the predictive experiment.</span></span> <span data-ttu-id="48c61-152">Kaynak adı almak için:</span><span class="sxs-lookup"><span data-stu-id="48c61-152">To get the Resource Name:</span></span>

1. <span data-ttu-id="48c61-153">Oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="48c61-153">Sign in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="48c61-154">Soldaki menüde tıklatın **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="48c61-154">In the left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="48c61-155">Adı altında çalışma alanına tıklayın ve ardından **Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="48c61-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="48c61-156">Adı altında tıklatın **Census modeli [Tahmine dayalı exp.]** .</span><span class="sxs-lookup"><span data-stu-id="48c61-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="48c61-157">Eklediğiniz yeni uç noktasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="48c61-157">Click the new endpoint you added.</span></span>
6. <span data-ttu-id="48c61-158">Uç nokta Panoda tıklatın **güncelleştirme kaynağı**.</span><span class="sxs-lookup"><span data-stu-id="48c61-158">On the endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="48c61-159">Web hizmeti için güncelleştirme kaynağı API belgelerine sayfasında bulabilirsiniz **kaynak adı** altında **güncelleştirilebilir kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="48c61-159">On the Update Resource API Documentation page for the web service, you can find the **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="48c61-160">Uç noktası güncelleniyor bitirmeden SAS belirteci süresi dolarsa, yeni bir belirteç almak için iş kimliğine sahip bir GET gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="48c61-160">If your SAS token expires before you finish updating the endpoint, you must perform a GET with the Job Id to obtain a fresh token.</span></span>

<span data-ttu-id="48c61-161">Kod başarıyla çalıştırıldı, yeni uç nokta yaklaşık 30 saniye içinde retrained modelini kullanarak başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="48c61-161">When the code has successfully run, the new endpoint should start using the retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="48c61-162">Özet</span><span class="sxs-lookup"><span data-stu-id="48c61-162">Summary</span></span>
<span data-ttu-id="48c61-163">Yeniden eğitme API'lerini kullanarak, Tahmine dayalı bir Web hizmeti gibi senaryoları etkinleştirme eğitilen modelini güncelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="48c61-163">Using the Retraining APIs, you can update the trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="48c61-164">Yeni verilerle yeniden eğitme düzenli modeli.</span><span class="sxs-lookup"><span data-stu-id="48c61-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="48c61-165">Kullanıcıların kendi verilerini kullanarak modeli yeniden eğitme yapmalarına izin amacı ile dağıtım müşteriler için bir modelin.</span><span class="sxs-lookup"><span data-stu-id="48c61-165">Distribution of a model to customers with the goal of letting them retrain the model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48c61-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48c61-166">Next steps</span></span>
[<span data-ttu-id="48c61-167">Bir Azure Machine Learning Klasik web hizmeti yeniden eğitme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="48c61-167">Troubleshooting the retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

