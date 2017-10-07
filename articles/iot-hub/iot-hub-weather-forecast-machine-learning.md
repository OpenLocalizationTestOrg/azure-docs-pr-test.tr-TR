---
title: "IOT hub'ı verilerle Azure Machine Learning kullanarak tahmin aaaWeather | Microsoft Docs"
description: "Azure Machine Learning toopredict hello Yağmur olasılığını hello sıcaklık ve nem algılayıcı IOT hub'ınızı topladığı veri tabanlı kullanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: machine learning hava durumu tahmini
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="b81e5-104">IOT hub'ınızı hello algılayıcı verilerini Azure Machine Learning kullanarak hava durumu tahmini</span><span class="sxs-lookup"><span data-stu-id="b81e5-104">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="b81e5-106">Machine learning, mevcut veri tooforecast gelecekteki davranışları, sonuçları ve eğilimleri öğrenin bilgisayarlar yardımcı olan veri bilimi bir tekniktir.</span><span class="sxs-lookup"><span data-stu-id="b81e5-106">Machine learning is a technique of data science that helps computers learn from existing data tooforecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="b81e5-107">Azure Machine Learning olası tooquickly kolaylaştıran bir bulut Tahmine dayalı analiz hizmeti oluşturma ve Tahmine dayalı modelleri analiz çözümleri olarak dağıtma ' dir.</span><span class="sxs-lookup"><span data-stu-id="b81e5-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible tooquickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="b81e5-108">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="b81e5-108">What you learn</span></span>

<span data-ttu-id="b81e5-109">Nasıl toouse Azure Machine Learning toodo hava tahmini (Yağmur olasılığını) kullanarak izin ver hello Azure IOT hub'ınızı sıcaklık ve nem verilerden öğrenin.</span><span class="sxs-lookup"><span data-stu-id="b81e5-109">You learn how toouse Azure Machine Learning toodo weather forecast (chance of rain) using hello temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="b81e5-110">Yağmur Hello olasılığını hello hazırlıklı hava durumu Tahmini modeli çıkışıdır.</span><span class="sxs-lookup"><span data-stu-id="b81e5-110">hello chance of rain is hello output of a prepared weather prediction model.</span></span> <span data-ttu-id="b81e5-111">Merhaba modeli geçmiş verileri tooforecast sıcaklık ve nem göre Yağmur olasılığını bağlı yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="b81e5-111">hello model is built upon historic data tooforecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="b81e5-112">Neler</span><span class="sxs-lookup"><span data-stu-id="b81e5-112">What you do</span></span>

- <span data-ttu-id="b81e5-113">Merhaba hava durumu Tahmini modeli bir web hizmeti olarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-113">Deploy hello weather prediction model as a web service.</span></span>
- <span data-ttu-id="b81e5-114">IOT hub'ınızı bir tüketici grubu ekleyerek veri erişimi için hazırlanın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="b81e5-115">Stream Analytics işi oluşturmak ve hello projeye yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="b81e5-115">Create a Stream Analytics job and configure hello job to:</span></span>
  - <span data-ttu-id="b81e5-116">IOT hub'ından sıcaklık ve nem verilerini okur.</span><span class="sxs-lookup"><span data-stu-id="b81e5-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="b81e5-117">Merhaba web hizmeti tooget hello Yağmur fırsat çağırın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-117">Call hello web service tooget hello rain chance.</span></span>
  - <span data-ttu-id="b81e5-118">Merhaba sonuç tooan Azure blob depolama kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b81e5-118">Save hello result tooan Azure blob storage.</span></span>
- <span data-ttu-id="b81e5-119">Microsoft Azure Storage Gezgini tooview hello hava tahmini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-119">Use Microsoft Azure Storage Explorer tooview hello weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="b81e5-120">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="b81e5-120">What you need</span></span>

- <span data-ttu-id="b81e5-121">Öğretici [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md) hangi hello gereksinimleri aşağıdaki kapsayan tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="b81e5-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="b81e5-122">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="b81e5-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="b81e5-123">Azure IOT hub'ı aboneliğinizdeki.</span><span class="sxs-lookup"><span data-stu-id="b81e5-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="b81e5-124">Tooyour Azure IOT hub'ı iletileri gönderir bir istemci uygulaması.</span><span class="sxs-lookup"><span data-stu-id="b81e5-124">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="b81e5-125">Bir Azure Machine Learning Studio hesabı.</span><span class="sxs-lookup"><span data-stu-id="b81e5-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="b81e5-126">([Machine Learning Studio ücretsiz deneyin](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="b81e5-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="b81e5-127">Merhaba hava durumu Tahmini modeli bir web hizmeti olarak dağıtma</span><span class="sxs-lookup"><span data-stu-id="b81e5-127">Deploy hello weather prediction model as a web service</span></span>

