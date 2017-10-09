---
title: "kullanmaya aaaGet önceden yapılandırılmış çözümleri | Microsoft Docs"
description: "Bu öğretici toolearn izleyin nasıl çözüm toodeploy bir Azure IOT paketi önceden yapılandırılmış."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a><span data-ttu-id="f46f1-103">Merhaba önceden yapılandırılmış çözümleri kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="f46f1-103">Get started with hello preconfigured solutions</span></span>

<span data-ttu-id="f46f1-104">Azure IOT paketi [önceden yapılandırılmış çözümleri] [ lnk-preconfigured-solutions] ortak IOT iş senaryolarını uygulayan birden çok Azure IOT Hizmetleri toodeliver uçtan uca çözümler birleştirin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="f46f1-105">Merhaba *Uzaktan izleme* önceden yapılandırılmış çözüm aygıtlarınızı tooand izleyiciler bağlanır.</span><span class="sxs-lookup"><span data-stu-id="f46f1-105">hello *remote monitoring* preconfigured solution connects tooand monitors your devices.</span></span> <span data-ttu-id="f46f1-106">Otomatik olarak veri toothat akışı yanıt işlemleri yaparak hello çözüm tooanalyze hello akış cihazlarınız ve tooimprove işletme sonuçlarını verilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-106">You can use hello solution tooanalyze hello stream of data from your devices and tooimprove business outcomes by making processes respond automatically toothat stream of data.</span></span>

<span data-ttu-id="f46f1-107">Bu öğretici nasıl tooprovision hello çözüm önceden yapılandırılmış Uzaktan izleme gösterir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-107">This tutorial shows you how tooprovision hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="f46f1-108">Bu ayrıca, hello aracılığıyla hello önceden yapılandırılmış çözümün temel özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f46f1-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="f46f1-109">Bu özelliklerin çoğunu hello çözümden erişebilirsiniz *Pano* hello önceden yapılandırılmış çözümün bir parçası dağıtır:</span><span class="sxs-lookup"><span data-stu-id="f46f1-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![Önceden yapılandırılmış uzaktan izleme panosu][img-dashboard]

<span data-ttu-id="f46f1-111">toocomplete Bu öğreticide, bir etkin Azure aboneliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="f46f1-112">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f46f1-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="f46f1-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="f46f1-114">Senaryoya genel bakış</span><span class="sxs-lookup"><span data-stu-id="f46f1-114">Scenario overview</span></span>

<span data-ttu-id="f46f1-115">Merhaba Uzaktan izleme çözümü dağıttığınızda, bunu, toostep yaygın bir uzaktan izleme senaryo aracılığıyla kaynak ile önceden doldurulmaz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-115">When you deploy hello remote monitoring preconfigured solution, it is prepopulated with resources that enable you toostep through a common remote monitoring scenario.</span></span> <span data-ttu-id="f46f1-116">Bu senaryoda, çeşitli aygıtlar bağlı toohello çözümü raporlama beklenmeyen sıcaklık değerleri.</span><span class="sxs-lookup"><span data-stu-id="f46f1-116">In this scenario, several devices connected toohello solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="f46f1-117">Merhaba aşağıdaki bölümlerde, nasıl göstermek için:</span><span class="sxs-lookup"><span data-stu-id="f46f1-117">hello following sections show you how to:</span></span>

* <span data-ttu-id="f46f1-118">Beklenmeyen sıcaklık değerleri gönderme hello aygıtları belirleyin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-118">Identify hello devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="f46f1-119">Bu cihazların yapılandırma toosend daha ayrıntılı telemetri.</span><span class="sxs-lookup"><span data-stu-id="f46f1-119">Configure these devices toosend more detailed telemetry.</span></span>
* <span data-ttu-id="f46f1-120">Bu cihazlarda hello bellenim güncelleştirerek Hello sorunu düzeltin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-120">Fix hello problem by updating hello firmware on these devices.</span></span>
* <span data-ttu-id="f46f1-121">Eyleminizi hello sorunu Çözümlendi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f46f1-121">Verify that your action has resolved hello issue.</span></span>

<span data-ttu-id="f46f1-122">Bir anahtar, bu senaryo bu eylemleri uzaktan hello çözüm panodan için gerçekleştirebilir özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-122">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="f46f1-123">Fiziksel erişim toohello aygıtları gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f46f1-123">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="f46f1-124">Görünüm hello çözüm Panosu</span><span class="sxs-lookup"><span data-stu-id="f46f1-124">View hello solution dashboard</span></span>

<span data-ttu-id="f46f1-125">Merhaba çözüm Panosu toomanage dağıtılan hello çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="f46f1-125">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="f46f1-126">Örneğin, telemetriyi görüntüleyebilir, cihazları ekleyebilir ve kuralları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="f46f1-127">Ne zaman hello Sağlama tamamlandıktan ve önceden yapılandırılmış çözümünüzün kutucuğu hello gösterir **hazır**, seçin **başlatma** tooopen Uzaktan izleme çözümü portalınızı yeni bir sekmede.</span><span class="sxs-lookup"><span data-stu-id="f46f1-127">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Merhaba önceden yapılandırılmış çözüm başlatma][img-launch-solution]

1. <span data-ttu-id="f46f1-129">Varsayılan olarak, hello çözüm portalı hello gösterir *Pano*.</span><span class="sxs-lookup"><span data-stu-id="f46f1-129">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="f46f1-130">Merhaba sol taraftaki hello sayfasının hello menüsünü kullanarak hello çözüm portalı tooother alanlarının gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-130">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Önceden yapılandırılmış uzaktan izleme panosu][img-menu]

