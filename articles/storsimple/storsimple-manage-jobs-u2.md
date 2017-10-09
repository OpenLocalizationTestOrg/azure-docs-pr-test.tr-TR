---
title: "aaaView ve StorSimple işlerini yönetme | Microsoft Docs"
description: "Merhaba StorSimple Yöneticisi hizmeti işleri sayfasında açıklar ve nasıl toouse, tootrack son, geçerli ve zamanlanmış yedekleme işleri."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a><span data-ttu-id="c1cc7-103">Merhaba StorSimple Yöneticisi hizmet tooview kullanma ve StorSimple işleri (güncelleştirme 2) yönetme</span><span class="sxs-lookup"><span data-stu-id="c1cc7-103">Use hello StorSimple Manager service tooview and manage StorSimple jobs (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a><span data-ttu-id="c1cc7-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c1cc7-104">Overview</span></span>
<span data-ttu-id="c1cc7-105">Merhaba **işleri** sayfasını görüntülemek için tek bir merkezi portal sağlar ve cihazlarda başlatılmış işlerini yönetme bağlı tooyour StorSimple Yöneticisi hizmeti.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-105">hello **Jobs** page provides a single central portal for viewing and managing jobs that were started on devices connected tooyour StorSimple Manager service.</span></span> <span data-ttu-id="c1cc7-106">Birden çok aygıt zamanlanmış, çalışan, tamamlandı, iptal edilmiş ve başarısız işleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="c1cc7-107">Sonuçları bir tablo biçiminde sunulur.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-107">Results are presented in a tabular format.</span></span> 

![İşler sayfası](./media/storsimple-manage-jobs-u2/jobs.png)

<span data-ttu-id="c1cc7-109">Hızlı bir şekilde hello işleri, içinde alanları gibi filtreleyerek ilginizi çekiyor mu bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c1cc7-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="c1cc7-110">**Durum** – işleri çalıştırıyor olabilir, tamamlandı, iptal edilmiş, başarısız, iptal etme veya hatalarla tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-110">**Status** – Jobs can be running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="c1cc7-111">**Başlangıç ve bitiş** – işleri filtrelenmiş göre hello tarih ve saat aralığı olabilir.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-111">**From and To** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="c1cc7-112">**Türü** – hello iş türü yedekleme, el ile yedekleme, geri yükleme, kopyalama, aygıt yük devretme, yerel olarak sabitlenmiş birim oluşturma, birim değiştirmek, Güncelleştir, paket veya sanal cihaz sağlamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-112">**Type** – hello job type can be backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
* <span data-ttu-id="c1cc7-113">**Aygıtları** – işleri belirli bağlı cihaz tooyour'nda bir hizmeti başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-113">**Devices** – Jobs are initiated on a certain device connected tooyour service.</span></span>
  <span data-ttu-id="c1cc7-114">Merhaba filtrelenen işler sonra öznitelikleri aşağıdaki hello hello temelinde tabloda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c1cc7-114">hello filtered jobs are then tabulated on hello basis of hello following attributes:</span></span>
  
  * <span data-ttu-id="c1cc7-115">**Tür** – yedekleme, el ile yedekleme, geri yükleme, kopyalama, aygıt yük devretme, yerel olarak sabitlenmiş birim oluşturma, birim değiştirmek, Güncelleştir, paket veya sanal cihaz sağlamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-115">**Type** – backup, manual backup, restore, clone, device failover, create locally pinned volume, modify volume, update, support package, or virtual device provisioning.</span></span>
  * <span data-ttu-id="c1cc7-116">**Durum** – çalışan, tamamlandı, iptal edilmiş, başarısız, iptal etme veya hatalarla tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-116">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
  * <span data-ttu-id="c1cc7-117">**Varlık** – hello işleri bir birim, bir yedekleme İlkesi veya bir aygıt ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-117">**Entity** – hello jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="c1cc7-118">Örneğin, zamanlanmış bir yedekleme işi bir yedekleme ilkesiyle ilişkili iken bir kopya iş bir birimi ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-118">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="c1cc7-119">Bir aygıt iş olağanüstü durum kurtarma (DR) veya geri yükleme işleminin sonucu olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-119">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
  * <span data-ttu-id="c1cc7-120">**Aygıt** – hello üzerinde hangi hello işi başlatıldı hello aygıt adı.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-120">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="c1cc7-121">**Tarihinde başlayan** – hello zaman zaman hello işi başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-121">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="c1cc7-122">**İlerleme** – hello tamamlanma çalışan işin.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-122">**Progress** – hello percentage completion of a running job.</span></span> <span data-ttu-id="c1cc7-123">Tamamlanmış bir iş için bu her zaman % 100 olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-123">For a completed job, this should always be 100%.</span></span>

<span data-ttu-id="c1cc7-124">işlerini Hello listesi, her 30 saniyede yenilenir.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-124">hello list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="c1cc7-125">Bu sayfada iş ile ilgili eylemler aşağıdaki hello gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c1cc7-125">You can perform hello following job-related actions on this page:</span></span>

* <span data-ttu-id="c1cc7-126">İş ayrıntılarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="c1cc7-126">View job details</span></span>
* <span data-ttu-id="c1cc7-127">Bir işi iptal etme</span><span class="sxs-lookup"><span data-stu-id="c1cc7-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="c1cc7-128">İş ayrıntılarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="c1cc7-128">View job details</span></span>
<span data-ttu-id="c1cc7-129">Aşağıdaki adımları tooview hello herhangi bir işi ayrıntılarını hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-129">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="c1cc7-130">tooview iş ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="c1cc7-130">tooview job details</span></span>
1. <span data-ttu-id="c1cc7-131">Merhaba üzerinde **işleri** sayfasında, hello iş, ilgilendiğiniz uygun filtrelerle bir sorgu çalıştırarak görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-131">On hello **Jobs** page, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="c1cc7-132">Çalışan veya işi iptal tamamlandı için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-132">You can search for completed, running, or canceled jobs.</span></span>
2. <span data-ttu-id="c1cc7-133">Bir iş seçin.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-133">Select a job.</span></span>
3. <span data-ttu-id="c1cc7-134">Merhaba sayfasının Hello altında tıklatın **ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-134">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="c1cc7-135">Merhaba, **yedekleme işi ayrıntılarını** iletişim kutusu, hello durumu, ayrıntıları, süresi istatistikleri ve veri istatistiklerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-135">In hello **Backup Job Details** dialog box, you can view hello status, details, time statistics, and data statistics.</span></span>
   
    ![İş Ayrıntıları sayfası](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a><span data-ttu-id="c1cc7-137">Bir işi iptal etme</span><span class="sxs-lookup"><span data-stu-id="c1cc7-137">Cancel a job</span></span>
<span data-ttu-id="c1cc7-138">Aşağıdaki adımları toocancel çalışan bir işi hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-138">Perform hello following steps toocancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="c1cc7-139">Bir birim toochange hello birim türü değiştirme veya bir birim genişletme gibi bazı işleri iptal edilemez.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-139">Some jobs, such as modifying a volume toochange hello volume type or expanding a volume, cannot be canceled.</span></span>
> 
> 

### <a name="toocancel-a-job"></a><span data-ttu-id="c1cc7-140">toocancel bir işi</span><span class="sxs-lookup"><span data-stu-id="c1cc7-140">toocancel a job</span></span>
1. <span data-ttu-id="c1cc7-141">Merhaba üzerinde **işleri** sayfasında, uygun filtrelerle bir sorgu çalıştırarak toocancel istediğiniz hello çalışan iş görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-141">On hello **Jobs** page, display hello running job(s) that you want toocancel by running a query with appropriate filters.</span></span>
2. <span data-ttu-id="c1cc7-142">Merhaba işi seçin.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-142">Select hello job.</span></span>
3. <span data-ttu-id="c1cc7-143">Merhaba sayfasının Hello altında tıklatın **iptal**.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-143">At hello bottom of hello page, click **Cancel**.</span></span>
4. <span data-ttu-id="c1cc7-144">Onayınız istendiğinde **Evet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-144">When prompted for confirmation, click **Yes**.</span></span>

<span data-ttu-id="c1cc7-145">Bu işi iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="c1cc7-145">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1cc7-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c1cc7-146">Next steps</span></span>
* <span data-ttu-id="c1cc7-147">Nasıl çok öğrenin[, StorSimple yedekleme ilkelerini yönetme](storsimple-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c1cc7-147">Learn how too[manage your StorSimple backup policies](storsimple-manage-backup-policies.md).</span></span>
* <span data-ttu-id="c1cc7-148">Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c1cc7-148">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

