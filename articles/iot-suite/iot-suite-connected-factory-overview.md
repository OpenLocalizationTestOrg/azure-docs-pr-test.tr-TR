---
title: "Azure IoT Paketi bağlı fabrikaya genel bakış | Microsoft Docs"
description: "Azure IoT Paketi önceden yapılandırılmış bağlı fabrika çözümü açıklaması."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: d502c8e2e2715899279f6ebcf7ed89c19a1bb9a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-connected-factory-preconfigured-solution"></a><span data-ttu-id="45f04-103">Önceden yapılandırılmış bağlı fabrika çözümlerini kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="45f04-103">Get started with the connected factory preconfigured solution</span></span>

<span data-ttu-id="45f04-104">Azure IoT Paketi [önceden yapılandırılmış çözümleri][lnk-preconfigured-solutions], ortak IoT iş senaryolarını uygulayan uçtan uca çözümler sunmak için birden çok Azure IoT hizmetini birleştirir.</span><span class="sxs-lookup"><span data-stu-id="45f04-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="45f04-105">Önceden yapılandırılmış *bağlı fabrika* çözümü endüstriyel cihazlarınıza bağlanır ve cihazları izler.</span><span class="sxs-lookup"><span data-stu-id="45f04-105">The *connected factory* preconfigured solution connects to and monitors your industrial devices.</span></span> <span data-ttu-id="45f04-106">Çözümü kullanarak cihazlarınızdan yapılan veri akışını analiz edebilir, operasyonel verimliliği ve karlılığı artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-106">You can use the solution to analyze the stream of data from your devices and to drive operational productivity and profitability.</span></span>

<span data-ttu-id="45f04-107">Bu öğretici, önceden yapılandırılmış bağlı fabrika çözümünün nasıl hazırlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="45f04-107">This tutorial shows you how to provision the connected factory preconfigured solution.</span></span> <span data-ttu-id="45f04-108">Ayrıca, önceden yapılandırılmış çözümün temel özelliklerinde rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="45f04-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="45f04-109">Bu özelliklerin birçoğuna önceden yapılandırılmış çözümün bir parçası olarak dağıtılan çözüm *panosundan* erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="45f04-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![önceden yapılandırılmış bağlı fabrika çözümü panosu][img-cf-home]

<span data-ttu-id="45f04-111">Bu öğreticiyi tamamlamak için etkin bir Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="45f04-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="45f04-112">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="45f04-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="45f04-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-the-solution"></a><span data-ttu-id="45f04-114">Çözüm sağlama</span><span class="sxs-lookup"><span data-stu-id="45f04-114">Provision the solution</span></span>

1. <span data-ttu-id="45f04-115">Azure hesabı kimlik bilgilerinizi kullanarak azureiotsuite.com adresinde oturum açın ve çözüm oluşturmak için “**+**” seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-115">Log on to azureiotsuite.com using your Azure account credentials, and click "**+**" to create a solution.</span></span>
2. <span data-ttu-id="45f04-116">**Bağlı fabrika** kutucuğunda **Seç**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-116">Click **Select** on the **Connected factory** tile.</span></span>
3. <span data-ttu-id="45f04-117">Önceden yapılandırılmış bağlı fabrika çözümünüz için bir **Çözüm adı** girin.</span><span class="sxs-lookup"><span data-stu-id="45f04-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="45f04-118">Çözümü hazırlarken kullanmak istediğiniz **Abonelik** ve **Bölge** seçimini yapın.</span><span class="sxs-lookup"><span data-stu-id="45f04-118">Select the **Subscription** and **Region** you want to use to provision the solution.</span></span>
5. <span data-ttu-id="45f04-119">Hazırlama işlemini başlatmak için **Çözümü Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-119">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="45f04-120">Bu işlemin çalışması genellikle birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="45f04-120">This process typically takes several minutes to run.</span></span>

