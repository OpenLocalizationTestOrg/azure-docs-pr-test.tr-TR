---
title: "aaaStorSimple anlık görüntü Yöneticisi birim grupları | Microsoft Docs"
description: "Toouse StorSimple Snapshot Manager MMC ek bileşenini toocreate hello ve birim gruplarını yönetme nasıl açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f7830b62761db7aa5139456b555b6168fb6a85de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a><span data-ttu-id="f0c6b-103">StorSimple Snapshot Manager toocreate kullanma ve birim grupları yönetme</span><span class="sxs-lookup"><span data-stu-id="f0c6b-103">Use StorSimple Snapshot Manager toocreate and manage volume groups</span></span>
## <a name="overview"></a><span data-ttu-id="f0c6b-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f0c6b-104">Overview</span></span>
<span data-ttu-id="f0c6b-105">Merhaba kullanabilirsiniz **birim grupları** hello düğümde **kapsam** bölmesi tooassign birimleri toovolume grupları, bir birim grubu hakkındaki bilgileri görüntüleyin yedeklemeleri zamanlamak ve birim grupları düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-105">You can use hello **Volume Groups** node on hello **Scope** pane tooassign volumes toovolume groups, view information about a volume group, schedule backups, and edit volume groups.</span></span>

<span data-ttu-id="f0c6b-106">Birim, yedeklemelerin uygulama tutarlı olduğunu kullanılan ilgili birimleri tooensure havuzları gruplarıdır.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-106">Volume groups are pools of related volumes used tooensure that backups are application-consistent.</span></span> <span data-ttu-id="f0c6b-107">Daha fazla bilgi için bkz: [birim ve birim grupları](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) ve [Windows birim gölge kopyası hizmeti ile tümleştirme](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="f0c6b-107">For more information, see [Volumes and volume groups](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) and [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="f0c6b-108">Bir birim grubundaki tüm birimleri, bir tek bulut hizmeti sağlayıcısını gelmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-108">All volumes in a volume group must come from a single cloud service provider.</span></span>
> * <span data-ttu-id="f0c6b-109">Birim grupları yapılandırdığınızda, Küme Paylaşılan birimleri (CSV) ve CSV olmayan hello içinde karıştırmamanızı aynı birim grubu.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-109">When you configure volume groups, do not mix cluster-shared volumes (CSVs) and non-CSVs in hello same volume group.</span></span> <span data-ttu-id="f0c6b-110">StorSimple Snapshot Manager csv bir karışımını desteklemez ve aynı anlık görüntü olmayan-csv hello.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-110">StorSimple Snapshot Manager does not support a mix of CSVs and non-CSVs in hello same snapshot.</span></span>

