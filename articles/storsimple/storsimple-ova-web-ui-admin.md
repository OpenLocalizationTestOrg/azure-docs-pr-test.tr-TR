---
title: "aaaStorSimple sanal dizinin web kullanıcı Arabirimi Yönetim | Microsoft Docs"
description: "Merhaba StorSimple sanal dizinin web kullanıcı Arabirimi nasıl tooperform temel aygıt yönetim görevleri açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: ea65b4c7-a478-43e6-83df-1d9ea62916a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 12/1/2016
ms.author: alkohli
ms.openlocfilehash: 31a20a587c4302231f027fcf772a50df33b23407
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-web-ui-tooadminister-your-storsimple-virtual-array"></a><span data-ttu-id="f2327-103">StorSimple sanal dizinizi Hello Web kullanıcı arabirimini tooadminister kullanın</span><span class="sxs-lookup"><span data-stu-id="f2327-103">Use hello Web UI tooadminister your StorSimple Virtual Array</span></span>
![Kurulum işlem akışı](./media/storsimple-ova-web-ui-admin/manage4.png)

## <a name="overview"></a><span data-ttu-id="f2327-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f2327-105">Overview</span></span>
<span data-ttu-id="f2327-106">Bu makalede Hello öğreticileri toohello Microsoft Azure StorSimple sanal dizinin (olarak da bilinen hello StorSimple şirket içi sanal cihaz) çalışan Mart 2016 genel kullanılabilirlik (GA) sürümü geçerli.</span><span class="sxs-lookup"><span data-stu-id="f2327-106">hello tutorials in this article apply toohello Microsoft Azure StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device) running March 2016 general availability (GA) release.</span></span> <span data-ttu-id="f2327-107">Bu makalede hello karmaşık iş akışları ve StorSimple sanal dizinin hello üzerinde gerçekleştirilen yönetim görevlerini bazıları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f2327-107">This article describes some of hello complex workflows and management tasks that can be performed on hello StorSimple Virtual Array.</span></span> <span data-ttu-id="f2327-108">Yönetebileceğiniz StorSimple sanal hello StorSimple Yöneticisi hizmeti kullanıcı Arabirimi (başvurulan tooas hello portal UI) kullanarak dizi hello ve hello cihaz için yerel web kullanıcı Arabirimi hello.</span><span class="sxs-lookup"><span data-stu-id="f2327-108">You can manage hello StorSimple Virtual Array using hello StorSimple Manager service UI (referred tooas hello portal UI) and hello local web UI for hello device.</span></span> <span data-ttu-id="f2327-109">Bu makalede, hello web kullanıcı arabirimini kullanarak gerçekleştirebilirsiniz hello görevlerde odaklanır.</span><span class="sxs-lookup"><span data-stu-id="f2327-109">This article focuses on hello tasks that you can perform using hello web UI.</span></span>

<span data-ttu-id="f2327-110">Bu makalede öğreticileri aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="f2327-110">This article includes hello following tutorials:</span></span>

* <span data-ttu-id="f2327-111">Merhaba hizmet verileri şifreleme anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="f2327-111">Get hello service data encryption key</span></span>
* <span data-ttu-id="f2327-112">Web kullanıcı Arabirimi Kurulum hatalarında sorun giderme</span><span class="sxs-lookup"><span data-stu-id="f2327-112">Troubleshoot web UI setup errors</span></span>
* <span data-ttu-id="f2327-113">Bir günlük paketi oluştur</span><span class="sxs-lookup"><span data-stu-id="f2327-113">Generate a log package</span></span>
* <span data-ttu-id="f2327-114">Kapatıldı veya aygıtınızı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="f2327-114">Shut down or restart your device</span></span>

## <a name="get-hello-service-data-encryption-key"></a><span data-ttu-id="f2327-115">Merhaba hizmet verileri şifreleme anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="f2327-115">Get hello service data encryption key</span></span>
<span data-ttu-id="f2327-116">StorSimple Yöneticisi hizmeti hello ile ilk Cihazınızı kaydederken bir hizmet verileri şifreleme anahtarı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f2327-116">A service data encryption key is generated when you register your first device with hello StorSimple Manager service.</span></span> <span data-ttu-id="f2327-117">Bu anahtarı ise hello hizmet kayıt anahtarı tooregister ek aygıtlarla hello StorSimple Yöneticisi hizmeti ile gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f2327-117">This key is then required with hello service registration key tooregister additional devices with hello StorSimple Manager service.</span></span>

<span data-ttu-id="f2327-118">Hizmet verileri şifreleme anahtarı yanlış ve tooretrieve gerekir, hello aşağıdakileri gerçekleştirmek hello yerel web kullanıcı Arabirimi hello cihazın adımlarda hizmetiniz ile kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="f2327-118">If you have misplaced your service data encryption key and need tooretrieve it, perform hello following steps in hello local web UI of hello device registered with your service.</span></span>

