---
title: "StorSimple yük devretme, StorSimple 8000 serisi fiziksel aygıt için olağanüstü durum kurtarma | Microsoft Docs"
description: "StorSimple 8000 serisi fiziksel aygıtınıza başka bir fiziksel aygıt üzerinden vermesine öğrenin."
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
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: f3ac9545a341fc24ca12c9f2547805d6956cd98a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-to-a-storsimple-8000-series-physical-device"></a><span data-ttu-id="bec61-103">StorSimple 8000 serisi fiziksel cihaza yük devri</span><span class="sxs-lookup"><span data-stu-id="bec61-103">Fail over to a StorSimple 8000 series physical device</span></span>

## <a name="overview"></a><span data-ttu-id="bec61-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="bec61-104">Overview</span></span>

<span data-ttu-id="bec61-105">Bu öğretici bir StorSimple 8000 serisi fiziksel cihazı başka bir StorSimple fiziksel cihazı bir olağanüstü durum varsa devretmek için gereken adımları açıklar.</span><span class="sxs-lookup"><span data-stu-id="bec61-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to another StorSimple physical device if there is a disaster.</span></span> <span data-ttu-id="bec61-106">StorSimple cihaz yük devretme özelliğini veri merkezindeki fiziksel bir kaynak aygıtı başka bir fiziksel cihaza geçirmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="bec61-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to another physical device.</span></span> <span data-ttu-id="bec61-107">Bu öğreticideki yönergeler yazılım sürümleri güncelleştirme 3 ve sonraki sürümleri çalıştıran fiziksel cihazları StorSimple 8000 serisi için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="bec61-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="bec61-108">Cihaz yük devretme ve olağanüstü durumdan kurtarmak için nasıl kullanıldığı hakkında daha fazla bilgi için şuraya gidin [StorSimple 8000 serisi cihazlar için yük devretme ve olağanüstü durum kurtarma](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="bec61-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="bec61-109">Bir StorSimple bulut uygulaması StorSimple fiziksel cihaza yük devretme için Git [StorSimple bulut uygulaması için yük devri](storsimple-8000-device-failover-cloud-appliance.md).</span><span class="sxs-lookup"><span data-stu-id="bec61-109">To fail over a StorSimple physical device to a StorSimple Cloud Appliance, go to [Fail over to a StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span> <span data-ttu-id="bec61-110">Kendisi için fiziksel bir aygıtı devretmek için Git [aynı StorSimple fiziksel cihazı yük devri](storsimple-8000-device-failover-same-device.md).</span><span class="sxs-lookup"><span data-stu-id="bec61-110">To fail over a physical device to itself, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="bec61-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bec61-111">Prerequisites</span></span>

- <span data-ttu-id="bec61-112">Cihaz yük devretme için konuları gözden geçirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="bec61-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="bec61-113">Daha fazla bilgi için Git [aygıt yük devretme için ortak konuları](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="bec61-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="bec61-114">Veri merkezinde dağıtılan bir StorSimple 8000 serisi fiziksel bir aygıtı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bec61-114">You must have a StorSimple 8000 series physical device deployed in the datacenter.</span></span> <span data-ttu-id="bec61-115">Cihaz, güncelleştirme 3 veya sonraki yazılım sürümü çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bec61-115">The device must run Update 3 or later software version.</span></span> <span data-ttu-id="bec61-116">Daha fazla bilgi için Git [şirket içi StorSimple Cihazınızı dağıtma](storsimple-8000-deployment-walkthrough-u2.md).</span><span class="sxs-lookup"><span data-stu-id="bec61-116">For more information, go to [Deploy your on-premises StorSimple device](storsimple-8000-deployment-walkthrough-u2.md).</span></span>


## <a name="steps-to-fail-over-to-a-physical-device"></a><span data-ttu-id="bec61-117">Fiziksel bir cihaza yük devri için adımları</span><span class="sxs-lookup"><span data-stu-id="bec61-117">Steps to fail over to a physical device</span></span>

<span data-ttu-id="bec61-118">Cihazınızı bir hedef fiziksel cihaza geri yüklemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="bec61-118">Perform the following steps to restore your device to a target physical device.</span></span>

1. <span data-ttu-id="bec61-119">Devretmek istediğiniz birim kapsayıcısı bulut anlık görüntüleri ilişkili olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bec61-119">Verify that the volume container you want to fail over has associated cloud snapshots.</span></span> <span data-ttu-id="bec61-120">Daha fazla bilgi için Git [yedeklemeler oluşturmak için Aygıt Yöneticisi'ni StorSimple hizmeti](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="bec61-120">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="bec61-121">StorSimple cihaz yöneticinize gidin ve ardından **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="bec61-121">Go to your StorSimple Device Manager and then click **Devices**.</span></span> <span data-ttu-id="bec61-122">İçinde **aygıtları** dikey penceresinde, hizmetiniz ile bağlı cihazlar listesine gidin.</span><span class="sxs-lookup"><span data-stu-id="bec61-122">In the **Devices** blade, go to the list of devices connected with your service.</span></span>
    <span data-ttu-id="bec61-123">![Cihazı seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="bec61-123">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)</span></span>
3. <span data-ttu-id="bec61-124">Seçin ve kaynak Cihazınızı tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bec61-124">Select and click your source device.</span></span> <span data-ttu-id="bec61-125">Kaynak aygıtın devretmek istediğiniz birim kapsayıcıları vardır.</span><span class="sxs-lookup"><span data-stu-id="bec61-125">The source device has the volume containers that you want to fail over.</span></span> <span data-ttu-id="bec61-126">Git **ayarlar > birim kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="bec61-126">Go to **Settings > Volume Containers**.</span></span>
4. <span data-ttu-id="bec61-127">Başka bir cihaza yük devri istediğiniz bir birim kapsayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="bec61-127">Select a volume container that you would like to fail over to another device.</span></span> <span data-ttu-id="bec61-128">Bu kapsayıcı içindeki birimlerin listesini görüntülemek için birim kapsayıcısı'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="bec61-128">Click the volume container to display the list of volumes within this container.</span></span> <span data-ttu-id="bec61-129">Bir birim, sağ tıklatın ve tıklatın seçin **Çevrimdışına Al** birimi çevrimdışı duruma getirmek için.</span><span class="sxs-lookup"><span data-stu-id="bec61-129">Select a volume, right-click, and click **Take Offline** to take the volume offline.</span></span> <span data-ttu-id="bec61-130">Bu işlemi, birim kapsayıcısındaki tüm birimler için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="bec61-130">Repeat this process for all the volumes in the volume container.</span></span>
5. <span data-ttu-id="bec61-131">Başka bir cihaza yük devri istediğiniz tüm birim kapsayıcıları için önceki adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="bec61-131">Repeat the previous step for all the volume containers you would like to fail over to another device.</span></span>
6. <span data-ttu-id="bec61-132">Geri dönerek **aygıtları** dikey.</span><span class="sxs-lookup"><span data-stu-id="bec61-132">Go back to the **Devices** blade.</span></span> <span data-ttu-id="bec61-133">Komut çubuğundaki **yük devri**.</span><span class="sxs-lookup"><span data-stu-id="bec61-133">From the command bar, click **Fail over**.</span></span>
    <span data-ttu-id="bec61-134">![Üzerinden başarısız'ı tıklatın](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)</span><span class="sxs-lookup"><span data-stu-id="bec61-134">![Click fail over](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)</span></span>
    
7. <span data-ttu-id="bec61-135">İçinde **yük devri** dikey penceresinde, aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="bec61-135">In the **Fail over** blade, perform the following steps:</span></span>
   
   1. <span data-ttu-id="bec61-136">Tıklatın **kaynak**.</span><span class="sxs-lookup"><span data-stu-id="bec61-136">Click **Source**.</span></span> <span data-ttu-id="bec61-137">Bulut anlık görüntüleri ile ilişkili birimi ile birim kapsayıcıları görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bec61-137">The volume containers with volumes associated with cloud snapshots are displayed.</span></span> <span data-ttu-id="bec61-138">Yalnızca görüntülenen kapsayıcıları, yük devretme için uygundur.</span><span class="sxs-lookup"><span data-stu-id="bec61-138">Only the containers displayed are eligible for failover.</span></span> <span data-ttu-id="bec61-139">Birim kapsayıcıları listesinde devretmek istediğiniz birim kapsayıcıları seçin.</span><span class="sxs-lookup"><span data-stu-id="bec61-139">In the list of volume containers, select the volume containers you would like to fail over.</span></span> <span data-ttu-id="bec61-140">**Yalnızca birim kapsayıcıları ilişkili bulut anlık görüntüleri ve çevrimdışı birimlerle birlikte görüntülenir.**</span><span class="sxs-lookup"><span data-stu-id="bec61-140">**Only the volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>

       ![Kaynak seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. <span data-ttu-id="bec61-142">Tıklatın **hedef**.</span><span class="sxs-lookup"><span data-stu-id="bec61-142">Click **Target**.</span></span> <span data-ttu-id="bec61-143">Önceki adımda seçtiğiniz birim kapsayıcıları için hedef aygıtta kullanılabilir aygıtları aşağı açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="bec61-143">For the volume containers selected in the previous step, select a target device from the drop-down list of available devices.</span></span> <span data-ttu-id="bec61-144">Yalnızca kaynak birim kapsayıcıları karşılamak için yeterli kapasiteye sahip aygıtlar listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bec61-144">Only the devices that have sufficient capacity to accommodate source volume containers are displayed in the list.</span></span>

        ![Hedef seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. <span data-ttu-id="bec61-146">Son olarak, tüm yük devretme ayarları altında gözden **Özet**.</span><span class="sxs-lookup"><span data-stu-id="bec61-146">Finally, review all the failover settings under **Summary**.</span></span> <span data-ttu-id="bec61-147">Ayarları gözden geçirdikten sonra seçilen birim kapsayıcıları birimlerin çevrimdışı olduğunu gösteren onay kutusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="bec61-147">After you have reviewed the settings, select the checkbox indicating that the volumes in selected volume containers are offline.</span></span> <span data-ttu-id="bec61-148">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bec61-148">Click **OK**.</span></span>

       ![Yük devretme ayarlarını gözden geçirin](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. <span data-ttu-id="bec61-150">StorSimple bir yük devretme işi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bec61-150">StorSimple creates a failover job.</span></span> <span data-ttu-id="bec61-151">Yük devretme işlemi aracılığıyla izlemek için iş bildirimi tıklatın **işleri** dikey.</span><span class="sxs-lookup"><span data-stu-id="bec61-151">Click the job notification to monitor the failover job via the **Jobs** blade.</span></span>

    <span data-ttu-id="bec61-152">Üzerinden başarısız birim kapsayıcısı yerel birim varsa, tek tek geri yükleme işleri kapsayıcıdaki her yerel birimi (değil için katmanlı birimleri) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="bec61-152">If the volume container that you failed over has local volumes, then you see individual restore jobs for each local volume (not for tiered volumes) in the container.</span></span> <span data-ttu-id="bec61-153">Bu geri yükleme işlerinin tamamlanmasını oldukça biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="bec61-153">These restore jobs may take quite some time to complete.</span></span> <span data-ttu-id="bec61-154">Yük devretme işine önceki tamamlanabilir olasıdır.</span><span class="sxs-lookup"><span data-stu-id="bec61-154">It is likely that the failover job may complete earlier.</span></span> <span data-ttu-id="bec61-155">Yalnızca geri yükleme işi tamamlandıktan sonra bu birimler yerel GARANTİLERİN sahip olur.</span><span class="sxs-lookup"><span data-stu-id="bec61-155">These volumes will have local guarantees only after the restore jobs are complete.</span></span>

    ![İzleyici yük devretme işine](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. <span data-ttu-id="bec61-157">Yük devretme işlemi tamamlandıktan sonra Git **aygıtları** dikey.</span><span class="sxs-lookup"><span data-stu-id="bec61-157">After the failover is completed, go to the **Devices** blade.</span></span>
   
   1. <span data-ttu-id="bec61-158">Yük devretme işlemi için hedef cihaz olarak kullanılan cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="bec61-158">Select the device that was used as the target device for the failover process.</span></span>

       ![Cihazı seçin](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. <span data-ttu-id="bec61-160">Git **birim kapsayıcıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="bec61-160">Go to the **Volume Containers** blade.</span></span> <span data-ttu-id="bec61-161">Eski aygıt birimlerden yanı sıra tüm birim kapsayıcıları, listelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="bec61-161">All the volume containers, along with the volumes from the old device, should be listed.</span></span>

       ![Görünüm hedef birim kapsayıcıları](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a><span data-ttu-id="bec61-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bec61-163">Next steps</span></span>

* <span data-ttu-id="bec61-164">Bir yük devretme gerçekleştirdikten sonra gerekebilir [StorSimple Cihazınızı silmek veya devre dışı bırakma](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="bec61-164">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="bec61-165">StorSimple cihaz Yöneticisi hizmetini kullanma hakkında daha fazla bilgi için Git [StorSimple Cihazınızı yönetmek için StorSimple cihaz Yöneticisi hizmetini kullanma](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="bec61-165">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

