---
title: "IOT paketi aaaAzure bağlı Fabrika genel bakış | Microsoft Docs"
description: "Hello Azure IOT paketi açıklamasını Fabrika önceden yapılandırılmış çözüm bağlı."
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
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a><span data-ttu-id="ef20f-103">Bağlı hello Fabrika önceden yapılandırılmış çözümü ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ef20f-103">Get started with hello connected factory preconfigured solution</span></span>

<span data-ttu-id="ef20f-104">Azure IOT paketi [önceden yapılandırılmış çözümleri] [ lnk-preconfigured-solutions] ortak IOT iş senaryolarını uygulayan birden çok Azure IOT Hizmetleri toodeliver uçtan uca çözümler birleştirin.</span><span class="sxs-lookup"><span data-stu-id="ef20f-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="ef20f-105">Merhaba *bağlı Fabrika* önceden yapılandırılmış çözüm endüstriyel aygıtlarınızı tooand izleyiciler bağlanır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-105">hello *connected factory* preconfigured solution connects tooand monitors your industrial devices.</span></span> <span data-ttu-id="ef20f-106">Merhaba çözüm tooanalyze hello akış cihazlarınız ve toodrive işletimsel verimliliğini ve Karlılık verilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-106">You can use hello solution tooanalyze hello stream of data from your devices and toodrive operational productivity and profitability.</span></span>

<span data-ttu-id="ef20f-107">Bu öğretici, tooprovision hello Fabrika nasıl bağlanacağını gösterir. önceden yapılandırılmış çözümü.</span><span class="sxs-lookup"><span data-stu-id="ef20f-107">This tutorial shows you how tooprovision hello connected factory preconfigured solution.</span></span> <span data-ttu-id="ef20f-108">Bu ayrıca, hello aracılığıyla hello önceden yapılandırılmış çözümün temel özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="ef20f-109">Bu özelliklerin çoğunu hello çözümden erişebilirsiniz *Pano* hello önceden yapılandırılmış çözümün bir parçası dağıtır:</span><span class="sxs-lookup"><span data-stu-id="ef20f-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![önceden yapılandırılmış bağlı fabrika çözümü panosu][img-cf-home]

<span data-ttu-id="ef20f-111">toocomplete Bu öğreticide, bir etkin Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="ef20f-112">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ef20f-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="ef20f-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-hello-solution"></a><span data-ttu-id="ef20f-114">Sağlama hello çözümü</span><span class="sxs-lookup"><span data-stu-id="ef20f-114">Provision hello solution</span></span>

1. <span data-ttu-id="ef20f-115">Azure hesabı kimlik bilgilerinizi kullanarak tooazureiotsuite.com üzerinde oturum öğesini tıklatıp "**+**" toocreate bir çözüm.</span><span class="sxs-lookup"><span data-stu-id="ef20f-115">Log on tooazureiotsuite.com using your Azure account credentials, and click "**+**" toocreate a solution.</span></span>
2. <span data-ttu-id="ef20f-116">Tıklatın **seçin** hello üzerinde **bağlı Fabrika** döşeme.</span><span class="sxs-lookup"><span data-stu-id="ef20f-116">Click **Select** on hello **Connected factory** tile.</span></span>
3. <span data-ttu-id="ef20f-117">Önceden yapılandırılmış bağlı fabrika çözümünüz için bir **Çözüm adı** girin.</span><span class="sxs-lookup"><span data-stu-id="ef20f-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="ef20f-118">Select hello **abonelik** ve **bölge** toouse tooprovision hello çözüm istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-118">Select hello **Subscription** and **Region** you want toouse tooprovision hello solution.</span></span>
5. <span data-ttu-id="ef20f-119">Tıklatın **çözümü Oluştur** toobegin hello sağlama işlemi.</span><span class="sxs-lookup"><span data-stu-id="ef20f-119">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="ef20f-120">Bu işlem genellikle birkaç dakika toorun alır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-120">This process typically takes several minutes toorun.</span></span>

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="ef20f-121">İşlem toocomplete sağlama hello için beklerken</span><span class="sxs-lookup"><span data-stu-id="ef20f-121">While you wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="ef20f-122">Çözümünüzle birlikte Hello kutucuğa tıklayın **sağlama** durumu.</span><span class="sxs-lookup"><span data-stu-id="ef20f-122">Click hello tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="ef20f-123">Bildirim hello **hazırlama durumlarına** gibi Azure Hizmetleri Azure aboneliğinize dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-123">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="ef20f-124">Hazırlama tamamlandığında durum değişikliklerini çok hello**hazır**.</span><span class="sxs-lookup"><span data-stu-id="ef20f-124">Once provisioning completes, hello status changes too**Ready**.</span></span>
4. <span data-ttu-id="ef20f-125">Merhaba döşeme toosee hello hello sağ bölmede çözümünüzün ayrıntılarını'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-125">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="ef20f-126">Merhaba önceden yapılandırılmış çözümü dağıtma sorunlarla karşılaşırsanız, gözden [hello azureiotsuite.com sitesindeki izinler] [ lnk-permissions] ve hello [bağlı Fabrika SSS](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="ef20f-126">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="ef20f-127">Merhaba sorunları devam ederse, bir hizmet bileti hello üzerinde oluşturma [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="ef20f-127">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="ef20f-128">Çözümünüz için listelenmeyen toosee beklediğiniz ayrıntılar bulunur?</span><span class="sxs-lookup"><span data-stu-id="ef20f-128">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="ef20f-129">[User Voice](https://feedback.azure.com/forums/321918-azure-iot)'da bize özellik önerileri verin.</span><span class="sxs-lookup"><span data-stu-id="ef20f-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="ef20f-130">Senaryoya genel bakış</span><span class="sxs-lookup"><span data-stu-id="ef20f-130">Scenario overview</span></span>

