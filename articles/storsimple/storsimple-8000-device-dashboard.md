---
title: "aaaUse StorSimple 8000 serisi aygıt Özet | Microsoft Docs"
description: "Merhaba StorSimple cihaz Yöneticisi Hizmeti aygıt Özet açıklar ve nasıl toouse, tooview storage ölçümleri ve bağlı başlatıcıları ve Bul hello seri numarasını ve IQN."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: b45ffc6ec52ebb6549c25a00c68c62460b208b7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-in-storsimple-device-manager-service"></a><span data-ttu-id="f30b1-103">Merhaba cihaz StorSimple Aygıt Yöneticisi'ni hizmetinde Özet kullanın</span><span class="sxs-lookup"><span data-stu-id="f30b1-103">Use hello device summary in StorSimple Device Manager service</span></span>

## <a name="overview"></a><span data-ttu-id="f30b1-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f30b1-104">Overview</span></span>
<span data-ttu-id="f30b1-105">Merhaba StorSimple cihaz Özet dikey bilgi belirli bir StorSimple cihazı için genel bir bakış sunar, buna karşılık toohello servis Özet dikey, Microsoft Azure StorSimple çözümünüzde dahil tüm hello cihazlar hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="f30b1-105">hello StorSimple device summary blade gives you an overview of information for a specific StorSimple device, in contrast toohello service summary blade, which gives you information about all hello devices included in your Microsoft Azure StorSimple solution.</span></span>

<span data-ttu-id="f30b1-106">Merhaba aygıt Özet dikey pencere, sistem yöneticisinin dikkat etmeniz gereken bu cihaz sorunları vurgulayan ile belirli bir StorSimple Aygıt Yöneticisi, kayıtlı bir StorSimple 8000 serisi aygıt Özet görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="f30b1-106">hello device summary blade provides a summary view of a StorSimple 8000 series device that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="f30b1-107">Bu öğretici hello aygıt Özet dikey tanıtır, hello içerik ve işlevi açıklanmaktadır ve bu dikey pencereden gerçekleştirebileceğiniz hello görevleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="f30b1-107">This tutorial introduces hello device summary blade, explains hello content and function, and describes hello tasks that you can perform from this blade.</span></span>

<span data-ttu-id="f30b1-108">Merhaba aygıt Özet dikey penceresinde aşağıdaki bilgilerle hello görüntüler:</span><span class="sxs-lookup"><span data-stu-id="f30b1-108">hello device summary blade displays hello following information:</span></span>