1. <span data-ttu-id="b81e5-128">Toohello Git [hava durumu Tahmini modeli sayfasına](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="b81e5-128">Go toohello [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="b81e5-129">Tıklatın **Studio'da Aç** Microsoft Azure Machine Learning Studio'da.</span><span class="sxs-lookup"><span data-stu-id="b81e5-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="b81e5-130">![Açık hello hava durumu Tahmini modeli sayfasında Cortana Intelligence Galerisi](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="b81e5-130">![Open hello weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="b81e5-131">Tıklatın **çalıştırmak** toovalidate hello hello modelinde adımları.</span><span class="sxs-lookup"><span data-stu-id="b81e5-131">Click **Run** toovalidate hello steps in hello model.</span></span> <span data-ttu-id="b81e5-132">Bu adım 2 dakika toocomplete sürebilir.</span><span class="sxs-lookup"><span data-stu-id="b81e5-132">This step might take 2 minutes toocomplete.</span></span>
   <span data-ttu-id="b81e5-133">![Azure Machine Learning Studio'da Aç hello hava durumu Tahmini modeli](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="b81e5-133">![Open hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="b81e5-134">Tıklatın **WEB hizmetini kurma** > **Tahmine dayalı Web hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="b81e5-135">![Azure Machine Learning Studio'da Hello hava durumu tahmini model dağıtma](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="b81e5-135">![Deploy hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="b81e5-136">Merhaba şemada hello sürükleyin **Web hizmeti girişi** modülü hello yakın bir yerde **Score Model** modülü.</span><span class="sxs-lookup"><span data-stu-id="b81e5-136">In hello diagram, drag hello **Web service input** module somewhere near hello **Score Model** module.</span></span>
1. <span data-ttu-id="b81e5-137">Merhaba bağlanmak **Web hizmeti girişi** modülü toohello **Score Model** modülü.</span><span class="sxs-lookup"><span data-stu-id="b81e5-137">Connect hello **Web service input** module toohello **Score Model** module.</span></span>
   <span data-ttu-id="b81e5-138">![Azure Machine Learning Studio'da iki modülleri Bağlan](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="b81e5-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="b81e5-139">Tıklatın **çalıştırmak** toovalidate hello hello modelinde adımları.</span><span class="sxs-lookup"><span data-stu-id="b81e5-139">Click **RUN** toovalidate hello steps in hello model.</span></span>
1. <span data-ttu-id="b81e5-140">Tıklatın **WEB hizmeti Dağıt** bir web hizmeti olarak toodeploy hello modeli.</span><span class="sxs-lookup"><span data-stu-id="b81e5-140">Click **DEPLOY WEB SERVICE** toodeploy hello model as a web service.</span></span>
1. <span data-ttu-id="b81e5-141">Hello modeli Hello Panoda hello karşıdan **Excel 2010 veya önceki çalışma kitabı** için **istek/yanıt**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-141">On hello dashboard of hello model, download hello **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="b81e5-142">Hello karşıdan olun **Excel 2010 veya önceki çalışma kitabı** bilgisayarınızda Excel daha sonraki bir sürümünü çalıştırıyor olsanız bile.</span><span class="sxs-lookup"><span data-stu-id="b81e5-142">Ensure that you download hello **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Merhaba Excel hello istek YANITI uç noktası için karşıdan yükle](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="b81e5-144">Merhaba Excel çalışma kitabını, hello Not **WEB hizmeti URL'si** ve **erişim tuşu**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-144">Open hello Excel workbook, make a note of hello **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="b81e5-145">Oluşturma, yapılandırma ve akış analizi işi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b81e5-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="b81e5-146">Akış Analizi işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b81e5-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="b81e5-147">Merhaba, [Azure portal](https://ms.portal.azure.com/), tıklatın **yeni** > **nesnelerin interneti** > **Stream Analytics işi**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-147">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="b81e5-148">Aşağıdaki bilgilerle hello işi için hello girin.</span><span class="sxs-lookup"><span data-stu-id="b81e5-148">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="b81e5-149">**İş adı**: hello işinin hello adı.</span><span class="sxs-lookup"><span data-stu-id="b81e5-149">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="b81e5-150">Merhaba adı genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b81e5-150">hello name must be globally unique.</span></span>

   <span data-ttu-id="b81e5-151">**Kaynak grubu**: kullanım hello aynı IOT hub'ınızı kullanan kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="b81e5-151">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="b81e5-152">**Konum**: kullanım hello aynı konumu, kaynak grubu olarak.</span><span class="sxs-lookup"><span data-stu-id="b81e5-152">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="b81e5-153">**PIN toodashboard**: kolay erişim tooyour IOT hub'hello panosundan için bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="b81e5-153">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Stream Analytics işi oluşturma](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="b81e5-155">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-155">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="b81e5-156">Bir giriş toohello Stream Analytics işi ekleme</span><span class="sxs-lookup"><span data-stu-id="b81e5-156">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="b81e5-157">Açık hello Stream Analytics işi.</span><span class="sxs-lookup"><span data-stu-id="b81e5-157">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="b81e5-158">Altında **iş topoloji**, tıklatın **girişleri**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="b81e5-159">Merhaba, **girişleri** bölmesinde tıklatın **Ekle**ve ardından aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="b81e5-159">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="b81e5-160">**Giriş diğer adı**: hello hello giriş için benzersiz diğer ad.</span><span class="sxs-lookup"><span data-stu-id="b81e5-160">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="b81e5-161">**Kaynak**: seçin **IOT hub'ı**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="b81e5-162">**Tüketici grubu**: oluşturduğunuz Select hello tüketici grubu.</span><span class="sxs-lookup"><span data-stu-id="b81e5-162">**Consumer group**: Select hello consumer group you created.</span></span>

   ![Azure'da bir giriş toohello Stream Analytics işi ekleme](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="b81e5-164">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-164">Click **Create**.</span></span>

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="b81e5-165">Bir çıkış toohello Stream Analytics işi ekleme</span><span class="sxs-lookup"><span data-stu-id="b81e5-165">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="b81e5-166">Altında **iş topoloji**, tıklatın **çıkışları**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="b81e5-167">Hello içinde **çıkışları** bölmesinde tıklatın **Ekle**ve ardından aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="b81e5-167">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="b81e5-168">**Çıkış diğer adları**: hello hello çıktı için benzersiz diğer ad.</span><span class="sxs-lookup"><span data-stu-id="b81e5-168">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="b81e5-169">**Havuz**: seçin **Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="b81e5-170">**Depolama hesabı**: Merhaba blob depolama alanınızın için depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="b81e5-170">**Storage account**: hello storage account for your blob storage.</span></span> <span data-ttu-id="b81e5-171">Bir depolama hesabı oluşturun veya var olan bir kullanın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="b81e5-172">**Kapsayıcı**: hello blob kaydettiğiniz yere hello kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="b81e5-172">**Container**: hello container where hello blob is saved.</span></span> <span data-ttu-id="b81e5-173">Bir kapsayıcı oluşturmak veya mevcut bir kullanın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="b81e5-174">**Olayı seri hale getirme biçimi**: seçin **CSV**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Azure'da bir çıktı toohello Stream Analytics işi ekleme](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="b81e5-176">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-176">Click **Create**.</span></span>

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a><span data-ttu-id="b81e5-177">Bir işlev toohello dağıttığınız Stream Analytics işi toocall hello web hizmeti Ekle</span><span class="sxs-lookup"><span data-stu-id="b81e5-177">Add a function toohello Stream Analytics job toocall hello web service you deployed</span></span>

1. <span data-ttu-id="b81e5-178">Altında **iş topoloji**, tıklatın **işlevleri** > **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="b81e5-179">Aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="b81e5-179">Enter hello following information:</span></span>

   <span data-ttu-id="b81e5-180">**İşlev diğer**: girin `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="b81e5-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="b81e5-181">**İşlev türü**: seçin **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="b81e5-182">**Alma seçeneği**: seçin **farklı bir abonelik alma**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="b81e5-183">**URL**: hello Excel çalışma kitabından hello aşağı ettiğiniz bir WEB hizmeti URL'si girin.</span><span class="sxs-lookup"><span data-stu-id="b81e5-183">**URL**: Enter hello WEB SERVICE URL that you noted down from hello Excel workbook.</span></span>

   <span data-ttu-id="b81e5-184">**Anahtar**: hello Excel çalışma kitabından hello aşağı ettiğiniz erişim anahtarı girin.</span><span class="sxs-lookup"><span data-stu-id="b81e5-184">**Key**: Enter hello ACCESS KEY that you noted down from hello Excel workbook.</span></span>

   ![Azure'da işlevi toohello akış analizi işi ekleme](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="b81e5-186">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-186">Click **Create**.</span></span>

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="b81e5-187">Merhaba Stream Analytics işi Hello sorgusu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="b81e5-187">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="b81e5-188">Altında **iş topoloji**, tıklatın **sorgu**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="b81e5-189">Merhaba var olan kodu koddan hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="b81e5-189">Replace hello existing code with hello following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="b81e5-190">Değiştir `[YourInputAlias]` hello işin giriş hello diğer adına sahip.</span><span class="sxs-lookup"><span data-stu-id="b81e5-190">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>

   <span data-ttu-id="b81e5-191">Değiştir `[YourOutputAlias]` hello işin hello çıkış diğer adına sahip.</span><span class="sxs-lookup"><span data-stu-id="b81e5-191">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>

1. <span data-ttu-id="b81e5-192">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-192">Click **Save**.</span></span>

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="b81e5-193">Merhaba Stream Analytics işini çalıştır</span><span class="sxs-lookup"><span data-stu-id="b81e5-193">Run hello Stream Analytics job</span></span>

<span data-ttu-id="b81e5-194">Merhaba Stream Analytics işinde tıklatın **Başlat** > **şimdi** > **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-194">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="b81e5-195">Merhaba işi başarıyla başladıktan sonra hello iş durumu değişiklikleri **durduruldu** çok**çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="b81e5-195">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Merhaba Stream Analytics işini çalıştır](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a><span data-ttu-id="b81e5-197">Microsoft Azure Storage Gezgini tooview hello hava tahmini kullanın</span><span class="sxs-lookup"><span data-stu-id="b81e5-197">Use Microsoft Azure Storage Explorer tooview hello weather forecast</span></span>

<span data-ttu-id="b81e5-198">Merhaba istemci uygulaması toostart toplama ve veri tooyour IOT hub sıcaklık ve nem gönderme çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-198">Run hello client application toostart collecting and sending temperature and humidity data tooyour IoT hub.</span></span> <span data-ttu-id="b81e5-199">IOT hub'ınızın aldığı her ileti için hello Stream Analytics işi hello hava tahmini web hizmeti tooproduce hello olasılığını Yağmur çağırır.</span><span class="sxs-lookup"><span data-stu-id="b81e5-199">For each message that your IoT hub receives, hello Stream Analytics job calls hello weather forecast web service tooproduce hello chance of rain.</span></span> <span data-ttu-id="b81e5-200">Merhaba sonuç sonra tooyour Azure blob depolama kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="b81e5-200">hello result is then saved tooyour Azure blob storage.</span></span> <span data-ttu-id="b81e5-201">Azure Storage Gezgini tooview hello sonuç kullanabileceğiniz bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="b81e5-201">Azure Storage Explorer is a tool that you can use tooview hello result.</span></span>

1. <span data-ttu-id="b81e5-202">[Microsoft Azure Storage Gezgini yükleyip](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="b81e5-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="b81e5-203">Azure Depolama Gezgini'ni açın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="b81e5-204">İçinde tooyour Azure hesabı oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-204">Sign in tooyour Azure account.</span></span>
1. <span data-ttu-id="b81e5-205">Aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="b81e5-205">Select your subscription.</span></span>
1. <span data-ttu-id="b81e5-206">Aboneliğinizi tıklayın > **depolama hesapları** > depolama hesabınız > **Blob kapsayıcıları** >, kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="b81e5-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="b81e5-207">Bir .csv dosyası toosee hello sonuç açın.</span><span class="sxs-lookup"><span data-stu-id="b81e5-207">Open a .csv file toosee hello result.</span></span> <span data-ttu-id="b81e5-208">Merhaba son sütun kayıtları Yağmur olasılığını hello.</span><span class="sxs-lookup"><span data-stu-id="b81e5-208">hello last column records hello chance of rain.</span></span>

   ![Azure Machine Learning ile hava tahmini sonucu alın](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="b81e5-210">Özet</span><span class="sxs-lookup"><span data-stu-id="b81e5-210">Summary</span></span>

<span data-ttu-id="b81e5-211">Azure Machine Learning tooproduce hello IOT hub'ınızı alan hello sıcaklık ve nem verilerine dayalı Yağmur olasılığını başarıyla kullandığınız.</span><span class="sxs-lookup"><span data-stu-id="b81e5-211">You’ve successfully used Azure Machine Learning tooproduce hello chance of rain based on hello temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]