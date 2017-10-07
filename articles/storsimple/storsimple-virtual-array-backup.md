---
title: "aaaMicrosoft Azure StorSimple sanal dizinin yedekleme Öğreticisi | Microsoft Docs"
description: "StorSimple sanal dizinin yukarı tooback nasıl paylaşımları ve birimler açıklar."
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
ms.openlocfilehash: 7a015fd594f8f56c48fab149a2736be9dec2c24b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-shares-or-volumes-on-your-storsimple-virtual-array"></a><span data-ttu-id="58106-103">Paylaşımlar veya birimler, StorSimple sanal dizisinde yedekle</span><span class="sxs-lookup"><span data-stu-id="58106-103">Back up shares or volumes on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="58106-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="58106-104">Overview</span></span>

<span data-ttu-id="58106-105">Merhaba StorSimple sanal dizinin bir dosya sunucusu veya bir iSCSI sunucusu yapılandırılmış bir karma bulut depolama şirket içi sanal cihazdır.</span><span class="sxs-lookup"><span data-stu-id="58106-105">hello StorSimple Virtual Array is a hybrid cloud storage on-premises virtual device that can be configured as a file server or an iSCSI server.</span></span> <span data-ttu-id="58106-106">Merhaba sanal dizinin hello kullanıcı toocreate hello cihazda zamanlanmış ve el ile yedeklerini tüm hello paylaşımları veya birimler izin verir.</span><span class="sxs-lookup"><span data-stu-id="58106-106">hello virtual array allows hello user toocreate scheduled and manual backups of all hello shares or volumes on hello device.</span></span> <span data-ttu-id="58106-107">Dosya sunucusu olarak yapılandırıldığında, öğe düzeyinde kurtarma de sağlar.</span><span class="sxs-lookup"><span data-stu-id="58106-107">When configured as a file server, it also allows item-level recovery.</span></span> <span data-ttu-id="58106-108">Bu öğretici nasıl toocreate zamanlanmış ve el ile yedekleme açıklar ve öğe düzeyinde kurtarma toorestore sanal dizisindeki silinmiş bir dosyayı gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="58106-108">This tutorial describes how toocreate scheduled and manual backups and perform item-level recovery toorestore a deleted file on your virtual array.</span></span>

<span data-ttu-id="58106-109">Bu öğretici toohello StorSimple sanal diziler yalnızca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="58106-109">This tutorial applies toohello StorSimple Virtual Arrays only.</span></span> <span data-ttu-id="58106-110">8000 serisi hakkında daha fazla bilgi için çok gidin[8000 serisi aygıtı için bir yedekleme oluşturmak](storsimple-manage-backup-policies-u2.md)</span><span class="sxs-lookup"><span data-stu-id="58106-110">For information on 8000 series, go too[Create a backup for 8000 series device](storsimple-manage-backup-policies-u2.md)</span></span>

## <a name="back-up-shares-and-volumes"></a><span data-ttu-id="58106-111">Paylaşımları ve birimler yedekleme</span><span class="sxs-lookup"><span data-stu-id="58106-111">Back up shares and volumes</span></span>

<span data-ttu-id="58106-112">Yedeklemeleri zaman noktası korumasını sağlar, kurtarılabilirliği iyileştirmeye ve paylaşımları ve birimler için geri yükleme sürelerini en aza.</span><span class="sxs-lookup"><span data-stu-id="58106-112">Backups provide point-in-time protection, improve recoverability, and minimize restore times for shares and volumes.</span></span> <span data-ttu-id="58106-113">StorSimple Cihazınızda iki yolla paylaşımı veya birimi yedekleyebilirsiniz: **zamanlanmış** veya **el ile**.</span><span class="sxs-lookup"><span data-stu-id="58106-113">You can back up a share or volume on your StorSimple device in two ways: **Scheduled** or **Manual**.</span></span> <span data-ttu-id="58106-114">Merhaba yöntemlerin her biri aşağıdaki bölümlerde hello ele alınmıştır.</span><span class="sxs-lookup"><span data-stu-id="58106-114">Each of hello methods is discussed in hello following sections.</span></span>

## <a name="change-hello-backup-start-time"></a><span data-ttu-id="58106-115">Merhaba yedekleme başlangıç saatini değiştir</span><span class="sxs-lookup"><span data-stu-id="58106-115">Change hello backup start time</span></span>

