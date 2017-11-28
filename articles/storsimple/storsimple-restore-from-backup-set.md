---
title: aaaRestore yedekten bir StorSimple biriminin | Microsoft Docs
description: "Nasıl toouse hello StorSimple Yöneticisi hizmeti yedekleme kataloğu sayfa toorestore bir StorSimple biriminin bir yedekleme kümesinden açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b979782e-3184-4465-ad5f-e4516a5885d2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e0efa74b14603be41af0cfc5400de3c39ab8824e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a><span data-ttu-id="794b0-103">Bir yedeklemek kümesinden StorSimple birimini geri</span><span class="sxs-lookup"><span data-stu-id="794b0-103">Restore a StorSimple volume from a backup set</span></span>
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a><span data-ttu-id="794b0-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="794b0-104">Overview</span></span>
<span data-ttu-id="794b0-105">Merhaba **yedekleme kataloğu** sayfası el ile veya otomatik yedeklemeler durumdayken, oluşturulan tüm hello yedekleme kümelerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="794b0-105">hello **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="794b0-106">Bir yedekleme İlkesi veya bir birim seçin için bu sayfayı toolist tüm hello yedekleri kullanın veya yedeklemeler, silebilir veya yedekleme toorestore kullanın veya bir birim kopyalama.</span><span class="sxs-lookup"><span data-stu-id="794b0-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

 ![Yedekleme kataloğu sayfası](./media/storsimple-restore-from-backup-set/HCS_BackupCatalog.png)

<span data-ttu-id="794b0-108">Bu öğretici açıklar nasıl toouse hello **yedekleme kataloğu** sayfa toorestore bir yedekleme kümesi aygıtınızdan üzerindeki bir birimi.</span><span class="sxs-lookup"><span data-stu-id="794b0-108">This tutorial explains how toouse hello **Backup Catalog** page toorestore a volume on your device from a backup set.</span></span>

## <a name="how-toouse-hello-backup-catalog"></a><span data-ttu-id="794b0-109">Nasıl toouse hello yedekleme kataloğu</span><span class="sxs-lookup"><span data-stu-id="794b0-109">How toouse hello backup catalog</span></span>
<span data-ttu-id="794b0-110">Merhaba **yedekleme kataloğu** sayfası, yedekleme kümesi seçiminiz toonarrow yardımcı olan bir sorgu sağlar.</span><span class="sxs-lookup"><span data-stu-id="794b0-110">hello **Backup Catalog** page provides a query that helps you toonarrow your backup set selection.</span></span> <span data-ttu-id="794b0-111">Şu parametreler hello üzerinde temel alınan hello yedekleme kümelerini filtreleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="794b0-111">You can filter hello backup sets that are retrieved based on hello following parameters:</span></span>

