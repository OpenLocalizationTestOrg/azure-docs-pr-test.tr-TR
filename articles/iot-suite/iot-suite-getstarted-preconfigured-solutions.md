---
title: "Önceden yapılandırılmış çözümleri kullanmaya başlama | Microsoft Belgeleri"
description: "Önceden yapılandırılmış bir Azure IoT Paketi çözümünün nasıl dağıtılacağını öğrenmek için bu öğreticiyi izleyin."
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
ms.openlocfilehash: 466825ab78a5ac9773d8beff69cca90ff9db6c01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-preconfigured-solutions"></a><span data-ttu-id="e4860-103">Önceden yapılandırılmış çözümleri kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="e4860-103">Get started with the preconfigured solutions</span></span>

<span data-ttu-id="e4860-104">Azure IoT Paketi [önceden yapılandırılmış çözümleri][lnk-preconfigured-solutions], ortak IoT iş senaryolarını uygulayan uçtan uca çözümler sunmak için birden çok Azure IoT hizmetini birleştirir.</span><span class="sxs-lookup"><span data-stu-id="e4860-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="e4860-105">Önceden yapılandırılmış *uzaktan izleme* çözümü cihazlarınıza bağlanır ve cihazları izler.</span><span class="sxs-lookup"><span data-stu-id="e4860-105">The *remote monitoring* preconfigured solution connects to and monitors your devices.</span></span> <span data-ttu-id="e4860-106">Cihazlarınızdan alınan veri akışını analiz etmek ve işlemleri bu veri akışına otomatik olarak yanıt verecek hale getirerek iş sonuçlarını iyileştirmek için bu çözümü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-106">You can use the solution to analyze the stream of data from your devices and to improve business outcomes by making processes respond automatically to that stream of data.</span></span>

<span data-ttu-id="e4860-107">Bu öğretici, önceden yapılandırılmış uzaktan izleme çözümünün nasıl hazırlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e4860-107">This tutorial shows you how to provision the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="e4860-108">Ayrıca, önceden yapılandırılmış çözümün temel özelliklerinde rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="e4860-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="e4860-109">Bu özelliklerin birçoğuna önceden yapılandırılmış çözümün bir parçası olarak dağıtılan çözüm *panosundan* erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e4860-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![Önceden yapılandırılmış uzaktan izleme panosu][img-dashboard]

<span data-ttu-id="e4860-111">Bu öğreticiyi tamamlamak için etkin bir Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e4860-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e4860-112">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e4860-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="e4860-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="e4860-114">Senaryoya genel bakış</span><span class="sxs-lookup"><span data-stu-id="e4860-114">Scenario overview</span></span>

<span data-ttu-id="e4860-115">Önceden yapılandırılmış uzaktan izleme çözümünü dağıttığınızda, genel bir uzaktan izleme senaryosunu adım adım görmenize olanak sağlayan kaynaklar ile önceden doldurulur.</span><span class="sxs-lookup"><span data-stu-id="e4860-115">When you deploy the remote monitoring preconfigured solution, it is prepopulated with resources that enable you to step through a common remote monitoring scenario.</span></span> <span data-ttu-id="e4860-116">Bu senaryoda, çözüme bağlı çeşitli cihazlar beklenmeyen sıcaklık değerleri bildirmektedir.</span><span class="sxs-lookup"><span data-stu-id="e4860-116">In this scenario, several devices connected to the solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="e4860-117">Aşağıdaki bölümlerde şunları nasıl yapacağınız açıklanır:</span><span class="sxs-lookup"><span data-stu-id="e4860-117">The following sections show you how to:</span></span>

* <span data-ttu-id="e4860-118">Beklenmeyen sıcaklık değerleri gönderen cihazları belirleme.</span><span class="sxs-lookup"><span data-stu-id="e4860-118">Identify the devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="e4860-119">Bu cihazları daha ayrıntılı telemetri göndermek için yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="e4860-119">Configure these devices to send more detailed telemetry.</span></span>
* <span data-ttu-id="e4860-120">Bu cihazlarda üretici yazılımını güncelleştirerek sorunu giderme.</span><span class="sxs-lookup"><span data-stu-id="e4860-120">Fix the problem by updating the firmware on these devices.</span></span>
* <span data-ttu-id="e4860-121">Eyleminizin sorunu çözdüğünü doğrulama.</span><span class="sxs-lookup"><span data-stu-id="e4860-121">Verify that your action has resolved the issue.</span></span>

<span data-ttu-id="e4860-122">Bu senaryonun temel bir özelliği, çözüm panosu kullanılarak tüm bu eylemlerin uzaktan gerçekleştirilebiliyor olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="e4860-122">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="e4860-123">Cihazlara fiziksel erişiminizin olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="e4860-123">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="e4860-124">Çözüm panosunu görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e4860-124">View the solution dashboard</span></span>

<span data-ttu-id="e4860-125">Çözüm panosu, dağıtılan çözümü yönetmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e4860-125">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="e4860-126">Örneğin, telemetriyi görüntüleyebilir, cihazları ekleyebilir ve kuralları yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="e4860-127">Sağlama tamamlandığında ve önceden yapılandırılmış çözümünüzün kutucuğu **Hazır**’ı gösterdiğinde, uzaktan izleme çözümü portalınızı yeni bir sekmede açmak için **Başlat**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-127">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Önceden yapılandırılmış çözümü başlatma][img-launch-solution]

1. <span data-ttu-id="e4860-129">Varsayılan olarak, çözüm portalı *panoyu* gösterir.</span><span class="sxs-lookup"><span data-stu-id="e4860-129">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="e4860-130">Sayfanın sol tarafındaki menüyü kullanarak çözüm portalının diğer alanlarına gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-130">You can navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Önceden yapılandırılmış uzaktan izleme panosu][img-menu]

<span data-ttu-id="e4860-132">Pano aşağıdaki bilgileri gösterir:</span><span class="sxs-lookup"><span data-stu-id="e4860-132">The dashboard displays the following information:</span></span>