### <a name="while-you-wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="45f04-121">Hazırlama işleminin tamamlanmasını beklerken</span><span class="sxs-lookup"><span data-stu-id="45f04-121">While you wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="45f04-122">Çözümünüzün **Hazırlama** durumuna sahip olan kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-122">Click the tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="45f04-123">Azure hizmetleri Azure aboneliğinize dağıtılırken **Hazırlama durumlarına** dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="45f04-123">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="45f04-124">Hazırlama tamamlandığında durum **Hazır** olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="45f04-124">Once provisioning completes, the status changes to **Ready**.</span></span>
4. <span data-ttu-id="45f04-125">Kutucuğa tıkladığınızda sağ bölmede çözümünüzün ayrıntılarını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="45f04-125">Click the tile to see the details of your solution in the right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="45f04-126">Önceden yapılandırılmış çözümün dağıtımında sorunlarla karşılaşırsanız bkz. [Azureiotsuite.com sitesindeki izinler][lnk-permissions] ve [Connected factory SSS](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="45f04-126">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="45f04-127">Sorunlar devam ederse [portalda][lnk-portal] bir hizmet bileti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="45f04-127">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="45f04-128">Görmeyi beklediğiniz ancak çözümünüz için listelenmemiş ayrıntılar mı var?</span><span class="sxs-lookup"><span data-stu-id="45f04-128">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="45f04-129">[User Voice](https://feedback.azure.com/forums/321918-azure-iot)'da bize özellik önerileri verin.</span><span class="sxs-lookup"><span data-stu-id="45f04-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="45f04-130">Senaryoya genel bakış</span><span class="sxs-lookup"><span data-stu-id="45f04-130">Scenario overview</span></span>

<span data-ttu-id="45f04-131">Önceden yapılandırılmış bağlı fabrika çözümünü dağıttığınızda, genel bir endüstriyel senaryoyu adım adım görmenize olanak sağlayan kaynaklar ile önceden doldurulur.</span><span class="sxs-lookup"><span data-stu-id="45f04-131">When you deploy the connected factory preconfigured solution, it is prepopulated with resources that enable you to step through a common industrial scenario.</span></span> <span data-ttu-id="45f04-132">Bu senaryoda, çözüme bağlı çeşitli fabrikalar genel donanım verimliliğini (OEE) ve ana performans göstergelerini (KPI) hesaplamak için gereken veri değerlerini raporlar.</span><span class="sxs-lookup"><span data-stu-id="45f04-132">In this scenario, several factories connected to the solution report the data values required to compute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="45f04-133">Aşağıdaki bölümlerde şunları nasıl yapacağınız açıklanır:</span><span class="sxs-lookup"><span data-stu-id="45f04-133">The following sections show you how to:</span></span>

* <span data-ttu-id="45f04-134">Fabrikayı, üretim hatlarını, istasyon OEE ve KPI değerlerini izleme</span><span class="sxs-lookup"><span data-stu-id="45f04-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="45f04-135">Azure Zaman Serisi Görüşlerini kullanarak bu cihazlardan oluşturulan telemetri verilerini analiz etme</span><span class="sxs-lookup"><span data-stu-id="45f04-135">Analyze the telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="45f04-136">Sorunları gidermek için uyarılara göre işlem yapma</span><span class="sxs-lookup"><span data-stu-id="45f04-136">Act on alerts to fix issues</span></span>

<span data-ttu-id="45f04-137">Bu senaryonun temel bir özelliği, çözüm panosu kullanılarak tüm bu eylemlerin uzaktan gerçekleştirilebiliyor olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="45f04-137">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="45f04-138">Cihazlara fiziksel erişiminizin olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="45f04-138">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="45f04-139">Çözüm panosunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="45f04-139">View the solution dashboard</span></span>

<span data-ttu-id="45f04-140">Çözüm panosu, dağıtılan çözümü yönetmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="45f04-140">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="45f04-141">Bu, genel fabrika yapılandırmasının hiyerarşik gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="45f04-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="45f04-142">Örneğin, OEE ve KPI’leri görüntüleyebilir, telemetri için yeni düğümler yayımlayabilir ve uyarıları eyleme dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="45f04-143">Sağlama tamamlandığında ve önceden yapılandırılmış çözümünüzün kutucuğu **Hazır**’ı gösterdiğinde, bağlı fabrika çözümü portalınızı yeni bir sekmede açmak için **Başlat**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="45f04-143">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your connected factory solution portal in a new tab.</span></span>

    ![Önceden yapılandırılmış çözümü başlatma][img-launch-solution]

1. <span data-ttu-id="45f04-145">Varsayılan olarak, çözüm portalı *panoyu* gösterir.</span><span class="sxs-lookup"><span data-stu-id="45f04-145">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="45f04-146">Portalın diğer alanlarına gitmek için sayfanın sol tarafındaki menüyü kullanın.</span><span class="sxs-lookup"><span data-stu-id="45f04-146">To navigate to other areas of the portal, use the menu on the left-hand side of the page.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü panosu][cf-img-menu]

<span data-ttu-id="45f04-148">Pano aşağıdaki bilgileri gösterir:</span><span class="sxs-lookup"><span data-stu-id="45f04-148">The dashboard displays the following information:</span></span>

* <span data-ttu-id="45f04-149">Çözümdeki durumu, konumu ve geçerli üretim yapılandırmasını gösteren bir **fabrika listesi** paneli.</span><span class="sxs-lookup"><span data-stu-id="45f04-149">A **Factory list** panel that shows the status, location, and current production configuration in the solution.</span></span> <span data-ttu-id="45f04-150">Çözümü ilk kez çalıştırdığınızda, bir dizi sanal cihaz bulunur.</span><span class="sxs-lookup"><span data-stu-id="45f04-150">When you first run the solution, there are a number of simulated devices.</span></span> <span data-ttu-id="45f04-151">Üretim hattı benzetimi, üretim hattı başına benzetimi yapılan görevleri gerçekleştiren ve verileri paylaşan üç gerçek OPC UA sunucusundan oluşur.</span><span class="sxs-lookup"><span data-stu-id="45f04-151">The production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="45f04-152">OPC UA hakkında daha fazla bilgi için bkz. [Connected factory SSS](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="45f04-152">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="45f04-153">Çözüme bağlı olan her cihazın konumunu görüntüleyen bir **harita**.</span><span class="sxs-lookup"><span data-stu-id="45f04-153">A **map** that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="45f04-154">Çözüm, bilgileri haritaya çizmek için Bing Haritalar API’sini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="45f04-154">The solution can use the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="45f04-155">Aboneliğiniz Bing Haritalar Kurumsal API’si için etkinleştirildiyse, bu özellik otomatik olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="45f04-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="45f04-156">Etkinleştirilmediyse, haritayı nasıl dinamik hale getireceğinizi öğrenmek için [SSS][lnk-faq] bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="45f04-156">If not, see the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="45f04-157">Telemetri veya OEE/KPI değeri belirli bir eşiği aştığında oluşturulan uyarıların gösterildiği **Uyarılar** paneli.</span><span class="sxs-lookup"><span data-stu-id="45f04-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="45f04-158">Kuruluşun tamamı için veya görüntülediğiniz fabrika/üretim hattı/istasyon için OEE değerlerinin gösterildiği **Genel Donanım Verimliliği** paneli.</span><span class="sxs-lookup"><span data-stu-id="45f04-158">An **Overall Equipment Efficiency** panel that shows the OEE values for the whole enterprise, or the factory/production line/station you are viewing.</span></span> <span data-ttu-id="45f04-159">Bu değer, kurumsal düzeyi bulmak için istasyon görünümünden toplanır.</span><span class="sxs-lookup"><span data-stu-id="45f04-159">This value is aggregated from the station view to the enterprise level.</span></span> <span data-ttu-id="45f04-160">OEE şekli ve bu şekli oluşturan öğeler daha fazla analiz edilebilir.</span><span class="sxs-lookup"><span data-stu-id="45f04-160">The OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="45f04-161">Kuruluşun tamamında veya görüntülediğiniz fabrika/üretim hattı/istasyonda üretilen birimlerin ve kullanılan enerjinin görüntülendiği **Ana Performans Göstergeleri** paneli.</span><span class="sxs-lookup"><span data-stu-id="45f04-161">**Key Performance Indicators** panel that displays the number of units produced and energy used by the whole enterprise or the factory/production line/station you are viewing.</span></span> <span data-ttu-id="45f04-162">Bu değerler, kurumsal düzeyi bulmak için istasyon görünümünden toplanır.</span><span class="sxs-lookup"><span data-stu-id="45f04-162">These values are aggregated from a station view to the enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="45f04-163">Fabrikaları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="45f04-163">View factories</span></span>

<span data-ttu-id="45f04-164">*Fabrikalar* paneli çözümdeki tüm fabrikaların coğrafi konumunu, durumlarını ve geçerli üretim yapılandırmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="45f04-164">The *Factories* panel shows you the geographical location of all the factories in the solution, their status, and current production configuration.</span></span> <span data-ttu-id="45f04-165">Konum listesinden, çözüm hiyerarşisindeki diğer düzeylere gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-165">From the locations list, you can navigate to the other levels in the solution hierarchy.</span></span> <span data-ttu-id="45f04-166">Listedeki satırlar, söz konusu konumdaki üretim hatlarının ayrıntılarına bağlanan birer köprüdür.</span><span class="sxs-lookup"><span data-stu-id="45f04-166">The rows in the list are hyperlinks that link details of the production lines at that location.</span></span> <span data-ttu-id="45f04-167">Böylelikle, üretim hattının detaylarına ve istasyon düzeyi görünümüne gitmek mümkün olur.</span><span class="sxs-lookup"><span data-stu-id="45f04-167">It is then possible to drill into the production line details and down to the station level view.</span></span> <span data-ttu-id="45f04-168">Ayrıca listeye filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-168">You can also apply a filter to the list.</span></span>

![Önceden yapılandırılmış bağlı fabrika çözümü fabrikaları][cf-img-factories] 

1. <span data-ttu-id="45f04-170">**Fabrika paneli**’nde bu çözümün fabrika listesi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="45f04-170">The **Factory panel** shows the factory list for this solution.</span></span>

2. <span data-ttu-id="45f04-171">Fabrika listesi başlangıçta hazırlama işlemi tarafından oluşturulan altı fabrika gösterir.</span><span class="sxs-lookup"><span data-stu-id="45f04-171">The factory list initially shows six factories created by the provisioning process.</span></span> <span data-ttu-id="45f04-172">Çözüme başka sanal ve fiziksel cihazlar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-172">You can add additional simulated and physical devices to the solution.</span></span>

3. <span data-ttu-id="45f04-173">Fabrikanın ayrıntılarını görüntülemek için fabrika listesindeki satıra tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-173">To view the details of a factory, click the row in the factory list.</span></span>

4. <span data-ttu-id="45f04-174">Üretim hattının ayrıntılarını görüntülemek için listedeki satıra tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-174">To view the details of a production line, click the row in the list.</span></span>

5. <span data-ttu-id="45f04-175">Üretim hattında bir istasyonun yayımlanmış OPC UA düğümlerini görüntülemek için listedeki satıra tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-175">To view the published OPC UA nodes of a station on the production line, click the row in the list.</span></span>

6. <span data-ttu-id="45f04-176">İstasyondaki belirli bir düğümün ayrıntılarını görüntülemek için listedeki satıra tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-176">To view details on a specific node in the station, click the row in the list.</span></span> <span data-ttu-id="45f04-177">Bu eylem, Zaman Serisi Görüşleri görselleriyle bağlam panelini başlatır.</span><span class="sxs-lookup"><span data-stu-id="45f04-177">This action launches the context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="45f04-178">Zaman Serisi Görüşleri gezgin ortamında daha fazla analiz yapmak için bu grafiklere tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-178">Click these graphs to do further analysis in the Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="45f04-179">Haritayı görüntüleme</span><span class="sxs-lookup"><span data-stu-id="45f04-179">View map</span></span>

<span data-ttu-id="45f04-180">Aboneliğinizin Bing Haritalar API’sine erişimi varsa, *Fabrikalar* haritasında size çözümdeki tüm fabrikaların coğrafi konumu ve durumu gösterilir.</span><span class="sxs-lookup"><span data-stu-id="45f04-180">If your subscription has access to the Bing Maps API, the *Factories* map shows you the geographical location and status of all the factories in the solution.</span></span> <span data-ttu-id="45f04-181">Konumun detaylarına gitmek için haritada görüntülenen konumlara tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-181">To drill into the location details, click the locations displayed on the map.</span></span>

![Önceden yapılandırılmış bağlı fabrika çözümü haritası][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="45f04-183">Uyarıları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="45f04-183">View alerts</span></span>

<span data-ttu-id="45f04-184">**Uyarı** panelinde, raporlanan bir değerin veya hesaplanan OEE/KPI değerinin yapılandırılmış eşiği aşmasından dolayı üretilen uyarılar gösterilir.</span><span class="sxs-lookup"><span data-stu-id="45f04-184">The **Alert** panel shows you alerts generated due to a reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="45f04-185">Bu panelde, istasyon düzeyi görünümünden genel görünüme kadar her hiyerarşi düzeyindeki uyarılar görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="45f04-185">This panel displays alerts at each level of the hierarchy, from the station level view to the global view.</span></span> <span data-ttu-id="45f04-186">Uyarılar, uyarının açıklamasını, tarihini, saatini, konumunu ve tekrarlanma sayısını içerir.</span><span class="sxs-lookup"><span data-stu-id="45f04-186">The alerts contain a description of the alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="45f04-187">Zaman Serisi Görüşleri verilerini kullanarak uyarıya neden olan fikirlerle ilgili görüş sahibi olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-187">You can gain insights in to the data that caused the alert using the Time Series Insights data.</span></span> <span data-ttu-id="45f04-188">Zaman Serisi Görüşleri’nin verileri, uygun olduğunda uyarılarda görselleştirilir.</span><span class="sxs-lookup"><span data-stu-id="45f04-188">The Time Series Insights data is visualized in the alerts where applicable.</span></span> <span data-ttu-id="45f04-189">Yöneticiyseniz, uyarılar üzerinde şu varsayılan eylemleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="45f04-189">If you are an Administrator, you can take default actions on the alerts such as:</span></span>

* <span data-ttu-id="45f04-190">Uyarıyı kapatma.</span><span class="sxs-lookup"><span data-stu-id="45f04-190">Close the alert.</span></span>
* <span data-ttu-id="45f04-191">Uyarıyı kabul etme.</span><span class="sxs-lookup"><span data-stu-id="45f04-191">Acknowledge the alert.</span></span>

<span data-ttu-id="45f04-192">İsteğe bağlı olarak, daha karmaşık eylemler de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="45f04-193">Örneğin, Montajın Basınç OPC UA Düğümü için şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="45f04-193">For example, for the Pressure OPC UA Node of the Assembly you could:</span></span>

* <span data-ttu-id="45f04-194">Destek bilgilerini yeni bir tarayıcı penceresinde bir web sayfasında gösterme.</span><span class="sxs-lookup"><span data-stu-id="45f04-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="45f04-195">Cihazda OPC UA metodunu çağırarak uyarıya neden olan sorunu giderme.</span><span class="sxs-lookup"><span data-stu-id="45f04-195">Mitigate the cause of the alert by calling an OPC UA method on the device.</span></span>
* <span data-ttu-id="45f04-196">Varsayılan eylemlerin kullanılabilirliğini engelleme.</span><span class="sxs-lookup"><span data-stu-id="45f04-196">Suppress the availability of the default actions.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü uyarıları][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="45f04-198">Bu uyarılar, önceden yapılandırılmış çözümdeki yapılandırma dosyasında belirtilen kurallar tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="45f04-198">These alerts are generated by rules that are specified in a configuration file in the preconfigured solution.</span></span> <span data-ttu-id="45f04-199">Bu kurallar, OEE veya KPI rakamları veya OPC UA Düğüm değerleri yapılandırılmış eşiği aştığında uyarılar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="45f04-199">These rules can generate alerts when the OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="45f04-200">**Uyarılar panosunda**, bu çözümde oluşturulan uyarılar gösterilir.</span><span class="sxs-lookup"><span data-stu-id="45f04-200">The **Alerts panel** shows the alerts generated in this solution.</span></span>

2. <span data-ttu-id="45f04-201">Uyarıların ayrıntılarını görüntülemek için, uyarılar panelinde uyarıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-201">To view the details of an alert, click the alert in the alerts panel.</span></span>

3. <span data-ttu-id="45f04-202">Uyarı verilerinde daha fazla analiz yapmak için, uyarı panelindeki grafiğe tıklayarak Zaman Serisi Görüşleri gezgin ortamını açın.</span><span class="sxs-lookup"><span data-stu-id="45f04-202">To further analyze the alert data, click the graph in the alert panel to open the Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="45f04-203">Uyarıya çözmek için, uyarı panelinde çeşitli eylemler sağlanır.</span><span class="sxs-lookup"><span data-stu-id="45f04-203">To address the alert, several actions are available in the alert panel.</span></span> <span data-ttu-id="45f04-204">Kendinize uygun seçeneği seçin ve eylemi yürütme komut düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-204">Choose the appropriate option for you and click the execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="45f04-205">Genel donanım verimliliğini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="45f04-205">View overall equipment efficiency</span></span>

<span data-ttu-id="45f04-206">OEE, üretimle ilgili önemli operasyonel parametreleri kullanarak üretim sürecinin verimliliğini derecelendirir.</span><span class="sxs-lookup"><span data-stu-id="45f04-206">OEE rates the efficiency of the manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="45f04-207">OEE, kullanılabilirlik oranı, performans oranı ve kalite oranının çarpılmasıyla hesaplanan standart bir endüstri ölçümüdür: OEE = kullanılabilirlik x performans x kalite.</span><span class="sxs-lookup"><span data-stu-id="45f04-207">OEE is an industry standard measure calculated by multiplying the availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![Önceden yapılandırılmış bağlı fabrika çözümü OEE][cf-img-oee]

1. <span data-ttu-id="45f04-209">Hiyerarşideki herhangi bir düzeyin OEE ölçümünü görüntülemek için, ihtiyacınız olan görünüme gidin.</span><span class="sxs-lookup"><span data-stu-id="45f04-209">To view OEE for any level in the hierarchy, navigate to the specific view you require.</span></span> <span data-ttu-id="45f04-210">Söz konusu görünümün OEE’si panelde OEE yüzdesini oluşturan öğelerden her biriyle birlikte görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="45f04-210">The OEE for that view displays in the panel along with each of the elements that make up the OEE percentage.</span></span>

2. <span data-ttu-id="45f04-211">Hiyerarşi verilerinin herhangi bir düzeyinde OEE’de daha fazla analiz yapmak için, OEE, kullanılabilirlik, performans veya kalite yüzdesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-211">To further analyze the OEE for any level in the hierarchy data, click either the OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="45f04-212">Son bir saatin, son 24 saatin ve son 7 günün verilerinin gösterildiği, Zaman Serisi Görüşleri ile desteklenen görselleştirmelerle bir bağlam paneli görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="45f04-212">A context panel appears with Time Series Insights powered visualizations that shows data from the last hour, last 24 hours, and last 7 days.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü TSI görselleştirmesi][cf-img-tsi-visualization]

3. <span data-ttu-id="45f04-214">Uyarı verilerini daha fazla analiz etmek için, uyarı panelindeki grafiğe tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-214">To further analyze the alert data, click the graph in the alert panel.</span></span> <span data-ttu-id="45f04-215">Bu eylem Zaman Serisi Görüşleri düzenleyici ortamını açar.</span><span class="sxs-lookup"><span data-stu-id="45f04-215">This action opens the Time Series Insights explorer environment.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü TSI gezgini][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="45f04-217">Önemli Performans Göstergelerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="45f04-217">View Key Performance Indicators</span></span>

<span data-ttu-id="45f04-218">Çözüm iki önemli performans göstergesi (*saat başına birim sayısı* ve *kWh cinsinden kullanılan enerji*) sağlar.</span><span class="sxs-lookup"><span data-stu-id="45f04-218">The solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![Önceden yapılandırılmış bağlı fabrika çözümü KPI][cf-img-kpi]

1. <span data-ttu-id="45f04-220">Hiyerarşideki herhangi bir düzeyin saat başına birim sayısını veya kullanılan enerji miktarını görüntülemek için, ihtiyacınız olan görünüme gidin.</span><span class="sxs-lookup"><span data-stu-id="45f04-220">To view units per hour or energy used for any level in the hierarchy, navigate to the specific view you require.</span></span> <span data-ttu-id="45f04-221">Saat başına birim sayısı ve kullanılan enerji miktarı panelde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="45f04-221">The units per hour and energy used display in the panel.</span></span>

2. <span data-ttu-id="45f04-222">Hiyerarşinin herhangi bir düzeyinde saat başına birim sayısını ve kullanılan enerji miktarını daha ayrıntılı analiz etmek için **Önemli Performans Göstergeleri** panelindeki ölçere tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-222">To analyze units per hour or energy used for any level in the hierarchy further, click the gauge in the **Key Performance Indicators** panel.</span></span> <span data-ttu-id="45f04-223">Son bir saatin, son 24 saatin ve son 7 günün verilerini görebilmenizi sağlayan Zaman Serisi Görüşleri ile desteklenen görselleştirmelerle bir bağlam paneli görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="45f04-223">A context panel appears with Time Series Insights powered visualizations enabling you to view data from the last hour, the last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="45f04-224">Senaryo gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="45f04-224">Scenario review</span></span>

<span data-ttu-id="45f04-225">Bu senaryoda, panoda fabrikalarınızın OEE ve KPI değerlerini izlediniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-225">In this scenario, you monitored your factories OEE and KPIs values, in the dashboard.</span></span> <span data-ttu-id="45f04-226">Ardından, anormallikleri saptayabilmek için OEE ve KPI’lerin telemetri verilerinde daha fazla detaya gitmenize yardımcı olacak daha fazla bilgi sağlamak üzere Zaman Serisi Görüşleri’ni kullandınız.</span><span class="sxs-lookup"><span data-stu-id="45f04-226">You then used Time Series Insights to provide more information to help drill further into the telemetry data for OEE and KPIs to help with detecting anomalies.</span></span> <span data-ttu-id="45f04-227">Ayrıca, fabrikalarınızdaki sorunları görüntülemek üzere uyarı panosundan yararlandınız ve uyarının sorununu çözmek için size sağlanan eylemleri kullandınız.</span><span class="sxs-lookup"><span data-stu-id="45f04-227">You also used the alert panel to view issues with your factories and you used the actions available to you to resolve the alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="45f04-228">Diğer özellikler</span><span class="sxs-lookup"><span data-stu-id="45f04-228">Other features</span></span>

<span data-ttu-id="45f04-229">Aşağıdaki bölümlerde, bağlı fabrika çözümünün önceki senaryoda bahsedilmeyen bazı ek özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="45f04-229">The following sections describe some additional features of the connected factory solution that are not described in the previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="45f04-230">Filtreleri uygulama</span><span class="sxs-lookup"><span data-stu-id="45f04-230">Apply filters</span></span>

1. <span data-ttu-id="45f04-231">Fabrika konumları panelinde veya uyarılar panelinde kullanılabilir filtrelerin listesini görüntülemek için **köşeli çift ayraca** tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-231">Click the **chevron** to display a list of available filters in either the factory locations panel or the alerts panel.</span></span>

2. <span data-ttu-id="45f04-232">Sizin için filtreler paneli görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="45f04-232">The filters panel is displayed for you.</span></span> 

    ![Önceden yapılandırılmış bağlı fabrika çözümü filtreleri][cf-img-alert-filter]

3. <span data-ttu-id="45f04-234">Gerek duyduğunuz filtreyi seçin.</span><span class="sxs-lookup"><span data-stu-id="45f04-234">Choose the filter that you require.</span></span> <span data-ttu-id="45f04-235">Filtre alanlarına serbest metin yazmak mümkündür.</span><span class="sxs-lookup"><span data-stu-id="45f04-235">It is also possible to type free text into the filter fields.</span></span>

4. <span data-ttu-id="45f04-236">Ardından filtre sizin için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="45f04-236">The filter is then applied for you.</span></span> <span data-ttu-id="45f04-237">Panoda, fabrikalar ve uyarılar tablolarının içinde görüntülenen bir huni aracılığıyla filtrenin durumu da gösterilir.</span><span class="sxs-lookup"><span data-stu-id="45f04-237">The filter state is also shown in the dashboard via a funnel that displays in the factories and alerts tables.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü filtreleri][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="45f04-239">Etkin bir filtre görüntülenen OEE ve KPI değerlerini etkilemez; yalnızca liste içeriğini filtreler.</span><span class="sxs-lookup"><span data-stu-id="45f04-239">An active filter does not affect the displayed OEE and KPI values, it only filters the list contents.</span></span>

5. <span data-ttu-id="45f04-240">Filtreyi temizlemek için huniye tıklayın ve filtre bağlam panelinde filtreye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-240">To clear a filter, click the funnel and click filter in the filter context panel.</span></span> <span data-ttu-id="45f04-241">Fabrikalar ve uyarılar tablolarında **Tümü** metni görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="45f04-241">The text **All** is displayed in the factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="45f04-242">OPC UA sunucusuna göz atma</span><span class="sxs-lookup"><span data-stu-id="45f04-242">Browse an OPC UA server</span></span>

<span data-ttu-id="45f04-243">Önceden yapılandırılmış çözümü dağıttığınızda, çözüm tarayıcısı üzerinden göz atabileceğiniz sanal OPC UA sunucularını otomatik olarak hazırlarsınız.</span><span class="sxs-lookup"><span data-stu-id="45f04-243">When you deploy the preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via the solution browser.</span></span> <span data-ttu-id="45f04-244">Bu sunucular, *sanal OPC UA sunucularıdır*.</span><span class="sxs-lookup"><span data-stu-id="45f04-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="45f04-245">Sanal sunucular herhangi bir gerçek ve fiziksel sunucuya dağıtmaya gerek kalmadan önceden yapılandırılmış çözümü denemenizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="45f04-245">Simulated servers make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical servers.</span></span> <span data-ttu-id="45f04-246">Çözüme gerçek bir OPC UA sunucusu bağlamak istemiyorsanız [OPC UA cihazınızı önceden yapılandırılmış bağlı fabrika çözümüne bağlama][lnk-connect-cf] öğreticisine bakın.</span><span class="sxs-lookup"><span data-stu-id="45f04-246">If you do want to connect a real OPC UA server to the solution, see the [Connect your OPC UA device to the connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="45f04-247">Pano gezinti çubuğunda **fabrika simgesine** tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-247">Click the **factory icon** in the dashboard navigation bar.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü sunucu tarayıcısı][cf-img-server-browser]

2. <span data-ttu-id="45f04-249">Önceden yapılandırılmış listedeki sunuculardan birini seçin.</span><span class="sxs-lookup"><span data-stu-id="45f04-249">Choose one of the servers from the preconfigured list.</span></span> <span data-ttu-id="45f04-250">Bu listede, önceden yapılandırılmış çözümde sizin için dağıtılan sunucular gösterilir.</span><span class="sxs-lookup"><span data-stu-id="45f04-250">This list shows the servers that are deployed for you in the preconfigured solution.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü sunucu seçimi][cf-img-server-choice]

3. <span data-ttu-id="45f04-252">**Bağlan**’a tıklayın; güvenlik iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="45f04-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="45f04-253">Benzetim için, **Devam Et**’e tıklamak güvenlidir</span><span class="sxs-lookup"><span data-stu-id="45f04-253">For the simulation, it is safe to click **Proceed**</span></span>

4. <span data-ttu-id="45f04-254">Sunucu ağacındaki düğümlerden herhangi birini genişletmek için düğüme tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-254">To expand any of the nodes in the server tree, click it.</span></span> <span data-ttu-id="45f04-255">Yayımlama telemetrisi olan düğümlerin yanında bir onay işareti vardır.</span><span class="sxs-lookup"><span data-stu-id="45f04-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü sunucu ağacı][cf-img-server-tree]