<span data-ttu-id="f46f1-132">Başlangıç Panosu aşağıdaki bilgilerle hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="f46f1-132">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="f46f1-133">Her cihaz hello konumunu görüntüler bir harita toohello çözüm bağlı.</span><span class="sxs-lookup"><span data-stu-id="f46f1-133">A map that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="f46f1-134">Merhaba çözümü ilk kez çalıştırdığınızda, 25 sanal cihazlar vardır.</span><span class="sxs-lookup"><span data-stu-id="f46f1-134">When you first run hello solution, there are 25 simulated devices.</span></span> <span data-ttu-id="f46f1-135">Merhaba sanal cihazlar Azure WebJobs olarak uygulanır ve hello çözüm hello haritada hello Bing Haritalar API'si tooplot bilgileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="f46f1-135">hello simulated devices are implemented as Azure WebJobs, and hello solution uses hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="f46f1-136">Merhaba bkz [SSS] [ lnk-faq] toolearn nasıl toomake hello harita dinamik.</span><span class="sxs-lookup"><span data-stu-id="f46f1-136">See hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="f46f1-137">Seçilen yakın gerçek zamanlı cihazdan nem ve sıcaklık telemetrisini çizen ve maksimum, minimum ve ortalama nem gibi toplu verileri görüntüleyen bir **Telemetri Geçmişi** paneli.</span><span class="sxs-lookup"><span data-stu-id="f46f1-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="f46f1-138">Bir telemetri değeri bir eşiği aştığında yeni uyarı etkinliklerini gösteren bir **Uyarı Geçmişi** paneli.</span><span class="sxs-lookup"><span data-stu-id="f46f1-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="f46f1-139">Merhaba önceden yapılandırılmış çözümü tarafından oluşturulan ek toohello örneklerde kendi alarmlarınızı tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-139">You can define your own alarms in addition toohello examples created by hello preconfigured solution.</span></span>
* <span data-ttu-id="f46f1-140">Zamanlanmış işler hakkında bilgiler gösteren bir **İşler** paneli.</span><span class="sxs-lookup"><span data-stu-id="f46f1-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="f46f1-141">**Yönetim işleri** sayfasından kendi işlerinizi zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="f46f1-142">Uyarıları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f46f1-142">View alarms</span></span>

<span data-ttu-id="f46f1-143">Merhaba alarm geçmişi paneli beş cihaza beklenen telemetri değerleri daha yüksek raporlama gösterir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-143">hello alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![Merhaba çözüm Panosu Yapılacaklar Alarm geçmişi][img-alarms]

