---
title: aaaManage StorSimple yedekleme ilkelerinizi | Microsoft Docs
description: "Merhaba StorSimple Yöneticisi hizmet toocreate kullanın ve el ile yedekleme, yedekleme zamanlamaları ve yedekleme bekletme yönetmek nasıl açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: d1834bc8-d520-4463-82ae-3b32fabd021c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 710cbe54d14031b4de43e9da292ed169085d5af9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies"></a><span data-ttu-id="6e52a-103">Merhaba StorSimple Yöneticisi hizmet toomanage yedekleme ilkelerini kullanma</span><span class="sxs-lookup"><span data-stu-id="6e52a-103">Use hello StorSimple Manager service toomanage backup policies</span></span>
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a><span data-ttu-id="6e52a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6e52a-104">Overview</span></span>
<span data-ttu-id="6e52a-105">Bu öğretici nasıl toouse hello StorSimple Yöneticisi hizmeti açıklanmaktadır **yedekleme ilkeleri** sayfa toocontrol yedekleme işlemleri ve yedekleme bekletme StorSimple birimlerinizi için.</span><span class="sxs-lookup"><span data-stu-id="6e52a-105">This tutorial explains how toouse hello StorSimple Manager service **Backup Policies** page toocontrol backup processes and backup retention for your StorSimple volumes.</span></span> <span data-ttu-id="6e52a-106">Ayrıca açıklanır nasıl toocomplete el ile yedekleme.</span><span class="sxs-lookup"><span data-stu-id="6e52a-106">It also describes how toocomplete a manual backup.</span></span>

<span data-ttu-id="6e52a-107">Merhaba **yedekleme ilkeleri** sayfası sağlar toomanage yedekleme ilkeleri ve zamanlama yerel ve bulut anlık görüntüleri.</span><span class="sxs-lookup"><span data-stu-id="6e52a-107">hello **Backup Policies** page allows you toomanage backup policies and schedule local and cloud snapshots.</span></span> <span data-ttu-id="6e52a-108">(Yedekleme kullanılan tooconfigure yedekleme zamanlamaları ve yedekleme bekletme birimlerin bir koleksiyon için ilkelerdir.) Yedekleme ilkeleri tootake birden çok birim görüntüsünü aynı anda etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6e52a-108">(Backup policies are used tooconfigure backup schedules and backup retention for a collection of volumes.) Backup policies enable you tootake a snapshot of multiple volumes simultaneously.</span></span> <span data-ttu-id="6e52a-109">Bu, bir yedekleme İlkesi tarafından oluşturulan hello yedekler kilitlenme tutarlı kopyaları olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6e52a-109">This means that hello backups created by a backup policy will be crash-consistent copies.</span></span> <span data-ttu-id="6e52a-110">Bu sayfayı hello yedekleme ilkeleri, kendi türleri, ilişkili hello birimleri, korunur yedekleme hello sayısı listeler ve bu ilkeler seçeneği tooenable hello.</span><span class="sxs-lookup"><span data-stu-id="6e52a-110">This page lists hello backup policies, their types, hello associated volumes, hello number of backups retained, and hello option tooenable these policies.</span></span>

<span data-ttu-id="6e52a-111">Merhaba **yedekleme ilkeleri** sayfası aynı zamanda toofilter hello varolan yedekleme ilkeleri tarafından bir veya daha fazla alanları izleyen Merhaba, sağlar:</span><span class="sxs-lookup"><span data-stu-id="6e52a-111">hello **Backup Policies** page also allows you toofilter hello existing backup policies by one or more of hello following fields:</span></span>

