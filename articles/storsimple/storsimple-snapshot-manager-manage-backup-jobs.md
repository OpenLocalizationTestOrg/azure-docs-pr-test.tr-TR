---
title: "aaaStorSimple anlık görüntü Yöneticisi'ni yedekleme işleri | Microsoft Docs"
description: "Toouse StorSimple Snapshot Manager MMC ek bileşenini tooview hello ve zamanlanmış, çalışmakta ve tamamlanan yedekleme işlerini yönetme nasıl açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bf4dcff6-c819-4766-b9d9-9922831cb200
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 3dba0a2aa527d17d67130f537bcdce5722b05a76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-backup-jobs"></a><span data-ttu-id="7bb29-103">StorSimple Snapshot Manager tooview kullanma ve yedekleme işlerini yönetme</span><span class="sxs-lookup"><span data-stu-id="7bb29-103">Use StorSimple Snapshot Manager tooview and manage backup jobs</span></span>

## <a name="overview"></a><span data-ttu-id="7bb29-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7bb29-104">Overview</span></span>
<span data-ttu-id="7bb29-105">Merhaba **işleri** hello düğümünde **kapsam** bölmesinde gösterilir hello **zamanlanmış**, **son 24 saat**, ve **çalıştıran**yedekleme etkileşimli olarak veya yapılandırılmış bir ilke tarafından başlatılan görev.</span><span class="sxs-lookup"><span data-stu-id="7bb29-105">hello **Jobs** node in hello **Scope** pane shows hello **Scheduled**, **Last 24 hours**, and **Running** backup tasks that you initiated interactively or by a configured policy.</span></span> 

<span data-ttu-id="7bb29-106">Bu öğretici hello nasıl kullanabileceğinizi açıklar **işleri** zamanlanmış, son ve şu anda çalışan yedekleme işleri hakkında düğümü toodisplay bilgi.</span><span class="sxs-lookup"><span data-stu-id="7bb29-106">This tutorial explains how you can use hello **Jobs** node toodisplay information about scheduled, recent, and currently running backup jobs.</span></span> <span data-ttu-id="7bb29-107">(Merhaba listesi işler ve ilgili bilgiler görüntülenir hello **sonuçları** bölmesinde.) Ayrıca, listelenen işini sağ tıklatın ve kullanılabilir eylemler listeleyen bir bağlam menüsü bakın.</span><span class="sxs-lookup"><span data-stu-id="7bb29-107">(hello list of jobs and corresponding information appears in hello **Results** pane.) Additionally, you can right-click a listed job and see a context menu that lists available actions.</span></span>

## <a name="view-scheduled-jobs"></a><span data-ttu-id="7bb29-108">Zamanlanan işleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="7bb29-108">View scheduled jobs</span></span>
<span data-ttu-id="7bb29-109">Aşağıdaki yordam tooview zamanlanmış yedekleme işlerini hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="7bb29-109">Use hello following procedure tooview scheduled backup jobs.</span></span>

#### <a name="tooview-scheduled-jobs"></a><span data-ttu-id="7bb29-110">Zamanlanmış tooview işleri</span><span class="sxs-lookup"><span data-stu-id="7bb29-110">tooview scheduled jobs</span></span>
1. <span data-ttu-id="7bb29-111">Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7bb29-111">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="7bb29-112">Merhaba, **kapsam** bölmesinde hello genişletin **işleri** düğümü ve tıklatın **zamanlanmış**.</span><span class="sxs-lookup"><span data-stu-id="7bb29-112">In hello **Scope** pane, expand hello **Jobs** node, and click **Scheduled**.</span></span> <span data-ttu-id="7bb29-113">Merhaba aşağıdaki bilgiler görüntülenir hello **sonuçları** bölmesi:</span><span class="sxs-lookup"><span data-stu-id="7bb29-113">hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="7bb29-114">**Ad** – hello hello zamanlanmış anlık görüntü adı</span><span class="sxs-lookup"><span data-stu-id="7bb29-114">**Name** – hello name of hello scheduled snapshot</span></span>
   * <span data-ttu-id="7bb29-115">**Sonraki çalıştırma** – hello tarih ve saat hello sonraki zamanlanmış anlık görüntüsünün</span><span class="sxs-lookup"><span data-stu-id="7bb29-115">**Next Run** – hello date and time of hello next scheduled snapshot</span></span>
   * <span data-ttu-id="7bb29-116">**Son çalıştırma** – hello tarih ve saat hello en son zamanlanmış anlık görüntü</span><span class="sxs-lookup"><span data-stu-id="7bb29-116">**Last Run** – hello date and time of hello most recent scheduled snapshot</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="7bb29-117">Tek seferlik yalnızca anlık görüntüler için hello **sonraki çalıştırmaya** ve **son çalıştırma** aynı hello olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7bb29-117">For one-time only snapshots, hello **Next Run** and **Last Run** will be hello same.</span></span>
     
     ![Zamanlanmış yedekleme işleri](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_scheduled.png) 
