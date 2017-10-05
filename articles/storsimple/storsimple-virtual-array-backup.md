---
title: "Microsoft Azure StorSimple sanal dizinin yedekleme Öğreticisi | Microsoft Docs"
description: "StorSimple sanal dizinin paylaşımları ve birimler yedekleme açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: e3cdcd9e-33b1-424d-82aa-b369d934067e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c926f0c80ce56cac3106ad97ec3ec2e18a8e2cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="1b4e0-103">Paylaşımlar veya birimler, StorSimple sanal dizisinde yedekle</span><span class="sxs-lookup"><span data-stu-id="1b4e0-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="1b4e0-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="1b4e0-104">Overview</span></span>

<span data-ttu-id="1b4e0-105">StorSimple sanal dizinin bir dosya sunucusu veya bir iSCSI sunucusu yapılandırılmış bir karma bulut depolama şirket içi sanal cihazdır.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-105">The StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="1b4e0-106">Sanal dizinin cihazda zamanlanmış ve el ile yedeklerini tüm paylaşımlar veya birimler oluşturmasına olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-106">The virtual array allows the user to create scheduled and manual backups of all the shares or volumes on the device.</span></span> <span data-ttu-id="1b4e0-107">Dosya sunucusu olarak yapılandırıldığında, öğe düzeyinde kurtarma de sağlar.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="1b4e0-108">Bu öğretici, zamanlanmış ve el ile yedekleme oluşturmak ve sanal dizisindeki silinmiş bir dosyayı geri yüklemek için öğe düzeyinde kurtarma gerçekleştirmek açıklar.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-108">This tutorial describes how to create scheduled and manual backups and perform item-level recovery to restore a deleted file on your virtual array.</span></span>

<span data-ttu-id="1b4e0-109">Bu öğretici, StorSimple sanal diziler için yalnızca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-109">This tutorial applies to the StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="1b4e0-110">8000 serisi hakkında daha fazla bilgi için Git [8000 serisi aygıtı için bir yedekleme oluşturmak](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="1b4e0-110">For information on 8000 series, go to [Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="1b4e0-111">Paylaşımları ve birimler yedekleme</span><span class="sxs-lookup"><span data-stu-id="1b4e0-111">Back up shares and volumes</span></span>

<span data-ttu-id="1b4e0-112">Yedeklemeleri zaman noktası korumasını sağlar, kurtarılabilirliği iyileştirmeye ve paylaşımları ve birimler için geri yükleme sürelerini en aza.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="1b4e0-113">StorSimple Cihazınızda iki yolla paylaşımı veya birimi yedekleyebilirsiniz: **zamanlanmış** veya **el ile**.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="1b4e0-114">Yöntemlerin her biri aşağıdaki bölümlerde ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-114">Each of the methods is discussed in the following sections.</span></span>