* <span data-ttu-id="6e52a-112">**İlke adı** – hello hello ilkesiyle ilişkili ad.</span><span class="sxs-lookup"><span data-stu-id="6e52a-112">**Policy name** – hello name associated with hello policy.</span></span> <span data-ttu-id="6e52a-113">Merhaba farklı ilkeleri türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6e52a-113">hello different types of policies include:</span></span>
  
  * <span data-ttu-id="6e52a-114">Zamanlanmış ilkeleri hello kullanıcı tarafından açıkça oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6e52a-114">Scheduled policies, which are explicitly created by hello user.</span></span>
  * <span data-ttu-id="6e52a-115">Bu birimi seçeneği için Hello varsayılan yedekleme hello birim oluşturma sırasında etkinleştirildiğinde oluşturulan otomatik ilkeleri.</span><span class="sxs-lookup"><span data-stu-id="6e52a-115">Automatic policies, which are created when hello default backup for this volume option was enabled at hello time of volume creation.</span></span> <span data-ttu-id="6e52a-116">Bu ilkeler, burada toohello adını hello hello Klasik Azure portalı hello kullanıcı tarafından yapılandırılan StorSimple biriminin birim adı başvuruyor VolumeName_Default olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="6e52a-116">These policies are named as VolumeName_Default where Volume name refers toohello name of hello StorSimple volume configured by hello user in hello Azure classic portal.</span></span> <span data-ttu-id="6e52a-117">22:30 aygıt zamanında başlayan günlük bulut anlık görüntüleri Hello otomatik ilkeleri sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="6e52a-117">hello automatic policies result in daily cloud snapshots beginning at 22:30 device time.</span></span>
  * <span data-ttu-id="6e52a-118">Başlangıçta hello StorSimple Snapshot Manager oluşturulan ilkeleri içe.</span><span class="sxs-lookup"><span data-stu-id="6e52a-118">Imported policies, which were originally created in hello StorSimple Snapshot Manager.</span></span> <span data-ttu-id="6e52a-119">Bu hello ilkeleri alındığı hello StorSimple Snapshot Manager konak açıklayan bir etiket vardır.</span><span class="sxs-lookup"><span data-stu-id="6e52a-119">These have a tag that describes hello StorSimple Snapshot Manager host that hello policies were imported from.</span></span>
* <span data-ttu-id="6e52a-120">**Birimleri** – hello hello ilkesiyle ilişkili birimler.</span><span class="sxs-lookup"><span data-stu-id="6e52a-120">**Volumes** – hello volumes associated with hello policy.</span></span> <span data-ttu-id="6e52a-121">Yedekleme oluşturulduğunda bir yedekleme ilkesiyle ilişkili tüm hello birimler birlikte gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="6e52a-121">All hello volumes associated with a backup policy are grouped together when backups are created.</span></span>
* <span data-ttu-id="6e52a-122">**Son başarılı yedekleme** – başlangıç tarihi ve Bu ilkeyle alınan hello son başarılı yedekleme.</span><span class="sxs-lookup"><span data-stu-id="6e52a-122">**Last successful backup** – hello date and time of hello last successful backup that was taken with this policy.</span></span>
* <span data-ttu-id="6e52a-123">**Sonraki yedekleme** – başlangıç tarihi ve bu ilke tarafından başlatılan hello sonraki zamanlanmış yedekleme.</span><span class="sxs-lookup"><span data-stu-id="6e52a-123">**Next backup** – hello date and time of hello next scheduled backup that will be initiated by this policy.</span></span>
* <span data-ttu-id="6e52a-124">**Zamanlamalar** – hello hello yedekleme ilkeyle ilişkilendirilmiş zamanlamaları sayısı.</span><span class="sxs-lookup"><span data-stu-id="6e52a-124">**Schedules** – hello number of schedules associated with hello backup policy.</span></span>

<span data-ttu-id="6e52a-125">Bu sayfadan gerçekleştirebileceğiniz sık kullanılan hello işlemleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6e52a-125">hello frequently used operations that you can perform from this page are:</span></span>

* <span data-ttu-id="6e52a-126">Yedekleme ilkesi ekleme</span><span class="sxs-lookup"><span data-stu-id="6e52a-126">Add a backup policy</span></span> 
* <span data-ttu-id="6e52a-127">Ekleyin veya bir zamanlama değiştirin</span><span class="sxs-lookup"><span data-stu-id="6e52a-127">Add or modify a schedule</span></span> 
* <span data-ttu-id="6e52a-128">Bir yedekleme ilkesi silme</span><span class="sxs-lookup"><span data-stu-id="6e52a-128">Delete a backup policy</span></span> 
* <span data-ttu-id="6e52a-129">El ile yedekleyin</span><span class="sxs-lookup"><span data-stu-id="6e52a-129">Take a manual backup</span></span> 
* <span data-ttu-id="6e52a-130">Birden çok birimleri ve zamanlamaları özel bir yedekleme ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e52a-130">Create a custom backup policy with multiple volumes and schedules</span></span> 

