---
title: StorSimple 8000 serisi bir birimde aaaClone | Microsoft Docs
description: "Merhaba farklı kopya türleri ve kullanım ve bir yedekleme kümesi tooclone bağımsız bir birim bir StorSimple 8000 serisi cihazda nasıl kullanabileceğiniz açıklanmaktadır."
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
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 4f7e1f62f17c7b2bd72820a00a5ab87b7e192332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-tooclone-a-volume"></a><span data-ttu-id="c468c-103">Azure portal tooclone bir birim Hello StorSimple cihaz Yöneticisi hizmetini kullanma</span><span class="sxs-lookup"><span data-stu-id="c468c-103">Use hello StorSimple Device Manager service in Azure portal tooclone a volume</span></span>

## <a name="overview"></a><span data-ttu-id="c468c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c468c-104">Overview</span></span>

<span data-ttu-id="c468c-105">Bu öğretici bir yedekleme kümesi tooclone hello aracılığıyla tek bir birim nasıl kullanabileceğinizi açıklar **yedekleme kataloğu** dikey.</span><span class="sxs-lookup"><span data-stu-id="c468c-105">This tutorial describes how you can use a backup set tooclone an individual volume via hello **Backup catalog** blade.</span></span> <span data-ttu-id="c468c-106">Ayrıca hello birbirinden açıklar *geçici* ve *kalıcı* klonlar.</span><span class="sxs-lookup"><span data-stu-id="c468c-106">It also explains hello difference between *transient* and *permanent* clones.</span></span> <span data-ttu-id="c468c-107">Bu öğreticide Hello yönerge güncelleştirme 3 veya üstünü çalıştıran tooall hello StorSimple 8000 serisi aygıt geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c468c-107">hello guidance in this tutorial applies tooall hello StorSimple 8000 series device running Update 3 or later.</span></span>

<span data-ttu-id="c468c-108">Merhaba StorSimple cihaz Yöneticisi hizmeti **yedekleme kataloğu** dikey penceresinde el ile veya otomatik yedeklemeler durumdayken, oluşturulan tüm hello yedekleme kümelerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="c468c-108">hello StorSimple Device Manager service **Backup catalog** blade displays all hello backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="c468c-109">Ardından, bir birim bir yedekleme kümesi tooclone seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c468c-109">You can then select a volume in a backup set tooclone.</span></span>

 ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a><span data-ttu-id="c468c-111">Bir birim kopyalama dikkat edilmesi gereken noktalar</span><span class="sxs-lookup"><span data-stu-id="c468c-111">Considerations for cloning a volume</span></span>

<span data-ttu-id="c468c-112">Bir birim kopyalarken aşağıdaki bilgilerle hello göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="c468c-112">Consider hello following information when cloning a volume.</span></span>

- <span data-ttu-id="c468c-113">Bir kopya hello aynı şekilde davranır normal bir birim olarak yolu.</span><span class="sxs-lookup"><span data-stu-id="c468c-113">A clone behaves in hello same way as a regular volume.</span></span> <span data-ttu-id="c468c-114">Bir birimde mümkündür herhangi bir işlem hello kopya için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c468c-114">Any operation that is possible on a volume is available for hello clone.</span></span>

- <span data-ttu-id="c468c-115">İzleme ve varsayılan yedekleme otomatik olarak kopyalanan bir birimde devre dışı.</span><span class="sxs-lookup"><span data-stu-id="c468c-115">Monitoring and default backup are automatically disabled on a cloned volume.</span></span> <span data-ttu-id="c468c-116">Tüm yedeklemeler için tooconfigure kopyalanan birim gerekir.</span><span class="sxs-lookup"><span data-stu-id="c468c-116">You would need tooconfigure a cloned volume for any backups.</span></span>

- <span data-ttu-id="c468c-117">Yerel olarak sabitlenmiş bir birim katmanlı birim kopyalandı.</span><span class="sxs-lookup"><span data-stu-id="c468c-117">A locally pinned volume is cloned as a tiered volume.</span></span> <span data-ttu-id="c468c-118">Yerel olarak sabitlenmiş kopyalanan birim toobe hello varsa, başlangıç kopyalama işlemi başarıyla tamamlandıktan sonra hello kopya tooa yerel olarak sabitlenmiş birim dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c468c-118">If you need hello cloned volume toobe locally pinned, you can convert hello clone tooa locally pinned volume after hello clone operation is successfully completed.</span></span> <span data-ttu-id="c468c-119">Çok katmanlı birim tooa yerel olarak dönüştürme hakkında bilgi sabitlenmiş birim için Git[değiştirmek hello birim türü](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span><span class="sxs-lookup"><span data-stu-id="c468c-119">For information about converting a tiered volume tooa locally pinned volume, go too[Change hello volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span>

