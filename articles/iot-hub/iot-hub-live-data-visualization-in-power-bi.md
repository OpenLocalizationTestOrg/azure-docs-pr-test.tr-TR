---
title: "Azure IOT Hub – Power BI algılayıcı verilerini gerçek zamanlı veri Görselleştirme | Microsoft Docs"
description: "Algılayıcı toplanan ve Azure IOT hub'ına gönderilen sıcaklık ve nem verileri görselleştirmek için Power BI kullanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "gerçek zamanlı veri görselleştirme, dinamik veri görselleştirme algılayıcı verileri Görselleştirme"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: b190fea06ffc2406d781c7edad091f097cca9c2d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="22bc0-104">Azure IOT Hub'ın Power BI kullanarak gerçek zamanlı algılayıcı verilerini görselleştirmek</span><span class="sxs-lookup"><span data-stu-id="22bc0-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="22bc0-106">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="22bc0-106">What you learn</span></span>

<span data-ttu-id="22bc0-107">Azure IOT hub'ınızın aldığı Power BI tarafından gerçek zamanlı algılayıcı verilerini görselleştirmek öğrenin.</span><span class="sxs-lookup"><span data-stu-id="22bc0-107">You learn how to visualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="22bc0-108">Web uygulamalarını IOT hub'ınızı verileri görselleştirmek denemek istiyorsanız, lütfen bkz [Azure IOT hub'ı gerçek zamanlı algılayıcı verilerini görselleştirmek için kullanım Azure Web Apps](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="22bc0-108">If you want to try visualize the data in your IoT hub with Web Apps, please see [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="22bc0-109">Neler</span><span class="sxs-lookup"><span data-stu-id="22bc0-109">What you do</span></span>

- <span data-ttu-id="22bc0-110">IOT hub'ınızı bir tüketici grubu ekleyerek veri erişimi için hazırlanın.</span><span class="sxs-lookup"><span data-stu-id="22bc0-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="22bc0-111">Oluşturmak, yapılandırmak ve Power BI hesabınızı IOT hub'ından veri aktarımı için bir akış analizi işi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="22bc0-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub to your Power BI account.</span></span>
- <span data-ttu-id="22bc0-112">Oluşturma ve verileri görselleştirmek için bir Power BI raporu yayımlama.</span><span class="sxs-lookup"><span data-stu-id="22bc0-112">Create and publish a Power BI report to visualize the data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="22bc0-113">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="22bc0-113">What you need</span></span>

- <span data-ttu-id="22bc0-114">Öğretici [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md) , aşağıdaki gereksinimleri ele alınmaktadır tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="22bc0-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="22bc0-115">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="22bc0-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="22bc0-116">Azure IOT hub'ı aboneliğinizdeki.</span><span class="sxs-lookup"><span data-stu-id="22bc0-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="22bc0-117">Azure IOT hub'ına iletileri gönderen bir istemci uygulaması.</span><span class="sxs-lookup"><span data-stu-id="22bc0-117">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="22bc0-118">Power BI hesabınız.</span><span class="sxs-lookup"><span data-stu-id="22bc0-118">A Power BI account.</span></span> <span data-ttu-id="22bc0-119">([Power BI ücretsiz deneyin](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="22bc0-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="22bc0-120">Oluşturma, yapılandırma ve akış analizi işi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="22bc0-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="22bc0-121">Akış Analizi işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="22bc0-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="22bc0-122">Azure Portal'da Yeni'ye tıklayın > nesnelerin interneti > Stream Analytics işi.</span><span class="sxs-lookup"><span data-stu-id="22bc0-122">In the Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="22bc0-123">İş için aşağıdaki bilgileri girin.</span><span class="sxs-lookup"><span data-stu-id="22bc0-123">Enter the following information for the job.</span></span>

   <span data-ttu-id="22bc0-124">**İş adı**: İş adı.</span><span class="sxs-lookup"><span data-stu-id="22bc0-124">**Job name**: The name of the job.</span></span> <span data-ttu-id="22bc0-125">Adın genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="22bc0-125">The name must be globally unique.</span></span>

   <span data-ttu-id="22bc0-126">**Kaynak grubu**: IOT hub'ınızı kullandığı aynı kaynak grubunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="22bc0-126">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="22bc0-127">**Konum**: aynı konumu, kaynak grubu olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="22bc0-127">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="22bc0-128">**Panoya Sabitle**: kolay erişim için bu seçeneği IOT hub'ınıza panodan denetleyin.</span><span class="sxs-lookup"><span data-stu-id="22bc0-128">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Stream Analytics işi oluşturma](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="22bc0-130">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22bc0-130">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="22bc0-131">Bir akış analizi işine giriş Ekle</span><span class="sxs-lookup"><span data-stu-id="22bc0-131">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="22bc0-132">Akış analizi işi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="22bc0-132">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="22bc0-133">Altında **iş topoloji**, tıklatın **girişleri**.</span><span class="sxs-lookup"><span data-stu-id="22bc0-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="22bc0-134">İçinde **girişleri** bölmesinde tıklatın **Ekle**ve ardından aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="22bc0-134">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="22bc0-135">**Giriş diğer adı**: giriş için benzersiz diğer ad.</span><span class="sxs-lookup"><span data-stu-id="22bc0-135">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="22bc0-136">**Kaynak**: seçin **IOT hub'ı**.</span><span class="sxs-lookup"><span data-stu-id="22bc0-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="22bc0-137">**Tüketici grubu**: yeni oluşturduğunuz tüketici grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="22bc0-137">**Consumer group**: Select the consumer group you just created.</span></span>
1. <span data-ttu-id="22bc0-138">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22bc0-138">Click **Create**.</span></span>

   ![Azure akış analizi işine giriş Ekle](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="22bc0-140">Akış analizi işine çıkış ekleme</span><span class="sxs-lookup"><span data-stu-id="22bc0-140">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="22bc0-141">Altında **iş topoloji**, tıklatın **çıkışları**.</span><span class="sxs-lookup"><span data-stu-id="22bc0-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="22bc0-142">İçinde **çıkışları** bölmesinde tıklatın **Ekle**ve ardından aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="22bc0-142">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="22bc0-143">**Çıkış diğer adları**: çıkış için benzersiz diğer ad.</span><span class="sxs-lookup"><span data-stu-id="22bc0-143">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="22bc0-144">**Havuz**: seçin **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="22bc0-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="22bc0-145">Tıklatın **Authorize**ve Power BI hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="22bc0-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="22bc0-146">Yetkilendirildikten sonra aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="22bc0-146">Once authorized, enter the following information:</span></span>

   <span data-ttu-id="22bc0-147">**Çalışma grubu**: hedef grup çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="22bc0-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="22bc0-148">**Veri kümesi adı**: bir veri kümesi adı girin.</span><span class="sxs-lookup"><span data-stu-id="22bc0-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="22bc0-149">**Tablo adı**: Tablo adı girin.</span><span class="sxs-lookup"><span data-stu-id="22bc0-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="22bc0-150">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22bc0-150">Click **Create**.</span></span>

   ![Azure Stream Analytics işinde bir çıktı ekleyin](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="22bc0-152">Stream Analytics işi sorgu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="22bc0-152">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="22bc0-153">Altında **iş topoloji**, tıklatın **sorgu**.</span><span class="sxs-lookup"><span data-stu-id="22bc0-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="22bc0-154">Değiştir `[YourInputAlias]` iş giriş diğer adı ile.</span><span class="sxs-lookup"><span data-stu-id="22bc0-154">Replace `[YourInputAlias]` with the input alias of the job.</span></span>
1. <span data-ttu-id="22bc0-155">Değiştir `[YourOutputAlias]` işinin çıkış diğer adına sahip.</span><span class="sxs-lookup"><span data-stu-id="22bc0-155">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>
1. <span data-ttu-id="22bc0-156">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="22bc0-156">Click **Save**.</span></span>

   ![Azure Stream Analytics işinde sorgu ekleme](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="22bc0-158">Stream Analytics işini çalıştır</span><span class="sxs-lookup"><span data-stu-id="22bc0-158">Run the Stream Analytics job</span></span>

<span data-ttu-id="22bc0-159">Stream Analytics işinde tıklatın **Başlat** > **şimdi** > **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="22bc0-159">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="22bc0-160">İş başarıyla başladıktan sonra iş durumu değişiklikleri **durduruldu** için **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="22bc0-160">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Azure Stream Analytics işini çalıştır](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-to-visualize-the-data"></a><span data-ttu-id="22bc0-162">Oluşturma ve verileri görselleştirmek için bir Power BI raporu yayımlama</span><span class="sxs-lookup"><span data-stu-id="22bc0-162">Create and publish a Power BI report to visualize the data</span></span>

1. <span data-ttu-id="22bc0-163">Örnek uygulama Cihazınızda çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="22bc0-163">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="22bc0-164">Öğreticiler altında başvurabilirsiniz değil, varsa [Cihazınızı](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="22bc0-164">If not, you can refer to the tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="22bc0-165">Oturum açın, [Power BI](https://powerbi.microsoft.com/en-us/) hesabı.</span><span class="sxs-lookup"><span data-stu-id="22bc0-165">Sign in to your [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="22bc0-166">Stream Analytics işi çıkış oluşturduğunuzda ayarladığınız Grup çalışma alanına gidin.</span><span class="sxs-lookup"><span data-stu-id="22bc0-166">Go to the group workspace that you set when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="22bc0-167">Tıklatın **veri kümeleri akış**.</span><span class="sxs-lookup"><span data-stu-id="22bc0-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="22bc0-168">Stream Analytics işi çıkış oluşturduğunuzda, belirttiğiniz listelenen dataset görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="22bc0-168">You should see the listed dataset that you specified when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="22bc0-169">Altında **Eylemler**, bir rapor oluşturmak için önce simgeyi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="22bc0-169">Under **ACTIONS**, click the first icon to create a report.</span></span>

   ![Microsoft Power BI raporu oluşturma](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="22bc0-171">Gerçek zamanlı sıcaklık zamanla göstermek için bir çizgi grafiği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="22bc0-171">Create a line chart to show real-time temperature over time.</span></span>
   1. <span data-ttu-id="22bc0-172">Rapor oluşturma sayfasında bir çizgi grafiği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="22bc0-172">On the report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="22bc0-173">Üzerinde **alanları** bölmesinde, Stream Analytics işi çıkış oluşturduğunuzda belirtilen tablonun genişletin.</span><span class="sxs-lookup"><span data-stu-id="22bc0-173">On the **Fields** pane, expand the table that you specified when you created the output for the Stream Analytics job.</span></span>
   1. <span data-ttu-id="22bc0-174">Sürükleme **EventEnqueuedUtcTime** için **eksen** üzerinde **görselleştirmeleri** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="22bc0-174">Drag **EventEnqueuedUtcTime** to **Axis** on the **Visualizations** pane.</span></span>
   1. <span data-ttu-id="22bc0-175">Sürükleme **sıcaklık** için **değerleri**.</span><span class="sxs-lookup"><span data-stu-id="22bc0-175">Drag **temperature** to **Values**.</span></span>

      <span data-ttu-id="22bc0-176">Şimdi bir çizgi grafiği oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="22bc0-176">Now a line chart is created.</span></span> <span data-ttu-id="22bc0-177">X eksenindeki tarih ve saati UTC saat diliminde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="22bc0-177">The x-axis displays date and time in the UTC time zone.</span></span> <span data-ttu-id="22bc0-178">Y ekseni sıcaklık algılayıcı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="22bc0-178">The y-axis displays temperature from the sensor.</span></span>

      ![Bir çizgi grafiği sıcaklık için bir Microsoft Power BI raporu ekleme](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="22bc0-180">Gerçek zamanlı nem zamanla göstermek için başka bir çizgi grafiği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="22bc0-180">Create another line chart to show real-time humidity over time.</span></span> <span data-ttu-id="22bc0-181">Bunu yapmak için yukarıdaki aynı adımları izleyin ve yerleştirin **EventEnqueuedUtcTime** eksenindeki ve **nem** y ekseni üzerinde.</span><span class="sxs-lookup"><span data-stu-id="22bc0-181">To do this, follow the same steps above and place **EventEnqueuedUtcTime** on the x-axis and **humidity** on the y-axis.</span></span>

   ![Bir çizgi grafiği nem için bir Microsoft Power BI raporu ekleme](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="22bc0-183">Tıklatın **kaydetmek** raporu kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="22bc0-183">Click **Save** to save the report.</span></span>
1. <span data-ttu-id="22bc0-184">Tıklatın **dosya** > **Web'de Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="22bc0-184">Click **File** > **Publish to web**.</span></span>
1. <span data-ttu-id="22bc0-185">Tıklatın **oluşturma katıştırma kodunu**ve ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="22bc0-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="22bc0-186">Rapor bağlantısı sağlanan rapor erişim ve raporu blog'unuza veya Web sitesi tümleştirmek için bir kod parçacığını bir kişiyle paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22bc0-186">You're provided the report link that you can share with anyone for report access and a code snippet to integrate the report into your blog or website.</span></span>

![Microsoft Power BI rapor yayımlayın](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="22bc0-188">Microsoft ayrıca sunar [Power BI mobil uygulamalarından](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) görüntüleme ve Power BI panolarınızı ve raporlarınızı ile etkileşim için mobil Cihazınızda.</span><span class="sxs-lookup"><span data-stu-id="22bc0-188">Microsoft also offers the [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22bc0-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="22bc0-189">Next steps</span></span>

<span data-ttu-id="22bc0-190">Azure IOT hub'ından gerçek zamanlı algılayıcı verilerini görselleştirmek için Power BI başarıyla kullandıysanız.</span><span class="sxs-lookup"><span data-stu-id="22bc0-190">You’ve successfully used Power BI to visualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="22bc0-191">Azure IOT Hub verilerini görselleştirmek için alternatif bir yolu yoktur.</span><span class="sxs-lookup"><span data-stu-id="22bc0-191">There is an alternate way to visualize data from Azure IoT Hub.</span></span> <span data-ttu-id="22bc0-192">Bkz: [Azure IOT hub'ı gerçek zamanlı algılayıcı verilerini görselleştirmek için kullanım Azure Web Apps](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="22bc0-192">See [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
