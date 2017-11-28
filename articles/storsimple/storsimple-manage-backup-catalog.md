---
title: "StorSimple yedekleme kataloğu yönetme | Microsoft Docs"
description: "StorSimple Yöneticisi hizmeti yedekleme kataloğu sayfası listesinde seçin ve bir birim için yedekleme kümelerini silmek için nasıl kullanılacağını açıklar."
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
ms.openlocfilehash: 5ee9855e1428c7a2d871d9c215d302c5c3b7101a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-your-backup-catalog"></a><span data-ttu-id="5876a-103">Yedekleme kataloğu yönetmek için StorSimple Yöneticisi hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="5876a-103">Use the StorSimple Manager service to manage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="5876a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="5876a-104">Overview</span></span>
<span data-ttu-id="5876a-105">StorSimple Yöneticisi hizmeti **yedekleme kataloğu** sayfası el ile veya zamanlanmış yedeklemeler durumdayken, oluşturulan tüm yedekleme kümelerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5876a-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="5876a-106">Bir yedekleme İlkesi ya da bir birim seçin için tüm yedeklemeler listelemek veya yedekleri de silmek için bu sayfayı kullanın ya da bir yedeği geri yüklemek veya bir birim kopyalamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="5876a-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

<span data-ttu-id="5876a-107">Bu öğretici, liste, seçin ve bir yedekleme kümesi silme açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5876a-107">This tutorial explains how to list, select, and delete a backup set.</span></span> <span data-ttu-id="5876a-108">Cihazınızı yedekten geri yükleme konusunda bilgi almak için şu adrese gidin [Cihazınızı yedekleme kümesinden geri](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="5876a-108">To learn how to restore your device from backup, go to [Restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span> <span data-ttu-id="5876a-109">Birim kopyalama öğrenmek için şu adrese gidin [bir StorSimple biriminin kopyalama](storsimple-clone-volume.md).</span><span class="sxs-lookup"><span data-stu-id="5876a-109">To learn how to clone a volume, go to [Clone a StorSimple volume](storsimple-clone-volume.md).</span></span>

![Yedekleme kataloğu](./media/storsimple-manage-backup-catalog/backupcatalog.png) 

<span data-ttu-id="5876a-111">**Yedekleme kataloğu** sayfası, yedekleme daraltmak için bir sorgu olarak seçimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="5876a-111">The **Backup Catalog** page provides a query to narrow your backup set selection.</span></span> <span data-ttu-id="5876a-112">Aşağıdaki parametreleri temel alınarak alınır yedekleme kümelerini filtreleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5876a-112">You can filter the backup sets that are retrieved, based on the following parameters:</span></span>

* <span data-ttu-id="5876a-113">**Aygıt** – yedekleme kümesi oluşturulduğu aygıt.</span><span class="sxs-lookup"><span data-stu-id="5876a-113">**Device** – The device on which the backup set was created.</span></span>
* <span data-ttu-id="5876a-114">**İlke veya birime yedekleme** – yedekleme İlkesi veya bu yedekleme kümesiyle ilişkili birim.</span><span class="sxs-lookup"><span data-stu-id="5876a-114">**Backup Policy or Volume** – The backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="5876a-115">**Başlangıç ve bitiş** – yedekleme kümesi oluşturduğunuzda tarih ve saat aralığı.</span><span class="sxs-lookup"><span data-stu-id="5876a-115">**From and To** – The date and time range when the backup set was created.</span></span>

<span data-ttu-id="5876a-116">Filtrelenmiş yedekleme kümelerini, ardından aşağıdaki özniteliklerini temel alarak tabloda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5876a-116">The filtered backup sets are then tabulated based on the following attributes:</span></span>

* <span data-ttu-id="5876a-117">**Ad** – yedekleme İlkesi veya yedekleme kümesiyle ilişkili birim adı.</span><span class="sxs-lookup"><span data-stu-id="5876a-117">**Name** – The name of the backup policy or volume associated with the backup set.</span></span>
* <span data-ttu-id="5876a-118">**Boyutu** – yedekleme kümesi gerçek boyutu.</span><span class="sxs-lookup"><span data-stu-id="5876a-118">**Size** – The actual size of the backup set.</span></span>
* <span data-ttu-id="5876a-119">**Oluşturma tarihi** – yedeklemelerin ne zaman oluşturulduğu tarih ve saat.</span><span class="sxs-lookup"><span data-stu-id="5876a-119">**Created On** – The date and time when the backups were created.</span></span> 
* <span data-ttu-id="5876a-120">**Tür** – yedekleme kümelerini yerel anlık görüntüleri olması veya Bulut anlık görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5876a-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="5876a-121">Bir bulut anlık görüntüsü bulutta bulunan birim verilerin yedeğini başvuruyor ancak yedekleme verilerinizin cihazda yerel olarak depolanan tüm birim yerel bir anlık görüntüdür.</span><span class="sxs-lookup"><span data-stu-id="5876a-121">A local snapshot is a backup of all your volume data stored locally on the device, whereas a cloud snapshot refers to the backup of volume data residing in the cloud.</span></span> <span data-ttu-id="5876a-122">Bulut anlık görüntüleri veri dayanıklılığı için seçilen ancak yerel anlık görüntüleri daha hızlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="5876a-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="5876a-123">**Başlatan** – yedeklemeleri otomatik olarak bir zamanlamaya göre veya el ile bir kullanıcı tarafından başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="5876a-123">**Initiated By** – The backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="5876a-124">Yedeklemeleri zamanlamak için bir yedekleme İlkesi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5876a-124">You can use a backup policy to schedule backups.</span></span> <span data-ttu-id="5876a-125">Alternatif olarak, kullanabileceğiniz **yedek alın** seçeneği el ile yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="5876a-125">Alternatively, you can use the **Take backup** option to take a manual backup.</span></span>

