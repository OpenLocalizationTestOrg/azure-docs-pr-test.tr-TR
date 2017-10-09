---
title: "aaaManage, StorSimple yedekleme kataloğu | Microsoft Docs"
description: "Nasıl toouse hello StorSimple cihaz Yöneticisi hizmeti yedekleme kataloğu sayfa toolist seçin ve yedekleme kümelerini Sil açıklanmaktadır."
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
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a><span data-ttu-id="e8d3a-103">Yedekleme kataloğu Hello StorSimple cihaz Yöneticisi hizmeti toomanage kullanın</span><span class="sxs-lookup"><span data-stu-id="e8d3a-103">Use hello StorSimple Device Manager service toomanage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="e8d3a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e8d3a-104">Overview</span></span>
<span data-ttu-id="e8d3a-105">Merhaba StorSimple cihaz Yöneticisi hizmeti **yedekleme kataloğu** dikey penceresinde el ile veya zamanlanmış yedeklemeler durumdayken, oluşturulan tüm hello yedekleme kümelerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-105">hello StorSimple Device Manager service **Backup Catalog** blade displays all hello backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="e8d3a-106">Bir yedekleme İlkesi veya bir birim seçin için bu sayfayı toolist tüm hello yedekleri kullanın veya yedeklemeler, silebilir veya yedekleme toorestore kullanın veya bir birim kopyalama.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

<span data-ttu-id="e8d3a-107">Bu öğretici bir yedekleme toolist, seçin ve delete nasıl ayarlanacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-107">This tutorial explains how toolist, select, and delete a backup set.</span></span> <span data-ttu-id="e8d3a-108">toolearn nasıl toorestore yedekleme aygıtınızdan Git çok[Cihazınızı yedekleme kümesinden geri](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="e8d3a-108">toolearn how toorestore your device from backup, go too[Restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span> <span data-ttu-id="e8d3a-109">bir birim tooclone Git çok nasıl toolearn[bir StorSimple biriminin kopyalama](storsimple-8000-clone-volume-u2.md).</span><span class="sxs-lookup"><span data-stu-id="e8d3a-109">toolearn how tooclone a volume, go too[Clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>