![Birim grupları düğümü](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

<span data-ttu-id="f0c6b-112">**Şekil 1: StorSimple anlık görüntü Yöneticisi birim grupları düğümü**</span><span class="sxs-lookup"><span data-stu-id="f0c6b-112">**Figure 1: StorSimple Snapshot Manager Volume Groups node**</span></span> 

<span data-ttu-id="f0c6b-113">Bu öğretici, StorSimple Snapshot Manager için nasıl kullanabileceğiniz açıklanır:</span><span class="sxs-lookup"><span data-stu-id="f0c6b-113">This tutorial explains how you can use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="f0c6b-114">Birim grupları hakkındaki bilgileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="f0c6b-114">View information about your volume groups</span></span>
* <span data-ttu-id="f0c6b-115">Birim grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="f0c6b-115">Create a volume group</span></span>
* <span data-ttu-id="f0c6b-116">Bir birim grubunu yedekleyin</span><span class="sxs-lookup"><span data-stu-id="f0c6b-116">Back up a volume group</span></span>
* <span data-ttu-id="f0c6b-117">Bir birim grubu Düzenle</span><span class="sxs-lookup"><span data-stu-id="f0c6b-117">Edit a volume group</span></span>
* <span data-ttu-id="f0c6b-118">Bir birim grubu Sil</span><span class="sxs-lookup"><span data-stu-id="f0c6b-118">Delete a volume group</span></span>

<span data-ttu-id="f0c6b-119">Tüm bu eylemleri de hello üzerinde kullanılabilir **Eylemler** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-119">All of these actions are also available on hello **Actions** pane.</span></span>

## <a name="view-volume-groups"></a><span data-ttu-id="f0c6b-120">Birim grupları görüntüle</span><span class="sxs-lookup"><span data-stu-id="f0c6b-120">View volume groups</span></span>
<span data-ttu-id="f0c6b-121">Merhaba tıklatırsanız **birim grupları** düğümü, hello **sonuçları** bölmesinde her bir birim grubu hakkında bilgi aşağıdaki hello gösterir, yaptığınız hello sütun seçimlerini bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-121">If you click hello **Volume Groups** node, hello **Results** pane shows hello following information about each volume group, depending on hello column selections you make.</span></span> <span data-ttu-id="f0c6b-122">(Merhaba hello sütunlarında **sonuçları** bölmesinde yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-122">(hello columns in hello **Results** pane are configurable.</span></span> <span data-ttu-id="f0c6b-123">Sağ hello **birimleri** düğümü, select **Görünüm**ve ardından **Sütun Ekle/Kaldır**.)</span><span class="sxs-lookup"><span data-stu-id="f0c6b-123">Right-click hello **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>

| <span data-ttu-id="f0c6b-124">Sonuçları sütun</span><span class="sxs-lookup"><span data-stu-id="f0c6b-124">Results column</span></span> | <span data-ttu-id="f0c6b-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0c6b-125">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f0c6b-126">Ad</span><span class="sxs-lookup"><span data-stu-id="f0c6b-126">Name</span></span> |<span data-ttu-id="f0c6b-127">Merhaba **adı** sütun hello birim grubu hello adını içerir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-127">hello **Name** column contains hello name of hello volume group.</span></span> |
| <span data-ttu-id="f0c6b-128">Uygulama</span><span class="sxs-lookup"><span data-stu-id="f0c6b-128">Application</span></span> |<span data-ttu-id="f0c6b-129">Merhaba **uygulamaları** hello Windows ana bilgisayar üzerinde çalışan ve sütun şu anda yüklü VSS yazıcılarının hello sayısı gösterir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-129">hello **Applications** column shows hello number of VSS writers currently installed and running on hello Windows host.</span></span> |
| <span data-ttu-id="f0c6b-130">Seçildi</span><span class="sxs-lookup"><span data-stu-id="f0c6b-130">Selected</span></span> |<span data-ttu-id="f0c6b-131">Merhaba **seçili** sütun hello birim grubunda bulunan birimleri hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-131">hello **Selected** column shows hello number of volumes that are contained in hello volume group.</span></span> <span data-ttu-id="f0c6b-132">Sıfır (0), uygulama hello birimleri hello birim grubu ile ilişkili olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-132">A zero (0) indicates that no application is associated with hello volumes in hello volume group.</span></span> |
| <span data-ttu-id="f0c6b-133">İçeri aktarılan</span><span class="sxs-lookup"><span data-stu-id="f0c6b-133">Imported</span></span> |<span data-ttu-id="f0c6b-134">Merhaba **Imported** sütun alınan birimler hello sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-134">hello **Imported** column shows hello number of imported volumes.</span></span> <span data-ttu-id="f0c6b-135">Ayarlandığında çok**doğru**, bu sütun bir birim grubu hello Azure portal ' alınan ve StorSimple Snapshot Manager'da oluşturulmadı belirtir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-135">When set too**True**, this column indicates that a volume group was imported from hello Azure portal and was not created in StorSimple Snapshot Manager.</span></span> |

> [!NOTE]
> <span data-ttu-id="f0c6b-136">StorSimple Snapshot Manager birim grupları ayrıca hello üzerinde görüntülenen **yedekleme ilkeleri** hello Azure portal sekmesindedir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-136">StorSimple Snapshot Manager volume groups are also displayed on hello **Backup Policies** tab in hello Azure portal.</span></span>
> 
> 

## <a name="create-a-volume-group"></a><span data-ttu-id="f0c6b-137">Birim grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="f0c6b-137">Create a volume group</span></span>
<span data-ttu-id="f0c6b-138">Aşağıdaki yordam toocreate bir birim grubu hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-138">Use hello following procedure toocreate a volume group.</span></span>

#### <a name="toocreate-a-volume-group"></a><span data-ttu-id="f0c6b-139">toocreate bir birim grubu</span><span class="sxs-lookup"><span data-stu-id="f0c6b-139">toocreate a volume group</span></span>
1. <span data-ttu-id="f0c6b-140">Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-140">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="f0c6b-141">Merhaba, **kapsam** bölmesinde sağ **birim grupları**ve ardından **birim grubu oluştur**.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-141">In hello **Scope** pane, right-click **Volume Groups**, and then click **Create Volume Group**.</span></span>
   
    ![Birim grubu oluştur](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    <span data-ttu-id="f0c6b-143">Merhaba **bir birim grubu oluşturun** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-143">hello **Create a volume group** dialog box appears.</span></span>
   
    ![Bir birim grubu iletişim kutusu oluşturma](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. <span data-ttu-id="f0c6b-145">Aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="f0c6b-145">Enter hello following information:</span></span>
   
   1. <span data-ttu-id="f0c6b-146">Merhaba, **adı** hello yeni birim grubu için benzersiz bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-146">In hello **Name** box, type a unique name for hello new volume group.</span></span>
   2. <span data-ttu-id="f0c6b-147">Merhaba, **uygulamaları** kutusunda, toohello birim grubu alacağınız hello birimleri ile ilişkili uygulama.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-147">In hello **Applications** box, select applications associated with hello volumes that you will be adding toohello volume group.</span></span>
      
       <span data-ttu-id="f0c6b-148">Merhaba **uygulamaları** VSS yazıcılarının olan ve StorSimple birimlerini kullanan uygulamalar için bunları etkin kutusunu listeler.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-148">hello **Applications** box lists only those applications that use StorSimple volumes and have VSS writers enabled for them.</span></span> <span data-ttu-id="f0c6b-149">Tüm birimlerin hello hello yazıcının farkında ise yalnızca bir VSS yazıcının etkin olduğu StorSimple birimler.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-149">A VSS writer is enabled only if all hello volumes that hello writer is aware of are StorSimple volumes.</span></span> <span data-ttu-id="f0c6b-150">Merhaba uygulamaları kutusu boş ise, VSS yazıcılarının desteklenen ve Azure StorSimple birimlerini kullanan bir uygulama yüklenmez.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-150">If hello Applications box is empty, then no applications that use Azure StorSimple volumes and have supported VSS writers are installed.</span></span> <span data-ttu-id="f0c6b-151">(Şu anda Azure StorSimple Microsoft Exchange ve SQL Server destekler.) VSS yazıcılarının hakkında daha fazla bilgi için bkz: [Windows birim gölge kopyası hizmeti ile tümleştirme](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="f0c6b-151">(Currently, Azure StorSimple supports Microsoft Exchange and SQL Server.) For more information about VSS writers, see [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>
      
       <span data-ttu-id="f0c6b-152">Bir uygulama seçerseniz, kendisiyle ilişkilendirilmiş tüm birimleri otomatik olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-152">If you select an application, all volumes associated with it are automatically selected.</span></span> <span data-ttu-id="f0c6b-153">Belirli bir uygulama ile ilişkili birimler seçerseniz, buna karşılık, hello uygulama otomatik olarak hello seçilen **uygulamaları** kutusu.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-153">Conversely, if you select volumes associated with a specific application, hello application is automatically selected in hello **Applications** box.</span></span> 
   3. <span data-ttu-id="f0c6b-154">Merhaba, **birimleri** kutusunda, StorSimple birimlerini tooadd toohello birim grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-154">In hello **Volumes** box, select StorSimple volumes tooadd toohello volume group.</span></span> 
      
      * <span data-ttu-id="f0c6b-155">Tek veya birden çok bölüm birimlerle içerebilir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-155">You can include volumes with single or multiple partitions.</span></span> <span data-ttu-id="f0c6b-156">(Birden çok bölüm birim dinamik diskleri veya temel diskleri birden çok bölüm olabilir.) Birden çok bölüm içeren bir birimdeki tek bir birim olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-156">(Multiple partition volumes can be dynamic disks or basic disks with multiple partitions.) A volume that contains multiple partitions is treated as a single unit.</span></span> <span data-ttu-id="f0c6b-157">Sonuç olarak, yalnızca bir hello bölümleri tooa birim grubu, tüm hello diğer bölümler eklerseniz, olan otomatik olarak eklenen toothat birim grubu hello aynı saat.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-157">Consequently, if you add only one of hello partitions tooa volume group, all hello other partitions are automatically added toothat volume group at hello same time.</span></span> <span data-ttu-id="f0c6b-158">Birden çok bölüm birim tooa birim Grup ekledikten sonra hello birden çok bölüm birim tek bir birim olarak kabul toobe devam eder.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-158">After you add a multiple partition volume tooa volume group, hello multiple partition volume continues toobe treated as a single unit.</span></span>
      * <span data-ttu-id="f0c6b-159">Tüm birimlerin toothem atayarak değil boş birim grupları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-159">You can create empty volume groups by not assigning any volumes toothem.</span></span> 
      * <span data-ttu-id="f0c6b-160">Küme Paylaşılan birimleri (CSV) ve CSV olmayan hello içinde karıştırmamanızı aynı birim grubu.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-160">Do not mix cluster-shared volumes (CSVs) and non-CSVs in hello same volume group.</span></span> <span data-ttu-id="f0c6b-161">StorSimple Snapshot Manager CSV birimleri karışımını desteklemez ve aynı anlık görüntü CSV olmayan birimlerin hello.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-161">StorSimple Snapshot Manager does not support a mix of CSV volumes and non-CSV volumes in hello same snapshot.</span></span>
4. <span data-ttu-id="f0c6b-162">Tıklatın **Tamam** toosave hello birim grubu.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-162">Click **OK** toosave hello volume group.</span></span>

## <a name="back-up-a-volume-group"></a><span data-ttu-id="f0c6b-163">Bir birim grubunu yedekleyin</span><span class="sxs-lookup"><span data-stu-id="f0c6b-163">Back up a volume group</span></span>
<span data-ttu-id="f0c6b-164">Bir birim grubu yordamı tooback aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-164">Use hello following procedure tooback up a volume group.</span></span>

#### <a name="tooback-up-a-volume-group"></a><span data-ttu-id="f0c6b-165">bir birim grubu tooback</span><span class="sxs-lookup"><span data-stu-id="f0c6b-165">tooback up a volume group</span></span>
1. <span data-ttu-id="f0c6b-166">Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-166">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="f0c6b-167">Merhaba, **kapsam** bölmesinde hello genişletin **birim grupları** düğümü, bir birim grubu adını sağ tıklatın ve ardından **ele yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-167">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Take Backup**.</span></span>
   
    ![Birim grubunu hemen yedekleyin](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. <span data-ttu-id="f0c6b-169">Merhaba, **ele yedekleme** iletişim kutusunda **yerel anlık görüntü** veya **bulut anlık görüntüsü**ve ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-169">In hello **Take Backup** dialog box, select **Local Snapshot** or **Cloud Snapshot**, and then click **Create**.</span></span>
   
    ![Yedekleme iletişim alın](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. <span data-ttu-id="f0c6b-171">Yedekleme hello tooconfirm çalıştığından, hello genişletin **işleri** düğümünü ve ardından **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-171">tooconfirm that hello backup is running, expand hello **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="f0c6b-172">Merhaba yedekleme listelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-172">hello backup should be listed.</span></span>
5. <span data-ttu-id="f0c6b-173">Tamamlanan tooview hello hello genişletin anlık görüntü, **yedekleme kataloğu** düğümü hello birim grup adını genişletin ve ardından **yerel anlık görüntü** veya **bulut anlık görüntüsü**.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-173">tooview hello completed snapshot, expand hello **Backup Catalog** node, expand hello volume group name, and then click **Local Snapshot** or **Cloud Snapshot**.</span></span> <span data-ttu-id="f0c6b-174">başarıyla tamamlandı, hello yedekleme listelenir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-174">hello backup will be listed if it finished successfully.</span></span>

## <a name="edit-a-volume-group"></a><span data-ttu-id="f0c6b-175">Bir birim grubu Düzenle</span><span class="sxs-lookup"><span data-stu-id="f0c6b-175">Edit a volume group</span></span>
<span data-ttu-id="f0c6b-176">Aşağıdaki yordam tooedit bir birim grubu hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-176">Use hello following procedure tooedit a volume group.</span></span>

#### <a name="tooedit-a-volume-group"></a><span data-ttu-id="f0c6b-177">tooedit bir birim grubu</span><span class="sxs-lookup"><span data-stu-id="f0c6b-177">tooedit a volume group</span></span>
1. <span data-ttu-id="f0c6b-178">Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-178">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="f0c6b-179">Merhaba, **kapsam** bölmesinde hello genişletin **birim grupları** düğümü, bir birim grubu adını sağ tıklatın ve ardından **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-179">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Edit**.</span></span>
3. <span data-ttu-id="f0c6b-180">Merhaba ** bir birim grubu oluşturun ** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-180">hello **Create a volume group **dialog box appears.</span></span> <span data-ttu-id="f0c6b-181">Merhaba değiştirebileceğiniz **adı**, **uygulamaları**, ve **birimleri** girişleri.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-181">You can change hello **Name**, **Applications**, and **Volumes** entries.</span></span>
4. <span data-ttu-id="f0c6b-182">Tıklatın **Tamam** toosave değişikliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-182">Click **OK** toosave your changes.</span></span>

## <a name="delete-a-volume-group"></a><span data-ttu-id="f0c6b-183">Bir birim grubu Sil</span><span class="sxs-lookup"><span data-stu-id="f0c6b-183">Delete a volume group</span></span>
<span data-ttu-id="f0c6b-184">Aşağıdaki yordam toodelete bir birim grubu hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-184">Use hello following procedure toodelete a volume group.</span></span> 

> [!WARNING]
> <span data-ttu-id="f0c6b-185">Bu da hello birim grubu ile ilişkili tüm hello yedeklerini siler.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-185">This also deletes all hello backups associated with hello volume group.</span></span>
> 
> 

#### <a name="toodelete-a-volume-group"></a><span data-ttu-id="f0c6b-186">toodelete bir birim grubu</span><span class="sxs-lookup"><span data-stu-id="f0c6b-186">toodelete a volume group</span></span>
1. <span data-ttu-id="f0c6b-187">Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-187">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="f0c6b-188">Merhaba, **kapsam** bölmesinde hello genişletin **birim grupları** düğümü, bir birim grubu adını sağ tıklatın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-188">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Delete**.</span></span>
3. <span data-ttu-id="f0c6b-189">Merhaba **birim grubunu Sil** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-189">hello **Delete Volume Group** dialog box appears.</span></span> <span data-ttu-id="f0c6b-190">Tür **Onayla** hello metin kutusuna ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-190">Type **Confirm** in hello text box, and then click **OK**.</span></span>
   
    <span data-ttu-id="f0c6b-191">Silinen hello birim grubu kaybolduktan hello hello listesinden **sonuçları** bölmesinde ve o birimi grubuyla ilişkili olan tüm yedeklemeler hello yedekleme Kataloğu'ndan silinir.</span><span class="sxs-lookup"><span data-stu-id="f0c6b-191">hello deleted volume group vanishes from hello list in hello **Results** pane and all backups that are associated with that volume group are deleted from hello backup catalog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0c6b-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f0c6b-192">Next steps</span></span>
* <span data-ttu-id="f0c6b-193">Nasıl çok öğrenin[StorSimple Snapshot Manager tooadminister StorSimple çözümünüzün kullanmak](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="f0c6b-193">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="f0c6b-194">Nasıl çok öğrenin[StorSimple Snapshot Manager toocreate kullanın ve yedekleme ilkelerini yönetme](storsimple-snapshot-manager-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f0c6b-194">Learn how too[use StorSimple Snapshot Manager toocreate and manage backup policies](storsimple-snapshot-manager-manage-backup-policies.md).</span></span>