<span data-ttu-id="ef20f-131">Bağlı hello dağıttığınızda Fabrika önceden yapılandırılmış çözüm, bu ortak endüstriyel senaryosu aracılığıyla toostep kaynak ile önceden doldurulmaz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-131">When you deploy hello connected factory preconfigured solution, it is prepopulated with resources that enable you toostep through a common industrial scenario.</span></span> <span data-ttu-id="ef20f-132">Bu senaryoda, birkaç oluşturucuları bağlı hello veri değerleri gerekli toocompute toohello çözüm raporu genel donanım verimliliği (OEE) ve ana performans göstergelerini (KPI'lar).</span><span class="sxs-lookup"><span data-stu-id="ef20f-132">In this scenario, several factories connected toohello solution report hello data values required toocompute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="ef20f-133">Merhaba aşağıdaki bölümlerde, nasıl göstermek için:</span><span class="sxs-lookup"><span data-stu-id="ef20f-133">hello following sections show you how to:</span></span>

* <span data-ttu-id="ef20f-134">Fabrikayı, üretim hatlarını, istasyon OEE ve KPI değerlerini izleme</span><span class="sxs-lookup"><span data-stu-id="ef20f-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="ef20f-135">Azure zaman serisi Öngörüler kullanarak bu cihazlardan oluşturulan hello telemetri verilerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="ef20f-135">Analyze hello telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="ef20f-136">Uyarıları toofix sorunları hareket</span><span class="sxs-lookup"><span data-stu-id="ef20f-136">Act on alerts toofix issues</span></span>

<span data-ttu-id="ef20f-137">Bir anahtar, bu senaryo bu eylemleri uzaktan hello çözüm panodan için gerçekleştirebilir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-137">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="ef20f-138">Fiziksel erişim toohello aygıtları gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ef20f-138">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="ef20f-139">Görünüm hello çözüm Panosu</span><span class="sxs-lookup"><span data-stu-id="ef20f-139">View hello solution dashboard</span></span>

<span data-ttu-id="ef20f-140">Merhaba çözüm Panosu toomanage dağıtılan hello çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef20f-140">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="ef20f-141">Bu, genel fabrika yapılandırmasının hiyerarşik gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="ef20f-142">Örneğin, OEE ve KPI’leri görüntüleyebilir, telemetri için yeni düğümler yayımlayabilir ve uyarıları eyleme dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="ef20f-143">Ne zaman hello Sağlama tamamlandıktan ve önceden yapılandırılmış çözümünüzün kutucuğu hello gösterir **hazır**, seçin **başlatma** tooopen bağlı Fabrika çözümü portalınızı yeni bir sekmede.</span><span class="sxs-lookup"><span data-stu-id="ef20f-143">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your connected factory solution portal in a new tab.</span></span>

    ![Merhaba önceden yapılandırılmış çözüm başlatma][img-launch-solution]

1. <span data-ttu-id="ef20f-145">Varsayılan olarak, hello çözüm portalı hello gösterir *Pano*.</span><span class="sxs-lookup"><span data-stu-id="ef20f-145">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="ef20f-146">toonavigate tooother alanları hello portalının hello sol taraftaki hello sayfasının hello menüsünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-146">toonavigate tooother areas of hello portal, use hello menu on hello left-hand side of hello page.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü panosu][cf-img-menu]

