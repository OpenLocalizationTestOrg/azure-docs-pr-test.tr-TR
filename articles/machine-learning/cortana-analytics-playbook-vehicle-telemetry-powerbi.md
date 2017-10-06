---
title: "araç sağlık ve yürüten aaaPower BI panosuna alışkanlıklarınıza - Azure | Microsoft Docs"
description: "Yürüten alışkanlıklarınıza ve araç sistem durumunu Cortana Intelligence toogain gerçek zamanlı ve Tahmine dayalı Öngörüler Hello özelliklerini kullanın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="dbcfe-103">Araç telemetri analizi çözüm şablon Power BI panosuna kurulum yönergeleri</span><span class="sxs-lookup"><span data-stu-id="dbcfe-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="dbcfe-104">Bu **menü** bu playbook toohello bölümlerde bağlar.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="dbcfe-105">Merhaba araç Telemetri analiz çözümü araba dealerships, otomobil üreticileri ve sigorta şirketler araç sistem durumu ve yürüten Cortana Intelligence toogain gerçek zamanlı ve Tahmine dayalı Öngörüler hello özelliklerini nasıl yararlanabilir genişletilebileceğini gösterir. R & D ve pazarlama kampanyaları hello alanında alışkanlıklarınıza toodrive geliştirmeleri müşteri deneyimi.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-105">hello Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits toodrive improvements in hello area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="dbcfe-106">Bu belge hello çözüm aboneliğinizde dağıtıldıktan sonra hello Power BI raporları ve panoyu nasıl yapılandırabileceğiniz adım adım yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-106">This document contains step by step instructions on how you can configure hello Power BI reports and dashboard once hello solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="dbcfe-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="dbcfe-107">Prerequisites</span></span>
1. <span data-ttu-id="dbcfe-108">Merhaba dağıtmak [Telemetri analizi](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) çözümü</span><span class="sxs-lookup"><span data-stu-id="dbcfe-108">Deploy hello [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="dbcfe-109">Microsoft Power BI Desktop yükleyin</span><span class="sxs-lookup"><span data-stu-id="dbcfe-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="dbcfe-110">Bir [Azure aboneliği](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dbcfe-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="dbcfe-111">Bir Azure aboneliğiniz yoksa, ücretsiz Azure aboneliği ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="dbcfe-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="dbcfe-112">Microsoft Power BI hesabı</span><span class="sxs-lookup"><span data-stu-id="dbcfe-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="dbcfe-113">Cortana Intelligence Suite bileşenleri</span><span class="sxs-lookup"><span data-stu-id="dbcfe-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="dbcfe-114">Merhaba araç Telemetri analizi çözüm şablonu bir parçası olarak, aboneliğinizde Cortana Intelligence Hizmetleri aşağıdaki hello dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-114">As part of hello Vehicle Telemetry Analytics solution template, hello following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="dbcfe-115">**Olay hub'ı** Azure'da araç telemetri olayları milyonlarca alma için.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="dbcfe-116">**Akış analizi** araç sistem üzerinde gerçek zamanlı Öngörüler öğrenilmesi ve bu verileri daha zengin toplu analiz için uzun vadeli depolamaya devam eder.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="dbcfe-117">**Machine Learning** anomali algılama gerçek zamanlı ve toplu toogain Tahmine dayalı Öngörüler işleme.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-117">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="dbcfe-118">**Hdınsight** ölçekte çevrelerini tootransform veriler</span><span class="sxs-lookup"><span data-stu-id="dbcfe-118">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="dbcfe-119">**Veri Fabrikası** planlama, kaynak yönetimi ve izleme hello toplu işleme ardışık orchestration işler.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>

<span data-ttu-id="dbcfe-120">**Power BI** gerçek zamanlı veri ve Tahmine dayalı analiz görselleştirmeleri için zengin bir Pano bu çözümü sunar.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="dbcfe-121">Merhaba çözümü kullanan iki farklı veri kaynakları: **benzetimli araç sinyalleri ve tanılama veri kümesi** ve **araç katalog**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-121">hello solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="dbcfe-122">Bir araç telematik simulator bu çözümün bir parçası olarak dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="dbcfe-123">Tanılama bilgisi yayar ve hello araç ve belirli bir noktada yönlendirmeli düzeni karşılık gelen toohello durumunu zamanında işaret eder.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-123">It emits diagnostic information and signals corresponding toohello state of hello vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="dbcfe-124">Merhaba araç katalog bir başvuru veri kümesi içeren Toplamıdır toomodel eşlemedir</span><span class="sxs-lookup"><span data-stu-id="dbcfe-124">hello Vehicle Catalog is a reference dataset containing VIN toomodel mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="dbcfe-125">Power BI panosuna hazırlama</span><span class="sxs-lookup"><span data-stu-id="dbcfe-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="dbcfe-126">Kurulum Power BI gerçek zamanlı Panosu</span><span class="sxs-lookup"><span data-stu-id="dbcfe-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="dbcfe-127">**Merhaba gerçek zamanlı Pano uygulaması başlangıç** hello dağıtım tamamlandıktan sonra hello el ile işlem yönergeleri izlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-127">**Start hello real-time dashboard application** Once hello deployment is completed, you should follow hello Manual Operation Instructions</span></span>

* <span data-ttu-id="dbcfe-128">Gerçek zamanlı Pano uygulaması RealtimeDashboardApp.zip indirin ve onu sıkıştırmasını açın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="dbcfe-129">Merhaba sıkıştırması açılmış klasöründe, uygulama yapılandırma dosyası 'RealtimeDashboardApp.exe.config' Değiştir appSettings Eventhub, Blob Storage ve ML hizmet bağlantıları hello değerlerle hello el ile işlem yönergeleri ve değişikliklerinizi kaydetmek için açın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-129">In hello unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with hello values in hello Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="dbcfe-130">Uygulama RealtimeDashboardApp.exe çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="dbcfe-131">Bir oturum açma penceresi açılır, geçerli Powerbı kimlik bilgilerinizi sağlayın ve hello tıklatın **kabul** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-131">A login window will pop up, provide your valid PowerBI credentials and click hello **Accept** button.</span></span> <span data-ttu-id="dbcfe-132">Merhaba uygulama toorun sonra başlar.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-132">Then hello app will start toorun.</span></span>

   ![Oturum açma BI tooPower](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Power BI panosuna izinleri](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="dbcfe-135">Oturum açma tooPowerBI Web sitesine gidin ve gerçek zamanlı bir pano oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-135">Login tooPowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="dbcfe-136">Şimdi, hazır tooconfigure hello Power BI panosuna gerçek zamanlı zengin Görselleştirmelerini toogain sahip olduğunuz ve Tahmine dayalı Öngörüler araç sistem durumu ve yürüten alışkanlıklarınıza.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-136">Now, you are ready tooconfigure hello Power BI dashboard with rich visualizations toogain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="dbcfe-137">Tüm hello raporları ve hello Pano yapılandırma tooan saat toocreate yaklaşık 45 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-137">It takes about 45 minutes tooan hour toocreate all hello reports and configure hello dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="dbcfe-138">Power BI raporları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="dbcfe-138">Configure Power BI reports</span></span>
<span data-ttu-id="dbcfe-139">Merhaba gerçek zamanlı raporlar ve hello Pano 30-45 dakika toocomplete hakkında alın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-139">hello real-time reports and hello dashboard take about 30-45 minutes toocomplete.</span></span> <span data-ttu-id="dbcfe-140">Çok Gözat[http://powerbi.com](http://powerbi.com) ve oturum açma.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-140">Browse too[http://powerbi.com](http://powerbi.com) and login.</span></span>

![Oturum açma BI tooPower](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="dbcfe-142">Yeni bir veri kümesi Power BI'da oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="dbcfe-143">Merhaba tıklatın **ConnectedCarsRealtime** veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-143">Click hello **ConnectedCarsRealtime** dataset.</span></span>

![Bağlı eçildiğindeki araba gerçek zamanlı veri kümesi](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="dbcfe-145">Boş bir rapor Hello kullanarak Kaydet **Ctrl + s**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-145">Save hello blank report using **Ctrl + s**.</span></span>

![Boş raporu kaydedin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="dbcfe-147">Rapor adı sağlayın *araç Telemetri analizi gerçek zamanlı - raporları*.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Rapor adı belirtin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="dbcfe-149">Gerçek zamanlı raporları</span><span class="sxs-lookup"><span data-stu-id="dbcfe-149">Real-time reports</span></span>
<span data-ttu-id="dbcfe-150">Bu çözümde üç gerçek zamanlı raporları vardır:</span><span class="sxs-lookup"><span data-stu-id="dbcfe-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="dbcfe-151">İşlemde araçları</span><span class="sxs-lookup"><span data-stu-id="dbcfe-151">Vehicles in operation</span></span>
2. <span data-ttu-id="dbcfe-152">Bakım gerektiren araçları</span><span class="sxs-lookup"><span data-stu-id="dbcfe-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="dbcfe-153">Araçlar sağlık istatistikleri</span><span class="sxs-lookup"><span data-stu-id="dbcfe-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="dbcfe-154">Tüm hello üç gerçek zamanlı raporları tooconfigure seçin veya sonra herhangi bir aşama durdurup hello toplu raporları yapılandırma toohello sonraki bölüme geçin.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-154">You can choose tooconfigure all hello three real-time reports or stop after any stage and proceed toohello next section of configuring hello batch reports.</span></span> <span data-ttu-id="dbcfe-155">Tüm toocreate öneririz hello üç toovisualize hello tam Öngörüler hello çözümün hello gerçek zamanlı yolunun bildirir.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-155">We recommend you toocreate all hello three reports toovisualize hello full insights of hello real-time path of hello solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="dbcfe-156">1. İşlemde araçları</span><span class="sxs-lookup"><span data-stu-id="dbcfe-156">1. Vehicles in operation</span></span>
<span data-ttu-id="dbcfe-157">Çift **sayfa 1** ve çok yeniden adlandırma "Taşıtlardan işleminde"</span><span class="sxs-lookup"><span data-stu-id="dbcfe-157">Double-click **Page 1** and rename it too“Vehicles in operation”</span></span>  
    <span data-ttu-id="dbcfe-158">![Araba - bağlı Taşıtlardan işleminde](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="dbcfe-159">Seçin **toplamıdır** alanının **alanları** ve görselleştirme türü olarak seçin **"Kart"**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="dbcfe-160">Kart görselleştirme şekilde gösterildiği gibi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-160">Card visualization is created as shown in figure.</span></span>  
    ![Bağlı araba - Select toplamıdır](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="dbcfe-162">Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-162">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="dbcfe-163">Seçin **Şehir** ve **toplamıdır** alanlarından.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="dbcfe-164">Görselleştirme çok değiştirme**"Harita"**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-164">Change visualization too**“Map”**.</span></span> <span data-ttu-id="dbcfe-165">Sürükleme **toplamıdır** değerleri alanında.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-165">Drag **vin** in values area.</span></span> <span data-ttu-id="dbcfe-166">Sürükleme **Şehir** alanlarından çok**gösterge** alanı.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-166">Drag **city** from fields too**Legend** area.</span></span>   
    <span data-ttu-id="dbcfe-167">![Araba - kart görselleştirme bağlı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="dbcfe-168">Seçin **biçimi** konusundaki **görselleştirmeleri**, tıklatın **başlık** hello değiştirip **metin** çok**"araçları işlem şehre göre"**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-168">Select **format** section from **Visualizations**, click **Title** and change hello **Text** too**“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="dbcfe-169">![Araba - bağlı Taşıtlardan işlemde şehre göre](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="dbcfe-170">Son görselleştirme şekilde gösterildiği gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-170">Final visualization looks as shown in figure.</span></span>    
    ![Bağlı araba - son Görselleştirme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="dbcfe-172">Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-172">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="dbcfe-173">Seçin **Şehir** ve **toplamıdır**, görselleştirme türünü çok değiştirme**kümelenmiş sütun grafiği**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-173">Select **City** and **vin**, change visualization type too**Clustered Column Chart**.</span></span> <span data-ttu-id="dbcfe-174">Sağlamak **Şehir** alanındaki **eksen alanı** ve **toplamıdır** içinde **alan değeri**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="dbcfe-175">Sıralama grafik tarafından **"Toplamıdır sayısı"**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="dbcfe-176">![Bağlı araba - toplamıdır sayısı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="dbcfe-177">Değişiklik grafik **başlık** çok**"Araçlar işlemde şehre göre"**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-177">Change chart **Title** too**“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="dbcfe-178">Merhaba tıklatın **biçimi** bölümünde sonra seçin **veri renkleri**, hello'ı tıklatın **"Açık"** çok**Tümünü Göster**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-178">Click hello **Format** section, then select **Data Colors**,  Click hello **“On”** too**Show All**</span></span>  
    <span data-ttu-id="dbcfe-179">![Bağlı araba - tüm veri renkleri göster](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="dbcfe-180">Renk simgesine tıklayarak tek tek Şehir Hello rengini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-180">Change hello color of individual city by clicking on color icon.</span></span>  
    ![Araba - değişiklik renkleri bağlı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="dbcfe-182">Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-182">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="dbcfe-183">Seçin **kümelenmiş sütun grafiği** görselleştirmeleri, gelen görselleştirme sürükleyin **Şehir** alanındaki **eksen** alanı **modeli** içinde **gösterge** alan ve **toplamıdır** içinde **değeri** alanı.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="dbcfe-184">![Bağlı araba - kümelenmiş sütun grafiği](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="dbcfe-185">![Bağlı araba - işleme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="dbcfe-186">Bu sayfadaki tüm görselleştirme şekilde gösterildiği gibi yeniden düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Bağlı araba - görselleştirmeleri](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="dbcfe-188">Merhaba "Araçlar işleminde" gerçek zamanlı rapor başarıyla yapılandırdınız.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-188">You have successfully configured hello “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="dbcfe-189">Toocreate hello sonraki gerçek zamanlı rapora devam veya buraya durdurun ve hello Pano yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-189">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="dbcfe-190">2. Bakım gerektiren araçları</span><span class="sxs-lookup"><span data-stu-id="dbcfe-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="dbcfe-191">Tıklatın ![Ekle](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd yeni bir rapor çok yeniden adlandırma**"Taşıtlardan gerektiren bakım"**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd a new report, rename it too**“Vehicles Requiring Maintenance”**</span></span>

![Bağlı araba - bakım gerektiren araçları](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="dbcfe-193">Seçin **toplamıdır** alan ve görselleştirme türünü çok değiştirmek**kartı**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-193">Select **vin** field and change visualization type too**Card**.</span></span>  
    <span data-ttu-id="dbcfe-194">![Bağlı araba - toplamıdır kartı Görselleştirme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="dbcfe-195">Biz hello kümesinde "MaintenanceLabel" adlı bir alana sahip.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-195">We have a field named “MaintenanceLabel” In hello dataset.</span></span> <span data-ttu-id="dbcfe-196">Bu alan "0" veya "1" değeri olabilir."</span><span class="sxs-lookup"><span data-stu-id="dbcfe-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="dbcfe-197">Çözümün bir parçası sağlandı ve hello gerçek zamanlı yolu ile tümleşik hello Azure Machine Learning modeli tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-197">It is set by hello Azure Machine Learning model provisioned as part of solution and integrated with hello real-time path.</span></span> <span data-ttu-id="dbcfe-198">bir araç bakım gerektirir "1" Merhaba değeri gösterir.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-198">hello value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="dbcfe-199">tooadd bir **sayfa düzeyi** bakım gerektiren taşıtlardan verileri göstermek için filtre:</span><span class="sxs-lookup"><span data-stu-id="dbcfe-199">tooadd a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="dbcfe-200">Sürükleme hello **"MaintenanceLabel"** içine alan **sayfa düzeyi filtrelerini**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-200">Drag hello **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="dbcfe-201">![Bağlı araba - sayfa düzeyi filtreleri](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="dbcfe-202">Tıklatın **temel filtreleme** menü MaintenanceLabel sayfa düzeyi filtresi altındaki mevcut.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="dbcfe-203">![Araba - bağlı temel filtreleme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="dbcfe-204">Filtre değeri çok ayarlamak**"1"**  </span><span class="sxs-lookup"><span data-stu-id="dbcfe-204">Set its filter value too**“1”**  </span></span>  
   <span data-ttu-id="dbcfe-205">![Bağlı araba - filtre değeri](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="dbcfe-206">Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-206">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="dbcfe-207">Seçin **kümelenmiş sütun grafiği** görselleştirmeleri gelen</span><span class="sxs-lookup"><span data-stu-id="dbcfe-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="dbcfe-208">![Bağlı araba - Vind kartı Görselleştirme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="dbcfe-209">![Bağlı araba - kümelenmiş sütun grafiği](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="dbcfe-210">Sürükleme alan **modeli** içine **eksen** alanı **toplamıdır** çok**değeri** alanı.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-210">Drag field **Model** into **Axis** area, **Vin** too**Value** area.</span></span> <span data-ttu-id="dbcfe-211">Görselleştirme tarafından sıralama **toplamıdır sayısı**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="dbcfe-212">Değişiklik grafik **başlık** çok**"modeli tarafından bakım gerektiren Taşıtlardan"**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-212">Change chart **Title** too**“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="dbcfe-213">Sürükleme **toplamıdır** içine alanları **doygunluğu** adresindeki mevcut **alanları** ![alanları](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) bölümünü **görselleştirme** sekmesi</span><span class="sxs-lookup"><span data-stu-id="dbcfe-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="dbcfe-214">![Bağlı araba - doygunluğu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="dbcfe-215">Değişiklik **veri renkleri** görselleştirmeleri içinde **biçimi** bölümü</span><span class="sxs-lookup"><span data-stu-id="dbcfe-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="dbcfe-216">Minimum rengini: **F2C812**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="dbcfe-217">Maksimum rengini: **FF6300**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="dbcfe-218">![Araba - renk değişiklikleri bağlı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="dbcfe-219">![Yeni görselleştirme renkleri araba - bağlı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="dbcfe-220">Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-220">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="dbcfe-221">Seçin **kümelenmiş sütun grafiği** görselleştirmeleri sürükleyin **toplamıdır** içine alan **değeri** alanında, sürükle **Şehir** içine alan **eksen** alanı.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="dbcfe-222">Sıralama grafik tarafından **"Toplamıdır sayısı"**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="dbcfe-223">Değişiklik grafik **başlık** çok**"şehre göre bakım gerektiren Taşıtlardan"** </span><span class="sxs-lookup"><span data-stu-id="dbcfe-223">Change chart **Title** too**“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="dbcfe-224">![Bağlı araba - şehre göre bakım gerektiren araçları](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="dbcfe-225">Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-225">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="dbcfe-226">Seçin **çok satır kartı** görselleştirmeleri, gelen görselleştirme sürükleyin **modeli** ve **toplamıdır** hello içine **alanları** alanı.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into hello **Fields** area.</span></span>  
<span data-ttu-id="dbcfe-227">![Bağlı araba - birden çok satır kartı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="dbcfe-228">Tüm hello görselleştirme yeniden düzenleme, hello son raporu şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="dbcfe-228">Rearranging all of hello visualization, hello final report looks as follows:</span></span>  
![Bağlı araba - birden çok satır kartı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="dbcfe-230">Merhaba "Taşıtlardan gerektiren bakım" gerçek zamanlı rapor başarıyla yapılandırdınız.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-230">You have successfully configured hello “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="dbcfe-231">Toocreate hello sonraki gerçek zamanlı rapora devam veya buraya durdurun ve hello Pano yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-231">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="dbcfe-232">3. Araçlar sağlık istatistikleri</span><span class="sxs-lookup"><span data-stu-id="dbcfe-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="dbcfe-233">Tıklatın ![Ekle](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd yeni rapor, çok yeniden adlandırma**"Taşıtlardan sağlık İstatistikleri"**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd new report, rename it too**“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="dbcfe-234">Seçin **ölçer** görselleştirme görselleştirmeleri, öğesinden sonra hello sürükleyin **hızı** içine alan **değeri Minimum, maksimum değer** alanları.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-234">Select **Gauge** visualization from visualizations, then drag hello **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="dbcfe-235">![Bağlı araba - birden çok satır kartı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="dbcfe-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="dbcfe-236">Değiştirme hello varsayılan toplama, **hızı** içinde **değeri alanı** çok**ortalama**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-236">Change hello default aggregation of **speed** in **Value area** too**Average**</span></span> 

<span data-ttu-id="dbcfe-237">Değiştirme hello varsayılan toplama, **hızı** içinde **Minimum alan** çok**en az**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-237">Change hello default aggregation of **speed** in **Minimum area** too**Minimum**</span></span>

<span data-ttu-id="dbcfe-238">Değiştirme hello varsayılan toplama, **hızı** içinde **maksimum alan** çok**maksimum**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-238">Change hello default aggregation of **speed** in **Maximum area** too**Maximum**</span></span>

![Bağlı araba - birden çok satır kartı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="dbcfe-240">Merhaba yeniden adlandırma **ölçer başlık** çok**"Ortalama hızı"**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-240">Rename hello **Gauge Title** too**“Average speed”**</span></span> 

![Bağlı araba - ölçer](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="dbcfe-242">Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-242">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="dbcfe-243">Benzer şekilde ekleme bir **ölçer** için **ortalama altyapısı Petrol**, **ortalama yakıt**, ve **ortalama altyapısı Sıcaklığın**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="dbcfe-244">Değiştirme adımları yukarıda göre her ölçer alanların hello varsayılan toplama **"Ortalama hızı"** ölçer.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-244">Change hello default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Bağlı araba - ölçerler](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="dbcfe-246">Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-246">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="dbcfe-247">Seçin **çizgi ve kümelenmiş sütun grafiği** görselleştirmeleri sonra sürükleyin **Şehir** içine alan **paylaşılan eksen**, sürükleyin **hızı**, **tirepressure ve engineoil alanları** içine **sütun değerlerini** alanı, kendi toplama türü çok değiştirme**ortalama**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type too**Average**.</span></span> 

<span data-ttu-id="dbcfe-248">Sürükleme hello **engineTemperature** içine alan **satır değerleri** alanı hello toplama türü çok değiştirme**ortalama**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-248">Drag hello **engineTemperature** field into **Line Values** area, change hello  aggregation type too**Average**.</span></span> 

![Bağlı araba - görselleştirmeleri alanları](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="dbcfe-250">Değişiklik hello grafik **başlık** çok**"Ortalama hızı, lastiği baskısı, altyapısı Petrol ve altyapısı Sıcaklık"**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-250">Change hello chart **Title** too**“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Bağlı araba - görselleştirmeleri alanları](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="dbcfe-252">Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-252">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="dbcfe-253">Seçin **Treemap** görselleştirmeleri, gelen görselleştirme sürükleyin hello **modeli** hello içine alan **grup** alan ve sürükleme hello alan  **MaintenanceProbability** hello içine **değerleri** alanı.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-253">Select **Treemap** visualization from visualizations, drag hello **Model** field into hello **Group** area, and drag hello field **MaintenanceProbability** into hello **Values** area.</span></span>

<span data-ttu-id="dbcfe-254">Değişiklik hello grafik **başlık** çok**"araç modelleri bakım gerektiren"**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-254">Change hello chart **Title** too**“Vehicle models requiring maintenance”**.</span></span>

![Araba - Grafik Başlığı Değiştir bağlı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="dbcfe-256">Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-256">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="dbcfe-257">Seçin **% 100 Yığılmış grafik** görselleştirme hello sürükleyin **Şehir** hello içine alan **eksen** alan ve sürükleme hello **MaintenanceProbability**, **RecallProbability** hello alanlarına **değeri** alanı.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-257">Select **100% Stacked Bar Chart** from visualization, drag hello **city** field into hello **Axis** area, and drag hello **MaintenanceProbability**, **RecallProbability** fields into hello **Value** area.</span></span>

![Bağlı araba - yeni görselleştirme ekleme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="dbcfe-259">Tıklatın **biçimi**seçin **veri renkleri**ve kümesi hello **MaintenanceProbability** renk toohello değeri **"F2C80F"**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-259">Click **Format**, select **Data Colors**, and set hello **MaintenanceProbability** color toohello value **“F2C80F”**.</span></span>

<span data-ttu-id="dbcfe-260">Değişiklik hello **başlık** Merhaba grafik çok**"Olasılık, araç bakım & geri çağırma tarafından Şehir"**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-260">Change hello **Title** of hello chart too**“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Bağlı araba - yeni görselleştirme ekleme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="dbcfe-262">Merhaba boş alanı tooadd yeni görselleştirme'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-262">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="dbcfe-263">Seçin **alan grafiği** görselleştirmeleri gelen görselleştirme hello sürükleyin **modeli** hello içine alan **eksen** alan ve sürükleme hello **engineOil, tirepressure, hız ve MaintenanceProbability** hello alanlarına **değerleri** alanı.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-263">Select **Area Chart** from visualization from visualizations, drag hello **Model** field into hello **Axis** area, and drag hello **engineOil, tirepressure, speed and MaintenanceProbability** fields into hello **Values** area.</span></span> <span data-ttu-id="dbcfe-264">Toplama tipine çok değiştirme**"Ortalama"**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-264">Change their aggregation type too**“Average”**.</span></span> 

![Bağlı araba - toplama türünü değiştir](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="dbcfe-266">Merhaba grafik Hello başlığını çok değiştirmek**"Ortalama altyapısı petrol, lastiği baskısı, hızlı ve Bakım olasılık modeli tarafından"**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-266">Change hello title of hello chart too**“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Araba - Grafik Başlığı Değiştir bağlı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="dbcfe-268">Merhaba boş alanı tooadd yeni görselleştirme tıklatın:</span><span class="sxs-lookup"><span data-stu-id="dbcfe-268">Click hello blank area tooadd new visualization:</span></span>

1. <span data-ttu-id="dbcfe-269">Seçin **dağılım grafiği** görselleştirme görselleştirmeleri gelen.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="dbcfe-270">Sürükleme hello **modeli** hello içine alan **ayrıntıları** ve **gösterge** alanı.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-270">Drag hello **Model** field into hello **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="dbcfe-271">Sürükleme hello **yakıt** hello içine alan **x ekseni** alanı hello toplama çok değiştirme**ortalama**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-271">Drag hello **fuel** field into hello **X-Axis** area, change hello aggregation too**Average**.</span></span>
4. <span data-ttu-id="dbcfe-272">Sürükleme **engineTemparature** içine **y ekseni alanında**, hello toplama çok değiştirmek**ortalama**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-272">Drag **engineTemparature** into **Y-Axis area**, change hello aggregation too**Average**</span></span>
5. <span data-ttu-id="dbcfe-273">Sürükleme hello **toplamıdır** hello içine alan **boyutu** alanı.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-273">Drag hello **vin** field into hello **Size** area.</span></span>

![Bağlı araba - yeni görselleştirme ekleme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="dbcfe-275">Değişiklik hello grafik **başlık** çok**"Yakıt ortalamalar, modeli tarafından altyapısı Sıcaklık"**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-275">Change hello chart **Title** too**“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Araba - Grafik Başlığı Değiştir bağlı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="dbcfe-277">Merhaba son rapor aşağıda gösterildiği gibi arar.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-277">hello final report will look like as shown below.</span></span>

![Bağlı araba son raporu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a><span data-ttu-id="dbcfe-279">PIN görselleştirmeleri panosundan hello raporları toohello gerçek zamanlı</span><span class="sxs-lookup"><span data-stu-id="dbcfe-279">Pin visualizations from hello reports toohello real-time dashboard</span></span>
<span data-ttu-id="dbcfe-280">Boş bir Pano üzerinde sonraki tooDashboards hello artı simgesine tıklayarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-280">Create a blank dashboard by clicking on hello plus icon next tooDashboards.</span></span> <span data-ttu-id="dbcfe-281">"Araç Telemetri analizi Pano" adı</span><span class="sxs-lookup"><span data-stu-id="dbcfe-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Bağlı araba Panosu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="dbcfe-283">PIN hello görselleştirme raporları toohello Pano yukarıda hello gelen.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-283">Pin hello visualization from hello above reports toohello dashboard.</span></span> 

![Bağlı araba Panosu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="dbcfe-285">Tüm hello üç raporları oluşturulur ve görselleştirmeleri karşılık gelen hello sabitlenmiş toohello Pano olduğunda hello Panosu aşağıdaki gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-285">hello dashboard should look as follows when all hello three reports are created and hello corresponding visualizations are pinned toohello dashboard.</span></span> <span data-ttu-id="dbcfe-286">Tüm hello raporları oluşturmadıysanız panonuz farklı görünebilir.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-286">If you have not created all hello reports, your dashboard could look different.</span></span> 

![Bağlı araba Panosu](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="dbcfe-288">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="dbcfe-288">Congratulations!</span></span> <span data-ttu-id="dbcfe-289">Merhaba gerçek zamanlı Pano başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-289">You have successfully created hello real-time dashboard.</span></span> <span data-ttu-id="dbcfe-290">Tooexecute CarEventGenerator.exe ve RealtimeDashboardApp.exe devam ederken, başlangıç panosunda canlı güncelleştirmeler görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-290">As you continue tooexecute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on hello dashboard.</span></span> <span data-ttu-id="dbcfe-291">Yaklaşık 10 too15 dakika toocomplete hello aşağıdaki adımları gerçekleştirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-291">It should take about 10 too15 minutes toocomplete hello following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="dbcfe-292">Power BI toplu işleme Pano Kurulumu</span><span class="sxs-lookup"><span data-stu-id="dbcfe-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="dbcfe-293">Yaklaşık iki saat (Merhaba hello dağıtımının başarılı tamamlama) hello son tooend toplu işleme ardışık düzen toofinish yürütmesi için alır ve üretilen veri yıl tutarında işlem.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-293">It takes about two hours (from hello successful completion of hello deployment) for hello end tooend batch processing pipeline toofinish execution and process a year worth of generated data.</span></span> <span data-ttu-id="dbcfe-294">Bu nedenle toofinish hello sonraki adımlara devam etmeden önce işleme hello bekleyin.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-294">So wait for hello processing toofinish before proceeding with hello next steps.</span></span> 
> 
> 

<span data-ttu-id="dbcfe-295">**Merhaba Power BI Tasarımcısı dosyasını indirin**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-295">**Download hello Power BI designer file**</span></span>

* <span data-ttu-id="dbcfe-296">Önceden yapılandırılmış bir Power BI Tasarımcısı dosyasına el ile işlem yönergeleri hello dağıtımının bir parçası olarak dahil edilir</span><span class="sxs-lookup"><span data-stu-id="dbcfe-296">A pre-configured Power BI designer file is included as part of hello deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="dbcfe-297">2 arayın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-297">Look for 2.</span></span> <span data-ttu-id="dbcfe-298">Kurulum Powerbı toplu işleme Pano burada adlı toplu işlem Pano için hello Powerbı şablonu yükleyebilir **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-298">Setup PowerBI batch processing dashboard You can download hello PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="dbcfe-299">Yerel olarak Kaydet</span><span class="sxs-lookup"><span data-stu-id="dbcfe-299">Save locally</span></span>

<span data-ttu-id="dbcfe-300">**Power BI raporları yapılandırın**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="dbcfe-301">Açık hello Tasarımcısı dosyasına '**ConnectedCarsPbiReport.pbix**' Power BI Desktop kullanma.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-301">Open hello designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="dbcfe-302">Değil zaten varsa yüklerseniz Power BI Desktop'hello [Power BI Desktop yükleme](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="dbcfe-302">If you do not already have, install hello Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="dbcfe-303">Merhaba tıklatın **Düzenle sorguları**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-303">Click hello **Edit Queries**.</span></span>

![Power BI Sorgu Düzenle](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="dbcfe-305">Merhaba çift **kaynak**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-305">Double-click hello **Source**.</span></span>

![Kümesi Power BI kaynağı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="dbcfe-307">Sunucu bağlantı dizesi hello dağıtımının bir parçası sağlanan hello Azure SQL server ile güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-307">Update Server connection string with hello Azure SQL server that got provisioned as part of hello deployment.</span></span>  <span data-ttu-id="dbcfe-308">Merhaba el ile işlem yönergeleri altında bakın</span><span class="sxs-lookup"><span data-stu-id="dbcfe-308">Look in hello Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="dbcfe-309">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="dbcfe-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="dbcfe-310">Sunucu: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="dbcfe-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="dbcfe-311">Veritabanı: connectedcar</span><span class="sxs-lookup"><span data-stu-id="dbcfe-311">Database: connectedcar</span></span>
    * <span data-ttu-id="dbcfe-312">Kullanıcı adı: kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="dbcfe-312">Username: username</span></span>
    * <span data-ttu-id="dbcfe-313">Parola: SQL server parolanızı Azure portalından yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="dbcfe-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="dbcfe-314">Bırakın **veritabanı** olarak *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-314">Leave **Database** as *connectedcar*.</span></span>

![Set Power BI veritabanı](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="dbcfe-316">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-316">Click **OK**.</span></span>
* <span data-ttu-id="dbcfe-317">Göreceğiniz **Windows kimlik bilgileri** sekmesi seçili varsayılan olarak, çok değiştirme**veritabanı kimlik bilgileri** tıklayarak **veritabanı** sekmesini sağ.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-317">You will see **Windows credential** tab selected by default, change it too**Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="dbcfe-318">Merhaba sağlamak **kullanıcıadı** ve **parola** onun dağıtım kurulumu sırasında belirtilen, Azure SQL veritabanı'nın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-318">Provide hello **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Veritabanı kimlik bilgileri sağlayın](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="dbcfe-320">Tıklatın **Bağlan**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-320">Click **Connect**</span></span>
* <span data-ttu-id="dbcfe-321">Her hello üç kalan sorgu sağ bölmesinde mevcut Hello yukarıdaki adımları yineleyin ve ardından hello veri kaynağı bağlantı ayrıntıları güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-321">Repeat hello above steps for each of hello three remaining queries present at right pane, and then update hello data source connection details.</span></span>
* <span data-ttu-id="dbcfe-322">Tıklatın **kapatın ve yük**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-322">Click **Close and Load**.</span></span> <span data-ttu-id="dbcfe-323">Power BI Desktop dosyası veri kümeleri bağlı tooSQL Azure veritabanı tabloları ' dir.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-323">Power BI Desktop file datasets are connected tooSQL Azure Database tables.</span></span>
* <span data-ttu-id="dbcfe-324">**Kapat** Power BI Desktop dosyası.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-324">**Close** Power BI Desktop file.</span></span>

![Power BI desktop Kapat](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="dbcfe-326">Tıklatın **kaydetmek** düğmesini toosave hello değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-326">Click **Save** button toosave hello changes.</span></span> 

<span data-ttu-id="dbcfe-327">Artık toohello toplu işleme hello çözüm yolunda karşılık gelen tüm hello raporları yapılandırdınız.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-327">You have now configured all hello reports corresponding toohello batch processing path in hello solution.</span></span> 

## <a name="upload-toopowerbicom"></a><span data-ttu-id="dbcfe-328">Çok karşıya*powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="dbcfe-328">Upload too*powerbi.com*</span></span>
1. <span data-ttu-id="dbcfe-329">Toohello Power BI web portalında http://powerbi.com ve oturum açma gidin.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-329">Navigate toohello Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="dbcfe-330">Tıklatın **veri alma**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="dbcfe-331">Merhaba Power BI Desktop dosyası karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-331">Upload hello Power BI Desktop File.</span></span>  
4. <span data-ttu-id="dbcfe-332">tooupload, tıklatın **Veri Al -> dosya alma yerel dosya ->**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-332">tooupload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="dbcfe-333">Toohello gidin **"**ConnectedCarsPbiReport.pbix**"**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-333">Navigate toohello **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="dbcfe-334">Merhaba dosya yüklendikten sonra geri tooyour gittiğinizde Power BI çalışma alanı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-334">Once hello file is uploaded, you will be navigated back tooyour Power BI work space.</span></span>  

<span data-ttu-id="dbcfe-335">Bir veri kümesi, rapor ve boş bir Pano sizin için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="dbcfe-336">PIN grafikleri tooa yeni pano adlı **araç Telemetri analizi Pano** içinde **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-336">Pin charts tooa new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="dbcfe-337">Yukarıda oluşturduğunuz hello boş Pano tıklayın ve ardından toohello gidin **raporları** bölümünde hello yeni rapor karşıya.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-337">Click hello blank dashboard created above and then navigate toohello **Reports** section click hello newly uploaded report.</span></span>  

![Araç Telemetri güç BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="dbcfe-339">**Not hello rapor altı sayfa vardır:**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-339">**Note hello report has six pages:**</span></span>  
<span data-ttu-id="dbcfe-340">Sayfa 1: Araç yoğunluğu</span><span class="sxs-lookup"><span data-stu-id="dbcfe-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="dbcfe-341">Sayfa 2: Gerçek zamanlı araç sistem durumu</span><span class="sxs-lookup"><span data-stu-id="dbcfe-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="dbcfe-342">Sayfa 3: Titizlikle Taşıtlardan güdümlü</span><span class="sxs-lookup"><span data-stu-id="dbcfe-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="dbcfe-343">Sayfa 4: Geri çekilen araçları</span><span class="sxs-lookup"><span data-stu-id="dbcfe-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="dbcfe-344">Sayfa 5: Verimli bir şekilde Taşıtlardan güdümlü yakıt</span><span class="sxs-lookup"><span data-stu-id="dbcfe-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="dbcfe-345">Sayfa 6: Contoso logosu</span><span class="sxs-lookup"><span data-stu-id="dbcfe-345">Page 6: Contoso Logo</span></span>  

![Bağlı araba güç BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="dbcfe-347">**Sayfa 3**, hello aşağıdaki PIN:</span><span class="sxs-lookup"><span data-stu-id="dbcfe-347">**From Page 3**, pin hello following:</span></span>  

1. <span data-ttu-id="dbcfe-348">Toplamıdır sayısı</span><span class="sxs-lookup"><span data-stu-id="dbcfe-348">Count of VIN</span></span>  
   ![Bağlı araba güç BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="dbcfe-350">Agresif taşıtlardan Waterfall grafik model tarafından yönetilen</span><span class="sxs-lookup"><span data-stu-id="dbcfe-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Araç Telemetri - PIN grafikleri 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="dbcfe-352">**Sayfa 5**, hello aşağıdaki PIN:</span><span class="sxs-lookup"><span data-stu-id="dbcfe-352">**From Page 5**, pin hello following:</span></span> 

1. <span data-ttu-id="dbcfe-353">Toplamıdır sayısı</span><span class="sxs-lookup"><span data-stu-id="dbcfe-353">Count of vin</span></span>    
   ![Araç Telemetri - PIN grafikleri 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="dbcfe-355">Verimli taşıtlardan modeli tarafından Yakıt Al: Kümelenmiş sütun grafiği</span><span class="sxs-lookup"><span data-stu-id="dbcfe-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Araç Telemetri - PIN grafik 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="dbcfe-357">**Sayfa 4**, hello aşağıdaki PIN:</span><span class="sxs-lookup"><span data-stu-id="dbcfe-357">**From Page 4**, pin hello following:</span></span>  

1. <span data-ttu-id="dbcfe-358">Toplamıdır sayısı</span><span class="sxs-lookup"><span data-stu-id="dbcfe-358">Count of vin</span></span>  
   ![Araç Telemetri - PIN grafikleri 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="dbcfe-360">Şehir tarafından geri çekilen taşıtlardan model: Treemap</span><span class="sxs-lookup"><span data-stu-id="dbcfe-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Araç Telemetri - PIN grafikleri 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="dbcfe-362">**Sayfa 6**, hello aşağıdaki PIN:</span><span class="sxs-lookup"><span data-stu-id="dbcfe-362">**From Page 6**, pin hello following:</span></span>  

1. <span data-ttu-id="dbcfe-363">Contoso Motors logosu</span><span class="sxs-lookup"><span data-stu-id="dbcfe-363">Contoso Motors logo</span></span>  
   ![Araç Telemetri - PIN grafikleri 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="dbcfe-365">**Merhaba Pano düzenleme**</span><span class="sxs-lookup"><span data-stu-id="dbcfe-365">**Organize hello dashboard**</span></span>  

1. <span data-ttu-id="dbcfe-366">Toohello Pano gidin</span><span class="sxs-lookup"><span data-stu-id="dbcfe-366">Navigate toohello dashboard</span></span>
2. <span data-ttu-id="dbcfe-367">Her grafiğinin üzerine getirin ve hello tam Pano resimde sağlanan hello adlandırma göre yeniden adlandırın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-367">Hover over each chart and rename it based on hello naming provided in hello complete dashboard image below.</span></span> <span data-ttu-id="dbcfe-368">Ayrıca hello grafikleri toolook hello Panosu aşağıdaki gibi geçici taşıyın.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-368">Also move hello charts around toolook like hello dashboard below.</span></span>  
   ![Araç Telemetri - Pano 2 düzenleme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Araç Telemetri güç BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="dbcfe-371">Bu belgede belirtildiği gibi tüm hello raporları oluşturduysanız, hello son tamamlanan Panosu aşağıdaki şekilde hello gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-371">If you have created all hello reports as mentioned in this document, hello final completed dashboard should look like hello following figure.</span></span> 

![Araç Telemetri - Pano 2 düzenleme](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="dbcfe-373">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="dbcfe-373">Congratulations!</span></span> <span data-ttu-id="dbcfe-374">Merhaba raporları başarıyla oluşturdunuz ve Pano toogain gerçek zamanlı, Tahmine dayalı hello ve toplu işlem ınsights araç sistem durumu ve yürüten alışkanlıklarınıza.</span><span class="sxs-lookup"><span data-stu-id="dbcfe-374">You have successfully created hello reports and hello dashboard toogain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