![Yedekleme kataloğu](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

<span data-ttu-id="e8d3a-111">Merhaba **yedekleme kataloğu** dikey yedekleme kümesi seçiminiz sorgu toonarrow sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-111">hello **Backup Catalog** blade provides a query toonarrow your backup set selection.</span></span> <span data-ttu-id="e8d3a-112">Şu parametreler hello üzerinde temel alınır hello yedekleme kümelerini filtreleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e8d3a-112">You can filter hello backup sets that are retrieved, based on hello following parameters:</span></span>

* <span data-ttu-id="e8d3a-113">**Aygıt** – hello cihaz üzerinde hangi hello yedekleme kümesi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-113">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="e8d3a-114">**Yedekleme İlkesi veya birim** – yedekleme İlkesi veya bu yedekleme kümesiyle ilişkili birim hello.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-114">**Backup policy or Volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="e8d3a-115">**Başlangıç ve bitiş** – hello yedekleme kümesi oluşturduğunuzda hello tarih ve saat aralığı.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-115">**From and To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="e8d3a-116">Merhaba filtrelenmiş yedekleme kümelerini sonra öznitelikleri aşağıdaki hello üzerinde temel tabloda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e8d3a-116">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="e8d3a-117">**Ad** – hello hello yedekleme İlkesi veya birim hello yedekleme kümesiyle ilişkili ad.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-117">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="e8d3a-118">**Boyutu** – hello hello yedekleme kümesinin gerçek boyutu.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-118">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="e8d3a-119">**Oluşturma tarihi** – başlangıç tarihi ve hello yedeklemelerin ne zaman oluşturulduğu saat.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-119">**Created On** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="e8d3a-120">**Tür** – yedekleme kümelerini yerel anlık görüntüleri olması veya Bulut anlık görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="e8d3a-121">Bir bulut anlık görüntüsü toplu veri hello bulutta bulunan toohello yedeğini başvuruyor ancak yerel anlık görüntü hello cihazda yerel olarak depolanan tüm birim verilerinizin yedeğidir.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-121">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="e8d3a-122">Bulut anlık görüntüleri veri dayanıklılığı için seçilen ancak yerel anlık görüntüleri daha hızlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="e8d3a-123">**Başlatan** – hello yedeklemeleri başlatılabilir otomatik olarak bir zamanlamaya göre veya el ile bir kullanıcı tarafından.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-123">**Initiated By** – hello backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="e8d3a-124">Bir yedekleme İlkesi tooschedule yedeklemeleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-124">You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="e8d3a-125">Alternatif olarak, hello kullanabilirsiniz **yedek alın** seçeneği tootake el ile yedekleme.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-125">Alternatively, you can use hello **Take backup** option tootake a manual backup.</span></span>

## <a name="list-backup-sets-for-a-backup-policy"></a><span data-ttu-id="e8d3a-126">Liste yedekleme için bir yedekleme İlkesi ayarlar</span><span class="sxs-lookup"><span data-stu-id="e8d3a-126">List backup sets for a backup policy</span></span>
<span data-ttu-id="e8d3a-127">Aşağıdaki adımları toolist hello tüm hello yedeklemeler için bir yedekleme İlkesi tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-127">Complete hello following steps toolist all hello backups for a backup policy.</span></span>

#### <a name="toolist-backup-sets"></a><span data-ttu-id="e8d3a-128">toolist yedekleme kümeleri</span><span class="sxs-lookup"><span data-stu-id="e8d3a-128">toolist backup sets</span></span>
1. <span data-ttu-id="e8d3a-129">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **yedekleme kataloğu**.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-129">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>

2. <span data-ttu-id="e8d3a-130">Filtre gibi Hello seçimleri:</span><span class="sxs-lookup"><span data-stu-id="e8d3a-130">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="e8d3a-131">Merhaba zaman aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-131">Specify hello time range.</span></span>
   2. <span data-ttu-id="e8d3a-132">Merhaba uygun cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-132">Select hello appropriate device.</span></span>
   3. <span data-ttu-id="e8d3a-133">Filtre ölçütü **yedekleme İlkesi** tooview hello karşılık gelen hello yedekler.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-133">Filter by **Backup policy** tooview hello corresponding hello backups.</span></span>
   3. <span data-ttu-id="e8d3a-134">Merhaba yedekleme İlkesi açılır listeden seçin **tüm** tüm hello seçili hello yedeklemelerin tooview aygıt.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-134">From hello backup policy dropdown list, choose **All** tooview all hello backups on hello selected device.</span></span>
   4. <span data-ttu-id="e8d3a-135">Tıklatın **Uygula** tooexecute bu sorgu.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-135">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="e8d3a-136">Seçili hello yedekleme ilkesiyle ilişkili hello yedeklemeler yedekleme kümelerini hello listesinde görünmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-136">hello backups associated with hello selected backup policy should appear in hello list of backup sets.</span></span>

      ![Toobackup Kataloğu gidin](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a><span data-ttu-id="e8d3a-138">Bir yedekleme kümesi seçin</span><span class="sxs-lookup"><span data-stu-id="e8d3a-138">Select a backup set</span></span>
<span data-ttu-id="e8d3a-139">Bir birim veya yedekleme ilkesi için bir yedekleme kümesi adımları tooselect aşağıdaki hello tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-139">Complete hello following steps tooselect a backup set for a volume or backup policy.</span></span>

#### <a name="tooselect-a-backup-set"></a><span data-ttu-id="e8d3a-140">tooselect bir yedekleme kümesi</span><span class="sxs-lookup"><span data-stu-id="e8d3a-140">tooselect a backup set</span></span>
1. <span data-ttu-id="e8d3a-141">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **yedekleme kataloğu**.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-141">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="e8d3a-142">Filtre gibi Hello seçimleri:</span><span class="sxs-lookup"><span data-stu-id="e8d3a-142">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="e8d3a-143">Merhaba zaman aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-143">Specify hello time range.</span></span> 
   2. <span data-ttu-id="e8d3a-144">Merhaba uygun cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-144">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="e8d3a-145">Birim veya yedekleme İlkesi tooselect istediğiniz hello yedekleme için filtre.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-145">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="e8d3a-146">Tıklatın **Uygula** tooexecute bu sorgu.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-146">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="e8d3a-147">Merhaba seçili hello birim veya yedekleme ilkesiyle ilişkili yedeklemeler yedekleme kümelerini hello listesinde görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-147">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Toobackup Kataloğu gidin](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="e8d3a-149">Seçin ve bir yedekleme kümesi'ni genişletin.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-149">Select and expand a backup set.</span></span> <span data-ttu-id="e8d3a-150">Şimdi hello yedekleme kümelerini içerdiği hello birimlerle ayrıntılarıyla görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-150">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="e8d3a-151">Merhaba **geri** ve **silmek** hello yedekleme kümesi hello bağlam menüsünü (sağ tıklatma) aracılığıyla seçenekleri mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-151">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="e8d3a-152">Seçtiğiniz hello yedekleme kümesinde aşağıdaki işlemlerden birini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-152">You can perform either of these actions on hello backup set that you selected.</span></span>

    ![Toobackup Kataloğu gidin](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a><span data-ttu-id="e8d3a-154">Bir yedekleme kümesi Sil</span><span class="sxs-lookup"><span data-stu-id="e8d3a-154">Delete a backup set</span></span>
<span data-ttu-id="e8d3a-155">Kendisiyle ilişkili tooretain hello veriler artık istediklerinde yedekleme silin.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-155">Delete a backup when you no longer wish tooretain hello data associated with it.</span></span> <span data-ttu-id="e8d3a-156">Aşağıdaki adımları toodelete bir yedekleme kümesi hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-156">Perform hello following steps toodelete a backup set.</span></span>

#### <a name="toodelete-a-backup-set"></a><span data-ttu-id="e8d3a-157">toodelete bir yedekleme kümesi</span><span class="sxs-lookup"><span data-stu-id="e8d3a-157">toodelete a backup set</span></span>
 <span data-ttu-id="e8d3a-158">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **yedekleme kataloğu**.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-158">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="e8d3a-159">Filtre gibi Hello seçimleri:</span><span class="sxs-lookup"><span data-stu-id="e8d3a-159">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="e8d3a-160">Merhaba zaman aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-160">Specify hello time range.</span></span> 
   2. <span data-ttu-id="e8d3a-161">Merhaba uygun cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-161">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="e8d3a-162">Birim veya yedekleme İlkesi tooselect istediğiniz hello yedekleme için filtre.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-162">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="e8d3a-163">Tıklatın **Uygula** tooexecute bu sorgu.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-163">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="e8d3a-164">Merhaba seçili hello birim veya yedekleme ilkesiyle ilişkili yedeklemeler yedekleme kümelerini hello listesinde görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-164">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Toobackup Kataloğu gidin](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="e8d3a-166">Seçin ve bir yedekleme kümesi'ni genişletin.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-166">Select and expand a backup set.</span></span> <span data-ttu-id="e8d3a-167">Şimdi hello yedekleme kümelerini içerdiği hello birimlerle ayrıntılarıyla görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-167">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="e8d3a-168">Merhaba **geri** ve **silmek** hello yedekleme kümesi hello bağlam menüsünü (sağ tıklatma) aracılığıyla seçenekleri mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-168">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="e8d3a-169">Seçili hello yedekleme kümesi sağ tıklayın ve hello bağlam menüsünden seçin **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-169">Right-click hello selected backup set and from hello context menu, select **Delete**.</span></span>

    ![Toobackup Kataloğu gidin](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. <span data-ttu-id="e8d3a-171">Onayınız istendiğinde hello görüntülenen bilgileri gözden geçirin ve tıklayın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-171">When prompted for confirmation, review hello displayed information and click **Delete**.</span></span> <span data-ttu-id="e8d3a-172">Merhaba seçili yedekleme kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-172">hello selected backup is deleted permanently.</span></span>

    ![Toobackup Kataloğu gidin](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. <span data-ttu-id="e8d3a-174">Merhaba silme işlemi devam ederken ve başarıyla tamamlandığında size bildirilecek.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-174">You will be notified when hello deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="e8d3a-175">Merhaba silme işlemi yapıldıktan sonra bu sayfada hello sorguyu yenileyin.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-175">After hello deletion is done, refresh hello query on this page.</span></span> <span data-ttu-id="e8d3a-176">Silinen hello yedekleme kümesi artık yedekleme kümelerini hello listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="e8d3a-176">hello deleted backup set will no longer appear in hello list of backup sets.</span></span>

    ![Toobackup Kataloğu gidin](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a><span data-ttu-id="e8d3a-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e8d3a-178">Next steps</span></span>
* <span data-ttu-id="e8d3a-179">Nasıl çok öğrenin[kullanın, bir yedekleme kümesi aygıtınızdan yedekleme kataloğu toorestore hello](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="e8d3a-179">Learn how too[use hello backup catalog toorestore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="e8d3a-180">Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e8d3a-180">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

