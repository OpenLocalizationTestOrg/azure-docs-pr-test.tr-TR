---
title: "aaaManage, StorSimple yedekleme kataloğu | Microsoft Docs"
description: "Nasıl toouse hello StorSimple Yöneticisi hizmeti yedekleme kataloğu sayfa toolist, seçin ve bir birim için yedekleme kümelerini Sil açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ad81bee9-fe43-40b3-a384-b15fb274ecd9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/28/2016
ms.author: v-sharos
ms.openlocfilehash: 14f565c174a10da2c9e2f934a533a5e493f77226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-backup-catalog"></a><span data-ttu-id="5f5b1-103">Yedekleme kataloğu Hello StorSimple Yöneticisi hizmet toomanage kullanın</span><span class="sxs-lookup"><span data-stu-id="5f5b1-103">Use hello StorSimple Manager service toomanage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="5f5b1-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5f5b1-104">Overview</span></span>
<span data-ttu-id="5f5b1-105">Merhaba StorSimple Yöneticisi hizmeti **yedekleme kataloğu** sayfası el ile veya zamanlanmış yedeklemeler durumdayken, oluşturulan tüm hello yedekleme kümelerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-105">hello StorSimple Manager service **Backup Catalog** page displays all hello backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="5f5b1-106">Bir yedekleme İlkesi veya bir birim seçin için bu sayfayı toolist tüm hello yedekleri kullanın veya yedeklemeler, silebilir veya yedekleme toorestore kullanın veya bir birim kopyalama.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

<span data-ttu-id="5f5b1-107">Bu öğretici bir yedekleme toolist, seçin ve delete nasıl ayarlanacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-107">This tutorial explains how toolist, select, and delete a backup set.</span></span> <span data-ttu-id="5f5b1-108">toolearn nasıl toorestore yedekleme aygıtınızdan Git çok[Cihazınızı yedekleme kümesinden geri](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="5f5b1-108">toolearn how toorestore your device from backup, go too[Restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span> <span data-ttu-id="5f5b1-109">bir birim tooclone Git çok nasıl toolearn[bir StorSimple biriminin kopyalama](storsimple-clone-volume.md).</span><span class="sxs-lookup"><span data-stu-id="5f5b1-109">toolearn how tooclone a volume, go too[Clone a StorSimple volume](storsimple-clone-volume.md).</span></span>

