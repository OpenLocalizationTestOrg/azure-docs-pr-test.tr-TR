---
title: "StorSimple 8000 serisi aygıt kullanma Özet | Microsoft Docs"
description: "StorSimple cihaz Yöneticisi Hizmeti aygıt Özet ve storage ölçümleri ve bağlı başlatıcıları görüntüleyin ve seri numarasını ve IQN bulmak için kullanın açıklar."
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
ms.openlocfilehash: 784d3ce9d8f926b00ac1c6fbf48a05c0b04f900a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-device-summary-in-storsimple-device-manager-service"></a><span data-ttu-id="66c44-103">StorSimple Aygıt Yöneticisi'ni hizmetinde Özet aygıtı kullanma</span><span class="sxs-lookup"><span data-stu-id="66c44-103">Use the device summary in StorSimple Device Manager service</span></span>

## <a name="overview"></a><span data-ttu-id="66c44-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="66c44-104">Overview</span></span>
<span data-ttu-id="66c44-105">StorSimple cihaz Özet dikey bilgi Microsoft Azure StorSimple çözümünüzde dahil tüm cihazlar hakkında bilgi verir hizmeti Özet dikey aksine belirli bir StorSimple cihazı için genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="66c44-105">The StorSimple device summary blade gives you an overview of information for a specific StorSimple device, in contrast to the service summary blade, which gives you information about all the devices included in your Microsoft Azure StorSimple solution.</span></span>

<span data-ttu-id="66c44-106">Cihaz Özet dikey pencere, sistem yöneticisinin dikkat etmeniz gereken bu cihaz sorunları vurgulayan ile belirli bir StorSimple Aygıt Yöneticisi, kayıtlı bir StorSimple 8000 serisi aygıt Özet görünümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="66c44-106">The device summary blade provides a summary view of a StorSimple 8000 series device that is registered with a given StorSimple Device Manager, highlighting those device issues that need a system administrator's attention.</span></span> <span data-ttu-id="66c44-107">Bu öğretici aygıt Özet dikey tanıtır, içerik ve işlevi açıklanmaktadır ve bu dikey pencereden gerçekleştirebileceğiniz görevleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="66c44-107">This tutorial introduces the device summary blade, explains the content and function, and describes the tasks that you can perform from this blade.</span></span>

<span data-ttu-id="66c44-108">Cihaz Özet dikey penceresinde aşağıdaki bilgileri görüntüler:</span><span class="sxs-lookup"><span data-stu-id="66c44-108">The device summary blade displays the following information:</span></span>

![Cihaz Özet dikey penceresi](./media/storsimple-8000-device-dashboard/device-summary1.png)

## <a name="management-command-bar"></a><span data-ttu-id="66c44-110">Yönetim Komut çubuğu</span><span class="sxs-lookup"><span data-stu-id="66c44-110">Management command bar</span></span>

<span data-ttu-id="66c44-111">StorSimple cihaz dikey penceresinde, StorSimple Cihazınızı yönetmek için seçenekler bakın.</span><span class="sxs-lookup"><span data-stu-id="66c44-111">In the StorSimple device blade, you see the options for managing your StorSimple device.</span></span> <span data-ttu-id="66c44-112">Dikey ve sol tarafındaki üstte yönetimi komutları bakın.</span><span class="sxs-lookup"><span data-stu-id="66c44-112">You see the management commands across the top of the blade and on the left side.</span></span> <span data-ttu-id="66c44-113">Paylaşımlar veya birimler eklemek veya güncelleştirmek veya Cihazınızı başarısız için bu seçenekleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="66c44-113">Use these options to add shares or volumes, or update or fail over your device.</span></span>

![Yönetim Komut çubuğu](./media/storsimple-8000-device-dashboard/device-summary2.png)

## <a name="essentials"></a><span data-ttu-id="66c44-115">Temel Bileşenler</span><span class="sxs-lookup"><span data-stu-id="66c44-115">Essentials</span></span>

<span data-ttu-id="66c44-116">Temel alan bazı gibi önemli özellikleri, durumu, model, hedef IQN ve yazılım sürümü yakalar.</span><span class="sxs-lookup"><span data-stu-id="66c44-116">The essentials area captures some of the important properties such as, the status, model, target IQN, and the software version.</span></span> 

![Cihaz temelleri](./media/storsimple-8000-device-dashboard/device-summary3.png)

## <a name="monitoring"></a><span data-ttu-id="66c44-118">İzleme</span><span class="sxs-lookup"><span data-stu-id="66c44-118">Monitoring</span></span>