3. <span data-ttu-id="7bb29-119">belirli bir iş üzerinde tooperform ek eylemleri sağ hello hello iş adı **sonuçları** bölmesinde ve hello menü seçeneklerini seçin.</span><span class="sxs-lookup"><span data-stu-id="7bb29-119">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="view-recent-jobs"></a><span data-ttu-id="7bb29-120">Son işleri görüntüle</span><span class="sxs-lookup"><span data-stu-id="7bb29-120">View recent jobs</span></span>
<span data-ttu-id="7bb29-121">Aşağıdaki yordam tooview yedekleme hello kullanın ve hello son 24 saat tamamlandığını işleri geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7bb29-121">Use hello following procedure tooview backup and restore jobs that were completed in hello last 24 hours.</span></span>

#### <a name="tooview-recent-jobs"></a><span data-ttu-id="7bb29-122">tooview en son işlerin</span><span class="sxs-lookup"><span data-stu-id="7bb29-122">tooview recent jobs</span></span>
1. <span data-ttu-id="7bb29-123">Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7bb29-123">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="7bb29-124">Merhaba, **kapsam** bölmesinde hello genişletin **işleri** düğümü ve tıklatın **son 24 saat**.</span><span class="sxs-lookup"><span data-stu-id="7bb29-124">In hello **Scope** pane, expand hello **Jobs** node, and click **Last 24 hours**.</span></span> <span data-ttu-id="7bb29-125">Merhaba **sonuçları** bölmesi hello yedekleme işlerini son 24 saat (64 işleri tooa maksimum) gösterir.</span><span class="sxs-lookup"><span data-stu-id="7bb29-125">hello **Results** pane shows backup jobs for hello last 24 hours (tooa maximum of 64 jobs).</span></span> <span data-ttu-id="7bb29-126">Merhaba aşağıdaki bilgiler görüntülenir hello **sonuçları** bağlı olarak hello bölmesini **Görünüm** belirlediğiniz seçenekleri:</span><span class="sxs-lookup"><span data-stu-id="7bb29-126">hello following information appears in hello **Results** pane, depending on hello **View** options you specify:</span></span>
   
   * <span data-ttu-id="7bb29-127">**Ad** – hello hello zamanlanmış anlık görüntü adı.</span><span class="sxs-lookup"><span data-stu-id="7bb29-127">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="7bb29-128">**Başlatılan** – hello tarih ve zaman hello anlık görüntü başladığı zaman.</span><span class="sxs-lookup"><span data-stu-id="7bb29-128">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="7bb29-129">**Durdurulmuş** – hello tarih ve zaman hello anlık görüntüsü tamamlandı veya sonlandırıldı zaman.</span><span class="sxs-lookup"><span data-stu-id="7bb29-129">**Stopped** – hello date and time when hello snapshot finished or was terminated.</span></span>
   * <span data-ttu-id="7bb29-130">**Geçen** – hello hello arasındaki süre miktarı **başlatıldı** ve **durduruldu** kez.</span><span class="sxs-lookup"><span data-stu-id="7bb29-130">**Elapsed** – hello amount of time between hello **Started** and **Stopped** times.</span></span>
   * <span data-ttu-id="7bb29-131">**Durum** – hello yakın zamanda tamamlandı hello iş durumu.</span><span class="sxs-lookup"><span data-stu-id="7bb29-131">**Status** – hello state of hello recently completed job.</span></span> <span data-ttu-id="7bb29-132">**Başarı** hello Yedekleme başarıyla oluşturulduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="7bb29-132">**Success** indicates that hello backup was created successfully.</span></span> <span data-ttu-id="7bb29-133">**Başarısız** o hello işi başarıyla çalışmadı gösterir.</span><span class="sxs-lookup"><span data-stu-id="7bb29-133">**Failed** indicates that hello job did not run successfully.</span></span>
   * <span data-ttu-id="7bb29-134">**Bilgi** – hello hello başarısızlık nedeni.</span><span class="sxs-lookup"><span data-stu-id="7bb29-134">**Information** – hello reason for hello failure.</span></span>
   * <span data-ttu-id="7bb29-135">**Bayt (MB) işlenen** – hello miktarını (MB) işlenmiş hello birim grubu verileri.</span><span class="sxs-lookup"><span data-stu-id="7bb29-135">**Bytes processed (MB)** – hello amount of data from hello volume group that was processed (in MBs).</span></span> 
     
     ![Son 24 saat hello çalışan işler](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_Last_24_hours.png) 
3. <span data-ttu-id="7bb29-137">belirli bir iş üzerinde tooperform ek eylemleri sağ hello hello iş adı **sonuçları** bölmesinde ve hello menü seçeneklerini seçin.</span><span class="sxs-lookup"><span data-stu-id="7bb29-137">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>
   
    ![Bir işi Sil](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Delete_backup.png)

