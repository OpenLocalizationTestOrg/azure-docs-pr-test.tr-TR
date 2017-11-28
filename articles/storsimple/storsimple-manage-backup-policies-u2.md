---
title: "StorSimple yedekleme ilkelerini yönetme | Microsoft Docs"
description: "El ile yedekleme, yedekleme zamanlamaları ve yedekleme bekletme oluşturmak ve yönetmek için StorSimple Yöneticisi hizmeti nasıl kullanabileceğiniz açıklanır."
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
ms.openlocfilehash: 5448247428ab96887470c6b53f7a9b3dcd9238f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-backup-policies-update-2"></a><span data-ttu-id="0c56a-103">Yedekleme ilkeleri (güncelleştirme 2) yönetmek için StorSimple Yöneticisi hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="0c56a-103">Use the StorSimple Manager service to manage backup policies (Update 2)</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="0c56a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0c56a-104">Overview</span></span>
<span data-ttu-id="0c56a-105">Bu öğretici StorSimple Yöneticisi hizmetini kullanma açıklanmaktadır **yedekleme ilkeleri** yedekleme işlemleri ve yedekleme bekletme için StorSimple birimlerinizi denetlemek için sayfa.</span><span class="sxs-lookup"><span data-stu-id="0c56a-105">This tutorial explains how to use the StorSimple Manager service **Backup Policies** page to control backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="0c56a-106">Ayrıca, el ile yedekleme tamamlamak nasıl açıklanır.</span><span class="sxs-lookup"><span data-stu-id="0c56a-106">It also describes how to complete a manual backup.</span></span>

<span data-ttu-id="0c56a-107">Bir birim yedeklediğinizde, yerel bir anlık görüntüsü veya bir bulut anlık görüntüsü oluşturmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0c56a-107">When you back up a volume, you can choose to create a local snapshot or a cloud snapshot.</span></span> <span data-ttu-id="0c56a-108">Yerel olarak sabitlenmiş bir birim yedekleme yapıyorsanız, bir bulut anlık görüntüsü belirtilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="0c56a-108">If you are backing up a locally pinned volume, we recommend that you specify a cloud snapshot.</span></span> <span data-ttu-id="0c56a-109">Çok sayıda karmaşası çok sahip bir veri kümesi ile birlikte yerel olarak sabitlenmiş bir birim yerel anlık görüntüleri alma hızla yerel alana çalıştırabilir durumda neden olur.</span><span class="sxs-lookup"><span data-stu-id="0c56a-109">Taking a large number of local snapshots of a locally pinned volume coupled with a data set that has a lot of churn will result in a situation in which you could rapidly run out of local space.</span></span> <span data-ttu-id="0c56a-110">Yerel anlık görüntüsünü seçerseniz, en son duruma geri, bunları bir gün için korumak için daha az günlük anlık görüntülerini almak ve bunları silmek öneririz.</span><span class="sxs-lookup"><span data-stu-id="0c56a-110">If you choose to take local snapshots, we recommend that you take fewer daily snapshots to back up the most recent state, retain them for a day, and then delete them.</span></span>

<span data-ttu-id="0c56a-111">Yerel olarak sabitlenmiş bir birim bir bulut anlık görüntüsünü, burada, yinelenenleri kaldırılmış sıkıştırılmış ve buluta, yalnızca değiştirilen verileri kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0c56a-111">When you take a cloud snapshot of a locally pinned volume, you copy only the changed data to the cloud, where it is deduplicated and compressed.</span></span> 

## <a name="the-backup-policies-page"></a><span data-ttu-id="0c56a-112">Yedekleme ilkeleri sayfası</span><span class="sxs-lookup"><span data-stu-id="0c56a-112">The Backup Policies page</span></span>
<span data-ttu-id="0c56a-113">**Yedekleme ilkeleri** sayfası yedekleme ilkelerini yönetmek ve yerel zamanlamak ve bulut anlık görüntüleri olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="0c56a-113">The **Backup Policies** page allows you to manage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="0c56a-114">(Yedekleme ilkeleri yedekleme zamanlamaları ve yedekleme bekletme birimlerin bir koleksiyon için yapılandırmak için kullanılır.) Yedekleme ilkeleri aynı anda birden çok birim bir anlık görüntüsünü olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="0c56a-114">(Backup policies are used to configure backup schedules and backup retention for a collection of volumes.) Backup policies enable you to take a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="0c56a-115">Bu, bir yedekleme İlkesi tarafından oluşturulan yedekleri kilitlenme tutarlı kopyaları olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0c56a-115">This means that the backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="0c56a-116">**Yedekleme ilkeleri** sayfasında yedekleme ilkelerini, türlerini, ilişkili birimler, yedeklerini korunur ve bu ilkeler etkinleştirme seçeneği listelenir.</span><span class="sxs-lookup"><span data-stu-id="0c56a-116">The **Backup Policies** page lists the backup policies, their types, the associated volumes, the number of backups retained, and the option to enable these policies.</span></span>