<span data-ttu-id="ef20f-148">Başlangıç Panosu aşağıdaki bilgilerle hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="ef20f-148">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="ef20f-149">A **Fabrika listesi** hello durumu, konum ve üretim yapılandırmasına hello çözümde gösterir paneli.</span><span class="sxs-lookup"><span data-stu-id="ef20f-149">A **Factory list** panel that shows hello status, location, and current production configuration in hello solution.</span></span> <span data-ttu-id="ef20f-150">Merhaba çözümü ilk kez çalıştırdığınızda, çok sayıda sanal cihaz vardır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-150">When you first run hello solution, there are a number of simulated devices.</span></span> <span data-ttu-id="ef20f-151">Merhaba üretim hattı benzetimi sanal görevlerini gerçekleştiren, veri paylaşımı üç gerçek OPC UA sunucularının üretim hattı başına oluşur.</span><span class="sxs-lookup"><span data-stu-id="ef20f-151">hello production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="ef20f-152">Merhaba OPC UA hakkında daha fazla bilgi için bkz: [bağlı Fabrika SSS](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="ef20f-152">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="ef20f-153">A **harita** her cihazın görüntüler hello konumu toohello çözüm bağlı.</span><span class="sxs-lookup"><span data-stu-id="ef20f-153">A **map** that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="ef20f-154">Merhaba çözüm hello haritada hello Bing Haritalar API'si tooplot bilgileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-154">hello solution can use hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="ef20f-155">Aboneliğiniz Bing Haritalar Kurumsal API’si için etkinleştirildiyse, bu özellik otomatik olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="ef20f-156">Değilse, hello bkz [SSS] [ lnk-faq] toolearn nasıl toomake hello harita dinamik.</span><span class="sxs-lookup"><span data-stu-id="ef20f-156">If not, see hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="ef20f-157">Telemetri veya OEE/KPI değeri belirli bir eşiği aştığında oluşturulan uyarıların gösterildiği **Uyarılar** paneli.</span><span class="sxs-lookup"><span data-stu-id="ef20f-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="ef20f-158">Bir **genel donanım verimliliği** hello tüm kuruluş veya hello Fabrika/üretim hello OEE değerleri satır /, istasyon gösterir görüntüleme paneli.</span><span class="sxs-lookup"><span data-stu-id="ef20f-158">An **Overall Equipment Efficiency** panel that shows hello OEE values for hello whole enterprise, or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="ef20f-159">Bu değer hello istasyon görünüm toohello Kurumsal düzeyden toplanır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-159">This value is aggregated from hello station view toohello enterprise level.</span></span> <span data-ttu-id="ef20f-160">Merhaba OEE şekil ve bağlı öğeleri daha fazla analiz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-160">hello OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="ef20f-161">**Ana performans göstergelerini** üretilen birim ve hello tüm kuruluş veya hello Fabrika/üretim hattı tarafından kullanılan enerji hello sayısını görüntüler /, istasyon paneli görüntülemekte olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-161">**Key Performance Indicators** panel that displays hello number of units produced and energy used by hello whole enterprise or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="ef20f-162">Bu değerleri istasyon görünüm toohello kuruluş düzeyinde toplanır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-162">These values are aggregated from a station view toohello enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="ef20f-163">Fabrikaları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="ef20f-163">View factories</span></span>

<span data-ttu-id="ef20f-164">Merhaba *oluşturucuları* panel hello çözüm, durum ve üretim yapılandırmasına tüm hello factory'leri coğrafi konumunu hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-164">hello *Factories* panel shows you hello geographical location of all hello factories in hello solution, their status, and current production configuration.</span></span> <span data-ttu-id="ef20f-165">Merhaba konumları listeden hello çözüm hiyerarşideki diğer düzeyleri toohello gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-165">From hello locations list, you can navigate toohello other levels in hello solution hierarchy.</span></span> <span data-ttu-id="ef20f-166">Merhaba satırları hello listesinde hello Üretim satırları bu konumda ayrıntılarını bağlantı köprüleri edilir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-166">hello rows in hello list are hyperlinks that link details of hello production lines at that location.</span></span> <span data-ttu-id="ef20f-167">Bundan sonra olası toodrill hello üretim satırı ayrıntıları ve toohello istasyon seviye görünümü aşağı olur.</span><span class="sxs-lookup"><span data-stu-id="ef20f-167">It is then possible toodrill into hello production line details and down toohello station level view.</span></span> <span data-ttu-id="ef20f-168">Ayrıca, bir filtre toohello listesi uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-168">You can also apply a filter toohello list.</span></span>

![Önceden yapılandırılmış bağlı fabrika çözümü fabrikaları][cf-img-factories] 

1. <span data-ttu-id="ef20f-170">Merhaba **Fabrika paneli** hello Bu çözüm için Fabrika listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-170">hello **Factory panel** shows hello factory list for this solution.</span></span>

2. <span data-ttu-id="ef20f-171">Merhaba Fabrika liste başlangıçta altı oluşturucuları hello sağlama işlemi tarafından oluşturulan gösterir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-171">hello factory list initially shows six factories created by hello provisioning process.</span></span> <span data-ttu-id="ef20f-172">Ek sanal ve fiziksel cihaz toohello çözüm ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-172">You can add additional simulated and physical devices toohello solution.</span></span>

3. <span data-ttu-id="ef20f-173">bir Fabrika tooview hello ayrıntılarını hello Fabrika listesindeki hello satır'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-173">tooview hello details of a factory, click hello row in hello factory list.</span></span>

4. <span data-ttu-id="ef20f-174">bir üretim satırının tooview hello Ayrıntılar hello listesindeki hello satır'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-174">tooview hello details of a production line, click hello row in hello list.</span></span>

5. <span data-ttu-id="ef20f-175">istasyonu hello üretim satırındaki OPC UA düğümlerinin tooview hello yayımlanan, hello listesinde hello satıra tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-175">tooview hello published OPC UA nodes of a station on hello production line, click hello row in hello list.</span></span>

6. <span data-ttu-id="ef20f-176">Merhaba istasyon, belirli bir düğümde tooview Ayrıntılar hello listesindeki hello satır'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-176">tooview details on a specific node in hello station, click hello row in hello list.</span></span> <span data-ttu-id="ef20f-177">Bu eylemin hello bağlam panel zaman serisi Öngörüler görselleştirmeleri ile başlatır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-177">This action launches hello context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="ef20f-178">Bu grafik toodo çözümlemeler hello zaman serisi Öngörüler explorer ortamında'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-178">Click these graphs toodo further analysis in hello Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="ef20f-179">Haritayı görüntüleme</span><span class="sxs-lookup"><span data-stu-id="ef20f-179">View map</span></span>