## <a name="add-a-backup-policy"></a><span data-ttu-id="6e52a-131">Yedekleme ilkesi ekleme</span><span class="sxs-lookup"><span data-stu-id="6e52a-131">Add a backup policy</span></span>
<span data-ttu-id="6e52a-132">Bir yedekleme İlkesi tooautomatically zamanlama Yedeklemelerinizin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6e52a-132">Add a backup policy tooautomatically schedule your backups.</span></span> <span data-ttu-id="6e52a-133">Hello Azure Klasik portalı tooadd StorSimple cihazınız için bir yedekleme İlkesi adımlarını izleyerek hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="6e52a-133">Perform hello following steps in hello Azure classic portal tooadd a backup policy for your StorSimple device.</span></span> <span data-ttu-id="6e52a-134">Hello İlkesi ekledikten sonra bir zamanlama tanımlayabilirsiniz (bkz [Ekle ya da bir zamanlamayı değiştirmek](#add-or-modify-a-schedule)).</span><span class="sxs-lookup"><span data-stu-id="6e52a-134">After you add hello policy, you can define a schedule (see [Add or modify a schedule](#add-or-modify-a-schedule)).</span></span>

[!INCLUDE [storsimple-add-backup-policy](../../includes/storsimple-add-backup-policy.md)]

<span data-ttu-id="6e52a-135">![Video var](./media/storsimple-manage-backup-policies/Video_icon.png) **Video var**</span><span class="sxs-lookup"><span data-stu-id="6e52a-135">![Video available](./media/storsimple-manage-backup-policies/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="6e52a-136">toowatch nasıl toocreate yerel veya Bulut yedekleme İlkesi, gösteren bir video tıklatın [burada](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span><span class="sxs-lookup"><span data-stu-id="6e52a-136">toowatch a video that demonstrates how toocreate a local or cloud backup policy, click [here](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).</span></span>

## <a name="add-or-modify-a-schedule"></a><span data-ttu-id="6e52a-137">Ekleyin veya bir zamanlama değiştirin</span><span class="sxs-lookup"><span data-stu-id="6e52a-137">Add or modify a schedule</span></span>
<span data-ttu-id="6e52a-138">Ekleyin veya ekli tooan varolan yedekleme İlkesi, StorSimple Cihazınızda bir zamanlama değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6e52a-138">You can add or modify a schedule that is attached tooan existing backup policy on your StorSimple device.</span></span> <span data-ttu-id="6e52a-139">Bir zamanlamayı değiştirmek veya hello hello Azure Klasik portalı tooadd adımlarını izleyerek gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e52a-139">Perform hello following steps in hello Azure classic portal tooadd or modify a schedule.</span></span>

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule.md)]

## <a name="delete-a-backup-policy"></a><span data-ttu-id="6e52a-140">Bir yedekleme ilkesi silme</span><span class="sxs-lookup"><span data-stu-id="6e52a-140">Delete a backup policy</span></span>
<span data-ttu-id="6e52a-141">StorSimple Cihazınızda hello Azure Klasik portalı toodelete bir yedekleme İlkesi adımlarını izleyerek hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="6e52a-141">Perform hello following steps in hello Azure classic portal toodelete a backup policy on your StorSimple device.</span></span>

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a><span data-ttu-id="6e52a-142">El ile yedekleyin</span><span class="sxs-lookup"><span data-stu-id="6e52a-142">Take a manual backup</span></span>
<span data-ttu-id="6e52a-143">Tek bir birim için hello Azure Klasik portalı toocreate isteğe bağlı (el ile) yedekleme adımlarını izleyerek hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="6e52a-143">Perform hello following steps in hello Azure classic portal toocreate an on-demand (manual) backup for a single volume.</span></span>

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a><span data-ttu-id="6e52a-144">Birden çok birimleri ve zamanlamaları özel bir yedekleme ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e52a-144">Create a custom backup policy with multiple volumes and schedules</span></span>
<span data-ttu-id="6e52a-145">Hello Azure Klasik portalı toocreate birden çok birimleri ve zamanlamaları sahip özel bir yedekleme İlkesi adımlarını izleyerek hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="6e52a-145">Perform hello following steps in hello Azure classic portal toocreate a custom backup policy that has multiple volumes and schedules.</span></span>

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy.md)]

## <a name="next-steps"></a><span data-ttu-id="6e52a-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6e52a-146">Next steps</span></span>
<span data-ttu-id="6e52a-147">Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6e52a-147">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

