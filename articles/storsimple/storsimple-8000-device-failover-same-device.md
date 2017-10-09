---
title: "aaaStorSimple yük devretme, 8000 serisi cihazlar için olağanüstü durum kurtarma | Microsoft Docs"
description: "Bilgi nasıl toofail StorSimple cihaz toohello üzerinden aynı aygıt."
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a><span data-ttu-id="be5eb-103">StorSimple fiziksel cihazı toosame Cihazınızı başarısız</span><span class="sxs-lookup"><span data-stu-id="be5eb-103">Fail over your StorSimple physical device toosame device</span></span>

## <a name="overview"></a><span data-ttu-id="be5eb-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="be5eb-104">Overview</span></span>

<span data-ttu-id="be5eb-105">Bir olağanüstü durum varsa Bu öğretici bir StorSimple 8000 serisi fiziksel aygıt tooitself hello adımları gerekli toofail açıklar.</span><span class="sxs-lookup"><span data-stu-id="be5eb-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooitself if there is a disaster.</span></span> <span data-ttu-id="be5eb-106">StorSimple hello aygıt yük devretme özelliği toomigrate veri kaynağı fiziksel CİHAZDAN hello datacenter tooanother fiziksel cihazın kullanır.</span><span class="sxs-lookup"><span data-stu-id="be5eb-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooanother physical device.</span></span> <span data-ttu-id="be5eb-107">Bu öğreticide Hello yönerge tooStorSimple 8000 serisi fiziksel cihazlar yazılım sürümleri güncelleştirme 3 ve sonraki sürümleri çalıştıran geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="be5eb-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="be5eb-108">cihaz yük devretme ve bir olağanüstü durum gelen kullanılan toorecover nedir hakkında daha fazla toolearn Git çok[StorSimple 8000 serisi cihazlar için yük devretme ve olağanüstü durum kurtarma](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="be5eb-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="be5eb-109">bir fiziksel aygıt tooanother fiziksel aygıt üzerinden toofail Git çok[toohello aynı başarısız StorSimple fiziksel cihazı](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="be5eb-109">toofail over a physical device tooanother physical device, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="be5eb-110">bir StorSimple fiziksel cihazı tooa StorSimple bulut uygulaması üzerinden toofail Git çok[tooa StorSimple bulut uygulaması başarısız](storsimple-8000-device-failover-cloud-appliance.md).</span><span class="sxs-lookup"><span data-stu-id="be5eb-110">toofail over a StorSimple physical device tooa StorSimple Cloud Appliance, go too[Fail over tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="be5eb-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="be5eb-111">Prerequisites</span></span>

- <span data-ttu-id="be5eb-112">Cihaz yük devretme için hello konuları gözden geçirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="be5eb-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="be5eb-113">Daha fazla bilgi için çok Git[aygıt yük devretme için ortak konuları](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="be5eb-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-toofail-over-toohello-same-device"></a><span data-ttu-id="be5eb-114">Adımları toofail toohello üzerinden aynı aygıt</span><span class="sxs-lookup"><span data-stu-id="be5eb-114">Steps toofail over toohello same device</span></span>

<span data-ttu-id="be5eb-115">Merhaba toohello toofail gerekiyorsa aşağıdaki adımları gerçekleştirin aynı aygıt.</span><span class="sxs-lookup"><span data-stu-id="be5eb-115">Perform hello following steps if you need toofail over toohello same device.</span></span>

1. <span data-ttu-id="be5eb-116">Tüm hello birimleri bulut anlık görüntülerini kullanarak Cihazınızı alın.</span><span class="sxs-lookup"><span data-stu-id="be5eb-116">Take cloud snapshots of all hello volumes in your device.</span></span> <span data-ttu-id="be5eb-117">Daha fazla bilgi için çok Git[Aygıt Yöneticisi'ni StorSimple hizmeti toocreate yedeklemeleri](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="be5eb-117">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="be5eb-118">Cihaz toofactory Varsayılanları sıfırlayın.</span><span class="sxs-lookup"><span data-stu-id="be5eb-118">Reset your device toofactory defaults.</span></span> <span data-ttu-id="be5eb-119">İzleyin hello ayrıntılı yönergeleri [nasıl tooreset StorSimple cihaz toofactory varsayılan ayarları](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="be5eb-119">Follow hello detailed instructions in [how tooreset a StorSimple device toofactory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="be5eb-120">Toohello StorSimple cihaz Yöneticisi hizmeti gidin ve ardından **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="be5eb-120">Go toohello StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="be5eb-121">Merhaba, **aygıtları** dikey penceresinde hello eski aygıt Göster olarak **çevrimdışı**.</span><span class="sxs-lookup"><span data-stu-id="be5eb-121">In hello **Devices** blade, hello old device should show as **Offline**.</span></span>

    ![Kaynak aygıt çevrimdışı](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="be5eb-123">Cihazınızı yapılandırmak ve StorSimple cihaz Yöneticisi hizmetiniz ile yeniden kaydedin.</span><span class="sxs-lookup"><span data-stu-id="be5eb-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="be5eb-124">Merhaba yeni kayıtlı cihaz olarak göstermelidir **yukarı tooset hazır**.</span><span class="sxs-lookup"><span data-stu-id="be5eb-124">hello newly registered device should show as **Ready tooset up**.</span></span> <span data-ttu-id="be5eb-125">Merhaba aygıt hello yeni cihaz için hello eski aygıt ile sayısal tooindicate hello aygıt ancak eklenmiş. aynı sıfırlama toofactory varsayılan oldu ve yeniden kayıtlı hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="be5eb-125">hello device name for hello new device is hello same as hello old device but appended with a numeral tooindicate that hello device was reset toofactory default and registered again.</span></span>

    ![Yeni kaydedilen cihaz hazır tooset ayarlama](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="be5eb-127">Merhaba yeni cihaz hello cihaz kurulumunu tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="be5eb-127">For hello new device, complete hello device setup.</span></span> <span data-ttu-id="be5eb-128">Daha fazla bilgi için çok Git[4. adım: minimum cihaz kurulumunu Tamamla](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="be5eb-128">For more information, go too[Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="be5eb-129">Merhaba üzerinde **aygıtları** dikey penceresinde hello aygıt hello durumunu değiştirir çok**çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="be5eb-129">On hello **Devices** blade, hello status of hello device changes too**Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="be5eb-130">**Merhaba en düşük yapılandırmayı ilk tamamlamak ya da, DR başarısız olabilir.**</span><span class="sxs-lookup"><span data-stu-id="be5eb-130">**Complete hello minimum configuration first, or your DR may fail.**</span></span>

    ![Yeni kaydedilen cihaz çevrimiçi](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="be5eb-132">Merhaba eski aygıt (çevrimdışı durumu) seçin ve hello Komut çubuğundaki **yük devri**.</span><span class="sxs-lookup"><span data-stu-id="be5eb-132">Select hello old device (status offline) and from hello command bar, click **Fail over**.</span></span> <span data-ttu-id="be5eb-133">Merhaba, **yük devri** dikey penceresinde hello kaynağı olarak eski aygıt seçin ve hello yeni cihaz kayıtlı gibi hello hedef aygıt belirtin.</span><span class="sxs-lookup"><span data-stu-id="be5eb-133">In hello **Fail over** blade, select old device as hello source and specify hello target device as hello newly registered device.</span></span>

    ![Yük devretme özeti](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="be5eb-135">Ayrıntılı yönergeler için çok başvuran[tooanother fiziksel aygıt üzerinden başarısız](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="be5eb-135">For detailed instructions, refer too[Fail over tooanother physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="be5eb-136">Bir aygıt geri yükleme iş hello izleyebilirsiniz oluşturulur **işleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="be5eb-136">A device restore job is created that you can monitor from hello **Jobs** blade.</span></span>

8. <span data-ttu-id="be5eb-137">Merhaba iş başarıyla tamamlandıktan sonra erişim hello yeni cihaz ve toohello gidin **birim kapsayıcıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="be5eb-137">After hello job has successfully completed, access hello new device and navigate toohello **Volume containers** blade.</span></span> <span data-ttu-id="be5eb-138">Merhaba eski aygıttan tüm hello birim kapsayıcıları toohello yeni cihaz geçirildiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="be5eb-138">Verify that all hello volume containers from hello old device have migrated toohello new device.</span></span>

   ![Birim kapsayıcıları geçişi](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="be5eb-140">Merhaba yük devretme işlemi tamamlandıktan sonra devre dışı bırakıp hello portalından hello eski aygıt silme.</span><span class="sxs-lookup"><span data-stu-id="be5eb-140">After hello failover is complete, you can deactivate and delete hello old device from hello portal.</span></span> <span data-ttu-id="be5eb-141">Merhaba eski aygıt (çevrimdışı), sağ seçin ve ardından **etkinliğini**.</span><span class="sxs-lookup"><span data-stu-id="be5eb-141">Select hello old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="be5eb-142">Merhaba aygıt devre dışı bırakıldıktan sonra hello cihazın hello durumu güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="be5eb-142">After hello device is deactivated, hello status of hello device is updated.</span></span>

     ![Kaynak aygıt devre dışı](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="be5eb-144">Select hello aygıt, sağ tıklatın ve ardından devre dışı **silmek**.</span><span class="sxs-lookup"><span data-stu-id="be5eb-144">Select hello deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="be5eb-145">Bu hello aygıt cihazların Merhaba listeden siler.</span><span class="sxs-lookup"><span data-stu-id="be5eb-145">This deletes hello device from hello list of devices.</span></span>

    ![Kaynak aygıt silindi](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="be5eb-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="be5eb-147">Next steps</span></span>

* <span data-ttu-id="be5eb-148">Bir yük devretme gerçekleştirdikten sonra çok gerekebilir[StorSimple Cihazınızı silmek veya devre dışı bırakma](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="be5eb-148">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="be5eb-149">Hizmet nasıl toouse hello StorSimple cihaz Yöneticisi hakkında daha fazla bilgi için çok Git[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="be5eb-149">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

