---
title: "Azure IOT Hub – Power BI algılayıcı verilerini aaaReal zaman veri Görselleştirme | Microsoft Docs"
description: "Hello algılayıcı ' toplanan ve tooyour Azure IOT hub gönderilen Power BI toovisualize sıcaklık ve nem verileri kullanın."
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
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="9fdb1-104">Azure IOT Hub'ın Power BI kullanarak gerçek zamanlı algılayıcı verilerini görselleştirmek</span><span class="sxs-lookup"><span data-stu-id="9fdb1-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="9fdb1-106">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="9fdb1-106">What you learn</span></span>

<span data-ttu-id="9fdb1-107">Hakkında bilgi edineceksiniz nasıl Azure IOT hub'ınızı alan toovisualize gerçek zamanlı algılayıcı verilerini Power BI tarafından.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-107">You learn how toovisualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="9fdb1-108">Tootry istiyorsanız hello veri görselleştirme IOT hub'ınıza Web uygulamalarıyla, lütfen bkz. [kullanım Azure Web Apps toovisualize gerçek zamanlı algılayıcı verileri Azure IOT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="9fdb1-108">If you want tootry visualize hello data in your IoT hub with Web Apps, please see [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="9fdb1-109">Neler</span><span class="sxs-lookup"><span data-stu-id="9fdb1-109">What you do</span></span>

- <span data-ttu-id="9fdb1-110">IOT hub'ınızı bir tüketici grubu ekleyerek veri erişimi için hazırlanın.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="9fdb1-111">Oluşturmak, yapılandırmak ve veri aktarımı için Stream Analytics işi, IOT hub tooyour Power BI hesabınızı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub tooyour Power BI account.</span></span>
- <span data-ttu-id="9fdb1-112">Oluşturma ve Power BI rapor toovisualize hello veri yayımlama.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-112">Create and publish a Power BI report toovisualize hello data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9fdb1-113">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="9fdb1-113">What you need</span></span>

- <span data-ttu-id="9fdb1-114">Öğretici [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md) hangi hello gereksinimleri aşağıdaki kapsayan tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="9fdb1-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="9fdb1-115">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="9fdb1-116">Azure IOT hub'ı aboneliğinizdeki.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="9fdb1-117">Tooyour Azure IOT hub'ı iletileri gönderir bir istemci uygulaması.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-117">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="9fdb1-118">Power BI hesabınız.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-118">A Power BI account.</span></span> <span data-ttu-id="9fdb1-119">([Power BI ücretsiz deneyin](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="9fdb1-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="9fdb1-120">Oluşturma, yapılandırma ve akış analizi işi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9fdb1-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="9fdb1-121">Akış Analizi işi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9fdb1-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="9fdb1-122">İçinde Azure portal Merhaba, yeni tıklayın > nesnelerin interneti > Stream Analytics işi.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-122">In hello Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="9fdb1-123">Aşağıdaki bilgilerle hello işi için hello girin.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-123">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="9fdb1-124">**İş adı**: hello işinin hello adı.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-124">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="9fdb1-125">Merhaba adı genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-125">hello name must be globally unique.</span></span>

   <span data-ttu-id="9fdb1-126">**Kaynak grubu**: kullanım hello aynı IOT hub'ınızı kullanan kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-126">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="9fdb1-127">**Konum**: kullanım hello aynı konumu, kaynak grubu olarak.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-127">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="9fdb1-128">**PIN toodashboard**: kolay erişim tooyour IOT hub'hello panosundan için bu seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-128">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Stream Analytics işi oluşturma](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="9fdb1-130">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-130">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="9fdb1-131">Bir giriş toohello Stream Analytics işi ekleme</span><span class="sxs-lookup"><span data-stu-id="9fdb1-131">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="9fdb1-132">Açık hello Stream Analytics işi.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-132">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="9fdb1-133">Altında **iş topoloji**, tıklatın **girişleri**.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="9fdb1-134">Merhaba, **girişleri** bölmesinde tıklatın **Ekle**ve ardından aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="9fdb1-134">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="9fdb1-135">**Giriş diğer adı**: hello hello giriş için benzersiz diğer ad.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-135">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="9fdb1-136">**Kaynak**: seçin **IOT hub'ı**.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="9fdb1-137">**Tüketici grubu**: yeni oluşturduğunuz Select hello tüketici grubu.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-137">**Consumer group**: Select hello consumer group you just created.</span></span>
1. <span data-ttu-id="9fdb1-138">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-138">Click **Create**.</span></span>

   ![Azure'da bir giriş tooa Stream Analytics işi ekleme](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="9fdb1-140">Bir çıkış toohello Stream Analytics işi ekleme</span><span class="sxs-lookup"><span data-stu-id="9fdb1-140">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="9fdb1-141">Altında **iş topoloji**, tıklatın **çıkışları**.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="9fdb1-142">Hello içinde **çıkışları** bölmesinde tıklatın **Ekle**ve ardından aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="9fdb1-142">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="9fdb1-143">**Çıkış diğer adları**: hello hello çıktı için benzersiz diğer ad.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-143">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="9fdb1-144">**Havuz**: seçin **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="9fdb1-145">Tıklatın **Authorize**ve Power BI hesabınızda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="9fdb1-146">Yetkilendirildikten sonra aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="9fdb1-146">Once authorized, enter hello following information:</span></span>

   <span data-ttu-id="9fdb1-147">**Çalışma grubu**: hedef grup çalışma alanınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="9fdb1-148">**Veri kümesi adı**: bir veri kümesi adı girin.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="9fdb1-149">**Tablo adı**: Tablo adı girin.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="9fdb1-150">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-150">Click **Create**.</span></span>

   ![Azure'da bir çıktı tooa Stream Analytics işi ekleme](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="9fdb1-152">Merhaba Stream Analytics işi Hello sorgusu yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9fdb1-152">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="9fdb1-153">Altında **iş topoloji**, tıklatın **sorgu**.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="9fdb1-154">Değiştir `[YourInputAlias]` hello işin giriş hello diğer adına sahip.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-154">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>
1. <span data-ttu-id="9fdb1-155">Değiştir `[YourOutputAlias]` hello işin hello çıkış diğer adına sahip.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-155">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>
1. <span data-ttu-id="9fdb1-156">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-156">Click **Save**.</span></span>

   ![Azure'da bir sorgu tooa Stream Analytics işi ekleme](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="9fdb1-158">Merhaba Stream Analytics işini çalıştır</span><span class="sxs-lookup"><span data-stu-id="9fdb1-158">Run hello Stream Analytics job</span></span>

<span data-ttu-id="9fdb1-159">Merhaba Stream Analytics işinde tıklatın **Başlat** > **şimdi** > **Başlat**.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-159">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="9fdb1-160">Merhaba işi başarıyla başladıktan sonra hello iş durumu değişiklikleri **durduruldu** çok**çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-160">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Azure Stream Analytics işini çalıştır](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a><span data-ttu-id="9fdb1-162">Oluşturma ve bir Power BI rapor toovisualize hello verileri yayımlama</span><span class="sxs-lookup"><span data-stu-id="9fdb1-162">Create and publish a Power BI report toovisualize hello data</span></span>

1. <span data-ttu-id="9fdb1-163">Merhaba örnek uygulaması aygıtınızda çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-163">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="9fdb1-164">Toohello öğreticileri altında başvurabilir, varsa [Cihazınızı](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="9fdb1-164">If not, you can refer toohello tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="9fdb1-165">İçinde tooyour oturum [Power BI](https://powerbi.microsoft.com/en-us/) hesabı.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-165">Sign in tooyour [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="9fdb1-166">Merhaba çıktı hello Stream Analytics işi için oluşturduğunuzda ayarladığınız toohello Grup çalışma alanına gidin.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-166">Go toohello group workspace that you set when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="9fdb1-167">Tıklatın **veri kümeleri akış**.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="9fdb1-168">Merhaba Stream Analytics işi çıkış hello oluşturduğunuzda belirttiğiniz listelenen hello dataset görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-168">You should see hello listed dataset that you specified when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="9fdb1-169">Altında **Eylemler**, hello ilk simge toocreate bir raporu tıklatın.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-169">Under **ACTIONS**, click hello first icon toocreate a report.</span></span>

   ![Microsoft Power BI raporu oluşturma](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="9fdb1-171">Bir çizgi grafiği tooshow gerçek zamanlı sıcaklık zamanla oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-171">Create a line chart tooshow real-time temperature over time.</span></span>
   1. <span data-ttu-id="9fdb1-172">Merhaba rapor oluşturma sayfasında bir çizgi grafiği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-172">On hello report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="9fdb1-173">Merhaba üzerinde **alanları** bölmesinde hello çıktı hello Stream Analytics işi için oluşturduğunuzda belirttiğiniz hello tablosunu genişletin.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-173">On hello **Fields** pane, expand hello table that you specified when you created hello output for hello Stream Analytics job.</span></span>
   1. <span data-ttu-id="9fdb1-174">Sürükleme **EventEnqueuedUtcTime** çok**eksen** hello üzerinde **görselleştirmeleri** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-174">Drag **EventEnqueuedUtcTime** too**Axis** on hello **Visualizations** pane.</span></span>
   1. <span data-ttu-id="9fdb1-175">Sürükleme **sıcaklık** çok**değerleri**.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-175">Drag **temperature** too**Values**.</span></span>

      <span data-ttu-id="9fdb1-176">Şimdi bir çizgi grafiği oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-176">Now a line chart is created.</span></span> <span data-ttu-id="9fdb1-177">Merhaba x ekseni hello UTC saat diliminde tarih ve saati görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-177">hello x-axis displays date and time in hello UTC time zone.</span></span> <span data-ttu-id="9fdb1-178">Merhaba y ekseni hello algılayıcı sıcaklık görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-178">hello y-axis displays temperature from hello sensor.</span></span>

      ![Bir çizgi grafiği için sıcaklık tooa Microsoft Power BI raporu ekleme](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="9fdb1-180">Başka bir çizgi grafiği tooshow gerçek zamanlı nem zamanla oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-180">Create another line chart tooshow real-time humidity over time.</span></span> <span data-ttu-id="9fdb1-181">toodo Bu, aynı adımları yukarıda hello izleyin ve yerleştirin **EventEnqueuedUtcTime** hello x ekseni üzerinde ve **nem** hello y ekseni üzerinde.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-181">toodo this, follow hello same steps above and place **EventEnqueuedUtcTime** on hello x-axis and **humidity** on hello y-axis.</span></span>

   ![Bir çizgi grafiği için nem tooa Microsoft Power BI raporu ekleme](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="9fdb1-183">Tıklatın **kaydetmek** toosave hello rapor.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-183">Click **Save** toosave hello report.</span></span>
1. <span data-ttu-id="9fdb1-184">Tıklatın **dosya** > **tooweb yayımlama**.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-184">Click **File** > **Publish tooweb**.</span></span>
1. <span data-ttu-id="9fdb1-185">Tıklatın **oluşturma katıştırma kodunu**ve ardından **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="9fdb1-186">Web günlüğünüze veya Web sitesi herkes rapor erişim ve bir kod parçacığı toointegrate hello raporu ile paylaşabilir hello rapor bağlantısı sağlanan.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-186">You're provided hello report link that you can share with anyone for report access and a code snippet toointegrate hello report into your blog or website.</span></span>

![Microsoft Power BI rapor yayımlayın](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="9fdb1-188">Microsoft ayrıca hello sunar [Power BI mobil uygulamalarından](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) görüntüleme ve Power BI panolarınızı ve raporlarınızı ile etkileşim için mobil Cihazınızda.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-188">Microsoft also offers hello [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fdb1-189">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9fdb1-189">Next steps</span></span>

<span data-ttu-id="9fdb1-190">Azure IOT hub'ından Power BI toovisualize gerçek zamanlı algılayıcı verilerini başarıyla kullanmış olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-190">You’ve successfully used Power BI toovisualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="9fdb1-191">Azure IOT hub'ı bir alternatif bir yol toovisualize verileri yoktur.</span><span class="sxs-lookup"><span data-stu-id="9fdb1-191">There is an alternate way toovisualize data from Azure IoT Hub.</span></span> <span data-ttu-id="9fdb1-192">Bkz: [kullanım Azure Web Apps toovisualize gerçek zamanlı algılayıcı verileri Azure IOT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="9fdb1-192">See [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
