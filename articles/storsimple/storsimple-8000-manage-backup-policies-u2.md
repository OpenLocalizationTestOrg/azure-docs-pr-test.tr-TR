---
title: aaaManage StorSimple 8000 serisi yedekleme ilkeleri | Microsoft Docs
description: "Merhaba StorSimple cihaz Yöneticisi hizmeti toocreate kullanın ve el ile yedekleme, yedekleme zamanlamaları ve yedekleme bekletme StorSimple 8000 serisi aygıtta yönetmek nasıl açıklanmaktadır."
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a><span data-ttu-id="9825c-103">Azure portal toomanage yedekleme ilkelerini Hello StorSimple cihaz Yöneticisi hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="9825c-103">Use hello StorSimple Device Manager service in Azure portal toomanage backup policies</span></span>


## <a name="overview"></a><span data-ttu-id="9825c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9825c-104">Overview</span></span>

<span data-ttu-id="9825c-105">Bu öğretici nasıl toouse hello StorSimple cihaz Yöneticisi hizmeti açıklanmaktadır **yedekleme İlkesi** dikey toocontrol yedekleme işlemleri ve yedekleme bekletme StorSimple birimlerinizi için.</span><span class="sxs-lookup"><span data-stu-id="9825c-105">This tutorial explains how toouse hello StorSimple Device Manager service **Backup policy** blade toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="9825c-106">Ayrıca açıklanır nasıl toocomplete el ile yedekleme.</span><span class="sxs-lookup"><span data-stu-id="9825c-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="9825c-107">Bir birim yedeklediğinizde, yerel bir anlık görüntüsü veya bir bulut anlık görüntüsü toocreate seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9825c-107">When you back up a volume, you can choose toocreate a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="9825c-108">Yerel olarak sabitlenmiş bir birim yedekleme yapıyorsanız, bir bulut anlık görüntüsü belirtilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="9825c-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="9825c-109">Çok sayıda karmaşası çok sahip bir veri kümesi ile birlikte yerel olarak sabitlenmiş bir birim yerel anlık görüntüleri alma hızla yerel alana çalıştırabilir durumda neden olur.</span><span class="sxs-lookup"><span data-stu-id="9825c-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="9825c-110">Yerel anlık görüntüleri tootake seçerseniz, daha az günlük anlık görüntüleri tooback hello en son durumunu almak için günde bir korumak ve bunları silin öneririz.</span><span class="sxs-lookup"><span data-stu-id="9825c-110">If you choose tootake local snapshots, we recommend that you take fewer daily snapshots tooback up hello most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="9825c-111">Yerel olarak sabitlenmiş bir birim bir bulut anlık görüntüsünü, burada, yinelenenleri kaldırılmış sıkıştırılmış ve yalnızca değiştirilen hello veri toohello bulut kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="9825c-111">When you take a cloud snapshot of a locally pinned volume, you copy only hello changed data toohello cloud, where it is deduplicated and compressed.</span></span>

## <a name="hello-backup-policy-blade"></a><span data-ttu-id="9825c-112">Merhaba yedekleme İlkesi dikey penceresi</span><span class="sxs-lookup"><span data-stu-id="9825c-112">hello Backup policy blade</span></span>

<span data-ttu-id="9825c-113">Merhaba **yedekleme İlkesi** StorSimple cihazınız için dikey verir toomanage yedekleme ilkeleri ve zamanlama yerel ve bulut anlık görüntüleri.</span><span class="sxs-lookup"><span data-stu-id="9825c-113">hello **Backup policy** blade for your StorSimple device allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="9825c-114">Yedekleme ilkeleri kullanılan tooconfigure yedekleme zamanlamaları ve yedekleme bekletme birimlerin bir koleksiyon için ' dir.</span><span class="sxs-lookup"><span data-stu-id="9825c-114">Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.</span></span> <span data-ttu-id="9825c-115">Yedekleme ilkeleri tootake birden çok birim görüntüsünü aynı anda etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="9825c-115">Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="9825c-116">Bu, bir yedekleme İlkesi tarafından oluşturulan hello yedekler kilitlenme tutarlı kopyaları olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="9825c-116">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span>

<span data-ttu-id="9825c-117">Merhaba yedekleme ilkeleri sekmeli liste Ayrıca, toofilter hello varolan yedekleme ilkeleri tarafından bir veya daha fazla alanları izleyen hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="9825c-117">hello backup policies tabular listing also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="9825c-118">**İlke adı** – hello hello ilkesiyle ilişkili ad.</span><span class="sxs-lookup"><span data-stu-id="9825c-118">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="9825c-119">Merhaba farklı ilkeleri türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9825c-119">hello different types of policies include:</span></span>

  * <span data-ttu-id="9825c-120">Zamanlanmış ilkeleri hello kullanıcı tarafından açıkça oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9825c-120">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="9825c-121">Başlangıçta hello StorSimple Snapshot Manager oluşturulan ilkeleri içe.</span><span class="sxs-lookup"><span data-stu-id="9825c-121">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="9825c-122">Bu hello ilkeleri alındığı hello StorSimple Snapshot Manager konak açıklayan bir etiket vardır.</span><span class="sxs-lookup"><span data-stu-id="9825c-122">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9825c-123">Otomatik veya varsayılan yedekleme ilkeleri artık hello birim oluşturma sırasında etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="9825c-123">Automatic or default backup policies are no longer enabled at hello time of volume creation.</span></span>

* <span data-ttu-id="9825c-124">**Son başarılı yedekleme** – başlangıç tarihi ve Bu ilkeyle alınan hello son başarılı yedekleme.</span><span class="sxs-lookup"><span data-stu-id="9825c-124">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>