5. <span data-ttu-id="45f04-257">Düğümü okumak, yazmak, yayımlamak veya çağırmak için bir öğeye sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-257">Right-click an item to read, write, publish, or call that node.</span></span> <span data-ttu-id="45f04-258">Kullanabileceğiniz eylemler, izinlerinize ve düğümün özniteliklerine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="45f04-258">The actions available to you depend on your permissions and the attributes of the node.</span></span> <span data-ttu-id="45f04-259">Okuma seçeneği belirli bir düğümün değerini gösteren içerik panelini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="45f04-259">The read option to displays a context panel showing the value of the specific node.</span></span> <span data-ttu-id="45f04-260">Yazma seçeneği yeni değer girebileceğiniz bir bağlam paneli görüntüler.</span><span class="sxs-lookup"><span data-stu-id="45f04-260">The write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="45f04-261">Çağırma seçeneği çağrı için parametreleri girebileceğiniz bir düğüm görüntüler.</span><span class="sxs-lookup"><span data-stu-id="45f04-261">The call option displays a node where you can enter the parameters for the call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="45f04-262">Düğümü yayımlama</span><span class="sxs-lookup"><span data-stu-id="45f04-262">Publish a node</span></span>

<span data-ttu-id="45f04-263">*Sanal OPC UA sunucusuna* göz attığınızda, yeni düğümleri yayımlamayı da seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-263">When you browse a *simulated OPC UA server*, you can also choose to publish new nodes.</span></span> <span data-ttu-id="45f04-264">Çözümde bu düğümlerden gelen telemetriyi analiz edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-264">You can analyze the telemetry from these nodes in the solution.</span></span> <span data-ttu-id="45f04-265">Bu *sanal OPC UA sunucuları* gerçek ve fiziksel cihaza dağıtmaya gerek olmadan önceden yapılandırılmış çözümü denemenizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="45f04-265">These *simulated OPC UA servers* make it easy to experiment with the preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="45f04-266">OPC UA sunucusu tarayıcı ağacında yayımlamak istediğiniz düğüme göz atın.</span><span class="sxs-lookup"><span data-stu-id="45f04-266">Browse to a node in the OPC UA server browser tree that you wish to publish.</span></span>

