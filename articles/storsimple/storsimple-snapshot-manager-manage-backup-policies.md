---
title: "aaaStorSimple anlık görüntü Yöneticisi'ni yedekleme ilkeleri | Microsoft Docs"
description: "Toouse StorSimple Snapshot Manager MMC ek bileşenini toocreate hello ve zamanlanmış yedeklemeler denetleyen hello yedekleme ilkelerini yönetme nasıl açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a><span data-ttu-id="3fe25-103">StorSimple Snapshot Manager toocreate kullanın ve yedekleme ilkelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="3fe25-103">Use StorSimple Snapshot Manager toocreate and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="3fe25-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3fe25-104">Overview</span></span>
<span data-ttu-id="3fe25-105">Bir yedekleme İlkesi birim verilerini yerel olarak veya hello bulut yedekleme için bir zamanlama oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3fe25-105">A backup policy creates a schedule for backing up volume data locally or in hello cloud.</span></span> <span data-ttu-id="3fe25-106">Bir yedekleme ilkesi oluşturduğunuzda, bir bekletme ilkesi de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fe25-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="3fe25-107">(En fazla 64 anlık görüntüleri tutabilirsiniz.) Yedekleme ilkeleri hakkında daha fazla bilgi için bkz: [yedekleme türleri](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) içinde [StorSimple 8000 serisi: karma bulut çözümünün](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3fe25-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="3fe25-108">Bu öğretici açıklar nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="3fe25-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="3fe25-109">Bir yedekleme İlkesi Oluştur</span><span class="sxs-lookup"><span data-stu-id="3fe25-109">Create a backup policy</span></span>
* <span data-ttu-id="3fe25-110">Yedekleme ilkesini Düzenle</span><span class="sxs-lookup"><span data-stu-id="3fe25-110">Edit a backup policy</span></span>
* <span data-ttu-id="3fe25-111">Bir yedekleme ilkesi silme</span><span class="sxs-lookup"><span data-stu-id="3fe25-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="3fe25-112">Bir yedekleme İlkesi Oluştur</span><span class="sxs-lookup"><span data-stu-id="3fe25-112">Create a backup policy</span></span>
<span data-ttu-id="3fe25-113">Aşağıdaki yordam toocreate yeni bir yedekleme İlkesi hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="3fe25-113">Use hello following procedure toocreate a new backup policy.</span></span>

