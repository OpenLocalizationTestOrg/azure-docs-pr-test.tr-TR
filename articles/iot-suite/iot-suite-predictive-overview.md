---
title: "önceden yapılandırılmış çözüm aaaPredictive bakım | Microsoft Docs"
description: "Hello Azure IOT paketi Tahmine dayalı bakım açıklamasını önceden yapılandırılmış çözümü."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="40c2b-103">Önceden yapılandırılmış tahmine dayalı bakım çözümüne genel bakış</span><span class="sxs-lookup"><span data-stu-id="40c2b-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="40c2b-104">Merhaba *Tahmine dayalı Bakım* [önceden yapılandırılmış çözüm] [ lnk_preconfigured_solutions] hello biri [Microsoft Azure IOT paketi] [ lnk_iot_suite] önceden yapılandırılmış çözümler.</span><span class="sxs-lookup"><span data-stu-id="40c2b-104">hello *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of hello [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="40c2b-105">Bu çözüm, gerçek zamanlı cihaz telemetri koleksiyonunu [Azure Machine Learning][lnk-machine-learning] kullanılarak oluşturulan tahmine dayalı modelle tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="40c2b-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="40c2b-106">Azure IOT paketi ile ve hızlı bir şekilde ve kolayca tooand İzleyici varlıklar bağlanmak, gerçek zamanlı panolar ve görselleştirmeleri telemetri analiz edin.</span><span class="sxs-lookup"><span data-stu-id="40c2b-106">With Azure IoT Suite, you can quickly and easily connect tooand monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="40c2b-107">Hello Tahmine dayalı bakım çözümü hello panolar ve görselleştirmeleri, verimlilikleri yönetebilen ve gelir akışlarını geliştiren yeni zekaya sahip sağlar.</span><span class="sxs-lookup"><span data-stu-id="40c2b-107">In hello predictive maintenance solution, hello dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="hello-scenario"></a><span data-ttu-id="40c2b-108">Merhaba senaryosu</span><span class="sxs-lookup"><span data-stu-id="40c2b-108">hello Scenario</span></span>

<span data-ttu-id="40c2b-109">Fabrikam, rekabetçi fiyatlarıyla büyük müşteri deneyimine odaklanan bölgesel bir havayoludur.</span><span class="sxs-lookup"><span data-stu-id="40c2b-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="40c2b-110">Uçuş rötarlarının bir nedeni bakım sorunlarıdır ve uçak motorunun bakımı özellikle zordur.</span><span class="sxs-lookup"><span data-stu-id="40c2b-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="40c2b-111">Böylece olarak kendi motorları muayene eder ve tooa planı göre bakım zamanlar Fabrikam uçuş sırasında maliyeti, motor arızasından kaçınmalısınız.</span><span class="sxs-lookup"><span data-stu-id="40c2b-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according tooa plan.</span></span> <span data-ttu-id="40c2b-112">Ancak, uçak motorları her zaman yıpranmaz aynı hello.</span><span class="sxs-lookup"><span data-stu-id="40c2b-112">However, aircraft engines don’t always wear hello same.</span></span> <span data-ttu-id="40c2b-113">Motorlardı bazı gereksiz bakımlar gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="40c2b-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="40c2b-114">Daha da önemlisi, bakım yapılana kadar çıkan sorunlar nedeniyle uçağın yerde kalmasıdır.</span><span class="sxs-lookup"><span data-stu-id="40c2b-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="40c2b-115">Bir konumda Uçağın olduğunda, burada doğru teknisyenlerin Merhaba veya yedek parçaların kullanılabilir değil, bu sorunları özellikle maliyetli olabilir.</span><span class="sxs-lookup"><span data-stu-id="40c2b-115">If an aircraft is at a location where hello right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="40c2b-116">Fabrikam uçağının, Hello motorları, uçuş sırasında motor koşullarını izleyen algılayıcılar ile donatılmıştır.</span><span class="sxs-lookup"><span data-stu-id="40c2b-116">hello engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="40c2b-117">Fabrikam hello Tahmine dayalı bakım çözümü toocollect hello algılayıcı verilerini hello uçuş sırasında toplanan kullanır.</span><span class="sxs-lookup"><span data-stu-id="40c2b-117">Fabrikam uses hello predictive maintenance solution toocollect hello sensor data collected during hello flight.</span></span> <span data-ttu-id="40c2b-118">Motor çalışması yıllarca biriktirdikten sonra hatası verileri Fabrikam'ın veri bilimcilerine şekilde toopredict hello uçak motorunun kalan kullanım ömrü (RUL) modeli oluşturmuştur.</span><span class="sxs-lookup"><span data-stu-id="40c2b-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way toopredict hello Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="40c2b-119">Merhaba modeli dört hello altyapısı algılayıcı verilerinden ve tooeventual hatası müşteri adayları motor yıpranmasıyla ilişkili arasında bir ilişki kullanır.</span><span class="sxs-lookup"><span data-stu-id="40c2b-119">hello model uses a correlation between data from four of hello engine sensors and engine wear that leads tooeventual failure.</span></span> <span data-ttu-id="40c2b-120">Fabrikam tooperform normal incelemeleri tooensure güvenliği devam ederken, bunu şimdi hello modelleri toocompute hello RUL her motor için her uçuştan sonra kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c2b-120">While Fabrikam continues tooperform regular inspections tooensure safety, it can now use hello models toocompute hello RUL for each engine after every flight.</span></span> <span data-ttu-id="40c2b-121">Merhaba modeli hello motorlarından hello uçuş sırasında toplanan hello telemetri kullanır.</span><span class="sxs-lookup"><span data-stu-id="40c2b-121">hello model uses hello telemetry collected from hello engines during hello flight.</span></span> <span data-ttu-id="40c2b-122">Fabrikam artık arızanın ve bakım planının ileri tarihli noktalarını tahmin edebiliyor ve önceden onarıyor.</span><span class="sxs-lookup"><span data-stu-id="40c2b-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="40c2b-123">Merhaba çözüm modeli asıl motor yıpranması verilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="40c2b-123">hello solution model uses actual engine wear data.</span></span>

