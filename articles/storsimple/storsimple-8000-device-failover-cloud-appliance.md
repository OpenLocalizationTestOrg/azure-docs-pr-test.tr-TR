---
title: "aaaStorSimple yük devretme, olağanüstü durum kurtarma tooa StorSimple bulut uygulaması | Microsoft Docs"
description: "Nasıl toofail, StorSimple 8000 serisi fiziksel aygıt tooa üzerinden bulut Gereci öğrenin."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a><span data-ttu-id="f9b52-103">StorSimple bulut uygulaması tooyour başarısız</span><span class="sxs-lookup"><span data-stu-id="f9b52-103">Fail over tooyour StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="f9b52-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f9b52-104">Overview</span></span>

<span data-ttu-id="f9b52-105">Bir olağanüstü durum varsa Bu öğretici bir StorSimple 8000 serisi fiziksel aygıt tooa StorSimple bulut uygulaması hello adımları gerekli toofail açıklar.</span><span class="sxs-lookup"><span data-stu-id="f9b52-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooa StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="f9b52-106">StorSimple hello datacenter tooa bulut uygulaması Azure'da çalışan bir kaynak fiziksel cihazdaki hello aygıt yük devretme özelliği toomigrate verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="f9b52-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooa cloud appliance running in Azure.</span></span> <span data-ttu-id="f9b52-107">Bu öğreticide Hello yönerge tooStorSimple 8000 serisi fiziksel cihazlar ve yazılım sürümlerini güncelleştirme 3 ve sonraki sürümleri çalıştıran bulut uygulamaları geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f9b52-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="f9b52-108">cihaz yük devretme ve bir olağanüstü durum gelen kullanılan toorecover nedir hakkında daha fazla toolearn Git çok[StorSimple 8000 serisi cihazlar için yük devretme ve olağanüstü durum kurtarma](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="f9b52-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="f9b52-109">StorSimple fiziksel cihazı tooanother fiziksel bir aygıtı, üzerinden toofail Git çok[tooa StorSimple fiziksel cihazı başarısız](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="f9b52-109">toofail over a StorSimple physical device tooanother physical device, go too[Fail over tooa StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="f9b52-110">bir aygıt tooitself üzerinden toofail Git çok[toohello aynı başarısız StorSimple fiziksel cihazı](storsimple-8000-device-failover-same-device.md).</span><span class="sxs-lookup"><span data-stu-id="f9b52-110">toofail over a device tooitself, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9b52-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f9b52-111">Prerequisites</span></span>

- <span data-ttu-id="f9b52-112">Cihaz yük devretme için hello konuları gözden geçirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="f9b52-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="f9b52-113">Daha fazla bilgi için çok Git[aygıt yük devretme için ortak konuları](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="f9b52-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="f9b52-114">Bir StorSimple bulut oluşturulur ve bu yordamı çalıştırmadan önce yapılandırılmış Gereci olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9b52-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="f9b52-115">DR Merhaba, çalışan 3 yazılım sürümü güncelleştirme ya da daha sonra bir 8020 bulut uygulaması için kullanmayı düşünün.</span><span class="sxs-lookup"><span data-stu-id="f9b52-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for hello DR.</span></span> <span data-ttu-id="f9b52-116">Merhaba 8020 modeli 64 TB vardır ve Premium depolama kullanır.</span><span class="sxs-lookup"><span data-stu-id="f9b52-116">hello 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="f9b52-117">Daha fazla bilgi için çok Git[dağıtma ve StorSimple bulut uygulaması yönetmek](storsimple-8000-cloud-appliance-u2.md).</span><span class="sxs-lookup"><span data-stu-id="f9b52-117">For more information, go too[Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-toofail-over-tooa-cloud-appliance"></a><span data-ttu-id="f9b52-118">Adımları toofail tooa bulut uygulaması üzerinden</span><span class="sxs-lookup"><span data-stu-id="f9b52-118">Steps toofail over tooa cloud appliance</span></span>

<span data-ttu-id="f9b52-119">Aşağıdaki adımları toorestore hello aygıt tooa hedef StorSimple bulut uygulaması hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="f9b52-119">Perform hello following steps toorestore hello device tooa target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="f9b52-120">Bu hello birim kapsayıcısı üzerinde toofail istediğiniz bulut anlık görüntüleri ilişkili doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f9b52-120">Verify that hello volume container you want toofail over has associated cloud snapshots.</span></span> <span data-ttu-id="f9b52-121">Daha fazla bilgi için çok Git[Aygıt Yöneticisi'ni StorSimple hizmeti toocreate yedeklemeleri](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="f9b52-121">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="f9b52-122">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="f9b52-122">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="f9b52-123">Merhaba, **aygıtları** dikey penceresinde, hizmetiniz ile bağlı cihazlar gidin toohello listesi.</span><span class="sxs-lookup"><span data-stu-id="f9b52-123">In hello **Devices** blade, go toohello list of devices connected with your service.</span></span>
    <span data-ttu-id="f9b52-124">![Cihazı seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="f9b52-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="f9b52-125">Seçin ve kaynak Cihazınızı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9b52-125">Select and click your source device.</span></span> <span data-ttu-id="f9b52-126">Merhaba kaynak aygıt üzerinden toofail istediğiniz hello birim kapsayıcıları sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f9b52-126">hello source device has hello volume containers that you want toofail over.</span></span> <span data-ttu-id="f9b52-127">Çok Git**ayarlar > birim kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="f9b52-127">Go too**Settings > Volume Containers**.</span></span>

    ![Cihazı seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="f9b52-129">Tooanother aygıt üzerinden toofail istediğiniz bir birim kapsayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="f9b52-129">Select a volume container that you would like toofail over tooanother device.</span></span> <span data-ttu-id="f9b52-130">Merhaba birim kapsayıcı toodisplay hello birimlerin listesini bu kapsayıcıdaki'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f9b52-130">Click hello volume container toodisplay hello list of volumes within this container.</span></span> <span data-ttu-id="f9b52-131">Bir birim, sağ tıklatın ve tıklatın seçin **Çevrimdışına Al** tootake hello çevrimdışı birim.</span><span class="sxs-lookup"><span data-stu-id="f9b52-131">Select a volume, right-click, and click **Take Offline** tootake hello volume offline.</span></span>

    ![Cihazı seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="f9b52-133">Merhaba birim kapsayıcısındaki tüm hello birimleri için bu işlemi yineleyin.</span><span class="sxs-lookup"><span data-stu-id="f9b52-133">Repeat this process for all hello volumes in hello volume container.</span></span>

     ![Cihazı seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="f9b52-135">Önceki adımı yineleyin hello tüm birim kapsayıcıları hello için tooanother aygıt üzerinden toofail istersiniz.</span><span class="sxs-lookup"><span data-stu-id="f9b52-135">Repeat hello previous step for all hello volume containers you would like toofail over tooanother device.</span></span>

7. <span data-ttu-id="f9b52-136">Toohello dönün **aygıtları** dikey.</span><span class="sxs-lookup"><span data-stu-id="f9b52-136">Go back toohello **Devices** blade.</span></span> <span data-ttu-id="f9b52-137">Merhaba Komut çubuğundaki **yük devri**.</span><span class="sxs-lookup"><span data-stu-id="f9b52-137">From hello command bar, click **Fail over**.</span></span>

    ![Üzerinden başarısız'ı tıklatın](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="f9b52-139">Merhaba, **yük devri** dikey penceresinde hello aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="f9b52-139">In hello **Fail over** blade, perform hello following steps:</span></span>
   
    1. <span data-ttu-id="f9b52-140">Tıklatın **kaynak**.</span><span class="sxs-lookup"><span data-stu-id="f9b52-140">Click **Source**.</span></span> <span data-ttu-id="f9b52-141">Üzerinden Hello birim kapsayıcıları toofail seçin.</span><span class="sxs-lookup"><span data-stu-id="f9b52-141">Select hello volume containers toofail over.</span></span> <span data-ttu-id="f9b52-142">**Yalnızca ilişkili bulut anlık görüntüleri ile birim kapsayıcıları hello ve çevrimdışı birimler görüntülenir.**</span><span class="sxs-lookup"><span data-stu-id="f9b52-142">**Only hello volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="f9b52-143">![Kaynak seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="f9b52-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="f9b52-144">Tıklatın **hedef**.</span><span class="sxs-lookup"><span data-stu-id="f9b52-144">Click **Target**.</span></span> <span data-ttu-id="f9b52-145">Bir hedef bulut uygulaması hello açılır listeden kullanılabilir aygıtları seçin.</span><span class="sxs-lookup"><span data-stu-id="f9b52-145">Select a target cloud appliance from hello dropdown list of available devices.</span></span> <span data-ttu-id="f9b52-146">**Yeterli kapasitesi tooaccommodate kaynak birim kapsayıcıları yalnızca hello cihazları hello listesinde görüntülenir.**</span><span class="sxs-lookup"><span data-stu-id="f9b52-146">**Only hello devices that have sufficient capacity tooaccommodate source volume containers are displayed in hello list.**</span></span>

        ![Hedef seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="f9b52-148">Merhaba yük devretme ayarları altında gözden **Özet** ve hello onay kutusu seçili birim kapsayıcıları hello birimlerinde çevrimdışı belirten seçin.</span><span class="sxs-lookup"><span data-stu-id="f9b52-148">Review hello failover settings under **Summary** and select hello checkbox indicating that hello volumes in selected volume containers are offline.</span></span> 

        ![Yük devretme ayarlarını gözden geçirin](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="f9b52-150">Bir yük devretme iş oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f9b52-150">A failover job is created.</span></span> <span data-ttu-id="f9b52-151">toomonitor hello yük devretme iş, hello iş bildirime tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f9b52-151">toomonitor hello failover job, click hello job notification.</span></span>

    ![İzleyici yük devretme işine](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="f9b52-153">Toohello Hello yük devretme tamamlandıktan sonra geri dönün **aygıtları** dikey.</span><span class="sxs-lookup"><span data-stu-id="f9b52-153">After hello failover is completed, go back toohello **Devices** blade.</span></span>

    1. <span data-ttu-id="f9b52-154">Merhaba hedef olarak hello yük devretme için kullanılan hello cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="f9b52-154">Select hello device that was used as hello target for hello failover.</span></span>

       ![Cihazı seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="f9b52-156">Tıklatın **birim kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="f9b52-156">Click **Volume Containers**.</span></span> <span data-ttu-id="f9b52-157">Merhaba birimleri hello eski aygıttan yanı sıra tüm hello birim kapsayıcıları listelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="f9b52-157">All hello volume containers, along with hello volumes from hello old device, should be listed.</span></span>

       <span data-ttu-id="f9b52-158">Üzerinden başarısız hello birim kapsayıcısı yerel olarak sabitlenmiş birimleri, bu birimlerin katmanlı birimler olarak yük devredildi.</span><span class="sxs-lookup"><span data-stu-id="f9b52-158">If hello volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="f9b52-159">Yerel olarak sabitlenmiş birimlerin bir StorSimple bulut uygulaması üzerinde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="f9b52-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![Görünüm hedef birim kapsayıcıları](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="f9b52-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f9b52-161">Next steps</span></span>

* <span data-ttu-id="f9b52-162">Bir yük devretme gerçekleştirdikten sonra çok gerekebilir[StorSimple Cihazınızı silmek veya devre dışı bırakma](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="f9b52-162">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="f9b52-163">Hizmet nasıl toouse hello StorSimple cihaz Yöneticisi hakkında daha fazla bilgi için çok Git[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f9b52-163">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