## <a name="list-backup-sets-for-a-volume"></a><span data-ttu-id="5876a-126">Liste yedekleme için bir birim ayarlar</span><span class="sxs-lookup"><span data-stu-id="5876a-126">List backup sets for a volume</span></span>
<span data-ttu-id="5876a-127">Bir birim için tüm yedeklemeler listelemek için aşağıdaki adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="5876a-127">Complete the following steps to list all the backups for a volume.</span></span>

#### <a name="to-list-backup-sets"></a><span data-ttu-id="5876a-128">Yedekleme kümelerini listesi</span><span class="sxs-lookup"><span data-stu-id="5876a-128">To list backup sets</span></span>
1. <span data-ttu-id="5876a-129">StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5876a-129">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="5876a-130">Şu şekilde filtre seçimleri:</span><span class="sxs-lookup"><span data-stu-id="5876a-130">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="5876a-131">Uygun cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="5876a-131">Select the appropriate device.</span></span>
   2. <span data-ttu-id="5876a-132">Aşağı açılan listesinde karşılık gelen yedeklemeler görüntülemek için bir birim seçin.</span><span class="sxs-lookup"><span data-stu-id="5876a-132">In the drop-down list, choose a volume to view the corresponding the backups.</span></span>
   3. <span data-ttu-id="5876a-133">Zaman aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="5876a-133">Specify the time range.</span></span>
   4. <span data-ttu-id="5876a-134">Onay simgesine tıklayarak</span><span class="sxs-lookup"><span data-stu-id="5876a-134">Click the check icon</span></span> ![Onay simgesi](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="5876a-136">Bu sorguyu yürütmek için.</span><span class="sxs-lookup"><span data-stu-id="5876a-136">to execute this query.</span></span>
      
      <span data-ttu-id="5876a-137">Seçili birimle ilişkilendirilen yedeklemeler yedekleme kümelerini listesinde görünmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5876a-137">The backups associated with the selected volume should appear in the list of backup sets.</span></span>

## <a name="select-a-backup-set"></a><span data-ttu-id="5876a-138">Bir yedekleme kümesi seçin</span><span class="sxs-lookup"><span data-stu-id="5876a-138">Select a backup set</span></span>
<span data-ttu-id="5876a-139">Bir birim veya yedekleme ilkesi için bir yedek seçmek için aşağıdaki adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="5876a-139">Complete the following steps to select a backup set for a volume or backup policy.</span></span>

#### <a name="to-select-a-backup-set"></a><span data-ttu-id="5876a-140">Bir yedekleme kümesi seçmek için</span><span class="sxs-lookup"><span data-stu-id="5876a-140">To select a backup set</span></span>
1. <span data-ttu-id="5876a-141">StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="5876a-141">On the StorSimple Manager service page, click the **Backup catalog** tab.</span></span>
2. <span data-ttu-id="5876a-142">Şu şekilde filtre seçimleri:</span><span class="sxs-lookup"><span data-stu-id="5876a-142">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="5876a-143">Uygun cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="5876a-143">Select the appropriate device.</span></span>
   2. <span data-ttu-id="5876a-144">Aşağı açılan listesinde, seçmek istediğiniz yedekleme için birim veya yedekleme ilkesini seçin.</span><span class="sxs-lookup"><span data-stu-id="5876a-144">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="5876a-145">Zaman aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="5876a-145">Specify the time range.</span></span>
   4. <span data-ttu-id="5876a-146">Onay simgesine tıklayarak</span><span class="sxs-lookup"><span data-stu-id="5876a-146">Click the check icon</span></span> ![Onay simgesi](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="5876a-148">Bu sorguyu yürütmek için.</span><span class="sxs-lookup"><span data-stu-id="5876a-148">to execute this query.</span></span>
      
      <span data-ttu-id="5876a-149">Yedekleme seçili birimle ilişkilendirilen veya yedekleme İlkesi yedekleme kümelerini listesinde görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="5876a-149">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="5876a-150">Seçin ve bir yedekleme kümesi'ni genişletin.</span><span class="sxs-lookup"><span data-stu-id="5876a-150">Select and expand a backup set.</span></span> <span data-ttu-id="5876a-151">**Geri** ve **silmek** Seçenekler sayfasının en altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5876a-151">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="5876a-152">Seçtiğiniz yedekleme kümesinde aşağıdaki işlemlerden birini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5876a-152">You can perform either of these actions on the backup set that you selected.</span></span>

## <a name="delete-a-backup-set"></a><span data-ttu-id="5876a-153">Bir yedekleme kümesi Sil</span><span class="sxs-lookup"><span data-stu-id="5876a-153">Delete a backup set</span></span>
<span data-ttu-id="5876a-154">Kendisiyle ilişkili verileri tutmak istediğiniz zaman bir yedekleme silin.</span><span class="sxs-lookup"><span data-stu-id="5876a-154">Delete a backup when you no longer wish to retain the data associated with it.</span></span> <span data-ttu-id="5876a-155">Bir yedekleme kümesi silmek için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5876a-155">Perform the following steps to delete a backup set.</span></span>

#### <a name="to-delete-a-backup-set"></a><span data-ttu-id="5876a-156">Bir yedekleme kümesi silmek için</span><span class="sxs-lookup"><span data-stu-id="5876a-156">To delete a backup set</span></span>
1. <span data-ttu-id="5876a-157">StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu sekmesini**.</span><span class="sxs-lookup"><span data-stu-id="5876a-157">On the StorSimple Manager service page, click the **Backup Catalog tab**.</span></span>
2. <span data-ttu-id="5876a-158">Şu şekilde filtre seçimleri:</span><span class="sxs-lookup"><span data-stu-id="5876a-158">Filter the selections as follows:</span></span>
   
   1. <span data-ttu-id="5876a-159">Uygun cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="5876a-159">Select the appropriate device.</span></span>
   2. <span data-ttu-id="5876a-160">Aşağı açılan listesinde, seçmek istediğiniz yedekleme için birim veya yedekleme ilkesini seçin.</span><span class="sxs-lookup"><span data-stu-id="5876a-160">In the drop-down list, choose the volume or backup policy for the backup that you wish to select.</span></span>
   3. <span data-ttu-id="5876a-161">Zaman aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="5876a-161">Specify the time range.</span></span>
   4. <span data-ttu-id="5876a-162">Onay simgesine tıklayarak</span><span class="sxs-lookup"><span data-stu-id="5876a-162">Click the check icon</span></span> ![Onay simgesi](./media/storsimple-manage-backup-catalog/HCS_CheckIcon.png) <span data-ttu-id="5876a-164">Bu sorguyu yürütmek için.</span><span class="sxs-lookup"><span data-stu-id="5876a-164">to execute this query.</span></span>
      
      <span data-ttu-id="5876a-165">Yedekleme seçili birimle ilişkilendirilen veya yedekleme İlkesi yedekleme kümelerini listesinde görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="5876a-165">The backups associated with the selected volume or backup policy should appear in the list of backup sets.</span></span>
3. <span data-ttu-id="5876a-166">Seçin ve bir yedekleme kümesi'ni genişletin.</span><span class="sxs-lookup"><span data-stu-id="5876a-166">Select and expand a backup set.</span></span> <span data-ttu-id="5876a-167">**Geri** ve **silmek** Seçenekler sayfasının en altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5876a-167">The **Restore** and **Delete** options are displayed at the bottom of the page.</span></span> <span data-ttu-id="5876a-168">**Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5876a-168">Click **Delete**.</span></span>
4. <span data-ttu-id="5876a-169">Silme işlemi devam ediyor ve ne zaman başarıyla tamamlandıktan olduğunda size bildirilecek.</span><span class="sxs-lookup"><span data-stu-id="5876a-169">You will be notified when the deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="5876a-170">Silme işlemini gerçekleştirdikten sonra bu sayfada sorguyu yenileyin.</span><span class="sxs-lookup"><span data-stu-id="5876a-170">After the deletion is done, refresh the query on this page.</span></span> <span data-ttu-id="5876a-171">Silinen yedekleme kümesi artık yedekleme kümelerini listesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="5876a-171">The deleted backup set will no longer appear in the list of backup sets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5876a-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5876a-172">Next steps</span></span>
* <span data-ttu-id="5876a-173">Bilgi edinmek için nasıl [Cihazınızı yedekleme kümesinden geri yüklemek için yedekleme Kataloğu'nu kullanma](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="5876a-173">Learn how to [use the backup catalog to restore your device from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="5876a-174">Bilgi edinmek için nasıl [StorSimple Cihazınızı yönetmek için StorSimple Yöneticisi hizmetini kullanma](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="5876a-174">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

