---
title: "aaaView ve StorSimple 8000 serisi işleri yönetme | Microsoft Docs"
description: "Merhaba StorSimple cihaz Yöneticisi hizmeti işler dikey penceresinde açıklar ve nasıl toouse, tootrack son, geçerli ve zamanlanmış yedekleme işleri."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="acebe-103">Merhaba StorSimple cihaz Yöneticisi hizmeti tooview kullanma ve işleri (güncelleştirme 3 ve üzeri) yönetme</span><span class="sxs-lookup"><span data-stu-id="acebe-103">Use hello StorSimple Device Manager service tooview and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="acebe-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="acebe-104">Overview</span></span>
<span data-ttu-id="acebe-105">Merhaba **işleri** dikey penceresini görüntülemek için tek bir merkezi portal sağlar ve cihazlarda başlatılmış işlerini yönetme bağlı tooyour StorSimple cihaz Yöneticisi hizmeti.</span><span class="sxs-lookup"><span data-stu-id="acebe-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="acebe-106">Birden çok aygıt zamanlanmış, çalışan, tamamlandı, iptal edilmiş ve başarısız işleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acebe-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="acebe-107">Sonuçları bir tablo biçiminde sunulur.</span><span class="sxs-lookup"><span data-stu-id="acebe-107">Results are presented in a tabular format.</span></span>