<span data-ttu-id="0c56a-117">**Yedekleme ilkeleri** sayfa Ayrıca, varolan yedekleme ilkeleri bir veya daha fazla aşağıdaki alanları tarafından filtre olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="0c56a-117">The **Backup Policies** page also allows you to filter the existing backup policies by one or more of the following fields:</span></span>

* <span data-ttu-id="0c56a-118">**İlke adı** – ilkeyle ilişkili ad.</span><span class="sxs-lookup"><span data-stu-id="0c56a-118">**Policy name** – The name associated with the policy.</span></span> <span data-ttu-id="0c56a-119">İlkeleri farklı türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0c56a-119">The different types of policies include:</span></span>
  
  * <span data-ttu-id="0c56a-120">Zamanlanmış ilkeleri, kullanıcı tarafından açıkça oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0c56a-120">Scheduled policies, which are explicitly created by the user.</span></span>
  * <span data-ttu-id="0c56a-121">Bu birimi seçeneği için varsayılan yedekleme birim oluşturma sırasında etkinleştirildiğinde oluşturulan otomatik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="0c56a-121">Automatic policies, which are created when the default backup for this volume option was enabled at the time of volume creation.</span></span> <span data-ttu-id="0c56a-122">Bu ilkeler olarak adlandırılır *VolumeName*_Default nerede *VolumeName* Klasik Azure portalındaki kullanıcı tarafından yapılandırılan StorSimple biriminin adına başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="0c56a-122">These policies are named as *VolumeName*_Default where *VolumeName* refers to the name of the StorSimple volume configured by the user in the Azure classic portal.</span></span> <span data-ttu-id="0c56a-123">22:30 aygıt zamanında başlayan günlük bulut anlık görüntüleri otomatik ilkeleri sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="0c56a-123">The automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="0c56a-124">StorSimple anlık görüntü Yöneticisi'nde ilk olarak oluşturulan alınan ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="0c56a-124">Imported policies, which were originally created in the StorSimple Snapshot Manager.</span></span> <span data-ttu-id="0c56a-125">Bu ilkeleri alındığı StorSimple Snapshot Manager konak açıklayan bir etiket vardır.</span><span class="sxs-lookup"><span data-stu-id="0c56a-125">These have a tag that describes the StorSimple Snapshot Manager host that the policies were imported from.</span></span>
* <span data-ttu-id="0c56a-126">**Birimleri** – ilkeyle ilişkili birimler.</span><span class="sxs-lookup"><span data-stu-id="0c56a-126">**Volumes** – The volumes associated with the policy.</span></span> <span data-ttu-id="0c56a-127">Yedekleme oluşturulduğunda bir yedekleme ilkesiyle ilişkili tüm birimler birlikte gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="0c56a-127">All the volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="0c56a-128">**Son başarılı yedekleme** – Bu ilkeyle alındığı son başarılı yedekleme saati ve tarihi.</span><span class="sxs-lookup"><span data-stu-id="0c56a-128">**Last successful backup** – The date and time of the last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="0c56a-129">**Sonraki yedekleme** – Bu ilke tarafından başlatılan bir sonraki zamanlanmış yedekleme saati ve tarihi.</span><span class="sxs-lookup"><span data-stu-id="0c56a-129">**Next backup** – The date and time of the next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="0c56a-130">**Zamanlamalar** – yedekleme ilkeyle ilişkilendirilmiş zamanlamaları sayısı.</span><span class="sxs-lookup"><span data-stu-id="0c56a-130">**Schedules** – The number of schedules associated with the backup policy.</span></span>

