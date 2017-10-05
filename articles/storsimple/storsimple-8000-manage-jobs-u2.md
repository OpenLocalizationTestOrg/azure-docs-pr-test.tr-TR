---
title: "StorSimple 8000 serisi işleri görüntüle ve Yönet | Microsoft Docs"
description: "StorSimple cihaz Yöneticisi hizmeti işler dikey penceresinde ve son, geçerli ve zamanlanmış yedekleme işlerini izleme açıklar."
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
ms.openlocfilehash: bf8038b7171053b75eeb9aed88bff4246e65a8a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-device-manager-service-to-view-and-manage-jobs-update-3-and-later"></a><span data-ttu-id="eb506-103">Görüntülemek ve işleri (güncelleştirme 3 ve üzeri) yönetmek için StorSimple cihaz Yöneticisi hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="eb506-103">Use the StorSimple Device Manager service to view and manage jobs (Update 3 and later)</span></span>

## <a name="overview"></a><span data-ttu-id="eb506-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="eb506-104">Overview</span></span>
<span data-ttu-id="eb506-105">**İşleri** dikey penceresini görüntülemek için tek bir merkezi portal sağlar ve StorSimple cihaz Yöneticisi hizmetinize bağlı cihazlarda başlatılmış işlerini yönetme.</span><span class="sxs-lookup"><span data-stu-id="eb506-105">The **Jobs** blade provides a single central portal for viewing and managing jobs that were started on devices connected to your StorSimple Device Manager service.</span></span> <span data-ttu-id="eb506-106">Birden çok aygıt zamanlanmış, çalışan, tamamlandı, iptal edilmiş ve başarısız işleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb506-106">You can view scheduled, running, completed, canceled, and failed jobs for multiple devices.</span></span> <span data-ttu-id="eb506-107">Sonuçları bir tablo biçiminde sunulur.</span><span class="sxs-lookup"><span data-stu-id="eb506-107">Results are presented in a tabular format.</span></span>