![Yedekleme kataloğu](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

<span data-ttu-id="5f5b1-111">Merhaba **yedekleme kataloğu** sayfası, yedekleme kümesi seçiminiz sorgu toonarrow sağlar.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-111">hello **Backup Catalog** page provides a query toonarrow your backup set selection.</span></span> <span data-ttu-id="5f5b1-112">Şu parametreler hello üzerinde temel alınır hello yedekleme kümelerini filtreleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5f5b1-112">You can filter hello backup sets that are retrieved, based on hello following parameters:</span></span>

* <span data-ttu-id="5f5b1-113">**Aygıt** – hello cihaz üzerinde hangi hello yedekleme kümesi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-113">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="5f5b1-114">**İlke veya birime yedekleme** – yedekleme İlkesi veya bu yedekleme kümesiyle ilişkili birim hello.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-114">**Backup Policy or Volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="5f5b1-115">**Başlangıç ve bitiş** – hello yedekleme kümesi oluşturduğunuzda hello tarih ve saat aralığı.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-115">**From and To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="5f5b1-116">Merhaba filtrelenmiş yedekleme kümelerini sonra öznitelikleri aşağıdaki hello üzerinde temel tabloda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5f5b1-116">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="5f5b1-117">**Ad** – hello hello yedekleme İlkesi veya birim hello yedekleme kümesiyle ilişkili ad.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-117">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="5f5b1-118">**Boyutu** – hello hello yedekleme kümesinin gerçek boyutu.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-118">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="5f5b1-119">**Oluşturma tarihi** – başlangıç tarihi ve hello yedeklemelerin ne zaman oluşturulduğu saat.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-119">**Created On** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="5f5b1-120">**Tür** – yedekleme kümelerini yerel anlık görüntüleri olması veya Bulut anlık görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="5f5b1-121">Bir bulut anlık görüntüsü toplu veri hello bulutta bulunan toohello yedeğini başvuruyor ancak yerel anlık görüntü hello cihazda yerel olarak depolanan tüm birim verilerinizin yedeğidir.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-121">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="5f5b1-122">Bulut anlık görüntüleri veri dayanıklılığı için seçilen ancak yerel anlık görüntüleri daha hızlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="5f5b1-123">**Başlatan** – hello yedeklemeleri başlatılabilir otomatik olarak bir zamanlamaya göre veya el ile bir kullanıcı tarafından.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-123">**Initiated By** – hello backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="5f5b1-124">Bir yedekleme İlkesi tooschedule yedeklemeleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-124">You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="5f5b1-125">Alternatif olarak, hello kullanabilirsiniz **yedek alın** seçeneği tootake el ile yedekleme.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-125">Alternatively, you can use hello **Take backup** option tootake a manual backup.</span></span>

## <a name="list-backup-sets-for-a-volume"></a><span data-ttu-id="5f5b1-126">Liste yedekleme için bir birim ayarlar</span><span class="sxs-lookup"><span data-stu-id="5f5b1-126">List backup sets for a volume</span></span>
<span data-ttu-id="5f5b1-127">Aşağıdaki adımları toolist hello bir birim için tüm hello yedeklemeler tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-127">Complete hello following steps toolist all hello backups for a volume.</span></span>

#### <a name="toolist-backup-sets"></a><span data-ttu-id="5f5b1-128">toolist yedekleme kümeleri</span><span class="sxs-lookup"><span data-stu-id="5f5b1-128">toolist backup sets</span></span>
1. <span data-ttu-id="5f5b1-129">Merhaba Hello StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-129">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
2. <span data-ttu-id="5f5b1-130">Filtre gibi Hello seçimleri:</span><span class="sxs-lookup"><span data-stu-id="5f5b1-130">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="5f5b1-131">Merhaba uygun cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-131">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="5f5b1-132">Merhaba aşağı açılan listesinde, bir birim tooview hello karşılık gelen hello yedeklemeleri seçin.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-132">In hello drop-down list, choose a volume tooview hello corresponding hello backups.</span></span>
   3. <span data-ttu-id="5f5b1-133">Merhaba zaman aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-133">Specify hello time range.</span></span>
   4. <span data-ttu-id="5f5b1-134">Merhaba onay simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="5f5b1-134">Click hello check icon</span></span> ![Onay simgesi](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="5f5b1-136">tooexecute bu sorgu.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-136">tooexecute this query.</span></span>
      
      <span data-ttu-id="5f5b1-137">Seçili hello birimle ilişkilendirilen hello yedeklemeler yedekleme kümelerini hello listesinde görünmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-137">hello backups associated with hello selected volume should appear in hello list of backup sets.</span></span>

## <a name="select-a-backup-set"></a><span data-ttu-id="5f5b1-138">Bir yedekleme kümesi seçin</span><span class="sxs-lookup"><span data-stu-id="5f5b1-138">Select a backup set</span></span>
<span data-ttu-id="5f5b1-139">Bir birim veya yedekleme ilkesi için bir yedekleme kümesi adımları tooselect aşağıdaki hello tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-139">Complete hello following steps tooselect a backup set for a volume or backup policy.</span></span>

#### <a name="tooselect-a-backup-set"></a><span data-ttu-id="5f5b1-140">tooselect bir yedekleme kümesi</span><span class="sxs-lookup"><span data-stu-id="5f5b1-140">tooselect a backup set</span></span>
1. <span data-ttu-id="5f5b1-141">Merhaba Hello StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-141">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
2. <span data-ttu-id="5f5b1-142">Filtre gibi Hello seçimleri:</span><span class="sxs-lookup"><span data-stu-id="5f5b1-142">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="5f5b1-143">Merhaba uygun cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-143">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="5f5b1-144">Merhaba aşağı açılan listesinde, tooselect istediğiniz hello yedekleme için hello birim veya yedekleme ilkesini seçin.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-144">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="5f5b1-145">Merhaba zaman aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-145">Specify hello time range.</span></span>
   4. <span data-ttu-id="5f5b1-146">Merhaba onay simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="5f5b1-146">Click hello check icon</span></span> ![Onay simgesi](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="5f5b1-148">tooexecute bu sorgu.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-148">tooexecute this query.</span></span>
      
      <span data-ttu-id="5f5b1-149">Merhaba seçili hello birim veya yedekleme ilkesiyle ilişkili yedeklemeler yedekleme kümelerini hello listesinde görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-149">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="5f5b1-150">Seçin ve bir yedekleme kümesi'ni genişletin.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-150">Select and expand a backup set.</span></span> <span data-ttu-id="5f5b1-151">Merhaba **geri** ve **silmek** seçenekler hello sayfasının hello altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-151">hello **Restore** and **Delete** options are displayed at hello bottom of hello page.</span></span> <span data-ttu-id="5f5b1-152">Seçtiğiniz hello yedekleme kümesinde aşağıdaki işlemlerden birini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-152">You can perform either of these actions on hello backup set that you selected.</span></span>

## <a name="delete-a-backup-set"></a><span data-ttu-id="5f5b1-153">Bir yedekleme kümesi Sil</span><span class="sxs-lookup"><span data-stu-id="5f5b1-153">Delete a backup set</span></span>
<span data-ttu-id="5f5b1-154">Kendisiyle ilişkili tooretain hello veriler artık istediklerinde yedekleme silin.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-154">Delete a backup when you no longer wish tooretain hello data associated with it.</span></span> <span data-ttu-id="5f5b1-155">Aşağıdaki adımları toodelete bir yedekleme kümesi hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-155">Perform hello following steps toodelete a backup set.</span></span>

#### <a name="toodelete-a-backup-set"></a><span data-ttu-id="5f5b1-156">toodelete bir yedekleme kümesi</span><span class="sxs-lookup"><span data-stu-id="5f5b1-156">toodelete a backup set</span></span>
1. <span data-ttu-id="5f5b1-157">Merhaba Hello StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu sekmesini**.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-157">On hello StorSimple Manager service page, click hello **Backup Catalog tab**.</span></span>
2. <span data-ttu-id="5f5b1-158">Filtre gibi Hello seçimleri:</span><span class="sxs-lookup"><span data-stu-id="5f5b1-158">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="5f5b1-159">Merhaba uygun cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-159">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="5f5b1-160">Merhaba aşağı açılan listesinde, tooselect istediğiniz hello yedekleme için hello birim veya yedekleme ilkesini seçin.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-160">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="5f5b1-161">Merhaba zaman aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-161">Specify hello time range.</span></span>
   4. <span data-ttu-id="5f5b1-162">Merhaba onay simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="5f5b1-162">Click hello check icon</span></span> ![Onay simgesi](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="5f5b1-164">tooexecute bu sorgu.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-164">tooexecute this query.</span></span>
      
      <span data-ttu-id="5f5b1-165">Merhaba seçili hello birim veya yedekleme ilkesiyle ilişkili yedeklemeler yedekleme kümelerini hello listesinde görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-165">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="5f5b1-166">Seçin ve bir yedekleme kümesi'ni genişletin.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-166">Select and expand a backup set.</span></span> <span data-ttu-id="5f5b1-167">Merhaba **geri** ve **silmek** seçenekler hello sayfasının hello altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-167">hello **Restore** and **Delete** options are displayed at hello bottom of hello page.</span></span> <span data-ttu-id="5f5b1-168">**Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-168">Click **Delete**.</span></span>
4. <span data-ttu-id="5f5b1-169">Merhaba silme işlemi devam ederken ve başarıyla tamamlandığında size bildirilecek.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-169">You will be notified when hello deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="5f5b1-170">Merhaba silme işlemi yapıldıktan sonra bu sayfada hello sorguyu yenileyin.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-170">After hello deletion is done, refresh hello query on this page.</span></span> <span data-ttu-id="5f5b1-171">Silinen hello yedekleme kümesi artık yedekleme kümelerini hello listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="5f5b1-171">hello deleted backup set will no longer appear in hello list of backup sets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f5b1-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5f5b1-172">Next steps</span></span>
* <span data-ttu-id="5f5b1-173">Nasıl çok öğrenin[kullanın, bir yedekleme kümesi aygıtınızdan yedekleme kataloğu toorestore hello](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="5f5b1-173">Learn how too[use hello backup catalog toorestore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="5f5b1-174">Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="5f5b1-174">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