![Cihaz Özet dikey penceresi](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a><span data-ttu-id="f30b1-110">Yönetim Komut çubuğu</span><span class="sxs-lookup"><span data-stu-id="f30b1-110">Management command bar</span></span>

<span data-ttu-id="f30b1-111">Merhaba StorSimple cihaz dikey penceresinde hello seçenekleri StorSimple Cihazınızı yönetmek için bkz.</span><span class="sxs-lookup"><span data-stu-id="f30b1-111">In hello StorSimple device blade, you see hello options for managing your StorSimple device.</span></span> <span data-ttu-id="f30b1-112">Merhaba üstte hello dikey ve hello sol tarafında hello yönetimi komutları bakın.</span><span class="sxs-lookup"><span data-stu-id="f30b1-112">You see hello management commands across hello top of hello blade and on hello left side.</span></span> <span data-ttu-id="f30b1-113">Bu seçenekler tooadd paylaşımları veya birimler kullanmak, güncelleştirme veya Cihazınızı başarısız.</span><span class="sxs-lookup"><span data-stu-id="f30b1-113">Use these options tooadd shares or volumes, or update or fail over your device.</span></span>

![Yönetim Komut çubuğu](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a><span data-ttu-id="f30b1-115">Temel Bileşenler</span><span class="sxs-lookup"><span data-stu-id="f30b1-115">Essentials</span></span>

<span data-ttu-id="f30b1-116">Merhaba essentials alanı bazı hello önemli özellikler gibi hello durumu, model, hedef IQN ve hello yazılım sürümü yakalar.</span><span class="sxs-lookup"><span data-stu-id="f30b1-116">hello essentials area captures some of hello important properties such as, hello status, model, target IQN, and hello software version.</span></span> 

![Cihaz temelleri](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a><span data-ttu-id="f30b1-118">İzleme</span><span class="sxs-lookup"><span data-stu-id="f30b1-118">Monitoring</span></span>

* <span data-ttu-id="f30b1-119">Merhaba **uyarıları** kutucuğu uyarı önem derecesine göre gruplandırılmış cihazınız için bir anlık görüntüsünü tüm hello etkin uyarıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="f30b1-119">hello **Alerts** tile provides a snapshot of all hello active alerts for your device, grouped by alert severity.</span></span>

    ![Uyarı döşeme](./media/storsimple-8000-device-dashboard/device-summary4.png)

    <span data-ttu-id="f30b1-121">Merhaba döşeme tooopen hello tıklatın **uyarıları** dikey ve ardından tek bir uyarı tooview ek herhangi dahil olmak üzere Bu uyarıyla ilgili ayrıntılar önerilen eylemler.</span><span class="sxs-lookup"><span data-stu-id="f30b1-121">Click hello tile tooopen hello **Alerts** blade and then click an individual alert tooview additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="f30b1-122">Merhaba sorunu çözerseniz hello uyarı işaretini kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f30b1-122">You can also clear hello alert if hello issue has been resolved.</span></span>

    ![Uyarı kutucuğa tıklayın](./media/storsimple-8000-device-dashboard/device-summary10.png)

* <span data-ttu-id="f30b1-124">Merhaba **durumunu** kutucuğu hello Aygıt durumu da dahil olmak üzere bir aygıt için hello donanım bileşen durumu fikir sağlar.</span><span class="sxs-lookup"><span data-stu-id="f30b1-124">hello **Status and health** tile provides insights into hello hardware component health for a device including hello device status.</span></span> <span data-ttu-id="f30b1-125">Merhaba Aygıt durumu yukarı çevrimdışı, çevrimiçi, devre dışı bırakılmış veya hazır tooset olabilir.</span><span class="sxs-lookup"><span data-stu-id="f30b1-125">hello device status may be offline, online, deactivated, or ready tooset up.</span></span>

    ![Durum ve sistem durumu kutucuğu](./media/storsimple-8000-device-dashboard/device-summary5.png)

* <span data-ttu-id="f30b1-127">Merhaba **birimleri** kutucuğu duruma göre gruplanmış Cihazınızı birimlerinde hello sayısı özetini sağlar.</span><span class="sxs-lookup"><span data-stu-id="f30b1-127">hello **Volumes** tile provides a summary of hello number of volumes in your device grouped by status.</span></span>

    ![Birimler kutucuğunu](./media/storsimple-8000-device-dashboard/device-summary6.png)

    <span data-ttu-id="f30b1-129">Merhaba döşeme tooopen hello tıklatın **birimleri** listesi dikey penceresinde, bir tek tek birim tooview'ı tıklatın veya özelliklerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f30b1-129">Click hello tile tooopen hello **Volumes** list blade, and then click on an individual volume tooview or modify its properties.</span></span>
    
    ![Birimler kutucuğunu tıklatın](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    <span data-ttu-id="f30b1-131">Daha fazla bilgi için bkz. nasıl çok[birimleri yönetme](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="f30b1-131">For more information, see how too[manage volumes](storsimple-8000-manage-volumes-u2.md).</span></span>

* <span data-ttu-id="f30b1-132">Merhaba, **kullanım** grafiği, cihaz ve son 7 gün, hello varsayılan süre hello tüketilen hello bulut depolama kullanılan hello birincil depolama görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f30b1-132">In hello **Usage** chart, you can view hello primary storage used across your device, and hello cloud storage consumed over hello past 7 days, hello default time period.</span></span>

     ![Kullanımı kutucuğu](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     <span data-ttu-id="f30b1-134">toochoose farklı zaman ölçeği kullanmak hello **Düzenle** hello grafik hello sağ üst köşedeki seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f30b1-134">toochoose a different time scale, use hello **Edit** option in hello top-right corner of hello chart.</span></span>

     ![Kullanım grafiği Düzenle](./media/storsimple-8000-device-dashboard/device-summary12.png)

     <span data-ttu-id="f30b1-136">Bu grafikte görüntülemek hello toplam birincil depolama (ana bilgisayar tooyour aygıt tarafından yazılan veri miktarı hello) için Ölçümler ve toplam hello bulut bir süre boyunca cihazınız tarafından tüketilen depolama.</span><span class="sxs-lookup"><span data-stu-id="f30b1-136">In this chart, you can view metrics for hello total primary storage (hello amount of data written by hosts tooyour device) and hello total cloud storage consumed by your device over a period of time.</span></span>
  
     <span data-ttu-id="f30b1-137">Bu bağlamda *birincil depolama* toohello toplam hello ana bilgisayar tarafından yazılan veri miktarını gösterir ve birim türüne göre ayrılabilir: *birincil katmanlı depolama* her ikisini de içeren yerel olarak depolanan verileri ve verileri Katmanlı toohello bulut.</span><span class="sxs-lookup"><span data-stu-id="f30b1-137">In this context, *primary storage* refers toohello total amount of data written by hello host, and can be broken down by volume type: *primary tiered storage* includes both locally stored data and data tiered toohello cloud.</span></span> <span data-ttu-id="f30b1-138">*Birincil yerel olarak sabitlenmiş depolama* yerel olarak depolanan yalnızca verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="f30b1-138">*Primary locally pinned storage* includes just data stored locally.</span></span> <span data-ttu-id="f30b1-139">*Bulut depolama*, üzerinde diğer yandan Merhaba, hello toplam hello bulutta depolanan veri miktarını ölçüsüdür.</span><span class="sxs-lookup"><span data-stu-id="f30b1-139">*Cloud storage*, on hello other hand, is a measurement of hello total amount of data stored in hello cloud.</span></span> <span data-ttu-id="f30b1-140">Bu depolama katmanlı veri ve yedeklemeler içerir.</span><span class="sxs-lookup"><span data-stu-id="f30b1-140">This storage includes tiered data and backups.</span></span> <span data-ttu-id="f30b1-141">Hello bulutta depolanan hello veri yinelenenleri kaldırılmış ve sıkıştırılmış ancak birincil depolama hello hello veri yinelenenleri kaldırılmış ve sıkıştırılmış önce kullanılan depolama alanı miktarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f30b1-141">hello data stored in hello cloud is deduplicated and compressed, whereas primary storage indicates hello amount of storage used before hello data is deduplicated and compressed.</span></span> <span data-ttu-id="f30b1-142">(Bu iki sayının tooget hello sıkıştırma oranı hakkında bir fikir karşılaştırabilirsiniz.) Hem birincil hem de için ve bulut depolama, gösterilen tutarlar yapılandırdığınız sıklığı izleme hello üzerinde dayalı hello.</span><span class="sxs-lookup"><span data-stu-id="f30b1-142">(You can compare these two numbers tooget an idea of hello compression rate.) For both primary and cloud storage, hello amounts shown are based on hello tracking frequency you configure.</span></span> <span data-ttu-id="f30b1-143">Bir hafta sıklığı seçerseniz, örneğin, daha sonra hello grafik veri her günü için hello önceki hafta gösterir.</span><span class="sxs-lookup"><span data-stu-id="f30b1-143">For example, if you choose a one week frequency, then hello chart shows data for each day in hello previous week.</span></span>

     <span data-ttu-id="f30b1-144">toosee hello süre, select hello tüketilen bulut depolama alanı miktarını **bulut depolama kullanılan** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="f30b1-144">toosee hello amount of cloud storage consumed over time, select hello **CLOUD STORAGE USED** option.</span></span> <span data-ttu-id="f30b1-145">select hello hello konak tarafından yazılmış toosee hello toplam depolama **birincil KATMANLI depolama kullanılan** ve **birincil yerel olarak SABİTLENMİŞ depolama kullanılan** seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="f30b1-145">toosee hello total storage that has been written by hello host, select hello **PRIMARY TIERED STORAGE USED** and **PRIMARY LOCALLY PINNED STORAGE USED** options.</span></span> 
     <span data-ttu-id="f30b1-146">Daha fazla bilgi için bkz: [kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti toomonitor hello](storsimple-monitor-device.md).</span><span class="sxs-lookup"><span data-stu-id="f30b1-146">For more information, see [Use hello StorSimple Device Manager service toomonitor your StorSimple device](storsimple-monitor-device.md).</span></span>


* <span data-ttu-id="f30b1-147">Merhaba **kapasite** sağlanmış döşeme görüntüler hello birincil depolama ve hello aygıt göreli toohello toplam depolama alanı için kullanılabilir arasında kalan hello aynı.</span><span class="sxs-lookup"><span data-stu-id="f30b1-147">hello **Capacity** tile displays hello primary storage that is provisioned and remaining across hello device relative toohello total storage available for hello same.</span></span> <span data-ttu-id="f30b1-148">**Sağlanan** toohello hazırlanmış ve kullanım için ayrılan depolama alanı miktarını başvuruyor **kalan** bu cihaz sağlanan kapasite kalan toohello başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="f30b1-148">**Provisioned** refers toohello amount of storage that is prepared and allocated for use, **Remaining** refers toohello remaining capacity that can be provisioned across this device.</span></span> 

    ![Kullanımı kutucuğu](./media/storsimple-8000-device-dashboard/device-summary8.png)

    <span data-ttu-id="f30b1-150">Merhaba kapasite katmanlı ve yerel olarak sabitlenmiş birimleri arasında nasıl sağlandığında bu kutucuğu tooview'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f30b1-150">Click this tile tooview how hello capacity is provisioned across tiered and locally pinned volumes.</span></span> <span data-ttu-id="f30b1-151">Merhaba **kalan katmanlı** kapasitesi ise hello sırasında bulut dahil olmak üzere sağlanabilir hello kullanılabilir kapasite **kalan yerel** hello disklerde kalan hello kapasitesi toothis aygıt eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="f30b1-151">hello **Remaining Tiered** capacity is hello available capacity that can be provisioned including cloud, while hello **Remaining Local** is hello capacity remaining on hello disks attached toothis device.</span></span>

    ![Kullanım grafiği tıklatın](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a><span data-ttu-id="f30b1-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f30b1-153">Next steps</span></span>
* <span data-ttu-id="f30b1-154">Merhaba hakkında daha fazla bilgi [StorSimple hizmeti Özet dikey](storsimple-8000-service-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="f30b1-154">Learn more about hello [StorSimple service summary blade](storsimple-8000-service-dashboard.md).</span></span>
* <span data-ttu-id="f30b1-155">Daha fazla bilgi edinmek [StorSimple Cihazınızı hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanarak](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f30b1-155">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

