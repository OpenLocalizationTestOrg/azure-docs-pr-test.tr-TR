---
title: "aaaView ve StorSimple sanal dizinin işlerini yönetme | Microsoft Docs"
description: "Merhaba StorSimple cihaz Yöneticisi hizmeti işleri sayfasında açıklar ve nasıl toouse onu hello StorSimple sanal dizinin tootrack yeni ve geçerli işleri."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a><span data-ttu-id="b5cfc-103">Merhaba StorSimple sanal dizinin Hello StorSimple cihaz Yöneticisi hizmet tooview işleri kullanın</span><span class="sxs-lookup"><span data-stu-id="b5cfc-103">Use hello StorSimple Device Manager service tooview jobs for hello StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="b5cfc-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b5cfc-104">Overview</span></span>
<span data-ttu-id="b5cfc-105">Merhaba **işleri** dikey görüntüleme ve bağlı tooyour StorSimple cihaz Yöneticisi hizmeti olan sanal dizileri başlatılan işlerini yönetmek için tek bir merkezi portal sağlar.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-105">hello **Jobs** blade provides a single central portal for viewing and managing jobs that are started on virtual arrays that are connected tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="b5cfc-106">Birden çok sanal cihazda çalışan, tamamlanmış ve başarısız işleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-106">You can view running, completed, and failed jobs for multiple virtual devices.</span></span> <span data-ttu-id="b5cfc-107">Sonuçları bir tablo biçiminde sunulur.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-107">Results are presented in a tabular format.</span></span>

