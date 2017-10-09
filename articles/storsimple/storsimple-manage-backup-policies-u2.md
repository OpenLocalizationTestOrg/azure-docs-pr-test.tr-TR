---
title: aaaManage StorSimple yedekleme ilkelerinizi | Microsoft Docs
description: "Merhaba StorSimple Yöneticisi hizmet toocreate kullanın ve el ile yedekleme, yedekleme zamanlamaları ve yedekleme bekletme yönetmek nasıl açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 4a2db707-bbfc-425c-bfeb-bc5c97781873
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 7b01f29a8d8a096d9890c8406557021317b9baff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies-update-2"></a><span data-ttu-id="f8ad3-103">Merhaba StorSimple Yöneticisi hizmeti toomanage yedekleme ilkeleri (güncelleştirme 2) kullanın</span><span class="sxs-lookup"><span data-stu-id="f8ad3-103">Use hello StorSimple Manager service toomanage backup policies (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="f8ad3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f8ad3-104">Overview</span></span>
<span data-ttu-id="f8ad3-105">Bu öğretici nasıl toouse hello StorSimple Yöneticisi hizmeti açıklanmaktadır **yedekleme ilkeleri** sayfa toocontrol yedekleme işlemleri ve yedekleme bekletme StorSimple birimlerinizi için.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="f8ad3-106">Ayrıca açıklanır nasıl toocomplete el ile yedekleme.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="f8ad3-107">Bir birim yedeklediğinizde, yerel bir anlık görüntüsü veya bir bulut anlık görüntüsü toocreate seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="f8ad3-108">Yerel olarak sabitlenmiş bir birim yedekleme yapıyorsanız, bir bulut anlık görüntüsü belirtilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="f8ad3-109">Çok sayıda karmaşası çok sahip bir veri kümesi ile birlikte yerel olarak sabitlenmiş bir birim yerel anlık görüntüleri alma hızla yerel alana çalıştırabilir durumda neden olur.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="f8ad3-110">Yerel anlık görüntüleri tootake seçerseniz, daha az günlük anlık görüntüleri tooback hello en son durumunu almak için günde bir korumak ve bunları silin öneririz.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="f8ad3-111">Yerel olarak sabitlenmiş bir birim bir bulut anlık görüntüsünü, burada, yinelenenleri kaldırılmış sıkıştırılmış ve yalnızca değiştirilen hello veri toohello bulut kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span> 