2. <span data-ttu-id="45f04-267">Düğüme sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-267">Right-click the node.</span></span>

3. <span data-ttu-id="45f04-268">**Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="45f04-268">Choose **Publish**.</span></span>

    ![Bağlı fabrika yayımlama düğümü][cf-img-publish-node]

4. <span data-ttu-id="45f04-270">Yayımlama işleminin başarılı olduğunu bildiren bir bağlam paneli görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="45f04-270">A context panel appears which tells you that the publish has succeeded.</span></span> <span data-ttu-id="45f04-271">Düğüm, istasyon düzeyi görünümünde yanında bir onay işaretiyle gösterilir.</span><span class="sxs-lookup"><span data-stu-id="45f04-271">The node appears in the station level view with a check mark beside it.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü yayımlama başarısı][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="45f04-273">Komut ve denetim</span><span class="sxs-lookup"><span data-stu-id="45f04-273">Command and control</span></span>

<span data-ttu-id="45f04-274">Bağlı fabrika, endüstri cihazlarınızı doğrudan buluttan kumanda etmenize ve denetlemenize olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="45f04-274">The connected factory allows you command and control your industry devices directly from the cloud.</span></span> <span data-ttu-id="45f04-275">Cihaz tarafından oluşturulan uyarıları yanıtlamak için bu özelliği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-275">You can use this feature to respond to alerts generated by the device.</span></span> <span data-ttu-id="45f04-276">Örneğin, buluttan cihaza bir komut gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-276">For example, you could send a command to the device from the cloud.</span></span> <span data-ttu-id="45f04-277">Kullanılabilir komutları, OPC UA sunucuları tarayıcı ağacındaki **StationCommands** düğümünde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-277">You can find the available commands in the **StationCommands** node in the OPC UA servers browser tree.</span></span> <span data-ttu-id="45f04-278">Bu senaryoda, Münih’teki üretim hattının montaj istasyonundaki basınç tahliye vanasını açıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="45f04-278">In this scenario, you open a pressure release valve on the assembly station of a production line in Munich.</span></span> <span data-ttu-id="45f04-279">Kumanda etme ve denetleme işlevselliğini kullanmak için, önceden yapılandırılmış çözüm dağıtımında **Yönetici** rolünde olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="45f04-279">To use the command and control functionality, you must be in the **Administrator** role for the preconfigured solution deployment.</span></span>

1. <span data-ttu-id="45f04-280">OPC UA sunucusu tarayıcı düğümünde **StationCommands** düğümüne göz atın.</span><span class="sxs-lookup"><span data-stu-id="45f04-280">Browse to the **StationCommands** node in the OPC UA server browser tree.</span></span>

2. <span data-ttu-id="45f04-281">Kullanmak istediğiniz komutu seçin.</span><span class="sxs-lookup"><span data-stu-id="45f04-281">Choose the command that you wish use.</span></span>

3. <span data-ttu-id="45f04-282">Düğüme sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="45f04-282">Right-click the node.</span></span>

4. <span data-ttu-id="45f04-283">**Çağır**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="45f04-283">Choose **Call**.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü çağır komutu][cf-img-call-command]