* <span data-ttu-id="e4860-133">Çözüme bağlı olan her bir cihazın konumunu görüntüleyen bir harita.</span><span class="sxs-lookup"><span data-stu-id="e4860-133">A map that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="e4860-134">Çözümü ilk kez çalıştırdığınızda, 25 sanal cihaz bulunur.</span><span class="sxs-lookup"><span data-stu-id="e4860-134">When you first run the solution, there are 25 simulated devices.</span></span> <span data-ttu-id="e4860-135">Sanal cihazlar Azure WebJobs olarak uygulanır ve çözüm de haritada bilgileri çizmek için Bing Haritaları API'sini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e4860-135">The simulated devices are implemented as Azure WebJobs, and the solution uses the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="e4860-136">Eşlemeyi nasıl dinamik hale getireceğinizi öğrenmek için [SSS][lnk-faq] bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="e4860-136">See the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="e4860-137">Seçilen yakın gerçek zamanlı cihazdan nem ve sıcaklık telemetrisini çizen ve maksimum, minimum ve ortalama nem gibi toplu verileri görüntüleyen bir **Telemetri Geçmişi** paneli.</span><span class="sxs-lookup"><span data-stu-id="e4860-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="e4860-138">Bir telemetri değeri bir eşiği aştığında yeni uyarı etkinliklerini gösteren bir **Uyarı Geçmişi** paneli.</span><span class="sxs-lookup"><span data-stu-id="e4860-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="e4860-139">Önceden yapılandırılmış çözüm tarafından oluşturulan örneklere ek olarak kendi alarmlarınızı tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-139">You can define your own alarms in addition to the examples created by the preconfigured solution.</span></span>
* <span data-ttu-id="e4860-140">Zamanlanmış işler hakkında bilgiler gösteren bir **İşler** paneli.</span><span class="sxs-lookup"><span data-stu-id="e4860-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="e4860-141">**Yönetim işleri** sayfasından kendi işlerinizi zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="e4860-142">Uyarıları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e4860-142">View alarms</span></span>

<span data-ttu-id="e4860-143">Uyarı geçmişi paneli beş cihazın beklenenden yüksek telemetri değerleri bildirdiğini gösteriyor.</span><span class="sxs-lookup"><span data-stu-id="e4860-143">The alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![Çözüm panosunda TODO Uyarı geçmişi][img-alarms]