![İşlerini dikey penceresi](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

<span data-ttu-id="eb506-109">Hızlı bir şekilde, içinde alanları gibi filtreleyerek ilginizi çekiyor mu işleri bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="eb506-109">You can quickly find the jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="eb506-110">**Durum** – işleri, başarılı, sürüyor, iptal edilmiş, başarısız, iptal etme veya ile başarılı oldu, hata olabilir.</span><span class="sxs-lookup"><span data-stu-id="eb506-110">**Status** – Jobs can be in progress, succeeded, canceled, failed, canceling, or succeeded with errors.</span></span>
* <span data-ttu-id="eb506-111">**Zaman aralığı** – işleri filtre tarih ve saat aralıklarına göre.</span><span class="sxs-lookup"><span data-stu-id="eb506-111">**Time range** – Jobs can be filtered based on the date and time range.</span></span> <span data-ttu-id="eb506-112">1 saat, son 30 gün, önceki yıl veya özel tarihi geçmiş 7 gün 24 saat geçmiş geçmiş aralıktır.</span><span class="sxs-lookup"><span data-stu-id="eb506-112">The ranges are past 1 hour, past 24 hours, past 7 days, past 30 days, past year, or custom date.</span></span>
* <span data-ttu-id="eb506-113">**Tür** – zamanlanmış yedekleme, el ile yedekleme, geri yükleme yedekleme iş türü olabilir kopyalama birimi, birim kapsayıcıları başarısız, yerel olarak sabitlenmiş birim oluşturma, birim değiştirmek, güncelleştirmeleri yüklemek, destek günlükleri toplamak ve bulut uygulaması oluşturma.</span><span class="sxs-lookup"><span data-stu-id="eb506-113">**Type** – The job type can be scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally-pinned volume, modify volume, install updates, collect support logs and create cloud appliance.</span></span>
* <span data-ttu-id="eb506-114">**Aygıtları** – işleri hizmetinize bağlanan bir aygıttaki belirli başlattı.</span><span class="sxs-lookup"><span data-stu-id="eb506-114">**Devices** – Jobs are initiated on a certain device connected to your service.</span></span>
  
<span data-ttu-id="eb506-115">Filtrelenen işler, ardından aşağıdaki öznitelikleri temel alınarak tabloda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="eb506-115">The filtered jobs are then tabulated on the basis of the following attributes:</span></span>
  
* <span data-ttu-id="eb506-116">**Ad** – zamanlanmış yedekleme, yedekleme, geri yükleme yedekleme, kopya birim, başarısız birim kapsayıcıları el ile yerel olarak sabitlenmiş birim oluşturma, birim değiştirmek, güncelleştirmeleri yüklemek, destek günlükleri toplamak veya Bulut uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eb506-116">**Name** – scheduled backup, manual backup, restore backup, clone volume, fail over volume containers, create locally pinned volume, modify volume, install updates, collect support logs, or create cloud appliance.</span></span>
* <span data-ttu-id="eb506-117">**Durum** – çalışan, tamamlandı, iptal edilmiş, başarısız, iptal etme veya hatalarla tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="eb506-117">**Status** – running, completed, canceled, failed, canceling, or completed with errors.</span></span>
* <span data-ttu-id="eb506-118">**Varlık** – işleri bir birim, bir yedekleme İlkesi veya bir aygıt ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="eb506-118">**Entity** – The jobs can be associated with a volume, a backup policy, or a device.</span></span> <span data-ttu-id="eb506-119">Örneğin, zamanlanmış bir yedekleme işi bir yedekleme ilkesiyle ilişkili iken bir kopya iş bir birimi ile ilişkilidir.</span><span class="sxs-lookup"><span data-stu-id="eb506-119">For example, a clone job is associated with a volume, whereas a scheduled backup job is associated with a backup policy.</span></span> <span data-ttu-id="eb506-120">Bir aygıt iş olağanüstü durum kurtarma (DR) veya geri yükleme işleminin sonucu olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eb506-120">A device job is created as a result of a disaster recovery (DR) or a restore operation.</span></span>
* <span data-ttu-id="eb506-121">**Aygıt** – işi başlatıldı aygıt adı.</span><span class="sxs-lookup"><span data-stu-id="eb506-121">**Device** – The name of the device on which the job was started.</span></span>
* <span data-ttu-id="eb506-122">**Tarihinde başlayan** – zaman zaman işi başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="eb506-122">**Started on** – The time when the job was started.</span></span>
* <span data-ttu-id="eb506-123">**Süre** – işi tamamlamak için gereken süre.</span><span class="sxs-lookup"><span data-stu-id="eb506-123">**Duration** – The time required to complete the job.</span></span>

<span data-ttu-id="eb506-124">İşlerin listesini her 30 saniyede yenilenir.</span><span class="sxs-lookup"><span data-stu-id="eb506-124">The list of jobs is refreshed every 30 seconds.</span></span>

<span data-ttu-id="eb506-125">Bu sayfada iş ile ilgili aşağıdaki eylemleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="eb506-125">You can perform the following job-related actions on this page:</span></span>

* <span data-ttu-id="eb506-126">İş ayrıntılarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="eb506-126">View job details</span></span>
* <span data-ttu-id="eb506-127">Bir işi iptal etme</span><span class="sxs-lookup"><span data-stu-id="eb506-127">Cancel a job</span></span>

## <a name="view-job-details"></a><span data-ttu-id="eb506-128">İş ayrıntılarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="eb506-128">View job details</span></span>
<span data-ttu-id="eb506-129">Herhangi bir işi ayrıntılarını görüntülemek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="eb506-129">Perform the following steps to view the details of any job.</span></span>

#### <a name="to-view-job-details"></a><span data-ttu-id="eb506-130">İş ayrıntılarını görüntülemek için</span><span class="sxs-lookup"><span data-stu-id="eb506-130">To view job details</span></span>
1. <span data-ttu-id="eb506-131">StorSimple cihaz Yöneticisi hizmetinize gidin ve ardından **işleri**.</span><span class="sxs-lookup"><span data-stu-id="eb506-131">Go to your StorSimple Device Manager service and then click **Jobs**.</span></span>

2. <span data-ttu-id="eb506-132">İçinde **işleri** dikey penceresinde, ilgilendiğiniz uygun filtrelerle bir sorgu çalıştırarak iş görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eb506-132">In the **Jobs** blade, display the job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="eb506-133">Çalışan veya işi iptal tamamlandı için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb506-133">You can search for completed, running, or canceled jobs.</span></span>

    ![İş dikey penceresi](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. <span data-ttu-id="eb506-135">Seçin ve bir iş'i tıklatın.</span><span class="sxs-lookup"><span data-stu-id="eb506-135">Select and click a job.</span></span>

    ![İş dikey penceresi](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. <span data-ttu-id="eb506-137">İş ayrıntıları dikey penceresinde, durumunu, ayrıntıları, süresi istatistikleri ve veri istatistiklerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb506-137">In the job details blade, you can view the status, details, time statistics, and data statistics.</span></span>
   
    ![İş ayrıntıları](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a><span data-ttu-id="eb506-139">Bir işi iptal etme</span><span class="sxs-lookup"><span data-stu-id="eb506-139">Cancel a job</span></span>
<span data-ttu-id="eb506-140">Çalışan bir işi iptal etmek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="eb506-140">Perform the following steps to cancel a running job.</span></span>

> [!NOTE]
> <span data-ttu-id="eb506-141">Birim türünü değiştirmek için bir birim değiştirmekten ya da bir birim genişletme gibi bazı işleri iptal edilemez.</span><span class="sxs-lookup"><span data-stu-id="eb506-141">Some jobs, such as modifying a volume to change the volume type or expanding a volume, cannot be canceled.</span></span>


### <a name="to-cancel-a-job"></a><span data-ttu-id="eb506-142">Bir işi iptal etmek için</span><span class="sxs-lookup"><span data-stu-id="eb506-142">To cancel a job</span></span>
1. <span data-ttu-id="eb506-143">Üzerinde **işleri** sayfasında, uygun filtrelerle bir sorgu çalıştırarak iptal etmek istediğiniz çalışan iş görüntüler.</span><span class="sxs-lookup"><span data-stu-id="eb506-143">On the **Jobs** page, display the running job(s) that you want to cancel by running a query with appropriate filters.</span></span> <span data-ttu-id="eb506-144">İşi seçin.</span><span class="sxs-lookup"><span data-stu-id="eb506-144">Select the job.</span></span>

2. <span data-ttu-id="eb506-145">Bağlam menüsü çağırma tıklatıp seçili iş üzerinde sağ **iptal**.</span><span class="sxs-lookup"><span data-stu-id="eb506-145">Right-click on the selected job to invoke the context menu and click **Cancel**.</span></span>

    ![İş ayrıntıları](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. <span data-ttu-id="eb506-147">Onayınız istendiğinde **Evet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb506-147">When prompted for confirmation, click **Yes**.</span></span> <span data-ttu-id="eb506-148">Bu işi iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="eb506-148">This job is now canceled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb506-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eb506-149">Next steps</span></span>
* <span data-ttu-id="eb506-150">Bilgi edinmek için nasıl [, StorSimple yedekleme ilkelerini yönetme](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="eb506-150">Learn how to [manage your StorSimple backup policies](storsimple-8000-manage-backup-policies-u2.md).</span></span>
* <span data-ttu-id="eb506-151">Bilgi edinmek için nasıl [StorSimple Cihazınızı yönetmek için StorSimple cihaz Yöneticisi hizmetini kullanma](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="eb506-151">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