## <a name="hello-backup-policies-page"></a><span data-ttu-id="f8ad3-112">Merhaba yedekleme ilkeleri sayfası</span><span class="sxs-lookup"><span data-stu-id="f8ad3-112">hello Backup Policies page</span></span>
<span data-ttu-id="f8ad3-113">Merhaba **yedekleme ilkeleri** sayfası sağlar toomanage yedekleme ilkeleri ve zamanlama yerel ve bulut anlık görüntüleri.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-113">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="f8ad3-114">(Yedekleme kullanılan tooconfigure yedekleme zamanlamaları ve yedekleme bekletme birimlerin bir koleksiyon için ilkelerdir.) Yedekleme ilkeleri tootake birden çok birim görüntüsünü aynı anda etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-114">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="f8ad3-115">Bu, bir yedekleme İlkesi tarafından oluşturulan hello yedekler kilitlenme tutarlı kopyaları olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-115">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="f8ad3-116">Merhaba **yedekleme ilkeleri** sayfası hello yedekleme ilkeleri, kendi türleri, ilişkili hello birimleri, korunur yedeklemeleri hello sayısını listeler ve bu ilkeler hello seçeneği tooenable.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-116">hello **Backup Policies** page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="f8ad3-117">Merhaba **yedekleme ilkeleri** sayfası aynı zamanda toofilter hello varolan yedekleme ilkeleri tarafından bir veya daha fazla alanları izleyen Merhaba, sağlar:</span><span class="sxs-lookup"><span data-stu-id="f8ad3-117">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="f8ad3-118">**İlke adı** – hello hello ilkesiyle ilişkili ad.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="f8ad3-119">Merhaba farklı ilkeleri türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f8ad3-119">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="f8ad3-120">Zamanlanmış ilkeleri hello kullanıcı tarafından açıkça oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="f8ad3-121">Bu birimi seçeneği için Hello varsayılan yedekleme hello birim oluşturma sırasında etkinleştirildiğinde oluşturulan otomatik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-121">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="f8ad3-122">Bu ilkeler olarak adlandırılır *VolumeName*_Default nerede *VolumeName* hello hello Klasik Azure portalı hello kullanıcı tarafından yapılandırılan StorSimple biriminin toohello adını gösterir.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-122">These policies are named as *VolumeName*_Default where *VolumeName* refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="f8ad3-123">22:30 aygıt zamanında başlayan günlük bulut anlık görüntüleri Hello otomatik ilkeleri sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-123">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="f8ad3-124">Başlangıçta hello StorSimple Snapshot Manager oluşturulan ilkeleri içe.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-124">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="f8ad3-125">Bu hello ilkeleri alındığı hello StorSimple Snapshot Manager konak açıklayan bir etiket vardır.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-125">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="f8ad3-126">**Birimleri** – hello hello ilkesiyle ilişkili birimler.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="f8ad3-127">Yedekleme oluşturulduğunda bir yedekleme ilkesiyle ilişkili tüm hello birimler birlikte gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="f8ad3-128">**Son başarılı yedekleme** – başlangıç tarihi ve Bu ilkeyle alınan hello son başarılı yedekleme.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-128">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="f8ad3-129">**Sonraki yedekleme** – başlangıç tarihi ve bu ilke tarafından başlatılan hello sonraki zamanlanmış yedekleme.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-129">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="f8ad3-130">**Zamanlamalar** – hello hello yedekleme ilkeyle ilişkilendirilmiş zamanlamaları sayısı.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-130">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="f8ad3-131">Bu sayfadan gerçekleştirebileceğiniz sık kullanılan hello işlemleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f8ad3-131">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="f8ad3-132">Yedekleme ilkesi ekleme</span><span class="sxs-lookup"><span data-stu-id="f8ad3-132">Add a backup policy</span></span> 
* <span data-ttu-id="f8ad3-133">Ekleyin veya bir zamanlama değiştirin</span><span class="sxs-lookup"><span data-stu-id="f8ad3-133">Add or modify a schedule</span></span> 
* <span data-ttu-id="f8ad3-134">Bir yedekleme ilkesi silme</span><span class="sxs-lookup"><span data-stu-id="f8ad3-134">Delete a backup policy</span></span> 
* <span data-ttu-id="f8ad3-135">El ile yedekleyin</span><span class="sxs-lookup"><span data-stu-id="f8ad3-135">Take a manual backup</span></span> 
* <span data-ttu-id="f8ad3-136">Birden çok birimleri ve zamanlamaları özel bir yedekleme ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8ad3-136">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="f8ad3-137">Yedekleme ilkesi ekleme</span><span class="sxs-lookup"><span data-stu-id="f8ad3-137">Add a backup policy</span></span>
<span data-ttu-id="f8ad3-138">Bir yedekleme İlkesi tooautomatically zamanlama Yedeklemelerinizin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-138">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="f8ad3-139">Hello Azure Klasik portalı tooadd StorSimple cihazınız için bir yedekleme İlkesi adımlarını izleyerek hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-139">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="f8ad3-140">Hello İlkesi ekledikten sonra bir zamanlama tanımlayabilirsiniz (bkz [Ekle ya da bir zamanlamayı değiştirmek](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="f8ad3-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

<span data-ttu-id="f8ad3-141">![Video var](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video var**</span><span class="sxs-lookup"><span data-stu-id="f8ad3-141">![Video available](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="f8ad3-142">toowatch nasıl toocreate yerel veya Bulut yedekleme İlkesi, gösteren bir video tıklatın [burada](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="f8ad3-142">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="f8ad3-143">Ekleyin veya bir zamanlama değiştirin</span><span class="sxs-lookup"><span data-stu-id="f8ad3-143">Add or modify a schedule</span></span>
<span data-ttu-id="f8ad3-144">Ekleyin veya ekli tooan varolan yedekleme İlkesi, StorSimple Cihazınızda bir zamanlama değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-144">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="f8ad3-145">Bir zamanlamayı değiştirmek veya hello hello Azure Klasik portalı tooadd adımlarını izleyerek gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-145">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="f8ad3-146">Bir yedekleme ilkesi silme</span><span class="sxs-lookup"><span data-stu-id="f8ad3-146">Delete a backup policy</span></span>
<span data-ttu-id="f8ad3-147">StorSimple Cihazınızda hello Azure Klasik portalı toodelete bir yedekleme İlkesi adımlarını izleyerek hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-147">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="f8ad3-148">El ile yedekleyin</span><span class="sxs-lookup"><span data-stu-id="f8ad3-148">Take a manual backup</span></span>
<span data-ttu-id="f8ad3-149">Tek bir birim için hello Azure Klasik portalı toocreate isteğe bağlı (el ile) yedekleme adımlarını izleyerek hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-149">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="f8ad3-150">Birden çok birimleri ve zamanlamaları özel bir yedekleme ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f8ad3-150">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="f8ad3-151">Hello Azure Klasik portalı toocreate birden çok birimleri ve zamanlamaları sahip özel bir yedekleme İlkesi adımlarını izleyerek hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="f8ad3-151">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a><span data-ttu-id="f8ad3-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f8ad3-152">Next steps</span></span>
<span data-ttu-id="f8ad3-153">Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f8ad3-153">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

