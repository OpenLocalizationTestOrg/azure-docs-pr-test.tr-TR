---
title: "IOT hub'ı verilerle Azure Machine Learning kullanarak tahmin hava durumu | Microsoft Docs"
description: "Yağmur olasılığını tahmin etmek için kullanımı Azure Machine Learning algılayıcı IOT hub'ınızı toplar sıcaklık ve nem verileri temel alan."
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
ms.openlocfilehash: 50ae54b9476c49b80236e295c0bf244df8236cff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="weather-forecast-using-the-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="ca780-104">IOT hub'ınızı algılayıcı verilerini Azure Machine Learning kullanarak tahmin hava durumu</span><span class="sxs-lookup"><span data-stu-id="ca780-104">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="ca780-106">Machine learning, gelecekteki davranışları, sonuçları ve eğilimleri tahmin etmek için var olan verilerden bilgi bilgisayarlar yardımcı olan veri bilimi bir tekniktir.</span><span class="sxs-lookup"><span data-stu-id="ca780-106">Machine learning is a technique of data science that helps computers learn from existing data to forecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="ca780-107">Azure Machine Learning, tahmine dayalı modelleri analiz çözümleri olarak hızlı bir şekilde oluşturmayı ve dağıtmayı mümkün kılan bulut tabanlı ve tahmine dayalı analiz hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="ca780-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible to quickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="ca780-108">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="ca780-108">What you learn</span></span>

<span data-ttu-id="ca780-109">Azure Machine Learning tahmin (Yağmur olasılığını) hava durumu için nasıl kullanılacağını öğrenin Azure IOT hub'ınızı sıcaklık ve nem verilerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="ca780-109">You learn how to use Azure Machine Learning to do weather forecast (chance of rain) using the temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="ca780-110">Yağmur hazırlıklı hava durumu Tahmini modeli çıktısını şansınızdır.</span><span class="sxs-lookup"><span data-stu-id="ca780-110">The chance of rain is the output of a prepared weather prediction model.</span></span> <span data-ttu-id="ca780-111">Model sıcaklık ve nem göre Yağmur olasılığını tahmin için geçmiş verilerin üzerine yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="ca780-111">The model is built upon historic data to forecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="ca780-112">Neler</span><span class="sxs-lookup"><span data-stu-id="ca780-112">What you do</span></span>

- <span data-ttu-id="ca780-113">Hava durumu Tahmini modeli bir web hizmeti olarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="ca780-113">Deploy the weather prediction model as a web service.</span></span>
- <span data-ttu-id="ca780-114">IOT hub'ınızı bir tüketici grubu ekleyerek veri erişimi için hazırlanın.</span><span class="sxs-lookup"><span data-stu-id="ca780-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="ca780-115">Stream Analytics işi oluşturmak ve işi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="ca780-115">Create a Stream Analytics job and configure the job to:</span></span>
  - <span data-ttu-id="ca780-116">IOT hub'ından sıcaklık ve nem verilerini okur.</span><span class="sxs-lookup"><span data-stu-id="ca780-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="ca780-117">Yağmur fırsat almak için web hizmeti çağrısı.</span><span class="sxs-lookup"><span data-stu-id="ca780-117">Call the web service to get the rain chance.</span></span>
  - <span data-ttu-id="ca780-118">Sonuç bir Azure blob depolama alanına kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ca780-118">Save the result to an Azure blob storage.</span></span>
- <span data-ttu-id="ca780-119">Microsoft Azure Storage Gezgini hava tahmini görüntülemek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca780-119">Use Microsoft Azure Storage Explorer to view the weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ca780-120">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="ca780-120">What you need</span></span>

- <span data-ttu-id="ca780-121">Öğretici [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md) , aşağıdaki gereksinimleri ele alınmaktadır tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="ca780-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="ca780-122">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="ca780-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="ca780-123">Azure IOT hub'ı aboneliğinizdeki.</span><span class="sxs-lookup"><span data-stu-id="ca780-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="ca780-124">Azure IOT hub'ına iletileri gönderen bir istemci uygulaması.</span><span class="sxs-lookup"><span data-stu-id="ca780-124">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="ca780-125">Bir Azure Machine Learning Studio hesabı.</span><span class="sxs-lookup"><span data-stu-id="ca780-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="ca780-126">([Machine Learning Studio ücretsiz deneyin](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="ca780-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-the-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="ca780-127">Bir web hizmeti olarak hava durumu Tahmini modeli dağıtın</span><span class="sxs-lookup"><span data-stu-id="ca780-127">Deploy the weather prediction model as a web service</span></span>