#### <a name="toocreate-a-backup-policy"></a><span data-ttu-id="3fe25-114">toocreate bir yedekleme İlkesi</span><span class="sxs-lookup"><span data-stu-id="3fe25-114">toocreate a backup policy</span></span>
1. <span data-ttu-id="3fe25-115">Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3fe25-115">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="3fe25-116">Merhaba, **kapsam** bölmesinde, sağ **yedekleme ilkeleri**, tıklatıp **yedekleme İlkesi Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="3fe25-116">In hello **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![Bir yedekleme İlkesi Oluştur](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="3fe25-118">Merhaba **bir ilke oluşturmak** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3fe25-118">hello **Create a Policy** dialog box appears.</span></span>

    ![Bir ilke - Genel sekmesi oluştur](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="3fe25-120">Merhaba üzerinde **genel** sekmesi, aşağıdaki bilgilerle tam hello:</span><span class="sxs-lookup"><span data-stu-id="3fe25-120">On hello **General** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="3fe25-121">Merhaba, **adı** metin kutusuna hello ilkesi için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="3fe25-121">In hello **Name** text box, type a name for hello policy.</span></span>
   2. <span data-ttu-id="3fe25-122">Merhaba, **birim grubu** metin kutusunda, tür hello hello ilkeyle ilişkilendirilmiş hello birim grubu adını.</span><span class="sxs-lookup"><span data-stu-id="3fe25-122">In hello **Volume group** text box, type hello name of hello volume group associated with hello policy.</span></span>
   3. <span data-ttu-id="3fe25-123">Şunlardan birini seçin **yerel anlık görüntü** veya **bulut anlık görüntü**.</span><span class="sxs-lookup"><span data-stu-id="3fe25-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="3fe25-124">Anlık görüntü tooretain Hello sayısını seçin.</span><span class="sxs-lookup"><span data-stu-id="3fe25-124">Select hello number of snapshots tooretain.</span></span> <span data-ttu-id="3fe25-125">Seçerseniz **tüm**, 64 anlık görüntüleri tutulur (Merhaba en fazla).</span><span class="sxs-lookup"><span data-stu-id="3fe25-125">If you select **All**, 64 snapshots will be retained (hello maximum).</span></span>
4. <span data-ttu-id="3fe25-126">Merhaba tıklatın **zamanlama** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="3fe25-126">Click hello **Schedule** tab.</span></span>

    ![Bir ilke - zamanlama sekmesi oluştur](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="3fe25-128">Merhaba üzerinde **zamanlama** sekmesi, aşağıdaki bilgilerle tam hello:</span><span class="sxs-lookup"><span data-stu-id="3fe25-128">On hello **Schedule** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="3fe25-129">Merhaba tıklatın **etkinleştirmek** onay kutusunu tooschedule hello sonraki yedekleme.</span><span class="sxs-lookup"><span data-stu-id="3fe25-129">Click hello **Enable** check box tooschedule hello next backup.</span></span>
   2. <span data-ttu-id="3fe25-130">Altında **ayarları**seçin **bir kez**, **günlük**, **haftalık**, veya **aylık**.</span><span class="sxs-lookup"><span data-stu-id="3fe25-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="3fe25-131">Merhaba, **Başlat** metin kutusuna hello takvim simgesini tıklatın ve bir başlangıç tarihi seçin.</span><span class="sxs-lookup"><span data-stu-id="3fe25-131">In hello **Start** text box, click hello calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="3fe25-132">Altında **Gelişmiş ayarları**, isteğe bağlı yineleme zamanlamaları ve bitiş tarihi ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3fe25-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="3fe25-133">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3fe25-133">Click **OK**.</span></span>

<span data-ttu-id="3fe25-134">Bir yedekleme ilkesi oluşturduktan sonra aşağıdaki bilgilerle hello hello görünür **sonuçları** bölmesi:</span><span class="sxs-lookup"><span data-stu-id="3fe25-134">After you create a backup policy, hello following information appears in hello **Results** pane:</span></span>

* <span data-ttu-id="3fe25-135">**Ad** – hello yedekleme ilkesi adı.</span><span class="sxs-lookup"><span data-stu-id="3fe25-135">**Name** – hello name of backup policy.</span></span>
* <span data-ttu-id="3fe25-136">**Tür** – yerel anlık görüntü veya Bulut anlık görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="3fe25-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="3fe25-137">**Birim grubu** – hello hello ilkeyle ilişkilendirilmiş birim grubu.</span><span class="sxs-lookup"><span data-stu-id="3fe25-137">**Volume Group** – hello volume group associated with hello policy.</span></span>
* <span data-ttu-id="3fe25-138">**Bekletme** – hello anlık görüntü sayısı tutulur; hello en fazla 64.</span><span class="sxs-lookup"><span data-stu-id="3fe25-138">**Retention** – hello number of snapshots retained; hello maximum is 64.</span></span>
* <span data-ttu-id="3fe25-139">**Oluşturulan** – Bu ilke oluşturulduysa başlangıç tarihi.</span><span class="sxs-lookup"><span data-stu-id="3fe25-139">**Created** – hello date that this policy was created.</span></span>
* <span data-ttu-id="3fe25-140">**Etkin** – hello İlkesi şu anda etkin olup olmadığını: **True** yürürlükte; olduğunu gösterir **False** etkin olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="3fe25-140">**Enabled** – whether hello policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="3fe25-141">Yedekleme ilkesini Düzenle</span><span class="sxs-lookup"><span data-stu-id="3fe25-141">Edit a backup policy</span></span>
<span data-ttu-id="3fe25-142">Aşağıdaki yordam tooedit mevcut bir yedekleme İlkesi hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="3fe25-142">Use hello following procedure tooedit an existing backup policy.</span></span>

#### <a name="tooedit-a-backup-policy"></a><span data-ttu-id="3fe25-143">tooedit bir yedekleme İlkesi</span><span class="sxs-lookup"><span data-stu-id="3fe25-143">tooedit a backup policy</span></span>
1. <span data-ttu-id="3fe25-144">Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3fe25-144">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="3fe25-145">Merhaba, **kapsam** bölmesinde hello tıklatın **yedekleme ilkeleri** düğümü.</span><span class="sxs-lookup"><span data-stu-id="3fe25-145">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="3fe25-146">Tüm hello yedekleme ilkeleri hello görünür **sonuçları** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="3fe25-146">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="3fe25-147">Tooedit istediğiniz ve ardından hello ilkesine sağ **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="3fe25-147">Right-click hello policy that you want tooedit, and then click **Edit**.</span></span>

    ![Yedekleme ilkesini Düzenle](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="3fe25-149">Ne zaman hello **bir ilke oluşturmak** penceresi görüntülenir, değişikliklerinizi girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3fe25-149">When hello **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="3fe25-150">Bir yedekleme ilkesi silme</span><span class="sxs-lookup"><span data-stu-id="3fe25-150">Delete a backup policy</span></span>
<span data-ttu-id="3fe25-151">Aşağıdaki yordam toodelete bir yedekleme İlkesi hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="3fe25-151">Use hello following procedure toodelete a backup policy.</span></span>

#### <a name="toodelete-a-backup-policy"></a><span data-ttu-id="3fe25-152">toodelete bir yedekleme İlkesi</span><span class="sxs-lookup"><span data-stu-id="3fe25-152">toodelete a backup policy</span></span>
1. <span data-ttu-id="3fe25-153">Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="3fe25-153">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="3fe25-154">Merhaba, **kapsam** bölmesinde hello tıklatın **yedekleme ilkeleri** düğümü.</span><span class="sxs-lookup"><span data-stu-id="3fe25-154">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="3fe25-155">Tüm hello yedekleme ilkeleri hello görünür **sonuçları** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="3fe25-155">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="3fe25-156">Toodelete istediğiniz ve ardından yedekleme ilkesini hello sağ **silmek**.</span><span class="sxs-lookup"><span data-stu-id="3fe25-156">Right-click hello backup policy that you want toodelete, and then click **Delete**.</span></span>
4. <span data-ttu-id="3fe25-157">Merhaba onaylama iletisi göründüğünde tıklayın **Evet**.</span><span class="sxs-lookup"><span data-stu-id="3fe25-157">When hello confirmation message appears, click **Yes**.</span></span>

    ![Yedek İlkesi onayını Sil](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="3fe25-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3fe25-159">Next steps</span></span>
* <span data-ttu-id="3fe25-160">Nasıl çok öğrenin[StorSimple Snapshot Manager tooadminister StorSimple çözümünüzün kullanmak](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="3fe25-160">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="3fe25-161">Nasıl çok öğrenin[StorSimple Snapshot Manager tooview kullanma ve yedekleme işlerini yönetme](storsimple-snapshot-manager-manage-backup-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="3fe25-161">Learn how too[use StorSimple Snapshot Manager tooview and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