<span data-ttu-id="ef20f-180">Aboneliğinizi erişim toohello Bing Haritalar API'si varsa, hello *oluşturucuları* eşlemesini gösterir, hello coğrafi konumu ve tüm hello oluşturucuları durumunu hello çözümde.</span><span class="sxs-lookup"><span data-stu-id="ef20f-180">If your subscription has access toohello Bing Maps API, hello *Factories* map shows you hello geographical location and status of all hello factories in hello solution.</span></span> <span data-ttu-id="ef20f-181">Merhaba konum ayrıntıları içine toodrill hello haritada görüntülenmelerini hello konumları'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-181">toodrill into hello location details, click hello locations displayed on hello map.</span></span>

![Önceden yapılandırılmış bağlı fabrika çözümü haritası][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="ef20f-183">Uyarıları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="ef20f-183">View alerts</span></span>

<span data-ttu-id="ef20f-184">Merhaba **uyarı** paneli gösterir, son oluşturulan uyarıların tooa bildirilen değer veya yapılandırılmış eşiğini aşan bir hesaplanmış OEE/KPI değeri.</span><span class="sxs-lookup"><span data-stu-id="ef20f-184">hello **Alert** panel shows you alerts generated due tooa reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="ef20f-185">Bu panoyu hello hiyerarşiden başlangıç istasyon düzey görünümü toohello genel görünümü her düzeyinde uyarıları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ef20f-185">This panel displays alerts at each level of hello hierarchy, from hello station level view toohello global view.</span></span> <span data-ttu-id="ef20f-186">Merhaba uyarıları hello uyarı, tarih, saat, konum ve yineleme sayısı açıklamasını içerir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-186">hello alerts contain a description of hello alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="ef20f-187">Merhaba zaman serisi istatistik verilerine kullanarak hello uyarıya neden toohello veri öngörü elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-187">You can gain insights in toohello data that caused hello alert using hello Time Series Insights data.</span></span> <span data-ttu-id="ef20f-188">Merhaba zaman serisi içindeki veri görselleştirilen Insights uyarıları uygunsa hello.</span><span class="sxs-lookup"><span data-stu-id="ef20f-188">hello Time Series Insights data is visualized in hello alerts where applicable.</span></span> <span data-ttu-id="ef20f-189">Bir yöneticiyseniz, gibi hello Uyarılardaki varsayılan eylemleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ef20f-189">If you are an Administrator, you can take default actions on hello alerts such as:</span></span>

* <span data-ttu-id="ef20f-190">Kapat hello uyarı.</span><span class="sxs-lookup"><span data-stu-id="ef20f-190">Close hello alert.</span></span>
* <span data-ttu-id="ef20f-191">Merhaba uyarı kabul ediyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-191">Acknowledge hello alert.</span></span>

<span data-ttu-id="ef20f-192">İsteğe bağlı olarak, daha karmaşık eylemler de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="ef20f-193">Örneğin, Merhaba baskısı OPC UA hello derleme düğümünün, olabilir:</span><span class="sxs-lookup"><span data-stu-id="ef20f-193">For example, for hello Pressure OPC UA Node of hello Assembly you could:</span></span>

* <span data-ttu-id="ef20f-194">Destek bilgilerini yeni bir tarayıcı penceresinde bir web sayfasında gösterme.</span><span class="sxs-lookup"><span data-stu-id="ef20f-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="ef20f-195">Merhaba hello uyarı hello aygıtta bir OPC UA yöntemini çağırarak en aza.</span><span class="sxs-lookup"><span data-stu-id="ef20f-195">Mitigate hello cause of hello alert by calling an OPC UA method on hello device.</span></span>
* <span data-ttu-id="ef20f-196">Merhaba varsayılan eylemleri Hello kullanılabilirliğini engelleyin.</span><span class="sxs-lookup"><span data-stu-id="ef20f-196">Suppress hello availability of hello default actions.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü uyarıları][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="ef20f-198">Bu uyarılar hello önceden yapılandırılmış çözümde yapılandırma dosyasında belirtilen kurallar tarafından oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="ef20f-198">These alerts are generated by rules that are specified in a configuration file in hello preconfigured solution.</span></span> <span data-ttu-id="ef20f-199">Merhaba OEE veya KPI rakamları veya OPC UA düğüm değerlerini kendi yapılandırılan eşiği aşıldığında bu kurallar uyarılar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-199">These rules can generate alerts when hello OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="ef20f-200">Merhaba **uyarıları paneli** hello bu çözümde oluşturulan uyarıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-200">hello **Alerts panel** shows hello alerts generated in this solution.</span></span>

2. <span data-ttu-id="ef20f-201">tooview hello bir uyarının ayrıntılarını hello uyarıları panelinde hello uyarıyı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-201">tooview hello details of an alert, click hello alert in hello alerts panel.</span></span>

3. <span data-ttu-id="ef20f-202">toofurther hello uyarı verileri çözümlemek, hello grafik ortamında hello uyarı paneli tooopen hello zaman serisi Öngörüler explorer'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-202">toofurther analyze hello alert data, click hello graph in hello alert panel tooopen hello Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="ef20f-203">Uyarı tooaddress Merhaba, çeşitli eylemler hello uyarı panelinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-203">tooaddress hello alert, several actions are available in hello alert panel.</span></span> <span data-ttu-id="ef20f-204">Merhaba sizin için uygun seçeneği seçin ve hello tıklatın eylem komut düğmesi yürütün.</span><span class="sxs-lookup"><span data-stu-id="ef20f-204">Choose hello appropriate option for you and click hello execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="ef20f-205">Genel donanım verimliliğini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="ef20f-205">View overall equipment efficiency</span></span>

<span data-ttu-id="ef20f-206">OEE oranları anahtar bir üretim ile ilgili işletimsel parametrelerini kullanarak hello üretim işlem verimliliğini hello.</span><span class="sxs-lookup"><span data-stu-id="ef20f-206">OEE rates hello efficiency of hello manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="ef20f-207">OEE olan standart ölçü hesaplanan hello kullanılabilirlik oranı, performans oranı ve kalite oranı çarparak sektör: OEE kullanılabilirlik performans x kalitesi x =.</span><span class="sxs-lookup"><span data-stu-id="ef20f-207">OEE is an industry standard measure calculated by multiplying hello availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![Önceden yapılandırılmış bağlı fabrika çözümü OEE][cf-img-oee]

1. <span data-ttu-id="ef20f-209">tooview OEE hello hiyerarşideki herhangi bir düzeye için ihtiyaç duyduğunuz toohello belirli görünüm gidin.</span><span class="sxs-lookup"><span data-stu-id="ef20f-209">tooview OEE for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="ef20f-210">Merhaba OEE bu görünümün hello paneli OEE yüzdesi hello yapmak hello öğelerin her biri ile birlikte görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ef20f-210">hello OEE for that view displays in hello panel along with each of hello elements that make up hello OEE percentage.</span></span>

2. <span data-ttu-id="ef20f-211">toofurther Merhaba OEE hello hiyerarşi verilerinde herhangi bir düzeye çözümlemek, hello OEE, kullanılabilirlik, performans veya kalite yüzdesi'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-211">toofurther analyze hello OEE for any level in hello hierarchy data, click either hello OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="ef20f-212">Bir bağlam paneli zaman serisi Insights ile Merhaba son bir saat, son 24 saat ve son 7 gün verileri gösterir güç beslemeli görselleştirmeleri görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-212">A context panel appears with Time Series Insights powered visualizations that shows data from hello last hour, last 24 hours, and last 7 days.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü TSI görselleştirmesi][cf-img-tsi-visualization]

3. <span data-ttu-id="ef20f-214">toofurther hello uyarı verileri çözümlemek, hello uyarı panelinde hello grafiğe tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-214">toofurther analyze hello alert data, click hello graph in hello alert panel.</span></span> <span data-ttu-id="ef20f-215">Bu eylemin hello zaman serisi Öngörüler explorer ortamı açılır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-215">This action opens hello Time Series Insights explorer environment.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü TSI gezgini][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="ef20f-217">Önemli Performans Göstergelerini görüntüleme</span><span class="sxs-lookup"><span data-stu-id="ef20f-217">View Key Performance Indicators</span></span>

<span data-ttu-id="ef20f-218">Merhaba çözümdür iki ana performans göstergelerini *saat başına birim* ve *KW/saat içinde kullanılan enerji*.</span><span class="sxs-lookup"><span data-stu-id="ef20f-218">hello solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![Önceden yapılandırılmış bağlı fabrika çözümü KPI][cf-img-kpi]

1. <span data-ttu-id="ef20f-220">saat veya hello hiyerarşideki herhangi bir düzeye için kullanılan enerji başına tooview birim toohello belirli görünüm ihtiyaç duyduğunuz gidin.</span><span class="sxs-lookup"><span data-stu-id="ef20f-220">tooview units per hour or energy used for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="ef20f-221">saat ve enerji başına Hello birim hello Masası'nda görünen kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-221">hello units per hour and energy used display in hello panel.</span></span>

2. <span data-ttu-id="ef20f-222">saat veya daha fazla hello hiyerarşideki herhangi bir düzeye için kullanılan enerji başına tooanalyze birim tıklatın hello hello ölçerde **anahtar performans göstergelerini** paneli.</span><span class="sxs-lookup"><span data-stu-id="ef20f-222">tooanalyze units per hour or energy used for any level in hello hierarchy further, click hello gauge in hello **Key Performance Indicators** panel.</span></span> <span data-ttu-id="ef20f-223">Zaman serisi gücü Öngörüler görselleştirmelerle hello son bir saat hello son 24 saat ve son 7 gün tooview verilerden etkinleştirme bağlamı paneli görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-223">A context panel appears with Time Series Insights powered visualizations enabling you tooview data from hello last hour, hello last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="ef20f-224">Senaryo gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="ef20f-224">Scenario review</span></span>

<span data-ttu-id="ef20f-225">Bu senaryoda, oluşturucuları OEE ve KPI'leri değerler hello panosunda izlenen.</span><span class="sxs-lookup"><span data-stu-id="ef20f-225">In this scenario, you monitored your factories OEE and KPIs values, in hello dashboard.</span></span> <span data-ttu-id="ef20f-226">Ardından anormallikleri algılama ile OEE ve KPI'leri toohelp için zaman serisi Öngörüler tooprovide daha fazla bilgi toohelp ayrıntıya daha fazla hello telemetri verileri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-226">You then used Time Series Insights tooprovide more information toohelp drill further into hello telemetry data for OEE and KPIs toohelp with detecting anomalies.</span></span> <span data-ttu-id="ef20f-227">Ayrıca hello uyarı paneli tooview sorunları, oluşturucuları ile kullanılan ve hello eylemleri kullanılabilir tooyou tooresolve hello uyarı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-227">You also used hello alert panel tooview issues with your factories and you used hello actions available tooyou tooresolve hello alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="ef20f-228">Diğer özellikler</span><span class="sxs-lookup"><span data-stu-id="ef20f-228">Other features</span></span>

<span data-ttu-id="ef20f-229">Aşağıdaki bölümlerde hello hello önceki senaryoda açıklanan olmayan bazı ek bağlı hello Fabrika çözüm özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="ef20f-229">hello following sections describe some additional features of hello connected factory solution that are not described in hello previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="ef20f-230">Filtreleri uygulama</span><span class="sxs-lookup"><span data-stu-id="ef20f-230">Apply filters</span></span>

1. <span data-ttu-id="ef20f-231">Merhaba tıklatın **Köşeli Çift Ayraca** toodisplay hello Fabrika konumları paneli veya hello uyarıları panelinde kullanılabilir filtrelerin listesi.</span><span class="sxs-lookup"><span data-stu-id="ef20f-231">Click hello **chevron** toodisplay a list of available filters in either hello factory locations panel or hello alerts panel.</span></span>

2. <span data-ttu-id="ef20f-232">Merhaba Filtreler paneli sizin için görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-232">hello filters panel is displayed for you.</span></span> 

    ![Önceden yapılandırılmış bağlı fabrika çözümü filtreleri][cf-img-alert-filter]

3. <span data-ttu-id="ef20f-234">İhtiyaç duyduğunuz hello filtre seçin.</span><span class="sxs-lookup"><span data-stu-id="ef20f-234">Choose hello filter that you require.</span></span> <span data-ttu-id="ef20f-235">Olası tootype serbest metin hello filtre alanlara da sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef20f-235">It is also possible tootype free text into hello filter fields.</span></span>

4. <span data-ttu-id="ef20f-236">Merhaba filtre ardından sizin için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-236">hello filter is then applied for you.</span></span> <span data-ttu-id="ef20f-237">Merhaba filtre durumu hello factory'leri görüntüler ve tabloları uyarıları bir huni aracılığıyla hello panosunda da gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-237">hello filter state is also shown in hello dashboard via a funnel that displays in hello factories and alerts tables.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü filtreleri][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="ef20f-239">Etkin bir filtreyi görüntülenen hello OEE ve KPI değerleri etkilemez yalnızca hello listesi içeriğine filtre uygular.</span><span class="sxs-lookup"><span data-stu-id="ef20f-239">An active filter does not affect hello displayed OEE and KPI values, it only filters hello list contents.</span></span>

5. <span data-ttu-id="ef20f-240">tooclear bir filtre hello Huni tıklayın ve filtre hello filtre bağlamı panelinde'yi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-240">tooclear a filter, click hello funnel and click filter in hello filter context panel.</span></span> <span data-ttu-id="ef20f-241">Merhaba metin **tüm** hello factory'leri görüntülenir ve tabloları uyarır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-241">hello text **All** is displayed in hello factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="ef20f-242">OPC UA sunucusuna göz atma</span><span class="sxs-lookup"><span data-stu-id="ef20f-242">Browse an OPC UA server</span></span>

<span data-ttu-id="ef20f-243">Hello önceden yapılandırılmış çözümü dağıttığınızda, hello çözüm tarayıcı yoluyla göz atabilirsiniz benzetimli OPC UA sunucuları otomatik olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-243">When you deploy hello preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via hello solution browser.</span></span> <span data-ttu-id="ef20f-244">Bu sunucular, *sanal OPC UA sunucularıdır*.</span><span class="sxs-lookup"><span data-stu-id="ef20f-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="ef20f-245">Sanal sunucuları sizin için tooexperiment Merhaba, gerek toodeploy gerçek, fiziksel sunucuları olmadan hello önceden yapılandırılmış Çözümle kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-245">Simulated servers make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical servers.</span></span> <span data-ttu-id="ef20f-246">Merhaba tooconnect gerçek OPC UA sunucu toohello çözüm istiyorsanız bkz [OPC UA cihaz bağlı toohello Fabrika önceden yapılandırılmış çözümünüz bağlanmak] [ lnk-connect-cf] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="ef20f-246">If you do want tooconnect a real OPC UA server toohello solution, see hello [Connect your OPC UA device toohello connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="ef20f-247">Merhaba tıklatın **Fabrika simgesi** hello Panosu gezinti çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="ef20f-247">Click hello **factory icon** in hello dashboard navigation bar.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü sunucu tarayıcısı][cf-img-server-browser]

2. <span data-ttu-id="ef20f-249">Merhaba sunuculardan biri hello önceden yapılandırılmış listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="ef20f-249">Choose one of hello servers from hello preconfigured list.</span></span> <span data-ttu-id="ef20f-250">Bu liste, sizin için önceden yapılandırılmış hello çözümde dağıtılan hello sunucularını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-250">This list shows hello servers that are deployed for you in hello preconfigured solution.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü sunucu seçimi][cf-img-server-choice]

3. <span data-ttu-id="ef20f-252">**Bağlan**’a tıklayın; güvenlik iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="ef20f-253">İsteğe bağlı olarak Hello benzetimi için güvenli tooclick olan **devam et**</span><span class="sxs-lookup"><span data-stu-id="ef20f-253">For hello simulation, it is safe tooclick **Proceed**</span></span>

4. <span data-ttu-id="ef20f-254">tooexpand herhangi bir hello sunucu ağacında hello düğüme tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-254">tooexpand any of hello nodes in hello server tree, click it.</span></span> <span data-ttu-id="ef20f-255">Yayımlama telemetrisi olan düğümlerin yanında bir onay işareti vardır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü sunucu ağacı][cf-img-server-tree]

5. <span data-ttu-id="ef20f-257">Bir öğe tooread sağ tıklatın, yazma, yayımlama veya bu düğüm çağırın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-257">Right-click an item tooread, write, publish, or call that node.</span></span> <span data-ttu-id="ef20f-258">Merhaba eylemleri kullanılabilir tooyou, izinleri ve hello düğümü hello özniteliklerini bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-258">hello actions available tooyou depend on your permissions and hello attributes of hello node.</span></span> <span data-ttu-id="ef20f-259">Merhaba seçeneği toodisplays hello belirli düğüm hello değerini gösteren bir bağlam panel okuyun.</span><span class="sxs-lookup"><span data-stu-id="ef20f-259">hello read option toodisplays a context panel showing hello value of hello specific node.</span></span> <span data-ttu-id="ef20f-260">Yeni bir değer girebileceğiniz bir bağlam panel Hello yazma seçeneği görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ef20f-260">hello write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="ef20f-261">Merhaba çağrısı seçeneği hello çağrısı için başlangıç parametreleri girebilecekleri bir düğüm görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ef20f-261">hello call option displays a node where you can enter hello parameters for hello call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="ef20f-262">Düğümü yayımlama</span><span class="sxs-lookup"><span data-stu-id="ef20f-262">Publish a node</span></span>

<span data-ttu-id="ef20f-263">Göz atarken bir *benzetimli OPC UA sunucu*, yeni düğümler toopublish de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-263">When you browse a *simulated OPC UA server*, you can also choose toopublish new nodes.</span></span> <span data-ttu-id="ef20f-264">Bu düğümden hello çözüm de hello telemetri analiz edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-264">You can analyze hello telemetry from these nodes in hello solution.</span></span> <span data-ttu-id="ef20f-265">Bunlar *benzetimli OPC UA sunucuları* gerçek, fiziksel cihazları dağıtmadan hello önceden yapılandırılmış çözümü ile kolay tooexperiment kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="ef20f-265">These *simulated OPC UA servers* make it easy tooexperiment with hello preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="ef20f-266">Merhaba toopublish istediğiniz OPC UA sunucu tarayıcı ağaç düğümünde tooa göz atın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-266">Browse tooa node in hello OPC UA server browser tree that you wish toopublish.</span></span>

2. <span data-ttu-id="ef20f-267">Merhaba düğümünü sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-267">Right-click hello node.</span></span>

3. <span data-ttu-id="ef20f-268">**Yayımla**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="ef20f-268">Choose **Publish**.</span></span>

    ![Bağlı fabrika yayımlama düğümü][cf-img-publish-node]

4. <span data-ttu-id="ef20f-270">Merhaba yayımlama söyleyen bir bağlam paneli görünür başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="ef20f-270">A context panel appears which tells you that hello publish has succeeded.</span></span> <span data-ttu-id="ef20f-271">Merhaba düğümü hello istasyon düzeyi görünümünde yanında bir onay işareti görünür.</span><span class="sxs-lookup"><span data-stu-id="ef20f-271">hello node appears in hello station level view with a check mark beside it.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü yayımlama başarısı][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="ef20f-273">Komut ve denetim</span><span class="sxs-lookup"><span data-stu-id="ef20f-273">Command and control</span></span>

<span data-ttu-id="ef20f-274">Merhaba bağlı Fabrika komut ve endüstri aygıtlarınızı hello bulut doğrudan denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef20f-274">hello connected factory allows you command and control your industry devices directly from hello cloud.</span></span> <span data-ttu-id="ef20f-275">Bu özellik toorespond tooalerts hello aygıt tarafından üretilen kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-275">You can use this feature toorespond tooalerts generated by hello device.</span></span> <span data-ttu-id="ef20f-276">Örneğin, bir komut toohello aygıt hello buluttan gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="ef20f-276">For example, you could send a command toohello device from hello cloud.</span></span> <span data-ttu-id="ef20f-277">Kullanılabilir komutlar hello hello bulabilirsiniz **StationCommands** hello OPC UA sunucuları tarayıcı ağaç düğümü.</span><span class="sxs-lookup"><span data-stu-id="ef20f-277">You can find hello available commands in hello **StationCommands** node in hello OPC UA servers browser tree.</span></span> <span data-ttu-id="ef20f-278">Bu senaryoda, bir baskısı yayın Vana Münih bir üretim satırının hello derleme istasyondaki açın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-278">In this scenario, you open a pressure release valve on hello assembly station of a production line in Munich.</span></span> <span data-ttu-id="ef20f-279">toouse hello komut ve denetim işlevleri, hello olmalıdır **yönetici** rolü hello için önceden yapılandırılmış Çözüm dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="ef20f-279">toouse hello command and control functionality, you must be in hello **Administrator** role for hello preconfigured solution deployment.</span></span>

1. <span data-ttu-id="ef20f-280">Toohello Gözat **StationCommands** hello OPC UA sunucu tarayıcı ağaç düğümü.</span><span class="sxs-lookup"><span data-stu-id="ef20f-280">Browse toohello **StationCommands** node in hello OPC UA server browser tree.</span></span>

2. <span data-ttu-id="ef20f-281">Kullanmak istediğiniz hello komutu seçin.</span><span class="sxs-lookup"><span data-stu-id="ef20f-281">Choose hello command that you wish use.</span></span>

3. <span data-ttu-id="ef20f-282">Merhaba düğümünü sağ tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ef20f-282">Right-click hello node.</span></span>

4. <span data-ttu-id="ef20f-283">**Çağır**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="ef20f-283">Choose **Call**.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü çağır komutu][cf-img-call-command]