> [!NOTE]
> <span data-ttu-id="58106-116">Bu sürümde, zamanlanmış yedeklemeler, her gün belirtilen zamanda çalışan ve tüm hello paylaşımlar veya birimler hello aygıtta yedekler varsayılan bir ilke tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="58106-116">In this release, scheduled backups are created by a default policy that runs daily at a specified time and backs up all hello shares or volumes on hello device.</span></span> <span data-ttu-id="58106-117">Şu olası toocreate özel ilkeler zamanlanmış yedeklemeler için şu anda değil.</span><span class="sxs-lookup"><span data-stu-id="58106-117">It is not possible toocreate custom policies for scheduled backups at this time.</span></span>


<span data-ttu-id="58106-118">StorSimple sanal dizinizi (22:30) günün belirli bir zamanda başlatır ve tüm hello paylaşımlar veya birimler hello aygıtta günde bir kez yedekler varsayılan yedekleme ilkesine sahip.</span><span class="sxs-lookup"><span data-stu-id="58106-118">Your StorSimple Virtual Array has a default backup policy that starts at a specified time of day (22:30) and backs up all hello shares or volumes on hello device once a day.</span></span> <span data-ttu-id="58106-119">Hangi hello yedekleme başlatır, ancak hello sıklığı ve hello (hangi yedeklemeleri tooretain hello sayısını belirtir) bekletme değiştirilemez hello zaman değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58106-119">You can change hello time at which hello backup starts, but hello frequency and hello retention (which specifies hello number of backups tooretain) cannot be changed.</span></span> <span data-ttu-id="58106-120">Bu yedeklemeler sırasında tüm sanal aygıt hello desteklenir.</span><span class="sxs-lookup"><span data-stu-id="58106-120">During these backups, hello entire virtual device is backed up.</span></span> <span data-ttu-id="58106-121">Bu olası hello aygıt hello performansını etkileyebilir ve hello cihazda dağıtılan hello iş yükleri etkiler.</span><span class="sxs-lookup"><span data-stu-id="58106-121">This could potentially impact hello performance of hello device and affect hello workloads deployed on hello device.</span></span> <span data-ttu-id="58106-122">Bu nedenle, bu yedeklemeler için yoğun olmayan saatler zamanlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="58106-122">Therefore, we recommend that you schedule these backups for off-peak hours.</span></span>

 <span data-ttu-id="58106-123">toochange hello varsayılan yedekleme başlangıç zamanı, başlangıç adımlarını izleyerek hello gerçekleştirmek [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="58106-123">toochange hello default backup start time, perform hello following steps in hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="toochange-hello-start-time-for-hello-default-backup-policy"></a><span data-ttu-id="58106-124">toochange hello için başlangıç saatini hello varsayılan yedekleme İlkesi</span><span class="sxs-lookup"><span data-stu-id="58106-124">toochange hello start time for hello default backup policy</span></span>

1. <span data-ttu-id="58106-125">Çok Git**aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="58106-125">Go too**Devices**.</span></span> <span data-ttu-id="58106-126">StorSimple cihaz Yöneticisi hizmetiniz ile kayıtlı cihazların Merhaba listesi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="58106-126">hello list of devices registered with your StorSimple Device Manager service will be displayed.</span></span> 
   
    ![toodevices gidin](./media/storsimple-virtual-array-backup/changebuschedule1.png)

2. <span data-ttu-id="58106-128">Seçin ve aygıtınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="58106-128">Select and click your device.</span></span> <span data-ttu-id="58106-129">Merhaba **ayarları** dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="58106-129">hello **Settings** blade will be displayed.</span></span> <span data-ttu-id="58106-130">Çok Git**Yönet > Yedekleme ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="58106-130">Go too**Manage > Backup policies**.</span></span>
   
    ![Cihazınızı seçin](./media/storsimple-virtual-array-backup/changebuschedule2.png)

3. <span data-ttu-id="58106-132">Merhaba, **yedekleme ilkeleri** dikey penceresinde hello varsayılan başlangıç zamanı, 22:30.</span><span class="sxs-lookup"><span data-stu-id="58106-132">In hello **Backup policies** blade, hello default start time is 22:30.</span></span> <span data-ttu-id="58106-133">Aygıt saat diliminde hello yeni başlangıç saati hello günlük zamanlama için belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58106-133">You can specify hello new start time for hello daily schedule in device time zone.</span></span>
   
    ![toobackup ilkeleri gidin](./media/storsimple-virtual-array-backup/changebuschedule5.png)

4. <span data-ttu-id="58106-135">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="58106-135">Click **Save**.</span></span>

### <a name="take-a-manual-backup"></a><span data-ttu-id="58106-136">El ile yedekleyin</span><span class="sxs-lookup"><span data-stu-id="58106-136">Take a manual backup</span></span>

<span data-ttu-id="58106-137">Ayrıca tooscheduled yedeklemeler, herhangi bir zamanda el ile (isteğe bağlı) yedekleme aygıtı veri alabilir.</span><span class="sxs-lookup"><span data-stu-id="58106-137">In addition tooscheduled backups, you can take a manual (on-demand) backup of device data at any time.</span></span>

#### <a name="toocreate-a-manual-backup"></a><span data-ttu-id="58106-138">toocreate el ile yedekleme</span><span class="sxs-lookup"><span data-stu-id="58106-138">toocreate a manual backup</span></span>

1. <span data-ttu-id="58106-139">Çok Git**aygıtları**.</span><span class="sxs-lookup"><span data-stu-id="58106-139">Go too**Devices**.</span></span> <span data-ttu-id="58106-140">Cihazınızı seçin ve sağ **...**  en sağdaki hello hello Seçili satırda.</span><span class="sxs-lookup"><span data-stu-id="58106-140">Select your device and right-click **...** at hello far right in hello selected row.</span></span> <span data-ttu-id="58106-141">Merhaba bağlam menüsünden seçin **yedek alın**.</span><span class="sxs-lookup"><span data-stu-id="58106-141">From hello context menu, select **Take backup**.</span></span>
   
    ![tootake yedekleme gidin](./media/storsimple-virtual-array-backup/takebackup1m.png)

2. <span data-ttu-id="58106-143">Merhaba, **yedek alın** dikey penceresinde tıklatın **yedek alın**.</span><span class="sxs-lookup"><span data-stu-id="58106-143">In hello **Take backup** blade, click **Take backup**.</span></span> <span data-ttu-id="58106-144">Bu işlem hello dosya sunucusundaki tüm hello paylaşımları veya iSCSI sunucunuzdaki tüm hello birimleri yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="58106-144">This will backup all hello shares on hello file server or all hello volumes on your iSCSI server.</span></span> 
   
    ![Başlangıç yedekleme](./media/storsimple-virtual-array-backup/takebackup2m.png)
   
    <span data-ttu-id="58106-146">Bir talep üzerine yedekleme başlatılır ve bir yedekleme işi başlatıldığını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58106-146">An on-demand backup starts and you see that a backup job has started.</span></span>
   
    ![Başlangıç yedekleme](./media/storsimple-virtual-array-backup/takebackup3m.png) 
   
    <span data-ttu-id="58106-148">Merhaba iş başarıyla tamamlandıktan sonra yeniden bildirilir.</span><span class="sxs-lookup"><span data-stu-id="58106-148">Once hello job has successfully completed, you are notified again.</span></span> <span data-ttu-id="58106-149">Merhaba Yedekleme işleminin ardından başlatır.</span><span class="sxs-lookup"><span data-stu-id="58106-149">hello backup process then starts.</span></span>
   
    ![Yedekleme işi oluşturuldu](./media/storsimple-virtual-array-backup/takebackup4m.png)

3. <span data-ttu-id="58106-151">tootrack hello ilerlemesini hello iş ayrıntılarına bakın ve hello yedeklemeler hello bildirim'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="58106-151">tootrack hello progress of hello backups and look at hello job details, click hello notification.</span></span> <span data-ttu-id="58106-152">Bu, çok sürer **iş ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="58106-152">This takes you too **Job details**.</span></span>
   
     ![yedekleme işi ayrıntıları](./media/storsimple-virtual-array-backup/takebackup5m.png)

4. <span data-ttu-id="58106-154">Merhaba Yedekleme tamamlandıktan sonra çok Git**Yönetim > Yedekleme kataloğu**.</span><span class="sxs-lookup"><span data-stu-id="58106-154">After hello backup is complete, go too**Management > Backup catalog**.</span></span> <span data-ttu-id="58106-155">Cihazınızda bir bulut anlık görüntüsü tüm hello paylaşımları (veya birimleri) görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="58106-155">You will see a cloud snapshot of all hello shares (or volumes) on your device.</span></span>
   
    ![Tamamlanan yedekleme](./media/storsimple-virtual-array-backup/takebackup19m.png) 

## <a name="view-existing-backups"></a><span data-ttu-id="58106-157">Var olan yedekleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="58106-157">View existing backups</span></span>
<span data-ttu-id="58106-158">tooview hello var olan yedekleri, hello Azure Portalı'ndaki adımları izleyerek hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="58106-158">tooview hello existing backups, perform hello following steps in hello Azure portal.</span></span>

#### <a name="tooview-existing-backups"></a><span data-ttu-id="58106-159">tooview var olan yedekleri</span><span class="sxs-lookup"><span data-stu-id="58106-159">tooview existing backups</span></span>

1. <span data-ttu-id="58106-160">Çok Git**aygıtları** dikey.</span><span class="sxs-lookup"><span data-stu-id="58106-160">Go too**Devices** blade.</span></span> <span data-ttu-id="58106-161">Seçin ve aygıtınızı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="58106-161">Select and click your device.</span></span> <span data-ttu-id="58106-162">Merhaba, **ayarları** dikey penceresinde çok Git**Yönetim > Yedekleme kataloğu**.</span><span class="sxs-lookup"><span data-stu-id="58106-162">In hello **Settings** blade, go too**Management > Backup Catalog**.</span></span>
   
    ![Toobackup katalog gidin](./media/storsimple-virtual-array-backup/viewbackups1.png)
2. <span data-ttu-id="58106-164">Filtreleme için kullanılan ölçüt toobe aşağıdaki hello belirtin:</span><span class="sxs-lookup"><span data-stu-id="58106-164">Specify hello following criteria toobe used for filtering:</span></span>
   
    - <span data-ttu-id="58106-165">**Zaman aralığı** – olabilir **son 1 saat**, **son 24 saat**, **son 7 gün**, **son 30 gündeki**, **geçen yıl** , ve **özel tarih**.</span><span class="sxs-lookup"><span data-stu-id="58106-165">**Time range** – can be **Past 1 hour**, **Past 24 hours**, **Past 7 days**, **Past 30 days**, **Past year**, and **Custom date**.</span></span>
    
    - <span data-ttu-id="58106-166">**Aygıtları** – dosya sunucularında veya iSCSI sunucuları, StorSimple cihaz Yöneticisi hizmetine kayıtlı hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="58106-166">**Devices** – select from hello list of file servers or iSCSI servers registered with your StorSimple Device Manager service.</span></span>
   
    - <span data-ttu-id="58106-167">**Başlatılan** – otomatik olarak **zamanlanmış** (göre bir yedekleme İlkesi) veya **el ile** (sizin tarafınızdan) başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="58106-167">**Initiated** – can be automatically **Scheduled** (by a backup policy) or **Manually** initiated (by you).</span></span>
   
    ![Filtre yedekleri](./media/storsimple-virtual-array-backup/viewbackups2.png)

3. <span data-ttu-id="58106-169">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="58106-169">Click **Apply**.</span></span> <span data-ttu-id="58106-170">Merhaba filtrelenmiş listesi yedeklemeleri hello görüntülenir **yedekleme kataloğu** dikey.</span><span class="sxs-lookup"><span data-stu-id="58106-170">hello filtered list of backups is displayed in hello **Backup catalog** blade.</span></span> <span data-ttu-id="58106-171">Not yalnızca 100 yedekleme öğeleri belirli bir zamanda görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="58106-171">Note only 100 backup elements can be displayed at a given time.</span></span>
   
    ![Güncelleştirilmiş yedekleme kataloğu](./media/storsimple-virtual-array-backup/viewbackups3.png)

## <a name="next-steps"></a><span data-ttu-id="58106-173">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="58106-173">Next steps</span></span>

<span data-ttu-id="58106-174">Daha fazla bilgi edinmek [StorSimple sanal dizinizi yönetme](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="58106-174">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