#### <a name="tooget-hello-service-data-encryption-key"></a><span data-ttu-id="f2327-119">tooget hello hizmet verileri şifreleme anahtarı</span><span class="sxs-lookup"><span data-stu-id="f2327-119">tooget hello service data encryption key</span></span>
1. <span data-ttu-id="f2327-120">Toohello yerel web kullanıcı Arabirimi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f2327-120">Connect toohello local web UI.</span></span> <span data-ttu-id="f2327-121">Çok Git**yapılandırma** > **bulut ayarları**.</span><span class="sxs-lookup"><span data-stu-id="f2327-121">Go too**Configuration** > **Cloud Settings**.</span></span>
2. <span data-ttu-id="f2327-122">Merhaba sayfasının Hello altında tıklatın **Get hizmet verileri şifreleme anahtarı**.</span><span class="sxs-lookup"><span data-stu-id="f2327-122">At hello bottom of hello page, click **Get service data encryption key**.</span></span> <span data-ttu-id="f2327-123">Bir anahtarı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f2327-123">A key will appear.</span></span> <span data-ttu-id="f2327-124">Kopyalayın ve bu anahtar kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f2327-124">Copy and save this key.</span></span>
   
    ![Hizmet verileri şifreleme anahtarı 1 alma](./media/storsimple-ova-web-ui-admin/image27.png)

## <a name="troubleshoot-web-ui-setup-errors"></a><span data-ttu-id="f2327-126">Web kullanıcı Arabirimi Kurulum hatalarında sorun giderme</span><span class="sxs-lookup"><span data-stu-id="f2327-126">Troubleshoot web UI setup errors</span></span>
<span data-ttu-id="f2327-127">Bazı durumlarda hello aygıtı hello yerel web kullanıcı Arabirimi aracılığıyla yapılandırdığınızda hatalarla karşılaşırsanız çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2327-127">In some instances when you configure hello device through hello local web UI, you might run into errors.</span></span> <span data-ttu-id="f2327-128">toodiagnose ve bu tür hatalarında sorun giderme, hello tanılama testleri çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2327-128">toodiagnose and troubleshoot such errors, you can run hello diagnostics tests.</span></span>