- <span data-ttu-id="c468c-120">(Bunu yine bir geçici kopya olduğunda) hemen kopyalandıktan sonra katmanlı toolocally kopyalanan bir birimden sabitlenmiş tooconvert deneyin hello dönüştürme hello aşağıdaki hata iletisi ile başarısız olur:</span><span class="sxs-lookup"><span data-stu-id="c468c-120">If you try tooconvert a cloned volume from tiered toolocally pinned immediately after cloning (when it is still a transient clone), hello conversion fails with hello following error message:</span></span>

    `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.`

    <span data-ttu-id="c468c-121">Yalnızca tooa farklı cihazda kopyalama, bu hata alınır.</span><span class="sxs-lookup"><span data-stu-id="c468c-121">This error is received only if you are cloning on tooa different device.</span></span> <span data-ttu-id="c468c-122">Merhaba geçici kopya tooa kalıcı kopya ilk dönüştürürseniz sabitlenmiş hello birim toolocally başarıyla dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c468c-122">You can successfully convert hello volume toolocally pinned if you first convert hello transient clone tooa permanent clone.</span></span> <span data-ttu-id="c468c-123">Merhaba geçici kopya tooconvert bir bulut anlık görüntüsünü, tooa kalıcı kopya.</span><span class="sxs-lookup"><span data-stu-id="c468c-123">Take a cloud snapshot of hello transient clone tooconvert it tooa permanent clone.</span></span>

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="c468c-124">Bir birimin bir kopyasını oluşturun</span><span class="sxs-lookup"><span data-stu-id="c468c-124">Create a clone of a volume</span></span>

<span data-ttu-id="c468c-125">Kopya oluşturma hello aynı aygıt, başka bir aygıt veya Bulut uygulaması yerel kullanarak veya Bulut anlık görüntü.</span><span class="sxs-lookup"><span data-stu-id="c468c-125">You can create a clone on hello same device, another device, or even a cloud appliance by using a local or cloud snapshot.</span></span>

<span data-ttu-id="c468c-126">Aşağıdaki Hello yordamı nasıl toocreate hello bir kopya yedekleme kataloğu açıklar.</span><span class="sxs-lookup"><span data-stu-id="c468c-126">hello procedure below describes how toocreate a clone from hello backup catalog.</span></span>  <span data-ttu-id="c468c-127">Alternatif yöntem tooinitiate kopya toogo çok uzun**birimleri**bir birim seçin, sonra tooinvoke hello bağlam menüsü sağ tıklatın ve seçin **kopya**.</span><span class="sxs-lookup"><span data-stu-id="c468c-127">An alternative method tooinitiate clone is toogo too**Volumes**, select a volume, then right-click tooinvoke hello context menu and select **Clone**.</span></span>

<span data-ttu-id="c468c-128">Merhaba yedekleme Kataloğu'ndan adımları toocreate biriminiz kopyasını aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c468c-128">Perform hello following steps toocreate a clone of your volume from hello backup catalog.</span></span>

#### <a name="tooclone-a-volume"></a><span data-ttu-id="c468c-129">tooclone bir birim</span><span class="sxs-lookup"><span data-stu-id="c468c-129">tooclone a volume</span></span>

1. <span data-ttu-id="c468c-130">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve ardından **yedekleme kataloğu**.</span><span class="sxs-lookup"><span data-stu-id="c468c-130">Go tooyour StorSimple Device Manager service and then click **Backup catalog**.</span></span>