5. <span data-ttu-id="ef20f-285">Bir bağlam panel hangi yöntemi bildiren hakkında toocall olan ve herhangi bir parametre ayrıntıyı uygulanabilir olduğunda görünür.</span><span class="sxs-lookup"><span data-stu-id="ef20f-285">A context panel appears informing you which method you are about toocall and any parameter details is applicable.</span></span>

6. <span data-ttu-id="ef20f-286">**Çağır**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="ef20f-286">Choose **Call**.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü çağrı bağlamı][cf-img-call-context]

7. <span data-ttu-id="ef20f-288">yöntem çağrısının Merhaba, başarılı bir şekilde güncelleştirilmiş tooinform Hello bağlam panosudur.</span><span class="sxs-lookup"><span data-stu-id="ef20f-288">hello context panel is updated tooinform you that hello method call succeeded.</span></span> <span data-ttu-id="ef20f-289">Merhaba çağrı sonucunda güncelleştirilmiş hello baskısı düğümü hello değeri okuyarak başarılı hello çağrısı doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-289">You can verify hello call succeeded by reading hello value of hello pressure node that updated as a result of hello call.</span></span>

    ![Önceden yapılandırılmış bağlı fabrika çözümü çağrı başarısı][cf-img-call-success]


## <a name="behind-hello-scenes"></a><span data-ttu-id="ef20f-291">Merhaba arka planda</span><span class="sxs-lookup"><span data-stu-id="ef20f-291">Behind hello scenes</span></span>

