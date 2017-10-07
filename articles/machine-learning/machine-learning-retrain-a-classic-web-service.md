---
title: Klasik web hizmeti aaaRetrain | Microsoft Docs
description: "Tooprogrammatically bir model ve güncelleştirme hello web hizmeti toouse hello yeni eğitilen model Azure Machine Learning nasıl yeniden eğitme öğrenin."
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
ms.openlocfilehash: d3ba21ed75f02868535cb2fcac607643303a9554
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-classic-web-service"></a><span data-ttu-id="9e7ff-103">Klasik web hizmetini yeniden eğitme</span><span class="sxs-lookup"><span data-stu-id="9e7ff-103">Retrain a Classic web service</span></span>
<span data-ttu-id="9e7ff-104">Merhaba dağıttığınız Tahmine dayalı Web Hizmeti uç noktası Puanlama hello varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-104">hello Predictive Web Service you deployed is hello default scoring endpoint.</span></span> <span data-ttu-id="9e7ff-105">Varsayılan uç noktalar hello ile senkronize eğitim ve puanlama denemeler özgün tutulur ve bu nedenle hello eğitilen model hello varsayılan uç noktası için değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-105">Default endpoints are kept in sync with hello original training and scoring experiments, and therefore hello trained model for hello default endpoint cannot be replaced.</span></span> <span data-ttu-id="9e7ff-106">tooretrain hello web hizmeti, yeni bir uç nokta toohello web hizmeti eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-106">tooretrain hello web service, you must add a new endpoint toohello web service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9e7ff-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9e7ff-107">Prerequisites</span></span>
<span data-ttu-id="9e7ff-108">Eğitim denemenizi ve Tahmine dayalı denemeye gösterildiği gibi ayarlamış olmanız gerekir [yeniden eğitme Machine Learning modellerini programlama aracılığıyla](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="9e7ff-108">You must have set up a training experiment and a predictive experiment as shown in [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9e7ff-109">Merhaba Tahmine dayalı denemeye Klasik machine learning web hizmeti dağıtılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-109">hello predictive experiment must be deployed as a Classic machine learning web service.</span></span> 
> 
> 

<span data-ttu-id="9e7ff-110">Web hizmetleri dağıtma hakkında ek bilgi için bkz: [bir Azure Machine Learning web hizmetini dağıtma](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="9e7ff-110">For additional information on Deploying web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="add-a-new-endpoint"></a><span data-ttu-id="9e7ff-111">Yeni bir uç nokta ekleyin</span><span class="sxs-lookup"><span data-stu-id="9e7ff-111">Add a new Endpoint</span></span>
<span data-ttu-id="9e7ff-112">Merhaba dağıttığınız Tahmine dayalı Web hizmeti Puanlama hello özgün eğitim ve puanlama denemeler eğitilen model ile eşitlenmiş olarak saklanmasını uç noktası varsayılan içerir.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-112">hello Predictive Web Service that you deployed contains a default scoring endpoint that is kept in sync with hello original training and scoring experiments trained model.</span></span> <span data-ttu-id="9e7ff-113">tooupdate, web hizmeti toowith yeni bir modeli yeni bir Puanlama uç noktası oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-113">tooupdate your web service toowith a new trained model, you must create a new scoring endpoint.</span></span> 

<span data-ttu-id="9e7ff-114">Yeni bir Puanlama uç noktası, hello hello eğitilen model ile güncelleştirilebilir Tahmine dayalı Web hizmeti üzerinde toocreate:</span><span class="sxs-lookup"><span data-stu-id="9e7ff-114">toocreate a new scoring endpoint, on hello Predictive Web Service that can be updated with hello trained model:</span></span>

> [!NOTE]
> <span data-ttu-id="9e7ff-115">Merhaba uç nokta toohello Tahmine dayalı Web hizmeti, hello eğitim Web hizmeti ekleme emin olun.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-115">Be sure you are adding hello endpoint toohello Predictive Web Service, not hello Training Web Service.</span></span> <span data-ttu-id="9e7ff-116">Eğitim ve Tahmine dayalı bir Web hizmeti doğru olarak dağıttıysanız, listelenen iki ayrı bir web hizmetleri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-116">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="9e7ff-117">Merhaba Tahmine dayalı Web hizmeti, "[Tahmine dayalı exp.]" bitmelidir.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-117">hello Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

<span data-ttu-id="9e7ff-118">Yeni bir uç noktası tooa web hizmeti eklemenin üç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="9e7ff-118">There are three ways in which you can add a new end point tooa web service:</span></span>

1. <span data-ttu-id="9e7ff-119">Programlama yoluyla</span><span class="sxs-lookup"><span data-stu-id="9e7ff-119">Programmatically</span></span>
2. <span data-ttu-id="9e7ff-120">Merhaba Microsoft Azure Web Hizmetleri portalı kullanın</span><span class="sxs-lookup"><span data-stu-id="9e7ff-120">Use hello Microsoft Azure Web Services portal</span></span>
3. <span data-ttu-id="9e7ff-121">Merhaba Klasik Azure portalını kullanın</span><span class="sxs-lookup"><span data-stu-id="9e7ff-121">Use hello Azure classic portal</span></span>

### <a name="programmatically-add-an-endpoint"></a><span data-ttu-id="9e7ff-122">Program aracılığıyla bir uç nokta ekleme</span><span class="sxs-lookup"><span data-stu-id="9e7ff-122">Programmatically add an endpoint</span></span>
<span data-ttu-id="9e7ff-123">Bu konuda sağlanan hello örnek kodu kullanarak Puanlama uç noktalar ekleyebilirsiniz [github deposunu](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="9e7ff-123">You can add scoring endpoints using hello sample code provided in this [github repository](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs).</span></span>

### <a name="use-hello-microsoft-azure-web-services-portal-tooadd-an-endpoint"></a><span data-ttu-id="9e7ff-124">Merhaba Microsoft Azure Web Hizmetleri portalı tooadd bir uç nokta kullanın</span><span class="sxs-lookup"><span data-stu-id="9e7ff-124">Use hello Microsoft Azure Web Services portal tooadd an endpoint</span></span>
1. <span data-ttu-id="9e7ff-125">Machine Learning Studio'da hello sol gezinti sütuna, Web Hizmetleri'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-125">In Machine Learning Studio, on hello left navigation column, click Web Services.</span></span>
2. <span data-ttu-id="9e7ff-126">Merhaba web hizmeti Pano Hello altındaki tıklatın **yönetin uç noktaları Önizleme**.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-126">At hello bottom of hello web service dashboard, click **Manage endpoints preview**.</span></span>
3. <span data-ttu-id="9e7ff-127">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-127">Click **Add**.</span></span>
4. <span data-ttu-id="9e7ff-128">Bir ad ve hello yeni uç noktası için bir açıklama yazın.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-128">Type a name and description for hello new endpoint.</span></span> <span data-ttu-id="9e7ff-129">Merhaba günlüğe kaydetme düzeyi ve örnek verileri etkinleştirilip etkinleştirilmediğini seçin.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-129">Select hello logging level and whether sample data is enabled.</span></span> <span data-ttu-id="9e7ff-130">Günlüğe kaydetme hakkında daha fazla bilgi için bkz: [Machine Learning web hizmetleri için günlüğe kaydetmeyi etkinleştirmek](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="9e7ff-130">For more information on logging, see [Enable logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>

### <a name="use-hello-azure-classic-portal-tooadd-an-endpoint"></a><span data-ttu-id="9e7ff-131">Hello Azure Klasik portalı tooadd bir uç nokta kullanın</span><span class="sxs-lookup"><span data-stu-id="9e7ff-131">Use hello Azure classic portal tooadd an endpoint</span></span>
1. <span data-ttu-id="9e7ff-132">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9e7ff-132">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9e7ff-133">Merhaba soldaki menüde tıklatın **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-133">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="9e7ff-134">Adı altında çalışma alanına tıklayın ve ardından **Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-134">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="9e7ff-135">Adı altında tıklatın **Census modeli [Tahmine dayalı exp.]** .</span><span class="sxs-lookup"><span data-stu-id="9e7ff-135">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="9e7ff-136">Merhaba sayfasının Hello altında tıklatın **uç nokta Ekle**.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-136">At hello bottom of hello page, click **Add Endpoint**.</span></span> <span data-ttu-id="9e7ff-137">Uç noktaları ekleme hakkında daha fazla bilgi için bkz: [uç noktaları oluşturma](machine-learning-create-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="9e7ff-137">For more information on adding endpoints, see [Creating Endpoints](machine-learning-create-endpoint.md).</span></span> 

## <a name="update-hello-added-endpoints-trained-model"></a><span data-ttu-id="9e7ff-138">Uç noktanın eğitilen Model güncelleştirme hello eklendi</span><span class="sxs-lookup"><span data-stu-id="9e7ff-138">Update hello added endpoint’s Trained Model</span></span>
<span data-ttu-id="9e7ff-139">toocomplete hello yeniden eğitme işlemi, eklediğiniz hello yeni uç nokta eğitilen modelini hello güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-139">toocomplete hello retraining process, you must update hello trained model of hello new endpoint that you added.</span></span>

* <span data-ttu-id="9e7ff-140">Merhaba Klasik Azure portalını kullanarak hello yeni uç nokta eklediyseniz, hello portalında hello yeni uç noktanın adına tıklayın, ardından hello **UpdateResource** bağlantı gereksinim tooupdate hello uç noktanın modeli tooget hello URL.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-140">If you added hello new endpoint using hello classic Azure portal, you can click hello new endpoint's name in hello portal, then hello **UpdateResource** link tooget hello URL you would need tooupdate hello endpoint's model.</span></span>
* <span data-ttu-id="9e7ff-141">Merhaba örnek kodu kullanarak hello endpoint eklediyseniz, bu hello tarafından tanımlanan hello Yardım URL'si konumunu içeren *HelpLocationURL* hello çıktı değeri.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-141">If you added hello endpoint using hello sample code, this includes location of hello help URL identified by hello *HelpLocationURL* value in hello output.</span></span>

<span data-ttu-id="9e7ff-142">tooretrieve hello yol URL'si:</span><span class="sxs-lookup"><span data-stu-id="9e7ff-142">tooretrieve hello path URL:</span></span>

1. <span data-ttu-id="9e7ff-143">Merhaba URL'sini kopyalayıp tarayıcınıza yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-143">Copy and paste hello URL into your browser.</span></span>
2. <span data-ttu-id="9e7ff-144">Merhaba güncelleştirme kaynağı bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-144">Click hello Update Resource link.</span></span>
3. <span data-ttu-id="9e7ff-145">Merhaba hello PATCH isteği gönderme URL'sini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-145">Copy hello POST URL of hello PATCH request.</span></span> <span data-ttu-id="9e7ff-146">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="9e7ff-146">For example:</span></span>
   
     <span data-ttu-id="9e7ff-147">DÜZELTME EKİ URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span><span class="sxs-lookup"><span data-stu-id="9e7ff-147">PATCH URL: https://management.azureml.net/workspaces/00bf70534500b34rebfa1843d6/webservices/af3er32ad393852f9b30ac9a35b/endpoints/newendpoint2</span></span>

<span data-ttu-id="9e7ff-148">Daha önce oluşturduğunuz endpoint Puanlama hello eğitilen model tooupdate hello artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-148">You can now use hello trained model tooupdate hello scoring endpoint that you created previously.</span></span>

<span data-ttu-id="9e7ff-149">Aşağıdaki örnek kod hello gösterir, nasıl toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*ve düzeltme eki URL tooupdate hello uç.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-149">hello following sample code shows you how toouse hello *BaseLocation*, *RelativeLocation*, *SasBlobToken*, and PATCH URL tooupdate hello endpoint.</span></span>

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
                        RelativeLocation = "your endpoint relative location", //from hello output, for example: “experimentoutput/8946abfd-79d6-4438-89a9-3e5d109183/8946abfd-79d6-4438-89a9-3e5d109183.ilearner”
                        SasBlobToken = "your endpoint SAS blob token" //from hello output, for example: “?sv=2013-08-15&sr=c&sig=37lTTfngRwxCcf94%3D&st=2015-01-30T22%3A53%3A06Z&se=2015-01-31T22%3A58%3A06Z&sp=rl”
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

<span data-ttu-id="9e7ff-150">Merhaba *apikey ile yapılan* ve hello *endpointUrl* için uç nokta panodan hello çağrısı alınabilir.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-150">hello *apiKey* and hello *endpointUrl* for hello call can be obtained from endpoint dashboard.</span></span>

<span data-ttu-id="9e7ff-151">Merhaba hello değerini *adı* parametresinde *kaynakları* eşleşme hello hello kaynak adını kaydedilmiş eğitilen Model hello Tahmine dayalı denemesinde.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-151">hello value of hello *Name* parameter in *Resources* should match hello Resource Name of hello saved Trained Model in hello predictive experiment.</span></span> <span data-ttu-id="9e7ff-152">tooget hello kaynak adı:</span><span class="sxs-lookup"><span data-stu-id="9e7ff-152">tooget hello Resource Name:</span></span>

1. <span data-ttu-id="9e7ff-153">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9e7ff-153">Sign in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9e7ff-154">Merhaba soldaki menüde tıklatın **Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-154">In hello left menu, click **Machine Learning**.</span></span>
3. <span data-ttu-id="9e7ff-155">Adı altında çalışma alanına tıklayın ve ardından **Web Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-155">Under Name, click your workspace and then click **Web Services**.</span></span>
4. <span data-ttu-id="9e7ff-156">Adı altında tıklatın **Census modeli [Tahmine dayalı exp.]** .</span><span class="sxs-lookup"><span data-stu-id="9e7ff-156">Under Name, click **Census Model [predictive exp.]**.</span></span>
5. <span data-ttu-id="9e7ff-157">Eklediğiniz hello yeni uç noktasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-157">Click hello new endpoint you added.</span></span>
6. <span data-ttu-id="9e7ff-158">Merhaba uç nokta Panoda tıklatın **güncelleştirme kaynağı**.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-158">On hello endpoint dashboard, click **Update Resource**.</span></span>
7. <span data-ttu-id="9e7ff-159">Merhaba güncelleştirme kaynağı API belgelerine sayfasında hello web hizmeti hello bulabilirsiniz **kaynak adı** altında **güncelleştirilebilir kaynakları**.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-159">On hello Update Resource API Documentation page for hello web service, you can find hello **Resource Name** under **Updatable Resources**.</span></span>

<span data-ttu-id="9e7ff-160">Merhaba uç noktası güncelleniyor bitirmeden SAS belirteci süresi dolarsa, bir GET hello iş kimliği tooobtain yeni bir belirteç ile gerçekleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-160">If your SAS token expires before you finish updating hello endpoint, you must perform a GET with hello Job Id tooobtain a fresh token.</span></span>

<span data-ttu-id="9e7ff-161">Merhaba kodu başarıyla çalıştırıldı, hello yeni uç nokta yaklaşık 30 saniye içinde retrained hello modelini kullanarak başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-161">When hello code has successfully run, hello new endpoint should start using hello retrained model in approximately 30 seconds.</span></span>

## <a name="summary"></a><span data-ttu-id="9e7ff-162">Özet</span><span class="sxs-lookup"><span data-stu-id="9e7ff-162">Summary</span></span>
<span data-ttu-id="9e7ff-163">Kullanarak yeniden eğitme API'lerini Merhaba, eğitilen modelini senaryoları gibi etkinleştirme Tahmine dayalı bir Web hizmeti hello güncelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9e7ff-163">Using hello Retraining APIs, you can update hello trained model of a predictive Web Service enabling scenarios such as:</span></span>

* <span data-ttu-id="9e7ff-164">Yeni verilerle yeniden eğitme düzenli modeli.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-164">Periodic model retraining with new data.</span></span>
* <span data-ttu-id="9e7ff-165">Kullanıcıların kendi verilerini kullanarak hello modeli yeniden eğitme yapmalarına izin hello amacı ile bir model toocustomers dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="9e7ff-165">Distribution of a model toocustomers with hello goal of letting them retrain hello model using their own data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e7ff-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e7ff-166">Next steps</span></span>
[<span data-ttu-id="9e7ff-167">Bir Azure Machine Learning Klasik web hizmeti Hello yeniden eğitme sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="9e7ff-167">Troubleshooting hello retraining of an Azure Machine Learning classic web service</span></span>](machine-learning-troubleshooting-retraining-models.md)