* <span data-ttu-id="794b0-112">**Aygıt** – hello cihaz üzerinde hangi hello yedekleme kümesi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="794b0-112">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="794b0-113">**Yedekleme İlkesi** veya **birim** – yedekleme İlkesi veya bu yedekleme kümesiyle ilişkili birim hello.</span><span class="sxs-lookup"><span data-stu-id="794b0-113">**Backup policy** or **volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="794b0-114">**Gelen** ve **için** – hello yedekleme kümesi oluşturduğunuzda hello tarih ve saat aralığı.</span><span class="sxs-lookup"><span data-stu-id="794b0-114">**From** and **To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="794b0-115">Merhaba filtrelenmiş yedekleme kümelerini sonra öznitelikleri aşağıdaki hello üzerinde temel tabloda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="794b0-115">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="794b0-116">**Ad** – hello hello yedekleme İlkesi veya birim hello yedekleme kümesiyle ilişkili ad.</span><span class="sxs-lookup"><span data-stu-id="794b0-116">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="794b0-117">**Boyutu** – hello hello yedekleme kümesinin gerçek boyutu.</span><span class="sxs-lookup"><span data-stu-id="794b0-117">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="794b0-118">**Oluşturulan** – başlangıç tarihi ve hello yedeklemelerin ne zaman oluşturulduğu saat.</span><span class="sxs-lookup"><span data-stu-id="794b0-118">**Created on** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="794b0-119">**Tür** – yedekleme kümelerini yerel anlık görüntüleri olması veya Bulut anlık görüntüler.</span><span class="sxs-lookup"><span data-stu-id="794b0-119">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="794b0-120">Bir bulut anlık görüntüsü toplu veri hello bulutta bulunan toohello yedeğini başvuruyor ancak yerel anlık görüntü hello cihazda yerel olarak depolanan tüm birim verilerinizin yedeğidir.</span><span class="sxs-lookup"><span data-stu-id="794b0-120">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="794b0-121">Bulut anlık görüntüleri veri dayanıklılığı için seçilen ancak yerel anlık görüntüleri daha hızlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="794b0-121">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="794b0-122">**Tarafından başlatılan** – hello yedeklemeleri otomatik olarak tooa zamanlamaya göre başlatılabilir veya bir kullanıcı tarafından el ile.</span><span class="sxs-lookup"><span data-stu-id="794b0-122">**Initiated by** – hello backups can be initiated automatically according tooa schedule or manually by a user.</span></span> <span data-ttu-id="794b0-123">(Bir yedekleme İlkesi tooschedule yedeklemeleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="794b0-123">(You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="794b0-124">Alternatif olarak, hello kullanabilirsiniz **yedek alın** seçeneği tootake etkileşimli bir yedek.)</span><span class="sxs-lookup"><span data-stu-id="794b0-124">Alternatively, you can use hello **Take backup** option tootake an interactive backup.)</span></span>

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a><span data-ttu-id="794b0-125">Nasıl toorestore, StorSimple birim bir yedekten</span><span class="sxs-lookup"><span data-stu-id="794b0-125">How toorestore your StorSimple volume from a backup</span></span>
<span data-ttu-id="794b0-126">Merhaba kullanabilirsiniz **yedekleme kataloğu** toorestore StorSimple biriminiz belirli bir yedekten sayfa.</span><span class="sxs-lookup"><span data-stu-id="794b0-126">You can use hello **Backup Catalog** page toorestore your StorSimple volume from a specific backup.</span></span> 

> [!WARNING]
> <span data-ttu-id="794b0-127">Bir yedekten geri yükleme hello var olan birimler hello yedekten yerini alır.</span><span class="sxs-lookup"><span data-stu-id="794b0-127">Restoring from a backup will replace hello existing volumes from hello backup.</span></span> <span data-ttu-id="794b0-128">Bu hello hello yedeğin alındığı sonra yazıldı herhangi bir veri kaybına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="794b0-128">This may cause hello loss of any data that was written after hello backup was taken.</span></span>
> 
> 