1. <span data-ttu-id="ca780-128">Git [hava durumu Tahmini modeli sayfasına](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="ca780-128">Go to the [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="ca780-129">Tıklatın **Studio'da Aç** Microsoft Azure Machine Learning Studio'da.</span><span class="sxs-lookup"><span data-stu-id="ca780-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="ca780-130">![Cortana Intelligence Galerisi'nde hava durumu Tahmini modeli sayfasını açın](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="ca780-130">![Open the weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="ca780-131">' I tıklatın **çalıştırmak** model adımlarda doğrulanacak.</span><span class="sxs-lookup"><span data-stu-id="ca780-131">Click **Run** to validate the steps in the model.</span></span> <span data-ttu-id="ca780-132">Bu adımı tamamlamak için 2 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ca780-132">This step might take 2 minutes to complete.</span></span>
   <span data-ttu-id="ca780-133">![Azure Machine Learning Studio'da hava durumu Tahmini modeli açın](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="ca780-133">![Open the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="ca780-134">Tıklatın **WEB hizmetini kurma** > **Tahmine dayalı Web hizmeti**.</span><span class="sxs-lookup"><span data-stu-id="ca780-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="ca780-135">![Azure Machine Learning Studio'da hava durumu Tahmini modeli dağıtın](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="ca780-135">![Deploy the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="ca780-136">Diyagramda sürükleyin **Web hizmeti girişi** yakın bir yerde Modülü **Score Model** modülü.</span><span class="sxs-lookup"><span data-stu-id="ca780-136">In the diagram, drag the **Web service input** module somewhere near the **Score Model** module.</span></span>
1. <span data-ttu-id="ca780-137">Bağlantı **Web hizmeti girişi** modülüne **Score Model** modülü.</span><span class="sxs-lookup"><span data-stu-id="ca780-137">Connect the **Web service input** module to the **Score Model** module.</span></span>
   <span data-ttu-id="ca780-138">![Azure Machine Learning Studio'da iki modülleri Bağlan](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="ca780-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="ca780-139">' I tıklatın **çalıştırmak** model adımlarda doğrulanacak.</span><span class="sxs-lookup"><span data-stu-id="ca780-139">Click **RUN** to validate the steps in the model.</span></span>
1. <span data-ttu-id="ca780-140">Tıklatın **WEB hizmeti Dağıt** bir web hizmeti olarak modeli dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="ca780-140">Click **DEPLOY WEB SERVICE** to deploy the model as a web service.</span></span>
1. <span data-ttu-id="ca780-141">Model Panoda karşıdan **Excel 2010 veya önceki çalışma kitabı** için **istek/yanıt**.</span><span class="sxs-lookup"><span data-stu-id="ca780-141">On the dashboard of the model, download the **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="ca780-142">Karşıdan yüklediğiniz olun **Excel 2010 veya önceki çalışma kitabı** bilgisayarınızda Excel daha sonraki bir sürümünü çalıştırıyor olsanız bile.</span><span class="sxs-lookup"><span data-stu-id="ca780-142">Ensure that you download the **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![İstek YANITI uç noktası için Excel indirin](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="ca780-144">Excel çalışma kitabı açın, Not **WEB hizmeti URL'si** ve **erişim tuşu**.</span><span class="sxs-lookup"><span data-stu-id="ca780-144">Open the Excel workbook, make a note of the **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="ca780-145">Oluşturma, yapılandırma ve akış analizi işi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ca780-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="ca780-146">Akış Analizi işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca780-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="ca780-147">İçinde [Azure portal](https://ms.portal.azure.com/), tıklatın **yeni** > **nesnelerin interneti** > **Stream Analytics işi**.</span><span class="sxs-lookup"><span data-stu-id="ca780-147">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="ca780-148">İş için aşağıdaki bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="ca780-148">Enter the following information for the job.</span></span>

   <span data-ttu-id="ca780-149">**İş adı**: İş adı.</span><span class="sxs-lookup"><span data-stu-id="ca780-149">**Job name**: The name of the job.</span></span> <span data-ttu-id="ca780-150">Adın genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca780-150">The name must be globally unique.</span></span>

   <span data-ttu-id="ca780-151">**Kaynak grubu**: IOT hub'ınızı kullandığı aynı kaynak grubunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca780-151">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="ca780-152">**Konum**: aynı konumu, kaynak grubu olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca780-152">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="ca780-153">**Panoya Sabitle**: kolay erişim için bu seçeneği IOT hub'ınıza panodan denetleyin.</span><span class="sxs-lookup"><span data-stu-id="ca780-153">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Stream Analytics işi oluşturma](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="ca780-155">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca780-155">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="ca780-156">Bir akış analizi işine giriş Ekle</span><span class="sxs-lookup"><span data-stu-id="ca780-156">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="ca780-157">Akış analizi işi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="ca780-157">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="ca780-158">Altında **iş topoloji**, tıklatın **girişleri**.</span><span class="sxs-lookup"><span data-stu-id="ca780-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="ca780-159">İçinde **girişleri** bölmesinde tıklatın **Ekle**ve ardından aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="ca780-159">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="ca780-160">**Giriş diğer adı**: giriş için benzersiz diğer ad.</span><span class="sxs-lookup"><span data-stu-id="ca780-160">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="ca780-161">**Kaynak**: seçin **IOT hub'ı**.</span><span class="sxs-lookup"><span data-stu-id="ca780-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="ca780-162">**Tüketici grubu**: oluşturduğunuz tüketici grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="ca780-162">**Consumer group**: Select the consumer group you created.</span></span>

   ![Azure akış analizi işine giriş Ekle](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="ca780-164">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca780-164">Click **Create**.</span></span>

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="ca780-165">Akış analizi işine çıkış ekleme</span><span class="sxs-lookup"><span data-stu-id="ca780-165">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="ca780-166">Altında **iş topoloji**, tıklatın **çıkışları**.</span><span class="sxs-lookup"><span data-stu-id="ca780-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="ca780-167">İçinde **çıkışları** bölmesinde tıklatın **Ekle**ve ardından aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="ca780-167">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="ca780-168">**Çıkış diğer adları**: çıkış için benzersiz diğer ad.</span><span class="sxs-lookup"><span data-stu-id="ca780-168">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="ca780-169">**Havuz**: seçin **Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="ca780-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="ca780-170">**Depolama hesabı**: blob depolama alanınızın için depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="ca780-170">**Storage account**: The storage account for your blob storage.</span></span> <span data-ttu-id="ca780-171">Bir depolama hesabı oluşturun veya var olan bir kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca780-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="ca780-172">**Kapsayıcı**: blob kaydettiğiniz yere kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="ca780-172">**Container**: The container where the blob is saved.</span></span> <span data-ttu-id="ca780-173">Bir kapsayıcı oluşturmak veya mevcut bir kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca780-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="ca780-174">**Olayı seri hale getirme biçimi**: seçin **CSV**.</span><span class="sxs-lookup"><span data-stu-id="ca780-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Azure Stream Analytics işinde bir çıktı ekleyin](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="ca780-176">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca780-176">Click **Create**.</span></span>

### <a name="add-a-function-to-the-stream-analytics-job-to-call-the-web-service-you-deployed"></a><span data-ttu-id="ca780-177">Bir işlev dağıttığınız web hizmetini çağırmak için Stream Analytics işi ekleme</span><span class="sxs-lookup"><span data-stu-id="ca780-177">Add a function to the Stream Analytics job to call the web service you deployed</span></span>

1. <span data-ttu-id="ca780-178">Altında **iş topoloji**, tıklatın **işlevleri** > **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ca780-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="ca780-179">Aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="ca780-179">Enter the following information:</span></span>

   <span data-ttu-id="ca780-180">**İşlev diğer**: girin `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="ca780-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="ca780-181">**İşlev türü**: seçin **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="ca780-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="ca780-182">**Alma seçeneği**: seçin **farklı bir abonelik alma**.</span><span class="sxs-lookup"><span data-stu-id="ca780-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="ca780-183">**URL**: Excel çalışma kitabından aşağı ettiğiniz WEB hizmeti URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="ca780-183">**URL**: Enter the WEB SERVICE URL that you noted down from the Excel workbook.</span></span>

   <span data-ttu-id="ca780-184">**Anahtar**: Excel çalışma kitabından aşağı ettiğiniz erişim ANAHTARINI girin.</span><span class="sxs-lookup"><span data-stu-id="ca780-184">**Key**: Enter the ACCESS KEY that you noted down from the Excel workbook.</span></span>

   ![Azure Stream Analytics işinde işlevi ekleme](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="ca780-186">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca780-186">Click **Create**.</span></span>

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="ca780-187">Stream Analytics işi sorgu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ca780-187">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="ca780-188">Altında **iş topoloji**, tıklatın **sorgu**.</span><span class="sxs-lookup"><span data-stu-id="ca780-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="ca780-189">Var olan kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ca780-189">Replace the existing code with the following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="ca780-190">Değiştir `[YourInputAlias]` iş giriş diğer adı ile.</span><span class="sxs-lookup"><span data-stu-id="ca780-190">Replace `[YourInputAlias]` with the input alias of the job.</span></span>

   <span data-ttu-id="ca780-191">Değiştir `[YourOutputAlias]` işinin çıkış diğer adına sahip.</span><span class="sxs-lookup"><span data-stu-id="ca780-191">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>

1. <span data-ttu-id="ca780-192">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca780-192">Click **Save**.</span></span>

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="ca780-193">Stream Analytics işini çalıştır</span><span class="sxs-lookup"><span data-stu-id="ca780-193">Run the Stream Analytics job</span></span>

<span data-ttu-id="ca780-194">Stream Analytics işinde tıklatın **Başlat** > **şimdi** > **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="ca780-194">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="ca780-195">İş başarıyla başladıktan sonra iş durumu değişiklikleri **durduruldu** için **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="ca780-195">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Stream Analytics işini çalıştır](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-to-view-the-weather-forecast"></a><span data-ttu-id="ca780-197">Microsoft Azure Storage Gezgini hava tahmini görüntülemek için kullanın</span><span class="sxs-lookup"><span data-stu-id="ca780-197">Use Microsoft Azure Storage Explorer to view the weather forecast</span></span>

<span data-ttu-id="ca780-198">Toplama ve IOT hub'ınıza sıcaklık ve nem veri göndermeye başlaması için istemci uygulaması çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ca780-198">Run the client application to start collecting and sending temperature and humidity data to your IoT hub.</span></span> <span data-ttu-id="ca780-199">IOT hub'ınızın aldığı her ileti için Stream Analytics işi Yağmur olasılığını üretmek için hava tahmini web hizmetini çağırır.</span><span class="sxs-lookup"><span data-stu-id="ca780-199">For each message that your IoT hub receives, the Stream Analytics job calls the weather forecast web service to produce the chance of rain.</span></span> <span data-ttu-id="ca780-200">Sonuç daha sonra Azure blob depolama alanına kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="ca780-200">The result is then saved to your Azure blob storage.</span></span> <span data-ttu-id="ca780-201">Azure Storage Gezgini sonucu görüntülemek için kullanabileceğiniz bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="ca780-201">Azure Storage Explorer is a tool that you can use to view the result.</span></span>

1. <span data-ttu-id="ca780-202">[Microsoft Azure Storage Gezgini yükleyip](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="ca780-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="ca780-203">Azure Depolama Gezgini'ni açın.</span><span class="sxs-lookup"><span data-stu-id="ca780-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="ca780-204">Azure hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ca780-204">Sign in to your Azure account.</span></span>
1. <span data-ttu-id="ca780-205">Aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="ca780-205">Select your subscription.</span></span>
1. <span data-ttu-id="ca780-206">Aboneliğinizi tıklayın > **depolama hesapları** > depolama hesabınız > **Blob kapsayıcıları** >, kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="ca780-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="ca780-207">Sonuç görmek için bir .csv dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="ca780-207">Open a .csv file to see the result.</span></span> <span data-ttu-id="ca780-208">Son sütun Yağmur olasılığını kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ca780-208">The last column records the chance of rain.</span></span>

   ![Azure Machine Learning ile hava tahmini sonucu alın](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="ca780-210">Özet</span><span class="sxs-lookup"><span data-stu-id="ca780-210">Summary</span></span>

<span data-ttu-id="ca780-211">IOT hub'ınızı alan sıcaklık ve nem verilerine dayalı Yağmur olasılığını üretmek için Azure Machine Learning başarıyla kullandıysanız.</span><span class="sxs-lookup"><span data-stu-id="ca780-211">You’ve successfully used Azure Machine Learning to produce the chance of rain based on the temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]