<span data-ttu-id="40c2b-124">Bakım gerekli olduğunda hello noktayı tahmin ederek çalışmasını, Fabrikam, işlemleri tooreduce maliyetleri en iyi duruma getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c2b-124">By predicting hello point when maintenance is required, Fabrikam can optimize its operations tooreduce costs.</span></span>

<span data-ttu-id="40c2b-125">Bakım düzenleyicileri, zamanlayıcılar ile çalışarak:</span><span class="sxs-lookup"><span data-stu-id="40c2b-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="40c2b-126">Belirli bir konumda Uçağın ile bakım toocoincide planlayın.</span><span class="sxs-lookup"><span data-stu-id="40c2b-126">Plan maintenance toocoincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="40c2b-127">Yeterli zaman bozmadan hello uçak toobe hizmet dışına için kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="40c2b-127">Ensure sufficient time is available for hello aircraft toobe out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="40c2b-128">tooschedule teknisyenleri tooensure Uçağın bekleme süresi olmadan verimli bir şekilde sunulur.</span><span class="sxs-lookup"><span data-stu-id="40c2b-128">tooschedule technicians tooensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="40c2b-129">Stok denetimi yöneticileri bakım planlarını alır; bu nedenle, sipariş sürecini ve yedek parça stoğunu en iyi hale getirebilirler.</span><span class="sxs-lookup"><span data-stu-id="40c2b-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="40c2b-130">Bu etkinlikler Fabrikam toominimize Uçağın yerdeki süresini etkinleştir ve Yolcuların ve personelin hello güvenliğini sağlarken işletim maliyetlerini azaltabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c2b-130">These activities enable Fabrikam toominimize aircraft ground time and reduce operating costs while ensuring hello safety of passengers and crew.</span></span>