#### <a name="toorun-hello-diagnostic-tests"></a><span data-ttu-id="f2327-129">toorun hello tanılama testleri</span><span class="sxs-lookup"><span data-stu-id="f2327-129">toorun hello diagnostic tests</span></span>
1. <span data-ttu-id="f2327-130">Merhaba yerel web kullanıcı Arabirimi, çok Git**sorun giderme** > **tanılama testleri**.</span><span class="sxs-lookup"><span data-stu-id="f2327-130">In hello local web UI, go too**Troubleshooting** > **Diagnostic tests**.</span></span>
   
    ![Tanılama'yı 1 çalıştırın](./media/storsimple-ova-web-ui-admin/image29.png)
2. <span data-ttu-id="f2327-132">Merhaba sayfasının Hello altında tıklatın **tanılama Testleri Çalıştır**.</span><span class="sxs-lookup"><span data-stu-id="f2327-132">At hello bottom of hello page, click **Run Diagnostic Tests**.</span></span> <span data-ttu-id="f2327-133">Bu ağ, aygıt, web proxy, saati veya Bulut ayarları ile ilgili tüm olası sorunları testleri toodiagnose başlatır.</span><span class="sxs-lookup"><span data-stu-id="f2327-133">This will initiate tests toodiagnose any possible issues with your network, device, web proxy, time, or cloud settings.</span></span> <span data-ttu-id="f2327-134">Merhaba aygıt testleri çalıştırma bildirilir.</span><span class="sxs-lookup"><span data-stu-id="f2327-134">You will be notified that hello device is running tests.</span></span>
3. <span data-ttu-id="f2327-135">Merhaba testleri tamamladıktan sonra hello sonuçları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f2327-135">After hello tests have completed, hello results will be displayed.</span></span> <span data-ttu-id="f2327-136">Merhaba aşağıdaki örnek tanılama testleri hello sonuçlarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f2327-136">hello following example shows hello results of diagnostic tests.</span></span> <span data-ttu-id="f2327-137">Bu aygıtta Hello web proxy ayarları yapılandırılmadı ve bu nedenle, hello web proxy testi değil çalıştırıldığı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f2327-137">Note that hello web proxy settings were not configured on this device, and therefore, hello web proxy test was not run.</span></span> <span data-ttu-id="f2327-138">Tüm ağ ayarlarını, DNS sunucusu için diğer testleri hello ve saat ayarları başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="f2327-138">All hello other tests for network settings, DNS server, and time settings were successful.</span></span>
   
    ![Tanılama 2 çalıştırma](./media/storsimple-ova-web-ui-admin/image30.png)

## <a name="generate-a-log-package"></a><span data-ttu-id="f2327-140">Bir günlük paketi oluştur</span><span class="sxs-lookup"><span data-stu-id="f2327-140">Generate a log package</span></span>
<span data-ttu-id="f2327-141">Bir günlük paketi Microsoft Support cihaz sorunları gidermenize yardımcı olabilecek tüm hello ilgili günlüklerini oluşur.</span><span class="sxs-lookup"><span data-stu-id="f2327-141">A log package is comprised of all hello relevant logs that can assist Microsoft Support with troubleshooting any device issues.</span></span> <span data-ttu-id="f2327-142">Bu sürümde, bir günlük paket hello yerel web kullanıcı Arabirimi oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="f2327-142">In this release, a log package can be generated via hello local web UI.</span></span>

#### <a name="toogenerate-hello-log-package"></a><span data-ttu-id="f2327-143">toogenerate hello günlük paketi</span><span class="sxs-lookup"><span data-stu-id="f2327-143">toogenerate hello log package</span></span>
1. <span data-ttu-id="f2327-144">Merhaba yerel web kullanıcı Arabirimi, çok Git**sorun giderme** > **sistem günlüklerini**.</span><span class="sxs-lookup"><span data-stu-id="f2327-144">In hello local web UI, go too**Troubleshooting** > **System logs**.</span></span>
   
    ![Günlük Paketi 1 oluştur](./media/storsimple-ova-web-ui-admin/image31.png)
2. <span data-ttu-id="f2327-146">Merhaba sayfasının Hello altında tıklatın **günlük Paket Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="f2327-146">At hello bottom of hello page, click **Create log package**.</span></span> <span data-ttu-id="f2327-147">Merhaba sistem günlüklerini paketi oluşturulacak.</span><span class="sxs-lookup"><span data-stu-id="f2327-147">A package of hello system logs will be created.</span></span> <span data-ttu-id="f2327-148">Bu işlem birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="f2327-148">This will take a couple of minutes.</span></span>
   
    ![2 günlük paketi oluştur](./media/storsimple-ova-web-ui-admin/image32.png)
   
    <span data-ttu-id="f2327-150">Hello paketi başarıyla oluşturulduktan sonra hello sayfa tooindicate hello saat ve tarih hello paketinin oluşturulduğu güncelleştirilecektir bildirilir.</span><span class="sxs-lookup"><span data-stu-id="f2327-150">You will be notified after hello package is successfully created, and hello page will be updated tooindicate hello time and date when hello package was created.</span></span>
   
    ![3 günlük paketi oluştur](./media/storsimple-ova-web-ui-admin/image33.png)
3. <span data-ttu-id="f2327-152">Tıklatın **yükleme günlük paketini**.</span><span class="sxs-lookup"><span data-stu-id="f2327-152">Click **Download log package**.</span></span> <span data-ttu-id="f2327-153">Sıkıştırılmış paketi sisteminizde indirilir.</span><span class="sxs-lookup"><span data-stu-id="f2327-153">A zipped package will be downloaded on your system.</span></span>
   
    ![Günlük Paketi 4 oluştur](./media/storsimple-ova-web-ui-admin/image34.png)
4. <span data-ttu-id="f2327-155">Merhaba indirilen günlük paketin sıkıştırmasını açın ve hello sistem günlük dosyalarını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="f2327-155">You can unzip hello downloaded log package and view hello system log files.</span></span>

## <a name="shut-down-and-restart-your-device"></a><span data-ttu-id="f2327-156">Kapatılır ve aygıtınızı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="f2327-156">Shut down and restart your device</span></span>
<span data-ttu-id="f2327-157">Kapatıldı veya hello yerel web kullanıcı arabirimini kullanarak sanal Cihazınızı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="f2327-157">You can shut down or restart your virtual device using hello local web UI.</span></span> <span data-ttu-id="f2327-158">Yeniden başlatma, hello birimler veya paylaşımlar çevrimdışı hello konakta alın ve cihaz hello önce öneririz.</span><span class="sxs-lookup"><span data-stu-id="f2327-158">We recommend that before you restart, take hello volumes or shares offline on hello host and then hello device.</span></span> <span data-ttu-id="f2327-159">Bu veri bozulması olasılığını en aza indirgenecektir.</span><span class="sxs-lookup"><span data-stu-id="f2327-159">This will minimize any possibility of data corruption.</span></span> 

#### <a name="tooshut-down-your-virtual-device"></a><span data-ttu-id="f2327-160">Sanal cihazınız aşağı tooshut</span><span class="sxs-lookup"><span data-stu-id="f2327-160">tooshut down your virtual device</span></span>
1. <span data-ttu-id="f2327-161">Merhaba yerel web kullanıcı Arabirimi, çok Git**Bakım** > **güç ayarları**.</span><span class="sxs-lookup"><span data-stu-id="f2327-161">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="f2327-162">Merhaba sayfasının Hello altında tıklatın **kapatma**.</span><span class="sxs-lookup"><span data-stu-id="f2327-162">At hello bottom of hello page, click **Shutdown**.</span></span>
   
    ![cihaz kapatma 1](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="f2327-164">Bir kapanma hello cihazın kapalı kalma süresi ile elde edilen etmekte olan tüm g/ç kesintiye uğrar belirten bir uyarı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f2327-164">A warning will appear stating that a shutdown of hello device will interrupt any IO that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="f2327-165">Merhaba onay simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="f2327-165">Click hello check icon</span></span> ![onay simgesi](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="f2327-167">.</span><span class="sxs-lookup"><span data-stu-id="f2327-167">.</span></span>
   
    ![cihaz kapatma uyarı](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="f2327-169">Bu hello kapatma başlatılan bildirilir.</span><span class="sxs-lookup"><span data-stu-id="f2327-169">You will be notified that hello shutdown has been initiated.</span></span>
   
    ![cihaz kapatma başlatıldı](./media/storsimple-ova-web-ui-admin/image38.png)
   
    <span data-ttu-id="f2327-171">Merhaba cihaz şimdi kapanacak.</span><span class="sxs-lookup"><span data-stu-id="f2327-171">hello device will now shut down.</span></span> <span data-ttu-id="f2327-172">Cihazınızı toostart istiyorsanız, Hyper-V Yöneticisi'ni hello aracılığıyla toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="f2327-172">If you want toostart your device, you will need toodo that through hello Hyper-V Manager.</span></span>

#### <a name="toorestart-your-virtual-device"></a><span data-ttu-id="f2327-173">toorestart sanal Cihazınızı</span><span class="sxs-lookup"><span data-stu-id="f2327-173">toorestart your virtual device</span></span>
1. <span data-ttu-id="f2327-174">Merhaba yerel web kullanıcı Arabirimi, çok Git**Bakım** > **güç ayarları**.</span><span class="sxs-lookup"><span data-stu-id="f2327-174">In hello local web UI, go too**Maintenance** > **Power settings**.</span></span>
2. <span data-ttu-id="f2327-175">Merhaba sayfasının Hello altında tıklatın **yeniden**.</span><span class="sxs-lookup"><span data-stu-id="f2327-175">At hello bottom of hello page, click **Restart**.</span></span>
   
    ![Aygıt yeniden başlatma](./media/storsimple-ova-web-ui-admin/image36.png)
3. <span data-ttu-id="f2327-177">Bu yeniden başlatmayı hello aygıt kapalı kalma süresi ile elde edilen etmekte olan tüm IOs kesintiye uğrar bildiren bir uyarı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f2327-177">A warning will appear stating that restarting hello device will interrupt any IOs that were in progress, resulting in a downtime.</span></span> <span data-ttu-id="f2327-178">Merhaba onay simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="f2327-178">Click hello check icon</span></span> ![onay simgesi](./media/storsimple-ova-web-ui-admin/image3.png)<span data-ttu-id="f2327-180">.</span><span class="sxs-lookup"><span data-stu-id="f2327-180">.</span></span>
   
    ![Uyarı yeniden başlatın](./media/storsimple-ova-web-ui-admin/image37.png)
   
    <span data-ttu-id="f2327-182">Bu hello yeniden başlatma bildirilir.</span><span class="sxs-lookup"><span data-stu-id="f2327-182">You will be notified that hello restart has been initiated.</span></span>
   
    ![başlatılan yeniden başlatma](./media/storsimple-ova-web-ui-admin/image39.png)
   
    <span data-ttu-id="f2327-184">Merhaba yeniden başlatma işlemi devam ederken, hello bağlantı toohello UI kaybedersiniz.</span><span class="sxs-lookup"><span data-stu-id="f2327-184">While hello restart is in progress, you will lose hello connection toohello UI.</span></span> <span data-ttu-id="f2327-185">Merhaba kullanıcı arabirimini düzenli aralıklarla yenileyerek hello yeniden izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2327-185">You can monitor hello restart by refreshing hello UI periodically.</span></span> <span data-ttu-id="f2327-186">Alternatif olarak, Hyper-V Yöneticisi'ni hello aracılığıyla hello aygıt yeniden başlatma durumunu izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2327-186">Alternatively, you can monitor hello device restart status through hello Hyper-V Manager.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2327-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f2327-187">Next steps</span></span>
<span data-ttu-id="f2327-188">Nasıl çok öğrenin[kullanım Cihazınızı StorSimple Yöneticisi hizmet toomanage hello](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f2327-188">Learn how too[use hello StorSimple Manager service toomanage your device](storsimple-virtual-array-manager-service-administration.md).</span></span>