5. <span data-ttu-id="45f04-285">Çağırmak üzere olduğunuz yöntem ve uygulanabilecek parametre ayrıntıları hakkında bilgi veren bir bağlam paneli açılır.</span><span class="sxs-lookup"><span data-stu-id="45f04-285">A context panel appears informing you which method you are about to call and any parameter details is applicable.</span></span>

6. <span data-ttu-id="45f04-286">**Çağır**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="45f04-286">Choose **Call**.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü çağrı bağlamı][cf-img-call-context]

7. <span data-ttu-id="45f04-288">Bağlam paneli, yöntem çağrısının başarılı olduğunu bildirecek şekilde güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="45f04-288">The context panel is updated to inform you that the method call succeeded.</span></span> <span data-ttu-id="45f04-289">Çağrı sonucu güncelleştirilen basınç düğümünün değerini okuyarak çağrının başarılı olduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-289">You can verify the call succeeded by reading the value of the pressure node that updated as a result of the call.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü çağrı başarısı][cf-img-call-success]


## <a name="behind-the-scenes"></a><span data-ttu-id="45f04-291">Arka planda</span><span class="sxs-lookup"><span data-stu-id="45f04-291">Behind the scenes</span></span>

<span data-ttu-id="45f04-292">Önceden yapılandırılmış bir çözümü dağıttığınızda, dağıtım işlemi seçtiğiniz Azure aboneliğinde birden çok kaynak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="45f04-292">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="45f04-293">Bu kaynakları Azure [portalında][lnk-portal] görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-293">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="45f04-294">Dağıtım işlemi, önceden yapılandırılmış çözümünüz için seçtiğiniz adı temel alan bir ada sahip bir **kaynak grubu** oluşturur:</span><span class="sxs-lookup"><span data-stu-id="45f04-294">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Azure portalında önceden yapılandırılmış çözüm][img-cf-portal]