## <a name="change-the-backup-start-time"></a><span data-ttu-id="1b4e0-115">Yedekleme başlangıç saatini değiştir</span><span class="sxs-lookup"><span data-stu-id="1b4e0-115">Change the backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="1b4e0-116">Bu sürümde, zamanlanmış yedeklemeler, her gün belirtilen zamanda çalışan ve tüm paylaşımlar veya birimler cihazda yedekler varsayılan bir ilke tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all the shares or volumes on the device.</span></span> <span data-ttu-id="1b4e0-117">Şu anda zamanlanmış yedeklemeler için özel ilkeler oluşturmak mümkün değil.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-117">It is not possible to create custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="1b4e0-118">StorSimple sanal dizinizi (22:30) günün belirli bir zamanda başlatır ve tüm paylaşımlar veya birimler cihazda günde bir kez yedekler varsayılan yedekleme ilkesine sahip.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all the shares or volumes on the device once a day.</span></span> <span data-ttu-id="1b4e0-119">Hangi yedekleme başlar, ancak sıklığı ve (hangi korumak için yedeklemeler sayısını belirtir) bekletme değiştirilemez zaman değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-119">You can change the time at which the backup starts, but the frequency and the retention (which specifies the number of backups to retain) cannot be changed.</span></span> <span data-ttu-id="1b4e0-120">Bu yedeklemeler sırasında sanal cihazın tamamının yedeklenir.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-120">During these backups, the entire virtual device is backed up.</span></span> <span data-ttu-id="1b4e0-121">Bu olası cihaz performansını etkileyebilir ve cihazda dağıtılan iş yükleri etkiler.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-121">This could potentially impact the performance of the device and affect the workloads deployed on the device.</span></span> <span data-ttu-id="1b4e0-122">Bu nedenle, bu yedeklemeler için yoğun olmayan saatler zamanlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="1b4e0-123">Varsayılan yedekleme başlangıç saati değiştirmek için aşağıdaki adımları gerçekleştirin [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1b4e0-123">To change the default backup start time, perform the following steps in the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="to-change-the-start-time-for-the-default-backup-policy"></a><span data-ttu-id="1b4e0-124">Varsayılan yedekleme ilkesinin başlangıç saati değiştirmek için</span><span class="sxs-lookup"><span data-stu-id="1b4e0-124">To change the start time for the default backup policy</span></span>