<span data-ttu-id="40c2b-131">toounderstand nasıl [Azure IOT paketi] [ lnk_iot_suite] hello müşterilerin gereksinim toorealize hello olası sağlar Tahmine dayalı bakım bu gözden [bilgi grafiği] [lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="40c2b-131">toounderstand how [Azure IoT Suite][lnk_iot_suite] provides hello capabilities customers need toorealize hello potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-hello-predictive-maintenance-solution-is-built"></a><span data-ttu-id="40c2b-132">Merhaba Tahmine dayalı bakım çözümü nasıl oluşturulur</span><span class="sxs-lookup"><span data-stu-id="40c2b-132">How hello predictive maintenance solution is built</span></span>

<span data-ttu-id="40c2b-133">Hello çözüm bir var olan Azure Machine Learning modeli IOT paketi hizmetleriyle toplanan cihaz telemetrisi çalışma bu özellikler bir şablon tooshow kullanır.</span><span class="sxs-lookup"><span data-stu-id="40c2b-133">hello solution uses an existing Azure Machine Learning model available as a template tooshow these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="40c2b-134">Microsoft'ta bir [regresyon modeli] [ lnk_regression_model] herkese açık verilerine dayalı uçak motorunun<sup>\[1\]</sup>ve adım adım nasıl toouse hello model konusunda yönergeler.</span><span class="sxs-lookup"><span data-stu-id="40c2b-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how toouse hello model.</span></span>

<span data-ttu-id="40c2b-135">Hello Azure IOT Tahmine dayalı bakım çözümü bu şablondan oluşturulan hello regresyon modeli kullanır.</span><span class="sxs-lookup"><span data-stu-id="40c2b-135">hello Azure IoT predictive maintenance solution uses hello regression model created from this template.</span></span> <span data-ttu-id="40c2b-136">Merhaba modeli Azure aboneliğinize dağıtılır ve otomatik olarak oluşturulan bir API üretir.</span><span class="sxs-lookup"><span data-stu-id="40c2b-136">hello model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="40c2b-137">Merhaba çözüm içeren bir alt kümesini 4 (toplamda 100) temsil eden veri sınama hello motorları ve hello 4 (of toplamda 21) algılayıcı veri akışı.</span><span class="sxs-lookup"><span data-stu-id="40c2b-137">hello solution includes a subset of hello testing data representing 4 (of 100 total) engines and hello 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="40c2b-138">Yeterli tooprovide hello eğitilen model ait doğru sonuç verilerdir.</span><span class="sxs-lookup"><span data-stu-id="40c2b-138">This data is sufficient tooprovide an accurate result from hello trained model.</span></span>

<span data-ttu-id="40c2b-139">*\[1\] A. Saxena ve K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set" (Turbofan Motor Bozulması Benzetimi Veri Kümesi), NASA Ames Prognostics Veri Deposu (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="40c2b-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="40c2b-140">Tahmine dayalı bakım ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="40c2b-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="40c2b-141">Bu öğretici nasıl tooprovision hello Tahmine dayalı bakım çözümü gösterir.</span><span class="sxs-lookup"><span data-stu-id="40c2b-141">This tutorial shows you how tooprovision hello predictive maintenance solution.</span></span> <span data-ttu-id="40c2b-142">Bu ayrıca, hello hello Tahmine dayalı bakım çözümü, temel özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="40c2b-142">It also walks you through hello basic features of hello predictive maintenance solution.</span></span> <span data-ttu-id="40c2b-143">Bu özelliklerin yanı sıra hello önceden yapılandırılmış çözümü dağıtır hello çözüm Panosu üzerinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c2b-143">You can access many of these features through hello solution dashboard that deploys along with hello preconfigured solution.</span></span>

<span data-ttu-id="40c2b-144">toocomplete Bu öğreticide, bir etkin Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="40c2b-144">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="40c2b-145">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c2b-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="40c2b-146">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="40c2b-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="40c2b-147">Çok oturum[azureiotsuite.com] [ lnk-azureiotsuite] Azure kullanarak hesap kimlik bilgilerini ve tıklatın  **+**  toocreate bir çözüm.</span><span class="sxs-lookup"><span data-stu-id="40c2b-147">Log on too[azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** toocreate a solution.</span></span>
1. <span data-ttu-id="40c2b-148">Tıklatın **seçin** hello **Tahmine dayalı Bakım** döşeme.</span><span class="sxs-lookup"><span data-stu-id="40c2b-148">Click **Select** hello **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="40c2b-149">Tahmine dayalı bakım için önceden yapılandırılmış çözümünüze ait bir **Çözüm adı** girin.</span><span class="sxs-lookup"><span data-stu-id="40c2b-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="40c2b-150">Select hello **bölge** ve **abonelik** toouse tooprovision hello çözüm istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="40c2b-150">Select hello **Region** and **Subscription** you want toouse tooprovision hello solution.</span></span>
1. <span data-ttu-id="40c2b-151">Tıklatın **çözümü Oluştur** toobegin hello sağlama işlemi.</span><span class="sxs-lookup"><span data-stu-id="40c2b-151">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="40c2b-152">Bu işlem genellikle birkaç dakika toorun alır.</span><span class="sxs-lookup"><span data-stu-id="40c2b-152">This process typically takes several minutes toorun.</span></span>

### <a name="wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="40c2b-153">İşlem toocomplete sağlama Merhaba bekleyin</span><span class="sxs-lookup"><span data-stu-id="40c2b-153">Wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="40c2b-154">Çözümünüzle birlikte Hello kutucuğa tıklayın **sağlama** durumu.</span><span class="sxs-lookup"><span data-stu-id="40c2b-154">Click hello tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="40c2b-155">Bildirim hello **hazırlama durumlarına** gibi Azure Hizmetleri Azure aboneliğinize dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="40c2b-155">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="40c2b-156">Hazırlama tamamlandığında durum değişikliklerini çok hello**hazır**.</span><span class="sxs-lookup"><span data-stu-id="40c2b-156">Once provisioning completes, hello status changes too**Ready**.</span></span>
1. <span data-ttu-id="40c2b-157">Merhaba döşeme toosee hello hello sağ bölmede çözümünüzün ayrıntılarını'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="40c2b-157">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span> <span data-ttu-id="40c2b-158">Bu bölmesinden hello çözüm panosu ve erişim hello Machine Learning çalışma alanı başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c2b-158">From this pane, you can launch hello solution dashboard and access hello Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="40c2b-159">Merhaba önceden yapılandırılmış çözümü dağıtma sorunlarla karşılaşırsanız, gözden [hello azureiotsuite.com sitesindeki izinler] [ lnk-permissions] ve hello [SSS] [ lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="40c2b-159">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [FAQ][lnk-faq].</span></span> <span data-ttu-id="40c2b-160">Merhaba sorunları devam ederse, bir hizmet bileti hello üzerinde oluşturma [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="40c2b-160">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="40c2b-161">Çözümünüz için listelenmeyen toosee beklediğiniz ayrıntılar bulunur?</span><span class="sxs-lookup"><span data-stu-id="40c2b-161">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="40c2b-162">[User Voice](https://feedback.azure.com/forums/321918-azure-iot)'da bize özellik önerileri verin.</span><span class="sxs-lookup"><span data-stu-id="40c2b-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-hello-solution"></a><span data-ttu-id="40c2b-163">Merhaba çözümü görüntüle</span><span class="sxs-lookup"><span data-stu-id="40c2b-163">View hello solution</span></span>

<span data-ttu-id="40c2b-164">Bu bölümde, hello çözümü kullanıcı Arabirimi aracılığıyla size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="40c2b-164">This section guides you through hello solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="40c2b-165">Tahmine Dayalı Bakım Panosu</span><span class="sxs-lookup"><span data-stu-id="40c2b-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="40c2b-166">Merhaba web uygulamasındaki bu sayfa Powerbı JavaScript denetimlerini kullanır (Merhaba bkz [Powerbı-visuals repository][lnk-powerbi]) toovisualize:</span><span class="sxs-lookup"><span data-stu-id="40c2b-166">This page in hello web application uses PowerBI JavaScript controls (see hello [PowerBI-visuals repository][lnk-powerbi]) toovisualize:</span></span>

* <span data-ttu-id="40c2b-167">blob depolama hello Stream Analytics işlerine Hello çıktı verileri.</span><span class="sxs-lookup"><span data-stu-id="40c2b-167">hello output data from hello Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="40c2b-168">Merhaba RUL ve döngüsü uçak motoru başına sayısı.</span><span class="sxs-lookup"><span data-stu-id="40c2b-168">hello RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a><span data-ttu-id="40c2b-169">Merhaba hello bulut çözümünün davranışını Gözlemleme</span><span class="sxs-lookup"><span data-stu-id="40c2b-169">Observing hello behavior of hello cloud solution</span></span>

<span data-ttu-id="40c2b-170">İçinde Azure portal Merhaba, toohello kaynak grubuna gidin hello çözüm adı ile hazırlanan kaynaklarınızı tooview seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="40c2b-170">In hello Azure portal, navigate toohello resource group with hello solution name you chose tooview your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="40c2b-171">Merhaba önceden yapılandırılmış çözümü hazırlarken, bir bağlantı toohello Machine Learning çalışma alanı içeren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="40c2b-171">When you provision hello preconfigured solution, you receive an email with a link toohello Machine Learning workspace.</span></span> <span data-ttu-id="40c2b-172">Merhaba toohello Machine Learning çalışma alanına da gidebilirsiniz [azureiotsuite.com] [ lnk-azureiotsuite] sağlanan çözümünüz için sayfa.</span><span class="sxs-lookup"><span data-stu-id="40c2b-172">You can also navigate toohello Machine Learning workspace from hello [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="40c2b-173">Merhaba çözüm hello olduğunda bir kutucuğu bu sayfada kullanılabilir **hazır** durumu.</span><span class="sxs-lookup"><span data-stu-id="40c2b-173">A tile is available on this page when hello solution is in hello **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="40c2b-174">Merhaba çözüm portalında hello örneği iki motorları her dört algılayıcılar uçak başına ile dört sanal cihaz toorepresent iki uçak ile sağlandığında görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c2b-174">In hello solution portal, you can see that hello sample is provisioned with four simulated devices toorepresent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="40c2b-175">Toohello çözüm portalına ilk gittiğinizde hello benzetim durdurulur.</span><span class="sxs-lookup"><span data-stu-id="40c2b-175">When you first navigate toohello solution portal, hello simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="40c2b-176">Tıklatın **benzetimi Başlat** toobegin hello benzetimi.</span><span class="sxs-lookup"><span data-stu-id="40c2b-176">Click **Start simulation** toobegin hello simulation.</span></span> <span data-ttu-id="40c2b-177">Merhaba algılayıcı geçmişi, RUL, döngüler ve RUL geçmişini doldurmak hello Pano.</span><span class="sxs-lookup"><span data-stu-id="40c2b-177">hello sensor history, RUL, Cycles, and RUL history populate hello dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="40c2b-178">RUL değeri 160 altındaysa (gösterim amaçlı seçilen rastgele eşik) olduğunda hello çözüm portalı RUL görüntülemek bir uyarı simgesi sonraki bir toohello görüntüler.</span><span class="sxs-lookup"><span data-stu-id="40c2b-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), hello solution portal displays a warning symbol next toohello RUL display.</span></span> <span data-ttu-id="40c2b-179">Merhaba çözüm portalı da hello uçak motorunu sarı vurgular.</span><span class="sxs-lookup"><span data-stu-id="40c2b-179">hello solution portal also highlights hello aircraft engine in yellow.</span></span> <span data-ttu-id="40c2b-180">Nasıl hello RUL değerleri bir genel düşüş eğilimi dikkat edin, ancak toobounce yukarı ve aşağı eğilimindedir.</span><span class="sxs-lookup"><span data-stu-id="40c2b-180">Notice how hello RUL values have a general downward trend overall, but tend toobounce up and down.</span></span> <span data-ttu-id="40c2b-181">Bu davranış hello değişen döngü uzunlukları ve hello model doğruluğundan sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="40c2b-181">This behavior results from hello varying cycle lengths and hello model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="40c2b-182">Merhaba tam benzetim, 148 Döngüyü yaklaşık 35 dakika toocomplete alır.</span><span class="sxs-lookup"><span data-stu-id="40c2b-182">hello full simulation takes around 35 minutes toocomplete 148 cycles.</span></span> <span data-ttu-id="40c2b-183">Merhaba 160 RUL eşiği ilk seferinde yaklaşık 5 dakika Merhaba karşılanır ve her iki motor hello eşiğine yaklaşık 8 dakikada vardı.</span><span class="sxs-lookup"><span data-stu-id="40c2b-183">hello 160 RUL threshold is met for hello first time at around 5 minutes and both engines hit hello threshold at around 8 minutes.</span></span>

<span data-ttu-id="40c2b-184">Merhaba benzetim 148 döngü için hello tam veri kümesinde çalışır ve son RUL ve döngü değerlerinde de kapanır.</span><span class="sxs-lookup"><span data-stu-id="40c2b-184">hello simulation runs through hello complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="40c2b-185">Merhaba benzetimi herhangi durdurabilirsiniz noktası ancak tıklatarak **benzetimi Başlat** yürütmelerini hello hello dataset hello başından benzetimi.</span><span class="sxs-lookup"><span data-stu-id="40c2b-185">You can stop hello simulation at any point, but clicking **Start Simulation** replays hello simulation from hello start of hello dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40c2b-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="40c2b-186">Next steps</span></span>

<span data-ttu-id="40c2b-187">Azure IOT okuma Tahmine dayalı bakım senaryolarını nasıl sağladığı hakkında daha fazla toolearn [hello nesnelerin interneti'nden değer yakalama][lnk_capture_value].</span><span class="sxs-lookup"><span data-stu-id="40c2b-187">toolearn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from hello Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="40c2b-188">Ele bir [izlenecek] [ lnk-predictive-walkthrough] hello Tahmine dayalı bakım çözümü.</span><span class="sxs-lookup"><span data-stu-id="40c2b-188">Take a [walkthrough][lnk-predictive-walkthrough] of hello predictive maintenance solution.</span></span>

<span data-ttu-id="40c2b-189">Merhaba bazıları diğer özellikleri ve yetenekleri hello IOT paketi önceden yapılandırılmış çözümleri ayrıca keşfedebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="40c2b-189">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="40c2b-190">[IoT Paketi için sık sorulan sorular][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="40c2b-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="40c2b-191">[Merhaba IOT güvenlikten plan][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="40c2b-191">[IoT security from hello ground up][lnk-security-groundup]</span></span>

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/