* <span data-ttu-id="9825c-125">**Sonraki yedekleme** – başlangıç tarihi ve bu ilke tarafından başlatılan hello sonraki zamanlanmış yedekleme.</span><span class="sxs-lookup"><span data-stu-id="9825c-125">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>

* <span data-ttu-id="9825c-126">**Birimleri** – hello hello ilkesiyle ilişkili birimler.</span><span class="sxs-lookup"><span data-stu-id="9825c-126">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="9825c-127">Yedekleme oluşturulduğunda bir yedekleme ilkesiyle ilişkili tüm hello birimler birlikte gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="9825c-127">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>

* <span data-ttu-id="9825c-128">**Zamanlamalar** – hello hello yedekleme ilkeyle ilişkilendirilmiş zamanlamaları sayısı.</span><span class="sxs-lookup"><span data-stu-id="9825c-128">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="9825c-129">Yedekleme ilkelerine gerçekleştirebileceğiniz sık kullanılan hello işlemleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="9825c-129">hello frequently used operations that you can perform for backup policies are:</span></span>

* <span data-ttu-id="9825c-130">Yedekleme ilkesi ekleme</span><span class="sxs-lookup"><span data-stu-id="9825c-130">Add a backup policy</span></span>
* <span data-ttu-id="9825c-131">Ekleyin veya bir zamanlama değiştirin</span><span class="sxs-lookup"><span data-stu-id="9825c-131">Add or modify a schedule</span></span>
* <span data-ttu-id="9825c-132">Bir birim Ekle Kaldır</span><span class="sxs-lookup"><span data-stu-id="9825c-132">Add or remove a volume</span></span>
* <span data-ttu-id="9825c-133">Bir yedekleme ilkesi silme</span><span class="sxs-lookup"><span data-stu-id="9825c-133">Delete a backup policy</span></span>
* <span data-ttu-id="9825c-134">El ile yedekleyin</span><span class="sxs-lookup"><span data-stu-id="9825c-134">Take a manual backup</span></span>

## <a name="add-a-backup-policy"></a><span data-ttu-id="9825c-135">Yedekleme ilkesi ekleme</span><span class="sxs-lookup"><span data-stu-id="9825c-135">Add a backup policy</span></span>

<span data-ttu-id="9825c-136">Bir yedekleme İlkesi tooautomatically zamanlama Yedeklemelerinizin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="9825c-136">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="9825c-137">Bir birim ilk oluşturduğunuzda, biriminiz ile ilişkili varsayılan yedekleme ilkesi bulunmamaktadır.</span><span class="sxs-lookup"><span data-stu-id="9825c-137">When you first create a volume, there is no default backup policy associated with your volume.</span></span> <span data-ttu-id="9825c-138">Bir yedekleme İlkesi tooprotect birim verilerini atayın ve tooadd gerekir.</span><span class="sxs-lookup"><span data-stu-id="9825c-138">You need tooadd and assign a backup policy tooprotect volume data.</span></span>

<span data-ttu-id="9825c-139">Hello Azure portal tooadd StorSimple cihazınız için bir yedekleme İlkesi adımlarını izleyerek hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="9825c-139">Perform hello following steps in hello Azure portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="9825c-140">Hello İlkesi ekledikten sonra bir zamanlama tanımlayabilirsiniz (bkz [Ekle ya da bir zamanlamayı değiştirmek](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="9825c-140">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="9825c-141">Ekleyin veya bir zamanlama değiştirin</span><span class="sxs-lookup"><span data-stu-id="9825c-141">Add or modify a schedule</span></span>

<span data-ttu-id="9825c-142">Ekleyin veya ekli tooan varolan yedekleme İlkesi, StorSimple Cihazınızda bir zamanlama değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9825c-142">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="9825c-143">Bir zamanlamayı değiştirmek veya hello hello Azure portal tooadd adımlarını izleyerek gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9825c-143">Perform hello following steps in hello Azure portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a><span data-ttu-id="9825c-144">Bir birim Ekle Kaldır</span><span class="sxs-lookup"><span data-stu-id="9825c-144">Add or remove a volume</span></span>

<span data-ttu-id="9825c-145">Ekleyebilir veya tooa yedekleme İlkesi, StorSimple Cihazınızda atanmış bir birim kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9825c-145">You can add or remove a volume assigned tooa backup policy on your StorSimple device.</span></span> <span data-ttu-id="9825c-146">Bir birimi kaldırmak veya hello hello Azure portal tooadd adımlarını izleyerek gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9825c-146">Perform hello following steps in hello Azure portal tooadd or remove a volume.</span></span>

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a><span data-ttu-id="9825c-147">Bir yedekleme ilkesi silme</span><span class="sxs-lookup"><span data-stu-id="9825c-147">Delete a backup policy</span></span>

<span data-ttu-id="9825c-148">StorSimple Cihazınızda hello Azure portal toodelete bir yedekleme İlkesi adımlarını izleyerek hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="9825c-148">Perform hello following steps in hello Azure portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="9825c-149">El ile yedekleyin</span><span class="sxs-lookup"><span data-stu-id="9825c-149">Take a manual backup</span></span>

<span data-ttu-id="9825c-150">Tek bir birim için hello Azure portal toocreate isteğe bağlı (el ile) yedekleme adımlarını izleyerek hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="9825c-150">Perform hello following steps in hello Azure portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a><span data-ttu-id="9825c-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9825c-151">Next steps</span></span>

<span data-ttu-id="9825c-152">Daha fazla bilgi edinmek [StorSimple Cihazınızı hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanarak](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="9825c-152">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