1. <span data-ttu-id="1b4e0-125">Git **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-125">Go to **Devices**.</span></span> <span data-ttu-id="1b4e0-126">StorSimple cihaz Yöneticisi hizmetiniz ile kaydedilmiş cihazların listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-126">The list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![aygıtlara gidin](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="1b4e0-128">Seçin ve aygıtınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-128">Select and click your device.</span></span> <span data-ttu-id="1b4e0-129">**Ayarları** dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-129">The **Settings** blade will be displayed.</span></span> <span data-ttu-id="1b4e0-130">Git **Yönet > Yedekleme ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-130">Go to **Manage > Backup policies**.</span></span>
   
    ![Cihazınızı seçin](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="1b4e0-132">İçinde **yedekleme ilkeleri** dikey penceresinde, varsayılan başlangıç zamanıdır 22:30.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-132">In the **Backup policies** blade, the default start time is 22:30.</span></span> <span data-ttu-id="1b4e0-133">Günlük Zamanlama için yeni başlangıç saati aygıt saat diliminde belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-133">You can specify the new start time for the daily schedule in device time zone.</span></span>
   
    ![Yedekleme ilkeleri gidin](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="1b4e0-135">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="1b4e0-136">El ile yedekleyin</span><span class="sxs-lookup"><span data-stu-id="1b4e0-136">Take a manual backup</span></span>

<span data-ttu-id="1b4e0-137">Zamanlanmış yedeklemeleri yanı sıra, el ile (isteğe bağlı) herhangi bir zamanda cihaz verilerin yedeğini sürebilir.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-137">In addition to scheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="to-create-a-manual-backup"></a><span data-ttu-id="1b4e0-138">El ile yedekleme oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="1b4e0-138">To create a manual backup</span></span>

1. <span data-ttu-id="1b4e0-139">Git **aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-139">Go to **Devices**.</span></span> <span data-ttu-id="1b4e0-140">Cihazınızı seçin ve sağ **...**  seçili satırdaki sağ uçta.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-140">Select your device and right-click **...** at the far right in the selected row.</span></span> <span data-ttu-id="1b4e0-141">Bağlam menüsünden seçin **yedek alın**.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-141">From the context menu, select **Take backup**.</span></span>
   
    ![yedek alın gidin](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="1b4e0-143">İçinde **yedek alın** dikey penceresinde tıklatın **yedek alın**.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-143">In the **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="1b4e0-144">Bu dosya sunucusundaki tüm paylaşımlar veya iSCSI sunucunuzdaki tüm birimleri yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-144">This will backup all the shares on the file server or all the volumes on your iSCSI server.</span></span> 
   
    ![Başlangıç yedekleme](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="1b4e0-146">Bir talep üzerine yedekleme başlatılır ve bir yedekleme işi başlatıldığını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![Başlangıç yedekleme](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="1b4e0-148">İş başarıyla tamamlandıktan sonra yeniden bildirilir.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-148">Once the job has successfully completed, you are notified again.</span></span> <span data-ttu-id="1b4e0-149">Yedekleme işleminin ardından başlatır.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-149">The backup process then starts.</span></span>
   
    ![Yedekleme işi oluşturuldu](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="1b4e0-151">Yedeklemeleri ilerlemesini izlemek ve iş ayrıntılarını inceleyin için bildirime tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-151">To track the progress of the backups and look at the job details, click the notification.</span></span> <span data-ttu-id="1b4e0-152">Bu, olanak sürer **iş ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-152">This takes you to  **Job details**.</span></span>
   
     ![yedekleme işi ayrıntıları](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="1b4e0-154">Yedekleme tamamlandıktan sonra Git **Yönetim > Yedekleme kataloğu**.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-154">After the backup is complete, go to **Management > Backup catalog**.</span></span> <span data-ttu-id="1b4e0-155">Cihazınızda bir bulut anlık görüntüsü tüm paylaşımlar (veya birimleri) görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-155">You will see a cloud snapshot of all the shares (or volumes) on your device.</span></span>
   
    ![Tamamlanan yedekleme](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="1b4e0-157">Var olan yedekleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="1b4e0-157">View existing backups</span></span>
<span data-ttu-id="1b4e0-158">Var olan yedekleri görüntülemek için Azure portalında aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-158">To view the existing backups, perform the following steps in the Azure portal.</span></span>

#### <a name="to-view-existing-backups"></a><span data-ttu-id="1b4e0-159">Var olan yedekleri görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="1b4e0-159">To view existing backups</span></span>

1. <span data-ttu-id="1b4e0-160">Git **aygıtları** dikey.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-160">Go to **Devices** blade.</span></span> <span data-ttu-id="1b4e0-161">Seçin ve aygıtınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-161">Select and click your device.</span></span> <span data-ttu-id="1b4e0-162">İçinde **ayarları** dikey penceresinde, Git **Yönetim > Yedekleme kataloğu**.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-162">In the **Settings** blade, go to **Management > Backup Catalog**.</span></span>
   
    ![Yedekleme Kataloğu'na gidin](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="1b4e0-164">Filtreleme için kullanılmak üzere aşağıdaki ölçütleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="1b4e0-164">Specify the following criteria to be used for filtering:</span></span>
   
    - <span data-ttu-id="1b4e0-165">**Zaman aralığı** – olabilir **son 1 saat**, **son 24 saat**, **son 7 gün**, **son 30 gündeki**, **geçen yıl** , ve **özel tarih**.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="1b4e0-166">**Aygıtları** – dosya sunucuları, StorSimple cihaz Yöneticisi hizmetine kayıtlı iSCSI sunucuları veya listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-166">**Devices** – select from the list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="1b4e0-167">**Başlatılan** – otomatik olarak **zamanlanmış** (göre bir yedekleme İlkesi) veya **el ile** (sizin tarafınızdan) başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Filtre yedekleri](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="1b4e0-169">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-169">Click **Apply**.</span></span> <span data-ttu-id="1b4e0-170">Yedeklemeleri filtrelenmiş listesi görüntülenir **yedekleme kataloğu** dikey.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-170">The filtered list of backups is displayed in the **Backup catalog** blade.</span></span> <span data-ttu-id="1b4e0-171">Not yalnızca 100 yedekleme öğeleri belirli bir zamanda görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="1b4e0-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Güncelleştirilmiş yedekleme kataloğu](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="1b4e0-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1b4e0-173">Next steps</span></span>

<span data-ttu-id="1b4e0-174">Daha fazla bilgi edinmek [StorSimple sanal dizinizi yönetme](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="1b4e0-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