![İşlerini dikey penceresi](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

<span data-ttu-id="b5cfc-109">Hızlı bir şekilde hello işleri, içinde alanları gibi filtreleyerek ilginizi çekiyor mu bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b5cfc-109">You can quickly find hello jobs you are interested in by filtering on fields such as:</span></span>

* <span data-ttu-id="b5cfc-110">**Zaman aralığı** – işleri filtrelenmiş göre hello tarih ve saat aralığı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-110">**Time range** – Jobs can be filtered based on hello date and time range.</span></span>
* <span data-ttu-id="b5cfc-111">**Aygıtları** – işleri bağlı belirli cihaz tooyour hizmette başlattı.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-111">**Devices** – Jobs are initiated on a specific device connected tooyour service.</span></span> <span data-ttu-id="b5cfc-112">Merhaba filtrelenen işler sonra öznitelikleri aşağıdaki hello üzerinde temel tabloda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="b5cfc-112">hello filtered jobs are then tabulated based on hello following attributes:</span></span>
  
  * <span data-ttu-id="b5cfc-113">**Ad** – hello iş adı olabilir **tüm**, **yedekleme**, **kopya**, **yük devri**, **güncelleştirmelerini yükleme** , veya **güncelleştirmelerini yükleme**.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-113">**Name** – hello job name can be **All**, **Backup**, **Clone**, **Fail over**, **Download updates**, or **Install updates**.</span></span>
  * <span data-ttu-id="b5cfc-114">**Durum** – işleri olabilir **tüm**, **devam eden**, **başarılı**, veya **başarısız**, veya **iptal edildi**.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-114">**Status** – Jobs can be **All**, **In progress**, **Succeeded**, or **Failed**, or **Canceled**.</span></span>
  * <span data-ttu-id="b5cfc-115">**Varlık** – hello işleri birim, paylaşım veya cihaz ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-115">**Entity** – hello jobs can be associated with a volume, share, or device.</span></span>
  * <span data-ttu-id="b5cfc-116">**Aygıt** – hello üzerinde hangi hello işi başlatıldı hello aygıt adı.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-116">**Device** – hello name of hello device on which hello job was started.</span></span>
  * <span data-ttu-id="b5cfc-117">**Tarihinde başlayan** – hello zaman zaman hello işi başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-117">**Started on** – hello time when hello job was started.</span></span>
  * <span data-ttu-id="b5cfc-118">**Süre** – hello süresince hangi hello işinde çalıştırıldı.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-118">**Duration** – hello duration for on which hello job was run.</span></span>
* <span data-ttu-id="b5cfc-119">**Durum** – tüm, çalışan, tamamlandı ya da başarısız işleri için arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-119">**Status** – You can search for all, running, completed, or failed jobs.</span></span>
* <span data-ttu-id="b5cfc-120">**İş türünü** – hello iş türü tümü, yedekleme, geri yükleme, yük devretme olması, güncelleştirmeleri karşıdan veya güncelleştirmeleri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-120">**Job type** – hello job type can be all, backup, restore, failover, download updates, or install updates.</span></span>

<span data-ttu-id="b5cfc-121">işlerini Hello listesi, her 30 saniyede yenilenir.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-121">hello list of jobs is refreshed every 30 seconds.</span></span>

## <a name="view-job-details"></a><span data-ttu-id="b5cfc-122">İş ayrıntılarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="b5cfc-122">View job details</span></span>
<span data-ttu-id="b5cfc-123">Aşağıdaki adımları tooview hello herhangi bir işi ayrıntılarını hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-123">Perform hello following steps tooview hello details of any job.</span></span>

#### <a name="tooview-job-details"></a><span data-ttu-id="b5cfc-124">tooview iş ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="b5cfc-124">tooview job details</span></span>
1. <span data-ttu-id="b5cfc-125">Merhaba üzerinde **işleri** dikey penceresinde, görüntü hello iş, ilgilendiğiniz uygun filtreleri ile çalışan bir sorgu.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-125">On hello **Jobs** blade, display hello job(s) you are interested in by running a query with appropriate filters.</span></span> <span data-ttu-id="b5cfc-126">Tamamlanan veya çalışan işleri arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-126">You can search for completed or running jobs.</span></span>
2. <span data-ttu-id="b5cfc-127">Bir işi hello tablo işleri listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-127">Select a job from hello tabular list of jobs.</span></span>
   
    ![İş dikey penceresi](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. <span data-ttu-id="b5cfc-129">Merhaba sayfasının Hello altında tıklatın **ayrıntıları**.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-129">At hello bottom of hello page, click **Details**.</span></span>
4. <span data-ttu-id="b5cfc-130">Merhaba, **ayrıntıları** iletişim kutusu, durumu, Ayrıntılar ve süresi istatistikleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-130">In hello **Details** dialog box, you can view status, details, and time statistics.</span></span> <span data-ttu-id="b5cfc-131">Merhaba aşağıda gösterilmiştir hello örneği **yedekleme işi ayrıntılarını** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-131">hello following illustration shows an example of hello **Backup Job Details** dialog box.</span></span>
   
    ![İş ayrıntıları](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a><span data-ttu-id="b5cfc-133">Merhaba sanal makine hello hiper yöneticide duraklatıldığında işi hataları</span><span class="sxs-lookup"><span data-stu-id="b5cfc-133">Job failures when hello virtual machine is paused in hello hypervisor</span></span>
<span data-ttu-id="b5cfc-134">Bir iş olduğunda StorSimple sanal dizinin ve hello aygıt (hiper yöneticide sağlanan sanal makine) ilerleme 15 dakikadan daha duraklatılır, hello işi başarısız.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-134">When a job is in progress on your StorSimple Virtual Array and hello device (virtual machine provisioned in hypervisor) is paused for greater than 15 minutes, hello job fails.</span></span> <span data-ttu-id="b5cfc-135">Bu tooyour StorSimple sanal dizinin zaman hello Microsoft Azure zaman ile eşitlenmemiş yapılıyor.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-135">This is due tooyour StorSimple Virtual Array time being out of sync with hello Microsoft Azure time.</span></span> 

<span data-ttu-id="b5cfc-136">Aşağıdaki hata hello görürsünüz: "cihaz zamanınızı hello Microsoft Azure süresi 15 dakikadan fazla ile eşitlenmedi.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-136">You will see hello following error: "Your device time is out of sync with hello Microsoft Azure time by more than 15 minutes.</span></span> <span data-ttu-id="b5cfc-137">Merhaba hiper yönetici ve hello aygıt saatleri bir NTP sunucusu ile eşitlendiğinden emin olmak.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-137">Ensure that hello hypervisor and hello device times are synchronized with an NTP servier.</span></span> <span data-ttu-id="b5cfc-138">Bağlantı sorunu olmadığından olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-138">Verify that there are no connectivity issues.</span></span> <span data-ttu-id="b5cfc-139">tootroubleshoot bağlantı sorunları, Çalıştır tanılama testleri hello yerel Web'den UI sanal cihazınızın."</span><span class="sxs-lookup"><span data-stu-id="b5cfc-139">tootroubleshoot connectivity issues, run diagnostic tests from hello local web UI of your virtual device."</span></span>

<span data-ttu-id="b5cfc-140">Bu hatalar toobackup, geri yükleme, güncelleştirme ve yük devretme işlemlerini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-140">These failures apply toobackup, restore, update, and failover jobs.</span></span> <span data-ttu-id="b5cfc-141">Hyper-V, sanal makine sağlandıktan, hello makine sonunda zaman, hiper yönetici ile eşitler.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-141">If your virtual machine is provisioned in Hyper-V, hello machine eventually synchronizes time with your hypervisor.</span></span> <span data-ttu-id="b5cfc-142">Bu gerçekleştikten sonra işi yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="b5cfc-142">Once that happens, you can restart your job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5cfc-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b5cfc-143">Next steps</span></span>
<span data-ttu-id="b5cfc-144">[Nasıl toouse hello yerel web kullanıcı Arabirimi tooadminister StorSimple sanal dizinizi öğrenin](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="b5cfc-144">[Learn how toouse hello local web UI tooadminister your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