## <a name="view-currently-running-jobs"></a><span data-ttu-id="7bb29-139">Şu anda çalışan işleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="7bb29-139">View currently running jobs</span></span>
<span data-ttu-id="7bb29-140">Şu anda çalışan yordamı tooview işleri aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="7bb29-140">Use hello following procedure tooview jobs that are currently running.</span></span>

#### <a name="tooview-currently-running-jobs"></a><span data-ttu-id="7bb29-141">şu anda çalışan işi tooview</span><span class="sxs-lookup"><span data-stu-id="7bb29-141">tooview currently running jobs</span></span>
1. <span data-ttu-id="7bb29-142">Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7bb29-142">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="7bb29-143">Merhaba, **kapsam** bölmesinde hello genişletin **işleri** düğümü ve tıklatın **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="7bb29-143">In hello **Scope** pane, expand hello **Jobs** node, and click **Running**.</span></span> <span data-ttu-id="7bb29-144">Merhaba bağlı olarak **Görünüm** belirttiğiniz bilgisinden hello görünür hello seçenekleri **sonuçları** bölmesi:</span><span class="sxs-lookup"><span data-stu-id="7bb29-144">Depending on hello **View** options you specify, hello following information appears in hello **Results** pane:</span></span>
   
   * <span data-ttu-id="7bb29-145">**Ad** – hello hello zamanlanmış anlık görüntü adı.</span><span class="sxs-lookup"><span data-stu-id="7bb29-145">**Name** – hello name of hello scheduled snapshot.</span></span>
   * <span data-ttu-id="7bb29-146">**Başlatılan** – hello tarih ve zaman hello anlık görüntü başladığı zaman.</span><span class="sxs-lookup"><span data-stu-id="7bb29-146">**Started** – hello date and time when hello snapshot began.</span></span>
   * <span data-ttu-id="7bb29-147">**Denetim noktası** – hello hello yedekleme geçerli eylem.</span><span class="sxs-lookup"><span data-stu-id="7bb29-147">**Checkpoint** – hello current action of hello backup.</span></span>
   * <span data-ttu-id="7bb29-148">**Durum** – hello tamamlanma yüzdesi.</span><span class="sxs-lookup"><span data-stu-id="7bb29-148">**Status** – hello percentage of completion.</span></span>
   * <span data-ttu-id="7bb29-149">**Geçen** – hello hello yedekleme başlamasından bu yana geçen süre miktarı.</span><span class="sxs-lookup"><span data-stu-id="7bb29-149">**Elapsed** – hello amount of time that has passed since hello backup began.</span></span> 
   * <span data-ttu-id="7bb29-150">**Ortalama verimi (MB)** – işlenen veri toothat (MB) işlenmesi için geçen toplam süre, toplam bayt oranı.</span><span class="sxs-lookup"><span data-stu-id="7bb29-150">**Average throughput (MB)** – ratio of total bytes of data processed toothat of total time taken for processing (MBs).</span></span>
   * <span data-ttu-id="7bb29-151">**Bayt (MB) işlenen** – toplam bayt (MB) işlenen veri.</span><span class="sxs-lookup"><span data-stu-id="7bb29-151">**Bytes processed (MB)** – total bytes of data processed (in MBs).</span></span>
   * <span data-ttu-id="7bb29-152">**(MB) yazılan bayt** – toplam bayt (MB) yazılan veri.</span><span class="sxs-lookup"><span data-stu-id="7bb29-152">**Bytes written (MB)** – total bytes of data written (in MBs).</span></span> <span data-ttu-id="7bb29-153">Merhaba veri yanı sıra hello meta verileri içerir ve bu nedenle hello bayt işlenen genellikle daha büyük.</span><span class="sxs-lookup"><span data-stu-id="7bb29-153">It includes hello data as well as hello metadata and hence is typically greater than hello Bytes Processed.</span></span>
     
     ![Şu anda çalışan işler](./media/storsimple-snapshot-manager-manage-backup-jobs/HCS_SSM_Jobs_running.png)
3. <span data-ttu-id="7bb29-155">belirli bir iş üzerinde tooperform ek eylemleri sağ hello hello iş adı **sonuçları** bölmesinde ve hello menü seçeneklerini seçin.</span><span class="sxs-lookup"><span data-stu-id="7bb29-155">tooperform additional actions on a specific job, right-click hello job name in hello **Results** pane and select from hello menu options.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bb29-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7bb29-156">Next steps</span></span>
* <span data-ttu-id="7bb29-157">Nasıl çok öğrenin[StorSimple Snapshot Manager tooadminister StorSimple çözümünüzün kullanmak](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="7bb29-157">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="7bb29-158">Nasıl çok öğrenin[StorSimple Snapshot Manager toomanage hello yedekleme Kataloğu'nu](storsimple-snapshot-manager-manage-backup-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="7bb29-158">Learn how too[use StorSimple Snapshot Manager toomanage hello backup catalog](storsimple-snapshot-manager-manage-backup-catalog.md).</span></span>