2. <span data-ttu-id="c468c-131">Bir yedekleme kümesi aşağıdaki gibi seçin:</span><span class="sxs-lookup"><span data-stu-id="c468c-131">Select a backup set as follows:</span></span>
   
   1. <span data-ttu-id="c468c-132">Merhaba uygun cihazı seçin.</span><span class="sxs-lookup"><span data-stu-id="c468c-132">Select hello appropriate device.</span></span>
   2. <span data-ttu-id="c468c-133">Merhaba aşağı açılan listesinde, tooselect istediğiniz hello yedekleme için hello birim veya yedekleme ilkesini seçin.</span><span class="sxs-lookup"><span data-stu-id="c468c-133">In hello drop-down list, choose hello volume or backup policy for hello backup that you wish tooselect.</span></span>
   3. <span data-ttu-id="c468c-134">Merhaba zaman aralığı belirtin.</span><span class="sxs-lookup"><span data-stu-id="c468c-134">Specify hello time range.</span></span>
   4. <span data-ttu-id="c468c-135">Tıklatın **Uygula** tooexecute bu sorgu.</span><span class="sxs-lookup"><span data-stu-id="c468c-135">Click **Apply** tooexecute this query.</span></span>

    <span data-ttu-id="c468c-136">Merhaba seçili hello birim veya yedekleme ilkesiyle ilişkili yedeklemeler yedekleme kümelerini hello listesinde görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="c468c-136">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>
   
    ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. <span data-ttu-id="c468c-138">Merhaba yedekleme kümesi tooview ilişkili hello birimleri genişletin.</span><span class="sxs-lookup"><span data-stu-id="c468c-138">Expand hello backup set tooview hello associated volumes.</span></span> <span data-ttu-id="c468c-139">Geri yüklemeden önce bu birimleri hello ana bilgisayar ve aygıt çevrimdışına alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c468c-139">These volumes must be taken offline on hello host and device before you can restore them.</span></span> <span data-ttu-id="c468c-140">Erişim hello hello birimlerde **birimleri** dikey cihaz ve ardından izleme hello adımları [bir birim çevrimdışına](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake çevrimdışı.</span><span class="sxs-lookup"><span data-stu-id="c468c-140">Access hello volumes on hello **Volumes** blade of your device, and then follow hello steps in [Take a volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake them offline.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="c468c-141">Merhaba aygıtta çevrimdışı hello birimleri olabilmesi hello birimlerde çevrimdışı hello konak ilk olarak, gerçekleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="c468c-141">Make sure that you have taken hello volumes offline on hello host first, before you take hello volumes offline on hello device.</span></span> <span data-ttu-id="c468c-142">Merhaba konakta çevrimdışı hello birimleri almazsanız, büyük olasılıkla toodata bozulmasına yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="c468c-142">If you do not take hello volumes offline on hello host, it could potentially lead toodata corruption.</span></span>
   
4. <span data-ttu-id="c468c-143">Geri toohello gidin **yedekleme kataloğu** ve yedekleme kümesinde bir birim seçin.</span><span class="sxs-lookup"><span data-stu-id="c468c-143">Navigate back toohello **Backup catalog** and select a volume in a backup set.</span></span> <span data-ttu-id="c468c-144">Sağ tıklayın ve ardından hello bağlam menüsünden seçin **kopya**.</span><span class="sxs-lookup"><span data-stu-id="c468c-144">Right-click and then from hello context menu, select **Clone**.</span></span>

   ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. <span data-ttu-id="c468c-146">Merhaba, **kopya** dikey penceresinde, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="c468c-146">In hello **Clone** blade, do hello following steps:</span></span>
   
    1. <span data-ttu-id="c468c-147">Bir hedef cihaz tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c468c-147">Identify a target device.</span></span> <span data-ttu-id="c468c-148">Bu hello kopya oluşturulacağı hello konumdur.</span><span class="sxs-lookup"><span data-stu-id="c468c-148">This is hello location where hello clone will be created.</span></span> <span data-ttu-id="c468c-149">Merhaba aynı cihaz veya başka bir aygıt belirtmek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c468c-149">You can choose hello same device or specify another device.</span></span>

      > [!NOTE]
      > <span data-ttu-id="c468c-150">Merhaba kopyalama için gereken hello kapasite hello hedef cihazda kullanılabilir hello kapasitesinden daha düşük olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="c468c-150">Make sure that hello capacity required for hello clone is lower than hello capacity available on hello target device.</span></span>
       
    2. <span data-ttu-id="c468c-151">Kopya için benzersiz birim adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="c468c-151">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="c468c-152">Merhaba ad 3 ile 127 karakter içermelidir.</span><span class="sxs-lookup"><span data-stu-id="c468c-152">hello name must contain between 3 and 127 characters.</span></span>
      
        > [!NOTE]
        > <span data-ttu-id="c468c-153">Merhaba **kopya birim olarak** alan **katmanlı** yerel olarak sabitlenmiş bir birim kopyalama olsa bile.</span><span class="sxs-lookup"><span data-stu-id="c468c-153">hello **Clone Volume As** field will be **Tiered** even if you are cloning a locally pinned volume.</span></span> <span data-ttu-id="c468c-154">Bu ayarı değiştiremezsiniz; Bununla birlikte, kopyalanan birim toobe de yerel olarak sabitlenmiş hello varsa, hello kopya başarıyla oluşturduktan sonra hello kopya tooa yerel olarak sabitlenmiş birim dönüştürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c468c-154">You cannot change this setting; however, if you need hello cloned volume toobe locally pinned as well, you can convert hello clone tooa locally pinned volume after you successfully create hello clone.</span></span> <span data-ttu-id="c468c-155">Çok katmanlı birim tooa yerel olarak dönüştürme hakkında bilgi sabitlenmiş birim için Git[değiştirmek hello birim türü](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span><span class="sxs-lookup"><span data-stu-id="c468c-155">For information about converting a tiered volume tooa locally pinned volume, go too[Change hello volume type](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).</span></span>
          
    3. <span data-ttu-id="c468c-156">Altında **bağlı Konaklar**, hello kopya için bir erişim denetimi kaydı (ACR) belirtin.</span><span class="sxs-lookup"><span data-stu-id="c468c-156">Under **Connected hosts**, specify an access control record (ACR) for hello clone.</span></span> <span data-ttu-id="c468c-157">Yeni bir ACR ekleyebilir veya hello varolan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="c468c-157">You can add a new ACR or choose from hello existing list.</span></span> <span data-ttu-id="c468c-158">Merhaba ACR hangi ana bilgisayarların bu kopya erişebilirsiniz belirler.</span><span class="sxs-lookup"><span data-stu-id="c468c-158">hello ACR will determine which hosts can access this clone.</span></span>
      
        ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. <span data-ttu-id="c468c-160">Tıklatın **kopya** toocomplete hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="c468c-160">Click **Clone** toocomplete hello operation.</span></span>