<span data-ttu-id="0c56a-131">Bu sayfadan gerçekleştirebileceğiniz sık kullanılan işlemleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0c56a-131">The frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="0c56a-132">Yedekleme ilkesi ekleme</span><span class="sxs-lookup"><span data-stu-id="0c56a-132">Add a backup policy</span></span> 
* <span data-ttu-id="0c56a-133">Ekleyin veya bir zamanlama değiştirin</span><span class="sxs-lookup"><span data-stu-id="0c56a-133">Add or modify a schedule</span></span> 
* <span data-ttu-id="0c56a-134">Bir yedekleme ilkesi silme</span><span class="sxs-lookup"><span data-stu-id="0c56a-134">Delete a backup policy</span></span> 
* <span data-ttu-id="0c56a-135">El ile yedekleyin</span><span class="sxs-lookup"><span data-stu-id="0c56a-135">Take a manual backup</span></span> 
* <span data-ttu-id="0c56a-136">Birden çok birimleri ve zamanlamaları özel bir yedekleme ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c56a-136">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="0c56a-137">Yedekleme ilkesi ekleme</span><span class="sxs-lookup"><span data-stu-id="0c56a-137">Add a backup policy</span></span>
<span data-ttu-id="0c56a-138">Otomatik olarak Yedeklemelerinizin zamanlamak için bir yedekleme ilkesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0c56a-138">Add a backup policy to automatically schedule your backups.</span></span> <span data-ttu-id="0c56a-139">StorSimple cihazınız için bir yedekleme ilkesi eklemek için Azure Klasik portalında aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0c56a-139">Perform the following steps in the Azure classic portal to add a backup policy for your StorSimple device.</span></span> <span data-ttu-id="0c56a-140">İlkeyi ekledikten sonra bir zamanlama tanımlayabilirsiniz (bkz [Ekle ya da bir zamanlamayı değiştirmek](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="0c56a-140">After you add the policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

<span data-ttu-id="0c56a-141">![Video var](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video var**</span><span class="sxs-lookup"><span data-stu-id="0c56a-141">![Video available](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="0c56a-142">Yerel oluşturma veya yedekleme İlkesi bulut gösteren bir video izlemek için tıklatın [burada](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="0c56a-142">To watch a video that demonstrates how to create a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="0c56a-143">Ekleyin veya bir zamanlama değiştirin</span><span class="sxs-lookup"><span data-stu-id="0c56a-143">Add or modify a schedule</span></span>
<span data-ttu-id="0c56a-144">Ekleyin veya mevcut bir yedekleme İlkesi, StorSimple Cihazınızda bağlı olduğu bir zamanlama değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0c56a-144">You can add or modify a schedule that is attached to an existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="0c56a-145">Eklemek veya bir zamanlamayı değiştirmek için Azure Klasik portalında aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0c56a-145">Perform the following steps in the Azure classic portal to add or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="0c56a-146">Bir yedekleme ilkesi silme</span><span class="sxs-lookup"><span data-stu-id="0c56a-146">Delete a backup policy</span></span>
<span data-ttu-id="0c56a-147">Bir yedekleme İlkesi, StorSimple Cihazınızda silmek için Azure Klasik portalında aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0c56a-147">Perform the following steps in the Azure classic portal to delete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="0c56a-148">El ile yedekleyin</span><span class="sxs-lookup"><span data-stu-id="0c56a-148">Take a manual backup</span></span>
<span data-ttu-id="0c56a-149">Tek bir birim için bir isteğe bağlı (el ile) yedekleme oluşturmak için Azure Klasik portalında aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0c56a-149">Perform the following steps in the Azure classic portal to create an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="0c56a-150">Birden çok birimleri ve zamanlamaları özel bir yedekleme ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="0c56a-150">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="0c56a-151">Birden çok birimleri ve zamanlamaları sahip özel bir yedekleme ilkesi oluşturmak için Azure Klasik portalında aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="0c56a-151">Perform the following steps in the Azure classic portal to create a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a><span data-ttu-id="0c56a-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0c56a-152">Next steps</span></span>
<span data-ttu-id="0c56a-153">Daha fazla bilgi edinmek [StorSimple Cihazınızı yönetmek için StorSimple Yöneticisi hizmetini kullanma](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="0c56a-153">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