<span data-ttu-id="ef20f-292">Önceden yapılandırılmış çözümü dağıttığınızda, hello dağıtım işlemi hello Seçtiğiniz Azure aboneliği birden çok kaynak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ef20f-292">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="ef20f-293">Bu kaynaklar hello Azure görüntüleyebilirsiniz [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="ef20f-293">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="ef20f-294">Merhaba dağıtım işlemi oluşturur bir **kaynak grubu** önceden yapılandırılmış çözümünüz için seçtiğiniz hello adına dayalı bir ada sahip:</span><span class="sxs-lookup"><span data-stu-id="ef20f-294">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Önceden yapılandırılmış çözümde hello Azure portalı][img-cf-portal]

<span data-ttu-id="ef20f-296">Her bir kaynağın hello ayarları hello hello kaynak grubundaki kaynaklar listesinde seçerek görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-296">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="ef20f-297">Merhaba hello önceden yapılandırılmış çözüm için kaynak kodunu da görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef20f-297">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="ef20f-298">Merhaba bağlı Fabrika önceden yapılandırılmış çözümün kaynak kodunu olduğu hello [azure-IOT-bağlı-Fabrika] [ lnk-cfgithub] GitHub deposunu:</span><span class="sxs-lookup"><span data-stu-id="ef20f-298">hello connected factory preconfigured solution source code is in hello [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="ef20f-299">İşiniz bittiğinde, Azure aboneliğinizin hello üzerinde hello önceden yapılandırılmış çözüm silebilirsiniz [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="ef20f-299">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="ef20f-300">Bu sitenin tüm hello önceden yapılandırılmış çözümü oluşturduğunuzda sağlanan kaynakları hello tooeasily Sil sağlar.</span><span class="sxs-lookup"><span data-stu-id="ef20f-300">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="ef20f-301">her şeyi silin tooensure toohello önceden yapılandırılmış çözümle ilgili, üzerinde hello silme [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="ef20f-301">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="ef20f-302">Merhaba portal Hello kaynak grubunda silmeyin.</span><span class="sxs-lookup"><span data-stu-id="ef20f-302">Do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ef20f-303">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="ef20f-303">Next Steps</span></span>

<span data-ttu-id="ef20f-304">Çalışan bir önceden çözüm dağıttıktan sonra aşağıdaki makaleler hello okuyarak IOT paketi ile Başlarken devam edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ef20f-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="ef20f-305">[Önceden yapılandırılmış bağlı fabrika çözümü yönergeleri][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="ef20f-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="ef20f-306">[Cihaz toohello bağlı Fabrika önceden yapılandırılmış çözümünüz Bağlan][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="ef20f-306">[Connect your device toohello Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="ef20f-307">[Merhaba azureiotsuite.com sitesindeki izinler][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="ef20f-307">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

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