4. <span data-ttu-id="c468c-161">Bir kopya iş başlatılır ve hello kopya başarıyla oluşturulduğunda size bildirilir.</span><span class="sxs-lookup"><span data-stu-id="c468c-161">A clone job is initiated and you are notified when hello clone is successfully created.</span></span> <span data-ttu-id="c468c-162">Merhaba iş bildirimi tıklatın ya da çok Git**işleri** dikey toomonitor hello kopyalama işi.</span><span class="sxs-lookup"><span data-stu-id="c468c-162">Click hello job notification or go too**Jobs** blade toomonitor hello clone job.</span></span>

    ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. <span data-ttu-id="c468c-164">Merhaba kopya işi tamamlandıktan sonra tooyour aygıt gidin ve ardından **birimleri**.</span><span class="sxs-lookup"><span data-stu-id="c468c-164">After hello clone job is complete, go tooyour device and then click **Volumes**.</span></span> <span data-ttu-id="c468c-165">Birimleri Hello listesinde hello aynı az önce oluşturulan hello kopya görmelisiniz hello kaynak biriminin birim kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="c468c-165">In hello list of volumes, you should see hello clone that was just created in hello same volume container that has hello source volume.</span></span>

    ![Yedekleme kümesi listesi](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

<span data-ttu-id="c468c-167">Bu yolla oluşturulan bir kopya geçici kopya ' dir.</span><span class="sxs-lookup"><span data-stu-id="c468c-167">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="c468c-168">Kopya türleri hakkında daha fazla bilgi için bkz: [geçici ve kalıcı klonlar](#transient-vs-permanent-clones).</span><span class="sxs-lookup"><span data-stu-id="c468c-168">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>


## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="c468c-169">Geçici ve kalıcı klonlar karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="c468c-169">Transient vs. permanent clones</span></span>
<span data-ttu-id="c468c-170">Yalnızca tooanother aygıt kopyaladığınızda geçici klonlar oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c468c-170">Transient clones are created only when you clone tooanother device.</span></span> <span data-ttu-id="c468c-171">Merhaba StorSimple cihaz Yöneticisi tarafından yönetilen bir yedekleme kümesi tooa farklı bir cihaz belirli bir birimden kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c468c-171">You can clone a specific volume from a backup set tooa different device managed by hello StorSimple Device Manager.</span></span> <span data-ttu-id="c468c-172">Merhaba geçici kopya hello özgün birimin başvuruları toohello veri vardır ve bu verileri tooread ve yazma hello hedef cihazda yerel olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="c468c-172">hello transient clone has references toohello data in hello original volume and uses that data tooread and write locally on hello target device.</span></span>

<span data-ttu-id="c468c-173">Bir geçici kopya bir bulut anlık görüntüsünü sonra hello elde edilen kopya olan bir *kalıcı* kopya.</span><span class="sxs-lookup"><span data-stu-id="c468c-173">After you take a cloud snapshot of a transient clone, hello resulting clone is a *permanent* clone.</span></span> <span data-ttu-id="c468c-174">Bu işlem sırasında hello verilerin bir kopyasını hello Bulutu üzerinde oluşturulur ve bu verileri hello veri hello boyutu tarafından belirlenir zaman toocopy hello ve (bir Azure Azure kopyalama budur) Azure gecikmeleri hello.</span><span class="sxs-lookup"><span data-stu-id="c468c-174">During this process, a copy of hello data is created on hello cloud and hello time toocopy this data is determined by hello size of hello data and hello Azure latencies (this is an Azure-to-Azure copy).</span></span> <span data-ttu-id="c468c-175">Bu işlem gün tooweeks alabilir.</span><span class="sxs-lookup"><span data-stu-id="c468c-175">This process can take days tooweeks.</span></span> <span data-ttu-id="c468c-176">Merhaba geçici kopya kalıcı bir kopya olur ve gelen kopyalandı tüm başvuruları toohello özgün birimin verileri yok.</span><span class="sxs-lookup"><span data-stu-id="c468c-176">hello transient clone becomes a permanent clone and doesn’t have any references toohello original volume data that it was cloned from.</span></span>

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="c468c-177">Geçici ve kalıcı klonlar senaryoları</span><span class="sxs-lookup"><span data-stu-id="c468c-177">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="c468c-178">Aşağıdaki bölümlerde hello geçici ve kalıcı klonlar kullanılabilir örnek durumlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c468c-178">hello following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="c468c-179">Geçici bir kopya ile öğe düzeyinde kurtarma</span><span class="sxs-lookup"><span data-stu-id="c468c-179">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="c468c-180">Toorecover bir yıl eski Microsoft PowerPoint sunusu dosyası gerekir.</span><span class="sxs-lookup"><span data-stu-id="c468c-180">You need toorecover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="c468c-181">BT yöneticiniz hello belirli saat yedekten tanımlar ve ardından birim filtreleri hello.</span><span class="sxs-lookup"><span data-stu-id="c468c-181">Your IT administrator identifies hello specific backup from that time, and then filters hello volume.</span></span> <span data-ttu-id="c468c-182">Hello Yöneticisi sonra hello birim klonlar, aradığınız hello dosyayı bulur ve tooyou sağlar.</span><span class="sxs-lookup"><span data-stu-id="c468c-182">hello administrator then clones hello volume, locates hello file that you are looking for, and provides it tooyou.</span></span> <span data-ttu-id="c468c-183">Bu senaryoda, bir geçici kopya kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c468c-183">In this scenario, a transient clone is used.</span></span>

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a><span data-ttu-id="c468c-184">Kalıcı bir kopya ile Merhaba üretim ortamında test etme</span><span class="sxs-lookup"><span data-stu-id="c468c-184">Testing in hello production environment with a permanent clone</span></span>
<span data-ttu-id="c468c-185">Tooverify hello üretim ortamında test hata gerekir.</span><span class="sxs-lookup"><span data-stu-id="c468c-185">You need tooverify a testing bug in hello production environment.</span></span> <span data-ttu-id="c468c-186">Merhaba üretim ortamında hello birimin bir kopyasını oluşturun ve sonra bu kopya toocreate bağımsız kopyalanan birimin bir bulut anlık görüntüsünü.</span><span class="sxs-lookup"><span data-stu-id="c468c-186">You create a clone of hello volume in hello production environment and then take a cloud snapshot of this clone toocreate an independent cloned volume.</span></span> <span data-ttu-id="c468c-187">Bu senaryoda, kalıcı bir kopya kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c468c-187">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c468c-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c468c-188">Next steps</span></span>
* <span data-ttu-id="c468c-189">Nasıl çok öğrenin[bir yedeklemek kümesinden StorSimple birimini geri](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="c468c-189">Learn how too[restore a StorSimple volume from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="c468c-190">Nasıl çok öğrenin[kullanım StorSimple Cihazınızı StorSimple cihaz Yöneticisi hizmeti tooadminister hello](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="c468c-190">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