> [!NOTE]
> <span data-ttu-id="e4860-145">Bu uyarılar önceden yapılandırılmış çözüme dahil edilen bir kural tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e4860-145">These alarms are generated by a rule that is included in the preconfigured solution.</span></span> <span data-ttu-id="e4860-146">Bu kural, bir cihaz tarafından gönderilen sıcaklık değeri 60’ı aştığında bir uyarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e4860-146">This rule generates an alert when the temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="e4860-147">Sol menüde [Kurallar](#add-a-rule) ve [Eylemler](#add-an-action)’i seçerek kendi kural ve eylemlerinizi tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in the left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="e4860-148">Cihazları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e4860-148">View devices</span></span>

<span data-ttu-id="e4860-149">*Cihazlar* listesi, çözümde kayıtlı olan tüm cihazları gösterir.</span><span class="sxs-lookup"><span data-stu-id="e4860-149">The *devices* list shows all the registered devices in the solution.</span></span> <span data-ttu-id="e4860-150">Cihaz listesinden cihaz meta verilerini görüntüleyip düzenleyebilir, cihaz ekleyip kaldırabilir ve cihazlarda yöntemler çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-150">From the device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="e4860-151">Cihaz listesindeki cihazları filtreleyebilir ve sıralayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-151">You can filter and sort the list of devices in the device list.</span></span> <span data-ttu-id="e4860-152">Ayrıca cihaz listesinde gösterilen sütunları özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-152">You can also customize the columns shown in the device list.</span></span>

1. <span data-ttu-id="e4860-153">Bu çözüm için cihaz listesini görüntülemek için **Cihazlar**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-153">Choose **Devices** to show the device list for this solution.</span></span>

   ![Çözüm portalında cihaz listesini görüntüleme][img-devicelist]

1. <span data-ttu-id="e4860-155">Cihaz listesi başlangıçta sağlama işlemi tarafından oluşturulan 25 sanal cihazı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e4860-155">The device list initially shows 25 simulated devices created by the provisioning process.</span></span> <span data-ttu-id="e4860-156">Çözüme başka sanal ve fiziksel cihazlar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-156">You can add additional simulated and physical devices to the solution.</span></span>

1. <span data-ttu-id="e4860-157">Cihaz ayrıntılarını görüntülemek için cihaz listesindeki bir cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-157">To view the details of a device, choose a device in the device list.</span></span>

   ![Çözüm portalında cihaz ayrıntılarını görüntüleme][img-devicedetails]

<span data-ttu-id="e4860-159">**Cihaz Ayrıntıları** panelinde altı bölüm bulunur:</span><span class="sxs-lookup"><span data-stu-id="e4860-159">The **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="e4860-160">Cihaz simgesini özelleştirmenizi, cihazı devre dışı bırakmanızı, kural eklemenizi, bir yöntem çağırmanızı veya bir komut göndermenizi sağlayan bağlantı koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="e4860-160">A collection of links that enable you to customize the device icon, disable the device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="e4860-161">Komutlar (cihazdan buluta iletiler) ile yöntemlerin (doğrudan yöntemler) bir karşılaştırması için bkz. [Buluttan cihaza iletişim kılavuzu][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="e4860-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="e4860-162">**Cihaz İkizi - Etiketler** bölümünde, cihazın etiket değerlerini düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-162">The **Device Twin - Tags** section enables you to edit tag values for the device.</span></span> <span data-ttu-id="e4860-163">Cihaz listesindeki etiket değerlerini görüntüleyebilir ve etiket değerlerini kullanarak cihaz listesini filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-163">You can display tag values in the device list and use tag values to filter the device list.</span></span>
* <span data-ttu-id="e4860-164">**Cihaz İkizi - İstenen Özellikler** bölümünde, cihaza gönderilecek özellik değerlerini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-164">The **Device Twin - Desired Properties** section enables you to set property values to be sent to the device.</span></span>
* <span data-ttu-id="e4860-165">**Cihaz İkizi - Bildirilen Özellikler** bölümünde cihazdan gönderilen özellik değerleri gösterilir.</span><span class="sxs-lookup"><span data-stu-id="e4860-165">The **Device Twin - Reported Properties** section shows property values sent from the device.</span></span>
* <span data-ttu-id="e4860-166">**Cihaz Özellikleri** bölümünde cihaz kimliği ve kimlik doğrulama anahtarları gibi kimlik kayıt defteri bilgileri gösterilir.</span><span class="sxs-lookup"><span data-stu-id="e4860-166">The **Device Properties** section shows information from the identity registry such as the device id and authentication keys.</span></span>
* <span data-ttu-id="e4860-167">**Son İşler** bölümünde yakın zamanda bu cihazı hedefleyen tüm işlere ilişkin bilgiler gösterilir.</span><span class="sxs-lookup"><span data-stu-id="e4860-167">The **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-the-device-list"></a><span data-ttu-id="e4860-168">Cihaz listesini filtreleme</span><span class="sxs-lookup"><span data-stu-id="e4860-168">Filter the device list</span></span>

<span data-ttu-id="e4860-169">Yalnızca beklenmeyen sıcaklık değerleri gönderen cihazları görüntülemek için bir filtre kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-169">You can use a filter to display only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="e4860-170">Önceden yapılandırılmış uzaktan izleme çözümü 60 değerinden yüksek ortalama sıcaklığa sahip cihazları göstermek için **Sistem durumu kötü olan cihazlar** filtresini içerir.</span><span class="sxs-lookup"><span data-stu-id="e4860-170">The remote monitoring preconfigured solution includes the **Unhealthy devices** filter to show devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="e4860-171">Ayrıca [kendi filtrelerinizi oluşturabilirsiniz](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="e4860-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="e4860-172">Kullanılabilir filtrelerin bir listesini görüntülemek için **Kayıtlı filtre aç**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-172">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="e4860-173">Ardından filtreyi uygulamak için **Sistem durumu kötü olan cihazlar**’ı seçin:</span><span class="sxs-lookup"><span data-stu-id="e4860-173">Then choose **Unhealthy devices** to apply the filter:</span></span>

    ![Filtrelerin listesini görüntüleme][img-unhealthy-filter]

1. <span data-ttu-id="e4860-175">Cihaz listesi artık yalnızca ortalama sıcaklık değeri 60’ın üzerinde olan cihazları gösterir.</span><span class="sxs-lookup"><span data-stu-id="e4860-175">The device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![Sistem durumu kötü olan cihazları gösteren filtrelenmiş cihaz listesini görüntüleme][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="e4860-177">İstenen özellikleri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e4860-177">Update desired properties</span></span>

<span data-ttu-id="e4860-178">Düzeltilmesi gerekebilen bir cihaz kümesi belirlediniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="e4860-179">Ancak 15 saniyelik veri sıklığının sorunu açık bir şekilde tanılamak için yeterli olmadığına karar verdiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-179">However, you decide that the data frequency of 15 seconds is not sufficient for a clear diagnosis of the issue.</span></span> <span data-ttu-id="e4860-180">Telemetri sıklığını beş saniye olarak değiştirmek sorunu daha iyi tanılamak için daha fazla veri noktasına sahip olmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e4860-180">Changing the telemetry frequency to five seconds to provide you with more data points to better diagnose the issue.</span></span> <span data-ttu-id="e4860-181">Bu yapılandırma değişikliğini çözüm portalından uzak cihazlarınıza gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-181">You can push this configuration change to your remote devices from the solution portal.</span></span> <span data-ttu-id="e4860-182">Değişikliği bir kez yapıp etkisini değerlendirerek daha sonra sonuçlara uygun şekilde eylem gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-182">You can make the change once, evaluate the impact, and then act on the results.</span></span>

<span data-ttu-id="e4860-183">Etkilenen cihazlar için **TelemetryInterval** istenen özelliğini değiştiren bir iş çalıştırmak için bu adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e4860-183">Follow these steps to run a job that changes the **TelemetryInterval** desired property for the affected devices.</span></span> <span data-ttu-id="e4860-184">Cihazlar yeni **TelemetryInterval** özellik değerini aldığında, her 15 saniyede bir yerine her beş saniyede bir telemetri gönderecek şekilde yapılandırmalarını değiştirirler:</span><span class="sxs-lookup"><span data-stu-id="e4860-184">When the devices receive the new **TelemetryInterval** property value, they change their configuration to send telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="e4860-185">Cihaz listesinde sistem durumu iyi olmayan cihazların listesini görüntülerken, **İş Zamanlayıcı**’yı ve ardından **Cihaz İkizini Düzenle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-185">While you are showing the list of unhealthy devices in the device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="e4860-186">İşe **Telemetri aralığını değiştir** adını verin.</span><span class="sxs-lookup"><span data-stu-id="e4860-186">Call the job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="e4860-187">**İstenen Özellik** adının **desired.Config.TelemetryInterval** değerini beş saniye olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e4860-187">Change the value of the **Desired Property** name **desired.Config.TelemetryInterval** to five seconds.</span></span>

1. <span data-ttu-id="e4860-188">**Zamanlama**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-188">Choose **Schedule**.</span></span>

    ![TelemetryInterval özelliğini beş saniye olarak değiştirme][img-change-interval]

1. <span data-ttu-id="e4860-190">İşin ilerleyişini portaldaki **Yönetim İşleri** sayfasında izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-190">You can monitor the progress of the job on the **Management Jobs** page in the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="e4860-191">Tek cihaz için istenen özellik değerini değiştirmek istiyorsanız, bir iş çalıştırmak yerine **Cihaz Ayrıntıları** panelindeki **İstenen Özellikler** bölümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="e4860-191">If you want to change a desired property value for an individual device, use the **Desired Properties** section in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="e4860-192">Bu iş, filtre tarafından seçilen tüm cihazlar için cihaz ikizinde **TelemetryInterval** istenen özelliğinin değerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e4860-192">This job sets the value of the **TelemetryInterval** desired property in the device twin for all the devices selected by the filter.</span></span> <span data-ttu-id="e4860-193">Cihazlar bu değeri cihaz ikizinden alarak davranışlarını güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="e4860-193">The devices retrieve this value from the device twin and update their behavior.</span></span> <span data-ttu-id="e4860-194">Bir cihaz, cihaz ikizinden istenen bir özelliği alıp işlediğinde, karşılık gelen bildirilen değer özelliğini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e4860-194">When a device retrieves and processes a desired property from a device twin, it sets the corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="e4860-195">Çağırma yöntemleri</span><span class="sxs-lookup"><span data-stu-id="e4860-195">Invoke methods</span></span>

<span data-ttu-id="e4860-196">İş çalışırken, sistem durumu kötü olan cihazlar listesindeki tüm cihazların eski (1.6’dan önceki) üretici yazılımına sahip olduğunu fark edersiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-196">While the job runs, you notice in the list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![Sistem durumu kötü olan cihazlar için bildirilen üretici yazılımı sürümünü görüntüleme][img-old-firmware]

<span data-ttu-id="e4860-198">Sistem durumu iyi olan diğer cihazların yakın zamanda 2.0 sürümüne güncelleştirildiğini bildiğiniz için, beklenmeyen sıcaklık değerlerinin kaynağı bu üretici yazılımı sürümü olabilir.</span><span class="sxs-lookup"><span data-stu-id="e4860-198">This firmware version may be the root cause of the unexpected temperature values because you know that other healthy devices were recently updated to version 2.0.</span></span> <span data-ttu-id="e4860-199">Eski üretici yazılımı sürümlerine sahip cihazları belirlemek için yerleşik **Eski üretici yazılımı cihazları** filtresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-199">You can use the built-in **Old firmware devices** filter to identify any devices with old firmware versions.</span></span> <span data-ttu-id="e4860-200">Daha sonra, portaldan hala eski üretici yazılımı sürümlerini çalıştıran tüm cihazları uzaktan güncelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e4860-200">From the portal, you can then remotely update all the devices still running old firmware versions:</span></span>

1. <span data-ttu-id="e4860-201">Kullanılabilir filtrelerin bir listesini görüntülemek için **Kayıtlı filtre aç**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-201">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="e4860-202">Ardından filtreyi uygulamak için **Eski üretici yazılımı cihazları**’nı seçin:</span><span class="sxs-lookup"><span data-stu-id="e4860-202">Then choose **Old firmware devices** to apply the filter:</span></span>

    ![Filtrelerin listesini görüntüleme][img-old-filter]

1. <span data-ttu-id="e4860-204">Cihaz listesi artık yalnızca eski üretici yazılımı sürümlerine sahip cihazları gösterir.</span><span class="sxs-lookup"><span data-stu-id="e4860-204">The device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="e4860-205">Bu liste **Sistem durumu kötü olan cihazlar** filtresi tarafından belirlenen beş cihazı ve üç ek cihazı içerir:</span><span class="sxs-lookup"><span data-stu-id="e4860-205">This list includes the five devices identified by the **Unhealthy devices** filter and three additional devices:</span></span>

    ![Eski cihazları gösteren filtrelenmiş cihaz listesini görüntüleme][img-filtered-old-list]

1. <span data-ttu-id="e4860-207">**İş Zamanlayıcı**’yı ve ardından **Invoke Yöntemi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="e4860-208">**İş Adı**’nı **Üretici yazılımını 2.0 sürümüne güncelleştirme** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e4860-208">Set **Job Name** to **Firmware update to version 2.0**.</span></span>

1. <span data-ttu-id="e4860-209">**Yöntem** olarak **InitiateFirmwareUpdate**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-209">Choose **InitiateFirmwareUpdate** as the **Method**.</span></span>

1. <span data-ttu-id="e4860-210">**FwPackageUri** parametresini **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e4860-210">Set the **FwPackageUri** parameter to **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="e4860-211">**Zamanlama**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-211">Choose **Schedule**.</span></span> <span data-ttu-id="e4860-212">Artık varsayılan ayar işin çalıştırılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="e4860-212">The default is for the job to run now.</span></span>

    ![Seçili cihazların üretici yazılımını güncelleştirmek için iş oluşturma][img-method-update]

> [!NOTE]
> <span data-ttu-id="e4860-214">Tek bir cihazda bir yöntem çağırmak istiyorsanız, bir iş çalıştırmak yerine **Cihaz Ayrıntıları** panelinde **Yöntemler**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-214">If you want to invoke a method on an individual device, choose **Methods** in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="e4860-215">Bu iş, filtre ile seçilen tüm cihazlarda **InitiateFirmwareUpdate** doğrudan yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="e4860-215">This job invokes the **InitiateFirmwareUpdate** direct method on all the devices selected by the filter.</span></span> <span data-ttu-id="e4860-216">Cihazlar hemen IoT Hub’a yanıt verir ve ardından üretici yazılımı güncelleştirme işlemini zaman uyumsuz olarak başlatır.</span><span class="sxs-lookup"><span data-stu-id="e4860-216">Devices respond immediately to IoT Hub and then initiate the firmware update process asynchronously.</span></span> <span data-ttu-id="e4860-217">Cihaz aşağıdaki ekran görüntülerinde gösterildiği gibi bildirilen özellik değerleri aracılığıyla üretici yazılımı güncelleştirme süreci hakkında durum bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="e4860-217">The devices provide status information about the firmware update process through reported property values, as shown in the following screenshots.</span></span> <span data-ttu-id="e4860-218">Cihaz ve iş listelerindeki bilgileri güncelleştirmek için **Yenile** simgesini seçin:</span><span class="sxs-lookup"><span data-stu-id="e4860-218">Choose the **Refresh** icon to update the information in the device and job lists:</span></span>

<span data-ttu-id="e4860-219">![Üretici yazılımı güncelleştirme listesinin çalıştığını gösteren iş listesi][img-update-1]
![Üretici yazılımının güncelleştirme durumunu gösteren cihaz listesi][img-update-2]
![Üretici yazılımı güncelleştirme listesinin tamamladığını gösteren iş listesi][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="e4860-219">![Job list showing the firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing the firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="e4860-220">Bir üretim ortamında, işleri belirlenen bir bakım penceresi sırasında çalışmak için zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-220">In a production environment, you can schedule jobs to run during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="e4860-221">Senaryo gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="e4860-221">Scenario review</span></span>

<span data-ttu-id="e4860-222">Bu senaryoda, panodaki uyarı geçmişini ve bir filtre kullanarak uzak cihazlarınızdan bazılarında olası bir sorun belirlediniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-222">In this scenario, you identified a potential issue with some of your remote devices using the alarm history on the dashboard and a filter.</span></span> <span data-ttu-id="e4860-223">Daha sonra sorunu tanılamaya yardımcı olmak üzere daha fazla bilgi sağlamak için bir filtre ve iş kullanarak cihazları uzaktan yapılandırdınız.</span><span class="sxs-lookup"><span data-stu-id="e4860-223">You then used the filter and a job to remotely configure the devices to provide more information to help diagnose the issue.</span></span> <span data-ttu-id="e4860-224">Son olarak, etkilenen cihazlarda bakım zamanlamak için bir filtre ve iş kullandınız.</span><span class="sxs-lookup"><span data-stu-id="e4860-224">Finally, you used a filter and a job to schedule maintenance on the affected devices.</span></span> <span data-ttu-id="e4860-225">Panoya dönerseniz, artık çözümünüzdeki cihazlardan gelen herhangi bir alarm olmadığını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e4860-225">If you return to the dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="e4860-226">Üretici yazılımının çözümünüzdeki tüm cihazlarda güncel olduğundan ve sistem durumu kötü başka cihaz olmadığından emin olmak için bir filtre kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e4860-226">You can use a filter to verify that the firmware is up-to-date on all the devices in your solution and that there are no more unhealthy devices:</span></span>

![Tüm cihazlarda güncel üretici yazılımı olduğunu gösteren filtre][img-updated]

![Tüm cihazların sistem durumunun iyi olduğunu gösteren filtre][img-healthy]

## <a name="other-features"></a><span data-ttu-id="e4860-229">Diğer özellikler</span><span class="sxs-lookup"><span data-stu-id="e4860-229">Other features</span></span>

<span data-ttu-id="e4860-230">Aşağıdaki bölümlerde, önceden yapılandırılmış uzaktan izleme çözümünün önceki senaryonun parçası olarak bahsedilmeyen bazı ek özellikleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e4860-230">The following sections describe some additional features of the remote monitoring preconfigured solution that are not described as part of the previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="e4860-231">Sütunları özelleştirme</span><span class="sxs-lookup"><span data-stu-id="e4860-231">Customize columns</span></span>

<span data-ttu-id="e4860-232">**Sütun düzenleyicisi**’ni seçerek cihaz listesinde gösterilen bilgileri özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-232">You can customize the information shown in the device list by choosing **Column editor**.</span></span> <span data-ttu-id="e4860-233">Bildirilen özellik ve etiket değerlerini gösteren sütunlar ekleyip kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="e4860-234">Ayrıca, sütunları yeniden sıralayabilir ve yeniden adlandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e4860-234">You can also reorder and rename columns:</span></span>

   ![Cihaz listesinde sütun düzenleyicisi][img-columneditor]

### <a name="customize-the-device-icon"></a><span data-ttu-id="e4860-236">Cihaz simgesini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="e4860-236">Customize the device icon</span></span>

<span data-ttu-id="e4860-237">Cihaz listesinde gösterilen cihaz simgesini, **Cihaz Ayrıntıları** panelinden aşağıdaki gibi özelleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e4860-237">You can customize the device icon displayed in the device list from the **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="e4860-238">Bir cihazın **Görüntü düzenleme** panelini açmak için kalem simgesini seçin:</span><span class="sxs-lookup"><span data-stu-id="e4860-238">Choose the pencil icon to open the **Edit image** panel for a device:</span></span>

   ![Cihaz görüntüsü düzenleyicisini açma][img-startimageedit]

1. <span data-ttu-id="e4860-240">Karşıya yeni bir görüntü yükleyip veya var olan görüntülerden birini seçip **Kaydet**’i seçin:</span><span class="sxs-lookup"><span data-stu-id="e4860-240">Either upload a new image or use one of the existing images and then choose **Save**:</span></span>

   ![Cihaz görüntüsü düzenleyicisini düzenleme][img-imageedit]

1. <span data-ttu-id="e4860-242">Seçtiğiniz görüntü, cihazın **Simge** sütununda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="e4860-242">The image you selected now displays in the **Icon** column for the device.</span></span>

> [!NOTE]
> <span data-ttu-id="e4860-243">Görüntü, blob depolama alanına depolanır.</span><span class="sxs-lookup"><span data-stu-id="e4860-243">The image is stored in blob storage.</span></span> <span data-ttu-id="e4860-244">Cihaz ikizindeki etiket, blob depolama alanındaki görüntünün bir bağlantısını içerir.</span><span class="sxs-lookup"><span data-stu-id="e4860-244">A tag in the device twin contains a link to the image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="e4860-245">Cihaz ekleme</span><span class="sxs-lookup"><span data-stu-id="e4860-245">Add a device</span></span>

<span data-ttu-id="e4860-246">Önceden yapılandırılmış çözümü dağıttığınızda cihaz listesinde görebileceğiniz 25 örnek cihazı otomatik olarak hazırlarsınız.</span><span class="sxs-lookup"><span data-stu-id="e4860-246">When you deploy the preconfigured solution, you automatically provision 25 sample devices that you can see in the device list.</span></span> <span data-ttu-id="e4860-247">Bu cihazlar bir Azure WebJob içinde çalışan *sanal cihazlardır*.</span><span class="sxs-lookup"><span data-stu-id="e4860-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="e4860-248">Sanal cihazlar herhangi bir gerçek ve fiziksel cihaza dağıtmaya gerek olmadan önceden yapılandırılmış çözümü denemenizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="e4860-248">Simulated devices make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical devices.</span></span> <span data-ttu-id="e4860-249">Çözüme gerçek bir cihaz bağlamak istemiyorsanız [Cihazınızı önceden yapılandırılmış uzaktan izleme çözümüne bağlama][lnk-connect-rm] öğreticisine bakın.</span><span class="sxs-lookup"><span data-stu-id="e4860-249">If you do want to connect a real device to the solution, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="e4860-250">Aşağıdaki adımlar bir sanal cihazın çözüme nasıl ekleneceğini göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="e4860-250">The following steps show you how to add a simulated device to the solution:</span></span>

1. <span data-ttu-id="e4860-251">Cihaz listesine geri gidin.</span><span class="sxs-lookup"><span data-stu-id="e4860-251">Navigate back to the device list.</span></span>

1. <span data-ttu-id="e4860-252">Bir cihaz eklemek için sol alt köşedeki **+ Cihaz Ekle** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="e4860-252">To add a device, choose **+ Add A Device** in the bottom left corner.</span></span>

   ![Önceden yapılandırılmış çözüme cihaz ekleme][img-adddevice]

1. <span data-ttu-id="e4860-254">**Sanal Cihaz** kutucuğundaki **Yeni Ekle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-254">Choose **Add New** on the **Simulated Device** tile.</span></span>

   ![Panoda yeni cihaz ayrıntılarını ayarlama][img-addnew]

   <span data-ttu-id="e4860-256">Yeni bir sanal cihaz oluşturmaya ek olarak, bir **Özel Cihaz** oluşturmayı seçerseniz fiziksel bir cihaz da ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-256">In addition to creating a new simulated device, you can also add a physical device if you choose to create a **Custom Device**.</span></span> <span data-ttu-id="e4860-257">Çözüme fiziksel cihazlar bağlama hakkında daha fazla bilgi edinmek için bkz. [Cihazınızı önceden yapılandırılmış IoT paketi uzak izleme çözümüne bağlama][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="e4860-257">To learn more about connecting physical devices to the solution, see [Connect your device to the IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="e4860-258">**Kendi Cihaz Kimliğimi tanımlamama izin ver**'i seçin ve **mydevice_01** gibi benzersiz bir cihaz kimliği girin.</span><span class="sxs-lookup"><span data-stu-id="e4860-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="e4860-259">**Oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-259">Choose **Create**.</span></span>

   ![Yeni bir cihaz kaydetme][img-definedevice]

1. <span data-ttu-id="e4860-261">**Bir sanal cihaz ekleme**’nin 3. adımında cihaz listesine geri dönmek için **Bitti**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-261">In step 3 of **Add a simulated device**, choose **Done** to return to the device list.</span></span>

1. <span data-ttu-id="e4860-262">Cihazınızın **Çalışıyor** olduğunu cihaz listesinde görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-262">You can view your device **Running** in the device list.</span></span>

    ![Cihaz listesinde yeni cihazı görüntüleme][img-runningnew]

1. <span data-ttu-id="e4860-264">Panodaki yeni cihazınızdan sanal telemetriyi de görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e4860-264">You can also view the simulated telemetry from your new device on the dashboard:</span></span>

    ![Yeni cihazdan telemetri görüntüleme][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="e4860-266">Bir cihazı devre dışı bırakma ve silme</span><span class="sxs-lookup"><span data-stu-id="e4860-266">Disable and delete a device</span></span>

<span data-ttu-id="e4860-267">Bir Cihazı devre dışı bırakabilir, devre dışı kaldıktan sonra da kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e4860-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Bir cihazı devre dışı bırakma ve kaldırma][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="e4860-269">Kural ekleme</span><span class="sxs-lookup"><span data-stu-id="e4860-269">Add a rule</span></span>

<span data-ttu-id="e4860-270">Yeni eklediğiniz yeni cihaz için hiçbir kural bulunmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="e4860-270">There are no rules for the new device you just added.</span></span> <span data-ttu-id="e4860-271">Bu bölümde, yeni cihaz tarafından bildirilen sıcaklık 47 dereceyi aştığında uyarı tetikleyen bir kural ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-271">In this section, you add a rule that triggers an alarm when the temperature reported by the new device exceeds 47 degrees.</span></span> <span data-ttu-id="e4860-272">Başlamadan önce, panoda yeni cihaz için telemetri geçmişinin, cihaz sıcaklığının hiçbir zaman 45 dereceyi aşmadığını gösterdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e4860-272">Before you start, notice that the telemetry history for the new device on the dashboard shows the device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="e4860-273">Cihaz listesine geri gidin.</span><span class="sxs-lookup"><span data-stu-id="e4860-273">Navigate back to the device list.</span></span>

1. <span data-ttu-id="e4860-274">Cihaz için bir kural eklemek üzere **Cihazlar Listesi**’nde yeni cihazınızı seçin ve ardından **Kural ekle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-274">To add a rule for the device, select your new device in the **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="e4860-275">Veri alanı olarak **Temperature** ve sıcaklık 47 dereceyi aştığında çıktı olarak **AlarmTemp** kullanan bir kural oluşturun:</span><span class="sxs-lookup"><span data-stu-id="e4860-275">Create a rule that uses **Temperature** as the data field and uses **AlarmTemp** as the output when the temperature exceeds 47 degrees:</span></span>

    ![Cihaz kuralı ekleme][img-adddevicerule]

1. <span data-ttu-id="e4860-277">Yaptığınız değişiklikleri kaydetmek için **Kuralları Kaydet ve Görüntüle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-277">To save your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="e4860-278">Yeni cihaz için cihaz ayrıntıları bölmesinde **Komutlar**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-278">Choose **Commands** in the device details pane for the new device.</span></span>

    ![Cihaz kuralı ekleme][img-adddevicerule2]

1. <span data-ttu-id="e4860-280">Komut listesinden **ChangeSetPointTemp**'i seçin ve **SetPointTemp**'i 45 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e4860-280">Select **ChangeSetPointTemp** from the command list and set **SetPointTemp** to 45.</span></span> <span data-ttu-id="e4860-281">Ardından **Komut Gönder**’i seçin:</span><span class="sxs-lookup"><span data-stu-id="e4860-281">Then choose **Send Command**:</span></span>

    ![Cihaz kuralı ekleme][img-adddevicerule3]

1. <span data-ttu-id="e4860-283">Panoya geri gidin.</span><span class="sxs-lookup"><span data-stu-id="e4860-283">Navigate back to the dashboard.</span></span> <span data-ttu-id="e4860-284">Kısa bir süre sonra yeni cihazınız tarafından raporlanan sıcaklık 47 derece eşiğini aştığında **Uyarı Geçmişi** bölmesinde yeni bir giriş görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="e4860-284">After a short time, you will see a new entry in the **Alarm History** pane when the temperature reported by your new device exceeds the 47-degree threshold:</span></span>

    ![Cihaz kuralı ekleme][img-adddevicerule4]

1. <span data-ttu-id="e4860-286">Panonun **Kurallar** sayfasında tüm kurallarınızı gözden geçirebilir ve düzenleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e4860-286">You can review and edit all your rules on the **Rules** page of the dashboard:</span></span>

    ![Cihaz kurallarını listeleme][img-rules]

1. <span data-ttu-id="e4860-288">Panonun **Eylemler** sayfasında bir kurala yanıt olarak gerçekleştirilebilecek tüm eylemleri gözden geçirebilir ve düzenleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e4860-288">You can review and edit all the actions that can be taken in response to a rule on the **Actions** page of the dashboard:</span></span>

    ![Cihaz eylemlerini listeleme][img-actions]

> [!NOTE]
> <span data-ttu-id="e4860-290">Bir kurala yanıt olarak bir e-posta iletisi veya SMS gönderebilen veya bir [Mantıksal Uygulama][lnk-logic-apps] aracılığıyla bir iş kolu sistemiyle tümleştirilebilen eylemler tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e4860-290">It is possible to define actions that can send an email message or SMS in response to a rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="e4860-291">Daha fazla bilgi için bkz. [Mantıksal Uygulamanızı önceden yapılandırılmış Azure IoT Paketi Uzaktan İzleme çözümüne bağlama][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="e4860-291">For more information, see the [Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="e4860-292">Filtreleri yönetme</span><span class="sxs-lookup"><span data-stu-id="e4860-292">Manage filters</span></span>

<span data-ttu-id="e4860-293">Cihaz listesinde, hub’ınıza bağlı cihazların özelleştirilmiş bir listesini görüntülemek üzere filtreler oluşturabilir, kaydedebilir ve yeniden yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-293">In the device list, you can create, save, and reload filters to display a customized list of devices connected to your hub.</span></span> <span data-ttu-id="e4860-294">Bir filtre oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="e4860-294">To create a filter:</span></span>

1. <span data-ttu-id="e4860-295">Cihaz listesinin üzerindeki filtre düzenleme simgesini seçin:</span><span class="sxs-lookup"><span data-stu-id="e4860-295">Choose the edit filter icon above the list of devices:</span></span>

    ![Filtre düzenleyicisini açın][img-editfiltericon]

1. <span data-ttu-id="e4860-297">**Filtre düzenleyicisi**’nde cihaz listesini filtrelemek için alan, işleç ve değerler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e4860-297">In the **Filter editor**, add the fields, operators, and values to filter the device list.</span></span> <span data-ttu-id="e4860-298">Filtrenizi daraltmak için birden fazla yan tümce ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-298">You can add multiple clauses to refine your filter.</span></span> <span data-ttu-id="e4860-299">Filtreyi uygulamak için **Filtre**’ye tıklayın:</span><span class="sxs-lookup"><span data-stu-id="e4860-299">Choose **Filter** to apply the filter:</span></span>

    ![Filtre oluşturma][img-filtereditor]

1. <span data-ttu-id="e4860-301">Bu örnekte liste, üreticiye ve model numarasına göre filtrelenmiştir:</span><span class="sxs-lookup"><span data-stu-id="e4860-301">In this example, the list is filtered by manufacturer and model number:</span></span>

    ![Filtrelenmiş liste][img-filterelist]

1. <span data-ttu-id="e4860-303">Filtrenizi özel bir adla kaydetmek için **Farklı kaydet** simgesini seçin:</span><span class="sxs-lookup"><span data-stu-id="e4860-303">To save your filter with a custom name, choose the **Save as** icon:</span></span>

    ![Filtre kaydetme][img-savefilter]

1. <span data-ttu-id="e4860-305">Daha önce kaydettiğiniz bir filtreyi yeniden uygulamak için **Kaydedilmiş filtreyi aç** simgesini seçin:</span><span class="sxs-lookup"><span data-stu-id="e4860-305">To reapply a filter you saved previously, choose the **Open saved filter** icon:</span></span>

    ![Filtre açma][img-openfilter]

<span data-ttu-id="e4860-307">Cihaz kimliği, cihaz durumu, istenen özellikler, bildirilen özellikler ve etiketlere göre filtreler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="e4860-308">Bir cihaza kendi özel etiketlerinizi **Cihaz Ayrıntıları** panelinin **Etiketler** bölümünden ekleyebilir veya birden fazla cihazda etiketleri güncelleştirmek için bir iş çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-308">You add your own custom tags to a device in the **Tags** section of the **Device Details** panel, or run a job to update tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="e4860-309">**Filtre düzenleyicisi**’nde **Gelişmiş görünüm**’ü kullanarak sorgu metnini doğrudan düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-309">In the **Filter editor**, you can use the **Advanced view** to edit the query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="e4860-310">Komutlar</span><span class="sxs-lookup"><span data-stu-id="e4860-310">Commands</span></span>

<span data-ttu-id="e4860-311">**Cihaz Ayrıntıları** panelinden cihaza komut gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-311">From the **Device Details** panel, you can send commands to the device.</span></span> <span data-ttu-id="e4860-312">Bir cihaz ilk kez başlatıldığında, desteklediği komutlar hakkında çözüme bilgi gönderir.</span><span class="sxs-lookup"><span data-stu-id="e4860-312">When a device first starts, it sends information about the commands it supports to the solution.</span></span> <span data-ttu-id="e4860-313">Komutlar ve metotlar arasındaki farklar için bkz. [Azure IoT Hub buluttan cihaza seçenekleri][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="e4860-313">For a discussion of the differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="e4860-314">Seçilen cihaz için **Cihaz Ayrıntıları** bölmesinde **Komutlar**’ı seçin:</span><span class="sxs-lookup"><span data-stu-id="e4860-314">Choose **Commands** in the **Device Details** panel for the selected device:</span></span>

   ![Panoda cihaz komutları][img-devicecommands]

1. <span data-ttu-id="e4860-316">Komut listesinden **PingDevice**'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-316">Select **PingDevice** from the command list.</span></span>

1. <span data-ttu-id="e4860-317">**Komut Gönder**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="e4860-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="e4860-318">Komutun durumunu komut geçmişinde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-318">You can see the status of the command in the command history.</span></span>

   ![Panoda komut durumu][img-pingcommand]

<span data-ttu-id="e4860-320">Çözüm, gönderdiği her bir komutun durumunu takip eder.</span><span class="sxs-lookup"><span data-stu-id="e4860-320">The solution tracks the status of each command it sends.</span></span> <span data-ttu-id="e4860-321">Sonuç başlangıçta **Beklemede**'dir.</span><span class="sxs-lookup"><span data-stu-id="e4860-321">Initially the result is **Pending**.</span></span> <span data-ttu-id="e4860-322">Cihaz komutu yürüttüğünü raporladığında, sonuç **Başarılı** olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="e4860-322">When the device reports that it has executed the command, the result is set to **Success**.</span></span>

## <a name="behind-the-scenes"></a><span data-ttu-id="e4860-323">Arka planda</span><span class="sxs-lookup"><span data-stu-id="e4860-323">Behind the scenes</span></span>

<span data-ttu-id="e4860-324">Önceden yapılandırılmış bir çözümü dağıttığınızda, dağıtım işlemi seçtiğiniz Azure aboneliğinde birden çok kaynak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e4860-324">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="e4860-325">Bu kaynakları Azure [portalında][lnk-portal] görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-325">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="e4860-326">Dağıtım işlemi, önceden yapılandırılmış çözümünüz için seçtiğiniz adı temel alan bir ada sahip bir **kaynak grubu** oluşturur:</span><span class="sxs-lookup"><span data-stu-id="e4860-326">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Azure portalında önceden yapılandırılmış çözüm][img-portal]

<span data-ttu-id="e4860-328">Her bir kaynağın ayarlarını, kaynak grubundaki kaynaklar listesinde seçerek görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-328">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="e4860-329">Önceden yapılandırılmış çözüm için kaynak kodunu da görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-329">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="e4860-330">Önceden yapılandırılmış uzaktan izleme çözümünün kaynak kodu [azure-iot-remote-monitoring][lnk-rmgithub] GitHub deposundadır:</span><span class="sxs-lookup"><span data-stu-id="e4860-330">The remote monitoring preconfigured solution source code is in the [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="e4860-331">**DeviceAdministration** klasörü, pano için kaynak kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="e4860-331">The **DeviceAdministration** folder contains the source code for the dashboard.</span></span>
* <span data-ttu-id="e4860-332">**Simulator** klasörü, sanal cihaz için kaynak kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="e4860-332">The **Simulator** folder contains the source code for the simulated device.</span></span>
* <span data-ttu-id="e4860-333">**EventProcessor** klasörü, gelen telemetriyi işleyen arka uç işleme için kaynak kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="e4860-333">The **EventProcessor** folder contains the source code for the back-end process that handles the incoming telemetry.</span></span>

<span data-ttu-id="e4860-334">İşiniz bittiğinde önceden yapılandırılmış çözümü [azureiotsuite.com][lnk-azureiotsuite] sitesindeki Azure aboneliğinizden silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e4860-334">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="e4860-335">Bu site, önceden yapılandırılmış çözümü oluşturduğunuzda sağlanan tüm kaynakları kolayca silmenize imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="e4860-335">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="e4860-336">Önceden yapılandırılmış çözümle ilgili her şeyi sildiğinizden emin olmak için bu öğeleri [azureiotsuite.com][lnk-azureiotsuite] sitesinde silin; kaynak grubunu portaldan silmeyin.</span><span class="sxs-lookup"><span data-stu-id="e4860-336">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site and do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4860-337">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e4860-337">Next Steps</span></span>

<span data-ttu-id="e4860-338">Çalışan bir önceden yapılandırılmış çözüm dağıttığınıza göre aşağıdaki makaleleri okuyarak IoT Paketi ile çalışmaya başlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e4860-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="e4860-339">[Uzaktan izleme önceden yapılandırılmış çözüm kılavuzu][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="e4860-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="e4860-340">[Cihazınızı önceden yapılandırılmış uzaktan izleme çözümüne bağlama][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="e4860-340">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="e4860-341">[azureiotsuite.com sitesindeki izinler][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="e4860-341">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

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