![İşlerini dikey penceresi](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="acebe-109">Hızlı bir şekilde hello işleri, içinde alanları gibi filtreleyerek ilginizi çekiyor mu bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="acebe-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="acebe-110">**Durum** – işleri, başarılı, sürüyor, iptal edilmiş, başarısız, iptal etme veya ile başarılı oldu, hata olabilir.</span><span class="sxs-lookup"><span data-stu-id="acebe-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="acebe-111">**Zaman aralığı** – işleri filtrelenmiş göre hello tarih ve saat aralığı olabilir.</span><span class="sxs-lookup"><span data-stu-id="acebe-111">**Time range** – Jobs can be filtered based on hello date and time range.</span></span> <span data-ttu-id="acebe-112">Merhaba 1 saat, son 30 gün, önceki yıl veya özel tarihi geçmiş 7 gün 24 saat geçmiş geçmiş aralıktır.</span><span class="sxs-lookup"><span data-stu-id="acebe-112">hello ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="acebe-113">**Tür** – zamanlanmış yedekleme, el ile yedekleme, geri yükleme yedekleme hello iş türü olabilir kopyalama birimi, birim kapsayıcıları başarısız, yerel olarak sabitlenmiş birim oluşturma, birim değiştirmek, güncelleştirmeleri yüklemek, destek günlükleri toplamak ve bulut uygulaması oluşturma.</span><span class="sxs-lookup"><span data-stu-id="acebe-113">**Type** – hello job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="acebe-114">**Aygıtları** – işleri belirli bağlı cihaz tooyour'nda bir hizmeti başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="acebe-114">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  
<span data-ttu-id="acebe-115">Merhaba filtrelenen işler sonra öznitelikleri aşağıdaki hello hello temelinde tabloda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="acebe-115">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
* <span data-ttu-id="acebe-116">**Ad** – zamanlanmış yedekleme, yedekleme, geri yükleme yedekleme, kopya birim, başarısız birim kapsayıcıları el ile yerel olarak sabitlenmiş birim oluşturma, birim değiştirmek, güncelleştirmeleri yüklemek, destek günlükleri toplamak veya Bulut uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="acebe-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="acebe-117">**Durum** – çalışan, tamamlandı, iptal edilmiş, başarısız, iptal etme veya hatalarla tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="acebe-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="acebe-118">**Varlık** – hello işleri bir birim, bir yedekleme İlkesi veya bir aygıt ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="acebe-118">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="acebe-119">Örneğin, zamanlanmış bir yedekleme işi bir yedekleme ilkesiyle ilişkili iken bir kopya iş bir birimi ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="acebe-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="acebe-120">Bir aygıt iş olağanüstü durum kurtarma (DR) veya geri yükleme işleminin sonucu olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="acebe-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="acebe-121">**Aygıt** – hello üzerinde hangi hello işi başlatıldı hello aygıt adı.</span><span class="sxs-lookup"><span data-stu-id="acebe-121">**Device** – hello name of hello device on which hello job was started.</span></span>
* <span data-ttu-id="acebe-122">**Tarihinde başlayan** – hello zaman zaman hello işi başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="acebe-122">**Started on** – hello time when hello job was started.</span></span>
* <span data-ttu-id="acebe-123">**Süre** – hello süresi gerekli toocomplete hello işi.</span><span class="sxs-lookup"><span data-stu-id="acebe-123">**Duration** – hello time required toocomplete hello job.</span></span>

<span data-ttu-id="acebe-124">işlerini Hello listesi, her 30 saniyede yenilenir.</span><span class="sxs-lookup"><span data-stu-id="acebe-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="acebe-125">Bu sayfada iş ile ilgili eylemler aşağıdaki hello gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="acebe-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="acebe-126">İş ayrıntılarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="acebe-126">View job details</span></span>
* <span data-ttu-id="acebe-127">Bir işi iptal etme</span><span class="sxs-lookup"><span data-stu-id="acebe-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="acebe-128">İş ayrıntılarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="acebe-128">View job details</span></span>
<span data-ttu-id="acebe-129">Aşağıdaki adımları tooview hello herhangi bir işi ayrıntılarını hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="acebe-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="acebe-130">tooview iş ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="acebe-130">tooview job details</span></span>
1. <span data-ttu-id="acebe-131">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve ardından **işleri**.</span><span class="sxs-lookup"><span data-stu-id="acebe-131">Go tooyour StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="acebe-132">Merhaba, **işleri** dikey penceresinde, görüntü hello iş, ilgilendiğiniz uygun filtreleri ile çalışan bir sorgu.</span><span class="sxs-lookup"><span data-stu-id="acebe-132">In hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="acebe-133">Çalışan veya işi iptal tamamlandı için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acebe-133">You can search for completed, running, or canceled jobs.</span></span>

    ![İş dikey penceresi](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="acebe-135">Seçin ve bir iş'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="acebe-135">Select and click a job.</span></span>

    ![İş dikey penceresi](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="acebe-137">Merhaba iş ayrıntıları dikey penceresinde hello durumu, ayrıntıları, süresi istatistikleri ve veri istatistiklerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="acebe-137">In hello job details blade, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![İş ayrıntıları](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="acebe-139">Bir işi iptal etme</span><span class="sxs-lookup"><span data-stu-id="acebe-139">Cancel a job</span></span>
<span data-ttu-id="acebe-140">Aşağıdaki adımları toocancel çalışan bir işi hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="acebe-140">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="acebe-141">Bir birim toochange hello birim türü değiştirme veya bir birim genişletme gibi bazı işleri iptal edilemez.</span><span class="sxs-lookup"><span data-stu-id="acebe-141">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="toocancel-a-job"></a><span data-ttu-id="acebe-142">toocancel bir işi</span><span class="sxs-lookup"><span data-stu-id="acebe-142">toocancel a job</span></span>
1. <span data-ttu-id="acebe-143">Merhaba üzerinde **işleri** sayfasında, uygun filtrelerle bir sorgu çalıştırarak toocancel istediğiniz hello çalışan iş görüntüler.</span><span class="sxs-lookup"><span data-stu-id="acebe-143">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span> <span data-ttu-id="acebe-144">Merhaba işi seçin.</span><span class="sxs-lookup"><span data-stu-id="acebe-144">Select hello job.</span></span>

2. <span data-ttu-id="acebe-145">Merhaba Seçili iş tooinvoke hello bağlam menüsünde sağ tıklatın ve **iptal**.</span><span class="sxs-lookup"><span data-stu-id="acebe-145">Right-click on hello selected job tooinvoke hello context menu and click **Cancel**.</span></span>

    ![İş ayrıntıları](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="acebe-147">Onayınız istendiğinde **Evet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="acebe-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="acebe-148">Bu işi iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="acebe-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="acebe-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="acebe-149">Next steps</span></span>
* <span data-ttu-id="acebe-150">Nasıl çok öğrenin[, StorSimple yedekleme ilkelerini yönetme](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="acebe-150">Learn how too[manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="acebe-151">Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="acebe-151">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

