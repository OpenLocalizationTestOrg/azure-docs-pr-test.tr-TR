---
title: aaaClone StorSimple biriminiz | Microsoft Docs
description: "Merhaba farklı kopya türlerini açıklar ve ne zaman toouse bunları ve bir yedekleme kümesi tooclone bağımsız bir birim nasıl kullanabileceğinizi açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b5d615f2-02a7-4222-9867-6c0385ce748c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e98d28db1abeb515ba78ab5860e7c5eba0dfcbb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume"></a><span data-ttu-id="e07a3-103">Merhaba StorSimple Yöneticisi hizmet tooclone bir birim kullanın</span><span class="sxs-lookup"><span data-stu-id="e07a3-103">Use hello StorSimple Manager service tooclone a volume</span></span>
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a><span data-ttu-id="e07a3-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="e07a3-104">Overview</span></span>
<span data-ttu-id="e07a3-105">Merhaba StorSimple Yöneticisi hizmeti **yedekleme kataloğu** sayfası el ile veya otomatik yedeklemeler durumdayken, oluşturulan tüm hello yedekleme kümelerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e07a3-105">hello StorSimple Manager service **Backup Catalog** page displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="e07a3-106">Bir yedekleme İlkesi veya bir birim seçin için bu sayfayı toolist tüm hello yedekleri kullanın veya yedeklemeler, silebilir veya yedekleme toorestore kullanın veya bir birim kopyalama.</span><span class="sxs-lookup"><span data-stu-id="e07a3-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