<span data-ttu-id="794b0-129">Bir birime geri başlatmadan önce hello birimin çevrimdışı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="794b0-129">Before you initiate a restore on a volume, ensure that hello volume is offline.</span></span> <span data-ttu-id="794b0-130">Tootake hello birimde çevrimdışı hello konak önce gerekir ve cihaz hello.</span><span class="sxs-lookup"><span data-stu-id="794b0-130">You will need tootake hello volume offline on hello host first and then hello device.</span></span> <span data-ttu-id="794b0-131">Merhaba adımları [bir birim çevrimdışına](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="794b0-131">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span> <span data-ttu-id="794b0-132">Bir yedekleme kümesinden adımları toorestore bir birim aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="794b0-132">Perform hello following steps toorestore a volume from a backup set.</span></span>

### <a name="toorestore-from-a-backup-set"></a><span data-ttu-id="794b0-133">bir yedekleme kümesinden toorestore</span><span class="sxs-lookup"><span data-stu-id="794b0-133">toorestore from a backup set</span></span>
1. <span data-ttu-id="794b0-134">Merhaba Hello StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="794b0-134">On hello StorSimple Manager service page, click hello **Backup catalog** tab.</span></span>
   
    ![Yedekleme kataloğu](./media/storsimple-restore-from-backup-set/HCS_Restore.png)
2. <span data-ttu-id="794b0-136">Bir yedekleme kümesi aşağıdaki gibi seçin:</span><span class="sxs-lookup"><span data-stu-id="794b0-136">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="794b0-137">Merhaba uygun cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="794b0-137">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="794b0-138">Merhaba aşağı açılan listesinde, tooselect istediğiniz hello yedekleme için hello birim veya yedekleme ilkesini seçin.</span><span class="sxs-lookup"><span data-stu-id="794b0-138">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="794b0-139">Merhaba zaman aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="794b0-139">Specify hello time range.</span></span>
   4. <span data-ttu-id="794b0-140">Merhaba onay simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="794b0-140">Click hello check icon</span></span> ![onay simgesi](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png) <span data-ttu-id="794b0-142">tooexecute bu sorgu.</span><span class="sxs-lookup"><span data-stu-id="794b0-142">tooexecute this query.</span></span>
      
      <span data-ttu-id="794b0-143">Merhaba seçili hello birim veya yedekleme ilkesiyle ilişkili yedeklemeler yedekleme kümelerini hello listesinde görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="794b0-143">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
3. <span data-ttu-id="794b0-144">Merhaba yedekleme kümesi tooview ilişkili hello birimleri genişletin.</span><span class="sxs-lookup"><span data-stu-id="794b0-144">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="794b0-145">Geri yüklemeden önce bu birimleri hello ana bilgisayar ve aygıt çevrimdışına alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="794b0-145">These volumes must be taken offline on hello host and device before you can restore them.</span></span> <span data-ttu-id="794b0-146">Merhaba adımları [bir birim çevrimdışına](storsimple-manage-volumes.md#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="794b0-146">Follow hello steps in [Take a volume offline](storsimple-manage-volumes.md#take-a-volume-offline).</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="794b0-147">Merhaba aygıtta çevrimdışı hello birimleri olabilmesi hello birimlerde çevrimdışı hello konak ilk olarak, gerçekleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="794b0-147">Make sure that you have taken hello volumes offline on hello host first, before you take hello volumes offline on hello device.</span></span> <span data-ttu-id="794b0-148">Merhaba konakta çevrimdışı hello birimleri almazsanız, büyük olasılıkla toodata bozulmasına yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="794b0-148">If you do not take hello volumes offline on hello host, it could potentially lead toodata corruption.</span></span>
   > 
   > 
4. <span data-ttu-id="794b0-149">Bir yedekleme kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="794b0-149">Select a backup set.</span></span> <span data-ttu-id="794b0-150">Tıklatın **geri** hello sayfanın hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="794b0-150">Click **Restore** at hello bottom of hello page.</span></span>
5. <span data-ttu-id="794b0-151">Onayınız istenir.</span><span class="sxs-lookup"><span data-stu-id="794b0-151">You will be prompted for confirmation.</span></span> 
   
    ![Onay sayfası](./media/storsimple-restore-from-backup-set/HCS_ConfirmRestore.png)
6. <span data-ttu-id="794b0-153">Merhaba geri yükleme bilgileri gözden geçirin ve hello onay simgesine ![onay simgesi](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span><span class="sxs-lookup"><span data-stu-id="794b0-153">Review hello restore information and click hello check icon ![check icon](./media/storsimple-restore-from-backup-set/HCS_CheckIcon.png).</span></span> <span data-ttu-id="794b0-154">Bu hello erişerek görüntüleyebileceğiniz bir geri yükleme işi başlatır **işleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="794b0-154">This will initiate a restore job that you can view by accessing hello **Jobs** page.</span></span> 
7. <span data-ttu-id="794b0-155">Merhaba geri yükleme tamamlandıktan sonra birimlerinizi Merhaba içeriğine hello yedekleme birimlerden değiştirilir olduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="794b0-155">After hello restore is complete, you can verify that hello contents of your volumes are replaced by volumes from hello backup.</span></span>

<span data-ttu-id="794b0-156">![Video var](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video var**</span><span class="sxs-lookup"><span data-stu-id="794b0-156">![Video available](./media/storsimple-restore-from-backup-set/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="794b0-157">toowatch nasıl hello kopya kullanın ve geri yükleme StorSimple silinmiş toorecover dosyalarında özellikleri gösteren bir video tıklatın [burada](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="794b0-157">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="794b0-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="794b0-158">Next steps</span></span>
* <span data-ttu-id="794b0-159">Nasıl çok öğrenin[yönetmek StorSimple birimlerini](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="794b0-159">Learn how too[Manage StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="794b0-160">Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="794b0-160">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