* <span data-ttu-id="66c44-119">**Uyarıları** kutucuğu uyarı önem derecesine göre gruplandırılmış cihazınız için bir anlık görüntüsünü tüm etkin uyarıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="66c44-119">The **Alerts** tile provides a snapshot of all the active alerts for your device, grouped by alert severity.</span></span>

    ![Uyarı döşeme](./media/storsimple-8000-device-dashboard/device-summary4.png)

    <span data-ttu-id="66c44-121">Açmak için kutucuğa tıklayın **uyarıları** dikey ve ardından herhangi dahil olmak üzere, bu uyarı hakkında ek ayrıntıları görüntülemek için bir bireysel uyarı önerilen eylemler.</span><span class="sxs-lookup"><span data-stu-id="66c44-121">Click the tile to open the **Alerts** blade and then click an individual alert to view additional details about that alert, including any recommended actions.</span></span> <span data-ttu-id="66c44-122">Sorunu çözerseniz uyarı işaretini kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66c44-122">You can also clear the alert if the issue has been resolved.</span></span>

    ![Uyarı kutucuğa tıklayın](./media/storsimple-8000-device-dashboard/device-summary10.png)

* <span data-ttu-id="66c44-124">**Durumunu** kutucuğu Aygıt durumu da dahil olmak üzere bir aygıt için donanım bileşen durumu fikir sağlar.</span><span class="sxs-lookup"><span data-stu-id="66c44-124">The **Status and health** tile provides insights into the hardware component health for a device including the device status.</span></span> <span data-ttu-id="66c44-125">Cihaz durumu, çevrimdışı, çevrimiçi, devre dışı bırakılmış veya ayarlamak hazır olması olabilir.</span><span class="sxs-lookup"><span data-stu-id="66c44-125">The device status may be offline, online, deactivated, or ready to set up.</span></span>

    ![Durum ve sistem durumu kutucuğu](./media/storsimple-8000-device-dashboard/device-summary5.png)