> [!NOTE]
> <span data-ttu-id="f46f1-145">Bu uyarılar hello önceden yapılandırılmış çözümde bulunan bir kural tarafından üretilir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-145">These alarms are generated by a rule that is included in hello preconfigured solution.</span></span> <span data-ttu-id="f46f1-146">Bir aygıt tarafından gönderilen hello sıcaklık değeri 60 aşarsa bu kural bir uyarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f46f1-146">This rule generates an alert when hello temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="f46f1-147">Seçerek kendi kurallar ve eylemler tanımlayabilirsiniz [kuralları](#add-a-rule) ve [Eylemler](#add-an-action) hello sol menüde.</span><span class="sxs-lookup"><span data-stu-id="f46f1-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in hello left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="f46f1-148">Cihazları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f46f1-148">View devices</span></span>

<span data-ttu-id="f46f1-149">Merhaba *aygıtları* listesi hello çözümde tüm kayıtlı hello cihazları gösterir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-149">hello *devices* list shows all hello registered devices in hello solution.</span></span> <span data-ttu-id="f46f1-150">Görüntüleyebilir ve cihaz meta verilerini düzenleme hello aygıt listesinde, eklemek veya cihazları kaldırın ve cihazlarda yöntemleri çağırma.</span><span class="sxs-lookup"><span data-stu-id="f46f1-150">From hello device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="f46f1-151">Filtrelemek ve sıralamak hello aygıt listesinde cihazların Merhaba listesi.</span><span class="sxs-lookup"><span data-stu-id="f46f1-151">You can filter and sort hello list of devices in hello device list.</span></span> <span data-ttu-id="f46f1-152">Merhaba aygıt listesinde gösterilen hello sütunlar özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-152">You can also customize hello columns shown in hello device list.</span></span>

1. <span data-ttu-id="f46f1-153">Seçin **aygıtları** Bu çözüm için tooshow hello cihaz listesi.</span><span class="sxs-lookup"><span data-stu-id="f46f1-153">Choose **Devices** tooshow hello device list for this solution.</span></span>

   ![Görünüm hello aygıt hello çözüm portalı listesinde][img-devicelist]

1. <span data-ttu-id="f46f1-155">Merhaba cihaz listesi, başlangıçta hello sağlama işlemi tarafından oluşturulan 25 sanal cihazlar gösterir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-155">hello device list initially shows 25 simulated devices created by hello provisioning process.</span></span> <span data-ttu-id="f46f1-156">Ek sanal ve fiziksel cihaz toohello çözüm ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-156">You can add additional simulated and physical devices toohello solution.</span></span>

1. <span data-ttu-id="f46f1-157">bir aygıt tooview hello ayrıntılarını hello aygıt listesinde bir cihaz seçin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-157">tooview hello details of a device, choose a device in hello device list.</span></span>

   ![Hello çözüm portalında Hello cihaz ayrıntıları görüntüleyin][img-devicedetails]

<span data-ttu-id="f46f1-159">Merhaba **cihaz ayrıntıları** Masası altı bölümleri içerir:</span><span class="sxs-lookup"><span data-stu-id="f46f1-159">hello **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="f46f1-160">Toocustomize hello aygıt simgesini etkinleştirmek, hello aygıtı devre dışı bırakmak, bir kural eklemek, bir yöntemi çağırma veya bir komut gönderme bağlantıları koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="f46f1-160">A collection of links that enable you toocustomize hello device icon, disable hello device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="f46f1-161">Komutlar (cihazdan buluta iletiler) ile yöntemlerin (doğrudan yöntemler) bir karşılaştırması için bkz. [Buluttan cihaza iletişim kılavuzu][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="f46f1-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="f46f1-162">Merhaba **cihaz çifti - etiketleri** bölüm hello aygıt tooedit etiket değerlerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="f46f1-162">hello **Device Twin - Tags** section enables you tooedit tag values for hello device.</span></span> <span data-ttu-id="f46f1-163">Etiket değerleri hello aygıt listesinde görüntülemek ve etiket değerleri toofilter hello aygıt listesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f46f1-163">You can display tag values in hello device list and use tag values toofilter hello device list.</span></span>
* <span data-ttu-id="f46f1-164">Merhaba **cihaz çifti - istenen özellikleri** bölüm tooset özellik değerlerini gönderilen toobe toohello aygıt sağlar.</span><span class="sxs-lookup"><span data-stu-id="f46f1-164">hello **Device Twin - Desired Properties** section enables you tooset property values toobe sent toohello device.</span></span>
* <span data-ttu-id="f46f1-165">Merhaba **cihaz çifti - bildirilen özellikleri** bölüm hello aygıtından gönderilen özellik değerlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-165">hello **Device Twin - Reported Properties** section shows property values sent from hello device.</span></span>
* <span data-ttu-id="f46f1-166">Merhaba **cihaz özellikleri** bölüm kimliği ve kimlik doğrulama anahtarlarının hello kimlik kayıt defteri hello cihazı gibi bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-166">hello **Device Properties** section shows information from hello identity registry such as hello device id and authentication keys.</span></span>
* <span data-ttu-id="f46f1-167">Merhaba **en son işlerin** bölüm bu cihazı kısa bir süre önce hedeflenen herhangi bir işi hakkında bilgileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-167">hello **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-hello-device-list"></a><span data-ttu-id="f46f1-168">Filtre hello cihaz listesi</span><span class="sxs-lookup"><span data-stu-id="f46f1-168">Filter hello device list</span></span>

<span data-ttu-id="f46f1-169">Bir filtre toodisplay beklenmeyen sıcaklık değerleri gönderen cihazları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-169">You can use a filter toodisplay only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="f46f1-170">Uzaktan izleme çözümü Hello içerir hello **sağlıksız aygıtları** 60'dan büyük bir ortalama sıcaklık değer tooshow aygıtlarla filtre.</span><span class="sxs-lookup"><span data-stu-id="f46f1-170">hello remote monitoring preconfigured solution includes hello **Unhealthy devices** filter tooshow devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="f46f1-171">Ayrıca [kendi filtrelerinizi oluşturabilirsiniz](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="f46f1-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="f46f1-172">Seçin **kaydedilmiş filtre Aç** toodisplay kullanılabilir filtrelerin listesi.</span><span class="sxs-lookup"><span data-stu-id="f46f1-172">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="f46f1-173">Ardından **sağlıksız aygıtları** tooapply hello Filtresi:</span><span class="sxs-lookup"><span data-stu-id="f46f1-173">Then choose **Unhealthy devices** tooapply hello filter:</span></span>

    ![Filtreler hello listesini görüntüle][img-unhealthy-filter]

1. <span data-ttu-id="f46f1-175">Merhaba cihaz listesi yalnızca ortalama sıcaklık değeri ile cihazları şimdi 60'dan büyük gösterir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-175">hello device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![Sağlıksız aygıtları gösteren hello filtrelenmiş aygıt listesini görüntüle][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="f46f1-177">İstenen özellikleri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f46f1-177">Update desired properties</span></span>

<span data-ttu-id="f46f1-178">Düzeltilmesi gerekebilen bir cihaz kümesi belirlediniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="f46f1-179">Ancak, hello veri sıklığı 15 saniye düz bir hello sorunu tanılama için yeterli değil karar verin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-179">However, you decide that hello data frequency of 15 seconds is not sufficient for a clear diagnosis of hello issue.</span></span> <span data-ttu-id="f46f1-180">Daha fazla veri noktaları toobetter sizinle hello sorunu tanılamak Hello telemetri sıklığı toofive saniye tooprovide değiştirme.</span><span class="sxs-lookup"><span data-stu-id="f46f1-180">Changing hello telemetry frequency toofive seconds tooprovide you with more data points toobetter diagnose hello issue.</span></span> <span data-ttu-id="f46f1-181">Bu yapılandırma değişikliği tooyour uzak aygıtlar hello çözüm Portalı'ndan gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-181">You can push this configuration change tooyour remote devices from hello solution portal.</span></span> <span data-ttu-id="f46f1-182">Bir kez hello etkiyi değerlendirmek ve hello sonuçlarına hareket hello değişiklik yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-182">You can make hello change once, evaluate hello impact, and then act on hello results.</span></span>

<span data-ttu-id="f46f1-183">Bu adımları toorun hello değiştiren bir iş izleyin **TelemetryInterval** özelliği hello etkilenen cihazlar için istenen.</span><span class="sxs-lookup"><span data-stu-id="f46f1-183">Follow these steps toorun a job that changes hello **TelemetryInterval** desired property for hello affected devices.</span></span> <span data-ttu-id="f46f1-184">Merhaba cihazların Merhaba yeni aldığınızda **TelemetryInterval** özellik değeri, bunlar değişiklik her beş saniyede 15 dakikada yerine kendi yapılandırma toosend telemetri:</span><span class="sxs-lookup"><span data-stu-id="f46f1-184">When hello devices receive hello new **TelemetryInterval** property value, they change their configuration toosend telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="f46f1-185">Merhaba aygıt listesinde sağlıksız cihazların Merhaba listesini gösteren sırada seçin **İş Zamanlayıcısı**, ardından **Düzenle cihaz çifti**.</span><span class="sxs-lookup"><span data-stu-id="f46f1-185">While you are showing hello list of unhealthy devices in hello device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="f46f1-186">Merhaba iş çağrısı **değiştirme telemetri aralığı**.</span><span class="sxs-lookup"><span data-stu-id="f46f1-186">Call hello job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="f46f1-187">Merhaba hello değerini değiştirin **istenen özelliği** adı **istenen. Config.TelemetryInterval** toofive saniye.</span><span class="sxs-lookup"><span data-stu-id="f46f1-187">Change hello value of hello **Desired Property** name **desired.Config.TelemetryInterval** toofive seconds.</span></span>

1. <span data-ttu-id="f46f1-188">**Zamanlama**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-188">Choose **Schedule**.</span></span>

    ![Merhaba TelemetryInterval özelliği toofive saniye değiştirme][img-change-interval]

1. <span data-ttu-id="f46f1-190">Merhaba hello işinde hello ilerlemesini izleyebilirsiniz **Yönetim işleri** hello portalında sayfası.</span><span class="sxs-lookup"><span data-stu-id="f46f1-190">You can monitor hello progress of hello job on hello **Management Jobs** page in hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="f46f1-191">Toochange istenen özellik değeri için tek bir cihaza istiyorsanız, hello kullanın **istenen özellikleri** hello bölümünde **cihaz ayrıntıları** bir iş çalıştırmak yerine paneli.</span><span class="sxs-lookup"><span data-stu-id="f46f1-191">If you want toochange a desired property value for an individual device, use hello **Desired Properties** section in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="f46f1-192">Bu iş hello hello değerini ayarlar **TelemetryInterval** tüm aygıtları hello Filtresi tarafından seçilen hello için hello cihaz çifti özelliğinde istenen.</span><span class="sxs-lookup"><span data-stu-id="f46f1-192">This job sets hello value of hello **TelemetryInterval** desired property in hello device twin for all hello devices selected by hello filter.</span></span> <span data-ttu-id="f46f1-193">Merhaba aygıtları hello cihaz çifti bu değerini almak ve davranışlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-193">hello devices retrieve this value from hello device twin and update their behavior.</span></span> <span data-ttu-id="f46f1-194">Bir aygıt alır ve bir cihaz çifti istenen özelliğinden işler hello karşılık gelen bildirilen değer özelliğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f46f1-194">When a device retrieves and processes a desired property from a device twin, it sets hello corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="f46f1-195">Çağırma yöntemleri</span><span class="sxs-lookup"><span data-stu-id="f46f1-195">Invoke methods</span></span>

<span data-ttu-id="f46f1-196">Merhaba iş çalışırken, hello sağlıksız aygıtlar listesinde tüm bu cihazların eski (küçüktür sürüm 1. 6) bellenim olduğunu fark sürümleri.</span><span class="sxs-lookup"><span data-stu-id="f46f1-196">While hello job runs, you notice in hello list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![Üretici yazılımı sürümüne hello sağlıksız cihazlar için Görünüm hello bildirdi][img-old-firmware]

<span data-ttu-id="f46f1-198">Bu üretici yazılımı sürümüne hello beklenmeyen hello kök nedeni olabilir sıcaklık değerleri sağlıklı diğer cihazları yeni güncelleştirilen tooversion 2.0 olduğunu bildiğiniz için.</span><span class="sxs-lookup"><span data-stu-id="f46f1-198">This firmware version may be hello root cause of hello unexpected temperature values because you know that other healthy devices were recently updated tooversion 2.0.</span></span> <span data-ttu-id="f46f1-199">Merhaba yerleşik kullanabilirsiniz **eski bellenim aygıtları** tooidentify eski bellenim sürümleri aygıtlarla filtre.</span><span class="sxs-lookup"><span data-stu-id="f46f1-199">You can use hello built-in **Old firmware devices** filter tooidentify any devices with old firmware versions.</span></span> <span data-ttu-id="f46f1-200">Merhaba Portalı'ndan sonra uzaktan hala eski bellenim sürümleri çalıştıran tüm hello cihazlar güncelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f46f1-200">From hello portal, you can then remotely update all hello devices still running old firmware versions:</span></span>

1. <span data-ttu-id="f46f1-201">Seçin **kaydedilmiş filtre Aç** toodisplay kullanılabilir filtrelerin listesi.</span><span class="sxs-lookup"><span data-stu-id="f46f1-201">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="f46f1-202">Ardından **eski bellenim aygıtları** tooapply hello Filtresi:</span><span class="sxs-lookup"><span data-stu-id="f46f1-202">Then choose **Old firmware devices** tooapply hello filter:</span></span>

    ![Filtreler hello listesini görüntüle][img-old-filter]

1. <span data-ttu-id="f46f1-204">Merhaba cihaz listesi şimdi yalnızca eski bellenim sürümleri ile cihazları gösterir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-204">hello device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="f46f1-205">Bu liste hello tarafından tanımlanan hello beş aygıtları içerir **sağlıksız aygıtları** filtre ve üç ek aygıtları:</span><span class="sxs-lookup"><span data-stu-id="f46f1-205">This list includes hello five devices identified by hello **Unhealthy devices** filter and three additional devices:</span></span>

    ![Eski aygıtları gösteren hello filtrelenmiş aygıt listesini görüntüle][img-filtered-old-list]

1. <span data-ttu-id="f46f1-207">**İş Zamanlayıcı**’yı ve ardından **Invoke Yöntemi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="f46f1-208">Ayarlama **iş adı** çok**bellenim güncelleştirme tooversion 2.0**.</span><span class="sxs-lookup"><span data-stu-id="f46f1-208">Set **Job Name** too**Firmware update tooversion 2.0**.</span></span>

1. <span data-ttu-id="f46f1-209">Seçin **InitiateFirmwareUpdate** hello olarak **yöntemi**.</span><span class="sxs-lookup"><span data-stu-id="f46f1-209">Choose **InitiateFirmwareUpdate** as hello **Method**.</span></span>

1. <span data-ttu-id="f46f1-210">Set hello **FwPackageUri** parametresi çok**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="f46f1-210">Set hello **FwPackageUri** parameter too**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="f46f1-211">**Zamanlama**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-211">Choose **Schedule**.</span></span> <span data-ttu-id="f46f1-212">Merhaba varsayılan hello iş toorun için sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="f46f1-212">hello default is for hello job toorun now.</span></span>

    ![İş tooupdate hello bellenim seçili hello aygıtların oluşturma][img-method-update]

> [!NOTE]
> <span data-ttu-id="f46f1-214">Tek bir cihaza bir yöntem tooinvoke istiyorsanız, tercih **yöntemleri** hello içinde **cihaz ayrıntıları** bir iş çalıştırmak yerine paneli.</span><span class="sxs-lookup"><span data-stu-id="f46f1-214">If you want tooinvoke a method on an individual device, choose **Methods** in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="f46f1-215">Bu iş hello çağırır **InitiateFirmwareUpdate** hello Filtresi tarafından seçilen tüm hello cihazlarda yöntemi doğrudan.</span><span class="sxs-lookup"><span data-stu-id="f46f1-215">This job invokes hello **InitiateFirmwareUpdate** direct method on all hello devices selected by hello filter.</span></span> <span data-ttu-id="f46f1-216">Aygıtları hemen tooIoT Hub yanıt ve hello bellenim güncelleştirme işlemini zaman uyumsuz olarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="f46f1-216">Devices respond immediately tooIoT Hub and then initiate hello firmware update process asynchronously.</span></span> <span data-ttu-id="f46f1-217">Merhaba aygıtlar hello ekran görüntüleri aşağıdaki gösterildiği gibi hello bellenim güncelleştirme işlemini bildirilen özellik değerleri ile ilgili durum bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="f46f1-217">hello devices provide status information about hello firmware update process through reported property values, as shown in hello following screenshots.</span></span> <span data-ttu-id="f46f1-218">Merhaba seçin **yenileme** hello cihaz ve iş listelerindeki simgesi tooupdate hello bilgileri:</span><span class="sxs-lookup"><span data-stu-id="f46f1-218">Choose hello **Refresh** icon tooupdate hello information in hello device and job lists:</span></span>

<span data-ttu-id="f46f1-219">![Merhaba bellenim güncelleştirme listesi çalışan gösteren iş listesi][img-update-1]
![bellenim güncelleştirme durumunu gösteren cihaz listesi][img-update-2]
![iş listesini gösteren hello bellenim güncelleştirme listesi tamamlandı][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="f46f1-219">![Job list showing hello firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing hello firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="f46f1-220">Bir üretim ortamında, belirlenen bakım penceresi sırasında işleri toorun zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-220">In a production environment, you can schedule jobs toorun during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="f46f1-221">Senaryo gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="f46f1-221">Scenario review</span></span>

<span data-ttu-id="f46f1-222">Bu senaryoda, bazı hello alarm geçmişi hello Pano ve bir filtre kullanarak uzak aygıtlarınız ile olası bir sorunu tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="f46f1-222">In this scenario, you identified a potential issue with some of your remote devices using hello alarm history on hello dashboard and a filter.</span></span> <span data-ttu-id="f46f1-223">Ardından kullanılan hello filtre ve iş tooremotely hello aygıtları tooprovide yapılandırmak daha fazla bilgi toohelp hello sorunu tanılamak.</span><span class="sxs-lookup"><span data-stu-id="f46f1-223">You then used hello filter and a job tooremotely configure hello devices tooprovide more information toohelp diagnose hello issue.</span></span> <span data-ttu-id="f46f1-224">Son olarak, bir filtre ve iş tooschedule bakım etkilenen hello cihazlarda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f46f1-224">Finally, you used a filter and a job tooschedule maintenance on hello affected devices.</span></span> <span data-ttu-id="f46f1-225">Toohello Pano döndürmesi durumunda olduğunu artık çözümünüzdeki aygıtlardan gelen uyarılar kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-225">If you return toohello dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="f46f1-226">Bir filtre kullanabilirsiniz bellenim hello tooverify çözümünüzdeki tüm hello cihazlarda güncel olduğunu ve artık uygun olmayan cihazlar:</span><span class="sxs-lookup"><span data-stu-id="f46f1-226">You can use a filter tooverify that hello firmware is up-to-date on all hello devices in your solution and that there are no more unhealthy devices:</span></span>

![Tüm cihazlarda güncel üretici yazılımı olduğunu gösteren filtre][img-updated]

![Tüm cihazların sistem durumunun iyi olduğunu gösteren filtre][img-healthy]

## <a name="other-features"></a><span data-ttu-id="f46f1-229">Diğer özellikler</span><span class="sxs-lookup"><span data-stu-id="f46f1-229">Other features</span></span>

<span data-ttu-id="f46f1-230">Merhaba aşağıdaki bölümlerde hello önceki senaryoda bir parçası olarak açıklanmamaktadır, bazı ek hello Uzaktan izleme çözümü özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="f46f1-230">hello following sections describe some additional features of hello remote monitoring preconfigured solution that are not described as part of hello previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="f46f1-231">Sütunları özelleştirme</span><span class="sxs-lookup"><span data-stu-id="f46f1-231">Customize columns</span></span>

<span data-ttu-id="f46f1-232">Merhaba aygıt listesinde seçerek gösterilen hello bilgileri özelleştirebilirsiniz **sütun düzenleyicisini**.</span><span class="sxs-lookup"><span data-stu-id="f46f1-232">You can customize hello information shown in hello device list by choosing **Column editor**.</span></span> <span data-ttu-id="f46f1-233">Bildirilen özellik ve etiket değerlerini gösteren sütunlar ekleyip kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="f46f1-234">Ayrıca, sütunları yeniden sıralayabilir ve yeniden adlandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f46f1-234">You can also reorder and rename columns:</span></span>

   ![Sütun Düzenleyicisi nleri hello cihaz listesi][img-columneditor]

### <a name="customize-hello-device-icon"></a><span data-ttu-id="f46f1-236">Merhaba aygıtı simgesi özelleştirme</span><span class="sxs-lookup"><span data-stu-id="f46f1-236">Customize hello device icon</span></span>

<span data-ttu-id="f46f1-237">Merhaba hello aygıt listesinden görüntülenen hello aygıtı simgesi özelleştirebilirsiniz **cihaz ayrıntıları** gibi panel:</span><span class="sxs-lookup"><span data-stu-id="f46f1-237">You can customize hello device icon displayed in hello device list from hello **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="f46f1-238">Merhaba Kurşun Kalem simgesini tooopen hello seçin **görüntü Düzenle** paneli bir aygıt için:</span><span class="sxs-lookup"><span data-stu-id="f46f1-238">Choose hello pencil icon tooopen hello **Edit image** panel for a device:</span></span>

   ![Cihaz görüntüsü düzenleyicisini açma][img-startimageedit]

1. <span data-ttu-id="f46f1-240">Ya da yeni bir resim yükleyin veya hello mevcut görüntülerden birini kullanın ve ardından **kaydetmek**:</span><span class="sxs-lookup"><span data-stu-id="f46f1-240">Either upload a new image or use one of hello existing images and then choose **Save**:</span></span>

   ![Cihaz görüntüsü düzenleyicisini düzenleme][img-imageedit]

1. <span data-ttu-id="f46f1-242">Merhaba şimdi seçtiğiniz görüntüsü görüntüler hello **simgesi** hello cihaz için sütun.</span><span class="sxs-lookup"><span data-stu-id="f46f1-242">hello image you selected now displays in hello **Icon** column for hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="f46f1-243">Merhaba görüntü blob depolama alanına depolanır.</span><span class="sxs-lookup"><span data-stu-id="f46f1-243">hello image is stored in blob storage.</span></span> <span data-ttu-id="f46f1-244">Merhaba cihaz çifti etiketinde blob depolama bir bağlantı toohello görüntüsü içerir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-244">A tag in hello device twin contains a link toohello image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="f46f1-245">Cihaz ekleme</span><span class="sxs-lookup"><span data-stu-id="f46f1-245">Add a device</span></span>

<span data-ttu-id="f46f1-246">Merhaba önceden yapılandırılmış çözümü dağıttığınızda, otomatik olarak hello aygıt listesinde görebilirsiniz 25 örnek cihazları hazırlama.</span><span class="sxs-lookup"><span data-stu-id="f46f1-246">When you deploy hello preconfigured solution, you automatically provision 25 sample devices that you can see in hello device list.</span></span> <span data-ttu-id="f46f1-247">Bu cihazlar bir Azure WebJob içinde çalışan *sanal cihazlardır*.</span><span class="sxs-lookup"><span data-stu-id="f46f1-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="f46f1-248">Sanal cihazlar sizin için tooexperiment hello gerek toodeploy gerçek fiziksel aygıtları olmadan hello önceden yapılandırılmış Çözümle kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="f46f1-248">Simulated devices make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical devices.</span></span> <span data-ttu-id="f46f1-249">Merhaba tooconnect gerçek cihaz toohello çözümü istiyorsanız bkz [Uzaktan izleme çözümü, aygıt toohello bağlanmak] [ lnk-connect-rm] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="f46f1-249">If you do want tooconnect a real device toohello solution, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="f46f1-250">Merhaba aşağıdaki adımlarda size yol gösterecektir tooadd bir sanal cihaz toohello çözüm:</span><span class="sxs-lookup"><span data-stu-id="f46f1-250">hello following steps show you how tooadd a simulated device toohello solution:</span></span>

1. <span data-ttu-id="f46f1-251">Geri toohello cihaz listesine gidin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-251">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="f46f1-252">tooadd bir cihaz seçin **+ Add A Device** sol alt köşede, hello.</span><span class="sxs-lookup"><span data-stu-id="f46f1-252">tooadd a device, choose **+ Add A Device** in hello bottom left corner.</span></span>

   ![Bir aygıt toohello önceden yapılandırılmış Çözüm Ekle][img-adddevice]

1. <span data-ttu-id="f46f1-254">Seçin **yeni Ekle** hello üzerinde **benzetimli aygıt** döşeme.</span><span class="sxs-lookup"><span data-stu-id="f46f1-254">Choose **Add New** on hello **Simulated Device** tile.</span></span>

   ![Panoda yeni cihaz ayrıntılarını ayarlama][img-addnew]

   <span data-ttu-id="f46f1-256">Toocreate seçerseniz ek toocreating yeni bir sanal cihaz, ayrıca bir fiziksel cihaz ekleyebilirsiniz bir **özel cihaz**.</span><span class="sxs-lookup"><span data-stu-id="f46f1-256">In addition toocreating a new simulated device, you can also add a physical device if you choose toocreate a **Custom Device**.</span></span> <span data-ttu-id="f46f1-257">fiziksel aygıtların toohello çözümünü bağlama hakkında daha fazla toolearn bkz [, aygıt toohello IOT paketi Uzaktan izleme çözümü bağlanmak][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="f46f1-257">toolearn more about connecting physical devices toohello solution, see [Connect your device toohello IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="f46f1-258">**Kendi Cihaz Kimliğimi tanımlamama izin ver**'i seçin ve **mydevice_01** gibi benzersiz bir cihaz kimliği girin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="f46f1-259">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-259">Choose **Create**.</span></span>

   ![Yeni bir cihaz kaydetme][img-definedevice]

1. <span data-ttu-id="f46f1-261">3. adımında **bir sanal cihaz ekleme**, seçin **Bitti** tooreturn toohello aygıt listesinde.</span><span class="sxs-lookup"><span data-stu-id="f46f1-261">In step 3 of **Add a simulated device**, choose **Done** tooreturn toohello device list.</span></span>

1. <span data-ttu-id="f46f1-262">Cihazınızı görüntüleyebilirsiniz **çalıştıran** hello aygıt listesinde.</span><span class="sxs-lookup"><span data-stu-id="f46f1-262">You can view your device **Running** in hello device list.</span></span>

    ![Cihaz listesinde yeni cihazı görüntüleme][img-runningnew]

1. <span data-ttu-id="f46f1-264">Ayrıca görüntüleyebilirsiniz hello benzetimli hello Panodaki yeni cihazınızdan telemetri:</span><span class="sxs-lookup"><span data-stu-id="f46f1-264">You can also view hello simulated telemetry from your new device on hello dashboard:</span></span>

    ![Yeni cihazdan telemetri görüntüleme][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="f46f1-266">Bir cihazı devre dışı bırakma ve silme</span><span class="sxs-lookup"><span data-stu-id="f46f1-266">Disable and delete a device</span></span>

<span data-ttu-id="f46f1-267">Bir Cihazı devre dışı bırakabilir, devre dışı kaldıktan sonra da kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f46f1-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Bir cihazı devre dışı bırakma ve kaldırma][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="f46f1-269">Kural ekleme</span><span class="sxs-lookup"><span data-stu-id="f46f1-269">Add a rule</span></span>

<span data-ttu-id="f46f1-270">Yeni eklediğiniz hello yeni cihaz için hiçbir kural vardır.</span><span class="sxs-lookup"><span data-stu-id="f46f1-270">There are no rules for hello new device you just added.</span></span> <span data-ttu-id="f46f1-271">Bu bölümde, hello sıcaklık 47 dereceyi aygıt aşıyor hello yeni raporlanan bir uyarıyı tetikleyen bir kural ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-271">In this section, you add a rule that triggers an alarm when hello temperature reported by hello new device exceeds 47 degrees.</span></span> <span data-ttu-id="f46f1-272">Başlamadan önce hello hello hello Panoda yeni cihaz için telemetri geçmişinin hello cihaz sıcaklığının hiçbir zaman 45 dereceyi aşmadığını gösterdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-272">Before you start, notice that hello telemetry history for hello new device on hello dashboard shows hello device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="f46f1-273">Geri toohello cihaz listesine gidin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-273">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="f46f1-274">tooadd hello aygıtı için bir kural hello yeni Cihazınızı seçin **cihazlar listesi**ve ardından **Ekle kuralı**.</span><span class="sxs-lookup"><span data-stu-id="f46f1-274">tooadd a rule for hello device, select your new device in hello **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="f46f1-275">Kullanan bir kural oluşturmak **sıcaklık** hello veri alanı olarak **AlarmTemp** hello hello sıcaklık 47 dereceyi aştığında çıktı olarak:</span><span class="sxs-lookup"><span data-stu-id="f46f1-275">Create a rule that uses **Temperature** as hello data field and uses **AlarmTemp** as hello output when hello temperature exceeds 47 degrees:</span></span>

    ![Cihaz kuralı ekleme][img-adddevicerule]

1. <span data-ttu-id="f46f1-277">yaptığınız değişiklikleri toosave seçin **kuralları Kaydet ve görüntüle**.</span><span class="sxs-lookup"><span data-stu-id="f46f1-277">toosave your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="f46f1-278">Seçin **komutları** hello cihaz ayrıntıları bölmesinde hello yeni cihaz için.</span><span class="sxs-lookup"><span data-stu-id="f46f1-278">Choose **Commands** in hello device details pane for hello new device.</span></span>

    ![Cihaz kuralı ekleme][img-adddevicerule2]

1. <span data-ttu-id="f46f1-280">Seçin **ChangeSetPointTemp** hello komut listesi ve kümesi **SetPointTemp** too45.</span><span class="sxs-lookup"><span data-stu-id="f46f1-280">Select **ChangeSetPointTemp** from hello command list and set **SetPointTemp** too45.</span></span> <span data-ttu-id="f46f1-281">Ardından **Komut Gönder**’i seçin:</span><span class="sxs-lookup"><span data-stu-id="f46f1-281">Then choose **Send Command**:</span></span>

    ![Cihaz kuralı ekleme][img-adddevicerule3]

1. <span data-ttu-id="f46f1-283">Geri toohello Pano gidin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-283">Navigate back toohello dashboard.</span></span> <span data-ttu-id="f46f1-284">Kısa bir süre sonra hello yeni bir giriş görürsünüz **Alarm geçmişi** hello sıcaklık yeni cihazınız tarafından raporlanan bölmesinde hello 47 derece eşiğini aşıyor:</span><span class="sxs-lookup"><span data-stu-id="f46f1-284">After a short time, you will see a new entry in hello **Alarm History** pane when hello temperature reported by your new device exceeds hello 47-degree threshold:</span></span>

    ![Cihaz kuralı ekleme][img-adddevicerule4]

1. <span data-ttu-id="f46f1-286">Gözden geçirin ve tüm kurallarınızı hello düzenleyin **kuralları** hello Pano sayfası:</span><span class="sxs-lookup"><span data-stu-id="f46f1-286">You can review and edit all your rules on hello **Rules** page of hello dashboard:</span></span>

    ![Cihaz kurallarını listeleme][img-rules]

1. <span data-ttu-id="f46f1-288">Gözden geçirin ve yanıt tooa kuralında hello üzerinde gerçekleştirilecek tüm hello Eylemler Düzenle **Eylemler** hello Pano sayfası:</span><span class="sxs-lookup"><span data-stu-id="f46f1-288">You can review and edit all hello actions that can be taken in response tooa rule on hello **Actions** page of hello dashboard:</span></span>

    ![Cihaz eylemlerini listeleme][img-actions]

> [!NOTE]
> <span data-ttu-id="f46f1-290">Bir e-posta iletisi gönderebilirsiniz olası toodefine Eylemler olduğu veya yanıt tooa SMS kuralı veya bir satır iş kolu sistemiyle tümleştirme bir [mantıksal uygulama][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="f46f1-290">It is possible toodefine actions that can send an email message or SMS in response tooa rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="f46f1-291">Daha fazla bilgi için bkz: Merhaba [bağlanmak mantıksal uygulama tooyour Azure IOT paketi Uzaktan izleme çözümü önceden yapılandırılmış][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="f46f1-291">For more information, see hello [Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="f46f1-292">Filtreleri yönetme</span><span class="sxs-lookup"><span data-stu-id="f46f1-292">Manage filters</span></span>

<span data-ttu-id="f46f1-293">Merhaba aygıt listesinde, oluşturmak, kaydedin ve filtreler toodisplay aygıtları bağlı tooyour hub özelleştirilmiş listesini yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-293">In hello device list, you can create, save, and reload filters toodisplay a customized list of devices connected tooyour hub.</span></span> <span data-ttu-id="f46f1-294">bir filtre toocreate:</span><span class="sxs-lookup"><span data-stu-id="f46f1-294">toocreate a filter:</span></span>

1. <span data-ttu-id="f46f1-295">Cihazların Merhaba listesi yukarıda Hello Düzenle filtre simgesini seçin:</span><span class="sxs-lookup"><span data-stu-id="f46f1-295">Choose hello edit filter icon above hello list of devices:</span></span>

    ![Açık hello filtre Düzenleyicisi][img-editfiltericon]

1. <span data-ttu-id="f46f1-297">Merhaba, **filtre Düzenleyicisi**, hello alanları, işleçler ve değerler toofilter hello cihaz listesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-297">In hello **Filter editor**, add hello fields, operators, and values toofilter hello device list.</span></span> <span data-ttu-id="f46f1-298">Filtre birden çok yan tümceleri toorefine ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-298">You can add multiple clauses toorefine your filter.</span></span> <span data-ttu-id="f46f1-299">Seçin **filtre** tooapply hello Filtresi:</span><span class="sxs-lookup"><span data-stu-id="f46f1-299">Choose **Filter** tooapply hello filter:</span></span>

    ![Filtre oluşturma][img-filtereditor]

1. <span data-ttu-id="f46f1-301">Bu örnekte, üretici ve model numarası tarafından hello listesi filtrelenir:</span><span class="sxs-lookup"><span data-stu-id="f46f1-301">In this example, hello list is filtered by manufacturer and model number:</span></span>

    ![Filtrelenmiş liste][img-filterelist]

1. <span data-ttu-id="f46f1-303">toosave filtre ile özel bir ad seçin hello **Farklı Kaydet** simgesi:</span><span class="sxs-lookup"><span data-stu-id="f46f1-303">toosave your filter with a custom name, choose hello **Save as** icon:</span></span>

    ![Filtre kaydetme][img-savefilter]

1. <span data-ttu-id="f46f1-305">tooreapply daha önce kaydedilmiş bir filtre seçin hello **kaydedilmiş filtre Aç** simgesi:</span><span class="sxs-lookup"><span data-stu-id="f46f1-305">tooreapply a filter you saved previously, choose hello **Open saved filter** icon:</span></span>

    ![Filtre açma][img-openfilter]

<span data-ttu-id="f46f1-307">Cihaz kimliği, cihaz durumu, istenen özellikler, bildirilen özellikler ve etiketlere göre filtreler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="f46f1-308">Kendi özel etiketler tooa aygıt hello eklemek **etiketleri** hello bölümünü **cihaz ayrıntıları** panel ya da bir iş tooupdate etiketleri birden fazla cihazda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f46f1-308">You add your own custom tags tooa device in hello **Tags** section of hello **Device Details** panel, or run a job tooupdate tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="f46f1-309">Merhaba, **filtre Düzenleyicisi**, hello kullanabilirsiniz **Gelişmiş görünümü** tooedit hello sorgu metni doğrudan.</span><span class="sxs-lookup"><span data-stu-id="f46f1-309">In hello **Filter editor**, you can use hello **Advanced view** tooedit hello query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="f46f1-310">Komutlar</span><span class="sxs-lookup"><span data-stu-id="f46f1-310">Commands</span></span>

<span data-ttu-id="f46f1-311">Merhaba gelen **cihaz ayrıntıları** paneli, komutları toohello aygıt gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-311">From hello **Device Details** panel, you can send commands toohello device.</span></span> <span data-ttu-id="f46f1-312">Bir cihaz ilk kez başlatıldığında toohello çözümünü destekler hello hakkında bilgi komutlar gönderir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-312">When a device first starts, it sends information about hello commands it supports toohello solution.</span></span> <span data-ttu-id="f46f1-313">Komutlar ve yöntemleri arasındaki farklar hello tartışma için bkz [Azure IOT Hub bulut aygıt seçenekleri][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="f46f1-313">For a discussion of hello differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="f46f1-314">Seçin **komutları** hello içinde **cihaz ayrıntıları** Masası hello seçili cihaz için:</span><span class="sxs-lookup"><span data-stu-id="f46f1-314">Choose **Commands** in hello **Device Details** panel for hello selected device:</span></span>

   ![Panoda cihaz komutları][img-devicecommands]

1. <span data-ttu-id="f46f1-316">Seçin **PingDevice** hello komutu listeden.</span><span class="sxs-lookup"><span data-stu-id="f46f1-316">Select **PingDevice** from hello command list.</span></span>

1. <span data-ttu-id="f46f1-317">**Komut Gönder**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="f46f1-318">Merhaba komutu hello komut geçmişinde hello durumunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-318">You can see hello status of hello command in hello command history.</span></span>

   ![Panoda komut durumu][img-pingcommand]

<span data-ttu-id="f46f1-320">Merhaba çözüm, gönderdiği her bir komutun hello durumunu izler.</span><span class="sxs-lookup"><span data-stu-id="f46f1-320">hello solution tracks hello status of each command it sends.</span></span> <span data-ttu-id="f46f1-321">Başlangıçta hello sonucudur **bekleyen**.</span><span class="sxs-lookup"><span data-stu-id="f46f1-321">Initially hello result is **Pending**.</span></span> <span data-ttu-id="f46f1-322">Merhaba cihaz onu hello komutu yürüttüğünü raporladığında hello sonuç çok kümesi**başarı**.</span><span class="sxs-lookup"><span data-stu-id="f46f1-322">When hello device reports that it has executed hello command, hello result is set too**Success**.</span></span>

## <a name="behind-hello-scenes"></a><span data-ttu-id="f46f1-323">Merhaba arka planda</span><span class="sxs-lookup"><span data-stu-id="f46f1-323">Behind hello scenes</span></span>

<span data-ttu-id="f46f1-324">Önceden yapılandırılmış çözümü dağıttığınızda, hello dağıtım işlemi hello Seçtiğiniz Azure aboneliği birden çok kaynak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f46f1-324">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="f46f1-325">Bu kaynaklar hello Azure görüntüleyebilirsiniz [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="f46f1-325">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="f46f1-326">Merhaba dağıtım işlemi oluşturur bir **kaynak grubu** önceden yapılandırılmış çözümünüz için seçtiğiniz hello adına dayalı bir ada sahip:</span><span class="sxs-lookup"><span data-stu-id="f46f1-326">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Önceden yapılandırılmış çözümde hello Azure portalı][img-portal]

<span data-ttu-id="f46f1-328">Her bir kaynağın hello ayarları hello hello kaynak grubundaki kaynaklar listesinde seçerek görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-328">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="f46f1-329">Merhaba hello önceden yapılandırılmış çözüm için kaynak kodunu da görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f46f1-329">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="f46f1-330">Merhaba uzaktan önceden yapılandırılmış çözümün kaynak kodunu izleme olduğu hello [azure-iot-remote-monitoring] [ lnk-rmgithub] GitHub deposunu:</span><span class="sxs-lookup"><span data-stu-id="f46f1-330">hello remote monitoring preconfigured solution source code is in hello [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="f46f1-331">Merhaba **DeviceAdministration** klasörü hello hello Pano için kaynak kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-331">hello **DeviceAdministration** folder contains hello source code for hello dashboard.</span></span>
* <span data-ttu-id="f46f1-332">Merhaba **Simulator** klasörü hello hello sanal cihaz için kaynak kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-332">hello **Simulator** folder contains hello source code for hello simulated device.</span></span>
* <span data-ttu-id="f46f1-333">Merhaba **EventProcessor** klasörü hello gelen telemetriyi işleyen hello arka uç işleme için hello kaynak kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="f46f1-333">hello **EventProcessor** folder contains hello source code for hello back-end process that handles hello incoming telemetry.</span></span>

<span data-ttu-id="f46f1-334">İşiniz bittiğinde, Azure aboneliğinizin hello üzerinde hello önceden yapılandırılmış çözüm silebilirsiniz [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="f46f1-334">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="f46f1-335">Bu sitenin tüm hello önceden yapılandırılmış çözümü oluşturduğunuzda sağlanan kaynakları hello tooeasily Sil sağlar.</span><span class="sxs-lookup"><span data-stu-id="f46f1-335">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="f46f1-336">her şeyi silin tooensure toohello önceden yapılandırılmış çözümle ilgili, üzerinde hello silme [azureiotsuite.com] [ lnk-azureiotsuite] site ve hello portal hello kaynak grubunda silmeyin.</span><span class="sxs-lookup"><span data-stu-id="f46f1-336">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site and do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f46f1-337">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f46f1-337">Next Steps</span></span>

<span data-ttu-id="f46f1-338">Çalışan bir önceden çözüm dağıttıktan sonra aşağıdaki makaleler hello okuyarak IOT paketi ile Başlarken devam edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f46f1-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="f46f1-339">[Uzaktan izleme önceden yapılandırılmış çözüm kılavuzu][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="f46f1-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="f46f1-340">[Uzaktan izleme çözümü, aygıt toohello Bağlan][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="f46f1-340">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="f46f1-341">[Merhaba azureiotsuite.com sitesindeki izinler][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="f46f1-341">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md