<span data-ttu-id="45f04-296">Her bir kaynağın ayarlarını, kaynak grubundaki kaynaklar listesinde seçerek görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-296">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="45f04-297">Önceden yapılandırılmış çözüm için kaynak kodunu da görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-297">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="45f04-298">Önceden yapılandırılmış bağlı fabrika çözümünün kaynak kodu [azure-iot-connected-factory][lnk-cfgithub] GitHub deposundadır:</span><span class="sxs-lookup"><span data-stu-id="45f04-298">The connected factory preconfigured solution source code is in the [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="45f04-299">İşiniz bittiğinde önceden yapılandırılmış çözümü [azureiotsuite.com][lnk-azureiotsuite] sitesindeki Azure aboneliğinizden silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45f04-299">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="45f04-300">Bu site, önceden yapılandırılmış çözümü oluşturduğunuzda sağlanan tüm kaynakları kolayca silmenize imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="45f04-300">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="45f04-301">Önceden yapılandırılmış çözümle ilgili her şeyi sildiğinizden emin olmak için bu öğeleri [azureiotsuite.com][lnk-azureiotsuite] sitesinde silin.</span><span class="sxs-lookup"><span data-stu-id="45f04-301">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="45f04-302">Portalda kaynak grubunu silmeyin.</span><span class="sxs-lookup"><span data-stu-id="45f04-302">Do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45f04-303">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="45f04-303">Next Steps</span></span>

<span data-ttu-id="45f04-304">Çalışan bir önceden yapılandırılmış çözüm dağıttığınıza göre aşağıdaki makaleleri okuyarak IoT Paketi ile çalışmaya başlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="45f04-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="45f04-305">[Önceden yapılandırılmış bağlı fabrika çözümü yönergeleri][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="45f04-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="45f04-306">[Cihazınızı önceden yapılandırılmış Bağlı fabrika çözümüne bağlama][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="45f04-306">[Connect your device to the Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="45f04-307">[azureiotsuite.com sitesindeki izinler][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="45f04-307">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md