* <span data-ttu-id="66c44-127">**Birimleri** kutucuğu duruma göre gruplanmış Cihazınızı birimlerin sayısı özetini sağlar.</span><span class="sxs-lookup"><span data-stu-id="66c44-127">The **Volumes** tile provides a summary of the number of volumes in your device grouped by status.</span></span>

    ![Birimler kutucuğunu](./media/storsimple-8000-device-dashboard/device-summary6.png)

    <span data-ttu-id="66c44-129">Açmak için kutucuğa tıklayın **birimleri** listesinde dikey ve onun özelliklerini görüntülemek veya değiştirmek için tek bir birimde'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="66c44-129">Click the tile to open the **Volumes** list blade, and then click on an individual volume to view or modify its properties.</span></span>
    
    ![Birimler kutucuğunu tıklatın](./media/storsimple-8000-device-dashboard/device-summary9.png)
    
    <span data-ttu-id="66c44-131">Daha fazla bilgi için bkz: nasıl yapılır [birimleri yönetme](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="66c44-131">For more information, see how to [manage volumes](storsimple-8000-manage-volumes-u2.md).</span></span>

* <span data-ttu-id="66c44-132">İçinde **kullanım** grafik, Cihazınızı kullanılan birincil depolama ve son 7 gün içindeki, varsayılan süre tüketilen bulut depolama görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66c44-132">In the **Usage** chart, you can view the primary storage used across your device, and the cloud storage consumed over the past 7 days, the default time period.</span></span>

     ![Kullanımı kutucuğu](./media/storsimple-8000-device-dashboard/device-summary7.png)
    
     <span data-ttu-id="66c44-134">Farklı bir zaman ölçeği seçmek için kullanın **Düzenle** grafiğin sağ üst köşedeki seçeneği.</span><span class="sxs-lookup"><span data-stu-id="66c44-134">To choose a different time scale, use the **Edit** option in the top-right corner of the chart.</span></span>

     ![Kullanım grafiği Düzenle](./media/storsimple-8000-device-dashboard/device-summary12.png)

     <span data-ttu-id="66c44-136">Bu grafik, toplam birincil depolama (aygıtınıza konaklar tarafından yazılan veri miktarı) ve bir süre boyunca cihazınız tarafından kullanılan toplam bulut depolama için ölçüleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66c44-136">In this chart, you can view metrics for the total primary storage (the amount of data written by hosts to your device) and the total cloud storage consumed by your device over a period of time.</span></span>
  
     <span data-ttu-id="66c44-137">Bu bağlamda *birincil depolama* toplam ana bilgisayar tarafından yazılan veri miktarını başvuruyor ve birim türüne göre ayrılabilir: *birincil katmanlı depolama* hem yerel olarak depolanan içeren veri ve veri katmanlı buluta.</span><span class="sxs-lookup"><span data-stu-id="66c44-137">In this context, *primary storage* refers to the total amount of data written by the host, and can be broken down by volume type: *primary tiered storage* includes both locally stored data and data tiered to the cloud.</span></span> <span data-ttu-id="66c44-138">*Birincil yerel olarak sabitlenmiş depolama* yerel olarak depolanan yalnızca verileri içerir.</span><span class="sxs-lookup"><span data-stu-id="66c44-138">*Primary locally pinned storage* includes just data stored locally.</span></span> <span data-ttu-id="66c44-139">*Bulut depolama*, toplam bulutta depolanan veri miktarına, diğer yandan ölçüsüdür.</span><span class="sxs-lookup"><span data-stu-id="66c44-139">*Cloud storage*, on the other hand, is a measurement of the total amount of data stored in the cloud.</span></span> <span data-ttu-id="66c44-140">Bu depolama katmanlı veri ve yedeklemeler içerir.</span><span class="sxs-lookup"><span data-stu-id="66c44-140">This storage includes tiered data and backups.</span></span> <span data-ttu-id="66c44-141">Bulutta depolanan veriler yinelenenleri kaldırılmış ve birincil depolama veri yinelenenleri kaldırılmış ve sıkıştırılmış önce kullanılan depolama alanı miktarını gösterir ancak sıkıştırılmış.</span><span class="sxs-lookup"><span data-stu-id="66c44-141">The data stored in the cloud is deduplicated and compressed, whereas primary storage indicates the amount of storage used before the data is deduplicated and compressed.</span></span> <span data-ttu-id="66c44-142">(Sıkıştırma oranı hakkında bir fikir edinmek için bu iki sayı karşılaştırabilirsiniz.) Hem birincil hem de için ve bulut depolama, gösterilen tutarlar, yapılandırdığınız izleme sıklığına bağlı.</span><span class="sxs-lookup"><span data-stu-id="66c44-142">(You can compare these two numbers to get an idea of the compression rate.) For both primary and cloud storage, the amounts shown are based on the tracking frequency you configure.</span></span> <span data-ttu-id="66c44-143">Bir hafta sıklığı seçerseniz, örneğin, daha sonra grafik veri önceki hafta içinde her gün için gösterir.</span><span class="sxs-lookup"><span data-stu-id="66c44-143">For example, if you choose a one week frequency, then the chart shows data for each day in the previous week.</span></span>

     <span data-ttu-id="66c44-144">Zaman içinde kullanılan bulut depolama alanı miktarını görmek için seçin **bulut depolama kullanılan** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="66c44-144">To see the amount of cloud storage consumed over time, select the **CLOUD STORAGE USED** option.</span></span> <span data-ttu-id="66c44-145">Ana bilgisayar tarafından yazılan toplam depolama görmek için seçin **birincil KATMANLI depolama kullanılan** ve **birincil yerel olarak SABİTLENMİŞ depolama kullanılan** seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="66c44-145">To see the total storage that has been written by the host, select the **PRIMARY TIERED STORAGE USED** and **PRIMARY LOCALLY PINNED STORAGE USED** options.</span></span> 
     <span data-ttu-id="66c44-146">Daha fazla bilgi için bkz: [StorSimple Cihazınızı izlemek için StorSimple cihaz Yöneticisi hizmetini kullanma](storsimple-monitor-device.md).</span><span class="sxs-lookup"><span data-stu-id="66c44-146">For more information, see [Use the StorSimple Device Manager service to monitor your StorSimple device](storsimple-monitor-device.md).</span></span>


* <span data-ttu-id="66c44-147">**Kapasite** kutucuğu aynı için toplam depolama alanı kullanılabilir göre aygıt üzerinden sağlanan ve kalan birincil depolama görüntüler.</span><span class="sxs-lookup"><span data-stu-id="66c44-147">The **Capacity** tile displays the primary storage that is provisioned and remaining across the device relative to the total storage available for the same.</span></span> <span data-ttu-id="66c44-148">**Sağlanan** hazır ve kullanım için ayrılan depolama alanı miktarını başvurduğu **kalan** bu aygıt arasında sağlanabilir kalan kapasite başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="66c44-148">**Provisioned** refers to the amount of storage that is prepared and allocated for use, **Remaining** refers to the remaining capacity that can be provisioned across this device.</span></span> 

    ![Kullanımı kutucuğu](./media/storsimple-8000-device-dashboard/device-summary8.png)

    <span data-ttu-id="66c44-150">Kapasite katmanlı ve yerel olarak sabitlenmiş birimleri arasında nasıl sağlandığında görüntülemek için bu kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="66c44-150">Click this tile to view how the capacity is provisioned across tiered and locally pinned volumes.</span></span> <span data-ttu-id="66c44-151">**Kalan katmanlı** kapasitesi ise bulut dahil olmak üzere sağlanabilir kullanılabilir kapasite sırada **kalan yerel** olduğundan bu cihaza bağlı diskler kalan kapasitesi.</span><span class="sxs-lookup"><span data-stu-id="66c44-151">The **Remaining Tiered** capacity is the available capacity that can be provisioned including cloud, while the **Remaining Local** is the capacity remaining on the disks attached to this device.</span></span>

    ![Kullanım grafiği tıklatın](./media/storsimple-8000-device-dashboard/device-summary13.png)


## <a name="next-steps"></a><span data-ttu-id="66c44-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="66c44-153">Next steps</span></span>
* <span data-ttu-id="66c44-154">Daha fazla bilgi edinmek [StorSimple hizmeti Özet dikey](storsimple-8000-service-dashboard.md).</span><span class="sxs-lookup"><span data-stu-id="66c44-154">Learn more about the [StorSimple service summary blade](storsimple-8000-service-dashboard.md).</span></span>
* <span data-ttu-id="66c44-155">Daha fazla bilgi edinmek [StorSimple Cihazınızı yönetmek için StorSimple cihaz Yöneticisi hizmetini kullanarak](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="66c44-155">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

