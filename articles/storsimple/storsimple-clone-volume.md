---
title: StorSimple birim kopyalama | Microsoft Docs
description: "Farklı kopya türlerini ve bunların ne zaman kullanılacağı ve bir yedekleme kümesi bağımsız bir birim kopyalamak için nasıl kullanabileceğiniz açıklanmaktadır."
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
ms.openlocfilehash: 8f1936fac543f559a44ad0f9c35b30d1a92dce68
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-manager-service-to-clone-a-volume"></a><span data-ttu-id="d0072-103">Bir birim kopyalamak için StorSimple Yöneticisi hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="d0072-103">Use the StorSimple Manager service to clone a volume</span></span>
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a><span data-ttu-id="d0072-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d0072-104">Overview</span></span>
<span data-ttu-id="d0072-105">StorSimple Yöneticisi hizmeti **yedekleme kataloğu** sayfası el ile veya otomatik yedeklemeler durumdayken, oluşturulan tüm yedekleme kümelerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d0072-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="d0072-106">Bir yedekleme İlkesi ya da bir birim seçin için tüm yedeklemeler listelemek veya yedekleri de silmek için bu sayfayı kullanın ya da bir yedeği geri yüklemek veya bir birim kopyalamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="d0072-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

![Yedekleme kataloğu sayfası](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

<span data-ttu-id="d0072-108">Bu öğretici, bir yedekleme kümesi bağımsız bir birim kopyalamak için nasıl kullanabileceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="d0072-108">This tutorial describes how you can use a backup set to clone an individual volume.</span></span> <span data-ttu-id="d0072-109">Ayrıca arasındaki farkı açıklar *geçici* ve *kalıcı* klonlar.</span><span class="sxs-lookup"><span data-stu-id="d0072-109">It also explains the difference between *transient* and *permanent* clones.</span></span> 

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="d0072-110">Bir birimin bir kopyasını oluşturun</span><span class="sxs-lookup"><span data-stu-id="d0072-110">Create a clone of a volume</span></span>
<span data-ttu-id="d0072-111">Bir kopya, yerel veya bir bulut anlık görüntüsü kullanarak aynı aygıt, başka bir aygıt veya sanal makine oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0072-111">You can create a clone on the same device, another device, or even a virtual machine by using a local or a cloud snapshot.</span></span>

#### <a name="to-clone-a-volume"></a><span data-ttu-id="d0072-112">Birim kopyalama</span><span class="sxs-lookup"><span data-stu-id="d0072-112">To clone a volume</span></span>
1. <span data-ttu-id="d0072-113">StorSimple Yöneticisi hizmet sayfasında, tıklatın **yedekleme kataloğu** sekmesinde ve bir yedekleme kümesi seçin.</span><span class="sxs-lookup"><span data-stu-id="d0072-113">On the StorSimple Manager service page, click the **Backup catalog** tab and select a backup set.</span></span>
2. <span data-ttu-id="d0072-114">İlişkili birimleri görüntülemek için yedekleme kümesini genişletin.</span><span class="sxs-lookup"><span data-stu-id="d0072-114">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="d0072-115">' I tıklatın ve yedekleme kümesinden bir birim seçin.</span><span class="sxs-lookup"><span data-stu-id="d0072-115">Click and select a volume from the backup set.</span></span>
   
     ![Bir birimi kopyalama](./media/storsimple-clone-volume/HCS_Clone.png) 
3. <span data-ttu-id="d0072-117">Tıklatın **kopya** seçilen birim kopyalamaya başlamak için.</span><span class="sxs-lookup"><span data-stu-id="d0072-117">Click **Clone** to begin cloning the selected volume.</span></span>
4. <span data-ttu-id="d0072-118">Kopya Birim Sihirbazı'nda altında **ad ve konum belirtin**:</span><span class="sxs-lookup"><span data-stu-id="d0072-118">In the Clone Volume wizard, under **Specify name and location**:</span></span>
   
   1. <span data-ttu-id="d0072-119">Bir hedef cihaz tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d0072-119">Identify a target device.</span></span> <span data-ttu-id="d0072-120">Bu, kopyanın oluşturulacağı konumdur.</span><span class="sxs-lookup"><span data-stu-id="d0072-120">This is the location where the clone will be created.</span></span> <span data-ttu-id="d0072-121">Aynı aygıt seçin veya başka bir aygıt belirtin.</span><span class="sxs-lookup"><span data-stu-id="d0072-121">You can choose the same device or specify another device.</span></span> <span data-ttu-id="d0072-122">Diğer bulut hizmeti sağlayıcıları ile ilişkili bir birim seçerseniz (değil Azure), hedef cihaz için aşağı açılan listesi yalnızca fiziksel cihazları gösterir.</span><span class="sxs-lookup"><span data-stu-id="d0072-122">If you choose a volume associated with other cloud service providers (not Azure), the drop-down list for the target device will only show physical devices.</span></span> <span data-ttu-id="d0072-123">Bir sanal cihazdaki diğer bulut hizmeti sağlayıcıları ile ilişkili bir birim kopyalayamıyor.</span><span class="sxs-lookup"><span data-stu-id="d0072-123">You cannot clone a volume associated with other cloud service providers on a virtual device.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="d0072-124">Kopya için gereken kapasiteyi hedef cihazda kullanılabilir kapasiteden daha düşük olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d0072-124">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span></span>
      > 
      > 
   2. <span data-ttu-id="d0072-125">Kopya için benzersiz birim adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="d0072-125">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="d0072-126">Adı 3 ile 127 karakter içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d0072-126">The name must contain between 3 and 127 characters.</span></span>
   3. <span data-ttu-id="d0072-127">Ok simgesine tıklama</span><span class="sxs-lookup"><span data-stu-id="d0072-127">Click the arrow icon</span></span> ![ok simgesi](./media/storsimple-clone-volume/HCS_ArrowIcon.png) <span data-ttu-id="d0072-129">sonraki sayfaya devam etmek için.</span><span class="sxs-lookup"><span data-stu-id="d0072-129">to proceed to the next page.</span></span>
5. <span data-ttu-id="d0072-130">Altında **bu birimi kullanabilir ana bilgisayarları belirleyin**:</span><span class="sxs-lookup"><span data-stu-id="d0072-130">Under **Specify hosts that can use this volume**:</span></span>
   
   1. <span data-ttu-id="d0072-131">Kopya için bir erişim denetimi kaydı (ACR) belirtin.</span><span class="sxs-lookup"><span data-stu-id="d0072-131">Specify an access control record (ACR) for the clone.</span></span> <span data-ttu-id="d0072-132">Yeni bir ACR ekleyebilir veya var olan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="d0072-132">You can add a new ACR or choose from the existing list.</span></span>
   2. <span data-ttu-id="d0072-133">Onay simgesine tıklayarak</span><span class="sxs-lookup"><span data-stu-id="d0072-133">Click the check icon</span></span> ![onay simgesi](./media/storsimple-clone-volume/HCS_CheckIcon.png)<span data-ttu-id="d0072-135">işlemi tamamlamak için.</span><span class="sxs-lookup"><span data-stu-id="d0072-135">to complete the operation.</span></span>
6. <span data-ttu-id="d0072-136">Bir kopya iş başlatılır ve kopya başarıyla oluşturulduğunda size bildirilecek.</span><span class="sxs-lookup"><span data-stu-id="d0072-136">A clone job will be initiated and you will be notified when the clone is successfully created.</span></span> <span data-ttu-id="d0072-137">Tıklatın **işi görüntüle** üzerinde kopya işi izlemek için **işleri** sayfası.</span><span class="sxs-lookup"><span data-stu-id="d0072-137">Click **View Job** to monitor the clone job on the **Jobs** page.</span></span>
7. <span data-ttu-id="d0072-138">Kopyalama işlemi tamamlandıktan sonra:</span><span class="sxs-lookup"><span data-stu-id="d0072-138">After the clone job is completed:</span></span>
   
   1. <span data-ttu-id="d0072-139">Git **aygıtları** sayfasında ve seçin **birim kapsayıcıları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d0072-139">Go to the **Devices** page, and select the **Volume Containers** tab.</span></span> 
   2. <span data-ttu-id="d0072-140">Kopyaladığınız kaynak birimle ilişkilendirilen birim kapsayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="d0072-140">Select the volume container that is associated with the source volume that you cloned.</span></span> <span data-ttu-id="d0072-141">Birimleri listesinde, yeni oluşturduğunuz kopya görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0072-141">In the list of volumes, you should see the clone that was just created.</span></span>

> [!NOTE]
> <span data-ttu-id="d0072-142">İzleme ve varsayılan yedekleme otomatik olarak kopyalanan bir birimde devre dışı.</span><span class="sxs-lookup"><span data-stu-id="d0072-142">Monitoring and default backup are automatically disabled on a cloned volume.</span></span>
> 
> 

<span data-ttu-id="d0072-143">Bu yolla oluşturulan bir kopya geçici kopya ' dir.</span><span class="sxs-lookup"><span data-stu-id="d0072-143">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="d0072-144">Kopya türleri hakkında daha fazla bilgi için bkz: [geçici ve kalıcı klonlar](#transient-vs-permanent-clones).</span><span class="sxs-lookup"><span data-stu-id="d0072-144">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>

<span data-ttu-id="d0072-145">Bu kopya artık normal bir birim ve bir birimde mümkündür herhangi bir işlem için kopya kullanılabilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d0072-145">This clone is now a regular volume, and any operation that is possible on a volume will be available for the clone.</span></span> <span data-ttu-id="d0072-146">Bu birimi tüm yedeklemeler için yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0072-146">You will need to configure this volume for any backups.</span></span>

## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="d0072-147">Geçici ve kalıcı klonlar karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="d0072-147">Transient vs. permanent clones</span></span>
<span data-ttu-id="d0072-148">Yalnızca farklı bir cihaz açın kopyalarken geçici ve kalıcı klonlar oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d0072-148">Transient and permanent clones are created only when you are cloning on to a different device.</span></span> <span data-ttu-id="d0072-149">Yedekleme için farklı bir cihaz kümesi belirli bir birimden kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d0072-149">You can clone a specific volume from a backup set to a different device.</span></span> <span data-ttu-id="d0072-150">Bu yolla oluşturulan bir kopya olduğundan bir *geçici* kopya.</span><span class="sxs-lookup"><span data-stu-id="d0072-150">A clone created in this way is a *transient* clone.</span></span> <span data-ttu-id="d0072-151">Geçici kopya özgün birimin başvuran ve bu birimde yerel olarak yazılırken okumak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="d0072-151">The transient clone will have references to the original volume and will use that volume to read while writing locally.</span></span> 

<span data-ttu-id="d0072-152">Bir geçici kopya bir bulut anlık görüntüsünü sonra sonuçta elde edilen kopya olacak bir *kalıcı* kopya.</span><span class="sxs-lookup"><span data-stu-id="d0072-152">After you take a cloud snapshot of a transient clone, the resulting clone will be a *permanent* clone.</span></span> <span data-ttu-id="d0072-153">Kalıcı kopya bağımsızdır ve tüm başvuruları gelen kopyalandı özgün birimine sahip değil.</span><span class="sxs-lookup"><span data-stu-id="d0072-153">The permanent clone is independent and doesn’t have any references to the original volume that it was cloned from.</span></span>  

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="d0072-154">Geçici ve kalıcı klonlar senaryoları</span><span class="sxs-lookup"><span data-stu-id="d0072-154">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="d0072-155">Aşağıdaki bölümlerde geçici ve kalıcı klonlar kullanılabilir örnek durumlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0072-155">The following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="d0072-156">Geçici bir kopya ile öğe düzeyinde kurtarma</span><span class="sxs-lookup"><span data-stu-id="d0072-156">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="d0072-157">Bir yıl eski Microsoft PowerPoint sunusu dosyası kurtarmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0072-157">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="d0072-158">BT yöneticiniz, o zaman çerçevesi belirli yedekten tanımlar ve birim filtreler.</span><span class="sxs-lookup"><span data-stu-id="d0072-158">Your IT administrator identifies the specific backup from that time frame, and then filters the volume.</span></span> <span data-ttu-id="d0072-159">Yönetici daha sonra birim klonlar, aradığınız dosya bulur ve olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d0072-159">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span></span> <span data-ttu-id="d0072-160">Bu senaryoda, bir geçici kopya kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0072-160">In this scenario, a transient clone is used.</span></span> 

<span data-ttu-id="d0072-161">![Video var](./media/storsimple-clone-volume/Video_icon.png) **Video var**</span><span class="sxs-lookup"><span data-stu-id="d0072-161">![Video available](./media/storsimple-clone-volume/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="d0072-162">Nasıl kopya kullanın ve geri yükleme silinmiş dosyaları kurtarmak için StorSimple özellikleri gösteren bir video izlemek için tıklatın [burada](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="d0072-162">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a><span data-ttu-id="d0072-163">Kalıcı bir kopya ile üretim ortamında test etme</span><span class="sxs-lookup"><span data-stu-id="d0072-163">Testing in the production environment with a permanent clone</span></span>
<span data-ttu-id="d0072-164">Üretim ortamında test hata doğrulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d0072-164">You need to verify a testing bug in the production environment.</span></span> <span data-ttu-id="d0072-165">Üretim ortamında bir bulut bu kopya anlık görüntüsü tarafından birimin bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d0072-165">You create a clone of the volume in the production environment by taking a cloud snapshot of this clone.</span></span> <span data-ttu-id="d0072-166">Kopyalanan birim artık bağımsızdır.</span><span class="sxs-lookup"><span data-stu-id="d0072-166">The cloned volume is now independent.</span></span> <span data-ttu-id="d0072-167">Bu senaryoda, kalıcı bir kopya kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d0072-167">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0072-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0072-168">Next steps</span></span>
* <span data-ttu-id="d0072-169">Bilgi edinmek için nasıl [bir yedeklemek kümesinden StorSimple birimini geri](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="d0072-169">Learn how to [restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="d0072-170">Bilgi edinmek için nasıl [StorSimple Cihazınızı yönetmek için StorSimple Yöneticisi hizmetini kullanma](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d0072-170">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