![Yedekleme kataloğu sayfası](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

<span data-ttu-id="e07a3-108">Bu öğretici, bir yedekleme kümesi tooclone bağımsız bir birim nasıl kullanabileceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="e07a3-108">This tutorial describes how you can use a backup set tooclone an individual volume.</span></span> <span data-ttu-id="e07a3-109">Ayrıca hello birbirinden açıklar *geçici* ve *kalıcı* klonlar.</span><span class="sxs-lookup"><span data-stu-id="e07a3-109">It also explains hello difference between *transient* and *permanent* clones.</span></span> 

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="e07a3-110">Bir birimin bir kopyasını oluşturun</span><span class="sxs-lookup"><span data-stu-id="e07a3-110">Create a clone of a volume</span></span>
<span data-ttu-id="e07a3-111">Kopya üzerinde hello oluşturma aynı aygıt, başka bir aygıt veya hatta bir sanal yerel ya da bir bulut anlık görüntüsü kullanarak makine.</span><span class="sxs-lookup"><span data-stu-id="e07a3-111">You can create a clone on hello same device, another device, or even a virtual machine by using a local or a cloud snapshot.</span></span>

#### <a name="tooclone-a-volume"></a><span data-ttu-id="e07a3-112">tooclone bir birim</span><span class="sxs-lookup"><span data-stu-id="e07a3-112">tooclone a volume</span></span>
1. <span data-ttu-id="e07a3-113">Merhaba Hello StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu** sekmesinde ve bir yedekleme kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="e07a3-113">On hello StorSimple Manager service page, click hello **Backup catalog** tab and select a backup set.</span></span>
2. <span data-ttu-id="e07a3-114">Merhaba yedekleme kümesi tooview ilişkili hello birimleri genişletin.</span><span class="sxs-lookup"><span data-stu-id="e07a3-114">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="e07a3-115">' I tıklatın ve hello yedekleme kümesinden bir birim seçin.</span><span class="sxs-lookup"><span data-stu-id="e07a3-115">Click and select a volume from hello backup set.</span></span>
   
     ![Bir birimi kopyalama](./media/storsimple-clone-volume/HCS_Clone.png) 
3. <span data-ttu-id="e07a3-117">Tıklatın **kopya** toobegin seçili hello birim kopyalama.</span><span class="sxs-lookup"><span data-stu-id="e07a3-117">Click **Clone** toobegin cloning hello selected volume.</span></span>
4. <span data-ttu-id="e07a3-118">Merhaba kopya Birim Sihirbazı'nda altında **ad ve konum belirtin**:</span><span class="sxs-lookup"><span data-stu-id="e07a3-118">In hello Clone Volume wizard, under **Specify name and location**:</span></span>
   
   1. <span data-ttu-id="e07a3-119">Bir hedef cihaz tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="e07a3-119">Identify a target device.</span></span> <span data-ttu-id="e07a3-120">Bu hello kopya oluşturulacağı hello konumdur.</span><span class="sxs-lookup"><span data-stu-id="e07a3-120">This is hello location where hello clone will be created.</span></span> <span data-ttu-id="e07a3-121">Merhaba aynı cihaz veya başka bir aygıt belirtmek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e07a3-121">You can choose hello same device or specify another device.</span></span> <span data-ttu-id="e07a3-122">Diğer bulut hizmeti sağlayıcıları ile ilişkili bir birim seçerseniz (değil Azure), hello açılan hello hedef aygıt yalnızca fiziksel cihazlarını göstermeyecektir için liste.</span><span class="sxs-lookup"><span data-stu-id="e07a3-122">If you choose a volume associated with other cloud service providers (not Azure), hello drop-down list for hello target device will only show physical devices.</span></span> <span data-ttu-id="e07a3-123">Bir sanal cihazdaki diğer bulut hizmeti sağlayıcıları ile ilişkili bir birim kopyalayamıyor.</span><span class="sxs-lookup"><span data-stu-id="e07a3-123">You cannot clone a volume associated with other cloud service providers on a virtual device.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="e07a3-124">Merhaba kopyalama için gereken hello kapasite hello hedef cihazda kullanılabilir hello kapasitesinden daha düşük olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e07a3-124">Make sure that hello capacity required for hello clone is lower than hello capacity available on hello target device.</span></span>
      > 
      > 
   2. <span data-ttu-id="e07a3-125">Kopya için benzersiz birim adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="e07a3-125">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="e07a3-126">Merhaba ad 3 ile 127 karakter içermelidir.</span><span class="sxs-lookup"><span data-stu-id="e07a3-126">hello name must contain between 3 and 127 characters.</span></span>
   3. <span data-ttu-id="e07a3-127">Merhaba ok simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="e07a3-127">Click hello arrow icon</span></span> ![ok simgesi](./media/storsimple-clone-volume/HCS_ArrowIcon.png) <span data-ttu-id="e07a3-129">tooproceed toohello sonraki sayfa.</span><span class="sxs-lookup"><span data-stu-id="e07a3-129">tooproceed toohello next page.</span></span>
5. <span data-ttu-id="e07a3-130">Altında **bu birimi kullanabilir ana bilgisayarları belirleyin**:</span><span class="sxs-lookup"><span data-stu-id="e07a3-130">Under **Specify hosts that can use this volume**:</span></span>
   
   1. <span data-ttu-id="e07a3-131">Merhaba kopya için bir erişim denetimi kaydı (ACR) belirtin.</span><span class="sxs-lookup"><span data-stu-id="e07a3-131">Specify an access control record (ACR) for hello clone.</span></span> <span data-ttu-id="e07a3-132">Yeni bir ACR ekleyebilir veya hello varolan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="e07a3-132">You can add a new ACR or choose from hello existing list.</span></span>
   2. <span data-ttu-id="e07a3-133">Merhaba onay simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="e07a3-133">Click hello check icon</span></span> ![onay simgesi](./media/storsimple-clone-volume/HCS_CheckIcon.png)<span data-ttu-id="e07a3-135">toocomplete hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="e07a3-135">toocomplete hello operation.</span></span>
6. <span data-ttu-id="e07a3-136">Bir kopya iş başlatılır ve hello kopya başarıyla oluşturulduğunda size bildirilecek.</span><span class="sxs-lookup"><span data-stu-id="e07a3-136">A clone job will be initiated and you will be notified when hello clone is successfully created.</span></span> <span data-ttu-id="e07a3-137">Tıklatın **işi görüntüle** toomonitor hello kopya hello işinde **işleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="e07a3-137">Click **View Job** toomonitor hello clone job on hello **Jobs** page.</span></span>
7. <span data-ttu-id="e07a3-138">Merhaba sonra kopyalama işi tamamlanır:</span><span class="sxs-lookup"><span data-stu-id="e07a3-138">After hello clone job is completed:</span></span>
   
   1. <span data-ttu-id="e07a3-139">Toohello Git **aygıtları** sayfası ve select hello **birim kapsayıcıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e07a3-139">Go toohello **Devices** page, and select hello **Volume Containers** tab.</span></span> 
   2. <span data-ttu-id="e07a3-140">Kopyaladığınız hello kaynak birimi ile ilişkili hello birim kapsayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="e07a3-140">Select hello volume container that is associated with hello source volume that you cloned.</span></span> <span data-ttu-id="e07a3-141">Birimleri Hello listesinde, yeni oluşturduğunuz hello kopya görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e07a3-141">In hello list of volumes, you should see hello clone that was just created.</span></span>

> [!NOTE]
> <span data-ttu-id="e07a3-142">İzleme ve varsayılan yedekleme otomatik olarak kopyalanan bir birimde devre dışı.</span><span class="sxs-lookup"><span data-stu-id="e07a3-142">Monitoring and default backup are automatically disabled on a cloned volume.</span></span>
> 
> 

<span data-ttu-id="e07a3-143">Bu yolla oluşturulan bir kopya geçici kopya ' dir.</span><span class="sxs-lookup"><span data-stu-id="e07a3-143">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="e07a3-144">Kopya türleri hakkında daha fazla bilgi için bkz: [geçici ve kalıcı klonlar](#transient-vs-permanent-clones).</span><span class="sxs-lookup"><span data-stu-id="e07a3-144">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>

<span data-ttu-id="e07a3-145">Bu kopya artık normal bir birim ve bir birimde mümkündür herhangi bir işlem hello kopya için kullanılabilir olacak.</span><span class="sxs-lookup"><span data-stu-id="e07a3-145">This clone is now a regular volume, and any operation that is possible on a volume will be available for hello clone.</span></span> <span data-ttu-id="e07a3-146">Bu birimi tooconfigure tüm yedeklemeler için gerekir.</span><span class="sxs-lookup"><span data-stu-id="e07a3-146">You will need tooconfigure this volume for any backups.</span></span>

## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="e07a3-147">Geçici ve kalıcı klonlar karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="e07a3-147">Transient vs. permanent clones</span></span>
<span data-ttu-id="e07a3-148">Yalnızca tooa farklı aygıtta kopyalarken geçici ve kalıcı klonlar oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e07a3-148">Transient and permanent clones are created only when you are cloning on tooa different device.</span></span> <span data-ttu-id="e07a3-149">Yedekleme kümesi tooa farklı bir cihaz belirli bir birimden kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e07a3-149">You can clone a specific volume from a backup set tooa different device.</span></span> <span data-ttu-id="e07a3-150">Bu yolla oluşturulan bir kopya olduğundan bir *geçici* kopya.</span><span class="sxs-lookup"><span data-stu-id="e07a3-150">A clone created in this way is a *transient* clone.</span></span> <span data-ttu-id="e07a3-151">Merhaba geçici kopya başvuruları toohello özgün birimin sahip olur ve bu birimi tooread yerel olarak yazılırken kullanır.</span><span class="sxs-lookup"><span data-stu-id="e07a3-151">hello transient clone will have references toohello original volume and will use that volume tooread while writing locally.</span></span> 

<span data-ttu-id="e07a3-152">Bir geçici kopya bir bulut anlık görüntüsünü sonra hello elde edilen kopya olacak bir *kalıcı* kopya.</span><span class="sxs-lookup"><span data-stu-id="e07a3-152">After you take a cloud snapshot of a transient clone, hello resulting clone will be a *permanent* clone.</span></span> <span data-ttu-id="e07a3-153">Merhaba kalıcı kopya bağımsızdır ve gelen kopyalandı tüm başvuruları toohello özgün birim yok.</span><span class="sxs-lookup"><span data-stu-id="e07a3-153">hello permanent clone is independent and doesn’t have any references toohello original volume that it was cloned from.</span></span>  

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="e07a3-154">Geçici ve kalıcı klonlar senaryoları</span><span class="sxs-lookup"><span data-stu-id="e07a3-154">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="e07a3-155">Aşağıdaki bölümlerde hello geçici ve kalıcı klonlar kullanılabilir örnek durumlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e07a3-155">hello following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="e07a3-156">Geçici bir kopya ile öğe düzeyinde kurtarma</span><span class="sxs-lookup"><span data-stu-id="e07a3-156">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="e07a3-157">Toorecover bir yıl eski Microsoft PowerPoint sunusu dosyası gerekir.</span><span class="sxs-lookup"><span data-stu-id="e07a3-157">You need toorecover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="e07a3-158">BT yöneticiniz hello belirli o zaman çerçevesi yedekten tanımlar ve ardından birim filtreleri hello.</span><span class="sxs-lookup"><span data-stu-id="e07a3-158">Your IT administrator identifies hello specific backup from that time frame, and then filters hello volume.</span></span> <span data-ttu-id="e07a3-159">Hello Yöneticisi sonra hello birim klonlar, aradığınız hello dosyayı bulur ve tooyou sağlar.</span><span class="sxs-lookup"><span data-stu-id="e07a3-159">hello administrator then clones hello volume, locates hello file that you are looking for, and provides it tooyou.</span></span> <span data-ttu-id="e07a3-160">Bu senaryoda, bir geçici kopya kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e07a3-160">In this scenario, a transient clone is used.</span></span> 

<span data-ttu-id="e07a3-161">![Video var](./media/storsimple-clone-volume/Video_icon.png) **Video var**</span><span class="sxs-lookup"><span data-stu-id="e07a3-161">![Video available](./media/storsimple-clone-volume/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="e07a3-162">toowatch nasıl hello kopya kullanın ve geri yükleme StorSimple silinmiş toorecover dosyalarında özellikleri gösteren bir video tıklatın [burada](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="e07a3-162">toowatch a video that demonstrates how you can use hello clone and restore features in StorSimple toorecover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a><span data-ttu-id="e07a3-163">Kalıcı bir kopya ile Merhaba üretim ortamında test etme</span><span class="sxs-lookup"><span data-stu-id="e07a3-163">Testing in hello production environment with a permanent clone</span></span>
<span data-ttu-id="e07a3-164">Tooverify hello üretim ortamında test hata gerekir.</span><span class="sxs-lookup"><span data-stu-id="e07a3-164">You need tooverify a testing bug in hello production environment.</span></span> <span data-ttu-id="e07a3-165">Bir bulut bu kopya anlık görüntüsü tarafından hello üretim ortamında hello birimin bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e07a3-165">You create a clone of hello volume in hello production environment by taking a cloud snapshot of this clone.</span></span> <span data-ttu-id="e07a3-166">Merhaba kopyalanan birim artık bağımsızdır.</span><span class="sxs-lookup"><span data-stu-id="e07a3-166">hello cloned volume is now independent.</span></span> <span data-ttu-id="e07a3-167">Bu senaryoda, kalıcı bir kopya kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e07a3-167">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e07a3-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e07a3-168">Next steps</span></span>
* <span data-ttu-id="e07a3-169">Nasıl çok öğrenin[bir yedeklemek kümesinden StorSimple birimini geri](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="e07a3-169">Learn how too[restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="e07a3-170">Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="e07a3-170">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

